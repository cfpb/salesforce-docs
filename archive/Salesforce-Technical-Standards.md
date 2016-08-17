
## CFPB Salesforce Technical Standards &  Guidelines

**May 10, 2016**

**Draft v1.3**

**Prepared By:** 

**Matt Meyers, Program Architect, Salesforce & the CFPB Platforms Team**

#### Table of Contents


[&](#heading=h.30j0zll)

[Guidelines](#heading=h.1fob9te)

[Introduction and Scope](#heading=h.3znysh7)

[Document Control](#heading=h.tyjcwt)

[Change Control](#heading=h.3dy6vkm)


[To Do](#heading=h.4d34og8)

[Related Documents](#heading=h.2s8eyo1)

[Source Code Management](#heading=h.17dp8vu)

[Git branching strategy and workflow](#heading=h.3rdcrjn)

[Naming Conventions](#heading=h.26in1rg)

[Custom Objects](#heading=h.lnxbz9)

[Custom Fields](#heading=h.35nkun2)

[Validation Rules](#heading=h.1ksv4uv)

[Workflow Rules](#heading=h.44sinio)

[Field Updates](#heading=h.z337ya)

[Email Alerts](#heading=h.3j2qqm3)

[Approval Processes](#heading=h.1y810tw)

[Approval Process Steps](#heading=h.4i7ojhp)

[Visualforce Pages](#heading=h.2xcytpi)

[Apex Classes](#heading=h.1ci93xb)

[Apex Batch, Schedulable, and Queueable Classes](#heading=h.3whwml4)

[Apex Triggers](#heading=h.2bn6wsx)

[Apex Test Classes](#heading=h.qsh70q)

[Apex Methods](#heading=h.3as4poj)

[Apex Variables](#heading=h.1pxezwc)

[Apex Constants](#heading=h.49x2ik5)

[Apex Type Names](#heading=h.2p2csry)

[Best Practices](#heading=h.147n2zr)

[Constants and Literals](#heading=h.3o7alnk)

[Code indentation](#heading=h.ihv636)

[Effective Testing](#heading=h.32hioqz)

[Bulkify All Code](#heading=h.1hmsyys)

[Never use SOQL queries or DML statements inside FOR loops](#heading=h.41mghml)

[Querying Large Data Sets](#heading=h.2grqrue)

[Triggers](#heading=h.vx1227)

[Muting Triggers](#heading=h.3fwokq0)

[Trigger Maintainability](#heading=h.1v1yuxt)

[Never Hardcode Ids](#heading=h.4f1mdlm)

[Custom Settings](#heading=h.2u6wntf)

[Enforcing Sharing Rules in Controllers](#heading=h.19c6y18)

[Governor Limits](#heading=h.3tbugp1)

[SOQL Query Optimization](#heading=h.28h4qwu)

[Visualforce Page Best Practices](#heading=h.nmf14n)

[Lightning Components Vs. Visualforce?](#heading=h.37m2jsg)

[Integrating Salesforce with External Systems](#heading=h.1mrcu09)

[Inbound Requests](#heading=h.46r0co2)

[Commenting](#heading=h.2lwamvv)

[Overview](#heading=h.111kx3o)

[Class Header](#heading=h.3l18frh)

[Function Header](#heading=h.206ipza)

[Subroutine header](#heading=h.4k668n3)

[Variables](#heading=h.2zbgiuw)

[Logging & Debugging](#heading=h.1egqt2p)

[Debugging](#heading=h.3ygebqi)

[Custom Logging](#heading=h.2dlolyb)

[Exception Handling](#heading=h.sqyw64)

[Abstract](#heading=h.3cqmetx)

[Catching Exceptions](#heading=h.1rvwp1q)

[Custom Exceptions](#heading=h.4bvk7pj)

[How to Write Good Unit Tests](#heading=h.2r0uhxc)

[Abstract](#heading=h.1664s55)

[Unit Test Introduction](#heading=h.3q5sasy)

[The Value of Unit Tests](#heading=h.25b2l0r)

[Unit Test Structure](#heading=h.kgcv8k)

[Set Up All Conditions for Testing](#heading=h.34g0dwd)

[Call the method (or Trigger) being tested](#heading=h.1jlao46)

[Verify the results are correct](#heading=h.43ky6rz)

[Clean up (is Easy!)](#heading=h.2iq8gzs)

[Where to put tests?](#heading=h.xvir7l)

[Putting it all together](#heading=h.3hv69ve)

[What to Test](#heading=h.1x0gk37)

[Stack Interface](#heading=h.4h042r0)

[Testing Normal Conditions](#heading=h.2w5ecyt)

[Testing Unexpected Conditions](#heading=h.1baon6m)

[Bad Input Values](#heading=h.3vac5uf)

[Boundary Conditions](#heading=h.2afmg28)

[Regression Tests](#heading=h.pkwqa1)

[Making use of Test.isRunningTest() method](#heading=h.39kk8xu)

[Force.com-specific Testing](#heading=h.1opuj5n)

[Properties of Well-Written Unit Tests](#heading=h.48pi1tg)

[Thorough](#heading=h.2nusc19)

[Repeatable](#heading=h.1302m92)

[Independent](#heading=h.3mzq4wv)

[Summary: Top 10 Best Practices (in no order)](#heading=h.2250f4o)

[Test Driven Development](#heading=h.haapch)

[Code Quality](#heading=h.319y80a)

[Test Code Structure](#heading=h.1gf8i83)

[Test Code Structure (continue)](#heading=h.40ew0vw)

[Test Code Structure (over and over)](#heading=h.2fk6b3p)

[SeeAllData](#heading=h.upglbi)

[Test Case Types](#heading=h.3ep43zb)

[Debugging](#heading=h.1tuee74)

[Commenting](#heading=h.4du1wux)

[Maintenance](#heading=h.2szc72q)

# Introduction and Scope

These standards will provide:

* A standard guideline for Apex and Visualforce development 

* Hints and tips and best practices for development.

* Easier maintenance/enhancement through consistent standards.

* Consistency with Java programming language naming conventions

The standards should be applied to all new development work and should be introduced to existing projects as far as is practically possible.

# Document Control

    1. Change Control

<table>
  <tr>
    <td>Date</td>
    <td>Version</td>
    <td>Revised By</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>01/12/2016</td>
    <td>0.1</td>
    <td>Matt Meyers</td>
    <td>Initial template draft</td>
  </tr>
  <tr>
    <td>2/17/2016</td>
    <td>1.0</td>
    <td>Matt Meyers</td>
    <td>Draft Complete</td>
  </tr>
  <tr>
    <td>3/20/2016</td>
    <td>1.1</td>
    <td>Bill Shelton</td>
    <td>Branding, Formatting, and Detailed Review (see comments)</td>
  </tr>
  <tr>
    <td>04/29/2016</td>
    <td>1.2</td>
    <td>Bill Shelton</td>
    <td> Add source code management section,edit commenting section</td>
  </tr>
</table>


    2. To Do

<table>
  <tr>
    <td>Name</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>Re-order</td>
    <td>Naming should be later (not the first thing seen)</td>
  </tr>
  <tr>
    <td>Source Control</td>
    <td>Add section on how source code should be managed</td>
  </tr>
  <tr>
    <td>Build HTML version</td>
    <td>Google doc is hard to use.  Let’s build an HTML mini-site</td>
  </tr>
  <tr>
    <td>Guidance</td>
    <td>Add guidance on when to use custom vs. configuration</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
  </tr>
</table>


    3. Related Documents

<table>
  <tr>
    <td>Document Name</td>
    <td>Location</td>
  </tr>
  <tr>
    <td>Java Code Conventions</td>
    <td>http://www.oracle.com/technetwork/java/codeconventions-150003.pdf</td>
  </tr>
  <tr>
    <td>Understanding Execution Governor Limits </td>
    <td>https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_gov_limits.htm </td>
  </tr>
  <tr>
    <td>Salesforce Cheat Sheets</td>
    <td>https://developer.salesforce.com/page/Cheat_Sheets </td>
  </tr>
  <tr>
    <td>Working With Salesforce Large Data Volumes</td>
    <td>http://www.salesforce.com/us/developer/docs/ldv/salesforce_large_data_volumes_bp.pdf
</td>
  </tr>
  <tr>
    <td>Testing Best Practices</td>
    <td>https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_testing_best_practices.htm </td>
  </tr>
  <tr>
    <td>Testing Example</td>
    <td>https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_testing_example.htm </td>
  </tr>
</table>


# Source Code Management

Source code for all [LIST SALESFORCE ASSET TYPES] will be stored in GitHub. We have both GitHub.com and GitHub Enterprise. The preference is to keep it in GitHub.com and practice open by default. [CITE OPEN SOURCE POLICY]

## Git branching strategy and workflow

...

# Naming Conventions

Naming conventions make the application easier to read and maintain.  The naming standards documented here cover customization and configuration areas of salesforce. Regardless of the context in which names are used, Names should be descriptive, concrete, and specific rather than general.  Having a generalized name such as *ProductLine* can have different semantics depending upon the context.  It’s better to use something the business identifies with and that will not create a potential conflict with other applications; e.g.,  *ReverseMortgage*.

    4. Custom Objects

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Custom object names should be unique, beginning with an uppercase letter. Whole words should be used and use of acronyms and abbreviations should be limited.
The object name should be singular (e.g. Review vs. Reviews, or OrderItem vs. Order Items) and should not include any underscores "_".

The object label when at all possible should be similar to that of the object name since giving the label a different name than the object will make the object hard to find in some place within Salesforce.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.

Added an underscore is acceptable if you are prefixing the object name to denote it is part of an application. For example: OrderApplication_Order and OrderApplication_OrderItem. Notice that OrderItem does not have any underscores.</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of custom object naming that should not be used

Object Name
Reason
CustAsset
Abbreviations have made this object name hard to understand
Orders
Object names should always be singular.
Order_Item
Object names should not have spaces. 

The following are examples of the naming convention that will be used

Object Name
Reason
CustomerAsset
Removing ambiguity from the name will improve readability and maintainability
Order
Making object names singular will ensure a standard naming convention across all objects.
OrderItem
Removing all underscores will help keep a standard naming convention as many times there are words that some may separate into two words and other may not. For example: Zipcode vs. Zip Code.
 </td>
  </tr>
</table>


    5. Custom Fields

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Custom object names should be unique, beginning with an uppercase letter. Whole words should be used and use of acronyms and abbreviations should be limited. 

Similar to custom object naming, custom fields should not contain any underscores "_".

When creating custom fields always complete the “Description” field unless the field name would be completely obvious to someone not familiar to the application as to what is the purpose of the field. </td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of custom field naming that should not be used

Custom Field Name
Description
Reason
C

Ambiguous names will cause confusion. Description was not completed.
Zip_Code

Field names should not have underscores.

The following are examples of the naming convention that will be used

Custom Field Name
Description
Reason
CountryCode

A succinct description of the object using whole words. Description is not required since the name is a commonly understood term.
ZipCode

Removing all underscores will help keep a standard naming convention as many times there are words that some may separate into two words and other may not. Description is not required since the name is a commonly understood term.
CompletionDate
Date that the order process was completed. Should only be set once payment is received and order was fulfilled.
Even though the name seems to make sense, there are business rules that need to be explained, and as such, a longer description was needed.
 </td>
  </tr>
</table>


    6. Validation Rules

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Validation rule names should be unique, beginning with an uppercase letter. Whole words should be used and use of acronyms and abbreviations should be limited.
<Field> <Rule> <Optional Dependency>
e.g. Postal Code Required (Suburb)
The above example shows that Postal Code is required dependent on values in the Suburb field. The exact rule definition is in the detail but keeing this format helps keeps the naming as intuitive as possible without being too restrictive.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.
As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read.</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of validation rule naming that should not be used

Validation Rule Name
Reason
Validate Address
Superfluous use of the word validate and does not allow future additional validation rules to easily distinguish what the rule is checking

The following are examples of the naming convention that will be used

Validation Rule Name
Reason
Street Address < 60 chars
Field and rule clearly identifiable
Post Code Not Blank
Field and rule clearly identifiable
Occupation Required
Field and rule clearly identifiable
Postal Code Required (Suburb)
Field, rule and dependency clearly identifiable
 </td>
  </tr>
</table>


    7. Workflow Rules

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Workflow rule names will follow the following convention:
Attribute
Naming Convention
Workflow Rule Name
<Event that fired the rule>
Note that this is not the action or actions being performed but the original event that fired the workflow rule. This allows the workflow actions to change over time.
Including the salesforce object in the rule name is unnecessary as there is a standard field in the list view that can show this and filter on it.
Whole words should be used and use of acronyms and abbreviations should be limited.
Description
A full description of the rule and what actions it performs
</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of workflow rule naming that should not be used

Attribute
Example
Reason
Workflow Rule Name
Contact – Send Email and Update Inactive Flag
Name is too long and describes the actions performed as part of the rule that may change over time making the name potentially confusing in the future.
Description
Sends an email
Not enough detail to be immediately clear what the workflow rule actions. Who is the email to? What about the field update?

The following are examples of the naming convention that will be used

Attribute
Example
Reason
Workflow Rule Name
Date of Death Changed
Describes the event that will fire the rule in a succinct way
Description
Sends an email to the Deceased Customer public group and updates the inactive flag of the contact for batch processing
Provides a clear and brief description of the intention of the actions performed. The description can be more easily updated and migrated as changes are made over time
</td>
  </tr>
</table>


    8. Field Updates

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Field update names will follow the following convention:
Attribute
Naming Convention
Field Update Name
Set <Name of Field> - <Value>
Whole words should be used and use of acronyms and abbreviations should be limited.
By using this convention the field update can be reused across workflow rules and approval processes and it is clear to the reviewer what action, field and value will be used.
Description
A full description of the field update including if other processes are dependent on the value

</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of field update naming that should not be used

Attribute
Example
Reason
Field Update Name
Customer Date of Death
This describes the rule that fires the field update but does not tell me which field is updated and to what value
Description
Updates the customer inactive flag
Doesn’t tell the reviewer at first glance what value is used and if this flag is used in other processes

The following are examples of the naming convention that will be used

Attribute
Example
Reason
Field Update Name
Set Customer Inactive Flag – False
Describes the field being updated and what value will be used when updating the field
Description
Updates the inactive flag on the customer record which will be used by batch apex for processing
Briefly describes interdependencies that may rely on this action being performed
</td>
  </tr>
</table>


    9. Email Alerts

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Email alert names will follow the following convention:
Attribute
Naming Convention
Email Alert Description
Email <Description of Recipient> - <Email Template Used>
Whole words should be used and use of acronyms and abbreviations should be limited.
By using this convention the email alert can be reused across workflow rules and approval processes and it is clear to the reviewer who the email will be sent to.

</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of email alert naming that should not be used

Attribute
Example
Reason
Email Alert Description
Inform team of change
Mixed case not used and it is unclear where the email will be sent

The following are examples of the naming convention that will be used

Attribute
Example
Reason
Email Alert Description
Email Deceased Customer Team – New Deceased Customer
Describes who is emailed and which template is used
</td>
  </tr>
</table>


    10. Approval Processes

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Approval process names will follow the following convention:
Attribute
Naming Convention
Process Name
<Event that fired the approval>
Note that this is not the action or actions being performed but the original event that will trigger the entry criteria. This allows the approval actions to change over time.
Including the salesforce object in the rule name is unnecessary as there is a standard field in the list view that can show this and filter on it.
Whole words should be used and use of acronyms and abbreviations should be limited.
Description
A full description of the rule and what actions it performs
 </td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of approval process naming that should not be used

Approval Process Name
Reason
Comp
Abbreviations can cause confusion. Whole words should be used.
Send Email On Reject
Actions performed in the approval process should not be used in the parent process name

The following are examples of the naming convention that will be used

Approval Process Name
Reason
Conflict Completed
Brief description of the entry criteria indicate a clear intention of when the process will be used
 </td>
  </tr>
</table>


    11. Approval Process Steps

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Approval process step names will follow the following convention:
Attribute
Naming Convention
Step Name
<Decision Outcome> - <User Friendly Description>
Description
A full description of the step including what it does and the intended actions that will be performed (e.g. who will it be assigned to)
 </td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of approval process step naming that should not be used

Approval Process Step Name
Reason
Step 1
This is not descriptive enough as it will be displayed in the approval related list to users. Does not provide what was evaluated.
Complex Approval – Step 1
More descriptive but does not provide users with a clear enough picture of what was evaluated

The following are examples of the naming convention that will be used

Approval Process Step Name
Reason
Auto Approved – Value within personal limit
The approval step becomes self documenting showing the administrator and user the result of the approval step
Auto Rejected – Value exceeds company policy
The approval step becomes self documenting showing the administrator and user the result of the approval step
Approval – Sent to Manager
The approval step becomes self documenting showing the administrator and user the result of the approval step
Approval – Sent to Legal
The approval step becomes self documenting showing the administrator and user the result of the approval step
 </td>
  </tr>
</table>


    12. Visualforce Pages

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Visualforce page names and labels should be unique, beginning with an uppercase letter. It should not contain underscores or spaces. The words should be concatenated with Initial uppercase and subsequent internal words capitalized.  Whole words should be used and use of acronyms and abbreviations should be limited.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL.</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of Visualforce Page naming that should not be used

Visualforce Page Name
Reason
Override_Customer_View
Underscores should not be used
Custoverrideview
Name and Label becomes hard to read without capitalization

The following are examples of the naming convention that will be used

Visualforce Page Name
Reason
CustomerView
Clearly defined and succinct name
MailFaxRequest
Clearly defined and succinct name
 </td>
  </tr>
</table>


    13. Apex Classes

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Class names should be unique, beginning with an uppercase letter. It should not contain underscores or spaces. The words should be concatenated with Initial uppercase and subsequent internal words capitalized.  Whole words should be used and use of acronyms and abbreviations should be limited.
Apex classes that are custom controller classes should be suffixed with Controller
Apex classes that are controller extensions should be suffixed with XController, where X is the name of the Visualforce page that is extended. That allows for easy searching of controllers related to Visualforce pages.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.
</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of Apex class naming that should not be used

Class Name
Reason
FHACustomer
Using acronyms should be avoided as they are not mnemonic
GrtBgClass
Whole words should be used in place of shortened versions GreatBigClass
addresshandler
Class does not begin with an uppercase letter
Address_Handler
Underscores should be avoided

The following are examples of the naming convention that will be used

Class Name
Reason
Customer
Full word used to describe the class and starts with uppercase
AddressHandler
Multiple words concatenated with subsequent words capitalised
MailFaxController
Controller Extension for the Mail_Fax__c object
CustomerController
Customer controller for the customer object
 </td>
  </tr>
</table>


    14. Apex Batch, Schedulable, and Queueable Classes

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Class names should be unique, beginning with an uppercase letter. It should not contain underscores or spaces. The words should be concatenated with Initial uppercase and subsequent internal words capitalised. Whole words should be used and use of acronyms and abbreviations should be limited.

Apex classes that are batch classes should be suffixed with _Batch
Apex classes that are Scheduleable classes should be suffixed with _Schedule
Apex classes that are Queuable classes should be suffixed with _Queueable
</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of Apex batch, scheduleable, and queueable class naming that should not be used

Class Name
Reason
GrtBgClass
Whole words should be used in place of shortened versions GreatBigClass and the appropriate suffix should be used.
contactbatch
Class does not begin with an uppercase letter and an underscore should always precede the suffix.
Address_Update_Batch
Underscores should be avoided other than for the suffix

The following are examples of the naming convention that will be used

Class Name
Reason
RoleExpiry_Batch
Multiple words concatenated with subsequent words capitalised. Suffixed with  _Batch denoting that this is a batch apex class.
RoleExpiry_Schedule
Multiple words concatenated with subsequent words capitalised. Suffixed with  _Schedule denoting that this is a scheduleable apex class.
RoleExpiry_Queueable
Multiple words concatenated with subsequent words capitalised. Suffixed with  _Queueable denoting that this is a queueable apex class.
 </td>
  </tr>
</table>


    15. Apex Triggers

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Triggers should always be named using the format [object Name][Operation]Trigger
OR
[Object Name]Trigger for triggers that include all operations for that object.
For example: AccountInsertTrigger, AccountUpdateTrigger, OrderInsertTrigger.
There should only be one trigger per operation per object. It is strongly recommended to include only a single trigger with all operations inside that trigger per object.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>None</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of trigger naming naming that should not be used

Validation Rule Name
Reason
UpdateAccountAddresses
The object name should always be before the operation in the name. 
AccountUpdateContacts
Is specific to a business function and would allow for other update triggers to be created for the same object.

The following are examples of the naming convention that will be used

Trigger Name
Reason
AccountUpdateTrigger
Generic trigger that performs only update operations.
AccountInsertTrigger
Generic trigger that performs only insert operations
AccountTrigger
Generic trigger that performs insert,update, and delete operations. This would be the only trigger for the account object.
 </td>
  </tr>
</table>


    16. Apex Test Classes

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Test class names should be unique, beginning with an uppercase letter. It should not contain spaces. The words should be concatenated with Initial uppercase and subsequent internal words capitalized.  Whole words should be used and use of acronyms and abbreviations should be limited.
The test class will use the convention <Apex Class Being Tested>Test. This keeps the alphabetical order of the classes intact.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of Apex class naming that should not be used

Class Name
Reason
TESTCustomerManagement
Test classes should not have "TEST" in the prefix, but rather have “Test” in the suffix. 

The following are examples of the naming convention that will be used

Class Name
Reason
CustomerManagementTest
Test class for the CustomerManagement Apex class. Will be listed alphabetically under the class being tested.
 </td>
  </tr>
</table>


    17. Apex Methods

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Methods should be verbs, in mixed case with the first letter lowercase, with the first letter of each internal word capitalized. Whole words should be used and use of acronyms and abbreviations should be limited.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of Apex method naming that should not be used

Method Name
Reason
handleCalculation() 
What is being handled?! 
performServices() 
Perform what services? 
dealWithInput() 
How exactly is the input being dealt with? 
NTInQ1()
Cannot determine from the name what the function does 

The following are examples of the naming convention that will be used

Method Name
Reason
ammortizationCalculation() 
Describes what calculation is performed 
repaginateDocument()
Describes the service being performed 
getEmployeeDetail() 
Describes what is being done 
numberOfTransactionsInQ1()
Longer names are better if they are needed for clarity 
 </td>
  </tr>
</table>


    18. Apex Variables

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Variables should be in mixed case with a lowercase first letter. Internal words start with capital letters.
Variable names should be short yet meaningful. The choice of a variable name should be mnemonic— that is, designed to indicate to the casual observer the intent of its use. One-character variable names should be avoided except for temporary "throwaway" variables. Common names for temporary variables are i, j, k,m, and n for integers; c, d, and e for characters.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>None</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of Apex variable naming that should not be used

Variable Name
Reason
x = x – y 
Variable names are ambiguous

The following are examples of the naming convention that will be used

Variable Name
Reason
currentBalance = lastBalance - lastPayment
Unambiguous names that have a clear meaning
 </td>
  </tr>
</table>


    19. Apex Constants

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>The names of variables declared class constants should be all uppercase with words separated by underscores ("_").
Common constants used across the application should be declared in the GlobalConstants class (see section 7.6)
Constant scope should be kept to the minimal required.  Private class attributes are preferred to publicly defined constants.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>None</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of Apex constant naming that should not be used

Class Name
Reason
maxCharacters
Indistinguishable from a variable name

The following are examples of the naming convention that will be used

Class Name
Reason
MAX_CHARACTERS
Uppercase letters help the reviewer determine that it is a constant
 </td>
  </tr>
</table>


    20. Apex Type Names

<table>
  <tr>
    <td>Rules for Naming</td>
  </tr>
  <tr>
    <td>Type names should use an uppercase first letter.  This follows the Java naming conventions. This is to ensure that the type names are not similar to the variable names that immediately proceed them.</td>
  </tr>
  <tr>
    <td>Exceptions</td>
  </tr>
  <tr>
    <td>None</td>
  </tr>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of Apex type naming that should not be used

Type Name
Reason
map<id,string> Contacts
"map", “id”, and “string” do not start with an uppercase letter.
String Contact
“string” does not start with an uppercase letter.

The following are examples of the naming convention that will be used

Type Name
Reason
Map<Id,String> Contacts
Starts with an uppercase letter
String Contact
Starts with an uppercase letter
</td>
  </tr>
</table>


# Best Practices

    21. Constants and Literals

Avoid 'hard coded' constants. For example

Public static final START_DAY = 2;	//Week begins on Monday

If (weekDay(currentDate) >= START_DAY…

is much easier to understand and maintain than

If (weekday(currrentDate) >= 2

    22. Code indentation

The highest level code for each routine should begin 1 tab stop (4 characters) in from the left, this allows comments delineating each section of code to show up clearly 

Each level of code should begin 1 tab stop further in than the level above.

When an expression will not ﬁt on a single line, break it according to these general principles:

• Break after a comma.

• Break before an operator.

• Prefer higher-level breaks to lower-level breaks.

• Align the new line with the beginning of the expression at the same level on the previous line.

Here are some examples of breaking method calls:

function(longExpression1, longExpression2, longExpression3,

         longExpression4, longExpression5);

var = function1(longExpression1,

                function2(longExpression2,

                          longExpression3));

Following are two examples of breaking an arithmetic expression. The ﬁrst is preferred, since the break occurs outside the parenthesized expression, which is at a higher level.

longName1 = longName2 * (longName3 + longName4 - longName5)

 + 4 * longname6; **// PREFER**

longName1 = longName2 * (longName3 + longName4

 - longName5) + 4 * longname6; **// AVOID**

Line wrapping for if statements should generally use:

//DON’T USE THIS INDENTATION

if ((condition1 && condition2)

    || (condition3 && condition4)

    ||!(condition5 && condition6)) { **//BAD WRAPS**

    doSomethingAboutIt(); **//MAKE THIS LINE EASY TO MISS**

}

//USE THIS INDENTATION INSTEAD

if ((condition1 && condition2)

        || (condition3 && condition4)

        ||!(condition5 && condition6)) 

{

    doSomethingAboutIt();

}

//OR USE THIS

if ((condition1 && condition2) || (condition3 && condition4)

        ||!(condition5 && condition6))

{

    doSomethingAboutIt();

}

    23. Effective Testing (NOTE:  http://www.salesforce.com/us/developer/docs/apexcode/Content/apex_testing_best_practices.htm)

The following principles apply to unit testing Apex code

1. Cover as many lines of code as possible

* You must have at least 75% of your Apex scripts covered by unit tests to deploy your scripts to production environments. In addition, all triggers should have some test coverage.

* Salesforce recommends that you have 100% of your scripts covered by unit tests, where possible.

2. In the case of conditional logic (including ternary operators), execute each branch of code logic.

3. Make calls to methods using both valid and invalid inputs.

4. Complete successfully without throwing any exceptions, unless those errors are expected and caught in a try…catch block.

5. Always handle all exceptions that are caught, instead of merely catching the exceptions.

6. Use System.assert* methods to prove that code behaves as expected. 

7. Use the runAs method to test your application in different user contexts.

8. Use the isTest annotation. Classes defined with the isTest annotation do not count against your organization limit of 1 MB for all Apex scripts.

9. Exercise bulk trigger functionality—use at least 201 records in your tests.

10. Write comments stating not only what is supposed to be tested, but the assumptions the tester made about the data, the expected outcome, and so on.

11. Debug statements and Comments are not included in the Code coverage.

12. User records are not covered by test methods.

13. Web service calls should be tested using a Mock class.

14. Large amounts of test data should be loaded by using the Test.loadData.

15. Never use @seeAllData.  Accessing data specific to a sandbox can result in deployments failing

16. Do not write test classes merely to get code coverage. It is much more effective to write the test code to cover specific business cases. You will find that if you use this method you will cover much more code, much faster than just writing test code to get coverage only. Additionally this will help ensure that you are meeting the business requirements in addition to testing for bugs. 

    24. Bulkify All Code

Bulkifying Apex code refers to the concept of making sure the code properly handles processing multiple records at one time. When a batch of records initiates Apex, a single instance of that Apex code is executed, but it needs to handle all of the records in that given batch. For example, a trigger could be invoked by a Force.com SOAP API call that inserted a batch of records. That trigger would need to be able to handle at least 200 records since triggers break up records into 200 record batches. As a rule of thumb make sure all apex code written can handle at least 200 records at a time. This number could be much greater as well for custom methods querying against large datasets. 

        1. Never use SOQL queries or DML statements inside FOR loops

A common mistake is that queries or DML statements are placed inside a for loop. There is a governor limit that enforces a maximum number of SOQL queries. There is another that enforces a maximum number of DML statements (insert, update, delete, undelete). When these operations are placed inside a for loop, database operations are invoked once per iteration of the loop making it very easy to reach these governor limits.

Instead, move any database operations outside of for loops. If you need to query, query once, retrieve all the necessary data in a single query, then iterate over the results. If you need to modify the data, batch up data into a list and invoke your DML once on that list of data. 

This practice definitely creates some complications but is critical to ensuring governor limits are not reached.

Here is an example of what NOT to do (incorrect lines are in bold) - 

//For loop to iterate through all the incoming Account records

for(Account a: accounts) {

      	  

    //THIS FOLLOWING QUERY IS INEFFICIENT AND DOESN'T SCALE

    //Since the SOQL Query for related Contacts is within the FOR loop, if this 

    //trigger is initiated 

    //with more than 100 records, the trigger will exceed the trigger governor limit

    //of maximum 100 SOQL Queries.

      	  

    **List<Contact> contacts = [select id, salutation, firstname, lastname, email **

**                              from Contact where accountId = :a.Id];**

 		  

    for(Contact c: contacts) {

        c.Description=c.salutation + ' ' + c.firstName + ' ' + c.lastname;

 	  	   

        //THIS FOLLOWING DML STATEMENT IS INEFFICIENT AND DOESN'T SCALE

        //Since the UPDATE dml operation is within the FOR loop, if this trigger is 

        //initiated with more than 150 records, the trigger will exceed the trigger 

        //governor limit of 150 DML Operations maximum.

      	                  	      

        **update c;**

    }    	  

}

        2. Querying Large Data Sets

The total number of records that can be returned by SOQL queries in a request is 50,000. If returning a large set of queries causes you to exceed your heap limit, then a SOQL query for loop must be used instead. It can process multiple batches of records through the use of internal calls to query and queryMore. If is possible to hit the heap limit and never even reach the max record limit of 50,000 records if you are querying a large number of fields in an object.

//A runtime exception is thrown if this query returns enough records to exceed your heap limit.

Account[] accts = [SELECT id FROM account];

       Instead, use a SOQL query for loop as in one of the following examples:

// Use this format for efficiency if you are executing DML statements 

// within the for loop.  Be careful not to exceed the 150 DML statement limit.

for (List<Account> acct : [SELECT id, name FROM account

                            WHERE name LIKE 'Acme']) 

{

    // Your code here

    update acct;

}

Let the Force.com platform chunk your large query results into batches of 200 records by using this syntax where the SOQL query is in the for loop definition, and then handle the individual datasets in the for loop logic.

**Note: **This approach is the one time when it is acceptable to use DML (insert, update, delete) inside of a for loop. You still need to be weary of the 150 DML statement limit within the loop. 

    1.  Triggers

There are many considerations that must be taken in account when developing apex triggers. A poorly written trigger can easily cause your application to cease to function.

        1. Muting Triggers

It is a best practice when developing triggers that you have the ability to easily disable the functionality of triggers. This is especially useful for when you need to perform data loads, or if a trigger is causing user errors. By default there is no easy way to disable a trigger using configuration. Once a trigger or other apex class has been migrated to production, the only way to disable it would be by using the metadata API to delete it.

In order to allow for making it easy to disable triggers, all triggers must have logic allowing the triggers to be disabled by profile and/or user using custom settings or custom metadata types. 

The example below shows how to implement the logic to disable a trigger using custom settings.

Public with sharing class Helper 

{

    public static Boolean IsTriggerEnabled()

    {

        TriggerExecutionSettings__c settings =     TriggerExecutionSettings__c.getValues("AccountInsertUpdate");

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

Public with sharing class Helper AccountInsertUpdateTrigger on Account (before insert, before update)

{

   if( triggerHelper.IsEnabled())

   {

      //DO SOMETHING

   }

}

	  

        2. Trigger Maintainability

When Salesforce triggers execute there is no guarantee in what order they will execute. This is why you should never have multiple triggers that operate on the same object and operation. Triggers should always be separated by operation for each object. For example: If you created two triggers that both handled the before update operation, there is no guarantee as to which trigger would execute first. This could create confusion when trying to debug the code and unexpected results.

When developing triggers, it is best to think of each trigger as the driver for your code. You want to separate the business logic to a separate helper class to keep the code within the trigger neat and separated by operation. 

Within the trigger you should create a fork for each trigger operation for before/after, and insert, update, and delete. Once you have identified the trigger operation, such as before update, you would then fire the helper method for before update in a separate class. This makes it easier to understand what the trigger is doing.

Take a look at the code sample below that executes a trigger for before insert and update.

Public with sharing class Helper AccountInsertUpdateTrigger on Account (before insert, before update)

{

   if( triggerHelper.IsEnabled() & trigger.IsBefore() && trigger.IsUpdate())

   {

      AccountTriggerHelper.BeforeUpdate();

   }

   else if( triggerHelper.IsEnabled() & trigger.IsBefore() && trigger.IsInsert())

   {

      AccountTriggerHelper.BeforeInsert();

   }

}

    2. Never Hardcode Ids

When deploying Apex code between sandbox and production environments, or installing Force.com AppExchange packages, it is essential to avoid hardcoding IDs in the Apex code. By doing so, if the record IDs change between environments, the logic can dynamically identify the proper data to operate against and not fail.

Here is a sample that hardcodes the record type IDs that are used in an conditional statement. This will work fine in the specific environment in which the code was developed, but if this code were to be installed in a separate org (ie. as part of an AppExchange package), there is no guarantee that the record type identifiers will be the same. 

for(Account a: Trigger.new){

     	 

   //Error - hardcoded the record type id

   if(a.RecordTypeId=='012500000009WAr'){     	  	

      //do some logic here.....

   }else if(a.RecordTypeId=='0123000000095Km'){

      //do some logic here for a different record type...

   }

    	 

}

Now, to properly handle the dynamic nature of the record type IDs, the following example queries for the record types in the code, stores the dataset in a map collection for easy retrieval, and ultimately avoids any hardcoding.

//Query for the Account record types

List<RecordType> rtypes = [Select Name, Id From RecordType 

                           where sObjectType='Account' and isActive=true];

     

//Create a map between the Record Type Name and Id for easy retrieval

Map<String,String> accountRecordTypes = new Map<String,String>{};

for(RecordType rt: rtypes)

   accountRecordTypes.put(rt.Name,rt.Id);

     

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

By ensuring no IDs are stored in the Apex code, you are making the code much more dynamic and flexible - and ensuring that it can be deployed safely to different environments.

    3.       Custom Settings 

Custom settings are a useful tool when you have application specific settings that you wish to store that let you configure the application rather than having to make a code change every time these settings change. 

Try to utilize custom settings whenever possible when you find that you need to hardcode a static value such as email addresses or Salesforce Ids within your application. 

Another good use of custom settings is to allow for tweaking of the performance of the application. For example: Instead of hard coding the number of records to process for a batch apex method to 200 records, you could create a custom setting that allows you to easily change the number of records to be processed for each batch. 

Additionally as mentioned above in the "Muting Triggers" section, Custom settings can be used to allow you to enable/disable triggers, or other code, since you are unable to do this easily from your production environment natively.

    4.       Enforcing Sharing Rules in Controllers

Like other Apex classes, all controllers and controller extensions run in system mode. Typically, we want a controller or controller extension to respect a user's organization-wide defaults, role hierarchy, and sharing rules. We can do that by using 'with sharing' keywords in the class definition. Note that if a controller extension extends a standard controller, the logic from the standard controller does not execute in system mode. Instead, it executes in user mode, in which the profile-based permissions, field-level security, and sharing rules of the current user apply. Unless you have a good reason for needing to expose all records of a class to the running user then all classes should ALWAYS use the "with sharing" keywords.

If you do not use this practice it is possible that a user could gain access to records that they normally would not have access to.

    5. Governor Limits

Because of the multitenant nature of Salesforce, various types of governorment limits are enforced to ensure that one tenant does consume all of the resources. The following are best practices to avoid hitting limits.

* Limiting queries by using static class variables to store query results instead of firing frequent queries.

* Never use SOQL/SOSL/DML in loops.

* Leverage custom settings to create custom sets of data, as well as create and associate custom data for an organization, profile, or specific user. All custom settings data is exposed in the application cache, which enables efficient access without the cost of repeated queries to the database. This data can then be used by formula fields, validation rules, Apex, and the SOAP API.

* Making sure that database statements such as insert(), update(), and delete() operate in bulk 

* Use system methods to track governor limits: Apex has a System class called Limits that lets you output debug messages for each governor limit. There are two versions of every method. The first returns the amount of the resource that has been used in the current context, while the second version contains the word limit and returns the total amount of the resource that is available for that context. Using these methods judiciously ensures that the execution governor limits are never hit.

* Enable governor limit warning emails: When an end-user invokes Apex code that surpasses more than 50% of any governor limit, you can specify a user in your organization to receive an email notification of the event with additional details. 

* Asynchronous execution: Use asynchronous apex (@future) appropriately. Async apex gets its own governor limits but there are a maximum of ten @future methods within a single apex transaction. Do not call future methods from triggers.

* Batch Apex: Use of Batch Apex to handle millions of records. Every batch gets its own set of governor limits. Do not initiate batches from triggers.

    6. SOQL Query Optimization

When writing SOQL queries you want to make sure that your queries will perform when running against both small and large datasets. The following are some best practices to use to build performing SOQL queries.

* Always limit the number of records that to be returning by the query by using the LIMIT keyword.

* Never use fields that are not indexed in the WHERE clause.

* Keep your queries as selective as possible and use custom indexes to improve performance.

* Try to avoid using the "NOT IN" keyword as this is a very expensive in regards to performance.

* Try to use the "AND" operator, and limit the use of OR operators in your statements.

* Try to avoid using a combinations or "AND" and “OR” operators in your statements.

* Try to avoid using the "ORDER" operator as it takes a lot of processing

* Use StartsWith as much as possible for query filters. Techniques such as reverse phone numbers can be used in this approach.

* Use record types to help with data segmentation

* Create skinny tables for commonly searched fields to decrease search times.

* Use the Salesforce query optimizer located in the developer console to make sure that your query will perform. Performing queries should have a score of less than 1. The closer to 1 the score, the worse the query will perform.

<table>
  <tr>
    <td>Demonstrative Example</td>
  </tr>
  <tr>
    <td>
The following are examples of bad SOQL queries.

Query
Reason
SELECT Id, Name FROM Account
This will return every record in the account object. This query will most likely never finish.
SELECT Id, Name FROM Account WHERE Active = true
This query is more selective than the last, but still would return too many records and would most likely never finish.
Select Id, Name FROM Account WHERE Name NOT IN: myAccountsList
This query fairly selective, but would still be an expensive query because the "NOT IN" operator is very processing intensive. Use the “IN” operator instead of “NOT IN” wherever possible.

The following are examples of good SOQL queries

Query
Reason
Select, Id, Name From Account WHERE name = ‘Salesforce’ LIMIT 1
Very selective query limiting the records returned to 1.
Select Id, Name FROM Account Where CreatedDate = Yesterday LIMIT 99
Very selective query limiting to just the records created within the past 24 hours. Also the query limits the total records returned to 100.
 </td>
  </tr>
</table>


    7. Visualforce Page Best Practices

Just because you can, doesn’t mean you should! Before going down the customization route make sure you properly evaluate the pros and cons of creatinge custom pages. This is especially true when creating custom pages to override standard functionality.  When overriding standard functionality you lose the advantage gained of new features in future releases.

If you do go down the customization route you must make sure you optimize the Visualforce pages you create for better performance in order to have a positive user experience. 

* Avoid using the rendered="false” if possible. Even though the components do not show up on the page, processing still needs to be done that will cause the page to render slower. If a large portion of the components of a visualforce page have rendered=”false”, consider creating a separate page instead of using partial rendering.

* Use Salesforce remoting or remote objects to perform asynchronous execution of apex using javascript. This will allow the user to perform operations without having to wait for the server to respond. 

* Cache data in custom settings, custom metadata types, and the org cache to improve the performance of the page. Access to data in these mechanisms is much faster than executing SOQL queries to retrieve the same data. Additionally they do not count against your max queries limit.

* Avoid the use of iframes whenever possible as these will slow the loading of the page. If you need to create a window into Salesforce from an external system consider using Canvas instead, since it is much more tightly integrated into Salesforce and takes care of the authentication for you. 

* Use minifiedminimized javascript and CSS file resources

* Avoid use of references to external scripts or resources. Instead download them as static resources and reference the static resources. Static resources are cached and provide for better performance. Never reference a Salesforce unsupported javascript or CSS library directly as these could change at any time. Any API that is not versioned is considered an unsupported API.

* Use only web optimized images and image maps to reduce the need to load multiple images.

* Use paging techniques when working with large datasets on a page. Avoid displaying more than 20 results per page. Use the SOQL offset or the standardSetController to control paging.

* Make sure all your SOQL queries are optimized using the query optimizer located in the developer console. 

* Use lazy loading techniques to load parts of the page first, giving users access to some of the functionality while other parts of the page are still loading. For example you can load the page first and then the data for the page once the page has finished loading. 

* Instead of polling to retrieve changes in data or refreshing the page considering using the streaming api to receive push notifications when data has changed.

For more Visualforce best practices see

[http://www.salesforce.com/docs/en/cce/salesforce_visualforce_best_practices/salesforce_visualforce_best_practices.pdf](http://www.salesforce.com/docs/en/cce/salesforce_visualforce_best_practices/salesforce_visualforce_best_practices.pdf)

    8. Lightning Components Vs. Visualforce?

Lightning components are a rather new addition to the Salesforce suite of development tools. There is much confusion as to what are lightning components and when to use lightning versus Visualforce.

        3. **What is Lightning?**

Lightning is a framework that Salesforce has built to allow for a new look and feel to Salesforce, as well as the ability to create faster, more lightweight applications.

There are three 3 main parts to lightning:

1. **Lightning Experience – **The lightning experience is a completely new look and feel to Salesforce that takes into account modern user interface design practices that is commonly used throughout the web today. This is based on responsive design patterns such that the format of what you can see on the screen is based on screen size that you are viewing the content. Instead create a single web application, each page is made up of various components that can be easily changed out or rearranged.

2. **Lightning Design System – **The design system is a new UI framework built off of angular that helps developers easily recreate the same look and feel of the Lightning Experience in their custom applications. This framework can be used in Visualforce, Lightning Components, or even in custom external based web applications. For more information on the design system visit [http://www.lightningdesignsystem.com](http://www.lightningdesignsystem.com) 

3. **Lightning Components –** Lightning components is a new development infrastructure that Salesforce has developed to quickly create high performing web applications based on a component model. A lightning component can be a web page or even a piece of a web page. Lightning components turns html, javascript, and CSS into an object-oriented language. Everything is a first class component in this framework. What this means is that instead of having to traverse the DOM you use getters and setters to access various elements of your application. For example the following are "objects" or “components” in the framework: “div”, “form”, “input”, “head”, “body”, “span”, javascript events such as “onclick”, etc. 

The real power of lightning is that you can pass components between each other to build reusable pieces of an application. You can even pass a javascript event that fires from one component to another! 

The Salesforce Lightning Experience is even built using Lightning Components. That means you can develop your own custom components using the same technology that Salesforce uses internally. Combining that with the Lightning Design System you can completely replicate any out of the box component in the Lightning Experience.

        4. **Lightning vs. Visualforce?**

The question many people ask is "Will Visualforce be going away?" Think of lightning as just yet another tool in your Salesforce Tool belt. Both have their uses based on what you are trying to do.

**Visualforce Pros**

* Can be made to look like the "Aloha" look and feel of Salesforce without much trouble.

* Can use the Lightning Design framework to make the look feel of that of the Lightning Experience.

* Allows for quick development of pages that interact directly with the Salesforce platform keeping everything on the server-side. 

* Is a tried and true development platform in use today by thousands of customers.

* Is better for single page applications that are not component based.

          **Lightning Pros **

* Since most everything runs client-side, and all server-side calls to Salesforce are performed asynchronously, it is very fast.

* Allows you to easily make applications with the same look and feel of the lightning experience. 

* Since everything is component based you can separate the development out to several different developers without risking the developers to walk over each other.

* Since even the styling is broken out you can have your UI designer work independently of your Salesforce developers on various components.

* Allows you to quickly change, add, or remove pieces of a page without having to think about refactoring the entire page. 

* Ideal when you have the need to create a more component-based application made up of multiple "mini application", rather than a single page application.

* Ideal for creating lightweight, responsive mobile applications.

          **Visualforce Cons**

* Is very heavy, and much slower than the lightning framework because it uses a stateful infrastructure to keep the state for round-trips from the server.

* Requires a lot of work to rearrange pieces of the screen. Usually requires a complete rework of the HTML. 

* Very difficult for multiple developers to work on the same page at the same time. Salesforce developers will typically have to wait for the UI designer to complete their work before adding functionality. 

**Lightning Cons**

* Requires a little bit of a learning curve for seasoned Visualforce developers, as it requires strong javascript skills and is a completely different approach to development on the Salesforce platform.

* Doesn’t support creating applications with the current "Aloha" UI look and feel.  

       

When deciding to use lightning or Visualforce, carefully consider each of the pros and and cons. Consider the following questions when making your decision?

1. Will the application be a standalone application, or can it be broken into multiple components?

2. Does the application need to be responsive and run on multiple device formats?

3. Will the application need to look and feel like the "Aloha" UI or the “Lightning Experience” UI?

4. Do our developers have strong javascript and CSS skills? Will there be considerable ramp up time if we choose to use lightning?

1.            Integrating Salesforce with External Systems

There are many different APIs that Salesforce has to offer within its toolkit. Just as with using Lightning and Visualforce there are many considerations you must make when choosing a specific API to use. 

    9.  Inbound Requests

Salesforce offers two primary types of APIs based on industry standards. The first is a SOAP based API, and the second is a REST based API. The REST API is very lightweight, has no WSDL definition file that is needed to install, and performs very well. The SOAP API is much heavier and slower than the REST API, but offer many more features and can handle many more records than the REST API.

**SOAP API**

The SOAP API was the very first API that Salesforce offered and as such is the most complete API available today. There are two flavors of this API available based on the type of user you are, and application that you are developing. The first is the enterprise API and the second is the partner API. Don’t be fooled by the names of the APIs. Just because you are not a partner, doesn’t mean that you can’t use the partner API. 

The SOAP API supports database operations such as query, insert, update, delete, as well as support many other metadata related requests related to users or understanding understanding the Salesforce data model. For a complete reference to the functionality of the SOAP API you may view the developers guide at:

[http://developer.salesforce.com/docs/atlas.en-us.api.meta/api/](http://developer.salesforce.com/docs/atlas.en-us.api.meta/api/) 

**Enterprise API**

The only difference between the enterprise and partner API is that the enterprise API is strongly typed to a specific Salesforce environment. The API exposes every Salesforce object standard and custom as data structures within the API. This makes it much quicker for one to develop, as there is no need to spend time creating data structures for each object you wish to work with within the org. 

The downside of the SOAP API is that every time you add a new field or object, or delete a field or object, you must reimport the WSDL that represents the new data structure. Deleting objects and fields is especially dangerous, as that will break your current integrations if you do not update the WSDL.

**Partner API**

The partner API on the other hand is not strongly typed for any one particular environment. It was originally designed for Salesforce partners to use where the data model could be different for each customer using their integration. Many customers also use this API because it reduces the risk of something breaking because a field was deleted, and in the long term reduces the overall maintenance cost since a new WSDL does not need to be imported every time the data model changes and you wish to access the new fields and/or objects in the data structure. 

The downside of the Partner API is that there is a substantial amount of additional coding and work required for the initial implementation because you must generate your own xml within your code to bind to each object and field. Once the initial setup is complete, the ongoing maintenance is the same, if not less than that of the Enterprise API. 

**REST API**

The REST API is an API that has similar functionality to that of the SOAP API, but is based on REST standards. That means there is no WSDL to download and maintain, and all requests are HTTP based using common Verbs such as Post, Get, Put, Patch, and Delete. The rest API takes requests and returns responses in either XML or JSON.

The REST API is a good API to just when you need to make lightweight operations with a quick response, such as on mobile devices. 

Just like the SOAP API, the REST API supports database operations such as query, insert, update, and delete except that since the REST API is a newer API it is isn’t as complete as the SOAP API. 

Aside from the actual functionality differences between the two APIs it is good to understand in general the differences between REST and SOAP. For more information on REST and SOAP visit the following sites below.

[http://en.wikipedia.org/wiki/SOAP](http://en.wikipedia.org/wiki/SOAP)

[http://en.wikipedia.org/wiki/Representational_state_transfer](http://en.wikipedia.org/wiki/Representational_state_transfer) 

**BULK API**

The REST and SOAP APIs are great tools for general transactional real-time applications, but tend to fall apart when you need to work with large volumes of data. When working with data volumes of above 50,000 records you should look to using the BULK API.

The BULK API is a REST based asynchronous API designed to handle inserting, updating, and deleting of large amounts of data. Generally speaking the BULK API can act on up to 50 million records in a rolling 24-hour period according to the official documentation. If you need to work with a larger amount of data than 50 million records per day, you can contact Salesforce support to have your limits increased with proper justification. 

For more information on the developing with the BULK API and limits of the BULK API visit the following sites below.

[https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/asynch_api_concepts_limits.htm](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/asynch_api_concepts_limits.htm) 

[https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/) 

**BEWARE OF YOUR DAILY API LIMITS**

Every time you make a call to the SOAP or REST API you use an API call that is allotted to your organization on a rolling 24 hour period. If you use up all of your API calls on at 24 hour period then you will be no longer allowed to make calls to the SOAP or REST API until you rolling 24 hour usage has dropped below the limit. 

This is one of the main reasons why it is recommended that if you need to process more than 50,000 records, you use the BULK API, as the BULK API does not take up your daily API limits. For example, if you need to process 1 million records and use the SOAP API processing 200 records at a time, you will use up 5,000 of your API calls. Not only does this take a long time to process you are will endanger your organization of breaching this limit. This is especially true as you add more services to your organization that are using the SOAP or REST APIs. 

**Apex Web Services**

If the SOAP API or the REST API won’t easily accomplish your business requirements, Salesforce allows you to create your own custom SOAP or REST API that you can expose for consumption by external systems. This API allows you to implement you own custom API methods with more complex logic than is available with the out of the box SOAP and REST APIs. 

Think of Apex Web Services as the "Custom API" where the SOAP and REST APIs are the “Out of the Box” APIs. The primary function for the out of the box APIs are for data movement and manipulation. Where the Custom API is more for working with smaller numbers of records where you need more complex logic application them. 

**BEWARE OF LONG RUNNING PROCESSES**

When a custom API call that takes longer than 5 seconds to complete gets put into what is called a "long running process queue". If you have too many concurrent methods that are in this long running process queue, Salesforce will block all future calls to your custom APIs, long and short running, until the long running process queue drops below the max allowed value of 10 concurrent long running process. Any additional calls to the custom API while the long running process queue is full will receive the error “Concurrent Requests Limit Exceeded”. This limit is in place to protect customers against denial of service attacks. 

It is imperative that you take care when designing custom apex services that they do not take longer than 5 seconds to complete. This is why it is recommended that you only utilize these service to operate on smaller numbers of records to avoid long running processes.

If you find that your methods are taking too long to complete you may want to think about breaking them up into multiple transactions. For example you may want to first call the SOAP API to retrieve the records and then send a smaller number of records at a time to the custom API. 

**Outbound Requests**

In addition to exposing APIs to external systems, Salesforce also has a few mechanisms for making calls out to external systems as well. 

1. **HTTP call-outs using Apex**

If you need to make a call out to an external web service, using apex you can use the HTTPRequest and HTTPResponse objects to make and receive HTTP calls to external systems. This is ideal for communicating with simple services that require simple HTTP messages to be passed like a REST API. 

2. **Call-Outs to SOAP APIs**

Salesforce also supports making more complex call-outs to SOAP APIs as well. In order to communicate with an external SOAP service you will need to import the WSDL under Develop->Classes. Once the WSDL has been imported a façade class is generated for each of the methods in the SOAP service. You then can use apex to execute those methods to make a call-out to the SOAP service. 

Occasionally the WSDL will not import because the Salesforce WSDL parser does not understand the WSDL. In this case you will manually need to recreate the façade by hand. This procedure is out of scope of this document. 

3. **Outbound Messaging**

Using the WSDL importer and the HttpRequest or HTTPResponse apex objects are fine to use when you need to make point-to-point calls. The only drawback is if you are unable to connect to the external service and/or failures occur there is not retry mechanism. 

When you need more complex handling with retry mechanisms built-in in, you may want to consider using Salesforce Outbound Messaging services. Outbound Messaging is part of the Salesforce workflow and approvals system. An outbound message can be automatically executed when a record has been inserted or updated. The real power behind Outbound Messaging is that if an error occurs while communicating with the external service, the outbound message will retry later. The Outbound Messaging system will retry to send the message for up to 24 hours. 

There are a couple drawbacks to using Outbound Messaging. Multiple messages can be sent at the same time if multiple updates occur to a specific record. Don’t use outbound messaging if sequence of events is important, such as with logging. 

Additionally in order to use outbound messaging you must export a WSDL and implement the service on the other end. Many times the time required to implement this service is less time that it would take to implement the retry mechanisms already built into the Outbound Messaging capability.

For more information on how Outbound Messaging works visit the page below.

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_om_outboundmessaging_understanding.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_om_outboundmessaging_understanding.htm) 

# Commenting 

    10. Overview

All methods should begin with a brief comment describing the functional characteristics of the method (what it does). This description should not describe the implementation details (how it does it) because these often change over time, resulting in unnecessary comment maintenance work, or worse yet erroneous comments. The code itself and any necessary inline or local comments will describe the implementation.

Parameters passed to a method should be described when their functions are not obvious and when the method expects the parameters to be in a specific range. Function return values and public variables that are changed by the routine must also be described at the beginning of each appropriate routine:

    11. Class Header

<table>
  <tr>
    <td>Section</td>
    <td>Comment Description</td>
  </tr>
  <tr>
    <td>Author</td>
    <td>Name of author of original code</td>
  </tr>
  <tr>
    <td>Company</td>
    <td>Salesforce.com</td>
  </tr>
  <tr>
    <td>Description</td>
    <td>What the routine does (not how).</td>
  </tr>
  <tr>
    <td>Inputs</td>
    <td>What inputs (if any) were passed into the constructor method</td>
  </tr>
  <tr>
    <td>Test Class</td>
    <td>The test class that covers the functions in this class</td>
  </tr>
  <tr>
    <td>History</td>
    <td>An updated list of who, when and what changed in the class</td>
  </tr>
  <tr>
    <td>Demonstrative example</td>
    <td></td>
  </tr>
  <tr>
    <td>/*------------------------------------------------------------
Author:        Matt Meyers
Company:       Salesforce.com
Description:   A utility class for the contact trigger
Inputs:        "customers" - Contact objects that are being triggered
               "oldCustomers" - Contacts object values before trigger event
               "ta" - Trigger action that is occurring
Test Class:    CustomerManagementTest
History
<Date>      <Authors Name>     <Brief Description of Change>
------------------------------------------------------------*/</td>
    <td></td>
  </tr>
</table>


    12. Function Header

<table>
  <tr>
    <td>Section</td>
    <td>Comment Description</td>
  </tr>
  <tr>
    <td>Author</td>
    <td>Name of author of original code</td>
  </tr>
  <tr>
    <td>Company</td>
    <td>Name of authors company</td>
  </tr>
  <tr>
    <td>Description</td>
    <td>What the test does (not how). Including an outline of all methods executed</td>
  </tr>
  <tr>
    <td>Inputs</td>
    <td>A description of the attributes passed to the method</td>
  </tr>
  <tr>
    <td>Returns</td>
    <td>A description of values passed back from the method</td>
  </tr>
  <tr>
    <td>History</td>
    <td>An updated list of who, when and what changed in the class</td>
  </tr>
  <tr>
    <td>Demonstrative example</td>
    <td></td>
  </tr>
  <tr>
    <td>/*------------------------------------------------------------
Author:        Matt Meyers
Company:       Salesforce.com
Description:   Function to return whether or not a trigger should be fired
               based on the trigger name passed in
Inputs:        The apex trigger name as defined in 'Apex Triggers'
Returns:       true - the trigger should fire
               false - the trigger should not fire
History
<Date>      <Authors Name>     <Brief Description of Change>
------------------------------------------------------------*/</td>
    <td></td>
  </tr>
</table>


    13. Subroutine header

<table>
  <tr>
    <td>Section</td>
    <td>Comment Description</td>
  </tr>
  <tr>
    <td>Description</td>
    <td>What the subroutine does (not how). Including an outline of all methods executed</td>
  </tr>
  <tr>
    <td>Inputs</td>
    <td>A brief description of all attributes passed into the routine</td>
  </tr>
  <tr>
    <td>History</td>
    <td>An updated list of who, when and what changed in the class</td>
  </tr>
  <tr>
    <td>Demonstrative example</td>
    <td></td>
  </tr>
  <tr>
    <td>/*
Description:   Overloaded Method to log a single record to the application log table
Inputs:        logLevel - Debug, Error, Info, Warning
               sourceClass - Originating trigger or utility class
               sourceFunction - Method in class above that caused the message
               referenceId - Process Identifier (e.g. Job Id)
               referenceInfo - Process information
               payLoad - Optional based on integration messages
               ex - the standard exception object for errors
               timeTaken - The time in milliseconds of the transaction

History
<Date>      <Authors Name>     <Brief Description of Change>
*/</td>
    <td></td>
  </tr>
</table>


    14. Variables

Every non-trivial variable declaration should include an in-line comment describing the use of the variable being declared:

MAX_USERS		//Max entry limit for user collection 

MEW_LINE		//New line character string

Note: Variables and methods should be named clearly enough that in_line commenting is only needed for complex or non-intuitive implementation details.

2. Logging & Debugging

    15.     Debugging

Unlike traditional languages such as Java, C++, and C#, Apex and Visualforce can be quite cumbersome and time consuming when trying to debug. You don’t have the luxury of being able to step through the code during runtime. 

Instead of having the ability to set breakpoints and halt execution of the code, you must instead use logging to capture the flow of events to help you troubleshoot the code.

Salesforce a debug log that allows you to output string or even deserialize objects to help you understand what the value of specific complex variables were at specific times during runtime. 

Take a look at the example below. Take note of the line highlighted in yellow. This statement when executed will write a log entry to the Salesforce debug log that you can later view by going to the developer’s console.

Public with sharing class SampleClass

{

    public List<Account> getLeads(Date CreatedDate)

    {

         List<Lead> = leads = [SELECT id,FirstName,LastName FROM Lead WHERE CreatedDate =: CreatedDate];

         System.Debug(‘Leads Retrieved: ‘ + leads);

    }

} 

While writing apex code you should always make sure to add debug statements in key areas of your code that would help in debugging should errors occur. 

Take a look at the example below that expands our example above.

Public with sharing class SampleClass

{

    public List<Account> getLeads(Date CreatedDate)

    {

         List<Lead> = leads = [SELECT id,FirstName,LastName FROM Lead WHERE CreatedDate =: CreatedDate];

         System.Debug(‘Leads Retrieved: ‘ + leads);

    }

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

Notice in the code above that we have added a new method to update our lead records and have added a try/catch block to catch an exception that has occurred. 

Adding debug statements within the catch block is an excellent way to help troubleshooting issues in the future. 

    16.  Custom Logging

The Salesforce debug log is good way to debug your code when you have a limited amount of logs that you want to review over a short period of time. When the Salesforce debug log breaks down is when you want to review logs for issues that occurred the previous day or before. Additionally if you wish to receive notifications of what an issue occurred this is also outside the scope of functionality of the Salesforce debug log.

It is for use cases like these that you want to use a custom logging framework in addition to the debug log to adequately troubleshoot your code. 

The logging framework should write log entries to a custom object. From there you can create workflow rules to send email notifications, create tasks, or even create a ticket in an external system when an error event occurs. 

Although this is a very helpful approach to logging and error notification in Salesforce you must take care when using it. Unlike using the debug log you must write records to the logging object for this approach, which takes up DML calls that may be needed for your application. Keep in mind your DML limits at all times when using this approach. Also keep in mind that every record created will also take up storage in your org so you will need to develop an approach for deleting log records that are no longer needed.

Make sure that when using this custom logging approach, you write a mechanism that will allow you to set the logging level and turn on/off logging by user and/or profile using custom settings by application. This will help you to avoid creating thousands of logging records unnecessarily taking up storage limits.

3. Exception Handling

    17. Abstract

Similar to most modern languages, Apex supports exception handling using try/catch blocks. As a best practice you should always encapsulate your code within a try/catch when there is a possibility of an exception occurring within your code. 

    18. Catching Exceptions

As of version 36.0 of the Salesforce API, there are 24 different types of exceptions that can be caught. When catching exceptions you should always try to catch the specific types of exceptions, whenever possible, as well as include a try/catch block to catch general exceptions outside of the specific ones when it makes sense. 

Working with our example from before notice that we are catching a "DMLException". Since this is the only type of exception that could occur within this code, there was no need to wrap the entire code within a general exception block. 

Public with sharing class SampleClass

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

If we expand our example with some more logic we need to make sure that we catch any unexpected exceptions that would occur when looping through our lead list. Perhaps we are setting a value that is not an acceptable value for the data type of a field on the lead record. 

Take note that we are catching 3 types of exceptions:

1. QueryException – To catch any exceptions that occur when retrieving the lead records.

2. DMLException – To catch any exceptions that occur when inserting the lead records.

3. Exception – To catch any other exceptions that may occur when looping through the lead records.

Public with sharing class SampleClass

{

public List<Account> getLeads(Date CreatedDate)

    {

         List<Lead> leads;

         

         Try

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

    19. Custom Exceptions

Since you can’t throw built-in Apex exceptions, but can only catch them, you can create custom exceptions to throw in your methods. That way, you can also specify detailed error messages and have more custom error handling in your catch block. 

To create your custom exception class, extend the built-in Exception class and make sure your class name ends with the word "Exception".

    Public class OrderException extends Exception

    {

    }

 

    Public with sharing class OrderController

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

 

If you find that you need to create exceptions that are multiple levels deep, then it may be a good time to start thinking about creating a custom exception class so that your exceptions are more easily traceable when trying to debug. 

1. **Sharing & Security **

 

There are many different mechanisms in which access to Salesforce is controlled. It is easiest to think of security in Salesforce broken up into the following 3 different categories: 

 

1. **Object Level Access – **Object level access controls the access various Salesforce standard and custom objects such as Account, Contact, Opportunity, or custom objects you create. Object level access defines if a user has access to Read, Create, Update, or delete records within that object. Additionally object level access also controls which fields users are allowed to view or update on those objects. All object level access within Salesforce is controlled by Profiles and Permission Sets. 

 

1. **Record Level Access – **Once a user has access to a specific object, users can then be limited to view or edit only specific records within that object. This is what we refer to as "Record Level" sharing within Salesforce. Sharing of records is controlled by Salesforce Organization-wide defaults, Criteria Based Sharing, Roles, and manual sharing.  

   

1. **System & Application Level Access – **System and application level access is access users are granted to perform specific actions across the Salesforce application. There are many different actions a user can perform that can be controlled such as user creation, ability to export data, ability to modify setup objects, etc. These permissions are controlled by Profiles and Permission Sets. 

 

1. ** Profiles & Permission Sets **

As mentioned above Profiles & Permission Sets control the object level access and System & Application level access for users. You can pretty much do the same thing with Profiles and Permission Sets except for that a user can only have one profile where you can assign multiple permission sets to a user or profile.  

 

It is recommended to use profiles to create a base set of permissions for users of specific groups. Then create permission sets for each application that users will need access to for each type of role in that application. 

 

For example: 

 

**Profiles** 

System Administrator  

Sales User  

Legal User  

Marketing User  

 

**Permission Sets** 

Order Management Application User  

Order Management Application Admin  

 

The permission sets would be assigned on a user-by-user basis based on the applications that the users need access to. This allows you to easily add or remove access to users for specific applications instead of having to create profiles of various different combinations to handle the same use cases. Think of permission sets as similar to Access Control Lists (ACL). 

 

 

1. **  Salesforce Sharing **

 

Salesforce sharing controls what records users have access to view and edit. Keep in mind that since the profile and permission sets control object level access, if a user doesn’t have access to a particular object, then even if sharing allows them to view or edit records within that object, they will not have access to those records since they don’t have access to the entire object through profiles or permission sets. 

 

When working with Salesforce sharing it is always best to use the most global sharing mechanisms first, then move to the more granular controls. As you move to the more granular sharing controls you need to be more aware of performance considerations. 

 

The following are the Salesforce sharing controls available. 

 

1. **Organization-Wide Defaults** 

Organization-Wide defaults are the highest level and most restrictive sharing controls available on the platform. These settings control the visibility of records on a global scale for objects. These settings are set on an object by object basis. 

 

The following are the available options: 

 

**Public Read/Write/Transfer** 

Public Read/Write/Transfer is the least restrictive organization-wide default and is available only for the lead and case object. This setting allows every user to view, edit, and change ownership of every record within the lead or case objects that are set to "Public Read/WriteTransfer" regardless of their other sharing settings. 

 

**Public Read/Write** 

Public Read/Write is the second least restrictive organization-wide default and is available for most standard and all custom objects. This setting allows every user to view and edit every record within the objects that are set to "Public Read/Write" regardless of their other sharing settings. 

 

**Public Read Only** 

Public Read Only is the second most restrictive organization-wide default and is available for most standard and all custom objects. This setting allows every user to view every record within the objects that are set to "Public Read Only" regardless of their other sharing settings. Users cannot edit records within the objects set to “Public Read Only” unless they are granted “edit” access through other sharing settings. 

 

 

 

**Private** 

Private is the most restrictive organization-wide default and is available for most standard and all custom objects. This setting restricts every user from viewing or editing records within the objects that are set to "Private" unless they are granted “view” or “edit” access through other sharing settings.  

 

1. **Criteria Based Sharing (Sharing Rules)** 

Criteria based sharing is rule or owner based sharing that grants read or read/write access for a set of records to specific groups of users. Criteria Based Sharing is next level of sharing controls below organization wide defaults. 

 

There are two types of rules that can be created. 

 

**Based on Record Owner** 

Rules based on record owner grant access to users in specific roles or groups to records that are owned by users within specific roles or groups. 

 

**Based On Criteria** 

Criteria based rules grant access to users in specific roles or groups to records that match specific criteria on the records within the object. 

 

1. **Role Based Sharing** 

Roles are hierarchal groupings of users within a Salesforce org. Role based sharing propagates the access to records that users have to users up the role hierarchy.  

 

For example: If the following role hierarchy exists: 

 

Sales VP 

 	| 

Sales Executives 

 

Then anyone that is a member of the "Sales VP" role will inherit the access from everyone in the “Sales Executives” role. 

 

**Note: **In order for access to be granted via role hierarches the setting "Grant Access Via Hierarchies" must be checked for each object that you wish to respect role hierarchy sharing. 

 

 

 

1. **Manual Sharing ** 

Manual sharing is the most granular and least performing of all sharing mechanisms within Salesforce.  Care must be taken when using manual sharing as too many manual sharing rules on any single object can cause a delay in response time when viewing records on that object.  

 

Manual sharing allows the owner of a record to manually grant (share) read or read/write access to a record to another user, group, or role.  

 

Manual shares can also be created programmatically using apex or apex triggers. Use caution while programmatically creating manual shares via apex as you can easily cause performance degradation if you are adding a large number of shares to a single object.  

 

1. **Territory Based Sharing (Territory Management)** 

Territory Management is a larger functionality in Salesforce that allows for creating territory groupings. Users and Accounts can then be assigned as members of a territory. Once a user has been added to a territory the user then is granted access to that account. You have the ability to specify for each territory is the users should gain read or read/write access to the account records. 

 

Additionally you can also choose is the users granted access to the accounts are granted access to related opportunities and/or cases to those accounts. 

 

For more information about territory management see 

 

**Territory Management Decision Guide** 

[https://developer.salesforce.com/page/Territory_Management_Decision_Guide](https://developer.salesforce.com/page/Territory_Management_Decision_Guide) 

 

**Territory Management Data Model** 

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_erd_territory2.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_erd_territory2.htm) 

 

**Territory Management Developers Guide** 

[https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/Territory2.htm](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/Territory2.htm)  

 

 

 

**Special Permissions That Affect Sharing** 

There are special permissions that can be set via profiles and permission sets that can override the Salesforce sharing settings.  

 

These permission exist in two types: 

 

**System / Administrative** 

Under the system permissions you will find the permissions "view all data" and “modify all data”. If a user has these permissions set, the user will be able to view and/or edit all records for all objects regardless of the sharing settings set.  

 

Be very careful when setting this permission, as this permission will open up access to all of your data to a single user. Even if a field is set as read-only on the object profile permissions, the user will still have full access to the object as well.  

 

**Object Level** 

In addition to the ability to grant global read or edit access to all records across all objects, you also can set read or edit access for all records for only a single object. At the object level if you set the permissions "view all" or “modify all” then all users in the profile or permission set will be able to view and/or edit all records within that object regardless of the sharing settings. 

 

4. How to Write Good Unit Tests 

(Source: [https://developer.salesforce.com/page/How_to_Write_Good_Unit_Tests](https://developer.salesforce.com/page/How_to_Write_Good_Unit_Tests))

    20. Abstract

This article shows how to craft good unit tests. It explores the proper structure of unit tests, the code scenarios that unit tests should cover, and the properties of well-written unit tests. There are plenty of code samples interspersed throughout the article to demonstrate and help illustrate the concepts.

    21. Unit Test Introduction

A unit test is code that exercises a specific portion of your codebase in a particular context. Typically, each unit test sends a specific input to a method and verifies that the method returns the expected value, or takes the expected action. Unit tests prove that the code you are testing does in fact do what you expect it to do.

The Force.com platform requires that at least 75% of the Apex Code in an org be executed via unit tests in order to deploy the code to production. You shouldn’t consider 75% code coverage to be an end-goal though. Instead, you should strive to increase the state coverage of your unit tests. Code has many more possible states than it has lines of code. For example, the following method has 4,294,967,296 different states:

double getFraction(Integer a){ return 1/a; }

Clearly, you wouldn’t want to test all of the different states for this program. Instead, you should probably test a few different inputs for this method, even if it means that you will have achieved 100% code coverage several times over.

Three different states that you might consider testing are a positive input, a negative input and a 0 input. Testing with a positive input, and with a negative input will behave as expected. Testing with a 0 input however will yield a surprise System.MathException. This is just one example of why it makes sense to focus on testing the different states of your code instead of focusing on just the 75% code coverage requirement.

    22. The Value of Unit Tests

One of the most valuable benefits of unit tests is that they give you confidence that your code works as you expect it to work. Unit tests give you the confidence to do long-term development because with unit tests in place, you know that your foundation code is dependable. Unit tests give you the confidence to refactor your code to make it cleaner and more efficient.

Unit tests also save you time because unit tests help prevent regressions from being introduced and released. Once a bug is found, you can write a unit test for it, you can fix the bug, and the bug can never make it to production again because the unit tests will catch it in the future.

Another advantage is that unit tests provide excellent implicit documentation because they show exactly how the code is designed to be used.

Lastly Salesforce.com uses unit tests to ensure that their releases don’t break customer code. The more tests you write, the better Salesforce.com is able to ensure they are not breaking customer customizations. Before and after every release Salesforce.com will run all test code written by their customers. Then after the release will run the code again. They then make sure that all tests had the same outcome before and after the release. That is why it is in your benefit to write good tests that cover as much of your code as possible.

Many developers have discovered these advantages. Some developers, including me, believe so strongly in the value of unit tests that we write our tests first and our production code second. I’m going to show you an example of this test-first development practice a little later on in the article.

    23. Unit Test Structure

Let’s take a look at how unit tests are best structured. All unit tests should follow the same basic structure.

A unit test should:

* Set up all conditions for testing.

* Call the method (or Trigger) being tested.

* Verify that the results are correct.

* Clean up modified records. (Not really necessary on Force.com.) 

Let’s discuss each of these in turn.

        5. Set Up All Conditions for Testing

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

        6. Call the method (or Trigger) being tested

Once you have set up the appropriate input data, you still need to execute your code. If you are testing a method, then you will call the method directly. In this case, we’re testing a Trigger, so we’ll need to perform the action that causes the trigger to execute. In our sample, that means that we will need to insert the Opportunity:

insert o;

        7. Verify the results are correct

Verifying that your code works as you expect it to work is the most important part of unit testing. It’s also one of the things that Force.com developers commonly neglect. Unit tests that do not verify the results of the code aren’t true unit tests. They are commonly referred to as smoke tests, which aren’t nearly as effective or informative as true unit tests.

A good way to tell if unit tests are properly verifying results is to look for liberal use of the System.assert() methods. If there aren’t any System.assert() method calls, then the tests aren’t verifying results properly. And, no, System.assert(true); doesn’t count.

Sample verification code for this trigger might look like this:

oAccount = [SELECT Name, Most_Recently_Created_Opportunity_Name__c

     FROM Account

     WHERE Id = :oAccount.Id];

System.assertEquals('My Oppty', oAccount.Most_Recently_Created_Opportunity_Name__c);

Notice that this unit testing code explicitly verifies that the trigger performed the action that we expected.

        8. Clean up (is Easy!)

Cleaning up after unit tests is easy, because there’s nothing to do! Actions performed on records inside of a unit test are not committed to the database. This means that we can insert, delete, and modify records without having to write any code that will clean up our changes. Even the results of trigger executions that affect existing data are not committed!

        9. Where to put tests?

Your Trigger files can never contain code other than the Trigger definition, so Trigger unit tests must always be located in a separate class file.

Unit tests for your classes are also required to be in a separate class. The most important reason for this is that by separating your class implementation and your unit tests, you will automatically be prevented from testing private methods and private properties. You shouldn’t test private methods and private properties because doing so will cause your unit tests to become a barrier to refactoring. With your classes and unit tests separated in to different files, you will always have the option to change the internal implementation of your classes should the need arise. If you ever do find yourself compelled to test a private or protected method, this is probably a strong indication that the method should be refactored in to its own stand-alone class.

As an additional incentive, this best practice of separating unit tests and classes also allows you to take advantage of the @isTest annotation. The code inside of an @isTest annotated file does not count against the overall Apex code size limitation for your org.

        10. Putting it all together

Here's the complete unit test for the trigger, which it's put in UpdateParentAccountWithOpportunityName_Test.cls.

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

Note the use of the @isTest annotation, as well as the general structure of the test - first the setup, then the action, and finally the verification.

    24. What to Test 

In the previous section, we discussed how unit tests should be structured, and where they should be located. In this section, we will discuss what types of scenarios you should test.

Broadly speaking, you should test your custom business logic. How thoroughly you test that business logic will probably vary depending on specific situations. On one end of the spectrum, you might choose to implement just a few tests that only cover the code paths that you believe are most likely to contain a bug. On the other end of the spectrum, you might choose to implement a large suite of unit tests that are incredibly thorough and test a wide variety of scenarios. Wherever a given project falls on that spectrum, you should be sure to write unit tests that verify your code behaves as expected in "normal" scenarios as well as in more "unexpected" scenarios, like boundary conditions or error conditions.

In order to give you a better idea of the kinds of things that you should be testing, I'll walk through the process of writing unit tests for an implementation of a Stack data structure that can be used to store Strings.

        11. Stack Interface

The first thing that I need to do is define the publicly accessible methods for our StringStack class:

public class StringStack {

    public void push(String s) { }

    public String pop() { return null; }

    public String peak() { return null; }

    public Boolean isEmpty() { return true; }

}

You’ll notice that I haven’t written any real implementation code for these method definitions. That’s because I’m going to use Test Driven Development techniques in this example. In Test Driven Development, unit tests are written before any real implementation code is written. I’ve found that writing my unit tests first helps me better understand how clients of my code are going to use it.

        12. Testing Normal Conditions

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

![image alt text](image_0.jpg)

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

![image alt text](image_1.jpg)

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

The  code passes this test too, so we are pretty confident that it handles the "normal" conditions pretty easily. Next, let’s test some of the more "unexpected" scenarios.

        13. Testing Unexpected Conditions

There are many scenarios that your code shouldn’t encounter. However, you can’t trust that clients of your code will always do the right thing, so you have to make sure that the code will still handle these unexpected scenarios appropriately. Let’s look at a few examples:

            1. Bad Input Values

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

            2. Boundary Conditions

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

            3. Regression Tests

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

    25. Making use of Test.isRunningTest() method

There are some situations, when you will just not be able to test some code in a normal matter - eg. you are using objects that cannot be inserted in tests, or doing some http requests. In such case, if you think there is no other option, consider using Test.isRunningTest(). This static method allows you to discover whether the code was run from test method. Therefore, for example you might:

* return hard-coded String instead of calling http request and parsing the body

* return a fixed array of objects from a method 

It might be actually used as a basic introduction to mocks, which are very widespread in other languages.

    26. Force.com-specific Testing

In addition to verifying that your code executes properly in normal scenarios, testing edge cases and preventing regressions, you may find that you need to test certain Force.com-specific aspects of your application as well. Things like Apex Callouts, SOSL queries, Governor Limits, etc. To learn more about these topics you’ll want to read these articles:

<table>
  <tr>
    <td>Document Name</td>
    <td>Location</td>
  </tr>
  <tr>
    <td>Testing Apex Callouts</td>
    <td>https://developer.salesforce.com/index.php?title=Virtual_Callout_Testing</td>
  </tr>
  <tr>
    <td>Testing SOSL</td>
    <td>http://www.salesforce.com/us/developer/docs/apexcode/index_Left.htm#StartTopic=Content%2Fapex_testing_SOSL.htm|SkinName=webhelp</td>
  </tr>
  <tr>
    <td>Verifying Large DataSets</td>
    <td>https://developer.salesforce.com/page/Apex_Code_Best_Practices#Best_Practice_.239:_Writing_Test_Methods_to_Verify_Large_Datasets</td>
  </tr>
  <tr>
    <td>Testing with RunAs</td>
    <td>http://www.salesforce.com/us/developer/docs/apexcode/index_Left.htm#StartTopic=Content%2Fapex_testing_tools_runas.htm|SkinName=webhelp</td>
  </tr>
</table>


    27. Properties of Well-Written Unit Tests

Well-written unit tests are thorough, repeatable, and independent. Let’s examine each of these properties in turn.

        14. Thorough

The most important aspect of well-written unit tests is that your unit tests must be thorough. The Force.com platform requires 75% code coverage, but this is a minimum and should not be your end goal. You should only be satisfied with your unit tests when you’re confident that your unit tests thoroughly verify that your code works as we expect it to work. To do this, your tests must use the various System.assert() calls. Unit tests should exercise the expected as well as the unexpected conditions in your code. Special attention should be paid to areas of code that are particularly likely to break.

        15. Repeatable

Every one of your unit tests should be able to be run repeatedly and continue to produce the same results, regardless of the environment in which the tests are being run. When your unit tests can be run in a repeatable and consistent manner, you can trust that your unit tests will only detect and alert you to real bugs, and not environmental differences.

One common mistake that might prevent you from writing repeatable unit tests is relying upon hard-coded information, like server urls. Your unit tests should not rely on hard-coded server urls because unit tests must be written in either a sandbox org or in a developer org. Sandbox orgs will always have different urls than the production orgs will have, and developer orgs will usually have different urls than the production org will have. If you hard-code the server urls, the unit tests may fail when you attempt to move your code to production. Another common mistake that might prevent your unit tests from being repeatable is relying upon hard-coded record ids. Record ids are entirely org-specific, and can not be used outside of a given org. Instead of relying upon hard-coded record ids, unit tests should create their own data, as we described in the Set Up All Conditions for Testing section.

        16. Independent

Your unit tests should only test one aspect of your code at a time, so that it is easy to understand the purpose of each unit test. Properly written, and well-decomposed unit tests are an excellent source of documentation. This may mean that you will need to write multiple unit tests in order to fully exercise one method. I’ve shown you one example of this in the Testing Normal Conditions section.

Also, keep in mind that each of your unit tests must be independent from your other unit tests. Unit tests do not alter the state of the Force.com database, and they are not guaranteed to run in a particular order, so you cannot rely upon one unit test to do the setup work for another unit test.

    28. Summary: Top 10 Best Practices (in no order)

(Source: [http://blog.force365.com/2014/09/19/apex-unit-test-best-practice/](http://blog.force365.com/2014/09/19/apex-unit-test-best-practice/))

        17. Test Driven Development

Follow Test Driven Development practice wherever possible. There is no excuse for writing unit tests after the functional code, such an approach is indicative of a flawed development process or lax standards. It’s never a good idea to estimate or deliver functional code without unit tests – the client won’t appreciate an unexpected phase of work at the point of deployment, not to mention the pressure this approach puts on system testing.

        18. Code Quality

Ensure unit tests are written to cover as many logical test cases as possible, code coverage is a welcome by-product but should always be a secondary concern. Developers who view unit tests as a necessary evil, or worse, need to be educated in the value of unit tests (code quality, regression testing, early identification of logical errors etc. etc.).

        19. Test Code Structure

For some time now I’ve adopted a Test Suite, Test Helper pattern. A suite class groups tests related to a functional area. A test helper class creates test data for a primary object such as Account (i.e. AccountTestHelper.cls), secondary objects such as price book entry would be created within the product test helper class. The suite concept provides a logical and predictable structure, the helper concept emphasises that test data creation should be centralised.

        20. Test Code Structure (continue)

. Put bulk tests in a separate class e.g. AccountTriggerBulkTestSuite.cls (in addition to AccountTriggerTestSuite.cls). Bulk tests can take a long time to complete – this can be really frustrating when debugging test failures – particularly in production.

        21. Test Code Structure (over and over)

Ensure test classes contain a limited number of test methods. I tend to limit this to 10. As with point 4, this relates to test execution time, individual methods can’t be selectively executed – the smallest unit of execution is the class.

        22. SeeAllData

Always use SeeAllData=true by exception and at the test method level only. Legacy test code related to pricebooks that historically required this can now be refactored to use Test.getStandardPricebookId(). Also, set the [Independent Auto-Number Sequence] flag to avoid gaps in auto number sequences through the creation of transient test data.

        23. Test Case Types

As the Apex Language reference proposes, write unit tests for the following test case types.

* **Positive Behaviour** – logical tests that ensure the code behaves as expected and provides successful positive outcomes

* **Negative Behaviour** – logical tests for code behaviour where parameters are missing, or records do not adhere to defined criteria – does the code protect the integrity of unaffected records – does the runtime exception handling function as expected

* **Bulk** – trigger related tests primarily – how the code behaves with a batch of 200 records – mix the batch composition to stress the code against governor limits

* **Restricted User** – test relevant combinations of user role and profile – this test case type is prone to failure through sharing model adjustments – triggers should delegate processing to handler classes that have the "with sharing" modifier

        24. Debugging

Always use the syntax below for debug statements within code (test and non-test code). An efficient practice is to add sensible outputs whilst writing the code. This approach avoids a code update or re-deployment to add debug statements during error diagnostics. Note – in such cases Checkpoints could be a better approach anyway – particularly in production. The use of the ERROR logging level enables a restrictive log filter to be applied such a clear debug log is produced and max log size truncation is avoided – note, log filters can also have a positive impact on transaction execution time.

System.debug(LoggingLevel.ERROR, 'my message');

        25.  Commenting

Always comment test methods verbosely to ensure the test case intent is clear and that the test code can be mapped to the related non-test code. Test classes should be fully self documenting and be viewed as the primary enabler for the future maintenance of the non-test code.

        26. Maintenance

Test code is highly dependent on the environment state. Any configuration change can require test code to be updated; this could be a new mandatory custom field or a sharing model adjustment. In many cases the resultant unit test failure state is not encountered until the next deployment to production, which can’t proceed until the tests are fixed. This scenario will be familiar to many people. The mitigation requires the local administrator to understand the risk, frequently run the full set of unit tests and to manage the test code update cycle proactively.
