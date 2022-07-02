### 4 conditions for a database
1. Structured data – data is stored in rows and columns <br>
2. Random access – to values <br>
3. Low latency – in a given set of rows if you want to search one row, it can be done in short span of time. We have features like indexes to facilitate this. <br>
   Both low latency and random access are co-related – both happen alongside. <br>
4. ACID properties. <br>

#### ACID Properties 
**Atomic** <br>
Eg – A is transferring Rs 5000 to B’s a/c, then 2 operations are happening – debit in A’s a/c and credit in B’s a/c
Atomicity means either both operations happen, or none happen. <br>

**Consistency** <br>
It means the **constraints** should be met. <br>
Eg- we have employee table, and I want each employee to have new ID, here we can place unique key constraint.  <br>
We can place different kinds of constraints to ensure data is consistent as per our requirements. <br>

**Isolation** <br>
Isolation means that If 2 persons are operating on a row – both are making a change to row, then these operations shouldn’t happen at random.  <br>
There should be a sequence associated with them through lock mechanism. <br>
That is concurrent operations on database should appear as though they happen in some sequence. <br> 

**Durability**  <br>
It means that whenever the system fails due crash, power cut etc, it should not be that system comes down. <br> That is data is safe. <br>
Things should be up and running after failure.  <br>

    
#### Hadoop makes a very poor database, because ...
1.	Supports unstructured data <br>
2.	No random access <br>
-	Data kept in form of files and not rows and columns. <br> 
-	So, random access not possible. <br>
3.	High latency  <br>
4.	No ACID compliance <br>

To overcome limitation of random access or quick access of data, google published a paper on **Big Table**, a distributed storage system for structured data. <br>
To recall, google gave 2 main papers, initially  – <br>
•	GFS or google file system – for storage <br>
•	MapReduce – for processing <br>

Now, it gave another paper for quick searching – BigTable. <br>

Hbase is a distributed database management system, that runs on top of Hadoop. <br>
So, if you have 4 node Hadoop cluster, Hbase runs on this Hadoop cluster. <br>

![img.png](img.png)<br>

#### Hbase properties
•	Distributed – stores data in HDFS <br>
•	Scalable – capacity directly proportional to number of nodes in the cluster. <br>
•	Fault tolerant – piggybacks on Hadoop. HDFS gives replication of data, and so same for HBase. <br>

