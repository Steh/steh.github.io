---
layout: post
title: 'Exchange: Verteilerlsiten'
categories: Exchange
tags:['Powershell', 'Verteilerliste','Verwaltungskonsole']
autor: StehSa
---
## Listen extern vefügbar machen
### Exchange Verwaltungs Konsolen:

1. Eigenschaften</li>
2. Nachrichtenübermittlungseinstellungen</li>
3. “Einstellungen für die Nachrichtenzustellung” </li>
4. “Authentifizierung aller Absender anfordern” dort Haken entfernen</li>

### PowerShell:

    Set-DistributionGroup -BypassSecurityGroupManagerCheck -RequireSenderAuthenticationEnabled:$false -Identity <Name-der-VerteilerGruppe>
