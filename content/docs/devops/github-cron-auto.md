---
slug: github-automatisch
title: github - Automate Publishing
date: 2022-03-28
featured: false
draft: false
toc: true
reward: false
pinned: false
carousel: false
comment: false
series:
- devops
categories:
- github
tags:
- automatisieren
images:
- images/github.png
---

## Github: Automate Publishing

Da ich schon öffter in das Filesize Limit von Github gelaufen bin nutze ich jetzt diesen Befehl um nur Dateien die kleiner als "100MB" in das Repositiry hinzuzufügen.

`find * -size -100M -type f -print0 | xargs -0 git add`

### Setup a new Repository

```
git init
find * -size -100M -type f -print0 | xargs -0 git add
git commit -m 'initial commit'
git remote add origin git@github.com:username/new_repo
git push -u origin master
```

### Mit einem Token bei dem Repository anmelden

1. Man muss sich einen privaten Token erstellen in seinem Github:
   - Settings → Developer settings → Generate new token.
2. diesen Token beim initialen verbinden mit dem Repository angeben
   `https://[USERNAME]:[NEW TOKEN]@github.com/[ORGANISATION]/[REPO].git`
   ein Beispiel wie es bei Euch aussehen könnte:
   `https://peterschmidt:ghp_ZHoeiuwFzGiuoewzgfdisjgfduh9uuheiwfuhwIUHGo@github.com/peterschmidt/mein_test_repo.git`
3. Sobald Ihr Euch mit dem korrekten "passwort" also dem Token angemeldet habt, sollte github Euch Eure privaten Daten lesen und schreiben lassen.
   - Vorausgesetzt, Ihr habt dem Token die entsprechenden Rechte gegeben:)

`git remote set-url origin https://niclasedge:<token>@github.com:niclasedge/docker-compose-backup`
