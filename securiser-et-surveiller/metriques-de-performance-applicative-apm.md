---
icon: eyes
---

# Métriques de performance applicative (APM)

Ce document a pour objectif de fournir des connaissances de base sur certaines métriques clés dans la gestion d'une application. Elles permettent de comprendre le comportement d'une application et d'améliorer ses performances.

Ces indicateurs sont particulièrement utiles pour prioriser les [tests de charge](../../constuire-developper-deployer/tests-et-strategies/tests-de-performance.md).

Si l'infrastructure est gérée par un infogérant, c'est lui qui est responsable de la collecte des données et de leur mise à disposition.



### Recommandations

Il est fortement recommandé d'utiliser un outil d'observabilité comme **Sentry** pour connaître comment se comporte l'application en production, et avoir de la visibilité sur les améliorations possibles.

***

### Métriques d'affichage

Plusieurs métriques existent :&#x20;

* FCP : le temps que prend le premier contenu à apparaître.
* Vitesse de chargement : le temps que prend une page pour se charger chez le client.
* TBT : le temps où l'utilisateur ne peut utiliser son application.
* LCP : le temps que prend le contenu le plus grand pour apparaître.



Les experts [Design](../../preparer-et-lancer/les-differents-roles-et-metiers/designer.md) et [accessibilité](../../concevoir/accessibilite.md) peuvent accompagner sur ces sujets.

Plus d'informations sont présentes sur le [blog de Chrome](https://developer.chrome.com/docs/lighthouse/performance/first-contentful-paint?hl=fr).

#### Comment mesurer

* [LIghthouse](https://developer.chrome.com/docs/lighthouse) permet d'identifier des points à améliorer.
* Une expertise externe.
* Certains tests de bout en bout (end-to-end) comme avec [Playwright](https://playwright.dev/).



### Temps de réponse d'une requête HTTP

Il s'agit du temps qu'une requête prend pour que sa réponse revienne au client qui l'a envoyée.

#### Comment mesurer

* Utiliser un outil d'observabilité et constater les temps.
  * Le [suivi de requêt](https://sentry.io/product/tracing/)e (request tracing) permet de voir par quel système passe une requête et les temps de passage.
* Simuler des envois de requêtes depuis une API.

Ces actions sont dépendantes d'un infogérant si elles sont réalisées en production.

#### Comment améliorer

Plusieurs éléments dans le système peuvent impacter ces performances : connexions à des dépendances externes, code complexe, etc.

Il faut alors prioriser l'ajout d'un outil et la récupération de ces données



### Performance d'une fonctionnalité

Il s'agit du temps passé sur l'exécution du code pour une fonctionnalité, y compris la logique métier et les appels, sans intégrer le temps d'arrivée d'une requête et la réception de la réponse par le client.

#### Comment mesurer

* Pour les langages le permettant, l'[AOP](https://fr.wikipedia.org/wiki/Programmation_orient%C3%A9e_aspect) permet d'insérer des points de mesure à des endroits stratégiques.
* Des mesures manuelles peuvent être ajoutées pour qu'elles puissent être lues à posteriori.
* Des tests unitaires et/ou d'intégration.

#### Comment améliorer

La séquence de la fonctionnalité doit être déconstruite et chaque action analysée : appels API, requêtes en base de données, etc.



### Temps de réponse d'une requête à une dépendance externe

Il s'agit du temps qu'une requête prend pour être interprétée par une base de données, une API, etc. et que sa réponse revienne à l'appelant.

#### Comment mesurer

* Utiliser un outil de mesure.
* En utilisant l'AOP.

#### Comment améliorer

Les pistes d'améliorations peuvent dépendre de plusieurs facteurs comme la complexité de la requête ou le nombre de lectures/écritures.

Différentes pistes sont possibles alors :&#x20;

* Segmentation de la base de données selon la lecture et l'écriture.
* Simplification de requête SQL.
* Utilisation de requêtes par lot (batch).



### Outils de mesure

* [Sentry](https://sentry.io/welcome/) : recommandé et utilisé par la DNUM, supporte le [suivi de requêtes](https://sentry.io/product/tracing/).
* [Lighthouse](https://developer.chrome.com/docs/lighthouse) : pour différentes métriques front.
* [APM Elastic](https://www.elastic.co/observability/application-performance-monitoring) : s'intègre avec la suite ELK.
