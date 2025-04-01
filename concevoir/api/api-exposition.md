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

# Exposition d'API

## Recommandations
- En matière d'échanges de données, c'est toujours le [Référentiel Général d'Interopérabilité (RGI)](https://www.numerique.gouv.fr/publications/interoperabilite/) qui fait foi
- Une **API REST** est suffisante dans la grande majorité des cas
- Un **webhook** est un mécanisme d'appels sortants (callout) basé sur HTTP. Il permet d'envoyer une notification du producteur vers le(s) consommateur(s). C'est une API REST simple, souvent sans payload, souvent utilisée pour l'intégration avec des logiciels/progiciels.
- **GraphQL** est un langage de requête pour API permettant aux clients de demander une grappe de données en un sel appel, tout en ne demandant que les données nécessaires.
- Le protocole SOAP est à éviter sauf contraintes existantes.

## Les questions à se poser

Quand on souhaite ouvrir une API, nous pouvons utiliser les questions "[QQOQCCP](https://fr.wikipedia.org/wiki/QQOQCCP)" qui nous permettent de mieux comprendre la situation et de définir une solution pertinente par rapport au besoin.

Ci-dessous se trouvent quelques questions utiles. _Ces questions peuvent ne pas être pertinentes suivant les phases de développement du produit._

* **Quoi :** quelle donnée est consommée ?
  * Quelle sensibilité ?
* **Pourquoi :** Quel est l'usage de la donnée ?
* **Qui :** par qui la donnée est-elle consommée ?
  * Des applications front-ends / back-ends ?
* **Où :** où la donnée sera-t-elle demandée ?
  * Clients internes et/ou externes ?
* **Quand :** quand la donnée est-elle consommée ?
  * Plage horaire ?
  * À quel moment dans une journée, semaine, etc. ?
* **Comment :** comment la donnée est-elle consommée ?
  * Quel protocole d'échange (HTTP + JSON, GraphQL, gRPC) ?
    * Plus d'informations [ici](api-normes.md#solutions-proposées).
  * Lecture et/ou écriture et/ou modification ?
* **Combien :** À quelle fréquence la donnée est-elle consommée (par jour, semaine, etc.) ?

### Utilisation des réponses

Les réponses à ces questions apportent des informations sur les modalités d'exposition, telles que :

* Le type de sécurité à mettre en place pour garantir la bonne consommation de la donnée
  * Cela pourra dépendre du type d'API, la nature de la donnée, l'architecture réseau, etc.
* Les usages "normaux" qui mettraient en évidence les usages "anormaux"
  * Exemple : nous savons que la donnée _D_ n'est consommée que tous les jours à la même heure, donc une consommation à une heure différente pourra être envisagé comme anormal.
* Le niveau de traçabilité aurons-nous besoin ?
  * Qui a appelé, comment identifie-t-on, quand, d'où, sur quel point ?
* Comment les versions de l'API sont-elles gérées et communiquées ?
* De quelle disponibilité a-t-on besoin ?
* La fréquence à laquelle il faut mettre à jour la donnée

Ces questions ne sont pas exhaustives, mais donnent une idée des points à aborder.

## Types d'API selon l'usage

Nous distinguons plusieurs types d'API selon la population qui consomme la donnée :

* Les APIs publiques, où aucune authentification ou validation des comptes n'est généralement nécessaire ;
  * Exception faîte des APIs qui pourront demander des informations sur leurs consommateurs.
* Les APIs partenaires, où une création et/ou une validation des comptes pourra être envisagée ;
  * Exemples : autres organismes publics, éditeurs de logiciels, etc.
* Les APIs privées, donc non-ouvertes à l'extérieur de l'organisation.

## Ressources supplémentaires

* Comment designer une API, par OCTO Technology : https://blog.octo.com/designer-une-api-rest
