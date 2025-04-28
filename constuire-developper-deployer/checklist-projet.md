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
    visible: false
---

# Checklist projet

Tous les projets doivent :&#x20;

* [ ] Être [open source](open-source.md)
* [ ] Se récupérer avec `git checkout ...`
* [ ] S'exécuter avec `docker compose up (-d)`



Voici ce que contiennent nos projets :&#x20;

* [ ] Pour la documentation :
  * [ ] Le `README.md`, synthétisant ce que fait l'application, ainsi que des liens pertinents au projet
  * [ ] `CONTRIBUTING.md`&#x20;
  * [ ] [`LICENCE(.txt)`](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository), voir [ici](https://www.data.gouv.fr/fr/pages/legal/licences/) pour la liste des licences
  * [ ] Un dossier `doc(s)` pour les documents techniques (choix de conception, ADRs, conventions spécifiques à l'équipe, etc.)
* [ ] Des fichiers liés à Git :&#x20;
  * [ ] `.gitignore`
  * [ ] Un dossier `.github` avec les workflows du projet, et/ou des templates d'[issues](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/manually-creating-a-single-issue-template-for-your-repository) et [PRs](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)
* [ ] Des fichiers liés à la conteneurisation du projet, pour une exécution locale :
  * [ ] Les fichiers liés à Docker : `docker-compose.yml` et `Dockerfile` dans chaque partie applicative (front, back)
  * [ ] `.dockerignore`&#x20;
* [ ] Des fichiers relatifs au projet :&#x20;
  * [ ] `package.json`&#x20;
  * [ ] [`pnpm-lock.yaml`](https://pnpm.io/) ou [`yarn.lock`](https://classic.yarnpkg.com/en/)
  * [ ] `tsconfig.json`
  * [ ] Les fichiers de configuration pour [Eslint](https://app.gitbook.com/o/WhkUfq5hgaTO6ZmJDX52/s/TxlFtrd9MnUa4wJ0FmXj/), [Prettier](https://prettier.io/docs/configuration), [Editorconfig](https://editorconfig.org/), [Husky](https://github.com/typicode/husky#readme), [Lint-Staged](https://github.com/lint-staged/lint-staged#readme)
  * [ ] Pour les tests, [Vitest](https://vitest.dev/config/) est recommandé, ou [Jest](https://jestjs.io/docs/getting-started)
  * [ ] Les fichiers `.env` et `.env.ENVIRONNEMENT` qui contiennent les variables d'environnement
  * [ ] La configuration pour [Sentry](https://sentry.io/welcome/)
* [ ] Pour un projet front-end :&#x20;
  * [ ] Les fichiers [vite](https://vite.dev/config/)
  * [ ] La configuration pour [Lighthouse](https://developer.chrome.com/docs/lighthouse/overview)

