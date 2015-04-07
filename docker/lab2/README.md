# Oefening 2, Run een simpele node.js server in een container

## maak een docker image configuratie

Maak een basis configuratie aan met behulp van de volgende Dockerfile

```
FROM <username>/base
RUN apt-get update -y
RUN apt-get install nodejs
RUN apt-get install npm
```
