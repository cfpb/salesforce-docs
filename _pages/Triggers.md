## Triggers
There are many considerations that must be taken in account when developing apex triggers. A poorly written trigger can easily cause your application to cease to function.
## Muting Triggers
It is a best practice when developing triggers that you have the ability to easily disable the functionality of triggers. This is especially useful for when you need to perform data loads, or if a trigger is causing user errors. By default there is no easy way to disable a trigger using configuration. Once a trigger or other apex class has been migrated to production, the only way to disable it would be by using the metadata API to delete it.  

In order to allow for making it easy to disable triggers, all triggers must have logic allowing the triggers to be disabled by profile and/or user using custom settings or custom metadata types.   

The example below shows how to implement the logic to disable a trigger using custom settings.

```java 
   Public with sharing class Helper 
    {
        public static Boolean IsTriggerEnabled()
        {
            TriggerExecutionSettings__c settings =     TriggerExecutionSettings__c.getValues(“AccountInsertUpdate”);

            List<Id> profileIds = settings.EnabledProfileIds__c.split(‘’’);
            Map<Id,Id> profileIdMap = new Map<Id,Id>();

            For(integer i=0;i<profileIds.size();++i)
            {
                profileIdMap.put(profileIds[i],profileIds[i]);
            }

            If(settings.enabled__c == true && profileIdMap.get(userInfo.getProfileId()) != null)
            {
               return true;
            }
            else
            {
               return false;
            }
        }
    }	  
```

```java
Public with sharing class Helper AccountInsertUpdateTrigger on Account (before insert, before update)
    {
       if( triggerHelper.IsEnabled())
       {
          //DO SOMETHING
       }
    }
```

## Trigger Maintainability
When Salesforce triggers execute there is no guarantee in what order they will execute. This is why you should never have multiple triggers that operate on the same object and operation. Triggers should always be separated by operation for each object. For example: If you created two triggers that both handled the before update operation, there is no guarantee as to which trigger would execute first. This could create confusion when trying to debug the code and unexpected results.  

When developing triggers, it is best to think of each trigger as the driver for your code. You want to separate the business logic to a separate helper class to keep the code within the trigger neat and separated by operation.   

Within the trigger you should create a fork for each trigger operation for before/after, and insert, update, and delete. Once you have identified the trigger operation, such as before update, you would then fire the helper method for before update in a separate class. This makes it easier to understand what the trigger is doing.  

Take a look at the code sample below that executes a trigger for before insert and update as well as after update.

```java
Public with sharing class Helper AccountTrigger on Account (before insert, before update, after update){
        if( triggerHelper.IsEnabled()){
            if( trigger.IsBefore()){
               if( trigger.IsInsert(){ 
                  AccountTriggerHelper.BeforeInsert();
               }          
               else if( trigger.IsUpdate()){        
                  AccountTriggerHelper.BeforeUpdate();
               }
            }
            else if ( trigger.IsAfter()){
               if( trigger.IsUpdate()){
                  AccountTriggerHelper.AfterUpdate();
               }
            }
        }
    }
```

## Never Hardcode Ids
When deploying Apex code between sandbox and production environments, or installing Force.com AppExchange packages, it is essential to avoid hardcoding IDs in the Apex code. By doing so, if the record IDs change between environments, the logic can dynamically identify the proper data to operate against and not fail.  

Here is a sample that hardcodes the record type IDs that are used in an conditional statement. This will work fine in the specific environment in which the code was developed, but if this code were to be installed in a separate org (ie. as part of an AppExchange package), there is no guarantee that the record type identifiers will be the same. 


```java
 for(Account a: Trigger.new){
        //Error - hardcoded the record type id
        if(a.RecordTypeId=='012500000009WAr'){     	  	
            //do some logic here.....
        }else if(a.RecordTypeId=='0123000000095Km'){
            //do some logic here for a different record type...
        }
    }
```


