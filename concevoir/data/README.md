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
    visible: true
---

# Data

## Choix de solution pour le stockage de données

* Base de données relationnelle : [PostgreSQL](postgresql.md)
  * Exception : MySQL ou MariaDB lorsqu'il vient avec la solution (ex : Drupal)
* **Stockage de documents** :
  * **Stockage simple** : privilégier le stockage type S3 plutôt que NAS si l'hébergement le permet
  * **Pas de solution GED standard et souveraine** à date au MAS. Ne considérer une solution de GED dédiée que s'il y a manipulation intensive de documents, et le besoin fort de fonctionnalités au-delà de la consultation (partage à des acteurs externes, travail collaboratif en édition...).
* **Base de données NoSQL** : pas de besoin identifié.
  * Des traces de MongoDB dans l'organisation
  * des [indications sur Elasticsearch ici](elasticsearch.md)

## Accès aux données

### Mapping objet-relationnel (ORM)

Une application métier DEVRAIT utiliser un framework de Mapping Objet-Relationnel (ORM) pour de nombreuses raisons :

* **Normalisation et réduction du code** d'accès aux données, meilleure maintenabilité (ex : renommage en un point) et testabilité (test unitaire auto des DAO, pas de code SQL). Moins de code = moins de bug !
* **Performance** : configuration d'un cache de niveau 2 pour les données à variation lente (données référentielles) et éventuellement d'un cache de niveau 1 pour les données métier vivantes (transactions)
* **Sécurisation** : protection native contre les injections SQL et les rafales de requêtes
* **Evolutivité** : Moindre adhérence à la technologie de base de données\
  &#xNAN;_&#x45;xemples : Hibernate pour Java, TypeORM pour TypeScript, Prisma_
