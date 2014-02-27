---
layout: post
title: "Exchange: IMAP Verbindung testen"
description: "Wie können IMAP verbindungen überprüft werden"
category: Exchange
tags: ["IMAP","Telnet"]
autor: Steh Sa
---
## Telnet
CMD/PowerShell öffnen
    # Unverschlüsselt
    telnet <SERVER-IP> 143
    
    # Verschlüsselt (SSL)
    telnet <SERVER-IP> 993

Sollte kein Wenn möglich nun das AnwendungsLog auf Fehlerüberprüfen.

## Quelle
[Webstersprodigy: Powershell Portscanner](http://webstersprodigy.net/2013/07/01/powershell-portscanner/ "Webstersprodigy: Powershell Portscanner")
[Github: Invoke-Portscan](https://github.com/webstersprodigy/PowerSploit/blob/Portscan/Recon/Invoke-Portscan.ps1 "Github: Invoke-Portscan")
