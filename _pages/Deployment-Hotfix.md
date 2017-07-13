##Deployment Hotfix

####Process Overview

Hotfix Relase: A release to production that includes only business-critical fixes and/or additions to address known bugs. Hotfixes are not considered regular releases.

O&M Release: A coordinated, scheduled release to production that includes fixes to all non-critical bugs that have been resolved by the Project Teams.

Product Releases: A scheduled release to production that includes net-new functionality. The functionality included within releases of this type is based on prioritization determinations made by the Change Control Board.

Hotfix Environment: The hotfix environment is where project teams will deploy changes for the same validation before moving the change to Production. Hotfix Release will use hotfix environment. All validation and testing should be performed in this environment so that platforms team will give the approval to move changes to the production environment. 


####Deploying to Production
In order to deploy a Hotfix release to production, the project team must first deploy their code and configuration to the Hotfix environment. The reason that the team must first deploy to these lower environment is so that we can verify that your application works as expected, and does not experience any complications during deployment. 


Below you will find a Hotfix production release process diagram.

![Deployment](/img/Deployment-Hotfix.png)