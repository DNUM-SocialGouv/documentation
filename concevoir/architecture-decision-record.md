---
icon: list-check
---

# Fiche de Décision d'Architecture (ADR)
Une Fiche de Décision d'Architecture (ADR) est un document qui capture une décision d'architecture importante en tenant compte du contexte et des conséquences de cette décision.

### Choix du modèle ?
👉 Plusieurs modèles sont proposés. Voir <a href="https://github.com/joelparkerhenderson/architecture-decision-record/tree/main/locales/en/templates" id="template-adr">modèles ADR</a>


## Modèle ADR By Michael Nygard

**Titre**  
Décrivez le titre de la décision.

**Statut**  
Quel est le statut ? (proposé, accepté, rejeté, déprécié, remplacé, etc.)

**Contexte**  
Quel est le problème ou le contexte qui motive cette décision ou ce changement ?

**Décision**  
Quelle est la décision ou le changement proposé/réalisé ?

**Conséquences**  
Qu'est-ce qui devient plus facile ou plus difficile à cause de ce changement ?


## Organisation des ADR

Pour assurer une gestion efficace des Fiches de Décision d'Architecture, il est recommandé :

- **Stockage centralisé** : Conserver tous les ADR dans un répertoire dédié du projet (ex. `/docs/adr/`).
- **Nomination cohérente** : Utiliser un format de nommage standard, tel que `adr-<numéro>-<titre>.md`.
- **Historisation** : Maintenir un historique des décisions pour faciliter le suivi des évolutions.
- **Référencement croisé** : Lier les ADR entre elles lorsque des décisions sont dépendantes ou liées.
- **Revue périodique** : Planifier des revues régulières pour valider la pertinence des décisions existantes.
- **Accessibilité** : S'assurer que les ADR sont facilement accessibles à toutes les parties prenantes du projet.


## Outil ADR Manager

- **VS Code ADR Extension**  
    Extension pour Visual Studio Code facilitant la création et la gestion des ADR directement depuis l’éditeur.  
    [ADR Extension sur le Marketplace VS Code](https://marketplace.visualstudio.com/items?itemName=StevenChen.vscode-adr-manager)

    ![Capture d’écran de l’extension ADR dans VS Code](./images/adr-extension-screenshot.png)