# Déploiement continu (CD)

## Flot de développement git adapté

Choisir une stratégie git parmi :

**Trunk Based Development** : c'est une stratégie de gestion des branches dans le développement logiciel où tous les développeurs travaillent directement sur une seule branche principale, souvent appelée "trunk" ou "main". Les changements sont intégrés fréquemment, et les développeurs créent de petites branches à courte durée de vie pour des fonctionnalités spécifiques, qui sont fusionnées rapidement. Cela favorise l'intégration continue et réduit les conflits de fusion, accélérant ainsi le développement.

**Git Flow** : c'est une méthodologie de branchement plus structurée et formalisée. Elle repose sur plusieurs branches principales, notamment main (pour les versions en production) et develop (pour l'intégration des nouvelles fonctionnalités). Les développeurs créent des branches de fonctionnalité (feature), des branches de correctif (hotfix), et des branches de version (release). Cela permet une gestion plus fine du cycle de vie des versions, mais peut entraîner des conflits et des intégrations plus complexes si les branches sont maintenues trop longtemps.

Plus de détails ici (en français) : [Trunk Based Development (TBD) vs Gitflow
](https://www.yieldstudio.fr/blog/trunk-base-development-tbd-vs-gitflow)

## Créer des releases à partir de tags git

Attention : déployer uniquement un tag.

## Livraison

Livrer l'application sous forme d'images Docker, poussées sur un repository du type harbor.
