### Glance / InMobi

#### Round 1
There is a streaming service called Show-Stream ( like Netflix, Disney etc) that has customers spread over the globe. <br> 
Show- **Stream** does not have a data warehouse in place.  <br>
Design the pipeline to ingest the data from json **events** residing in S3 and build a **Data Warehouse**. <br> 
How will you go about it? How do you go about deciding the **tech stack**? <br>
```
Source S3://showstrteam/rawEvents/<date>/<hr>/file_n.json ( multiple events in one file, 100 such files)
```
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
