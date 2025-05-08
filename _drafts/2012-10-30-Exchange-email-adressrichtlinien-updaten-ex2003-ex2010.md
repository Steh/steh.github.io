---
layout: single
title: "Exchange: Legacy E-Mail Adressrichtlinien"
tagline: "Ausgeben und Updaten"
categories: Exchange2010
tags: ['AdressListen', 'PowerShell']
autor: StehSa
--- 

# Der folgende PowerShell-Befehl gibt alle Adressrichtlinien aus, die aktualisiert werden können.

```powershell
# Legacy Adressrichtlinien ausgeben
Get-EmailAddressPolicy | Where-Object {$_.RecipientFilterType -eq "Legacy"}
Get-EmailAddressPolicy | Format-List Name, *RecipientFilter*, ExchangeVersion

# Nach Exchange 2010 übertragen
Get-EmailAddressPolicy | Set-EmailAddressPolicy -RecipientFilter <FILTER>

# Listen aktualisieren
Get-EmailAddressPolicy | Update-EmailAddressPolicy
```

[Microsoft-Hilfeseite zur Migration in Exchange 2010](http://technet.microsoft.com/en-us/library/cc164375.aspx)