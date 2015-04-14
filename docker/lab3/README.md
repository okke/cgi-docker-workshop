# Oefening 3, redis client server voorbeeld

In deze oefening maken we 2 docker images aan. Voor de server en voor de client.
Maak hiervoor `/data/redis/server` en `/data/redis/client` aan waarin de `Dockerfile` en bijbehorende bestanden
geplaatst kunnen worden.

Beide docker images hebben Redis installatie nodig. 

```
FROM <username>/base

RUN apt-get install -y redis-server
```

En beide images maken gebruik van een startup script wat als volgt in een image wordt gekopieerd en gestart:

```
ADD startup.sh /tmp/                         

# dos 2 unix indien nodig
#
RUN tr -d '\r' < /tmp/startup.sh > .tmp                
RUN mv -f .tmp /tmp/startup.sh                         

RUN chmod +x /tmp/startup.sh                           
ENTRYPOINT exec /tmp/startup.sh                        
```

In de server configuratie dient de standaard Redis port worden opengezet:

```
EXPOSE 6379
```

Het startup script voor de server:

```
#!/bin/bash
echo "Starting Redis server"
redis-server
```

Het startup script voor de client:

```
#!/bin/bash
redis-cli -h $DB_PORT_6379_TCP_ADDR
```
(Merk op, de gebruikte environment variable wordt door docker aangemaakt zodra een container gelinkt wordt)

Maak de images op de gebruikelijke manier

Run de server met het volgende docker commando:

```
docker run --name redis -d <username>/redis-srv
```

(Merk op, --name geeft de container een naam die we nodig hebben om te kunnen linken, -d zorgt ervoor dat de container in de achtergrond doordraait)


Run de client met het volgende docker commando:

```
docker run --link redis:db -it <username>/redis-cli
```
(Merk op, de --link zorgt ervoor dat de container met de naam 'redis' gelinkt wordt als 'db'. Vervolgens wordt 'db' gebruikt als environment variable prefix voor het doorgeven vaan poort nummers)

Je krijgt nu een Redis prompt waarin je redis commando's kan geven (zie http://redis.io/commands).

Probeer bijvoorbeeld

```
SET soep heet
GET soep
```

Sluit de redis prompt (exit) en start wederom een client container. Als het goed is draait de server nog en zijn de resultaten van alle SET commando's bewaard.

Kill de server container

```
docker kill redis
```

Start een nieuwe server container en een nieuwe client container en zie dat alles nu echt weggegooid is.

