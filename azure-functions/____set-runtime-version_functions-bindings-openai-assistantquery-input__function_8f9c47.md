---
merged_at: 2026-01-26T21:02:36.327427
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __set-runtime-version_functions-bindings-openai-assistantquery-input__functions-_a155fd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _set-runtime-version_functions-bindings-openai-assistantquery-input.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: set-runtime-version.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/set-runtime-version -->

# How to target Azure Functions runtime versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A function app runs on a specific version of the Azure Functions runtime. By default, function apps are created in the latest 4.x version of the Functions runtime. Your function apps are supported only when they run on a [supported major version](functions-versions). This article explains how to configure a function app in Azure to target, or *pin* to, a specific version when required.

The way that you target a specific version depends on whether you're running Windows or Linux. This version of the article supports Windows. Choose your operating system at the top of the article.

The way that you target a specific version depends on whether you're running Windows or Linux. This version of the article supports Linux. Choose your operating system at the top of the article.

Important

When possible, always run your functions on the latest supported version of the Azure Functions runtime. You should only pin your app to a specific version if you're instructed to do so due to an issue with the latest version. Always move up to the latest runtime version as soon as your functions can run correctly.

During local development, your installed version of Azure Functions Core Tools must match the major runtime version used by the function app in Azure. For more information, see [Core Tools versions](functions-run-local#v2).

## Update your runtime version

When possible, you should always run your function apps on the latest supported version of the Azure Functions runtime. If your function app is currently running on an older version of the runtime, you should migrate your app to version 4.x

When your app has existing functions, you must take precautions before moving to a later major runtime version. The following articles detail breaking changes between major versions, including language-specific breaking changes. They also provide you with step-by-step instructions for a successful migration of your existing function app.

To determine your current runtime version, see [View the current runtime version](#view-the-current-runtime-version).

## View the current runtime version

You can view the current runtime version of your function app in one of these ways:

To view and update the runtime version currently used by a function app, follow these steps:

In the

[Azure portal](https://portal.azure.com), browse to your function app.Expand

**Settings**, and then select**Configuration**.In the

**Function runtime settings**tab, note the**Runtime version**. In this example, the version is set to`~4`

.

## Pin to a specific version

Azure Functions lets you use the `FUNCTIONS_EXTENSION_VERSION`

app setting to target the runtime version used by a given function app. If you specify only the major version (`~4`

), the function app is automatically updated to new minor versions of the runtime as they become available. Minor version updates are done automatically because new minor versions aren't likely to introduce changes that would break your functions.

Linux apps use the [ linuxFxVersion site setting](functions-app-settings#linuxfxversion) along with

`FUNCTIONS_EXTENSION_VERSION`

to determine the correct Linux base image in which to run your functions. When you create a new function app on Linux, the runtime automatically chooses the correct base image for you based on the runtime version of your language stack.Pinning to a specific runtime version causes your function app to restart.

When you specify a specific minor version (such as `4.0.12345`

) in `FUNCTIONS_EXTENSION_VERSION`

, the function app is pinned to that specific version of the runtime until you explicitly choose to move back to automatic version updates. You should only pin to a specific minor version long enough to resolve any issues with your function app that prevent you from targeting the major version. Older minor versions are regularly removed from the production environment. When your function app is pinned to a minor version that is later removed, your function app is instead run on the closest existing version instead of the version set in `FUNCTIONS_EXTENSION_VERSION`

. Minor version removals are announced in [App Service announcements](https://github.com/Azure/app-service-announcements/issues).

Note

When you try to publish from Visual Studio to an app that is pinned to a specific minor version of the runtime, a dialog prompts you to update to the latest version or cancel the publish. To avoid this check when you must use a specific minor version, add the `<DisableFunctionExtensionVersionUpdate>true</DisableFunctionExtensionVersionUpdate>`

property in your `.csproj`

file.

Use one of these methods to temporarily pin your app to a specific version of the runtime:

To view and update the runtime version currently used by a function app, follow these steps:

In the

[Azure portal](https://portal.azure.com), browse to your function app.Expand

**Settings**, and then select**Configuration**.In the

**Function runtime settings**tab, note the**Runtime version**. In this example, the version is set to`~4`

.

To pin your app to a specific minor version, in the left pane, expand

**Settings**, and then select**Environment variables**.From the

**App settings**tab, select**FUNCTIONS_EXTENSION_VERSION**, change**Value**to your required minor version, and then select**Apply**.Select

**Apply**, and then select**Confirm**to apply the changes and restart the app.

The function app restarts after the change is made to the application setting.

To pin your function app to a specific runtime version on Linux, you set a version-specific base image URL in the [ linuxFxVersion site setting](functions-app-settings#linuxfxversion) in the format

`DOCKER|<PINNED_VERSION_IMAGE_URI>`

.Important

Pinned function apps on Linux don't receive regular security and host functionality updates. Unless recommended by a support professional, use the [ FUNCTIONS_EXTENSION_VERSION](functions-app-settings#functions_extension_version) setting and a standard

[value for your language and version, such as](functions-app-settings#linuxfxversion)

`linuxFxVersion`

`Python|3.12`

. For valid values, see the [.](functions-app-settings#linuxfxversion)

`linuxFxVersion`

reference articlePinning to a specific runtime isn't currently supported for Linux function apps running in a Consumption plan.

The following example shows the [ linuxFxVersion](functions-app-settings#linuxfxversion) value required to pin a Node.js 16 function app to a specific runtime version of 4.14.0.3:

`DOCKER|mcr.microsoft.com/azure-functions/node:4.14.0.3-node16`


When needed, a support professional can provide you with a valid base image URI for your application.

Use the following Azure CLI commands to view and set the [ linuxFxVersion](functions-app-settings#linuxfxversion). You can't currently set

[in the portal or by using Azure PowerShell:](functions-app-settings#linuxfxversion)

`linuxFxVersion`

To view the current runtime version, use the

[az functionapp config show](/en-us/cli/azure/functionapp/config)command:`az functionapp config show --name <function_app> \ --resource-group <my_resource_group> --query 'linuxFxVersion' -o tsv`

In this code, replace

`<function_app>`

with the name of your function app. Also, replace`<my_resource_group>`

with the name of the resource group for your function app. The current value ofis returned.`linuxFxVersion`

To update the

setting in the function app, use the`linuxFxVersion`

[az functionapp config set](/en-us/cli/azure/functionapp/config)command:`az functionapp config set --name <FUNCTION_APP> \ --resource-group <RESOURCE_GROUP> \ --linux-fx-version <LINUX_FX_VERSION>`

Replace

`<FUNCTION_APP>`

with the name of your function app. Also, replace`<RESOURCE_GROUP>`

with the name of the resource group for your function app. Finally, replace`<LINUX_FX_VERSION>`

with the value of a specific image provided to you by a support professional.

You can run these commands from the [Azure Cloud Shell](../cloud-shell/overview) by choosing **Open Cloud Shell** in the preceding code examples. You can also use the [Azure CLI locally](/en-us/cli/azure/install-azure-cli) to execute this command after executing [ az login](/en-us/cli/azure/reference-index#az-login) to sign in.

The function app restarts after the change is made to the site config.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-openai-assistantquery-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistantquery-input -->

# Azure OpenAI assistant query input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant query input binding allows you to integrate Assistants API queries into your code executions.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
/// <summary>
/// HTTP GET function that queries the conversation history of the assistant chat bot.
/// </summary>
[Function(nameof(GetChatState))]
public static IActionResult GetChatState(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "assistants/{assistantId}")] HttpRequestData req,
string assistantId,
[AssistantQueryInput("{assistantId}", TimestampUtc = "{Query.timestampUTC}", ChatStorageConnectionSetting = DefaultChatStorageConnectionSetting, CollectionName = DefaultCollectionName)] AssistantState state)
{
return new OkObjectResult(state);
}
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
/*
* HTTP GET function that queries the conversation history of the assistant chat bot.
*/
@FunctionName("GetChatState")
public HttpResponseMessage getChatState(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "assistants/{assistantId}")
HttpRequestMessage<Optional<String>> request,
@BindingName("assistantId") String assistantId,
@AssistantQuery(name = "AssistantState", id = "{assistantId}", timestampUtc = "{Query.timestampUTC}", chatStorageConnectionSetting = DEFAULT_CHATSTORAGE, collectionName = DEFAULT_COLLECTION) AssistantState state,
final ExecutionContext context) {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(state)
.build();
}
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
const { app, input, output } = require("@azure/functions");
const chatBotQueryInput = input.generic({
type: 'assistantQuery',
id: '{assistantId}',
timestampUtc: '{Query.timestampUTC}',
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
})
app.http('GetChatState', {
methods: ['GET'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraInputs: [chatBotQueryInput],
handler: async (_, context) => {
const state = context.extraInputs.get(chatBotQueryInput)
return { status: 200, jsonBody: state }
}
})
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
import { HttpRequest, InvocationContext, app, input, output } from "@azure/functions"
const chatBotQueryInput = input.generic({
type: 'assistantQuery',
id: '{assistantId}',
timestampUtc: '{Query.timestampUTC}',
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
})
app.http('GetChatState', {
methods: ['GET'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraInputs: [chatBotQueryInput],
handler: async (_, context) => {
const state: any = context.extraInputs.get(chatBotQueryInput)
return { status: 200, jsonBody: state }
}
})
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

Here's the *function.json* file for Get Chat State:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"route": "assistants/{assistantId}",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"name": "State",
"type": "assistantQuery",
"direction": "in",
"dataType": "string",
"id": "{assistantId}",
"timestampUtc": "{Query.timestampUTC}",
"chatStorageConnectionSetting": "AzureWebJobsStorage",
"collectionName": "ChatState"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata, $State)
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $State
Headers = @{
"Content-Type" = "application/json"
}
})
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
@apis.function_name("GetChatState")
@apis.route(route="assistants/{assistantId}", methods=["GET"])
@apis.assistant_query_input(
arg_name="state",
id="{assistantId}",
timestamp_utc="{Query.timestampUTC}",
chat_storage_connection_setting=DEFAULT_CHAT_STORAGE_SETTING,
collection_name=DEFAULT_CHAT_COLLECTION_NAME,
)
def get_chat_state(req: func.HttpRequest, state: str) -> func.HttpResponse:
return func.HttpResponse(state, status_code=200, mimetype="application/json")
```


## Attributes

Apply the `AssistantQuery`

attribute to define an assistant query input binding, which supports these parameters:

| Parameter | Description |
|---|---|
Id |
Gets the ID of the assistant to query. |
TimeStampUtc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Annotations

The `assistantQuery`

annotation enables you to define an assistant query input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
id |
Gets the ID of the assistant to query. |
timeStampUtc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Decorators

During the preview, define the input binding as a `generic_input_binding`

binding of type `assistantQuery`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
id |
Gets the ID of the assistant to query. |
time_stamp_utc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `assistantQuery` . |
direction |
Must be `in` . |
name |
The name of the input binding. |
id |
Gets the ID of the assistant to query. |
timeStampUtc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
id |
Gets the ID of the assistant to query. |
timeStampUtc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Usage

See the [Example section](#example) for complete examples.


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-twilio_functions-bindings-rabbitmq-output.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-twilio.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-twilio -->

# Twilio binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to send text messages by using [Twilio](https://www.twilio.com/) bindings in Azure Functions. Azure Functions supports output bindings for Twilio.

This is reference information for Azure Functions developers. If you're new to Azure Functions, start with the following resources:

C# developer references:


## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

There is currently no support for Twilio for an isolated worker process app.

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

## Example

Unless otherwise noted, these examples are specific to version 2.x and later version of the Functions runtime.

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The Twilio binding isn't currently supported for a function app running in an isolated worker process.

The following example shows a Twilio output binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding.

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "twilioSms",
"name": "message",
"accountSidSetting": "TwilioAccountSid",
"authTokenSetting": "TwilioAuthToken",
"from": "+1425XXXXXXX",
"direction": "out",
"body": "Azure Functions Testing"
}
```


Here's the JavaScript code:

```
module.exports = async function (context, myQueueItem) {
context.log('Node.js queue trigger function processed work item', myQueueItem);
// In this example the queue item is a JSON string representing an order that contains the name of a
// customer and a mobile number to send text updates to.
var msg = "Hello " + myQueueItem.name + ", thank you for your order.";
// Even if you want to use a hard coded message in the binding, you must at least
// initialize the message binding.
context.bindings.message = {};
// A dynamic message can be set instead of the body in the output binding. The "To" number
// must be specified in code.
context.bindings.message = {
body : msg,
to : myQueueItem.mobileNumber
};
};
```


Complete PowerShell examples aren't currently available for SendGrid bindings.

The following example shows how to send an SMS message using the output binding as defined in the following *function.json*.

```
{
"type": "twilioSms",
"name": "twilioMessage",
"accountSidSetting": "TwilioAccountSID",
"authTokenSetting": "TwilioAuthToken",
"from": "+1XXXXXXXXXX",
"direction": "out",
"body": "Azure Functions Testing"
}
```


You can pass a serialized JSON object to the `func.Out`

parameter to send the SMS message.

```
import logging
import json
import azure.functions as func
def main(req: func.HttpRequest, twilioMessage: func.Out[str]) -> func.HttpResponse:
message = req.params.get('message')
to = req.params.get('to')
value = {
"body": message,
"to": to
}
twilioMessage.set(json.dumps(value))
return func.HttpResponse(f"Message sent")
```


The following example shows how to use the [TwilioSmsOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.twiliosmsoutput) annotation to send an SMS message. Values for `to`

, `from`

, and `body`

are required in the attribute definition even if you override them programmatically.

```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
public class TwilioOutput {
@FunctionName("TwilioOutput")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = { HttpMethod.GET, HttpMethod.POST },
authLevel = AuthorizationLevel.FUNCTION) HttpRequestMessage<Optional<String>> request,
@TwilioSmsOutput(
name = "twilioMessage",
accountSid = "AzureWebJobsTwilioAccountSID",
authToken = "AzureWebJobsTwilioAuthToken",
to = "+1XXXXXXXXXX",
body = "From Azure Functions",
from = "+1XXXXXXXXXX") OutputBinding<String> twilioMessage,
final ExecutionContext context) {
String message = request.getQueryParameters().get("message");
String to = request.getQueryParameters().get("to");
StringBuilder builder = new StringBuilder()
.append("{")
.append("\"body\": \"%s\",")
.append("\"to\": \"%s\"")
.append("}");
final String body = String.format(builder.toString(), message, to);
twilioMessage.setValue(body);
return request.createResponseBuilder(HttpStatus.OK).body("Message sent").build();
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the output binding. C# script instead uses a [function.json configuration file](#configuration).

The Twilio binding isn't currently supported for a function app running in an isolated worker process.

## Annotations

The [TwilioSmsOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.twiliosmsoutput) annotation allows you to declaratively configure the Twilio output binding by providing the following configuration values:

+

Place the [TwilioSmsOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.twiliosmsoutput) annotation on an [ OutputBinding<T>](/en-us/java/api/com.microsoft.azure.functions.outputbinding) parameter, where

`T`

may be any native Java type such as `int`

, `String`

, `byte[]`

, or a POJO type.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file, which differs by runtime version:

| function.json property | Description |
|---|---|
type |
must be set to `twilioSms` . |
direction |
must be set to `out` . |
name |
Variable name used in function code for the Twilio SMS text message. |
accountSidSetting |
This value must be set to the name of an app setting that holds your Twilio Account Sid (`TwilioAccountSid` ). When not set, the default app setting name is `AzureWebJobsTwilioAccountSid` . |
authTokenSetting |
This value must be set to the name of an app setting that holds your Twilio authentication token (`TwilioAccountAuthToken` ). When not set, the default app setting name is `AzureWebJobsTwilioAuthToken` . |
from |
This value is set to the phone number that the SMS text is sent from. |
body |
This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function. |

In version 2.x, you set the `to`

value in your code.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-rabbitmq-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-rabbitmq-output -->

# RabbitMQ output binding for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the RabbitMQ output binding to send messages to a RabbitMQ queue.

Note

The RabbitMQ bindings are only fully supported on [Elastic Premium](functions-premium-plan) and [Dedicated (App Service)](dedicated-plan) plans. [Flex Consumption](flex-consumption-plan) and [Consumption](consumption-plan) plans aren't yet supported.

RabbitMQ bindings aren't supported by the Azure Functions v1.x runtime.

For information on setup and configuration details, see the [overview](functions-bindings-rabbitmq-output).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

```
[Function(nameof(RabbitMQFunction))]
[RabbitMQOutput(QueueName = "destinationQueue", ConnectionStringSetting = "RabbitMQConnection")]
public static string Run([RabbitMQTrigger("queue", ConnectionStringSetting = "RabbitMQConnection")] string item,
FunctionContext context)
{
var logger = context.GetLogger(nameof(RabbitMQFunction));
logger.LogInformation(item);
var message = $"Output message created at {DateTime.Now}";
return message;
}
```


The following Java function uses the `@RabbitMQOutput`

annotation from the [Java RabbitMQ types](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-rabbitmq) to describe the configuration for a RabbitMQ queue output binding. The function sends a message to the RabbitMQ queue when triggered by a TimerTrigger every 5 minutes.

```
@FunctionName("RabbitMQOutputExample")
public void run(
@TimerTrigger(name = "keepAliveTrigger", schedule = "0 */5 * * * *") String timerInfo,
@RabbitMQOutput(connectionStringSetting = "rabbitMQConnectionAppSetting", queueName = "hello") OutputBinding<String> output,
final ExecutionContext context) {
output.setValue("Some string");
}
```


The following example shows a RabbitMQ output binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding. The function reads in the message from an HTTP trigger and outputs it to the RabbitMQ queue.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"authLevel": "function",
"name": "input",
"methods": [
"get",
"post"
]
},
{
"type": "rabbitMQ",
"name": "outputMessage",
"queueName": "outputQueue",
"connectionStringSetting": "rabbitMQConnectionAppSetting",
"direction": "out"
}
]
}
```


Here's JavaScript code:

```
module.exports = async function (context, input) {
context.bindings.outputMessage = input.body;
};
```


The following example shows a RabbitMQ output binding in a *function.json* file and a Python function that uses the binding. The function reads in the message from an HTTP trigger and outputs it to the RabbitMQ queue.

Here's the binding data in the *function.json* file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get",
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "rabbitMQ",
"name": "outputMessage",
"queueName": "outputQueue",
"connectionStringSetting": "rabbitMQConnectionAppSetting",
"direction": "out"
}
]
}
```


In * _init_.py*:

```
import azure.functions as func
def main(req: func.HttpRequest, outputMessage: func.Out[str]) -> func.HttpResponse:
input_msg = req.params.get('message')
outputMessage.set(input_msg)
return 'OK'
```


## Attributes

Both [isolated worker process](dotnet-isolated-process-guide) and [in-process](functions-dotnet-class-library) C# libraries use an attribute to define an output binding that writes to a RabbitMQ queue.

The `RabbitMQOutputAttribute`

constructor accepts these parameters:

| Parameter | Description |
|---|---|
QueueName |
Name of the queue from which to receive messages. |
HostName |
This parameter is no longer supported and is ignored. It will be removed in a future version. |
ConnectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**UserNameSetting****PasswordSetting****Port**`5672`

.**DisableCertificateValidation**## Annotations

The `RabbitMQOutput`

annotation allows you to create a function that runs when a RabbitMQ message is created.

The annotation supports the following configuration settings:

| Setting | Description |
|---|---|
queueName |
Name of the queue from which to receive messages. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `RabbitMQ` . |
direction |
Must be set to `out` . |
name |
The name of the variable that represents the queue in function code. |
queueName |
Name of the queue to send messages to. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

The parameter type supported by the RabbitMQ trigger depends on the Functions runtime version, the extension package version, and the C# modality used.

The RabbitMQ bindings currently support only string and serializable object types when running in an isolated worker process.

Use the following parameter types for the output binding:

`byte[]`

- If the parameter value is null when the function exits, Functions doesn't create a message.`string`

- If the parameter value is null when the function exits, Functions doesn't create a message.`POJO`

- If the parameter value isn't formatted as a Java object, an error will be received.

The queue message is available via `context.bindings.<NAME>`

where `<NAME>`

matches the name defined in function.json. If the payload is JSON, the value is deserialized into an object.

### Connections

Important

The RabbitMQ binding doesn't support Microsoft Entra authentication and managed identities. You can use Azure Key Vault to centrally managed your RabbitMQ connection strings. To learn more, see [Manage Connections](manage-connections).

Starting with version 2.x of the extension, `hostName`

, `userNameSetting`

, and `passwordSetting`

are no longer supported to define a connection to the RabbitMQ server. You must instead use `connectionStringSetting`

.

The `connectionStringSetting`

property can only accept the name of a key-value pair in app settings. You can't directly set a connection string value in the binding.

For example, when you have set `connectionStringSetting`

to `rabbitMQConnection`

in your binding definition, your function app must have an app setting named `rabbitMQConnection`

that returns either a connection value like `amqp://myuser:***@contoso.rabbitmq.example.com:5672`

or an [Azure Key Vault reference](../app-service/app-service-key-vault-references).

When running locally, you must also have the key value for `connectionStringSetting`

defined in your *local.settings.json* file. Otherwise, your app can't connect to the service from your local computer and an error occurs.


---

<!-- DOCUMENTO FUSIONADO: migrate-version-3-version-4.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/migrate-version-3-version-4 -->

# Migrate apps from Azure Functions version 3.x to version 4.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions version 4.x is highly backwards compatible to version 3.x. Most apps should safely migrate to 4.x without requiring significant code changes. For more information about Functions runtime versions, see [Azure Functions runtime versions overview](functions-versions).

Important

As of December 13, 2022, function apps running on versions 2.x and 3.x of the Azure Functions runtime have reached the end of extended support. For more information, see [Retired versions](functions-versions#retired-versions).

This article walks you through the process of safely migrating your function app to run on version 4.x of the Functions runtime. Because project migration instructions are language dependent, make sure to choose your development language from the selector at the top of the article.

## Identify function apps to migrate

Use the following PowerShell script to generate a list of function apps in your subscription that currently target versions 2.x or 3.x:

```
$Subscription = '<YOUR SUBSCRIPTION ID>'
Set-AzContext -Subscription $Subscription | Out-Null
$FunctionApps = Get-AzFunctionApp
$AppInfo = @{}
foreach ($App in $FunctionApps)
{
if ($App.ApplicationSettings["FUNCTIONS_EXTENSION_VERSION"] -like '*3*')
{
$AppInfo.Add($App.Name, $App.ApplicationSettings["FUNCTIONS_EXTENSION_VERSION"])
}
}
$AppInfo
```


## Choose your target .NET version

On version 3.x of the Functions runtime, your C# function app targets .NET Core 3.1 using the in-process model or .NET 5 using the isolated worker model.

When you migrate your function app, you have the opportunity to choose the target version of .NET. You can update your C# project to one of the following versions of .NET that are supported by Functions version 4.x:

| .NET version |
|
|---|

1,2

[Isolated worker model](dotnet-isolated-process-guide)3[Isolated worker model](dotnet-isolated-process-guide)[Isolated worker model](dotnet-isolated-process-guide),[In-process model](functions-dotnet-class-library)2[See policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework)[Isolated worker model](dotnet-isolated-process-guide)1 The [isolated worker model](dotnet-isolated-process-guide) supports Long Term Support (LTS) and Standard Term Support (STS) versions of .NET, as well as .NET Framework. The [in-process model](functions-dotnet-class-library) only supports LTS releases of .NET, ending with .NET 8. For a full feature and functionality comparison between the two models, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

2 Support ends for the in-process model on November 10, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/in-process-model). For continued full support, you should [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

3 .NET 9 previously had an expected end-of-support date of May 12, 2026. During the .NET 9 service window, the .NET team extended support for STS versions to 24 months, starting with .NET 9. For more information, see [the blog post](https://devblogs.microsoft.com/dotnet/dotnet-sts-releases-supported-for-24-months/).

Tip

**We recommend updating to .NET 8 on the isolated worker model.** .NET 8 is the fully released version with the longest support window from .NET.

Although you can choose to instead use the in-process model, we don't recommend this approach if you can avoid it. [Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model), so you'll need to move to the isolated worker model before then. Doing so while migrating to version 4.x will decrease the total effort required, and the isolated worker model will give your app [additional benefits](dotnet-isolated-in-process-differences), including the ability to more easily target future versions of .NET. If you're moving to the isolated worker model, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can also handle many of the necessary code changes for you.

This guide doesn't present specific examples for .NET 10 (preview) or .NET 9. If you need to target one of those versions, you can adapt the .NET 8 examples.

## Prepare for migration

If you haven't already, identify the list of apps that need to be migrated in your current Azure Subscription by using the [Azure PowerShell](#identify-function-apps-to-migrate).

Before you migrate an app to version 4.x of the Functions runtime, you should do the following tasks:

- Review the list of
[breaking changes between 3.x and 4.x](#breaking-changes-between-3x-and-4x). - Complete the steps in
[Migrate your local project](#migrate-your-local-project)to migrate your local project to version 4.x. - After migrating your project, fully test the app locally using version 4.x of the
[Azure Functions Core Tools](functions-run-local). [Run the pre-upgrade validator](#run-the-pre-upgrade-validator)on the app hosted in Azure, and resolve any identified issues.- Update your function app in Azure to the new version. If you need to minimize downtime, consider using a
[staging slot](functions-deployment-slots)to test and verify your migrated app in Azure on the new runtime version. You can then deploy your app with the updated version settings to the production slot. For more information, see[Update using slots](#update-using-slots). - Publish your migrated project to the updated function app.

When you use Visual Studio to publish a version 4.x project to an existing function app at a lower version, you're prompted to let Visual Studio update the function app to version 4.x during deployment. This update uses the same process defined in [Update without slots](#update-without-slots).

## Migrate your local project

Upgrading instructions are language dependent. If you don't see your language, choose it from the selector at the [top of the article](#top).

Choose the tab that matches your target version of .NET and the desired process model (in-process or isolated worker process).

Tip

If you're moving to an LTS or STS version of .NET using the isolated worker model, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can be used to automatically make many of the changes mentioned in the following sections.

### Project file

The following example is a `.csproj`

project file that uses .NET Core 3.1 on version 3.x:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netcoreapp3.1</TargetFramework>
<AzureFunctionsVersion>v3</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="3.0.13" />
</ItemGroup>
<ItemGroup>
<Reference Include="Microsoft.CSharp" />
</ItemGroup>
<ItemGroup>
<None Update="host.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
</None>
<None Update="local.settings.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
<CopyToPublishDirectory>Never</CopyToPublishDirectory>
</None>
</ItemGroup>
</Project>
```


Use one of the following procedures to update this XML file to run in Functions version 4.x:

These steps assume a local C# project; if your app instead uses C# script (*.csx* files), you should [convert to the project model](functions-reference-csharp#convert-a-c-script-app-to-a-c-project) before continuing.

The following changes are required in the *.csproj* XML project file:

Set the value of

`PropertyGroup`

.`TargetFramework`

to`net8.0`

.Set the value of

`PropertyGroup`

.`AzureFunctionsVersion`

to`v4`

.Add the following

`OutputType`

element to the`PropertyGroup`

:`<OutputType>Exe</OutputType>`

In the

`ItemGroup`

.`PackageReference`

list, replace the package reference to`Microsoft.NET.Sdk.Functions`

with the following references:`<FrameworkReference Include="Microsoft.AspNetCore.App" /> <PackageReference Include="Microsoft.Azure.Functions.Worker" Version="1.21.0" /> <PackageReference Include="Microsoft.Azure.Functions.Worker.Sdk" Version="1.17.2" /> <PackageReference Include="Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore" Version="1.2.1" /> <PackageReference Include="Microsoft.ApplicationInsights.WorkerService" Version="2.22.0" /> <PackageReference Include="Microsoft.Azure.Functions.Worker.ApplicationInsights" Version="1.2.0" />`

Make note of any references to other packages in the

`Microsoft.Azure.WebJobs.*`

namespaces. You'll replace these packages in a later step.Add the following new

`ItemGroup`

:`<ItemGroup> <Using Include="System.Threading.ExecutionContext" Alias="ExecutionContext"/> </ItemGroup>`


After you make these changes, your updated project should look like the following example:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
<RootNamespace>My.Namespace</RootNamespace>
<OutputType>Exe</OutputType>
<ImplicitUsings>enable</ImplicitUsings>
<Nullable>enable</Nullable>
</PropertyGroup>
<ItemGroup>
<FrameworkReference Include="Microsoft.AspNetCore.App" />
<PackageReference Include="Microsoft.Azure.Functions.Worker" Version="1.21.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.Sdk" Version="1.17.2" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore" Version="1.2.1" />
<PackageReference Include="Microsoft.ApplicationInsights.WorkerService" Version="2.22.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.ApplicationInsights" Version="1.2.0" />
<!-- Other packages may also be in this list -->
</ItemGroup>
<ItemGroup>
<None Update="host.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
</None>
<None Update="local.settings.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
<CopyToPublishDirectory>Never</CopyToPublishDirectory>
</None>
</ItemGroup>
<ItemGroup>
<Using Include="System.Threading.ExecutionContext" Alias="ExecutionContext"/>
</ItemGroup>
</Project>
```


### Package and namespace changes

Based on the model you're migrating to, you might need to update or change the packages your application references. When you adopt the target packages, you then need to update the namespace of using statements and some types you reference. You can see the effect of these namespace changes on `using`

statements in the [HTTP trigger template examples](#http-trigger-template) later in this article.

If you haven't already, update your project to reference the latest stable versions of:

Depending on the triggers and bindings your app uses, your app might need to reference a different set of packages. The following table shows the replacements for some of the most commonly used extensions:

| Scenario | Changes to package references |
|---|---|
| Timer trigger | Add
|
| Storage bindings | Replace`Microsoft.Azure.WebJobs.Extensions.Storage` with
|
| Blob bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Storage.Blobs` with the latest version of
|
| Queue bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Storage.Queues` with the latest version of
|
| Table bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Tables` with the latest version of
|
| Cosmos DB bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.CosmosDB` and/or `Microsoft.Azure.WebJobs.Extensions.DocumentDB` with the latest version of
|
| Service Bus bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.ServiceBus` with the latest version of
|
| Event Hubs bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.EventHubs` with the latest version of
|
| Event Grid bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.EventGrid` with the latest version of
|
| SignalR Service bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.SignalRService` with the latest version of
|
| Durable Functions | Replace references to`Microsoft.Azure.WebJobs.Extensions.DurableTask` with the latest version of
|
| Durable Functions (SQL storage provider) |
Replace references to`Microsoft.DurableTask.SqlServer.AzureFunctions` with the latest version of
|
| Durable Functions (Netherite storage provider) |
Replace references to`Microsoft.Azure.DurableTask.Netherite.AzureFunctions` with the latest version of
|
| SendGrid bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.SendGrid` with the latest version of
|
| Kafka bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Kafka` with the latest version of
|
| RabbitMQ bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.RabbitMQ` with the latest version of
|
| Dependency injection and startup config |
Remove references to`Microsoft.Azure.Functions.Extensions` (The isolated worker model provides this functionality by default.) |

See [Supported bindings](functions-triggers-bindings#supported-bindings) for a complete list of extensions to consider, and consult each extension's documentation for full installation instructions for the isolated process model. Be sure to install the latest stable version of any packages you are targeting.

Tip

Any changes to extension versions during this process might require you to update your `host.json`

file as well. Be sure to read the documentation of each extension that you use.
For example, the Service Bus extension has breaking changes in the structure between versions 4.x and 5.x. For more information, see [Azure Service Bus bindings for Azure Functions](/en-us/azure/azure-functions/functions-bindings-service-bus?tabs=isolated-process%2Cextensionv5%2Cextensionv3&pivots=programming-language-csharp#hostjson-settings).

**Your isolated worker model application should not reference any packages in the Microsoft.Azure.WebJobs.* namespaces or Microsoft.Azure.Functions.Extensions.** If you have any remaining references to these, they should be removed.


Tip

Your app might also depend on Azure SDK types, either as part of your triggers and bindings or as a standalone dependency. You should take this opportunity to update these as well. The latest versions of the Functions extensions work with the latest versions of the [Azure SDK for .NET](/en-us/dotnet/azure/sdk/azure-sdk-for-dotnet), almost all of the packages for which are the form `Azure.*`

.

### Program.cs file

When migrating to run in an isolated worker process, you must add the following program.cs file to your project:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
var host = new HostBuilder()
.ConfigureFunctionsWebApplication()
.ConfigureServices(services => {
services.AddApplicationInsightsTelemetryWorkerService();
services.ConfigureFunctionsApplicationInsights();
})
.Build();
host.Run();
```


This example includes [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) to improve performance and provide a familiar programming model when your app uses HTTP triggers. If you don't intend to use HTTP triggers, you can replace the call to `ConfigureFunctionsWebApplication`

with a call to `ConfigureFunctionsWorkerDefaults`

. If you do so, you can remove the reference to `Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore`

from your project file. However, for the best performance, even for functions with other trigger types, you should keep the `FrameworkReference`

to ASP.NET Core.

The *Program.cs* file replaces any file that has the `FunctionsStartup`

attribute, which is typically a *Startup.cs* file. In places where your `FunctionsStartup`

code would reference `IFunctionsHostBuilder.Services`

, you can instead add statements within the `.ConfigureServices()`

method of the `HostBuilder`

in your *Program.cs*. To learn more about working with *Program.cs*, see [Start-up and configuration](dotnet-isolated-process-guide#start-up-and-configuration) in the isolated worker model guide.

The default *Program.cs* examples previously described include setup of [Application Insights](dotnet-isolated-process-guide#application-insights). In your *Program.cs*, you must also configure any log filtering that should apply to logs coming from code in your project. In the isolated worker model, the *host.json* file only controls events emitted by the Functions host runtime. If you don't configure filtering rules in *Program.cs*, you might see differences in the log levels present for various categories in your telemetry.

Although you can register custom configuration sources as part of the `HostBuilder`

, these similarly apply only to code in your project. The platform also needs trigger and binding configuration, and this should be provided through the [application settings](../app-service/configure-common#configure-app-settings), [Key Vault references](../app-service/app-service-key-vault-references?toc=/azure/azure-functions/toc.json), or [App Configuration references](../app-service/app-service-configuration-references?toc=/azure/azure-functions/toc.json) features.

After you move everything from any existing `FunctionsStartup`

to the *Program.cs* file, you can delete the `FunctionsStartup`

attribute and the class it was applied to.

### local.settings.json file

The local.settings.json file is only used when running locally. For information, see [Local settings file](functions-develop-local#local-settings-file).

When you migrate to version 4.x, make sure that your local.settings.json file has at least the following elements:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "AzureWebJobsStorageConnectionStringValue",
"FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated"
}
}
```


Note

When migrating from running in-process to running in an isolated worker process, you need to change the `FUNCTIONS_WORKER_RUNTIME`

value to "dotnet-isolated".

### host.json file

No changes are required to your `host.json`

file. However, if your Application Insights configuration in this file from your in-process model project, you might want to make other changes in your `Program.cs`

file. The `host.json`

file only controls logging from the Functions host runtime, and in the isolated worker model, some of these logs come from your application directly, giving you more control. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### Class name changes

Some key classes changed names between versions. These changes are a result either of changes in .NET APIs or in differences between in-process and isolated worker process. The following table indicates key .NET classes used by Functions that could change when migrating:

| .NET Core 3.1 | .NET 5 | .NET 8 |
|---|---|---|
`FunctionName` (attribute) |
`Function` (attribute) |
`Function` (attribute) |
`ILogger` |
`ILogger` |
`ILogger` , `ILogger<T>` |
`HttpRequest` |
`HttpRequestData` |
`HttpRequestData` , `HttpRequest` (using
|
`IActionResult` |
`HttpResponseData` |
`HttpResponseData` , `IActionResult` (using
|
`FunctionsStartup` (attribute) |
Uses
`Program.cs` |

[instead](#programcs-file)`Program.cs`

There might also be class name differences in bindings. For more information, see the reference articles for the specific bindings.

### Other code changes

This section highlights other code changes to consider as you work through the migration. These changes aren't needed by all applications, but you should evaluate if any are relevant to your scenarios. Make sure to check [Breaking changes between 3.x and 4.x](#breaking-changes-between-3x-and-4x) for other changes you might need to make to your project.

#### JSON serialization

By default, the isolated worker model uses *System.Text.Json* for JSON serialization. To customize serializer options or switch to JSON.NET (*Newtonsoft.Json*), see [Customizing JSON serialization](dotnet-isolated-process-guide#customizing-json-serialization).

#### Application Insights log levels and filtering

Logs can be sent to Application Insights from both the Functions host runtime and code in your project. The *host.json* allows you to configure rules for host logging, but to control logs coming from your code, you need to configure filtering rules as part of your *Program.cs*. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### HTTP trigger template

The differences between in-process and isolated worker process can be seen in HTTP triggered functions. The HTTP trigger template for version 3.x (in-process) looks like the following example:

```
using System;
using System.IO;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace Company.Function
{
public static class HttpTriggerCSharp
{
[FunctionName("HttpTriggerCSharp")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.AuthLevelValue, "get", "post", Route = null)] HttpRequest req,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string name = req.Query["name"];
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic data = JsonConvert.DeserializeObject(requestBody);
name = name ?? data?.name;
string responseMessage = string.IsNullOrEmpty(name)
? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
: $"Hello, {name}. This HTTP triggered function executed successfully.";
return new OkObjectResult(responseMessage);
}
}
}
```


The HTTP trigger template for the migrated version looks like the following example:

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace Company.Function
{
public class HttpTriggerCSharp
{
private readonly ILogger<HttpTriggerCSharp> _logger;
public HttpTriggerCSharp(ILogger<HttpTriggerCSharp> logger)
{
_logger = logger;
}
[Function("HttpTriggerCSharp")]
public IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get")] HttpRequest req)
{
_logger.LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult($"Welcome to Azure Functions, {req.Query["name"]}!");
}
}
}
```


To update your project to Azure Functions 4.x:

Update your local installation of

[Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools)to version 4.x.Update your app's

[Azure Functions extensions bundle](extension-bundles)to 2.x or above. For more information, see[breaking changes](#breaking-changes-between-3x-and-4x).

If needed, move to one of the

[Java versions supported on version 4.x](functions-reference-java#supported-versions).Update the app's

`POM.xml`

file to modify the`FUNCTIONS_EXTENSION_VERSION`

setting to`~4`

, as in the following example:`<configuration> <resourceGroup>${functionResourceGroup}</resourceGroup> <appName>${functionAppName}</appName> <region>${functionAppRegion}</region> <appSettings> <property> <name>WEBSITE_RUN_FROM_PACKAGE</name> <value>1</value> </property> <property> <name>FUNCTIONS_EXTENSION_VERSION</name> <value>~4</value> </property> </appSettings> </configuration>`


- If needed, move to one of the
[Node.js versions supported on version 4.x](functions-reference-node#node-version).

- Take this opportunity to upgrade to PowerShell 7.2, which is recommended. For more information, see
[PowerShell versions](functions-reference-powershell#powershell-versions).

- If you're using Python 3.6, move to one of the
[supported versions](functions-reference-python#supported-python-versions).

### Run the pre-upgrade validator

Azure Functions provides a pre-upgrade validator to help you identify potential issues when migrating your function app to 4.x. To run the pre-upgrade validator:

In the

[Azure portal](https://portal.azure.com), navigate to your function app.Open the

**Diagnose and solve problems**page.In

**Function App Diagnostics**, start typing`Functions 4.x Pre-Upgrade Validator`

and then choose it from the list.After validation completes, review the recommendations and address any issues in your app. If you need to make changes to your app, make sure to validate the changes against version 4.x of the Functions runtime, either

[locally using Azure Functions Core Tools v4](#migrate-your-local-project)or by[using a staging slot](#update-using-slots).

## Update your function app in Azure

You need to update the runtime of the function app host in Azure to version 4.x before you publish your migrated project. The runtime version used by the Functions host is controlled by the `FUNCTIONS_EXTENSION_VERSION`

application setting, but in some cases other settings must also be updated. Both code changes and changes to application settings require your function app to restart.

The easiest way is to [update without slots](#update-without-slots) and then republish your app project. You can also minimize the downtime in your app and simplify rollback by [updating using slots](#update-using-slots).

### Update without slots

The simplest way to update to v4.x is to set the `FUNCTIONS_EXTENSION_VERSION`

application setting to `~4`

on your function app in Azure. You must follow a [different procedure](#update-using-slots) on a site with slots.

```
az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~4 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>
```


You must also set another setting, which differs between Windows and Linux.

When running on Windows, you also need to enable .NET 8.0, which is required by version 4.x of the runtime.

```
az functionapp config set --net-framework-version v8.0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>
```


.NET 6 is required for function apps in any language running on Windows.

In this example, replace `<APP_NAME>`

with the name of your function app and `<RESOURCE_GROUP_NAME>`

with the name of the resource group.

You can now republish your app project that has been migrated to run on version 4.x.

### Update using slots

Using [deployment slots](functions-deployment-slots) is a good way to update your function app to the v4.x runtime from a previous version. By using a staging slot, you can run your app on the new runtime version in the staging slot and switch to production after verification. Slots also provide a way to minimize downtime during the update. If you need to minimize downtime, follow the steps in [Minimum downtime update](#minimum-downtime-update).

After you've verified your app in the updated slot, you can swap the app and new version settings into production. This swap requires setting [ WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0](functions-app-settings#website_override_sticky_extension_versions) in the production slot. How you add this setting affects the amount of downtime required for the update.

#### Standard update

If your slot-enabled function app can handle the downtime of a full restart, you can update the `WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS`

setting directly in the production slot. Because changing this setting directly in the production slot causes a restart that impacts availability, consider doing this change at a time of reduced traffic. You can then swap in the updated version from the staging slot.

The [ Update-AzFunctionAppSetting](/en-us/powershell/module/az.functions/update-azfunctionappsetting) PowerShell cmdlet doesn't currently support slots. You must use Azure CLI or the Azure portal.

Use the following command to set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

in the production slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>`

In this example, replace

`<APP_NAME>`

with the name of your function app and`<RESOURCE_GROUP_NAME>`

with the name of the resource group. This command causes the app running in the production slot to restart.Use the following command to also set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS`

in the staging slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Use the following command to change

`FUNCTIONS_EXTENSION_VERSION`

and update the staging slot to the new runtime version:`az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~4 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Version 4.x of the Functions runtime requires .NET 6 in Windows. On Linux, .NET apps must also update to .NET 6. Use the following command so that the runtime can run on .NET 6:

When running on Windows, you also need to enable .NET 8.0, which is required by version 4.x of the runtime.

`az functionapp config set --net-framework-version v8.0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>`

.NET 6 is required for function apps in any language running on Windows.

In this example, replace

`<APP_NAME>`

with the name of your function app and`<RESOURCE_GROUP_NAME>`

with the name of the resource group.If your code project required any updates to run on version 4.x, deploy those updates to the staging slot now.

Confirm that your function app runs correctly in the updated staging environment before swapping.

Use the following command to swap the updated staging slot to production:

`az functionapp deployment slot swap -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME> --target-slot production`


#### Minimum downtime update

To minimize the downtime in your production app, you can swap the `WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS`

setting from the staging slot into production. After that, you can swap in the updated version from a prewarmed staging slot.

Use the following command to set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

in the staging slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Use the following commands to swap the slot with the new setting into production, and at the same time restore the version setting in the staging slot.

`az functionapp deployment slot swap -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME> --target-slot production az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~3 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

You may see errors from the staging slot during the time between the swap and the runtime version being restored on staging. This error can happen because having

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

only in staging during a swap removes the`FUNCTIONS_EXTENSION_VERSION`

setting in staging. Without the version setting, your slot is in a bad state. Updating the version in the staging slot right after the swap should put the slot back into a good state, and you call roll back your changes if needed. However, any rollback of the swap also requires you to directly remove`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

from production before the swap back to prevent the same errors in production seen in staging. This change in the production setting would then cause a restart.Use the following command to again set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

in the staging slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

At this point, both slots have

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

set.Use the following command to change

`FUNCTIONS_EXTENSION_VERSION`

and update the staging slot to the new runtime version:`az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~4 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Version 4.x of the Functions runtime requires .NET 6 in Windows. On Linux, .NET apps must also update to .NET 6. Use the following command so that the runtime can run on .NET 6:

When running on Windows, you also need to enable .NET 8.0, which is required by version 4.x of the runtime.

`az functionapp config set --net-framework-version v8.0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>`

.NET 6 is required for function apps in any language running on Windows.

In this example, replace

`<APP_NAME>`

with the name of your function app and`<RESOURCE_GROUP_NAME>`

with the name of the resource group.If your code project required any updates to run on version 4.x, deploy those updates to the staging slot now.

Confirm that your function app runs correctly in the updated staging environment before swapping.

Use the following command to swap the updated and prewarmed staging slot to production:

`az functionapp deployment slot swap -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME> --target-slot production`


## Breaking changes between 3.x and 4.x

The following are key breaking changes to be aware of before upgrading a 3.x app to 4.x, including language-specific breaking changes. For a full list, see Azure Functions GitHub issues labeled [ Breaking Change: Approved](https://github.com/Azure/azure-functions/issues?q=is%3Aissue+label%3A%22Breaking+Change%3A+Approved%22+is%3A%22closed+OR+open%22).

If you don't see your programming language, go select it from the [top of the page](#top).

### Runtime

Azure Functions Proxies was a feature in versions 1.x through 3.x of the Azure Functions runtime. This feature isn't supported in version 4.x. For more information, see

[Serverless REST APIs using Azure Functions](functions-proxies).Logging to Azure Storage using

*AzureWebJobsDashboard*is no longer supported in 4.x. You should instead use[Application Insights](functions-monitoring). ([#1923](https://github.com/Azure/Azure-Functions/issues/1923))Azure Functions 4.x now enforces

[minimum version requirements for extensions](functions-versions#minimum-extension-versions). Update to the latest version of affected extensions. For non-.NET languages,[update](extension-bundles)to extension bundle version 2.x or later. ([#1987](https://github.com/Azure/Azure-Functions/issues/1987))Default and maximum timeouts are now enforced in 4.x for function apps running on Linux in a Consumption plan. (

[#1915](https://github.com/Azure/Azure-Functions/issues/1915))Azure Functions 4.x uses

`Azure.Identity`

and`Azure.Security.KeyVault.Secrets`

for the Key Vault provider and has deprecated the use of Microsoft.Azure.KeyVault. For more information about how to configure function app settings, see the Key Vault option in[Manage key storage](function-keys-how-to#manage-key-storage). ([#2048](https://github.com/Azure/Azure-Functions/issues/2048))Function apps that share storage accounts now fail to start when their host IDs are the same. For more information, see

[Host ID considerations](storage-considerations#host-id-considerations). ([#2049](https://github.com/Azure/Azure-Functions/issues/2049))

Azure Functions 4.x supports newer versions of .NET. See

[Supported languages in Azure Functions](supported-languages)for a full list of versions.`InvalidHostServicesException`

is now a fatal error. ([#2045](https://github.com/Azure/Azure-Functions/issues/2045))`EnableEnhancedScopes`

is enabled by default. ([#1954](https://github.com/Azure/Azure-Functions/issues/1954))Remove

`HttpClient`

as a registered service. ([#1911](https://github.com/Azure/Azure-Functions/issues/1911))

- Default thread count has been updated. Functions that aren't thread-safe or have high memory usage could be impacted. (
[#1962](https://github.com/Azure/Azure-Functions/issues/1962))

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/migrate-version-3-version-4 -->

# Migrate apps from Azure Functions version 3.x to version 4.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions version 4.x is highly backwards compatible to version 3.x. Most apps should safely migrate to 4.x without requiring significant code changes. For more information about Functions runtime versions, see [Azure Functions runtime versions overview](functions-versions).

Important

As of December 13, 2022, function apps running on versions 2.x and 3.x of the Azure Functions runtime have reached the end of extended support. For more information, see [Retired versions](functions-versions#retired-versions).

This article walks you through the process of safely migrating your function app to run on version 4.x of the Functions runtime. Because project migration instructions are language dependent, make sure to choose your development language from the selector at the top of the article.

## Identify function apps to migrate

Use the following PowerShell script to generate a list of function apps in your subscription that currently target versions 2.x or 3.x:

```
$Subscription = '<YOUR SUBSCRIPTION ID>'
Set-AzContext -Subscription $Subscription | Out-Null
$FunctionApps = Get-AzFunctionApp
$AppInfo = @{}
foreach ($App in $FunctionApps)
{
if ($App.ApplicationSettings["FUNCTIONS_EXTENSION_VERSION"] -like '*3*')
{
$AppInfo.Add($App.Name, $App.ApplicationSettings["FUNCTIONS_EXTENSION_VERSION"])
}
}
$AppInfo
```


## Choose your target .NET version

On version 3.x of the Functions runtime, your C# function app targets .NET Core 3.1 using the in-process model or .NET 5 using the isolated worker model.

When you migrate your function app, you have the opportunity to choose the target version of .NET. You can update your C# project to one of the following versions of .NET that are supported by Functions version 4.x:

| .NET version |
|
|---|

1,2

[Isolated worker model](dotnet-isolated-process-guide)3[Isolated worker model](dotnet-isolated-process-guide)[Isolated worker model](dotnet-isolated-process-guide),[In-process model](functions-dotnet-class-library)2[See policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework)[Isolated worker model](dotnet-isolated-process-guide)1 The [isolated worker model](dotnet-isolated-process-guide) supports Long Term Support (LTS) and Standard Term Support (STS) versions of .NET, as well as .NET Framework. The [in-process model](functions-dotnet-class-library) only supports LTS releases of .NET, ending with .NET 8. For a full feature and functionality comparison between the two models, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

2 Support ends for the in-process model on November 10, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/in-process-model). For continued full support, you should [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

3 .NET 9 previously had an expected end-of-support date of May 12, 2026. During the .NET 9 service window, the .NET team extended support for STS versions to 24 months, starting with .NET 9. For more information, see [the blog post](https://devblogs.microsoft.com/dotnet/dotnet-sts-releases-supported-for-24-months/).

Tip

**We recommend updating to .NET 8 on the isolated worker model.** .NET 8 is the fully released version with the longest support window from .NET.

Although you can choose to instead use the in-process model, we don't recommend this approach if you can avoid it. [Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model), so you'll need to move to the isolated worker model before then. Doing so while migrating to version 4.x will decrease the total effort required, and the isolated worker model will give your app [additional benefits](dotnet-isolated-in-process-differences), including the ability to more easily target future versions of .NET. If you're moving to the isolated worker model, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can also handle many of the necessary code changes for you.

This guide doesn't present specific examples for .NET 10 (preview) or .NET 9. If you need to target one of those versions, you can adapt the .NET 8 examples.

## Prepare for migration

If you haven't already, identify the list of apps that need to be migrated in your current Azure Subscription by using the [Azure PowerShell](#identify-function-apps-to-migrate).

Before you migrate an app to version 4.x of the Functions runtime, you should do the following tasks:

- Review the list of
[breaking changes between 3.x and 4.x](#breaking-changes-between-3x-and-4x). - Complete the steps in
[Migrate your local project](#migrate-your-local-project)to migrate your local project to version 4.x. - After migrating your project, fully test the app locally using version 4.x of the
[Azure Functions Core Tools](functions-run-local). [Run the pre-upgrade validator](#run-the-pre-upgrade-validator)on the app hosted in Azure, and resolve any identified issues.- Update your function app in Azure to the new version. If you need to minimize downtime, consider using a
[staging slot](functions-deployment-slots)to test and verify your migrated app in Azure on the new runtime version. You can then deploy your app with the updated version settings to the production slot. For more information, see[Update using slots](#update-using-slots). - Publish your migrated project to the updated function app.

When you use Visual Studio to publish a version 4.x project to an existing function app at a lower version, you're prompted to let Visual Studio update the function app to version 4.x during deployment. This update uses the same process defined in [Update without slots](#update-without-slots).

## Migrate your local project

Upgrading instructions are language dependent. If you don't see your language, choose it from the selector at the [top of the article](#top).

Choose the tab that matches your target version of .NET and the desired process model (in-process or isolated worker process).

Tip

If you're moving to an LTS or STS version of .NET using the isolated worker model, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can be used to automatically make many of the changes mentioned in the following sections.

### Project file

The following example is a `.csproj`

project file that uses .NET Core 3.1 on version 3.x:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netcoreapp3.1</TargetFramework>
<AzureFunctionsVersion>v3</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="3.0.13" />
</ItemGroup>
<ItemGroup>
<Reference Include="Microsoft.CSharp" />
</ItemGroup>
<ItemGroup>
<None Update="host.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
</None>
<None Update="local.settings.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
<CopyToPublishDirectory>Never</CopyToPublishDirectory>
</None>
</ItemGroup>
</Project>
```


Use one of the following procedures to update this XML file to run in Functions version 4.x:

These steps assume a local C# project; if your app instead uses C# script (*.csx* files), you should [convert to the project model](functions-reference-csharp#convert-a-c-script-app-to-a-c-project) before continuing.

The following changes are required in the *.csproj* XML project file:

Set the value of

`PropertyGroup`

.`TargetFramework`

to`net8.0`

.Set the value of

`PropertyGroup`

.`AzureFunctionsVersion`

to`v4`

.Add the following

`OutputType`

element to the`PropertyGroup`

:`<OutputType>Exe</OutputType>`

In the

`ItemGroup`

.`PackageReference`

list, replace the package reference to`Microsoft.NET.Sdk.Functions`

with the following references:`<FrameworkReference Include="Microsoft.AspNetCore.App" /> <PackageReference Include="Microsoft.Azure.Functions.Worker" Version="1.21.0" /> <PackageReference Include="Microsoft.Azure.Functions.Worker.Sdk" Version="1.17.2" /> <PackageReference Include="Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore" Version="1.2.1" /> <PackageReference Include="Microsoft.ApplicationInsights.WorkerService" Version="2.22.0" /> <PackageReference Include="Microsoft.Azure.Functions.Worker.ApplicationInsights" Version="1.2.0" />`

Make note of any references to other packages in the

`Microsoft.Azure.WebJobs.*`

namespaces. You'll replace these packages in a later step.Add the following new

`ItemGroup`

:`<ItemGroup> <Using Include="System.Threading.ExecutionContext" Alias="ExecutionContext"/> </ItemGroup>`


After you make these changes, your updated project should look like the following example:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
<RootNamespace>My.Namespace</RootNamespace>
<OutputType>Exe</OutputType>
<ImplicitUsings>enable</ImplicitUsings>
<Nullable>enable</Nullable>
</PropertyGroup>
<ItemGroup>
<FrameworkReference Include="Microsoft.AspNetCore.App" />
<PackageReference Include="Microsoft.Azure.Functions.Worker" Version="1.21.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.Sdk" Version="1.17.2" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore" Version="1.2.1" />
<PackageReference Include="Microsoft.ApplicationInsights.WorkerService" Version="2.22.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.ApplicationInsights" Version="1.2.0" />
<!-- Other packages may also be in this list -->
</ItemGroup>
<ItemGroup>
<None Update="host.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
</None>
<None Update="local.settings.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
<CopyToPublishDirectory>Never</CopyToPublishDirectory>
</None>
</ItemGroup>
<ItemGroup>
<Using Include="System.Threading.ExecutionContext" Alias="ExecutionContext"/>
</ItemGroup>
</Project>
```


### Package and namespace changes

Based on the model you're migrating to, you might need to update or change the packages your application references. When you adopt the target packages, you then need to update the namespace of using statements and some types you reference. You can see the effect of these namespace changes on `using`

statements in the [HTTP trigger template examples](#http-trigger-template) later in this article.

If you haven't already, update your project to reference the latest stable versions of:

Depending on the triggers and bindings your app uses, your app might need to reference a different set of packages. The following table shows the replacements for some of the most commonly used extensions:

| Scenario | Changes to package references |
|---|---|
| Timer trigger | Add
|
| Storage bindings | Replace`Microsoft.Azure.WebJobs.Extensions.Storage` with
|
| Blob bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Storage.Blobs` with the latest version of
|
| Queue bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Storage.Queues` with the latest version of
|
| Table bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Tables` with the latest version of
|
| Cosmos DB bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.CosmosDB` and/or `Microsoft.Azure.WebJobs.Extensions.DocumentDB` with the latest version of
|
| Service Bus bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.ServiceBus` with the latest version of
|
| Event Hubs bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.EventHubs` with the latest version of
|
| Event Grid bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.EventGrid` with the latest version of
|
| SignalR Service bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.SignalRService` with the latest version of
|
| Durable Functions | Replace references to`Microsoft.Azure.WebJobs.Extensions.DurableTask` with the latest version of
|
| Durable Functions (SQL storage provider) |
Replace references to`Microsoft.DurableTask.SqlServer.AzureFunctions` with the latest version of
|
| Durable Functions (Netherite storage provider) |
Replace references to`Microsoft.Azure.DurableTask.Netherite.AzureFunctions` with the latest version of
|
| SendGrid bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.SendGrid` with the latest version of
|
| Kafka bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Kafka` with the latest version of
|
| RabbitMQ bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.RabbitMQ` with the latest version of
|
| Dependency injection and startup config |
Remove references to`Microsoft.Azure.Functions.Extensions` (The isolated worker model provides this functionality by default.) |

See [Supported bindings](functions-triggers-bindings#supported-bindings) for a complete list of extensions to consider, and consult each extension's documentation for full installation instructions for the isolated process model. Be sure to install the latest stable version of any packages you are targeting.

Tip

Any changes to extension versions during this process might require you to update your `host.json`

file as well. Be sure to read the documentation of each extension that you use.
For example, the Service Bus extension has breaking changes in the structure between versions 4.x and 5.x. For more information, see [Azure Service Bus bindings for Azure Functions](/en-us/azure/azure-functions/functions-bindings-service-bus?tabs=isolated-process%2Cextensionv5%2Cextensionv3&pivots=programming-language-csharp#hostjson-settings).

**Your isolated worker model application should not reference any packages in the Microsoft.Azure.WebJobs.* namespaces or Microsoft.Azure.Functions.Extensions.** If you have any remaining references to these, they should be removed.


Tip

Your app might also depend on Azure SDK types, either as part of your triggers and bindings or as a standalone dependency. You should take this opportunity to update these as well. The latest versions of the Functions extensions work with the latest versions of the [Azure SDK for .NET](/en-us/dotnet/azure/sdk/azure-sdk-for-dotnet), almost all of the packages for which are the form `Azure.*`

.

### Program.cs file

When migrating to run in an isolated worker process, you must add the following program.cs file to your project:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
var host = new HostBuilder()
.ConfigureFunctionsWebApplication()
.ConfigureServices(services => {
services.AddApplicationInsightsTelemetryWorkerService();
services.ConfigureFunctionsApplicationInsights();
})
.Build();
host.Run();
```


This example includes [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) to improve performance and provide a familiar programming model when your app uses HTTP triggers. If you don't intend to use HTTP triggers, you can replace the call to `ConfigureFunctionsWebApplication`

with a call to `ConfigureFunctionsWorkerDefaults`

. If you do so, you can remove the reference to `Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore`

from your project file. However, for the best performance, even for functions with other trigger types, you should keep the `FrameworkReference`

to ASP.NET Core.

The *Program.cs* file replaces any file that has the `FunctionsStartup`

attribute, which is typically a *Startup.cs* file. In places where your `FunctionsStartup`

code would reference `IFunctionsHostBuilder.Services`

, you can instead add statements within the `.ConfigureServices()`

method of the `HostBuilder`

in your *Program.cs*. To learn more about working with *Program.cs*, see [Start-up and configuration](dotnet-isolated-process-guide#start-up-and-configuration) in the isolated worker model guide.

The default *Program.cs* examples previously described include setup of [Application Insights](dotnet-isolated-process-guide#application-insights). In your *Program.cs*, you must also configure any log filtering that should apply to logs coming from code in your project. In the isolated worker model, the *host.json* file only controls events emitted by the Functions host runtime. If you don't configure filtering rules in *Program.cs*, you might see differences in the log levels present for various categories in your telemetry.

Although you can register custom configuration sources as part of the `HostBuilder`

, these similarly apply only to code in your project. The platform also needs trigger and binding configuration, and this should be provided through the [application settings](../app-service/configure-common#configure-app-settings), [Key Vault references](../app-service/app-service-key-vault-references?toc=/azure/azure-functions/toc.json), or [App Configuration references](../app-service/app-service-configuration-references?toc=/azure/azure-functions/toc.json) features.

After you move everything from any existing `FunctionsStartup`

to the *Program.cs* file, you can delete the `FunctionsStartup`

attribute and the class it was applied to.

### local.settings.json file

The local.settings.json file is only used when running locally. For information, see [Local settings file](functions-develop-local#local-settings-file).

When you migrate to version 4.x, make sure that your local.settings.json file has at least the following elements:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "AzureWebJobsStorageConnectionStringValue",
"FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated"
}
}
```


Note

When migrating from running in-process to running in an isolated worker process, you need to change the `FUNCTIONS_WORKER_RUNTIME`

value to "dotnet-isolated".

### host.json file

No changes are required to your `host.json`

file. However, if your Application Insights configuration in this file from your in-process model project, you might want to make other changes in your `Program.cs`

file. The `host.json`

file only controls logging from the Functions host runtime, and in the isolated worker model, some of these logs come from your application directly, giving you more control. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### Class name changes

Some key classes changed names between versions. These changes are a result either of changes in .NET APIs or in differences between in-process and isolated worker process. The following table indicates key .NET classes used by Functions that could change when migrating:

| .NET Core 3.1 | .NET 5 | .NET 8 |
|---|---|---|
`FunctionName` (attribute) |
`Function` (attribute) |
`Function` (attribute) |
`ILogger` |
`ILogger` |
`ILogger` , `ILogger<T>` |
`HttpRequest` |
`HttpRequestData` |
`HttpRequestData` , `HttpRequest` (using
|
`IActionResult` |
`HttpResponseData` |
`HttpResponseData` , `IActionResult` (using
|
`FunctionsStartup` (attribute) |
Uses
`Program.cs` |

[instead](#programcs-file)`Program.cs`

There might also be class name differences in bindings. For more information, see the reference articles for the specific bindings.

### Other code changes

This section highlights other code changes to consider as you work through the migration. These changes aren't needed by all applications, but you should evaluate if any are relevant to your scenarios. Make sure to check [Breaking changes between 3.x and 4.x](#breaking-changes-between-3x-and-4x) for other changes you might need to make to your project.

#### JSON serialization

By default, the isolated worker model uses *System.Text.Json* for JSON serialization. To customize serializer options or switch to JSON.NET (*Newtonsoft.Json*), see [Customizing JSON serialization](dotnet-isolated-process-guide#customizing-json-serialization).

#### Application Insights log levels and filtering

Logs can be sent to Application Insights from both the Functions host runtime and code in your project. The *host.json* allows you to configure rules for host logging, but to control logs coming from your code, you need to configure filtering rules as part of your *Program.cs*. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### HTTP trigger template

The differences between in-process and isolated worker process can be seen in HTTP triggered functions. The HTTP trigger template for version 3.x (in-process) looks like the following example:

```
using System;
using System.IO;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace Company.Function
{
public static class HttpTriggerCSharp
{
[FunctionName("HttpTriggerCSharp")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.AuthLevelValue, "get", "post", Route = null)] HttpRequest req,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string name = req.Query["name"];
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic data = JsonConvert.DeserializeObject(requestBody);
name = name ?? data?.name;
string responseMessage = string.IsNullOrEmpty(name)
? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
: $"Hello, {name}. This HTTP triggered function executed successfully.";
return new OkObjectResult(responseMessage);
}
}
}
```


The HTTP trigger template for the migrated version looks like the following example:

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace Company.Function
{
public class HttpTriggerCSharp
{
private readonly ILogger<HttpTriggerCSharp> _logger;
public HttpTriggerCSharp(ILogger<HttpTriggerCSharp> logger)
{
_logger = logger;
}
[Function("HttpTriggerCSharp")]
public IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get")] HttpRequest req)
{
_logger.LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult($"Welcome to Azure Functions, {req.Query["name"]}!");
}
}
}
```


To update your project to Azure Functions 4.x:

Update your local installation of

[Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools)to version 4.x.Update your app's

[Azure Functions extensions bundle](extension-bundles)to 2.x or above. For more information, see[breaking changes](#breaking-changes-between-3x-and-4x).

If needed, move to one of the

[Java versions supported on version 4.x](functions-reference-java#supported-versions).Update the app's

`POM.xml`

file to modify the`FUNCTIONS_EXTENSION_VERSION`

setting to`~4`

, as in the following example:`<configuration> <resourceGroup>${functionResourceGroup}</resourceGroup> <appName>${functionAppName}</appName> <region>${functionAppRegion}</region> <appSettings> <property> <name>WEBSITE_RUN_FROM_PACKAGE</name> <value>1</value> </property> <property> <name>FUNCTIONS_EXTENSION_VERSION</name> <value>~4</value> </property> </appSettings> </configuration>`


- If needed, move to one of the
[Node.js versions supported on version 4.x](functions-reference-node#node-version).

- Take this opportunity to upgrade to PowerShell 7.2, which is recommended. For more information, see
[PowerShell versions](functions-reference-powershell#powershell-versions).

- If you're using Python 3.6, move to one of the
[supported versions](functions-reference-python#supported-python-versions).

### Run the pre-upgrade validator

Azure Functions provides a pre-upgrade validator to help you identify potential issues when migrating your function app to 4.x. To run the pre-upgrade validator:

In the

[Azure portal](https://portal.azure.com), navigate to your function app.Open the

**Diagnose and solve problems**page.In

**Function App Diagnostics**, start typing`Functions 4.x Pre-Upgrade Validator`

and then choose it from the list.After validation completes, review the recommendations and address any issues in your app. If you need to make changes to your app, make sure to validate the changes against version 4.x of the Functions runtime, either

[locally using Azure Functions Core Tools v4](#migrate-your-local-project)or by[using a staging slot](#update-using-slots).

## Update your function app in Azure

You need to update the runtime of the function app host in Azure to version 4.x before you publish your migrated project. The runtime version used by the Functions host is controlled by the `FUNCTIONS_EXTENSION_VERSION`

application setting, but in some cases other settings must also be updated. Both code changes and changes to application settings require your function app to restart.

The easiest way is to [update without slots](#update-without-slots) and then republish your app project. You can also minimize the downtime in your app and simplify rollback by [updating using slots](#update-using-slots).

### Update without slots

The simplest way to update to v4.x is to set the `FUNCTIONS_EXTENSION_VERSION`

application setting to `~4`

on your function app in Azure. You must follow a [different procedure](#update-using-slots) on a site with slots.

```
az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~4 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>
```


You must also set another setting, which differs between Windows and Linux.

When running on Windows, you also need to enable .NET 8.0, which is required by version 4.x of the runtime.

```
az functionapp config set --net-framework-version v8.0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>
```


.NET 6 is required for function apps in any language running on Windows.

In this example, replace `<APP_NAME>`

with the name of your function app and `<RESOURCE_GROUP_NAME>`

with the name of the resource group.

You can now republish your app project that has been migrated to run on version 4.x.

### Update using slots

Using [deployment slots](functions-deployment-slots) is a good way to update your function app to the v4.x runtime from a previous version. By using a staging slot, you can run your app on the new runtime version in the staging slot and switch to production after verification. Slots also provide a way to minimize downtime during the update. If you need to minimize downtime, follow the steps in [Minimum downtime update](#minimum-downtime-update).

After you've verified your app in the updated slot, you can swap the app and new version settings into production. This swap requires setting [ WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0](functions-app-settings#website_override_sticky_extension_versions) in the production slot. How you add this setting affects the amount of downtime required for the update.

#### Standard update

If your slot-enabled function app can handle the downtime of a full restart, you can update the `WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS`

setting directly in the production slot. Because changing this setting directly in the production slot causes a restart that impacts availability, consider doing this change at a time of reduced traffic. You can then swap in the updated version from the staging slot.

The [ Update-AzFunctionAppSetting](/en-us/powershell/module/az.functions/update-azfunctionappsetting) PowerShell cmdlet doesn't currently support slots. You must use Azure CLI or the Azure portal.

Use the following command to set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

in the production slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>`

In this example, replace

`<APP_NAME>`

with the name of your function app and`<RESOURCE_GROUP_NAME>`

with the name of the resource group. This command causes the app running in the production slot to restart.Use the following command to also set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS`

in the staging slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Use the following command to change

`FUNCTIONS_EXTENSION_VERSION`

and update the staging slot to the new runtime version:`az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~4 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Version 4.x of the Functions runtime requires .NET 6 in Windows. On Linux, .NET apps must also update to .NET 6. Use the following command so that the runtime can run on .NET 6:

When running on Windows, you also need to enable .NET 8.0, which is required by version 4.x of the runtime.

`az functionapp config set --net-framework-version v8.0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>`

.NET 6 is required for function apps in any language running on Windows.

In this example, replace

`<APP_NAME>`

with the name of your function app and`<RESOURCE_GROUP_NAME>`

with the name of the resource group.If your code project required any updates to run on version 4.x, deploy those updates to the staging slot now.

Confirm that your function app runs correctly in the updated staging environment before swapping.

Use the following command to swap the updated staging slot to production:

`az functionapp deployment slot swap -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME> --target-slot production`


#### Minimum downtime update

To minimize the downtime in your production app, you can swap the `WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS`

setting from the staging slot into production. After that, you can swap in the updated version from a prewarmed staging slot.

Use the following command to set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

in the staging slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Use the following commands to swap the slot with the new setting into production, and at the same time restore the version setting in the staging slot.

`az functionapp deployment slot swap -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME> --target-slot production az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~3 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

You may see errors from the staging slot during the time between the swap and the runtime version being restored on staging. This error can happen because having

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

only in staging during a swap removes the`FUNCTIONS_EXTENSION_VERSION`

setting in staging. Without the version setting, your slot is in a bad state. Updating the version in the staging slot right after the swap should put the slot back into a good state, and you call roll back your changes if needed. However, any rollback of the swap also requires you to directly remove`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

from production before the swap back to prevent the same errors in production seen in staging. This change in the production setting would then cause a restart.Use the following command to again set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

in the staging slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

At this point, both slots have

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

set.Use the following command to change

`FUNCTIONS_EXTENSION_VERSION`

and update the staging slot to the new runtime version:`az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~4 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Version 4.x of the Functions runtime requires .NET 6 in Windows. On Linux, .NET apps must also update to .NET 6. Use the following command so that the runtime can run on .NET 6:

When running on Windows, you also need to enable .NET 8.0, which is required by version 4.x of the runtime.

`az functionapp config set --net-framework-version v8.0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>`

.NET 6 is required for function apps in any language running on Windows.

In this example, replace

`<APP_NAME>`

with the name of your function app and`<RESOURCE_GROUP_NAME>`

with the name of the resource group.If your code project required any updates to run on version 4.x, deploy those updates to the staging slot now.

Confirm that your function app runs correctly in the updated staging environment before swapping.

Use the following command to swap the updated and prewarmed staging slot to production:

`az functionapp deployment slot swap -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME> --target-slot production`


## Breaking changes between 3.x and 4.x

The following are key breaking changes to be aware of before upgrading a 3.x app to 4.x, including language-specific breaking changes. For a full list, see Azure Functions GitHub issues labeled [ Breaking Change: Approved](https://github.com/Azure/azure-functions/issues?q=is%3Aissue+label%3A%22Breaking+Change%3A+Approved%22+is%3A%22closed+OR+open%22).

If you don't see your programming language, go select it from the [top of the page](#top).

### Runtime

Azure Functions Proxies was a feature in versions 1.x through 3.x of the Azure Functions runtime. This feature isn't supported in version 4.x. For more information, see

[Serverless REST APIs using Azure Functions](functions-proxies).Logging to Azure Storage using

*AzureWebJobsDashboard*is no longer supported in 4.x. You should instead use[Application Insights](functions-monitoring). ([#1923](https://github.com/Azure/Azure-Functions/issues/1923))Azure Functions 4.x now enforces

[minimum version requirements for extensions](functions-versions#minimum-extension-versions). Update to the latest version of affected extensions. For non-.NET languages,[update](extension-bundles)to extension bundle version 2.x or later. ([#1987](https://github.com/Azure/Azure-Functions/issues/1987))Default and maximum timeouts are now enforced in 4.x for function apps running on Linux in a Consumption plan. (

[#1915](https://github.com/Azure/Azure-Functions/issues/1915))Azure Functions 4.x uses

`Azure.Identity`

and`Azure.Security.KeyVault.Secrets`

for the Key Vault provider and has deprecated the use of Microsoft.Azure.KeyVault. For more information about how to configure function app settings, see the Key Vault option in[Manage key storage](function-keys-how-to#manage-key-storage). ([#2048](https://github.com/Azure/Azure-Functions/issues/2048))Function apps that share storage accounts now fail to start when their host IDs are the same. For more information, see

[Host ID considerations](storage-considerations#host-id-considerations). ([#2049](https://github.com/Azure/Azure-Functions/issues/2049))

Azure Functions 4.x supports newer versions of .NET. See

[Supported languages in Azure Functions](supported-languages)for a full list of versions.`InvalidHostServicesException`

is now a fatal error. ([#2045](https://github.com/Azure/Azure-Functions/issues/2045))`EnableEnhancedScopes`

is enabled by default. ([#1954](https://github.com/Azure/Azure-Functions/issues/1954))Remove

`HttpClient`

as a registered service. ([#1911](https://github.com/Azure/Azure-Functions/issues/1911))

- Default thread count has been updated. Functions that aren't thread-safe or have high memory usage could be impacted. (
[#1962](https://github.com/Azure/Azure-Functions/issues/1962))

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-data-explorer -->

# Azure Data Explorer bindings for Azure Functions overview (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure Data Explorer](/en-us/azure/data-explorer/index) bindings in Azure Functions. Azure Functions supports input bindings and output bindings for Azure Data Explorer clusters.

| Action | Type |
|---|---|
| Read data from a database |
|

[Output binding](functions-bindings-azure-data-explorer-output)## Install the extension

The extension NuGet package you install depends on the C# mode you're using in your function app.

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kusto/).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Kusto --prerelease
```


## Install the bundle

Azure Data Explorer bindings extension is part of a preview [extension bundle](extension-bundles), which is specified in your *host.json* project file.

You can add the preview extension bundle by adding or replacing the following code in your *host.json* file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
}
```


## Functions runtime

Note

Python language support for the Azure Data Explorer bindings extension is available starting with v4.6.0 or later of the [Functions runtime](set-runtime-version#manual-version-updates-on-linux). You might need to update your installation of Azure Functions [Core Tools](functions-run-local) for local development.

## Install the bundle

The Azure Data Explorer bindings extension is part of a preview [extension bundle](extension-bundles), which is specified in your *host.json* project file.

You can add the preview extension bundle by adding or replacing the following code in your *host.json* file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
}
```


## Install the bundle

Azure Data Explorer bindings extension is part of a preview [extension bundle](extension-bundles), which is specified in your *host.json* project file.

You can add the preview extension bundle by adding or replacing the following code in your *host.json* file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
}
```


## Update packages

Add the Java library for Azure Data Explorer bindings to your Functions project with an update to the `pom.xml`

file in your Python Azure Functions project, as follows:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-kusto</artifactId>
<version>1.0.4-Preview</version>
</dependency>
```


## Kusto connection string

Azure Data Explorer bindings for Azure Functions have a required property for the connection string on all bindings. The connection string is documented at [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto).

## Considerations

- Azure Data Explorer binding supports version 4.x and later of the Functions runtime.
- Source code for the Azure Data Explorer bindings is in
[this GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto). - For enhanced security, your function app should use managed identities when connecting to Azure Data Explorer instead of using connection strings that contain keys. For more information, see
[Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For managed identity-based connections, you must set the`managedServiceIdentity`

property in the binding definition. - This binding requires connectivity to Azure Data Explorer. For input bindings, users require
**Viewer**permissions. For output bindings, users require**Ingestor**permissions. For more information about permissions, see[Role-based access control](/en-us/azure/data-explorer/kusto/management/access-control/role-based-access-control).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/streaming-logs -->

# Enable streaming execution logs in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

While developing an application, you often want to see what's being written to the logs in near real time when running in Azure.

There are two ways to view the stream of log files that your function executions generate.

When your function app is [connected to Application Insights](configure-monitoring#enable-application-insights-integration), you can use [Live Metrics Stream](/en-us/azure/azure-monitor/app/live-stream) to view log data and other metrics in near real-time in the Azure portal. Live Metrics stream is *the recommended way to view streaming logs* it supports all plan types and is the method to use when monitoring functions running on multiple-instances. It also uses [sampled data](configure-monitoring#configure-sampling), so it can protect you from producing too much data during times of peak loads.

Important

By default, the Live Metrics stream includes logs from all apps connected to a given Application Insights instance. When you have more than one app sending log data, you should [filter your log stream data](/en-us/azure/azure-monitor/app/live-stream#filter-by-server-instance).

Log streams can be viewed both in the portal and in most local development environments. The way that you enable and view streaming logs depends on your log streaming method, either Live Metrics or built-in.

To view the Live Metrics Stream for your app, select the

**Overview**tab of your function app.When you have Application Insights enabled, you see an

**Application Insights**link under**Configured features**. This link takes you to the Application Insights page for your app.In Application Insights, select

**Live Metrics Stream**.[Sampled log entries](configure-monitoring#configure-sampling)are displayed under**Sample Telemetry**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-idempotent -->

# Designing Azure Functions for identical input

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The reality of event-driven and message-based architecture dictates the need to accept identical requests while preserving data integrity and system stability.

To illustrate, consider an elevator call button. As you press the button, it lights up and an elevator is sent to your floor. A few moments later, someone else joins you in the lobby. This person smiles at you and presses the illuminated button a second time. You smile back and chuckle to yourself as you're reminded that the command to call an elevator is idempotent.

Pressing an elevator call button a second, third, or fourth time has no bearing on the final result. When you press the button, regardless of the number of times, the elevator is sent to your floor. Idempotent systems, like the elevator, result in the same outcome no matter how many times identical commands are issued.

When it comes to building applications, consider the following scenarios:

- What happens if your inventory control application tries to delete the same product more than once?
- How does your human resource application behave if there is more than one request to create an employee record for the same person?
- Where does the money go if your banking app gets 100 requests to make the same withdrawal?

There are many contexts where requests to a function may receive identical commands. Some situations include:

- Retry policies sending the same request many times.
- Cached commands replayed to the application.
- Application errors sending multiple identical requests.

To protect data integrity and system health, an idempotent application contains logic that may contain the following behaviors:

- Verifying of the existence of data before trying to execute a delete.
- Checking to see if data already exists before trying to execute a create action.
- Reconciling logic that creates eventual consistency in data.
- Concurrency controls.
- Duplication detection.
- Data freshness validation.
- Guard logic to verify input data.

Ultimately idempotency is achieved by ensuring a given action is possible and is only executed once.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/python-memory-profiler-reference -->

# Profile Python apps memory usage in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

During development or after deploying your local Python function app project to Azure, it's a good practice to analyze for potential memory bottlenecks in your functions. Such bottlenecks can decrease the performance of your functions and lead to errors. The following instructions show you how to use the [memory-profiler](https://pypi.org/project/memory-profiler) Python package, which provides line-by-line memory consumption analysis of your functions as they execute.

Note

Memory profiling is intended only for memory footprint analysis in development environments. Please do not apply the memory profiler on production function apps.

## Prerequisites

Before you start developing a Python function app, you must meet these requirements:

[Python 3.7 or above](https://www.python.org/downloads). To check the full list of supported Python versions in Azure Functions, see the[Python developer guide](functions-reference-python#supported-python-versions).The

[Azure Functions Core Tools](functions-run-local#v2), version 4.x or greater. Check your version with`func --version`

. To learn about updating, see[Azure Functions Core Tools on GitHub](https://github.com/Azure/azure-functions-core-tools).[Visual Studio Code](https://code.visualstudio.com/)installed on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).An active Azure subscription.


If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Memory profiling process

In your requirements.txt, add

`memory-profiler`

to ensure the package is bundled with your deployment. If you're developing on your local machine, you may want to[activate a Python virtual environment](how-to-create-function-azure-cli?pivots=programming-language-python#create-venv)and do a package resolution by`pip install -r requirements.txt`

.In your function script (for example,

*__init__.py*for the Python v1 programming model and*function_app.py*for the v2 model), add the following lines above the`main()`

function. These lines ensure the root logger reports the child logger names, so that the memory profiling logs are distinguishable by the prefix`memory_profiler_logs`

.`import logging import memory_profiler root_logger = logging.getLogger() root_logger.handlers[0].setFormatter(logging.Formatter("%(name)s: %(message)s")) profiler_logstream = memory_profiler.LogFile('memory_profiler_logs', True)`

Apply the following decorator above any functions that need memory profiling. The decorator doesn't work directly on the trigger entrypoint

`main()`

method. You need to create subfunctions and decorate them. Also, due to a memory-profiler known issue, when applying to an async coroutine, the coroutine return value is always`None`

.`@memory_profiler.profile(stream=profiler_logstream)`

Test the memory profiler on your local machine by using Azure Functions Core Tools command

`func host start`

. When you invoke the functions, they should generate a memory usage report. The report contains file name, line of code, memory usage, memory increment, and the line content in it.To check the memory profiling logs on an existing function app instance in Azure, you can query the memory profiling logs for recent invocations with

[Kusto](/en-us/azure/azure-monitor/logs/log-query-overview)queries in Application Insights, Logs.`traces | where timestamp > ago(1d) | where message startswith_cs "memory_profiler_logs:" | parse message with "memory_profiler_logs: " LineNumber " " TotalMem_MiB " " IncreMem_MiB " " Occurrences " " Contents | union ( traces | where timestamp > ago(1d) | where message startswith_cs "memory_profiler_logs: Filename: " | parse message with "memory_profiler_logs: Filename: " FileName | project timestamp, FileName, itemId ) | project timestamp, LineNumber=iff(FileName != "", FileName, LineNumber), TotalMem_MiB, IncreMem_MiB, Occurrences, Contents, RequestId=itemId | order by timestamp asc`


## Example

Here's an example of performing memory profiling on an asynchronous and a synchronous HTTP trigger, named "HttpTriggerAsync" and "HttpTriggerSync" respectively. We'll build a Python function app that simply sends out GET requests to the Microsoft's home page.

### Create a Python function app

A Python function app should follow Azure Functions specified [folder structure](functions-reference-python#folder-structure). To scaffold the project, we recommend using the Azure Functions Core Tools by running the following commands:

```
func init PythonMemoryProfilingDemo --python
cd PythonMemoryProfilingDemo
func new -l python -t HttpTrigger -n HttpTriggerAsync -a anonymous
func new -l python -t HttpTrigger -n HttpTriggerSync -a anonymous
```


### Update file contents

The *requirements.txt* defines the packages that are used in our project. Besides the Azure Functions SDK and memory-profiler, we introduce `aiohttp`

for asynchronous HTTP requests and `requests`

for synchronous HTTP calls.

```
# requirements.txt
azure-functions
memory-profiler
aiohttp
requests
```


Create the asynchronous HTTP trigger.

Replace the code in the asynchronous HTTP trigger *HttpTriggerAsync/__init__.py* with the following code, which configures the memory profiler, root logger format, and logger streaming binding.

```
# HttpTriggerAsync/__init__.py
import azure.functions as func
import aiohttp
import logging
import memory_profiler
# Update root logger's format to include the logger name. Ensure logs generated
# from memory profiler can be filtered by "memory_profiler_logs" prefix.
root_logger = logging.getLogger()
root_logger.handlers[0].setFormatter(logging.Formatter("%(name)s: %(message)s"))
profiler_logstream = memory_profiler.LogFile('memory_profiler_logs', True)
async def main(req: func.HttpRequest) -> func.HttpResponse:
await get_microsoft_page_async('https://microsoft.com')
return func.HttpResponse(
f"Microsoft page loaded.",
status_code=200
)
@memory_profiler.profile(stream=profiler_logstream)
async def get_microsoft_page_async(url: str):
async with aiohttp.ClientSession() as client:
async with client.get(url) as response:
await response.text()
# @memory_profiler.profile does not support return for coroutines.
# All returns become None in the parent functions.
# GitHub Issue: https://github.com/pythonprofilers/memory_profiler/issues/289
```


Create the synchronous HTTP trigger.

Replace the code in the asynchronous HTTP trigger *HttpTriggerSync/__init__.py* with the following code.

```
# HttpTriggerSync/__init__.py
import azure.functions as func
import requests
import logging
import memory_profiler
# Update root logger's format to include the logger name. Ensure logs generated
# from memory profiler can be filtered by "memory_profiler_logs" prefix.
root_logger = logging.getLogger()
root_logger.handlers[0].setFormatter(logging.Formatter("%(name)s: %(message)s"))
profiler_logstream = memory_profiler.LogFile('memory_profiler_logs', True)
def main(req: func.HttpRequest) -> func.HttpResponse:
content = profile_get_request('https://microsoft.com')
return func.HttpResponse(
f"Microsoft page response size: {len(content)}",
status_code=200
)
@memory_profiler.profile(stream=profiler_logstream)
def profile_get_request(url: str):
response = requests.get(url)
return response.content
```


### Profile Python function app in local development environment

After you make the above changes, there are a few more steps to initialize a Python virtual environment for Azure Functions runtime.

Open a Windows PowerShell or any Linux shell as you prefer.

Create a Python virtual environment by

`py -m venv .venv`

in Windows, or`python3 -m venv .venv`

in Linux.Activate the Python virtual environment with

`.venv\Scripts\Activate.ps1`

in Windows PowerShell or`source .venv/bin/activate`

in Linux shell.Restore the Python dependencies with

`pip install -r requirements.txt`

Start the Azure Functions runtime locally with Azure Functions Core Tools

`func host start`

Send a GET request to

`https://localhost:7071/api/HttpTriggerAsync`

or`https://localhost:7071/api/HttpTriggerSync`

.It should show a memory profiling report similar to the following section in Azure Functions Core Tools.

`Filename: <ProjectRoot>\HttpTriggerAsync\__init__.py Line # Mem usage Increment Occurrences Line Contents ============================================================ 19 45.1 MiB 45.1 MiB 1 @memory_profiler.profile 20 async def get_microsoft_page_async(url: str): 21 45.1 MiB 0.0 MiB 1 async with aiohttp.ClientSession() as client: 22 46.6 MiB 1.5 MiB 10 async with client.get(url) as response: 23 47.6 MiB 1.0 MiB 4 await response.text()`


## Next steps

For more information about Azure Functions Python development, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistantpost-input -->

# Azure OpenAI assistant post input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant post input binding lets you send prompts to assistant chat bots.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
/// <summary>
/// HTTP POST function that sends user prompts to the assistant chat bot.
/// </summary>
[Function(nameof(PostUserQuery))]
public static IActionResult PostUserQuery(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "assistants/{assistantId}")] HttpRequestData req,
string assistantId,
[AssistantPostInput("{assistantId}", "{Query.message}", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", ChatStorageConnectionSetting = DefaultChatStorageConnectionSetting, CollectionName = DefaultCollectionName)] AssistantState state)
{
return new OkObjectResult(state.RecentMessages.Any() ? state.RecentMessages[state.RecentMessages.Count - 1].Content : "No response returned.");
}
```


This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
/*
* HTTP POST function that sends user prompts to the assistant chat bot.
*/
@FunctionName("PostUserResponse")
public HttpResponseMessage postUserResponse(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "assistants/{assistantId}")
HttpRequestMessage<Optional<String>> request,
@BindingName("assistantId") String assistantId,
@AssistantPost(name="newMessages", id = "{assistantId}", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", userMessage = "{Query.message}", chatStorageConnectionSetting = DEFAULT_CHATSTORAGE, collectionName = DEFAULT_COLLECTION) AssistantState state,
final ExecutionContext context) {
List<AssistantMessage> recentMessages = state.getRecentMessages();
String response = recentMessages.isEmpty() ? "No response returned." : recentMessages.get(recentMessages.size() - 1).getContent();
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(response)
.build();
}
```


This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
const { app, input, output } = require("@azure/functions");
const assistantPostInput = input.generic({
type: 'assistantPost',
id: '{assistantId}',
chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%',
userMessage: '{Query.message}',
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
})
app.http('PostUserResponse', {
methods: ['POST'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraInputs: [assistantPostInput],
handler: async (_, context) => {
const chatState = context.extraInputs.get(assistantPostInput)
const content = chatState.recentMessages[0].content
return {
status: 200,
body: content,
headers: {
'Content-Type': 'text/plain'
}
};
}
})
```


```
import { HttpRequest, InvocationContext, app, input, output } from "@azure/functions"
const assistantPostInput = input.generic({
type: 'assistantPost',
id: '{assistantId}',
chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%',
userMessage: '{Query.message}',
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
})
app.http('PostUserResponse', {
methods: ['POST'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraInputs: [assistantPostInput],
handler: async (_, context) => {
const chatState: any = context.extraInputs.get(assistantPostInput)
const content = chatState.recentMessages[0].content
return {
status: 200,
body: content,
headers: {
'Content-Type': 'text/plain'
}
};
}
})
```


This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

Here's the *function.json* file for post user query:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"route": "assistants/{assistantId}",
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
"name": "State",
"type": "assistantPost",
"direction": "in",
"dataType": "string",
"id": "{assistantId}",
"userMessage": "{Query.message}",
"chatModel": "%CHAT_MODEL_DEPLOYMENT_NAME%",
"chatStorageConnectionSetting": "AzureWebJobsStorage",
"collectionName": "ChatState"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata, $State)
$recent_message_content = "No recent messages!"
if ($State.recentMessages.Count -gt 0) {
$recent_message_content = $State.recentMessages[0].content
}
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $recent_message_content
Headers = @{
"Content-Type" = "text/plain"
}
})
```


This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
@apis.function_name("PostUserQuery")
@apis.route(route="assistants/{assistantId}", methods=["POST"])
@apis.assistant_post_input(
arg_name="state",
id="{assistantId}",
user_message="{Query.message}",
chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%",
chat_storage_connection_setting=DEFAULT_CHAT_STORAGE_SETTING,
collection_name=DEFAULT_CHAT_COLLECTION_NAME,
)
def post_user_response(req: func.HttpRequest, state: str) -> func.HttpResponse:
# Parse the JSON string into a dictionary
data = json.loads(state)
# Extract the content of the recentMessage
recent_message_content = data["recentMessages"][0]["content"]
return func.HttpResponse(
recent_message_content, status_code=200, mimetype="text/plain"
)
```


## Attributes

Apply the `PostUserQuery`

attribute to define an assistant post input binding, which supports these parameters:

| Parameter | Description |
|---|---|
Id |
The ID of the assistant to update. |
UserMessage |
Gets or sets the user message for the chat completion model, encoded as a string. |
AIConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
ChatModel |
Optional. Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
Temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
TopP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
MaxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
IsReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Annotations

The `PostUserQuery`

annotation enables you to define an assistant post input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
The name of the output binding. |
id |
The ID of the assistant to update. |
userMessage |
Gets or sets the user message for the chat completion model, encoded as a string. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chatModel |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
topP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
maxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Decorators

During the preview, define the output binding as a `generic_output_binding`

binding of type `postUserQuery`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
id |
The ID of the assistant to update. |
user_message |
Gets or sets the user message for the chat completion model, encoded as a string. |
ai_connection_name |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chat_model |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
top_p |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
max_tokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
is_reasoning _model |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `PostUserQuery` . |
direction |
Must be `out` . |
name |
The name of the output binding. |
id |
The ID of the assistant to update. |
userMessage |
Gets or sets the user message for the chat completion model, encoded as a string. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chatModel |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
topP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
maxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
id |
The ID of the assistant to update. |
userMessage |
Gets or sets the user message for the chat completion model, encoded as a string. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chatModel |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
topP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
maxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Usage

See the [Example section](#example) for complete examples.
