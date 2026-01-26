---
merged_at: 2026-01-26T23:29:57.728555
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-event-grid-blob-trigger -->

# Tutorial: Trigger Azure Functions on blob containers by using an event subscription

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Previous versions of the Azure Functions Blob Storage trigger poll your storage container for changes. More recent versions of the Blob Storage extension (5.x+) instead use an Event Grid event subscription on the container. This event subscription reduces latency by triggering your function instantly as changes occur in the subscribed container.

This article shows how to create a function that runs based on events raised when a blob is added to a container. You use Visual Studio Code for local development and to validate your code before deploying your project to Azure.

- Create an event-based Blob Storage triggered function in a new project.
- Validate locally within Visual Studio Code by using the Azurite emulator.
- Create a blob storage container in a new storage account in Azure.
- Create a function app in the Flex Consumption plan.
- Create an event subscription to the new blob container.
- Deploy and validate your function code in Azure.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

This article creates a C# app that runs in isolated worker mode, which supports .NET 8.0.

Tip

This tutorial shows you how to create an app that runs on the [Flex Consumption plan](flex-consumption-plan). The Flex Consumption plan only supports the event-based version of the Blob Storage trigger.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Node.js 14.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension installs[Azure Functions Core Tools](functions-run-local)for you the first time you locally run your functions.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21(Linux).[Apache Maven](https://maven.apache.org), version 3.0 or above.[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

[Azure Storage extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage)for Visual Studio Code.

Note

The Azure Storage extension for Visual Studio Code is in preview.

## Create a Blob triggered function

When you create a Blob Storage trigger function by using Visual Studio Code, you also create a new project. You need to edit the function to consume an event subscription as the source, rather than use the regular polled container.

In Visual Studio Code, press F1 to open the command palette, enter

`Azure Functions: Create Function...`

, and select**Create new project**.For your project workspace, select a directory location. Make sure that you either create a new folder or choose an empty folder for the project workspace.

Don't choose a project folder that's already part of a workspace.

At the prompts, provide the following information:

Prompt Action **Select a language**Select `C#`

.**Select a .NET runtime**Select `.NET 8.0 Isolated LTS`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Provide a namespace**Enter `My.Functions`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language**Select `Python`

.**Select a Python programming model**Select `Model V2`

**Select a Python interpreter to create a virtual environment**Select your preferred Python interpreter. If an option isn't shown, enter the full path to your Python binary. **Select a template for your project's first function**Select `Blob trigger`

. (The event-based template isn't yet available.)**Provide a function name**Enter `EventGridBlobTrigger`

.**The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language**Select `Java`

.**Select a version of Java**Select `Java 11`

or`Java 8`

, the Java version on which your functions run in Azure and that you've locally verified.**Provide a group ID**Select `com.function`

.**Provide an artifact ID**Select `EventGridBlobTrigger`

(or the default).**Provide a version**Select `1.0-SNAPSHOT`

.**Provide a package name**Select `com.function`

.**Provide an app name**Accept the generated name starting with `EventGridBlobTrigger`

.**Select the build tool for Java project**Select `Maven`

.**Select how you would like to open your project**Select `Open in current window`

.An HTTP triggered function (

`HttpExample`

) is created for you. You won't use this function and must instead create a new function.Prompt Action **Select a language for your function project**Select `TypeScript`

.**Select a TypeScript programming model**Select `Model V4`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language for your function project**Select `JavaScript`

.**Select a JavaScript programming model**Select `Model V4`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `eventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language for your function project**Select `PowerShell`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.

In the command palette, enter

`Azure Functions: Create Function...`

and select`EventGridBlobTrigger`

. If you don't see this template, first select**Change template filter**>**All**.At the prompts, provide the following information:

Prompt Action **Provide a package name**Select `com.function`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.

You now have a function that can be triggered by events in a Blob Storage container.

## Update the trigger source

You need to switch the trigger source from the default Blob trigger source (container polling) to an event subscription source.

Open the function_app.py project file. You see a definition for the

`EventGridBlobTrigger`

function with the`blob_trigger`

decorator applied.Update the decorator by adding

`source = "EventGrid"`

. Your function should now look something like this:`@app.blob_trigger(arg_name="myblob", source="EventGrid", path="samples-workitems", connection="<STORAGE_ACCOUNT>") def EventGridBlobTrigger(myblob: func.InputStream): logging.info(f"Python blob trigger function processed blob" f"Name: {myblob.name}" f"Blob Size: {myblob.length} bytes")`

In this definition,

`source = "EventGrid"`

indicates that an event subscription to the`samples-workitems`

blob container is used as the source of the event that starts the trigger.

## (Optional) Review the code

Open the generated `EventGridBlobTrigger.cs`

file. You see a definition for an `EventGridBlobTrigger`

function that looks something like this:

```
[Function(nameof(EventGridBlobTriggerCSharp))]
public async Task Run([BlobTrigger("PathValue/{name}", Source = BlobTriggerSource.EventGrid, Connection = "ConnectionValue")] Stream stream, string name)
{
using var blobStreamReader = new StreamReader(stream);
var content = await blobStreamReader.ReadToEndAsync();
_logger.LogInformation("C# Blob Trigger (using Event Grid) processed blob\n Name: {name} \n Data: {content}", name, content);
}
```


In this definition, `Source = BlobTriggerSource.EventGrid`

indicates that an event subscription to the blob container (in the example `PathValue`

) is the source of the event that starts the trigger.

Open the generated `EventGridBlobTrigger.java`

file. You see a definition for an `EventGridBlobTrigger`

function that looks something like this:

```
@FunctionName("EventGridBlobTrigger")
@StorageAccount("<STORAGE_ACCOUNT>")
public void run(
@BlobTrigger(name = "content", source = "EventGrid", path = "samples-workitems/{name}", dataType = "binary") byte[] content,
@BindingName("name") String name,
final ExecutionContext context
) {
context.getLogger().info("Java Blob trigger function processed a blob. Name: " + name + "\n Size: " + content.length + " Bytes");
}
```


In this definition, `source = EventGrid`

indicates that an event subscription to the `samples-workitems`

blob container is the source of the event that starts the trigger.

In the `EventGridBlobTrigger`

folder, open the `function.json`

file and find a binding definition like this with a `type`

of `blobTrigger`

and a `source`

of `EventGrid`

:

```
{
"bindings": [
{
"name": "InputBlob",
"type": "blobTrigger",
"direction": "in",
"path": "samples-workitems/{name}",
"source": "EventGrid",
"connection":""
}
]
}
```


The `path`

indicates that the `samples-workitems`

blob container is the source of the event that starts the trigger.

Open the generated `EventGridBlobTrigger.js`

file. You see a definition for a function that looks something like this:

```
const { app } = require('@azure/functions');
app.storageBlob('storageBlobTrigger1', {
path: 'samples-workitems/{name}',
connection: 'MyStorageAccountAppSetting',
source: 'EventGrid',
handler: (blob, context) => {
context.log(
`Storage blob function processed blob "${context.triggerMetadata.name}" with size ${blob.length} bytes`
);
},
});
```


In this definition, a `source`

of `EventGrid`

indicates that an event subscription to the `samples-workitems`

blob container is the source of the event that starts the trigger.

Open the generated `EventGridBlobTrigger.ts`

file. You see a definition for a function that looks something like this:

```
import { app, InvocationContext } from '@azure/functions';
export async function storageBlobTrigger1(blob: Buffer, context: InvocationContext): Promise<void> {
context.log(
`Storage blob function processed blob "${context.triggerMetadata.name}" with size ${blob.length} bytes`
);
}
app.storageBlob('storageBlobTrigger1', {
path: 'samples-workitems/{name}',
connection: 'MyStorageAccountAppSetting',
source: 'EventGrid',
handler: storageBlobTrigger1,
});
```


In this definition, a `source`

of `EventGrid`

indicates that an event subscription to the `samples-workitems`

blob container is the source of the event that starts the trigger.

## Upgrade the Storage extension

To use the Event Grid-based Blob Storage trigger, you need version 5.x or later of the Azure Functions Storage extension.

To upgrade your project to the required extension version, run this [ dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs
```


Open the

`host.json`

project file, and review the`extensionBundle`

element.If

`extensionBundle.version`

isn't at least`3.3.0`

, replace the`extensionBundle`

element with this version:`"extensionBundle": { "id": "Microsoft.Azure.Functions.ExtensionBundle", "version": "[4.0.0, 5.0.0)" }`


## Prepare local storage emulation

Visual Studio Code uses Azurite to emulate Azure Storage services when running locally. Use Azurite to emulate the Azure Blob Storage service during local development and testing.

If you haven't already done so, install the

[Azurite v3 extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=Azurite.azurite).Verify that the

*local.settings.json*file has`"UseDevelopmentStorage=true"`

set for`AzureWebJobsStorage`

. This setting tells Core Tools to use Azurite instead of a real storage account connection when running locally.Press F1 to open the command palette, type

`Azurite: Start Blob Service`

, and press enter. This action starts the Azurite Blob Storage service emulator.Select the Azure icon in the Activity bar, expand

**Workspace**>**Attached Storage Accounts**>**Local Emulator**, right-click**Blob Containers**, select**Create Blob Container...**, enter the name`samples-workitems`

, and press Enter.Expand

**Blob Containers**>**samples-workitems**and select**Upload files...**.Choose a file to upload to the locally emulated container. Your function processes this file later to verify and debug your function code. A text file might work best with the Blob trigger template code.


## Run the function locally

With a file in emulated storage, you can run your function to simulate an event raised by an Event Grid subscription. The event info passed to your trigger depends on the file you added to the local container.

Set any breakpoints and press F5 to start your project for local debugging. Azure Functions Core Tools should be running in your Terminal window.

Back in the Azure area, expand

**Workspace**>**Local Project**>**Functions**, right-click the function, and select**Execute Function Now...**.In the request body dialog, type

`samples-workitems/<TEST_FILE_NAME>`

, replacing`<TEST_FILE_NAME>`

with the name of the file you uploaded in the local storage emulator.Press Enter to run the function. The value you provided is the path to your blob in the local emulator. This string gets passed to your trigger in the request payload, which simulates the payload when an event subscription calls your function to report a blob being added to the container.

Review the output of this function execution. You should see in the output the name of the file and its contents logged. If you set any breakpoints, you might need to continue the execution.


Now that you've successfully validated your function code locally, it's time to publish the project to a new function app in Azure.

## Prepare the Azure Storage account

Event subscriptions to Azure Storage require a general-purpose v2 storage account. You can use the Azure Storage extension for Visual Studio Code to create this storage account.

In Visual Studio Code, press F1 to open the command palette and enter

`Azure Storage: Create Storage Account...`

. Provide this information when prompted:Prompt Action **Enter the name of the new storage account**Provide a globally unique name. Storage account names must have 3 to 24 characters in length with only lowercase letters and numbers. For easier identification, use the same name for the resource group and the function app name. **Select a location for new resources**For better performance, choose a [region near you](https://azure.microsoft.com/regions/).The extension creates a general-purpose v2 storage account with the name you provide. The same name is also used for the resource group that contains the storage account. The Event Grid-based Blob Storage trigger requires a general-purpose v2 storage account.

Press F1 again and in the command palette enter

`Azure Storage: Create Blob Container...`

. Provide this information when prompted:Prompt Action **Select a resource**Select the general-purpose v2 storage account that you created. **Enter a name for the new blob container**Enter `samples-workitems`

, which is the container name referenced in your code project.

Your function app also needs a storage account to run. For simplicity, this tutorial uses the same storage account for your blob trigger and your function app. However, in production, you might want to use a separate storage account with your function app. For more information, see [Storage considerations for Azure Functions](storage-considerations).

## Create the function app

Use these steps to create a function app in the Flex Consumption plan. When you host your app in a Flex Consumption plan, Blob Storage triggers must use event subscriptions.

In the command palette, enter

**Azure Functions: Create function app in Azure...(Advanced)**.Follow the prompts and provide this information:

Prompt Selection **Enter a globally unique name for the new function app**Type a globally unique name that identifies your new function app and then select Enter. Valid characters for a function app name are `a-z`

,`0-9`

, and`-`

.**Select a hosting plan**Choose **Flex Consumption**, which is the recommended[hosting plan](functions-scale)for serverless hosting.**Select a location for new resources**Select a location in a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Select a runtime stack**Select the language version you currently run locally. **Select an instance size**Select **512**. You can always[change the instance size](flex-consumption-how-to#configure-instance-memory)setting to a larger size later.**Enter the maximum instance count**Select the default value of **100**, which limits the total scale-out of your app. You can also choose a different value between 40 and 1,000.**Select a resource group**Select **Create new resource group**and accept the default or enter another name for the new group that's unique in your subscription.**Select resource authentication type**Select **Managed identity**so that your app connects to remote resources by using Microsoft Entra ID authentication instead of using shared secrets (connection strings and keys), which are less secure.**Select a user assigned identity**Select **Create new user-assigned identity**.**Select a location for new resources**Select the same region as the storage account you created. If for some reason this region isn't supported by the Flex Consumption play, it isn't displayed. In that case, choose a nearby [region](https://azure.microsoft.com/regions/)instead. For more information, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Select a storage account**Choose the name of the storage account you created. **Select an Application Insights resource for your app**Choose **Create new Application Insights resource**and at the prompt provide the name for the instance used to store runtime data from your functions.A notification appears after your function app is created. Select

**View Output**in this notification to view the creation results, including the Azure resources that you created.

## Deploy your function code

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Update application settings

Because the publishing process doesn't automatically upload required application settings from the `local.settings.json`

file, you must upload them to your function app so that your function runs correctly in Azure.

In the command palette, enter

`Azure Functions: Download Remote Settings...`

, and in the**Select a resource**prompt choose the name of your function app.When prompted that the

`AzureWebJobsStorage`

setting already exists, select**Yes**to overwrite the local emulator setting with the actual storage account connection string from Azure.In the

`local.settings.json`

file, replace the local emulator setting with same connection string used for`AzureWebJobsStorage`

.Remove the

`FUNCTIONS_WORKER_RUNTIME`

entry, which isn't supported in a Flex Consumption plan.In the command palette, enter

`Azure Functions: Upload Local Settings...`

, and in the**Select a resource**prompt choose the name of your function app.

Now both the Functions host and the trigger share the same storage account.

## Build the endpoint URL

To create an event subscription, you need to provide Event Grid with the URL of the specific endpoint to report Blob Storage events. This *blob extension* URL is composed of these parts:

| Part | Example |
|---|---|
| Base function app URL | `https://<FUNCTION_APP_NAME>.azurewebsites.net` |
| Blob-specific path | `/runtime/webhooks/blobs` |
| Function query string | `?functionName=Host.Functions.<FUNCTION_NAME>` |
| Blob extension access key | `&code=<BLOB_EXTENSION_KEY>` |

While your app connects to the storage account by using Microsoft Entra ID authentication, the blob extension access key helps protect your blob extension webhook from unauthorized access. To find your blob extension access key:

In Visual Studio Code, select the Azure icon in the Activity bar. In

**Resources**, expand your subscription, expand**Function App**, right-click the function app you created, and select**Open in portal**.Under

**Functions**in the left menu, select**App keys**.Under

**System keys**, select the key named**blobs_extension**, and copy the key**Value**.Include this value in the query string of the new endpoint URL.

Create a new endpoint URL for the Blob Storage trigger based on the following example:

`https://<FUNCTION_APP_NAME>.azurewebsites.net/runtime/webhooks/blobs?functionName=Host.Functions.EventGridBlobTrigger&code=<BLOB_EXTENSION_KEY>`

In this example, replace

`<FUNCTION_APP_NAME>`

with the name of your function app, and`<BLOB_EXTENSION_KEY>`

with the value you got from the portal. If you used a different name for your function, replace`EventGridBlobTrigger`

with that function name.

You can now use this endpoint URL to create an event subscription.

## Create the event subscription

An event subscription, powered by Azure Event Grid, raises events based on changes in the subscribed blob container. This event is then sent to the blob extension endpoint for your function. After you create an event subscription, you can't update the endpoint URL.

In Visual Studio Code, choose the Azure icon in the Activity bar. In

**Resources**, expand your subscription, expand**Storage accounts**, right-click the storage account you created earlier, and select**Open in portal**.Sign in to the

[Azure portal](https://portal.azure.com)and make a note of the**Resource group**for your storage account. Create your other resources in the same group to make it easier to clean up resources when you're done.Select the

**Events**option from the left menu.In the

**Events**window, select the**+ Event Subscription**button, and provide values from the following table into the**Basic**tab:Setting Suggested value Description **Name***myBlobEventSub*Name that identifies the event subscription. Use the name to quickly find the event subscription. **Event Schema****Event Grid Schema**Use the default schema for events. **System Topic Name***samples-workitems-blobs*Name for the topic, which represents the container. The topic is created with the first subscription, and you use it for future event subscriptions. **Filter to Event Types***Blob Created***Endpoint Type****Web Hook**The blob storage trigger uses a web hook endpoint. **Endpoint**Your Azure-based URL endpoint Use the URL endpoint that you built, which includes the key value. Select

**Confirm selection**to validate the endpoint URL.Select the

**Filters**tab and provide the following information to the prompts:Setting Suggested value Description **Enable subject filtering***Enabled*Enables filtering on which blobs can trigger the function. **Subject Begins With**`/blobServices/default/containers/<CONTAINER_NAME>/blobs/<BLOB_PREFIX>`

Replace `<CONTAINER_NAME`

and`<BLOB_PREFIX>`

with values you choose. This setting triggers the subscription only for blobs that start with`BLOB_PREFIX`

and are in the`CONTAINER_NAME`

container.**Subject Ends With***.txt*Ensures that the function is only triggered by blobs ending with `.txt`

.For more information on filtering to specific blobs, see

[Event Filtering for Azure Event Hubs](../event-grid/event-filtering).Select

**Create**to create the event subscription.

## Upload a file to the container

You can upload a file from your computer to your blob storage container by using Visual Studio Code.

In Visual Studio Code, press F1 to open the command palette and type

`Azure Storage: Upload Files...`

.In the

**Open**dialog box, choose a file, preferably a text file, and select**Upload**.Provide the following information at the prompts:

Setting Suggested value Description **Enter the destination directory of this upload**default Accept the default value of `/`

, which is the container root.**Select a resource**Storage account name Choose the name of the storage account you created in a previous step. **Select a resource type****Blob Containers**You're uploading to a blob container. **Select Blob Container****samples-workitems**This value is the name of the container you created in a previous step.

Browse your local file system to find a file to upload, then select the **Upload** button to upload the file.

## Verify the function in Azure

When you upload a file to the **samples-workitems** container, the function triggers. You can verify the function by checking the following items on the Azure portal:

In your storage account, go to the

**Events**page, select**Event Subscriptions**, and you should see that an event was delivered. There might be up to a five-minute delay for the event to show up on the chart.Back in your function app page in the portal, under

**Functions**find your function and select**Invocations and more**. You should see traces written from your successful function execution.

## Clean up resources

When you continue to the [next step](#next-steps) and add an Azure Storage queue binding to your function, you'll need to keep all your resources in place to build on what you've already done.

Otherwise, you can use the following steps to delete the function app and its related resources to avoid incurring any further costs.

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


For more information about Functions costs, see [Estimating Consumption plan costs](functions-consumption-costs).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-sql-input -->

# Azure SQL input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure SQL input binding retrieves data from a database and passes it to the input parameter of the function.

For information on setup and configuration details, see the [overview](functions-bindings-azure-sql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-outofproc).

This section contains the following examples:

[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-c-oop)[HTTP trigger, get multiple rows from route data](#http-trigger-get-multiple-items-from-route-data-c-oop)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-c-oop)

The examples refer to a `ToDoItem`

class and a corresponding database table:

```
namespace AzureSQL.ToDo
{
public class ToDoItem
{
public Guid Id { get; set; }
public int? order { get; set; }
public string title { get; set; }
public string url { get; set; }
public bool? completed { get; set; }
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get row by ID from query string

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single record. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses a query string to specify the ID. That ID is used to retrieve a `ToDoItem`

record with the specified query.

Note

The HTTP query string parameter is case-sensitive.

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker.Http;
namespace AzureSQLSamples
{
public static class GetToDoItem
{
[FunctionName("GetToDoItem")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "gettodoitem")]
HttpRequest req,
[SqlInput(commandText: "select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
commandType: System.Data.CommandType.Text,
parameters: "@Id={Query.id}",
connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItem)
{
return new OkObjectResult(toDoItem.FirstOrDefault());
}
}
}
```


### HTTP trigger, get multiple rows from route parameter

The following example shows a [C# function](functions-dotnet-class-library) that retrieves documents returned by the query. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses route data to specify the value of a query parameter. That parameter is used to filter the `ToDoItem`

records in the specified query.

```
using System.Collections.Generic;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker.Http;
namespace AzureSQLSamples
{
public static class GetToDoItems
{
[FunctionName("GetToDoItems")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "gettodoitems/{priority}")]
HttpRequest req,
[SqlInput(commandText: "select [Id], [order], [title], [url], [completed] from dbo.ToDo where [Priority] > @Priority",
commandType: System.Data.CommandType.Text,
parameters: "@Priority={priority}",
connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItems)
{
return new OkObjectResult(toDoItems);
}
}
}
```


### HTTP trigger, delete rows

The following example shows a [C# function](functions-dotnet-class-library) that executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the SQL database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
namespace AzureSQL.ToDo
{
public static class DeleteToDo
{
// delete all items or a specific item from querystring
// returns remaining items
// uses input binding with a stored procedure DeleteToDo to delete items and return remaining items
[FunctionName("DeleteToDo")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "delete", Route = "DeleteFunction")] HttpRequest req,
ILogger log,
[SqlInput(commandText: "DeleteToDo", commandType: System.Data.CommandType.StoredProcedure,
parameters: "@Id={Query.id}", connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItems)
{
return new OkObjectResult(toDoItems);
}
}
}
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-java).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-java)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-java)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-java)

The examples refer to a `ToDoItem`

class (in a separate file `ToDoItem.java`

) and a corresponding database table:

```
package com.function;
import java.util.UUID;
public class ToDoItem {
public UUID Id;
public int order;
public String title;
public String url;
public boolean completed;
public ToDoItem() {
}
public ToDoItem(UUID Id, int order, String title, String url, boolean completed) {
this.Id = Id;
this.order = order;
this.title = title;
this.url = url;
this.completed = completed;
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get multiple rows

The following example shows a SQL input binding in a Java function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

```
package com.function;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.sql.annotation.SQLInput;
import java.util.Optional;
public class GetToDoItems {
@FunctionName("GetToDoItems")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@SQLInput(
name = "toDoItems",
commandText = "SELECT * FROM dbo.ToDo",
commandType = "Text",
connectionStringSetting = "SqlConnectionString")
ToDoItem[] toDoItems) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(toDoItems).build();
}
}
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding in a Java function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

```
public class GetToDoItem {
@FunctionName("GetToDoItem")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@SQLInput(
name = "toDoItems",
commandText = "SELECT * FROM dbo.ToDo",
commandType = "Text",
parameters = "@Id={Query.id}",
connectionStringSetting = "SqlConnectionString")
ToDoItem[] toDoItems) {
ToDoItem toDoItem = toDoItems[0];
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(toDoItem).build();
}
}
```


### HTTP trigger, delete rows

The following example shows a SQL input binding in a Java function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
public class DeleteToDo {
@FunctionName("DeleteToDo")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@SQLInput(
name = "toDoItems",
commandText = "dbo.DeleteToDo",
commandType = "StoredProcedure",
parameters = "@Id={Query.id}",
connectionStringSetting = "SqlConnectionString")
ToDoItem[] toDoItems) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(toDoItems).build();
}
}
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-js).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-javascript)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-javascript)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-javascript)

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get multiple rows

