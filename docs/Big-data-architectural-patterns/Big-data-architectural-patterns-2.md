# Big Data Architectural Principles

![img_3.png](images/img_3.png)<br>

1. build loosely coupled or decoupled system. <br>
This holds true not just for Big Data Systems, but for any system. <br>
This means - the way I analyze my data shouldn't be dependent on the way I analyze my data. <br>
So, I could change the way I collect my data by changing the tool and it shouldn't be impacting the way I store, process and/or analyze my data. <br>
This lets you be future-proof, lets you iterate, and lets you migrate over time. <br>

2. Being able to pick right tool for the right Job. <br>
If your system is loosely coupled, it gives you flexibility to pick right tool for right Job. <br>
Rather than trying to pick one tool to do everything, choose one which fits your use case. <br>
Eg-  <br>
   - for streaming you an use Kafka, AWS Kineses <br>
   - for ML - sagemaker <br>
   - for storage - RDS, HDFS/S3 etc <br>

3. Leverage managed and serverless services - <br>
Not an architectural principle, but more of a recommendation. <br>
By leveraging managed and serverless services, you can focus on what really matters. <br>
It lets you focus on analytics, the transformations, the ETL, rather than loading softwares and otehr pieces. <br>

4. Use event-journaling design Patterns - <br>
It means as you are collecting data into big data systems its a good practice to not override your data. <br>
So, if you are getting data records, and some of those data records are getting corrected, then rather than correcting those records, keep appending to your dataset. <br>
Why -> if you have large volume of data, and if there is ever an issue like -> <br>
* your job has a bug, Or <br>
* you accidently delete your data, <br> 
...you have the option to replay history and regenrate your data. <br>

So, go for immutable datasets (data lake), materialized views. <br>

5. Be cost-conscious <br>
Lot of times, big data doesnt have to mean big cost. <br>
If you architect it correctly, say you are building a hadoop system and are decoupling storage and processing layers, you can build a very cost effective, performant system, and keep the cost down. <br>

6. Use ML to enable you applications. <br>
This is a growing trend wherein more and more companies are leveraging ML to build their competitive advantages. <br>

## A simplified data processing pipeline
below, we see simplified data processing pipeline.
![img_4.png](images/img_4.png)

Your exact use case may not match it, but you should look at logical constructs here.

for example, in  Collect layer, you need to ask questions like ->
- How am I gonna capture and collect this information?
- If I have different datasets, I may not be collecting and storing these datasets in the same way.
- If I have GPS data or clickstream data, I would like to collect it dir=fferently from imagery or satellite data.

You must also note there is a cycle here. Its not exactly a waterfall model. 
Often times you collect and store raw data, and that raw data is in original form like csv, json etc.
Then you often times would like to take that raw data and create curated datasets - query optimized datasets to be able to very rapidly access that data. This could be through ML, Data warehousing etc. 
This is a iterative process wherein you take raw data, and pass it through various transformations processes, and convert it to normalized/den-normalized form in order for it to be consumed by different stakeholders.



## What is the temperature of my data?
![img_5.png](images/img_5.png)

Often times we talk about temperature of your data, that means velocity of your data, your queries and your analytics.
We will discuss about temperature across those specturms.