# 👀 Sentry

***

## Présentation

Sentry est une plateforme de monitoring d'erreurs et de performance pour applications. Elle collecte les exceptions, les traces et les contextes pour aider à diagnostiquer et résoudre les problèmes en production.

## Objectif et public

Document destiné aux développeurs et ingénieurs DevOps souhaitant intégrer Sentry dans leurs applications pour la supervision des erreurs et performance.

## Prérequis

* Compte Sentry (self-hosted ou SaaS)
* DSN (Data Source Name) fourni par Sentry
* Accès au dépôt et CI/CD si "releases" est utilisé

## Installation rapide

Remplacer `YOUR_DSN` par le DSN réel (ne pas le publier en clair).

JavaScript (browser) :

```bash
npm install @sentry/browser
```

Python :

```bash
pip install sentry-sdk
```

## Configuration générale

* Récupérer le DSN depuis le projet Sentry
* Configurer environnement (production, staging)
* Définir les releases (version de l'app)
* Filtrer les données sensibles (PII)

## Exemples d'initialisation par langage

JavaScript (Browser)

```javascript
import * as Sentry from "@sentry/browser";

Sentry.init({
    dsn: "https://<PUBLIC_KEY>@sentry.io/<PROJECT_ID>",
    environment: "production",
    release: "my-app@1.2.3",
    tracesSampleRate: 0.2, // pour performance
});
```

Node.js

```javascript
const Sentry = require("@sentry/node");
Sentry.init({ dsn: process.env.SENTRY_DSN, environment: "production" });
```

Python (Flask/Django/Generic)

```python
import sentry_sdk
from sentry_sdk.integrations.flask import FlaskIntegration

sentry_sdk.init(
        dsn="https://<PUBLIC_KEY>@sentry.io/<PROJECT_ID>",
        integrations=[FlaskIntegration()],
        environment="staging",
        release="backend@2.0.0"
)
```

Java (Spring Boot)

```java
// ajouter sentry-spring dependency, puis
Sentry.init(options -> {
    options.setDsn(System.getenv("SENTRY_DSN"));
    options.setEnvironment("production");
    options.setRelease("service@1.0.0");
});
```

## Concepts clés

DSN

* Chaîne utilisée par les SDK pour authentifier et adresser les événements vers le projet Sentry.

Environnements & Releases

* Environnement : "production", "staging", "development".
* Release : version de l'application utilisée pour associer erreurs et commits.

Breadcrumbs

* Petits indices (logs, requêtes) qui mènent à l'erreur. À enrichir (user actions, network).

Tags / Context / Scope

* Tags : paires clé/valeur pour filtrer et regrouper.
* Context : informations structurées (OS, runtime, custom).
* User : id, email pour identifier les utilisateurs affectés.

Grouping & Issues

* Sentry groupe les événements similaires en "issues". Configurable via fingerprinting.

Performance (Tracing)

* Suivi des transactions et spans. Configurer tracesSampleRate/tracesSampler.

## Alerting & Notifications

* Règles d'alerte basées sur events, frequency, regression, adoption.
* Intégrations : Slack, PagerDuty, Email, Webhooks. Exemple de règle : "Alerter si > 5 erreurs nouvelles en 5 minutes".

## Intégrations courantes

* Source maps (JS)
* GitHub/GitLab (releases, commits)
* Slack, Microsoft Teams
* APM frameworks (DB, HTTP clients)
* CI/CD pour upload des sourcemaps et releases

## Bonnes pratiques

* Ne pas logguer de données sensibles (PII).
* Utiliser releases et associer commits.
* Filtrer les erreurs non-actionnables (bots, healthchecks).
* Régler sample rate pour éviter des coûts élevés.
* Tester les intégrations (captureMessage, captureException).

## Sécurité et confidentialité

* Masquer/filtrer les champs sensibles via beforeSend ou transformations.
* Ne pas inclure de tokens/credentials dans le payload.
* Respecter la GDPR en anonymisant les données personnelles.

## Dépannage

* Vérifier que le DSN est correct.
* Contrôler la configuration réseau/proxy.
* Activer debug/logging SDK (ex : debug: true) pour voir en local.
* Vérifier quotas et ingestion dans Sentry.

## Tableau présentant les SDKs supportés et l'usage recommandé:

| Langage / Plateforme | SDK recommandé                | Usage principal             |
| -------------------- | ----------------------------- | --------------------------- |
| JavaScript (browser) | @sentry/browser               | Erreurs client & sourcemaps |
| Node.js              | @sentry/node                  | Backend, worker jobs        |
| Python               | sentry-sdk                    | Web frameworks, scripts     |
| Java                 | sentry-java / sentry-spring   | Applications JVM            |
| mobile (iOS/Android) | sentry-cocoa / sentry-android | Applications mobiles        |

## Exemples

Capturer une erreur manuelle (JS) :

```javascript
try {
    doSomething();
} catch (e) {
    Sentry.captureException(e);
}
```

Ajouter un tag (Python) :

```python
from sentry_sdk import configure_scope

with configure_scope() as scope:
        scope.set_tag("feature_flag", "new_checkout")
        scope.set_user({"id": "123"})
        # then capture
        sentry_sdk.capture_message("Test with tag")
```
