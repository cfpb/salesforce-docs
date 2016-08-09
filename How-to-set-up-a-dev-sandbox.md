####Current Sandboxes Purchase

* Full: 4

* Partial: None

* Dev Pro: 5

* Developer: 95

####Naming Structure

Sandbox names and descriptions are an important part of the sandbox management strategy.    Being able to easily identify the purpose of the sandbox as well as the responsible team/person is key.  Sandbox creation will be handled by an admin in production once approval has been given for a sandbox request.  Sandboxes requests should be addressed to the COE for review and approval.  Once approved the sandbox will be created adhering to the following naming convention.

Team Name | Team Number | Sandbox Purpose| Developer Initials (where applicable)

For the SES project team 1 developer sandbox for John Smith would be created with the following name.

Example: SES1DevJS

Sandbox names have a maximum of 10 characters so team names will need to be abbreviated.

Example: Mosaic team build sandbox: Mos1Build


####Standard Team Sandboxes

Each new project team should expect to be allocated 1 master build sandbox, 1 master dev sandbox, 1 sandbox per developer (if requested), 1 data migration development sandbox (if requested).


The master build sandbox should be where configuration is done including page layouts, profiles, workflow etc.

The master dev sandbox should be where all of the custom development is done if the team is working in one sandbox.  If the team has one sandbox per developer then the master dev is where all of the custom development will be combined prior to it being pushed to the enterprise level integration sandbox.

####Jenkins CI jobs

Jenkins and Github will be used for continuous integration during the development life cycle.  There will be template jobs provided to the team to assist with validation and deployment across the team orgs.

####Enterprise Sandboxes

There are a number of sandboxes in the deployment path from the team sandboxes to production.  The first stop on the path to production is the Integration sandbox.  Teams will be validating their code and configuration against this environment often to help find bugs early in the process.  Once code and configuration are ready to be deployed and they are successfully deployed in integration they will be pushed to the UAT environment.  The UAT environment will be a stable full sandbox used for UAT prior to releases being deployed into production.  Upon completion of UAT releases will be deployed to Staging which will serve as a mock deployment for production.  Staging will be a full sandbox that is a nearly identical copy of production (the data will be slightly out of sync based on refresh timelines).

####Salesforce Admin Steps to Create a Dev Sandbox
1. Create sandbox
2. Log in to sandbox as the admin
3. Go to Setup > Quick Find > Users 
4. Navigate to user, click on user's name
5. Make user an admin
   1. Click "edit"
   1. Set "User License" to Salesforce
   1. Set "Profile" to System administrator
   1. Click Save
4. Set email
  1. Click Edit
  1. Replace the email address, ```firstname.lastname=cfpb.gov@example.com``` with ```firstname.lastname@cfpb.gov```
  1. The user will get notified to confirm the email address change, which they must do within 72 hours(?)
6. Click the “Reset Password” button
7. The user will receive a link to reset their password.

This _should_ be enough. **But**, an unknown question is around the security question and how that works _if_ it has not been set.  

####Salesforce Admin Steps to Grant User Access to Sandbox
1. Go to Salesforce Setup
2. Search for 'Sandbox' - Find sandbox name and click 'Login'
3. Change URL to be 'https://cfpb--<sanbox name>.cs##.my.salesforce.com'
4. Go to Setup - Maintain Users on that sandbox
5. Find the user & click Edit
6. Change Email, set User License to 'Salesforce', set Profile to 'System Admin', check 'Service Cloud User', check 'Generate New Password'
7. Click Save  

If no email was sent to the user, search 'Email' - 'Deliverability', Set Access level to 'System Email Only'. 


