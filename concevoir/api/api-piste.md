# Exposition d'API via PISTE

[PISTE](https://piste.gouv.fr/) est une API Gateway interministérielle proposée par l'AIFE(DGFIP).
A noter que la DINUM ne se positionne pas officiellement sur PISTE : ni explicitement recommandé, ni déconseillé.

## Quand utiliser PISTE ?

PISTE est particulièrement intéressant pour :
- Exposer une API à un grand nombre d'acteurs. Ex : tous les éditeurs de logiciels d'un marché, nombreux partenaires institutionnels...

PISTE n'est pas adapté ou pas recommandé dans les cas suivants :
- Pas d'API GraphQL ou tout autre paradigme que REST/HTTPS
- API non exposée sur Internet

## Caractéristiques de PISTE
- Repose sur la solution commerciale **Axway API Gateway**
- Hébergée sur **OVH-SecNumCloud** et infogérée par un prestataire de l'AIFE
- l'API est soit publique (visible au catalogue PISTE, avec ou sans validation), soit privée
- l'AIFE refacture un coût fixe par projet. La convention de gestion étant déjà établie entre l'AIFE et le Ministère, cette partie n'est pas à refaire pour chaque nouvelle API.

## Considérations de sécurité
- PISTE conserve systématiquement les traces pendant 10 jours. Afin de s'assurer qu'aucune donnée sensible n'est stockée, il convient de demander explicitement aux équipes PISTE l'anonymisation de ces traces.
- Le trafic entre PISTE et nos applications métiers repasse nécessairement par Internet. Un VPN AIFE existe entre PISTE et le RIE, offrant éventuellement une route plus sécurisée vers nos applications métier hébergées en interne.

## Projets concernés par PISTE
- ONVS (en cours, exposition d'API aux Etablissements de Santé)
- SIVSS (en cours, exposition d'API aux ARS et autres administrations)
- AQUA-SISE (à confirmer)

Contre-exemples :
- MEDLE : un seul éditeur partenaire en expérimentation