---
description: Aussi nommés tests end-to-end, ou e2e.
---

# Tests de bout en bout

Ces tests vérifient l'ensemble de l'application et ses dépendances :

* Soit en simulant une action utilisateur sur le front, soit en envoyant une requête HTTP à l'API (si aucun front).
* En vérifiant que le résultat attendu est conforme aux attentes (code d'erreur, affichage, etc.)

Dans la [pyramide de tests](https://martinfowler.com/articles/practical-test-pyramid.html#TheTestPyramid), ce sont les tests les plus en haut car :

* Ils prennent du temps à s'exécuter : au moins plusieurs secondes pour chaque test.
  * La boucle de feedback est donc longue.
* Ils sont les plus coûteux à mettre en place : toute l'architecture du projet doit être instanciée.

Ainsi, les parcours les plus importants pour les utilisateurs devraient être testés. Plusieurs critères de choix existent :

* Nombre d'utilisation :
  * Exemple : 90% des utilisateurs font cette action au moins 5 fois par jour.
* Chemin critique :
  * Exemple : l'accès à l'application se fait par une authentification.
* etc.



Un dialogue entre les parties prenantes est nécessaire pour déterminer quels comportements mériteraient d'être testés de cette manière.



### Outil privilégié

Nous recommandons [Playwright](https://playwright.dev/) pour l'écriture et l'exécution de ces tests :&#x20;

* Activement maintenu.
* Supporte plusieurs plateformes (NodeJS, Java, etc.).
* Bien documenté.
* **Adopté au sein de la DNUM**.
