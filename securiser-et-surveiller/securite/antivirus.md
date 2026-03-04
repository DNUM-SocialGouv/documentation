# 🔒 Antivirus

Toute pièce-jointe téléchargée sur un produit - par IHM ou par API - fait systématiquement l'objet d'un contrôle antivirus. Les solutions diffèrent en partie suivant l'hébergement :

## Intranet Rosny/Duquesne

Les flux entrants dans l'Intranet sont passés automatiquement à l'antivirus via le protocole [ICAP](antivirus.md#icap). S'assurer tout-de-même :

* que le flux ICAP figure bien dans le Dossier d'Architecture
* que la fonctionnalité est bien activée par l'infogérant pour les flux à contrôler

## Cegedim

Similaire à l'Intranet.

## Atlas@OVH

En cible le contrôle antivirus des pièces-jointes se fera automatiquement via l'Ingress-Controller de Kubernetes (Traefik).\
En attendant cette cible, les applications appellent explicitement un antivirus ClamAV par API depuis le code de l'application. Cet antivirus est un composant géré par l'application et non par la plateforme Atlas.\

La cible nécessite clarification :
* L'ICAP sera t-il implémenté au niveau de l'Ingress-Controller (Traefik) ou en amont ?
* Sera t-il possible de désactiver l'ICAP pour une url donnée, pour des raisons de performance et de contrôle antivirus asynchrone ? (Ex : batch par API sur SICLE, document volumineux type blueprint de chantier)
* Par défaut l'ICAP sera t-il activé sur les flux sortants également (download d'un document depuis l'application métier vers le poste utilisateur) ?
* A quelle date l'évolution ICAP sera disponible ?

## Autres hébergements à date
* Faute d'ICAP, Docaposte effectue un contrôle par API ClamAV, comme sur Atlas.
* Il n'y a pas de guideline pour d'autres hébergements éventuels

## ICAP

Le [protocole ICAP](https://fr.wikipedia.org/wiki/ICAP) permet à un Reverse Proxy de déléguer le contrôle antivirus d'une pièce-jointe à un antivirus distant.
