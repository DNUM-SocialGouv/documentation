# Lutte anti-bots
L'enjeu est d'identifier les différentes menaces impliquant des bots (automates logiciels) et les solutions pour y faire face.

## Enjeux et menaces dans le contexte du Ministère
Les bots sont prévus pour mener différents types d'attaques et servent différents objectifs malveillants :
- **Attaque par déni de service (DoS)** : ralentir ou bloquer un service, par une sollicitation massive depuis une ou plusieurs sources (attaque distribuée DDoS).
- **Vol de données** : par exemple par [web scraping](https://fr.wikipedia.org/wiki/Web_scraping).
- **Attaque par force brute** : obtenir un accès sans en être le détenteur légitime, afin de mener des actions illicites (détourner des subventions, manipuler le résultat d'élections professionnelles...)\
_Les attaques sont souvent dépersonnalisées, opportunistes, mais pas toujours. Elles peuvent donc être ciblées ou systématiques._ 

## Recommandations
- [**Des solutions au niveau réseau/middleware**](#solutions-anti-bots-au-niveau-réseaumiddleware) sont à appliquer selon le contexte avec l'infogérant et/ou l'hébergeur. Sauf à appliquer l'approche ZeroTrust, il est déconseillé d'implémenter un anti-DDoS au niveau applicatif. Celui-ci étant déjà actif au niveau de l'hébergement.
- [**Des solutions au niveau applicatif**](#solutions-anti-bots-au-niveau-applicatif) sont à appliquer selon le contexte avec l'architecte solution ou lead tech du projet (ou en sollicitant un [accompagnement SDPSN / DD](https://msociauxfr.sharepoint.com/teams/BureauDesignDev/SitePages/Notreoffre.aspx))
- **Rate-limiting pour l'API** : le Rate-limiting au niveau [API Gateway](../Architecture/api-gateway.md) ou [Reverse Proxy](https://fr.wikipedia.org/wiki/Proxy_inverse) est la solution à privilégier pour protéger une API des bots.
- **Rate-limiting + Honeypot pour l'IHM** : malgré les problèmes d'accessibilité de l'approche Honeypot, cette combinaison reste efficace pour protéger l'IHM.

## Solutions anti-bots au niveau réseau/middleware
Ces mécanismes sont pris en charge en amont par l'hébergeur ou l'infogérant, ou plus localement par une [API Gateway](../Architecture/api-gateway.md) ou un [Reverse Proxy](https://fr.wikipedia.org/wiki/Proxy_inverse) du projet :
- **Filtrage IP (whitelist)** : limiter l'accès à un nombre fini de clients connus ou déclarés.
- **Blocage IP** : bloquer l'accès à des bots déjà identifiés, ou des sources habituelles d'intrusion.
- **Rate-limiting** : limiter de manière statique ou dynamique le nombre de requêtes d'un même client sur un temps donné. Le rate-limiting est à définir route par route
- **Observabilité applicative** : observer l'activité applicative grâce aux logs, pour déceler les comportements inhabituels et apprendre en continu. Une stratégie prudente vise à autoriser uniquement les comportements considérés comme habituels, plutôt que de bloquer les comportements inhabituels.

## Solutions anti-bots au niveau applicatif
- **Captcha** : vise à distinguer les humains des bots par l'analyse en arrière-plan d'un faisceau d'indices (comme le comportement de l'utilisateur) et/ou par un défi utilisateur visuel ou auditif. Le défi utilisateur est une vraie douleur en terme d'ergonomie et d'accessibilité, et est de moins en moins efficace face à la complexité des bots. Le choix d'une solution de captcha est un savant mélange entre ergonomie, accessibilité, sécurité, coût et performance. L'avenir est aux solutions intelligentes et discrètes.
- **Honeypot** : consiste à cacher un champ de formulaire qui n'est pas censé être utilisé. S'il est utilisé, le client est considéré comme un bot. L'approche présente peu d'intérêt car il est facilement identifiable et contournable. Il présente par ailleurs un problème bloquant d'accessibilité. Ne pas confondre Honeypot et [Honey Bucket](https://dec.alaska.gov/eh/solid-waste/how-do-i-dispose-of/honeybucket-waste/) qui servent des objectifs différents.
- **2FA/MFA** : l'authentification à 2 facteurs, présentée à la connexion et/ou lors d'une opération sensible et constitue une protection anti-bots importante.

## Comparaison de différents Captcha
- [**CaptchÉtat v2**](https://static.piste.gouv.fr/captchEtat/docs/CAPTCHA_v2_GUIDE_IMPLEMENTATION.pdf) (AIFE)
    - Avantages : solution étatique, accessibilité prise en compte (ex : défi audio)
    - Inconvénients : défi déclenché systématiquement, paramétrage dans PISTE
    - Avis : tombe en désuétude, à voir si une v3 intelligente est prévue
- [**Friendly Captcha**](https://friendlycaptcha.com/fr/#features)
    - Avantages : analyse en arrière-plan (aucun défi utilisateur), RGPD, européen, accessible (relativement au WCAG [d'après la déclaration de l'éditeur](https://friendlycaptcha.com/insights/captcha-accessibility/), non évalué au RGAA)
    - Inconvénients : payant (mais [référencé à l'UGAP](https://www.ugap.fr/editeurs-logiciels/friendly-captcha-gmbh-f31479))
    - Avis : option viable
- [**hCaptcha**](https://www.hcaptcha.com/#comprehensive)
    - Avantages : analyse en arrière-plan (défi déclenché si besoin), effort d'accessibilité
    - Inconvénients : payant
    - Avis : option viable
- [**Cloudflare Turnstile**](https://www.cloudflare.com/application-services/products/turnstile/) (repose sur hcaptcha)
    - Avantages : analyse en arrière-plan (aucun défi utilisateur), version gratuite
    - Inconvénient : payant pour retirer le logo Cloudflare, plus lourd à installer (écosystème éditeur)
    - Avis : option viable
- [**Google reCAPTCHA 3**](https://cloud.google.com/security/products/recaptcha)
    - Avantages : analyse en arrière-plan (défi déclenché si besoin), gratuit
    - Inconvénients : pas conforme RGPD, tracking commercial
    - Avis : prohibé
