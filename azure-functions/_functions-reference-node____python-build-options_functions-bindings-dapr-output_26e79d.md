---
merged_at: 2026-01-26T23:29:57.727688
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-node -->

# Azure Functions Node.js developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This guide is an introduction to developing Azure Functions using JavaScript or TypeScript. The article assumes that you have already read the [Azure Functions developer guide](functions-reference).

Important

The content of this article changes based on your choice of the Node.js programming model in the selector at the top of this page. The version you choose should match the version of the [ @azure/functions](https://www.npmjs.com/package/@azure/functions) npm package you're using in your app. If you don't have that package listed in your

`package.json`

, the default is v3. Learn more about the differences between v3 and v4 in the [migration guide](functions-node-upgrade-v4).

As a Node.js developer, you might also be interested in one of the following articles:

| Getting started | Concepts | Guided learning |
|---|---|---|

## Considerations

- The Node.js programming model shouldn't be confused with the Azure Functions runtime:
**Programming model**: Defines how you author your code and is specific to JavaScript and TypeScript.**Runtime**: Defines underlying behavior of Azure Functions and is shared across all languages.

- The version of the programming model is strictly tied to the version of the
npm package. It's versioned independently of the`@azure/functions`

[runtime](functions-versions). Both the runtime and the programming model use the number 4 as their latest major version, but that's a coincidence. - You can't mix the v3 and v4 programming models in the same function app. As soon as you register one v4 function in your app, any v3 functions registered in
*function.json*files are ignored.

## Supported versions

The following table shows each version of the Node.js programming model along with its supported versions of the Azure Functions runtime and Node.js.

|
|---|

[Functions Runtime Version](functions-versions)

[Node.js Version](https://github.com/nodejs/release#release-schedule)

[Functions Versions](functions-versions)for more info.[Functions Versions](functions-versions)for more info.## Folder structure

The required folder structure for a JavaScript project looks like the following example:

```
<project_root>/
| - .vscode/
| - node_modules/
| - myFirstFunction/
| | - index.js
| | - function.json
| - mySecondFunction/
| | - index.js
| | - function.json
| - .funcignore
| - host.json
| - local.settings.json
| - package.json
```


The main project folder, *<project_root>*, can contain the following files:

**.vscode/**: (Optional) Contains the stored Visual Studio Code configuration. To learn more, see[Visual Studio Code settings](https://code.visualstudio.com/docs/getstarted/settings).**myFirstFunction/function.json**: Contains configuration for the function's trigger, inputs, and outputs. The name of the directory determines the name of your function.**myFirstFunction/index.js**: Stores your function code. To change this default file path, see[using scriptFile](#using-scriptfile).**.funcignore**: (Optional) Declares files that shouldn't get published to Azure. Usually, this file contains*.vscode/*to ignore your editor setting,*test/*to ignore test cases, and*local.settings.json*to prevent local app settings being published.**host.json**: Contains configuration options that affect all functions in a function app instance. This file does get published to Azure. Not all options are supported when running locally. To learn more, see[host.json](functions-host-json).**local.settings.json**: Used to store app settings and connection strings when it's running locally. This file doesn't get published to Azure. To learn more, see[local.settings.file](functions-develop-local#local-settings-file).**package.json**: Contains configuration options like a list of package dependencies, the main entrypoint, and scripts.

The recommended folder structure for a JavaScript project looks like the following example:

```
<project_root>/
| - .vscode/
| - node_modules/
| - src/
| | - functions/
| | | - myFirstFunction.js
| | | - mySecondFunction.js
| - test/
| | - functions/
| | | - myFirstFunction.test.js
| | | - mySecondFunction.test.js
| - .funcignore
| - host.json
| - local.settings.json
| - package.json
```


The main project folder, *<project_root>*, can contain the following files:

**.vscode/**: (Optional) Contains the stored Visual Studio Code configuration. To learn more, see[Visual Studio Code settings](https://code.visualstudio.com/docs/getstarted/settings).**src/functions/**: The default location for all functions and their related triggers and bindings.**test/**: (Optional) Contains the test cases of your function app.**.funcignore**: (Optional) Declares files that shouldn't get published to Azure. Usually, this file contains*.vscode/*to ignore your editor setting,*test/*to ignore test cases, and*local.settings.json*to prevent local app settings being published.**host.json**: Contains configuration options that affect all functions in a function app instance. This file does get published to Azure. Not all options are supported when running locally. To learn more, see[host.json](functions-host-json).**local.settings.json**: Used to store app settings and connection strings when it's running locally. This file doesn't get published to Azure. To learn more, see[local.settings.file](functions-develop-local#local-settings-file).**package.json**: Contains configuration options like a list of package dependencies, the main entrypoint, and scripts.

## Registering a function

The v3 model registers a function based on the existence of two files. First, you need a `function.json`

file located in a folder one level down from the root of your app. Second, you need a JavaScript file that [exports](https://nodejs.org/api/modules.html#modules_module_exports) your function. By default, the model looks for an `index.js`

file in the same folder as your `function.json`

. If you're using TypeScript, you must use the [ scriptFile](#using-scriptfile) property in

`function.json`

to point to the compiled JavaScript file. To customize the file location or export name of your function, see [configuring your function's entry point](functions-reference-node#configure-function-entry-point).

The function you export should always be declared as an [ async function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) in the v3 model. You can export a synchronous function, but then you must call

[to signal that your function is completed, which is deprecated and not recommended.](#contextdone)

`context.done()`

Your function is passed an [invocation context](#invocation-context) as the first argument and your

[inputs](#inputs)as the remaining arguments.

The following example is a simple function that logs that it was triggered and responds with `Hello, world!`

:

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"authLevel": "anonymous",
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


```
module.exports = async function (context, request) {
context.log("Http function was triggered.");
context.res = { body: "Hello, world!" };
};
```


The programming model loads your functions based on the `main`

field in your `package.json`

. You can set the `main`

field to a single file or multiple files by using a [glob pattern](https://wikipedia.org/wiki/Glob_(programming)). The following table shows example values for the `main`

field:

| Example | Description |
|---|---|
`src/index.js` |
Register functions from a single root file. |
`src/functions/*.js` |
Register each function from its own file. |
`src/{index.js,functions/*.js}` |
A combination where you register each function from its own file, but you still have a root file for general app-level code. |

In order to register a function, you must import the `app`

object from the `@azure/functions`

npm module and call the method specific to your trigger type. The first argument when registering a function is the function name. The second argument is an `options`

object specifying configuration for your trigger, your handler, and any other inputs or outputs. In some cases where trigger configuration isn't necessary, you can pass the handler directly as the second argument instead of an `options`

object.

Registering a function can be done from any file in your project, as long as that file is loaded (directly or indirectly) based on the `main`

field in your `package.json`

file. The function should be registered at a global scope because you can't register functions once executions start.

The following example is a simple function that logs that it was triggered and responds with `Hello, world!`

:

```
const { app } = require("@azure/functions");
app.http("helloWorld1", {
methods: ["POST", "GET"],
handler: async (request, context) => {
context.log("Http function was triggered.");
return { body: "Hello, world!" };
},
});
```


## Inputs and outputs

Your function is required to have exactly one primary input called the trigger. It might also have secondary inputs and/or outputs. Inputs and outputs are configured in your `function.json`

files and are also referred to as [bindings](functions-triggers-bindings).

### Inputs

Inputs are bindings with `direction`

set to `in`

. The main difference between a trigger and a secondary input is that the `type`

for a trigger ends in `Trigger`

, for example type [ blobTrigger](functions-bindings-storage-blob-trigger) vs type

[. Most functions only use a trigger, and not many secondary input types are supported.](functions-bindings-storage-blob-input)

`blob`

Inputs can be accessed in several ways:

Use the arguments in the same order that they're defined in*[Recommended]*As arguments passed to your function:`function.json`

. The`name`

property defined in`function.json`

doesn't need to match the name of your argument, although we recommend it for the sake of organization.`module.exports = async function (context, myTrigger, myInput, myOtherInput) { ... };`


**As properties of**Use the key matching the:`context.bindings`

`name`

property defined in`function.json`

.`module.exports = async function (context) { context.log("This is myTrigger: " + context.bindings.myTrigger); context.log("This is myInput: " + context.bindings.myInput); context.log("This is myOtherInput: " + context.bindings.myOtherInput); };`


### Outputs

Outputs are bindings with `direction`

set to `out`

and can be set in several ways:

If you're using an async function, you can return the value directly. You must change the*[Recommended for single output]*Return the value directly:`name`

property of the output binding to`$return`

in`function.json`

like in the following example:`{ "name": "$return", "type": "http", "direction": "out" }`

`module.exports = async function (context, request) { return { body: "Hello, world!", }; };`


If you're using an async function, you can return an object with a property matching the name of each binding in your*[Recommended for multiple outputs]*Return an object containing all outputs:`function.json`

. The following example uses output bindings named "httpResponse" and "queueOutput":`{ "name": "httpResponse", "type": "http", "direction": "out" }, { "name": "queueOutput", "type": "queue", "direction": "out", "queueName": "helloworldqueue", "connection": "storage_APPSETTING" }`

`module.exports = async function (context, request) { let message = "Hello, world!"; return { httpResponse: { body: message, }, queueOutput: message, }; };`


**Set values on**If you're not using an async function or you don't want to use the previous options, you can set values directly on`context.bindings`

:`context.bindings`

, where the key matches the name of the binding. The following example uses output bindings named "httpResponse" and "queueOutput":`{ "name": "httpResponse", "type": "http", "direction": "out" }, { "name": "queueOutput", "type": "queue", "direction": "out", "queueName": "helloworldqueue", "connection": "storage_APPSETTING" }`

`module.exports = async function (context, request) { let message = "Hello, world!"; context.bindings.httpResponse = { body: message, }; context.bindings.queueOutput = message; };`


### Bindings data type

You can use the `dataType`

property on an input binding to change the type of your input. However, the approach has some limitations:

- In Node.js, only
`string`

and`binary`

are supported (`stream`

isn't) - For HTTP inputs, the
`dataType`

property is ignored. Instead, use properties on the`request`

object to get the body in your desired format. For more information, see[HTTP request](#http-request).

In the following example of a [storage queue trigger](functions-bindings-storage-queue-trigger), the default type of `myQueueItem`

is a `string`

, but if you set `dataType`

to `binary`

, the type changes to a Node.js `Buffer`

.

```
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "helloworldqueue",
"connection": "storage_APPSETTING",
"dataType": "binary"
}
```


```
const { Buffer } = require("node:buffer");
module.exports = async function (context, myQueueItem) {
if (typeof myQueueItem === "string") {
context.log("myQueueItem is a string");
} else if (Buffer.isBuffer(myQueueItem)) {
context.log("myQueueItem is a buffer");
}
};
```


Your function is required to have exactly one primary input called the trigger. It might also have secondary inputs, a primary output called the return output, and/or secondary outputs. Inputs and outputs are also referred to as [bindings](functions-triggers-bindings) outside the context of the Node.js programming model. Before v4 of the model, these bindings were configured in `function.json`

files.

### Trigger input

The trigger is the only required input or output. For most trigger types, you register a function by using a method on the `app`

object named after the trigger type. You can specify configuration specific to the trigger directly on the `options`

argument. For example, an HTTP trigger allows you to specify a route. During execution, the value corresponding to this trigger is passed in as the first argument to your handler.

```
const { app } = require('@azure/functions');
app.http('helloWorld1', {
route: 'hello/world',
handler: async (request, context) => {
...
}
});
```


### Return output

The return output is optional, and in some cases configured by default. For example, an HTTP trigger registered with `app.http`

is configured to return an HTTP response output automatically. For most output types, you specify the return configuration on the `options`

argument with the help of the `output`

object exported from the `@azure/functions`

module. During execution, you set this output by returning it from your handler.

The following example uses a [timer trigger](functions-bindings-timer) and a [storage queue output](functions-bindings-storage-queue-output):

```
const { app, output } = require('@azure/functions');
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.storageQueue({
connection: 'storage_APPSETTING',
...
}),
handler: (myTimer, context) => {
return { hello: 'world' }
}
});
```


### Extra inputs and outputs

In addition to the trigger and return, you might specify extra inputs or outputs on the `options`

argument when registering a function. The `input`

and `output`

objects exported from the `@azure/functions`

module provide type-specific methods to help construct the configuration. During execution, you get or set the values with `context.extraInputs.get`

or `context.extraOutputs.set`

, passing in the original configuration object as the first argument.

The following example is a function triggered by a [storage queue](functions-bindings-storage-queue-trigger), with an extra [storage blob input](functions-bindings-storage-blob-input) that is copied to an extra [storage blob output](functions-bindings-storage-blob-output). The queue message should be the name of a file and replaces `{queueTrigger}`

as the blob name to be copied, with the help of a [binding expression](functions-bindings-expressions-patterns).

```
const { app, input, output } = require("@azure/functions");
const blobInput = input.storageBlob({
connection: "storage_APPSETTING",
path: "helloworld/{queueTrigger}",
});
const blobOutput = output.storageBlob({
connection: "storage_APPSETTING",
path: "helloworld/{queueTrigger}-copy",
});
app.storageQueue("copyBlob1", {
queueName: "copyblobqueue",
connection: "storage_APPSETTING",
extraInputs: [blobInput],
extraOutputs: [blobOutput],
handler: (queueItem, context) => {
const blobInputValue = context.extraInputs.get(blobInput);
context.extraOutputs.set(blobOutput, blobInputValue);
},
});
```


### Generic inputs and outputs

The `app`

, `trigger`

, `input`

, and `output`

objects exported by the `@azure/functions`

module provide type-specific methods for most types. For all the types that aren't supported, a `generic`

method is provided to allow you to manually specify the configuration. The `generic`

method can also be used if you want to change the default settings provided by a type-specific method.

The following example is a simple HTTP triggered function using generic methods instead of type-specific methods.

```
const { app, output, trigger } = require("@azure/functions");
app.generic("helloWorld1", {
trigger: trigger.generic({
type: "httpTrigger",
methods: ["GET", "POST"],
}),
return: output.generic({
type: "http",
}),
handler: async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
return { body: `Hello, world!` };
},
});
```


## SDK types

Several binding extensions now enable you to work directly with the Azure SDK types.

### Azure Blob storage

SDK bindings capability in Azure Functions enables you to work directly with the Azure Blob storage SDK types like `BlobClient`

and `ContainerClient`

instead of raw data. This provides full access to all SDK methods when working with blobs.

To configure your project to work with SDK types:

- Add the
`@azure/functions-extensions-blob`

extension preview packages to the`package.json`

file in the project, which should include at least these packages:

```
"dependencies": {
"@azure/functions": "4.7.2-preview",
"@azure/functions-extensions-blob": "0.2.0-preview"
},
```


- Add
`enableHttpStream: true`

in your`app.setup`

to support streaming types:

```
import { app } from '@azure/functions';
app.setup({
enableHttpStream: true,
});
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


Keep these considerations in mind when working with SDK types:

- Always have
`import "@azure/functions-extensions-blob"`

first in your files to ensure side effects run. - Set
`sdkBinding: true`

in your binding configuration. - Use the appropriate client type for your operation:
`blobClient`

for operations on a single blob`containerClient`

for operations on a container

- Handle errors appropriately with
`try`

/`catch`

blocks - For large blob operations, consider using streaming methods to avoid memory issues.

For more information, see these [Blob Storage SDK Bindings for Node.js Samples](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-nodejs):
for more examples on how to incorporate SDK Bindings for Blob into your function app.

### Azure Service Bus

This example uses the SDK type [ ServiceBusReceivedMessage](/en-us/javascript/api/@azure/service-bus/servicebusreceivedmessage) obtained from

`ServiceBusMessageContext`

provided by the Service Bus trigger:```
import '@azure/functions-extensions-servicebus'; // Ensure the Service Bus extension is imported
import { app, InvocationContext } from '@azure/functions';
import { ServiceBusMessageContext } from '@azure/functions-extensions-servicebus';
//This a SDKbinding = true
export async function serviceBusQueueTrigger(
serviceBusMessageContext: ServiceBusMessageContext,
context: InvocationContext
): Promise<void> {
const message = serviceBusMessageContext.messages[0];
context.log(message);
// Get current retry count from custom properties, default to 0
const currentRetryCount = message.applicationProperties?.retryCnt ? parseInt(message.applicationProperties.retryCnt as string) : 0;
context.log(`Current retry count: ${currentRetryCount}`);
if (currentRetryCount >= 3) {
// After 3 retries, complete the message to remove it from the queue
context.log(`Maximum retry count (3) reached. Completing message to prevent infinite loop.`);
await serviceBusMessageContext.actions.complete(message);
context.log('Message completed after maximum retries');
} else {
// Abandon with updated retry count
const newRetryCount = currentRetryCount + 1;
const propertiesToModify = {
retryCnt: newRetryCount.toString(),
lastRetryTime: new Date().toISOString(),
errorMessage: "Processing failed"
};
context.log(`Abandoning message with retry count: ${newRetryCount}`);
await serviceBusMessageContext.actions.abandon(message, propertiesToModify);
}
context.log('triggerMetadata: ', context.triggerMetadata);
context.log('Message body:', message.body);
}
app.serviceBusQueue('serviceBusQueueTrigger1', {
connection: 'ServiceBusConnection',
queueName: 'testqueue',
sdkBinding: true,
autoCompleteMessages: false,
cardinality: 'many',
handler: serviceBusQueueTrigger,
});
```


For another example using SDK types see the [exponential backoff strategy sample](https://github.com/Azure/azure-functions-nodejs-extensions/blob/main/azure-functions-nodejs-extensions-servicebus/samples/serviceBusTriggerExponentialBackOff/src/functions/serviceBusTopicTrigger.ts).

## Invocation context

Each invocation of your function is passed an invocation `context`

object, used to read inputs, set outputs, write to logs, and read various metadata. In the v3 model, the context object is always the first argument passed to your handler.

The `context`

object has the following properties:

| Property | Description |
|---|---|
`invocationId` |
The ID of the current function invocation. |
`executionContext` |
See
|

`bindings`

[bindings](#contextbindings).`bindingData`

[event hub trigger](functions-bindings-event-hubs-trigger)has an`enqueuedTimeUtc`

property.`traceContext`

[.](https://www.w3.org/TR/trace-context/)`Trace Context`

`bindingDefinitions`

`function.json`

.`req`

[HTTP request](#http-request).`res`

[HTTP response](#http-response).### context.executionContext

The `context.executionContext`

object has the following properties:

| Property | Description |
|---|---|
`invocationId` |
The ID of the current function invocation. |
`functionName` |
The name of the function that is being invoked. The name of the folder containing the `function.json` file determines the name of the function. |
`functionDirectory` |
The folder containing the `function.json` file. |
`retryContext` |
See
|

#### context.executionContext.retryContext

The `context.executionContext.retryContext`

object has the following properties:

| Property | Description |
|---|---|
`retryCount` |
A number representing the current retry attempt. |
`maxRetryCount` |
Maximum number of times an execution is retried. A value of `-1` means to retry indefinitely. |
`exception` |
Exception that caused the retry. |

### context.bindings

The `context.bindings`

object is used to read inputs or set outputs. The following example is a [storage queue trigger](functions-bindings-storage-queue-trigger), which uses `context.bindings`

to copy a [storage blob input](functions-bindings-storage-blob-input) to a [storage blob output](functions-bindings-storage-blob-output). The queue message's content replaces `{queueTrigger}`

as the file name to be copied, with the help of a [binding expression](functions-bindings-expressions-patterns).

```
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"connection": "storage_APPSETTING",
"queueName": "helloworldqueue"
},
{
"name": "myInput",
"type": "blob",
"direction": "in",
"connection": "storage_APPSETTING",
"path": "helloworld/{queueTrigger}"
},
{
"name": "myOutput",
"type": "blob",
"direction": "out",
"connection": "storage_APPSETTING",
"path": "helloworld/{queueTrigger}-copy"
}
```


```
module.exports = async function (context, myQueueItem) {
const blobValue = context.bindings.myInput;
context.bindings.myOutput = blobValue;
};
```


### context.done

The `context.done`

method is deprecated. Before async functions were supported, you would signal your function is done by calling `context.done()`

:

```
module.exports = function (context, request) {
context.log("this pattern is now deprecated");
context.done();
};
```


We recommend that you remove the call to `context.done()`

and mark your function as async so that it returns a promise (even if you don't `await`

anything). As soon as your function finishes (in other words, the returned promise resolves), the v3 model knows your function is done.

```
module.exports = async function (context, request) {
context.log("you don't need context.done or an awaited call");
};
```


Each invocation of your function is passed an invocation `context`

object, with information about your invocation and methods used for logging. In the v4 model, the `context`

object is typically the second argument passed to your handler.

The `InvocationContext`

class has the following properties:

| Property | Description |
|---|---|
`invocationId` |
The ID of the current function invocation. |
`functionName` |
The name of the function. |
`extraInputs` |
Used to get the values of extra inputs. For more information, see
|

`extraOutputs`

[extra inputs and outputs](#extra-inputs-and-outputs).`retryContext`

[retry context](#retry-context).`traceContext`

[.](https://www.w3.org/TR/trace-context/)`Trace Context`

`triggerMetadata`

[event hub trigger](functions-bindings-event-hubs-trigger)has an`enqueuedTimeUtc`

property.`options`

### Retry context

The `retryContext`

object has the following properties:

| Property | Description |
|---|---|
`retryCount` |
A number representing the current retry attempt. |
`maxRetryCount` |
Maximum number of times an execution is retried. A value of `-1` means to retry indefinitely. |
`exception` |
Exception that caused the retry. |

For more information, see [ retry-policies](functions-bindings-errors#retry-policies).

## Logging

In Azure Functions, it's recommended to use `context.log()`

to write logs. Azure Functions integrates with Azure Application Insights to better capture your function app logs. Application Insights, part of Azure Monitor, provides facilities for collection, visual rendering, and analysis of both application logs and your trace outputs. To learn more, see [monitoring Azure Functions](functions-monitoring).

Note

If you use the alternative Node.js `console.log`

method, those logs are tracked at the app-level and will *not* be associated with any specific function. We *highly recommend* that your use `context`

for logging instead of `console`

so that all logs are associated with a specific function.

The following example writes a log at the default "information" level, including the invocation ID:

```
context.log(`Something has happened. Invocation ID: "${context.invocationId}"`);
```


### Log levels

In addition to the default `context.log`

method, the following methods are available that let you write logs at specific levels:

| Method | Description |
|---|---|
`context.log.error()` |
Writes an error-level event to the logs. |
`context.log.warn()` |
Writes a warning-level event to the logs. |
`context.log.info()` |
Writes an information-level event to the logs. |
`context.log.verbose()` |
Writes a trace-level event to the logs. |

| Method | Description |
|---|---|
`context.trace()` |
Writes a trace-level event to the logs. |
`context.debug()` |
Writes a debug-level event to the logs. |
`context.info()` |
Writes an information-level event to the logs. |
`context.warn()` |
Writes a warning-level event to the logs. |
`context.error()` |
Writes an error-level event to the logs. |

### Configure log level

Azure Functions lets you define the threshold level to be used when tracking and viewing logs. To set the threshold, use the `logging.logLevel`

property in the `host.json`

file. This property lets you define a default level applied to all functions, or a threshold for each individual function. To learn more, see [How to configure monitoring for Azure Functions](configure-monitoring).

## Track custom data

By default, Azure Functions writes output as traces to Application Insights. For more control, you can instead use the [Application Insights Node.js SDK](https://github.com/microsoft/applicationinsights-node.js) to send custom data to your Application Insights instance.

```
const appInsights = require("applicationinsights");
appInsights.setup();
const client = appInsights.defaultClient;
module.exports = async function (context, request) {
// Use this with 'tagOverrides' to correlate custom logs to the parent function invocation.
var operationIdOverride = {
"ai.operation.id": context.traceContext.traceparent,
};
client.trackEvent({
name: "my custom event",
tagOverrides: operationIdOverride,
properties: { customProperty2: "custom property value" },
});
client.trackException({
exception: new Error("handled exceptions can be logged with this method"),
tagOverrides: operationIdOverride,
});
client.trackMetric({
name: "custom metric",
value: 3,
tagOverrides: operationIdOverride,
});
client.trackTrace({
message: "trace message",
tagOverrides: operationIdOverride,
});
client.trackDependency({
target: "http://dbname",
name: "select customers proc",
data: "SELECT * FROM Customers",
duration: 231,
resultCode: 0,
success: true,
dependencyTypeName: "ZSQL",
tagOverrides: operationIdOverride,
});
client.trackRequest({
name: "GET /customers",
url: "http://myserver/customers",
duration: 309,
resultCode: 200,
success: true,
tagOverrides: operationIdOverride,
});
};
```


The `tagOverrides`

parameter sets the `operation_Id`

to the function's invocation ID. This setting enables you to correlate all of the automatically generated and custom logs for a given function invocation.

## HTTP triggers

HTTP and webhook triggers use request and response objects to represent HTTP messages.

HTTP and webhook triggers use `HttpRequest`

and `HttpResponse`

objects to represent HTTP messages. The classes represent a subset of the [fetch standard](https://developer.mozilla.org/docs/Web/API/fetch), using Node.js's [ undici](https://undici.nodejs.org/) package.

### HTTP Request

The request can be accessed in several ways:

**As the second argument to your function:**`module.exports = async function (context, request) { context.log(`Http function processed request for url "${request.url}"`);`


**From the**`context.req`

property:`module.exports = async function (context, request) { context.log(`Http function processed request for url "${context.req.url}"`);`


**From the named input bindings:**This option works the same as any non HTTP binding. The binding name in`function.json`

must match the key on`context.bindings`

, or "request1" in the following example:`{ "name": "request1", "type": "httpTrigger", "direction": "in", "authLevel": "anonymous", "methods": ["get", "post"] }`

`module.exports = async function (context, request) { context.log(`Http function processed request for url "${context.bindings.request1.url}"`);`


The `HttpRequest`

object has the following properties:

| Property | Type | Description |
|---|---|---|
`method` |
`string` |
HTTP request method used to invoke this function. |
`url` |
`string` |
Request URL. |
`headers` |
`Record<string, string>` |
HTTP request headers. This object is case sensitive. It's recommended to use `request.getHeader('header-name')` instead, which is case insensitive. |
`query` |
`Record<string, string>` |
Query string parameter keys and values from the URL. |
`params` |
`Record<string, string>` |
Route parameter keys and values. |
`user` |
`HttpRequestUser \| null` |
Object representing logged-in user, either through Functions authentication, SWA Authentication, or null when no such user is logged in. |
`body` |
`Buffer \| string \| any` |
If the media type is "application/octet-stream" or "multipart/*", `body` is a Buffer. If the value is a JSON parse-able string, `body` is the parsed object. Otherwise, `body` is a string. |
`rawBody` |
`string` |
The body as a string. Despite the name, this property doesn't return a Buffer. |
`bufferBody` |
`Buffer` |
The body as a buffer. |

The request can be accessed as the first argument to your handler for an HTTP triggered function.

```
async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
```


The `HttpRequest`

object has the following properties:

| Property | Type | Description |
|---|---|---|
`method` |
`string` |
HTTP request method used to invoke this function. |
`url` |
`string` |
Request URL. |
`headers` |
`Headers` |

`query`

`URLSearchParams`

`params`

`Record<string, string>`

`user`

`HttpRequestUser \| null`

`body`

`ReadableStream \| null`

`bodyUsed`

`boolean`

In order to access a request or response's body, the following methods can be used:

| Method | Return Type |
|---|---|
`arrayBuffer()` |
`Promise<ArrayBuffer>` |

`blob()`

`Promise<Blob>`

`formData()`

`Promise<FormData>`

`json()`

`Promise<unknown>`

`text()`

`Promise<string>`

Note

The body functions can be run only once. Subsequent calls resolve with empty strings/ArrayBuffers.

### HTTP Response

The response can be set in several ways:

**Set the**`context.res`

property:`module.exports = async function (context, request) { context.res = { body: `Hello, world!` };`


**Return the response:**If your function is async and you set the binding name to`$return`

in your`function.json`

, you can return the response directly instead of setting it on`context`

.`{ "type": "http", "direction": "out", "name": "$return" }`

`module.exports = async function (context, request) { return { body: `Hello, world!` };`


**Set the named output binding:**This option works the same as any non HTTP binding. The binding name in`function.json`

must match the key on`context.bindings`

, or "response1" in the following example:`{ "type": "http", "direction": "out", "name": "response1" }`

`module.exports = async function (context, request) { context.bindings.response1 = { body: `Hello, world!` };`


**Call**This option is deprecated. It implicitly calls`context.res.send()`

:`context.done()`

and can't be used in an async function.`module.exports = function (context, request) { context.res.send(`Hello, world!`);`


If you create a new object when setting the response, that object must match the `HttpResponseSimple`

interface, which has the following properties:

| Property | Type | Description |
|---|---|---|
`headers` |
`Record<string, string>` (optional) |
HTTP response headers. |
`cookies` |
`Cookie[]` (optional) |
HTTP response cookies. |
`body` |
`any` (optional) |
HTTP response body. |
`statusCode` |
`number` (optional) |
HTTP response status code. If not set, defaults to `200` . |
`status` |
`number` (optional) |
The same as `statusCode` . This property is ignored if `statusCode` is set. |

You can also modify the `context.res`

object without overwriting it. The default `context.res`

object uses the `HttpResponseFull`

interface, which supports the following methods in addition to the `HttpResponseSimple`

properties:

| Method | Description |
|---|---|
`status()` |
Sets the status. |
`setHeader()` |
Sets a header field. NOTE: `res.set()` and `res.header()` are also supported and do the same thing. |
`getHeader()` |
Get a header field. NOTE: `res.get()` is also supported and does the same thing. |
`removeHeader()` |
Removes a header. |
`type()` |
Sets the "content-type" header. |
`send()` |
This method is deprecated. It sets the body and calls `context.done()` to indicate a sync function is finished. NOTE: `res.end()` is also supported and does the same thing. |
`sendStatus()` |
This method is deprecated. It sets the status code and calls `context.done()` to indicate a sync function is finished. |
`json()` |
This method is deprecated. It sets the "content-type" to "application/json", sets the body, and calls `context.done()` to indicate a sync function is finished. |

The response can be set in several ways:

**As a simple interface with type**This option is the most concise way of returning responses.`HttpResponseInit`

:`return { body: `Hello, world!` };`


The `HttpResponseInit`

interface has the following properties:

| Property | Type | Description |
|---|---|---|
`body` |
`BodyInit` (optional) |
HTTP response body as one of
`ArrayBuffer` |

[,](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array)

`AsyncIterable<Uint8Array>`

[,](https://developer.mozilla.org/docs/Web/API/Blob)

`Blob`

[,](https://developer.mozilla.org/docs/Web/API/FormData)

`FormData`

[,](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array)

`Iterable<Uint8Array>`

[,](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)

`NodeJS.ArrayBufferView`

[,](https://developer.mozilla.org/docs/Web/API/URLSearchParams)

`URLSearchParams`

`null`

, or `string`

.`jsonBody`

`any`

(optional)`HttpResponseInit.body`

property is ignored in favor of this property.`status`

`number`

(optional)`200`

.`headers`

[(optional)](https://developer.mozilla.org/docs/Web/API/Headers)`HeadersInit`

`cookies`

`Cookie[]`

(optional)**As a class with type**This option provides helper methods for reading and modifying various parts of the response like the headers.`HttpResponse`

:`const response = new HttpResponse({ body: `Hello, world!` }); response.headers.set("content-type", "application/json"); return response;`


The `HttpResponse`

class accepts an optional `HttpResponseInit`

as an argument to its constructor and has the following properties:

| Property | Type | Description |
|---|---|---|
`status` |
`number` |
HTTP response status code. |
`headers` |
`Headers` |

`cookies`

`Cookie[]`

`body`

`ReadableStream | null`

`bodyUsed`

`boolean`

## HTTP streams

HTTP streams is a feature that makes it easier to process large data, stream OpenAI responses, deliver dynamic content, and support other core HTTP scenarios. It lets you stream requests to and responses from HTTP endpoints in your Node.js function app. Use HTTP streams in scenarios where your app requires real-time exchange and interaction between client and server over HTTP. You can also use HTTP streams to get the best performance and reliability for your apps when using HTTP.

Important

HTTP streams aren't supported in the v3 model. [Upgrade to the v4 model](functions-node-upgrade-v4) to use the HTTP streaming feature.
The existing `HttpRequest`

and `HttpResponse`

types in programming model v4 already support various ways of handling the message body, including as a stream.

### Prerequisites

- The
version 4.3.0 or later.`@azure/functions`

npm package [Azure Functions runtime](functions-versions)version 4.28 or later.[Azure Functions Core Tools](functions-run-local)version 4.0.5530 or a later version, which contains the correct runtime version.

### Enable streams

Use these steps to enable HTTP streams in your function app in Azure and in your local projects:

If you plan to stream large amounts of data, modify the

setting in Azure. The default maximum body size allowed is`FUNCTIONS_REQUEST_BODY_SIZE_LIMIT`

`104857600`

, which limits your requests to a size of ~100 MB.For local development, also add

`FUNCTIONS_REQUEST_BODY_SIZE_LIMIT`

to the[local.settings.json file](functions-develop-local#local-settings-file).Add the following code to your app in any file included by your

[main field](functions-reference-node#registering-a-function).`const { app } = require("@azure/functions"); app.setup({ enableHttpStream: true });`


### Stream examples

This example shows an HTTP triggered function that receives data via an HTTP POST request, and the function streams this data to a specified output file:

```
const { app } = require('@azure/functions');
const { createWriteStream } = require('fs');
const { Writable } = require('stream');
app.http('httpTriggerStreamRequest', {
methods: ['POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
const writeStream = createWriteStream('<output file path>');
await request.body.pipeTo(Writable.toWeb(writeStream));
return { body: 'Done!' };
},
});
```


This example shows an HTTP triggered function that streams a file's content as the response to incoming HTTP GET requests:

```
const { app } = require('@azure/functions');
const { createReadStream } = require('fs');
app.http('httpTriggerStreamResponse', {
methods: ['GET'],
authLevel: 'anonymous',
handler: async (request, context) => {
const body = createReadStream('<input file path>');
return { body };
},
});
```


For a ready-to-run sample app using streams, check out this example on [GitHub](https://github.com/Azure-Samples/azure-functions-nodejs-stream).

### Stream considerations

- Use
`request.body`

to obtain the maximum benefit from using streams. You can still continue to use methods like`request.text()`

, which always return the body as a string.

## Hooks

Hooks aren't supported in the v3 model. [Upgrade to the v4 model](functions-node-upgrade-v4) to use hooks.

Use a hook to execute code at different points in the Azure Functions lifecycle. Hooks are executed in the order they're registered and can be registered from any file in your app. There are currently two scopes of hooks, "app" level and "invocation" level.

### Invocation hooks

Invocation hooks are executed once per invocation of your function, either before in a `preInvocation`

hook or after in a `postInvocation`

hook. By default your hook executes for all trigger types, but you can also filter by type. The following example shows how to register an invocation hook and filter by trigger type:

```
const { app } = require('@azure/functions');
app.hook.preInvocation((context) => {
if (context.invocationContext.options.trigger.type === 'httpTrigger') {
context.invocationContext.log(
`preInvocation hook executed for http function ${context.invocationContext.functionName}`
);
}
});
app.hook.postInvocation((context) => {
if (context.invocationContext.options.trigger.type === 'httpTrigger') {
context.invocationContext.log(
`postInvocation hook executed for http function ${context.invocationContext.functionName}`
);
}
});
```


The first argument to the hook handler is a context object specific to that hook type.

The `PreInvocationContext`

object has the following properties:

| Property | Description |
|---|---|
`inputs` |
The arguments passed to the invocation. |
`functionHandler` |
The function handler for the invocation. Changes to this value affect the function itself. |
`invocationContext` |
The
|

`hookData`

The `PostInvocationContext`

object has the following properties:

| Property | Description |
|---|---|
`inputs` |
The arguments passed to the invocation. |
`result` |
The result of the function. Changes to this value affect the overall result of the function. |
`error` |
The error thrown by the function, or null/undefined if there's no error. Changes to this value affect the overall result of the function. |
`invocationContext` |
The
|

`hookData`

### App hooks

App hooks are executed once per instance of your app, either during startup in an `appStart`

hook or during termination in an `appTerminate`

hook. App terminate hooks have a limited time to execute and don't execute in all scenarios.

The Azure Functions runtime currently [doesn't support](https://github.com/Azure/azure-functions-host/issues/8222) context logging outside of an invocation. Use the Application Insights [npm package](https://www.npmjs.com/package/applicationinsights) to log data during app level hooks.

The following example registers app hooks:

```
const { app } = require('@azure/functions');
app.hook.appStart((context) => {
// add your logic here
});
app.hook.appTerminate((context) => {
// add your logic here
});
```


The first argument to the hook handler is a context object specific to that hook type.

The `AppStartContext`

object has the following properties:

| Property | Description |
|---|---|
`hookData` |
The recommended place to store and share data between hooks in the same scope. You should use a unique property name so that it doesn't conflict with other hooks' data. |

The `AppTerminateContext`

object has the following properties:

| Property | Description |
|---|---|
`hookData` |
The recommended place to store and share data between hooks in the same scope. You should use a unique property name so that it doesn't conflict with other hooks' data. |

## Scaling and concurrency

By default, Azure Functions automatically monitors the load on your application and creates more host instances for Node.js as needed. Azure Functions uses built-in (not user configurable) thresholds for different trigger types to decide when to add instances, such as the age of messages and queue size for QueueTrigger. For more information, see [How the Consumption and Premium plans work](event-driven-scaling).

This scaling behavior is sufficient for many Node.js applications. For CPU-bound applications, you can improve performance further by using multiple language worker processes. You can increase the number of worker processes per host from the default of 1 up to a max of 10 by using the [FUNCTIONS_WORKER_PROCESS_COUNT](functions-app-settings#functions_worker_process_count) application setting. Azure Functions then tries to evenly distribute simultaneous function invocations across these workers. This behavior makes it less likely that a CPU-intensive function blocks other functions from running. The setting applies to each host that Azure Functions creates when scaling out your application to meet demand.

Warning

Use the `FUNCTIONS_WORKER_PROCESS_COUNT`

setting with caution. Multiple processes running in the same instance can lead to unpredictable behavior and increase function load times. If you use this setting, we *highly recommend* that you offset these downsides by [running from a package file](run-functions-from-deployment-package).

## Node version

You can see the current version that the runtime is using by logging `process.version`

from any function. See [ supported versions](#supported-versions) for a list of Node.js versions supported by each programming model.

### Setting the Node version

The way that you upgrade your Node.js version depends on the OS on which your function app runs.

When it runs on Windows, the Node.js version is set by the [ WEBSITE_NODE_DEFAULT_VERSION](functions-app-settings#website_node_default_version) application setting. This setting can be updated either by using the Azure CLI or in the Azure portal.

For more information about Node.js versions, see [Supported versions](#supported-versions).

Before upgrading your Node.js version, make sure your function app is running on the latest version of the Azure Functions runtime. If you need to upgrade your runtime version, see [Migrate apps from Azure Functions version 3.x to version 4.x](migrate-version-3-version-4?pivots=programming-language-javascript).

Run the Azure CLI [ az functionapp config appsettings set](/en-us/cli/azure/functionapp/config#az-functionapp-config-appsettings-set) command to update the Node.js version for your function app running on Windows:

```
az functionapp config appsettings set --settings WEBSITE_NODE_DEFAULT_VERSION=~22 \
--name <FUNCTION_APP_NAME> --resource-group <RESOURCE_GROUP_NAME>
```


This sets the [ WEBSITE_NODE_DEFAULT_VERSION application setting](functions-app-settings#website_node_default_version) the supported LTS version of

`~22`

.After changes are made, your function app restarts. To learn more about Functions support for Node.js, see [Language runtime support policy](language-support-policy).

## Environment variables

Environment variables can be useful for operational secrets (connection strings, keys, endpoints, etc.) or environmental settings such as profiling variables. You can add environment variables in both your local and cloud environments and access them through `process.env`

in your function code.

The following example logs the `WEBSITE_SITE_NAME`

environment variable:

```
module.exports = async function (context) {
context.log(`WEBSITE_SITE_NAME: ${process.env["WEBSITE_SITE_NAME"]}`);
};
```


```
async function timerTrigger1(myTimer, context) {
context.log(`WEBSITE_SITE_NAME: ${process.env["WEBSITE_SITE_NAME"]}`);
}
```


### In local development environment

When you run locally, your functions project includes a [ local.settings.json file](functions-run-local), where you store your environment variables in the

`Values`

object.```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "",
"FUNCTIONS_WORKER_RUNTIME": "node",
"CUSTOM_ENV_VAR_1": "hello",
"CUSTOM_ENV_VAR_2": "world"
}
}
```


### In Azure cloud environment

When you run in Azure, the function app lets you set and use [Application settings](functions-app-settings), such as service connection strings, and exposes these settings as environment variables during execution.

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

### Worker environment variables

There are several Functions environment variables specific to Node.js:

#### languageWorkers**node**arguments

This setting allows you to specify custom arguments when starting your Node.js process. It's most often used locally to start the worker in debug mode, but can also be used in Azure if you need custom arguments.

Warning

If possible, avoid using `languageWorkers__node__arguments`

in Azure because it can have a negative effect on cold start times. Rather than using prewarmed workers, the runtime has to start a new worker from scratch with your custom arguments.

#### logging**logLevel**Worker

This setting adjusts the default log level for Node.js-specific worker logs. By default, only warning or error logs are shown, but you can set it to `information`

or `debug`

to help diagnose issues with the Node.js worker. For more information, see [configuring log levels](configure-monitoring#configure-log-levels).

## ECMAScript modules (preview)

Note

As ECMAScript modules are currently a preview feature in Node.js 14 or higher in Azure Functions.

[ECMAScript modules](https://nodejs.org/docs/latest-v14.x/api/esm.html#esm_modules_ecmascript_modules) (ES modules) are the new official standard module system for Node.js. So far, the code samples in this article use the CommonJS syntax. When running Azure Functions in Node.js 14 or higher, you can choose to write your functions using ES modules syntax.

To use ES modules in a function, change its filename to use a `.mjs`

extension. The following *index.mjs* file example is an HTTP triggered function that uses ES modules syntax to import the `uuid`

library and return a value.

```
import { v4 as uuidv4 } from "uuid";
async function httpTrigger1(context, request) {
context.res.body = uuidv4();
}
export default httpTrigger;
```


```
import { v4 as uuidv4 } from "uuid";
async function httpTrigger1(request, context) {
return { body: uuidv4() };
}
app.http("httpTrigger1", {
methods: ["GET", "POST"],
handler: httpTrigger1,
});
```


## Configure function entry point

The `function.json`

properties `scriptFile`

and `entryPoint`

can be used to configure the location and name of your exported function. The `scriptFile`

property is required when you're using TypeScript and should point to the compiled JavaScript.

### Using `scriptFile`


By default, a JavaScript function is executed from `index.js`

, a file that shares the same parent directory as its corresponding `function.json`

.

`scriptFile`

can be used to get a folder structure that looks like the following example:

```
<project_root>/
| - node_modules/
| - myFirstFunction/
| | - function.json
| - lib/
| | - sayHello.js
| - host.json
| - package.json
```


The `function.json`

for `myFirstFunction`

should include a `scriptFile`

property pointing to the file with the exported function to run.

```
{
"scriptFile": "../lib/sayHello.js",
"bindings": [
...
]
}
```


### Using `entryPoint`


In the v3 model, a function must be exported using `module.exports`

in order to be found and run. By default, the function that executes when triggered is the only export from that file, the export named `run`

, or the export named `index`

. The following example sets `entryPoint`

in `function.json`

to a custom value, "logHello":

```
{
"entryPoint": "logHello",
"bindings": [
...
]
}
```


```
async function logHello(context) {
context.log("Hello, world!");
}
module.exports = { logHello };
```


## Local debugging

We recommend that you use VS Code for local debugging, which starts your Node.js process in debug mode automatically and attaches to the process for you. For more information, see [run the function locally](how-to-create-function-vs-code?pivot=programming-language-javascript#run-the-function-locally).

If you're using a different tool for debugging or want to start your Node.js process in debug mode manually, add `"languageWorkers__node__arguments": "--inspect"`

under `Values`

in your [local.settings.json](functions-develop-local#local-settings-file). The `--inspect`

argument tells Node.js to listen for a debug client, on port 9229 by default. For more information, see the [Node.js debugging guide](https://nodejs.org/en/learn/getting-started/debugging).

## Recommendations

This section describes several impactful patterns for Node.js apps that we recommend you follow.

### Choose single-vCPU App Service plans

When you create a function app that uses the App Service plan, we recommend that you select a single-vCPU plan rather than a plan with multiple vCPUs. Today, Functions runs Node.js functions more efficiently on single-vCPU VMs, and using larger VMs doesn't produce the expected performance improvements. When necessary, you can manually scale out by adding more single-vCPU VM instances, or you can enable autoscale. For more information, see [Scale instance count manually or automatically](/en-us/azure/azure-monitor/autoscale/autoscale-get-started?toc=/azure/app-service/toc.json).

### Run from a package file

When you develop Azure Functions in the serverless hosting model, cold starts are a reality. *Cold start* refers to the first time your function app starts after a period of inactivity, taking longer to start up. For Node.js apps with large dependency trees in particular, cold start can be significant. To speed up the cold start process, [run your functions as a package file](run-functions-from-deployment-package) when possible. Many deployment methods use this model by default, but if you're experiencing large cold starts you should check to make sure you're running this way.

### Use a single static client

When you use a service-specific client in an Azure Functions application, don't create a new client with every function invocation because you can hit connection limits. Instead, create a single, static client in the global scope. For more information, see [managing connections in Azure Functions](manage-connections).

### Use `async`

and `await`


When writing Azure Functions in Node.js, you should write code using the `async`

and `await`

keywords. Writing code using `async`

and `await`

instead of callbacks or `.then`

and `.catch`

with Promises helps avoid two common problems:

- Throwing uncaught exceptions that
[crash the Node.js process](https://nodejs.org/api/process.html#process_warning_using_uncaughtexception_correctly), potentially affecting the execution of other functions. - Unexpected behavior, such as missing logs from
`context.log`

, caused by asynchronous calls that aren't properly awaited.

In the following example, the asynchronous method `fs.readFile`

is invoked with an error-first callback function as its second parameter. This code causes both of the issues previously mentioned. An exception that isn't explicitly caught in the correct scope can crash the entire process (issue #1). Returning without ensuring the callback finishes means the http response sometimes has an empty body (issue #2).

```
// DO NOT USE THIS CODE
const { app } = require('@azure/functions');
const fs = require('fs');
app.http('httpTriggerBadAsync', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
let fileData;
fs.readFile('./helloWorld.txt', (err, data) => {
if (err) {
context.error(err);
// BUG #1: This will result in an uncaught exception that crashes the entire process
throw err;
}
fileData = data;
});
// BUG #2: fileData is not guaranteed to be set before the invocation ends
return { body: fileData };
},
});
```


In the following example, the asynchronous method `fs.readFile`

is invoked with an error-first callback function as its second parameter. This code causes both of the issues previously mentioned. An exception that isn't explicitly caught in the correct scope can crash the entire process (issue #1). Calling the deprecated `context.done()`

method outside of the scope of the callback can signal the function is finished before the file is read (issue #2). In this example, calling `context.done()`

too early results in missing log entries starting with `Data from file:`

.

```
// NOT RECOMMENDED PATTERN
const fs = require("fs");
module.exports = function (context) {
fs.readFile("./hello.txt", (err, data) => {
if (err) {
context.log.error("ERROR", err);
// BUG #1: This will result in an uncaught exception that crashes the entire process
throw err;
}
context.log(`Data from file: ${data}`);
// context.done() should be called here
});
// BUG #2: Data is not guaranteed to be read before the Azure Function's invocation ends
context.done();
};
```


Use the `async`

and `await`

keywords to help avoid both of these issues. Most APIs in the Node.js ecosystem have been converted to support promises in some form. For example, starting in v14, Node.js provides an `fs/promises`

API to replace the `fs`

callback API.

In the following example, any unhandled exceptions thrown during the function execution only fail the individual invocation that raised the exception. The `await`

keyword means that steps following `readFile`

only execute after it's complete.

```
// Recommended pattern
const { app } = require('@azure/functions');
const fs = require('fs/promises');
app.http('httpTriggerGoodAsync', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
try {
const fileData = await fs.readFile('./helloWorld.txt');
return { body: fileData };
} catch (err) {
context.error(err);
// This rethrown exception will only fail the individual invocation, instead of crashing the whole process
throw err;
}
},
});
```


With `async`

and `await`

, you also don't need to call the `context.done()`

callback.

```
// Recommended pattern
const fs = require("fs/promises");
module.exports = async function (context) {
let data;
try {
data = await fs.readFile("./hello.txt");
} catch (err) {
context.log.error("ERROR", err);
// This rethrown exception will be handled by the Functions Runtime and will only fail the individual invocation
throw err;
}
context.log(`Data from file: ${data}`);
};
```


## Troubleshoot

See the [Node.js Troubleshoot guide](functions-node-troubleshoot).

## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/python-build-options -->

# Build your Python Azure Functions apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions supports three build options for publishing your Python apps to Azure. Choose your build method based on your local environment, app dependencies, and runtime requirements.

## Quick comparison for build actions

| Deployment type | Where dependencies are installed | Typical use case |
|---|---|---|
|

[Local build](#local-build)[Custom dependencies](#custom-dependencies)## Deployment package considerations

When deploying your Python function app to Azure, keep these packaging requirements in mind:

**Package contents, not the folder**: Deploy the contents of your project folder, not the folder itself.**Root-level**: Ensure a single`host.json`

`host.json`

file is at the root of the deployment package, not nested in a subfolder.**Exclude development files**: You can exclude folders like`tests/`

,`.github/`

, and`.venv*/`

from the deployed package by including them in`.funcignore`

.**The build environment must match the production environment**: Your dependencies must be built on an ubuntu machine using the same python version as the production app.[Remote build](#remote-build)handles this scenario automatically.**Dependencies must be installed into**: Remote build installs all dependencies listed in`./.python_packages/lib/site-packages`

`requirements.txt`

into the correct directory.**Keep deployment package size in mind**: large dependency sets increase build time, cold start latency, and module import and initialization time. Applications with large scientific or ML libraries (including`pytorch`

) are especially impacted.**Remote build has a 60-second timeout**: If dependency installation exceeds the limit, the build fails. In that case, consider using a[local build](#local-build)and deploying with prebuilt dependencies.**Module import has a 2-minute time limit**: Python module loading and function indexing during startup has a 2-minute limit for Python 3.13 and above, or for older python versions with`PYTHON_ENABLE_INIT_INDEXING`

enabled. If your app exceeds this, reduce top-level imports or use lazy imports (import modules inside the function body instead of at the global scope).

## Remote build

Remote build is the recommended approach for a code-only deployment of your Python app to Functions.


With [remote build](functions-deployment-technologies#remote-build), the Functions platform handles package installation and ensures compatibility with the remote
runtime environment. Using remote build also results in a smaller deployment package.

You can use remote build when you publish your Python app using these tools:

: the**Azure Functions Core Tools**command requests a remote build by default when publishing Python apps.`func azure functionapp publish`

:**AZ CLI**uses remote build by default when deploying Python apps.`az functionapp deployment source config-zip`

: the**Visual Studio Code****Azure Functions: Deploy to Azure...**command always uses a remote build.: the**Continuous delivery by using GitHub Actions****Azure/functions-action@v1**action uses remote build when the`remote-build`

parameter is set to`true`

for the Flex Consumption plan or when`scm-do-build-during-deployment`

and`enable-oryx-build`

are set to`true`

for Dedicated plans.

To enable remote build for other scenarios, like [ Continuous delivery with Azure Pipelines](functions-how-to-azure-devops), see

[Enabling Remote Build](functions-deployment-technologies#remote-build).

Remote build also supports custom package indexes when by using the [ PIP_EXTRA_INDEX_URL](functions-app-settings#pip_extra_index_url) app setting. For more information, see

[Remote build](functions-deployment-technologies#remote-build).

Important

Remote build installs all dependencies listed in `requirements.txt`

. To ensure all required packages are installed, be sure to include those dependencies in your `requirements.txt`

file.

## Local build

If you don't request a remote build, then dependencies are instead installed on your machine. The entire local project and dependencies are then packaged locally and deployed to your function app. Using local build results in a larger package upload.

You also need to install dependencies into the correct directory. Use `pip install --target="./.python_packages/lib/site-packages"`

to install required dependencies into your local `.python_packages/lib/site-packages`

folder.
For example, if you have your dependencies listed in a `requirements.txt`

file, you can run this command:

```
pip install --target="./.python_packages/lib/site-packages" -r requirements.txt
```


Use local build when:

- You're developing locally on Linux or macOS.
- Remote build isn't available or is restricted.
- You want to define dependencies in a file other than
`requirements.txt`

, such as`pyproject.toml`

.

The following tools can be configured to use local build:

: use**Azure Functions Core Tools**with the`func azure functionapp publish`

`--no-build`

flag.:**AZ CLI**with the`az functionapp deployment source config-zip`

`--build-remote=false`

flag.: set the**Continuous delivery by using GitHub Actions**`remote-build`

parameter to`false`

for the Flex Consumption plan or set`scm-do-build-during-deployment`

and`enable-oryx-build`

to`false`

for Dedicated plans.

Important

When developing your Python apps on a Windows computer, don't use local build. Packages built on a Windows computer often have issues being deployed to and running on Linux in Azure Functions. Only use local build if you're confident the package runs on Linux based systems.

## Custom dependencies

Azure Functions supports custom and other non-PyPI dependencies by using the [ PIP_EXTRA_INDEX_URL](functions-app-settings#pip_extra_index_url) app setting or by creating a local build on a Linux or macOS computer.

### Remote build with an extra index URL

When your private packages are available online, you can request a remote build after setting the private package location by using the [ PIP_EXTRA_INDEX_URL](functions-app-settings#pip_extra_index_url) app setting.
When you set

[, remote builds use this package feed during deployment.](functions-app-settings#pip_extra_index_url)

`PIP_EXTRA_INDEX_URL`

[replaces the package index, so consider using](functions-app-settings#pip_index_url)

`PIP_INDEX_URL`

[instead to prevent unexpected behavior.](functions-app-settings#pip_extra_index_url)

`PIP_EXTRA_INDEX_URL`

### Local packages or wheels

Local packages and wheels are supported when building python Azure Function apps.

To install these packages or wheels using [remote build](#remote-build), you can include the dependencies in your `requirements.txt`

file and deploy with [remote build enabled](functions-deployment-technologies#remote-build).

For example, your `requirements.txt`

file might look like the following snippet:

```
# Installing a custom wheel
<my_package_wheel>.whl
# Installing a local package
path/to/my/package
```


To install these dependencies using [local build](#local-build), install the dependencies into your local `.python_packages/lib/site-packages`

folder and deploy with [remote build disabled](#local-build).
For example, if you have the packages defined in your `requirements.txt`

file, you can install and publish using the following commands and Core Tools:

```
pip install --target="./.python_packages/lib/site-packages" -r requirements.txt
func azure functionapp publish <APP_NAME> --no-build
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-publish -->

# Dapr Publish output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr publish output binding allows you to publish a message to a Dapr topic during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using a Dapr publish output binding to perform a Dapr publish operation to a pub/sub component and topic.

```
[FunctionName("PublishOutputBinding")]
public static void Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = "topic/{topicName}")] HttpRequest req,
[DaprPublish(PubSubName = "%PubSubName%", Topic = "{topicName}")] out DaprPubSubEvent pubSubEvent,
ILogger log)
{
string requestBody = new StreamReader(req.Body).ReadToEnd();
pubSubEvent = new DaprPubSubEvent(requestBody);
}
```


The following example creates a `"TransferEventBetweenTopics"`

function using the `DaprPublishOutput`

binding with an [ DaprTopicTrigger](functions-bindings-dapr-trigger-topic):

```
@FunctionName("TransferEventBetweenTopics")
public String run(
@DaprTopicTrigger(
pubSubName = "%PubSubName%",
topic = "A")
String request,
@DaprPublishOutput(
pubSubName = "%PubSubName%",
topic = "B")
OutputBinding<String> payload,
final ExecutionContext context) throws JsonProcessingException {
context.getLogger().info("Java function processed a TransferEventBetweenTopics request from the Dapr Runtime.");
}
```


In the following example, the Dapr publish output binding is paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('PublishOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "topic/{topicName}",
name: "req"
}),
return: daprPublishOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { payload: payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprPublish`

:

```
{
"bindings":
{
"type": "daprPublish",
"direction": "out",
"name": "pubEvent",
"pubsubname": "%PubSubName%",
"topic": "B"
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
# Example to use Dapr Service Invocation Trigger and Dapr State Output binding to persist a new state into statestore
param (
$subEvent
)
Write-Host "PowerShell function processed a TransferEventBetweenTopics request from the Dapr Runtime."
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $subEvent["data"]
$messageFromTopicA = "Transfer from Topic A: $jsonString".Trim()
$publish_output_binding_req_body = @{
"payload" = $messageFromTopicA
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name pubEvent -Value $publish_output_binding_req_body
```


The following example shows a Dapr Publish output binding, which uses the [v2 Python programming model](functions-reference-python). To use `daprPublish`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="TransferEventBetweenTopics")
@app.dapr_topic_trigger(arg_name="subEvent", pub_sub_name="%PubSubName%", topic="A", route="A")
@app.dapr_publish_output(arg_name="pubEvent", pub_sub_name="%PubSubName%", topic="B")
def main(subEvent, pubEvent: func.Out[bytes]) -> None:
logging.info('Python function processed a TransferEventBetweenTopics request from the Dapr Runtime.')
subEvent_json = json.loads(subEvent)
payload = "Transfer from Topic A: " + str(subEvent_json["data"])
pubEvent.set(json.dumps({"payload": payload}).encode('utf-8'))
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprPublish`

to define a Dapr publish output binding, which supports these parameters:

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
PubSubName |
The name of the Dapr pub/sub to send the message. | ✔️ | ✔️ |
Topic |
The name of the Dapr topic to send the message. | ✔️ | ✔️ |
Payload |
Required. The message being published. |
❌ | ✔️ |

## Annotations

The `DaprPublishOutput`

annotation allows you to have a function access a published message.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pubSubName |
The name of the Dapr pub/sub to send the message. | ✔️ | ✔️ |
topic |
The name of the Dapr topic to send the message. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pubsubname |
The name of the publisher component service. | ✔️ | ✔️ |
topic |
The name/identifier of the publisher topic. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pubsubname |
The name of the publisher component service. | ✔️ | ✔️ |
topic |
The name/identifier of the publisher topic. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_publish_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pub_sub_name |
The name of the publisher event. | ✔️ | ✔️ |
topic |
The publisher topic name/identifier. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr publish output binding, start by setting up a Dapr pub/sub component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprPublish`

in Python v2, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-dotnet-dependency-injection -->

# Use dependency injection in .NET Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions supports the dependency injection (DI) software design pattern, which is a technique to achieve [Inversion of Control (IoC)](/en-us/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#dependency-inversion) between classes and their dependencies.

Dependency injection in Azure Functions is built on the .NET Core Dependency Injection features. Familiarity with

[.NET Core dependency injection](/en-us/aspnet/core/fundamentals/dependency-injection)is recommended. There are differences in how you override dependencies and how configuration values are read with Azure Functions on the Consumption plan.Support for dependency injection begins with Azure Functions 2.x.

Dependency injection patterns differ depending on whether your C# functions run

[in-process](functions-dotnet-class-library)or[out-of-process](dotnet-isolated-process-guide).

Important

The guidance in this article applies only to [C# class library functions](functions-dotnet-class-library), which run in-process with the runtime. This custom dependency injection model doesn't apply to [.NET isolated functions](dotnet-isolated-process-guide), which lets you run .NET functions out-of-process. The .NET isolated worker process model relies on regular ASP.NET Core dependency injection patterns. To learn more, see [Dependency injection](dotnet-isolated-process-guide#dependency-injection) in the .NET isolated worker process guide.

## Prerequisites

Before you can use dependency injection, you must install the following NuGet packages:

[Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/)package version 1.0.28 or later[Microsoft.Extensions.DependencyInjection](https://www.nuget.org/packages/Microsoft.Extensions.DependencyInjection/)(currently, only version 2.x or later supported)

## Register services

To register services, create a method to configure and add components to an `IFunctionsHostBuilder`

instance. The Azure Functions host creates an instance of `IFunctionsHostBuilder`

and passes it directly into your method.

Warning

For function apps running in the Consumption or Premium plans, modifications to configuration values used in triggers can cause scaling errors. Any changes to these properties by the `FunctionsStartup`

class results in a function app startup error.

Injection of `IConfiguration`

can lead to unexpected behavior. To learn more about adding configuration sources, see [Customizing configuration sources](#customizing-configuration-sources).

To register the method, add the `FunctionsStartup`

assembly attribute that specifies the type name used during startup.

```
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.DependencyInjection;
[assembly: FunctionsStartup(typeof(MyNamespace.Startup))]
namespace MyNamespace;
public class Startup : FunctionsStartup
{
public override void Configure(IFunctionsHostBuilder builder)
{
builder.Services.AddHttpClient();
builder.Services.AddSingleton<IMyService>((s) => {
return new MyService();
});
builder.Services.AddSingleton<ILoggerProvider, MyLoggerProvider>();
}
}
```


This example uses the [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http/) package required to register an `HttpClient`

at startup.

### Caveats

A series of registration steps run before and after the runtime processes the startup class. Therefore, keep in mind the following items:

*The startup class is meant for only setup and registration.*Avoid using services registered at startup during the startup process. For instance, don't try to log a message in a logger that is being registered during startup. This point of the registration process is too early for your services to be available for use. After the`Configure`

method is run, the Functions runtime continues to register other dependencies, which can affect how your services operate.*The dependency injection container only holds explicitly registered types*. The only services available as injectable types are what are set up in the`Configure`

method. As a result, Functions-specific types like`BindingContext`

and`ExecutionContext`

aren't available during setup or as injectable types.*Configuring ASP.NET authentication isn't supported*. The Functions host configures ASP.NET authentication services to properly expose APIs for core lifecycle operations. Other configurations in a custom`Startup`

class can override this configuration, causing unintended consequences. For example, calling`builder.Services.AddAuthentication()`

can break authentication between the portal and the host, leading to messages such as[Azure Functions runtime is unreachable](functions-recover-storage-account#aspnet-authentication-overrides).

## Use injected dependencies

Constructor injection is used to make your dependencies available in a function. The use of constructor injection requires that you don't use static classes for injected services or for your function classes.

The following sample demonstrates how the `IMyService`

and `HttpClient`

dependencies are injected into an HTTP-triggered function.

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Logging;
using System.Net.Http;
using System.Threading.Tasks;
namespace MyNamespace;
public class MyHttpTrigger
{
private readonly HttpClient _client;
private readonly IMyService _service;
public MyHttpTrigger(IHttpClientFactory httpClientFactory, IMyService service)
{
this._client = httpClientFactory.CreateClient();
this._service = service;
}
[FunctionName("MyHttpTrigger")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
ILogger log)
{
var response = await _client.GetAsync("https://microsoft.com");
var message = _service.GetMessage();
return new OkObjectResult("Response from function with injected dependencies.");
}
}
```


This example uses the [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http/) package required to register an `HttpClient`

at startup.

## Service lifetimes

Azure Functions apps provide the same service lifetimes as [ASP.NET Dependency Injection](/en-us/aspnet/core/fundamentals/dependency-injection#service-lifetimes). For a Functions app, the different service lifetimes behave as follows:

**Transient**: Transient services are created upon each resolution of the service.**Scoped**: The scoped service lifetime matches a function execution lifetime. Scoped services are created once per function execution. Later requests for that service during the execution reuse the existing service instance.**Singleton**: The singleton service lifetime matches the host lifetime and is reused across function executions on that instance. Singleton lifetime services are recommended for connections and clients, for example`DocumentClient`

or`HttpClient`

instances.

View or download a [sample of different service lifetimes](https://github.com/Azure/azure-functions-dotnet-extensions/tree/main/src/samples/DependencyInjection/Scopes) on GitHub.

## Logging services

If you need your own logging provider, register a custom type as an instance of [ ILoggerProvider](/en-us/dotnet/api/microsoft.extensions.logging.iloggerfactory), which is available through the

[Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/)NuGet package.

Application Insights is added by Azure Functions automatically.

Warning

- Don't add
`AddApplicationInsightsTelemetry()`

to the services collection, which registers services that conflict with services provided by the environment. - Don't register your own
`TelemetryConfiguration`

or`TelemetryClient`

if you're using the built-in Application Insights functionality. If you need to configure your own`TelemetryClient`

instance, create one via the injected`TelemetryConfiguration`

as shown in[Log custom telemetry in C# functions](functions-dotnet-class-library?tabs=v2,cmd#log-custom-telemetry-in-c-functions).

### ILogger<T> and ILoggerFactory

The host injects `ILogger<T>`

and `ILoggerFactory`

services into constructors. However, by default these new logging filters are filtered out of the function logs. You need to modify the `host.json`

file to opt in to extra filters and categories.

The following example demonstrates how to add an `ILogger<HttpTrigger>`

with logs that are exposed to the host.

```
namespace MyNamespace;
public class HttpTrigger
{
private readonly ILogger<HttpTrigger> _log;
public HttpTrigger(ILogger<HttpTrigger> log)
{
_log = log;
}
[FunctionName("HttpTrigger")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)] HttpRequest req)
{
_log.LogInformation("C# HTTP trigger function processed a request.");
// ...
}
```


The following example `host.json`

file adds the log filter.

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
},
"logLevel": {
"MyNamespace.HttpTrigger": "Information"
}
}
}
```


For more information about log levels, see [Configure log levels](configure-monitoring#configure-log-levels).

## Function app provided services

The function host registers many services. The following services are safe to take as a dependency in your application:

| Service Type | Lifetime | Description |
|---|---|---|
`Microsoft.Extensions.Configuration.IConfiguration` |
Singleton | Runtime configuration |
`Microsoft.Azure.WebJobs.Host.Executors.IHostIdProvider` |
Singleton | Responsible for providing the ID of the host instance |

If there are other services you want to take a dependency on, [create an issue and propose them on GitHub](https://github.com/azure/azure-functions-host).

### Overriding host services

Overriding services provided by the host is currently not supported. If there are services you want to override, [create an issue and propose them on GitHub](https://github.com/azure/azure-functions-host).

## Working with options and settings

Values defined in [app settings](functions-how-to-use-azure-function-app-settings#settings) are available in an `IConfiguration`

instance, which allows you to read app settings values in the startup class.

You can extract values from the `IConfiguration`

instance into a custom type. Copying the app settings values to a custom type makes it easy test your services by making these values injectable. Settings read into the configuration instance must be simple key/value pairs. For functions running in an Elastic Premium plan, application setting names can only contain letters, numbers (`0-9`

), periods (`.`

), colons (`:`

) and underscores (`_`

). For more information, see [App setting considerations](functions-app-settings#app-setting-considerations).

Consider the following class that includes a property named consistent with an app setting:

```
public class MyOptions
{
public string MyCustomSetting { get; set; }
}
```


And a `local.settings.json`

file that might structure the custom setting as follows:

```
{
"IsEncrypted": false,
"Values": {
"MyOptions:MyCustomSetting": "Foobar"
}
}
```


From inside the `Startup.Configure`

method, you can extract values from the `IConfiguration`

instance into your custom type using the following code:

```
builder.Services.AddOptions<MyOptions>()
.Configure<IConfiguration>((settings, configuration) =>
{
configuration.GetSection("MyOptions").Bind(settings);
});
```


Calling `Bind`

copies values that have matching property names from the configuration into the custom instance. The options instance is now available in the IoC container to inject into a function.

The options object is injected into the function as an instance of the generic `IOptions`

interface. Use the `Value`

property to access the values found in your configuration.

```
using System;
using Microsoft.Extensions.Options;
public class HttpTrigger
{
private readonly MyOptions _settings;
public HttpTrigger(IOptions<MyOptions> options)
{
_settings = options.Value;
}
}
```


For more information, see [Options pattern in ASP.NET Core](/en-us/aspnet/core/fundamentals/configuration/options).

## Using ASP.NET Core user secrets

When you develop your app locally, ASP.NET Core provides a [Secret Manager tool](/en-us/aspnet/core/security/app-secrets#secret-manager) that allows you to store secret information outside the project root. It makes it less likely that secrets are accidentally committed to source control. Azure Functions Core Tools (version 3.0.3233 or later) automatically reads secrets created by the ASP.NET Core Secret Manager.

To configure a .NET Azure Functions project to use user secrets, run the following command in the project root.

```
dotnet user-secrets init
```


Then use the `dotnet user-secrets set`

command to create or update secrets.

```
dotnet user-secrets set MySecret "my secret value"
```


To access user secrets values in your function app code, use `IConfiguration`

or `IOptions`

.

## Customizing configuration sources

To specify other configuration sources, override the `ConfigureAppConfiguration`

method in your function app's `StartUp`

class.

The following sample adds configuration values from both base and optional environment-specific app settings files.

```
using System.IO;
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
[assembly: FunctionsStartup(typeof(MyNamespace.Startup))]
namespace MyNamespace;
public class Startup : FunctionsStartup
{
public override void ConfigureAppConfiguration(IFunctionsConfigurationBuilder builder)
{
FunctionsHostBuilderContext context = builder.GetContext();
builder.ConfigurationBuilder
.AddJsonFile(Path.Combine(context.ApplicationRootPath, "appsettings.json"), optional: true, reloadOnChange: false)
.AddJsonFile(Path.Combine(context.ApplicationRootPath, $"appsettings.{context.EnvironmentName}.json"), optional: true, reloadOnChange: false)
.AddEnvironmentVariables();
}
public override void Configure(IFunctionsHostBuilder builder)
{
}
}
```


Add configuration providers to the `ConfigurationBuilder`

property of `IFunctionsConfigurationBuilder`

. For more information on using configuration providers, see [Configuration in ASP.NET Core](/en-us/aspnet/core/fundamentals/configuration/#configuration-providers).

A `FunctionsHostBuilderContext`

is obtained from `IFunctionsConfigurationBuilder.GetContext()`

. Use this context to retrieve the current environment name and resolve the location of configuration files in your function app folder.

By default, configuration files such as `appsettings.json`

aren't automatically copied to the function app's output folder. Update your `.csproj`

file to match the following sample to ensure the files are copied.

```
<None Update="appsettings.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
</None>
<None Update="appsettings.Development.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
<CopyToPublishDirectory>Never</CopyToPublishDirectory>
</None>
```


## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-target-based-scaling -->

# Target-based scaling

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Target-based scaling provides a fast and intuitive scaling model for customers and is currently supported for these binding extensions:

[Apache Kafka](#apache-kafka)[Azure Cosmos DB](#azure-cosmos-db)[Azure Event Hubs](#event-hubs)[Azure Queue Storage](#storage-queues)[Azure Service Bus (queue and topics)](#service-bus-queues-and-topics)

Target-based scaling replaces the previous Azure Functions incremental scaling model as the default for these extension types. Incremental scaling added or removed a maximum of one worker at [each new instance rate](event-driven-scaling#understanding-scaling-behaviors), with complex decisions for when to scale. In contrast, target-based scaling allows scale up of four instances at a time, and the scaling decision is based on a simple target-based equation:

In this equation, *event source length* refers to the number of events that must be processed. The default *target executions per instance* values come from the Software Development Kits (SDKs) used by the Azure Functions extensions. You don't need to make any changes for target-based scaling to work.

## Considerations

The following considerations apply when using target-based scaling:

- Target-based scaling is enabled by default for function apps on the
[Consumption plan](consumption-plan),[Flex Consumption plan](flex-consumption-plan), and[Elastic Premium plans](functions-premium-plan). Event-driven scaling isn't supported when running on[Dedicated (App Service) plans](dedicated-plan). - Target-based scaling is enabled by default starting with version 4.19.0 of the Functions runtime.
- When you use target-based scaling, scale limits are still honored. For more information, see
[Limit scale out](event-driven-scaling#limit-scale-out). - To achieve the most accurate scaling based on metrics, use only one target-based triggered function per function app. You should also consider running in a Flex Consumption plan, which offers
[per-function scaling](flex-consumption-plan#per-function-scaling). - When multiple functions in the same function app are all requesting to scale out at the same time, a sum across those functions is used to determine the change in desired instances. Functions requesting to scale out override functions requesting to scale in.
- When there are scale-in requests without any scale-out requests, the max scale in value is used.

## Opting out

Target-based scaling is enabled by default for function apps hosted on a Consumption plan or on a Premium plans. To disable target-based scaling and fall back to incremental scaling, add the following app setting to your function app:

| App Setting | Value |
|---|---|
`TARGET_BASED_SCALING_ENABLED` |
0 |

## Customizing target-based scaling

You can make the scaling behavior more or less aggressive based on your app's workload by adjusting *target executions per instance*. Each extension has different settings that you can use to set *target executions per instance*.

This table summarizes the `host.json`

values that are used for the *target executions per instance* values and the defaults:

| Extension | host.json values | Default Value |
|---|---|---|
| Event Hubs (Extension v5.x+) | extensions.eventHubs.maxEventBatchSize | 100* |
| Event Hubs (Extension v3.x+) | extensions.eventHubs.eventProcessorOptions.maxBatchSize | 10 |
| Event Hubs (if defined) | extensions.eventHubs.targetUnprocessedEventThreshold | n/a |
| Service Bus (Extension v5.x+, Single Dispatch) | extensions.serviceBus.maxConcurrentCalls | 16 |
| Service Bus (Extension v5.x+, Single Dispatch Sessions Based) | extensions.serviceBus.maxConcurrentSessions | 8 |
| Service Bus (Extension v5.x+, Batch Processing) | extensions.serviceBus.maxMessageBatchSize | 1000 |
| Service Bus (Functions v2.x+, Single Dispatch) | extensions.serviceBus.messageHandlerOptions.maxConcurrentCalls | 16 |
| Service Bus (Functions v2.x+, Single Dispatch Sessions Based) | extensions.serviceBus.sessionHandlerOptions.maxConcurrentSessions | 2000 |
| Service Bus (Functions v2.x+, Batch Processing) | extensions.serviceBus.batchOptions.maxMessageCount | 1000 |
| Storage Queue | extensions.queues.batchSize | 16 |

* The default `maxEventBatchSize`

changed in [v6.0.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/6.0.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package. In earlier versions, this value was 10.

For some binding extensions, the *target executions per instance* configuration is set using a function attribute:

| Extension | Function trigger setting | Default Value |
|---|---|---|
| Apache Kafka | `lagThreshold` |
1000 |
| Azure Cosmos DB | `maxItemsPerInvocation` |
100 |

To learn more, see the [example configurations for the supported extensions](#supported-extensions).

## Premium plan with runtime scale monitoring enabled

When [runtime scale monitoring](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers) is enabled the extensions themselves handle dynamic scaling because the [scale controller](event-driven-scaling#runtime-scaling) doesn't have access to services secured by a virtual network. After you enable runtime scale monitoring, you'll need to upgrade your extension packages to these minimum versions to unlock the extra target-based scaling functionality:

| Extension Name | Minimum Version Needed |
|---|---|
| Apache Kafka | 3.9.0 |
| Azure Cosmos DB | 4.1.0 |
| Event Hubs | 5.2.0 |
| Service Bus | 5.9.0 |
| Storage Queue | 5.1.0 |

## Dynamic concurrency support

Target-based scaling introduces faster scaling, and uses defaults for *target executions per instance*. When using Service Bus, Storage queues, or Kafka, you can also enable [dynamic concurrency](functions-concurrency#dynamic-concurrency). In this configuration, the _target execution per instance value is determined automatically by the dynamic concurrency feature. It starts with limited concurrency and identifies the best setting over time.

## Supported extensions

The way in which you configure target-based scaling in your host.json file depends on the specific extension type. This section provides the configuration details for the extensions that currently support target-based scaling.

### Service Bus queues and topics

The Service Bus extension support three execution models, determined by the `IsBatched`

and `IsSessionsEnabled`

attributes of your Service Bus trigger. The default value for `IsBatched`

and `IsSessionsEnabled`

is `false`

.

| Execution Model | IsBatched | IsSessionsEnabled | Setting Used for target executions per instance |
|---|---|---|---|
| Single dispatch processing | false | false | maxConcurrentCalls |
| Single dispatch processing (session-based) | false | true | maxConcurrentSessions |
| Batch processing | true | false | maxMessageBatchSize or maxMessageCount |

Note

**Scale efficiency:** For the Service Bus extension, use *Manage* rights on resources for the most efficient scaling. With *Listen* rights, scaling reverts to incremental scale because the queue or topic length can't be used to inform scaling decisions. To learn more about setting rights in Service Bus access policies, see [Shared Access Authorization Policy](../service-bus-messaging/service-bus-sas#shared-access-authorization-policies).

#### Single dispatch processing

In this model, each invocation of your function processes a single message. The `maxConcurrentCalls`

setting governs *target executions per instance*. The specific setting depends on the version of the Service Bus extension.

Modify the `host.json`

setting `maxConcurrentCalls`

, as in the following example:

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"maxConcurrentCalls": 16
}
}
}
```


#### Single dispatch processing (session-based)

In this model, each invocation of your function processes a single message. However, depending on the number of active sessions for your Service Bus topic or queue, each instance leases one or more sessions. The specific setting depends on the version of the Service Bus extension.

Modify the `host.json`

setting `maxConcurrentSessions`

to set *target executions per instance*, as in the following example:

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"maxConcurrentSessions": 8
}
}
}
```


#### Batch processing

In this model, each invocation of your function processes a batch of messages. The specific setting depends on the version of the Service Bus extension.

Modify the `host.json`

setting `maxMessageBatchSize`

to set *target executions per instance*, as in the following example:

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"maxMessageBatchSize": 1000
}
}
}
```


### Event Hubs

For Azure Event Hubs, Azure Functions scales based on the number of unprocessed events distributed across all the partitions in the event hub within a list of valid instance counts. By default, the `host.json`

attributes used for *target executions per instance* are `maxEventBatchSize`

and `maxBatchSize`

. However, if you choose to fine-tune target-based scaling, you can define a separate parameter `targetUnprocessedEventThreshold`

that overrides to set *target executions per instance* without changing the batch settings. If `targetUnprocessedEventThreshold`

is set, the total unprocessed event count is divided by this value to determine the number of instances, which is then be rounded up to a worker instance count that creates a balanced partition distribution.

Warning

Setting `batchCheckpointFrequency`

above 1 for hosting plans supported by [target based scaling](#considerations) can cause incorrect scaling behavior. The platform calculates unprocessed events as "current position - checkpointed position", which may incorrectly indicate unprocessed messages when batches have been processed but not yet checkpointed, preventing proper scale-in when no messages remain.

#### Scaling Behavior and Stability

For Event Hubs, frequent scale-in and scale-out operations can trigger partition rebalancing, which leads to processing delays and increased latency. To mitigate this:

- The platform uses a predefined list of valid worker counts to guide scaling decisions.
- The platform ensures that scaling is stable and deliberate, avoiding disruptive changes to partition assignments.
- If the desired worker count isn't in the valid list—for example, 17, the system automatically selects the next largest valid count, which in this case is 32. Additionally, to prevent rapid repeated scaling, scale-in requests are throttled for 3 minutes after the last scale-up. This delay helps reduce unnecessary rebalancing and contributes to maintaining throughput efficiency.

#### Valid Instance Counts for Event Hubs

For each Event Hubs partition count, we calculate a corresponding list of valid instance counts to ensure optimal distribution and efficient scaling. These counts are chosen to align well with partitioning and concurrency requirements:

| Partition Count | Valid Instance Counts |
|---|---|
| 1 | [1] |
| 2 | [1, 2] |
| 4 | [1, 2, 4] |
| 8 | [1, 2, 3, 4, 8] |
| 10 | [1, 2, 3, 4, 5, 10] |
| 16 | [1, 2, 3, 4, 5, 6, 8, 16] |
| 32 | [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 16, 32] |

These predefined counts help ensure that instances are distributed as evenly as possible across partitions, minimizing idle or overloaded workers.

Note

Note: For Premium and Dedicated event hub tiers the partition count can exceed 32, allowing for larger valid instance count sets. These tiers support higher throughput and scalability, and the valid worker count list is extended accordingly to evenly distribute event hub partitions across instances. Also, since Event Hubs is a partitioned workload, the number of partitions in your event hub is the limit for the maximum target instance count.

#### Event Hubs settings

The specific setting depends on the version of the Event Hubs extension.

Modify the `host.json`

setting `maxEventBatchSize`

to set *target executions per instance*, as in the following example:

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"maxEventBatchSize" : 100
}
}
}
```


When defined in `host.json`

, `targetUnprocessedEventThreshold`

is used as *target executions per instance* instead of `maxEventBatchSize`

, as in the following example:

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"targetUnprocessedEventThreshold": 153
}
}
}
```


