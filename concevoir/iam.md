---
icon: lock
---

# Authentification des utilisateurs

Cette page recense les bonnes pratiques pour l'authentification des différentes populations d'utilisateurs.

## Bonnes pratiques pour l'authentification des populations

| Population cible                                                                                                                        | Solution(s) préconisée(s)                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Agent du MAS</strong><br><strong>Agent d'autres Ministères</strong><br><strong>Service déconcentré (hors DDETS)</strong></p> | <p>Si disponibilité EBIOS 1 à 3 : ProConnect seul<br>Si disponibilité EBIOS 4 : Solution spécifique (nécessaire) ET ProConnect (facultatif)</p> |
| **Service déconcentré DDETS (@departement.gouv.fr)**                                                                                    | <p>ProConnect Identité<br><em>(en attendant un FI ProConnect du MIOM)</em></p>                                                                  |
| <p><strong>Collectivité territoriale</strong><br>(région, département, commune)</p>                                                     | <p>ProConnect Identité<br><em>(pas de FI ProConnect identifié à date)</em></p>                                                                  |
| **Entreprise du secteur privé**                                                                                                         | ProConnect Identité                                                                                                                             |
| **Association avec/sans SIRET**                                                                                                         | ProConnect Identité                                                                                                                             |
| <p><strong>Domaine DGEFP</strong><br>(entreprises, agents, associations)</p>                                                            | EFP Connect                                                                                                                                     |
| <p><strong>Domaine DGT</strong><br>(entreprises, agents, associations)</p>                                                              | _Positionnement EFP Connect vs ProConnect à clarifier en 2025_                                                                                  |
| **Particulier (citoyen)**                                                                                                               | <p>Nécessaire : Solution spécifique (email, lien magique)<br>Facultatif : FranceConnect OU FranceConnect+</p>                                   |
| <p><strong>Professionnel de Santé</strong><br>dans l'exercice de la médecine</p>                                                        | Pro Santé Connect (carte CPS / e-CPS)                                                                                                           |
| <p><strong>Santé et Médico-Social</strong><br>hors champ médical stricte</p>                                                            | Plage / Pasrel                                                                                                                                  |

## Solutions existantes

**Solution spécifique - SSO LDAP** repose sur des annuaires LDAP et un système d'authentification intégré à l'application : framework type Spring Security et/ou serveur IAM dédié Keycloak.\
\&#xNAN;_A noter que les annuaires LDAP ne sont pas accessibles depuis un cloud public._\
MFA : Oui avec Keycloak

**Solution spécifique - Sans SSO** repose sur une gestion locale des comptes utilisateurs sans. Cette solution ne DEVRAIT PAS être mise en œuvre, ou alors de manière provisoire pour un POC/MVP.\
MFA : Oui avec Keycloak

**Solution spécifique - Lien magique** : lorsque les utilisateurs se connectent seulement de manière occasionnelle (ex: mise à jour périodique de référentiels), envisager une solution sans mot de passe (ex: jeton d'accès à usage unique sous forme de lien magique envoyé par email).\
MFA : Non

[**FranceConnect**](https://franceconnect.gouv.fr/franceconnect) permet de déléguer l'authentification d'un Particulier à un Fournisseur d'Identité connu. Il convient cependant de réconcilier les identités à la première connexion (création ou rapprochement de compte dans l'application) et lors des connexions suivantes.\
MFA : Non

[**FranceConnect+**](https://franceconnect.gouv.fr/franceconnect-plus) est utilisé par le Fournisseur de Service dans le cas de démarches avec données particulièrement sensibles, données de santé et flux financiers. Dans ce cas un 2nd facteur d'authentification (App mobile France Identité) entre en jeu.\
MFA : Oui

[**ProConnect(et ProConnect Identité)**](https://www.proconnect.gouv.fr/) sert à identifier tout professionnel du public ou du privé. [Le fonctionnement est très différent suivant que l'utilisateur est connu ou pas de l'un des Fournisseurs d'Identité](iam.md#proconnect). A noter aussi que le Fournisseur de Service choisit sa surface d'exposition lors du raccordement à ProConnect : Internet (accès FS public via FI public), RIE (accès FS @RIE via FI @RIE), Hybride (accès FS public via FI @RIE).\
MFA : Oui

[**EFP Connect**](https://info.efpconnect.emploi.gouv.fr/) est le vecteur d'authentificaiton pour les démarches de la sphère Emploi (DGEFP), et progressivement de la sphère travail (DGT). EFP Connect centralise la gestion des rôles et habilitations pour les applications métier de son périmètre.\
MFA : Oui

[**Pro Santé Connect**](https://esante.gouv.fr/produits-services/pro-sante-connect) authentifie et identifie obligatoirement les Professionnels de Santé dans l'exercice de la médecine. Il repose sur les cartes professionnelles CPS et e-CPS, et le répertoire RPPS. Le raccordement d'un service est assez lourd.\
MFA : Oui

[**Pasrel (et portail Plage)**](https://connect-pasrel.atih.sante.fr/cas/login) sert à identifier les personnes de la sphère Santé et Médico-Social, dans le périmètre de l'ATIH. Il repose sur le répertoire FINESS des Etablissements de Santé et de leurs collaborateurs.\
MFA : Non

## ProConnect vs ProConnect Identité

_MonComptePro, InclusionConnect et AgentConnect ont fusionné pour devenir ProConnect._\
Le fonctionnement de ProConnect est différent suivant que l'utilisateur est connu ou pas d'un Fournisseur d'Identité de l'administration :

| Aspect                                     | ProConnect (avec FI)                                                                                                                                                                                                                                               | ProConnect Identité                                                                                                                                                        |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authentification                           | Authentification portée par un FI du public. Routage vers le bon FI basé sur le FQDN de l’email. [La table de correspondance est portée par ProConnect](https://grist.numerique.gouv.fr/o/docs/3kQ829mp7bTy/AgentConnect-Configuration-des-Fournisseurs-dIdentite) | Compte email à créer sur ProConnect. Pas d’authentification par FI pour les comptes ProConnect Identité. C’est ProConnect qui porte une authentification par mot de passe. |
| Traits d’identité et données individuelles | Fourni par le FI                                                                                                                                                                                                                                                   | Gestion libre sur le compte ProConnect                                                                                                                                     |
| Entité(s) de rattachement                  | Fournie(s) par le FI.                                                                                                                                                                                                                                              | Gestion libre des SIRET sur le compte ProConnect. Certification du dirigeant à venir (2025)                                                                                |
