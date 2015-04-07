# Oefening 1, Een basis container

Maak een basis configuratie aan met behulp van de volgende Dockerfile

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

En start een container

```
docker run -it <username>/base
```

