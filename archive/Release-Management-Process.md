New Project Initiation Steps 

Shared Org

Pre-condition: 
New Project created
Release manager creates new repo in github named {Project Name}-deploy
Lead developer forks the {Project Name}-deploy repo to {Team}/{Project Name}-deploy
Lead developer creates a new empty package in their dev org
Team optionally creates a branch/fork for any developer specific sandboxes; e.g., cool-feature-1
Release manager clones Jenkins/Ant job template that will push package to fork {Team}/{Project Name}-deploy.

Day 1 Project Step

Developer 1
Developer creates a new apex class in eclipse and saves to salesforce dev org.
Developer creates new visualforce page in the Salesforce UI.
Developer creates a new custom object in the Salesforce UI. 
Developer add the new apex class, visualforce page, and custom object to the package.

Configurator 1 (working on same org as developer)
Configurator creates new page layout, record type, custom field, etc in the Salesforce UI.
Configurator adds the new page layouts, record types, workflow rules, etc to the package.

Jenkins/Ant Automated Process
      6.  Syncs package with git repo hourly and pushes to fork, {Team}/{Project Name}-deploy, and optionally to named branch.

    


Day 1+X Project Step

      Developer 1
Developer refreshes IDE from org.
Developer updates apex class.



      Developer 2
Developer creates new apex class in eclipse.
Developer adds apex class to the package. 

     
Configurator 1
Configurator creates report in Salesforce UI
Configurator creates approval process in salesforce UI
Configurator adds the report and approval process to the package.

Configurator 2

Updates existing page layout in the Salesforce UI.
Updates existing workflow rule in the Salesforce UI.

Jenkins/Ant
      6. Syncs package with git repo hourly and pushes to fork, {Team}/{Project Name}-deploy, and optionally to named branch.

Deploy to Team QA

Lead Developer 
Verifies package, and updates readme.md in fork, {Team}/{Project Name}-deploy, and captures the manual pre-deploy and post deploy steps.
Performs pre-deploy manual steps in Team QA
Executes Jenkins job {Project Name} - Deploy to QA. 
     Jenkins / ANT
Executes git repo sych that pushes to fork, {Team}/{Project Name}-deploy to make sure the repo is current.
Deploys from the repo to the Team QA org.
      4. Performs post deploy manual steps in Team QA.


Deploy to Integration

Lead Developer
Verifies that package is tested and ready to deploy to integration. 
Creates pull request from fork {Team}/{Project Name}-deploy to {Salesforce}/{Project Name}-deploy. 
Adds label/version in pull request. e.g., v2.5.09 … v2.5.10
Creates a new ticket in RemedyForce for the deployment. Includes link to pull request in the ticket.
Creates a comment in the pull request, requesting to deploy to integration and references the case number in the pull request.


Release Manager

Reviews pull request and RemedyForce ticket. Verifies that the appropriate approval have been given in the ticket. 
Release manager and COE Reviews code and provides comments for any required changes.
Once all comments have been addressed, release manager accepts pull request and merges into the {Salesforce}/{Project Name}-Deploy repo.
Executes any pre-deployment steps specified from the readme.md.
Executes Jenkins job “Deploy to Integration” to deploy package from the {Salesforce}/{Project Name}-Deploy repo to the Integration Sandbox.
Executes any post deployment steps specified from the readme.md.
Comments on the pull request that the deployment is complete or failed accordingly.
Closes the ticket in RemedyForce once deployment is complete, regardless if the deployment was successful or failed. 


Deploy to UAT


Lead Developer
Creates a ticket in RemedyForce requesting to deploy to UAT. Includes link to pull request in the ticket.
Creates comment in pull request asking to deploy from {Project Name}-Deploy repo to UAT and includes RemedyForce ticket number in the comment. 



Release Manager
Reviews pull request and RemedyForce ticket. Verifies that the appropriate approval have been given in the ticket. 
Performs any pre-deployment steps
Executes jenkins job to deploy package from repo {Project Name}-Deploy to the UAT sandbox.
Performs any post deployment steps
Comments on the pull request that the deployment is complete or failed accordingly.
Closes the ticket in RemedyForce once deployment is complete, regardless if the deployment was successful or failed.

Project Team
Tests to make sure everything is functioning as expected in the UAT sandbox.


Deploy to “X Platform Sandbox”


Lead Developer
Creates a ticket in RemedyForce requesting to deploy to “X Platform Sandbox”. Includes link to pull request in the ticket.
Creates comment in pull request asking to deploy from {Project Name}-Deploy repo to “X Platform Sandbox” and includes RemedyForce ticket number in the comment. 



Release Manager
Reviews pull request and RemedyForce ticket. Verifies that the appropriate approval have been given in the ticket. 
Performs any pre-deployment steps
Executes jenkins job to deploy package from repo {Project Name}-Deploy to “X Platform Sandbox”.
Performs any post deployment steps
Comments on the pull request that the deployment is complete or failed accordingly.
Closes the ticket in RemedyForce once deployment is complete, regardless if the deployment was successful or not. 


Deploy to Staging 

Project Team
Testing completed successfully in UAT for project  {Project Name}

Lead Developer
Provides comment in pull request asking to deploy from {Project Name}-Deploy repo to production. 

Release Manager
Approves request for deployment to production and schedules deployment to production.
Performs any pre-deployment steps for deployment to staging.
Using jenkins deploys package from repo {Project Name}-Deploy to Staging.
Performs any post deployment steps for staging.
If the deployment failed, removes the deployment from the schedule and closes the ticket in RemedyForce.


Project Team / Release
Performs final smoke test to make sure everything is working as expected in the staging sandbox.


Deploy to Production

Release Manager
The day before the scheduled deployment date, uses jenkins to perform a full backup of the production environment and checks into the master repo with a new version/label.
On the scheduled deployment date performs any pre-deployment steps.
Using jenkins deploys the package from repo {Project Name}-Deploy to production. 
Performs any post deployment steps.
If the deployment failed, works with the project team to remedy the failure. If the failure cannot be easily remedied, the release is rolled back. 
Uses Jenkins to perform a full post deployment backup of the production environment and checks into the master repo.
Closes the remedyForce ticket.

Project Team
Perform testing in production to validate everything is working as expected.
