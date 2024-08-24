---
title: Bookstack
date: 2022-11-24
featured: true
draft: false
toc: true
reward: false
pinned: false
carousel: false
comment: false
series: null
categories:
- Documentation
tags:
- open source
images:
- bookstack.webp
---

> open Source Wiki Software, basiert auf Larvel
> https://www.bookstackapp.com/

## Übersicht
### Vorteile:
- Open Source
- Sehr gute Suche
- API
### Nachteile:
- basiert auf MySQL

## Setup
- Docker Compose mit reverse Proxy
- CD einrichten mit Github Actions


## Deployment
- Kann mit Docker Container bereitgestellt werden
> Mein bevorzugtes Image kommt vom Linuxserver Repository

```yaml
# docker-compose.yaml
---
version: "2"
services:
  bookstack:
    image: lscr.io/linuxserver/bookstack:latest
    container_name: bookstack
    environment:
      - PUID=1000
      - PGID=1000
      - APP_URL=
      - DB_HOST=bookstack_db
      - DB_USER=bookstack
      - DB_PASS=${DB_PASS}
      - DB_DATABASE=bookstackapp
      - API_REQUESTS_PER_MIN=2000
      - APP_URL=https://bookstack.meine-domain.com
      #- WKHTMLTOPDF=/usr/bin/wkhtmltopdf
      - ALLOW_UNTRUSTED_SERVER_FETCHING=true
      - ALLOW_ROBOTS=false
      - FILE_UPLOAD_SIZE_LIMIT=100
      - STORAGE_TYPE=local_secure_restricted
      #- APP_THEME=dg
      - MAIL_DRIVER=smtp
      # Host, Port & Encryption mechanism to use
      - MAIL_HOST=smtp.googlemail.com
      - MAIL_PORT=465
      - MAIL_ENCRYPTION=tls
      # Authentication details for your SMTP service
      - MAIL_USERNAME=meine-mail@googlemail.com
      - MAIL_PASSWORD=rxdnjsjzqywypeac
      # The "from" email address for outgoing email
      - MAIL_FROM=meine-mail@googlemail.com
      # The "from" name used for outgoing email
      - MAIL_FROM_NAME=Niclas via BookStack
    volumes:
      - ./bookstack_config:/config # hier werden auch die hochgeladenen Bilder etc gesichert
      #- ./.env:/var/www/bookstack/.env # optional via env file oder die Variablen direkt über compose definieren
    restart: unless-stopped
    depends_on:
      - bookstack_db
    networks:
      - proxy
    labels:
      # optional: via traefik reverse proxy bereitstellen
      - "traefik.enable=true"
      - "traefik.docker.network=proxy"
      - "traefik.http.routers.bookstack-secure.entrypoints=websecure"
      - "traefik.http.routers.bookstack-secure.rule=Host(`bookstack.meine-domain.com`)"

  bookstack_db: # datenbank in der die BookStack Daten gespeichert werden
    image: lscr.io/linuxserver/mariadb
    container_name: bookstack_db
    environment:
      - PUID=1000
      - PGID=1000
      - MYSQL_ROOT_PASSWORD=${DB_PASS}
      - TZ=Europe/London
      - MYSQL_DATABASE=bookstackapp
      - MYSQL_USER=bookstack
      - MYSQL_PASSWORD=${DB_PASS}
    volumes:
      - ./db_config:/config
    restart: unless-stopped
    networks:
      - proxy

networks:
  proxy:
    external: true

```

### Continuous Delivery
- CD via Github Action
- jenkins
- o.ä.

