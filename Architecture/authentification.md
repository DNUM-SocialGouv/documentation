# Authentification
Normes et standard pour l'authentification des différentes populations d'utilisateurs.

## Standard pour l'authentification des populations
|Population cible|Solution(s) préconisée(s)|
|---|---|
|**Agent du MAS</br>Agent d'autres Ministères</br>Service déconcentré de l'Etat**|Si dispo EBIOS 1 à 3 : ProConnect seul</br>Si dispo EBIOS 4 : Solution spécifique (nécessaire) ET ProConnect (facultatif)|
|**Collectivité territoriale**</br>(région, département, commune)|ProConnect Identité</br>_(pas de FI ProConnect identifié)_|
|**Entreprise du secteur privé**|ProConnect|
|**Association loi 1901 avec/sans SIRET**|ProConnect|
|**Particulier**|Nécessaire : Solution spécifique (email, lien magique)</br>Facultatif : FranceConnect OU FranceConnect+|
|**Professionnel de Santé**</br>dans l'exercice de la médecine|Pro Santé Connect (carte CPS / e-CPS)|
|**Santé et Médico-Social**</br>hors champ médical stricte|Plage / Pasrel|

## Solutions existantes

**Solution spécifique - SSO LDAP** repose sur des annuaires LDAP et un système d'authentification intégré à l'application : framework type Spring Security et/ou serveur IAM dédié Keycloak.\
MFA : Oui avec Keycloak

**Solution spécifique - Sans SSO** repose sur une gestion locale des comptes utilisateurs sans. Cette solution ne DEVRAIT PAS être mise en œuvre, ou alors de manière provisoire pour un POC/MVP.\
MFA : Oui avec Keycloak

**Solution spécifique - Lien magique** : lorsque les utilisateurs se connectent seulement de manière occasionnelle (ex: mise à jour périodique de référentiels), envisager une solution sans mot de passe (ex: jeton d'accès à usage unique sous forme de lien magique envoyé par email).\
MFA : Non

[**FranceConnect**](https://franceconnect.gouv.fr/franceconnect) permet de déléguer l'authentification d'un Particulier à un Fournisseur d'Identité connu. Il convient cependant de réconcilier les identités à la première connexion (création ou rapprochement de compte dans l'application) et lors des connexions suivantes.\
MFA : Non

[**FranceConnect+**](https://franceconnect.gouv.fr/franceconnect-plus) est utilisé par le Founrisseur de Service dans le cas de démarches avec données particulièrement sensibles, données de santé et flux financiers. Dans ce cas un 2nd facteur d'authentification (App mobile France Identité) entre en jeu.\
MFA : Oui

[**ProConnect**](https://www.proconnect.gouv.fr/) sert à identifier tout professionnel du public ou du privé. Le fonctionnement est très différent suivant que l'utilisateur est connu ou pas de l'un des Fournisseurs d'Identité (cf. comparaison infra). A noter aussi que le Fournisseur de Service choisit sa surface d'exposition lors du raccordement à ProConnect : Internet (accès FS public via FI public), RIE (accès FS @RIE via FI @RIE), Hybride (accès FS public via FI @RIE).\
MFA : Oui

[**EFPConnect**](https://info.efpconnect.emploi.gouv.fr/) conjointement à MesDémarchesEmploi est le vecteur d'authentificaiton actuel pour les démarches de la sphère Emploi (DGEFP). Il convient de clarifier sa cible et sa trajectoire.\
MFA : Non

[**Pro Santé Connect**](https://esante.gouv.fr/produits-services/pro-sante-connect) authentifie et identifie obligatoirement les Professionnels de Santé dans l'exercice de la médecine. Il repose sur les cartes professionnelles CPS et e-CPS, et le répertoire RPPS. Le raccordement d'un service est très lourd.\
MFA : Oui

[**Plage (aka compte Pasrel)**](https://connect-pasrel.atih.sante.fr/cas/login) sert à identifier les personnes de la sphère Santé et Médico-Social, dans le périmètre de l'ATIH. Il repose sur le répertoire FINESS des Etablissements de Santé et de leurs collaborateurs.\
MFA : Non

## ProConnect vs ProConnect Identité
_MonComptePro, InclusionConnect et AgentConnect ont fusionné pour devenir ProConnect._
Le fonctionnement de ProConnect est différent suivant que l'utilisateur est connu ou pas d'un Fournisseur d'Identité :
|Aspect|ProConnect (avec FI)|ProConnect Identité|
|---|---|---|
|Authentification|Authentification portée par un FI du public. Routage vers le bon FI basé sur le FQDN de l’email. [La table de correspondance est portée par ProConnect](https://grist.incubateur.net/o/docs/3kQ829mp7bTy/ProConnect-Configuration-des-Fournisseurs-dIdentite)|Compte email à créer sur ProConnect. Pas d’authentification par FI pour les comptes ProConnect Identité. C’est ProConnect qui porte une authentification par mot de passe.|
|Traits d’identité et données individuelles|Fourni par le FI|Gestion libre sur le compte ProConnect|
|Entité(s) de rattachement|Fournie(s) par le FI.|Gestion libre des SIRET sur le compte ProConnect. Certification du dirigeant à venir (2025)|

## Transition EFPConnect vers ProConnect (à décider)
|Scénario|Avantages|Inconvénients|
|---|---|---|
|I. ProConnect sur MesDémarches|Scénario pouvant servir de solution transitoire tout au long du scénario 2.</br>Réconciliation de comptes à implémenter seulement sur EFPConnect dans un premier temps (effort centralisé).</br>L’utilisateur n’a plus besoin de créer explicitement un compte EFPConnect et retenir un mot de passe EFPConnect.</br>Permet de mitiger le risque d'un « plouf » de ProConnect|Ajoute des redirections à l’utilisateur dans la cinématique d’authentification.</br>Moindre lisibilité et compréhension de la cinématique par l’utilisateur|
|II. ProConnect remplace EFPConnect|Implémentation progressive de ProConnect, service par service.</br>Décommissionnement progressif puis définitif d’EFPConnect|Réconciliation de comptes à implémenter seulement sur EFPConnect (pratique de réconciliation à harmoniser)

A noter : beaucoup de liens morts sur MesDémarches/EFPConnect. Combien de services actifs parmi les 20 listés sur MesDémarches ? Est-il déjà acté de décommissionner MesDémarches?