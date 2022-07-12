#### Introduction
Databases don't impact your functional requirement. <br>
you can meet your functional requirements using any database you want. <br>
But non-functional requirement are impacted by kind of database you choose and these include -> <br>
- certain kind of query pattern <br>
- certain kind of data structure <br>
- scale requirements - these are different kind of databases designed to handle different kind of scales. <br>

#### Factors impacting choice of database
1. structure of data <br>
2. query pattern <br>
3. amount of scale you need to handle. <br>

#### Caching solution
Whatever solution you choose in a System Design Interview, there is likely requirement for some kind of caching solution. <br>
Use cases here include -> <br>
- you are querying a database, and you don't want to query it lots of time, you can cache your value in the cache. <br>
- if you are making remote call to a different service, and it is having high latency, you might want to cache the response of that system locally in a caching solution. <br>

Cache normally includes key and a value. <br>
key = your predicates that are in the WHERE clause in your query <br>
Value = response you are expecting form the service <br>

common solution - redis, memcache. <br>
Redis - battle tested for use as caching. <br>


#### Blob storage
Suppose you want to store images for amazon ecommerce website or netflix video. <br>
In this case, you use blob storage like amazon S3. <br>
Note - this is not really a database, since in a database you generally query your data. This is plain storage case. <br>
Now, along with S3 you would want to include CDN (Content delivery network). CDN is used to distribute the same image geographically in lot of locations. <br>
eg - product image is stored in s3 which is being queried or accessed by people across the globe. So for betetr performance, you can store it locally in their geography for faster response times. <br>
So, to summarize, for Blob kind of content - S3 + CDN. <br>

#### Search Engines
If you are building a product like Amazon and you want to provide text searching capabilities on various products. <br>
So, seller has uploaded product along with Title and Description. <br>
Now, you would want users to be abel to search that product by providing text of the title and description. <br>
Likewise, users in Netflix want to search movie name, movie titles, movie genres, etc. <br>
Similarly, you want to deisgn something like Google Maps where you want ot provide text searching capabilities with support for Fuzzy Search. <br>
So, for all of these use cases, you would be using Text Search Engine. <br>
Common ones are Elastic Search and Solr, and both are built on top of Apache Lucene. <br>
Lucene fundamentally provides text searching capabilities. <br>

Fuzzy Search - suppose you are providing text search capabilities, and user makes a typo. <br>
for example - Instead of _AIRPORT_, he types _AIRPROT_ <br>
Now, you wouldn't want to return null as it distorts user experience. <br>
Instead, you would want to return closest option based on Edit distance. <br>
for example, AIRPROT can be converted to AIRPORT by interchanging 'R' and 'O' - they are at edit distance of 2. <br>
So you can provide a level fuzziness factor that your search engine needs to support. <br>

One thing to note is that ElasticSearch and Solr are not databases. These are Search Engines. <br>
Why important -> <br>
Whenever you write something in a Database, your database gives you a guarantee that data wouldn't be lost. <br>
Now, both of these Search Engines don't give such guarantee. They claim that they are giving a good enough availability and redundancy, but potential data could be lost. <br>
So, you should NOT keep any of these as your primary sources of Truth. <br>
Your primary data source should be somewhere else, and you could load your data into either of these systems to provide searching capabilities and these 2 are very efficient at search. <br>

#### Time Series Database
If your want to store metrics kind of data. <br>
Say you are building a system like graphite, grafana, prometheus. <br> 
These are Application Metrics Tracking systems. <br>
Let's say we have a use case wherein there arr lot of applications which are pushing metrics related to their Throughput, CPU utilization, Latencies, etc <br> 
And you want to build a system to support that. <br>
Here we use Time Series Database. <br>
Think of time series database as an extension of relational database but with not all functionalities and certain additional functionalities. <br>
Regular databases have ability to update  records and query random records. <br>
but whenever you are building a metrics kind of system, you never do random updates. You always do sequential updates, in append-only mode. <br>
Also, the read queries that you do, they are kind of bulk queries with the time range - last hour, last day, last week data etc. <br>
But you don't do a random read or random update. <br>
Time series databases are optimized for this kind of query pattern and input pattern. <br>
So, there are a lot of time series databases like influxDB, openTS db (open time series database). <br>

