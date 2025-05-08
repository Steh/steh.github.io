---
layout: post
title: "Exchange: IMAP Verbindung testen"
description: "Wie können IMAP verbindungen überprüft werden"
category: Exchange
tags: ["IMAP","Telnet"]
autor: Steh Sa
---

## IMAP Config ausgeben
Exchange PowerShel öffnen

    Get-ExchangeServer <ServerName> | Get-ImapSettings

## Telnet
CMD/PowerShell öffnen

    # Unverschlüsselt
    telnet <SERVER-IP> 143
    
    # Verschlüsselt (SSL)
    telnet <SERVER-IP> 993

Sollte ein Fehler auftreten, Wenn möglich nun das AnwendungsLog auf Fehler überprüfen.

Wenn die Verbindung aufgebaut werden kann, wird folgendes ausgeschrieben:
    
    * OK Microsoft Exchange Server 2003 IMAP4rev1 server version 6.5.7638.1

## Quelle
[Webstersprodigy: Powershell Portscanner](http://webstersprodigy.net/2013/07/01/powershell-portscanner/ "Webstersprodigy: Powershell Portscanner")

[Github: Invoke-Portscan](https://github.com/webstersprodigy/PowerSploit/blob/Portscan/Recon/Invoke-Portscan.ps1 "Github: Invoke-Portscan")

[MSXFaq: Mail im Internet - IMAP4-Telnet](http://www.msxfaq.de/internet/imap4telnet.htm "MSXFaq: Mail im Internet - IMAP4-Telnet")
