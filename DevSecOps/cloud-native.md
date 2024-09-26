# Application cloud native

Il s'agit d'une application qui suit un certain nombre de principes et prérequis afin de pouvoir être déployé dans le cloud.

- [12-factor app](https://12factor.net/fr/)
- [15 factors](https://developer.ibm.com/articles/15-factor-applications/#the-additional-factors-and-why-they-are-important1)

## Environnements de développement / intégration / préproduction / production semblables

L'application doit notamment utiliser docker compose en local.

## Application conteneurisée

L'application doit être livrée via des images Docker.

## Migrations de données réversibles

Indispensable s'il est nécessaire de re déployer une ancienne version (rollback).

## Pré-requis de l'équipe technique produit

- Gestion de configuration et définition claire de la gestion de branche (gitflow, trunk-based, etc.)
- Validation par les pairs lors de revue de code (merge request)
- Refacto en continu pour limiter la dette technique
- Homogéneisation des pratiques au sein de l'organisation (facilite la réversibilité interne)
- Cadre de cohérence technique
