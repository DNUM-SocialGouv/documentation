# Processus asynchrone

## Différences avec un processus synchrone

Dans le cas d'un processus synchrone, lorsqu'un utilisateur utilise une interface pour envoyer une requête quelconque,
sa réponse arrivera dès que le serveur aura terminé de la traiter.

![sync.png](img/sync.png)

1. L'utilisateur utilise l'interface de l'application pour exécuter une action,
2. Une requête est utilisée au serveur,
3. Le serveur la traite,
4. Le serveur renvoie une réponse,
5. L'utilisateur peut continuer d'utiliser l'application.

En revanche, dans le cas d'un processus asynchrone, le serveur répond qu'il a tenu compte de la requête dès qu'il la 
reçoit. Cela lui permettra de la traiter à un moment opportun et surtout de redonner la main à l'utilisateur, qui pourra
continuer d'utiliser le produit.

![async.png](img/async.png)

1. L'utilisateur utilise l'interface de l'application pour exécuter une action,
2. Une requête est utilisée au serveur,
3. Le serveur la prend en compte et renvoie à l'utilisateur que sa requête va être traitée,
4. L'utilisateur a de nouveau la main pour manipuler l'interface,
5. Le serveur a terminé de traiter la requête et le résultat est disponible.

## Avantages et inconvénients

## Quand utiliser un process asynchrone

## Quels moyens de récupérer une information
