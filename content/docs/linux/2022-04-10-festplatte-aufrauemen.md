---
slug: festplatte-aufrauemen
title: Festplatten aufräumen auf Linux Systemen
date: 2022-04-10
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
- festplatte
images:
- images/linux.png
---

## Festplatten aufräumen auf Linux Systemen



## Wo wird der Speicherplatz genutzt?
### ncdu - Zeigt Dir die Ordner die den meisten Speicherplatz nutzen

```shell
# ncdu installieren
apt install ncdu

# in das Verzeichniss wechseln, dass durchsucht werden soll:
cd /

# ncdu starten
ncdu # startet einen scan, anschließend kann sieht man wo der meiste Speicher verbraucht wird
```


### Docker aufräumen


```shell
docker system prune
# Remove all unused containers, networks, images (both dangling and unreferenced), and optionally, volumes.
```