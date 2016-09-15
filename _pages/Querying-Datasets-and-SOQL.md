## Querying Large Data Sets
The total number of records that can be returned by SOQL queries in a request is 50,000. If returning a large set of queries causes you to exceed your heap limit, then a SOQL query for loop must be used instead. It can process multiple batches of records through the use of internal calls to query and queryMore. If is possible to hit the heap limit and never even reach the max record limit of 50,000 records if you are querying a large number of fields in an object.  

    // A runtime exception is thrown if this query returns 
    // enough records to exceed your heap limit.
    Account[] accts = [SELECT id FROM account];

Instead, use a SOQL query for loop as in one of the following examples:  

    // Use this format for efficiency if you are executing DML statements 
    // within the for loop.  Be careful not to exceed the 150 DML statement limit.
    for (List<Account> acct : [SELECT id, name FROM account
                            WHERE name LIKE 'Acme']) 
    {
        // Your code here
        update acct;
    }

Let the Force.com platform chunk your large query results into batches of 200 records by using this syntax where the SOQL query is in the for loop definition, and then handle the individual datasets in the for loop logic.  

**Note:** This approach is the one time when it is acceptable to use DML (insert, update, delete) inside of a for loop. You still need to be weary of the 150 DML statement limit within the loop.  

## SOQL Query Optimization
When writing SOQL queries you want to make sure that your queries will perform when running against both small and large datasets. The following are some best practices to use to build performing SOQL queries.
* Always limit the number of records that to be returning by the query by using the LIMIT keyword.
* Never use fields that are not indexed in the WHERE clause.
* Keep your queries as selective as possible and use custom indexes to improve performance.
* Try to avoid using the “NOT IN” keyword as this is a very expensive in regards to performance.
* Try to use the “AND” operator, and limit the use of OR operators in your statements.
* Try to avoid using a combinations or “AND” and “OR” operators in your statements.
* Try to avoid using the “ORDER” operator as it takes a lot of processing
* Use StartsWith as much as possible for query filters. Techniques such as reverse phone numbers can be used in this approach.
* Use record types to help with data segmentation
* Create skinny tables for commonly searched fields to decrease search times.
* Use the Salesforce query optimizer located in the developer console to make sure that your query will perform. Performing queries should have a score of less than 1. The closer to 1 the score, the worse the query will perform.

#### Demonstrative Example
The following are examples of bad SOQL queries.

|Query | Reason |
|-------------|:--------|
```SELECT Id, Name FROM Account```|This will return every record in the account object. This query will most likely never finish.  
```SELECT Id, Name FROM Account WHERE Active = true```|This query is more selective than the last, but still would return too many records and would most likely never finish.  
```Select Id, Name FROM Account WHERE Name NOT IN: myAccountsList```|This query fairly selective, but would still be an expensive query because the “NOT IN” operator is very processing intensive. Use the “IN” operator instead of “NOT IN” wherever possible.

The following are examples of good SOQL queries

|Query | Reason |
|-------------|:--------|
```Select, Id, Name FROM Account WHERE name = ‘Salesforce’ LIMIT 1``` |Very selective query limiting the records returned to 1.  
```Select Id, Name FROM Account WHERE CreatedDate = Yesterday LIMIT 99```|Very selective query limiting to just the records created within the past 24 hours. Also the query limits the total records returned to 100.
 
## Never use SOQL queries or DML statements inside FOR loops
A common mistake is that queries or DML statements are placed inside a for loop. There is a governor limit that enforces a maximum number of SOQL queries. There is another that enforces a maximum number of DML statements (insert, update, delete, undelete). When these operations are placed inside a for loop, database operations are invoked once per iteration of the loop making it very easy to reach these governor limits.  

Instead, move any database operations outside of for loops. If you need to query, query once, retrieve all the necessary data in a single query, then iterate over the results. If you need to modify the data, batch up data into a list and invoke your DML once on that list of data.  

This practice definitely creates some complications but is critical to ensuring governor limits are not reached.
Here is an example of what NOT to do (*incorrect lines):   

    //For loop to iterate through all the incoming Account records
    for(Account a: accounts) {
      	  
        //THIS FOLLOWING QUERY IS INEFFICIENT AND DOESN'T SCALE
        //Since the SOQL Query for related Contacts is within the FOR loop, if this 
        //trigger is initiated 
        //with more than 100 records, the trigger will exceed the trigger governor limit
        //of maximum 100 SOQL Queries.
      	  
        *List<Contact> contacts = [select id, salutation, firstname, lastname, email 
                              from Contact where accountId = :a.Id];
 		  
        for(Contact c: contacts) {
            c.Description=c.salutation + ' ' + c.firstName + ' ' + c.lastname;
 	  	   
            //THIS FOLLOWING DML STATEMENT IS INEFFICIENT AND DOESN'T SCALE
            //Since the UPDATE DML (data manipulation language) operation is within the FOR loop, if this trigger is 
            //initiated with more than 150 records, the trigger will exceed the trigger 
            //governor limit of 150 DML Operations maximum.
      	                  	      
            *update c;
        }    	  
    }