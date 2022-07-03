#### Background   
CTM is just starting its journey to make use of the data that has been captured since launch. <br> 
The first data driven capability identified by the business is the automatic sorting of the insurance products returned to a customer based on their past selections and similar customer selections. <br>  
In essence we want to understand better what customers are focused on when using the site and therefore use that understanding to present their results in a manner that is more personalised.  <br>
 
#### Technical Detail 
 
Our events in JSON format are pushed onto Kafka from a number of services, capturing all activity on the main site e.g., changes to customer personal details, when a customer has purchased insurance etc.  <br>
These events are read from Kafka and saved in an S3 bucket in a single sub directory.   <br>
 
#### Task for the Interview 
 
Assuming that nothing else besides the above exists; come up with high-level options to build this data processing pipeline. <br>
 
You can make any assumptions necessary about the platform or the data, but please state what these are and the reasons behind them.  <br>
Considering aspects such as streaming vs batch processing, testing, performance, implementation and documentation. <br>

#### Please answer the following 
 
•	Whiteboard a high-level design for the solution (present in any tool, whiteboard, PPT, Miro etc.) <br>
•	Detail your thought process needed to efficiently implement the new technical solution  <br>
•	For Streaming assume data is pushed to Kafka as described above, for batch assume data is on some filesystem/object store such as SFTP or S3. <br>
•	Describe the challenges that might arise regarding data quality across the platform <br>
