# FoldingAtHome-Docker

Template und Erklärung für FoldingAtHome in Docker für das #SchenklRadio Team

# Vorraussetzungen

- Linux
- Docker
- Docker-compose
- Git
- Internet (nach außen offene Ports: 80, 443, 8080)

# Einrichtung

## Docker & Docker-compose & git installieren

Offizielle Docker-Installations-Anleitung für Debian/Ubuntu: https://docs.docker.com/engine/install/ubuntu/  
Linux Mint ist hier gleichbedeutend mit Ubuntu.

Ist Docker installiert, braucht ihr noch git, um an die Daten aus diesem Repository ranzukommen.  
Installierbar mit jedem Paketmanager, gerne per GUI oder CLI, das Paket heißt `git`.  

In Kürze:

In einem Terminal deiner Wahl folgendes eingeben:  
```
sudo apt update
sudo apt install -y docker.io docker-compose git
```

## Namen überlegen und merken

In diesem Beispiel: asdf

## Passkey beantragen

Den gemerkten Namen in das Formular eintragen
-> https://apps.foldingathome.org/getpasskey

Der Passkey kommt dann per E-Mail.

In diesem Beispiel: 0123

## Dieses Repo Clonen

In einem Terminal deiner Wahl folgendes eingeben:  
`git clone https://github.com/schenklklopfer/FoldingAtHome-Docker`

## Daten in docker-compose.yml eintragen

In dem gerade erstellten Verzeichnis "FoldingAtHome-Docker" liegt eine Datei mit dem Namen "docker-compose.yml" diese wird hier angepasst:  
Die Datei mit einem Texteditor deiner Wahl anpassen.  
Wenn ihr schon im Terminal seid, kann das z.B. mit `nano docker-compose.yml` gemacht werden.  

Den überlegten Namen bei "USER=" eintragen.  
Den per E-Mail bekommenen Passkey bei "PASSKEY=" eintragen.

Die Datei speichern

In diesem Beispiel sieht das dann so aus:
```
---
version: "3"
services:
  folding-at-home:
    image: yurinnick/folding-at-home:latest
    environment:
      - USER=asdf
      - PASSKEY=0123
      - TEAM=263779
      - ENABLE_GPU=false
      - ENABLE_SMP=true
    restart: unless-stopped

```
## Starten

In einem Terminal deiner Wahl das vorhin geclonte Verzeichnis betreten (falls noch nicht geschehen):  
`cd FoldingAtHome-Docker`

Mit folgendem Befehl wird der Prozess gestartet:  
`docker-compose up -d`

## Status einsehen

In einem Terminal deiner Wahl das vorhin geclonte Verzeichnis betreten (falls noch nicht geschehen):  
`cd FoldingAtHome-Docker`

Mit folgendem Befehl wird der Fortschritt beobachtet:  
`docker-compose logs -f`

## Beenden

In einem Terminal deiner Wahl das vorhin geclonte Verzeichnis betreten (falls noch nicht geschehen):  
`cd FoldingAtHome-Docker`

Mit folgendem Befehl wird der Fortschritt beobachtet:  
`docker-compose down`
