###Source Code and Configuration Management

[Source code Comment standards for this project](_pages/Comment-standards.md)

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

#### Release Management 

####Versioning & Deploying Code and Configuration Between Environments

Versioning of code and configuration has always been a rather large pain point for project teams and developers. Salesforce itself does not support versioning of the code and configuration within an org. Project teams cannot use standard development practices to check-in both your code and configuration. 

The first problem is that developers can write apex code on their local machines or directly in the Salesforce UI. Even if they are developing code in an external tool as soon as they save their changes are being “deployed” to the Salesforce org. The developer could then “commit” the code to source control, but what if someone made a change to the code directly in the UI without the developer’s knowledge? That code would never get checked into source control.

The second problem is the management of the configuration. You cannot easily edit configuration files and then check them into source control. Instead you perform the configurations directly in the UI. It would then take a developer to download all the configuration files using a development tool such as eclipse to check them into source control. This is definitely not a feasible practice. 

If you want to create a more repeatable process to retrieve/deploy Salesforce code and configuration you would use the Salesforce metadata API along with some ANT scripts to automate the deployments. This only gets you halfway there. Even after you create the automated scripts, you still would need to manually create the ```package.xml``` file that lists all of the files that you wish to retrieve or deploy. This is a very tedious and time consuming practice.

####Salesforce Change Set to the Rescue!

Salesforce offers a feature in the UI that allows you to “package” the components of an application by adding each of the components to a Change Set. This Change Set then acts as an inventory for all of the components in your application for a particular release. You can then use ANT and the Salesforce metadata API to create automated scripts that retrieve the components of a Change Set and then commit those components into source control. You can then use the same scripts to take the Change Set in source control and deploy the code and configuration to a target Salesforce environment. 

This is the basis of the deployment process outlined in this document. Below you will find a sample of what a Change Set in Salesforce looks like.

![Package](/img/Outbound_Change_Set.png)

####Deploying between Salesforce Environments 

An automation engine called “Jenkins” helps you automate deployments by executing step-by-step tasks. We have created a series of ANT scripts that use the Salesforce metadata API to retrieve Salesforce packages and commit them to Git/GitHub source control. Then other ANT scripts take what has been committed to Git or GitHub source control and deploys them to a specified target Salesforce environment. Jenkins is used to automate these scripts so that you do not need to type into a command line every time you wish to perform a deployment. 

A typical basic release from one environment to another environment would proceed as follows:

1. A developer or configurator creates a new Change Set in a Salesforce org per Release. 
1. A developer or configurator adds code and components to that Change Set for a particular release.
1. An automated Jenkins job runs on an hourly basis committing any new or updated components to GitHub source control. 
1. A manually initiated Jenkins job is executed by the release manager to deploy the code and configuration from the GitHub source control repository to the target Salesforce environment. 

#### PackageSource Control
As mentioned above, Salesforce out of the box does not support versioning of the code and configuration. This is why we are using GitHub with individual repositories to store and version the code and configuration for each Salesforce Change Set that is created. 

The following are the different repositories that will be used for releases. 

1. **Project Master Repository** - Every project team will have their own dedicated repository in GitHub. When a new project is established a new GitHub repository for that team will be created. The naming for project master repository is {Project Name} - Deploy. <br><br>This repository is managed by the release management team and is used to deploy Change Sets to the various platform environments such as Integration, UAT, Staging, and Production. <br><br>Project teams will fork this repository to manage their day-to-day versioning of code currently in flight. Once the coding and configuration for a Change Set is complete for a release, a pull request will be made by that project team requesting the release manager to merge the forked repository specfic release branch with the corresponding release branch on master. 
1. **Project Master Forked Repository** - This is a repository that has been forked from the “Project Master Repository” or {Project Name} - Deploy repository. This repository will be mapped directly to the “Project Dev” environment. A Jenkins job will be configured that will automatically take any code or components checked into the Change Set in the “Project Dev” environment and will automatically commit those code and components to the forked repository. 
1. **Individual Developer Forked Repositories** - In the case that a project team is using a distributed development model with one or more individual developer environments in addition to their “Project Dev” environment, one or more developer repositories will be forked from the “Project Master Forked Repository”. These are in essence double forked repositories. Each of these double forked repositories will be mapped directly to an individual developer sandbox similar to how the “Project Master Forked Repository” is mapped to the “Project Dev” environment. <br><br>For each individual developer environment and repository, a Jenkins job will be created that will take any components that are in a Change Set in the individual developer sandbox and will commit them to their dedicated double forked repository on a routine basis automatically.  Once the developer is ready to move their code and configuration to the “Project Dev” environment, the developer will create a pull request requesting that their repository be merged with the “Project Master Forked Repository”. The project lead developer would then accept the pull request and would execute a Jenkins job that would automatically deploy the package within the developer’s double forked repository to the “Project Dev” sandbox.

