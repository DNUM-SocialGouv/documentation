---
icon: lock
---

# Antivirus applicatif

L'enjeu est de s'assurer que toute pièce-jointe uploadée et downloadée sur une application métier, par interface ou par API, fait systématiquement l'objet d'un contrôle antivirus.
Les solutions diffèrent en partie suivant l'hébergement :

## Intranet Rosny/Dusquesne
Les flux entrants dans l'Intranet sont passés automatiquement à l'antivirus via le protocole [ICAP](#icap).
S'assurer tout-de-même :
- que le flux ICAP figure bien dans le Dossier d'Architecture
- que la fonctionnalité est bien activée par l'infogérant pour les flux à contrôler.

## Cegedim
Similaire à l'Intranet. Pas de différence identifiée.

## Atlas@OVH
En cible le contrôle antivirus des pièces-jointes devrait se faire automatiquement via le Reverse Proxy de l'Ingress (NGinx).
A date la solution n'est pas claire. Certaines applications appellent explicitement l'antivirus ClamAV par API depuis le code de l'application.

## ICAP
Le [protocole ICAP](https://fr.wikipedia.org/wiki/ICAP) permet à un Reverse Proxy de déléguer le contrôle antivirus d'une pièce-jointe à un antivirus distant.