The following example shows a SQL input binding that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo',
commandType: 'Text',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo',
commandType: 'Text',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: (request, context) => {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
},
});
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id',
commandType: 'Text',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItem = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItem,
};
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id',
commandType: 'Text',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: (request, context) => {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItem = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItem,
};
},
});
```


### HTTP trigger, delete rows

The following example shows a SQL input binding that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const sqlInput = input.sql({
commandText: 'DeleteToDo',
commandType: 'StoredProcedure',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const sqlInput = input.sql({
commandText: 'DeleteToDo',
commandType: 'StoredProcedure',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: (request, context) => {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
},
});
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-powershell).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-powershell)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-powershell)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-powershell)

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get multiple rows

The following example shows a SQL input binding in a function.json file and a PowerShell function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItems",
"type": "sql",
"direction": "in",
"commandText": "select [Id], [order], [title], [url], [completed] from dbo.ToDo",
"commandType": "Text",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request, $todoItems)
Write-Host "PowerShell function with SQL Input Binding processed a request."
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $todoItems
})
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding in a PowerShell function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItem",
"type": "sql",
"direction": "in",
"commandText": "select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
"commandType": "Text",
"parameters": "@Id = {Query.id}",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request, $todoItem)
Write-Host "PowerShell function with SQL Input Binding processed a request."
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $todoItem
})
```


