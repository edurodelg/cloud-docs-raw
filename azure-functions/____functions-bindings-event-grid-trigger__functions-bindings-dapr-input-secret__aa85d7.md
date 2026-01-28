---
merged_at: 2026-01-28T07:43:39.523363
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid-trigger -->

# Azure Event Grid trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the function trigger to respond to an event sent by an [Event Grid source](../event-grid/overview). You must have an event subscription to the source to receive events. To learn how to create an event subscription, see [Create a subscription](event-grid-how-tos#create-a-subscription). For information on binding setup and configuration, see the [overview](functions-bindings-event-grid).

Note

Event Grid triggers aren't natively supported in an internal load balancer App Service Environment (ASE). The trigger uses an HTTP request that can't reach the function app without a gateway into the virtual network.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

For an HTTP trigger example, see [Receive events to an HTTP endpoint](../event-grid/receive-events).

The type of the input parameter used with an Event Grid trigger depends on these three factors:

- Functions runtime version
- Binding extension version
- Modality of the C# function.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

When running your C# function in an isolated worker process, you need to define a custom type for event properties. The following example defines a `MyEventType`

class.

```
{
public string? Id { get; set; }
public string? Topic { get; set; }
public string? Subject { get; set; }
public string? EventType { get; set; }
public DateTime EventTime { get; set; }
public IDictionary<string, object>? Data { get; set; }
}
```


The following example shows how the custom type is used in both the trigger and an Event Grid output binding:

```
[Function(nameof(EventGridFunction))]
[EventGridOutput(TopicEndpointUri = "MyEventGridTopicUriSetting", TopicKeySetting = "MyEventGridTopicKeySetting")]
public static MyEventType Run([EventGridTrigger] MyEventType input, FunctionContext context)
{
var logger = context.GetLogger(nameof(EventGridFunction));
logger.LogInformation(input.Data?.ToString());
var outputEvent = new MyEventType()
{
Id = "unique-id",
Subject = "abc-subject",
Data = new Dictionary<string, object>
{
{ "myKey", "myValue" }
}
};
return outputEvent;
}
```


This section contains the following examples:

The following examples show trigger binding in [Java](functions-reference-java) that use the binding and generate an event, first receiving the event as `String`

and second as a POJO.

### Event Grid trigger, String parameter

```
@FunctionName("eventGridMonitorString")
public void logEvent(
@EventGridTrigger(
name = "event"
)
String content,
final ExecutionContext context) {
context.getLogger().info("Event content: " + content);
}
```


### Event Grid trigger, POJO parameter

This example uses the following POJO, representing the top-level properties of an Event Grid event:

```
import java.util.Date;
import java.util.Map;
public class EventSchema {
public String topic;
public String subject;
public String eventType;
public Date eventTime;
public String id;
public String dataVersion;
public String metadataVersion;
public Map<String, Object> data;
}
```


Upon arrival, the event's JSON payload is de-serialized into the `EventSchema`

POJO for use by the function. This process allows the function to access the event's properties in an object-oriented way.

