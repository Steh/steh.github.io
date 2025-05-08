---
layout: post
categories: PowerShell
title: 'PowerShell: IIS Befehle'
tags: [PowerShell, IIS]
autor: StehSa
---

## Verfügbare Befehle
    Get-Command -PSSnapin WebAdministration

## Verschiedenes
    # WebApplicationen anzeigen
    Get-WebApplication
    
    # Webseite
    Get-Website
    
    # Bindungen
    Get-WebBinding
    
    # Web Konfigurations Datei
    Get-WebConfigFile
    
    # Web Zertifikat Server (2012)
    Get-WebCentralCertProvider
