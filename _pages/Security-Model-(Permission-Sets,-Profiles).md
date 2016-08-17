### Objectives
CFPB requires a profile and permission set approach that is optimized based on the following parameters:

* Profile Maintenance Effort
* Permission Set Maintenance Effort
* Profile Consistency
* Permission Set Consistency
* Ease of Provisioning Regular Users
* Ease of Provisioning Crossover Users
* Page Layout Flexibility
* Permissions Model

The selected approach is as follows (for example in SES):
![Profile Model](/img/profile_model.png)

This is an example of roles with two (2) example permissions sets (SES Examiner, SES Super User); the actual diagram may vary from project to project.


#### Classification
Permission/Profile Type | Description | Naming Guidelines
----|----|-----------------
Common Profile | This serves as a single profile assigned to all CRM license users. As the org grows, there may be a need for additional profiles: - Special purpose ones where the common profile does not meet requirements - Profiles to match additional license types (e.g., Platform, Communities, etc.) This does not account for system administrator or API profiles.|CRM User, Platform User, Customer Community User, etc.
Baseline Permission Set | This permission set will be assigned by default to all Service Cloud users. As the org grows, there may be a need for additional baseline permission sets to align with license types or other user groups. | Global - Baseline - Service Cloud User
Base Application User Permission Set | Each application will have a permission set that contains the minimum permissions needed for use of the application. This is essentially the “regular user” permission set. | App - SES, App - Mosaic, etc.
Feature Permission Set | These permission sets enable additional functionality from the base application permission set. There should be no permissions repeated here from the base application permission set. | App - Mosaic - Approve KB Article
Function Permission Set | These permission sets are for users with enhanced permissions within the application (e.g., super users and supervisors). There should be no permissions repeated here from the base application permission set. | App - Mosaic - Power User
Overlay Permission Set | These permissions sets are for features or functions that are not application-specific. These would be of two types: - Pervasive permissions, assigned to a large number of users (though not all users, otherwise the permissions would go in the baseline permission set) - Special purpose permissions, such as data stewards or super users of org functions that are not application-specific | Global - View All Data, Global - API Enabled, Global - Author Apex, etc.


### Rules and Guidance
1. Each new application will have a single permission set that is assigned to all users of that application, regardless of function. In special circumstances, there can be two base permission sets if not enough commonality can be established in a single one.
1. Feature and function permission sets for applications (e.g., super users and supervisors) will contain only the delta against the base permission set for that application. Under no circumstances will permissions be repeated from the base permission set within feature permission sets.
1. The creation of overlay permission sets should be coordinated with the COE. These are cross-functional permission sets used for parts of the org that are not application-specific (e.g., management of regulations, product lines, etc.).
1. The creation of new profiles is possible only under exceptional circumstances. Any new profiles must have proper justification and require approval from COE before development begins.
1. The COE may revisit the decision for a single profile by license type and opt for division-specific profiles if there is a business need in the future. The objective is to minimize places where permission updates need to be made, thereby reducing maintenance costs.
1. Additions to the baseline permission set(s) will be governed and managed by the COE. Development teams can petition for new permissions in the baseline, but this would be a rare circumstance since development teams should focus on application-specific functionality.
1. System administrators will use a new profile that is cloned from the out-of-the-box System Administrator profile, per best practices.
1. API profiles will be created as needed, though every effort should be made to keep all integration users on a single API profile. The specifics of the profile must be defined in conjunction with the security team.

____

### TODO/Outstanding Tasks
- Identify the system and object permissions that need to go in the common profile (these should be minimal, if any) and a name for it, according to the agreed upon standards
- Identify the system and object permissions that need to go in the baseline permission set and a name for it, according to the agreed upon standards
Define an SOP for review of permission set and profile creation
- The CoE needs to sign off on this policy and include it in the technical guidelines
- The SES Development Team needs to realign its profile and permission sets in accordance with this policy
Come up with naming convention for permission sets
- Define a base API profile
- Clone the System Administrator to a custom profile
- Define a policy for “view all” and “modify all” on permission sets and profile

