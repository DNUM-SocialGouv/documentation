# API Management
Normes et standards pour l'exposition d'APIs

## Stratégie Microgateway au MAS
0. **Limiter en amont les cas où on a besoin d’une API Gateway**
- Rationalisation des applications métier pour en limiter le nombre : découpage en modules ou éventuellement microservices collocalisés, plutôt qu'en applications/SI distincts
- Colocalisation du Front-Office et Back-Office sur le même hébergement autant que possible
- Appels directs d’APIs en environnement maitrisé (ex: API dédiée au backoffice + 2 Way SSL)
1. **Stratégie Microgateway plutôt que API Gateway centralisée**
- Éviter autant que possible de centraliser les flux dans une API Gateway (SPOF, effet ESB, moindre agilité...)
- Instancier une Microgateway par application/SI plutôt qu’une Gateway par hébergement
3. **Identifier les cas qui nécessitent systématiquement une API Gateway**
- Exposé sur Internet
- Sensibilité particulière des données
- Nombreux clients / clients hétérogènes / clients mal connu
- Si on décide d’appliquer « Zero Trust », alors API Gateway systématique
4. **Industrialiser le déploiement de microgateways pour accélérer les projets et limiter l’impact Ops**
- Concevoir une « Minimum Viable Gateway » (ex Kong DB-less) : images docker, fichiers de configuration type, pipeline CI/CD, etc.
- Utiliser PISTE pour exposer transitoirement le legacy déployé sur le MAS (non-Cloud)

## Solutions d'API Management en lien avec le contexte MAS
- PISTE
- Kong
- Gravitee
- API Management from-scratch?
_Après analyse rapide du marché, aucune autre solution d'API Management ne semble présenter d'intérêt pour le MAS (ex: MuleSoft Anypoint)_

## Points à traiter
- Assimiler la boîte à outils Notes
- Analyser les types d'interconnexions compte-tenu des différents hébergements du MAS (cloud-to-cloud, cloud-to-intra, intra-to-cloud, intra-to-intra...)
- Comprendre la vision DINUM en matière d'API du secteur public
- Anlyser l'existant et les solutions
- Interviewer les équipes REACTEUR, SIVA et AQUA-SISE pour avoir leur REX
- Concevoir une "Minimum Viable Gateway"