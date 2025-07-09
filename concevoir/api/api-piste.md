# Exposition d'API via PISTE

PISTE est une API Gateway proposée en interministériel par l'AIFE(DGFIP).
A noter que PISTE n'est ni explicitement recommandé, ni déconseillé par la DINUM.

## Quand utiliser PISTE ?

PISTE est particulièrement intéressant pour :
* Exposer une API à un grand nombre d'acteurs. Ex : tous les éditeurs de logiciels d'un marché, nombreux partenaires institutionnels...

PISTE n'est pas adapté ou pas recommandé
- Pas d'API GraphQL ou tout autre paradigme que REST/HTTPS

## Caractéristiques de PISTE
- Repose sur la solution commerciale **Axway API Gateway**
- Hébergée
- Infogéré
- l'AIFE refacture un coût fixe par projet. La convention de gestion étant déjà établie entre l'AIFE et le Ministère, cette partie n'est pas à refaire pour chaque nouvelle API.

## Considérations de sécurité
- PISTE conserve systématiquement les traces pendant 10 jours. Afin de s'assurer qu'aucune donnée sensible n'est stockée, il convient de demander explicitement aux équipes PISTE l'anonymisation de ces traces.

## Exemples de projets concernés
- AQUA-SISE
- ONVS
- SIVSS