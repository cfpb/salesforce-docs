# Lightning Vs Visualforce

**Lightning Components**  
Lightning components are a rather new addition to the Salesforce suite of development tools. There is much confusion as to what are lightning components and when to use lightning versus Visualforce.

**What is Lightning?**  
Lightning is a framework that Salesforce has built to allow for a new look and feel to Salesforce, as well as the ability to create faster, more lightweight applications.

There are three 3 main parts to Lightning:  
  
1. **Lightning Experience** – The lightning experience is a completely new look and feel to Salesforce that takes into account modern user interface design practices that is commonly used throughout the web today. This is based on responsive design patterns such that the format of what you can see on the screen is based on screen size that you are viewing the content. Instead create a single web application, each page is made up of various components that can be easily changed out or rearranged.  

2. **Lightning Design System** – The design system is a new UI framework built off of angular that helps developers easily recreate the same look and feel of the Lightning Experience in their custom applications. This framework can be used in Visualforce, Lightning Components, or even in custom external based web applications. For more information on the design system visit http://www.lightningdesignsystem.com.

3. **Lightning Components** – Lightning components is a new development infrastructure that Salesforce has developed to quickly create high performing web applications based on a component model. A lightning component can be a web page or even a piece of a web page. Lightning components turns html, javascript, and CSS into an object-oriented language. Everything is a first class component in this framework. What this means is that instead of having to traverse the DOM you use getters and setters to access various elements of your application. For example the following are “objects” or “components” in the framework: “div”, “form”, “input”, “head”, “body”, “span”, javascript events such as “onclick”, etc.
The real power of lightning is that you can pass components between each other to build reusable pieces of an application. You can even pass a javascript event that fires from one component to another!

The Salesforce Lightning Experience is even built using Lightning Components. That means you can develop your own custom components using the same technology that Salesforce uses internally. Combining that with the Lightning Design System you can completely replicate any out of the box component in the Lightning Experience.

**Lightning Vs. Visualforce Comparison**
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
* Since everything is component based you can separate the development out to several different developers without risking the developers to walk over each other.
* Since even the styling is broken out you can have your UI designer work independently of your Salesforce developers on various components.
* Allows you to quickly change, add, or remove pieces of a page without having to think about refactoring the entire page.
* Ideal when you have the need to create a more component-based application made up of multiple “mini application”, rather than a single page application.
* Ideal for creating lightweight, responsive mobile applications.
 
**Visualforce Cons**
* Is very heavy, and much slower than the lightning framework because it uses a stateful infrastructure to keep the state for round-trips from the server.
* Requires a lot of work to rearrange pieces of the screen. Usually requires a complete rework of the HTML.
* Very difficult for multiple developers to work on the same page at the same time. Salesforce developers will typically have to wait for the UI designer to complete their work before adding functionality.
 
**Lightning Cons**
* Requires a little bit of a learning curve for seasoned Visualforce developers, as it requires strong javascript skills and is a completely different approach to development on the Salesforce platform.
* Doesn’t support creating applications with the current “Aloha” UI look and feel.  
      
When deciding to use lightning or Visualforce, carefully consider each of the pros and cons. Consider the following questions when making your decision?
 
1. Will the application be a standalone application, or can it be broken into multiple components?  
2. Does the application need to be responsive and run on multiple device formats?  
3. Will the application need to look and feel like the “Aloha” UI or the “Lightning Experience” UI?  
4. Do our developers have strong JavaScript and CSS skills? Will there be considerable ramp up time if we choose to use lightning?  
 

