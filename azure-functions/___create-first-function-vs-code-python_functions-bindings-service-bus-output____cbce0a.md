---
merged_at: 2026-01-28T07:43:39.512878
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-python -->

# Quickstart: Create and deploy function code to Azure using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Visual Studio Code to create a function that responds to HTTP requests from a template. Use GitHub Copilot to improve the generated function code, verify code updates locally, and then deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Use Visual Studio Code to create a [custom handler](functions-custom-handlers) function that responds to HTTP requests. After verifying the code locally, you deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Custom handlers can be used to create functions in any language or runtime by running an HTTP server process. This article supports both Go and Rust.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Make sure to select your preferred development language at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17, or 21 (Linux-only).[Apache Maven](https://maven.apache.org), version 3.0 or above.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

## Install or update Core Tools

The Azure Functions extension for Visual Studio Code integrates with Azure Functions Core Tools so that you can run and debug your functions locally in Visual Studio Code using the Azure Functions runtime. Before getting started, it's a good idea to install Core Tools locally or update an existing installation to use the latest version.

In Visual Studio Code, select F1 to open the command palette, and then search for and run the command **Azure Functions: Install or Update Core Tools**.

This command tries to either start a package-based installation of the latest version of Core Tools or update an existing package-based installation. If you don't have npm or Homebrew installed on your local computer, you must instead [manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project in your preferred language. Later in the article, you update, run, and then publish your function code to Azure.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

.Choose the directory location for your project workspace and choose

**Select**. You should either create a new folder or choose an empty folder for the project workspace. Don't choose a project folder that is already part of a workspace.Provide the following information at the prompts:

Prompt Selection **Select a language**Choose `C#`

.**Select a .NET runtime**Choose `.NET 8.0 LTS`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Provide a namespace**Type `My.Functions`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Java`

.**Select a version of Java**Choose `Java 8`

,`Java 11`

,`Java 17`

or`Java 21`

, the Java version on which your functions run in Azure. Choose a Java version that you've verified locally.**Provide a group ID**Choose `com.function`

.**Provide an artifact ID**Choose `myFunction`

.**Provide a version**Choose `1.0-SNAPSHOT`

.**Provide a package name**Choose `com.function`

.**Provide an app name**Choose `myFunction-12345`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Select the build tool for Java project**Choose `Maven`

.**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `JavaScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `TypeScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Python`

.**Select a Python interpreter to create a virtual environment**Choose your preferred Python interpreter. If an option isn't shown, type in the full path to your Python binary. **Select a template for your project's first function**Choose `HTTP trigger`

.**Name of the function you want to create**Enter `HttpExample`

.**Authorization level**Choose `FUNCTION`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `PowerShell`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `Custom Handler`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Using this information, Visual Studio Code generates a code project for Azure Functions with an HTTP trigger function endpoint. You can view the local project files in the Explorer. To learn more about files that are created, see

[Generated project files](functions-develop-vs-code?tabs=javascript#generated-project-files).

In the local.settings.json file, update the

`AzureWebJobsStorage`

setting as in the following example:`"AzureWebJobsStorage": "UseDevelopmentStorage=true",`

This setting tells the local Functions host to use the storage emulator for the storage connection required by the Python v2 model. When you publish your project to Azure, this setting uses the default storage account instead. If you use an Azure Storage account during local development, set your storage account connection string here.


## Start the emulator

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run your function locally.


## Create and build your function

The *function.json* file in the *HttpExample* folder declares an HTTP trigger function. You complete the function by adding a handler and compiling it into an executable.

Press

`Ctrl + N`(`Cmd + N`on macOS) to create a new file. Save it as*handler.go*in the function app root (in the same folder as*host.json*).In

*handler.go*, add the following code and save the file. This is your Go custom handler.`package main import ( "fmt" "log" "net/http" "os" ) func helloHandler(w http.ResponseWriter, r *http.Request) { message := "This HTTP triggered function executed successfully. Pass a name in the query string for a personalized response.\n" name := r.URL.Query().Get("name") if name != "" { message = fmt.Sprintf("Hello, %s. This HTTP triggered function executed successfully.\n", name) } fmt.Fprint(w, message) } func main() { listenAddr := ":8080" if val, ok := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT"); ok { listenAddr = ":" + val } http.HandleFunc("/api/HttpExample", helloHandler) log.Printf("About to listen on %s. Go to https://127.0.0.1%s/", listenAddr, listenAddr) log.Fatal(http.ListenAndServe(listenAddr, nil)) }`

Press

`Ctrl + Shift + ``or select*New Terminal*from the*Terminal*menu to open a new integrated terminal in VS Code.Compile your custom handler using the following command. An executable file named

`handler`

(`handler.exe`

on Windows) is output in the function app root folder.`go build handler.go`


## Configure your function app

The function host needs to be configured to run your custom handler binary when it starts.

Open

*host.json*.In the

`customHandler.description`

section, set the value of`defaultExecutablePath`

to`handler`

(on Windows, set it to`handler.exe`

).In the

`customHandler`

section, add a property named`enableForwardingHttpRequest`

and set its value to`true`

. For functions consisting of only an HTTP trigger, this setting simplifies programming by allow you to work with a typical HTTP request instead of the custom handler[request payload](functions-custom-handlers#request-payload).Confirm the

`customHandler`

section looks like this example. Save the file.`"customHandler": { "description": { "defaultExecutablePath": "handler", "workingDirectory": "", "arguments": [] }, "enableForwardingHttpRequest": true }`


The function app is configured to start your custom handler executable.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure.

To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the Output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to

**WSL Bash**.With Core Tools still running in

**Terminal**, choose the Azure icon in the activity bar. In the**Workspace**area, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the new function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in

**Terminal**panel.With the

**Terminal**panel focused, press`Ctrl + C`to stop Core Tools and disconnect the debugger.

After you verify that the function runs correctly on your local computer, you can optionally use AI tools, such as GitHub Copilot in Visual Studio Code, to update template-generated function code.

## Use AI to normalize and validate input

This example prompt for Copilot Chat updates the existing function code to retrieve parameters from either the query string or JSON body. It applies formatting or type conversions and returns the parameters as JSON in the response:

```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Make sure that any added packages are compatible with the version of the packages already in the project
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Update the FunctionTest.java file to test the new logic.
```


You can customize your prompt to add specifics as needed. Then run the app again locally and verify that it works as expected after the code changes. This time, use a message body like:

```
{ "name": "devon torres", "email": "torres.devon@contoso.com", "age": "34" }
```


Tip

GitHub Copilot is powered by AI, so surprises and mistakes are possible. If you encounter any errors during execution, paste the error message in the chat window, select **Agent** mode, and ask Copilot to help resolve the error. For more information, see [Copilot FAQs](https://aka.ms/copilot-general-use-faqs).

When running in **Agent** mode, the results of this customization depend on the specific tools available to your agent.

When you're satisfied with your app, use Visual Studio Code to publish the project directly to Azure.

After you verify that the function runs correctly on your local computer, use Visual Studio Code to publish the project directly to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Compile the custom handler for Azure

In this section, you compile your project for deployment to Azure in a function app running Linux. In most cases, you need to recompile your binary and adjust your configuration to match the target platform before publishing it to Azure.

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Run the function in Azure

Press

`F1`to display the command palette, then search for and run the command`Azure Functions:Execute Function Now...`

. If prompted, select your subscription.Select your new function app resource and

`HttpExample`

as your function.In

**Enter request body**type`{ "name": "Contoso", "email": "me@contoso.com", "age": "34" }`

, then press Enter to send this request message to your function.When the function executes in Azure, the response is displayed in the notification area. Expand the notification to review the full response.


## Troubleshooting

Use the following table to resolve the most common issues encountered when using this article.

| Problem | Solution |
|---|---|
| Can't create a local function project? | Make sure you have the
|

[Azure Functions Core Tools installed](functions-run-local?tabs=node).When running on Windows, make sure that the default terminal shell for Visual Studio Code isn't set to WSL Bash.

## Clean up resources

When you continue to the [next step](#next-steps) and add an Azure Storage queue binding to your function, you'll need to keep all your resources in place to build on what you've already done.

Otherwise, you can use the following steps to delete the function app and its related resources to avoid incurring any further costs.

- In Visual Studio Code, select the Azure icon to open the Azure explorer.
- In the Resource Groups section, find your resource group.
- Right-click the resource group and select
**Delete**.

To learn more about Functions costs, see [Estimating Consumption plan costs](functions-consumption-costs).

## Next steps

You used [Visual Studio Code](functions-develop-vs-code) to create a function app with a simple HTTP-triggered function. In the next articles, you expand that function by connecting to either Azure Cosmos DB or Azure Storage. To learn more about connecting to other Azure services, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function). If you want to learn more about security, see [Securing Azure Functions](security-concepts).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus-output -->

# Azure Service Bus output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Azure Service Bus output binding to send queue or topic messages.

For information on setup and configuration details, see the [overview](functions-bindings-service-bus).

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

This code defines and initializes the `ILogger`

:

```
private readonly ILogger<ServiceBusReceivedMessageFunctions> _logger;
public ServiceBusReceivedMessageFunctions(ILogger<ServiceBusReceivedMessageFunctions> logger)
{
_logger = logger;
}
```


This example shows a [C# function](dotnet-isolated-process-guide) that receives a message and writes it to a second queue:

```
[Function(nameof(ServiceBusReceivedMessageFunction))]
[ServiceBusOutput("outputQueue", Connection = "ServiceBusConnection")]
public string ServiceBusReceivedMessageFunction(
[ServiceBusTrigger("queue", Connection = "ServiceBusConnection")] ServiceBusReceivedMessage message)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
_logger.LogInformation("Message Content-Type: {contentType}", message.ContentType);
var outputMessage = $"Output message created at {DateTime.Now}";
return outputMessage;
}
```


This example uses an HTTP trigger with an `OutputType`

object to both send an HTTP response and write the output message.

```
[Function("HttpSendMsg")]
public async Task<OutputType> Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req, FunctionContext context)
{
_logger.LogInformation($"C# HTTP trigger function processed a request for {context.InvocationId}.");
HttpResponseData response = req.CreateResponse(HttpStatusCode.OK);
await response.WriteStringAsync("HTTP response: Message sent");
return new OutputType()
{
OutputEvent = "MyMessage",
HttpResponse = response
};
}
```


This code defines the multiple output type `OutputType`

, which includes the Service Bus output binding definition on `OutputEvent`

:

```
public class OutputType
{
[ServiceBusOutput("TopicOrQueueName", Connection = "ServiceBusConnection")]
public string OutputEvent { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The following example shows a Java function that sends a message to a Service Bus queue `myqueue`

when triggered by an HTTP request.

```
@FunctionName("httpToServiceBusQueue")
@ServiceBusQueueOutput(name = "message", queueName = "myqueue", connection = "AzureServiceBusConnection")
public String pushToQueue(
@HttpTrigger(name = "request", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
final String message,
@HttpOutput(name = "response") final OutputBinding<T> result ) {
result.setValue(message + " has been sent.");
return message;
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@QueueOutput`

annotation on function parameters whose value would be written to a Service Bus queue. The parameter type should be `OutputBinding<T>`

, where `T`

is any native Java type of a plan old Java object (POJO).

Java functions can also write to a Service Bus topic. The following example uses the `@ServiceBusTopicOutput`

annotation to describe the configuration for the output binding.

```
@FunctionName("sbtopicsend")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@ServiceBusTopicOutput(name = "message", topicName = "mytopicname", subscriptionName = "mysubscription", connection = "ServiceBusConnection") OutputBinding<String> message,
final ExecutionContext context) {
String name = request.getBody().orElse("Azure Functions");
message.setValue(name);
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
}
```


The following example shows a timer triggered [TypeScript function](functions-reference-node?tabs=typescript) that sends a queue message every 5 minutes.

```
import { app, InvocationContext, output, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<string> {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.serviceBusQueue({
queueName: 'testqueue',
connection: 'MyServiceBusConnection',
}),
handler: timerTrigger1,
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


The following example shows a timer triggered [JavaScript function](functions-reference-node) that sends a queue message every 5 minutes.

```
const { app, output } = require('@azure/functions');
const serviceBusOutput = output.serviceBusQueue({
queueName: 'testqueue',
connection: 'MyServiceBusConnection',
});
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: serviceBusOutput,
handler: (myTimer, context) => {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
},
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


The following example shows a Service Bus output binding in a *function.json* file and a [PowerShell function](functions-reference-powershell) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "serviceBus",
"direction": "out",
"connection": "AzureServiceBusConnectionString",
"name": "outputSbMsg",
"queueName": "outqueue",
"topicName": "outtopic"
}
]
}
```


Here's the PowerShell that creates a message as the function's output.

```
param($QueueItem, $TriggerMetadata)
Push-OutputBinding -Name outputSbMsg -Value @{
name = $QueueItem.name
employeeId = $QueueItem.employeeId
address = $QueueItem.address
}
```


The following example demonstrates how to write out to a Service Bus topics and Service Bus queues in Python. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

This example shows how to write out to a Service Bus topic.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.route(route="put_message")
@app.service_bus_topic_output(arg_name="message",
connection="AzureServiceBusConnectionString",
topic_name="outTopic")
def main(req: func.HttpRequest, message: func.Out[str]) -> func.HttpResponse:
input_msg = req.params.get('message')
message.set(input_msg)
return 'OK'
```


