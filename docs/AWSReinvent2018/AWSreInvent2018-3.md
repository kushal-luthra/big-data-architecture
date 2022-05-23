## Collect Layer

![img_6.png](images/img_6.png)

### Types of data sources
![img_8.png](images/img_8.png)<br>
In collection phase, often times you have different data sources -><br>
- transactional databases like relational databases, MongoDB, or NOSql database.<br>
Often times these are records that you need to be able to analyze and process.<br>
We can call those **Transactions**<br>
- Similarly, you might have log data like Media files, Application Log files.<br>
These are large **Files/Objects** that you may be needing to store.<br>
- Finally, we have streaming data like device sensors, IoT platforms.<br>
These are **Events** data.<br>

Each of those collections methods often require different way of collecting of data.<br>

And, often times, storing these data is also different. <br>
For Transactional data, it usually goes into NoSQL or relational database.<br>
(we will discuss the criteria for this).<br>
For Files/Objects data, the defacto standard is HDFS/S3 - we need a big object store for which datalake based on HDFS/S3 is needed.<br>
For stream storage, we have 3 main options -><br>
- Apache Kafka <br>
  - open source project.<br>
  - well established.<br>
  - High throughput distributed streaming platform.<br>
  - so a client which wants to migrate their data can begin by moving over their kafka systems to ec2.<br>
- Amazon Kinesis Data Streamings <br>
  - Managed Stream **storage**<br>
  - for example, here we define number of shards, and each shard pcoesses a 1000 records/seconds.<br> 
  Say, you wanna scale up to 100,000 records, you would only need to change the number of shards required, and not be worried about number of servers being used, etc.<br>
- Amazon Kinesis Data Firehose<br>
  - Managed **data delivery** <br>
  - lets say you have streaming data, and instead of capturing real time insights, you want to capture that data, and do some sort of advanced processing or offline procesing of that data.<br>
  - here AWS Kinesis Firehose comes into picture. It allows you configure an end point to be abel to store thet data. This could be S3 bucket (data lake) or Elastic Search (ELK Stack). <br>
  This allows you to configure various destionations in order to store the data as the data is flowing in.<br>
  In data streams you configure number of shards.<br>
  In firehose, its purely based on amount of data that is sent though that pipe.<br> 
    - So, you dont have hvae to pre-provision, but there are soft limits to amount of data to be processed per second.<br>


### Which Streaming/Message Storage should I use?
![img_7.png](images/img_7.png)<br>

SQS (Simple Queue Service) Vs Streaming Storage -><br>
- If your use case if a simple producer and single consumer - go for SQS.<br>
- If yours is a case of complex architecture wherein you have multiple consumers and also want to store stream data, opt for Stream Storage.<br>

### Which File/Object Storage should I use?

![img_9.png](images/img_9.png)<br>
Here S3/HDFS are defacto standards.<br>

1. S3 allows you to build your data lake in a robust manner.<br>
You can run various analytics on it.<br>
Its natively supported by wide number of tools including hadoop ecosystem  like HDFS, presto, hive etc can talk to S3 to be able to read and process that data.<br>

2. Decouple Storage and Compute<br>
- no need to run compute clusters for storage (**unlike HDFS**)<br>
  - S3 is cheap ~ Storage & EMR for compute<br>
  - in HDFS, you need to keep cluster always on.<br>
- can run transient Amazon EMR clusters with  Amazon EC2 spot instances.<br>
- multiple & heterogenous anlaysis clusters  and servcies can use the same data.<br>
  - consider a scenario wherein you ingest data into S3. Now since storage si separated from compute, youcan run different clustes on top of same source of data.<br>
  For example, one load can be of spark on EMR(based on reserved instances), and other for GPUs (based on spot instances)<br>

3. Designed for 99.999999999 % durability (11 Nines).<br>
Tremendous data reliability.<br>

4. Data replication within the same region is done automatically.<br>

5. Security - it used encryption at rest and in transit both.<br>

#### Data Tiering
![img_10.png](images/img_10.png)<br>
Its about maintaining data in different tiers based on use case.<br>

Use of s3 implies no use of HDFS?<br>
No. One can store their working datasets like quick analysis intermediate data in HDFS for faster access.<br>
For example, say you to do some analysis on data that involves iterative reads, and here you can use HDFS storage on EMR cluster.<br>

AWS gives S3 analytics report that recommends which object should be placed in which tier.<br>

Now, lets talk about databases.<br>
![img_11.png](images/img_11.png)<br>
When it comes to databases, we have large number of options based on purpose.<br>

|Purpose|Database |
|caching|AWS elasticCache, DynamoDB Accelerator|
|Graph DB | Amazon Neptune|
|Key-value document| Amazon DynamoDB|
|SQL/RDBMS|Amazon RDS (Relational Database Service)|


Amazon DynamoDB Accelerator (DAX) - its a dynamoDB Front end which has a write-through cache.<br>

### Which Store should I use?
![img_12.png](images/img_12.png)<br>

Choosing a right database involves asking right questions, including -><br>
- what is the Data Structure ?<br>
- How will data be accessed?<br>
- What is the temperature of the data?<br>
- what will be solution cost?<br>

![img_13.png](images/img_13.png)<br>

![img_14.png](images/img_14.png)<br>

What is the data structure?<br>
- Do I have a very fixed schema?<br>
- am I doing key-value lookups -> eg - we have tons of session data, and we can use dynamoDB or key-value store.<br>
- is it very very relational data such that you are constantly traversing  the graphs<br>

Also data access pattern is important.<br>
eg- <br>
- amazon aurora - very very high throughput transactional data need<br>
- if you need analytical capability of OLAP then use Amazon Redshift.<br>

![img_15.png](images/img_15.png)<br>
