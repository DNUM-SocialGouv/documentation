---
description: Aussi nommés tests end-to-end, ou e2e.
---

# Tests de bout en bout

Ces tests vérifient l'ensemble des couches de l'application et ses dépendances :

* Soit en simulant une action utilisateur sur le front, soit par une requête HTTP à l'API (si aucun front).
* En vérifiant que le résultat attendu est conforme aux attentes (code d'erreur, affichage, etc.)

Ces tests sont tout en haut de la [pyramide des tests](https://martinfowler.com/articles/practical-test-pyramid.html#TheTestPyramid) :

* **Boucle de feedback plus longue** : chaque test prend au moins plusieurs secondes à s'exécuter
* **Plus coûteux** : toute l'architecture du projet doit être instanciée.

Seuls les parcours les plus importants pour les utilisateurs doivent être testés. Un dialogue entre les parties prenantes est nécessaire pour déterminer quels comportements méritent d'être testés de bout en bout :
  * Taux d'utilisation (ex : 90% des utilisateurs font cette action au moins 5 fois par jour)
  * Chemin critique (ex : l'accès à l'application se fait par une authentification)
  * etc.

### Outil privilégié

Nous recommandons [Playwright](https://playwright.dev/) pour l'écriture et l'exécution de ces tests :&#x20;

* Activement maintenu.
* Supporte plusieurs plateformes (NodeJS, Java, etc.).
* Bien documenté.
* **Adopté au sein de la DNUM**.
