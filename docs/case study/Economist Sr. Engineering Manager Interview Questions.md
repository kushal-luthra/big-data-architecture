### Economist Case Study 

The Economist Group’s core business is our global news subscriptions business. Users subscribe to a weekly online magazine. <br> 
They go through various **stages**: <br>
_anonymous visitor ==> registered user ==> subscriber_. <br>

All subscription information is stored in upstream **transactional systems** - **Salesforce** and **Zuora**. <br>
Different **events** can take place - cancellations, re-subscription/renewals. <br> 

From time to time, the Group offers various promotions and offers in order to acquire new customers. <br> 
The user behaviour data (**click stream** info) is also available in Google Analytics.  <br>

Design a **data warehouse** and associated **data pipelines** for the Economist Group so that the analysts and data scientists can report on key metrics.  Document the <br> 
1. Architecture <br>
2. Data flow, data model <br>
3. Data observability <br>
4. KPIs, metrics <br>
5. Assumptions <br>