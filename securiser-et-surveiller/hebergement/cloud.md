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

# Hébergements Cloud

La stratégie Cloud des ministères sociaux répond aux enjeux suivants :
* La modernisation de l’action publique implique des services fluides et performants
* Le Cloud rend possible l'agilité, les pratiques DevOps et l'usage de technologies modernes
* Le Cloud est l'hébergement par défaut dans la doctrine [Cloud au Centre](https://www.legifrance.gouv.fr/circulaire/id/45205) de l’Etat

## Grands principes de la stratégie Cloud de la DNUM

* Les nouvelles applications (incluant les refontes) vont, par défaut, dans le Cloud. L’hébergement interne est réservé pour les périmètres non cloudifiables.
* Privilégier le recours aux SaaS (souverains) quand c’est possible
* Privilégier l’utilisation des fonctionnalités natives proposées par les Cloud Services Providers (PaaS plutôt que CaaS/IaaS)
* Le passage vers le Cloud doit s’accompagner d’une transformation des modèles d’architecture applicative (cloud native), d’organisation des équipes (DevOps, CI/CD), et d’optimisation financière et environnementale (FinOps, GreenOps)
* La bascule « telle quelle » (ou lift and shift), limitant la transformation, ne doit être utilisée que dans les cas qui le justifient (ex : migration de masse pour cause de fermeture de DC)
* Comme toute transformation, le passage vers le Cloud doit s’accompagner d’un volet RH (formation des agents, internalisation des compétences clés, accompagnement des équipes, …)

## Quel hébergement Cloud pour mon cas d'usage ?

Plusieurs typologies de besoins, nécessitant des offres d’hébergement appropriées, selon :

* La confidentialité des données
* Les besoins en services d’infrastructure
* Les exigences réglementaires, notamment le HDS

Pour répondre à ces typologies, 3 offres ont été identifiées :

* Cloud générique : qui vise à héberger toute application sans contrainte réglementaire spécifique
* Cloud HDS : qui vise à héberger les applications manipulant des données de santé et nécessitant une [certification HDS](https://esante.gouv.fr/produits-services/hds) de l'hébergement et de l'infogérance
* Cloud de confiance : qui vise à héberger les applications les plus sensibles, y compris celles contenant des données de santé sensibles, nécessitant une qualification [SecNumCloud par l'ANSSI](https://cyber.gouv.fr/secnumcloud-pour-les-fournisseurs-de-services-cloud)

> \[!TIP] Quels sont les critères discriminants qui définissent les données d’une sensibilité particulière ? Deux conditions doivent être réunies pour que les données soient qualifiées comme particulièrement sensibles au sens de la doctrine :
>
> * d’une part, elles doivent être sensibles soit par nature (parce qu’identifiées comme un secret légal) soit du fait de leur emploi (parce qu’impliquées dans une mission essentielle de l’État) ;
> * et d’autre part, leur violation aurait pour conséquence une atteinte à l’ordre public, la sécurité publique, la santé, la vie des personnes ou la propriété intellectuelle.

## Caractéristiques des plateformes d'hébergement
Vu des produits numériques déployés, ces caractéristiques peuvent être optionnelles ou systématiques :
|Plateforme         |Type de cloud |BDD managé|S3 managé|HDS Hébergeur|HDS Infogéreur|SecNumCloud|EBIOS max|Antivirus PJ|
|-------------------|--------------|----------|---------|-------------|--------------|-----------|---------|------------|
|**Atlas@OVH**      |CaaS          |O         |O        |O            |N             |N          |2-3-3-2  |API ClamAV  |
|**Atlas@OVH-SNC**  |CaaS          |N         |N        |O            |N             |O          |4-X-X-X  |API ClamAV  |
|**Cegedim.cloud**  |CaaS/IaaS     |O         |O        |O            |O             |O          |4-X-X-X  |SentinelOne?|
|**Rosny(intra)**   |CaaS/IaaS     |N         |O        |N            |N             |N          |4-X-X-X  |Sys?ICAP?   |
|**Dusquene(intra)**|CaaS/IaaS     |N         |O        |N            |N             |N          |4-X-X-X  |Sys?ICAP?   |

Précisions :
- OVH propose un S3 standard et un S3 haute-performance
- Généralement le stockage en bloc (ou FS partagé sur SAN) est disponible seulement si avec les offres IaaS (VM traditionnelle). Préférer S3 de toute façon
- Aujourd'hui OVH-SNC n'accueille que Champollion mais à vocation à devenir l'hébergement hautement sécurisé du ministère

## Interconnexions sécurisées
Voici les interconnexions sécurisées entre hébergements via le RIE ou VPN
|                 |Atlas@OVH |Cegedim  |Rosny    |Dusquene |Atlas@OVH-SNC|
|-----------------|----------|---------|---------|---------|-------------|
|**Atlas@OVH**    |==========|=========|=========|=========|=============|
|**Cegedim**      |N         |=========|=========|=========|=============|
|**Rosny**        |N         |VPN ?    |=========|=========|=============|
|**Dusquene**     |N         |VPN ?    |O (RIE ?)|=========|=============|
|**Atlas@OVH-SNC**|VPN IPSec |N        |?        |?        |=============|