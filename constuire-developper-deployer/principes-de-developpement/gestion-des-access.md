# 🔒 Gestion des accès

## Enjeux

La gestion des accès (ou ses synonymes habilitations, droits, autorisations...) couvre :

* la création et la suppression d’un compte utilisateur
* la validation et le rattachement hiérarchique des comptes utilisateurs créés
* la gestion des accès aux différentes fonctionnalités et données de l'application
* la délégation de gestion à un autre utilisateur ou groupe d'utilisateurs
* la traçabilité de ces actions

La gestion des accès implique nécessairement la recherche de compromis entre :

* **UX** : parcours fluide pour les utilisateurs (éviter de recréer des comptes et mot de passe…)
* **Sécurité** : contrôler raisonnablement l’accès aux ressources
* **Exploitabilité** : minimiser l’effort de provisionnement des comptes et habilitations, et du support associé
* **Complexité fonctionnelle** :
  * Ne restreindre l'accès aux fonctionnalités et aux données, que si c’est strictement nécessaire
  * Ne gérer les habilitations fines de niveau champ, que si c’est strictement nécessaire
  * Si besoin, enrichir la gestion des habilitations avec les incréments du produit

## Recommandations

1. **Automatiser le provisionnement des accès autant que possible**

* Pour les usagers personnes morales (entreprises, associations), utiliser les **SIRET renvoyés par ProConnect**
* Pour les agents publics en administration centrale (Ministères Sociaux) ou gérés en central (ARS, DREETS), utiliser :
  * l’**entité d’appartenance renvoyée par ProConnect** au format DNUM/SDPSN/DD
  * ou à défaut, le **nom de domaine FQDN de l’email** (ex: @ars.sante.fr, @oise.gouv.fr)
* Pour les collectivités territoriales, utiliser :
  * le **nom de domaine FQDN de l’email** (ex: oise.fr)
  * ou éventuellement les SIRET renvoyés par ProConnect

2. **Centraliser la gestion des rôles et habilitations par domaine métier**\
   Notamment s'il existe (Domaine DGEFP, DGT, SMS)Un serveur d’authentification par domaine métier si possible
3. **Déléguer la gestion des comptes partenaires**\
   La gestion des comptes partenaires (identités, rôles, habilitations) DEVRAIT être déléguée aux partenaires eux-mêmes, par exemple via les espaces partenaires d'EFPConnect, ProConnect et Plage.

/!\ Les annuaires AD du Ministère ne contiennent ni rôles ni habilitations.
