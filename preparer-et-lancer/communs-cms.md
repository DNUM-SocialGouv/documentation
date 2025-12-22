# ♻️ Gestion de contenus (CMS)

## Usages

Les solutions de CMS répondent à différents besoins :
* **Site institutionnel ou un site éditorial** : un CMS Headful est adapté, mais ne permet pas d'implémenter de logique métier
* **Application métier avec des contenus éditoriaux embarqués** : un CMS headless est plus approprié
* **Approche hybride application métier / site éditorial** : pas de solution simple et transparente. Il faut faire des compromis (2 solutions avec un style similaire, sous-domaines DNS, gestion du contenu par l'équipe produit, etc.)

## Les CMS aux Ministères Sociaux
* **Ondine** est le socle des sites éditoriaux des Ministères Sociaux
* [**Sites Conformes (anc. Sites Faciles**](https://sites.beta.gouv.fr/) est un commun numérique interministériel et vient challenger le socle Ondine.
* [**Strapi**](https://strapi.io) est un CMS headless Open source français très utilisé dans la sphère BetaGouv
* [**Grist**](communs-grist.md) permet de construire un CMS headless minimal et 0-déploiement

## Comparaison des CMS

Points communs :
* Recherche texte intégrale, y compris dans les pièces-jointes

|                          | **Socle Ondine**       | **Sites Conformes**         | **Strapi**           | **Grist**          |
| ------------------------ | ---------------------- | --------------------------- | -------------------- | ------------------ |
| CMS Headful (IHM)        | Oui       l            | Oui                         | Non                  | Non                |
| CMS Headless             | Non                    | Oui                         | Oui                  | Oui (contenu brut) |
| Entité porteuse          | SG/DICOM               | SPM/DINUM                   | Strapi               | SPM/DINUM          |
| Permet le dév spécifique | Non                    | Oui                         | Oui                  | Oui                |
| Recherche full-text      | Oui                    | Oui                         | Oui                  | Non                |
| ProConnect natif         | Non                    | Oui                         | n/a                  | n/a                |
| Conformité RGAA          | 50% des critères       | 82% des critères            | Non                  | n/a                |
| DSFR natif               | Oui                    | Oui                         | n/a                  | n/a                |
| Open source              | Non                    | Oui                         | Oui                  | Oui                |
| Stack technique          | Varnish + Drupal + PHP | Wagtail + Django + Python   | Node.js              | Python             |
| Stockage de données      | MariaDB                | PostgreSQL                  | PostgreSQL           | n/a (SaaS)         |
| Stockage index           | Solr                   | PostgreSQL ou Elasticsearch | PostgreSQL, ES...    | n/a (SaaS)         |
| Stockage de documents    | GlusterFS              | S3                          | S3                   | n/a (SaaS)         |
| Conformité RGS           | Oui                    | n/a                         | n/a                  | Oui                |
| Montées de version       | Par l'équipe socle     | Par l'équipe produit        | Par l'équipe produit | Par l'équipe socle |
| Hébergement Min Sociaux  | Cegedim (cible Atlas)  | Atlas                       | Atlas                | n/a (SaaS)         |