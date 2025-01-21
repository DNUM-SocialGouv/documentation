# Elasticsearch

[Elasticsearch](https://www.elastic.co/fr/elasticsearch) est une base de données optimisée pour les recherches et
l'analytique.

## Questions à se poser

Ci-dessous des questions à se poser lorsqu'il est considéré d'intégrer ElasticSearch dans une nouvelle stack, ou une
stack existante :

### Besoin

- Quels besoins de l'application ElasticSearch couvre-t-il, et comment ?
- Par rapport à d'autres outils du marché, comment ES se démarque dans la couverture des besoins ?
- Si ES est considéré pour remplacer une solution existante, quels efforts (coûts, temps, ressources humaines, etc.)
  sont nécessaires pour ce remplacement ?

### Performance

- Compte-tenu des besoins, en quoi ES est plus performant que d'autres solutions ?
- Comment l'opérabilité d'ES a été pris en compte ?
  - Observabilité, redondance, résilience, compétences, etc.

### Sécurité et conformité

TODO

## Incident dû à la licence

Elastic, l'entreprise proposant l'offre commerciale autour d'ELasticSearch et d'autres produits (Kibana, Logstash, etc.)
a décidé en 2021 de ne plus proposer de mise à jour sous licence open-source. AWS (Amazon Web Services) lance alors,
avec le soutien d'autres acteurs, [OpenSearch](https://aws.amazon.com/what-is/opensearch/), qui est un fork (déviation),
une version basée sur la dernière version open-source d'Elasticsearch tout en continuant à la faire évoluer grâce à la
communiquée.

Depuis Elastic s'est ravisé et a proposé qu'Elasticsearch soit de nouveau
[open-source](https://www.elastic.co/blog/elasticsearch-is-open-source-again) (sous conditions).
