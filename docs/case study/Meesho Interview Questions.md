#### Round 1
Design a data platform. <br> 
multiple sources and sinks. <br>
connectors for reading/writing data. <br>

purpose -  <br>
1. read data -> perform ETL (transform on sequence of rules - string commands  in spark sql  -> load into sink). <br>

2. configurable. <br>

3. define pipeline :  <br>

    a pipeline is bunch of similar events. event can be supplier data etc. <br>
    events of similar data is from same source for example supplier data from kafka. <br> 
    
4. Transformation are tied to events not pipeline. <br>
    event 1 -  T1-> T2  <br>
    event 2 -  T1 -> T4 -> T5 <br>
    
    transformation are event specific. <br>
    source and sink are pipeline specific. <br>

Also, what will be its Base classes and functions. <br>
Purpose of functions. <br>


#### Round 2
Consider an Ecommerce Website, with ClickStream events data being generated at the rate of 500k/second. <br>
These events can be add_to_cart, view, order, wishlisted, ... etc. <br>
The storage is Cloud Storage. <br>

Requirements - Build a data platform with following characteristics --> <br>

1. Self serve platform to provide ETL (hourly, daily, weekly etc) <br>
e.g.  <br>
- Product view count per hour per product, <br> 
- Product view count per day per product etc, <br>
- User has ordered product after clicking on ad in last 3 days <br>

2. Adhoc queries/Notebook interface - Analysts (300 DAU) <br>

3. ML use cases (feature engineering, training etc - timetravel queries, historical data ) } hudi | deltalake <br>

Existing - 1500 - 2000 jobs (sql) <br>
1. Might contain duplicate <br>
2. Non optimized (No predicates/filters) <br>

What are things you will take care of for new jobs/sql? <br>

