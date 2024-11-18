# Authentification
Normes et standard pour l'authentification des différentes populations d'utilisateurs.

## Préconisation principale pour l'authentification des populations
|Population cible|Solution(s) préconisées|
|---|---|
|<b>Agent du MAS</b>|Solution maison|
|<b>Particulier</b>|FranceConnect OU FranceConnect+|
|<b>Secteur privé, associations</b>|ProConnect|
|<b>Agent d'autres Ministères, collectivités territoriales</b>|ProConnect|
|<b>Professionnels de santé</b>|(e-)CPS / Plage|

## Solutions existantes

<b>Solution maison - SSO LDAP</b> repose sur un annuaire LDAP (généralement Active Directory mais aussi AC, SD, EntraID?) et un système d'authentification (composant, framework ou serveur dédié type KeyCloak).
<br>MFA : Oui avec KeyCloack

<b>Solution Maison - spécifique</b> repose sur une gestion locale des comptes utilisateurs. Cette solution ne DEVRAIT PAS être mise en oeuvre, ou alors de manière provisoire pour un MVP.
<br>MFA : Non

<b>FranceConnect</b> permet de déléguer l'authentification d'un Particulier à un Fournisseur d'Identité connu. Il convient cependant de réconcilier les identités à la première connexion (création ou rapprochement de compte dans l'application) et lors des connexions suivantes.
<br>https://franceconnect.gouv.fr/franceconnect
<br>MFA : Non

<b>FranceConnect+</b> est utilisé par le Founrisseur de Service dans le cas de démarches avec données sensibles, données de santé et flux financiers. Dans ce cas un 2nd facteur d'authentification (App mobile France Identité) entre en jeu.
<br>https://franceconnect.gouv.fr/franceconnect-plus
<br>MFA : Oui

<b>ProConnect</b> sert à identifier tout professionnel du public ou du privé. Cela dit le fonctionnement est très différent pour le public et le privé (cf. comparaison infra). Il convient de choisir la surface d'exposition de ProConnect pour chaque fournisseur de service : Internet, RIE, Hybride.
<br>https://www.proconnect.gouv.fr/
<br>MFA : T1 2025 

<b>EFPConnect</b> conjointement à MesDémarchesEmploi est le vecteur d'authentificaiton actuel pour les démarches de la sphère Emploi (DGEFP). Il convient de clarifier sa cible et sa trajectoire.
<br>https://info.efpconnect.emploi.gouv.fr/
<br>MFA : Non

<b>Pro Santé Connect</b> authentifie et identifie obligatoirement les Professionnels de Santé dans l'exercice de leur métier. Il repose sur les cartes professionnelles CPS et e-CPS, et le répertoire RPPS. Le raccordement d'un service est très lourd.
<br>https://esante.gouv.fr/produits-services/pro-sante-connect
<br>MFA : Oui

<b>Plage</b> conjointement avec le portail e-MPSI sert à identifier les Etablissements de Santé et leurs collaborateurs, dans la sphère Santé et Médico-Social donc. Il repose sur le répertoire FINESS des Etablissements de Santé.
<br>https://connect-pasrel.atih.sante.fr/cas/login
<br>MFA : Non

## ProConnect Public vs Privé
MonComptePro, InclusionConnect et AgentConnect fusionnent pour devenir ProConnect. Néanmoins le fonctionnement de ProConnect est différent suivant les cas d'utilisateurs publics et privés :
|Aspect|ProConnect<br>pour agents publics|ProConnect<br>pour secteur privé|
|---|---|---|
|Authentification|Authentification portée par un FI du public. Routage vers le bon FI basé sur le FQDN de l’email. La table de correspondance est portée par ProConnect : https://grist.incubateur.net/o/docs/3kQ829mp7bTy/ProConnect-Configuration-des-Fournisseurs-dIdentite|Compte email à créer sur ProConnect. Pas d’authentification par FI pour les comptes ProConnect du privé. C’est ProConnect qui porte une authentification par mot de passe.|
|Traits d’identité et données individuelles|Fourni par le FI|Gestion libre sur le compte ProConnect|
|Entité(s) de rattachement|Fournie(s) par le FI<br>Voir modèle de données pour multi-affectations?<br>SIRET(s) pour services déconcentrés ?|<br>Gestion libre des SIRET sur le compte ProConnect<br>Certification du dirigeant à venir (2025)|


## Points à traiter
- <b>Délégation de gestion</b> la connexion par un mandataire, expert-comptable, juriste/avocat, tuteur, etc. n’est pas étudiée à ce stade (ex : AidantsConnect)
- <b>Associations</b>
- <b>Services déconcentrés</b> : collectivités territoriales, parapublic, etc.
- <b>Sphère Santé et Médico-Social</b>
- <b>Habilitation</b> : L’authentification d’agents publics et d’entreprises privées ne dispensent pas forcément de provisionner des comptes dans les apps (gestion des habilitations). Il est cependant possible d’automatiser certaines habilitations via les données fournies par le vecteur d’authentification (unités d’appartenance, FQDN de l’email, SIRET…)
- <b>Keycloack</b> : avantages/inconvénients d'une instance Keycloack partagée
- <b>EFPConnect vs ProConnect</b> : faire arrêter la stratégie en COPRO ? Qui décide in fine ? Garder MesDémarches comme catalogue de démarches?
- <b>Harmoniser les pratiques d’implémentation FranceConnect et ProConnect</b> :
    - Réconciliation de compte avec FranceConnect/ProConnect lors de la création puis à chaque authentification (y a-t-il déjà un compte existant, quels champs pour le rapprochement, etc.)
    - Ajouter une matrice pour la cohabitation de différents vecteurs d’authentification (ex. FranceConnect + ProConnect + email)
- <b>RENATER</b> : Quid de la fédération d’identité RENATER qui apparait distinctement dans ProConnect (hors cinématique de base). Des applications du MAS sont-elles concernées par le FI RENATER ?

## Transition EFPConnect vers ProConnect
|Scénario|Avantages|Inconvénients|
|---|---|---|
|I. ProConnect sur MesDémarches|+ Scénario pouvant servir de solution transitoire tout au long du scénario 2<br>+ Réconciliation de comptes à implémenter seulement sur EFPConnect dans un premier temps (effort centralisé)<br>+ L’utilisateur n’a plus besoin de créer explicitement un compte EFPConnect et retenir un mot de passe EFPConnect<br>+ Permet de dérisquer un « plouf » de ProConnect|- Ajoute des redirections à l’utilisateur dans la cinématique d’authentification<br>- Moindre lisibilité et compréhension de la cinématique par l’utilisateur|
|II. ProConnect remplace EFPConnect|+ Implémentation progressive de ProConnect, service par service<br>+ Décommissionnement progressif puis définitif d’EFPConnect|- Réconciliation de comptes à implémenter seulement sur EFPConnect (pratique de réconciliation à harmoniser)

<u>/!\\</u> Beaucoup de liens morts sur MesDémarches/EFPConnect. Combien de services actifs parmi les 20 listés sur MesDémarches ? Est-il déjà acté de décommissionner MesDémarches?