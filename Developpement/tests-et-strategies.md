# Tests et stratégies

## Front

### Outillage

Nous utilisons [Jest](https://jestjs.io/) ou [Vitest](https://vitest.dev/guide/), et **Vitest** est notre choix par
défaut :

- Temps d'éxécution des tests inférieur à Jest ;
- Moins de dépendances lourdes, car Vite fourni plus de choses "out-of-the-box" ;
- Moins de configuration pour l'utiliser.

Nous utilisons également [TestingLibrary](https://testing-library.com/), qui nous permet d'écrire des tests unitaires et
des tests d'intégration.

Enfin, afin de bien tester les appels API, nous utilisons aussi
[JestMockAdapter](https://www.npmjs.com/package/jest-mock-axios) pour Axios ou
[JestFetchMock](https://www.npmjs.com/package/jest-fetch-mock) pour Fetch.

Ces plugins nous facilitent les tests pour les différents cas :

- Réponse 200 (ok)
- Erreur métier (4XX)
- Erreur serveur (5XX)

### Stratégie

Nous nous servons de la couverture de test afin d'identifier les composants peu ou pas testés, ce qui nous donne une
idée de là où nous devons accentuer notre effort.

Nous testons unitairement chaque composant, onglet et page en fonction de l'articulation de l'application front.

Si l'application utilise des contextes, nous testons chaque composant, onglet et page en 2 étapes :

1. Avec les valeurs par défaut du contexte ;
2. Avec des valeurs différentes.
