---
title: Github SSH Key
linkTitle: Github SSH Key
date: 2022-10-30
description: 'Nutzen einer Github Action um Hugo auf dem eiogenen Server zu Veröffentlichen

  '
tags:
- HUGO
- github actions
series:
- DevOps
---

## SSH Key erstellen und hinterlegen

1. Lokalen Key generieren
- `ssh-keygen -t ed25519 -C "you@gmail.com"`
2. public key bei github hinterlegen: 
- kopiere `cat ~/.ssh/id_rsa.pub`
3. github sagen, welchen schlüssel es nutzen soll (optional, falls der Pfad vom standard abweicht)
- `git config core.sshCommand "ssh -i ~/.ssh/id_rsa -F /dev/null"`

## Remote Repository definieren

- git remote add origin git@github.com:username/repo-name.git
  - darauf achten, dass es die ssh key adresse ist. sonst versucht sich git mit username und password anzumelden

Falls bereits ein falscher remote vorhanden:
1. aktuellen remote anzeigen: `git remote -v` 
2. remote entfernen: `git remote rm origin``
3. neuen remote via `git remote add ...` hinzufügen

