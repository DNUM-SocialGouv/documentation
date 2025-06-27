---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Sécurisation

## Recommandations
- La [**sécurisation de l'API au niveau applicatif**](#sécurisation-au-niveau-applicatif) est nécessaire, pour identifier le client et agir si besoin (quotas, blocage temporaire...)
- Il convient également de [**sécuriser les échanges au niveau transport**](#sécurisation-au-niveau-transport), quelle que soit la sécurisation choisie au niveau applicatif.
- Si l'objectif est **ZeroTrust**, on recherche la sécurisation forte au niveau applicatif ET au niveau transport. Sinon il faut apprécier la combinaison des mécanismes de sécurité (ex : VPN + SSL + API Key, OAuth + SSL mutuel...)

## Sécurisation au niveau applicatif
Voici différentes manières de sécuriser une API REST au niveau applicatif, du plus sécurisé au moins sécurisé :
|Mécanisme|Description|Cas d'usage|Exemples|
|---------|-----------|-----------|--------|
|**OAuth2**|Protocole standard et complet|Données particulièrement sensibles.</br>Habilitations de niveau champ.</br>Consentement utilisateur.|API partenaire particulièrement sensible.</br>Fournisseur de Données FranceConnect.|
|**JWT Token**|Mécanisme de jeton avec authentification préalable.</br>Peut-être utilisé en combinaison avec OAuth2.|Signature numérique.</br>Chiffrement des données.</br>Performance (Stateless).|Exposer une API à un grand nombre de partenaires, avec les mêmes habilitations.</br>Environnement distribué.</br>Routage entre micro-services.|
|**API Key**|Mécanisme minimum utile et nécessaire|Authentification simple de l'application cliente sans gestion de session native (pas d'expiration/rafraichissement de jetons).|API privée exposée à d'autres applications internes.</br>Référentiel de données publiques.|
|**Basic Auth**|Authentification simple par identifiant et mot de passe|_A proscrire_|_n/a_|

Quelle que soit la solution, il faut prévoir un mécanisme de **révocation d'accès** pour un client en particulier. Pour une **révocation immédiate**, il peut-être nécessaire de gérer une session ou blacklist en base de données, au détriment de la performance. Mais une durée de session courte est généralement suffisante.

## Sécurisation au niveau transport
Voici différentes manières de sécuriser une API REST au niveau transport, du plus sécurisé au moins sécurisé :
- **VPN** : plus lourd et moins performant. A réserver au transport de données particulièrement sensibles en contexte Internet.
- **Rupture de protocole** : dès lors que l'API est exposée sur Internet, il faut au moins un intermédiaire de type [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/), [Reverse Proxy](https://fr.wikipedia.org/wiki/Proxy_inverse) ou [API Gateway](api-gateway.md) pour réduire le risque de trafic non sollicité et autres intrusions.
- **Certificats SSL mutuels** (2 Way SSL) : double authentification des parties. Nécessite le paramétrage de certificats SSL de chaque côté, dans un reverse proxy ou une API Gateway.
- **Certificat SSL simple** : déploiement de certificat côté API seulement. Convient pour une API publique ou une API partenaire pas trop sensible.