Suppose you want to write lots of information, and you want store that info for various kind of analytics requirements. <br> 
Eg - amazon or uber - analytics on all transaction. <br>
So, you would need a data warehouse, which is basically a large database wherein you push your data and provide querying capabilities on top of your data to service lot of reports. <br>
Now, these are generally  not used fo transactional systems. <br>
They are used for offline reporting. <br>
eg - hadoop, redshift. <br>


#### SQL Vs NoSQL : which one to choose?
![img.png](img.png) <br>
Now, lets discuss on bigger scenarios wherein your want to choose between a relational and non-relational databases, i.e. SQL vs NoSQL. <br>
You need to ask 'what is structure of my data?' If structured info - choose RDBMS. <br>
For example, User Profile - name, age, address. These are standard information that every person would have, and so can use RDBMS. <br>

Suppose your data is structured, next question that comes up is that 'do you need ACID guarantees?' <br>
If yes, then RDBMS like Oracle, postgres, SQL Server, etc would suit. <br>
For example - bank transaction -> Here every transaction would have 2 components - credit and debit, and both should happen - in one account money is debited and in another account money is credited. <br>
Further, you would want that when user checks balance, they should reflect the latest correct value. Here consistency is important. <br>
Likewise, for Inventory management system and Order Management System, we need ACID guarantees. <br>

Now lets you have relational data, but you don't need ACID guarantees. <br>
That is, there is no use case of atomicity requirements. <br>
You could choose either relational or non-relational database, it wouldn't make much of a difference. <br>
Normally you would be able to map a structured data into a NoSQL model. <br>
so, either of these scenarios would be fine. <br>

Now, lets say you do not have structured data, then what do you do? <br>
There are a bunch of scenarios where your use case might fit in. <br>
These include -> <br>
    a. document DB <br>
    b. columnar Db <br>

##### Document DB
Suppose you are trying to build catalogue kind of system for an e-commerce website like amazon which has information of all items available on that platform. <br>
Here each item would have certain kind of attributed, which may or may not overlap with other items. <br>
e.g. -shirt (size, color) vs refrigerator (volume, power saving rating) Vs Milk (quantity, expiry date). <br>
Normally you would to store this info in JSON and dump into a database. <br>
But you would also would want ot query it.  <br>
Now, querying on JSON is a bit tricky in relational databases. <br>
But there are certain kinds of database that are optimized for these kinds of queries. <br>
These are databases where you have a lot of data not just in terms of volume, but in terms of structure so you have lot of attributes and wide variety. <br>
Here you need documentDB. <br>
There arr lot of providers of DocumentDb like MongoDB, Couchbase. <br>
earlier we looked at elastic search and Solr for text searching - these are special cases of document databases. <br>
Now, lets say you don't have relational data and you also don't have complex queries, you could still use document DB, provided your use case doesn't fall into Columnar db category discussed below. <br>

##### Column Database
Let's say you have an ever-increasing data. <br>
eg - uber - driver of uber are continuously sending location, and you have use case of managing this ever-increasing data - however number of queries are finite. <br>
Here we use columnar database like HBase, Cassandra. <br>
Note - Cassandra is easier to deploy unlike HBase (which is coupled with Hadoop), so may prefer Cassandra. <br>

Often there is no single database that can fit your design. <br>
Consider amazon inventory - when you are managing inventory on that side, you need to make sure you are not overselling any item. <br> 
Say you have only 1 quantity of an item, and there are 10 users who want to buy it, then you want to have there is ACID property so as to ensure there is only 1 of the user to commit the transaction, and other user should not be able to commit the transaction. <br>
Here it would make sense to use an RDBMS. <br>
But data in Amazon is ever-increasing data, and as it grows you cannot purge it since there are often legal restrictions in terms of purging the older data. <br>
So, instead we use Cassandra along with RDBMS. <br>
Here we keep details of order until it is delivered in RDBMS, and post that the corresponding info gets moved to Cassandra, and entry is removed from RDBMS. <br>

Consider another example - here you want to find sale of sugar in last 5 days. <br>
Now, sugar is not a brand. It is a category and has different variety, and this info is available in document database like MongoDb, wherein there is info about userId and corresponding order info and you extract list of all users who purchase sugar in last 5 days. <br>
Now, use this list to query RDBMS (for latest orders) and Cassandra(for older info). <br>
So, here we are using all the 3 systems, in combination to provide various querying capabilities. <br>


Credits : [CodeKarle](https://www.youtube.com/watch?v=cODCpXtPHbQ) <br>
Credits : [Sandeep Kaul](https://www.linkedin.com/in/sandeep1904/) <br>






