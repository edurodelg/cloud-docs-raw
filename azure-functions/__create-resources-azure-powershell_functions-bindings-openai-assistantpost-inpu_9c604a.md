---
merged_at: 2026-01-25T15:41:11.636118
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _create-resources-azure-powershell_functions-bindings-openai-assistantpost-input.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: create-resources-azure-powershell.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/create-resources-azure-powershell -->

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

<!-- DOCUMENTO FUSIONADO: functions-bindings-openai-assistantpost-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistantpost-input -->

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

<!-- DOCUMENTO FUSIONADO: functions-dotnet-class-library.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-dotnet-class-library -->

# Develop legacy C# class library functions using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

This article is an introduction to developing Azure Functions by using C# in .NET class libraries. These class libraries are used to run *in-process with the Functions runtime*. Your .NET functions can alternatively run _isolated from the Functions *runtime*, which offers several advantages. To learn more, see [the isolated worker model](dotnet-isolated-process-guide). For a comprehensive comparison between these two models, see [Differences between the in-process model and the isolated worker model](dotnet-isolated-in-process-differences).

Important

This article supports .NET class library functions that run in-process with the runtime. Your C# functions can also run out-of-process and isolated from the Functions runtime. The isolated worker process model is the only way to run non-LTS versions of .NET and .NET Framework apps in current versions of the Functions runtime. To learn more, see [.NET isolated worker process functions](dotnet-isolated-process-guide).
For a comprehensive comparison between isolated worker process and in-process .NET Functions, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

As a C# developer, you might also be interested in one of the following articles:

| Getting started | Concepts | Guided learning/samples |
|---|---|---|

Azure Functions supports C# and C# script programming languages. If you're looking for guidance on [using C# in the Azure portal](functions-create-function-app-portal), see [C# script (.csx) developer reference](functions-reference-csharp).

## Supported versions

Versions of the Functions runtime support specific versions of .NET. To learn more about Functions versions, see [Azure Functions runtime versions overview](functions-versions). Version support also depends on whether your functions run in-process or isolated worker process.

Note

