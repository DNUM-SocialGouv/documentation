# 🔒 ProConnect

[ProConnect](https://partenaires.proconnect.gouv.fr/) identifie et authentifie les **utilisateurs professionnels publics et privés**. Il résulte de la fusion des anciens services AgentConnect, MonComptePro et InclusionConnect.\
Cette synthèse oriente les équipes produits sans se substituer à la [documentation officielle de ProConnect](https://partenaires.proconnect.gouv.fr/docs).

## Avantages
Pour se donner du courage, voici les avantages à migrer vers ProConnect :
* **Economie sur l'hébergement et l'exploitation** :
  * **Moins de composants** : on se passe de 2 instances Keycloak
  * [Support centralisé](https://proconnect.crisp.help/fr/)
  * **Gestion des accès automatisable** basée sur l'email et l'entité d'appartenance de l'utilisateur
* **Sécurité renforcée** :
  * Plus de mots de passe en base
  * 2FA natif
  * Moins de composants, moins d'obsolescence
  * Possibilité de limiter l'accès aux seuls agents publics
  * Chaque FI/FS choisit son exposition : Internet (accès FS public via FI public), RIE (accès FS @RIE via FI @RIE), "Hybridge" (accès FS public via FI @RIE).
* **Gain en UX** :
  * SSO ProConnect
  * Environnement visuel normalisé
* Et toutes les futures évolutions de ProConnect qu'on n'aura pas besoin d'implémenter sur chaque application !

## ProConnect vs FranceConnect

ProConnect possède certaines caractéristiques de FranceConnect :

* Développé et opéré par la DINUM
* Standard OpenIdConnect
* Serveur d'authentification intermédiaire entre Fournisseurs de Service (FS) et Fournisseurs d'Identité (FI)
* Demande d'habilitation via [DataPass](https://datapass.api.gouv.fr/demandes/pro_connect_service_provider/nouveau)

ProConnect diffère de FranceConnect sur ces points notables :

* Pas de choix explicite du FI (routage implicite par l'adresse email)
* Pas de redressement des traits d'identité au RNIPP
* Possibilité légale d'utiliser ProConnect comme moyen d'authentification unique pour accéder à un service public numérique
* Pas de notion de Fournisseurs de Données (FD)
* Dans certains cas, ProConnect s'appuie sur FranceConnect pour la certification d'identité

## ProConnect vs ProConnect Identité

Le fonctionnement de ProConnect diffère si l'utilisateur est connu ou pas d'un FI de l'administration :

| Aspect                                               | ProConnect (avec FI)                                                                                                                                                                                                                                                         | ProConnect Identité                                                                                                                                                        |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authentification                                     | Authentification portée par un FI du public. Routage vers le bon FI basé sur le nom de domaine de l’email. [La table de correspondance est portée par ProConnect](https://grist.numerique.gouv.fr/o/docs/3kQ829mp7bTy/AgentConnect-Configuration-des-Fournisseurs-dIdentite) | Compte email à créer sur ProConnect. Pas d’authentification par FI pour les comptes ProConnect Identité. C’est ProConnect qui porte une authentification par mot de passe. |
| Traits d’identité et données individuelles           | Fourni par le FI                                                                                                                                                                                                                                                             | Déclaratif (ou définie périodiquement via une connexion à FranceConnect pour les noms de domaines gratuits)                                                                |
| Entités de rattachement                              | Fournies par le FI                                                                                                                                                                                                                                                           | <p>Gestion libre des SIRET sur le compte ProConnect.<br>Certification possible du dirigeant via parcours dédié</p>                                                         |
| [2FA](authentification-proconnect.md#2fa-proconnect) | Implémenté et déclenché par le FI                                                                                                                                                                                                                                            | A la main de l'utilisateur sur son compte ProConnect Identité                                                                                                              |
| Adresses email supportées                            | \*.gouv.fr                                                                                                                                                                                                                                                                   | \*                                                                                                                                                                         |

_Un paramétrage de ProConnect permet de restreindre l'accès à un FS aux seuls agents publics._

## 2FA ProConnect

Le fonctionnement du 2FA ProConnect di point de vue du FS est décrit [ici](https://partenaires.proconnect.gouv.fr/docs/fournisseur-service/double_authentification)

Chaque FS demande un niveau de sécurité, notamment :
* **eidas1** : pas d'exigence 2FA, tout FI possible.
* **eidas2** : le FI doit fournir un 2FA afin que la connexion soit acceptée par le FS. Sinon ProConnect affichera une erreur.

Le mécanisme 2FA déclenché dépend donc de chaque FI :
* **Notre FI Ministères Sociaux** :
  * Un code de vérification est systématiquement envoyé par email (1.5FA)
* **ProConnect Identité**
  * Par défaut, ProConnect Identité envoie un code de vérification par email (1.5FA).
  * Sur son [compte ProConnect Identité](https://identite.proconnect.gouv.fr/connection-and-account), un utilisateur peut
    * soit ne rien faire et conserver le fonctionnement par défaut (1.5FA)
    * soit configurer un 2FA (Authenticator, passkey). Ce 2FA est au choix déclenché pour les FS qui l'exigent, ou systématiquement pour tous les FS
* **FI MEN** : _A faire_

## FAQ
* **Faut-il un autre moyen d'authentification ?**
Non, ProConnect suffit à authentifier tous les professionnels. Il est fortement déconseillé de proposer une authentification par email et mot de passe (moindre niveau global de sécurité, complexité des écrans et de l'application, pas de ROI, charge de support...).\
Exception : Pro Santé Connect surpasse ProConnect en termes d'obligation réglementaire et s'impose donc pour l'authentification des PS dans l'exercice de la médecine.\_

* **Faut-il un serveur Keycloak avec ProConnect ?**
Non, un serveur d'authentification Keycloak est inutile dans la plupart des cas.\
Exception : le produit est un progiciel dont le paramétrage ne permet pas de satisfaire aux spécifications de ProConnect.

## Sources de veille
* [Salon Tchap "ProConnect - Support et retex"](https://www.tchap.gouv.fr/#/room/!kBghcRpyMNThkFQjdW:agent.dinum.tchap.gouv.fr)
* [Releases ProConnect (core)](https://github.com/proconnect-gouv/federation/releases)
* [Releases ProConnect Identité](https://github.com/proconnect-gouv/proconnect-identite/releases)
* [Feuille de route](https://www.proconnect.gouv.fr/feuille-de-route)
* [Canal Mattermost BetaGouv (privé)](https://mattermost.incubateur.net/betagouv/channels/startup--proconnect)