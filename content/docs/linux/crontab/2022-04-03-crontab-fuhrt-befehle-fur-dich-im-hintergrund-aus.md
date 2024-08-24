---
slug: crontab-fuhrt-befehle-fur-dich-im-hintergrund-aus
title: crontab - führt Befehle für Dich im Hintergrund aus
date: 2022-04-03
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
- crontab
- automation
images:
- images/linux.png
---

## crontab: führt Befehle für Dich im Hintergrund aus

Das Tool crontab ist standart auf allen linux oder osx Systemen.
Es wird genutzt um bestimmte Befehle oder Sktipte auszüführen in definierten Intervalen.

## Crontab öffnen und bearbeiten
Um crontab zu nutzen öffnet man das crontab File und für das gewünschte Interval und den gewünschten Befehl hinzu

```
# das crontab file öffnen
crontab -e
```

### Beispiel für ein crontab Befehl
```
*/30 * * * * rsync auvh -O --no-perms rsync -aP root@89.x.x.x:/home/user /Share/vmbackup/backup
```


## Die Struktur eines cronjobs
### und Optionen für die Intervale
```
# For details see man 4 crontabs

# Example of job definition:
.---------------- minute (0 - 59)
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
|  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
|  |  |  |  |
*  *  *  *  * user-name  command to be executed
```

Hilfe beim verstehen der Zeitintervale: https://crontab.guru/

### Weitere Startoptionen
```
@yearly
@annually
@monthly
@weekly
@daily
@hourly
@reboot	# Sehr nützlich, da man es direkt nach einem Neustart laufen lassen kann
```

## Monitoring

### Standart cron log
Im Syslog werden basis informationen über crontab ausgegeben.
Dies kann eingesehen via:
```
grep CRON /var/log/syslog
```

### Erweitertes cron log erstellen
Falls Ihr genauere Informationen über das ausgeführte Skript möchtet könnt Iht die ausgabe des Sktiptes in ein Logfile angeben.
Die tut Ihr indem Ihr diese Zeile hinter Euren Befehl in crontab schreibt:

```

0 0 * * * rsync auvh -O --no-perms rsync -aP root@89.x.x.x:/home/user /Share/vmbackup/backup >> /var/log/cron.log 2>&1
```