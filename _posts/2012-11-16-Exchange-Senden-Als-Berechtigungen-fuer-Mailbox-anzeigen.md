---
layout: post
title: Exchange: Senden-Als Berechtigungen für Mailbox anzeigen
categories: [Exchange]
tags: []
meta:
  _publicize_pending: '1'
  original_post_id: '78'
  _wp_old_slug: '78'
  _elasticsearch_indexed_on: '2012-11-16 10:31:50'
---
  Get-Mailbox <MAILBOX> | Get-ADPermission | where {($_.ExtendedRights -like "*Send-As*")} | Fl
