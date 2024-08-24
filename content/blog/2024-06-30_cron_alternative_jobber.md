---
title: Jobber - eine übersichtlicher Cron alternative
description: eine übersichtlicher Cron alternative
authors: niclasedge
images: ./docs/azure/az104/Pasted image 20230508124233.png
tags:
- macos
- linux
created: 30.06.2024
---

:::info

Jobber ist ein leistungsstarkes Tool zur Verwaltung und Planung von Aufgaben, das als Alternative zu cron dient. Hier sind die grundlegenden Schritte und Befehle, um Jobber zu nutzen:

:::

Cron ist seit Jahrzehnten das Standard-Tool für die Planung wiederkehrender Aufgaben in Unix-basierten Systemen. Doch mit der zunehmenden Komplexität moderner Infrastrukturen und Anforderungen stoßen viele Entwickler und Systemadministratoren an die Grenzen von Cron. Hier kommt Jobber ins Spiel - ein leistungsfähiger und flexibler Ersatz für Cron, der zusätzliche Funktionen und eine verbesserte Benutzerfreundlichkeit bietet.

## Was ist Jobber?

Jobber ist ein Open-Source-Aufgabenplaner für Linux-Systeme, der als Alternative zu Cron entwickelt wurde. Er bietet erweiterte Funktionen wie:

- Fehlerbenachrichtigungen
- Wiederholungsversuche für fehlgeschlagene Jobs
- Zeitzonenunterstützung
- Detaillierte Protokollierung

## Installieren
1. **Jobber installieren**:
   ```sh
   brew install jobber
   ```

2. **Jobber-Dienst starten**:
   ```sh
   sudo brew services start jobber
   ```

## Konfigurieren
Jobber verwendet eine YAML-Konfigurationsdatei, um Jobs zu definieren. Diese Datei befindet sich normalerweise unter `/etc/jobber.yaml`.

`jobber init` erstellt die initiale Konfig Datei

#### Beispiel-Konfigurationsdatei Linux
Hier ist ein Beispiel für eine Jobber-Konfigurationsdatei:
```yaml title="/etc/jobber.yaml"
version: 1.4

jobs:
  - name: "DailyBackup"
    cmd: "rsync -a /home/user/documents /backup/documents"
    time: "0 2 * * *"
    onError: "Continue"
    notifyOnError: true

  - name: "WeeklyCleanup"
    cmd: "rm -rf /tmp/*"
    time: "0 3 * * 0"
    onError: "Backoff"
    notifyOnError: true
```
In diesem Beispiel wird ein tägliches Backup um 2 Uhr morgens und eine wöchentliche Bereinigung des `/tmp`-Verzeichnisses um 3 Uhr morgens am Sonntag definiert.

`jobber reload` - nachdem die Konfig angepasst wurde

:::warning

Da ich in einem Powershell Skript git nutze kam es zu einem Fehler:
`fatal: could not read Username for 'https://github.com': Device not configured`

:::

Dieser konnte gelöst werden indem man den Remote neu setzt im Skript:
```powershell title="test.ps1"
git remote set-url origin git@github.com:username/reponame.git
git push
```

## Jobber benutzen

#### Jobber-Befehle
1. **Job testen**:
   ```sh
   jobber test DailyBackup
   ```
   Dieser Befehl führt den Job `DailyBackup` sofort aus und zeigt das Ergebnis an.

2. **Job pausieren**:
   ```sh
   jobber pause DailyBackup
   ```
   Pausiert den Job `DailyBackup`.

3. **Job fortsetzen**:
   ```sh
   jobber resume DailyBackup
   ```
   Setzt den pausierten Job `DailyBackup` fort.

4. **Job-Befehl anzeigen**:
   ```sh
   jobber cat DailyBackup
   ```
   Zeigt das Shell-Skript an, das der Job `DailyBackup` ausführt.

5. **Job-Log anzeigen**:
   ```sh
   jobber log
   ```
   Zeigt das Protokoll der letzten Job-Ausführungen an.

#### Jobber-Dienste verwalten
1. **Jobber-Dienst stoppen**:
   ```sh
   sudo brew services stop jobber
   ```

2. **Jobber-Dienst neu starten**:
   ```sh
   sudo brew services restart jobber
   ```


## Praktische Beispiele

Lassen Sie uns nun einige praktische Beispiele für die Verwendung von Jobber betrachten.

### Beispiel 1: Einfacher Backup-Job

Hier ist ein einfacher Job, der täglich um 2 Uhr morgens ein Backup durchführt:

```yaml
- name: Daily Backup
  cmd: /path/to/backup-script.sh
  time: 0 2 * * *
  onError: Continue
  notifyOnError: true
  notifyOnFailure: true
```

### Beispiel 2: Systemaktualisierung mit Wiederholungsversuch

Dieser Job führt eine Systemaktualisierung durch und versucht es bei Fehlern bis zu dreimal:

```yaml
- name: System Update
  cmd: sudo apt-get update && sudo apt-get upgrade -y
  time: 0 4 * * 0  # Jeden Sonntag um 4 Uhr morgens
  onError: Backoff(5m, 3)
  notifyOnError: true
```

### Beispiel 3: Datenbankbereinigung mit Zeitzonenvorgabe

Ein Job zur Datenbankbereinigung, der in einer bestimmten Zeitzone ausgeführt wird:

```yaml
- name: Database Cleanup
  cmd: /usr/local/bin/db-cleanup-script
  time: 0 1 * * *
  timezone: America/New_York
  notifyOnSuccess: true
```

### Beispiel 4: Protokollrotation mit bedingter Ausführung

Dieser Job rotiert Protokolldateien, aber nur wenn der verfügbare Festplattenspeicher unter 20% fällt:

```yaml
- name: Log Rotation
  cmd: |
    if [ $(df -h / | awk 'NR==2 {print $5}' | sed 's/%//') -gt 80 ]; then
      /usr/sbin/logrotate /etc/logrotate.conf
    fi
  time: '0 0 * * *'
  onError: Stop
  notifyOnError: true
```

### Beispiel 5: Mehrstufiger Deployment-Prozess

Ein komplexerer Job, der einen mehrstufigen Deployment-Prozess durchführt:

```yaml
- name: Production Deployment
  cmd: |
    set -e
    echo "Starting deployment process..."
    /path/to/backup-production.sh
    /path/to/deploy-staging.sh
    /path/to/run-tests.sh
    /path/to/deploy-production.sh
    echo "Deployment completed successfully!"
  time: '0 22 * * 5'  # Jeden Freitag um 22 Uhr
  notifyOnSuccess: true
  notifyOnError: true
  onError: Stop
```

## Vorteile von Jobber gegenüber Cron

1. **Bessere Fehlerbehandlung**: Jobber bietet detaillierte Fehlerbenachrichtigungen und die Möglichkeit, Jobs bei Fehlern automatisch zu wiederholen.
2. **Flexiblere Zeitplanung**: Mit Unterstützung für Zeitzonen und komplexere Zeitpläne.
3. **Verbesserte Sicherheit**: Jobber läuft unter dem Benutzer-Kontext, was die Sicherheit erhöht.
4. **Detaillierte Protokollierung**: Einfachere Fehlersuche durch bessere Logging-Funktionen.
5. **Einfachere Konfiguration**: Die YAML-basierte Konfiguration ist leichter zu lesen und zu warten als die Cron-Syntax.

## Fazit

Jobber bietet eine moderne und leistungsfähige Alternative zu Cron. Mit seinen erweiterten Funktionen und der benutzerfreundlichen Konfiguration ist es besonders für komplexe Umgebungen und anspruchsvolle Aufgabenplanungen geeignet. Die praktischen Beispiele in diesem Artikel zeigen nur einen kleinen Teil der Möglichkeiten, die Jobber bietet. Durch den Einsatz von Jobber können Entwickler und Systemadministratoren ihre Aufgabenplanung optimieren und robuster gestalten.


Citations:
[1] https://help.getjobber.com/hc/en-us/articles/115009379027-Job-Basics
[2] https://help.getjobber.com/hc/en-us/articles/7061327071639-Jobber-App-Basics
[3] https://dev.to/jobber/building-an-app-in-jobber-platform-5259
[4] https://www.youtube.com/watch?v=FOlDqEpH-iA
[5] https://github.com/dshearer/jobber
[6] https://www.youtube.com/watch?v=zHSfbUgCfgg
[7] https://dshearer.github.io/jobber/doc/v1.4/
[8] https://www.youtube.com/watch?v=LNT5C_XLmfI
[9] https://curc.readthedocs.io/en/latest/running-jobs/slurm-commands.html
[10] https://www.youtube.com/watch?v=JSab2Tw9B5U
[11] https://www.redhat.com/sysadmin/jobs-bg-fg
[12] https://help.getjobber.com/hc/en-us/categories/115001335727-Videos
[13] https://www.linuxlinks.com/jobber-run-commands-schedule/
[14] https://www.youtube.com/channel/UCE_6hSXDXbyz1r9uoh6hv5w
[15] https://docs.automic.com/documentation/webhelp/english/ALL/components/TERMA_DOCU/6.4.6/AAI%20Guides/Content/Reference/CLI/CLI_Jobs.htm
