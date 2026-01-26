---
merged_at: 2026-01-26T23:29:57.726809
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-ai-enabled-apps -->

# Use AI tools and models in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides serverless compute resources that integrate with AI and Azure services to streamline building cloud-hosted intelligent applications. This article provides a survey of the breadth of AI-related scenarios, integrations, and other AI resources that you can use in your function apps.

Consider using Azure Functions in your AI-enabled experiences for these scenarios:

| Scenario | Description |
|---|---|
|

[Agentic workflows](#agentic-workflows)[Retrieval-augmented generation (RAG)](#retrieval-augmented-generation)Select one of these scenarios to learn more in this article.

This article is language-specific, so make sure you choose your programming language at the [top of the page](#top).

## Tools and MCP servers

AI models and agents use *function calling* to request external resources known as *tools*. Function calling lets models and agents dynamically invoke specific functionality based on the context of a conversation or task.

Functions is particularly well-suited for implementing function calling in agentic workflows because it efficiently scales to handle demand and provides [binding extensions](functions-triggers-bindings) that simplify connecting agents with remote Azure services. When you build or host AI tools in Functions, you also get serverless pricing models and platform security features.

The Model Context Protocol (MCP) is the industry standard for interacting with remote servers. It provides a standardized way for AI models and agents to communicate with external systems. An MCP server lets these AI clients efficiently determine the tools and capabilities of an external system.

Azure Functions currently supports exposing your function code by using these types of tools:

| Tool type | Description |
|---|---|
|

[Queue-based Azure Functions tool](#queue-based-azure-functions-tools)### Remote MCP servers

Functions supports these options for creating and hosting remote MCP servers:

- Use the
[MCP binding extension](functions-bindings-mcp)to create and host custom MCP servers as you would any other function app. - Self host MCP servers created by using the official MCP SDKs.
*This hosting option is currently in preview.*

Here's a comparison of the current MCP server hosting options provided by Functions:

| Feature |
|
|---|

*[Functions triggers and bindings](functions-triggers-bindings)Python

TypeScript

JavaScript

Java

Python

TypeScript

Java

[MCP binding extension](functions-bindings-mcp)[Custom handlers](functions-custom-handlers)*Configuration details for self-hosted MCP servers change during the preview.

Here are some options to help you get started hosting MCP servers in Functions:

| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

[Remote custom MCP server](https://github.com/Azure-Samples/remote-mcp-functions-dotnet)[Weather server](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-dotnet)[HelloTool](https://github.com/Azure/azure-functions-templates/tree/dev/Functions.Templates/Templates/McpToolTrigger-CSharp-Isolated)| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

[Remote custom MCP server](https://github.com/Azure-Samples/remote-mcp-functions-python)[Weather server](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-python)| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

[Remote custom MCP server](https://github.com/Azure-Samples/remote-mcp-functions-typescript)[Weather server](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-node)| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

PowerShell isn't currently supported for either MCP server hosting option.

### Queue-based Azure Functions tools

In addition to MCP servers, you can implement AI tools by using Azure Functions with queue-based communication. Azure AI Foundry provides Azure Functions-specific tools that enable asynchronous function calling by using message queues. With these tools, AI agents interact with your code by using messaging patterns.

This tool approach is ideal for AI Foundry scenarios that require:

- Reliable message delivery and processing
- Decoupling between AI agents and function execution
- Built-in retry and error handling capabilities
- Integration with existing Azure messaging infrastructure

Here are some reference samples for function calling scenarios:

Uses an

[Azure AI Foundry Agent Service]client to call a custom remote MCP server implemented by using Azure Functions.

Uses function calling features for agents in Azure AI SDKs to implement custom function calling.


## Agentic workflows

AI-driven processes often determine how to interact with models and other AI assets. However, some scenarios require a higher level of predictability or well-defined steps. These directed agentic workflows orchestrate separate tasks or interactions that agents must follow.

The [Durable Functions extension](durable/durable-functions-overview) helps you take advantage of the strengths of Functions to create multistep, long-running operations with built-in fault tolerance. These workflows work well for your directed agentic workflows. For example, a trip planning solution might first gather requirements from the user, search for plan options, obtain user approval, and finally make required bookings. In this scenario, you can build an agent for each step and then coordinate their actions as a workflow using Durable Functions.

For more workflow scenario ideas, see [Application patterns](durable/durable-functions-overview#application-patterns) in Durable Functions.

## Retrieval-augmented generation

Because Functions can handle multiple events from various data sources simultaneously, it's an effective solution for real-time AI scenarios, like RAG systems that require fast data retrieval and processing. Rapid event-driven scaling reduces the latency your customers experience, even in high-demand situations.

Here are some reference samples for RAG-based scenarios:

For RAG, you can use SDKs, including Azure Open AI and Azure SDKs, to build your scenarios. ::: zone-end


Shows you how to create a friendly chat bot that issues simple prompts, receives text completions, and sends messages, all in a stateful session using the

[OpenAI binding extension].

## AI tools and frameworks for Azure Functions

Functions lets you build apps in your preferred language and use your favorite libraries. Because of this flexibility, you can use a wide range of AI libraries and frameworks in your AI-enabled function apps.

Here are some key Microsoft AI frameworks you should be aware of:

| Framework/library | Description |
|---|---|
|

[Azure AI Foundry Agent Service](/en-us/azure/ai-foundry/agents/overview)[Azure AI Services SDKs](/en-us/azure/ai-foundry/)Functions also lets your apps reference third-party libraries and frameworks, so you can use all of your favorite AI tools and libraries in your AI-enabled functions.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-scheduled-function -->

# Create a function in the Azure portal that runs on a schedule

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to use the Azure portal to create a function that runs [serverless](https://azure.microsoft.com/solutions/serverless/) on Azure based on a schedule that you define.

Note

In-portal editing is only supported for JavaScript, PowerShell, and C# Script functions.
Python in-portal editing is supported only when running in the Consumption plan.
To create a C# Script app that supports in-portal editing, you must choose a runtime **Version** that supports the **in-process model**.

When possible, you should [develop your functions locally](functions-develop-local).

To learn more about the limitations on editing function code in the Azure portal, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal).

## Prerequisites

To complete this tutorial:

Ensure that you have an Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create a function app

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Function App**.Under

**Select a hosting option**, select**Consumption**>**Select**to create your app in the default**Consumption**plan. In this[serverless](https://azure.microsoft.com/overview/serverless-computing/)hosting option, you pay only for the time your functions run.[Premium plan](functions-premium-plan)also offers dynamic scaling. When you run in an App Service plan, you must manage the[scaling of your function app](functions-scale).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which you create your new function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. You should create a new resource group because there are [known limitations when creating new function apps in an existing resource group](functions-scale#limitations-for-creating-new-function-apps-in-an-existing-resource-group).**Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

. To guarantee a unique app name, you can optionally enable**Secure unique default hostname**, which is currently in preview.**Runtime stack**Preferred language Choose a runtime that supports your favorite function programming language. In-portal editing is only available for JavaScript, PowerShell, Python, TypeScript, and C# script.

To create a C# Script app that supports in-portal editing, you must choose a runtime**Version**that supports the**in-process model**.

C# class library and Java functions must be[developed locally](functions-develop-local#local-development-environments).**Version**Version number Choose the version of your installed runtime. **Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access.**Operating system**Windows An operating system is preselected for you based on your runtime stack selection, but you can change the setting if necessary. In-portal editing is only supported on Windows. Accept the default options in the remaining tabs, including the default behavior of creating a new storage account on the

**Storage**tab and a new Application Insight instance on the**Monitoring**tab. You can also choose to use an existing storage account or Application Insights instance.Select

**Review + create**to review the app configuration you chose, and then select**Create**to provision and deploy the function app.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

Your new function app is ready to use. Next, you create a function in the new function app.


## Create a timer triggered function

In your function app, select

**Overview**, and then select**+ Create**under**Functions**.Under

**Select a template**, scroll down and choose the**Timer trigger**template.In

**Template details**, configure the new trigger with the settings as specified in the table below the image, and then select**Create**.Setting Suggested value Description **Name**Default Defines the name of your timer triggered function. **Schedule**0 */1 * * * * A six field [CRON expression](functions-bindings-timer#ncrontab-expressions)that schedules your function to run every minute.

## Test the function

In your function, select

**Code + Test**and expand the**Logs**.Verify execution by viewing the information written to the logs.


Now, you change the function's schedule so that it runs once every hour instead of every minute.

## Update the timer schedule

In your function, select

**Integration**. Here, you define the input and output bindings for your function and also set the schedule.Select

**Timer (myTimer)**.Update the

**Schedule**value to`0 0 */1 * * *`

, and then select**Save**.

You now have a function that runs once every hour, on the hour.

## Clean up resources

Other quickstarts in this collection build upon this quickstart. If you plan to work with subsequent quickstarts, tutorials, or with any of the services you've created in this quickstart, don't clean up the resources.

*Resources* in Azure refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You've created resources to complete these quickstarts. You might be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In the Azure portal, go to the

**Resource group**page.To get to that page from the function app page, select the

**Overview**tab, and then select the link under**Resource group**.To get to that page from the dashboard, select

**Resource groups**, and then select the resource group that you used for this article.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**and follow the instructions.Deletion might take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You created a function that runs based on a schedule. For more information about timer triggers, see [Timer trigger for Azure Functions](functions-bindings-timer).

Now that you've created your first function, let's add an output binding to the function that writes a message to a Storage queue.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-openai-text-completion -->

# Tutorial: Add Azure OpenAI text completion hints to your functions in Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Visual Studio Code to add an HTTP endpoint to the function app you created in the previous quickstart article. When triggered, this new HTTP endpoint uses an [Azure OpenAI text completion input binding](functions-bindings-openai-textcompletion-input) to get text completion hints from your data model.

During this tutorial, you learn how to accomplish these tasks:

- Create resources in Azure OpenAI.
- Deploy a model in the OpenAI resource.
- Set access permissions to the model resource.
- Enable your function app to connect to OpenAI.
- Add OpenAI bindings to your HTTP triggered function.

## 1. Check prerequisites

- Complete the steps in
[part 1 of Create a function in Azure using Visual Studio Code](how-to-create-function-vs-code). - Obtain access to Azure OpenAI in your Azure subscription. If you haven't already been granted access, complete
[this form](https://aka.ms/oai/access)to request access.

- Install
[.NET Core CLI tools](/en-us/dotnet/core/tools/?tabs=netcore2x).

- The
[Azurite storage emulator](../storage/common/storage-use-azurite?tabs=npm). While you can also use an actual Azure Storage account, the article assumes you're using this emulator.

## 2. Create your Azure OpenAI resources

The following steps show how to create an Azure OpenAI data model in the Azure portal.

Sign in with your Azure subscription in the

[Azure portal](https://portal.azure.com).Select

**Create a resource**and search for the**Azure OpenAI**. When you locate the service, select**Create**.On the

**Create Azure OpenAI**page, provide the following information for the fields on the**Basics**tab:Field Description **Subscription**Your subscription, which has been onboarded to use Azure OpenAI. **Resource group**The resource group you created for the function app in the previous article. You can find this resource group name by right-clicking the function app in the Azure Resources browser, selecting properties, and then searching for the `resourceGroup`

setting in the returned JSON resource file.**Region**Ideally, the same location as the function app. **Name**A descriptive name for your Azure OpenAI Service resource, such as *mySampleOpenAI*.**Pricing Tier**The pricing tier for the resource. Currently, only the Standard tier is available for the Azure OpenAI Service. For more info on pricing visit the [Azure OpenAI pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/)Select

**Next**twice to accept the default values for both the**Network**and**Tags**tabs. The service you create doesn't have any network restrictions, including from the internet.Select

**Next**a final time to move to the final stage in the process:**Review + submit**.Confirm your configuration settings, and select

**Create**.The Azure portal displays a notification when the new resource is available. Select

**Go to resource**in the notification or search for your new Azure OpenAI resource by name.In the Azure OpenAI resource page for your new resource, select

**Click here to view endpoints**under**Essentials**>**Endpoints**. Copy the**endpoint**URL and the**keys**. Save these values, you need them later.

Now that you have the credentials to connect to your model in Azure OpenAI, you need to set these access credentials in application settings.

## 3. Deploy a model

Now you can deploy a model. You can select from one of several available models in Azure OpenAI Studio.

To deploy a model, follow these steps:

Sign in to

[Azure OpenAI Studio](https://oai.azure.com).Choose the subscription and the Azure OpenAI resource you created, and select

**Use resource**.Under

**Management**select**Deployments**.Select

**Create new deployment**and configure the following fields:Field Description **Deployment name**Choose a name carefully. The deployment name is used in your code to call the model by using the client libraries and the REST APIs, so you must save for use later on. **Select a model**Model availability varies by region. For a list of available models per region, see [Model summary table and region availability](/en-us/azure/ai-services/openai/concepts/models#model-summary-table-and-region-availability).Important

When you access the model via the API, you need to refer to the deployment name rather than the underlying model name in API calls, which is one of the key differences between OpenAI and Azure OpenAI. OpenAI only requires the model name. Azure OpenAI always requires deployment name, even when using the model parameter. In our docs, we often have examples where deployment names are represented as identical to model names to help indicate which model works with a particular API endpoint. Ultimately your deployment names can follow whatever naming convention is best for your use case.

Accept the default values for the rest of the setting and select

**Create**.The deployments table shows a new entry that corresponds to your newly created model.


You now have everything you need to add Azure OpenAI-based text completion to your function app.

## 4. Update application settings

In Visual Studio Code, open the local code project you created when you completed the

[previous article](how-to-create-function-vs-code?pivot=programming-language-csharp).In the local.settings.json file in the project root folder, update the

`AzureWebJobsStorage`

setting to`UseDevelopmentStorage=true`

. You can skip this step if the`AzureWebJobsStorage`

setting in*local.settings.json*is set to the connection string for an existing Azure Storage account instead of`UseDevelopmentStorage=true`

.In the local.settings.json file, add these settings values:

: required by the binding extension. Set this value to the endpoint of the Azure OpenAI resource you created earlier.`AZURE_OPENAI_ENDPOINT`

: required by the binding extension. Set this value to the key for the Azure OpenAI resource.`AZURE_OPENAI_KEY`

: used to define the input binding. Set this value to the name you chose for your model deployment.`CHAT_MODEL_DEPLOYMENT_NAME`


Save the file. When you deploy to Azure, you must also add these settings to your function app.


## 5. Register binding extensions

Because you're using an Azure OpenAI output binding, you must have the corresponding bindings extension installed before you run the project.

Except for HTTP and timer triggers, bindings are implemented as extension packages. To add the Azure OpenAI extension package to your project, run this [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the **Terminal** window:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.OpenAI --prerelease
```


## 5. Update the extension bundle

To access the preview Azure OpenAI bindings, you must use a preview version of the extension bundle that contains this extension.

Replace the `extensionBundle`

setting in your current `host.json`

file with this JSON:

```
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
```


Now, you can use the Azure OpenAI output binding in your project.

## 6. Return text completion from the model

The code you add creates a `whois`

HTTP function endpoint in your existing project. In this function, data passed in a URL `name`

parameter of a GET request is used to dynamically create a completion prompt. This dynamic prompt is bound to a text completion input binding, which returns a response from the model based on the prompt. The completion from the model is returned in the HTTP response.

In your existing

`HttpExample`

class file, add this`using`

statement:`using Microsoft.Azure.Functions.Worker.Extensions.OpenAI.TextCompletion;`

In the same file, add this code that defines a new HTTP trigger endpoint named

`whois`

:`[Function(nameof(WhoIs))] public IActionResult WhoIs([HttpTrigger(AuthorizationLevel.Function, Route = "whois/{name}")] HttpRequest req, [TextCompletionInput("Who is {name}?", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%")] TextCompletionResponse response) { if(!String.IsNullOrEmpty(response.Content)) { return new OkObjectResult(response.Content); } else { return new NotFoundObjectResult("Something went wrong."); } }`


Update the

`pom.xml`

project file to add this reference to the`properties`

collection:`<azure-functions-java-library-openai>0.5.0-preview</azure-functions-java-library-openai>`

In the same file, add this dependency to the

`dependencies`

collection:`<dependency> <groupId>com.microsoft.azure.functions</groupId> <artifactId>azure-functions-java-library-openai</artifactId> <version>${azure-functions-java-library-openai}</version> </dependency>`

In the existing

`Function.java`

project file, add these`import`

statements:`import com.microsoft.azure.functions.openai.annotation.textcompletion.TextCompletion; import com.microsoft.azure.functions.openai.annotation.textcompletion.TextCompletionResponse;`

In the same file, add this code that defines a new HTTP trigger endpoint named

`whois`

:`@FunctionName("WhoIs") public HttpResponseMessage whoIs( @HttpTrigger( name = "req", methods = {HttpMethod.GET}, authLevel = AuthorizationLevel.ANONYMOUS, route = "whois/{name}") HttpRequestMessage<Optional<String>> request, @BindingName("name") String name, @TextCompletion(prompt = "Who is {name}?", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", name = "response", isReasoningModel = false) TextCompletionResponse response, final ExecutionContext context) { return request.createResponseBuilder(HttpStatus.OK) .header("Content-Type", "application/json") .body(response.getContent()) .build(); }`


In Visual Studio Code, Press F1 and in the command palette type

`Azure Functions: Create Function...`

, select**HTTP trigger**, type the function name`whois`

, and press Enter.In the new

`whois.js`

code file, replace the contents of the file with this code:`const { app, input } = require("@azure/functions"); // This OpenAI completion input requires a {name} binding value. const openAICompletionInput = input.generic({ prompt: 'Who is {name}?', maxTokens: '100', type: 'textCompletion', chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%' }) app.http('whois', { methods: ['GET'], route: 'whois/{name}', authLevel: 'function', extraInputs: [openAICompletionInput], handler: async (_request, context) => { var response = context.extraInputs.get(openAICompletionInput) return { body: response.content.trim() } } });`


In Visual Studio Code, Press F1 and in the command palette type

`Azure Functions: Create Function...`

, select**HTTP trigger**, type the function name`whois`

, and press Enter.In the new

`whois.ts`

code file, replace the contents of the file with this code:`import { app, input } from "@azure/functions"; // This OpenAI completion input requires a {name} binding value. const openAICompletionInput = input.generic({ prompt: 'Who is {name}?', maxTokens: '100', type: 'textCompletion', chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%' }) app.http('whois', { methods: ['GET'], route: 'whois/{name}', authLevel: 'function', extraInputs: [openAICompletionInput], handler: async (_request, context) => { var response: any = context.extraInputs.get(openAICompletionInput) return { body: response.content.trim() } } });`


In the existing

`function_app.py`

project file, add this`import`

statement:`import json`

In the same file, add this code that defines a new HTTP trigger endpoint named

`whois`

:`@app.route(route="whois/{name}", methods=["GET"]) @app.text_completion_input( arg_name="response", prompt="Who is {name}?", max_tokens="100", chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%", ) def whois(req: func.HttpRequest, response: str) -> func.HttpResponse: response_json = json.loads(response) return func.HttpResponse(response_json["content"], status_code=200)`


In Visual Studio Code, Press F1 and in the command palette type

`Azure Functions: Create Function...`

, select**HTTP trigger**, type the function name`whois`

, select**Anonymous**, and press Enter.Open the new

`whois/function.json`

code file and replace its contents with this code, which adds a definition for the`TextCompletionResponse`

input binding:`{ "bindings": [ { "authLevel": "function", "type": "httpTrigger", "direction": "in", "name": "Request", "route": "whois/{name}", "methods": [ "get" ] }, { "type": "http", "direction": "out", "name": "Response" }, { "type": "textCompletion", "direction": "in", "name": "TextCompletionResponse", "prompt": "Who is {name}?", "maxTokens": "100", "chatModel": "%CHAT_MODEL_DEPLOYMENT_NAME%" } ] }`

Replace the content of the

`whois/run.ps1`

code file with this code, which returns the input binding response:`using namespace System.Net param($Request, $TriggerMetadata, $TextCompletionResponse) Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{ StatusCode = [HttpStatusCode]::OK Body = $TextCompletionResponse.Content })`


## 7. Run the function

In Visual Studio Code, Press F1 and in the command palette type

`Azurite: Start`

and press Enter to start the Azurite storage emulator.Press

`F5`to start the function app project and Core Tools in debug mode.With the Core Tools running, send a GET request to the

`whois`

endpoint function, with a name in the path, like this URL:`http://localhost:7071/api/whois/<NAME>`

Replace the

`<NAME>`

string with the value you want passed to the`"Who is {name}?"`

prompt. The`<NAME>`

must be the URL-encoded name of a public figure, like`Abraham%20Lincoln`

.The response you see is the text completion response from your Azure OpenAI model.

After a response is returned, press

`Ctrl + C`to stop Core Tools.

## 8. Clean up resources

In Azure, *resources* refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You created resources to complete these quickstarts. You could be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-sql -->

# Azure SQL bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure SQL](/en-us/azure/azure-sql/index) bindings in Azure Functions. Azure Functions supports input bindings, output bindings, and a function trigger for the Azure SQL and SQL Server products.

| Action | Type |
|---|---|
| Trigger a function when a change is detected on a SQL table |
|

[Input binding](functions-bindings-azure-sql-input)[Output binding](functions-bindings-azure-sql-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Sql/).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Sql
```


To use a preview version of the Microsoft.Azure.Functions.Worker.Extensions.Sql package, add the `--prerelease`

flag to the command. You can view preview functionality on the [Azure Functions SQL Extensions release page](https://github.com/Azure/azure-functions-sql-extension/releases).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Sql --prerelease
```


Note

Breaking changes between preview releases of the Azure SQL bindings for Azure Functions requires that all Functions targeting the same database use the same version of the SQL extension package.

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

If your app needs to use preview functionality, you should instead reference the latest version of the preview bundle. For more information, see [Work with preview extension bundles](extension-bundles#work-with-preview-extension-bundles).

You can view preview functionality on the [Azure Functions SQL Extensions release page](https://github.com/Azure/azure-functions-sql-extension/releases).

Note

Breaking changes between preview releases of the Azure SQL bindings for Azure Functions requires that all Functions targeting the same database use the same version of the SQL extension package.

## Update packages

Add the [Azure Functions Java SQL Types package](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-sql) to your functions project with an update to the `pom.xml`

file in your project, as in this example:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-sql</artifactId>
<version>2.1.0</version>
</dependency>
```


## SQL connection string

Azure SQL bindings for Azure Functions have a required property for the connection string on all bindings and triggers. These pass the connection string to the Microsoft.Data.SqlClient library and supports the connection string as defined in the [SqlClient ConnectionString documentation](/en-us/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-core-5.0&preserve-view=true#Microsoft_Data_SqlClient_SqlConnection_ConnectionString).

Important

For optimal security, you should use Microsoft Entra ID with managed identities for connections between Functions and Azure SQL Database. Managed identities make your app more secure by eliminating secrets from your application deployments, such as credentials in the connection strings, server names, and ports being used. You can learn how to use managed identities in this tutorial, [Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).

Notable keywords include:

`Authentication`

: allows a function to connect to Azure SQL with Microsoft Entra ID and managed identities. For more information, see[Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).`Command timeout`

: allows a function to wait for specified amount of time in seconds before terminating a query (default 30 seconds)`ConnectRetryCount`

: allows a function to automatically make additional reconnection attempts, especially applicable to Azure SQL Database serverless tier (default 1)`Pooling`

: allows a function to reuse connections to the database, which can improve performance (default`true`

). Additional settings for connection pooling include`Connection Lifetime`

,`Max Pool Size`

, and`Min Pool Size`

. Learn more about connection pooling in the[ADO.NET documentation](/en-us/sql/connect/ado-net/sql-server-connection-pooling)

## Considerations

- Azure SQL binding supports version 4.x and later of the Functions runtime.
- Source code for the Azure SQL bindings can be found in
[this GitHub repository](https://github.com/Azure/azure-functions-sql-extension). - This binding requires connectivity to an Azure SQL or SQL Server database.
- Output bindings against tables with columns of data types
`NTEXT`

,`TEXT`

, or`IMAGE`

aren't supported and data upserts will fail. These types[will be removed](/en-us/sql/t-sql/data-types/ntext-text-and-image-transact-sql)in a future version of SQL Server and aren't compatible with the`OPENJSON`

function used by this Azure Functions binding. - Use
[managed identities](/en-us/azure/azure-sql/database/authentication-azure-ad-user-assigned-managed-identity)instead of usernames and passwords. - Consider using an
[Azure Key Value](/en-us/azure/app-service/app-service-key-vault-references)to store application settings.

## Samples

In addition to the samples for C#, Java, JavaScript, PowerShell, and Python available in the [Azure SQL bindings GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples), more are available in Azure Samples:

[C# ToDo API sample with Azure SQL bindings](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/)[Use SQL bindings in Azure Stream Analytics](../stream-analytics/sql-database-upsert#option-1-update-by-key-with-the-azure-function-sql-binding)[Send data from Azure SQL with Python](/en-us/samples/azure-samples/sqlbindings-python-datatransfer/sample-load-data-from-sql-using-python-and-azure-functions/)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-state -->

# Dapr State output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr state output binding allows you to save a value to a Dapr state during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using the Dapr state output binding to persist a new state into the state store.

```
[FunctionName("StateOutputBinding")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = "state/{key}")] HttpRequest req,
[DaprState("statestore", Key = "{key}")] IAsyncCollector<string> state,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
await state.AddAsync(requestBody);
return new OkResult();
}
```


The following example creates a `"CreateNewOrderHttpTrigger"`

function using the `DaprStateOutput`

binding with an `HttpTrigger`

:

```
@FunctionName("CreateNewOrderHttpTrigger")
public String run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@DaprStateOutput(
stateStore = "%StateStoreName%",
key = "product")
OutputBinding<String> product,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger (CreateNewOrderHttpTrigger) processed a request.");
}
```


In the following example, the Dapr state output binding is paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('StateOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "state/{key}",
name: "req"
}),
return: daprStateOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { value : payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprState`

output:

```
{
"bindings":
{
"type": "daprState",
"stateStore": "%StateStoreName%",
"direction": "out",
"name": "order",
"key": "order"
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


The following example shows a Dapr State output binding, which uses the [v2 Python programming model](functions-reference-python). To use `daprState`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="HttpTriggerFunc")
@app.route(route="req", auth_level=dapp.auth_level.ANONYMOUS)
@app.dapr_state_output(arg_name="state", state_store="statestore", key="newOrder")
def main(req: func.HttpRequest, state: func.Out[str] ) -> str:
# request body must be passed this way '{\"value\": { \"key\": \"some value\" } }'
body = req.get_body()
if body is not None:
state.set(body.decode('utf-8'))
logging.info(body.decode('utf-8'))
else:
logging.info('req body is none')
return 'ok'
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprState`

to define a Dapr state output binding, which supports these parameters:

| Parameter | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
StateStore |
The name of the state store to save state. | ✔️ | ❌ |
Key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
Value |
Required. The value being stored. |
❌ | ✔️ |

## Annotations

The `DaprStateOutput`

annotation allows you to function access a state store.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
stateStore |
The name of the state store to save state. | ✔️ | ❌ |
key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
value |
Required. The value being stored. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
stateStore |
The name of the state store to save state. | ✔️ | ❌ |
key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
value |
Required. The value being stored. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
stateStore |
The name of the state store to save state. | ✔️ | ❌ |
key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
value |
Required. The value being stored. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_state_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
stateStore |
The name of the state store to save state. | ✔️ | ❌ |
key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
value |
Required. The value being stored. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr state output binding, start by setting up a Dapr state store component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-premium-plan -->

# Azure Functions Premium plan

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Functions Elastic Premium plan is a dynamic scale hosting option for function apps. For other hosting plan options, see [Azure Functions hosting options](functions-scale).

Important

Azure Functions can run on the Azure App Service platform. In the App Service platform, plans that host Premium plan function apps are referred to as *Elastic* Premium plans, with SKU names like `EP1`

. If you choose to run your function app on a Premium plan, make sure to create a plan with an SKU name that starts with "E", such as `EP1`

. App Service plan SKU names that start with "P", such as `P1V2`

(Premium V2 Small plan), are actually [Dedicated hosting plans](dedicated-plan). Because they are Dedicated and not Elastic Premium, plans with SKU names starting with "P" won't scale dynamically and may increase your costs.

Premium plan hosting provides the following benefits for your functions:

*Always ready*and*prewarmed*instances to avoid cold starts- Virtual network connectivity
- Support for
[longer runtime durations](#longer-run-duration) [Choice of Premium instance sizes](#available-instance-skus)- More predictable pricing, compared with the Consumption plan
- High-density app allocation for plans with multiple function apps
- Support for
[Linux container deployments](container-concepts)

When you use the Premium plan, you add and remove instances of the Azure Functions host based on the number of incoming events, just like the [Flex Consumption plan](flex-consumption-plan) and the [Consumption plan](consumption-plan). You can deploy multiple function apps to the same Premium plan. You can configure the compute instance size, base plan size, and maximum plan size.

## Billing

You pay for the Premium plan based on the number of core seconds and memory allocated across instances. This billing model differs from the Consumption plan, which bills you based on per-second resource consumption and executions. The Premium plan has no execution charge. This billing model results in a minimum monthly cost per active plan, whether the function is active or idle. All function apps in a Premium plan share allocated instances. For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).

Note

Every premium plan always has at least one active (billed) instance.

## Create a Premium plan

When you create a function app in the Azure portal, the Consumption plan is the default. To create a function app that runs in a Premium plan, you must explicitly create or choose an Azure Functions Premium hosting plan by using one of the *Elastic Premium* versions. You host the function app you create in this plan. The Azure portal makes it easy to create both the Premium plan and the function app at the same time. You can run more than one function app in the same Premium plan, but they must both run on the same operating system (Windows or Linux).

The following articles show you how to programmatically create a function app with a Premium plan:

## Eliminate cold starts

When events or executions don't occur in the Consumption plan, your app might scale to zero instances. When new events arrive, the system must create a new instance that runs your app. Specializing new instances takes time, depending on the app. This extra latency on the first call is often called a [cold start](event-driven-scaling#cold-start).

The Premium plan provides two features that work together to effectively eliminate cold starts in your functions: *always ready instances* and *prewarmed instances*. Always ready instances are a category of preallocated instances unaffected by scaling, and the prewarmed instances are a buffer as you scale due to HTTP events.

When events begin to trigger the app, the system first routes them to the always ready instances. As the function becomes active due to HTTP events, other instances warm as a buffer. These buffered instances are called prewarmed instances. This buffer reduces cold start for new instances required during scale.

### Always ready instances

In the Premium plan, you can have your app always ready on a specified number of instances. Your app runs continuously on those instances, regardless of load. If load exceeds what your always ready instances can handle, the app adds more instances as necessary, up to your specified maximum.

This app-level setting also controls your plan's minimum instances. For example, consider three function apps in the same Premium plan. When two of your apps have always ready instance count set to one, and the third app is set to five, the minimum number for your whole plan is five. This number also reflects the minimum number of instances for which your plan is billed. The maximum number of always ready instances supported per app is 20.

You can configure the number of always ready instances in the Azure portal by selecting your **Function App**, going to the **App Service plan** > **Scale Out** menu option on the left, and editing the **App Scale out** options. In the function app edit window, always ready instances are specific to that app.

### Prewarmed instances

The prewarmed instance count setting provides warmed instances as a buffer during HTTP scale and activation events. Prewarmed instances continue to buffer until the maximum scale-out limit is reached. The default prewarmed instance count is 1 and, for most scenarios, keep this value as 1.

Consider a less common scenario, such as an app running in a custom container. Because custom containers have a long warm-up time, you might consider increasing this buffer of prewarmed instances. A prewarmed instance becomes active only after all active instances are in use.

You can also define a warmup trigger that runs during the prewarming process. You can use a warmup trigger to preload custom dependencies during the prewarming process so your functions are ready to start processing requests immediately. To learn more, see [Azure Functions warmup trigger](functions-bindings-warmup).

Consider this example that shows how always ready instances and prewarmed instances work together. A premium function app has two always ready instances configured, and the default of one prewarmed instance.


- When the app is idle and no events are triggering, the app is provisioned and running with two instances. At this time, you're billed for the two always ready instances but aren't billed for a prewarmed instance because no prewarmed instance is allocated.
- As your application starts receiving HTTP traffic, requests are load balanced across the two always ready instances. As soon as those two instances start processing events, an instance is added to fill the prewarmed buffer. The app is now running with three provisioned instances: the two always ready instances, and the third prewarmed and inactive buffer. You're billed for the three instances.
- As load increases and your app needs more instances to handle HTTP traffic, that prewarmed instance swaps to an active instance. HTTP load is now routed to all three instances, and a fourth instance is instantly provisioned to fill the prewarmed buffer.
- This sequence of scaling and prewarming continues until the maximum instance count for the app is reached or load decreases causing the platform to scale back in after a period. No instances are prewarmed or activated beyond the maximum.

You can't change the prewarmed instance count setting in the portal. You must instead use the Azure CLI or Azure PowerShell.

### Maximum function app instances

In addition to the [plan maximum burst count](#plan-and-sku-settings), you can configure a per-app maximum. You configure the app maximum by using the [app scale limit](event-driven-scaling#limit-scale-out). The maximum app scale-out limit can't exceed the maximum burst instances of the plan.

## Private network connectivity

Function apps deployed to a Premium plan can take advantage of [virtual network integration for web apps](../app-service/overview-vnet-integration). When configured, your app can communicate with resources within your virtual network or secured via service endpoints. You can also use IP restrictions on the app to restrict incoming traffic.

When assigning a subnet to your function app in a Premium plan, you need a subnet with enough IP addresses for each potential instance. You need an IP block with at least 100 available addresses.

For more information, see [Integrate Azure Functions with a virtual network](functions-create-vnet).

## Rapid elastic scale

The same rapid scaling logic as the Flex Consumption and Consumption plans automatically adds more compute instances for your app. Apps in the same App Service Plan scale independently from one another based on the needs of an individual app. However, Functions apps in the same App Service Plan share VM resources to help reduce costs, when possible. The number of apps associated with a VM depends on the footprint of each app and the size of the VM.

To learn more about how scaling works, see [Event-driven scaling in Azure Functions](event-driven-scaling).

## Longer run duration

Functions in a Consumption plan are limited to 10 minutes for a single execution. In the Premium plan, the run duration defaults to 30 minutes to prevent runaway executions. However, you can [modify the host.json configuration](functions-host-json#functiontimeout) to make the duration unbounded for Premium plan apps, with the following limitations:

- Platform upgrades can trigger a managed shutdown and halt the function execution with a grace period of 10 minutes.
- An idle timer stops the worker after 60 minutes with no new executions.
[Scale-in behavior](event-driven-scaling#scale-in-behaviors)can cause worker shutdown after 60 minutes.[Slot swaps](functions-deployment-slots)can terminate executions on the source and target slots during the swap.

## Migration

If you have an existing function app, you can use Azure CLI commands to migrate your app between a Consumption plan and a Premium plan on Windows. The specific commands depend on the direction of the migration. For more information, see [Plan migration](functions-how-to-use-azure-function-app-settings#plan-migration).

This migration isn't supported on Linux.

## Premium plan settings

When you create the plan, you set two plan size settings: the minimum number of instances (or plan size) and the maximum burst limit.

If your app needs more instances beyond the always ready instances, it can continue to scale out until the number of instances reaches the plan maximum burst limit, or the app maximum scale-out limit if you set it. You pay for instances only while they're running and allocated to you, on a per-second basis. The platform makes its best effort at scaling your app out to the defined maximum limits.

You can configure the plan size in the Azure portal by selecting your **Function App** deployed to that plan, going to the **App Service plan** > **Scale Up** menu options on the left, and choosing a larger plan size. To increase the maximum burst limit, choose the **Scale Out** menu option and edit the **Plan Scale out** > **Maximum burst** option.

The minimum for every Premium plan is at least one instance. The actual minimum number of instances is determined based on the always ready instances requested by apps in the plan. For example, if app A requests five always ready instances, and app B requests two always ready instances in the same plan, the minimum plan size is determined as five. App A runs on all five instances, and app B runs on two.

Important

You're charged for each instance allocated in the minimum instance count whether or not functions are executing.

In most circumstances, this autocalculated minimum is sufficient. However, scaling beyond the minimum occurs at a best effort. It's possible, though unlikely, that at a specific time scale-out could be delayed if other instances are unavailable. By setting a minimum higher than the autocalculated minimum, you reserve instances in advance of scale-out.

You can configure the minimum instances in the Azure portal by selecting your **Function App** deployed to that plan, going to the **App Service plan** > **Scale Out** menu option on the left, and editing the **Plan Scale out** > **Minimum Instances** option.

### Available instance SKUs

When you create or scale your plan, choose from three instance sizes. You're billed for the total number of cores and memory you provision, per second for each instance allocated to you. Your app can automatically scale out to multiple instances as needed.

| SKU | Cores | Memory | Storage |
|---|---|---|---|
| EP1 | 1 | 3.5 GB | 250 GB |
| EP2 | 2 | 7 GB | 250 GB |
| EP3 | 4 | 14 GB | 250 GB |

### Memory usage considerations

Running on a machine with more memory doesn't always mean that your function app uses all available memory.

For example, a JavaScript function app is constrained by the default memory limit in Node.js. To increase this fixed memory limit, add the app setting `languageWorkers:node:arguments`

with a value of `--max-old-space-size=<max memory in MB>`

.

For plans with more than 4 GB of memory, set the Bitness Platform Setting to `64 Bit`

under [General settings](../app-service/configure-common#configure-general-settings).

## Region max scale-out

The following table lists currently supported maximum scale-out values for a single plan in each region and OS configuration:

| Region | Windows | Linux |
|---|---|---|
| Australia Central | 100 | 20 |
| Australia Central 2 | 100 | Not Available |
| Australia East | 100 | 40 |
| Australia Southeast | 100 | 20 |
| Brazil South | 100 | 20 |
| Canada Central | 100 | 100 |
| Central India | 100 | 20 |
| Central US | 100 | 100 |
| China East 2 | 20 | 20 |
| China North 2 | 20 | 20 |
| China North 3 | 20 | 20 |
| East Asia | 100 | 20 |
| East US | 100 | 100 |
| East US 2 | 80 | 100 |
| France Central | 100 | 60 |
| Germany West Central | 100 | 20 |
| Israel Central | 100 | 20 |
| Italy North | 100 | 20 |
| Japan East | 100 | 20 |
| Japan West | 100 | 20 |
| Jio India West | 100 | 20 |
| Korea Central | 100 | 20 |
| Korea South | 40 | 20 |
| Mexico Central | 20 | 20 |
| North Central US | 100 | 20 |
| North Europe | 100 | 100 |
| Norway East | 100 | 20 |
| South Africa North | 100 | 20 |
| South Africa West | 20 | 20 |
| South Central US | 100 | 100 |
| South India | 100 | Not Available |
| Southeast Asia | 100 | 20 |
| Spain Central | 20 | 20 |
| Switzerland North | 100 | 20 |
| Switzerland West | 100 | 20 |
| UAE North | 100 | 100 |
| UK South | 100 | 100 |
| UK West | 100 | 20 |
| USGov Arizona | 20 | 20 |
| USGov Texas | 20 | Not Available |
| USGov Virginia | 80 | 20 |
| West Central US | 100 | 20 |
| West Europe | 100 | 100 |
| West India | 100 | 20 |
| West US | 100 | 100 |
| West US 2 | 100 | 20 |
| West US 3 | 100 | 20 |

For more information, see [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=functions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-input -->

# Azure Database for MySQL input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure Database for MySQL input binding retrieves data from a database and passes it to the input parameter of the function.

For information on setup and configuration, see the [overview](functions-bindings-azure-mysql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

This section contains the following examples:

[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-c-oop)[HTTP trigger, get multiple rows from route data](#http-trigger-get-multiple-items-from-route-data-c-oop)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-c-oop)

The examples refer to a `Product`

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


### HTTP trigger, get a row by ID from a query string

The following example shows a C# function that retrieves a single record. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses a query string to specify the ID. That ID is used to retrieve a `Product`

record with the specified query.

Note

The HTTP query string parameter is case-sensitive.

```
using System.Collections.Generic;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Azure.Functions.Worker.Http;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.InputBindingIsolatedSamples
{
public static class GetProductById
{
[Function(nameof(GetProductById))]
public static IEnumerable<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproducts/{productId}")]
HttpRequestData req,
[MySqlInput("select * from Products where ProductId = @productId",
"MySqlConnectionString",
parameters: "@ProductId={productId}")]
IEnumerable<Product> products)
{
return products;
}
}
}
```


### HTTP trigger, get multiple rows from a route parameter

The following example shows a [C# function](functions-dotnet-class-library) that retrieves rows that the query returned. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses route data to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

```
using System.Collections.Generic;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Azure.Functions.Worker.Http;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.InputBindingIsolatedSamples
{
public static class GetProducts
{
[Function(nameof(GetProducts))]
public static IEnumerable<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproducts")]
HttpRequestData req,
[MySqlInput("select * from Products",
"MySqlConnectionString")]
IEnumerable<Product> products)
{
return products;
}
}
}
```


### HTTP trigger, delete rows

The following example shows a [C# function](functions-dotnet-class-library) that executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the MySQL database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


```
namespace AzureMySqlSamples.InputBindingSamples
{
public static class GetProductsStoredProcedure
{
[FunctionName(nameof(GetProductsStoredProcedure))]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproducts-storedprocedure/{cost}")]
HttpRequest req,
[MySql("DeleteProductsCost",
"MySqlConnectionString",
commandType: System.Data.CommandType.StoredProcedure,
parameters: "@Cost={cost}")]
IEnumerable<Product> products)
{
return new OkObjectResult(products);
}
}
}
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-java).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-java)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-java)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-java)

The examples refer to a `Product`

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
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding in a Java function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

```
package com.function;
import com.function.Common.Product;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.mysql.annotation.CommandType;
import com.microsoft.azure.functions.mysql.annotation.MySqlInput;
import java.util.Optional;
public class GetProducts {
@FunctionName("GetProducts")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "getproducts}")
HttpRequestMessage<Optional<String>> request,
@MySqlInput(
name = "products",
commandText = "SELECT * FROM Products",
commandType = CommandType.Text,
connectionStringSetting = "MySqlConnectionString")
Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products).build();
}
}
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding in a Java function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

```
public class GetProductById {
@FunctionName("GetProductById")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "getproducts/{productid}")
HttpRequestMessage<Optional<String>> request,
@MySqlInput(
name = "products",
commandText = "SELECT * FROM Products WHERE ProductId= @productId",
commandType = CommandType.Text,
parameters = "@productId={productid}",
connectionStringSetting = "MySqlConnectionString")
Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products).build();
}
}
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding in a Java function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


```
public class DeleteProductsStoredProcedure {
@FunctionName("DeleteProductsStoredProcedure")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "Deleteproducts-storedprocedure/{cost}")
HttpRequestMessage<Optional<String>> request,
@MySqlInput(
name = "products",
commandText = "DeleteProductsCost",
commandType = CommandType.StoredProcedure,
parameters = "@Cost={cost}",
connectionStringSetting = "MySqlConnectionString")
Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products).build();
}
}
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-js).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-javascript)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-javascript)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-javascript)

The examples refer to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const mysqlInput = input.generic({
commandText: 'select * from Products',
commandType: 'Text',
connectionStringSetting: 'MySqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and MySQL input binding function processed a request.');
const products = context.extraInputs.get(mysqlInput);
return {
jsonBody: products,
};
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [mysqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const mysqlInput = input.generic({
type: 'mysql',
commandText: 'select * from Products where Cost = @Cost',
parameters: '@Cost={Cost}',
commandType: 'Text',
connectionStringSetting: 'MySqlConnectionString'
})
app.http('GetProducts', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'getproducts/{cost}',
extraInputs: [mysqlInput],
handler: async (request, context) => {
const products = JSON.stringify(context.extraInputs.get(mysqlInput));
return {
status: 200,
body: products
};
}
});
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const mysqlInput = input.generic({
commandText: 'select * from Products where ProductId= @productId',
commandType: 'Text',
parameters: '@productId={productid}',
connectionStringSetting: 'MySqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and MySQL input binding function processed a request.');
const products = context.extraInputs.get(mysqlInput);
return {
jsonBody: products,
};
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [mysqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const mysqlInput = input.generic({
type: 'mysql',
commandText: 'select * from Products where ProductId= @productId',
commandType: 'Text',
parameters: '@productId={productid}',
connectionStringSetting: 'MySqlConnectionString'
})
app.http('GetProducts', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'getproducts/{productid}',
extraInputs: [mysqlInput],
handler: async (request, context) => {
const products = JSON.stringify(context.extraInputs.get(mysqlInput));
return {
status: 200,
body: products
};
}
});
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const mysqlInput = input.generic({
commandText: 'DeleteProductsCost',
commandType: 'StoredProcedure',
parameters: '@Cost={cost}',
connectionStringSetting: 'MySqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and MySQL input binding function processed a request.');
const products = context.extraInputs.get(mysqlInput);
return {
jsonBody: products,
};
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [mysqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const mysqlInput = input.generic({
type: 'mysql',
commandText: 'DeleteProductsCost',
commandType: 'StoredProcedure',
parameters: '@Cost={cost}',
connectionStringSetting: 'MySqlConnectionString'
})
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
route: 'DeleteProductsByCost',
extraInputs: [mysqlInput],
handler: async (request, context) => {
const products = JSON.stringify(context.extraInputs.get(mysqlInput));
return {
status: 200,
body: products
};
}
});
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-powershell).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-powershell)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-powershell)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-powershell)

The examples refer to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a PowerShell function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get"
],
"route": "getproducts/{cost}"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "products",
"type": "mysql",
"direction": "in",
"commandText": "select * from Products",
"commandType": "Text",
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
param($Request, $TriggerMetadata, $products)
Write-Host "PowerShell function with MySql Input Binding processed a request."
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $products
})
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding in a PowerShell function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get"
],
"route": "getproducts/{productid}"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "products",
"type": "mysql",
"direction": "in",
"commandText": "select * from Products where ProductId= @productId",
"commandType": "Text",
"parameters": "MySqlConnectionString",
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
param($Request, $TriggerMetadata, $products)
Write-Host "PowerShell function with MySql Input Binding processed a request."
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $products
})
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a PowerShell function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = 'cost';
END
```


```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get"
],
"route": "deleteproducts-storedprocedure/{cost}"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "products",
"type": "mysql",
"direction": "in",
"commandText": "DeleteProductsCost",
"commandType": "StoredProcedure",
"parameters": "@Cost={cost}",
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
param($Request, $TriggerMetadata, $products)
Write-Host "PowerShell function with MySql Input Binding processed a request."
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $products
}
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-python).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-python)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-python)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-python)

The examples refer to a database table:

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

### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a Python function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

The following example is sample Python code for the function_app.py file:

```
import azure.functions as func
import datetime
import json
import logging
app = func.FunctionApp()
@app.generic_trigger(arg_name="req", type="httpTrigger", route="getproducts/{cost}")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_input_binding(arg_name="products", type="mysql",
commandText= "select * from Products",
command_type="Text",
connection_string_setting="MySqlConnectionString")
def mysql_test(req: func.HttpRequest, products: func.MySqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), products))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding in a Python function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

The following example is sample Python code for the function_app.py file:

```
import azure.functions as func
import datetime
import json
import logging
app = func.FunctionApp()
@app.generic_trigger(arg_name="req", type="httpTrigger", route="getproducts/{cost}")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_input_binding(arg_name="products", type="mysql",
commandText= "select * from Products where ProductId= @productId",
command_type="Text",
parameters= "@productId={productid}",
connection_string_setting="MySqlConnectionString")
def mysql_test(req: func.HttpRequest, products: func.MySqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), products))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a Python function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


