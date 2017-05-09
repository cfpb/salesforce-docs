##Visualforce Page Best Practices
Just because you can, doesn’t mean you should! Before going down the customization route make sure you properly evaluate the pros and cons of creating custom pages. This is especially true when creating custom pages to override standard functionality.  When overriding standard functionality you lose the advantage gained of new features in future releases.
If you do go down the customization route you must make sure you optimize the Visualforce pages you create for better performance in order to have a positive user experience. 

* Avoid using the rendered=”false” if possible. Even though the components do not show up on the page, processing still needs to be done that will cause the page to render slower. If a large portion of the components of a Visualforce page have rendered=”false”, consider creating a separate page instead of using partial rendering.
* Use Salesforce remote objects to perform asynchronous execution of apex using JavaScript. This will allow the user to perform operations without having to wait for the server to respond. 
* Cache data in custom settings, custom metadata types, and the org cache to improve the performance of the page. Access to data in these mechanisms is much faster than executing SOQL queries to retrieve the same data. Additionally they do not count against your max queries limit.
* Avoid the use of iframes whenever possible as these will slow the loading of the page. If you need to create a window into Salesforce from an external system consider using Canvas instead, since it is much more tightly integrated into Salesforce and takes care of the authentication for you. 
* Use minified JavaScript and CSS file resources
* Avoid use of references to external scripts or resources. Instead download them as static resources and reference the static resources. Static resources are cached and provide for better performance. Never reference a Salesforce unsupported JavaScript or CSS library directly as these could change at any time. Any API that is not versioned is considered an unsupported API.
* Use only web optimized images and image maps to reduce the need to load multiple images.
* Use paging techniques when working with large datasets on a page. Avoid displaying more than 20 results per page. Use the SOQL offset or the standardSetController to control paging.
* Make sure all your SOQL queries are optimized using the query optimizer located in the developer console. 
* Use lazy loading techniques to load parts of the page first, giving users access to some of the functionality while other parts of the page are still loading. For example you can load the page first and then the data for the page once the page has finished loading. 
* Instead of polling to retrieve changes in data or refreshing the page consider using the streaming api to receive push notifications when data has changed.

For more Visualforce best practices see
http://www.salesforce.com/docs/en/cce/salesforce_visualforce_best_practices/salesforce_visualforce_best_practices.pdf  

## Lightning Components Vs. Visualforce?
Lightning components are a rather new addition to the Salesforce suite of development tools. There is much confusion as to what are lightning components and when to use lightning versus Visualforce.

### What is Lightning?
Lightning is a framework that Salesforce has built to allow for a new look and feel to Salesforce, as well as the ability to create faster, more lightweight applications.  

There are three 3 main parts to lightning:

1.  **Lightning Experience** – The lightning experience is a completely new look and feel to Salesforce that takes into account modern user interface design practices that are commonly used throughout the web today. This is based on responsive design patterns such that the format of what you can see on the screen is based on the screen size on which you are viewing the content. Each page is made up of various components that can be easily changed out or rearranged.
1.  **Lightning Design System** – The design system is a new UI framework built off of angular that helps developers easily recreate the same look and feel of the Lightning Experience in their custom applications. This framework can be used in Visualforce, Lightning Components, or even in custom external based web applications. For more information on the design system visit http://www.lightningdesignsystem.com 
1.  **Lightning Components** – Lightning components is a new development infrastructure that Salesforce has developed to quickly create high performing web applications based on a component model. A lightning component can be a web page or even a piece of a web page. Lightning components turn HTML, JavaScript, and CSS into an object-oriented language. Everything is a first class component in this framework. What this means is that instead of having to traverse the DOM you use getters and setters to access various elements of your application. For example the following are “objects” or “components” in the framework: “div”, “form”, “input”, “head”, “body”, “span”, JavaScript events such as “onclick”, etc. 
The real power of lightning is that you can pass components between each other to build reusable pieces of an application. You can even pass a JavaScript event that fires from one component to another! 

The Salesforce Lightning Experience is even built using Lightning Components. That means you can develop your own custom components using the same technology that Salesforce uses internally. Combining that with the Lightning Design System you can completely replicate any out of the box component in the Lightning Experience.

### Lightning vs. Visualforce?
The question many people ask is “Will Visualforce be going away?” Think of lightning as just yet another tool in your Salesforce Tool belt. Both have their uses based on what you are trying to do.

**Visualforce Pros**  

* Can be made to look like the “Aloha” look and feel of Salesforce without much trouble.
* Can use the Lightning Design framework to make the look feel of that of the Lightning Experience.
* Allows for quick development of pages that interact directly with the Salesforce platform keeping everything on the server-side. 
* Is a tried and true development platform in use today by thousands of customers.
* Is better for single page applications that are not component based.  

**Lightning Pros**   

* Since most everything runs client-side, and all server-side calls to Salesforce are performed asynchronously, it is very fast.
* Allows you to easily make applications with the same look and feel of the lightning experience. 
* Since everything is component based you can separate the development out to several different developers without risking the developers stepping on each other.
* Since even the styling is broken out you can have your UI designer work independently of your Salesforce developers on various components.
* Allows you to quickly change, add, or remove pieces of a page without having to think about refactoring the entire page. 
* Ideal when you have the need to create a more component-based application made up of multiple “mini applications”, rather than a single page application.
* Ideal for creating lightweight, responsive mobile applications.

**Visualforce Cons**  

* Is very heavy, and much slower than the lightning framework because it uses a stateful infrastructure to keep the state for round-trips from the server.
* Requires a lot of work to rearrange pieces of the screen. Usually requires a complete rework of the HTML. 
* Very difficult for multiple developers to work on the same page at the same time. Salesforce developers will typically have to wait for the UI designer to complete their work before adding functionality.  

**Lightning Cons**   

* Requires a little bit of a learning curve for seasoned Visualforce developers, as it requires strong JavaScript skills and is a completely different approach to development on the Salesforce platform.
* Doesn’t support creating applications with the current “Aloha” UI look and feel.  
       
When deciding to use lightning or Visualforce, carefully consider each of the pros and and cons. Consider the following questions when making your decision?  

1.  Will the application be a standalone application, or can it be broken into multiple components?
1.  Does the application need to be responsive and run on multiple device formats?
1.  Will the application need to look and feel like the “Aloha” UI or the “Lightning Experience” UI?
1.  Do our developers have strong JavaScript and CSS skills? Will there be considerable ramp up time if we choose to use lightning?
