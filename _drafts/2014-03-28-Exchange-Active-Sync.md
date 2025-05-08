---
layout: post
title: 'Exchange: nicht mehr gültige ActiveSync Geräte entfernen'
category: Exchange2010
tagline: "Geräte die älter länger als 90 Tage nicht Synchronisiert haben, entfernen."
tags : [Exchange, ActiveSync]
autor: StehSa
---


## PowerShell Befehle
    # Alle ActiveSync Geräte anzeigen die länger als 90 Tage nicht Synchronisiert wurden, löschen!
    Get-ActiveSyncDevice -ResultSize unlimited | Get-ActiveSyncDeviceStatistics | where {$_.LastSyncAttemptTime -lt (get-date).adddays(-90)} | Remove-ActiveSyncDevice

# Quelle
[ldap389.info: powershell-remove-stale-activesync-mobile-device-partnerships-exchange](http://www.ldap389.info/en/2012/07/31/powershell-remove-stale-activesync-mobile-device-partnerships-exchange/)
