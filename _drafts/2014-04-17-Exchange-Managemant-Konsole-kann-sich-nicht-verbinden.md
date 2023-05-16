---
layout: post
categories: Exchange
title: 'Exchange: Exchange Management Konsole kann sich nicht verbinden'
tagline: 'Server wurde gelöscht oder ist nicht mehr aktiv'
tags: [Exchange, Regedit, ManagementKonsole]
autor: StehSa
---

## Fehlermeldung
![Fehlermeldung](http://steh.github.io/resources/2014-04-17-Exchange-Managemant-Konsole-kann-sich-nicht-verbinden_1.png)

## Fehlerbehebung
Folgende Datei löschen
    
    # Datei löschen
    C:\Users\<User>\AppData\Roaming\Microsoft\MMC\Exchange Management Console

Folgenden Registry Schlüssel entfernen

    # mit Regedit entfernen
    [HKEY_CURRENT_USER\Software\Microsoft\ExchangeServer\v14\AdminTools] NodeStructureSettings
    
    # per PowerSehell
    Remove-ItemProperty -Path HKCU:\Software\Microsoft\ExchangeServer\v14\AdminTools\ -Name NodeStructureSettings

Exchange Management Konsole ausführen

## Quelle

[Technet](http://social.technet.microsoft.com/Forums/en-US/7eb73a50-a5db-4393-a9af-10cff4d670ff/emc-onpremises-is-trying-to-connect-to-old-server?forum=exchange2010)

[KB2019500: XADM/Exch2010/ Exchange EMC cannot access the AD configuration data ](http://support.microsoft.com/kb/2019500)
