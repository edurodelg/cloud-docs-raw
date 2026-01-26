---
merged_at: 2026-01-26T23:29:57.702763
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-how-to -->

# Create and manage function apps in the Flex Consumption plan

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create function apps hosted in the [Flex Consumption plan](flex-consumption-plan) in Azure Functions. It also shows you how to manage certain features of a Flex Consumption plan hosted app.

Function app resources are langauge-specific. Make sure to choose your preferred code development language at the beginning of the article.

## Prerequisites

An Azure account with an active subscription. If you don't already have one, you can

[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).: used to create and manage resources in Azure. When using the Azure CLI on your local computer, make sure to use version 2.60.0, or a later version. You can also use[Azure CLI](/en-us/cli/azure/install-azure-cli)[Azure Cloud Shell](../cloud-shell/overview), which has the correct Azure CLI version.: used to create and develop apps, create Azure resources, and deploy code projects to Azure. When using Visual Studio Code, make sure to also install the latest[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). You can also install the[Azure Tools extension pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack).While not required to create a Flex Consumption plan app, you need a code project to be able to deploy to and validate a new function app. Complete the first part of one of these quickstart articles, where you create a code project with an HTTP triggered function:

[Create an Azure Functions project from the command line](how-to-create-function-azure-cli)[Create an Azure Functions project using Visual Studio Code](how-to-create-function-vs-code)

To create an app in a new Flex Consumption plan during a Maven deployment, you must create your local app project and then update the project's pom.xml file. For more information, see

