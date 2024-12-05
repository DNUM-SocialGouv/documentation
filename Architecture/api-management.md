# API Management
L'API Management répond à de nombreux enjeux autour des APIs. Le sous-domaine **API Gateway** adresse les enjeux d'interopérabilité et de sécurité des échanges**. C'est ce sur quoi nous nous concentrons ici.

Une API Gateway peut-être vu comme un **middleware de type Reverse Proxy spécialisé dans l'exposition d'API** (protocole HTTPS ou autre, load balancing)

## Fonctionnalités d'une API Gateway
- Sécurisation des échanges (protocoles de sécurité, authentification, provisionnement de comptes et d'habilitations...)
- Protection des échanges (quotas, anti-DoS...)
- Pré-validation des trames et renvoi d'erreurs HTTP
- Supervision (traçabilité, audit...)
_la transformation des flux et l'implémentation de règles métier dans la Gateway n'est pas une bonne pratique_

## Enjeux des API dans le contexte du MAS
- Plusieurs centaines d'applications métier
- Toujours plus d'ouverture des SI (dématérialisation, OpenData par défaut, DLNUF, coopération et réutilisation inter-administrations...)
- De plus en plus d'hébergements (Duquesne, Rosny, Cegedim, RIE, OVH, Scalingo, SaaS...)
- De plus en plus d'interconnexions réseau et d'échanges de données entre ces hébergements (intra-intra, cloud-cloud, intra-cloud, cloud-intra)
- Des cybermenaces croissantes
- Une efficacité budgétaire à optimiser

## Stratégie d'API Gateway proposée
1. **Limiter en amont les cas où on a besoin d’une API Gateway**
- Rationalisation des applications métier pour en limiter le nombre : découpage en modules ou éventuellement microservices, plutôt qu'en applications/SI distincts
- Colocalisation des Front-Office et Back-Office sur un même hébergement pour limiter les interconnexions
- Appels directs d’APIs en environnement maîtrisé (ex: API dédiée au backoffice + 2 Way SSL)
2. **Stratégie Microgateway plutôt que API Gateway centralisée**
- Éviter si possible de centraliser les flux dans une même API Gateway (SPOF, effet ESB, moindre agilité, complexité de la gouvernance...)
- Instancier une Microgateway par SI ou éventuellement par hébergement (ex: API-M dans l'offre FabNum?)
3. **Identifier les cas qui nécessitent systématiquement une API Gateway**
- API publique (nombreux clients / clients hétérogènes / clients mal connu)
- API partenaires exposée sur Internet et/ou exposant des données particulièrement sensibles
- API privée exposant des données particulièrement sensible
- Périmètre métier avec stratégie Zero Trust
4. **Utiliser PISTE dans certains cas**
- API critique d'envergure nationale
- API partenaire ou API publique massivement utilisée
- Exposer transitoirement l'API d'une application legacy à Duquesne ou Rosny
_Ce positionnement de PISTE tiens compte des conseils de la DINUM mais la DINUM n'a pas de recommandation officielle concernant PISTE (hors catalogue)_
5. **Industrialiser le déploiement de microgateways pour accélérer les projets et limiter l’impact Ops** pour les autres cas
- Concevoir une « Minimum Viable Gateway » (Kong DB-less ou Gravitee) : images docker, fichiers de configuration type, pipeline CI/CD, etc.

## Solutions d'API Management en lien avec le contexte MAS
- PISTE (DGFIP)
- Kong Gateway
- Gravitee.io
_Après analyse rapide du marché, aucune autre solution d'API Management ne semble présenter d'intérêt significatif pour le MAS (ex: MuleSoft Anypoint)_

## Points à traiter
- Interviewer les équipes REACTEUR, SIVA et AQUA-SISE pour avoir leur REX
- Continuer à analyser les types d'interconnexions compte-tenu des différents hébergements du MAS (cloud-to-cloud, cloud-to-intra, intra-to-cloud, intra-to-intra...)
=======
L'API Management répond à de nombreux enjeux autour des APIs. Le sous-domaine **API Gateway** adresse les enjeux d'interopérabilité et de sécurité des échanges**. C'est ce sur quoi nous nous concentrons pour l'instant.

## Fonctionnalités d'une API Gateway
- Exposition HTTP via Reverse Proxy
- Sécurisation des échanges (choix des protocoles, authentification, provisionning de comptes et d'habilitations...)
- Protection via divers mécanismes (quotas...)
- Supervision (traçabilité, audit...)

## Enjeux techniques dans le contexte du MAS
- Plusieurs centaines d'applications métier
- Un besoin croissant d'ouverture (dématérialisation, OpenData, coopération inter-administration...)
- De plus en plus d'hébergements (Intra, Cegedim, OVH, Scalingo)
- De plus en plus d'interconnexions entre hébergements (intra-intra, cloud-cloud, intra-cloud, cloud-intra)
- Un risque cyber croissant
- Une efficacité budgétaire à travailler

## Stratégie d'API Gateway proposée
0. **Limiter en amont les cas où on a besoin d’une API Gateway**
- Rationalisation des applications métier pour en limiter le nombre : découpage en modules ou éventuellement microservices collocalisés, plutôt qu'en applications/SI distincts
- Colocalisation du Front-Office et Back-Office sur le même hébergement
- Appels directs d’APIs en environnement maîtrisé (ex: API dédiée au backoffice + 2 Way SSL)
1. **Stratégie Microgateway plutôt que API Gateway centralisée**
- Éviter autant que possible de centraliser les flux dans une API Gateway (SPOF, effet ESB, moindre agilité...)
- Instancier une Microgateway par application/SI plutôt qu’une Gateway par hébergement
2. **Identifier les cas qui nécessitent systématiquement une API Gateway**
- Exposé sur Internet
- Sensibilité particulière des données
- Nombreux clients / clients hétérogènes / clients mal connu
- Si on décide d’appliquer « Zero Trust », alors API Gateway systématique
3. **Industrialiser le déploiement de microgateways pour accélérer les projets et limiter l’impact Ops**
- Concevoir une « Minimum Viable Gateway » (ex Kong DB-less) : images docker, fichiers de configuration type, pipeline CI/CD, etc.
- Utiliser PISTE pour exposer transitoirement le legacy déployé sur le MAS (non-Cloud)

## Solutions d'API Management en lien avec le contexte MAS
- PISTE
- Kong
- Gravitee
- API Management from-scratch?
_Après analyse rapide du marché, aucune autre solution d'API Management ne semble présenter d'intérêt pour le MAS (ex: MuleSoft Anypoint)_

## Points à traiter
- Interviewer les équipes REACTEUR, SIVA et AQUA-SISE pour avoir leur REX
- Analyser les types d'interconnexions compte-tenu des différents hébergements du MAS (cloud-to-cloud, cloud-to-intra, intra-to-cloud, intra-to-intra...)
- Comprendre la vision SPM/DINUM en matière d'API du secteur public
- Concevoir une "Minimum Viable Gateway"