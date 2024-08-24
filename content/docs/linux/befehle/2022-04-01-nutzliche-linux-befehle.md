---
slug: nutzliche-linux-befehle
title: Nützliche Befehle
date: 2022-04-01
featured: false
draft: false
toc: true
reward: false
pinned: false
carousel: false
comment: false
series:
- Linux
categories:
- Linux
tags:
- befehl
images:
- images/linux.png
---

## Linux: Nützliche Befehle
Wenn man anfängt mit Linux zu arbeiten, ist man schnell überwältigt von all den Befehlen/Programmen/Optionen etc. die Linux einem im Hintergrund anbietet.
Diese Optionen können einem das Leben ungemein vereinfachen und einem helfen seine "Arbeit" schneller zu erledigen.
Hier ist eine Sammlung von Befehlen die ich mit mit der Zeit erarbeitet habe und im Einsatz habe:

### Files & Folders
Ordner kopieren:
```cp -R /etc/* /etc_backup```
Einen Ordner und dessen Inhalt löschen:
```rm -rf dirName```
Synchronisiere einen Ordner mit dem Anderen (Inklusive löschungen):
```rsync -auvhP /source/ /output/```
### Network
Gib mir alle Dienste die an einem Port "Lauschen":
```netstat -tulpn | grep LISTEN```

### User hinzufügen und berechtigen docker zu nutzen
```shell
# create user with home directory
useradd -m <USERNAME>

# add user to sudoers
usermod -aG sudo <USERNAME>

# allow user to run docker commands without password prompt
sudo visudo
<USERNAME>     ALL=(ALL) NOPASSWD:/usr/bin/docker
```

### SSH Schlüßel erzeugen
```shell
# switch to user
su - <USERNAME>

# generate ssh-key
ssh-keygen -t rsa -b 4096
```
