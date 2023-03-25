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
# Example attack_config.ym
* [Attack Range Configuration](https://attack-range.readthedocs.io/en/latest/Attack_Range_Config.html)

```bash
general:
  attack_range_password: "changeme"
  cloud_provider: local
  use_prebuilt_images_with_packer: "0"
  ingest_bots3_data: "1"
local:
  install_es: "1"
  splunk_es_app: "splunk-enterprise-security_701.spl"
kali_server:
  kali_server: "1"
windows_servers:
- hostname: ar-win-dc
  windows_image: windows-2019-v3-0-0
  create_domain: '1'
  install_red_team_tools: '1'
  bad_blood: '1'
- hostname: ar-win-2
  windows_image: windows-2016-v3-0-0
  join_domain: '1'
  install_red_team_tools: '1'
linux_servers:
- hostname: ar-linux
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
## Installs all dependencys
curl -sSL https://install.python-poetry.org/ | python -
poetry install
poetry shell

# configure attack_range or copy your default config
python attack_range.py configure

# build lab
python attack_range.py build

```
## install Enterprice Security
* add the following to your config and copy the install file to the apps folder
```bash
splunk_server:
  install_es: "1"
  splunk_es_app: "splunk-enterprise-security_701.spl"
```
# Important Commands
```bash

```

# Start Attack
* needs Atomic Read Team or PurpleSharp
  * Atomic Read Team Technics: [Atomics](https://atomicredteam.io/atomics/)
  * PurpleSharp Technics: [PurpleSharp](https://www.purplesharp.com/en/latest/index.html)

```bash
# find the target Name
python attack_range.py show

# Start Attack
## Atomic Read Team
python attack_range.py simulate -e ART -te T1003.001 -t ar-win-ar-ar-0

## Purple Sharp with 
python attack_range.py simulate -e PurpleSharp -te T1003.001 -t ar-win-ar-ar-0
python attack_range.py simulate -e PurpleSharp -sp threat_actor_simulation.json  -t ar-win-ar-ar-0
```

# Debuging
* If you get an error while building, destroy the build and start over
    * ```python attack_range.py destroy```
* If you get an error about Network change the IPs used
```bash
# On ERROR change IP from the machines
## vim attack_range/vagrant/<system>_server/Vagrantfile
10.0.1.XX -> 192.168.56.XX
```

# Used Applications
* Vagrant
* Poetry
  * "is a tool for dependency management and packaging in Python. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you."
* VirtualBox
* Atomic Red Team
* PurpleSharp
# references
* [Github Splunk Attack Range](https://github.com/splunk/attack_range)
* [Attack Range Local](https://attack-range.readthedocs.io/en/latest/Attack_Range_Local.html)
* [Detecting CVE-2020-1472 (CISA ED 20-04) Using Splunk Attack Range ](https://www.splunk.com/en_us/blog/security/detecting-cve-2020-1472-using-splunk-attack-range.html)
* [Atomic Red Team: Atomics](https://atomicredteam.io/atomics/)
* [PurpleSharp](https://www.purplesharp.com/en/latest/)
* [PurpleSharp GitHub](https://github.com/mvelazc0/PurpleSharp)
* [PurpleSharp: Active Directory Purple Team Playbook](https://github.com/mvelazc0/PurpleAD)
* [Youtube: AttackRange + PurpleSharp Integration](https://www.youtube.com/watch?v=XV_hnNv69gY&t=41s)
* [Python Poetry](https://python-poetry.org/)
* [Prelude Security](https://www.preludesecurity.com/)