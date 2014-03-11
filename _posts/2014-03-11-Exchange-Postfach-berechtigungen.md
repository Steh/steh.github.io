---
layout: post
title: "E-Mail Adressrichtlinien Updaten (Ex2003 -> Ex2010)"
categories: Exchange
tags: []
status: draft
type: post
published: true
--- 

Der Folgende PowerShell Befehl gibt alle Adressrichtlinien die aktualisiert werden können aus.

    Get-EmailAddressPolicy | where {$_.RecipientFilterType –eq “Legacy”}
    Get-EmailAddressPolicy | Format-List Name, *RecipientFilter*, ExchangeVersion

[Microsoft Hilfeseite zur Migration in Exchange 2010](http://technet.microsoft.com/en-us/library/cc164375.aspx)
