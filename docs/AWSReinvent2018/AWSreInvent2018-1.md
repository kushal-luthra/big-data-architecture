![img.png](images/img.png) <br>
There are different kind of analytical systems.<br>
Some customers are looking at doing batch-interactive analytics with their data.<br>
Others are looking at being able to to take real time data feeds, and store them for insights, and some go beyond, seking building of data models on top of it, power inferencing and do ML with that data.<br>

As we step step into the architecture discussion, we are going to discuss architecture for -><br>
- Streaming procesisng<br>
- datalakes and batch interaction<br>
- machine learning.<br>

Note - you dont need to pick them right away. You can start small, architect it in a way that it enables you to build more and more features on top of it over time, incrementally.<br>

Now, lets look at different model of delivering big data services.<br>
![img.png](images/img_.png)<br>

Virtualized - eg- EC2 instances that we create & install kafka on top of it. Customer owns environment and manages it themselves.<br>
Managed Services - EMR (hadoop platform as a service), RDS - managed by AWS - customers still thinking about requirements like what configuration you need, what should be auto-scaling policy etc.<br>
Serverless/Clusterless/Containerized - Lambda, Athena, Glue - tehse are services that abstract out the servers away from you.<br>

Various services - both open source and AWS based are mentioned below -<br>
![img_1.png](images/img_1.png)<br>

Going forward we will discuss -><br>
* different kind of reference architectures.<br>
* what tools should one choose?<br>
* How?<br>
* Why?<br>
![img_2.png](images/img_2.png)<br>