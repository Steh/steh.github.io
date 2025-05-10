---
title: "Splunk basics from Splunk4Champions"
categories: 
  - informationsecurity
tags:
  - blue team
classes: 
  - wide
excerpt: ""
toc: true
date: 2023-10-24
---

This page is based on the app [Splunk4Champions][def]

## searchmodes

* *Fast mode* uses the least amount of system resources. It is great to use Fast Mode when merely checking if data is present or not or after a search is already built.
* *Smart mode* is best when exploring data, as it will only pull back raw events if there are no transforming commands in the search, and will display any field extractions in the events. If there are transforming commands like stats, chart, or timechart in the search, it will only return the aggregated/transformed events. This saves on system resources and results in faster searches.
* *Verbose mode* returns as much information as possible from the data, including all events and field information.

## format search

```bash
## reformat
# Linux & Windows:
Ctrl + Shift + F

# Mac
Command + Shift + F

## expand macros
# Linux & Windows
Ctrl + Shift + E

# Mac
Command + Shift + E
```

## supported languages

```bash
German          de-DE
English         en-GB
English-US      en-US
French          fr-FR
Italian         it-IT
Japanese        ja-JP
Korean          ko-KR
Chinese simpl.  zh-CN
Chinese trad.   zh-TW
```

## Using Job inspector to optimize searches

```bash
## open Job inspector
Job -> Inspect Job

    "command.search.index" -> time to read the idx files
    "command.search.rawdata" -> time to read rawdata
    "command.search.filter" -> time to filter non-matching events
    "command.search.kv" -> field extractions (matching field -> values)
    "command.search.typer" -> processing event types

## search propertys
optimizedSearch - shows an optimized search version
```

* [youtube: Using the Splunk Search Job Inspector in Splunk Enterprise 6.X][def2]
* [youtube: Remastered - Job Inspector ramblings - Martin Mueller][def3]
* [splunk: Built-in optimization][def4]
* [splunk: Clara-fication: Search Best Practices][def5]

## optimze search

1. Only search in the index you need
1. Restrict time range
1. Always think about the number of buckets to open
1. Tell exactly what you want (before the first pipe)
1. Try to reduce the scan count
1. Lispy Efficiency
1. Avoid using wildcards as prefixes or in the middle of the string (breaks bloomfilter)

## TERMS

* [splunk.com: Use CASE() and TERM() to match phrases][def6]
* **CASE()**
  * Matches case-sensitive values
  * Exmaple: **host=CASE(LOCALHOST)**
* **TERM()**
  * searches more effictively
  * TERM can only be used with minor breakers, not with major breakers
  * you can see what you can put in TERM() by move the mouse over the log terms, whatever you can highlight in one peace contains only minor breakers and can be used with TERM or PREFIX directives

## how is data stored?

* bloomfilter
* tsidx
* journal.gz

## search comand types

* streaming commands should always appear bevor transforming commands
* Streaming commands
  * eval, fields, head, iplocation, replace...
* Transforming commands
  * addtotals, chart, mvcombine, rare, stats, table, timechart, top...

## tstats

* `tstats`` command performs statistical queries on indexed fields in tsidx files. The indexed fields can be from indexed data or accelerated data models.

## Searching Metrics

* mcatalog
* mstats
* mpreview

## source

* [github.com - Splunk4Champions][def]

[def]: https://github.com/bautt/splunk4champions2
[def2]: https://www.youtube.com/watch?v=n3OqaB6GVXs
[def3]: https://www.youtube.com/watch?v=1QCZ5klSptM
[def4]: https://docs.splunk.com/Documentation/Splunk/latest/Search/Built-inoptimization
[def5]: https://www.splunk.com/en_us/blog/customers/splunk-clara-fication-search-best-practices.html?locale=en_us
[def6]: https://docs.splunk.com/Documentation/Splunk/latest/Search/UseCASEandTERMtomatchphrases
