# net.bulletproof.dxn
********** Java spring boot (using Maven) application *************
****** Author: David Ndukwu ****
****** Submitted: 6th December 2015 ****


**** -------- SOME NOTES ------ ******

1. For the sake of simplicity and avoidance of rework, application 1 and application 2 have combined into a single application.
2. It is expected that the user of this application will set up a MongoDB database in order to run the application. Instructions on how to do this will be provided 

later.
3. This application will run on Tomcat port 9090 as the default port 8080 has been dedicated to the author's other applications (please see the 

'application.properties' file)
4. Finally, steps on how to run this application (e.g. wrt setting up Spring Boot/MongoDB/Mavern dependencies) will be ommitted from this guide as the developer 

assumes technical expertise on the part of his examiners.



**** Step 1: -------- Configure MongoDB Database ------ ******
1. Download and set up MongoDB to your preferred location (URI = https://www.mongodb.org/downloads#production). Navigate to the \bin directory of the mongoDB 

installation and type the below command:
>> mongod --dbpath C:\mongodbdata\customerdb --smallfiles

The action will start up a MongoDB database in the directory 'C:\mongodbdata\customerdb\', creating the associated files. Once sucessfully started, Mongos will now be 

ready to receive requests on its default port 27017.


**** Step 2: -------- Import Project Package into IDE------ ******
Launch a new instance of Eclipse or your prereferred IDE and import the project package. This is to enable the application to be run on an embedded tomcat, so no need 

to download and install Tomcat separately. The developer would like to crave the indulgence of his examiner to get this working.


**** Step 3: Application ------ ******
1. Start the embedded Tomcat for the Spring boot launcher from within the IDE. Once sucessfully started, the application will now be ready to receive requests on port 

9090. 
Note: For simplicity, the sample CSV file has been placed in the /src directory of the project. 

2. Open up your browser of choice and paste the string below on the address bar:
 URL = http://localhost:9090/customerData/endpoint
This will invoke the web service listening on the controller method getCustomerData(). This will load the entire CSV input and post the data as JSON to the URL, with 

the customerID deleanated uniquely by the number of records counter. Please see the CustomerData class for the fields permitted for a Customer.

3. Open up your browser of choice and paste the string below on the address bar:
 URL = http://localhost:9090/customerData/save
This will invoke the web service listening on the controller method saveCustomerData(). This action will save all the csv data input into a MongoDB database called 

'Customers'

4. Open up your browser of choice and paste the string below on the address bar:
 URL = http://localhost:9090/customerData/list
This will invoke the web service listening on the controller method listAllCustomerData(). This action will list all the customers from the MongoDB Customers database. 

Note the projection to eliminate the MongoDB default ID.

5. Open up your browser of choice and paste the string below on the address bar:
 URL = http://localhost:9090/customerData/{id}. Please replace id parameter by customer id e.g. http://localhost:9090/customerData/4 will cause an order to be created 

in the Orders database for the customer with ID = 4 (Firstname = Vinu, Lastname = Kumar). For simplicity, the order amount is fixed at 10 units of currency. Once the 

order has been successfully created, the service will refresh, listing a paged result (10 records) for the orders in the system (with the associated customer Data).

6.  Open up your browser of choice and paste the string below on the address bar:
 URL = http://localhost:9090/customerData?firstName=Vinu&lastName=Kumar. This action will cause the service to return the most recent order details (i.e limit = 1) for 

customer where Firstname = "Vinu" and Lastname = "Kumar".  


Note that for tasks 5 & 6 that the order id has been assumed to the the mongoDB generated _id field.



