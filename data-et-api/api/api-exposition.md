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

# Exposition

## Les questions à se poser

Quand on souhaite ouvrir une API, nous pouvons utiliser les questions "[QQOQCCP](https://fr.wikipedia.org/wiki/QQOQCCP)" qui nous permettent de mieux comprendre la situation et de définir une solution pertinente par rapport au besoin.

Ci-dessous se trouvent quelques-unes des questions qu'il pourrait être utile de se poser. _À noter que ces questions peuvent ne pas être pertinentes suivant les phases de développement du produit._

* **Quoi :** qu'est-ce qui sera consommé ?
  * Quelle donnée ?
  * Quelle sensibilité ?
* **Pourquoi :** Quel sera l'usage de la donnée ?
* **Qui :** Par qui la donnée sera-t-elle consommée ?
  * Des applications front-ends / back-ends ?
* **Où :** Où la donnée sera-t-elle demandée ?
  * Clients internes et/ou externes ?
* **Quand :** Quand sera-t-elle être consommée ?
  * Plage horaire ?
  * À quel moment dans une journée, semaine, etc. ?
* **Comment :** comment la donnée sera-t-elle consommée ?
  * Quel protocole d'échange (HTTP + JSON, GraphQL, gRPC) ?
    * Plus d'informations pourront être trouvées [ici](api-normes.md#solutions-proposées).
  * Lecture et/ou écriture ? Si écriture, pour quel type ? (mise à jour ou soumission de donnée entière)
* **Combien :** À quelle fréquence sera-t-elle consommée ?
  * Par jour, semaine, etc.

### Utilisation des réponses

La réponse (ou non-réponse) à ces questions nous apportent des informations sur les modalités d'exposition, telles que :

* Quel type de sécurité devra-t-on mettre en place pour garantir la bonne consommation de la donnée ?
  * Cela pourra dépendre du type d'API, la nature de la donnée, l'architecture réseau, etc.
* Quels seraient les usages "normaux" qui mettraient en évidence les usages "anormaux" ?
  * Exemple : nous savons que la donnée _D_ n'est consommée que tous les jours à la même heure, donc une consommation à une heure différente pourra être envisagé comme anormal.
* De quel niveau de traçabilité aurons-nous besoin ?
  * Qui a appelé, comment identifie-t-on, quand, d'où, sur quel point ?
* Comment les versions de l'API devront-elles être gérées et communiquées ?
* De quelle disponibilité aura-t-on besoin ?
* À quelle fréquence faudra-t-il mettre à jour la donnée ?

Ces questions ne sont pas exhaustives, mais donnent une idée des points à aborder lors de la conception et l'exposition d'une API.

## Types d'API selon l'usage

Nous distinguons plusieurs types d'API selon la population qui consommera la donnée :

* Les APIs publiques, où aucune authentification ou validation des comptes n'est généralement nécessaire ;
  * Exception faîte des APIs qui pourront demander des informations sur leurs consommateurs.
* Les APIs partenaires, où une création et/ou une validation des comptes pourra être envisagée ;
  * Exemples : autres organismes publics, éditeurs de logiciels, etc.
* Les APIs privées, donc non-ouvertes à l'extérieur.

Pour ce dernier type, la sécurité qu'on pourra mettre en place dépendra de plusieurs facteurs. Ces facteurs pourront être identifiés grâce aux questions précédentes.

## Ressources supplémentaires

* Comment désigner une API, d'Octo : https://blog.octo.com/designer-une-api-rest
