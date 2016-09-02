# What to Test 
Broadly speaking, you should test your custom business logic. How thoroughly you test that business logic will probably vary depending on specific situations. On one end of the spectrum, you might choose to implement just a few tests that only cover the code paths that you believe are most likely to contain a bug. On the other end of the spectrum, you might choose to implement a large suite of unit tests that are incredibly thorough and test a wide variety of scenarios. Wherever a given project falls on that spectrum, you should be sure to write unit tests that verify your code behaves as expected in "normal" scenarios as well as in more "unexpected" scenarios, like boundary conditions or error conditions.  

In order to give you a better idea of the kinds of things that you should be testing, I'll walk through the process of writing unit tests for an implementation of a Stack data structure that can be used to store Strings.

## Stack Interface
The first thing that I need to do is define the publicly accessible methods for our StringStack class:  

    public class StringStack {
        public void push(String s) { }
        public String pop() { return null; }
        public String peak() { return null; }
        public Boolean isEmpty() { return true; }
    }

You’ll notice that I haven’t written any real implementation code for these method definitions. That’s because I’m going to use Test Driven Development techniques in this example. In Test Driven Development, unit tests are written before any real implementation code is written. I’ve found that writing my unit tests first helps me better understand how clients of my code are going to use it.

## Testing Normal Conditions
Next, I’m going to write a test that will exercise my code in the most basic way – I’m going to add just one String value to the Stack:  

    /* Verifies that push(), pop() and peak() work correctly
     * when there is only 1 object on the Stack. */
    static testMethod void basicTest() {
        // Instantiate a StringStack.
        StringStack oStack = new StringStack();

        // Verify the initial state is as expected.
        System.assert(oStack.isEmpty());

        // Set up some test data.
        String sOnlyString = 'Only String';

        // Call the push() method and verify the Stack is no longer empty
        oStack.push(sOnlyString);
        System.assert(!oStack.isEmpty());

        // Verify that the value we pushed on the Stack is the one we expected
        String sPeakValue = oStack.peak();
        System.assertEquals(sOnlyString, sPeakValue);
        System.assert(!oStack.isEmpty());

        // Verify the Stack state after pop() is called.
        String sPopValue = oStack.pop();
        System.assertEquals(sOnlyString, sPopValue);
        System.assert(oStack.isEmpty());
    }  

If you run this test right now, your code is going to fail:

![Failed Test](/img/failed_test.png)

So, now that we know what we need to implement, we’re going to write the code needed to pass the first unit test:  

    public class StringStack {
        private List<String> stack;

        public StringStack(){
            stack = new List<String>();
        }

        public void push(String s){ stack.add(s); }

        public String pop() {
            return stack.remove(lastItemIndex);
        }

        public String peak() {
            return stack.get( lastItemIndex );
        }

        public Boolean isEmpty() { return stack.isEmpty(); }

        // Helper Property
        private Integer lastItemIndex {
            get { return stack.size() - 1; }
        }
    }  

Now if we run the unit test again, the code passes the test:

![Passed Test](/img/passed_test.png)  

In fact, you can see that we have 100% code coverage. We could stop here, but we really want to be confident in the code, so there are a few more conditions that we’re going to test. We haven’t yet verified that the Stack implementation handles multiple values, and that it can pop() them in the correct order, so the next test is going to verify those things:  

    /* Verifies that push(), pop() and peak() work correctly
    * when there are multiple objects on the Stack. */
    static testMethod void verifyCorrectOrderTest() {
        // Instantiate a StringStack.
        StringStack stack = new StringStack();

        // Set up some test data.
        String bottomString = 'Bottom String';
        String middleString = 'Middle String';
        String topString = 'Top String';

        // Call the push() method with multiple objects
        stack.push(bottomString);
        stack.push(middleString);
        stack.push(topString);

        // Verify that the 'top' object is the object we expected
        String peakValue = stack.peak();
        System.assertEquals(topString, peakValue);

        // Verify that the order of the objects is as we expected
        String popValue = stack.pop();
        System.assertEquals(topString, popValue);
        popValue = stack.pop();
        System.assertEquals(middleString, popValue);
        popValue = stack.pop();
        System.assertEquals(bottomString, popValue);
        System.assert(stack.isEmpty());
    }  

The code passes this test too, so we are pretty confident that it handles the "normal" conditions pretty easily. Next, let’s test some of the more "unexpected" scenarios.

## Testing Unexpected Conditions
There are many scenarios that your code shouldn’t encounter. However, you can’t trust that clients of your code will always do the right thing, so you have to make sure that the code will still handle these unexpected scenarios appropriately. Let’s look at a few examples:

