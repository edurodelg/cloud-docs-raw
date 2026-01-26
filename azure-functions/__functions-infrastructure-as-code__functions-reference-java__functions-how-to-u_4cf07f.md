---
merged_at: 2026-01-26T21:02:36.360775
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-infrastructure-as-code.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-infrastructure-as-code -->

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

<!-- DOCUMENTO FUSIONADO: _functions-reference-java__functions-how-to-use-nat-gateway_functions-how-to-git_b237fb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-reference-java.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-java -->

# Azure Functions Java developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This guide contains detailed information to help you succeed developing Azure Functions using Java.

As a Java developer, if you're new to Azure Functions, consider first reading one of the following articles:

| Getting started | Concepts | Scenarios/samples |
|---|---|---|

## Java function basics

A Java function is a `public`

method, decorated with the annotation `@FunctionName`

. This method defines the entry for a Java function, and must be unique in a particular package. The package can have multiple classes with multiple public methods annotated with `@FunctionName`

. A single package is deployed to a function app in Azure. In Azure, the function app provides the deployment, execution, and management context for your individual Java functions.

## Programming model

The concepts of [triggers and bindings](functions-triggers-bindings) are fundamental to Azure Functions. Triggers start the execution of your code. Bindings give you a way to pass data to and return data from a function, without having to write custom data access code.

## Create Java functions

To make it easier to create Java functions, there are Maven-based tooling and archetypes that use predefined Java templates to help you create projects with a specific function trigger.

### Maven-based tooling

The following developer environments have Azure Functions tooling that lets you create Java function projects:

These articles show you how to create your first functions using your IDE of choice.

### Project scaffolding

If you prefer command line development from the Terminal, the simplest way to scaffold Java-based function projects is to use `Apache Maven`

