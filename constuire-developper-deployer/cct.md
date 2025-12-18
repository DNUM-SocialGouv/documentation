# ✅ Cadre de Cohérence Technique

## Caractère du référentiel

Ces exigences constituent un **cadre de cohérence technique obligatoire** pour garantir :

- La sécurité et la confidentialité des données
- La conformité aux obligations légales (RGPD, RGAA, RGS, souveraineté numérique)
- La maintenabilité et la pérennité des applications
- La qualité de service aux usagers

Chaque critère fournit un cadre opérationnel à appliquer lors de la conception, du développement, de la revue et du déploiement.

Les critères documentés sont fortement conseillés. Une dérogation est possible si justifiée et documentée.

## 1. Lisibilité et compréhension du code

Favoriser une compréhension rapide et homogène du code, sans règles lourdes, en appliquant les principes fondamentaux du clean code.

- **Nommage expressif** : Utiliser des noms explicites et cohérents (mots métier quand pertinent), éviter les abréviations obscures et centraliser les valeurs « magiques » dans des constantes pour rendre l'intention immédiatement visible en revue de code. Les noms de fonctions doivent être des verbes d'action clairs, les noms de classes des noms substantifs, et les booléens doivent être des questions posées (ex : `isValid`, `hasPermission`). Éviter les noms génériques (`data`, `temp`, `obj`) qui masquent l'intention réelle. Éviter les préfixes inutiles (ex : `strName`, `intAge`) qui n'apportent pas de valeur et nuisent à la lisibilité.
- **Principes DRY (Don't Repeat Yourself) et KISS (Keep It Simple, Stupid)** : Éliminer la duplication de code en extrayant les logiques communes dans des fonctions/classes réutilisables, tout en évitant la sur-abstraction prématurée (YAGNI - You Aren't Gonna Need It). Préférer la simplicité explicite à la complexité implicite ; si une solution complexe n'apporte pas de bénéfice mesurable, choisir la solution la plus simple qui fonctionne.
- **Fonctions et responsabilités uniques** : Écrire de courtes fonctions (≤ 50 lignes idéalement, max 100) centrées sur une responsabilité unique (Single Responsibility Principle), maintenir une profondeur d'imbrication ≤ 4 niveaux et éviter les « objets dieux » (> 500 lignes ou > 10 méthodes publiques) en scindant les rôles en composants simples et cohérents. Chaque fonction doit faire une seule chose et la faire bien, avec un niveau d'abstraction uniforme. Préférer peu d'arguments (idéalement ≤ 3) : si une fonction a trop de paramètres, elle fait probablement trop de choses. Utiliser des objets de paramètres pour regrouper les arguments liés. Éviter les flags (booléens) dans les paramètres : préférer deux fonctions claires plutôt qu'une fonction avec un booléen pour améliorer la lisibilité. Éviter les effets de bord cachés : une fonction ne doit pas modifier des variables globales ou des paramètres d'entrée sans que cela soit explicite dans son nom et sa signature.
- **Complexité maîtrisée** : Viser une complexité cyclomatique ≤ 10 par fonction en privilégiant des structures simples (early return, guard clauses, boucles claires) et un flux top‑down lisible afin de limiter la charge cognitive ; refactoriser systématiquement au-delà de ce seuil. Utiliser des techniques de réduction de complexité : extraction de méthodes, composition d'objets, remplacement de conditions par stratégies. Préférer la composition aux chaînes d'if/else : utiliser des objets de configuration et des fonctions spécialisées plutôt que des chaînes de conditions interminables pour améliorer la lisibilité et la maintenabilité. Encapsuler les conditions limites : centraliser la gestion des cas particuliers dans des fonctions dédiées plutôt que de les éparpiller dans le code, facilitant ainsi la maintenance et la compréhension. Préférer les conditions positives pour améliorer la lisibilité : éviter les conditions négatives au profit de conditions positives quand possible.
- **Code auto-documenté** : Écrire du code qui exprime clairement son intention sans nécessiter de commentaires pour comprendre le « quoi ». Le code doit être lisible comme une prose claire. Documenter uniquement le « pourquoi » via des commentaires concis lorsqu'une décision technique ou métier non-évidente nécessite une explication. Éviter les commentaires redondants qui répètent ce que le code fait déjà.
- **Documentation des APIs publiques** : Fournir une documentation structurée des APIs publiques (exemples d'usage, paramètres, retours, exceptions, pré/post-conditions) avec génération automatique via des outils adaptés au langage utilisé et maintien synchronisé avec le code. Les contrats d'interface doivent être clairs et explicites.

## 2. Architecture et structure du code

Structurer de façon simple et stable afin de faciliter l'évolution à coût maîtrisé.

- **Séparation des responsabilités** : Organiser une arborescence claire avec séparation des couches (présentation, métier, données) et des modules cohérents/autonomes pour faciliter la navigation et les changements localisés. Appliquer le principe de dépendance inversée (Dependency Inversion Principle) : les couches hautes ne doivent pas dépendre des couches basses, mais des abstractions communes.
- **Principes SOLID** :
  - **Single Responsibility Principle (SRP)** : Chaque classe/module doit avoir une seule raison d'être. Une classe ne doit gérer qu'un seul aspect de la fonctionnalité.
  - **Open/Closed Principle (OCP)** : Les entités doivent être ouvertes à l'extension, mais fermées à la modification. Utiliser la composition ou les mécanismes d'extension propres au langage pour étendre sans modifier le code existant.
  - **Liskov Substitution Principle (LSP)** : Les objets d'un type parent doivent pouvoir être remplacés par des instances de leurs types dérivés sans casser le comportement attendu.
  - **Interface Segregation Principle (ISP)** : Ne pas forcer les classes à implémenter des interfaces qu'elles n'utilisent pas. Créer des interfaces spécifiques et ciblées plutôt que des interfaces « god ».
  - **Dependency Inversion Principle (DIP)** : Quand possible, dépendre des abstractions (interfaces) plutôt que des implémentations concrètes. Les modules de haut niveau ne doivent pas dépendre des modules de bas niveau.
- **Principes Domain-Driven Design (DDD)** : Structurer le code autour du domaine métier pour améliorer la compréhension et la maintenabilité du code.
  - **Langage omniprésent (Ubiquitous Language)** : Utiliser systématiquement le vocabulaire métier dans le code, les conversations et la documentation. Les termes techniques doivent correspondre exactement aux concepts métier, favorisant une communication claire entre développeurs et experts métier.
  - **Contexte borné (Bounded Context)** : Délimiter clairement les frontières des modèles de domaine. Chaque contexte borné possède son propre modèle de domaine et son vocabulaire, évitant ainsi les ambiguïtés et les conflits de sens entre différents domaines.
  - **Entités et objets de valeur** : Distinguer les entités (objets identifiés par leur identité, même si leurs attributs changent) des objets de valeur (objets définis uniquement par leurs attributs, immuables et interchangeables). Les entités représentent des concepts métier avec un cycle de vie, tandis que les objets de valeur encapsulent des concepts métier sans identité propre.
  - **Agrégats (Aggregates)** : Regrouper des entités et objets de valeur en agrégats avec une racine d'agrégat qui garantit l'intégrité et la cohérence des invariants métier. Les agrégats délimitent les frontières de transaction et de cohérence, simplifiant ainsi la gestion des modifications et la persistance.
  - **Services de domaine (Domain Services)** : Identifier les opérations métier qui ne s'appartiennent naturellement ni à une entité ni à un objet de valeur. Ces services encapsulent des règles métier qui nécessitent la collaboration de plusieurs objets du domaine.
  - **Repositories (Repositories)** : Abstraire la persistance et l'accès aux données via des interfaces exprimées dans le langage du domaine. Les repositories masquent les détails techniques de la persistance et permettent de raisonner en termes métier lors de la récupération et de la sauvegarde des agrégats.
  - **Événements de domaine (Domain Events)** : Modéliser les événements significatifs qui se produisent dans le domaine métier. Ces événements permettent de découpler les parties du système et de synchroniser les différents contextes bornés ou les systèmes externes.
  - **Couche anti-corruption (Anti-Corruption Layer)** : Isoler le domaine métier des systèmes externes ou des contextes voisins en créant une couche de traduction qui transforme les modèles externes en modèles du domaine, préservant l'intégrité du modèle métier.
- **Patterns et abstractions pragmatiques** : Appliquer des patterns simples et consistants ; n'introduire des abstractions (interfaces, ports/adapters) que lorsqu'elles apportent un bénéfice concret (testabilité, évolutivité, réduction du couplage). Éviter la sur-ingénierie : ne pas créer d'abstractions « au cas où » (YAGNI), mais uniquement quand le besoin réel est identifié. **Préférence pour les objets de valeur** : Plutôt que de manipuler des types primitifs partout, créer des objets de valeur pour encapsuler la logique métier et améliorer la sémantique du code. Un objet de valeur représente un concept métier avec ses opérations associées plutôt que d'utiliser des variables primitives séparées.
- **Encapsulation des détails internes** : Exposer seulement ce qui est nécessaire pour l'utilisation du module. Cacher les détails d'implémentation et les fonctions internes pour maintenir une interface claire et stable. Ne pas exposer les fonctions internes qui doivent rester privées au module.
- **Couplage faible et cohésion forte** : Maintenir un couplage faible entre modules et une cohésion forte au sein des modules. La cohésion mesure la force de la relation entre les éléments d'un module : viser une cohésion fonctionnelle (tous les éléments contribuent à une seule fonction) ou séquentielle (sortie d'un élément = entrée du suivant). Détecter et éviter les cycles de dépendances via des outils automatisés avec échec CI si cycles détectés, afin de simplifier les refactorings et éviter la dégradation progressive. **Loi de Déméter** : Une fonction ne doit connaître que ses dépendances directes, pas les dépendances de ses dépendances. Éviter les chaînes d'appels profondes et préférer des fonctions dédiées ou des méthodes déléguées pour améliorer le couplage et la maintenabilité.
- **Configuration et versionnement** : Externaliser configuration et secrets par environnement avec validation de schéma au démarrage ; stabiliser et versionner les APIs exposées (sémantique majeur.mineur.patch) avec dépréciation progressive (warnings, délai d'adaptation) pour limiter les ruptures contractuelles et maintenir la compatibilité ascendante.
- **Documentation architecturale** : Documenter l'architecture via des diagrammes C4 (Context, Container, Component, Code) maintenus à jour pour les décisions structurantes, facilitant l'onboarding et les évolutions majeures.
- **Structure du code source** : Regrouper verticalement ce qui est lié : les concepts liés doivent être proches dans le code pour faciliter la compréhension. Déclarer les variables près de leur usage : réduire la portée des variables au minimum nécessaire pour améliorer la lisibilité et éviter les erreurs. Préférer l'immutabilité quand le langage le permet et éviter les déclarations de variables en début de fonction si elles ne sont utilisées que plus tard.

## 3. Base de données et persistance

Assurer une persistance fiable avec des choix simples adaptés au volume et aux usages.

- Pas de NoSQL : définir des contraintes d'intégrité explicites (PK, FK, UNIQUE, CHECK) et créer des index sur les requêtes fréquentes en analysant les query plans, avec une revue périodique (trimestrielle) pour éviter les index inutiles ou redondants ; monitorer les requêtes lentes (> 100ms) avec des outils dédiés (pg_stat_statements, MySQL slow query log, APM).
- Utiliser un ORM pour la plupart des requêtes ; utiliser systématiquement des requêtes préparées/paramétrées pour prévenir les injections SQL, éviter SELECT \* en sélectionnant explicitement les colonnes nécessaires, et prévenir N+1 via jointures ou chargements adaptés (eager/lazy) selon le besoin de données réel ; logger et analyser les requêtes générées par l'ORM en développement.
- Gérer des migrations versionnées, réversibles et idempotentes (Flyway, Liquibase, TypeORM migrations, Alembic), testées sur des échantillons réalistes et des copies de production anonymisées ; maintenir des schémas rigoureusement alignés entre tous les environnements et interdire les modifications manuelles de schéma.
- Définir une politique de transactions explicite : utiliser les niveaux d'isolation appropriés, gérer les rollbacks automatiques sur erreur, et limiter la durée des transactions pour éviter les locks prolongés.
- Classifier les données selon leur sensibilité (publiques, internes, confidentielles, sensibles/personnelles) et appliquer des mesures de protection graduées : les données sensibles doivent être chiffrées au repos au niveau colonne (AES-256 minimum) ; pseudonymiser ou anonymiser systématiquement les données personnelles dans les environnements de développement et test.
- Mettre en place un masquage automatique des données sensibles dans les logs, messages d'erreur et interfaces de débogage ; interdire l'accès direct aux données de production depuis les environnements de développement, sauf demande explicite et tracée, et mettre en place des mécanismes d'audit pour tout accès aux données sensibles.
- Chiffrer les échanges (TLS en transit) et les données sensibles au repos (chiffrement au niveau colonne si nécessaire), utiliser des comptes à privilèges minimaux avec rotation régulière (trimestrielle minimum) des identifiants ; réaliser des sauvegardes automatiques périodiques (quotidiennes pour prod) avec tests de restauration mensuels et conservation selon politique définie.

## 4. Sécurité applicative

Mettre en place des protections de base efficaces, adaptées à l'exposition du service.

- Mettre en place une authentification robuste (OAuth2/OIDC, JWT avec rotation, sessions sécurisées) avec politique de mots de passe forte (longueur minimale 12 caractères, complexité, sans rotation forcée selon NIST) et MFA obligatoire pour les comptes administrateurs ; gérer correctement les sessions (durées adaptées, invalidation explicite, protection contre fixation) ainsi que des contrôles d'accès côté serveur fondés sur le moindre privilège (RBAC ou ABAC).
- Valider systématiquement toutes les entrées (whitelist plutôt que blacklist, validation de type et format), encoder les sorties selon le contexte (HTML, JS, URL, SQL), activer les protections essentielles (anti-XSS, tokens CSRF, sanitization), et utiliser des bibliothèques éprouvées (DOMPurify, OWASP libraries) ; servir exclusivement en HTTPS sur tous les environnements publics avec redirections automatiques.
- Gérer les secrets via variables d'environnement/coffre et proscrire tout secret en clair dans le code, la configuration et les journaux.
- Activer les en-têtes de sécurité essentiels (`Content-Security-Policy strict`, `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, `Strict-Transport-Security` avec `preload`, `Referrer-Policy: strict-origin-when-cross-origin`), une politique CORS restrictive (whitelist explicite des origines autorisées) et un rate limiting adapté (par IP, par endpoint, par utilisateur) pour réduire l'exposition aux attaques automatisées et DDoS.
- Mettre en place une matrice d'habilitations régulièrement auditée : documenter qui a accès à quoi, avec quel niveau de privilège et pour quelle durée ; implémenter une revue trimestrielle des accès avec révocation des comptes inactifs et traçabilité des modifications d'habilitations.
- Maintenir un inventaire des dépendances tierces avec scan automatique de vulnérabilités (Snyk, OWASP Dependency-Check) et application rapide des patches de sécurité (sous 48h pour vulnérabilités critiques).

## 5. Fiabilité et résilience

Viser une fiabilité raisonnable avec des mécanismes simples à opérer.

- Mettre en place un logging structuré pour tracer les événements métiers critiques et faciliter le diagnostic :
  - Utiliser un format JSON en déploiement et un format lisible en local pour faciliter le développement.
  - Tracer systématiquement les événements métiers critiques : authentifications (réussies/échouées avec la cause), toutes les actions de consultation/modification/suppression de données, et autres opérations sensibles.
  - Inclure dans chaque ligne de log un request_id (généré côté front pour les requêtes utilisateur, par un autre micro-service ou par un middleware côté back pour les appels API directs), ainsi que le chemin du fichier et le numéro de ligne pour faciliter le débogage.
  - Logger les tracebacks originaux en les capturant avant toute transformation par des blocs try/catch, afin de conserver la stack trace complète.
  - Configurer les access logs du serveur web/reverse proxy (ex. Nginx, Traefik) en deux lignes : une première avec méthode HTTP, URL, referrer, headers (en nettoyant le header d'authentification), une seconde avec les mêmes informations plus la durée de la requête.
- Mettre en place un wrapper unifiant log et remontée vers Sentry pour les niveaux >= ERROR : chaque action de logging doit créer une ligne de log locale et envoyer l'information vers Sentry (avec tout le contexte : request_id, stack trace, variables d'environnement pertinentes) afin de centraliser le suivi des erreurs critiques.
- **Gestion des erreurs** : Séparer la logique métier de la gestion des erreurs : ne pas mélanger la logique principale avec la gestion des erreurs. Utiliser des exceptions plutôt que des codes d'erreur : les exceptions sont plus expressives et plus faciles à gérer que les codes d'erreur retournés. Ajouter du contexte aux exceptions : les messages d'erreur doivent être informatifs et inclure le contexte nécessaire pour comprendre et résoudre le problème plutôt que des messages génériques. Éviter les valeurs nulles pour les concepts métier : utiliser des valeurs explicites plutôt que des valeurs nulles pour représenter des concepts métier, selon les mécanismes disponibles dans le langage utilisé.
- Définir des timeouts explicites pour toutes les opérations I/O (appels API, BDD, services externes) avec valeurs adaptées au contexte (ex : 5s pour API synchrone, 30s pour opérations lourdes) ; implémenter des retries avec backoff exponentiel (ex : 3 tentatives max avec délais 1s, 2s, 4s) et jitter pour éviter les retry storms ; mettre en place des circuit breakers pour isoler les services défaillants et éviter la propagation de pannes.
- Prévoir une dégradation gracieuse (fallback sur cache, fonctionnalité réduite, messages utilisateur explicites) pour éviter les pannes totales et maintenir une expérience utilisateur acceptable même en mode dégradé.
- Exposer des health checks distincts (liveness pour redémarrage, readiness pour traffic) avec vérification des dépendances critiques (BDD, services externes) ; collecter et exposer des métriques essentielles (taux d'erreur, latence p50/p95/p99, throughput) avec des dashboards opérationnels. Définir des SLO (Service Level Objectives) mesurables (ex: 99.9% uptime, p95 < 500ms) et des SLI (Service Level Indicators) pour les suivre.
- Déclencher des alertes progressives : warnings pour déviations mineures, critiques pour incidents majeurs avec escalade automatique si non traité ; éviter le sur-alerting en définissant des seuils pertinents et en regroupant les alertes corrélées.
- Réaliser des sauvegardes périodiques et tester la restauration afin d'assurer un redémarrage maîtrisé en cas d'incident.

## 6. Performance et efficacité

Optimiser les ressources serveur et client par des pratiques techniques ciblées pour éviter les goulets d'étranglement courants.

- Mesurer systématiquement avec des outils d'APM (ex. Sentry Performance Monitoring, Elastic APM, Tempo) avant de se lancer dans des optimisations : profiler les opérations critiques (temps de réponse, requêtes lentes, utilisation mémoire) pour identifier les vrais goulets d'étranglement et valider les gains après refactoring, en évitant les optimisations prématurées. Définir des budgets de performance par endpoint (ex : API < 200ms p95, pages < 1s LCP) avec monitoring continu.
- Éviter les problèmes de requêtes N+1 en utilisant des jointures appropriées, des eager loading ou des batch loads selon l'ORM/framework utilisé (TypeORM/Prisma pour Node/TypeScript avec relations/findMany include, JPA/Hibernate pour Spring Boot avec @EntityGraph ou FetchType.EAGER), et en analysant les requêtes SQL générées pour détecter les patterns problématiques.
- Implémenter la pagination au niveau SQL (LIMIT/OFFSET ou curseurs) plutôt qu'en mémoire dans le backend, et à fortiori jamais côté frontend : charger uniquement les données nécessaires à la page demandée et transmettre les métadonnées de pagination (total, page courante) pour une navigation efficace.
- Sélectionner explicitement les colonnes nécessaires (éviter SELECT \*), analyser les plans d'exécution pour détecter les scans complets de table, et créer des index adaptés aux patterns de requêtes fréquentes (composite indexes pour WHERE multi-colonnes, couvrant pour éviter les lookups).
- Ajouter un cache simple et ciblé sur les points chauds identifiés (données lues fréquemment, résultats de calculs coûteux) avec une stratégie d'expiration explicite (TTL adapté au contexte) et des mécanismes d'invalidation adaptés (event-driven, write-through, cache aside) ; utiliser Redis/ioredis pour Node/TypeScript ou Spring Cache avec Redis/Caffeine pour Java/Spring Boot. Monitorer le hit ratio du cache (objectif > 80%) et ajuster la stratégie si nécessaire.
- Configurer un connection pooling approprié pour la base de données (taille min/max adaptée à la charge, timeout de connexion, idle timeout) et les clients HTTP pour les services externes afin d'éviter l'overhead de création de connexions répétées.
- Activer la compression des réponses HTTP (gzip, brotli) pour les contenus textuels (JSON, HTML, CSS, JS) avec seuils appropriés (> 1KB) ; utiliser HTTP/2 ou HTTP/3 quand possible pour réduire la latence.
- Optimiser côté client : maîtriser la taille des bundles (code splitting, tree-shaking), activer le lazy-loading des ressources lourdes et optimiser les images (formats modernes, compression) pour améliorer les temps de chargement perçus.
- Prévoir une architecture scalable (composants stateless, équilibrage de charge, scaling horizontal) lorsque la charge ou la criticité l'exige, avec monitoring pour déclencher les actions de scale.

## 7. Tests et qualité logicielle

Assurer une couverture de tests rigoureuse pour garantir la fiabilité et éviter les régressions, en appliquant les principes du clean code pour les tests (Clean Code Tests).

- **Pyramide des tests et stratégie** : Appliquer la pyramide des tests (unitaires, tests d'intégration, tests E2E) pour équilibrer vitesse d'exécution et confiance ; viser une couverture ≥ 90% sur le code partagé, la logique métier et l'authentification avec des tests unitaires rapides (< 10ms par test) et isolés. Ces zones critiques doivent être exhaustivement testées (scénarios nominaux, cas limites, cas d'erreur) avec des frameworks adaptés au langage et à l'écosystème technique utilisé.
- **Clean Code pour les tests** :
  - **Tests clairs et expressifs** : Les tests doivent être lisibles comme une documentation vivante. Utiliser des noms de tests descriptifs qui expliquent le comportement testé plutôt que des noms génériques. Suivre le pattern Arrange-Act-Assert (AAA) ou Given-When-Then pour structurer les tests de manière claire.
  - **Un seul concept par test** : Chaque test doit vérifier une seule chose. Éviter les tests qui vérifient plusieurs comportements à la fois, ce qui rend difficile l'identification de la cause d'un échec.
  - **Tests rapides et indépendants** : Les tests unitaires doivent être rapides (< 10ms) et ne pas dépendre les uns des autres. Ils doivent pouvoir s'exécuter dans n'importe quel ordre et être isolés (pas de dépendances partagées, pas d'état global).
  - **FIRST principles** : Les tests doivent être **Fast** (rapides), **Independent** (indépendants), **Repeatable** (répétables), **Self-Validating** (auto-vérifiants avec des assertions claires), **Timely** (écrits au bon moment, idéalement avant le code - TDD).
- **Tests de non-régression** : Mettre en place des tests de non-régression complets couvrant les parcours utilisateurs principaux, les scénarios d'intégration entre composants et les cas d'usage métiers critiques, avec une exécution automatique en CI pour détecter rapidement les régressions.
- **Tests d'intégration** : Écrire des tests d'intégration couvrant les interactions avec les APIs, la base de données et les services tiers, en utilisant des environnements de test isolés et reproductibles (Docker, Testcontainers) avec données de test cohérentes. Utiliser des fixtures réutilisables et des factories pour créer des données de test de manière maintenable.
- **Tests E2E** : Mettre en place des tests E2E critiques (Playwright, Cypress) sur les parcours métiers essentiels, exécutés sur environnements staging pré-production ; maintenir ces tests stables (< 5% de flakiness) avec stratégies de retry intelligentes et isolation des tests. Garder le nombre de tests E2E limité et ciblés sur les parcours critiques pour maintenir leur maintenabilité.
- **Sécurité et dépendances** : Intégrer des analyses SAST et des scans de dépendances dans la CI, pour détecter tôt les failles de sécurité et les bibliothèques vulnérables.
- **Tests de charge** : Réaliser des tests de charge (k6 recommandé pour sa simplicité et scriptabilité JS) sur les scénarios sensibles à la performance pour prévenir les régressions : définir des seuils acceptables (throughput, latence p95, taux d'erreur) et faire échouer la CI si dépassement. Exécuter des tests de charge complets en pré-production pour valider la scalabilité.

## 8. Analyse statique et outillage

Mettre en place des garde‑fous automatisés pour maintenir la qualité et détecter précocement les problèmes, en intégrant des métriques de clean code et des détections automatiques de code smells.

- **Linting et formatage** : Configurer des linters avec des règles adaptées au langage et faire échouer la CI de façon systématique sur les erreurs bloquantes (formatage, sécurité, bonnes pratiques) ; les avertissements doivent être traités progressivement, mais ne bloquent pas le déploiement. Mettre en place des hooks pre-commit pour appliquer automatiquement le formatage et bloquer les commits non conformes. Configurer des règles spécifiques pour détecter les violations de clean code (noms génériques, fonctions trop longues, complexité excessive).
- **Métriques de clean code** :
  - **Complexité cyclomatique** : Maintenir une complexité cyclomatique ≤ 10 par fonction (15 maximum acceptable) avec alertes automatiques en cas de dépassement. Utiliser des outils d'analyse (SonarQube, CodeClimate) pour suivre cette métrique et identifier les fonctions à refactoriser.
  - **Duplication de code** : Maintenir une duplication de code ≤ 3% avec détection automatique des blocs dupliqués. Identifier et extraire les patterns répétitifs en fonctions réutilisables.
  - **Couverture de tests** : Viser une couverture ≥ 90% sur le code critique avec monitoring continu. Les outils doivent identifier les zones non couvertes et alerter en cas de baisse de couverture.
  - **Longueur des fonctions/classes** : Détecter automatiquement les fonctions > 100 lignes et les classes > 500 lignes ou avec > 10 méthodes publiques (code smells « God Object ») avec alertes en CI.
  - **Profondeur d'imbrication** : Détecter les blocs avec une profondeur d'imbrication > 4 niveaux et suggérer des refactorings (extraction de méthodes, early returns).
  - **Paramètres de fonctions** : Alerter sur les fonctions avec > 5 paramètres et suggérer l'introduction de paramètres d'objets (refactoring « Introduce Parameter Object »).
- **Vérification stricte des types et code mort** : Activer la vérification stricte des types quand le langage le permet et éliminer régulièrement le code mort via des outils automatisés adaptés au langage utilisé.
- **Détection de code smells** : Configurer des outils d'analyse de code pour détecter automatiquement les code smells courants :
  - Longues méthodes
  - Classes trop grandes (God Object)
  - Duplication de code
  - Paramètres trop nombreux
  - Dépendances circulaires
  - Noms génériques ou non expressifs
  - Commentaires morts ou code commenté
- **Sécurité et dépendances** : Intégrer un scan automatisé des dépendances via des outils adaptés au gestionnaire de dépendances utilisé et des secrets dans la CI avec échec sur vulnérabilités critiques ; suivre les métriques de qualité (couverture de tests, duplication de code) avec des alertes sur dérive.
- **Analyses SAST** : Configurer des analyses SAST (SonarQube, CodeQL, Semgrep) pour détecter les vulnérabilités et failles de sécurité dans le code, avec rapports CI lisibles et intégration dans le workflow de revue. Exécuter ces analyses à chaque commit/PR ; planifier des revues qualité hebdomadaires ou mensuelles selon la criticité du projet.
- **Documentation des suppressions** : Documenter les suppressions justifiées de warnings/erreurs via commentaires inline avec référence au ticket associé ; réviser périodiquement ces suppressions pour éviter l'accumulation de dette technique masquée. Mettre en place un processus de revue trimestrielle des suppressions pour identifier celles qui peuvent être corrigées.
- **Rapports de qualité** : Produire des rapports de qualité automatisés avec tendances historiques et générer des alertes en cas de dérive notable pour concentrer l'effort correctif là où il est le plus utile. Les rapports doivent inclure les métriques de clean code (complexité, duplication, longueur des fonctions/classes) avec des visualisations claires et des recommandations d'actions.

## 9. Déploiement et conteneurisation

Standardiser et sécuriser le build et le déploiement via une automatisation fiable et reproductible.

- Construire des images Docker optimisées (multi‑stage pour réduire la taille, .dockerignore pour exclure les fichiers inutiles) et exécuter systématiquement les conteneurs en utilisateur non‑root avec des privilèges minimaux ; scanner les images pour vulnérabilités (Trivy, Clair) avant déploiement. Appliquer l'immutabilité : interdire les modifications in-place, versionner avec tags sémantiques + SHA de commit, conserver les N dernières versions pour rollback rapide.
- Mettre en place un pipeline CI/CD complet qui automatise build, tests, analyse de sécurité et déploiement, avec des étapes conditionnelles selon l'environnement et une capacité de rollback rapide et testée en cas d'incident ; versionner les configurations de déploiement (Helm charts, Terraform, etc.). Maintenir une parité maximale entre environnements (dev, staging, production) et tester systématiquement migrations et déploiements en staging avant production.
- Définir une stratégie de déploiement adaptée au contexte. Configurer des health checks (liveness, readiness, startup probes) et définir explicitement resource limits et requests (CPU, mémoire) pour éviter les saturations et OOM.
- Centraliser les journaux applicatifs et système via des outils dédiés (ELK, Loki, CloudWatch) et collecter des métriques essentielles (CPU, mémoire, latence, taux d'erreur) avec des dashboards opérationnels pour une visibilité en temps réel.
- Gérer les secrets de façon sécurisée via des variables d'environnement chiffrées ou un coffre (Vault) .

## 10. Optimisation front‑end

Optimiser le front pour garantir une expérience utilisateur fluide et sécurisée.

- Maîtriser la taille des bundles via code splitting intelligent (par route, par fonctionnalité), minification et tree-shaking, en limitant les dépendances volumineuses et en utilisant des alternatives légères quand possible ; analyser régulièrement la composition des bundles (webpack-bundle-analyzer, source-map-explorer pour React/Webpack et Angular) pour identifier les opportunités d'optimisation. Définir des budgets de performance en CI (taille max des bundles) avec échec automatique en cas de dépassement.
- Activer le lazy‑loading systématique pour les ressources lourdes (images, composants non critiques, données) et optimiser les images avec des formats modernes (WebP, AVIF) et une compression appropriée ; implémenter le responsive images (srcset, sizes) pour adapter la charge selon les devices. Prioriser le critical path : CSS critique inline, preload des fonts critiques, skeleton screens pour chargements longs.
- Mesurer et monitorer les Core Web Vitals en continu : LCP (Largest Contentful Paint) < 2.5s, FID (First Input Delay) < 100ms, CLS (Cumulative Layout Shift) < 0.1. Mettre en place un monitoring RUM (Real User Monitoring) pour mesurer les performances réelles en production et configurer des alertes automatiques sur dégradation.
- Implémenter une stratégie de cache HTTP efficace (assets immutables avec hash de contenu, cache busting) et utiliser un CDN pour les ressources statiques. Évaluer l'intérêt des Service Workers pour offline-first ou amélioration des performances selon le contexte applicatif.
- Respecter strictement un HTML sémantique (balises appropriées, structure hiérarchique), fournir des métadonnées complètes (Open Graph, Twitter Cards, meta description) et utiliser les attributs ARIA de façon appropriée pour une accessibilité fiable ; tester régulièrement avec des lecteurs d'écran et des outils automatisés.
- Combiner les tests E2E et accessibilité RGAA via Playwright + @axe-core/playwright ou playwright-lighthouse pour valider simultanément le fonctionnement et la conformité sur les parcours critiques.
- Appliquer une Content Security Policy (CSP) stricte avec whitelisting des sources autorisées et configurer des cookies sécurisés (HttpOnly, Secure, SameSite) ; servir systématiquement l'application en HTTPS sur tous les environnements publics avec HSTS activé.

## 11. Collaboration et maintenabilité

Encadrer les pratiques d'équipe pour favoriser la pérennité et la transmission de connaissances, en appliquant les principes du clean code pour la maintenabilité et le refactoring continu.

- **Documentation maintenue** : Maintenir une documentation à jour et accessible : README complet avec instructions d'installation/déploiement, documentation des APIs (OpenAPI/Swagger), diagrammes d'architecture pour les décisions clés, et changelog régulier pour suivre l'évolution ; la documentation doit être revue et mise à jour lors des changements majeurs. Maintenir des ADR (Architecture Decision Records) pour toutes les décisions architecturales majeures, avec contexte, options considérées, décision prise et conséquences anticipées.
- **Revue de code et collaboration** : Pratiquer systématiquement la revue de code avec au moins un relecteur pour chaque PR, des conventions de branches (GitFlow, GitHub Flow) et de commits standardisés (Conventional Commits) pour garder un historique clair, des PRs descriptives avec contexte et tests associés. Créer et maintenir un glossaire métier partagé (termes métiers et techniques) versionné avec le code. Les revues de code doivent vérifier non seulement la fonctionnalité, mais aussi l'application des principes de clean code (nommage, simplicité, testabilité).
- **Refactoring continu** :
  - **Boy Scout Rule** : Laisser le code dans un meilleur état qu'on ne l'a trouvé. Chaque modification doit améliorer légèrement la qualité du code, même si ce n'est pas l'objectif principal de la tâche.
  - **Refactoring par petites étapes** : Refactoriser régulièrement par petites étapes plutôt que par grandes réécritures. Chaque refactoring doit être accompagné de tests pour garantir qu'aucune régression n'est introduite.
  - **Dette technique maîtrisée** : Éviter l'accumulation de dette technique en refactorisant au fur et à mesure. Quand une dette technique est identifiée, la documenter et la planifier dans le backlog avec une estimation d'effort. Ne pas laisser s'accumuler les « quick fixes » et les « workarounds » qui deviennent des problèmes structurels.
  - **Code smells et refactoring** : Identifier et corriger les code smells courants (longues méthodes, classes trop grandes, duplication, paramètres trop nombreux, dépendances circulaires) via des refactorings ciblés (extraction de méthodes, extraction de classes, introduction de paramètres d'objets, etc.).
- **Gestion des dépendances** : Gérer activement les dépendances : appliquer immédiatement les security patches, planifier mensuellement les mises à jour mineures et trimestriellement les majeures ; automatiser avec dependabot/renovate en conservant une revue humaine systématique.
- **Partage de connaissances** : Limiter le bus factor par partage systématique des connaissances critiques : sessions régulières de knowledge sharing (démos, tech talks), documentation d'onboarding complète avec checklist, rotation des responsabilités sur les composants sensibles. Organiser des sessions de code review collective et de pair programming pour partager les bonnes pratiques de clean code.
- **Gestion des tickets et dette technique** : Tenir un suivi rigoureux des tickets (bugs, features, améliorations) avec priorités, échéances et statuts à jour ; tracer les dettes techniques dans un backlog dédié avec planification et estimation d'effort pour leur résolution progressive. Allouer régulièrement du temps (ex : 10-20% du temps de développement) pour le refactoring et l'amélioration continue.
- **Post-mortems et apprentissage** : Conduire des post-mortems blameless après chaque incident majeur : analyse des causes racines, actions correctives documentées, partage public si pertinent pour favoriser la transparence et l'apprentissage collectif.
- **Licences et contributions** : Documenter explicitement les licences de tous les composants (code source, dépendances) et fournir un guide de contribution clair si le dépôt est partagé ou ouvert, avec une politique de sécurité (déclaration de vulnérabilités) et un code de conduite pour encadrer les contributions. Le guide de contribution doit inclure les standards de clean code attendus dans le projet.

## 12. Conformité et réglementation

Respecter rigoureusement les obligations légales et sectorielles applicables aux services publics numériques français.

- RGPD : implémenter des mécanismes complets et vérifiables de consentement éclairé, de droit à l'oubli (suppression effective des données dans tous les systèmes et backups), de portabilité (export dans un format structuré standard) et de rectification, avec traitement des demandes dans les délais légaux (maximum 1 mois) et traçabilité des actions réalisées. Maintenir un registre des traitements à jour (Article 30 RGPD).
- Gestion des incidents RGPD : définir et tester une procédure de notification CNIL sous 72h en cas de violation de données, avec notification des personnes concernées si risque élevé ; préparer un template de notification prêt à l'emploi et désigner les responsables de la chaîne d'alerte.
- Sous-traitance et tiers : établir des DPA (Data Processing Agreement) obligatoires avec tous les sous-traitants traitant des données personnelles, incluant clauses de réversibilité et portabilité ; auditer périodiquement les sous-traitants sur leurs pratiques de sécurité et conformité.
- Accessibilité RGAA : viser systématiquement le niveau AA à 100% de conformité, en combinant tests automatisés réguliers (axe-core, lighthouse, WAVE). Voir [la page dédiée](../concevoir/accessibilite.md) pour plus de détails.
- Traçabilité réglementaire : mettre en place une journalisation exhaustive des opérations sensibles (authentifications, accès aux données personnelles, modifications critiques) avec horodatage fiable, conservation selon les durées légales et possibilité d'audit ; définir et communiquer une politique de conservation claire avec procédures de purge documentées.
- RGS (Référentiel Général de Sécurité) : voir la politique de sécurité du ministère.
- Archivage légal : implémenter un système d'archivage à valeur probante pour les documents et données soumis à obligations légales de conservation (signature électronique qualifiée, horodatage qualifié, empreintes cryptographiques SHA-256 minimum) ; respecter les durées de conservation selon le Code du patrimoine (5 ans minimum pour archives publiques) et les textes sectoriels applicables.
- Open data : pour les données publiques réutilisables, prévoir dès la conception leur extraction et publication en formats ouverts (CSV, JSON, XML) conformément à la loi pour une République numérique et au Code des relations entre le public et l'administration ; documenter les métadonnées selon le standard DCAT-AP et publier sur data.gouv.fr ou portail sectoriel approprié.
- Formation et sensibilisation : organiser une formation RGPD obligatoire pour toute l'équipe (renouvellement annuel) et une sensibilisation continue à la sécurité (phishing tests, newsletters, retours d'expérience sur incidents) pour maintenir une culture de vigilance.

## 13. Technologies recommandées

Ce cadre technique recommande les stacks **Node.js/React (TypeScript)** et **Java/Spring Boot** comme stacks de référence pour tous les nouveaux projets de développement d'applications web. Ces stacks sont préconisées car elles offrent une forte agilité, une productivité élevée et un écosystème moderne adapté au développement rapide d'applications web.

Le choix entre les deux stacks se fera par le Ministère.

### Stack Node.js/React

| Catégorie              | Technologies                                                                                                                  |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **Runtime/Langage**    | Node.js (LTS, version 22 minimum)<br>TypeScript (version 5+ avec configuration stricte)                                       |
| **Framework Backend**  | Hono (typage et validation des routes partagés via client RPC)                                                                |
| **Base de données**    | PostgreSQL avec Prisma<br>Migrations de base de données via l'ORM                                                             |
| **Validation**         | Zod ou class-validator                                                                                                        |
| **Authentification**   | ProConnect (OAuth2/OIDC) / JWT                                                                                                |
| **Documentation API**  | OpenAPI/Swagger automatique                                                                                                   |
| **Tests backend**      | Vitest (TU), Supertest et Testcontainers (TI)                                                                                 |
| **Linting/Analyse**    | ESLint (règles TypeScript strictes), Prettier, Biome                                                                          |
| **Framework Frontend** | React 18+ avec TypeScript ou Next.js 14+ pour le SSR/SSG                                                                      |
| **État Frontend**      | TanStack Query (React.js)<br>Pinia (Vue.js)                                                                                   |
| **Styling Frontend**   | DSFR, via [lib react-ds](https://github.com/codegouvfr/react-dsfr)<br>Tailwind CSS ou CSS Modules avec approche utility-first |
| **Tests Frontend**     | Vitest + React Testing Library pour les tests unitaires<br>Playwright pour les tests E2E                                      |
| **Build Frontend**     | Vite ou Next.js (React - préconisé)<br>Vite                                                                                   |
| **Dépendances**        | Yarn                                                                                                                          |
| **CI/CD**              | PIC interne (Gitlab)                                                                                                          |
| **Conteneurisation**   | Docker avec images multi-stages optimisées basées sur Node.js slim                                                            |
| **Monitoring**         | Sentry (Erreurs et APM), Outil pour les logs                                                                                  |
| **Logging**            | Pino                                                                                                                          |

### Stack Java/Spring Boot

| Catégorie              | Technologies                                                                                                                 |
| ---------------------- |------------------------------------------------------------------------------------------------------------------------------|
| **Langage**            | Java 21 ou 25 (LTS)<br>avec records, pattern matching avec Temurin (OpenJDK)                                                 |
| **Framework Backend**  | Spring Boot 3.x+ ou 4 avec Spring Framework 6.x+ ou 7<br>Architecture en couches via Spring Data et Spring Security          |
| **Base de données**    | PostgreSQL avec Spring Data JPA et Hibernate comme ORM<br>Liquibase pour les migrations de base de données                   |
| **Validation**         | Bean Validation (Jakarta Validation) avec annotations                                                                        |
| **Authentification**   | Spring Security avec ProConnect (OAuth2/OIDC) et JWT pour les APIs stateless<br>JWT dans les cookies                         |
| **Documentation API**  | SpringDoc OpenAPI (Swagger) pour la documentation automatique des APIs REST                                                  |
| **Tests**              | JUnit 5 et/ou Assert4j et Mockito<br>Spring Boot Test avec @SpringBootTest<br>Testcontainers pour les tests avec dépendances |
| **Linting/Analyse**    | Checkstyle, PMD, SpotBugs pour la détection de code smells et vulnérabilités                                                 |
| **Framework Frontend** | Angular avec TypeScript                                                                                                      |
| **État Frontend**      | Signals Angular (gestion réactive moderne) et Services Angular                                                               |
| **Styling Frontend**   | DSFR via [lib ngx-dsfr](https://www.npmjs.com/package/@edugouvfr/ngx-dsfr)<br>Tailwind CSS                                   |
| **Tests Frontend**     | Jest ou Jasmine + Karma pour les tests unitaires<br>Playwright pour les tests E2E                                            |
| **Build Frontend**     | Angular CLI (build intégré)                                                                                                  |
| **Dépendances/Build**  | Maven/Gradle avec wrapper pour garantir la version                                                                           |
| **CI/CD**              | PIC interne (GitLab CI)                                                                                                      |
| **Conteneurisation**   | Docker avec images multi-stages optimisées basées sur OpenJDK Alpine                                                         |
| **Monitoring**         | Sentry (Erreurs et APM), Outil pour les logs                                                                                 |
| **Logging**            | Logback ou Log4j2 avec SLF4J pour le logging structuré (format JSON en production)                                           |
