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

* search command to compare two fields
* Possibility to use functions
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

## Metadata

When you want to know the time data were writen to an Index/sourcetype you can use metadata.

```bash
# show the metadata lastTime, firstTime and recentTime for the sourcetype
| metadata type=sourcetypes index=_internal 

# format the output to human readable
| metadata type=sourcetypes index=_internal 
| rename totalCount as Count firstTime as "First Event" lastTime as "Last Event" recentTime as "Last Update" 
| fieldformat Count=tostring(Count, "commas") 
| fieldformat "First Event"=strftime('First Event', "%c") 
| fieldformat "Last Event"=strftime('Last Event', "%c") 
| fieldformat "Last Update"=strftime('Last Update', "%c")
```

[Splunk Documentation][def3]

## references

* [Splunk Search Command of the Week: Where Command](https://kinneygroup.com/blog/splunk-where-command/)
* [SPL2 Search Reference: where command usage](https://docs.splunk.com/Documentation/SCS/current/SearchReference/WhereCommandUsage)
* [Docs Splunk: | metadata][def3]

[def3]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Metadata
