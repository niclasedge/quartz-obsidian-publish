---
title: Github Action HUGO Deployment
linkTitle: Github Actions Hugo Deployment
date: 2022-10-30
description: 'Nutzen einer Github Action um Hugo auf dem eiogenen Server zu Veröffentlichen

  '
tags:
- HUGO
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
name: Website

on:
  workflow_dispatch:
  push:

jobs:
  build:
    name: Build and Deploy
    runs-on: ubuntu-latest
    steps:
      - name: 🛒 Checkout
        uses: actions/checkout@v2

      - name: ✨ Setup Hugo
        env:
          HUGO_VERSION: 0.105.0
        run: |
          mkdir ~/hugo
          cd ~/hugo
          curl -L "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_Linux-64bit.tar.gz" --output hugo.tar.gz
          tar -xvzf hugo.tar.gz
          sudo mv hugo /usr/local/bin

      - name: ✨ Setup NPM dependencies
        run: |
          npm install --save-dev autoprefixer
          npm install --save-dev postcss-cli
          npm install -D postcss


      - name: 🛠️ Build
        run: hugo --minify

      - name: 🔑 Install SSH Key
        run: |
          install -m 600 -D /dev/null ~/.ssh/id_rsa
          echo "${{ secrets.PRIVATE_SSH_KEY }}" > ~/.ssh/id_rsa
          echo "${{ secrets.KNOWN_HOSTS }}" > ~/.ssh/known_hosts

      - name: 🚀 Deploy
        run: rsync --archive --delete --stats 'public/' ${{ secrets.REMOTE_DEST }}
        
```

## Secrets hinzufügen
- REMOTE_DEST = USER@server-ip:/home/USER/public
- KNOWN_HOSTS = 
    - `ssh-keyscan <IP of Server>`



### Referenzen:
- [https://swharden.com/blog/2022-03-20-github-actions-hugo/](https://swharden.com/blog/2022-03-20-github-actions-hugo/)

- [https://serverpilot.io/docs/how-to-use-ssh-public-key-authentication/](https://serverpilot.io/docs/how-to-use-ssh-public-key-authentication/)