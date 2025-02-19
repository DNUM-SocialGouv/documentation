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

## Back(Nodejs)

### Outilliage

Pour tester un backend en TypeScript, nous d'utilisons [Jest](https://jestjs.io/) comme framework principal. 
Jest offre une excellente compatibilité avec TypeScript, des fonctionnalités de mocking avancées et un écosystème mature.
Cependant, d'autres outils comme [Vitest](https://vitest.dev/guide/) peuvent également être utilisés si vous souhaitez 
bénéficier de meilleures performances dans certains scénarios.

**Outils recommandés**  

- Jest : Framework de test principal.
- [Supertest](https://www.npmjs.com/package/supertest) : Pour tester vos routes HTTP.
- [MSW](https://mswjs.io/) : Pour simuler les appels API externes.
- [Sinon](https://sinonjs.org/) : Pour créer des spies, stubs et mocks afin de tester le comportement des fonctions, 
des dépendances et des appels d’API sans réellement exécuter leur logique complète.
- [ts-jest](https://www.npmjs.com/package/ts-jest) : Pour gérer le transpileur TypeScript.

### Stratégie

1. **Les tests unitaires** doivent couvrir chaque fonction ou méthode isolée. 
Utilisez des mocks pour simuler les dépendances externes (bases de données, services tiers, etc.).

2. **Tests d'intégration** ces tests vérifient l’interaction entre plusieurs modules (routes, contrôleurs, services, etc.).

3. **Tests de bout en bout** (E2E) ces tests vérifient l'ensemble du flux applicatif, du point d'entrée (API ou interface)
aux couches inférieures (base de données, services externes, etc.). 
Utilisez des outils comme Supertest pour tester vos API.
- Tests des erreurs :
Testez systématiquement les scénarios d'erreur :
    - Réponses 4XX (erreurs utilisateur)
    - Réponses 5XX (erreurs serveur)
- Utilisation de bases de données en mémoire :
Pour éviter d'utiliser une base de données réelle, employez des solutions comme **SQLite** en mémoire
ou des librairies **comme Mongo Memory Server**.

