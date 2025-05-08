---
title: "cribl"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

# replay

add metadata field:
* __replay = true


# Data Management

## 3 V´s of data

* Volume
    * amount of data being generated and collected
* Variety
 * Structured data
 * semi-structuted data
 * unstructured data 
* value
    * processing framework that transforms raw data into events

## Terms

* Telemetry Data
    * Data about a systems performance for monitoring and analysis
* 011y Data
    * Data that provides insights into system behavior and interactions
* Security Data
    * data that is used to protect systems and data from threats

## data optimization

* collection
    * data is collected from the right sources in a timely, accurate manner
* reduction
    * filtering, aggregating and summarizing data
* shaping
    * transformation and structuring of data to make it more accessible and usable
* enrichment
    * enhance with additional context, metadata or sources to improve its value

## MELT

* Metrics
    * numerical representations of data measured over intervals of time
    * Examples: Responce Time, CPU Usage, ...
    * track service performance
    * but at first define what you want to meassure
* Events
    * A set of key values pairs describing something that occured at a point in time
* Logs
    * system-generated record of data that describes what is going on during the event
* Traces
    * marks the path taken by a transcation within an application to be completed

## common data tools

* data lake
    * centralized ropistory for storing diverse data at alow cost
* agents
    * software deployed in an infrastructure that emits information about what is going on
* object storage
    * cheap storage for long-term retention
* time series databases:
    * optimized for fast time-series analysis
* indexed log analystics:
    * engines for investigations and searches
* SIEM/UEBA
    * great for incident correlation, response and user analytics

# Stream Fundamentals 

* sources:
    * push-based: Sources that **send** data to Stream
    * pull-based: Sources that Stream **fetches** data from
    * collectors: Ability to **fetch** data from local or remote sources **on a schedule**
* destinations
    * **Streaming** accept event in real time/mini-batch
    * **Non-Streaming** accept eventy in (larger) groups or batches

## routing traffic

* Routes
    * direct data to pipelines
    * evaluate incoming events against filters
    * each route can be associated with only one pipeline and one output
    * evaluated in order
    * routes default with "Final flag" set to Yes
* Quick Connect
    * design for testing and simple usecases

# parsing events

* Field that starts with __ are internal fields
    * like __InputId
* these will not be passed down to Destinations
* if ab event cannot be JSON-parsed, all of its content will be assigned to a field called **_raw**

# JavaScript in Cribl

* is used in filters and Value Expressions in Stream and Edge
* Filter:
    * ```source.endsWith('.log') || type = 'vpcflow' ```
* Value Expression:
    * ```location = 'New York'````
    * ```hour = Math.floor(_time/3600)```

# Data Tools

* Sample Data
    * Processing -> Pipelines
* Import Data
    * Uplaod Samples
* Edge Data
    * Download Files from Edge
* Capute Data
    * Capture Data from live inputs
    * Also Possible to use Datagens as Test datasets

* [Text][def]

[def]: https://steh.github.io