# How to Write Good Unit Tests 
(Source: https://developer.salesforce.com/page/How_to_Write_Good_Unit_Tests)
## Abstract
This article shows how to craft good unit tests. It explores the proper structure of unit tests, the code scenarios that unit tests should cover, and the properties of well-written unit tests. There are plenty of code samples interspersed throughout the article to demonstrate and help illustrate the concepts.

## Unit Test Introduction
A unit test is code that exercises a specific portion of your codebase in a particular context. Typically, each unit test sends a specific input to a method and verifies that the method returns the expected value, or takes the expected action. Unit tests prove that the code you are testing does in fact do what you expect it to do.     
   
The Force.com platform requires that at least 75% of the Apex Code in an org be executed via unit tests in order to deploy the code to production. You shouldn’t consider 75% code coverage to be an end-goal though. Instead, you should strive to increase the state coverage of your unit tests. Code has many more possible states than it has lines of code. For example, the following method has 4,294,967,296 different states:
    double getFraction(Integer a){ return 1/a; }    

Clearly, you wouldn’t want to test all of the different states for this program. Instead, you should probably test a few different inputs for this method, even if it means that you will have achieved 100% code coverage several times over.  

Three different states that you might consider testing are a positive input, a negative input and a 0 input. Testing with a positive input, and with a negative input will behave as expected. Testing with a 0 input however will yield a surprise System.MathException. This is just one example of why it makes sense to focus on testing the different states of your code instead of focusing on just the 75% code coverage requirement.

## The Value of Unit Tests
One of the most valuable benefits of unit tests is that they give you confidence that your code works as you expect it to work. Unit tests give you the confidence to do long-term development because with unit tests in place, you know that your foundation code is dependable. Unit tests give you the confidence to refactor your code to make it cleaner and more efficient.    

Unit tests also save you time because unit tests help prevent regressions from being introduced and released. Once a bug is found, you can write a unit test for it, you can fix the bug, and the bug can never make it to production again because the unit tests will catch it in the future.  

Another advantage is that unit tests provide excellent implicit documentation because they show exactly how the code is designed to be used.    

Lastly Salesforce.com uses unit tests to ensure that their releases don’t break customer code. The more tests you write, the better Salesforce.com is able to ensure they are not breaking customer customizations. Before and after every release Salesforce.com will run all test code written by their customers. Then after the release will run the code again. They then make sure that all tests had the same outcome before and after the release. That is why it is in your benefit to write good tests that cover as much of your code as possible.    

Many developers have discovered these advantages. Some developers, including me, believe so strongly in the value of unit tests that we write our tests first and our production code second. I’m going to show you an example of this test-first development practice a little later on in the article.

## Unit Test Structure
Let’s take a look at how unit tests are best structured. All unit tests should follow the same basic structure.  

A unit test should:    
* Set up all conditions for testing.
* Call the method (or Trigger) being tested.
* Verify that the results are correct.
* Clean up modified records. (Not really necessary on Force.com.)  

Let’s discuss each of these in turn.

### Set Up All Conditions for Testing
Typically, methods perform some sort of operation upon data. So in order to test your methods, you’ll need to set up the data required by the method. This might be as simple as declaring a few variables, or as complex as creating a number of records in the Force.com database. For example, if you have a trigger like this one that updates an Opportunity’s parent Account after the Opportunity is inserted:    

    trigger UpdateParentAccountWithOpportunityName on Opportunity (after insert) {
      // Create a Map from Account Ids to Opportunities.
      Map<Id, Opportunity> accountIdOpportunityMap = new Map<Id, Opportunity>();
      for(Opportunity oOpportunity : Trigger.new){
          accountIdOpportunityMap.put(oOpportunity.AccountId, oOpportunity);
      }

      // Create a list of Accounts to Update.
      List<Account> accounts = new List<Account>();
      for(Account oAccount : [SELECT Id, Most_Recently_Created_Opportunity_Name__c
                     FROM Account
                     WHERE Id IN :accountIdOpportunityMap.keySet()]) {
          oAccount.Most_Recently_Created_Opportunity_Name__c =
              ((Opportunity) accountIdOpportunityMap.get(oAccount.Id)).Name;
          accounts.add(oAccount);
      }

      update accounts;
    }

Then, your setup code could look something like this:    

    Account oAccount = new Account(Name='My Account');
    insert oAccount;
    Opportunity oOpportunity = new Opportunity(AccountId=oAccount.Id,
      Name='My Oppty', StageName='Prospecting',
      CloseDate=Date.today());

Your unit tests should always create their own test data to execute against. That way, you can be confident that your tests aren’t dependent upon the state of a particular environment and will be repeatable even if they are executed in a different environment from which they were written.    

If you find that many of your unit tests require very similar setup code, be sure to properly decompose the setup code so that you don’t repeat yourself.

### Call the method (or Trigger) being tested
Once you have set up the appropriate input data, you still need to execute your code. If you are testing a method, then you will call the method directly. In this case, we’re testing a Trigger, so we’ll need to perform the action that causes the trigger to execute. In our sample, that means that we will need to insert the Opportunity:  

    insert o;

### Verify the results are correct
Verifying that your code works as you expect it to work is the most important part of unit testing. It’s also one of the things that Force.com developers commonly neglect. Unit tests that do not verify the results of the code aren’t true unit tests. They are commonly referred to as smoke tests, which aren’t nearly as effective or informative as true unit tests.  

A good way to tell if unit tests are properly verifying results is to look for liberal use of the System.assert() methods. If there aren’t any System.assert() method calls, then the tests aren’t verifying results properly. And, no, System.assert(true); doesn’t count.  

Sample verification code for this trigger might look like this:  

      oAccount = [SELECT Name, Most_Recently_Created_Opportunity_Name__c
          FROM Account
          WHERE Id = :oAccount.Id];  

      System.assertEquals('My Oppty', oAccount.Most_Recently_Created_Opportunity_Name__c);  

Notice that this unit testing code explicitly verifies that the trigger performed the action that we expected.

### Clean up (is Easy!)
Cleaning up after unit tests is easy, because there’s nothing to do! Actions performed on records inside of a unit test are not committed to the database. This means that we can insert, delete, and modify records without having to write any code that will clean up our changes. Even the results of trigger executions that affect existing data are not committed!

### Where to put tests?
Your Trigger files can never contain code other than the Trigger definition, so Trigger unit tests must always be located in a separate class file.  

Unit tests for your classes are also required to be in a separate class. The most important reason for this is that by separating your class implementation and your unit tests, you will automatically be prevented from testing private methods and private properties. You shouldn’t test private methods and private properties because doing so will cause your unit tests to become a barrier to refactoring. With your classes and unit tests separated in to different files, you will always have the option to change the internal implementation of your classes should the need arise. If you ever do find yourself compelled to test a private or protected method, this is probably a strong indication that the method should be refactored in to its own stand-alone class.  

As an additional incentive, this best practice of separating unit tests and classes also allows you to take advantage of the @isTest annotation. The code inside of an @isTest annotated file does not count against the overall Apex code size limitation for your org.

### Putting it all together
Here's the complete unit test for the trigger, which it's put in UpdateParentAccountWithOpportunityName_Test.cls.

```java
    @isTest
    private class UpdateParentAccountWithOpptyName_Test{
        static testMethod void testUpdateParentAccount() {
            // Set up the Account record.
            Account oAccount = new Account(Name='Test Account');
            insert oAccount;

            // Verify that the initial state is as expected.
            oAccount = [SELECT Name, Most_Recently_Created_Opportunity_Name__c
              FROM Account
              WHERE Id = :oAccount.Id];
            System.assertEquals(null, oAccount.Most_Recently_Created_Opportunity_Name__c);

            // Set up the Opportunity record.
            String sOpportunityName = 'My Opportunity';
            Opportunity oOpportunity = new Opportunity(AccountId=oAccount.Id,
                                     Name=sOpportunityName,
                                     StageName='Prospecting',
                                     CloseDate=Date.today());

            // Cause the Trigger to execute.
            insert oOpportunity;

            // Verify that the results are as expected.
            oAccount = [SELECT Name, Most_Recently_Created_Opportunity_Name__c
                    FROM Account
                    WHERE Id = :oAccount.Id];
            System.assertEquals(sOpportunityName, oAccount.Most_Recently_Created_Opportunity_Name__c);
        }
    }  
```
Note the use of the @isTest annotation, as well as the general structure of the test - first the setup, then the action, and finally the verification.
