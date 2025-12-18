# 🔌 Exposition d'API

L'API Gateway adresse l'interopérabilité et la sécurisation des échanges. C'est un **middleware de type Reverse Proxy, spécialisé dans l'exposition d'API**.

## Fonctionnalités d'une API Gateway

* Sécurisation des échanges : exposition HTTPS, authentification, provisionnement de comptes et d'habilitations...
* Translation éventuelle de protocole
* Protection des échanges : quotas, anti-DoS...
* Répartition de charge
* Pré-validation des trames et renvoi d'erreurs HTTP
* Supervision, traçabilité, audit...
* _Eviter de transformer les flux ou d'implémenter des règles métier dans l'API Gateway, même si elle le permet._

## Enjeux des API dans le contexte des Ministères Sociaux

* Plusieurs centaines d'applications métier
* Toujours plus d'ouverture des SI : dématérialisation, OpenData par défaut, DLNUF, échanges et réutilisation inter-administrations...
* Davantage d'hébergements (Duquesne, Rosny, Cegedim, RIE, OVH, SaaS...)
* Toujours plus d'interconnexions entre ces hébergements (intra-intra, cloud-cloud, intra-cloud, cloud-intra)
* Des menaces cyber croissantes
* Une efficacité budgétaire à optimiser

## Vision cible

Instancier et gérer une seule API Gateway par hébergement :

* 1 Gateway Rosny et/ou Dusquene
* 1 Gateway Cegedim
* 1 Gateway OVH
* 1 Gateway OVH-SecNumCloud

## Recommandations concernant l'API Gateway

1. **Limiter en amont les cas où l'on a besoin d’une API Gateway**

* Limiter le nombre d'applications métier en découpant en modules plutôt qu'en applications
* Limiter les interconnexions en déployant ensemble le front-office et le back-office
* Appels directs d’APIs en environnement maîtrisé (ex: API dédiée au backoffice + 2 Way SSL)

2. **Identifier les cas qui nécessitent systématiquement une API Gateway**

* API publique (nombreux clients / clients hétérogènes / clients mal connus)
* API partenaires exposée sur Internet ou exposant des données sensibles
* API privée exposant des données sensibles
* Périmètre métier avec stratégie Zero Trust

3. **Identifier quelle API Gateway réutiliser**

* Si possible, utiliser l'API Gateway unique de l'hébergement visé (ex : future API Gateway Atlas ?)
* Sinon instancier une API Gateway par domaine métier ET par hébergement (ex : API Gateway DGEFP sur Rosny/Dusquene)
* Passer par [PISTE](api-piste.md) si c'est pertinent et si les conditions sont réunies
* Eviter d'héberger une API Gateway dédiée par application

## Solutions d'API Gateway aux Ministères Sociaux

* **Gravitee.io** utilisé par 2 produits
* [**PISTE**](api-piste.md)
* **Hasura.io** utilisé en interne sur un projet pur Data.

## Pistes explorées et décisions d'architecture

Aucune autre solution sur le marché ne semble présenter d'intérêt particulier dans le contexte. Ex :

* **Hasura.io** est un Data-as-a-Service qui offre un développement rapide mais une moindre exploitabilité et testabilité. Peut être intéressant pour un projet pure Data, mais pas en complément d'une application métier.
* **MuleSoft Anypoint** trop orienté éditeur
* **Kong Gateway** équivalent à Gravitee
