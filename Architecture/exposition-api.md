# Exposition d'API

## Les questions à se poser

Quand on souhaite ouvrir une API, nous pouvons utiliser les questions "[QQOQCCP](https://fr.wikipedia.org/wiki/QQOQCCP)"
qui nous permettent de mieux comprendre la situation et de définir une solution pertinente par rapport au besoin.

Ci-dessous se trouvent quelques-unes des questions qu'il pourrait être utile de se poser :

- **Quoi :** qu'est-ce qui sera consommé ? 
  - Quelle donnée ?
  - Pour quelle criticité ?
- **Qui :** Par qui la donnée sera-t-elle consommée ?
  - Des applications front-ends / back-ends ?
- **Où :** Où la donnée sera-t-elle demandée ?
  - Clients internes et/ou externes ?
- **Quand :** Quand sera-t-elle être consommée ?
    - Plage horaire ?
    - À quel moment dans une journée, semaine, etc. ?
- **Comment :** comment la donnée sera-t-elle consommée ?
  - Quel protocole d'échange (HTTP + JSON ? GraphQL ? gRPC ?) ?
    - Plus d'informations pourront être trouvées [ici](normes/norme-api.md).
  - Lecture et/ou écriture ? Si écriture, pour quel type ? (mise à jour ou soumission de donnée entière)
- **Combien :** À quelle fréquence sera-t-elle consommée ?
  - Par jour, semaine, etc.
- **Pourquoi :** Quel sera l'usage de la donnée ?

### Utilisation des réponses

La réponse (ou non-réponse) à ces questions nous apportent des informations sur les modalités d'exposition, telles que :

- Quel type de sécurité devra-t-on mettre en place pour garantir la bonne consommation de la donnée ?
- Quels seraient les usages "normaux" qui mettraient en évidence les usages "anormaux" ?
- De quel niveau de traçabilité aurons-nous besoin ?
  - Qui a appelé, comment identifie-t-on, quand, d'où, sur quel point ?
- Comment les versions de l'API devront-elles être gérées et communiquées ?
- De quelle disponibilité aura-t-on besoin ?
- À quelle fréquence faudra-t-il mettre à jour la donnée ?

Ces questions ne sont pas exhaustives, mais donnent une idée des points à aborder lors de la conception et l'exposition 
d'une API.
