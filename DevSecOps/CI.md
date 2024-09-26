# Intégration continue (CI)

L'intégration continue est la pratique de validation qualimétrique (quality gates) de l'application, effectuée typiquement à chaque commit / merge request / release.

Validations à inclure dans chaque CI :

- exécution des tests (unitaires, intégration, end-to-end)
  - Attention particulière portée à la partie API et authentification en particulier
  - Avoir un scenario complet "standard" en test end-to-end
- vérification du formattage du code
- lint : recherche des erreurs automatique dans le code
- qualité de code : SonarQube, complexité intrinsèque
- mises à jour régulières des dépendances (notamment bugs fixs et failles de sécurité)
