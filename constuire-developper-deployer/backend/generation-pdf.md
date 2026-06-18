# Génération de PDF

Voici quelques recommandations pour favoriser la génération de documents PDF accessibles :

## Librairies recommandées
- JS : PDFKit
- Java : iText ou PDFBox
 
## Utilisation de PDFKit dans SIRENA
Les résultats sont satisfaisants, avec accessibilité conforme à la norme PDF/UA-1
Cependant, PDFKit ne suffit pas pour l’accessibilité. Il faut baliser correctement le contenu et utiliser la norme **ISO 32000-2 – PDF Association** (Chapitre 17.4 nottament) dont voici les points-clés :
- La collaboration dev / expert A11Y / métier est importante dès la conception
- Définir les titres, sous-titres, sous-sections, etc.
- Listes : utiliser LB pour chaque item, définir les rôles si nécessaire (roleMap manquant)
- Lignes horizontales / décoratives : ajouter en tant qu’artifact cf. La documentation
- Métadonnées : auteur, titre, sujet, mots-clés
- Polices : charger Roboto, taille de caractères minimum pour lisibilité (12pt)
- Vérifier l’ordre logique pour la lecture par lecteur d’écran

## Vérification avec PAC
Pour vérifier que le PDF généré est accessible, utiliser l’outil de vérification [PAC : PDF Accessibility Checker](https://pdfa.org/product/pac/) :
=> L'onglet WCAG doit passer au Vert à minima

## HTML comme alternative au PDF
Pour rappel, il existe des alternatives aux PDFs. Côté front, on génère une page HTML accessible optimisée pour l’impression avec CSS Print. L’utilisateur peut ensuite l’imprimer.