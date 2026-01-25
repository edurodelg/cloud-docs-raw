---
merged_at: 2026-01-25T15:41:11.642596
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-create-vnet_functions-bindings-storage-table-output.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-create-vnet.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-vnet -->

# Tutorial: Integrate Azure Functions with an Azure virtual network by using private endpoints

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to use Azure Functions to connect to resources in an Azure virtual network by using private endpoints. You create a new function app using a new storage account that's locked behind a virtual network by using the Azure portal. The virtual network uses a Service Bus queue trigger.

In this tutorial, you'll:

- Create a function app in the Elastic Premium plan with virtual network integration and private endpoints.
- Create Azure resources, such as the Service Bus
- Lock down your Service Bus behind a private endpoint.
- Deploy a function app that uses both the Service Bus and HTTP triggers.
- Test to see that your function app is secure inside the virtual network.
- Clean up resources.

## Create a function app in a Premium plan

You create a C# function app in an [Elastic Premium plan](functions-premium-plan), which supports networking capabilities such as virtual network integration on create along with serverless scale. This tutorial uses C# and Windows. Other languages and Linux are also supported.

On the Azure portal menu or the

**Home**page, select**Create a resource**.On the

**New**page, select**Compute**>**Function App**.On the

**Basics**page, use the following table to configure the function app settings.Setting Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Publish**Code Choose to publish code files or a Docker container. **Runtime stack**.NET This tutorial uses .NET. **Version**6 (LTS) This tutorial uses .NET 6.0 running [in the same process as the Functions host](functions-dotnet-class-library).**Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Operating system**Windows This tutorial uses Windows but also works for Linux. [Plan](functions-scale)Functions Premium Hosting plan that defines how resources are allocated to your function app. By default, when you select **Premium**, a new App Service plan is created. The default**Sku and size**is**EP1**, where*EP*stands for*elastic premium*. For more information, see the list of[Premium SKUs](functions-premium-plan#available-instance-skus).

When you run JavaScript functions on a Premium plan, choose an instance that has fewer vCPUs. For more information, see[Choose single-core Premium plans](functions-reference-node#considerations-for-javascript-functions).Select

**Next: Storage**. On the**Storage**page, enter the following settings.Setting Suggested value Description [Storage account](../storage/common/storage-account-create)Globally unique name Create a storage account used by your function app. Storage account names must be between 3 and 24 characters long. They might contain numbers and lowercase letters only. You can also use an existing account that isn't restricted by firewall rules and meets the [storage account requirements](storage-considerations#storage-account-requirements). When you use Functions with a locked down storage account, you need a v2 storage account. This version is the default storage version created when creating a function app with networking capabilities through the Azure portal.Select

**Next: Networking**. On the**Networking**page, enter the following settings.Note

Some of these settings aren't visible until other options are selected.

Setting Suggested value Description **Enable public access**Off Deny public network access blocks all incoming traffic except that comes from private endpoints. **Enable network injection**On The ability to configure your application with virtual network integration at creation appears in the portal window after this option is switched to **On**.**Virtual Network**Create New Select the **Create New**field. In the pop-out screen, provide a name for your virtual network and select**Ok**. Options to restrict inbound and outbound access to your function app on create are displayed. You must explicitly enable virtual network integration in the**Outbound access**portion of the window to restrict outbound access.Enter the following settings for the

**Inbound access**section. This step creates a private endpoint on your function app.Tip

To continue interacting with your function app from the Azure portal, you need to add your local computer to the virtual network. If you don't wish to restrict inbound access, skip this step.

Setting Suggested value Description **Enable private endpoints**On The ability to configure your application with virtual network integration at creation appears in the portal after this option is enabled. **Private endpoint name**myInboundPrivateEndpointName Name that identifies your new function app private endpoint. **Inbound subnet**Create New This option creates a new subnet for your inbound private endpoint. Multiple private endpoints might be added to a singular subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**. To learn more about subnet sizing, see[Subnets](functions-networking-options#subnets).**DNS**Azure Private DNS Zone This value indicates which DNS server your private endpoint uses. In most cases if you're working within Azure, Azure Private DNS Zone is the DNS zone you should use as using **Manual**for custom DNS zones have increased complexity.Enter the following settings for the

**Outbound access**section. This step integrates your function app with a virtual network on creation. It also exposes options to create private endpoints on your storage account and restrict your storage account from network access on create. When function app is virtual network integrated, all outbound traffic by default goes[through the virtual network](../app-service/overview-vnet-integration#how-regional-virtual-network-integration-works).Setting Suggested value Description **Enable VNet Integration**On This setting integrates your function app with a virtual network on create and direct all outbound traffic through the virtual network. **Outbound subnet**Create new This setting creates a new subnet for your function app's virtual network integration. A function app can only be virtual network integrated with an empty subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**. The option to create**Storage private endpoints**is displayed. To use your function app with virtual networks, you need to join it to a subnet.Enter the following settings for the

**Storage private endpoint**section. This step creates private endpoints for the blob, queue, file, and table endpoints on your storage account on create. This approach effectively integrates your storage account with the virtual network.Setting Suggested value Description **Add storage private endpoint**On The ability to configure your application with virtual network integration at creation is displayed in the portal after this option is enabled. **Private endpoint name**myInboundPrivateEndpointName Name that identifies your storage account private endpoint. **Private endpoint subnet**Create New This setting creates a new subnet for your inbound private endpoint on the storage account. Multiple private endpoints might be added to a singular subnet. Provide a **Subnet Name**. The**Subnet Address Block**might be left at the default value. Select**Ok**.**DNS**Azure Private DNS Zone This value indicates which DNS server your private endpoint uses. In most cases if you're working within Azure, Azure Private DNS Zone is the DNS zone you should use as using **Manual**for custom DNS zones will have increased complexity.Select

**Next: Monitoring**. On the**Monitoring**page, enter the following settings.Setting Suggested value Description [Application Insights](functions-monitoring)Default Create an Application Insights resource of the same app name in the nearest supported region. Expand this setting if you need to change the **New resource name**or store your data in a different**Location**in an[Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/).Select

**Review + create**to review the app configuration selections.On the

**Review + create**page, review your settings. Then select**Create**to create and deploy the function app.In the upper-right corner of the portal, select the

**Notifications**icon and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

Congratulations! You successfully created your premium function app.

Note

Some deployments might occasionally fail to create the private endpoints in the storage account with the error `StorageAccountOperationInProgress`

. This failure occurs even though the function app itself gets created successfully. When you encounter such an error, delete the function app and retry the operation. You can instead create the private endpoints on the storage account manually.

### Create a Service Bus

Next, you create a Service Bus instance that is used to test the functionality of your function app's network capabilities in this tutorial.

On the Azure portal menu or the

**Home**page, select**Create a resource**.On the

**New**page, search for*Service Bus*. Then select**Create**.On the

**Basics**tab, use the following table to configure the Service Bus settings. All other settings can use the default values.Setting Suggested value Description **Subscription**Your subscription The subscription in which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Namespace name**myServiceBus The name of the Service Bus instance for which the private endpoint is enabled. [Location](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your function app. **Pricing tier**Premium Choose this tier to use private endpoints with Azure Service Bus. Select

**Review + create**. After validation finishes, select**Create**.

## Lock down your Service Bus

Create the private endpoint to lock down your Service Bus:

In your new Service Bus, in the menu on the left, select

**Networking**.On the

**Private endpoint connections**tab, select**Private endpoint**.On the

**Basics**tab, use the private endpoint settings shown in the following table.Setting Suggested value Description **Subscription**Your subscription The subscription in which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Name**sb-endpoint The name of the private endpoint for the service bus. [Region](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your storage account. On the

**Resource**tab, use the private endpoint settings shown in the following table.Setting Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. **Resource type**Microsoft.ServiceBus/namespaces The resource type for the Service Bus. **Resource**myServiceBus The Service Bus you created earlier in the tutorial. **Target subresource**namespace The private endpoint that is used for the namespace from the Service Bus. On the

**Virtual Network**tab, for the**Subnet**setting, choose**default**.Select

**Review + create**. After validation finishes, select**Create**.After the private endpoint is created, return to the

**Networking**section of your Service Bus namespace and check the**Public Access**tab.Ensure

**Selected networks**is selected.Select

**+ Add existing virtual network**to add the recently created virtual network.On the

**Add networks**tab, use the network settings from the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. **Virtual networks**myVirtualNet The name of the virtual network to which your function app connects. **Subnets**functions The name of the subnet to which your function app connects. Select

**Add your client IP address**to give your current client IP access to the namespace.Note

Allowing your client IP address is necessary to enable the Azure portal to

[publish messages to the queue later in this tutorial](#test-your-locked-down-function-app).Select

**Enable**to enable the service endpoint.Select

**Add**to add the selected virtual network and subnet to the firewall rules for the Service Bus.Select

**Save**to save the updated firewall rules.

Resources in the virtual network can now communicate with the Service Bus using the private endpoint.

## Create a queue

Create the queue where your Azure Functions Service Bus trigger gets events:

In your Service Bus, in the menu on the left, select

**Queues**.Select

**Queue**. For the purposes of this tutorial, provide the name*queue*as the name of the new queue.Select

**Create**.

Important

This tutorial currently shows you how to connect to Service Bus using a connection string, which requires you to handle a share secret. For improved security, you should instead use managed identities when connecting to Service Bus from your app. For more information, see [Identity-based connections](functions-bindings-service-bus-trigger?tabs=extensionv5#identity-based-connections) in the Service Bus binding reference article.

## Get a Service Bus connection string

In your Service Bus, in the menu on the left, select

**Shared access policies**.Select

**RootManageSharedAccessKey**. Copy and save the**Primary Connection String**. You need this connection string when you configure the app settings.

## Configure your function app settings

In your function app, in the menu on the left, select

**Configuration**.To use your function app with virtual networks and service bus, update the app settings shown in the following table. To add or edit a setting, select

**+ New application setting**or the**Edit**icon in the rightmost column of the app settings table. When you finish, select**Save**.Setting Suggested value Description **SERVICEBUS_CONNECTION**myServiceBusConnectionString Create this app setting for the connection string of your Service Bus. This storage connection string is from the [Get a Service Bus connection string](#get-a-service-bus-connection-string)section.**WEBSITE_CONTENTOVERVNET**1 Create this app setting. A value of 1 enables your function app to scale when your storage account is restricted to a virtual network. Since you're using an Elastic Premium hosting plan, In the

**Configuration**view, select the**Function runtime settings**tab. Set**Runtime Scale Monitoring**to**On**. Then select**Save**. Runtime-driven scaling allows you to connect non-HTTP trigger functions to services that run inside your virtual network.

Note

Runtime scaling isn't needed for function apps hosted in a Dedicated App Service plan.

## Deploy a Service Bus trigger and HTTP trigger

Note

Enabling private endpoints on a function app also makes the Source Control Manager (SCM) site publicly inaccessible. The following instructions give deployment directions using the Deployment Center within the function app. Alternatively, use [zip deploy](functions-deployment-technologies#zip-deploy) or [self-hosted](/en-us/azure/devops/pipelines/agents/docker) agents that are deployed into a subnet on the virtual network.

In GitHub, go to the following sample repository. It contains a function app and two functions, an HTTP trigger, and a Service Bus queue trigger.

At the top of the page, select

**Fork**to create a fork of this repository in your own GitHub account or organization.In your function app, in the menu on the left, select

**Deployment Center**. Then select**Settings**.On the

**Settings**tab, use the deployment settings shown in the following table.Setting Suggested value Description **Source**GitHub You should have created a GitHub repository for the sample code in step 2. **Organization**myOrganization The organization your repo is checked into. It's usually your account. **Repository**functions-vnet-tutorial The repository forked from [https://github.com/Azure-Samples/functions-vnet-tutorial](https://github.com/Azure-Samples/functions-vnet-tutorial).**Branch**main The main branch of the repository you created. **Runtime stack**.NET The sample code is in C#. **Version**.NET Core 3.1 The runtime version. Select

**Save**.Your initial deployment might take a few minutes. When your app is successfully deployed, on the

**Logs**tab, you see a**Success (Active)**status message. If necessary, refresh the page.

Congratulations! You successfully deployed your sample function app.

### Test your locked-down function app

In your function app, in the menu on the left, select

**Functions**.Select

**ServiceBusQueueTrigger**.In the menu on the left, select

**Monitor**.

You see that you can't monitor your app. Your browser doesn't have access to the virtual network, so it can't directly access resources within the virtual network.

Here's an alternative way to monitor your function by using Application Insights:

In your function app, in the menu on the left, select

**Application Insights**. Then select**View Application Insights data**.In the menu on the left, select

**Live metrics**.Open a new tab. In your Service Bus, in the menu on the left, select

**Queues**.Select your queue.

In the menu on the left, select

**Service Bus Explorer**. Under**Send**, for**Content Type**, choose**Text/Plain**. Then enter a message.Select

**Send**to send the message.On the

**Live metrics**tab, you should see that your Service Bus queue trigger fired. If it hasn't, resend the message from**Service Bus Explorer**.

Congratulations! You successfully tested your function app setup with private endpoints.

## Understand private DNS zones

You used a private endpoint to connect to Azure resources. You're connecting to a private IP address instead of the public endpoint. Existing Azure services are configured to use an existing DNS to connect to the public endpoint. You must override the DNS configuration to connect to the private endpoint.

A private DNS zone is created for each Azure resource that was configured with a private endpoint. A DNS record is created for each private IP address associated with the private endpoint.

The following DNS zones were created in this tutorial:

- privatelink.file.core.windows.net
- privatelink.blob.core.windows.net
- privatelink.servicebus.windows.net
- privatelink.azurewebsites.net

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Next steps

In this tutorial, you created a Premium function app, storage account, and Service Bus. You secured all of these resources behind private endpoints.

Use the following links to learn more Azure Functions networking options and private endpoints:


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-storage-table-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table-output -->

# Azure Tables output bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use an Azure Tables output binding to write entities to a table in [Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table/introduction) or [Azure Table Storage](../storage/tables/table-storage-overview).

For information on setup and configuration details, see the [overview](functions-bindings-storage-table)

Note

This output binding only supports creating new entities in a table. If you need to update an existing entity from your function code, instead use an Azure Tables SDK directly.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

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


The following function, which is started by a Queue Storage trigger, writes a new `MyDataTable`

entity to a table named **OutputTable**.

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


The following example shows a Java function that uses an HTTP trigger to write a single table row.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPerson {
@FunctionName("addPerson")
public HttpResponseMessage get(
@HttpTrigger(name = "postPerson", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/{partitionKey}/{rowKey}") HttpRequestMessage<Optional<Person>> request,
@BindingName("partitionKey") String partitionKey,
@BindingName("rowKey") String rowKey,
@TableOutput(name="person", partitionKey="{partitionKey}", rowKey = "{rowKey}", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person> person,
final ExecutionContext context) {
Person outPerson = new Person();
outPerson.setPartitionKey(partitionKey);
outPerson.setRowKey(rowKey);
outPerson.setName(request.getBody().get().getName());
person.setValue(outPerson);
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(outPerson)
.build();
}
}
```


The following example shows a Java function that uses an HTTP trigger to write multiple table rows.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPersons {
@FunctionName("addPersons")
public HttpResponseMessage get(
@HttpTrigger(name = "postPersons", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/") HttpRequestMessage<Optional<Person[]>> request,
@TableOutput(name="person", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person[]> persons,
final ExecutionContext context) {
persons.setValue(request.getBody().get());
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(request.getBody().get())
.build();
}
}
```


The following example shows a table output binding that writes multiple table entities.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
interface PersonEntity {
PartitionKey: string;
RowKey: string;
Name: string;
}
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const rows: PersonEntity[] = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
}
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: httpTrigger1,
});
```


```
const { app, output } = require('@azure/functions');
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: async (request, context) => {
const rows = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
},
});
```


The following example demonstrates how to write multiple entities to a table from a function.

Binding configuration in *function.json*:

```
{
"bindings": [
{
"name": "InputData",
"type": "manualTrigger",
"direction": "in"
},
{
"tableName": "Person",
"connection": "MyStorageConnectionAppSetting",
"name": "TableBinding",
"type": "table",
"direction": "out"
}
],
"disabled": false
}
```


PowerShell code in *run.ps1*:

```
param($InputData, $TriggerMetadata)
foreach ($i in 1..10) {
Push-OutputBinding -Name TableBinding -Value @{
PartitionKey = 'Test'
RowKey = "$i"
Name = "Name $i"
}
}
```


The following example demonstrates how to use the Table storage output binding. Configure the `table`

binding in the *function.json* by assigning values to `name`

, `tableName`

, `partitionKey`

, and `connection`

:

The following function generates a unique UUI for the `rowKey`

value and persists the message into Table storage.

```
import logging
import uuid
import json
import azure.functions as func
app = func.FunctionApp()
@app.route(route="table_out_binding")
@app.table_output(arg_name="message",
connection="AzureWebJobsStorage",
table_name="messages")
def table_out_binding(req: func.HttpRequest, message: func.Out[str]):
row_key = str(uuid.uuid4())
data = {
"Name": "Output binding message",
"PartitionKey": "message",
"RowKey": row_key
}
table_json = json.dumps(data)
message.set(table_json)
return table_json
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#table-output).

In [C# class libraries](dotnet-isolated-process-guide), the `TableInputAttribute`

supports the following properties:

| Attribute property | Description |
|---|---|
TableName |
The name of the table to which to write. |
PartitionKey |
The partition key of the table entity to write. |
RowKey |
The row key of the table entity to write. |
Connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [TableOutput](https://github.com/Azure/azure-functions-java-library/blob/master/src/main/java/com/microsoft/azure/functions/annotation/TableOutput.java/) annotation on parameters to write values into your tables. The attribute supports the following elements:

| Element | Description |
|---|---|
name |
The variable name used in function code that represents the table or entity. |
dataType |
Defines how Functions runtime should treat the parameter value. To learn more, see
|

**tableName****partitionKey****rowKey****connection**[Connections](#connections).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.table()`

method.

| Property | Description |
|---|---|
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
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
Must be set to `out` . This property is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the table or entity. Set to `$return` to reference the function return value. |
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
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

When you want the function to write to a single entity, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements [ITableEntity] | Functions attempts to serialize a plain-old CLR object (POCO) type as the entity. The type must implement [ITableEntity] or have a string `RowKey` property and a string `PartitionKey` property. |

When you want the function to write to multiple entities, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single entity types |
An array containing multiple entities. Each entry represents one entity. |

For other output scenarios, create and use a [TableClient](/en-us/dotnet/api/azure.data.tables.tableclient) with other types from [Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

There are two options for outputting a Table storage row from a function by using the [TableStorageOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.tableoutput) annotation:

| Options | Description |
|---|---|
Return value |
By applying the annotation to the function itself, the return value of the function persists as a Table storage row. |
Imperative |
To explicitly set the table row, apply the annotation to a specific parameter of the type
`OutputBinding<T>` |

`T`

includes the `PartitionKey`

and `RowKey`

properties. You can accompany these properties by implementing `ITableEntity`

or inheriting `TableEntity`

.To write to table data, use the `Push-OutputBinding`

cmdlet, set the `-Name TableBinding`

parameter and `-Value`

parameter equal to the row data. See the [PowerShell example](#example) for more detail.

There are two options for outputting a Table storage row message from a function:

| Options | Description |
|---|---|
Return value |
Set the `name` property in function.json to `$return` . With this configuration, the function's return value persists as a Table storage row. |
Imperative |
Pass a value to the
`set` is persisted as table row. |

For specific usage details, see [Example](#example).

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Table |
|


---

<!-- DOCUMENTO FUSIONADO: functions-networking-options.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-networking-options -->

# Azure Functions networking options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes the networking features available across the hosting options for Azure Functions. The following networking options can be categorized as inbound and outbound networking features. Inbound features allow you to restrict access to your app, whereas outbound features allow you to connect your app to resources secured by a virtual network and control how outbound traffic is routed.

The [hosting models](functions-scale) have different levels of network isolation available. Choosing the correct one helps you meet your network isolation requirements.

| Feature |
|
|---|

[Consumption plan](consumption-plan)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)/

[ASE](../app-service/environment/intro)

[Container Apps](../container-apps/functions-overview)

1

[Inbound IP restrictions](functions-networking-options#inbound-networking-features)[Inbound Private Endpoints](functions-networking-options#inbound-networking-features)[Virtual network integration](functions-networking-options#virtual-network-integration)23[Outbound IP restrictions](functions-networking-options#outbound-ip-restrictions)- For more information, see
[Networking in Azure Container Apps environment](../container-apps/networking). - There are special considerations when working with
[virtual network triggers](functions-networking-options#virtual-network-triggers-non-http). - Only the Dedicated/ASE plan supports gateway-required virtual network integration.

## Quickstart resources

Use the following resources to quickly get started with Azure Functions networking scenarios. These resources are referenced throughout the article.

- ARM templates, Bicep files, and Terraform templates:
- ARM templates only:
- Tutorials:

## Inbound networking features

The following features let you filter inbound requests to your function app.

### Inbound access restrictions

You can use access restrictions to define a priority-ordered list of IP addresses that are allowed or denied access to your app. The list can include IPv4 and IPv6 addresses, or specific virtual network subnets using [service endpoints](#use-service-endpoints). When there are one or more entries, an implicit "deny all" exists at the end of the list. IP restrictions work with all function-hosting options.

Access restrictions are available in the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium](functions-premium-plan), [Consumption](consumption-plan), and [App Service](dedicated-plan).

Note

With network restrictions in place, you can deploy only from within your virtual network, or when you put the IP address of the machine you're using to access the Azure portal on the **Safe Recipients** list. However, you can still manage the function using the portal.

To learn more, see [Azure App Service static access restrictions](../app-service/app-service-ip-restrictions).

### Private endpoints

[Azure Private Endpoint](../private-link/private-endpoint-overview) is a network interface that connects you privately and securely to a service powered by Azure Private Link. Private Endpoint uses a private IP address from your virtual network, effectively bringing the service into your virtual network.

You can use Private Endpoint for your functions hosted in the [Flex Consumption](flex-consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) plans.

If you want to make calls to Private Endpoints, then you must make sure that your DNS lookups resolve to the private endpoint. You can enforce this behavior in one of the following ways:

- Integrate with Azure DNS private zones. When your virtual network doesn't have a custom DNS server, this is done automatically.
- Manage the private endpoint in the DNS server used by your app. To manage a private endpoint, you must know the endpoint address and use an A record to reference the endpoint you're trying to reach.
- Configure your own DNS server to forward to
[Azure DNS private zones](../dns/private-dns-privatednszone).

To learn more, see [using Private Endpoints for Web Apps](../app-service/networking/private-endpoint).

To call other services that have a private endpoint connection, such as storage or service bus, be sure to configure your app to make [outbound calls to private endpoints](#private-endpoints). For more details on using private endpoints with the storage account for your function app, visit [restrict your storage account to a virtual network](#restrict-your-storage-account-to-a-virtual-network).

### Service endpoints

Using service endpoints, you can restrict many Azure services to selected virtual network subnets to provide a higher level of security. Regional virtual network integration enables your function app to reach Azure services that are secured with service endpoints. This configuration is supported on all [plans](functions-scale#networking-features) that support virtual network integration. Follow these steps to access a secured service endpoint:

- Configure regional virtual network integration with your function app to connect to a specific subnet.
- Go to the destination service and configure service endpoints against the integration subnet.

To learn more, see [Virtual network service endpoints](../virtual-network/virtual-network-service-endpoints-overview).

#### Use Service Endpoints

To restrict access to a specific subnet, create a restriction rule with a **Virtual Network** type. You can then select the subscription, virtual network, and subnet that you want to allow or deny access to.

If service endpoints aren't already enabled with `Microsoft.Web`

for the subnet that you selected, they're automatically enabled unless you select the **Ignore missing Microsoft.Web service endpoints** check box. The scenario where you might want to enable service endpoints on the app but not the subnet depends mainly on whether you have the permissions to enable them on the subnet.

If you need someone else to enable service endpoints on the subnet, select the **Ignore missing Microsoft.Web service endpoints** check box. Your app is configured for service endpoints, which you enable later on the subnet.

You can't use service endpoints to restrict access to apps that run in an App Service Environment. When your app is in an App Service Environment, you can control access to it by applying IP access rules.

To learn how to set up service endpoints, see [Establish Azure Functions private site access](functions-create-private-site-access).

## Outbound networking features

You can use the features in this section to manage outbound connections made by your app.

### Virtual network integration

This section details the features that Functions supports to control data outbound from your app.

Virtual network integration gives your function app access to resources in your virtual network. Once integrated, your app routes outbound traffic through the virtual network. This allows your app to access private endpoints or resources with rules allowing traffic from only select subnets. When the destination is an IP address outside of the virtual network, the source IP will still be sent from the one of the addresses listed in your app's properties, unless you've configured a NAT Gateway.

Azure Functions supports two kinds of virtual network integration:

[Regional virtual network integration](#regional-virtual-network-integration)for apps running on the[Flex Consumption](flex-consumption-plan),[Elastic Premium](functions-premium-plan),[Dedicated (App Service)](dedicated-plan), and[Container Apps](functions-container-apps-hosting)hosting plans (recommended)[Gateway-required virtual network integration](../app-service/configure-gateway-required-vnet-integration)for apps running on the[Dedicated (App Service)](dedicated-plan)hosting plan

To learn how to set up virtual network integration, see [Enable virtual network integration](#enable-virtual-network-integration).

### Regional virtual network integration

Using regional virtual network integration enables your app to access:

- Resources in the same virtual network as your app.
- Resources in virtual networks peered to the virtual network your app is integrated with.
- Service endpoint secured services.
- Resources across Azure ExpressRoute connections.
- Resources across peered connections, which include Azure ExpressRoute connections.
- Private endpoints

When you use regional virtual network integration, you can use the following Azure networking features:

: You can block outbound traffic with an NSG that's placed on your integration subnet. The inbound rules don't apply because you can't use virtual network integration to provide inbound access to your app.[Network security groups (NSGs)](#network-security-groups): You can place a route table on the integration subnet to send outbound traffic where you want.[Route tables (UDRs)](#routes)

Note

When you route all of your outbound traffic into your virtual network, it's subject to the NSGs and UDRs that are applied to your integration subnet. When virtual network integrated, your function app's outbound traffic to public IP addresses is still sent from the addresses that are listed in your app properties, unless you provide routes that direct the traffic elsewhere.

Regional virtual network integration isn't able to use port 25.

Considerations for the [Flex Consumption](flex-consumption-plan) plan:

- The app and the virtual network must be in the same region.
- Ensure that the
`Microsoft.App`

Azure resource provider is enabled for your subscription by[following these instructions](../azure-resource-manager/management/resource-providers-and-types#register-resource-provider). This is needed for subnet delegation. The Azure portal and Azure CLI enforce this registration when you create a Flex Consumption app, since virtual network integration can be enabled at any point after your app is created. - The subnet delegation required when running in a Flex Consumption plan is
`Microsoft.App/environments`

. This differs from the Elastic Premium and Dedicated (App Service) plans, which have a different delegation requirement. - You can plan for 40 IP addresses to be used at the most for one function app, even if the app scales beyond 40. For example, if you have 15 Flex Consumption function apps that are integrated in the same subnet, you must plan for 15x40 = 600 IP addresses used at the most. This limit is subject to change, and isn't enforced.
- The subnet can't already be in use for other purposes (like private or service endpoints, or
[delegated](../virtual-network/subnet-delegation-overview)to any other hosting plan or service). While you can share the same subnet with multiple Flex Consumption apps, the networking resources are shared across these function apps, which can lead to one app impacting the performance of others on the same subnet. - You can't share the same subnet between a Container Apps environment and a Flex Consumption app.
- The Flex Consumption plan currently doesn't support subnets with names that contain underscore (
`_`

) characters.

Considerations for the [Elastic Premium](functions-premium-plan), [Dedicated (App Service)](dedicated-plan), and [Container Apps](functions-container-apps-hosting) plans:

- The feature is available for Elastic Premium and App Service Premium V2 and Premium V3. It's also available in Standard but only from newer App Service deployments. If you are on an older deployment, you can only use the feature from a Premium V2 App Service plan. If you want to make sure you can use the feature in a Standard App Service plan, create your app in a Premium V3 App Service plan. Those plans are only supported on our newest deployments. You can scale down if you desire after that.
- The feature can't be used by Isolated plan apps that are in an App Service Environment.
- The app and the virtual network must be in the same region.
- The feature requires an unused subnet that's a /28 or larger in an Azure Resource Manager virtual network.
- The integration subnet can be used by only one App Service plan.
- You can have up to two regional virtual network integrations per App Service plan. Multiple apps in the same App Service plan can use the same integration subnet.
- The subnet can't already be in use for other purposes (like private or service endpoints, or
[delegated](../virtual-network/subnet-delegation-overview)to the Flex Consumption plan or any other service). While you can share the same subnet with multiple apps in the same App Service plan, the networking resources are shared across these function apps, which can lead to one app impacting the performance of others on the same subnet. - You can't delete a virtual network with an integrated app. Remove the integration before you delete the virtual network.
- You can't change the subscription of an app or a plan while there's an app that's using regional virtual network integration.

### Enable virtual network integration

In your function app in the

[Azure portal](https://portal.azure.com), select**Networking**, then under**VNet Integration**select**Click here to configure**.Select

**Add VNet**.The drop-down list contains all of the Azure Resource Manager virtual networks in your subscription in the same region. Select the virtual network you want to integrate with.

The Flex Consumption and Elastic Premium hosting plans only support regional virtual network integration. If the virtual network is in the same region, either create a new subnet or select an empty, pre-existing subnet.

To select a virtual network in another region, you must have a virtual network gateway provisioned with point to site enabled. Virtual network integration across regions is only supported for Dedicated plans, but global peerings work with regional virtual network integration.


During the integration, your app is restarted. When integration is finished, you see details on the virtual network you're integrated with. By default, Route All is enabled, and all traffic is routed into your virtual network.

If you prefer to only have your private traffic ([RFC1918](https://datatracker.ietf.org/doc/html/rfc1918#section-3) traffic) routed, follow the steps in this [App Service article](../app-service/overview-vnet-integration#application-routing).

### Subnets

Virtual network integration depends on a dedicated subnet. When you provision a subnet, Azure reserves the first five IP addresses for internal use. The way remaining IP addresses are consumed depends on your hosting plan. Since subnet size can't be changed after assignment, use a subnet that's large enough to accommodate whatever scale your app might reach.

#### Elastic Premium and Dedicated Plans

In Elastic Premium and Dedicated (App Service) plans, each running instance of your function app consumes one IP address from the subnet. When you scale up or down, the required address space may temporarily double to accommodate the transition. If multiple apps share the same subnet, the total IP address usage is the sum of all instances across those apps, plus the temporary doubling during scaling events.

**IP Consumption Scenarios**

| Scenario | IP Address Consumption |
|---|---|
| 1 app, 1 instance | 1 IP address |
| 1 app, 5 instances | 5 IP addresses |
| 1 app, scaling from 5 to 10 instances | Up to 20 IP addresses (temporary, during scale operation) |
| 3 apps, 5 instances each | 15 IP addresses |

**CIDR Range Recommendations**

| CIDR block size | Max available addresses | Max horizontal scale (instances)1 |
|---|---|---|
| /28 | 11 | 5 |
| /27 | 27 | 13 |
| /26 | 59 | 29 |
| /25 | 123 | 612 |
| /24 | 251 | 1253 |

1Assumes that you need to scale up or down in either size or SKU at some point.

2 Although the number of IP addresses supports 61 instances, individual apps on the Dedicated plan have a [30 instance maximum](functions-scale#scale).

2 Although the number of IP addresses supports 125 instances, individual apps on the Elastic Premium plan have a [100 instance maximum](functions-scale#scale).

**Additional Considerations**

For function apps on the Elastic Premium or Dedicated plans:

- To avoid any issues with subnet capacity for Functions Elastic Premium plans, you should use a /24 with 256 addresses for Windows and a /26 with 64 addresses for Linux. When creating subnets in Azure portal as part of integrating with the virtual network, a minimum size of /24 and /26 is required for Windows and Linux respectively.
- Each App Service plan can support up to two subnets that can be used for VNet integration. Multiple apps from a single App Service plan can join the same subnet, but apps from a different plan can't use that same subnet.

#### Flex Consumption Plan

In the Flex Consumption plan, outbound network traffic from function app instances are routed through shared gateways that are dedicated to the subnet. Each shared gateway consumes 1 IP address from the subnet. Regardless of how many apps are integrated with a single subnet, at most 27 shared gateways (27 IP addresses) will be used to support all instances. When selecting a subnet size, what matters is the total number of instances across all apps integrated with the subnet. When a subnet is used for too many instances or for apps performing I/O intensive workloads, network capacity issues may occur such as increased average latency and timeouts. The scale-out of apps will not be affected.

A /27 subnet size (27 usable IP addresses) is recommended to support a single function app, which can scale-out to a maximum of 1,000 instances.

If you expect your single function app to scale beyond 1,000 instances or expect the total instance count of multiple function apps to exceed 1,000 instances, then use a /26 subnet and contact the product group to request an increase to your maximum instance count.

Important

Integrating Flex Consumption function apps with a subnet size less than /27 or integrating multiple apps with a /27 size subnet reduces the available outbound network capacity for them. If you plan to do so, load test your apps with production-scale workloads to ensure network capacity constraints are not observed.

**IP Consumption Scenarios**

| Scenario | Maximum IP Address Consumption |
|---|---|
| 1 app | Up to 27 IP addresses (/27 subnet size) |
| 2 apps | Up to 27 IP addresses (/27 subnet size) |
| 10 apps | Up to 27 IP addresses (/27 subnet size) |

### Network security groups

You can use [network security groups](../virtual-network/network-security-groups-overview) to control traffic between resources in your virtual network. For example, you can create a security rule that blocks your app's outbound traffic from reaching a resource in your virtual network or from leaving the network. These security rules apply to apps that have configured virtual network integration. To block traffic to public addresses, you must have virtual network integration and Route All enabled. The inbound rules in an NSG don't apply to your app because virtual network integration affects only outbound traffic from your app.

To control inbound traffic to your app, use the Access Restrictions feature. An NSG that's applied to your integration subnet is in effect regardless of any routes applied to your integration subnet. If your function app is virtual network integrated with [Route All](../app-service/configure-vnet-integration-routing#configure-application-routing) enabled, and you don't have any routes that affect public address traffic on your integration subnet, all of your outbound traffic is still subject to NSGs assigned to your integration subnet. When Route All isn't enabled, NSGs are only applied to RFC1918 traffic.

### Routes

You can use route tables to route outbound traffic from your app to wherever you want. By default, route tables only affect your RFC1918 destination traffic. When [Route All](../app-service/overview-vnet-integration#application-routing) is enabled, all of your outbound calls are affected. When Route All is disabled, only private traffic (RFC1918) is affected by your route tables. Routes that are set on your integration subnet won't affect replies to inbound app requests. Common destinations can include firewall devices or gateways.

If you want to route all outbound traffic on-premises, you can use a route table to send all outbound traffic to your ExpressRoute gateway. If you do route traffic to a gateway, be sure to set routes in the external network to send any replies back.

Border Gateway Protocol (BGP) routes also affect your app traffic. If you have BGP routes from something like an ExpressRoute gateway, your app outbound traffic is affected. By default, BGP routes affect only your RFC1918 destination traffic. When your function app is virtual network integrated with **Route All** enabled, all outbound traffic can be affected by your BGP routes.

### Outbound IP restrictions

Outbound IP restrictions are available in a Flex Consumption plan, Elastic Premium plan, App Service plan, or App Service Environment. You can configure outbound restrictions for the virtual network where your App Service Environment is deployed.

When you integrate a function app in an Elastic Premium plan or an App Service plan with a virtual network, the app can still make outbound calls to the internet by default. By integrating your function app with a virtual network with Route All enabled, you force all outbound traffic to be sent into your virtual network, where network security group rules can be used to restrict traffic. For Flex Consumption all traffic is already routed through the virtual network and **Route All** isn't needed.

To learn how to control the outbound IP using a virtual network, see [Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway](functions-how-to-use-nat-gateway).

### Azure DNS private zones

After your app integrates with your virtual network, it uses the same DNS server that your virtual network is configured with and will work with the Azure DNS private zones linked to the virtual network.

### Automation

The following APIs let you programmatically manage regional virtual network integrations:

**Azure CLI**: Use thecommands to add, list, or remove a regional virtual network integration.`az functionapp vnet-integration`

**ARM templates**: Regional virtual network integration can be enabled by using an Azure Resource Manager template. For a full example, see[this Functions quickstart template](https://azure.microsoft.com/resources/templates/function-premium-vnet-integration/).

## Hybrid Connections

[Hybrid Connections](../azure-relay/relay-hybrid-connections-protocol) is a feature of Azure Relay that you can use to access application resources in other networks. It provides access from your app to an application endpoint. You can't use it to access your application. Hybrid Connections is available to functions that run on Windows in all but the Consumption plan.

As used in Azure Functions, each hybrid connection correlates to a single TCP host and port combination. This means that the hybrid connection's endpoint can be on any operating system and any application as long as you're accessing a TCP listening port. The Hybrid Connections feature doesn't know or care what the application protocol is or what you're accessing. It just provides network access.

To learn more, see the [App Service documentation for Hybrid Connections](../app-service/app-service-hybrid-connections). These same configuration steps support Azure Functions.

Important

Hybrid Connections is only supported when your function app runs on Windows. Linux apps aren't supported.

## Connecting to Azure Services through a virtual network

Virtual network integration enables your function app to access resources in a virtual network. This section overviews things you should consider when attempting to connect your app to certain services.

### Restrict your storage account to a virtual network

Note

To quickly deploy a function app with private endpoints enabled on the storage account, refer to the following template: [Function app with Azure Storage private endpoints](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/function-app-storage-private-endpoints).

When you create a function app, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage. You can replace this storage account with one that is secured with service endpoints or private endpoints.

You can use a network restricted storage account with function apps on the Flex Consumption, Elastic Premium, and Dedicated (App Service) plans; the Consumption plan isn't supported. For Elastic Premium and Dedicated plans, you have to ensure that private [content share routing](../app-service/configure-vnet-integration-routing#content-share) is configured. To learn how to configure your function app with a storage account secured with a virtual network, see [Restrict your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network).

### Use Key Vault references

You can use Azure Key Vault references to use secrets from Azure Key Vault in your Azure Functions application without requiring any code changes. Azure Key Vault is a service that provides centralized secrets management, with full control over access policies and audit history.

If virtual network integration is configured for the app, [Key Vault references](../app-service/app-service-key-vault-references) can be used to retrieve secrets from a network-restricted vault.

### Virtual network triggers (non-HTTP)

Your workload might require your app to be triggered from an event source protected by a virtual network. There's two options if you want your app to dynamically scale based on the number of events received from non-HTTP trigger sources:

- Run your function app in a
[Flex Consumption](flex-consumption-plan). - Run your function app in an
[Elastic Premium plan](functions-premium-plan)and enable virtual network trigger support.

Function apps running on the [Dedicated (App Service)](dedicated-plan) plans don't dynamically scale based on events. Rather, scale out is dictated by [autoscale](dedicated-plan#scaling) rules you define.

#### Elastic Premium plan with virtual network triggers

The [Elastic Premium plan](functions-premium-plan) lets you create functions that are triggered by services secured by a virtual network. These non-HTTP triggers are known as *virtual network triggers*.

By default, virtual network triggers don't cause your function app to scale beyond their prewarmed instance count. However, certain extensions support virtual network triggers that cause your function app to scale dynamically. You can enable this *dynamic scale monitoring* in your function app for supported extensions in one of these ways:

In the

[Azure portal](https://portal.azure.com), navigate to your function app.Under

**Settings**select**Configuration**, then in the**Function runtime settings**tab set**Runtime Scale Monitoring**to**On**.Select

**Save**to update the function app configuration and restart the app.


Tip

Enabling the monitoring of virtual network triggers can affect the performance of your application, though the impact is likely to be small.

Support for dynamic scale monitoring of virtual network triggers isn't available in version 1.x of the Functions runtime.

The extensions in this table support dynamic scale monitoring of virtual network triggers. To get the best scaling performance, you should upgrade to versions that also support [target-based scaling](functions-target-based-scaling#premium-plan-with-runtime-scale-monitoring-enabled).

| Extension (minimum version) | Runtime scale monitoring only | With
|
|---|

[Microsoft.Azure.WebJobs.Extensions.CosmosDB](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.CosmosDB)[Microsoft.Azure.WebJobs.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask)[Microsoft.Azure.WebJobs.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs)[Microsoft.Azure.WebJobs.Extensions.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ServiceBus)[Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage/)** Queue storage only.

Important

When you enable virtual network trigger monitoring, only triggers for these extensions can cause your app to scale dynamically. You can still use triggers from extensions that aren't in this table, but they won't cause scaling beyond their prewarmed instance count. For a complete list of all trigger and binding extensions, see [Triggers and bindings](functions-triggers-bindings#supported-bindings).

#### App Service plan and App Service Environment with virtual network triggers

When your function app runs in either an App Service plan or an App Service Environment, you can write functions that are triggered by resources secured by a virtual network. For your functions to get triggered correctly, your app must be connected to a virtual network with access to the resource defined in the trigger connection.

For example, assume you want to configure Azure Cosmos DB to accept traffic only from a virtual network. In this case, you must deploy your function app in an App Service plan that provides virtual network integration with that virtual network. Integration enables a function to be triggered by that Azure Cosmos DB resource.

## Testing considerations

When testing functions in a function app with private endpoints, you must do your testing from within the same virtual network, such as on a virtual machine (VM) in that network. To use the **Code + Test** option in the portal from that VM, you need to add following [CORS origins](functions-how-to-use-azure-function-app-settings?tabs=portal#cors) to your function app:

`https://functions-next.azure.com`

`https://functions-staging.azure.com`

`https://functions.azure.com`

`https://portal.azure.com`


When you restrict access to your function app with private endpoints or any other access restriction, you also must add the service tag `AzureCloud`

to the allowed list. To update the allowed list:

Navigate to your function app and select

**Settings**>**Networking**and then select**Inbound access configuration**>**Public network access**.Make sure that

**Public network access**is set to**Enabled from select virtual networks and IP addresses**.**Add a rule**under Site access and rules:Select

`Service Tag`

as the Source settings**Type**and`AzureCloud`

as the**Service Tag**.Make sure the action is

**Allow**, and set your desired name and priority.


## Troubleshooting

The feature is easy to set up, but that doesn't mean your experience will be problem free. If you encounter problems accessing your desired endpoint, there are some utilities you can use to test connectivity from the app console. There are two consoles that you can use. One is the Kudu console, and the other is the console in the Azure portal. To reach the Kudu console from your app, go to **Tools** > **Kudu**. You can also reach the Kudo console at [sitename].scm.azurewebsites.net. After the website loads, go to the **Debug console** tab. To get to the Azure portal-hosted console from your app, go to **Tools** > **Console**.

#### Tools

In native Windows apps, the tools **ping**, **nslookup**, and **tracert** won't work through the console because of security constraints (they work in [custom Windows containers](../app-service/quickstart-custom-container)). To fill the void, two separate tools are added. To test DNS functionality, we added a tool named **nameresolver.exe**. The syntax is:

```
nameresolver.exe hostname [optional: DNS Server]
```


You can use nameresolver to check the hostnames that your app depends on. This way you can test if you have anything misconfigured with your DNS or perhaps don't have access to your DNS server. You can see the DNS server that your app uses in the console by looking at the environmental variables WEBSITE_DNS_SERVER and WEBSITE_DNS_ALT_SERVER.

Note

The nameresolver.exe tool currently doesn't work in custom Windows containers.

You can use the next tool to test for TCP connectivity to a host and port combination. This tool is called **tcpping** and the syntax is:

```
tcpping.exe hostname [optional: port]
```


The **tcpping** utility tells you if you can reach a specific host and port. It can show success only if there's an application listening at the host and port combination, and there's network access from your app to the specified host and port.

#### Debug access to virtual network-hosted resources

A number of things can prevent your app from reaching a specific host and port. Most of the time it's one of these things:

**A firewall is in the way.**If you have a firewall in the way, you hit the TCP timeout. The TCP timeout is 21 seconds in this case. Use the**tcpping**tool to test connectivity. TCP timeouts can be caused by many things beyond firewalls, but start there.**DNS isn't accessible.**The DNS timeout is 3 seconds per DNS server. If you have two DNS servers, the timeout is 6 seconds. Use nameresolver to see if DNS is working. You can't use nslookup, because that doesn't use the DNS your virtual network is configured with. If inaccessible, you could have a firewall or NSG blocking access to DNS or it could be down.

If those items don't answer your problems, look first for things like:

**Regional virtual network integration**

- Is your destination a non-RFC1918 address and you don't have
**Route All**enabled? - Is there an NSG blocking egress from your integration subnet?
- If you're going across Azure ExpressRoute or a VPN, is your on-premises gateway configured to route traffic back up to Azure? If you can reach endpoints in your virtual network but not on-premises, check your routes.
- Do you have enough permissions to set delegation on the integration subnet? During regional virtual network integration configuration, your integration subnet is delegated to Microsoft.Web/serverFarms. The VNet integration UI delegates the subnet to Microsoft.Web/serverFarms automatically. If your account doesn't have sufficient networking permissions to set delegation, you'll need someone who can set attributes on your integration subnet to delegate the subnet. To manually delegate the integration subnet, go to the Azure Virtual Network subnet UI and set the delegation for Microsoft.Web/serverFarms.

**Gateway-required virtual network integration**

- Is the point-to-site address range in the RFC 1918 ranges (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255)?
- Does the gateway show as being up in the portal? If your gateway is down, then bring it back up.
- Do certificates show as being in sync, or do you suspect that the network configuration was changed? If your certificates are out of sync or you suspect that a change was made to your virtual network configuration that wasn't synced with your ASPs, select
**Sync Network**. - If you're going across a VPN, is the on-premises gateway configured to route traffic back up to Azure? If you can reach endpoints in your virtual network but not on-premises, check your routes.
- Are you trying to use a coexistence gateway that supports both point to site and ExpressRoute? Coexistence gateways aren't supported with virtual network integration.

Debugging networking issues is a challenge because you can't see what's blocking access to a specific host:port combination. Some causes include:

- You have a firewall up on your host that prevents access to the application port from your point-to-site IP range. Crossing subnets often requires public access.
- Your target host is down.
- Your application is down.
- You had the wrong IP or hostname.
- Your application is listening on a different port than what you expected. You can match your process ID with the listening port by using "netstat -aon" on the endpoint host.
- Your network security groups are configured in such a manner that they prevent access to your application host and port from your point-to-site IP range.

You don't know what address your app actually uses. It could be any address in the integration subnet or point-to-site address range, so you need to allow access from the entire address range.

More debug steps include:

- Connect to a VM in your virtual network and attempt to reach your resource host:port from there. To test for TCP access, use the PowerShell command
**Test-NetConnection**. The syntax is:

```
Test-NetConnection hostname [optional: -Port]
```


- Bring up an application on a VM and test access to that host and port from the console from your app by using
**tcpping**.

#### On-premises resources

If your app can't reach a resource on-premises, check if you can reach the resource from your virtual network. Use the **Test-NetConnection** PowerShell command to check for TCP access. If your VM can't reach your on-premises resource, your VPN or ExpressRoute connection might not be configured properly.

If your virtual network-hosted VM can reach your on-premises system but your app can't, the cause is likely one of the following reasons:

- Your routes aren't configured with your subnet or point-to-site address ranges in your on-premises gateway.
- Your network security groups are blocking access for your point-to-site IP range.
- Your on-premises firewalls are blocking traffic from your point-to-site IP range.
- You're trying to reach a non-RFC 1918 address by using the regional virtual network integration feature.

#### Deleting the App Service plan or web app before disconnecting the VNet integration

If you deleted the web app or the App Service plan without disconnecting the VNet integration first, you will not be able to do any update/delete operations on the virtual network or subnet that was used for the integration with the deleted resource. A subnet delegation 'Microsoft.Web/serverFarms' will remain assigned to your subnet and will prevent the update/delete operations.

In order to do update/delete the subnet or virtual network again you need to re-create the VNet integration and then disconnect it:

- Re-create the App Service plan and web app (it is mandatory to use the exact same web app name as before).
- Navigate to the 'Networking' blade on the web app and configure the VNet integration.
- After the VNet integration is configured, select the 'Disconnect' button.
- Delete the App Service plan or web app.
- Update/Delete the subnet or virtual network.

If you still encounter issues with the VNet integration after following the steps above, please contact Microsoft Support.

### Network troubleshooter

You can also use the Network troubleshooter to resolve connection issues. To open the network troubleshooter, go to the app in the Azure portal. Select **Diagnostic and solve problem**, and then search for **Network troubleshooter**.

**Connection issues** - It checks the status of the virtual network integration, including checking if the Private IP has been assigned to all instances of the plan and the DNS settings. If a custom DNS isn't configured, default Azure DNS is applied. The troubleshooter also checks for common Function app dependencies including connectivity for Azure Storage and other binding dependencies.


**Configuration issues** - This troubleshooter checks if your subnet is valid for virtual network integration.


**Subnet/VNet deletion issue** - This troubleshooter checks if your subnet has any locks and if it has any unused Service Association Links that might be blocking the deletion of the VNet/subnet.

## Next steps

To learn more about networking and Azure Functions:

[Follow the tutorial about getting started with virtual network integration](functions-create-vnet)[Read the Functions networking FAQ](functions-networking-faq)[Learn more about virtual network integration with App Service/Functions](../app-service/overview-vnet-integration)[Learn more about virtual networks in Azure](../virtual-network/virtual-networks-overview)[Enable more networking features and control with App Service Environments](../app-service/environment/intro)[Connect to individual on-premises resources without firewall changes by using Hybrid Connections](../app-service/app-service-hybrid-connections)
