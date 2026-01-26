---
merged_at: 2026-01-26T23:29:57.710397
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-custom-handlers -->

# Azure Functions custom handlers

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions executes your app code by using language-specific handlers. These language-specific handlers allow Functions to support [most key languages](supported-languages) by default. However, you might need to run code in another language or package.

Custom handlers are lightweight web servers that receive events from the Azure Functions host process. You can use custom handlers to deploy to Azure Functions any code project that supports HTTP primitives.

Custom handlers are best suited for situations where you want to:

- Implement a function app in a language that's not currently offered out-of-the-box, such as Go or Rust.
- Implement a function app in a runtime that's not currently featured by default, such as Deno.
[Deploy a server](#deploy-self-hosted-mcp-servers)built with the standard MCP SDKs to Azure Functions.

With custom handlers, you can use [triggers and input and output bindings](functions-triggers-bindings) via [extension bundles](functions-bindings-register).

Get started with Azure Functions custom handlers with [quickstarts in Go and Rust](create-first-function-vs-code-other).

## Overview

The following diagram shows the relationship between the Functions host and a web server implemented as a custom handler.

- Each event triggers a request sent to the Functions host. An event is any trigger that Azure Functions supports.
- The Functions host then issues a
[request payload](#request-payload)to the web server. The payload holds trigger and input binding data and other metadata for the function. - The web server executes the individual function, and returns a
[response payload](#response-payload)to the Functions host. - The Functions host passes data from the response to the function's output bindings for processing.

An Azure Functions app implemented as a custom handler must configure the *host.json*, *local.settings.json*, and *function.json* files according to a few conventions.

## Deploy self-hosted MCP servers

Custom handlers also enables you to host MCP servers that you build by using official MCP SDKs in Azure Functions. Custom handlers provides a simple and streamlined experience for hosting your MCP servers in Azure. For more information, see [Self-hosted remote MCP server on Azure Functions](self-hosted-mcp-servers).

Note

The ability to have Azure Functions host MCP servers you create using official MCP SDKs is currently in preview.

## Application structure

To implement a custom handler, your application needs the following aspects:

- A
*host.json*file at the root of your app - A
*local.settings.json*file at the root of your app - A
*function.json*file for each function (inside a folder that matches the function name) - A command, script, or executable that runs a web server

The following diagram shows how these files look on the file system for a function named "MyQueueFunction" and a custom handler executable named *handler.exe*.

```
| /MyQueueFunction
| function.json
|
| host.json
| local.settings.json
| handler.exe
```


### Configuration

You configure the application through the *host.json* and *local.settings.json* files.

#### host.json

*host.json* directs the Functions host where to send requests by pointing to a web server that can process HTTP events.

Define a custom handler by configuring the *host.json* file with details on how to run the web server through the `customHandler`

section.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
}
}
```


The `customHandler`

section points to a target as defined by the `defaultExecutablePath`

. The execution target can be a command, executable, or file where the web server is implemented.

Use the `arguments`

array to pass any arguments to the executable. Arguments support expansion of environment variables (application settings) by using `%%`

notation.

You can also change the working directory used by the executable with `workingDirectory`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "app/handler.exe",
"arguments": [
"--database-connection-string",
"%DATABASE_CONNECTION_STRING%"
],
"workingDirectory": "app"
}
}
}
```


##### Bindings support

Standard triggers along with input and output bindings are available by referencing [extension bundles](functions-bindings-register) in your *host.json* file.

#### local.settings.json

*local.settings.json* defines application settings used when running the function app locally. Because it might contain secrets, exclude *local.settings.json* from source control. In Azure, use application settings instead.

For custom handlers, set `FUNCTIONS_WORKER_RUNTIME`

to `Custom`

in *local.settings.json*.

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "Custom"
}
}
```


### Function metadata

When you use a custom handler, the *function.json* contents are the same as when you define a function in any other context. The only requirement is that you must place *function.json* files in a folder named to match the function name.

The following *function.json* configures a function that has a queue trigger and a queue output binding. Because it's in a folder named *MyQueueFunction*, it defines a function named *MyQueueFunction*.

**MyQueueFunction/function.json**

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "messages-incoming",
"connection": "AzureWebJobsStorage"
},
{
"name": "$return",
"type": "queue",
"direction": "out",
"queueName": "messages-outgoing",
"connection": "AzureWebJobsStorage"
}
]
}
```


