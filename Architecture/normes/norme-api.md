---
hidden: true
---

# Utilisation d'APIs par des applicatifs

## ADR log
22/11/2024 : Première version

## Objectifs

Le but est de définir les protocoles d'échanges via APIs utilisables par l'ensemble des applicatifs de manière à unifier les mécanismes de transfert de données.

Nous définirons des protocoles techniques, des types d'APIs et les prérequis applicables, les solutions techniques de création/consommation de ces APIs ne sont pas abordés (sous-entendu les choix techniques de framework de développement ne seront pas définis ici).

## Exigences

### Fonctionnelles

* Facilité d'intégration dans un système tiers
* Flexibilité de la requête
* Flexibilité du format de données
* Echange de données efficace

### Non-fonctionnelles

* Facilité de maintenance
* Capacité de débug
* Sécurisation des échanges en transit
* Mise à l'échelle
* Performance

### Contraintes techniques et organisationnelles

* Non lié à un outil technique/un langage de programmation/éditeur spécifique
* Des compétences techniques doivent être présentes sur le marché et en interne

## Solutions proposées

### REST (Representational State Transfer)

REST est un style d'architecture basé sur HTTP utilisant les verbes standards du protocole pour manipuler des ressources. Il est stateless et utilise généralement du JSON pour le format de données.

<details>
<summary>Avantages</summary>
  
* Basé sur le standard HTTP
* Flexible et évolutif
* Mise en cache possible
* Facile à implémenter et utiliser
* Documentation facilement générable
* Beaucoup d'outils sur le marché et en opensource

</details>

<details>
<summary>Inconvénients</summary>
  
* Suivant le cas d'usage peut nécessiter plusieurs requêtes
* Dépendant du modèle de données exposé par le système
* Mise en cache possible
* Facile à implémenter et utiliser

</details>

### SOAP (Simple Object Access Protocol)

SOAP est un protocole basé sur XML pour échanger des messages structurés. Il est indépendant du protocole de transport et propose des fonctionnalités avancées en particulier la gestion des transactions.

<details>
<summary>Avantages</summary>
  
* Fortement typé
* Indépendant du protocole
* Sécurité avancée avec Ws-Security
* Gestion native des erreurs
* Outils de génération de code disponibles

</details>

<details>
<summary>Inconvénients</summary>
  
* Complexe et verbeux
* Performances potentiellement plus faibles du fait de l'utilisation de XML
* Moins flexible
* Nécessite des outils spécialisés
* Compétence plus rare

</details>

### Webhook

Un webhook est un mécanisme de callback HTTP permettant de recevoir des notifications depuis un service externe.

<details>
<summary>Avantages</summary>
  
* Idéal pour l'asynchrone
* Bon pour le temps réel
* Réduit la charge sur le système client du fait de l'absence de polling
* Parfait pour les systèmes événementiels

</details>

<details>
<summary>Inconvénients</summary>
  
* Unidirectionnel
* Gestion des erreurs et des retries plus complexes
* Nécessite une bonne connaissance de l'asynchrone
* Debug parfois complexe
* Sécurisation plus complexe

</details>

### Graphql

Graphql est un langage de requête pour API permettant aux clients de demander exactement les données nécessaires en présentant un point d'entrée unique pour toutes les opérations.

<details>
<summary>Avantages</summary>
  
* Flexibilité maximale côté client
* Pas de sous ou sur-sollicitation de données
* Fort typage
* Documentation autogénérée et introspection
* Outils de développement puissants

</details>

<details>
<summary>Inconvénients</summary>
  
* Complexité accrue côté serveur
* Compétence plus rare
* Mise en cache plus complexe comparé
* Parfois compliqué à optimiser sur des requêtes complexes
* Sécurisation plus complexe en particulier gestion des autorisations

</details>



## Analyse comparative

|Critère|REST|SOAP|Webhook|GraphQL|
|-|-|-|-|-|
|Flexibilité|Bonne|Faible|Moyenne|Elevée|
|Performance|Bonne|Moyenne|Très bonne|Bonne|
|Complexité|Faible|Elevée|Faible|Moyenne|
|Sécurité|Bonne|Très bonne|Moyenne|Bonne|
|Scalabilité|Très bonne|Bonne|Très bonne|Bonne|
|Expérience développeur|Très bonne|Moyenne|Bonne|Très bonne|


## Recommandations

Pour l'immense majorité des applications des appels REST sont suffisants en particulier s'il s'agit d'APIs simples.

GraphQL peut être considéré en particulier s'il s'agit de livrer une API publique servant divers types de client ou alors des dashboards avec des besoins de données variés.

Les webhooks sont à considérer dans le cadre d'intégration de systèmes tiers (Github, Mattermost, services SaaS en général) mais à éviter au-delà la majorité des applications étant synchrones.

SOAP est à éviter sauf contraintes techniques avérées.