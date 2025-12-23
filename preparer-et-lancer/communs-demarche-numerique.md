# ♻️ Démarche Numérique et Démat Social

* [**Démarche Numérique**](https://demarche.numerique.gouv.fr/) (anc. Démarches Simplifiées) est un SaaS interministériel de dématérialisation des démarches administratives.
* [**Démat Social**](https://demat.social.gouv.fr/) est un fork de Démarche Numérique, instancié et déployé sur HDS par et pour les Ministères Sociaux.

## Ce que permet Démarche Numérique

### Pour le déposant

### Pour l'instructeur
* De faire intervenir ponctuellement des experts externes
* D'échanger par message avec le déposant

### Pour l'administrateur
* Délivrer une attestation PDF en fin de parcours
* De finement

### Pour le développeur d'application métier
* API GraphQL pour récupérer facilement les données nécessaires sur un ensemble de dossiers

## Ce que ne permet PAS Démarche Numérique
* Personnaliser le workflow de validation des dossiers. L'instruction dans Démarche Numérique reste volontairement assez simple pour ne pas encourager la sur-administration.
* Conserver des données au-delà de 12 mois. Démarche Numérique n'est pas fait pour gérer un référentiel d'information.
* Dupliquer une démarche précédente
* Pour un instructeur, de modifier le dépôt initial du déclarant
* API REST

## Bien choisir entre Démarche Numérique et Démat Social

{% hint style="info" %}
**Sauf contrainte HDS, il est préférable d'utiliser Démarche Numérique plutôt que Démat Social.**
{% endhint %}

|                                | [Démarche Numérique](https://demarche.numerique.gouv.fr/) | [Démat Social](https://demat.social.gouv.fr/)                                                      |
| ------------------------------ | --------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Entité porteuse                | SPM/DINUM                                                 | DNUM des Ministères Sociaux                                                                        |
| SecNumCloud                    | ✅                                                       | ❌                                                                                                 |
| HDS                            | ❌                                                       | ✅                                                                                                 |
| Connexion FranceConnect        | ✅                                                       | ❌                                                                                                 |
| Connexion ProConnect           | ✅                                                       | ❌ (en cours)                                                                                      |
| Champs spécifiques Min Sociaux | n/a                                                       | <p>Champ NIR sécurisé<br>2 champs FINESS (avec lookup FINESS)<br>Champ RPPS (avec lookup RPPS)</p> |
| Homologation RGS               | ✅                                                       | ✅                                                                                                 |
| Version en production          | 2025-12-23                                                | 2023-12-22 (24 mois de retard sur DN)                                                              |
| Accès Admin et Instructeur     | Internet et RIE                                           | RIE seulement                                                                                      |
| Hébergement                    | OVH                                                       | Cegedim                                                                                            |
| Exploitation                   | SPM/DINUM                                                 | Cegedim                                                                                            |
| Homologation RGS               | ✅                                                       | ✅                                                                                                |
| Open source                    | ✅                                                       | ❌                                                                                                |

## Sources de veille
* [Documentation complète Démarche Numérique](https://doc.demarches-simplifiees.fr/)
* [Nouveautés de Démarche Numérique](https://github.com/demarches-simplifiees/demarches-simplifiees.fr/releases)
* [Salon Tchap de Démarche Numérique](https://www.tchap.gouv.fr/#/room/#demarchessimplifieesS454OP0:agent.dinum.tchap.gouv.fr)