---
slug: linux-firewall
title: ufw - Linux Firewall
date: 2022-04-05
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
- firewall
- sicherheit
images:
- images/linux.png
---

## ufw: Linux Firewall
Die simpelste Firewall für Linux Distributionen ist wohl die ufw (uncomplicated firewall)

Es gibt einige simple Befehle und man ist schnell im Rennen (uns abgesichert).

### 1. Installation
``` shell
sudo alt install ufw
```
### 2. default optionen
``` shell
sudo ufw default deny incomming
sudo ufw default allow outgoing
```
### 3. Ports freigeben
#### prüfen welche Ports genutzt werden:
```shell
ss -nptl
```
#### Ports freigeben
``` shell
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
...
```
#### Ports sperren
Da wir mit der default deny incomming sowieso alle ports gesperrt haben, die nicht freigegeben sind ist dies nicht nötig, aber die Option ist da.
``` shell
sudo ufw deny 22
```

### 4. Firewall aktivieren/deaktivieren
``` shell
sudo ufw enable
sudo ufw disable
```

### 5. Status prüfen
``` shell
sudo ufw status
```