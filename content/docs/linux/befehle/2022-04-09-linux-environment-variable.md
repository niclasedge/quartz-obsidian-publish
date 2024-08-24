---
slug: linux-environment-variable
title: Umgebungsvariablen
date: 2022-04-09
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
- Umgebungsvariable
images:
- images/linux.png
---

## Linux: Environment Variable

### Umgebungsvariable definieren in Linux

```
export EMAIL=meineemail@googlemail.com
```

### Variable anzeigen

```
printenv EMAIL # meineemail@googlemail.com
```

## Umgebungsvariable nutzen

#### Variable in Docker Compose Datei nutzen:

```
---
version: "3.1"
services:
  code-server:
    image: lscr.io/linuxserver/code-server
    container_name: code-server
    environment:     
      - PASSWORD=${MAIL_PASSWORD} #nutzt die Umgebungsvariable
```

#### Variable in Python Datei nutzen

```
import os

mail = os.environ.get('EMAIL')

print(mail) # prints meineemail@googlemail.com
```

## Variable in Datei speichern

1.  Man schreibt die Variable in eine Datei (zum Beispiel `~/.bashrc`)
    -   `export VARIABLE_NAME=variablen-text`
2.  Man läd die Datei neu ein via `source ~/.bashrc`

___

You can add it to the file `.profile` or your login shell profile file (located in your home directory).

To change the environmental variable "permanently" you'll need to consider at least these situations:

1.  Login/Non-login shell
2.  Interactive/Non-interactive shell

### bash

1.  Bash as login shell will load `/etc/profile`, `~/.bash_profile`, `~/.bash_login`, `~/.profile` in the order
2.  Bash as non-login interactive shell will load `~/.bashrc`
3.  Bash as non-login non-interactive shell will load the configuration specified in environment variable `$BASH_ENV`

```
$EDITOR ~/.profile
#add lines at the bottom of the file:  
     export LD_LIBRARY_PATH=/usr/lib/oracle/11.2/client64/lib
     export ORACLE_HOME=/usr/lib/oracle/11.2/client64
```

### zsh

```
$EDITOR ~/.zprofile
#add lines at the bottom of the file:  
     export LD_LIBRARY_PATH=/usr/lib/oracle/11.2/client64/lib
     export ORACLE_HOME=/usr/lib/oracle/11.2/client64
```

### fish

```
set -Ux LD_LIBRARY_PATH /usr/lib/oracle/11.2/client64/lib
set -Ux ORACLE_HOME /usr/lib/oracle/11.2/client64
```

### ksh

```
$EDITOR ~/.profile
#add lines at the bottom of the file:  
     export LD_LIBRARY_PATH=/usr/lib/oracle/11.2/client64/lib
     export ORACLE_HOME=/usr/lib/oracle/11.2/client64
```

### bourne

```
$EDITOR ~/.profile
#add lines at the bottom of the file:  
     LD_LIBRARY_PATH=/usr/lib/oracle/11.2/client64/lib     
     ORACLE_HOME=/usr/lib/oracle/11.2/client64
     export LD_LIBRARY_PATH ORACLE_HOME
```

### csh or tcsh

```
$EDITOR ~/.login
#add lines at the bottom of the file:  
     setenv LD_LIBRARY_PATH /usr/lib/oracle/11.2/client64/lib
     setenv ORACLE_HOME /usr/lib/oracle/11.2/client64
```
