# Tests de performance

Ce type de tests consiste à vérifier la performance des fonctionnalités d'une application.

Pour cela, une montée en charge est simulée pour s'assurer que le temps de réponse reste acceptable.

Il est courant de mandater un prestataire pour la réalisation de ces tests. L'équipe détermine alors les cas à tester et les conditions de réussite des tests.

Il est tout à fait possible pour l'équipe produit d'exécuter certains tests en autonomie, ce qui permet d'itérer plus rapidement.

Dans le cas où le produit numérique est infogéré, la collaboration avec l'infogérant est indispensable pour s'assurer de tests représentatifs et pour ne pas perturber l'infrastructure.

### Cas à tester

Il est recommandé de lister d'abord les cas les plus importants à tester, tels que :

* Les parcours utilisateurs critiques (qui ne doivent pas échouer).
* Les parcours à contrainte forte de performance (ex : réponse en moins de _x_ secondes).
* Les parcours susceptibles d'être utilisés par un nombre croissant d'utilisateurs (ex : montée en charge prévue).

De plus, ces tests permettent de vérifier la résilience de l'application et l'infrastructure : scaling, redondance, etc.

Un échange avec le [responsable métier](../../preparer-et-lancer/les-differents-roles-et-metiers/responsable-metier.md) et/ou le [co-chef de produit](../../preparer-et-lancer/les-differents-roles-et-metiers/co-chef-produit.md) permet d'identifier les cas pertinents. À l'inverse, tout tester n'est pas un gage de qualité et le risque d'investir de l'effort sur des parcours secondaires est plus grand.



### Considérations importantes

* Prendre en compte la richesse du réseau : ne pas tester à partir du réseau interne qui ne simulerait pas les conditions réelles (WAF, réseaux privés, passerelles, gateways, etc.)
* Tester en environnement iso-production : les utilisateurs étant en production, pour être sûr de fournir un service adapté, exécuter ces tests sur un environnement approchant. Ne pas uniquement se baser sur des tests exécutés sur les postes de développement ou depuis les serveurs d'une chaîne de CI.
* Éviter les sous-estimations : tester avec les conditions prévues et tester avec des conditions plus poussées.
* Identifier les systèmes impactés par les tests : en cas de communication avec des APIs externes, informer les acteurs et prendre des actions adaptées si nécessaire (ex : bouchons).



### Quand faire appel à une prestation externe

Bien que faire appel à une prestation puisse être onéreux, elle peut être la bonne chose à faire suivant le contexte :

* Les cas à tester et leur pertinence ne sont pas encore identifiés : cela peut rentrer dans la mission d'une expertise externe.
* La rédaction et l'exécution des cas de tests prend trop de temps : il faut penser aux cas importants et aux conditions de réussite de chaque test.
* Le coût d'apprentissage et d'exécution est trop élevé : la délégation de ces tests est alors judicieuse.
* La maîtrise de l'infrastructure est du côté de l'infogérance : l'équipe n'a alors qu'une maîtrise partielle, voire nulle, sur les environnements. Une expertise externe pourra intervenir pour collaborer avec l'infogérance pour mettre en place l'environnement de test.

À part le prix, la boucle de feedback d'une telle sollicitation est plus élevée que si ces tests étaient gérés en interne.



### Outils sur le marché

Certains prestataires s'en remettent à des solutions propriétaires ou des tests configurés manuellement.\
Des solutions alternatives existent :&#x20;

* [**K6**](https://k6.io/) **: outil recommandé**, propose une API JS/TS.
* [Gatling](https://docs.gatling.io/) : propose une API JS/TS et Java.
* [Artillery](https://github.com/artilleryio/artillery) : propose une API YAML, et s'intègre avec Playwright.
* [JMeter](https://jmeter.apache.org/) : propose une API Java.

