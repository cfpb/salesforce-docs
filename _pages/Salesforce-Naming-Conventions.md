##Salesforce Naming Conventions

Naming conventions make the application easier to read and maintain. The naming standards documented here cover customization and configuration areas of salesforce. Regardless of the context in which names are used, Names should be descriptive, concrete, and specific rather than general. Having a generalized name such as ProductLine can have different semantics depending upon the context. It’s better to use something the business identifies with and that will not create a potential conflict with other applications; e.g., ReverseMortgage.

### 1. Custom Objects
#### Rules for Naming
Custom object names should be unique, beginning with an uppercase letter. Whole words should be used and use of acronyms and abbreviations should be limited. The object name should be singular (e.g. Review vs. Reviews, or OrderItem vs. Order Items) and should not include any underscores "_". The object label when at all possible should be similar to that of the object name since giving the label a different name than the object will make the object hard to find in some place within Salesforce.

#### Exceptions
Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA. Added an underscore is acceptable if you are prefixing the object name to denote it is part of an application. For example: OrderApplication_Order and OrderApplication_OrderItem. Notice that OrderItem does not have any underscores.

#### Demonstrative Example
The following are examples of custom object naming that should _not_ be used 
The following are examples of custom object naming that should _not_ be used 

|Object  Name | Reason |
|-------------|:--------|
```CustAsset```| Abbreviations have made this object name hard to understand 
```Orders``` | Object names should always be singular. 
```Order_Item``` | Object names should not have underscores. 

The following are examples of the naming convention that will be used:

|Object  Name | Reason |
|-------------|:--------|
```CustomerAsset``` | Removing ambiguity from the name will improve readability and maintainability 
```Order``` |  Making object names singular will ensure a standard naming convention across all objects. 
```OrderItem``` | Removing all underscores will help keep a standard naming convention as many times there are words that some may separate into two words and other may not. For example: ```Zipcode``` vs. ```Zip Code```.

____

### 2. Custom Fields

##### Rules for Naming
Custom object names should be unique, beginning with an uppercase letter. Whole words should be used and use of acronyms and abbreviations should be limited. Similar to custom object naming, custom fields should not contain any underscores "_". When creating custom fields always complete the “Description” field unless the field name would be completely obvious to someone not familiar to the application as to what is the purpose of the field.

##### Exceptions

Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.

##### Demonstrative Example

The following are examples of custom field naming that should not be used 

| Custom Field Name |  Reason |
|-------------------|:--------|
```C``` | Ambiguous names will cause confusion. Description was not completed. 
```Zip_Code``` | Field names should not have underscores. 

The following are examples of the naming convention that will be used 

| Custom Field Name | Reason 
|-------------------|:--------|
```CountryCode``` | A succinct description of the object using whole words. Description is not required since the name is a commonly understood term. 
```ZipCode``` | Removing all underscores will help keep a standard naming convention as many times there are words that some may separate into two words and other may not. Description is not required since the name is a commonly understood term. 
```CompletionDate``` | Date that the order process was completed. Should only be set once payment is received and order was fulfilled. Even though the name seems to make sense, there are business rules that need to be explained, and as such, a longer description was needed.

____

### 3. Validation Rules

#### Rules for Naming

Validation rule names should be unique, beginning with an uppercase letter. Whole words should be used and use of acronyms and abbreviations should be limited. e.g. 

&lt;FIELD&gt;  &lt;RULE&gt;  &lt;OPTIONAL DEPENDENCY&gt;  

```Postal Code Required (Suburb)``` 

The above example shows that Postal Code is required dependent on values in the Suburb field. The exact rule definition is in the detail but keeping this format helps keeps the naming as intuitive as possible without being too restrictive.

#### Exceptions

Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA. As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read.

#### Demonstrative Example

The following are examples of validation rule naming that should **not** be used:

| Validation Rule Name | Reason |
|----------------------|:-------|
```Validate Address``` | Superfluous use of the word validate and does not allow future additional validation rules to easily distinguish what the rule is checking 

The following are examples of the naming convention that will be used:

| Validation Rule Name | Reason |
|----------------------|:-------|
```Street Address < 60 chars``` | Field and rule clearly identified
```Zipcode not blank``` | ibid
```Occupation required``` | ibid
``` Zipcode required (Suburb)``` | FIELD, RULE, and DEPENDENCY clearly identified

