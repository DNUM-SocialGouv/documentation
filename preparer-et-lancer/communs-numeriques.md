# ♻️ Solutions et communs numériques

La réutilisation de solutions et communs numériques découle d'une [démarche de rationalisation](rationalisation.md).

Parmi les différentes solutions numériques au catalogue, les communs numériques sont des ressources produites et gérées par une communauté d'utilisateurs selon des règles de gouvernance conjointement élaborées.

Tout produit DOIT réutiliser au maximum les solutions et communs numériques, en suivant les recommandations de ce guide.

## Quelle solution commun numérique pour quel produit ?

Mon produit est un(e)...

* **Site éditorial** (ou produit à forte composante éditoriale)
  * pour un gestionnaire de contenus (CMS) : [voir la page dédiée aux CMS](communs-cms.md)
  * pour un Wiki, une base de connaissance, une FAQ : [**GitBook**](https://www.gitbook.com/) est un Wiki SaaS gratuit avec contenu stocké sur GitHub. Exemples d'usages :
    * Le présent [guide DNUM](https://dnum-ministeres-sociaux.gitbook.io/ressources/) (instance DNUM partagée)
    * [Base de connaissance VAO](https://dnum-ministeres-sociaux.gitbook.io/vao-documentation/t1eK0jUdXMliu8S6UWUr) (instance DNUM partagée)
    * [Base de connaissance Mon Suivi Social](https://mon-suivi-social.gitbook.io/mon-suivi-social) (instance dédiée)
    * Documentation produit interne
    * [Base de connaissance / FAQ DACCORD](https://docs.accord-depot.travail.gouv.fr/)
* **Démarche administrative en ligne**
  * pour le **front-office usager** :
    * utiliser [Démarche Numérique (ou Démat Social)](communs-demarche-numerique.md) pour éviter le développement spécifique
    * en dernier recours, envisager le développement spécifique du front-office
  * pour le **back-office agent** :
    * utiliser les nombreuses fonctionnalités d'administration et d'instruction de [Démarche Numérique (ou Démat Social)](communs-demarche-numerique.md)
    * si cela ne suffit pas, envisager un back-office _complémentaire_ à Démarche Numérique (intégration par API)
    * en dernier recours, envisager le développement spécifique complet du produit
* **Référentiel de données**
  * Si possible paramétrage front et back sur [Grist](communs-grist.md) pour une application de gestion interne ou à portée et criticité modérée
  * Sinon développement front spécifique sur la base d'un [backend-as-a-service](communs-numeriques.md#backends-as-a-service)
  * Sinon envisager le développement spécifique complet du référentiel

## API externes

* Les API Entreprise
  * [API Entreprise complète](https://www.data.gouv.fr/fr/dataservices/api-entreprise/) : pas de recherche multicritères
  * [API SIRENE de l'INSEE](https://portail-api.insee.fr/catalog/api/2ba0e549-5587-3ef1-9082-99cd865de66f) pour les besoins simples de recherche
  * [API Recherche Entreprise](https://www.data.gouv.fr/fr/dataservices/api-recherche-dentreprises/) : recherche par SIRET/nom ET filtrage sur critères (codes d'activité, géographie...)
  * [API Association du Compte Asso (DJEPVA) via API Entreprise](https://www.data.gouv.fr/dataservices/api-donnees-associations-djepva-bouquet-api-entreprise/) : intègre Alsace-Moselle et les données des autres API (RNA, SIRENE, DILA)
* [API Base d'Adresse Nationale (BAN)](https://www.data.gouv.fr/dataservices/api-adresse-base-adresse-nationale-ban/)
* [API Recherche des personnes physiques (SFiP)](https://www.data.gouv.fr/dataservices/api-service-finances-publiques-sfip/) : données personnelles d'un citoyen (état civil complet, dernière adresse connue de l’administration fiscale, identifiant fiscal ou SPI).

La plupart des APIs du service public sont référencées sur [https://www.data.gouv.fr/dataservices](https://www.data.gouv.fr/dataservices)

## API internes
Les API [https://arssante.opendatasoft.com/](https://arssante.opendatasoft.com/) :
* API des établissements de santé (données FINESS)
* API des professionnels de santé (données RPPS)

## Frameworks et librairies standards

Des lors qu'il y a développement spécifique, le projet DOIT réutiliser au maximum les "building blocks" listés ci-dessous :

* [**Authentification**](../concevoir/authentification.md)
* [**Stockage et accès aux données**](../concevoir/data/)
* [**API Gateway**](../concevoir/api/api-gateway.md)
* Stockage documentaire et GED (type S3…)
* **Emailing transactionnel** (templating et envois) : Sarbacane Sendkit (anc. Tipimail)
* Publipostage PDF (gestion des templates avec balises + production de documents)
* Workflow : pas de solution pertinente identifiée
* **Décisionnel** (tableaux de bord, production de fichiers CSV, DataViz, etc.) : [Metabase](https://www.metabase.com/start/oss/)
* **Mesure d'audience** : [Matomo](communs-numeriques.md#matomo-pour-la-mesure-daudience)
* **ETL/ELT**
  * ETL lightweight embarqué dans les projets : SpringBatch en Java, _à définir en JS_
  * Projet à dominante ETL : Talend EE (géré par le bureau DATA)
  * Orchestrateur de flux : Kestra (géré par le bureau DATA)
* Chatbot
* IA : YAGNI :-)

## Backends as a Service

* Eventuellement Grist comme Backend-as-a-Service avec un frontend spécifique s'il n'y a pas besoin de permissions Grist avancées. Quelques limitations de Grist :
  * Les permissions avancées ne sont pas accessibles par API
  * Pas de propagation de l'authentification ProConnect par API : compte de service seulement
  * l'API de l'instance DINUM est limitée à 10 appels en parallèle par document Grist
* Manifest.build a été écarté car trop limité

## Matomo pour la mesure d'audience

[Matomo](https://matomo.org/) est la solution de mesure d'audience et d'utilisation de nos services numériques (web analytics). Tout projet DEVRAIT réutiliser l'une des 3 instances de Matomo existantes :

| Instance       | Hébergement                                                       |
| -------------- | ----------------------------------------------------------------- |
| Atlas (FabNum) | [SaaS @boscop.fr](https://boscop.fr/matomo-hebergement/)          |
| DICOM          | [SaaS @matomo.org](https://matomo.org/matomo-cloud/)              |
| Cegedim        | [SaaS @Cegedim.cloud](https://cegedim.cloud/produits/analytique/) |

Bien qu'[Eulerian](https://www.eulerian.com/) soit une solution souveraine, elle n'est pas privilégiée.

## Pistes explorées et décisions d'architecture

* **GLPI** écarté en 04/2025 (workflow pas assez contraignant pour le métier et pas paramétrable ; pas 12-factors (stockage FS) ; peu accessible)
* **Manifest.build** est un Backend-as-a-Service open source en JS. Convient pour des besoins CRUD simple. Très limité sur l'authentification et la gestion des droits.
* **Directus.io** est un Backend-as-a-Service satisfaisant mais a été écarté à cause de son coût de licence