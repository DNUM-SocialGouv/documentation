# ♻️ Communs numériques

Un commun numérique est une ressource numérique produite et gérée par une communauté d'utilisateurs en selon des règles de gouvernance conjointement élaborées. Tout projet DOIT tenter de réutiliser des communs numériques en suivant ce guide, et PEUT y contribuer.

## Quel commun numérique pour quel projet ?

Mon produit est un(e)...

* **Site éditorial (ou avec une part significative de contenu éditorial)**
  * pour un gestionnaire de contenus (CMS) : [voir la page dédiée aux CMS](communs-cms.md)
  * pour un Wiki, une base de connaissance : [**GitBook**](https://www.gitbook.com/) est un Wiki SaaS gratuit avec contenu stocké sur GitHub. Exemples d'usages :
    * Le présent [guide DNUM](https://dnum-ministeres-sociaux.gitbook.io/ressources/) (instance DNUM partagée)
    * [Base de connaissance VAO](https://dnum-ministeres-sociaux.gitbook.io/vao-documentation/t1eK0jUdXMliu8S6UWUr) (instance DNUM partagée)
    * [Base de connaissance Mon Suivi Social](https://mon-suivi-social.gitbook.io/mon-suivi-social) (instance dédiée)
    * Documentation produit
* **Démarche administrative en ligne**
  * pour le **front usager** :
    * utiliser Démarche Numérique ou Démat Social autant que possible, plutôt que de développer une application front spécifique pour chaque besoin métier
      * utiliser Démarche Numérique plutôt que Démat Social si possible. Voir comment [choisir entre Démarche Numérique et Démat Social](communs-numeriques.md#choisir-entre-démarche-numérique-et-démat-social)
    * en dernier recours, envisager le développement spécifique du front usager
  * pour le **back-office agent** :
    * utiliser les nombreuses fonctionnalités d'administration et d'instruction de Démarche Numérique (ou Démat Social)
    * si cela ne suffit pas, envisager un back-office complémentaire à Démarche Numérique, sur la base de [Grist](communs-grist.md)
    * en dernier recours seulement, envisager le développement complet du back-office
* **Référentiel de données**
  * Si possible paramétrage front et back sur [Grist](communs-grist.md) pour une application de gestion interne ou à portée et criticité modérée
  * Sinon développement front spécifique sur la base d'un [backend-as-a-service](communs-numeriques.md#backends-as-a-service)
  * Sinon envisager le développement spécifique complet du référentiel

Des lors qu'il y a développement spécifique, le projet DOIT réutiliser au maximum les communs listés ci-dessous

* [les communs numériques](communs-numeriques.md#solutions-transverses-et-communs-numériques)
* [les API externes](communs-numeriques.md#api-externes)
* [les API internes](communs-numeriques.md#api-internes)
* [les frameworks et librairies standards](communs-numeriques.md#frameworks-et-librairies-standards)

## Solutions transverses et communs numériques
* [**Démarche Numérique**](https://demarche.numerique.gouv.fr/) : solution SaaS interministérielle de dématérialisation des démarches administratives.
* [**Grist**](communs-grist.md) : tableur avancé open source, enrichi et hébergé par la DINUM
* [**Démat Social**](https://demat.social.gouv.fr/) est un fork de Démarche Numérique, déployé aux Ministères Sociaux.

## API externes

* Les API Entreprise
  * [API Entreprise complète](https://www.data.gouv.fr/fr/dataservices/api-entreprise/) : pas de recherche multicritères
  * [API SIRENE de l'INSEE](https://portail-api.insee.fr/catalog/api/2ba0e549-5587-3ef1-9082-99cd865de66f) pour les besoins simples de recherche
  * [API Recherche Entreprise](https://www.data.gouv.fr/fr/dataservices/api-recherche-dentreprises/) : recherche par SIRET/nom ET filtrage sur critères (codes d'activité, géographie...)
  * [API Association du Compte Asso (DJEPVA) via API Entreprise](https://www.data.gouv.fr/dataservices/api-donnees-associations-djepva-bouquet-api-entreprise/) : intègre Alsace-Moselle et les données des autres API (RNA, SIRENE, DILA)
* [API Base d'Adresse Nationale (BAN)](https://www.data.gouv.fr/dataservices/api-adresse-base-adresse-nationale-ban/)
* [API Recherche des personnes physiques (SFiP)](https://www.data.gouv.fr/dataservices/api-service-finances-publiques-sfip/) : données personnelles d'un citoyen (état civil complet, dernière adresse connue de l’administration fiscale, identifiant fiscal ou SPI).

La plupart des APIs du service public sont référencées sur [https://www.data.gouv.fr/dataservices](https://www.data.gouv.fr/dataservices)

## API internes
Les API [https://arssante.opendatasoft.com/](https://arssante.opendatasoft.com/) :
* API des établissements de santé (données FINESS)
* API des professionnels de santé (données RPPS)

## Frameworks et librairies standards

* [Authentification](../concevoir/authentification.md)
* Stockage documentaire et GED (type S3…)
* Notifications (envois emails)
* Publipostage (gestion des templates avec balises + production de documents)
* [Stockage et accès aux données](../concevoir/data/)
* [API Gateway](../concevoir/api/api-gateway.md)
* Workflow
* Statistiques (tableaux de bord, production de fichiers CSV, décisionnel)
  * Metabase
  * [Matomo pour la mesure d'audience](communs-numeriques.md#matomo-pour-la-mesure-daudience)
* Chatbot
* IA
* ETL/ELT : Talend EE, Kestra

## Backends as a Service

* Eventuellement Grist comme Backend-as-a-Service avec un frontend spécifique s'il n'y a pas besoin de permissions Grist avancées. Quelques limitations de Grist :
  * Les permissions avancées ne sont pas accessibles par API
  * Pas de propagation de l'authentification ProConnect par API : compte de service seulement
  * l'API de l'instance DINUM est limitée à 10 appels en parallèle par document Grist
* Manifest.build a été écarté car trop limité

## Matomo pour la mesure d'audience

[Matomo](https://matomo.org/) est la solution de mesure d'audience et d'utilisation de nos services numériques (web analytics). Tout projet DEVRAIT réutiliser l'une des 3 instances de Matomo existantes :

| Instance       | Hébergement                                                       |
| -------------- | ----------------------------------------------------------------- |
| Atlas (FabNum) | [SaaS @boscop.fr](https://boscop.fr/matomo-hebergement/)          |
| DICOM          | [SaaS @matomo.org](https://matomo.org/matomo-cloud/)              |
| Cegedim        | [SaaS @Cegedim.cloud](https://cegedim.cloud/produits/analytique/) |

Bien qu'[Eulerian](https://www.eulerian.com/) soit une solution souveraine, elle n'est pas privilégiée.

## Choisir entre Démarche Numérique et Démat Social

|                                     | [Démarche Numérique](https://demarche.numerique.gouv.fr/)    | [Démat Social](https://demat.social.gouv.fr/)                                                      |
| ----------------------------------- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| Entité responsable                  | SPM/DINUM                                                    | DNUM des Ministères Sociaux                                                                        |
| Hébergement                         | SecNumCloud@OVH                                              | HDS@Cegedim                                                                                        |
| Connexion FranceConnect             | Oui                                                          | Non                                                                                                |
| Connexion ProConnect                | Oui                                                          | Non                                                                                                |
| Champs spécifiques                  | n/a                                                          | <p>Champ NIR sécurisé<br>2 champs FINESS (avec lookup FINESS)<br>Champ RPPS (avec lookup RPPS)</p> |
| Montées de version                  | \~tous les jours                                             | 3-12 mois de retard                                                                                |
| Numérotation des versions           | AAAA-MM-DD-version                                           | x.y.z                                                                                              |
| Accès Administrateur et Instructeur | Internet                                                     | RIE seulement                                                                                      |

## Pistes explorées et décisions d'architecture

* **GLPI** écarté en 04/2025 (workflow pas assez contraignant pour le métier et pas paramétrable ; pas 12-factors (stockage FS) ; peu accessible)
* **Manifest.build** est un Backend-as-a-Service open source en JS. Convient pour des besoins CRUD simple. Très limité sur l'authentification et la gestion des droits.
* **Directus.io** est un Backend-as-a-Service satisfaisant mais a été écarté à cause de son coût de licence

## Sources de veille
* [Releases Démarche Numérique](https://github.com/demarches-simplifiees/demarches-simplifiees.fr/releases)
* [Salon Tchap "Démarche Numérique"](https://www.tchap.gouv.fr/#/room/#demarchessimplifieesS454OP0:agent.dinum.tchap.gouv.fr)