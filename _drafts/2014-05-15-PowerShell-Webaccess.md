---
layout: post
title: "PowerShell: WebAccess einrichten"
categories: PowerShell
tags: [PowerShell]
autor: StehSa
--- 

## PowerShell Webaccess aktivieren
    Install-PswaWebapplication

## Berechtigungsgruppen aktiveren
    Add-PswaAuthorizationRule –UserName <BenutzerName> -ComputerName <ZielComputername> -ConfigurationName microsoft.powershell
