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

```bash
for cmd
set SUBSCRIPTION_ID=cdcf4dd7-6f73-46d6-b098-e01bbef0f315
az account set --subscription %SUBSCRIPTION_ID%
```
```bash
for powershell
$SUBSCRIPTION_ID="your-subscription-id"
az account set --subscription $SUBSCRIPTION_ID
```
### Step 3: Create a Resource Group
Create a resource group where all your resources for the AKS cluster will reside:

```bash
az group create --name aks-rg1 --location eastus

```
### Step 4: Retrieve and Set the Latest Kubernetes Version

```
set LATEST_VERSION=$(az aks get-versions --location eastus --query 'orchestrators[-1].orchestratorVersion' --output tsv)
```

### step 5: Create a Service Principal and Extract Credentials
Create a service principal and extract the APP_ID and CLIENT_SECRET into variables:

```bash
set SP_INFO=$(az ad sp create-for-rbac --skip-assignment --output json) 
set APP_ID=$(echo $SP_INFO | jq -r '.appId') 
set CLIENT_SECRET=$(echo $SP_INFO | jq -r '.password')

$SP_INFO = az ad sp create-for-rbac --skip-assignment --output json | ConvertFrom-Json
$APP_ID = $SP_INFO.appId
$CLIENT_SECRET = $SP_INFO.password

```
Note: Ensure jq is installed on your system for parsing JSON in the shell. You can install it via apt-get install jq on Ubuntu/Debian, brew install jq on macOS, or choco install jq on Windows (using Chocolatey).

### Step 6: Create the AKS Cluster
With the variables set, you can now create the AKS cluster:
```bash
az aks create --resource-group aks-rg1 --name aksdemo1 --location centralus --node-count 1 --enable-addons monitoring --enable-cluster-autoscaler --min-count 1 --max-count 5 --node-vm-size Standard_DS2_v2 --kubernetes-version $LATEST_VERSION --network-plugin azure --service-principal $APP_ID --client-secret $CLIENT_SECRET --zones 1 2 3 --enable-private-cluster --generate-ssh-keys

  ```


