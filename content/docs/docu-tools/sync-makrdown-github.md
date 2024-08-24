---
title: Markdown Dateien synchronisieren
description: mit Github oder Ordnern
date: 2022-11-25 16:21:28.178000+00:00
preview: ''
draft: false
featured: true
toc: true
reward: false
pinned: false
carousel: false
comment: false
tags:
- link
categories: Linux
series:
- linux
images:
- github.png
---

> Szenario: 
> 1. automatisiere git sync
> 2. synchronisiere content Ordner


### Shell Script für Git sync
- fügt Dateien automatisch zu GIT hinzu und läd Daten runter

```shell
#!/bin/bash

cd '/Users/user/GITHUB/repository1'
git pull
git add .
git commit -m "Dateien geändert am `date +'%Y-%m-%d %H:%M:%S'`"
git push  origin main

cd '/Users/user/GITHUB/repository2'
git add .
git pull
git commit -m "Dateien geändert am `date +'%Y-%m-%d %H:%M:%S'`"
git push  origin main
```
git add . && git pull && git commit -m "Dateien geändert am `date +'%Y-%m-%d %H:%M:%S'`" && git push 

### Ordner Synchronisieren
#### Optionen für Ordner Sync
- rsync - sync in eine Richtung
- unison - bidirektionale synchronisation
- https://freefilesync.org/ - desktop app mit GUI
- syncthing
    - Rechner tauschen untereinander automatisch datein aus
- seafile . dropbox/oneDrive ersatz
    - man braucht einen server

#### UNISON option
> via brew installieren

```shell
unison -auto -batch  /Users/user/Seafile/Privat/blog-content/  /Users/user/GITHUB/repository/content/
```
- auto: nimmt die empfihlenen einstellungen
- batch: stellt keine Fragen mehr

#### RSYNC option
```shell
rsync -avzP  /Users/user/Privat/blog-content/   /Users/user/GITHUB/repository1/content
```
- a: archiv
- P: zeigt den fortschitt an
- optional: --delete, wenn gelöschte daten auch am ziel gelöscht werden sollen


### Cronjob einstellen

```shell
# crontab -e
*/5 * * * *  /Users/user/git.sh && unison -auto -batch  /Users/user/Seafile/Privat/blog-content/  /Users/user/GITHUB/repository/content/
```
- prüft alle 5 min github nach änderungen und synchronisiert die Ordner Bidirektional
