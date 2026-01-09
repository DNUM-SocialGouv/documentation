# ♻️ Grist

[Grist](https://grist.numerique.gouv.fr/) est le tableur collaboratif et souverain de l'Etat pour centraliser, analyser et partager nos données.

## Différences entre instances SaaS et DINUM

L'offre SaaS n'a pas vocation à être utilisée en production. En revanche il est important de comprendre les différences entre les instances SaaS et DINUM :

|                              | [Offre SaaS](https://www.getgrist.com)   | [Instance DINUM](https://grist.numerique.gouv.fr/) |
| ---------------------------- | ---------------------------------------- | -------------------------------------------------- |
| Niveau de licence            | Basic (gratuit) ou Premium (payant)      | Open-Source (gratuit)                              |
| Entité responsable           | getgrist.com                             | SPN/DINUM/OPI                                      |
| Hébergement                  | getgrist.com                             | SecNumCloud@Outscale                               |
| ProConnect                   | ❌                                      | ✅                                                 |
| Envoi d'invitation par email | ✅                                      | ❌ (partager le lien aux utilisateurs)             |
| Webhooks - urls autorisées   | \*                                       | \*.gouv.fr                                         |
| Homologation RGS             | ❌                                      | ✅                                                 |

## Ressources
* [Webinaire d'introduction](https://tube.numerique.gouv.fr/w/hMJ8DMj1beqv1D12vpgBKq)
* [Webinaire pour comprendre les permissions avancées](https://tube.numerique.gouv.fr/w/3u3QfzMv66euFsa4zQDMhm)
* [Info techniques sur l'hébergement Grist DINUM](https://docs.numerique.gouv.fr/docs/3537d3d6-e8c2-43fb-b530-73b3361083c1/)

## API
* [Doc API](https://support.getgrist.com/fr/api/)
* webhooks (envoi vers service externe) déclenchés sur opérations C+U+D ou explicitement par un bouton d'action

## Notes

* SHIFT+ENTRER pour forcer un retour à la ligne à l'intérieur d'une cellule
* "?embed=true" a la fin d'une URL donne une vue simplifiée juste avec le contenu Grist
* illustration de lookupOne pour initialiser un champ de type Référence. Ici le réseau de l'utilisateur connecté : Users.lookupOne(Email=user.Email).Reseau
* Renseigner systématiquement un message explicatif pour chaque permission avancée. Ce message est affiché à l'utilisateur en cas d'erreur.
* Donnée obligatoire (1 seul champ obligatoire par table lors de la création car tentative d’enregistrement immédiate)
* Grist comme Backend-as-a-service : pour cas très simples seulement car
  * pas possible de propager l'authentification ProConnect au backend Grist
  * pas possible de récupérer les permissions par API
* Grist DINUM supporte au moins 100 000 lignes dans une même table (REX)

## Sélection de plugins

Si la source n'est pas officielle, il est préférable de copier-coller le contenu d'un plugin dans un "Custom Widget Plugin" plutôt que de référencer le code externe.

* Ajouter un entête DSFR à une page Grist : https://github.com/agrippaharfleur/grist-custom-widgets/tree/main/dsfr-en-tete
* Plugin gouv de publipostage PDF: https://github.com/betagouv/grist-custom-widgets-fr-admin/tree/main/app/omFiller
* Plugin gouv pour Kanban : https://github.com/gristgouv/grist-widget-varamil/tree/main/kanban
* Initiative de référencement des plugins Grist : https://docs.getgrist.com/9DZa7JFegUxz/GristHub/p/1

## Sources de veille
* [Newsletter Grist FR](https://support.getgrist.com/fr/newsletters/)
* [Forum de la communauté Grist FR](https://forum.grist.libre.sh/)
* [Backlog officiel Grist](https://github.com/orgs/gristlabs/projects/4/views/1). Suivre cette évolution qui permettra peut-être de rendre un widget public : https://github.com/gristlabs/grist-core/issues/348.
* [Salon Tchap "Grist - Annonces"](https://www.tchap.gouv.fr/#/room/!yYdrqZlxydxriafaRE:agent.dinum.tchap.gouv.fr)
* [Salon Tchap "Grist - Utilisateurs"](https://www.tchap.gouv.fr/#/room/!TLRWBCVNfbjgrNKmox:agent.dinum.tchap.gouv.fr)
* [Salon Tchap "Grist - Contributions"](https://www.tchap.gouv.fr/#/room/!kkwhrcxoMcnAGMXMIM:agent.dinum.tchap.gouv.fr)