# 🔒 Authentification des utilisateurs

Présentation des solutions d'authentification pour les différentes populations d'utilisateurs.

## Solutions par population d'utilisateurs

| Population cible                                                                                                                                        | Solution(s) préconisée(s)                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Agent des Ministères Sociaux</strong><br><strong>Agent d'autres Ministères</strong><br><strong>Service déconcentré (hors DDETS)</strong></p> | <p><a href="authentification-proconnect.md">ProConnect</a><br><em>(FI ProConnect des Ministères Sociaux)</em></p>           |
| <p><strong>Service déconcentré DDETS</strong><br>@departement.gouv.fr</p>                                                                               | <p><a href="authentification-proconnect.md">ProConnect Identité</a><br><em>(en attendant un FI ProConnect du MIOM)</em></p> |
| <p><strong>Collectivité territoriale</strong><br>(région, département, commune)</p>                                                                     | <p><a href="authentification-proconnect.md">ProConnect Identité</a><br><em>(pas de FI ProConnect identifié à date)</em></p> |
| **Entreprise du secteur privé**                                                                                                                         | [ProConnect Identité](authentification-proconnect.md)                                                                       |
| **Association loi 1901/1908 avec/sans SIRET**                                                                                                           | [ProConnect Identité](authentification-proconnect.md)                                                                       |
| <p><strong>Domaine DGEFP</strong><br>(entreprises, agents, associations)</p>                                                                            | EFP Connect                                                                                                                 |
| <p><strong>Domaine DGT</strong><br>(entreprises, agents, associations)</p>                                                                              | [ProConnect](authentification-proconnect.md)                                                                                |
| **Particulier**                                                                                                                                         | <p>Obligatoire : Solution spécifique (email, lien magique)<br>Facultatif : FranceConnect OU FranceConnect+</p>              |
| **Professionnel de Santé**                                                                                                                              | [Pro Santé Connect](authentification-pro-sante-connect.md) (carte CPS / e-CPS)                                              |
| <p><strong>Domaine ATIH</strong></p>                                                                                                                    | [Plage / Pasrel](authentification-plage-pasrel.md)                                                                          |

_Ces solutions ne sont pas nécessairement exclusives, une application pouvant parfois cumuler les méthodes d'authentification._

## Solutions existantes

**Solution spécifique - SSO LDAP** repose sur des annuaires LDAP et une authentification intégrée à l'application : framework type Spring Security et/ou serveur IAM dédié Keycloak.\
A noter que les annuaires LDAP ne sont pas accessibles depuis un cloud public._\
2FA : Oui avec Keycloak

**Solution spécifique - Sans SSO** repose sur une gestion locale (mot de passe en base de données) des comptes utilisateurs. Cette solution legacy ne DOIT PAS être mise en œuvre pour les professionnels.\
2FA : Possible

**Solution spécifique - Lien magique** : lorsque les utilisateurs se connectent seulement de manière occasionnelle (ex: mise à jour périodique de référentiels), envisager une solution sans mot de passe (ex: jeton d'accès à usage unique sous forme de lien magique envoyé par email).\
2FA : Non

[**FranceConnect**](https://franceconnect.gouv.fr/franceconnect) permet de déléguer l'authentification d'un Particulier à un Fournisseur d'Identité connu. Il convient cependant de réconcilier les identités à la première connexion (création ou rapprochement de compte dans l'application) et lors des connexions suivantes.\
2FA : Non

[**FranceConnect+**](https://franceconnect.gouv.fr/franceconnect-plus) est utilisé par le Fournisseur de Service dans le cas de démarches avec données particulièrement sensibles, données de santé et flux financiers. Dans ce cas un 2FA est porté par l'application mobile [France Identité](https://france-identite.gouv.fr/) ou celle de La Poste.\
2FA : Oui

[**EFP Connect**](https://info.efpconnect.emploi.gouv.fr/) est la solution d'authentification pour les démarches de la sphère Emploi (DGEFP). Il est également utilisé par opportunité par quelques applications de la sphère travail (DGT) sans être la cible de ce domaine. EFP Connect centralise la gestion des rôles et habilitations pour les applications métier de son périmètre.\
2FA : Oui

[**Pro Santé Connect**](https://esante.gouv.fr/produits-services/pro-sante-connect) authentifie et identifie obligatoirement les Professionnels de Santé. Il repose sur les cartes professionnelles CPS et e-CPS, et le répertoire RPPS. Le raccordement d'un service est assez lourd.\
2FA : Oui

## Sources de veille

* [Salon Tchap "FranceConnect - Communications partenaires"](https://www.tchap.gouv.fr/#/room/#franceconnect:agent.dinum.tchap.gouv.fr)
* [FranceConnect - Documentation officielle](https://docs.partenaires.franceconnect.gouv.fr/fs/)
