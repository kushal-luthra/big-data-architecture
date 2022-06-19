### IHS Markit System Design Round

Sharing the question below for reference.

We are given 3 data sources ->
1. Azure SQL Database -
   1. contains dealership data, with info ->
      1. dealer_id
      2. region
      3. OEM Data
   2. This data is updated once a week
2. MongoDb database -
   1. Customer Profile data
      1. customer_id
      2. dealer_id
      3. array of marketing history
   2. This data is updated once a day
3. Pub/Sub queue messages containing Sales 
   1. updated in real time
   2. contains sales information, with info ->
      1. customer_id
      2. dealer_id
      3. timestamp of Sale


Design a system to ingest data from multiple sources and report below Aggregates KPIs  on Dashboard
- aggregate sales total by Dealer, Month, Region, OEM etc