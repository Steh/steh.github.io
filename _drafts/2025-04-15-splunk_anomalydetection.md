---
title: "Splunk anomalydetection Command"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "A guide to using the Splunk 'anomalydetection' command for identifying anomalies in data."
toc: true
---

```bash
anomalydetection [<method-option>] [<action-option>] [<pthresh-option>] [<cutoff-option>] [<field-list>]
```

## Method Options

- **histogram**: Detect anomalies based on histogram analysis.
- **zscore**: Use z-score to identify outliers.
- **iqr**: Apply interquartile range for anomaly detection.

## Action Options

- **annotate**: Add anomaly information to the results.
- **filter**: Filter out non-anomalous data.
- **summary**: Generate a summary of anomalies.

## Source

- [Splunk Documentation: anomalydetection Command][def]
- [About the Splunk Machine Learning Toolkit][def1]

[def]: https://docs.splunk.com/Documentation/Splunk/9.3.3/SearchReference/Anomalydetection
[def1]: https://docs.splunk.com/Documentation/MLApp/latest/User/AboutMLTK
