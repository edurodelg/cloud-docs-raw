---
merged_at: 2026-01-26T21:02:36.358029
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: migrate-aws-lambda-to-azure-functions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/migration/migrate-aws-lambda-to-azure-functions -->

# Migrate AWS Lambda workloads to Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Migrating a serverless workload that uses Amazon Web Services (AWS) Lambda to Azure Functions requires careful planning and implementation. This article provides essential guidance to help you:

- Perform a discovery process on your existing workload.
- Learn how to perform key migration activities like premigration planning and workload assessment.
- Evaluate and optimize a migrated workload.

## Scope

This article describes the migration of an AWS Lambda instance to Azure Functions.

This article doesn't address:

- Migration to your own container hosting solution, such as through Azure Container Apps.
- Hosting AWS Lambda containers in Azure.
- Fundamental Azure adoption approaches by your organization, such as
[Azure landing zones](/en-us/azure/cloud-adoption-framework/ready/landing-zone/)or other topics addressed in the Cloud Adoption Framework[migrate methodology](/en-us/azure/cloud-adoption-framework/migrate/).

## Migration custom chat mode

To make it easier to migrate your AWS Lambda apps to Azure using Visual Studio Code, Azure Functions provides a [custom chat mode](https://code.visualstudio.com/docs/copilot/customization/custom-chat-modes) in GitHub Copilot. Use these steps to add the `LambdaToFunctionMigration`

custom chat mode to your project in Visual Studio Code:

If you don't already have the

[GitHub Copilot for Azure](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot)Visual Studio Code extension, install it now.Open your Lambda project as a workspace in Visual Studio Code.

Run this prompt in

**Agent**mode in GitHub Copilot:`Help me migrate my Lambda app to Azure`

When prompted in the notification area, select

**Install**to add the`LambdaToFunctionMigration`

custom chat mode to your project.

You can now use guided prompts defined in this custom chat for each stage of your migration. Start typing `/LambdaMigration`

in chat to see the complete list of available commands.

### Compare functionality

This article maps AWS Lambda features to Azure Functions equivalents to help ensure compatibility.

Important

You might choose to include optimization in your migration plan, but Microsoft recommends a two-step process. Migrate "like-to-like" functionalities first, and then evaluate optimization opportunities on Azure.

Optimization efforts should be continuous and run through your workload team's change control processes. A migration that adds more capabilities during a migration incurs risk and unnecessarily extends the process.

### Workload perspective

This article focuses on how to migrate an AWS Lambda workload to Azure Functions and the common dependencies for serverless workloads. This process might involve several services because workloads comprise many resources and processes to manage those resources. To have a comprehensive strategy, you must combine the recommendations presented in this article with a larger plan that includes the other components and processes in your workload.

## Perform a discovery process on your existing workload

The first step is to conduct a detailed discovery process to evaluate your existing AWS Lambda workload. The goal is to understand which AWS features and services your workload relies on. Compile a comprehensive inventory of your AWS Lambda functions by using AWS tooling like service-specific SDKs, APIs, CloudTrail, and AWS CLI to assess the workload on AWS. You should understand the following key aspects of your AWS Lambda inventory:

- Use cases
- Configurations
- Security and networking setups
- Tooling, monitoring, logging, and observability mechanisms
- Dependencies
- Reliability objectives and current reliability status
- Cost of ownership
- Performance targets and current performance

Tip

Use this custom chat mode prompt to generate an assessment report for your AWS Lambda setup:

```
/LambdaMigration-Phase1-AssessLambdaProject
```


## Perform premigration planning

Before you start migrating your workload, you must map AWS Lambda features to Azure Functions to ensure compatibility and develop a migration plan. Then you can select key workloads for a proof of concept.

You also need to [map the AWS services](/en-us/azure/architecture/aws-professional) that Lambda depends on to the equivalent dependencies in Azure.

## Map AWS Lambda features to Azure Functions

The following tables compare AWS Lambda concepts, resources, and properties with their corresponding equivalents on Azure Functions, specifically, the Flex Consumption hosting plan.

[Supported languages](#supported-languages)[Programming model](#programming-model)[Event triggers and bindings](#event-triggers-and-bindings)[Permissions](#permissions)[Function URL](#function-url)[Networking](#networking)[Observability and monitoring](#observability-and-monitoring)[Scaling and concurrency](#scaling-and-concurrency)[Cold-start protection](#cold-start-protection)[Pricing](#pricing)[Source code storage](#source-code-storage)[Local development](#local-development)[Deployment](#deployment)[Time-out and memory limits](#time-out-and-memory-limits)[Secret management](#secret-management)[State management](#state-management)[Stateful orchestration](#stateful-orchestration)[Other differences and considerations](#other-differences-and-considerations)

### Supported languages

| Programming language |
|
|---|

[Azure Functions supported versions](/en-us/azure/azure-functions/supported-languages)

[Custom handlers](/en-us/azure/azure-functions/functions-custom-handlers)[OS-only runtime](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-provided.html)[Custom handlers](/en-us/azure/azure-functions/functions-custom-handlers)[OS-only runtime](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-provided.html)[Custom handlers](/en-us/azure/azure-functions/functions-custom-handlers)### Programming model

| Feature | AWS Lambda | Azure Functions |
|---|---|---|
| Triggers | Integrates with other AWS services via event sources. Provides automatic and programmatic ways to link Lambda functions with event sources. | Triggers a function based on specific events, such as updates in a database or a new message in a queue. For example, an Azure Cosmos DB trigger allows functions to automatically respond to inserts and updates in an Azure Cosmos DB container. This action enables real-time processing of data changes. Functions also integrates with Azure Event Grid, so it can process events from Azure services, like Azure Storage and Azure Media Services, and external event sources. Event Grid serves as a centralized, extensible event routing service that complements Functions triggers and enables high scalability and broad event-source coverage. |
| Bindings | Doesn't have bindings. Uses AWS SDKs within Lambda functions to manually manage interactions with other AWS services. | Bindings, configured as input or output, enable declarative connections to services, which minimize the need for explicit SDK code. For example, you can configure bindings to read from Blob Storage, write to Azure Cosmos DB, or send emails via SendGrid without manually managing the integrations. |

### Event triggers and bindings

| AWS Lambda trigger or service |
|
|---|

[HTTP trigger](/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger)[Azure Queue Storage trigger](/en-us/azure/azure-functions/functions-bindings-storage-queue-trigger)or[Azure Service Bus trigger](/en-us/azure/azure-functions/functions-bindings-service-bus-trigger)[Event Grid trigger](/en-us/azure/azure-functions/functions-bindings-event-grid-trigger)or[Service Bus trigger](/en-us/azure/azure-functions/functions-bindings-service-bus-trigger)[Event Hubs trigger](/en-us/azure/azure-functions/functions-bindings-event-hubs-trigger)[Azure Cosmos DB change feed trigger](/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-trigger)[Timer trigger](/en-us/azure/azure-functions/functions-bindings-timer)[Blob Storage trigger](/en-us/azure/azure-functions/functions-bindings-storage-blob-trigger)[Azure SQL trigger](/en-us/azure/azure-functions/functions-bindings-azure-sql-trigger)[Apache Kafka trigger](/en-us/azure/azure-functions/functions-bindings-kafka-trigger)[Azure Redis trigger](/en-us/azure/azure-functions/functions-bindings-cache)[RabbitMQ trigger](/en-us/azure/azure-functions/functions-bindings-rabbitmq-trigger)### Permissions

| AWS Lambda | Azure Functions |
|---|---|
| The Lambda execution role grants Lambda functions permissions to interact with other AWS services. Each Lambda function has an associated identity and access management (IAM) role that determines its permissions while it runs. | Managed identities provide an identity for your function app that allows it to authenticate with other Azure services without storing credentials in the code. Role-based access control assigns appropriate roles to the managed identity in Microsoft Entra ID to grant access to the resources that it requires. |
| Resource-based policy statements: - AWSLambda_FullAccess gives full access to all Lambda operations, including creating, updating, and deleting functions. - AWSLambda_ReadOnlyAccess gives read-only access to view Lambda functions and their configurations. - Custom IAM policies. |
Resource-based built-in roles: - The Owner role gives full access, including access permissions management. - The Contributor role can create and delete function apps, configure settings, and deploy code. It can't manage access. - The Monitoring Reader role can grant read-only access to monitoring data and settings. It can also allocate custom roles. |

### Function URL

| AWS Lambda | Azure Functions |
|---|---|
`https://<url-id>.lambda-url.<region>.on.aws` |
- `<appname>.azurewebsites.net` (original, global default hostname) - `<appname>-<randomhash>.<Region>.azurewebsites.net` (new, unique default hostname) |

### Networking

| AWS Lambda | Azure Functions |
|---|---|
| All Lambda functions run securely inside a default system-managed virtual private cloud (VPC). You can also configure your Lambda function to access resources in a custom VPC. | Function apps can be network secured and can access other services inside the network. Inbound network access can be restricted to only a firewall list of IP addresses and to a specific virtual network via service endpoints or private endpoints. Outbound network access is enabled through the virtual network integration feature. The function app can have all its traffic restricted to a virtual network's subnet and can also access other services inside that virtual network. |

### Observability and monitoring

| AWS Lambda | Azure Functions |
|---|---|
| Amazon CloudWatch helps with monitoring and observability by collecting and tracking metrics, aggregating and analyzing logs, setting alarms, creating custom dashboards, and implementing automated responses to changes in resource performance and metrics. | Azure Monitor provides comprehensive monitoring and observability for Azure Functions, particularly through its Application Insights feature. Application Insights collects telemetry data such as request rates, response times, and failure rates. It visualizes application component relationships, monitors real-time performance, logs detailed diagnostics, and allows custom metric tracking. These capabilities help maintain the performance, availability, and reliability of Azure Functions, while enabling custom dashboards, alerts, and automated responses. |
| AWS Lambda generates telemetry data from your function invocations and can export this data by using OpenTelemetry semantics. You can configure your Lambda functions to send this telemetry data to any OpenTelemetry-compliant endpoint. This action allows for correlation of traces and logs, consistent standards-based telemetry data, and integration with other observability tools that support OpenTelemetry. | Configure your functions app to export log and trace data in an OpenTelemetry format. You can export telemetry data to any compliant endpoint by using OpenTelemetry. OpenTelemetry provides benefits such as correlation of traces and logs, consistent standards-based telemetry data, and integration with other providers. You can enable OpenTelemetry at the function app level in the host configuration and in your code project to optimize data exportation from your function code. For more information, see
|

### Scaling and concurrency

| AWS Lambda | Azure Functions |
|---|---|
| AWS uses an on-demand scaling model. Automatically scale your function operation in response to demand. Concurrency, or the number of requests handled by an instance, is always 1. | Instances are dynamically added and removed based on the number of incoming events and the configured concurrency for each instance. You can configure the
|

### Cold-start protection

| AWS Lambda | Azure Functions |
|---|---|
| Provisioned concurrency reduces latency and ensures predictable function performance by pre-initializing a requested number of function instances. Provisioned concurrency suits latency-sensitive applications and is priced separately from standard concurrency. | Function apps allow you to configure concurrency for each instance, which drives its scale. Multiple jobs can run in parallel in the same instance of the app, and subsequent jobs in the instance don't incur the initial cold start. Function apps also have always ready instances. Customers can specify a number of prewarmed instances to eliminate cold-start latency and ensure consistent performance. Function apps also scale out to more instances based on demand, while maintaining the always ready instances. |
| Reserved concurrency specifies the maximum number of concurrent instances that a function can have. This limit ensures that a portion of your account's concurrency quota is set aside exclusively for that function. AWS Lambda dynamically scales out to handle incoming requests even when reserved concurrency is set, as long as the requests don't exceed the specified reserved concurrency limit. The lower limit for reserved concurrency in AWS Lambda is 1. The upper limit for reserved concurrency in AWS Lambda is determined by the account's regional concurrency quota. By default, this limit is 1,000 concurrent operations for each region. | Azure Functions doesn't have an equivalent feature to reserved concurrency. To achieve similar functionality, isolate specific functions into separate function apps and set the maximum scale-out limit for each app. Azure Functions dynamically scales out, or adds more instances, and scales in, or removes instances, within the scale-out limit set. By default, apps that run in a Flex Consumption plan start with a configurable limit of 100 overall instances. The lowest maximum instance count value is 40, and the highest supported maximum instance count value is 1,000.
|

### Pricing

| AWS Lambda | Azure Functions |
|---|---|
| - Pay per use for the total invocation count and for the GB/s for each instance (with a fixed concurrency of 1) - 1 ms increments - 400,000 Gbps free tier |
- Pay per use for the total invocation count and for the GB/s of each instance (with configurable concurrent invocations) - 100 ms increments - 100,000 Gbps free tier -
|

### Source code storage

| AWS Lambda | Azure Functions |
|---|---|
| AWS Lambda manages the storage of your function code in its own managed storage system. You don't need to supply more storage. | Functions requires a customer-supplied Blob Storage container to maintain the deployment package that contains your app's code. You can configure the settings to use the same or a different storage account for deployments and manage authentication methods for accessing the container. |

### Local development

| AWS Lambda feature | Azure Functions feature |
|---|---|
| - SAM CLI -
|
- Azure Functions Core Tools - Visual Studio Code - Visual Studio - GitHub Codespaces - VSCode.dev - Maven -
|

### Deployment

| Feature | AWS Lambda | Azure Functions |
|---|---|---|
| Deployment package | - ZIP file - Container image |
ZIP file (For container image deployment, use the dedicated or premium SKU.) |
| ZIP file size (console) | 50 MB maximum | 500 MB maximum for ZIP deployment |
| ZIP file size (CLI/SDK) | 250 MB maximum for ZIP deployment, 500 MB maximum for unzipped | 500 MB maximum for ZIP deployment |
| Container image size | 10 GB maximum | Container support with flexible storage via Azure |
| Large artifact handling | Use container images for larger deployments. | Attach Blob Storage or Azure Files shares to access large files from the app. |
| Packaging common dependencies to functions | Layers | Deployment .Zip, on demand from storage, or containers (ACA, dedicated, EP SKUs only) |
| Blue-green deployment or function versioning | Use function qualifiers to reference a specific state of your function by using either a version number or an alias name. Qualifiers enable version management and gradual deployment strategies. | Use continuous integration and continuous delivery systems for blue-green deployments. |

### Time-out and memory limits

| Feature | AWS Lambda limits | Azure Functions limits |
|---|---|---|
| Execution time-out | 900 seconds (15 minutes) | The default time-out is 30 minutes. The maximum time-out is unbounded. However, the grace period given to a function execution is 60 minutes during scale-in and 10 minutes during platform updates. For more information, see
|

[2-GB and 4-GB](/en-us/azure/azure-functions/functions-scale#service-limits)instance sizes. Each region in a given subscription has a memory limit of 512,000 MB for all instances of apps, which you can increase by calling support. The total memory usage of all instances across all function apps in a region must stay within this quota.Although 2 GB and 4 GB are the instance size options, the concurrency for each instance can be higher than 1. Therefore, a single instance can handle multiple concurrent executions, depending on the configuration. Configuring concurrency appropriately can help optimize resource usage and manage performance. By balancing memory allocation and concurrency settings, you can effectively manage the resources allocated to your function apps and ensure efficient performance and cost control. For more information, see

[Regional subscription memory quotas](/en-us/azure/azure-functions/flex-consumption-plan#regional-subscription-memory-quotas).### Secret management

| AWS Lambda | Azure Functions |
|---|---|
| AWS Secrets Manager allows you to store, manage, and retrieve secrets such as database credentials, API keys, and other sensitive information. Lambda functions can retrieve secrets by using the AWS SDK. | We recommend that you use secretless approaches like managed identities to enable secure access to Azure resources without hardcoding credentials. When secrets are required, such as for partner or legacy systems, Azure Key Vault provides a secure solution to store and manage secrets, keys, and certificates. |
| AWS Systems Manager Parameter Store is a service that stores configuration data and secrets. Parameters can be encrypted by using AWS KMS and retrieved by Lambda functions by using the AWS SDK. Lambda functions can store configuration settings in environment variables. Sensitive data can be encrypted with a KMS key for secure access. |
Azure Functions uses application settings to store configuration data. These settings map directly to environment variables for ease of use within the function. These settings can be encrypted and securely stored in the Azure App Service configuration. For more advanced scenarios, Azure App Configuration provides robust features for managing multiple configurations. It enables feature flagging and supports dynamic updates across services. |

### State management

| AWS Lambda | Azure Functions |
|---|---|
| AWS Lambda handles simple state management by using services like Amazon S3 for object storage, DynamoDB for fast and scalable NoSQL state storage, and SQS for message queue handling. These services ensure data persistence and consistency across Lambda function executions. | Azure Functions uses `AzureWebJobsStorage` to manage state by enabling bindings and triggers with Azure Storage services like Blob Storage, Queue Storage, and Table Storage. It allows functions to easily read and write state. For more complex state management, Durable Functions provides advanced workflow orchestration and state persistence capabilities by using Azure Storage. |

### Stateful orchestration

| AWS Lambda | Azure Functions |
|---|---|
| No native state orchestration. Use AWS Step Functions for workflows. | Durable Functions helps with complex state management by providing durable workflow orchestration and stateful entities. It enables long-running operations, automatic checkpointing, and reliable state persistence. These features enable building intricate workflows to ensure fault tolerance and scalability for stateful applications. |

### Other differences and considerations

| Feature | AWS Lambda | Azure Functions |
|---|---|---|
| Grouping functions | Each AWS Lambda function is an independent entity. | A function app serves as a container for multiple functions. It provides a shared execution context and configuration for the functions that it contains. Treating multiple functions as a single entity simplifies deployment and management. Functions also uses a per-function scaling strategy, where each function is scaled independently, except for HTTP, Blob Storage, and Durable Functions triggers. These triggered functions scale in their own groups. |
| Custom domains | Enabled via API Gateway | You can
|

[custom containers that run in an Container Apps environment](/en-us/azure/azure-functions/functions-how-to-custom-container).## Create a migration plan

Select key workloads for a proof of concept.

Start by selecting one to two medium-sized, noncritical workloads from your total inventory. These workloads serve as the foundation for your proof-of-concept migration. You can test the process and identify potential challenges without risking major disruption to your operations.

Test iteratively and gather feedback.

Tip

Use this custom chat mode prompt to check the current status of the migration process at any time:

`/LambdaMigration-GetStatus`

Use the proof of concept to gather feedback, identify gaps, and fine-tune the process before you scale to larger workloads. This iterative approach ensures that by the time you move to full-scale migration, you address potential challenges and refine the process.


## Build the migration assets

This step is a transitional development phase. During this phase, you build source code, infrastructure as code (IaC) templates, and deployment pipelines to represent the workload in Azure. You must adapt function code for compatibility and best practices before you can perform the migration.

[Adapt function code, configuration files, and infrastructure as code files](#adapt-function-code-configuration-files-and-infrastructure-as-code-files)Tip

Use this custom chat mode prompt to start the code migration process:

`/LambdaMigration-Phase2-MigrateLambdaCode`

[Adjust configuration settings](#adjust-configuration-settings)[Generate IaC files](#generate-iac-files)[Use tools for refactoring](#use-tools-for-refactoring)

### Adapt function code, configuration files, and infrastructure as code files

To update code for Azure Functions runtime requirements:

Modify your code to adhere to the Azure Functions programming model. For instance, adapt your function signatures to match the format that Azure Functions requires. For more information about function definition and execution context, see

[Azure Functions developer guides](/en-us/azure/azure-functions/functions-reference-node).Use the

[Azure Functions extensions bundle](/en-us/azure/azure-functions/functions-bindings-register)to handle various bindings and triggers that are similar to AWS services. For .NET applications, you should use the appropriate NuGet packages instead of the extensions bundle.Use the extensions bundle to integrate with other Azure services such as Azure Storage, Azure Service Bus, and Azure Cosmos DB without needing to manually configure each binding through SDKs. For more information, see

[Connect functions to Azure services by using bindings](/en-us/azure/azure-functions/add-bindings-existing-function)and[Azure Functions binding expression patterns](/en-us/azure/azure-functions/functions-bindings-expressions-patterns).

These snippets are examples of common SDK code. The AWS Lambda code maps to the corresponding triggers, bindings, or SDK code snippets in Azure Functions.

**Reading from Amazon S3 versus Azure Blob Storage**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const s3 = new AWS.S3();
exports.handler = async (event) => {
const params = {
Bucket: 'my-bucket',
Key: 'my-object.txt',
};
const data = await
s3.getObject(params).promise();
console.log('File content:',
data.Body.toString());
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.storageblob('blobTrigger', {
path: 'my-container/{blobName}',
connection: 'AzureWebJobsStorage',
}, async (context, myBlob) => {
context.log(`Blob content:
${myBlob.toString()}`);
});
```


**Writing to Amazon Simple Queue Service (SQS) versus Azure Queue Storage**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const sqs = new AWS.SQS();
exports.handler = async (event) => {
const params = {
QueueUrl:
'https://sqs.amazonaws.com/123456789012/MyQueue',
MessageBody: 'Hello, world!',
};
await
sqs.sendMessage(params).promise();
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.queue('queueTrigger', {
queueName: 'myqueue-items',
connection: 'AzureWebJobsStorage',
}, async (context, queueMessage) => {
context.log(`Queue message:
${queueMessage}`);
});
```


**Writing to DynamoDB versus Azure Cosmos DB**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const dynamoDb = new AWS.DynamoDB.DocumentClient();
exports.handler = async (event) => {
const params = {
TableName: 'my-table',
Key: { id: '123' },
};
const data = await dynamoDb.get(params).promise();
console.log('DynamoDB record:', data.Item);
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.cosmosDB('cosmosTrigger', {
connectionStringSetting: 'CosmosDBConnection',
databaseName: 'my-database',
containerName: 'my-container',
leaseContainerName: 'leases',
}, async (context, documents) => {
documents.forEach(doc => {
context.log(`Cosmos DB document: ${JSON.stringify(doc)}`);
});
});
```


**Amazon CloudWatch Events versus an Azure timer trigger**

AWS Lambda code (SDK)

```
exports.handler = async (event) => {
console.log('Scheduled event:', event);
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.timer('timerTrigger', { schedule: '0 */5 * * * *', // Runs every 5 minutes }, async (context, myTimer) => { if (myTimer.isPastDue) { context.log('Timer is running late!'); } context.log(Timer function executed at: ${new Date().toISOString()}); });
```


**Amazon Simple Notification Service (SNS) versus an Azure Event Grid trigger**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const sns = new AWS.SNS();
exports.handler = async (event) => {
const params = {
Message: 'Hello, Event Grid!',
TopicArn: 'arn:aws:sns:us-east-1:123456789012:MyTopic',
};
await sns.publish(params).promise();
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.eventGrid('eventGridTrigger', {},
async (context, eventGridEvent) => {
context.log(`Event Grid event:
${JSON.stringify(eventGridEvent)}`);
});
```


**Amazon Kinesis versus an Azure Event Hubs trigger**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const kinesis = new AWS.Kinesis();
exports.handler = async (event) => {
const records =
event.Records.map(record =>
Buffer.from(record.kinesis.data,
'base64').toString());
console.log('Kinesis records:', records);
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.eventHub('eventHubTrigger', {
connection: 'EventHubConnection',
eventHubName: 'my-event-hub',
}, async (context, eventHubMessages) =>
{
eventHubMessages.forEach(message =>
{
context.log(`Event Hub message:
${message}`);
});
});
```


See the following GitHub repositories to compare AWS Lambda code and Azure Functions code:

[AWS Lambda code](https://github.com/MadhuraBharadwaj-MSFT/TestLambda)[Azure Functions code](https://github.com/MadhuraBharadwaj-MSFT/TestAzureFunction)[Azure samples repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples), which includes starter, IaC, and end-to-end samples for Azure Functions

### Adjust configuration settings

Ensure that your function's time-out and [memory](/en-us/azure/azure-functions/flex-consumption-how-to#configure-instance-memory) settings are compatible with Azure Functions. For more information about configurable settings, see [host.json reference for Azure Functions](/en-us/azure/azure-functions/functions-host-json).

Follow the recommended best practices for permissions, access, networking, and deployment configurations.

#### Configure permissions

Follow best practices when you set up permissions on your function apps. For more information, see [Configure your function app and storage account with managed identity](https://eng.ms/docs/cloud-ai-platform/devdiv/serverless-paas-balam/serverless-paas-vikr/app-service-web-apps/app-service-team-documents/functionteamdocs/faqs/tutorial-secretless-mi#configure-your-function-app-and-storage-account-with-managed-identity).

**main.bicep**

```
// User-assigned managed identity that the function app uses to reach Storage and Service Bus
module processorUserAssignedIdentity './core/identity/userAssignedIdentity.bicep' = {
name: 'processorUserAssignedIdentity'
scope: rg
params: {
location: location
tags: tags
identityName: !empty(processorUserAssignedIdentityName) ? processorUserAssignedIdentityName : '${abbrs.managedIdentityUserAssignedIdentities}processor-${resourceToken}'
}
}
```


For more information, see [rbac.bicep](https://github.com/Azure-Samples/functions-quickstart-javascript-azd/blob/main/infra/app/rbac.bicep).

#### Configure network access

Azure Functions supports [virtual network integration](/en-us/azure/azure-functions/functions-networking-options#virtual-network-integration), which gives your function app access to resources in your virtual network. After integration, your app routes outbound traffic through the virtual network. Then your app can access private endpoints or resources by using rules that only allow traffic from specific subnets. If the destination is an IP address outside of the virtual network, the source IP address is one of the addresses listed in your app's properties, unless you configure a NAT gateway.

When you enable [virtual network integration](/en-us/azure/azure-functions/flex-consumption-how-to#enable-virtual-network-integration) for your function apps,
follow the best practices in [TSG for virtual network integration for web apps and function apps](https://eng.ms/docs/cloud-ai-platform/devdiv/serverless-paas-balam/serverless-paas-vikr/app-service-web-apps/app-service-team-documents/functionteamdocs/faqs/tsg-vnet-integration).

**main.bicep**

```
// Virtual network and private endpoint
module serviceVirtualNetwork 'app/vnet.bicep' = {
name: 'serviceVirtualNetwork'
scope: rg
params: {
location: location
tags: tags
vNetName: !empty(vNetName) ? vNetName : '${abbrs.networkVirtualNetworks}${resourceToken}'
}
}
module servicePrivateEndpoint 'app/storage-PrivateEndpoint.bicep' = {
name: 'servicePrivateEndpoint'
scope: rg
params: {
location: location
tags: tags
virtualNetworkName: !empty(vNetName) ? vNetName : '${abbrs.networkVirtualNetworks}${resourceToken}'
subnetName: serviceVirtualNetwork.outputs.peSubnetName
resourceName: storage.outputs.name
}
}
```


For more information, see [VNet.bicep](https://github.com/Azure-Samples/functions-quickstart-javascript-azd/blob/main/infra/app/vnet.bicep) and [storage-PrivateEndpoint.bicep](https://github.com/Azure-Samples/functions-quickstart-javascript-azd/blob/main/infra/app/storage-PrivateEndpoint.bicep).

#### Configure deployment settings

Deployments follow a single path. After you build your project code and zip it into an application package, deploy it to a Blob Storage container. When it starts, your app gets the package and runs your function code from it. By default, the same storage account that stores internal host metadata, such as `AzureWebJobsStorage`

, also serves as the deployment container. However, you can use an alternative storage account or choose your preferred authentication method by configuring your app's deployment settings. For more information, see [Deployment technology details](/en-us/azure/azure-functions/functions-deployment-technologies#deployment-technology-details) and [Configure deployment settings](/en-us/azure/azure-functions/flex-consumption-how-to#configure-deployment-settings).

### Generate IaC files

Use tools like Bicep, Azure Resource Manager templates, or Terraform to create IaC files to deploy Azure resources.

Tip

Use this custom chat mode prompt to generate infrastructure as code (IaC) files for Azure Functions:

`/LambdaMigration-Phase3-GenerateFunctionsInfra`

Define resources such as Azure Functions, storage accounts, and networking components in your IaC files.

Use this

[IaC samples repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC)for samples that use Azure Functions recommendations and best practices.

### Use tools for refactoring

Use tools like GitHub Copilot in VS Code for help with code refactoring, manual refactoring for specific changes, or other migration aids.

Note

Use *Agent mode* in GitHub Copilot in VS Code.

The following articles provide specific examples and detailed steps to facilitate the migration process:

## Develop a step-by-step process for Day-0 migration

Develop failover and failback strategies for your migration and thoroughly test them in a preproduction environment. We recommend that you perform end-to-end testing before you finally transition from AWS Lambda to Azure Functions.

Validate functionality

Test each function thoroughly to ensure that it works as expected. These tests should include input/output, event triggers, and bindings verification.

Tip

Use this custom chat mode prompt to validate the migrated Azure Functions code:

`/LambdaMigration-Phase4-ValidateCode`

Use tools like curl or

[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)extensions on VS Code to send HTTP requests for HTTP-triggered functions.For other triggers, such as timers or queues, ensure that the triggers fire correctly and the functions run as expected.


Validate performance

Conduct performance testing to compare the new Azure Functions deployment with the previous AWS Lambda deployment.

Monitor metrics like response time, run time, and resource consumption.

Tip

Use this custom chat mode prompt to validate the infrastructure configuration:

`/LambdaMigration-Phase5-ValidateInfra`

Use Application Insights for

[monitoring, log analysis, and troubleshooting](/en-us/azure/azure-functions/functions-monitoring)during the testing phase.

Troubleshoot by using the diagnose and solve problems feature

Use the

[diagnose and solve problems](/en-us/azure/app-service/overview-diagnostics)feature in the Azure portal to troubleshoot your function app. This tool provides a set of diagnostics features that can help you quickly identify and resolve common problems, such as application crashes, performance degradation, and configuration problems. Follow the guided troubleshooting steps and recommendations that the tool provides to address problems that you identify.

## Evaluate the end state of the migrated workload

Before you decommission resources in AWS, you need to be confident that the platform meets current workload expectations and that nothing blocks workload maintenance or further development.

Deploy and test functions to validate their performance and correctness.

### Deploy to Azure

Tip

Use this custom chat mode prompt to deploy the validated project to Azure:

```
/LambdaMigration-Phase6-DeployToAzure
```


Deploy workloads by using the [VS Code](/en-us/azure/azure-functions/functions-develop-vs-code#publish-to-azure) publish feature. You can also deploy workloads from the command line by using [Azure Functions Core Tools](/en-us/azure/azure-functions/functions-run-local#project-file-deployment) or the [Azure CLI](/en-us/cli/azure/functionapp/deployment/source#az-functionapp-deployment-source-config-zip). [Azure DevOps](/en-us/azure/azure-functions/functions-how-to-azure-devops#deploy-your-app) and [GitHub Actions](/en-us/azure/azure-functions/functions-how-to-github-actions) also use One Deploy.

Azure Functions Core Tools:

[Deploy your function app](/en-us/azure/azure-functions/flex-consumption-how-to#deploy-your-code-project)by using[Azure Functions Core Tools](/en-us/azure/azure-functions/functions-run-local)with the`func azure functionapp publish <FunctionAppName>`

command.Continuous integration and continuous deployment (CI/CD) pipelines: Set up a CI/CD pipeline by using services like GitHub Actions, Azure DevOps, or another CI/CD tool.


For more information, see [Continuous delivery by using GitHub Actions](/en-us/azure/azure-functions/functions-how-to-github-actions) or [Continuous delivery with Azure Pipelines](/en-us/azure/azure-functions/functions-how-to-azure-devops).

## Explore sample migration scenarios

Use the [MigrationGetStarted repo](https://github.com/MadhuraBharadwaj-MSFT/MigrationGetStarted) as a template to begin your proof of concept. This repo includes a ready-to-deploy Azure Functions project that has the infrastructure and source code files to help you get started.

If you prefer to use Terraform, use [MigrationGetStarted-Terraform](https://github.com/MadhuraBharadwaj-MSFT/MigrationGetStarted-Terraform) instead.

## Optimize and monitor the application's performance on Azure

After you migrate your workload, we recommend that you explore more features on Azure. These features might help you fulfill future workload requirements and help close gaps.

### Use Application Insights for monitoring and troubleshooting

Enable [Application Insights](/en-us/azure/azure-functions/functions-monitoring) for your function app to collect detailed telemetry data for monitoring and troubleshooting. You can enable Application Insights through the Azure portal or in the function app's host.json configuration file. After you enable Application Insights, you can:

Collect telemetry data. Application Insights provides various telemetry data such as request logs, performance metrics, exceptions, and dependencies.

Analyze logs and metrics. Access the Application Insights dashboard from the Azure portal to visualize and analyze logs, metrics, and other telemetry data. Use the built-in tools to create custom queries and visualize data to gain insights into the performance and behavior of your function app.

Set up alerts. Configure alerts in Application Insights to notify you of critical problems, performance degradation, or specific events. These alerts help you proactively monitor and quickly respond to problems.


### Optimize for cost and performance

Scaling and performance optimization:

Use autoscaling features to handle varying workloads efficiently.

Optimize function code to improve performance by reducing run time, optimizing dependencies, and using efficient coding practices.

Implement caching strategies to reduce repeated processing and latency for frequently accessed data.


Cost management:

Use

[Microsoft Cost Management](/en-us/azure/cost-management-billing/cost-management-billing-overview)tools to monitor and analyze your Azure Functions costs.Set up budgeting and cost alerts to manage and predict expenses effectively.


---

<!-- DOCUMENTO FUSIONADO: migrate-plan-consumption-to-flex.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/migration/migrate-plan-consumption-to-flex -->

# Migrate Consumption plan apps to the Flex Consumption plan

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides step-by-step instructions for migrating your existing function apps hosted in the [Consumption plan](../consumption-plan) in Azure Functions to instead use the [Flex Consumption plan](../flex-consumption-plan).

The way you migrate your app to the Flex Consumption plan depends on whether your app runs on Linux or on Windows. Make sure to select your operating system at the top of the article.

Tip

Azure Functions provides Azure CLI commands in [ az functionapp flex-migration](/en-us/cli/azure/functionapp/flex-migration) that automate most of the steps required to move your Linux app from the Consumption to the Flex Consumption plan. This article features these commands, which are currently only supported for apps running on Linux.

When you migrate your existing serverless apps, your functions can take advantage of these benefits of the Flex Consumption plan:

**Enhanced performance**: your apps benefit from improved scalability and always-ready instances to reduce cold start impacts.**Improved controls**: fine-tune your functions with per-function scaling and concurrency settings.**Expanded networking**: virtual network integration and private endpoints let you run your functions in both public and private networks.**Future platform investment**: as the top serverless hosting plan, current and future investments are made on Flex Consumption first for platform stability, performance, and features.

The Flex Consumption plan is the recommended serverless hosting option for your functions going forward. For more information, see [Flex Consumption plan benefits](../flex-consumption-plan#benefits). For a detailed comparison between hosting plans, see [Azure Functions hosting options](../functions-scale).

## Considerations

Before starting a migration, keep these considerations in mind:

If you're running Consumption plan function apps on Azure Government regions, review this guidance now to prepare for migration until Flex Consumption is enabled in Azure Government.

Due to the significant configuration and behavior differences between the two plans, you aren't able to

*shift*an existing Consumption plan app to the Flex Consumption plan. The migration process instead has you create a new Flex Consumption plan app that's equivalent to your current app. This new app runs in the same resource group and with the same dependencies as your current app.You should prioritize the migration of your apps that run in a Consumption plan on Linux.

This article assumes that you have a general understanding of Functions concepts and architectures and are familiar with features of your apps being migrated. Such concepts include triggers and bindings, authentication, and networking customization.

This article shows you how to both evaluate the current app and deploy your new Flex Consumption plan app using either the

[Azure portal](https://portal.azure.com)or the[Azure CLI](/en-us/cli/azure). If your current app deployment is defined by using infrastructure-as-code (IaC), you can generally follow the same steps. You can perform the same actions directly in your ARM templates or Bicep files, with these resource-specific considerations:- The Flex Consumption plan introduced a new section in the
`Microsoft.Web/sites`

resource type called`functionAppConfig`

, which contains many of the configurations that were application settings. For more information, see[Flex Consumption plan deprecations](../functions-app-settings#flex-consumption-plan-deprecations). - You can find resource configuration details for a Flex Consumption plan app in
[Automate resource deployment for your function app in Azure Functions](../functions-infrastructure-as-code?pivots=flex-consumption-plan). - Functions maintains a set of canonical Flex Consumption plan deployment examples for
[ARM templates](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC/armtemplate),[Bicep files](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC/bicep), and[Terraform files](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC).

- The Flex Consumption plan introduced a new section in the

## Prerequisites

Access to the Azure subscription containing one or more function apps to migrate. The account used to run Azure CLI commands must be able to:

- Create and manage function apps and App Service hosting plans.
- Assign roles to managed identities.
- Create and manage storage accounts.
- Create and manage Application Insights resources.
- Access all dependent resources of your app, such as Azure Key Vault, Azure Service Bus, or Azure Event Hubs.

Being assigned to the

**Owner**or**Contributor**roles in your resource group generally provides sufficient permissions.[Azure CLI](/en-us/cli/azure), version v2.77.0, or a later version. Scripts are tested using Azure CLI in[Azure Cloud Shell](/en-us/azure/cloud-shell/overview).The

[resource-graph](../../governance/resource-graph/first-query-azurecli)extension, which you can install by using thecommand:`az extension add`

`az extension add --name resource-graph`

The

, which is used to work with JSON output.`jq`

tool

## Identify potential apps to migrate

Use these steps to make a list of the function apps you need to migrate. In this list, make note of their names, resource groups, locations, and runtime stacks. You can then repeat the steps in this guide for each app you decide to migrate to the Flex Consumption plan.

The way that function app information is maintained depends on whether your app runs on Linux or Windows.

For Linux Consumption apps, use the new [ az functionapp flex-migration list](/en-us/cli/azure/functionapp/flex-migration#az-functionapp-flex-migration-list) command to identify apps that are eligible for migration:

```
az functionapp flex-migration list
```


This command automatically scans your subscription and returns two arrays:

**eligible_apps**: Linux Consumption apps that can be migrated to Flex Consumption. These apps are compatible with Flex Consumption.**ineligible_apps**: Apps that can't be migrated, along with the specific reasons why. The reasons for incompatibility need to be reviewed and addressed before continuing.

Note

This command only evaluates function apps running on the **Linux Consumption plan**. Apps running on other hosting plans (Windows Consumption, Premium, Dedicated, or Flex Consumption) won't appear in either the `eligible_apps`

or `ineligible_apps`

arrays. If you have many function apps and aren't sure which hosting plan each one uses, you can run `az functionapp list --query "[].{name:name, sku:sku}" -o table`

to see all apps and their SKUs, where `Dynamic`

indicates a Consumption plan app.

The output includes the app name, resource group, location, and runtime stack for each app, along with eligibility status and migration readiness information.

Use this [ az graph query](/en-us/cli/azure/graph#az-graph-query) command to list all function apps in your subscription that are running in a Consumption plan:

```
az graph query -q "resources | where subscriptionId == '$(az account show --query id -o tsv)' \
| where type == 'microsoft.web/sites' | where ['kind'] == 'functionapp' | where properties.sku == 'Dynamic' \
| project name, location, resourceGroup" \
--query data --output table
```


This command generates a table with the app name, location, and resource group for all Consumption apps running on Windows in the current subscription.

You're prompted to install the [resource-graph extension](/en-us/cli/azure/graph), if it isn't already installed.

## Assess your existing app

Before migrating to the Flex Consumption plan, you should perform these checks to make sure that your function app can be migrated successfully:

### Confirm region compatibility

Confirm that the Flex Consumption plan is currently supported in the same region as the Consumption plan app you intend to migrate.


Confirmed:When the`az functionapp flex-migration list`

command output has your app in the`eligible_apps`

list, the Flex Consumption plan is supported in the same region used by your current Linux Consumption app. In this case, you can continue to[Verify language stack compatibility].


Action required:When the`az functionapp flex-migration list`

command output has your app in the`ineligible_apps`

list, you see an error message stating`The site '<name>' is not in a region supported in Flex Consumption. Please see the list regions supported in Flex Consumption by running az functionapp list-flexconsumption-locations`

. In this case, the Flex Consumption plan isn't yet supported in the region used by your current Linux Consumption app.

Use this [ az functionapp list-flexconsumption-locations](/en-us/cli/azure/functionapp#az-functionapp-list-flexconsumption-locations) command to list all regions where Flex Consumption plan is available:

```
az functionapp list-flexconsumption-locations --query "sort_by(@, &name)[].{Region:name}" -o table
```


This command generates a table of Azure regions where the Flex Consumption plan is currently supported.

If your region isn't currently supported and you still choose to migrate your function app, your app must run in a different region where the Flex Consumption plan is supported. However, running your app in a different region from other connected services can introduce extra latency. Make sure that the new region can meet your application's performance requirements before you complete the migration.

### Verify language stack compatibility

Flex Consumption plans don't yet support all [Functions language stacks](../supported-languages). This table indicates which language stacks are currently supported:

| Stack setting | Stack name | Supported |
|---|---|---|
`dotnet-isolated` |
|

`node`

[JavaScript/TypeScript](../functions-reference-node)`java`

[Java](../functions-reference-java)`python`

`powershell`

[PowerShell](../functions-reference-powershell)`dotnet`

[.NET (in-process model)](../functions-dotnet-class-library)`custom`

[Custom handlers](../functions-custom-handlers)

Confirmed:If the`az functionapp flex-migration list`

command included your app in the`eligible_apps`

list, your Linux Consumption app is already using a supported language stack by Flex Consumption and you can continue to[Verify stack version compatibility].


Action required:If the`az functionapp flex-migration list`

command included your app in the`ineligible_apps`

list with an error message stating`Runtime '<name>' not supported for function apps on the Flex Consumption plan.`

, your Linux Consumption app isn't running a supported runtime by Flex Consumption yet.

If your function app uses an unsupported runtime stack:

- For C# apps that run in-process with the runtime (
`dotnet`

), you must first migrate your app to .NET isolated. For more information, see[Migrate C# apps from the in-process model to the isolated worker model](../migrate-dotnet-to-isolated-model).

### Verify stack version compatibility

Before migrating, you must make sure that your app's runtime stack version is supported when running in a Flex Consumption plan in the current region.


Confirmed:If the`az functionapp flex-migration list`

command included your app in the`eligible_apps`

list, your Linux Consumption app is already using a supported language stack version by Flex Consumption and you can continue to[Verify deployment slots usage].


Action required:If the`az functionapp flex-migration list`

command included your app in the`ineligible_apps`

list with an error message stating`Invalid version {0} for runtime {1} for function apps on the Flex Consumption plan. Supported versions for runtime {1} are {2}.`

, your Linux Consumption app isn't running a supported runtime by Flex Consumption yet.

Use this [ az functionapp list-flexconsumption-runtimes](/en-us/cli/azure/functionapp#az-functionapp-list-flexconsumption-runtimes) command to verify Flex Consumption plan support for your language stack version in a specific region:

```
az functionapp list-flexconsumption-runtimes --location <REGION> --runtime <LANGUAGE_STACK> --query '[].{version:version}' -o tsv
```


In this example, replace `<REGION>`

with your current region and `<LANGUAGE_STACK>`

with one of these values:

| Language stack | Value |
|---|---|
|

`dotnet-isolated`

[Java](../functions-reference-java)`java`

[JavaScript](../functions-reference-node)`node`

[PowerShell](../functions-reference-powershell)`powershell`

[Python](../functions-reference-python)`python`

[TypeScript](../functions-reference-node)`node`

This command displays all versions of the specified language stack supported by the Flex Consumption plan in your region.

If your function app uses an unsupported language stack version, you must first [upgrade your app code to a supported version](../update-language-versions) before migrating to the Flex Consumption plan.

### Verify deployment slots usage

Consumption plan apps can have a deployment slot defined. For more information, see [Azure Functions deployment slots](../functions-deployment-slots). However, the Flex Consumption plan doesn't currently support deployment slots. Before you migrate, you must determine if your app has a deployment slot. If so, you need to define a strategy for how to manage your app without deployment slots when running in a Flex Consumption plan.


Confirmed:When your current app has deployment slots enabled, the`az functionapp flex-migration list`

command shows your function app in the`eligible_apps`

list without a warning, continue to[Verify the use of certificates].


Action required:Your current app has deployment slots enabled, the`az functionapp flex-migration list`

command shows your function app in the`eligible_apps`

list but adds a warning that states:`The site '<name>' has slots configured. This will not block migration, but please note that slots are not supported in Flex Consumption.`


Use this [ az functionapp deployment slot list](/en-us/cli/azure/functionapp/deployment/slot#az-functionapp-deployment-slot-list) command to list any deployment slots defined in your function app:

```
az functionapp deployment slot list --name <APP_NAME> --resource-group <RESOURCE_GROUP> --output table
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. If the command returns an entry, your app has deployment slots enabled.

If your function app is currently using deployment slots, you can't currently reproduce this functionality in the Flex Consumption plan. Before migrating, you should:

- Consider rearchitecting your application to use separate function apps. In this way, you can develop, test, and deploy your function code to a second nonproduction app instead of using slots, or
- Migrate any new code or features from the deployment slot into the main (
**production**) slot.

### Verify the use of certificates

Transport Layer Security (TLS) certificates, previously known as Secure Sockets Layer (SSL) certificates, are used to help secure internet connections. TSL/SSL certificates, which include managed certificates, bring-your-own certificates (BYOC), or public-key certificates, aren't currently supported by the Flex Consumption plan.


Confirmed:If the`az functionapp flex-migration list`

command included your app in the`eligible_apps`

list, your Linux Consumption app is already not using certificates, and you can continue to[Verify your Blob storage triggers].


Action required:If the`az functionapp flex-migration list`

command included your app in the`ineligible_apps`

list with an error message stating`The site '<name>' is using TSL/SSL certificates. TSL/SSL certificates are not supported in Flex Consumption.`

or`The site '<name>' has the WEBSITE_LOAD_CERTIFICATES app setting configured. Certificate loading is not supported in Flex Consumption.`

, your Linux Consumption app isn't yet compatible with Flex Consumption.

Use the [ az webapp config ssl list](/en-us/cli/azure/webapp/config/ssl#az-webapp-config-ssl-list) command to list any TSL/SSL certificates available to your function app:

```
az webapp config ssl list --resource-group <RESOURCE_GROUP>
```


In this example, replace `<RESOURCE_GROUP>`

with your resource group name. If this command produces output, your app is likely using certificates.

If your app currently relies on TSL/SSL certificates, you shouldn't proceed with the migration until after support for certificates is added to the Flex Consumption plan.

### Verify your Blob storage triggers

Currently, the Flex Consumption plan only supports event-based triggers for Azure Blob storage, which are defined with a `Source`

setting of `EventGrid`

. Blob storage triggers that use container polling and use a `Source`

setting of `LogsAndContainerScan`

aren't supported in Flex Consumption. Because container polling is the default, you must determine if any of your Blob storage triggers are using the default `LogsAndContainerScan`

source setting. For more information, see [Trigger on a blob container](../storage-considerations#trigger-on-a-blob-container).


Confirmed:If the`az functionapp flex-migration list`

command included your app in the`eligible_apps`

list, your Linux Consumption app is already not using a blob storage triggers with`EventGrid`

as the source. You can continue to[Consider dependent services].


Action required:If the`az functionapp flex-migration list`

command included your app in the`ineligible_apps`

list with an error message stating`The site '<name>' has blob storage trigger(s) that don't use Event Grid as the source: <list> Flex Consumption only supports Event Grid-based blob triggers. Please convert these triggers to use Event Grid or replace them with Event Grid triggers before migration.`

, your Linux Consumption app isn't yet compatible with Flex Consumption.

Use this [`az functionapp function list`

] command to determine if your app has any Blob storage triggers that don't use Event Grid as the source:

```
az functionapp function list --name <APP_NAME> --resource-group <RESOURCE_GROUP> \
--query "[?config.bindings[0].type=='blobTrigger' && config.bindings[0].source!='EventGrid'].{Function:name,TriggerType:config.bindings[0].type,Source:config.bindings[0].source}" \
--output table
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. If the command returns rows, there is at least one trigger using container polling in your function app.

If your app has any Blob storage triggers that don't have an Event Grid source, you must change to an Event Grid source before you migrate to the Flex Consumption plan.

The basic steps to change an existing Blob storage trigger to an Event Grid source are:

Add or update the

`source`

property in your Blob storage trigger definition to`EventGrid`

and redeploy the app.[Build the endpoint URL](../functions-event-grid-blob-trigger#build-the-endpoint-url)in your function app used to be used by the event subscription.[Create an event subscription](../functions-event-grid-blob-trigger#create-the-event-subscription)on your Blob storage container.

For more information, see [Tutorial: Trigger Azure Functions on blob containers using an event subscription](../functions-event-grid-blob-trigger).

## Consider dependent services

Because Azure Functions is a compute service, you must consider the effect of migration on data and services both upstream and downstream of your app.

### Data protection strategies

Here are some strategies to protect both upstream and downstream data during the migration:

**Idempotency**: Ensure your functions can safely process the same message multiple times without negative side effects. For more information, see[Designing Azure Functions for identical input](../functions-idempotent).**Logging and monitoring**: Enable detailed logging in both apps during migration to track message processing. For more information, see[Monitor executions in Azure Functions](../functions-monitoring).**Checkpointing**: For streaming triggers, such as the Event Hubs trigger, implement correct checkpoint behaviors to track processing position. For more information, see[Azure Functions reliable event processing](../functions-reliable-event-processing).**Parallel processing**: Consider temporarily running both apps in parallel during the cutover. Make sure to carefully monitor and validate how data is processed from the upstream service. For more information, see[Active-active pattern for non-HTTPS trigger functions](/en-us/azure/reliability/reliability-functions#active-active-pattern-for-non-https-trigger-functions).**Gradual cutover**: For high-volume systems, consider implementing a gradual cutover by redirecting portions of traffic to the new app. You can manage the routing of requests upstream from your apps by using services such as[Azure API Management](../functions-openapi-definition)or[Azure Application Gateway](../../app-service/overview-app-gateway-integration).

### Mitigations by trigger type

You should plan mitigation strategies to protect data for the specific function triggers you might have in your app:

| Trigger | Risk to data | Strategy |
|---|---|---|
|

With the new app running, switch clients to use the new container.

Allow the original container to be processed completely before stopping the old app.

[Azure Cosmos DB](../functions-bindings-cosmosdb-v2-trigger)Set this new lease container as the

`leaseCollectionName`

configuration in your new app.Requires that your

[functions be idempotent](../functions-idempotent)or you must be able to handle the results of duplicate change feed processing.Set the

`StartFromBeginning`

configuration to `false`

in the new app to avoid reprocessing the entire feed.[Azure Event Grid](../functions-bindings-event-grid-trigger)Requires that your

[functions be idempotent](../functions-idempotent)or you must be able to handle the results of duplicate event processing.[Azure Event Hubs](../functions-bindings-event-hubs-trigger)[consumer group](../../event-hubs/event-hubs-features#consumer-groups)for use by the new app. For more information, see[Migration strategies for Event Grid triggers](../functions-reliable-event-processing#migration-strategies-for-event-grid-triggers).[Azure Service Bus](../functions-bindings-service-bus-trigger)Update senders and clients to use the new topic or queue.

After the original topic is empty, shut down the old app.

[Azure Storage queue](../functions-bindings-storage-queue-trigger)Update senders and clients to use the new queue.

After the original queue is empty, shut down the old app.

[HTTP](../functions-bindings-http-webhook-trigger)[Timer](../functions-bindings-timer)[Disable the timer trigger](../disable-function)in the old app after the new app runs successfully.## Start the migration for Linux

The [az functionapp flex-migration start](/en-us/cli/azure/functionapp/flex-migration#az-functionapp-flex-migration-start) command automatically collects application configuration information and creates a new Flex Consumption app with the same configurations as the source app. Use the command as shown in this example:

```
az functionapp flex-migration start \
--source-name <SOURCE_APP_NAME> \
--source-resource-group <SOURCE_RESOURCE_GROUP> \
--name <NEW_APP_NAME> \
--resource-group <RESOURCE_GROUP>
```


In this example, replace these placeholders with the indicated values:

| Placeholder | Value |
|---|---|
`<SOURCE_APP_NAME>` |
The name of your original app. |
`<SOURCE_RESOURCE_GROUP>` |
The resource group of the original app. |
`<NEW_APP_NAME>` |
The name of the new app. |
`<RESOURCE_GROUP>` |
The resource group of the new app. |

The `az functionapp flex-migration start`

command performs these basic tasks:

- Assesses your source app for compatibility with the Flex Consumption hosting plan.
- Creates a function app in the Flex Consumption plan.
- Migrates most configurations including app settings, identity assignments, storage mounts, CORS settings, custom domains, and access restrictions.

### Command Options

The migration command supports several options to customize the migration:

| Option | Description |
|---|---|
`--storage-account` |
Specify a different storage account for the new app |
`--maximum-instance-count` |
Set the maximum number of instances for scaling |
`--skip-access-restrictions` |
Skip migrating IP access restrictions |
`--skip-cors` |
Skip migrating CORS settings |
`--skip-hostnames` |
Skip migrating custom domains |
`--skip-managed-identities` |
Skip migrating managed identity configurations |
`--skip-storage-mount` |
Skip migrating storage mount configurations |

For complete command options, use `az functionapp flex-migration start --help`

.

After you've completed running `az functionapp flex-migration start`

successfully, continue to [Get the code deployment package](#get-the-code-deployment-package).

## Premigration tasks

Before proceeding with the migration, you must collect key information about and resources used by your Consumption plan app to help make a smooth transition to running in the Flex Consumption plan.

You should complete these tasks before you migrate your app to run in a Flex Consumption plan:

### Collect app settings

If you plan to use the same trigger and bindings sources and other settings from app settings, you need to first take note of the current app settings in your existing Consumption plan app.

Use this [ az functionapp config appsettings list](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-list) command to return an

`app_settings`

object that that contains the existing app setting as JSON:```
app_settings=$(az functionapp config appsettings list --name `<APP_NAME>` --resource-group `<RESOURCE_GROUP>`)
echo $app_settings
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively.

Caution

App settings frequently contain keys and other shared secrets. Always store applications settings securely, ideally encrypted. For improved security, you should use Microsoft Entra ID authentication with managed identities in the new Flex Consumption plan app instead of shared secrets.

### Collect application configurations

There are other app configurations not found in app settings. You should also capture these configurations from your existing app so that you can be sure to properly recreate them in the new app.

Review these settings. If any of them exist in the current app, you must decide whether they must also be recreated in the new Flex Consumption plan app:

| Configuration | Setting | Comment |
|---|---|---|
| CORS settings | `cors` |
Determines any existing cross-origin resource sharing (CORS) settings, which your clients might require. |
| Custom domains | If your app is currently using a domain other than `*.azurewebsites.net` , you would need to replace this custom domain mapping with a mapping to your new app. |
|
| HTTP version | `http20Enabled` |
Determines if HTTP 2.0 is required by your app. |
| HTTPS only | `httpsOnly` |
Determines if TSL/SSL is required to access your app. |
| Incoming client certificates | `clientCertEnabled` `clientCertMode` `clientCertExclusionPaths` |
Sets requirements for client requests that use certificates for authentication. |
| Maximum scale-out limit | `WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT` |
Sets the limit on scaled-out instances. The default maximum value is 200. This value is found in your app settings, but in a Flex Consumption plan app it instead gets added as a site setting (`maximumInstanceCount` ). |
| Minimum inbound TLS version | `minTlsVersion` |
Sets a minimum version of TLS required by your app. |
| Minimum inbound TLS Cipher | `minTlsCipherSuite` |
Sets a minimum TLS cipher requirement for your app. |
| Mounted Azure Files shares | `azureStorageAccounts` |
Determines if any explicitly mounted file shares exist in your app (Linux-only). |
| SCM basic auth publishing credentials | `scm.allow` |
Determines if the
`scm` publishing site is enabled |

[publishing methods](../functions-deployment-technologies)require it.

Use this script to obtain the relevant application configurations of your existing app:

```
# Set the app and resource group names
appName=<APP_NAME>
rgName=<RESOURCE_GROUP>
echo "Getting commonly used site settings..."
az functionapp config show --name $appName --resource-group $rgName \
--query "{http20Enabled:http20Enabled, httpsOnly:httpsOnly, minTlsVersion:minTlsVersion, \
minTlsCipherSuite:minTlsCipherSuite, clientCertEnabled:clientCertEnabled, \
clientCertMode:clientCertMode, clientCertExclusionPaths:clientCertExclusionPaths}"
echo "Checking for SCM basic publishing credentials policies..."
az resource show --resource-group $rgName --name scm --namespace Microsoft.Web \
--resource-type basicPublishingCredentialsPolicies --parent sites/$appName --query properties
echo "Checking for the maximum scale-out limit configuration..."
az functionapp config appsettings list --name $appName --resource-group $rgName \
--query "[?name=='WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT'].value" -o tsv
echo "Checking for any file share mount configurations..."
az webapp config storage-account list --name $appName --resource-group $rgName
echo "Checking for any custom domains..."
az functionapp config hostname list --webapp-name $appName --resource-group $rgName --query "[?contains(name, 'azurewebsites.net')==\`false\`]" --output table
echo "Checking for any CORS settings..."
az functionapp cors show --name $appName --resource-group $rgName
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. If any of the site settings or checks return non-null values, make a note of them.

### Identify managed identities and role-based access

Before migrating, you should document whether your app relies on the system-assigned managed identity or any user-assigned managed identities. You must also determine the role-based access control (RBAC) permissions granted to these identities. You must recreate the system-assigned managed identity and any role assignments in your new app. You should be able to reuse your user-assigned managed identities in your new app.

This script checks for both the system-assigned managed identity and any user-assigned managed identities associated with your app:

```
appName=<APP_NAME>
rgName=<RESOURCE_GROUP>
echo "Checking for a system-assigned managed identity..."
systemUserId=$(az functionapp identity show --name $appName --resource-group $rgName --query "principalId" -o tsv)
if [[ -n "$systemUserId" ]]; then
echo "System-assigned identity principal ID: $systemUserId"
echo "Checking for role assignments..."
az role assignment list --assignee $systemUserId --all
else
echo "No system-assigned identity found."
fi
echo "Checking for user-assigned managed identities..."
userIdentities=$(az functionapp identity show --name $appName --resource-group $rgName --query 'userAssignedIdentities' -o json)
if [[ "$userIdentities" != "{}" && "$userIdentities" != "null" ]]; then
echo "$userIdentities" | jq -c 'to_entries[]' | while read -r identity; do
echo "User-assigned identity name: $(echo "$identity" | jq -r '.key' | sed 's|.*/userAssignedIdentities/||')"
echo "Checking for role assignments..."
az role assignment list --assignee $(echo "$identity" | jq -r '.value.principalId') --all --output json
echo
done
else
echo "No user-assigned identities found."
fi
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. Make a note of all identities and their role assignments.

### Identify built-in authentication settings

Before migrating to Flex Consumption, you should collect information about any built-in authentication configurations. If you want to have your app use the same client authentication behaviors, you must recreate them in the new app. For more information, see [Authentication and authorization in Azure Functions](../../app-service/overview-authentication-authorization).

Pay special attention to redirect URIs, allowed external redirects, and token settings to ensure a smooth transition for authenticated users.

Use this [ az webapp auth show](/en-us/cli/azure/webapp/auth#az-webapp-auth-show) command to determine if

[built-in authentication](../../app-service/overview-authentication-authorization)is configured in your function app:

```
az webapp auth show --name <APP_NAME> --resource-group <RESOURCE_GROUP>
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. Review the output to determine if authentication is enabled and which identity providers are configured.

You should recreate these setting in your new app post-migration so that your clients can maintain access using their preferred provider.

### Review inbound access restrictions

It's possible to set [inbound access restrictions](../functions-networking-options#inbound-access-restrictions) on apps in a Consumption plan. You might want to maintain these restrictions in your new app. For each restriction defined, make sure to capture these properties:

- IP addresses or CIDR ranges
- Priority values
- Action type (Allow/Deny)
- Names of the rules

This [ az functionapp config access-restriction show] command returns a list of any existing IP-based access restrictions:

```
az functionapp config access-restriction show --name <APP_NAME> --resource-group <RESOURCE_GROUP>
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively.

When running in the Flex Consumption plan, you can recreate these inbound IP-based restrictions. You can further secure your app by implementing other networking restrictions, such as virtual network integration and inbound private endpoints. For more information, see [Virtual network integration](../flex-consumption-plan#virtual-network-integration).

## Get the code deployment package

To be able to redeploy your app, you must have either your project's source files or the deployment package. Ideally, your project files are maintained in source control so that you can easily redeploy function code to your new app. If you have your source code files, you can skip this section and continue to [Capture performance benchmarks (optional)](#capture-performance-benchmarks-optional).

If you no longer have access to your project source files, you can download the current deployment package from the existing Consumption plan app in Azure. The location of the deployment package depends on whether you run on Linux or Windows.

Consumption plan apps on Linux maintain the deployment zip package file in one of these locations:

An Azure Blob storage container named

`scm-releases`

in the default host storage account (`AzureWebJobsStorage`

). This container is the default deployment source for a Consumption plan app on Linux.If your app has a

`WEBSITE_RUN_FROM_PACKAGE`

setting that is a URL, the package is in an externally accessible location that you maintain. An external package should be hosted in a blob storage container with restricted access. For more information, see[External package URL](../functions-deployment-technologies#external-package-url).

Tip

If your storage account is restricted to managed identity access only, you might need to grant your Azure account read access to the storage container by adding it to the `Storage Blob Data Reader`

role.

The deployment package is compressed using the `squashfs`

format. To see what's inside the package, you must use tools that can decompress this format.

Use these steps to download the deployment package from your current app:

Use this

command to get the`az functionapp config appsettings list`

`WEBSITE_RUN_FROM_PACKAGE`

app setting, if present:`az functionapp config appsettings list --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --query "[?name=='WEBSITE_RUN_FROM_PACKAGE'].value" -o tsv`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group name and app name, respectively. If this command returns a URL, then you can download the deployment package file from that remote location and skip to the next section.If the

`WEBSITE_RUN_FROM_PACKAGE`

value is`1`

or nothing, use this script to get the deployment package for the existing app:`appName=<APP_NAME> rgName=<RESOURCE_GROUP> echo "Getting the storage account connection string from app settings..." storageConnection=$(az functionapp config appsettings list --name $appName --resource-group $rgName \ --query "[?name=='AzureWebJobsStorage'].value" -o tsv) echo "Getting the package name..." packageName=$(az storage blob list --connection-string $storageConnection --container-name scm-releases \ --query "[0].name" -o tsv) echo "Download the package? $packageName? (Y to proceed, any other key to exit)" read -r answer if [[ "$answer" == "Y" || "$answer" == "y" ]]; then echo "Proceeding with download..." az storage blob download --connection-string $storageConnection --container-name scm-releases \ --name $packageName --file $packageName else echo "Exiting script." exit 0 fi`

Again, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group name and app name. The package .zip file is downloaded to the directory from which you executed the command.

The location of your project source files depends on the `WEBSITE_RUN_FROM_PACKAGE`

app setting as follows:

`WEBSITE_RUN_FROM_PACKAGE` value |
Source file location |
|---|---|
`1` |
The files are in a zip package that is stored in the Azure Files share of the storage account defined by the `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` setting. The name of the files share is defined by the `WEBSITE_CONTENTSHARE` setting. |
| An endpoint URL | The files are in a zip package in an externally accessible location that you maintain. An external package should be hosted in a blob storage container with restricted access. For more information, see
|

Use this

command to get the`az functionapp config appsettings list`

`WEBSITE_RUN_FROM_PACKAGE`

app setting, if present:`az functionapp config appsettings list --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --query "[?name=='WEBSITE_RUN_FROM_PACKAGE'].value" -o tsv`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group name and app name, respectively. If this command returns a URL, then you can download the deployment package file from that remote location and skip to the next section.If the

`WEBSITE_RUN_FROM_PACKAGE`

value is`1`

or nothing, use this script to get the deployment package for the existing app:`appName=<APP_NAME> rgName=<RESOURCE_GROUP> echo "Getting the storage account connection string and file share from app settings..." json=$(az functionapp config appsettings list --name $appName --resource-group $rgName \ --query "[?name=='WEBSITE_CONTENTAZUREFILECONNECTIONSTRING' || name=='WEBSITE_CONTENTSHARE'].value" -o json) storageConnection=$(echo "$json" | jq -r '.[0]') fileShare=$(echo "$json" | jq -r '.[1]') echo "Getting the package name..." packageName=$(az storage file list --share-name $fileShare --connection-string $storageConnection \ --path "data/SitePackages" --query "[?ends_with(name, '.zip')] | sort_by(@, &properties.lastModified)[-1].name" \ -o tsv) echo "Download the package? $packageName? (Y to proceed, any other key to exit)" read -r answer if [[ "$answer" == "Y" || "$answer" == "y" ]]; then echo "Proceeding with download..." az storage file download --connection-string $storageConnection --share-name $fileShare \ --path "data/SitePackages/$packageName" else echo "Exiting script." exit 0 fi`

Again, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group name and app name. The package .zip file is downloaded to the directory from which you executed the command.

## Capture performance benchmarks (optional)

If you plan to validate performance improvement in your app based on the migration to the Flex Consumption plan, you should (optionally) capture the performance benchmarks of your current plan. Then, you can compare them to the same benchmarks for your app running in a Flex Consumption plan for comparison.

Tip

Always compare performance under similar conditions, such as time-of-day, day-of-week, and client load. Try to run the two benchmarks as close together as possible.

Here are some benchmarks to consider for your structured performance testing:

| Suggested benchmark | Comment |
|---|---|
Cold-start |
Measure the time from first request to the first response after an idle period. |
Throughput |
Measure the maximum requests-per-second using
|

**Latency**`P50`

, `P95`

, and `P99`

response times under various load conditions. You can monitor these metrics in Application Insights.You can use this Kusto query to review the suggested latency response times in Application Insights:

```
requests
| where timestamp > ago(1d)
| summarize percentiles(duration, 50, 95, 99) by bin(timestamp, 1h)
| render timechart
```


## Migration Steps

The migration of your functions from a Consumption plan app to a Flex Consumption plan app follows these main steps:

### Verify Flex Consumption app created and configured

After running the [az functionapp flex-migration start](/en-us/cli/azure/functionapp/flex-migration#az-functionapp-flex-migration-start) command, you should verify that your new Flex Consumption app was created successfully and properly configured. Here are some steps to validate the migration results:

**Verify the new app exists and is running:**`az functionapp show --name <NEW_APP_NAME> --resource-group <RESOURCE_GROUP> \ --query "{name:name, kind:kind, sku:properties.sku}" --output table`

**Review migrated app settings:**`az functionapp config appsettings list --name <NEW_APP_NAME> --resource-group <RESOURCE_GROUP> \ --output table`

Compare these settings with your source app to ensure critical configurations were transferred.

**Check managed identity configuration:**`az functionapp identity show --name <NEW_APP_NAME> --resource-group <RESOURCE_GROUP>`

**Verify any custom domains were migrated:**`az functionapp config hostname list --webapp-name <NEW_APP_NAME> --resource-group <RESOURCE_GROUP> \ --output table`


### Review Migration Summary

The automated migration command should have transferred most configurations. However, you should manually verify that these items weren't migrated and they might need to be configured manually:

**Certificates**: TSL/SSL certificates aren't supported in Flex Consumption yet**Deployment slots**: Not supported in Flex Consumption**Built-in authentication settings**: These need to be reconfigured manually**CORS settings**: May need manual verification depending on your configuration

If any critical settings are missing or incorrect, you can manually configure them using the steps outlined in the [Windows migration process](#create-an-app-in-the-flex-consumption-plan) sections of this article.

[Final review of the plan](#final-review-of-the-plan)[Create an app in the Flex Consumption plan](#create-an-app-in-the-flex-consumption-plan)[Apply migrated app settings in the new app](#apply-migrated-app-settings-in-the-new-app)[Apply other app configurations](#apply-other-app-configurations)[Configure scale and concurrency settings](#configure-scale-and-concurrency-settings)[Configure any custom domains and CORS access](#configure-any-custom-domains-and-cors-access)[Configure managed identities and assign roles](#configure-managed-identities-and-assign-roles)[Configure Network Access Restrictions](#configure-network-access-restrictions)[Enable monitoring](#enable-monitoring)[Configure built-in authentication](#configure-built-in-authentication)[Deploy Your App Code to the New Flex Consumption App](#deploy-your-app-code-to-the-new-flex-consumption-app)

### Final review of the plan

Before proceeding with the migration process, take a moment to perform these last preparatory steps:

**Review all the collected information**: Go through all the notes, configuration details, and application settings you documented in the previous assessment and premigration sections. If anything is unclear, rerun the Azure CLI commands again or get the information from the portal.**Define your migration plan**: Based on your findings, create a checklist for your migration that highlights:- Any settings that need special attention
- Triggers and bindings or other dependencies that might be affected during migration
- Testing strategy for post-migration validation
- Rollback plan if there are unexpected issues

**Downtime planning**: Consider when to stop the original function app to avoid both data loss and duplicate processing of events, and how this might affect your users or downstream systems. In some cases, you might need to[disable specific functions](../disable-function)before stopping the entire app.

A careful final review helps ensure a smoother migration process and minimizes the risk of overlooking important configurations.

### Create an app in the Flex Consumption plan

There are various ways to create a function app in the Flex Consumption plan along with other required Azure resources:

| Create option | Reference articles |
|---|---|
| Azure CLI |
|

[Create a function app in the Azure portal](../functions-create-function-app-portal)[ARM template](../functions-create-first-function-resource-manager)[azd](../create-first-function-azure-developer-cli)[Bicep](../functions-create-first-function-bicep)[Terraform](../functions-create-first-function-terraform)[Visual Studio Code deployment](../functions-develop-vs-code#publish-to-azure)[Visual Studio deployment](../functions-develop-vs#publish-to-azure)Tip

When possible, you should use Microsoft Entra ID for authentication instead of connection strings, which contain shared keys. Using managed identities is a best practice that improves security by eliminating the need to store shared secrets directly in application settings. If your original app used connection strings, the Flex Consumption plan is designed to support managed identities. Most of these links show you how to enable managed identities in your function app.

### Apply migrated app settings in the new app

Before deploying your code, you must configure the new app with the relevant Flex Consumption plan app settings from your original function app.

Important

Not all Consumption plan app settings are supported when running in a Flex Consumption plan. For more information, see [Flex Consumption plan deprecations](../functions-app-settings#flex-consumption-plan-deprecations).

Run this script that performs these tasks:

- Gets app settings from the old app, ignoring settings that don't apply in a Flex Consumption plan or that already exist in the new app.
- Writes the collected settings locally to a temporary file.
- Applies settings from the file to your new app.
- Deletes the temporary file.

```
sourceAppName=<SOURCE_APP_NAME>
destAppName=<DESTINATION_APP_NAME>
rgName=<RESOURCE_GROUP>
echo "Getting app settings from the old app..."
app_settings=$(az functionapp config appsettings list --name $sourceAppName --resource-group $rgName)
# Filter out settings that don't apply to Flex Consumption apps or that will already have been created
filtered_settings=$(echo "$app_settings" | jq 'map(select(
(.name | ascii_downcase) != "website_use_placeholder_dotnetisolated" and
(.name | ascii_downcase | startswith("azurewebjobsstorage") | not) and
(.name | ascii_downcase) != "website_mount_enabled" and
(.name | ascii_downcase) != "enable_oryx_build" and
(.name | ascii_downcase) != "functions_extension_version" and
(.name | ascii_downcase) != "functions_worker_runtime" and
(.name | ascii_downcase) != "functions_worker_runtime_version" and
(.name | ascii_downcase) != "functions_max_http_concurrency" and
(.name | ascii_downcase) != "functions_worker_process_count" and
(.name | ascii_downcase) != "functions_worker_dynamic_concurrency_enabled" and
(.name | ascii_downcase) != "scm_do_build_during_deployment" and
(.name | ascii_downcase) != "website_contentazurefileconnectionstring" and
(.name | ascii_downcase) != "website_contentovervnet" and
(.name | ascii_downcase) != "website_contentshare" and
(.name | ascii_downcase) != "website_dns_server" and
(.name | ascii_downcase) != "website_max_dynamic_application_scale_out" and
(.name | ascii_downcase) != "website_node_default_version" and
(.name | ascii_downcase) != "website_run_from_package" and
(.name | ascii_downcase) != "website_skip_contentshare_validation" and
(.name | ascii_downcase) != "website_vnet_route_all" and
(.name | ascii_downcase) != "applicationinsights_connection_string"
))')
echo "Settings to migrate..."
echo "$filtered_settings"
echo "Writing settings to a local a local file (app_settings_filtered.json)..."
echo "$filtered_settings" > app_settings_filtered.json
echo "Applying settings to the new app..."
output=$(az functionapp config appsettings set --name $destAppName --resource-group $rgName --settings @app_settings_filtered.json)
echo "Deleting the temporary settings file..."
rm -rf app_settings_filtered.json
echo "Current app settings in the new app..."
az functionapp config appsettings list --name $destAppName --resource-group $rgName
```


In this example, replace `<RESOURCE_GROUP>`

, `<SOURCE_APP_NAME>`

, and `<DEST_APP_NAME>`

with your resource group name and the old a new app names, respectively. This script assumes that both apps are in the same resource group.

### Apply other app configurations

Find the list of other app configurations from your old app that you [collected during premigration](#collect-application-configurations) and also set them in the new app.

In this script, set the value for any configuration set in the original app and comment-out any commands for any configuration not set (`null`

):

```
appName=<APP_NAME>
rgName=<RESOURCE_GROUP>
http20Setting=<YOUR_HTTP_20_SETTING>
minTlsVersion=<YOUR_TLS_VERSION>
minTlsCipher=<YOUR_TLS_CIPHER>
httpsOnly=<YOUR_HTTPS_ONLY_SETTING>
certEnabled=<CLIENT_CERT_ENABLED>
certMode=<YOUR_CLIENT_CERT_MODE>
certExPaths=<CERT_EXCLUSION_PATHS>
scmAllowBasicAuth=<ALLOW_SCM_BASIC_AUTH>
# Apply HTTP version and minimum TLS settings
az functionapp config set --name $appName --resource-group $rgName --http20-enabled $http20Setting
az functionapp config set --name $appName --resource-group $rgName --min-tls-version $minTlsVersion
# Apply the HTTPS-only setting
az functionapp update --name $appName --resource-group $rgName --set HttpsOnly=$httpsOnly
# Apply incoming client cert settings
az functionapp update --name $appName --resource-group $rgName --set clientCertEnabled=$certEnabled
az functionapp update --name $appName --resource-group $rgName --set clientCertMode=$certMode
az functionapp update --name $appName --resource-group $rgName --set clientCertExclusionPaths=$certExPaths
# Apply the TLS cipher suite setting
az functionapp update --name $appName --resource-group $rgName --set minTlsCipherSuite=$minTlsCipher
# Apply the allow scm basic auth configuration
az resource update --resource-group $rgName --name scm --namespace Microsoft.Web --resource-type basicPublishingCredentialsPolicies \
--parent sites/$appName --set properties.allow=$scmAllowBasicAuth
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group and function app names, respectively. Also, replace the placeholders of any variable definitions for existing settings you want to recreate in the new app, and comment-out any `null`

settings.

### Configure scale and concurrency settings

The Flex Consumption plan implements per-function scaling, where each function within your app can scale independently based on its workload. Scaling is also more strictly related to concurrency settings, which are used to make scaling decisions based on the current concurrent executions. For more information, see both [Per-function scaling](../flex-consumption-plan#per-function-scaling) and [Concurrency](../flex-consumption-plan#concurrency) in the Flex Consumption plan article.

Consider concurrency settings first if you want your new app to scale similarly to your original app. Setting higher concurrency values can result in fewer instances being created to handle the same load.

If you had a custom scale-out limit set in your original app, you can also apply it to your new app. Otherwise, you can skip to the next section.

The default maximum instance count is 100, and it must be set to a value of 40 or higher.

Use this [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to set the maximum scale-out.

```
az functionapp scale config set --name <APP_NAME> --resource-group <RESOURCE_GROUP> \
--maximum-instance-count <MAX_SCALE_SETTING>
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group and function app names, respectively. Replace `<MAX_SCALE_SETTING>`

with the maximum scale value you're setting.

### Configure any custom domains and CORS access

If your original app had any bound custom domains or any CORS settings defined, recreate them in your new app. For more information about custom domains, see [Set up an existing custom domain in Azure App Service](../../app-service/app-service-web-tutorial-custom-domain).

Use this

command to rebind any custom domain mappings to your app:`az functionapp config hostname add`

`az functionapp config hostname add --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --hostname <CUSTOM_DOMAIN>`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively. Replace`<CUSTOM_DOMAIN>`

with your custom domain name.Use this

command to replace any CORS settings:`az functionapp cors add`

`az functionapp cors add --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --allowed-origins <ALLOWED_ORIGIN_1> <ALLOWED_ORIGIN_2> <ALLOWED_ORIGIN_N>`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively. Replace`<ALLOWED_ORIGIN_*>`

with your allowed origins.

### Configure managed identities and assign roles

The way that you configure managed identities in your new app depends on the kind of managed identity:

| Managed identity type | Create identity | Role assignments |
|---|---|---|
| User-assigned | Optional | You can continue to use the same user-assigned managed identities with the new app. You must reassign these identities to your Flex Consumption app and verify that they still have the correct role assignments in remote services. If you choose to create new identities for the new app, you must assign the same roles as the existing identities. |
| System-assigned | Yes | Because each function app has its own system-assigned managed identity, you must enable the system-assigned managed identity in the new app and reassign the same roles as in the original app. |

Recreating the role assignments correctly is key to ensuring your function app has the same access to Azure resources after the migration.

Tip

If your original app used connection strings or other shared secrets for authentication, this is a great opportunity to improve your app's security by switching to using Microsoft Entra ID authentication with managed identities. For more information, see [Tutorial: Create a function app that connects to Azure services using identities instead of secrets](../functions-identity-based-connections-tutorial).

Use this

command to enable the system-assigned managed identity in your new app:`az functionapp identity assign`

`az functionapp identity assign --name <APP_NAME> --resource-group <RESOURCE_GROUP>`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively.Use this script to get the principal ID of the system assigned identity and add it to the required roles:

`# Get the principal ID of the system identity principalId=$(az functionapp identity show --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --query principalId -o tsv) # Assign a role in a specific resource (scope) to the system identity az role assignment create --assignee $principalId --role "<ROLE_NAME>" --scope "<RESOURCE_ID>"`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively. Replace`<ROLE_NAME>`

and`<RESOURCE_ID>`

with the role name and specific resource you captured from the original app.Repeat the previous commands for each role required by the new app.


### Configure Network Access Restrictions

If your original app had any IP-based inbound access restrictions, you can recreate any of the same inbound access rules you want to keep in your new app.

Tip

The Flex Consumption plan [fully supports virtual network integration](../flex-consumption-plan#virtual-network-integration). Because of this, you also have the option to use inbound private endpoints after migration. For more information, see [Private endpoints](../functions-networking-options#private-endpoints).

Use this [ az functionapp config access-restriction add](/en-us/cli/azure/functionapp/config/access-restriction#az-functionapp-config-access-restriction-add) command for each IP access restriction you want to replicate in the new app:

```
az functionapp config access-restriction add --name <APP_NAME> --resource-group <RESOURCE_GROUP> \
--rule-name <RULE_NAME> --action Deny --ip-address <IP_ADDRESS> --priority <PRIORITY>
```


In this example, replace these placeholders with the values from your original app:

| Placeholder | Value |
|---|---|
`<APP_NAME>` |
Your function app name. |
`<RESOURCE_GROUP>` |
Your resource group. |
`<RULE_NAME>` |
Friendly name for the IP rule. |
`<Priority>` |
Priority for the exclusion. |
`<IP_Address>` |
The IP address to exclude. |

Run this command for each documented IP restriction from the original app.

### Enable monitoring

Before you start your new app in the Flex Consumption plan, make sure that Application Insights is enabled. Having Application Insights configured helps you to troubleshoot any issues that might occur during code deployment and start-up.

Implement a comprehensive monitoring strategy that covers app metrics, logs, and costs. By using such a strategy, you can validate the success of your migration, identify any issues promptly, and optimize the performance and cost of your new app.

If you plan to compare this new app with your current app, make sure your scheme also collects the required benchmarks for comparison. For more information, see [Configure monitoring](../flex-consumption-how-to#monitor-your-app-in-azure).

### Configure built-in authentication

If your original app used built-in client authentication (sometimes called Easy Auth), you should recreate it in your new app. If you're planning to reuse the same client registration, make sure to set the new app's authenticated endpoints in the authentication provider.

Based on the information you collected earlier, use the [ az webapp auth update](/en-us/cli/azure/webapp/auth#az-webapp-auth-update) command to recreate each built-in authentication registration required by your app.

### Deploy Your App Code to the New Flex Consumption App

With your new Flex Consumption plan app fully configured based on the settings from the original app, it's time to deploy your code to the new app resources in Azure.

Caution

After successful deployment, triggers in your new app immediately start processing data from connected services. To minimize duplicated data and prevent data loss while starting the new app and shutting-down the original app, you should review the strategies that you defined in [mitigations by trigger type](#mitigations-by-trigger-type).

Functions provides several ways to deploy your code, either from the code project or as a ready-to-run deployment package.

Tip

If your project code is maintained in a source code repository, now is the perfect time to configure a continuous deployment pipeline. Continuous deployment lets you automatically deploy application updates based on changes in a connected repository.

You should update your existing deployment workflows to deploy your source code to your new app:

You can also create a new continuous deployment workflow for your new app. For more information, see [Continuous deployment for Azure Functions](../functions-continuous-deployment)

## Post-migration tasks

After a successful migration, you should perform these follow-up tasks:

### Verify basic functionality

Verify the new app is running in a Flex Consumption plan:

Use this

command two view the details about the hosting plan:`az functionapp show`

`az functionapp show --name <APP_NAME> --resource-group <RESOURCE_GROUP> --query "serverFarmId"`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively.Use an HTTP client to call at least one HTTP trigger endpoint on your new app to make sure it responds as expected.


### Capture performance benchmarks

With your new app running, you can run the same performance benchmarks that you collected from your original app, such as:

| Suggested benchmark | Comment |
|---|---|
Cold-start |
Measure the time from first request to the first response after an idle period. |
Throughput |
Measure the maximum requests-per-second using
|

**Latency**`P50`

, `P95`

, and `P99`

response times under various load conditions. You can monitor these metrics in Application Insights.You can use this Kusto query to review the suggested latency response times in Application Insights:

```
requests
| where timestamp > ago(1d)
| summarize percentiles(duration, 50, 95, 99) by bin(timestamp, 1h)
| render timechart
```


Note

Flex Consumption plan metrics differ from Consumption plan metrics. When comparing performance before and after migration, keep in mind that you must use different metrics to track similar performance characteristics. For more information, see [Configure monitoring](../flex-consumption-how-to#monitor-your-app-in-azure).

### Create custom dashboards

Azure Monitor metrics and Application Insights enable you to [create dashboards in the Azure portal](/en-us/azure/azure-portal/azure-portal-dashboards) that display charts from both platform metrics and runtime logs and analytics.

Consider setting-up dashboards and alerts on your key metrics in the Azure portal. For more information, see [Monitor your app in Azure](../flex-consumption-how-to?tabs=azure-portal#monitor-your-app-in-azure).

### Refine plan settings

Actual performance improvements and cost implications of the migration can vary based on your app-specific workloads and configuration. The Flex Consumption plan provides several settings that you can adjust to refine the performance of your app. You might want to make adjustments to more closely match the behavior of the original app or to balance cost versus performance. For more information, see [Fine-tune your app](../flex-consumption-how-to#fine-tune-your-app) in the Flex Consumption article.

### Update your Infrastructure as Code

If you manage your function app infrastructure using Bicep or Terraform, you need to update your IaC files to target the Flex Consumption plan. This section shows the key differences between Consumption and Flex Consumption plan resource definitions.

Important

You can't convert an existing Consumption plan app to Flex Consumption in place. You need to create new resources with a new name or delete the existing resources before deploying the Flex Consumption equivalents.

#### Key differences

When migrating your IaC from Consumption to Flex Consumption, consider these important changes:

| Aspect | Consumption plan | Flex Consumption plan |
|---|---|---|
| Hosting plan SKU | `Y1` (Dynamic) |
`FC1` (FlexConsumption) |
| Plan required | Optional (auto-created) | Required (must be explicit) |
| Operating system | Windows or Linux | Linux only |
| Configuration | App settings | `functionAppConfig` section |
| Storage content share | `WEBSITE_CONTENTSHARE` setting |
`deployment.storage` in `functionAppConfig` |

The examples below demonstrate the key differences between Consumption and Flex Consumption plan resource definitions, and use system assigned managed identity, but they are not complete. They don't include all required resources such as storage accounts, Application Insights, or all necessary role assignments. For complete, production-ready examples, review the [Flex Consumption IaC samples](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC).

**Consumption plan (before):**

```
// Consumption plan (optional - auto-created if omitted)
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
name: 'Y1'
tier: 'Dynamic'
}
properties: {
reserved: true // Linux
}
}
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp,linux'
properties: {
serverFarmId: hostingPlan.id
siteConfig: {
linuxFxVersion: 'DOTNET-ISOLATED|8.0'
appSettings: [
{ name: 'FUNCTIONS_EXTENSION_VERSION', value: '~4' }
{ name: 'FUNCTIONS_WORKER_RUNTIME', value: 'dotnet-isolated' }
{ name: 'AzureWebJobsStorage__accountName', value: storageAccount.name }
{ name: 'WEBSITE_CONTENTAZUREFILECONNECTIONSTRING__accountName', value: storageAccount.name }
{ name: 'WEBSITE_CONTENTSHARE', value: functionAppName }
{ name: 'APPLICATIONINSIGHTS_CONNECTION_STRING', value: appInsights.properties.ConnectionString }
{ name: 'APPLICATIONINSIGHTS_AUTHENTICATION_STRING', value: 'Authorization=AAD' }
]
}
}
identity: {
type: 'SystemAssigned'
}
}
```


**Flex Consumption plan (after):**

```
// Flex Consumption plan (required)
resource hostingPlan 'Microsoft.Web/serverfarms@2023-12-01' = {
name: hostingPlanName
location: location
sku: {
name: 'FC1'
tier: 'FlexConsumption'
}
kind: 'functionapp'
properties: {
reserved: true
}
}
// Deployment storage container (required)
resource deploymentContainer 'Microsoft.Storage/storageAccounts/blobServices/containers@2023-05-01' = {
name: '${storageAccount.name}/default/deployments'
}
resource functionApp 'Microsoft.Web/sites@2023-12-01' = {
name: functionAppName
location: location
kind: 'functionapp,linux'
properties: {
serverFarmId: hostingPlan.id
functionAppConfig: {
deployment: {
storage: {
type: 'blobContainer'
value: '${storageAccount.properties.primaryEndpoints.blob}deployments'
authentication: {
type: 'SystemAssignedIdentity'
}
}
}
scaleAndConcurrency: {
maximumInstanceCount: 100
instanceMemoryMB: 2048
}
runtime: {
name: 'dotnet-isolated'
version: '8.0'
}
}
siteConfig: {
appSettings: [
{ name: 'AzureWebJobsStorage__accountName', value: storageAccount.name }
{ name: 'APPLICATIONINSIGHTS_CONNECTION_STRING', value: appInsights.properties.ConnectionString }
{ name: 'APPLICATIONINSIGHTS_AUTHENTICATION_STRING', value: 'Authorization=AAD' }
]
}
}
identity: {
type: 'SystemAssigned'
}
}
```


Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

with `Authorization=AAD`

, you must also assign the **Monitoring Metrics Publisher** role to the function app's managed identity on the Application Insights resource.

For complete Bicep examples, see the [Flex Consumption Bicep samples](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC/bicep).

#### Reconciling IaC after migration

If you use Infrastructure as Code (IaC) to manage your Azure resources, you need to update your IaC files after migrating to Flex Consumption to prevent configuration drift. Here's a recommended approach:

**Don't mix manual and IaC deployments**: If you used the Azure CLI or portal to create your Flex Consumption app during migration, update your IaC files before the next deployment. Otherwise, your IaC might attempt to recreate the old Consumption plan resources.**Update resource names or use lifecycle management**: Since you can't convert a Consumption app to Flex Consumption in place, you have two options:**New resource names**: Update your IaC to use new names for the hosting plan and function app. This approach keeps your old resources intact until you're confident the migration succeeded.**Import existing resources**: If you want to keep the same names, delete the old resources first, then let your IaC create the new Flex Consumption resources. Alternatively, import the manually-created resources into your Terraform state using`terraform import`

or reference existing resources in Bicep.

**Verify state alignment**: After updating your IaC files, run a plan/preview operation (`terraform plan`

or`az deployment group what-if`

) to confirm no unexpected changes will occur.**Update CI/CD pipelines**: If your deployment pipelines reference the old Consumption plan configuration, update them to use the new Flex Consumption resource definitions and deployment methods.

Tip

To minimize disruption, consider running both the old Consumption app and new Flex Consumption app in parallel during a transition period. Update your IaC to manage the new Flex Consumption app, verify it works correctly, then remove the old Consumption app resources from both Azure and your IaC files.

### Remove the original app (optional)

After thoroughly testing your new Flex Consumption function app and validating that everything is working as expected, you might want to clean up resources to avoid unnecessary costs. Even though triggers in the original app are likely already disabled, you might wait a few days or even weeks before removing the original app entirely. This delay, which depends on your application's usage patterns, makes sure that all scenarios, including infrequent ones, are properly tested. Only after you're satisfied with the migration results, should you proceed to remove your original function app.

Important

This action deletes your original function app. The Consumption plan remains intact if other apps are using it. Before you proceed, make sure you've successfully migrated all functionality to the new Flex Consumption app, verified no traffic is being directed to the original app, and backed up any relevant logs, configuration, or data that might be needed for reference.

Use the [ az functionapp delete](/en-us/cli/azure/functionapp#az-functionapp-delete) command to delete the original function app:

```
az functionapp delete --name <ORIGINAL_APP_NAME> --resource-group <RESOURCE_GROUP>
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group and function app names, respectively.

## Troubleshooting and Recovery Strategies

Despite careful planning, migration issues can occur. Here's how to handle potential issues during migration:

| Issue | Solution |
|---|---|
| Cold start performance issues | • Review
• Check for missing dependencies |

[extension bundles](../extension-bundles)• Update binding configurations

[Application Insights connection](../configure-monitoring#enable-application-insights-integration)[General troubleshooting steps](#general-troubleshooting-steps)[General troubleshooting steps](#general-troubleshooting-steps)If you experience issues migrating a production app, you might want to [rollback the migration to the original app](#rollback-steps-for-critical-production-apps) while you troubleshoot.

### General troubleshooting steps

Use these steps for cases where the new app fails to start or function triggers aren't processing events:

In your new app page in the

[Azure portal](https://portal.azure.com), select**Diagnose and solve problems**in the left pane of the app page. Select**Availability and Performance**and review the**Function App Down or Reporting Errors**detector. For more information, see[Azure Functions diagnostics overview](../functions-diagnostics).In the app page, select

**Monitoring**>**Application Insights**>**View Application Insights data**then select**Investigate**>**Failures**and check for any failure events.Select

**Monitoring**>**Logs**and run this Kusto query to check these tables for errors:`traces | where severityLevel == 3 | where cloud_RoleName == "<APP_NAME>" | where timestamp > ago(1d) | project timestamp, message, operation_Name, customDimensions | order by timestamp desc`

In these queries, replace

`<APP_NAME>`

with the name of your new app. These queries check for errors in the past day (`where timestamp > ago(1d)`

).Back in the app page, select

**Settings**>**Environment variables**and verify that all critical application settings were correctly transferred. Look for any[deprecated settings](../functions-app-settings#flex-consumption-plan-deprecations)that might have been incorrectly migrated or any typos or incorrect connection strings. Verify the[default host storage connection](../functions-recover-storage-account).Select

**Settings**>**Identity**and double-check that the expected identities exist and that they have been assigned to the correct roles.In your code, verify that all binding configurations are correct, paying particular attention to connection string names, storage queue and container names, and consumer group settings in Event Hubs triggers.


### Rollback steps for critical production apps

If you aren't able to troubleshoot successfully, you might want to revert to using your original app while you continue to troubleshoot.

If the original app was stopped, restart it:

Use this

command to restart the original function app:`az functionapp start`

`az functionapp delete --name <ORIGINAL_APP_NAME> --resource-group <RESOURCE_GROUP>`

If you created new queues/topics/containers, ensure clients are redirected back to the original resources.

If you modified DNS or custom domains, revert these changes to point to the original app.


## Providing feedback

If you encounter issues with your migration using this article or want to provide other feedback on this guidance, use one of these methods to get help or provide your feedback:

-[Get help at Microsoft Q&A](/en-us/answers/tags/87/azure-functions/)

-Create an issue in the [Azure Functions repo](https://github.com/Azure/Azure-Functions/issues)

-[Provide product feedback](https://feedback.azure.com/d365community/forum/9df02822-f224-ec11-b6e6-000d3a4f0da0)

-[Create a support ticket](https://azure.microsoft.com/support/create-ticket)

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-host-json___configure-encrypt-at-rest-using-cmk_self-hosted-mcp-serve_15bc64.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-host-json.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json -->

# host.json reference for Azure Functions 2.x and later

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The host.json metadata file contains configuration options that affect all functions in a function app instance. This article lists the settings that are available starting with version 2.x of the Azure Functions runtime.

Note

This article is for Azure Functions 2.x and later versions. For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

Other function app configuration options are managed depending on where the function app runs:

**Deployed to Azure**: in your[application settings](functions-app-settings)**On your local computer**: in the[local.settings.json](functions-develop-local#local-settings-file)file.

Configurations in host.json related to bindings are applied equally to each function in the function app.

You can also [override or apply settings per environment](#override-hostjson-values) using application settings.

## Sample host.json file

The following sample *host.json* file for version 2.x+ has all possible options specified (excluding any that are for internal use only).

```
{
"version": "2.0",
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
},
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
},
"extensions": {
"blobs": {},
"cosmosDb": {},
"durableTask": {},
"eventHubs": {},
"http": {},
"queues": {},
"sendGrid": {},
"serviceBus": {}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
},
"functions": [ "QueueProcessor", "GitHubWebHook" ],
"functionTimeout": "00:05:00",
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
},
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"Function.MyFunction": "Information",
"default": "None"
},
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 20,
"evaluationInterval": "01:00:00",
"initialSamplingPercentage": 100.0,
"samplingPercentageIncreaseTimeout" : "00:00:01",
"samplingPercentageDecreaseTimeout" : "00:00:01",
"minSamplingPercentage": 0.1,
"maxSamplingPercentage": 100.0,
"movingAverageRatio": 1.0,
"excludedTypes" : "Dependency;Event",
"includedTypes" : "PageView;Trace"
},
"dependencyTrackingOptions": {
"enableSqlCommandTextInstrumentation": true
},
"enableLiveMetrics": true,
"enableDependencyTracking": true,
"enablePerformanceCountersCollection": true,
"httpAutoCollectionOptions": {
"enableHttpTriggerExtendedInfoCollection": true,
"enableW3CDistributedTracing": true,
"enableResponseHeaderInjection": true
},
"snapshotConfiguration": {
"agentEndpoint": null,
"captureSnapshotMemoryWeight": 0.5,
"failedRequestLimit": 3,
"handleUntrackedExceptions": true,
"isEnabled": true,
"isEnabledInDeveloperMode": false,
"isEnabledWhenProfiling": true,
"isExceptionSnappointsEnabled": false,
"isLowPrioritySnapshotUploader": true,
"maximumCollectionPlanSize": 50,
"maximumSnapshotsRequired": 3,
"problemCounterResetInterval": "24:00:00",
"provideAnonymousTelemetry": true,
"reconnectInterval": "00:15:00",
"shadowCopyFolder": null,
"shareUploaderProcess": true,
"snapshotInLowPriorityThread": true,
"snapshotsPerDayLimit": 30,
"snapshotsPerTenMinutesLimit": 1,
"tempFolder": null,
"thresholdForSnapshotting": 1,
"uploaderProxy": null
}
}
},
"managedDependency": {
"enabled": true
},
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
},
"telemetryMode": "OpenTelemetry",
"watchDirectories": [ "Shared", "Test" ],
"watchFiles": [ "myFile.txt" ]
}
```


The following sections of this article explain each top-level property. All are optional unless otherwise indicated.

## aggregator

Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](configure-monitoring#configure-the-aggregator).

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


| Property | Default | Description |
|---|---|---|
| batchSize | 1000 | Maximum number of requests to aggregate. |
| flushTimeout | 00:00:30 | Maximum time period to aggregate. |

Function invocations are aggregated when the first of the two limits are reached.

## applicationInsights

This setting is a child of [logging](#logging).

Controls options for Application Insights, including [sampling options](configure-monitoring#configure-sampling).

For the complete JSON structure, see the earlier [example host.json file](#sample-hostjson-file).

Note

Log sampling may cause some executions to not show up in the Application Insights monitor blade. To avoid log sampling, add `excludedTypes: "Request"`

to the `samplingSettings`

value.

| Property | Default | Description |
|---|---|---|
| samplingSettings | n/a | See
|

[applicationInsights.dependencyTrackingOptions](#applicationinsightsdependencytrackingoptions).[applicationInsights.samplingSettings.excludedTypes](#applicationinsightssamplingsettings), For more information, see see[Select and filter your metrics](/en-us/azure/azure-monitor/app/live-stream#select-and-filter-your-metrics).[applicationInsights.httpAutoCollectionOptions](#applicationinsightshttpautocollectionoptions).[applicationInsights.snapshotConfiguration](#applicationinsightssnapshotconfiguration).### applicationInsights.samplingSettings

For more information about these settings, see [Sampling in Application Insights](/en-us/azure/azure-monitor/app/sampling).

| Property | Default | Description |
|---|---|---|
| isEnabled | true | Enables or disables sampling. |
| maxTelemetryItemsPerSecond | 20 | The target number of telemetry items logged per second on each server host. If your app runs on many hosts, reduce this value to remain within your overall target rate of traffic. |
| evaluationInterval | 01:00:00 | The interval at which the current rate of telemetry is reevaluated. Evaluation is performed as a moving average. You might want to shorten this interval if your telemetry is liable to sudden bursts. |
| initialSamplingPercentage | 100.0 | The initial sampling percentage applied at the start of the sampling process to dynamically vary the percentage. Don't reduce value while you're debugging. |
| samplingPercentageIncreaseTimeout | 00:00:01 | When the sampling percentage value changes, this property determines how soon afterwards Application Insights is allowed to raise sampling percentage again to capture more data. |
| samplingPercentageDecreaseTimeout | 00:00:01 | When the sampling percentage value changes, this property determines how soon afterwards Application Insights is allowed to lower sampling percentage again to capture less data. |
| minSamplingPercentage | 0.1 | As sampling percentage varies, this property determines the minimum allowed sampling percentage. |
| maxSamplingPercentage | 100.0 | As sampling percentage varies, this property determines the maximum allowed sampling percentage. |
| movingAverageRatio | 1.0 | In the calculation of the moving average, the weight assigned to the most recent value. Use a value equal to or less than 1. Smaller values make the algorithm less reactive to sudden changes. |
| excludedTypes | null | A semi-colon delimited list of types that you don't want to be sampled. Recognized types are: `Dependency` , `Event` , `Exception` , `PageView` , `Request` , and `Trace` . All instances of the specified types are transmitted; the types that aren't specified are sampled. |
| includedTypes | null | A semi-colon delimited list of types that you want to be sampled; an empty list implies all types. Type listed in `excludedTypes` override types listed here. Recognized types are: `Dependency` , `Event` , `Exception` , `PageView` , `Request` , and `Trace` . Instances of the specified types are sampled; the types that aren't specified or implied are transmitted without sampling. |

### applicationInsights.httpAutoCollectionOptions

| Property | Default | Description |
|---|---|---|
| enableHttpTriggerExtendedInfoCollection | true | Enables or disables extended HTTP request information for HTTP triggers: incoming request correlation headers, multi-instrumentation keys support, HTTP method, path, and response. |
| enableW3CDistributedTracing | true | Enables or disables support of W3C distributed tracing protocol (and turns on legacy correlation schema). Enabled by default if `enableHttpTriggerExtendedInfoCollection` is true. If `enableHttpTriggerExtendedInfoCollection` is false, this flag applies to outgoing requests only, not incoming requests. |
| enableResponseHeaderInjection | true | Enables or disables injection of multi-component correlation headers into responses. Enabling injection allows Application Insights to construct an Application Map to when several instrumentation keys are used. Enabled by default if `enableHttpTriggerExtendedInfoCollection` is true. This setting doesn't apply if `enableHttpTriggerExtendedInfoCollection` is false. |

### applicationInsights.dependencyTrackingOptions

| Property | Default | Description |
|---|---|---|
| enableSqlCommandTextInstrumentation | false | Enables collection of the full text of SQL queries, which is disabled by default. For more information on collecting SQL query text, see
|

### applicationInsights.snapshotConfiguration

For more information on snapshots, see [Debug snapshots on exceptions in .NET apps](/en-us/azure/azure-monitor/app/snapshot-debugger) and [Troubleshoot problems enabling Application Insights Snapshot Debugger or viewing snapshots](/en-us/troubleshoot/azure/azure-monitor/app-insights/snapshot-debugger-troubleshoot).

| Property | Default | Description |
|---|---|---|
| agentEndpoint | null | The endpoint used to connect to the Application Insights Snapshot Debugger service. If null, a default endpoint is used. |
| captureSnapshotMemoryWeight | 0.5 | The weight given to the current process memory size when checking if there's enough memory to take a snapshot. The expected value is a greater than 0 proper fraction (0 < CaptureSnapshotMemoryWeight < 1). |
| failedRequestLimit | 3 | The limit on the number of failed requests to request snapshots before the telemetry processor is disabled. |
| handleUntrackedExceptions | true | Enables or disables tracking of exceptions that aren't tracked by Application Insights telemetry. |
| isEnabled | true | Enables or disables snapshot collection |
| isEnabledInDeveloperMode | false | Enables or disables snapshot collection is enabled in developer mode. |
| isEnabledWhenProfiling | true | Enables or disables snapshot creation even if the Application Insights Profiler is collecting a detailed profiling session. |
| isExceptionSnappointsEnabled | false | Enables or disables filtering of exceptions. |
| isLowPrioritySnapshotUploader | true | Determines whether to run the SnapshotUploader process at below normal priority. |
| maximumCollectionPlanSize | 50 | The maximum number of problems that we can track at any time in a range from one to 9999. |
| maximumSnapshotsRequired | 3 | The maximum number of snapshots collected for a single problem, in a range from one to 999. A problem may be thought of as an individual throw statement in your application. Once the number of snapshots collected for a problem reaches this value, no more snapshots will be collected for that problem until problem counters are reset (see `problemCounterResetInterval` ) and the `thresholdForSnapshotting` limit is reached again. |
| problemCounterResetInterval | 24:00:00 | How often to reset the problem counters in a range from one minute to seven days. When this interval is reached, all problem counts are reset to zero. Existing problems that have already reached the threshold for doing snapshots, but haven't yet generated the number of snapshots in `maximumSnapshotsRequired` , remain active. |
| provideAnonymousTelemetry | true | Determines whether to send anonymous usage and error telemetry to Microsoft. This telemetry may be used if you contact Microsoft to help troubleshoot problems with the Snapshot Debugger. It's also used to monitor usage patterns. |
| reconnectInterval | 00:15:00 | How often we reconnect to the Snapshot Debugger endpoint. Allowable range is one minute to one day. |
| shadowCopyFolder | null | Specifies the folder to use for shadow copying binaries. If not set, the folders specified by the following environment variables are tried in order: Fabric_Folder_App_Temp, LOCALAPPDATA, APPDATA, TEMP. |
| shareUploaderProcess | true | If true, only one instance of SnapshotUploader will collect and upload snapshots for multiple apps that share the InstrumentationKey. If set to false, the SnapshotUploader will be unique for each (ProcessName, InstrumentationKey) tuple. |
| snapshotInLowPriorityThread | true | Determines whether or not to process snapshots in a low IO priority thread. Creating a snapshot is a fast operation but, in order to upload a snapshot to the Snapshot Debugger service, it must first be written to disk as a minidump. That happens in the SnapshotUploader process. Setting this value to true uses low-priority IO to write the minidump, which won't compete with your application for resources. Setting this value to false speeds up minidump creation at the expense of slowing down your application. |
| snapshotsPerDayLimit | 30 | The maximum number of snapshots allowed in one day (24 hours). This limit is also enforced on the Application Insights service side. Uploads are rate limited to 50 per day per application (that is, per instrumentation key). This value helps prevent creating additional snapshots that will eventually be rejected during upload. A value of zero removes the limit entirely, which isn't recommended. |
| snapshotsPerTenMinutesLimit | 1 | The maximum number of snapshots allowed in 10 minutes. Although there's no upper bound on this value, exercise caution increasing it on production workloads because it could impact the performance of your application. Creating a snapshot is fast, but creating a minidump of the snapshot and uploading it to the Snapshot Debugger service is a much slower operation that will compete with your application for resources (both CPU and I/O). |
| tempFolder | null | Specifies the folder to write minidumps and uploader log files. If not set, then %TEMP%\Dumps is used. |
| thresholdForSnapshotting | 1 | How many times Application Insights needs to see an exception before it asks for snapshots. |
| uploaderProxy | null | Overrides the proxy server used in the Snapshot Uploader process. You may need to use this setting if your application connects to the internet via a proxy server. The Snapshot Collector runs within your application's process and will use the same proxy settings. However, the Snapshot Uploader runs as a separate process and you may need to configure the proxy server manually. If this value is null, then Snapshot Collector will attempt to autodetect the proxy's address by examining `System.Net.WebRequest.DefaultWebProxy` and passing on the value to the Snapshot Uploader. If this value isn't null, then autodetection isn't used and the proxy server specified here will be used in the Snapshot Uploader. |

## blobs

Configuration settings can be found in [Storage blob triggers and bindings](functions-bindings-storage-blob#hostjson-settings).

## console

This setting is a child of [logging](#logging). It controls the console logging when not in debugging mode.

```
{
"logging": {
...
"console": {
"isEnabled": false,
"DisableColors": true
},
...
}
}
```


| Property | Default | Description |
|---|---|---|
| DisableColors | false | Suppresses log formatting in the container logs on Linux. Set to true if you're seeing unwanted ANSI control characters in the container logs when running on Linux. |
| isEnabled | false | Enables or disables console logging. |

## Azure Cosmos DB

Configuration settings can be found in [Azure Cosmos DB triggers and bindings](functions-bindings-cosmosdb-v2#hostjson-settings).

## customHandler

Configuration settings for a custom handler. For more information, see [Azure Functions custom handlers](functions-custom-handlers#configuration).

```
"customHandler": {
"description": {
"defaultExecutablePath": "server",
"workingDirectory": "handler",
"arguments": [ "--port", "%FUNCTIONS_CUSTOMHANDLER_PORT%" ]
},
"enableForwardingHttpRequest": false
}
```


| Property | Default | Description |
|---|---|---|
| defaultExecutablePath | n/a | The executable to start as the custom handler process. It's a required setting when using custom handlers and its value is relative to the function app root. |
| workingDirectory | function app root |
The working directory in which to start the custom handler process. It's an optional setting and its value is relative to the function app root. |
| arguments | n/a | An array of command line arguments to pass to the custom handler process. |
| enableForwardingHttpRequest | false | If set, all functions that consist of only an HTTP trigger and HTTP output is forwarded the original HTTP request instead of the custom handler
|

## durableTask

Configuration setting can be found in [bindings for Durable Functions](durable/durable-functions-bindings#host-json).

## concurrency

Enables dynamic concurrency for specific bindings in your function app. For more information, see [Dynamic concurrency](functions-concurrency#dynamic-concurrency).

```
{
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
}
}
```


| Property | Default | Description |
|---|---|---|
| dynamicConcurrencyEnabled | false | Enables dynamic concurrency behaviors for all triggers supported by this feature, which is off by default. |
| snapshotPersistenceEnabled | true | Learned concurrency values are periodically persisted to storage so new instances start from those values instead of starting from 1 and having to redo the learning. |

## eventHub

Configuration settings can be found in [Event Hub triggers and bindings](functions-bindings-event-hubs#host-json).

## extensions

Property that returns an object that contains all of the binding-specific settings, such as [http](#http) and [eventHub](#eventhub).

## extensionBundle

Extension bundles let you add a compatible set of Functions binding extensions to your function app. To learn more, see [Extension bundles for local development](extension-bundles).

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

The following properties are available in `extensionBundle`

:

| Property | Description |
|---|---|
`id` |
The namespace for Azure Functions extension bundles. |
`version` |
The version range of the bundle to install. The Azure Functions runtime always chooses the maximum permissible version that the version range or interval defines. For example, a `version` value range of `[4.0.0, 5.0.0)` allows all bundle versions from 4.0.0 up to (but not including) 5.0.0. For more information, see the
|

Tip

You might also see the version range defined in your *host.json* as `[4.*, 5.0.0)`

, which is interpreted the same as `[4.0.0, 5.0.0)`

.

## functions

A list of functions that the job host runs. An empty array means run all functions. Intended for use only when [running locally](functions-run-local). In function apps in Azure, you should instead follow the steps in [How to disable functions in Azure Functions](disable-function) to disable specific functions rather than using this setting.

```
{
"functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```


## functionTimeout

Indicates the timeout duration for all function executions. It follows the [timespan string format](/en-us/dotnet/fundamentals/runtime-libraries/system-timespan-parse). A value of `-1`

indicates unbounded execution, but keeping a fixed upper bound is recommended.

```
{
"functionTimeout": "00:05:00"
}
```


The format of the timespan string needs to follow the syntax `[d.]hh:mm:ss`

and the valid values are:

- d = days (optional)
- hh = hours (0–23)
- mm = minutes (0–59)
- ss = seconds (0–59)

Tip

When you need to set a 24-hour timeout, you must define it as one day (`"1.00:00:00"`

) instead of 24 hours (`"24:00:00"`

). You might also use `"23:59:59"`

.

For more information on the default and maximum values for specific plans, see [Function app timeout duration](functions-scale#timeout).

## healthMonitor

Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).

```
{
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
}
}
```


| Property | Default | Description |
|---|---|---|
| enabled | true | Specifies whether the feature is enabled. |
| healthCheckInterval | 10 seconds | The time interval between the periodic background health checks. |
| healthCheckWindow | 2 minutes | A sliding time window used in conjunction with the `healthCheckThreshold` setting. |
| healthCheckThreshold | 6 | Maximum number of times the health check can fail before a host recycle is initiated. |
| counterThreshold | 0.80 | The threshold at which a performance counter will be considered unhealthy. |

## http

Configuration settings can be found in [http triggers and bindings](functions-bindings-http-webhook#hostjson-settings).

## logging

Controls the logging behaviors of the function app, including Application Insights.

```
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"Function.MyFunction": "Information",
"default": "None"
},
"console": {
...
},
"applicationInsights": {
...
}
}
```


| Property | Default | Description |
|---|---|---|
| fileLoggingMode | debugOnly | Determines the file logging behavior when running in Azure. Options are `never` , `always` , and `debugOnly` . This setting isn't used when running locally. When possible, you should use Application Insights when debugging your functions in Azure. Using `always` negatively impacts your app's cold start behavior and data throughput. The default `debugOnly` setting generates log files when you're debugging using the Azure portal. |
| logLevel | n/a | Object that defines the log category filtering for functions in the app. This setting lets you filter logging for specific functions. For more information, see
|

[console](#console)logging setting.[applicationInsights](#applicationinsights)setting.## managedDependency

Managed dependency is a feature that is currently only supported with PowerShell based functions. It enables dependencies to be automatically managed by the service. When the `enabled`

property is set to `true`

, the `requirements.psd1`

file is processed. Dependencies are updated when any minor versions are released. For more information, see [Managed dependency](functions-reference-powershell#dependency-management) in the PowerShell article.

```
{
"managedDependency": {
"enabled": true
}
}
```


## queues

Configuration settings can be found in [Storage queue triggers and bindings](functions-bindings-storage-queue#host-json).

## sendGrid

Configuration setting can be found in [SendGrid triggers and bindings](functions-bindings-sendgrid#host-json).

## serviceBus

Configuration setting can be found in [Service Bus triggers and bindings](functions-bindings-service-bus).

## singleton

Configuration settings for Singleton lock behavior. For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```
{
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
}
}
```


| Property | Default | Description |
|---|---|---|
| lockPeriod | 00:00:15 | The period that function level locks are taken for. The locks auto-renew. |
| listenerLockPeriod | 00:01:00 | The period that listener locks are taken for. |
| listenerLockRecoveryPollingInterval | 00:01:00 | The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup. |
| lockAcquisitionTimeout | 00:01:00 | The maximum amount of time the runtime will try to acquire a lock. |
| lockAcquisitionPollingInterval | n/a | The interval between lock acquisition attempts. |

## telemetryMode

*This feature is currently in preview.*

Used to enable output of logs and traces in an OpenTelemetry output format to one or more endpoints that support OpenTelemetry. When this setting is set to `OpenTelemetry`

, OpenTelemetry output is used. By default without this setting, all logs, traces, and events are sent to Application Insights using the standard outputs. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## version

This value indicates the schema version of host.json. The version string `"version": "2.0"`

is required for a function app that targets the v2 runtime, or a later version. There are no host.json schema changes between v2 and v3.

## watchDirectories

A set of [shared code directories](functions-reference-csharp#watched-directories) that should be monitored for changes. Ensures that when code in these directories is changed, the changes are picked up by your functions.

```
{
"watchDirectories": [ "Shared" ]
}
```


## watchFiles

An array of one or more names of files that are monitored for changes that require your app to restart. This guarantees that when code in these files is changed, the updates are picked up by your functions.

```
{
"watchFiles": [ "myFile.txt" ]
}
```


## Override host.json values

There may be instances where you wish to configure or modify specific settings in a host.json file for a specific environment, without changing the host.json file itself. You can override specific host.json values by creating an equivalent value as an application setting. When the runtime finds an application setting in the format `AzureFunctionsJobHost__path__to__setting`

, it overrides the equivalent host.json setting located at `path.to.setting`

in the JSON. When expressed as an application setting, the dot (`.`

) used to indicate JSON hierarchy is replaced by a double underscore (`__`

).

For example, say that you wanted to disable Application Insight sampling when running locally. If you changed the local host.json file to disable Application Insights, this change might get pushed to your production app during deployment. The safer way to do this is to instead create an application setting as `"AzureFunctionsJobHost__logging__applicationInsights__samplingSettings__isEnabled":"false"`

in the `local.settings.json`

file. You can see this in the following `local.settings.json`

file, which doesn't get published:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "{storage-account-connection-string}",
"FUNCTIONS_WORKER_RUNTIME": "{language-runtime}",
"AzureFunctionsJobHost__logging__applicationInsights__samplingSettings__isEnabled":"false"
}
}
```


Overriding host.json settings using environment variables follows the ASP.NET Core naming conventions. When the element structure includes an array, the numeric array index should be treated as an additional element name in this path. For more information, see [Naming of environment variables](/en-us/aspnet/core/fundamentals/configuration/#naming-of-environment-variables).


---

<!-- DOCUMENTO FUSIONADO: __configure-encrypt-at-rest-using-cmk_self-hosted-mcp-servers_scenario-database-_b75e88.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _configure-encrypt-at-rest-using-cmk_self-hosted-mcp-servers.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: configure-encrypt-at-rest-using-cmk.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/configure-encrypt-at-rest-using-cmk -->

# Encrypt your application data at rest using customer-managed keys

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Encrypting your function app's application data at rest requires an Azure Storage Account and an Azure Key Vault. These services are used when you run your app from a deployment package.

[Azure Storage provides encryption at rest](../storage/common/storage-service-encryption). You can use system-provided keys or your own, customer-managed keys. This is where your application data is stored when it's not running in a function app in Azure.[Running from a deployment package](run-functions-from-deployment-package)is a deployment feature of App Service. It allows you to deploy your site content from an Azure Storage Account using a Shared Access Signature (SAS) URL.[Key Vault references](../app-service/app-service-key-vault-references)are a security feature of App Service. It allows you to import secrets at runtime as application settings. Use this to encrypt the SAS URL of your Azure Storage Account.

## Set up encryption at rest

### Create an Azure Storage account

First, [create an Azure Storage account](../storage/common/storage-account-create) and [encrypt it with customer managed keys](../storage/common/customer-managed-keys-overview). Once the storage account is created, use the [Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer) to upload package files.

Next, use the Storage Explorer to [generate an SAS](../vs-azure-tools-storage-manage-with-storage-explorer?tabs=windows#generate-a-sas-in-storage-explorer).

Note

Save this SAS URL, this is used later to enable secure access of the deployment package at runtime.

### Configure running from a package from your storage account

Once you upload your file to Blob storage and have an SAS URL for the file, set the `WEBSITE_RUN_FROM_PACKAGE`

application setting to the SAS URL. The following example does it by using Azure CLI:

```
az webapp config appsettings set --name <app-name> --resource-group <resource-group-name> --settings WEBSITE_RUN_FROM_PACKAGE="<your-SAS-URL>"
```


Adding this application setting causes your function app to restart. After the app has restarted, browse to it and make sure that the app has started correctly using the deployment package. If the application didn't start correctly, see the [Run from package troubleshooting guide](run-functions-from-deployment-package#troubleshooting).

### Encrypt the application setting using Key Vault references

Now you can replace the value of the `WEBSITE_RUN_FROM_PACKAGE`

application setting with a Key Vault reference to the SAS-encoded URL. This keeps the SAS URL encrypted in Key Vault, which provides an extra layer of security.

Use the following

command to create a Key Vault instance.`az keyvault create`

`az keyvault create --name "Contoso-Vault" --resource-group <group-name> --location eastus`

Follow

[these instructions to grant your app access](../app-service/app-service-key-vault-references#grant-your-app-access-to-a-key-vault)to your key vault:Use the following

command to add your external URL as a secret in your key vault:`az keyvault secret set`

`az keyvault secret set --vault-name "Contoso-Vault" --name "external-url" --value "<SAS-URL>"`

Use the following

command to create the`az webapp config appsettings set`

`WEBSITE_RUN_FROM_PACKAGE`

application setting with the value as a Key Vault reference to the external URL:`az webapp config appsettings set --settings WEBSITE_RUN_FROM_PACKAGE="@Microsoft.KeyVault(SecretUri=https://Contoso-Vault.vault.azure.net/secrets/external-url/<secret-version>"`

The

`<secret-version>`

will be in the output of the previous`az keyvault secret set`

command.

Updating this application setting causes your function app to restart. After the app has restarted, browse to it make sure it has started correctly using the Key Vault reference.

## How to rotate the access token

It is best practice to periodically rotate the SAS key of your storage account. To ensure the function app does not inadvertently lose access, you must also update the SAS URL in Key Vault.

Rotate the SAS key by navigating to your storage account in the Azure portal. Under

**Settings**>**Access keys**, select the icon to rotate the SAS key.Copy the new SAS URL, and use the following command to set the updated SAS URL in your key vault:

`az keyvault secret set --vault-name "Contoso-Vault" --name "external-url" --value "<SAS-URL>"`

Update the key vault reference in your application setting to the new secret version:

`az webapp config appsettings set --settings WEBSITE_RUN_FROM_PACKAGE="@Microsoft.KeyVault(SecretUri=https://Contoso-Vault.vault.azure.net/secrets/external-url/<secret-version>"`

The

`<secret-version>`

will be in the output of the previous`az keyvault secret set`

command.

## How to revoke the function app's data access

There are two methods to revoke the function app's access to the storage account.

### Rotate the SAS key for the Azure Storage account

If the SAS key for the storage account is rotated, the function app will no longer have access to the storage account, but it will continue to run with the last downloaded version of the package file. Restart the function app to clear the last downloaded version.

### Remove the function app's access to Key Vault

You can revoke the function app's access to the site data by disabling the function app's access to Key Vault. To do this, remove the access policy for the function app's identity. This is the same identity you created earlier while configuring key vault references.

## Summary

Your application files are now encrypted at rest in your storage account. When your function app starts, it retrieves the SAS URL from your key vault. Finally, the function app loads the application files from the storage account.

If you need to revoke the function app's access to your storage account, you can either revoke access to the key vault or rotate the storage account keys, both of which invalidate the SAS URL.

## Frequently Asked Questions

### Is there any additional charge for running my function app from the deployment package?

Only the cost associated with the Azure Storage Account and any applicable egress charges.

### How does running from the deployment package affect my function app?

- Running your app from the deployment package makes
`wwwroot/`

read-only. Your app receives an error when it attempts to write to this directory. - TAR and GZIP formats are not supported.
- This feature is not compatible with local cache.


---

<!-- DOCUMENTO FUSIONADO: self-hosted-mcp-servers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/self-hosted-mcp-servers -->

# Self-hosted remote MCP server on Azure Functions (public preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides two ways of hosting remote MCP servers:

- MCP servers created with the
[Functions MCP extension](functions-bindings-mcp) - MCP servers built with the
[official MCP SDKs](https://modelcontextprotocol.io/docs/sdk)

With the first approach, you can use the Azure Functions programming model with triggers and bindings to build the MCP server. Then, you can host the server remotely by deploying it to a Function app.

If you already have an MCP server created with the official MCP SDKs and just want to host it remotely, the second approach likely suits your needs. You don't need to make any code changes to the server to host it on Azure Functions. Instead, you can add the required Functions artifacts, and the server is ready to be deployed. As such, these servers are referred to as *self-hosted MCP servers*.


This article provides an overview of self-hosted MCP servers and links to relevant articles and samples.

## Custom handlers

Self-hosted MCP servers deploy to the Azure Functions platform as *custom handlers*. Custom handlers are lightweight web servers that receive events from the Functions host. They provide a way to run on the Functions platform applications built with frameworks different from the Functions programming model or in languages not supported out-of-the-box. For more information, see [Azure Functions custom handlers](functions-custom-handlers).

When you deploy an MCP SDK based server to Azure Functions, you must include a *host.json* in your project. The minimal *host.json* looks like this:

```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "python",
"arguments": ["Path to main script file, e.g. hello_world.py"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "npm",
"arguments": ["run", "start"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "dotnet",
"arguments": ["Path to the compiled DLL, e.g. HelloWorld.dll"]
},
"port": "<MCP server port>"
}
}
```


Note

Because the payload deployed to Azure Functions is the content of the `bin/output`

directory, the path to the compiled DLL is relative to that directory, *not* to the project root.

Example not yet available.

Using a `configuration Profile`

value of `mcp-custom-handler`

automatically configures these Functions host settings, which are required for running your MCP server in Azure Functions:

`http.enableProxying`

to`true`

`http.routes`

to`[{ "route": "{*route}" }]`

`extensions.http.routePrefix`

to`""`


This example shows a host.json file with extra custom handler properties set equivalent to using the `mcp-custom-handler`

profile:

```
{
"version": "2.0",
"extensions": {
"http": {
"routePrefix": ""
}
},
"customHandler": {
"description": {
"defaultExecutablePath": "",
"arguments": [""]
},
"http": {
"enableProxying": true,
"defaultAuthorizationLevel": "anonymous",
"routes": [
{
"route": "{*route}",
// Default authorization level is `defaultAuthorizationLevel`
},
{
"route": "admin/{*route}",
"authorizationLevel": "admin"
}
]
}
}
}
```


This table explains the properties of `customHandler.http`

, along with default values:

| Property | What it does | Default value |
|---|---|---|
`enableProxying` |
Controls how the Azure Functions host handles HTTP requests to custom handlers. When `enableProxying` is set to `true` , the Functions host acts as a reverse proxy and forwards the entire HTTP request (including headers, body, query parameters) directly to the custom handler. This setting gives the custom handler full access to the original HTTP request details. When `enableProxying` is `false` , the Functions host processes the request first and transforms it into the Azure Functions request/response format before passing it to the custom handler. |
`false` |
`defaultAuthorizationLevel` |
Controls the authentication requirement for accessing custom handler endpoints. For example, `function` requires a function-specific API key to access. For more information, see
|
`function` |
`route` |
Specifies the URL path pattern that the custom handler responds to. `{*route}` matches any URL path (such as `/` , `/mcp` , `/api/tools` , or `/anything/nested/path` ) and forwards the request to the custom handler. |
`{*route}` |

## Built-in server authentication

OAuth-based authentication and authorization provided by the App Service platform implements the requirements of the [MCP authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), such as issuing 401 challenge and exposing the Protected Resource Metadata (PRM) document. When you enable built-in authentication, clients attempting to access the server are redirected to identity providers like Microsoft Entra ID for authentication before connecting.

For more information, see [Configure built-in server authorization (preview)](../app-service/configure-authentication-mcp) and [Hosting MCP servers on Azure Functions](functions-mcp-tutorial).

## Azure AI Foundry agent integrations

Agents in Azure AI Foundry can be [configured to use tools](functions-mcp-tutorial#configure-azure-ai-foundry-agent-to-use-your-tools) in MCP servers hosted in Azure Functions.

## Register your server in Azure API Center

When you register your MCP server in Azure API Center, you create a private organizational tool catalog. This approach is recommended for sharing MCP servers across your organization with consistent governance and discoverability. For more information, see [Register MCP servers hosted in Azure Functions in Azure API Center](register-mcp-server-api-center).

## Public preview support

The ability to host your own SDK-based MCP servers in Functions is currently in preview and supports these features:

**Stateless**servers that use the**streamable-http**transport. If you need your server to be stateful, consider using the Functions MCP extension.- Servers implemented with the Python, TypeScript, C#, or Java MCP SDKs.
- When running the project locally, you must use the Azure Functions Core Tools (
`func start`

command). You can't currently use`F5`

to start running with the debugger. - Servers must be hosted as
[Flex Consumption plan](flex-consumption-plan)apps.

## Samples

Not yet available.


---

<!-- DOCUMENTO FUSIONADO: scenario-database-changes-azure-sqldb.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-database-changes-azure-sqldb -->

# Quickstart: Respond to Azure SQL Database changes using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this Quickstart, you use Visual Studio Code to build an app that responds to changes in an Azure SQL Database table. After testing the code locally, you deploy it to a new serverless function app running in a Flex Consumption plan in Azure Functions.

The project source uses the Azure Developer CLI (azd) extension with Visual Studio Code to simplify initializing and verifying your project code locally, and deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

Important

While responding to [changes in an Azure SQL database](functions-bindings-azure-mysql-trigger) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension requires[Azure Functions Core Tools](functions-run-local). When this tool isn't available locally, the extension tries to install it by using a package-based installer. You can also install or update the Core Tools package by running`Azure Functions: Install or Update Azure Functions Core Tools`

from the command palette. If you don't have npm or Homebrew installed on your local computer, you must instead[manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

- The
[Azure Developer CLI extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.azure-dev)for Visual Studio Code.

- The
[SQL Server (mssql) extension](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)for Visual Studio Code.

## Initialize the project

You can use the `azd init`

command from the command palette to create a local Azure Functions code project from a template.

In Visual Studio Code, open a folder or workspace in which you want to create your project.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Initialize App (init)`

, and then choose**Select a template**.When prompted, search for and select

`Azure Functions with SQL Triggers and Bindings`

.When prompted, enter a unique environment name, such as

`sqldbchanges`

.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

Before you can run your app locally, you must create the resources in Azure.

## Create Azure resources

This project is configured to use the `azd provision`

command to create a function app in a Flex Consumption plan, along with other required Azure resources that follow current best practices.

In Visual Studio Code, press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Sign In with Azure Developer CLI`

, and then sign in using your Azure account.Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Provision Azure resources (provision)`

to create the required Azure resources.When prompted in the Terminal window, provide these required deployment parameters:

Prompt Description Select an Azure Subscription to use Select the subscription in which you want your resources to be created. *location*deployment parameterAzure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. *vnetEnabled*deployment parameterWhile the template supports creating resources inside a virtual network, to simplify deployment and testing, choose `False`

.

The `azd provision`

command uses your response to these prompts with the Bicep configuration files to create and configure these required Azure resources, following the latest best practices:

- Flex Consumption plan and function app
- Azure SQL Database (default name: ToDo)
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)

Post-provision hooks also generate the *local.settings.json* file, which is required to run locally. This file contains the settings required to connect to your database in Azure.

## Review the code (optional)

The sample defines two functions:

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`httptrigger-sql-output` |
|

`ToDo`

table.`ToDoTrigger`

[sql_trigger.cs](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql/blob/main/sql_trigger.cs)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [ToDoItem.cs](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql/blob/main/ToDoItem.cs).

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`http_trigger_sql_output` |
|

`ToDo`

table.`httptrigger-sql-output`

[sql_trigger_todo](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql/blob/main/function_app.py#L15C5-L15C21)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [todo_item.py](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql/blob/main/todo_item.py).

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`httpTriggerSqlOutput` |
|

`ToDo`

table.`sqlTriggerToDo`

[sql_trigger.ts](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql/blob/main/src/functions/sql_trigger.ts)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [ToDoItem.ts](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql/blob/main/src/models/ToDoItem.ts).

Both functions use the app-level `AZURE_SQL_CONNECTION_STRING_KEY_*`

environment variables that define an identity-based connection to the Azure SQL Database instance using Microsoft Entra ID authentication. These environment variables are created for you both in Azure (function app settings) and locally (local.settings.json) during the `azd provision`

operation.

## Connect to the SQL database

You can use the SQL Server (mssql) extension for Visual Studio Code to connect to the new database. This extension helps you make updates in the `ToDo`

table to run the SQL trigger function.

Press

`F1`and in the command palette search for and run the command`MS SQL: Add Connection`

.In the

**Connection dialog**, change**Input type**to**Browse Azure**and then set these remaining options:Option Choose Description **Server**Your SQL Server instance By default, all servers accessible to your Azure account are displayed. Use **Subscription**,**Resource group**, and**Location**to help filter the servers list.**Database**`ToDo`

The database created during the provisioning process. **Authentication type****Microsoft Entra ID**If you aren't already signed-in, select **Sign in**and sign in to your Azure account.**Tenant ID**The specific account tenant. If your account has more than one tenant, choose the correct tenant for your subscription. Select

**Connect**to connect to your database. The connection uses your local user account, which is granted admin permissions in the hosting server and mapped to`dbo`

in the database.In the

**SQL Server**view, locate and expand**Connections**and then your new server in SQL Server explorer. Expand**Tables**and verify that the`ToDo`

table exists. If it doesn't exist, you might need run`azd provision`

again and check for errors.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to your new function app in Azure.

Press

`F1`and in the command palette search for and run the command`Azurite: Start`

.To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar.The

**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel, and you can see the name of the function that's running locally.

With the app running, you can verify and debug both function triggers.

To verify the HTTP trigger function that writes to a SQL output binding:

Copy this JSON object, which you can also find in the

`test.http`

project file:`{ "id": "11111111-1111-1111-1111-111111111111", "order": 1, "title": "Test Todo Item", "url": "https://example.com", "completed": false }`

This data represents a row that you insert in your SQL database when you call the HTTP endpoint. The output binding translates the data object into an

`INSERT`

operation in the database.With the app running, in the

**Azure**view under**Workspace**expand**Local project**>**Functions**.Right-select your HTTP function (or

`Ctrl`+click on macOS), select**Execute function now**, paste the copied JSON data, and press`Enter`.The function handles the HTTP request and writes the item to the connected SQL database and returns the created object.

Back in the SQL Server explorer, right-select the

`ToDo`

table (or`Ctrl`+click on macOS), and choose**Select Top 1000**. When the query executes, it returns the inserted or updated row.Repeat Step 3 and resend the same data object with the same ID. This time, the output binding performs an

`UPDATE`

operation instead of an`INSERT`

and modifies the existing row in the database.

When you're done, type `Ctrl`+`C` in the terminal to stop the Core Tools process.

## Deploy to Azure

You can run the `azd deploy`

command from Visual Studio Code to deploy the project code to your already provisioned resources in Azure.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Deploy to Azure (deploy)`

.The

`azd deploy`

command packages and deploys your code to the deployment container. The app is then started and runs in the deployed package.After the command completes successfully, your app is running in Azure. Make a note of the

`Endpoint`

value, which is the URL of your function app running in Azure.

## Invoke the function on Azure

In Visual Studio Code, press

`F1`and in the command palette search for and run the command`Azure: Open in portal`

, select`Function app`

, and choose your new app. Sign in with your Azure account, if necessary.Select

**Log stream**in the left pane, which connects to the Application Insights logs for your app.Return to Visual Studio Code to run both the functions in Azure.


Press

`F1`to open the command palette, search for and run the command`Azure Functions: Execute Function Now...`

.Search for and select your remote function app from the list, then select the HTTP trigger function.

As before, paste your JSON object data in

**Enter payload body**and press`Enter`.`{ "id": "11111111-1111-1111-1111-111111111111", "order": 1, "title": "Test Todo Item", "url": "https://example.com", "completed": false }`

To perform an

`INSERT`

instead of an`UPDATE`

, replace the`id`

with a new GUID value.Return to the portal and view the execution output in the log window.


## Clean up resources

When you're done working with your function app and related resources, you can use this command to delete the function app and its related resources from Azure and avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.


---

<!-- DOCUMENTO FUSIONADO: ___functions-bindings-warmup_functions-bindings-cache-trigger-redislist_function_7fe6b7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-bindings-warmup_functions-bindings-cache-trigger-redislist_functions_cecfc5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-warmup_functions-bindings-cache-trigger-redislist.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-warmup.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-warmup -->

# Azure Functions warmup trigger

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with the warmup trigger in Azure Functions. A warmup trigger is invoked when an instance is added to scale a running function app. The warmup trigger lets you define a function that runs when a new instance of your function app is started. You can use a warmup trigger to preload custom dependencies so your functions are ready to start processing requests immediately. Some actions for a warmup trigger might include opening connections, loading dependencies, or running any other custom logic before your app begins receiving traffic.

The following considerations apply when using a warmup trigger:

- There can be only one warmup trigger function per function app, and it can't be invoked after the instance is already running.
- The name of the function that is the warmup trigger for your app should be
`warmup`

(case-insensitive). - The warmup trigger isn't available to apps running on the
[Consumption plan](consumption-plan). - The warmup trigger isn't supported on version 1.x of the Functions runtime.
- Support for the warmup trigger is provided by default in all development environments. You don't have to manually install the package or register the extension.
- The warmup trigger is only called during scale-out operations, not during restarts or other nonscaling startups. Make sure your logic can load all required dependencies without relying on the warmup trigger. Lazy loading is a good pattern to achieve this goal.
- Dependencies created by warmup trigger should be shared with other functions in your app. To learn more, see
[Static clients](manage-connections#static-clients). - If the
[built-in authentication](../app-service/overview-authentication-authorization)(also known as Easy Auth) is used,[HTTPS Only](../app-service/configure-ssl-bindings#enforce-https)should be enabled for the warmup trigger to get invoked.

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that runs on each new instance when added to your app.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public static class Warmup
{
[Function(nameof(Warmup))]
public static void Run([WarmupTrigger] object warmupContext, FunctionContext context)
{
var logger = context.GetLogger(nameof(Warmup));
logger.LogInformation("Function App instance is now warm!");
}
}
}
```


The following example shows a warmup trigger that runs when each new instance is added to your app.

```
@FunctionName("Warmup")
public void warmup( @WarmupTrigger Object warmupContext, ExecutionContext context) {
context.getLogger().info("Function App instance is warm.");
}
```


The following example shows a [JavaScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
const { app } = require('@azure/functions');
app.warmup('warmupTrigger', {
handler: (warmupContext, context) => {
context.log('Function App instance is warm.');
},
});
```


The following example shows a [TypeScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
import { app, InvocationContext, WarmupContext } from '@azure/functions';
export async function warmupFunction(warmupContext: WarmupContext, context: InvocationContext): Promise<void> {
context.log('Function App instance is warm.');
}
app.warmup('warmup', {
handler: warmupFunction,
});
```


Here's the *function.json* file:

```
{
"bindings": [
{
"type": "warmupTrigger",
"direction": "in",
"name": "warmupContext"
}
]
}
```


PowerShell example code pending.

The following example shows a warmup trigger in a *function.json* file and a [Python function](functions-reference-python) that runs on each new instance when it'is added to your app.

Your function must be named `warmup`

(case-insensitive) and there can only be one warmup function per app.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.warm_up_trigger('warmup')
def warmup(warmup) -> None:
logging.info('Function App instance is warm')
```


For more information, see [Configuration](#configuration).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `WarmupTrigger`

attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

Use the `WarmupTrigger`

attribute to define the function. This attribute has no parameters.

## Annotations

Warmup triggers don't require annotations. Just use a name of `warmup`

(case-insensitive) for the `FunctionName`

annotation.

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Required - must be set to `warmupTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code. A `name` of `warmupContext` is recommended for the binding parameter. |

See the [Example section](#example) for complete examples.

## Usage

The following considerations apply to using a warmup function in C#:

- Your function must be named
`warmup`

(case-insensitive) using the`Function`

attribute. - A return value attribute isn't required.
- Use the
`Microsoft.Azure.Functions.Worker.Extensions.Warmup`

package - You can pass an object instance to the function.

Your function must be named `warmup`

(case-insensitive) using the `FunctionName`

annotation.

The function type in function.json must be set to `warmupTrigger`

.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cache-trigger-redislist.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redislist -->

# RedisListTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function.

For more information about Azure Cache for Redis triggers and bindings, [Redis Extension for Azure Functions](https://github.com/Azure/azure-functions-redis-extension/tree/main).

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Lists | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

Redis triggers aren't currently supported for functions running on a [Consumption plan](consumption-plan) or a [Flex Consumption plan](flex-consumption-plan).

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

The following sample polls the key `listTest`

.:

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisListTrigger
{
public class SimpleListTrigger
{
private readonly ILogger<SimpleListTrigger> logger;
public SimpleListTrigger(ILogger<SimpleListTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimpleListTrigger))]
public void Run(
[RedisListTrigger(Common.connectionStringSetting, "listTest")] string entry)
{
logger.LogInformation(entry);
}
}
}
```


The following sample polls the key `listTest`

at a localhost Redis instance at `redisLocalhost`

:

```
package com.function.RedisListTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimpleListTrigger {
@FunctionName("SimpleListTrigger")
public void run(
@RedisListTrigger(
name = "req",
connection = "redisConnectionString",
key = "listTest",
pollingIntervalInMs = 1000,
maxBatchSize = 1)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample uses the same `index.js`

file, with binding data in the `function.json`

file.

Here's the `index.js`

file:

```
module.exports = async function (context, entry) {
context.log(entry);
}
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This sample uses the same `run.ps1`

file, with binding data in the `function.json`

file.

Here's the `run.ps1`

file:

```
param($entry, $TriggerMetadata)
Write-Host $entry
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file.

The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

Here's the `__init__.py`

file:

```
import logging
def main(entry: str):
logging.info(entry)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
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

`Key`

`INameResolver`

.`PollingIntervalInMs`

`1000`

`MessagesPerWorker`

`100`

`Count`

`COUNT`

argument in [and](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`10`

`ListPopFromBeginning`

[, or to pop entries from the end using](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`true`

## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
"entry" | ||
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`listPopFromBeginning`

`true`

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json Property | Description | Optional | Default |
|---|---|---|---|
`type` |
Name of the trigger. | No | |
`listPopFromBeginning` |
Whether to delete the stream entries after the function has run. Set to `true` . |
Yes | `true` |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`INameResolver`

.`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`name`

`direction`

`in`

.See the Example section for complete examples.

## Usage

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function. The trigger polls Redis at a configurable fixed interval, and uses [ LPOP](https://redis.io/commands/lpop/) and

[to pop entries from the lists.](https://redis.io/commands/rpop/)

`RPOP`

| Type | Description |
|---|---|
`byte[]` |
The message from the channel. |
`string` |
The message from the channel. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |


---

<!-- DOCUMENTO FUSIONADO: functions-container-apps-hosting.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-container-apps-hosting -->

# Azure Container Apps hosting of Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

A new hosting method for running Azure Functions directly in Azure Container Apps is now available. See [Native Azure Functions Support in Azure Container Apps](https://techcommunity.microsoft.com/blog/appsonazureblog/announcing-native-azure-functions-support-in-azure-container-apps/4414039). This integration allows you to use the full features and capabilities of Azure Container Apps. You also benefit from the functions programming model and simplicity of autoscaling provided by Azure Functions.

We recommend this approach for most new workloads. For more information, see [Azure Functions on Azure Container Apps](../container-apps/functions-overview).

Azure Functions provides integrated support for developing, deploying, and managing containerized function apps on [Azure Container Apps](../container-apps/overview). Use Azure Container Apps to host your function app containers when you need to run your event-driven functions in Azure in the same environment as other microservices, APIs, websites, workflows, or any container hosted programs. Container Apps hosting lets you run your functions in a fully managed, Kubernetes-based environment with built-in support for open-source monitoring, mTLS, Dapr, and Kubernetes Event-driven Autoscaling (KEDA).

You can write your function code in any [language stack supported by Functions](supported-languages). You can use the same Functions triggers and bindings with event-driven scaling. You can also use existing Functions client tools and the Azure portal to create containers, deploy function app containers to Container Apps, and configure continuous deployment.

Container Apps integration also means that network and observability configurations, which are defined at the Container App environment level, apply to your function app as they do to all microservices running in a Container Apps environment. You also get the other cloud-native capabilities of Container Apps, including KEDA, Dapr, Envoy. You can still use Application Insights to monitor your functions executions, and your function app can access the same virtual networking resources provided by the environment.

For a general overview of container hosting options for Azure Functions, see [Linux container support in Azure Functions](container-concepts).

## Hosting and workload profiles

There are two primary plans for Container Apps: a serverless [Consumption plan](../container-apps/plans#consumption) and a [Dedicated plan](../container-apps/plans#dedicated). Both can be used in Workload profiles environment types, with workload profiles determining the compute and memory resources available to your apps. A workload profile determines the amount of compute and memory resources available to container apps deployed in an environment. These profiles are configured to fit the different needs of your applications.

The Consumption workload profile is the default profile added to every Workload profiles environment type. You can add Dedicated workload profiles to your environment as you create an environment or after it's created. To learn more about workload profiles, see [Workload profiles in Azure Container Apps](../container-apps/workload-profiles-overview).

Container Apps hosting of containerized function apps is supported in all [regions that support Container Apps](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?products=container-apps).

If your app doesn't have specific hardware requirements, you can run your environment either in a Consumption plan or in a Dedicated plan using the default Consumption workload profile. When running functions on Container Apps, you're charged only for the Container Apps usage. For more information, see the [Azure Container Apps pricing page](https://azure.microsoft.com/pricing/details/container-apps/).

Azure Functions on Azure Container Apps supports GPU-enabled hosting in the Dedicated plan with workload profiles.

To learn how to create and deploy a function app container to Container Apps in the default Consumption plan, see [Create your first containerized functions on Azure Container Apps](functions-deploy-container-apps).

To learn how to create a Container Apps environment with workload profiles and deploy a function app container to a specific workload, see [Container Apps workload profiles](functions-how-to-custom-container#container-apps-workload-profiles).

## Functions in containers

To use Container Apps hosting, your code must run on a function app in a Linux container that you create and maintain. Functions maintains a set of [language-specific base images](https://mcr.microsoft.com/catalog?search=functions) that you can use to generate your containerized function apps.

When you create a code project using [Azure Functions Core Tools](functions-run-local) and include the [ --docker option](functions-core-tools-reference#func-init), Core Tools generates the Dockerfile with the correct base image, which you can use as a starting point when creating your container.

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

When you make changes to your functions code, you must rebuild and republish your container image. For more information, see [Update an image in the registry](functions-how-to-custom-container#update-an-image-in-the-registry).

## Deployment options

Azure Functions currently supports the following methods of deploying a containerized function app to Azure Container Apps:

[Apache Maven](https://github.com/microsoft/azure-maven-plugins/wiki/Azure-Functions:-Configuration-Details#properties-for-azure-container-apps-hosting-of-azure-functions)[ARM templates](/en-us/azure/templates/microsoft.web/sites?pivots=deployment-language-arm-template)[Azure CLI](functions-deploy-container-apps)[Azure Developer CLI (azd)](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/azdtemplates)[Azure Functions Core Tools](functions-run-local#deploy-containers)[Azure Pipeline tasks](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/AzurePipelineTasks)[Azure portal](https://aka.ms/funconacablade)[Bicep files](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/Biceptemplates)[GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/GitHubActions)[Visual Studio Code](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/VSCode%20Sample)

You can continuously deploy your containerized apps from source code using either [Azure Pipelines](functions-how-to-azure-devops?pivots=v1#deploy-a-container) or [GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/GitHubActions). The continuous deployment feature of Functions isn't currently supported when deploying to Container Apps.

## Managed identity authorization

For the best security, you should connect to remote services using Microsoft Entra authentication and managed identity authorization. You can use managed identities for these connections:

When running in Container Apps, you can use Microsoft Entra ID with managed identities for all binding extensions that support managed identities. Currently, only these binding extensions support event-driven scaling when using managed identity authentication:

- Azure Event Hubs
- Azure Queue Storage
- Azure Service Bus

For other bindings, use fixed replicas when using managed identity authentication. For more information, see the [Functions developer guide](functions-reference#connections).

## Virtual network integration

When you host your function apps in a Container Apps environment, your functions are able to take advantage of both internally and externally accessible virtual networks. To learn more about environment networks, see [Networking in Azure Container Apps environment](../container-apps/networking).

## Event-driven scaling

All Functions triggers can be used in your containerized function app. However, only these triggers can dynamically scale (from zero instances) based on received events when running in a Container Apps environment:

- Azure Cosmos DB (KEDA connection)
- Azure Event Grid
- Azure Event Hubs
- Azure Blob Storage (Event Grid based)
- Azure Queue Storage
- Azure Service Bus
- Durable Functions (MSSQL storage provider)
- HTTP
- Kafka
- Timer

Azure Functions on Container Apps is designed to configure the scale parameters and rules as per the event target. You don't need to worry about configuring the KEDA scaled objects. You can still set minimum and maximum replica count when creating or modifying your function app. The following Azure CLI command sets the minimum and maximum replica count when creating a new function app in a Container Apps environment from an Azure Container Registry:

```
az functionapp create --name <APP_NAME> --resource-group <MY_RESOURCE_GROUP> --max-replicas 15 --min-replicas 1 --storage-account <STORAGE_NAME> --environment MyContainerappEnvironment --image <LOGIN_SERVER>/azurefunctionsimage:v1 --registry-username <USERNAME> --registry-password <SECURE_PASSWORD> --registry-server <LOGIN_SERVER>
```


The following command sets the same minimum and maximum replica count on an existing function app:

```
az functionapp config container set --name <APP_NAME> --resource-group <MY_RESOURCE_GROUP> --max-replicas 15 --min-replicas 1
```


## Managed resource groups

Azure Functions on Container Apps runs your containerized function app resources in specially managed resource groups. These managed resource groups help protect the consistency of your apps by preventing unintended or unauthorized modification or deletion of resources in the managed group, even by service principals.

A managed resource group is created for you the first time you create function app resources in a Container Apps environment. Container Apps resources required by your containerized function app run in this managed resource group. Any other function apps that you create in the same environment use this existing group.

A managed resource group gets removed automatically after all function app container resources are removed from the environment. While the managed resource group is visible, any attempts to modify or remove the managed resource group result in an error. To remove a managed resource group from an environment, remove all of the function app container resources and it gets removed for you.

If you run into any issues with these managed resource groups, you should contact support.

## Application logging

You can monitor your containerized function app hosted in Container Apps using Azure Monitor Application Insights in the same way you do with apps hosted by Azure Functions. For more information, see [Monitor Azure Functions](monitor-functions).

For bindings that support event-driven scaling, scale events are logged as `FunctionsScalerInfo`

and `FunctionsScalerError`

events in your Log Analytics workspace. For more information, see [Application Logging in Azure Container Apps](../container-apps/logging).

## Considerations for Container Apps hosting

Keep in mind the following considerations when deploying your function app containers to Container Apps:

- These limitations apply to Kafka triggers:
- The protocol value of
`ssl`

isn't supported when hosted on Container Apps. Use a[different protocol value](functions-bindings-kafka-trigger?pivots=programming-language-csharp#attributes). - For a Kafka trigger to dynamically scale when connected to Event Hubs, the
`username`

property must resolve to an application setting that contains the actual username value. When the default`$ConnectionString`

value is used, the Kafka trigger isn't able to cause the app to scale dynamically.

- The protocol value of
- For the built-in Container Apps
[policy definitions](../container-apps/policy-reference#policy-definitions), currently only environment-level policies apply to Azure Functions containers. - By default, a containerized function app monitors port 80 for incoming requests. If your app must use a different port, use the
to change this default port.`WEBSITES_PORT`

application setting - You aren't currently able to use built-in continuous deployment features when hosting on Container Apps. You must instead deploy from source code using either
[Azure Pipelines](functions-how-to-azure-devops?pivots=v1#deploy-a-container)or[GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/GitHubActions). - You currently can't move a Container Apps hosted function app deployment between resource groups or between subscriptions. Instead, you would have to recreate the existing containerized app deployment in a new resource group, subscription, or region.
- When using Container Apps, you don't have direct access to the lower-level Kubernetes APIs.
- The
`containerapp`

extension conflicts with the`appservice-kube`

extension in Azure CLI. If you have previously published apps to Azure Arc, run`az extension list`

and make sure that`appservice-kube`

isn't installed. If it is, you can remove it by running`az extension remove -n appservice-kube`

.


---

<!-- DOCUMENTO FUSIONADO: __functions-bindings-event-grid_functions-create-maven-intellij__functions-bindi_de312e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-event-grid_functions-create-maven-intellij.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-event-grid.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid -->

# Azure Event Grid bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This reference shows how to connect to Azure Event Grid using Azure Functions triggers and bindings.

Event Grid is an Azure service that sends HTTP requests to notify you about events that happen in publishers. A *publisher* is the service or resource that originates the event. For example, an Azure blob storage account is a publisher, and [a blob upload or deletion is an event](../storage/blobs/storage-blob-event-overview). Some [Azure services have built-in support for publishing events to Event Grid](../event-grid/concepts#event-sources).

Event *handlers* receive and process events. Azure Functions is one of several [Azure services that have built-in support for handling Event Grid events](../event-grid/overview#event-handlers). Functions provides an Event Grid trigger, which invokes a function when an event is received from Event Grid. A similar output binding can be used to send events from your function to an [Event Grid custom topic](../event-grid/post-to-custom-topic).

You can also use an HTTP trigger to handle Event Grid Events. To learn more, see [Receive events to an HTTP endpoint](../event-grid/receive-events). We recommend using the Event Grid trigger over HTTP trigger.

| Action | Type |
|---|---|
| Run a function when an Event Grid event is dispatched |
|

[Output binding](functions-bindings-event-grid-output)[HTTP endpoint](../event-grid/receive-events)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid), version 3.x.

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

Considerations for the Event Grid extension:

- Event Grid extension versions earlier than 3.x don't support
[CloudEvents schema](../event-grid/cloudevents-schema#azure-functions). To consume this schema, instead use an HTTP trigger. - The Event Grid output binding is only available for Functions 2.x and higher.

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to `Stream`

, and to types from [Azure.Messaging](/en-us/dotnet/api/azure.messaging) is in preview.

**Event Grid trigger**

When you want the function to process a single event, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions tries to deserialize the JSON data of the event into a plain-old CLR object (POCO) type. |
`string` |
The event as a string. |
1 |

[CloudEvent](/en-us/dotnet/api/azure.messaging.cloudevent)1[EventGridEvent](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridevent)1When you want the function to process a batch of events, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
`CloudEvent[]` 1,`EventGridEvent[]` 1,`string[]` ,`BinaryData[]` 1 |
An array of events from the batch. Each entry represents one event. |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventGrid 3.3.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid/3.3.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Event Grid output binding**

When you want the function to write a single event, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. |
`byte[]` |
The bytes of the event message. |
| JSON serializable types | An object representing a JSON event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventGridPublisherClient](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient) with other types from [Azure.Messaging.EventGrid](/en-us/dotnet/api/azure.messaging.eventgrid) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## host.json settings

The Event Grid trigger uses a webhook HTTP request, which can be configured using the same [ host.json settings as the HTTP Trigger](functions-bindings-http-webhook#hostjson-settings).

## Next steps

- If you have questions, submit an issue to the team
[here](https://github.com/Azure/azure-sdk-for-net/issues) [Event Grid trigger](functions-bindings-event-grid-trigger)[Event Grid output binding](functions-bindings-event-grid-output)[Run a function when an Event Grid event is dispatched](functions-bindings-event-grid-trigger)[Dispatch an Event Grid event](functions-bindings-event-grid-trigger)


---

<!-- DOCUMENTO FUSIONADO: functions-create-maven-intellij.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-maven-intellij -->

# Create your first Java function in Azure using IntelliJ

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Java and IntelliJ to create an Azure function.

Specifically, this article shows you:

- How to create an HTTP-triggered Java function in an IntelliJ IDEA project.
- Steps for testing and debugging the project in the integrated development environment (IDE) on your own computer.
- Instructions for deploying the function project to Azure Functions.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - An
[Azure supported Java Development Kit (JDK)](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21. (Java 21 is currently supported on Linux only) - An
[IntelliJ IDEA](https://www.jetbrains.com/idea/download/)Ultimate Edition or Community Edition installed [Maven 3.5.0+](https://maven.apache.org/download.cgi)- Latest
[Function Core Tools](https://github.com/Azure/azure-functions-core-tools)

## Install plugin and sign in

To install the Azure Toolkit for IntelliJ and then sign in, follow these steps:

In IntelliJ IDEA's

**Settings/Preferences**dialog (Ctrl+Alt+S), select**Plugins**. Then, find the**Azure Toolkit for IntelliJ**in the**Marketplace**and select**Install**. After it's installed, select**Restart**to activate the plugin.To sign in to your Azure account, open the

**Azure Explorer**sidebar, and then select the**Azure Sign In**icon in the bar on top (or from the IDEA menu, select**Tools > Azure > Azure Sign in**).In the

**Azure Sign In**window, select**OAuth 2.0**, and then select**Sign in**. For other sign-in options, see[Sign-in instructions for the Azure Toolkit for IntelliJ](/en-us/azure/developer/java/toolkit-for-intellij/sign-in-instructions).In the browser, sign in with your account and then go back to IntelliJ. In the

**Select Subscriptions**dialog box, select the subscriptions that you want to use, then select**Select**.

## Create your local project

To use Azure Toolkit for IntelliJ to create a local Azure Functions project, follow these steps:

Open IntelliJ IDEA's

**Welcome**dialog, select**New Project**to open a new project wizard, then select**Azure Functions**.Select

**Http Trigger**, then select**Next**and follow the wizard to go through all the configurations in the following pages. Confirm your project location, then select**Finish**. IntelliJ IDEA then opens your new project.

## Run the project locally

To run the project locally, follow these steps:

Important

You must have the JAVA_HOME environment variable set correctly to the JDK directory that is used during code compiling using Maven. Make sure that the version of the JDK is at least as high as the `Java.version`

setting.

Navigate to

*src/main/java/org/example/functions/HttpTriggerJava.java*to see the code generated. Beside line 17, you should see a green**Run**button. Select it and then select**Run 'Functions-azur...'**. You should see your function app running locally with a few logs.You can try the function by accessing the displayed endpoint from browser, such as

`http://localhost:7071/api/HttpTriggerJava?name=Azure`

.The log is also displayed in your IDEA. Stop the function app by selecting

**Stop**.

## Debug the project locally

To debug the project locally, follow these steps:

Select the

**Debug**button in the toolbar. If you don't see the toolbar, enable it by choosing**View**>**Appearance**>**Toolbar**.Select line 20 of the file

*src/main/java/org/example/functions/HttpTriggerJava.java*to add a breakpoint. Access the endpoint`http://localhost:7071/api/HttpTriggerJava?name=Azure`

again and you should find that the breakpoint is hit. You can then try more debug features like**Step**,**Watch**, and**Evaluation**. Stop the debug session by selecting**Stop**.

## Create the function app in Azure

Use the following steps create a function app and related resources in your Azure subscription:

In Azure Explorer in your IDEA, right-click

**Function App**and then select**Create**.Select

**More Settings**and provide the following information at the prompts:Prompt Selection **Subscription**Choose the subscription to use. **Resource Group**Choose the resource group for your function app. **Name**Specify the name for a new function app. Here you can accept the default value. **Platform**Select **Windows-Java 17**or another platform as appropriate.**Region**For better performance, choose a [region](https://azure.microsoft.com/regions/)near you.**Hosting Options**Choose the hosting options for your function app. **Plan**Choose the App Service plan pricing tier you want to use, or select **+**to create a new App Service plan.Important

To create your app in the Flex Consumption plan, select

**Flex Consumption**. The[Flex Consumption plan](flex-consumption-plan)is currently in preview.Select

**OK**. A notification is displayed after your function app is created.

## Deploy your project to Azure

To deploy your project to Azure, follow these steps:

Select and expand the Azure icon in IntelliJ Project explorer, then select

**Deploy to Azure -> Deploy to Azure Functions**.You can select the function app from the previous section. To create a new one, select

**+**on the**Function**line. Type in the function app name and choose the proper platform. Here, you can accept the default value. Select**OK**and the new function app you created is automatically selected. Select**Run**to deploy your functions.

## Manage function apps from IDEA

To manage your function apps with **Azure Explorer** in your IDEA, follow these steps:

Select

**Function App**to see all your function apps listed.Select one of your function apps, then right-click and select

**Show Properties**to open the detail page.Right-click your

**HttpTrigger-Java**function app, then select**Trigger Function in Browser**. You should see that the browser is opened with the trigger URL.

## Add more functions to the project

To add more functions to your project, follow these steps:

Right-click the package

**org.example.functions**and select**New -> Azure Function Class**.Fill in the class name

**HttpTest**and select**HttpTrigger**in the create function class wizard, then select**OK**to create. In this way, you can create new functions as you want.

## Cleaning up functions

Select one of your function apps using **Azure Explorer** in your IDEA, then right-click and select **Delete**. This command might take several minutes to run. When it's done, the status refreshes in **Azure Explorer**.

## Next steps

You've created a Java project with an HTTP triggered function, run it on your local machine, and deployed it to Azure. Now, extend your function by continuing to the following article:


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-cache-trigger-redisstream_functions-bindings-openai.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cache-trigger-redisstream.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redisstream -->

# RedisStreamTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The `RedisStreamTrigger`

reads new entries from a stream and surfaces those elements to the function.

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Streams | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

Redis triggers aren't currently supported for functions running on a [Consumption plan](consumption-plan) or a [Flex Consumption plan](/en-us/azure/azure-functions/flex-consumption-plan).

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisStreamTrigger
{
internal class SimpleStreamTrigger
{
private readonly ILogger<SimpleStreamTrigger> logger;
public SimpleStreamTrigger(ILogger<SimpleStreamTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimpleStreamTrigger))]
public void Run(
[RedisStreamTrigger(Common.connectionStringSetting, "streamKey")] string entry)
{
logger.LogInformation(entry);
}
}
}
```


```
package com.function.RedisStreamTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimpleStreamTrigger {
@FunctionName("SimpleStreamTrigger")
public void run(
@RedisStreamTrigger(
name = "req",
connection = "redisConnectionString",
key = "streamTest",
pollingIntervalInMs = 1000,
maxBatchSize = 1)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample uses the same `index.js`

file, with binding data in the `function.json`

file.

Here's the `index.js`

file:

```
module.exports = async function (context, entry) {
context.log(entry);
}
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisStreamTrigger",
"connection": "redisConnectionString",
"key": "streamTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This sample uses the same `run.ps1`

file, with binding data in the `function.json`

file.

Here's the `run.ps1`

file:

```
param($entry, $TriggerMetadata)
Write-Host ($entry | ConvertTo-Json)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisStreamTrigger",
"connection": "redisConnectionString",
"key": "streamTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file.

Here's the `__init__.py`

file:

```
import logging
def main(entry: str):
logging.info(entry)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisStreamTrigger",
"connection": "redisConnectionString",
"key": "streamTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


## Attributes

| Parameters | Description | Required | Default |
|---|---|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Key`

`PollingIntervalInMs`

`1000`

`MessagesPerWorker`

`100`

`Count`

`10`

`DeleteAfterProcess`

`false`

## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
`entry` |
Yes | |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`deleteAfterProcess`

`false`

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json Properties | Description | Required | Default |
|---|---|---|---|
`type` |
Yes | ||
`deleteAfterProcess` |
Optional | `false` |
|
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`name`

`direction`

See the Example section for complete examples.

## Usage

The `RedisStreamTrigger`

Azure Function reads new entries from a stream and surfaces those entries to the function.

The trigger polls Redis at a configurable fixed interval, and uses [ XREADGROUP](https://redis.io/commands/xreadgroup/) to read elements from the stream.

The consumer group for all instances of a function is the name of the function, that is, `SimpleStreamTrigger`

for the [StreamTrigger sample](https://github.com/Azure/azure-functions-redis-extension/blob/main/samples/dotnet/RedisStreamTrigger/SimpleStreamTrigger.cs).

Each functions instance uses the [ WEBSITE_INSTANCE_ID](/en-us/azure/app-service/reference-app-settings?tabs=kudu%2Cdotnet#scaling) or generates a random GUID to use as its consumer name within the group to ensure that scaled out instances of the function don't read the same messages from the stream.

| Type | Description |
|---|---|
`byte[]` |
The message from the channel. |
`string` |
The message from the channel. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-openai.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai -->

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
