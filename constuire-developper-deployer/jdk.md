
# 📘 Standard JDK — Choix d’Eclipse Temurin

## Objectif

Ce document définit le **cadre de cohérence** pour le choix d’**Eclipse Temurin** comme distribution Java (JDK) de référence.

Il vise à garantir :
- la cohérence des choix techniques,
- la pérennité des architectures,
- la maîtrise des risques,
- la conformité open source,
- la soutenabilité économique,

## Périmètre

Ce standard s’applique à :
- toutes les applications Java,
- toutes les plateformes d’exécution JVM,
- tous les environnements (DEV / INT / PREPROD / PROD), Legacy et Cloud
- tous les produits de la DNUM

## Décision d’architecture

Eclipse Temurin est retenu comme distribution Java standard

### Préconsisation :
- Cibler la dernière version du JDK/JRE Temurin

## Périmètre d'application  
### Produit en Build - Devrait appliquer la recommandation
Le produit devra adopter le JDK Temurin pour l'ensemble des environnements. 
Pour les environnements cloud, une image docker officielle devrait être utilisées  


### Produit déjà en Production avec un autre OpenJDK
Dans le cadre de la gestion de l'absolescence logicielle, le JDK Temurin devrait être préviligié. 

