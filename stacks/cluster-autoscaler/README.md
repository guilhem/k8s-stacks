# Cluster Autoscaler Stack

This stack allows you to deploy the following components:

* [cluster-autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler)


## Usage

Once you have fill all the prerequisites, you can now deploy this stack on your cluster. To do it, export the following variables:

```bash
export AZ_CLIENT_ID=<YOUR_SP_CLIENT_ID> 
export AZ_CLIENT_SECRET=<YOUR_SP_CLIENT_SECRET> 
export AZ_SUBSCRIPTION_ID=<YOUR_SUBSCRIPTION_ID>
export AZ_TENANT_ID=<YOUR_TENANT_ID>
export AZ_RESOURCE_GROUP=<YOUR_AKS_RESOURCE_GROUP>
export AZ_NODE_RESOURCE_GROUP=<YOUR_AKS_RESOURCES_RESOURCE_GROUP> 
export AZ_CLUSTER_NAME=<YOUR_CLUSTER_NAME> 
export AZ_NODE_POOL_NAME=<YOUR_AKS_NODE_POOL_NAME>
```

Once done, run the installation

```bash
helmfile apply
```

## Helper

To easily get the previous information, you can use Azure CLI 

### Login to Azure using Azure CLI

```bash
az login
```

### Check if you are in the right subscription

```bash
az account show
az account set -s <YOUR_SUBSCRIPTION>
```

### Export the required variables 

```bash
# Export your service principal credentials
export AZ_CLIENT_ID=<YOUR_SP_CLIENT_ID> 
export AZ_CLIENT_SECRET=<YOUR_SP_CLIENT_SECRET>
 
# Export your AKS Resource Group & Cluster Name (the one from Azure, NOT the Rancher display name)
export AZ_RESOURCE_GROUP=<YOUR_RESOURCE_GROUP>
export AZ_CLUSTER_NAME=<YOUR_CLUSTER_NAME>

# Fetch your Subscription ID
export AZ_SUBSCRIPTION_ID=`az account list --query '[?isDefault].id' -o tsv`

# Fetch your Tenant ID
export AZ_TENANT_ID=`az account list --query '[?isDefault].tenantId' -o tsv`

# Fetch your AKS components Resource Group (MC_XXXX)
export AZ_NODE_RESOURCE_GROUP=$(az group list --query "[?starts_with(name, 'MC_${AZ_RESOURCE_GROUP}_${AZ_CLUSTER_NAME}')].name" --output tsv)

# Fetch your AKS node pool name
export AZ_NODE_POOL_NAME=`az aks show -n ${AZ_CLUSTER_NAME} --resource-group ${AZ_RESOURCE_GROUP} --query agentPoolProfiles[].name -o tsv`
```
