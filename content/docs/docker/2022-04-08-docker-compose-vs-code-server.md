---
slug: docker-compose-vs-code-server
title: service - VS Code Server
authors: edge
tags:
- service
- docker compose
date: 2022-04-08
series:
- Docker Guide
---

Man kann einen VS Code Server auf seinem Server aufsetzen und via Website erreichen.

```yaml file="docker-compose.yml Datei"
---
version: "3.1"
services:
  code-server:
    image: lscr.io/linuxserver/code-server
    container_name: code-server
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - PASSWORD=${MAIL_PASSWORD} #optional
      - HASHED_PASSWORD= #optional
      - SUDO_PASSWORD=${MAIL_PASSWORD} #optional
      - SUDO_PASSWORD_HASH= #optional
      #- PROXY_DOMAIN=code-server.my.domain #optional
      - DEFAULT_WORKSPACE=/config/workspace #optional
    volumes:
      - ./config:/config
      - /home/nedge:/config/workspace
    restart: unless-stopped
    networks:
      - proxy
    labels:
      - "traefik.enable=true"
      - "traefik.docker.network=proxy"
      - "traefik.http.routers.code-secure.entrypoints=websecure"
      - "traefik.http.routers.code-secure.rule=Host(`code.domain.com`)"
networks:
  proxy:
    external: true
```