To learn how to change the Functions runtime version used by your function app, see [view and update the current runtime version](set-runtime-version#view-the-current-runtime-version).

The following table shows the highest level of .NET or .NET Framework that can be used with a specific version of Functions.

| Functions runtime version |
|
|---|

[In-process model](functions-dotnet-class-library)

4

15.NET 9.0

.NET 8.0

.NET Framework 4.8

231 .NET 6 was previously supported on both models but reached the [end of official support](https://dotnet.microsoft.com/platform/support/policy) on November 12, 2024. .NET 7 was previously supported on the isolated worker model but reached the [end of official support](https://dotnet.microsoft.com/platform/support/policy) on May 14, 2024.

2 The build process also requires the [.NET SDK](https://dotnet.microsoft.com/download).

3 Support ends for version 1.x of the Azure Functions runtime on September 14, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/hostv1). For continued full support, you should [migrate your apps to version 4.x](migrate-version-1-version-4).

4 Support ends for the in-process model on November 10, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/in-process-model). For continued full support, you should [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

5 You can't run .NET 10 apps on Linux in the Consumption plan. To run on Linux, you should instead use the [Flex Consumption plan](flex-consumption-plan). For step-by-step migration instructions, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex?pivots=platform-linux).

For the latest news about Azure Functions releases, including the removal of specific older minor versions, monitor [Azure App Service announcements](https://github.com/Azure/app-service-announcements/issues).

### Updating to target .NET 8

Apps using the in-process model can target .NET 8 by following the steps outlined in this section. However, if you choose to exercise this option, you should still begin planning your [migration to the isolated worker model](migrate-dotnet-to-isolated-model) in advance of [support ending for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model).

Many apps can change the configuration of the function app in Azure without updates to code or redeployment. To run .NET 8 with the in-process model, three configurations are required:

- The
[application setting](functions-how-to-use-azure-function-app-settings)`FUNCTIONS_WORKER_RUNTIME`

must be set with the value "dotnet". - The application setting
`FUNCTIONS_EXTENSION_VERSION`

must be set with the value "~4". - The application setting
`FUNCTIONS_INPROC_NET8_ENABLED`

must be set with the value "1". - You must
[update the stack configuration](update-language-versions#update-the-stack-configuration)to reference .NET 8.

Support for .NET 8 still uses version 4.x of the Functions runtime, and no change to the configured runtime version is required.

To update your local project, first make sure you're using the latest versions of local tools. Then ensure that the project references [version 4.4.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.4.0). You can then change your `TargetFramework`

to "net8.0". You must also update `local.settings.json`

to include both `FUNCTIONS_WORKER_RUNTIME`

set to "dotnet" and `FUNCTIONS_INPROC_NET8_ENABLED`

set to "1".

The following example is a minimal `project`

file with these changes:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="4.4.0" />
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


The following example is a minimal `local.settings.json`

file with these changes:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_INPROC_NET8_ENABLED": "1",
"FUNCTIONS_WORKER_RUNTIME": "dotnet"
}
}
```


If your app uses [ Microsoft.Azure.DurableTask.Netherite.AzureFunctions](https://www.nuget.org/packages/Microsoft.Azure.DurableTask.Netherite.AzureFunctions), ensure it targets version 1.5.3 or later. Due to a behavior change in .NET 8, apps with older versions of the package throw an ambiguous constructor exception.

You might need to make other changes to your app based on the version support of its other dependencies.

Version 4.x of the Functions runtime provides equivalent functionality for .NET 6 and .NET 8. The in-process model doesn't include other features or updates that integrate with new .NET 8 capabilities. For example, the runtime doesn't support keyed services. To take full advantage of the latest .NET 8 capabilities and enhancements, you must [migrate to the isolated worker model](migrate-dotnet-to-isolated-model).

## Functions class library project

In Visual Studio, the **Azure Functions** project template creates a C# class library project that contains the following files:

[host.json](functions-host-json)- stores configuration settings that affect all functions in the project when running locally or in Azure.[local.settings.json](functions-develop-local#local-settings-file)- stores app settings and connection strings that are used when running locally. This file contains secrets and isn't published to your function app in Azure. Instead,[add app settings to your function app](functions-develop-vs#function-app-settings).

When you build the project, a folder structure that looks like the following example is generated in the build output directory:

```
<framework.version>
| - bin
| - MyFirstFunction
| | - function.json
| - MySecondFunction
| | - function.json
| - host.json
```


This directory is what gets deployed to your function app in Azure. The binding extensions required in [version 2.x](functions-versions) of the Functions runtime are [added to the project as NuGet packages](functions-develop-vs?tabs=in-process#add-bindings).

Important

The build process creates a *function.json* file for each function. This *function.json* file isn't meant to be edited directly. You can't change binding configuration or disable the function by editing this file. To learn how to disable a function, see [How to disable functions](disable-function).

## Methods recognized as functions

In a class library, a function is a method with a `FunctionName`

and a trigger attribute, as shown in the following example:

```
public static class SimpleExample
{
[FunctionName("QueueTrigger")]
public static void Run(
[QueueTrigger("myqueue-items")] string myQueueItem,
ILogger log)
{
log.LogInformation($"C# function processed: {myQueueItem}");
}
}
```


The `FunctionName`

attribute marks the method as a function entry point. The name must be unique within a project, start with a letter and only contain letters, numbers, `_`

, and `-`

, up to 127 characters in length. Project templates often create a method named `Run`

, but the method name can be any valid C# method name. The preceding example shows a static method being used, but functions aren't required to be static.

The trigger attribute specifies the trigger type and binds input data to a method parameter. The example function is triggered by a queue message, and the queue message is passed to the method in the `myQueueItem`

parameter.

## Method signature parameters

The method signature might contain parameters other than the one used with the trigger attribute. Here are some of the other parameters that you can include:

[Input and output bindings](functions-triggers-bindings)marked as such by decorating them with attributes.- An
`ILogger`

or`TraceWriter`

([version 1.x-only](functions-versions#creating-1x-apps)) parameter for[logging](#logging). - A
`CancellationToken`

parameter for[graceful shutdown](#cancellation-tokens). [Binding expressions](functions-bindings-expressions-patterns)parameters to get trigger metadata.

The order of parameters in the function signature doesn't matter. For example, you can put trigger parameters before or after other bindings, and you can put the logger parameter before or after trigger or binding parameters.

### Output bindings

A function can have zero or multiple output bindings defined by using output parameters.

The following example modifies the preceding one by adding an output queue binding named `myQueueItemCopy`

. The function writes the contents of the message that triggers the function to a new message in a different queue.

```
public static class SimpleExampleWithOutput
{
[FunctionName("CopyQueueMessage")]
public static void Run(
[QueueTrigger("myqueue-items-source")] string myQueueItem,
[Queue("myqueue-items-destination")] out string myQueueItemCopy,
ILogger log)
{
log.LogInformation($"CopyQueueMessage function processed: {myQueueItem}");
myQueueItemCopy = myQueueItem;
}
}
```


Values assigned to output bindings are written when the function exits. You can use more than one output binding in a function by assigning values to multiple output parameters.

The binding reference articles ([Storage queues](functions-bindings-storage-queue), for example) explain which parameter types you can use with trigger, input, or output binding attributes.

### Binding expressions example

The following code gets the name of the queue to monitor from an app setting, and it gets the queue message creation time in the `insertionTime`

parameter.

```
public static class BindingExpressionsExample
{
[FunctionName("LogQueueMessage")]
public static void Run(
[QueueTrigger("%queueappsetting%")] string myQueueItem,
DateTimeOffset insertionTime,
ILogger log)
{
log.LogInformation($"Message content: {myQueueItem}");
log.LogInformation($"Created at: {insertionTime}");
}
}
```


## Autogenerated function.json

The build process creates a *function.json* file in a function folder in the build folder. As noted earlier, this file isn't meant to be edited directly. You can't change binding configuration or disable the function by editing this file.

The purpose of this file is to provide information to the scale controller to use for [scaling decisions on the Consumption plan](event-driven-scaling). For this reason, the file only has trigger info, not input/output bindings.

The generated *function.json* file includes a `configurationSource`

property that tells the runtime to use .NET attributes for bindings, rather than *function.json* configuration. Here's an example:

```
{
"generatedBy": "Microsoft.NET.Sdk.Functions-1.0.0.0",
"configurationSource": "attributes",
"bindings": [
{
"type": "queueTrigger",
"queueName": "%input-queue-name%",
"name": "myQueueItem"
}
],
"disabled": false,
"scriptFile": "..\\bin\\FunctionApp1.dll",
"entryPoint": "FunctionApp1.QueueTrigger.Run"
}
```


## Microsoft.NET.Sdk.Functions

The *function.json* file generation is performed by the NuGet package [Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).

The following example shows the relevant parts of the `.csproj`

files that have different target frameworks of the same `Sdk`

package:

```
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="4.5.0" />
</ItemGroup>
```


Important

Starting with version 4.0.6517 of the Core Tools, in-process model projects must reference [version 4.5.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.5.0). If an earlier version is used, the

`func start`

command will error.Among the `Sdk`

package dependencies are triggers and bindings. A 1.x project refers to 1.x triggers and bindings because those triggers and bindings target the .NET Framework, while 4.x triggers and bindings target .NET Core.

The `Sdk`

package also depends on [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json), and indirectly on [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage). These dependencies make sure that your project uses the versions of those packages that work with the Functions runtime version that the project targets. For example, `Newtonsoft.Json`

has version 11 for .NET Framework 4.6.1, but the Functions runtime that targets .NET Framework 4.6.1 is only compatible with `Newtonsoft.Json`

9.0.1. So your function code in that project also has to use `Newtonsoft.Json`

9.0.1.

The source code for `Microsoft.NET.Sdk.Functions`

is available in the GitHub repo [azure-functions-vs-build-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## Local runtime version

Visual Studio uses the [Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools) to run Functions projects on your local computer. The Core Tools is a command-line interface for the Functions runtime.

If you install the Core Tools using the Windows installer (MSI) package or by using npm, it doesn't affect the Core Tools version used by Visual Studio. For the Functions runtime version 1.x, Visual Studio stores Core Tools versions in *%USERPROFILE%\AppData\Local\Azure.Functions.Cli* and uses the latest version stored there. For Functions 4.x, the Core Tools are included in the **Azure Functions and Web Jobs Tools** extension. For Functions 1.x, you can see what version is being used in the console output when you run a Functions project:

```
[3/1/2018 9:59:53 AM] Starting Host (HostId=contoso2-1518597420, Version=2.0.11353.0, ProcessId=22020, Debug=False, Attempt=0, FunctionsExtensionVersion=)
```


## ReadyToRun

You can compile your function app as [ReadyToRun binaries](/en-us/dotnet/core/deploying/ready-to-run). ReadyToRun is a form of ahead-of-time compilation that can improve startup performance to help reduce the impact of [cold-start](event-driven-scaling#cold-start) when running in a [Consumption plan](consumption-plan).

ReadyToRun is available in .NET 6 and later versions and requires [version 4.0 of the Azure Functions runtime](functions-versions).

To compile your project as ReadyToRun, update your project file by adding the `<PublishReadyToRun>`

and `<RuntimeIdentifier>`

elements. The following example is the configuration for publishing to a Windows 32-bit function app.

```
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
<PublishReadyToRun>true</PublishReadyToRun>
<RuntimeIdentifier>win-x86</RuntimeIdentifier>
</PropertyGroup>
```


Important

Starting in .NET 6, support for Composite ReadyToRun compilation has been added. Check out [ReadyToRun Cross platform and architecture restrictions](/en-us/dotnet/core/deploying/ready-to-run).

You can also build your app with ReadyToRun from the command line. For more information, see the `-p:PublishReadyToRun=true`

option in [ dotnet publish](/en-us/dotnet/core/tools/dotnet-publish).

## Supported types for bindings

Each binding has its own supported types; for instance, a blob trigger attribute can be applied to a string parameter, a POCO parameter, a `CloudBlockBlob`

parameter, or any of several other supported types. The [binding reference article for blob bindings](functions-bindings-storage-blob-trigger#usage) lists all supported parameter types. For more information, see [Triggers and bindings](functions-triggers-bindings) and the [binding reference docs for each binding type](functions-triggers-bindings#related-content).

Tip

If you plan to use the HTTP or WebHook bindings, plan to avoid port exhaustion that can be caused by improper instantiation of `HttpClient`

. For more information, see [How to manage connections in Azure Functions](manage-connections).

## Binding to method return value

You can use a method return value for an output binding, by applying the attribute to the method return value. For examples, see [Triggers and bindings](functions-triggers-bindings).

Use the return value only if a successful function execution always results in a return value to pass to the output binding. Otherwise, use `ICollector`

or `IAsyncCollector`

, as shown in the following section.

## Writing multiple output values

To write multiple values to an output binding, or if a successful function invocation might not result in anything to pass to the output binding, use the [ ICollector](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or

[types. These types are write-only collections that are written to the output binding when the method completes.](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)

`IAsyncCollector`

This example writes multiple queue messages into the same queue using `ICollector`

:

```
public static class ICollectorExample
{
[FunctionName("CopyQueueMessageICollector")]
public static void Run(
[QueueTrigger("myqueue-items-source-3")] string myQueueItem,
[Queue("myqueue-items-destination")] ICollector<string> myDestinationQueue,
ILogger log)
{
log.LogInformation($"C# function processed: {myQueueItem}");
myDestinationQueue.Add($"Copy 1: {myQueueItem}");
myDestinationQueue.Add($"Copy 2: {myQueueItem}");
}
}
```


## Async

To make a function [asynchronous](/en-us/dotnet/csharp/programming-guide/concepts/async/), use the `async`

keyword and return a `Task`

object.

```
public static class AsyncExample
{
[FunctionName("BlobCopy")]
public static async Task RunAsync(
[BlobTrigger("sample-images/{blobName}")] Stream blobInput,
[Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
CancellationToken token,
ILogger log)
{
log.LogInformation($"BlobCopy function processed.");
await blobInput.CopyToAsync(blobOutput, 4096, token);
}
}
```


You can't use `out`

parameters in async functions. For output bindings, use the [function return value](#binding-to-method-return-value) or a [collector object](#writing-multiple-output-values) instead.

## Cancellation tokens

A function can accept a [CancellationToken](/en-us/dotnet/api/system.threading.cancellationtoken) parameter, which enables the operating system to notify your code when the function is about to be terminated. You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.

Consider the case when you have a function that processes messages in batches. The following Azure Service Bus-triggered function processes an array of [ServiceBusReceivedMessage](/en-us/dotnet/api/azure.messaging.servicebus.servicebusreceivedmessage) objects, which represents a batch of incoming messages to be processed by a specific function invocation:

```
using Azure.Messaging.ServiceBus;
using System.Threading;
namespace ServiceBusCancellationToken
{
public static class servicebus
{
[FunctionName("servicebus")]
public static void Run([ServiceBusTrigger("csharpguitar", Connection = "SB_CONN")]
ServiceBusReceivedMessage[] messages, CancellationToken cancellationToken, ILogger log)
{
try
{
foreach (var message in messages)
{
if (cancellationToken.IsCancellationRequested)
{
log.LogInformation("A cancellation token was received. Taking precautionary actions.");
//Take precautions like noting how far along you are with processing the batch
log.LogInformation("Precautionary activities --complete--.");
break;
}
else
{
//business logic as usual
log.LogInformation($"Message: {message} was processed.");
}
}
}
catch (Exception ex)
{
log.LogInformation($"Something unexpected happened: {ex.Message}");
}
}
}
}
```


## Logging

In your function code, you can write output to logs that appear as traces in Application Insights. The recommended way to write to the logs is to include a parameter of type [ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger), which is typically named `log`

. Version 1.x of the Functions runtime used `TraceWriter`

, which also writes to Application Insights, but doesn't support structured logging. Don't use `Console.Write`

to write your logs, since this data isn't captured by Application Insights.

### ILogger

In your function definition, include an [ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger) parameter, which supports [structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).

With an `ILogger`

object, you call `Log<level>`

[extension methods on ILogger](/en-us/dotnet/api/microsoft.extensions.logging.loggerextensions#methods) to create logs. The following code writes `Information`

logs with category `Function.<YOUR_FUNCTION_NAME>.User.`

:

```
public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, ILogger logger)
{
logger.LogInformation("Request for item with key={itemKey}.", id);
```


To learn more about how Functions implements `ILogger`

, see [Collecting telemetry data](functions-monitoring#collecting-telemetry-data). Categories prefixed with `Function`

assume you're using an `ILogger`

instance. If you choose to instead use an `ILogger<T>`

, the category name might instead be based on `T`

.

### Structured logging

The order of placeholders, not their names, determines which parameters are used in the log message. Suppose you have the following code:

```
string partitionKey = "partitionKey";
string rowKey = "rowKey";
logger.LogInformation("partitionKey={partitionKey}, rowKey={rowKey}", partitionKey, rowKey);
```


If you keep the same message string and reverse the order of the parameters, the resulting message text would have the values in the wrong places.

Placeholders are handled this way so that you can do structured logging. Application Insights stores the parameter name-value pairs and the message string. The result is that the message arguments become fields that you can query on.

If your logger method call looks like the previous example, you can query the field `customDimensions.prop__rowKey`

. The `prop__`

prefix is added to ensure there are no collisions between fields the runtime adds and fields your function code adds.

You can also query on the original message string by referencing the field `customDimensions.prop__{OriginalFormat}`

.

Here's a sample JSON representation of `customDimensions`

data:

```
{
"customDimensions": {
"prop__{OriginalFormat}":"C# Queue trigger function processed: {message}",
"Category":"Function",
"LogLevel":"Information",
"prop__message":"c9519cbf-b1e6-4b9b-bf24-cb7d10b1bb89"
}
}
```


### Log custom telemetry

There's a Functions-specific version of the Application Insights SDK that you can use to send custom telemetry data from your functions to Application Insights: [Microsoft.Azure.WebJobs.Logging.ApplicationInsights](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Logging.ApplicationInsights). Use the following command from the command prompt to install this package:

```
dotnet add package Microsoft.Azure.WebJobs.Logging.ApplicationInsights --version <VERSION>
```


In this command, replace `<VERSION>`

with a version of this package that supports your installed version of [Microsoft.Azure.WebJobs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs/).

The following C# examples uses the [custom telemetry API](/en-us/azure/azure-monitor/app/api-custom-events-metrics). The example is for a .NET class library, but the Application Insights code is the same for C# script.

Version 2.x and later versions of the runtime use newer features in Application Insights to automatically correlate telemetry with the current operation. There's no need to manually set the operation `Id`

, `ParentId`

, or `Name`

fields.

```
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;
using Microsoft.ApplicationInsights.Extensibility;
using System.Linq;
namespace functionapp0915
{
public class HttpTrigger2
{
private readonly TelemetryClient telemetryClient;
/// Using dependency injection will guarantee that you use the same configuration for telemetry collected automatically and manually.
public HttpTrigger2(TelemetryConfiguration telemetryConfiguration)
{
this.telemetryClient = new TelemetryClient(telemetryConfiguration);
}
[FunctionName("HttpTrigger2")]
public Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)]
HttpRequest req, ExecutionContext context, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
DateTime start = DateTime.UtcNow;
// Parse query parameter
string name = req.Query
.FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
.Value;
// Write an event to the customEvents table.
var evt = new EventTelemetry("Function called");
evt.Context.User.Id = name;
this.telemetryClient.TrackEvent(evt);
// Generate a custom metric, in this case let's use ContentLength.
this.telemetryClient.GetMetric("contentLength").TrackValue(req.ContentLength);
// Log a custom dependency in the dependencies table.
var dependency = new DependencyTelemetry
{
Name = "GET api/planets/1/",
Target = "swapi.co",
Data = "https://swapi.co/api/planets/1/",
Timestamp = start,
Duration = DateTime.UtcNow - start,
Success = true
};
dependency.Context.User.Id = name;
this.telemetryClient.TrackDependency(dependency);
return Task.FromResult<IActionResult>(new OkResult());
}
}
}
```


In this example, the custom metric data gets aggregated by the host before being sent to the customMetrics table. To learn more, see the [GetMetric](/en-us/azure/azure-monitor/app/api-custom-events-metrics#getmetric) documentation in Application Insights.

When running locally, you must add the `APPINSIGHTS_INSTRUMENTATIONKEY`

setting, with the Application Insights key, to the [local.settings.json](functions-develop-local#local-settings-file) file.

Don't call `TrackRequest`

or `StartOperation<RequestTelemetry>`

because you see duplicate requests for a function invocation. The Functions runtime automatically tracks requests.

Don't set `telemetryClient.Context.Operation.Id`

. This global setting causes incorrect correlation when many functions are running simultaneously. Instead, create a new telemetry instance (`DependencyTelemetry`

, `EventTelemetry`

) and modify its `Context`

property. Then pass in the telemetry instance to the corresponding `Track`

method on `TelemetryClient`

(`TrackDependency()`

, `TrackEvent()`

, `TrackMetric()`

). This method ensures that the telemetry has the correct correlation details for the current function invocation.

## Testing functions

The following articles show how to run an in-process C# class library function locally for testing purposes:

## Environment variables

To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`

