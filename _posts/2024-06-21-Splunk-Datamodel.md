---
title: "A Technical Guide to Splunk Data Models"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "Learn how to create, fill, maintain, validate, and request data from Splunk Data Models in this comprehensive guide."
toc: true
--- 

## A Technical Guide to Splunk Data Models

Splunk Data Models are essential for organizing and accelerating searches, providing structured data for Splunk's Pivot interface and creating efficient dashboards. This guide will walk you through the processes of creating, filling, maintaining, validating, and requesting data from Splunk Data Models.

## Creating a Splunk Data Model

1. **Log in to Splunk**: Access your Splunk instance through your web browser.
2. **Navigate to Data Models**: Go to `Settings > Data models`.
3. **Create New Data Model**:
   - Click on `New Data Model`.
   - Enter a `Title` and an optional `ID` and `Description`.
   - Choose the `Permissions` (private or shared in an app).
   - Click `Create`.

4. **Add Data Model Objects**:
   - Click on `Add Object`.
   - Choose the `Root Event Object` or `Root Search Object`.
   - Provide an `Object Name`, `Display Name`, and `Description`.
   - Define the `Constraint` (base search).
       - ```(`cim_Vulnerabilities_indexes`) tag=vulnerability tag=report```
   - Add `Fields` (auto-extracted or manually defined).

5. **Save the Data Model**: Click `Save` to store the Data Model.

6. **Use Accelerations** (recommendet after development)
   - Enable acceleration for faster search performance.
   - Navigate to the Data Model, click `Edit > Edit Acceleration`.
   - Check `Accelerate` and set the `Summary Range`.
   - Click `Save`.

### Dataset

### Event
**Explanation**: Event datasets focus on raw data, applying constraints to select specific events for analysis.

- **Fields**: `username`, `timestamp`, `ip_address`
- **Constraints**: `status="success"`
- **Example**: You have a log source that records user login activities. An event dataset might filter these logs to include only successful login events.

### Search
**Explanation**: Search datasets use the results of saved searches, allowing for complex queries and aggregations.

- **Search Query**: `index=web_logs | stats avg(response_time) as avg_response_time by endpoint`
- **Fields**: `endpoint`, `avg_response_time`
- **Example**: You want to track the average response time of a web application. You could create a search dataset based on a saved search that calculates this metric.

### Transaction
**Explanation**: Transaction datasets group related events, useful for analyzing multi-step processes or transactions.

- **Transaction Definition**: Group events by `session_id` with a start event of `action="add_to_cart"` and an end event of `action="checkout"`.
- **Fields**: `session_id`, `user_id`, `total_time`, `items_purchased`
- **Example**: You need to analyze a user's journey through an e-commerce site, from adding items to the cart to checkout.

## Validating a Splunk Data Model

1. **Use the Datamodel "CIM Validation (S.o.S.)"**:

Is only availiable for internal Datamodels

    - Select Settings > Data models
    - Locate the CIM Validation (S.o.S.) data model and in the Actions column, click Pivot.
    - Click one of the following to create the Pivot:
      - Top level dataset
      - Missing extractions
      - Untagged events

2. **Use the datamodelsimple command**

The `datamodelsimple` command in Splunk is designed to retrieve and explore the structure of data models, including listing available models, objects within a model, and attributes of a specific object.

```bash
# List All Data Models
| datamodelsimple type=models

# List all objects in a specific datamodel
| datamodelsimple type=objects datamodel=Authentication

# List Attributes (Fields) for a Specific Object in a Data Model
| datamodelsimple type=attributes datamodel=Authentication nodename=Authentication.Failed_Authentication
```

3. 

- open the app "CIM Vladiator"
  - Search Type: Datamodel
  - Target datamodel: `<your Model>`
  - Search:
    - `| datamodel Vulnerabilites search`
    - `index=vulnerabilities`

4. Search for errors in Log
`index=_internal sourcetype=splunkd "DataModelAccelerator" OR "DataModel"`

## Requesting Data from a Splunk Data Model

```bash
# | from
## rely on accelerated Data
| from datamodel:<datamodel>

# | datamodel
## rely on index data
| datamodel <DataModelName> <ObjectName> search

# tstats
| tstats count FROM datamodel=Network WHERE ip=10.9.8.7 by <Fields>
| tstats count 
   FROM datamodel=Network.Network_Traffic 
   WHERE src=10.9.8.7
   BY Network_Traffic.src, Network_Traffic.dest, Network_Traffic.action
```

## source

[Splunk How to use the CIM data model][def]
[Splunk Use the CIM to validate your data][def1]
[Splunk Common Information Model Add-on Manual][def2]
[Splunk Use the CIM to normalize CPU performance metrics][def3]
[Splunk Base - SA-cim_vladiator][def4]

[def]: https://docs.splunk.com/Documentation/CIM/5.3.2/User/Howtousethesereferencetables
[def1]: https://docs.splunk.com/Documentation/CIM/5.3.2/User/UsetheCIMtovalidateyourdata
[def2]: https://docs.splunk.com/Documentation/CIM/latest/User/UsetheCIMtonormalizedataatsearchtime
[def3]: https://docs.splunk.com/Documentation/CIM/5.3.2/User/UsetheCIMtonormalizeCPUperformancemetrics
[def4]: https://splunkbase.splunk.com/app/2968
