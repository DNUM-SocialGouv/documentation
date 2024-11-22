# Principes d'architecture

Il est impératif de poser quelques grands principes apportant des garanties sur les aspects techniques ou organisationnels afin de répondre à plusieurs ambitions : 
* proposer une meilleure expérience sur nos SI pour les citoyens et les agents
* faciliter le travail des équipes de la DNUM et de nos partenaires
* simplifier notre SI

## Grands principes

### 1 - Interopérabilité

Les systèmes doivent proposer l'accès à leurs données via des mécanismes standards et non liés à une technologie ou à un éditeur spécifique.

Cela permet de découpler l'accès à la donnée de la solution technique et donc de mieux gérer l'évolution du parc sur le long terme.

### 2 - La donnée au centre

Il est impératif d'avoir un propriétaire clairement identifié pour chaque point de donnée. Cette donnée doit venir d'un unique système/SI agissant comme source de vérité pour l'ensemble des autres systèmes.

Les SI doivent être responsables de la création, gestion et consommation de la donnée. En valorisant au mieux les sources existantes il devient plus simple pour tous de simplifier l'expérience utilisateur ainsi que réduire nos problématiques d'intégration.

### 3 - Sécurisé par défaut

Une application doit proposer par défaut lors de sa conception le niveau de sécurité nécessaire pour ses usagers et les systèmes qui en dépendent.

### 4 - Transparence et interdépendance

Les applications communiquent clairement sur leurs évolutions, leur état de santé et proposent de la donnée (sous forme de KPI, log, traces, ...) permettant aux systèmes ou équipes qui en dépendent d'avoir de manière transparente les informations nécessaires à leur activité.

Les décisions structurantes et leurs implications, particulièrement en matière d'architecture et conception, sont partagées et documentées ; par exemple par des ADR ([Architecture Decision Record voire Any Decision Record](https://adr.github.io/)).

### 5 - L'art de l'essentiel

Il est nécessaire d'être évolutif dans la conception de la solution, le juste niveau de complexité, d'exigences ou de ressources doit être jugé à l'aune du besoin réel.

Une application en microservices sous kubernetes n'est sans doute pas nécessaire pour faire un formulaire de contact.

Les choix de conception doivent être raisonnables et raisonnés.