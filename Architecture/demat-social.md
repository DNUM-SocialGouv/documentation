# Démat Social

Démat Social sert à dématérialiser des démarches administratives de manière simple et homogène. Démat Social est un fork
de Démarches Simplifiées, et est déployé au MAS.
[Documentation complète de Démarches Simplifiées](https://doc.demarches-simplifiees.fr/)

## Recommandations fortes

- Utiliser Démarches Simplifiées et Démat Social plutôt que de développer une application front spécifique pour chaque
  besoin métier
- Utiliser Démarches Simplifiées plutôt que Démat Social si possible
- Si besoin ajouter un back-office derrière Démarches Simplifiées ou Démat Social pour le travail des agents

## Ecarts entre Démarches Simplifiées et Démat Social

|                                     | [Démarches Simplifiées](https://www.demarches-simplifiees.fr/) | [Démat Social](https://demat.social.gouv.fr/)                                              |
| ----------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Entité responsable                  | SPM/DINUM                                                      | MAS/DNUM                                                                                   |
| Hébergement HDS                     | Non                                                            | Oui                                                                                        |
| Connexion FranceConnect             | Oui                                                            | Non                                                                                        |
| Connexion ProConnect                | Oui                                                            | Non                                                                                        |
| Champs spécifiques                  | n/a                                                            | Champ NIR sécurisé</br>Champ FINESS (avec lookup FINESS)</br>Champ RPPS (avec lookup RPPS) |
| Montées de version                  | ~tous les jours                                                | 3-12 mois de retard                                                                        |
| Numérotation des versions           | AAAA-MM-DD-version                                             | x.y.z                                                                                      |
| Accès Administrateur et Instructeur | Internet                                                       | RIE seulement                                                                              |
