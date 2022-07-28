# Overview

Hello there, I am Huy, this is project building a CI/CD Pipeline for 'DevOps Engineer for Microsoft Azure' program from Udacity.

This project consists of flask application that is developed to predict housing prices in Boston (the model is already created by the instructor). 

This repositry demonstrate:
- Deploying the app in Azure CloudShell
- Deploying the app as a web server using Azure App Service.

Once anything has been changed (commits) in the github repositry, it will trigger an action for test automation (CI). A pipeline has been created using Azure DevOps tool, and also any changes will be tested in the pipeline and deployed to app service. All these steps are explianed well in the demo below. 
 

## Project Plan

A [Trello](https://trello.com/b/CSY4dyDy/building-a-ci-cd-pipeline-udacity) board has been created to keep track of the tasks.

A [spreadsheet](project-schedule-h.xlsx) has been created to manage the project schedule.

## Instructions

Here is an architectural diagram:
![arch diagram](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/ArchitechturalDiagram.PNG)

## Deploy the app in Azure Cloud Shell

In Azure Cloud Shell, clone the repo:
```
git clone git@github.com:huytnq/Azure_Devops_Udacity_Project2.git
```
![screenshot-gitClone-AzureCloud](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Clone_Project.PNG)

Create a virtual environment:
```
python3 -m venv ~/.AzureDevops
```

Activate the virtual environment:
```
source ~/.AzureDevops/bin/activate
```

Change into the new directory:
```
cd Azure_Devops_Udacity_Project2
```

Install dependencies in the virtual environment and run tests:
```
make all
```
![make-all](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Make_All.PNG)
![make-all2](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Make_All2.PNG)
![make-all3](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Make_All3.PNG)
![make-all4](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Make_All4.PNG)

A successful GitHub build test 
![screenshot-build-success-actiongithub](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Github_CI_Build.PNG)

## Deploy the app to an Azure App Service

Create an App Service in Azure. In this example the App Service is cicd-nanodegree-haneen and the resource group is flask-app, you can either create it using Azure cloudShell or the portal itself.
In the Azure cloudShell type:

```
az webapp up -n huytnq1-ml-pythonapp -location eastus
```

Next, create the pipeline in Azure DevOps. More information on this process can be found [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops&WT.mc_id=udacity_learn-wwl). The basic steps to set up the pipeline are:

- Go to [https://dev.azure.com](https://dev.azure.com) and sign in.
- Create a new private project.
-Create a new service connection to Azure Resource Manager, select subscription and the app service.
- Create a new pipeline linked to your GitHub repo using GiThub YAML File.

Screenshot of the App Service in Azure:

![screenshot-webapp-service](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/App_Service.PNG)

Screenshot of a successful deployment of the project in Azure Pipelines:

![screenshot-azure-pipeline-deployment](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Azure_Pipelines.PNG)

To test the app running in Azure App Service, edit line 28 of the make_predict_azure_app.sh script with the DNS name of your app. Then run the script:
```
./make_predict_azure_app.sh 
```

If it's working you should see the following output:

![screenshot-prediction](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Make_Predict.PNG)

You can also visit the URL of the App Service via the browser and you should see the following page:

![screenshot-browser](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/App_Service_URL.PNG)

View the app logs:

in the browser bar type: https://huytnq1-ml-pythonapp.scm.azurewebsites.net/api/logs/docker


![screenshot-log-webapp](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/App_Logs.PNG)


> 

## Enhancements
Improving the model performance.

## Load testing

We can use locust to do a load test against our application locally. 

Install locust:
```
pip install locust
```
Ensure the app is running:
```
python app.py
```

Start locust:
```
locust
```
Open a browser and go to [http://localhost:8089](http://localhost:8089). Enter the total number of users to simulate, spawn rate, set the host to your <app-service>, and click Start Swarming:

![screenshot-loadtest](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Lotus_Config.PNG)

You can then watch the load test:

![screenshot-locust](https://raw.githubusercontent.com/huytnq/Azure_Devops_Udacity_Project2/main/Screenshot/Lotus_Load_Test.PNG)

## GET_PASSES_THIS_REPO_UDACITY_PLEASE 
## Demo 

A ![Demo](https://www.youtube.com/watch?v=s3KX6pqJj8A&ab_channel=HuyTNQ)



