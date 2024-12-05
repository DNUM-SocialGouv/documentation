# Démarche de rationalisation

## L'enjeu de cette démarche

L'architecture est uniquement positionnée pour répondre aux enjeux de gestion du patrimoine applicatif du fait de sa vision globale sur les applications, SI, services et les besoins auxquels ils répondent.

A ce titre les objectifs principaux sont : 
* expliciter les critères de décision pour les ajouts de nouvelles applications
* valoriser au mieux les solutions existantes
* dessiner une trajectoire de convergence de notre parc vers la cible de notre stratégie
* supporter l'organisation dans sa transformation sur la base de nos principes d'architecture

## Processus RADAR pour une nouvelle application

{% hint style="info" %}
Ce processus est en constante évolution et se fait toujours sur la base d'une impression holistique d'un projet et de ses problématiques spécifiques
{% endhint %}

RADAR pour Réutiliser, Adapter, Développer, Acheter et Reformuler est un framework simple pour attaquer le sujet de la dette technique et de la rationalisation des applications. 

L'objectif est de fournir des orientations sur la meilleure manière de traiter un besoin métier à travers une solution technologique en indiquant un ordre clair de préférence quant au choix de la solution.


<details>
<summary><strong>Réutiliser</strong></summary>

**Si le besoin fonctionnel (ou technique) peut être traité par de la configuration ou une modification mineure dans un système existant c'est alors l'option privilégiée.**

S'il ne s'agit que d'un flux de données on privilégie alors également la réutilisation des sources existantes en évitant les duplications.

* L'application en question peut être côté DNUM ou dans le reste de l'écosystème (y compris les solutions en SaaS) tant qu'elles sont connues et en production
* Les contraintes de sécurité et de gouvernance sont à apprécier sur la réutilisation de certaines solutions surtout en interministériel

</details>

<details>
<summary><strong>Adapter</strong></summary>
  
Si le besoin sort suffisamment de ce qui est faisable avec une solution actuellement dans le SI avec un effort raisonnable de configuration on peut alors considérer l'adaptation d'une solution tierce. 

* Il peut s'agir d'une solution opensource, venant d'une autre source gouvernementale ou potentiellement d'un partenaire existant
* Dans ce cas il est attendu que l'effort d'intégration de cette solution dans le SI se fasse uniquement sur notre capacité à disposer des compétences nécessaires à son déploiement et son exploitation et non sur un achat de services (SaaS)

</details>

<details>
<summary><strong>Développer</strong></summary>
  
Quand le besoin est trop spécifique on peut alors considérer la construction d'un produit dédié pouvant porter cette fonction. 
* Ce produit doit alors respecter nos [principes d'architectures](./principes.md) pour garantir sa valorisation dans le temps
* Si des options de sécurité/hébergement spécifiques sont nécessaires alors l'option spécifique est préférable autrement une analyse technico-financière plus précise doit également être réalisée pour identifier si l'option "Acheter" est plus pertinente.

</details>

<details>
<summary><strong>Acheter</strong></summary>
  
Il peut être pertinent de choisir une solution tierce venant du privé pour répondre à certains besoins.

* Dans ce cas sauf contraintes spécifiques le SaaS est à privilégier tant que celui-ci est en mesure de s'aligner avec nos normes et standards applicables
* Une réflexion doit être menée également sur la volonté ou non d'investir sur la solution en question vis-à-vis du reste de l'écosystème avec lequel il s'intègre s'il s'agit d'un besoin ponctuel (amélioration continue)

</details>

<details>
<summary><strong>Reformuler</strong></summary>
  
Parfois un besoin peut être tellement spécifique qu'il devient déraisonnable techniquement ou financièrement de le traiter tel quel. Il convient alors de repartir du besoin initial et l'analyser de manière plus précise pour identifier une manière plus pragmatique d'approcher le sujet de manière plus itérative.

De cette manière on arrive alors à créer un produit complet en partant d'une solution plus basique mais en restant aligné avec notre capacité à livrer.

</details>