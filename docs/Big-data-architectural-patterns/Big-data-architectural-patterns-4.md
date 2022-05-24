## Data Processing Layer
![img_16.png](images/img_16.png)<br>

### Interactive & Batch Analytics
Lets look at interactive & batch analytics. <br>
![img.png](images/img_17.png) <br>
 
- Elastic Search - useful for Log data Text Search capabilities. <br>
- Redshift & Redshift Spectrum - for data warehousing needs. <br>
- Athena ~ Hive - perform SQL based queries on Data that resides on S3. <br>
  - S3 Select - is somewhat similar to Athena, but there are some differences. <br>
  - You can think about AWS S3 Select as a cost-efficient storage optimization that allows retrieving data that matches the predicate in S3 and glacier aka push down filtering. <br> 
  - AWS Athena is fully managed analytical service that allows running arbitrary ANSI SQL compliant queries - group by, having, window and geo functions, SQL DDL and DML. <br>
- EMR - Its Hadoop & Spark as a service that lets you run various platform applications. <br>
  - one thing special about EMR is that you have root access to EC2 instances that EMR is using unlike other managed services. <br>
    eg - in RDS, you ENIN point that allows you to perform database functions, but you cannot do SSH on it. <br>

### Streaming/Real-time Analytics
![img_1.png](images/img_18.png) <br>
If you look at Hadoop ecosystem, the number of services that perform real-time analytics has been growing - Spark Streaming, Flink, Storm.  <br>
Just like Athena allows you to perform SQL queries on S3 even though it is not a relational database, AWS Kinesis Data Analytics allows you to perform SQL queries on your real time data even though it is not really a database. <br>
So you could write SQL - tumbling windows, random cut forest, different sort of expressions to analyze data.

In respect to AWS Lambda, one thing to note is that it polls every second.<br>
That means if you are looking for sub-second latency, use other tool like Amazon KCL.<br>

### Predictive Analytics
![img_2.png](images/img_19.png) <br>

**Application Services**<br> 
One thing is to note that make sure to write your data in open standards like orc, parquet, CSV or JSON. <br>
That ways you can use different tools with it for your use case. <br>

**Platforms**<br> 
This layer allows us to build models and test them.<br>


### Which Analytics should I use?
![img_3.png](images/img_20.png)





