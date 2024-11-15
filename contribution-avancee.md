# Contribution avancée

## Par ligne de commande, avec clé SSH

Tout d'abord, il faut ajouter une clé SSH à votre compte GitHub et à votre poste.
La marche à suivre est documentée [ici](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

Une fois cela fait, il vous reste à récupérer [le dépôt](https://github.com/DNUM-SocialGouv/documentation) du projet :
```shell
git clone git@github.com:DNUM-SocialGouv/documentation.git
```

Ensuite, une copie (fork) du dépôt devra être faite vers votre compte GitHub, et il existe un bouton présent sur la page
d'un dépôt pour le faire.

Maintenant sur le poste local, il faut lier le dépôt copié sur votre compte au code qui a été cloné précédemment :
```shell
git remote add <NOM_REMOTE> <LIEN_GIT_DU_FORK> 
```
Où :

- `NOM_REMOTE` est le nom attribué à la [remote Git](https://git-scm.com/docs/git-remote) liée à la copie,
- `LIEN_GIT_DU_FORK` est le lien Git vers le dépôt.

Avec ces étapes, vous pourrez ensuite proposer des modifications à la documentation en :

- Créant au préalable une branche sur votre poste,
- Faire des commits,
- Et pousser les changements sur votre fork, et non pas la version distante `origin`
  - Avec `git push <NOM_REMOTE> <VOTRE_BRANCHE>`

Il ne vous restera qu'à [créer une Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork)
de votre branche, vers la branche `main` de la version `origin`, directement depuis l'interface GitHub.

### Points d'attention

Si vous avez plusieurs identités Git sur votre poste, il faudra probablement configurer Git pour qu'il utilise la bonne
identité :
```shell
git config user.email "john.doe@example.com"
```