**Bad Input Values**  

One potentially unexpected condition that the code might encounter is an unexpected value, like null, being passed to the push() method. You have a few implementation options for handling this scenario. Your code could ignore the null value, it could insert a special placeholder value, or it could not allow null values to be pushed on to the Stack at all. In my implementation, I’m not going to allow null values to be pushed on to the Stack at all, and I’m going to throw an exception if a client my code attempts to do so. My unit tests should explicitly test this design decision, so I’m going to write it first:  

    static testMethod void nullValueNotAllowedExceptionTest() {
        StringStack oStack = new StringStack();

        try {
            stack.push(null);
        } catch (StringStack.NullValueNotAllowedException e){
            // Exit the test if the expected NullValueNotAllowedException is thrown.
            return;
        }

        // Fail the test if the expected NullValueNotAllowedException is not thrown.
        System.assert(false,
            'A NullValueNotAllowedException was expected, but was not thrown.');
    }  

At this point, the code is still going to fail this new unit test, so I need to change my push() implementation to make it pass this new unit test:  

    public void push(String s){
        if (s == null) { throw new NullValueNotAllowedException(); }
            stack.add(s);
        }

    public class NullValueNotAllowedException extends Exception {}  

Now the implementation passes all unit tests again.  

Bad input values are one of the most commonly encountered unexpected scenarios in development. A common scenario in Apex where you might encounter unexpected, or missing data is if a query doesn’t return a record, but your code expects one to be present:   

    Account oAccount = [SELECT Name FROM Account WHERE Id = :accountId];
    String sAccountName = oAccount.Name;  

If the record that you are querying for has gone missing due to a deletion, or some other action, you’re going to have a bug on your hands because a won't be pointing to a record, but will be null.

**Boundary Conditions**  

Boundary conditions are another common source of bugs. Let’s verify that our StringStack implementation handles the overflow and underflow boundary conditions. Please note that the following example was written before the list limit was removed but the concept of boundary conditions is still very much valid.  

The Apex documentation indicates that a List used to only contain 1,000 records. If a 1,001th object were to be added to our List-based Stack implementation, a System exception would be thrown. Instead of letting this generic exception be thrown, I’m going to design a test that expects a StringStack-specific exception be thrown when there is an overflow condition.  

    static testMethod void stackOverflowTest() {
        StringStack oStack = new StringStack();

        try {       
            for (Integer nIndex = 0; nIndex < StringStack.MAX_STACK_DEPTH + 1; nIndex++) {
                oStack.push('String ' + nIndex);
            }
        } catch (StringStack.StackOverflowException e) {
            // Exit the test if the expected StackOverflowException is thrown.
            return;
        }

        // Fail the test if the expected StackOverflowException is not thrown.
        System.assert(false,
            'A StackOverflowException was expected, but was not thrown.');      
        }  

Notice that the above unit test illustrates a common, and useful, pattern for verifying that a piece of code does in fact throw an exception as expected. The unit test’s try-catch block only catches a StackOverflowException. If this StackOverflowException is not thrown, this unit test would fail.
Now that I have a unit test that expects a StackOverflowException to be thrown, I need to modify the code to actually throw this exception:  

    public void push(String s) {
        if (s == null) { throw new NullValueNotAllowedException(); }
        if (this.isFull()) { throw new StackOverflowException(); }
        stack.add(s);
    }

    public static final Integer MAX_STACK_DEPTH = 1000;
    public Boolean isFull() { return MAX_STACK_DEPTH == stack.size(); }

    public class StackOverflowException extends Exception {}  

Now that I’ve handled the overflow boundary condition, I also need to test the underflow boundary condition where there is nothing in the stack to pop(). My current implementation of pop() will generate a System.ListException in this scenario. I want to hide the internal implementation of my StringStack class though, so I’m going to write a unit test that expects a StringStack-specific exception be thrown in this scenario too.  

    static testMethod void stackPopUnderflowTest() {
        StringStack oStack = new StringStack();

        try {
            oStack.pop();
        } catch (StringStack.StackUnderflowException e) {
            // Exit the test if the expected StackUnderflowException is thrown.
           return;
        }

        // Fail the test if the expected StackUnderflowException is not thrown.
        System.assert(false,
                'A StackUnderflowException was expected, but was not thrown.');
    }  

Here’s the modified version of the pop() method that passes this new unit test:  

    public String pop() {
        if (this.isEmpty()) { throw new StackUnderflowException(); }
        return stack.remove( lastItemIndex );
    }

    public class StackUnderflowException extends Exception {}  

Notice that this exception-expecting unit test follows the same pattern as the previous exception-expecting unit test. This is a very useful pattern.

**Regression Tests**  

Fixing bugs is usually frustrating. It’s even more frustrating when you have to fix the same bug multiple times. That’s why it’s a good idea to add tests to your test suite every time you find a bug in your code. For example, if I were to release my code in to production as it is, a StringStack client might discover that the peak() method doesn’t handle the underflow boundary condition in the same way as the pop() method. In order to verify that this bug doesn’t get reintroduced in a future release, I’m going to write one last unit test:  

    static testMethod void stackPeakUnderflowTest() {
        StringStack oStack = new StringStack();

        try {
            oStack.peak();
        } catch (StringStack.StackUnderflowException e) {
            // Exit the test if the expected StackUnderflowException is thrown.
            return;
        }
        // Fail the test if the expected StackUnderflowException is not thrown.
        System.assert(false,
            'A StackUnderflowException was expected, but was not thrown.');
    }  

And finally, I’ll make the following change so that my code passes this new unit test:  

    public String peak() {
        if (this.isEmpty()) { throw new StackUnderflowException(); }
        return stack.get( lastItemIndex );
    }

# Making use of Test.isRunningTest() method

There are some situations, when you will just not be able to test some code in a normal matter; e.g., you're using objects that cannot be inserted in tests, or doing some http requests. In such case, if you think there is no other option, consider using Test.isRunningTest(). This static method allows you to discover whether the code was run from test method. Therefore, for example you might:  
* return hard-coded String instead of calling http request and parsing the body
* return a fixed array of objects from a method   
It might be actually used as a basic introduction to mocks, which are very widespread in other languages.

# Force.com-specific Testing  
In addition to verifying that your code executes properly in normal scenarios, testing edge cases and preventing regressions, you may find that you need to test certain Force.com-specific aspects of your application as well. Things like Apex Callouts, SOSL queries, Governor Limits, etc. To learn more about these topics you’ll want to read these articles: 

|Document Name | 
|-------------|
| [Testing Apex Callouts](https://developer.salesforce.com/index.php?title=Virtual_Callout_Testing) |
| [Testing SOSL](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_testing_SOSL.htm) |
| [Verifying Large DataSets](https://developer.salesforce.com/page/Best_Practice:_Ensure_Test_Methods_Verify_Large_Datasets) |
| [Testing with RunAs](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_testing_tools_runas.htm) |


# Properties of Well-Written Unit Tests
Well-written unit tests are thorough, repeatable, and independent. Let’s examine each of these properties in turn.
## Thorough
The most important aspect of well-written unit tests is that your unit tests must be thorough. The Force.com platform requires 75% code coverage, but this is a minimum and should not be your end goal. You should only be satisfied with your unit tests when you’re confident that your unit tests thoroughly verify that your code works as we expect it to work. To do this, your tests must use the various System.assert() calls. Unit tests should exercise the expected as well as the unexpected conditions in your code. Special attention should be paid to areas of code that are particularly likely to break.

## Repeatable
Every one of your unit tests should be able to be run repeatedly and continue to produce the same results, regardless of the environment in which the tests are being run. When your unit tests can be run in a repeatable and consistent manner, you can trust that your unit tests will only detect and alert you to real bugs, and not environmental differences.  

One common mistake that might prevent you from writing repeatable unit tests is relying upon hard-coded information, like server URLs. Your unit tests should not rely on hard-coded server URLs because unit tests must be written in either a sandbox org or in a developer org. Sandbox orgs will always have different URLs than the production orgs will have, and developer orgs will usually have different URLs than the production org will have. If you hard-code the server URLs, the unit tests may fail when you attempt to move your code to production. Another common mistake that might prevent your unit tests from being repeatable is relying upon hard-coded record ids. Record ids are entirely org-specific, and can not be used outside of a given org. Instead of relying upon hard-coded record ids, unit tests should create their own data, as we described in the Set Up All Conditions for Testing section.

## Independent
Your unit tests should only test one aspect of your code at a time, so that it is easy to understand the purpose of each unit test. Properly written, and well-decomposed unit tests are an excellent source of documentation. This may mean that you will need to write multiple unit tests in order to fully exercise one method. I’ve shown you one example of this in the Testing Normal Conditions section.    

Also, keep in mind that each of your unit tests must be independent from your other unit tests. Unit tests do not alter the state of the Force.com database, and they are not guaranteed to run in a particular order, so you cannot rely upon one unit test to do the setup work for another unit test.