# cgi-docker-workshop

Wat heb je nodig om met Docker aan de slag te gaan?

## VirtualBox

Docker heeft een Linux gebaseerd host OS nodig. We gebruiken VirtualBox om een Linux VM te draaien.

Installeer VirtualBox: https://www.virtualbox.org/wiki/Downloads

## Vagrant

Om gemakkelijk met linux images om te gaan, gebruiken we Vagrant. Met behulp van Vagrant configureren we VM’s op een manier om snel VM’s op te tuigen en weg te gooien.

Installeer Vagrant: http://www.vagrantup.com/downloads.html

(!!! Let op !!! Installeer Vagrant in een directory zonder spaties! Dus niet in “c:\Program Files\Vagrant”)

Binnen CGI wordt gebruik gemaakt van een proxy. Zorg dat je proxy instellingen goed zijn door de volgende systeem variabelen te definiëren:
```
HTTP_PROXY=proxy.nl.logica.com:80
HTTPS_PROXY=proxy.nl.logica.com:80
```

En door de proxy plugin voor Vagrant te installeren: Run het volgende commando vanaf de commandline:

```
vagrant plugin install vagrant-proxyconf
```

Vagrant kan gebruik maken van voorgedefinieerde (base) images. Run het volgende commando vanaf de commandline:

```
vagrant box add ubuntu-docker https://github.com/jose-lpa/packer-ubuntu_14.04/releases/download/v2.0/ubuntu-14.04.box
```

je hebt nu de beschikking over een basis Ubuntu installatie met Docker.

## Git

Een basisconfiguratie om mee aan de slag te gaan heb ik op GitHub geplaatst. 

Download en installeer Git: http://git-scm.com/download/

## Basis setup

Maak een werk directory aan (hernoem deze niet, in de configuratie files wordt deze directory gebruikt om bestanden tussen VM, DockerContainer en host machine te delen)


```
mkdir c:\Data
```

In deze directory, clone de basisconfiguratie:

```
cd c:\Data
git clone https://github.com/okke/cgi-docker-workshop.git
```

Test de basisconfiguratie. run de volgende commandline commando’s

```
cd c:\Data\cgi-workshop-docker\vagrant
vagrant up
vagrant ssh
docker help
```

Voordat we starten, zorg dat je de laatste versie van de basisconfiguratie hebt:

```
cd c:\Data\cgi-workshop-docker
git pull
```
