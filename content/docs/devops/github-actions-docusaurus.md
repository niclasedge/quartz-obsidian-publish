---
title: Github Action Docusaurus Deployment
linkTitle: Github Actions Docusaurus Deployment
date: 2022-10-30
description: 'Nutzen einer Github Action um Docusaurus auf dem eiogenen Server zu
  Veröffentlichen

  '
tags:
- Docusaurus
- github actions
series:
- DevOps
---
## SSH Secret bei Github einrichten

1. neues key pair erstellen
- `ssh-keygen -t ed25519 -C "you@gmail.com"`
2. auf dem Zielserver den Public Key in die Datei authorized_keys speichern
- `cat ~/.ssh/id_ed25519.pub`
- `nano ~/.ssh/authorized_keys`public key einfügen
3. private key bei github hinterlegen
- in dem jeweiligen repo auf "settings" -> "Secrets" -> "Actions" + "New repository secret"

## Action erstellen
```yaml
name: Deploy Docusaurus

on:
  push:
    branches:
      - main  # Change to the branch you want to deploy from

jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest

    steps:
      - name: 🛒 Checkout
        uses: actions/checkout@v2

      - name: 📦 Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: 16

      - name: 🔑 Install SSH Key
        run: |
          install -m 600 -D /dev/null ~/.ssh/id_rsa
          echo "${{ secrets.PRIVATE_SSH_KEY }}" > ~/.ssh/id_rsa
          echo "${{ secrets.KNOWN_HOSTS }}" > ~/.ssh/known_hosts
      - name: 🚀 Build and Deploy
        run: |
          npm install
          npm run build
          rsync -avz --delete ./build/ ${{ secrets.REMOTE_DEST }}
        
```

## Secrets hinzufügen
- REMOTE_DEST = 
    - USER@server-ip:/home/USER/public
- KNOWN_HOSTS = 
    - `ssh-keyscan <IP of Server>`
- PRIVATE_SSH_KEY:
-----BEGIN OPENSSH PRIVATE KEY-----


### Referenzen:
- [https://swharden.com/blog/2022-03-20-github-actions-hugo/](https://swharden.com/blog/2022-03-20-github-actions-hugo/)

- [https://serverpilot.io/docs/how-to-use-ssh-public-key-authentication/](https://serverpilot.io/docs/how-to-use-ssh-public-key-authentication/)