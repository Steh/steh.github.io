---
title: "Splunk: baselining"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

## Introduction

* mean
    * `stats avg(field)`
* median
    * `stats median(field)`
* mode
    * `stats mode(field)`
* Standard deviation
    * `stats stdev(field)`
* Quartiles and percentiles
    * `stats perc75(field) perc25(field)`


## source

* [splunk: Finding and removing outliers][def]
* [Z-Scoring Your Way to Better Threat Detection][def1]
* [Stop Chasing Ghosts: How Five-Number Summaries Reveal Real Anomalies][def2]

[def]: https://docs.splunk.com/Documentation/Splunk/latest/Search/Findingandremovingoutliers
[def1]: https://dispatch.thorcollective.com/p/z-scoring-your-way-to-better-threat-detection
[def2]: https://dispatch.thorcollective.com/p/stop-chasing-ghosts-how-five-number
