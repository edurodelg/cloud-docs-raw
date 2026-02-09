---
merged_at: 2026-02-09T09:45:30.486278
merged_files: 8
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scripts/functions-cli-create-serverless -->

# Create a function app for serverless code execution

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This Azure Functions sample script creates a function app, which is a container for your functions. The function app is created using the [Consumption plan](../consumption-plan), which is ideal for event-driven serverless workloads.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Sample script

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell that you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account.

To open the Cloud Shell, just select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com](https://shell.azure.com).

When Cloud Shell opens, verify that **Bash** is selected for your environment. Subsequent sessions will use Azure CLI in a Bash environment, Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press **Enter** to run it.

### Sign in to Azure

Cloud Shell is automatically authenticated under the initial account signed-in with. Use the following script to sign in using a different subscription, replacing *subscriptionId* with your Azure subscription ID.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

```
subscription="subscriptionId" # Set Azure subscription ID here
az account set -s $subscription # ...or use 'az login'
```


For more information, see [set active subscription](/en-us/cli/azure/account#az-account-set) or [log in interactively](/en-us/cli/azure/reference-index#az-login).

### Run the script

```
# Function app and storage account names must be unique.
# Variable block
let "randomIdentifier=$RANDOM*$RANDOM"
location="eastus"
resourceGroup="msdocs-azure-functions-rg-$randomIdentifier"
tag="create-function-app-consumption"
storage="msdocsaccount$randomIdentifier"
functionApp="msdocs-serverless-function-$randomIdentifier"
skuStorage="Standard_LRS"
functionsVersion="4"
# Create a resource group
echo "Creating $resourceGroup in "$location"..."
az group create --name $resourceGroup --location "$location" --tags $tag
# Create an Azure storage account in the resource group.
echo "Creating $storage"
az storage account create --name $storage --location "$location" --resource-group $resourceGroup --sku $skuStorage
# Create a serverless function app in the resource group.
echo "Creating $functionApp"
az functionapp create --name $functionApp --storage-account $storage --consumption-plan-location "$location" --resource-group $resourceGroup --functions-version $functionsVersion
```


## Clean up resources

Use the following command to remove the resource group and all resources associated with it using the [az group delete](/en-us/cli/azure/group#az-group-delete) command - unless you have an ongoing need for these resources. Some of these resources may take a while to create, as well as to delete.

```
az group delete --name $resourceGroup
```


## Sample reference

Each command in the table links to command specific documentation. This script uses the following commands:

| Command | Notes |
|---|---|
|

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](/en-us/cli/azure).

Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scripts/functions-cli-create-serverless-python -->

# Create a serverless Python function app using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This Azure Functions sample script creates a function app, which is a container for your functions. This script creates an Azure Function app using the [Consumption plan](../consumption-plan).

Note

The function app created runs on Python version 3.9. Python version 3.7 and 3.8 are also supported by Azure Functions.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Sample script

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell that you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account.

To open the Cloud Shell, just select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com](https://shell.azure.com).

When Cloud Shell opens, verify that **Bash** is selected for your environment. Subsequent sessions will use Azure CLI in a Bash environment, Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press **Enter** to run it.

### Sign in to Azure

Cloud Shell is automatically authenticated under the initial account signed-in with. Use the following script to sign in using a different subscription, replacing *subscriptionId* with your Azure subscription ID.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

```
subscription="subscriptionId" # Set Azure subscription ID here
az account set -s $subscription # ...or use 'az login'
```


For more information, see [set active subscription](/en-us/cli/azure/account#az-account-set) or [log in interactively](/en-us/cli/azure/reference-index#az-login).

### Run the script

```
# Function app and storage account names must be unique.
# Variable block
let "randomIdentifier=$RANDOM*$RANDOM"
location="eastus"
resourceGroup="msdocs-azure-functions-rg-$randomIdentifier"
tag="create-function-app-consumption-python"
storage="msdocsaccount$randomIdentifier"
functionApp="msdocs-serverless-python-function-$randomIdentifier"
skuStorage="Standard_LRS"
functionsVersion="4"
pythonVersion="3.9" #Allowed values: 3.7, 3.8, and 3.9
# Create a resource group
echo "Creating $resourceGroup in "$location"..."
az group create --name $resourceGroup --location "$location" --tags $tag
# Create an Azure storage account in the resource group.
echo "Creating $storage"
az storage account create --name $storage --location "$location" --resource-group $resourceGroup --sku $skuStorage
# Create a serverless python function app in the resource group.
echo "Creating $functionApp"
az functionapp create --name $functionApp --storage-account $storage --consumption-plan-location "$location" --resource-group $resourceGroup --os-type Linux --runtime python --runtime-version $pythonVersion --functions-version $functionsVersion
```


## Clean up resources

Use the following command to remove the resource group and all resources associated with it using the [az group delete](/en-us/cli/azure/group#az-group-delete) command - unless you have an ongoing need for these resources. Some of these resources may take a while to create, as well as to delete.

```
az group delete --name $resourceGroup
```


## Sample reference

Each command in the table links to command specific documentation. This script uses the following commands:

| Command | Notes |
|---|---|
|

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](/en-us/cli/azure).

Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scripts/functions-cli-create-app-service-plan -->

# Create a Function App in an App Service plan

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This Azure Functions sample script creates a function app, which is a container for your functions. The function app that is created uses a dedicated App Service plan, which means your server resources are always on.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Sample script

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell that you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account.

To open the Cloud Shell, just select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com](https://shell.azure.com).

When Cloud Shell opens, verify that **Bash** is selected for your environment. Subsequent sessions will use Azure CLI in a Bash environment, Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press **Enter** to run it.

### Sign in to Azure

Cloud Shell is automatically authenticated under the initial account signed-in with. Use the following script to sign in using a different subscription, replacing *subscriptionId* with your Azure subscription ID.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

```
subscription="subscriptionId" # Set Azure subscription ID here
az account set -s $subscription # ...or use 'az login'
```


For more information, see [set active subscription](/en-us/cli/azure/account#az-account-set) or [log in interactively](/en-us/cli/azure/reference-index#az-login).

### Run the script

```
# Function app and storage account names must be unique.
# Variable block
let "randomIdentifier=$RANDOM*$RANDOM"
location="eastus"
resourceGroup="msdocs-azure-functions-rg-$randomIdentifier"
tag="create-function-app-consumption"
storage="msdocsaccount$randomIdentifier"
appServicePlan="msdocs-app-service-plan-$randomIdentifier"
functionApp="msdocs-serverless-function-$randomIdentifier"
skuStorage="Standard_LRS"
skuPlan="B1"
functionsVersion="4"
# Create a resource group
echo "Creating $resourceGroup in "$location"..."
az group create --name $resourceGroup --location "$location" --tags $tag
# Create an Azure storage account in the resource group.
echo "Creating $storage"
az storage account create --name $storage --location "$location" --resource-group $resourceGroup --sku $skuStorage
# Create an App Service plan
echo "Creating $appServicePlan"
az functionapp plan create --name $appServicePlan --resource-group $resourceGroup --location "$location" --sku $skuPlan
# Create a Function App
echo "Creating $functionApp"
az functionapp create --name $functionApp --storage-account $storage --plan $appServicePlan --resource-group $resourceGroup --functions-version $functionsVersion
```


## Clean up resources

Use the following command to remove the resource group and all resources associated with it using the [az group delete](/en-us/cli/azure/group#az-group-delete) command - unless you have an ongoing need for these resources. Some of these resources may take a while to create, as well as to delete.

```
az group delete --name $resourceGroup
```


## Sample reference

Each command in the table links to command specific documentation. This script uses the following commands:

| Command | Notes |
|---|---|
|

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)[az functionapp plan create](/en-us/cli/azure/functionapp/plan#az-functionapp-plan-create)[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](/en-us/cli/azure).

Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scripts/functions-cli-create-premium-plan -->

# Create a function app in a Premium plan - Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This Azure Functions sample script creates a function app, which is a container for your functions. The function app that is created uses a [scalable Premium plan](../functions-premium-plan).

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Sample script

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell that you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account.

To open the Cloud Shell, just select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com](https://shell.azure.com).

When Cloud Shell opens, verify that **Bash** is selected for your environment. Subsequent sessions will use Azure CLI in a Bash environment, Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press **Enter** to run it.

### Sign in to Azure

Cloud Shell is automatically authenticated under the initial account signed-in with. Use the following script to sign in using a different subscription, replacing *subscriptionId* with your Azure subscription ID.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

```
subscription="subscriptionId" # Set Azure subscription ID here
az account set -s $subscription # ...or use 'az login'
```


For more information, see [set active subscription](/en-us/cli/azure/account#az-account-set) or [log in interactively](/en-us/cli/azure/reference-index#az-login).

### Run the script

```
# Function app and storage account names must be unique.
# Variable block
let "randomIdentifier=$RANDOM*$RANDOM"
location="eastus"
resourceGroup="msdocs-azure-functions-rg-$randomIdentifier"
tag="create-function-app-premium-plan"
storage="msdocsaccount$randomIdentifier"
premiumPlan="msdocs-premium-plan-$randomIdentifier"
functionApp="msdocs-function-$randomIdentifier"
skuStorage="Standard_LRS" # Allowed values: Standard_LRS, Standard_GRS, Standard_RAGRS, Standard_ZRS, Premium_LRS, Premium_ZRS, Standard_GZRS, Standard_RAGZRS
skuPlan="EP1"
functionsVersion="4"
# Create a resource group
echo "Creating $resourceGroup in "$location"..."
az group create --name $resourceGroup --location "$location" --tags $tag
# Create an Azure storage account in the resource group.
echo "Creating $storage"
az storage account create --name $storage --location "$location" --resource-group $resourceGroup --sku $skuStorage
# Create a Premium plan
echo "Creating $premiumPlan"
az functionapp plan create --name $premiumPlan --resource-group $resourceGroup --location "$location" --sku $skuPlan
# Create a Function App
echo "Creating $functionApp"
az functionapp create --name $functionApp --storage-account $storage --plan $premiumPlan --resource-group $resourceGroup --functions-version $functionsVersion
```


## Clean up resources

Use the following command to remove the resource group and all resources associated with it using the [az group delete](/en-us/cli/azure/group#az-group-delete) command - unless you have an ongoing need for these resources. Some of these resources may take a while to create, as well as to delete.

```
az group delete --name $resourceGroup
```


## Sample reference

Each command in the table links to command specific documentation. This script uses the following commands:

| Command | Notes |
|---|---|
|

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)[az functionapp plan create](/en-us/cli/azure/functionapp/plan#az-functionapp-plan-create)[specific SKU](../functions-premium-plan#available-instance-skus).[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](/en-us/cli/azure).

Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scripts/functions-cli-create-function-app-connect-to-storage-account -->

# Create a function app with a named Storage account connection

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This Azure Functions sample script creates a function app and connects the function to an Azure Storage account. The created app setting that contains the storage connection string can be used with a [storage trigger or binding](../functions-bindings-storage-blob).

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Sample script

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell that you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account.

To open the Cloud Shell, just select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com](https://shell.azure.com).

When Cloud Shell opens, verify that **Bash** is selected for your environment. Subsequent sessions will use Azure CLI in a Bash environment, Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press **Enter** to run it.

### Sign in to Azure

Cloud Shell is automatically authenticated under the initial account signed-in with. Use the following script to sign in using a different subscription, replacing *subscriptionId* with your Azure subscription ID.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

```
subscription="subscriptionId" # Set Azure subscription ID here
az account set -s $subscription # ...or use 'az login'
```


For more information, see [set active subscription](/en-us/cli/azure/account#az-account-set) or [log in interactively](/en-us/cli/azure/reference-index#az-login).

### Run the script

```
# Function app and storage account names must be unique.
# Variable block
let "randomIdentifier=$RANDOM*$RANDOM"
location="eastus"
resourceGroup="msdocs-azure-functions-rg-$randomIdentifier"
tag="create-function-app-connect-to-storage-account"
storage="msdocsaccount$randomIdentifier"
functionApp="msdocs-serverless-function-$randomIdentifier"
skuStorage="Standard_LRS"
functionsVersion="4"
# Create a resource group
echo "Creating $resourceGroup in "$location"..."
az group create --name $resourceGroup --location "$location" --tags $tag
# Create an Azure storage account in the resource group.
echo "Creating $storage"
az storage account create --name $storage --location "$location" --resource-group $resourceGroup --sku $skuStorage
# Create a serverless function app in the resource group.
echo "Creating $functionApp"
az functionapp create --name $functionApp --resource-group $resourceGroup --storage-account $storage --consumption-plan-location "$location" --functions-version $functionsVersion
# Get the storage account connection string.
connstr=$(az storage account show-connection-string --name $storage --resource-group $resourceGroup --query connectionString --output tsv)
# Update function app settings to connect to the storage account.
az functionapp config appsettings set --name $functionApp --resource-group $resourceGroup --settings StorageConStr=$connstr
```


## Clean up resources

Use the following command to remove the resource group and all resources associated with it using the [az group delete](/en-us/cli/azure/group#az-group-delete) command - unless you have an ongoing need for these resources. Some of these resources may take a while to create, as well as to delete.

```
az group delete --name $resourceGroup
```


## Sample reference

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
|

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)[Consumption plan](../consumption-plan).[az storage account show-connection-string](/en-us/cli/azure/storage/account#az-storage-account-show-connection-string)[az functionapp config appsettings set](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set)## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](/en-us/cli/azure).

Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scripts/functions-cli-create-function-app-github-continuous -->

# Create a function app in Azure that is deployed from GitHub

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This Azure Functions sample script creates a function app using the [Consumption plan](../consumption-plan), along with its related resources. The script also configures your function code for continuous deployment from a public GitHub repository. There is also commented out code for using a private GitHub repository.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Sample script

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell that you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account.

To open the Cloud Shell, just select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com](https://shell.azure.com).

When Cloud Shell opens, verify that **Bash** is selected for your environment. Subsequent sessions will use Azure CLI in a Bash environment, Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press **Enter** to run it.

### Sign in to Azure

Cloud Shell is automatically authenticated under the initial account signed-in with. Use the following script to sign in using a different subscription, replacing *subscriptionId* with your Azure subscription ID.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

```
subscription="subscriptionId" # Set Azure subscription ID here
az account set -s $subscription # ...or use 'az login'
```


For more information, see [set active subscription](/en-us/cli/azure/account#az-account-set) or [log in interactively](/en-us/cli/azure/reference-index#az-login).

### Run the script

```
# Function app and storage account names must be unique.
let "randomIdentifier=$RANDOM*$RANDOM"
location=eastus
resourceGroup="msdocs-azure-functions-rg-$randomIdentifier"
tag="deploy-function-app-with-function-github"
storage="msdocs$randomIdentifier"
skuStorage="Standard_LRS"
functionApp=mygithubfunc$randomIdentifier
functionsVersion="4"
runtime="node"
# Public GitHub repository containing an Azure Functions code project.
gitrepo=https://github.com/Azure-Samples/functions-quickstart-javascript
## Enable authenticated git deployment in your subscription when using a private repo.
#token=<Replace with a GitHub access token when using a private repo.>
#az functionapp deployment source update-token \
# --git-token $token
# Create a resource group.
echo "Creating $resourceGroup in ""$location""..."
az group create --name $resourceGroup --location "$location" --tags $tag
# Create an Azure storage account in the resource group.
echo "Creating $storage"
az storage account create --name $storage --location "$location" --resource-group $resourceGroup --sku $skuStorage
# Create a function app with source files deployed from the specified GitHub repo.
echo "Creating $functionApp"
az functionapp create --name $functionApp --storage-account $storage --consumption-plan-location "$location" --resource-group $resourceGroup --deployment-source-url $gitrepo --deployment-source-branch main --functions-version $functionsVersion --runtime $runtime
# Connect to function application
curl -s "https://${functionApp}.azurewebsites.net/api/httpexample?name=Azure"
```


## Clean up resources

Use the following command to remove the resource group and all resources associated with it using the [az group delete](/en-us/cli/azure/group#az-group-delete) command - unless you have an ongoing need for these resources. Some of these resources may take a while to create, as well as to delete.

```
az group delete --name $resourceGroup
```


## Sample reference

Each command in the table links to command specific documentation. This script uses the following commands:

| Command | Notes |
|---|---|
|

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)[Consumption plan](../consumption-plan)and associates it with a Git or Mercurial repository.## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](/en-us/cli/azure).

Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scripts/functions-cli-create-function-app-connect-to-cosmos-db -->

# Create an Azure Function that connects to an Azure Cosmos DB

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This Azure Functions sample script creates a function app and connects the function to an Azure Cosmos DB database. It makes the connection using an Azure Cosmos DB endpoint and access key that it adds to app settings. The created app setting that contains the connection can be used with an [Azure Cosmos DB trigger or binding](../functions-bindings-cosmosdb).

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Sample script

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell that you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account.

To open the Cloud Shell, just select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com](https://shell.azure.com).

When Cloud Shell opens, verify that **Bash** is selected for your environment. Subsequent sessions will use Azure CLI in a Bash environment, Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press **Enter** to run it.

### Sign in to Azure

Cloud Shell is automatically authenticated under the initial account signed-in with. Use the following script to sign in using a different subscription, replacing *subscriptionId* with your Azure subscription ID.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

```
subscription="subscriptionId" # Set Azure subscription ID here
az account set -s $subscription # ...or use 'az login'
```


For more information, see [set active subscription](/en-us/cli/azure/account#az-account-set) or [log in interactively](/en-us/cli/azure/reference-index#az-login).

### Run the script

```
# Function app and storage account names must be unique.
# Variable block
let "randomIdentifier=$RANDOM*$RANDOM"
location="eastus"
resourceGroup="msdocs-azure-functions-rg-$randomIdentifier"
tag="create-function-app-connect-to-cosmos-db"
storage="msdocsaccount$randomIdentifier"
functionApp="msdocs-serverless-function-$randomIdentifier"
skuStorage="Standard_LRS"
functionsVersion="4"
# Create a resource group
echo "Creating $resourceGroup in "$location"..."
az group create --name $resourceGroup --location "$location" --tags $tag
# Create a storage account for the function app.
echo "Creating $storage"
az storage account create --name $storage --location "$location" --resource-group $resourceGroup --sku $skuStorage
# Create a serverless function app in the resource group.
echo "Creating $functionApp"
az functionapp create --name $functionApp --resource-group $resourceGroup --storage-account $storage --consumption-plan-location "$location" --functions-version $functionsVersion
# Create an Azure Cosmos DB database account using the same function app name.
echo "Creating $functionApp"
az cosmosdb create --name $functionApp --resource-group $resourceGroup
# Get the Azure Cosmos DB connection string.
endpoint=$(az cosmosdb show --name $functionApp --resource-group $resourceGroup --query documentEndpoint --output tsv)
echo $endpoint
key=$(az cosmosdb keys list --name $functionApp --resource-group $resourceGroup --query primaryMasterKey --output tsv)
echo $key
# Configure function app settings to use the Azure Cosmos DB connection string.
az functionapp config appsettings set --name $functionApp --resource-group $resourceGroup --setting CosmosDB_Endpoint=$endpoint CosmosDB_Key=$key
```


## Clean up resources

Use the following command to remove the resource group and all resources associated with it using the [az group delete](/en-us/cli/azure/group#az-group-delete) command - unless you have an ongoing need for these resources. Some of these resources may take a while to create, as well as to delete.

```
az group delete --name $resourceGroup
```


## Sample reference

| Command | Notes |
|---|---|
|

[az storage accounts create](/en-us/cli/azure/storage/account#az-storage-account-create)[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)[Consumption plan](../consumption-plan).[az cosmosdb create](/en-us/cli/azure/cosmosdb#az-cosmosdb-create)[az cosmosdb show](/en-us/cli/azure/cosmosdb#az-cosmosdb-show)[az cosmosdb keys list](/en-us/cli/azure/cosmosdb/keys#az-cosmosdb-keys-list)[az functionapp config appsettings set](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set)## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](/en-us/cli/azure).

More Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scripts/functions-cli-mount-files-storage-linux -->

# Mount a file share to a Python function app using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This Azure Functions sample script creates a function app using the [Consumption plan](../consumption-plan) and creates a share in Azure Files. It then mounts the share so that the data can be accessed by your functions.

Note

The function app created runs on Python version 3.9. Azure Functions also [supports Python versions 3.7 and 3.8](../functions-reference-python#supported-python-versions).

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Sample script

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell that you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account.

To open the Cloud Shell, just select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com](https://shell.azure.com).

When Cloud Shell opens, verify that **Bash** is selected for your environment. Subsequent sessions will use Azure CLI in a Bash environment, Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press **Enter** to run it.

### Sign in to Azure

Cloud Shell is automatically authenticated under the initial account signed-in with. Use the following script to sign in using a different subscription, replacing *subscriptionId* with your Azure subscription ID.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

```
subscription="subscriptionId" # Set Azure subscription ID here
az account set -s $subscription # ...or use 'az login'
```


For more information, see [set active subscription](/en-us/cli/azure/account#az-account-set) or [log in interactively](/en-us/cli/azure/reference-index#az-login).

### Run the script

```
# Function app and storage account names must be unique.
# Variable block
let "randomIdentifier=$RANDOM*$RANDOM"
location="eastus"
resourceGroup="msdocs-azure-functions-rg-$randomIdentifier"
tag="functions-cli-mount-files-storage-linux"
export AZURE_STORAGE_ACCOUNT="msdocsstorage$randomIdentifier"
functionApp="msdocs-serverless-function-$randomIdentifier"
skuStorage="Standard_LRS"
functionsVersion="4"
pythonVersion="3.9" #Allowed values: 3.7, 3.8, and 3.9
share="msdocs-fileshare-$randomIdentifier"
directory="msdocs-directory-$randomIdentifier"
shareId="msdocs-share-$randomIdentifier"
mountPath="/mounted-$randomIdentifier"
# Create a resource group
echo "Creating $resourceGroup in "$location"..."
az group create --name $resourceGroup --location "$location" --tags $tag
# Create an Azure storage account in the resource group.
echo "Creating $AZURE_STORAGE_ACCOUNT"
az storage account create --name $AZURE_STORAGE_ACCOUNT --location "$location" --resource-group $resourceGroup --sku $skuStorage
# Set the storage account key as an environment variable.
export AZURE_STORAGE_KEY=$(az storage account keys list -g $resourceGroup -n $AZURE_STORAGE_ACCOUNT --query '[0].value' -o tsv)
# Create a serverless function app in the resource group.
echo "Creating $functionApp"
az functionapp create --name $functionApp --storage-account $AZURE_STORAGE_ACCOUNT --consumption-plan-location "$location" --resource-group $resourceGroup --os-type Linux --runtime python --runtime-version $pythonVersion --functions-version $functionsVersion
# Work with Storage account using the set env variables.
# Create a share in Azure Files.
echo "Creating $share"
az storage share create --name $share
# Create a directory in the share.
echo "Creating $directory in $share"
az storage directory create --share-name $share --name $directory
# Create webapp config storage account
echo "Creating $AZURE_STORAGE_ACCOUNT"
az webapp config storage-account add \
--resource-group $resourceGroup \
--name $functionApp \
--custom-id $shareId \
--storage-type AzureFiles \
--share-name $share \
--account-name $AZURE_STORAGE_ACCOUNT \
--mount-path $mountPath \
--access-key $AZURE_STORAGE_KEY
# List webapp storage account
az webapp config storage-account list --resource-group $resourceGroup --name $functionApp
```


## Clean up resources

Use the following command to remove the resource group and all resources associated with it using the [az group delete](/en-us/cli/azure/group#az-group-delete) command - unless you have an ongoing need for these resources. Some of these resources may take a while to create, as well as to delete.

```
az group delete --name $resourceGroup
```


## Sample reference

Each command in the table links to command specific documentation. This script uses the following commands:

| Command | Notes |
|---|---|
|

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)[az storage share create](/en-us/cli/azure/storage/share#az-storage-share-create)[az storage directory create](/en-us/cli/azure/storage/directory#az-storage-directory-create)[az webapp config storage-account add](/en-us/cli/azure/webapp/config/storage-account#az-webapp-config-storage-account-add)[az webapp config storage-account list](/en-us/cli/azure/webapp/config/storage-account#az-webapp-config-storage-account-list)## Next steps

For more information on the Azure CLI, see [Azure CLI documentation](/en-us/cli/azure).

Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples).
