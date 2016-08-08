5/20/16 - Draft. Please edit and provide feedback.
Updated: 06/10/16

**Git Branches**
These are the list of branches in the Salesforce org for code and configuration repos. Teams can use a different strategy, including the use of feature branches:

- ```master``` (production ready)
- ```integration``` (ready for integration sandbox)
- ```pre-prod``` (UAT and staging. Do we need more? If so, why?)

**Git tags/versions (semantic versioning)**:
Semantic versioning will be used for the code, config, and deployment repos in the Salesforce org. Product teams may choose to use a different way to name release. Examples:
- 1.01.01
- 2.00.09RC-1
- etc.



**Salesforce _main_ Repos:**
Following is a list the primary repositories in the Salesforce org. Teams are **required** to fork the code, config, and deploy repos and refresh them at least twice per week. 
- ```salesforce-code``` (current classes, triggers, pages, lightning components?)
- ```salesforce-config``` (a periodic snapshot of configuration items in Salesforce)
- ```product-deploy```, where _product_ is the name of an application; e.g., ses-deploy, mosaic-deploy
- ```salesforce-docs``` (technical and other related documentation)

**Draft workflow**
Precondition: Development Lead from product team is keeping source code and configuration up-to date; that is, they're performing daily syncs with ```INTEGRATION```. 
- Dev Lead forks the appropriate deployment repository from the Salesforce GitHub org; e.g., [mosaic-deploy](https://github.cfpb.gov/Salesforce/mosaic-deploy)
- Dev Lead [[creates a deployment package]] in the Team-Build sandbox
- Dev Lead merges this package into the team's fork of their deployment repo
  - TODO: May need to leverage Ant and Jenkins
- Dev Lead adds a release tag; e.g., 2.4.09 or whatever the business and team agree is a way to version the release
- Dev Lead creates a pull request from their deployment repo to the matching deployment repo in the Salesforce org, specifying a request to merge into the ```integration``` branch.
- Dev Lead includes all additional deployment and configuration instructions as part of the pull request.
- The Release Manager reviews, validates, and merges the pull request. Note that this step can take as much time as needed and may involve numerous conversations and dialogues within and outside of the GitHub pull request. TODO: articulate required criteria, such as version (tag), test coverage, etc. 
- The Release Manager deploys to ```integration``` and coordinates deployments to higher environments
- The Release Manager deploys to ```UAT```, ```staging```, ```production```
- The Release Manager synchs both code and configuration from ```production``` to ``salesforce-code```` and ```salesforce-config``` and increments the version; e.g., ```2.4.9``` becomes ```2.4.10``` 


**Norms**
- All Salesforce peeps are expected to actively follow GitHub so they can be aware of any pending changes and make comments should they see something wrong
- Each repository should contain copious amounts of quality documentation. This includes a world-class ```README``` that tells any developer how to navigate and maintain the application.  It should include all the ins and outs, the speedbumps, skeletons, etc.

____

**TODO**

- If deploying from org to org, Jenkins needs to compare the git hash with what's being deployed. 

