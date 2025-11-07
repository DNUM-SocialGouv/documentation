---
description: >-
  Présentation des solutions d'authentification pour les différentes populations
  d'utilisateurs.
---

# 🔒 Authentification des utilisateurs

## Solutions par population d'utilisateurs

| Population cible                                                                                                                        | Solution(s) préconisée(s)                                                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Agent du MAS</strong><br><strong>Agent d'autres Ministères</strong><br><strong>Service déconcentré (hors DDETS)</strong></p> | <p>Si disponibilité EBIOS 1 à 3 : [ProConnect](authentification-proconnect.md) seul<br>Si disponibilité EBIOS 4 : Solution spécifique (nécessaire) ET [ProConnect](authentification-proconnect.md) (facultatif)</p> |
| <p><strong>Service déconcentré DDETS</strong><br>@departement.gouv.fr</p>                                                               | <p>[ProConnect Identité](authentification-proconnect.md)<br><em>(en attendant un FI ProConnect du MIOM)</em></p>                                                                                                    |
| <p><strong>Collectivité territoriale</strong><br>(région, département, commune)</p>                                                     | <p>[ProConnect Identité](authentification-proconnect.md)<br><em>(pas de FI ProConnect identifié à date)</em></p>                                                                                                    |
| **Entreprise du secteur privé**                                                                                                         | [ProConnect Identité](authentification-proconnect.md)                                                                                                                                                               |
| **Association avec/sans SIRET**                                                                                                         | [ProConnect Identité](authentification-proconnect.md)                                                                                                                                                               |
| <p><strong>Domaine DGEFP</strong><br>(entreprises, agents, associations)</p>                                                            | EFP Connect                                                                                                                                                                                                         |
| <p><strong>Domaine DGT</strong><br>(entreprises, agents, associations)</p>                                                              | _Positionnement EFP Connect vs ProConnect à clarifier en 2026_                                                                                                                                                      |
| **Particulier (citoyen)**                                                                                                               | <p>Obligatoire : Solution spécifique (email, lien magique)<br>Facultatif : FranceConnect OU FranceConnect+</p>                                                                                                      |
| <p><strong>Professionnel de Santé</strong><br>dans l'exercice de la médecine</p>                                                        | Pro Santé Connect (carte CPS / e-CPS)                                                                                                                                                                               |
| <p><strong>Santé et Médico-Social</strong><br>hors champ médical stricte</p>                                                            | [Plage / Pasrel](authentification-plage-pasrel.md)                                                                                                                                                                  |

_Ces solutions ne sont pas toujours exclusives : le tableau peut être reparcouru pour chaque population d'utilisateurs._

## Solutions existantes

**Solution spécifique - SSO LDAP** repose sur des annuaires LDAP et un système d'authentification intégré à l'application : framework type Spring Security et/ou serveur IAM dédié Keycloak.\
\&#xNAN;_A noter que les annuaires LDAP ne sont pas accessibles depuis un cloud public._\
2FA : Oui avec Keycloak

**Solution spécifique - Sans SSO** repose sur une gestion locale des comptes utilisateurs sans. Cette solution ne DEVRAIT PAS être mise en œuvre, ou alors de manière provisoire pour un POC/MVP.\
2FA : Possible

**Solution spécifique - Lien magique** : lorsque les utilisateurs se connectent seulement de manière occasionnelle (ex: mise à jour périodique de référentiels), envisager une solution sans mot de passe (ex: jeton d'accès à usage unique sous forme de lien magique envoyé par email).\
2FA : Non

[**FranceConnect**](https://franceconnect.gouv.fr/franceconnect) permet de déléguer l'authentification d'un Particulier à un Fournisseur d'Identité connu. Il convient cependant de réconcilier les identités à la première connexion (création ou rapprochement de compte dans l'application) et lors des connexions suivantes.\
2FA : Non

[**FranceConnect+**](https://franceconnect.gouv.fr/franceconnect-plus) est utilisé par le Fournisseur de Service dans le cas de démarches avec données particulièrement sensibles, données de santé et flux financiers. Dans ce cas un 2FA est porté par l'application mobile [France Identité](https://france-identite.gouv.fr/) ou celle de La Poste.\
2FA : Oui

[**EFP Connect**](https://info.efpconnect.emploi.gouv.fr/) est le vecteur d'authentificaiton pour les démarches de la sphère Emploi (DGEFP), et progressivement de la sphère travail (DGT). EFP Connect centralise la gestion des rôles et habilitations pour les applications métier de son périmètre.\
2FA : Oui

[**Pro Santé Connect**](https://esante.gouv.fr/produits-services/pro-sante-connect) authentifie et identifie obligatoirement les Professionnels de Santé dans l'exercice de la médecine. Il repose sur les cartes professionnelles CPS et e-CPS, et le répertoire RPPS. Le raccordement d'un service est assez lourd.\
Service obligatoire pour les professionnels de santé dans l'exercice de la médecine.\
2FA : Oui