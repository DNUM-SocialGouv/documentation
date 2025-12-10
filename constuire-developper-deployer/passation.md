# 🔁 Passation des projets

Dans le cadre de nos développements internes, il nous arrive de léguer nos projets à des équipes externes afin d'assurer une continuité dans leur évolution, et aussi de pouvoir prioriser d'autres sujets.

Nous suivons une checklist afin de nous assurer que la passation se déroule bien, et de tirer de ce processus des apprentissages qui pourront être partagés.

## Utilisation

Cette checklist est partagée entre les membres de l'équipe et la ou les personnes arrivant sur le projet. Pour chacune des cases à cocher, sentons-nous libre de supprimer les mentions inutiles, d'en ajouter de nouvelles propres au projet et d'ajouter des porteurs et des dates de réalisation pour chacune des actions.

Exemple :

```markdown
### Accès

Les accès suivants ont été accordés :

- [ ] @JohnDoe - 31/02/2042 : Dépôt GitHub
- [ ] @JaneDoe - 32/02/2042 : Figma
```

***

## Checklist

### Accès

Les accès suivants ont été accordés :

* [ ] Dépôt GitHub
* [ ] Figma
* [ ] Groupe Teams
* [ ] Hébergement :
  * [ ] Cegedim
  * [ ] Scalingo
* [ ] Jira
* [ ] Mattermost
* [ ] Mattomo
* [ ] Miro
* [ ] Sentry
* [ ] Sonar
* [ ] Sharepoint

### Inclusion

* [ ] Les invitations au daily et autres rituels sont envoyées ;
* [ ] Les membres de l'équipe, ainsi que les stakeholders et les personnes clés sont présentées ;
* [ ] Une personne de l'équipe est désignée comme "[Buddy](https://factorial.fr/blog/buddy-parrainage/)" afin de faciliter l'intégration dans l'équipe ;

### Montée en compétence

* [ ] Des tickets avec un périmètre cadré, et relativement simples à réaliser, sont présents sur Jira afin de permettre une montée en compétence progressive sur le projet ;

### Nettoyage du travail existant

* [ ] Aucune branche en cours n'est présente lors de la passation ;
* [ ] Toutes les branches déjà intégrées à la branche principale, ou inutiles, sont supprimées ;
* [ ] Toutes les branches sont poussées sur le dépôt git, quel que soit leur état d'avancement ;
  * [ ] Un statut sur leur contenu est fourni dans une PR ;
  * [ ] Toute autre information permettant la reprise est ajoutée ;

### Partage d'informations

* [ ] Des choix techniques importants pour l'équipe sont documentés dans le même dépôt que le code ;
  * [ ] Des pratiques standards sont présentes au sein de l'équipe ;
  * [ ] La stratégie de tests est présente ;
  * [ ] Le Dossier d'Architecture est commenté ;
  * [ ] Si applicable, les requêtes particulièrement complexes vers la base de données sont documentées ;
* [ ] La chaîne de CI est présentée, ainsi que ses étapes ;
* [ ] La gestion de la dette technique est visibilisée sous forme de tickets sur Jira ou de documentation dans le même dépôt que le code ;
* [ ] La stratégie de gestion des branches git est précisée dans une documentation dans le dépôt ;
* [ ] Le contexte du projet et sa proposition de valeur, ainsi que le domaine fonctionnel et le périmètre existant sont présentés grâce à une démonstration du projet ;
  * [ ] L'historique (pertinent) du projet est expliqué ;
* [ ] Les tickets sur Jira sont présentés, ainsi que leur thématique fonctionnelle ;
* [ ] Si applicable, les éventuelles échéances à venir sont présentées avec leurs finalités ;
* [ ] Une description des environnements est faîte, et la procédure de déploiement sur les différents environnements est documentée ;

### Prise en main initiale

* [ ] Le projet tourne avec `docker` et `docker-compose`, conformément à ce qui est précisé [ici](principes-de-developpement/cloud-native.md) ;
  * [ ] Les dépendances spécifiques, manuelles et/ou implicites, est indiquées ainsi que comment les gérer et leur utilité ;
* [ ] Les procédures de migrations de schéma de base de données sont présentes et documentées ;
  * [ ] Si applicable, les scripts d'initialisation ou d'hydratation pour les données de tests sont présents et documentés ;
* [ ] Un fichier `README.md` existe à la racine du projet et indique comment lancer le projet ;

### Production de valeur continue

* [ ] Des tickets priorisés et suffisamment clairs sont présents dans le backlog sur Jira, afin qu'ils puissent être réalisés une fois la passation terminée ;
