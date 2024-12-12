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
