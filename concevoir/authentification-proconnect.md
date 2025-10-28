# 🔒 ProConnect

## ProConnect

[ProConnect](https://partenaires.proconnect.gouv.fr/) identifie et authentifie les **utilisateurs professionnels publics et privés**. Il résulte de la fusion des anciens services AgentConnect, MonComptePro et InclusionConnect. Cette synthèse oriente les équipes produits ans se substituer à la [documentation officielle de ProConnect](https://partenaires.proconnect.gouv.fr/docs).

## ProConnect vs FranceConnect

ProConnect possède certaines caractéristiques de FranceConnect :

* Développé et opéré par la DINUM
* Standard OpenIdConnect
* Serveur d'authentification intermédiaire entre Fournisseurs de Service (FS) et Fournisseurs d'Identité (FI)
* Demande d'habilitation via [DataPass](https://datapass.api.gouv.fr/demandes/pro_connect_service_provider/nouveau)

ProConnect diffère de FranceConnect sur ces points notables :

* Pas de choix explicite du FI (routage par l'adresse email)
* Pas de redressement des traits d'identité au RNIPP
* Possibilité légale d'utiliser ProConnect comme moyen d'authentification unique pour accéder à un service public numérique
* Pas de notion de Fournisseurs de Données (FD)

### ProConnect vs ProConnect Identité

Le fonctionnement de ProConnect diffère si l'utilisateur est connu ou pas d'un FI de l'administration :

| Aspect                                               | ProConnect (avec FI)                                                                                                                                                                                                                                               | ProConnect Identité                                                                                                                                                        |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authentification                                     | Authentification portée par un FI du public. Routage vers le bon FI basé sur le FQDN de l’email. [La table de correspondance est portée par ProConnect](https://grist.numerique.gouv.fr/o/docs/3kQ829mp7bTy/AgentConnect-Configuration-des-Fournisseurs-dIdentite) | Compte email à créer sur ProConnect. Pas d’authentification par FI pour les comptes ProConnect Identité. C’est ProConnect qui porte une authentification par mot de passe. |
| Traits d’identité et données individuelles           | Fourni par le FI                                                                                                                                                                                                                                                   | Gestion libre sur le compte ProConnect                                                                                                                                     |
| Entités de rattachement                              | Fournies par le FI                                                                                                                                                                                                                                                 | <p>Gestion libre des SIRET sur le compte ProConnect.<br>Certification possible du dirigeant via parcours dédié</p>                                                         |
| [2FA](authentification-proconnect.md#2fa-proconnect) | Implémenté et déclenché par le FI                                                                                                                                                                                                                                  | A la main de l'utilisateur sur son compte ProConnect Identité                                                                                                              |
| Adresses email supportées                            | \*.gouv.fr                                                                                                                                                                                                                                                         | \*                                                                                                                                                                         |

_Un paramétrage de ProConnect permet de restreindre l'accès à un FS aux seuls agents publics._

### 2FA ProConnect

Le fonctionnement du 2FA ProConnect est décrit [ici](https://partenaires.proconnect.gouv.fr/docs/fournisseur-service/double_authentification)

Indépendamment des FI de chaque administration, ProConnect offre les mécanismes 2FA suivants :

* **Par défaut ProConnect envoie un code de vérification à 10 chiffres par email**. On peut alors parler de "1.5FA".
* Sur son [compte ProConnect Identité](https://identite.proconnect.gouv.fr/connection-and-account), un utilisateur peut
  * conserver le fonctionnement par défaut
  * configurer un 2FA (Authenticator, passkey) déclenché uniquement pour les FS qui l'exigent
  * déclencher ce 2FA systématiquement, pour tous les FS

Ainsi à la connexion :

* **Si** le FS exige un niveau _eidas1_
  * **Alors** le 2FA ProConnect n'est pas déclenché (sauf vérification contextuelle ou périodique à l'initiative de ProConnect)
* **Si** le FS exige un niveau _eidas2_ ou supérieur
  * **Si** l'agent public se connecte avec le FI de son administration **Et** le FI offre déjà un niveau _eidas2_ ou supérieur
    * **Alors** ProConnect ne déclenche pas de 2FA supplémentaire
  * **Sinon Si** l'utilisateur public ou privé se connecte avec ProConnect Identité **Et** l'utilisateur a configuré le 2FA sur son compte
    * **Alors** c'est la configuration de son compte qui s'applique
  * **Sinon** ProConnect déclenche son 2FA par défaut

_Si le 2FA par défaut de ProConnect n'est pas satisfaisant d'un point de vue métier ("1.5FA"), c'est au FS d'implémenter son propre 2FA (Authenticator, carte à puce, etc.). Un 2FA par email ou SMS hors-ProConnect ne présente que peu d'intérêt._

### Faut-il un autre moyen d'authentification ?

**Non, ProConnect suffit à authentifier tous les professionnels**. Il est fortement déconseillé de proposer une authentification par email et mot de passe (moindre niveau global de sécurité, complexité des écrans et de l'application, pas de ROI, charge de support...).\
Exception : Pro Santé Connect surpasse ProConnect en termes d'obligation réglementaire et s'impose donc pour l'authentification des PS dans l'exercice de la médecine.\_

### Faut-il un serveur Keycloak avec ProConnect ?

**Non, un serveur d'authentification Keycloak est inutile dans la plupart des cas.**\
Exception : l'application métier est un progiciel dont le paramétrage ne permet pas de satisfaire aux spécifications de ProConnect.