The following example is sample Python code for the function_app.py file:

```
import azure.functions as func
import datetime
import json
import logging
app = func.FunctionApp()
@app.generic_trigger(arg_name="req", type="httpTrigger", route="getproducts/{cost}")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_input_binding(arg_name="products", type="mysql",
commandText= "DeleteProductsCost",
command_type="StoredProcedure",
parameters= "@Cost={cost}",
connection_string_setting="MySqlConnectionString")
def mysql_test(req: func.HttpRequest, products: func.MySqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), products))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the `MySqlAttribute`

attribute to declare the MySQL bindings on the function. The attribute has the following properties:

| Attribute property | Description |
|---|---|
`CommandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`ConnectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
`CommandType` |
Required. A
`CommandType` |

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)

`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)

`StoredProcedure`

`Parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@MySQLInput`

annotation on parameters whose values would come from Azure Database for MySQL. This annotation supports the following elements:

| Element | Description |
|---|---|
`commandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
`commandType` |
Required. A
`CommandType` |

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)

`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)

`StoredProcedure`

`name`

`parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `input.generic()`

method:

| Property | Description |
|---|---|
`commandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

`commandType`

[value, which is](/en-us/dotnet/api/system.data.commandtype)`CommandType`

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)`StoredProcedure`

`parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).## Configuration

The following table explains the binding configuration properties that you set in the function.json file:

| Property | Description |
|---|---|
`type` |
Required. Must be set to `mysql` . |
`direction` |
Required. Must be set to `in` . |
`name` |
Required. The name of the variable that represents the query results in function code. |
`commandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