, as shown in the following code example:

```
public static class EnvironmentVariablesExample
{
[FunctionName("GetEnvironmentVariables")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, ILogger log)
{
log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
log.LogInformation(GetEnvironmentVariable("AzureWebJobsStorage"));
log.LogInformation(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}
private static string GetEnvironmentVariable(string name)
{
return name + ": " +
System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
}
```


App settings can be read from environment variables both when developing locally and when running in Azure. When developing locally, app settings come from the `Values`

collection in the *local.settings.json* file. In both environments, local and Azure, `GetEnvironmentVariable("<app setting name>")`

retrieves the value of the named app setting. For instance, when you're running locally, "My Site Name" would be returned if your *local.settings.json* file contains `{ "Values": { "WEBSITE_SITE_NAME": "My Site Name" } }`

.

The [System.Configuration.ConfigurationManager.AppSettings](/en-us/dotnet/api/system.configuration.configurationmanager.appsettings) property is an alternative API for getting app setting values, but we recommend that you use `GetEnvironmentVariable`

as shown here.

## Binding at runtime

In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [ declarative](https://en.wikipedia.org/wiki/Declarative_programming) bindings in attributes. Imperative binding is useful when binding parameters need to be computed at runtime rather than design time. With this pattern, you can bind to supported input and output bindings on-the-fly in your function code.

Define an imperative binding as follows:

**Do not**include an attribute in the function signature for your desired imperative bindings.Pass in an input parameter

or`Binder binder`

.`IBinder binder`

Use the following C# pattern to perform the data binding.

`using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...))) { ... }`

`BindingTypeAttribute`

is the .NET attribute that defines your binding, and`T`

is an input or output type that's supported by that binding type.`T`

can't be an`out`

parameter type (such as`out JObject`

). For example, the Mobile Apps table output binding supports[six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use[ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs)or[IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)with imperative binding.

### Single attribute example

The following example code creates a [Storage blob output binding](functions-bindings-storage-blob-output) with blob path that's defined at run time, then writes a string to the blob.

```
public static class IBinderExample
{
[FunctionName("CreateBlobUsingBinder")]
public static void Run(
[QueueTrigger("myqueue-items-source-4")] string myQueueItem,
IBinder binder,
ILogger log)
{
log.LogInformation($"CreateBlobUsingBinder function processed: {myQueueItem}");
using (var writer = binder.Bind<TextWriter>(new BlobAttribute(
$"samples-output/{myQueueItem}", FileAccess.Write)))
{
writer.Write("Hello World!");
};
}
}
```


[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Extensions.Storage/Blobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob) input or output binding, and [TextWriter](/en-us/dotnet/api/system.io.textwriter) is a supported output binding type.

### Multiple attributes example

The preceding example gets the app setting for the function app's main Storage account connection string (which is `AzureWebJobsStorage`

). You can specify a custom app setting to use for the Storage account by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`

. Use a `Binder`

parameter, not `IBinder`

. For example:

```
public static class IBinderExampleMultipleAttributes
{
[FunctionName("CreateBlobInDifferentStorageAccount")]
public async static Task RunAsync(
[QueueTrigger("myqueue-items-source-binder2")] string myQueueItem,
Binder binder,
ILogger log)
{
log.LogInformation($"CreateBlobInDifferentStorageAccount function processed: {myQueueItem}");
var attributes = new Attribute[]
{
new BlobAttribute($"samples-output/{myQueueItem}", FileAccess.Write),
new StorageAccountAttribute("MyStorageAccount")
};
using (var writer = await binder.BindAsync<TextWriter>(attributes))
{
await writer.WriteAsync("Hello World!!");
}
}
}
```


## Triggers and bindings

This table shows the bindings that are supported in the major versions of the Azure Functions runtime:

| Type | 4.x1 |
1.x2 |
Trigger | Input | Output |
|---|---|---|---|---|---|
|

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)[Azure Data Explorer](functions-bindings-azure-data-explorer)[Azure SQL](functions-bindings-azure-sql)[Dapr](functions-bindings-dapr)4[Event Grid](functions-bindings-event-grid)[Event Hubs](functions-bindings-event-hubs)[HTTP and webhooks](functions-bindings-http-webhook)[IoT Hub](functions-bindings-event-iot)[Kafka](functions-bindings-kafka)3[Mobile Apps](functions-bindings-mobile-apps)[Model Context Protocol](functions-bindings-mcp)[Notification Hubs](functions-bindings-notification-hubs)[Queue Storage](functions-bindings-storage-queue)[Redis](functions-bindings-cache)[RabbitMQ](functions-bindings-rabbitmq)3[SendGrid](functions-bindings-sendgrid)[Service Bus](functions-bindings-service-bus)[Azure SignalR Service](functions-bindings-signalr-service)[Table Storage](functions-bindings-storage-table)[Timer](functions-bindings-timer)[Twilio](functions-bindings-twilio)- Register all bindings except HTTP and timer. See
[Register Azure Functions binding extensions](functions-bindings-register). This step isn't required when using version 1.x of the Functions runtime. [Support ends for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1).[Migrate your apps to version 4.x](migrate-version-1-version-4)for full support.- Triggers aren't supported in the Consumption plan. This binding type requires
[runtime-driven triggers](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers). - This binding type is supported in Kubernetes, Azure IoT Edge, and other self-hosted modes only.
