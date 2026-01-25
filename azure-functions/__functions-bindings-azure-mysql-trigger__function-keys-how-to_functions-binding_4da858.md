---
merged_at: 2026-01-25T15:41:11.645800
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-azure-mysql-trigger__function-keys-how-to_functions-bindings_885103.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-azure-mysql-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-trigger -->

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

<!-- DOCUMENTO FUSIONADO: _function-keys-how-to_functions-bindings-expressions-patterns.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: function-keys-how-to.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/function-keys-how-to -->

# Work with access keys in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you use secret keys to make it more difficult to access your function endpoints. This article describes the kinds of access keys that Functions supports, and how to work with access keys.

While access keys provide some mitigation against unwanted access, you should consider other options to secure HTTP endpoints in production. For example, it's not a good practice to distribute shared secrets in a public app. If your function is being called from a public client, you should consider implementing these or other security mechanisms:

[Enable App Service Authentication/Authorization](security-concepts#enable-app-service-authenticationauthorization)[Use Azure API Management (APIM) to authenticate requests](security-concepts#use-azure-api-management-apim-to-authenticate-requests)[Deploy your function app to a virtual network](security-concepts#deploy-your-function-app-to-a-virtual-network)[Deploy your function app in isolation](security-concepts#deploy-your-function-app-in-isolation)

Access keys provide the basis for HTTP authorization in HTTP triggered functions. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).

## Understand keys

The scope of an access key and the actions it supports depend on the type of access key.

| Key type | Key name | HTTP auth level | Description |
|---|---|---|---|
Function |
`default` or user defined |
`function` |
Allows access only to a specific function endpoint. |
Host |
`default` or user defined |
`function` |
Allows access to all function endpoints in a function app. |
Master |
`_master` |
`admin` |
Special host key that also provides administrative access to the runtime REST APIs in a function app. Because the master key grants elevated permissions in your function app, you shouldn't share this key with third parties or distribute it in native client applications. |
System |
Depends on the extension | n/a | Specific extensions might require a system-managed key to access webhook endpoints. System keys are designed for extension-specific function endpoints that get called by internal components. For example, the
Only specific extensions can create system keys. You can't explicitly set their values. Like other keys, you can generate a new value for the key from the portal or by using the key APIs. |

Each key is named for reference. There's a default key (named `default`

) at the function and host level. Function keys take precedence over host keys. When two keys are defined with the same name, the function key is always used.

The following table compares the uses for various kinds of access keys:

| Action | Scope | Key type |
|---|---|---|
| Execute a function | Specific function | Function |
| Execute a function | Any function | Function or host |
Call an `admin` endpoint |
Function app | Master-only |
| Call Durable Task extension APIs | Function app* |
System |
| Call an extension-specific Webhook (internal) | Function app* |
system |

*Scope determined by the extension.

## Key requirements

In Functions, access keys are randomly generated 32-byte arrays that are encoded as URL-safe base-64 strings. While you can generate your own access keys and use them with Functions, we strongly recommend that you instead allow Functions to generate all of your access keys for you.

Functions-generated access keys include special signature and checksum values that indicate the type of access key and that Azure Functions generated it. Having these extra components in the key itself makes it much easier to determine the source of these kinds of secrets located during security scanning and other automated processes.

To allow Functions to generate your keys for you, don't supply the key `value`

to any of the APIs that you can use to generate keys.

## Manage key storage

Keys are stored as part of your function app in Azure and are encrypted at rest. By default, keys are stored in a Blob storage container in the account provided by the `AzureWebJobsStorage`

