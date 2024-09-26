# Observabilité

## Gestion des erreurs et alertes

L'application doit utiliser Sentry ou une solution équivalente.

## Suivi des performances

L'application doit utiliser une solution de traces pour suivre les performances (APM: application performance management).

La solution préconisée est Sentry

## Logs

Les logs de l'application doivent :

- être formattés en json pour être facilement exploités dans Grafana ou Kibana
- ne pas contenir d'information personnelle et/ou sensible
- contenir un maximum de contexte (ex: requête http en cours, id utilisateur, autres informations utiles au débogage)
- contenir la liste des requêtes http (access logs) : domaine, path, duration, etc.
