### Integrating Salesforce with External Systems

There are many different APIs that Salesforce has to offer within its toolkit. Just as with using Lightning and Visualforce there are many considerations you must make when choosing a specific API to use. 

#### Inbound Requests

Salesforce offers two primary types of APIs based on industry standards. The first is a SOAP based API, and the second is a REST based API. The REST API is very lightweight, has no WSDL definition file that is needed to install, and performs very well. The SOAP API is much heavier and slower than the REST API, but offers many more features and can handle many more records than the REST API.

**SOAP API**

The SOAP API was the very first API that Salesforce offered and as such is the most complete API available today. There are two flavors of this API available based on the type of user you are, and application that you are developing. The first is the enterprise API and the second is the partner API. Don’t be fooled by the names of the APIs. Just because you are not a partner, doesn’t mean that you can’t use the partner API. 

The SOAP API supports database operations such as query, insert, update, delete, as well as supports many other meta-data related requests related to users or understanding the Salesforce data model. For a complete reference to the functionality of the SOAP API you may view the developers guide at:

[http://developer.salesforce.com/docs/atlas.en-us.api.meta/api/](http://developer.salesforce.com/docs/atlas.en-us.api.meta/api/) 

- **Enterprise API**

    The only difference between the enterprise and partner API is that the enterprise API is strongly typed to a specific Salesforce environment. The API exposes every Salesforce object standard and custom as data structures within the API. This makes it much quicker for one to develop, as there is no need to spend time creating data structures for each object you wish to work with within the org. 

    The downside of the SOAP API is that every time you add a new field or object, or delete a field or object, you must re-import the WSDL that represents the new data structure. Deleting objects and fields is especially dangerous, as that will break your current integrations if you do not update the WSDL.

- **Partner API**

    The partner API on the other hand is not strongly typed for any one particular environment. It was originally designed for Salesforce partners to use where the data model could be different for each customer using their integration. Many customers also use this API because it reduces the risk of something breaking because a field was deleted, and in the long term reduces the overall maintenance cost since a new WSDL does not need to be imported every time the data model changes and you wish to access the new fields and/or objects in the data structure. 

    The downside of the Partner API is that there is a substantial amount of additional coding and work required for the initial implementation because you must generate your own XML within your code to bind to each object and field. Once the initial setup is complete, the ongoing maintenance is the same, if not less than that of the Enterprise API. 

**REST API**

The REST API is an API that has similar functionality to that of the SOAP API, but is based on REST standards. That means there is no WSDL to download and maintain, and all requests are HTTP based using common Verbs such as Post, Get, Put, Patch, and Delete. The rest API takes requests and returns responses in either XML or JSON.

The REST API is a good API to use when you need to make lightweight operations with a quick response, such as on mobile devices. 

Just like the SOAP API, the REST API supports database operations such as query, insert, update, and delete except that since the REST API is a newer API it is not as complete as the SOAP API. 

Aside from the actual functionality differences between the two APIs it is good to understand in general the differences between REST and SOAP. For more information on REST and SOAP visit the following sites below.

[http://en.wikipedia.org/wiki/SOAP](http://en.wikipedia.org/wiki/SOAP)

[http://en.wikipedia.org/wiki/Representational_state_transfer](http://en.wikipedia.org/wiki/Representational_state_transfer) 

**BULK API**

The REST and SOAP APIs are great tools for general transactional real-time applications, but tend to fall apart when you need to work with large volumes of data. When working with data volumes of above 50,000 records you should look to using the BULK API.

The BULK API is a REST based asynchronous API designed to handle inserting, updating, and deleting large amounts of data. Generally speaking the BULK API can act on up to 50 million records in a rolling 24-hour period according to the official documentation. If you need to work with a larger amount of data than 50 million records per day, you can contact Salesforce support to have your limits increased with proper justification. 

For more information on the developing with the BULK API and limits of the BULK API visit the following sites below.

[https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/asynch_api_concepts_limits.htm](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/asynch_api_concepts_limits.htm) 

[https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/) 

**BEWARE OF YOUR DAILY API LIMITS**

Every time you make a call to the SOAP or REST API you use an API call that is allotted to your organization on a rolling 24 hour period. If you use up all of your API calls on at 24 hour period then you will be no longer allowed to make calls to the SOAP or REST API until your rolling 24 hour usage has dropped below the limit. 

This is one of the main reasons why it is recommended that if you need to process more than 50,000 records, you use the BULK API, as the BULK API does not take up your daily API limits. For example, if you need to process 1 million records and use the SOAP API processing 200 records at a time, you will use up 5,000 of your API calls. Not only does this take a long time to process you are will endanger your organization of breaching this limit. This is especially true as you add more services to your organization that are using the SOAP or REST APIs. 

**Apex Web Services**

If the SOAP API or the REST API won’t easily accomplish your business requirements, Salesforce allows you to create your own custom SOAP or REST API that you can expose for consumption by external systems. This API allows you to implement you own custom API methods with more complex logic than is available with the out of the box SOAP and REST APIs. 

Think of Apex Web Services as the "Custom API" where the SOAP and REST APIs are the “Out of the Box” APIs. The primary function for the out of the box APIs are for data movement and manipulation. Where the Custom API is more for working with smaller numbers of records where you need more complex logic application them. 

**BEWARE OF LONG RUNNING PROCESSES**

When a custom API call that takes longer than 5 seconds to complete gets put into what is called a "long running process queue". If you have too many concurrent methods that are in this long running process queue, Salesforce will block all future calls to your custom APIs, long and short running, until the long running process queue drops below the max allowed value of 10 concurrent long running process. Any additional calls to the custom API while the long running process queue is full will receive the error “Concurrent Requests Limit Exceeded”. This limit is in place to protect customers against denial of service attacks. 

It is imperative that you take care when designing custom apex services that they do not take longer than 5 seconds to complete. This is why it is recommended that you only utilize these service to operate on smaller numbers of records to avoid long running processes.

If you find that your methods are taking too long to complete you may want to think about breaking them up into multiple transactions. For example you may want to first call the SOAP API to retrieve the records and then send a smaller number of records at a time to the custom API. 

**Outbound Requests**

In addition to exposing APIs to external systems, Salesforce also has a few mechanisms for making calls out to external systems. 

1. **HTTP call-outs using Apex**

    If you need to make a call out to an external web service, using apex you can use the HTTPRequest and HTTPResponse objects to make and receive HTTP calls to external systems. This is ideal for communicating with simple services that require simple HTTP messages to be passed like a REST API. 

2. **Call-Outs to SOAP APIs**

    Salesforce also supports making more complex call-outs to SOAP APIs as well. In order to communicate with an external SOAP service you will need to import the WSDL under Develop->Classes. Once the WSDL has been imported a facade class is generated for each of the methods in the SOAP service. You then can use apex to execute those methods to make a call-out to the SOAP service. 

    Occasionally the WSDL will not import because the Salesforce WSDL parser does not understand the WSDL. In this case you will manually need to recreate the facade by hand. This procedure is out of scope of this document. 

3. **Outbound Messaging**

    Using the WSDL importer and the HttpRequest or HTTPResponse apex objects are fine to use when you need to make point-to-point calls. The only drawback is if you are unable to connect to the external service and/or failures occur there is not retry mechanism. 

    When you need more complex handling with retry mechanisms built-in in, you may want to consider using Salesforce Outbound Messaging services. Outbound Messaging is part of the Salesforce workflow and approvals system. An outbound message can be automatically executed when a record has been inserted or updated. The real power behind Outbound Messaging is that if an error occurs while communicating with the external service, the outbound message will retry later. The Outbound Messaging system will retry to send the message for up to 24 hours. 

    There are a couple drawbacks to using Outbound Messaging. Multiple messages can be sent at the same time if multiple updates occur to a specific record. Don’t use outbound messaging if sequence of events is important, such as with logging. 

    Additionally in order to use outbound messaging you must export a WSDL and implement the service on the other end. Many times the time required to implement this service is less time that it would take to implement the retry mechanisms already built into the Outbound Messaging capability.

    For more information on how Outbound Messaging works visit the page below.

    [https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_om_outboundmessaging_understanding.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_om_outboundmessaging_understanding.htm) 