This example shows how to write out to a Service Bus queue.

```
import azure.functions as func
app = func.FunctionApp()
@app.route(route="put_message")
@app.service_bus_queue_output(
arg_name="msg",
connection="AzureServiceBusConnectionString",
queue_name="outqueue")
def put_message(req: func.HttpRequest, msg: func.Out[str]):
msg.set(req.get_body().decode('utf-8'))
return 'OK'
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the output binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#service-bus-output).

In [C# class libraries](dotnet-isolated-process-guide), use the [ServiceBusOutputAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.ServiceBus/src/ServiceBusOutputAttribute.cs) to define the queue or topic written to by the output.

The following table explains the properties you can set using the attribute:

| Property | Description |
|---|---|
EntityType |
Sets the entity type as either `Queue` for sending messages to a queue or `Topic` when sending messages to a topic. |
QueueOrTopicName |
Name of the topic or queue to send messages to. Use `EntityType` to set the destination type. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `service_bus_topic_output`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the queue or topic message in function code. |
`queue_name` |
Name of the queue. Set only if sending queue messages, not for a topic. |
`topic_name` |
Name of the topic. Set only if sending topic messages, not for a queue. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `ServiceBusQueueOutput`

and `ServiceBusTopicOutput`

annotations are available to write a message as a function output. The parameter decorated with these annotations must be declared as an `OutputBinding<T>`

where `T`

is the type corresponding to the message's type.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `output.serviceBusQueue()`

method.

| Property | Description |
|---|---|
queueName |
Name of the queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

The following table explains the properties that you can set on the `options`

object passed to the `output.serviceBusTopic()`

method.

| Property | Description |
|---|---|
topicName |
Name of the topic. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

The following table explains the binding configuration properties that you set in the *function.json* file and the `ServiceBus`

attribute.

| function.json property | Description |
|---|---|
type |
Must be set to `serviceBus` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the queue or topic message in function code. Set to "$return" to reference the function return value. |
queueName |
Name of the queue. Set only if sending queue messages, not for a topic. |
topicName |
Name of the topic. Set only if sending topic messages, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**accessRights**(v1 only)`manage`

and `listen`

. The default is `manage`

, which indicates that the `connection`

has the **Manage**permission. If you use a connection string that doesn't have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property isn't available because the latest version of the Service Bus SDK doesn't support manage operations.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

All C# modalities and extension versions support the following output parameter types:

| Type | Description |
|---|---|
|
Use when the message to write is simple text. When the parameter value is null when the function exits, Functions doesn't create a message. |
byte[] |
Use for writing binary data messages. When the parameter value is null when the function exits, Functions doesn't create a message. |
Object |
When a message contains JSON, Functions serializes the object into a JSON message payload. When the parameter value is null when the function exits, Functions creates a message with a null object. |

Messaging-specific parameter types contain extra message metadata and aren't compatible with JSON serialization. As a result, it isn't possible to use `ServiceBusMessage`

with the output binding in the isolated model. The specific types supported by the output binding depend on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write a single message, the Service Bus output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message as a string. Use when the message is simple text. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | An object representing the message. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple messages, the Service Bus output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single message types |
An array containing multiple message. Each entry represents one message. |

For other output scenarios, create and use a [ServiceBusClient](/en-us/dotnet/api/azure.messaging.servicebus.servicebusclient) with other types from [Azure.Messaging.ServiceBus](/en-us/dotnet/api/azure.messaging.servicebus) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

In Azure Functions 1.x, the runtime creates the queue if it doesn't exist and you have set `accessRights`

to `manage`

. In Azure Functions version 2.x and higher, the queue or topic must already exist; if you specify a queue or topic that doesn't exist, the function fails.

Use the [Azure Service Bus SDK](../service-bus-messaging/) rather than the built-in output binding.

Output to the Service Bus is available via the `Push-OutputBinding`

cmdlet where you pass arguments that match the name designated by binding's name parameter in the *function.json* file.

The output function parameter must be defined as `func.Out[str]`

or `func.Out[bytes]`

. Refer to the [output example](#example) for details.
Alternatively, you can use the [Azure Service Bus SDK](../service-bus-messaging/) rather than the built-in output binding.

For a complete example, see [the examples section](#example).

## Connections

The `connection`

property is a reference to environment configuration which specifies how the app should connect to Service Bus. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Get the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues#get-the-connection-string). The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name. For example, if you set `connection`

to "MyServiceBus", the Functions runtime looks for an app setting that is named "AzureWebJobsMyServiceBus". If you leave `connection`

empty, the Functions runtime uses the default Service Bus connection string in the app setting that is named "AzureWebJobsServiceBus".

### Identity-based connections

If you are using [version 5.x or higher of the extension](functions-bindings-service-bus?extensionv5), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the `connection`

property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Fully Qualified Namespace | `<CONNECTION_NAME_PREFIX>__fullyQualifiedNamespace` |
The fully qualified Service Bus namespace. | <service_bus_namespace>.servicebus.windows.net |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:fullyQualifiedNamespace`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your topics and queues at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Service Bus extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
Trigger1 |
|

[Azure Service Bus Data Sender](../role-based-access-control/built-in-roles#azure-service-bus-data-sender)1 For triggering from Service Bus topics, the role assignment needs to have effective scope over the Service Bus subscription resource. If only the topic is included, an error will occur. Some clients, such as the Azure portal, don't expose the Service Bus subscription resource as a scope for role assignment. In such cases, the Azure CLI may be used instead. To learn more, see [Azure built-in roles for Azure Service Bus](../service-bus-messaging/service-bus-managed-service-identity#resource-scope).

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Service Bus |
|

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr -->

# Dapr Extension for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr Extension for Azure Functions is a set of tools and services that allow developers to easily integrate Azure Functions with the [Distributed Application Runtime (Dapr)](https://docs.dapr.io/) platform.

Azure Functions is an event-driven compute service that provides a set of [triggers and bindings](functions-triggers-bindings) to easily connect with other Azure services. Dapr provides a set of building blocks and best practices for building distributed applications, including microservices, state management, pub/sub messaging, and more.

With the integration between Dapr and Functions, you can build functions that react to events from Dapr or external systems.

| Action | Direction | Type |
|---|---|---|
| Trigger on a Dapr input binding | N/A |
|

[daprServiceInvocationTrigger](functions-bindings-dapr-trigger-svc-invoke)[daprTopicTrigger](functions-bindings-dapr-trigger-topic)[daprState](functions-bindings-dapr-input-state)[daprSecret](functions-bindings-dapr-input-secret)[daprState](functions-bindings-dapr-output-state)[daprInvoke](functions-bindings-dapr-output-invoke)[daprPublish](functions-bindings-dapr-output-publish)[daprBinding](functions-bindings-dapr-output)## Install extension

The extension NuGet package you install depends on the C# mode [in-process](functions-dotnet-class-library) or [isolated worker process](dotnet-isolated-process-guide) you're using in your function app:

This extension is available by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Dapr), version 1.0.0.

Using the .NET CLI:

```
dotnet add package Microsoft.Azure.WebJobs.Extensions.Dapr
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

## Dapr enablement

You can configure Dapr using various [arguments and annotations][dapr-args] based on the runtime context. You can configure Dapr for Azure Functions through two channels:

- Infrastructure as Code (IaC) templates, as in Bicep or Azure Resource Manager (ARM) templates
- The Azure portal

When using an IaC template, specify the following arguments in the `properties`

section of the container app resource definition.

```
DaprConfig: {
enabled: true
appId: '${envResourceNamePrefix}-funcapp'
appPort: 3001
httpReadBufferSize: ''
httpMaxRequestSize: ''
logLevel: ''
enableApiLogging: true
}
```


The above Dapr configuration values are considered application-scope changes. When you run a container app in multiple-revision mode, changes to these settings won't create a new revision. Instead, all existing revisions are restarted to ensure they're configured with the most up-to-date values.

When configuring Dapr using the Azure portal, navigate to your function app and select **Dapr** from the left-side menu:


## Dapr ports and listeners

When you're triggering a function from Dapr, the extension exposes port `3001`

automatically to listen to incoming requests from the Dapr sidecar.

Important

Port `3001`

is only exposed and listened to if a Dapr trigger is defined in the function app. When using Dapr, the sidecar waits to receive a response from the defined port before completing instantiation. *Do not* define the `dapr.io/port`

annotation or `--app-port`

unless you have a trigger. Doing so may lock your application from the Dapr sidecar.

If you're only using input and output bindings, port `3001`

doesn't need to be exposed or defined.

By default, when Azure Functions tries to communicate with Dapr, it calls Dapr over the port resolved from the environment variable `DAPR_HTTP_PORT`

. If that variable is null, it defaults to port `3500`

.

You can override the Dapr address used by input and output bindings by setting the `DaprAddress`

property in the `function.json`

for the binding (or the attribute). By default, it uses `http://localhost:{DAPR_HTTP_PORT}`

.

The function app still exposes another port and endpoint for things like HTTP triggers, which locally defaults to `7071`

, but in a container, defaults to `80`

.

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An in-process class library is a compiled C# function runs in the same process as the Functions runtime.

The Dapr Extension supports parameter types according to the table below.

| Binding | Parameter types |
|---|---|
| Dapr trigger |
|

