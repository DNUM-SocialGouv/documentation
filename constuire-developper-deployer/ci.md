# ✅ Intégration continue (CI)

L'intégration continue est la pratique de contrôle qualité automatique de l'application, effectuée typiquement à chaque commit ou pull/merge request.

## Checklist

La CI doit inclure :

* [ ] Les tests (unitaires, intégration, end-to-end)
  * Attention particulière sur la partie API et authentification
  * Scenario complet nominal en test end-to-end
  * Pour le frontend, des tests d'accessibilité
  * Pour le frontend, un test automatisé de Lighthouse (par exemple via une [GitHub Action](https://github.com/GoogleChrome/lighthouse-ci)) avec obligatoirement un résultat de 100 % pour l'accessibilité
* [ ] Formatage du code (ex : prettier en JS)
* [ ] Qualité de code (analyse statique du code)
  * [ ] linter
  * [ ] SonarQube
    * Code smells
    * Duplication
    * Complexité
    * Security hotspots
* [ ] Mises à jour régulières des dépendances
  * Systématiquement pour les versions mineures
  * Attention aux failles de sécurité
  * Utilisation d'un outil supplémentaire en fonction de l'écosystème (ex : SocketSecurity dans le monde JS) pour vérifier les vulnérabilités des dépendances utilisées.