####Auditing and Tracking of a Release
There are two mechanisms that are used by the release management team to ensure that appropriate approvals are given for deployments to various environments and to track all communication throughout the process.

1. **Pull Requests** - Pull requests in GitHub are a mechanism to request that code from a forked repository release branch are merged into a corresponding parent repository release branch. Within the pull request the requester and release manager can collaborate with each other about the release. Any metadata item that cannot be deployed via Change Set has to be detailed as a pre or post deployment manual step in the deployment document and this has to be attached with the pull request.The pull request stays open till the code reviews are complete for a release. Once the release manager accepts the pull request, the code is ready to be deployed to upstream environments.

1. **RemedyForce Tickets** - RemedyForce tickets are used for audit tracking to ensure that the requester has the authority to request deployment from one environment to another. When a pull request is opened a RemedyForce ticket must also be opened requesting the deployment from one environment to another. Once the deployment has been completed, the RemedyForce ticket is then closed. Multiple RemedyForce tickets will be open throughout the entire release process for each time a deployment to a new environment is requested. Each time a ticket is opened that ticket must be notated in the pull request.

####Wrapping Things Up and Walk-through the Entire Process
Now that you understand the individual components involved in the release management process, you can walk through a complete release scenario by team member role from start to finish below. 

The simulation below walks through the following:
  1. Initiation of a new project.
  1. What happens on day one of development for the project.
  1. What happens every day after day one during development for the project.
  1. Requesting of a project package to be deployed to the Integration sandbox.
  1. Requesting of a project package to be deployed to the UAT sandbox.
  1. Requesting of a project package to be deployed to production. 
  1. What happens after deployment to production. 

###Release Management Scenario


####New Project Initiation
A new Salesforce project has just been established. The project has team members and is ready to start development. The following are the steps that must be performed before the project team can begin development. 


**ROLE: Project Manager / Lead Developer**

1. Submits RemedyForce ticket for the setup of a new Salesforce project for {Project Name}. 
1. Optionally the project manager / lead developer specify additional individual sandboxes needed if they are opting for a distributed development model.
1. Once submitted the RemedyForce ticket must go through the appropriate approvals. Once approved the ticket is then routed to the release manager.

**Release Manager**

1. Receives notification of the RemedyForce ticket to setup a new Salesforce project.
1. Creates Project Team Dev and Project Team Build/UAT sandboxes and grants the project lead access to the sandboxes.
1. Creates additional individual developer sandboxes as requested in the ticket. 
1. Creates a new repository in GitHub named {Project Name}-deploy.
1. Creates a new {Project Name} folder in Jenkins.
1. Clones the following Jenkins jobs and puts them in the {Project Name} folder.
    1. **{Project Name}-Retrieve and Commit** - Retrieves all code and components in the Project Dev sandbox on a hourly basis and commits to the project forked Repository.
    1. **{Project Name}-Deploy Package** - Deploys the package in the forked project team repository to the project team build/UAT environment.
    1. **{Project Name}-Deploy to Integration** - Retrieves the package from the Project Dev environment and commits it to the Project Master Repository. It then deploys the package from the Project Master Repository to the Integration platform sandbox.
    1. **{Project Name}-Deploy to UAT** - Deploys the package from the Project Master Repository to the platform UAT sandbox.
    1. **{Project Name}-Deploy to Staging** - Deploys the package from the Project Master repository to the platform Staging sandbox.
    1. **{Project Name} - Deploy to Production**  - Retrieves all configuration and code in production and backs up to the Salesforce Master Repository. Then deploys the package from the Project Master Repository to production. Then performs another backup of all code and configuration in production to the Salesforce Master repository. 
    1. **{Project Name} - Deploy Specific Version** - Template job that can be used to perform ad-hoc deployments from a specific commit in GitHub to a Salesforce environment. For example, if you needed to roll back changes from a previous commit this job would be used. 
