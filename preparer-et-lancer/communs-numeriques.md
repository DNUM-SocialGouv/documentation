---
icon: recycle
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Communs numériques

Un commun numérique est une ressource numérique produite, gérée et gouvernée par une communauté d'utilisateurs selon des règles de gouvernance conjointement élaborées. Tout projet DOIT tenter de réutiliser des communs numériques en suivant ce guide, et PEUT y contribuer.

## Arbre de décision suivant la nature du projet

Mon produit est un(e)...

* **Site éditorial public**
  * voir comment [choisir entre le Socle Ondine et Sites Faciles](communs-numeriques.md#choisir-entre-socle-ondine-et-sites-faciles)
* **Démarche administrative en ligne**
  * pour le **front usager** :
    * utiliser Démarches Simplifiées ou Démat Social autant que possible, plutôt que de développer une application front spécifique pour chaque besoin métier
      * utiliser Démarches Simplifiées plutôt que Démat Social si possible. Voir comment [choisir entre Démarches Simplifiées et Démat Social](communs-numeriques.md#choisir-entre-démarches-simplifiées-et-démat-social)
    * en dernier recours, envisager le développement spécifique du front usager
  * pour le **back-office agent** :
    * utiliser les nombreuses fonctionnalités d'administration et d'instruction de Démarches Simplifiées (ou Démat Social)
    * si cela ne suffit pas, envisager un back-office complémentaire à DS
    * en dernier recours seulement, envisager le développement complet du back-office
* **Base de données / Référentiel**
  * [Grist](https://grist.numerique.gouv.fr/) pour un besoin très simple
  * éventuellement un backend-as-a-service également pour un besoin simple
  * sinon envisager le développement spécifique

Des lors qu'il y a développement spécifique, le projet DOIT réutiliser au maximum :

* [les communs numériques](communs-numeriques.md#communs-numériques-au-mas)
* [les API internes et externes](communs-numeriques.md#api-externes-et-internes)
* [les frameworks et librairies standards](communs-numeriques.md#frameworks-et-librairies-standards)

## Communs numériques au MAS

Communs numériques grand public (solutions open source) :

* _Aucun commun de haut-niveau identifié à date._

Communs numériques inter-ministériels :

* [**Démarches Simplifiées**](https://doc.demarches-simplifiees.fr/) : solution de dématérialisation des démarches administratives. Elle est inter-ministérielle, générique et hébergée en mode SaaS.
* [**Sites Faciles**](https://sites-faciles.beta.numerique.gouv.fr/) : base de site web CMS
* [**Grist**](https://grist.numerique.gouv.fr/) est un tableur avancé développé en partie par la DINUM

Communs numériques internes :

* [**Démat Social**](https://demat.social.gouv.fr/) est un fork de Démarches Simplifiées, déployé au MAS.
* **Ondine**

## API externes et internes

API particulièrement intéressantes pour le MAS :

* Les API Entreprise
  * [API Entreprise complète](https://www.data.gouv.fr/fr/dataservices/api-entreprise/) : pas de recherche multi-critères
  * [API SIRENE de l'INSEE](https://portail-api.insee.fr/catalog/api/2ba0e549-5587-3ef1-9082-99cd865de66f?aq=ALL) pour les besoins simples de recherche
  * [API Recherche Entreprise](https://www.data.gouv.fr/fr/dataservices/api-recherche-dentreprises/) : recherche par SIRET/nom ET filtrage sur critères (codes d'activité, géographie...)
  * API des établissements de santé: pas d'API Finess native mais [exposition API du fichier "t\_finess" sur OpenDataSoft](https://arssante.opendatasoft.com/)
* Les API Association
  * [API Association](https://www.associations.gouv.fr/les-api-et-autres-outils.html)
  * [API Association annonces officielles et comptes annuels](https://api.gouv.fr/les-api/api-annonces-comptes-annuels-associations-joafe)
  * [API Subvention](https://api.gouv.fr/les-api/api-data-subvention)
* [API Base d'Adresse Nationale (BAN)](https://www.data.gouv.fr/fr/dataservices/api-base-dadresse-nationale-ban/)

## Frameworks et librairies standards

* [Authentification](../concevoir/iam.md)
* Stockage documentaire et GED (type S3, …)
* Notifications (envois emails)
* Publipostage (gestion des templates avec balises + production de documents)
* [Stockage et accès aux données](../concevoir/data/)
* [API Gateway](../concevoir/api/api-gateway.md)
* Workflow
* Statistiques (tableaux de bord, production de fichiers CSV, BI)
  * Metabase ? Superset ?
  * Matomo (quelle instance ?)
* Chatbot
* IA
* ETL/ELT

## Choisir entre Démarches Simplifiées et Démat Social

|                                     | [Démarches Simplifiées](https://demarches.numerique.gouv.fr) | [Démat Social](https://demat.social.gouv.fr/)                                                      |
| ----------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Entité responsable                  | SPM/DINUM                                                      | MAS/DNUM                                                                                           |
| Hébergement                         | SecNumCloud@OVH                                                | HDS@Cegedim                                                                                        |
| Connexion FranceConnect             | Oui                                                            | Non                                                                                                |
| Connexion ProConnect                | Oui                                                            | Non                                                                                                |
| Champs spécifiques                  | n/a                                                            | <p>Champ NIR sécurisé<br>2 champs FINESS (avec lookup FINESS)<br>Champ RPPS (avec lookup RPPS)</p> |
| Montées de version                  | \~tous les jours                                               | 3-12 mois de retard                                                                                |
| Numérotation des versions           | AAAA-MM-DD-version                                             | x.y.z                                                                                              |
| Accès Administrateur et Instructeur | Internet                                                       | RIE seulement                                                                                      |

## Choisir entre Socle Ondine et Sites Faciles

Points communs :

* Solution de type CMS
* DSFR natif
* API pour usage CMS headless
* Formulaires simples
* Contributions possibles au produit
* Produit maintenu, mais montées de versions à effectuer soi-même
* A héberger en interne sur Intranet ou Cegedim ; sauf à faire évoluer l'infra de la FabNum pour PHP ou Python
* Recherche texte intégrale, y compris dans les pièces-jointes

Différences :

|                      | Socle Ondine       | [Sites Faciles](https://sites-faciles.beta.numerique.gouv.fr/) |
| -------------------- | ------------------ | -------------------------------------------------------------- |
| Entité responsable   | SG/DICOM           | SPM/DINUM/OPI                                                  |
| Open source          | Non (_pas à date_) | Oui                                                            |
| Stack technique      | Varnish/Drupal/PHP | Wagtail(CMS)/Django/Python                                     |
| Stockage de données  | MariaDB            | PostgreSQL                                                     |
| Stockage index       | Solr               | PostgreSQL ou Elasticsearch                                    |
| Stockage de fichiers | GlusterFS (ou S3?) | Filesystem ou S3                                               |
| Instance multi-sites | Oui                | Non                                                            |
| ProConnect natif     | Non                | Oui                                                            |
| Conformité RGAA      | RGAA 4 à 75%       | RGAA 4.1 partiel                                               |
| Conformité RGS       | Oui                | n/c                                                            |
| Dév. spécifique      | Non (non souhaité) | Oui (possible)                                                 |

Synthèse :

* Le socle Ondine est davantage industrialisé pour être hébergé en interne. Il bénéficie des forces de Drupal.
* Sites Faciles est plus moderne en termes de technologies et peut-être hébergé plus facilement en externe.

## Suivi des pistes explorées et décisions d'architecture

* GLPI écarté 04/2025.
* Manifest.build est un backend-as-a-service open source en JS. Convient pour des besoins CRUD simple. Très limité sur l'authentification et la gestion des droits.
