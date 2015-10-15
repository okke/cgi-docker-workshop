# Oefening 2, Run een simpele node.js server in een container

## maak een docker image configuratie

Maak de volgende directory aan: `/data/nodejs` 

Maak in deze directory een basis nodejs container aan met behulp van de volgende `Dockerfile`

```
FROM <username>/base
RUN apt-get update -y
RUN curl --silent --location https://deb.nodesource.com/setup_0.12 | sudo bash -
RUN apt-get install -y nodejs
```

*Merk op, er wordt gebruik gemaakt van de eerder aangemaakte `base` docker container* 


Test je nodejs configuratie door een image te maken en te kijken of je in een container gebaseerd op dit image een *node* en een *npm* commando hebt.

```
docker build -t "<username>/nodejs" .
docker run -it <username>/nodejs
```

Maak wederom een nieuwe directory aan: `/data/hellonode` 

Maak hierin een `src` directory aan en plaats daar de volgende twee files in:

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
FROM <username>/nodejs

COPY ./src /src
RUN cd /src; npm install
EXPOSE  8080

CMD ["node", "/src/index.js"]
```

Maak op de gebruikelijke wijze (docker build) een image en run deze met het volgende commando

```
docker run -d -p 8080:8080 <username>/nodejs
```

