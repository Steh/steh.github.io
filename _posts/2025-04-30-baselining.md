---
title: "Splunk: Baselining"
categories: 
  - informationsecurity
tags:
  - splunk
classes: 
  - wide
excerpt: "A guide to statistical measures in Splunk for baselining and anomaly detection."
toc: true
date: 2025-04-30
---

## Introduction

When working with Splunk, understanding statistical measures is crucial for baselining and anomaly detection. Below are some common statistical functions and their usage:

### average/mean

- **Command**: `stats avg(field)`
- **Purpose**: Calculate the average value of a field to identify the central tendency of your data.
- **Importance**: Provides a baseline for normal behavior, making it easier to spot deviations.
- **Example**: For values `10, 20, 30, 60, 80`, the mean is `(10 + 20 + 30 + 60 + 80) / 5 = 40`.

### Median

- **Command**: `stats median(field)`
- **Purpose**: Find the middle value of a field, especially useful for datasets with outliers.
- **Importance**: Less affected by extreme values, offering a robust baseline.
- **Example**: For values `10, 20, 30, 60, 80`, the median is `30`.

### Mode

- **Command**: `stats mode(field)`
- **Purpose**: Determine the most frequently occurring value in a field.
- **Importance**: Highlights common patterns or repeated values in your dataset.
- **Example**: For values `10, 20, 20, 60, 80`, the mode is `20`.

### Standard Deviation

- **Command**: `stats stdev(field)`
- **Purpose**: Measure the amount of variation or dispersion in a dataset.
- **Importance**: Quantifies data spread, helping to define thresholds for normal versus abnormal behavior.
- **Example**: For values `10, 20, 30, 60, 80`, the standard deviation is approximately `31.62`.

### Quartiles and Percentiles

- **Command**: `stats perc75(field) perc25(field)`
- **Purpose**: Calculate the 75th and 25th percentiles to segment and identify data spread.
- **Importance**: Provides a detailed view of data distribution for precise baselining and anomaly detection.
- **Example**: For values `10, 20, 30, 60, 80`, the 25th percentile is `20` and the 75th percentile is `60`.

## Statistic Baselining

### Z-Score:
A z-score tells you how many standard deviations a value is from the mean.

### IQR (Interquartile Range):

IQR = Q3 - Q1 (difference between 75th and 25th percentiles).
Advantage: Works even if data isn’t normally distribute

### When to use which?

* Use z-score for symmetric, bell-shaped data.
* Use IQR for skewed or non-normal data

## Splunk Commands

### Stats

- **Command**: `stats`
- **Purpose**: Perform aggregations like sum, average, count, etc., on fields in your dataset.
- **Importance**: Essential for summarizing data and deriving insights.
- **Example**: `| stats count by status` counts the occurrences of each status value.

### Streamstats

- **Command**: `streamstats`
- **Purpose**: Calculate running totals, averages, or other statistics over a stream of events.
- **Importance**: Useful for tracking trends or cumulative metrics in real-time.
- **Example**: `| streamstats sum(bytes) as cumulative_bytes` calculates a running total of bytes.

### Eventstats

- **Command**: `eventstats`
- **Purpose**: Add aggregated statistics to each event without reducing the number of events.
- **Importance**: Allows for comparisons between individual events and overall statistics.
- **Example**: `| eventstats avg(duration) as avg_duration` adds the average duration to each event.

### Bin

- **Command**: `bin`
- **Purpose**: Group numeric or time values into buckets for easier analysis.
- **Importance**: Simplifies data by categorizing it into ranges or intervals.
- **Example**: `| bin span=5m _time` groups events into 5-minute intervals.

### Timechart

- **Command**: `timechart`
- **Purpose**: Create time-based visualizations of aggregated data.
- **Importance**: Ideal for monitoring trends and patterns over time.
- **Example**: `| timechart span=1h count by status` shows hourly counts of each status value.

## Baselining with Standard Deviation

Baselining with standard deviation is a statistical method used to identify normal behavior and detect anomalies in data. Here's how you can use it in Splunk:

* avg vs. median for Baselining
   * use Median for Skewed Data or Outliers
      * **Median** is robust against extreme values and better represents the “typical” case when data is uneven or contains anomalies.
      * **Example:** Login counts, network traffic with occasional spikes.

   * use Mean for Symmetric, Consistent Data
      * **Mean (average)** works well when data is evenly distributed without significant outliers.
      *  **Example**: Sensor readings, consistent process counts.

### Steps to Baseline with Standard Deviation

1. **Calculate the Mean**:
   Use the `stats avg(field)` command to calculate the average value of the field you want to baseline.

   ```bash
   | stats avg(response_time) as mean
   ```

2. **Calculate the Standard Deviation**:
   Use the `stats stdev(field)` command to calculate the standard deviation of the field.

   ```bash
   | stats stdev(response_time) as stddev
   ```

3. **Define Thresholds**:
   Use the mean and standard deviation to define thresholds for normal behavior. For example:
   - Lower Threshold: `mean - (2 * stddev)`
   - Upper Threshold: `mean + (2 * stddev)`

4. **Filter Anomalies**:
   Use a `where` clause to filter events that fall outside the thresholds.

   ```bash
   | eval lower_threshold = mean - (2 * stddev)
   | eval upper_threshold = mean + (2 * stddev)
   | where response_time < lower_threshold OR response_time > upper_threshold
   ```

### Example Use Case: Standard Deviation

Suppose you are monitoring the response time of a web application. You can use the following search to identify anomalies:

```bash
index=web_logs sourcetype=access_combined
| stats avg(response_time) as mean, stdev(response_time) as stddev
| eval lower_threshold = mean - (2 * stddev)
| eval upper_threshold = mean + (2 * stddev)
| where response_time < lower_threshold OR response_time > upper_threshold
```

This search calculates the mean and standard deviation of response times, defines thresholds, and filters out events that are outside the normal range.

## Baselining with Z-Score

Baselining with Z-Score is a statistical method used to identify anomalies by measuring how far a data point is from the mean in terms of standard deviations. 

> **The Empirical Rule [1][def1], [2][def5]**
>  - 68% of data falls within ±1 standard deviation
>  - 95% falls within ±2 standard deviations
>  - 99.7% falls within ±3 standard deviations

### Steps to Baseline with Z-Score

1. **Calculate the Mean and Standard Deviation**:
   Use the `stats` command to calculate the average and standard deviation of the field you want to baseline.

   ```bash
   | stats avg(count) as mean, stdev(count) as stddev
   ```

2. **Calculate the Z-Score**:
   Use the `eval` command to calculate the Z-Score for each event. The formula for Z-Score is:
   ```bash
   Z-Score = (count - mean) / standard deviation
   ```

   In Splunk:
   ```bash
   | eval z_score = (count - mean) / stddev
   ```

3. **Define Thresholds**:
   Decide on a threshold for the Z-Score to identify anomalies. Common thresholds are:
   - Z-Score > 3 or Z-Score < -3 (indicating the data point is more than 3 standard deviations away from the mean).

4. **Filter Anomalies**:
   Use a `where` clause to filter events with Z-Scores outside the threshold.

   ```bash
   | where abs(z_score) > 3
   ```

### Example Use Case: Z-Score

Suppose you are monitoring the response time of a web application. You can use the following search to identify anomalies:

```bash
index=web_logs sourcetype=access_combined action=failed
| bin _time span=1h
| stats count as failed_logins by _time
| stats avg(failed_logins) as mean, stdev(failed_logins) as stdev
| eval z_score = (failed_logins - mean) / stdev
| where abs(z_score) > 3
```

This search calculates the mean and standard deviation of response times, computes the Z-Score for each event, and filters out events with Z-Scores greater than 3 or less than -3.

## Optional

If you only want to see the anomalies from the last 24h you could at the following befor the last where

```bash
....
# filter only for events from the last day
| where _time >= relative_time(now(), "-1d@d") AND _time < relative_time(now(), "@d")
...Y
```

## Examples

