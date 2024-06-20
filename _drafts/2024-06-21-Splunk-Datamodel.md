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

# A Technical Guide to Splunk Data Models

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

## Maintaining a Splunk Data Model

1. **Regular Updates**:
   - Periodically review and update the Data Model to align with any changes in your data sources or organizational requirements.

2. **Manage Permissions**:
   - Ensure appropriate access controls by updating permissions.
   - Go to `Settings > Data models`, select the Data Model, and click `Edit Permissions`.

3. **Optimize Performance**:
   - Monitor the performance of accelerated Data Models.
   - Adjust the summary range or constraints as necessary.

## Validating a Splunk Data Model

1. **Use the Data Model Editor**:
   - Access the Data Model via `Settings > Data models`.
   - Select the Data Model and click `Edit`.
   - Verify each object, field, and constraint to ensure they are correctly configured.

## Requesting Data from a Splunk Data Model

```
# | datamodel
| datamodel <DataModelName> <ObjectName> search

# tstats
| tstats count FROM datamodel=Network WHERE ip=10.9.8.7 by <Fields>
```

## source

[Splunk How to use the CIM data model][def]

[def]: https://docs.splunk.com/Documentation/CIM/5.3.2/User/Howtousethesereferencetables