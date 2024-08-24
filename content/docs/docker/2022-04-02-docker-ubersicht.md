---
slug: docker-ubersicht
title: Getting Started
tags:
- übersicht
date: 2022-04-02
series:
- Docker Guide
---
## Docker Installieren

### Raspberri Pi Raspian OS
```shell
# install script runterladen
curl -fsSL https://get.docker.com -o get-docker.sh

# script laufen lassen
sudo sh get-docker.sh

# User zu docker gruppe hinzufügen
sudo usermod -aG docker [user_name]
```

## Docker Compose Installieren

```shell
sudo apt-get update
sudo apt-get install docker-compose-plugin

# Verify that Docker Compose is installed correctly by checking the version.
docker compose version
```


## Über Docker

### Was ist Docker?

### Vorteile von Docker:

## Docker Syntax:

### Teile von Docker
- Docker Image
    - Ein vordeffiniertes oder selbst erstelltes Image, dass einen Dienst bereitstellt. Zum Beispiel MySQL Server, Wordpress Blog, etc.
- Docker Container
- Docker Volume:
    - persistentes Volume: Ist ein Volume, dass die Daten von einem Ordner auf dem Rechner nimmt
        - ```/ordner_hostrechner:/ordner_docker```
- Docker Network: 

### Docker Image und Container erstellen
- Dockerfile: 
    - Hier kann man sich ein eigenes Docker Image nach eingenen Wünschen erstellen. Dies geschieht mit einem Dockerfile und dem "build" Befehl.
- Docker-Compose:
    - Definiert mehrere Dienste/Images in einer Datei
    - Kann auch über den Docker Befehl mit optionen erreicht werden
    - Ist deutlich übersichtlicher als der Docker Befehl mit Optionen und besser Nachvollziehbar


### Beispiel: Verschiedene Stufen von Komplexität
1. Vorgefertigtes Image nutzen
2. Eigenes Image erstellen mit Dockerfile
3. Einen Stack aus mehreren Services mit docker-compose file erstellen:
