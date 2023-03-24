---
title: "Splunk: Attack Range"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 
# attack_config.ym
* (Attack Range Configuration)[https://attack-range.readthedocs.io/en/latest/Attack_Range_Config.html]

## to install ES
* add the following to your config and copy the install file to the apps folder
```bash
splunk_server:
  ...
  install_es: "1"
  splunk_es_app: "splunk-enterprise-security_701.spl"
  ...
```

# Installation
## Linux x64
```bash
# download repo
git clone https://github.com/splunk/attack_range.git
cd attack_range

# install virtualbox and vagrant
apt-get update
apt-get install virtualbox
wget https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_x86_64.deb
apt install ./vagrant_2.2.19_x86_64.deb

# install and run poetry
curl -sSL https://install.python-poetry.org/ | python -
poetry shell
poetry install

# configure attack_range or copy your default config
python attack_range.py configure

# build lab
python attack_range.py build

```

# Start Attack
```bash
python attack_range.py simulate -e ART -te T1003.001 -t ar-win-ar-ar-0
python attack_range.py simulate -e PurpleSharp -te T1003.001 -t ar-win-ar-ar-0
```

# Debuging
* If you get an error while building, destroy the build and start over
    * ```python attack_range.py destroy```
* If you get an error about Network change the IPs used
    * ```bash
# On ERROR change IP from the machines
## vim attack_range/vagrant/<system>_server/Vagrantfile
10.0.1.XX -> 192.168.56.XX```

# references
* (Github Splunk Attack Range)[https://github.com/splunk/attack_range]
* (Attack Range Local)[https://attack-range.readthedocs.io/en/latest/Attack_Range_Local.html]
* (Detecting CVE-2020-1472 (CISA ED 20-04) Using Splunk Attack Range )[https://www.splunk.com/en_us/blog/security/detecting-cve-2020-1472-using-splunk-attack-range.html]
