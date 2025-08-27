---
icon: table
---

# Grist
Version SaaS

# Différences entre la version SaaS et la version DINUM
La version SaaS n'a pas vocation. En revanche elle est utile pour certains tests et il est important de comprendre les différences entre la version commerciale et la version interministérielle :

|                              | [Version SaaS](https://www.getgrist.com) | [Version DINUM](https://grist.numerique.gouv.fr/) |
| ---------------------------- | ---------------------------------------- | ------------------------------------------------- |
| Niveau de licence            | Basic ou Premium (payant)                | Open-Source (gratuit)                             |
| Entité responsable           | getgrist.com                             | SPN/DINUM                                         |
| Hébergement                  | getgrist.com                             | SecNumCloud@OVH                                   |
| Authentification             | Non                                      | ProConnect et ProConnect Identité                 |
| Envoi d'invitation par email | Oui                                      | Non                                               |
| Webhooks - urls autorisées   | *                                        | *.gouv.fr                                         |

## Ressources
- [Gestion avancée des droits](https://tube.numerique.gouv.fr/w/3u3QfzMv66euFsa4zQDMhm)
- [Doc API](https://support.getgrist.com/fr/api/)
- [Backlog officiel Grist](https://github.com/orgs/gristlabs/projects/4/views/1)

## API
- webhooks (envoi vers service externe) déclenchés sur opérations C+U+D ou explicitement sur un bouton d'action

## Notes
- L'instance DINUM grist.numerique.gouv.fr n'envoie pas d'invitation aux nouveaux utilisateurs. Il faut copier le lien et l'envoyer par un autre canal.
- Forcer un retour à la ligne à l'intérieur d'une cellule se fait avec SHIFT+ENTRER
- "?embed=true" a la fin d'une URL donne une vue simplifiée juste avec le contenu Grist
- illustration de lookupOne pour initialiser un champ de type Référence. Ici le réseau de l'utilisateur connecté : Reseaux.lookupOne(Nom="Users.lookupOne(Email=user.Email).Reseau.Nom)
- Penser à systématiquement mettre un message explicatif pour chaque permission avancée. Ce message est affiché à l'utilisateur en cas d'erreur.
- Donnée obligatoire (1 seul champ obligatoire par table lors de la création car tentative d’enregistrement immédiate)

## Sélection de plugins
- Ajouter un entête type DSFR : https://agrippaharfleur.github.io/grist-custom-widgets/dsfr-en-tete/