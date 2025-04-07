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

# API Gateway

L'API Management répond à de nombreux enjeux autour des APIs. Le sous-domaine API Gateway adresse les enjeux d'interopérabilité et de sécurisation des échanges. Une API Gateway peut être vue comme un **middleware de type Reverse Proxy, spécialisé dans l'exposition d'API**

## Fonctionnalités d'une API Gateway

* Sécurisation des échanges : exposition HTTPS, authentification, provisionnement de comptes et d'habilitations...
* translation éventuelle de protocole
* Protection des échanges : quotas, anti-DoS...
* Répartition de charge
* Pré-validation des trames et renvoi d'erreurs HTTP
* Supervision, traçabilité, audit... _"Pas de métier dans le middleware" : éviter de transformer les flux ou d'implémenter des règles métier dans la Gateway, même si l'outil le permet._

## Enjeux des API dans le contexte du MAS

* Plusieurs centaines d'applications métier
* Toujours plus d'ouverture des SI : dématérialisation, OpenData par défaut, DLNUF, échanges et réutilisation inter-administrations...
* Davantage d'hébergements (Duquesne, Rosny, Cegedim, RIE, OVH, Scalingo, SaaS...)
* Toujours plus d'interconnexions entre ces hébergements (intra-intra, cloud-cloud, intra-cloud, cloud-intra)
* Des menaces cyber croissantes
* Une efficacité budgétaire à optimiser

## Vision cible

Instancier et gérer une seule API Gateway par hébergement :

* 1 Gateway Rosny et/ou Dusquene
* 1 Gateway Cegedim
* 1 Gateway FabNum
* etc.

## Recommandations concernant l'API Gateway

1. **Limiter en amont les cas où l'on a besoin d’une API Gateway**

* Rationalisation des applications métier pour en limiter le nombre : découpage en modules ou éventuellement microservices, plutôt qu'en applications/SI distincts
* Colocalisation des Front-Office et Back-Office sur un même hébergement pour limiter les interconnexions
* Appels directs d’APIs en environnement maîtrisé (ex: API dédiée au backoffice + 2 Way SSL)

2. **Identifier les cas qui nécessitent systématiquement une API Gateway**

* API publique (nombreux clients / clients hétérogènes / clients mal connus)
* API partenaires exposée sur Internet et/ou exposant des données particulièrement sensibles
* API privée exposant des données particulièrement sensible
* Périmètre métier avec stratégie Zero Trust

3. **Identifier quelle API Gateway réutiliser**

* Si possible, utiliser l'API Gateway unique de l'hébergement visé (ex : future API Gateway FabNum?)
* Sinon instancier une API Gateway par domaine métier ET par hébergement (ex : API Gateway DGEFP sur Rosny/Dusquene)
* Eviter d'héberger une API Gateway dédiée par application
* Eviter de passer par PISTE@DGFIP (moindre agilité, hors CI/CD, perte de contrôle lié à la gouvernance DGFIP) sauf cas extrêmes : 0 budget, exposer transitoirement l'API d'une application legacy hébergée à Duquesne ou Rosny, API partenaire ou API publique massivement utilisée. Ce positionnement de PISTE tiens compte des conseils de la DINUM mais la DINUM n'a pas de recommandation officielle concernant PISTE (hors catalogue)

## Solutions d'API Gateway dans le contexte MAS

Solution utilisées aux MAS, à différents niveaux :
* **Gravitee.io** utilisé par 2 projets
* **PISTE (DGFIP)** utilisé par 1-2 projet
* **Hasura.io** mise sur le développement rapide (API low-code) mais une moindre sécurisation, exploitabilité, testabilité...

Aucune autre solution sur le marché ne semble présenter d'intérêt particulier pour le MAS. Ex :
* MuleSoft Anypoint trop orienté éditeur
* Kong Gateway équivalent à Gravitee
