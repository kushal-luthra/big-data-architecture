
In addition to incorporating a Hadoop data lake, we also made all data services in this ecosystem horizontally scalable, thereby improving the efficiency and stability of our Big Data platform.
Unlike the first generation of our platform in which data pipelines were vulnerable to upstream data format changes, our second iteration allowed us to schematize all data, transitioning from JSON to Parquet to store schema and data together.

Limitations
1. small file problem - massive amount of small files stored in our HDFS 
2. latency = HIGH - data latency was still far from what our business needed. New data was only accessible to users once every 24 hours, which was too slow to make real-time decisions.
3. prcoess whole day snapshot again - both ingestion of the new data and modeling of the related derived table were based on creating new snapshots of the entire dataset and swapping the old and new tables to provide users with access to fresh data. The ingestion jobs had to return to the source datastore, create a new snapshot, and ingest or convert the entire dataset into consumable, columnar Parquet files during every run. With our data stores growing, these jobs could take over twenty hours with over 1,000 Spark executors to run.
4. upsert not available - reprocess whole days.

Uber architecture gen3
Limitations of existing system
1. HDFS scalability limitation
2. need something Faster data in Hadoop - data in real-time
3. Support of updates and deletes in Hadoop and Parquet needed. 
4. Faster ETL and modeling: need upsert processing in ETL pipeline

Solution -
1. Hudi -
   1. update, insert, and delete existing Parquet data in Hadoop. 
   2. allows data users to incrementally pull out only changed data, significantly improving query efficiency and allowing for incremental updates of derived modeled tables.
2. Generic data ingestion using Kafka & [Marmary](https://eng.uber.com/marmaray-hadoop-ingestion-open-source/), a data ingestion platform at Uber.
all streaming data ingested using Kafka and loaded using marmary.
Why Kafka -
It acts as unified ingestion service wherein all upstream datastore events (as well as classic logging messages from different applications and services) stream into Kafka with a unified Avro encoding including standard global metadata headers attached (i.e., timestamp, row key, version, data center information, and originating host). <br>
Both the Streaming and Big Data teams use these storage changelog events as their source input data for further processing.
Marmary -
It runs in mini-batches and picks up the upstream storage changelogs from Kafka, applying them on top of the existing data in Hadoop using Hudi library.<br>