1. Updates settings in the Jenkins jobs for the project specific settings such as git repositories, package name, usernames, and passwords.

**Lead Developer**

1. Forks the Project Master Repository ( {Project Name}-deploy ) to {Team}/{Project Name}-deploy
1. Creates a new empty Change Set based on a Release in their Project Dev sandbox.
1. Creates a new empty Release branch in {Team}/{Project Name}-deploy.
1. Informs the release manager of the new change set name.

**Release Manager**

1. Creates the release specific branch in ( {Project Name}-deploy ) Project Master Repository.
1. Creates the retrieve-commit and deploy Jenkins jobs for that specific release.

**Developers (for each individual developer sandbox)**

1. Creates a fork for their individual specific sandbox. e.g.,( {developer name}/{Project Name}-deploy ) in their indivdual GitHub account. This is the double forked repository we mentioned earlier.
1. Create new empty change set in their respective individual developer sandbox. 


####Day 1 Project Step
Now that all of the initial project initiation steps have been completed, the project team can now begin development. 

**Developer 1**

1. Creates a new apex class in Eclipse IDE and saves to the Platform Dev sandbox.
1. Creates a new Visualforce page in the Salesforce UI.
1. Creates a new custom object in the Salesforce UI. 
1. Adds the new apex class, Visualforce page, and custom object to the Change Set.

**Configurator 1 (working on same org as developer)**

1. Creates a new page layout, record type, custom field, etc in the Salesforce UI.
1. Adds the new page layouts, record types, workflow rules, etc to the Change Set.

**Jenkins/Ant {Project Name}-Retrieve and Commit job**

1. Syncs Change Set with git repository hourly and pushes to fork, {Team}/{Project Name}-deploy. All components not currently in the repository that are in the Change Set are added to the repository. Any existing components in the Change Set that are also in the repository are updated in the repository. 

**Note:** Only code and components that are in the Change Set are committed to the repository. 

####Day 1+X Project Step
This step represents every day after the first day of development. 

**Developer 1**

1. Refreshes the Eclipse IDE from the Project Dev.
1. Updates an existing apex class.

**Developer 2**

1. Creates a new apex class in the Eclipse IDE.
1. Adds a new apex class to the package. 

**Configurator 1**

1. Creates a new object in the Salesforce UI.
1. Creates an approval process in the salesforce UI.
1. Adds the object and approval process to the package.

**Configurator 2**

1. Updates an existing page layout in the Salesforce UI.
1. Updates an existing workflow rule in the Salesforce UI.

**Jenkins/Ant {Project Name}-Retrieve and Commit job**

1. Syncs Change Set with git repository hourly and pushes to fork, {Team}/{Project Name}-deploy. All components not currently in the repository that are in the Change Set are added to the repository. Any existing components in the Change Set that also in the repository are updated in the repository. 

**Note:** Only code and components that are in the package are committed to the repository. 

####Deploy to Team QA
In this step the project team now has enough code and configuration completed that they are ready to start testing their application and demoing it to end users. In order to QA and demo to end using they need to deploy their application to their project team’s build / QA sandbox.

**Lead Developer**

1. Verifies Change Set, and updates ```README.md``` in fork, {Team}/{Project Name}-deploy, and captures the manual pre-deploy and post deploy steps.

1. Performs pre-deploy manual steps in Team Build/QA.

1. Executes Jenkins job {Project Name} - Deploy to QA. 

     **Jenkins / ANT**
    1. Executes git repository sync that pushes to fork, {Team}/{Project Name}-deploy to make sure the repository is current.
    1. Deploys from the repository to the Team QA org.
