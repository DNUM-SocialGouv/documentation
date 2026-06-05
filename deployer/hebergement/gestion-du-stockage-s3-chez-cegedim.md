# Gestion du stockage S3 chez CEGEDIM

### 1. Le message principal à retenir

L'offre de stockage Cegedim est un service brut. Tout fonctionne dès la livraison, mais **aucune protection contre la perte de données n'est activée par défaut**.

Concrètement avec la version par défaut :

* Si un développeur, un script ou un attaquant supprime un fichier, **il est perdu définitivement**.
* Si un fichier est écrasé par un autre du même nom, **l'ancien est perdu**.
* La **géo-réplication entre Boulogne et Toulouse** (si elle est souscrite) protège uniquement contre la perte d'un datacenter — **elle ne protège pas contre les suppressions accidentelles** (elles sont répliquées dans les deux sites).

La protection des données est donc une **responsabilité du projet**, pas de Cegedim.

Dans la suite de ce document, nous allons présenter les différentes décisions à prendre, à quel moment du projet, et avec quel niveau d'irréversibilité.

***

### 2. Ce que Cegedim livre par défaut

📄 _Doc. Cegedim :_ [_Démarrer avec l'Object Storage_](https://academy.cegedim.cloud/storage/object-storage/object-storage-get-started) _et_ [_Limitations et bonnes pratiques_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/limitation-and-best-practices)

#### Ce qui fonctionne tout seul

| Élément                                                    | Niveau                              |
| ---------------------------------------------------------- | ----------------------------------- |
| Stockage S3 standard, accessible via les outils du marché  | ✅ Inclus                            |
| Chiffrement automatique des données (transit et au repos)  | ✅ Inclus, transparent               |
| Haute disponibilité matérielle (pannes disque, redondance) | ✅ Inclus                            |
| Géo-réplication active/active Boulogne ↔ Toulouse          | ✅ Optionnel (à souscrire)           |
| Logs internes des opérations (qui a fait quoi, quand)      | ✅ Conservés en interne chez Cegedim |

#### Ce qui n'est PAS livré et qui doit être activé par le projet

| Risque                                                              | Couvert par défaut ?                 |
| ------------------------------------------------------------------- | ------------------------------------ |
| Suppression accidentelle d'un fichier                               | ❌ Non                                |
| Écrasement involontaire (PUT sur un nom existant)                   | ❌ Non                                |
| Bug applicatif qui purge ou écrase massivement                      | ❌ Non                                |
| Suppression malveillante (clé d'accès compromise)                   | ❌ Non                                |
| Conformité légale (archive immuable, RGPD long terme)               | ❌ Non                                |
| Sauvegarde de secours (type "snapshot quotidien")                   | ❌ Non, **aucune** sauvegarde native  |
| Accès à ses propres logs en self-service                            | ❌ Non, passer par un ticket support  |
| Notifications événementielles (alerter une appli sur un PUT/DELETE) | ❌ Non, fonctionnalité non disponible |

> ⚠️ **Point structurant** : Cegedim confirme noir sur blanc dans sa documentation qu'il n'y a **pas de capacité de sauvegarde native**. Si un fichier est perdu, il est perdu. Toute protection doit être configurée en amont. [📄 Source](https://academy.cegedim.cloud/storage/object-storage/object-storage-get-started/manage-versioning-in-bucket)

***

### 3. Les leviers disponibles pour les projets

📄 _Doc. Cegedim :_ [_Fonctionnalités de l'Object Storage_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features)

#### 3.1 Versioning de bucket — la protection de base

📄 _Doc. Cegedim :_ [_Gérer le versioning d'un bucket_](https://academy.cegedim.cloud/storage/object-storage/object-storage-get-started/manage-versioning-in-bucket)

**À quoi ça sert** : conserver toutes les versions successives d'un fichier. Une suppression ne supprime plus réellement le fichier, elle pose un "drapeau de suppression" que l'on peut retirer pour restaurer.

**Ce que ça protège** : suppression accidentelle, écrasement involontaire, bug applicatif simple.

**Ce que ça ne protège PAS** : un attaquant qui possède les clés d'accès peut, en plus, supprimer les versions historiques une par une.

**Points d'attention** :

* Activation rapide, sans interruption de service, sur un bucket déjà en production.
* **Choix irréversible** : une fois activé, on ne peut plus le désactiver, seulement le _suspendre_.
* **Surcoût de stockage** : on paie l'espace pris par toutes les versions conservées → à coupler obligatoirement avec une règle de purge (voir 3.3).

#### 3.2 Object Lock — l'immuabilité pour la conformité

📄 _Doc. Cegedim :_ [_Object Lock_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/object-lock)

**À quoi ça sert** : empêcher physiquement la suppression ou la modification d'un fichier pendant une durée définie (jours, mois, années). Aucune intervention possible avant l'échéance, **même pas par Cegedim**.

**Ce que ça protège** : conformité réglementaire (archivage légal, données RGPD long terme, données médicales), protection absolue contre une compromission de clés d'accès.

**Deux modes existent** :

| Mode           | Niveau de blocage                                                                     | Quand l'utiliser                                                                                              |
| -------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **GOVERNANCE** | Bloque tout le monde **sauf** un compte avec une permission spéciale de contournement | Tests, pilote, périmètres où une exception reste possible. Pendant les phases de développement, preprod, etc. |
| **COMPLIANCE** | Bloque **absolument tout le monde, y compris Cegedim**. Aucun retour arrière          | Archive légale, exigence réglementaire formelle                                                               |

**Points d'attention — CRITIQUES** :

* 🛑 **Activable uniquement à la création d'un bucket**. Impossible d'ajouter Object Lock sur un bucket existant. → À décider **avant** la création.
* 🛑 **Demande Cegedim manuelle obligatoire** : l'Object Store doit avoir une option spéciale désactivée (« ADO »), ce qui **n'est pas possible via le portail self-service ITCare**. Il faut **ouvrir un ticket** auprès de Cegedim. Compter plusieurs jours.
* 🛑 **Effet de bord de cette option** : sans ADO, **si un datacenter tombe, les opérations échouent** (la résilience cross-DC transparente est désactivée). À arbitrer.
* 🛑 **Piège du mode COMPLIANCE** : une erreur de saisie (6 ans au lieu de 6 jours) = données figées 6 ans, sans recours possible. **Toujours valider d'abord en GOVERNANCE**, puis basculer en COMPLIANCE uniquement après validation complète.

#### 3.3 Lifecycle — purge automatique des fichiers

📄 _Doc. Cegedim :_ [_Bucket Lifecycle_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/bucket-lifecycle)

**À quoi ça sert** : supprimer automatiquement des fichiers selon des règles (âge, ancienneté de version, etc.). Sert principalement à **maîtriser le coût du versioning** en purgeant les versions trop anciennes.

**Points d'attention** :

* ⚠️ Une suppression par lifecycle est **définitive** (sauf si Object Lock activé).
* Cegedim ne propose **que la suppression** : pas de transition vers du stockage "froid" moins cher (pas d'équivalent du service Glacier d'AWS).
* Mécanisme asynchrone : un fichier marqué "à expirer" peut subsister 24–48h après l'échéance théorique.

#### 3.4 Bucket Policies — restreindre les accès

_📄 Doc. Cegedim :_ [_Bucket Policies_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/bucket-policies) _et_ [_Gérer les accès à un bucket_](https://academy.cegedim.cloud/storage/object-storage/object-storage-get-started/manage-bucket-access)

**À quoi ça sert** : poser des règles d'accès au niveau d'un bucket :

* N'autoriser que certaines plages d'adresses IP (typiquement, le réseau interne uniquement).
* Réserver un bucket en lecture seule à certaines applications.
* Au contraire, rendre publiquement accessible (à manier avec extrême prudence).

**Points d'attention** :

* Très puissant et **gratuit** (pas de surcoût).
* Le filtrage par IP **ne fonctionne qu'en IPv4** (limitation Cegedim).
* Une policy mal rédigée peut soit **bloquer toute l'application**, soit **exposer publiquement le bucket**. À faire revoir.

#### 3.5 Presigned URLs — partage temporaire sans clé

📄 _Doc. Cegedim :_ [_Presigned URL_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/presigned-url)

**À quoi ça sert** : générer une URL "à durée limitée" pour qu'un partenaire externe ou un utilisateur final accède à un fichier, sans lui donner les clés d'accès au système.

**Points d'attention** :

* Durée maximale : **7 jours**.
* Une URL d'upload pointant sur un nom de fichier existant **écrase l'original** → activer le versioning en parallèle.

#### 3.6 Géo-réplication Boulogne ↔ Toulouse

📄 _Doc. Cegedim :_ [_Object Storage — Vue générale_](https://academy.cegedim.cloud/storage/object-storage)

**À quoi ça sert** : disposer de toutes les données dans les deux datacenters, en actif/actif.

**Ce que ça protège** : panne complète d'un datacenter (incendie, désastre).

**Ce que ça NE protège PAS** :

* ❌ Suppression accidentelle : elle est **répliquée** sur les deux sites.
* ❌ Bug applicatif, erreur humaine, compromission de clés.

**Points d'attention** :

* Coût stockage approximativement doublé.
* 🛑 **Choix irréversible à la création de l'Object Store**. Impossible d'activer/désactiver après coup.

#### 3.7 Gestion des utilisateurs techniques (« Object Users »)

📄 _Doc. Cegedim :_ [_Gérer les Object Users_](https://academy.cegedim.cloud/storage/object-storage/object-storage-get-started/manage-object-users)

Chaque Object Store dispose d'un utilisateur initial avec tous les droits. Il est possible d'en créer d'autres pour cloisonner les rôles (un compte pour l'application qui écrit, un compte pour celle qui lit, etc.).

**Points d'attention** :

* ⚠️ Le mot de passe (« secret\_key ») n'est affiché **qu'une seule fois** à la création. À conserver dans un coffre sécurisé immédiatement.
* ⚠️ En cas de rotation des clés, prévoir une « période de grâce » (les deux clés valides en parallèle), faute de quoi les applications tombent en erreur d'authentification immédiatement.
* ⚠️ La propagation d'une nouvelle clé peut prendre **quelques minutes** sur l'infrastructure Cegedim.

***

### 4. Les décisions structurantes à prendre AVANT de démarrer

_📄 Doc. Cegedim :_ [_Limitations et bonnes pratiques_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/limitation-and-best-practices) _et_ [_Object Lock_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/object-lock)

Trois choix sont **irréversibles à la création** et engagent le projet pour toute sa durée.

| Décision                                      | Posée à                    | Réversible ? | À arbitrer avec         |
| --------------------------------------------- | -------------------------- | ------------ | ----------------------- |
| Géo-réplication (1 ou 2 datacenters)          | Création de l'Object Store | ❌ Non        | Architecture + budget   |
| Option ADO désactivée (prérequis Object Lock) | Création de l'Object Store | ❌ Non        | Sécurité / conformité   |
| Object Lock activé sur un bucket              | Création du bucket         | ❌ Non        | Métier (besoin légal ?) |

**Conséquences pratiques** :

* Si on prévoit qu'**au moins un bucket** aura besoin d'Object Lock (conformité, archive légale), il faut **demander à Cegedim, dès la création de l'Object Store, l'option ADO désactivée**. Cela ne se fait pas via le portail self-service, il faut **ouvrir un ticket**. Sinon, il faudra recréer un Object Store séparé plus tard.
* Si on hésite sur la géo-réplication, **mieux vaut la prendre** : la désactiver coûte trop cher en re-création.

***

### 5. Les irréversibilités à connaître (au-delà de la création)

📄 _Doc. Cegedim :_ [_Limitations et bonnes pratiques_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/limitation-and-best-practices)

| Action                                          | Effet                                 | Conséquence                                              |
| ----------------------------------------------- | ------------------------------------- | -------------------------------------------------------- |
| Suppression d'un bucket                         | Définitive                            | Bucket et contenu perdus                                 |
| Suppression d'une version spécifique d'un objet | Définitive                            | Pas de récupération                                      |
| Activation du versioning                        | Plus désactivable                     | Peut juste être suspendu                                 |
| Activation d'Object Lock sur un bucket          | Plus désactivable                     | À vie                                                    |
| Pose d'une rétention COMPLIANCE                 | Plus modifiable, plus raccourcissable | Données figées jusqu'à l'échéance, **même pour Cegedim** |
| Suppression d'un Object User                    | Définitive                            | Recréer + redistribuer les clés                          |

***

### 6. Ce qu'il faut savoir sur les logs et la traçabilité

📄 _Doc. Cegedim :_ [_**Compatibilité API S3**_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/s3-api-compatibility) **et** [_Limitations et bonnes pratiques_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/limitation-and-best-practices)

* Cegedim enregistre toutes les opérations (création, lecture, écriture, suppression) en interne.
* En revanche, **le projet ne peut pas y accéder en libre-service**. Pour extraire ces logs en cas d'incident, il faut ouvrir un ticket support.
* Aucun mécanisme d'alerte temps réel n'est disponible (pas d'équivalent d'un système de notifications événementielles).
* Conséquence : en cas d'incident (suppression suspecte, fuite), prévoir dans le plan de réponse à incident le délai de réponse Cegedim.

***

### 7. Recommandations selon la criticité des données

Trois niveaux à arbitrer avec l'équipe en fonction de la nature des données stockées.

#### Niveau 1 — Données métier classiques, non-reproductibles

_📄 Doc. Cegedim :_ [_Versioning_](https://academy.cegedim.cloud/storage/object-storage/object-storage-get-started/manage-versioning-in-bucket)_,_ [_Lifecycle_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/bucket-lifecycle) _et_ [_Accès bucket_](https://academy.cegedim.cloud/storage/object-storage/object-storage-get-started/manage-bucket-access)

**Effort : faible, sans rupture de service.**

1. Activer le versioning sur les buckets.
2. Activer une règle de purge (par exemple : conserver les versions historiques 30/60 jours).
3. Restreindre par IP les accès (réseau interne uniquement).
4. Auditer les comptes techniques : retirer les inutilisés, planifier une rotation des clés.

#### Niveau 2 — Données réglementaires ou critiques (conformité, archives légales)

📄 _Doc. Cegedim :_ [_Object Lock_](https://academy.cegedim.cloud/storage/object-storage/object-storage-features/object-lock)

**Effort : moyen, nécessite des arbitrages amont.**

5. Anticiper dès la création de l'Object Store la désactivation de l'option ADO (ticket Cegedim).
6. Créer les buckets avec Object Lock activé d'emblée.
7. Tester en mode GOVERNANCE pendant une phase pilote, basculer en COMPLIANCE après validation.

#### Niveau 3 — Données ultra-critiques (RTO court, exigence forte)

📄 _Doc. Cegedim :_ [_Object Storage — Vue générale_](https://academy.cegedim.cloud/storage/object-storage)

**Effort : significatif, à industrialiser.**

8. Mettre en place une sauvegarde externe régulière vers un autre Object Store (idéalement un autre tenant, etc.).
9. Tester la restauration périodiquement (drill de DR).
10. Documenter explicitement la procédure d'extraction des logs Cegedim dans le plan de réponse à incident.

***

### 8. Répartition des responsabilités (RACI implicite)

#### Ce qui est de la responsabilité de Cegedim

* Disponibilité du service (matériel, réseau, redondance, géo-réplication si souscrite).
* Chiffrement par défaut.
* Conservation des logs internes (et extraction sur demande).

#### Ce qui est de la responsabilité du projet

* Activation du versioning, du lifecycle, de l'Object Lock sur chaque bucket.
* Définition des règles d'accès (Bucket Policies).
* Gestion des comptes techniques et de la rotation des clés d'accès.
* Stratégie de sauvegarde au-delà du versioning, si exigence forte.
* Surveillance applicative des volumes et anomalies (pas d'alerting Cegedim).
* Documentation et runbooks de restauration.

***

### 9. Questions à poser / arbitrages à formaliser

Avant de signer le démarrage technique, il est utile que l'équipe technique réponde explicitement aux questions suivantes :

1. **Géo-réplication** : souscrite ou pas ? Quel surcoût stockage accepté ?
2. **Object Lock** : un bucket en aura-t-il besoin sur la durée du projet ? Si oui ou si doute → exiger ADO désactivée dès la création de l'Object Store.
3. **RPO (Recovery Point Objective)** : combien de temps de rétention pour les versions historiques ? 30 jours ? 60 ? 90 ?
4. **Réseau** : quelles plages d'IP doivent avoir accès aux buckets ? Réseau interne uniquement ? Partenaire externe ?
5. **Sauvegarde externe** : nécessaire (criticité Niveau 3) ou non ? Quel budget ?
6. **Comptes techniques** : qui détient les clés ? Quelle fréquence de rotation ? Quelle procédure de révocation en urgence ?
7. **Restauration** : a-t-on déjà testé qu'on sait restaurer un fichier supprimé ? Qui le fait ? Sous quel délai ?
8. **Logs** : qui ouvre les tickets Cegedim ? Quel SLA accepté ?

***

### 10. En résumé visuel

```javascript
            ┌────────────────────────────────────────┐
            │   Stockage Cegedim livré "nu"          │
            │   = aucune protection logique          │
            └────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────────────┐
    │  Décision N°1 (irréversible) à la création        │
    │  → Géo-réplication oui/non                        │
    │  → ADO désactivé (prérequis Object Lock futur)    │
    └───────────────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────────────┐
    │  Niveau 1 (rapide, sans rupture) :                │
    │  • Versioning  • Lifecycle  • Restriction IP      │
    │  • Comptes techniques cloisonnés                  │
    └───────────────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────────────┐
    │  Niveau 2 (si conformité légale) :                │
    │  • Object Lock GOVERNANCE → puis COMPLIANCE       │
    │  • Ticket Cegedim obligatoire                     │
    └───────────────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────────────┐
    │  Niveau 3 (criticité maximale) :                  │
    │  • Sauvegarde externe                             │
    │  • Tests de restauration périodiques              │
    └───────────────────────────────────────────────────┘
```
