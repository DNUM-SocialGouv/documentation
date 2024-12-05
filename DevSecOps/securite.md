# Sécurité

## Gestion des secrets

### Checklist

- [ ] utiliser des variables d'environnement pour configurer les secrets de l'application
- [ ] ne pas inclure de secrets non chiffrés dans le code source
- [ ] utiliser l'outil gitleaks dans un pre-commit hook git
- [ ] ne pas inclure de secrets non chiffrés dans les images docker
  - par ex : le token Sentry pour pousser les source maps 
- [ ] ne pas afficher les secrets dans les logs ni les envoyer sur sentry
- [ ] utiliser les outils à disposition pour les projets open source
  - ex : GitGuardian


## Anonymisation des données

### Checklist

- [ ] générer un dump anonymisé de la DB 
  - pour recharger en environnement d'intégration/preprod
  - pour calculer des KPI

## Confiance des commits

### Checklist

- [ ] signer l'intégralité des commits via des clés gpg / ssh / autre
  - objectif : certifier l'auteur des commits

## Authentification 2FA (github, gitlab ...)

### Checklist

- [ ] sécurisation des comptes via une méthode 2FA
