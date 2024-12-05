# Structure d'un dépôt git d'une application

{% hint style="info" %}
**Important :** 

Une application doit pouvoir se lancer en local avec seulement 2 étapes : 
- `git checkout ...`
- `docker compose up -d`
{% endhint %}

## Organisation du dépôt 

Pour une application ayant : 

- un backend java
- un frontend react
- une base de données postgres
- un service keycloak

on doit avoir l'organisation suivante :

```plaintext
docker/
    keycloak/
        realm/
        sql/
        theme/
src/
    back/
        Dockerfile
        README.md
    front/
        Dockerfile
        README.md
docker-compose.yaml
README.md
.dockerignore
.env
.env.example
```