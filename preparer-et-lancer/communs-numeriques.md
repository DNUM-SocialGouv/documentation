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

* **Site éditorial**
  * Soit socle [ONDINE ](../undefined/nos-produits/communs-numeriques/ondine.md)du MAS (Drupal)
  * Soit [Sites faciles](https://sites-faciles.beta.numerique.gouv.fr/)
* **Démarche administrative en ligne**
  * **Front usager** :
    * utiliser Démarches Simplifiées ou Démat Social autant que possible, plutôt que de développer une application front spécifique pour chaque besoin métier
    * Utiliser Démarches Simplifiées plutôt que Démat Social si possible. Voir les [différences entre Démarches Simplifiées et Démat Social](communs-numeriques.md#choisir-entre-démarches-simplifiées-et-démat-social).
  * **Back-office agent** :
    * si Démarches Simplifiées (ou Démat Social) ne peut pas couvrir les besoins des agents, envisager en sus un back-office de traitement
    * envisager le développement spécifique complet du back-office en réutilisant [API](#api-réutilisableset-services-externes-) et [frameworks](#frameworks-et-librairies-standards-pour-le-développement-spécifique) standards
* **Projet Référentiel**
  * [Grist](https://grist.numerique.gouv.fr/) pour un besoin simple
  * Sinon développement spécifique

## Communs numériques dans le contexte du MAS

Communs numériques grand public (solutions open source) :
* 

Communs numériques inter-ministériels :
* [**Démarches Simplifiées**](https://doc.demarches-simplifiees.fr/) est une solution de dématérialisation des démarches administratives. Elle est inter-ministérielle, générique et hébergée en mode SaaS.
* [**Sites Faciles**](https://sites-faciles.beta.numerique.gouv.fr/) est une base de site web CMS
* [Grist](https://grist.numerique.gouv.fr/) est un tableur avancé

Communs numériques internes :
* [**Démat Social**](https://demat.social.gouv.fr/) est un fork de Démarches Simplifiées, déployé au MAS.
* **Ondine**

## API réutilisables et services externes :
* [API Base d'Adresse Nationale (BAN)](https://www.data.gouv.fr/fr/dataservices/api-base-dadresse-nationale-ban/)
* [API Entreprise](https://www.data.gouv.fr/fr/dataservices/api-entreprise/)
* [API Associations](https://www.associations.gouv.fr/les-api-et-autres-outils.html)
* API Finess
* [Grist](https://grist.numerique.gouv.fr/)

## Frameworks et librairies pour le développement spécifique

_En cours_

* [Authentification](/concevoir/iam.md)
* GED (type S3, …)
* Notifications (envois emails)
* Publipostage (gestion des templates avec balises + production de documents)
* [API Gateway](/concevoir/api/api-gateway.md)
* Workflow
* Tableaux de bord
* Statistiques (production de fichiers Excel, BI)
* Chatbot...
* Base de données
* Accès/ORM

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
- Open source
- A héberger en interne
- DSFR natif
- API pour usage CMS headless

Différences :
|                      | **Socle Ondine**       | [Sites Faciles](https://sites-faciles.beta.numerique.gouv.fr/)|
| -------------------  | ---------------------- | -------------------------- |
| Stack technique      | Varnish/Drupal/PHP     | Wagtail(CMS)/Django/Python |
| Stockage de données  | MariaDB+Solr+GlusterFS | PostgreSQL                 |
| Stockage de fichiers | GlusterFS (ou S3?)     | Filesystem ou S3           |
| Instance multi-sites | Oui                    | Non                        |
| ProConnect natif     | ?                      | Oui                        |
| RGAA                 | ?                      | ?                          |
| RGS                  | ?                      | ?                          |
| Recherche intégrale  | ?                      | ?                          |
