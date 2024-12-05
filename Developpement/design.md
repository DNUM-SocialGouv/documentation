# Design

## DSFR

Nos produits utilisent le [DSFR](https://www.systeme-de-design.gouv.fr/) et nous nous sommes demandés quels portages
seraient les plus pertinents.

Pour cela, nous avons choisi différents critères : 

- La page documentaire sur le site du DSFR, [ici]https://www.systeme-de-design.gouv.fr/communaute/portages-en-cours,
- Les signes de vie du projet (contributions, popularité),
- La qualité de la documentation,
- Le nombre de composants implémentés, par rapport aux composants proposés par le DSFR,
- La bibliothèque/framework dans lequel le portage est développé.

### Portage React : codegouv.fr/react-dsfr

React est utilisé dans nos développements et nous avons étudié deux bibliothèques :
_[codegouv.fr/react-dsfr](https://github.com/codegouvfr/react-dsfr)_ et
_[dataesr/react-dsfr](https://github.com/dataesr/react-dsfr)_.

Des deux bibliothèques, nous avons trouvé que _[codegouv.fr/react-dsfr](https://github.com/codegouvfr/react-dsfr)_
était celle qui devait être privilégiée dans nos développements en raison de ses contributions fréquentes.

### Portage Vue : vue-dsfr

Vue est également utilisé dans nos développements.

Nous avons identifié que la bibliothèque [vue-dsfr](https://github.com/dnum-mi/vue-dsfr) était la plus à même de
répondre à nos besoins.

### Portage Angular : ngx-dsfr

Bien que nous n'utilisions pas Angular dans nos développements internes, les portages Angular ont également été étudiés.

Ici, nous avons identifié [ngx-dsfr](https://gitlab.mim-libre.fr/men/transverse/dsmen/ngx-dsfr-components) comme
bibliothèque à privilégier lors des développements.

De plus, nous avons également noté la présence de
[ngx-dsfr-ext](https://gitlab.mim-libre.fr/men/transverse/dsmen/ngx-dsfr-ext), maintenu par la même équipe, et qui
propose des composants, non-officiels, mais qui évitent aux équipes de les développer elles-mêmes.