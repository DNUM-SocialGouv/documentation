---
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

Un commun numérique est une ressource numérique produite, gérée et gouvernée par une communauté d'utilisateurs selon des règles de gouvernance conjointement élaborées. Tout projet DOIT tenter de réutiliser des communs numériques, et si possible y contribuer, en suivant ce guide.

## Arbre de décision suivant la nature du projet
Mon projet est un/une ...
* **Site éditorial public**
  * voir comment [choisir entre le Socle Ondine et Sites Faciles](#choisir-entre-socle-ondine-et-sites-faciles)
* **Démarche administrative en ligne**
  * pour le **front usager** :
    * utiliser Démarches Simplifiées ou Démat Social autant que possible, plutôt que de développer une application front spécifique pour chaque besoin métier
      * utiliser Démarches Simplifiées plutôt que Démat Social si possible. Voir comment [choisir entre Démarches Simplifiées et Démat Social](communs-numeriques.md#choisir-entre-démarches-simplifiées-et-démat-social)
    * En dernier recours, envisager le développement spécifique du front usager
  * pour le **back-office agent** :
    * utiliser les nombreuses fonctionnalités d'administration et d'instruction de Démarches Simplifiées (ou Démat Social)
    * Si cela ne suffit pas, envisager un back-office complémentaire à DS
    * En dernier recours seulement, envisager le développement complet du back-office
* **Base de données / Référentiel**
  * [Grist](https://grist.numerique.gouv.fr/) pour un besoin simple
  * sinon envisager le développement spécifique

Des lors qu'il y a développement spécifique, le projet DOIT réutiliser au maximum :
- [les communs numériques](#communs-numériques-dans-le-contexte-du-mas)
- [les API internes et externes](#api-réutilisables)
- [les frameworks et librairies standards](#frameworks-et-librairies-standards)

## Communs numériques dans le contexte du MAS

Communs numériques grand public (solutions open source) :
* _Aucun commun de haut-niveau identifié à date. GLPI écarté 04/2025._

Communs numériques inter-ministériels :
* [**Démarches Simplifiées**](https://doc.demarches-simplifiees.fr/) : solution de dématérialisation des démarches administratives. Elle est inter-ministérielle, générique et hébergée en mode SaaS.
* [**Sites Faciles**](https://sites-faciles.beta.numerique.gouv.fr/) : base de site web CMS
* [**Grist**](https://grist.numerique.gouv.fr/) est un tableur avancé développé en partie par la DINUM

Communs numériques internes :
* [**Démat Social**](https://demat.social.gouv.fr/) est un fork de Démarches Simplifiées, déployé au MAS.
* **Ondine**

## API externes et internes

API externes particulièrement intéressantes pour le MAS :
* [**API Base d'Adresse Nationale (BAN)**](https://www.data.gouv.fr/fr/dataservices/api-base-dadresse-nationale-ban/)
* [**API Entreprise**](https://www.data.gouv.fr/fr/dataservices/api-entreprise/)
* [**API Associations**](https://www.associations.gouv.fr/les-api-et-autres-outils.html)

API internes MAS à réutiliser :
* API Finess

## Frameworks et librairies standards

_En cours_

* [Authentification](/concevoir/iam.md)
* Stockage documentaire et GED (type S3, …)
* Notifications (envois emails)
* Publipostage (gestion des templates avec balises + production de documents)
* [Stockage et accès aux données](/concevoir/data/README.md)
* [API Gateway](/concevoir/api/api-gateway.md)
  * _Reste à positionner Hasura et à mieux positionner PISTE_
* Workflow
* Statistiques (tableaux de bord, production de fichiers CSV, BI)
  * Metabase ?
* Chatbot
* IA

## Choisir entre Démarches Simplifiées et Démat Social

|                                     | [Démarches Simplifiées](https://www.demarches-simplifiees.fr/) | [Démat Social](https://demat.social.gouv.fr/)                                                      |
| ----------------------------------- | -------------------------- | -------------------------------------------------------------------------------------------------- |
| Entité responsable                  | SPM/DINUM                  | MAS/DNUM                                                                                           |
| Hébergement                         | SecNumCloud@OVH            | HDS@Cegedim                                                                                        |
| Connexion FranceConnect             | Oui                        | Non                                                                                                |
| Connexion ProConnect                | Oui                        | Non                                                                                                |
| Champs spécifiques                  | n/a                        | <p>Champ NIR sécurisé<br>2 champs FINESS (avec lookup FINESS)<br>Champ RPPS (avec lookup RPPS)</p> |
| Montées de version                  | \~tous les jours           | 3-12 mois de retard                                                                                |
| Numérotation des versions           | AAAA-MM-DD-version         | x.y.z                                                                                              |
| Accès Administrateur et Instructeur | Internet                   | RIE seulement                                                                                      |

## Choisir entre Socle Ondine et Sites Faciles

Points communs :
- DSFR natif
- API pour usage CMS headless
- Formulaires simples
- Contributions possibles au produit
- Produit maintenu, mais montées de versions à effectuer soi-même
- A héberger en interne sur Cegedim, sauf à faire évoluer l'infra de la FabNum pour PHP ou Python
- Recherche intégrale, y compris dans les pièces-jointes

Différences :
|                      | [Socle Ondine](/undefined/nos-produits/communs-numeriques/ondine.md) | [Sites Faciles](https://sites-faciles.beta.numerique.gouv.fr/)|
| -------------------  | -------------------------- | -------------------------- |
| Entité responsable   | SG/DICOM                   | SPM/DINUM/OPI              |
| Open source          | Non (_pas à date_)         | Oui                        |
| Stack technique      | Varnish/Drupal/PHP         | Wagtail(CMS)/Django/Python |
| Stockage de données  | MariaDB                    | PostgreSQL                 |
| Stockage index       | Solr                       | PostgreSQL ou Elasticsearch|
| Stockage de fichiers | GlusterFS (ou S3?)         | Filesystem ou S3           |
| Instance multi-sites | Oui                        | Non                        |
| ProConnect natif     | Non                        | Oui                        |
| Conformité RGAA      | 75%                        | n/c                        |
| Homologation RGS     | ?                          | n/c (à faire)              |
| Avis                 | ?                          | ?                          |

Synthèse :
- Le socle Ondine est davantage industrialisé pour être hébergé en interne. Il bénéficie de la robustesse de Drupal
- Sites Faciles a une stack technique plus moderne et est davantage propice au développement métier spécifique
