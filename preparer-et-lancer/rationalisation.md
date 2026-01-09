# ♻️ Démarche de rationalisation

> _Il semble que la perfection soit atteinte non quand il n'y a plus rien à ajouter, mais quand il n'y a plus rien à retrancher. Au terme de son évolution, la machine se dissimule._ Antoine de Saint-Exupéry.

## Objectifs de la démarche

* Limiter la complexité et l'hétérogénéité du parc applicatif
* Eviter les solutions spécifiques en réponse à des problèmes bien connus
* Limiter le coût total de possession (hébergement, exploitation, maintenance) dans le temps
* Limiter les risques liés à la sécurité 

## Processus RADAR

**RADAR pour Réutiliser, Adapter, Développer, Acheter, Reformuler** est un moyen mnémotechnique pour gérer la complexité :
1. **Réutiliser** une solution existante déjà déployée en production :
    * Solution DNUM (ex : extension d'EFPConnect à la DGT, socle Ondine pour un nouveau site éditorial, Démat Social pour une nouvelle démarche)
    * Solution interministérielle (ex : Démarche Numérique, PISTE@DGFIP)
2. **Adapter** une solution open source existante :
    * Solution interministérielle (ex : DématSocial étend Démarche Numérique, Portail BI repose sur Sites Conformes)
    * Solution grand public (ex : N8N ou Kestra pour un agrégateur de données, Metabase pour un tableau de bord, KeyCloak comme socle d'EFP Connect et ProConnect)
3. **Développer** un produit dédié, seulement si on sait justifier qu'un besoin est trop spécifique pour une solution existante.
4. **Acheter** : une solution commerciale en SaaS par souci d'efficacité.
5. **Reformuler** un besoin déraisonnable, pour identifier une approche plus pragmatique.
