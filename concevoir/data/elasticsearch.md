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

# ElasticSearch

[ElasticSearch](https://www.elastic.co/fr/elasticsearch) ou "ES" est une base de données optimisée pour les recherches et l'analytique.

## Questions à se poser

* **Besoin**
  * Quels besoins de l'application justifient ES ?
  * Que couvre ES en plus de PostgreSQL (notre base de donnée relationnelle par défaut) ?
* **Performance**
  * Comment mesurer la performance d'ES par rapport à d'autres solutions répondant également au besoin ?
  * Quelles sont ces mesures ?
* **Maintenabilité**
  * Comment l'exploitabilité d'ES a été prise en compte (observabilité, redondance, résilience, etc.) ?
  * L'hébergeur et l'infogérant supportent-ils ES ?
* **Sécurité et conformité**
  * Quelles données sont stockées dans ES ?
  * Quel est leur niveau de criticité ?
* **Coût**
  * Si ES est ajouté à une stack existante, le coût total d'une deuxième base de données a t-il bien été pris en compte ?
  * Si ES est considéré pour remplacer une solution existante, quels efforts (coûts, temps, ressources humaines, etc.) sont nécessaires pour ce remplacement ?
  * Quels efforts sont nécessaires pour maintenir ES dans le temps ?

## Incident dû à la licence

Elastic, l'entreprise proposant l'offre commerciale autour d'ES et d'autres produits (Kibana, Logstash, etc.) a décidé en 2021 de ne plus proposer de mise à jour sous licence open-source. AWS (Amazon Web Services) lance alors, avec le soutien d'autres acteurs, [OpenSearch](https://aws.amazon.com/what-is/opensearch/), qui est un fork (déviation) de la dernière version open-source d'ES tout en continuant à la faire évoluer grâce à la communauté.

Depuis Elastic s'est ravisée et propose de nouveau [ES en open-source](https://www.elastic.co/blog/elasticsearch-is-open-source-again) (sous conditions).
