# Elasticsearch

[Elasticsearch](https://www.elastic.co/fr/elasticsearch) est une base de données optimisée pour les recherches et
l'analytique.

## Questions à se poser

Ci-dessous des questions à se poser lorsqu'il est considéré d'intégrer ElasticSearch dans une nouvelle stack, ou une
stack existante :

### Besoin

- Quels besoins de l'application ElasticSearch couvre-t-il, et comment ?
- PostgreSQL étant notre base de donnée relationnelle par défaut, comment ES se démarque-t-il dans la couverture des
  besoins ?

### Performance

- Comment peut-on mesurer la performance d'ES par rapport à d'autres solutions répondant également au besoin ?
- Quelles sont ces mesures ?

### Maintenabilité

- Comment l'opérabilité d'ES a été prise en compte ?
  - Observabilité, redondance, résilience, etc.
- Si on ajoute ES à une stack existante, à quel point le coût (hébergement et maintenance) et la complexité d'avoir une
  deuxième base de données a été pris en compte ?
- À quel point l'hébergeur est-il capable de supporter ES ?

### Sécurité et conformité

- Quelles données seront stockées dans ES ?
- Quel est leur niveau de criticité ?

### Coût

- Si ES est considéré pour remplacer une solution existante, quels efforts (coûts, temps, ressources humaines, etc.)
  sont nécessaires pour ce remplacement ?
- Quels efforts sont nécessaires pour maintenir ES dans le temps ?

## Incident dû à la licence

Elastic, l'entreprise proposant l'offre commerciale autour d'ELasticSearch et d'autres produits (Kibana, Logstash, etc.)
a décidé en 2021 de ne plus proposer de mise à jour sous licence open-source. AWS (Amazon Web Services) lance alors,
avec le soutien d'autres acteurs, [OpenSearch](https://aws.amazon.com/what-is/opensearch/), qui est un fork (déviation),
une version basée sur la dernière version open-source d'Elasticsearch tout en continuant à la faire évoluer grâce à la
communauté.

Depuis Elastic s'est ravisé et a proposé qu'Elasticsearch soit de nouveau
[open-source](https://www.elastic.co/blog/elasticsearch-is-open-source-again) (sous conditions).
