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
    visible: true
---

# Démarche de rationalisation

## Enjeu et objectifs

L'architecture des SI répond aux enjeux de gestion du patrimoine applicatif par une vision transverse des applications, SI, services et besoins auxquels ils répondent.

Ses principaux objectifs sont :

* valoriser au mieux les solutions existantes
* expliciter et objectiver les critères de décision pour l'ajout d'une nouvelle application
* supporter l'organisation dans sa transformation
* dessiner et maintenir la trajectoire de convergence du parc vers une cible partagée

## Processus RADAR pour une nouvelle application

**RADAR pour Réutiliser, Adapter, Développer, Acheter et Reformuler** est un moyen mnémotechnique simple pour adresser la complexité et la rationalisation des applications. L'objectif est de fournir des orientations sur la meilleure manière de traiter un besoin métier ou technique à travers une solution technologique.

## 1. Réutiliser

**Adresser le besoin par configuration ou évolution mineure d'un système déployé existant.** Tant qu'elle est déployée en production, la solution à réutiliser peut être :

* à la DNUM (ex: extension d'EFPConnect à la DGT, socle CMS Ondine, Démat Social)
* dans l'écosystème interministériel (ex: Démarches Simplifiées, PISTE@DGFIP)
* voire en SaaS (ex: produits Microsoft du ministère) La sécurité (ex: besoin d'hébergement HDS) et la gouvernance (ex: PISTE@DGFIP) sont souvent des enjeux important à apprécier pour la réutilisation maitrisée de solutions.

## 2. Adapter

**Adresser le besoin par l'évolution raisonnable et maitrisée d'une solution existante.** La solution à adapter et à redéployer peut être :

* une application interne (ex?)
* une solution open source interministérielle (ex: Démat Social comme fork de Démarches Simplifiées, Sites Faciles)
* une solution open source grand public (ex: Keycloack)

## 3. Développer

**Si malgré la recherche de compromis et d'arbitrages, le besoin est trop spécifique pour être porté par une solution existante, on considère la construction d'un produit dédié.** Ce produit doit alors respecter l'ensemble des préconisations de cette documentation pour garantir sa valorisation dans le temps.

## 4. Acheter

Pour des raisons de temps, de coût et d'efficacité, il peut être pertinent de souscrire à une solution venant du privé. **Dans ce cas le SaaS est à privilégier**. Une réflexion doit également être menée sur la volonté ou non d'investir sur la solution vis-à-vis de la stratégie, notamment s'il s'agit d'un besoin ponctuel.

## 5. Reformuler

Parfois un besoin peut être si spécifique qu'il devient déraisonnable techniquement ou financièrement de le traiter tel quel. Il convient alors d'analyser le besoin initial à nouveau, pour identifier une approche plus objective et pragmatique du sujet.
