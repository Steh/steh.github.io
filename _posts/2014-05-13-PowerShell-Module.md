---
layout: post
categories: PowerShell
title: 'PowerShell: Verfügbare Module anzeigen'
tagline: 'Verfügbare Module'
tags: [PowerShell,]
autor: StehSa
---
{% include JB/setup %}

## PowerShell Befehl
    Get-Command -module * | group ModuleName | Sort-Object Name | select Name
