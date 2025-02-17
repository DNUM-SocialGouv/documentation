# Hébergement & Cloud

## Pourquoi une stratégie Hébergement et Cloud pour les ministères sociaux ?

- Des enjeux de modernisation de l’action publique via la mise à disposition de services fluides et performants
- Des besoins applicatifs forts, que ce soit en termes d’agilité ou de composantes technologiques, nécessitant des
  cibles Cloud et des modes de fonctionnement DevOps
- La [Doctrine Cloud au Centre](https://www.numerique.gouv.fr/services/cloud/doctrine/) de l’Etat faisant du Cloud le socle d’hébergement par défaut


## Les grands principes de la stratégie hébergement et Cloud de la DNUM

- Les nouvelles applications (incluant les refontes) vont, par défaut, dans le Cloud. L’hébergement interne est réservé
  pour les périmètres non cloudifiables.
- Privilégier le recours au SaaS quand c’est possible, et l’utilisation des fonctionnalités natives proposées par les
  CSP (PaaS > IaaS)
- Le passage vers le Cloud doit s’accompagner d’une transformation des modèles d’architecture applicative (cloud
  native), d’organisation des équipes (DevOps, CI/CD), et d’optimisation financière et environnementale (FinOps,
  GreenOps)
- La bascule « telle quelle » (ou lift and shift), limitant la transformation, ne doit être utilisée que dans les cas
  qui le justifient (ex : migration de masse pour cause de fermeture de DC)
- Comme toute transformation, le passage vers le Cloud doit s’accompagner d’un volet RH (formation des agents,
  internalisation des compétences clés, accompagnement des équipes, …)

## Quel hébergement Cloud pour mon cas d'usage ?

Plusieurs typologies de besoins, nécessitant des offres d’hébergement appropriées, selon :

- La confidentialité des données
- Les besoins en services d’infrastructure
- Les exigences réglementaires, notamment le HDS

Pour répondre à ces typologies, 3 offres ont été identifiées :

- Cloud générique : qui vise à héberger toute application sans contrainte réglementaire spécifique
- Cloud HDS : qui vise à héberger les applications manipulant des données de santé et nécessitant une
  [certification HDS](https://esante.gouv.fr/produits-services/hds) de l'hébergement et de l'infogérance
- Cloud de confiance : qui vise à héberger les applications les plus sensibles, y compris celles contenant des données
  de santé sensibles, nécessitant une qualification
  [SecNumCloud par l'ANSSI](https://cyber.gouv.fr/secnumcloud-pour-les-fournisseurs-de-services-cloud)

> [!TIP] Quels sont les critères discriminants qui définissent les données d’une sensibilité particulière ? Deux
> conditions doivent être réunies pour que les données soient qualifiées comme particulièrement sensibles au sens de la
> doctrine :
>
> - d’une part, elles doivent être sensibles soit par nature (parce qu’identifiées comme un secret légal) soit du fait
>   de leur emploi (parce qu’impliquées dans une mission essentielle de l’État) ;
> - et d’autre part, leur violation aurait pour conséquence une atteinte à l’ordre public, la sécurité publique, la
>   santé, la vie des personnes ou la propriété intellectuelle.

## Plateforme Cloud FabNum

- Plateforme type PaaS (on pousse du code, pas des images)
- Sur cloud public OVH
- Niveaux EBIOS 2-3-3-2
- Services :
  - Stockage objet
  - BDD Managée ou pas
  - Pas de NAS : considérer qu'il n'y a pas de système de fichier accessible aux applications

## Cegedim.Cloud

- Plateforme IaaS/CaaS
- Services
  - Stockage objet
  - BDD Managée ou pas
