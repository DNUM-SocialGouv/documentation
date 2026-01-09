# 🔁 Passation des projets internes

Dans le cadre de nos développements internes, il arrive de transférer nos projets à des équipes externes afin d'assurer une continuité dans leur évolution, et de pouvoir prioriser d'autres sujets.

Nous suivons la checklist ci-dessous afin que la passation se déroule au mieux, et afin d'en tirer des apprentissages pour tous. Cette checklist est partagée entre les membres de l'équipe et les personnes arrivant sur le projet. Pour chacune des cases à cocher, sentons-nous libre d'ajouter des porteurs et des dates de réalisation pour chacune des actions. Exemple :

```markdown
## Accès aux outils

Les accès suivants ont été accordés :

- [ ] @JohnDoe - 31/02/2042 : Dépôt GitHub
- [ ] @JaneDoe - 32/02/2042 : Figma
```
## Accès aux outils

Les accès suivants ont été accordés :
* [ ] Dépôt GitHub
* [ ] Figma
* [ ] Groupe Teams
* [ ] Hébergement :
  * [ ] Atlas
  * [ ] Cegedim
  * [ ] Scalingo
* [ ] Jira
* [ ] Mattermost
* [ ] Matomo
* [ ] Miro
* [ ] Sentry
* [ ] Sonar
* [ ] Sharepoint

## Embarquement des équipes

* [ ] Les invitations au daily et autres rituels sont envoyées
* [ ] Les membres de l'équipe, les parties prenantes et les personnes clés sont présentées
* [ ] Une personne de l'équipe est désignée comme "[Buddy](https://factorial.fr/blog/buddy-parrainage/)" afin de faciliter l'intégration dans l'équipe

## Montée en compétence

* [ ] Des tickets avec un périmètre clair, et relativement simples à réaliser, sont présents sur Jira afin de permettre une montée en compétence progressive

## Nettoyage du travail existant

* [ ] Aucune branche en cours n'est présente lors de la passation
* [ ] Toutes les branches déjà intégrées à la branche principale, ainsi que les branches inutiles, sont supprimées
* [ ] Toutes les branches sont poussées sur le dépôt git, quel que soit leur état d'avancement
  * [ ] Un statut sur leur contenu est fourni dans une PR
  * [ ] Toute autre information permettant la reprise est ajoutée

## Partage d'informations

Les éléments suivant sont impérativement présents, soit sous forme de tickets dans le backlog (Jira), soit sous forme de documentation dans le repo du code source :
* [ ] Les choix techniques importants
  * [ ] Pratiques standards au sein de l'équipe
  * [ ] Stratégie de tests
  * [ ] Documentation des requêtes SQL particulièrement complexes
* [ ] Lien vers le Dossier d'Architecture auto-portant et à jour
* [ ] La chaîne de CI et ses étapes
* [ ] L'état précis et la gestion de la dette technique
* [ ] La stratégie de gestion des branches git
* [ ] Le contexte du projet et sa proposition de valeur, ainsi que le domaine fonctionnel et le périmètre existant sont présentés grâce à une démonstration du projet
  * [ ] L'historique (pertinent) du projet
* [ ] Les tickets sur Jira sont présentés, ainsi que leur thématique fonctionnelle
* [ ] Les éventuelles échéances à venir et leurs finalités
* [ ] Une description des différents environnements et de la procédure de déploiement sur chaque environnement

## Prise en main initiale

* [ ] Le projet tourne avec `docker` et `docker-compose`, conformément à l'approche [cloud native](principes-de-developpement/cloud-native.md)
  * [ ] Les dépendances spécifiques, manuelles et/ou implicites, sont indiquées ainsi que comment les gérer et leur utilité
* [ ] Les procédures de migrations de schéma de base de données sont documentées
  * [ ] Si applicable, les scripts d'initialisation ou d'hydratation pour les données de tests sont présents et documentés
* [ ] Un fichier `README.md` existe à la racine du projet et indique comment lancer le projet

## Production de valeur continue

* [ ] Des tickets priorisés et suffisamment clairs sont présents dans le backlog sur Jira, afin qu'ils puissent être réalisés une fois la passation terminée
