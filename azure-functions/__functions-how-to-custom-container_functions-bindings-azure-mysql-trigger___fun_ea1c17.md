---
merged_at: 2026-01-26T23:29:57.713238
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-custom-container -->

# Work with containers and Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates the support that Azure Functions provides for containerized function apps that run in an Azure Container Apps environment. For more information, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

Important

A new hosting method for running Azure Functions directly in Azure Container Apps is now available. See [Native Azure Functions Support in Azure Container Apps](https://techcommunity.microsoft.com/blog/appsonazureblog/announcing-native-azure-functions-support-in-azure-container-apps/4414039). This integration allows you to use the full features and capabilities of Azure Container Apps. You also benefit from the functions programming model and simplicity of autoscaling provided by Azure Functions.

We recommend this approach for most new workloads. For more information, see [Azure Functions on Azure Container Apps](../container-apps/functions-overview).

This article demonstrates the support that Azure Functions provides for function apps that run in Linux containers.

Choose the hosting environment for your containerized function app at the top of this article.

If you want to jump right in, the following article shows you how to create your first function in a Linux container and deploy the image from a container registry to a supported Azure hosting service:


[Create your first containerized Azure Functions on Azure Container Apps]

To learn more about deployments to Azure Container Apps, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

Important

This article currently shows how to connect to the default storage account by using a connection string. For the best security, instead create a managed identity-based connection to Azure Storage using Microsoft Entra authentication. For more information, see [Connections](functions-reference#connections).

## Create containerized function apps

Functions makes it easy to deploy and run your function apps as Linux containers, which you create and maintain. Functions maintains a set of [language-specific base images](https://mcr.microsoft.com/catalog?search=functions) that you can use when creating containerized function apps.

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

For a complete example of how to create the local containerized function app from the command line and publish the image to a container registry, see [Create a function app in a local Linux container](functions-create-container-registry).

## Generate the Dockerfile

Functions tooling provides a Docker option that generates a Dockerfile with your functions code project. You can use this file with Docker to create your functions in a container that derives from the correct base image, which includes language and version.

The way you create a Dockerfile depends on how you create your project.

When you create a Functions project using

[Azure Functions Core Tools](functions-run-local), include the`--docker`

option when you run thecommand, as in the following example:`func init`

`func init --docker`

You can also add a Dockerfile to an existing project by using the

`--docker-only`

option when you run thecommand in an existing project folder, as in the following example:`func init`

`func init --docker-only`


For a complete example, see [Create a function app in a local Linux container](functions-create-container-registry#create-and-test-the-local-functions-project).

## Create your function app in a container

With a Functions-generated Dockerfile in your code project, you can use Docker to create the containerized function app on your local computer. The following `docker build`

command creates an image of your containerized functions from the project in the local directory:

```
docker build --tag <DOCKER_ID>/<IMAGE_NAME>:v1.0.0 .
```


For an example of how to create the container, see [Build the container image and verify locally](functions-create-container-registry#build-the-container-image-and-verify-locally).

## Update an image in the registry

When you make changes to your functions code project or need to update to the latest base image, rebuild the container locally. Republish the updated image to your chosen container registry. The following command rebuilds the image from the root folder with an updated version number and pushes it to your registry:

```
az acr build --registry <REGISTRY_NAME> --image <LOGIN_SERVER>/azurefunctionsimage:v1.0.1 .
```


Replace `<REGISTRY_NAME>`

with your Container Registry instance and `<LOGIN_SERVER>`

with the sign-in server name.

Update an existing deployment to use the new image. You can update the function app to use the new image either by using the Azure CLI or in the [Azure portal](https://portal.azure.com):

```
az functionapp config container set --image <IMAGE_NAME> --registry-password <SECURE_PASSWORD>--registry-username <USER_NAME> --name <APP_NAME> --resource-group <RESOURCE_GROUP>
```


In this example, `<IMAGE_NAME>`

is the full name of the new image with version. Private registries require you to supply a username and password. Store these credentials securely.

You should also consider [enabling continuous deployment](#enable-continuous-deployment-to-azure).

## Create a containerized function app using the Azure portal

When you create a function app in the [Azure portal](https://portal.azure.com), you can choose to deploy the function app from an image in a container registry. To learn how to create a containerized function app in a container registry, see [Create your function app in a container](#create-your-function-app-in-a-container).

The following steps create and deploy an existing containerized function app from a container registry.

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Compute**>**Function App**.Under

**Select a hosting option**, choose**Functions Premium**>**Select**.This action creates a function app hosted by Azure Functions in the

[Premium plan](functions-premium-plan), which supports dynamic scaling. You can also choose to run in an**App Service plan**, but in this kind of dedicated plan you must manage the[scaling of your function app](functions-scale).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription in which you create your function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. You should create a resource group because there are [known limitations when creating new function apps in an existing resource group](functions-scale#limitations-for-creating-new-function-apps-in-an-existing-resource-group).**Function App name**An app name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Secure unique default hostname**Enabled Enable this feature so you don't have to worry about domain name collisions, regardless of your app name. **Do you want to deploy code or container image?**Container image Deploy a containerized function app from a registry. To create a function app in registry, see [Create a function app in a local Linux container](functions-create-container-registry).**Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access.**Linux plan**New plan (default) Creates a new Premium plan to host your app. You can also choose an existing premium plan. **Pricing plan**Elastic Premium EP1 `EP1`

is the most affordable plan. You can choose a larger plan if you need to.**Zone Redundancy**Disabled You don't need this feature in a nonproduction app. Accept the default options of creating a new storage account on the

**Storage**tab and a new Application Insight instance on the**Monitoring**tab. You can also choose to use an existing storage account or Application Insights instance.Select

**Review + create**to review the app configuration selections.On the

**Review + create**page, review your settings, and then select**Create**to provision the function app using a default base image.After your function app resource is created, select

**Go to resource**. In the function app page, select**Deployment Center**.In the

**Deployment Center**, you can connect your container registry as the source of the image. You can also enable GitHub Actions or Azure Pipelines for more robust continuous deployment of updates to your container in the registry.

## Create a containerized function app using the Azure portal

When you create a Container Apps-hosted function app in the [Azure portal](https://portal.azure.com), you can choose to deploy your function app from an image in a container registry. To learn how to create a containerized function app in a container registry, see [Create your function app in a container](#create-your-function-app-in-a-container).

The following steps create and deploy an existing containerized function app from a container registry.

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Compute**>**Function App**.Under

**Select a hosting option**, choose**Container Apps environment**>**Select**.On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription in which you create your function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. You should create a resource group because there are [known limitations when creating new function apps in an existing resource group](functions-scale#limitations-for-creating-new-function-apps-in-an-existing-resource-group).**Function App name**Unique name *Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access.*App name must be unique within the Azure Container Apps environment.Still on the

**Basics**page, accept the suggested new environment for**Azure Container Apps environment**. To minimize costs, the new default environment is created in the**Consumption + Dedicated**with the default workload profile and without zone redundancy. For more information, see[Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).You can also choose to use an existing Container Apps environment. To create a custom environment, instead select

**Create new**. In the**Create Container Apps Environment**page, you can add nondefault workload profiles or enable zone redundancy. To learn about environments, see[Azure Container Apps environments](../container-apps/environment).Select the

**Deployment**tab and unselect**Use quickstart image**. Otherwise, the function app is deployed from the base image for your function app language.Choose your

**Image type**, public or private. Choose**Private**if you're using Azure Container Registry or some other private registry. Supply the**Image**name, including the registry prefix. If you're using a private registry, provide the image registry authentication credentials. The**Public**setting only supports images stored publicly in Docker Hub.Under

**Container resource allocation**, select your desired number of CPU cores and available memory. If your environment has other workload profiles added, you can select a nondefault**Workload profile**. Choices  affect the cost of hosting your app. See the[Container Apps pricing page](https://azure.microsoft.com/pricing/details/container-apps/)to estimate your potential costs.Select

**Review + create**to review the app configuration selections.On the

**Review + create**page, review your settings, and then select**Create**to provision the function app and deploy your container image from the registry.

## Work with images in Azure Functions

When your function app container is deployed from a registry, Functions maintains information about the source image.

Use the following commands to get data about the image or change the deployment image used:

: returns information about the image used for deployment.`az functionapp config container show`

: change registry settings or update the image used for deployment, as shown in the previous example.`az functionapp config container set`


## Use Container Apps workload profiles

Workload profiles are feature of Container Apps that let you better control your deployment resources. Azure Functions on Azure Container Apps also supports workload profiles. For more information, see [Workload profiles in Azure Container Apps](../container-apps/workload-profiles-overview).

You can also set the amount of CPU and memory resources allocated to your app.

You can create and manage both workload profiles and resource allocations using the Azure CLI or in the Azure portal.

You enable workload profiles when you create your container app environment. For an example, see [Create a container app in a profile](../container-apps/workload-profiles-manage-cli#create-a-container-app-in-a-profile).

You can add, edit, and delete profiles in your environment. For an example, see [Add profiles](../container-apps/workload-profiles-manage-cli#add-profiles).

When you create a containerized function app in an environment that has workload profiles enabled, you should also specify the profile in which to run. Specify the profile by using the `--workload-profile-name`

parameter of the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command, like in this example:

```
az functionapp create --name <APP_NAME> --storage-account <STORAGE_NAME> --environment MyContainerappEnvironment --resource-group AzureFunctionsContainers-rg --functions-version 4 --runtime <LANGUAGE_STACK> --image <IMAGE_URI> --workload-profile-name <PROFILE_NAME> --cpu <CPU_COUNT> --memory <MEMORY_SIZE>
```


In the [az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command, the `--environment`

parameter specifies the Container Apps environment and the `--image`

parameter specifies the image to use for the function app. In this example, replace `<STORAGE_NAME>`

with the name you used in the previous section for the storage account. Also, replace `<APP_NAME>`

with a name appropriate to you that is unique in the environment.

To set the resources allocated to your app, replace `<CPU_COUNT>`

with your desired number of virtual CPUs, with a minimum of 0.5 up to the maximum allowed by the profile. For `<MEMORY_SIZE>`

, choose a dedicated memory amount from 1 GB up to the maximum allowed by the profile.

You can use the [az functionapp container set](/en-us/cli/azure/functionapp/config/container#az-functionapp-config-container-set) command to manage the allocated resources and the workload profile used by your app.

```
az functionapp container set --name <APP_NAME> --resource-group AzureFunctionsContainers-rg --workload-profile-name <PROFILE_NAME> --cpu <CPU_COUNT> --memory <MEMORY_SIZE>
```


## Use application settings

Azure Functions lets you work with application settings for containerized function apps in the standard way. For more information, see [Use application settings](functions-how-to-use-azure-function-app-settings#settings).

Tip

By default, a containerized function app monitors port 80 for incoming requests. If your app must use a different port, use the [ WEBSITES_PORT application setting](../app-service/reference-app-settings#custom-containers) to change this port.

## Enable continuous deployment to Azure

When you host your containerized function app on Azure Container Apps, there are two ways to set up continuous deployment from a source code repository:

You aren't currently able to continuously deploy containers based on image changes in a container registry. You must instead use these source-code based continuous deployment pipelines.

## Enable continuous deployment to Azure

Important

Webhook-based deployment isn't currently supported when running your container in an [Elastic Premium plan](functions-premium-plan). If you need to use the continuous deployment method described in this section, instead deploy your container in an [App Service plan](dedicated-plan). When running in an Elastic Premium plan, you need to manually restart your app whenever you make updates to your container in the repository.

You can also configure continuous deployment from a source code repository using either [Azure Pipelines](functions-how-to-azure-devops#deploy-a-container) or [GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/blob/main/samples/GitHubActions/Func_on_ACA_GitHubAction_deployment.yml).

You can enable Azure Functions to automatically update your deployment of an image whenever you update the image in the registry.

Use the following command to enable continuous deployment and to get the webhook URL:

`az functionapp deployment container config --enable-cd --query CI_CD_URL --output tsv --name <APP_NAME> --resource-group AzureFunctionsContainers-rg`

The

[az functionapp deployment container config](/en-us/cli/azure/functionapp/deployment/container#az-functionapp-deployment-container-config)command enables continuous deployment and returns the deployment webhook URL. You can retrieve this URL at any time by using the[az functionapp deployment container show-cd-url](/en-us/cli/azure/functionapp/deployment/container#az-functionapp-deployment-container-show-cd-url)command.As before, replace

`<APP_NAME>`

with your function app name.Copy the deployment webhook URL to the clipboard.

Open

[Docker Hub](https://hub.docker.com/), sign in, and select**Repositories**on the navigation bar. Locate and select the image, select the**Webhooks**tab, specify a**Webhook name**, paste your URL in**Webhook URL**, and then select**Create**.With the webhook set, Azure Functions redeploys your image whenever you update it in Docker Hub.


## Enable SSH connections

SSH enables secure communication between a container and a client. With SSH enabled, you can connect to your container using App Service Advanced Tools (Kudu). For easy connection to your container using SSH, Azure Functions provides a base image that has SSH already enabled. You only need to edit your *Dockerfile*, then rebuild, and redeploy the image. You can then connect to the container through the Advanced Tools (Kudu).

In your

*Dockerfile*, append the string`-appservice`

to the base image in your`FROM`

instruction, as in the following example:`FROM mcr.microsoft.com/azure-functions/node:4-node18-appservice`

This example uses the SSH-enabled version of the Node.js version 18 base image. Visit the

[Azure Functions base image repos](https://mcr.microsoft.com/en-us/catalog?search=functions)to verify that you're using the latest version of the SSH-enabled base image.Rebuild the image by using the

`docker build`

command, replace the`<DOCKER_ID>`

with your Docker Hub account ID, as in the following example.`docker build --tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 .`

Push the updated image to Docker Hub, which should take considerably less time than the first push. Only the updated segments of the image need to be uploaded now.

`docker push <DOCKER_ID>/azurefunctionsimage:v1.0.0`

Azure Functions automatically redeploys the image to your functions app. The process takes place in less than a minute.

In the

[Azure portal](https://portal.azure.com), locate your function app. In the left menu, select**Development Tools**>**SSH**. Select**Go**. Connecting might take a few moments if Azure is still updating the container image.After a connection is established with your container, run the

`top`

command to view the currently running processes.

## Related content

The following articles provide more information about deploying and managing containers:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-trigger -->

# Azure Database for MySQL trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Database for MySQL trigger bindings monitor the user table for changes (inserts and updates) and invoke the function with updated row data.

Azure Database for MySQL trigger bindings use `az_func_updated_at`

and column data to monitor the user table for changes. As such, you need to alter the table structure to allow change tracking on the MySQL table before you use the trigger support. You can enable the change tracking on a table through the following query. For example, enable it on the `Products`

table:

```
ALTER TABLE Products
ADD az_func_updated_at TIMESTAMP DEFAULT
CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP;
```


The table for leases contains all columns that correspond to the primary key from the user table and three more columns: `az_func_AttemptCount`

, `az_func_LeaseExpirationTime`

, and `az_func_SyncCompletedTime`

. If any of the primary key columns have the same name, the result is an error message that lists conflicts. In this case, the listed primary key columns must be renamed for the trigger to work.

## Functionality overview

When the trigger function starts, it initiates two separate loops: the change polling loop and the lease renewal loop. These loops run continuously until the function is stopped.

The Azure Database for MySQL trigger binding uses the polling loop to check for changes. The polling loop triggers the user function when it detects changes. At a high level, the loop looks like this example:

```
while (true) {
1. Get list of changes on table - up to a maximum number controlled by the MySql_Trigger_MaxBatchSize setting
2. Trigger function with list of changes
3. Wait for delay controlled by MySql_Trigger_PollingIntervalMs setting
}
```


Changes are processed in the order that they're made. The oldest changes are processed first. Consider these points about change processing:

- If changes occur in multiple rows at once, the exact order in which they're sent to the function is based on the ascending order of the
`az_func_updated_at`

column and primary key columns. - Changes are batched for a row. If multiple changes occur in a row between each iteration of the loop, only the latest change entry that exists for that row is considered.

Note

Currently, managed identities aren't supported for connections between Azure Functions and Azure Database for MySQL.

## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

The example refers to a `Product`

class and a corresponding database table:

```
namespace AzureMySqlSamples.Common
{
public class Product
{
public int? ProductId { get; set; }
public string Name { get; set; }
public int Cost { get; set; }
public override bool Equals(object obj)
{
if (obj is Product)
{
var that = obj as Product;
return this.ProductId == that.ProductId && this.Name == that.Name && this.Cost == that.Cost;
}
return false;
}
}
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


You enable change tracking on the database by adding one column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The Azure Database for MySQL trigger binds to `IReadOnlyList<MySqlChange<T>>`

, which lists `MySqlChange`

objects. Each object has two properties:

`Item`

: The item that was changed. The type of the item should follow the table schema, as seen in the`ToDoItem`

class.`Operation`

: A value from the`MySqlChangeOperation`

enumeration. The possible value is`Update`

for both inserts and updates.

The following example shows a [C# function](functions-dotnet-class-library) that's invoked when changes occur in the `Product`

table:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Extensions.Logging;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.TriggerBindingSamples
{
private static readonly Action<ILogger, string, Exception> _loggerMessage = LoggerMessage.Define<string>(LogLevel.Information, eventId: new EventId(0, "INFO"), formatString: "{Message}");
[Function(nameof(ProductsTrigger))]
public static void Run(
[MySqlTrigger("Products", "MySqlConnectionString")]
IReadOnlyList<MySqlChange<Product>> changes, FunctionContext context)
{
ILogger logger = context.GetLogger("ProductsTrigger");
// The output is used to inspect the trigger binding parameter in test methods.
foreach (MySqlChange<Product> change in changes)
{
Product product = change.Item;
_loggerMessage(logger, $"Change operation: {change.Operation}", null);
_loggerMessage(logger, $"Product Id: {product.ProductId}, Name: {product.Name}, Cost: {product.Cost}", null);
}
}
}
```


## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-java).

The example refers to a `Product`

class, a `MySqlChangeProduct`

class, a `MySqlChangeOperation`

enumeration, and a corresponding database table.

In a separate file named Product.java:

```
package com.function.Common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class Product {
@JsonProperty("ProductId")
private int ProductId;
@JsonProperty("Name")
private String Name;
@JsonProperty("Cost")
private int Cost;
public Product() {
}
public Product(int productId, String name, int cost) {
ProductId = productId;
Name = name;
Cost = cost;
}
}
```


In a separate file named MySqlChangeProduct.java:

```
package com.function.Common;
public class MySqlChangeProduct {
private MySqlChangeOperation Operation;
private Product Item;
public MySqlChangeProduct() {
}
public MySqlChangeProduct(MySqlChangeOperation operation, Product item) {
this.Operation = operation;
this.Item = item;
}
}
```


In a separate file named MySqlChangeOperation.java:

```
package com.function.Common;
import com.google.gson.annotations.SerializedName;
public enum MySqlChangeOperation {
@SerializedName("0")
Update
}
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


You enable change tracking on the database by adding the following column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The Azure Database for MySQL trigger binds to `MySqlChangeProduct[]`

, which is an array of `MySqlChangeProduct`

objects. Each object has two properties:

`item`

: The item that was changed. The type of the item should follow the table schema, as seen in the`Product`

class.`operation`

: A value from the`MySqlChangeOperation`

enumeration. The possible value is`Update`

for both inserts and updates.

The following example shows a Java function that's invoked when changes occur in the `Product`

table:

```
/**
* Copyright (c) Microsoft Corporation. All rights reserved.
* Licensed under the MIT License. See License.txt in the project root for
* license information.
*/
package com.function;
import com.microsoft.azure.functions.ExecutionContext;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.mysql.annotation.MySqlTrigger;
import com.function.Common.MySqlChangeProduct;
import com.google.gson.Gson;
import java.util.logging.Level;
public class ProductsTrigger {
@FunctionName("ProductsTrigger")
public void run(
@MySqlTrigger(
name = "changes",
tableName = "Products",
connectionStringSetting = "MySqlConnectionString")
MySqlChangeProduct[] changes,
ExecutionContext context) {
context.getLogger().log(Level.INFO, "MySql Changes: " + new Gson().toJson(changes));
}
}
```


## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-powershell).

The example refers to a `Product`

database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


You enable change tracking on the database by adding one column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The Azure Database for MySQL trigger binds to `Product`

, which lists objects. Each object has two properties:

`item`

: The item that was changed. The structure of the item follows the table schema.`operation`

: The possible value is`Update`

for both inserts and updates.

The following example shows a PowerShell function that's invoked when changes occur in the `Product`

table.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"name": "changes",
"type": "mysqlTrigger",
"direction": "in",
"tableName": "Products",
"connectionStringSetting": "MySqlConnectionString"
}
],
"disabled": false
}
```


The [Configuration](#configuration) section explains these properties.

The following example is sample PowerShell code for the function in the run.ps1 file:

```
using namespace System.Net
param($changes)
# The output is used to inspect the trigger binding parameter in test methods.
# Use -Compress to remove new lines and spaces for testing purposes.
$changesJson = $changes | ConvertTo-Json -Compress
Write-Host "MySql Changes: $changesJson"
```


## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-js).

The example refers to a `Product`

database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


You enable change tracking on the database by adding one column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The Azure Database for MySQL trigger binds to `Changes`

, which is an array of objects. Each object has two properties:

`item`

: The item that was changed. The structure of the item follows the table schema.`operation`

: The possible value is`Update`

for both inserts and updates.

The following example shows a JavaScript function that's invoked when changes occur in the `Product`

table.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"name": "changes",
"type": "mysqlTrigger",
"direction": "in",
"tableName": "Products",
"connectionStringSetting": "MySqlConnectionString",
}
],
"disabled": false
}
```


The [Configuration](#configuration) section explains these properties.

The following example is sample JavaScript code for the function in the `index.js`

file:

```
module.exports = async function (context, changes) {
context.log(`MySql Changes: ${JSON.stringify(changes)}`)
}
```


## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-python).

The example refers to a `Product`

database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


You enable change tracking on the database by adding one column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


Note

You must use Azure Functions version 1.22.0b4 for Python.

The Azure Database for MySQL trigger binds to a variable named `Product`

, which lists objects. Each object has two properties:

`item`

: The item that was changed. The structure of the item follows the table schema.`operation`

: The possible value is`Update`

for both inserts and updates.

The following example shows a Python function that's invoked when changes occur in the `Product`

table.

The following example is sample Python code for the function_app.py file:

```
import json
import logging
import azure.functions as func
app = func.FunctionApp()
# The function is triggered when a change (insert, update)
# is made to the Products table.
@app.function_name(name="ProductsTrigger")
@app.mysql_trigger(arg_name="products",
table_name="Products",
connection_string_setting="MySqlConnectionString")
def products_trigger(products: str) -> None:
logging.info("MySQL Changes: %s", json.loads(products))
```


## Attributes

| Attribute property | Description |
|---|---|
`TableName` |
Required. The name of the table that the trigger monitors. |
`ConnectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database that contains the table monitored for changes. The name of the connection string setting corresponds to the application setting (in local.settings.json for local development) that contains the
|

`LeasesTableName`

`Leases_{FunctionId}_{TableId}`

.## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@MySQLTrigger`

annotation on parameters whose values would come from Azure Database for MySQL. This annotation supports the following elements:

| Element | Description |
|---|---|
`name` |
Required. The name of the parameter that the trigger binds to. |
`tableName` |
Required. The name of the table that the trigger monitors. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database that contains the table monitored for changes. The name of the connection string setting corresponds to the application setting (in local.settings.json for local development) that contains the
|

`LeasesTableName`

`Leases_{FunctionId}_{TableId}`

.## Configuration

The following table explains the binding configuration properties that you set in the function.json file:

| Property | Description |
|---|---|
`name` |
Required. The name of the parameter that the trigger binds to. |
`type` |
Required. Must be set to `MysqlTrigger` . |
`direction` |
Required. Must be set to `in` . |
`tableName` |
Required. The name of the table that the trigger monitors. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database that contains the table monitored for changes. The name of the connection string setting corresponds to the application setting (in local.settings.json for local development) that contains the
|

`LeasesTableName`

`Leases_{FunctionId}_{TableId}`

.## Optional configuration

You can configure the following optional settings for the Azure Database for MySQL trigger for local development or for cloud deployments.

### host.json

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

| Setting | Default | Description |
|---|---|---|
`MaxBatchSize` |
`100` |
The maximum number of changes processed with each iteration of the trigger loop before they're sent to the triggered function. |
`PollingIntervalMs` |
`1000` |
The delay in milliseconds between processing each batch of changes. (1,000 ms is 1 second.) |
`MaxChangesPerWorker` |
`1000` |
The upper limit on the number of pending changes in the user table that are allowed per application worker. If the count of changes exceeds this limit, it might result in a scale-out. The setting applies only for Azure function apps with
|

#### Example host.json file

Here's an example host.json file with the optional settings:

```
{
"version": "2.0",
"extensions": {
"MySql": {
"MaxBatchSize": 300,
"PollingIntervalMs": 1000,
"MaxChangesPerWorker": 100
}
},
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
},
"logLevel": {
"default": "Trace"
}
}
}
```


### local.setting.json

The local.settings.json file stores app settings and settings that local development tools use. Settings in the local.settings.json file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.

Important

Because the local.settings.json file might contain secrets, such as connection strings, you should never store it in a remote repository. Tools that support Azure Functions provide ways to synchronize settings in the local.settings.json file with the [app settings](functions-how-to-use-azure-function-app-settings#settings) in the function app to which your project is deployed.

| Setting | Default | Description |
|---|---|---|
`MySql_Trigger_BatchSize` |
`100` |
The maximum number of changes processed with each iteration of the trigger loop before they're sent to the triggered function. |
`MySql_Trigger_PollingIntervalMs` |
`1000` |
The delay in milliseconds between processing each batch of changes. (1,000 ms is 1 second.) |
`MySql_Trigger_MaxChangesPerWorker` |
`1000` |
The upper limit on the number of pending changes in the user table that are allowed per application worker. If the count of changes exceeds this limit, it might result in a scale-out. The setting applies only for Azure function apps with
|

#### Example local.settings.json file

Here's an example local.settings.json file with the optional settings:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_WORKER_RUNTIME": "dotnet",
"MySqlConnectionString": "",
"MySql_Trigger_MaxBatchSize": 300,
"MySql_Trigger_PollingIntervalMs": 1000,
"MySql_Trigger_MaxChangesPerWorker": 100
}
}
```


## Set up change tracking (required)

Setting up change tracking for use with the Azure Database for MySQL trigger requires you to add a column in a table by using a function. You can complete these steps from any MySQL tool that supports running queries, including [Visual Studio Code](/en-us/sql/tools/visual-studio-code/mssql-extensions) or [Azure Data Studio](/en-us/azure-data-studio/download-azure-data-studio).

Azure Database for MySQL trigger bindings use `az_func_updated_at`

and column data to monitor the user table for changes. As such, you need to alter the table structure to allow change tracking on the MySQL table before you use the trigger support. You can enable the change tracking on a table through the following query. For example, enable it on the `Products`

table:

```
ALTER TABLE Products;
ADD az_func_updated_at
TIMESTAMP DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The table for leases contains all columns that correspond to the primary key from the user table and two more columns: `az_func_AttemptCount`

and `az_func_LeaseExpirationTime`

. If any of the primary key columns have the same name, the result is an error message that lists conflicts. In this case, the listed primary key columns must be renamed for the trigger to work.

## Enable runtime-driven scaling

Optionally, your functions can scale automatically based on the number of changes that are pending to be processed in the user table. To allow your functions to scale properly on the Premium plan when you're using Azure Database for MySQL triggers, you need to enable runtime scale monitoring.

In the Azure portal, in your function app, select

**Configuration**.On the

**Function runtime settings**tab, for**Runtime Scale Monitoring**, select**On**.

## Retry support

### Startup retries

If an exception occurs during startup, the host runtime automatically attempts to restart the trigger listener with an exponential backoff strategy. These retries continue until either the listener is successfully started or the startup is canceled.

### Function exception retries

If an exception occurs in the user function during change processing, the batch of rows currently being processed is retried again in 60 seconds. Other changes are processed as normal during this time, but the rows in the batch that caused the exception are ignored until the time-out period elapses.

If the function execution fails five consecutive times for a particular row, that row is ignored for all future changes. Because the rows in a batch aren't deterministic, rows in a failed batch might end up in different batches in subsequent invocations. This behavior means that not all rows in the failed batch are necessarily ignored. If other rows in the batch caused the exception, the "good" rows might end up in a different batch that doesn't fail in future invocations.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-expressions-patterns -->

# Azure Functions binding expressions and patterns

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

One of the most powerful features of [triggers and bindings](functions-triggers-bindings) in Azure Functions is *binding expressions*. In the `function.json`

file and in function parameters and code, you can use expressions that resolve to values from various sources.

Most expressions are wrapped in curly braces. For example, in a queue trigger function, `{queueTrigger}`

resolves to the queue message text. If the `path`

property for a blob output binding is `container/{queueTrigger}`

and a queue message `HelloWorld`

triggers the function, a blob named `HelloWorld`

is created.

App settings

It's a best practice to manage secrets and connection strings by using app settings rather than configuration files. This practice limits access to these secrets and makes it safe to store files such as `function.json`

in public source-control repositories.

App settings are also useful whenever you want to change a configuration based on the environment. For example, in a test environment, you might want to monitor a different container for queue storage or blob storage.

Binding expressions for app settings are identified differently from other binding expressions: they're wrapped in percent signs rather than curly braces. For example, if the path for a blob output binding is `%Environment%/newblob.txt`

and the `Environment`

app setting value is `Development`

, a blob is created in the `Development`

container.

When a function is running locally, values for app settings come from the `local.settings.json`

file.

Note

The `connection`

property of triggers and bindings is a special case and automatically resolves values as app settings, without percent signs.

The following example is an Azure Queue Storage trigger that uses an app setting `%input_queue_name%`

to define the queue to trigger on:

```
{
"bindings": [
{
"name": "order",
"type": "queueTrigger",
"direction": "in",
"queueName": "%input_queue_name%",
"connection": "MY_STORAGE_ACCT_APP_SETTING"
}
]
}
```


You can use the same approach in class libraries:

```
[FunctionName("QueueTrigger")]
public static void Run(
[QueueTrigger("%input_queue_name%")]string myQueueItem,
ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
}
```


## Trigger file name

The `path`

value for a blob trigger can be a pattern that lets you refer to the name of the triggering blob in other bindings and function code. The pattern can also include filtering criteria that specify which blobs can trigger a function invocation.

For example, in the following binding for a blob trigger, the `path`

pattern is `sample-images/{filename}`

. This pattern creates a binding expression named `filename`

.

```
{
"bindings": [
{
"name": "image",
"type": "blobTrigger",
"path": "sample-images/{filename}",
"direction": "in",
"connection": "MyStorageConnection"
},
...
```


You can then use the expression `filename`

in an output binding to specify the name of the blob that you're creating:

```
...
{
"name": "imageSmall",
"type": "blob",
"path": "sample-images-sm/{filename}",
"direction": "out",
"connection": "MyStorageConnection"
}
],
}
```


Function code has access to this same value by using `filename`

as a parameter name:

```
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, ILogger log)
{
log.LogInformation($"Blob trigger processing: {filename}");
// ...
}
```


The same ability to use binding expressions and patterns applies to attributes in class libraries. In the following example, the attribute constructor parameters are the same `path`

values as the preceding `function.json`

examples:

```
[FunctionName("ResizeImage")]
public static void Run(
[BlobTrigger("sample-images/{filename}")] Stream image,
[Blob("sample-images-sm/{filename}", FileAccess.Write)] Stream imageSmall,
string filename,
ILogger log)
{
log.LogInformation($"Blob trigger processing: {filename}");
// ...
}
```


You can also create expressions for parts of the file name. In the following example, the function is triggered only on file names that match a pattern: `anyname-anyfile.csv`

.

```
{
"name": "myBlob",
"type": "blobTrigger",
"direction": "in",
"path": "testContainerName/{date}-{filetype}.csv",
"connection": "OrderStorageConnection"
}
```


For more information on how to use expressions and patterns in the blob path string, see the [reference for Azure Blob Storage bindings](functions-bindings-storage-blob).

## Trigger metadata

In addition to the data payload that a trigger provides (such as the content of the queue message that triggered a function), many triggers provide other metadata values. You can use these values as input parameters in C# and F# or as properties on the `context.bindings`

object in JavaScript.

For example, an Azure Queue Storage trigger supports the following properties:

`QueueTrigger`

(triggering message content if the string is valid)`DequeueCount`

`ExpirationTime`

`Id`

`InsertionTime`

`NextVisibleTime`

`PopReceipt`


These metadata values are accessible in the `function.json`

file properties. For example, suppose you use a queue trigger and the queue message contains the name of a blob that you want to read. In the `function.json`

file, you can use the `queueTrigger`

metadata property in the blob `path`

property, as shown in the following example:

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "queueTrigger",
"queueName": "myqueue-items",
"connection": "MyStorageConnection",
},
{
"name": "myInputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}",
"direction": "in",
"connection": "MyStorageConnection"
}
]
}
```


You can find details of metadata properties for each trigger in the corresponding reference article. For an example, see the [metadata for an Azure Queue Storage trigger](functions-bindings-storage-queue-trigger#message-metadata). Documentation is also available on the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.

## JSON payloads

In some scenarios, you can refer to the trigger payload's properties in the configuration for other bindings in the same function and in function code. This approach requires that the trigger payload is JSON and is smaller than a threshold specific to each trigger. Typically, the payload size needs to be less than 100 MB, but you should check the reference content for each trigger.

Using trigger payload properties might affect the performance of your application. It also forces the trigger parameter type to be a simple type (like a string) or a custom object type that represents JSON data. You can't use it with streams, clients, or other SDK types.

The following example shows the `function.json`

file for a webhook function that receives a blob name in JSON: `{"BlobName":"HelloWorld.txt"}`

. A blob input binding reads the blob, and the HTTP output binding returns the blob contents in the HTTP response. Notice that the blob input binding gets the blob name by referring directly to the `BlobName`

property (`"path": "strings/{BlobName}"`

).

```
{
"bindings": [
{
"name": "info",
"type": "httpTrigger",
"direction": "in",
"webHookType": "genericJson"
},
{
"name": "blobContents",
"type": "blob",
"direction": "in",
"path": "strings/{BlobName}",
"connection": "AzureWebJobsStorage"
},
{
"name": "res",
"type": "http",
"direction": "out"
}
]
}
```


For this approach to work in C# and F#, you need a class that defines the fields to be deserialized, as in the following example:

```
using System.Net;
using Microsoft.Extensions.Logging;
public class BlobInfo
{
public string BlobName { get; set; }
}
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents, ILogger log)
{
if (blobContents == null) {
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.LogInformation($"Processing: {info.BlobName}");
return req.CreateResponse(HttpStatusCode.OK, new {
data = $"{blobContents}"
});
}
```


In JavaScript, JSON deserialization is automatically performed:

```
module.exports = async function (context, info) {
if ('BlobName' in info) {
context.res = {
body: { 'data': context.bindings.blobContents }
}
}
else {
context.res = {
status: 404
};
}
}
```


### Dot notation

If some of the properties in your JSON payload are objects with properties, you can refer to them directly by using dot (`.`

) notation. This notation doesn't work for [Azure Cosmos DB](functions-bindings-cosmosdb-v2) or [Azure Table Storage](functions-bindings-storage-table-output) bindings.

For example, suppose your JSON looks like this example:

```
{
"BlobName": {
"FileName":"HelloWorld",
"Extension":"txt"
}
}
```


You can refer directly to `FileName`

as `BlobName.FileName`

. With this JSON format, here's what the `path`

property in the preceding example would look like:

```
"path": "strings/{BlobName.FileName}.{BlobName.Extension}",
```


In C#, you would need two classes:

```
public class BlobInfo
{
public BlobName BlobName { get; set; }
}
public class BlobName
{
public string FileName { get; set; }
public string Extension { get; set; }
}
```


## New GUIDs

The `{rand-guid}`

binding expression creates a GUID. The following blob path in a `function.json`

file creates a blob with a name like *50710cb5-84b9-4d87-9d83-a03d6976a682.txt*:

```
{
"type": "blob",
"name": "blobOutput",
"direction": "out",
"path": "my-output-container/{rand-guid}.txt"
}
```


## Current date and time

The binding expression `DateTime`

resolves to `DateTime.UtcNow`

. The following blob path in a `function.json`

file creates a blob with a name like *2018-02-16T17-59-55Z.txt*:

```
{
"type": "blob",
"name": "blobOutput",
"direction": "out",
"path": "my-output-container/{DateTime}.txt"
}
```


## Binding at runtime

In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in `function.json`

and attributes. Imperative binding is useful when binding parameters need to be computed at runtime rather than design time. To learn more, see the [C# developer reference](functions-dotnet-class-library#binding-at-runtime) or the [C# script developer reference](functions-reference-csharp#binding-at-runtime).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-networking-faq -->

# Frequently asked questions about networking in Azure Functions

This article lists frequently asked questions about networking in Azure Functions. For a more comprehensive overview, see [Functions networking options](functions-networking-options).

## How do I set a static IP in Functions?

Deploying a function in an App Service Environment is the primary way to have static inbound and outbound IP addresses for your functions. For details on using an App Service Environment, start with the article [Create and use an internal load balancer with an App Service Environment](../app-service/environment/create-ilb-ase).

You can also use a virtual network NAT gateway to route outbound traffic through a public IP address that you control. To learn more, see [Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway](functions-how-to-use-nat-gateway).

## How do I restrict internet access to my function?

You can restrict internet access in a couple of ways:

[Private endpoints](functions-networking-options#private-endpoints): Restrict inbound traffic to your function app by private link over your virtual network, effectively blocking inbound traffic from the public internet.[IP restrictions](../app-service/app-service-ip-restrictions): Restrict inbound traffic to your function app by IP range.- Under IP restrictions, you are also able to configure
[Service Endpoints](../virtual-network/virtual-network-service-endpoints-overview), which restrict your Function to only accept inbound traffic from a particular virtual network.

- Under IP restrictions, you are also able to configure
- Removal of all HTTP triggers. For some applications, it's enough to simply avoid HTTP triggers and use any other event source to trigger your function.

Keep in mind that the Azure portal editor requires direct access to your running function. Any code changes through the Azure portal will require the device you're using to browse the portal to have its IP added to the approved list. But you can still use anything under the platform features tab with network restrictions in place.

## How do I restrict my function app to a virtual network?

You are able to restrict **inbound** traffic for a function app to a virtual network using [Service Endpoints](functions-networking-options#use-service-endpoints). This configuration still allows the function app to make outbound calls to the internet.

To completely restrict a function such that all traffic flows through a virtual network, you can use a [private endpoints](functions-networking-options#private-endpoints) with outbound virtual network integration or an App Service Environment. To learn more, see [Integrate Azure Functions with an Azure virtual network by using private endpoints](functions-create-vnet).

## How can I access resources in a virtual network from a function app?

You can access resources in a virtual network from a running function by using virtual network integration. For more information, see [Virtual network integration](functions-networking-options#virtual-network-integration).

## How do I access resources protected by service endpoints?

By using virtual network integration you can access service-endpoint-secured resources from a running function. For more information, see [virtual network integration](functions-networking-options#virtual-network-integration).

## How can I trigger a function from a resource in a virtual network?

You are able to allow HTTP triggers to be called from a virtual network using [Service Endpoints](functions-networking-options#use-service-endpoints) or [Private Endpoint connections](functions-networking-options#private-endpoints).

You can also trigger a function from all other resources in a virtual network by deploying your function app to a Premium plan, App Service plan, or App Service Environment. See [non-HTTP virtual network triggers](functions-networking-options#virtual-network-triggers-non-http)
for more information

## How can I deploy my function app in a virtual network?

Deploying to an App Service Environment is the only way to create a function app that's wholly inside a virtual network. For details on using an internal load balancer with an App Service Environment, start with the article [Create and use an internal load balancer with an App Service Environment](../app-service/environment/create-ilb-ase).

For scenarios where you need only one-way access to virtual network resources, or less comprehensive network isolation, see the [Functions networking overview](functions-networking-options).

## Next steps

To learn more about networking and functions:

[Follow the tutorial about getting started with virtual network integration](functions-create-vnet)[Learn more about the networking options in Azure Functions](functions-networking-options)[Learn more about virtual network integration with App Service and Functions](../app-service/overview-vnet-integration)[Learn more about virtual networks in Azure](../virtual-network/virtual-networks-overview)[Enable more networking features and control with App Service Environments](../app-service/environment/intro)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache -->

# Overview of Azure functions for Azure Redis

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to use either Azure Managed Redis or Azure Cache for Redis with Azure Functions to create optimized serverless and event-driven architectures.

Azure Functions provides an event-driven programming model where triggers and bindings are key features. With Azure Functions, you can easily build event-driven serverless applications. Azure Redis services (Azure Managed Redis and Azure Cache for Redis) provide a set of building blocks and best practices for building distributed applications, including microservices, state management, pub/sub messaging, and more.

Azure Redis can be used as a trigger for Azure Functions, allowing you to initiate a serverless workflow. This functionality can be highly useful in data architectures like a write-behind cache, or any event-based architectures.

You can integrate Azure Redis and Azure Functions to build functions that react to events from Azure Redis or external systems.

| Action | Direction |
|---|---|
|

[Trigger on Redis lists](functions-bindings-cache-trigger-redislist)[Trigger on Redis streams](functions-bindings-cache-trigger-redisstream)[Read a cached value](functions-bindings-cache-input)[Write a values to cache](functions-bindings-cache-output)## Scope of availability for functions triggers and bindings

| Tier | Azure Cache for Redis (Basic, Standard, Premium, Enterprise, Enterprise Flash) | Azure Managed Redis (Memory Optimized, Basic, Compute Optimized, Flash Optimized) |
|---|---|---|
| Pub/Sub | Yes | Yes |
| Lists | Yes | Yes |
| Streams | Yes | Yes |
| Bindings | Yes | Yes |

Important

Redis triggers are currently only supported for functions running in either a [Elastic Premium plan](functions-premium-plan) or a dedicated [App Service plan](dedicated-plan).

## Install extension

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Redis).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Redis
```


## Install bundle

To be able to use this binding extension in your app, make sure that the *host.json* file in the root of your project contains this `extensionBundle`

reference:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


In this example, the `version`

value of `[4.0.0, 5.0.0)`

instructs the Functions host to use a bundle version that is at least `4.0.0`

but less than `5.0.0`

, which includes all potential versions of 4.x. This notation effectively maintains your app on the latest available minor version of the v4.x extension bundle.

When possible, you should use the latest extension bundle major version and allow the runtime to automatically maintain the latest minor version. You can view the contents of the latest bundle on the [extension bundles release page](https://github.com/Azure/azure-functions-extension-bundles/releases/latest). For more information, see [Azure Functions extension bundles](extension-bundles).

## Update packages

Add the [Azure Functions Java Redis Annotations package](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-redis) to your project by updating the `pom.xml`

file to add this dependency:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-redis</artifactId>
<version>1.0.0</version>
</dependency>
```


## Redis connection string

Azure Redis triggers and bindings have a required property that indicates the application setting or collection name that contains cache connection information. The Redis trigger or binding looks for an environmental variable holding the connection string with the name passed to the `Connection`

parameter.

In local development, the `Connection`

can be defined using the [local.settings.json](/en-us/azure/azure-functions/functions-develop-local#local-settings-file) file. When deployed to Azure, [application settings](/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings) can be used.

When connecting to a cache instance with an Azure function, you can use one of these kinds of connections in your deployments:

A user-assigned managed identity must be associated with your function app, and that identity must also be granted explicit permissions in your cache service. For more information, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).

These examples show the key name and value of app settings required to connect to each cache service based on the kind of client authentication, assuming that the `Connection`

property in the binding is set to `Redis`

.

```
"Redis__redisHostName": "<cacheName>.<region>.redis.azure.net",
"Redis__principalId": "<principalId>",
"Redis__clientId": "<clientId>"
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table-input -->

# Azure Tables input bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Azure Tables input binding to read a table in [Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table/introduction) or [Azure Table Storage](../storage/tables/table-storage-overview).

For information on setup and configuration details, see the [overview](functions-bindings-storage-table).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Example

The usage of the binding depends on the extension package version and the C# modality used in your function app, which can be one of the following:

An [isolated worker process class library](dotnet-isolated-process-guide) compiled C# function runs in a process isolated from the runtime.

Choose a version to see examples for the mode and version.

The following `MyTableData`

class represents a row of data in the table:

```
public class MyTableData : Azure.Data.Tables.ITableEntity
{
public string Text { get; set; }
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public DateTimeOffset? Timestamp { get; set; }
public ETag ETag { get; set; }
}
```


The following function, which is started by a Queue Storage trigger, reads a row key from the queue, which is used to get the row from the input table. The expression `{queueTrigger}`

binds the row key to the message metadata, which is the message string.

```
[Function("TableFunction")]
[TableOutput("OutputTable", Connection = "AzureWebJobsStorage")]
public static MyTableData Run(
[QueueTrigger("table-items")] string input,
[TableInput("MyTable", "<PartitionKey>", "{queueTrigger}")] MyTableData tableInput,
FunctionContext context)
{
var logger = context.GetLogger("TableFunction");
logger.LogInformation($"PK={tableInput.PartitionKey}, RK={tableInput.RowKey}, Text={tableInput.Text}");
return new MyTableData()
{
PartitionKey = "queue",
RowKey = Guid.NewGuid().ToString(),
Text = $"Output record with rowkey {input} created at {DateTime.Now}"
};
}
```


The following Queue-triggered function returns the first 5 entities as an `IEnumerable<T>`

, with the partition key value set as the queue message.

```
[Function("TestFunction")]
public static void Run([QueueTrigger("myqueue", Connection = "AzureWebJobsStorage")] string partition,
[TableInput("inTable", "{queueTrigger}", Take = 5, Filter = "Text eq 'test'",
Connection = "AzureWebJobsStorage")] IEnumerable<MyTableData> tableInputs,
FunctionContext context)
{
var logger = context.GetLogger("TestFunction");
logger.LogInformation(partition);
foreach (MyTableData tableInput in tableInputs)
{
logger.LogInformation($"PK={tableInput.PartitionKey}, RK={tableInput.RowKey}, Text={tableInput.Text}");
}
}
```


The `Filter`

and `Take`

properties are used to limit the number of entities returned.

The following example shows an HTTP triggered function which returns a list of person objects who are in a specified partition in Table storage. In the example, the partition key is extracted from the http route, and the tableName and connection are from the function settings.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() { return this.PartitionKey; }
public void setPartitionKey(String key) { this.PartitionKey = key; }
public String getRowKey() { return this.RowKey; }
public void setRowKey(String key) { this.RowKey = key; }
public String getName() { return this.Name; }
public void setName(String name) { this.Name = name; }
}
@FunctionName("getPersonsByPartitionKey")
public Person[] get(
@HttpTrigger(name = "getPersons", methods = {HttpMethod.GET}, authLevel = AuthorizationLevel.FUNCTION, route="persons/{partitionKey}") HttpRequestMessage<Optional<String>> request,
@BindingName("partitionKey") String partitionKey,
@TableInput(name="persons", partitionKey="{partitionKey}", tableName="%MyTableName%", connection="MyConnectionString") Person[] persons,
final ExecutionContext context) {
context.getLogger().info("Got query for person related to persons with partition key: " + partitionKey);
return persons;
}
```


The TableInput annotation can also extract the bindings from the json body of the request, like the following example shows.

```
@FunctionName("GetPersonsByKeysFromRequest")
public HttpResponseMessage get(
@HttpTrigger(name = "getPerson", methods = {HttpMethod.GET}, authLevel = AuthorizationLevel.FUNCTION, route="query") HttpRequestMessage<Optional<String>> request,
@TableInput(name="persons", partitionKey="{partitionKey}", rowKey = "{rowKey}", tableName="%MyTableName%", connection="MyConnectionString") Person person,
final ExecutionContext context) {
if (person == null) {
return request.createResponseBuilder(HttpStatus.NOT_FOUND)
.body("Person not found.")
.build();
}
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(person)
.build();
}
```


The following example uses a filter to query for persons with a specific name in an Azure Table, and limits the number of possible matches to 10 results.

```
@FunctionName("getPersonsByName")
public Person[] get(
@HttpTrigger(name = "getPersons", methods = {HttpMethod.GET}, authLevel = AuthorizationLevel.FUNCTION, route="filter/{name}") HttpRequestMessage<Optional<String>> request,
@BindingName("name") String name,
@TableInput(name="persons", filter="Name eq '{name}'", take = "10", tableName="%MyTableName%", connection="MyConnectionString") Person[] persons,
final ExecutionContext context) {
context.getLogger().info("Got query for person related to persons with name: " + name);
return persons;
}
```


The following example shows a table input binding that uses a queue trigger to read a single table row. The binding specifies a `partitionKey`

and a `rowKey`

. The `rowKey`

value "{queueTrigger}" indicates that the row key comes from the queue message string.

```
import { app, input, InvocationContext } from '@azure/functions';
const tableInput = input.table({
tableName: 'Person',
partitionKey: 'Test',
rowKey: '{queueTrigger}',
connection: 'MyStorageConnectionAppSetting',
});
interface PersonEntity {
PartitionKey: string;
RowKey: string;
Name: string;
}
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<void> {
context.log('Node.js queue trigger function processed work item', queueItem);
const person = <PersonEntity>context.extraInputs.get(tableInput);
context.log('Person entity name: ' + person.Name);
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [tableInput],
handler: storageQueueTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const tableInput = input.table({
tableName: 'Person',
partitionKey: 'Test',
rowKey: '{queueTrigger}',
connection: 'MyStorageConnectionAppSetting',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [tableInput],
handler: (queueItem, context) => {
context.log('Node.js queue trigger function processed work item', queueItem);
const person = context.extraInputs.get(tableInput);
context.log('Person entity name: ' + person.Name);
},
});
```


The following function uses a queue trigger to read a single table row as input to a function.

In this example, the binding configuration specifies an explicit value for the table's `partitionKey`

and uses an expression to pass to the `rowKey`

. The `rowKey`

expression, `{queueTrigger}`

, indicates that the row key comes from the queue message string.

Binding configuration in *function.json*:

```
{
"bindings": [
{
"queueName": "myqueue-items",
"connection": "MyStorageConnectionAppSetting",
"name": "MyQueueItem",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "PersonEntity",
"type": "table",
"tableName": "Person",
"partitionKey": "Test",
"rowKey": "{queueTrigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "in"
}
],
"disabled": false
}
```


PowerShell code in *run.ps1*:

```
param($MyQueueItem, $PersonEntity, $TriggerMetadata)
Write-Host "PowerShell queue trigger function processed work item: $MyQueueItem"
Write-Host "Person entity name: $($PersonEntity.Name)"
```


The following function uses an HTTP trigger to read a single table row as input to a function.

In this example, binding configuration specifies an explicit value for the table's `partitionKey`

and uses an expression to pass to the `rowKey`

. The `rowKey`

expression, `{id}`

indicates that the row key comes from the `{id}`

part of the route in the request.

```
import json
import azure.functions as func
app = func.FunctionApp()
@app.route(route="messages/{id}")
@app.table_input(arg_name="messageJSON",
connection="AzureWebJobsStorage",
table_name="messages",
row_key='{id}',
partition_key="message")
def table_in_binding(req: func.HttpRequest, messageJSON):
message = json.loads(messageJSON)
return func.HttpResponse(f"Table row: {messageJSON}")
```


With this simple binding, you can't programmatically handle a case in which no row that has a row key ID is found. For more fine-grained data selection, use the [storage SDK](/en-us/azure/developer/python/sdk/examples/azure-sdk-example-storage-use?tabs=cmd).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#table-input).

In [C# class libraries](dotnet-isolated-process-guide), the `TableInputAttribute`

supports the following properties:

| Attribute property | Description |
|---|---|
TableName |
The name of the table. |
PartitionKey |
Optional. The partition key of the table entity to read. |
RowKey |
Optional. The row key of the table entity to read. |
Take |
Optional. The maximum number of entities to read into an
`IEnumerable<T>` |

`RowKey`

.**Filter**[. Can't be used with](/en-us/dotnet/api/system.collections.generic.ienumerable-1)`IEnumerable<T>`

`RowKey`

.**Connection**[Connections](#connections).## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@TableInput`

annotation on parameters whose value would come from Table storage. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

. This annotation supports the following elements:

| Element | Description |
|---|---|
|
The name of the variable that represents the table or entity in function code. |
|
The name of the table. |
|
Optional. The partition key of the table entity to read. |
|
Optional. The row key of the table entity to read. |
|
Optional. The maximum number of entities to read. |
|
Optional. An OData filter expression for table input. |
|
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `input.table()`

method.

| Property | Description |
|---|---|
tableName |
The name of the table. |
partitionKey |
Optional. The partition key of the table entity to read. |
rowKey |
Optional. The row key of the table entity to read. Can't be used with `take` or `filter` . |
take |
Optional. The maximum number of entities to return. Can't be used with `rowKey` . |
filter |
Optional. An OData filter expression for the entities to return from the table. Can't be used with `rowKey` . |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `table` . This property is set automatically when you create the binding in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the binding in the Azure portal. |
name |
The name of the variable that represents the table or entity in function code. |
tableName |
The name of the table. |
partitionKey |
Optional. The partition key of the table entity to read. |
rowKey |
Optional. The row key of the table entity to read. Can't be used with `take` or `filter` . |
take |
Optional. The maximum number of entities to return. Can't be used with `rowKey` . |
filter |
Optional. An OData filter expression for the entities to return from the table. Can't be used with `rowKey` . |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to your table service. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections)

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string for tables in Azure Table storage, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage). To obtain a connection string for tables in Azure Cosmos DB for Table, follow the steps shown at the [Azure Cosmos DB for Table FAQ](/en-us/azure/cosmos-db/table/table-api-faq#what-is-the-connection-string-that-i-need-to-use-to-connect-to-the-api-for-table-).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage". If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [the Tables API extension](functions-bindings-storage-table#table-api-extension), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). This only applies when accessing tables in Azure Storage. To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Table Service URI | `<CONNECTION_NAME_PREFIX>__tableServiceUri` 1 |
The data plane URI of the Azure Storage table service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.table.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__serviceUri`

can be used as an alias. If both forms are provided, the `tableServiceUri`

form is used. The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables.

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables in Azure Storage. The URI can only designate the table service. As an alternative, you can provide a URI specifically for each service under the same prefix, allowing a single connection to be used.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your Azure Storage table service at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Azure Tables extension against Azure Storage in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles (Azure Storage1) |
|---|---|
| Input binding |
|

[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)1 If your app is instead connecting to tables in Azure Cosmos DB for Table, using an identity isn't supported and the connection must use a connection string.

## Usage

The usage of the binding depends on the extension package version, and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see usage details for the mode and version.

When working with a single table entity, the Azure Tables input binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements
|

[ITableEntity](/en-us/dotnet/api/azure.data.tables.itableentity)or have a string`RowKey`

property and a string `PartitionKey`

property.[TableEntity](/en-us/dotnet/api/azure.data.tables.tableentity)1When working with multiple entities from a query, the Azure Tables input binding can bind to the following types:

| Type | Description |
|---|---|
`IEnumerable<T>` where `T` implements
|
An enumeration of entities returned by the query. Each entry represents one entity. The type `T` must implement
`RowKey` property and a string `PartitionKey` property. |
1 |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Tables 1.2.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables/1.2.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

The [TableInput](/en-us/java/api/com.microsoft.azure.functions.annotation.tableinput) attribute gives you access to the table row that triggered the function.

Data is passed to the input parameter as specified by the `name`

key in the *function.json* file. Specifying The `partitionKey`

and `rowKey`

allows you to filter to specific records.

Table data is passed to the function as a JSON string. De-serialize the message by calling `json.loads`

as shown in the input [example](#example).

For specific usage details, see [Example](#example).
