# Tests de performance

Ce type de tests consiste à vérifier la performance des fonctionnalités d'une application.

Pour cela, une montée en charge est simulée pour s'assurer que le temps de réponse reste acceptable.

Il est courant de mandater un prestataire pour la réalisation de ces tests. L'équipe détermine alors les cas à tester et les conditions de réussite des tests.

Il est tout à fait possible pour l'équipe produit d'exécuter certains tests en autonomie, ce qui permet d'itérer plus rapidement.

Dans le cas où le produit numérique est infogéré, la collaboration avec l'infogérant est indispensable pour s'assurer de tests représentatifs et pour ne pas perturber l'infrastructure.

De plus, ces tests permettent de vérifier la résilience de l'application et l'infrastructure : scalabilité, redondance, etc.

### Cas à tester

Il est recommandé de lister d'abord les cas les plus importants à tester, tels que :

* Les parcours utilisateurs critiques (qui ne doivent pas échouer).
* Les parcours à contrainte forte de performance (ex : réponse en moins de _x_ secondes).
* Les parcours susceptibles d'être utilisés par un nombre croissant d'utilisateurs (ex : montée en charge prévue).
* À l'inverse, tester tous les cas n'est pas un gage de qualité.

Un échange avec le [responsable métier](../../preparer-et-lancer/les-differents-roles-et-metiers/responsable-metier.md) et/ou le [co-chef de produit](../../preparer-et-lancer/les-differents-roles-et-metiers/co-chef-produit.md) permet d'identifier les cas pertinents.

### Considérations importantes

* Prendre en compte la richesse du réseau : ne pas tester à partir du réseau interne qui ne simulerait pas les conditions réelles (WAF, réseaux privés, passerelles, gateways, etc.)
* Tester en environnement iso-production : les utilisateurs étant en production, pour être sûr de fournir un service adapté, exécuter ces tests sur un environnement proche. Ne pas uniquement se baser sur des tests exécutés sur les postes de développement ou depuis les serveurs d'une chaîne de CI.
* Éviter les sous-estimations : tester avec les conditions prévues et tester avec des conditions plus poussées.
* Identifier les systèmes impactés par les tests : en cas de communication avec des APIs externes, informer les acteurs et prendre des actions adaptées si nécessaire (ex : bouchons).

### Quand faire appel à une prestation externe

Bien qu'une prestation puisse être onéreuse, elle est préférable suivant le contexte :

* **Les cas pertinents à tester ne sont pas encore identifiés** et une expertise externe peut aider à les définir.
* **L'équipe n'a pas le temps** : une expertise externe permet d'aider la rédaction et l'exécution des tests.
* **L'équipe n'a pas les compétences** ni le temps de les acquérir : une expertise externe permet de démarrer en évitant les écueils et de monter en compétence.
* **L'équipe n'a pas la maitrise de l'hébergement** : l'infogérant pourrait prendre en charge une partie des actions.

A noter que toute sollicitation externe (contractualisation, mobilisation de l'expert, prise de connaissance, etc.) allonge la boucle de feedback par rapport à une gestion interne par l'équipe

### Outils sur le marché

Certains prestataires s'en remettent à des solutions propriétaires ou des tests configurés manuellement.\
Voici des solutions alternatives open-source :

* [**K6 (notre recommandation)**](https://k6.io/) : propose une API JS/TS.
* [Gatling](https://docs.gatling.io/) : propose une API JS/TS et Java.
* [Artillery](https://github.com/artilleryio/artillery) : propose une API YAML, et s'intègre avec Playwright.
* [JMeter](https://jmeter.apache.org/) : propose une API Java.
