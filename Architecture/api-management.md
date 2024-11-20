# API Management
Normes et standards pour l'exposition d'APIs

## Stratégie Microgateway au MAS
1. **Stratégie Microgateway plutôt que API Gateway centralisée**
- Éviter à tout prix de centraliser les flux dans une API Gateway (SPOF, effet ESB, moindre agilité...)
- Instancier une microgateway par application/SI plutôt qu’une Gateway par hébergement
2. **Limiter en amont les cas où on a besoin d’une API Gateway**
- Rationalisation des applications métier pour en limiter le nombre (découpage en modules/services OK, mais pas en applications/SI distincts)
- Colocalisation du Front-Office et Back-Office sur le même hébergement autant que possible
- Appels directs d’APIs en environnement maitrisé (ex: API dédiée au backoffice + 2 Way SSL)
- Attention, si on décide d’appliquer radicalement « Zero Trust », alors API Gateway systématique
3. **Identifier les cas qui nécessitent systématiquement une API Gateway**
- Exposé sur Internet
- Sensibilité particulière
- Nombreux clients
4. **Industrialiser le déploiement de microgateways pour accélérer les projets et limiter l’impact Ops**
- Designer une « Minimum Viable Gateway » (ex Kong DB-less) : images docker, fichiers de configuration type, pipeline CI/CD, etc.
- Utiliser PISTE pour exposer transitoirement le legacy déployé sur le MAS (non-Cloud)