---
title: "MISP2Splunk"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

## Installation

´´´bash
### generate temp install user
sudo useradd misp-install --no-create-home -G sudo -s /bin/bash
sudo passwd misp-install
sudo su misp-install

### -A stands for: install all features
wget -O /tmp/INSTALL.sh https://raw.githubusercontent.com/MISP/MISP/2.4/INSTALL/INSTALL.sh
bash /tmp/INSTALL.sh -A

### save your passwords and remove the files afterwards
rm MISP-authkey.txt mysql.txt

### remove install user
sudo userdel misp-install

## Probleme
# bei Problemen von vorne anfangen
rm -rf /var/www/MISP

# Add directory to safe.directory
git config --system --add safe.directory /usr/local/src/misp-modules

# wenn Datenbank verbindung nicht hergestellt werden kann manuelle setzen
sudo mysql -u root -p -e "grant all on misp.* to misp@localhost identified by 'MISP-DB-Password';"
sudo mysql -u root -p -e "flush privileges;"

# credentials anpassen
vim /var/www/MISP/app/Config/database.php

# ordner existiert
rm -rf /usr/local/src/faup

# Datenbank einrichten
mysql -u root -p

mysql> create database misp;
mysql> grant usage on . to misp@localhost identified by 'misp password';
mysql> grant all privileges on misp.* to misp@localhost;
mysql> exit

# Import the empty MySQL database from MYSQL.sql
# https://github.com/MISP/MISP/blob/2.4/INSTALL/MYSQL.sql
mysql -u misp -p misp < INSTALL/MYSQL.sql
https://github.com/MISP/MISP/issues/7952
https://github.com/MISP/MISP/blob/2.4/INSTALL/INSTALL.sh
´´´

## source

* [Text][def]

[def]: https://www.misp-project.org/best-practices-in-threat-intelligence.html