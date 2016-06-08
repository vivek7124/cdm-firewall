# CDM Firewall

This project contains the configuration files in yaml for managing the Google Cloud Platform project network firewall configurations. The yamls contained within this project will be used by the Google Cloud Platforms [Cloud Deployment Manager](https://cloud.google.com/deployment-manager/overview). Each yaml file within the root of the repository correlates to a project that the rules are applied to. This allows for applying different rules across different projects. Also the actual firewall rules are within the rules directory. When a new firewall rule is created a yaml for that rule will be added to this folder and added appropriately to the project yamls where the rule needs to go.

This project only contains firewall rules which would need to be applied to a new project after its network is stood up using the CDM deployment in [cdm-platform](https://git.hdtechlab.com/cloud/cdm-platform). The cdm-platform repository is used to setup all of the necessary networks, storage, load balancers, etc.

## Installation

Utilizing Cloud Deployment Manager locally requires the Google Cloud Platform [Cloud SDK](https://cloud.google.com/sdk/). Local usage is covered in the usage section below. For continuous deployment to the environment the build environment will utilize runners in the projects to execute the deployments as needed.

Additionally, this repository has a submodule that contains the Cloud Deployment Manager templates for use with these deployments. The template project can be found at https://git.hdtechlab.com/cloud/cdm-templates. When you clone this repository you will need to run the following command to pull the submodule:

`git submodule update --init`

## Usage

When executing a deployment it is important to understand the existing state that your deployment is in. For instance, if deploying something completely new you will pass the create command within the command below. Otherwise, you will pass update or delete to an already deployed deployment.

### Local Usage

For executing a deployment locally from the command line, ensure that you are already authenticated to Google Cloud, and use the following with substitutions as necessary:

`gcloud deployment-manager deployments {create | update | delete} deployment name --config internal.yaml --project hd-www-dev`

### Continuous Delivery

When delivering deployments via a continuous delivery method, the automated build system will handle executing the deployment for you via a runner within the appropriate project. All that will need to be supplied is the repo and deployment.

## Rule Add / Update Requests

To submit changes to this repository the use of GitLab's [Forking Workflow](http://doc.gitlab.com/ee/workflow/forking_workflow.html) will be used.

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-firewall-rule`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-firewall-rule`
5. Checkout master: `git checkout master`
6. Merge your change to master: `git merge my-new-firewall-rule`
7. Commit your merge to master: `git commit`
5. Submit a merge request and include @IT_Security_Firewall_Compliance_Review at the top description with the inclusion of a description of your new rule and application of it.
