# Passation des projets

Dans le cadre de nos développements internes, il nous arrive de léguer nos projets à des équipes externes afin d'assurer
une continuité dans leur évolution, et aussi de pouvoir prioriser d'autres sujets.

Nous suivons une checklist afin de nous assurer que la passation se déroule bien, et de tirer de ce processus des
apprentissages qui pourront être partagés.

## Utilisation

Cette checklist est partagée entre les membres de l'équipe et la ou les personnes arrivant sur le projet.
Pour chacune des cases à cocher, sentez-vous libre de supprimer les mentions inutiles et d'ajouter des porteurs et des
dates de réalisation pour chacune des actions.

Exemple :
```markdown
### Accès

Les accès suivants ont été accordés :
- [ ] @JohnDoe - 31/02/2042 : Dépôt GitHub
- [ ] @JaneDoe - 32/02/2042 : Figma
```

---

## Checklist

### Accès

Les accès suivants ont été accordés :
- [ ] Dépôt GitHub
- [ ] Figma
- [ ] Jira
- [ ] Mattermost
- [ ] Miro
- [ ] Sharepoint

### Inclusion

- [ ] Les invitations aux dailies et autres rituels ont été envoyées

### Montée en compétence

- [ ] Des tickets avec un périmètre cadré, et relativement simples à réaliser, sont présents dans Jira afin de permettre
  une montée en compétence progressive sur le projet ;

### Partage d'informations

- [ ] Des choix techniques importants pour l'équipe sont documentés dans le même dépôt que le code ;
- [ ] La gestion de la dette technique est visibilisée sous forme de tickets sur Jira ou de documentation dans le même
  dépôt que le code ;
- [ ] Le contexte du projet et sa proposition de valeur ont été expliqués ;

### Prise en main initiale

- [ ] Le projet tourne avec `docker` et `docker-compose`, conformément à ce qui est précisé [ici](cloud-native.md) ;
- [ ] Un fichier `README.md` existe à la racine du projet et indique comment lancer le projet ;

### Production de valeur continue

- [ ] Des tickets priorisés et suffisamment clairs sont présents dans le backlog sur Jira ;
