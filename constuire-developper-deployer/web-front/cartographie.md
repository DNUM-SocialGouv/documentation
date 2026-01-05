# 📍 Cartographie

Il existe plusieurs solutions de représentation cartographique du territoire, suivant la place de la cartographie dans le produit numérique :

* Si la cartographie ne présente pas de données sensibles, considérer l'[instance uMap interministérielle](cartographie.md#instance-umap-interministérielle)
* Si la cartographie est une fonctionnalité spécifique d'un produit, implémenter la [cartographie souveraine minimum](cartographie.md#cartographie-souveraine-minimum)
* Si la cartographie est la finalité du produit, envisager le [Système d'Information Géographique du Ministère](cartographie.md#sig-arcgis-du-ministère)

## Instance uMap interministérielle
L'[instance uMap (OpenStreetMap) de l'ANCT](https://umap.incubateur.anct.gouv.fr/fr/) est accessible librement par tout agent public.

Avantages :
* Pas de déploiement d'un composant de cartographie
* Géolocalisation possible de l'utilisateur
* Connexion à diverses sources de données (GeoJSON, DataGouv, etc.)
* Peut-être embarqué sous forme d'iframe dans un produit
* Connexion ProConnect pour l'administrateur

Inconvénients :
* Non adapté aux données nominatives ou particulièrement sensibles, car les moyens de sécurisation sont limités entre uMap et la source de données.

## Cartographie spécifique minimum

Pour intégrer une cartographie dans une application web javascript, voici la solution spécifique et souveraine minimum :

* **Composant web** : [Leaflet](https://leafletjs.com/)
* **Fond de carte** : OpenStreetMap (par défaut) ou bien IGN (satellite, relief, cadastre, etc.)
* **Géocodage des Points d'Intérêt** : API de géocodage de la [Géoplateforme IGN](https://geoservices.ign.fr/documentation/services/services-geoplateforme/geocodage). _A noter que l’API BAN de géocodage est dépréciée._
* **Affichage des Points d'Intérêt sur la carte** : en javascript, ajout explicite de POI avec le résultat du géocodage stocké en base au préalable.

Exemple de projet implémentant cette solution : SILAV

Partant de cette solution minimum, il est possible de l'enrichir : traçage de polygones, calcul de distances, etc.

## SIG ArcGIS du Ministère

Un [Système d'Information Géographique (SIG)](https://fr.wikipedia.org/wiki/Syst%C3%A8me_d'information_g%C3%A9ographique) est une solution complète de collecte, de traitement et de publication de données géographiques. Le bureau DATA du Ministère met en oeuvre la solution commerciale [ArcGIS](https://www.arcgis.com/).

Avantages d'ArcGIS :

* Pertinent pour les besoins forts de maitrise du territoire (ex: gestion des eaux, de la propagation d'épidémies, etc.)
* Solution reconnue et utilisée par d'autres administrations comme le Ministère de l'Intérieur et l'Institut Géographique National (IGN).

Inconvénients d'ArcGIS :

* Vendor lock-in : on implémente dans l'outil, et non autour ou à-côté.
* Moindre CI/CD
