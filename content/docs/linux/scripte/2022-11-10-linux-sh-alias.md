---
title: Shell script via alias auf Linux ausführen
date: 2022-11-10
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
- shell
- script
images:
- images/linux.png
---

> Create an alias so you can execute a shell script via the comandline

## Create shell script
git.sh file
```shell
#!/bin/bash
cd /Users/username/GITHUB/hugo-aperto && 
git add . &&
git commit -m "daily" &&
git pull && 
git push
```

## add alias to shell file
-   Bash shell: _~/.bashrc_
-   Zsh shell: _~/.zshrc_
-   Fish shell: _~/.config/fish/config.fish_

```shell
# add this to the shell
alias <aliasname>='/Users/user/git.sh'
```

## reload shell
`source ~/.zshrc`
