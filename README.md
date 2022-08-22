# FoldingAtHome-Docker

Vorlage und Erklärung für FoldingAtHome in Docker für das #SchenklRadio Team

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
`sudo docker-compose up -d`

## Status einsehen

In einem Terminal deiner Wahl das vorhin geclonte Verzeichnis betreten (falls noch nicht geschehen):  
`cd FoldingAtHome-Docker`

Mit folgendem Befehl wird der Fortschritt beobachtet:  
`sudo docker-compose logs -f`

## Beenden

In einem Terminal deiner Wahl das vorhin geclonte Verzeichnis betreten (falls noch nicht geschehen):  
`cd FoldingAtHome-Docker`

Mit folgendem Befehl wird der Fortschritt beobachtet:  
`sudo docker-compose down`


## Einstellmöglichkeiten

**Kleinere Jobs:**  

Wollt ihr kleinere Jobs haben, die schneller durchgerechnet sind, könnt ihr folgendes in die "environment" Sektion angeben:  
`      - POWER=light`

Also sieht eure docker-compose.yml dann so aus:  

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
      - POWER=light
      - ENABLE_GPU=false
      - ENABLE_SMP=true
    restart: unless-stopped
```

Wichtig, nach der Änderung an der docker-compose.yml müsst ihr den Prozess beenden und neu starten:
`sudo docker-compose down && sudo docker-compose up -d`

## Hinweise

**Betrieb:**  

Ihr solltet darauf achte ein Projekt immer zu 100% durchlaufen zu lassen.  
Es früher zu beenden geht natürlich, aber i.d.R. fangt ihr am nächsten Tag von Vorne oder mit einem neuen Projekt an.  
(Es kann funtkonieren, dass an einem Punkt weitergemacht wird, oder ihr ein paar Prozente verliert, muss es aber nicht)
Weiter ist es sehr sinnvoll das zu tun, weil der Wissenschaft hauptsächlich an an einem Stück durchgerechnete Aufgaben nützlich sind.

Diese Anleitung ist daher am Besten für Systeme geeignet, die 24/7 laufen.

**Statistiken:**

Die offizielle Statistikseite für das Team ist: https://stats.foldingathome.org/team/263779

Die inoffizielle Statsitikseite mit viel mehr Details ist: https://folding.extremeoverclocking.com/team_summary.php?s=&t=263779

Wenn ihr wissen wollt, für was ihr gerade Rechnleistung spendet, schaut mit `sudo docker-compose logs -f` nach, an welcher "Projekt-ID" ihr gerade beteiligt seid und fügt diese in folgenden Link ein: https://stats.foldingathome.org/project/<ID>  
Z.B. dieses: https://stats.foldingathome.org/project/16959
