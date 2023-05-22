---
title: "Splunk commands"
categories: 
- informationsecurity
tags:
- blue team
- splunk
- commands
classes: 
- wide
excerpt: "An overview of some Splunk commands"
toc: true
--- 

## where

* searchcommand to compare two fields
* Possibility to use funtions
  * isnotnull()
  * isnull()
  * like()
  * ....

```conf
# compare two field values
index=_index
| where a > b

# search for wildcards
index=perfmon counter=* 
| where counter like “%Disk%”

... | where like(ipaddress, "198.%")

# search for string in field
... | where foo="bar"
```

## references
* (Splunk Search Command of the Week: Where Command)[https://kinneygroup.com/blog/splunk-where-command/]
* (SPL2 Search Reference: where command usage)[https://docs.splunk.com/Documentation/SCS/current/SearchReference/WhereCommandUsage]