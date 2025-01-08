# Stratégie de test

## Front

Vous pouvez utiliser [Jest]() ou [Vite](). Cependant, nous vous recommandons **Vite**.
Nous vous invitions à bien configurer votre collecte de coverage, celà vous permet de voir les composants peu ou pas testés. Ce qui vous donnera une idée de là où vous devez mettre l'effort.
Nous vous invition à utiliser [TestingLibrary](), cette librairie front vous permet d'écrire des tests unitaires et des tests d'intergration.

Nous vous recommandons de tester unitairement chaque composant, parent et onglet/page en fonction de l'articulation de votre application front.

Si vous utilisez des contextes, nous vous recommondons de tester chaque composant, parent et onglet et/ou page en 2 étapes :

1. Avec les valeurs par défaut du contexte
2. Avec des valeurs que vous définissez.

Afin de bien tester les appels API, nous vous recomandons [AxiosMock]() si vous utilisez Axios ou [FetchMock]() si vous utilisez Fetch.
Ces plugins vous permettrons de tester les différents cas :

- Le cas d'une réponse 200(ok)
- Le cas d'une erreur métier(4XX)
- Le cas d'une erreur 500
