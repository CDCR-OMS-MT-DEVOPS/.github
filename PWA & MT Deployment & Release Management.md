# PWA & MT Deployment & Release Management

## Overview of MT Platform Deployment Services
Application (AppDev) teams should control when and how often they wish to deploy their software to the various EIS-MiddleTier (MT) clusters. These deployments should be executed via CI/CD automation workflows that are developed by, maintained by and governed by the MT/DevOps team.

The MT/DevOps team serves the AppDev community by facilitating the entry of their products into our MT configuration and CI/CD automation workflows with the outcome being a deployable product.

AppDev teams need only notify the MT/DevOps team the first time they are deploying their front and/or backend component into a specific MT cluster (Dev, UAT, Staging, Production).  Thereafter, the AppDev team can use the provided CI/CD automation to deploy their application components to the target MT cluster.

All application components **must** be deployed to each MT cluster in the following sequence, there are no exceptions:
1. **MT Dev** : This represents the “appsdev” & “apidev” domains, private/internal only domains for developers to integration test their components. When changes to an application component are merged to the "main" branch, this triggers a build and deployment of the component to this cluster.
1. **MT UAT** : This represents the “appstest” & “apitest” domains, public domains that product teams use for both demos of and end-user testing of Agile sprint deliveries.
1. **MT Staging** : This represents the “appsstage” & “apistage” domains, public domains that product teams, stakeholders, and end-users use for pre-production testing.  The Staging cluster is an exact mirror of Production, thus it is the main proving ground for the MT/DevOps team to practice Production deployments to ensure that the first deployment and all subsequent scheduled and automated Production deployments will perform smoothly.  Once this last level of **deployment** and **application** vetting has completed successfully, the application components are considered production-ready.
1. **MT Production** : This represents the “apps” & “api” domains, a public domain used for production deployments of applications that have passed all previous deployment vetting.  AppDev teams must consider potential end-user outages on all subsequent deployments.

##Deploying a Front and/or Backend Component For The First Time
When you have a new project or a new front and/or backend component that has never been deployed before, it is the responsibility of the AppDev team to notify the MT/DevOps team of the need to add the new component to the MT configuration and to ensure CI/CD automation is available.  The AppDev team must perform this initial notification via the [Deployment Request Form](https://cdcr.sharepoint.com/sites/CDCR_EIS_T_MiddleTierPWA/Lists/DeployRequest/AllItems.aspx). 

AppDev responsibility aside, this process is collaborative.  The AppDev and MT/DevOps teams must work together to determine the precise MT infrastructure needs of the application components such as: database type, location & credentials, 3rd-party endpoints & credentials/api-keys, scaling of application, component naming conventions.

If your application is not listed on the [Deployment Request Form](https://cdcr.sharepoint.com/sites/CDCR_EIS_T_MiddleTierPWA/Lists/DeployRequest/AllItems.aspx), then choose the “Application Name” of “**NEW PROJECT**” and provide the name of your project in the “Comments” field.  Set the “Target MT Cluster” to “**DEV**” and in the “Comments” field list the URL path name for your desired frontend and/or list the Docker image name for your desired backend server.  

## When to Use Deployment Automation for Higher Environments

AppDev teams first build and deploy their apps to the MT Dev cluster after their code has been reviewed and merged to the "main" branch. The Dev cluster is considered a lower environment.  Higher MT environments are UAT, Staging and Production.

AppDev teams must verify that all of the following prerequisites are met in order to use deployment automation to higher MT environments:
- The frontend and/or backend component(s) to be deployed must already exist in the MT.
- You already have automation created for higher MT environments.
- The deployment does not require a change in the MT server/service configuration or routing.
- The deployment does not require the MT cluster to be stopped and restarted.
- If the CCB process is not applicable for this deployment OR if the CCB process has been invoked and the CCB has been approved.

If you meet **all** of these prerequisites, then you may use deployment automation for your project and do not need to schedule the deployment.  Just run your GHE workflow or Azure pipeline when your team has determined that your application is ready for deployment.  

Be sure to monitor the progress of your deployment to determine the success or failure of your deployment.  If your deployment failed and you are unable to resolve the issue, please contact the MT/DevOps team to either resolve the deployment issue or to rollback the deployment when a partial deployment has occurred.

## When to Use a Scheduled Deployment for Higher Environments
If you do not meet any of the aforementioned prerequisites above in “_When to Use Deployment Automation for Higher Environments_”, then you must schedule your deployment.  

Scheduling your deployment is very easy however and all you have to do is fill out a [Deployment Request Form](https://cdcr.sharepoint.com/sites/CDCR_EIS_T_MiddleTierPWA/Lists/DeployRequest/AllItems.aspx) located in SharePoint.  The MT/DevOps team will work with your team to schedule your deployment based on the timeframe you require, but also when it has the least amount of impact on consumers of the MT platform.  You will be notified via email as the deployment requests changes state from a new request to a completed request.  You will also be notified if your deployment request requires any clarification.

## When to Use the Change Control Board (CCB) Process
The CCB process typically involves deployments to Production, but may also apply to deployments to the UAT and Staging clusters.   Although the CCB process does not involve deployments to the Dev cluster, please be mindful of the potential impact to your fellow developers when deploying to MT Dev.  

The CCB process should be used whenever the result of a deployment to an EIS-MiddleTier (MT) cluster will cause an outage that disrupts the daily operations of the end-users of the applications impacted by the deployment.  Outage length of an MT cluster is not the issue as an entire MT cluster can be fully restarted and functional in 5 minutes.  In most cases the MT will not require a restart as only one or two servers or frontends are all that is updated.  The need for the CCB is for end-user awareness to allow them to plan for the outage and to be aware that new application functionality is on the way.

Sometimes this notification to the end-users may cause the end-user to ask that the rollout/deployment of any new functionality await their approval or the approval of third-parties such as Labor or Union representatives.  The project team usually tries to get these types of approvals before the CCB process so that during the CCB meeting, the request will not be rejected.

Deployments to the UAT and Staging clusters will impact CDCR and external testers.  Deployments to Production will impact the daily operations of all end-users of the impacted application(s).  This must be factored into whether the CCB process should be used or not as well.  In addition, an ITS-II or above can provide a justification/exception to bypass the CCB process altogether.

- If the CCB process is required, the [Deployment Request Form](https://cdcr.sharepoint.com/sites/CDCR_EIS_T_MiddleTierPWA/Lists/DeployRequest/AllItems.aspx) will be filled out after CCB approval and before the scheduled deployment date.
- If the CCB process is not required, the [Deployment Request Form](https://cdcr.sharepoint.com/sites/CDCR_EIS_T_MiddleTierPWA/Lists/DeployRequest/AllItems.aspx) can be filled out at any time before the scheduled deployment date.

## The Deployment Request Form
As previously mentioned, deployments of PWA frontend and/or MT backend components to an EIS-MiddleTier (MT) cluster are automated via GHE workflows or DevOps pipelines.  However, when an MT deployment must be scheduled, you may use our Deployment Request Form located in SharePoint to do so via the following link:

https://cdcr.sharepoint.com/sites/CDCR_EIS_T_MiddleTierPWA/Lists/DeployRequest/AllItems.aspx
