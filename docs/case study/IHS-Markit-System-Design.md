### IHS Markit System Design Round

Sharing the question below for reference. <br>

We are given **3 data sources** -> <br>
1. Azure SQL Database - <br>
   1. contains dealership data, with info -> <br>
      1. dealer_id <br>
      2. region <br>
      3. OEM Data <br>
   2. This data is updated once a week <br>
2. MongoDb database - <br>
   1. Customer Profile data <br>
      1. customer_id <br>
      2. dealer_id <br>
      3. array of marketing history <br>
   2. This data is updated once a day <br>
3. Pub/Sub queue messages containing Sales <br> 
   1. updated in real time <br>
   2. contains sales information, with info -> <br>
      1. customer_id <br>
      2. dealer_id <br>
      3. timestamp of Sale <br>


Design a system to ingest data from multiple sources and report below Aggregates KPIs  on Dashboard <br>
- aggregate sales total by Dealer, Month, Region, OEM etc <br>