____

### 4. Workflow Rules

#### Rules for Naming

Workflow rule names will follow the following convention: 

|Attribute | Naming Convention |
|----------|:----------------|
|Workflow Rule Name | Note that this is not the action or actions being performed but the original event that fired the workflow rule. This allows the workflow actions to change over time. Including the salesforce object in the rule name is unnecessary as there is a standard field in the list view that can show this and filter on it. Whole words should be used and use of acronyms and abbreviations should be limited.|
|Description | A full description of the rule and what actions it performs|

#### Exceptions

As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read

#### Demonstrative Example

The following are examples of workflow rule naming that should not be used:

|Attribute | Example | Reason| 
|----------|:---------|--------|
|Workflow Rule Name | Contact – Send Email and Update Inactive Flag | Name is too long and describes the actions performed as part of the rule that may change over time making the name potentially confusing in the future.| |Description | Sends an email | Not enough detail to be immediately clear what the workflow rule actions. Who is the email to? What about the field update?| 

 The following are examples of the naming convention that will be used: 

| Attribute | Example | Reason |
|-----------|:---------|:-------|
|Workflow Rule Name | Date of Death Changed | Describes the event that will fire the rule in a succinct way |
|Description | Sends an email to the Deceased Customer public group and updates the inactive flag of the contact for batch processing | Provides a clear and brief description of the intention of the actions performed. The description can be more easily updated and migrated as changes are made over time|

____

### 5. Field Updates

#### Rules for Naming

Field update names will follow the following convention: 

|Attribute | Naming Convention |
|-----------|:---------|
|Field Update Name | Set &lt;NAME OF FIELD&gt; - &lt;VALUE&gt; Whole words should be used and use of acronyms and abbreviations should be limited. By using this convention the field update can be reused across workflow rules and approval processes and it is clear to the reviewer what action, field and value will be used. 
|Description | A full description of the field update including if other processes are dependent on the value

#### Exceptions

As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read

#### Demonstrative Example

The following are examples of field update naming that should not be used :

|Attribute | Example | Reason |
|----------|:--------|--------|
|Field Update Name | Customer Date of Death | This describes the rule that fires the field update but does not tell me which field is updated and to what value |
|Description | Updates the customer inactive flag | Doesn’t tell the reviewer at first glance what value is used and if this flag is used in other processes| 

The following are examples of the naming convention that will be used :

|Attribute | Example | Reason |
|----------|:--------|--------|
|Field Update Name | Set Customer Inactive Flag – False | Describes the field being updated and what value will be used when updating the field 
| Description | Updates the inactive flag on the customer record which will be used by batch apex for processing | Briefly describes interdependencies that may rely on this action being performed |


### 6. Email Alerts

#### Rules for Naming

Email alert names will follow the following convention: 

|Attribute | Naming Convention 
|----------|:-----------------
|Email Alert Description | Email &lt;Description of Recipient&gt; - &lt;Email Template Used&gt; Whole words should be used and use of acronyms and abbreviations should be limited. By using this convention the email alert can be reused across workflow rules and approval processes and it is clear to the reviewer who the email will be sent to.|

#### Exceptions

As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read

#### Demonstrative Example

The following are examples of email alert naming that should not be used:

|Attribute | Example | Reason 
|----------|:--------|-------
|Email Alert Description | Inform team of change | Mixed case not used and it is unclear where the email will be sent 

The following are examples of the naming convention that will be used :

|Attribute | Example | Reason 
|----------|:--------|------- 
Email Alert Description  |Email Deceased Customer Team – New Deceased Customer | Describes who is emailed and which template is used

____

### 7. Approval Processes

#### Rules for Naming

Approval process names will follow the following convention: 

|Attribute | Naming Convention 
|----------|:----------------
|Process Name | &lt;Event that fired the approval&gt; Note that this is not the action or actions being performed but the original event that will trigger the entry criteria. This allows the approval actions to change over time. <br/>Including the salesforce object in the rule name is unnecessary as there is a standard field in the list view that can show this and filter on it. Whole words should be used and use of acronyms and abbreviations should be limited.
|Description | A full description of the rule and what actions it performs

#### Exceptions

As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read

#### Demonstrative Example

The following are examples of approval process naming that should not be used :

