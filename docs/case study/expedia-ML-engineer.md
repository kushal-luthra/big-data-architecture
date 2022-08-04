#### Expedia ML Engineer Round 1
Q1 - Find the largest number that can be formed with the given digits <br>
``` 
# Find the largest number that can be formed with the given digits.
# Input = [4, 7, 9, 2, 3]
# Output: 97432 

# Input = [8, 6, 0, 4, 6, 4, 2, 7]
# Output: 87664420
```
 <br> <br>

Q2 <br>
![img_2.png](images/img_5.png) <br>
![img_3.png](images/img_6.png) <br>
![img_4.png](images/img_7.png) <br>


#### Expedia ML Engineer Round 2
Topics covered are -> <br>
1. Discuss your main project in company, and what is your Technology stack? <br>
2. Spark internals -> <br>
   1. What are the common params used while submitting Spark job? <br>
   2. How to optimize spark shuffle? <br>
   3. How does spark execute your job once you do a spark-submit? <br>
   4. Discuss challenges faced in setting up Streaming job, and what are various spark sql commands in streaming data job? <br>
3. Spark hands-on  <br>
``` 
Assume you get input in this format in a spark dataframe, write a spark code to get What were the top 5 ranked songs in 2021? 
The output should contain columns - rank, group_name, and song_name.

year  year_rank  group_name  				artist      song_name
2021  1          Kesha						Kesha        LMN
2021  2			 Taylor						Taylor       XYZ
2021  3			 Kesha feat. Snoop Dogg     Kesha        ABC
2021  3          Kesha feat. Snoop Dogg     Snoop Dogg   ABC
2021  4          Eminem                     Eminem       DEF
2021  5          Lady Gaga feat. Rihanaa    Lady Gaga    GHI
2021  5          Lady Gaga feat. Rihanaa    Rihannaa     GHI 

Ans -
cols_list = ['year_rank', 'group_name', 'song_name']

df\
.where('year=2021 and year_rank<=5')\
.select(cols_list)\
.distinct()

```

#### Expedia ML Engineer Round 3
This is primarily System Design round. <br>
Questions asked are -> <br>
Discuss your main project in company, and what is your Technology stack? <br><br>

Case Study <br>
Expedia partners with Hotels to consult them to earn more revenue by pricing their facilities rightly. <br>
 
Consider a use case wherein, partners want answer to below questions -> <br>
- what is my Inventory Utilization?  <br>
Hotels allocate rooms to different vendors - Expedia, MMT, Go-Ibibo, etc. <br>
Inventory Utilization = % of rooms utilized as proportion of number of rooms allocated to it by Hotel. <br>
For example, if 50 rooms allocated, and 30 got booked, then inventory utilization is (30/50)*100 = 60% <br>
 <br>
- What has been my historical inventory utilization? <br>
<br>
- How do I foresee occupancy in coming days - next 7 days, 30 days, 90 days, etc. <br>
  - This part is about applying ML Algo on predicting data. <br>
  - Here again, questions included - <br>
    - How will I store my ML Algo object? <br>
    - Where will I place my ML Algo object? <br>
    - How will I refresh it - full vs delta refresh? <br>