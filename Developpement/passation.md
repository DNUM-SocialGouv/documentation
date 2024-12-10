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

### Nettoyage du travail existant

- [ ] Toutes les branches mergées, ou inutiles, ont été supprimées ;
- [ ] Toutes les branches ont été poussées sur le dépôt git, quel que soit leur état d'avancement ;
  - [ ] Un statut sur leur contenu a été fourni dans une PR ;
  - [ ] Toute autre information permettant la reprise a été ajoutée ;

### Partage d'informations

- [ ] Des choix techniques importants pour l'équipe sont documentés dans le même dépôt que le code ;
  - [ ] Si applicable, les requêtes particulièrement complexes vers la base de données sont documentées ;
- [ ] La gestion de la dette technique est visibilisée sous forme de tickets sur Jira ou de documentation dans le même
  dépôt que le code ;
- [ ] La stratégie de gestion des branches git a été précisée dans une documentation dans le dépôt ;
- [ ] Le contexte du projet et sa proposition de valeur ont été expliqués ;

### Prise en main initiale

- [ ] Le projet tourne avec `docker` et `docker-compose`, conformément à ce qui est précisé [ici](cloud-native.md) ;
  - [ ] Les dépendances spécifiques, manuelles et/ou implicites, ont été indiquées ainsi que comment les gérer et leur
        utilité ;
- [ ] Les procédures de migrations de schéma de base de données sont présentes et documentées ;
  - [ ] Si applicable, les scripts d'initialisation ou d'hydratation pour les données de tests sont présents et
        documentés ;
- [ ] Un fichier `README.md` existe à la racine du projet et indique comment lancer le projet ;

### Production de valeur continue

- [ ] Des tickets priorisés et suffisamment clairs sont présents dans le backlog sur Jira ;