[daprState](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/input-bindings.md#state-input-binding)[daprSecret](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/input-bindings.md#state-input-binding)[daprState](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/output-bindings.md#topic-publish-output-binding)[daprInvoke](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/output-bindings.md#service-invocation-output-binding)[daprPublish](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/output-bindings.md#topic-publish-output-binding)[daprBinding](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/output-bindings.md#topic-publish-output-binding)For examples using these types, see [the GitHub repository for the extension](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/dotnet-azurefunction).

## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

`HttpTrigger`

.[Dapr Kafka](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/python-v2-azurefunction#3-dapr-binding)[.NET In-process](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/dotnet-azurefunction)[.NET Isolated](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/dotnet-isolated-azurefunction)## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

`HttpTrigger`

.[Dapr Kafka](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/python-v2-azurefunction#3-dapr-binding)[JavaScript](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/javascript-azurefunction)## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

[Python v1](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/python-azurefunction)[Python v2](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/python-v2-azurefunction)## Troubleshooting

This section describes how to troubleshoot issues that can occur when using the Dapr extension for Azure Functions.

### Ensure Dapr is enabled in your environment

If you're using Dapr bindings and triggers in Azure Functions, and Dapr isn't enabled in your environment, you might receive the error message: `Dapr sidecar isn't present. Please see (https://aka.ms/azure-functions-dapr-sidecar-missing) for more information.`

To enable Dapr in your environment:

If your Azure Function is deployed in Azure Container Apps, refer to

[Dapr enablement instructions for the Dapr extension for Azure Functions](functions-bindings-dapr#dapr-enablement).If your Azure Function is deployed in Kubernetes, verify that your

[deployment's YAML configuration](https://github.com/azure/azure-functions-dapr-extension/blob/master/deploy/kubernetes/kubernetes-deployment.md#sample-kubernetes-deployment)has the following annotations:`annotations: ... dapr.io/enabled: "true" dapr.io/app-id: "functionapp" # You should only set app-port if you are using a Dapr trigger in your code. dapr.io/app-port: "<DAPR_APP_PORT>" ...`

If you're running your Azure Function locally, run the following command to ensure you're

[running the function app with Dapr](https://github.com/azure/azure-functions-dapr-extension/tree/master/samples/python-v2-azurefunction#step-2---run-function-app-with-dapr):`dapr run --app-id functionapp --app-port <DAPR_APP_PORT> --components-path <COMPONENTS_PATH> -- func host start`


### Verify app-port value in Dapr configuration

The Dapr extension for Azure Functions starts an HTTP server on port `3001`

by default. You can configure this port using the [ DAPR_APP_PORT environment variable](https://docs.dapr.io/reference/environment/).

If you provide an incorrect app port value when running an Azure Functions app, you might receive the error message: `The Dapr sidecar is configured to listen on port {portInt}, but the app server is running on port {appPort}. This may cause unexpected behavior. For more information, visit [this link](https://aka.ms/azfunc-dapr-app-config-error).`

To resolve this error message:

In your container app's Dapr settings:

If you're using a Dapr trigger in your code, verify that the app port is set to

`3001`

or to the value of the`DAPR_APP_PORT`

environment variable.If you're

*not*using a Dapr trigger in your code, verify that the app port is*not*set. It should be empty.

Verify that you provide the correct app port value in the Dapr configuration.

If you're using Azure Container Apps, specify the app port in Bicep:

`DaprConfig: { ... appPort: <DAPR_APP_PORT> ... }`

If you're using a Kubernetes environment, set the

`dapr.io/app-port`

annotation:`annotations: ... dapr.io/app-port: "<DAPR_APP_PORT>" ...`

If you're developing locally, verify you set

`--app-port`

when running the function app with Dapr:`dapr run --app-id functionapp --app-port <DAPR_APP_PORT> --components-path <COMPONENTS_PATH> -- func host start`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-hubs -->

# Azure Event Hubs trigger and bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with [Azure Event Hubs](../event-hubs/event-hubs-about) bindings for Azure Functions. Azure Functions supports trigger and output bindings for Event Hubs.

| Action | Type |
|---|---|
| Respond to events sent to an event hub event stream. |
|

[Output binding](functions-bindings-event-hubs-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs), version 6.x.

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

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following options:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Azure.Messaging.EventHubs] is in preview.

**Event Hubs trigger**

When you want the function to process a single event, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

If you are migrating from any older versions of the Event Hubs SDKs, note that this version drops support for the legacy

`Body`

type in favor of [EventBody](/en-us/dotnet/api/azure.messaging.eventhubs.eventdata.eventbody).When you want the function to process a batch of events, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string[]` |
An array of events from the batch, as strings. Each entry represents one event. |
`EventData[]` 1 |
An array of events from the batch, as instances of
|

`T[]`

where `T`

is a JSON serializable type11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventHubs 5.5.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs/5.5.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Event Hubs output binding**

When you want the function to write a single event, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | An object representing the event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventHubProducerClient](/en-us/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) with other types from [Azure.Messaging.EventHubs](/en-us/dotnet/api/azure.messaging.eventhubs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Types for Azure EventHub are in Preview. Follow the [Python SDK Bindings for EventHub Sample](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python) to get started with SDK Types for Event Hubs in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| EventHub trigger |
|

`EventData`

## host.json settings

The [host.json](functions-host-json#eventhub) file contains settings that control behavior for the Event Hubs trigger. The configuration is different depending on the extension version.

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"maxEventBatchSize" : 100,
"minEventBatchSize" : 25,
"maxWaitTime" : "00:05:00",
"batchCheckpointFrequency" : 1,
"prefetchCount" : 300,
"transportType" : "amqpWebSockets",
"webProxy" : "https://proxyserver:8080",
"customEndpointAddress" : "amqps://company.gateway.local",
"targetUnprocessedEventThreshold" : 75,
"initialOffsetOptions" : {
"type" : "fromStart",
"enqueuedTimeUtc" : ""
},
"clientRetryOptions":{
"mode" : "exponential",
"tryTimeout" : "00:01:00",
"delay" : "00:00:00.80",
"maximumDelay" : "00:01:00",
"maximumRetries" : 3
}
}
}
}
```


| Property | Default | Description |
|---|---|---|
maxEventBatchSize2 |
100 | The maximum number of events included in a batch for a single invocation. Must be at least 1. |
minEventBatchSize1 |
1 | The minimum number of events desired in a batch. The minimum applies only when the function is receiving multiple events and must be less than `maxEventBatchSize` .The minimum size isn't strictly guaranteed. A partial batch is dispatched when a full batch can't be prepared before the `maxWaitTime` has elapsed. Partial batches are also likely for the first invocation of the function after scaling takes place. |
maxWaitTime1 |
00:01:00 | The maximum interval that the trigger should wait to fill a batch before invoking the function. The wait time is only considered when `minEventBatchSize` is larger than 1 and is otherwise ignored. If less than `minEventBatchSize` events were available before the wait time elapses, the function is invoked with a partial batch. The longest allowed wait time is 10 minutes.NOTE: This interval is not a strict guarantee for the exact timing on which the function is invoked. There is a small margin of error due to timer precision. When scaling takes place, the first invocation with a partial batch may occur more quickly or may take up to twice the configured wait time. |
| batchCheckpointFrequency | 1 | The number of batches to process before creating a checkpoint for the event hub.NOTE: Setting this value above 1 for hosting plans supported by
|
| prefetchCount | 300 | The number of events that is eagerly requested from Event Hubs and held in a local cache to allow reads to avoid waiting on a network operation |
| transportType | amqpTcp | The protocol and transport that is used for communicating with Event Hubs. Available options: `amqpTcp` , `amqpWebSockets` |
| webProxy | null | The proxy to use for communicating with Event Hubs over web sockets. A proxy cannot be used with the `amqpTcp` transport. |
| customEndpointAddress | null | The address to use when establishing a connection to Event Hubs, allowing network requests to be routed through an application gateway or other path needed for the host environment. The fully qualified namespace for the event hub is still needed when a custom endpoint address is used, and it must be specified explicitly or via the connection string. |
targetUnprocessedEventThreshold1 |
null | The desired number of unprocessed events per function instance. The threshold is used in target-based scaling to override the default scaling threshold inferred from the `maxEventBatchSize` option. When set, the total unprocessed event count is divided by this value to determine the number of function instances needed. The instance count is rounded up to a number that creates a balanced partition distribution. |
| initialOffsetOptions/type | fromStart | The location in the event stream to start processing when a checkpoint does not exist in storage. Applies to all partitions. For more information, see the
`fromStart` , `fromEnd` , `fromEnqueuedTime` |

`initialOffsetOptions/type`

is configured as `fromEnqueuedTime`

, this setting is mandatory. Supports time in any format supported by [DateTime.Parse()](/en-us/dotnet/standard/base-types/parsing-datetime), such as`2020-10-26T20:31Z`

. For clarity, you should also specify a timezone. When timezone isn't specified, Functions assumes the local timezone of the machine running the function app, which is UTC when running on Azure.`exponential`

, `fixed`

1 Using `minEventBatchSize`

and `maxWaitTime`

requires [v5.3.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/5.3.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package, or a later version.

2 The default `maxEventBatchSize`

changed in [v6.0.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/6.0.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package. In earlier versions, this was 10.

The `clientRetryOptions`

are used to retry operations between the Functions host and Event Hubs (such as fetching events and sending events). Refer to guidance on [Azure Functions error handling and retries](functions-bindings-error-pages#retries) for information on applying retry policies to individual functions.

For a reference of host.json in Azure Functions 2.x and beyond, see [host.json reference for Azure Functions](functions-host-json).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-data-explorer-output -->

# Azure Data Explorer output bindings for Azure Functions (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure Data Explorer output binding ingests data to Azure Data Explorer.

For information on setup and configuration details, see the [overview](functions-bindings-azure-data-explorer).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure Data Explorer output binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-outofproc).

This section contains the following examples:

The examples refer to `Product`

class and a corresponding database table:

```
public class Product
{
[JsonProperty(nameof(ProductID))]
public long ProductID { get; set; }
[JsonProperty(nameof(Name))]
public string Name { get; set; }
[JsonProperty(nameof(Cost))]
public double Cost { get; set; }
}
```


```
.create-merge table Products (ProductID:long, Name:string, Cost:double)
```


#### HTTP trigger, write one record

The following example shows a [C# function](functions-dotnet-class-library) that adds a record to a database. The function uses data provided in an HTTP POST request as a JSON body.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples
{
public static class AddProduct
{
[Function("AddProduct")]
[KustoOutput(Database: "productsdb", Connection = "KustoConnectionString", TableName = "Products")]
public static async Task<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "addproductuni")]
HttpRequestData req)
{
Product? prod = await req.ReadFromJsonAsync<Product>();
return prod ?? new Product { };
}
}
}
```


#### HTTP trigger, write records with mapping

The following example shows a [C# function](functions-dotnet-class-library) that adds a collection of records to a database. The function uses mapping that transforms a `Product`

to `Item`

.

To transform data from `Product`

to `Item`

, the function uses a mapping reference:

```
.create-merge table Item (ItemID:long, ItemName:string, ItemCost:float)
-- Create a mapping that transforms an Item to a Product
.create-or-alter table Product ingestion json mapping "item_to_product_json" '[{"column":"ProductID","path":"$.ItemID"},{"column":"Name","path":"$.ItemName"},{"column":"Cost","path":"$.ItemCost"}]'
```


```
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common
{
public class Item
{
public long ItemID { get; set; }
public string? ItemName { get; set; }
public double ItemCost { get; set; }
}
}
```


```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples
{
public static class AddProductsWithMapping
{
[Function("AddProductsWithMapping")]
[KustoOutput(Database: "productsdb", Connection = "KustoConnectionString", TableName = "Products", MappingRef = "item_to_product_json")]
public static async Task<Item> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "addproductswithmapping")]
HttpRequestData req)
{
Item? item = await req.ReadFromJsonAsync<Item>();
return item ?? new Item { };
}
}
}
```


More samples for the Java Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-java).

This section contains the following examples:

The examples refer to a `Products`

class (in a separate file `Product.java`

) and a corresponding database table `Products`

(defined earlier):

```
package com.microsoft.azure.kusto.common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class Product {
@JsonProperty("ProductID")
public long ProductID;
@JsonProperty("Name")
public String Name;
@JsonProperty("Cost")
public double Cost;
public Product() {
}
public Product(long ProductID, String name, double Cost) {
this.ProductID = ProductID;
this.Name = name;
this.Cost = Cost;
}
}
```


### HTTP trigger, write a record to a table

The following example shows an Azure Data Explorer output binding in a Java function that adds a product record to a table. The function uses data provided in an HTTP POST request as a JSON body. The function takes another dependency on the [com.fasterxml.jackson.core](https://github.com/FasterXML/jackson) library to parse the JSON body.

```
<dependency>
<groupId>com.fasterxml.jackson.core</groupId>
<artifactId>jackson-databind</artifactId>
<version>2.13.4.1</version>
</dependency>
```


```
package com.microsoft.azure.kusto.outputbindings;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.OutputBinding;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoOutput;
import com.microsoft.azure.kusto.common.Product;
import java.io.IOException;
import java.util.Optional;
import static com.microsoft.azure.kusto.common.Constants.*;
public class AddProduct {
@FunctionName("AddProduct")
public HttpResponseMessage run(@HttpTrigger(name = "req", methods = {
HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS, route = "addproductuni") HttpRequestMessage<Optional<String>> request,
@KustoOutput(name = "product", database = "productsdb", tableName = "Products", connection = KUSTOCONNSTR) OutputBinding<Product> product)
throws IOException {
if (request.getBody().isPresent()) {
String json = request.getBody().get();
ObjectMapper mapper = new ObjectMapper();
Product p = mapper.readValue(json, Product.class);
product.setValue(p);
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(product)
.build();
} else {
return request.createResponseBuilder(HttpStatus.NO_CONTENT).header("Content-Type", "application/json")
.build();
}
}
}
```


### HTTP trigger, write to two tables

The following example shows an Azure Data Explorer output binding in a Java function that adds records to a database in two different tables (`Product`

and `ProductChangeLog`

). The function uses data provided in an HTTP POST request as a JSON body and multiple output bindings. The function takes another dependency on the [com.fasterxml.jackson.core](https://github.com/FasterXML/jackson) library to parse the JSON body.

```
<dependency>
<groupId>com.fasterxml.jackson.core</groupId>
<artifactId>jackson-databind</artifactId>
<version>2.13.4.1</version>
</dependency>
```


The second table, `ProductsChangeLog`

, corresponds to the following definition:

```
.create-merge table ProductsChangeLog (ProductID:long, CreatedAt:datetime)
```


and Java class in `ProductsChangeLog.java`

:

```
package com.microsoft.azure.kusto.common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class ProductsChangeLog {
@JsonProperty("ProductID")
public long ProductID;
@JsonProperty("CreatedAt")
public String CreatedAt;
public ProductsChangeLog() {
}
public ProductsChangeLog(long ProductID, String CreatedAt) {
this.ProductID = ProductID;
this.CreatedAt = CreatedAt;
}
}
```


```
package com.microsoft.azure.kusto.outputbindings;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.OutputBinding;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoOutput;
import com.microsoft.azure.kusto.common.Product;
import com.microsoft.azure.kusto.common.ProductsChangeLog;
import static com.microsoft.azure.kusto.common.Constants.*;
import java.io.IOException;
import java.time.Clock;
import java.time.Instant;
import java.util.Optional;
public class AddMultiTable {
@FunctionName("AddMultiTable")
public HttpResponseMessage run(@HttpTrigger(name = "req", methods = {
HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS, route = "addmultitable") HttpRequestMessage<Optional<String>> request,
@KustoOutput(name = "product", database = "productsdb", tableName = "Products", connection = KUSTOCONNSTR) OutputBinding<Product> product,
@KustoOutput(name = "productChangeLog", database = "productsdb", tableName = "ProductsChangeLog",
connection = KUSTOCONNSTR) OutputBinding<ProductsChangeLog> productChangeLog)
throws IOException {
if (request.getBody().isPresent()) {
String json = request.getBody().get();
ObjectMapper mapper = new ObjectMapper();
Product p = mapper.readValue(json, Product.class);
product.setValue(p);
productChangeLog.setValue(new ProductsChangeLog(p.ProductID, Instant.now(Clock.systemUTC()).toString()));
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(product)
.build();
} else {
return request.createResponseBuilder(HttpStatus.NO_CONTENT).header("Content-Type", "application/json")
.build();
}
}
}
```


More samples for the Azure Data Explorer output binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-node).

This section contains the following examples:

The examples refer to a database table.

The examples refer to the tables `Products`

and `ProductsChangeLog`

(defined earlier).

### HTTP trigger, write records to a table

The following example shows an Azure Data Explorer output binding in a *function.json* file and a JavaScript function that adds records to a table. The function uses data provided in an HTTP POST request as a JSON body.

The following example is binding data in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"post"
],
"route": "addproduct"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "product",
"type": "kusto",
"database": "productsdb",
"direction": "out",
"tableName": "Products",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
// Insert the product, which will insert it into the Products table.
module.exports = async function (context, req) {
// Note that this expects the body to be a JSON object or array of objects which have a property
// matching each of the columns in the table to insert to.
context.bindings.product = req.body;
return {
status: 201,
body: req.body
};
}
```


### HTTP trigger, write to two tables

The following example shows an Azure Data Explorer output binding in a *function.json* file and a JavaScript function that adds records to a database in two different tables (`Products`

and `ProductsChangeLog`

). The function uses data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `ProductsChangeLog`

, corresponds to the following definition:

```
.create-merge table ProductsChangeLog (ProductID:long, CreatedAt:datetime)
```


The following snippet is binding data in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"post"
],
"route": "addmultitable"
},
{
"name": "res",
"type": "http",
"direction": "out"
},
{
"name": "product",
"type": "kusto",
"database": "productsdb",
"direction": "out",
"tableName": "Products",
"connection": "KustoConnectionString"
},
{
"name": "productchangelog",
"type": "kusto",
"database": "productsdb",
"direction": "out",
"tableName": "ProductsChangeLog",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
module.exports = async function (context, req) {
context.log('JavaScript HTTP trigger and Kusto output binding function processed a request.');
context.log(req.body);
if (req.body) {
var changeLog = {ProductID:req.body.ProductID, CreatedAt: new Date().toISOString()};
context.bindings.product = req.body;
context.bindings.productchangelog = changeLog;
context.res = {
body: req.body,
mimetype: "application/json",
status: 201
}
} else {
context.res = {
status: 400,
body: "Error reading request body"
}
}
}
```


More samples for the Azure Data Explorer output binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python).

This section contains the following examples:

The examples refer to the tables `Products`

and `ProductsChangeLog`

(defined earlier).

### HTTP trigger, write records to a table

The following example shows an Azure Data Explorer output binding in a *function.json* file and a Python function that adds records to a table. The function uses data provided in an HTTP POST request as a JSON body.

The following snippet is binding data in the *function.json* file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "Anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
],
"route": "addproductuni"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"name": "product",
"type": "kusto",
"database": "sdktestsdb",
"direction": "out",
"tableName": "Products",
"connection": "KustoConnectionString"
}
]
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import azure.functions as func
from Common.product import Product
def main(req: func.HttpRequest, product: func.Out[str]) -> func.HttpResponse:
body = str(req.get_body(),'UTF-8')
product.set(body)
return func.HttpResponse(
body=body,
status_code=201,
mimetype="application/json"
)
```


### HTTP trigger, write to two tables

The following example shows an Azure Data Explorer output binding in a *function.json* file and a JavaScript function that adds records to a database in two different tables (`Products`

and `ProductsChangeLog`

). The function uses data provided in an HTTP POST request as a JSON body and multiple output bindings. The second table, `ProductsChangeLog`

, corresponds to the following definition:

```
.create-merge table ProductsChangeLog (ProductID:long, CreatedAt:datetime)
```


The following snippet is binding data in the *function.json* file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "Anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
],
"route": "addmultitable"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"name": "product",
"type": "kusto",
"database": "sdktestsdb",
"direction": "out",
"tableName": "Products",
"connection": "KustoConnectionString"
},
{
"name": "productchangelog",
"type": "kusto",
"database": "sdktestsdb",
"direction": "out",
"tableName": "ProductsChangeLog",
"connection": "KustoConnectionString"
}
]
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import json
from datetime import datetime
import azure.functions as func
from Common.product import Product
def main(req: func.HttpRequest, product: func.Out[str],productchangelog: func.Out[str]) -> func.HttpResponse:
body = str(req.get_body(),'UTF-8')
# parse x:
product.set(body)
id = json.loads(body)["ProductID"]
changelog = {
"ProductID": id,
"CreatedAt": datetime.now().isoformat(),
}
productchangelog.set(json.dumps(changelog))
return func.HttpResponse(
body=body,
status_code=201,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [KustoAttribute](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/src/KustoAttribute.cs) attribute to declare the Azure Data Explorer bindings on the function, which has the following properties.

| Attribute property | Description |
|---|---|
| Database | Required. The database against which the query must be executed. |
| Connection | Required. The name of the variable that holds the connection string, which is resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| TableName | Required. The table to ingest the data into. |
| MappingRef | Optional. Attribute to pass a
|

`multijson/json`

. It can be set to *text*formats supported in the`datasource`

format [enumeration](/en-us/azure/data-explorer/kusto/api/netfx/kusto-ingest-client-reference#enum-datasourceformat). Samples are validated and provided for CSV and JSON formats.## Annotations

The [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) uses the [ @KustoInput](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/java-library/src/main/java/com/microsoft/azure/functions/kusto/annotation/KustoInput.java) annotation (

`com.microsoft.azure.functions.kusto.annotation.KustoOutput`

).| Element | Description |
|---|---|
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, which is resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| tableName | Required. The table to ingest the data into. |
| mappingRef | Optional. Attribute to pass a
|

`multijson/json`

. It can be set to *text*formats supported in the`datasource`

format [enumeration](/en-us/azure/data-explorer/kusto/api/netfx/kusto-ingest-client-reference#enum-datasourceformat). Samples are validated and provided for CSV and JSON formats.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
| type | Required. Must be set to `kusto` . |
| direction | Required. Must be set to `out` . |
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| tableName | Required. The table to ingest the data into. |
| mappingRef | Optional. Attribute to pass a
|

`multijson/json`

. It can be set to *text*formats supported in the`datasource`

format [enumeration](/en-us/azure/data-explorer/kusto/api/netfx/kusto-ingest-client-reference#enum-datasourceformat). Samples are validated and provided for CSV and JSON formats.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The attribute's constructor takes the database and the attributes `TableName`

, `MappingRef`

, and `DataFormat`

and the connection setting name. The KQL command can be a KQL statement or a KQL function. The connection string setting name corresponds to the application setting (in `local.settings.json`

for local development) that contains the [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For example:`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId`

. Queries executed by the input binding are parameterized. The values provided in the KQL parameters are used at runtime.

Important

For optimal security, your function app should use managed identities when connecting to Azure Data Explorer instead of using a connection string, which contains keys. For more information, see [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For mananaged identity-based connections, you must set the `managedServiceIdentity`

property in the binding definition.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-data-explorer-output -->

# Azure Data Explorer output bindings for Azure Functions (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure Data Explorer output binding ingests data to Azure Data Explorer.

For information on setup and configuration details, see the [overview](functions-bindings-azure-data-explorer).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure Data Explorer output binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-outofproc).

This section contains the following examples:

The examples refer to `Product`

class and a corresponding database table:

```
public class Product
{
[JsonProperty(nameof(ProductID))]
public long ProductID { get; set; }
[JsonProperty(nameof(Name))]
public string Name { get; set; }
[JsonProperty(nameof(Cost))]
public double Cost { get; set; }
}
```


```
.create-merge table Products (ProductID:long, Name:string, Cost:double)
```


#### HTTP trigger, write one record

The following example shows a [C# function](functions-dotnet-class-library) that adds a record to a database. The function uses data provided in an HTTP POST request as a JSON body.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples
{
public static class AddProduct
{
[Function("AddProduct")]
[KustoOutput(Database: "productsdb", Connection = "KustoConnectionString", TableName = "Products")]
public static async Task<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "addproductuni")]
HttpRequestData req)
{
Product? prod = await req.ReadFromJsonAsync<Product>();
return prod ?? new Product { };
}
}
}
```


#### HTTP trigger, write records with mapping

The following example shows a [C# function](functions-dotnet-class-library) that adds a collection of records to a database. The function uses mapping that transforms a `Product`

to `Item`

.

To transform data from `Product`

to `Item`

, the function uses a mapping reference:

```
.create-merge table Item (ItemID:long, ItemName:string, ItemCost:float)
-- Create a mapping that transforms an Item to a Product
.create-or-alter table Product ingestion json mapping "item_to_product_json" '[{"column":"ProductID","path":"$.ItemID"},{"column":"Name","path":"$.ItemName"},{"column":"Cost","path":"$.ItemCost"}]'
```


```
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common
{
public class Item
{
public long ItemID { get; set; }
public string? ItemName { get; set; }
public double ItemCost { get; set; }
}
}
```


```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples
{
public static class AddProductsWithMapping
{
[Function("AddProductsWithMapping")]
[KustoOutput(Database: "productsdb", Connection = "KustoConnectionString", TableName = "Products", MappingRef = "item_to_product_json")]
public static async Task<Item> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "addproductswithmapping")]
HttpRequestData req)
{
Item? item = await req.ReadFromJsonAsync<Item>();
return item ?? new Item { };
}
}
}
```


More samples for the Java Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-java).

This section contains the following examples:

The examples refer to a `Products`

class (in a separate file `Product.java`

) and a corresponding database table `Products`

(defined earlier):

```
package com.microsoft.azure.kusto.common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class Product {
@JsonProperty("ProductID")
public long ProductID;
@JsonProperty("Name")
public String Name;
@JsonProperty("Cost")
public double Cost;
public Product() {
}
public Product(long ProductID, String name, double Cost) {
this.ProductID = ProductID;
this.Name = name;
this.Cost = Cost;
}
}
```


### HTTP trigger, write a record to a table

The following example shows an Azure Data Explorer output binding in a Java function that adds a product record to a table. The function uses data provided in an HTTP POST request as a JSON body. The function takes another dependency on the [com.fasterxml.jackson.core](https://github.com/FasterXML/jackson) library to parse the JSON body.

```
<dependency>
<groupId>com.fasterxml.jackson.core</groupId>
<artifactId>jackson-databind</artifactId>
<version>2.13.4.1</version>
</dependency>
```


```
package com.microsoft.azure.kusto.outputbindings;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.OutputBinding;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoOutput;
import com.microsoft.azure.kusto.common.Product;
import java.io.IOException;
import java.util.Optional;
import static com.microsoft.azure.kusto.common.Constants.*;
public class AddProduct {
@FunctionName("AddProduct")
public HttpResponseMessage run(@HttpTrigger(name = "req", methods = {
HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS, route = "addproductuni") HttpRequestMessage<Optional<String>> request,
@KustoOutput(name = "product", database = "productsdb", tableName = "Products", connection = KUSTOCONNSTR) OutputBinding<Product> product)
throws IOException {
if (request.getBody().isPresent()) {
String json = request.getBody().get();
ObjectMapper mapper = new ObjectMapper();
Product p = mapper.readValue(json, Product.class);
product.setValue(p);
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(product)
.build();
} else {
return request.createResponseBuilder(HttpStatus.NO_CONTENT).header("Content-Type", "application/json")
.build();
}
}
}
```


### HTTP trigger, write to two tables

The following example shows an Azure Data Explorer output binding in a Java function that adds records to a database in two different tables (`Product`

and `ProductChangeLog`

). The function uses data provided in an HTTP POST request as a JSON body and multiple output bindings. The function takes another dependency on the [com.fasterxml.jackson.core](https://github.com/FasterXML/jackson) library to parse the JSON body.

```
<dependency>
<groupId>com.fasterxml.jackson.core</groupId>
<artifactId>jackson-databind</artifactId>
<version>2.13.4.1</version>
</dependency>
```


The second table, `ProductsChangeLog`

, corresponds to the following definition:

```
.create-merge table ProductsChangeLog (ProductID:long, CreatedAt:datetime)
```


and Java class in `ProductsChangeLog.java`

:

```
package com.microsoft.azure.kusto.common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class ProductsChangeLog {
@JsonProperty("ProductID")
public long ProductID;
@JsonProperty("CreatedAt")
public String CreatedAt;
public ProductsChangeLog() {
}
public ProductsChangeLog(long ProductID, String CreatedAt) {
this.ProductID = ProductID;
this.CreatedAt = CreatedAt;
}
}
```


```
package com.microsoft.azure.kusto.outputbindings;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.OutputBinding;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoOutput;
import com.microsoft.azure.kusto.common.Product;
import com.microsoft.azure.kusto.common.ProductsChangeLog;
import static com.microsoft.azure.kusto.common.Constants.*;
import java.io.IOException;
import java.time.Clock;
import java.time.Instant;
import java.util.Optional;
public class AddMultiTable {
@FunctionName("AddMultiTable")
public HttpResponseMessage run(@HttpTrigger(name = "req", methods = {
HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS, route = "addmultitable") HttpRequestMessage<Optional<String>> request,
@KustoOutput(name = "product", database = "productsdb", tableName = "Products", connection = KUSTOCONNSTR) OutputBinding<Product> product,
@KustoOutput(name = "productChangeLog", database = "productsdb", tableName = "ProductsChangeLog",
connection = KUSTOCONNSTR) OutputBinding<ProductsChangeLog> productChangeLog)
throws IOException {
if (request.getBody().isPresent()) {
String json = request.getBody().get();
ObjectMapper mapper = new ObjectMapper();
Product p = mapper.readValue(json, Product.class);
product.setValue(p);
productChangeLog.setValue(new ProductsChangeLog(p.ProductID, Instant.now(Clock.systemUTC()).toString()));
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(product)
.build();
} else {
return request.createResponseBuilder(HttpStatus.NO_CONTENT).header("Content-Type", "application/json")
.build();
}
}
}
```


More samples for the Azure Data Explorer output binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-node).

This section contains the following examples:

The examples refer to a database table.

The examples refer to the tables `Products`

and `ProductsChangeLog`

(defined earlier).

### HTTP trigger, write records to a table

The following example shows an Azure Data Explorer output binding in a *function.json* file and a JavaScript function that adds records to a table. The function uses data provided in an HTTP POST request as a JSON body.

The following example is binding data in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"post"
],
"route": "addproduct"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "product",
"type": "kusto",
"database": "productsdb",
"direction": "out",
"tableName": "Products",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
// Insert the product, which will insert it into the Products table.
module.exports = async function (context, req) {
// Note that this expects the body to be a JSON object or array of objects which have a property
// matching each of the columns in the table to insert to.
context.bindings.product = req.body;
return {
status: 201,
body: req.body
};
}
```


### HTTP trigger, write to two tables

The following example shows an Azure Data Explorer output binding in a *function.json* file and a JavaScript function that adds records to a database in two different tables (`Products`

and `ProductsChangeLog`

). The function uses data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `ProductsChangeLog`

, corresponds to the following definition:

```
.create-merge table ProductsChangeLog (ProductID:long, CreatedAt:datetime)
```


The following snippet is binding data in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"post"
],
"route": "addmultitable"
},
{
"name": "res",
"type": "http",
"direction": "out"
},
{
"name": "product",
"type": "kusto",
"database": "productsdb",
"direction": "out",
"tableName": "Products",
"connection": "KustoConnectionString"
},
{
"name": "productchangelog",
"type": "kusto",
"database": "productsdb",
"direction": "out",
"tableName": "ProductsChangeLog",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
module.exports = async function (context, req) {
context.log('JavaScript HTTP trigger and Kusto output binding function processed a request.');
context.log(req.body);
if (req.body) {
var changeLog = {ProductID:req.body.ProductID, CreatedAt: new Date().toISOString()};
context.bindings.product = req.body;
context.bindings.productchangelog = changeLog;
context.res = {
body: req.body,
mimetype: "application/json",
status: 201
}
} else {
context.res = {
status: 400,
body: "Error reading request body"
}
}
}
```


More samples for the Azure Data Explorer output binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python).

This section contains the following examples:

The examples refer to the tables `Products`

and `ProductsChangeLog`

(defined earlier).

### HTTP trigger, write records to a table

The following example shows an Azure Data Explorer output binding in a *function.json* file and a Python function that adds records to a table. The function uses data provided in an HTTP POST request as a JSON body.

The following snippet is binding data in the *function.json* file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "Anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
],
"route": "addproductuni"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"name": "product",
"type": "kusto",
"database": "sdktestsdb",
"direction": "out",
"tableName": "Products",
"connection": "KustoConnectionString"
}
]
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import azure.functions as func
from Common.product import Product
def main(req: func.HttpRequest, product: func.Out[str]) -> func.HttpResponse:
body = str(req.get_body(),'UTF-8')
product.set(body)
return func.HttpResponse(
body=body,
status_code=201,
mimetype="application/json"
)
```


### HTTP trigger, write to two tables

The following example shows an Azure Data Explorer output binding in a *function.json* file and a JavaScript function that adds records to a database in two different tables (`Products`

and `ProductsChangeLog`

). The function uses data provided in an HTTP POST request as a JSON body and multiple output bindings. The second table, `ProductsChangeLog`

, corresponds to the following definition:

```
.create-merge table ProductsChangeLog (ProductID:long, CreatedAt:datetime)
```


The following snippet is binding data in the *function.json* file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "Anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
],
"route": "addmultitable"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"name": "product",
"type": "kusto",
"database": "sdktestsdb",
"direction": "out",
"tableName": "Products",
"connection": "KustoConnectionString"
},
{
"name": "productchangelog",
"type": "kusto",
"database": "sdktestsdb",
"direction": "out",
"tableName": "ProductsChangeLog",
"connection": "KustoConnectionString"
}
]
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import json
from datetime import datetime
import azure.functions as func
from Common.product import Product
def main(req: func.HttpRequest, product: func.Out[str],productchangelog: func.Out[str]) -> func.HttpResponse:
body = str(req.get_body(),'UTF-8')
# parse x:
product.set(body)
id = json.loads(body)["ProductID"]
changelog = {
"ProductID": id,
"CreatedAt": datetime.now().isoformat(),
}
productchangelog.set(json.dumps(changelog))
return func.HttpResponse(
body=body,
status_code=201,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [KustoAttribute](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/src/KustoAttribute.cs) attribute to declare the Azure Data Explorer bindings on the function, which has the following properties.

| Attribute property | Description |
|---|---|
| Database | Required. The database against which the query must be executed. |
| Connection | Required. The name of the variable that holds the connection string, which is resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| TableName | Required. The table to ingest the data into. |
| MappingRef | Optional. Attribute to pass a
|

`multijson/json`

. It can be set to *text*formats supported in the`datasource`

format [enumeration](/en-us/azure/data-explorer/kusto/api/netfx/kusto-ingest-client-reference#enum-datasourceformat). Samples are validated and provided for CSV and JSON formats.## Annotations

The [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) uses the [ @KustoInput](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/java-library/src/main/java/com/microsoft/azure/functions/kusto/annotation/KustoInput.java) annotation (

`com.microsoft.azure.functions.kusto.annotation.KustoOutput`

).| Element | Description |
|---|---|
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, which is resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| tableName | Required. The table to ingest the data into. |
| mappingRef | Optional. Attribute to pass a
|

`multijson/json`

. It can be set to *text*formats supported in the`datasource`

format [enumeration](/en-us/azure/data-explorer/kusto/api/netfx/kusto-ingest-client-reference#enum-datasourceformat). Samples are validated and provided for CSV and JSON formats.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
| type | Required. Must be set to `kusto` . |
| direction | Required. Must be set to `out` . |
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| tableName | Required. The table to ingest the data into. |
| mappingRef | Optional. Attribute to pass a
|

`multijson/json`

. It can be set to *text*formats supported in the`datasource`

format [enumeration](/en-us/azure/data-explorer/kusto/api/netfx/kusto-ingest-client-reference#enum-datasourceformat). Samples are validated and provided for CSV and JSON formats.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The attribute's constructor takes the database and the attributes `TableName`

, `MappingRef`

, and `DataFormat`

and the connection setting name. The KQL command can be a KQL statement or a KQL function. The connection string setting name corresponds to the application setting (in `local.settings.json`

for local development) that contains the [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For example:`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId`

. Queries executed by the input binding are parameterized. The values provided in the KQL parameters are used at runtime.

Important

For optimal security, your function app should use managed identities when connecting to Azure Data Explorer instead of using a connection string, which contains keys. For more information, see [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For mananaged identity-based connections, you must set the `managedServiceIdentity`

property in the binding definition.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-hubs-trigger -->

# Azure Event Hubs trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with [Azure Event Hubs](../event-hubs/event-hubs-about) trigger for Azure Functions. Azure Functions supports trigger and [output bindings](functions-bindings-event-hubs-output) for Event Hubs.

For information on setup and configuration details, see the [overview](functions-bindings-event-hubs).

Use the function trigger to respond to an event sent to an event hub event stream. You need read access to the underlying event hub to set up the trigger. When the function is triggered, the message passed to the function is typed as a string.

Event Hubs scaling decisions for the Consumption and Premium plans are done via Target Based Scaling. For more information, see [Target Based Scaling](functions-target-based-scaling).

For information about how Azure Functions responds to events sent to an event hub event stream using triggers, see [Integrate Event Hubs with serverless functions on Azure](/en-us/azure/architecture/serverless/event-hubs-functions/event-hubs-functions#consuming-events-with-azure-functions).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

The following example shows a [C# function](dotnet-isolated-process-guide) that is triggered based on an event hub, where the input message string is written to the logs:

```
{
private readonly ILogger<EventHubsFunction> _logger;
public EventHubsFunction(ILogger<EventHubsFunction> logger)
{
_logger = logger;
}
[Function(nameof(EventHubFunction))]
[FixedDelayRetry(5, "00:00:10")]
[EventHubOutput("dest", Connection = "EventHubConnection")]
public string EventHubFunction(
[EventHubTrigger("src", Connection = "EventHubConnection")] string[] input,
FunctionContext context)
{
_logger.LogInformation("First Event Hubs triggered message: {msg}", input[0]);
var message = $"Output message created at {DateTime.Now}";
return message;
}
```


The following example shows an Event Hubs trigger [TypeScript function](functions-reference-node?tabs=typescript). The function reads [event metadata](#event-metadata) and logs the message.

```
import { app, InvocationContext } from '@azure/functions';
export async function eventHubTrigger1(message: unknown, context: InvocationContext): Promise<void> {
context.log('Event hub function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('SequenceNumber =', context.triggerMetadata.sequenceNumber);
context.log('Offset =', context.triggerMetadata.offset);
}
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'one',
handler: eventHubTrigger1,
});
```


To receive events in a batch, set `cardinality`

to `many`

, as shown in the following example.

```
import { app, InvocationContext } from '@azure/functions';
export async function eventHubTrigger1(messages: unknown[], context: InvocationContext): Promise<void> {
context.log(`Event hub function processed ${messages.length} messages`);
for (let i = 0; i < messages.length; i++) {
context.log('Event hub message:', messages[i]);
context.log(`EnqueuedTimeUtc = ${context.triggerMetadata.enqueuedTimeUtcArray[i]}`);
context.log(`SequenceNumber = ${context.triggerMetadata.sequenceNumberArray[i]}`);
context.log(`Offset = ${context.triggerMetadata.offsetArray[i]}`);
}
}
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'many',
handler: eventHubTrigger1,
});
```


The following example shows an Event Hubs trigger [JavaScript function](functions-reference-node). The function reads [event metadata](#event-metadata) and logs the message.

```
const { app } = require('@azure/functions');
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'one',
handler: (message, context) => {
context.log('Event hub function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('SequenceNumber =', context.triggerMetadata.sequenceNumber);
context.log('Offset =', context.triggerMetadata.offset);
},
});
```


To receive events in a batch, set `cardinality`

to `many`

, as shown in the following example.

```
const { app } = require('@azure/functions');
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'many',
handler: (messages, context) => {
context.log(`Event hub function processed ${messages.length} messages`);
for (let i = 0; i < messages.length; i++) {
context.log('Event hub message:', messages[i]);
context.log(`EnqueuedTimeUtc = ${context.triggerMetadata.enqueuedTimeUtcArray[i]}`);
context.log(`SequenceNumber = ${context.triggerMetadata.sequenceNumberArray[i]}`);
context.log(`Offset = ${context.triggerMetadata.offsetArray[i]}`);
}
},
});
```


Here's the PowerShell code:

```
param($eventHubMessages, $TriggerMetadata)
Write-Host "PowerShell eventhub trigger function called for message array: $eventHubMessages"
$eventHubMessages | ForEach-Object { Write-Host "Processed message: $_" }
```


This example uses SDK types to directly access the underlying [ EventData](/en-us/python/api/azure-eventhub/azure.eventhub.eventdata) object provided by the Event Hubs trigger:

The function reads the event body and logs it.

```
import logging
import azure.functions as func
import azurefunctions.extensions.bindings.eventhub as eh
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.event_hub_message_trigger(
arg_name="event", event_hub_name="EVENTHUB_NAME", connection="EventHubConnection"
)
def eventhub_trigger(event: eh.EventData):
logging.info(
"Python EventHub trigger processed an event %s",
event.body_as_str()
)
```


For examples of using the EventData type, see the [ EventData](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-eventhub/samples/eventhub_samples_eventdata/function_app.py) samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the

[Python SDK Bindings for Event Hubs Sample](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python).

Note

Known limitations include:

- The
`enqueued_time`

property is not supported. - Batch message support is supported with runtime version 4.1039 or greater.

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

The following example shows an Event Hubs trigger binding and a Python function that uses the binding. The function reads [event metadata](#event-metadata) and logs the message. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="EventHubTrigger1")
@app.event_hub_message_trigger(arg_name="myhub",
event_hub_name="<EVENT_HUB_NAME>",
connection="<CONNECTION_SETTING>")
def test_function(myhub: func.EventHubEvent):
logging.info('Python EventHub trigger processed an event: %s',
myhub.get_body().decode('utf-8'))
```


The following example shows an Event Hubs trigger binding which logs the message body of the Event Hubs trigger.

```
@FunctionName("ehprocessor")
public void eventHubProcessor(
@EventHubTrigger(name = "msg",
eventHubName = "myeventhubname",
connection = "myconnvarname") String message,
final ExecutionContext context )
{
context.getLogger().info(message);
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `EventHubTrigger`

annotation on parameters whose value comes from the event hub. Parameters with these annotations cause the function to run when an event arrives. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

The following example illustrates extensive use of `SystemProperties`

and other Binding options for further introspection of the Event along with providing a well-formed `BlobOutput`

path that is Date hierarchical.

```
package com.example;
import java.util.Map;
import java.time.ZonedDateTime;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
/**
* Azure Functions with Event Hub trigger.
* and Blob Output using date in path along with message partition ID
* and message sequence number from EventHub Trigger Properties
*/
public class EventHubReceiver {
@FunctionName("EventHubReceiver")
@StorageAccount("bloboutput")
public void run(
@EventHubTrigger(name = "message",
eventHubName = "%eventhub%",
consumerGroup = "%consumergroup%",
connection = "eventhubconnection",
cardinality = Cardinality.ONE)
String message,
final ExecutionContext context,
@BindingName("Properties") Map<String, Object> properties,
@BindingName("SystemProperties") Map<String, Object> systemProperties,
@BindingName("PartitionContext") Map<String, Object> partitionContext,
@BindingName("EnqueuedTimeUtc") Object enqueuedTimeUtc,
@BlobOutput(
name = "outputItem",
path = "iotevents/{datetime:yy}/{datetime:MM}/{datetime:dd}/{datetime:HH}/" +
"{datetime:mm}/{PartitionContext.PartitionId}/{SystemProperties.SequenceNumber}.json")
OutputBinding<String> outputItem) {
var et = ZonedDateTime.parse(enqueuedTimeUtc + "Z"); // needed as the UTC time presented does not have a TZ
// indicator
context.getLogger().info("Event hub message received: " + message + ", properties: " + properties);
context.getLogger().info("Properties: " + properties);
context.getLogger().info("System Properties: " + systemProperties);
context.getLogger().info("partitionContext: " + partitionContext);
context.getLogger().info("EnqueuedTimeUtc: " + et);
outputItem.setValue(message);
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to configure the trigger. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-hubs-trigger).

Use the `EventHubTriggerAttribute`

to define a trigger on an event hub, which supports the following properties.

| Parameters | Description |
|---|---|
EventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced in
`%eventHubName%` |

**ConsumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. When omitted, the`$Default`

consumer group is used.**Connection**[Connections](#connections).## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `event_hub_message_trigger`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the event item in function code. |
`event_hub_name` |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [EventHubTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhubtrigger) annotation, which supports the following settings:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.eventHub()`

method.

| Property | Description |
|---|---|
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**cardinality**`many`

in order to enable batching. If omitted or set to `one`

, a single message is passed to the function.**connection**[Connections](#connections).The following table explains the trigger configuration properties that you set in the *function.json* file, which differs by runtime version.

| function.json property | Description |
|---|---|
type |
Must be set to `eventHubTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the event item in function code. |
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**cardinality**`many`

in order to enable batching. If omitted or set to `one`

, a single message is passed to the function.**connection**[Connections](#connections).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

To learn more about how Event Hubs trigger and IoT Hub trigger scales, see [Consuming Events with Azure Functions](/en-us/azure/architecture/serverless/event-hubs-functions/event-hubs-functions#consuming-events-with-azure-functions).

Functions also supports Python SDK type bindings for Azure Event Hubs, which lets you work with data using these underlying SDK types:

Important

Support for Event Hubs SDK types in Python is in Preview and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

The parameter type supported by the Event Hubs output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single event, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

If you are migrating from any older versions of the Event Hubs SDKs, note that this version drops support for the legacy

`Body`

type in favor of [EventBody](/en-us/dotnet/api/azure.messaging.eventhubs.eventdata.eventbody).When you want the function to process a batch of events, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string[]` |
An array of events from the batch, as strings. Each entry represents one event. |
`EventData[]` 1 |
An array of events from the batch, as instances of
|

`T[]`

where `T`

is a JSON serializable type11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventHubs 5.5.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs/5.5.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

The parameter type can be one of the following:

- Any native Java types such as int, String, byte[].
- Nullable values using Optional.
- Any POJO type.

To learn more, see the [EventHubTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhubtrigger) reference.

## Event metadata

The Event Hubs trigger provides several [metadata properties](functions-bindings-expressions-patterns). Metadata properties can be used as part of binding expressions in other bindings or as parameters in your code. The properties come from the [EventData](/en-us/dotnet/api/microsoft.servicebus.messaging.eventdata) class.

| Property | Type | Description |
|---|---|---|
`PartitionContext` |
|

`PartitionContext`

instance.`EnqueuedTimeUtc`

`DateTime`

`Offset`

`string`

`PartitionKey`

`string`

`Properties`

`IDictionary<String,Object>`

`SequenceNumber`

`Int64`

`SystemProperties`

`IDictionary<String,Object>`

See [code examples](#example) that use these properties earlier in this article.

## Connections

The `connection`

property is a reference to environment configuration which specifies how the app should connect to Event Hubs. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

Obtain this connection string by clicking the **Connection Information** button for the [namespace](../event-hubs/event-hubs-create#create-an-event-hubs-namespace), not the event hub itself. The connection string must be for an Event Hubs namespace, not the event hub itself.

When used for triggers, the connection string must have at least "read" permissions to activate the function. When used for output bindings, the connection string must have "send" permissions to send messages to the event stream.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

### Identity-based connections

If you are using [version 5.x or higher of the extension](functions-bindings-event-hubs?tabs=extensionv5), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the `connection`

property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Fully Qualified Namespace | `<CONNECTION_NAME_PREFIX>__fullyQualifiedNamespace` |
The fully qualified Event Hubs namespace. | `myeventhubns.servicebus.windows.net` |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:fullyQualifiedNamespace`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You will need to create a role assignment that provides access to your event hub at runtime. The scope of the role assignment can be for an Event Hubs namespace, or the event hub itself. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Event Hubs extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
|

[Azure Event Hubs Data Sender](../role-based-access-control/built-in-roles#azure-event-hubs-data-sender)## host.json settings

The [host.json](functions-host-json#eventhub) file contains settings that control Event Hubs trigger behavior. See the [host.json settings](functions-bindings-event-hubs#hostjson-settings) section for details regarding available settings.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/dotnet-aspire-integration -->

# Azure Functions with Aspire

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Aspire](/en-us/dotnet/aspire/get-started/aspire-overview) is an opinionated stack that simplifies development of distributed applications in the cloud. The integration of Aspire with Azure Functions enables you to develop, debug, and orchestrate an Azure Functions .NET project as part of the Aspire app host.

## Prerequisites

Set up your development environment for using Azure Functions with Aspire:

[Install the Aspire Prerequisites](/en-us/dotnet/aspire/fundamentals/setup-tooling#install-aspire-prerequisites).- Full support for the Azure Functions integration requires Aspire 13.1 or later. Aspire 13.0 also includes a preview version of
`Aspire.Hosting.Azure.Functions`

which acts as a release candidate with go-live support.

- Full support for the Azure Functions integration requires Aspire 13.1 or later. Aspire 13.0 also includes a preview version of
- Install the
[Azure Functions Core Tools](functions-run-local).

If you use Visual Studio, update to version 17.12 or later. You must also have the latest version of the Azure Functions tools for Visual Studio. To check for updates:

- Go to
**Tools**>**Options**. - Under
**Projects and Solutions**, select**Azure Functions**. - Select
**Check for updates**and install updates as prompted.

## Solution structure

A solution that uses Azure Functions and Aspire has multiple projects, including an [app host project](/en-us/dotnet/aspire/fundamentals/app-host-overview) and one or more Functions projects.

The app host project is the entry point for your application. It orchestrates the setup of the components of your application, including the Functions project.

The solution typically also includes a *service defaults* project. This project provides a set of default services and configurations to be used across projects in your application.

### App host project

To successfully configure the integration, make sure that the app host project meets the following requirements:

- The app host project must reference
[Aspire.Hosting.Azure.Functions](https://www.nuget.org/packages/Aspire.Hosting.Azure.Functions). This package defines the necessary logic for the integration. - The app host project needs to have a project reference for each Functions project that you want to include in the orchestration.
- In the app host's
`AppHost.cs`

file, you must include the project by calling`AddAzureFunctionsProject<TProject>()`

on your`IDistributedApplicationBuilder`

instance. You use this method instead of using the`AddProject<TProject>()`

method that you use for other project types in Aspire. If you use`AddProject<TProject>()`

, the Functions project can't start properly.

The following example shows a minimal `AppHost.cs`

file for an app host project:

```
var builder = DistributedApplication.CreateBuilder(args);
builder.AddAzureFunctionsProject<Projects.MyFunctionsProject>("MyFunctionsProject");
builder.Build().Run();
```


### Azure Functions project

To successfully configure the integration, make sure that the Azure Functions project meets the following requirements:

The Functions project must reference the

[2.x versions](dotnet-isolated-process-guide#version-2x)of[Microsoft.Azure.Functions.Worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker/)and[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk/). You must also update any[Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore/)references to the 2.x version.Your

`Program.cs`

file must use the`IHostApplicationBuilder`

version of the[host instance startup](dotnet-isolated-process-guide#start-up-and-configuration). This requirement means that you must use`FunctionsApplication.CreateBuilder(args)`

.If your solution includes a service defaults project, ensure that your Functions project is configured to use it:

- The Functions project should include a project reference to the service defaults project.
- Before you build
`IHostApplicationBuilder`

in`Program.cs`

, include a call to`builder.AddServiceDefaults()`

.


The following example shows a minimal `Program.cs`

file for a Functions project used in Aspire:

```
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.Hosting;
var builder = FunctionsApplication.CreateBuilder(args);
builder.AddServiceDefaults();
builder.ConfigureFunctionsWebApplication();
builder.Build().Run();
```


This example doesn't include the default Application Insights configuration that appears in many other `Program.cs`

examples and in the Azure Functions templates. Instead, you configure OpenTelemetry integration in Aspire by calling the `builder.AddServiceDefaults`

method.

To get the most out of the integration, consider the following guidelines:

- Don't include any direct Application Insights integrations in the Functions project. Monitoring in Aspire is instead handled through its OpenTelemetry support. You can configure Aspire to export data to Azure Monitor through the service defaults project.
- Don't define custom app settings in the
`local.settings.json`

file for the Functions project. The only setting that should be in`local.settings.json`

is`"FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated"`

. Set all other app configurations through the app host project.

## Connection configuration with Aspire

The app host project defines resources and helps you create connections between them by using code. This section shows how to configure and customize connections that your Azure Functions project uses.

Aspire includes default connection permissions that can help you get started. However, these permissions might not be appropriate or sufficient for your application.

For scenarios that use Azure role-based access control (RBAC), you can customize permissions by calling the `WithRoleAssignments()`

method on the project resource. When you call `WithRoleAssignments()`

, all default role assignments are removed, and you must explicitly define the full set role assignments that you want. If you host your application on Azure Container Apps, using `WithRoleAssignments()`

also requires that you call `AddAzureContainerAppEnvironment()`

on `DistributedApplicationBuilder`

.

### Azure Functions host storage

Azure Functions requires a [host storage connection ( AzureWebJobsStorage)](functions-reference#connecting-to-host-storage-with-an-identity) for several of its core behaviors. When you call

`AddAzureFunctionsProject<TProject>()`

in your app host project, an `AzureWebJobsStorage`

connection is created by default and provided to the Functions project. This default connection uses the Azure Storage emulator for local development runs and automatically provisions a storage account when it's deployed. For more control, you can replace this connection by calling `.WithHostStorage()`

on the Functions project resource.The default permissions that Aspire sets for the host storage connection depends on whether you call `WithHostStorage()`

or not. Adding `WithHostStorage()`

removes a [Storage Account Contributor](../role-based-access-control/built-in-roles#storage-account-contributor) assignment. The following table lists the default permissions that Aspire sets for the host storage connection:

| Host storage connection | Default roles |
|---|---|
No call to `WithHostStorage()` |
|

`WithHostStorage()`

[Storage Blob Data Contributor](../role-based-access-control/built-in-roles#storage-blob-data-contributor),[Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor),[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)The following example shows a minimal `AppHost.cs`

file for an app host project that replaces the host storage and specifies a role assignment:

```
using Azure.Provisioning.Storage;
var builder = DistributedApplication.CreateBuilder(args);
builder.AddAzureContainerAppEnvironment("myEnv");
var myHostStorage = builder.AddAzureStorage("myHostStorage");
builder.AddAzureFunctionsProject<Projects.MyFunctionsProject>("MyFunctionsProject")
.WithHostStorage(myHostStorage)
.WithRoleAssignments(myHostStorage, StorageBuiltInRole.StorageBlobDataOwner);
builder.Build().Run();
```


Note

[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner) is the role that we recommend for the [basic needs of the host storage connection](functions-reference#connecting-to-host-storage-with-an-identity). Your app might encounter problems if the connection to the blob service has only the Aspire default of [Storage Blob Data Contributor](../role-based-access-control/built-in-roles#storage-blob-data-contributor).

For production scenarios, include calls to both `WithHostStorage()`

and `WithRoleAssignments()`

. You can then set this role explicitly, along with any others that you need.

### Trigger and binding connections

Your triggers and bindings reference connections by name. The following Aspire integrations provide these connections through a call to `WithReference()`

on the project resource:

The following example shows a minimal `AppHost.cs`

file for an app host project that configures a queue trigger. In this example, the corresponding queue trigger has its `Connection`

property set to `MyQueueTriggerConnection`

, so the call to `WithReference()`

specifies the name.

```
var builder = DistributedApplication.CreateBuilder(args);
var myAppStorage = builder.AddAzureStorage("myAppStorage").RunAsEmulator();
var queues = myAppStorage.AddQueues("queues");
builder.AddAzureFunctionsProject<Projects.MyFunctionsProject>("MyFunctionsProject")
.WithReference(queues, "MyQueueTriggerConnection");
builder.Build().Run();
```


For other integrations, calls to `WithReference`

set the configuration in a different way. They make the configuration available to [Aspire client integrations](/en-us/dotnet/aspire/fundamentals/integrations-overview#client-integrations), but not to triggers and bindings. For these integrations, call `WithEnvironment()`

to pass the connection information for the trigger or binding to resolve.

The following example shows how to set the environment variable `MyBindingConnection`

for a resource that exposes a connection string expression:

```
builder.AddAzureFunctionsProject<Projects.MyFunctionsProject>("MyFunctionsProject")
.WithEnvironment("MyBindingConnection", otherIntegration.Resource.ConnectionStringExpression);
```


If you want both Aspire client integrations and the system of triggers and bindings to use a connection, you can configure both `WithReference()`

and `WithEnvironment()`

.

For some resources, the structure of a connection might be different between when you run it locally and when you publish it to Azure. In the previous example, `otherIntegration`

could be a resource that runs as an emulator, so `ConnectionStringExpression`

would return an emulator connection string. However, when the resource is published, Aspire might set up an identity-based connection, and `ConnectionStringExpression`

would return the service's URI. In this case, to set up [identity-based connections for Azure Functions](functions-reference#configure-an-identity-based-connection), you might need to provide a different environment variable name.

The following example uses `builder.ExecutionContext.IsPublishMode`

to conditionally add the necessary suffix:

```
builder.AddAzureFunctionsProject<Projects.MyFunctionsProject>("MyFunctionsProject")
.WithEnvironment("MyBindingConnection" + (builder.ExecutionContext.IsPublishMode ? "__serviceUri" : ""), otherIntegration.Resource.ConnectionStringExpression);
```


For details on the connection formats that each binding supports, and the permissions that those formats require, consult the binding's [reference pages](functions-triggers-bindings#supported-bindings).

## Hosting the application

Aspire supports two different ways to host your Functions project in Azure:

[Publish as a container app (default)](#publish-as-a-container-app)[Publish as a function app](#publish-as-a-function-app)using preview App Service integration

In both cases, your project is deployed as a container. Aspire takes care of building the container image for you and pushing it to Azure Container Registry.

### Publish as a container app

By default, when you publish an Aspire project to Azure, it's deployed to Azure Container Apps. The system sets up scaling rules for your Functions project using [KEDA](https://keda.sh/). When using Azure Container Apps, additional setup is needed for function keys. See [Access keys on Azure Container Apps](#access-keys-on-azure-container-apps) for more information.

#### Access keys on Azure Container Apps

Several Azure Functions scenarios use access keys to provide a basic mitigation against unwanted access. For example, HTTP trigger functions by default require an access key to be invoked, though this requirement can be disabled using the [ AuthLevel property](functions-bindings-http-webhook-trigger#attributes). See

[Work with access keys in Azure Functions](function-keys-how-to)for scenarios which may require a key.

When you deploy a Functions project using Aspire to Azure Container Apps, the system doesn't automatically create or manage Functions access keys. If you need to use access keys, you can manage them as part of your App Host setup. This section shows you how to create an extension method that you can call from your app host's `Program.cs`

file to create and manage access keys. This approach uses Azure Key Vault to store the keys and mounts them into the container app as secrets.

Note

The behavior here relies on the `ContainerApps`

secret provider, which is only available starting with Functions host version `4.1044.0`

. This version is not yet available in all regions, and until it is, when you publish your Aspire project, the base image used for the Functions project may not include the necessary changes.

These steps require Bicep version `0.38.3`

or later. You can check your Bicep version by running `bicep --version`

from a command prompt. If you have the Azure CLI installed, you can use `az bicep upgrade`

to quickly update Bicep to the latest version.

Add the following NuGet packages to your app host project:

Create a new class in your app host project and include the following code:

```
using Aspire.Hosting.Azure;
using Azure.Provisioning.AppContainers;
namespace Aspire.Hosting;
internal static class Extensions
{
private record SecretMapping(string OriginalName, IAzureKeyVaultSecretReference Reference);
public static IResourceBuilder<T> PublishWithContainerAppSecrets<T>(
this IResourceBuilder<T> builder,
IResourceBuilder<AzureKeyVaultResource>? keyVault = null,
string[]? hostKeyNames = null,
string[]? systemKeyExtensionNames = null)
where T : AzureFunctionsProjectResource
{
if (!builder.ApplicationBuilder.ExecutionContext.IsPublishMode)
{
return builder;
}
keyVault ??= builder.ApplicationBuilder.AddAzureKeyVault("functions-keys");
var hostKeysToAdd = (hostKeyNames ?? []).Append("default").Select(k => $"host-function-{k}");
var systemKeysToAdd = systemKeyExtensionNames?.Select(k => $"host-systemKey-{k}_extension") ?? [];
var secrets = hostKeysToAdd.Union(systemKeysToAdd)
.Select(secretName => new SecretMapping(
secretName,
CreateSecretIfNotExists(builder.ApplicationBuilder, keyVault, secretName.Replace("_", "-"))
)).ToList();
return builder
.WithReference(keyVault)
.WithEnvironment("AzureWebJobsSecretStorageType", "ContainerApps")
.PublishAsAzureContainerApp((infra, app) => ConfigureFunctionsContainerApp(infra, app, builder.Resource, secrets));
}
private static void ConfigureFunctionsContainerApp(
AzureResourceInfrastructure infrastructure,
ContainerApp containerApp,
IResource resource,
List<SecretMapping> secrets)
{
const string volumeName = "functions-keys";
const string mountPath = "/run/secrets/functions-keys";
var appIdentityAnnotation = resource.Annotations.OfType<AppIdentityAnnotation>().Last();
var containerAppIdentityId = appIdentityAnnotation.IdentityResource.Id.AsProvisioningParameter(infrastructure);
var containerAppSecretsVolume = new ContainerAppVolume
{
Name = volumeName,
StorageType = ContainerAppStorageType.Secret
};
foreach (var mapping in secrets)
{
var secret = mapping.Reference.AsKeyVaultSecret(infrastructure);
containerApp.Configuration.Secrets.Add(new ContainerAppWritableSecret()
{
Name = mapping.Reference.SecretName.ToLowerInvariant(),
KeyVaultUri = secret.Properties.SecretUri,
Identity = containerAppIdentityId
});
containerAppSecretsVolume.Secrets.Add(new SecretVolumeItem
{
Path = mapping.OriginalName.Replace("-", "."),
SecretRef = mapping.Reference.SecretName.ToLowerInvariant()
});
}
containerApp.Template.Containers[0].Value!.VolumeMounts.Add(new ContainerAppVolumeMount
{
VolumeName = volumeName,
MountPath = mountPath
});
containerApp.Template.Volumes.Add(containerAppSecretsVolume);
}
public static IAzureKeyVaultSecretReference CreateSecretIfNotExists(
IDistributedApplicationBuilder builder,
IResourceBuilder<AzureKeyVaultResource> keyVault,
string secretName)
{
var secretParameter = ParameterResourceBuilderExtensions.CreateDefaultPasswordParameter(builder, $"param-{secretName}", special: false);
builder.AddBicepTemplateString($"key-vault-key-{secretName}", """
param location string = resourceGroup().location
param keyVaultName string
param secretName string
@secure()
param secretValue string
// Reference the existing Key Vault
resource keyVault 'Microsoft.KeyVault/vaults@2023-07-01' existing = {
name: keyVaultName
}
// Deploy the secret only if it does not already exist
@onlyIfNotExists()
resource newSecret 'Microsoft.KeyVault/vaults/secrets@2023-07-01' = {
parent: keyVault
name: secretName
properties: {
value: secretValue
}
}
""")
.WithParameter("keyVaultName", keyVault.GetOutput("name"))
.WithParameter("secretName", secretName)
.WithParameter("secretValue", secretParameter);
return keyVault.GetSecret(secretName);
}
}
```


You can then use this method in your app host's `Program.cs`

file:

```
builder.AddAzureFunctionsProject<Projects.MyFunctionsProject>("MyFunctionsProject")
.WithHostStorage(storage)
.WithExternalHttpEndpoints()
.PublishWithContainerAppSecrets(systemKeyExtensionNames: ["mcp"]);
```


This example uses a default key vault created by the extension method. It results in a default key and a system key for use with the [Model Context Protocol extension](functions-bindings-mcp#connect-to-your-mcp-server).

To use these keys from clients, you need to retrieve them from the key vault.

### Publish as a function app

Note

Publishing as a function app requires the Aspire Azure App Service integration, which is currently in preview.

You can configure Aspire to deploy to a function app using the [Aspire Azure App Service integration](https://aspire.dev/integrations/cloud/azure/azure-functions). Because Aspire publishes the Functions project as a container, the hosting plan for your function app must support deploying containerized applications.

To publish your Aspire Functions project as a function app, follow these steps:

- Add a reference to the
[Aspire.Hosting.Azure.AppService](https://www.nuget.org/packages/Aspire.Hosting.Azure.AppService)NuGet package in your app host project. - In the
`AppHost.cs`

file, call`AddAzureAppServiceEnvironment()`

on your`IDistributedApplicationBuilder`

instance to create an App Service plan. Note that despite the name, this does not provision an App Service Environment resource. - On the Functions project resource, call
`.WithExternalHttpEndpoints()`

. This is required for deploying with the Aspire Azure App Service integration. - On the Functions project resource, call
`.PublishAsAzureAppServiceWebsite((infra, app) => app.Kind = "functionapp,linux")`

to publish that project to the plan.

Important

Make sure that you set the `app.Kind`

property to `"functionapp,linux"`

. This setting ensures the resource is created as a function app, which affects experiences for working with your application.

The following example shows a minimal `AppHost.cs`

file for an app host project that publishes a Functions project as a function app:

```
var builder = DistributedApplication.CreateBuilder(args);
builder.AddAzureAppServiceEnvironment("functions-env");
builder.AddAzureFunctionsProject<Projects.MyFunctionsProject>("MyFunctionsProject")
.WithExternalHttpEndpoints()
.PublishAsAzureAppServiceWebsite((infra, app) => app.Kind = "functionapp,linux");
```


This configuration creates a Premium V3 plan. When using a dedicated App Service plan SKU, scaling isn't event-based. Instead, scaling is managed through the App Service plan settings.

## Considerations and best practices

Consider the following points when you're evaluating the integration of Azure Functions with Aspire:

Trigger and binding configuration through Aspire is currently limited to specific integrations. For details, see

[Connection configuration with Aspire](#connection-configuration-with-aspire)in this article.Your function project's

`Program.cs`

file should use the`IHostApplicationBuilder`

version of[host instance startup](dotnet-isolated-process-guide#start-up-and-configuration).`IHostApplicationBuilder`

allows you to call`builder.AddServiceDefaults()`

to add[Aspire service defaults](/en-us/dotnet/aspire/fundamentals/service-defaults)to your Functions project.Aspire uses OpenTelemetry for monitoring. You can configure Aspire to export data to Azure Monitor through the service defaults project.

In many other Azure Functions contexts, you might include direct integration with Application Insights by registering the worker service. We don't recommend this kind of integration in Aspire. It can lead to runtime errors with version 2.22.0 of

`Microsoft.ApplicationInsights.WorkerService`

, though version 2.23.0 addresses this problem. When you're using Aspire, remove any direct Application Insights integrations from your Functions project.For Functions projects enlisted into a Aspire orchestration, most of the application configuration should come from the Aspire app host project. Avoid setting things in

`local.settings.json`

, other than the`FUNCTIONS_WORKER_RUNTIME`

setting. If you set the same environment variable in`local.settings.json`

and Aspire, the system uses the Aspire version.Don't configure the Azure Storage emulator for any connections in

`local.settings.json`

. Many Functions starter templates include the emulator as a default for`AzureWebJobsStorage`

. However, emulator configuration can prompt some developer tooling to start a version of the emulator that can conflict with the version that Aspire uses.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deployment-slots -->

# Azure Functions deployment slots

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions deployment slots allow your function app to run different instances called *slots*. Slots are different environments exposed by using a publicly available endpoint. One app instance is always mapped to the production slot, and you can swap instances assigned to a slot on demand.

The number of available slots depends on your specific hosting option:

| Hosting option | Slots (including production) |
|---|---|
|

[Flex Consumption plan](flex-consumption-plan)[Premium plan](functions-premium-plan)[Dedicated (App Service) plan](dedicated-plan)[1-20](../azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits)[Container Apps](../container-apps/functions-overview)[Revisions](../container-apps/revisions)The following descriptions reflect how functions are affected by swapping slots:

- Traffic redirection is seamless; no requests are dropped because of a swap. This seamless behavior occurs because the next function trigger is routed to the swapped slot.
- Currently executing function are terminated during the swap. To learn how to write stateless and defensive functions, see
[Improve the performance and reliability of Azure Functions](performance-reliability#write-functions-to-be-stateless).

## Why use slots?

There are many advantages to using deployment slots, including:

**Different environments for different purposes**: Using different slots gives you the opportunity to differentiate app instances before swapping to production or a staging slot.**Prewarming**: Deploying to a slot instead of directly to production allows the app to warm up before going live. Additionally, using slots reduces latency for HTTP-triggered workloads. Instances are warmed up before deployment, which reduces the cold start for newly deployed functions.**Easy fallbacks**: After a swap with production, the slot with a previously staged app now has the previous production app. If the changes swapped into the production slot aren't as you expect, you can immediately reverse the swap to get your "last known good instance" back.**Minimize restarts**: Changing app settings in a production slot requires a restart of the running app. You can instead change settings in a staging slot and swap the settings change into production with a prewarmed instance. Slots are the recommended way to migrate between Functions runtime versions while maintaining the highest availability. To learn more, see[Minimum downtime update](migrate-version-3-version-4#minimum-downtime-update).

## Swap operations

During a swap, one slot is considered the source and the other is the target. The source slot has the instance of the application that is applied to the target slot. The following steps ensure the target slot doesn't experience downtime during a swap:

**Apply settings:**Settings from the target slot are applied to all instances of the source slot. For example, the production settings are applied to the staging instance. The applied settings include the following categories:[Slot-specific](#manage-settings)app settings and connection strings (if applicable)[Continuous deployment](../app-service/deploy-continuous-deployment)settings (if enabled)[App Service authentication](../app-service/overview-authentication-authorization)settings (if enabled)

**Wait for restarts and availability:**The swap waits for every instance in the source slot to complete its restart and to be available for requests. If any instance fails to restart, the swap operation reverts all changes to the source slot and stops the operation.**Update routing:**If all instances on the source slot are warmed up successfully, the two slots complete the swap by switching routing rules. After this step, the target slot (for example, the production slot) has the app that was previously warmed up in the source slot.**Repeat operation:**Now that the source slot has the preswap app previously in the target slot, complete the same operation by applying all settings and restarting the instances for the source slot.

Keep in mind the following points:

At any point of the swap operation, initialization of the swapped apps happens on the source slot. The target slot remains online while the source slot is prepared, whether the swap succeeds or fails.

To swap a staging slot with the production slot, make sure that the production slot is

*always*the target slot. This way, the swap operation doesn't affect your production app.Settings related to event sources and bindings must be configured as

[deployment slot settings](#manage-settings)*before you start a swap*. Marking them as "sticky" ahead of time ensures events and outputs are directed to the proper instance.When you create a new staging slot, all existing settings from the production slot are created in the new slot, regardless of the

*stickiness*of the setting.

## Manage settings

Some configuration settings are slot-specific. The following lists detail which settings change when you swap slots, and which remain the same.

**Slot-specific settings**:

- Publishing endpoints
- Custom domain names
- Nonpublic certificates and TLS/SSL settings
- Scale settings
- IP restrictions
- Always On
- Diagnostic settings
- Cross-origin resource sharing (CORS)
- Private endpoints

**Non slot-specific settings**:

- General settings, such as framework version, 32/64-bit, web sockets
- App settings (can be configured to stick to a slot)
- Connection strings (can be configured to stick to a slot)
- Handler mappings
- Public certificates
- Hybrid connections *
- Virtual network integration *
- Service endpoints *
- Azure Content Delivery Network *

Features marked with an asterisk (*) don't get swapped, by design.

Note

Certain app settings that apply to unswapped settings are also not swapped. For example, since diagnostic settings aren't swapped, related app settings like `WEBSITE_HTTPLOGGING_RETENTION_DAYS`

and `DIAGNOSTICS_AZUREBLOBRETENTIONDAYS`

are also not swapped, even if they don't show up as slot settings.

### Create a deployment setting

You can mark settings as a deployment setting, which makes it *sticky*. A sticky setting doesn't swap with the app instance.

If you create a deployment setting in one slot, make sure to create the same setting with a unique value in any other slot that is involved in a swap. This way, while a setting's value doesn't change, the setting names remain consistent among slots. This name consistency ensures your code doesn't try to access a setting that is defined in one slot but not another.

Use the following steps to create a deployment setting:

Navigate to

**Deployment slots**in the function app, and then select the slot name.Select

**Configuration**, and then select the setting name you want to stick with the current slot.Select

**Deployment slot setting**, and then select**OK**.Once setting section disappears, select

**Save**to keep the changes

## Deployment

Slots are empty when you create a slot. You can use any of the [supported deployment technologies](functions-deployment-technologies) to deploy your application to a slot.

## Scaling

All slots scale to the same number of workers as the production slot.

- For Consumption plans, the slot scales as the function app scales.
- For App Service plans, the app scales to a fixed number of workers. Slots run on the same number of workers as the app plan.

## View slots

You can view information about existing slots using either the [Azure CLI](/en-us/cli/azure) or through the [Azure portal](https://portal.azure.com).

Use these steps to create a new slot in the portal:

Navigate to your function app.

Select

**Deployment slots**and the existing slots are shown.

## Add a slot

You can add a slot using either the [Azure CLI](/en-us/cli/azure) or through the [Azure portal](https://portal.azure.com).

Use these steps to create a slot in the portal:

Navigate to your function app.

Select

**Deployment slots**, and then select**+ Add Slot**.Type the name of the slot and select

**Add**.

You can also create a slot by using ARM templates or Bicep files. For an example of how to create a function app in a Consumption plan with a deployment slot, see this [Azure Resource Manager quickstart](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/function-app-create-dynamic-slot).

## Access slot resources

You access resources (HTTP triggers and administrator endpoints) in a staging slot in the same way as the production slot. However, instead of the function app host name you use the slot-specific host name in the request URL, along with any slot-specific keys. Because staging slots are live apps, you must [secure your functions](security-concepts) in a staging slot as you would in the production slot.

## Swap slots

You can swap slots in an out of production using either the [Azure CLI](/en-us/cli/azure) or through the [Azure portal](https://portal.azure.com).

Use these steps to swap a staging slot into production:

Navigate to the function app.

Select

**Deployment slots**, and then select**Swap**.Verify the configuration settings for your swap and select

**Swap**.

The swap operation can take a few seconds.

## Roll back a swap

If a swap results in an error or you simply want to "undo" a swap, you can roll back to the initial state. To return to the preswapped state, do another swap to reverse the swap.

## Remove a slot

You can remove a slot using either the [Azure CLI](/en-us/cli/azure) or through the [Azure portal](https://portal.azure.com).

Use these steps to remove a slot from your app in the portal:

Navigate to

**Deployment slots**in the function app, and then select the slot name.Select

**Delete**.Type the name of the deployment slot you want to delete, and then select

**Delete**.Close the confirmation pane.


## Change App Service plan

With a function app that is running under an App Service plan, you can change the underlying App Service plan for a slot.

Note

You can't change a slot's App Service plan under the Consumption plan.

Use the following steps to change a slot's App Service plan:

Navigate to

**Deployment slots**in the function app, and then select the slot name.Under

**App Service plan**, select**Change App Service plan**.Select the plan you want to upgrade to, or create a new plan.

Select

**OK**.

## Considerations

Azure Functions deployment slots have the following considerations:

- The number of slots available to an app depends on the plan. The Consumption plan is only allowed one deployment slot. More slots are available for apps running under other plans. For details, see
[Service limits](functions-scale#service-limits). - Swapping a slot resets keys for apps that have an
`AzureWebJobsSecretStorageType`

app setting equal to`files`

. - When slots are enabled, your function app is set to read-only mode in the portal.
- Slot swaps might fail when your function app is using a
[secured storage account](configure-networking-how-to)as its default storage account (set in`AzureWebJobsStorage`

). For more information, see thereference.`WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS`

- Use function app names shorter than 32 characters. Names longer than 32 characters are at risk of causing
[host ID collisions](storage-considerations#host-id-considerations).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-trigger-svc-invoke -->

# Dapr Service Invocation trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can be triggered on a Dapr service invocation using the following Dapr events.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("CreateNewOrder")]
public static void Run(
[DaprServiceInvocationTrigger] JObject payload,
[DaprState("%StateStoreName%", Key = "order")] out JToken order,
ILogger log)
{
log.LogInformation("C# function processed a CreateNewOrder request from the Dapr Runtime.");
// payload must be of the format { "data": { "value": "some value" } }
order = payload["data"];
}
```


Here's the Java code for the Dapr Service Invocation trigger:

```
@FunctionName("CreateNewOrder")
public String run(
@DaprServiceInvocationTrigger(
methodName = "CreateNewOrder")
)
```


Use the `app`

object to register the `daprInvokeOutput`

:

```
const { app, trigger } = require('@azure/functions');
app.generic('InvokeOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "invoke/{appId}/{methodName}",
name: "req"
}),
return: daprInvokeOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { body: payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprServiceInvocationTrigger`

:

```
{
"bindings": [
{
"type": "daprServiceInvocationTrigger",
"name": "payload",
"direction": "in"
}
]
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
$payload
)
# C# function processed a CreateNewOrder request from the Dapr Runtime.
Write-Host "PowerShell function processed a CreateNewOrder request from the Dapr Runtime."
# Payload must be of the format { "data": { "value": "some value" } }
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $payload| ConvertTo-Json
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name order -Value $payload["data"]
```


The following example shows a Dapr Service Invocation trigger, which uses the [v2 Python programming model](functions-reference-python). To use the `daprServiceInvocationTrigger`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="RetrieveOrder")
@app.dapr_service_invocation_trigger(arg_name="payload", method_name="RetrieveOrder")
@app.dapr_state_input(arg_name="data", state_store="statestore", key="order")
def main(payload, data: str) :
# Function should be invoked with this command: dapr invoke --app-id functionapp --method RetrieveOrder --data '{}'
logging.info('Python function processed a RetrieveOrder request from the Dapr Runtime.')
logging.info(data)
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprServiceInvocationTrigger`

to trigger a Dapr service invocation binding, which supports the following properties.

| Parameter | Description |
|---|---|
MethodName |
Optional. The name of the method the Dapr caller should use. If not specified, the name of the function is used as the method name. |

## Annotations

The `DaprServiceInvocationTrigger`

annotation allows you to create a function that gets invoked by Dapr runtime.

| Element | Description |
|---|---|
methodName |
The method name. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
type |
Must be set to `daprServiceInvocationTrigger` . |
name |
The name of the variable that represents the Dapr data in function code. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
type |
Must be set to `daprServiceInvocationTrigger` . |
name |
The name of the variable that represents the Dapr data in function code. |

See the [Example section](#example) for complete examples.

## Usage

To use a Dapr Service Invocation trigger, learn more about which components to use with the Service Invocation trigger and how to set them up in the official Dapr documentation.

To use the `daprServiceInvocationTrigger`

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-input-state -->

# Dapr State input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr state input binding allows you to read Dapr state during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("StateInputBinding")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "state/{key}")] HttpRequest req,
[DaprState("statestore", Key = "{key}")] string state,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult(state);
}
```


The following example creates a `"RetrieveOrder"`

function using the `DaprStateInput`

binding with the [ DaprServiceInvocationTrigger](functions-bindings-dapr-trigger-svc-invoke):

```
@FunctionName("RetrieveOrder")
public String run(
@DaprServiceInvocationTrigger(
methodName = "RetrieveOrder")
String payload,
@DaprStateInput(
stateStore = "%StateStoreName%",
key = "order")
String product,
final ExecutionContext context)
```


In the following example, the Dapr invoke input binding is added as an `extraInput`

and paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('StateInputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['GET'],
route: "state/{key}",
name: "req"
}),
extraInputs: [daprStateInput],
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const daprStateInputValue = context.extraInputs.get(daprStateInput);
// print the fetched state value
context.log(daprStateInputValue);
return daprStateInputValue;
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprState`

:

```
{
"bindings":
{
"type": "daprState",
"direction": "in",
"key": "order",
"stateStore": "%StateStoreName%",
"name": "order"
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
$payload, $order
)
# C# function processed a CreateNewOrder request from the Dapr Runtime.
Write-Host "PowerShell function processed a RetrieveOrder request from the Dapr Runtime."
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $order | ConvertTo-Json
Write-Host "$jsonString"
```


The following example shows a Dapr State input binding, which uses the [v2 Python programming model](functions-reference-python). To use the `daprState`

binding alongside the `daprServiceInvocationTrigger`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="RetrieveOrder")
@app.dapr_service_invocation_trigger(arg_name="payload", method_name="RetrieveOrder")
@app.dapr_state_input(arg_name="data", state_store="statestore", key="order")
def main(payload, data: str) :
# Function should be invoked with this command: dapr invoke --app-id functionapp --method RetrieveOrder --data '{}'
logging.info('Python function processed a RetrieveOrder request from the Dapr Runtime.')
logging.info(data)
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprState`

to read Dapr state into your function, which supports these parameters:

| Parameter | Description |
|---|---|
StateStore |
The name of the state store to retrieve state. |
Key |
The name of the key to retrieve from the specified state store. |

## Annotations

The `DaprStateInput`

annotation allows you to read Dapr state into your function.

| Element | Description |
|---|---|
stateStore |
The name of the Dapr state store. |
key |
The state store key value. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
stateStore |
The name of the state store. |
key |
The name of the key to retrieve from the specified state store. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
key |
The name of the key to retrieve from the specified state store. |
stateStore |
The name of the state store. |

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr state input binding, start by setting up a Dapr state store component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprState`

in Python v2, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`
