---
hidden : true
---

# 📄 Dossier d'Architecture

Cette page présente les bonnes pratiques essentielles autour du Dossier d'Architecture (DA), pour :
* Faciliter la collaboration avec l'ensemble des acteurs concernés par le DA
* Rédiger un DA conforme aux exigences de la DNUM
* Faciliter la validation en Comité d'Architecture (COAT) en réduisant les itérations

## Acteurs concernés

De nombreux acteurs interviennent tout au long du cycle de vie d'un DA :
* Le **responsable du DA** au sein de l’équipe produit. Il peut s'agir d'un responsable produit, d'un architecte technique, d'un Tech Lead, interne DNUM ou externe.
* L'**équipe d'accompagnement technique** qui doit valider chaque DA l'ensemble des DA prend en charge certains DA et qui valident l'ensemble des DA des produits
* La **Mission Architecture (MA)** en relecture afin d'anticiper les remarques du COAT
* Les **COAT** pour valider les nouveaux DA et les changements majeurs en production (composants, flux)

_Elle apporte un rôle de conseil, de revue et peut faciliter les échanges avec d’autres parties prenantes (hébergeur, confnum, DO, etc.).
Dans certains cas, elle peut co-rédiger le DA. La responsabilité du document reste toujours portée par l’équipe produit, même lorsque l’équipe d’accompagnement technique contribue à sa rédaction._

* Toute personne (nouvel arrivant, auditeur...) souhaitant s'informer sur le projet peut, après avoir obtenu les droits, consulter et apporter des commentaires au DA sur le répertoire partagé du projet 

## Pré-requis
Avant toute contribution à un DA, l’équipe produit concernée doit prendre connaissance :
* du [**Pack DA**](https://msociauxfr.sharepoint.com/sites/DNUM_DA) qui inclut un modèle de DA, des modèles de schémas, des nomenclatures et des exemples de DA rédigés.
* des [**règles de gouvernance du DA**](https://msociauxfr.sharepoint.com/sites/DNUM_DA)
* de **DA existants** représentatifs de son domaine métier, son hébergement et ses technologies

## Pour une collaboration efficace
1. Par défaut, l’équipe d’accompagnement technique intervient pour revue, conseil ou clarification des points incertains du DA. 
* Si nécessaire, l’équipe d’accompagnement technique peut identifier le bon interlocuteur (DO, hébergeur, confnum, etc.) et faciliter les échanges.
* Dans certains cas, elle peut co-rédiger le DA avec l’équipe produit.
* Dans tous les cas, l'équipe produit reste responsable de ce document.

2. L'équipe produit doit fournir le DA via des liens SharePoint éditables.

✅ Un premier lien doit mener au document Word ; un second aux sources des schémas.

ℹ️ Si l'équipe produit ne dispose pas d’un SharePoint projet, l'équipe d'accompagnement technique peut fournir sur demande un dossier dans notre SharePoint de travail.

❌ Nous n’intervenons pas sur un DA envoyé en pièce jointe par mail : risque important de versions concurrentes rendant notre intervention inefficace.

3.  L'équipe produit doit fournir une documentation fonctionnelle pour permettre d’appréhender le contexte et le sujet ; ou organiser un point de clarification.

## Points d'auto-contrôle pour maximiser les chances de validation en COAT
Ces règles déjà exposées dans le Pack DA sont fréquemment enfreintes, ce qui engendre une moindre efficacité des COAT (échanges supplémentaires, validation avec réserve, rejet, repassage en COAT, etc.).

✅ L'équipe produit peut utiliser ces éléments comme une liste de contrôles avant soumission du DA.

* **Conformité au modèle de DA** : baser tout nouveau DA sur le modèle du Pack DA, ou à défaut intégrer les nouveautés jusqu'au modèle de DA le plus récent
5. Vérifier la présence et la mise à jour de l’encart de suivi des changements (dernière page ou bloc 17 pour les anciens DA).
6. Respecter la nomenclature définie dans l’encart de suivi (exemple : DA-NomProjet-V1.0.3.docx).
7. Utiliser les templates Draw.io ou PowerPoint fournis dans le pack DA pour les schémas.
8. Assurer la cohérence des noms de catégories d'utilisateurs et de composants dans toutes les rubriques du DA.

## FAQ
* Faut-il intégrer les nouveautés du pack DA à relivraison du DA ?
 * Non obligatoire, mais mise à niveau occasionnelle recommandée et bienvenue