```
@FunctionName("eventGridMonitor")
public void logEvent(
@EventGridTrigger(
name = "event"
)
EventSchema event,
final ExecutionContext context) {
context.getLogger().info("Event content: ");
context.getLogger().info("Subject: " + event.subject);
context.getLogger().info("Time: " + event.eventTime); // automatically converted to Date by the runtime
context.getLogger().info("Id: " + event.id);
context.getLogger().info("Data: " + event.data);
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `EventGridTrigger`

annotation on parameters whose value would come from Event Grid. Parameters with these annotations cause the function to run when an event arrives. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

The following example shows an event grid trigger [TypeScript function](functions-reference-node?tabs=typescript).

```
import { app, EventGridEvent, InvocationContext } from '@azure/functions';
export async function eventGridTrigger1(event: EventGridEvent, context: InvocationContext): Promise<void> {
context.log('Event grid function processed event:', event);
}
app.eventGrid('eventGridTrigger1', {
handler: eventGridTrigger1,
});
```


The following example shows an event grid trigger [JavaScript function](functions-reference-node).

```
const { app } = require('@azure/functions');
app.eventGrid('eventGridTrigger1', {
handler: (event, context) => {
context.log('Event grid function processed event:', event);
},
});
```


The following example shows how to configure an Event Grid trigger binding in the *function.json* file.

```
{
"bindings": [
{
"type": "eventGridTrigger",
"name": "eventGridEvent",
"direction": "in"
}
]
}
```


The Event Grid event is made available to the function via a parameter named `eventGridEvent`

, as shown in the following PowerShell example.

```
param($eventGridEvent, $TriggerMetadata)
# Make sure to pass hashtables to Out-String so they're logged correctly
$eventGridEvent | Out-String | Write-Host
```


The following example shows an Event Grid trigger binding and a Python function that uses the binding. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="eventGridTrigger")
@app.event_grid_trigger(arg_name="event")
def eventGridTest(event: func.EventGridEvent):
result = json.dumps({
'id': event.id,
'data': event.get_json(),
'topic': event.topic,
'subject': event.subject,
'event_type': event.event_type,
})
logging.info('Python EventGrid trigger processed an event: %s', result)
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the [EventGridTrigger](https://github.com/Azure/azure-functions-eventgrid-extension/blob/master/src/EventGridExtension/TriggerBinding/EventGridTriggerAttribute.cs) attribute. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-grid-trigger).

Here's an `EventGridTrigger`

attribute in a method signature:

```
[Function(nameof(EventGridFunction))]
[EventGridOutput(TopicEndpointUri = "MyEventGridTopicUriSetting", TopicKeySetting = "MyEventGridTopicKeySetting")]
public static MyEventType Run([EventGridTrigger] MyEventType input, FunctionContext context)
{
```


## Annotations

The [EventGridTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventgridtrigger) annotation allows you to declaratively configure an Event Grid binding by providing configuration values. See the [example](#example) and [configuration](#configuration) sections for more detail.

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file. There are no constructor parameters or properties to set in the `EventGridTrigger`

attribute.

| function.json property | Description |
|---|---|
type |
Required - must be set to `eventGridTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code for the parameter that receives the event data. |

See the [Example section](#example) for complete examples.

## Usage

The Event Grid trigger uses a webhook HTTP request, which can be configured using the same [ host.json settings as the HTTP Trigger](functions-bindings-http-webhook#hostjson-settings).

The parameter type supported by the Event Grid trigger depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single event, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions tries to deserialize the JSON data of the event into a plain-old CLR object (POCO) type. |
`string` |
The event as a string. |
1 |

[CloudEvent](/en-us/dotnet/api/azure.messaging.cloudevent)1[EventGridEvent](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridevent)1When you want the function to process a batch of events, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
`CloudEvent[]` 1,`EventGridEvent[]` 1,`string[]` ,`BinaryData[]` 1 |
An array of events from the batch. Each entry represents one event. |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventGrid 3.3.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid/3.3.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

The Event Grid event instance is available via the parameter associated to the `EventGridTrigger`

attribute, typed as an `EventSchema`

.

The Event Grid instance is available via the parameter configured in the *function.json* file's `name`

property.

The Event Grid instance is available via the parameter configured in the *function.json* file's `name`

property, typed as `func.EventGridEvent`

.

## Event schema

Data for an Event Grid event is received as a JSON object in the body of an HTTP request. The JSON looks similar to the following example:

```
[{
"topic": "/subscriptions/{subscriptionid}/resourceGroups/eg0122/providers/Microsoft.Storage/storageAccounts/egblobstore",
"subject": "/blobServices/default/containers/{containername}/blobs/blobname.jpg",
"eventType": "Microsoft.Storage.BlobCreated",
"eventTime": "2018-01-23T17:02:19.6069787Z",
"id": "{guid}",
"data": {
"api": "PutBlockList",
"clientRequestId": "{guid}",
"requestId": "{guid}",
"eTag": "0x8D562831044DDD0",
"contentType": "application/octet-stream",
"contentLength": 2248,
"blobType": "BlockBlob",
"url": "https://egblobstore.blob.core.windows.net/{containername}/blobname.jpg",
"sequencer": "000000000000272D000000000003D60F",
"storageDiagnostics": {
"batchId": "{guid}"
}
},
"dataVersion": "",
"metadataVersion": "1"
}]
```


The example shown is an array of one element. Event Grid always sends an array and may send more than one event in the array. The runtime invokes your function once for each array element.

The top-level properties in the event JSON data are the same among all event types, while the contents of the `data`

property are specific to each event type. The example shown is for a blob storage event.

For explanations of the common and event-specific properties, see [Event properties](../event-grid/event-schema#event-properties) in the Event Grid documentation.

## Next steps

- If you have questions, submit an issue to the team
[here](https://github.com/Azure/azure-sdk-for-net/issues) [Dispatch an Event Grid event](functions-bindings-event-grid-output)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-input-secret -->

# Dapr Secret input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr secret input binding allows you to read secrets data as input during function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("RetrieveSecret")]
public static void Run(
[DaprServiceInvocationTrigger] object args,
[DaprSecret("kubernetes", "my-secret", Metadata = "metadata.namespace=default")] IDictionary<string, string> secret,
ILogger log)
{
log.LogInformation("C# function processed a RetrieveSecret request from the Dapr Runtime.");
}
```


The following example creates a `"RetrieveSecret"`

function using the `DaprSecretInput`

binding with the [ DaprServiceInvocationTrigger](functions-bindings-dapr-trigger-svc-invoke):

```
@FunctionName("RetrieveSecret")
public void run(
@DaprServiceInvocationTrigger(
methodName = "RetrieveSecret") Object args,
@DaprSecretInput(
secretStoreName = "kubernetes",
key = "my-secret",
metadata = "metadata.namespace=default")
Map<String, String> secret,
final ExecutionContext context)
```


In the following example, the Dapr secret input binding is paired with a Dapr invoke trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('RetrieveSecret', {
trigger: trigger.generic({
type: 'daprServiceInvocationTrigger',
name: "payload"
}),
extraInputs: [daprSecretInput],
handler: async (request, context) => {
context.log("Node function processed a RetrieveSecret request from the Dapr Runtime.");
const daprSecretInputValue = context.extraInputs.get(daprSecretInput);
// print the fetched secret value
for (var key in daprSecretInputValue) {
context.log(`Stored secret: Key=${key}, Value=${daprSecretInputValue[key]}`);
}
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprServiceInvocationTrigger`

:

```
{
"bindings":
{
"type": "daprSecret",
"direction": "in",
"name": "secret",
"key": "my-secret",
"secretStoreName": "localsecretstore",
"metadata": "metadata.namespace=default"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System
using namespace Microsoft.Azure.WebJobs
using namespace Microsoft.Extensions.Logging
using namespace Microsoft.Azure.WebJobs.Extensions.Dapr
using namespace Newtonsoft.Json.Linq
param (
$payload, $secret
)
# PowerShell function processed a CreateNewOrder request from the Dapr Runtime.
Write-Host "PowerShell function processed a RetrieveSecretLocal request from the Dapr Runtime."
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $secret | ConvertTo-Json
Write-Host "$jsonString"
```


The following example shows a Dapr Secret input binding, which uses the [v2 Python programming model](functions-reference-python). To use the `daprSecret`

binding alongside the `daprServiceInvocationTrigger`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="RetrieveSecret")
@app.dapr_service_invocation_trigger(arg_name="payload", method_name="RetrieveSecret")
@app.dapr_secret_input(arg_name="secret", secret_store_name="localsecretstore", key="my-secret", metadata="metadata.namespace=default")
def main(payload, secret: str) :
# Function should be invoked with this command: dapr invoke --app-id functionapp --method RetrieveSecret --data '{}'
logging.info('Python function processed a RetrieveSecret request from the Dapr Runtime.')
secret_dict = json.loads(secret)
for key in secret_dict:
logging.info("Stored secret: Key = " + key +
', Value = ' + secret_dict[key])
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprSecret`

to define a Dapr secret input binding, which supports these parameters:

| Parameter | Description |
|---|---|
SecretStoreName |
The name of the secret store to get the secret. |
Key |
The key identifying the name of the secret to get. |
Metadata |
Optional. An array of metadata properties in the form `"key1=value1&key2=value2"` . |

## Annotations

The `DaprSecretInput`

annotation allows you to have your function access a secret.

| Element | Description |
|---|---|
secretStoreName |
The name of the Dapr secret store. |
key |
The secret key value. |
metadata |
Optional. The metadata values. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
key |
The secret key value. |
secretStoreName |
Name of the secret store as defined in the local-secret-store.yaml component file. |
metadata |
The metadata namespace. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
key |
The secret key value. |
secretStoreName |
Name of the secret store as defined in the local-secret-store.yaml component file. |
metadata |
The metadata namespace. |

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr secret input binding, start by setting up a Dapr secret store component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprSecret`

in **Python v2**, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-identity-access-azure-sql-with-managed-identity -->

# Tutorial: Connect a function app to Azure SQL with managed identity and SQL bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides a [managed identity](../active-directory/managed-identities-azure-resources/overview), which is a turn-key solution for securing access to [Azure SQL Database](/en-us/azure/sql-database/) and other Azure services. Managed identities make your app more secure by eliminating secrets from your app, such as credentials in the connection strings. In this tutorial, you'll add managed identity to an Azure Function that utilizes [Azure SQL bindings](functions-bindings-azure-sql). A sample Azure Function project with SQL bindings is available in the [ToDo backend example](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/).

When you're finished with this tutorial, your Azure Function will connect to Azure SQL database without the need of username and password.

An overview of the steps you'll take:

## Grant database access to Microsoft Entra user

First enable Microsoft Entra authentication to SQL database by assigning a Microsoft Entra user as the Active Directory admin of the server. This user is different from the Microsoft account you used to sign up for your Azure subscription. It must be a user that you created, imported, synced, or invited into Microsoft Entra ID. For more information on allowed Microsoft Entra users, see [Microsoft Entra features and limitations in SQL database](/en-us/azure/azure-sql/database/authentication-aad-overview#azure-ad-features-and-limitations).

Enabling Microsoft Entra authentication can be completed via the Azure portal, PowerShell, or Azure CLI. Directions for Azure CLI are below and information completing this via Azure portal and PowerShell is available in the [Azure SQL documentation on Microsoft Entra authentication](/en-us/azure/azure-sql/database/authentication-aad-configure).

If your Microsoft Entra tenant doesn't have a user yet, create one by following the steps at

[Add or delete users using Microsoft Entra ID](../active-directory/fundamentals/add-users-azure-active-directory).Find the object ID of the Microsoft Entra user using the

and replace`az ad user list`

*<user-principal-name>*. The result is saved to a variable.For Azure CLI 2.37.0 and newer:

`azureaduser=$(az ad user list --filter "userPrincipalName eq '<user-principal-name>'" --query [].id --output tsv)`

For older versions of Azure CLI:

`azureaduser=$(az ad user list --filter "userPrincipalName eq '<user-principal-name>'" --query [].objectId --output tsv)`

Tip

To see the list of all user principal names in Microsoft Entra ID, run

`az ad user list --query [].userPrincipalName`

.Add this Microsoft Entra user as an Active Directory admin using

command in the Cloud Shell. In the following command, replace`az sql server ad-admin create`

*<server-name>*with the server name (without the`.database.windows.net`

suffix).`az sql server ad-admin create --resource-group myResourceGroup --server-name <server-name> --display-name ADMIN --object-id $azureaduser`


For more information on adding an Active Directory admin, see [Provision a Microsoft Entra administrator for your server](/en-us/azure/azure-sql/database/authentication-aad-configure#provision-azure-ad-admin-sql-database)

## Enable system-assigned managed identity on Azure Function

In this step we'll add a system-assigned identity to the Azure Function. In later steps, this identity will be given access to the SQL database.

To enable system-assigned managed identity in the Azure portal:

- Create an Azure Function in the portal as you normally would. Navigate to it in the portal.
- Scroll down to the Settings group in the left navigation.
- Select Identity.
- Within the System assigned tab, switch Status to On. Click Save.


For information on enabling system-assigned managed identity through Azure CLI or PowerShell, check out more information on [using managed identities with Azure Functions](../app-service/overview-managed-identity?tabs=dotnet&toc=/azure/azure-functions/toc.json#add-a-system-assigned-identity).

Tip

For user-assigned managed identity, switch to the User Assigned tab. Click Add and select a Managed Identity. For more information on creating user-assigned managed identity, see the [Manage user-assigned managed identities](../active-directory/managed-identities-azure-resources/how-manage-user-assigned-managed-identities).

## Grant SQL database access to the managed identity

In this step we'll connect to the SQL database with a Microsoft Entra user account and grant the managed identity access to the database.

Open your preferred SQL tool and login with a Microsoft Entra user account (such as the Microsoft Entra user we assigned as administrator). This can be accomplished in Cloud Shell with the SQLCMD command.

`sqlcmd -S <server-name>.database.windows.net -d <db-name> -U <aad-user-name> -P "<aad-password>" -G -l 30`

In the SQL prompt for the database you want, run the following commands to grant permissions to your function. For example,

`CREATE USER [<identity-name>] FROM EXTERNAL PROVIDER; ALTER ROLE db_datareader ADD MEMBER [<identity-name>]; ALTER ROLE db_datawriter ADD MEMBER [<identity-name>]; GO`

*<identity-name>*is the name of the managed identity in Microsoft Entra ID. If the identity is system-assigned, the name is always the same as the name of your Function app.

## Configure Azure Function SQL connection string

In the final step we'll configure the Azure Function SQL connection string to use Microsoft Entra managed identity authentication.

The connection string setting name is identified in our Functions code as the binding attribute "ConnectionStringSetting", as seen in the SQL input binding [attributes and annotations](functions-bindings-azure-sql-input?pivots=programming-language-csharp#attributes).

In the application settings of our Function App the SQL connection string setting should be updated to follow this format:

`Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; Database=testdb`


*testdb* is the name of the database we're connecting to and *demo.database.windows.net* is the name of the server we're connecting to.

Tip

For user-assigned managed identity, use `Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; User Id=ClientIdOfManagedIdentity; Database=testdb`

.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/deployment-zip-push -->

# Zip deployment for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to deploy your function app project files to Azure from a .zip (compressed) file. You learn how to do a push deployment, both by using Azure CLI and by using the REST APIs. [Azure Functions Core Tools](functions-run-local) also uses these deployment APIs when publishing a local project to Azure.

Zip deployment is also an easy way to [run your functions from a package file in Azure](run-functions-from-deployment-package). It's the default deployment technology in the [Consumption](consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) hosting plans. The [Flex Consumption](flex-consumption-plan) plan doesn't support zip deployment.

Azure Functions has the full range of continuous deployment and integration options that are provided by Azure App Service. For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment).

To speed up development, you might find it easier to deploy your function app project files directly from a .zip file. The .zip deployment API takes the contents of a .zip file and extracts the contents into the `wwwroot`

folder of your function app. This .zip file deployment uses the same Kudu service that powers continuous integration-based deployments, including:

- Deletion of files that were left over from earlier deployments.
- Deployment customization, including running deployment scripts.
- Deployment logs.
- Syncing function triggers in a
[Consumption plan](functions-scale)function app.

For more information, see the [.zip deployment reference](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file-or-url).

Important

When you use .zip deployment, any files from the previous deployment are either deleted or updated during a subsequent deployment to your function app. Other files and directories in your function app that weren't part of the previous deployment are maintained.

## Deployment .zip file requirements

The zip archive you deploy must contain all of the files needed to run your function app. You can manually create a zip archive from the contents of a Functions project folder using built-in .zip compression functionality or non-Microsoft tools.

The archive must include the [host.json](functions-host-json) file at the root of the extracted folder. The selected language stack for the function app creates other requirements:

Important

For languages that generate compiled output for deployment, make sure to compress the contents of the output folder you plan to publish and not the entire project folder. When Functions extracts the contents of the zip archive, the `host.json`

file must exist in the root of the package.

A zip deployment process extracts the zip archive's files and folders in the `wwwroot`

directory. If you include the parent directory when creating the archive, the system won't find the files it expects to see in `wwwroot`

.

## Deploy by using Azure CLI

You can use Azure CLI to trigger a push deployment. Push deploy a .zip file to your function app by using the [az functionapp deployment source config-zip](/en-us/cli/azure/functionapp/deployment/source#az-functionapp-deployment-source-config-zip) command. To use this command, you must use Azure CLI version 2.0.21 or later. To see what Azure CLI version you're using, use the `az --version`

command.

In the following command, replace the `<zip_file_path>`

placeholder with the path to the location of your .zip file. Also, replace `<app_name>`

with the unique name of your function app and replace `<resource_group>`

with the name of your resource group.

```
az functionapp deployment source config-zip -g <resource_group> -n \
<app_name> --src <zip_file_path>
```


This command deploys project files from the downloaded .zip file to your function app in Azure. It then restarts the app. To view the list of deployments for this function app, you must use the REST APIs.

When you're using Azure CLI on your local computer, `<zip_file_path>`

is the path to the .zip file on your computer. You can also run Azure CLI in [Azure Cloud Shell](../cloud-shell/overview). When you use Cloud Shell, you must first upload your deployment .zip file to the Azure Files account that's associated with your Cloud Shell. In that case, `<zip_file_path>`

is the storage location that your Cloud Shell account uses. For more information, see [Persist files in Azure Cloud Shell](../cloud-shell/persisting-shell-storage).

## Deploy ZIP file with REST APIs

You can use the [deployment service REST APIs](https://github.com/projectkudu/kudu/wiki/REST-API) to deploy the .zip file to your app in Azure. To deploy, send a POST request to `https://<app_name>.scm.azurewebsites.net/api/zipdeploy`

. The POST request must contain the .zip file in the message body. The deployment credentials for your app are provided in the request by using HTTP BASIC authentication. For more information, see the [.zip push deployment reference](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file).

For the HTTP BASIC authentication, you need your App Service deployment credentials. To see how to set your deployment credentials, see [Set and reset user-level credentials](../app-service/deploy-configure-credentials#userscope).

### With cURL

The following example uses the cURL tool to deploy a .zip file. Replace the placeholders `<deployment_user>`

, `<zip_file_path>`

, and `<app_name>`

. When prompted by cURL, type in the password.

```
curl -X POST -u <deployment_user> --data-binary "@<zip_file_path>" https://<app_name>.scm.azurewebsites.net/api/zipdeploy
```


This request triggers push deployment from the uploaded .zip file. You can review the current and past deployments by using the `https://<app_name>.scm.azurewebsites.net/api/deployments`

endpoint, as shown in the following cURL example. Again, replace `<app_name>`

with the name of your app and `<deployment_user>`

with the username of your deployment credentials.

```
curl -u <deployment_user> https://<app_name>.scm.azurewebsites.net/api/deployments
```


#### Asynchronous zip deployment

While deploying synchronously, you might receive errors related to connection timeouts. Add `?isAsync=true`

to the URL to deploy asynchronously. You receive a response as soon as the zip file is uploaded with a `Location`

header pointing to the pollable deployment status URL. When polling the URL provided in the `Location`

header, you receive an HTTP 202 (Accepted) response while the process is ongoing and an HTTP 200 (OK) response once the archive has been expanded and the deployment completes successfully.

#### Microsoft Entra authentication

An alternative to using HTTP BASIC authentication for the zip deployment is to use a Microsoft Entra identity. Microsoft Entra identity might be needed if [HTTP BASIC authentication is disabled for the SCM site](../app-service/deploy-configure-credentials#disable-basic-authentication).

A valid Microsoft Entra access token for the user or service principal performing the deployment is required. An access token can be retrieved using the Azure CLI's `az account get-access-token`

command. The access token is used in the Authentication header of the HTTP POST request.

```
curl -X POST \
--data-binary "@<zip_file_path>" \
-H "Authorization: Bearer <access_token>" \
"https://<app_name>.scm.azurewebsites.net/api/zipdeploy"
```


### With PowerShell

The following example uses [Publish-AzWebapp](/en-us/powershell/module/az.websites/publish-azwebapp) upload the .zip file. Replace the placeholders `<group-name>`

, `<app-name>`

, and `<zip-file-path>`

.

```
Publish-AzWebapp -ResourceGroupName <group-name> -Name <app-name> -ArchivePath <zip-file-path>
```


This request triggers push deployment from the uploaded .zip file.

To review the current and past deployments, run the following commands. Again, replace the `<deployment-user>`

, `<deployment-password>`

, and `<app-name>`

placeholders.

```
$username = "<deployment-user>"
$password = "<deployment-password>"
$apiUrl = "https://<app-name>.scm.azurewebsites.net/api/deployments"
$base64AuthInfo = [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(("{0}:{1}" -f $username, $password)))
$userAgent = "powershell/1.0"
Invoke-RestMethod -Uri $apiUrl -Headers @{Authorization=("Basic {0}" -f $base64AuthInfo)} -UserAgent $userAgent -Method GET
```


## Deploy by using ARM Template

You can use [ZipDeploy ARM template extension](https://github.com/projectkudu/kudu/wiki/MSDeploy-VS.-ZipDeploy#zipdeploy) to push your .zip file to your function app.

### Example ZipDeploy ARM Template

This template includes both a production and staging slot and deploys to one or the other. Typically, you would use this template to deploy to the staging slot and then swap to get your new zip package running on the production slot.

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
"appServiceName": {
"type": "string"
},
"deployToProduction": {
"type": "bool",
"defaultValue": false
},
"slot": {
"type": "string",
"defaultValue": "staging"
},
"packageUri": {
"type": "secureString"
}
},
"resources": [
{
"condition": "[parameters('deployToProduction')]",
"type": "Microsoft.Web/sites/extensions",
"apiVersion": "2021-02-01",
"name": "[format('{0}/ZipDeploy', parameters('appServiceName'))]",
"properties": {
"packageUri": "[parameters('packageUri')]",
"appOffline": true
}
},
{
"condition": "[not(parameters('deployToProduction'))]",
"type": "Microsoft.Web/sites/slots/extensions",
"apiVersion": "2021-02-01",
"name": "[format('{0}/{1}/ZipDeploy', parameters('appServiceName'), parameters('slot'))]",
"properties": {
"packageUri": "[parameters('packageUri')]",
"appOffline": true
}
}
]
}
```


For the initial deployment, you would deploy directly to the production slot. For more information, see [Slot deployments](functions-infrastructure-as-code#slot-deployments).

## Run functions from the deployment package

You can also choose to run your functions directly from the deployment package file. This method skips the deployment step of copying files from the package to the `wwwroot`

directory of your function app. Instead, the Functions runtime mounts the package file, and the contents of the `wwwroot`

directory become read-only.

Zip deployment integrates with this feature, which you can enable by setting the function app setting `WEBSITE_RUN_FROM_PACKAGE`

to a value of `1`

. For more information, see [Run your functions from a deployment package file](run-functions-from-deployment-package).

## Deployment customization

The deployment process assumes that the .zip file that you push contains a ready-to-run app. By default, no customizations are run. To enable the same build processes that you get with continuous integration, add the following to your application settings:

`SCM_DO_BUILD_DURING_DEPLOYMENT=true`


When you use .zip push deployment, this setting is **false** by default. The default is **true** for continuous integration deployments. When set to **true**, your deployment-related settings are used during deployment. You can configure these settings either as app settings or in a .deployment configuration file that's located in the root of your .zip file. For more information, see [Repository and deployment-related settings](https://github.com/projectkudu/kudu/wiki/Configurable-settings#repository-and-deployment-related-settings) in the deployment reference.

## Download your function app files

If you created your functions by using the editor in the Azure portal, you can download your existing function app project as a .zip file in one of these ways:

**From the Azure portal:**Sign in to the

[Azure portal](https://portal.azure.com), and then go to your function app.On the

**Overview**tab, select**Download app content**. Select your download options, and then select**Download**.

The downloaded .zip file is in the correct format to be republished to your function app by using .zip push deployment. The portal download can also add the files needed to open your function app directly in Visual Studio.

**Using REST APIs:**Use the following deployment GET API to download the files from your

`<function_app>`

project:`https://<function_app>.scm.azurewebsites.net/api/zip/site/wwwroot/`

Including

`/site/wwwroot/`

makes sure your zip file includes only the function app project files and not the entire site. If you aren't already signed in to Azure, you are asked to do so.

You can also download a .zip file from a GitHub repository. When you download a GitHub repository as a .zip file, GitHub adds an extra folder level for the branch. This extra folder level means that you can't deploy the .zip file directly as you downloaded it from GitHub. If you're using a GitHub repository to maintain your function app, you should use [continuous integration](functions-continuous-deployment) to deploy your app.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-private-site-access -->

# Tutorial: Establish Azure Functions private site access

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to enable [private site access](functions-networking-options#private-endpoints) with Azure Functions. By using private site access, you can require that your function code is only triggered from a specific virtual network.

Private site access is useful in scenarios when access to the function app needs to be limited to a specific virtual network. For example, the function app may be applicable to only employees of a specific organization, or services which are within the specified virtual network (such as another Azure Function, Azure Virtual Machine, or an AKS cluster).

If a Functions app needs to access Azure resources within the virtual network, or connected via [service endpoints](../virtual-network/virtual-network-service-endpoints-overview), then [virtual network integration](functions-create-vnet) is needed.

In this tutorial, you learn how to configure private site access for your function app:

- Create a virtual machine
- Create an Azure Bastion service
- Create an Azure Functions app
- Configure a virtual network service endpoint
- Create and deploy an Azure Function
- Invoke the function from outside and within the virtual network

If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Topology

The following diagram shows the architecture of the solution to be created:

## Prerequisites

For this tutorial, it's important that you understand IP addressing and subnetting. You can start with [this article that covers the basics of addressing and subnetting](https://support.microsoft.com/help/164015/understanding-tcp-ip-addressing-and-subnetting-basics). Many more articles and videos are available online.

## Sign in to Azure portal

Sign in to the [Azure portal](https://portal.azure.com).

## Create a virtual machine

The first step in this tutorial is to create a new virtual machine inside a virtual network. The virtual machine will be used to access your function once you've restricted its access to only be available from within the virtual network.

Select the

**Create a resource**button.In the search field, type

**Windows Server**, and select**Windows Server**in the search results.Select

**Windows Server 2019 Datacenter**from the list of Windows Server options, and press the**Create**button.In the

*Basics*tab, use the VM settings as specified in the table below the image:Setting Suggested value Description *Subscription*Your subscription The subscription under which your resources are created. *Resource group*myResourceGroup Choose the resource group to contain all the resources for this tutorial. Using the same resource group makes it easier to clean up resources when you're done with this tutorial. *Virtual machine name*myVM The VM name needs to be unique in the resource group *Region*(US) North Central US Choose a region near you or near the functions to be accessed. *Public inbound ports*None Select **None**to ensure there is no inbound connectivity to the VM from the internet. Remote access to the VM will be configured via the Azure Bastion service.Choose the

*Networking*tab and select**Create new**to configure a new virtual network.In

*Create virtual network*, use the settings in the table below the image:Setting Suggested value Description *Name*myResourceGroup-vnet You can use the default name generated for your virtual network. *Address range*10.10.0.0/16 Use a single address range for the virtual network. *Subnet name*Tutorial Name of the subnet. *Address range*(subnet)10.10.1.0/24 The subnet size defines how many interfaces can be added to the subnet. This subnet is used by the VM. A /24 subnet provides 254 host addresses. Select

**OK**to create the virtual network.Back in the

*Networking*tab, ensure**None**is selected for*Public IP*.Choose the

*Management*tab, then in*Diagnostic storage account*, choose**Create new**to create a new Storage account.Leave the default values for the

*Identity*,*Auto-shutdown*, and*Backup*sections.Select

*Review + create*. After validation completes, select**Create**. The VM create process takes a few minutes.

## Configure Azure Bastion

[Azure Bastion](https://azure.microsoft.com/services/azure-bastion/) is a fully managed Azure service which provides secure RDP and SSH access to virtual machines directly from the Azure portal. Using the Azure Bastion service removes the need to configure network settings related to RDP access.

In the portal, choose

**Add**at the top of the resource group view.In the search field, type

**Bastion**.Select

**Bastion**in the search results.Select

**Create**to begin the process of creating a new Azure Bastion resource. You will notice an error message in the*Virtual network*section as there is not yet an AzureBastionSubnet subnet. The subnet is created in the following steps. Use the settings in the table below the image:Setting Suggested value Description *Name*myBastion The name of the new Bastion resource *Region*North Central US Choose a [region](https://azure.microsoft.com/regions/)near you or near other services your functions access.*Virtual network*myResourceGroup-vnet The virtual network in which the Bastion resource will be created in *Subnet*AzureBastionSubnet The subnet in your virtual network to which the new Bastion host resource will be deployed. You must create a subnet using the name value **AzureBastionSubnet**. This value lets Azure know which subnet to deploy the Bastion resources to. You must use a subnet of at least**/27**or larger (/27, /26, and so on).Note

For a detailed, step-by-step guide to creating an Azure Bastion resource, refer to the

[Create an Azure Bastion host](../bastion/tutorial-create-host-portal)tutorial.Create a subnet in which Azure can provision the Azure Bastion host. Choosing

**Manage subnet configuration**opens a new pane where you can define a new subnet. Choose**+ Subnet**to create a new subnet.The subnet must be of the name

**AzureBastionSubnet**and the subnet prefix must be at least**/27**. Select**OK**to create the subnet.On the

*Create a Bastion*page, select the newly created**AzureBastionSubnet**from the list of available subnets.Select

**Review & Create**. Once validation completes, select**Create**. It will take a few minutes for the Azure Bastion resource to be created.

## Create an Azure Functions app

The next step is to create a function app in Azure using the [Consumption plan](consumption-plan). You deploy your function code to this resource later in the tutorial.

In the portal, choose

**Add**at the top of the resource group view.Select

**Compute > Function App**On the

*Basics*section, use the function app settings as specified in the table below.Setting Suggested value Description *Resource Group*myResourceGroup Choose the resource group to contain all the resources for this tutorial. Using the same resource group for the function app and VM makes it easier to clean up resources when you're done with this tutorial. *Function App name*Globally unique name Name that identifies your new function app. Valid characters are a-z (case insensitive), 0-9, and -. *Publish*Code Option to publish code files or a Docker container. *Runtime stack*Preferred language Choose a runtime that supports your favorite function programming language. *Region*North Central US Choose a [region](https://azure.microsoft.com/regions/)near you or near other services your functions access.Select the

**Next: Hosting >**button.For the

*Hosting*section, select the proper*Storage account*,*Operating system*, and*Plan*as described in the following table.Setting Suggested value Description *Storage account*Globally unique name Create a storage account used by your function app. Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only. You can also use an existing account, which must meet the [storage account requirements](storage-considerations#storage-account-requirements).*Operating system*Preferred operating system An operating system is pre-selected for you based on your runtime stack selection, but you can change the setting if necessary. *Plan*Consumption The [hosting plan](functions-scale)dictates how the function app is scaled and resources available to each instance.Select

**Review + Create**to review the app configuration selections.Select

**Create**to provision and deploy the function app.

## Configure access restrictions

The next step is to configure [access restrictions](../app-service/app-service-ip-restrictions) to ensure only resources on the virtual network can invoke the function.

[Private site](functions-networking-options#private-endpoints) access is enabled by creating an Azure Virtual Network [service endpoint](../virtual-network/virtual-network-service-endpoints-overview) between the function app and the specified virtual network. Access restrictions are implemented via service endpoints. Service endpoints ensure only traffic originating from within the specified virtual network can access the designated resource. In this case, the designated resource is the Azure Function.

Within the function app, select the

**Networking**link under the*Settings*section header.The

*Networking*page is the starting point to configure Azure Front Door, the Azure CDN, and also Access Restrictions.Select

**Configure Access Restrictions**to configure private site access.On the

*Access Restrictions*page, you see only the default restriction in place. The default doesn't place any restrictions on access to the function app. Select**Add rule**to create a private site access restriction configuration.In the

*Add Access Restriction*pane, provide a*Name*,*Priority*, and*Description*for the new rule.Select

**Virtual Network**from the*Type*drop-down box, then select the previously created virtual network, and then select the**Tutorial**subnet.Note

It may take several minutes to enable the service endpoint.

The

*Access Restrictions*page now shows that there is a new restriction. It may take a few seconds for the*Endpoint status*to change from Disabled through Provisioning to Enabled.Important

Each function app has an

[Advanced Tool (Kudu) site](../app-service/app-service-ip-restrictions#restrict-access-to-an-scm-site)that is used to manage function app deployments. This site is accessed from a URL like:`<FUNCTION_APP_NAME>.scm.azurewebsites.net`

. Enabling access restrictions on the Kudu site prevents the deployment of the project code from a local developer workstation, and then an agent is needed within the virtual network to perform the deployment.

## Access the functions app

Return to the previously created function app. In the

*Overview*section, copy the URL.If you try to access the function app now from your computer outside of your virtual network, you'll receive an HTTP 403 page indicating that access is forbidden.

Return to the resource group and select the previously created virtual machine. In order to access the site from the VM, you need to connect to the VM via the Azure Bastion service.

Select

**Connect**and then choose**Bastion**.Provide the required username and password to log into the virtual machine.

Note

For enhanced security, you should require Microsoft Entra authentication to access your virtual machines in Azure.

Select

**Connect**. A new browser window will pop up to allow you to interact with the virtual machine. It's possible to access the site from the web browser on the VM because the VM is accessing the site through the virtual network. While the site is only accessible from within the designated virtual network, a public DNS entry remains.

## Create a function

The next step in this tutorial is to create an HTTP-triggered Azure Function. Invoking the function via an HTTP GET or POST should result in a response of "Hello, {name}".

Follow one of the following quickstarts to create and deploy your Azure Functions app.

When publishing your Azure Functions project, choose the function app resource that you created earlier in this tutorial.

Verify the function is deployed.


## Invoke the function directly

In order to test access to the function, you need to copy the function URL. Select the deployed function, and then select

**Get Function Url**. Then click the**Copy**button to copy the URL to your clipboard.Paste the URL into a web browser. When you now try to access the function app from a computer outside of your virtual network, you receive an HTTP 403 response indicating access to the app is forbidden.


## Invoke the function from the virtual network

Accessing the function via a web browser (by using the Azure Bastion service) on the configured VM on the virtual network results in success!

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-trigger -->

# Azure Cosmos DB trigger for Azure Functions 2.x and higher

The Azure Cosmos DB Trigger uses the [Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed) to listen for inserts and updates across partitions. The change feed publishes new and updated items, not including updates from deletions. For an end-to-end scenario that uses the Azure Cosmos DB trigger, see [Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions](scenario-database-changes-azure-cosmosdb).

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Cosmos DB scaling decisions for the Consumption and Premium plans are done via target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

This article supports both programming models.

## Example

The usage of the trigger depends on the extension package version and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

An in-process class library is a compiled C# function runs in the same process as the Functions runtime.

The following examples depend on the extension version for the given C# mode.

Apps using [Azure Cosmos DB extension version 4.x](functions-bindings-cosmosdb-v2?tabs=extensionv4) or higher have different attribute properties, which are shown here. This example refers to a simple `ToDoItem`

type.

```
namespace CosmosDBSamplesV2
{
// Customize the model with your own desired properties
public class ToDoItem
{
public string id { get; set; }
public string Description { get; set; }
}
}
```


```
using System.Collections.Generic;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using Microsoft.Extensions.Logging;
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "databaseName",
containerName: "containerName",
Connection = "CosmosDBConnectionSetting",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)]IReadOnlyList<ToDoItem> input, ILogger log)
{
if (input != null && input.Count > 0)
{
log.LogInformation("Documents modified " + input.Count);
log.LogInformation("First document Id " + input[0].id);
}
}
}
}
```


The following example shows a [C# function](functions-dotnet-class-library) that is invoked when there are inserts or updates in the specified database and collection.

```
using Microsoft.Azure.Documents;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using Microsoft.Extensions.Logging;
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
LeaseCollectionName = "leases",
CreateLeaseCollectionIfNotExists = true)]IReadOnlyList<Document> documents,
ILogger log)
{
if (documents != null && documents.Count > 0)
{
log.LogInformation($"Documents modified: {documents.Count}");
log.LogInformation($"First document Id: {documents[0].Id}");
}
}
}
}
```


This example refers to a simple `ToDoItem`

type:

```
public class ToDoItem
{
public string? Id { get; set; }
public string? Description { get; set; }
}
```


The following function is invoked when there are inserts or updates in the specified database and collection.

```
[Function("CosmosTrigger")]
public void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
containerName:"TriggerItems",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<ToDoItem> todoItems,
FunctionContext context)
{
if (todoItems is not null && todoItems.Any())
{
foreach (var doc in todoItems)
{
_logger.LogInformation("ToDoItem: {desc}", doc.Description);
}
}
}
```


The following code defines a `MyDocument`

type:

```
public class MyDocument
{
public string? Id { get; set; }
public string? Text { get; set; }
public int Number { get; set; }
public bool Boolean { get; set; }
}
```


An `IReadOnlyList<T>`

is used as the Azure Cosmos DB trigger binding parameter in the following example:

```
[Function(nameof(CosmosDBFunction))]
[ExponentialBackoffRetry(5, "00:00:04", "00:15:00")]
[CosmosDBOutput("%CosmosDb%", "%CosmosContainerOut%", Connection = "CosmosDBConnection", CreateIfNotExists = true)]
public object? Run(
[CosmosDBTrigger(
"%CosmosDb%",
"%CosmosContainerIn%",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<MyDocument> input,
FunctionContext context)
{
if (input != null && input.Any())
{
foreach (var doc in input)
{
_logger.LogInformation("Doc Id: {id}", doc.Id);
}
// Cosmos Output
return input.Select(p => new { id = p.Id });
}
return null;
}
```


This example requires the following `using`

statements:

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
```


This function is invoked when there are inserts or updates in the specified database and container.

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

```
@FunctionName("CosmosDBTriggerFunction")
public void run(
@CosmosDBTrigger(
name = "items",
databaseName = "ToDoList",
containerName = "Items",
leaseContainerName="leases",
connection = "AzureCosmosDBConnection",
createLeaseContainerIfNotExists = true
)
Object inputItem,
final ExecutionContext context
) {
context.getLogger().info("Items modified: " + inputItems.size());
}
```


```
@FunctionName("cosmosDBMonitor")
public void cosmosDbProcessor(
@CosmosDBTrigger(name = "items",
databaseName = "ToDoList",
collectionName = "Items",
leaseCollectionName = "leases",
createLeaseCollectionIfNotExists = true,
connectionStringSetting = "AzureCosmosDBConnection") String[] items,
final ExecutionContext context ) {
context.getLogger().info(items.length + "item(s) is/are changed.");
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger`

annotation on parameters whose value would come from Azure Cosmos DB. This annotation can be used with native Java types, plain-old Java objects (POJOs), or nullable values using `Optional<T>`

.

The following example shows an Azure Cosmos DB trigger [TypeScript function](functions-reference-node?tabs=typescript). The function writes log messages when Azure Cosmos DB records are added or modified.

```
import { app, InvocationContext } from '@azure/functions';
export async function cosmosDBTrigger1(documents: unknown[], context: InvocationContext): Promise<void> {
context.log(`Cosmos DB function processed ${documents.length} documents`);
}
app.cosmosDB('cosmosDBTrigger1', {
connection: '<connection-app-setting>',
databaseName: 'Tasks',
containerName: 'Items',
createLeaseContainerIfNotExists: true,
handler: cosmosDBTrigger1,
});
```


TypeScript samples aren't documented for model v3.

The following example shows an Azure Cosmos DB trigger [JavaScript function](functions-reference-node). The function writes log messages when Azure Cosmos DB records are added or modified.

```
const { app } = require('@azure/functions');
app.cosmosDB('cosmosDBTrigger1', {
connection: '<connection-app-setting>',
databaseName: 'Tasks',
containerName: 'Items',
createLeaseContainerIfNotExists: true,
handler: (documents, context) => {
context.log(`Cosmos DB function processed ${documents.length} documents`);
},
});
```


The following example shows an Azure Cosmos DB trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding. The function writes log messages when Azure Cosmos DB records are added or modified.

Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

Here's the JavaScript code:

```
module.exports = async function (context, documents) {
context.log('First document Id modified : ', documents[0].id);
}
```


The following example shows how to run a function as data changes in Azure Cosmos DB.

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

In the *run.ps1* file, you have access to the document that triggers the function via the `$Documents`

parameter.

```
param($Documents, $TriggerMetadata)
Write-Host "First document Id modified : $($Documents[0].id)"
```


The following example shows an Azure Cosmos DB trigger binding. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="CosmosDBTrigger")
@app.cosmos_db_trigger(arg_name="documents",
connection="CONNECTION_SETTING",
database_name="DB_NAME",
container_name="CONTAINER_NAME",
lease_container_name="leases",
create_lease_container_if_not_exists="true")
def test_function(documents: func.DocumentList) -> str:
if documents:
logging.info('Document id: %s', documents[0]['id'])
```


The function writes log messages when Azure Cosmos DB records are modified. Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

Here's the Python code:

```
import logging
import azure.functions as func
def main(documents: func.DocumentList) -> str:
if documents:
logging.info('First document Id modified: %s', documents[0]['id'])
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated process](dotnet-isolated-process-guide) C# libraries use `CosmosDBTriggerAttribute`

to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-trigger).

The specific properties depends both on the process model and the extension version:

In-process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.WebJobs`

namespace, which defines these properties:

| Attribute property |
Description |
**Connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**ContainerName** |
The name of the container being monitored. |
**LeaseConnection** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**CreateLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**LeasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**StartFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

In-process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.WebJobs`

namespace, which defines these properties:

| Attribute property |
Description |
**ConnectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**CollectionName** |
The name of the collection being monitored. |
**LeaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `ConnectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**CreateLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**LeasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `CreateLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**CheckpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**CheckpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**UseMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |
**UseDefaultJsonSerialization** |
(Optional) Lets you use `JsonConvert.DefaultSettings` in the monitored collection. This setting only applies to the monitored collection and the consumer to setup the serialization used in the monitored collection. The `JsonConvert.DefaultSettings` must be set in a class derived from `CosmosDBWebJobsStartup` . |

Isolated worker process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.CosmosDB/src/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.Functions.Worker`

namespace, which defines these properties:

| Attribute property |
Description |
**Connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**ContainerName** |
The name of the container being monitored. |
**LeaseConnection** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**CreateLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**LeasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**StartFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

Isolated worker process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.CosmosDB/src/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.Functions.Worker`

namespace, which defines these properties:.

| Attribute property |
Description |
**ConnectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**CollectionName** |
The name of the collection being monitored. |
**LeaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `ConnectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**CreateLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**LeasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `CreateLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**CheckpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**CheckpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**UseMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |
**UseDefaultJsonSerialization** |
(Optional) Lets you use `JsonConvert.DefaultSettings` in the monitored collection. This setting only applies to the monitored collection and the consumer to setup the serialization used in the monitored collection. The `JsonConvert.DefaultSettings` must be set in a class derived from `CosmosDBWebJobsStartup` . |

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `cosmos_db_trigger`

:

| Property |
Description |
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the container being monitored. |
`container_name` |
The name of the Azure Cosmos DB container being monitored. |
`connection` |
The connection string of the Azure Cosmos DB being monitored. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

Use the `@CosmosDBTrigger`

annotation on parameters that read data from Azure Cosmos DB. The annotation supports the following properties:

| Attribute property |
Description |
**connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**name** |
The name of the function. |
**databaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**containerName** |
The name of the container being monitored. |
**leaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**createLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers isn't [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#nondata-operations-arent-allowed) and your function app isn't allowed to start. |
**leasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease isn't renewed within this interval, it expires and ownership of the partition moves to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renewal interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, `East US,South Central US,North Europe` . |

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger`

annotation on parameters that read data from Azure Cosmos DB. The annotation supports the following properties:


## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.cosmosDB()`

method. The `type`

, `direction`

, and `name`

properties don't apply to the v4 model.

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property |
Description |
**type** |
Must be set to `cosmosDBTrigger` . |
**direction** |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
**name** |
The variable name used in function code that represents the list of documents with changes. |
**connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](functions-bindings-cosmosdb-v2-trigger#connections). |
**databaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**containerName** |
The name of the container being monitored. |
**leaseConnection** |
(Optional) The name of an app setting or setting container that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**createLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**leasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `createLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**startFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

| function.json property |
Description |
**type** |
Must be set to `cosmosDBTrigger` . |
**direction** |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
**name** |
The variable name used in function code that represents the list of documents with changes. |
**connectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**databaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**collectionName** |
The name of the collection being monitored. |
**leaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `connectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**createLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**leasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `createLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**checkpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**checkpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**useMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |

See the [Example section](#example) for complete examples.

## Usage

The trigger requires a second collection that it uses to store *leases* over the partitions. Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `LeaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Attributes section](#attributes).

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `leaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Annotations section](#annotations).

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `leaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Configuration section](#configuration).

The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself. If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.

The parameter type supported by the Azure Cosmos DB trigger depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single document, the Cosmos DB trigger can bind to the following types:

| Type |
Description |
| JSON serializable types |
Functions tries to deserialize the JSON data of the document from the Cosmos DB change feed into a plain-old CLR object (POCO) type. |

When you want the function to process a batch of documents, the Cosmos DB trigger can bind to the following types:

| Type |
Description |
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities included in the batch. Each entry represents one document from the Cosmos DB change feed. |

## Connections

The `connectionStringSetting`

/`connection`

and `leaseConnectionStringSetting`

/`leaseConnection`

properties are references to environment configuration which specifies how the app should connect to Azure Cosmos DB. They may specify:

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

The connection string for your database account should be stored in an application setting with a name matching the value specified by the connection property of the binding configuration.

### Identity-based connections

If you are using [version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the connection property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property |
Environment variable template |
Description |
Example value |
| Account Endpoint |
`<CONNECTION_NAME_PREFIX>__accountEndpoint` |
The Azure Cosmos DB account endpoint URI. |
https://<database_account_name>.documents.azure.com:443/ |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Cosmos DB does not use Azure RBAC for data operations. Instead, it uses a [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) which is built on similar concepts. You will need to create a role assignment that provides access to your database account at runtime. Azure RBAC Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Azure Cosmos DB extension in normal operation. Your application may require additional permissions based on the code you write.

1 These roles cannot be used in an Azure RBAC role assignment. See the [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) documentation for details on how to assign these roles.

2 When using identity, Cosmos DB treats container creation as a management operation. It is not available as a data-plane operation for the trigger. You will need to ensure that you create the containers needed by the trigger (including the lease container) before setting up your function.

## Next steps

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-trigger -->

# Azure Cosmos DB trigger for Azure Functions 2.x and higher

The Azure Cosmos DB Trigger uses the [Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed) to listen for inserts and updates across partitions. The change feed publishes new and updated items, not including updates from deletions. For an end-to-end scenario that uses the Azure Cosmos DB trigger, see [Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions](scenario-database-changes-azure-cosmosdb).

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Cosmos DB scaling decisions for the Consumption and Premium plans are done via target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

This article supports both programming models.

## Example

The usage of the trigger depends on the extension package version and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

An in-process class library is a compiled C# function runs in the same process as the Functions runtime.

The following examples depend on the extension version for the given C# mode.

Apps using [Azure Cosmos DB extension version 4.x](functions-bindings-cosmosdb-v2?tabs=extensionv4) or higher have different attribute properties, which are shown here. This example refers to a simple `ToDoItem`

type.

```
namespace CosmosDBSamplesV2
{
// Customize the model with your own desired properties
public class ToDoItem
{
public string id { get; set; }
public string Description { get; set; }
}
}
```


```
using System.Collections.Generic;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using Microsoft.Extensions.Logging;
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "databaseName",
containerName: "containerName",
Connection = "CosmosDBConnectionSetting",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)]IReadOnlyList<ToDoItem> input, ILogger log)
{
if (input != null && input.Count > 0)
{
log.LogInformation("Documents modified " + input.Count);
log.LogInformation("First document Id " + input[0].id);
}
}
}
}
```


The following example shows a [C# function](functions-dotnet-class-library) that is invoked when there are inserts or updates in the specified database and collection.

```
using Microsoft.Azure.Documents;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using Microsoft.Extensions.Logging;
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
LeaseCollectionName = "leases",
CreateLeaseCollectionIfNotExists = true)]IReadOnlyList<Document> documents,
ILogger log)
{
if (documents != null && documents.Count > 0)
{
log.LogInformation($"Documents modified: {documents.Count}");
log.LogInformation($"First document Id: {documents[0].Id}");
}
}
}
}
```


This example refers to a simple `ToDoItem`

type:

```
public class ToDoItem
{
public string? Id { get; set; }
public string? Description { get; set; }
}
```


The following function is invoked when there are inserts or updates in the specified database and collection.

```
[Function("CosmosTrigger")]
public void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
containerName:"TriggerItems",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<ToDoItem> todoItems,
FunctionContext context)
{
if (todoItems is not null && todoItems.Any())
{
foreach (var doc in todoItems)
{
_logger.LogInformation("ToDoItem: {desc}", doc.Description);
}
}
}
```


The following code defines a `MyDocument`

type:

```
public class MyDocument
{
public string? Id { get; set; }
public string? Text { get; set; }
public int Number { get; set; }
public bool Boolean { get; set; }
}
```


An `IReadOnlyList<T>`

is used as the Azure Cosmos DB trigger binding parameter in the following example:

```
[Function(nameof(CosmosDBFunction))]
[ExponentialBackoffRetry(5, "00:00:04", "00:15:00")]
[CosmosDBOutput("%CosmosDb%", "%CosmosContainerOut%", Connection = "CosmosDBConnection", CreateIfNotExists = true)]
public object? Run(
[CosmosDBTrigger(
"%CosmosDb%",
"%CosmosContainerIn%",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<MyDocument> input,
FunctionContext context)
{
if (input != null && input.Any())
{
foreach (var doc in input)
{
_logger.LogInformation("Doc Id: {id}", doc.Id);
}
// Cosmos Output
return input.Select(p => new { id = p.Id });
}
return null;
}
```


This example requires the following `using`

statements:

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
```


This function is invoked when there are inserts or updates in the specified database and container.

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

```
@FunctionName("CosmosDBTriggerFunction")
public void run(
@CosmosDBTrigger(
name = "items",
databaseName = "ToDoList",
containerName = "Items",
leaseContainerName="leases",
connection = "AzureCosmosDBConnection",
createLeaseContainerIfNotExists = true
)
Object inputItem,
final ExecutionContext context
) {
context.getLogger().info("Items modified: " + inputItems.size());
}
```


```
@FunctionName("cosmosDBMonitor")
public void cosmosDbProcessor(
@CosmosDBTrigger(name = "items",
databaseName = "ToDoList",
collectionName = "Items",
leaseCollectionName = "leases",
createLeaseCollectionIfNotExists = true,
connectionStringSetting = "AzureCosmosDBConnection") String[] items,
final ExecutionContext context ) {
context.getLogger().info(items.length + "item(s) is/are changed.");
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger`

annotation on parameters whose value would come from Azure Cosmos DB. This annotation can be used with native Java types, plain-old Java objects (POJOs), or nullable values using `Optional<T>`

.

The following example shows an Azure Cosmos DB trigger [TypeScript function](functions-reference-node?tabs=typescript). The function writes log messages when Azure Cosmos DB records are added or modified.

```
import { app, InvocationContext } from '@azure/functions';
export async function cosmosDBTrigger1(documents: unknown[], context: InvocationContext): Promise<void> {
context.log(`Cosmos DB function processed ${documents.length} documents`);
}
app.cosmosDB('cosmosDBTrigger1', {
connection: '<connection-app-setting>',
databaseName: 'Tasks',
containerName: 'Items',
createLeaseContainerIfNotExists: true,
handler: cosmosDBTrigger1,
});
```


TypeScript samples aren't documented for model v3.

The following example shows an Azure Cosmos DB trigger [JavaScript function](functions-reference-node). The function writes log messages when Azure Cosmos DB records are added or modified.

```
const { app } = require('@azure/functions');
app.cosmosDB('cosmosDBTrigger1', {
connection: '<connection-app-setting>',
databaseName: 'Tasks',
containerName: 'Items',
createLeaseContainerIfNotExists: true,
handler: (documents, context) => {
context.log(`Cosmos DB function processed ${documents.length} documents`);
},
});
```


The following example shows an Azure Cosmos DB trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding. The function writes log messages when Azure Cosmos DB records are added or modified.

Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

Here's the JavaScript code:

```
module.exports = async function (context, documents) {
context.log('First document Id modified : ', documents[0].id);
}
```


The following example shows how to run a function as data changes in Azure Cosmos DB.

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

In the *run.ps1* file, you have access to the document that triggers the function via the `$Documents`

parameter.

```
param($Documents, $TriggerMetadata)
Write-Host "First document Id modified : $($Documents[0].id)"
```


The following example shows an Azure Cosmos DB trigger binding. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="CosmosDBTrigger")
@app.cosmos_db_trigger(arg_name="documents",
connection="CONNECTION_SETTING",
database_name="DB_NAME",
container_name="CONTAINER_NAME",
lease_container_name="leases",
create_lease_container_if_not_exists="true")
def test_function(documents: func.DocumentList) -> str:
if documents:
logging.info('Document id: %s', documents[0]['id'])
```


The function writes log messages when Azure Cosmos DB records are modified. Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

Here's the Python code:

```
import logging
import azure.functions as func
def main(documents: func.DocumentList) -> str:
if documents:
logging.info('First document Id modified: %s', documents[0]['id'])
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated process](dotnet-isolated-process-guide) C# libraries use `CosmosDBTriggerAttribute`

to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-trigger).

The specific properties depends both on the process model and the extension version:

In-process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.WebJobs`

namespace, which defines these properties:

| Attribute property |
Description |
**Connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**ContainerName** |
The name of the container being monitored. |
**LeaseConnection** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**CreateLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**LeasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**StartFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

In-process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.WebJobs`

namespace, which defines these properties:

| Attribute property |
Description |
**ConnectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**CollectionName** |
The name of the collection being monitored. |
**LeaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `ConnectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**CreateLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**LeasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `CreateLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**CheckpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**CheckpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**UseMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |
**UseDefaultJsonSerialization** |
(Optional) Lets you use `JsonConvert.DefaultSettings` in the monitored collection. This setting only applies to the monitored collection and the consumer to setup the serialization used in the monitored collection. The `JsonConvert.DefaultSettings` must be set in a class derived from `CosmosDBWebJobsStartup` . |

Isolated worker process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.CosmosDB/src/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.Functions.Worker`

namespace, which defines these properties:

| Attribute property |
Description |
**Connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**ContainerName** |
The name of the container being monitored. |
**LeaseConnection** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**CreateLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**LeasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**StartFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

Isolated worker process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.CosmosDB/src/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.Functions.Worker`

namespace, which defines these properties:.

| Attribute property |
Description |
**ConnectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**CollectionName** |
The name of the collection being monitored. |
**LeaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `ConnectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**CreateLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**LeasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `CreateLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**CheckpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**CheckpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**UseMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |
**UseDefaultJsonSerialization** |
(Optional) Lets you use `JsonConvert.DefaultSettings` in the monitored collection. This setting only applies to the monitored collection and the consumer to setup the serialization used in the monitored collection. The `JsonConvert.DefaultSettings` must be set in a class derived from `CosmosDBWebJobsStartup` . |

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `cosmos_db_trigger`

:

| Property |
Description |
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the container being monitored. |
`container_name` |
The name of the Azure Cosmos DB container being monitored. |
`connection` |
The connection string of the Azure Cosmos DB being monitored. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

Use the `@CosmosDBTrigger`

annotation on parameters that read data from Azure Cosmos DB. The annotation supports the following properties:

| Attribute property |
Description |
**connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**name** |
The name of the function. |
**databaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**containerName** |
The name of the container being monitored. |
**leaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**createLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers isn't [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#nondata-operations-arent-allowed) and your function app isn't allowed to start. |
**leasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease isn't renewed within this interval, it expires and ownership of the partition moves to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renewal interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, `East US,South Central US,North Europe` . |

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger`

annotation on parameters that read data from Azure Cosmos DB. The annotation supports the following properties:


## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.cosmosDB()`

method. The `type`

, `direction`

, and `name`

properties don't apply to the v4 model.

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property |
Description |
**type** |
Must be set to `cosmosDBTrigger` . |
**direction** |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
**name** |
The variable name used in function code that represents the list of documents with changes. |
**connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](functions-bindings-cosmosdb-v2-trigger#connections). |
**databaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**containerName** |
The name of the container being monitored. |
**leaseConnection** |
(Optional) The name of an app setting or setting container that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**createLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**leasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `createLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**startFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

| function.json property |
Description |
**type** |
Must be set to `cosmosDBTrigger` . |
**direction** |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
**name** |
The variable name used in function code that represents the list of documents with changes. |
**connectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**databaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**collectionName** |
The name of the collection being monitored. |
**leaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `connectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**createLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**leasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `createLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**checkpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**checkpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**useMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |

See the [Example section](#example) for complete examples.

## Usage

The trigger requires a second collection that it uses to store *leases* over the partitions. Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `LeaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Attributes section](#attributes).

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `leaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Annotations section](#annotations).

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `leaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Configuration section](#configuration).

The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself. If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.

The parameter type supported by the Azure Cosmos DB trigger depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single document, the Cosmos DB trigger can bind to the following types:

| Type |
Description |
| JSON serializable types |
Functions tries to deserialize the JSON data of the document from the Cosmos DB change feed into a plain-old CLR object (POCO) type. |

When you want the function to process a batch of documents, the Cosmos DB trigger can bind to the following types:

| Type |
Description |
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities included in the batch. Each entry represents one document from the Cosmos DB change feed. |

## Connections

The `connectionStringSetting`

/`connection`

and `leaseConnectionStringSetting`

/`leaseConnection`

properties are references to environment configuration which specifies how the app should connect to Azure Cosmos DB. They may specify:

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

The connection string for your database account should be stored in an application setting with a name matching the value specified by the connection property of the binding configuration.

### Identity-based connections

If you are using [version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the connection property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property |
Environment variable template |
Description |
Example value |
| Account Endpoint |
`<CONNECTION_NAME_PREFIX>__accountEndpoint` |
The Azure Cosmos DB account endpoint URI. |
https://<database_account_name>.documents.azure.com:443/ |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Cosmos DB does not use Azure RBAC for data operations. Instead, it uses a [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) which is built on similar concepts. You will need to create a role assignment that provides access to your database account at runtime. Azure RBAC Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Azure Cosmos DB extension in normal operation. Your application may require additional permissions based on the code you write.

1 These roles cannot be used in an Azure RBAC role assignment. See the [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) documentation for details on how to assign these roles.

2 When using identity, Cosmos DB treats container creation as a management operation. It is not available as a data-plane operation for the trigger. You will need to ensure that you create the containers needed by the trigger (including the lease container) before setting up your function.

## Next steps

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/run-functions-from-deployment-package -->

# Run your functions from a package file in Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure, you can run your functions directly from a deployment package file in your function app. The other option is to deploy your files in the `c:\home\site\wwwroot`

(Windows) or `/home/site/wwwroot`

(Linux) directory of your function app.

This article describes the benefits of running your functions from a package. It also shows how to enable this functionality in your function app.

## Benefits of running from a package file

There are several benefits to running functions from a package file:

- Reduces the risk of file copy locking issues.
- Can be deployed to a production app (with restart).
- Verifies the files that are running in your app.
- Improves the performance of
[Azure Resource Manager deployments](functions-infrastructure-as-code). - Reduces cold-start times, particularly for JavaScript functions with large npm package trees.

For more information, see [this announcement](https://github.com/Azure/app-service-announcements/issues/84).

## Enable functions to run from a package

Function apps on the [Flex Consumption](flex-consumption-plan) hosting plan run from a package by default. No special configuration needs to be done.

To enable your function app to run from a package on the [Consumption](consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) hosting plans, add a `WEBSITE_RUN_FROM_PACKAGE`

app setting to your function app. The `WEBSITE_RUN_FROM_PACKAGE`

app setting can have one of the following values:

| Value | Description |
|---|---|
`1` |
Indicates that the function app runs from a local package file deployed in the `c:\home\data\SitePackages` (Windows) or `/home/data/SitePackages` (Linux) folder of your function app. |
`<URL>` |
Sets a URL that is the remote location of the specific package file you want to run. Required for functions apps running on Linux in a Consumption plan. |

The following table indicates the recommended `WEBSITE_RUN_FROM_PACKAGE`

values for deployment to a specific operating system and hosting plan:

| Hosting plan | Windows | Linux |
|---|---|---|
|

`1`

is highly recommended.`<URL>`

is supported.[Premium](functions-premium-plan)`1`

is recommended.`1`

is recommended.[Dedicated](dedicated-plan)`1`

is recommended.`1`

is recommended.## General considerations

- Do not add the
`WEBSITE_RUN_FROM_PACKAGE`

app setting to apps on the[Flex Consumption](flex-consumption-plan)plan. - The package file must be .zip formatted. Tar and gzip formats aren't supported.
[Zip deployment](#integration-with-zip-deployment)is recommended.- When deploying your function app to Windows, you should set
`WEBSITE_RUN_FROM_PACKAGE`

to`1`

and publish with zip deployment. - When you run from a package, the
`wwwroot`

folder is read-only and you receive an error if you write files to this directory. Files are also read-only in the Azure portal. - The maximum size for a deployment package file is 1 GB.
- The deployment uses temporary storage when unpacking your project files. This means that your function app must have enough available temporary storage space to hold the contents of your package. Keep in mind that the temporary storage limit for a Consumption plan is
[500 MB per plan](functions-scale#service-limits). To learn about how to troubleshoot issues with temporary storage, see[How to troubleshoot temporary storage on Azure App Service](/en-us/troubleshoot/azure/app-service/temporary-storage-for-azure-app-service).

- The deployment uses temporary storage when unpacking your project files. This means that your function app must have enough available temporary storage space to hold the contents of your package. Keep in mind that the temporary storage limit for a Consumption plan is
- You can't use the local cache when running from a deployment package.
- If your project needs to use remote build, don't use the
`WEBSITE_RUN_FROM_PACKAGE`

app setting. Instead, add the`SCM_DO_BUILD_DURING_DEPLOYMENT=true`

deployment customization app setting. For Linux, also add the`ENABLE_ORYX_BUILD=true`

setting. For more information, see[Remote build](functions-deployment-technologies#remote-build).

Note

The `WEBSITE_RUN_FROM_PACKAGE`

app setting does not work with MSDeploy as described in [MSDeploy VS. ZipDeploy](https://github.com/projectkudu/kudu/wiki/MSDeploy-VS.-ZipDeploy). You will receive an error during deployment, such as `ARM-MSDeploy Deploy Failed`

. To resolve this error, change `/MSDeploy`

to `/ZipDeploy`

.

### Add the WEBSITE_RUN_FROM_PACKAGE setting

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

### Creating the zip archive

The zip archive you deploy must contain all of the files needed to run your function app. You can manually create a zip archive from the contents of a Functions project folder using built-in .zip compression functionality or non-Microsoft tools.

The archive must include the [host.json](functions-host-json) file at the root of the extracted folder. The selected language stack for the function app creates other requirements:

Important

For languages that generate compiled output for deployment, make sure to compress the contents of the output folder you plan to publish and not the entire project folder. When Functions extracts the contents of the zip archive, the `host.json`

file must exist in the root of the package.

## Use WEBSITE_RUN_FROM_PACKAGE = 1

This section provides information about how to run your function app from a local package file.

### Considerations for deploying from an on-site package

- Using an on-site package is the recommended option for running from the deployment package, except when running on Linux hosted in a Consumption plan.
[Zip deployment](#integration-with-zip-deployment)is the recommended way to upload a deployment package to your site.- When not using zip deployment, make sure the
`c:\home\data\SitePackages`

(Windows) or`/home/data/SitePackages`

(Linux) folder has a file named`packagename.txt`

. This file contains only the name, without any whitespace, of the package file in this folder that's currently running.

### Integration with zip deployment

Zip deployment is a feature of Azure App Service that lets you deploy your function app project to the `wwwroot`

directory. The project is packaged as a .zip deployment file. The same APIs can be used to deploy your package to the `c:\home\data\SitePackages`

(Windows) or `/home/data/SitePackages`

(Linux) folder.

When you set the `WEBSITE_RUN_FROM_PACKAGE`

app setting value to `1`

, the zip deployment APIs copy your package to the `c:\home\data\SitePackages`

(Windows) or `/home/data/SitePackages`

(Linux) folder instead of extracting the files to `c:\home\site\wwwroot`

(Windows) or `/home/site/wwwroot`

(Linux). It also creates the `packagename.txt`

file. After your function app is automatically restarted, the package is mounted to `wwwroot`

as a read-only filesystem. For more information about zip deployment, see [Zip deployment for Azure Functions](deployment-zip-push).

Note

When a deployment occurs, a restart of the function app is triggered. Function executions currently running during the deploy are terminated. For information about how to write stateless and defensive functions, sett [Write functions to be stateless](performance-reliability#write-functions-to-be-stateless).

## Use WEBSITE_RUN_FROM_PACKAGE = URL

This section provides information about how to run your function app from a package deployed to a URL endpoint. This option is the only one supported for running from a Linux-hosted package with a Consumption plan. This option is not supported in the [Flex Consumption](flex-consumption-plan) plan.

### Considerations for deploying from a URL

- Do not set
`WEBSITE_RUN_FROM_PACKAGE = <URL>`

in apps on the[Flex Consumption](flex-consumption-plan)plan. This option is not supported. - Function apps running on Windows experience a slight increase in
[cold-start time](event-driven-scaling#cold-start)when the application package is deployed to a URL endpoint via`WEBSITE_RUN_FROM_PACKAGE = <URL>`

. - When you specify a URL, you must also
[manually sync triggers](functions-deployment-technologies#trigger-syncing)after you publish an updated package. - The Functions runtime must have permissions to access the package URL.
- Don't deploy your package to Azure Blob Storage as a public blob. Instead, use a private container with a
[shared access signature (SAS)](../storage/common/storage-sas-overview)or[use a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity)to enable the Functions runtime to access the package. - You must maintain any SAS URLs used for deployment. When an SAS expires, the package can no longer be deployed. In this case, you must generate a new SAS and update the setting in your function app. You can eliminate this management burden by
[using a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity). - When running on a Premium plan, make sure to
[eliminate cold starts](functions-premium-plan#eliminate-cold-starts). - When you're running on a Dedicated plan, ensure you enable
[Always On](dedicated-plan#always-on). - You can use
[Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer)to upload package files to blob containers in your storage account.

### Manually uploading a package to Blob Storage

To deploy a zipped package when using the URL option, you must create a .zip compressed deployment package and upload it to the destination. The following procedure deploys to a container in Blob Storage:

Create a .zip package for your project using the utility of your choice.

In the

[Azure portal](https://portal.azure.com), search for your storage account name or browse for it in the storage accounts list.In the storage account, select

**Containers**under**Data storage**.Select

**+ Container**to create a new Blob Storage container in your account.In the

**New container**page, provide a**Name**(for example,*deployments*), ensure the**Anonymous access level**is**Private**, and then select**Create**.Select the container you created, select

**Upload**, browse to the location of the .zip file you created with your project, and then select**Upload**.After the upload completes, choose your uploaded blob file, and copy the URL. If you aren't

[using a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity), you might need to generate a SAS URL.Search for your function app or browse for it in the

**Function App**page.In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select**+ Add**.Enter the value

`WEBSITE_RUN_FROM_PACKAGE`

for the**Name**, and paste the URL of your package in Blob Storage for the**Value**.Select

**Apply**, and then select**Apply**and**Confirm**to save the setting and restart the function app.

Now you can run your function in Azure to verify that deployment of the deployment package .zip file was successful.

### Fetch a package from Azure Blob Storage using a managed identity

You can configure Azure Blob Storage to [authorize requests with Microsoft Entra ID](/en-us/azure/storage/blobs/authorize-access-azure-active-directory?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). This configuration means that instead of generating a SAS key with an expiration, you can instead rely on the application's [managed identity](/en-us/azure/app-service/overview-managed-identity). By default, the app's system-assigned identity is used. If you wish to specify a user-assigned identity, you can set the `WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID`

app setting to the resource ID of that identity. The setting can also accept `SystemAssigned`

as a value, which is equivalent to omitting the setting.

To enable the package to be fetched using the identity:

Ensure that the blob is

[configured for private access](/en-us/azure/storage/blobs/anonymous-read-access-configure#set-the-anonymous-access-level-for-a-container).Grant the identity the

[Storage Blob Data Reader](/en-us/azure/role-based-access-control/built-in-roles#storage-blob-data-reader)role with scope over the package blob. See[Assign an Azure role for access to blob data](/en-us/azure/storage/blobs/assign-azure-role-data-access)for details on creating the role assignment.Set the

`WEBSITE_RUN_FROM_PACKAGE`

application setting to the blob URL of the package. This URL is usually of the form`https://{storage-account-name}.blob.core.windows.net/{container-name}/{path-to-package}`

or similar.If you wish to specify a user-assigned identity, you can set the

`WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID`

app setting to the resource ID of that identity. The setting can also accept "SystemAssigned" as a value, although this is the same as omitting the setting altogether. A resource ID is a standard representation for a resource in Azure. For a user-assigned managed identity, that is going to be`/subscriptions/subid/resourcegroups/rg-name/providers/Microsoft.ManagedIdentity/userAssignedIdentities/identity-name`

. The resource ID of a user-assigned managed identity can be obtained in the**Settings**->**Properties**->**ID for the user assigned managed identity**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-errors -->

# Azure Functions error handling and retries

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Handling errors in Azure Functions helps you avoid lost data, avoid missed events, and monitor the health of your application. It's also an important way to help you understand the retry behaviors of event-based triggers.

This article describes general strategies for error handling and the available retry strategies.

Important

The preview of retry policy support for certain triggers was removed in December 2022. Retry policies for supported triggers are now in general availability (GA). The [Retries](#retries) section of this article lists extensions that currently support retry policies.

## Handling errors

Errors that occur in an Azure function can come from:

- Use of built-in Azure Functions
[triggers and bindings](functions-triggers-bindings). - Calls to APIs of underlying Azure services.
- Calls to REST endpoints.
- Calls to client libraries, packages, or non-Microsoft APIs.

To avoid loss of data or missed messages, you should practice good error handling. This table describes some recommended error-handling practices and provides links to more information:

| Recommendation | Details |
|---|---|
| Enable Application Insights | Azure Functions integrates with Application Insights to collect error data, performance data, and runtime logs. Use Application Insights to discover and better understand errors that occur in your function executions. To learn more, see
|

[Binding error codes](#binding-error-codes)in this article. Depending on your specific retry strategy, you might also raise a new exception to run the function again.[Retries](#retries)in this article.[Designing Azure Functions for identical input](functions-idempotent).Tip

When you use output bindings, you can't handle errors that occur from accessing the remote service. Because of this behavior, you should validate all data passed to your output bindings to avoid raising any known exceptions. If you must be able to handle such exceptions in your function code, you should access the remote service by using the client SDK instead of relying on output bindings.

## Retries

Two kinds of retries are available for your functions:

- Built-in retry behaviors of individual trigger extensions
- Retry policies that the Azure Functions runtime provides

The following table indicates which triggers support retries and where the retry behavior is configured. It also links to more information about errors that come from the underlying services.

| Trigger/binding | Retry source | Configuration |
|---|---|---|
| Azure Cosmos DB |
|

[Binding extension](functions-bindings-storage-blob-trigger#poison-blobs)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](../event-grid/delivery-and-retry)[Retry policies](#retry-policies)[Retry policies](#retry-policies)[Binding extension](functions-bindings-storage-queue-trigger#poison-messages)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](functions-bindings-rabbitmq-trigger#dead-letter-queues)[Dead letter queue](https://www.rabbitmq.com/dlx.html)[Binding extension](functions-bindings-service-bus-trigger)[host.json](functions-bindings-service-bus#hostjson-settings)*[Retry policies](#retry-policies)* Requires version 5.x of the Azure Service Bus extension. In older extension versions, the [Service Bus dead letter queue](../service-bus-messaging/service-bus-dead-letter-queues#maximum-delivery-count) implements retry behaviors.

## Retry policies

With Azure Functions, you can define retry policies for specific trigger types. The runtime enforces these retry policies. The following trigger types currently support retry policies:

Retry support is the same for both v1 and v2 Python programming models.

Retry policies aren't supported in version 1.x of the Azure Functions runtime.

The retry policy tells the runtime to rerun a failed execution until either successful completion occurs or the maximum number of retries is reached.

A retry policy is evaluated when a function that a supported trigger type executes raises an uncaught exception. As a best practice, you should catch all exceptions in your code and raise new exceptions for any errors that you want to result in a retry.

Important

Event Hubs checkpoints aren't written until after the retry policy for the execution finishes. Because of this behavior, progress on the specific partition is paused until the current batch finishes processing. For more information, see [Reliable event processing with Azure Functions and Event Hubs](functions-reliable-event-processing).

Version 5.x of the Event Hubs extension supports extra retry capabilities for interactions between the Azure Functions host and the event hub. For more information, see `clientRetryOptions`

in the [Event Hubs host.json reference](functions-bindings-event-hubs#host-json).

### Retry strategies

You can configure two retry strategies that are supported by policy:

A specified amount of time is allowed to elapse between each retry.

When you use a Consumption plan, you're billed only for the time that your function code is running. You aren't billed for the wait time between executions in either of these retry strategies.

### Maximum retry counts

You can configure the maximum number of times that a function execution is retried before eventual failure. The current retry count is stored in the memory of the instance.

It's possible for an instance to have a failure between retry attempts. When an instance fails during a retry policy, the retry count is lost. When there are instance failures, the Event Hubs trigger can resume processing and retry the batch on a new instance, with the retry count reset to zero. The timer trigger doesn't resume on a new instance.

This behavior means that the maximum retry count is a best effort. In some rare cases, an execution could be retried more than the requested maximum number of times. For timer triggers, the retries can be less than the requested maximum number.

### Retry examples

Examples are provided for both fixed delay and exponential backoff strategies. To see examples for a specific strategy, you must first select that strategy on the previous tab.

Function-level retries are supported with the following NuGet packages:

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)version 1.9.0 and later[Microsoft.Azure.Functions.Worker.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs)version 5.2.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Kafka](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kafka)version 3.8.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer)version 4.2.0 and later

```
[Function(nameof(TimerFunction))]
[FixedDelayRetry(5, "00:00:10")]
public static void Run([TimerTrigger("0 */5 * * * *")] TimerInfo timerInfo,
FunctionContext context)
{
var logger = context.GetLogger(nameof(TimerFunction));
logger.LogInformation($"Function Ran. Next timer schedule = {timerInfo.ScheduleStatus?.Next}");
}
```


| Property | Description |
|---|---|
`MaxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`DelayInterval` |
The delay used between retries. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a retry policy defined in the `function.json`

file:

```
{
"disabled": false,
"bindings": [
{
....
}
],
"retry": {
"strategy": "fixedDelay",
"maxRetryCount": 4,
"delayInterval": "00:00:10"
}
}
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
const { app } = require('@azure/functions');
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: (myTimer, context) => {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
},
});
```


The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTriggerWithRetry(myTimer: Timer, context: InvocationContext): Promise<void> {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
}
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: timerTriggerWithRetry,
});
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import logging
from azure.functions import AuthLevel, Context, FunctionApp, TimerRequest
app = FunctionApp(http_auth_level=AuthLevel.ANONYMOUS)
@app.timer_trigger(schedule="*/1 * * * * *", arg_name="mytimer",
run_on_startup=False,
use_monitor=False)
@app.retry(strategy="fixed_delay", max_retry_count="3",
delay_interval="00:00:01")
def mytimer(mytimer: TimerRequest, context: Context) -> None:
logging.info(f'Current retry count: {context.retry_context.retry_count}')
if context.retry_context.retry_count == \
context.retry_context.max_retry_count:
logging.info(
f"Max retries of {context.retry_context.max_retry_count} for "
f"function {context.function_name} has been reached")
else:
raise Exception("This is a retryable exception")
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixed_delay` and `exponential_backoff` . |
`max_retry_count` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delay_interval` |
The delay used between retries when you're using a `fixed_delay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimum_interval` |
The minimum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximum_interval` |
The maximum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

```
@FunctionName("TimerTriggerJava1")
@FixedDelayRetry(maxRetryCount = 4, delayInterval = "00:00:10")
public void run(
@TimerTrigger(name = "timerInfo", schedule = "0 */5 * * * *") String timerInfo,
final ExecutionContext context
) {
context.getLogger().info("Java Timer trigger function executed at: " + LocalDateTime.now());
}
```


## Binding error codes

When you're integrating with Azure services, errors might originate from the APIs of the underlying services. Information that relates to binding-specific errors is available in the "Exceptions and return codes" sections of the following articles:

[Azure Cosmos DB](/en-us/rest/api/cosmos-db/http-status-codes-for-cosmosdb)[Blob Storage](functions-bindings-storage-blob-output#exceptions-and-return-codes)[Event Grid](../event-grid/troubleshoot-errors)[Event Hubs](functions-bindings-event-hubs-output#exceptions-and-return-codes)[IoT Hub](functions-bindings-event-iot-output#exceptions-and-return-codes)[Notification Hubs](functions-bindings-notification-hubs#exceptions-and-return-codes)[Queue Storage](functions-bindings-storage-queue-output#exceptions-and-return-codes)[Service Bus](functions-bindings-service-bus-output#exceptions-and-return-codes)[Table Storage](functions-bindings-storage-table-output#exceptions-and-return-codes)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-error-pages -->

# Azure Functions error handling and retries

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Handling errors in Azure Functions helps you avoid lost data, avoid missed events, and monitor the health of your application. It's also an important way to help you understand the retry behaviors of event-based triggers.

This article describes general strategies for error handling and the available retry strategies.

Important

The preview of retry policy support for certain triggers was removed in December 2022. Retry policies for supported triggers are now in general availability (GA). The [Retries](#retries) section of this article lists extensions that currently support retry policies.

## Handling errors

Errors that occur in an Azure function can come from:

- Use of built-in Azure Functions
[triggers and bindings](functions-triggers-bindings). - Calls to APIs of underlying Azure services.
- Calls to REST endpoints.
- Calls to client libraries, packages, or non-Microsoft APIs.

To avoid loss of data or missed messages, you should practice good error handling. This table describes some recommended error-handling practices and provides links to more information:

| Recommendation | Details |
|---|---|
| Enable Application Insights | Azure Functions integrates with Application Insights to collect error data, performance data, and runtime logs. Use Application Insights to discover and better understand errors that occur in your function executions. To learn more, see
|

[Binding error codes](#binding-error-codes)in this article. Depending on your specific retry strategy, you might also raise a new exception to run the function again.[Retries](#retries)in this article.[Designing Azure Functions for identical input](functions-idempotent).Tip

When you use output bindings, you can't handle errors that occur from accessing the remote service. Because of this behavior, you should validate all data passed to your output bindings to avoid raising any known exceptions. If you must be able to handle such exceptions in your function code, you should access the remote service by using the client SDK instead of relying on output bindings.

## Retries

Two kinds of retries are available for your functions:

- Built-in retry behaviors of individual trigger extensions
- Retry policies that the Azure Functions runtime provides

The following table indicates which triggers support retries and where the retry behavior is configured. It also links to more information about errors that come from the underlying services.

| Trigger/binding | Retry source | Configuration |
|---|---|---|
| Azure Cosmos DB |
|

[Binding extension](functions-bindings-storage-blob-trigger#poison-blobs)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](../event-grid/delivery-and-retry)[Retry policies](#retry-policies)[Retry policies](#retry-policies)[Binding extension](functions-bindings-storage-queue-trigger#poison-messages)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](functions-bindings-rabbitmq-trigger#dead-letter-queues)[Dead letter queue](https://www.rabbitmq.com/dlx.html)[Binding extension](functions-bindings-service-bus-trigger)[host.json](functions-bindings-service-bus#hostjson-settings)*[Retry policies](#retry-policies)* Requires version 5.x of the Azure Service Bus extension. In older extension versions, the [Service Bus dead letter queue](../service-bus-messaging/service-bus-dead-letter-queues#maximum-delivery-count) implements retry behaviors.

## Retry policies

With Azure Functions, you can define retry policies for specific trigger types. The runtime enforces these retry policies. The following trigger types currently support retry policies:

Retry support is the same for both v1 and v2 Python programming models.

Retry policies aren't supported in version 1.x of the Azure Functions runtime.

The retry policy tells the runtime to rerun a failed execution until either successful completion occurs or the maximum number of retries is reached.

A retry policy is evaluated when a function that a supported trigger type executes raises an uncaught exception. As a best practice, you should catch all exceptions in your code and raise new exceptions for any errors that you want to result in a retry.

Important

Event Hubs checkpoints aren't written until after the retry policy for the execution finishes. Because of this behavior, progress on the specific partition is paused until the current batch finishes processing. For more information, see [Reliable event processing with Azure Functions and Event Hubs](functions-reliable-event-processing).

Version 5.x of the Event Hubs extension supports extra retry capabilities for interactions between the Azure Functions host and the event hub. For more information, see `clientRetryOptions`

in the [Event Hubs host.json reference](functions-bindings-event-hubs#host-json).

### Retry strategies

You can configure two retry strategies that are supported by policy:

A specified amount of time is allowed to elapse between each retry.

When you use a Consumption plan, you're billed only for the time that your function code is running. You aren't billed for the wait time between executions in either of these retry strategies.

### Maximum retry counts

You can configure the maximum number of times that a function execution is retried before eventual failure. The current retry count is stored in the memory of the instance.

It's possible for an instance to have a failure between retry attempts. When an instance fails during a retry policy, the retry count is lost. When there are instance failures, the Event Hubs trigger can resume processing and retry the batch on a new instance, with the retry count reset to zero. The timer trigger doesn't resume on a new instance.

This behavior means that the maximum retry count is a best effort. In some rare cases, an execution could be retried more than the requested maximum number of times. For timer triggers, the retries can be less than the requested maximum number.

### Retry examples

Examples are provided for both fixed delay and exponential backoff strategies. To see examples for a specific strategy, you must first select that strategy on the previous tab.

Function-level retries are supported with the following NuGet packages:

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)version 1.9.0 and later[Microsoft.Azure.Functions.Worker.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs)version 5.2.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Kafka](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kafka)version 3.8.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer)version 4.2.0 and later

```
[Function(nameof(TimerFunction))]
[FixedDelayRetry(5, "00:00:10")]
public static void Run([TimerTrigger("0 */5 * * * *")] TimerInfo timerInfo,
FunctionContext context)
{
var logger = context.GetLogger(nameof(TimerFunction));
logger.LogInformation($"Function Ran. Next timer schedule = {timerInfo.ScheduleStatus?.Next}");
}
```


| Property | Description |
|---|---|
`MaxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`DelayInterval` |
The delay used between retries. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a retry policy defined in the `function.json`

file:

```
{
"disabled": false,
"bindings": [
{
....
}
],
"retry": {
"strategy": "fixedDelay",
"maxRetryCount": 4,
"delayInterval": "00:00:10"
}
}
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
const { app } = require('@azure/functions');
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: (myTimer, context) => {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
},
});
```


The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTriggerWithRetry(myTimer: Timer, context: InvocationContext): Promise<void> {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
}
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: timerTriggerWithRetry,
});
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import logging
from azure.functions import AuthLevel, Context, FunctionApp, TimerRequest
app = FunctionApp(http_auth_level=AuthLevel.ANONYMOUS)
@app.timer_trigger(schedule="*/1 * * * * *", arg_name="mytimer",
run_on_startup=False,
use_monitor=False)
@app.retry(strategy="fixed_delay", max_retry_count="3",
delay_interval="00:00:01")
def mytimer(mytimer: TimerRequest, context: Context) -> None:
logging.info(f'Current retry count: {context.retry_context.retry_count}')
if context.retry_context.retry_count == \
context.retry_context.max_retry_count:
logging.info(
f"Max retries of {context.retry_context.max_retry_count} for "
f"function {context.function_name} has been reached")
else:
raise Exception("This is a retryable exception")
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixed_delay` and `exponential_backoff` . |
`max_retry_count` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delay_interval` |
The delay used between retries when you're using a `fixed_delay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimum_interval` |
The minimum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximum_interval` |
The maximum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

```
@FunctionName("TimerTriggerJava1")
@FixedDelayRetry(maxRetryCount = 4, delayInterval = "00:00:10")
public void run(
@TimerTrigger(name = "timerInfo", schedule = "0 */5 * * * *") String timerInfo,
final ExecutionContext context
) {
context.getLogger().info("Java Timer trigger function executed at: " + LocalDateTime.now());
}
```


## Binding error codes

When you're integrating with Azure services, errors might originate from the APIs of the underlying services. Information that relates to binding-specific errors is available in the "Exceptions and return codes" sections of the following articles:

[Azure Cosmos DB](/en-us/rest/api/cosmos-db/http-status-codes-for-cosmosdb)[Blob Storage](functions-bindings-storage-blob-output#exceptions-and-return-codes)[Event Grid](../event-grid/troubleshoot-errors)[Event Hubs](functions-bindings-event-hubs-output#exceptions-and-return-codes)[IoT Hub](functions-bindings-event-iot-output#exceptions-and-return-codes)[Notification Hubs](functions-bindings-notification-hubs#exceptions-and-return-codes)[Queue Storage](functions-bindings-storage-queue-output#exceptions-and-return-codes)[Service Bus](functions-bindings-service-bus-output#exceptions-and-return-codes)[Table Storage](functions-bindings-storage-table-output#exceptions-and-return-codes)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-concurrency -->

# Concurrency in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, a single function app instance allows for multiple events to be processed concurrently. Because these run on the same compute instance, they share memory, CPU, and connection resources. In certain hosting plans, high demand on a specific instance causes the Functions host to automatically create new instances to handle the increased load. In these *dynamic scale* plans, there's a tradeoff between concurrency and scaling behaviors. To provide more control over how your app runs, Functions provides a way for you to manage the number of concurrent executions.

Functions provides two main ways of managing concurrency:

[Fixed per-instance concurrency](#fixed-per-instance-concurrency): You can configure host-level limits on concurrency that are specific to individual triggers. This model is the default concurrency behavior for Functions.[Dynamic concurrency](#dynamic-concurrency): For certain trigger types, the Functions host can automatically determine the best level of concurrency for that trigger in your function app. You must[opt in to this concurrency model](#dynamic-concurrency-configuration).

This article describes the concurrency behaviors of event-driven triggers in Functions and how these behaviors affect scaling in dynamic plans. It also compares the fixed per-instance and dynamic concurrency models.

## Scaling versus concurrency

For functions that use event-based triggers or respond to HTTP requests, you can quickly reach the limits of concurrent executions during periods of high demand. During such periods, you must be able to scale your function app by adding instances to avoid a backlog in processing incoming requests. The way that we scale your app depends on your hosting plan:

| Scale type | Hosting plans | Description |
|---|---|---|
| Dynamic (event-driven) scaling |
|

[Event-driven scaling in Azure Functions](event-driven-scaling).[Dedicated (App Service) plans](dedicated-plan)[set up an autoscale scheme](dedicated-plan#scaling).Before any scaling might occur, your function app attempts to handle increases in load by handling multiple invocations of the same type in a single instance. As a result, these concurrent executions on a given instance directly impact scale decisions. For instance, when an app in a dynamic scale plan hits a concurrency limit, it might need to scale to keep up with incoming demand.

The balance of scale versus concurrency you try to achieve in your app depends on where bottlenecks might occur: in processing (CPU-intensive process limitations) or in a downstream service (I/O-based limitations).

## Fixed per-instance concurrency

By default, most triggers support a fixed per-instance concurrency configuration model via [target-based scaling](functions-target-based-scaling). In this model, each trigger type has a per-instance concurrency limit.

You can override the concurrency default values for most triggers by setting a specific per-instance concurrency for that trigger type. For many triggers, you configure concurrency settings in the [host.json file](functions-host-json). For example, the [Azure Service Bus trigger](functions-bindings-service-bus-trigger) provides both a `MaxConcurrentCalls`

and a `MaxConcurrentSessions`

setting in *host.json*. These settings work together to control the maximum number of messages that each function app processes concurrently on each instance.

In certain target-based scaling scenarios, such as when you use an Apache Kafka or Azure Cosmos DB trigger, the concurrency configuration is in the function declaration, not in the *host.json* file. Other trigger types have built-in mechanisms for load balancing invocations across instances. For example, Azure Event Hubs and Azure Cosmos DB both use a partition-based scheme.

For trigger types that support concurrency configuration, the concurrency settings are applied to all running instances. This way, you can control the maximum concurrency for your functions on each instance. For example, when your function is CPU-intensive or resource-intensive, you might choose to limit concurrency to keep instances healthy. In this case, you can rely on scaling to handle increased loads. Similarly, when your function makes requests to a downstream service that's being throttled, you should also consider limiting concurrency to avoid overloading the downstream service.

## HTTP trigger concurrency

*Applies only to the Flex Consumption plan*

HTTP trigger concurrency is a special type of fixed per-instance concurrency. In HTTP trigger concurrency, the default concurrency also depends on the [instance size](flex-consumption-plan#instance-sizes).

The Flex Consumption plan scales all HTTP trigger functions together as a group. For more information, see [Per-function scaling](event-driven-scaling#per-function-scaling).

The following table indicates the default concurrency setting for HTTP triggers on a given instance, based on the configured instance memory size:

| Instance size (MB) | Default concurrency* |
|---|---|
| 512 | 4 |
| 2,048 | 16 |
| 4,096 | 32 |

*In Python apps, all instance sizes use an HTTP trigger concurrency level of one by default.

These default values should work well for most cases, and you can start with them. Consider that at a given number of HTTP requests, increasing the HTTP concurrency value reduces the number of instances required to handle HTTP requests. Likewise, decreasing the HTTP concurrency value requires more instances to handle the same load.

If you need to fine-tune the HTTP concurrency, you can do so by using the Azure CLI. For more information, see [Set HTTP concurrency limits](flex-consumption-how-to#set-http-concurrency-limits).

The default concurrency values in the preceding table apply only when you don't set your own HTTP concurrency setting. When you don't explicitly set an HTTP concurrency setting, the default concurrency increases as shown in the table when you change the instance size. After you specifically set an HTTP concurrency value, that value is maintained despite changes in the instance size.

## Determine optimal fixed per-instance concurrency

Fixed per-instance concurrency configurations give you control of certain trigger behaviors, such as throttling your functions. But it can be difficult to determine the optimal values for these settings. Generally, you have to arrive at acceptable values by an iterative process of load testing. Even after you determine a set of values that work for a particular load profile, the number of events that arrive from your connected services can change from day to day. This variability can cause your app to run with suboptimal values. For example, your function app might process demanding message payloads on the last day of the week, which requires you to throttle concurrency down. However, during the rest of the week, the message payloads might be lighter, which means you can use a higher concurrency level the rest of the week.

Ideally, the system should allow instances to process as much work as they can while keeping each instance healthy and latencies low. Dynamic concurrency is designed for that purpose.

## Dynamic concurrency

Functions provides a dynamic concurrency model that simplifies configuring concurrency for all function apps that run in the same plan.

Note

Dynamic concurrency is currently only supported for the Azure Blob Storage, Azure Queue Storage, and Service Bus triggers. Also, you must use the extension versions listed in [Extension support](#extension-support), later in this article.

### Benefits

Dynamic concurrency provides the following benefits:

**Simplified configuration**: You no longer have to manually determine per-trigger concurrency settings. The system learns the optimal values for your workload over time.**Dynamic adjustments**: Concurrency is adjusted up or down dynamically in real time, which allows the system to adapt to changing load patterns over time.**Instance health protection**: The runtime limits concurrency to levels that a function app instance can comfortably handle. These limits protect the app from overloading itself by taking on more work than it should.**Improved throughput**: Overall throughput is improved, because individual instances don't pull more work than they can quickly process. As a result, work is load-balanced more effectively across instances. For functions that can handle higher loads, higher throughput can be obtained by increasing concurrency to values above the default configuration.

### Dynamic concurrency configuration

You can turn on dynamic concurrency at the host level in the *host.json* file. When it's turned on, the concurrency levels of any binding extensions that support this feature are adjusted automatically as needed. In these cases, dynamic concurrency settings override any manually configured concurrency settings.

By default, dynamic concurrency is turned off. When you turn on dynamic concurrency, concurrency starts at a level of one for each function. The concurrency level is adjusted up to an optimal value, which the host determines.

You can turn on dynamic concurrency in your function app by adding the following settings to your *host.json* file:

```
{
"version": "2.0",
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
}
}
```


When `snapshotPersistenceEnabled`

is `true`

, which is the default value, the learned concurrency values are periodically persisted to storage. New instances start from those values instead of starting from a level of one and having to redo the learning.

### Concurrency manager

Behind the scenes, when dynamic concurrency is turned on, a concurrency manager process runs in the background. This manager constantly monitors instance health metrics, like CPU and thread utilization, and changes throttles as needed. When one or more throttles are turned on, function concurrency is adjusted down until the host is healthy again. When throttles are turned off, concurrency can increase. Various heuristics are used to intelligently adjust concurrency up or down as needed based on these throttles. Over time, concurrency for each function stabilizes to a particular level. Because it can take time to determine the optimal concurrency value, use dynamic concurrency only if a suboptimal value is acceptable for your solution initially or after a period of inactivity.

Concurrency levels are managed for each individual function. Specifically, the system balances between resource-intensive functions that require a low level of concurrency and more lightweight functions that can handle higher concurrency. The balance of concurrency for each function helps to maintain the overall health of the function app instance.

When dynamic concurrency is turned on, you find dynamic concurrency decisions in your logs. For example, log entries are added when various throttles are turned on, and whenever concurrency is adjusted up or down for each function. These logs are written under the **Host.Concurrency** log category in the **traces** table.

### Extension support

Dynamic concurrency is enabled for a function app at the host level, and any extensions that support dynamic concurrency run in that mode. Dynamic concurrency requires collaboration between the host and individual trigger extensions. Only the listed versions of the following extensions support dynamic concurrency.

| Extension | Version | Description |
|---|---|---|
Queue Storage |
|

`BatchSize`

and `NewBatchThreshold`

configuration options govern concurrency. When you use dynamic concurrency, those configuration values are ignored. Dynamic concurrency is integrated into the message loop, so the number of messages retrieved per iteration is dynamically adjusted. When throttles are turned on, the host is overloaded. Message processing is paused until the throttles are turned off. When the throttles are turned off, concurrency increases.**Blob Storage**[Version 5.x](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage)(Storage extension)**Service Bus**[Version 5.x](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ServiceBus)**Single dispatch topic/queue processing**: Each invocation of your function processes a single message. When you use a fixed per-instance configuration, the

`MaxConcurrentCalls`

configuration option governs concurrency. When you use dynamic concurrency, that configuration value is ignored, and concurrency is adjusted dynamically.**Session-based single dispatch topic/queue processing**: Each invocation of your function processes a single message. Depending on the number of active sessions for your topic or queue, each instance leases one or more sessions. Messages in each session are processed serially, to guarantee ordering in a session. When you don't use dynamic concurrency, the

`MaxConcurrentSessions`

setting governs concurrency. When dynamic concurrency is turned on, the `MaxConcurrentSessions`

value is ignored, and the number of sessions that each instance processes is dynamically adjusted.**Batch processing**: Each invocation of your function processes a batch of messages, governed by the

`MaxMessageCount`

setting. Because batch invocations are serial, concurrency for your batch-triggered function is always one, and dynamic concurrency doesn't apply.## Next steps

For more information, see the following resources:
