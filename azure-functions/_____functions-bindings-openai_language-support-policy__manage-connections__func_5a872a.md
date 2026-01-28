---
merged_at: 2026-01-28T07:43:39.528704
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai -->

# Azure OpenAI extension for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI extension for Azure Functions implements a set of triggers and bindings that enable you to easily integrate features and behaviors of [Azure OpenAI in Foundry Models](/en-us/azure/ai-services/openai/overview) into your function code executions.

Azure Functions is an event-driven compute service that provides a set of [triggers and bindings](functions-triggers-bindings) to easily connect with other Azure services.

With the integration between Azure OpenAI and Functions, you can build functions that can:

| Action | Trigger/binding type |
|---|---|
| Use a standard text prompt for content completion |
|

[Azure OpenAI assistant trigger](functions-bindings-openai-assistant-trigger)[Azure OpenAI assistant create output binding](functions-bindings-openai-assistantcreate-output)[Azure OpenAI assistant post input binding](functions-bindings-openai-assistantpost-input)[Azure OpenAI assistant query input binding](functions-bindings-openai-assistantquery-input)[Azure OpenAI embeddings input binding](functions-bindings-openai-embeddings-input)[Azure OpenAI embeddings store output binding](functions-bindings-openai-embeddingsstore-output)[Azure OpenAI semantic search input binding](functions-bindings-openai-semanticsearch-input)## Install extension

The extension NuGet package you install depends on the C# mode [in-process](functions-dotnet-class-library) or [isolated worker process](dotnet-isolated-process-guide) you're using in your function app:

Add the Azure OpenAI extension to your project by installing the [Microsoft.Azure.Functions.Worker.Extensions.OpenAI](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI) NuGet package, which you can do using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.OpenAI --prerelease
```


When using a vector database for storing content, you should also install at least one of these NuGet packages:

- Azure AI Search:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.AzureAISearch](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.AzureAISearch) - Azure Cosmos DB for MongoDB vCore:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBSearch](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBSearch) - Azure Cosmos DB for NoSQL:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBSearch](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBNoSQLSearch) - Azure Data Explorer:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.Kusto](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.Kusto)

## Install bundle

To be able to use this preview binding extension in your app, you must reference a preview extension bundle that includes it.

Add or replace the following code in your `host.json`

file, which specifically targets the latest [preview version of the 4.x bundle](https://github.com/Azure/azure-functions-extension-bundles/releases?q=preview+NOT+experimental&expanded=true):

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.0.0, 5.0.0)"
}
}
```


Select the previous link to verify that the latest preview bundle version does contain the preview extension.

## Connecting to OpenAI

To use the Azure OpenAI binding extension, you need to specify a connection to OpenAI. This connection is defined using application settings, and the `AIConnectionName`

property of the trigger or binding. You can also use environment variables to define key-based connections.

We recommend that you use managed identity-based connections and the `AIConnectionName`

property.

The OpenAI bindings have an `AIConnectionName`

property that you can use to specify the `<ConnectionNamePrefix>`

for this group of app settings that define the connection to Azure OpenAI:

| Setting name | Description |
|---|---|
`<CONNECTION_NAME_PREFIX>__endpoint` |
Sets the URI endpoint of the Azure OpenAI in Foundry Models. This setting is always required. |
`<CONNECTION_NAME_PREFIX>__clientId` |
Sets the specific user-assigned identity to use when obtaining an access token. Requires that `<CONNECTION_NAME_PREFIX>__credential` is set to `managedidentity` . The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a Resource ID and a client ID. If not specified, the system-assigned identity is used. This property is used differently in
`credential` shouldn't be set. |
`<CONNECTION_NAME_PREFIX>__credential` |
Defines how an access token is obtained for the connection. Use `managedidentity` for managed identity authentication. This value is only valid when a managed identity is available in the hosting environment. |
`<CONNECTION_NAME_PREFIX>__managedIdentityResourceId` |
When `credential` is set to `managedidentity` , this property can be set to specify the resource Identifier to be used when obtaining a token. The property accepts a resource identifier corresponding to the resource ID of the user-defined managed identity. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used. This property is used differently in
`credential` shouldn't be set. |
`<CONNECTION_NAME_PREFIX>__key` |
Sets the shared secret key required to access the endpoint of Azure OpenAI using key-based authentication. As a security best practice, you should always use Microsoft Entra ID with managed identities for authentication. |

Consider these managed identity connection settings when then `AIConnectionName`

property is set to `myAzureOpenAI`

:

`myAzureOpenAI__endpoint=https://contoso.openai.azure.com/`

`myAzureOpenAI__credential=managedidentity`

`myAzureOpenAI__clientId=aaaaaaaa-bbbb-cccc-1111-222222222222`


At runtime, these settings are collectively interpreted by the host as a single `myAzureOpenAI`

setting like this:

```
"myAzureOpenAI":
{
"endpoint": "https://contoso.openai.azure.com/",
"credential": "managedidentity",
"clientId": "aaaaaaaa-bbbb-cccc-1111-222222222222"
}
```