### Request payload

When the Functions host receives a queue message, it sends an HTTP post request to the custom handler with a payload in the body.

The following code shows a sample request payload. The payload includes a JSON structure with two members: `Data`

and `Metadata`

.

The `Data`

member includes keys that match input and trigger names as defined in the bindings array in the *function.json* file.

The `Metadata`

member includes [metadata generated from the event source](functions-bindings-expressions-patterns#trigger-metadata).

```
{
"Data": {
"myQueueItem": "{ message: \"Message sent\" }"
},
"Metadata": {
"DequeueCount": 1,
"ExpirationTime": "2019-10-16T17:58:31+00:00",
"Id": "800ae4b3-bdd2-4c08-badd-f08e5a34b865",
"InsertionTime": "2019-10-09T17:58:31+00:00",
"NextVisibleTime": "2019-10-09T18:08:32+00:00",
"PopReceipt": "AgAAAAMAAAAAAAAAAgtnj8x+1QE=",
"sys": {
"MethodName": "QueueTrigger",
"UtcNow": "2019-10-09T17:58:32.2205399Z",
"RandGuid": "24ad4c06-24ad-4e5b-8294-3da9714877e9"
}
}
}
```


### Response payload

By convention, function responses are formatted as key/value pairs. Supported keys include:

| Data type | Remarks | |
|---|---|---|
`Outputs` |
object | Holds response values as defined by the `bindings` array in function.json.For instance, if a function is configured with a queue output binding named "myQueueOutput", then `Outputs` contains a key named `myQueueOutput` , which the custom handler sets to the messages that it sends to the queue. |
`Logs` |
array | Messages that appear in the Functions invocation logs. When running in Azure, messages appear in Application Insights. |
`ReturnValue` |
string | Used to provide a response when an output is configured as `$return` in the function.json file. |

This table shows an example of a response payload.

```
{
"Outputs": {
"res": {
"body": "Message enqueued"
},
"myQueueOutput": [
"queue message 1",
"queue message 2"
]
},
"Logs": [
"Log message 1",
"Log message 2"
],
"ReturnValue": "{\"hello\":\"world\"}"
}
```


## Examples

You can implement custom handlers in any language that supports receiving HTTP events. The following examples show how to implement a custom handler by using the Go programming language.

### Function with bindings

This example shows a function named `order`

that accepts a `POST`

request with a payload representing a product order. When you post an order to the function, it creates a Queue Storage message and returns an HTTP response.

#### Implementation

In a folder named *order*, the *function.json* file configures the HTTP-triggered function.

**order/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": ["post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"type": "queue",
"name": "message",
"direction": "out",
"queueName": "orders",
"connection": "AzureWebJobsStorage"
}
]
}
```


This function is defined as an [HTTP triggered function](functions-bindings-http-webhook-trigger) that returns an [HTTP response](functions-bindings-http-webhook-output) and outputs a [Queue storage](functions-bindings-storage-queue-output) message.

At the root of the app, the *host.json* file is configured to run an executable file named `handler.exe`

(`handler`

in Linux or macOS).

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


This is the HTTP request sent to the Functions runtime.

```
POST http://127.0.0.1:7071/api/order HTTP/1.1
Content-Type: application/json
{
"id": 1005,
"quantity": 2,
"color": "black"
}
```


The Functions runtime sends the following HTTP request to the custom handler:

```
POST http://127.0.0.1:<FUNCTIONS_CUSTOMHANDLER_PORT>/order HTTP/1.1
Content-Type: application/json
{
"Data": {
"req": {
"Url": "http://localhost:7071/api/order",
"Method": "POST",
"Query": "{}",
"Headers": {
"Content-Type": [
"application/json"
]
},
"Params": {},
"Body": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}"
}
},
"Metadata": {
}
}
```


Note

Some portions of the payload were removed for brevity.

*handler.exe* is the compiled Go custom handler program that runs a web server and responds to function invocation requests from the Functions host.

```
package main
import (
"encoding/json"
"fmt"
"log"
"net/http"
"os"
)
type InvokeRequest struct {
Data map[string]json.RawMessage
Metadata map[string]interface{}
}
type InvokeResponse struct {
Outputs map[string]interface{}
Logs []string
ReturnValue interface{}
}
func orderHandler(w http.ResponseWriter, r *http.Request) {
var invokeRequest InvokeRequest
d := json.NewDecoder(r.Body)
d.Decode(&invokeRequest)
var reqData map[string]interface{}
json.Unmarshal(invokeRequest.Data["req"], &reqData)
outputs := make(map[string]interface{})
outputs["message"] = reqData["Body"]
resData := make(map[string]interface{})
resData["body"] = "Order enqueued"
outputs["res"] = resData
invokeResponse := InvokeResponse{outputs, nil, nil}
responseJson, _ := json.Marshal(invokeResponse)
w.Header().Set("Content-Type", "application/json")
w.Write(responseJson)
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/order", orderHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler runs a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

Even though the Functions host receives the original HTTP request at `/api/order`

, it invokes the custom handler by using the function name (its folder name). In this example, the function is defined at the path of `/order`

. The host sends the custom handler an HTTP request at the path of `/order`

.

When you send `POST`

requests to this function, the trigger data and function metadata are available via the HTTP request body. You can access the original HTTP request body in the payload's `Data.req.Body`

.

The function's response is formatted into key/value pairs where the `Outputs`

member holds a JSON value where the keys match the outputs as defined in the *function.json* file.

This is an example payload that this handler returns to the Functions host.

```
{
"Outputs": {
"message": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}",
"res": {
"body": "Order enqueued"
}
},
"Logs": null,
"ReturnValue": null
}
```


By setting the `message`

output equal to the order data that came in from the request, the function outputs that order data to the configured queue. The Functions host also returns the HTTP response configured in `res`

to the caller.

### HTTP-only function

For HTTP-triggered functions with no additional bindings or outputs, you might want your handler to work directly with the HTTP request and response instead of the custom handler [request](#request-payload) and [response](#response-payload) payloads. You can configure this behavior in *host.json* by using the `enableProxyingHttpRequest`

setting, which supports response streaming.

Important

The primary purpose of the custom handlers feature is to enable languages and runtimes that don't currently have first-class support on Azure Functions. While you might be able to run web applications by using custom handlers, Azure Functions isn't a standard reverse proxy. Some components of the HTTP request, such as certain headers and routes, might be restricted. Your application might also experience excessive [cold start](event-driven-scaling#cold-start).

To address these circumstances, consider running your web apps on [Azure App Service](../app-service/overview).

The following example demonstrates how to configure an HTTP-triggered function with no additional bindings or outputs. The scenario implemented in this example features a function named `hello`

that accepts a `GET`

or `POST`

.

#### Implementation

In a folder named *hello*, the *function.json* file configures the HTTP-triggered function.

**hello/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"authLevel": "function",
"direction": "in",
"name": "req",
"methods": ["get", "post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
}
]
}
```


The function is configured to accept both `GET`

and `POST`

requests, and the result value is provided through an argument named `res`

.

At the root of the app, the *host.json* file is configured to run `handler.exe`

and `enableProxyingHttpRequest`

is set to `true`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
},
"enableProxyingHttpRequest": true
}
}
```


The following is a POST request to the Functions host. The Functions host then sends the request to the custom handler.

```
POST http://127.0.0.1:7071/api/hello HTTP/1.1
Content-Type: application/json
{
"message": "Hello World!"
}
```


The *handler.go* file implements a web server and HTTP function.

```
package main
import (
"fmt"
"io/ioutil"
"log"
"net/http"
"os"
)
func helloHandler(w http.ResponseWriter, r *http.Request) {
w.Header().Set("Content-Type", "application/json")
if r.Method == "GET" {
w.Write([]byte("hello world"))
} else {
body, _ := ioutil.ReadAll(r.Body)
w.Write(body)
}
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/api/hello", helloHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler creates a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

`GET`

requests are handled by returning a string, and `POST`

requests have access to the request body.

The route for the order function here is `/api/hello`

, same as the original request.

Note

The `FUNCTIONS_CUSTOMHANDLER_PORT`

isn't the public facing port used to call the function. The Functions host uses this port to call the custom handler.

## Deploying

You can deploy a custom handler to every Azure Functions hosting option. If your handler requires operating system or platform dependencies (such as a language runtime), you might need to use a [custom container](functions-how-to-custom-container).

When you create a function app in Azure for custom handlers, select .NET Core as the stack.

To deploy a custom handler app by using Azure Functions Core Tools, run the following command.

```
func azure functionapp publish $functionAppName
```


Note

Ensure all files required to run your custom handler are in the folder and included in the deployment. If your custom handler is a binary executable or has platform-specific dependencies, ensure these files match the target deployment platform.

## Restrictions

- The custom handler web server needs to start within 60 seconds.

## Samples

For examples of how to implement functions in a variety of different languages, see the [custom handler samples GitHub repo](https://github.com/Azure-Samples/functions-custom-handlers).

## Troubleshooting and support

### Trace logging

If your custom handler process fails to start or if it has problems communicating with the Functions host, increase the function app's log level to `Trace`

to see more diagnostic messages from the host.

To change the function app's default log level, configure the `logLevel`

setting in the `logging`

section of *host.json*.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"logging": {
"logLevel": {
"default": "Trace"
}
}
}
```


The Functions host outputs extra log messages, including information related to the custom handler process. Use the logs to investigate problems starting your custom handler process or invoking functions in your custom handler.

Locally, logs are printed to the console.

In Azure, [query Application Insights traces](analyze-telemetry-data#query-telemetry-data) to view the log messages. If your app produces a high volume of logs, only a subset of log messages are sent to Application Insights. [Disable sampling](configure-monitoring#configure-sampling) to ensure all messages are logged.

### Test custom handler in isolation

Custom handler apps are web server processes, so it might be helpful to start them on their own and test function invocations by sending mock [HTTP requests](#request-payload). For sending HTTP requests with payloads, make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

You can also use this strategy in your CI/CD pipelines to run automated tests on your custom handler.

### Execution environment

Custom handlers run in the same environment as a typical Azure Functions app. Test your handler to ensure the environment contains all the dependencies it needs to run. For apps that require additional dependencies, you might need to run them by using a [custom container image](functions-how-to-custom-container) hosted on Azure Functions [Premium plan](functions-premium-plan).

### Get support

If you need help on a function app with custom handlers, you can submit a request through regular support channels. However, due to the wide variety of possible languages used to build custom handlers apps, support isn't unlimited.

Support is available if the Functions host has problems starting or communicating with the custom handler process. For problems specific to the inner workings of your custom handler process, such as issues with the chosen language or framework, our Support Team can't provide assistance in this context.

## Next steps

Get started building an Azure Functions app in Go or Rust with the [custom handlers quickstart](create-first-function-vs-code-other).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-trigger -->

# SignalR Service trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the *SignalR* trigger binding to respond to messages sent from Azure SignalR Service. When function is triggered, messages passed to the function is parsed as a json object.

In SignalR Service serverless mode, SignalR Service uses the [Upstream](../azure-signalr/concept-upstream) feature to send messages from client to Function App. And Function App uses SignalR Service trigger binding to handle these messages. The general architecture is shown below:


For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following sample shows a C# function that receives a message event from clients and logs the message content.

```
[Function(nameof(OnClientMessage))]
public static void OnClientMessage(
[SignalRTrigger("Hub", "messages", "sendMessage", "content", ConnectionStringSetting = "SignalRConnection")]
SignalRInvocationContext invocationContext, string content, FunctionContext functionContext)
{
var logger = functionContext.GetLogger(nameof(OnClientMessage));
logger.LogInformation("Connection {connectionId} sent a message. Message content: {content}", invocationContext.ConnectionId, content);
}
```


Important

Class based model of SignalR Service bindings in C# isolated worker doesn't optimize how you write SignalR triggers due to the limitation of C# worker model. For more information about class based model, see [Class based model](../azure-signalr/signalr-concept-serverless-development-config#class-based-model).

SignalR trigger isn't currently supported for Java.

Here's binding data in the *function.json* file:

```
{
"type": "signalRTrigger",
"name": "invocation",
"hubName": "hubName1",
"category": "messages",
"event": "SendMessage",
"parameterNames": [
"message"
],
"direction": "in"
}
```


```
app.generic("function1",
{
trigger: { "type": "signalRTrigger", "name": "invocation", "direction": "in", "hubName": "hubName1", "event": "SendMessage", "category": "messages" },
handler: (triggerInput, context) => {
context.log(`Receive ${triggerInput.Arguments[0]} from ${triggerInput.ConnectionId}.`)
}
})
```


Complete PowerShell examples are pending.

Here's the Python code:

```
import logging
import json
import azure.functions as func
def main(invocation) -> None:
invocation_json = json.loads(invocation)
logging.info("Receive {0} from {1}".format(invocation_json['Arguments'][0], invocation_json['ConnectionId']))
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `SignalRTrigger`

attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

The following table explains the properties of the `SignalRTrigger`

attribute.

| Attribute property | Description |
|---|---|
HubName |
This value must be set to the name of the SignalR hub for the function to be triggered. |
Category |
This value must be set as the category of messages for the function to be triggered. The category can be one of the following values:
|
Event |
This value must be set as the event of messages for the function to be triggered. For messages category, event is the target in
connections category, only connected and disconnected is used. |
ParameterNames |
(Optional) A list of names that binds to the parameters. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Annotations

There isn't currently a supported Java annotation for a SignalR trigger.

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `SignalRTrigger` . |
direction |
Must be set to `in` . |
name |
Variable name used in function code for trigger invocation context object. |
hubName |
This value must be set to the name of the SignalR hub for the function to be triggered. |
category |
This value must be set as the category of messages for the function to be triggered. The category can be one of the following values:
|
event |
This value must be set as the event of messages for the function to be triggered. For messages category, event is the target in
connections category, only connected and disconnected is used. |
parameterNames |
(Optional) A list of names that binds to the parameters. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

See the [Example section](#example) for complete examples.

## Usage

### Managed identity-based connections

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

### Payloads

The trigger input type is declared as either `InvocationContext`

or a custom type. If you choose `InvocationContext`

, you get full access to the request content. For a custom type, the runtime tries to parse the JSON request body to set the object properties.

### InvocationContext

`InvocationContext`

contains all the content in the message sent from a SignalR service, which includes the following properties:

| Property | Description |
|---|---|
| Arguments | Available for messages category. Contains arguments in
|
| Error | Available for disconnected event. It can be Empty if the connection closed with no error, or it contains the error messages. |
| Hub | The hub name that the message belongs to. |
| Category | The category of the message. |
| Event | The event of the message. |
| ConnectionId | The connection ID of the client that sends the message. |
| UserId | The user identity of the client that sends the message. |
| Headers | The headers of the request. |
| Query | The query of the request when clients connect to the service. |
| Claims | The claims of the client. |

### Using `ParameterNames`


The property `ParameterNames`

in `SignalRTrigger`

lets you bind arguments of invocation messages to the parameters of functions. You can use the name you defined as part of [binding expressions](functions-bindings-expressions-patterns) in other binding or as parameters in your code. That gives you a more convenient way to access arguments of `InvocationContext`

.

Say you have a JavaScript SignalR client trying to invoke method `broadcast`

in Azure Function with two arguments `message1`

, `message2`

.

```
await connection.invoke("broadcast", message1, message2);
```


After you set `parameterNames`

, the names you defined correspond to the arguments sent on the client side.

```
[SignalRTrigger(parameterNames: new string[] {"arg1, arg2"})]
```


Then, the `arg1`

contains the content of `message1`

, and `arg2`

contains the content of `message2`

.

`ParameterNames`

considerations

For the parameter binding, the order matters. If you're using `ParameterNames`

, the order in `ParameterNames`

matches the order of the arguments you invoke in the client. If you're using attribute `[SignalRParameter]`

in C#, the order of arguments in Azure Function methods matches the order of arguments in clients.

`ParameterNames`

and attribute `[SignalRParameter]`

**cannot** be used at the same time, or you'll get an exception.

### SignalR Service integration

SignalR Service needs a URL to access Function App when you're using SignalR Service trigger binding. The URL should be configured in **Upstream Settings** on the SignalR Service side.


When using SignalR Service trigger, the URL can be simple and formatted as follows:

```
<Function_App_URL>/runtime/webhooks/signalr?code=<API_KEY>
```


The `Function_App_URL`

can be found on Function App's Overview page and the `API_KEY`

is generated by Azure Function. You can get the `API_KEY`

from `signalr_extension`

in the **App keys** blade of Function App.

If you want to use more than one Function App together with one SignalR Service, upstream can also support complex routing rules. Find more details at [Upstream settings](../azure-signalr/concept-upstream).

### Step-by-step sample

You can follow the sample in GitHub to deploy a chat room on Function App with SignalR Service trigger binding and upstream feature: [Bidirectional chat room sample](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/BidirectionChat)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-output -->

# Azure Cache for Redis output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cache for Redis output bindings lets you change the keys in a cache based on a set of available trigger on the cache.

For information on setup and configuration details, see the [overview](functions-bindings-cache).

## Scope of availability for functions bindings

| Binding Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Output | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[Function(nameof(SetDeleter))]
[RedisOutput(Common.connectionString, "DEL")]
public static string Run(
[RedisPubSubTrigger(Common.connectionString, "__keyevent@0__:set")] string key,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
return key;
}
}
}
```


```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.WebJobs.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[FunctionName(nameof(SetDeleter))]
public static void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyevent@0__:set")] string key,
[Redis(Common.connectionStringSetting, "DEL")] out string[] arguments,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
arguments = new string[] { key };
}
}
}
```


The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

```
package com.function.RedisOutputBinding;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SetDeleter {
@FunctionName("SetDeleter")
@RedisOutput(
name = "value",
connection = "redisConnectionString",
command = "DEL")
public String run(
@RedisPubSubTrigger(
name = "key",
connection = "redisConnectionString",
channel = "__keyevent@0__:set")
String key,
final ExecutionContext context) {
context.getLogger().info("Deleting recently SET key '" + key + "'");
return key;
}
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in the `function.json`` file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisConnectionString",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "index.js"
}
```


This code from the `index.js`

file takes the key from the trigger and returns it to the output binding to delete the cached item.

```
module.exports = async function (context, key) {
context.log("Deleting recently SET key '" + key + "'");
return key;
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "retVal",
"direction": "out"
}
],
"scriptFile": "run.ps1"
}
```


This code from the `run.ps1`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
param($key, $TriggerMetadata)
Write-Host "Deleting recently SET key '$key'"
Push-OutputBinding -Name retVal -Value $key
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "__init__.py"
}
```