`commandType`

[value, which is](/en-us/dotnet/api/system.data.commandtype)`CommandType`

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)`StoredProcedure`

`parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The attribute's constructor takes the MySQL command text, the command type, parameters, and the name of the connection string setting. The command can be a MySQL query with the command type `System.Data.CommandType.Text`

or a stored procedure name with the command type `System.Data.CommandType.StoredProcedure`

. The name of the connection string setting corresponds to the application setting (in local.settings.json for local development) that contains the [connection string](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html) to Azure Database for MySQL.

If an exception occurs when an Azure Database for MySQL input binding is executed, the function code stops running. The result might be an error code, such as an HTTP trigger that returns a 500 error code.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output -->

# Dapr Binding output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr output binding allows you to send a value to a Dapr output binding during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using a Dapr service invocation trigger and a Dapr output binding to read and process a binding request.

```
[FunctionName("SendMessageToKafka")]
public static async Task Run(
[DaprServiceInvocationTrigger] JObject payload,
[DaprBinding(BindingName = "%KafkaBindingName%", Operation = "create")] IAsyncCollector<object> messages,
ILogger log)
{
log.LogInformation("C# function processed a SendMessageToKafka request.");
await messages.AddAsync(payload);
}
```


The following example creates a `"SendMessageToKafka"`

function using the `DaprBindingOutput`

binding with the [ DaprServiceInvocationTrigger](functions-bindings-dapr-output):

```
@FunctionName("SendMessageToKafka")
public String run(
@DaprServiceInvocationTrigger(
methodName = "SendMessageToKafka")
String payload,
@DaprBindingOutput(
bindingName = "%KafkaBindingName%",
operation = "create")
OutputBinding<String> product,
final ExecutionContext context) {
context.getLogger().info("Java function processed a SendMessageToKafka request.");
product.setValue(payload);
return payload;
}
```


In the following example, the Dapr output binding is paired with the Dapr invoke output trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('SendMessageToKafka', {
trigger: trigger.generic({
type: 'daprServiceInvocationTrigger',
name: "payload"
}),
return: daprBindingOutput,
handler: async (request, context) => {
context.log("Node function processed a SendMessageToKafka request from the Dapr Runtime.");
context.log(context.triggerMetadata.payload)
return { "data": context.triggerMetadata.payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprBinding`

:

```
{
"bindings":
{
"type": "daprBinding",
"direction": "out",
"bindingName": "%KafkaBindingName%",
"operation": "create",
"name": "messages"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($req, $TriggerMetadata)
Write-Host "Powershell SendMessageToKafka processed a request."
$invoke_output_binding_req_body = @{
"data" = $req
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name messages -Value $invoke_output_binding_req_body
```


The following example shows a Dapr Binding output binding, which uses the [v2 Python programming model](functions-reference-python). To use `@dapp.dapr_binding_output`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="SendMessageToKafka")
@app.dapr_service_invocation_trigger(arg_name="payload", method_name="SendMessageToKafka")
@app.dapr_binding_output(arg_name="messages", binding_name="%KafkaBindingName%", operation="create")
def main(payload: str, messages: func.Out[bytes]) -> None:
logging.info('Python processed a SendMessageToKafka request from the Dapr Runtime.')
messages.set(json.dumps({"data": payload}).encode('utf-8'))
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprBinding`

to define a Dapr binding output binding, which supports these parameters:

| Parameter | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
BindingName |
The name of the Dapr binding. | ✔️ | ✔️ |
Operation |
The configured binding operation. | ✔️ | ✔️ |
Metadata |
The metadata namespace. | ❌ | ✔️ |
Data |
Required. The data for the binding operation. |
❌ | ✔️ |

## Annotations

The `DaprBindingOutput`

annotation allows you to create a function that sends an output binding.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
bindingName |
The name of the Dapr binding. | ✔️ | ✔️ |
output |
The configured binding operation. | ✔️ | ✔️ |
metadata |
The metadata namespace. | ❌ | ✔️ |
data |
Required. The data for the binding operation. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
bindingName |
The name of the binding. | ✔️ | ✔️ |
operation |
The binding operation. | ✔️ | ✔️ |
metadata |
The metadata namespace. | ❌ | ✔️ |
data |
Required. The data for the binding operation. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
bindingName |
The name of the binding. | ✔️ | ✔️ |
operation |
The binding operation. | ✔️ | ✔️ |
metadata |
The metadata namespace. | ❌ | ✔️ |
data |
Required. The data for the binding operation. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_binding_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
binding_name |
The name of the binding event. | ✔️ | ✔️ |
operation |
The binding operation name/identifier. | ✔️ | ✔️ |
metadata |
The metadata namespace. | ❌ | ✔️ |
data |
Required. The data for the binding operation. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr output binding, start by setting up a Dapr output binding component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

[Dapr output binding component specs](https://docs.dapr.io/reference/components-reference/supported-bindings/)[How to: Use output bindings to interface with external resources](https://docs.dapr.io/developing-applications/building-blocks/bindings/howto-bindings/)

To use the `daprBinding`

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook-output -->

# Azure Functions HTTP output bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the HTTP output binding to respond to the HTTP request sender (HTTP trigger). This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.

The default return value for an HTTP-triggered function is:

`HTTP 204 No Content`

with an empty body in Functions 2.x and higher`HTTP 200 OK`

with an empty body in Functions 1.x

## Attribute

A return value attribute isn't required when using [HttpResponseData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httpresponsedata). However, when using a [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) and [multi-binding output objects](dotnet-isolated-process-guide#multiple-output-bindings), the `[HttpResultAttribute]`

attribute should be applied to the object property. The attribute takes no parameters. To learn more, see [Usage](#usage).

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [HttpOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.httpoutput) annotation to define an output variable other than the default variable returned by the function. This annotation supports the following settings:

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
type |
Must be set to `http` . |
direction |
Must be set to `out` . |
name |
The variable name used in function code for the response, or `$return` to use the return value. |

## Usage

To send an HTTP response, use the language-standard response patterns.

In .NET, the response type depends on the C# mode:

The HTTP triggered function returns an object of one of the following types:

[IActionResult](/en-us/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)1(or`Task<IActionResult>`

)[HttpResponse](/en-us/dotnet/api/microsoft.aspnetcore.http.httpresponse)1(or`Task<HttpResponse>`

)[HttpResponseData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httpresponsedata)(or`Task<HttpResponseData>`

)- JSON serializable types representing the response body for a
`200 OK`

response.

1 This type is only available when using [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration).

When one of these types is used as part of [multi-binding output objects](dotnet-isolated-process-guide#multiple-output-bindings), the `[HttpResult]`

attribute should be applied to the object property. The attribute takes no parameters.

For Java, use an [HttpResponseMessage.Builder](/en-us/java/api/com.microsoft.azure.functions.httpresponsemessage.builder) to create a response to the HTTP trigger. To learn more, see [HttpRequestMessage and HttpResponseMessage](functions-reference-java#httprequestmessage-and-httpresponsemessage).

For example responses, see the [trigger examples](functions-bindings-http-webhook-trigger#example).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-rabbitmq -->

# RabbitMQ bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [RabbitMQ](https://www.rabbitmq.com/) via [triggers and bindings](functions-triggers-bindings).

Note

The RabbitMQ bindings are only fully supported on [Elastic Premium](functions-premium-plan) and [Dedicated (App Service)](dedicated-plan) plans. [Flex Consumption](flex-consumption-plan) and [Consumption](consumption-plan) plans aren't yet supported.

RabbitMQ bindings aren't supported by the Azure Functions v1.x runtime.

The Azure Functions RabbitMQ extension allows you to send and receive messages using the RabbitMQ API with Functions.

| Action | Type |
|---|---|
| Run a function when a RabbitMQ message comes through the queue |
|

[Output binding](functions-bindings-rabbitmq-output)## Prerequisites

Before working with the RabbitMQ extension, you must [set up your RabbitMQ endpoint](https://github.com/Azure/azure-functions-rabbitmq-extension/wiki/Setting-up-a-RabbitMQ-Endpoint). To learn more about RabbitMQ, see the [getting started page](https://www.rabbitmq.com/getstarted.html).

## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Rabbitmq).

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

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

```
{
"version": "2.0",
"extensions": {
"rabbitMQ": {
"prefetchCount": 100,
"queueName": "queue",
"connectionString": "%<MyConnectionAppSetting>%",
"port": 10
}
}
}
```


| Property | Default | Description |
|---|---|---|
`prefetchCount` |
30 | Gets or sets the number of messages that the message receiver can simultaneously request and is cached. |
`queueName` |
n/a | Name of the queue to receive messages from. |
`connectionString` |
n/a | The app setting that contains the RabbitMQ message queue connection string. |
`port` |
0 | (ignored if using connectionString) Gets or sets the Port used. Defaults to 0, which points to rabbitmq client's default port setting: 5672. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-best-practices -->

# Best practices for reliable Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions is an event-driven, compute-on-demand service that extends the existing Azure App Service application platform. It adds capabilities to implement code triggered by events occurring in Azure, in a partner service, and in on-premises systems. By using Functions, you can build solutions that connect to data sources or messaging solutions, which makes it easier to process and react to events. Functions runs in Azure data centers, which are complex with many integrated components. In a hosted cloud environment, it's expected that VMs can occasionally restart or move, and systems upgrades occur. Your functions apps also likely depend on external APIs, Azure Services, and other databases, which are also prone to periodic unreliability.

This article details some best practices for designing and deploying efficient function apps that remain healthy and perform well in a cloud-based environment.

## Choose the correct hosting plan

When you create a function app in Azure, you must choose a hosting plan for your app. The plan you choose affects performance, reliability, and cost. Azure Functions provides the following hosting plans:

When possible, use the [Flex Consumption plan](flex-consumption-plan) to host your dynamic scale apps.

In the context of the App Service platform, the *Premium* plan that dynamically hosts your functions is the Elastic Premium plan (EP). Other Dedicated (App Service) plans are called Premium. For more information, see [Azure Functions Premium plan](functions-premium-plan).

The hosting plan you choose determines the following behaviors:

- How your function app scales based on demand and how instance allocation is managed.
- The resources available to each function app instance.
- Support for advanced functionality, such as Azure Virtual Network connectivity.

For more information about choosing the correct hosting plan and a detailed comparison between the plans, see [Azure Functions hosting options](functions-scale).

Choose the correct plan when you create your function app. Functions provides a limited ability to switch your hosting plan, primarily between Consumption and Elastic Premium plans. For more information, see [Plan migration](functions-how-to-use-azure-function-app-settings?tabs=portal#plan-migration).

## Configure storage correctly

Functions requires a storage account be associated with your function app. The Functions host uses the storage account connection for operations such as managing triggers and logging function executions. It's also used when dynamically scaling function apps. For more information, see [Storage considerations for Azure Functions](storage-considerations).

A misconfigured file system or storage account in your function app can affect the performance and availability of your functions. For help with troubleshooting an incorrectly configured storage account, see the [storage troubleshooting](functions-recover-storage-account) article.

### Storage connection settings

Function apps that scale dynamically can run either from an Azure Files endpoint in your storage account or from the file servers associated with your scaled-out instances. This behavior is controlled by the following application settings:

The Premium plan and the Consumption plan on Windows support these settings. The Flex Consumption plan doesn't require these settings and uses a Blob storage container to host deployment packages instead of an Azure Files share.

When you create your function app in the Azure portal or by using Azure CLI or Azure PowerShell, you create these settings for your function app when needed. When you create your resources from an Azure Resource Manager template (ARM template), you need to also include `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

