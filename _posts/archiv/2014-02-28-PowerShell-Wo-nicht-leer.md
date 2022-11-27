---
layout: post
title: "PowerShell: Where not empty"
description: "Leere Werte rausfiltern"
category: PowerShell
tags: ["PowerShell"]
autor: Steh Sa
---

## Befehle
    
    # Ausgeben wo Company nicht leer
    Get-User stehsa | Where {$_.Company}
    
    # Ausgeben wo Company leer
    Get-User stehsa | Where {!$_.Company}
    


## Quelle

[jdhitsolutions.com: Filtering Empty Values in PowerShell](http://jdhitsolutions.com/blog/2011/08/filtering-empty-values-in-powershell/ "jdhitsolutions.com: Filtering Empty Values in PowerShell")
