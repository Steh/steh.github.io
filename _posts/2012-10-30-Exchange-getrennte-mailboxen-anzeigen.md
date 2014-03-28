---
layout: post
title: "Exchange: Getrennte Mailboxen"
tagline: 'Anzeigen und wieder einbinden'
categories: Exchange2010
tags: ['GetrennteMailbox', 'Mailbox', 'Powershell']
autor: StehSa
---

## Anzeigen

    #Gibt alle Mailboxen aus bei den DisconnectDate vorhanden ist
    Get-MailboxStatistics -server <MBX-Stiki> | Where {$_.DisconnectDate}

## Anhängen

    #Bindet eine gelöschte Mailbox wieder an einen AD Benutzer
    Connect-Mailbox -Identity <RunspaceId-der-gelöschten-Mailbox> -Database <Ziel-Datenbank> -User <ADUser> -Alias <ExchangeAlias>
