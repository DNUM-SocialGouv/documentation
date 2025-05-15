---
icon: eyes
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

# Observabilité

## Erreurs

### Checklist

* [ ] Utiliser un outil de remontée d'erreurs avec toute la pile d'appels de fonctions (ex : [Sentry](https://sentry.io/welcome/)).
* [ ] Ajouter des alertes et des notifications sur l'environnement de production.

### Bonnes pratiques

* Les erreurs doivent être remontées avec un maximum de contexte.
* **Attention : ne pas transmettre d'informations personnelles et sensibles**.

## Suivi des performances

### Checklist

* [ ] Utiliser une solution de traces pour suivre les performances (APM : [application performance management](https://fr.wikipedia.org/wiki/Application_performance_management)).
  * Ex de solutions : [Sentry](https://sentry.io/welcome/), [Elastic APM](https://www.elastic.co/observability/application-performance-monitoring) ou [Tempo](https://grafana.com/docs/tempo/latest/) via Grafana.
* [ ] Ajouter des alertes et des notifications sur l'environnement de production.
  * Ex : alerte si le P95 des requêtes back-end dépasse 1s.

## Logs

### Checklist

Les logs de l'application doivent :

* [ ] Être formatés en JSON (pour être facilement filtrables dans Grafana ou Kibana).
* [ ] Ne pas contenir d'information personnelle et/ou sensible.
* [ ] Contenir un maximum de contexte (ex : requête HTTP en cours, ID utilisateur, autres informations utiles au débogage).
* [ ] Contenir la liste des requêtes http (access logs) : domaine, chemin, durée, etc.

Des alertes peuvent être mises en place sur les logs pour détecter des comportements anormaux si les alertes d'erreurs et de performance ne suffisent pas.
