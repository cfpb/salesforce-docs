###Deployment Pipeline

####Process Overview
The goal of the release management process is to create a process that defines 

1. The environments necessary to enable multiple project teams to concurrently develop applications on the Salesforce platform 
1. The mechanism that enables project teams to easily move Salesforce configuration and code from one environment to another 
1. The process that all Salesforce project teams follow to deploy code and configuration from one environment to another in a repeatable fashion to ensure business continuity while reducing the total time of deployment of applications to production.  

####Development Models
There are two different models that a project team can use while developing their applications.

1. **Centralized Development Model** - A centralized development model is a development structure in which all team members configure and develop Salesforce applications in a single environment. This structure is typically used when there are a small number of developers working on separate capabilities that do not conflict with each other.
1. **Distributed Development Model** - A distributed development model is a development structure in which each developer has their own dedicated Salesforce sandbox where they develop application features. They can perform configuration and code changes in their dedicated environment. When they have completed a specific feature, that feature is then deployed to a master team development environment that is typically controlled by a project lead. This allows many developers to function independently without impacting other team members. This structure is typically used for larger development teams.

####Salesforce Environments
The salesforce environments used for Salesforce releases are broken up into categories:

**Project Environments** - Project environments are Salesforce sandbox environments that are dedicated to a single project team. The project team has full access to the environments and does not share the environments with any other project team. The project team members manage all releases among all of their environments and choose the level of access each member has to each of their environments.

Project team environments consist of the the following environments:

1. **Project Dev**  - The project development environment is where the master code and configuration will reside for the project’s application.

1. **Project UAT/Build**  - The project UAT/Build environment is the environment where the project team will deploy their code on a routine basis from the project dev environment to test and demo their application to end users. No development should occur in the Project UAT/Build environment.

1. **Individual Developer Environments** - If a project team is using the distributed development model, then they will have individual developer sandboxes dedicated to each developer. When a developer is done with a particular feature, then that feature is deployed to the Project Dev environment. 

1. **Project Data** - If a project team is conducting a data migration they may request an additional sandbox in which to practice their data migration.  The type of sandbox may vary based on the number of records being loaded.
        
**NOTE:** Individual developer environments can also be used in either model for proof of concepts. Project teams should avoid creating proof of concepts in their Project Dev org if at all possible.

**Platform Environments** - Platform environments are Salesforce sandbox environments that are shared across all project teams. Access to these environments is limited for the project team members. The platform release manager is the owner of the platform environments and manages all releases among the different environments including production.

Platform environments consist of the the following environments:

1. **Integration** - The integration environment is the first environment where all project teams deploy to the same environment. The purpose of the integration environment is to verify that each project’s applications will deploy and not adversely affect another project team’s application. Once a project team’s application is deployed to the integration environment successfully, the project team would then perform system level testing to verify that the application works as expected. Also at this time the project team will also test any integrations to other external systems.

1. **UAT** - The UAT environment is where all of the user acceptance testing is performed for each project’s applications that will be deployed to production. The UAT environment is a full sandbox allowing for a complete end to end testing to occur with a complete data set. Because this environment contains production data, only users that have been cleared to interact with production data are granted access to this environment. Typically access in this environment will mirror the access levels granted in production.

1. **Staging** - The staging environment is an environment primarily reserved for the release manager. This environment is used by the release manager to perform the final deployment rehearsal before deploying to production. This gives the release manager one more chance to catch any problems with the deployment steps. Once the deployment has been completed to staging, the release manager will grant temporary access to the project team to perform a sanity check to make sure that the deployment to staging was successful and the application performs as expected.

1. **Production** - This is the live environment where users are actively using the system. 

####Deploying to Production
In order to deploy a release to production, the project team must first deploy their code and configuration to the different platform environments described above. The reason that the team must first deploy to these lower environments is so that we can verify that your application works as expected, does not conflict with other teams environments, and does not experience any complications during deployment. 


Below you will find a diagram of the environments described above depicting the flow a deployment must go through in order to be deployed to production.

![Deployment](/img/Deployment-Pipeline.png)
