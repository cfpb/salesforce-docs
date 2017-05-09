###Effective Testing and Debugging

- [Writing good tests](/_pages/Writing-good-tests.md)
- [Unit testing](/_pages/Unit-testing.md)
- Browser Testing (SauceLabs) - More to come
- Security Testing (Checkmarx) - More to come
- 508/WCAG - More to come
- [Top 10 Best Practices](/_pages/Top-10-Best-Practices.md)

####Testing

(NOTE:  http://www.salesforce.com/us/developer/docs/apexcode/Content/apex_testing_best_practices.htm)

The following principles apply to unit testing Apex code

1. Cover as many lines of code as possible

* Salesforce requires that you have at least 75% of your Apex scripts covered by unit tests to deploy your scripts to production environments. In addition, all triggers should have some test coverage.

* Salesforce recommends that you have 100% of your scripts covered by unit tests, where possible.

* In order for a project team to deploy to production or pre-production instances at CFPB, it is required that ALL classes and triggers have at least 90% of code covered by unit tests.

2. In the case of conditional logic (including ternary operators), execute each branch of code logic.

3. Make calls to methods using both valid and invalid inputs.

4. Complete successfully without throwing any exceptions, unless those errors are expected and caught in a try…catch block.

5. Always handle all exceptions that are caught, instead of merely catching the exceptions.

6. Use ```System.assert``` methods to prove that code behaves as expected. 

7. Use the ```runAs``` method to test your application in different user contexts.

8. Use the isTest annotation. Classes defined with the isTest annotation do not count against your organization limit of 1 MB for all Apex scripts.

9. Exercise bulk trigger functionality—use at least 201 records in your tests.

10. Write comments stating not only what is supposed to be tested, but the assumptions the tester made about the data, the expected outcome, and so on.

11. Debug statements and Comments are not included in the Code coverage.

12. User records are not covered by test methods.

13. Web service calls should be tested using a Mock class.

14. Large amounts of test data should be loaded by using the Test.loadData.

15. Never use @seeAllData.  Accessing data specific to a sandbox can result in deployments failing

16. Do not write test classes merely to get code coverage. It is much more effective to write the test code to cover specific business cases. You will find that if you use this method you will cover much more code, much faster than just writing test code to get coverage only. Additionally this will help ensure that you are meeting the business requirements in addition to testing for bugs. 


