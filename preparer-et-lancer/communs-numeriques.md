---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Communs numériques

Tout projet DOIT tenter de réutiliser des communs numériques, en suivant l'arbre de décision ci-dessous, avant d'engager des développements spécifiques.

## Arbre de décision suivant la nature du projet

* **Site éditorial**
  * Soit socle [ONDINE ](../concevoir/accessibilite/developpement.md)du MAS (Drupal)
  * Soit [Sites faciles](https://sites-faciles.beta.numerique.gouv.fr/)
* **Démarche administrative en ligne**
  * **Front usager** : utiliser Démarches Simplifiées ou Démat Social autant que possible, plutôt que de développer une application front spécifique pour chaque besoin métier
    * Utiliser Démarches Simplifiées plutôt que Démat Social si possible. Voir les [différences entre Démarches Simplifiées et Démat Social](communs-numeriques.md#écarts-entre-démarches-simplifiées-et-démat-social).
  * **Back-office agent** : si Démarches Simplifiées (ou Démat Social) ne put pas couvrir les besoins des agents, envisager en sus un back-office de traitement
    * Privilégier GLPI comme back-office de traitement
    * Si malgré la recherche de compromis, GLPI présente toujours trop de limites :
      * envisager le développement spécifique autour de GLPI (API et webhook)
      * envisager d'enrichir GLPI ou demander son adaptation
      * envisager le développement spécifique complet du back-office
* **Projet Référentiel**
  * Soit GLPI pour les besoins simples (gestion de parc, inventaire) sans contrôle précis sur la modélisation des données en base
  * Soit développement spécifique

## Nos communs numériques

* [**Démarches Simplifiées**](https://doc.demarches-simplifiees.fr/) est une solution de dématérialisation des démarches administratives. Elle est inter-ministérielle, générique et hébergée en mode SaaS.
* [**Démat Social**](https://demat.social.gouv.fr/) est un fork de Démarches Simplifiées, déployé au MAS.
* [**GLPI**](https://glpi-project.org/fr/) est une solution open source générique de gestion de parc matériel et de gestion de demandes et incidents

## Nos futures briques communes

_En cours_

* Authentification agent / métier (interne + ProConnect)
* Authentification publique (interne + FranceConnect)
* Statistiques (production de fichiers Excel, BI)
* Notifications (envois emails)
* GED (S3, …)
* Publipostage (gestion des templates avec balises + production de documents)
* API Base d'Adresse Nationale (BAN)
* API Entreprise
* API Associations
* API Piste (CaptchEtat, Chorus)
* Workflow
* Tableaux de bord
* Chatbot...

## Écarts entre Démarches Simplifiées et Démat Social

|                                     | [Démarches Simplifiées](https://www.demarches-simplifiees.fr/) | [Démat Social](https://demat.social.gouv.fr/)                                                      |
| ----------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Entité responsable                  | SPM/DINUM                                                      | MAS/DNUM                                                                                           |
| Hébergement                         | SecNumCloud@OVH                                                | HDS@Cegedim                                                                                        |
| Connexion FranceConnect             | Oui                                                            | Non                                                                                                |
| Connexion ProConnect                | Oui                                                            | Non                                                                                                |
| Champs spécifiques                  | n/a                                                            | <p>Champ NIR sécurisé<br>2 champs FINESS (avec lookup FINESS)<br>Champ RPPS (avec lookup RPPS)</p> |
| Montées de version                  | \~tous les jours                                               | 3-12 mois de retard                                                                                |
| Numérotation des versions           | AAAA-MM-DD-version                                             | x.y.z                                                                                              |
| Accès Administrateur et Instructeur | Internet                                                       | RIE seulement                                                                                      |

## Limites de GLPI

_En cours_

* Volumétrie / Performance
* Complexité des workflow
* Accessibilité
* Disponibilité sur les hébergements
