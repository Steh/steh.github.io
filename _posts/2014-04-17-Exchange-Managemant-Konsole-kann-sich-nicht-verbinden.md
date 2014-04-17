---
layout: post
categories: Exchange
title: 'Exchange: Exchange Management Konsole kann sich nicht verbinden'
tagline: 'Server wurde gelöscht oder ist nicht mehr aktiv'
tags: [Exchange, Regedit, ManagementKosole]
autor: StehSa
---
{% include JB/setup %}

## Fehlermeldung
![Fehlermeldung]({{ site.url }}\resources\2014-04-17-Exchange-Managemant-Konsole-kann-sich-nicht-verbinden_1.png)

## Folgendes durchführen
1. Folgende Datei Löschen
    C:\Users\<User>\AppData\Roaming\Microsoft\MMC\Exchange Management Console
2. Folgenden Registry Schlüssel entfernen
    [HKEY_CURRENT_USER\Software\Microsoft\ExchangeServer\v14\AdminTools] NodeStructureSettings
3. Exchange Management Konsole ausführen
{{ site.url }}

## Quelle
[windowsitpro.com: Creating Remote Sessions...](http://windowsitpro.com/scripting/creating-remote-sessions-powershell-20)
