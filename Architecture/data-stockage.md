---
icon: floppy_disk
---

# Stockage et accès aux données

## Choix par défaut pour le stockage de données

- SGBDR : [PostgreSQL](outils/postgresql.md)
- NoSQL : MongoDB
- Stockage de documents : S3 compatible plutôt que NAS _Privilégier les stockages managés_ si l'hébergement le permet.

## Mapping objet-relationnel (ORM)

Une application métier devrait systématiquement utiliser un framework de Mapping Objet-Relationnel (ORM) pour de
nombreuses raisons :

- **Normalisation et réduction du code** d'accès aux données, meilleure maintenabilité (ex : renommage en un point) et
  testabilité (test unitaire auto des DAO, pas de code SQL). Moins de code = moins de bug !
- **Performance** : configuration d'un cache de niveau 2 pour les données à variation lente (données référentielles) et
  éventuellement d'un cache de niveau 1 pour les données métier vivantes (transactions)
- **Sécurisation** : protection native contre les injections SQL et les rafales de requêtes
- Moindre adhérence à la technologie de base de données\
  _ex : Hibernate_
