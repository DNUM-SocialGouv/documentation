---
icon: cloud
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

La stratégie cloud de la DNUM répond aux enjeux suivants :

* La modernisation de l’action publique implique des services fluides et performants
* Le cloud facilite l'agilité, les pratiques DevOps et l'usage de technologies modernes
* Le cloud est l'hébergement par défaut dans la doctrine [cloud au centre](https://www.numerique.gouv.fr/offre-accompagnement/cloud-administrations/la-doctrine-de-l%C3%A9tat/) de l’Etat

## Grands principes

* Le passage au cloud nécessite d'adopter de nouveaux paradigmes :
  * volet RH (formation des agents, internalisation des compétences-clés, accompagnement des équipes)
  * transformation des architectures applicatives (cloud native, 12 factors)
  * ré-organisation des équipes (DevOps, CI/CD, tests automatisés)
  * optimisation financière (FinOps) et environnementale (RGESN, GreenOps)
* Privilégier l’utilisation des fonctionnalités natives des fournisseurs de cloud
  * privilégier le SaaS si la souveraineté et le coût le permettent; sinon
  * privilégier le PaaS au CaaS (_sans raison évidente, le PaaS ne fait pas partie de la stratégie DNUM à l'heure actuelle_)
  * privilégier le CaaS au IaaS
* Les nouvelles applications (incluant les refontes) vont par défaut dans le cloud
  * l’hébergement interne est réservé aux périmètres non cloudifiables, mais suivent a minima une logique de conteneurisation
  * la bascule « telle quelle » est limitée aux cas extrêmes (ex : migration de masse avant fermeture de DC)

## Quel hébergement cloud pour quel cas d'usage ?

3 offres de cloud sont déployées en plus de l'existant Rosny/Dusquene :

* **Cloud générique (Atlas@OVH)** : applications sans contrainte réglementaire spécifique
* **Cloud HDS (auj. Cegedim, demain Atlas@OVH-HDS)** : applications manipulant des données de santé et nécessitant une [certification HDS](https://esante.gouv.fr/produits-services/hds) de l'hébergement et/ou de l'infogérance
* **Cloud de confiance (Atlas@OVH-SecNumCloud)** : applications manipulant des données particulièrement sensibles, y compris celles contenant des données de santé sensibles, nécessitant une qualification [SecNumCloud par l'ANSSI](https://cyber.gouv.fr/secnumcloud-pour-les-fournisseurs-de-services-cloud). Les données sont **particulièrement sensibles** lorsqu'elles réunissent deux conditions :
  * elles doivent être sensibles soit par nature (parce qu’identifiées comme un secret légal) soit du fait de leur emploi (parce qu’impliquées dans une mission essentielle de l’État)
  * leur violation aurait pour conséquence une atteinte à l’ordre public, la sécurité publique, la santé, la vie des personnes ou la propriété intellectuelle.

Les "clouds internes" de l'Etat Pi (MININT) et Nubo (DGFIP) ne sont pas utilisés au Ministère :
* nous n'avons pas besoin du niveau "diffusion restreinte" du cloud Pi
* nous préférons l'offre SecNumCloud d'OVH au Cloud Nubo

## Caractéristiques des plateformes d'hébergement

Connaitre ses caractéristiques permet de mieux choisir et anticiper l'atterrissage sur la plateforme appropriée. Les hébergement se distinguent par Dans le détail, les hébergements historiques et modernes ont des caractéristiques différentes. :

* les services d’infrastructure qu'ils proposent (stockage managé, middlewares, mécanismes de sécurité natifs). Vu des produits numériques déployés, les services peuvent être optionnelles ou systématiques.
* leurs modes d'exploitation (infogérance, CI/CD)
* les exigences réglementaires auxquelles elles répondent (HDS, SecNumCloud)

| Plateforme           | Type de cloud | BDD managé | S3 managé | HDS Hébergeur | HDS Infogéreur | SecNumCloud | EBIOS max | Antivirus PJ     |
| -------------------- | ------------- | ---------- | --------- | ------------- | -------------- | ----------- | --------- | ---------------- |
| **Atlas@OVH**        | CaaS          | O          | O         | O             | N              | N           | 2-3-3-3   | API@ClamAV       |
| **Atlas@OVH-SNC**    | CaaS          | N          | N         | O             | N              | O           | 4-3-3-3   | API@ClamAV       |
| **Cegedim HDS**      | CaaS/IaaS     | O          | O         | O             | O              | O           | 4-3-3-3   | ICAP@RP(auto)    |
| **Rosny (Travail)**  | CaaS/IaaS     | N          | O         | N             | N              | O           | 4-3-3-3   | ICAP (auto?)     |
| **Dusquene (Santé)** | CaaS/IaaS     | N          | O         | N             | N              | O           | 4-3-3-3   | ICAP (auto?)     |

Précisions :

* OVH propose un S3 standard et un S3 haute-performance
* Généralement le stockage en bloc (ou FS partagé sur SAN) est disponible seulement si avec les offres IaaS (VM traditionnelle). Préférer S3 de toute façon
* Aujourd'hui OVH-SNC n'accueille que Champollion mais à vocation à devenir l'hébergement hautement sécurisé du ministère

## Interconnexions sécurisées

Voici les interconnexions sécurisées entre hébergements via le RIE ou VPN

|                   | Atlas@OVH  | Cegedim   | Rosny     | Dusquene  | Atlas@OVH-SNC |
| ----------------- | ---------- | --------- | --------- | --------- | ------------- |
| **Atlas@OVH**     | ========== | ========= | ========= | ========= | ============= |
| **Cegedim**       | N          | ========= | ========= | ========= | ============= |
| **Rosny**         | N          | VPN ?     | ========= | ========= | ============= |
| **Dusquene**      | N          | VPN ?     | O (RIE ?) | ========= | ============= |
| **Atlas@OVH-SNC** | VPN IPSec  | N         | ?         | ?         | ============= |

## Notes sur HDS
* HDS est une norme qui comprend 6 niveaux d'activité, du stockage de la donnée à l'infogérance de l'application
* HDS vs SecNumCloud :
  * HDS et SecNumCloud ont évolué séparément, sans concertation. D'où la difficulté parfois de positionner l'un et l'autre.
  * Etre SecNumCloud ne veut pas dire être HDS, et inversement
  * HDS n'a pas de notion de souveraineté, contrairement à SecNumCloud
* HDS est du "droit mou" soumis a interprétation :
  * HDS ne traite pas des systèmes intermédiaires entre l'utilisateur et le système qui stocke la donnée : offre PaaS sur sous-traitant hébergeur HDS, API Gateway...
  * Lorsque l'application est développée en agile ou exploitée en interne, on peut considérer qu'il n'y a pas d'infogérance, donc pas d'infogérance HDS