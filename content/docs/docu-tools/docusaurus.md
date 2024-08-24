---
title: Docusaurus
date: 2022-11-23
description: 'Markdown Documentation Platform with Static Site rendering based on
  React.js

  '
featured: false
draft: false
toc: true
reward: false
pinned: false
carousel: false
comment: false
categories: Documentation
tags:
- markdown
- static site generator
- open source
images:
- docusaurus.jpeg
---
> Platform die auf Markdown basiert und davon eine Statische Website erstellt
> - https://docusaurus.io/

TODOS:
- https://github.com/cmfcmf/docusaurus-search-local
- Tags anzeigen lassen

## Übersicht
### Vorteile:
- basiert auf Markdown Dateien
- Open Source 
- Konfiguration mit YAML Datei
- Sehr gute Suche mit auto verfollständigung
    - via algolia
    - 3rd party dienst
- github integration, seite bearbeiten
### Nachteile:
- keine

## Setup
- docusaurus npm package installieren
- seite mit npm erstellen
- yaml file konfigurieren
- markdown Dateien hinzufügen
- statische Seite generieren
- Statische Seite bereitstellen
  - Docker Compose mit reverse Proxy
- CD einrichten mit Github Actions



## Deployment
- Kann mit Docker Container bereitgestellt werden

### Continuous Delivery
- CD via Github Action
- jenkins
- o.ä.

![](git-deploy.png)

