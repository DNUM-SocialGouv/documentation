# Tests et stratégies

## Front

Vous pouvez utiliser [Jest](https://jestjs.io/) ou [Vite](https://vite.dev/). Cependant, nous vous recommandons
**Vite** pour des raisons de performance (temps d'éxécution des tests, moins
de dépendances lourdes) mais aussi par ce que la mise en place de Vite est plus simple que celle de Jest. En effet,
l'intégration de Vite est plus fluide. Nous vous recommandons de bien configurer votre collecte de coverage, celà vous
permet de voir les composants peu ou pas testés. Ce qui vous donnera une idée de là où vous devez mettre l'effort. Nous
vous invitons à utiliser [TestingLibrary](https://testing-library.com/), cette librairie front vous permet d'écrire des
tests unitaires et des tests d'intégration.

Nous vous recommandons de tester unitairement chaque composant, parent et onglet/page en fonction de l'articulation de
votre application front.

Si vous utilisez des contextes, nous vous recommandons de tester chaque composant, parent et onglet et/ou page en 2
étapes :

1. Avec les valeurs par défaut du contexte
2. Avec des valeurs que vous définissez

Afin de bien tester les appels API, nous vous recommandons
[JestMockAdapter](https://www.npmjs.com/package/jest-mock-axios) si vous utilisez Axios ou
[JestFetchMock](https://www.npmjs.com/package/jest-fetch-mock) si vous utilisez Fetch. Ces plugins vous permettront de
tester les différents cas :

- cas d'une réponse 200 (ok)
- cas d'une erreur métier (4XX)
- cas d'une erreur serveur (5XX)
