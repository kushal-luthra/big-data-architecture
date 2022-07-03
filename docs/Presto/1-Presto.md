#### What is the Presto?
Presto is an _open source_ _distributed_ system that can run on multiple machines. <br> 
Its **distributed SQL query engine** was built for fast analytic queries. <br>

Presto was initially designed at Facebook as they needed to run interactive queries against large data warehouses in Hadoop.  <br>
It was explicitly designed to fill the gap/need to be able to run fast queries against data warehouses storing petabytes of data. <br> 

Presto is a SQL based querying engine that uses an **_MPP architecture_** to scale out.  <br>
Because it is a querying engine only, it separates compute and storage relying on connectors to integrate with other data sources to query against. <br> 
In this capacity, it excels against other technologies in the space providing the ability to query against: <br>
- Traditional Databases <br>
- Non-relational Databases <br>
- Columnar file formats like ORC, Parquet and Avro – stored on - HDFS, AWS S3 etc. <br> <br>


#### Presto Architecture
At a high level, the Presto architecture looks something like this: <br>

![img.png](img.png) <br>

A typical Presto deployment will include one Presto Coordinator and any number of Presto Workers. <br>
- Presto Coordinator: Used to submit queries and manages parsing, planning, and scheduling query execution across Presto Workers. <br> 
Coordinators connect with workers and clients via REST. <br>
- Presto Worker: Processes the queries, adding more workers gives you faster query processing. <br>

When it comes to managing the data itself, Presto has several important components that enable this. <br>
- Catalog: Presto Catalogs contain the information about where data is located – they contain schemas and the data source. <br> 
When users run a SQL statement in Presto, it means they’re running it against one or more catalogs. <br> 
Eg - Hive catalog, Postgres catalog etc. <br>
- Tables and schemas: If you’re familiar with relational databases, it’s the same concept.  <br>
- Connector: Connectors are used to integrate Presto with external data sources like object stores, relational databases, or Hive. <br>

Last, when it comes to running Presto queries there are some specific components to know. <br>
- Statements and Queries - Presto executes SQL statements. It parses SQL statement, creates a query along with a distributed query plan that is then distributed across a series of Presto workers. <br> 
A statement is simply passing along the instructions while the query is actually executing it. <br>

- Stage: To execute a query, Presto breaks it up into stages. There may be several stages that implement different sections of the query. <br> 
Every query has a “roots” stage which aggregates all the data from other stages.  <br>
Keep in mind the stages themselves don’t run on Presto workers, they may run on the database underneath (this is called push-down). <br>

- Task: Stages (from above) are implemented as a series of tasks that may be distributed over a network of Presto workers. <br> 
Tasks have inputs and outputs and are executed in parallel with a series of drivers. <br>

- Split: Splits are sections of larger data sets and how tasks operate. When Presto schedules a query, the Coordinator keeps track of which machines are running tasks and what splits are being processed by tasks. <br>

- Drivers and Operators: Tasks contain one or more parallel drivers and they are operators in memory. An operator consumes, transforms and produces data. <br>

- Exchange: Exchanges transfer data between Presto nodes for different stages of a query.  <br>
Tasks produce data into an output buffer and consume data from other tasks using an exchange client. <br>

#### Deployments, Configurations & Installations
In practice, you might deploy Presto in the cloud or on-prem. Presto sits between your BI tool and your storage. <br>

**Alluxio** provides a multi-tiered layer for Presto caching, enabling consistent high performance with jobs that run up to 10x faster, makes the important data local to Presto, so there are no copies to manage (and lower costs), and connects to a variety of storage systems and clouds so Presto can query data stored anywhere.


#### Presto Vs Hive
| Presto                                                                                                                                                                                             | Hive                                                                                                                                                      |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| ANSI SQL                                                                                                                                                                                           | HiveQL                                                                                                                                                    |
| not available in Presto                                                                                                                                                                            | Users can plugin custom code in Hive                                                                                                                      |
| Presto can handle limited amounts of data                                                                                                                                                          | Can handle larger volume of data                                                                                                                          |
| low failure tolerance                                                                                                                                                                              | can tolerate failures                                                                                                                                     |
| Presto uses MPP architecture to query HDFS without map-reduce <br> MPP Querying engine that executes queries in memory, pipelined across the network between stages, thus avoiding unnecessary I/O | uses map-reduce architecture and writes data to disk <br> MPP Querying engine that does Batch processing using Apache Tez or MapReduce compute frameworks |

Note ->
- Spark : general purpose processing engine. <br>
- Hive   : MPP Querying engine. Does Batch processing using Apache Tez or MapReduce compute frameworks. <br>
- Presto : MPP Querying engine. Executes queries in memory, pipelined across the network between stages, thus avoiding unnecessary I/O. <br> <br> <br> <br>


[Credits 1](https://www.alluxio.io/learn/presto/architecture/) <br>
[Credits 2](https://www.alluxio.io/learn/presto/)