When using managed identities, make sure to add your identity to the [Cognitive Services OpenAI User](../role-based-access-control/built-in-roles/ai-machine-learning#cognitive-services-openai-user) role.

When running locally, you must add these settings to the *local.settings.json* project file. For more information, see [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

For more information, see [Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/language-support-policy -->

# Azure Functions language stack support policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the support policy for the language stacks supported by Azure Functions. Guidance is language-specific. Make sure to choose your preferred development language at the [top of the article](#top).

## Retirement process

The Functions runtime includes the Functions host and programming language-specific workers. To maintain full-support coverage when running your functions in Azure, Functions support aligns with end-of-life support for a given language. To help you keep your apps up-to-date and supported, Functions implements a phased reduction in support as language stack versions reach their end-of-life dates. Support ends on the earlier of: the community end-of-support date for the language or the end-of-support date for the underlying base operating system. Retirement dates are published at general availability (GA) to allow time for upgrade planning and testing.

**Notification phase**:The Functions team sends you notification emails about upcoming language version retirements that affect your function apps. When you receive this notification, you should prepare to upgrade these apps to use to a supported version.

**Retirement phase**:After the language end-of-life date, function apps that use retired language versions can still be created and deployed, and they continue to run on the platform. However, these apps aren't eligible for new features, security patches, and performance optimizations until after you upgrade them to a supported language version. Further, if required, in certain cases we will limit the number of instances allocated to these apps including limit scaling to 1 instance.

Important

If you're running function apps using an unsupported runtime or language version, you might encounter issues and performance implications and are required to upgrade before receiving support for your function app. As such, you're highly encouraged to upgrade the language version of such an app to a supported version. TO learn how, see

[Update language stack versions in Azure Functions](update-language-versions).

## Retirement policy exceptions

Any Functions-supported exceptions to language-specific retirement policies are documented here:

There are currently no exceptions to the general retirement policy.


## Language support-related resources

Use these resources to better understand and plan for language support-related changes in your function apps.

| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[.NET support policy page](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)**Configuring language versions**[Isolated worker model](dotnet-isolated-process-guide#supported-versions)[In-process model](functions-dotnet-class-library#supported-versions)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Node.js release page on GitHub](https://github.com/nodejs/Release#release-schedule)**Configuring language versions**[Setting the Node version](functions-reference-node#setting-the-node-version)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Node.js release page on GitHub](https://github.com/nodejs/Release#release-schedule)**Configuring language versions**[Setting the Node version](functions-reference-node#setting-the-node-version)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Java support on Azure and Azure Stack](/en-us/azure/developer/java/fundamentals/java-support-on-azure)**Configuring language versions**[Update the stack configuration](update-language-versions#update-the-stack-configuration)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[PowerShell Support Lifecycle](/en-us/powershell/scripting/powershell-support-lifecycle#powershell-end-of-support-dates)**Configuring language versions**[Changing the PowerShell version](functions-reference-python#supported-python-versions)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Python developer's guide](https://devguide.python.org/#status-of-python-branches)**Configuring language versions**[Changing Python version](set-runtime-version?tabs=azure-portal&pivots=platform-linux#manual-version-updates-on-linux)## Frequently asked questions

This section provides you with answers to questions that are frequently asked about language support policies.

### Which versions of my preferred language does Functions currently support?

For the up-to-date list of supported language stack versions, see [Supported languages in Azure Functions](supported-languages#languages-by-runtime-version).

### How long will Functions continue to support my language version?

Support ends on the earlier of: the community end-of-support date for the language or the end-of-support date for the underlying base operating system. Retirement dates are published at general availability (GA) to allow time for upgrade planning and testing. For the expected end-of-life dates of currently supported versions, see [Supported languages in Azure Functions](supported-languages#languages-by-runtime-version).

### What happens when my runtime version reaches the end of support?

After a previously supported Functions runtime version reaches its end-of-support, Microsoft no longer provides bug fixes, security updates, or patches. Apps using retired versions may also face performance degradation. You must upgrade to a supported version to maintain security and stability.

### Can I continue to use an unsupported language stack or runtime version?

You can continue to use previously supported language stacks and Functions runtime versions beyond the end-of-support date. However, you must take into account that unsupported runtime versions don't receive updates, security patches, or official support from Microsoft. Your apps might also face performance degradation when using retired runtime versions.

### How do I upgrade my function app to a newer supported language stack or runtime version?

To make sure that your app is compatible with both the latest supported Functions runtime version and the latest version of your language stack, see [Update language stack versions in Azure Functions](update-language-versions)

### How do I check which language stack and runtime version is being used by my function app?

Azure provides these methods to check the current runtime version used by your function app:

The language stack used by your function app is determined based on the value of the `FUNCTIONS_WORKER_RUNTIME`

application setting. For more information, see [Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

## Related articles

To learn more about how to upgrade your function app's language version, see these articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/manage-connections -->

# Manage connections in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Functions in a function app share resources. Among those shared resources are connections: HTTP connections, database connections, and connections to services such as Azure Storage. When many functions are running concurrently in a Consumption plan, it's possible to run out of available connections. This article explains how to code your functions to avoid using more connections than they need.

Note

Connection limits described in this article apply only when running in a [Consumption plan](consumption-plan). However, the techniques described here may be beneficial when running on any plan.

## Connection limit

The number of available connections in a Consumption plan is limited partly because a function app in this plan runs in a [sandbox environment](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox). One of the restrictions that the sandbox imposes on your code is a limit on the number of outbound connections, which is currently 600 active (1,200 total) connections per instance. When you reach this limit, the functions runtime writes the following message to the logs: `Host thresholds exceeded: Connections`

. For more information, see the [Functions service limits](functions-scale#service-limits).

This limit is per instance. When the [scale controller adds function app instances](event-driven-scaling) to handle more requests, each instance has an independent connection limit. That means there's no global connection limit, and you can have much more than 600 active connections across all active instances.

When troubleshooting, make sure that you have enabled Application Insights for your function app. Application Insights lets you view metrics for your function apps like executions. For more information, see [View telemetry in Application Insights](analyze-telemetry-data#view-telemetry-in-application-insights).

## Static clients

To avoid holding more connections than necessary, reuse client instances rather than creating new ones with each function invocation. We recommend reusing client connections for any language that you might write your function in. For example, .NET clients like the [HttpClient](/en-us/dotnet/api/system.net.http.httpclient?view=netcore-3.1&preserve-view=true), [DocumentClient](/en-us/dotnet/api/microsoft.azure.documents.client.documentclient), and Azure Storage clients can manage connections if you use a single, static client.

Here are some guidelines to follow when you're using a service-specific client in an Azure Functions application:

*Do not*create a new client with every function invocation.*Do*create a single, static client that every function invocation can use.*Consider*creating a single, static client in a shared helper class if different functions use the same service.

## Client code examples

This section demonstrates best practices for creating and using clients from your function code.

### HTTP requests

Here's an example of C# function code that creates a static [HttpClient](/en-us/dotnet/api/system.net.http.httpclient?view=netcore-3.1&preserve-view=true) instance:

```
// Create a single, static HttpClient
private static HttpClient httpClient = new HttpClient();
public static async Task Run(string input)
{
var response = await httpClient.GetAsync("https://example.com");
// Rest of function
}
```


A common question about [HttpClient](/en-us/dotnet/api/system.net.http.httpclient?view=netcore-3.1&preserve-view=true) in .NET is "Should I dispose of my client?" In general, you dispose of objects that implement `IDisposable`

when you're done using them. But you don't dispose of a static client because you aren't done using it when the function ends. You want the static client to live for the duration of your application.

### Azure Cosmos DB clients

[CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) connects to an Azure Cosmos DB instance. The Azure Cosmos DB documentation recommends that you [use a singleton Azure Cosmos DB client for the lifetime of your application](/en-us/azure/cosmos-db/performance-tips-dotnet-sdk-v3-sql#sdk-usage). The following example shows one pattern for doing that in a function:

```
#r "Microsoft.Azure.Cosmos"
using Microsoft.Azure.Cosmos;
private static Lazy<CosmosClient> lazyClient = new Lazy<CosmosClient>(InitializeCosmosClient);
private static CosmosClient cosmosClient => lazyClient.Value;
private static CosmosClient InitializeCosmosClient()
{
// Perform any initialization here
var uri = "https://youraccount.documents.azure.com:443";
var authKey = "authKey";
return new CosmosClient(uri, authKey);
}
public static async Task Run(string input)
{
Container container = cosmosClient.GetContainer("database", "collection");
MyItem item = new MyItem{ id = "myId", partitionKey = "myPartitionKey", data = "example" };
await container.UpsertItemAsync(document);
// Rest of function
}
```


Also, create a file named "function.proj" for your trigger and add the below content :

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.Azure.Cosmos" Version="3.23.0" />
</ItemGroup>
</Project>
```


## SqlClient connections

Your function code can use the .NET Framework Data Provider for SQL Server ([SqlClient](/en-us/dotnet/api/system.data.sqlclient)) to make connections to a SQL relational database. This is also the underlying provider for data frameworks that rely on ADO.NET, such as [Entity Framework](/en-us/ef/ef6/). Unlike [HttpClient](/en-us/dotnet/api/system.net.http.httpclient) and [DocumentClient](/en-us/dotnet/api/microsoft.azure.documents.client.documentclient) connections, ADO.NET implements connection pooling by default. But because you can still run out of connections, you should optimize connections to the database. For more information, see [SQL Server Connection Pooling (ADO.NET)](/en-us/dotnet/framework/data/adonet/sql-server-connection-pooling).

Tip

Some data frameworks, such as Entity Framework, typically get connection strings from the **ConnectionStrings** section of a configuration file. In this case, you must explicitly add SQL database connection strings to the **Connection strings** collection of your function app settings and in the [local.settings.json file](functions-develop-local#local-settings-file) in your local project. If you're creating an instance of [SqlConnection](/en-us/dotnet/api/system.data.sqlclient.sqlconnection) in your function code, you should store the connection string value in **Application settings** with your other connections.

## Next steps

For more information about why we recommend static clients, see [Improper instantiation antipattern](/en-us/azure/architecture/antipatterns/improper-instantiation/).

For more Azure Functions performance tips, see [Optimize the performance and reliability of Azure Functions](functions-best-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-overview -->

# What is Azure Functions?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions is a serverless solution that allows you to build robust apps while using less code, and with less infrastructure and lower costs. Instead of worrying about deploying and maintaining servers, you can use the cloud infrastructure to provide all the up-to-date resources needed to keep your applications running.

You focus on the code that matters most to you, in the most productive language for you, and Azure Functions handles the rest. For a list of supported languages, see [Supported languages in Azure Functions](supported-languages).

## Scenarios

Functions provides a comprehensive set of event-driven [triggers and bindings](functions-triggers-bindings) that connect your functions to other services without having to write extra code.

The following list includes common integrated scenarios that use Functions.

| If you want to... | then... |
|---|---|
|

[Process data in real time](functions-scenarios#real-time-stream-and-event-processing)[Run AI inference](functions-scenarios#machine-learning-and-ai)[Run scheduled task](functions-scenarios#run-scheduled-tasks)[Build a scalable web API](functions-scenarios#build-a-scalable-web-api)[Build a serverless workflow](functions-scenarios#build-a-serverless-workflow)[Respond to database changes](functions-scenarios#respond-to-database-changes)[Create reliable message systems](functions-scenarios#create-reliable-message-systems)These scenarios allow you to build event-driven systems using modern architectural patterns. For more information, see [Azure Functions scenarios](functions-scenarios).

## Development lifecycle

With Functions, you write your function code in your preferred language using your favorite development tools, and then deploy your code to the Azure cloud. Functions provides native support for developing in [C#, Java, JavaScript, PowerShell, or Python](supported-languages), plus the ability to use [custom handlers](functions-custom-handlers) for other languages, such as Rust and Go.

Functions integrates directly with Visual Studio, Visual Studio Code, Maven, and other popular development tools to enable seamless debugging and [deployments](functions-deployment-technologies).

Functions also integrates with Azure Monitor and Azure Application Insights to provide comprehensive monitoring and analysis of your [functions in the cloud](functions-monitoring).

## Hosting options

Functions provides various [hosting options](functions-scale) for your business needs and application workload. [Event-driven scaling hosting options](event-driven-scaling) range from fully serverless, where you only pay for execution time (Consumption plan), to always-warm instances kept ready for the fastest response times (Premium plan).

When you have excess App Service hosting resources, you can host your functions in an existing App Service plan. This kind of Dedicated hosting plan is also a good choice when you need predictable scaling behaviors and costs from your functions.

If you want complete control over your runtime environment and dependencies, you can even deploy your functions in containers that you can fully customize. Your custom containers can be hosted by Functions, deployed as part of a microservices architecture in Azure Container Apps, or even self-hosted in Kubernetes.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-get-started -->

# Getting started with Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Functions](functions-overview) allows you to implement your system's logic as event-driven, readily available blocks of code. These code blocks are called "functions". This article is to help you find your way to the most helpful Azure Functions content as quickly as possible. For more general information about Azure Functions, see the [Introduction to Azure Functions](functions-overview).

Make sure to choose your preferred development language at the top of the article.

## Create your first function

Complete one of our quickstart articles to create and deploy your first functions in less than five minutes.

You can create your first function by using one of the following tools:

Besides the natively supported programming languages, you can use [custom handlers](functions-custom-handlers) to create functions in any language that supports HTTP primitives. The article [Create a Go or Rust function in Azure using Visual Studio Code](create-first-function-vs-code-other) shows you how to use custom handlers to write your function code in either Rust or Go.

## Review end-to-end samples

These sites let you browse existing functions reference projects and samples in your desired language:

## Scenarios

While Functions provides compute resources to run your code in any Azure-based topology, here are some scenario ideas to help you get started:

[Process file uploads](functions-scenarios#process-file-uploads)[Real-time stream and event processing](functions-scenarios#real-time-stream-and-event-processing)[Machine learning and AI](functions-scenarios#machine-learning-and-ai)[Run scheduled tasks](functions-scenarios#run-scheduled-tasks)[Build a scalable web API](functions-scenarios#build-a-scalable-web-api)[Build a serverless workflow](functions-scenarios#build-a-serverless-workflow)[Respond to database changes](functions-scenarios#respond-to-database-changes)[Create reliable message systems](functions-scenarios#create-reliable-message-systems)

## Explore an interactive tutorial

Complete one of the following interactive training modules to learn more about Functions:

[Choose the best Azure serverless technology for your business scenario](/en-us/training/modules/serverless-fundamentals/)[Well-Architected Framework - Performance efficiency](/en-us/training/modules/azure-well-architected-performance-efficiency/)[Execute an Azure Function with triggers](/en-us/training/modules/execute-azure-function-with-triggers/)

To learn even more, see the [full listing of interactive tutorials](/en-us/training/browse/?expanded=azure&products=azure-functions).

## Related content

Learn more about developing functions by reviewing one of these C# reference articles:

Learn more about developing functions by reviewing the [Java language reference](functions-reference-java) article.

Learn more about developing functions by reviewing the [Node.js language reference](functions-reference-node) article.

Learn more about developing functions by reviewing the [PowerShell language reference](functions-reference-powershell) article.

Learn more about developing functions by reviewing the [Python language reference](functions-reference-python) article.

Learn more about developing functions using Rust, Go, and other languages by reviewing the [custom handlers](functions-custom-handlers) documentation.

You might also be interested in these articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-nat-gateway -->

# Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Virtual network address translation (NAT) simplifies outbound-only internet connectivity for virtual networks. When configured on a subnet, all outbound connectivity uses your specified static public IP addresses. An NAT can be useful for apps that need to consume a third-party service that uses an allowlist of IP address as a security measure. To learn more, see [What is Azure NAT Gateway?](../virtual-network/nat-gateway/nat-overview).

This tutorial shows you how to use NAT gateways to route outbound traffic from an HTTP triggered function. This function lets you check its own outbound IP address. During this tutorial, you'll:

- Create a virtual network
- Create a Premium plan function app
- Create a public IP address
- Create a NAT gateway
- Configure function app to route outbound traffic through the NAT gateway

Note

You can't use a NAT gateway to route outbound traffic to an Azure Storage account in the same region as your function app. Services deployed in the same region your storage account use private Azure IP addresses for communication. For more information, see [NAT Gateway frequenty asked questions](/en-us/azure/nat-gateway/faq#can-i-use-nat-gateway-to-connect-to-a-storage-account-public-endpoint-in-the-same-region).

## Topology

The following diagram shows the architecture of the solution that you create:

Functions running in the Premium plan have the same hosting capabilities as web apps in Azure App Service, which includes the VNet Integration feature. To learn more about VNet Integration, including troubleshooting and advanced configuration, see [Integrate your app with an Azure virtual network](../app-service/overview-vnet-integration).

## Prerequisites

For this tutorial, it's important that you understand IP addressing and subnetting. You can start with [this article that covers the basics of addressing and subnetting](https://support.microsoft.com/help/164015/understanding-tcp-ip-addressing-and-subnetting-basics). Many more articles and videos are available online.

If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

If you've already completed the [integrate Functions with an Azure virtual network](functions-create-vnet) tutorial, you can skip to [Create an HTTP trigger function](#create-function).

## Create a virtual network

From the Azure portal menu, select

**Create a resource**. From the Azure Marketplace, select**Networking**>**Virtual network**.In

**Create virtual network**, enter or select the settings specified as shown in the following table:Setting Value Subscription Select your subscription. Resource group Select **Create new**, enter*myResourceGroup*, then select**OK**.Name Enter *myResourceGroup-vnet*.Location Select **East US**.Select

**Next: IP Addresses**, and for**IPv4 address space**, enter*10.10.0.0/16*.Select

**Add subnet**, then enter*Tutorial-Net*for**Subnet name**and*10.10.1.0/24*for**Subnet address range**.Select

**Add**, then select**Review + create**. Leave the rest as default and select**Create**.In

**Create virtual network**, select**Create**.

Next, you create a function app in the [Premium plan](functions-premium-plan). This plan provides serverless scale while supporting virtual network integration.

## Create a function app in a Premium plan

This tutorial shows you how to create your function app in a [Premium plan](functions-premium-plan). The same functionality is also available when you host your app in a [Flex Consumption plan](flex-consumption-plan) or in a [Dedicated (App Service) plan](dedicated-plan).

Note

For the best experience in this tutorial, choose .NET for runtime stack and choose Windows for operating system. Also, create your function app in the same region as your virtual network.

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Compute**>**Function App**.Under

**Select a hosting option**, select**Functions Premium**>**Select**to create your app in a[Premium plan](functions-premium-plan). In this[serverless](https://azure.microsoft.com/overview/serverless-computing/)hosting option, you pay only for the time your functions run. To learn more about different hosting plans, see[Overview of plans](functions-scale#overview-of-plans).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which to create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

. To guarantee a unique app name, you can optionally enable**Secure unique default hostname**, which is currently in preview.**Do you want to deploy code or container image?**Code Option to publish code files or a Docker container. **Operating system**Preferred OS Choose either Linux or Windows. **Runtime stack**Preferred language Choose a runtime that supports your favorite function programming language. **Version**Supported language version Choose a supported version of your function programming language. **Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services your functions access.Under

**Environment details**for either**Windows Plan**or**Linux Plan**, select**Create new**,**Name**your App Service plan, and select a**Pricing plan**. The default pricing plan is**EP1**, where EP stands for*elastic premium*. To learn more, see the[list of Premium SKUs](functions-premium-plan#available-instance-skus). When running JavaScript functions on a Premium plan, you should choose an instance that has fewer vCPUs. For more information, see[Choose single-core Premium plans](functions-reference-node#considerations-for-javascript-functions).Unless you want to enable

, keep the default value of**Zone Redundancy****Disabled**.Select

**Next: Storage**. On the**Storage**page, create the default host[storage account](../storage/common/storage-account-create)required by your function app. Storage account names must be between 3 and 24 characters in length and only can contain numbers and lowercase letters. You can also use an existing account, which must meet the[storage account requirements](storage-considerations#storage-account-requirements).Unless you're enabling virtual network integration, select

**Next: Monitoring**to skip the**Networking**tab. On the**Monitoring**page, enter the following settings:Setting Suggested value Description Enable Application Insights Yes Enables built-in Application Insight integration for monitoring your functions code. [Application Insights](functions-monitoring)Default Creates an Application Insights resource of the same *App name*in the nearest supported region. By expanding this setting, you can change the**New resource name**or choose a different**Location**in an[Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/)to store your data.Select

**Review + create**to accept the defaults for the remaining pages and review the app configuration selections.On the

**Review + create**page, review your settings, and then select**Create**to provision and deploy the function app.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

## Connect your function app to the virtual network

You can now connect your function app to the virtual network.

In your function app, select

**Networking**in the left menu, then under**VNet Integration**, select**Click here to configure**.On the

**VNET Integration**page, select**Add VNet**.In

**Network Feature Status**, use the settings in the table below the image:Setting Suggested value Description **Virtual Network**MyResourceGroup-vnet This virtual network is the one you created earlier. **Subnet**Create New Subnet Create a subnet in the virtual network for your function app to use. VNet Integration must be configured to use an empty subnet. **Subnet name**Function-Net Name of the new subnet. **Virtual network address block**10.10.0.0/16 You should only have one address block defined. **Subnet Address Block**10.10.2.0/24 The subnet size restricts the total number of instances that your Premium plan function app can scale out to. This example uses a `/24`

subnet with 254 available host addresses. This subnet is over-provisioned, but easy to calculate.Select

**OK**to add the subnet. Close the**VNet Integration**and**Network Feature Status**pages to return to your function app page.

The function app can now access the virtual network. When connectivity is enabled, the [ vnetrouteallenabled](functions-app-settings#vnetrouteallenabled) site setting is set to

`1`

. You must have either this site setting or the legacy [application setting set to](functions-app-settings#website_vnet_route_all)

`WEBSITE_VNET_ROUTE_ALL`

`1`

.Next, you'll add an HTTP-triggered function to the function app.

## Create an HTTP trigger function

From the left menu of the

**Functions**window, select**Functions**, then select**Add**from the top menu.From the

**New Function**window, select**Http trigger**and accept the default name for**New Function**, or enter a new name.In

**Code + Test**, replace the template-generated C# script (.csx) code with the following code:`#r "Newtonsoft.Json" using System.Net; using Microsoft.AspNetCore.Mvc; using Microsoft.Extensions.Primitives; using Newtonsoft.Json; public static async Task<IActionResult> Run(HttpRequest req, ILogger log) { log.LogInformation("C# HTTP trigger function processed a request."); var client = new HttpClient(); var response = await client.GetAsync(@"https://ifconfig.me"); var responseMessage = await response.Content.ReadAsStringAsync(); return new OkObjectResult(responseMessage); }`

This code calls an external website that returns the IP address of the caller, which in this case is this function. This method lets you easily determine the outbound IP address being used by your function app.


Now you're ready to run the function and check the current outbound IPs.

## Verify current outbound IPs

Now, you can run the function. But first, check in the portal and see what outbound IPs are being use by the function app.

In your function app, select

**Properties**and review the**Outbound IP Addresses**field.Now, return to your HTTP trigger function, select

**Code + Test**and then**Test/Run**.Select

**Run**to execute the function, then switch to the**Output**and verify that IP address in the HTTP response body is one of the values from the outbound IP addresses you viewed earlier.

Now, you can create a public IP and use a NAT gateway to modify this outbound IP address.

## Create public IP

From your resource group, select

**Add**, search the Azure Marketplace for**Public IP address**, and select**Create**. Use the settings in the table below the image:Setting Suggested value **IP Version**IPv4 **SKU**Standard **Tier**Regional **Name**Outbound-IP **Subscription**ensure your subscription is displayed **Resource group**myResourceGroup (or name you assigned to your resource group) **Location**East US (or location you assigned to your other resources) **Availability Zone**No Zone Select

**Create**to submit the deployment.Once the deployment completes, navigate to your newly created Public IP Address resource and view the IP Address in the

**Overview**.

## Create NAT gateway

Now, let's create the NAT gateway. When you start with the [previous virtual networking tutorial](functions-create-vnet), `Function-Net`

was the suggested subnet name and `MyResourceGroup-vnet`

was the suggested virtual network name in that tutorial.

From your resource group, select

**Add**, search the Azure Marketplace for**NAT gateway**, and select**Create**. Use the settings in the table below the image to populate the**Basics**tab:Setting Suggested value **Subscription**Your subscription **Resource group**myResourceGroup (or name you assigned to your resource group) **NAT gateway name**myNatGateway **Region**East US (or location you assigned to your other resources) **Availability Zone**None Select

**Next: Outbound IP**. In the**Public IP addresses**field, select the previously created public IP address. Leave**Public IP Prefixes**unselected.Select

**Next: Subnet**. Select the*myResourceGroup-vnet*resource in the**Virtual network**field and*Function-Net*subnet.Select

**Review + Create**then**Create**to submit the deployment.

Once the deployment completes, the NAT gateway is ready to route traffic from your function app subnet to the Internet.

## Verify new outbound IPs

Repeat [the steps earlier](#verify-current-outbound-ips) to run the function again. You should now see the outbound IP address that you configured in the NAT shown in the function output.

## Clean up resources

You created resources to complete this tutorial. You'll be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). To avoid incurring extra costs, delete the resources when you know longer need them.

In the Azure portal, go to the

**Resource group**page.To get to that page from the function app page, select the

**Overview**tab, and then select the link under**Resource group**.To get to that page from the dashboard, select

**Resource groups**, and then select the resource group that you used for this article.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**and follow the instructions.Deletion might take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-github-actions -->

# Continuous delivery by using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use a [GitHub Actions workflow](https://docs.github.com/actions/learn-github-actions/introduction-to-github-actions#the-components-of-github-actions) to define a workflow to automatically build and deploy code to your function app in Azure Functions.

A YAML file (.yml) that defines the workflow configuration is maintained in the `/.github/workflows/`

path in your repository. This definition contains the actions and parameters that make up the workflow, which is specific to the development language of your functions. A GitHub Actions workflow for Functions performs the following tasks, regardless of language:

- Set up the environment.
- Build the code project.
- Deploy the package to a function app in Azure.

The Azure Functions action handles the deployment to an existing function app in Azure.

You can create a workflow configuration file for your deployment manually. You can also generate the file from a set of language-specific templates in one of these ways:

- In the Azure portal
- Using the Azure CLI
- From your GitHub repository

If you don't want to create your YAML file by hand, select a different method at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).A GitHub account. If you don't have one, sign up for

[free](https://github.com/join).A working function app hosted on Azure with source code in a GitHub repository.


[Azure CLI](/en-us/cli/azure/install-azure-cli), when developing locally. You can also use the Azure CLI in Azure Cloud Shell.

## Generate deployment credentials

Since GitHub Actions uses your publish profile to access your function app during deployment, you first need to get your publish profile and store it securely as a [GitHub secret](https://docs.github.com/en/actions/reference/encrypted-secrets).

Important

The publish profile is a valuable credential that allows access to Azure resources. Make sure you always transport and store it securely. In GitHub, the publish profile must only be stored in GitHub secrets.

### Download your publish profile

To download the publishing profile of your function app:

In the

[Azure portal](https://portal.azure.com), locate the page for your function app, expand**Settings**>**Configuration**in the left column.In the

**Configuration**page, select the**General settings**tab and make sure that**SCM Basic Auth Publishing Credentials**is turned**On**. When this setting is**Off**, you can't use publish profiles, so select**On**and then**Save**.Go back to the function app's

**Overview**page, and then select**Get publish profile**.Save and copy the contents of the file.


### Add the GitHub secret

In

[GitHub](https://github.com/), go to your repository.Go to

**Settings**.Select

**Secrets and variables > Actions**.Select

**New repository secret**.Add a new secret with the name

`AZURE_FUNCTIONAPP_PUBLISH_PROFILE`

and the value set to the contents of the publishing profile file.Select

**Add secret**.

GitHub can now authenticate to your function app in Azure.

## Create the workflow from a template

The best way to manually create a workflow configuration is to start from the officially supported template.

Choose either

**Windows**or**Linux**to make sure that you get the template for the correct operating system.Copy the language-specific template from the Azure Functions actions repository using the following link:

Update the

`env.AZURE_FUNCTIONAPP_NAME`

parameter with the name of your function app resource in Azure. You may optionally need to update the parameter that sets the language version used by your app, such as`DOTNET_VERSION`

for C#.Add this new YAML file in the

`/.github/workflows/`

path in your repository.

## Create the workflow configuration in the portal

When you use the portal to enable GitHub Actions, Functions creates a workflow file based on your application stack and commits it to your GitHub repository in the correct directory.

The portal automatically gets your publish profile and adds it to the GitHub secrets for your repository.

### During function app create

You can get started quickly with GitHub Actions through the Deployment tab when you create a function in Azure portal. To add a GitHub Actions workflow when you create a new function app:

In the

[Azure portal](https://portal.azure.com), select**Deployment**in the**Create Function App**flow.Enable

**Continuous Deployment**if you want each code update to trigger a code push to Azure portal.Enter your GitHub organization, repository, and branch.

Complete configuring your function app. Your GitHub repository now includes a new workflow file in

`/.github/workflows/`

.

### For an existing function app

To add a GitHub Actions workflow to an existing function app:

Navigate to your function app in the

[Azure portal](https://portal.azure.com)and select**Deployment Center**.For

**Source**select**GitHub**. If you don't see the default message*Building with GitHub Actions*, select**Change provider**choose**GitHub Actions**and select**OK**.If you haven't already authorized GitHub access, select

**Authorize**. Provide your GitHub credentials and select**Sign in**. To authorize a different GitHub account, select**Change Account**and sign in with another account.Select your GitHub

**Organization**,**Repository**, and**Branch**. To deploy with GitHub Actions, you must have write access to this repository.In

**Authentication settings**, choose whether to have GitHub Actions authenticate with a**User-assigned identity**or using**Basic authentication**credentials. For basic authentication, the current credentials are used.Select

**Preview file**to see the workflow file that gets added to your GitHub repository in`github/workflows/`

.Select

**Save**to add the workflow file to your repository.

## Add workflow configuration to your repository

You can use the [ az functionapp deployment github-actions add](/en-us/cli/azure/functionapp/deployment/github-actions) command to generate a workflow configuration file from the correct template for your function app. The new YAML file is then stored in the correct location (

`/.github/workflows/`

) in the GitHub repository you provide, while the publish profile file for your app is added to GitHub secrets in the same repository.Run this

`az functionapp`

command, replacing the values`githubUser/githubRepo`

,`MyResourceGroup`

, and`MyFunctionapp`

:`az functionapp deployment github-actions add --repo "githubUser/githubRepo" -g MyResourceGroup -n MyFunctionapp --login-with-github`

This command uses an interactive method to retrieve a personal access token for your GitHub account.

In your terminal window, you should see something like the following message:

`Please navigate to https://github.com/login/device and enter the user code XXXX-XXXX to activate and retrieve your GitHub personal access token.`

Copy the unique

`XXXX-XXXX`

code, browse to[https://github.com/login/device](https://github.com/login/device), and enter the code you copied. After entering your code, you should see something like the following message:`Verified GitHub repo and branch Getting workflow template using runtime: java Filling workflow template with name: func-app-123, branch: main, version: 8, slot: production, build_path: . Adding publish profile to GitHub Fetching publish profile with secrets for the app 'func-app-123' Creating new workflow file: .github/workflows/master_func-app-123.yml`

Go to your GitHub repository and select

**Actions**. Verify that your workflow ran.

## Create the workflow configuration file

You can create the GitHub Actions workflow configuration file from the Azure Functions templates directly from your GitHub repository.

In

[GitHub](https://github.com/), go to your repository.Select

**Actions**and**New workflow**.Search for

*functions*.In the displayed functions app workflows authored by Microsoft Azure, find the one that matches your code language and select

**Configure**.In the newly created YAML file, update the

`env.AZURE_FUNCTIONAPP_NAME`

parameter with the name of your function app resource in Azure. You may optionally need to update the parameter that sets the language version used by your app, such as`DOTNET_VERSION`

for C#.Verify that the new workflow file is being saved in

`/.github/workflows/`

and select**Commit changes...**.

## Update a workflow configuration

If for some reason, you need to update or change an existing workflow configuration, just navigate to the `/.github/workflows/`

location in your repository, open the specific YAML file, make any needed changes, and then commit the updates to the repository.

## Example: workflow configuration file

The following template example uses version 1 of the `functions-action`

and a `publish profile`

for authentication. The template depends on your chosen language and the operating system on which your function app is deployed:

```
name: Deploy DotNet project to Azure Function App
on:
[push]
env:
AZURE_FUNCTIONAPP_NAME: 'your-app-name' # set this to your function app name on Azure
AZURE_FUNCTIONAPP_PACKAGE_PATH: '.' # set this to the path to your function app project, defaults to the repository root
DOTNET_VERSION: '6.0.x' # set this to the dotnet version to use (e.g. '2.1.x', '3.1.x', '5.0.x')
jobs:
build-and-deploy:
runs-on: windows-latest
environment: dev
steps:
- name: 'Checkout GitHub Action'
uses: actions/checkout@v3
- name: Setup DotNet ${{ env.DOTNET_VERSION }} Environment
uses: actions/setup-dotnet@v3
with:
dotnet-version: ${{ env.DOTNET_VERSION }}
- name: 'Resolve Project Dependencies Using Dotnet'
shell: pwsh
run: |
pushd './${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }}'
dotnet build --configuration Release --output ./output
popd
- name: 'Run Azure Functions Action'
uses: Azure/functions-action@v1
id: fa
with:
app-name: ${{ env.AZURE_FUNCTIONAPP_NAME }}
package: '${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }}/output'
publish-profile: ${{ secrets.AZURE_FUNCTIONAPP_PUBLISH_PROFILE }}
```


## Azure Functions action

The Azure Functions action (`Azure/functions-action`

) defines how your code is published to an existing function app in Azure, or to a specific slot in your app.

### Parameters

The following parameters are required for all function app plans:

| Parameter | Explanation |
|---|---|
app-name |
The name of your function app. |
package |
This is the location in your project to be published. By default, this value is set to `.` , which means all files and folders in the GitHub repository will be deployed. |

The following parameters are required for the Flex Consumption plan:

| Parameter | Explanation |
|---|---|
sku |
Set this to `flexconsumption` when authenticating with publish-profile. When using RBAC credentials or deploying to a non-Flex Consumption plan, the Action can resolve the value, so the parameter does not need to be included. |
remote-build |
Set this to `true` to enable a build action from Kudu when the package is deployed to a Flex Consumption app. Oryx build is always performed during a remote build in Flex Consumption; do not set scm-do-build-during-deployment or enable-oryx-build. By default, this parameter is set to `false` . |

The following parameters are specific to the Consumption, Elastic Premium, and App Service (Dedicated) plans:

| Parameter | Explanation |
|---|---|
scm-do-build-during-deployment |
(Optional) Allow the Kudu site (e.g. `https://<APP_NAME>.scm.azurewebsites.net/` ) to perform pre-deployment operations, such as
`false` . Set this to `true` when you do want to control deployment behaviors using Kudu instead of resolving dependencies in your GitHub workflow. For more information, see the
`SCM_DO_BUILD_DURING_DEPLOYMENT` |
enable-oryx-build |
(Optional) Allow Kudu site to resolve your project dependencies with Oryx. By default, this is set to `false` . If you want to use
scm-do-build-during-deployment and enable-oryx-build to `true` . |

Optional parameters for all function app plans:

| Parameter | Explanation |
|---|---|
slot-name |
This is the
publish-profile parameter contains the credentials for the slot instead of the production site. Currently not supported in Flex Consumption. |

**publish-profile****respect-pom-xml**`true`

and set `package`

to `.`

. By default, this parameter is set to `false`

, which means that the `package`

parameter must point to your app's artifact location, such as `./target/azure-functions/`

**respect-funcignore**`true`

when your repository has a .funcignore file and you want to use it exclude paths and files, such as text editor configurations, .vscode/, or a Python virtual environment (.venv/). The default setting is `false`

.### Considerations

Keep the following considerations in mind when using the Azure Functions action:

When using GitHub Actions, the way that your code is deployed depends on your hosting plan, as shown in this table:

Hosting plan Deployment method [Flex Consumption](flex-consumption-plan)[One deploy](functions-deployment-technologies#one-deploy)[Elastic Premium](functions-premium-plan)[Zip deploy](deployment-zip-push)to apps on the[Consumption](consumption-plan)[Dedicated (App Service)](dedicated-plan)[Zip deploy](deployment-zip-push)to apps on the[Consumption](consumption-plan)[Consumption](consumption-plan)Windows: [Zip deploy](deployment-zip-push)

Linux:[external package URL](functions-deployment-technologies#external-package-url)** The ability to run your apps on Linux in a Consumption plan is planned for retirement. For more information, see

[Azure Functions Consumption plan hosting](consumption-plan).The credentials required by GitHub to connection to Azure for deployment are stored as Secrets in your GitHub repository and accessed in the deployment as

`secrets.<SECRET_NAME>`

.The easiest way for GitHub Actions to authenticate with Azure Functions for deployment is by using a publish profile. You can also authenticate using a service principal. To learn more, see

[this GitHub Actions repository](https://github.com/Azure/functions-action).The actions for setting up the environment and running a build are generated from the templates, and are language specific.

The templates use

`env`

elements to define settings unique to your build and deployment.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-infrastructure-as-code -->

# Automate resource deployment for your function app in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use a Bicep file or an Azure Resource Manager (ARM) template to automate the process of deploying your function app. During the deployment, you can use existing Azure resources or create new ones.

You can obtain these benefits in your production apps by using deployment automation, both infrastructure-as-code (IaC) and continuous integration and deployment (CI/CD):

**Consistency**: Define your infrastructure in code to ensure consistent deployments across environments.**Version Control**: Track changes to your infrastructure and application configurations in source control, along with your project code.**Automation**: Automate deployment, which reduces manual errors and shortens release process.**Scalability**: Easily replicate infrastructure for multiple environments, such as development, testing, and production.**Disaster Recovery**: Quickly recreate infrastructure after failures or during migrations.

This article shows you how to automate the creation of Azure resources and deployment configurations for Azure Functions. To learn more about continuous deployment of your project code, see [Continuous deployment for Azure Functions](functions-continuous-deployment).

The template code to create the required Azure resources depends on the desired hosting options for your function app. This article supports the following hosting options:

| Hosting option | Deployment type | Sample templates |
|---|---|---|
|

[Bicep](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.web/function-app-flex-managed-identities/main.bicep)[ARM template](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.web/function-app-flex-managed-identities/azuredeploy.json)[Terraform](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC/terraformazurerm)[Premium plan](functions-premium-plan)[Bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-premium-plan/main.bicep)[ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-premium-plan/azuredeploy.json)[Dedicated plan](dedicated-plan)[Bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/main.bicep)[ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/azuredeploy.json)[Azure Container Apps](../container-apps/functions-overview)[Bicep](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/ACAKindfunctionapp)[Consumption plan](consumption-plan)[Bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/main.bicep)[ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/azuredeploy.json)Make sure to select your hosting plan at the top of the article.

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

When using this article, keep these considerations in mind:

There's no canonical way to structure an ARM template.

A Bicep deployment can be modularized into multiple Bicep files and

[Azure Verified Modules (AVMs)](https://azure.github.io/Azure-Verified-Modules/overview/introduction/).This article assumes that you have a basic understanding of

[creating Bicep files](../azure-resource-manager/bicep/file)or[authoring Azure Resource Manager templates](../azure-resource-manager/templates/syntax).

- Examples are shown as individual sections for specific resources. For a broad set of complete Bicep file and ARM template examples, see
[these function app deployment examples](/en-us/samples/browse/?expanded=azure&terms=%22azure%20functions%22&products=azure-resource-manager).

- Examples are shown as individual sections for specific resources. For Bicep,
[Azure Verified Modules (AVM)](https://azure.github.io/Azure-Verified-Modules/)are shown, when available. For a broad set of complete Bicep file and ARM template examples, see[these Flex Consumption app deployment examples](/en-us/samples/browse/?expanded=azure&terms=%22azure%20functions%20flex%22&products=azure-resource-manager).

- Examples are shown as individual sections for specific resources.

## Required resources

You must create or configure these resources for an Azure Functions-hosted deployment:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)*[hosting plan](#create-the-hosting-plan)[Microsoft.Web/serverfarms](/en-us/azure/templates/microsoft.web/serverfarms)[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)You must create or configure these resources for an Azure Functions-hosted deployment:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)*[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)An Azure Container Apps-hosted deployment typically consists of these resources:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)*[managed environment](../container-apps/functions-overview#)[Microsoft.App/managedEnvironments](/en-us/azure/templates/microsoft.app/managedenvironments)[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)An Azure Arc-hosted deployment typically consists of these resources:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)1[App Service Kubernetes environment](../app-service/overview-arc-integration#app-service-kubernetes-environment)[Microsoft.ExtendedLocation/customLocations](/en-us/azure/templates/microsoft.extendedlocation/customlocations)[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)*If you don't already have a Log Analytics Workspace that can be used by your Application Insights instance, you also need to create this resource.

When you deploy multiple resources in a single Bicep file or ARM template, the order in which resources are created is important. This requirement is a result of dependencies between resources. For such dependencies, make sure to use the `dependsOn`

element to define the dependency in the dependent resource. For more information, see either [Define the order for deploying resources in ARM templates](../azure-resource-manager/templates/resource-dependency) or [Resource dependencies in Bicep](../azure-resource-manager/bicep/resource-dependencies).

## Prerequisites

- The examples are designed to execute in the context of an existing resource group.
- Both Application Insights and storage logs require you to have an existing
[Azure Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-overview). Workspaces can be shared between services, and as a rule of thumb you should create a workspace in each geographic region to improve performance. For an example of how to create a Log Analytics workspace, see[Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace?tabs=azure-resource-manager#create-a-workspace). You can find the fully qualified workspace resource ID in a workspace page in the[Azure portal](https://portal.azure.com)under**Settings**>**Properties**>**Resource ID**.

- This article assumes that you have already created a
[managed environment](../container-apps/environment)in Azure Container Apps. You need both the name and the ID of the managed environment to create a function app hosted on Container Apps.

- This article assumes that you have already created an
[App Service-enabled custom location](../app-service/overview-arc-integration)on an[Azure Arc-enabled Kubernetes cluster](/en-us/azure/azure-arc/kubernetes/overview). You need both the custom location ID and the Kubernetes environment ID to create a function app hosted in an Azure Arc custom location.

## Create storage account

All function apps require an Azure storage account. You need a general purpose account that supports blobs, tables, queues, and files. For more information, see [Azure Functions storage account requirements](storage-considerations#storage-account-requirements).

Important

The storage account is used to store important app data, sometimes including the application code itself. You should limit access from other apps and users to the storage account.

This example section creates a Standard general purpose v2 storage account:

```
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-05-01' = {
name: storageAccountName
location: location
kind: 'StorageV2'
sku: {
name: 'Standard_LRS'
}
properties: {
supportsHttpsTrafficOnly: true
defaultToOAuthAuthentication: true
allowBlobPublicAccess: false
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-linux-consumption/main.bicep#L37) file in the templates repository.

For more context, see the complete [storage-PrivateEndpoint.bicep](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd/blob/main/infra/app/storage-PrivateEndpoint.bicep) file in the sample repository.

You need to set the connection string of this storage account as the `AzureWebJobsStorage`

app setting, which Functions requires. The templates in this article construct this connection string value based on the created storage account, which is a best practice. For more information, see [Application configuration](#application-configuration).

### Deployment container

Deployments to an app running in the Flex Consumption plan require a container in Azure Blob Storage as the deployment source. You can use either the default storage account or you can specify a separate storage account. For more information, see [Configure deployment settings](flex-consumption-how-to#configure-deployment-settings).

This deployment account must already be configured when you create your app, including the specific container used for deployments. To learn more about configuring deployments, see [Deployment sources](#deployment-sources).

This example shows how to create a container in the storage account:

```
}
// Azure Functions Flex Consumption
module functionApp 'br/public:avm/res/web/site:0.16.0' = {
name: 'functionapp'
scope: rg
params: {
kind: 'functionapp,linux'
name: functionAppName_resolved
location: location
tags: union(tags, { 'azd-service-name': 'api' })
serverFarmResourceId: appServicePlan.outputs.resourceId
managedIdentities: {
systemAssigned: true
}
functionAppConfig: {
deployment: {
storage: {
type: 'blobContainer'
value: '${storage.outputs.primaryBlobEndpoint}${deploymentStorageContainerName}'
authentication: {
type: 'SystemAssignedIdentity'
}
```


This example shows how to use the [AVM for storage accounts](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/storage/storage-account) to create the blob storage container along with the storage account. For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L133).

Other deployment settings are [configured with the app itself](#deployment-sources).

### Enable storage logs

Because the storage account is used for important function app data, you should monitor the account for modification of that content. To monitor your storage account, you need to configure Azure Monitor resource logs for Azure Storage. In this example section, a Log Analytics workspace named `myLogAnalytics`

is used as the destination for these logs.

```
resource blobService 'Microsoft.Storage/storageAccounts/blobServices@2021-09-01' existing = {
name:'default'
parent:storageAccountName
}
resource storageDataPlaneLogs 'Microsoft.Insights/diagnosticSettings@2021-05-01-preview' = {
name: '${storageAccountName}-logs'
scope: blobService
properties: {
workspaceId: myLogAnalytics.id
logs: [
{
category: 'StorageWrite'
enabled: true
}
]
metrics: [
{
category: 'Transaction'
enabled: true
}
]
}
}
```


This same workspace can be used for the Application Insights resource defined later. For more information, including how to work with these logs, see [Monitoring Azure Storage](../storage/blobs/monitor-blob-storage).

## Create Application Insights

You should be using Application Insights for monitoring your function app executions. Application Insights now requires an Azure Log Analytics workspace, which can be shared. These examples assume you're using an existing workspace and have the fully qualified resource ID for the workspace. For more information, see [Azure Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-overview).

In this example section, the Application Insights resource is defined with the type `Microsoft.Insights/components`

and the kind `web`

:

```
resource applicationInsight 'Microsoft.Insights/components@2020-02-02' = {
name: applicationInsightsName
location: appInsightsLocation
tags: tags
kind: 'web'
properties: {
Application_Type: 'web'
WorkspaceResourceId: '<FULLY_QUALIFIED_RESOURCE_ID>'
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-linux-consumption/main.bicep#L60) file in the templates repository.

The connection must be provided to the function app using the [ APPLICATIONINSIGHTS_CONNECTION_STRING](functions-app-settings#applicationinsights_connection_string) application setting. For more information, see

[Application configuration](#application-configuration).

The examples in this article obtain the connection string value for the created instance. Older versions might instead use [ APPINSIGHTS_INSTRUMENTATIONKEY](functions-app-settings#appinsights_instrumentationkey) to set the instrumentation key, which is no longer recommended.

## Create the hosting plan

Apps hosted in an Azure Functions [Flex Consumption plan](flex-consumption-plan), [Premium plan](functions-premium-plan), or [Dedicated (App Service) plan](dedicated-plan) must have the hosting plan explicitly defined.

Flex Consumption is a Linux-based hosting plan that builds on the Consumption *pay for what you use* serverless billing model. The plan features support for private networking, instance memory size selection, and improved managed identity support.

A Flex Consumption plan is a special type of `serverfarm`

resource. You can specify it by using `FC1`

for the `Name`

property value in the `sku`

property with a `tier`

value of `FlexConsumption`

.

This example section creates a Flex Consumption plan:

```
scaleAndConcurrency: {
maximumInstanceCount: maximumInstanceCount
instanceMemoryMB: instanceMemoryMB
}
runtime: {
name: functionAppRuntime
version: functionAppRuntimeVersion
}
}
siteConfig: {
alwaysOn: false
}
configs: [{
name: 'appsettings'
properties:{
```


This example uses the [AVM for App Service plans](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/web/serverfarm). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L156).

Because the Flex Consumption plan currently only supports Linux, you must also set the `reserved`

property to `true`

.

The Premium plan offers the same scaling as the Consumption plan but includes dedicated resources and extra capabilities. To learn more, see [Azure Functions Premium Plan](functions-premium-plan).

A Premium plan is a special type of `serverfarm`

resource. You can specify it by using either `EP1`

, `EP2`

, or `EP3`

for the `Name`

property value in the `sku`

property. The way that you define the Functions hosting plan depends on whether your function app runs on Windows or on Linux. This example section creates an `EP1`

plan:

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
name: 'EP1'
tier: 'ElasticPremium'
family: 'EP'
}
kind: 'elastic'
properties: {
maximumElasticWorkerCount: 20
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-premium-plan/main.bicep#L62) file in the templates repository.

For more information about the `sku`

object, see [ SkuDefinition](/en-us/azure/templates/microsoft.web/serverfarms#skudescription) or review the example templates.

In the Dedicated (App Service) plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs in App Service plans, similar to web apps. For more information, see [Dedicated plan](dedicated-plan).

For a sample Bicep file/Azure Resource Manager template, see [Function app on Azure App Service plan](https://azure.microsoft.com/resources/templates/function-app-create-dedicated/).

In Functions, the Dedicated plan is just a regular App Service plan, which is defined by a `serverfarm`

resource. You must provide at least the `name`

value. For a list of supported plan names, see the `--sku`

setting in [ az appservice plan create](/en-us/cli/azure/appservice/plan#az-appservice-plan-create) for the current list of supported values for a Dedicated plan.

The way that you define the hosting plan depends on whether your function app runs on Windows or on Linux:

```
resource hostingPlanName 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
tier: 'Standard'
name: 'S1'
size: 'S1'
family: 'S'
capacity: 1
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/main.bicep#L62) file in the templates repository.

## Create the hosting plan

You don't need to explicitly define a Consumption hosting plan resource. When you skip this resource definition, a plan is automatically either created or selected on a per-region basis when you create the function app resource itself.

You can explicitly define a Consumption plan as a special type of `serverfarm`

resource, which you specify using the value `Dynamic`

for the `computeMode`

and `sku`

properties. This example section shows you how to explicitly define a consumption plan. The way that you define a hosting plan depends on whether your function app runs on Windows or on Linux.

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
name: 'Y1'
tier: 'Dynamic'
size: 'Y1'
family: 'Y'
capacity: 0
}
properties: {
computeMode: 'Dynamic'
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/main.bicep#L40) file in the templates repository.

## Kubernetes environment

Azure Functions can be deployed to [Azure Arc-enabled Kubernetes](../app-service/overview-arc-integration) either as a code project or a containerized function app.

To create the app and plan resources, you must have already [created an App Service Kubernetes environment](../app-service/manage-create-arc-environment) for an Azure Arc-enabled Kubernetes cluster. The examples in this article assume you have the resource ID of the custom location (`customLocationId`

) and App Service Kubernetes environment (`kubeEnvironmentId`

) to which you're deploying, which are set in this example:

```
param kubeEnvironmentId string
param customLocationId string
```


Both sites and plans must reference the custom location through an `extendedLocation`

field. As shown in this truncated example, `extendedLocation`

sits outside of `properties`

, as a peer to `kind`

and `location`

:

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
...
{
extendedLocation: {
name: customLocationId
}
}
}
```


The plan resource should use the Kubernetes (`K1`

) value for `SKU`

, the `kind`

field should be `linux,kubernetes`

, and the `reserved`

property should be `true`

, since it's a Linux deployment. You must also set the `extendedLocation`

and `kubeEnvironmentProfile.id`

to the custom location ID and the Kubernetes environment ID, respectively, which might look like this example section:

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
kind: 'linux,kubernetes'
sku: {
name: 'K1'
tier: 'Kubernetes'
}
extendedLocation: {
name: customLocationId
}
properties: {
kubeEnvironmentProfile: {
id: kubeEnvironmentId
}
reserved: true
}
}
```


## Create the function app

The function app resource is defined by a resource of type `Microsoft.Web/sites`

and `kind`

that includes `functionapp`

, at a minimum.

The way that you define a function app resource depends on whether you're hosting on Linux or on Windows:

For a list of application settings required when running on Windows, see [Application configuration](#application-configuration). For a sample Bicep file/Azure Resource Manager template, see the [function app hosted on Windows in a Consumption plan](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-windows-consumption) template.

For a list of application settings required when running on Windows, see [Application configuration](#application-configuration).

Flex Consumption replaces many of the standard application settings and site configuration properties used in Bicep and ARM template deployments. For more information, see [Application configuration](#application-configuration).

```
AzureWebJobsStorage__blobServiceUri: 'https://${storage.outputs.name}.blob.${environment().suffixes.storage}'
AzureWebJobsStorage__queueServiceUri: 'https://${storage.outputs.name}.queue.${environment().suffixes.storage}'
AzureWebJobsStorage__tableServiceUri: 'https://${storage.outputs.name}.table.${environment().suffixes.storage}'
// Application Insights settings are always included
APPLICATIONINSIGHTS_CONNECTION_STRING: applicationInsights.outputs.connectionString
APPLICATIONINSIGHTS_AUTHENTICATION_STRING: 'Authorization=AAD'
}
}]
}
}
// Consolidated Role Assignments
module rbacAssignments 'rbac.bicep' = {
name: 'rbacAssignments'
scope: rg
params: {
storageAccountName: storage.outputs.name
appInsightsName: applicationInsights.outputs.name
managedIdentityPrincipalId: functionApp.outputs.?systemAssignedMIPrincipalId ?? ''
userIdentityPrincipalId: principalId
allowUserIdentityPrincipal: !empty(principalId)
}
}
// Outputs
output AZURE_LOCATION string = location
output AZURE_TENANT_ID string = tenant().tenantId
output AZURE_FUNCTION_NAME string = functionApp.outputs.name
output APPLICATIONINSIGHTS_CONNECTION_STRING string = applicationInsights.outputs.connectionString
```


This example uses the [AVM for function apps](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/web/serverfarm). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L173).

Note

If you choose to optionally define your Consumption plan, you must set the `serverFarmId`

property on the app so that it points to the resource ID of the plan. Make sure that the function app has a `dependsOn`

setting that also references the plan. If you didn't explicitly define a plan, one gets created for you.

Set the `serverFarmId`

property on the app so that it points to the resource ID of the plan. Make sure that the function app has a `dependsOn`

setting that also references the plan.

```
resource functionAppName_resource 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp'
properties: {
serverFarmId: hostingPlanName.id
siteConfig: {
appSettings: [
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};EndpointSuffix=${environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'WEBSITE_CONTENTAZUREFILECONNECTIONSTRING'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};EndpointSuffix=${environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'WEBSITE_CONTENTSHARE'
value: toLower(functionAppName)
}
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'FUNCTIONS_WORKER_RUNTIME'
value: 'node'
}
{
name: 'WEBSITE_NODE_DEFAULT_VERSION'
value: '~14'
}
]
}
}
}
```


For a complete end-to-end example, see this [main.bicep file](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/main.bicep).

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp'
properties: {
serverFarmId: hostingPlan.id
siteConfig: {
alwaysOn: true
appSettings: [
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};EndpointSuffix=${environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'FUNCTIONS_WORKER_RUNTIME'
value: 'node'
}
{
name: 'WEBSITE_NODE_DEFAULT_VERSION'
value: '~14'
}
]
}
}
}
```


For a complete end-to-end example, see this [main.bicep file](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/main.bicep).

## Deployment sources

You can use the [ linuxFxVersion](functions-app-settings#linuxfxversion) site setting to request that a specific Linux container be deployed to your app when it's created. More settings are required to access images in a private repository. For more information, see

[Application configuration](#application-configuration).

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

Your Bicep file or ARM template can optionally also define a deployment for your function code, which could include these methods:

The Flex Consumption plan maintains your project code in zip-compressed package file in a blob storage container known as the *deployment container*. You can configure both the storage account and container used for deployment. For more information, see [Deployment](flex-consumption-plan#deployment).

You must use * one deploy* to publish your code package to the deployment container. During an ARM template or Bicep deployment, you can do this by

[defining a package source](#deployment-package)that uses the

`/onedeploy`

extension. If you choose to instead directly upload your package to the container, the package doesn't get automatically deployed.### Deployment container

The specific storage account and container used for deployments, the authentication method, and credentials are set in the `functionAppConfig.deployment.storage`

element of the `properties`

for the site. The container and any application settings must exist when the app is created. For an example of how to create the storage container, see [Deployment container](#deployment-container).

This example uses a system assigned managed identity to access the specified blob storage container, which is created elsewhere in the deployment:

```
// Consolidated Role Assignments
module rbacAssignments 'rbac.bicep' = {
name: 'rbacAssignments'
scope: rg
params: {
storageAccountName: storage.outputs.name
appInsightsName: applicationInsights.outputs.name
managedIdentityPrincipalId: functionApp.outputs.?systemAssignedMIPrincipalId ?? ''
userIdentityPrincipalId: principalId
allowUserIdentityPrincipal: !empty(principalId)
}
}
// Outputs
output AZURE_LOCATION string = location
output AZURE_TENANT_ID string = tenant().tenantId
output AZURE_FUNCTION_NAME string = functionApp.outputs.name
output APPLICATIONINSIGHTS_CONNECTION_STRING string = applicationInsights.outputs.connectionString
```


This example uses the [AVM for function apps](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/web/site). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L185).

When using managed identities, you must also enable the function app to access the storage account using the identity, as shown in this example:

```
module storageRoleAssignment_User 'br/public:avm/ptn/authorization/resource-role-assignment:0.1.2' = if (allowUserIdentityPrincipal && !empty(userIdentityPrincipalId)) {
name: 'storageRoleAssignment-User-${uniqueString(storageAccount.id, userIdentityPrincipalId)}'
params: {
resourceId: storageAccount.id
roleDefinitionId: roleDefinitions.storageBlobDataOwner
principalId: userIdentityPrincipalId
principalType: 'User'
description: 'Storage Blob Data Owner role for user identity (development/testing)'
roleName: 'Storage Blob Data Owner'
}
}
```


This example uses the [AVM for resource-scoped role assignment](https://github.com/Azure/bicep-registry-modules/tree/main/avm/ptn/authorization/resource-role-assignment). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/rbac.bicep#L45).

This example requires you to know the GUID value for the role being assigned. You can get this ID value for any friendly role name by using the [az role definition list](/en-us/cli/azure/role/definition#az-role-definition-list) command, as in this example:

```
az role definition list --output tsv --query "[?roleName=='Storage Blob Data Owner'].{name:name}"
```


When using a connection string instead of managed identities, you need to instead set the `authentication.type`

to `StorageAccountConnectionString`

and set `authentication.storageAccountConnectionStringName`

to the name of the application setting that contains the deployment storage account connection string.

### Deployment package

The Flex Consumption plan uses *one deploy* for deploying your code project. The code package itself is the same as you would use for zip deployment in other Functions hosting plans. However, the name of the package file itself must be `released-package.zip`

.

To include a one deploy package in your template, use the `/onedeploy`

resource definition for the remote URL that contains the deployment package. The Functions host must be able to access both this remote package source and the deployment container.

This example adds a one deploy source to an existing app:

```
@description('The name of the function app.')
param functionAppName string
@description('The location into which the resources should be deployed.')
param location string = resourceGroup().location
@description('The zip content URL for released-package.zip.')
param packageUri string
resource functionAppName_OneDeploy 'Microsoft.Web/sites/extensions@2022-09-01' = {
name: '${functionAppName}/onedeploy'
location: location
properties: {
packageUri: packageUri
remoteBuild: false
}
}
```


Your Bicep file or ARM template can optionally also define a deployment for your function code using a [zip deployment package](deployment-zip-push).

To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure. In most examples, top-level configurations are applied by using `siteConfig`

. It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine. Top-level information is required before the child `sourcecontrols/web`

resource is applied. Although it's possible to configure these settings in the child-level `config/appSettings`

resource, in some cases your function app must be deployed *before* `config/appSettings`

is applied.

## Zip deployment package

Zip deployment is a recommended way to deploy your function app code. By default, functions that use zip deployment run in the deployment package itself. For more information, including the requirements for a deployment package, see [Zip deployment for Azure Functions](deployment-zip-push). When using resource deployment automation, you can reference the .zip deployment package in your Bicep or ARM template.

To use zip deployment in your template, set the `WEBSITE_RUN_FROM_PACKAGE`

setting in the app to `1`

and include the `/zipDeploy`

resource definition.

For a Consumption plan on Linux, instead set the URI of the deployment package directly in the `WEBSITE_RUN_FROM_PACKAGE`

setting, as shown in [this example template](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-linux-consumption#L152).

This example adds a zip deployment source to an existing app:

```
@description('The name of the function app.')
param functionAppName string
@description('The location into which the resources should be deployed.')
param location string = resourceGroup().location
@description('The zip content url.')
param packageUri string
resource functionAppName_ZipDeploy 'Microsoft.Web/sites/extensions@2021-02-01' = {
name: '${functionAppName}/ZipDeploy'
location: location
properties: {
packageUri: packageUri
}
}
```


Keep the following things in mind when including zip deployment resources in your template:

- Consumption plans on Linux don't support
`WEBSITE_RUN_FROM_PACKAGE = 1`

. You must instead set the URI of the deployment package directly in the`WEBSITE_RUN_FROM_PACKAGE`

setting. For more information, see[WEBSITE_RUN_FROM_PACKAGE](functions-app-settings#website_run_from_package). For an example template, see[Function app hosted on Linux in a Consumption plan](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-linux-consumption).

The

`packageUri`

must be a location that can be accessed by Functions. Consider using Azure blob storage with a shared access signature (SAS). After the SAS expires, Functions can no longer access the share for deployments. When you regenerate your SAS, remember to update the`WEBSITE_RUN_FROM_PACKAGE`

setting with the new URI value.When setting

`WEBSITE_RUN_FROM_PACKAGE`

to a URI, you must[manually sync triggers](functions-deployment-technologies#trigger-syncing).Make sure to always set all required application settings in the

`appSettings`

collection when adding or updating settings. Existing settings not explicitly set are removed by the update. For more information, see[Application configuration](#application-configuration).Functions doesn't support Web Deploy (

`msdeploy`

) for package deployments. You must instead use zip deployment in your deployment pipelines and automation. For more information, see[Zip deployment for Azure Functions](deployment-zip-push).

## Remote builds

The deployment process assumes that the .zip file that you use or a zip deployment contains a ready-to-run app. This means that by default no customizations are run.

There are scenarios that require you to rebuild your app remotely. One such example is when you need to include Linux-specific packages in Python or Node.js apps that you developed on a Windows computer. In this case, you can configure Functions to perform a remote build on your code after the zip deployment.

The way that you request a remote build depends on the operating system to which you're deploying:

When an app is deployed to Windows, language-specific commands (like `dotnet restore`

for C# apps or `npm install`

for Node.js apps) are run.

To enable the same build processes that you get with continuous integration, add `SCM_DO_BUILD_DURING_DEPLOYMENT=true`

to your application settings in your deployment code and remove the `WEBSITE_RUN_FROM_PACKAGE`

entirely.

## Linux containers

If you're deploying a [containerized function app](functions-how-to-custom-container) to an Azure Functions Premium or Dedicated plan, you must:

- Set the
site setting with the identifier of your container image.`linuxFxVersion`

- Set any required
settings when obtaining the container from a private registry.`DOCKER_REGISTRY_SERVER_*`

- Set
application setting to`WEBSITES_ENABLE_APP_SERVICE_STORAGE`

`false`

.

If some settings are missing, the application provisioning might fail with this HTTP/500 error:


`Function app provisioning failed.`


For more information, see [Application configuration](#application-configuration).

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp'
properties: {
serverFarmId: hostingPlan.id
siteConfig: {
appSettings: [
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'FUNCTIONS_WORKER_RUNTIME'
value: 'node'
}
{
name: 'WEBSITE_NODE_DEFAULT_VERSION'
value: '~14'
}
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'DOCKER_REGISTRY_SERVER_URL'
value: dockerRegistryUrl
}
{
name: 'DOCKER_REGISTRY_SERVER_USERNAME'
value: dockerRegistryUsername
}
{
name: 'DOCKER_REGISTRY_SERVER_PASSWORD'
value: dockerRegistryPassword
}
{
name: 'WEBSITES_ENABLE_APP_SERVICE_STORAGE'
value: 'false'
}
]
linuxFxVersion: 'DOCKER|myacr.azurecr.io/myimage:mytag'
}
}
dependsOn: [
storageAccount
]
}
```


When deploying [containerized functions to Azure Container Apps](../container-apps/functions-overview), your template must:

- Set the
`kind`

field to a value of`functionapp,linux,container,azurecontainerapps`

. - Set the
`managedEnvironmentId`

site property to the fully qualified URI of the Container Apps environment. - Add a resource link in the site's
`dependsOn`

collection when creating a`Microsoft.App/managedEnvironments`

resource at the same time as the site.

The definition of a containerized function app deployed from a private container registry to an existing Container Apps environment might look like this example:

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
kind: 'functionapp,linux,container,azurecontainerapps'
location: location
properties: {
serverFarmId: hostingPlanName
siteConfig: {
linuxFxVersion: 'DOCKER|myacr.azurecr.io/myimage:mytag'
appSettings: [
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
]
}
managedEnvironmentId: managedEnvironmentId
}
dependsOn: [
storageAccount
hostingPlan
]
}
```


When deploying functions to Azure Arc, the value you set for the `kind`

field of the function app resource depends on the type of deployment:

| Deployment type | `kind` field value |
|---|---|
| Code-only deployment | `functionapp,linux,kubernetes` |
| Container deployment | `functionapp,linux,kubernetes,container` |

You must also set the `customLocationId`

as you did for the [hosting plan resource](#create-the-hosting-plan).

The definition of a containerized function app, using a .NET 6 quickstart image, might look like this example:

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
kind: 'kubernetes,functionapp,linux,container'
location: location
extendedLocation: {
name: customLocationId
}
properties: {
serverFarmId: hostingPlanName
siteConfig: {
linuxFxVersion: 'DOCKER|mcr.microsoft.com/azure-functions/4-dotnet-isolated6.0-appservice-quickstart'
appSettings: [
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
]
alwaysOn: true
}
}
dependsOn: [
storageAccount
hostingPlan
]
}
```


## Application configuration

In a Flex Consumption plan, you configure your function app in Azure with two types of properties:

| Configuration | `Microsoft.Web/sites` property |
|---|---|
| Application configuration | `functionAppConfig` |
| Application settings | `siteConfig.appSettings` collection |

These application configurations are maintained in `functionAppConfig`

:

| Behavior | Setting in `functionAppConfig` |
|---|---|
|

`scaleAndConcurrency.alwaysReady`

[Deployment source](#deployment-sources)`deployment`

[Instance size](flex-consumption-plan#instance-sizes)`scaleAndConcurrency.instanceMemoryMB`

[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency)`scaleAndConcurrency.triggers.http.perInstanceConcurrency`

[Language runtime](functions-app-settings#functions_worker_runtime)`runtime.name`

[Language version](supported-languages)`runtime.version`

[Maximum instance count](event-driven-scaling#flex-consumption-plan)`scaleAndConcurrency.maximumInstanceCount`

[Site update strategy](flex-consumption-site-updates)`siteUpdateStrategy.type`

The Flex Consumption plan also supports these application settings:

- Connection string-based settings:
- Managed identity-based settings:

Functions provides the following options for configuring your function app in Azure:

| Configuration | `Microsoft.Web/sites` property |
|---|---|
| Site settings | `siteConfig` |
| Application settings | `siteConfig.appSettings` collection |

These site settings are required on the `siteConfig`

property:

These site settings are required only when using managed identities to obtain the image from an Azure Container Registry instance:

These application settings are required (or recommended) for a specific operating system and hosting option:

These application settings are required for container deployments:

These settings are only required when deploying from a private container registry:

Keep these considerations in mind when working with site and application settings using Bicep files or ARM templates:

- The optional
`alwaysReady`

setting contains an array of one or more`{name,instanceCount}`

objects, with one for each[per-function scale group](flex-consumption-plan#per-function-scaling). These are the scale groups being used to make always-ready scale decisions. This example sets always-ready counts for both the`http`

group and a single function named`helloworld`

, which is of a nongrouped trigger type:`alwaysReady: [ { name: 'http' instanceCount: 2 } { name: 'function:helloworld' instanceCount: 1 } ]`


- There are important considerations for when you should set
`WEBSITE_CONTENTSHARE`

in an automated deployment. For detailed guidance, see thereference.`WEBSITE_CONTENTSHARE`


- For container deployments, also set
to`WEBSITES_ENABLE_APP_SERVICE_STORAGE`

`false`

, since your app content is provided in the container itself.

You should always define your application settings as a

`siteConfig/appSettings`

collection of the`Microsoft.Web/sites`

resource being created, as is done in the examples in this article. This definition guarantees the settings your function app needs to run are available on initial startup.When adding or updating application settings using templates, make sure that you include all existing settings with the update. You must do this because the underlying update REST API calls replace the entire

`/config/appsettings`

resource. If you remove the existing settings, your function app won't run. To programmatically update individual application settings, you can instead use the Azure CLI, Azure PowerShell, or the Azure portal to make these changes. For more information, see[Work with application settings](functions-how-to-use-azure-function-app-settings#settings).When possible, you should use managed identity-based connections to other Azure services, including the

`AzureWebJobsStorage`

connection. For more information, see[Configure an identity-based connection](functions-reference#configure-an-identity-based-connection).

## Slot deployments

Functions lets you deploy different versions of your code to unique endpoints in your function app. This option makes it easier to develop, validate, and deploy functions updates without impacting functions running in production. Deployment slots is a feature of Azure App Service. The number of slots available [depends on your hosting plan](functions-scale#service-limits). For more information, see [Azure Functions deployment slots](functions-deployment-slots) functions.

A slot resource is defined in the same way as a function app resource (`Microsoft.Web/sites`

), but instead you use the `Microsoft.Web/sites/slots`

resource identifier. For an example deployment (in both Bicep and ARM templates) that creates both a production and a staging slot in a Premium plan, see [Azure Function App with a Deployment Slot](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-deployment-slot).

To learn about how to swap slots by using templates, see [Automate with Resource Manager templates](../app-service/deploy-staging-slots#automate-with-resource-manager-templates).

Keep the following considerations in mind when working with slot deployments:

Don't explicitly set the

`WEBSITE_CONTENTSHARE`

setting in the deployment slot definition. This setting is generated for you when the app is created in the deployment slot.When you swap slots, some application settings are considered "sticky," in that they stay with the slot and not with the code being swapped. You can define such a

*slot setting*by including`"slotSetting":true`

in the specific application setting definition in your template. For more information, see[Manage settings](functions-deployment-slots#manage-settings).

## Secured deployments

You can create your function app in a deployment where one or more of the resources have been secured by integrating with virtual networks. Virtual network integration for your function app is defined by a `Microsoft.Web/sites/networkConfig`

resource. This integration depends on both the referenced function app and virtual network resources. Your function app might also depend on other private networking resources, such as private endpoints and routes. For more information, see [Azure Functions networking options](functions-networking-options).

These projects provide Bicep-based examples of how to deploy your function apps in a virtual network, including with network access restrictions:

[High-scale HTTP triggered function connects to an event hub secured by a virtual network](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md): An HTTP triggered function (.NET isolated worker mode) accepts calls from any source and then sends the body of those HTTP calls to a secure event hub running in a virtual network by using virtual network integration.[Function is triggered by a Service Bus queue secured in a virtual network](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md): A Python function is triggered by a Service Bus queue secured in a virtual network. The queue is accessed in the virtual network using private endpoint. A virtual machine in the virtual network is used to send messages.

When creating a deployment that uses a secured storage account, you must both explicitly set the `WEBSITE_CONTENTSHARE`

setting and create the file share resource named in this setting. Make sure you create a `Microsoft.Storage/storageAccounts/fileServices/shares`

resource using the value of `WEBSITE_CONTENTSHARE`

, as shown in this example ([ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-private-endpoints-storage-private-endpoints/azuredeploy.json#L467)|[Bicep file](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-private-endpoints-storage-private-endpoints/main.bicep#L351)). You'll also need to set the site property `vnetContentShareEnabled`

to true.

Note

When these settings aren't part of a deployment that uses a secured storage account, you see this error during deployment validation: `Could not access storage account using provided connection string`

.

These projects provide both Bicep and ARM template examples of how to deploy your function apps in a virtual network, including with network access restrictions:

| Restricted scenario | Description |
|---|---|
|

[Virtual network integration](functions-networking-options#virtual-network-integration).[Create a function app that accesses a secured storage account](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-storage-private-endpoints)[Restrict your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network).[Create a function app and storage account that both use private endpoints](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-private-endpoints-storage-private-endpoints)[Private endpoints](functions-networking-options#private-endpoints).### Restricted network settings

You might also need to use these settings when your function app has network restrictions:

| Setting | Value | Description |
|---|---|---|
`WEBSITE_CONTENTOVERVNET` |

`1`

[Restrict your storage account to a virtual network](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).`vnetrouteallenabled`

`1`

[Regional virtual network integration](functions-networking-options#regional-virtual-network-integration). This site setting supersedes the application setting[.](functions-app-settings#website_vnet_route_all)`WEBSITE_VNET_ROUTE_ALL`

### Considerations for network restrictions

When you're restricting access to the storage account through the private endpoints, you aren't able to access the storage account through the portal or any device outside the virtual network. You can give access to your secured IP address or virtual network in the storage account by [Managing the default network access rule](../storage/common/storage-network-security-set-default-access).

## Function access keys

Host-level [function access keys](function-keys-how-to) are defined as Azure resources. This means that you can create and manage host keys in your ARM templates and Bicep files. A host key is defined as a resource of type `Microsoft.Web/sites/host/functionKeys`

. This example creates a host-level access key named `my_custom_key`

when the function app is created:

```
resource functionKey 'Microsoft.Web/sites/host/functionKeys@2022-09-01' = {
name: '${parameters('name')}/default/my_custom_key'
properties: {
name: 'my_custom_key'
}
dependsOn: [
resourceId('Microsoft.Web/Sites', parameters('name'))
]
}
```


In this example, the `name`

parameter is the name of the new function app. You must include a `dependsOn`

setting to guarantee that the key is created with the new function app. Finally, the `properties`

object of the host key can also include a `value`

property that can be used to set a specific key.

When you don't set the `value`

property, Functions automatically generates a new key for you when the resource is created, which is recommended. To learn more about access keys, including security best practices for working with access keys, see [Work with access keys in Azure Functions](function-keys-how-to).

## Create your template

Experts with Bicep or ARM templates can manually code their deployments using a simple text editor. For the rest of us, there are several ways to make the development process easier:

**Visual Studio Code**: There are extensions available to help you work with both[Bicep files](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-bicep)and[ARM templates](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools). You can use these tools to help make sure that your code is correct, and they provide some[basic validation](functions-infrastructure-as-code?tabs=vs-code#validate-your-template).**Azure portal**: When you[create your function app and related resources in the portal](functions-create-function-app-portal), the final**Review + create**screen has a**Download a template for automation**link.This link shows you the ARM template generated based on the options you chose in portal. This template can seem a bit complex when you're creating a function app with many new resources. However, it can provide a good reference for how your ARM template might look.


## Validate your template

When you manually create your deployment template file, it's important to validate your template before deployment. All deployment methods validate your template syntax and raise a `validation failed`

error message as shown in the following JSON formatted example:

```
{"error":{"code":"InvalidTemplate","message":"Deployment template validation failed: 'The resource 'Microsoft.Web/sites/func-xyz' is not defined in the template. Please see https://aka.ms/arm-template for usage details.'.","additionalInfo":[{"type":"TemplateViolation","info":{"lineNumber":0,"linePosition":0,"path":""}}]}}
```


The following methods can be used to validate your template before deployment:

The following [Azure resource group deployment v2 task](/en-us/azure/devops/pipelines/tasks/deploy/azure-resource-group-deployment?view=azure-devops&preserve-view=true) with `deploymentMode: 'Validation'`

instructs Azure Pipelines to validate the template.

```
- task: AzureResourceManagerTemplateDeployment@3
inputs:
deploymentScope: 'Resource Group'
subscriptionId: # Required subscription ID
action: 'Create Or Update Resource Group'
resourceGroupName: # Required resource group name
location: # Required when action == Create Or Update Resource Group
templateLocation: 'Linked artifact'
csmFile: # Required when TemplateLocation == Linked Artifact
csmParametersFile: # Optional
deploymentMode: 'Validation'
```


You can also create a test resource group to find [preflight](../azure-resource-manager/troubleshooting/quickstart-troubleshoot-arm-deployment?tabs=azure-cli#fix-preflight-error) and [deployment](../azure-resource-manager/troubleshooting/quickstart-troubleshoot-arm-deployment?tabs=azure-cli#fix-deployment-error) errors.

## Deploy your template

You can use any of the following ways to deploy your Bicep file and template:

### Deploy to Azure button

Note

This method doesn't support deploying Bicep files currently.

Replace `<url-encoded-path-to-azuredeploy-json>`

with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json`

file in GitHub.

Here's an example that uses markdown:

```
[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```


Here's an example that uses HTML:

```
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="https://azuredeploy.net/deploybutton.png"></a>
```


### Deploy using PowerShell

The following PowerShell commands create a resource group and deploy a Bicep file or ARM template that creates a function app with its required resources. To run locally, you must have [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) installed. To sign in to Azure, you must first run [ Connect-AzAccount](/en-us/powershell/module/az.accounts/connect-azaccount).

```
# Register Resource Providers if they're not already registered
Register-AzResourceProvider -ProviderNamespace "microsoft.web"
Register-AzResourceProvider -ProviderNamespace "microsoft.storage"
# Create a resource group for the function app
New-AzResourceGroup -Name "MyResourceGroup" -Location 'West Europe'
# Deploy the template
New-AzResourceGroupDeployment -ResourceGroupName "MyResourceGroup" -TemplateFile main.bicep -Verbose
```


To test out this deployment, you can use a [template like this one](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/function-app-create-dynamic) that creates a function app on Windows in a Consumption plan.

## Next steps

Learn more about how to develop and configure Azure Functions.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-infrastructure-as-code -->

# Automate resource deployment for your function app in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use a Bicep file or an Azure Resource Manager (ARM) template to automate the process of deploying your function app. During the deployment, you can use existing Azure resources or create new ones.

You can obtain these benefits in your production apps by using deployment automation, both infrastructure-as-code (IaC) and continuous integration and deployment (CI/CD):

**Consistency**: Define your infrastructure in code to ensure consistent deployments across environments.**Version Control**: Track changes to your infrastructure and application configurations in source control, along with your project code.**Automation**: Automate deployment, which reduces manual errors and shortens release process.**Scalability**: Easily replicate infrastructure for multiple environments, such as development, testing, and production.**Disaster Recovery**: Quickly recreate infrastructure after failures or during migrations.

This article shows you how to automate the creation of Azure resources and deployment configurations for Azure Functions. To learn more about continuous deployment of your project code, see [Continuous deployment for Azure Functions](functions-continuous-deployment).

The template code to create the required Azure resources depends on the desired hosting options for your function app. This article supports the following hosting options:

| Hosting option | Deployment type | Sample templates |
|---|---|---|
|

[Bicep](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.web/function-app-flex-managed-identities/main.bicep)[ARM template](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.web/function-app-flex-managed-identities/azuredeploy.json)[Terraform](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC/terraformazurerm)[Premium plan](functions-premium-plan)[Bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-premium-plan/main.bicep)[ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-premium-plan/azuredeploy.json)[Dedicated plan](dedicated-plan)[Bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/main.bicep)[ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/azuredeploy.json)[Azure Container Apps](../container-apps/functions-overview)[Bicep](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/ACAKindfunctionapp)[Consumption plan](consumption-plan)[Bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/main.bicep)[ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/azuredeploy.json)Make sure to select your hosting plan at the top of the article.

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

When using this article, keep these considerations in mind:

There's no canonical way to structure an ARM template.

A Bicep deployment can be modularized into multiple Bicep files and

[Azure Verified Modules (AVMs)](https://azure.github.io/Azure-Verified-Modules/overview/introduction/).This article assumes that you have a basic understanding of

[creating Bicep files](../azure-resource-manager/bicep/file)or[authoring Azure Resource Manager templates](../azure-resource-manager/templates/syntax).

- Examples are shown as individual sections for specific resources. For a broad set of complete Bicep file and ARM template examples, see
[these function app deployment examples](/en-us/samples/browse/?expanded=azure&terms=%22azure%20functions%22&products=azure-resource-manager).

- Examples are shown as individual sections for specific resources. For Bicep,
[Azure Verified Modules (AVM)](https://azure.github.io/Azure-Verified-Modules/)are shown, when available. For a broad set of complete Bicep file and ARM template examples, see[these Flex Consumption app deployment examples](/en-us/samples/browse/?expanded=azure&terms=%22azure%20functions%20flex%22&products=azure-resource-manager).

- Examples are shown as individual sections for specific resources.

## Required resources

You must create or configure these resources for an Azure Functions-hosted deployment:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)*[hosting plan](#create-the-hosting-plan)[Microsoft.Web/serverfarms](/en-us/azure/templates/microsoft.web/serverfarms)[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)You must create or configure these resources for an Azure Functions-hosted deployment:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)*[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)An Azure Container Apps-hosted deployment typically consists of these resources:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)*[managed environment](../container-apps/functions-overview#)[Microsoft.App/managedEnvironments](/en-us/azure/templates/microsoft.app/managedenvironments)[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)An Azure Arc-hosted deployment typically consists of these resources:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)1[App Service Kubernetes environment](../app-service/overview-arc-integration#app-service-kubernetes-environment)[Microsoft.ExtendedLocation/customLocations](/en-us/azure/templates/microsoft.extendedlocation/customlocations)[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)*If you don't already have a Log Analytics Workspace that can be used by your Application Insights instance, you also need to create this resource.

When you deploy multiple resources in a single Bicep file or ARM template, the order in which resources are created is important. This requirement is a result of dependencies between resources. For such dependencies, make sure to use the `dependsOn`

element to define the dependency in the dependent resource. For more information, see either [Define the order for deploying resources in ARM templates](../azure-resource-manager/templates/resource-dependency) or [Resource dependencies in Bicep](../azure-resource-manager/bicep/resource-dependencies).

## Prerequisites

- The examples are designed to execute in the context of an existing resource group.
- Both Application Insights and storage logs require you to have an existing
[Azure Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-overview). Workspaces can be shared between services, and as a rule of thumb you should create a workspace in each geographic region to improve performance. For an example of how to create a Log Analytics workspace, see[Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace?tabs=azure-resource-manager#create-a-workspace). You can find the fully qualified workspace resource ID in a workspace page in the[Azure portal](https://portal.azure.com)under**Settings**>**Properties**>**Resource ID**.

- This article assumes that you have already created a
[managed environment](../container-apps/environment)in Azure Container Apps. You need both the name and the ID of the managed environment to create a function app hosted on Container Apps.

- This article assumes that you have already created an
[App Service-enabled custom location](../app-service/overview-arc-integration)on an[Azure Arc-enabled Kubernetes cluster](/en-us/azure/azure-arc/kubernetes/overview). You need both the custom location ID and the Kubernetes environment ID to create a function app hosted in an Azure Arc custom location.

## Create storage account

All function apps require an Azure storage account. You need a general purpose account that supports blobs, tables, queues, and files. For more information, see [Azure Functions storage account requirements](storage-considerations#storage-account-requirements).

Important

The storage account is used to store important app data, sometimes including the application code itself. You should limit access from other apps and users to the storage account.

This example section creates a Standard general purpose v2 storage account:

```
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-05-01' = {
name: storageAccountName
location: location
kind: 'StorageV2'
sku: {
name: 'Standard_LRS'
}
properties: {
supportsHttpsTrafficOnly: true
defaultToOAuthAuthentication: true
allowBlobPublicAccess: false
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-linux-consumption/main.bicep#L37) file in the templates repository.

For more context, see the complete [storage-PrivateEndpoint.bicep](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd/blob/main/infra/app/storage-PrivateEndpoint.bicep) file in the sample repository.

You need to set the connection string of this storage account as the `AzureWebJobsStorage`

app setting, which Functions requires. The templates in this article construct this connection string value based on the created storage account, which is a best practice. For more information, see [Application configuration](#application-configuration).

### Deployment container

Deployments to an app running in the Flex Consumption plan require a container in Azure Blob Storage as the deployment source. You can use either the default storage account or you can specify a separate storage account. For more information, see [Configure deployment settings](flex-consumption-how-to#configure-deployment-settings).

This deployment account must already be configured when you create your app, including the specific container used for deployments. To learn more about configuring deployments, see [Deployment sources](#deployment-sources).

This example shows how to create a container in the storage account:

```
}
// Azure Functions Flex Consumption
module functionApp 'br/public:avm/res/web/site:0.16.0' = {
name: 'functionapp'
scope: rg
params: {
kind: 'functionapp,linux'
name: functionAppName_resolved
location: location
tags: union(tags, { 'azd-service-name': 'api' })
serverFarmResourceId: appServicePlan.outputs.resourceId
managedIdentities: {
systemAssigned: true
}
functionAppConfig: {
deployment: {
storage: {
type: 'blobContainer'
value: '${storage.outputs.primaryBlobEndpoint}${deploymentStorageContainerName}'
authentication: {
type: 'SystemAssignedIdentity'
}
```


This example shows how to use the [AVM for storage accounts](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/storage/storage-account) to create the blob storage container along with the storage account. For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L133).

Other deployment settings are [configured with the app itself](#deployment-sources).

### Enable storage logs

Because the storage account is used for important function app data, you should monitor the account for modification of that content. To monitor your storage account, you need to configure Azure Monitor resource logs for Azure Storage. In this example section, a Log Analytics workspace named `myLogAnalytics`

is used as the destination for these logs.

```
resource blobService 'Microsoft.Storage/storageAccounts/blobServices@2021-09-01' existing = {
name:'default'
parent:storageAccountName
}
resource storageDataPlaneLogs 'Microsoft.Insights/diagnosticSettings@2021-05-01-preview' = {
name: '${storageAccountName}-logs'
scope: blobService
properties: {
workspaceId: myLogAnalytics.id
logs: [
{
category: 'StorageWrite'
enabled: true
}
]
metrics: [
{
category: 'Transaction'
enabled: true
}
]
}
}
```


This same workspace can be used for the Application Insights resource defined later. For more information, including how to work with these logs, see [Monitoring Azure Storage](../storage/blobs/monitor-blob-storage).

## Create Application Insights

You should be using Application Insights for monitoring your function app executions. Application Insights now requires an Azure Log Analytics workspace, which can be shared. These examples assume you're using an existing workspace and have the fully qualified resource ID for the workspace. For more information, see [Azure Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-overview).

In this example section, the Application Insights resource is defined with the type `Microsoft.Insights/components`

and the kind `web`

:

```
resource applicationInsight 'Microsoft.Insights/components@2020-02-02' = {
name: applicationInsightsName
location: appInsightsLocation
tags: tags
kind: 'web'
properties: {
Application_Type: 'web'
WorkspaceResourceId: '<FULLY_QUALIFIED_RESOURCE_ID>'
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-linux-consumption/main.bicep#L60) file in the templates repository.

The connection must be provided to the function app using the [ APPLICATIONINSIGHTS_CONNECTION_STRING](functions-app-settings#applicationinsights_connection_string) application setting. For more information, see

[Application configuration](#application-configuration).

The examples in this article obtain the connection string value for the created instance. Older versions might instead use [ APPINSIGHTS_INSTRUMENTATIONKEY](functions-app-settings#appinsights_instrumentationkey) to set the instrumentation key, which is no longer recommended.

## Create the hosting plan

Apps hosted in an Azure Functions [Flex Consumption plan](flex-consumption-plan), [Premium plan](functions-premium-plan), or [Dedicated (App Service) plan](dedicated-plan) must have the hosting plan explicitly defined.

Flex Consumption is a Linux-based hosting plan that builds on the Consumption *pay for what you use* serverless billing model. The plan features support for private networking, instance memory size selection, and improved managed identity support.

A Flex Consumption plan is a special type of `serverfarm`

resource. You can specify it by using `FC1`

for the `Name`

property value in the `sku`

property with a `tier`

value of `FlexConsumption`

.

This example section creates a Flex Consumption plan:

```
scaleAndConcurrency: {
maximumInstanceCount: maximumInstanceCount
instanceMemoryMB: instanceMemoryMB
}
runtime: {
name: functionAppRuntime
version: functionAppRuntimeVersion
}
}
siteConfig: {
alwaysOn: false
}
configs: [{
name: 'appsettings'
properties:{
```


This example uses the [AVM for App Service plans](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/web/serverfarm). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L156).

Because the Flex Consumption plan currently only supports Linux, you must also set the `reserved`

property to `true`

.

The Premium plan offers the same scaling as the Consumption plan but includes dedicated resources and extra capabilities. To learn more, see [Azure Functions Premium Plan](functions-premium-plan).

A Premium plan is a special type of `serverfarm`

resource. You can specify it by using either `EP1`

, `EP2`

, or `EP3`

for the `Name`

property value in the `sku`

property. The way that you define the Functions hosting plan depends on whether your function app runs on Windows or on Linux. This example section creates an `EP1`

plan:

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
name: 'EP1'
tier: 'ElasticPremium'
family: 'EP'
}
kind: 'elastic'
properties: {
maximumElasticWorkerCount: 20
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-premium-plan/main.bicep#L62) file in the templates repository.

For more information about the `sku`

object, see [ SkuDefinition](/en-us/azure/templates/microsoft.web/serverfarms#skudescription) or review the example templates.

In the Dedicated (App Service) plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs in App Service plans, similar to web apps. For more information, see [Dedicated plan](dedicated-plan).

For a sample Bicep file/Azure Resource Manager template, see [Function app on Azure App Service plan](https://azure.microsoft.com/resources/templates/function-app-create-dedicated/).

In Functions, the Dedicated plan is just a regular App Service plan, which is defined by a `serverfarm`

resource. You must provide at least the `name`

value. For a list of supported plan names, see the `--sku`

setting in [ az appservice plan create](/en-us/cli/azure/appservice/plan#az-appservice-plan-create) for the current list of supported values for a Dedicated plan.

The way that you define the hosting plan depends on whether your function app runs on Windows or on Linux:

```
resource hostingPlanName 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
tier: 'Standard'
name: 'S1'
size: 'S1'
family: 'S'
capacity: 1
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/main.bicep#L62) file in the templates repository.

## Create the hosting plan

You don't need to explicitly define a Consumption hosting plan resource. When you skip this resource definition, a plan is automatically either created or selected on a per-region basis when you create the function app resource itself.

You can explicitly define a Consumption plan as a special type of `serverfarm`

resource, which you specify using the value `Dynamic`

for the `computeMode`

and `sku`

properties. This example section shows you how to explicitly define a consumption plan. The way that you define a hosting plan depends on whether your function app runs on Windows or on Linux.

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
name: 'Y1'
tier: 'Dynamic'
size: 'Y1'
family: 'Y'
capacity: 0
}
properties: {
computeMode: 'Dynamic'
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/main.bicep#L40) file in the templates repository.

## Kubernetes environment

Azure Functions can be deployed to [Azure Arc-enabled Kubernetes](../app-service/overview-arc-integration) either as a code project or a containerized function app.

To create the app and plan resources, you must have already [created an App Service Kubernetes environment](../app-service/manage-create-arc-environment) for an Azure Arc-enabled Kubernetes cluster. The examples in this article assume you have the resource ID of the custom location (`customLocationId`

) and App Service Kubernetes environment (`kubeEnvironmentId`

) to which you're deploying, which are set in this example:

```
param kubeEnvironmentId string
param customLocationId string
```


Both sites and plans must reference the custom location through an `extendedLocation`

field. As shown in this truncated example, `extendedLocation`

sits outside of `properties`

, as a peer to `kind`

and `location`

:

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
...
{
extendedLocation: {
name: customLocationId
}
}
}
```


The plan resource should use the Kubernetes (`K1`

) value for `SKU`

, the `kind`

field should be `linux,kubernetes`

, and the `reserved`

property should be `true`

, since it's a Linux deployment. You must also set the `extendedLocation`

and `kubeEnvironmentProfile.id`

to the custom location ID and the Kubernetes environment ID, respectively, which might look like this example section:

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
kind: 'linux,kubernetes'
sku: {
name: 'K1'
tier: 'Kubernetes'
}
extendedLocation: {
name: customLocationId
}
properties: {
kubeEnvironmentProfile: {
id: kubeEnvironmentId
}
reserved: true
}
}
```


## Create the function app

The function app resource is defined by a resource of type `Microsoft.Web/sites`

and `kind`

that includes `functionapp`

, at a minimum.

The way that you define a function app resource depends on whether you're hosting on Linux or on Windows:

For a list of application settings required when running on Windows, see [Application configuration](#application-configuration). For a sample Bicep file/Azure Resource Manager template, see the [function app hosted on Windows in a Consumption plan](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-windows-consumption) template.

For a list of application settings required when running on Windows, see [Application configuration](#application-configuration).

Flex Consumption replaces many of the standard application settings and site configuration properties used in Bicep and ARM template deployments. For more information, see [Application configuration](#application-configuration).

```
AzureWebJobsStorage__blobServiceUri: 'https://${storage.outputs.name}.blob.${environment().suffixes.storage}'
AzureWebJobsStorage__queueServiceUri: 'https://${storage.outputs.name}.queue.${environment().suffixes.storage}'
AzureWebJobsStorage__tableServiceUri: 'https://${storage.outputs.name}.table.${environment().suffixes.storage}'
// Application Insights settings are always included
APPLICATIONINSIGHTS_CONNECTION_STRING: applicationInsights.outputs.connectionString
APPLICATIONINSIGHTS_AUTHENTICATION_STRING: 'Authorization=AAD'
}
}]
}
}
// Consolidated Role Assignments
module rbacAssignments 'rbac.bicep' = {
name: 'rbacAssignments'
scope: rg
params: {
storageAccountName: storage.outputs.name
appInsightsName: applicationInsights.outputs.name
managedIdentityPrincipalId: functionApp.outputs.?systemAssignedMIPrincipalId ?? ''
userIdentityPrincipalId: principalId
allowUserIdentityPrincipal: !empty(principalId)
}
}
// Outputs
output AZURE_LOCATION string = location
output AZURE_TENANT_ID string = tenant().tenantId
output AZURE_FUNCTION_NAME string = functionApp.outputs.name
output APPLICATIONINSIGHTS_CONNECTION_STRING string = applicationInsights.outputs.connectionString
```


This example uses the [AVM for function apps](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/web/serverfarm). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L173).

Note

If you choose to optionally define your Consumption plan, you must set the `serverFarmId`

property on the app so that it points to the resource ID of the plan. Make sure that the function app has a `dependsOn`

setting that also references the plan. If you didn't explicitly define a plan, one gets created for you.

Set the `serverFarmId`

property on the app so that it points to the resource ID of the plan. Make sure that the function app has a `dependsOn`

setting that also references the plan.

```
resource functionAppName_resource 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp'
properties: {
serverFarmId: hostingPlanName.id
siteConfig: {
appSettings: [
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};EndpointSuffix=${environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'WEBSITE_CONTENTAZUREFILECONNECTIONSTRING'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};EndpointSuffix=${environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'WEBSITE_CONTENTSHARE'
value: toLower(functionAppName)
}
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'FUNCTIONS_WORKER_RUNTIME'
value: 'node'
}
{
name: 'WEBSITE_NODE_DEFAULT_VERSION'
value: '~14'
}
]
}
}
}
```


For a complete end-to-end example, see this [main.bicep file](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/main.bicep).

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp'
properties: {
serverFarmId: hostingPlan.id
siteConfig: {
alwaysOn: true
appSettings: [
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};EndpointSuffix=${environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'FUNCTIONS_WORKER_RUNTIME'
value: 'node'
}
{
name: 'WEBSITE_NODE_DEFAULT_VERSION'
value: '~14'
}
]
}
}
}
```


For a complete end-to-end example, see this [main.bicep file](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/main.bicep).

## Deployment sources

You can use the [ linuxFxVersion](functions-app-settings#linuxfxversion) site setting to request that a specific Linux container be deployed to your app when it's created. More settings are required to access images in a private repository. For more information, see

[Application configuration](#application-configuration).

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

Your Bicep file or ARM template can optionally also define a deployment for your function code, which could include these methods:

The Flex Consumption plan maintains your project code in zip-compressed package file in a blob storage container known as the *deployment container*. You can configure both the storage account and container used for deployment. For more information, see [Deployment](flex-consumption-plan#deployment).

You must use * one deploy* to publish your code package to the deployment container. During an ARM template or Bicep deployment, you can do this by

[defining a package source](#deployment-package)that uses the

`/onedeploy`

extension. If you choose to instead directly upload your package to the container, the package doesn't get automatically deployed.### Deployment container

The specific storage account and container used for deployments, the authentication method, and credentials are set in the `functionAppConfig.deployment.storage`

element of the `properties`

for the site. The container and any application settings must exist when the app is created. For an example of how to create the storage container, see [Deployment container](#deployment-container).

This example uses a system assigned managed identity to access the specified blob storage container, which is created elsewhere in the deployment:

```
// Consolidated Role Assignments
module rbacAssignments 'rbac.bicep' = {
name: 'rbacAssignments'
scope: rg
params: {
storageAccountName: storage.outputs.name
appInsightsName: applicationInsights.outputs.name
managedIdentityPrincipalId: functionApp.outputs.?systemAssignedMIPrincipalId ?? ''
userIdentityPrincipalId: principalId
allowUserIdentityPrincipal: !empty(principalId)
}
}
// Outputs
output AZURE_LOCATION string = location
output AZURE_TENANT_ID string = tenant().tenantId
output AZURE_FUNCTION_NAME string = functionApp.outputs.name
output APPLICATIONINSIGHTS_CONNECTION_STRING string = applicationInsights.outputs.connectionString
```


This example uses the [AVM for function apps](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/web/site). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L185).

When using managed identities, you must also enable the function app to access the storage account using the identity, as shown in this example:

```
module storageRoleAssignment_User 'br/public:avm/ptn/authorization/resource-role-assignment:0.1.2' = if (allowUserIdentityPrincipal && !empty(userIdentityPrincipalId)) {
name: 'storageRoleAssignment-User-${uniqueString(storageAccount.id, userIdentityPrincipalId)}'
params: {
resourceId: storageAccount.id
roleDefinitionId: roleDefinitions.storageBlobDataOwner
principalId: userIdentityPrincipalId
principalType: 'User'
description: 'Storage Blob Data Owner role for user identity (development/testing)'
roleName: 'Storage Blob Data Owner'
}
}
```


This example uses the [AVM for resource-scoped role assignment](https://github.com/Azure/bicep-registry-modules/tree/main/avm/ptn/authorization/resource-role-assignment). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/rbac.bicep#L45).

This example requires you to know the GUID value for the role being assigned. You can get this ID value for any friendly role name by using the [az role definition list](/en-us/cli/azure/role/definition#az-role-definition-list) command, as in this example:

```
az role definition list --output tsv --query "[?roleName=='Storage Blob Data Owner'].{name:name}"
```


When using a connection string instead of managed identities, you need to instead set the `authentication.type`

to `StorageAccountConnectionString`

and set `authentication.storageAccountConnectionStringName`

to the name of the application setting that contains the deployment storage account connection string.

### Deployment package

The Flex Consumption plan uses *one deploy* for deploying your code project. The code package itself is the same as you would use for zip deployment in other Functions hosting plans. However, the name of the package file itself must be `released-package.zip`

.

To include a one deploy package in your template, use the `/onedeploy`

resource definition for the remote URL that contains the deployment package. The Functions host must be able to access both this remote package source and the deployment container.

This example adds a one deploy source to an existing app:

```
@description('The name of the function app.')
param functionAppName string
@description('The location into which the resources should be deployed.')
param location string = resourceGroup().location
@description('The zip content URL for released-package.zip.')
param packageUri string
resource functionAppName_OneDeploy 'Microsoft.Web/sites/extensions@2022-09-01' = {
name: '${functionAppName}/onedeploy'
location: location
properties: {
packageUri: packageUri
remoteBuild: false
}
}
```


Your Bicep file or ARM template can optionally also define a deployment for your function code using a [zip deployment package](deployment-zip-push).

To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure. In most examples, top-level configurations are applied by using `siteConfig`

. It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine. Top-level information is required before the child `sourcecontrols/web`

resource is applied. Although it's possible to configure these settings in the child-level `config/appSettings`

resource, in some cases your function app must be deployed *before* `config/appSettings`

is applied.

## Zip deployment package

Zip deployment is a recommended way to deploy your function app code. By default, functions that use zip deployment run in the deployment package itself. For more information, including the requirements for a deployment package, see [Zip deployment for Azure Functions](deployment-zip-push). When using resource deployment automation, you can reference the .zip deployment package in your Bicep or ARM template.

To use zip deployment in your template, set the `WEBSITE_RUN_FROM_PACKAGE`

setting in the app to `1`

and include the `/zipDeploy`

resource definition.

For a Consumption plan on Linux, instead set the URI of the deployment package directly in the `WEBSITE_RUN_FROM_PACKAGE`

setting, as shown in [this example template](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-linux-consumption#L152).

This example adds a zip deployment source to an existing app:

```
@description('The name of the function app.')
param functionAppName string
@description('The location into which the resources should be deployed.')
param location string = resourceGroup().location
@description('The zip content url.')
param packageUri string
resource functionAppName_ZipDeploy 'Microsoft.Web/sites/extensions@2021-02-01' = {
name: '${functionAppName}/ZipDeploy'
location: location
properties: {
packageUri: packageUri
}
}
```


Keep the following things in mind when including zip deployment resources in your template:

- Consumption plans on Linux don't support
`WEBSITE_RUN_FROM_PACKAGE = 1`

. You must instead set the URI of the deployment package directly in the`WEBSITE_RUN_FROM_PACKAGE`

setting. For more information, see[WEBSITE_RUN_FROM_PACKAGE](functions-app-settings#website_run_from_package). For an example template, see[Function app hosted on Linux in a Consumption plan](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-linux-consumption).

The

`packageUri`

must be a location that can be accessed by Functions. Consider using Azure blob storage with a shared access signature (SAS). After the SAS expires, Functions can no longer access the share for deployments. When you regenerate your SAS, remember to update the`WEBSITE_RUN_FROM_PACKAGE`

setting with the new URI value.When setting

`WEBSITE_RUN_FROM_PACKAGE`

to a URI, you must[manually sync triggers](functions-deployment-technologies#trigger-syncing).Make sure to always set all required application settings in the

`appSettings`

collection when adding or updating settings. Existing settings not explicitly set are removed by the update. For more information, see[Application configuration](#application-configuration).Functions doesn't support Web Deploy (

`msdeploy`

) for package deployments. You must instead use zip deployment in your deployment pipelines and automation. For more information, see[Zip deployment for Azure Functions](deployment-zip-push).

## Remote builds

The deployment process assumes that the .zip file that you use or a zip deployment contains a ready-to-run app. This means that by default no customizations are run.

There are scenarios that require you to rebuild your app remotely. One such example is when you need to include Linux-specific packages in Python or Node.js apps that you developed on a Windows computer. In this case, you can configure Functions to perform a remote build on your code after the zip deployment.

The way that you request a remote build depends on the operating system to which you're deploying:

When an app is deployed to Windows, language-specific commands (like `dotnet restore`

for C# apps or `npm install`

for Node.js apps) are run.

To enable the same build processes that you get with continuous integration, add `SCM_DO_BUILD_DURING_DEPLOYMENT=true`

to your application settings in your deployment code and remove the `WEBSITE_RUN_FROM_PACKAGE`

entirely.

## Linux containers

If you're deploying a [containerized function app](functions-how-to-custom-container) to an Azure Functions Premium or Dedicated plan, you must:

- Set the
site setting with the identifier of your container image.`linuxFxVersion`

- Set any required
settings when obtaining the container from a private registry.`DOCKER_REGISTRY_SERVER_*`

- Set
application setting to`WEBSITES_ENABLE_APP_SERVICE_STORAGE`

`false`

.

If some settings are missing, the application provisioning might fail with this HTTP/500 error:


`Function app provisioning failed.`


For more information, see [Application configuration](#application-configuration).

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp'
properties: {
serverFarmId: hostingPlan.id
siteConfig: {
appSettings: [
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'FUNCTIONS_WORKER_RUNTIME'
value: 'node'
}
{
name: 'WEBSITE_NODE_DEFAULT_VERSION'
value: '~14'
}
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'DOCKER_REGISTRY_SERVER_URL'
value: dockerRegistryUrl
}
{
name: 'DOCKER_REGISTRY_SERVER_USERNAME'
value: dockerRegistryUsername
}
{
name: 'DOCKER_REGISTRY_SERVER_PASSWORD'
value: dockerRegistryPassword
}
{
name: 'WEBSITES_ENABLE_APP_SERVICE_STORAGE'
value: 'false'
}
]
linuxFxVersion: 'DOCKER|myacr.azurecr.io/myimage:mytag'
}
}
dependsOn: [
storageAccount
]
}
```


When deploying [containerized functions to Azure Container Apps](../container-apps/functions-overview), your template must:

- Set the
`kind`

field to a value of`functionapp,linux,container,azurecontainerapps`

. - Set the
`managedEnvironmentId`

site property to the fully qualified URI of the Container Apps environment. - Add a resource link in the site's
`dependsOn`

collection when creating a`Microsoft.App/managedEnvironments`

resource at the same time as the site.

The definition of a containerized function app deployed from a private container registry to an existing Container Apps environment might look like this example:

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
kind: 'functionapp,linux,container,azurecontainerapps'
location: location
properties: {
serverFarmId: hostingPlanName
siteConfig: {
linuxFxVersion: 'DOCKER|myacr.azurecr.io/myimage:mytag'
appSettings: [
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
]
}
managedEnvironmentId: managedEnvironmentId
}
dependsOn: [
storageAccount
hostingPlan
]
}
```


When deploying functions to Azure Arc, the value you set for the `kind`

field of the function app resource depends on the type of deployment:

| Deployment type | `kind` field value |
|---|---|
| Code-only deployment | `functionapp,linux,kubernetes` |
| Container deployment | `functionapp,linux,kubernetes,container` |

You must also set the `customLocationId`

as you did for the [hosting plan resource](#create-the-hosting-plan).

The definition of a containerized function app, using a .NET 6 quickstart image, might look like this example:

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
kind: 'kubernetes,functionapp,linux,container'
location: location
extendedLocation: {
name: customLocationId
}
properties: {
serverFarmId: hostingPlanName
siteConfig: {
linuxFxVersion: 'DOCKER|mcr.microsoft.com/azure-functions/4-dotnet-isolated6.0-appservice-quickstart'
appSettings: [
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
]
alwaysOn: true
}
}
dependsOn: [
storageAccount
hostingPlan
]
}
```


## Application configuration

In a Flex Consumption plan, you configure your function app in Azure with two types of properties:

| Configuration | `Microsoft.Web/sites` property |
|---|---|
| Application configuration | `functionAppConfig` |
| Application settings | `siteConfig.appSettings` collection |

These application configurations are maintained in `functionAppConfig`

:

| Behavior | Setting in `functionAppConfig` |
|---|---|
|

`scaleAndConcurrency.alwaysReady`

[Deployment source](#deployment-sources)`deployment`

[Instance size](flex-consumption-plan#instance-sizes)`scaleAndConcurrency.instanceMemoryMB`

[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency)`scaleAndConcurrency.triggers.http.perInstanceConcurrency`

[Language runtime](functions-app-settings#functions_worker_runtime)`runtime.name`

[Language version](supported-languages)`runtime.version`

[Maximum instance count](event-driven-scaling#flex-consumption-plan)`scaleAndConcurrency.maximumInstanceCount`

[Site update strategy](flex-consumption-site-updates)`siteUpdateStrategy.type`

The Flex Consumption plan also supports these application settings:

- Connection string-based settings:
- Managed identity-based settings:

Functions provides the following options for configuring your function app in Azure:

| Configuration | `Microsoft.Web/sites` property |
|---|---|
| Site settings | `siteConfig` |
| Application settings | `siteConfig.appSettings` collection |

These site settings are required on the `siteConfig`

property:

These site settings are required only when using managed identities to obtain the image from an Azure Container Registry instance:

These application settings are required (or recommended) for a specific operating system and hosting option:

These application settings are required for container deployments:

These settings are only required when deploying from a private container registry:

Keep these considerations in mind when working with site and application settings using Bicep files or ARM templates:

- The optional
`alwaysReady`

setting contains an array of one or more`{name,instanceCount}`

objects, with one for each[per-function scale group](flex-consumption-plan#per-function-scaling). These are the scale groups being used to make always-ready scale decisions. This example sets always-ready counts for both the`http`

group and a single function named`helloworld`

, which is of a nongrouped trigger type:`alwaysReady: [ { name: 'http' instanceCount: 2 } { name: 'function:helloworld' instanceCount: 1 } ]`


- There are important considerations for when you should set
`WEBSITE_CONTENTSHARE`

in an automated deployment. For detailed guidance, see thereference.`WEBSITE_CONTENTSHARE`


- For container deployments, also set
to`WEBSITES_ENABLE_APP_SERVICE_STORAGE`

`false`

, since your app content is provided in the container itself.

You should always define your application settings as a

`siteConfig/appSettings`

collection of the`Microsoft.Web/sites`

resource being created, as is done in the examples in this article. This definition guarantees the settings your function app needs to run are available on initial startup.When adding or updating application settings using templates, make sure that you include all existing settings with the update. You must do this because the underlying update REST API calls replace the entire

`/config/appsettings`

resource. If you remove the existing settings, your function app won't run. To programmatically update individual application settings, you can instead use the Azure CLI, Azure PowerShell, or the Azure portal to make these changes. For more information, see[Work with application settings](functions-how-to-use-azure-function-app-settings#settings).When possible, you should use managed identity-based connections to other Azure services, including the

`AzureWebJobsStorage`

connection. For more information, see[Configure an identity-based connection](functions-reference#configure-an-identity-based-connection).

## Slot deployments

Functions lets you deploy different versions of your code to unique endpoints in your function app. This option makes it easier to develop, validate, and deploy functions updates without impacting functions running in production. Deployment slots is a feature of Azure App Service. The number of slots available [depends on your hosting plan](functions-scale#service-limits). For more information, see [Azure Functions deployment slots](functions-deployment-slots) functions.

A slot resource is defined in the same way as a function app resource (`Microsoft.Web/sites`

), but instead you use the `Microsoft.Web/sites/slots`

resource identifier. For an example deployment (in both Bicep and ARM templates) that creates both a production and a staging slot in a Premium plan, see [Azure Function App with a Deployment Slot](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-deployment-slot).

To learn about how to swap slots by using templates, see [Automate with Resource Manager templates](../app-service/deploy-staging-slots#automate-with-resource-manager-templates).

Keep the following considerations in mind when working with slot deployments:

Don't explicitly set the

`WEBSITE_CONTENTSHARE`

setting in the deployment slot definition. This setting is generated for you when the app is created in the deployment slot.When you swap slots, some application settings are considered "sticky," in that they stay with the slot and not with the code being swapped. You can define such a

*slot setting*by including`"slotSetting":true`

in the specific application setting definition in your template. For more information, see[Manage settings](functions-deployment-slots#manage-settings).

## Secured deployments

You can create your function app in a deployment where one or more of the resources have been secured by integrating with virtual networks. Virtual network integration for your function app is defined by a `Microsoft.Web/sites/networkConfig`

resource. This integration depends on both the referenced function app and virtual network resources. Your function app might also depend on other private networking resources, such as private endpoints and routes. For more information, see [Azure Functions networking options](functions-networking-options).

These projects provide Bicep-based examples of how to deploy your function apps in a virtual network, including with network access restrictions:

[High-scale HTTP triggered function connects to an event hub secured by a virtual network](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md): An HTTP triggered function (.NET isolated worker mode) accepts calls from any source and then sends the body of those HTTP calls to a secure event hub running in a virtual network by using virtual network integration.[Function is triggered by a Service Bus queue secured in a virtual network](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md): A Python function is triggered by a Service Bus queue secured in a virtual network. The queue is accessed in the virtual network using private endpoint. A virtual machine in the virtual network is used to send messages.

When creating a deployment that uses a secured storage account, you must both explicitly set the `WEBSITE_CONTENTSHARE`

setting and create the file share resource named in this setting. Make sure you create a `Microsoft.Storage/storageAccounts/fileServices/shares`

resource using the value of `WEBSITE_CONTENTSHARE`

, as shown in this example ([ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-private-endpoints-storage-private-endpoints/azuredeploy.json#L467)|[Bicep file](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-private-endpoints-storage-private-endpoints/main.bicep#L351)). You'll also need to set the site property `vnetContentShareEnabled`

to true.

Note

When these settings aren't part of a deployment that uses a secured storage account, you see this error during deployment validation: `Could not access storage account using provided connection string`

.

These projects provide both Bicep and ARM template examples of how to deploy your function apps in a virtual network, including with network access restrictions:

| Restricted scenario | Description |
|---|---|
|

[Virtual network integration](functions-networking-options#virtual-network-integration).[Create a function app that accesses a secured storage account](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-storage-private-endpoints)[Restrict your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network).[Create a function app and storage account that both use private endpoints](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-private-endpoints-storage-private-endpoints)[Private endpoints](functions-networking-options#private-endpoints).### Restricted network settings

You might also need to use these settings when your function app has network restrictions:

| Setting | Value | Description |
|---|---|---|
`WEBSITE_CONTENTOVERVNET` |

`1`

[Restrict your storage account to a virtual network](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).`vnetrouteallenabled`

`1`

[Regional virtual network integration](functions-networking-options#regional-virtual-network-integration). This site setting supersedes the application setting[.](functions-app-settings#website_vnet_route_all)`WEBSITE_VNET_ROUTE_ALL`

### Considerations for network restrictions

When you're restricting access to the storage account through the private endpoints, you aren't able to access the storage account through the portal or any device outside the virtual network. You can give access to your secured IP address or virtual network in the storage account by [Managing the default network access rule](../storage/common/storage-network-security-set-default-access).

## Function access keys

Host-level [function access keys](function-keys-how-to) are defined as Azure resources. This means that you can create and manage host keys in your ARM templates and Bicep files. A host key is defined as a resource of type `Microsoft.Web/sites/host/functionKeys`

. This example creates a host-level access key named `my_custom_key`

when the function app is created:

```
resource functionKey 'Microsoft.Web/sites/host/functionKeys@2022-09-01' = {
name: '${parameters('name')}/default/my_custom_key'
properties: {
name: 'my_custom_key'
}
dependsOn: [
resourceId('Microsoft.Web/Sites', parameters('name'))
]
}
```


In this example, the `name`

parameter is the name of the new function app. You must include a `dependsOn`

setting to guarantee that the key is created with the new function app. Finally, the `properties`

object of the host key can also include a `value`

property that can be used to set a specific key.

When you don't set the `value`

property, Functions automatically generates a new key for you when the resource is created, which is recommended. To learn more about access keys, including security best practices for working with access keys, see [Work with access keys in Azure Functions](function-keys-how-to).

## Create your template

Experts with Bicep or ARM templates can manually code their deployments using a simple text editor. For the rest of us, there are several ways to make the development process easier:

**Visual Studio Code**: There are extensions available to help you work with both[Bicep files](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-bicep)and[ARM templates](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools). You can use these tools to help make sure that your code is correct, and they provide some[basic validation](functions-infrastructure-as-code?tabs=vs-code#validate-your-template).**Azure portal**: When you[create your function app and related resources in the portal](functions-create-function-app-portal), the final**Review + create**screen has a**Download a template for automation**link.This link shows you the ARM template generated based on the options you chose in portal. This template can seem a bit complex when you're creating a function app with many new resources. However, it can provide a good reference for how your ARM template might look.


## Validate your template

When you manually create your deployment template file, it's important to validate your template before deployment. All deployment methods validate your template syntax and raise a `validation failed`

error message as shown in the following JSON formatted example:

```
{"error":{"code":"InvalidTemplate","message":"Deployment template validation failed: 'The resource 'Microsoft.Web/sites/func-xyz' is not defined in the template. Please see https://aka.ms/arm-template for usage details.'.","additionalInfo":[{"type":"TemplateViolation","info":{"lineNumber":0,"linePosition":0,"path":""}}]}}
```


The following methods can be used to validate your template before deployment:

The following [Azure resource group deployment v2 task](/en-us/azure/devops/pipelines/tasks/deploy/azure-resource-group-deployment?view=azure-devops&preserve-view=true) with `deploymentMode: 'Validation'`

instructs Azure Pipelines to validate the template.

```
- task: AzureResourceManagerTemplateDeployment@3
inputs:
deploymentScope: 'Resource Group'
subscriptionId: # Required subscription ID
action: 'Create Or Update Resource Group'
resourceGroupName: # Required resource group name
location: # Required when action == Create Or Update Resource Group
templateLocation: 'Linked artifact'
csmFile: # Required when TemplateLocation == Linked Artifact
csmParametersFile: # Optional
deploymentMode: 'Validation'
```


You can also create a test resource group to find [preflight](../azure-resource-manager/troubleshooting/quickstart-troubleshoot-arm-deployment?tabs=azure-cli#fix-preflight-error) and [deployment](../azure-resource-manager/troubleshooting/quickstart-troubleshoot-arm-deployment?tabs=azure-cli#fix-deployment-error) errors.

## Deploy your template

You can use any of the following ways to deploy your Bicep file and template:

### Deploy to Azure button

Note

This method doesn't support deploying Bicep files currently.

Replace `<url-encoded-path-to-azuredeploy-json>`

with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json`

file in GitHub.

Here's an example that uses markdown:

```
[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```


Here's an example that uses HTML:

```
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="https://azuredeploy.net/deploybutton.png"></a>
```


### Deploy using PowerShell

The following PowerShell commands create a resource group and deploy a Bicep file or ARM template that creates a function app with its required resources. To run locally, you must have [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) installed. To sign in to Azure, you must first run [ Connect-AzAccount](/en-us/powershell/module/az.accounts/connect-azaccount).

```
# Register Resource Providers if they're not already registered
Register-AzResourceProvider -ProviderNamespace "microsoft.web"
Register-AzResourceProvider -ProviderNamespace "microsoft.storage"
# Create a resource group for the function app
New-AzResourceGroup -Name "MyResourceGroup" -Location 'West Europe'
# Deploy the template
New-AzResourceGroupDeployment -ResourceGroupName "MyResourceGroup" -TemplateFile main.bicep -Verbose
```


To test out this deployment, you can use a [template like this one](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/function-app-create-dynamic) that creates a function app on Windows in a Consumption plan.

## Next steps

Learn more about how to develop and configure Azure Functions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-github-actions -->

# Continuous delivery by using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use a [GitHub Actions workflow](https://docs.github.com/actions/learn-github-actions/introduction-to-github-actions#the-components-of-github-actions) to define a workflow to automatically build and deploy code to your function app in Azure Functions.

A YAML file (.yml) that defines the workflow configuration is maintained in the `/.github/workflows/`

path in your repository. This definition contains the actions and parameters that make up the workflow, which is specific to the development language of your functions. A GitHub Actions workflow for Functions performs the following tasks, regardless of language:

- Set up the environment.
- Build the code project.
- Deploy the package to a function app in Azure.

The Azure Functions action handles the deployment to an existing function app in Azure.

You can create a workflow configuration file for your deployment manually. You can also generate the file from a set of language-specific templates in one of these ways:

- In the Azure portal
- Using the Azure CLI
- From your GitHub repository

If you don't want to create your YAML file by hand, select a different method at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).A GitHub account. If you don't have one, sign up for

[free](https://github.com/join).A working function app hosted on Azure with source code in a GitHub repository.


[Azure CLI](/en-us/cli/azure/install-azure-cli), when developing locally. You can also use the Azure CLI in Azure Cloud Shell.

## Generate deployment credentials

Since GitHub Actions uses your publish profile to access your function app during deployment, you first need to get your publish profile and store it securely as a [GitHub secret](https://docs.github.com/en/actions/reference/encrypted-secrets).

Important

The publish profile is a valuable credential that allows access to Azure resources. Make sure you always transport and store it securely. In GitHub, the publish profile must only be stored in GitHub secrets.

### Download your publish profile

To download the publishing profile of your function app:

In the

[Azure portal](https://portal.azure.com), locate the page for your function app, expand**Settings**>**Configuration**in the left column.In the

**Configuration**page, select the**General settings**tab and make sure that**SCM Basic Auth Publishing Credentials**is turned**On**. When this setting is**Off**, you can't use publish profiles, so select**On**and then**Save**.Go back to the function app's

**Overview**page, and then select**Get publish profile**.Save and copy the contents of the file.


### Add the GitHub secret

In

[GitHub](https://github.com/), go to your repository.Go to

**Settings**.Select

**Secrets and variables > Actions**.Select

**New repository secret**.Add a new secret with the name

`AZURE_FUNCTIONAPP_PUBLISH_PROFILE`

and the value set to the contents of the publishing profile file.Select

**Add secret**.

GitHub can now authenticate to your function app in Azure.

## Create the workflow from a template

The best way to manually create a workflow configuration is to start from the officially supported template.

Choose either

**Windows**or**Linux**to make sure that you get the template for the correct operating system.Copy the language-specific template from the Azure Functions actions repository using the following link:

Update the

`env.AZURE_FUNCTIONAPP_NAME`

parameter with the name of your function app resource in Azure. You may optionally need to update the parameter that sets the language version used by your app, such as`DOTNET_VERSION`

for C#.Add this new YAML file in the

`/.github/workflows/`

path in your repository.

## Create the workflow configuration in the portal

When you use the portal to enable GitHub Actions, Functions creates a workflow file based on your application stack and commits it to your GitHub repository in the correct directory.

The portal automatically gets your publish profile and adds it to the GitHub secrets for your repository.

### During function app create

You can get started quickly with GitHub Actions through the Deployment tab when you create a function in Azure portal. To add a GitHub Actions workflow when you create a new function app:

In the

[Azure portal](https://portal.azure.com), select**Deployment**in the**Create Function App**flow.Enable

**Continuous Deployment**if you want each code update to trigger a code push to Azure portal.Enter your GitHub organization, repository, and branch.

Complete configuring your function app. Your GitHub repository now includes a new workflow file in

`/.github/workflows/`

.

### For an existing function app

To add a GitHub Actions workflow to an existing function app:

Navigate to your function app in the

[Azure portal](https://portal.azure.com)and select**Deployment Center**.For

**Source**select**GitHub**. If you don't see the default message*Building with GitHub Actions*, select**Change provider**choose**GitHub Actions**and select**OK**.If you haven't already authorized GitHub access, select

**Authorize**. Provide your GitHub credentials and select**Sign in**. To authorize a different GitHub account, select**Change Account**and sign in with another account.Select your GitHub

**Organization**,**Repository**, and**Branch**. To deploy with GitHub Actions, you must have write access to this repository.In

**Authentication settings**, choose whether to have GitHub Actions authenticate with a**User-assigned identity**or using**Basic authentication**credentials. For basic authentication, the current credentials are used.Select

**Preview file**to see the workflow file that gets added to your GitHub repository in`github/workflows/`

.Select

**Save**to add the workflow file to your repository.

## Add workflow configuration to your repository

You can use the [ az functionapp deployment github-actions add](/en-us/cli/azure/functionapp/deployment/github-actions) command to generate a workflow configuration file from the correct template for your function app. The new YAML file is then stored in the correct location (

`/.github/workflows/`

) in the GitHub repository you provide, while the publish profile file for your app is added to GitHub secrets in the same repository.Run this

`az functionapp`

command, replacing the values`githubUser/githubRepo`

,`MyResourceGroup`

, and`MyFunctionapp`

:`az functionapp deployment github-actions add --repo "githubUser/githubRepo" -g MyResourceGroup -n MyFunctionapp --login-with-github`

This command uses an interactive method to retrieve a personal access token for your GitHub account.

In your terminal window, you should see something like the following message:

`Please navigate to https://github.com/login/device and enter the user code XXXX-XXXX to activate and retrieve your GitHub personal access token.`

Copy the unique

`XXXX-XXXX`

code, browse to[https://github.com/login/device](https://github.com/login/device), and enter the code you copied. After entering your code, you should see something like the following message:`Verified GitHub repo and branch Getting workflow template using runtime: java Filling workflow template with name: func-app-123, branch: main, version: 8, slot: production, build_path: . Adding publish profile to GitHub Fetching publish profile with secrets for the app 'func-app-123' Creating new workflow file: .github/workflows/master_func-app-123.yml`

Go to your GitHub repository and select

**Actions**. Verify that your workflow ran.

## Create the workflow configuration file

You can create the GitHub Actions workflow configuration file from the Azure Functions templates directly from your GitHub repository.

In

[GitHub](https://github.com/), go to your repository.Select

**Actions**and**New workflow**.Search for

*functions*.In the displayed functions app workflows authored by Microsoft Azure, find the one that matches your code language and select

**Configure**.In the newly created YAML file, update the

`env.AZURE_FUNCTIONAPP_NAME`

parameter with the name of your function app resource in Azure. You may optionally need to update the parameter that sets the language version used by your app, such as`DOTNET_VERSION`

for C#.Verify that the new workflow file is being saved in

`/.github/workflows/`

and select**Commit changes...**.

## Update a workflow configuration

If for some reason, you need to update or change an existing workflow configuration, just navigate to the `/.github/workflows/`

location in your repository, open the specific YAML file, make any needed changes, and then commit the updates to the repository.

## Example: workflow configuration file

The following template example uses version 1 of the `functions-action`

and a `publish profile`

for authentication. The template depends on your chosen language and the operating system on which your function app is deployed:

```
name: Deploy DotNet project to Azure Function App
on:
[push]
env:
AZURE_FUNCTIONAPP_NAME: 'your-app-name' # set this to your function app name on Azure
AZURE_FUNCTIONAPP_PACKAGE_PATH: '.' # set this to the path to your function app project, defaults to the repository root
DOTNET_VERSION: '6.0.x' # set this to the dotnet version to use (e.g. '2.1.x', '3.1.x', '5.0.x')
jobs:
build-and-deploy:
runs-on: windows-latest
environment: dev
steps:
- name: 'Checkout GitHub Action'
uses: actions/checkout@v3
- name: Setup DotNet ${{ env.DOTNET_VERSION }} Environment
uses: actions/setup-dotnet@v3
with:
dotnet-version: ${{ env.DOTNET_VERSION }}
- name: 'Resolve Project Dependencies Using Dotnet'
shell: pwsh
run: |
pushd './${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }}'
dotnet build --configuration Release --output ./output
popd
- name: 'Run Azure Functions Action'
uses: Azure/functions-action@v1
id: fa
with:
app-name: ${{ env.AZURE_FUNCTIONAPP_NAME }}
package: '${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }}/output'
publish-profile: ${{ secrets.AZURE_FUNCTIONAPP_PUBLISH_PROFILE }}
```


## Azure Functions action

The Azure Functions action (`Azure/functions-action`

) defines how your code is published to an existing function app in Azure, or to a specific slot in your app.

### Parameters

The following parameters are required for all function app plans:

| Parameter | Explanation |
|---|---|
app-name |
The name of your function app. |
package |
This is the location in your project to be published. By default, this value is set to `.` , which means all files and folders in the GitHub repository will be deployed. |

The following parameters are required for the Flex Consumption plan:

| Parameter | Explanation |
|---|---|
sku |
Set this to `flexconsumption` when authenticating with publish-profile. When using RBAC credentials or deploying to a non-Flex Consumption plan, the Action can resolve the value, so the parameter does not need to be included. |
remote-build |
Set this to `true` to enable a build action from Kudu when the package is deployed to a Flex Consumption app. Oryx build is always performed during a remote build in Flex Consumption; do not set scm-do-build-during-deployment or enable-oryx-build. By default, this parameter is set to `false` . |

The following parameters are specific to the Consumption, Elastic Premium, and App Service (Dedicated) plans:

| Parameter | Explanation |
|---|---|
scm-do-build-during-deployment |
(Optional) Allow the Kudu site (e.g. `https://<APP_NAME>.scm.azurewebsites.net/` ) to perform pre-deployment operations, such as
`false` . Set this to `true` when you do want to control deployment behaviors using Kudu instead of resolving dependencies in your GitHub workflow. For more information, see the
`SCM_DO_BUILD_DURING_DEPLOYMENT` |
enable-oryx-build |
(Optional) Allow Kudu site to resolve your project dependencies with Oryx. By default, this is set to `false` . If you want to use
scm-do-build-during-deployment and enable-oryx-build to `true` . |

Optional parameters for all function app plans:

| Parameter | Explanation |
|---|---|
slot-name |
This is the
publish-profile parameter contains the credentials for the slot instead of the production site. Currently not supported in Flex Consumption. |

**publish-profile****respect-pom-xml**`true`

and set `package`

to `.`

. By default, this parameter is set to `false`

, which means that the `package`

parameter must point to your app's artifact location, such as `./target/azure-functions/`

**respect-funcignore**`true`

when your repository has a .funcignore file and you want to use it exclude paths and files, such as text editor configurations, .vscode/, or a Python virtual environment (.venv/). The default setting is `false`

.### Considerations

Keep the following considerations in mind when using the Azure Functions action:

When using GitHub Actions, the way that your code is deployed depends on your hosting plan, as shown in this table:

Hosting plan Deployment method [Flex Consumption](flex-consumption-plan)[One deploy](functions-deployment-technologies#one-deploy)[Elastic Premium](functions-premium-plan)[Zip deploy](deployment-zip-push)to apps on the[Consumption](consumption-plan)[Dedicated (App Service)](dedicated-plan)[Zip deploy](deployment-zip-push)to apps on the[Consumption](consumption-plan)[Consumption](consumption-plan)Windows: [Zip deploy](deployment-zip-push)

Linux:[external package URL](functions-deployment-technologies#external-package-url)** The ability to run your apps on Linux in a Consumption plan is planned for retirement. For more information, see

[Azure Functions Consumption plan hosting](consumption-plan).The credentials required by GitHub to connection to Azure for deployment are stored as Secrets in your GitHub repository and accessed in the deployment as

`secrets.<SECRET_NAME>`

.The easiest way for GitHub Actions to authenticate with Azure Functions for deployment is by using a publish profile. You can also authenticate using a service principal. To learn more, see

[this GitHub Actions repository](https://github.com/Azure/functions-action).The actions for setting up the environment and running a build are generated from the templates, and are language specific.

The templates use

`env`

elements to define settings unique to your build and deployment.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-azure-devops -->

# Continuous delivery with Azure Pipelines

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use [Azure Pipelines](/en-us/azure/devops/pipelines/) to automatically deploy your code project to a function app in Azure. Azure Pipelines lets you build, test, and deploy with continuous integration (CI) and continuous delivery (CD) using [Azure DevOps](/en-us/azure/devops/).

YAML pipelines are defined using a YAML file in your repository. A step is the smallest building block of a pipeline and can be a script or task (prepackaged script). [Learn about the key concepts and components that make up a pipeline](/en-us/azure/devops/pipelines/get-started/key-pipelines-concepts).

You use the `AzureFunctionApp`

task to deploy your code. There are now two versions of `AzureFunctionApp`

, which are compared in this table:

| Comparison/version |
|
|---|

[AzureFunctionApp@1](/en-us/azure/devops/pipelines/tasks/reference/azure-function-app-v1)

[Flex Consumption plan](flex-consumption-plan)** Enhanced validation support makes pipelines less likely to fail because of errors.

Choose your task version at the top of the article.

Note

Upgrade from `AzureFunctionApp@1`

to `AzureFunctionApp@2`

for access to new features and long-term support.

## Prerequisites

An Azure DevOps organization. If you don't have one, you can

[create one for free](/en-us/azure/devops/pipelines/get-started/pipelines-sign-up). If your team already has one, then make sure you're an administrator of the Azure DevOps project that you want to use.An ability to run pipelines on Microsoft-hosted agents. You can either purchase a

[parallel job](/en-us/azure/devops/pipelines/licensing/concurrent-jobs)or you can request a free tier.If you plan to use GitHub instead of Azure Repos, you also need a GitHub repository. If you don't have a GitHub account, you can

[create one for free](https://github.com).An existing function app in Azure that has its source code in a supported repository. If you don't yet have an Azure Functions code project, you can create one by completing the following language-specific article:


Remember to upload the local code project to your GitHub or Azure Repos repository after you publish it to your function app.

## Build your app

- Sign in to your Azure DevOps organization and navigate to your project.
- In your project, navigate to the
**Pipelines**page. Then choose the action to create a new pipeline. - Walk through the steps of the wizard by first selecting
**GitHub**as the location of your source code. - You might be redirected to GitHub to sign in. If so, enter your GitHub credentials.
- When the list of repositories appears, select your sample app repository.
- Azure Pipelines will analyze your repository and recommend a template. Select
**Save and run**, then select**Commit directly to the main branch**, and then choose**Save and run**again. - A new run is started. Wait for the run to finish.

### Example YAML build pipelines

The following language-specific pipelines can be used for building apps.

You can use the following sample to create a YAML file to build a .NET app:

```
pool:
vmImage: 'windows-latest'
steps:
- task: UseDotNet@2
displayName: 'Install .NET 8.0 SDK'
inputs:
packageType: 'sdk'
version: '8.0.x'
installationPath: $(Agent.ToolsDirectory)/dotnet
- script: |
dotnet restore
dotnet build --configuration Release
- task: DotNetCoreCLI@2
displayName: 'dotnet publish'
inputs:
command: publish
arguments: '--configuration Release --output $(System.DefaultWorkingDirectory)/publish_output'
projects: 'csharp/*.csproj'
publishWebProjects: false
modifyOutputPath: false
zipAfterPublish: false
- task: ArchiveFiles@2
displayName: "Archive files"
inputs:
rootFolderOrFile: "$(System.DefaultWorkingDirectory)/publish_output"
includeRootFolder: false
archiveFile: "$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip"
- task: PublishBuildArtifacts@1
inputs:
PathtoPublish: '$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip'
artifactName: 'drop'
```


- Sign in to your Azure DevOps organization and navigate to your project.
- In your project, navigate to the
**Pipelines**page. Then select**New pipeline**. - Select one of these options for
**Where is your code?**:**GitHub**: You might be redirected to GitHub to sign in. If so, enter your GitHub credentials. When this connection is your first GitHub connection, the wizard also walks you through the process of connecting DevOps to your GitHub accounts.**Azure Repos Git**: You're immediately able to choose a repository in your current DevOps project.

- When the list of repositories appears, select your sample app repository.
- Azure Pipelines analyzes your repository and in
**Configure your pipeline**provides a list of potential templates. Choose the appropriate**function app**template for your language. If you don't see the correct template select**Show more**. - Select
**Save and run**, then select**Commit directly to the main branch**, and then choose**Save and run**again. - A new run is started. Wait for the run to finish.

### Example YAML build pipelines

The following language-specific pipelines can be used for building apps.

You can use the following sample to create a YAML file to build a .NET app.

If you see errors when building your app, verify that the version of .NET that you use matches your Azure Functions version. For more information, see [Azure Functions runtime versions overview](functions-versions).

```
pool:
vmImage: 'windows-latest'
steps:
- task: UseDotNet@2
displayName: 'Install .NET 8.0 SDK'
inputs:
packageType: 'sdk'
version: '8.0.x'
installationPath: $(Agent.ToolsDirectory)/dotnet
- script: |
dotnet restore
dotnet build --configuration Release
- task: DotNetCoreCLI@2
displayName: 'dotnet publish'
inputs:
command: publish
arguments: '--configuration Release --output $(System.DefaultWorkingDirectory)/publish_output'
projects: 'csharp/*.csproj'
publishWebProjects: false
modifyOutputPath: false
zipAfterPublish: false
- task: ArchiveFiles@2
displayName: "Archive files"
inputs:
rootFolderOrFile: "$(System.DefaultWorkingDirectory)/publish_output"
includeRootFolder: false
archiveFile: "$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip"
- task: PublishBuildArtifacts@1
inputs:
PathtoPublish: '$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip'
artifactName: 'drop'
```


## Deploy your app

You'll deploy with the [Azure Function App Deploy v2](/en-us/azure/devops/pipelines/tasks/reference/azure-function-app-v2) task. This task requires an [Azure service connection](/en-us/azure/devops/pipelines/library/service-endpoints) as an input. An Azure service connection stores the credentials to connect from Azure Pipelines to Azure. You should create a connection that uses [workload identity federation](/en-us/azure/devops/pipelines/library/connect-to-azure#create-an-azure-resource-manager-service-connection-that-uses-workload-identity-federation).

To deploy to Azure Functions, add this snippet at the end of your `azure-pipelines.yml`

file, depending on whether your app runs on Linux or Windows:

```
trigger:
- main
variables:
# Azure service connection established during pipeline creation
azureSubscription: <Name of your Azure subscription>
appName: <Name of the function app>
# Agent VM image name
vmImageName: 'windows-latest'
- task: AzureFunctionApp@2 # Add this at the end of your file
inputs:
azureSubscription: <Name of your Azure subscription>
appType: functionApp # this specifies a Windows-based function app
appName: $(appName)
package: $(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip
deploymentMethod: 'auto' # 'auto' | 'zipDeploy' | 'runFromPackage'. Required. Deployment method. Default: auto.
#Uncomment the next lines to deploy to a deployment slot
#Note that deployment slots is not supported for Linux Dynamic SKU
#deployToSlotOrASE: true
#resourceGroupName: '<RESOURCE_GROUP>'
#slotName: '<SLOT_NAME>'
```


The default `appType`

is Windows (`functionApp`

). You can specify Linux by setting the `appType`

to `functionAppLinux`

. A [Flex Consumption](/en-us/azure/azure-functions/flex-consumption-plan) app runs on Linux, and you to must set both `appType: functionAppLinux`

and `isFlexConsumption: true`

.

The snippet assumes that the build steps in your YAML file produce the zip archive in the `$(System.ArtifactsDirectory)`

folder on your agent.

You deploy using the [Azure Function App Deploy](/en-us/azure/devops/pipelines/tasks/deploy/azure-function-app) task. This task requires an [Azure service connection](/en-us/azure/devops/pipelines/library/service-endpoints) as an input. An Azure service connection stores the credentials to connect from Azure Pipelines to Azure.

Important

Deploying to a Flex Consumption app isn't supported using @v1 of the `AzureFunctionApp`

task.

To deploy to Azure Functions, add this snippet at the end of your `azure-pipelines.yml`

file:

```
trigger:
- main
variables:
# Azure service connection established during pipeline creation
azureSubscription: <Name of your Azure subscription>
appName: <Name of the function app>
# Agent VM image name
vmImageName: 'ubuntu-latest'
- task: DownloadBuildArtifacts@1 # Add this at the end of your file
inputs:
buildType: 'current'
downloadType: 'single'
artifactName: 'drop'
itemPattern: '**/*.zip'
downloadPath: '$(System.ArtifactsDirectory)'
- task: AzureFunctionApp@1
inputs:
azureSubscription: $(azureSubscription)
appType: functionAppLinux # default is functionApp
appName: $(appName)
package: $(System.ArtifactsDirectory)/**/*.zip
```


This snippet sets the `appType`

to `functionAppLinux`

, which is required when deploying to an app that runs on Linux. The default `appType`

is Windows (`functionApp`

).

The example assumes that the build steps in your YAML file produce the zip archive in the `$(System.ArtifactsDirectory)`

folder on your agent.

## Deploy a container

Tip

We recommend using the Azure Functions support in Azure Container Apps for hosting your function app in a custom Linux container. For more information, see [Azure Functions on Azure Container Apps overview](../container-apps/functions-overview).

When deploying a containerized function app, the deployment task you use depends on the specific hosting environment.

You can use the [Azure Container Apps Deploy](/en-us/azure/devops/pipelines/tasks/reference/azure-container-apps-v1) task (`AzureContainerApps`

) to deploy a function app image to an Azure Container App instance that is optimized for Azure Functions.

This code deploys the base image for a .NET 8 isolated process model function app:

```
trigger:
- main
pool:
vmImage: 'ubuntu-latest'
steps:
- task: AzureContainerApps@1
inputs:
azureSubscription: <Name of your Azure subscription>
imageToDeploy: 'mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0'
containerAppName: <Name of your container app>
resourceGroup: <Name of the resource group>
```


Ideally, you would build your own custom container in the pipeline instead of using a base image, as shown in this example. For more information, see [Deploy to Azure Container Apps from Azure Pipelines](../container-apps/azure-pipelines).

## Deploy to a slot

Important

The Flex Consumption plan doesn't currently support slots.
Linux apps also don't support slots when running in a Consumption plan, and [support for these apps is being retired in the future](consumption-plan).

```
trigger:
- main
variables:
# Azure service connection established during pipeline creation
azureSubscription: <Name of your Azure subscription>
appName: <Name of the function app>
# Agent VM image name
vmImageName: 'windows-latest'
- task: AzureFunctionApp@2 # Add this at the end of your file
inputs:
azureSubscription: <Name of your Azure subscription>
appType: functionApp # this specifies a Windows-based function app
appName: $(appName)
package: $(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip
deploymentMethod: 'auto' # 'auto' | 'zipDeploy' | 'runFromPackage'. Required. Deployment method. Default: auto.
deployToSlotOrASE: true
resourceGroupName: '<RESOURCE_GROUP>'
slotName: '<SLOT_NAME>'
```


You can configure your function app to have multiple slots. Slots allow you to safely deploy your app and test it before making it available to your customers.

The following YAML snippet shows how to deploy to a staging slot, and then swap to a production slot:

```
- task: AzureFunctionApp@1
inputs:
azureSubscription: <Azure service connection>
appType: functionAppLinux
appName: <Name of the function app>
package: $(System.ArtifactsDirectory)/**/*.zip
deployToSlotOrASE: true
resourceGroupName: <Name of the resource group>
slotName: staging
- task: AzureAppServiceManage@0
inputs:
azureSubscription: <Azure service connection>
WebAppName: <name of the function app>
ResourceGroupName: <name of resource group>
SourceSlot: staging
SwapWithProduction: true
```


When using [deployment slots](functions-deployment-slots), you can also add the following task to perform a slot swap as part of your deployment.

```
- task: AzureAppServiceManage@0
inputs:
azureSubscription: <AZURE_SERVICE_CONNECTION>
WebAppName: <APP_NAME>
ResourceGroupName: <RESOURCE_GROUP>
SourceSlot: <SLOT_NAME>
SwapWithProduction: true
```


## Create a pipeline with Azure CLI

To create a build pipeline in Azure, use the `az functionapp devops-pipeline create`

[command](/en-us/cli/azure/functionapp/devops-pipeline#az-functionapp-devops-pipeline-create). The build pipeline is created to build and release any code changes that are made in your repo. The command generates a new YAML file that defines the build and release pipeline and then commits it to your repo. The prerequisites for this command depend on the location of your code.

If your code is in GitHub:

You must have

**write**permissions for your subscription.You must be the project administrator in Azure DevOps.

You must have permissions to create a GitHub personal access token (PAT) that has sufficient permissions. For more information, see

[GitHub PAT permission requirements.](/en-us/azure/devops/pipelines/repos/github#repository-permissions-for-personal-access-token-pat-authentication)You must have permissions to commit to the main branch in your GitHub repository so you can commit the autogenerated YAML file.


If your code is in Azure Repos:

You must have

**write**permissions for your subscription.You must be the project administrator in Azure DevOps.


## Next steps

- Review the
[Azure Functions overview](functions-overview). - Review the
[Azure DevOps overview](/en-us/azure/devops/pipelines/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model -->

# Migrate C# apps from the in-process model to the isolated worker model

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

[Support for the in-process model ends on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you migrate your apps to the isolated worker model by following the instructions in this article.

This article walks you through the process of safely migrating your .NET function app from the [in-process model](functions-dotnet-class-library) to the [isolated worker model](dotnet-isolated-process-guide). To learn about the high-level differences between these models, see the [execution mode comparison](dotnet-isolated-in-process-differences).

This guide assumes that your app is running on version 4.x of the Functions runtime. If not, you should use the following guides to upgrade your host version. These host-version migration guides also help you migrate to the isolated worker model as you work through them.

[Migrate apps from Azure Functions version 2.x and 3.x to version 4.x](migrate-version-3-version-4)[Migrate apps from Azure Functions version 1.x to version 4.x](migrate-version-1-version-4)

When supported, this article takes advantage of [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) in the isolated worker model, which improves performance and provides a familiar programming model when your app uses HTTP triggers.

## Identify function apps to migrate

Use the following Azure PowerShell script to generate a list of function apps in your subscription that currently use the in-process model.

The script uses the subscription that Azure PowerShell is currently configured to use. You can change the subscription by first running `Set-AzContext -Subscription '<YOUR SUBSCRIPTION ID>'`

and replacing `<YOUR SUBSCRIPTION ID>`

with the ID of the subscription you would like to evaluate.

```
$FunctionApps = Get-AzFunctionApp
$AppInfo = @{}
foreach ($App in $FunctionApps)
{
if ($App.Runtime -eq 'dotnet')
{
$AppInfo.Add($App.Name, $App.Runtime)
}
}
$AppInfo
```


## Choose your target .NET version

On version 4.x of the Functions runtime, your .NET function app targets .NET 6 or .NET 8 when using the in-process model.

When you migrate your function app, you have the opportunity to choose the target version of .NET. You can update your C# project to one of the following versions of .NET that are supported by Functions version 4.x:

| .NET version |
|
|---|

1,2

[Isolated worker model](dotnet-isolated-process-guide)3[Isolated worker model](dotnet-isolated-process-guide)[Isolated worker model](dotnet-isolated-process-guide),[In-process model](functions-dotnet-class-library)2[See policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework)[Isolated worker model](dotnet-isolated-process-guide)1 The [isolated worker model](dotnet-isolated-process-guide) supports Long Term Support (LTS) and Standard Term Support (STS) versions of .NET, as well as .NET Framework. The [in-process model](functions-dotnet-class-library) only supports LTS releases of .NET, ending with .NET 8. For a full feature and functionality comparison between the two models, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

2 Support ends for the in-process model on November 10, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/in-process-model). For continued full support, you should [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

3 .NET 9 previously had an expected end-of-support date of May 12, 2026. During the .NET 9 service window, the .NET team extended support for STS versions to 24 months, starting with .NET 9. For more information, see [the blog post](https://devblogs.microsoft.com/dotnet/dotnet-sts-releases-supported-for-24-months/).

Tip

**We recommend upgrading to .NET 8 on the isolated worker model.** This provides a quick migration path to the fully released version with the longest support window from .NET.

This guide doesn't present specific examples for .NET 10 (preview) or .NET 9. If you need to target one of those versions, you can adapt the .NET 8 examples.

## Prepare for migration

Before you migrate an app to the isolated worker model, you should thoroughly review the contents of this guide. You should also familiarize yourself with the features of the [isolated worker model](dotnet-isolated-process-guide) and the [differences between the two models](dotnet-isolated-in-process-differences).

To migrate the application:

- Migrate your local project to the isolated worker model by following the steps in
[Migrate your local project](#migrate-your-local-project). - After migrating your project, fully test the app locally using version 4.x of the
[Azure Functions Core Tools](functions-run-local). [Update your function app in Azure](#update-your-function-app-in-azure)to the isolated model.

## Migrate your local project

The section outlines the various changes that you need to make to your local project to move it to the isolated worker model. Some of the steps change based on your target version of .NET. Use the tabs to select the instructions that match your desired version.

Tip

If you're moving to an LTS or STS version of .NET, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can be used to automatically make many of the changes mentioned in the following sections.

First, convert the project file and update your dependencies. As you do, you see build errors for the project. In subsequent steps, you'll make the corresponding changes to remove these errors.

### Project file

The following example is a *.csproj* project file that uses .NET 8 on version 4.x:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
<RootNamespace>My.Namespace</RootNamespace>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="4.1.1" />
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


Use one of the following procedures to update this XML file to run in the isolated worker model:

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


Changing your project's target framework might also require changes to parts of your toolchain, outside of project code. For example, in VS Code, you might need to update the `azureFunctions.deploySubpath`

extension setting through user settings or your project's *.vscode/settings.json* file. Check for any dependencies on the framework version that might exist outside of your project code, as part of build steps or a CI/CD pipeline.

### Package references

When migrating to the isolated worker model, you need to change the packages your application references.

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

When migrating to run in an isolated worker process, you must add a *Program.cs* file to your project with the following contents:

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

### Function signature changes

Some key types change between the in-process model and the isolated worker model. Many of these relate to the attributes, parameters, and return types that make up the function signature. For each of your functions, you must make changes to:

- The function attribute, which also sets the function's name
- How the function obtains an
`ILogger`

/`ILogger<T>`

- Trigger and binding attributes and parameters

The rest of this section walks you through each of these steps.

#### Function attributes

The `Function`

attribute in the isolated worker model replaces the `FunctionName`

attribute. The new attribute has the same signature, and the only difference is in the name. You can therefore just perform a string replacement across your project.

#### Logging

In the in-process model, you could include an optional `ILogger`

parameter for your function, or you could use dependency injection to get an `ILogger<T>`

. If your app already used dependency injection, the same mechanisms work in the isolated worker model.

However, for any Functions that relied on the `ILogger`

method parameter, you need to make a change. We recommended that you use dependency injection to obtain an `ILogger<T>`

. Use the following steps to migrate the function's logging mechanism:

In your function class, add a

`private readonly ILogger<MyFunction> _logger;`

property, replacing`MyFunction`

with the name of your function class.Create a constructor for your function class that takes in the

`ILogger<T>`

as a parameter:`public MyFunction(ILogger<MyFunction> logger) { _logger = logger; }`

Replace both instances of

`MyFunction`

in the preceding code snippet with the name of your function class.For logging operations in your function code, replace references to the

`ILogger`

parameter with`_logger`

.Remove the

`ILogger`

parameter from your function signature.

To learn more, see [Logging in the isolated worker model](dotnet-isolated-process-guide#logging).

#### Trigger and binding changes

When you [changed your package references in a previous step](#package-references), you introduced errors for your triggers and bindings that you can now fix:

Remove any

`using Microsoft.Azure.WebJobs;`

statements.Add a

`using Microsoft.Azure.Functions.Worker;`

statement.For each binding attribute, change the attribute's name as specified in its reference documentation, which you can find in the

[Supported bindings](functions-triggers-bindings#supported-bindings)index. In general, the attribute names change as follows:**Triggers typically remain named the same way.**For example,`QueueTrigger`

is the attribute name for both models.**Input bindings typically need**For example, if you used the`Input`

added to their name.`CosmosDB`

input binding attribute in the in-process model, the attribute would now be`CosmosDBInput`

.**Output bindings typically need**For example, if you used the`Output`

added to their name.`Queue`

output binding attribute in the in-process model, this attribute would now be`QueueOutput`

.

Update the attribute parameters to reflect the isolated worker model version, as specified in the binding's reference documentation.

For example, in the in-process model, a blob output binding is represented by a

`[Blob(...)]`

attribute that includes an`Access`

property. In the isolated worker model, the blob output attribute would be`[BlobOutput(...)]`

. The binding no longer requires the`Access`

property, so that parameter can be removed. So`[Blob("sample-images-sm/{fileName}", FileAccess.Write, Connection = "MyStorageConnection")]`

would become`[BlobOutput("sample-images-sm/{fileName}", Connection = "MyStorageConnection")]`

.Move output bindings out of the function parameter list. If you have just one output binding, you can apply this to the return type of the function. If you have multiple outputs, create a new class with properties for each output, and apply the attributes to those properties. To learn more, see

[Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).Consult each binding's reference documentation for the types it allows you to bind to. In some cases, you might need to change the type. For output bindings, if the in-process model version used an

`IAsyncCollector<T>`

, you can replace this with binding to an array of the target type:`T[]`

. You can also consider replacing the output binding with a client object for the service it represents, either as the binding type for an input binding if available, or by[injecting a client yourself](dotnet-isolated-process-guide#register-azure-clients).If your function includes an

`IBinder`

parameter, remove it. Replace the functionality with a client object for the service it represents, either as the binding type for an input binding if available, or by[injecting a client yourself](dotnet-isolated-process-guide#register-azure-clients).Update the function code to work with any new types.


### local.settings.json file

The *local.settings.json* file is only used when running locally. For information, see [Local settings file](functions-develop-local#local-settings-file).

When migrating from running in-process to running in an isolated worker process, you need to change the `FUNCTIONS_WORKER_RUNTIME`

value to *dotnet-isolated*. Make sure that your *local.settings.json* file has at least the following elements:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated"
}
}
```


The value you have for `AzureWebJobsStorage`

might be different. You don't need to change its value as part of the migration.

### host.json file

No changes are required to your *host.json* file. However, if your Application Insights configuration is in this file from your in-process model project, you might want to make additional changes in your *Program.cs* file. The *host.json* file only controls logging from the Functions host runtime, and in the isolated worker model, some of these logs come from your application directly, giving you more control. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### Other code changes

This section highlights other code changes to consider as you work through the migration. These changes aren't needed by all applications, but you should evaluate if any are relevant to your scenarios.

#### JSON serialization

By default, the isolated worker model uses *System.Text.Json* for JSON serialization. To customize serializer options or switch to JSON.NET (*Newtonsoft.Json*), see [Customizing JSON serialization](dotnet-isolated-process-guide#customizing-json-serialization).

#### Application Insights log levels and filtering

Logs can be sent to Application Insights from both the Functions host runtime and code in your project. The *host.json* allows you to configure rules for host logging, but to control logs coming from your code, you need to configure filtering rules as part of your *Program.cs*. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### Example function migrations

#### HTTP trigger example

An HTTP trigger for the in-process model might look like the following example:

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Logging;
namespace Company.Function
{
public static class HttpTriggerCSharp
{
[FunctionName("HttpTriggerCSharp")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = null)] HttpRequest req,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult($"Welcome to Azure Functions, {req.Query["name"]}!");
}
}
}
```


An HTTP trigger for the migrated version might look like the following example:

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


## Update your function app in Azure

Updating your function app to the isolated model involves two changes that should be completed together, because if you only complete one, the app is in an error state. Both of these changes also cause the app process to restart. For these reasons, you should perform the update using a [staging slot](functions-deployment-slots). Staging slots help minimize downtime for your app and allow you to test and verify your migrated code with your updated configuration in Azure. You can then deploy your fully migrated app to the production slot through a swap operation.

Important

When an app's deployed payload doesn't match the configured runtime, it's in [an error state](errors-diagnostics/diagnostic-events/azfd0013). During the migration process, you put the app into this state, ideally only temporarily. Deployment slots help mitigate the effect of this, because the error state will be resolved in your staging (nonproduction) environment before the changes are applied as single update to your production environment. Slots also defend against any mistakes and allow you to detect any other issues before reaching production.

During the process, you might still see errors in logs coming from your staging (nonproduction) slot. This is expected, though these should go away as you proceed through the steps. Before you perform the slot swap operation, you should confirm that these errors stop being raised and that your application is working as expected.

Use the following steps to use deployment slots to update your function app to the isolated worker model:

[Create a deployment slot](functions-deployment-slots#add-a-slot)if you haven't already. You might also want to familiarize yourself with the slot swap process and ensure that you can make updates to the existing application with minimal disruption.Change the configuration of the staging (nonproduction) slot to use the isolated worker model by setting the

`FUNCTIONS_WORKER_RUNTIME`

application setting to`dotnet-isolated`

.`FUNCTIONS_WORKER_RUNTIME`

should**not**be marked as a*slot setting*.If you're also targeting a different version of .NET as part of your update, you should also change the stack configuration. To do so, see

[Update the stack configuration](update-language-versions?pivots=programming-language-csharp#update-the-stack-configuration). You can use the same instructions for any future .NET version updates you make.If you have any automated infrastructure provisioning such as a CI/CD pipeline, make sure that the automations are also updated to keep

`FUNCTIONS_WORKER_RUNTIME`

set to`dotnet-isolated`

and to target the correct .NET version.Publish your migrated project to the staging (nonproduction) slot of your function app.

If you use Visual Studio to publish an isolated worker model project to an existing app or slot that uses the in-process model, it can also complete the previous step for you at the same time. If you didn't complete the previous step, Visual Studio prompts you to update the function app during deployment. Visual Studio presents this as a single operation, but these are still two separate operations. You might still see errors in your logs from the staging (nonproduction) slot during the interim state.

Confirm that your application is working as expected within the staging (nonproduction) slot.

Perform a

[slot swap operation](functions-deployment-slots#swap-slots)to apply the changes you made in your staging (nonproduction) slot to the production slot. A slot swap happens as a single update, which avoids introducing the interim error state in your production environment.Confirm that your application is working as expected within the production slot.


Once you complete these steps, the migration is complete, and your app runs on the isolated model. Congratulations! Repeat the steps from this guide as necessary for [any other apps that need migration](#identify-function-apps-to-migrate).
