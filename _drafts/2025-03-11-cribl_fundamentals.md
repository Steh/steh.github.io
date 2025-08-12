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

1. Discovery: This stage involves identifying and locating data sources. Cribl Edge plays a crucial role here, acting as an intelligent agent that automatically discovers data at its source.
2. Processing: Once discovered, data needs processing. Cribl Stream excels at this stage, transforming and securing data in real-time before routing it to its final destination
3. Storing: Processed data needs storage. Cribl Lake offers a fast and easy solution for storing data in an open, non-proprietary format, avoiding vendor lock-in and simplifying storage management.
4. Exploring: Finally, stored data needs exploration and analysis. Cribl Search empowers users to search, explore, and analyze data directly in its location, eliminating the need to move data to separate systems.

Cribl Stream processes and optimizes machine data for efficient analysis.
•

Cribl Edge simplifies data collection and forwarding from various sources.
•

Cribl Lake offers is a fast and easy solution for storing data in an open, non-proprietary format.
•

Cribl Search facilitates data exploration and visualization without data movement.
•

Cribl.Cloud provides a scalable and readily deployable platform for the Cribl Suite.

* Crible Access
    * Cribl Members is a centralized solution for user access management across Cribl products.
    * It offers granular access control at various levels (organization, product, worker group, fleet, resource).
    * Different roles (User, Read Only, Editor, Admin) define user capabilities within each access level.
    * Cribl Members empowers secure and controlled access to Cribl data and configurations.

* Technologies
    * Git enables version control and deployment of Cribl configurations.
    * JavaScript is used for data manipulation within Cribl Stream pipelines.
    * Regex empowers you to perform pattern matching and data manipulation tasks.
    * KQL facilitates user-friendly data searches within Cribl Search.
    * Cribl Knowledge Objects offer reusable functionalities for data processing tasks. 

# Stream Architecture: Overview

* Cribl Leader Nodes act as the central hub, managing configurations for Worker Nodes and Edge deployments.
* Worker Nodes, grouped logically based on shared configurations, perform the actual data processing tasks.
* You can have a flexible number of Worker Nodes and Groups to match your specific data processing requirements.

Worker Groups: Organizing Data Processing

Stream Fundamentals: Sources, Destinations & Collectors

* Stream Fundamentals: Routes & QuickConnect
* Understand the difference between QuickConnect (simple data flow) and Routes (flexible data processing).
* Grasp how routes use filters to match events and direct them to pipelines.
* Recognize the importance of route order and the "final flag" for efficient processing.
* Be familiar with cloning events and how it's achieved using routes.
* Know when to choose QuickConnect for simplicity or Routes for complex routing scenarios.

1. Pipelines define the order of data processing through a series of Functions.
2. Functions are Javascript programs that perform specific actions on events.
3. Packs offer pre-built configurations for faster deployment and streamlined data processing.

Remember...

Cribl Edge offers a centralized approach to managing and collecting data from a wide range of sources. Leverage Cribl Edge's features to simplify agent management, optimize data processing, and gain deeper insights into your IT environment. Some key takeaways:

    •

Saves resources by eliminating the need for multiple agents, simplifying configuration, and minimizing data movement.
•

Manages large deployments efficiently with centralized control.
•

Enables real-time processing at the edge for quicker insights.
•

Search functionality on Edge nodes (Cribl.Cloud) facilitates quicker issue identification and resolution

Cribl Edge allows you to analyze data directly at the edge before deciding to collect and process it further.

    •

Cribl Edge offers various sources, including unique options like Cribl Internal Source (captures Edge's logs and metrics), File Monitor Source (collects log text files), and Exec Source (executes commands and collects output).
•

Cribl Edge seamlessly integrates with Kubernetes environments, making it easy to gather data from containers.
•

Pay close attention to the different source types and their functionalities.
•

Understand the advantages and disadvantages of Cribl HTTP and Cribl TCP destinations.
•

Familiarize yourself with Cribl's unique sources like Cribl Internal Source, File Monitor Source, and Exec Source.

Grasp the differences between Single and Distributed Modes for Cribl Edge deployment.
•

Leverage Fleets and Subfleets for efficient Edge Node management. Fleets and Subfleets group Edge Nodes logically based on shared characteristics or data types. Fleets relate to Edge Nodes similarly to how Worker Groups relate to Worker Nodes.
•

Cribl Leader Node manages Worker Nodes and Edge Nodes, sending configuration information to both. Be familiar with communication ports used by the Leader Node for Worker and Edge Node interactions.
•

Cribl Edge Nodes collect data at the network edge (e.g., servers).
•

Consider Worker Groups for complex data processing exceeding Cribl Edge's single CPU limitation.

Cribl Edge is ideal for data collection at the edge, while Cribl Stream is better suited for complex data processing tasks due to its superior processing power.

    •

The Cribl Edge UI provides a centralized console to manage Fleets (groups of Edge Nodes) and individual Edge Nodes.
•

Fleets help manage Edge Nodes based on shared characteristics.
•

Explore details of individual Edge Nodes, including processes, files, and system state.
•

Cribl Edge Collect allows data source to destination connections similar to Cribl Stream's Quick Connect.

Search Query Components 

You'll start by shaping the search - Formulate the right questions to filter out irrelevant data and pinpoint valuable information. Then, Define what's being searched and filter the results:

    •

Dataset Providers: Specify the data source for the search.
•

Datasets: Define the specific data set within the data source to be searched.
•

Operators: Filter the data based on specific criteria (e.g., AND, OR, NOT).
•

Functions: Perform calculations or manipulations on the data within the search query.
•

Time Range: Specify the timeframe for the search.


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