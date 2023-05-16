---
layout: post
title: "Exchange: Arbitration Mailbox verschieben"
description: "Was sind Arbitration Mailboxen und wie werden diese Behandelt"
category: Exchange
tags: ["Arbitration","Move-Request"]
---

## Was sind diese "Arbitration" Mailboxen

    Arbitration = Vermittlung

Sind Vermittlungspostfächer die zum speichern von organisationsweiten Daten verwendet werden. 
zum Beispiel: Administrator-Überwachungsprotokolle, eDiscovery-Suchmetadaten, Unified Messaging-Daten

Arbitration mailboxen werden beim Anlegen der Exchange Organisation erstellt.

Listen von Arbitration Mailboxen:
* Microsoft Exchange Approval Assistant
* Microsoft Exchange
* Discovery Search Mailbox
* Microsoft Exchange Federation Mailbox

## PowerShell Befehle 

    # Mailboxen anzeigen
    Get-Mailbox -Arbitration
    
    # letzte Systemmailbox löschen
    Get-Mailbox -Arbitration | Remove-Mailbox -Arbitration -RemoveLastArbitrationMailboxAllowed


## Mailboxen verschieben
Wenn die Server auf denen die Arbitration Mailboxen liegen gelöscht werden müssen die Mailboxen verschoben werden.

   
## Funktion Testen
Überprüfen ob folgedenes Problemlos möglich ist

    # Cmdlet ausführen
    Search-AdminAuditLog


## Quelle
[Technet: Verschieben des Exchange 2010-Systempostfachs nach Exchange 2013](http://technet.microsoft.com/de-de/library/dn249849%28v=exchg.150%29.aspx "Technet: Verschieben des Exchange 2010-Systempostfachs nach Exchange 2013")
