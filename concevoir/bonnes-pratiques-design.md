---
icon: list-check
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

# Bonnes pratiques de design

Ces bonnes pratiques garantissent que chaque produit numérique respecte les principes de base de conception d'expérience utilisateur.

{% hint style="info" %}
Ces bonnes pratiques doivent être mis en oeuvre par les designers en charge du produit, en collaboration avec le ou la cheffe de produit ainsi que les responsables métier et dev.
{% endhint %}

***

## Check-list pour les chef(fes) de produit

À copier-coller et utiliser pour suivre les étapes clés du processus de design 👇

* [ ] **Trouver un.e designer senior** référent sur votre produit.
* [ ] **Fichier Figma DNUM** créé et centralisant tous les éléments nécessaires.
* [ ] **Profils utilisateurs** définis avec leurs besoins et contextes d’usage.
* [ ] **Cartographies des usages** (parcours en diagrammes, journey map, carte d'empathie, etc.) disponibles.
* [ ] **Inspirations et adhérences** documentées (parangonnage, solutions similaires ou associées).
* [ ] **Vision de design** rédigée, claire et partagée avec les équipes.
* [ ] **Maquettes 100 % DSFR & RGAA** ou nouveaux composants respectant le DSFR et les standards RGAA.
* [ ] **Idéation** réalisée avec au moins 3 idées UX/UI pour chaque parcours principal.
* [ ] **Tests utilisateurs** menés (au moins 5 tests par profil utilisateur).
* [ ] **Annotation RGAA** ajoutées dans les maquettes.
* [ ] **Responsivité** documentée par des maquettes d'écrans mobiles à coté des écrans desktop.
* [ ] **Niveau d’effort et impact utilisateur** évalués pour chaque changement ou nouvelle fonctionnalité.
* [ ] Documentation à jour dans les espaces partagés (Doc de design, Figma, Figjam, etc.).

{% hint style="info" %}
**Astuce :** Demandez à votre designer de suivre cette checklist et de l'utiliser pour créer un planning de ses actions. Les designers sont en charge de mener et de valider chaque étape avec vous et l'équipe afin de garantir une collaboration fluide et un produit final de qualité !
{% endhint %}

***

## Etapes essentielles

Ce guide rassemble les étapes essentielles à suivre, de la compréhension des utilisateurs jusqu’à la mise en accessibilité. Il permet une collaboration fluide entre les parties prenantes et assure que nos produits répondent à nos exigences de qualité d'expérience utilisateurs.

***

### 1. **Fichier Figma dans l’espace DNUM**

* Centralise tous les éléments du processus de design.
* Sert de base unique pour les phases de collaboration et de tests.
* Doit inclure : maquettes, prototypes, annotations d’accessibilité, documentation visuelle.

{% hint style="info" %}
**Astuce** : Demandez à votre designer d'utiliser les modèles créés par la DNUM :

* Conception, maquettage, prototypage :[Modèle de fichier Figma](https://www.figma.com/design/XMBYkb0Yfgf5Xwus7Qqi4F/Mod%C3%A8le-Figma?m=auto\&t=4yobmo0a54wCxCct-6)
* Ateliers, diagrammes, idéation : [Modèle de fichier Figjam](https://www.figma.com/board/etgOPbk0hSxLYYWNM6XAJ0/Mod%C3%A8le---Fiichier-Figjam?t=irWaNRhEZf6oeXR3-6)
* Autres modèles utiles : [Modèle d'atelier RACI](https://www.figma.com/board/s9HzWSaD1LE7x84QUlN0EJ/Mod%C3%A8le---Atelier-RACI?t=irWaNRhEZf6oeXR3-6), [Modèle d'atelier vision](https://www.figma.com/board/ti4nGxJl3va5N67vhARvQJ/Mod%C3%A8le---Atelier-vision-et-besoins-produit?t=irWaNRhEZf6oeXR3-6), [Librairie de composants Sharepoint](https://www.figma.com/design/G6JxOLI7zE4BHcmwvMZDSH/SharePoint-Web-UI-Kit-\(Community\)?m=auto\&t=irWaNRhEZf6oeXR3-6)
{% endhint %}

***

### 2. **Profils utilisateurs**

* Définir : nombre d’utilisateurs, contexte d’utilisation, usages et besoins.
* Documenter les profils clés pour guider la conception.

***

### 3. **Cartographies des usages dans leur contexte**

* Inclure des outils visuels comme :
  * Parcours utilisateurs
  * Journey map
  * Story mapping
  * Carte d’empathie
  * Captures d’écran des interfaces existantes
* Ces éléments permettent une vision globale et contextuelle des usages.

***

### 4. **Inspirations et adhérences**

* Réaliser un parangonnage (benchmarking) des solutions :
  * Similaires existantes.
  * Associées à des enjeux similaires.
  * Représentant des solutions idéales.
* Identifier les adhérences techniques ou organisationnelles à prendre en compte.

***

### 5. **Vision de design**

* Répondre à cette question clé :
  * _Qu’est-ce qui sera amélioré dans la vie des utilisateurs une fois le produit mis à jour ?_
* Décrire clairement l’impact attendu et les erreurs d'expériences à éviter.

***

### 6. **100 % DSFR, le système de design de l'état français**

Le Design System est obligatoire pour les sites grand publics communiquant au nom de l'État et dont l'URL est en .gouv.fr

* Utilisez la dernière librairie [Figma DSFR](https://www.figma.com/@gouvfr)
* Validez les usages des composants en consultant le [site DSFR](https://www.systeme-de-design.gouv.fr/composants-et-modeles).
* En cas de création de nouveaux composants, s'assurer qu’ils respectent les standards UX/UI du DSFR.
* Discutez avec les dev sur le portage utilisé (Angular, React, Vue, etc) et demandez l'accès à la documentation de la librairie de portage utilisée

{% hint style="danger" %}
L'usage du DSFR est encadré :

* Seuls les sites en .gouv.fr peuvent bénéficier du DSFR
* Pour les sites internes, extranets, outils d'agent seuls **l'en-tête et le pied de page** sont obligatoires. Il est toutefois recommandé d'utiliser le DSFR sur l'intégralité du produit lors d'une refonte afin de faciliter la conception et le développement.
{% endhint %}

***

### 7. **Idéation**

L'idéation, ou recherche de solutions adaptées aux besoins des utilisateurs, doit se faire avec toutes les parties prenantes qui ont un impact sur le produit fini (responsable métier, responsable produit, expert recherche utilisateur, développeurs, etc.).

* Co-créer au moins 3 idées d’UX/UI différentes pour les parcours principaux.
* Encourager des approches innovantes et collaboratives pour répondre aux besoins identifiés.
* Encourager l'utilisation de FranceConnect ou équivalent.
* S'assurer que l'application respecte le ["Dites le nous une fois"](https://www.numerique.gouv.fr/services/guichet-dites-le-nous-une-fois/)

{% hint style="info" %}
**Astuce :** Intégrer la simplification du langage à ce stade permet de tester les hypothèses avec les utilisateurs. Ressource utile : [Sensibiliser et s’exercer aux méthodes de simplification des documents](https://www.modernisation.gouv.fr/outils-et-formations/simplifier-les-documents-administratifs#ConsidererUsager)
{% endhint %}

***

### 8. **Tests utilisateurs**

* Réaliser des tests utilisateurs sur maquettes ou prototypes :
  * Minimum de 5 tests par profil utilisateur.
  * Priorité donnée aux parcours les plus stratégiques.

***

### 9. **Mise en accessibilité**

* Faire une revue accessibilité sur maquette avec un expert en accessibilité.
* Mettre à jour les designs et ajouter les annotations spécifiques pour l’accessibilité.
* Faciliter l’intégration des exigences légales et des bonnes pratiques pour les développeurs.

***

### 10. **Documentation des maquettes pour dev et Responsive Design**

* S’assurer que tous les designs sont adaptés aux différents types d’écrans (mobile, tablette, desktop).
* Vérifier que les maquettes incluent des versions spécifiques pour les formats principaux.
* Prioriser les parcours critiques sur mobile, notamment pour des utilisateurs en déplacement.
* Garantir la cohérence visuelle et fonctionnelle entre les versions desktop et mobile.
* Tester les prototypes sur plusieurs tailles d’écran avant les validations finales.

{% hint style="info" %}
**Astuce :** Pensez à organiser les maquettes en parcours utilisateurs afin de faciliter la compréhension par les développeurs.&#x20;

**A noter :** Même si votre application n'est utilisable que sur ordinateur, elle doit pouvoir être utilisable à un zoom de 200 %
{% endhint %}

***

### 11. **Niveau d’effort de développement et impact utilisateur**

* Évaluer et documenter :
  * Le niveau d’effort technique par fonctionnalité.
  * L’impact attendu sur l’expérience utilisateur.
* Prioriser les fonctionnalités sur la base de ces critères.

***

### 12. **Suivi et documentation continue**

* Chaque étape de design doit être documentée dans l’espace partagé (Doc design, Figma, Figjam, etc.).
* Encourager un feedback continu et des démos avec les dev pour ajuster les décisions de design.