Now, to properly handle the dynamic nature of the record type IDs, the following example queries for the record types in the code, stores the dataset in a map collection for easy retrieval, and ultimately avoids any hardcoding.   

```java
//Query for the Account record types
    List<RecordType> rtypes = [Select Name, Id From RecordType 
                           where sObjectType='Account' and isActive=true];
     
    //Create a map between the Record Type Name and Id for easy retrieval
    Map<String,String> accountRecordTypes = new Map<String,String>{};
    for(RecordType rt: rtypes){
        accountRecordTypes.put(rt.Name,rt.Id);
        }
     
    for(Account a: Trigger.new){
        //Use the Map collection to dynamically retrieve the Record Type Id
        //Avoid hardcoding Ids in the Apex code
        if(a.RecordTypeId==accountRecordTypes.get('Healthcare'))
        {     	  	
            //do some logic here.....
        }else if(a.RecordTypeId==accountRecordTypes.get('High Tech'))
        {
            //do some logic here for a different record type...
        }
    }   
```

By ensuring no IDs are stored in the Apex code, you are making the code much more dynamic and flexible - and ensuring that it can be deployed safely to different environments.

## Custom Settings 
Custom settings are a useful tool when you have application specific settings that you wish to store that let you configure the application rather than having to make a code change every time these settings change.   

Try to utilize custom settings whenever possible when you find that you need to hardcode a static value such as email addresses or Salesforce Ids within your application.  

Another good use of custom settings is to allow for tweaking of the performance of the application. For example: Instead of hard coding the number of records to process for a batch apex method to 200 records, you could create a custom setting that allows you to easily change the number of records to be processed for each batch.   

Additionally as mentioned above in the “Muting Triggers” section, Custom settings can be used to allow you to enable/disable triggers, or other code, since you are unable to do this easily from your production environment natively.

## Enforcing Sharing Rules in Controllers

Like other Apex classes, all controllers and controller extensions run in system mode. Typically, we want a controller or controller extension to respect a user's organization-wide defaults, role hierarchy, and sharing rules. We can do that by using 'with sharing' keywords in the class definition. Note that if a controller extension extends a standard controller, the logic from the standard controller does not execute in system mode. Instead, it executes in user mode, in which the profile-based permissions, field-level security, and sharing rules of the current user apply. Unless you have a good reason for needing to expose all records of a class to the running user then all classes should ALWAYS use the “with sharing” keywords.  

If you do not use this practice it is possible that a user could gain access to records that they normally would not have access to.

## Governor Limits

Because of the multitenant nature of Salesforce, various types of governor limits are enforced to ensure that one tenant does consume all of the resources. The following are best practices to avoid hitting limits.  

* Limiting queries by using static class variables to store query results instead of firing frequent queries.  
* Never use SOQL/SOSL/DML in loops.
* Leverage custom settings to create custom sets of data, as well as create and associate custom data for an organization, profile, or specific user. All custom settings data is exposed in the application cache, which enables efficient access without the cost of repeated queries to the database. This data can then be used by formula fields, validation rules, Apex, and the SOAP API.
* Making sure that database statements such as insert(), update(), and delete() operate in bulk 
* Use system methods to track governor limits: Apex has a System class called Limits that lets you output debug messages for each governor limit. There are two versions of every method. The first returns the amount of the resource that has been used in the current context, while the second version contains the word limit and returns the total amount of the resource that is available for that context. Using these methods judiciously ensures that the execution governor limits are never hit.
* Enable governor limit warning emails: When an end-user invokes Apex code that surpasses more than 50% of any governor limit, you can specify a user in your organization to receive an email notification of the event with additional details. 
* Asynchronous execution: Use asynchronous apex (@future) appropriately. Async apex gets its own governor limits but there are a maximum of ten @future methods within a single apex transaction. Do not call future methods from triggers.
* Batch Apex: Use of Batch Apex to handle millions of records. Every batch gets its own set of governor limits. Do not initiate batches from triggers.
