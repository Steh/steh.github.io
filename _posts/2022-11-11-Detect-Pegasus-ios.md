---
layout: post
title:  "Pegasus unter IOS untersuchen"
date:   2022-11-11
categories: pegasus
---
# Pegasus unter IOS untersuchen
1. verschlüsseltes Backup über den Finder anlegen
2. MVT installieren ``pip3 install mvt``
3. verschlüsseltes Backup entschlüsseln: 
    ``cd /Users/Steh/Library/Application Support/MobileSync
    mvt-ios decrypt-backup Backup --destination Backup-dec``
4. Erkennungsfile Downloaden: https://github.com/AmnestyTech/investigations
5. Backup überprüfen
``mvt-ios check-backup Backup-dec -o ioc_output -i pegasus.stix2 cytrox.stix2``

* https://docs.mvt.re/en/latest/iocs/
* https://docs.mvt.re/en/latest/ios/backup/check/
* https://medium.com/@henry-kehler/mvt-quick-start-guide-87224a904189
* https://www.heise.de/hintergrund/iPhones-selbst-auf-Pegasus-und-andere-Spyware-pruefen-6143960.html
* https://github.com/AmnestyTech/investigations