---
layout: post
categories: WinServer2012
title: 'WinServer2012: Remote Session spiegeln'
tags: [WinServer2012, MSTSC]
autor: StehSa
---
{% include JB/setup %}

# Session Spiegeln
    mstsc /v:<ZIEL-IP> /shadow:<Session-ID> /noconsentprompt
# Session-ID Anzeigen
    quser
