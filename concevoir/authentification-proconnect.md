---
icon: lock
---

# ProConnect
[ProConnect](https://partenaires.proconnect.gouv.fr/) identifie et authentifie les **utilisateurs professionnels publics et privés**. Il résulte de la fusion des anciens services AgentConnect, MonComptePro et InclusionConnect.
Cette synthèse oriente les équipes produits ans se substituer à la [documentation officielle de ProConnect](https://partenaires.proconnect.gouv.fr/docs).

# ProConnect vs FranceConnect
ProConnect possède certaines caractéristiques de FranceConnect :
* Développé et opéré par la DINUM
* Standard OpenIdConnect
* ProConnect est un serveur d'authentification intermédiaire entre Fournisseurs de Service (FS) et Fournisseurs d'Identité (FI)
* Demande d'habilitation via [DataPass](https://datapass.api.gouv.fr/demandes/pro_connect_service_provider/nouveau)

ProConnect diffère de FranceConnect sur ces points notables :
* Pas de choix explicite du FI (routage par l'adresse email)
* Pas de redressement des traits d'identité au RNIPP
* Possibilité légale d'utiliser ProConnect comme moyen d'authentification unique
* Pas de notion de Fournisseurs de Données (FD)

## ProConnect vs ProConnect Identité

Le fonctionnement de ProConnect diffère si l'utilisateur est connu ou pas d'un FI de l'administration :

| Aspect                                     | ProConnect (avec FI)                                                                                                                                                                                                                                               | ProConnect Identité                                                                                                                                                        |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authentification                           | Authentification portée par un FI du public. Routage vers le bon FI basé sur le FQDN de l’email. [La table de correspondance est portée par ProConnect](https://grist.numerique.gouv.fr/o/docs/3kQ829mp7bTy/AgentConnect-Configuration-des-Fournisseurs-dIdentite) | Compte email à créer sur ProConnect. Pas d’authentification par FI pour les comptes ProConnect Identité. C’est ProConnect qui porte une authentification par mot de passe. |
| Traits d’identité et données individuelles | Fourni par le FI                                                                                                                                                                                                                                                   | Gestion libre sur le compte ProConnect                                                                                                                                     |
| Entités de rattachement                    | Fournies par le FI.                                                                                                                                                                                                                                                | Gestion libre des SIRET sur le compte ProConnect. Certification du dirigeant à venir (2025)                                                                                |
| [2FA](#2fa-proconnect)                     | Implémenté et déclenché par le FI                                                                                                                                                                                                                                  | A la main de l'utilisateur sur son compte ProConnect Identité                                                                                                              |
| Adresses email supportées                  | *.gouv.fr                                                                                                                                                                                                                                                          | *                                                                                                                                                                          |

## 2FA ProConnect
Le fonctionnement du 2FA ProConnect est décrit [ici](https://partenaires.proconnect.gouv.fr/docs/fournisseur-service/double_authentification)

Indépendamment des FI de chaque administration, ProConnect offre les mécanismes 2FA suivants :
- **Par défaut ProConnect envoie un code de vérification à 10 chiffres par email**. On peut alors parler de "1.5FA"
- Sur son [compte ProConnect Identité](https://identite.proconnect.gouv.fr/connection-and-account), un utilisateur peut
    - conserver le fonctionnement par défaut
    - configurer un 2FA (Authenticator, passkey) déclenché uniquement pour les FS qui l'exigent
    - déclencher ce 2FA systématiquement, pour tous les FS

Ainsi à la connexion :
- Si le FS exige un niveau "eidas1", le 2FA ProConnect ne sera pas déclenché (sauf vérification contextuelle ou périodique)
- Si le FS exige un niveau "eidas2" ou supérieur :
    - Si le FI de l'agent public offre un niveau eidas2 ou supérieur, ProConnect ne déclenche pas de 2FA supplémentaire car l'exigence est déjà satisfaite
    - Si l'utilisateur passe par ProConnect Identité, c'est la configuration de son compte qui s'applique

Si le 1.5FA par défaut de ProConnect n'est pas satisfaisant, c'est au FS d'implémenter son propre 2FA (Authenticator, carte à puce, etc.). Un 2FA spécifique par email ou SMS n'a que peu d'intérêt.

## Faut-il proposer un autre moyen d'authentification ?
Non, ProConnect suffit à authentifier tous les professionnels. Il est fortement déconseillé de proposer une authentification par email et mot de passe (moindre niveau global de sécurité, complexité des écrans et de l'application, pas de ROI, charge de support...).

## Faut-il un serveur Keycloak avec ProConnect ?
Non, un serveur d'authentification Keycloak est inutile dans la plupart des cas.
Cela dit il peut-être nécessaire si l'application métier est un progiciel dont le paramétrage ne permet pas de satisfaire aux spécifications de ProConnect.
