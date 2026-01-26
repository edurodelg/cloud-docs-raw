---
merged_at: 2026-01-26T23:29:57.722713
merged_files: 2
---


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
