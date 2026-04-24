# 🔒 ProConnect

[ProConnect](https://partenaires.proconnect.gouv.fr/) identifie et authentifie les **utilisateurs professionnels publics et privés**. Il résulte de la fusion des anciens services AgentConnect, MonComptePro et InclusionConnect.\
Cette synthèse vise à orienter les équipes produits, sans se substituer à la [documentation officielle de ProConnect](https://partenaires.proconnect.gouv.fr/docs).

## Avantages de ProConnect
* **Sécurité renforcée**
  * Plus de mots de passe en base
  * MFA natif et aligné sur les standards étatiques
  * Solution standard => moins de code spécifique => moins de failles
  * Moindre obsolescence
  * Révocation centralisée des accès en cas de départ de l’entité
  * SLO ProConnect (Single Log-Out)
* **Gains d’UX**
  * SSO ProConnect
  * Connexion silencieuse par défaut (pas besoin de cliquer sur le « bouton ProConnect »)
  * Environnement visuel normalisé
* **Economie sur l'hébergement**
  * ProConnect c’est souvent l’occasion de décommissionner des VMs Keycloak (ex : 2 instances x 3 env = 6 VM)
* **Economie sur l'exploitation**
  * Support utilisateur niveau 1 reporté en partie sur ProConnect (https://proconnect.crisp.help/fr/)
  * Gestion des accès partiellement automatisable
* **Et toutes les fonctionnalités futures de ProConnect, qu'on n'aura pas à implémenter sur chaque application !**

## ProConnect vs FranceConnect

ProConnect possède certaines caractéristiques de FranceConnect :

* Développé et opéré par la DINUM
* Standard OpenIdConnect
* Serveur d'authentification intermédiaire entre Fournisseurs de Service (FS) et Fournisseurs d'Identité (FI)
* Demande d'habilitation via [DataPass](https://datapass.api.gouv.fr/demandes/pro_connect_service_provider/nouveau)

ProConnect diffère de FranceConnect sur ces points notables :

* Pas de choix explicite du FI (routage implicite sur l'adresse email)
* Pas de redressement des traits d'identité au RNIPP
* Possibilité légale d'utiliser ProConnect comme moyen d'authentification unique pour accéder à un service public numérique
* Pas de notion de Fournisseurs de Données (FD)
* Dans certains cas, ProConnect s'appuie sur FranceConnect pour la certification d'identité

## ProConnect vs ProConnect Identité

Le fonctionnement de ProConnect diffère si l'utilisateur est connu ou pas d'un FI de l'administration :

|                                                      | ProConnect (avec FI)                                                                                                                                                                                                                                                         | ProConnect Identité                                                                                                                                                        |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authentification                                     | Authentification portée par un FI du public. Routage vers le bon FI basé sur le nom de domaine de l’email. [La table de correspondance est portée par ProConnect](https://grist.numerique.gouv.fr/o/docs/3kQ829mp7bTy/AgentConnect-Configuration-des-Fournisseurs-dIdentite) | Compte email à créer sur ProConnect. Pas d’authentification par FI pour les comptes ProConnect Identité. C’est ProConnect qui porte une authentification par mot de passe. |
| Traits d’identité et données individuelles           | Fourni par le FI                                                                                                                                                                                                                                                             | Déclaratif (ou définie périodiquement via une connexion à FranceConnect pour les noms de domaines gratuits)                                                                |
| Entités de rattachement                              | Fournies par le FI                                                                                                                                                                                                                                                           | <p>Gestion libre des SIRET sur le compte ProConnect.<br>Certification possible du dirigeant via parcours dédié</p>                                                         |
| [2FA](authentification-proconnect.md#2fa-proconnect) | Implémenté et déclenché par le FI                                                                                                                                                                                                                                            | A la main de l'utilisateur sur son compte ProConnect Identité                                                                                                              |
| Adresses email supportées                            | \*.gouv.fr                                                                                                                                                                                                                                                                   | \*                                                                                                                                                                         |

_Un paramétrage de ProConnect permet de restreindre l'accès à un FS aux seuls agents publics._

## 2FA ProConnect

Le fonctionnement du 2FA ProConnect du point de vue du FS est décrit [ici](https://partenaires.proconnect.gouv.fr/docs/fournisseur-service/double_authentification)

Chaque FS demande un niveau de sécurité :
* **eidas1** : pas d'exigence 2FA, tout FI possible.
* **eidas2** : le FI doit fournir un 2FA afin que la connexion soit acceptée. Sinon ProConnect affiche une erreur.

Le mécanisme 2FA déclenché dépend donc de chaque FI :
* **Notre FI Ministères Sociaux** :
  * Un code de vérification est systématiquement envoyé par email (1.5FA)
* **ProConnect Identité**
  * Par défaut, ProConnect Identité envoie un code de vérification par email (1.5FA).
  * Sur son [compte ProConnect Identité](https://identite.proconnect.gouv.fr/connection-and-account), chaque utilisateur peut
    * soit ne rien faire et conserver le fonctionnement par défaut (1.5FA)
    * soit configurer un 2FA (Authenticator, passkey). Ce 2FA est au choix déclenché pour les FS qui l'exigent, ou systématiquement pour tous les FS
* **FI MEN** : _A faire. Multiples IDP._
* **FI MIOM** : _A faire_

## FAQ
* **Faut-il un autre moyen d'authentification ?**
Non, ProConnect suffit à authentifier la plupart des professionnels. Il est fortement déconseillé de proposer une authentification par email et mot de passe, sauf exceptions :\
  * Entreprise ou association sans SIRET
  * Pro Santé Connect surpasse ProConnect en termes d'obligation réglementaire et s'impose donc pour l'authentification des Professionnels de Santé.\_

* **Faut-il un serveur Keycloak avec ProConnect ?**
Non, un serveur d'authentification intermédiaire est inutile et contre-productif dans la plupart des cas.\
Exception : le produit est un progiciel dont le paramétrage ne permet pas de satisfaire aux spécifications de ProConnect.

## Sources de veille
* [Salon Tchap "ProConnect - Support et retex"](https://www.tchap.gouv.fr/#/room/!kBghcRpyMNThkFQjdW:agent.dinum.tchap.gouv.fr)
* [Releases ProConnect (core)](https://github.com/proconnect-gouv/federation/releases)
* [Releases ProConnect Identité](https://github.com/proconnect-gouv/proconnect-identite/releases)
* [Feuille de route](https://www.proconnect.gouv.fr/feuille-de-route)
* [Canal Mattermost BetaGouv (privé)](https://mattermost.incubateur.net/betagouv/channels/startup--proconnect)