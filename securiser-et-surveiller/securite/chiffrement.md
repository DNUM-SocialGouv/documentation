# 🔒 Chiffrement des données

De manière non-exhaustive on identifie plusieurs niveaux de chiffrement des données :

* [Chiffrement au repos](chiffrement.md#chiffrement-au-repos)
* [Chiffrement en transit](chiffrement.md#chiffrement-en-transit)
* [Chiffrement par l'application](chiffrement.md#chiffrement-par-lapplication)
* [Chiffrement de bout-en-bout](chiffrement.md#chiffrement-de-bout-en-bout)

Ces modes de chiffrements ne sont pas exclusifs. Une même donnée est souvent chiffrée plusieurs fois.

## Chiffrement au repos

Le chiffrement des données au repos (ou chiffrement à froid) consiste à chiffrer les données au niveau de leur stockage persistant, afin de se prémunir d'un accès non autorisé ou d'un vol de matériel. Dans un environnement cloud il est abstrait et pris en charge par le fournisseur au niveau de ses baies de stockage. C'est notamment le cas chez Cegedim et OVH. Poussé à l'extrême et si l'hébergeur le permet, le chiffrement au repos d'une base de données permet de tout chiffrer à l'exception des tables temporaires de travail.

## Chiffrement en transit

Ce chiffrement consiste à protéger d'une interception éventuelle les données qui circulent entre les couches d'un système ou entre systèmes :

* Interactions utilisateurs ou appels d'API via HTTPS
* Accès à la base de données en TLS
* Etc. Ce chiffrement ne nécessite pas de développement spécifique : on s'appuie sur les options de sécurité de la couche transport.

## Chiffrement par l'application

Cela consiste pour l'application à chiffrer explicitement les données les plus sensibles. L'application est alors la seule à connaitre la clé de déchiffrement, ce qui complique encore l'accès non-autorisé aux données persistées. En revanche le chiffrement et le déchiffrement ont des désavantages :

* Impact sur la performance transactionnelle
* Fonctionnalités de recherche limitées et complexifiées

## Chiffrement de bout en bout

Ce chiffrement consiste à chiffrer les données d'un utilisateur à l'autre, de telle sorte que même le serveur ne peut pas lire les données échangées. Utilisé typiquement pour la messagerie sécurisée, il est rarement mis en oeuvre dans nos applications métier. Dans notre contexte on peut néanmoins mentionner Tchap et MS Santé.