### Storage Queues

For **v2.x+** of the Storage extension, modify the `host.json`

setting `batchSize`

to set *target executions per instance*:

```
{
"version": "2.0",
"extensions": {
"queues": {
"batchSize": 16
}
}
}
```


Note

**Scale efficiency:** For the storage queue extension, messages with [visibilityTimeout](/en-us/rest/api/storageservices/put-message#uri-parameters) are still counted in *event source length* by the Storage Queue APIs. This can cause overscaling of your function app. Consider using Service Bus queues que scheduled messages, [limiting scale out](event-driven-scaling#limit-scale-out), or not using visibilityTimeout for your solution.

### Azure Cosmos DB

Azure Cosmos DB uses a function-level attribute, `MaxItemsPerInvocation`

. The way you set this function-level attribute depends on your function language.

For a compiled C# function, set `MaxItemsPerInvocation`

in your trigger definition, as shown in the following examples for an in-process C# function:

```
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
collectionName: "Items",
MaxItemsPerInvocation: 100,
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


Note

Since Azure Cosmos DB is a partitioned workload, the number of physical partitions in your container is the limit for the target instance count. To learn more about Azure Cosmos DB scaling, see [physical partitions](/en-us/azure/cosmos-db/nosql/change-feed-processor#dynamic-scaling) and [lease ownership](/en-us/azure/cosmos-db/nosql/change-feed-processor#dynamic-scaling).

### Apache Kafka

The Apache Kafka extension uses a function-level attribute, `LagThreshold`

. For Kafka, the number of *desired instances* is calculated based on the total consumer lag divided by the `LagThreshold`

setting. For a given lag, reducing the lag threshold increases the number of desired instances.

The way you set this function-level attribute depends on your function language. This example sets the threshold to `100`

.

For a compiled C# function, set `LagThreshold`

in your trigger definition, as shown in the following examples for an in-process C# function for a Kafka Event Hubs trigger:

```
[FunctionName("KafkaTrigger")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "$ConnectionString",
Password = "%EventHubConnectionString%",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default",
LagThreshold = 100)] KafkaEventData<string> kevent, ILogger log)
{
log.LogInformation($"C# Kafka trigger function processed a message: {kevent.Value}");
}
```


## Next steps

To learn more, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-output -->

# Azure Database for MySQL output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use the Azure Database for MySQL output binding to write to a database.

For information on setup and configuration, see the [overview](functions-bindings-azure-mysql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

This section contains the following example:

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


### HTTP trigger, write one record

The following example shows a [C# function](functions-dotnet-class-library) that adds a record to a database, by using data provided in an HTTP `POST`

request as a JSON body.

```
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Azure.Functions.Worker.Http;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.OutputBindingSamples
{
public static class AddProduct
{
[FunctionName(nameof(AddProduct))]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "addproduct")]
[FromBody] Product prod,
[MySql("Products", "MySqlConnectionString")] out Product product)
{
product = prod;
return new CreatedResult($"/api/addproduct", product);
}
}
}
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-java).

