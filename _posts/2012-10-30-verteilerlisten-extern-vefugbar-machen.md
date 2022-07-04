---
layout: post
title: "Exchange: Verteilerlisten"
categories: Exchange
tags: ['Powershell', 'Verteilerlisten', 'Verwaltungskonsole']
autor: StehSa
---

## Listen extern vefügbar machen
### Exchange Verwaltungs Konsolen:

1. Eigenschaften
2. Nachrichtenübermittlungseinstellungen
3. “Einstellungen für die Nachrichtenzustellung”
4. “Authentifizierung aller Absender anfordern” dort Haken entfernen

### PowerShell:

    Set-DistributionGroup -BypassSecurityGroupManagerCheck -RequireSenderAuthenticationEnabled:$false -Identity <Name-der-VerteilerGruppe>
