---
merged_at: 2026-02-01T08:17:25.339894
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mcp-trigger -->

# MCP tool trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the MCP tool trigger to define tool endpoints in a [Model Content Protocol (MCP)](https://github.com/modelcontextprotocol) server. Client language models and agents can use tools to perform specific tasks, such as storing or accessing code snippets.

For information on setup and configuration details, see the [overview](functions-bindings-mcp).

## Example

Note

For C#, the Azure Functions MCP extension supports only the [isolated worker model](dotnet-isolated-process-guide).

This code creates an endpoint to expose a tool named `SaveSnippet`

that tries to persist a named code snippet to blob storage.

```
private const string BlobPath = "snippets/{mcptoolargs.snippetname}.json";
[Function(nameof(SaveSnippet))]
[BlobOutput(BlobPath)]
public string SaveSnippet(
[McpToolTrigger("save_snippet", "Saves a code snippet into your snippet collection.")]
ToolInvocationContext context,
[McpToolProperty("snippetname", "The name of the snippet.", isRequired: true)]
string name,
[McpToolProperty("snippet", "The code snippet.", isRequired: true)]
string snippet
)
{
return snippet;
}
```


This code creates an endpoint to expose a tool named `GetSnippet`

that tries to retrieve a code snippet by name from blob storage.

```
private const string BlobPath = "snippets/{mcptoolargs.snippetname}.json";
[Function(nameof(GetSnippet))]
public object GetSnippet(
[McpToolTrigger("get_snippets", "Gets code snippets from your snippet collection.")]
ToolInvocationContext context,
[BlobInput(BlobPath)] string snippetContent
)
{
return snippetContent;
}
```


The tool properties for the `GetSnippet`

function are configured in `Program.cs`

:

```
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Services
.AddApplicationInsightsTelemetryWorkerService()
.ConfigureFunctionsApplicationInsights();
builder
.ConfigureMcpTool("get_snippets")
.WithProperty("snippetname", "string", "The name of the snippet.", required: true);
builder.Build().Run();
```


Tip

The example above used literal strings for things like the name of the "get_snippets" tool in both `Program.cs`

and the function. Consider instead using shared constant strings to keep things in sync across your project.

For the complete code example, see [SnippetTool.cs](https://github.com/Azure-Samples/remote-mcp-functions-dotnet/blob/main/src/SnippetsTool.cs).

This code creates an endpoint to expose a tool named `SaveSnippets`

that tries to persist a named code snippet to blob storage.

```
@FunctionName("SaveSnippets")
@StorageAccount("AzureWebJobsStorage")
public String saveSnippet(
@McpToolTrigger(
name = "saveSnippets",
description = "Saves a text snippet to your snippets collection."
)
String mcpToolInvocationContext,
@McpToolProperty(
name = "snippetName",
propertyType = "string",
description = "The name of the snippet.",
required = true
)
String snippetName,
@McpToolProperty(
name = "snippet",
propertyType = "string",
description = "The content of the snippet.",
required = true
)
String snippet,
@BlobOutput(name = "outputBlob", path = "snippets/{mcptoolargs.snippetName}.json")
OutputBinding<String> outputBlob,
final ExecutionContext context
) {
// Log the entire incoming JSON for debugging
context.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and content
context.getLogger().info("Saving snippet with name: " + snippetName);
context.getLogger().info("Snippet content:\n" + snippet);
// Write the snippet content to the output blob
outputBlob.setValue(snippet);
return "Successfully saved snippet '" + snippetName + "' with " + snippet.length() + " characters.";
}
```


This code creates an endpoint to expose a tool named `GetSnippets`

that tries to retrieve a code snippet by name from blob storage.

```
@FunctionName("GetSnippets")
@StorageAccount("AzureWebJobsStorage")
public String getSnippet(
@McpToolTrigger(
name = "getSnippets",
description = "Gets a text snippet from your snippets collection."
)
String mcpToolInvocationContext,
@McpToolProperty(
name = "snippetName",
propertyType = "string",
description = "The name of the snippet.",
required = true
)
String snippetName,
@BlobInput(name = "inputBlob", path = "snippets/{mcptoolargs.snippetName}.json")
String inputBlob,
final ExecutionContext context
) {
// Log the entire incoming JSON for debugging
context.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and the fetched snippet content from the blob
context.getLogger().info("Retrieving snippet with name: " + snippetName);
context.getLogger().info("Snippet content:");
context.getLogger().info(inputBlob);
// Return the snippet content or a not found message
if (inputBlob != null && !inputBlob.trim().isEmpty()) {
return inputBlob;
} else {
return "Snippet '" + snippetName + "' not found.";
}
}
```


For the complete code example, see [Snippets.java](https://github.com/Azure-Samples/remote-mcp-functions-java/blob/main/src/main/java/com/function/Snippets.java).

Example code for JavaScript isn't currently available. See the TypeScript examples for general guidance using Node.js.

This code creates an endpoint to expose a tool named `savesnippet`

that tries to persist a named code snippet to blob storage.

```
import { app, InvocationContext, input, output, arg } from "@azure/functions";
app.mcpTool("saveSnippet", {
toolName: SAVE_SNIPPET_TOOL_NAME,
description: SAVE_SNIPPET_TOOL_DESCRIPTION,
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION),
[SNIPPET_PROPERTY_NAME]: arg.string().describe(SNIPPET_PROPERTY_DESCRIPTION)
},
extraOutputs: [blobOutputBinding],
handler: saveSnippet,
});
```


This code handles the `savesnippet`

trigger:

```
export async function saveSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Saving snippet");
// Get snippet name and content from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
snippet?: string;
};
const snippetName = mcptoolargs?.snippetname;
const snippet = mcptoolargs?.snippet;
if (!snippetName) {
return "No snippet name provided";
}
if (!snippet) {
return "No snippet content provided";
}
// Save the snippet to blob storage using the output binding
context.extraOutputs.set(blobOutputBinding, snippet);
console.info(`Saved snippet: ${snippetName}`);
return snippet;
}
```


This code creates an endpoint to expose a tool named `getsnippet`

that tries to retrieve a code snippet by name from blob storage.

```
import { app, InvocationContext, input, output, arg } from "@azure/functions";
app.mcpTool("getSnippet", {
toolName: GET_SNIPPET_TOOL_NAME,
description: GET_SNIPPET_TOOL_DESCRIPTION,
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION)
},
extraInputs: [blobInputBinding],
handler: getSnippet,
});
```


This code handles the `getsnippet`

trigger:

```
export async function getSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Getting snippet");
// Get snippet name from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
};
const snippetName = mcptoolargs?.snippetname;
console.info(`Snippet name: ${snippetName}`);
if (!snippetName) {
return "No snippet name provided";
}
// Get the content from blob binding - properly retrieving from extraInputs
const snippetContent = context.extraInputs.get(blobInputBinding);
if (!snippetContent) {
return `Snippet '${snippetName}' not found`;
}
console.info(`Retrieved snippet: ${snippetName}`);
return snippetContent as string;
}
```


For the complete code example, see [snippetsMcpTool.ts](https://github.com/Azure-Samples/remote-mcp-functions-typescript/blob/main/src/functions/snippetsMcpTool.ts).

This code uses the `mcp_tool_trigger`

decorator to create an endpoint to expose a tool named `save_snippet`

that tries to persist a named code snippet to blob storage.

```
@app.mcp_tool_trigger(
arg_name="context",
tool_name="save_snippet",
description="Save a snippet with a name.",
tool_properties=tool_properties_save_snippets_json,
)
@app.blob_output(arg_name="file", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def save_snippet(file: func.Out[str], context) -> str:
content = json.loads(context)
snippet_name_from_args = content["arguments"][_SNIPPET_NAME_PROPERTY_NAME]
snippet_content_from_args = content["arguments"][_SNIPPET_PROPERTY_NAME]
if not snippet_name_from_args:
return "No snippet name provided"
if not snippet_content_from_args:
return "No snippet content provided"
file.set(snippet_content_from_args)
logging.info(f"Saved snippet: {snippet_content_from_args}")
return f"Snippet '{snippet_content_from_args}' saved successfully"
```


This code uses the `mcp_tool_trigger`

decorator to create an endpoint to expose a tool named `get_snippet`

that tries to retrieve a code snippet by name from blob storage.

```
@app.mcp_tool_trigger(
arg_name="context",
tool_name="get_snippet",
description="Retrieve a snippet by name.",
tool_properties=tool_properties_get_snippets_json,
)
@app.blob_input(arg_name="file", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def get_snippet(file: func.InputStream, context) -> str:
"""
Retrieves a snippet by name from Azure Blob Storage.
Args:
file (func.InputStream): The input binding to read the snippet from Azure Blob Storage.
context: The trigger context containing the input arguments.
Returns:
str: The content of the snippet or an error message.
"""
snippet_content = file.read().decode("utf-8")
logging.info(f"Retrieved snippet: {snippet_content}")
return snippet_content
```


For the complete code example, see [function_app.py](https://github.com/Azure-Samples/remote-mcp-functions-python/blob/main/src/function_app.py).

Important

The MCP extension doesn't currently support PowerShell apps.

## Attributes

C# libraries use `McpToolTriggerAttribute`

to define the function trigger.

The attribute's constructor takes the following parameters:

| Parameter | Description |
|---|---|
ToolName |
(Required) name of the tool that's being exposed by the MCP trigger endpoint. |
Description |
(Optional) friendly description of the tool endpoint for clients. |

See [Usage](#usage) to learn how to define properties of the endpoint as input parameters.

## Annotations

The `@McpToolTrigger`

annotation creates a function that exposes a tool endpoint in your remote MCP server.

The annotation supports the following configuration options:

| Parameter | Description |
|---|---|
name |
(Required) name of the tool that's being exposed by the MCP trigger endpoint. |
description |
(Optional) friendly description of the tool endpoint for clients. |

The `@McpToolProperty`

annotation defines individual properties for your tools. Each property parameter in your function should be annotated with this annotation.

The `@McpToolProperty`

annotation supports the following configuration options:

| Parameter | Description |
|---|---|
name |
(Required) name of the tool property that gets exposed to clients. |
propertyType |
(Required) type of the tool property. Valid types are: `string` , `number` , `integer` , `boolean` , `object` . |
description |
(Optional) description of what the tool property does. |
required |
(Optional) if set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |

## Decorators

*Applies only to the Python v2 programming model.*

The `mcp_tool_trigger`

decorator requires version 1.24.0 or later of the [ azure-functions package](https://pypi.org/project/azure-functions/). The following MCP trigger properties are supported on

`mcp_tool_trigger`

:| Property | Description |
|---|---|
arg_name |
The variable name (usually `context` ) used in function code to access the execution context. |
tool_name |
(Required) The name of the MCP server tool exposed by the function endpoint. |
description |
A description of the MCP server tool exposed by the function endpoint. |
tool_properties |
The JSON string representation of one or more property objects that expose properties of the tool to clients. |

## Configuration

The trigger supports these binding options, which are defined in your code:

| Options | Description |
|---|---|
type |
Must be set to `mcpToolTrigger` . Only used with generic definitions. |
toolName |
(Required) The name of the MCP server tool exposed by the function endpoint. |
description |
A description of the MCP server tool exposed by the function endpoint. |
toolProperties |
An array of `toolProperty` objects that expose properties of the tool to clients. |
extraOutputs |
When defined, sends function output to another binding. |
handler |
The method that contains the actual function code. |

See the [Example section](#example) for complete examples.

## Usage

The MCP tool trigger can bind to the following types:

| Type | Description |
|---|---|
|

[define tool properties](#tool-properties).When binding to a JSON serializable type, you can optionally also include a parameter of type

[ToolInvocationContext](https://github.com/Azure/azure-functions-mcp-extension/blob/main/src/Microsoft.Azure.Functions.Worker.Extensions.Mcp/Abstractions/ToolInvocationContext.cs)to access the tool call information.### Tool properties

MCP clients invoke tools with arguments to provide data and context for the tool's operation. The clients know how to collect and pass these arguments based on properties that the tool advertises as part of the protocol. You therefore need to define properties of the tool in your function code.

When you define a tool property, it's optional by default, and the client can omit it when invoking the tool. You need to explicitly mark properties as required if the tool can't operate without them.

Note

Earlier versions of the MCP extension preview made all tool properties required by default. This behavior changed as of version `1.0.0-preview.7`

, and now you must explicitly mark properties as required.

In C#, you can define properties for your tools in several ways. Which approach you use is a matter of code style preference. The options are:

- Your function takes input parameters using the
`McpToolProperty`

attribute. - You define a custom type with the properties, and the function binds to that type.
- You use the
`FunctionsApplicationBuilder`

to define properties in your`Program.cs`

file.

You can define one or more tool properties by applying the `McpToolProperty`

attribute to input binding-style parameters in your function.

The `McpToolPropertyAttribute`

type supports these properties:

| Property | Description |
|---|---|
PropertyName |
Name of the tool property that gets exposed to clients. |
Description |
Description of what the tool property does. |
IsRequired |
(Optional) If set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |

The property type is inferred from the type of the parameter to which you apply the attribute. For example `[McpToolProperty("snippetname", "The name of the snippet.", true)] string name`

defines a required tool property named `snippetname`

of type `string`

in MCP messages.

You can see these attributes used in the `SaveSnippet`

tool in the [Examples](#example).

In Java, you define tool properties by using the `@McpToolProperty`

annotation on individual function parameters. Each parameter that represents a tool property should be annotated with this annotation, specifying the property name, type, description, and whether it's required.

You can see these annotations used in the [Examples](#example).

You can configure tool properties in the trigger definition's `toolProperties`

field, which is a string representation of an array of `ToolProperty`

objects.

A `ToolProperty`

object has this structure:

```
{
"propertyName": "Name of the property",
"propertyType": "Type of the property",
"description": "Optional property description",
"isRequired": true|false,
"isArray": true|false
}
```


The fields of a `ToolProperty`

object are:

| Property | Description |
|---|---|
propertyName |
Name of the tool property that gets exposed to clients. |
propertyType |
Type of the tool property. Valid types are: `string` , `number` , `integer` , `boolean` , `object` . See `isArray` for array types. |
description |
Description of what the tool property does. |
isRequired |
(Optional) If set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |
isArray |
(Optional) If set to `true` , the tool property is an array of the specified property type. Defaults to `false` . |

You can provide the `toolProperties`

field as an array of `ToolProperty`

objects, or you can use the `arg`

helpers from `@azure/functions`

to define properties in a more type-safe way:

```
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION)
}
```


For more information, see [Examples](#example).

## host.json settings

The host.json file contains settings that control MCP trigger behaviors. See the [host.json settings](functions-bindings-mcp#hostjson-settings) section for details regarding available settings.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-twilio -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-rabbitmq-output -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-kafka-trigger -->

# Apache Kafka trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Apache Kafka trigger in Azure Functions to run your function code in response to messages in Kafka topics. You can also use a [Kafka output binding](functions-bindings-kafka-output) to write from your function to a topic. For information on setup and configuration details, see [Apache Kafka bindings for Azure Functions overview](functions-bindings-kafka).

Important

Kafka bindings are available for Functions on the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium Plan](functions-premium-plan), and [Dedicated (App Service) plan](dedicated-plan). They are only supported on version 4.x of the Functions runtime.

## Example

The usage of the trigger depends on the C# modality used in your function app, which can be one of the following modes:

A compiled C# function that uses an [isolated worker process class library](dotnet-isolated-process-guide) that runs in a process that's separate from the runtime.

The attributes you use depend on the specific event provider.

The following example shows a C# function that reads and logs the Kafka message as a Kafka event:

```
[Function("KafkaTrigger")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default")] string eventData, FunctionContext context)
{
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {JObject.Parse(eventData)["Value"]}");
}
```


To receive events in a batch, use a string array as input, as shown in the following example:

```
[Function("KafkaTriggerMany")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default",
IsBatched = true)] string[] events, FunctionContext context)
{
foreach (var kevent in events)
{
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {JObject.Parse(kevent)["Value"]}");
}
```


The following function logs the message and headers for the Kafka Event:

```
[Function("KafkaTriggerWithHeaders")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default")] string eventData, FunctionContext context)
{
var eventJsonObject = JObject.Parse(eventData);
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {eventJsonObject["Value"]}");
var headersJArr = eventJsonObject["Headers"] as JArray;
logger.LogInformation("Headers for this event: ");
foreach (JObject header in headersJArr)
{
logger.LogInformation($"{header["Key"]} {System.Text.Encoding.UTF8.GetString((byte[])header["Value"])}");
}
}
```


For a complete set of working .NET examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/dotnet-isolated/).

The usage of the trigger depends on your version of the Node.js programming model.

In the Node.js v4 model, you define your trigger directly in your function code. For more information, see the [Azure Functions Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4).

In these examples, the event providers are either Confluent or Azure Event Hubs. These examples show how to define a Kafka trigger for a function that reads a Kafka message.

```
const { app } = require("@azure/functions");
async function kafkaTrigger(event, context) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Key: " + event.Key);
context.log("Event Value (as string): " + event.Value);
let event_obj = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
app.generic("Kafkatrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string"
},
handler: kafkaTrigger,
});
```


To receive events in a batch, set the `cardinality`

value to `many`

, as shown in these examples:

```
const { app } = require("@azure/functions");
async function kafkaTriggerMany(events, context) {
for (const event of events) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Key: " + event.Key);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
}
app.generic("kafkaTriggerMany", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string",
cardinality: "MANY"
},
handler: kafkaTriggerMany,
});
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. This example defines the trigger for the specific provider with a generic Avro schema:

```
const { app } = require("@azure/functions");
async function kafkaAvroGenericTrigger(event, context) {
context.log("Processed kafka event: ", event);
if (context.triggerMetadata?.key !== undefined) {
context.log("message key: ", context.triggerMetadata?.key);
}
}
app.generic("kafkaAvroGenericTrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
protocol: "SASLSSL",
password: "EventHubConnectionString",
dataType: "string",
topic: "topic",
authenticationMode: "PLAIN",
avroSchema:
'{"type":"record","name":"Payment","namespace":"io.confluent.examples.clients.basicavro","fields":[{"name":"id","type":"string"},{"name":"amount","type":"double"},{"name":"type","type":"string"}]}',
consumerGroup: "$Default",
username: "$ConnectionString",
brokerList: "%BrokerList%",
},
handler: kafkaAvroGenericTrigger,
});
```


For a complete set of working JavaScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/javascript-v4/src/functions).

```
import { app, InvocationContext } from "@azure/functions";
// This is a sample interface that describes the actual data in your event.
interface EventData {
registertime: number;
userid: string;
regionid: string;
gender: string;
}
export async function kafkaTrigger(
event: any,
context: InvocationContext
): Promise<void> {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj: EventData = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
app.generic("Kafkatrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string"
},
handler: kafkaTrigger,
});
```


To receive events in a batch, set the `cardinality`

value to `many`

, as shown in these examples:

```
import { app, InvocationContext } from "@azure/functions";
// This is a sample interface that describes the actual data in your event.
interface EventData {
registertime: number;
userid: string;
regionid: string;
gender: string;
}
interface KafkaEvent {
Offset: number;
Partition: number;
Topic: string;
Timestamp: number;
Value: string;
}
export async function kafkaTriggerMany(
events: any,
context: InvocationContext
): Promise<void> {
for (const event of events) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj: EventData = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
}
app.generic("kafkaTriggerMany", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string",
cardinality: "MANY"
},
handler: kafkaTriggerMany,
});
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. This example defines the trigger for the specific provider with a generic Avro schema:

```
import { app, InvocationContext } from "@azure/functions";
export async function kafkaAvroGenericTrigger(
event: any,
context: InvocationContext
): Promise<void> {
context.log("Processed kafka event: ", event);
context.log(
`Message ID: ${event.id}, amount: ${event.amount}, type: ${event.type}`
);
if (context.triggerMetadata?.key !== undefined) {
context.log(`Message Key : ${context.triggerMetadata?.key}`);
}
}
app.generic("kafkaAvroGenericTrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
protocol: "SASLSSL",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
dataType: "string",
topic: "topic",
authenticationMode: "PLAIN",
avroSchema:
'{"type":"record","name":"Payment","namespace":"io.confluent.examples.clients.basicavro","fields":[{"name":"id","type":"string"},{"name":"amount","type":"double"},{"name":"type","type":"string"}]}',
consumerGroup: "$Default",
brokerList: "%BrokerList%",
},
handler: kafkaAvroGenericTrigger,
});
```


For a complete set of working TypeScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/typescript-v4/src/functions).

The specific properties of the `function.json`

file depend on your event provider. In these examples, the event providers are either Confluent or Azure Event Hubs. The following examples show a Kafka trigger for a function that reads and logs a Kafka message.

The following `function.json`

file defines the trigger for the specific provider:

```
{
"bindings": [
{
"type": "kafkaTrigger",
"name": "kafkaEvent",
"direction": "in",
"protocol" : "SASLSSL",
"password" : "%ConfluentCloudPassword%",
"dataType" : "string",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"consumerGroup" : "$Default",
"username" : "%ConfluentCloudUserName%",
"brokerList" : "%BrokerList%",
"sslCaLocation": "confluent_cloud_cacert.pem"
}
]
}
```


The following code runs when the function is triggered:

```
using namespace System.Net
param($kafkaEvent, $TriggerMetadata)
Write-Output "Powershell Kafka trigger function called for message $kafkaEvent.Value"
```


To receive events in a batch, set the `cardinality`

value to `many`

in the function.json file, as shown in the following examples:

```
{
"bindings": [
{
"type": "kafkaTrigger",
"name": "kafkaEvent",
"direction": "in",
"protocol" : "SASLSSL",
"password" : "%ConfluentCloudPassword%",
"dataType" : "string",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"cardinality" : "MANY",
"consumerGroup" : "$Default",
"username" : "%ConfluentCloudUserName%",
"brokerList" : "%BrokerList%",
"sslCaLocation": "confluent_cloud_cacert.pem"
}
]
}
```


The following code parses the array of events and logs the event data:

```
using namespace System.Net
param($kafkaEvents, $TriggerMetadata)
$kafkaEvents
foreach ($kafkaEvent in $kafkaEvents) {
$event = $kafkaEvent | ConvertFrom-Json -AsHashtable
Write-Output "Powershell Kafka trigger function called for message $event.Value"
}
```


The following code logs the header data:

```
using namespace System.Net
param($kafkaEvents, $TriggerMetadata)
foreach ($kafkaEvent in $kafkaEvents) {
$kevent = $kafkaEvent | ConvertFrom-Json -AsHashtable
Write-Output "Powershell Kafka trigger function called for message $kevent.Value"
Write-Output "Headers for this message:"
foreach ($header in $kevent.Headers) {
$DecodedValue = [System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($header.Value))
$Key = $header.Key
Write-Output "Key: $Key Value: $DecodedValue"
}
}
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. The following function.json defines the trigger for the specific provider with a generic Avro schema:

```
{
"bindings" : [ {
"type" : "kafkaTrigger",
"direction" : "in",
"name" : "kafkaEvent",
"protocol" : "SASLSSL",
"password" : "ConfluentCloudPassword",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"avroSchema" : "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}",
"consumerGroup" : "$Default",
"username" : "ConfluentCloudUsername",
"brokerList" : "%BrokerList%"
} ]
}
```


The following code runs when the function is triggered:

```
using namespace System.Net
param($kafkaEvent, $TriggerMetadata)
Write-Output "Powershell Kafka trigger function called for message $kafkaEvent.Value"
```


For a complete set of working PowerShell examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/powershell/).

The usage of the trigger depends on your version of the Python programming model.

In the Python v2 model, you define your trigger directly in your function code using decorators. For more information, see the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

These examples show how to define a Kafka trigger for a function that reads a Kafka message.

```
@KafkaTrigger.function_name(name="KafkaTrigger")
@KafkaTrigger.kafka_trigger(
arg_name="kevent",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
consumer_group="$Default1")
def kafka_trigger(kevent : func.KafkaEvent):
logging.info(kevent.get_body().decode('utf-8'))
logging.info(kevent.metadata)
```


This example receives events in a batch by setting the `cardinality`

value to `many`

.

```
@KafkaTrigger.function_name(name="KafkaTriggerMany")
@KafkaTrigger.kafka_trigger(
arg_name="kevents",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
cardinality="MANY",
data_type="string",
consumer_group="$Default2")
def kafka_trigger_many(kevents : typing.List[func.KafkaEvent]):
for event in kevents:
logging.info(event.get_body())
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger.

```
@KafkaTriggerAvro.function_name(name="KafkaTriggerAvroOne")
@KafkaTriggerAvro.kafka_trigger(
arg_name="kafkaTriggerAvroGeneric",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
consumer_group="$Default",
avro_schema= "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}")
def kafka_trigger_avro_one(kafkaTriggerAvroGeneric : func.KafkaEvent):
logging.info(kafkaTriggerAvroGeneric.get_body().decode('utf-8'))
logging.info(kafkaTriggerAvroGeneric.metadata)
```


For a complete set of working Python examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/python-v2/).

The annotations you use to configure your trigger depend on the specific event provider.

The following example shows a Java function that reads and logs the content of the Kafka event:

```
@FunctionName("KafkaTrigger")
public void runSingle(
@KafkaTrigger(
name = "KafkaTrigger",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
dataType = "string"
) String kafkaEventData,
final ExecutionContext context) {
context.getLogger().info(kafkaEventData);
}
```


To receive events in a batch, use an input string as an array, as shown in the following example:

```
@FunctionName("KafkaTriggerMany")
public void runMany(
@KafkaTrigger(
name = "kafkaTriggerMany",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
cardinality = Cardinality.MANY,
dataType = "string"
) String[] kafkaEvents,
final ExecutionContext context) {
for (String kevent: kafkaEvents) {
context.getLogger().info(kevent);
}
}
```


The following function logs the message and headers for the Kafka Event:

```
@FunctionName("KafkaTriggerManyWithHeaders")
public void runSingle(
@KafkaTrigger(
name = "KafkaTrigger",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
dataType = "string",
cardinality = Cardinality.MANY
) List<String> kafkaEvents,
final ExecutionContext context) {
Gson gson = new Gson();
for (String keventstr: kafkaEvents) {
KafkaEntity kevent = gson.fromJson(keventstr, KafkaEntity.class);
context.getLogger().info("Java Kafka trigger function called for message: " + kevent.Value);
context.getLogger().info("Headers for the message:");
for (KafkaHeaders header : kevent.Headers) {
String decodedValue = new String(Base64.getDecoder().decode(header.Value));
context.getLogger().info("Key:" + header.Key + " Value:" + decodedValue);
}
}
}
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. The following function defines a trigger for the specific provider with a generic Avro schema:

```
private static final String schema = "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}";
@FunctionName("KafkaAvroGenericTrigger")
public void runOne(
@KafkaTrigger(
name = "kafkaAvroGenericSingle",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "ConfluentCloudUsername",
password = "ConfluentCloudPassword",
avroSchema = schema,
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL) Payment payment,
final ExecutionContext context) {
context.getLogger().info(payment.toString());
}
```


For a complete set of working Java examples for Confluent, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/java/confluent/src/main/java/com/contoso/kafka).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `KafkaTriggerAttribute`

to define the function trigger.

The following table explains the properties you can set by using this trigger attribute:

| Parameter | Description |
|---|---|
BrokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**Topic****ConsumerGroup****AvroSchema****KeyAvroSchema****KeyDataType**`KeyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**AuthenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

, and `OAuthBearer`

.**Username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**SslCaLocation****SslCertificateLocation****SslKeyLocation****SslKeyPassword****SslCertificatePEM**[Connections](#connections)for more information.**SslKeyPEM**[Connections](#connections)for more information.**SslCaPEM**[Connections](#connections)for more information.**SslCertificateandKeyPEM**[Connections](#connections)for more information.**SchemaRegistryUrl**[Connections](#connections)for more information.**SchemaRegistryUsername**[Connections](#connections)for more information.**SchemaRegistryPassword**[Connections](#connections)for more information.**OAuthBearerMethod**`oidc`

and `default`

.**OAuthBearerClientId**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**OAuthBearerClientSecret**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**OAuthBearerScope****OAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.**OAuthBearerExtensions**`oidc`

method is used. For example: `supportFeatureX=true,organizationId=sales-emea`

.## Annotations

The `KafkaTrigger`

annotation enables you to create a function that runs when it receives a topic. Supported options include the following elements:

| Element | Description |
|---|---|
name |
(Required) The name of the variable that represents the queue or topic message in function code. |
brokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `dataType`

.**dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**consumerGroup****avroSchema****authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****lagThreshold****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

function.json property |
Description |
|---|---|
type |
(Required) Set to `kafkaTrigger` . |
direction |
(Required) Set to `in` . |
name |
(Required) The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `dataType`

.**dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual byte array parameter type.**consumerGroup****avroSchema****keyAvroSchema****keyDataType**`keyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****sslCertificatePEM**[Connections](#connections)for more information.**sslKeyPEM**[Connections](#connections)for more information.**sslCaPEM**[Connections](#connections)for more information.**sslCertificateandKeyPEM**[Connections](#connections)for more information.**lagThreshold****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.**oAuthBearerMethod**`oidc`

and `default`

.**oAuthBearerClientId**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**oAuthBearerClientSecret**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**oAuthBearerScope****oAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file. Python uses snake_case naming conventions for configuration properties.

function.json property |
Description |
|---|---|
type |
(Required) Set to `kafkaTrigger` . |
direction |
(Required) Set to `in` . |
name |
(Required) The name of the variable that represents the brokered data in function code. |
broker_list |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `data_type`

.**data_type**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**consumerGroup****avroSchema****authentication_mode**`NOTSET`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NOTSET`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****lag_threshold****schema_registry_url**[Connections](#connections)for more information.**schema_registry_username**[Connections](#connections)for more information.**schema_registry_password**[Connections](#connections)for more information.**o_auth_bearer_method**`oidc`

and `default`

.**o_auth_bearer_client_id**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**o_auth_bearer_client_secret**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**o_auth_bearer_scope****o_auth_bearer_token_endpoint_url**`oidc`

method is used. See [Connections](#connections)for more information.Note

Certificate PEM-related properties and Avro key-related properties aren't yet available in the Python library.

## Usage

The Kafka trigger currently supports Kafka events as strings and string arrays that are JSON payloads.

The Kafka trigger passes Kafka messages to the function as strings. The trigger also supports string arrays that are JSON payloads.

In a Premium plan, you must enable runtime scale monitoring for the Kafka output to scale out to multiple instances. To learn more, see [Enable runtime scaling](functions-bindings-kafka#enable-runtime-scaling).

You can't use the **Test/Run** feature of the **Code + Test** page in the Azure portal to work with Kafka triggers. You must instead send test events directly to the topic being monitored by the trigger.

For a complete set of supported host.json settings for the Kafka trigger, see [host.json settings](functions-bindings-kafka#hostjson-settings).

## Connections

Store all connection information required by your triggers and bindings in application settings, not in the binding definitions in your code. This guidance applies to credentials, which you should never store in your code.

Important

Credential settings must reference an [application setting](functions-how-to-use-azure-function-app-settings#settings). Don't hard-code credentials in your code or configuration files. When running locally, use the [local.settings.json file](functions-develop-local#local-settings-file) for your credentials, and don't publish the local.settings.json file.

When connecting to a managed Kafka cluster provided by [Confluent in Azure](https://www.confluent.io/azure/), you can use one of the following authentication methods.

Note

When using the Flex Consumption plan, file location-based certificate authentication properties (`SslCaLocation`

, `SslCertificateLocation`

, `SslKeyLocation`

) aren't supported. Instead, use the PEM-based certificate properties (`SslCaPEM`

, `SslCertificatePEM`

, `SslKeyPEM`

, `SslCertificateandKeyPEM`

) or store certificates in Azure Key Vault.

#### Schema Registry

To make use of schema registry provided by Confluent in Kafka Extension, set the following credentials:

| Setting | Recommended Value | Description |
|---|---|---|
SchemaRegistryUrl |
`SchemaRegistryUrl` |
URL of the schema registry service used for schema management. Usually of the format `https://psrc-xyz.us-east-2.aws.confluent.cloud` |
SchemaRegistryUsername |
`CONFLUENT_API_KEY` |
Username for basic auth on schema registry (if required). |
SchemaRegistryPassword |
`CONFLUENT_API_SECRET` |
Password for basic auth on schema registry (if required). |

#### Username/Password authentication

While using this form of authentication, make sure that `Protocol`

is set to either `SaslPlaintext`

or `SaslSsl`

, `AuthenticationMode`

is set to `Plain`

, `ScramSha256`

or `ScramSha512`

and, if the CA cert being used is different from the default ISRG Root X1 cert, make sure to update `SslCaLocation`

or `SslCaPEM`

.

| Setting | Recommended value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
Username |
`ConfluentCloudUsername` |
App setting named `ConfluentCloudUsername` contains the API access key from the Confluent Cloud web site. |
Password |
`ConfluentCloudPassword` |
App setting named `ConfluentCloudPassword` contains the API secret obtained from the Confluent Cloud web site. |
SslCaPEM |
`SSLCaPemCertificate` |
App setting named `SSLCaPemCertificate` that contains the CA certificate as a string in PEM format. The value should follow the standard format, for example: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----` . |

#### SSL authentication

Ensure that `Protocol`

is set to `SSL`

.

| Setting | Recommended Value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
SslCaPEM |
`SslCaCertificatePem` |
App setting named `SslCaCertificatePem` that contains PEM value of the CA certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslCertificatePEM |
`SslClientCertificatePem` |
App setting named `SslClientCertificatePem` that contains PEM value of the client certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslKeyPEM |
`SslClientKeyPem` |
App setting named `SslClientKeyPem` that contains PEM value of the client private key as a string. The value should follow the standard format: `-----BEGIN PRIVATE KEY-----\nMII...JQ==\n-----END PRIVATE KEY-----` |
SslCertificateandKeyPEM |
`SslClientCertificateAndKeyPem` |
App setting named `SslClientCertificateAndKeyPem` that contains PEM value of the client certificate and client private key concatenated as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----\n-----BEGIN PRIVATE KEY-----\nMIIE....BM=\n-----END PRIVATE KEY-----` |
SslKeyPassword |
`SslClientKeyPassword` |
App setting named `SslClientKeyPassword` that contains the password for the private key (if any). |

#### OAuth authentication

When using OAuth authentication, configure the OAuth-related properties in your binding definitions.

The string values you use for these settings must be present as [application settings in Azure](functions-how-to-use-azure-function-app-settings#settings) or in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file) during local development.

You should also set the `Protocol`

and `AuthenticationMode`

in your binding definitions.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-app-settings -->

# App settings reference for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Application settings in a function app contain configuration options that affect all functions for that function app. These settings are accessed as environment variables. This article lists the app settings that are available in function apps.

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

In this article, example connection string values are truncated for readability.

Azure Functions uses the Azure App Service platform for hosting. You might find some settings relevant to hosting your function app in [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings).

## App setting considerations

When you use app settings, you should be aware of the following considerations:

Changing application settings causes your function app to restart by default across all hosting plans. For zero-downtime deployments when changing settings, use the

[Flex Consumption plan](flex-consumption-plan)with[rolling updates as the site update strategy](flex-consumption-site-updates). For other hosting plans, see[optimize deployments](functions-best-practices#optimize-deployments)for guidance on minimizing downtime.In setting names, double-underscore (

`__`

) and colon (`:`

) are considered reserved values. Double-underscores are interpreted as hierarchical delimiters on both Windows and Linux. Colons are interpreted in the same way only on Windows. For example, the setting`AzureFunctionsWebHost__hostid=somehost_123456`

would be interpreted as the following JSON object:`"AzureFunctionsWebHost": { "hostid": "somehost_123456" }`

In this article, only double-underscores are used, since they're supported on both operating systems. Most of the settings that support managed identity connections use double-underscores.

When functions runs locally, app settings are specified in the

`Values`

collection in the[local.settings.json](functions-develop-local#local-settings-file).There are other function app configuration options in the

[host.json](functions-host-json)file and in the[local.settings.json](functions-develop-local#local-settings-file)file.You can use application settings to override host.json setting values without having to change the host.json file itself. This approach is helpful for scenarios where you need to configure or modify specific host.json settings for a specific environment. This approach also lets you change host.json settings without having to republish your project. To learn more, see the

[host.json reference article](functions-host-json#override-hostjson-values).This article documents the settings that are most relevant to your function apps. Because Azure Functions runs on App Service, other application settings are also supported. For more information, see

[Environment variables and app settings in Azure App Service](../app-service/reference-app-settings).Some scenarios also require you to work with settings documented in

[App Service site settings](#app-service-site-settings).Changing any

*read-only*[App Service application settings](../app-service/reference-app-settings#app-environment)can put your function app into an unresponsive state.Take care when updating application settings by using REST APIs, including ARM templates. Because these APIs replace the existing application settings, you must include all existing settings when adding or modifying settings using REST APIs or ARM templates. When possible, use Azure CLI or Azure PowerShell to programmatically work with application settings. For more information, see

[Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

## APPINSIGHTS_INSTRUMENTATIONKEY

The instrumentation key for Application Insights. Don't use both `APPINSIGHTS_INSTRUMENTATIONKEY`

and `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When possible, use `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When Application Insights runs in a sovereign cloud, you must use `APPLICATIONINSIGHTS_CONNECTION_STRING`

. For more information, see [How to configure monitoring for Azure Functions](configure-monitoring).

| Key | Sample value |
|---|---|
| APPINSIGHTS_INSTRUMENTATIONKEY | `55555555-af77-484b-9032-64f83bb83bb` |

Don't use both `APPINSIGHTS_INSTRUMENTATIONKEY`

and `APPLICATIONINSIGHTS_CONNECTION_STRING`

. We recommend that you use `APPLICATIONINSIGHTS_CONNECTION_STRING`

.

## APPLICATIONINSIGHTS_AUTHENTICATION_STRING

Enables access to Application Insights by using Microsoft Entra authentication. Use this setting when you must connect to your Application Insights workspace by using Microsoft Entra authentication. For more information, see [Microsoft Entra authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication).

When you use `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

, the specific value that you set depends on the type of managed identity:

| Managed identity | Setting value |
|---|---|
| System-assigned | `Authorization=AAD` |
| User-assigned | `Authorization=AAD;ClientId=<USER_ASSIGNED_CLIENT_ID>` |

This authentication requirement is applied to connections from the Functions host, snapshot debugger, profiler, and any language-specific agents. To use this setting, the managed identity must already be available to the function app, with an assigned role equivalent to [Monitoring Metrics Publisher](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher).

Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

to connect to Application Insights using Microsoft Entra authentication, you should also [Disable local authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication#disable-local-authentication). This configuration requires Microsoft Entra authentication in order for telemetry to be ingested into your workspace.

## APPLICATIONINSIGHTS_CONNECTION_STRING

The connection string for Application Insights. Don't use both `APPINSIGHTS_INSTRUMENTATIONKEY`

and `APPLICATIONINSIGHTS_CONNECTION_STRING`

. We recommend the use of `APPLICATIONINSIGHTS_CONNECTION_STRING`

in all cases. It's a requirement in the following cases:

- When your function app requires the added customizations supported by using the connection string
- When your Application Insights instance runs in a sovereign cloud, which requires a custom endpoint

For more information, see [Connection strings](/en-us/azure/azure-monitor/app/sdk-connection-string).

| Key | Sample value |
|---|---|
| APPLICATIONINSIGHTS_CONNECTION_STRING | `InstrumentationKey=...` |

To connect to Application Insights with Microsoft Entra authentication, you should use [ APPLICATIONINSIGHTS_AUTHENTICATION_STRING](#applicationinsights_authentication_string).

## AZURE_FUNCTION_PROXY_DISABLE_LOCAL_CALL

Important

Azure Functions proxies was a feature of [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. For more information, see [Functions proxies](functions-proxies).

## AZURE_FUNCTION_PROXY_BACKEND_URL_DECODE_SLASHES

Important

Azure Functions proxies was a feature of [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. For more information, see [Functions proxies](functions-proxies).

## AZURE_FUNCTIONS_ENVIRONMENT

Configures the runtime [hosting environment](/en-us/dotnet/api/microsoft.extensions.hosting.environments) of the function app when running in Azure. This value is read during initialization. The runtime accepts only these values:

| Value | Description |
|---|---|
`Production` |
Represents a production environment, with reduced logging and full performance optimizations. This value is the default when `AZURE_FUNCTIONS_ENVIRONMENT` either isn't set or is set to an unsupported value. |
`Staging` |
Represents a staging environment, such as when running in a
|

`Development`

`AZURE_FUNCTIONS_ENVIRONMENT`

to `Development`

when running on your local computer. This setting can't be overridden in the local.settings.json file.Use this setting instead of `ASPNETCORE_ENVIRONMENT`

when you need to change the runtime environment in Azure to something other than `Production`

. For more information, see [Environment-based Startup class and methods](/en-us/aspnet/core/fundamentals/environments#environments).

This setting isn't available in version 1.x of the Functions runtime.

## AzureFunctionsJobHost__*

In version 2.x and later versions of the Functions runtime, application settings can override [host.json](functions-host-json) settings in the current environment. These overrides are expressed as application settings named `AzureFunctionsJobHost__path__to__setting`

. For more information, see [Override host.json values](functions-host-json#override-hostjson-values).

## AzureFunctionsWebHost__hostid

Sets the host ID for a given function app, which should be a unique ID. This setting overrides the automatically generated host ID value for your app. Use this setting only when you need to prevent host ID collisions between function apps that share the same storage account.

A host ID must meet the following requirements:

- Be between 1 and 32 characters
- Contain only lowercase letters, numbers, and dashes
- Not start or end with a dash
- Not contain consecutive dashes

An easy way to generate an ID is to take a GUID, remove the dashes, and make it lower case, such as by converting the GUID `1835D7B5-5C98-4790-815D-072CC94C6F71`

to the value `1835d7b55c984790815d072cc94c6f71`

.

| Key | Sample value |
|---|---|
| AzureFunctionsWebHost__hostid | `myuniquefunctionappname123456789` |

For more information, see [Host ID considerations](storage-considerations#host-id-considerations).

## AzureWebJobsDashboard

*This setting is deprecated and is only supported when running on version 1.x of the Azure Functions runtime.*

Optional storage account connection string for storing logs and displaying them in the **Monitor** tab in the Azure portal. The storage account must be a general-purpose one that supports blobs, queues, and tables. To learn more, see [Storage account requirements](storage-considerations#storage-account-requirements).

| Key | Sample value |
|---|---|
| AzureWebJobsDashboard | `DefaultEndpointsProtocol=https;AccountName=...` |

## AzureWebJobsDisableHomepage

A value of `true`

disables the default landing page that is shown for the root URL of a function app. The default value is `false`

.

| Key | Sample value |
|---|---|
| AzureWebJobsDisableHomepage | `true` |

When this app setting is omitted or set to `false`

, a page similar to the following example is displayed in response to the URL `<functionappname>.azurewebsites.net`

.


## AzureWebJobsDotNetReleaseCompilation

`true`

means use `Release`

mode when compiling .NET code. `false`

means use Debug mode. Default is `true`

.

| Key | Sample value |
|---|---|
| AzureWebJobsDotNetReleaseCompilation | `true` |

## AzureWebJobsFeatureFlags

A comma-delimited list of beta features to enable. Beta features enabled by these flags aren't production ready, but can be enabled for experimental use before they go live.

| Key | Sample value |
|---|---|
| AzureWebJobsFeatureFlags | `feature1,feature2,EnableProxies` |

If your app currently has this setting, add new flags to the end of the comma-delineated list.

Currently supported feature flags:

| Flag value | Description |
|---|---|
`EnableProxies` |
Re-enables proxies on version 4.x of the Functions runtime while you plan your migration to Azure API Management. For more information, see
|

`EnableAzureMonitorTimeIsoFormat`

`ISO 8601`

time format in Azure Monitor logs for Linux apps running on a Dedicated (App Service) plan.## AzureWebJobsKubernetesSecretName

Indicates the Kubernetes Secrets resource used for storing keys. Supported only when running in Kubernetes.

| Key | Sample value |
|---|---|
| AzureWebJobsKubernetesSecretName | `<SECRETS_RESOURCE>` |

Considerations when you use a Kubernetes Secrets resource:

- You must also set
`AzureWebJobsSecretStorageType`

to`kubernetes`

. When`AzureWebJobsKubernetesSecretName`

isn't set, the repository is considered read only. In this case, the values must be generated before deployment. - The
[Azure Functions Core Tools](functions-run-local)generates the values automatically when deploying to Kubernetes. [Immutable secrets](https://kubernetes.io/docs/concepts/configuration/secret/#secret-immutable)aren't supported and using them results in runtime errors.

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultClientId

The client ID of the user-assigned managed identity or the app registration used to access the vault where keys are stored. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

. Supported in version 4.x and later versions of the Functions runtime.

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultClientId | `<CLIENT_ID>` |

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultClientSecret

The secret for client ID of the user-assigned managed identity or the app registration used to access the vault where keys are stored. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

. Supported in version 4.x and later versions of the Functions runtime.

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultClientSecret | `<CLIENT_SECRET>` |

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultName

*This setting is deprecated and was only used when running on version 3.x of the Azure Functions runtime.*

The name of a key vault instance used to store keys. This setting was only used in version 3.x of the Functions runtime, which is no longer supported. For version 4.x, instead use `AzureWebJobsSecretStorageKeyVaultUri`

. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

.

The vault must have an access policy corresponding to the system-assigned managed identity of the hosting resource. The access policy should grant the identity the following secret permissions: `Get`

,`Set`

, `List`

, and `Delete`

.

When your functions run locally, the developer identity is used. Settings must be in the [local.settings.json file](functions-develop-local#local-settings-file).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultName | `<VAULT_NAME>` |

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultTenantId

The tenant ID of the app registration used to access the vault where keys are stored. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

. Supported in version 4.x and later versions of the Functions runtime. To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultTenantId | `<TENANT_ID>` |

## AzureWebJobsSecretStorageKeyVaultUri

The URI of a key vault instance used to store keys. Supported in version 4.x and later versions of the Functions runtime. We recommend this setting for using a key vault instance for key storage. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

.

The `AzureWebJobsSecretStorageKeyVaultUri`

value should be the full value of **Vault URI** displayed in the **Key Vault overview** tab, including `https://`

.

The vault must have an access policy corresponding to the system-assigned managed identity of the hosting resource. The access policy should grant the identity the following secret permissions: `Get`

,`Set`

, `List`

, and `Delete`

.

When your functions run locally, the developer identity is used, and settings must be in the [local.settings.json file](functions-develop-local#local-settings-file).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultUri | `https://<VAULT_NAME>.vault.azure.net` |

Important

Secrets aren't scoped to individual function apps through the `AzureWebJobsSecretStorageKeyVaultUri`

setting. If multiple function apps are configured to use the same Key Vault they share the same secrets, potentially leading to key collisions or overwrites. To avoid unintended behavior, we recommend that you use a separate Key Vault instance for each function app.

To learn more, see [Manage Key Storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageSas

A Blob Storage SAS URL for a second storage account used for key storage. By default, Functions uses the account set in `AzureWebJobsStorage`

. When using this secret storage option, make sure that `AzureWebJobsSecretStorageType`

isn't explicitly set or is set to `blob`

. To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageSas | `<BLOB_SAS_URL>` |

## AzureWebJobsSecretStorageType

Specifies the repository or provider to use for key storage. Keys are always encrypted before being stored using a secret unique to your function app.

| Key | Value | Description |
|---|---|---|
| AzureWebJobsSecretStorageType | `blob` |
Keys are stored in a Blob storage container in the account provided by the `AzureWebJobsStorage` setting. Blob storage is the default behavior when `AzureWebJobsSecretStorageType` isn't set.To specify a different storage account, use the `AzureWebJobsSecretStorageSas` setting to indicate the SAS URL of a second storage account. |
| AzureWebJobsSecretStorageType | `files` |
Keys are persisted on the file system. This behavior is the default for Functions v1.x. |
| AzureWebJobsSecretStorageType | `keyvault` |
Keys are stored in a key vault instance set by `AzureWebJobsSecretStorageKeyVaultName` . |
| AzureWebJobsSecretStorageType | `kubernetes` |
Supported only when running the Functions runtime in Kubernetes. When `AzureWebJobsKubernetesSecretName` isn't set, the repository is considered read only. In this case, the values must be generated before deployment. The
|

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsStorage

Specifies the connection string for an Azure Storage account that the Functions runtime uses for normal operations. Some uses of this storage account by Functions include key management, timer trigger management, and Event Hubs checkpoints. The storage account must be a general-purpose one that supports blobs, queues, and tables. For more information, see [Storage account requirements](storage-considerations#storage-account-requirements).

| Key | Sample value |
|---|---|
| AzureWebJobsStorage | `DefaultEndpointsProtocol=https;AccountName=...` |

Instead of a connection string, you can use an identity-based connection for this storage account. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobsStorage__accountName

When using an identity-based storage connection, sets the account name of the storage account instead of using the connection string in `AzureWebJobsStorage`

. This syntax is unique to `AzureWebJobsStorage`

and can't be used for other identity-based connections.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__accountName | `<STORAGE_ACCOUNT_NAME>` |

For sovereign clouds or when using a custom DNS, you must instead use the service-specific `AzureWebJobsStorage__*ServiceUri`

settings.

## AzureWebJobsStorage__blobServiceUri

When using an identity-based storage connection, sets the data plane URI of the blob service of the storage account.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__blobServiceUri | `https://<STORAGE_ACCOUNT_NAME>.blob.core.windows.net` |

Use this setting instead of `AzureWebJobsStorage__accountName`

in sovereign clouds or when using a custom DNS. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobsStorage__clientId

Sets the client ID of a specific user-assigned identity used to obtain an access token for managed identity authentication. Requires that `AzureWebJobsStorage__credential`

be set to `managedidentity`

. The value is a client ID that corresponds to an identity assigned to the application. You can't set both `AzureWebJobsStorage__managedIdentityResourceId`

and `AzureWebJobsStorage__clientId`

. When not set, the system-assigned identity is used.

## AzureWebJobsStorage__credential

Defines how an access token is obtained for the connection. Use `managedidentity`

for managed identity authentication. When using `managedidentity`

, a managed identity must be available in the hosting environment. Don't set `AzureWebJobsStorage__credential`

in local development scenarios.

## AzureWebJobsStorage__managedIdentityResourceId

Sets the resource identifier of a user-assigned identity used to obtain an access token for managed identity authentication. Requires that `AzureWebJobsStorage__credential`

be set to `managedidentity`

. The value is the resource ID of an identity assigned to the application used for managed identity authentication. You can't set both `AzureWebJobsStorage__managedIdentityResourceId`

and `AzureWebJobsStorage__clientId`

. When not set, the system-assigned identity is used.

## AzureWebJobsStorage__queueServiceUri

When using an identity-based storage connection, sets the data plane URI of the queue service of the storage account.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__queueServiceUri | `https://<STORAGE_ACCOUNT_NAME>.queue.core.windows.net` |

Use this setting instead of `AzureWebJobsStorage__accountName`

in sovereign clouds or when using a custom DNS. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobsStorage__tableServiceUri

When using an identity-based storage connection, sets data plane URI of a table service of the storage account.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__tableServiceUri | `https://<STORAGE_ACCOUNT_NAME>.table.core.windows.net` |

Use this setting instead of `AzureWebJobsStorage__accountName`

in sovereign clouds or when using a custom DNS. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobs_TypeScriptPath

Path to the compiler used for TypeScript. Allows you to override the default if you need to.

| Key | Sample value |
|---|---|
| AzureWebJobs_TypeScriptPath | `%HOME%\typescript` |

## DOCKER_REGISTRY_SERVER_PASSWORD

Indicates the password used to access a private container registry. This setting is only required when deploying your containerized function app from a private container registry. For more information, see [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings#custom-containers).

## DOCKER_REGISTRY_SERVER_URL

Indicates the URL of a private container registry. This setting is only required when deploying your containerized function app from a private container registry. For more information, see [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings#custom-containers).

## DOCKER_REGISTRY_SERVER_USERNAME

Indicates the account used to access a private container registry. This setting is only required when deploying your containerized function app from a private container registry. For more information, see [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings#custom-containers).

## DOCKER_SHM_SIZE

Sets the shared memory size (in bytes) when the Python worker is using shared memory. To learn more, see [Shared memory](https://github.com/Azure/azure-functions-python-worker/wiki/Shared-Memory).

| Key | Sample value |
|---|---|
| DOCKER_SHM_SIZE | `268435456` |

The preceding value sets a shared memory size of ~256 MB.

Requires that [FUNCTIONS_WORKER_SHARED_MEMORY_DATA_TRANSFER_ENABLED](#functions_worker_shared_memory_data_transfer_enabled) is set to `1`

.

## ENABLE_ORYX_BUILD

Indicates whether the [Oryx build system](https://github.com/microsoft/Oryx) is used during deployment. `ENABLE_ORYX_BUILD`

must be set to `true`

when doing remote build deployments to Linux. For more information, see [Remote build](functions-deployment-technologies#remote-build).

| Key | Sample value |
|---|---|
| ENABLE_ORYX_BUILD | `true` |

## FUNCTION_APP_EDIT_MODE

Indicates whether you can edit your function app in the Azure portal. Valid values are `readwrite`

and `readonly`

.

| Key | Sample value |
|---|---|
| FUNCTION_APP_EDIT_MODE | `readonly` |

The runtime sets the value based on the language stack and deployment status of your function app. For more information, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal).

## FUNCTIONS_EXTENSION_VERSION

The version of the Functions runtime that hosts your function app. A tilde (`~`

) with major version means use the latest version of that major version, for example, `~4`

. When new minor versions of the same major version are available, they're automatically installed in the function app.

| Key | Sample value |
|---|---|
| FUNCTIONS_EXTENSION_VERSION | `~4` |

The following major runtime version values are supported:

| Value | Runtime target | Comment |
|---|---|---|
`~4` |
4.x | Recommended |
`~1` |
1.x | Support ends September 14, 2026 |

A value of `~4`

means that your app runs on version 4.x of the runtime. A value of `~1`

pins your app to version 1.x of the runtime. Runtime versions 2.x and 3.x are no longer supported. For more information, see [Azure Functions runtime versions overview](functions-versions).

If requested by support to pin your app to a specific minor version, use the full version number, for example, `4.0.12345`

. For more information, see [How to target Azure Functions runtime versions](set-runtime-version).

## FUNCTIONS_INPROC_NET8_ENABLED

Indicates whether to an app can use .NET 8 on the in-process model. To use .NET 8 on the in-process model, this value must be set to `1`

. See [Updating to target .NET 8](functions-dotnet-class-library#updating-to-target-net-8) for complete instructions, including other required configuration values.

| Key | Sample value |
|---|---|
| FUNCTIONS_INPROC_NET8_ENABLED | `1` |

Set to `0`

to disable support for .NET 8 on the in-process model.

## FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR

This app setting is a temporary way for Node.js apps to enable a breaking change that makes entry point errors easier to troubleshoot on Node.js v18 or lower. We highly recommend using `true`

, especially for programming model v4 apps, which always use entry point files. The behavior without the breaking change (`false`

) ignores entry point errors and doesn't log them in Application Insights.

Starting with Node.js v20, the app setting has no effect and the breaking change behavior is always enabled.

For Node.js v18 or lower, the app setting is used, and the default behavior depends on if the error happens before or after a model v4 function has been registered:

- If the error is thrown before, the default behavior matches
`false`

. For example, if you're using model v3 or your entry point file doesn't exist. - If the error is thrown after, the default behavior matches
`true`

. For example, if you try to register duplicate model v4 functions.

| Key | Value | Description |
|---|---|---|
| FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR | `true` |
Block on entry point errors and log them in Application Insights. |
| FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR | `false` |
Ignore entry point errors and don't log them in Application Insights. |

## FUNCTIONS_REQUEST_BODY_SIZE_LIMIT

Overrides the default limit on the body size of requests sent to HTTP endpoints. The value is given in bytes, with a default maximum request size of 104,857,600 bytes.

| Key | Sample value |
|---|---|
| FUNCTIONS_REQUEST_BODY_SIZE_LIMIT | `250000000` |

## FUNCTIONS_V2_COMPATIBILITY_MODE

Important

This setting is no longer supported. It was originally provided to enable a short-term workaround for apps that targeted the v2.x runtime. They would be able to instead run on the v3.x runtime while it was still supported. Except for legacy apps that run on version 1.x, all function apps must run on version 4.x of the Functions runtime: `FUNCTIONS_EXTENSION_VERSION=~4`

. For more information, see [Azure Functions runtime versions overview](functions-versions).

## FUNCTIONS_WORKER_PROCESS_COUNT

Specifies the maximum number of language worker processes, with a default value of `1`

. The maximum value allowed is `10`

. Function invocations are evenly distributed among language worker processes. Language worker processes are spawned every 10 seconds until the count set by `FUNCTIONS_WORKER_PROCESS_COUNT`

is reached. Using multiple language worker processes isn't the same as [scaling](functions-scale). Consider using this setting when your workload has a mix of CPU-bound and I/O-bound invocations. This setting applies to all language runtimes, except for .NET running in process (`FUNCTIONS_WORKER_RUNTIME=dotnet`

).

| Key | Sample value |
|---|---|
| FUNCTIONS_WORKER_PROCESS_COUNT | `2` |

## FUNCTIONS_WORKER_RUNTIME

The language or language stack of the worker runtime to load in the function app. This value corresponds to the language being used in your application, for example, `python`

. Starting with version 2.x of the Azure Functions runtime, a given function app can only support a single language.

| Key | Sample value |
|---|---|
| FUNCTIONS_WORKER_RUNTIME | `node` |

Valid values:

| Value | Language/language stack |
|---|---|
`dotnet` |
|

`dotnet-isolated`

[C# (isolated worker process)](dotnet-isolated-process-guide)`java`

[Java](functions-reference-java)`node`

[JavaScript](functions-reference-node?tabs=javascript)[TypeScript](functions-reference-node?tabs=typescript)`powershell`

[PowerShell](functions-reference-powershell)`python`

[Python](functions-reference-python)`custom`

[Other](functions-custom-handlers)## FUNCTIONS_WORKER_SHARED_MEMORY_DATA_TRANSFER_ENABLED

This setting enables the Python worker to use shared memory to improve throughput. Enable shared memory when your Python function app is hitting memory bottlenecks.

| Key | Sample value |
|---|---|
| FUNCTIONS_WORKER_SHARED_MEMORY_DATA_TRANSFER_ENABLED | `1` |

With this setting enabled, you can use the [DOCKER_SHM_SIZE](#docker_shm_size) setting to set the shared memory size. To learn more, see [Shared memory](https://github.com/Azure/azure-functions-python-worker/wiki/Shared-Memory).

## JAVA_APPLICATIONINSIGHTS_ENABLE_TELEMETRY

Indicates whether the Java worker process should output telemetry in an Open Telemetry format to the Application Insights endpoint. Setting this flag to `True`

tells the Functions host to let the Java worker process stream OpenTelemetry logs directly, which prevents duplicate host-level entries. For more information, see [Configure application settings](opentelemetry-howto?pivots=programming-language-java#configure-application-settings).

## JAVA_ENABLE_SDK_TYPES

Enables your function app to use native Azure SDK types in bindings.

Note

Support for binding to SDK types is currently in preview and limited to the Azure Blob Storage SDK. For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

| Key | Sample value |
|---|---|
| JAVA_ENABLE_SDK_TYPES | `true` |

For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

## JAVA_OPTS

Used to customize the Java virtual machine (JVM) used to run your Java functions when running on a [Premium plan](functions-premium-plan) or [Dedicated plan](dedicated-plan). When running on a Consumption plan, instead use `languageWorkers__java__arguments`

. For more information, see [Customize JVM](functions-reference-java#customize-jvm).

## languageWorkers__java__arguments

Used to customize the Java virtual machine (JVM) used to run your Java functions when running on a [Consumption plan](functions-premium-plan). This setting does increase the cold start times for Java functions running in a Consumption plan. For a Premium or Dedicated plan, instead use `JAVA_OPTS`

. For more information, see [Customize JVM](functions-reference-java#customize-jvm).

## MDMaxBackgroundUpgradePeriod

Controls the managed dependencies background update period for PowerShell function apps, with a default value of `7.00:00:00`

(weekly).

Each PowerShell worker process initiates checking for module upgrades on the PowerShell Gallery on process start and every `MDMaxBackgroundUpgradePeriod`

after the start. When a new module version is available in the PowerShell Gallery, it's installed to the file system and made available to PowerShell workers. Decreasing this value lets your function app get newer module versions sooner, but it also increases the app resource usage, including network I/O, CPU, and storage. Increasing this value decreases the app's resource usage, but it can also delay delivering new module versions to your app.

| Key | Sample value |
|---|---|
| MDMaxBackgroundUpgradePeriod | `7.00:00:00` |

To learn more, see [Dependency management](functions-reference-powershell#dependency-management).

## MDNewSnapshotCheckPeriod

Specifies how often each PowerShell worker checks whether managed dependency upgrades are installed. The default frequency is `01:00:00`

(hourly).

After new module versions are installed to the file system, every PowerShell worker process must be restarted. Restarting PowerShell workers affects your app availability because it can interrupt current function execution. Until all PowerShell worker processes are restarted, function invocations can use either the old or the new module versions. Restarting all PowerShell workers completes within `MDNewSnapshotCheckPeriod`

.

Within every `MDNewSnapshotCheckPeriod`

, the PowerShell worker checks whether or not managed dependency upgrades are installed. When upgrades are installed, a restart is initiated. Increasing this value decreases the frequency of interruptions because of restarts. However, the increase might also increase the time during which function invocations could use either the old or the new module versions, nondeterministically.

| Key | Sample value |
|---|---|
| MDNewSnapshotCheckPeriod | `01:00:00` |

To learn more, see [Dependency management](functions-reference-powershell#dependency-management).

## MDMinBackgroundUpgradePeriod

The period of time after a previous managed dependency upgrade check before another upgrade check is started, with a default of `1.00:00:00`

(daily).

To avoid excessive module upgrades on frequent Worker restarts, checking for module upgrades isn't performed when any worker already initiated that check in the last `MDMinBackgroundUpgradePeriod`

.

| Key | Sample value |
|---|---|
| MDMinBackgroundUpgradePeriod | `1.00:00:00` |

To learn more, see [Dependency management](functions-reference-powershell#dependency-management).

## OTEL_EXPORTER_OTLP_ENDPOINT

Indicates the URL to which OpenTelemetry-formatted data is exported for ingestion. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## OTEL_EXPORTER_OTLP_HEADERS

Sets an optional list of headers that are applied to all outgoing data exported to an OpenTelemetry endpoint. You should use this setting when the OpenTelemetry endpoint requires to supply an API key. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## PIP_INDEX_URL

Overrides the default base URL of the Python Package Index (`https://pypi.org/simple`

) when running a remote build. Because this setting replaces the package index, you might see unexpected behaviour on restore. Only use this setting when you need to use a complete set of custom dependencies. When possible, you should instead use `PIP_EXTRA_URL`

, which lets you reference an additional package index. For more information, see [Custom dependencies](python-build-options#custom-dependencies) in the Python build article.

| Key | Sample value |
|---|---|
| PIP_INDEX_URL | `http://my.custom.package.repo/simple` |

These custom dependencies can be in a package index repository compliant with PEP 503 (the simple repository API) or in a local directory that follows the same format. For more information, see [ pip documentation for --index-url](https://pip.pypa.io/en/stable/cli/pip_wheel/?highlight=index%20url#cmdoption-i).


## PIP_EXTRA_INDEX_URL

The value for this setting indicates an extra index URL for custom packages for Python apps, to use in addition to the `--index-url`

. Use this setting when you need to run a remote build using custom dependencies that are found in an extra package index. For more information, see [Custom dependencies](python-build-options#custom-dependencies) in the Python build article.

| Key | Sample value |
|---|---|
| PIP_EXTRA_INDEX_URL | `http://my.custom.package.repo/simple` |

Should follow the same rules as `--index-url`

. For more information, see [ pip documentation for --extra-index-url](https://pip.pypa.io/en/stable/cli/pip_wheel/?highlight=index%20url#cmdoption-extra-index-url).


## PROJECT

A [continuous deployment](functions-continuous-deployment) setting that tells the Kudu deployment service the folder in a connected repository to location the deployable project.

| Key | Sample value |
|---|---|
| PROJECT | `WebProject/WebProject.csproj` |

## PYTHON_APPLICATIONINSIGHTS_ENABLE_TELEMETRY

Indicates whether the Python worker process should output telemetry in an Open Telemetry format to the Application Insights endpoint. Setting this flag to `True`

tells the Functions host to let the Python worker process export OpenTelemetry data to [Application Insights endpoint](#applicationinsights_connection_string). For more information, see [Configure application settings](opentelemetry-howto?pivots=programming-language-python#configure-application-settings).

## PYTHON_ISOLATE_WORKER_DEPENDENCIES

The configuration is specific to Python function apps. It defines the prioritization of module loading order. By default, this value is set to `0`

.

| Key | Value | Description |
|---|---|---|
| PYTHON_ISOLATE_WORKER_DEPENDENCIES | `0` |
Prioritize loading the Python libraries from internal Python worker's dependencies, which is the default behavior. Non-Microsoft libraries defined in requirements.txt might be shadowed. |
| PYTHON_ISOLATE_WORKER_DEPENDENCIES | `1` |
Prioritize loading the Python libraries from application's package defined in requirements.txt. This value prevents your libraries from colliding with internal Python worker's libraries. |

## PYTHON_ENABLE_DEBUG_LOGGING

Enables debug-level logging in a Python function app. A value of `1`

enables debug-level logging. Without this setting or with a value of `0`

, only information and higher-level logs are sent from the Python worker to the Functions host. Use this setting when debugging or tracing your Python function executions.

When debugging Python functions, make sure to also set a debug or trace [logging level](functions-host-json#logging) in the host.json file, as needed. To learn more, see [How to configure monitoring for Azure Functions](configure-monitoring).

## PYTHON_ENABLE_OPENTELEMETRY

Indicates whether the Python worker process should export telemetry to an Open Telemetry endpoint. Setting this flag to `True`

tells the Functions host to let the Python worker process export OpenTelemetry data to the configured [OTEL_EXPORTER_OTLP_ENDPOINT](#otel_exporter_otlp_endpoint). For more information, see [Configure application settings](opentelemetry-howto?pivots=programming-language-python#configure-application-settings).

## PYTHON_ENABLE_WORKER_EXTENSIONS

The configuration is specific to Python function apps. Setting this value to `1`

allows the worker to load in [Python worker extensions](develop-python-worker-extensions) defined in requirements.txt. It enables your function app to access new features provided by partner packages. It can also change the behavior of function load and invocation in your app. Ensure the extension you choose is trustworthy as you bear the risk of using it. Azure Functions gives no express warranties to any extensions. For how to use an extension, visit the extension's manual page or readme doc. By default, this value sets to `0`

.

| Key | Value | Description |
|---|---|---|
| PYTHON_ENABLE_WORKER_EXTENSIONS | `0` |
Disable any Python worker extension. |
| PYTHON_ENABLE_WORKER_EXTENSIONS | `1` |
Allow Python worker to load extensions from requirements.txt. |

## PYTHON_THREADPOOL_THREAD_COUNT

Specifies the maximum number of threads that a Python language worker would use to run function invocations, with a default value of `1`

for Python version `3.8`

and below. For Python version `3.9`

and above, the value is set to `None`

. This setting doesn't guarantee the number of threads that would be set during executions. The setting allows Python to expand the number of threads to the specified value. The setting only applies to Python functions apps. Additionally, the setting applies to synchronous functions invocation and not for coroutines.

| Key | Sample value | Max value |
|---|---|---|
| PYTHON_THREADPOOL_THREAD_COUNT | 2 | 32 |

## SCALE_CONTROLLER_LOGGING_ENABLED

*This setting is currently in preview.*

This setting controls logging from the Azure Functions scale controller. For more information, see [Scale controller logs](functions-monitoring#scale-controller-logs).

| Key | Sample value |
|---|---|
| SCALE_CONTROLLER_LOGGING_ENABLED | `AppInsights:Verbose` |

The value for this key is supplied in the format `<DESTINATION>:<VERBOSITY>`

, which is defined as follows:

| Property | Description |
|---|---|
`<DESTINATION>` |
The destination to which logs are sent. Valid values are `AppInsights` and `Blob` .When you use `AppInsights` , ensure that the
When you set the destination to `Blob` , logs are created in a blob container named `azure-functions-scale-controller` in the default storage account set in the `AzureWebJobsStorage` application setting. |
`<VERBOSITY>` |
Specifies the level of logging. Supported values are `None` , `Warning` , and `Verbose` .When set to `Verbose` , the scale controller logs a reason for every change in the worker count, and information about the triggers that factor into those decisions. Verbose logs include trigger warnings and the hashes used by the triggers before and after the scale controller runs. |

Tip

Keep in mind that while you leave scale controller logging enabled, it impacts the [potential costs of monitoring your function app](functions-monitoring#application-insights-pricing-and-limits). Consider enabling logging until you collect enough data to understand how the scale controller is behaving, and then disabling it.

## SCM_DO_BUILD_DURING_DEPLOYMENT

Controls remote build behavior during deployment. When `SCM_DO_BUILD_DURING_DEPLOYMENT`

is set to `true`

, the project is built remotely during deployment.

| Key | Sample value |
|---|---|
| SCM_DO_BUILD_DURING_DEPLOYMENT | `true` |

## SCM_LOGSTREAM_TIMEOUT

Controls the timeout, in seconds, when connected to streaming logs. The default value is 7200 (2 hours).

| Key | Sample value |
|---|---|
| SCM_LOGSTREAM_TIMEOUT | `1800` |

The preceding sample value of `1800`

sets a timeout of 30 minutes. For more information, see [Enable streaming execution logs in Azure Functions](streaming-logs).

## WEBSITE_CONTENTAZUREFILECONNECTIONSTRING

Connection string for storage account where the function app code and configuration are stored in event-driven scaling plans. For more information, see [Storage account connection setting](storage-considerations#storage-account-connection-setting).

| Key | Sample value |
|---|---|
| WEBSITE_CONTENTAZUREFILECONNECTIONSTRING | `DefaultEndpointsProtocol=https;AccountName=...` |

This setting is required for both Consumption and Elastic Premium plan apps. It's not required for Dedicated plan apps, which Functions doesn't dynamically scale.

The Flex Consumption plan is now the recommended serverless hosting plan for Azure Functions. It offers faster scaling, reduced cold starts, private networking, and more control over performance and cost. For more information, see [Flex Consumption plan](flex-consumption-plan).

Changing or removing this setting can cause your function app to not start. To learn more, see [this troubleshooting article](functions-recover-storage-account#storage-account-application-settings-were-deleted).

Azure Files doesn't currently support using managed identity when accessing the file share. For more information, see [Azure Files supported authentication scenarios](../storage/files/storage-files-active-directory-overview#supported-authentication-scenarios).

You might use a [KeyVault reference](../app-service/app-service-key-vault-references) for this connection setting. However, additional configuration is required to create and dynamically scale a function app in a Premium or Consumption plan when the storage connection string is maintained in a KeyVault. For more information, see [Considerations for Azure Files mounting](../app-service/app-service-key-vault-references#considerations-for-azure-files-mounting).

## WEBSITE_CONTENTOVERVNET

Important

WEBSITE_CONTENTOVERVNET is a legacy app setting that has been replaced by the [vnetContentShareEnabled](#vnetcontentshareenabled) site property.

A value of `1`

enables your function app to scale across stamps when you have your storage account restricted to a virtual network. You should enable this setting when restricting your storage account to a virtual network. Only required when using `WEBSITE_CONTENTSHARE`

and `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

. To learn more, see [Restrict your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network).

| Key | Sample value |
|---|---|
| WEBSITE_CONTENTOVERVNET | `1` |

This app setting is required for cross-stamp scaling on the [Elastic Premium](functions-premium-plan) and [Dedicated (App Service) plans](dedicated-plan) (Standard and higher) when the storage account is VNet-restricted. Without this setting, the function app can only scale within a single stamp (approximately 1-20 instances). Not supported when running on a [Consumption plan](consumption-plan).

Note

You must take special care when routing to the content share in a storage account shared by multiple function apps in the same plan. For more information, see [Consistent routing through virtual networks](storage-considerations#consistent-routing-through-virtual-networks) in the Storage considerations article.

## WEBSITE_CONTENTSHARE

The name of the file share that Functions uses to store function app code and configuration files. This content is required by event-driven scaling plans. Used with `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

. Default is a unique string generated by the runtime, which begins with the function app name. For more information, see [Storage account connection setting](storage-considerations#storage-account-connection-setting).

| Key | Sample value |
|---|---|
| WEBSITE_CONTENTSHARE | `functionapp091999e2` |

This setting is required only for Consumption and Premium plan apps. It's not required for Dedicated plan apps, which aren't dynamically scaled by Functions.

The Flex Consumption plan is now the recommended serverless hosting plan for Azure Functions. It offers faster scaling, reduced cold starts, private networking, and more control over performance and cost. For more information, see [Flex Consumption plan](flex-consumption-plan).

The share is created when your function app is created. Changing or removing this setting can cause your function app to not start. To learn more, see [this troubleshooting article](functions-recover-storage-account#storage-account-application-settings-were-deleted).

The following considerations apply when using an Azure Resource Manager (ARM) template or Bicep file to create a function app during deployment:

- When you don't set a
`WEBSITE_CONTENTSHARE`

value for the main function app or any apps in slots, unique share values are generated for you. Not setting`WEBSITE_CONTENTSHARE`

*is the recommended approach*for an ARM template deployment. - There are scenarios where you must set the
`WEBSITE_CONTENTSHARE`

value to a predefined value, such as when you[use a secured storage account in a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network). In this case, you must set a unique share name for the main function app and the app for each deployment slot. For a storage account secured by a virtual network, you must also create the share itself as part of your automated deployment. For more information, see[Secured deployments](functions-infrastructure-as-code#secured-deployments). - Don't make
`WEBSITE_CONTENTSHARE`

a slot setting. - When you specify
`WEBSITE_CONTENTSHARE`

, the value must follow[this guidance for share names](/en-us/rest/api/storageservices/naming-and-referencing-shares--directories--files--and-metadata#share-names).

## WEBSITE_DNS_SERVER

Sets the DNS server used by an app when resolving IP addresses. This setting is often required when using certain networking functionality, such as [Azure DNS private zones](functions-networking-options#azure-dns-private-zones) and [private endpoints](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).

| Key | Sample value |
|---|---|
| WEBSITE_DNS_SERVER | `168.63.129.16` |

## WEBSITE_ENABLE_BROTLI_ENCODING

Controls whether Brotli encoding is used for compression instead of the default gzip compression. When `WEBSITE_ENABLE_BROTLI_ENCODING`

is set to `1`

, Brotli encoding is used. Otherwise, gzip encoding is used.

## WEBSITE_FUNCTIONS_ARMCACHE_ENABLED

Disables caching when deploying function apps using Azure Resource Manager (ARM) templates.

| Key | Sample value |
|---|---|
| WEBSITE_FUNCTIONS_ARMCACHE_ENABLED | 0 |

## WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT

The maximum number of instances that the app can scale out to. Default is no limit.

Important

This setting is in preview. An [app property for function max scale out](event-driven-scaling#limit-scale-out) now exists. We recommend this property to limit scale-out.

| Key | Sample value |
|---|---|
| WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT | `5` |

## WEBSITE_NODE_DEFAULT_VERSION

*Windows only.*
Sets the version of Node.js to use when running your function app on Windows. You should use a tilde (`~`

) to have the runtime use the latest available version of the targeted major version. For example, when set to `~18`

, the latest version of Node.js 18 is used. When a major version is targeted with a tilde, you don't have to manually update the minor version.

| Key | Sample value |
|---|---|
| WEBSITE_NODE_DEFAULT_VERSION | `~18` |

## WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS

When you perform [a slot swap](functions-deployment-slots#swap-slots) on a function app running on a Premium plan, the swap can fail when the dedicated storage account used by the app is network restricted. This failure is caused by a legacy [application logging feature](../app-service/troubleshoot-diagnostic-logs#enable-application-logging-windows), which both Functions and App Service share. This setting overrides that legacy logging feature and allows the swap to occur.

| Key | Sample value |
|---|---|
| WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS | `0` |

Add `WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS`

with a value of `0`

to all slots to make sure that legacy diagnostic settings don't block your swaps. You can also add this setting and value to just the production slot as a [deployment slot ( sticky) setting](functions-deployment-slots#create-a-deployment-setting).

## WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS

By default, the version settings for function apps are specific to each slot. This setting is used when upgrading functions by using [deployment slots](functions-deployment-slots). This approach prevents unanticipated behavior due to changing versions after a swap. Set to `0`

in production and in the slot to make sure that all version settings are also swapped. For more information, see [Upgrade using slots](migrate-version-3-version-4#update-using-slots).

| Key | Sample value |
|---|---|
| WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS | `0` |

## WEBSITE_RUN_FROM_PACKAGE

Enables your function app to run from a package file, which can be locally mounted or deployed to an external URL.

| Key | Sample value |
|---|---|
| WEBSITE_RUN_FROM_PACKAGE | `1` |

Valid values are either a URL that resolves to the location of an external deployment package file, or `1`

. When set to `1`

, the package must be in the `d:\home\data\SitePackages`

folder. When you use zip deployment with `WEBSITE_RUN_FROM_PACKAGE`

enabled, the package is automatically uploaded to this location. For more information, see [Run your functions from a package file](run-functions-from-deployment-package).

When you use `WEBSITE_RUN_FROM_PACKAGE=<URL>`

, the URL must resolve to the package file location in an accessible storage location, such as an Azure Blob Storage container. The container must be private to prevent unauthorized access, which requires you to use either a shared access signature (SAS) in the URL or Microsoft Entra ID authentication to allow access. Using Microsoft Entra ID with managed identities is recommended.

This is an example of setting `WEBSITE_RUN_FROM_PACKAGE`

to the URL of a deployment package in an Azure Blog Storage container:

`WEBSITE_RUN_FROM_PACKAGE=https://contosostorageaccount.blob.core.windows.net/mycontainer/mypackage.zip`


When using SAS, you append the token to the URL as a query parameter.

When you [deploy a package from Azure Blob Storage using a user-assigned managed identity](run-functions-from-deployment-package#fetch-a-package-from-azure-blob-storage-using-a-managed-identity), you must also set [ WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID](#website_run_from_package_blob_mi_resource_id) to the resource ID of the user-assigned managed identity. When you deploy from an external package URL, you must also manually sync triggers. For more information, see

[Trigger syncing](functions-deployment-technologies#trigger-syncing).

## WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID

Indicates the resource ID of a user-assigned managed identity that's used when accessing a deployment package from an external Azure Blob Storage container secured using Microsoft Entra ID. This setting requires that [ WEBSITE_RUN_FROM_PACKAGE](#website_run_from_package) be set to the URL of the deployment package in a private container.

Setting `WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID=SystemAssigned`

is the same as omitting the setting, in which case the system-assigned managed identity for the app is used.

## WEBSITE_SKIP_CONTENTSHARE_VALIDATION

The [WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](#website_contentazurefileconnectionstring) and [WEBSITE_CONTENTSHARE](#website_contentshare) settings have extra validation checks to ensure that the app can be properly started. Creation of application settings fail when the function app can't properly call out to the downstream Storage Account or Key Vault due to networking constraints or other limiting factors. When WEBSITE_SKIP_CONTENTSHARE_VALIDATION is set to `1`

, the validation check is skipped. Otherwise, the value defaults to `0`

and the validation takes place.

| Key | Sample value |
|---|---|
| WEBSITE_SKIP_CONTENTSHARE_VALIDATION | `1` |

If validation is skipped and either the connection string or content share isn't valid, the app isn't able to start properly. In this case, functions return HTTP 500 errors. For more information, see [Troubleshoot error: "Azure Functions Runtime is unreachable"](functions-recover-storage-account).

## WEBSITE_SLOT_NAME

Read-only. Name of the current deployment slot. The name of the production slot is `Production`

.

| Key | Sample value |
|---|---|
| WEBSITE_SLOT_NAME | `Production` |

## WEBSITE_TIME_ZONE

Allows you to set the timezone for your function app.

| Key | OS | Sample value |
|---|---|---|
| WEBSITE_TIME_ZONE | Windows | `Eastern Standard Time` |
| WEBSITE_TIME_ZONE | Linux | `America/New_York` |

The default time zone used with the CRON expressions is Coordinated Universal Time (UTC). To have your CRON expression based on another time zone, create an app setting for your function app named `WEBSITE_TIME_ZONE`

.

The value of this setting depends on the operating system and plan on which your function app runs.

| Operating system | Plan | Value |
|---|---|---|
Windows |
All | Set the value to the name of the desired time zone as given by the second line from each pair given by the Windows command `tzutil.exe /L` |
Linux |
Premium Dedicated |
Set the value to the name of the desired time zone as shown in the
|

Note

`WEBSITE_TIME_ZONE`

and `TZ`

aren't currently supported when running on Linux in a [Flex Consumption](flex-consumption-plan) or [Consumption](consumption-plan) plan. In this case, the setting `WEBSITE_TIME_ZONE`

or `TZ`

can create SSL-related issues and cause metrics to stop working for your app.

For example, Eastern Time in the US (represented by `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux)) currently uses UTC-05:00 during standard time and UTC-04:00 during daylight time. To have a timer trigger fire at 10:00 AM Eastern Time every day, create an app setting for your function app named `WEBSITE_TIME_ZONE`

, set the value to `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux), and then use the following NCRONTAB expression:

```
"0 0 10 * * *"
```


When you use `WEBSITE_TIME_ZONE`

, the time is adjusted for time changes in the specific timezone, including daylight saving time and changes in standard time.

## WEBSITE_USE_PLACEHOLDER

Indicates whether to use a specific [cold start](event-driven-scaling#cold-start) optimization when running on the [Consumption plan](consumption-plan). Set to `0`

to disable the cold-start optimization on the Consumption plan.

| Key | Sample value |
|---|---|
| WEBSITE_USE_PLACEHOLDER | `1` |

## WEBSITE_USE_PLACEHOLDER_DOTNETISOLATED

Indicates whether to use a specific [cold start](event-driven-scaling#cold-start) optimization when running .NET isolated worker process functions on the [Consumption plan](consumption-plan). Set to `0`

to disable the cold-start optimization on the Consumption plan.

| Key | Sample value |
|---|---|
| WEBSITE_USE_PLACEHOLDER_DOTNETISOLATED | `1` |

## WEBSITE_VNET_ROUTE_ALL

Important

WEBSITE_VNET_ROUTE_ALL is a legacy app setting that has been replaced by the [vnetRouteAllEnabled](#vnetrouteallenabled) site setting.

Indicates whether all outbound traffic from the app is routed through the virtual network. A setting value of `1`

indicates that all application traffic is routed through the virtual network. You need this setting when configuring [Regional virtual network integration](functions-networking-options#regional-virtual-network-integration) in the Elastic Premium and Dedicated hosting plans. It's also used when a [virtual network NAT gateway is used to define a static outbound IP address](functions-how-to-use-nat-gateway).

| Key | Sample value |
|---|---|
| WEBSITE_VNET_ROUTE_ALL | `1` |

## WEBSITES_ENABLE_APP_SERVICE_STORAGE

Indicates whether the `/home`

directory is shared across scaled instances, with a default value of `true`

. You should set this value to `false`

when deploying your function app in a container.

## App Service site settings

Some configurations must be maintained at the App Service level as site settings, such as language versions. These settings are managed in the Azure portal, by using REST APIs, or by using Azure CLI or Azure PowerShell. The following are site settings that could be required, depending on your runtime language, OS, and versions.

## AcrUseManagedIdentityCreds

Indicates whether the image is obtained from an Azure Container Registry instance using managed identity authentication. A value of `true`

requires that you use managed identity. We recommend this approach over stored authentication credentials as a security best practice.

## AcrUserManagedIdentityID

Indicates the managed identity to use when obtaining the image from an Azure Container Registry instance. Requires that `AcrUseManagedIdentityCreds`

is set to `true`

. These values are valid:

| Value | Description |
|---|---|
`system` |
The system assigned managed identity of the function app is used. |
`<USER_IDENTITY_RESOURCE_ID>` |
The fully qualified resource ID of a user-assigned managed identity. |

The identity that you specify must be added to the `ACRPull`

role in the container registry. For more information, see [Create and configure a function app on Azure with the image](functions-deploy-container-apps?tabs=acr#create-and-configure-a-function-app-on-azure-with-the-image).

## alwaysOn

On a function app running in a [Dedicated (App Service) plan](dedicated-plan), the Functions runtime goes idle after a few minutes of inactivity, a which point only requests to an HTTP trigger *wakes up* your function app. To make sure that your non-HTTP triggered functions run correctly, including Timer trigger functions, enable Always On for the function app by setting the `alwaysOn`

site setting to a value of `true`

.

## functionsRuntimeAdminIsolationEnabled

Determines whether the built-in administrator (`/admin`

) endpoints in your function app can be accessed. When set to `false`

(the default), the app allows requests to endpoints under `/admin`

when those requests present a [master key](function-keys-how-to#understand-keys) in the request. When `true`

, `/admin`

endpoints can't be accessed, even with a master key.

This property can't be set for apps running on Linux in a Consumption plan. It can't be set for apps running on version 1.x of Azure Functions. If you're using version 1.x, you must first [migrate to version 4.x](migrate-version-1-version-4).

## linuxFxVersion

For function apps running on Linux, `linuxFxVersion`

indicates the language and version for the language-specific worker process. This information is used, along with [ FUNCTIONS_EXTENSION_VERSION](#functions_extension_version), to determine which specific Linux container image is installed to run your function app. This setting can be set to a predefined value or a custom image URI.

This value is set for you when you create your Linux function app. You might need to set it for ARM template and Bicep deployments and in certain upgrade scenarios.

### Valid linuxFxVersion values

You can use the following Azure CLI command to see a table of current `linuxFxVersion`

values, by supported Functions runtime version:

```
az functionapp list-runtimes --os linux --query "[].{stack:join(' ', [runtime, version]), LinuxFxVersion:linux_fx_version, SupportedFunctionsVersions:to_string(supported_functions_versions[])}" --output table
```


The previous command requires you to upgrade to version 2.40 of the Azure CLI.

### Custom images

When you create and maintain your own custom Linux container for your function app, the `linuxFxVersion`

value is instead in the format `DOCKER|<IMAGE_URI>`

, as in the following example:

```
linuxFxVersion = "DOCKER|contoso.com/azurefunctionsimage:v1.0.0"
```


This example indicates the registry source of the deployed container. For more information, see [Working with containers and Azure Functions](functions-how-to-custom-container).

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

## netFrameworkVersion

Sets the specific version of .NET for C# functions. For more information, see [Update your function app in Azure](migrate-version-3-version-4?pivots=programming-language-csharp#update-your-function-app-in-azure).

## powerShellVersion

Sets the specific version of PowerShell on which your functions run. For more information, see [Changing the PowerShell version](functions-reference-powershell#changing-the-powershell-version).

When running locally, you instead use the [ FUNCTIONS_WORKER_RUNTIME_VERSION](functions-reference-powershell#running-local-on-a-specific-version) setting in the local.settings.json file.

## vnetContentShareEnabled

Apps running in a Premium plan use a file share to store content. The name of this content share is stored in the [ WEBSITE_CONTENTSHARE](#website_contentshare) app setting and its connection string is stored in

[. To route traffic between your function app and content share through a virtual network, you must also set](#website_contentazurefileconnectionstring)

`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

`vnetContentShareEnabled`

to `true`

. Enabling this site property is required for cross-stamp scaling when [restricting your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network)in the Elastic Premium and Dedicated hosting plans. Without this setting, the function app can only scale within a single stamp (approximately 1-20 instances).

Note

You must take special care when routing to the content share in a storage account shared by multiple function apps in the same plan. For more information, see [Consistent routing through virtual networks](storage-considerations#consistent-routing-through-virtual-networks) in the Storage considerations article.

This site property replaces the legacy [ WEBSITE_CONTENTOVERVNET](#website_contentovervnet) setting.

## vnetImagePullEnabled

Functions [supports function apps running in Linux containers](functions-how-to-custom-container). To connect and pull from a container registry inside a virtual network, you must set `vnetImagePullEnabled`

to `true`

. This site property is supported in the Elastic Premium and Dedicated hosting plans. The Flex Consumption plan doesn't rely on site properties or app settings to configure Networking. For more information, see [Flex Consumption plan deprecations](#flex-consumption-plan-deprecations).

## vnetRouteAllEnabled

Indicates whether all outbound traffic from the app is routed through the virtual network. A setting value of `true`

indicates that all application traffic is routed through the virtual network. Use this setting when configuring [Regional virtual network integration](functions-networking-options#regional-virtual-network-integration) in the Elastic Premium and Dedicated plans. It's also used when a [virtual network NAT gateway is used to define a static outbound IP address](functions-how-to-use-nat-gateway). For more information, see [Configure application routing](../app-service/configure-vnet-integration-routing#configure-application-routing).

This site setting replaces the legacy [WEBSITE_VNET_ROUTE_ALL](#website_vnet_route_all) setting.

## Flex Consumption plan deprecations

In the [Flex Consumption plan](flex-consumption-plan), these site properties and application settings are deprecated and shouldn't be used when creating function app resources:

| Setting/property | Reason |
|---|---|
`ENABLE_ORYX_BUILD` |
Replaced by the `remoteBuild` parameter when deploying in Flex Consumption |
`FUNCTIONS_EXTENSION_VERSION` |
App Setting is set by the backend. A value of ~1 can be ignored. |
`FUNCTIONS_WORKER_RUNTIME` |
Replaced by `name` in `properties.functionAppConfig.runtime` |
`FUNCTIONS_WORKER_RUNTIME_VERSION` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`FUNCTIONS_MAX_HTTP_CONCURRENCY` |
Replaced by scale and concurrency's trigger section |
`FUNCTIONS_WORKER_PROCESS_COUNT` |
Setting not valid |
`FUNCTIONS_WORKER_DYNAMIC_CONCURRENCY_ENABLED` |
Setting not valid |
`SCM_DO_BUILD_DURING_DEPLOYMENT` |
Replaced by the `remoteBuild` parameter when deploying in Flex Consumption |
`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` |
Replaced by functionAppConfig's deployment section |
`WEBSITE_CONTENTOVERVNET` |
Not used for networking in Flex Consumption |
`WEBSITE_CONTENTSHARE` |
Replaced by functionAppConfig's deployment section |
`WEBSITE_DNS_SERVER` |
DNS is inherited from the integrated virtual network in Flex |
`WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT` |
Replaced by `maximumInstanceCount` in `properties.functionAppConfig.scaleAndConcurrency` |
`WEBSITE_NODE_DEFAULT_VERSION` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`WEBSITE_RUN_FROM_PACKAGE` |
Not used for deployments in Flex Consumption |
`WEBSITE_SKIP_CONTENTSHARE_VALIDATION` |
Content share isn't used in Flex Consumption |
`WEBSITE_VNET_ROUTE_ALL` |
Not used for networking in Flex Consumption |
`properties.alwaysOn` |
Not valid |
`properties.containerSize` |
Renamed as `instanceMemoryMB` |
`properties.ftpsState` |
FTPS not supported |
`properties.isReserved` |
Not valid |
`properties.IsXenon` |
Not valid |
`properties.javaVersion` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`properties.LinuxFxVersion` |
Replaced by `properties.functionAppConfig.runtime` |
`properties.netFrameworkVersion` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`properties.powerShellVersion` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`properties.siteConfig.functionAppScaleLimit` |
Renamed as `maximumInstanceCount` |
`properties.siteConfig.preWarmedInstanceCount` |
Renamed as `alwaysReadyInstances` |
`properties.use32BitWorkerProcess` |
32-bit not supported |
`properties.vnetBackupRestoreEnabled` |
Not used for networking in Flex Consumption |
`properties.vnetContentShareEnabled` |
Not used for networking in Flex Consumption |
`properties.vnetImagePullEnabled` |
Not used for networking in Flex Consumption |
`properties.vnetRouteAllEnabled` |
Not used for networking in Flex Consumption |
`properties.windowsFxVersion` |
Not valid |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-trigger -->

# Azure Blob storage trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Blob storage trigger starts a function when a new or updated blob is detected. The blob contents are provided as [input to the function](functions-bindings-storage-blob-input).

Tip

There are several ways to execute your function code based on changes to blobs in a storage container. If you choose to use the Blob storage trigger, there are two implementations offered: a polling-based one (referenced in this article) and an event-based one. It is recommended that you use the [event-based implementation](functions-event-grid-blob-trigger) as it has lower latency than the other. Also, the Flex Consumption plan supports only the event-based Blob storage trigger.

For details about differences between the two implementations of the Blob storage trigger, as well as other triggering options, see

[Working with blobs].

For information on setup and configuration details, see the [overview](functions-bindings-storage-blob).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example is a [C# function](dotnet-isolated-process-guide) that runs in an isolated worker process and uses a blob trigger with both blob input and blob output blob bindings. The function is triggered by the creation of a blob in the *test-samples-trigger* container. It reads a text file from the *test-samples-input* container and creates a new text file in an output container based on the name of the triggered file.

```
public static class BlobFunction
{
[Function(nameof(BlobFunction))]
[BlobOutput("test-samples-output/{name}-output.txt")]
public static string Run(
[BlobTrigger("test-samples-trigger/{name}")] string myTriggerItem,
[BlobInput("test-samples-input/sample1.txt")] string myBlob,
FunctionContext context)
{
var logger = context.GetLogger("BlobFunction");
logger.LogInformation("Triggered Item = {myTriggerItem}", myTriggerItem);
logger.LogInformation("Input Item = {myBlob}", myBlob);
// Blob Output
return "blob-output content";
}
}
```


This function uses a byte array to write a log when a blob is added or updated in the `myblob`

container.

```
@FunctionName("blobprocessor")
public void run(
@BlobTrigger(name = "file",
dataType = "binary",
path = "myblob/{name}",
connection = "MyStorageAccountAppSetting") byte[] content,
@BindingName("name") String filename,
final ExecutionContext context
) {
context.getLogger().info("Name: " + filename + " Size: " + content.length + " bytes");
}
```


This [SDK types example](functions-reference-java#sdk-types) uses `BlobClient`

to access properties of the blob.

```
@FunctionName("processBlob")
public void run(
@BlobTrigger(
name = "content",
path = "images/{name}",
connection = "AzureWebJobsStorage") BlobClient blob,
@BindingName("name") String file,
ExecutionContext ctx)
{
ctx.getLogger().info("Size = " + blob.getProperties().getBlobSize());
}
```


This [SDK types example](functions-reference-java#sdk-types) uses `BlobContainerClient`

to access info about blobs in the container that triggered the function.

```
@FunctionName("containerOps")
public void run(
@BlobTrigger(
name = "content",
path = "images/{name}",
connection = "AzureWebJobsStorage") BlobContainerClient container,
ExecutionContext ctx)
{
container.listBlobs()
.forEach(b -> ctx.getLogger().info(b.getName()));
}
```


This [SDK types example](functions-reference-java#sdk-types) uses `BlobClient`

to get information from the input binding about the blob that triggered the execution.

```
@FunctionName("checkAgainstInputBlob")
public void run(
@BlobInput(
name = "inputBlob",
path = "inputContainer/input.txt") BlobClient inputBlob,
@BlobTrigger(
name = "content",
path = "images/{name}",
connection = "AzureWebJobsStorage",
dataType = "string") String triggerBlob,
ExecutionContext ctx)
{
ctx.getLogger().info("Size = " + inputBlob.getProperties().getBlobSize());
}
```


This example shows how to get the BlobClient from both a Storage Blob trigger and from the input binding on an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import { app, InvocationContext } from "@azure/functions";
export async function storageBlobTrigger(
blobStorageClient: StorageBlobClient, // SDK binding provides this client
context: InvocationContext
): Promise<void> {
context.log(`Blob trigger processing: ${context.triggerMetadata.name}`);
// Access to full SDK capabilities
const blobProperties = await blobStorageClient.blobClient.getProperties();
context.log(`Blob size: ${blobProperties.contentLength}`);
// Download blob content
const downloadResponse = await blobStorageClient.blobClient.download();
context.log(`Content: ${downloadResponse}`);
}
// Register the function
app.storageBlob("storageBlobTrigger", {
path: "snippets/{name}",
connection: "AzureWebJobsStorage",
sdkBinding: true, // Enable SDK binding
handler: storageBlobTrigger,
});
```


This example shows how to get the `ContainerClient`

from both a Storage Blob input binding using an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import {
app,
HttpRequest,
HttpResponseInit,
input,
InvocationContext,
} from "@azure/functions";
const blobInput = input.storageBlob({
path: "snippets",
connection: "AzureWebJobsStorage",
sdkBinding: true,
});
export async function listBlobs(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
// Get input binding for a specific container
const storageBlobClient = context.extraInputs.get(
blobInput
) as StorageBlobClient;
// List all blobs in the container
const blobs = [];
for await (const blob of storageBlobClient.containerClient.listBlobsFlat()) {
blobs.push(blob.name);
}
return { jsonBody: { blobs } };
}
app.http("listBlobs", {
methods: ["GET"],
authLevel: "function",
extraInputs: [blobInput],
handler: listBlobs,
});
```


The following example shows a blob trigger [TypeScript code](functions-reference-node). The function writes a log when a blob is added or updated in the `samples-workitems`

container.

The string `{name}`

in the blob trigger path `samples-workitems/{name}`

creates a [binding expression](functions-bindings-expressions-patterns) that you can use in function code to access the file name of the triggering blob. For more information, see [Blob name patterns](#blob-name-patterns) later in this article.

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
handler: storageBlobTrigger1,
});
```


The following example shows a blob trigger [JavaScript code](functions-reference-node). The function writes a log when a blob is added or updated in the `samples-workitems`

container.

The string `{name}`

in the blob trigger path `samples-workitems/{name}`

creates a [binding expression](functions-bindings-expressions-patterns) that you can use in function code to access the file name of the triggering blob. For more information, see [Blob name patterns](#blob-name-patterns) later in this article.

```
const { app } = require('@azure/functions');
app.storageBlob('storageBlobTrigger1', {
path: 'samples-workitems/{name}',
connection: 'MyStorageAccountAppSetting',
handler: (blob, context) => {
context.log(
`Storage blob function processed blob "${context.triggerMetadata.name}" with size ${blob.length} bytes`
);
},
});
```


The following example demonstrates how to create a function that runs when a file is added to `source`

blob storage container.

The function configuration file (*function.json*) includes a binding with the `type`

of `blobTrigger`

and `direction`

set to `in`

.

```
{
"bindings": [
{
"name": "InputBlob",
"type": "blobTrigger",
"direction": "in",
"path": "source/{name}",
"connection": "MyStorageAccountConnectionString"
}
]
}
```


Here's the associated code for the *run.ps1* file.

```
param([byte[]] $InputBlob, $TriggerMetadata)
Write-Host "PowerShell Blob trigger: Name: $($TriggerMetadata.Name) Size: $($InputBlob.Length) bytes"
```


This example uses SDK types to directly access the underlying [ BlobClient](/en-us/python/api/azure-storage-blob/azure.storage.blob.blobclient) object provided by the Blob storage trigger:

```
import azure.functions as func
import azurefunctions.extensions.bindings.blob as blob
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.blob_trigger(
arg_name="client", path="PATH/TO/BLOB", connection="AzureWebJobsStorage"
)
def blob_trigger(client: blob.BlobClient):
logging.info(
f"Python blob trigger function processed blob \n"
f"Properties: {client.get_blob_properties()}\n"
f"Blob content head: {client.download_blob().read(size=1)}"
)
```


For examples of using other SDK types, see the [ ContainerClient](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py) and

[samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_storagestreamdownloader/function_app.py)

`StorageStreamDownloader`

[Python SDK Bindings for Blob Sample](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python).

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

This example logs information from the incoming blob metadata.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="BlobTrigger1")
@app.blob_trigger(arg_name="myblob",
path="PATH/TO/BLOB",
connection="CONNECTION_SETTING")
def test_function(myblob: func.InputStream):
logging.info(f"Python blob trigger function processed blob \n"
f"Name: {myblob.name}\n"
f"Blob Size: {myblob.length} bytes")
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the [BlobAttribute](/en-us/dotnet/api/microsoft.azure.webjobs.blobattribute) attribute to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#blob-trigger).

The attribute's constructor takes the following parameters:

| Parameter | Description |
|---|---|
BlobPath |
The path to the blob. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

**Access****Source**`BlobTriggerSource.EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is`BlobTriggerSource.LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container.Here's an `BlobTrigger`

attribute in a method signature:

```
[Function(nameof(BlobFunction))]
[BlobOutput("test-samples-output/{name}-output.txt")]
public static string Run(
[BlobTrigger("test-samples-trigger/{name}")] string myTriggerItem,
[BlobInput("test-samples-input/sample1.txt")] string myBlob,
FunctionContext context)
```


When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using decorators, the following properties on the `blob_trigger`

decorator define the Blob Storage trigger:

| Property | Description |
|---|---|
`arg_name` |
Declares the parameter name in the function signature. When the function is triggered, this parameter's value has the contents of the queue message. |
`path` |
The
|

`connection`

`source`

`EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is`LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container.For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `@BlobTrigger`

attribute is used to give you access to the blob that triggered the function. Refer to the [trigger example](#example) for details. Use the `source`

property to set the source of the triggering event. Use `EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is `LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container. |

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.storageBlob()`

method.

| Property | Description |
|---|---|
path |
The
|

**connection**[Connections](#connections).**source**`EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is`LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container.The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blobTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. Exceptions are noted in the
|
name |
The name of the variable that represents the blob in function code. |
path |
The
|

**connection**[Connections](#connections).**source**`EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is`LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container.See the [Example section](#example) for complete examples.

## Metadata

The blob trigger provides several metadata properties. These properties can be used as part of binding expressions in other bindings or as parameters in your code. These values have the same semantics as the [CloudBlob](/en-us/dotnet/api/microsoft.azure.storage.blob.cloudblob) type.

| Property | Type | Description |
|---|---|---|
`BlobTrigger` |
`string` |
The path to the triggering blob. |
`Uri` |
`System.Uri` |
The blob's URI for the primary location. |
`Properties` |
|

`Metadata`

`IDictionary<string,string>`

The following example logs the path to the triggering blob, including the container:

```
public static void Run(string myBlob, string blobTrigger, ILogger log)
{
log.LogInformation($"Full blob path: {blobTrigger}");
}
```


## Metadata

The blob trigger provides several metadata properties. These properties can be used as part of binding expressions in other bindings or as parameters in your code.

| Property | Description |
|---|---|
`blobTrigger` |
The path to the triggering blob. |
`uri` |
The blob's URI for the primary location. |
`properties` |
The blob's system properties. |
`metadata` |
The user-defined metadata for the blob. |

## Metadata

Metadata is available through the `$TriggerMetadata`

parameter.

## Usage

The binding types supported by Blob trigger depend on the extension package version and the C# modality used in your function app.

The blob trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

Binding to `string`

, or `Byte[]`

is only recommended when the blob size is small. This is recommended because the entire blob contents are loaded into memory. For most blobs, use a `Stream`

or `BlobClient`

type. For more information, see [Concurrency and memory usage](functions-bindings-storage-blob-trigger#memory-usage-and-concurrency).

If you get an error message when trying to bind to one of the Storage SDK types, make sure that you have a reference to [the correct Storage SDK version](functions-bindings-storage-blob#tabpanel_2_functionsv1_in-process).

You can also use the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) to specify the storage account to use. You can do this when you need to use a different storage account than other functions in the library. The constructor takes the name of an app setting that contains a storage connection string. The attribute can be applied at the parameter, method, or class level. The following example shows class level and method level:

```
[StorageAccount("ClassLevelStorageAppSetting")]
public static class AzureFunctions
{
[FunctionName("BlobTrigger")]
[StorageAccount("FunctionLevelStorageAppSetting")]
public static void Run( //...
{
....
}
```


The storage account to use is determined in the following order:

- The
`BlobTrigger`

attribute's`Connection`

property. - The
`StorageAccount`

attribute applied to the same parameter as the`BlobTrigger`

attribute. - The
`StorageAccount`

attribute applied to the function. - The
`StorageAccount`

attribute applied to the class. - The default storage account for the function app, which is defined in the
`AzureWebJobsStorage`

application setting.

Note

Support for binding to SDK types is currently in preview and limited to the Azure Blob Storage SDK. For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

Access the blob data via a parameter that matches the name designated by binding's name parameter in the *function.json* file.

Access blob data via the parameter typed as [InputStream](/en-us/python/api/azure-functions/azure.functions.inputstream). Refer to the [trigger example](#example) for details.

Functions also support Python SDK type bindings for Azure Blob storage, which lets you work with blob data using these underlying SDK types:

Note

Only synchronous SDK types are supported.

Important

SDK types support for Python is generally available and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to Azure Blobs. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage). The connection string must be for a general-purpose storage account, not a [Blob storage account](../storage/common/storage-account-overview#types-of-storage-accounts).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage". If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [version 5.x or higher of the extension](functions-bindings-storage-blob#install-extension) ([bundle 3.x or higher](functions-bindings-storage-blob?tabs=extensionv3#install-bundle) for non-.NET language stacks), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Blob Service URI | `<CONNECTION_NAME_PREFIX>__serviceUri` 1 |
The data plane URI of the blob service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.blob.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__blobServiceUri`

can be used as an alias. If the connection configuration will be used by a blob trigger, `blobServiceUri`

must also be accompanied by `queueServiceUri`

. See below.

The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables. The URI can only designate the blob service. As an alternative, you can provide a URI specifically for each service, allowing a single connection to be used. If both versions are provided, the multi-service form is used. To configure the connection for multiple services, instead of `<CONNECTION_NAME_PREFIX>__serviceUri`

, set:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Blob Service URI | `<CONNECTION_NAME_PREFIX>__blobServiceUri` |
The data plane URI of the blob service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.blob.core.windows.net |
Queue Service URI (required for blob triggers2) |
`<CONNECTION_NAME_PREFIX>__queueServiceUri` |
The data plane URI of a queue service, using the HTTPS scheme. This value is only needed for blob triggers. | https://<storage_account_name>.queue.core.windows.net |

2 The blob trigger handles failure across multiple retries by writing [poison blobs](functions-bindings-storage-blob-trigger#poison-blobs) to a queue. In the `serviceUri`

form, the `AzureWebJobsStorage`

connection is used. However, when specifying `blobServiceUri`

, a queue service URI must also be provided with `queueServiceUri`

. It's recommended that you use the service from the same storage account as the blob service. You also need to make sure the trigger can read and write messages in the configured queue service by assigning a role like [Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor).

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You need to create a role assignment that provides access to your blob container at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Blob Storage extension in normal operation. Your application may require further permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
and
1Extra permissions must also be granted to the AzureWebJobsStorage connection. 2 |

[Storage Blob Data Reader](../role-based-access-control/built-in-roles#storage-blob-data-reader)[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner)1 The blob trigger handles failure across multiple retries by writing [poison blobs](functions-bindings-storage-blob-trigger#poison-blobs) to a queue on the storage account specified by the connection.

2 The AzureWebJobsStorage connection is used internally for blobs and queues that enable the trigger. If it's configured to use an identity-based connection, it needs extra permissions beyond the default requirement. The required permissions are covered by the [Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner), [Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor), and [Storage Account Contributor](../role-based-access-control/built-in-roles#storage-account-contributor) roles. To learn more, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## Blob name patterns

You can specify a blob name pattern in the `path`

property in *function.json* or in the `BlobTrigger`

attribute constructor. The name pattern can be a [filter or binding expression](functions-bindings-expressions-patterns). The following sections provide examples.

Tip

A container name can't contain a resolver in the name pattern.

### Get file name and extension

The following example shows how to bind to the blob file name and extension separately:

```
"path": "input/{blobname}.{blobextension}",
```


If the blob is named *original-Blob1.txt*, the values of the `blobname`

and `blobextension`

variables in function code are *original-Blob1* and *txt*.

### Filter on blob name

The following example triggers only on blobs in the `input`

container that start with the string "original-":

```
"path": "input/original-{name}",
```


If the blob name is *original-Blob1.txt*, the value of the `name`

variable in function code is `Blob1.txt`

.

### Filter on file type

The following example triggers only on *.png* files:

```
"path": "samples/{name}.png",
```


### Filter on curly braces in file names

To look for curly braces in file names, escape the braces by using two braces. The following example filters for blobs that have curly braces in the name:

```
"path": "images/{{20140101}}-{name}",
```


If the blob is named *{20140101}-soundfile.mp3*, the `name`

variable value in the function code is *soundfile.mp3*.

## Polling and latency

Polling works as a hybrid between inspecting logs and running periodic container scans. Blobs are scanned in groups of 10,000 at a time with a continuation token used between intervals. If your function app is on the Consumption plan, there can be up to a 10-minute delay in processing new blobs if a function app has gone idle.

Warning

[Storage logs are created on a "best effort"](/en-us/rest/api/storageservices/About-Storage-Analytics-Logging) basis. There's no guarantee that all events are captured. Under some conditions, logs may be missed.

If you require faster or more reliable blob processing, you should consider switching your hosting to use an App Service plan with Always On enabled, which may result in increased costs. You might also consider using a trigger other than the classic polling blob trigger. For more information and a comparison of the various triggering options for blob storage containers, see [Trigger on a blob container](storage-considerations#trigger-on-a-blob-container).

## Blob receipts

The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob. To determine if a given blob version has been processed, it maintains *blob receipts*.

Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`

). A blob receipt has the following information:

- The triggered function (
`<FUNCTION_APP_NAME>.Functions.<FUNCTION_NAME>`

, for example:`MyFunctionApp.Functions.CopyBlob`

) - The container name
- The blob type (
`BlockBlob`

or`PageBlob`

) - The blob name
- The ETag (a blob version identifier, for example:
`0x8D1DC6E70A277EF`

)

To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually. While reprocessing might not occur immediately, it's guaranteed to occur at a later point in time. To reprocess immediately, the *scaninfo* blob in *azure-webjobs-hosts/blobscaninfo* can be updated. Any blobs with a last modified timestamp after the `LatestScan`

property will be scanned again.

## Poison blobs

When a blob trigger function fails for a given blob, Azure Functions retries that function a total of five times by default.

If all five tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*. The maximum number of retries is configurable. The same MaxDequeueCount setting is used for poison blob handling and poison queue message handling. The queue message for poison blobs is a JSON object that contains the following properties:

- FunctionId (in the format
`<FUNCTION_APP_NAME>.Functions.<FUNCTION_NAME>`

) - BlobType (
`BlockBlob`

or`PageBlob`

) - ContainerName
- BlobName
- ETag (a blob version identifier, for example:
`0x8D1DC6E70A277EF`

)

## Memory usage and concurrency

When you bind to an [output type](#usage) that doesn't support streaming, such as `string`

, or `Byte[]`

, the runtime must load the entire blob into memory more than one time during processing. This can result in higher-than expected memory usage when processing blobs. When possible, use a stream-supporting type. Type support depends on the C# mode and extension version. For more information, see [Binding types](functions-bindings-storage-blob#binding-types).

At this time, the runtime must load the entire blob into memory more than one time during processing. This can result in higher-than expected memory usage when processing blobs.

Memory usage can be further impacted when multiple function instances are concurrently processing blob data. If you are having memory issues using a Blob trigger, consider reducing the number of concurrent executions permitted. Reducing the concurrency can have the side effect of increasing the backlog of blobs waiting to be processed. The memory limits of your function app depend on the plan. For more information, see [Service limits](functions-scale#service-limits).

The way that you can control the number of concurrent executions depends on the version of the Storage extension you are using.

When using version 5.0.0 of the Storage extension or a later version, you control trigger concurrency by using the `maxDegreeOfParallelism`

setting in the [blobs configuration in host.json](functions-bindings-storage-blob#hostjson-settings).

Limits apply separately to each function that uses a blob trigger.

## host.json properties

The [host.json](functions-host-json#blobs) file contains settings that control blob trigger behavior. See the [host.json settings](functions-bindings-storage-blob#hostjson-settings) section for details regarding available settings.

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/create-resources-azure-powershell -->

# Create function app resources in Azure using PowerShell

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure PowerShell example scripts in this article create function apps and other resources required to host your functions in Azure. A function app provides an execution context in which your functions are executed. All functions running in a function app share the same resources and connections, and they're all scaled together.

After the resources are created, you can deploy your project files to the new function app. To learn more, see [Deployment methods](functions-deployment-technologies#deployment-methods).

Every function app requires your PowerShell scripts to create the following resources:

| Resource | cmdlet | Description |
|---|---|---|
| Resource group |
|

[resource group](../azure-resource-manager/management/overview)in which you'll create your function app.[New-AzStorageAccount](/en-us/powershell/module/az.storage/new-azstorageaccount)[storage account](../storage/common/storage-account-create)used by your function app. Storage account names must be between 3 and 24 characters in length and can contain numbers and lowercase letters only. You can also use an existing account, which must meet the[storage account requirements](storage-considerations#storage-account-requirements).[New-AzFunctionAppPlan](/en-us/powershell/module/az.functions/new-azfunctionappplan)[Consumption plan](consumption-plan), since Consumption plans are created when you run`New-AzFunctionApp`

. For more information, see [Azure Functions hosting options](functions-scale).[New-AzFunctionApp](/en-us/powershell/module/az.functions/new-azfunctionapp)`-Name`

parameter must be a globally unique name across all of Azure App Service. Valid characters in `-Name`

are `a-z`

(case insensitive), `0-9`

, and `-`

. Most examples create a function app that supports C# functions. You can change the language by using the `-Runtime`

parameter, with supported values of `DotNet`

, `Java`

, `Node`

, `PowerShell`

, and `Python`

. Use the `-RuntimeVersion`

to choose a [specific language version](supported-languages#languages-by-runtime-version).This article contains the following examples:

[Create a serverless function app for C#](#create-a-serverless-function-app-for-c)[Create a serverless function app for Python](#create-a-serverless-function-app-for-python)[Create a scalable function app in a Premium plan](#create-a-scalable-function-app-in-a-premium-plan)[Create a function app in a Dedicated plan](#create-a-function-app-in-a-dedicated-plan)[Create a function app with a named Storage connection](#create-a-function-app-with-a-named-storage-connection)[Create a function app with an Azure Cosmos DB connection](#create-a-function-app-with-an-azure-cosmos-db-connection)[Create a function app with continuous deployment](#create-a-function-app-with-continuous-deployment)[Create a serverless Python function app and mount file share](#create-a-serverless-python-function-app-and-mount-file-share)

## Prerequisites

- If you choose to use Azure PowerShell locally:
[Install the latest version of the Az PowerShell module](/en-us/powershell/azure/install-azure-powershell).- Connect to your Azure account using the
[Connect-AzAccount](/en-us/powershell/module/az.accounts/connect-azaccount)cmdlet.

- If you choose to use Azure Cloud Shell:
- See
[Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview)for more information.

- See

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create a serverless function app for C#

The following script creates a serverless C# function app in the default Consumption plan:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-consumption"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a serverless function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -Runtime DotNet-Isolated -FunctionsVersion $functionsVersion
```


## Create a serverless function app for Python

The following script creates a serverless Python function app in a Consumption plan:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-consumption-python"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-python-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
$pythonVersion = "3.9" #Allowed values: 3.7, 3.8, and 3.9
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a serverless Python function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -OSType Linux -Runtime Python -RuntimeVersion $pythonVersion -FunctionsVersion $functionsVersion
```


## Create a scalable function app in a Premium plan

The following script creates a C# function app in an Elastic Premium plan that supports [dynamic scale](event-driven-scaling):

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-premium-plan"}
$storage = "msdocsaccount$randomIdentifier"
$premiumPlan = "msdocs-premium-plan-$randomIdentifier"
$functionApp = "msdocs-function-$randomIdentifier"
$skuStorage = "Standard_LRS" # Allowed values: Standard_LRS, Standard_GRS, Standard_RAGRS, Standard_ZRS, Premium_LRS, Premium_ZRS, Standard_GZRS, Standard_RAGZRS
$skuPlan = "EP1"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a Premium plan
Write-Host "Creating $premiumPlan"
New-AzFunctionAppPlan -Name $premiumPlan -ResourceGroupName $resourceGroup -Location $location -Sku $skuPlan -WorkerType Windows
# Create a Function App
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -PlanName $premiumPlan -ResourceGroupName $resourceGroup -Runtime DotNet -FunctionsVersion $functionsVersion
```


## Create a function app in a Dedicated plan

The following script creates a function app hosted in a Dedicated plan, which isn't scaled dynamically by Functions:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-app-service-plan"}
$storage = "msdocsaccount$randomIdentifier"
$appServicePlan = "msdocs-app-service-plan-$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$skuPlan = "B1"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create an App Service plan
Write-Host "Creating $appServicePlan"
New-AzFunctionAppPlan -Name $appServicePlan -ResourceGroupName $resourceGroup -Location $location -Sku $skuPlan -WorkerType Windows
# Create a Function App
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -PlanName $appServicePlan -ResourceGroupName $resourceGroup -Runtime DotNet -FunctionsVersion $functionsVersion
```


## Create a function app with a named Storage connection

The following script creates a function app with a named Storage connection in application settings:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-connect-to-storage-account"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a serverless function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -Runtime DotNet -FunctionsVersion $functionsVersion
# Get the storage account connection string.
$connstr = (Get-AzStorageAccount -StorageAccountName $storage -ResourceGroupName $resourceGroup).Context.ConnectionString
# Update function app settings to connect to the storage account.
Update-AzFunctionAppSetting -Name $functionApp -ResourceGroupName $resourceGroup -AppSetting @{StorageConStr = $connstr}
```


## Create a function app with an Azure Cosmos DB connection

The following script creates a function app and a connected Azure Cosmos DB account:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-connect-to-cosmos-db"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a serverless function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -Runtime DotNet -FunctionsVersion $functionsVersion
# Create an Azure Cosmos DB database account using the same function app name.
Write-Host "Creating $functionApp"
New-AzCosmosDBAccount -Name $functionApp -ResourceGroupName $resourceGroup -Location $location
# Get the Azure Cosmos DB connection string.
$endpoint = (Get-AzCosmosDBAccount -Name $functionApp -ResourceGroupName $resourceGroup).DocumentEndpoint
Write-Host $endpoint
$key = (Get-AzCosmosDBAccountKey -Name $functionApp -ResourceGroupName $resourceGroup).PrimaryMasterKey
Write-Host $key
# Configure function app settings to use the Azure Cosmos DB connection string.
Update-AzFunctionAppSetting -Name $functionApp -ResourceGroupName $resourceGroup -AppSetting @{CosmosDB_Endpoint = $endpoint; CosmosDB_Key = $key}
```


## Create a function app with continuous deployment

The following script creates a function app that has continuous deployment configured to publish from a public GitHub repository:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "deploy-function-app-with-function-github"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "mygithubfunc$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
$runtime = "Node"
# Public GitHub repository containing an Azure Functions code project.
$gitrepo = "https://github.com/Azure-Samples/functions-quickstart-javascript"
<# Set GitHub personal access token (PAT) to enable authenticated GitHub deployment in your subscription when using a private repo.
$token = <Replace with a GitHub access token when using a private repo.>
$propertiesObject = @{
token = $token
}
Set-AzResource -PropertyObject $propertiesObject -ResourceId /providers/Microsoft.Web/sourcecontrols/GitHub -ApiVersion 2018-02-01 -Force
#>
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -Runtime $runtime -FunctionsVersion $functionsVersion
# Configure GitHub deployment from a public GitHub repo and deploy once.
$propertiesObject = @{
repoUrl = $gitrepo
branch = 'main'
isManualIntegration = $True # $False when using a private repo
}
Set-AzResource -PropertyObject $propertiesObject -ResourceGroupName $resourceGroup -ResourceType Microsoft.Web/sites/sourcecontrols -ResourceName $functionApp/web -ApiVersion 2018-02-01 -Force
# Connect to function application
Invoke-RestMethod -Uri "https://$functionApp.azurewebsites.net/api/httpexample?name=Azure"
```


## Create a serverless Python function app and mount file share

The following script creates a Python function app on Linux and creates and mounts an external Azure Files share:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "functions-cli-mount-files-storage-linux"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
$pythonVersion = "3.9" #Allowed values: 3.7, 3.8, and 3.9
$share = "msdocs-fileshare-$randomIdentifier"
$directory = "msdocs-directory-$randomIdentifier"
$shareId = "msdocs-share-$randomIdentifier"
$mountPath = "/mounted-$randomIdentifier"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Get the storage account key.
$keys = Get-AzStorageAccountKey -Name $storage -ResourceGroupName $resourceGroup
$storageKey = $keys[0].Value
## Create a serverless Python function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -OSType Linux -Runtime Python -RuntimeVersion $pythonVersion -FunctionsVersion $functionsVersion
# Create a share in Azure Files.
Write-Host "Creating $share"
$storageContext = New-AzStorageContext -StorageAccountName $storage -StorageAccountKey $storageKey
New-AzStorageShare -Name $share -Context $storageContext
# Create a directory in the share.
Write-Host "Creating $directory in $share"
New-AzStorageDirectory -ShareName $share -Path $directory -Context $storageContext
# Add a storage account configuration to the function app
Write-Host "Adding $storage configuration"
$storagePath = New-AzWebAppAzureStoragePath -Name $shareid -Type AzureFiles -ShareName $share -AccountName $storage -MountPath $mountPath -AccessKey $storageKey
Set-AzWebApp -Name $functionApp -ResourceGroupName $resourceGroup -AzureStoragePath $storagePath
# Get a function app's storage account configurations.
(Get-AzWebApp -Name $functionApp -ResourceGroupName $resourceGroup).AzureStoragePath
```


Mounted file shares are only supported on Linux. For more information, see [Mount file shares](storage-considerations#mount-file-shares).

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, delete the resource group by running the following PowerShell command:

```
Remove-AzResourceGroup -Name myResourceGroup
```


This command might take a minute to run.

## Next steps

For more information on Azure PowerShell, see [Azure PowerShell documentation](/en-us/powershell/azure).

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
<!-- Source: N/A -->

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-custom-remote-mcp-server -->

# Quickstart: Build a custom remote MCP server using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you create a custom remote Model Context Protocol (MCP) server from a template project using the Azure Developer CLI (`azd`

). The MCP server uses the Azure Functions MCP server extension to provide tools for AI models, agents, and assistants. After running the project locally and verifying your code using GitHub Copilot, you deploy it to a new serverless function app in Azure Functions that follows current best practices for secure and scalable deployments.

Tip

Functions also enables you to deploy an existing MCP server code project to a Flex Consumption plan app without having to make changes to your code project. For more information, see [Quickstart: Host existing MCP servers on Azure Functions](scenario-host-mcp-server-sdks).

Because the new app runs on the Flex Consumption plan, which follows a *pay-for-what-you-use* billing model, completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Important

While [creating custom MCP servers](functions-bindings-mcp) is supported for all Functions languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

## Prerequisites

[Java 17 Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure)- If you use another
[supported version of Java](supported-languages?pivots=programming-language-java#languages-by-runtime-version), you must update the project's pom.xml file. - Set the
`JAVA_HOME`

environment variable to the install location of the correct version of the Java Development Kit (JDK).

- If you use another
[Apache Maven 3.8.x](https://maven.apache.org)

[Visual Studio Code](https://code.visualstudio.com/)with these extensions:[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). This extension requires[Azure Functions Core Tools](functions-run-local)and attempts to install it when not available.

[Azure CLI](/en-us/cli/azure/install-azure-cli). You can also run Azure CLI commands in[Azure Cloud Shell](../cloud-shell/overview).An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template.

- In Visual Studio Code, open a folder or workspace where you want to create your project.

In the Terminal, run this

`azd init`

command:`azd init --template remote-mcp-functions-dotnet -e mcpserver-dotnet`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-dotnet)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command:`azd init --template remote-mcp-functions-java -e mcpserver-java`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-java)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command:`azd init --template remote-mcp-functions-typescript -e mcpserver-ts`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-typescript)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command:`azd init --template remote-mcp-functions-python -e mcpserver-python`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-python)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

## Start the storage emulator

Use the Azurite emulator to simulate an Azure Storage account connection when running your code project locally.

If you haven't already,

[install Azurite](/en-us/azure/storage/common/storage-use-azurite#install-azurite).Press

`F1`. In the command palette, search for and run the command`Azurite: Start`

to start the local storage emulator.

## Run your MCP server locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer by using the Azurite emulator.

To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel, and you can see the name of the functions that are running locally.Make a note of the local MCP server endpoint (like

`http://localhost:7071/runtime/webhooks/mcp`

), which you use to configure GitHub Copilot in Visual Studio Code.

## Verify using GitHub Copilot

To verify your code, add the running project as an MCP server for GitHub Copilot in Visual Studio Code:

Press

`F1`. In the command palette, search for and run**MCP: Add Server**.Choose

**HTTP (Server-Sent Events)**for the transport type.Enter the URL of the MCP endpoint you copied in the previous step.

Use the generated

**Server ID**and select**Workspace**to save the MCP server connection to your Workspace settings.Open the command palette and run

**MCP: List Servers**and verify that the server you added is listed and running.In Copilot chat, select

**Agent**mode and run this prompt:`Say Hello`

When prompted to run the tool, select

**Allow in this Workspace**so you don't have to keep granting permission. The prompt runs and returns a`Hello World`

response and function execution information is written to the logs.Now, select some code in one of your project files and run this prompt:

`Save this snippet as snippet1`

Copilot stores the snippet and responds to your request with information about how to retrieve the snippet by using the

`getSnippets`

tool. Again, you can review the function execution in the logs and verify that the`saveSnippets`

function ran.In Copilot chat, run this prompt:

`Retrieve snippet1 and apply to NewFile`

Copilot retrieves the snippets, adds it to a file called

`NewFile`

, and does whatever else it thinks is needed to make the code snippet work in your project. The Functions logs show that the`getSnippets`

endpoint was called.When you're done testing, press Ctrl+C to stop the Functions host.


## Review the code (optional)

You can review the code that defines the MCP server tools:

The function code for the MCP server tools is defined in the `src`

folder. The `McpToolTrigger`

attribute exposes the functions as MCP Server tools:

```
[Function(nameof(SayHello))]
public string SayHello(
[McpToolTrigger(HelloToolName, HelloToolDescription)] ToolInvocationContext context
)
{
logger.LogInformation("C# MCP tool trigger function processed a request.");
return "Hello I am MCP Tool!";
}
```


```
[Function(nameof(GetSnippet))]
public object GetSnippet(
[McpToolTrigger(GetSnippetToolName, GetSnippetToolDescription)]
ToolInvocationContext context,
[BlobInput(BlobPath)] string snippetContent
)
{
return snippetContent;
}
[Function(nameof(SaveSnippet))]
[BlobOutput(BlobPath)]
public string SaveSnippet(
[McpToolTrigger(SaveSnippetToolName, SaveSnippetToolDescription)]
ToolInvocationContext context,
[McpToolProperty(SnippetNamePropertyName, SnippetNamePropertyDescription, true)]
string name,
[McpToolProperty(SnippetPropertyName, SnippetPropertyDescription, true)]
string snippet
)
{
return snippet;
}
}
```


You can view the complete project template in the [Azure Functions .NET MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-dotnet) GitHub repository.

The function code for the MCP server tools is defined in the `src/main/java/com/function/`

folder. The `@McpToolTrigger`

annotation exposes the functions as MCP Server tools:

```
description = "The messages to be logged.",
isRequired = true,
isArray = true)
String messages,
final ExecutionContext functionExecutionContext
) {
functionExecutionContext.getLogger().info("Hello, World!");
functionExecutionContext.getLogger().info("Tool Name: " + mcpToolInvocationContext.getName());
functionExecutionContext.getLogger().info("Transport Type: " + mcpToolInvocationContext.getTransportType());
// Handle different transport types
if (mcpToolInvocationContext.isHttpStreamable()) {
functionExecutionContext.getLogger().info("Session ID: " + mcpToolInvocationContext.getSessionid());
} else if (mcpToolInvocationContext.isHttpSse()) {
if (mcpToolInvocationContext.getClientinfo() != null) {
functionExecutionContext.getLogger().info("Client: " +
mcpToolInvocationContext.getClientinfo().get("name").getAsString() + " v" +
```


```
// Write the snippet content to the output blob
outputBlob.setValue(snippet);
return "Successfully saved snippet '" + snippetName + "' with " + snippet.length() + " characters.";
}
/**
* Azure Function that handles retrieving a text snippet from Azure Blob Storage.
* <p>
* The function is triggered by an MCP Tool Trigger. The snippet name is provided
* as an MCP tool property, and the snippet content is read from the blob at the
* path derived from the snippet name.
*
* @param mcpToolInvocationContext The JSON input from the MCP tool trigger.
* @param snippetName The name of the snippet to retrieve, provided as an MCP tool property.
* @param inputBlob The Azure Blob input binding that fetches the snippet content.
* @param functionExecutionContext The execution context for logging.
*/
@FunctionName("GetSnippets")
@StorageAccount("AzureWebJobsStorage")
public String getSnippet(
@McpToolTrigger(
name = "getSnippets",
description = "Gets a text snippet from your snippets collection.")
String mcpToolInvocationContext,
@McpToolProperty(
name = SNIPPET_NAME_PROPERTY_NAME,
propertyType = "string",
description = "The name of the snippet.",
isRequired = true)
String snippetName,
@BlobInput(name = "inputBlob", path = BLOB_PATH)
String inputBlob,
final ExecutionContext functionExecutionContext
) {
// Log the entire incoming JSON for debugging
functionExecutionContext.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and the fetched snippet content from the blob
```


You can view the complete project template in the [Azure Functions Java MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-java) GitHub repository.

The function code for the MCP server tools is defined in the `src/function_app.py`

file. The MCP function annotations expose these functions as MCP Server tools:

```
tool_properties_save_snippets_json = json.dumps([prop.to_dict() for prop in tool_properties_save_snippets_object])
tool_properties_get_snippets_json = json.dumps([prop.to_dict() for prop in tool_properties_get_snippets_object])
@app.generic_trigger(
arg_name="context",
type="mcpToolTrigger",
toolName="hello_mcp",
description="Hello world.",
toolProperties="[]",
)
def hello_mcp(context) -> None:
"""
```


```
@app.generic_trigger(
arg_name="context",
type="mcpToolTrigger",
toolName="save_snippet",
description="Save a snippet with a name.",
toolProperties=tool_properties_save_snippets_json,
)
@app.generic_output_binding(arg_name="file", type="blob", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def save_snippet(file: func.Out[str], context) -> str:
content = json.loads(context)
snippet_name_from_args = content["arguments"][_SNIPPET_NAME_PROPERTY_NAME]
snippet_content_from_args = content["arguments"][_SNIPPET_PROPERTY_NAME]
if not snippet_name_from_args:
return "No snippet name provided"
if not snippet_content_from_args:
return "No snippet content provided"
file.set(snippet_content_from_args)
logging.info(f"Saved snippet: {snippet_content_from_args}")
return f"Snippet '{snippet_content_from_args}' saved successfully"
```


You can view the complete project template in the [Azure Functions Python MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-python) GitHub repository.

The function code for the MCP server tools is defined in the `src`

folder. The MCP function registration exposes these functions as MCP Server tools:

```
export async function mcpToolHello(_toolArguments:unknown, context: InvocationContext): Promise<string> {
console.log(_toolArguments);
// Get name from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
name?: string;
};
const name = mcptoolargs?.name;
console.info(`Hello ${name}, I am MCP Tool!`);
return `Hello ${name || 'World'}, I am MCP Tool!`;
}
// Register the hello tool
app.mcpTool('hello', {
toolName: 'hello',
description: 'Simple hello world MCP Tool that responses with a hello message.',
toolProperties:{
name: arg.string().describe('Required property to identify the caller.').optional()
},
handler: mcpToolHello
});
```


```
// SaveSnippet function - saves a snippet with a name
export async function saveSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Saving snippet");
// Get snippet name and content from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
snippet?: string;
};
const snippetName = mcptoolargs?.snippetname;
const snippet = mcptoolargs?.snippet;
if (!snippetName) {
return "No snippet name provided";
}
if (!snippet) {
return "No snippet content provided";
}
// Save the snippet to blob storage using the output binding
context.extraOutputs.set(blobOutputBinding, snippet);
console.info(`Saved snippet: ${snippetName}`);
return snippet;
}
```


You can view the complete project template in the [Azure Functions TypeScript MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-typescript) GitHub repository.

After verifying the MCP server tools locally, you can publish the project to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure. The project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Developer CLI (azd): Package, Provison and Deploy (up)`

. Then, sign in by using your Azure account.If you're not already signed in, authenticate with your Azure account.

When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. After the command completes successfully, you see links to the resources you created.


## Connect to your remote MCP server

Your MCP server is now running in Azure. When you access the tools, you need to include a system key in your request. This key provides a degree of access control for clients accessing your remote MCP server. After you get this key, you can connect GitHub Copilot to your remote server.

Run this script that uses

`azd`

and the Azure CLI to print out both the MCP server URL and the system key (`mcp_extension`

) required to access the tools:`eval $(azd env get-values --output dotenv) MCP_EXTENSION_KEY=$(az functionapp keys list --resource-group $AZURE_RESOURCE_GROUP \ --name $AZURE_FUNCTION_NAME --query "systemKeys.mcp_extension" -o tsv) printf "MCP Server URL: %s\n" "https://$SERVICE_API_NAME.azurewebsites.net/runtime/webhooks/mcp" printf "MCP Server key: %s\n" "$MCP_EXTENSION_KEY"`

In Visual Studio Code, press

`F1`to open the command palette, search for and run the command`MCP: Open Workspace Folder MCP Configuraton`

, which opens the`mcp.json`

configuration file.In the

`mcp.json`

configuration, find the named MCP server you added earlier, change the`url`

value to your remote MCP server URL, and add a`headers.x-functions-key`

element, which contains your copied MCP server access key, as in this example:`{ "servers": { "remote-mcp-function": { "type": "http", "url": "https://contoso.azurewebsites.net/runtime/webhooks/mcp", "headers": { "x-functions-key": "A1bC2dE3fH4iJ5kL6mN7oP8qR9sT0u..." } } } }`

Select the

**Start**button above your server name in the open`mcp.json`

to restart the remote MCP server, this time using your deployed app.

## Verify your deployment

You can now have GitHub Copilot use your remote MCP tools just as you did locally, but now the code runs securely in Azure. Replay the same commands you used earlier to ensure everything works correctly.

## Clean up resources

When you're done working with your MCP server and related resources, use this command to delete the function app and its related resources from Azure to avoid incurring further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without confirmation from you. This command doesn't affect your local code project.
