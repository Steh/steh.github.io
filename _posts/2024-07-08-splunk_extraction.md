---
title: "Mastering Field Extraction in Splunk: Quick Guide"
categories: 
- informationsecurity
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

## Understanding `extractions`

In Splunk, you configure field extractions in `props.conf` using three main types: `TRANSFORMS`, `REPORT`, and `EXTRACT`. Here's a brief overview of each:

## Index Time vs. Search Time Extractions

- **Index-Time Extractions (`TRANSFORMS`)**:
  - Occur when data is ingested.
  - Use sparingly due to performance impact.
  - Example:

    ```bash
    [source::example_logs]
    TRANSFORMS-add_fields = add_field_transform
    ```

- **Search-Time Extractions (`REPORT` and `EXTRACT`)**:
  - Occur when you run a search.
  - Preferred for most cases to avoid index-time load.
  - `REPORT` references a field transform in `transforms.conf`.
  - `EXTRACT` includes the regex directly in `props.conf`.
    - for straightforward extractions that don’t need reuse or complex handling
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

## Step-by-Step Guide to Field Extraction with transforms.conf

### 1. Identifying Data Patterns

Identify the data patterns for extraction. For example, in logs like:

```bash
2023-07-08 12:34:56,789 INFO User=john.doe Action=login Status=success
```

You might extract `User`, `Action`, and `Status`.

### 2. Create Extraction in SPL

- develope and test the extraction

```bash
# extraction on the _raw data
index=mydata
| rex field=_raw User=(?P<user>\S+) Action=(?P<action>\S+) Status=(?P<status>\S+)
```

### 3. Defining Extractions in `transforms.conf`

- Define the extraction in the `transforms.conf`
- the following are equivalent for search-time field extractions:
  - Using FORMAT:
  
  ```bash
  REGEX  = ([a-z]+)=([a-z]+)
  FORMAT = field1::$1 <field-name>::<field-value>
  ```

  - Without using FORMAT
  
  ```bash
  REGEX  = (?<_KEY_1>[a-z]+)=(?<_VAL_1>[a-z]+)
  ````

```bash
# extraction on the _raw data
[extract_user_action_status]
REGEX = User=(?P<user>\S+) Action=(?P<action>\S+) Status=(?P<status>\S+)

# extraction on specific field, doesn´t work if field contains an white space
[extract_user_action_status]
REGEX = User=(?P<user>\S+) Action=(?P<action>\S+) Status=(?P<status>\S+)
SOURCE_KEY = field
```

Test the extraction on your data. The extract command reloads the config from props and transforms configuration file.

```bash
index=mydata
| extract extract_user_action_status
```

### 4. Configuring `props.conf`

Define the source type and reference the transforms:

```bash
# Option 1 reference to the stanza in transforms.conf
[your_log_sourcetype]
TRANSFORMS-extract_user_action_status = extract_user_action_status
```

### 4. Reload config

- you need to restart the Server to update the configuration
- until then you can reload the extractions from props.conf and transforms.conf with the following:

```bash
| extract reload=t

```

## references

- [splunk.com props.conf: Field extraction configuration][def]
- [splunk.com transforms.conf][def1]
- [splunk.com Configure advanced extractions with field transforms][def2]

[def]: https://docs.splunk.com/Documentation/Splunk/latest/Admin/Propsconf#Field_extraction_configuration
[def1]: https://docs.splunk.com/Documentation/Splunk/9.2.2/Admin/Transformsconf
[def2]: https://docs.splunk.com/Documentation/Splunk/latest/Knowledge/Configureadvancedextractionswithfieldtransforms