### HTTP trigger, delete rows

The following example shows a SQL input binding in a function.json file and a PowerShell function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItems",
"type": "sql",
"direction": "in",
"commandText": "DeleteToDo",
"commandType": "StoredProcedure",
"parameters": "@Id = {Query.id}",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request, $todoItems)
Write-Host "PowerShell function with SQL Input Binding processed a request."
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $todoItems
})
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-python).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-python)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-python)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-python)

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get multiple rows

The following example shows a SQL input binding in a function.json file and a Python function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

The following python code is a sample function_app.py file:

```
import json
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="GetToDo")
@app.route(route="gettodo")
@app.sql_input(arg_name="todo",
command_text="select [Id], [order], [title], [url], [completed] from dbo.ToDo",
command_type="Text",
connection_string_setting="SqlConnectionString")
def get_todo(req: func.HttpRequest, todo: func.SqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), todo))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding in a Python function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

The following python code is a sample function_app.py file:

```
import json
import logging
import azure.functions as func
from azure.functions.decorators.core import DataType
app = func.FunctionApp()
@app.function_name(name="GetToDo")
@app.route(route="gettodo/{id}")
@app.sql_input(arg_name="todo",
command_text="select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
command_type="Text",
parameters="@Id={id}",
connection_string_setting="SqlConnectionString")
def get_todo(req: func.HttpRequest, todo: func.SqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), todo))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, delete rows

The following example shows a SQL input binding in a function.json file and a Python function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


The following python code is a sample function_app.py file:

```
import json
import logging
import azure.functions as func
from azure.functions.decorators.core import DataType
app = func.FunctionApp()
@app.function_name(name="DeleteToDo")
@app.route(route="deletetodo/{id}")
@app.sql_input(arg_name="todo",
command_text="DeleteToDo",
command_type="StoredProcedure",
parameters="@Id={id}",
connection_string_setting="SqlConnectionString")
def get_todo(req: func.HttpRequest, todo: func.SqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), todo))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [SqlAttribute](https://github.com/Azure/azure-functions-sql-extension/blob/main/src/SqlAttribute.cs) attribute to declare the SQL bindings on the function, which has the following properties:

| Attribute property | Description |
|---|---|
CommandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
ConnectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
CommandType |
Required. A
|

**Parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@SQLInput`

annotation (`com.microsoft.azure.functions.sql.annotation.SQLInput`

) on parameters whose value would come from Azure SQL. This annotation supports the following elements:

| Element | Description |
|---|---|
commandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
commandType |
Required. A
|

**name****parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `input.sql()`

method.

| Property | Description |
|---|---|
commandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

**commandType**[CommandType](/en-us/dotnet/api/system.data.commandtype)value, which is[Text](/en-us/dotnet/api/system.data.commandtype#fields)for a query and[StoredProcedure](/en-us/dotnet/api/system.data.commandtype#fields)for a stored procedure.**parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
type |
Required. Must be set to `sql` . |
direction |
Required. Must be set to `in` . |
name |
Required. The name of the variable that represents the query results in function code. |
commandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

**commandType**[CommandType](/en-us/dotnet/api/system.data.commandtype)value, which is[Text](/en-us/dotnet/api/system.data.commandtype#fields)for a query and[StoredProcedure](/en-us/dotnet/api/system.data.commandtype#fields)for a stored procedure.**parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The binding definition includes the SQL command text, the command type, parameters, and the connection string setting name. The command can be a Transact-SQL (T-SQL) query with the command type `System.Data.CommandType.Text`

or stored procedure name with the command type `System.Data.CommandType.StoredProcedure`

. The connection string setting name corresponds to the application setting (in `local.settings.json`

for local development) that contains the [connection string](/en-us/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-core-5.0&preserve-view=true#Microsoft_Data_SqlClient_SqlConnection_ConnectionString) to the Azure SQL or SQL Server instance.

Important

For optimal security, you should use Microsoft Entra ID with managed identities for connections between Functions and Azure SQL Database. Managed identities make your app more secure by eliminating secrets from your application deployments, such as credentials in the connection strings, server names, and ports being used. You can learn how to use managed identities in this tutorial, [Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).

Queries executed by the input binding are [parameterized](/en-us/dotnet/api/microsoft.data.sqlclient.sqlparameter) in Microsoft.Data.SqlClient to reduce the risk of [SQL injection](/en-us/sql/relational-databases/security/sql-injection) from the parameter values passed into the binding.

If an exception occurs when a SQL input binding is executed, then the function code doesn't execute. This behavior may result in an error code being returned, such as an HTTP trigger returning a 500 error code.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/openapi-apim-integrate-visual-studio -->

# Create serverless APIs in Visual Studio using Azure Functions and API Management integration

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

REST APIs are often described using an OpenAPI definition (formerly known as Swagger) file. This file contains information about operations in an API and how the request and response data for the API should be structured.

In this tutorial, you learn how to:

- Create the code project in Visual Studio
- Install the OpenAPI extension
- Add an HTTP trigger endpoint, which includes OpenAPI definitions
- Test function APIs locally using built-in OpenAPI functionality
- Publish project to a function app in Azure
- Enable API Management integration
- Download the OpenAPI definition file

The serverless function you create provides an API that lets you determine whether an emergency repair on a wind turbine is cost-effective. Since you create both the function app and API Management instance in a consumption tier, your cost for completing this tutorial is minimal.

## Prerequisites

[Visual Studio 2022](https://azure.microsoft.com/downloads/). Make sure you select the**Azure development**workload during installation.An active

[Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create a[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create the code project

The Azure Functions project template in Visual Studio creates a project that you can publish to a function app in Azure. You'll also create an HTTP triggered function from a template that supports OpenAPI definition file (formerly Swagger file) generation.

From the Visual Studio menu, select

**File**>**New**>**Project**.In

**Create a new project**, enter*functions*in the search box, choose the**Azure Functions**template, and then select**Next**.In

**Configure your new project**, enter a**Project name**for your project like`TurbineRepair`

, and then select**Create**.For the

**Create a new Azure Functions application**settings, select one of these options for**Functions worker**, where the option you choose depends on your chosen process model:**.NET 8.0 Isolated (Long Term Support)**: Your C# functions run in the isolated worker model, which is recommended. For more information, see the[isolated worker model guide](dotnet-isolated-process-guide).For the rest of the options, use the values in the following table:

Setting Value Description **Function template****Empty**This creates a project without a trigger, which gives you more control over the name of the HTTP triggered function when you add it later. **Use Azurite for runtime storage account (AzureWebJobsStorage)****Selected**You can use the emulator for local development of HTTP trigger functions. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. **Authorization level****Function**When running in Azure, clients must provide a key when accessing the endpoint. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Select

**Create**to create the function project.

Next, you update the project by installing the OpenAPI extension for Azure Functions, which enables the discoverability of API endpoints in your app.

## Install the OpenAPI extension

To install the OpenAPI extension:

From the

**Tools**menu, select**NuGet Package Manager**>**Package Manager Console**.In the console, run the following

[Install-Package](/en-us/nuget/tools/ps-ref-install-package)command to install the OpenAPI extension:`NuGet\Install-Package Microsoft.Azure.Functions.Worker.Extensions.OpenApi -Version 1.5.1`

You might need to update the

[specific version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenApi), based on your version of .NET.

Now, you can add your HTTP endpoint function.

## Add an HTTP endpoint function

In a C# class library, the bindings used by the function are defined by applying attributes in the code. To create a function with an HTTP trigger:

In

**Solution Explorer**, right-click your project node and select**Add**>**New Azure Function**.Enter

**Turbine.cs**for the class, and then select**Add**.Choose the

**Http trigger**template, set**Authorization level**to**Function**, and then select**Add**. A Turbine.cs code file is added to your project that defines a new function endpoint with an HTTP trigger.

Now you can replace the HTTP trigger template code with code that implements the Turbine function endpoint, along with attributes that use OpenAPI to define endpoint.

## Update the function code

The function uses an HTTP trigger that takes two parameters:

| Parameter name | Description |
|---|---|
hours |
The estimated time to make a turbine repair, up to the nearest whole hour. |
capacity |
The capacity of the turbine, in kilowatts. |

The function then calculates how much a repair costs, and how much revenue the turbine could make in a 24-hour period. Parameters are supplied either in the query string or in the payload of a POST request.

In the Turbine.cs project file, replace the contents of the class generated from the HTTP trigger template with the following code, which depends on your process model:

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.WebJobs.Extensions.OpenApi.Core.Attributes;
using Microsoft.Azure.WebJobs.Extensions.OpenApi.Core.Enums;
using Microsoft.Extensions.Logging;
using Microsoft.OpenApi.Models;
using Newtonsoft.Json;
using System.Net;
namespace TurbineRepair
{
public class Turbine
{
const double revenuePerkW = 0.12;
const double technicianCost = 250;
const double turbineCost = 100;
private readonly ILogger<Turbine> _logger;
public Turbine(ILogger<Turbine> logger)
{
_logger = logger;
}
[Function("TurbineRepair")]
[OpenApiOperation(operationId: "Run")]
[OpenApiSecurity("function_key", SecuritySchemeType.ApiKey, Name = "code", In = OpenApiSecurityLocationType.Query)]
[OpenApiRequestBody("application/json", typeof(RequestBodyModel),
Description = "JSON request body containing { hours, capacity}")]
[OpenApiResponseWithBody(statusCode: HttpStatusCode.OK, contentType: "application/json", bodyType: typeof(string),
Description = "The OK response message containing a JSON result.")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = null)] HttpRequest req,
ILogger log)
{
// Get request body data.
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic? data = JsonConvert.DeserializeObject(requestBody);
int? capacity = data?.capacity;
int? hours = data?.hours;
// Return bad request if capacity or hours are not passed in
if (capacity == null || hours == null)
{
return new BadRequestObjectResult("Please pass capacity and hours in the request body");
}
// Formulas to calculate revenue and cost
double? revenueOpportunity = capacity * revenuePerkW * 24;
double? costToFix = hours * technicianCost + turbineCost;
string repairTurbine;
if (revenueOpportunity > costToFix)
{
repairTurbine = "Yes";
}
else
{
repairTurbine = "No";
};
return new OkObjectResult(new
{
message = repairTurbine,
revenueOpportunity = "$" + revenueOpportunity,
costToFix = "$" + costToFix
});
}
public class RequestBodyModel
{
public int Hours { get; set; }
public int Capacity { get; set; }
}
}
}
```


This function code returns a message of `Yes`

or `No`

to indicate whether an emergency repair is cost-effective. It also returns the revenue opportunity that the turbine represents and the cost to fix the turbine.

## Run and verify the API locally

When you run the function, the OpenAPI endpoints make it easy to try out the function locally using a generated page. You don't need to provide function access keys when running locally.

Press F5 to start the project. When Functions runtime starts locally, a set of OpenAPI and Swagger endpoints are shown in the output, along with the function endpoint.

In your browser, open the RenderSwaggerUI endpoint, which should look like

`http://localhost:7071/api/swagger/ui`

. A page is rendered, based on your OpenAPI definitions.Select

**POST**>**Try it out**, enter values for`hours`

and`capacity`

either as query parameters or in the JSON request body, and select**Execute**.When you enter integer values like 6 for

`hours`

and 2500 for`capacity`

, you get a JSON response that looks like the following example:

Now you have a function that determines the cost-effectiveness of emergency repairs. Next, you publish your project and API definitions to Azure.

## Publish the project to Azure

Before you can publish your project, you must have a function app in your Azure subscription. Visual Studio publishing creates a function app the first time you publish your project. It can also create an API Management instance that integrates with your function app to expose the TurbineRepair API.

In

**Solution Explorer**, right-click the project and select**Publish**and in**Target**, select**Azure**then**Next**.For the

**Specific target**, choose**Azure Function App (Windows)**to create a function app that runs on Windows, then select**Next**.In

**Function Instance**, choose**+ Create a new Azure Function...**.Create a new instance using the values specified in the following table:

Setting Value Description **Name**Globally unique name Name that uniquely identifies your new function app. Accept this name or enter a new name. Valid characters are: `a-z`

,`0-9`

, and`-`

.**Subscription**Your subscription The Azure subscription to use. Accept this subscription or select a new one from the drop-down list. [Resource group](../azure-resource-manager/management/overview)Name of your resource group The resource group in which to create your function app. Select an existing resource group from the drop-down list or choose **New**to create a new resource group.[Plan Type](functions-scale)Consumption When you publish your project to a function app that runs in a [Consumption plan](consumption-plan), you pay only for executions of your functions app. Other hosting plans incur higher costs.**Location**Location of the service Choose a **Location**in a[region](https://azure.microsoft.com/regions/)near you or other services your functions access.[Azure Storage](storage-considerations)General-purpose storage account An Azure Storage account is required by the Functions runtime. Select **New**to configure a general-purpose storage account. You can also choose an existing account that meets the[storage account requirements](storage-considerations#storage-account-requirements).Select

**Create**to create a function app and its related resources in Azure. Status of resource creation is shown in the lower left of the window.Back in

**Functions instance**, make sure that**Run from package file**is checked. Your function app is deployed using[Zip Deploy](functions-deployment-technologies#zip-deploy)with[Run-From-Package](run-functions-from-deployment-package)mode enabled. This deployment method is recommended for your functions project, since it results in better performance.Select

**Next**, and in**API Management**page, also choose**+ Create an API Management API**.Create an

**API in API Management**by using values in the following table:Setting Value Description **API name**TurbineRepair Name for the API. **Subscription name**Your subscription The Azure subscription to use. Accept this subscription or select a new one from the drop-down list. **Resource group**Name of your resource group Select the same resource group as your function app from the drop-down list. **API Management service**New instance Select **New**to create a new API Management instance in the same location in the serverless tier. Select**OK**to create the instance.Select

**Create**to create the API Management instance with the TurbineRepair API from the function integration.Select

**Finish**and after the publish profile creation process completes, select**Close**.Verify the Publish page now says

**Ready to publish**, and then select**Publish**to deploy the package containing your project files to your new function app in Azure.After the deployment completes, the root URL of the function app in Azure is shown in the

**Publish**tab.

## Get the function access key

In the

**Publish**tab, select the ellipses (**...**) next to**Hosting**and select**Open in Azure portal**. The function app you created is opened in the Azure portal in your default browser.Under

**Functions**on the**Overview page**, select >**Turbine**then select**Function keys**.Under

**Function keys**, select the*copy to clipboard*icon next to the**default**key. You can now set this key you copied in API Management so that it can access the function endpoint.

## Configure API Management

In the function app page, expand

**API**and select**API Management**.If the function app isn't already connected to the new API Management instance, select it under

**API Management**, select**API**>**OpenAPI Document on Azure Functions**, make sure**Import functions**is checked, and select**Link API**. Make sure that only**TurbineRepair**is selected for import and then**Select**.Select

**Go to API Management**at the top of the page, and in the API Management instance, expand**APIs**.Under

**APIs**>**All APIs**, select**OpenAPI Document on Azure Functions**>**POST Run**, then under**Inbound processing**select**Add policy**>**Set query parameters**.Below

**Inbound processing**, in**Set query parameters**, type`code`

for**Name**, select**+Value**, paste in the copied function key, and select**Save**. API Management includes the function key when it passes calls through to the function endpoint.

Now that the function key is set, you can call the `turbine`

API endpoint to verify that it works when hosted in Azure.

## Verify the API in Azure

In the API, select the

**Test**tab and then**POST Run**, enter the following code in the**Request body**>**Raw**, and select**Send**:`{ "hours": "6", "capacity": "2500" }`

As before, you can also provide the same values as query parameters.

Select

**Send**, and then view the**HTTP response**to verify the same results are returned from the API.

## Download the OpenAPI definition

If your API works as expected, you can download the OpenAPI definition for the new hosted APIs from API Management.

-
- Under
**APIs**, select**OpenAPI Document on Azure Functions**, select the ellipses (**...**), and select**Export**.

- Under
Choose the means of API export, including OpenAPI files in various formats. You can also

[export APIs from Azure API Management to the Power Platform](../api-management/export-api-power-platform).

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group.

From the Azure portal menu or **Home** page, select **Resource groups**. Then, on the **Resource groups** page, select the group you created.

On the **myResourceGroup** page, make sure that the listed resources are the ones you want to delete.

Select **Delete resource group**, type the name of your group in the text box to confirm, and then select **Delete**.

## Next steps

You've used Visual Studio 2022 to create a function that's self-documenting because of the [OpenAPI Extension](https://github.com/Azure/azure-functions-openapi-extension) and integrated with API Management. You can now refine the definition in API Management in the portal. You can also [learn more about API Management](../api-management/api-management-key-concepts).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings -->

# Manage your function app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, a function app provides the execution context for your individual functions. Function app behaviors apply to all functions hosted by a given function app. All functions in a function app must be of the same [language](supported-languages).

Individual functions in a function app are deployed together and are scaled together. All functions in the same function app share resources, per instance, as the function app scales.

Connection strings, environment variables, and other application settings are defined separately for each function app. Any data that must be shared between function apps should be stored externally in a persisted store.

## Get started in the Azure portal

Note

Because of limitations on editing function code in the [Azure portal](https://portal.azure.com), you should develop your functions locally and publish your code project to a function app in Azure. For more information, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal)

To view the app settings in your function app, follow these steps:

Sign in to the

[Azure portal](https://portal.azure.com)using your Azure account. Search for your function app and select it.In the left pane of your function app, expand

**Settings**, select**Environment variables**, and then select the**App settings**tab.

## Work with application settings

In addition to the predefined app settings used by Azure Functions, you can create any number of app settings, as required by your function code. For more information, see [App settings reference for Azure Functions](functions-app-settings).

These settings are stored encrypted. For more information, see [App settings security](security-concepts#application-settings).

You can manage app settings from the [Azure portal](functions-how-to-use-azure-function-app-settings?tabs=portal#settings), and by using the [Azure CLI](functions-how-to-use-azure-function-app-settings?tabs=azurecli#settings) and [Azure PowerShell](functions-how-to-use-azure-function-app-settings?tabs=powershell#settings). You can also manage app settings from [Visual Studio Code](functions-develop-vs-code#application-settings-in-azure) and from [Visual Studio](functions-develop-vs#function-app-settings).

Note

Changing application settings causes your function app to restart by default across all hosting plans. For zero-downtime deployments when changing settings, use the [Flex Consumption plan](flex-consumption-plan) with [rolling updates as the site update strategy](flex-consumption-site-updates). For other hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments) for guidance on minimizing downtime.

To view your app settings, see [Get started in the Azure portal](#get-started-in-the-azure-portal).

The **App settings** tab maintains settings that are used by your function app:

### Use application settings

The function app settings values can also be read in your code as environment variables. For more information, see the Environment variables section of these language-specific reference articles:

When you develop a function app locally, you must maintain local copies of these values in the *local.settings.json* project file. For more information, see [Local settings file](functions-develop-local#local-settings-file).

## FTPS deployment settings

Azure Functions supports deploying project code to your function app by using FTPS. Because this deployment method requires you to [sync triggers](functions-deployment-technologies#trigger-syncing), it isn't recommended. To securely transfer project files, always use FTPS and not FTP.

To get the credentials required for FTPS deployment, use one of these methods:

You can get the FTPS publishing credentials in the Azure portal by downloading the publishing profile for your function app.

Important

The publishing profile contains important security credentials. Always secure the downloaded file on your local computer.

To download the publishing profile of your function app:

In the

[Azure portal](https://portal.azure.com), locate the page for your function app, expand**Settings**>**Configuration**in the left column.In the

**Configuration**page, select the**General settings**tab and make sure that**SCM Basic Auth Publishing Credentials**is turned**On**. When this setting is**Off**, you can't use publish profiles, so select**On**and then**Save**.Go back to the function app's

**Overview**page, and then select**Get publish profile**.Save and copy the contents of the file.


- In the file, locate the
`publishProfile`

element with the attribute`publishMethod="FTP"`

. In this element, the`publishUrl`

,`userName`

, and`userPWD`

attributes contain the target URL and credentials for FTPS publishing.

## Hosting plan type

When you create a function app, you also create a hosting plan in which the app runs. A plan can have one or more function apps. The functionality, scaling, and pricing of your functions depend on the type of plan. For more information, see [Azure Functions hosting options](functions-scale).

You can determine the type of plan being used by your function app from the Azure portal, or by using the Azure CLI or Azure PowerShell APIs.

The following values indicate the plan type:

| Plan type | Azure portal | Azure CLI/PowerShell |
|---|---|---|
|

**Consumption**`Dynamic`

[Premium](functions-premium-plan)**ElasticPremium**`ElasticPremium`

[Dedicated (App Service)](dedicated-plan)To determine the type of plan used by your function app, see the

**App Service Plan**in the**Overview**page of the function app in the[Azure portal](https://portal.azure.com).To see the pricing tier, select the name of the

**App Service Plan**, and then select**Settings > Properties**from the left pane.

## Plan migration

You can migrate a function app between a Consumption plan and a Premium plan on Windows.

Tip

We recommend you migrate your Consumption plan app to run in a Flex Consumption plan instead of a Premium plan. Migration to the Flex Consumption plan is the only migration option for a Linux Consumption plan app. For more information, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex).

When migrating between plans, keep in mind the following considerations:

- Direct migration to a Dedicated (App Service) plan isn't supported.
- Migration isn't supported on Linux.
- The source plan and the target plan must be in the same resource group and geographical region. For more information, see
[Move an app to another App Service plan](../app-service/app-service-plan-manage#move-an-app-to-another-app-service-plan). - The specific CLI commands depend on the direction of the migration.
- Downtime in your function executions occurs as the function app is migrated between plans.
- State and other app-specific content is maintained, because the same Azure Files share is used by the app both before and after migration.

You can migrate your plan using these tools:

You can use the [Azure portal](https://portal.azure.com) to switch to a different plan.

Choose the direction of the migration for your app on Windows.

## Development limitations in the Azure portal

The following table shows the operating systems and languages that support in-portal editing:

| Language | Flex Consumption | Premium | Dedicated | Consumption |
|---|---|---|---|---|
| C# | ||||
| Java | ||||
| JavaScript (Node.js) | ✔ | ✔ | Windows-only | |
| Python | Linux-only | Linux-only | Linux-only | |
| PowerShell | Windows-only | Windows-only | Windows-only | |
| TypeScript (Node.js) |

Consider these limitations when you develop your functions in the [Azure portal](https://portal.azure.com):

- In-portal editing is supported only for functions that were created or last modified in the Azure portal.
- In-portal editing is supported only for
[JavaScript](functions-reference-node),[PowerShell](functions-reference-powershell),[Python](functions-reference-python), and[C# script](functions-reference-csharp)(in-process) functions. - In-portal editing isn't currently supported by the
[Flex Consumption plan](flex-consumption-plan#considerations). - The ability to run your apps on Linux in a Consumption plan is planned for retirement. For more information, see
[Azure Functions Consumption plan hosting](consumption-plan). - When you deploy code to a function app from outside the Azure portal, you can no longer edit any of the code for that function app in the portal. In this case, just continue using
[local development](functions-develop-local). - For Python, development with custom modules isn't currently supported in the portal. To add custom modules to your function app, you must
[develop your app locally](functions-develop-local). - For compiled C# functions and Java functions, you can create the function app and related resources in the portal. However, you must create the functions code project locally and then publish it to Azure.

When possible, develop your functions locally and publish your code project to a function app in Azure. For more information, see [Code and test Azure Functions locally](functions-develop-local).

## Manually install extensions

C# class library functions can include the NuGet packages for [binding extensions](functions-bindings-register) directly in the class library project. For other non-.NET languages and C# script, you should [use extension bundles](extension-bundles). If you must manually install extensions, you can do so by [using Azure Functions Core Tools](functions-core-tools-reference#func-extensions-install) locally. If you can't use extension bundles and are only able to work in the portal, you need to use [Advanced Tools (Kudu)](#kudu) to manually create the extensions.csproj file directly in the site. Make sure to first remove the `extensionBundle`

element from the *host.json* file.

This same process works for any other file you need to add to your app.

Important

When possible, don't edit files directly in your function app in Azure. We recommend [downloading your app files locally](deployment-zip-push#download-your-function-app-files), using [Core Tools to install extensions](functions-core-tools-reference#func-extensions-install) and other packages, validating your changes, and then [republishing your app using Core Tools](functions-run-local#publish) or one of the other [supported deployment methods](functions-deployment-technologies#deployment-methods).

The Functions editor built into the Azure portal lets you update your function code and configuration files directly in the portal:

Select your function app, then under

**Functions**, select**Functions**.Choose your function and select

**Code + test**under**Developer**.Choose your file to edit and select

**Save**when you finish.

Files in the root of the app, such as function.proj or extensions.csproj need to be created and edited by using the [Advanced Tools (Kudu)](#kudu):

Select your function app, expand

**Development tools**, and then select**Advanced tools**>**Go**.If prompted, sign in to the Source Control Manager (SCM) site with your Azure credentials.

From the

**Debug console**menu, choose**CMD**.Navigate to

`.\site\wwwroot`

, select the plus (**+**) button at the top, and select**New file**.Give the file a name, such as

`extensions.csproj`

, and then press Enter.Select the edit button next to the new file, add or update code in the file, and then select

**Save**.For a project file like

*extensions.csproj*, run the following command to rebuild the extensions project:`dotnet build extensions.csproj`


## Platform features

Function apps run in the Azure App Service platform, which maintains them. As such, your function apps have access to most of the features of Azure's core web hosting platform. When you use the [Azure portal](https://portal.azure.com), the left pane is where you access the many features of the App Service platform that you can use in your function apps.

The following matrix indicates Azure portal feature support by hosting plan and operating system:

| Feature | Consumption plan | Flex Consumption plan | Premium plan | Dedicated plan |
|---|---|---|---|---|
|

Linux:

**X****X**[App Service editor](#editor)Linux:

**X****X**Linux:

**X**Linux:

**X**[Backups](../app-service/manage-backup)**X****X****X**[Console](#console)Linux:

**X****X**Linux: SSH

Linux: SSH

The rest of this article focuses on the following features in the portal that are useful for your function apps:

For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service/configure-common).

### App Service editor

The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike. Choosing this option launches a separate browser tab with a basic editor. This editor enables you to integrate with the Git repository, run and debug code, and modify function app settings. This editor provides an enhanced development environment for your functions compared with the built-in function editor.

We recommend that you consider developing your functions on your local computer. When you develop locally and publish to Azure, your project files are read-only in the Azure portal. For more information, see [Code and test Azure Functions locally](functions-develop-local).

### Console

The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line. Common commands include directory and file creation and navigation, as well as executing batch files and scripts.

When developing locally, we recommend using the [Azure Functions Core Tools](functions-run-local) and the [Azure CLI](/en-us/cli/azure/).

### Advanced tools (Kudu)

The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app. From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables. You can also launch **Kudu** by browsing to the SCM endpoint for your function app, for example: `https://<myfunctionapp>.scm.azurewebsites.net/`

.

### Deployment Center

When you use a source control solution to develop and maintain your functions code, Deployment Center lets you build and deploy from source control. Your project is built and deployed to Azure when you make updates. For more information, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

### Cross-origin resource sharing

To prevent malicious code execution on the client, modern browsers block requests from web applications to resources running in a separate domain. [Cross-origin resource sharing (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS) lets an `Access-Control-Allow-Origin`

header declare which origins are allowed to call endpoints on your function app.

When you configure the **Allowed origins** list for your function app, the `Access-Control-Allow-Origin`

header is automatically added to all responses from HTTP endpoints in your function app.

If there's another domain entry, the wildcard (*) is ignored.

### Authentication

When functions use an HTTP trigger, you can require calls to first be authenticated. App Service supports Microsoft Entra authentication and sign-in with social providers, such as Facebook, Microsoft, and X. For information about configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/overview-authentication-authorization).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-powershell -->

# Azure Functions PowerShell developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides details about how you write Azure Functions using PowerShell.

A PowerShell Azure function (function) is represented as a PowerShell script that executes when triggered. Each function script has a related `function.json`

file that defines how the function behaves, such as how it's triggered and its input and output parameters. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

Like other kinds of functions, PowerShell script functions take in parameters that match the names of all the input bindings defined in the `function.json`

file. A `TriggerMetadata`

parameter is also passed that contains additional information on the trigger that started the function.

This article assumes that you have already read the [Azure Functions developer guide](functions-reference). It also assumes that you completed the [Functions quickstart for PowerShell](how-to-create-function-vs-code?pivot=programming-language-powershell) to create your first PowerShell function.

## Folder structure

The required folder structure for a PowerShell project looks like the following. This default can be changed. For more information, see the [scriptFile](#configure-function-scriptfile) section.

```
PSFunctionApp
| - MyFirstFunction
| | - run.ps1
| | - function.json
| - MySecondFunction
| | - run.ps1
| | - function.json
| - Modules
| | - myFirstHelperModule
| | | - myFirstHelperModule.psd1
| | | - myFirstHelperModule.psm1
| | - mySecondHelperModule
| | | - mySecondHelperModule.psd1
| | | - mySecondHelperModule.psm1
| - local.settings.json
| - host.json
| - requirements.psd1
| - profile.ps1
| - extensions.csproj
| - bin
```


At the root of the project, there's a shared [ host.json](functions-host-json) file that can be used to configure the function app. Each function has a folder with its own code file (.ps1) and binding configuration file (

`function.json`

). The name of the function.json file's parent directory is always the name of your function.Certain bindings require the presence of an `extensions.csproj`

file. Binding extensions, required in [version 2.x and later versions](functions-versions) of the Functions runtime, are defined in the `extensions.csproj`

file, with the actual library files in the `bin`

folder. When developing locally, you must [register binding extensions](extension-bundles). When you develop functions in the Azure portal, this registration is done for you.

In PowerShell Function Apps, you might optionally have a `profile.ps1`

which runs when a function app starts to run (otherwise know as a * cold start*). For more information, see

[PowerShell profile](#powershell-profile).

## Defining a PowerShell script as a function

By default, the Functions runtime looks for your function in `run.ps1`

, where `run.ps1`

shares the same parent directory as its corresponding `function.json`

.

Your script is passed several arguments on execution. To handle these parameters, add a `param`

block to the top of your script as in the following example:

```
# $TriggerMetadata is optional here. If you don't need it, you can safely remove it from the param block
param($MyFirstInputBinding, $MySecondInputBinding, $TriggerMetadata)
```


### TriggerMetadata parameter

The `TriggerMetadata`

parameter is used to supply additional information about the trigger. This metadata varies from binding to binding but they all contain a `sys`

property that contains the following data:

```
$TriggerMetadata.sys
```


| Property | Description | Type |
|---|---|---|
| UtcNow | When, in UTC, the function was triggered | DateTime |
| MethodName | The name of the Function that was triggered | string |
| RandGuid | a unique guid to this execution of the function | string |

Every trigger type has a different set of metadata. For example, the `$TriggerMetadata`

for `QueueTrigger`

contains the `InsertionTime`

, `Id`

, `DequeueCount`

, among other things. For more information on the queue trigger's metadata, go to the [official documentation for queue triggers](functions-bindings-storage-queue-trigger#message-metadata). Check the documentation on the [triggers](functions-triggers-bindings) you're working with to see what comes inside the trigger metadata.

## Bindings

In PowerShell, [bindings](functions-triggers-bindings) are configured and defined in a function's function.json. Functions interact with bindings in many ways.

### Reading trigger and input data

Trigger and input bindings are read as parameters passed to your function. Input bindings have a `direction`

set to `in`

in function.json. The `name`

property defined in `function.json`

is the name of the parameter, in the `param`

block. Since PowerShell uses named parameters for binding, the order of the parameters doesn't matter. However, it's a best practice to follow the order of the bindings defined in the `function.json`

.

```
param($MyFirstInputBinding, $MySecondInputBinding)
```


### Writing output data

In Functions, an output binding has a `direction`

set to `out`

in the function.json. You can write to an output binding by using the `Push-OutputBinding`

cmdlet, which is available to the Functions runtime. In all cases, the `name`

property of the binding as defined in `function.json`

corresponds to the `Name`

parameter of the `Push-OutputBinding`

cmdlet.

The following example shows how to call `Push-OutputBinding`

in your function script:

```
param($MyFirstInputBinding, $MySecondInputBinding)
Push-OutputBinding -Name myQueue -Value $myValue
```


You can also pass in a value for a specific binding through the pipeline.

```
param($MyFirstInputBinding, $MySecondInputBinding)
Produce-MyOutputValue | Push-OutputBinding -Name myQueue
```


`Push-OutputBinding`

behaves differently based on the value specified for `-Name`

:

When the specified name can't be resolved to a valid output binding, then an error is thrown.

When the output binding accepts a collection of values, you can call

`Push-OutputBinding`

repeatedly to push multiple values.When the output binding only accepts a singleton value, calling

`Push-OutputBinding`

a second time raises an error.

#### Push-OutputBinding syntax

The following are valid parameters for calling `Push-OutputBinding`

:

| Name | Type | Position | Description |
|---|---|---|---|
`-Name` |
String | 1 | The name of the output binding you want to set. |
`-Value` |
Object | 2 | The value of the output binding you want to set, which is accepted from the pipeline ByValue. |
`-Clobber` |
SwitchParameter | Named | (Optional) When specified, forces the value to be set for a specified output binding. |

The following common parameters are also supported:

`Verbose`

`Debug`

`ErrorAction`

`ErrorVariable`

`WarningAction`

`WarningVariable`

`OutBuffer`

`PipelineVariable`

`OutVariable`


For more information, see [About CommonParameters](/en-us/powershell/module/microsoft.powershell.core/about/about_commonparameters).

#### Push-OutputBinding example: HTTP responses

An HTTP trigger returns a response using an output binding named `response`

. In the following example, the output binding of `response`

has the value of "output #1":

```
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "output #1"
})
```


Because the output is to HTTP, which accepts a singleton value only, an error is thrown when `Push-OutputBinding`

is called a second time.

```
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "output #2"
})
```


For outputs that only accept singleton values, you can use the `-Clobber`

parameter to override the old value instead of trying to add to a collection. The following example assumes that you have already added a value. By using `-Clobber`

, the response from the following example overrides the existing value to return a value of "output #3":

```
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "output #3"
}) -Clobber
```


#### Push-OutputBinding example: Queue output binding

`Push-OutputBinding`

is used to send data to output bindings, such as an [Azure Queue storage output binding](functions-bindings-storage-queue-output). In the following example, the message written to the queue has a value of "output #1":

```
Push-OutputBinding -Name outQueue -Value "output #1"
```


The output binding for a Storage queue accepts multiple output values. In this case, calling the following example after the first writes to the queue a list with two items: "output #1" and "output #2".

```
Push-OutputBinding -Name outQueue -Value "output #2"
```


The following example, when called after the previous two, adds two more values to the output collection:

```
Push-OutputBinding -Name outQueue -Value @("output #3", "output #4")
```


When written to the queue, the message contains these four values: "output #1", "output #2", "output #3", and "output #4".

#### Get-OutputBinding cmdlet

You can use the `Get-OutputBinding`

cmdlet to retrieve the values currently set for your output bindings. This cmdlet retrieves a hashtable that contains the names of the output bindings with their respective values.

The following example uses `Get-OutputBinding`

to return current binding values:

```
Get-OutputBinding
```


```
Name Value
---- -----
MyQueue myData
MyOtherQueue myData
```


`Get-OutputBinding`

also contains a parameter called `-Name`

, which can be used to filter the returned binding, as in the following example:

```
Get-OutputBinding -Name MyQ*
```


```
Name Value
---- -----
MyQueue myData
```


Wildcards (*) are supported in `Get-OutputBinding`

.

## Logging

Logging in PowerShell functions works like regular PowerShell logging. You can use the logging cmdlets to write to each output stream. Each cmdlet maps to a log level used by Functions.

| Functions logging level | Logging cmdlet |
|---|---|
| Error | `Write-Error` |
| Warning | `Write-Warning` |
| Information | `Write-Information` `Write-Host` `Write-Output` Writes to the `Information` log level. |
| Debug | `Write-Debug` |
| Trace | `Write-Progress` `Write-Verbose` |

In addition to these cmdlets, anything written to the pipeline is redirected to the `Information`

log level and displayed with the default PowerShell formatting.

Important

Using the `Write-Verbose`

or `Write-Debug`

cmdlets isn't enough to see verbose and debug level logging. You must also configure the log level threshold, which declares what level of logs you actually care about. To learn more, see [Configure the function app log level](#configure-the-function-app-log-level).

### Configure the function app log level

Azure Functions lets you define the threshold level to make it easy to control the way Functions writes to the logs. To set the threshold for all traces written to the console, use the `logging.logLevel.default`

property in the [ host.json file](functions-host-json). This setting applies to all functions in your function app.

The following example sets the threshold to enable verbose logging for all functions, but sets the threshold to enable debug logging for a function named `MyFunction`

:

```
{
"logging": {
"logLevel": {
"Function.MyFunction": "Debug",
"default": "Trace"
}
}
}
```


For more information, see [host.json reference](functions-host-json).

### Viewing the logs

If your Function App is running in Azure, you can use Application Insights to monitor it. Read [monitoring Azure Functions](functions-monitoring) to learn more about viewing and querying function logs.

If you're running your Function App locally for development, logs default to the file system. To see the logs in the console, set the `AZURE_FUNCTIONS_ENVIRONMENT`

environment variable to `Development`

before starting the Function App.

## Triggers and bindings types

There are many triggers and bindings available to you to use with your function app. For the full list of triggers and bindings, see [Supported bindings](functions-triggers-bindings#supported-bindings).

All triggers and bindings are represented in code as a few real data types:

- Hashtable
- string
- byte[]
- int
- double
- HttpRequestContext
- HttpResponseContext

The first five types in this list are standard .NET types. The last two are used only by the [HttpTrigger trigger](#http-triggers-and-bindings).

Each binding parameter in your functions must be one of these types.

### HTTP triggers and bindings

HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.

#### Request object

The request object that is passed into the script is of the type `HttpRequestContext`

, which has the following properties:

| Property | Description | Type |
|---|---|---|
`Body` |
An object that contains the body of the request. `Body` is serialized into the best type based on the data. For example, if the data is JSON, it's passed in as a hashtable. If the data is a string, it's passed in as a string. |
object |
`Headers` |
A dictionary that contains the request headers. | Dictionary<string,string>* |
`Method` |
The HTTP method of the request. | string |
`Params` |
An object that contains the routing parameters of the request. | Dictionary<string,string>* |
`Query` |
An object that contains the query parameters. | Dictionary<string,string>* |
`Url` |
The URL of the request. | string |

* All `Dictionary<string,string>`

keys are case-insensitive.

#### Response object

The response object that you should send back is of the type `HttpResponseContext`

, which has the following properties:

| Property | Description | Type |
|---|---|---|
`Body` |
An object that contains the body of the response. | object |
`ContentType` |
A short hand for setting the content type for the response. | string |
`Headers` |
An object that contains the response headers. | Dictionary or Hashtable |
`StatusCode` |
The HTTP status code of the response. | string or int |

#### Accessing the request and response

When you work with HTTP triggers, you can access the HTTP request the same way you would with any other input binding. It's in the `param`

block.

Use an `HttpResponseContext`

object to return a response, as shown in the following example:

`function.json`


```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"authLevel": "anonymous"
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


`run.ps1`


```
param($req, $TriggerMetadata)
$name = $req.Query.Name
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "Hello $name!"
})
```


The result of invoking this function would be:

```
irm http://localhost:5001?Name=Functions
Hello Functions!
```


### Type-casting for triggers and bindings

For certain bindings like the blob binding, you're able to specify the type of the parameter.

For example, to have data from Blob storage supplied as a string, add the following type cast to my `param`

block:

```
param([string] $myBlob)
```


## PowerShell profile

In PowerShell, there's the concept of a PowerShell profile. If you're not familiar with PowerShell profiles, see [About profiles](/en-us/powershell/module/microsoft.powershell.core/about/about_profiles).

In PowerShell Functions, the profile script is executed once per PowerShell worker instance in the app when first deployed and after being idled ([cold start](#cold-start). When concurrency is enabled by setting the [PSWorkerInProcConcurrencyUpperBound](#concurrency) value, the profile script is run for each runspace created.

When you create a function app using tools, such as Visual Studio Code and Azure Functions Core Tools, a default `profile.ps1`

is created for you. The default profile is maintained
[on the Core Tools GitHub repository](https://github.com/Azure/azure-functions-core-tools/blob/main/src/Cli/func/StaticResources/profile.ps1)
and contains:

- Automatic MSI authentication to Azure.
- The ability to turn on the Azure PowerShell
`AzureRM`

PowerShell aliases if you would like.

## PowerShell versions

The following table shows the PowerShell versions available to each major version of the Functions runtime, and the .NET version required:

| Functions version | PowerShell version | .NET version |
|---|---|---|
| 4.x | PowerShell 7.4 | .NET 8 |
| 4.x | PowerShell 7.2 (support ending) | .NET 6 |

You can see the current version by printing `$PSVersionTable`

from any function.

To learn more about Azure Functions runtime support policy, refer to this [article](language-support-policy)

Note

Support for PowerShell 7.2 in Azure Functions ends on November 8, 2024. You might have to resolve some breaking changes when upgrading your PowerShell 7.2 functions to run on PowerShell 7.4. Follow this [migration guide](https://github.com/Azure/azure-functions-powershell-worker/wiki/Upgrading-your-Azure-Function-Apps-to-run-on-PowerShell-7.4) to upgrade to PowerShell 7.4.

### Running local on a specific version

When you run PowerShell functions locally, you need to add the setting `"FUNCTIONS_WORKER_RUNTIME_VERSION" : "7.4"`

to the `Values`

array in the local.setting.json file in the project root. When running locally on PowerShell 7.4, your local.settings.json file looks like the following example:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "",
"FUNCTIONS_WORKER_RUNTIME": "powershell",
"FUNCTIONS_WORKER_RUNTIME_VERSION" : "7.4"
}
}
```


Note

In PowerShell Functions, the value "~7" for FUNCTIONS_WORKER_RUNTIME_VERSION refers to "7.0.x". We don't automatically upgrade PowerShell Function apps that have "~7" to "7.4". Going forward, for PowerShell Function Apps, we require that apps specify both the major and minor version they want to target. It's necessary to mention "7.4" if you want to target "7.4.x"

### Changing the PowerShell version

Take these considerations into account before you migrate your PowerShell function app to PowerShell 7.4:

Because the migration might introduce breaking changes in your app, review this

[migration guide](https://github.com/Azure/azure-functions-powershell-worker/wiki/Upgrading-your-Azure-Function-Apps-to-run-on-PowerShell-7.4)before upgrading your app to PowerShell 7.4.Make sure that your function app is running on the latest version of the Functions runtime in Azure, which is version 4.x. For more information, see

[View the current runtime version](set-runtime-version#view-the-current-runtime-version).

Use the following steps to change the PowerShell version used by your function app. You can perform this operation either in the Azure portal or by using PowerShell.

In the

[Azure portal](https://portal.azure.com), browse to your function app.Under

**Settings**, choose**Configuration**. In the**General settings**tab, locate the**PowerShell version**.Choose your desired

**PowerShell Core version**and select**Save**. When warned about the pending restart choose**Continue**. The function app restarts on the chosen PowerShell version.

Note

Azure Functions support for PowerShell 7.4 is generally available (GA). You might see PowerShell 7.4 still indicated as preview in the Azure portal, but this value will be updated soon to reflect the GA status.

The function app restarts after the change is made to the configuration.

## Dependency management

Managing modules in Azure Functions written in PowerShell can be approached in two ways: using the Managed Dependencies feature or including the modules directly in your app content. Each method has its own advantages, and choosing the right one depends on your specific needs.

### Choosing the right module management approach

**Why use the Managed Dependencies feature?**

**Simplified initial installation**: Automatically handles module installation based on your`requirements.psd1`

file.**Auto-upgrades**: Modules are updated automatically, including security fixes, without requiring manual intervention.

**Why include modules in app content?**

**No dependency on the PowerShell Gallery**: Modules are bundled with your app, eliminating external dependencies.**More control**: Avoids the risk of regressions caused by automatic upgrades, giving you full control over which module versions are used.**Compatibility**: Works on Flex Consumption and is recommended for other Linux SKUs.

### Managed Dependencies feature

The Managed Dependencies feature allows Azure Functions to automatically download and manage PowerShell modules specified in the `requirements.psd1`

file. This feature is enabled by default in new PowerShell function apps.

#### Configuring requirements.psd1

To use Managed Dependencies in Azure Functions with PowerShell, you need to configure a `requirements.psd1`

file. This file specifies the modules your function requires, and Azure Functions automatically downloads and updates these modules to ensure that your environment stays up-to-date.

Here's how to set up and configure the `requirements.psd1`

file:

- Create a
`requirements.psd1`

file in the root directory of your Azure Function if one doesn't already exist. - Define the modules and their versions in a PowerShell data structure.

Example `requirements.psd1`

file:

```
@{
'Az' = '9.*' # Specifies the Az module and will use the latest version with major version 9
}
```


### Including modules in app content

For more control over your module versions and to avoid dependencies on external resources, you can include modules directly in your function app’s content.

To include custom modules:

**Create a**at the root of your function app.`Modules`

folder`mkdir ./Modules`

**Copy modules to the**using one of the following methods:`Modules`

folder**If modules are already available locally**:`Copy-Item -Path /mymodules/mycustommodule -Destination ./Modules -Recurse`

**Using**:`Save-Module`

to retrieve from the PowerShell Gallery`Save-Module -Name MyCustomModule -Path ./Modules`

**Using**:`Save-PSResource`

from the`PSResourceGet`

module`Save-PSResource -Name MyCustomModule -Path ./Modules`


Your function app should have the following structure:

```
PSFunctionApp
| - MyFunction
| | - run.ps1
| | - function.json
| - Modules
| | - MyCustomModule
| | - MyOtherCustomModule
| | - MySpecialModule.psm1
| - local.settings.json
| - host.json
| - requirements.psd1
```


When you start your function app, the PowerShell language worker adds this `Modules`

folder to the `$env:PSModulePath`

so that you can rely on module autoloading just as you would in a regular PowerShell script.

Note

If your function app is under source control, you should confirm that all the content in the Modules folder that you add isn't excluded by .gitignore. For example, if one of your modules has a bin folder that is getting excluded, you would want to modify the .gitignore by replacing `bin`

with

```
**/bin/**
!Modules/**
```


### Troubleshooting Managed Dependencies

#### Enabling Managed Dependencies

In order for Managed Dependencies to function, the feature must be enabled in host.json:

```
{
"managedDependency": {
"enabled": true
}
}
```


#### Target specific versions

When targeting specific module versions, it’s important to follow both of the following steps to ensure the correct module version is loaded:

**Specify the module version in**`requirements.psd1`

:`@{ 'Az.Accounts' = '1.9.5' }`

**Add an import statement to**`profile.ps1`

:`Import-Module Az.Accounts -RequiredVersion '1.9.5'`


Following these steps ensures the specified version is loaded when your function starts.

#### Configure specific Managed Dependency interval settings

You can configure how Managed Dependencies are downloaded and installed using the following app settings:

| Setting | Default Value | Description |
|---|---|---|
MDMaxBackgroundUpgradePeriod |
`7.00:00:00` (seven days) |
Controls the background update period for PowerShell function apps. |
MDNewSnapshotCheckPeriod |
`01:00:00` (one hour) |
Specifies how often the PowerShell worker checks for updates. |
MDMinBackgroundUpgradePeriod |
`1.00:00:00` (one day) |
Minimum time between upgrade checks. |

#### Dependency management considerations

**Internet Access**: Managed Dependencies require access to`https://www.powershellgallery.com`

to download modules. Ensure that your environment allows this access, including modifying firewall/VNet rules as needed. The required endpoints are described in[Troubleshooting Cmdlets](/en-us/powershell/gallery/how-to/getting-support/troubleshooting-cmdlets#required-network-endpoints). These endpoints can be added to the allow list, as required.**License Acceptance**: Managed Dependencies doesn't support modules that require license acceptance.**Flex Consumption Plan**: The Managed Dependencies feature isn't supported in the Flex Consumption plan. Use custom modules instead.**Module Locations**: On your local computer, modules are typically installed in one of the globally available folders in your`$env:PSModulePath`

. When running in Azure, the`$env:PSModulePath`

for a PowerShell function app differs from`$env:PSModulePath`

in a regular PowerShell script and contains both the`Modules`

folder uploaded with your app contents and a separate location managed by Managed Dependencies.

## Environment variables

In Functions, [app settings](functions-app-settings), such as service connection strings, are exposed as environment variables during execution. You can access these settings using `$env:NAME_OF_ENV_VAR`

, as shown in the following example:

```
param($myTimer)
Write-Host "PowerShell timer trigger function ran! $(Get-Date)"
Write-Host $env:AzureWebJobsStorage
Write-Host $env:WEBSITE_SITE_NAME
```


There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

When running locally, app settings are read from the [local.settings.json](functions-develop-local#local-settings-file) project file.

## Concurrency

By default, the Functions PowerShell runtime can only process one invocation of a function at a time. However, this concurrency level might not be sufficient in the following situations:

- When you're trying to handle a large number of invocations at the same time.
- When you have functions that invoke other functions inside the same function app.

There are a few concurrency models that you could explore depending on the type of workload:

Increase

`FUNCTIONS_WORKER_PROCESS_COUNT`

. Increasing this setting allows handling function invocations in multiple processes within the same instance, which introduces certain CPU and memory overhead. In general, I/O-bound functions don't suffer from this overhead. For CPU-bound functions, the impact might be significant.Increase the

`PSWorkerInProcConcurrencyUpperBound`

app setting value. Increasing this setting allows creating multiple runspaces within the same process, which significantly reduces CPU and memory overhead.

You set these environment variables in the [app settings](functions-app-settings) of your function app.

Depending on your use case, Durable Functions might significantly improve scalability. To learn more, see [Durable Functions application patterns](durable/durable-functions-overview?tabs=powershell#application-patterns).

Note

You might get "requests are being queued due to no available runspaces" warnings. This message isn't an error. The message is telling you that requests are being queued. They're handled when the previous requests are completed.

### Considerations for using concurrency

PowerShell is a *single_threaded* scripting language by default. However, concurrency can be added by using multiple PowerShell runspaces in the same process. The number of runspaces created, and therefore the number of concurrent threads per worker, is limited by the `PSWorkerInProcConcurrencyUpperBound`

application setting. By default, the number of runspaces is set to 1,000 in version 4.x of the Functions runtime. In versions 3.x and below, the maximum number of runspaces is set to 1. The throughput of your function app is affected by the amount of CPU and memory available in the selected plan.

Azure PowerShell uses some *process-level* contexts and state to help save you from excess typing. However, if you turn on concurrency in your function app and invoke actions that change state, you could end up with race conditions. These race conditions are difficult to debug because one invocation relies on a certain state and the other invocation changed the state.

There's immense value in concurrency with Azure PowerShell, since some operations can take a considerable amount of time. However, you must proceed with caution. If you suspect that you're experiencing a race condition, set the PSWorkerInProcConcurrencyUpperBound app setting to `1`

and instead use [language worker process level isolation](functions-app-settings#functions_worker_process_count) for concurrency.

## Configure function scriptFile

By default, a PowerShell function is executed from `run.ps1`

, a file that shares the same parent directory as its corresponding `function.json`

.

The `scriptFile`

property in the `function.json`

can be used to get a folder structure that looks like the following example:

```
FunctionApp
| - host.json
| - myFunction
| | - function.json
| - lib
| | - PSFunction.ps1
```


In this case, the `function.json`

for `myFunction`

includes a `scriptFile`

property referencing the file with the exported function to run.

```
{
"scriptFile": "../lib/PSFunction.ps1",
"bindings": [
// ...
]
}
```


## Use PowerShell modules by configuring an entryPoint

PowerShell functions in this article are shown with the default `run.ps1`

script file generated by the templates.
However, you can also include your functions in PowerShell modules. You can reference your specific function code in the module by using the `scriptFile`

and `entryPoint`

fields in the function.json` configuration file.

In this case, `entryPoint`

is the name of a function or cmdlet in the PowerShell module referenced in `scriptFile`

.

Consider the following folder structure:

```
FunctionApp
| - host.json
| - myFunction
| | - function.json
| - lib
| | - PSFunction.psm1
```


Where `PSFunction.psm1`

contains:

```
function Invoke-PSTestFunc {
param($InputBinding, $TriggerMetadata)
Push-OutputBinding -Name OutputBinding -Value "output"
}
Export-ModuleMember -Function "Invoke-PSTestFunc"
```


In this example, the configuration for `myFunction`

includes a `scriptFile`

property that references `PSFunction.psm1`

, which is a PowerShell module in another folder. The `entryPoint`

property references the `Invoke-PSTestFunc`

function, which is the entry point in the module.

```
{
"scriptFile": "../lib/PSFunction.psm1",
"entryPoint": "Invoke-PSTestFunc",
"bindings": [
// ...
]
}
```


With this configuration, the `Invoke-PSTestFunc`

gets executed exactly as a `run.ps1`

would.

## Considerations for PowerShell functions

When you work with PowerShell functions, be aware of the considerations in the following sections.

### Cold Start

When developing Azure Functions in the [serverless hosting model](consumption-plan), cold starts are a reality. *Cold start* refers to period of time it takes for your function app to start running to process a request. Cold start happens more frequently in the Consumption plan because your function app gets shut down during periods of inactivity.

#### Avoid using Install-Module

Running `Install-Module`

in your function script on each invocation can cause performance issues. Instead, use `Save-Module`

or `Save-PSResource`

before publishing your function app to bundle the necessary modules.

For more information, see [Dependency management](#dependency-management).

## Next steps

For more information, see the following resources:
