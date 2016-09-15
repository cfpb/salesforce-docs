
#Summary: Top 10 Best Practices (in no order)  

(Source: http://blog.force365.com/2014/09/19/apex-unit-test-best-practice/)  

**Test Driven Development**  

Follow Test Driven Development practice wherever possible. There is no excuse for writing unit tests after the functional code, such an approach is indicative of a flawed development process or lax standards. It’s never a good idea to estimate or deliver functional code without unit tests – the client won’t appreciate an unexpected phase of work at the point of deployment, not to mention the pressure this approach puts on system testing.

**Code Quality**  

Ensure unit tests are written to cover as many logical test cases as possible, code coverage is a welcome by-product but should always be a secondary concern. Developers who view unit tests as a necessary evil, or worse, need to be educated in the value of unit tests (code quality, regression testing, early identification of logical errors etc. etc.).

**Test Code Structure**  

For some time now I’ve adopted a Test Suite, Test Helper pattern. A suite class groups tests related to a functional area. A test helper class creates test data for a primary object such as Account (i.e. ```AccountTestHelper.cls```), secondary objects such as price book entry would be created within the product test helper class. The suite concept provides a logical and predictable structure, the helper concept emphasizes that test data creation should be centralized.

**Test Code Structure (continue)**  

Put bulk tests in a separate class e.g. AccountTriggerBulkTestSuite.cls (in addition to AccountTriggerTestSuite.cls). Bulk tests can take a long time to complete – this can be really frustrating when debugging test failures – particularly in production.

**Test Code Structure (over and over)**  

Ensure test classes contain a limited number of test methods. I tend to limit this to 10. As with point 4, this relates to test execution time, individual methods can’t be selectively executed – the smallest unit of execution is the class.

**SeeAllData**   

Always use SeeAllData=true by exception and at the test method level only. Legacy test code related to pricebooks that historically required this can now be refactored to use Test.getStandardPricebookId(). Also, set the [Independent Auto-Number Sequence] flag to avoid gaps in auto number sequences through the creation of transient test data.

**Test Case Types**  

As the Apex Language reference proposes, write unit tests for the following test case types.
* _Positive Behavior_ – logical tests that ensure the code behaves as expected and provides successful positive outcomes
* _Negative Behavior_ – logical tests for code behavior where parameters are missing, or records do not adhere to defined criteria – does the code protect the integrity of unaffected records – does the runtime exception handling function as expected
* _Bulk_– trigger related tests primarily – how the code behaves with a batch of 200 records – mix the batch composition to stress the code against governor limits
* _Restricted User_ – test relevant combinations of user role and profile – this test case type is prone to failure through sharing model adjustments – triggers should delegate processing to handler classes that have the “with sharing” modifier

**Debugging**   

Always use the syntax below for debug statements within code (test and non-test code). An efficient practice is to add sensible outputs whilst writing the code. This approach avoids a code update or re-deployment to add debug statements during error diagnostics. Note – in such cases Checkpoints could be a better approach anyway – particularly in production. The use of the ERROR logging level enables a restrictive log filter to be applied such a clear debug log is produced and max log size truncation is avoided – note, log filters can also have a positive impact on transaction execution time.
System.debug(LoggingLevel.ERROR, 'my message');

**Commenting**  

Always comment test methods verbosely to ensure the test case intent is clear and that the test code can be mapped to the related non-test code. Test classes should be fully self documenting and be viewed as the primary enabler for the future maintenance of the non-test code.

**Maintenance**  

Test code is highly dependent on the environment state. Any configuration change can require test code to be updated; this could be a new mandatory custom field or a sharing model adjustment. In many cases the resultant unit test failure state is not encountered until the next deployment to production, which can’t proceed until the tests are fixed. This scenario will be familiar to many people. The mitigation requires the local administrator to understand the risk, frequently run the full set of unit tests and to manage the test code update cycle proactively.
