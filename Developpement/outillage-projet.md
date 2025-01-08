# Outillage sur les projets

## Managers de packages

### Java

Sur les projets réalisés avec Java, nous utilisons [maven](https://maven.apache.org/) en tant que standard sur des
projets "simples" (sans modules) ou plus complexes. C'est à l'appréciation de l'équipe projet, et nous conseillons
d'avoir recours aux [sous-modules](https://maven.apache.org/guides/mini/guide-multiple-modules-4.html) dès que des
questions se posent sur :

1. la navigation dans le code
2. la factorisation/réutilisation du code
3. l'isolation d'une dépendance
4. la séparation des sujets

Dans cette optique toutes les parties du projet doivent être organisées au sein de modules spécifiques, ce qui permet de
structurer le code en ensembles relativement indépendants et potentiellement réutilisables.

### TypeScript

Pour les projets en TS, nous utilisons [yarn](https://yarnpkg.com/) ou [pnpm](https://pnpm.io/) comme gestinnaire de dépendances.
Nous utilisons d'autre outils qui nous permettent de vérifier automatiquement la qualité du code :

- [Eslint](https://eslint.org/) qui permet de valider une centaines de régles. Eslint, permet aussi de valider une partie des régles d'A11y.
- [Prettier](https://prettier.io/) qui permet de formatter son code en fonction des standards de l'équipe.

Nous vous recommandons de mettre en place des hooks de pré-commit. Nous vous invition à utiliser [Husky](https://typicode.github.io/husky/), [CommitLint](https://commitlint.js.org/) et [Pre-commit](https://pre-commit.com/).  
Ainsi vous vous assurez que votre pipeline(CI) ne va pas fail et vous vous assurez que toute l'équipe respecte les mêmes standards.