```bash
index=_internal source=*license_usage.log* type="Usage" 
| stats sum(b) as bytes by idx,_time
| bin _time span=1d
| stats sum(bytes) as bytes by _time,idx
| eval GB=round(bytes/1024/1024/1024, 10)
| eventstats avg(GB) as mean stdev(GB) as stdev by idx
| eval lower_threshold = mean - (2 * stdev)
| eval upper_threshold = mean + (2 * stdev)
| where GB > upper_threshold
| fields - lower_threshold - stdev - bytes
| sort - _time
```

### show only the complete index data for each index that is over the threashold
```bash
index=_internal source=*license_usage.log* type="Usage" 
# Step 1: Bin the _time field into daily intervals for time-based anal
| bin _time span=1d

# Step 2: Aggregate raw license usage data by index and time
| stats sum(b) as bytes by idx,_time

# Step 3: Convert bytes to gigabytes for easier readability
| eval GB=bytes/1024/1024/1024

# Step 4: For each index, calculate the maximum daily GB usage, mean, and standard deviation across all days
| eventstats max(GB) as max_GB avg(GB) as mean stdev(GB) as stdev by idx

# Step 5: Calculate lower and upper thresholds (mean ± 2*stdev) for anomaly detection per index
| eval lower_threshold = mean - (2 * stdev)
| eval upper_threshold = mean + (2 * stdev)

# Step 6: Keep only indexes where the maximum daily usage exceeds the upper threshold
| where max_GB > upper_threshold

# Step 7: Remove intermediate fields for cleaner output
| fields - lower_threshold - stdev - bytes - max_GB
```

## Optimize your results

* think about how many datapoints you need for a reliable baseline
   * n >= 30 should be the minimum

### how many datapoints do you need to create a reliable baseline (experimental)

* [see][def10]

```bash
## filter telidP with fewer than 20 datapoint
| eventstats count as count_datapoints by your_values
| where count_datapoints > 20
```

## Sources

For further reading and practical examples, refer to the following resources:

1. [Splunk: Finding and Removing Outliers][def]
2. [Z-Scoring Your Way to Better Threat Detection][def1]
3. [Stop Chasing Ghosts: How Five-Number Summaries Reveal Real Anomalies][def2]
4. [Unravel the Mysteries of Variance and Standard Deviation][def3]
5. [Using Stats in Splunk Part 1: Basic Anomaly Detection][def4]
6. [Statistics How To: Empirical Rule ( 68-95-99.7)][def5]
7. [Using stats, eventstats & streamstats for Threat Hunting…Stat!][def7]
8. [][def8]
9. [Intel: Anomaly Detection ][def9]
10. [How to Determine the Minimum Size Needed for a Statistical Sample][def10]

[def]: https://docs.splunk.com/Documentation/Splunk/latest/Search/Findingandremovingoutliers
[def1]: https://dispatch.thorcollective.com/p/z-scoring-your-way-to-better-threat-detection
[def2]: https://dispatch.thorcollective.com/p/stop-chasing-ghosts-how-five-number
[def3]: https://medium.com/data-analytics-magazine/unravel-the-mysteries-of-variance-and-standard-deviation-your-ultimate-guide-fc29f9471270
[def4]: https://hurricanelabs.com/splunk-tutorials/using-stats-in-splunk-part-1-basic-anomaly-detection/
[def5]: https://www.statisticshowto.com/probability-and-statistics/statistics-definitions/empirical-rule/
[def6]: https://medium.com/detect-fyi/powershell-threat-hunting-identifying-obfuscation-using-standard-deviation-9b2d9f53697f
[def7]: https://www.splunk.com/en_us/blog/security/stats-eventstats-streamstats-threat-hunting.html
[def8]: https://dataheroes.ai/blog/anomaly-detection-techniques-you-need-to-know/
[def9]: https://www.intel.com/content/www/us/en/developer/topic-technology/artificial-intelligence/training/course-anomaly-detection.html
[def10]: https://www.dummies.com/article/academics-the-arts/math/statistics/how-to-determine-the-minimum-size-needed-for-a-statistical-sample-169793/