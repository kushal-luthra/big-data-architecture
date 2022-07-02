So far, we have discussed so far – <br>
•	What is Hbase? <br>
•	Why NoSQL required and where Hbase solves our purpose? <br>
•	What is CAP theorem? <br>

Cassandra is an alternate to Hbase but with Hadoop it is not that much famous. <br>

Topics –
1.	What is Casandra
2.	CAP theorem & Cassandra
3.	How does Cassandra cluster looks like?
4.	Tunable read/write consistency.
5.	Diff between HBase and Cassandra


#### What is Casandra?
It is a distributed column-oriented database and highly performant. <br>
Since distributed, so highly scalable – add few more nodes and it scales out. <br>

When do we use Cassandra -> When we require transactional activities or quick searching – low latency retrieval of data, we can use Cassandra. <br>

So far this is similar to Hbase. <br>

#### CAP theorem & Cassandra (Eventual Consistency)
Hbase is CP system. <br>
Cassandra is AP system. <br>

Consistency is eventual – if you retrieve data it might respond in some time. <br>
Consider you have LinkedIn profile and someone likes your posts. <br>
Consider you have 1000 likes on posts, and after this 1 more person does a like – system shows 1001 likes, but sometimes it gives 1000 likes. That is not latest value. <br>
That is, we can tolerate late information in this use case. Here getting a response, i.e. Availability is more important. <br>

It won’t show error, and gives eventual consistency. <br>


#### How does Cassandra Cluster looks like?
In case of Hbase, we run on Hadoop cluster, and like Hadoop, Hbase also follows Master-Slave architecture, wherein - <br>
-	HMaster = master <br>
-	Region Server = Slave <br>
If master goes down, the system crashes ~ non-availability. <br>

In Cassandra, it follows Peer-to-Peer architecture, wherein -> <br>
-	There is no master <br>
-	All nodes are peers <br>
-	It’s a Decentralized architecture <br>
-	Nodes communicate using Gossip Protocol. <br>

A master slave architecture can be down at time when master fails. <br>
In Cassandra, because of Decentralized Architecture, where there is no master, it is highly available. <br>


#### Tunable Read/Write Consistency
Cassandra is a AP System. <br>
It by default compromises on the consistency in order to be highly available. <br>
Step 1: Client will send request to get value of A. <br>
Step 2: The request will go to one of the machines, for instance node5. <br>
Step 3: Node 5 will go and talk to Node 1 to get the results. <br>
Step 4 : Node 5 will return the result to the client. <br>
Cassandra provides you a tunable consistency through Quorum. <br>
So, you can tune to get result -based on 3 approaches  <br>
-	1 node. <br>
o	Default mode. <br>
o	Availability is High + Consistency is Low <br>
-	Quorum based <br>
o	I want the result only when 2 nodes agree on the same result. Here Quorum = 2 <br>
o	Availability is High + Consistency is moderate <br>
-	All Node based  <br>
o	I want the result only when all nodes agree on the same result. <br>
o	Availability is Low + Consistency is High  <br>


#### Differences between Hbase and Cassandra

##### Similarities
- Both are NoSQL databases <br>
- Both hold data in columnar fashion <br>
- Both are highly scalable <br>
- Used when you want to perform <br> 
  - transactions (update/inserts) <br>
  - quick reads. <br>
- Low latency operations <br>

##### Differences

|Hbase	| Cassandra                                                                         |
|--------------------|-----------------------------------------------------------------------------------|
|master-slave architecture	| decentralized architecture (so highly available as no dependency on single master) |
|CP| 	AP + Tuneable Consistency (one node, all node, Quorum based)                     |
|runs on top of Hadoop cluster - so data kept in HDFS	| has a separate cluster                                                            |
|preferred choice when working on Hadoop cluster| Not suited with hadoop                                                            |	 
|Hbase can be accessed using Shell commands, which are somewhat hard to understand. <br>You can use Apache Phoenix on top of Hbase to give you SQL-like interface.|	It has its own SQL-like syntax, called Cassandra SQL (CSQL).|
