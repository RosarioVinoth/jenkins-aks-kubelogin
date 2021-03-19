# jenkins-aks-kubelogin

## Setup

### Setup Jenkins
Setup [Jenkins](https://docs.microsoft.com/en-us/azure/developer/jenkins/configure-on-linux-vm)

### Install required packages
apt-get update\
apt-get install unzip\
install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management)

### Create Credentials

1.Create Microsoft Azure Service Principle credentials (sp_client_id and sp_client_secret)\
2.Create secert file (kubeconfig)

> az login -t <tenant_id>\
> az account set -s <subscription_id>\
> az aks get-credentials --resource-group <rg> --name <aks_name> --file <kubeconfig.aks_name>

Create Secret file by uploading the kubeconfig created in above setup


Create new pipeline project with the code below.
