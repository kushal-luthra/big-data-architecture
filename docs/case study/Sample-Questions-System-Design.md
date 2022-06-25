### Meesho

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


### Glance / InMobi

#### Round 1
There is a streaming service called Show-Stream ( like Netflix, Disney etc) that has customers spread over the globe. <br> 
Show- Stream does not have a data warehouse in place.  <br>
Design the pipeline to ingest the data from json events residing in S3. <br> 
How will you go about it? How do you go about deciding the tech stack? <br>

Source S3://showstrteam/rawEvents/<date>/<hr>/file_n.json ( multiple events in one file, 100 such files)

What are these events ?   <br>
These events are all actions that the user performs on the app/browser :- user creation, playing a show, pausing a show, searching content etc etc. <br>


#### Round 2
We are given streaming input with information in format given below --> <br>
```
Input: UserID, follow/unfollow, recipeientUserID
```

As an output you need to get 2 kinds of information - <br>
1. List of users I follow <br>
2. Count of users I follow <br>

Questions -> <br>
a. How will you capture this information? <br>
b. how will you store/transform the data? <br>

### Uber System Design Interview Questions
System Design competency. <br>

Below is Uber Schema -   <br>
```
rider - rider id, name, age, gender, dob, phone, current payment type , current payment account;

rider_bookmarks - bookmark id, rider_id, bookmark_tag('home','office' etc), bookmark_locn id;

driver - driver id, name, joined date, curr cab id; check if running multiple vehicle so have curr cab id;

cab - vehicle type, per_km, base_fare, etc; cab id, cab type, brand, reg no, year of make;

map_grid = locn in a map grid of 1x1km; id, latitude,longitude;

locn - human readable landmark locn - india gate, school, rly station etc; id, map_grid_id, is_landmark, related_locn_id, zip_code;

trip - trip_id, cab id,rider id,start time, end time,request time, is surge applied, surge %, rider rating, driver rating, start locn id, end locn id;

payment - id, type, base fare, surge fare, total fare, payment timestamp, card no, transaction id

```

Question – <br>
System Design to handle scenario wherein customers who used Uber app to take a ride but couldn’t subscribe to the ride. <br> 
That is ,they drop off at the final tunnel. <br>


### Economist Case Study 

The Economist Group’s core business is our global news subscriptions business. Users subscribe to a weekly online magazine. <br> 
They go through various stages: anonymous visitor ==>registered user ==> subscriber. <br>

All subscription information is stored in upstream **transactional systems** - **Salesforce** and **Zuora**. Different events can take place - cancellations, re-subscription/renewals. <br> 

From time to time, the Group offers various promotions and offers in order to acquire new customers. <br> 
The user behaviour data (**click stream** info) is also available in Google Analytics.  <br>

Design a **data warehouse** and associated **data pipelines** for the Economist Group so that the analysts and data scientists can report on key metrics.  Document the <br> 
1. Architecture <br>
2. Data flow, data model <br>
3. Data observability <br>
4. KPIs, metrics <br>
5. Assumptions <br>