setting. You can use the [ AzureWebJobsSecretStorageType](functions-app-settings#azurewebjobssecretstoragetype) setting to override this default behavior and instead store keys in one of these alternate locations:

| Location | Value | Description |
|---|---|---|
| A second storage account | `blob` |
Stores keys in Blob storage in a storage account that's different than the one used by the Functions runtime. The specific account and container used are defined by a shared access signature (SAS) URL set in the
`AzureWebJobsSecretStorageSas` |

`AzureWebJobsSecretStorageSas`

setting when the SAS URL changes.[Azure Key Vault](/en-us/azure/key-vault/general/overview)`keyvault`

[is used to store keys.](functions-app-settings#azurewebjobssecretstoragekeyvaulturi)`AzureWebJobsSecretStorageKeyVaultUri`

`files`

`kubernetes`

[AzureWebJobsKubernetesSecretName](functions-app-settings#azurewebjobskubernetessecretname)is used to store keys. Supported only when your function app is deployed to Kubernetes. The[Azure Functions Core Tools](functions-run-local)generates the values automatically when you use it to deploy your app to a Kubernetes cluster.[Immutable secrets](https://kubernetes.io/docs/concepts/configuration/secret/#secret-immutable)aren't supported.`ContainerApps`

When you use Key Vault for key storage, the app settings you need depend on the managed identity type, either system-assigned or user-assigned.

| Setting name | System-assigned | User-assigned | App registration |
|---|---|---|---|
|

[AzureWebJobsSecretStorageKeyVaultClientId](functions-app-settings#azurewebjobssecretstoragekeyvaultclientid)[AzureWebJobsSecretStorageKeyVaultClientSecret](functions-app-settings#azurewebjobssecretstoragekeyvaultclientsecret)[AzureWebJobsSecretStorageKeyVaultTenantId](functions-app-settings#azurewebjobssecretstoragekeyvaulttenantid)Important

Secrets aren't scoped to individual function apps through the `AzureWebJobsSecretStorageKeyVaultUri`

setting. If multiple function apps are configured to use the same Key Vault they share the same secrets, potentially leading to key collisions or overwrites. To avoid unintended behavior, we recommend that you use a separate Key Vault instance for each function app.

## Use access keys

HTTP triggered functions can generally be called by using a URL that includes the function name. When the authorization level of a given function is set as a value other than `anonymous`

, you must also provide an access key in your request. The access key can either be provided in the URL using the `?code=`

query string or in the request header (`x-functions-key`

). For more information, see [Access key authorization](functions-bindings-http-webhook-trigger#api-key-authorization).

To access the runtime REST APIs (under `/admin/`

), you must provide the master key (`_master`

) in the `x-functions-key`

request header. You can [remove the admin endpoints](security-concepts#disable-administrative-endpoints) using the `functionsRuntimeAdminIsolationEnabled`

site property.

## Get your function access keys

You can get function and host keys programmatically by using these Azure Resource Manager APIs:

To learn how to call Azure Resource Manager APIs, see the [Azure REST API reference](/en-us/rest/api/azure/).

You can use these methods to get access keys without having to use the REST APIs.

Sign in to the Azure portal, then search for and select

**Function App**.Select the function app you want to work with.

In the left menu, expand

**Functions**, and then select**App keys**.The

**App keys**page appears.  the host keys are displayed, which can be used to access any function in the app. The system key is also displayed, which gives anyone administrator-level access to all function app APIs.

You can also practice least privilege by using the key for a specific function. You can get function-specific keys from the **Function keys** tab of a specific HTTP-triggered function.

Tip

You can also obtain access keys for your functions by using the Azure Functions Core Tools command `func azure functionapp list-functions`

with the `--show-keys`

option. For more information, see the [Azure Functions Core Tools reference](functions-core-tools-reference#func-azure-functionapp-list-functions).

## Renew or create access keys

When you renew or create your access key values, you must manually redistribute the updated key values to all clients that call your function.

You can renew function and host keys programmatically or create new ones by using these Azure Resource Manager APIs:

[Create Or Update Function Secret](/en-us/rest/api/appservice/webapps/createorupdatefunctionsecret)[Create Or Update Function Secret Slot](/en-us/rest/api/appservice/webapps/createorupdatefunctionsecretslot)[Create Or Update Host Secret](/en-us/rest/api/appservice/webapps/createorupdatehostsecret)[Create Or Update Host Secret Slot](/en-us/rest/api/appservice/webapps/createorupdatehostsecretslot)

To learn how to call Azure Resource Manager APIs, see the [Azure REST API reference](/en-us/rest/api/azure/).

You can use these methods to get access keys without having to manually create calls to the REST APIs.

Sign in to the Azure portal, then search for and select

**Function App**.Select the function app you want to work with.

In the left menu, expand

**Functions**, and then select**App keys**.The

**App keys**page appears.  the host keys are displayed, which can be used to access any function in the app. The system key is also displayed, which gives anyone administrator-level access to all function app APIs.Select

**Renew key value**next to the key you want to renew, then select**Renew and save**.

You can also renew a function key in the **Function keys** tab of a specific HTTP-triggered function.

## Delete access keys

You can delete function and host keys programmatically by using these Azure Resource Manager APIs:

To learn how to call Azure Resource Manager APIs, see the [Azure REST API reference](/en-us/rest/api/azure/).


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-expressions-patterns.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-expressions-patterns -->

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

<!-- DOCUMENTO FUSIONADO: _functions-bindings-storage-table-input_functions-host-json-v1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-storage-table-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table-input -->

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


---

<!-- DOCUMENTO FUSIONADO: functions-host-json-v1.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json-v1 -->

# host.json reference for Azure Functions 1.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The *host.json* metadata file contains configuration options that affect all functions in a function app instance. This article lists the settings that are available for the version 1.x runtime. The JSON schema is at [http://json.schemastore.org/host](http://json.schemastore.org/host).

Note

This article is for Azure Functions 1.x. For a reference of host.json in Functions 2.x and later, see [host.json reference for Azure Functions 2.x](functions-host-json).

Other function app configuration options are managed in your [app settings](functions-app-settings).

Some host.json settings are only used when running locally in the [local.settings.json](functions-develop-local#local-settings-file) file.

## Sample host.json file

The following sample *host.json* files have all possible options specified.

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
},
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
},
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix"
}
},
"eventHub": {
"maxBatchSize": 64,
"prefetchCount": 256,
"batchCheckpointFrequency": 1
},
"functions": [ "QueueProcessor", "GitHubWebHook" ],
"functionTimeout": "00:05:00",
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
},
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 20,
"maxConcurrentRequests": 10,
"dynamicThrottlesEnabled": false
},
"id": "9f4ea53c5136457d883d685e57164f08",
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
},
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
},
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
},
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
},
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
},
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
},
"watchDirectories": [ "Shared" ],
}
```


The following sections of this article explain each top-level property. All are optional unless otherwise indicated.

## aggregator

Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](configure-monitoring#configure-the-aggregator).

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


| Property | Default | Description |
|---|---|---|
| batchSize | 1000 | Maximum number of requests to aggregate. |
| flushTimeout | 00:00:30 | Maximum time period to aggregate. |

Function invocations are aggregated when the first of the two limits are reached.

## applicationInsights

Controls the [sampling feature in Application Insights](configure-monitoring#configure-sampling).

```
{
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
}
}
```


| Property | Default | Description |
|---|---|---|
| isEnabled | true | Enables or disables sampling. |
| maxTelemetryItemsPerSecond | 5 | The threshold at which sampling begins. |

## DocumentDB

Configuration settings for the [Azure Cosmos DB trigger and bindings](functions-bindings-cosmosdb).

```
{
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix1"
}
}
}
```


| Property | Default | Description |
|---|---|---|
| GatewayMode | Gateway | The connection mode used by the function when connecting to the Azure Cosmos DB service. Options are `Direct` and `Gateway` |
| Protocol | Https | The connection protocol used by the function when connection to the Azure Cosmos DB service. Read
|

## durableTask

Configuration settings for [Durable Functions](durable/durable-functions-overview).

Note

All major versions of Durable Functions are supported on all versions of the Azure Functions runtime. However, the schema of the *host.json* configuration differs slightly depending on the version of the Azure Functions runtime and the version of the Durable Functions extension that you use.

The following code provides two examples of `durableTask`

settings in *host.json*: one for Durable Functions 2.x and one for Durable Functions 1.x. You can use both examples with Azure Functions 2.0 and 3.0. With Azure Functions 1.0, the available settings are the same, but the `durableTask`

section of *host.json* is located in the root of the *host.json* configuration instead of being a field under `extensions`

.

```
{
"extensions": {
"durableTask": {
"hubName": "MyTaskHub",
"defaultVersion": "1.0",
"versionMatchStrategy": "CurrentOrOlder",
"versionFailureStrategy": "Reject",
"storageProvider": {
"connectionStringName": "AzureWebJobsStorage",
"controlQueueBatchSize": 32,
"controlQueueBufferThreshold": 256,
"controlQueueVisibilityTimeout": "00:05:00",
"FetchLargeMessagesAutomatically": true,
"maxQueuePollingInterval": "00:00:30",
"partitionCount": 4,
"trackingStoreConnectionStringName": "TrackingStorage",
"trackingStoreNamePrefix": "DurableTask",
"useLegacyPartitionManagement": false,
"useTablePartitionManagement": true,
"workItemQueueVisibilityTimeout": "00:05:00",
"QueueClientMessageEncoding": "UTF8"
},
"tracing": {
"traceInputsAndOutputs": false,
"traceReplayEvents": false,
},
"httpSettings":{
"defaultAsyncRequestSleepTimeMilliseconds": 30000,
"useForwardedHost": false,
},
"notifications": {
"eventGrid": {
"topicEndpoint": "https://topic_name.westus2-1.eventgrid.azure.net/api/events",
"keySettingName": "EventGridKey",
"publishRetryCount": 3,
"publishRetryInterval": "00:00:30",
"publishEventTypes": [
"Started",
"Completed",
"Failed",
"Terminated"
]
}
},
"maxConcurrentActivityFunctions": 10,
"maxConcurrentOrchestratorFunctions": 10,
"maxConcurrentEntityFunctions": 10,
"extendedSessionsEnabled": false,
"extendedSessionIdleTimeoutInSeconds": 30,
"useAppLease": true,
"useGracefulShutdown": false,
"maxEntityOperationBatchSize": 50,
"maxOrchestrationActions": 100000,
"storeInputsInOrchestrationHistory": false
}
}
}
```


| Property | Default value | Description |
|---|---|---|
| hubName | TestHubName (DurableFunctionsHub in v1.x) | The name of the hub that stores the current state of a function app. Task hub names must start with a letter and consist of only letters and numbers. If you don't specify a name, the default value is used. Alternate task hub names can be used to isolate multiple Durable Functions applications from each other, even if they use the same storage back end. For more information, see
|

[orchestration versioning](durable/durable-functions-orchestration-versioning)feature to enable scenarios like zero-downtime deployments with breaking changes. You can use any string value for the version.`None`

, `Strict`

, and `CurrentOrOlder`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).`defaultVersion`

value. Valid values are `Reject`

and `Fail`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).**Consumption plan for Python**: 32**Consumption plan for other languages**: 128**Dedicated or Premium plan**: 256*hh:mm:ss*format.*hh:mm:ss*format.`true`

, large messages that exceed the queue size limit are retrieved. When this setting is `false`

, a blob URL that points to each large message is retrieved.**Consumption plan**: 10**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine[durable task scheduler](durable/durable-task-scheduler/durable-task-scheduler). Otherwise, the maximum number of concurrent entity executions is limited to the`maxConcurrentOrchestratorFunctions`

value.*hh:mm:ss*format. Higher values can result in higher message processing latencies. Lower values can result in higher storage costs because of increased storage transactions.connectionStringName (v2.x)

azureStorageConnectionStringName (v1.x)

trackingStoreConnectionStringName

`connectionStringName`

value (v2.x) or `azureStorageConnectionStringName`

value (v1.x) connection is used.`trackingStoreConnectionStringName`

is specified. If you don't specify a prefix, the default value of `DurableTask`

is used. If `trackingStoreConnectionStringName`

isn't specified, the History and Instances tables use the `hubName`

value as their prefix, and the `trackingStoreNamePrefix`

setting is ignored.`true`

, the entire contents of function inputs and outputs are logged.`EventGridTopicEndpoint`

URL.*hh:mm:ss*format.`Started`

, `Completed`

, `Failed`

, and `Terminated`

.`extendedSessionsEnabled`

setting is `true`

.[Disaster recovery and geo-distribution in Durable Functions](durable/durable-functions-disaster-recovery-geo-distribution). This setting is available starting in v2.3.0.`false`

, an algorithm is used that reduces the possibility of duplicate function execution when scaling out. This setting is available starting in v2.3.0. **Setting this value to**.`true`

isn't recommendedIn v2.x: false

`true`

, an algorithm is used that's designed to reduce costs for Azure Storage v2 accounts. This setting is available starting in WebJobs.Extensions.DurableTask v2.10.0. Using this setting with a managed identity requires WebJobs.Extensions.DurableTask v3.x or later, or Worker.Extensions.DurableTask v1.2.x or later.**Consumption plan**: 50**Dedicated or Premium plan**: 5,000[batch](durable/durable-functions-perf-and-scale#entity-operation-batching). If this value is 1, batching is disabled, and a separate function invocation processes each operation message. This setting is available starting in v2.6.1.`true`

, the Durable Task Framework saves activity inputs in the History table, and activity function inputs appear in orchestration history query results.`DurableTaskClient`

uses the gRPC client to manage orchestration instances. This setting applies to Durable Functions .NET isolated worker and Java apps.*hh:mm:ss*format for the HTTP client used by the gRPC client in Durable Functions. The client is currently supported for .NET isolated worker apps (.NET 6 and later versions) and for Java apps.Many of these settings are for optimizing performance. For more information, see [Performance and scale](durable/durable-functions-perf-and-scale).

## eventHub

Configuration settings for [Event Hub triggers and bindings](functions-bindings-event-hubs?tabs=functionsv1#hostjson-settings).

## functions

A list of functions that the job host runs. An empty array means run all functions. Intended for use only when [running locally](functions-run-local). In function apps in Azure, you should instead follow the steps in [How to disable functions in Azure Functions](disable-function) to disable specific functions rather than using this setting.

```
{
"functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```


## functionTimeout

Indicates the timeout duration for all functions. In a serverless Consumption plan, the valid range is from 1 second to 10 minutes, and the default value is 5 minutes. In an App Service plan, there is no overall limit and the default is *null*, which indicates no timeout.

```
{
"functionTimeout": "00:05:00"
}
```


## healthMonitor

Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).

