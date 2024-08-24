---
slug: scp-daten-zwischen-linux-server-kopieren
title: scp - Daten zwischen Linux Server kopieren
date: 2022-04-04
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

## scp: Daten zwischen Linux Server kopieren

Wenn man mit mehreren Geräten arbeitet kommt man oft in die Lage, daten von einer Maschiene auf die andere zu kopieren.

Dies kann über FTP oder SFTP passieren.

Oder Ihr nutzt einfach das Linux standart tool "scp"
scp steht für secure copy.

Der Befehlt verschlüsseld die Daten und kann auch zu einem externen Gerät hin kopieren.


Hier müssen (wie bei ssh) der username und die IP/Hostname angegeben werden und der Zielpfad:

### Dateien kopieren
``` shell
scp QUELLDATEI  username@zielip:ZIELPFAD

scp backup.tar  root@192.168.1.2:/home/root/daten
```
### Ordner kopieren

```shell
scp -r /home root@192.168.1.2:/home
``` mit docker-compose file erstellen: