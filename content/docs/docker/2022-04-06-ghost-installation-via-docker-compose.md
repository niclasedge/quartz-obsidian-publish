---
slug: ghost-installation-via-docker-compose
title: Ghost CMS Installation via Docker Compose
authors: edge
tags:
- service
- docker compose
- linux
- ghost cms
date: 2022-04-06
series:
- Docker Guide
---

Chost CMS ist eine open source "headless" alternative zu Wordpress.

Es ist deutlich simpler in der Bedienung und basiert auf einem modernen Technologie Stack ().

Des Weiteren hat es viele Features als standard mit an Board siehe:

[

Ghost: The simple, powerful WordPress alternative

Trying to find out how Ghost compares to WordPress? We’ve put together a full rundown of Ghost vs WordPress and the differences between them.

![](https://ghost.org/favicon.ico)

![](https://ghost.org/images/meta/ghost.png)

](https://ghost.org/vs/wordpress/)

Da ich mittlerweile alles über eigene Docker Container mit Hilfe von Docker Compose steuere, habe ich dies auch hier getan. Und es Funktioniert super!

So kann ich eine neue Website in 2 Minuten aufsetzen und bereitstellen:)

#### Installationsschritte

0.  alle benötigte login Daten von google besorgen, siehe Abschnitt 2§
1.  docker-compose.yml Datei in gewünschtem Ordner erstellen
2.  via `cd wunschordner` Befehl in den Ordner wechseln
3.  den Befehl `docker compose up -d` ausführen
4.  Fertig!
5.  ggf müsst Ihr den Port bei Eurer Firewall freigeben
    -   ich nutze die ufw von Linux
        -   der Befehl um einen Port freizugeben is `sudo ufw allow 49160`

#### Mein docker-compose.yml file:

```
version: "3"
services:
  ghost:
    image: ghost:latest
    ports:
      - 49160:2368 # bitte 49160 auf gewünschten port ändern
    environment:
      url: https://blog.meinewebsite.com
      # if you use googlemail for transactional mail
      mail__from: Dein Name <meinemail@googlemail.com>
      mail__options__auth__user: meinemail@googlemail.com
      # special app password generated in https://myaccount.google.com/ -> security -> app password
      # need 2FA active
      mail__options__auth__pass: mein_app_passwort 
      mail__transport: SMTP
      mail__options__port: 465
      mail__options__host: smtp.googlemail.com
      mail__options__secure: true

      
      # Use mailgun for transactional mail
      # mail__transport: SMTP
      # mail__from: niclasedge@googlemail.com
      # mail__options__service: SMTP
      # mail__options__host: smtp.eu.mailgun.org
      # mail__options__port: 587
      # mail__options__auth__user: postmaster@sandboxd_test.mailgun.org
      # mail__options__auth__pass: mein_auth_pass_von_mailgun
    volumes:
      - ./data:/var/lib/ghost/content
    restart: unless-stopped
volumes:
  ghost:
```

#### Was geändert werden muss:

1.  url - hier kommt Eure URL rein
2.  mail\_\_from - hier kommt Eure googlemail
3.  mail\_\_options\_\_auth\_\_user - hier kommt Eure googlemail rein
4.  mail\_\_options\_\_auth\_\_pass # hier kommt Euer App passwort rein

## 2§ Einrichten der Email für Mitglieder und Newsletter

### Einrichten der "normalen" eMail Funktion (googlemail)

Die Login Daten werden über Umgebungsvariablen im docker-compose.yml hinterlegt.

Falls Ihr **googlemail** nutzt könnt Ihr Euch an meinem Setup orientieren.

-   Für googlemail müsst Ihr 2FA aktiviert haben
-   und Euch ein App Password generieren [https://myaccount.google.com/](https://myaccount.google.com/) \-> security -> app password
-   Falls Ihr nicht weiter kommt schaut Euch diesen Artikel an, sind alle Schritte im Detail beschrieben: [https://officialrajdeepsingh.dev/how-to-config-gmail-smtp-in-ghost-cms/](https://officialrajdeepsingh.dev/how-to-config-gmail-smtp-in-ghost-cms/)

Für andere Anbieter müsste man ggf. nocheinmal googlen:)

### Einrichten der "erweiterten" Newsletter eMail Funktion

Um die erweiterte Funktion eines eMail Newsletters zu nützen benötigt Ihr einen mailgun account.

-   Dazu benötigt Ihr wie gesagt einen Mailgun Account+
-   Falls Ihr nicht weiter kommt, kann ich Euch diesen Artikel empfehlen, da sind alle Schritte nochmal erklärt: [https://bavatuesdays.com/configuring-email-for-a-ghost-docker-container-on-reclaim-cloud/](https://bavatuesdays.com/configuring-email-for-a-ghost-docker-container-on-reclaim-cloud/)

## 3§ Themempfehlungen

kommt noch

## 4§ Weiterführende Links:

Wer sich mit dem anpassen der Themes und der Struktur der Platform beschäftigen möchte kann sie diesen Artikel ansehen: [https://www.christhefreelancer.com/ghost-theme-development-guide/](https://www.christhefreelancer.com/ghost-theme-development-guide/)

Und wenn Ihr einen Kurs zum Thema Ghost CMS Development möchtet ist hier der passende Skillshare Kurs: [Skillshare class](https://skl.sh/3aFWINn)