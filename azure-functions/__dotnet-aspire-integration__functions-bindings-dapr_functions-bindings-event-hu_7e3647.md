---
merged_at: 2026-01-25T15:41:11.650093
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _dotnet-aspire-integration__functions-bindings-dapr_functions-bindings-event-hub_873933.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: dotnet-aspire-integration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/dotnet-aspire-integration -->

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

<!-- DOCUMENTO FUSIONADO: _functions-bindings-dapr_functions-bindings-event-hubs.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-dapr.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr -->

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

<!-- DOCUMENTO FUSIONADO: functions-bindings-event-hubs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-hubs -->

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

<!-- DOCUMENTO FUSIONADO: __functions-bindings-event-iot__disable-function_functions-kubernetes-keda__func_c19e9f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-event-iot__disable-function_functions-kubernetes-keda.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-event-iot.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-iot -->

# Azure IoT Hub bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with Azure Functions bindings for IoT Hub. The IoT Hub support is based on the [Azure Event Hubs Binding](functions-bindings-event-hubs).

Important

While the following code samples use the Event Hub API, the given syntax is applicable for IoT Hub functions.

| Action | Type |
|---|---|
| Respond to events sent to an IoT hub event stream. |
|

## Install extension

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

<!-- DOCUMENTO FUSIONADO: _disable-function_functions-kubernetes-keda.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: disable-function.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/disable-function -->

# How to disable functions in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to disable a function in Azure Functions. To *disable* a function means to make the runtime ignore the event intended to trigger the function. This ability lets you prevent a specific function from running without having to modify and republish the entire function app.

You can disable a function in place by creating an app setting in the format `AzureWebJobs.<FUNCTION_NAME>.Disabled`

set to `true`

. You can create and modify this application setting in several ways, including by using the [Azure CLI](/en-us/cli/azure/), [Azure PowerShell](/en-us/powershell/azure/), and from your function's **Overview** tab in the [Azure portal](https://portal.azure.com).

Note

Changing application settings causes your function app to restart by default across all hosting plans. For zero-downtime deployments when changing settings, use the [Flex Consumption plan](flex-consumption-plan) with [rolling updates as the site update strategy](flex-consumption-site-updates). For other hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments) for guidance on minimizing downtime.

## Disable a function

Use one of these modes to create an app setting that disables an example function named `QueueTrigger`

:

Use the **Enable** and **Disable** buttons on the function's **Overview** page. These buttons work by changing the value of the `AzureWebJobs.QueueTrigger.Disabled`

app setting. The function-specific app setting is created the first time a function is disabled.

Even when you publish to your function app from a local project, you can still use the portal to disable functions in the function app.

Note