This code from the `__init__.py`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
import logging
def main(key: str) -> str:
logging.info("Deleting recently SET key '" + key + "'")
return key
```


## Attributes

Note

All commands are supported for this binding.

The way in which you define an output binding parameter depends on whether your C# functions runs [in-process](functions-dotnet-class-library) or in an [isolated worker process](dotnet-isolated-process-guide).

The output binding is defined this way:

| Definition | Example | Description |
|---|---|---|
On an `out` parameter |
`[Redis(<Connection>, <Command>)] out string <Return_Variable>` |
The string variable returned by the method is a key value that the binding uses to execute the command against the specific cache. |

In this case, the type returned by the method is a key value that the binding uses to execute the command against the specific cache.

When your function has multiple output bindings, you can instead apply the binding attribute to the property of a type that is a key value, which the binding uses to execute the command against the specific cache. For more information, see [Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).

Regardless of the C# process mode, the same properties are supported by the output binding attribute:

| Attribute property | Description |
|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Command`

`DEL`

.## Annotations

The `RedisOutput`

annotation supports these properties:

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.See the [Example section](#example) for complete examples.

## Usage

The output returns a string, which is the key of the cache entry on which apply the specific command.

There are three types of connections that are allowed from an Azure Functions instance to a Redis Cache in your deployments. For local development, you can also use service principal secrets. Use the `appsettings`

to configure each of the following types of client authentication, assuming the `Connection`

was set to `Redis`

in the function.

Important

For optimal security, your function app should use Microsoft Entra ID with managed identities to authorize requests against your cache, if possible. Authorization by using Microsoft Entra ID and managed identities provides superior security and ease of use over shared access key authorization. For more information about using managed identities with your cache, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-vnet -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table-output -->

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
