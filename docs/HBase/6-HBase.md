#### CAP Theorem
Very important w.r.t. distributed databases. <br>
•	C – consistency <br>
•	A – availability <br>
•	P – partition tolerance <br>

CAP theorem says that out of these 3, we can only get 2. <br>
There is no way we can design a system with all 3 features as guarantee. <br>
We have to decide our system based on our requirements – which feature we are Ok not having. <br>

Based on above, we have 3 kinds of systems – <br>
•	CA system – consistency and availability <br>
•	AP System – availability and partition tolerance <br>
•	CP system – consistency and partition tolerance <br>

#### Consistency
- It means each node will hold the latest value. <br>
- Whenever we seek result, we shall get latest value not older one. <br>
- Eg – sending message to someone on WhatsApp; if that person is not connected to internet, that person shall not get any garbage info depicting that message until the time he connects back to internet. Instead, we shall give him correct data. <br>
  We have to exactly give data which is latest. Eg - chat application. We don’t want to give stale info or garbage info to message sender. Rather there will be a timeout and status get updated as soon as receiver receives message. <br>
- Similarly, in banking, consistency is priority. If bank doesn’t know latest balance it will deny transaction. It is ok to deny transaction if it is doubtful – but cannot allow transactions.  <br>
  So, in banking we need consistency. <br>
- Consistency means ->  
    - Latest value is shown, and it is a guarantee that value shown is latest <br>

#### Availability
- System should always give a response no matter what. <br> 
- Even if it is not sure that value is latest, it will return something. The system won’t timeout, the system won’t error out. <br>
- To make sure system always gives response or do not error out, we need to compromise on one thing – that we cannot have consistency. Sometimes we give old data. <br>

#### Partition tolerance
- It states that a system will continue to operate even when there is network or partition failure. Even if system gets disconnected, it will continue to operate. <br>

#### CAP Theorem w.r.t Distributed Systems
- CAP theorem applies to distributed systems that store data. <br>
- CAP theorem states that it is impossible for a distributed data store to simultaneously provide more than 2 out of 3 guarantees, namely consistency, availability, and partition tolerance. <br>
- Consistency guarantees that every node in the distributed system returns the same most successful and recent write <br>
- Availability is when every requires receives a response without the guarantee that it contains the most recent write <br>
- Partition tolerance is when the system continues to function and upholds guarantees in spite of network failures. <br>

![img.png](img_11.png)<br>

CA – provided by RDBMS systems <br>
We won’t discuss CA further <br>

We focus on AP and CP. <br>
Why – when we talk about distributed systems, we need to ensure partition tolerance is there. <br>
So, the tradeoff is always between availability and consistency. We have to choose one or the other. <br>

NoSQL systems store data in a distributed manner across a cluster of interconnected machines and provide network partitioning. <br>
There are 2 flavors of NoSQL databases that provide different set of guarantees – <br>
- CP – HBase and MongoDB <br>
- AP – Cassandra and DynamoDB <br>

![img.png](img_12.png)<br>
![img.png](img_13.png)<br>
![img.png](img_14.png)<br>

CP – Eg - chat application. We don’t want to give stale info or garbage info to message sender. Rather there will be a timeout and status get updated as soon as receiver receives message. <br>
Likewise in banking application, we need CP -> GooglePay and Paytm gives error as consistency is important. <br>

AP – MMT travel portal.  <br>

Cases where we chose Consistency over Availability. <br>
We want latest results. If results are not latest give error or timeout. <br>
Eg – chat application, UPI, banking etc. <br>

Cases where we prefer availability over consistency. <br>
We want immediate results even if it is not the latest. <br>
Eg – MMT booking hotel on it –  <br>It shows a price, but system isn’t able to confirm if rates are latest or not. It tries to go with earlier result. Here we don’t want to error or timeout to customer as it will degrade user experience. <br> 


#### Proving CAP Theorem by Contradiction Approach
![img.png](img_15.png)<br>
![img.png](img_16.png)<br>
![img.png](img_17.png)<br>
![img.png](img_18.png)<br>
![img.png](img_19.png)<br>

Let us try to provide cap theorem by contradiction. <br> <br>
Consider a case wherein we have 2 node cluster and each maintaining an initial value for object O with initial value v0. <br> <br>
Now, both nodes have a copy of vO with them <br> <br>
Then if network failure happens, then client request comes in such that it updates value of Object v0 to v1 on G1. <br> <br>
Now, another client comes in, and connects to G2 machine and pulls value of object O, and it gets vO and not v1 which is latest. If you want to be consistent, the system should wait until network gets restored. So, there will be a timeout if you want to be consistent. <br> <br>
This contradicts our all 3 guarantees. <br> <br>
CAP theorem proved. <br> <br>
Note network partition means network failure. <br> <br>
