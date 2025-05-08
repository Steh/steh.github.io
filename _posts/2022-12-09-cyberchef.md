---
title:  "Cyberchef"
date:   2022-12-09
excerpt: ""
categories: informationsecurity
tags: 
- cyberchef
- blue team
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
classes: wide
---

## Examples

* change IP format (windows log is decimal and reversed)
  * from decimal to dotted decimal [see example](https://gchq.github.io/CyberChef/#recipe=Change_IP_format('Decimal','Dotted%20Decimal')&input=NjcyMTc2MDA)
    * 67217600 -> 4.1.168.192
* Malware Anaylsis
  * copy file to cyberchef
  * extract strings

## How To start

* Go to a Website
  * [https://gchq.github.io][def4]
* Download the application and start the website
  * [GitHub CyberChef releases][def3]
* Install it with nvm and start your own server

### Install on Arm64

```bash
# Install
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash

# reload shell and install latest version
nvm install node

# restart shell and activate
nvm use node

# install CyberChef and start it
git clone https://github.com/gchq/CyberChef.git
cd CyberChef
npm install

```

### apache2 proxy

```bash
# if you aren´t on the same system you can install an reverse proxy
# only for development
## install apache2
apt install apache2

## enable proxy mod
sudo a2enmod proxy
sudo a2enmod proxy_http

## add a configuration for the proxy
vim /etc/apache2/sites-availiable/cyberchef-proxy.conf

  <VirtualHost *:80>
      ProxyPass / http://localhost:8080/ nocanon
      ProxyPassReverse / http://localhost:8080/
  </VirtualHost>

# disable the default config and enable the new one
a2ensite chyberchef-proxy
a2dissite 000-default.conf

systemctl reload apache2
```

## investigating the operations

* you find all the operations in
  * ```Cyberchef/src/core/operations/```

## creating new operations

* creating new operation ([ref][def1])
  * ```npm run newop```

## Refrences

* [TryHackme Advent of Cyber Day 7](https://tryhackme.com/room/adventofcyber4)
* [macOS Big Sur: How to setup Node.js on Apple M1 Machine][def5]
* [CyberChef Workshop by didiers stevens][def2]

[def1]: https://github.com/gchq/CyberChef/wiki/Adding-a-new-operation
[def2]: https://didierstevens.com/workshop-cc.zip
[def3]: https://github.com/gchq/CyberChef/releases
[def4]: https://gchq.github.io
[def5]: https://www.jurnalanas.com/blog/node-js-mac-m1
