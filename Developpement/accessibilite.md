# Accessibilité

Il est recommandé de lire la définition de l'accessibilité présente dans la [section Design](../Design/Accessibilite.md).

## DSFR et portages

Le [DSFR](https://www.systeme-de-design.gouv.fr/), qui est le Système de Design de l'État, est
[porté](design.md#dsfr) sur divers outils tels que React, Vue ou
encore Angular.

Au-delà du caractère [obligatoire](../Design/Processus-de-design.md#utilisation-obligatoire-du-design-system-dsfr) de
son utilisation, les composants du système de design sont conçus avec l'accessibilité au cœur.

## Guides des pratiques de développement

Des guides, tels que le [WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/fr) ou le
[RGAA](https://accessibilite.numerique.gouv.fr/), existent afin de permettre et faciliter les pratiques de
développement :

- Les notices d'intégration de [AcceDe Web](https://www.accede-web.com/notices/html-et-css/) ;

## Outillage et pratiques

Certains projets utilisent [Lighthouse](https://github.com/GoogleChrome/lighthouse) afin de vérifier le niveau
d'accessibilité, notamment comme étape du processus de CI.

Pour les projets en TS, certains plugins [Eslint](https://eslint.org/) permettent de s'assurer automatiquement que les régles d'accessibilité sont respectées (par exemple [react-a11y](https://github.com/reactjs/react-a11y)).
Nous vous recommandons aussi de compléter vos tests unitaires et d'intégrations avec l'utilisation de [jest-axe](https://www.npmjs.com/package/jest-axe) dans le cas où vous utilisez [Jest](https://jestjs.io/) pour vos tests.

Nous vous recommandons d'écrire un test spécifique pour chaque **composants**, **chaque parent** et au niveau de **la page** ou/et de **l'onglet**.
