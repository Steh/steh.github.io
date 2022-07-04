---
type: post
layout: post
title: "Exchange: Funktionspostfächer administrieren"
description: "Erstellen und Administrieren von Funktionpostfächern mit der PowerShell"
category: Exchange
tags: ["Exchange", "PowerShell", "Funktionpostfächer", "Shared-Mailbox"]
---

## Erstellen von Funktionspostfächern

    # benötigte Werte ausgeben
    Get-Mailbox <mailbox> -RecipientTypeDetails:SharedMailbox | Select Name,UserPrincipalName,Database,OrganizationalUnit
    
    #Neues Funktionspostfach
    New-Mailbox -UserPrincipalName <alias>@<domain> -Alias <alias> -Name <Name> -Database <Database> -OrganizationalUnit <OrganisationalUnit> -Shared

    # User-Mailbox -> Funktionspostfach
    Get-Mailbox  | Set-Mailbox -type Shared
    
    # Funktionspostfach -> User-Mailbox
    Get-Mailbox  | Set-Mailbox -type Regular

## Rechte vergeben
### Vollzugriff
Vergibt Vollzugriff auf alle Unterordner eines bestimmten Postfachs und zeigt es Automatisch in Outlook an.

    Add-MailboxPermission -Identity <Funktionspostfach> -User <Benutzer> -AccessRights Fullaccess -InheritanceType all -Automapping $true

### Senden Als

    Add-MailboxPermission -Identity <Funktionspostfach> -User <Benutzer> -ExtendedRights 'Send-as'

### Manager

    Set-User -IgnoreDefaultScope -Identity <Funktionspostfach> -Manager <Benutzer> 
