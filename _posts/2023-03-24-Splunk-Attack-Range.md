---
title: "Attack Range by Splunk"
categories: 
- informationsecurity
tags:
- blue team
- splunk
- atomic red team
- attack range  
classes: 
- wide
excerpt: "Attack Range is designed to simulate a real-world attack scenario, allowing security teams to test and improve their detection and response capabilities." 
toc: true
---
## How to

1. Install Attack Range
2. Create an attack_config.yml
3. build the environment
4. start your tests
5. stop the environment
6. optional: destroy your environment

## Basic commands

```bash
#Builds a new Attack Range based on your configuration in attack_range.yml
python attack_range.py build

#Destroys an Attack Range and deletes/deprovision all used ressources
python attack_range.py destroy

#Stops an Attack Range which will shutdown the instances but not deprovision it
python attack_range.py stop

# Resumes a stopped Attack Range
python attack_range.py resume

#Shows the ressources of an Attack Range
python attack_range.py show

# start attack
python attack_range.py simulate -e ART -te T1003.001 -t ar-win-ar-ar-0
```

## Installation

### Linux x64

```bash
# Download the Attack Range repository
git clone https://github.com/splunk/attack_range.git
cd attack_range

# Install VirtualBox (beta for arm) and Vagrant on MacOS ARM
brew update
brew install --cask virtualbox@beta
brew install --cask vagrant

# Install VirtualBox and Vagrant on linux
apt-get update
apt-get install virtualbox
wget https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_x86_64.deb
apt install ./vagrant_2.2.19_x86_64.deb

# Install and run Poetry
## Install all dependencies
curl -sSL https://install.python-poetry.org/ | python3 -
poetry install
poetry shell

# Configure Attack Range or copy your default config
python attack_range.py configure

# Build the lab
python attack_range.py build
```

### My attack_config.yml

* [Attack Range Configuration](https://attack-range.readthedocs.io/en/latest/Attack_Range_Config.html)

```conf
general:
  attack_range_password: "changeme"
  cloud_provider: local
  use_prebuilt_images_with_packer: "0"
  ingest_bots3_data: "1"
local:
  # Enable Enterprise Security
  install_es: "1"
  # Save to the apps folder from Attack Range
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

## Start Attack

* needs Atomic Read Team or PurpleSharp
  * Atomic Read Team Technics: [Atomics](https://atomicredteam.io/atomics/)
  * PurpleSharp Technics: [PurpleSharp](https://www.purplesharp.com/en/latest/index.html)

```bash
# start environment
poetry shell

# find the target Name
python attack_range.py show

# Start Attack
## Atomic Read Team
python attack_range.py simulate -e ART -te T1003.001 -t ar-win-ar-ar-0

## Purple Sharp with 
### MITRE ATTACK Technique
python attack_range.py simulate -e PurpleSharp -te T1003.001 -t ar-win-ar-ar-0

### MITRE ATTACK Technique
python attack_range.py simulate -e PurpleSharp -te T1003.001, -t ar-win-ar-ar-0

### Playbook
python attack_range.py simulate -e PurpleSharp -sp threat_actor_simulation.json  -t ar-win-ar-ar-0

### Example Playbook
{
"type": "local",
"sleep": 5,
"playbooks": [
   {
      "name": "Process Injection Simulation Playbook",
      "enabled": true,
      "tasks": [
      {
         "technique_id": "T1055.002",
         "variation": 1
      },
      {
         "technique_id": "T1055.003",
         "variation": 1
      },
      {
         "technique_id": "T1055.004",
         "variation": 1
      }
      ]
   }
]
} 
```

Other Examples for PurpleSharp: [mvelazc0@github: PurpleSharp PurpleTeamPlaybooks](https://github.com/mvelazc0/PurpleTeamPlaybook.git)

## Debuging

* If you get an error while building, destroy the build and start over
  * ```python attack_range.py destroy```
* To allow the Adressrange from attack_range

```conf
# /etc/vbox/networks.conf
* 0.0.0.0/0 ::/0
```

## Applications Used

* **Vagrant**: A lightweight, reproducible, and portable virtual development environment creation and configuration tool.
* **Poetry**: A Python dependency management and packaging tool.
* **VirtualBox**: A virtualization platform for creating and running virtual machines on your computer.
* **Ansible**: An automation tool for configuration management, application deployment, and infrastructure provisioning.
* **Atomic Red Team**: A framework designed for testing endpoint detection and response (EDR) and other security controls.
* **PurpleSharp**: A Microsoft tool that simulates adversary techniques based on the MITRE ATT&CK framework in a Windows environment.

## sources

* [Github Splunk Attack Range](https://github.com/splunk/attack_range)
* [Attack Range Local](https://attack-range.readthedocs.io/en/latest/Attack_Range_Local.html)
* [Detecting CVE-2020-1472 (CISA ED 20-04) Using Splunk Attack Range](https://www.splunk.com/en_us/blog/security/detecting-cve-2020-1472-using-splunk-attack-range.html)
* [Atomic Red Team: Atomics](https://atomicredteam.io/atomics/)
* [PurpleSharp](https://www.purplesharp.com/en/latest/)
* [PurpleSharp GitHub](https://github.com/mvelazc0/PurpleSharp)
* [PurpleSharp: Active Directory Purple Team Playbook](https://github.com/mvelazc0/PurpleAD)
* [Youtube: AttackRange + PurpleSharp Integration](https://www.youtube.com/watch?v=XV_hnNv69gY&t=41s)
* [Python Poetry](https://python-poetry.org/)
* [Prelude Security](https://www.preludesecurity.com/)
* [Virtualbox: 6.7. Host-Only Networking](https://www.virtualbox.org/manual/ch06.html)
* [Vagrant: Getting Started](https://www.vagrantup.com/intro/getting-started)
* [Vagrant: Networking](https://www.vagrantup.com/docs/networking)
