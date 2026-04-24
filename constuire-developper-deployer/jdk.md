# 📘 Standard JDK/JRE — Choix d’Eclipse Temurin pour les produits DNUM

## 🎯 Objectif

Ce document définit le **cadre de cohérence** pour le choix d’**Eclipse Temurin** comme distribution Java (JDK/JRE) de référence pour les produits de la DNUM.

Il vise à garantir :
- la cohérence des choix techniques des produits développés en Java,
- la pérennité des architectures,
- la maîtrise des risques (techniques, sécurité, conformité),
- la conformité open source et réglementaire,
- la soutenabilité économique (TCO),
- la standardisation des environnements d’exécution Java.

## 📌 Périmètre

Ce standard s’applique à :
- tous les produits DNUM développés en Java,
- toutes les plateformes d’exécution JVM,
- tous les environnements : DEV, INT, PREPROD, PROD,
- tous les contextes : legacy, on-premise, cloud et conteneurisés.

## 🧭 Décision d’architecture

**La distribution Eclipse Temurin est retenue comme standard JDK/JRE pour l’ensemble des produits de la DNUM.**

### Justifications
- Conformité au standard OpenJDK  
- Gouvernance ouverte (Eclipse Foundation)  
- Distribution stable, certifiée et largement adoptée  
- Absence de dépendance à un éditeur propriétaire  
- Optimisation des coûts (licence et exploitation)  
- Compatibilité avec les environnements cloud et DevOps  

## ⚙️ Préconisations

- Cibler une version LTS supportée (ex: Java 25)  
- Privilégier la dernière version LTS stable disponible  
- Maintenir une cohérence de version entre les environnements (DEV → PROD)  
- Mettre en place une politique de mise à jour régulière (patchs sécurité / CPU)  

## 📦 Périmètre d’application

### 🟢 Produits en cours de développement (Build)

Les produits en phase de développement :
- doivent adopter Eclipse Temurin sur l’ensemble des environnements,
- doivent garantir l’alignement des versions JDK entre les environnements,
- doivent intégrer ce standard dans les pipelines CI/CD.

#### Cloud / Conteneurisation
- L’utilisation des images Docker officielles Temurin est requise,
- Les images doivent être :
  - maintenues à jour,
  - issues de sources fiables (registry officiel),
  - versionnées explicitement (ex : `temurin:25-jdk`).

### 🟡 Produits existants en production (avec autre OpenJDK)

Pour les produits déjà en production :

- Le maintien en condition opérationnelle reste prioritaire,
- Le passage à Eclipse Temurin doit être étudié dans le cadre :
  - de la gestion de l’obsolescence logicielle,
  - des montées de version Java (LTS),
  - des travaux de modernisation ou de migration cloud.

#### Recommandation
**Eclipse Temurin doit être privilégié comme cible lors des évolutions techniques.**

## ⚠️ Points de vigilance

- Vérifier la compatibilité applicative lors d’un changement de distribution JDK  
- Tester les dépendances critiques (JDBC, librairies natives, sécurité)  
- Vérifier les certificats (cacerts) si personnalisés  
- S’assurer de la bonne configuration des variables (JAVA_HOME, PATH)  

## 🏁 Synthèse

Eclipse Temurin est retenu comme standard DNUM car il permet :

- une standardisation du runtime Java,  
- une réduction des risques techniques et juridiques,  
- une optimisation des coûts,  
- un alignement avec les pratiques cloud et DevOps,  
- une pérennité des systèmes Java.  