1. Performs post deploy manual steps in Team QA.

**Note:** Notice that the lead developer entered any manual steps in the ```README.md``` in their repository. The ```README.md``` is used throughout the release management process to track any pre or post manual changes needed in addition to the automated deployment. This should be updated on a routine basis when new manual steps are needed. 

####Deploy to Integration
In this step the project team has completed the current version of their application and is ready to start the deployment process to production. The first step in that process is deploying their application to the platform integration sandbox.

**Lead Developer**

1. Verifies that the Change Set is tested and ready to deploy to integration. 
Creates a pull request from fork ( {Team}/{Project Name}-deploy ) release branch to ( {Salesforce}/{Project Name}-deploy ) release branch. 
1. Adds label/version in pull request. e.g., v2.5.09 … v2.5.10.
1. Creates a new ticket in RemedyForce for the deployment. Includes link to pull request in the ticket.
1. Creates a comment in the pull request, requesting to deploy to integration and references the ticket in the pull request.

**Note:** Notice that the lead developer added a label to the pull request. Labels are used so we can track each version that is committed. The labels can be any nomenclature that the project team wants to use to track each release. 

**Release Manager**

1. Reviews the pull request and RemedyForce ticket. Verifies that the appropriate approval have been given in the ticket. 
1. Release manager and COE Reviews code and provides comments for any required changes in the pull request. 
1. Once all comments have been addressed, the release manager accepts the pull request and merges into the {Salesforce}/{Project Name}-Deploy repository release branch.
1. Tag a release in GitHub for future reference purposes and deploying a specific release to upstream environments.
1. Executes any pre-deployment steps specified from the ```README.md```.
1. Executes Jenkins job “{Project Name}-Deploy to Integration” to deploy the release tag from the {Salesforce}/{Project Name}-Deploy repository to the Integration Sandbox.
1. Executes any post deployment steps specified from the ```README.md```.
1. This process of pull request could iterate a couple of times in order to fix defects found during the integration tests. Please note that for each integration fix cycle, a pull request has to be generated and a new release tag with an incremental number will to be generated.
1. Comments on the pull request that the deployment is complete or failed accordingly. 
1. Closes the ticket in RemedyForce once deployment is complete, regardless if the deployment was successful or failed. If the deployment failed the project team must fix any issues and create a new RemedyForce ticket. 


####Deploy to UAT
In this step the project team has successfully completed all system testing in the platform integration sandbox and has verified that there are no functional issues with their application and that their application hasn’t impacted any other applications in the integration sandbox.

**Lead Developer**

1. Creates a ticket in RemedyForce requesting to deploy to UAT. Includes link to the pull request in the ticket.
1. Creates a comment in the pull request asking to deploy from {Project Name}-Deploy repository to UAT and includes the RemedyForce ticket number in the comment. 

**Release Manager**

1. Reviews pull request and RemedyForce ticket. Verifies that the appropriate approvals have been given in the ticket. 
1. Performs any pre-deployment steps as outlined in the ```README.md``` file. 
1. Executes Jenkins job “{Project Name}-Deploy to UAT” to deploy the latest release tag from repository {Project Name}-Deploy to the UAT sandbox.
1. Performs any post deployment steps as outlined in the ```README.md``` file.
1. Comments on the pull request that the deployment is complete or failed accordingly.
1. Closes the ticket in RemedyForce once deployment is complete, regardless if the deployment was successful or failed. If the deployment failed the project team must fix any issues and then open a new remedyForce ticket to deploy to integration again. Once tests pass in integration they can then request deployment to UAT again. 

**Project Team**
Tests to make sure everything is functioning as expected in the UAT sandbox.

####Deploy to “X Platform Sandbox”
This is an optional step that can be used if the project team wishes to deploy their application to another sandbox now listed in this scenario. 

**Lead Developer**

1. Creates a ticket in RemedyForce requesting to deploy to “X Platform Sandbox”. Includes link to pull request in the ticket. 
1. Creates comment in pull request asking to deploy from {Project Name}-Deploy repository to “X Platform Sandbox” and includes RemedyForce ticket number in the comment. 