Disabled functions can still be run by calling the REST endpoint using a master key. To learn more, see [Run a disabled function](#run-a-disabled-function). This means that a disabled function still runs when started from the **Test/Run** window in the portal using the **master (Host key)**.

## Disable functions in a slot

By default, app settings also apply to apps running in deployment slots. You can, however, override the app setting used by the slot by setting a slot-specific app setting. For example, you might want a function to be active in production but not during deployment testing. It's common to disable timer triggered functions in slots to prevent simultaneous executions.

To disable a function only in the staging slot:

Navigate to the slot instance of your function app by selecting **Deployment slots** under **Deployment**, choosing your slot, and selecting **Functions** in the slot instance. Choose your function, then use the **Enable** and **Disable** buttons on the function's **Overview** page. These buttons work by changing the value of the `AzureWebJobs.<FUNCTION_NAME>.Disabled`

app setting. This function-specific setting is created the first time you disable the function.

You can also directly add the app setting named `AzureWebJobs.<FUNCTION_NAME>.Disabled`

with value of `true`

in the **Configuration** for the slot instance. When you add a slot-specific app setting, make sure to check the **Deployment slot setting** box. This option maintains the setting value with the slot during swaps.

To learn more, see [Azure Functions Deployment slots](functions-deployment-slots).

## Run a disabled function

You can still cause a disabled function to run by supplying the master access key (`_master`

) in a REST request to the endpoint URL of the disabled function. In this way, you can develop and validate functions in Azure in a disabled state while preventing them from being accessed by others. Using any other type of key in the request returns an HTTP 404 response.

Caution

Due to the elevated permissions in your function app granted by the master key, you shouldn't share this key with third parties or distribute it in native client applications. Use caution when choosing the admin HTTP access level for your function endpoints.

To learn more about the master key, see [Understand keys](function-keys-how-to#understand-keys). To learn more about calling non-HTTP triggered functions, see [Manually run a non HTTP-triggered function](functions-manually-run-non-http).

## Disable functions locally

Functions can be disabled in the same way when running locally. To disable a function named `QueueTrigger`

, add an entry to the Values collection in the local.settings.json file, as follows:

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "python",
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"AzureWebJobs.QueueTrigger.Disabled": true
}
}
```


## Considerations

Keep the following considerations in mind when you disable functions:

When you disable an HTTP triggered function by using the methods described in this article, the endpoint can still be accessed when running on your local computer and

[in the portal](#run-a-disabled-function).At this time, function names that contain a hyphen (

`-`

) can't be disabled when running on Linux. If you plan to disable your functions when running on Linux, don't use hyphens in your function names.

## Next steps

This article is about disabling automatic triggers. For more information about triggers, see [Triggers and bindings](functions-triggers-bindings).


---

<!-- DOCUMENTO FUSIONADO: functions-kubernetes-keda.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-kubernetes-keda -->

# Azure Functions on Kubernetes with KEDA

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Functions runtime provides flexibility in hosting where and how you want. [KEDA](https://keda.sh) (Kubernetes-based Event Driven Autoscaling) pairs seamlessly with the Azure Functions runtime and tooling to provide event driven scale in Kubernetes.

Important

Running your containerized function apps on Kubernetes, either by using KEDA or by direct deployment, is an open-source effort that you can use free of cost. Best-effort support is provided by contributors and from the community by using [GitHub issues in the Azure Functions repository](https://github.com/Azure/Azure-Functions/issues). Please use these issues to report bugs and raise feature requests.

For fully-supported Kubernetes deployments, instead consider [Azure Container Apps hosting of Azure Functions](../container-apps/functions-overview).

## How Kubernetes-based functions work

The Azure Functions service is made up of two key components: a runtime and a scale controller. The Functions runtime runs and executes your code. The runtime includes logic on how to trigger, log, and manage function executions. The Azure Functions runtime can run *anywhere*. The other component is a scale controller. The scale controller monitors the rate of events that are targeting your function, and proactively scales the number of instances running your app. To learn more, see [Azure Functions scale and hosting](functions-scale).

Kubernetes-based Functions provides the Functions runtime in a [Docker container](functions-create-container-registry) with event-driven scaling through KEDA. KEDA can scale in to zero instances (when no events are occurring) and out to *n* instances. It does this by exposing custom metrics for the Kubernetes autoscaler (Horizontal Pod Autoscaler). Using Functions containers with KEDA makes it possible to replicate serverless function capabilities in any Kubernetes cluster. These functions can also be deployed using [Azure Kubernetes Services (AKS) virtual nodes](/en-us/azure/aks/virtual-nodes-cli) feature for serverless infrastructure.

## Managing KEDA and functions in Kubernetes

To run Functions on your Kubernetes cluster, you must install the KEDA component. You can install this component in one of the following ways:

Azure Functions Core Tools: using the

.`func kubernetes install`

commandHelm: there are various ways to install KEDA in any Kubernetes cluster, including Helm. Deployment options are documented on the

[KEDA site](https://keda.sh/docs/deploy/).

## Deploying a function app to Kubernetes

You can deploy any function app to a Kubernetes cluster running KEDA. Since your functions run in a Docker container, your project needs a Dockerfile. You can create a Dockerfile by using the [ --docker option](functions-core-tools-reference#func-init) when calling

`func init`

to create the project. If you forgot to create your Dockerfile, you can always call `func init`

again from the root of your code project.(Optional) If you need to create your Dockerfile, use the

command with the`func init`

`--docker-only`

option:`func init --docker-only`

To learn more about Dockerfile generation, see the

reference.`func init`

Use the

command to build your image and deploy your containerized function app to Kubernetes:`func kubernetes deploy`

`func kubernetes deploy --name <name-of-function-deployment> --registry <container-registry-username>`

In this example, replace

`<name-of-function-deployment>`

with the name of your function app. The deploy command performs these tasks:- The Dockerfile created earlier is used to build a local image for your containerized function app.
- The local image is tagged and pushed to the container registry where the user is logged in.
- A manifest is created and applied to the cluster that defines a Kubernetes
`Deployment`

resource, a`ScaledObject`

resource, and`Secrets`

, which includes environment variables imported from your`local.settings.json`

file.


### Deploying a function app from a private registry

The previous deployment steps work for private registries as well. If you're pulling your container image from a private registry, include the `--pull-secret`

flag that references the Kubernetes secret holding the private registry credentials when running `func kubernetes deploy`

.

## Removing a function app from Kubernetes

After deploying you can remove a function by removing the associated `Deployment`

, `ScaledObject`

, an `Secrets`

created.

```
kubectl delete deploy <name-of-function-deployment>
kubectl delete ScaledObject <name-of-function-deployment>
kubectl delete secret <name-of-function-deployment>
```


## Uninstalling KEDA from Kubernetes

You can remove KEDA from your cluster in one of the following ways:

Azure Functions Core Tools: using the

.`func kubernetes remove`

commandHelm: see the uninstall steps

[on the KEDA site](https://keda.sh/docs/deploy/).

## Supported triggers in KEDA

KEDA has support for the following Azure Function triggers:

### HTTP Trigger support

You can use Azure Functions that expose HTTP triggers, but KEDA doesn't directly manage them. You can use the KEDA prometheus trigger to [scale HTTP Azure Functions from one to n instances](https://dev.to/anirudhgarg_99/scale-up-and-down-a-http-triggered-function-app-in-kubernetes-using-keda-4m42).

## Next Steps

For more information, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: _functions-deployment-slots_functions-create-function-app-portal.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-deployment-slots.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deployment-slots -->

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

<!-- DOCUMENTO FUSIONADO: functions-create-function-app-portal.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-function-app-portal -->

# Create a function app in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the Azure portal to create a function app that's hosted in Azure Functions. These hosting plan options, which support dynamic, event-driven scaling, are featured:

| Hosting option | Description |
|---|---|
|

[Premium plan](functions-premium-plan)[Consumption plan](consumption-plan)The Flex Consumption plan is the recommended plan for hosting serverless compute resources in Azure.

Choose your preferred hosting plan at the [top](#top) of the article. For more information about all supported hosting options, see [Azure Functions hosting options](functions-scale).

## Prerequisites

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

## Create a function app

You must have a function app to host the execution of your functions. A function app lets you group functions as a logical unit for easier management, deployment, scaling, and sharing of resources.

Use these steps to create your function app and related Azure resources in the Azure portal.

In the

[Azure portal](https://portal.azure.com), from the menu or the**Home**page, select**Create a resource**.Select

**Get started**and then**Create**under**Function App**.Under

**Select a hosting option**, choose**Flex Consumption**>**Select**.On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription in which you create your new function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access. Unsupported regions aren't displayed. For more information, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Runtime stack**Preferred language Choose one of the supported language runtime stacks. In-portal editing using Visual Studio Code for the Web is currently only available for Node.js, PowerShell, and Python apps. C# class library and Java functions must be [developed locally](functions-develop-local#local-development-environments).**Version**Language version Choose a supported version of your language runtime stack. **Instance size**Default Determines the amount of instance memory allocated for each instance of your app. For more information, see [Instance sizes](flex-consumption-plan#instance-sizes).On the

**Storage**page, accept the default behavior of creating a new[default host storage account](storage-considerations)or choose to use an existing storage account.

On the

**Monitoring**page, make sure that**Enable Application Insights**is selected. Accept the default to create a new Application Insights instance, or else choose to use an existing instance. When you create an Application Insights instance, you're also asked to select a Log Analytics**Workspace**.On the

**Authentication**page, change the**Authentication type**to**Managed identity**for all resources. With this option, a user-assigned managed identity is also created that your app uses to access these Azure resources using Microsoft Entra ID authentication. Managed identities with Microsoft Entra ID provides the highest level of security for connecting to Azure resources.Accept the default options in the remaining tabs and then select

**Review + create**to review the app configuration you chose.When you're satisfied, select

**Create**to provision and deploy the function app and related resources.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

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

## Next steps

You can now deploy a code project to the function app resources you created in Azure.

You can create, verify, and deploy a code project to your new function app from these local environments:
