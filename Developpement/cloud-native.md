# Application cloud native

Il s'agit d'une application qui suit un certain nombre de principes et prérequis afin de pouvoir être déployée dans le cloud.

- [12-factor app](https://12factor.net/fr/)
- [15 factors](https://developer.ibm.com/articles/15-factor-applications/#the-additional-factors-and-why-they-are-important1)

## Application conteneurisée

- L'application doit être livrée via des images Docker
- En local, l'environnement de développement complet doit utiliser [Docker Compose](https://docs.docker.com/compose/). Le lancement complet de l'environnement doit se faire par un simple `docker compose up`
  - Se référer à la page de la [structure d'un dépôt](/DevSecOps/structure-repo.md) pour le prérequis d'instanciation de l'environnement local.
- En intégration / préproduction / production, la priorité est donnée au déploiement sur un cluster [Kubernetes](https://kubernetes.io/fr/). À défaut, Docker Compose doit être utilisé si le déploiement se fait sur des VM

## Migrations de données réversibles

C'est indispensable s'il est nécessaire de redéployer une ancienne version (rollback).

## Pré-requis de l'équipe technique produit

- Gestion de configuration et définition claire de la gestion des branches git (feature, intégration, preproduction)
- Les tags sont utilisés pour la production
- Validation par les pairs lors de revue de code (merge/pull request)
- Refactoring en continu pour limiter la dette technique
- Homogénéisation des pratiques au sein de l'organisation (facilite la réversibilité interne)
- Cadre de cohérence technique
