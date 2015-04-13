# Oefening 2, Run een simpele node.js server in een container

## maak een docker image configuratie

Maak een basis node.js configuratie aan met behulp van de volgende Dockerfile (Merk op, er wordt gebruik gemaakt van de eerder aangemaakte docker image)

!! Doe dit in een aparte directory bijvoorbeeld docker/images/node

```
FROM <username>/base
RUN apt-get update -y
RUN apt-get install nodejs
RUN apt-get install npm
```

Test je nodejs configuratie door een image te maken en te kijken of je in een container gebaseerd op dit image een *nodejs* en een *npm* commando hebt.

```
docker build -t "<name>/nodejs" .
docker run -it <name>/nodejs
```

!! Maak wederom een nieuwe directory aan bijvoorbeeld docker/images/hellonode

Maak een source directory aan en plaats daar de volgende twee files in:

src/package.json
```
{
  "name": "docker-hello-from-node",
  "private": true,
  "version": "0.0.1",
  "description": "Say hi inside a docker container from node",
  "author": "Me",
  "dependencies": {
    "express": "3.2.4"
  }
}
```

src/index.js
```
var express = require('express');

var PORT = 8080;

var app = express();

app.get('/', function (req, res) {
 res.send('Hello world\n');
});

app.listen(PORT);

console.log('Running on http://localhost:' + PORT);
```

En maak een Dockerfile aan

```
FROM <name>/node

COPY ./src /src
RUN cd /src; npm install
EXPOSE  8080

CMD ["nodejs", "/src/index.js"]
```

Maak op de gebruikelijke wijze (docker build) een image en run deze met het volgende commando

```
docker run -p 8080:8080
```

