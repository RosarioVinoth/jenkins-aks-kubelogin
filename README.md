# jenkins-aks-kubelogin

How to connect to AKS from Jenkins using Kubelogin.

## Setup

### Setup Jenkins
Setup [Jenkins](https://docs.microsoft.com/en-us/azure/developer/jenkins/configure-on-linux-vm)

### Install required packages
apt-get update\
apt-get install unzip\
install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management)

### Create Credentials in Jenkins

1.Create Microsoft Azure Service Principle credential (sp_client_id and sp_client_secret)\
    *id of the credential need to be added to the Jenkinsfile*

2.Create secert file credential (kubeconfig)\
    *kubeconfig have to be populated as shown below and id of the credential need to added to the Jenkinsfile*
    
    > az login -t <tenant_id>
    > az account set -s <subscription_id>
    > az aks get-credentials --resource-group <rg> --name <aks_name> --file <kubeconfig.aks_name>

## Configure Jenkins

1.In the jenkins dashboard, select new item and select pipeline as project.\
2.In the pipeline section select SCM as git and pass this respository url.

## Test

1.Select the job created above and click build now.

# References
[kubelogin1](https://github.com/Azure/kubelogin)\
[kubelogin2](https://stackoverflow.com/questions/54004007/azure-devop-pipelines-authentication-to-aks-with-azure-ad-rbac-configured/54115121#54115121)
