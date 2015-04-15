# Oefening 1, Een basis container
De volgende commando's worden uitgevoerd vanuit de Ubuntu shell. De `c:\Data` directory is gekoppeld aan de `/data` directory van de Ubuntu virtual machine die de host zal zijn voor de Docker containers. Doordat deze directories gekoppeld zijn kunnen configuratie bestanden zowel vanaf het Windows host OS als de Ubuntu VM worden aangemaakt.

Log in op de Ubuntu VM middels `vagrant ssh`

## maak een docker image configuratie
Maak de volgende directory aan: `/data/base` 
Plaats hierin een `Dockerfile` bestand met de volgende basis configuratie

```
FROM ubuntu

ENV http_proxy http://proxy.nl.logica.com:80
ENV https_proxy http://proxy.nl.logica.com:80
ENV no_proxy=localhost,127.0.0.1

RUN apt-get update -y
```

Maak een docker image met het volgende docker commando (verander username door eigen naam):

```
docker build -t "<username>/base" .
```

Controleer of de image aangemaakt is

```
docker images
```

## test de docker image

Run een commando in een container

```
docker run <username>/base ls
docker run <username>/base ps
```

Of start een (inter actieve) container

```
docker run -it <username>/base
```

