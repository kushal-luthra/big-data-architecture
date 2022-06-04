# Data Consumption Process

![img.png](images/img_26.png)

![img_1.png](images/img_27.png)


When it comes to consumption, we have 2 categories of users -
1. Business users - who want to make sense of data. <br>
The service here involved is applications like visualization applications like Tableau and Amazon Quicksight (amazon managed visualization tool), Kibana (visualization on elastic search).<br>

2. Data Scientist - They want to get access to an endpoint and play with data. They would like to use Athena, Redshift, etc.<br>


We could ask questions like what type of BI or UI one could use in this type of solution.<br>
Answer depends on who is user and what is the function they are doing.
Eg - 
Business user would not prefer to be asked to use Jupyter notebooks, nor would a data scientist enjoy being placed in front of dashboard with little flexibility to play around with data.<br>
In this stage, solutions you would find would be a suite of different UI being used to be able to perform these analytics.<br>

Jupyter - used in data science space.<br>
Sagemaker allows you to have a managed Jupyter environment, running both Jupyter and Jupyter Lab.<br>
You could also run managed Jupyter or managed notebooks on EMR. So, if you are looking at just Hadoop ecosystem, we have option of EMR or managed hadoop environment.<br>

ELK Stack - Kibana can allow doing Log analysis.<br>
There are also partner products like Splunk, Tableau, Looker and MircoStrategy.<br>