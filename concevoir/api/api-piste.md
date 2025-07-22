# Exposition d'API via PISTE

[PISTE](https://piste.gouv.fr/) est une API Gateway interministérielle proposée par l'AIFE(DGFIP) :
- Basée sur la solution commerciale **Axway API Gateway**
- Hébergement **OVH-SecNumCloud**
- Convention de refacturation déjà établie entre AIFE et Ministère, pour l'ensemble des API.
- L'AIFE refacture un coût fixe par API.
_La DINUM ne se positionne pas officiellement sur PISTE : ni recommandé, ni déconseillé._

## Quand utiliser PISTE ?
PISTE est particulièrement intéressant pour **exposer une API à un nombre significatif d'acteurs** : tous les éditeurs de logiciels d'un marché, nombreux partenaires institutionnels...
PISTE n'est pas une solution pertinente pour :
- Une API exposée à un faible nombre de partenaires bien identifiés
- Une API GraphQL ou tout autre paradigme que REST/HTTP
- Une API exposée en Interne
- Un produit agile avec évolutions fréquentes et CI/CD au delà de l'environnement d'intégration

## Sécurité
- PISTE conserve systématiquement les traces pendant 10 jours. On peut demander demander aux équipes PISTE l'anonymisation définitive des traces.
- Le trafic entre PISTE et nos applications métiers repasse nécessairement par Internet. Le filtrage IP et DNS est fortement recommandé. Un VPN existant entre PISTE et le RIE, offre éventuellement une route plus sécurisée vers nos applications métier.
- PISTE se charge de la sécurisation OAuth2 avec les clients. OAuth2 n'est donc pas nécessaire entre PISTE et l'application métier. Un jeton JWT peut véhiculer les informations utilisateur vers l'application métier.
- PISTE permet des scopes OAuth2 pour gérer des droits plus fins par client
- PISTE permet la mise en place de quotas et limites d'utilisation

## Implémentation
- l'API doit respecter [le guide des bonnes pratiques de développement PISTE](PISTE%20-%20Guide%20de%20bonnes%20pratiques%20API_v2.00.pdf)
- L'application [MPSS](https://mpss.piste.gouv.fr/) permet de créer des bouchons pour simuler nos APIs.
- Un environnement bac-à-sable "sandbox" permet d'exposer des API de test.

## Administration des accès
- Une API sur PISTE est
    - soit publique (visible au catalogue PISTE, avec ou sans validation). _Rendre l'API publique peut générer beaucoup de sollicitations_
    - soit privée (non visible au catalogue PISTE)
- L'administration des accès se fait sur [piste.gouv.fr](https://piste.gouv.fr/), dans un espace dédié aux administrateurs d'API.
- Il existe 2 façons d'enrôler un client sur une API privée :
    - le client a déjà un compte PISTE : enrôler le compte client existant pour cette API
    - le client n'a pas de compte PISTE : créer un compte pour le client et l'enrôler en même temps, ce qui lui envoie un email d'invitation
- L'administrateur de l'API a la main pour révoquer des accès à tout moment.
- Adresse de support : piste.aife@finances.gouv.fr

## Projets concernés par PISTE
- AQUA-SISE (API Référentiels, API Signalements)
- ONVS (en cours, exposition d'API aux Etablissements de Santé)
- SIVSS (en cours, exposition d'API aux ARS et autres administrations)

Contre-exemples de projets avec décision de ne pas passer par PISTE :
- PTT : interfaçage de PPT et SUIT, 2 applications métier internes bien que sur des hébergements différents
- MEDLE : un seul éditeur de logiciel partenaire, en expérimentation

## TODO
- expliciter le coût et le conventionnement