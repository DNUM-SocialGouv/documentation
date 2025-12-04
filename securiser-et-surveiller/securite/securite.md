# 🔒 Sécurité

## Gestion des secrets

* [ ] Utiliser des variables d'environnement pour configurer les secrets de l'application.
* [ ] Injecter uniquement des secrets chiffrés dans le code source.
* [ ] Injecter uniquement des secrets chiffrés dans les images docker
    * Ex : le token Sentry pour pousser les source maps.
* [ ] Utiliser l'outil [Gitleaks](https://github.com/gitleaks/gitleaks) dans un pre-commit hook git.
* [ ] Écrire uniquement des données non-sensibles et non-nominatives dans les logs.
* [ ] Utiliser les outils à disposition pour les projets open source.
  * Ex : GitGuardian

## Anonymisation des données

Voir la page correspondante, [ici](../../concevoir/data/anonymisation.md).

## Confiance des commits

* [ ] Signer l'intégralité des commits via des clés gpg / ssh / autre.
  * Objectif : certifier l'auteur des commits.

## Authentification 2FA (GitHub, Gitlab, ...)

* [ ] Sécurisation des comptes via une méthode 2FA.
