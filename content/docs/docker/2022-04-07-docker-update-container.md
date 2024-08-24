---
slug: docker-update-container
title: service - Watchtower
description: Auto Update Container
tags:
- docker
- service
- docker compose
date: 2022-04-07
series:
- Docker Guide
---

Wenn man einen Container auf eine neue Imageversion updaten möchte hat man einige Optionen.
Die simpelste ist, dass aktuellste image zu "pullen", den container zu löschen und ihn mit docker run ... neu zu generieren. 

### 1§ Installierte image Version Prüfen

`sudo docker images`

### 2§ Aktuellstes Image pullen
`sudo docker pull portainer/portainer-ce:latest`

### 3§ Alten Container entfernen

```
# container id herausfinden
sudo docker ps

# container anhalten
sudo docker stop [container id]

# container löschen
sudo docker rm [container id]
```
**Dabei ist zu Beachten, dass sich die angeschlossenen Volumes dabei unangetastet bleiben!**

### 4§ Neuen Container mit dem neuen Image generieren
`sudo docker run run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest`


### Alternative: Automatische Updates via Watchtower einrichten

```yaml title="docker-compose.yml"
version: "3"
services:
  watchtower:
    container_name: watchtower
    image: containrrr/watchtower
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - WATCHTOWER_SCHEDULE=0 15 12 * * *
      - TZ=Europe/Berlin
      - WATCHTOWER_NOTIFICATIONS=email
      - WATCHTOWER_NOTIFICATION_EMAIL_FROM=${EMAIL}
      - WATCHTOWER_NOTIFICATION_EMAIL_TO=${EMAIL}
      - WATCHTOWER_NOTIFICATION_EMAIL_SERVER=smtp.googlemail.com
      - WATCHTOWER_NOTIFICATION_EMAIL_SERVER_PORT=465
      - WATCHTOWER_NOTIFICATION_EMAIL_SERVER_USER=${EMAIL}
      - WATCHTOWER_NOTIFICATION_EMAIL_SERVER_PASSWORD=PASSWORD
      - WATCHTOWER_NOTIFICATIONS_HOSTNAME=watchtower.domain.com
      - WATCHTOWER_NOTIFICATION_EMAIL_SUBJECTTAG=remote

```
