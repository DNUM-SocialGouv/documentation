# PostgreSQL

[PostgreSQL](https://www.postgresql.org/) est un système de gestion de base de données
(_[SGBD](https://fr.wikipedia.org/wiki/Syst%C3%A8me_de_gestion_de_base_de_donn%C3%A9es)_, ou _DBMS_ en anglais) sous
licence BSD (donc [libre](https://fr.wikipedia.org/wiki/Licence_libre)), qui est utilisé depuis maintenant depuis
plusieurs années par diverses organisations.

C'est un SGBD relationnel, c'est-à-dire que les entités sont liées par des relations avec une multiplicité, exemples :

- Une salle de cinéma peut avoir entre une et plusieurs places, mais ne contient qu'un écran.
- Un écran d'une salle de cinéma n'est associé qu'à une salle.

PostgreSQL est le choix **par défaut** quand un nouveau produit a besoin d'une base de données. Ainsi, si nous
considérons d'autres options (autres bases relationnelles, bases non-relationnelles, etc.), celles-ci sont toujours
comparées par rapport à ce qu'elles pourraient apporter de plus par rapport à PostgreSQL.

Un exemple est présent sur la [page d'ElasticSearch](elasticsearch.md).
