Hadoop is not a database. <br>
BigTable paper led to Hbase, which is a distributed database management system running on top of Hadoop. <br>

To recall 4 requirements of database are – <br>
1.	Structured data <br>
2.	Low latency <br>
3.	Random reads <br>
4.	ACID compliance <br>

Let us see how Hbase fares against these requirements of database. <br>
1.	Structured – loose data structure. <br>
-	HBase is not as rigid as traditional databases like MySQL. For example, all rows will have equal number of columns.
2.	Low latency – real time access using row-based indices called row keys. <br>
3.	Random access – row keys allow access updates to one record. <br>
4.	Somewhat ACID compliant – some transactions will have ACID properties. <br>

Hbase can offer 2 things – <br>
1. Quick searching – based on row-keys. <br>
2. Processing – mapreduce. <br>
   Not the main use case as we already have Hive for this.


### Hbase Vs Relational Databases
Properties of Hbase – <br>
1.	Columnar store  <br>
2.	Denormalized storage <br>
3.	Only CRUD operations <br>
4.	ACID at row level. <br>

#### Columnar storage
Traditional databases provide row-based architecture, while Hbase provides column based <br>

![img.png](img_1.png)<br> <br>

1 row is divided into many rows depending on number of columns. <br>
Advantage of columnar of stores – <br>
a.	Sparse tables – if your table is sparse, no waste when storing sparse data. <br>
b.	Dynamic attributes – update attributes dynamically without changing storage structure. <br> 

Sparse Tables -  <br>
In traditional databases, columns which have no values, they still occupy space even if no data is present in them. Thus, there is wastage of space. <br>
In Hbase, we handle sparse tables. <br>

Dynamic attributes – <br>
Unlike Hbase, in traditional databases changing column types/adding new columns/dropping them – all of this is a painful task. <br>
In columnar store of Hbase, each row can have a different number of columns. For example, in below image, we have ‘expiry’ column for id 1 and 4 only. <br>

![img.png](img_2.png)<br> <br>

Further no extra space – sparse table handled. <br>
Dynamically adding columns. We can have different columns with different rows. <br>

#### Denormalized Storage
In traditional database, data is normalized. <br>
That is data is divided into multiple small tables. <br>
In Hbase, we don’t prefer normalization.  <br>
That means we store data into 1 big table. <br>
Advantage. – read a single record to get all details about a person in a single read operation.  <br>

![img.png](img_3.png)<br> <br>

#### CRUD operations in Hbase 
In normal database, we have join operations. <br>
In Hbase, we can only perform CRUD operations. <br>
Join/groupBy/orderBy – not supported in Hbase. <br>
CRUD – create, read, update & delete. <br>
Note – since data is denormalized, so no need of Joins.  <br>
This is why Hbase tables should be self-contained – i.e., contain all required info in 1 row. <br>

#### ACID Compliance at row level
Traditional databases are ACID compliant. <br>
Hbase provides ACID compliance at row level. <br>
That means,  <br>
•	Whenever we are trying to update multiple columns for a single row, then either all of them will be updated or none will be updated. <br>
•	When we talk about updates for multiple rows in Hbase then there is no guarantee. There could be a possibility that few rows got updated and rest not updated. <br>
•	It also means, even if we are updating single column in multiple rows, there is no guarantee. <br>

![img.png](img_4.png)<br>