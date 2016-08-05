### Logging & Troubleshooting

####Custom Logging

The Salesforce debug log is good way to debug your code when you have a limited amount of logs that you want to review over a short period of time. When the Salesforce debug log breaks down is when you want to review logs for issues that occurred the previous day or before. Additionally if you wish to receive notifications of what an issue occurred this is also outside the scope of functionality of the Salesforce debug log.
It is for use cases like these that you want to use a custom logging framework in addition to the debug log to adequately troubleshoot your code. 

The logging framework should write log entries to a custom object. From there you can create workflow rules to send email notifications, create tasks, or even create a ticket in an external system when an error event occurs. 
Although this is a very helpful approach to logging and error notification in Salesforce you must take care when using it. Unlike using the debug log you must write records to the logging object for this approach, which takes up DML calls that may be needed for your application. Keep in mind your DML limits at all times when using this approach. Also keep in mind that every record created will also take up storage in your org so you will need to develop an approach for deleting log records that are no longer needed.

Make sure that when using this custom logging approach, you write a mechanism that will allow you to set the logging level and turn on/off logging by user and/or profile using custom settings by application. This will help you to avoid creating thousands of logging records unnecessarily taking up storage limits.