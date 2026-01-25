---
merged_at: 2026-01-25T15:41:11.636929
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _scenario-custom-remote-mcp-server_functions-versions.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: scenario-custom-remote-mcp-server.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-custom-remote-mcp-server -->

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


---

<!-- DOCUMENTO FUSIONADO: functions-versions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-versions -->

# Azure Functions runtime versions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Functions currently supports two versions of the runtime host. The following table details the currently supported runtime versions, their support level, and when they should be used:]

| Version | Support level | Description |
|---|---|---|
| 4.x | GA | Check out Recommended runtime version for functions in all languages.
|
| 1.x | GA (
|

**Support will end for version 1.x on September 14, 2026.**We highly recommend you[migrate your apps to version 4.x](migrate-version-1-version-4?pivots=programming-language-csharp), which supports .NET Framework 4.8, .NET 8, .NET 9, and .NET 10 Preview.Important

As of December 13, 2022, function apps running on versions 2.x and 3.x of the Azure Functions runtime reached the end of extended support. For more information, see [Retired versions](#retired-versions).

This article details some of the differences between supported versions, how you can create each version, and how to change the version on which your functions run.

## Levels of support

There are two levels of support:

**Generally available (GA)**- Fully supported and approved for production use.**Preview**- Not yet supported, but expected to reach GA status in the future.

## Languages

All functions in a function app must share the same language. You choose the language of functions in your function app when you create the app. The language of your function app is maintained in the [FUNCTIONS_WORKER_RUNTIME](functions-app-settings#functions_worker_runtime) setting, and can't be changed when there are existing functions.

Make sure to select your preferred development language at the [top of the article](#top).

The following table shows the .NET versions supported by Azure Functions.

The supported version of .NET depends on both your Functions runtime version and your selected execution model.

Your function app code runs in a separate .NET worker process. Use with [supported versions of .NET and .NET Framework](dotnet-isolated-process-guide#supported-versions). For more information, see [Guide for running C# Azure Functions in the isolated worker model](dotnet-isolated-process-guide).

| Supported version | Support level | Expected end-of-support date |
|---|---|---|
| .NET 10 | GA |
|

[November 10, 2026](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle)1[November 10, 2026](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle)[.NET Framework Support Policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework).1 .NET 9 previously had an expected end-of-support date of May 12, 2026. During the .NET 9 service window, the .NET team extended support for STS versions to 24 months, starting with .NET 9. For more information, see [the blog post](https://devblogs.microsoft.com/dotnet/dotnet-sts-releases-supported-for-24-months/).

.NET 6 was previously supported by the isolated worker model but reached the end of official support on [November 12, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).

.NET 7 was previously supported by the isolated worker model but reached the end of official support on [May 14, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).

For more information, see [Guide for running C# Azure Functions in the isolated worker model](dotnet-isolated-process-guide).

The following table shows the language versions supported for Java function apps:

| Supported version | Support level | Supported until |
|---|---|---|
Java 25 |
Preview | Pending* |
Java 21 |
GA | See
|

**Java 17**[Release and servicing roadmap](/en-us/java/openjdk/support#release-and-servicing-roadmap).**Java 11**[Release and servicing roadmap](/en-us/java/openjdk/support#release-and-servicing-roadmap).**Java 8**[Temurin support page](https://adoptium.net/support/).*The end-of-support date for Java 25 is determined when general availability (GA) is declared.

For more information on developing and running Java function apps, see [Azure Functions Java developer guide](functions-reference-java).

The following table shows the language versions supported for Node.js function apps:

| Supported version | Support level | Expected end-of-support date |
|---|---|---|
|

[Node.js 22](https://endoflife.date/nodejs)[Node.js 20](https://endoflife.date/nodejs)TypeScript is supported through transpiling to JavaScript. For more information, see [Azure Functions Node.js developer guide](functions-reference-node#supported-versions).

The following table shows the language version supported for PowerShell function apps:

| Supported version | Support level | Expected end-of-support date |
|---|---|---|
|

For more information, see [Azure Functions PowerShell developer guide](functions-reference-powershell).

The following table shows the language versions supported for Python function apps:

| Supported version | Support level | Expected end-of-support date |
|---|---|---|
| Python 3.13 | GA | October 2029 |
| Python 3.12 | GA | October 2028 |
| Python 3.11 | GA | October 2027 |
| Python 3.10 | GA | October 2026 |

For more information, see [Azure Functions Python developer guide](functions-reference-python).

For information about planned changes to language support, see the [Azure roadmap updates](https://techcommunity.microsoft.com/search?q=functions+roadmap).

For information about the language versions of previously supported versions of the Functions runtime, see [Retired runtime versions](language-support-policy#language-support-related-resources).

## Run on a specific version

The version of the Functions runtime used by published apps in Azure is dictated by the [ FUNCTIONS_EXTENSION_VERSION](functions-app-settings#functions_extension_version) application setting. In some cases and for certain languages, other settings can apply.

By default, function apps created in the Azure portal, by the Azure CLI, or from Visual Studio tools are set to version 4.x. You can modify this version if needed. You can only downgrade the runtime version to 1.x after you create your function app but before you add any functions. Updating to a later major version is allowed even with apps that have existing functions.

### Migrating existing function apps

When your app has existing functions, you must take precautions before moving to a later major runtime version. The following articles detail breaking changes between major versions, including language-specific breaking changes. They also provide you with step-by-step instructions for a successful migration of your existing function app.

### Changing the version of apps in Azure

The following major runtime version values are used:

| Value | Runtime target |
|---|---|
`~4` |
4.x |
`~1` |
1.x |

Important

Don't arbitrarily change this app setting, because other app setting changes and changes to your function code might be required. For existing function apps, follow the [migration instructions](#migrating-existing-function-apps).

### Pinning to a specific minor version

To resolve issues that your function app could have when running on the latest major version, you must temporarily pin your app to a specific minor version. Pinning gives you time to get your app running correctly on the latest major version. The way that you pin to a minor version differs between Windows and Linux. To learn more, see [How to target Azure Functions runtime versions](set-runtime-version).

Older minor versions are periodically removed from Functions. For the latest news about Azure Functions releases, including the removal of specific older minor versions, monitor [Azure App Service announcements](https://github.com/Azure/app-service-announcements/issues).

## Minimum extension versions

There's technically not a correlation between binding extension versions and the Functions runtime version. However, starting with version 4.x the Functions runtime enforces a minimum version for all trigger and binding extensions.

If you receive a warning about a package not meeting a minimum required version, you should update that NuGet package to the minimum version as you normally would. The minimum version requirements for extensions used in Functions v4.x can be found in [the linked configuration file](https://github.com/Azure/azure-functions-host/blob/dev/src/WebJobs.Script/extensionrequirements.json).

For C# script, update the extension bundle reference in the *host.json* as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


There's technically not a correlation between extension bundle versions and the Functions runtime version. However, starting with version 4.x the Functions runtime enforces a minimum version for extension bundles.

If you receive a warning about your extension bundle version not meeting a minimum required version, update your existing extension bundle reference in the *host.json* as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


To learn more about extension bundles, see [Extension bundles](extension-bundles).

## Retired versions

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

These versions of the Functions runtime reached the end of extended support on December 13, 2022.

| Version | Current support level | Previous support level |
|---|---|---|
| 3.x | Out of support | GA |
| 2.x | Out of support | GA |

As soon as possible, you should migrate your apps to version 4.x to obtain full support. For a complete set of language-specific migration instructions, see [Migrate apps to Azure Functions version 4.x](migrate-version-3-version-4).

Apps using versions 2.x and 3.x can still be created and deployed from your CI/CD DevOps pipeline, and all existing apps continue to run without breaking changes. However, your apps aren't eligible for new features, security patches, and performance optimizations. You can only get related service support after you upgrade your apps to version 4.x.

Versions 2.x and 3.x are no longer supported due to the end of support for .NET Core 3.1, which was a core dependency. This requirement affects all [languages supported by Azure Functions](supported-languages).

## Locally developed application versions

You can make the following updates to function apps to locally change the targeted versions.

### Visual Studio runtime versions

In Visual Studio, you select the runtime version when you create a project. Azure Functions tools for Visual Studio supports the two major runtime versions. The correct version is used when debugging and publishing based on project settings. The version settings are defined in the *.csproj* file in the following properties:

```
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
```


If you're using the [isolated worker model](dotnet-isolated-process-guide), you can choose, `net9.0`

, `net8.0`

, or `net48`

as the target framework. You can also choose to use [preview support](dotnet-isolated-process-guide#preview-net-versions) for `net10.0`

. If you're using the [in-process model](functions-dotnet-class-library), you can choose `net8.0`

or `net6.0`

, and you must include the `Microsoft.NET.Sdk.Functions`

extension set to at least `4.4.0`

. .NET 10 is not supported by the in-process model; if you are on the in-process model and wish to use .NET 10, [migrate your app to the isolated worker model](migrate-dotnet-to-isolated-model).

.NET 6 was previously supported on the isolated worker model and the in-process model, but it reached the end of official support on [November 12, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).
.NET 7 was previously supported on the isolated worker model but reached the end of official support on [May 14, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).

### Visual Studio Code and Azure Functions Core Tools

[Azure Functions Core Tools](functions-run-local) is used for command-line development and also by the [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) for Visual Studio Code. For more information, see [Install the Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools).

For Visual Studio Code development, you might also need to update the user setting for the `azureFunctions.projectRuntime`

to match the version of the tools installed. This setting also updates the templates and languages used during function app creation.

## Bindings

Starting with version 2.x, the runtime uses a new [binding extensibility model](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) that offers these advantages:

Support for non-Microsoft binding extensions.

Decoupling of runtime and bindings. This change allows binding extensions to be versioned and released independently. You can, for example, opt to upgrade to a version of an extension that relies on a newer version of an underlying SDK.

A lighter execution environment, where only the bindings in use are known and loaded by the runtime.


Except for HTTP and timer triggers, all bindings must be explicitly added to the function app project, or registered in the portal. For more information, see [Azure Functions binding expression patterns](functions-bindings-expressions-patterns).

This table shows the bindings that are supported in the major versions of the Azure Functions runtime:

| Type | 4.x1 |
1.x2 |
Trigger | Input | Output |
|---|---|---|---|---|---|
|

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)[Azure Data Explorer](functions-bindings-azure-data-explorer)[Azure SQL](functions-bindings-azure-sql)[Dapr](functions-bindings-dapr)4[Event Grid](functions-bindings-event-grid)[Event Hubs](functions-bindings-event-hubs)[HTTP and webhooks](functions-bindings-http-webhook)[IoT Hub](functions-bindings-event-iot)[Kafka](functions-bindings-kafka)3[Mobile Apps](functions-bindings-mobile-apps)[Model Context Protocol](functions-bindings-mcp)[Notification Hubs](functions-bindings-notification-hubs)[Queue Storage](functions-bindings-storage-queue)[Redis](functions-bindings-cache)[RabbitMQ](functions-bindings-rabbitmq)3[SendGrid](functions-bindings-sendgrid)[Service Bus](functions-bindings-service-bus)[Azure SignalR Service](functions-bindings-signalr-service)[Table Storage](functions-bindings-storage-table)[Timer](functions-bindings-timer)[Twilio](functions-bindings-twilio)- Register all bindings except HTTP and timer. See
[Register Azure Functions binding extensions](functions-bindings-register). This step isn't required when using version 1.x of the Functions runtime. [Support ends for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1).[Migrate your apps to version 4.x](migrate-version-1-version-4)for full support.- Triggers aren't supported in the Consumption plan. This binding type requires
[runtime-driven triggers](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers). - This binding type is supported in Kubernetes, Azure IoT Edge, and other self-hosted modes only.

## Function app timeout duration

The `functionTimeout`

property in the [host.json](functions-host-json#functiontimeout) project file sets the timeout duration for functions in a function app. This property applies specifically to function executions. After the trigger starts function execution, the function needs to return or respond within the timeout duration. When an execution exceeds this duration, a timeout error occurs and the language worker process restarts. For C# apps running in-process, the host process itself restarts. To avoid timeouts and subsequent process restarts, it's important to [write robust functions](functions-best-practices#write-robust-functions). For more information, see [Improve Azure Functions performance and reliability](performance-reliability#make-sure-background-tasks-complete).

The following table shows the default and maximum values (in minutes) for specific plans:

| Plan | Default | Maximum1 |
|---|---|---|
|
30 | Unbounded2 |
|
304 |
Unbounded2 |
|
304 |
Unbounded3 |
|
30 | Unbounded5 |
|
5 | 10 |

- Regardless of the function app timeout setting, 230 seconds is the maximum amount of time that an HTTP triggered function can take to respond to a request. This limit exists because of the
[default idle timeout of Azure Load Balancer](../app-service/faq-availability-performance-application-issues#why-does-my-request-time-out-after-230-seconds). For longer processing times, consider using the[Durable Functions async pattern](durable/durable-functions-overview#async-http)or[defer the actual work and return an immediate response](performance-reliability#avoid-long-running-functions). - There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors)for the Flex Consumption and Premium plans, and a grace period of 10 minutes is given during platform updates. - Requires the App Service plan be set to
[Always On](/en-us/azure/azure-functions/dedicated-plan#always-on). A grace period of 10 minutes is given during platform updates. - The default timeout for version 1.x of the Functions host runtime is
*unbounded*. - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to zero, the default timeout depends on the specific triggers used in the app.

These values assume that the Azure Functions host process starts and runs correctly. There's a maximum timeout of 60 seconds for the language-specific worker process to also start. The worker process startup timeout isn't currently configurable.

## Related content

For more information, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: __python-memory-profiler-reference__dedicated-plan_functions-bindings-azure-data_243f17.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _python-memory-profiler-reference__dedicated-plan_functions-bindings-azure-data-_7022ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: python-memory-profiler-reference.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/python-memory-profiler-reference -->

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

<!-- DOCUMENTO FUSIONADO: _dedicated-plan_functions-bindings-azure-data-explorer.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: dedicated-plan.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/dedicated-plan -->

# Dedicated hosting plans for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article is about hosting your function app with dedicated resources in an App Service plan, including in an App Service Environment (ASE). For other hosting options, see the [hosting plan article](functions-scale).

An App Service plan defines a set of dedicated compute resources for an app to run. These dedicated compute resources are analogous to the [ server farm](https://wikipedia.org/wiki/Server_farm) in conventional hosting. One or more function apps can be configured to run on the same computing resources (App Service plan) as other App Service apps, such as web apps. The dedicated App Service plans supported for function app hosting include Basic, Standard, Premium, and Isolated SKUs. For details about how the App Service plan works, see the

[Azure App Service plans in-depth overview](../app-service/overview-hosting-plans).

Important

Free and Shared tier App Service plans aren't supported by Azure Functions. For a lower-cost option hosting your function executions, you should instead consider the [Consumption plan](consumption-plan) or the [Flex Consumption plan](flex-consumption-plan), where you are billed based on function executions.

Consider a dedicated App Service plan in the following situations:

- You have existing, underutilized VMs that are already running other App Service instances.
- You want to provide a custom image on which to run your functions.

## Billing

You pay for function apps in an App Service Plan as you would for other App Service resources. This differs from Azure Functions [Consumption plan](consumption-plan) or [Premium plan](functions-premium-plan) hosting, which have consumption-based cost components. You are billed only for the plan, regardless of how many function apps or web apps run in the plan. To learn more, see the [App Service pricing page](https://azure.microsoft.com/pricing/details/app-service/windows/).

## Always On

When you run your app on an App Service plan, you should enable the **Always on** setting so that your function app runs correctly. On an App Service plan, the Functions runtime goes idle after a few minutes of inactivity. The **Always on** setting is available only on an App Service plan. In other plans, the platform activates function apps automatically. If you choose not to enable **Always on**, you can reactivate an idled app in these ways:

- Send a request to an HTTP trigger endpoint or any other endpoint on the app. Even a failed request should wake up your app.
- Access your app in the
[Azure portal](https://portal.azure.com).

Even with **Always on** enabled, the execution timeout for individual functions is controlled by the `functionTimeout`

setting in the [host.json](functions-host-json#functiontimeout) project file.

## Scaling

Using an App Service plan, you can manually scale out by adding more VM instances. You can also enable autoscale, though autoscale will be slower than the elastic scale of the Premium plan. For more information, see [Scale instance count manually or automatically](/en-us/azure/azure-monitor/autoscale/autoscale-get-started?toc=%2fazure%2fapp-service%2ftoc.json). You can also scale up by choosing a different App Service plan. For more information, see [Scale up an app in Azure](../app-service/manage-scale-up).

Note

When running JavaScript (Node.js) functions on an App Service plan, you should choose a plan that has fewer vCPUs. For more information, see [Choose single-core App Service plans](functions-reference-node#choose-single-vcpu-app-service-plans).

## App Service Environments

Running in an App Service Environment (ASE) lets you fully isolate your functions and take advantage of higher numbers of instances than an App Service Plan. To get started, see [Introduction to the App Service Environments](../app-service/environment/overview).

If you just want to run your function app in a virtual network, you can do this using the [Premium plan](functions-premium-plan). To learn more, see [Establish Azure Functions private site access](functions-create-private-site-access).


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-azure-data-explorer.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-data-explorer -->

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

<!-- DOCUMENTO FUSIONADO: functions-develop-local.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-local -->

# Code and test Azure Functions locally

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Whenever possible, you should create and validate your Azure Functions code project in a local development environment. Azure Functions Core Tools provides a local runtime version of Azure Functions that integrates with popular development tools for an integrated development, debugging, and deployments. Your local functions can even connect to live Azure services.

This article provides some shared guidance for local development, such as working with the [local.settings.json file](#local-settings-file). It also links to development environment-specific guidance.

Tip

You can find detailed information about how to develop functions locally in the linked IDE-specific guidance articles.

## Local development environments

The way in which you develop functions on your local computer depends on your [language](supported-languages) and tooling preferences. Make sure to choose your preferred language at the [top of the article](#top).

Tip

All local development relies on Azure Functions Core Tools to provide the Functions runtime for debugging in a local environment.

You can use these development environments to code functions locally in your preferred language:

| Environment | Description |
|---|---|
|

**Azure development**workload of[Visual Studio](https://www.visualstudio.com/vs/). Lets you compile and deploy your C# function code to Azure as a .NET class library. Includes the Core Tools for local testing. To learn more, see[Create your first C# function in Azure using Visual Studio](functions-create-your-first-function-visual-studio)[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a C# function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-csharp).| Environment | Description |
|---|---|
|

[Create your first function with Java and Maven](how-to-create-function-azure-cli?pivots=programming-language-java).[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-java).[IntelliJ IDEA](functions-create-maven-intellij)[Create your first Java function in Azure using IntelliJ](functions-create-maven-intellij).[Eclipse](functions-create-maven-eclipse)[Create your first Java function in Azure using Ecplise](functions-create-maven-eclipse).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a Node.js function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-javascript).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-powershell).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a PowerShell function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-powershell).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a Python function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-python).Each of these local development environments lets you create function app projects and use predefined function templates to create new functions. Each uses the Core Tools so that you can test and debug your functions against the real Functions runtime on your own machine just as you would any other app. You can also publish your function app project from any of these environments to Azure.

## Local project files

A Functions project directory contains the following files in the project root folder, regardless of language:

| File name | Description |
|---|---|
| host.json | To learn more, see the
|

[local settings file](#local-settings-file).[local settings file](#local-settings-file).Other files in the project depend on your language and specific functions. For more information, see the developer guide for your language.

### Local settings file

The `local.settings.json`

file stores app settings and settings used by local development tools. Settings in the `local.settings.json`

file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.

Important

Because the `local.settings.json`

file might contain secrets, such as connection strings, you should use caution committing to source control. Tools that support Functions provide ways to synchronize settings in the `local.settings.json`

file with the [app settings](functions-how-to-use-azure-function-app-settings#settings) in the function app to which your project is deployed.

The `local.settings.json`

file has this structure:

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "<language worker>",
"AzureWebJobsStorage": "<connection-string>",
"MyBindingConnection": "<binding-connection-string>",
"AzureWebJobs.HttpExample.Disabled": "true"
},
"Host": {
"LocalHttpPort": 7071,
"CORS": "*",
"CORSCredentials": false
},
"ConnectionStrings": {
"SQLConnectionString": "<sqlclient-connection-string>"
}
}
```


These settings are supported when you run projects locally:

| Setting | Description |
|---|---|
`IsEncrypted` |
When this setting is set to `true` , all values are encrypted with a local machine key. Used with `func settings` commands. Default value is `false` . You might want to encrypt the local.settings.json file on your local computer when it contains secrets, such as service connection strings. The host automatically decrypts settings when it runs. Use the `func settings decrypt` command before trying to read locally encrypted settings. |
`Values` |
Collection of application settings used when a project is running locally. These key-value (string-string) pairs correspond to application settings in your function app in Azure, like
`AzureWebJobsStorage` |

`Connection`

for the [Blob storage trigger](functions-bindings-storage-blob-trigger#configuration). For these properties, you need an application setting defined in the

`Values`

array. See the subsequent table for a list of commonly used settings. Values must be strings and not JSON objects or arrays. Setting names can't include a double underline (

`__`

) and shouldn't include a colon (`:`

). Double underline characters are reserved by the runtime, and the colon is reserved to support [dependency injection](functions-dotnet-dependency-injection#working-with-options-and-settings).

`Host`

`LocalHttpPort`

`func host start`

and `func run`

). The `--port`

command-line option takes precedence over this setting. For example, when running in Visual Studio IDE, you may change the port number by navigating to the "Project Properties -> Debug" window and explicitly specifying the port number in a `host start --port <your-port-number>`

command that can be supplied in the "Application Arguments" field.`CORS`

[cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Origins are supplied as a comma-separated list with no spaces. The wildcard value (*) is supported, which allows requests from any origin.`CORSCredentials`

`true`

, allows `withCredentials`

requests.`ConnectionStrings`

`ConnectionStrings`

section of a configuration file, like [Entity Framework](/en-us/ef/ef6/). Connection strings in this object are added to the environment with the provider type of[System.Data.SqlClient](/en-us/dotnet/api/system.data.sqlclient). Items in this collection aren't published to Azure with other app settings. You must explicitly add these values to the`Connection strings`

collection of your function app settings. If you're creating a [in your function code, you should store the connection string value with your other connections in](/en-us/dotnet/api/system.data.sqlclient.sqlconnection)`SqlConnection`

**Application Settings**in the portal.The following application settings can be included in the ** Values** array when running locally:

| Setting | Values | Description |
|---|---|---|
`AzureWebJobsStorage` |
Storage account connection string, or`UseDevelopmentStorage=true` |
Contains the connection string for an Azure storage account. Required when using triggers other than HTTP. For more information, see the
`AzureWebJobsStorage` |

When you have the

[Azurite Emulator](../storage/common/storage-use-azurite)installed locally and you set

[to](functions-app-settings#azurewebjobsstorage)

`AzureWebJobsStorage`

`UseDevelopmentStorage=true`

, Core Tools uses the emulator. For more information, see [Local storage emulator](#local-storage-emulator).

`AzureWebJobs.<FUNCTION_NAME>.Disabled`

`true`

|`false`

`"AzureWebJobs.<FUNCTION_NAME>.Disabled": "true"`

to the collection, where `<FUNCTION_NAME>`

is the name of the function. To learn more, see [How to disable functions in Azure Functions](disable-function#disable-functions-locally).`FUNCTIONS_WORKER_RUNTIME`

`dotnet`

`dotnet-isolated`

`node`

`java`

`powershell`

`python`

[reference.](functions-app-settings#functions_worker_runtime)`FUNCTIONS_WORKER_RUNTIME`

`FUNCTIONS_WORKER_RUNTIME_VERSION`

`~7`

`powerShellVersion`

site configuration setting, when it runs in Azure, which can be [set in the portal](functions-reference-powershell#changing-the-powershell-version).To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-node#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-java#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-powershell#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-python#environment-variables) in the developer guide.

## Synchronize settings

When you develop your functions locally, any local settings required by your app must also be present in app settings of the function app to which your code is deployed. You might also need to download current settings from the function app to your local project. While you can [manually configure app settings in the Azure portal](functions-how-to-use-azure-function-app-settings?tabs=portal#settings), the following tools also let you synchronize app settings with local settings in your project:

## Triggers and bindings

When you develop your functions locally, you need to take trigger and binding behaviors into consideration. For HTTP triggers, you can call the HTTP endpoint on the local computer, using `http://localhost/`

. For non-HTTP triggered functions, there are several options to run locally:

- The easiest way to test bindings during local development is to use connection strings that target live Azure services. You can target live services by adding the appropriate connection string settings in the
`Values`

array in the local.settings.json file. When you do this, local executions during testing might affect your production services. Instead, consider setting-up separate services to use during development and testing, and then switch to different services during production. - For storage-based triggers, you can use a
[local storage emulator](#local-storage-emulator). - You can manually run non-HTTP trigger functions by using special administrator endpoints. For more information, see
[Manually run a non-HTTP-triggered function](functions-manually-run-non-http).

During local testing, you must be running the host provided by Core Tools (func.exe) locally. For more information, see [Azure Functions Core Tools](functions-run-local).

## HTTP test tools

During development, it's easy to call any of your function endpoints from a web browser when they support the HTTP GET method. However, for other HTTP methods that support payloads, such as POST or PUT, you need to use an HTTP test tool to create and send these HTTP requests to your function endpoints.

Caution

For scenarios where your requests must include sensitive data, make sure to use a tool that protects your data and reduces the risk of exposing any sensitive data to the public. Sensitive data you should protect might include: credentials, secrets, access tokens, API keys, geolocation data, even personal data.

You can keep your data secure by choosing an HTTP test tool that works either offline or locally, doesn't sync your data to the cloud, and doesn't require that you sign in to an online account. Some tools can also protect your data from accidental exposure by implementing specific security features.

Avoid using tools that centrally store your HTTP request history (including sensitive information), don't follow best security practices, or don't respect data privacy concerns.

Consider using one of these tools for securely sending HTTP requests to your function endpoints:

[Visual Studio Code](https://code.visualstudio.com/download)with an[extension from Visual Studio Marketplace](https://marketplace.visualstudio.com/vscode), such as[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)[PowerShell Invoke-RestMethod](/en-us/powershell/module/microsoft.powershell.utility/invoke-restmethod)[Microsoft Edge - Network Console tool](/en-us/microsoft-edge/devtools-guide-chromium/network-console/network-console-tool)[Bruno](https://www.usebruno.com/)[curl](https://curl.se/)

## Local storage emulator

During local development, you can use the local [Azurite emulator](../storage/common/storage-use-azurite) when testing functions with Azure Storage bindings (Queue Storage, Blob Storage, and Table Storage), without having to connect to remote storage services. Azurite integrates with Visual Studio Code and Visual Studio, and you can also run it from the command prompt using npm. For more information, see [Use the Azurite emulator for local Azure Storage development](../storage/common/storage-use-azurite).

The following setting in the `Values`

collection of the local.settings.json file tells the local Functions host to use Azurite for the default `AzureWebJobsStorage`

connection:

```
"AzureWebJobsStorage": "UseDevelopmentStorage=true"
```


With this setting value, any Azure Storage trigger or binding that uses `AzureWebJobsStorage`

as its connection connects to Azurite when running locally. Keep these considerations in mind when using storage emulation during local execution:

- You must have Azurite installed and running.
- You should test with an actual storage connection to Azure services before publishing to Azure.
- When you publish your project, don't publish the
`AzureWebJobsStorage`

setting as`UseDevelopmentStorage=true`

. In Azure, the`AzureWebJobsStorage`

setting must always be the connection string of the storage account used by your function app. For more information, see.`AzureWebJobsStorage`


## Related articles

- To learn more about local development of functions using Visual Studio, see
[Develop Azure Functions using Visual Studio](functions-develop-vs).

- To learn more about local development of functions using Visual Studio Code on a Mac, Linux, or Windows computer, see
[Develop Azure Functions by using Visual Studio Code](functions-develop-vs-code). - To learn more about developing functions from the command prompt or terminal, see
[Work with Azure Functions Core Tools](functions-run-local).