Approval Process Name | Reason 
----------------------|:----------
|Comp | Abbreviations can cause confusion. Whole words should be used. 
|Send Email On Reject | Actions performed in the approval process should not be used in the parent process name 

The following are examples of the naming convention that will be used :

Approval Process Name | Reason 
----------------------|:---------- 
| Conflict Completed | Brief description of the entry criteria indicate a clear intention of when the process will be used

____

### 8. Approval Process Steps

#### Rules for Naming

Approval process step names will follow the following convention: 

Attribute | Naming Convention 
----------|:---------- 
Step Name | &lt;Decision Outcome&gt; - &lt;User Friendly Description&gt;
Description | A full description of the step including what it does and the intended actions that will be performed (e.g. who will it be assigned to)

#### Exceptions

As there is an upper limit for the number of characters in the name field the use of abbreviations will be permitted if by including them the name becomes easier to read

#### Demonstrative Example

The following are examples of approval process step naming that should not be used :

Approval Process Step Name | Reason 
---------------------------|:-------
Step 1 | This is not descriptive enough as it will be displayed in the approval related list to users. Does not provide what was evaluated. 
Complex Approval – Step 1 | More descriptive but does not provide users with a clear enough picture of what was evaluated 

The following are examples of the naming convention that will be used:

Approval Process Step Name | Reason 
---------------------------|:-------
Auto Approved – Value within personal limit | The approval step becomes self documenting showing the administrator and user the result of the approval step
Auto Rejected – Value exceeds company policy | The approval step becomes self documenting showing the administrator and user the result of the approval step
Approval – Sent to Manager | The approval step becomes self documenting showing the administrator and user the result of the approval step 
Approval – Sent to Legal | The approval step becomes self documenting showing the administrator and user the result of the approval step

____

### 9. Visualforce Pages

#### Rules for Naming

Visualforce page names and labels should be unique, beginning with an uppercase letter. It should not contain underscores or spaces. The words should be concatenated with Initial uppercase and subsequent internal words capitalized. Whole words should be used and use of acronyms and abbreviations should be limited.

#### Exceptions

Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL.

#### Demonstrative Example

The following are examples of Visualforce Page naming that should not be used:

Visualforce Page Name | Reason 
----------------------|:-------
Override_Customer_View | Underscores should not be used 
Custoverrideview | Name and Label becomes hard to read without capitalization 

The following are examples of the naming convention that will be used :

Visualforce Page Name | Reason 
----------------------|:-------
CustomerView | Clearly defined and succinct name 
MailFaxRequest | Clearly defined and succinct name

____

### 10. Apex Classes

#### Rules for Naming

Class names should be unique, beginning with an uppercase letter. It should not contain underscores or spaces. The words should be concatenated with Initial uppercase and subsequent internal words capitalized. Whole words should be used and use of acronyms and abbreviations should be limited. Apex classes that are custom controller classes should be suffixed with Controller Apex classes that are controller extensions should be suffixed with XController, where X is the name of the Visualforce page that is extended. That allows for easy searching of controllers related to Visualforce pages.

#### Exceptions

Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.

#### Demonstrative Example

The following are examples of Apex class naming that should not be used :
     
Class Name | Reason   
-----------|:------  
FHACustomer | Using acronyms should be avoided as they are not mnemonic    
GrtBgClass | Whole words should be used in place of shortened versions  GreatBigClass      
addresshandler | Class does not begin with an uppercase letter     
Address_Handler | Underscores should be avoided   

The following are examples of the naming convention that will be used:

Class Name | Reason 
-----------|:------
Customer | Full word used to describe the class and starts with uppercase 
AddressHandler | Multiple words concatenated with subsequent words capitalized
MailFaxController | Controller Extension for the Mail_Fax__c object
CustomerController | Customer controller for the customer object

____

### 11. Apex Batch, Schedulable, and Queueable Classes

#### Rules for Naming

Class names should be unique, beginning with an uppercase letter. It should not contain underscores or spaces. The words should be concatenated with Initial uppercase and subsequent internal words capitalized. Whole words should be used and use of acronyms and abbreviations should be limited. Apex classes that are batch classes should be suffixed with _Batch Apex classes that are Scheduleable classes should be suffixed with _Schedule Apex classes that are Queuable classes should be suffixed with _Queueable

#### Exceptions

Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.

