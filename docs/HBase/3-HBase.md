#### How is data laid out in Hbase?
In traditional database, data is stored in rows and columns in a 2D data model, as shown below - <br>
![img.png](img_5.png) <br>

So, in traditional database we have a 2-dimensional data model, wherein each value can be associated with a ‘Id’ and column. <br>
Eg – ‘jill’ can be associated as id=3 and column=’To’ <br>

In Hbase, we have 4-dimensional data model,  <br>
•	Row Key <br>
•	Column <br>
•	Column Family <br>
•	Timestamp <br>
![img.png](img_6.png)<br>
Consider an example of Employee data, wherein it has below columns – <br>
•	empId <br>
•	dept <br>
•	grade <br>
•	title <br>
•	name <br>
•	SSN <br>
![img.png](img_7.png)<br>

In above, we have 4 dimensions as shown below - <br>
•	empId as row key – as it uniquely identifies a record. <br>
•	Dept, grade, title, name and SSN – columns. <br>
•	Dept, grade and title represent one column family (work), and Name & SSN as other column family (Personal) <br>
o	Column family represents logical grouping of data. <br>
•	Timestamp  <br>
o	It is represented as epoch time. Eg – for a title, a person is AVP at one epoch time, and is VP at another timestamp. <br>
o	Whole purpose of timestamp is to maintain versions.  <br>
	By default it will give you latest version. <br>

#### Row Key
-	Uniquely identifies a row <br>
-	Represented internally as a byte array <br>
o	All data in Hbase is internally represented as Byte array. <br>
o	There is no concept of INT, String, etc. <br>
-	Can be primitives, structures, arrays <br>
-	Sorted in ascending order. <br>
o	Reason to keep keys in sorted manner is that it can use Binary Search technique to quickly retrieve data in O(longN) time. <br>

#### Column Family
All rows have the same set of columns families <br>
Each column family is stored in a separate data file <br>
Set up at schema definition time. <br>
Can have different columns for each row. <br>
•	For example, if we have 10000 rows and we have 10000 rows, and we have 2 column families, then each of the 10000 rows are bound to have these 2 column families. But number of columns under the column family may vary from row to row. <br>
•	For example, we have 6000 rows with 10 columns and 4000 rows with 15 columns. <br>

#### Columns
Columns are units within a column family. <br>
New columns can be added in the fly. <br>
Syntax : ColumnFamily: ColumnName  <br>
eg- Work:Department. <br>

#### Timestamp
Used as the version number for the values stored in a column. <br>
The value for any version can be accessed. <br>


Likewise, we have another example- <br>
![img.png](img_8.png)<br>
