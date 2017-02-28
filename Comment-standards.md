###Source Code and Configuration Management

####Comment Standards

All methods should begin with a brief comment describing the functional characteristics of the method (what it does). This description should not describe the implementation details (how it does it) because these often change over time, resulting in unnecessary comment maintenance work, or worse yet erroneous comments. The code itself and any necessary inline or local comments will follow the standards as defined by the [SalesforceFoundation](https://github.com/SalesforceFoundation/ApexDoc#documenting-class-files):

#####Class Comments

Located in the lines above the class declaration. The special tokens are all optional.

|token | description|
|-------------|:--------|
|@author | the author of the class|
|@date | the date the class was first implemented|
|@group | a group to display this class under, in the menu hierarchy|
|@group-content | a relative path to a static html file that provides content about the group|
|@description | one or more lines that provide an overview of the class|

Example

```
/**
 * @author Salesforce.com Foundation
 * @date 2014
 *
 * @group Accounts
 * @group-content ../../ApexDocContent/Accounts.htm
 *
 * @description Trigger Handler on Accounts that handles ensuring the correct system flags are set on
 * our special accounts (Household, One-to-One), and also detects changes on Household Account that requires
 * name updating.
 */
public with sharing class ACCT_Accounts_TDTM extends TDTM_Runnable {
```

#####Property Comments

Located in the lines above a property. The special tokens are all optional.

|token | description|
|-------------|:--------|
|@description | one or more lines that describe the property|

Example

```    
    /************************************************************************** *****************************
     * @description specifies whether state and country picklists are enabled in this org.
     * returns true if enabled.
     */
    public static Boolean isStateCountryPicklistsEnabled {
        get {
```

#####Method Comments

In order for ApexDoc to identify class methods, the method line must contain an explicit scope (global, public, private, testMethod, webService). The comment block is located in the lines above a method. The special tokens are all optional.

|token | description|
|-------------|:--------|
|@description | one or more lines that provide an overview of the method|
|@param _param name_ | a description of what the parameter does|
|@return | a description of the return value from the method|
|@example | Example code usage. This will be wrapped in  tags to preserve whitespace|

Example

```
    /************************************************************************** *****************************
     * @description Returns field describe data
     * @param objectName the name of the object to look up
     * @param fieldName the name of the field to look up
     * @return the describe field result for the given field
     * @example
     * Account a = new Account();
     */
    public static Schema.DescribeFieldResult getFieldDescribe(String objectName, String fieldName) {
```

