# adf-workflow-template
This is an example template to implement CI/CD as a Data Engineer using GitHub Actions to deploy ARM template to Azure Data Factory.

## Why a data engineer should implement CI/CD?
- Automated testing: Automating the deployment of code to production ensures consistency and minimizes human errors.
- Consistent deployments: Automating the deployment of code to production ensures consistency and minimizes human errors.
- Rapid feedback: A CI/CD process provides rapid feedback on any issues with the code, allowing the team to quickly identify and address the problem.
- Continuous improvement: Continuous improvement of the code and pipeline can prevent similar issues from occurring in the future and ensure that the pipeline is always operating at peak efficiency.

## GitHub Actions
In GitHub Actions, a workflow is described in a YAML file and is made up of steps that are done in order. These steps can run on runners provided by GitHub or on runners that you host yourself. Workflows are run on Runners, which are computing resources that can be customized with specific tools and settings as needed. Workflow yml files are stored in .github/workflows subfolder.

## Try this template
Create a new repo using this template:
![image](https://github.com/Karenzhang7717/adf-workflow-template/assets/64809520/dce9abff-56f0-44e4-8ba8-d9efab47cd0e)
Clone the repo:
```bash
[pip install foobar](https://github.com/Karenzhang7717/adf-workflow-template.git)
```
## Prerequisites
Prerequisites:
- Azure Subscription
- Azure Data Factory instance
-GitHub repository integration set up. (follow the steps here to set it up if you do not have it set up already)

## Generate deployment credentials
You must generate credentials to authenticate and authorize GitHub Actions to deploy your ARM template to the specified Data Factory. Using the Azure CLI command 

```bash
az ad sp create-for-rbac --name {myApp} --role contributor --scopes /subscriptions/{subscription- id}/resourceGroups/{MyResourceGroup} --sdk-auth 
```

you can create a service principal. Execute this command in the Azure portal or locally using Azure Cloud Shell. Replace the placeholder 'myApp' with your application's name.

## Configure the GitHub secrets

- Go to your repository on GitHub. 
![image](https://github.com/Karenzhang7717/adf-workflow-template/assets/64809520/10008c86-b59e-4b1b-bbcb-50dbf2bd6242)

- Choose Configuration > Secrets > New secret. 
- Copy the entire JSON output from the Azure CLI command and paste it into the value field of the secret. Name the confidential information 'AZURE_CREDENTIALS'. 
- Create a new secret 'AZURE_RG'. Add the name of your resource group to the value field of the secret. 
- Create a new secret titled 'AZURE_SUBSCRIPTION'. Add your subscription ID to the value field of the secret.
![image](https://github.com/Karenzhang7717/adf-workflow-template/assets/64809520/d1407ef3-fbb6-423f-897e-e0ac3e91fbcc)

## Step by step guidance to create GitHub Workflow yml file
please see here: https://medium.com/@karenzhang7717/automate-data-engineering-deployment-with-github-actions-36b6bf499533

## Testing the workflow
Since in the workflow file, we specified any changes in the adf_publish branch will trigger the workflow, to test that everything is set up properly, make some changes in your Dev ADF instance and Publish these. This should trigger the workflow to execute.
To check it, browse to the repository -> Actions -> and identify your workflow.
![image](https://github.com/Karenzhang7717/adf-workflow-template/assets/64809520/e8407505-6d5a-4d77-b10e-719f99341e1a)

You can further drill down into each execution and see more details such as all the steps and their duration.
![image](https://github.com/Karenzhang7717/adf-workflow-template/assets/64809520/e192b679-9c1b-4cda-bc8f-6be4d6c3c3a9)



