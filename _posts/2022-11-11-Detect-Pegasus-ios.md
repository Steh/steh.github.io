---
title: "Check for Pegasus on iOS"
date: 2022-11-11
categories:
- Information Security
tags:
- Pegasus
excerpt: 'How to check for Pegasus and other spyware on iOS'
---

## Investigating Pegasus on iOS

1. Create an encrypted backup using Finder.
2. Install MVT by running `pip3 install mvt`.
3. Decrypt the encrypted backup:

```bash
cd /Users/Steh/Library/Application Support/MobileSync
mvt-ios decrypt-backup Backup --destination Backup-dec`
```

4. Download the detection file from: [AmnestyTech Investigations Repository](https://github.com/AmnestyTech/investigations)
5. Verify the backup:

```bash
mvt-ios check-backup Backup-dec -o ioc_output -i pegasus.stix2 cytrox.stix2
```

## References

- [MVT IOCs Documentation](https://docs.mvt.re/en/latest/iocs/)
- [Checking iOS Backups with MVT](https://docs.mvt.re/en/latest/ios/backup/check/)
- [MVT Quick Start Guide](https://medium.com/@henry-kehler/mvt-quick-start-guide-87224a904189)
- [Heise.de: iPhones selbst auf Pegasus und andere Spyware prüfen](https://www.heise.de/hintergrund/iPhones-selbst-auf-Pegasus-und-andere-Spyware-pruefen-6143960.html)
- [AmnestyTech Investigations Repository](https://github.com/AmnestyTech/investigations)
