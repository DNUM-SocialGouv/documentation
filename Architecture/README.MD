# Architecture

Il est impératif de poser quelques grands principes apportant des garanties sur les aspects techniques ou
organisationnels afin de répondre à plusieurs ambitions :

- Offrir une meilleure expérience sur nos SI pour les usagers et les agents
- Faciliter le travail des équipes de la DNUM et de ses partenaires
- Simplifier notre SI

## La raison d'être

L'architecture est à la croisée des chemins entre les différents métiers du numérique. Un produit numérique se faisant
rarement en isolation, il s'inscrit dans un écosystème complexe. Que ce soit sur la partie amont lors
de la captation du besoin ou pendant les phases de développement voire de maintenance, les architectes sont là pour
**fluidifier les échanges** entre équipes et s'assurer de l'adéquation entre le besoin et la façon d'y répondre. Pour se
faire l'architecture se positionne comme un accélérateur pour fournir aux chefs de produits/projets et leurs équipes les
informations, outils et méthodes dont ils ont besoin pour interagir de manière sereine avec notre écosystème.

### Les missions de l'architecture dans l'organisation

L'architecture à 3 missions principales pour la DNUM et son écosystème :

- Faire vivre un référentiel de standards et normes partagés sur son périmètre et en alignement avec les autres parties
  prenantes en particulier concernant les aspects [développement](../Developpement/README.md),
  [DevSecOps](../DevSecOps/README.md) et [hébergement](../Hebergement/README.md)
- Travailler à l'amélioration continue des SI et applications en développant un catalogue de solutions réutilisables et
  d'offres de services communes centrés sur des cas d'usages s'inscrivant dans une
  [démarche de rationalisation](./demarche.md)
- Accompagner les équipes projets dans leurs besoins via notre offre de services

## Grands principes

### 1 - Interopérabilité

Les systèmes doivent proposer l'accès à leurs données via des mécanismes standards et non liés à une technologie ou à un
éditeur spécifique. Cela permet de découpler l'accès à la donnée de la solution technique et donc de mieux gérer
l'évolution du parc sur le long terme.

### 2 - La donnée au centre

Il est impératif d'avoir un propriétaire clairement identifié pour chaque point de donnée. Cette donnée doit venir d'un
unique système/SI agissant comme source de vérité pour l'ensemble des autres systèmes. Les SI doivent être responsables
de la création, gestion et consommation de la donnée. En valorisant au mieux les sources existantes il devient plus
simple pour tous de simplifier l'expérience utilisateur ainsi que réduire nos problématiques d'intégration.

### 3 - Transparence et interdépendance

Les applications communiquent clairement sur leurs évolutions, leur état de santé et proposent de la donnée (sous forme
de KPI, log, traces...) permettant aux systèmes ou équipes qui en dépendent d'accéder aux informations nécessaires à leur activité.

Les décisions structurantes et leurs implications, particulièrement en matière d'architecture et conception, sont
partagées et documentées ; par exemple par des ADR ou [Architecture Decision Record](https://adr.github.io/).

### 4 - L'art de l'essentiel

Il est nécessaire d'être évolutif dans la conception de la solution, le juste niveau de complexité, d'exigences ou de
ressources doit être jugé à l'aune du besoin réel. Une application en microservices sous Kubernetes n'est sans doute pas
nécessaire pour faire un formulaire de contact.
