# 🔒 Authentification via Pro Santé Connect

## Intro

Cette page synthétise quelques informations de présentations de PSC disponibles [ici](https://industriels.esante.gouv.fr/produits-et-services/pro-sante-connect)
et répertorie les actions à effectuer pour activer l'authentification via PSC.

## Présentation 

Pro Santé Connect (PSC) est le Fournisseur d'Identité (FI) officiel du secteur de la santé en France, développé et maintenu par l'Agence du Numérique en Santé (ANS). Il s'agit d'un service standard basé sur le protocole OpenID Connect, gratuit et conforme aux exigences réglementaires.
Grâce à Pro Santé Connect, les professionnels de santé recensés dans l'Annuaire Santé (alimenté par le répertoire RPPS) peuvent s'authentifier de manière simple, sécurisée et unifiée sur les services numériques en santé.
Depuis le 1er janvier 2023, l'implémentation de PSC est **obligatoire** pour tous les services numériques en santé dits "sensibles" (au sens défini dans la PGSSI-S).

**Quelques chiffres**

* 611 services raccordés en production
* Plus de 2 millions d'authentifications sur le dernier mois
* 38% d'authentifications par e-CPS (carte électronique)
* Jusqu'à 11 millions d'authentifications mensuelles au pic d'utilisation

## Pré-requis

1. Créer un compte responsable technique sur iSC
   Inscrivez-vous sur iSC (Fournisseur d'Identité de l'ANS pour les Industriels). Ce compte unique vous donnera accès à tous les services clés de l'ANS :

   * Espace Authentifié du Portail Industriels
   * Plateforme Convergence
   * Statistiques PSC
   * Et autres services ANS

(Délai : immédiat)

2. Effectuer une demande d'accès à l'API Pro Santé Connect
   L'accès aux fonctionnalités PSC nécessite une demande DataPass spécifique à chaque besoin.

    Important : Une demande DataPass distincte est requise pour chaque service que vous souhaitez raccorder.

(Délai : variable selon validation)

3. Activer votre Espace Authentifié
   Une fois votre compte iSC créé et validé, activez votre Espace Authentifié pour accéder à des informations personnalisées adaptées à vos besoins.

(Délai : immédiat après validation du compte)


## Parcours de raccordement

Le parcours de raccordement est détaillé [ici](https://industriels.esante.gouv.fr/produits-et-services/pro-sante-connect/parcours-raccordement).


## Notes : 

*Le raccordement à l'environnement de bac à sable (BAS) peut se faire rapidement et permets de commencer à travailler 
à l'intégration de PSC dans nos applications. Il y a également une application Android eCPS BAS qui permets de tester 
l'authentification via PSC.*

*Attention pour la validation de notre compte iSC, pour les comptes de l'organisation DNUM
des collègues sont déjà existants dans iSC en tant que référents. En même temps que la demande il est conseillé 
de contacter M. Lascombes ou M. Borgis.*

*Pro Santé Connect a fait le choix de ne pas gérer les "profils" mais envoie toutes les informations 
nécessaires (Exercices et activités) dans l'endpoint UserInfo. C'est à la charge de l'application si besoin
de proposer les profils disponibles.*

*Pour notre projet nous ne savions pas exactement quels attributs allaient être renseignés dans le retour JSON
de l'endpoint UserInfo. L'ANS propose un [simulateur](https://essaietaecps.eservices.esante.gouv.fr/) pour avoir cette visibilité.
De cette manière on peut récupérer un JSON de nos utilisateurs en production et l'affecter dans nos profils de test via
leur autre outil [EDIT](https://edit.esante.gouv.fr/login)*

*Le support Pro Santé Connect réponds en général efficacement sous quelques jours : prosanteconnect.editeurs@esante.gouv.fr*
