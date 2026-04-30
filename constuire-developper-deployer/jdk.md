# 🧿 Standard JDK/JRE

## 🎯 Objectif

Ce document définit le **cadre de cohérence** pour le choix d’**Eclipse Temurin** comme distribution Java (JDK/JRE) de référence pour les produits de la DNUM.

Il vise à garantir :

* la cohérence des choix techniques des produits développés en Java,
* la pérennité des architectures,
* la maîtrise des risques (techniques, sécurité, conformité),
* la conformité open source et réglementaire,
* la soutenabilité économique (TCO),
* la standardisation des environnements d’exécution Java.

## 📌 Périmètre

Ce standard s’applique :

* aux produits développés en Java,
* aux plateformes JVM on‑premise, cloud et conteneurisées,
* à l’ensemble des environnements (DEV, INT, PREPROD, PROD),

⚠️ **Avec une application différenciée selon le cycle de vie des produits** (nouveaux projets vs existant).

## 🧭 Décision d’architecture

#### Principe général

**Eclipse Temurin est retenu comme distribution JDK/JRE de référence pour la DNUM.**

Cette décision s’inscrit dans une **trajectoire progressive de convergence**, fondée sur :

* les opportunités projets,
* la maîtrise des risques,
* la capacité des plateformes d’exploitation.

#### Justifications

* Conformité au standard OpenJDK
* Gouvernance ouverte (Eclipse Foundation)
* Distribution stable, certifiée et largement adoptée
* Absence de dépendance à un éditeur propriétaire
* Optimisation des coûts (licences et exploitation)
* Large adoption dans les environnements cloud et conteneurisés



## ⚙️ Principes structurants

### Versions Java

* ✅ **Seules les versions LTS sont autorisées** dans le cadre de ce standard.
* ✅ La version retenue doit être une **version LTS supportée** au moment du projet.
* ❌ L’utilisation de versions non‑LTS est exclue.

### 📦 Périmètre d’application

#### 🟢 Produits en cours de développement (nouveaux projets)

Pour les nouveaux produits Java :

* ✅ **Eclipse Temurin est obligatoire** sur l’ensemble des environnements.
* ✅ Une version **LTS exclusivement** doit être utilisée.
* ✅ La version JDK doit être cohérente entre DEV → PROD.
* ✅ Le standard doit être intégré aux pipelines CI/CD.

#### ☁️ Cloud & conteneurisation

* ✅ L’utilisation des **images Docker officielles Eclipse Temurin** est requise.
* ✅ Les images doivent être :
  * maintenues à jour,
  * issues des registries officiels,
  * versionnées explicitement (ex. `temurin:25-jdk`).

ℹ️ En environnement conteneurisé, **Eclipse Temurin constitue déjà le standard de fait** et ne fait pas l’objet de remise en question.

#### 🟡 Produits existants en production

Pour les produits Java existants :

* ✅ Le **maintien en condition opérationnelle** reste prioritaire.
* 🔁 Le passage à Eclipse Temurin est **recommandé mais non obligatoire**.
* ✅ Il doit être étudié **à l’occasion** :
  * de la gestion de l’obsolescence,
  * des montées de version Java (LTS),
  * des travaux de modernisation, refonte ou migration cloud.
* ❌ **Aucune migration massive ou automatisée n’est attendue à court terme.**

**Recommandation**

Eclipse Temurin constitue la **cible privilégiée** lors des évolutions techniques de l’existant.

#### 🔴 Cas des plateformes très obsolètes

Pour les plateformes reposant sur :

* des OS en fin de vie (ex. CentOS),
* des stacks techniques très anciennes,

➡️ **Un simple changement de JDK est insuffisant**.

Ces situations relèvent d’**approches globales de modernisation** :

* refonte applicative,
* replatforming,
* conteneurisation,
* ou trajectoire produit dédiée.



### 🧩 Pré‑requis et dépendances infrastructure

L’adoption d’Eclipse Temurin est **conditionnée** par la disponibilité des briques d’exploitation suivantes :

* Mise à disposition des repositories Temurin (RPM signés, Katello, etc.),
* Adaptation des outillages :
  * Ansible,
  * RunDeck,
  * supervision JVM,
* Gestion et **standardisation des certificats / keystores** (sujet transverse).

ℹ️ Tant que ces pré‑requis ne sont pas en place, Eclipse Temurin constitue une **cible d’architecture** et non une obligation immédiate pour l’existant.



## ⚠️ Points de vigilance

* Vérifier la compatibilité applicative lors d’un changement de distribution JDK
* Tester les dépendances critiques (JDBC, librairies natives, sécurité)
* Vérifier les certificats (cacerts) si personnalisés
* S’assurer de la bonne configuration des variables (JAVA\_HOME, PATH)



## 🏁 Synthèse

Eclipse Temurin est retenu comme standard DNUM car il permet :

* une standardisation du runtime Java,
* une réduction des risques techniques et juridiques,
* une optimisation des coûts,
* une meilleure gestion de l’obsolescence Java,
* un alignement avec les pratiques cloud et DevOps,
* une pérennité des systèmes Java.
