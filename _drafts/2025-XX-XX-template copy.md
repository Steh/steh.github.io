---
title: "Splunk: Use Metric Data"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

# get all fields in an index
| mcatalog values(metric_name) WHERE index=your_index

## source

* [Text][def]

[def]: https://steh.github.io
