# ♻️ Démarche Numérique et Démat Social

## Usages

Les solutions de CMS répondent à différents besoins :
* **Site institutionnel ou éditorial** : un CMS Headful est adapté, mais ne permet pas d'implémenter de logique métier
* **Application métier avec contenus éditoriaux embarqués simples** : ajouter des options de paramétrage à l'application métier peut suffire. L'ajout d'une page se fait par l'équipe technique.
* **Application métier avec contenus éditoriaux embarqués riches/complexe** : un CMS headless est recommandé
* **Approche hybride application métier / site éditorial** : pas de solution simple et transparente. Il faut faire des compromis (2 solutions avec un style similaire, sous-domaines DNS, gestion du contenu par l'équipe produit, etc.)

## Les CMS aux Ministères Sociaux
* **Ondine** est le socle des sites éditoriaux des Ministères Sociaux
* [**Sites Conformes (anc. Sites Faciles)**](https://sites.beta.gouv.fr/) est un commun numérique interministériel et vient challenger le socle Ondine.
* [**Strapi**](https://strapi.io) est un CMS headless Open source français très utilisé dans la sphère BetaGouv
* [**Grist**](communs-grist.md) permet de construire un CMS headless minimal et 0-déploiement

## Comparaison des CMS

Points communs :
* Recherche texte intégrale, y compris dans les pièces-jointes

|                          | **Socle Ondine**       | **Sites Conformes**         | **Strapi**           | **Grist**          |
| ------------------------ | ---------------------- | --------------------------- | -------------------- | ------------------ |
| CMS Headful (IHM)        | ✅                    | ✅                          | ❌                   | ❌                |
| CMS Headless (API)       | ❌                    | ✅                          | ✅                   | ✅ (contenu brut) |
| Entité porteuse          | SG/DICOM               | SPM/DINUM                   | Strapi               | SPM/DINUM          |
| Permet le dév spécifique | ❌                    | ✅                          | ✅                   | ✅                |
| Recherche full-text      | ✅                    | ✅                          | ✅                   | ❌                |
| ProConnect natif         | ❌                    | ✅                          | n/a                  | n/a                |
| Conformité RGAA          | 75% des critères       | 82% des critères            | n/a                  | n/a                |
| DSFR natif               | ✅                    | ✅                          | n/a                  | n/a                |
| Open source              | ❌                    | ✅                          | ✅                   | ✅                |
| Stack technique          | Varnish + Drupal + PHP | Wagtail + Django + Python   | Node.js              | Python             |
| Stockage de données      | MariaDB                | PostgreSQL                  | PostgreSQL           | n/a (SaaS)         |
| Stockage index           | Solr                   | PostgreSQL ou Elasticsearch | PostgreSQL, ES...    | n/a (SaaS)         |
| Stockage de documents    | GlusterFS              | S3                          | S3                   | n/a (SaaS)         |
| Conformité RGS           | ✅                    | n/a                         | n/a                   | ✅                |
| Hébergement              | Cegedim (cible Atlas)  | Atlas                       | Atlas                | n/a (SaaS)         |
| Exploitation             | Equipe socle           | Equipe produit              | Equipe produit       | Equipe socle       |

## Sources de veille
* [Nouveautés de Démarche Numérique](https://github.com/demarches-simplifiees/demarches-simplifiees.fr/releases)
* [Salon Tchap "Démarche Numérique"](https://www.tchap.gouv.fr/#/room/#demarchessimplifieesS454OP0:agent.dinum.tchap.gouv.fr)

## Choisir entre Démarche Numérique et Démat Social

|                                | [Démarche Numérique](https://demarche.numerique.gouv.fr/) | [Démat Social](https://demat.social.gouv.fr/)                                                      |
| ------------------------------ | --------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Entité porteuse                | SPM/DINUM                                                 | DNUM des Ministères Sociaux                                                                        |
| Hébergement                    | OVH                                                       | Cegedim                                                                                            |
| SecNumCloud                    | ✅                                                       | ❌                                                                                                 |
| HDS                            | ❌                                                       | ✅                                                                                                 |
| Connexion FranceConnect        | ✅                                                       | ❌                                                                                                 |
| Connexion ProConnect           | ✅                                                       | ❌                                                                                                 |
| Champs spécifiques Min Sociaux | n/a                                                       | <p>Champ NIR sécurisé<br>2 champs FINESS (avec lookup FINESS)<br>Champ RPPS (avec lookup RPPS)</p> |
| Montées de version             | \~tous les jours                                          | 3-12 mois de retard                                                                                |
| Numérotation des versions      | AAAA-MM-DD-version                                        | x.y.z                                                                                              |
| Accès Admin et Instructeur     | Internet et RIE                                           | RIE seulement                                                                                      |