# Exposition d'API via PISTE

PISTE est une API Gateway de l'AIFE(DGFIP) offert en interministériel
L'API Gateway adresse l'interopérabilité et la sécurisation des échanges. C'est un **middleware de type Reverse Proxy, spécialisé dans l'exposition d'API**.

## Quand utiliser PISTE ?

PISTE est particulièrement intéressant pour :
* Exposer une API à un grand nombre d'acteurs. Ex : tous les éditeurs de logiciels d'un marché, un grand nombre de partenaires institutionnels)
* Translation éventuelle de protocole
* Protection des échanges : quotas, anti-DoS...
* Répartition de charge
* Pré-validation des trames et renvoi d'erreurs HTTP
* Supervision, traçabilité, audit...
* _Eviter de transformer les flux ou d'implémenter des règles métier dans l'API Gateway, même si elle le permet._

PISTE n'est pas adapté ou pas recommandé
- Pas d'API GraphQL ou tout autre paradigme que REST/HTTPS

## Caractéristiques de PISTE

## Considérations de sécurité
- PISTE conserve systématiquement les traces pendant 10 jours. Afin de s'assurer qu'aucune donnée sensible n'est stockée, il convient de demander explicitement aux équipes PISTE l'anonymisation de ces traces.