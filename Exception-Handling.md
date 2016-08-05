
##  Exception Handling

### Abstract

Similar to most modern languages, Apex supports exception handling using try/catch blocks. As a best practice you should always encapsulate your code within a try/catch when there is a possibility of an exception occurring within your code. 

### Catching Exceptions

As of version 36.0 of the Salesforce API, there are 24 different types of exceptions that can be caught. When catching exceptions you should always try to catch the specific types of exceptions, whenever possible, as well as include a try/catch block to catch general exceptions outside of the specific ones when it makes sense. 

Working with our example from before notice that we are catching a "DMLException". Since this is the only type of exception that could occur within this code, there was no need to wrap the entire code within a general exception block. 

```java
public with sharing class SampleClass
{
    public List<Account> updateLeads(List<Lead> leads)
    {
        try
        {   
           insert leads;
        }
        catch(DMLException e)
        {
            System.Debug(‘An error occurred while inserting leads. Exception: ‘ + e.getLineNumber() + ‘:’ + getStackTraceString);
        } 
    }
} 
```

If we expand our example with some more logic we need to make sure that we catch any unexpected exceptions that would occur when looping through our lead list. Perhaps we are setting a value that is not an acceptable value for the data type of a field on the lead record. 

Take note that we are catching 3 types of exceptions:

1. QueryException – To catch any exceptions that occur when retrieving the lead records.

2. DMLException – To catch any exceptions that occur when inserting the lead records.

3. Exception – To catch any other exceptions that may occur when looping through the lead records.

```java
public with sharing class SampleClass
{
    public List<Account> getLeads(Date CreatedDate)
    {
         List<Lead> leads;

         try
         {
              leads = [SELECT id,FirstName,LastName FROM Lead WHERE CreatedDate =:   CreatedDate];
         }
         catch(QueryException e)
         {
                 System.Debug(‘An error occurred while retrieving leads. Exception: ‘ + e.getLineNumber() + ‘:’ + getStackTraceString);
         }

         System.Debug(‘Leads Retrieved: ‘ + leads);
         Return leads;
    }

    public List<Account> updateLeads(List<Lead> leads)
    {
        try
        {
            try
            {
                for(integer i=0;i<leads.size();++i)
                {
                   //DO SOMETHING
                }
                insert leads;
            }
            catch(DMLException e)
            {
                System.Debug(‘An error occurred while inserting leads. Exception: ‘ + e.getLineNumber() + ‘:’ + getStackTraceString);
            } 
        }
        catch(Exception ex)
        {
           System.Debug(‘An unexpected error occurred while inserting leads. Exception: ‘ + e.getLineNumber() + ‘:’ + getStackTraceString);
        }

    }
} 
```

### Custom Exceptions

Since you can’t throw built-in Apex exceptions, but can only catch them, you can create custom exceptions to throw in your methods. That way, you can also specify detailed error messages and have more custom error handling in your catch block. 

To create your custom exception class, extend the built-in Exception class and make sure your class name ends with the word "Exception".

```java
public class OrderException extends Exception
{

}

public with sharing class OrderController
{

     try
     {
         //DO SOMETHING
     }
     catch(Exception e)
     {
       throw new OrderException(‘Could not create order.’,e);
    }
}
```

If you find that you need to create exceptions that are multiple levels deep, then it may be a good time to start thinking about creating a custom exception class so that your exceptions are more easily traceable when trying to debug. 