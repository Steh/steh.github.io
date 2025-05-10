---
title: "Splunk: Mastering Field Extraction, a Quick Guide"
categories: 
- informationsecurity
- Splunk
tags:
- blue team
classes: 
- wide
excerpt: "Learn how to configure and test field extractions in Splunk using regex in transforms.conf and props.conf."
toc: true
---

Field extraction in Splunk is essential for deriving meaningful insights from your data. By configuring `transforms.conf` and `props.conf`, you can tailor Splunk to parse your data accurately. This guide will help you set up and test field extractions efficiently.

## Understanding `props.conf` and `transforms.conf`

In Splunk, `props.conf` and `transforms.conf` define how data is parsed and processed:

- **props.conf**: Specifies source type definitions, time extraction, and field extractions, often referencing `transforms.conf`.
- **transforms.conf**: Defines complex field extractions, lookups, anonymization, and routing.

## Types of Extractions

Field extractions in `props.conf` can be configured using three main types:

- **`TRANSFORMS`**: Used for index-time extractions by referencing `transforms.conf`.
- **`REPORT`**: Used for search-time extractions by referencing `transforms.conf`.
- **`EXTRACT`**: Used for search-time extractions with regex directly in `props.conf`.

### Index-Time vs. Search-Time Extractions

- **Index-Time Extractions (`TRANSFORMS`)**:  
  - Occur during data ingestion.  
  - Use sparingly due to performance impact.  
  - Example:
    ```bash
    [source::example_logs]
    TRANSFORMS-add_fields = add_field_transform
    ```

- **Search-Time Extractions (`REPORT` and `EXTRACT`)**:  
  - Occur during search execution.  
  - Preferred for most cases to avoid index-time load.  
  - Example for `REPORT`:
    ```bash
    [source::example_logs]
    REPORT-add_fields = add_field_transform
    ```
  - Example for `EXTRACT`:
    ```ini
    [source::example_logs]
    EXTRACT-field = (?<field_name>\w+)
    ```

## Step-by-Step Guide to Field Extraction

### 1. Identify Data Patterns

Identify patterns in your data for extraction. For example, in logs like:

```bash
2023-07-08 12:34:56,789 INFO User=john.doe Action=login Status=success
```

You might extract `User`, `Action`, and `Status`.

### 2. Develop and Test the Extraction in SPL

Use the `rex` command to test your extraction:

```bash
index=mydata
| rex field=_raw "User=(?P<user>\S+) Action=(?P<action>\S+) Status=(?P<status>\S+)"
```

### 3. Define Extractions in `transforms.conf`

Define the extraction logic in `transforms.conf`:

```bash
[extract_user_action_status]
REGEX = User=(?P<user>\S+) Action=(?P<action>\S+) Status=(?P<status>\S+)
```

For extractions on specific fields:

```bash
[extract_user_action_status]
REGEX = User=(?P<user>\S+) Action=(?P<action>\S+) Status=(?P<status>\S+)
SOURCE_KEY = field
```

### 4. Configure `props.conf`

Reference the extraction in `props.conf`:

```bash
[your_log_sourcetype]
TRANSFORMS-extract_user_action_status = extract_user_action_status
```

### 5. Reload Configurations

To apply changes without restarting Splunk, reload the configurations:

```bash
| extract reload=t
```

## References

- [Splunk Documentation: props.conf - Field Extraction Configuration][def]
- [Splunk Documentation: transforms.conf][def1]
- [Splunk Documentation: Configure Advanced Extractions with Field Transforms][def2]

[def]: https://docs.splunk.com/Documentation/Splunk/latest/Admin/Propsconf#Field_extraction_configuration  
[def1]: https://docs.splunk.com/Documentation/Splunk/9.2.2/Admin/Transformsconf  
[def2]: https://docs.splunk.com/Documentation/Splunk/latest/Knowledge/Configureadvancedextractionswithfieldtransforms