in the template.

On your first deployment using an ARM template, don't include `WEBSITE_CONTENTSHARE`

, which is generated for you.

You can use the following ARM template examples to help correctly configure these settings:

[Consumption plan](https://azure.microsoft.com/resources/templates/function-app-create-dynamic/)[Dedicated plan](https://azure.microsoft.com/resources/templates/function-app-create-dedicated/)[Premium plan with VNET integration](https://azure.microsoft.com/resources/templates/function-premium-vnet-integration/)[Consumption plan with a deployment slot](https://azure.microsoft.com/resources/templates/function-app-create-dynamic-slot/)

Important

The Azure Files service doesn't currently support identity-based connections. The Flex Consumption plan fully supports managed identities. For more information, see [Create an app without Azure Files](storage-considerations#create-an-app-without-azure-files).

### Storage account configuration

When creating a function app, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage. Functions relies on Azure Storage for operations such as managing triggers and logging function executions. The storage account connection string for your function app is found in the `AzureWebJobsStorage`

and `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

application settings.

Keep in mind the following considerations when creating this storage account:

To reduce latency, create the storage account in the same region as the function app.

To improve performance in production, use a separate storage account for each function app. This aspect is especially true with Durable Functions and Event Hubs triggered functions.

For Event Hubs triggered functions, don't use an account with

[Data Lake Storage enabled](https://github.com/Azure/azure-functions-eventhubs-extension/issues/81).

### Handling large data sets

When running on Linux, you can add extra storage by mounting a file share. Mounting a share is a convenient way for a function to process a large existing data set. For more information, see [Mount file shares](storage-considerations#mount-file-shares).

## Organize your functions

As part of your solution, you likely develop and publish multiple functions. These functions are often combined into a single function app, but they can also run in separate function apps. In Premium and Dedicated (App Service) hosting plans, multiple function apps can also share the same resources by running in the same plan. How you group your functions and function apps can affect the performance, scaling, configuration, deployment, and security of your overall solution.

For Consumption and Premium plan, all functions in a function app are dynamically scaled together.

For more information on how to organize your functions, see [Function organization best practices](performance-reliability#function-organization-best-practices).

## Optimize deployments

When you deploy a function app, remember that the unit of deployment for functions in Azure is the function app. You deploy all functions in a function app at the same time, usually from the same deployment package.

Consider these options for a successful deployment:

Have your functions run from the deployment package. This

[run from package approach](run-functions-from-deployment-package)provides the following benefits:- Reduces the risk of file copy locking problems.
- Can be deployed directly to a production app and doesn't trigger a restart.
- All files in the package are available to your app.
- Improves the performance of ARM template deployments.
- Might reduce cold-start times, particularly for JavaScript functions with large npm package trees.

Consider using

[continuous deployment](functions-continuous-deployment)to connect deployments to your source control solution. Continuous deployments also let you run from the deployment package.For

[Premium plan hosting](functions-premium-plan), consider adding a warmup trigger to reduce latency when new instances are added. For more information, see[Azure Functions warm-up trigger](functions-bindings-warmup).To minimize deployment downtime, use deployment slots for Consumption, Premium, and Dedicated plans. Or, configure rolling updates for zero-downtime deployments in the Flex Consumption plan. For more information, see

[Azure Functions deployment slots](functions-deployment-slots)and[site update strategies in Flex Consumption](flex-consumption-site-updates).

## Write robust functions

Follow design principles that help with the general performance and availability of your functions. These principles include:

[Avoid long running functions](performance-reliability#avoid-long-running-functions)[Plan cross-function communication](performance-reliability#cross-function-communication)[Write functions to be stateless](performance-reliability#write-functions-to-be-stateless)[Write defensive functions](performance-reliability#write-defensive-functions)

Transient failures are common in cloud computing, so use a [retry pattern](/en-us/azure/architecture/patterns/retry) when accessing cloud-based resources. Many triggers and bindings already implement retry.

Prioritize integration testing by continuously testing your functions in the context of the full application and in your build automation pipelines.

## Design for security

Consider security during the planning phase, not after your functions are ready. For more information, see [Securing Azure Functions](security-concepts).

## Consider concurrency

As demand builds on your function app because of incoming events, Consumption and Premium plans scale out the function apps. It's important to understand how your function app responds to load and how the triggers can be configured to handle incoming events. For a general overview, see [Event-driven scaling in Azure Functions](event-driven-scaling).

Dedicated (App Service) plans require you to provide scaling for your function apps.

### Worker process count

In some cases, it's more efficient to handle the load by creating multiple processes, called language worker processes, in the instance before scale-out. The [FUNCTIONS_WORKER_PROCESS_COUNT](functions-app-settings#functions_worker_process_count) setting controls the maximum number of language worker processes allowed. The default for this setting is `1`

, which means that multiple processes aren't used. After the maximum number of processes are reached, the function app scales out to more instances to handle the load. This setting doesn't apply for [C# class library functions](functions-dotnet-class-library), which run in the host process.

When you use `FUNCTIONS_WORKER_PROCESS_COUNT`

on a Premium plan or Dedicated (App Service) plan, consider the number of cores provided by your plan. For example, the Premium plan `EP2`

provides two cores, so you should start with a value of `2`

and increase by two as needed, up to the maximum.

### Trigger configuration

When you plan for throughput and scaling, understand how the different types of triggers process events. Some triggers give you control over batching behaviors and concurrency. Adjusting these values can help each instance scale appropriately for the demands of the invoked functions. You apply these configuration options to all triggers in a function app, and maintain them in the host.json file for the app. For settings details, see the Configuration section of the specific trigger reference.

To learn more about how Functions processes message streams, see [Azure Functions reliable event processing](functions-reliable-event-processing).

### Plan for connections

Connection limits apply to function apps running in [Consumption plan](consumption-plan). These limits apply to each instance. Because of these limits and as a general best practice, optimize your outbound connections from your function code. For more information, see [Manage connections in Azure Functions](manage-connections).

### Language-specific considerations

For your language of choice, keep in mind the following considerations:

[Use cancellation tokens](functions-dotnet-class-library?#cancellation-tokens)(in-process only).

## Maximize availability

Cold start is a key consideration for serverless architectures. For more information, see [Cold starts](event-driven-scaling#cold-start). If cold start is a concern for your scenario, see [Understanding serverless cold start](https://azure.microsoft.com/blog/understanding-serverless-cold-start/).

Both Flex Consumption and Premium plans are recommended for reducing cold starts while maintaining dynamic scale. Use the following guidance to reduce cold starts and improve availability in all hosting plans.

| Plan | Guidance |
|---|---|
Flex Consumption plan |
•
•
|

**Premium plan**[Implement a Warmup trigger in your function app](functions-bindings-warmup)•

[Set the values for Always-Ready instances and Max Burst limit](functions-premium-plan#plan-and-sku-settings)•

[Use virtual network trigger support when using non-HTTP triggers on a virtual network](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers)**Dedicated plans**[Run on at least two instances with Azure App Service Health Check enabled](../app-service/monitor-instances-health-check)•

[Implement autoscaling](/en-us/azure/architecture/best-practices/auto-scaling)**Consumption plan**•

[Review the](event-driven-scaling#limit-scale-out)`functionAppScaleLimit`

setting, which can limit scale-out• Check for a Daily Usage Quota (GB-Sec) limit set during development and testing. Consider removing this limit in production environments.

## Monitor effectively

Azure Functions offers built-in integration with Azure Application Insights to monitor your function execution and traces written from your code. For more information, see [Monitor executions in Azure Functions](functions-monitoring). Azure Monitor also provides facilities for monitoring the health of the function app itself. For more information, see [Monitor Azure Functions](monitor-functions).

Be aware of the following considerations when using Application Insights integration to monitor your functions:

Remove the

[AzureWebJobsDashboard](functions-app-settings#azurewebjobsdashboard)application setting. This setting was supported in older versions of Functions. Removing`AzureWebJobsDashboard`

improves the performance of your functions.Review the

[Application Insights logs](analyze-telemetry-data). If data you expect to find is missing, consider adjusting the sampling settings to better capture your monitoring scenario. Use the`excludedTypes`

setting to exclude certain types from sampling, such as`Request`

or`Exception`

. For more information, see[Configure sampling](configure-monitoring?tabs=v2#configure-sampling).

Azure Functions also allows you to [send system-generated and user-generated logs to Azure Monitor Logs](functions-monitor-log-analytics). Integration with Azure Monitor Logs is currently in preview.

## Build in redundancy

Your business needs might require that your functions always be available, even during a data center outage. To learn how to use a multiregional approach to keep your critical functions always running, see [Reliability in Azure Functions](/en-us/azure/reliability/reliability-functions).
