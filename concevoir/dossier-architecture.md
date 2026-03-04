# 📄 Dossier d'Architecture

Cette page présente les bonnes pratiques essentielles autour du Dossier d'Architecture (DA) des produits DNUM/SDPC, pour :
* Collaborer efficacement avec l'ensemble des acteurs concernés par le DA
* Rédiger un DA conforme aux exigences de la DNUM
* Faciliter la validation en Comité d'Architecture (COAT) en limitant les itérations

## Acteurs concernés

De nombreux acteurs interviennent tout au long du cycle de vie d'un DA :
* Le **responsable du DA** au sein de l’équipe produit. Il s'agit d'un responsable produit, architecte technique ou responsable technique, interne DNUM ou externe.
* Les **membres du COAT** pour valider les nouveaux DA et les changements majeurs en production (composants, flux)
* Les **architectes SDPC (DNUM/SDPC/ST)** valide chaque DA SDPC avant passage en COAT. Elle peut faciliter les échanges avec d’autres parties prenantes (hébergeur, ConfNum, partenaires...).
    * Lors d'un accompagnement soutenu, elle peut co-rédiger le DA avec l'équipe produit, qui porte toujours la responsabilité du DA.
    * Elle peut aussi rédiger et porter la responsabilité du DA pour les produits réalisés en interne.
* Les **architectes SDCID (DNUM/SDCID/MA)** en relecture afin d'anticiper les remarques du COAT
* Toute personne (nouvel arrivant, auditeur...) souhaitant s'informer sur un produit peut, après avoir obtenu les droits, consulter et apporter des commentaires au DA.

## Pré-requis
Avant toute contribution au DA, l’équipe produit prend connaissance :
* du [**Pack DA**](https://msociauxfr.sharepoint.com/sites/DNUM_DA) qui inclut un modèle de DA, des modèles de schémas, des nomenclatures et des exemples de DA rédigés.
* des [**règles de gouvernance du DA**](https://msociauxfr.sharepoint.com/sites/DNUM_DA)
* d'exemples de **DA existants** représentatifs de son domaine métier, son hébergement et ses technologies
* des **bonnes pratiques** ci-dessous

## Pour une collaboration efficace
* 📄**Nommage et versioning du DA** :
    * Respecter le nommage des fichiers définit dans le Pack DA
        * Ex : "DA - NomProjet - v1.0.3.docx".
    * Le DA et les schémas sources suivent le même numéro de version, même s'il n'y a pas de modification des schémas.
        * Ex : "DA - NomProjet - v1.0.3.docx" et "DA - NomProjet - v1.0.3.pptx"
    * Commencer le versioning à 1.0.0
    * Le DA et les schémas ont le même nom de fichier. Seule l'extension diffère : .docx pour le DA, .pptx ou .drawio pour les schémas
* 📂 **Partage de DA** :
    * Le DA de référence et les schémas sources sont et restent dans le répertoire partagé du produit. Si l'équipe produit n'a pas encore mis en place un répertoire produit, les architectes SDPC peuvent fournir un répertoire provisoire.
    * Le DA est partagé via des liens SharePoint, et non par email (sécurité, risque important de versions divergentes...)
    * L'équipe produit donne les droits d'accès en écriture sur le répertoire du DA, afin de pouvoir commenter ou co-rediger le document.
* 👨‍💼Un architecte SDPC, après validation du DA, dépose une copie dans le répertoire de la MA (SDCID). Les schémas ne sont pas nécessaires pour que la MA commente le DA.
    * TODO à clarifier : comment le DA devrait être partagé au COAT, aujourd'hui par email

## Points d'auto-contrôle pour maximiser les chances de validation en COAT
Rappel de quelques règles fréquemment enfreintes, qui engendrent des allers-retours, validation avec réserve, rejet, repassage en COAT :
* **Remplir les éléments de contexte** Remplissage exemplaire du DICT** : clair (ex : "L'appli 2 est la refonte de l'appli 1) et argumenté.
* **Remplissage exemplaire du DICT** : clair (ex : T2 incompatible avec C4) et argumenté.
* **Matrice des flux** : bien remplir la description de chaque flux. Clarifier l'objectif du flux, les mécanismes et protocoles d'authentification et de chiffrement par exemple.
* **Conformité au modèle de DA** : baser tout nouveau DA sur le modèle du Pack DA, ou à défaut intégrer les nouveautés jusqu'au modèle de DA le plus récent, y compris pour les modèles de schémas. Il n'est pas nécessaire d'intégrer les nouveautés du pack DA à chaque version du DA, mais une mise à jour opportuniste (cherry picking) est recommandée.
* Assurer la **cohérence des noms** de populations d'utilisateurs et composants dans toutes les rubriques du DA.
* **Suivi des changements** : bien mettre à jour l’encart de suivi des changements. Ne pas hésiter à utiliser ce log pour tracer les décisions (ADR)