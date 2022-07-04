---
type: post
title: "Exchange: Mit welchem ClientAccessServer bin ich verbunden?"
categories: [Exchange]
tags: [Exchange, PowerShell]
status: publish
autor: StehSa
---
    #mit welchem CAS wurde ine Verbindung aufgebaut
    Get-LogonStatistics stiki | Select-Object ClientName,ApplicationId
