---
title: CMS Architektur und DevOps Pipeline
date: 2022-10-25
description: 'HUGO DevOps Pipeline

  '
featured: false
draft: false
toc: true
reward: false
pinned: false
carousel: false
comment: false
series:
- Hugo
- DevOps
categories:
- Hugo
tags:
- cms
images:
- images/devops.png
---

## Übersicht

> Der Plan:

- [ ] Hugo Design erstellen
- [ ] Hugo DevOps Pipeline erstellen mit Github Actions
  - deployment auf eigenen Server
  - bereitgestellt via Docker
  - reverse proxy auf eigene URL
- [ ] Zentraler Speicher auf Postgress DB
- [ ] Daten abruf via selbst gehostetem CMS
  - baserow?
  - zwischentabelle um baserow ID mit der Postgress ID abzugleichen
- [ ] trigger: wenn neue daten in postgress
  - aktualisiere baserow
  - trigger deployment via github
