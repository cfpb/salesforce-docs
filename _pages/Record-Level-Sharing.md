###Sharing & Security

There are many different mechanisms in which access to Salesforce is controlled. It is easiest to think of security in Salesforce broken up into the following 3 different categories: 

1. **Object Level Access** – Object level access controls the access various Salesforce standard and custom objects such as Account, Contact, Opportunity, or custom objects you create. Object level access defines if a user has access to Read, Create, Update, or delete records within that object. Additionally object level access also controls which fields users are allowed to view or update on those objects. All object level access within Salesforce is controlled by Profiles and Permission Sets. 

1. **Record Level Access** – Once a user has access to a specific object, users can then be limited to view or edit only specific records within that object. This is what we refer to as "Record Level" sharing within Salesforce. Sharing of records is controlled by Salesforce Organization-wide defaults, Criteria Based Sharing, Roles, manual sharing, and Apex Sharing.  

1. **System & Application Level Access** – System and application level access is access users are granted to perform specific actions across the Salesforce application. There are many different actions a user can perform that can be controlled such as user creation, ability to export data, ability to modify setup objects, etc. These permissions are controlled by Profiles and Permission Sets. 

###Profiles & Permission Sets

As mentioned above Profiles & Permission Sets control the object level access and System & Application level access for users. You can pretty much do the same thing with Profiles and Permission Sets except for that a user can only have one profile where you can assign multiple permission sets to a user or profile.  

It is recommended to use profiles to create a base set of permissions for users of specific groups. Then create permission sets for each application that users will need access to for each type of role in that application. For example:   

**Profiles** 

System Administrator  

Sales User  

Legal User  

Marketing User  


**Permission Sets** 

Order Management Application User  

Order Management Application Admin  

The permission sets would be assigned on a user-by-user basis based on the applications that the users need access to. This allows you to easily add or remove access to users for specific applications instead of having to create profiles of various different combinations to handle the same use cases. Think of permission sets as similar to Access Control Lists (ACL). 



###Salesforce Sharing

Salesforce sharing controls what records users have access to view and edit. Keep in mind that since the profile and permission sets control object level access, if a user doesn’t have access to a particular object, then even if sharing allows them to view or edit records within that object, they will not have access to those records since they don’t have access to the entire object through profiles or permission sets. 
 
When working with Salesforce sharing it is always best to use the most global sharing mechanisms first, then move to the more granular controls. As you move to the more granular sharing controls you need to be more aware of performance considerations. 
 
The following are the Salesforce sharing controls available. 
 
###Organization-Wide Defaults  
Organization-Wide defaults are the highest level and most restrictive sharing controls available on the platform. These settings control the visibility of records on a global scale for objects. These settings are set on an object by object basis. 
 
The following are the available options: 
 
***Public Read/Write/Transfer***  
Public Read/Write/Transfer is the least restrictive organization-wide default and is available only for the lead and case object. This setting allows every user to view, edit, and change ownership of every record within the lead or case objects that are set to “Public Read/WriteTransfer” regardless of their other sharing settings. 
 
***Public Read/Write***   
Public Read/Write is the second least restrictive organization-wide default and is available for most standard and all custom objects. This setting allows every user to view and edit every record within the objects that are set to “Public Read/Write” regardless of their other sharing settings. 
 
***Public Read Only***  
Public Read Only is the second most restrictive organization-wide default and is available for most standard and all custom objects. This setting allows every user to view every record within the objects that are set to “Public Read Only” regardless of their other sharing settings. Users cannot edit records within the objects set to “Public Read Only” unless they are granted “edit” access through other sharing settings.  
 
***Private***   
Private is the most restrictive organization-wide default and is available for most standard and all custom objects. This setting restricts every user from viewing or editing records within the objects that are set to “Private” unless they are granted “view” or “edit” access through other sharing settings.  
 
###Criteria Based Sharing (Sharing Rules)    
Criteria based sharing is rule or owner based sharing that grants read or read/write access for a set of records to specific groups of users. Criteria Based Sharing is the next level of sharing controls below organization wide defaults. 
 
There are two types of rules that can be created. 
 
***Based on Record Owner***  
Rules based on record owner grant access to users in specific roles or groups to records that are owned by users within specific roles or groups. 
 
***Based On Criteria***  
Criteria based rules grant access to users in specific roles or groups to records that match specific criteria on the records within the object. 
 
###Role Based Sharing  
Roles are hierarchal groupings of users within a Salesforce org. Role based sharing propagates the access to records that users have to users up the role hierarchy.  
 
For example: If the following role hierarchy exists: 
 
Sales VP 
 	| 
Sales Executives 
 
Then anyone that is a member of the “Sales VP” role will inherit the access from everyone in the “Sales Executives” role. 
 
***Note:*** In order for access to be granted via role hierarchies the setting “Grant Access Via Hierarchies” must be checked for each object that you wish to respect role hierarchy sharing. 
 
 
 
###Manual Sharing    
Manual sharing is the most granular and least performing of all sharing mechanisms within Salesforce.  Care must be taken when using manual sharing as too many manual sharing rules on any single object can cause a delay in response time when viewing records on that object.  
 
Manual sharing allows the owner of a record to manually grant (share) read or read/write access to a record to another user, group, or role.  
 
Manual shares can also be created programmatically using apex or apex triggers. Use caution while programmatically creating manual shares via apex as you can easily cause performance degradation if you are adding a large number of shares to a single object.  
 
###Special Permissions That Affect Sharing  
There are special permissions that can be set via profiles and permission sets that can override the Salesforce sharing settings.  
 
These permission exist in two types: 
 
***System / Administrative***   
Under the system permissions you will find the permissions “view all data” and “modify all data”. If a user has these permissions, the user will be able to view and/or edit all records for all objects regardless of the sharing settings set.  
 
Be very careful when setting these permissions, as these permissions will open up access to all of your data to a single user. Even if a field is set as read-only on the object profile permissions, the user will still have full access to the object as well.  
 
***Object Level***   
In addition to the ability to grant global read or edit access to all records across all objects, you can set read or edit access for all records for only a single object. At the object level if you set the permissions “view all” or “modify all” then all users in the profile or permission set will be able to view and/or edit all records within that object regardless of the sharing settings. 
