---
icon: recycle
---

# Communs numériques

Un commun numérique est une ressource numérique produite et gérée par une communauté d'utilisateurs en selon des règles de gouvernance conjointement élaborées. Tout projet DOIT tenter de réutiliser des communs numériques en suivant ce guide, et PEUT y contribuer.

## Quel commun numérique pour quel projet ?

Mon produit est un(e)...

* **Site éditorial public**
  * pour un CMS : voir comment [choisir entre le Socle Ondine et Sites Faciles](communs-numeriques.md#choisir-entre-socle-ondine-et-sites-faciles)
  * pour un Wiki, une base de connaissance : GitBook (cf. infra)
* **Démarche administrative en ligne**
  * pour le **front usager** :
    * utiliser Démarches Simplifiées ou Démat Social autant que possible, plutôt que de développer une application front spécifique pour chaque besoin métier
      * utiliser Démarches Simplifiées plutôt que Démat Social si possible. Voir comment [choisir entre Démarches Simplifiées et Démat Social](communs-numeriques.md#choisir-entre-démarches-simplifiées-et-démat-social)
    * en dernier recours, envisager le développement spécifique du front usager
  * pour le **back-office agent** :
    * utiliser les nombreuses fonctionnalités d'administration et d'instruction de Démarches Simplifiées (ou Démat Social)
    * si cela ne suffit pas, envisager un back-office complémentaire à DS, sur la base de [Grist](https://grist.numerique.gouv.fr/)
    * en dernier recours seulement, envisager le développement complet du back-office
* **Référentiel de données**
  * Si possible paramétrage front et back sur [Grist](https://grist.numerique.gouv.fr/) pour une application de gestion interne ou à portée et criticité modérée
  * Sinon développement front spécifique sur la base d'un [backend-as-a-service](#backends-as-a-service)
  * Sinon envisager le développement spécifique complet du référentiel

Des lors qu'il y a développement spécifique, le projet DOIT réutiliser au maximum :

* [les communs numériques](communs-numeriques.md#communs-numériques-au-mas)
* [les API internes et externes](communs-numeriques.md#api-externes-et-internes)
* [les frameworks et librairies standards](communs-numeriques.md#frameworks-et-librairies-standards)

## Solutions transverses et communs numériques au MAS

Solutions et communs numériques grand public (solutions open source ou SaaS) :

* [**GitBook**](https://www.gitbook.com/) : Wiki SaaS gratuit avec contenu stocké sur GitHub. Exemples d'utilisation :
  * Le présent [guide DNUM](https://dnum-ministeres-sociaux.gitbook.io/ressources/) (instance DNUM partagée)
  * [Base de connaissance VAO](https://dnum-ministeres-sociaux.gitbook.io/vao-documentation/t1eK0jUdXMliu8S6UWUr) (instance DNUM partagée)
  * [Base de connaissance Mon Suivi Social](https://mon-suivi-social.gitbook.io/mon-suivi-social) (instance dédiée)

Solutions et communs numériques inter-ministériels :

* [**Démarches Simplifiées**](https://doc.demarches-simplifiees.fr/) : solution SaaS interministérielle de dématérialisation des démarches administratives.
* [**Sites Faciles**](https://sites-faciles.beta.numerique.gouv.fr/) : base de site web CMS
* [**Grist**](https://grist.numerique.gouv.fr/) : tableur avancé open source, enrichi et hébergé par la DINUM

Solutions et communs numériques internes :

* [**Démat Social**](https://demat.social.gouv.fr/) est un fork de Démarches Simplifiées, déployé au MAS.
* **Ondine**

## API externes et internes

API particulièrement intéressantes pour le MAS :

* Les API Entreprise
  * [API Entreprise complète](https://www.data.gouv.fr/fr/dataservices/api-entreprise/) : pas de recherche multicritères
  * [API SIRENE de l'INSEE](https://portail-api.insee.fr/catalog/api/2ba0e549-5587-3ef1-9082-99cd865de66f) pour les besoins simples de recherche
  * [API Recherche Entreprise](https://www.data.gouv.fr/fr/dataservices/api-recherche-dentreprises/) : recherche par SIRET/nom ET filtrage sur critères (codes d'activité, géographie...)
  * [API des établissements de santé](https://arssante.opendatasoft.com/) : données FINESS
  * [API des professionnels de santé](https://arssante.opendatasoft.com/) : données RPPS
  * [API Association du Compte Asso (DJEPVA) via API Entreprise](https://www.data.gouv.fr/dataservices/api-donnees-associations-djepva-bouquet-api-entreprise/) : intègre Alsace-Moselle et les données des autres API (RNA, SIRENE, DILA)
* [API Base d'Adresse Nationale (BAN)](https://www.data.gouv.fr/dataservices/api-adresse-base-adresse-nationale-ban/)

## Frameworks et librairies standards

* [Authentification](../concevoir/authentification.md)
* Stockage documentaire et GED (type S3, …)
* Notifications (envois emails)
* Publipostage (gestion des templates avec balises + production de documents)
* [Stockage et accès aux données](../concevoir/data/)
* [API Gateway](../concevoir/api/api-gateway.md)
* Workflow
* Statistiques (tableaux de bord, production de fichiers CSV, BI)
  * Metabase ? Superset ?
  * [Matomo pour la mesure d'audience](communs-numeriques.md#matomo-pour-la-mesure-daudience)
* Chatbot
* IA
* ETL/ELT : Talend EE

## Backends as a Service
* Eventuellement Grist comme Backend-as-a-Service avec un frontend spécifique s'il n'y a pas besoin de permissions Grist avancées. Quelques limitations de Grist :
  * Les permissions avancées ne sont pas accessibles par API
  * Pas de propagation de l'authentification ProConnect par API : compte de service seulement
  * l'API  de l'instance DINUM est limitée à 10 appels en parallèle par document Grist
* Directus.io est satisfaisant mais a un coût de licence
* Manifest.build a été écarté car trop limité

## Matomo pour la mesure d'audience

[Matomo](https://matomo.org/) est la solution de mesure d'audience et d'utilisation de nos services numériques (web analytics). Tout projet DEVRAIT réutiliser l'une des 3 instances de Matomo existantes :

| Instance       | Hébergement                                                       |
| -------------- | ----------------------------------------------------------------- |
| Atlas (FabNum) | [SaaS @boscop.fr](https://boscop.fr/matomo-hebergement/)          |
| DICOM          | [SaaS @matomo.org](https://matomo.org/matomo-cloud/)              |
| Cegedim        | [SaaS @Cegedim.cloud](https://cegedim.cloud/produits/analytique/) |

Bien qu'[Eulerian](https://www.eulerian.com/) soit une solution souveraine, elle n'est pas privilégiée.

## Choisir entre Démarches Simplifiées et Démat Social

|                                     | [Démarches Simplifiées](https://demarches.numerique.gouv.fr) | [Démat Social](https://demat.social.gouv.fr/)                                                      |
| ----------------------------------- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| Entité responsable                  | SPM/DINUM                                                    | MAS/DNUM                                                                                           |
| Hébergement                         | SecNumCloud@OVH                                              | HDS@Cegedim                                                                                        |
| Connexion FranceConnect             | Oui                                                          | Non                                                                                                |
| Connexion ProConnect                | Oui                                                          | Non                                                                                                |
| Champs spécifiques                  | n/a                                                          | <p>Champ NIR sécurisé<br>2 champs FINESS (avec lookup FINESS)<br>Champ RPPS (avec lookup RPPS)</p> |
| Montées de version                  | \~tous les jours                                             | 3-12 mois de retard                                                                                |
| Numérotation des versions           | AAAA-MM-DD-version                                           | x.y.z                                                                                              |
| Accès Administrateur et Instructeur | Internet                                                     | RIE seulement                                                                                      |

## Choisir entre Socle Ondine et Sites Faciles

Points communs :

* Solution de type CMS
* DSFR natif
* API pour usage CMS headless
* Formulaires simples
* Contributions possibles au produit
* Produit maintenu, mais montées de versions à effectuer soi-même
* A héberger en interne sur Intranet ou Cegedim ; sauf à faire évoluer Atlas pour PHP ou Python
* Recherche texte intégrale, y compris dans les pièces-jointes

Différences dans notre contexte:

|                      | Socle Ondine         | [Sites Faciles](https://sites-faciles.beta.numerique.gouv.fr/) |
| -------------------- | -------------------- | -------------------------------------------------------------- |
| Entité responsable   | SG/DICOM             | SPM/DINUM/OPI                                                  |
| Open source          | Non                  | Oui                                                            |
| Stack technique      | Varnish/Drupal/PHP   | Wagtail(CMS)/Django/Python                                     |
| Stockage de données  | MariaDB              | PostgreSQL                                                     |
| Stockage index       | Solr                 | PostgreSQL ou Elasticsearch                                    |
| Stockage de fichiers | GlusterFS (ou S3?)   | Filesystem ou S3                                               |
| Instance multi-sites | Oui                  | Non                                                            |
| ProConnect natif     | Non                  | Oui                                                            |
| Conformité RGAA      | RGAA 4 à 75%         | RGAA 4.1 partiel                                               |
| Conformité RGS       | Oui                  | n/c                                                            |
| Dév spécifique       | Non                  | Oui                                                            |
| Montées de version   | A la charge du socle | A la charge des équipes produits                               |

Synthèse :

* Le socle Ondine est industrialisé pour être hébergé en interne. Sa migration sur la cible Cloud est prévue. Il bénéficie des forces et faiblesses de Drupal.
* Sites Faciles est plus moderne en termes de technologies et peut-être hébergé plus facilement sur un cloud.

## Pistes explorées et décisions d'architecture

* **GLPI** écarté en 04/2025 (workflow pas assez contraignant pour le métier et pas paramétrable ; pas 12-factors (stockage FS) ; peu accessible)
* **Manifest.build** est un backend-as-a-service open source en JS. Convient pour des besoins CRUD simple. Très limité sur l'authentification et la gestion des droits.