This section contains the following example:

The example refers to a `Product`

class and a corresponding database table:

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


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write a record to a table

The following example shows an Azure Database for MySQL output binding in a Java function that adds a record to a table, by using data provided in an HTTP `POST`

request as a JSON body. The function takes an additional dependency on the [com.google.code.gson](https://github.com/google/gson) library to parse the JSON body.

```
<dependency>
<groupId>com.google.code.gson</groupId>
<artifactId>gson</artifactId>
<version>2.10.1</version>
</dependency>
```


```
package com.function;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.OutputBinding;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.mysql.annotation.MySqlOutput;
import com.fasterxml.jackson.core.JsonParseException;
import com.fasterxml.jackson.databind.JsonMappingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.function.Common.Product;
import java.io.IOException;
import java.util.Optional;
public class AddProduct {
@FunctionName("AddProduct")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "addproduct")
HttpRequestMessage<Optional<String>> request,
@MySqlOutput(
name = "product",
commandText = "Products",
connectionStringSetting = "MySqlConnectionString")
OutputBinding<Product> product) throws JsonParseException, JsonMappingException, IOException {
String json = request.getBody().get();
ObjectMapper mapper = new ObjectMapper();
Product p = mapper.readValue(json, Product.class);
product.setValue(p);
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(product).build();
}
}
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

This section contains the following example:

The example refers to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write records to a table

The following example shows an Azure Database for MySQL output binding that adds records to a table, by using data provided in an HTTP `POST`

request as a JSON body.

```
const { app, output } = require('@azure/functions');
const mysqlOutput = output.generic({
type: 'mysql',
commandText: 'Products',
connectionStringSetting: 'MySqlConnectionString'
})
// Upsert the product, which will insert it into the Products table if the primary key (ProductId) for that item doesn't exist.
// If it does, update it to have the new name and cost.
app.http('AddProduct', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [mysqlOutput],
handler: async (request, context) => {
// Note that this expects the body to be a JSON object or array of objects that have a property
// matching each of the columns in the table to upsert to.
const product = await request.json();
context.extraOutputs.set(mysqlOutput, product);
return {
status: 201,
body: JSON.stringify(product)
};
}
});
```


```
const { app, output } = require('@azure/functions');
const mysqlOutput = output.generic({
type: 'mysql',
commandText: 'Products',
connectionStringSetting: 'MySqlConnectionString'
})
// Upsert the product, which will insert it into the Products table if the primary key (ProductId) for that item doesn't exist.
// If it does, update it to have the new name and cost.
app.http('AddProduct', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [mysqlOutput],
handler: async (request, context) => {
// Note that this expects the body to be a JSON object or array of objects that have a property
// matching each of the columns in the table to upsert to.
const product = await request.json();
context.extraOutputs.set(mysqlOutput, product);
return {
status: 201,
body: JSON.stringify(product)
};
}
});
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-powershell).