[Create a Java Flex Consumption app using Maven](#create-and-deploy-your-app-using-maven)Return to this article after you create and run the local project, but before you're asked to create Azure resources. You create the function app and other Azure resources in the next section.


## Create a Flex Consumption app

This section shows you how to create a function app in the Flex Consumption plan by using either the Azure CLI, Azure portal, or Visual Studio Code. For an example of creating an app in a Flex Consumption plan using Bicep/ARM templates, see the [Flex Consumption repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md#iac-samples-overview).

You can skip this section if you choose to instead [create and deploy your app using Maven](#create-and-deploy-your-app-using-maven).

To support your function code, you need to create three resources:

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A
[Storage account](../storage/common/storage-account-create), which is used to maintain state and other information about your functions. - A function app in the Flex Consumption plan, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources in the Flex Consumption plan.

If you haven't done so already, sign in to Azure:

`az login`

The

command signs you into your Azure account.`az login`

Use the

`az functionapp list-flexconsumption-locations`

command to review the list of regions that currently support Flex Consumption in alphabetical order.`az functionapp list-flexconsumption-locations --query "sort_by(@, &name)[].{Region:name}" -o table`


Create a resource group in one of the currently supported regions listed by the command in the previous step.

`az group create --name <RESOURCE_GROUP> --location <REGION>`

In the previous command, replace

`<RESOURCE_GROUP>`

with a value that's unique in your subscription and`<REGION>`

with one of the currently supported regions. The[az group create](/en-us/cli/azure/group#az-group-create)command creates a resource group.Create a general-purpose storage account in your resource group and region:

`az storage account create --name <STORAGE_NAME> --location <REGION> --resource-group <RESOURCE_GROUP> --sku Standard_LRS --allow-blob-public-access false`

In the previous example, replace

`<STORAGE_NAME>`

with a name that's appropriate to you and unique in Azure Storage. Names must contain three to 24 characters consisting of numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account that Azure Functions supports according to[storage account requirements](storage-considerations#storage-account-requirements). The[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)command creates the storage account.Important

The storage account is used to store important app data, sometimes including the application code itself. You should limit access from other apps and users to the storage account.

Create the function app in Azure:

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime dotnet-isolated --runtime-version 8.0`

[C# apps that run in-process](functions-dotnet-class-library)aren't currently supported when running in a Flex Consumption plan.`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime java --runtime-version 17`

For Java apps, Java 11 is also currently supported.

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime node --runtime-version 20`

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime python --runtime-version 3.11`

For Python apps, Python 3.10 is also currently supported.

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime powershell --runtime-version 7.4`

In this example, replace both

`<RESOURCE_GROUP>`

and`<STORAGE_NAME>`

with the resource group and the name of the account you used in the previous step, respectively. Also replace`<APP_NAME>`

with a globally unique name appropriate to you. The`<APP_NAME>`

is also the default domain name server (DNS) domain for the function app. Thecommand creates the function app in Azure.`az functionapp create`

This command creates a function app running in the Flex Consumption plan.

Because you created the app without specifying

[always ready instances](#set-always-ready-instance-counts), your app only incurs costs when actively executing functions. The command also creates an associated Azure Application Insights instance in the same resource group, with which you can monitor your function app and view logs. For more information, see[Monitor Azure Functions](functions-monitoring).

## Deploy your code project

For deployment, Flex Consumption plan apps use a Blob storage container to host .zip package files that contain your project code and all libraries that are required for your app to run. For more information, see [Deployment](flex-consumption-plan#deployment).

You can skip this section if you choose to instead [create and deploy your app using Maven](#create-and-deploy-your-app-using-maven).

You can choose to deploy your project code to an existing function app using various tools:

You can use the Azure CLI to upload a deployment package file to the deployment share for a function app in Azure. To make this deployment, you must produce a .zip package file that can run when the package is mounted to your app.

This package file must contain all of the build output files and referenced libraries required for your project to run.

For projects with a large number of libraries, you should package the root of your project file and request a [remote build](functions-deployment-technologies#remote-build).

For Python projects, you should package the root of your project file and always request a [remote build](functions-deployment-technologies#remote-build). Using a remote build prevents potential issues that can occur when you build a project on Windows to be deployed on Linux.

Using your preferred development tool, build the code project.

Create a .zip file that contains the output of the build directory. For more information, see

[Project structure](dotnet-isolated-process-guide#project-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP>`


Using your preferred development tool, build the code project.

Create a .zip file that contains the output of the build directory. For more information, see

[Folder structure](functions-reference-java#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP>`


Create a .zip file that contains the root directory of your code project. For more information, see

[Folder structure](functions-reference-powershell#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP>`


Create a .zip file that contains the root directory of your code project. For more information, see

[Folder structure](functions-reference-node#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP> --build-remote true`

Make sure to set

`--build-remote true`

to perform a[remote build](functions-deployment-technologies#remote-build).

Create a .zip file that contains the root directory of your code project. For more information, see

[Folder structure](functions-reference-python#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP> --build-remote true`

Make sure to set

`--build-remote true`

to perform a[remote build](functions-deployment-technologies#remote-build).

## Create and deploy your app using Maven

You can use Maven to create a Flex Consumption hosted function app and required resources during deployment by modifying the pom.xml file.

Create a Java code project by completing the first part of one of these quickstart articles:

In your Java code project, open the pom.xml file and make these changes to create your function app in the Flex Consumption plan:

Change the value of

`<properties>.<azure.functions.maven.plugin.version>`

to`1.34.0`

.In the

`<plugin>.<configuration>`

section for the`azure-functions-maven-plugin`

, add or uncomment the`<pricingTier>`

element as follows:`<pricingTier>Flex Consumption</pricingTier>`


(Optional) Customize the Flex Consumption plan in your Maven deployment by also including these elements in the

`<plugin>.<configuration>`

section: .`<instanceSize>`

- sets the[instance memory](flex-consumption-plan#instance-sizes)size for the function app. The default value is`2048`

.`<maximumInstances>`

- sets the highest value for the maximum instances count of the function app.`<alwaysReadyInstances>`

- sets the[always ready instance counts](flex-consumption-plan#always-ready-instances)with child elements for HTTP trigger groups (`<http>`

), Durable Functions groups (`<durable>`

), and other specific triggers (`<my_function>`

). When you set any instance count greater than zero, you're charged for these instances whether your functions execute or not. For more information, see[Billing](flex-consumption-plan#billing).

Before you can deploy, sign in to your Azure subscription using the Azure CLI.

`az login`

The

command signs you into your Azure account.`az login`

Use the following command to deploy your code project to a new function app in Flex Consumption.

`mvn azure-functions:deploy`

Maven uses settings in the pom.xml template to create your function app in a Flex Consumption plan in Azure, along with the other required resources. Should these resources already exist, the code is deployed to your function app, overwriting any existing code.


## Enable virtual network integration

You can enable [virtual network integration](functions-networking-options#virtual-network-integration) for your app in a Flex Consumption plan. The examples in this section assume that your account already contains a [virtual network and subnet](../virtual-network/quick-create-cli#create-a-virtual-network-and-subnet). You can enable virtual network integration when you create your app or at a later time.

Important

The Flex Consumption plan currently doesn't support subnets with names that contain underscore (`_`

) characters.

To enable virtual networking when you create your app:

You can enable virtual network integration by running the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command and including the

`--vnet`

and `--subnet`

parameters.[Create the virtual network and subnet](../virtual-network/quick-create-cli#create-a-virtual-network-and-subnet), if you don't have one already.Complete steps 1-4 in

[Create a Flex Consumption app](#create-a-flex-consumption-app)to create the resources required by your app.Run the

command, including the`az functionapp create`

`--vnet`

and`--subnet`

parameters, as in this example:`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime <RUNTIME_NAME> --runtime-version <RUNTIME_VERSION> --vnet <VNET_RESOURCE_ID> --subnet <SUBNET_NAME>`

The

`<VNET_RESOURCE_ID>`

value is the resource ID for the virtual network, which is in the format:`/subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP>/providers/Microsoft.Network/virtualNetworks/<VNET_NAME>`

. You can use this command to get a list of virtual network IDs, filtered by`<RESOURCE_GROUP>`

:`az network vnet list --resource-group <RESOURCE_GROUP> --output tsv --query "[]".id`

.

For end-to-end examples of how to create apps in Flex Consumption with virtual network integration see these resources:

[Flex Consumption: HTTP to Event Hubs using virtual network integration](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md)[Flex Consumption: triggered from Service Bus using virtual network integration](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md)

To modify or delete virtual network integration in an existing app:

Use the [ az functionapp vnet-integration add](/en-us/cli/azure/functionapp/vnet-integration#az-functionapp-vnet-integration-add) command to enable virtual network integration to an existing function app:

```
az functionapp vnet-integration add --resource-group <RESOURCE_GROUP> --name <APP_NAME> --vnet <VNET_RESOURCE_ID> --subnet <SUBNET_NAME>
```


Use the [ az functionapp vnet-integration remove](/en-us/cli/azure/functionapp/vnet-integration#az-functionapp-vnet-integration-remove) command to disable virtual network integration in your app:

```
az functionapp vnet-integration remove --resource-group <RESOURCE_GROUP> --name <APP_NAME>
```


Use the [ az functionapp vnet-integration list](/en-us/cli/azure/functionapp/vnet-integration#az-functionapp-vnet-integration-list) command to list the current virtual network integrations for your app:

```
az functionapp vnet-integration list --resource-group <RESOURCE_GROUP> --name <APP_NAME>
```


When you're choosing a subnet, these considerations apply:

- The subnet you choose can't already be used for other purposes, such as with private endpoints or service endpoints, or be delegated to any other hosting plan or service.
- You can't share the same subnet between a Container Apps environment and a Flex Consumption app.
- You can share the same subnet with more than one app running in a Flex Consumption plan. Because the networking resources are shared across all apps, one function app might affect the performance of others on the same subnet.
- In a Flex Consumption plan, a single function app might use up to 40 IP addresses, even when the app scales beyond 40 instances. While this rule of thumb is helpful when estimating the subnet size you need, it isn't strictly enforced.

## Configure deployment settings

In the Flex Consumption plan, the deployment package that contains your app's code is maintained in an Azure Blob Storage container. By default, deployments use the same storage account (`AzureWebJobsStorage`

) and connection string value used by the Functions runtime to maintain your app. The connection string is stored in the `DEPLOYMENT_STORAGE_CONNECTION_STRING`

application setting. However, you can instead designate a blob container in a separate storage account as the deployment source for your code. You can also change the authentication method used to access the container.

A customized deployment source should meet this criteria:

- The storage account must already exist.
- The container to use for deployments must also exist.
- When more than one app uses the same storage account, each should have its own deployment container. Using a unique container for each app prevents the deployment packages from being overwritten, which would happen if apps shared the same container.

When configuring deployment storage authentication, keep these considerations in mind:

- As a security best practice, you should use managed identities when connecting to Azure Storage from your apps. For more information, see
[Connections](functions-reference#connections). - When you use a connection string to connect to the deployment storage account, the application setting that contains the connection string must already exist.
- When you use a user-assigned managed identity, the provided identity gets linked to the function app. The
`Storage Blob Data Contributor`

role scoped to the deployment storage account also gets assigned to the identity. - When you use a system-assigned managed identity, an identity gets created when a valid system-assigned identity doesn't already exist in your app. When a system-assigned identity does exists, the
`Storage Blob Data Contributor`

role scoped to the deployment storage account also gets assigned to the identity.

To configure deployment settings when you create your function app in the Flex Consumption plan:

Use the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command and supply these extra options that customize deployment storage:

| Parameter | Description |
|---|---|
`--deployment-storage-name` |
The name of the deployment storage account. |
`--deployment-storage-container-name` |
The name of the container in the account to contain your app's deployment package. |
`--deployment-storage-auth-type` |
The authentication type to use for connecting to the deployment storage account. Accepted values include `StorageAccountConnectionString` , `UserAssignedIdentity` , and `SystemAssignedIdentity` . |
`--deployment-storage-auth-value` |
When using `StorageAccountConnectionString` , this parameter is set to the name of the application setting that contains the connection string to the deployment storage account. When you set `UserAssignedIdentity` , this parameter is set to the name of the resource ID of the identity you want to use. |

This example creates a function app in the Flex Consumption plan with a separate deployment storage account and user assigned identity:

```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_NAME> --runtime dotnet-isolated --runtime-version 8.0 --flexconsumption-location "<REGION>" --deployment-storage-name <DEPLOYMENT_ACCOUNT_NAME> --deployment-storage-container-name <DEPLOYMENT_CONTAINER_NAME> --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value <MI_RESOURCE_ID>
```


You can also modify the deployment storage configuration for an existing app.

Use the [ az functionapp deployment config set](/en-us/cli/azure/functionapp/deployment/config#az-functionapp-deployment-config-set) command to modify the deployment storage configuration:

```
az functionapp deployment config set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --deployment-storage-name <DEPLOYMENT_ACCOUNT_NAME> --deployment-storage-container-name <DEPLOYMENT_CONTAINER_NAME>
```


## Configure instance memory

The instance memory size used by your Flex Consumption plan can be explicitly set when you create your app. For more information about supported sizes, see [Instance sizes](flex-consumption-plan#instance-sizes).

To set an instance memory size that's different from the default when creating your app:

Specify the `--instance-memory`

parameter in your [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command. This example creates a C# app with an instance size of

`4096`

:```
az functionapp create --instance-memory 4096 --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime dotnet-isolated --runtime-version 8.0
```


At any point, you can change the instance memory size setting used by your app.

This example uses the [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to change the instance memory size setting to 512 MB:

```
az functionapp scale config set --resource-group <resourceGroup> --name <APP_NAME> --instance-memory 512
```


## Set always ready instance counts

You can set a specific number of always ready instances for the [Per-function scaling](flex-consumption-plan#per-function-scaling) groups or individual functions, to keep your functions loaded and ready to execute. There are three special groups, as in per-function scaling:

`http`

- All of the HTTP triggered functions in the app scale together into their own instances.`durable`

- All of the Durable triggered functions (Orchestration, Activity, Entity) in the app scale together into their own instances.`blob`

- All of the blob (Event Grid) triggered functions in the app scale together into their own instances.

Use `http`

, `durable`

, or `blob`

as the name for the name value pair setting to configure always ready counts for these groups. For all other functions in the app you need to configure always ready for each individual function using the format `function:<FUNCTION_NAME>=n`

.

To define one or more always ready instance designations, use the `--always-ready-instances`

parameter with the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command. This example sets the always ready instance count for all HTTP triggered functions to

`10`

:```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_NAME> --runtime <LANGUAGE_RUNTIME> --runtime-version <RUNTIME_VERSION> --flexconsumption-location <REGION> --always-ready-instances http=10
```


This example sets the always ready instance count for all Durable trigger functions to `3`

and sets the always ready instance count to `2`

for a service bus triggered function named `function5`

:

```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_NAME> --runtime <LANGUAGE_RUNTIME> --runtime-version <RUNTIME_VERSION> --flexconsumption-location <REGION> --always-ready-instances durable=3 function:function5=2
```


You can also modify always ready instances on an existing app by adding or removing instance designations or by changing existing instance designation counts.

This example uses the [ az functionapp scale config always-ready set](/en-us/cli/azure/functionapp/scale/config/always-ready#az-functionapp-scale-config-always-ready-set) command to change the always ready instance count for the HTTP triggers group to

`10`

:```
az functionapp scale config always-ready set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --settings http=10
```


To remove always ready instances, use the [ az functionapp scale config always-ready delete](/en-us/cli/azure/functionapp/scale/config/always-ready#az-functionapp-scale-config-always-ready-delete) command, as in this example that removes all always ready instances from both the HTTP triggers group and also a function named

`hello_world`

:```
az functionapp scale config always-ready delete --resource-group <RESOURCE_GROUP> --name <APP_NAME> --setting-names http function:hello_world
```


## Set HTTP concurrency limits

Unless you set specific limits, HTTP concurrency defaults for Flex Consumption plan apps are determined based on your instance size setting. For more information, see [HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency).

Here's how you can set HTTP concurrency limits for an existing app:

Use the [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to set specific HTTP concurrency limits for your app, regardless of instance size.

```
az functionapp scale config set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --trigger-type http --trigger-settings perInstanceConcurrency=10
```


This example sets the HTTP trigger concurrency level to `10`

. After you specifically set an HTTP concurrency value, that value is maintained despite any changes in your app's instance size setting.

## Set site update strategy

The Flex Consumption plan uniquely supports two different site update strategies that control how your function app handles code deployments and configuration changes. By default, Flex Consumption plan apps use the `Recreate`

strategy, which terminates currently executing functions during deployments. To enable zero-downtime deployments, you can configure the `RollingUpdate`

strategy instead. For more information, see [Site update strategies in Flex Consumption](flex-consumption-site-updates).

Note

Site update strategy configuration is currently in public preview and is only available through Bicep or ARM templates. You can't configure this setting using the Azure CLI, Azure portal, or Visual Studio Code.

Site update strategy configuration isn't currently supported in the Azure CLI. Use Bicep or ARM templates as described in [Configure site update strategy](flex-consumption-site-updates#configure-your-update-strategy).

## View currently supported regions

To view the list of regions that currently support Flex Consumption plans:

If you haven't done so already, sign in to Azure:

`az login`

The

command signs you into your Azure account.`az login`

Use the

`az functionapp list-flexconsumption-locations`

command to review the list of regions that currently support Flex Consumption in alphabetical order.`az functionapp list-flexconsumption-locations --query "sort_by(@, &name)[].{Region:name}" -o table`


When you create an app in the [Azure portal](flex-consumption-how-to?tabs=azure-portal#create-a-flex-consumption-app) or by using [Visual Studio Code](flex-consumption-how-to?tabs=vs-code#create-a-flex-consumption-app), currently unsupported regions are filtered out of the region list.

## Monitor your app in Azure

Azure Monitor provides these distinct sets of metrics to help you better understand how your function app runs in Azure:

- Platform metrics: provides infrastructure-level insights
- Application Insights: provides code-level insights, including traces and errors logs.

If you [enable Application Insights in your app](configure-monitoring#enable-application-insights-integration), you're able to:

- Track detailed execution times and dependencies
- Monitor individual function performance
- Analyze failures and exceptions
- Correlate platform metrics with application behavior with custom queries

For more information, see [Monitor Azure Functions](monitor-functions).

### Supported metrics

Run this script to view all of the platform metrics that are currently available your app:

```
appId=$(az functionapp show --name <APP_NAME> --resource-group <RESOURCE_GROUP> --query id -o tsv)
az monitor metrics list-definitions --resource $appId --query "[].{Name:name.localizedValue,Value:name.value}" -o table
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group and function app names, respectively. This script gets the fully qualified app ID and returns the available platform metrics in a table.

### View metrics

You can review current metrics either in the Azure portal or by using the Azure CLI.

In the Azure portal, you can also create metrics alerts and pin charts and other reports to dashboards in the portal.

Use this script to generate a report of the current metrics for your app:

```
appId=$(az functionapp show --name <APP_NAME> --resource-group <RESOURCE_GROUP> --query id -o tsv)
appId=$(az functionapp show --name func-fuxigh6c255de --resource-group exampleRG --query id -o tsv)
echo -e "\nAlways-ready and on-emand execution counts..."
az monitor metrics list --resource $appId --metric "AlwaysReadyFunctionExecutionCount" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "OnDemandFunctionExecutionCount" --interval PT1H --output table
echo -e "\nExecution units (MB-ms) in always-ready and on-emand execution counts..."
az monitor metrics list --resource $appId --metric "AlwaysReadyFunctionExecutionUnits" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "OnDemandFunctionExecutionUnits" --interval PT1H --output table
echo -e "\nAlways-ready resource utilization..."
az monitor metrics list --resource $appId --metric "AlwaysReadyUnits" --interval PT1H --output table
echo -e "\nMemory utilization..."
az monitor metrics list --resource $appId --metric "AverageMemoryWorkingSet" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "MemoryWorkingSet" --interval PT1H --output table
echo -e "\nInstance count and CPU utilization..."
az monitor metrics list --resource $appId --metric "InstanceCount" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "CpuPercentage" --interval PT1H --output table
```


To learn more about metrics for Azure Functions, see [Monitor Azure Functions](monitor-functions).

### View logs

When your app is connected to Application Insights, you can better analyze your app performance and troubleshoot problems during execution.

- Use "Performance" to analyze response times and dependencies
- Use "Failures" to identify any errors occurring after migration
- Create custom queries in "Logs" to analyze function behavior. For example:

Use this query to compare success rates by instance:

```
requests
| where timestamp > ago(7d)
| summarize successCount=countif(success == true), failureCount=countif(success == false) by bin(timestamp, 1h), cloud_RoleName
| render timechart
```


Use this query to analyze the number of instances that were actively processing your function:

```
let _startTime = ago(20m); //Adjust start time as needed
let _endTime = now(); //Adjust end time as needed
let bins = 1s; //Adjust bin as needed - this will give per second results
requests
| where operation_Name == 'EventHubsTrigger' //Replace with the name of the function in the function app that you are analyzing
| where timestamp between(_startTime .. _endTime)
| make-series dcount(cloud_RoleInstance) default=0 on timestamp from _startTime to _endTime step bins
| render columnchart
```


### View costs

Because you can tune your app to adjust performance versus operating costs, it's important to track the costs associated with running your app in the Flex Consumption plan.

To view the current costs:

In your function app page in the

[Azure portal](https://portal.azure.com), select the resource group link.In the resource group page, select

**Cost Management**>**Cost analysis**.Review the current costs and cost trajectory of the app itself.

Optionally, select

**Cost Management**>**Alerts**and then**+ Add**to create a new alert for the app.

## Fine-tune your app

The Flex Consumption plan provides several settings that you can tune to refine the performance of your app. Actual performance and costs can vary based on your app-specific workload patterns and configuration. For example, higher [memory instance sizes](flex-consumption-plan#instance-sizes) can improve performance for memory-intensive operations but at a higher cost per active period.

Here are some adjustments you can make to fine-tune performance versus cost:

[Adjust concurrency settings](functions-concurrency)to maximize throughput per instance.[Choose the appropriate memory size](#configure-instance-memory)for your workload. Higher memory sizes cost more but can improve performance.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-blob-storage-events -->

# Quickstart: Respond to blob storage events by using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use Visual Studio Code to build an app that responds to events in a Blob Storage container. After testing the code locally by using an emulator, you deploy it to a new serverless function app running in a Flex Consumption plan in Azure Functions.

The project uses the Azure Developer CLI (`azd`

) extension with Visual Studio Code to simplify initializing and verifying your project code locally, as well as deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension requires[Azure Functions Core Tools](functions-run-local). When this tool isn't available locally, the extension tries to install it by using a package-based installer. You can also install or update the Core Tools package by running`Azure Functions: Install or Update Azure Functions Core Tools`

from the command palette. If you don't have npm or Homebrew installed on your local computer, you must instead[manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21 (Linux).[Apache Maven](https://maven.apache.org), version 3.0 or above.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

- The
[Azure Developer CLI extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.azure-dev)for Visual Studio Code.

[REST Client extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)or an equivalent REST tool you use to securely execute HTTP requests.

## Initialize the project

Use the `azd init`

command from the command palette to create a local Azure Functions code project from a template.

In Visual Studio Code, open a folder or workspace where you want to create your project.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Initialize App (init)`

, then choose**Select a template**.There might be a slight delay while

`azd`

initializes the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions C# Event Grid Blob Trigger using Azure Developer CLI`

.When prompted in the terminal, enter a unique environment name, such as

`blobevents-dotnet`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions Python Event Grid Blob Trigger using Azure Developer CLI`

.When prompted in the terminal, enter a unique environment name, such as

`blobevents-python`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions TypeScript Event Grid Blob Trigger using Azure Developer CLI`

.When prompted, enter a unique environment name, such as

`blobevents-typescript`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions Java Event Grid Blob Trigger using Azure Developer CLI`

.When prompted, enter a unique environment name, such as

`blobevents-java`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-java-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions PowerShell Event Grid Blob Trigger using Azure Developer CLI`

.When prompted, enter a unique environment name, such as

`blobevents-powershell`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-powershell-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

In `azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

## Add the local.settings.json file

Functions needs the local.settings.json file to configure the host when running locally.

Run this command to go to the

`src`

app folder:`cd src`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "java", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "powershell", "FUNCTIONS_WORKER_RUNTIME_VERSION": "7.2", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "python", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


## Create and activate a virtual environment

In the `src`

folder, run these commands to create and activate a virtual environment named `.venv`

:

```
python3 -m venv .venv
source .venv/bin/activate
```


If Python doesn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


## Set up local storage emulator

Use the Azurite emulator to run your code project locally before creating and using Azure resources.

If you haven't already,

[install Azurite](/en-us/azure/storage/common/storage-use-azurite#install-azurite).Press

`F1`. In the command palette, search for and run the command`Azurite: Start`

to start the local storage emulator.In the

**Azure**area, expand**Workspace**>**Attached Storage Accounts**>**Local Emulator**, right-click (Ctrl-click on Mac)**Blob Containers**, select**Create Blob Container...**, and create these two blob storage containers in the local emulator:`unprocessed-pdf`

: container that the trigger monitors for storage events.`processed-pdf`

: container where the function sends processed blobs as output.

Expand

**Blob Containers**, right-click (Ctrl-click on Mac)**unprocessed-pdf**, select**Upload Files...**, press`Enter`to accept the root directory, and upload the PDF files from the`data`

project folder.

When running locally, you can use REST to trigger the function by simulating the function receiving a message from an event subscription.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer by using the Azurite emulator. The `PDFProcessorSTORAGE`

environment variable defines the storage account connection, which is also set to `"UseDevelopmentStorage=true"`

in the local.settings.json file when running locally.

Run this command from the

`src`

project folder in a terminal or command prompt:`func start`

`mvn clean package mvn azure-functions:run`

`npm install func start`

`npm install npm start`

When the Functions host starts, it writes the name of the trigger and the trigger type to the terminal output. In Functions, the project root folder contains the host.json file.

With Core Tools still running in

**Terminal**, open the`test.http`

file in your project and select**Send Request**to trigger the`ProcessBlobUpload`

function by sending a test blob event to the blob event webhook.This step simulates receiving an event from an event subscription when running locally, and you should see the request and processed file information written in the logs. If you aren't using

*REST Client*, you must use another secure REST tool to call the endpoint with the payload in`test.http`

.In the Workspace area for the blob container, expand

**processed-pdf**and verify that the function processed the PDF file and copied it with a`processed-`

prefix.When you're done, press Ctrl+C in the terminal window to stop the

`func.exe`

host process.

## Review the code (optional)

You can review the code that defines the Event Grid blob trigger in the [ProcessBlobUpload.cs project file](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-eventgrid-blob/blob/main/src/ProcessBlobUpload.cs). The function demonstrates how to:

- Use
`BlobTrigger`

with`Source = BlobTriggerSource.EventGrid`

for near real-time processing - Bind to
`BlobClient`

for the source blob and`BlobContainerClient`

for the destination - Process blob content and copy it to another container by using streams

You can review the code that defines the Event Grid blob trigger in the [function_app.py project file](https://github.com/Azure-Samples/functions-quickstart-python-azd-eventgrid-blob/blob/main/src/function_app.py). The function demonstrates how to:

- Use
`@app.blob_trigger`

with`source="EventGrid"`

for near real-time processing - Access blob content using the
`InputStream`

parameter - Copy processed files to the destination container using the Azure Storage SDK

You can review the code that defines the Event Grid blob trigger in the [processBlobUpload.ts project file](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-eventgrid-blob/blob/main/src/functions/processBlobUpload.ts). The function demonstrates how to:

- Use
`app.storageBlob()`

with`source: 'EventGrid'`

for near real-time processing - Access blob content using the Node.js Azure Storage SDK
- Process and copy files to the destination container asynchronously

You can review the code that defines the Event Grid blob trigger in the [ProcessBlobUpload.java project file](https://github.com/Azure-Samples/functions-quickstart-java-azd-eventgrid-blob/blob/main/src/src/main/java/com/microsoft/azure/samples/ProcessBlobUpload.java). The function demonstrates how to:

- Use
`@BlobTrigger`

with`source = "EventGrid"`

for near real-time processing - Access blob content using
`BlobInputStream`

parameter - Copy processed files to the destination container using Azure Storage SDK for Java

You can review the code that defines the Event Grid blob trigger in the [ProcessBlobUpload/run.ps1 project file](https://github.com/Azure-Samples/functions-quickstart-powershell-azd-eventgrid-blob/blob/main/src/processBlobUpload/run.ps1) and the corresponding [function.json](https://github.com/Azure-Samples/functions-quickstart-powershell-azd-eventgrid-blob/blob/main/src/processBlobUpload/function.json). The function demonstrates how to:

- Configure blob trigger with
`"source": "EventGrid"`

in function.json for near real-time processing - Access blob content using PowerShell Azure Storage cmdlets
- Process and copy files to the destination container using Azure PowerShell modules

After you review and verify your function code locally, it's time to publish the project to Azure.

## Create Azure resources and deploy

Use the `azd up`

command to create the function app in a Flex Consumption plan along with other required Azure resources, including the event subscription. After the infrastructure is ready, `azd`

also deploys your project code to the new function app in Azure.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Developer CLI (azd): Sign In with Azure Developer CLI`

, then sign in by using your Azure account.In the project root, press

`F1`to open the command palette. Search for and run the command`Azure Developer CLI (azd): Provision and Deploy (up)`

to create the required Azure resources and deploy your code.When prompted in the Terminal window, provide these required deployment parameters:

Prompt Description Select an Azure Subscription to use Choose the subscription in which you want to create your resources. *Environment name*An environment that's used to maintain a unique deployment context for your app. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. The

`azd up`

command uses your responses to these prompts with the Bicep configuration files to create and configure these required Azure resources, following the latest best practices:- Flex Consumption plan and function app
- Azure Storage account with blob containers
- Application Insights (recommended)
- Access policies and roles for your account
- Event Grid subscription for blob events
- Service-to-service connections by using managed identities (instead of stored connection strings)

After the command completes successfully, your app runs in Azure with an event subscription configured to trigger your function when blobs are added to the

`unprocessed-pdf`

container.Make a note of the

`AZURE_STORAGE_ACCOUNT_NAME`

and`AZURE_FUNCTION_APP_NAME`

in the output. These names are unique for your storage account and function app in Azure, respectively.

## Verify the deployed function

In Visual Studio Code, press

`F1`. In the command palette, search for and run the command`Azure Storage: Upload Files...`

. Accept the root directory, and as before, upload one or more PDF files from the`data`

project folder.When prompted, select the name of your new storage account (from

`AZURE_STORAGE_ACCOUNT_NAME`

). Select**Blob Containers**>**unprocessed-pdf**.Press

`F1`. In the command palette, search for and run the command`Azure Storage: Open in Explorer`

. Select the same storage account >**Blob Containers**>**processed-pdf**, then**Open in new window**.In the Explorer, verify that the PDF files you uploaded were processed by your function. The output is written to the

`processed-pdf`

container with a`processed-`

prefix.

The Event Grid blob trigger processes files within seconds of upload. This speed demonstrates the near real-time capabilities of this approach compared to traditional polling-based blob triggers.

## Redeploy your code

Run the `azd up`

command as many times as you need to both provision your Azure resources and deploy code updates to your function app.

Note

Deployed code files are always overwritten by the latest deployment package.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that were used when creating Azure resources.

## Clean up resources

When you're done working with your function app and related resources, use this command to delete the function app and its related resources from Azure. This action helps you avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-embeddings-input -->

# Azure OpenAI embeddings input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI embeddings input binding allows you to generate embeddings for inputs. The binding can generate embeddings from files or raw text inputs.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about embeddings in Azure OpenAI Service, see [Understand embeddings in Azure OpenAI Service](/en-us/azure/ai-services/openai/concepts/understand-embeddings).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example shows how to generate embeddings for a raw text string.

```
internal class EmbeddingsRequest
{
[JsonPropertyName("rawText")]
public string? RawText { get; set; }
[JsonPropertyName("filePath")]
public string? FilePath { get; set; }
[JsonPropertyName("url")]
public string? Url { get; set; }
}
/// <summary>
/// Example showing how to use the <see cref="EmbeddingsAttribute"/> input binding to generate embeddings
/// for a raw text string.
/// </summary>
[Function(nameof(GenerateEmbeddings_Http_RequestAsync))]
public async Task GenerateEmbeddings_Http_RequestAsync(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = "embeddings")] HttpRequestData req,
[EmbeddingsInput("{rawText}", InputType.RawText, EmbeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%")] EmbeddingsContext embeddings)
{
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
EmbeddingsRequest? requestBody = JsonSerializer.Deserialize<EmbeddingsRequest>(request);
this.logger.LogInformation(
"Received {count} embedding(s) for input text containing {length} characters.",
embeddings.Count,
requestBody?.RawText?.Length);
// TODO: Store the embeddings into a database or other storage.
}
```


This example shows how to retrieve embeddings stored at a specified file that is accessible to the function.

```
[Function(nameof(GetEmbeddings_Http_FilePath))]
public async Task GetEmbeddings_Http_FilePath(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = "embeddings-from-file")] HttpRequestData req,
[EmbeddingsInput("{filePath}", InputType.FilePath, MaxChunkLength = 512, EmbeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%")] EmbeddingsContext embeddings)
{
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
EmbeddingsRequest? requestBody = JsonSerializer.Deserialize<EmbeddingsRequest>(request);
this.logger.LogInformation(
"Received {count} embedding(s) for input file '{path}'.",
embeddings.Count,
requestBody?.FilePath);
// TODO: Store the embeddings into a database or other storage.
}
```


This example shows how to generate embeddings for a raw text string.

```
@FunctionName("GenerateEmbeddingsHttpRequest")
public HttpResponseMessage generateEmbeddingsHttpRequest(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "embeddings")
HttpRequestMessage<EmbeddingsRequest> request,
@EmbeddingsInput(name = "Embeddings", input = "{RawText}", inputType = InputType.RawText, embeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%") String embeddingsContext,
final ExecutionContext context) {
if (request.getBody() == null)
{
throw new IllegalArgumentException(
"Invalid request body. Make sure that you pass in {\"rawText\": value } as the request body.");
}
JSONObject embeddingsContextJsonObject = new JSONObject(embeddingsContext);
context.getLogger().info(String.format("Received %d embedding(s) for input text containing %s characters.",
embeddingsContextJsonObject.get("count"),
request.getBody().getRawText().length()));
// TODO: Store the embeddings into a database or other storage.
return request.createResponseBuilder(HttpStatus.ACCEPTED)
.header("Content-Type", "application/json")
.build();
}
```


This example shows how to retrieve embeddings stored at a specified file that is accessible to the function.

```
@FunctionName("GenerateEmbeddingsHttpFilePath")
public HttpResponseMessage generateEmbeddingsHttpFilePath(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "embeddings-from-file")
HttpRequestMessage<EmbeddingsRequest> request,
@EmbeddingsInput(name = "Embeddings", input = "{FilePath}", inputType = InputType.FilePath, maxChunkLength = 512, embeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%") String embeddingsContext,
final ExecutionContext context) {
if (request.getBody() == null)
{
throw new IllegalArgumentException(
"Invalid request body. Make sure that you pass in {\"filePath\": value } as the request body.");
}
JSONObject embeddingsContextJsonObject = new JSONObject(embeddingsContext);
context.getLogger().info(String.format("Received %d embedding(s) for input file %s.",
embeddingsContextJsonObject.get("count"),
request.getBody().getFilePath()));
// TODO: Store the embeddings into a database or other storage.
return request.createResponseBuilder(HttpStatus.ACCEPTED)
.header("Content-Type", "application/json")
.build();
}
```


This example shows how to generate embeddings for a raw text string.

```
const embeddingsHttpInput = input.generic({
input: '{rawText}',
inputType: 'RawText',
type: 'embeddings',
embeddingsModel: '%EMBEDDING_MODEL_DEPLOYMENT_NAME%'
})
app.http('generateEmbeddings', {
methods: ['POST'],
route: 'embeddings',
authLevel: 'function',
extraInputs: [embeddingsHttpInput],
handler: async (request, context) => {
let requestBody = await request.json();
let response = context.extraInputs.get(embeddingsHttpInput);
context.log(
`Received ${response.count} embedding(s) for input text containing ${requestBody.RawText.length} characters.`
);
// TODO: Store the embeddings into a database or other storage.
return {status: 202}
}
});
```


```
interface EmbeddingsHttpRequest {
RawText?: string;
}
const embeddingsHttpInput = input.generic({
input: '{rawText}',
inputType: 'RawText',
type: 'embeddings',
embeddingsModel: '%EMBEDDING_MODEL_DEPLOYMENT_NAME%'
})
app.http('generateEmbeddings', {
methods: ['POST'],
route: 'embeddings',
authLevel: 'function',
extraInputs: [embeddingsHttpInput],
handler: async (request, context) => {
let requestBody: EmbeddingsHttpRequest = await request.json();
let response: any = context.extraInputs.get(embeddingsHttpInput);
context.log(
`Received ${response.count} embedding(s) for input text containing ${requestBody.RawText.length} characters.`
);
// TODO: Store the embeddings into a database or other storage.
return {status: 202}
}
});
```


This example shows how to generate embeddings for a raw text string.

```
const embeddingsFilePathInput = input.generic({
input: '{filePath}',
inputType: 'FilePath',
type: 'embeddings',
maxChunkLength: 512,
embeddingsModel: '%EMBEDDING_MODEL_DEPLOYMENT_NAME%'
})
app.http('getEmbeddingsFilePath', {
methods: ['POST'],
route: 'embeddings-from-file',
authLevel: 'function',
extraInputs: [embeddingsFilePathInput],
handler: async (request, context) => {
let requestBody = await request.json();
let response = context.extraInputs.get(embeddingsFilePathInput);
context.log(
`Received ${response.count} embedding(s) for input file ${requestBody.FilePath}.`
);
// TODO: Store the embeddings into a database or other storage.
return {status: 202}
}
});
```


```
interface EmbeddingsFilePath {
FilePath?: string;
}
const embeddingsFilePathInput = input.generic({
input: '{filePath}',
inputType: 'FilePath',
type: 'embeddings',
maxChunkLength: 512,
embeddingsModel: '%EMBEDDING_MODEL_DEPLOYMENT_NAME%'
})
app.http('getEmbeddingsFilePath', {
methods: ['POST'],
route: 'embeddings-from-file',
authLevel: 'function',
extraInputs: [embeddingsFilePathInput],
handler: async (request, context) => {
let requestBody: EmbeddingsFilePath = await request.json();
let response: any = context.extraInputs.get(embeddingsFilePathInput);
context.log(
`Received ${response.count} embedding(s) for input file ${requestBody.FilePath}.`
);
// TODO: Store the embeddings into a database or other storage.
return {status: 202}
}
});
```


This example shows how to generate embeddings for a raw text string.

Here's the *function.json* file for generating the embeddings:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"route": "embeddings",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"name": "Embeddings",
"type": "embeddings",
"direction": "in",
"inputType": "RawText",
"input": "{rawText}",
"embeddingsModel": "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata, $Embeddings)
$input = $Request.Body.RawText
Write-Host "Received $($Embeddings.Count) embedding(s) for input text containing $($input.Length) characters."
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::Accepted
})
```


This example shows how to generate embeddings for a raw text string.

```
@app.function_name("GenerateEmbeddingsHttpRequest")
@app.route(route="embeddings", methods=["POST"])
@app.embeddings_input(
arg_name="embeddings",
input="{rawText}",
input_type="rawText",
embeddings_model="%EMBEDDING_MODEL_DEPLOYMENT_NAME%",
)
def generate_embeddings_http_request(
req: func.HttpRequest, embeddings: str
) -> func.HttpResponse:
user_message = req.get_json()
embeddings_json = json.loads(embeddings)
embeddings_request = {"raw_text": user_message.get("rawText")}
logging.info(
f'Received {embeddings_json.get("count")} embedding(s) for input text '
f'containing {len(embeddings_request.get("raw_text"))} characters.'
)
# TODO: Store the embeddings into a database or other storage.
return func.HttpResponse(status_code=200)
```


## Attributes

Apply the `EmbeddingsInput`

attribute to define an embeddings input binding, which supports these parameters:

| Parameter | Description |
|---|---|
Input |
The input string for which to generate embeddings. |
AIConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
EmbeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
MaxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
MaxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
InputType |
Optional. Gets the type of the input. |

## Annotations

The `EmbeddingsInput`

annotation enables you to define an embeddings input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
input |
The input string for which to generate embeddings. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
maxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
inputType |
Optional. Gets the type of the input. |

## Decorators

During the preview, define the input binding as a `generic_input_binding`

binding of type `embeddings`

, which supports these parameters: `embeddings`

decorator supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
input |
The input string for which to generate embeddings. |
ai_connection_name |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddings_model |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
max_overlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
input_type |
Gets the type of the input. |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `EmbeddingsInput` . |
direction |
Must be `in` . |
name |
The name of the input binding. |
input |
The input string for which to generate embeddings. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
maxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
inputType |
Optional. Gets the type of the input. |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
input |
The input string for which to generate embeddings. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
maxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
inputType |
Optional. Gets the type of the input. |

See the [Example section](#example) for complete examples.

## Usage

Changing the default embeddings `model`

changes the way that embeddings are stored in the vector database. Changing the default model can cause the lookups to start misbehaving when they don't match the rest of the data that was previously ingested into the vector database. The default model for embeddings is `text-embedding-ada-002`

.

When calculating the maximum character length for input chunks, consider that the maximum input tokens allowed for second-generation input embedding models like `text-embedding-ada-002`

is `8191`

. A single token is approximately four characters in length (in English), which translates to roughly 32,000 (English) characters of input that can fit into a single chunk.
