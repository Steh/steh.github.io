---
layout: post
categories: PowerShell
title: 'PowerShell: Java Version anzeigen'
tags: [PowerShell, Java]
autor: StehSa
---

## PowerShell Befehl

    Get-WmiObject -Class Win32_Product -Filter "Name like 'Java%'"
