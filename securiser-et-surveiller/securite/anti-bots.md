# 🔒 Sécurité anti-bots

L'enjeu est d'identifier les différentes menaces impliquant des bots (automates logiciels) et les solutions pour y faire face.

## Menaces dans notre contexte

Les bots sont prévus pour mener différents types d'attaques et servent différents objectifs malveillants :

* **Attaque par déni de service (DoS)** : ralentir ou bloquer un service, par une sollicitation massive depuis une ou plusieurs sources (attaque distribuée DDoS).
* **Vol de données** : par exemple par [web scraping](https://fr.wikipedia.org/wiki/Web_scraping).
* **Attaque par force brute** : obtenir un accès sans en être le détenteur légitime, afin de mener des actions illicites (détourner des subventions, manipuler le résultat d'élections professionnelles...)\
  \&#xNAN;_Les attaques sont souvent dépersonnalisées, opportunistes, mais pas toujours. Elles peuvent donc être ciblées ou systématiques._

## Enjeux d'accessibilité

[Captcha et accessibilité](https://design.numerique.gouv.fr/articles/2024-11-28-captcha-et-accessibilite/)

## Recommandations

* [**Des solutions au niveau réseau/middleware**](anti-bots.md#solutions-anti-bots-au-niveau-réseaumiddleware) sont à appliquer selon le contexte avec l'infogérant et/ou l'hébergeur. Sauf à appliquer l'approche ZeroTrust, il est déconseillé d'implémenter un anti-DDoS au niveau applicatif. Celui-ci étant déjà actif au niveau de l'hébergement.
* [**Des solutions au niveau applicatif**](anti-bots.md#solutions-anti-bots-au-niveau-applicatif) sont à appliquer selon le contexte avec l'architecte solution ou lead tech du produit (ou en sollicitant un [accompagnement technique](mailto:dnum-sdpsn.accotech@sg.social.gouv.fr))
* **Rate-limiting pour l'API** : le Rate-limiting au niveau [API Gateway](../../concevoir/api/api-gateway.md) ou [Reverse Proxy](https://fr.wikipedia.org/wiki/Proxy_inverse) est la solution à privilégier pour protéger une API des bots.
* **Rate-limiting + Honeypot pour l'IHM** : combinaison efficace pour protéger l'IHM. Attention cependant à ne pas créer de problème d'accessibilité avec Honeypot.

## Solutions anti-bots au niveau réseau/middleware

Ces mécanismes sont pris en charge en amont par l'hébergeur ou l'infogérant, ou plus localement par une [API Gateway](../../concevoir/api/api-gateway.md) ou un [Reverse Proxy](https://fr.wikipedia.org/wiki/Proxy_inverse) :

* **Filtrage IP (whitelist)** : limiter l'accès à un nombre fini de clients connus ou déclarés.
* **Blocage IP** : bloquer l'accès à des bots déjà identifiés, ou des sources habituelles d'intrusion.
* **Rate-limiting** : limiter de manière statique ou dynamique le nombre de requêtes d'un même client sur un temps donné. Le rate-limiting est à définir route par route par l'équipe produit en charge de l'application.
* **Observabilité applicative** : observer l'activité applicative grâce aux logs, pour déceler les comportements inhabituels et apprendre en continu. Une stratégie prudente vise à autoriser uniquement les comportements considérés comme habituels, plutôt que de bloquer les comportements inhabituels.

## Solutions anti-bots au niveau applicatif

* **Honeypot** : consiste à cacher un champ de formulaire qui n'est pas censé être utilisé. S'il est utilisé, le client web est considéré comme un bot. Le honeypot est cependant identifiable et contournable par un robot plus sophistiqué. Il peut présenter un problème d'accessibilité s'il n'est pas bien implémenté.
* **2FA** : l'authentification à 2 facteurs, présentée à la connexion et/ou lors d'une opération sensible et constitue une protection anti-bots importante.
* **Captcha** : vise à distinguer les humains des bots par l'analyse en arrière-plan d'un faisceau d'indices (comme le comportement de l'utilisateur) et/ou par un défi utilisateur visuel ou auditif. **Le défi utilisateur est une vraie douleur en terme d'ergonomie et d'accessibilité**, et est de moins en moins efficace face à la complexité des bots. L'avenir est aux solutions intelligentes et discrètes.

## Comparaison de différents Captcha

* [**Friendly Captcha**](https://friendlycaptcha.com/fr/#features)
  * Avantages : analyse en arrière-plan (aucun défi utilisateur), RGPD, européen
  * Inconvénients : non évalué au RGAA, payant (mais [référencé à l'UGAP](https://www.ugap.fr/editeurs-logiciels/friendly-captcha-gmbh-f31479))
  * Avis : option viable, mais à évaluer au RGAA
* [**hCaptcha**](https://www.hcaptcha.com/#comprehensive)
  * Avantages : analyse en arrière-plan (défi déclenché si besoin), effort d'accessibilité
  * Inconvénients : non évalué au RGAA, payant
  * Avis : option viable, mais à évaluer au RGAA
* [**Cloudflare Turnstile**](https://www.cloudflare.com/application-services/products/turnstile/)
  * Avantages : analyse en arrière-plan (aucun défi utilisateur), version gratuite
  * Inconvénient : non évalué au RGAA, payant pour retirer le logo Cloudflare
  * Avis : option viable, mais à évaluer au RGAA
* [**CaptchÉtat v2**](https://static.piste.gouv.fr/captchEtat/docs/CAPTCHA_v2_GUIDE_IMPLEMENTATION.pdf) (AIFE)
  * Avantages : solution étatique, accessibilité partielle (ex : défi audio)
  * Inconvénients : défi déclenché systématiquement, pas complètement accessible, paramétrage dans PISTE
  * Avis : à éviter, sauf si une v3 intelligente est prévue
* [**Google reCAPTCHA 3**](https://cloud.google.com/security/products/recaptcha)
  * Avantages : analyse en arrière-plan (défi déclenché si besoin), gratuit
  * Inconvénients : pas conforme RGPD, tracking commercial
  * Avis : prohibé
* [**ALTCHA**](https://altcha.org/fr)
  * Avantages : solution auto-hébergée, moderne, gratuite, conforme RGPD, EAA (Europeen Accessibility Act niveau AA WCAG 2.2)
  * Inconvénients : solution recente, un effort de sécurisation par le developpeur est nécessaire à fin de prévenir les attaques
  * Avis : Option viable, une validation sécurité reste nécessaire
