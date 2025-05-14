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

# Tests et stratégies

## Front

### Outillage

Nous utilisons [Jest](https://jestjs.io/) ou [Vitest](https://vitest.dev/guide/), et **Vitest** est notre choix par défaut :

* Temps d’exécution des tests inférieur à Jest ;
* Moins de dépendances lourdes, car Vite fourni plus de choses "out-of-the-box" ;
* Moins de configuration pour l'utiliser.

Nous utilisons également [TestingLibrary](https://testing-library.com/), qui nous permet d'écrire des tests unitaires et des tests d'intégration.

Enfin, afin de bien tester les appels API, nous utilisons aussi [JestMockAdapter](https://www.npmjs.com/package/jest-mock-axios) pour Axios ou [JestFetchMock](https://www.npmjs.com/package/jest-fetch-mock) pour Fetch.

Ces plugins nous facilitent les tests pour les différents cas :

* Réponse 2XX (OK)
* Erreur métier (4XX)
* Erreur serveur (5XX)

### Stratégie

Nous nous servons de la couverture de test afin d'identifier les composants peu ou pas testés, ce qui nous donne une idée de là où nous devons accentuer notre effort.

Nous testons unitairement chaque composant, onglet et page en fonction de l'articulation de l'application front.

Si l'application utilise des contextes, nous testons chaque composant, onglet et page en 2 étapes :

1. Avec les valeurs par défaut du contexte ;
2. Avec des valeurs différentes.

## Back (Node)

### Outillage

Pareillement aux outils utilisés [côté frontend](./#front), nous utilisons également Jest et Vitest pour les backends.

**Outils recommandés**

* Jest : outil de test principal,
* [Supertest](https://www.npmjs.com/package/supertest) : pour tester les points d'entrée HTTP,
* [MSW](https://mswjs.io/) : pour simuler les appels API externes,
* [Sinon](https://sinonjs.org/) : pour créer des spies, stubs et mocks afin de tester le comportement des fonctions, des dépendances et des appels d’API sans réellement exécuter leur logique complète,
* [ts-jest](https://www.npmjs.com/package/ts-jest) : pour gérer le transpileur TypeScript.

### Stratégie

1. **Les tests unitaires** doivent couvrir chaque unité fonctionnelle : cela peut être une classe ou un ensemble de fichiers couvrant une fonctionnalité. Nous utilisons des mocks pour simuler les dépendances externes (bases de données, services tiers, etc.).
2. **Tests d'intégration** ces tests vérifient l’interaction entre plusieurs modules avec des dépendances externes (routes, services).
3. **Tests de bout en bout** (E2E) ces tests vérifient l'ensemble du flux applicatif, du point d'entrée (API ou interface) aux couches inférieures (base de données, services externes, etc.).

Nous utilisons des outils comme Supertest pour tester nos APIs. Nous testons également les retours en erreur du serveur :

* Réponses 4XX (erreurs utilisateur),
* Réponses 5XX (erreurs serveur).

Enfin, nous utilisons des bases de données en mémoire pour éviter d'instancier une base de données réelle : SQLite ou Mongo Memory Server pour le NoSQL.
