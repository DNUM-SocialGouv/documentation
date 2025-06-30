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

# Cloud

## Pourquoi une stratégie Cloud pour les ministères sociaux ?

* Des enjeux de modernisation de l’action publique via la mise à disposition de services fluides et performants
* Des besoins applicatifs forts, que ce soit en termes d’agilité ou de composantes technologiques, nécessitant des cibles Cloud et des modes de fonctionnement DevOps
* La [Doctrine Cloud au Centre](https://www.numerique.gouv.fr/services/cloud/doctrine/) de l’Etat faisant du Cloud le socle d’hébergement par défaut

## Les grands principes de la stratégie Cloud de la DNUM

* Les nouvelles applications (incluant les refontes) vont, par défaut, dans le Cloud. L’hébergement interne est réservé pour les périmètres non cloudifiables.
* Privilégier le recours au SaaS quand c’est possible, et l’utilisation des fonctionnalités natives proposées par les CSP (PaaS > IaaS)
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

## Plateformes d'hébergement

|Plateforme         |Type de cloud |BDD managé*|S3 managé*|FS partagé*|HDS Hébergeur|HDS Infogéreur*|SecNumCloud|EBIOS max|Antivirus  |
|-------------------|--------------|-----------|----------|-----------|-------------|---------------|-----------|---------|-----------|
|**FabNum@OVH**     |PaaS Node/Java|O          |O         |N          |N            |N              |N          |2-3-3-2  |           |
|**Cegedim.cloud**  |CaaS/IaaS     |O          |O         |O          |O            |O              |N          |         |SentinelOne|
|**Rosny(intra)**   |n/a           |O          |N         |O          |N            |N              |N          |         |           |
|**Dusquene(intra)**|n/a           |O          |N         |O          |N            |N              |N          |         |           |
|_OVH SNC_          |CaaS          |?          |?         |N          |N            |N              |O          |         |           |
(*) _Optionnel_

## Interconnexions sécurisées
Voici les interconnexions sécurisées entre hébergements via le RIE ou VPN
|            |FabNum               |Cegedim  |Rosny    |Dusquene |_OVH SNC_|
|------------|---------------------|---------|---------|---------|---------|
|**FabNum**  |=====================|=========|=========|=========|=========|
|**Cegedim** |?                    |=========|=========|=========|=========|
|**Rosny**   |?                    |VPN ?    |=========|=========|=========|
|**Dusquene**|?                    |VPN ?    |RIE ?    |=========|=========|
|_OVH SNC_   |Flux sortant SNC=>OVH|         |         |         |=========|

_Représenter le RIE ?_
_Représenter PI ?_
_Représenter NUBO ?_