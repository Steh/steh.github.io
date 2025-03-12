---
title: "Splunk4Admins"
categories: 
- splunk
tags:
- blue team
classes: 
- wide
excerpt: ""
toc: true
--- 

## Search under the hood
based on splunk education course "Search Under the Hood (eLearning)"

### Seach Job Inspector

open Job under Search Bar

* contains header with overall runtime
  * return Results
  * scanned Events
  * execution Time
* Execution Cost
  * what component takes the longest
  * if one takes signifitiant longer you should investigate into it
    * `command.search.index` - Time to search the index for the location to read in rawdata files
    * `command.search.filter` - Time to filter out events that do not match
    * `command.search.rawdata` - Time to read events from rawdata files 
* Search Job properties
  * diskusage
  * optimizedSearch
    * Splunk will try to optimize your search

## Comments

* three ticks
  * ` ``` `

## Splunk Architecture

* index
  * contains 
    * journal.gz
      * contains slices of rawdata, 128kb
    * .tsidx - time series index file
      * index fields to journal files
      * contains lexicon of location for stored keywords
    * Bloom Filter ([def][Splexicon: Bloom Filter])
      * rules out buckets that dont contain data
      * creates a bloomfilter (kind of a hash) and compares it to presaved filters in buckets

## Streaming vs. Non-Streaming Commands

* Transforming Commands
  * Commands that take events as input and output a transformed dataset, typically a summary or aggregation.
  * Operate on an entire result set of data
  * `stats`, `timechart`. `top` 
* Streaming Commands
  * Process each event independently and can start returning results before all data is read.
  * Centralized
    * processes data as it comes in
    * `streamstats`, `transaction`
  * Distributable
    *  operates on each event individual
    * `eval`, `rename`

[Command Types][def3]

## Breakers and Segmentation

* Events Split by major breakers
  * spaces, brackets, tab and quotation mark
* next break by minor breakers:
  * `.`, `,`, `$`,`=`

```bash
Example:
index=web clientip=76.169.7.252
  would search [AND 169 252 7 76 index::web]

# term must be break by major breakers in raw data
index=web clientip=TERM(76.169.7.252)
  would search [AND 76.169.7.252 index::web]

search can be viewd im _internal and search for LISPY

## searching in tsidx files
# search with tstats (only works if the term is not seperated by major breakers)
| tstats count where index=you_data source=StuffYouDefine TERM(Computername=MyPC)

# stats count by values
| tstats count where index=you_data source=StuffYouDefine by PREFIX(Computername=)
```

* wildcards in the middle of a string can be costly
* lispy expression can seen in search.log in Job Inspector

* [Breakers & Segmentation][def2]
* [Event segmentation and searching][def4]

## | fieldsummary

```bash
# command calculates summary statistics for one or more fields in your events. The summary information is displayed as a results table. 
...
| fieldsummary 

```

## Informational Functions

```bash
eval field1 = isnull()
```

[fieldsummary command overview][def1]

## Knowledge Objects

`Settings` -> `All configuration`

* Fields
* Calculated Fields
* Lookups
* Event types
  * categories events
  * Save search as Even Type
  * `eventtype=web_logs`
*  Tags
  * `tag=vuln`
* Workflow Actions
  * 
* Reports and Alerts
* Macros
* Data Models

## source

[def]: https://docs.splunk.com/Splexicon:Bloomfilter
[def1]: https://docs.splunk.com/Documentation/SCS/current/SearchReference/FieldsummaryCommandOverview
[def2]: https://docs.splunk.com/Documentation/Splunk/latest/Data/Abouteventsegmentation
[def4]: https://docs.splunk.com/Documentation/Splunk/latest/Search/Eventsegmentationandsearching
[def3]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Commandsbytype