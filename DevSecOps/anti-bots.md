# Lutte anti-bots
L'enjeu est d'identifier les différentes menaces impliquant des bots (automates logiciels) et les solutions pour y faire face.

## Enjeux et menaces dans le contexte du Ministère
Les bots sont prévus pour mener différents types d'attaques et servent différents objectifs malveillants :
- **Attaque par déni de service (DoS)** pour ralentir ou bloquer un service, par une sollicitation massive depuis une ou plusieurs sources (attaque distribuée DDoS).
- **Vol de données** : par exemple par [web scraping](https://fr.wikipedia.org/wiki/Web_scraping).
- **Action illicite** acte malveillant en vue d'obtenir un profit ou un résultat, pour soit ou pour autrui. Ex: vol de subvention.
- **Ingérence** manipulation de données en vue de fausser une information, un résultat.
- **Attaque par force brute** : l'attaque par brute force n'est pas un but en soit mais peut servir d'autres objectifs.\
_Les attaques sont souvent dépersonnalisées, opportunistes, mais pas toujours. Elles peuvent être ciblées ou systématiques._ 

## Recommandations
- [**Solutions au niveau réseau**](#solutions-anti-bots-au-niveau-réseau) : sauf bonne raison d'appliquer l'approche ZeroTrust, il n'est pas nécessaire de réimplémenter un anti-DDoS au niveau applicatif. Celui-ci étant déjà actif au niveau de l'hébergement.
- [**Solutions au niveau applicatif**](#solutions-anti-bots-au-niveau-applicatif) : le choix d'une solution de captcha est un savent mélange entre ergonomie, accessibilité, sécurité, coût et performance.
- **Observation des logs** : Quels que soient les mécanismes en place, il convient de continuer à observer les logs techniques et applicatifs pour déceler les comportements inhabituels. Une stratégie vise à autoriser uniquement les comportements considérés comme habituels, plutôt que de bloquer les comportements inhabituels.

## Solutions anti-bots au niveau réseau
Ces mécanismes sont pris en charge en amont par l'hébergeur, ou plus localement par une [API Gateway](../Architecture/api-gateway.md) ou un [Reverse Proxy](https://fr.wikipedia.org/wiki/Proxy_inverse) du projet :
- **Filtrage IP (whitelist)** : limiter l'accès à un nombre fini de clients connus ou déclarés.
- **Blocage IP** : bloquer l'accès à des bots déjà identifiés, ou des sources habituelles d'intrusion.
- **Rate-limiting** : limiter de manière statique ou dynamique le nombre de requêtes d'un même client sur un temps donné.

## Solutions anti-bots au niveau applicatif
- **Captcha** : vise à distinguer les humains des bots par un challenge visuel ou auditif. Le captcha est une vraie douleur en terme d'ergonomie et d'accessibilité, et est de moins en moins efficace face à la complexité des bots.
- **reCaptcha** : Captcha invisible qui analyse en arrière-plan le comportement de l'utilisateur, et peut déclencher un captcha pour confirmer l'humanité de l'utilisateur. L'avenir est à ce genre de solutions intelligentes, discrètes, passives, qui se basent sur un faisceau d'indices.
- **Honeypot** : consiste à cacher un champ de formulaire qui n'est pas sensé être utilisé. S'il est utilisé, le client est considéré comme un bot. L'approche présente peu d'intérêt car il est facilement identifiable et contournable. Il présente par ailleurs un problème bloquant d'accessibilité. Ne pas confondre Honeypot et [Honey Bucket](https://dec.alaska.gov/eh/solid-waste/how-do-i-dispose-of/honeybucket-waste/) qui servent des objectifs différents.
- **2FA/MFA** : l'authentification à 2 facteurs peut-être présentée à la connexion et/ou lors d'une opération sensible et constitue une protection anti-bots importante.

## Comparaison de différents Captcha
- [**Captchétat v2**](https://static.piste.gouv.fr/captchEtat/docs/CAPTCHA_v2_GUIDE_IMPLEMENTATION.pdf) (AIFE)
    - Avantages : solution étatique, accessibilité prise en compte
    - Inconvénients : déclenchement systématique, paramétrage dans PISTE
- **hCaptcha**
- [**Cloudflare**](https://www.cloudflare.com/fr-fr/plans/)
    - Avantages : solution complète, déclenchement contextuel
    - Inconvénient : payant, fullstack (WAF)
- [**Google reCAPTCHA 2**](https://cloud.google.com/security/products/recaptcha)
    Avantages : ergonomie, sécurité, performance, gratuit
    Inconvénients : pas de garantie vie privée