This section contains the following example:

The example refers to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write records to a table

The following example shows an Azure Database for MySQL output binding in a function.json file and a PowerShell function that adds records to a table, by using data provided in an HTTP `POST`

request as a JSON body.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"direction": "in",
"type": "httpTrigger",
"methods": [
"post"
],
"route": "addproduct"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "product",
"type": "mysql",
"direction": "out",
"commandText": "Products",
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
# Trigger binding data passed in via parameter block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell function with MySql Output Binding processed a request."
# Note that this expects the body to be a JSON object or array of objects
# that have a property matching each of the columns in the table to upsert to.
$req_body = $Request.Body
# Assign the value that you want to pass to the MySQL output binding.
# The -Name value corresponds to the name property in the function.json file for the binding.
Push-OutputBinding -Name product -Value $req_body
# Assign the value to return as the HTTP response.
# The -Name value matches the name property in the function.json file for the binding.
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-python).

This section contains the following example:

The example refers to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


Note

You must use Azure Functions version 1.22.0b4 for Python.

### HTTP trigger, write records to a table

The following example shows an Azure Database for MySQL output binding in a function.json file and a Python function that adds records to a table, by using data provided in an HTTP `POST`

request as a JSON body.

The following example is sample Python code for the function_app.py file:

```
import json
import azure.functions as func
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.generic_trigger(arg_name="req", type="httpTrigger", route="addproduct")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_output_binding(arg_name="r", type="mysql",
command_text="Products",
connection_string_setting="MySqlConnectionString")
def mysql_output(req: func.HttpRequest, r: func.Out[func.MySqlRow]) \
-> func.HttpResponse:
body = json.loads(req.get_body())
row = func.MySqlRow.from_dict(body)
r.set(row)
return func.HttpResponse(
body=req.get_body(),
status_code=201,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the `MySqlAttribute`

attribute to declare the MySQL bindings on the function, which has the following properties:

| Attribute property | Description |
|---|---|
`CommandText` |
Required. The name of the table that the binding writes to. |
`ConnectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@MySQLOutput`

annotation on parameters whose value would come from Azure Database for MySQL. This annotation supports the following elements:

| Element | Description |
|---|---|
`commandText` |
Required. The name of the table that the binding writes to. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |
`name` |
Required. The unique name of the function binding. |

## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.generic()`

