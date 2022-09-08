#### Probabilistic Data Structures

[Source](https://www.youtube.com/watch?v=F7EhDBfsTA8) <br>

### What?
- Allows to do things in-memory at scale, which otherwise is not possible inside MEMORY. <br>
- Have small footprint. <br>
- Need to accept a predictable level of inaccuracy. <br>

### Types
1. Bloom Filters - are for set membership. <br>
- That is check if value is present or not. <br>

2. Count-Min Sketch - <br>
- Does 2 things - check if present, and if yes, keeps track of count of occurrences. <br>
In normal scenarios, we can use hash map;  Key-value pair; <br>
Issue - more JVM heap size and more time; <br>
Soln - count-min sketch; <br>
Count + minimum + sketch (i.e. rough idea); <br>
Hashing function must all be different. That is each hash function shall give diff output for same input. <br> 
So if 3 functions, then 3 diff output for same input value. <br>

When initialising a sketch, a couple of values to be considered - <br>
* Epsilon - accepted error added to counts with each item; How wrong those counts could be? <br>
* Delta - probability that estimate is outside accepted error; what is the probability of the wrong counts being in tolerable range? <br>

These 2 variables help get us assess what is the Width and Depth of Count Min Sketch. <br>

Width = math.ceil(2/epsilon) <br>
Depth - math.ceil(-math.log(1-delta)/math.log(2)) <br>

We can use stream library for this. <br>

In count-min sketch, unlike bloom filter focus is on less memory consumption and the runtime isn’t sufficient. <br>

Eg - if you aren’t caring about count, but only looking at values like what is top 10 things bought today etc, this count min sketch is useful. <br>

Use cases - <br>
* Any kind of freq tracking. <br>
* NLP <br>
* Extension - heavy hitters(twitter trends), range query(Solr). <br> 

3. HyperLogLog (27.31 min) - <br>
It is for cardinality. <br>
For example in my list of things, how many unique items are there, what are unique visitors on my site. <br>

In normal scenario this can be done via Set. <br>
In HyperLogLog - <br>


