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

# PostgreSQL

[PostgreSQL](https://www.postgresql.org/) est un système de gestion de base de données ([_SGBD_](https://fr.wikipedia.org/wiki/Syst%C3%A8me_de_gestion_de_base_de_donn%C3%A9es), ou _DBMS_ en anglais) sous licence BSD (donc [libre](https://fr.wikipedia.org/wiki/Licence_libre)), qui est utilisé depuis maintenant depuis plusieurs années par diverses organisations.

C'est un SGBD relationnel, c'est-à-dire que les entités sont liées par des relations avec une multiplicité, exemples :

* Une salle de cinéma peut avoir entre une et plusieurs places, mais ne contient qu'un écran.
* Un écran d'une salle de cinéma n'est associé qu'à une salle.

PostgreSQL est devenue la référence de la base de données open-source dans l'industrie depuis déjà quelques années (rachat de solutions concurrentes, évolutions de PostgreSQL pour atteindre plusieurs usages). C'est aujourd'hui un outil incontournable dans les stacks requérant un stockage structuré de données.

PostgreSQL est le choix **par défaut** quand un nouveau produit a besoin d'une base de données. Ainsi, si nous considérons d'autres options (autres bases relationnelles, bases non-relationnelles, etc.), celles-ci sont toujours comparées par rapport à ce qu'elles pourraient apporter de plus par rapport à PostgreSQL, et chaque comparaison doit être **solidement argumentée** sur des points tels que :

* La sécurité,
* Le coût d'ajout,
* La performance,
* La maintenabilité,
* etc.

Solidement, ici, signifie que des arguments mesurables, concrets et ciblés, et argumentés doivent être apportés.

Un exemple de questionnement est présent sur la [page d'ElasticSearch](../../../../Architecture/outils/elasticsearch.md).
