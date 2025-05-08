---
title: "Splunk4Admins"
categories: 
  - splunk
tags:
  - blue team
classes: 
  - wide
excerpt: "A guide for Splunk administrators covering search optimization, architecture, and commands."
toc: true
date: 2024-09-24
---

## Search Under the Hood

Based on the Splunk education course "Search Under the Hood (eLearning)."

### Search Job Inspector

Open the Job Inspector under the search bar to analyze search performance:

* **Header**: Displays overall runtime details:
  * Returned Results
  * Scanned Events
  * Execution Time
* **Execution Cost**: Identifies which components take the longest:
  * `command.search.index` - Time to search the index for rawdata file locations.
  * `command.search.filter` - Time to filter out events that do not match.
  * `command.search.rawdata` - Time to read events from rawdata files.
* **Search Job Properties**:
  * Disk usage
  * Optimized Search: Splunk attempts to optimize your search automatically.

## Comments in Splunk

Use triple backticks for comments in Splunk:

```bash
# Example:
```
```

## Splunk Architecture

Understand the components of an index:

* **Index**:
  * Contains:
    * `journal.gz`: Slices of rawdata, 128 KB each.
    * `.tsidx`: Time series index file.
      * Indexes fields to journal files.
      * Contains a lexicon of stored keyword locations.
    * **Bloom Filter** ([Splexicon: Bloom Filter][def]):
      * Rules out buckets that do not contain data.
      * Creates a bloom filter (a type of hash) and compares it to pre-saved filters in buckets.

## Streaming vs. Non-Streaming Commands

* **Transforming Commands**:
  * Take events as input and output a transformed dataset (e.g., summary or aggregation).
  * Operate on the entire result set.
  * Examples: `stats`, `timechart`, `top`.
* **Streaming Commands**:
  * Process each event independently and can return results before all data is read.
  * **Centralized**:
    * Processes data as it comes in.
    * Examples: `streamstats`, `transaction`.
  * **Distributable**:
    * Operates on each event individually.
    * Examples: `eval`, `rename`.

[Command Types][def3]

## Breakers and Segmentation

* Events are split by **major breakers**:
  * Spaces, brackets, tabs, and quotation marks.
* Further split by **minor breakers**:
  * `.`, `,`, `$`, `=`.

```bash
# Example:
index=web clientip=76.169.7.252
# Searches as: [AND 169 252 7 76 index::web]

# To search for an exact term:
index=web clientip=TERM(76.169.7.252)
# Searches as: [AND 76.169.7.252 index::web]
```

* Use `tstats` for efficient searches in `.tsidx` files:

```bash
# Search with tstats:
| tstats count where index=your_data source=StuffYouDefine TERM(Computername=MyPC)

# Stats count by values:
| tstats count where index=your_data source=StuffYouDefine by PREFIX(Computername=)
```

* Avoid wildcards in the middle of strings as they are costly.
* Lispy expressions can be viewed in `search.log` via the Job Inspector.

[Breakers & Segmentation][def2]  
[Event Segmentation and Searching][def4]

## `| fieldsummary` Command

```bash
# Calculates summary statistics for one or more fields in your events.
| fieldsummary
```

[fieldsummary Command Overview][def1]

## Informational Functions

```bash
# Example:
eval field1 = isnull()
```

## Knowledge Objects

Access via `Settings` -> `All Configurations`:

* **Fields**
* **Calculated Fields**
* **Lookups**
* **Event Types**:
  * Categorize events.
  * Save searches as event types (e.g., `eventtype=web_logs`).
* **Tags**:
  * Example: `tag=vuln`.
* **Workflow Actions**
* **Reports and Alerts**
* **Macros**
* **Data Models**

## Sources

* [Splexicon: Bloom Filter][def]
* [fieldsummary Command Overview][def1]
* [Breakers & Segmentation][def2]
* [Event Segmentation and Searching][def4]
* [Command Types][def3]

[def]: https://docs.splunk.com/Splexicon:Bloomfilter  
[def1]: https://docs.splunk.com/Documentation/SCS/current/SearchReference/FieldsummaryCommandOverview  
[def2]: https://docs.splunk.com/Documentation/Splunk/latest/Data/Abouteventsegmentation  
[def4]: https://docs.splunk.com/Documentation/Splunk/latest/Search/Eventsegmentationandsearching  
[def3]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Commandsbytype