#### Demonstrative Example

The following are examples of Apex batch, scheduleable, and queueable class naming that should not be used 

Class Name | Reason 
-----------|:------
GrtBgClass | Whole words should be used in place of shortened versions GreatBigClass and the appropriate suffix should be used. 
contactbatch | Class does not begin with an uppercase letter and an underscore should always precede the suffix. 
Address_Update_Batch | Underscores should be avoided other than for the suffix 

The following are examples of the naming convention that will be used 

Class Name | Reason
-----------|:------
RoleExpiry_Batch | Multiple words concatenated with subsequent words capitalized. Suffixed with _Batch denoting that this is a batch apex class. RoleExpiry_Schedule | Multiple words concatenated with subsequent words capitalized. Suffixed with _Schedule denoting that this is a scheduleable apex class. 
RoleExpiry_Queueable | Multiple words concatenated with subsequent words capitalized. Suffixed with _Queueable denoting that this is a queueable apex class.

____

### 12. Apex Triggers

#### Rules for Naming
Triggers should always be named using the format [object Name][Operation]Trigger OR [Object Name]Trigger for triggers that include all operations for that object. For example: AccountInsertTrigger, AccountUpdateTrigger, OrderInsertTrigger. There should only be one trigger per operation per object. It is strongly recommended to include only a single trigger with all operations inside that trigger per object.

#### Exceptions

None

#### Demonstrative Example

The following are examples of trigger naming naming that should not be used 

Validation Rule Name | Reason 
-----------|:------
UpdateAccountAddresses | The object name should always be before the operation in the name. 
AccountUpdateContacts | Is specific to a business function and would allow for other update triggers to be created for the same object. 

The following are examples of the naming convention that will be used 

Trigger Name | Reason 
-----------|:------
AccountUpdateTrigger | Generic trigger that performs only update operations. AccountInsertTrigger | Generic trigger that performs only insert operations AccountTrigger | Generic trigger that performs insert,update, and delete operations. This would be the only trigger for the account object.

____

### 13. Apex Test Classes

#### Rules for Naming

Test class names should be unique, beginning with an uppercase letter. It should not contain spaces. The words should be concatenated with Initial uppercase and subsequent internal words capitalized. Whole words should be used and use of acronyms and abbreviations should be limited. The test class will use the convention Test. This keeps the alphabetical order of the classes intact.

#### Exceptions

Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.

#### Demonstrative Example

The following are examples of Apex class naming that should not be used Class Name Reason TESTCustomerManagement Test classes should not have "TEST" in the prefix, but rather have “Test” in the suffix. The following are examples of the naming convention that will be used 

Class Name | Reason 
-----------|:------
CustomerManagementTest | Test class for the CustomerManagement Apex class. Will be listed alphabetically under the class being tested.

____

### 14. Apex Methods

#### Rules for Naming

Methods should be verbs, in mixed case with the first letter lowercase, with the first letter of each internal word capitalized. Whole words should be used and use of acronyms and abbreviations should be limited.

#### Exceptions

Widely used and commonly understood acronyms and abbreviations can be used instead of the long form. For example HTTP or URL or ACMA.

#### Demonstrative Example
The following are examples of Apex method naming that should not be used 

Method Name | Reason 
-----------|:------
handleCalculation() | What is being handled?! 
performServices() | Perform what services? 
dealWithInput() | How exactly is the input being dealt with? 
NTInQ1() | Cannot determine from the name what the function does 

The following are examples of the naming convention that will be used 

Method Name | Reason 
-----------|:------
ammortizationCalculation() | Describes what calculation is performed repaginateDocument() | Describes the service being performed getEmployeeDetail() | Describes what is being done 
numberOfTransactionsInQ1() | Longer names are better if they are needed for clarity

____

### 15. Apex Variables

#### Rules for Naming
Variables should be in mixed case with a lowercase first letter. Internal words start with capital letters. Variable names should be short yet meaningful. The choice of a variable name should be mnemonic— that is, designed to indicate to the casual observer the intent of its use. One-character variable names should be avoided except for temporary "throwaway" variables. Common names for temporary variables are i, j, k,m, and n for integers; c, d, and e for characters.

#### Exceptions
None

#### Demonstrative Example

The following are examples of Apex variable naming that should not be used 

