# Azure CLI Subscription and AKS Cluster Creation

## Overview

This guide provides a step-by-step process for selecting an Azure subscription, retrieving necessary information, and creating an Azure Kubernetes Service (AKS) cluster using the Azure CLI.

## Prerequisites

- Azure CLI installed on your machine.
- A valid Azure account (https://portal.azure.com) with the necessary permissions to create resources.

- Install Azure CLI
If you haven’t installed Azure CLI, download it from the official Azure CLI installation page https://learn.microsoft.com/en-us/cli/azure/install-azure-cli .
- Verify Installation
After installation, verify it by opening a command prompt or terminal and running:
```bash
az --version
```

## Steps to Create an AKS Cluster

### Step 1: Log in to Azure

### log in to your Azure account. This command will prompt a browser window for authentication.

```bash
az login --tenant 'XXXXX-XXXX-XXXX-XXXX'
```

### Step 2: Get and Set the Desired Subscription ID
To get a list of available subscriptions, use the following command:

```bash
az account list --output table

```
From the list, note the SubscriptionId you want to use. Then, set it as the active subscription:

```bash for cmd
set SUBSCRIPTION_ID=0cf17461-0023-4636-8167-0ae9e684107d
az account set --subscription %SUBSCRIPTION_ID%

echo %SUBSCRIPTION_ID%
```
```bash for powershell
$SUBSCRIPTION_ID="0cf17461-0023-4636-8167-0ae9e684107d"
az account set --subscription $SUBSCRIPTION_ID
```
### Step 3: Create a Resource Group
Create a resource group where all your resources for the AKS cluster will reside:

```bash
az group create --name aks-rg1 --location eastus

```
### Step 4: Retrieve and Set the Latest Kubernetes Version

``` bash cmd
for /f "delims=" %i in ('az aks get-versions --location eastus --query "values[?isPreview==null].version | [-1]" -o tsv') do set LATEST_VERSION=%i
```
``` powershell
$LATEST_VERSION = az aks get-versions --location eastus --query "values[?isPreview==null].version | [-1]" -o tsv
echo $LATEST_VERSION
```
### step 5: Create a Service Principal and Extract Credentials
Create a service principal and extract the APP_ID and CLIENT_SECRET into variables:

```bash
set SP_INFO=$(az ad sp create-for-rbac --skip-assignment --output json) 
set APP_ID=$(echo $SP_INFO | jq -r '.appId') 
set CLIENT_SECRET=$(echo $SP_INFO | jq -r '.password')
```
``` bash cmd
for /f "delims=" %i in ('powershell -Command "az ad sp create-for-rbac --skip-assignment --output json"') do set SP_INFO=%i
powershell -Command "$env:SP_INFO='%SP_INFO%'; $appId = ($env:SP_INFO | ConvertFrom-Json).appId; Write-Host $appId"

```
``` bash powershell
$SP_INFO = az ad sp create-for-rbac --skip-assignment --output json | ConvertFrom-Json
$APP_ID = $SP_INFO.appId
$CLIENT_SECRET = $SP_INFO.password

```
Note: Ensure jq is installed on your system for parsing JSON in the shell. You can install it via apt-get install jq on Ubuntu/Debian, brew install jq on macOS, or choco install jq on Windows (using Chocolatey).

### Step 6: Create the AKS Cluster
With the variables set, you can now create the AKS cluster:
``` bash
az aks create --resource-group aks-rg1 --name aksdemo1 --location eastus --node-count 1 --enable-addons monitoring --enable-cluster-autoscaler --min-count 1 --max-count 5 --node-vm-size Standard_D2pds_v6 --kubernetes-version $LATEST_VERSION --network-plugin azure --service-principal $APP_ID --client-secret $CLIENT_SECRET --zones 1 2 3 --generate-ssh-keys
```

``` bash
az aks create --resource-group aks-rg1 --name aksdemo1 --location centralindia --node-count 3 --enable-addons monitoring --generate-ssh-keys --kubernetes-version $LATEST_VERSION --enable-cluster-autoscaler --min-count 1 --max-count 5
```

### --enable-private-cluster
This flag ensures that the API server's traffic is routed through a private IP address inside the Azure Virtual Network (VNet) and cannot be accessed over the public internet. Even if the --enable-private-cluster-publicFqdn option is enabled (as it was in your case), the traffic is still being routed through private endpoints.
What Happens When a Cluster Is Private:
API Server Access: By enabling the private cluster option, the Kubernetes API server is only accessible from within the VNet or peered VNets. If your machine is not in that VNet, you cannot access the API server directly.
Public DNS: The public DNS for the API server may still exist, but it resolves to the private endpoint when accessed from within the Azure network.
Private DNS Zone: Azure sets up a private DNS zone for the cluster, allowing private IP addresses to be used for the Kubernetes API server in the VNet.

#### Issues -
1) if you are getting error with new account please run the below command to set the namespace
``` bash
az provider register --namespace Microsoft.ContainerService

az provider show --namespace Microsoft.ContainerService --query "registrationState"

```
2) Preflight validation check for resource(s) for container service aksdemo in resource group aksdemo_group failed. Message: Insufficient regional vcpu quota left for location centralindia. left regional vcpu quota 0, requested quota 8. Details:

first check usage in different region using below command if it is available or not
``` bash
az vm list-usage -l eastus -o table
```
https://learn.microsoft.com/en-us/answers/questions/2088453/(errcode-insufficientvcpuquota)-insufficient-regio

3) (AddContainerInsightsSolutionError) Code="MissingSubscriptionRegistration" Message="The subscription is not registered to use namespace 'Microsoft.OperationsManagement'. See https://aka.ms/rps-not-found for how to register subscriptions." Details=[{"code":"MissingSubscriptionRegistration","message":"The subscription is not registered to use namespace 'Microsoft.OperationsManagement'. See https://aka.ms/rps-not-found for how to register subscriptions.","target":"Microsoft.OperationsManagement"}]
Code: AddContainerInsightsSolutionError

run the below commands to register namespace
``` bash
az provider register --namespace Microsoft.OperationsManagement
az provider show --namespace Microsoft.OperationsManagement --query "registrationState"
```

### Step 7: Install AKS cli to connect with local cmd or poershell

``` bash
az aks install-cli
```
### Step 8: Configure cluster Credentials (kube config)
``` bash
az aks get-credentials --resource-group aks-rg1 --name aksdemo1
```

### Step 9: List AKS Node
``` bash
kubectl get nodes -o wide
```
### To see the AKS config context if cluster dns is private
Use kubectl config get-contexts to list all contexts.
Use kubectl config current-context to see the active context.
Use kubectl config use-context <context-name> to switch to another context.

# Note: Delete the cluster
``` bash 
az aks delete --resource-group aks-rg1 --name aksdemo1 --yes --no-wait
```
