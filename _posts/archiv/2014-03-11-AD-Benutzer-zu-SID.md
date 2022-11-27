---
layout: post
title: "Active Directory: Benutzer zu SID anzeigen"
categories: Outlook
tags: ["ActiveDirectory", "SID"]
--- 


## Global Catalog Server herausfinden

    Get-ADForest | fl GlobalCatalogs

## User zu SID suchen

    Get-ADUser -Filter {SID -like "<SID>"} -Server <GLOBAL-CATALOG>:3268 | Select Name,SID | Format-Table -Auto