Variable Name | Reason
-----------|:------
 x = x – y | Variable names are ambiguous 

 The following are examples of the naming convention that will be used 

 Variable Name | Reason 
 -----------|:------
currentBalance = lastBalance - lastPayment | Unambiguous names that have a clear meaning


____

### 16. Apex Constants

#### Rules for Naming
The names of variables declared class constants should be all uppercase with words separated by underscores ("_"). Common constants used across the application should be declared in the GlobalConstants class (see section 7.6) Constant scope should be kept to the minimal required. Private class attributes are preferred to publicly defined constants.

#### Exceptions
None

#### Demonstrative Example

The following are examples of Apex constant naming that should not be used 

Class Name | Reason 
-----------|:------
maxCharacters | Indistinguishable from a variable name 

The following are examples of the naming convention that will be used 

Class Name | Reason 
-----------|:------
MAX_CHARACTERS | Uppercase letters help the reviewer determine that it is a constant

____

### 17. Apex Type Names

#### Rules for Naming

Type names should use an uppercase first letter. This follows the Java naming conventions. This is to ensure that the type names are not similar to the variable names that immediately proceed them.

#### Exceptions
None

#### Demonstrative Example

The following are examples of Apex type naming that should not be used 

Type Name | Reason 
-----------|:------
map Contacts | "map", “id”, and “string” do not start with an uppercase letter. 
String Contact | “string” does not start with an uppercase letter. 

The following are examples of the naming convention that will be used 

Type Name | Reason 
-----------|:------
Map Contacts | Starts with an uppercase letter String Contact Starts with an uppercase letter

____

### 18. Public Groups

Public Groups and Queues are very similar in how they are used within Salesforce and as such should follow the same naming conventions.

_What is a Public Group?_
Public groups in Salesforce are a security mechanism in Salesforce that allows you to “group” users together that need common access to something in Salesforce.

Instead of manually assigned users to the “thing” you want them to have access, you just add or remove the user from the group. When you want to remove access from all users in the group to the “thing”, you just remove the group from having access.

_Examples of Types of Access_
- Granting access to a listview on an object to a group of users
- Using criteria based sharing to grant access to a set of users who are in a group
- Sharing access to a record to a set of users who are in a group

#### Rules for Naming

Business users will view public group labels while viewing the users and groups a record is shared with. Group labels will need to make sense to business users pertaining to their business process. Administrators will need to be able to easily sort public groups when adding/removing users from groups. Group name will need to make sense to administrators pertaining to specific applications.

- Always prefix the group name with the application. ie: “Mosaic_Complaints”. This will allow easy sorting of the groups by the administrator by application.
- Give the label of the group the same postfix name as what was given to the name. ie: “Complaints”.  This allows for business users to easily associate the group with a business process, but also makes it easy for a system administrator to match a group name to the label in the application. 

#### Exceptions
None

#### Demonstrative Example

![Create a new Group](/img/group_naming_example.png)

![Public Groups](/img/group_naming_example_1.png)
____

### 19. Queues

Public Groups and Queues are very similar in how they are used within Salesforce and as such should follow the same naming conventions.

_What is a Queue?_
Queues are similar to public groups in that they allow you to assign one or more users as members of the queue. Where queues differ is that when you setup a queue, you also associate one or more Salesforce objects with the queue. Once you associate a Salesforce object with a queue, you can then set the queue as the owner of a record of an associated object. 


_Examples of Types of Access_
-Queue granted as owner of a record grants all users read access to the record 
-Using criteria based sharing to grant access to a set of users who are in a queue

#### Rules for Naming

Business users will view queue labels while working with list views and viewing record owners. Queue labels will need to make sense to business users pertaining to their business process. Administrators will need to be able to easily sort queues when adding/removing users from the queues. Queue names will need to make sense to administrators pertaining to specific applications.

-Always prefix the queue with the application. ie: “Mosaic_Complaints”. This will allow easy sorting of the queues by the administrator by application.
-Give the label of the queue the same postfix name as what was given to the name. ie: “Complaints”.  This allows for business users to easily associate the queue with a business process, but also makes it easy for a system administrator to match a queue name to the label in the application. 

#### Exceptions
None

#### Demonstrative Example

![Create a new Group](/img/group_naming_example.png)

![Public Groups](/img/group_naming_example_1.png)
