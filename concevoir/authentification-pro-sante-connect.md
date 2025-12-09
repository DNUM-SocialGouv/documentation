# 🔒 Pro Santé Connect

Pro Santé Connect (PSC) est le Fournisseur d'Identité (FI) officiel des Professionnels de Santé (PS) en France. PSC est :
* Développé et maintenu par l'Agence du Numérique en Santé (ANS)
* Basé sur les PS dans l'Annuaire Santé, lui-même alimenté par le répertoire RPPS
* Basé sur le protocole standard OpenID Connect
* Gratuit
* Conforme aux exigences réglementaires
* Obligatoire depuis 2023 pour tous les services numériques en santé dits "sensibles" (au sens défini dans la PGSSI-S)

**Quelques chiffres :**

* Plus de 600 services raccordés en production
* Plusieurs millions d'authentifications par mois et jusqu'à 11 millions en pic
* 38% d'authentifications par e-CPS (carte électronique sur smartphone)

## Pré-requis

1. Créer un compte responsable technique sur iSC
   S'inscrire sur iSC (Fournisseur d'Identité de l'ANS pour les Industriels). Ce compte unique donne accès à tous les services clés de l'ANS :

   * Espace Authentifié du Portail Industriels
   * Plateforme Convergence
   * Statistiques PSC
   * Etc.

(Délai : immédiat)

2. Effectuer une demande d'accès à l'API Pro Santé Connect
   L'accès aux fonctionnalités PSC nécessite une demande DataPass, distincte pour chaque service à raccorder.

(Délai : variable selon validation)

3. Activer votre Espace Authentifié
   Une fois votre compte iSC créé et validé, activez votre Espace Authentifié pour accéder à des informations personnalisées adaptées à vos besoins.

(Délai : immédiat après validation du compte)


## Parcours de raccordement

Le parcours de raccordement est [détaillé ici](https://industriels.esante.gouv.fr/produits-et-services/pro-sante-connect#paragraph-id--34273).


## Notes
* Le raccordement à l'environnement de bac à sable (BAS) peut se faire rapidement et permet de commencer à travailler 
à l'intégration de PSC dans nos applications. Une application Android eCPS BAS permet de tester 
l'authentification via PSC.
* Attention pour la validation de notre compte iSC, pour les comptes de l'organisation DNUM
des collègues sont déjà existants dans iSC en tant que référents. Il est conseillé de les contacter en même temps que la demande.
* Pro Santé Connect a fait le choix de ne pas gérer les "profils" mais envoie toutes les informations 
nécessaires (Exercices et activités) dans l'endpoint UserInfo. C'est à la charge de l'application si besoin
de proposer les profils disponibles.
* Pour notre projet nous ne savions pas exactement quels attributs allaient être renseignés dans le retour JSON
de l'endpoint UserInfo. L'ANS propose un [simulateur](https://essaietaecps.eservices.esante.gouv.fr/) pour avoir cette visibilité.
On peut ainsi récupérer un JSON de nos utilisateurs en production et l'affecter dans nos profils de test via
un autre outil [EDIT](https://edit.esante.gouv.fr/login)
* Le support Pro Santé Connect répond en général efficacement sous quelques jours : prosanteconnect.editeurs@esante.gouv.fr

## Sources de veille
[Documentation officielle](https://industriels.esante.gouv.fr/produits-et-services/pro-sante-connect)
