---
description: Bienvenue !
icon: face-smiling-hands
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

# Introduction

Voici un ensemble de ressources destiné aux agents de la sous-direction des projets (produits) et services numériques de la direction du numérique des ministères sociaux, ainsi qu'à leurs partenaires et sous-traitants.

Ceci est l'expérimentation de la mise en place d'un nouveau cadre organisationnel.

{% hint style="warning" %}
**Ce document est ouvert et accessible à toutes et tous, par design. Il ne contient pas d'informations confidentielles. S'il peut inspirer d'autres organisations, ou bien donner envie à des personnes de nous rejoindre, alors tant mieux.💛**
{% endhint %}

***

### Contribuer

Vous êtes bienvenus pour contribuer à cette documentation, proposer de nouvelles choses ou mettre au défi son contenu. Pour ce faire, vous pouvez simplement proposer des [_pull requests_](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) (PR) sur [ce dépôt](https://github.com/DNUM-SocialGouv/documentation).

Pour les personnes familières avec les collaborations sur les projets Git et qui préfèrent modifier le code sur le poste local, une documentation est disponible [ici](contribution-avancee.md).

***

### Table des matières

1. [Pourquoi cette démarche ?](./#pourquoi-cette-demarche)
2. [Nouveau cadre organisationnel](./#un-nouveau-cadre-organisationnel)
3. [Cycle de vie produit](./#cycle-de-vie-produit)
4. [Je suis chef.fe de produit](./#je-suis-chef.fe-de-produit)

***

## Pourquoi cette démarche ?

### Constat <a href="#constat" id="constat"></a>

La sous-direction possède un parc de [240 applications](nos-produits/) et 40 à 50 chefs de projet/produit pour les piloter en lien avec les équipes métiers.

Au regard de ce parc, on note des enjeux d'optimisation :

* **Livraisons inégales** (retards, instabilité, lenteur de la conception à la mise en production, qualité de l'expérience utilisateur, qualité du code)
* **Manque de maitrise** (hétérogénéité technologique, code-source non maitrisé, absence d'intégration continue, obsolescence, sécurité imparfaite)
* **Investissements épars** (à chaque nouveau besoin, une nouvelle application)

### Opportunités <a href="#opportunites" id="opportunites"></a>

Nous notons des opportunités à travers cette démarche :

* Faciliter le quotidien des équipes (meilleure maîtrise des systèmes, déploiement continu)
* Améliorer l'expérience de toutes et tous (rapidité de développement, qualité - sécurité, design, expérience utilisateur)
* Optimiser les coûts

### Un nouveau cadre organisationnel <a href="#un-nouveau-cadre-organisationnel" id="un-nouveau-cadre-organisationnel"></a>

Nous souhaitons donc expérimenter avec la mise en place d'un nouveau cadre organisationnel qui permettra de :

1. Assurer la cohérence globale
   1. Création du [**comité produit**](https://direction-du-numerique-ministere.gitbook.io/ressources/readme/comite-produit) qui se réunit toutes les semaines pour passer en revue les nouveaux projets, refontes, et petit à petit des projets où il existe une opportunité de pivoter
   2. Publication de **normes et standards** (ici même) afin de guider et d'harmoniser la conception des produits et services
2. Construire un **catalogue de standards et de communs numériques** et ainsi identifier les points de mutualisation entre différents besoins ou services (librairies, plateformes, référentiels)
3. [**Accompagner les équipes**](https://msociauxfr.sharepoint.com/teams/ProductTeams-DevDesignAccessibilitRechercheutilisateurCoachi/SitePages/Accueil.aspx) en continu pour offrir un appui technique, d'architecture, de DevSecOps, de gestion des données, de design, d'accessibilité, de recherche utilisateur

***

## Nouveau cadre organisationnel

{% hint style="warning" %}
**Le comité produit est toujours en version bêta et son organisation est susceptible d'évoluer. Il se réunit chaque semaine depuis le 1ᵉʳ octobre 2024.**
{% endhint %}

> <mark style="color:purple;background-color:purple;">**Le comité produit accompagne et soutient les équipes en identifiant leurs besoins, en les orientant, en les aidant et surtout en leur proposant des solutions.**</mark>

### Rôles du comité

1. Rencontrer l'équipe produit à chaque étape du [processus _phase-gate_](./#processus-phase-gate) afin de valider les orientations et les décisions techniques, mais aussi d'identifier avec les équipes des besoins d'accompagnement (technique, architecture, design, devops, etc)
2. Développer le catalogue de standards et de communs numériques : écrire les normes, identifier les réutilisations

### Composition du comité

Aujourd'hui, il est composé de :

* 1 responsable de la technologie
* 1 architecte
* 1 responsable des communs numériques
* 1 responsable du design
* 1 responsable des opérations produit
* 1 responsable des produits data
* 2 responsables des infrastructures cloud (à la Fabrique Numérique et au Département des Opérations)
* 1 responsable de la sécurité
* 1 conseiller transformation numérique

D'autres profils, notamment métier, participent au comité produit en fonction de l'actualité.

### Produits concernés par le comité

* Les nouveaux produits et services numériques
* Les refontes fonctionnelles et techniques
* Les évolutions majeures lorsque c'est pertinent : évolution significative du design, nouvelles populations d'utilisateurs, ajout de composants dans l'architecture, mises en conformité, etc.\
  Point à discuter : concernant les logiciels low-code/no-code, powerapps et powerbi, l'organisation est en cours de construction avec les différents bureaux

### Processus "phase-gate"

Un processus "phase-gate" assure le suivi récurrent du patrimoine applicatif, tout au long du cycle de vie des produits :

* Chaque passage en comité produit pour go/no go garantit que le produit a le niveau de maturité et de qualité requis pour passer à la phase suivante et qu'il s’inscrit dans la stratégie globale
* Définir des attentes réalistes et adaptées à chaque étape du cycle de vie d’un produit​ : cadre de cohérence technique, règles d'interopérabilité, pratiques de développement​
* Valider le respect de ces attentes à l’aide de points de passage (ou gates) entre chaque phase​ pour faciliter le passage de l’innovation à l’industrialisation, garantir la conformité des applications mises en œuvre, assurer l’expérience utilisateur (sécurité, disponibilité …), confirmer la pertinence métier, identifier les axes de rationalisation du système d'information

A chaque phase, un suivi est assuré sur les différents aspects d'un produit :

* Organisation et gouvernance
* La valeur métier
* La méthodologie
* L'architecture
* Les données
* La sécurité
* Les pratiques de développement

Des réponses aux questions qui s'enrichissent à chaque phase.

***

## Cycle de vie produit

Les produits doivent suivre un cycle de vie standard, incluant des étapes de validation par le comité​ produit.

### Phases du cycle de vie produit

_NB : un produit peut s'arrêter à chaque étape pour des raisons de pertinence, de contexte, de budget..._

|                                                          | Objectif                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Livrables-type                                                                                                                         |
| -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Idée**                                              | Comprendre et évaluer l’intérêt/pertinence avant de s’engager davantage en termes de temps et de ressources.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | <p>vision produit<br>analyse d'un besoin<br>note de cadrage<br>simple prise de contact<br>démarche de rationalisation</p>              |
| <p><strong>2. POC</strong><br>Preuve de concept</p>      | Valider l’intérêt et la pertinence d’une idée et/ou démontrer la faisabilité technique. Le PoC est une bonne pratique pour réduire le risque, mais n'est pas obligatoire.                                                                                                                                                                                                                                                                                                                                                                                                          | <p>parcours utilisateur<br>maquettes statiques ou interactives<br>démonstrateur<br>code source<br>règles de gestion documentées</p>    |
| <p><strong>3. MVP</strong><br>Produit Minimum Viable</p> | <p>Développer et déployer en production, une première version avec les fonctionnalités de base afin de valider les hypothèses.<br>- <strong>Produit</strong> : un produit opérationnel (en production) mis dans la main d’utilisateurs qui peuvent l’utiliser pour réaliser leurs tâches<br>-<strong>Minimum</strong> : minimum en temps, effort (devs, ressources), coûts, fonctionnalités<br>- <strong>Viable</strong> : valeur réelle pour les 1ers utilisateurs, valeur d’apprentissage sur le besoin et la pertinence des solutions, stabilité fonctionnelle et technique</p> | <p>produit opérationnel (site, app...)<br>documentation fonctionnelle associée<br>documentation technique(dossiers d'architecture)</p> |
| **4. Construction**                                      | Continuer à développer le produit par incréments stables                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                                                                                                                        |
| **5. Généralisation**                                    | Étendre le produit à 100 % de la cible                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                                                                                        |
| **6. Arrêt**                                             | Le produit ne touche plus son audience ou bien est remplacé. Le produit peut s'arrêter à chaque étape                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | <p>calendrier d'arrêt<br>post-mortem<br>documentations à jour<br>communication interne/externe</p>                                     |

***

## Je suis chef.fe de produit

### Je travaille sur un nouveau produit

Je remplis [ce formulaire](https://www.demarches-simplifiees.fr/commencer/dnum-comite-produit-inscription-d-un-produit) avec les informations que j'ai, pour prendre contact avec le Comité Produit.

### J'ai besoin d'aide et d'accompagnement

J'ai besoin d'appui sur le design, la recherche utilisateur, l'accessibilité, l'architecture, la sécurité, la méthodo... Je contacte le [bureau Design et Développement](https://msociauxfr.sharepoint.com/teams/BureauDesignDev) qui est là pour m'aider.
