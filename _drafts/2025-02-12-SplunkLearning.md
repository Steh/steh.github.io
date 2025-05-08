---
title: "Splunk basics"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "This guide on Splunk basics covers essential commands and functionalities, including field operations, the erex command for regex extraction, and time management techniques, to enhance data analysis and search efficiency" 
toc: true
--- 

## Using Fields

´´´
# Field Operators

=, != for Numericals or string values

>, >=, <, <= only with numerical values
´´´

# erex command
The erex command is used to extract fields from event data using examples. 
The generated regex can be viewed under Jobs.

´´´ 
index=games
| erex Character fromfield=_raw examples"pixie, Kooby"
´´´

* [erex search reference][def]

# commands

## addtotal
The addtotals command computes the arithmetic sum of all numeric fields for each search result. The results appear in the Statistics tab. 

´´´bash
# Calculate the sums for the fields that begin with amount or that contain the text size in the field name. Save the sums in the field called TotalAmount. 
source="addtotalsData.csv" 
| chart sum(sales) by products quarter
| addtotals fieldname=TotalAmount amount* *size*

## fieldformat
With the fieldformat command you can use an <eval-expression> to change the format of a field value when the results render. This command changes the appearance of the results without changing the underlying value of the field. 

´´´
... | fieldformat start_time = strftime(start_time, "%H:%M:%S")
´´´

* [fieldformat search reference][def4]

## top
Finds the most common values for the fields in the field list. Calculates a count and a percentage of the frequency the values occur in the events. If the <by-clause> is included, the results are grouped by the field you specify in the <by-clause>. 

´´´
# This search returns the 20 most common values of the "referer" field. The results show the number of events (count) that have that a count of referer, and the percent that each referer is of the total number of events. 
sourcetype=access_* | top limit=20 referer

# This search returns the top "action" values for each "referer_domain". 
sourcetype=access_* 
| top action by referer_domain
´´´

## timechart
like stats but with time buckets

´´´
index="_internal" OR index="_audit" 
| timechart span=1m sum(linecount) by index
´´´

## trendline
Computes the moving averages of fields: simple moving average (sma), exponential moving average (ema), and weighted moving average (wma) The output is written to a new field, which you can specify. 

## fields

´´´bash
# removes these fields
| fields - source host

# removes _raw and only includes host
| fields -_raw host
´´´

# time

* time ist most efficient filter
* all events are sorted by time
* every event has: _time (timestamp) and metadata fields (host, source, sourcetype and index)

```bash
[+|-]<time_integer><time_unit>@<time_unit>

# rounds down last 30m and rounding down to 1h
-30m@h

# rounds down to last hour
earliest= -h@h

# getting everything from the last month
earliest= -mon@mon latest=@mon

# search to start at 3 hours past midnight 
earliest=@d+3h

# all time
earliest=0

```
## Time specifiers
|Time range | Valid values | 
| ------ | ------ |
|seconds | s, sec, secs, second, seconds |
|minutes | m, min, minute, minutes |
|hours | h, hr, hrs, hour, hours |
|days | d, day, days |
|weeks | w, week, weeks |
|months | mon, month, months |
|quarters | q, qtr, qtrs, quarter, quarters | 
|years | y, yr, yrs, year, years |

https://docs.splunk.com/Documentation/Splunk/9.4.0/Search/Specifytimemodifiersinyoursearch

## formatting

´´´bash
# time search was started
eval field1 = now()

# time event was processed by eval
eval field1 = time()

# from now one day back to the beginning of the hour
field1 = relative_time(now(), "-1d@h")

# format the timefield yesterday
yesterdayString = strftime(yesterday, "%F $H:%M")
´´´

## source

* [erex search reference][def]
* [addtotal search reference][def3]
* [fieldformat search reference][def4]
* [timechart search reference][def5]
* [About Splunk regular expressions][def1]
* [Youtube: Introduction to RegEx][def2]
* [Statistical and charting functions][def6]
* [The sequence of search-time operations][def7]

[def]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Erex
[def1]: https://docs.splunk.com/Documentation/Splunk/latest/Knowledge/Aboutsplunkregularexpressions
[def2]: https://www.youtube.com/watch?v=QvxLJ9f6AK0
[def3]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Addtotals
[def4]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Fieldformat
[def5]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Timechart
[def6]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/CommonStatsFunctions
[def7]: https://docs.splunk.com/Documentation/Splunk/latest/Knowledge/Searchtimeoperationssequence