```
{
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
}
}
```


| Property | Default | Description |
|---|---|---|
| enabled | true | Specifies whether the feature is enabled. |
| healthCheckInterval | 10 seconds | The time interval between the periodic background health checks. |
| healthCheckWindow | 2 minutes | A sliding time window used with the `healthCheckThreshold` setting. |
| healthCheckThreshold | 6 | Maximum number of times the health check can fail before a host recycle is initiated. |
| counterThreshold | 0.80 | The threshold at which a performance counter will be considered unhealthy. |

## http

Configuration settings for [http triggers and bindings](functions-bindings-http-webhook).

```
{
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 200,
"maxConcurrentRequests": 100,
"dynamicThrottlesEnabled": true
}
}
```


| Property | Default | Description |
|---|---|---|
| dynamicThrottlesEnabled | false | When enabled, this setting causes the request processing pipeline to periodically check system performance counters like connections/threads/processes/memory/cpu/etc. and if any of those counters are over a built-in high threshold (80%), requests are rejected with a 429 "Too Busy" response until the counter(s) return to normal levels. |
| maxConcurrentRequests | unbounded (`-1` ) |
The maximum number of HTTP functions that will be executed in parallel. This allows you to control concurrency, which can help manage resource utilization. For example, you might have an HTTP function that uses a lot of system resources (memory/cpu/sockets) such that it causes issues when concurrency is too high. Or you might have a function that makes outbound requests to a third party service, and those calls need to be rate limited. In these cases, applying a throttle here can help. |
| maxOutstandingRequests | unbounded (`-1` ) |
The maximum number of outstanding requests that are held at any given time. This limit includes requests that are queued but have not started executing, and any in progress executions. Any incoming requests over this limit are rejected with a 429 "Too Busy" response. That allows callers to employ time-based retry strategies, and also helps you to control maximum request latencies. This only controls queuing that occurs within the script host execution path. Other queues such as the ASP.NET request queue will still be in effect and unaffected by this setting. |
| routePrefix | api | The route prefix that applies to all routes. Use an empty string to remove the default prefix. |