method:

| Property | Description |
|---|---|
`commandText` |
Required. The name of the table that the binding writes to. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |

## Configuration

The following table explains the binding configuration properties that you set in the function.json file:

| Property | Description |
|---|---|
`type` |
Required. Must be set to `Mysql` . |
`direction` |
Required. Must be set to `out` . |
`name` |
Required. The name of the variable that represents the entity in function code. |
`commandText` |
Required. The name of the table that the binding writes to. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Note

The output binding supports all special characters, including dollar sign ($), backtick (`), hyphen (-), and underscore (_). For more information, see the [MySQL community documentation](https://dev.mysql.com/doc/refman/8.0/en/identifiers.html).

A programming language might define member attributes that contain special characters that it supports. For example, C# has a few limitations for defining [variables](/en-us/dotnet/csharp/fundamentals/coding-style/identifier-names).

Otherwise, you can use `JObject`

for the output binding that covers all special characters. You can follow a [detailed example on GitHub](https://github.com/Azure/azure-functions-mysql-extension/blob/main/samples/samples-csharp/OutputBindingSamples/AddProductJObject.cs).

## Usage

The `CommandText`

property is the name of the table where the data is stored. The name of the connection string setting corresponds to the application setting that contains the connection string to Azure Database for MySQL.

If an exception occurs when a MySQL input binding is executed, the function code won't run. The result might be an error code, such as an HTTP trigger that returns a 500 error code.
