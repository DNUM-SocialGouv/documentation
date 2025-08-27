---
icon: table
---

# Grist
Version SaaS

# Différences entre la version SaaS et la version DINUM
La version SaaS n'a pas vocation. En revanche elle est utile pour certains tests et il est important de comprendre les différences entre la version commerciale et la version interministérielle :

|                              | [Version SaaS](https://www.getgrist.com) | [Version DINUM](https://grist.numerique.gouv.fr/) |
| ---------------------------- | ---------------------------------------- | ------------------------------------------------- |
| Niveau de licence            | Premium                                  | Open-Source                                       |
| Entité responsable           | getgrist.com                             | SPN/DINUM                                         |
| Hébergement                  | getgrist.com                             | OVH@SecNumCloud                                   |
| Authentification             | Non                                      | ProConnect et ProConnect Identité                 |
| Envoi d'invitation par email | Oui                                      | Non                                               |
| Webhooks - urls autorisées   | *                                        | *.gouv.fr                                         |

## Gestion des droits
- Gestion avancée des droits : [webinaire DINUM 2024](https://tube.numerique.gouv.fr/w/3u3QfzMv66euFsa4zQDMhm)
- [Backlog officiel Grist](https://github.com/orgs/gristlabs/projects/4/views/1)

## Exploitation
-	Donnée obligatoire (1 seul champ obligatoire par table lors de la création car tentative d’enregistrement immédiate) :  
-	Initialiser avec le Réseau avec celui de l’utilisateur connecté :
-	Reseaux.lookupOne(Nom=Users.lookupOne(Email=user.Email).Reseau.Nom)

## API
- webhooks (envoi vers service externe) déclenchés sur opérations C+U+D ou explicitement sur un bouton d'action

## Notes
- Forcer un retour à la ligne à l'intérieur d'une cellule se fait avec SHIFT+ENTRER
- "?embed=true" a la fin d'une URL donne une vue simplifiée juste avec le contenu Grist