## id

The unique ID for a job host. Can be a lower case GUID with dashes removed. Required when running locally. When running in Azure, we recommend that you not set an ID value. An ID is generated automatically in Azure when `id`

is omitted.

If you share a Storage account across multiple function apps, make sure that each function app has a different `id`

. You can omit the `id`

property or manually set each function app's `id`

to a different value. The timer trigger uses a storage lock to ensure that there will be only one timer instance when a function app scales out to multiple instances. If two function apps share the same `id`

and each uses a timer trigger, only one timer runs.

```
{
"id": "9f4ea53c5136457d883d685e57164f08"
}
```


## logger

Controls filtering for logs written by an [ILogger](functions-dotnet-class-library#ilogger) object or by [context.log](functions-reference-node#contextlog-method).

```
{
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
}
```


| Property | Default | Description |
|---|---|---|
| categoryFilter | n/a | Specifies filtering by category |
| defaultLevel | Information | For any categories not specified in the `categoryLevels` array, send logs at this level and above to Application Insights. |
| categoryLevels | n/a | An array of categories that specifies the minimum log level to send to Application Insights for each category. The category specified here controls all categories that begin with the same value, and longer values take precedence. In the preceding sample host.json file, all categories that begin with "Host.Aggregator" log at `Information` level. All other categories that begin with "Host", such as "Host.Executor", log at `Error` level. |

## queues

Configuration settings for [Storage queue triggers and bindings](functions-bindings-storage-queue).

```
{
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
}
}
```


| Property | Default | Description |
|---|---|---|
| maxPollingInterval | 60000 | The maximum interval in milliseconds between queue polls. |
| visibilityTimeout | 0 | The time interval between retries when processing of a message fails. |
| batchSize | 16 | The number of queue messages that the Functions runtime retrieves simultaneously and processes in parallel. When the number being processed gets down to the `newBatchThreshold` , the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function is `batchSize` plus `newBatchThreshold` . This limit applies separately to each queue-triggered function. If you want to avoid parallel execution for messages received on one queue, you can set `batchSize` to 1. However, this setting eliminates concurrency only so long as your function app runs on a single virtual machine (VM). If the function app scales out to multiple VMs, each VM could run one instance of each queue-triggered function.The maximum `batchSize` is 32. |
| maxDequeueCount | 5 | The number of times to try processing a message before moving it to the poison queue. |
| newBatchThreshold | batchSize/2 | Whenever the number of messages being processed concurrently gets down to this number, the runtime retrieves another batch. |

## SendGrid

Configuration setting for the [SendGrind output binding](functions-bindings-sendgrid)

```
{
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
}
}
```


| Property | Default | Description |
|---|---|---|
| from | n/a | The sender's email address across all functions. |

## serviceBus

Configuration setting for [Service Bus triggers and bindings](functions-bindings-service-bus).

```
{
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
}
}
```


| Property | Default | Description |
|---|---|---|
| maxConcurrentCalls | 16 | The maximum number of concurrent calls to the callback that the message pump should initiate. By default, the Functions runtime processes multiple messages concurrently. To direct the runtime to process only a single queue or topic message at a time, set `maxConcurrentCalls` to 1. |
| prefetchCount | n/a | The default PrefetchCount that will be used by the underlying ServiceBusReceiver. |
| autoRenewTimeout | 00:05:00 | The maximum duration within which the message lock will be renewed automatically. |
| autoComplete | true | When true, the trigger completes the message processing automatically on successful execution of the operation. When false, it is the responsibility of the function to complete the message before returning. |

## singleton

Configuration settings for Singleton lock behavior. For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```
{
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
}
}
```


| Property | Default | Description |
|---|---|---|
| lockPeriod | 00:00:15 | The period that function level locks are taken for. The locks auto-renew. |
| listenerLockPeriod | 00:01:00 | The period that listener locks are taken for. |
| listenerLockRecoveryPollingInterval | 00:01:00 | The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup. |
| lockAcquisitionTimeout | 00:01:00 | The maximum amount of time the runtime tries to acquire a lock. |
| lockAcquisitionPollingInterval | n/a | The interval between lock acquisition attempts. |

## tracing

*Version 1.x*

Configuration settings for logs that you create by using a `TraceWriter`

object. To learn more, see [C# Logging].

```
{
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
}
}
```


| Property | Default | Description |
|---|---|---|
| consoleLevel | info | The tracing level for console logging. Options are: `off` , `error` , `warning` , `info` , and `verbose` . |
| fileLoggingMode | debugOnly | The tracing level for file logging. Options are `never` , `always` , `debugOnly` . |

## watchDirectories

A set of [shared code directories](functions-reference-csharp#watched-directories) that should be monitored for changes. Ensures that when code in these directories is changed, the changes are picked up by your functions.

```
{
"watchDirectories": [ "Shared" ]
}
```