archetypes. The Java Maven archetype for Azure Functions is published under the following *groupId*:*artifactId*: [com.microsoft.azure:azure-functions-archetype](https://search.maven.org/artifact/com.microsoft.azure/azure-functions-archetype/).

The following command generates a new Java function project using this archetype:

```
mvn archetype:generate \
-DarchetypeGroupId=com.microsoft.azure \
-DarchetypeArtifactId=azure-functions-archetype
```


To get started using this archetype, see the [Java quickstart](how-to-create-function-azure-cli?pivots=programming-language-java).

## Folder structure

Here's the folder structure of an Azure Functions Java project:

```
FunctionsProject
| - src
| | - main
| | | - java
| | | | - FunctionApp
| | | | | - MyFirstFunction.java
| | | | | - MySecondFunction.java
| - target
| | - azure-functions
| | | - FunctionApp
| | | | - FunctionApp.jar
| | | | - host.json
| | | | - MyFirstFunction
| | | | | - function.json
| | | | - MySecondFunction
| | | | | - function.json
| | | | - bin
| | | | - lib
| - pom.xml
```


You can use a shared [host.json](functions-host-json) file to configure the function app. Each function has its own code file (.java) and binding configuration file (function.json).

You can have more than one function in a project. However, don't put your functions into separate jars. Using multiple jars in a single function app isn't supported. The `FunctionApp`

in the target directory is what gets deployed to your function app in Azure.

## Triggers and annotations

Functions are invoked by a trigger, such as an HTTP request, a timer, or an update to data. Your function needs to process that trigger, and any other inputs, to produce one or more outputs.

Use the Java annotations included in the [com.microsoft.azure.functions.annotation.*](/en-us/java/api/com.microsoft.azure.functions.annotation) package to bind input and outputs to your methods. For more information, see the [Java reference docs](/en-us/java/api/com.microsoft.azure.functions.annotation).

Important

You must configure an Azure Storage account in your [local.settings.json](functions-develop-local#local-settings-file) to run Azure Blob storage, Azure Queue storage, or Azure Table storage triggers locally.

Example:

```
public class Function {
public String echo(@HttpTrigger(name = "req",
methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
String req, ExecutionContext context) {
return String.format(req);
}
}
```


Here's the generated corresponding `function.json`

by the [azure-functions-maven-plugin](https://mvnrepository.com/artifact/com.microsoft.azure/azure-functions-maven-plugin):

```
{
"scriptFile": "azure-functions-example.jar",
"entryPoint": "com.example.Function.echo",
"bindings": [
{
"type": "httpTrigger",
"name": "req",
"direction": "in",
"authLevel": "anonymous",
"methods": [ "GET","POST" ]
},
{
"type": "http",
"name": "$return",
"direction": "out"
}
]
}
```


## Java versions

The version of Java on which your app runs in Azure is specified in the pom.xml file. The Maven archetype currently generates a pom.xml for Java 8, which you can change before publishing. The Java version in pom.xml should match the version of Java on which you develop and test your app locally.

### Supported versions

The following table shows current supported Java versions for each major version of the Functions runtime, by operating system:

| Functions version | Java versions (Windows) | Java versions (Linux) |
|---|---|---|
| 4.x | 21 17 11 8 |
21 17 11 8 |
| 3.x | 11 8 |
11 8 |
| 2.x | 8 | n/a |

Unless you specify a Java version for your deployment, the Maven archetype defaults to Java 8 during deployment to Azure.

### Specify the deployment version

You can control the version of Java targeted by the Maven archetype by using the `-DjavaVersion`

parameter. This parameter must match [supported Java versions](supported-languages?pivots=programming-language-java#languages-by-runtime-version).

The Maven archetype generates a pom.xml that targets the specified Java version. The following elements in pom.xml indicate the Java version to use:

| Element | Java 8 value | Java 11 value | Java 17 value | Java 21 value | Description |
|---|---|---|---|---|---|
`Java.version` |
1.8 | 11 | 17 | 21 | Version of Java used by the maven-compiler-plugin. |
`JavaVersion` |
8 | 11 | 17 | 21 | Java version hosted by the function app in Azure. |

The following examples show the settings for Java 8 in the relevant sections of the pom.xml file:

`Java.version`


```
<properties>
<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
<java.version>1.8</java.version>
<azure.functions.maven.plugin.version>1.6.0</azure.functions.maven.plugin.version>
<azure.functions.java.library.version>1.3.1</azure.functions.java.library.version>
<functionAppName>fabrikam-functions-20200718015742191</functionAppName>
<stagingDirectory>${project.build.directory}/azure-functions/${functionAppName}</stagingDirectory>
</properties>
```


`JavaVersion`


```
<runtime>
<!-- runtime os, could be windows, linux or docker-->
<os>windows</os>
<javaVersion>8</javaVersion>
<!-- for docker function, please set the following parameters -->
<!-- <image>[hub-user/]repo-name[:tag]</image> -->
<!-- <serverId></serverId> -->
<!-- <registryUrl></registryUrl> -->
</runtime>
```


Important

You must have the JAVA_HOME environment variable set correctly to the JDK directory that is used during code compiling using Maven. Make sure that the version of the JDK is at least as high as the `Java.version`

setting.

### Specify the deployment OS

Maven also lets you specify the operating system on which your function app runs in Azure. Use the `os`

element to choose the operating system.

| Element | Windows | Linux | Docker |
|---|---|---|---|
`os` |
`windows` |
`linux` |
`docker` |

The following example shows the operating system setting in the `runtime`

section of the pom.xml file:

```
<runtime>
<!-- runtime os, could be windows, linux or docker-->
<os>windows</os>
<javaVersion>8</javaVersion>
<!-- for docker function, please set the following parameters -->
<!-- <image>[hub-user/]repo-name[:tag]</image> -->
<!-- <serverId></serverId> -->
<!-- <registryUrl></registryUrl> -->
</runtime>
```


## JDK runtime availability and support

Microsoft and [Adoptium](https://adoptium.net/) builds of OpenJDK are provided and supported on Functions for Java 8 (Adoptium), Java 11, 17 and 21 (MSFT). These binaries are provided as a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure. They contain all the components for building and running Java SE applications.

For local development or testing, you can download the [Microsoft build of OpenJDK](/en-us/java/openjdk/download) or [Adoptium Temurin](https://adoptium.net/?variant=openjdk8&jvmVariant=hotspot) binaries for free. [Azure support](https://azure.microsoft.com/support/) for issues with the JDKs and function apps is available with a [qualified support plan](https://azure.microsoft.com/support/plans/).

If you would like to continue using the Zulu for Azure binaries on your Function app, [configure your app accordingly](https://github.com/Azure/azure-functions-java-worker/wiki/Customize-JVM-to-use-Zulu). You can continue to use the Azul binaries for your site. However, any security patches or improvements are only available in new versions of the OpenJDK. Because of this, you should eventually remove this configuration so that your apps use the latest available version of Java.

## Customize JVM

Functions lets you customize the Java virtual machine (JVM) used to run your Java functions. The [following JVM options](https://github.com/Azure/azure-functions-java-worker/blob/master/worker.config.json#L7) are used by default:

`-XX:+TieredCompilation`

`-XX:TieredStopAtLevel=1`

`-noverify`

`-Djava.net.preferIPv4Stack=true`

`-jar`


You can provide other arguments to the JVM by using one of the following application settings, depending on the plan type:

| Plan type | Setting name | Comment |
|---|---|---|
|

`languageWorkers__java__arguments`

[Premium plan](functions-premium-plan)[Dedicated plan](dedicated-plan)`JAVA_OPTS`

The following sections show you how to add these settings. To learn more about working with application settings, see the [Work with application settings](functions-how-to-use-azure-function-app-settings#settings) section.

### Azure portal

In the [Azure portal](https://portal.azure.com), use the [Application Settings tab](functions-how-to-use-azure-function-app-settings#settings) to add either the `languageWorkers__java__arguments`

or the `JAVA_OPTS`

setting.

### Azure CLI

You can use the [az functionapp config appsettings set](/en-us/cli/azure/functionapp/config/appsettings) command to add these settings, as shown in the following example for the `-Djava.awt.headless=true`

option:

```
az functionapp config appsettings set \
--settings "languageWorkers__java__arguments=-Djava.awt.headless=true" \
--name <APP_NAME> --resource-group <RESOURCE_GROUP>
```


This example enables headless mode. Replace `<APP_NAME>`

with the name of your function app, and `<RESOURCE_GROUP>`

with the resource group.

## Third-party libraries

Azure Functions supports the use of third-party libraries. By default, all dependencies specified in your project `pom.xml`

file are automatically bundled during the [ mvn package](https://github.com/Microsoft/azure-maven-plugins/blob/master/azure-functions-maven-plugin/README.md#azure-functionspackage) goal. For libraries not specified as dependencies in the

`pom.xml`

file, place them in a `lib`

directory in the function's root directory. Dependencies placed in the `lib`

directory are added to the system class loader at runtime.The `com.microsoft.azure.functions:azure-functions-java-library`

dependency is provided on the classpath by default, and doesn't need to be included in the `lib`

directory. Also, [azure-functions-java-worker](https://github.com/Azure/azure-functions-java-worker) adds dependencies listed [here](https://github.com/Azure/azure-functions-java-worker/wiki/Azure-Java-Functions-Worker-Dependencies) to the classpath.

## Data type support

You can use plain-old Java objects (POJOs), types defined in `azure-functions-java-library`

, or primitive data types such as `String`

and `Integer`

to bind to input or output bindings.

Note

Support for binding to SDK types is currently in preview and limited to the Azure Blob Storage SDK. For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

### POJOs

For converting input data to POJO, [azure-functions-java-worker](https://github.com/Azure/azure-functions-java-worker) uses the [gson](https://github.com/google/gson) library. POJO types used as inputs to functions should be `public`

.

### Binary data

Bind binary inputs or outputs to `byte[]`

, by setting the `dataType`

field in your function.json to `binary`

:

```
@FunctionName("BlobTrigger")
@StorageAccount("AzureWebJobsStorage")
public void blobTrigger(
@BlobTrigger(name = "content", path = "myblob/{fileName}", dataType = "binary") byte[] content,
@BindingName("fileName") String fileName,
final ExecutionContext context
) {
context.getLogger().info("Java Blob trigger function processed a blob.\n Name: " + fileName + "\n Size: " + content.length + " Bytes");
}
```


If you expect null values, use `Optional<T>`

.

### SDK types (preview)

You can currently use these Blob Storage SDK types in your bindings: `BlobClient`

and `BlobContainerClient`

.

With SDK types support enabled, your functions can use Azure SDK client types to access blobs as streams directly from storage, which provides these benefits over POJOs or binary types:

- Lower latency
- Reduced memory requirements
- Removes request-based size limits (uses service defaults)
- Provides access to the full SDK surface: metadata, ACLs, legal holds, and other SDK-specific data.

#### Requirements

- Set the
app setting to`JAVA_ENABLE_SDK_TYPES`

`true`

to enable SDK types. `azure-functions-maven-plugin`

(or Gradle plug-in) version`1.38.0`

or a higher version.

#### Examples

Blob trigger that uses `BlobClient`

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


Blob trigger that uses `BlobContainerClient`

to access info about blobs in the container.

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


Blob input binding that uses `BlobClient`

to get information about the blob that triggered the execution.

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


#### Considerations

- The
`dataType`

setting on`@BlobTrigger`

is ignored when binding to an SDK type. - Currently, only one SDK type can be used at a time in a given function definition. When a function has both a Blog trigger or input binding and a Blob output binding, one binding can use an SDK type (such as
`BlobClient`

) and the others must use a native type or POJO. - You can use managed identities with SDK types.

#### Troubleshooting

These are potential errors that might occur when using SDK types:

| Exception | Meaning |
|---|---|
`SdkAnalysisException` |
Build plug-in couldn’t create metadata. This might be due to duplicate SDK-types in a single function definition, an unsupported parameter type, or some other misconfiguration. |
`SdkRegistryException` |
Runtime doesn’t recognize the stored FQCN, which can be caused by mismatched library versions. |
`SdkHydrationException` |
Middleware failed to build the SDK client, which can occur due to missing environment variables, reflection errors, credential failures, and similar runtime issues. |
`SdkTypeCreationException` |
Factory couldn’t turn metadata into the final SDK type, which is usually caused by a casting issues. |

Check the inner message for more details about the exact cause. Most SDK types issues are caused by misspelled environment variable names or missing dependencies.

## Bindings

Input and output bindings provide a declarative way to connect to data from within your code. A function can have multiple input and output bindings.

### Input binding example

```
package com.example;
import com.microsoft.azure.functions.annotation.*;
public class Function {
@FunctionName("echo")
public static String echo(
@HttpTrigger(name = "req", methods = { HttpMethod.PUT }, authLevel = AuthorizationLevel.ANONYMOUS, route = "items/{id}") String inputReq,
@TableInput(name = "item", tableName = "items", partitionKey = "Example", rowKey = "{id}", connection = "AzureWebJobsStorage") TestInputData inputData,
@TableOutput(name = "myOutputTable", tableName = "Person", connection = "AzureWebJobsStorage") OutputBinding<Person> testOutputData
) {
testOutputData.setValue(new Person(httpbody + "Partition", httpbody + "Row", httpbody + "Name"));
return "Hello, " + inputReq + " and " + inputData.getKey() + ".";
}
public static class TestInputData {
public String getKey() { return this.rowKey; }
private String rowKey;
}
public static class Person {
public String partitionKey;
public String rowKey;
public String name;
public Person(String p, String r, String n) {
this.partitionKey = p;
this.rowKey = r;
this.name = n;
}
}
}
```


You invoke this function with an HTTP request.

- HTTP request payload is passed as a
`String`

for the argument`inputReq`

. - One entry is retrieved from Table storage, and is passed as
`TestInputData`

to the argument`inputData`

.

To receive a batch of inputs, you can bind to `String[]`

, `POJO[]`

, `List<String>`

, or `List<POJO>`

.

```
@FunctionName("ProcessIotMessages")
public void processIotMessages(
@EventHubTrigger(name = "message", eventHubName = "%AzureWebJobsEventHubPath%", connection = "AzureWebJobsEventHubSender", cardinality = Cardinality.MANY) List<TestEventData> messages,
final ExecutionContext context)
{
context.getLogger().info("Java Event Hub trigger received messages. Batch size: " + messages.size());
}
public class TestEventData {
public String id;
}
```


This function gets triggered whenever there's new data in the configured event hub. Because the `cardinality`

is set to `MANY`

, the function receives a batch of messages from the event hub. `EventData`

from event hub gets converted to `TestEventData`

for the function execution.

### Output binding example

You can bind an output binding to the return value by using `$return`

.

```
package com.example;
import com.microsoft.azure.functions.annotation.*;
public class Function {
@FunctionName("copy")
@StorageAccount("AzureWebJobsStorage")
@BlobOutput(name = "$return", path = "samples-output-java/{name}")
public static String copy(@BlobTrigger(name = "blob", path = "samples-input-java/{name}") String content) {
return content;
}
}
```


If there are multiple output bindings, use the return value for only one of them.

To send multiple output values, use `OutputBinding<T>`

defined in the `azure-functions-java-library`

package.

```
@FunctionName("QueueOutputPOJOList")
public HttpResponseMessage QueueOutputPOJOList(@HttpTrigger(name = "req", methods = { HttpMethod.GET,
HttpMethod.POST }, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "itemsOut", queueName = "test-output-java-pojo", connection = "AzureWebJobsStorage") OutputBinding<List<TestData>> itemsOut,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String query = request.getQueryParameters().get("queueMessageId");
String queueMessageId = request.getBody().orElse(query);
itemsOut.setValue(new ArrayList<TestData>());
if (queueMessageId != null) {
TestData testData1 = new TestData();
testData1.id = "msg1"+queueMessageId;
TestData testData2 = new TestData();
testData2.id = "msg2"+queueMessageId;
itemsOut.getValue().add(testData1);
itemsOut.getValue().add(testData2);
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + queueMessageId).build();
} else {
return request.createResponseBuilder(HttpStatus.INTERNAL_SERVER_ERROR)
.body("Did not find expected items in CosmosDB input list").build();
}
}
public static class TestData {
public String id;
}
```


You invoke this function on an `HttpRequest`

object. It writes multiple values to Queue storage.

## HttpRequestMessage and HttpResponseMessage

These helper types, which are designed to work with HTTP Trigger functions, are defined in `azure-functions-java-library`

:

| Specialized type | Target | Typical usage |
|---|---|---|
`HttpRequestMessage<T>` |
HTTP Trigger | Gets method, headers, or queries |
`HttpResponseMessage` |
HTTP Output Binding | Returns status other than 200 |

## Metadata

Few triggers send [trigger metadata](functions-triggers-bindings) along with input data. You can use annotation `@BindingName`

to bind to trigger metadata.

```
package com.example;
import java.util.Optional;
import com.microsoft.azure.functions.annotation.*;
public class Function {
@FunctionName("metadata")
public static String metadata(
@HttpTrigger(name = "req", methods = { HttpMethod.GET, HttpMethod.POST }, authLevel = AuthorizationLevel.ANONYMOUS) Optional<String> body,
@BindingName("name") String queryValue
) {
return body.orElse(queryValue);
}
}
```


In the preceding example, the `queryValue`

is bound to the query string parameter `name`

in the HTTP request URL, `http://{example.host}/api/metadata?name=test`

. Here's another example, showing how to bind to `Id`

from queue trigger metadata.

```
@FunctionName("QueueTriggerMetadata")
public void QueueTriggerMetadata(
@QueueTrigger(name = "message", queueName = "test-input-java-metadata", connection = "AzureWebJobsStorage") String message,@BindingName("Id") String metadataId,
@QueueOutput(name = "output", queueName = "test-output-java-metadata", connection = "AzureWebJobsStorage") OutputBinding<TestData> output,
final ExecutionContext context
) {
context.getLogger().info("Java Queue trigger function processed a message: " + message + " with metadataId:" + metadataId );
TestData testData = new TestData();
testData.id = metadataId;
output.setValue(testData);
}
```


Note

The name provided in the annotation needs to match the metadata property.

## Execution context

`ExecutionContext`

, defined in the `azure-functions-java-library`

, contains helper methods that are used to communicate with the functions runtime. For more information, see the [ExecutionContext reference article](/en-us/java/api/com.microsoft.azure.functions.executioncontext).

### Logger

Use `getLogger`

, defined in `ExecutionContext`

, to write logs from function code.

Example:

```
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
public class Function {
public String echo(@HttpTrigger(name = "req", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) String req, ExecutionContext context) {
if (req.isEmpty()) {
context.getLogger().warning("Empty request body received by function " + context.getFunctionName() + " with invocation " + context.getInvocationId());
}
return String.format(req);
}
}
```


## View logs and trace

You can use the Azure CLI to stream Java stdout and stderr logging, and other application logging.

Here's how to configure your function app to write application logging by using the Azure CLI:

```
az webapp log config --name functionname --resource-group myResourceGroup --application-logging true
```


To stream logging output for your function app by using the Azure CLI, open a new command prompt, Bash, or Terminal session, and enter the following command:

The [az webapp log tail](/en-us/cli/azure/webapp/log) command has options to filter output by using the `--provider`

option.

To download the log files as a single ZIP file by using the Azure CLI, open a new command prompt, Bash, or Terminal session, and enter the following command:

```
az webapp log download --resource-group resourcegroupname --name functionappname
```


You must enable file system logging in the Azure portal or the Azure CLI before running this command.

## Environment variables

In Functions, [app settings](functions-app-settings), such as service connection strings, are exposed as environment variables during execution. You can access these settings by using, `System.getenv("AzureWebJobsStorage")`

.

The following example gets the [application setting](functions-how-to-use-azure-function-app-settings#settings), with the key named `myAppSetting`

:

```
public class Function {
public String echo(@HttpTrigger(name = "req", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) String req, ExecutionContext context) {
context.getLogger().info("My app setting value: "+ System.getenv("myAppSetting"));
return String.format(req);
}
}
```


## Use dependency injection in Java Functions

Azure Functions Java supports the dependency injection (DI) software design pattern, which is a technique to achieve [Inversion of Control (IoC)](/en-us/dotnet/architecture/modern-web-apps-azure/architectural-principles#dependency-inversion) between classes and their dependencies. Java Azure Functions provides a hook to integrate with popular Dependency Injection frameworks in your Functions Apps. [Azure Functions Java SPI](https://github.com/Azure/azure-functions-java-additions/tree/dev/azure-functions-java-spi) contains an interface [FunctionInstanceInjector](https://github.com/Azure/azure-functions-java-additions/blob/dev/azure-functions-java-spi/src/main/java/com/microsoft/azure/functions/spi/inject/FunctionInstanceInjector.java). By implementing this interface, you can return an instance of your function class and your functions are invoked on this instance. This gives frameworks like [Spring](/en-us/azure/developer/java/spring-framework/getting-started-with-spring-cloud-function-in-azure?toc=%2Fazure%2Fazure-functions%2Ftoc.json), [Quarkus](/en-us/azure/azure-functions/functions-create-first-quarkus), Google Guice, Dagger, etc. the ability to create the function instance and register it into their IOC container. This means you can use those Dependency Injection frameworks to manage your functions naturally.

Note

Microsoft Azure Functions Java SPI Types ([azure-function-java-spi](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-spi/1.0.0)) is a package that contains all SPI interfaces for third parties to interact with Microsoft Azure functions runtime.

### Function instance injector for dependency injection

[azure-function-java-spi](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-spi/1.0.0) contains an interface FunctionInstanceInjector

```
package com.microsoft.azure.functions.spi.inject;
/**
* The instance factory used by DI framework to initialize function instance.
*
* @since 1.0.0
*/
public interface FunctionInstanceInjector {
/**
* This method is used by DI framework to initialize the function instance. This method takes in the customer class and returns
* an instance create by the DI framework, later customer functions will be invoked on this instance.
* @param functionClass the class that contains customer functions
* @param <T> customer functions class type
* @return the instance that will be invoked on by azure functions java worker
* @throws Exception any exception that is thrown by the DI framework during instance creation
*/
<T> T getInstance(Class<T> functionClass) throws Exception;
}
```


For more examples that use FunctionInstanceInjector to integrate with Dependency injection frameworks refer to [this](https://github.com/Azure/azure-functions-java-worker/tree/dev/samples/dependency-injection-example) repository.

## Next steps

For more information about Azure Functions Java development, see the following resources:

[Best practices for Azure Functions](functions-best-practices)[Azure Functions developer reference](functions-reference)[Azure Functions triggers and bindings](functions-triggers-bindings)- Local development and debug with
[Visual Studio Code](https://code.visualstudio.com/docs/java/java-azurefunctions),[IntelliJ](functions-create-maven-intellij), and[Eclipse](functions-create-maven-eclipse) [Remote Debug Java functions using Visual Studio Code](https://code.visualstudio.com/docs/java/java-serverless#_remote-debug-functions-running-in-the-cloud)[Maven plugin for Azure Functions](https://github.com/Microsoft/azure-maven-plugins/blob/develop/azure-functions-maven-plugin/README.md)- Streamline function creation through the
`azure-functions:add`

goal, and prepare a staging directory for[ZIP file deployment](deployment-zip-push).


---

<!-- DOCUMENTO FUSIONADO: _functions-how-to-use-nat-gateway_functions-how-to-github-actions.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-how-to-use-nat-gateway.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-nat-gateway -->

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

<!-- DOCUMENTO FUSIONADO: functions-how-to-github-actions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-github-actions -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-notification-hubs -->

# Azure Notification Hubs output bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to send push notifications by using [Azure Notification Hubs](../notification-hubs/notification-hubs-push-notification-overview) bindings in Azure Functions. Azure Functions supports output bindings for Notification Hubs.

You must configure Notification Hubs for the Platform Notifications Service (PNS) you want to use. For more information about how to get push notifications in your client app from Notification Hubs, see [Quickstart: Set up push notifications in a notification hub](../notification-hubs/configure-notification-hub-portal-pns-settings).

Important

Google has [deprecated Google Cloud Messaging (GCM) in favor of Firebase Cloud Messaging (FCM)](https://developers.google.com/cloud-messaging/faq). However, output bindings for Notification Hubs doesn't support FCM. To send notifications using FCM, use the [Firebase API](https://firebase.google.com/docs/cloud-messaging/server#choosing-a-server-option) directly in your function or use [template notifications](../notification-hubs/notification-hubs-templates-cross-platform-push-messages).

## Packages: Functions 1.x

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

The Notification Hubs bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs) NuGet package, version 1.x. Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/v2.x/src/WebJobs.Extensions.NotificationHubs) GitHub repository.

The following table lists how to add support for output binding in each development environment.

| Development environment | To add support in Functions 1.x |
|---|---|
| Local development: C# class library |
|

## Packages: Functions 2.x and higher

Output binding isn't available in Functions 2.x and higher.

## Example: template

The notifications you send can be native notifications or [template notifications](../notification-hubs/notification-hubs-templates-cross-platform-push-messages). A native notification targets a specific client platform, as configured in the `platform`

property of the output binding. A template notification can be used to target multiple platforms.

Template examples for each language:

[C# script: out parameter](#c-script-template-example-out-parameter)[C# script: asynchronous](#c-script-template-example-asynchronous)[C# script: JSON](#c-script-template-example-json)[C# script: library types](#c-script-template-example-library-types)[F#](#f-template-example)[JavaScript](#javascript-template-example)

### C# script template example: out parameter

This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages) that contains a `message`

placeholder in the template:

```
using System;
using System.Threading.Tasks;
using System.Collections.Generic;
public static void Run(string myQueueItem, out IDictionary<string, string> notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
notification = GetTemplateProperties(myQueueItem);
}
private static IDictionary<string, string> GetTemplateProperties(string message)
{
Dictionary<string, string> templateProperties = new Dictionary<string, string>();
templateProperties["message"] = message;
return templateProperties;
}
```


### C# script template example: asynchronous

If you're using asynchronous code, out parameters aren't allowed. In this case, use `IAsyncCollector`

to return your template notification. The following code is an asynchronous example of the previous example:

```
using System;
using System.Threading.Tasks;
using System.Collections.Generic;
public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
log.Info($"Sending Template Notification to Notification Hub");
await notification.AddAsync(GetTemplateProperties(myQueueItem));
}
private static IDictionary<string, string> GetTemplateProperties(string message)
{
Dictionary<string, string> templateProperties = new Dictionary<string, string>();
templateProperties["user"] = "A new user wants to be added : " + message;
return templateProperties;
}
```


### C# script template example: JSON

This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages) that contains a `message`

placeholder in the template using a valid JSON string:

```
using System;
public static void Run(string myQueueItem, out string notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```


### C# script template example: library types

This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/):

```
#r "Microsoft.Azure.NotificationHubs"
using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;
public static void Run(string myQueueItem, out Notification notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
notification = GetTemplateNotification(myQueueItem);
}
private static TemplateNotification GetTemplateNotification(string message)
{
Dictionary<string, string> templateProperties = new Dictionary<string, string>();
templateProperties["message"] = message;
return new TemplateNotification(templateProperties);
}
```


### F# template example

This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages) that contains `location`

and `message`

:

```
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```


### JavaScript template example

This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages) that contains `location`

and `message`

:

```
module.exports = async function (context, myTimer) {
var timeStamp = new Date().toISOString();
if (myTimer.IsPastDue)
{
context.log('Node.js is running late!');
}
context.log('Node.js timer trigger function ran!', timeStamp);
context.bindings.notification = {
location: "Redmond",
message: "Hello from Node!"
};
};
```


## Example: APNS native

This C# script example shows how to send a native Apple Push Notification Service (APNS) notification:

```
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"
using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;
public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
// In this example, the queue item is a new user to be processed in the form of a JSON string with
// a "name" value.
//
// The JSON format for a native Apple Push Notification Service (APNS) notification is:
// { "aps": { "alert": "notification message" }}
log.LogInformation($"Sending APNS notification of a new user");
dynamic user = JsonConvert.DeserializeObject(myQueueItem);
string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" +
user.name + ")\" }}";
log.LogInformation($"{apnsNotificationPayload}");
await notification.AddAsync(new AppleNotification(apnsNotificationPayload));
}
```


## Example: WNS native

This C# script example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native Windows Push Notification Service (WNS) toast notification:

```
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"
using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;
public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
// In this example, the queue item is a new user to be processed in the form of a JSON string with
// a "name" value.
//
// The XML format for a native WNS toast notification is ...
// <?xml version="1.0" encoding="utf-8"?>
// <toast>
// <visual>
// <binding template="ToastText01">
// <text id="1">notification message</text>
// </binding>
// </visual>
// </toast>
log.Info($"Sending WNS toast notification of a new user");
dynamic user = JsonConvert.DeserializeObject(myQueueItem);
string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
"<toast><visual><binding template=\"ToastText01\">" +
"<text id=\"1\">" +
"A new user wants to be added (" + user.name + ")" +
"</text>" +
"</binding></visual></toast>";
log.Info($"{wnsNotificationPayload}");
await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));
}
```


## Attributes

In [C# class libraries](functions-dotnet-class-library), use the [NotificationHub](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) attribute.

The attribute's constructor parameters and properties are described in the [Configuration](#configuration) section.

## Configuration

The following table lists the binding configuration properties that you set in the *function.json* file and the `NotificationHub`

attribute:

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Set to `notificationHub` . |
direction |
n/a | Set to `out` . |
name |
n/a | Variable name used in function code for the notification hub message. |
tagExpression |
TagExpression |
Tag expressions allow you to specify that notifications be delivered to a set of devices that are registered to receive notifications matching the tag expression. For more information, see
|

**hubName****HubName****connection****ConnectionStringSetting***DefaultFullSharedAccessSignature*value for your notification hub. For more information, see[Connection string setup](#connection-string-setup).**platform****Platform**[Notification Hubs templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages). When**platform**is set, it must be one of the following values:`apns`

: Apple Push Notification Service. For more information on configuring the notification hub for APNS and receiving the notification in a client app, see[Send push notifications to .NET MAUI apps using Azure Notification Hubs via a backend service](/en-us/dotnet/maui/data-cloud/push-notifications).`adm`

:[Amazon Device Messaging](https://developer.amazon.com/device-messaging). For more information on configuring the notification hub for Azure Deployment Manager (ADM) and receiving the notification in a Kindle app, see[Send push notifications to Android devices using Firebase SDK](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started).`wns`

:[Windows Push Notification Services](/en-us/windows/uwp/design/shell/tiles-and-notifications/windows-push-notification-services--wns--overview)targeting Windows platforms. WNS also supports Windows Phone 8.1 and later. For more information, see[Send notifications to Universal Windows Platform apps using Azure Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification).`mpns`

:[Microsoft Push Notification Service](/en-us/previous-versions/windows/apps/ff402558(v=vs.105)). This platform supports Windows Phone 8 and earlier Windows Phone platforms. For more information, see[Send notifications to Universal Windows Platform apps using Azure Notification Hubs](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns).

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

### function.json file example

Here's an example of a Notification Hubs binding in a *function.json* file:

```
{
"bindings": [
{
"type": "notificationHub",
"direction": "out",
"name": "notification",
"tagExpression": "",
"hubName": "my-notification-hub",
"connection": "MyHubConnectionString",
"platform": "apns"
}
],
"disabled": false
}
```


### Connection string setup

To use a notification hub output binding, you must configure the connection string for the hub.

Important

The Notification Hubs binding doesn't support Microsoft Entra authentication and managed identities. You can use Azure Key Vault to centrally manage your notification hub connection string and help with key rotation. To learn more, see [Manage Connections](manage-connections).

You can select an existing notification hub or create a new one from the **Integrate** tab in the Azure portal. You can also configure the connection string manually.

To configure the connection string to an existing notification hub:

Navigate to your notification hub in the

[Azure portal](https://portal.azure.com), choose**Access policies**, and select the copy button next to the**DefaultFullSharedAccessSignature**policy.The connection string for the

*DefaultFullSharedAccessSignature*policy is copied to your notification hub. This connection string lets your function send notification messages to the hub.Navigate to your function app in the Azure portal, expand

**Settings**, and then select**Environment variables**.From the

**App setting**tab, select**+ Add**to add a key such as**MyHubConnectionString**. The**Name**of this app setting is the output binding connection setting in*function.json*or the .NET attribute. For more information, see[Configuration](#configuration).For the value, paste the copied

*DefaultFullSharedAccessSignature*connection string from your notification hub, and then select**Apply**.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Notification Hub |
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/performance-reliability -->

# Improve the performance and reliability of Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance to improve the performance and reliability of your [serverless](https://azure.microsoft.com/solutions/serverless/) function apps. For a more general set of Azure Functions best practices, see [Azure Functions best practices](functions-best-practices).

The following are best practices in how you build and architect your serverless solutions using Azure Functions.

## Avoid long running functions

Large, long-running functions can cause unexpected timeout issues. To learn more about the timeouts for a given hosting plan, see [function app timeout duration](functions-scale#timeout).

A function can become large because of many Node.js dependencies. Importing dependencies can also cause increased load times that result in unexpected timeouts. Dependencies are loaded both explicitly and implicitly. A single module loaded by your code may load its own additional modules.

Whenever possible, refactor large functions into smaller function sets that work together and return responses fast. For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it's common for webhooks to require an immediate response. You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function. This approach lets you defer the actual work and return an immediate response.

## Make sure background tasks complete

When your function starts any tasks, callbacks, threads, processes, they must complete before your function code returns. Because Functions doesn't track these background threads, site shutdown can occur regardless of background thread status, which can cause unintended behavior in your functions.

For example, if a function starts a background task and returns a successful response before the task completes, the Functions runtime considers the execution as having completed successfully, regardless of the result of the background task. If this background task is performing essential work, it may be preempted by site shutdown, leaving that work in an unknown state.

## Cross function communication

[Durable Functions](durable/durable-functions-overview) and [Azure Logic Apps](../logic-apps/logic-apps-overview) are built to manage state transitions and communication between multiple functions.

If not using Durable Functions or Logic Apps to integrate with multiple functions, it's best to use storage queues for cross-function communication. The main reason is that storage queues are cheaper and much easier to provision than other storage options.

Individual messages in a storage queue are limited in size to 64 KB. If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB in the Standard tier, and up to 100 MB in the Premium tier.

Service Bus topics are useful if you require message filtering before processing.

Event hubs are useful to support high volume communications.

## Write functions to be stateless

Functions should be stateless and idempotent if possible. Associate any required state information with your data. For example, an order being processed would likely have an associated `state`

member. A function could process an order based on that state while the function itself remains stateless.

Idempotent functions are especially recommended with timer triggers. For example, if you have something that absolutely must run once a day, write it so it can run anytime during the day with the same results. The function can exit when there's no work for a particular day. Also if a previous run failed to complete, the next run should pick up where it left off. This is particularly important for message-based bindings that retry on failure. For more information, see [Designing Azure Functions for identical input](functions-idempotent).

## Write defensive functions

Assume your function could encounter an exception at any time. Design your functions with the ability to continue from a previous fail point during the next execution. Consider a scenario that requires the following actions:

- Query for 10,000 rows in a database.
- Create a queue message for each of those rows to process further down the line.

Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time. You need to design your functions to be prepared for it.

How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing? Track items in a set that you’ve completed. Otherwise, you might insert them again next time. This double-insertion can have a serious impact on your work flow, so [make your functions idempotent](functions-idempotent).

If a queue item was already processed, allow your function to be a no-op.

Take advantage of defensive measures already provided for components you use in the Azure Functions platform. For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers and bindings](functions-bindings-storage-queue-trigger#poison-messages).

For HTTP based functions consider [API versioning strategies](/en-us/azure/architecture/reference-architectures/serverless/web-app#api-versioning) with Azure API Management. For example, if you have to update your HTTP based function app, deploy the new update to a separate function app and use API Management revisions or versions to direct clients to the new version or revision. Once all clients are using the version or revision and no more executions are left on the previous function app, you can deprovision the previous function app.

## Function organization best practices

As part of your solution, you may develop and publish multiple functions. These functions are often combined into a single function app, but they can also run in separate function apps. In Premium and dedicated (App Service) hosting plans, multiple function apps can also share the same resources by running in the same plan. How you group your functions and function apps can impact the performance, scaling, configuration, deployment, and security of your overall solution. There aren't rules that apply to every scenario, so consider the information in this section when planning and developing your functions.

### Organize functions for performance and scaling

Each function that you create has a memory footprint. While this footprint is usually small, having too many functions within a function app can lead to slower startup of your app on new instances. It also means that the overall memory usage of your function app might be higher. It's hard to say how many functions should be in a single app, which depends on your particular workload. However, if your function stores a lot of data in memory, consider having fewer functions in a single app.

If you run multiple function apps in a single Premium plan or dedicated (App Service) plan, these apps are all sharing the same resources allocated to the plan. If you have one function app that has a much higher memory requirement than the others, it uses a disproportionate amount of memory resources on each instance to which the app is deployed. Because this could leave less memory available for the other apps on each instance, you might want to run a high-memory-using function app like this in its own separate hosting plan.

Note

When using the [Consumption plan](functions-scale), we recommend you always put each app in its own plan, since apps are scaled independently anyway. For more information, see [Multiple apps in the same plan](consumption-plan#multiple-apps-in-the-same-plan).

Consider whether you want to group functions with different load profiles. For example, if you have a function that processes many thousands of queue messages, and another that is only called occasionally but has high memory requirements, you might want to deploy them in separate function apps so they get their own sets of resources and they scale independently of each other.

### Organize functions for configuration and deployment

Function apps have a `host.json`

file, which is used to configure advanced behavior of function triggers and the Azure Functions runtime. Changes to the `host.json`

file apply to all functions within the app. If you have some functions that need custom configurations, consider moving them into their own function app.

All functions in your local project are deployed together as a set of files to your function app in Azure. You might need to deploy individual functions separately or use features like [deployment slots](functions-deployment-slots) for some functions and not others. In such cases, you should deploy these functions (in separate code projects) to different function apps.

### Organize functions by privilege

Connection strings and other credentials stored in application settings gives all of the functions in the function app the same set of permissions in the associated resource. Consider minimizing the number of functions with access to specific credentials by moving functions that don't use those credentials to a separate function app. You can always use techniques such as [function chaining](/en-us/training/modules/chain-azure-functions-data-using-bindings/) to pass data between functions in different function apps.

## Scalability best practices

There are a number of factors that impact how instances of your function app scale. The details are provided in the documentation for [function scaling](functions-scale). The following are some best practices to ensure optimal scalability of a function app.

### Share and manage connections

Reuse connections to external resources whenever possible. See [how to manage connections in Azure Functions](manage-connections).

### Avoid sharing storage accounts

When you create a function app, you must associate it with a storage account. The storage account connection is maintained in the [AzureWebJobsStorage application setting](functions-app-settings#azurewebjobsstorage).

To maximize performance, use a separate storage account for each function app. This approach is particularly important when you have Durable Functions or Event Hubs triggered functions, which both generate a high volume of storage transactions. When your application logic interacts with Azure Storage, either directly (using the Storage SDK) or through one of the storage bindings, you should use a dedicated storage account. For example, if you have an event hub-triggered function writing some data to blob storage, use two storage accounts: one for the function app and another for the blobs that the function stores.

### Don't mix test and production code in the same function app

Functions within a function app share resources. For example, memory is shared. If you're using a function app in production, don't add test-related functions and resources to it. It can cause unexpected overhead during production code execution.

Be careful what you load in your production function apps. Memory is averaged across each function in the app.

If you have a shared assembly referenced in multiple .NET functions, put it in a common shared folder. Otherwise, you could accidentally deploy multiple versions of the same binary that behave differently between functions.

Don't use verbose logging in production code, which has a negative performance impact.

### Use async code but avoid blocking calls

Asynchronous programming is a recommended best practice, especially when blocking I/O operations are involved.

In C#, always avoid referencing the `Result`

property or calling `Wait`

method on a `Task`

instance. This approach can lead to thread exhaustion.

Tip

If you plan to use the HTTP or WebHook bindings, plan to avoid port exhaustion that can be caused by improper instantiation of `HttpClient`

. For more information, see [How to manage connections in Azure Functions](manage-connections).

### Use multiple worker processes

By default, any host instance for Functions uses a single worker process. To improve performance, especially with single-threaded runtimes like Python, use the [FUNCTIONS_WORKER_PROCESS_COUNT](functions-app-settings#functions_worker_process_count) to increase the number of worker processes per host (up to 10). Azure Functions then tries to evenly distribute simultaneous function invocations across these workers.

The FUNCTIONS_WORKER_PROCESS_COUNT applies to each host that Functions creates when scaling out your application to meet demand.

### Receive messages in batch whenever possible

Some triggers like Event Hub enable receiving a batch of messages on a single invocation. Batching messages has much better performance. You can configure the max batch size in the `host.json`

file as detailed in the [host.json reference documentation](functions-host-json)

For C# functions, you can change the type to a strongly-typed array. For example, instead of `EventData sensorEvent`

the method signature could be `EventData[] sensorEvent`

. For other languages, you'll need to explicitly set the cardinality property in your `function.json`

to `many`

in order to enable batching [as shown here](https://github.com/Azure/azure-webjobs-sdk-templates/blob/df94e19484fea88fc2c68d9f032c9d18d860d5b5/Functions.Templates/Templates/EventHubTrigger-JavaScript/function.json#L10).

### Configure host behaviors to better handle concurrency

The `host.json`

file in the function app allows for configuration of host runtime and trigger behaviors. In addition to batching behaviors, you can manage concurrency for a number of triggers. Often adjusting the values in these options can help each instance scale appropriately for the demands of the invoked functions.

Settings in the host.json file apply across all functions within the app, within a *single instance* of the function. For example, if you had a function app with two HTTP functions and [ maxConcurrentRequests](functions-bindings-http-webhook#hostjson-settings) requests set to 25, a request to either HTTP trigger would count towards the shared 25 concurrent requests. When that function app is scaled to 10 instances, the ten functions effectively allow 250 concurrent requests (10 instances * 25 concurrent requests per instance).

Other host configuration options are found in the [host.json configuration article](functions-host-json).

## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redispubsub -->

# RedisPubSubTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Redis features [publish/subscribe functionality](https://redis.io/docs/latest/commands/pubsub/) that enables messages to be sent to Redis and broadcast to subscribers.

For more information about Azure Cache for Redis triggers and bindings, [Redis Extension for Azure Functions](https://github.com/Azure/azure-functions-redis-extension/tree/main).

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Pub/Sub Trigger | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Warning

This trigger isn't supported on a [Consumption plan](/en-us/azure/azure-functions/consumption-plan) or a [Flex Consumption plan](/en-us/azure/azure-functions/flex-consumption-plan) plan because Redis PubSub requires clients to always be actively listening to receive all messages. For consumption plans, your function might miss certain messages published to the channel.

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Examples

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

This sample listens to the channel `pubsubTest`

.

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisPubSubTrigger
{
internal class SimplePubSubTrigger
{
private readonly ILogger<SimplePubSubTrigger> logger;
public SimplePubSubTrigger(ILogger<SimplePubSubTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimplePubSubTrigger))]
public void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "pubsubTest")] string message)
{
logger.LogInformation(message);
}
}
}
```


This sample listens to any keyspace notifications for the key `keyspaceTest`

.

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisPubSubTrigger
{
internal class KeyspaceTrigger
{
private readonly ILogger<KeyspaceTrigger> logger;
public KeyspaceTrigger(ILogger<KeyspaceTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(KeyspaceTrigger))]
public void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyspace@0__:keyspaceTest")] string message)
{
logger.LogInformation(message);
}
}
}
```


This sample listens to any `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisPubSubTrigger
{
internal class KeyeventTrigger
{
private readonly ILogger<KeyeventTrigger> logger;
public KeyeventTrigger(ILogger<KeyeventTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(KeyeventTrigger))]
public void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyevent@0__:del")] string message)
{
logger.LogInformation($"Key '{message}' deleted.");
}
}
}
```


This sample listens to the channel `pubsubTest`

.

```
package com.function.RedisPubSubTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimplePubSubTrigger {
@FunctionName("SimplePubSubTrigger")
public void run(
@RedisPubSubTrigger(
name = "req",
connection = "redisConnectionString",
channel = "pubsubTest",
pattern = false)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample listens to any keyspace notifications for the key `myKey`

.

```
package com.function.RedisPubSubTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class KeyspaceTrigger {
@FunctionName("KeyspaceTrigger")
public void run(
@RedisPubSubTrigger(
name = "req",
connection = "redisConnectionString",
channel = "__keyspace@0__:keyspaceTest",
pattern = false)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample listens to any `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
package com.function.RedisPubSubTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class KeyeventTrigger {
@FunctionName("KeyeventTrigger")
public void run(
@RedisPubSubTrigger(
name = "req",
connection = "redisConnectionString",
channel = "__keyevent@0__:del",
pattern = false)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample uses the same `index.js`

file, with binding data in the `function.json`

file determining on which channel the trigger occurs.

Here's the `index.js`

file:

```
module.exports = async function (context, message) {
context.log(message);
}
```


From `function.json`

:

Here's binding data to listen to the channel `pubsubTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "pubsubTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


Here's binding data to listen to keyspace notifications for the key `keyspaceTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyspace@0__:keyspaceTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


Here's binding data to listen to `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:del",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This sample uses the same `run.ps1`

file, with binding data in the `function.json`

file determining on which channel the trigger occurs.

Here's the `run.ps1`

file:

```
param($message, $TriggerMetadata)
Write-Host $message
```


From `function.json`

:

Here's binding data to listen to the channel `pubsubTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "pubsubTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


Here's binding data to listen to keyspace notifications for the key `keyspaceTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyspace@0__:keyspaceTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


Here's binding data to listen to `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:del",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file determining on which channel the trigger occurs.

Here's the `__init__.py`

file:

```
import logging
def main(message: str):
logging.info(message)
```


From `function.json`

:

Here's binding data to listen to the channel `pubsubTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "pubsubTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


Here's binding data to listen to keyspace notifications for the key `keyspaceTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyspace@0__:keyspaceTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


Here's binding data to listen to `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:del",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


## Attributes

| Parameter | Description | Required | Default |
|---|---|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Channel`

`INameResolver`

.## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
Name of the variable holding the value returned by the function. | Yes | |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`channel`

## Configuration

| function.json property | Description | Required | Default |
|---|---|---|---|
`type` |
Trigger type. For the pub sub trigger, the type is `redisPubSubTrigger` . |
Yes | |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`channel`

`pattern`

`pattern`

is true, then the channel is treated like a *glob-style*pattern instead of as a literal.`name`

`direction`

`in`

.Important

The `connection`

parameter does not hold the Redis cache connection string itself. Instead, it points to the name of the environment variable that holds the connection string. This makes the application more secure. For more information, see [Redis connection string](functions-bindings-cache#redis-connection-string).

## Usage

Redis features [publish/subscribe functionality](https://redis.io/docs/latest/commands/pubsub/) that enables messages to be sent to Redis and broadcast to subscribers. The `RedisPubSubTrigger`

enables Azure Functions to be triggered on pub/sub activity. The `RedisPubSubTrigger`

subscribes to a specific channel pattern using [ PSUBSCRIBE](https://redis.io/commands/psubscribe/), and surfaces messages received on those channels to the function.

### Prerequisites and limitations

- The
`RedisPubSubTrigger`

isn't capable of listening to[keyspace notifications](https://redis.io/docs/latest/develop/pubsub/keyspace-notifications/)on clustered caches. - Basic tier functions don't support triggering on
`keyspace`

or`keyevent`

notifications through the`RedisPubSubTrigger`

. - The
`RedisPubSubTrigger`

isn't supported on a[Consumption plan](/en-us/azure/azure-functions/consumption-plan)or a[Flex Consumption plan](/en-us/azure/azure-functions/flex-consumption-plan)because Redis PubSub requires clients to always be actively listening to receive all messages. For consumption plans, your function might miss certain messages published to the channel. - Functions with the
`RedisPubSubTrigger`

shouldn't be scaled out to multiple instances. Each instance listens and processes each pub sub message, resulting in duplicate processing.

Warning

This trigger isn't supported on a [Consumption plan](/en-us/azure/azure-functions/consumption-plan) or a [Flex Consumption plan](/en-us/azure/azure-functions/flex-consumption-plan) because Redis PubSub requires clients to always be actively listening to receive all messages. For consumption plans, your function might miss certain messages published to the channel.

## Triggering on keyspace notifications

Redis offers a built-in concept called [keyspace notifications](https://redis.io/docs/latest/develop/pubsub/keyspace-notifications/). When enabled, this feature publishes notifications of a wide range of cache actions to a dedicated pub/sub channel. Supported actions include actions that affect specific keys, called *keyspace notifications*, and specific commands, called *keyevent notifications*. A huge range of Redis actions are supported, such as `SET`

, `DEL`

, and `EXPIRE`

. The full list can be found in the [keyspace notification documentation](https://redis.io/docs/latest/develop/pubsub/keyspace-notifications/).

The `keyspace`

and `keyevent`

notifications are published with the following syntax:

```
PUBLISH __keyspace@0__:<affectedKey> <command>
PUBLISH __keyevent@0__:<affectedCommand> <key>
```


Because these events are published on pub/sub channels, the `RedisPubSubTrigger`

is able to pick them up. See the [RedisPubSubTrigger](functions-bindings-cache-trigger-redispubsub) section for more examples.

Important

In Azure Cache for Redis, `keyspace`

events must be enabled before notifications are published. For more information, see [Advanced Settings](/en-us/azure/azure-cache-for-redis/cache-configure#keyspace-notifications-advanced-settings).

| Type | Description |
|---|---|
`string` |
The channel message serialized as JSON (UTF-8 encoded for byte types) in the format that follows. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel into the given custom type. |

JSON string format

```
{
"SubscriptionChannel":"__keyspace@0__:*",
"Channel":"__keyspace@0__:mykey",
"Message":"set"
}
```


| Type | Description |
|---|---|
`string` |
The channel message serialized as JSON (UTF-8 encoded for byte types) in the format that follows. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |

```
{
"SubscriptionChannel":"__keyspace@0__:*",
"Channel":"__keyspace@0__:mykey",
"Message":"set"
}
```

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