**Note:** If the project team needs to deploy to another sandbox at the project level and not the platform level they can have the release manager clone a Jenkins job that they can run to deploy to their other sandboxes without requiring a pull request or RemedyForce ticket. 

**Release Manager**

1. Reviews the pull request and RemedyForce ticket. Verifies that the appropriate approval have been given in the ticket. 
1. Performs any pre-deployment steps as outlined in the ```README.md``` file. 
1. Executes Jenkins job “{Project Name}-Deploy to X Platform Sandbox” to deploy the latest release tag from repository {Project Name}-Deploy to “X Platform Sandbox”.
1. Performs any post deployment steps as outlined in the ```README.md``` file.
Comments on the pull request that the deployment is complete or failed accordingly.
1. Closes the ticket in RemedyForce once deployment is complete, regardless if the deployment was successful or not. Just as with failures when deploying to UAT, if any failures occur they must open a new RemedyForce ticket to deploy to integration first and then they can deploy again to this environment if they make any changes to their code or configuration. 

####Deploy to Staging 
Once all testing has been completed in UAT and signed off, the release manager will then perform a practice deployment to staging just as if a deployment to production was occurring. This step is entirely for the release manager to make sure that he has all of the deployment steps correct before deploying to production. 

**Lead Developer**

1. Provides comment in pull request asking to deploy from {Project Name}-Deploy repository to production. 
1. Creates a ticket in RemedyForce requesting to deploy to production. Includes link to pull request in the ticket. 

**Release Manager**

1. Approves request for deployment to production and schedules deployment to production.
1. Performs any pre-deployment steps as outlined in the ```README.md``` file. 
1. Executes Jenkins job “{Project Name}-Deploy to Staging” a specific release tag. 
1. Performs any post-deployment steps as outlined in the ```README.md``` file. 
If the deployment failed, removes the deployment from the schedule and closes the ticket in RemedyForce. As with previous steps the project team must fix any issues in code and configuration. Once they fix the issues they can open a ticket in RemedyForce to deploy to integration again. 

**Project Team / Release**

1. Performs final smoke tests to make sure everything is working as expected in the staging sandbox.

**Note:** Only project team members who are authorized to access production data will be granted access to test in the staging sandbox.

####Deploy to Production
This is the final step in the release management process. 

**Release Manager**

1. The day before the scheduled deployment date, uses Jenkins to perform a full backup of the production environment and commits into the Salesforce master repository with a new version/label for the backup.
1. On the scheduled deployment date performs any pre-deployment steps as outlined in the ```README.md```.
1. Executes Jenkins job “{Project Name}-Deploy to Production” a specific release tag. 
1. Performs any post deployment steps as outlined in the ```README.md```.
1. If the deployment failed, works with the project team to remedy the failure. If the failure cannot be easily remedied, the release is rolled back. 
1. Uses Jenkins to perform a full post deployment backup of the production environment and commits into the master Salesforce repository.
1. Closes the remedyForce ticket.
1. Closes the pull request.

**Project Team**

1. Performs testing in production to validate everything is working as expected.

####Next Release Initiation
This is the first step in the next release cycle. 

It is recommended that at the beginning of each release, the existing sandboxes for the previous release are retired and replaced with new sandboxes so that all sandboxes reflect the most recent version of production. This step is optional and up to each individual project team. 
The longer a project team goes without refreshing their sandboxes, the higher the risk that there will be problems when they attempt to deploy to the platform sandbox environments and production. 

**Release Manager**

1. Refreshes the platform, UAT, and staging sandboxes as needed. It is recommended that this is done once a month after a release to ensure that all platform sandboxes match production to reduce deployment issues. 

**Project Team**

1. Creates RemedyForce ticket to create environments for the next release.

**Release Manager**

1. Creates a new sandbox for the project team dev for the next release. 
1. Creates and/or refreshes any developer specific sandboxes (as requested).

**Project Team**

1. Creates RemedyForce ticket to retire the previous version sandboxes when no longer needed. 

**Release Manager**

1. Deletes previous version project sandboxes.
