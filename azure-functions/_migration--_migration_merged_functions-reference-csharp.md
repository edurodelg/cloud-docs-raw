---
merged_at: 2026-01-28T07:43:39.527330
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/migration/migrate-aws-lambda-to-azure-functions -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/migration/migrate-plan-consumption-to-flex -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-csharp -->

# Azure Functions legacy C# script (.csx) developer reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article is an introduction to developing Azure Functions by using C# script (*.csx*).

Important

C# script apps run in the host process and are supported primarily to provide a convenient in-portal experience to help you quickly get started creating and running C# functions. For production-quality apps, you should instead develop your C# functions locally as a [compiled C# class library project that uses the isolated process model](dotnet-isolated-process-guide). To learn how to migrate a C# script project to a C# class library (isolated worker) project, see [Convert a C# script app to a C# project](#convert-a-c-script-app-to-a-c-project).

Azure Functions lets you develop functions using C# in one of the following ways:

| Type | Execution process | Code extension | Development environment | Reference |
|---|---|---|---|---|
| C# script | in-process | .csx |
|

[This article](#create-a-c-script-app)[Visual Studio](functions-develop-vs)[Visual Studio Code](functions-develop-vs-code)[Core Tools](functions-run-local)[.NET isolated worker process functions](dotnet-isolated-process-guide)[Visual Studio](functions-develop-vs)[Visual Studio Code](functions-develop-vs-code)[Core Tools](functions-run-local)[In-process C# class library functions](functions-dotnet-class-library)Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

## How .csx works

Data flows into your C# function via method arguments. Argument names are specified in a `function.json`

file, and there are predefined names for accessing things like the function logger and cancellation tokens.

The *.csx* format allows you to write less "boilerplate" and focus on writing just a C# function. Instead of wrapping everything in a namespace and class, just define a `Run`

method. Include any assembly references and namespaces at the beginning of the file as usual.

A function app's *.csx* files are compiled when an instance is initialized. This compilation step means things like cold start may take longer for C# script functions compared to C# class libraries. This compilation step is also why C# script functions are editable in the Azure portal, while C# class libraries aren't.

C# script code always runs in the same process as the Functions host.

## Folder structure

The folder structure for a C# script project looks like the following example:

```
FunctionsProject
| - MyFirstFunction
| | - run.csx
| | - function.json
| | - function.proj
| - MySecondFunction
| | - run.csx
| | - function.json
| | - function.proj
| - host.json
| - extensions.csproj
| - bin
```


There's a shared [host.json](functions-host-json) file that can be used to configure the function app. Each function has its own code file (.csx) and binding configuration file (function.json).

The binding extensions required in [version 2.x and later versions](functions-versions) of the Functions runtime are defined in the `extensions.csproj`

file, with the actual library files in the `bin`

folder. When developing locally, you must [register binding extensions](extension-bundles). When you develop functions in the Azure portal, this registration is done for you.

## Create a C# script app

There are currently two ways to create a C# script app:

Create a C# script project by passing the `--csx`

option when running the [ func init](functions-core-tools-reference#func-init) command. You must also set

`--worker-runtime`

to `dotnet`

, as in this example:```
func init --worker-runtime dotnet --csx
```


When working with a C# script app, you must supply the `--csx`

option for other Core Tools where it's supported.

When deploying your C# script project to a function app in Azure, you can only deploy it to an app that uses the [in-process model for C#](functions-dotnet-class-library).

Keep these considerations in mind before creating a C# script app:

- C# script is supported primarily to provide a convenient in-portal experience to help you quickly get started creating and running C# functions. For production-quality apps, you should instead develop your C# functions locally as a
[compiled C# class library project](dotnet-isolated-process-guide). - C# script is only supported when running
[in-process with the Functions host](functions-dotnet-class-library), which is a[legacy execution mode for C#](https://aka.ms/azure-functions-retirements/in-process-model). - You can't host C# script apps in the
[Flex Consumption plan](flex-consumption-plan), which is the recommended plan for dynamic scale apps. This is because the Flex Consumption plan only supports C# apps that use the[isolated worker model](dotnet-isolated-process-guide).

## Binding to arguments

Input or output data is bound to a C# script function parameter via the `name`

property in the *function.json* configuration file. The following example shows a *function.json* file and *run.csx* file for a queue-triggered function. The parameter that receives data from the queue message is named `myQueueItem`

because that's the value of the `name`

property.

```
{
"disabled": false,
"bindings": [
{
"type": "queueTrigger",
"direction": "in",
"name": "myQueueItem",
"queueName": "myqueue-items",
"connection":"MyStorageConnectionAppSetting"
}
]
}
```


```
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.Extensions.Logging;
using Microsoft.WindowsAzure.Storage.Queue;
using System;
public static void Run(CloudQueueMessage myQueueItem, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem.AsString}");
}
```


The `#r`

statement is explained [later in this article](#referencing-external-assemblies).

## Connections

When possible, use managed identity-based connections in your triggers and bindings. For more information, see the [Function developer guide](functions-reference#connections).

## Supported types for bindings

Each binding has its own supported types; for instance, a blob trigger can be used with a string parameter, a POCO parameter, a `CloudBlockBlob`

parameter, or any of several other supported types. The [binding reference article for blob bindings](functions-bindings-storage-blob-trigger#usage) lists all supported parameter types for blob triggers. For more information, see [Triggers and bindings](functions-triggers-bindings) and the [binding reference docs for each binding type](functions-triggers-bindings#related-content).

Tip

If you plan to use the HTTP or WebHook bindings, plan to avoid port exhaustion that can be caused by improper instantiation of `HttpClient`

. For more information, see [How to manage connections in Azure Functions](manage-connections).

## Referencing custom classes

If you need to use a custom Plain Old CLR Object (POCO) class, you can include the class definition inside the same file or put it in a separate file.

The following example shows a *run.csx* example that includes a POCO class definition.

```
public static void Run(string myBlob, out MyClass myQueueItem)
{
log.Verbose($"C# Blob trigger function processed: {myBlob}");
myQueueItem = new MyClass() { Id = "myid" };
}
public class MyClass
{
public string Id { get; set; }
}
```


A POCO class must have a getter and setter defined for each property.

## Reusing .csx code

You can use classes and methods defined in other *.csx* files in your *run.csx* file. To do that, use `#load`

directives in your *run.csx* file. In the following example, a logging routine named `MyLogger`

is shared in *myLogger.csx* and loaded into *run.csx* using the `#load`

directive:

Example *run.csx*:

```
#load "mylogger.csx"
using Microsoft.Extensions.Logging;
public static void Run(TimerInfo myTimer, ILogger log)
{
log.LogInformation($"Log by run.csx: {DateTime.Now}");
MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```


Example *mylogger.csx*:

```
public static void MyLogger(ILogger log, string logtext)
{
log.LogInformation(logtext);
}
```


Using a shared *.csx* file is a common pattern when you want to strongly type the data passed between functions by using a POCO object. In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order`

to strongly type the order data:

Example *run.csx* for HTTP trigger:

```
#load "..\shared\order.csx"
using System.Net;
using Microsoft.Extensions.Logging;
public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, ILogger log)
{
log.LogInformation("C# HTTP trigger function received an order.");
log.LogInformation(req.ToString());
log.LogInformation("Submitting to processing queue.");
if (req.orderId == null)
{
return new HttpResponseMessage(HttpStatusCode.BadRequest);
}
else
{
await outputQueueItem.AddAsync(req);
return new HttpResponseMessage(HttpStatusCode.OK);
}
}
```


Example *run.csx* for queue trigger:

```
#load "..\shared\order.csx"
using System;
using Microsoft.Extensions.Logging;
public static void Run(Order myQueueItem, out Order outputQueueItem, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed order...");
log.LogInformation(myQueueItem.ToString());
outputQueueItem = myQueueItem;
}
```


Example *order.csx*:

```
public class Order
{
public string orderId {get; set; }
public string custName {get; set;}
public string custAddress {get; set;}
public string custEmail {get; set;}
public string cartId {get; set; }
public override String ToString()
{
return "\n{\n\torderId : " + orderId +
"\n\tcustName : " + custName +
"\n\tcustAddress : " + custAddress +
"\n\tcustEmail : " + custEmail +
"\n\tcartId : " + cartId + "\n}";
}
}
```


You can use a relative path with the `#load`

directive:

`#load "mylogger.csx"`

loads a file located in the function folder.`#load "loadedfiles\mylogger.csx"`

loads a file located in a folder in the function folder.`#load "..\shared\mylogger.csx"`

loads a file located in a folder at the same level as the function folder, that is, directly under*wwwroot*.

The `#load`

directive works only with *.csx* files, not with *.cs* files.

## Binding to method return value

You can use a method return value for an output binding, by using the name `$return`

in *function.json*.

```
{
"name": "$return",
"type": "blob",
"direction": "out",
"path": "output-container/{id}"
}
```


Here's the C# script code using the return value, followed by an async example:

```
public static string Run(WorkItem input, ILogger log)
{
string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
log.LogInformation($"C# script processed queue message. Item={json}");
return json;
}
```


```
public static Task<string> Run(WorkItem input, ILogger log)
{
string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
log.LogInformation($"C# script processed queue message. Item={json}");
return Task.FromResult(json);
}
```


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
public static void Run(ICollector<string> myQueue, ILogger log)
{
myQueue.Add("Hello");
myQueue.Add("World!");
}
```


## Logging

To log output to your streaming logs in C#, include an argument of type [ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger). We recommend that you name it `log`

. Avoid using `Console.Write`

in Azure Functions.

```
public static void Run(string myBlob, ILogger log)
{
log.LogInformation($"C# Blob trigger function processed: {myBlob}");
}
```


Note

For information about a newer logging framework that you can use instead of `TraceWriter`

, see the [ILogger](functions-dotnet-class-library#ilogger) documentation in the .NET class library developer guide.

### Custom metrics logging

You can use the `LogMetric`

extension method on `ILogger`

to create custom metrics in Application Insights. Here's a sample method call:

```
logger.LogMetric("TestMetric", 1234);
```


This code is an alternative to calling `TrackMetric`

by using the Application Insights API for .NET.

## Async

To make a function [asynchronous](/en-us/dotnet/csharp/programming-guide/concepts/async/), use the `async`

keyword and return a `Task`

object.

```
public async static Task ProcessQueueMessageAsync(
string blobName,
Stream blobInput,
Stream blobOutput)
{
await blobInput.CopyToAsync(blobOutput, 4096);
}
```


You can't use `out`

parameters in async functions. For output bindings, use the [function return value](#binding-to-method-return-value) or a [collector object](#writing-multiple-output-values) instead.

## Cancellation tokens

A function can accept a [CancellationToken](/en-us/dotnet/api/system.threading.cancellationtoken) parameter, which enables the operating system to notify your code when the function is about to be terminated. You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.

The following example shows how to check for impending function termination.

```
using System;
using System.IO;
using System.Threading;
public static void Run(
string inputText,
TextWriter logger,
CancellationToken token)
{
for (int i = 0; i < 100; i++)
{
if (token.IsCancellationRequested)
{
logger.WriteLine("Function was cancelled at iteration {0}", i);
break;
}
Thread.Sleep(5000);
logger.WriteLine("Normal processing for queue message={0}", inputText);
}
}
```


## Importing namespaces

If you need to import namespaces, you can do so as usual, with the `using`

clause.

```
using System.Net;
using System.Threading.Tasks;
using Microsoft.Extensions.Logging;
public static Task<HttpResponseMessage> Run(HttpRequestMessage req, ILogger log)
```


The following namespaces are automatically imported and are therefore optional:

`System`

`System.Collections.Generic`

`System.IO`

`System.Linq`

`System.Net.Http`

`System.Threading.Tasks`

`Microsoft.Azure.WebJobs`

`Microsoft.Azure.WebJobs.Host`


## Referencing external assemblies

For framework assemblies, add references by using the `#r "AssemblyName"`

directive.

```
#r "System.Web.Http"
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.Extensions.Logging;
public static Task<HttpResponseMessage> Run(HttpRequestMessage req, ILogger log)
```


The following assemblies are automatically added by the Azure Functions hosting environment:

`mscorlib`

`System`

`System.Core`

`System.Xml`

`System.Net.Http`

`Microsoft.Azure.WebJobs`

`Microsoft.Azure.WebJobs.Host`

`Microsoft.Azure.WebJobs.Extensions`

`System.Web.Http`

`System.Net.Http.Formatting`


The following assemblies may be referenced by simple-name, by runtime version:

In code, assemblies are referenced like the following example:

```
#r "AssemblyName"
```


## Referencing custom assemblies

To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:

Shared assemblies are shared across all functions within a function app. To reference a custom assembly, upload the assembly to a folder named

`bin`

in the root folder (wwwroot) of your function app.Private assemblies are part of a given function's context, and support side-loading of different versions. Private assemblies should be uploaded in a

`bin`

folder in the function directory. Reference the assemblies using the file name, such as`#r "MyAssembly.dll"`

.

For information on how to upload files to your function folder, see the section on [package management](#using-nuget-packages).

### Watched directories

The directory that contains the function script file is automatically watched for changes to assemblies. To watch for assembly changes in other directories, add them to the `watchDirectories`

list in [host.json](functions-host-json).

## Using NuGet packages

The way that both binding extension packages and other NuGet packages are added to your function app depends on the [targeted version of the Functions runtime](functions-versions).

By default, the [supported set of Functions extension NuGet packages](functions-triggers-bindings#supported-bindings) are made available to your C# script function app by using extension bundles. To learn more, see [Extension bundles](extension-bundles).

If for some reason you can't use extension bundles in your project, you can also use the Azure Functions Core Tools to install extensions based on bindings defined in the function.json files in your app. When using Core Tools to register extensions, make sure to use the `--csx`

option. To learn more, see [func extensions install](functions-core-tools-reference#func-extensions-install).

By default, Core Tools reads the function.json files and adds the required packages to an *extensions.csproj* C# class library project file in the root of the function app's file system (wwwroot). Because Core Tools uses dotnet.exe, you can use it to add any NuGet package reference to this extensions file. During installation, Core Tools builds the extensions.csproj to install the required libraries. Here's an example *extensions.csproj* file that adds a reference to *Microsoft.ProjectOxford.Face* version *1.1.0*:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netstandard2.0</TargetFramework>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.ProjectOxford.Face" Version="1.1.0" />
</ItemGroup>
</Project>
```


Note

For C# script (.csx), you must set `TargetFramework`

to a value of `netstandard2.0`

. Other target frameworks, such as `net8.0`

, aren't supported.

To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the function app root folder. For more information, see [Configuring NuGet behavior](/en-us/nuget/consume-packages/configuring-nuget-behavior).

If you're working on your project only in the portal, you'll need to manually create the extensions.csproj file or a Nuget.Config file directly in the site. To learn more, see [Manually install extensions](functions-how-to-use-azure-function-app-settings#manually-install-extensions).

## Environment variables

To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`

, as shown in the following code example:

```
public static void Run(TimerInfo myTimer, ILogger log)
{
log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
log.LogInformation(GetEnvironmentVariable("AzureWebJobsStorage"));
log.LogInformation(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}
public static string GetEnvironmentVariable(string name)
{
return name + ": " +
System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```


## Retry policies

Functions supports two built-in retry policies. For more information, see [Retry policies](functions-bindings-error-pages#retry-policies).

Here's the retry policy in the *function.json* file:

```
{
"disabled": false,
"bindings": [
{
....
}
],
"retry": {
"strategy": "fixedDelay",
"maxRetryCount": 4,
"delayInterval": "00:00:10"
}
}
```


function.json property |
Description |
|---|---|
| strategy | Use `fixedDelay` . |
| maxRetryCount | Required. The maximum number of retries allowed per function execution. `-1` means to retry indefinitely. |
| delayInterval | The delay that's used between retries. Specify it as a string with the format `HH:mm:ss` . |

## Binding at runtime

In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [ declarative](https://en.wikipedia.org/wiki/Declarative_programming) bindings in

*function.json*. Imperative binding is useful when binding parameters need to be computed at runtime rather than design time. With this pattern, you can bind to supported input and output bindings on-the-fly in your function code.

Define an imperative binding as follows:

**Do not**include an entry in*function.json*for your desired imperative bindings.- Pass in an input parameter
or`Binder binder`

.`IBinder binder`

- Use the following C# pattern to perform the data binding.

```
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
...
}
```


`BindingTypeAttribute`

is the .NET attribute that defines your binding and `T`

is an input or output type that's
supported by that binding type. `T`

can't be an `out`

parameter type (such as `out JObject`

). For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [ IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for

`T`

.### Single attribute example

The following example code creates a [Storage blob output binding](functions-bindings-storage-blob-output) with blob path that's defined at run time, then writes a string to the blob.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;
public static async Task Run(string input, Binder binder)
{
using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
{
writer.Write("Hello World!!");
}
}
```


[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Extensions.Storage/Blobs/BlobAttribute.cs)
defines the [Storage blob](functions-bindings-storage-blob) input or output binding, and
[TextWriter](/en-us/dotnet/api/system.io.textwriter) is a supported output binding type.

### Multiple attributes example

The preceding example gets the app setting for the function app's main Storage account connection string (which is `AzureWebJobsStorage`

). You can specify a custom app setting to use for the Storage account by adding the
[StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)
and passing the attribute array into `BindAsync<T>()`

. Use a `Binder`

parameter, not `IBinder`

. For example:

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;
public static async Task Run(string input, Binder binder)
{
var attributes = new Attribute[]
{
new BlobAttribute("samples-output/path"),
new StorageAccountAttribute("MyStorageAccount")
};
using (var writer = await binder.BindAsync<TextWriter>(attributes))
{
writer.Write("Hello World!");
}
}
```


The following table lists the .NET attributes for each binding type and the packages in which they're defined.

## Convert a C# script app to a C# project

The easiest way to convert a C# script function app to a compiled C# class library project is to start with a new project. You can then, for each function, migrate the code and configuration from each run.csx file and function.json file in a function folder to a single new .cs class library code file. For example, when you have a C# script function named `HelloWorld`

you'll have two files: `HelloWorld/run.csx`

and `HelloWorld/function.json`

. For this function, you create a code file named `HelloWorld.cs`

in your new class library project.

If you are using C# scripting for portal editing, you can [download the app content to your local machine](deployment-zip-push#download-your-function-app-files). Choose the **Site content** option instead of **Content and Visual Studio project**. You don't need to generate a project, and don't include application settings in the download. You're defining a new development environment, and this environment shouldn't have the same permissions as your hosted app environment.

These instructions show you how to convert C# script functions (which run in-process with the Functions host) to C# class library functions that run in an [isolated worker process](dotnet-isolated-process-guide).

Complete the

**Create a functions app project**section from your preferred quickstart:

If your original C# script code includes an

`extensions.csproj`

file or any`function.proj`

files, copy the package references from these file and add them to the new project's`.csproj`

file in the same`ItemGroup`

with the Functions core dependencies.Tip

Conversion provides a good opportunity to update to the latest versions of your dependencies. Doing so may require additional code changes in a later step.

Copy the contents of the original

`host.json`

file into the new project's`host.json`

file, except for the`extensionBundles`

section (compiled C# projects don't use[extension bundles](extension-bundles)and you must explicitly add references to all extensions used by your functions). When merging host.json files, remember that theschema is versioned, with most apps using version 2.0. The contents of the`host.json`

`extensions`

section can differ based on specific versions of the binding extensions used by your functions. See individual extension reference articles to learn how to correctly configure the host.json for your specific versions.For any

[shared files referenced by a](#reusing-csx-code), create a new`#load`

directive`.cs`

file for each of these shared references. It's simplest to create a new`.cs`

file for each shared class definition. If there are static methods without a class, you need to define new classes for these methods.Perform the following tasks for each

`<FUNCTION_NAME>`

folder in your original project:Create a new file named

`<FUNCTION_NAME>.cs`

, replacing`<FUNCTION_NAME>`

with the name of the folder that defined your C# script function. You can create a new function code file from one of the trigger-specific templates in the following way:Using the

`func new --name <FUNCTION_NAME>`

command and choosing the correct trigger template at the prompt.Copy the

`using`

statements from your`run.csx`

file and add them to the new file. You do not need any`#r`

directives.For any

`#load`

statement in your`run.csx`

file, add a new`using`

statement for the namespace you used for the shared code.In the new file, define a class for your function under the namespace you are using for the project.

Create a new method named

`RunHandler`

or something similar. This new method serves as the new entry point for the function.Copy the static method that represents your function, along with any functions it calls, from

`run.csx`

into your new class as a second method. From the new method you created in the previous step, call into this static method. This indirection step is helpful for navigating any differences as you continue the upgrade. You can keep the original method exactly the same and simply control its inputs from the new context. You may need to create parameters on the new method which you then pass into the static method call. After you have confirmed that the migration has worked as intended, you can remove this extra level of indirection.For each binding in the

`function.json`

file, add the corresponding attribute to your new method. To quickly find binding examples, see[Manually add bindings based on examples](add-bindings-existing-function?tabs=csharp).Add any extension packages required by the bindings to your project, if you haven't already done so.


Recreate any application settings required by your app in the

`Values`

collection of the[local.settings.json file](functions-develop-local#local-settings-file).Verify that your project runs locally:

Use

`func start`

to run your app from the command line. For more information, see[Run functions locally](functions-run-local#start).Publish your project to a new function app in Azure:

[Create your Azure resources](how-to-create-function-azure-cli?pivots=programming-language-csharp#create-supporting-azure-resources-for-your-function)and deploy the code project to Azure by using the`func azure functionapp publish <APP_NAME>`

command. For more information, see[Deploy project files](functions-run-local#project-file-deployment).

### Example function conversion

This section shows an example of the migration for a single function.

The original function in C# scripting has two files:

`HelloWorld/function.json`

`HelloWorld/run.csx`


The contents of `HelloWorld/function.json`

are:

```
{
"bindings": [
{
"authLevel": "FUNCTION",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
}
]
}
```


The contents of `HelloWorld/run.csx`

are:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string name = req.Query["name"];
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic data = JsonConvert.DeserializeObject(requestBody);
name = name ?? data?.name;
string responseMessage = string.IsNullOrEmpty(name)
? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
: $"Hello, {name}. This HTTP triggered function executed successfully.";
return new OkObjectResult(responseMessage);
}
```


After migrating to the isolated worker model with ASP.NET Core integration, these are replaced by a single `HelloWorld.cs`

:

```
using System.Net;
using Microsoft.Azure.Functions.Worker;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Logging;
using Microsoft.AspNetCore.Routing;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
namespace MyFunctionApp
{
public class HelloWorld
{
private readonly ILogger _logger;
public HelloWorld(ILoggerFactory loggerFactory)
{
_logger = loggerFactory.CreateLogger<HelloWorld>();
}
[Function("HelloWorld")]
public async Task<IActionResult> RunHandler([HttpTrigger(AuthorizationLevel.Function, "get")] HttpRequest req)
{
return await Run(req, _logger);
}
// From run.csx
public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string name = req.Query["name"];
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic data = JsonConvert.DeserializeObject(requestBody);
name = name ?? data?.name;
string responseMessage = string.IsNullOrEmpty(name)
? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
: $"Hello, {name}. This HTTP triggered function executed successfully.";
return new OkObjectResult(responseMessage);
}
}
}
```


## Binding configuration and examples

This section contains references and examples for defining triggers and bindings in C# script.

### Blob trigger

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blobTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the blob in function code. |
path |
The
|

**connection**[Connections](functions-bindings-storage-blob-trigger#connections).The following example shows a blob trigger definition in a *function.json* file and code that uses the binding. The function writes a log when a blob is added or updated in the `samples-workitems`

[container](../storage/blobs/storage-blobs-introduction#blob-storage-resources).

Here's the binding data in the *function.json* file:

```
{
"disabled": false,
"bindings": [
{
"name": "myBlob",
"type": "blobTrigger",
"direction": "in",
"path": "samples-workitems/{name}",
"connection":"MyStorageAccountAppSetting"
}
]
}
```


The string `{name}`

in the blob trigger path `samples-workitems/{name}`

creates a [binding expression](functions-bindings-expressions-patterns) that you can use in function code to access the file name of the triggering blob. For more information, see [Blob name patterns](functions-bindings-storage-blob-trigger#blob-name-patterns).

Here's C# script code that binds to a `Stream`

:

```
public static void Run(Stream myBlob, string name, ILogger log)
{
log.LogInformation($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```


Here's C# script code that binds to a `CloudBlockBlob`

:

```
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Blob;
public static void Run(CloudBlockBlob myBlob, string name, ILogger log)
{
log.LogInformation($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```


### Blob input

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blob` . |
direction |
Must be set to `in` . |
name |
The name of the variable that represents the blob in function code. |
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

The following example shows blob input and output bindings in a *function.json* file and C# script code that uses the bindings. The function makes a copy of a text blob. The function is triggered by a queue message that contains the name of the blob to copy. The new blob is named *{originalblobname}-Copy*.

In the *function.json* file, the `queueTrigger`

metadata property is used to specify the blob name in the `path`

properties:

```
{
"bindings": [
{
"queueName": "myqueue-items",
"connection": "MyStorageConnectionAppSetting",
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "myInputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "in"
},
{
"name": "myOutputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}-Copy",
"connection": "MyStorageConnectionAppSetting",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
public static void Run(string myQueueItem, string myInputBlob, out string myOutputBlob, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
myOutputBlob = myInputBlob;
}
```


### Blob output

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blob` . |
direction |
Must be set to `out` . |
name |
The name of the variable that represents the blob in function code. |
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

The following example shows blob input and output bindings in a *function.json* file and C# script code that uses the bindings. The function makes a copy of a text blob. The function is triggered by a queue message that contains the name of the blob to copy. The new blob is named *{originalblobname}-Copy*.

In the *function.json* file, the `queueTrigger`

metadata property is used to specify the blob name in the `path`

properties:

```
{
"bindings": [
{
"queueName": "myqueue-items",
"connection": "MyStorageConnectionAppSetting",
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "myInputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "in"
},
{
"name": "myOutputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}-Copy",
"connection": "MyStorageConnectionAppSetting",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
public static void Run(string myQueueItem, string myInputBlob, out string myOutputBlob, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
myOutputBlob = myInputBlob;
}
```


### RabbitMQ trigger

The following example shows a RabbitMQ trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function reads and logs the RabbitMQ message.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "rabbitMQTrigger",
"direction": "in",
"queueName": "queue",
"connectionStringSetting": "rabbitMQConnectionAppSetting"
}
]
}
```


Here's the C# script code:

```
using System;
public static void Run(string myQueueItem, ILogger log)
{
log.LogInformation($"C# Script RabbitMQ trigger function processed: {myQueueItem}");
}
```


### Queue trigger

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `queueTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
In the function.json file only. Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that contains the queue item payload in the function code. |
queueName |
The name of the queue to poll. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

The following example shows a queue trigger binding in a *function.json* file and C# script code that uses the binding. The function polls the `myqueue-items`

queue and writes a log each time a queue item is processed.

Here's the *function.json* file:

```
{
"disabled": false,
"bindings": [
{
"type": "queueTrigger",
"direction": "in",
"name": "myQueueItem",
"queueName": "myqueue-items",
"connection":"MyStorageConnectionAppSetting"
}
]
}
```


Here's the C# script code:

```
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.Extensions.Logging;
using Microsoft.WindowsAzure.Storage.Queue;
using System;
public static void Run(CloudQueueMessage myQueueItem,
DateTimeOffset expirationTime,
DateTimeOffset insertionTime,
DateTimeOffset nextVisibleTime,
string queueTrigger,
string id,
string popReceipt,
int dequeueCount,
ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
$"queueTrigger={queueTrigger}\n" +
$"expirationTime={expirationTime}\n" +
$"insertionTime={insertionTime}\n" +
$"nextVisibleTime={nextVisibleTime}\n" +
$"id={id}\n" +
$"popReceipt={popReceipt}\n" +
$"dequeueCount={dequeueCount}");
}
```


### Queue output

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `queue` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the queue in function code. Set to `$return` to reference the function return value. |
queueName |
The name of the queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

The following example shows an HTTP trigger binding in a *function.json* file and C# script code that uses the binding. The function creates a queue item with a **CustomQueueMessage** object payload for each HTTP request received.

Here's the *function.json* file:

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"authLevel": "function",
"name": "input"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "queue",
"direction": "out",
"name": "$return",
"queueName": "outqueue",
"connection": "MyStorageConnectionAppSetting"
}
]
}
```


Here's C# script code that creates a single queue message:

```
public class CustomQueueMessage
{
public string PersonName { get; set; }
public string Title { get; set; }
}
public static CustomQueueMessage Run(CustomQueueMessage input, ILogger log)
{
return input;
}
```


You can send multiple messages at once by using an `ICollector`

or `IAsyncCollector`

parameter. Here's C# script code that sends multiple messages, one with the HTTP request data and one with hard-coded values:

```
public static void Run(
CustomQueueMessage input,
ICollector<CustomQueueMessage> myQueueItems,
ILogger log)
{
myQueueItems.Add(input);
myQueueItems.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```


### Table input

This section outlines support for the [Tables API version of the extension](functions-bindings-storage-table?tabs=in-process,table-api) only.

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `table` . This property is set automatically when you create the binding in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the binding in the Azure portal. |
name |
The name of the variable that represents the table or entity in function code. |
tableName |
The name of the table. |
partitionKey |
Optional. The partition key of the table entity to read. |
rowKey |
Optional. The row key of the table entity to read. Can't be used with `take` or `filter` . |
take |
Optional. The maximum number of entities to return. Can't be used with `rowKey` . |
filter |
Optional. An OData filter expression for the entities to return from the table. Can't be used with `rowKey` . |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

The following example shows a table input binding in a *function.json* file and C# script code that uses the binding. The function uses a queue trigger to read a single table row.

The *function.json* file specifies a `partitionKey`

and a `rowKey`

. The `rowKey`

value `{queueTrigger}`

indicates that the row key comes from the queue message string.

```
{
"bindings": [
{
"queueName": "myqueue-items",
"connection": "MyStorageConnectionAppSetting",
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "personEntity",
"type": "table",
"tableName": "Person",
"partitionKey": "Test",
"rowKey": "{queueTrigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "in"
}
],
"disabled": false
}
```


Here's the C# script code:

```
#r "Azure.Data.Tables"
using Microsoft.Extensions.Logging;
using Azure.Data.Tables;
public static void Run(string myQueueItem, Person personEntity, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
log.LogInformation($"Name in Person entity: {personEntity.Name}");
}
public class Person : ITableEntity
{
public string Name { get; set; }
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public DateTimeOffset? Timestamp { get; set; }
public ETag ETag { get; set; }
}
```


### Table output

This section outlines support for the [Tables API version of the extension](functions-bindings-storage-table?tabs=in-process,table-api) only.

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

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

The following example shows a table output binding in a *function.json* file and C# script code that uses the binding. The function writes multiple table entities.

Here's the *function.json* file:

```
{
"bindings": [
{
"name": "input",
"type": "manualTrigger",
"direction": "in"
},
{
"tableName": "Person",
"connection": "MyStorageConnectionAppSetting",
"name": "tableBinding",
"type": "table",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
public static void Run(string input, ICollector<Person> tableBinding, ILogger log)
{
for (int i = 1; i < 10; i++)
{
log.LogInformation($"Adding Person entity {i}");
tableBinding.Add(
new Person() {
PartitionKey = "Test",
RowKey = i.ToString(),
Name = "Name" + i.ToString() }
);
}
}
public class Person
{
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public string Name { get; set; }
}
```


### Timer trigger

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `timerTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the timer object in function code. |
schedule |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as in this example: "%ScheduleAppSetting%". |

**runOnStartup**`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***runOnStartup**should rarely if ever be set to`true`

, especially in production.**useMonitor**`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.The following example shows a timer trigger binding in a *function.json* file and a C# script function that uses the binding. The function writes a log indicating whether this function invocation is due to a missed schedule occurrence. The [ TimerInfo](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) object is passed into the function.

Here's the binding data in the *function.json* file:

```
{
"schedule": "0 */5 * * * *",
"name": "myTimer",
"type": "timerTrigger",
"direction": "in"
}
```


Here's the C# script code:

```
public static void Run(TimerInfo myTimer, ILogger log)
{
if (myTimer.IsPastDue)
{
log.LogInformation("Timer is running late!");
}
log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}" );
}
```


### HTTP trigger

The following table explains the trigger configuration properties that you set in the *function.json* file:

| function.json property | Description |
|---|---|
type |
Required - must be set to `httpTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code for the request or request body. |
authLevel |
Determines what keys, if any, need to be present on the request in order to invoke the function. For supported values, see
|

**methods**[customize the HTTP endpoint](functions-bindings-http-webhook-trigger#customize-the-http-endpoint).**route**`<functionname>`

. For more information, see [customize the HTTP endpoint](functions-bindings-http-webhook-trigger#customize-the-http-endpoint).**webHookType***Supported only for the version 1.x runtime.*Configures the HTTP trigger to act as a

[webhook](https://en.wikipedia.org/wiki/Webhook)receiver for the specified provider. For supported values, see[WebHook type](functions-bindings-http-webhook-trigger#webhook-type).The following example shows a trigger binding in a *function.json* file and a C# script function that uses the binding. The function looks for a `name`

parameter either in the query string or the body of the HTTP request.

Here's the *function.json* file:

```
{
"disabled": false,
"bindings": [
{
"authLevel": "function",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
}
]
}
```


Here's C# script code that binds to `HttpRequest`

:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string name = req.Query["name"];
string requestBody = String.Empty;
using (StreamReader streamReader = new StreamReader(req.Body))
{
requestBody = await streamReader.ReadToEndAsync();
}
dynamic data = JsonConvert.DeserializeObject(requestBody);
name = name ?? data?.name;
return name != null
? (ActionResult)new OkObjectResult($"Hello, {name}")
: new BadRequestObjectResult("Please pass a name on the query string or in the request body");
}
```


You can bind to a custom object instead of `HttpRequest`

. This object is created from the body of the request and parsed as JSON. Similarly, a type can be passed to the HTTP response output binding and returned as the response body, along with a `200`

status code.

```
using System.Net;
using System.Threading.Tasks;
using Microsoft.Extensions.Logging;
public static string Run(Person person, ILogger log)
{
return person.Name != null
? (ActionResult)new OkObjectResult($"Hello, {person.Name}")
: new BadRequestObjectResult("Please pass an instance of Person.");
}
public class Person {
public string Name {get; set;}
}
```


### HTTP output

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
type |
Must be set to `http` . |
direction |
Must be set to `out` . |
name |
The variable name used in function code for the response, or `$return` to use the return value. |

### Event Hubs trigger

The following table explains the trigger configuration properties that you set in the *function.json* file:

| function.json property | Description |
|---|---|
type |
Must be set to `eventHubTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the event item in function code. |
eventHubName |
Functions 2.x and higher. The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` . In version 1.x, this property is named `path` . |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**connection**[Connections](functions-bindings-event-hubs-trigger#connections).The following example shows an Event Hubs trigger binding in a *function.json* file and a C# script function that uses the binding. The function logs the message body of the Event Hubs trigger.

The following examples show Event Hubs binding data in the *function.json* file for Functions runtime version 2.x and later versions.

```
{
"type": "eventHubTrigger",
"name": "myEventHubMessage",
"direction": "in",
"eventHubName": "MyEventHub",
"connection": "myEventHubReadConnectionAppSetting"
}
```


Here's the C# script code:

```
using System;
public static void Run(string myEventHubMessage, TraceWriter log)
{
log.Info($"C# function triggered to process a message: {myEventHubMessage}");
}
```


To get access to event metadata in function code, bind to an [EventData](/en-us/dotnet/api/microsoft.servicebus.messaging.eventdata) object. You can also access the same properties by using binding expressions in the method signature. The following example shows both ways to get the same data:

```
#r "Microsoft.Azure.EventHubs"
using System.Text;
using System;
using Microsoft.ServiceBus.Messaging;
using Microsoft.Azure.EventHubs;
public void Run(EventData myEventHubMessage,
DateTime enqueuedTimeUtc,
Int64 sequenceNumber,
string offset,
TraceWriter log)
{
log.Info($"Event: {Encoding.UTF8.GetString(myEventHubMessage.Body)}");
log.Info($"EnqueuedTimeUtc={myEventHubMessage.SystemProperties.EnqueuedTimeUtc}");
log.Info($"SequenceNumber={myEventHubMessage.SystemProperties.SequenceNumber}");
log.Info($"Offset={myEventHubMessage.SystemProperties.Offset}");
// Metadata accessed by using binding expressions
log.Info($"EnqueuedTimeUtc={enqueuedTimeUtc}");
log.Info($"SequenceNumber={sequenceNumber}");
log.Info($"Offset={offset}");
}
```


To receive events in a batch, make `string`

or `EventData`

an array:

```
public static void Run(string[] eventHubMessages, TraceWriter log)
{
foreach (var message in eventHubMessages)
{
log.Info($"C# function triggered to process a message: {message}");
}
}
```


### Event Hubs output

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `eventHub` . |
direction |
Must be set to `out` . This parameter is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the event. |
eventHubName |
Functions 2.x and higher. The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. In Functions 1.x, this property is named `path` . |
connection |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

The following example shows an event hub trigger binding in a *function.json* file and a C# script function that uses the binding. The function writes a message to an event hub.

The following examples show Event Hubs binding data in the *function.json* file for Functions runtime version 2.x and later versions.

```
{
"type": "eventHub",
"name": "outputEventHubMessage",
"eventHubName": "myeventhub",
"connection": "MyEventHubSendAppSetting",
"direction": "out"
}
```


Here's C# script code that creates one message:

```
using System;
using Microsoft.Extensions.Logging;
public static void Run(TimerInfo myTimer, out string outputEventHubMessage, ILogger log)
{
String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
log.LogInformation(msg);
outputEventHubMessage = msg;
}
```


Here's C# script code that creates multiple messages:

```
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, ILogger log)
{
string message = $"Message created at: {DateTime.Now}";
log.LogInformation(message);
outputEventHubMessage.Add("1 " + message);
outputEventHubMessage.Add("2 " + message);
}
```


### Event Grid trigger

The following table explains the binding configuration properties for C# script that you set in the *function.json* file. There are no constructor parameters or properties to set in the `EventGridTrigger`

attribute.

| function.json property | Description |
|---|---|
type |
Required - must be set to `eventGridTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code for the parameter that receives the event data. |

The following example shows an Event Grid trigger defined in the *function.json* file.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "eventGridTrigger",
"name": "eventGridEvent",
"direction": "in"
}
],
"disabled": false
}
```


Here's an example of a C# script function that uses an `EventGridEvent`

binding parameter:

```
#r "Azure.Messaging.EventGrid"
using Azure.Messaging.EventGrid;
using Microsoft.Extensions.Logging;
public static void Run(EventGridEvent eventGridEvent, ILogger log)
{
log.LogInformation(eventGridEvent.Data.ToString());
}
```


Here's an example of a C# script function that uses a `JObject`

binding parameter:

```
#r "Newtonsoft.Json"
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
public static void Run(JObject eventGridEvent, TraceWriter log)
{
log.Info(eventGridEvent.ToString(Formatting.Indented));
}
```


### Event Grid output

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `eventGrid` . |
direction |
Must be set to `out` . This parameter is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the event. |
topicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
topicKeySetting |
The name of an app setting that contains an access key for the custom topic. |

The following example shows the Event Grid output binding data in the *function.json* file.

```
{
"type": "eventGrid",
"name": "outputEvent",
"topicEndpointUri": "MyEventGridTopicUriSetting",
"topicKeySetting": "MyEventGridTopicKeySetting",
"direction": "out"
}
```


Here's C# script code that creates one event:

```
#r "Microsoft.Azure.EventGrid"
using System;
using Microsoft.Azure.EventGrid.Models;
using Microsoft.Extensions.Logging;
public static void Run(TimerInfo myTimer, out EventGridEvent outputEvent, ILogger log)
{
outputEvent = new EventGridEvent("message-id", "subject-name", "event-data", "event-type", DateTime.UtcNow, "1.0");
}
```


Here's C# script code that creates multiple events:

```
#r "Microsoft.Azure.EventGrid"
using System;
using Microsoft.Azure.EventGrid.Models;
using Microsoft.Extensions.Logging;
public static void Run(TimerInfo myTimer, ICollector<EventGridEvent> outputEvent, ILogger log)
{
outputEvent.Add(new EventGridEvent("message-id-1", "subject-name", "event-data", "event-type", DateTime.UtcNow, "1.0"));
outputEvent.Add(new EventGridEvent("message-id-2", "subject-name", "event-data", "event-type", DateTime.UtcNow, "1.0"));
}
```


### Service Bus trigger

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `serviceBusTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the queue or topic message in function code. |
queueName |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
topicName |
Name of the topic to monitor. Set only if monitoring a topic, not for a queue. |
subscriptionName |
Name of the subscription to monitor. Set only if monitoring a topic, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**accessRights**`manage`

and `listen`

. The default is `manage`

, which indicates that the `connection`

has the **Manage**permission. If you use a connection string that does not have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property is not available because the latest version of the Service Bus SDK doesn't support manage operations.**isSessionsEnabled**`true`

if connecting to a [session-aware](../service-bus-messaging/message-sessions)queue or subscription.`false`

otherwise, which is the default value.**autoComplete**`true`

when the trigger should automatically call complete after processing, or if the function code will manually call complete.Setting to

`false`

is only supported in C#.If set to

`true`

, the trigger completes the message automatically if the function execution completes successfully, and abandons the message otherwise.<br/When set to

`false`

, you are responsible for calling [ServiceBusReceiver](/en-us/dotnet/api/azure.messaging.servicebus.servicebusreceiver)methods to complete, abandon, or deadletter the message, session, or batch. When an exception is thrown (and none of the`ServiceBusReceiver`

methods are called), then the lock remains. Once the lock expires, the message is re-queued with the `DeliveryCount`

incremented and the lock is automatically renewed.This property is available only in Azure Functions 2.x and higher.

The following example shows a Service Bus trigger binding in a *function.json* file and a C# script function that uses the binding. The function reads message metadata and logs a Service Bus queue message.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"queueName": "testqueue",
"connection": "MyServiceBusConnection",
"name": "myQueueItem",
"type": "serviceBusTrigger",
"direction": "in"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System;
public static void Run(string myQueueItem,
Int32 deliveryCount,
DateTime enqueuedTimeUtc,
string messageId,
TraceWriter log)
{
log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
log.Info($"EnqueuedTimeUtc={enqueuedTimeUtc}");
log.Info($"DeliveryCount={deliveryCount}");
log.Info($"MessageId={messageId}");
}
```


### Service Bus output

The following table explains the binding configuration properties that you set in the *function.json* file.

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

has the **Manage**permission. If you use a connection string that does not have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property is not available because the latest version of the Service Bus SDK doesn't support manage operations.The following example shows a Service Bus output binding in a *function.json* file and a C# script function that uses the binding. The function uses a timer trigger to send a queue message every 15 seconds.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"schedule": "0/15 * * * * *",
"name": "myTimer",
"runsOnStartup": true,
"type": "timerTrigger",
"direction": "in"
},
{
"name": "outputSbQueue",
"type": "serviceBus",
"queueName": "testqueue",
"connection": "MyServiceBusConnection",
"direction": "out"
}
],
"disabled": false
}
```


Here's C# script code that creates a single message:

```
public static void Run(TimerInfo myTimer, ILogger log, out string outputSbQueue)
{
string message = $"Service Bus queue message created at: {DateTime.Now}";
log.LogInformation(message);
outputSbQueue = message;
}
```


Here's C# script code that creates multiple messages:

```
public static async Task Run(TimerInfo myTimer, ILogger log, IAsyncCollector<string> outputSbQueue)
{
string message = $"Service Bus queue messages created at: {DateTime.Now}";
log.LogInformation(message);
await outputSbQueue.AddAsync("1 " + message);
await outputSbQueue.AddAsync("2 " + message);
}
```


### Azure Cosmos DB v2 trigger

This section outlines support for the [version 4.x+ of the extension](functions-bindings-cosmosdb-v2?tabs=in-process,extensionv4) only.

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `cosmosDBTrigger` . |
direction |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
name |
The variable name used in function code that represents the list of documents with changes. |
connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****leaseConnection**When not set, the

`connection`

value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions.**leaseDatabaseName**`databaseName`

setting is used.**leaseContainerName**`leases`

is used.**createLeaseContainerIfNotExists**`true`

, the leases container is automatically created when it doesn't already exist. The default value is `false`

. When using Microsoft Entra identities if you set the value to `true`

, creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed)and your Function won't be able to start.**leasesContainerThroughput**`createLeaseContainerIfNotExists`

is set to `true`

. This parameter is automatically set when the binding is created using the portal.**leaseContainerPrefix****feedPollDelay****leaseAcquireInterval****leaseExpirationInterval****leaseRenewInterval****maxItemsPerInvocation**[transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions)is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch.**startFromBeginning**`true`

when there are leases already created has no effect.**startFromTime**`2021-02-16T14:19:29Z`

. This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect.**preferredLocations**The following example shows an Azure Cosmos DB trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function writes log messages when Azure Cosmos DB records are added or modified.

Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Here's the C# script code:

```
using System;
using System.Collections.Generic;
using Microsoft.Extensions.Logging;
// Customize the model with your own desired properties
public class ToDoItem
{
public string id { get; set; }
public string Description { get; set; }
}
public static void Run(IReadOnlyList<ToDoItem> documents, ILogger log)
{
log.LogInformation("Documents modified " + documents.Count);
log.LogInformation("First document Id " + documents[0].id);
}
```


### Azure Cosmos DB v2 input

This section outlines support for the [version 4.x+ of the extension](functions-bindings-cosmosdb-v2?tabs=in-process,extensionv4) only.

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `cosmosDB` . |
direction |
Must be set to `in` . |
name |
The variable name used in function code that represents the list of documents with changes. |
connection |
The name of an app setting or setting container that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****partitionKey**[partitioned](/en-us/azure/cosmos-db/partitioning-overview#logical-partitions)containers.**id**[binding expressions](functions-bindings-expressions-patterns). Don't set both the`id`

and `sqlQuery`

properties. If you don't set either one, the entire container is retrieved.**sqlQuery**`SELECT * FROM c where c.departmentId = {departmentId}`

. Don't set both the `id`

and `sqlQuery`

properties. If you don't set either one, the entire container is retrieved.**preferredLocations**`East US,South Central US,North Europe`

.This section contains the following examples:

[Queue trigger, look up ID from string](#queue-trigger-look-up-id-from-string-c-script)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-c-script)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-c-script)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-c-script)[HTTP trigger, get multiple docs, using SqlQuery](#http-trigger-get-multiple-docs-using-sqlquery-c-script)[HTTP trigger, get multiple docs, using DocumentClient](#http-trigger-get-multiple-docs-using-documentclient-c-script)

The HTTP trigger examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV2
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


#### Queue trigger, look up ID from string

The following example shows an Azure Cosmos DB input binding in a *function.json* file and a C# script function that uses the binding. The function reads a single document and updates the document's text value.

Here's the binding data in the *function.json* file:

```
{
"name": "inputDocument",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"id" : "{queueTrigger}",
"partitionKey": "{partition key value}",
"connectionStringSetting": "MyAccount_COSMOSDB",
"direction": "in"
}
```


Here's the C# script code:

```
using System;
// Change input document contents using Azure Cosmos DB input binding
public static void Run(string myQueueItem, dynamic inputDocument)
{
inputDocument.text = "This has changed.";
}
```


#### Queue trigger, get multiple docs, using SqlQuery

The following example shows an Azure Cosmos DB input binding in a *function.json* file and a C# script function that uses the binding. The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

Here's the binding data in the *function.json* file:

```
{
"name": "documents",
"type": "cosmosDB",
"direction": "in",
"databaseName": "MyDb",
"collectionName": "MyCollection",
"sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
"connectionStringSetting": "CosmosDBConnection"
}
```


Here's the C# script code:

```
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{
foreach (var doc in documents)
{
// operate on each document
}
}
public class QueuePayload
{
public string departmentId { get; set; }
}
```


#### HTTP trigger, look up ID from query string

The following example shows a C# script function that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "cosmosDB",
"name": "toDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"Id": "{Query.id}",
"PartitionKey" : "{Query.partitionKeyValue}"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
using Microsoft.Extensions.Logging;
public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.LogInformation($"ToDo item not found");
}
else
{
log.LogInformation($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, look up ID from route data

The following example shows a C# script function that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
],
"route":"todoitems/{partitionKeyValue}/{id}"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "cosmosDB",
"name": "toDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"id": "{id}",
"partitionKey": "{partitionKeyValue}"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
using Microsoft.Extensions.Logging;
public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.LogInformation($"ToDo item not found");
}
else
{
log.LogInformation($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, get multiple docs, using SqlQuery

The following example shows a C# script function that retrieves a list of documents. The function is triggered by an HTTP request. The query is specified in the `SqlQuery`

attribute property.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "cosmosDB",
"name": "toDoItems",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"sqlQuery": "SELECT top 2 * FROM c order by c._ts desc"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
using Microsoft.Extensions.Logging;
public static HttpResponseMessage Run(HttpRequestMessage req, IEnumerable<ToDoItem> toDoItems, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.LogInformation(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, get multiple docs, using DocumentClient

The following example shows a C# script function that retrieves a list of documents. The function is triggered by an HTTP request. The code uses a `DocumentClient`

instance provided by the Azure Cosmos DB binding to read a list of documents. The `DocumentClient`

instance could also be used for write operations.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "cosmosDB",
"name": "client",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "inout"
}
],
"disabled": false
}
```


Here's the C# script code:

```
#r "Microsoft.Azure.Documents.Client"
using System.Net;
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;
using Microsoft.Extensions.Logging;
public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, DocumentClient client, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");
string searchterm = req.GetQueryNameValuePairs()
.FirstOrDefault(q => string.Compare(q.Key, "searchterm", true) == 0)
.Value;
if (searchterm == null)
{
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.LogInformation($"Searching for word: {searchterm} using Uri: {collectionUri.ToString()}");
IDocumentQuery<ToDoItem> query = client.CreateDocumentQuery<ToDoItem>(collectionUri)
.Where(p => p.Description.Contains(searchterm))
.AsDocumentQuery();
while (query.HasMoreResults)
{
foreach (ToDoItem result in await query.ExecuteNextAsync())
{
log.LogInformation(result.Description);
}
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


### Azure Cosmos DB v2 output

This section outlines support for the [version 4.x+ of the extension](functions-bindings-cosmosdb-v2?tabs=in-process,extensionv4) only.

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****createIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**partitionKey**`createIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**containerThroughput**`createIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**preferredLocations**`East US,South Central US,North Europe`

.This section contains the following examples:

#### Queue trigger, write one doc

The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function uses a queue input binding for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the binding data in the *function.json* file:

```
{
"name": "employeeDocument",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": true,
"connectionStringSetting": "MyAccount_COSMOSDB",
"direction": "out"
}
```


Here's the C# script code:

```
#r "Newtonsoft.Json"
using Microsoft.Azure.WebJobs.Host;
using Newtonsoft.Json.Linq;
using Microsoft.Extensions.Logging;
public static void Run(string myQueueItem, out object employeeDocument, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
dynamic employee = JObject.Parse(myQueueItem);
employeeDocument = new {
id = employee.name + "-" + employee.employeeId,
name = employee.name,
employeeId = employee.employeeId,
address = employee.address
};
}
```


#### Queue trigger, write docs using IAsyncCollector

To create multiple documents, you can bind to `ICollector<T>`

or `IAsyncCollector<T>`

where `T`

is one of the supported types.

This example refers to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV2
{
public class ToDoItem
{
public string id { get; set; }
public string Description { get; set; }
}
}
```


Here's the function.json file:

```
{
"bindings": [
{
"name": "toDoItemsIn",
"type": "queueTrigger",
"direction": "in",
"queueName": "todoqueueforwritemulti",
"connectionStringSetting": "AzureWebJobsStorage"
},
{
"type": "cosmosDB",
"name": "toDoItemsOut",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System;
using Microsoft.Extensions.Logging;
public static async Task Run(ToDoItem[] toDoItemsIn, IAsyncCollector<ToDoItem> toDoItemsOut, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed {toDoItemsIn?.Length} items");
foreach (ToDoItem toDoItem in toDoItemsIn)
{
log.LogInformation($"Description={toDoItem.Description}");
await toDoItemsOut.AddAsync(toDoItem);
}
}
```


### Azure Cosmos DB v1 trigger

The following example shows an Azure Cosmos DB trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function writes log messages when Azure Cosmos DB records are modified.

Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


Here's the C# script code:

```
#r "Microsoft.Azure.Documents.Client"
using System;
using Microsoft.Azure.Documents;
using System.Collections.Generic;
public static void Run(IReadOnlyList<Document> documents, TraceWriter log)
{
log.Info("Documents modified " + documents.Count);
log.Info("First document Id " + documents[0].Id);
}
```


### Azure Cosmos DB v1 input

This section contains the following examples:

[Queue trigger, look up ID from string](#queue-trigger-look-up-id-from-string-c-script)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-c-script)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-c-script)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-c-script)[HTTP trigger, get multiple docs, using SqlQuery](#http-trigger-get-multiple-docs-using-sqlquery-c-script)[HTTP trigger, get multiple docs, using DocumentClient](#http-trigger-get-multiple-docs-using-documentclient-c-script)

The HTTP trigger examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


#### Queue trigger, look up ID from string

The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function reads a single document and updates the document's text value.

Here's the binding data in the *function.json* file:

```
{
"name": "inputDocument",
"type": "documentDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"id" : "{queueTrigger}",
"partitionKey": "{partition key value}",
"connection": "MyAccount_COSMOSDB",
"direction": "in"
}
```


Here's the C# script code:

```
using System;
// Change input document contents using Azure Cosmos DB input binding
public static void Run(string myQueueItem, dynamic inputDocument)
{
inputDocument.text = "This has changed.";
}
```


#### Queue trigger, get multiple docs, using SqlQuery

The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

Here's the binding data in the *function.json* file:

```
{
"name": "documents",
"type": "documentdb",
"direction": "in",
"databaseName": "MyDb",
"collectionName": "MyCollection",
"sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
"connection": "CosmosDBConnection"
}
```


Here's the C# script code:

```
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{
foreach (var doc in documents)
{
// operate on each document
}
}
public class QueuePayload
{
public string departmentId { get; set; }
}
```


#### HTTP trigger, look up ID from query string

The following example shows a [C# script function](functions-reference-csharp) that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "documentDB",
"name": "toDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "in",
"Id": "{Query.id}"
}
],
"disabled": true
}
```


Here's the C# script code:

```
using System.Net;
public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, look up ID from route data

The following example shows a [C# script function](functions-reference-csharp) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
],
"route":"todoitems/{id}"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "documentDB",
"name": "toDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "in",
"Id": "{id}"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, get multiple docs, using SqlQuery

The following example shows a [C# script function](functions-reference-csharp) that retrieves a list of documents. The function is triggered by an HTTP request. The query is specified in the `SqlQuery`

attribute property.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "documentDB",
"name": "toDoItems",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "in",
"sqlQuery": "SELECT top 2 * FROM c order by c._ts desc"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
public static HttpResponseMessage Run(HttpRequestMessage req, IEnumerable<ToDoItem> toDoItems, TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.Info(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, get multiple docs, using DocumentClient

The following example shows a [C# script function](functions-reference-csharp) that retrieves a list of documents. The function is triggered by an HTTP request. The code uses a `DocumentClient`

instance provided by the Azure Cosmos DB binding to read a list of documents. The `DocumentClient`

instance could also be used for write operations.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "documentDB",
"name": "client",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "inout"
}
],
"disabled": false
}
```


Here's the C# script code:

```
#r "Microsoft.Azure.Documents.Client"
using System.Net;
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;
public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, DocumentClient client, TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");
string searchterm = req.GetQueryNameValuePairs()
.FirstOrDefault(q => string.Compare(q.Key, "searchterm", true) == 0)
.Value;
if (searchterm == null)
{
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.Info($"Searching for word: {searchterm} using Uri: {collectionUri.ToString()}");
IDocumentQuery<ToDoItem> query = client.CreateDocumentQuery<ToDoItem>(collectionUri)
.Where(p => p.Description.Contains(searchterm))
.AsDocumentQuery();
while (query.HasMoreResults)
{
foreach (ToDoItem result in await query.ExecuteNextAsync())
{
log.Info(result.Description);
}
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


### Azure Cosmos DB v1 output

This section contains the following examples:

- Queue trigger, write one doc
- Queue trigger, write docs using
`IAsyncCollector`


#### Queue trigger, write one doc

The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function uses a queue input binding for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the binding data in the *function.json* file:

```
{
"name": "employeeDocument",
"type": "documentDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": true,
"connection": "MyAccount_COSMOSDB",
"direction": "out"
}
```


Here's the C# script code:

```
#r "Newtonsoft.Json"
using Microsoft.Azure.WebJobs.Host;
using Newtonsoft.Json.Linq;
public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
dynamic employee = JObject.Parse(myQueueItem);
employeeDocument = new {
id = employee.name + "-" + employee.employeeId,
name = employee.name,
employeeId = employee.employeeId,
address = employee.address
};
}
```


#### Queue trigger, write docs using IAsyncCollector

To create multiple documents, you can bind to `ICollector<T>`

or `IAsyncCollector<T>`

where `T`

is one of the supported types.

This example refers to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


Here's the function.json file:

```
{
"bindings": [
{
"name": "toDoItemsIn",
"type": "queueTrigger",
"direction": "in",
"queueName": "todoqueueforwritemulti",
"connection": "AzureWebJobsStorage"
},
{
"type": "documentDB",
"name": "toDoItemsOut",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System;
public static async Task Run(ToDoItem[] toDoItemsIn, IAsyncCollector<ToDoItem> toDoItemsOut, TraceWriter log)
{
log.Info($"C# Queue trigger function processed {toDoItemsIn?.Length} items");
foreach (ToDoItem toDoItem in toDoItemsIn)
{
log.Info($"Description={toDoItem.Description}");
await toDoItemsOut.AddAsync(toDoItem);
}
}
```


### Azure SQL trigger

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-csx).

The example refers to a `ToDoItem`

class and a corresponding database table:

```
namespace AzureSQL.ToDo
{
public class ToDoItem
{
public Guid Id { get; set; }
public int? order { get; set; }
public string title { get; set; }
public string url { get; set; }
public bool? completed { get; set; }
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


[Change tracking](functions-bindings-azure-sql-trigger#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to a `IReadOnlyList<SqlChange<T>>`

, a list of `SqlChange`

objects each with two properties:

**Item:**the item that was changed. The type of the item should follow the table schema as seen in the`ToDoItem`

class.**Operation:**a value from`SqlChangeOperation`

enum. The possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a SQL trigger in a function.json file and a [C# script function](functions-reference-csharp) that is invoked when there are changes to the `ToDo`

table:

The following is binding data in the function.json file:

```
{
"name": "todoChanges",
"type": "sqlTrigger",
"direction": "in",
"tableName": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The following is the C# script function:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static void Run(IReadOnlyList<SqlChange<ToDoItem>> todoChanges, ILogger log)
{
log.LogInformation($"C# SQL trigger function processed a request.");
foreach (SqlChange<ToDoItem> change in todoChanges)
{
ToDoItem toDoItem = change.Item;
log.LogInformation($"Change operation: {change.Operation}");
log.LogInformation($"Id: {toDoItem.Id}, Title: {toDoItem.title}, Url: {toDoItem.url}, Completed: {toDoItem.completed}");
}
}
```


### Azure SQL input

More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-csx).

This section contains the following examples:

The examples refer to a `ToDoItem`

class and a corresponding database table:

```
namespace AzureSQL.ToDo
{
public class ToDoItem
{
public Guid Id { get; set; }
public int? order { get; set; }
public string title { get; set; }
public string url { get; set; }
public bool? completed { get; set; }
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


#### HTTP trigger, get row by ID from query string

The following example shows an Azure SQL input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function is triggered by an HTTP request that uses a query string to specify the ID. That ID is used to retrieve a `ToDoItem`

record with the specified query.

Note

The HTTP query string parameter is case-sensitive.

Here's the binding data in the *function.json* file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItem",
"type": "sql",
"direction": "in",
"commandText": "select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
"commandType": "Text",
"parameters": "@Id = {Query.id}",
"connectionStringSetting": "SqlConnectionString"
}
```


Here's the C# script code:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Collections.Generic;
public static IActionResult Run(HttpRequest req, ILogger log, IEnumerable<ToDoItem> todoItem)
{
return new OkObjectResult(todoItem);
}
```


#### HTTP trigger, delete rows

The following example shows an Azure SQL input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding to execute a stored procedure with input from the HTTP request query parameter. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the SQL database.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


Here's the binding data in the *function.json* file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItems",
"type": "sql",
"direction": "in",
"commandText": "DeleteToDo",
"commandType": "StoredProcedure",
"parameters": "@Id = {Query.id}",
"connectionStringSetting": "SqlConnectionString"
}
```


```
using System;
using System.Collections.Generic;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
namespace AzureSQL.ToDo
{
public static class DeleteToDo
{
// delete all items or a specific item from querystring
// returns remaining items
// uses input binding with a stored procedure DeleteToDo to delete items and return remaining items
[FunctionName("DeleteToDo")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "delete", Route = "DeleteFunction")] HttpRequest req,
ILogger log,
[Sql(commandText: "DeleteToDo", commandType: System.Data.CommandType.StoredProcedure,
parameters: "@Id={Query.id}", connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItems)
{
return new OkObjectResult(toDoItems);
}
}
}
```


Here's the C# script code:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Collections.Generic;
public static IActionResult Run(HttpRequest req, ILogger log, IEnumerable<ToDoItem> todoItems)
{
return new OkObjectResult(todoItems);
}
```


### Azure SQL output

More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-csx).

This section contains the following examples:

The examples refer to a `ToDoItem`

class and a corresponding database table:

```
namespace AzureSQL.ToDo
{
public class ToDoItem
{
public Guid Id { get; set; }
public int? order { get; set; }
public string title { get; set; }
public string url { get; set; }
public bool? completed { get; set; }
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


#### HTTP trigger, write records to a table

The following example shows a SQL output binding in a function.json file and a [C# script function](functions-reference-csharp) that adds records to a table, using data provided in an HTTP POST request as a JSON body.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItem",
"type": "sql",
"direction": "out",
"commandText": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The following is sample C# script code:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static IActionResult Run(HttpRequest req, ILogger log, out ToDoItem todoItem)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = new StreamReader(req.Body).ReadToEnd();
todoItem = JsonConvert.DeserializeObject<ToDoItem>(requestBody);
return new OkObjectResult(todoItem);
}
```


#### HTTP trigger, write to two tables

The following example shows a SQL output binding in a function.json file and a [C# script function](functions-reference-csharp) that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItem",
"type": "sql",
"direction": "out",
"commandText": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
},
{
"name": "requestLog",
"type": "sql",
"direction": "out",
"commandText": "dbo.RequestLog",
"connectionStringSetting": "SqlConnectionString"
}
```


The following is sample C# script code:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static IActionResult Run(HttpRequest req, ILogger log, out ToDoItem todoItem, out RequestLog requestLog)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = new StreamReader(req.Body).ReadToEnd();
todoItem = JsonConvert.DeserializeObject<ToDoItem>(requestBody);
requestLog = new RequestLog();
requestLog.RequestTimeStamp = DateTime.Now;
requestLog.ItemCount = 1;
return new OkObjectResult(todoItem);
}
public class RequestLog {
public DateTime RequestTimeStamp { get; set; }
public int ItemCount { get; set; }
}
```


### RabbitMQ output

The following example shows a RabbitMQ output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function reads in the message from an HTTP trigger and outputs it to the RabbitMQ queue.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"authLevel": "function",
"name": "input",
"methods": [
"get",
"post"
]
},
{
"type": "rabbitMQ",
"name": "outputMessage",
"queueName": "outputQueue",
"connectionStringSetting": "rabbitMQConnectionAppSetting",
"direction": "out"
}
]
}
```


Here's the C# script code:

```
using System;
using Microsoft.Extensions.Logging;
public static void Run(string input, out string outputMessage, ILogger log)
{
log.LogInformation(input);
outputMessage = input;
}
```


### SendGrid output

The following example shows a SendGrid output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "queueTrigger",
"name": "mymsg",
"queueName": "myqueue",
"connection": "AzureWebJobsStorage",
"direction": "in"
},
{
"type": "sendGrid",
"name": "$return",
"direction": "out",
"apiKey": "SendGridAPIKeyAsAppSetting",
"from": "{FromEmail}",
"to": "{ToEmail}"
}
]
}
```


Here's the C# script code:

```
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;
using Microsoft.Azure.WebJobs.Host;
public static SendGridMessage Run(Message mymsg, ILogger log)
{
SendGridMessage message = new SendGridMessage()
{
Subject = $"{mymsg.Subject}"
};
message.AddContent("text/plain", $"{mymsg.Content}");
return message;
}
public class Message
{
public string ToEmail { get; set; }
public string FromEmail { get; set; }
public string Subject { get; set; }
public string Content { get; set; }
}
```


### SignalR trigger

Here's example binding data in the *function.json* file:

```
{
"type": "signalRTrigger",
"name": "invocation",
"hubName": "SignalRTest",
"category": "messages",
"event": "SendMessage",
"parameterNames": [
"message"
],
"direction": "in"
}
```


And, here's the code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using System;
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
using Microsoft.Extensions.Logging;
public static void Run(InvocationContext invocation, string message, ILogger logger)
{
logger.LogInformation($"Receive {message} from {invocationContext.ConnectionId}.");
}
```


### SignalR input

The following example shows a SignalR connection info input binding in a *function.json* file and a [C# Script function](functions-reference-csharp) that uses the binding to return the connection information.

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "chat",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the C# Script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static SignalRConnectionInfo Run(HttpRequest req, SignalRConnectionInfo connectionInfo)
{
return connectionInfo;
}
```


You can set the `userId`

property of the binding to the value from either header using a [binding expression](functions-bindings-signalr-service-input#binding-expressions-for-http-trigger): `{headers.x-ms-client-principal-id}`

or `{headers.x-ms-client-principal-name}`

.

Example function.json:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "chat",
"userId": "{headers.x-ms-client-principal-id}",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the C# Script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static SignalRConnectionInfo Run(HttpRequest req, SignalRConnectionInfo connectionInfo)
{
// connectionInfo contains an access key token with a name identifier
// claim set to the authenticated user
return connectionInfo;
}
```


### SignalR output

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalRMessages",
"hubName": "<hub_name>",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


Here's the C# Script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
object message,
IAsyncCollector<SignalRMessage> signalRMessages)
{
return signalRMessages.AddAsync(
new SignalRMessage
{
Target = "newMessage",
Arguments = new [] { message }
});
}
```


You can send a message only to connections that have been authenticated to a user by setting the *user ID* in the SignalR message.

Example function.json:

```
{
"type": "signalR",
"name": "signalRMessages",
"hubName": "<hub_name>",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


Here's the C# script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
object message,
IAsyncCollector<SignalRMessage> signalRMessages)
{
return signalRMessages.AddAsync(
new SignalRMessage
{
// the message will only be sent to this user ID
UserId = "userId1",
Target = "newMessage",
Arguments = new [] { message }
});
}
```


You can send a message only to connections that have been added to a group by setting the *group name* in the SignalR message.

Example function.json:

```
{
"type": "signalR",
"name": "signalRMessages",
"hubName": "<hub_name>",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


Here's the C# Script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
object message,
IAsyncCollector<SignalRMessage> signalRMessages)
{
return signalRMessages.AddAsync(
new SignalRMessage
{
// the message will be sent to the group with this name
GroupName = "myGroup",
Target = "newMessage",
Arguments = new [] { message }
});
}
```


SignalR Service allows users or connections to be added to groups. Messages can then be sent to a group. You can use the `SignalR`

output binding to manage groups.

The following example adds a user to a group.

Example *function.json*

```
{
"type": "signalR",
"name": "signalRGroupActions",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"hubName": "chat",
"direction": "out"
}
```


*Run.csx*

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
HttpRequest req,
ClaimsPrincipal claimsPrincipal,
IAsyncCollector<SignalRGroupAction> signalRGroupActions)
{
var userIdClaim = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier);
return signalRGroupActions.AddAsync(
new SignalRGroupAction
{
UserId = userIdClaim.Value,
GroupName = "myGroup",
Action = GroupAction.Add
});
}
```


The following example removes a user from a group.

Example *function.json*

```
{
"type": "signalR",
"name": "signalRGroupActions",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"hubName": "chat",
"direction": "out"
}
```


*Run.csx*

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
HttpRequest req,
ClaimsPrincipal claimsPrincipal,
IAsyncCollector<SignalRGroupAction> signalRGroupActions)
{
var userIdClaim = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier);
return signalRGroupActions.AddAsync(
new SignalRGroupAction
{
UserId = userIdClaim.Value,
GroupName = "myGroup",
Action = GroupAction.Remove
});
}
```


### Twilio output

The following example shows a Twilio output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function uses an `out`

parameter to send a text message.

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "twilioSms",
"name": "message",
"accountSidSetting": "TwilioAccountSid",
"authTokenSetting": "TwilioAuthToken",
"from": "+1425XXXXXXX",
"direction": "out",
"body": "Azure Functions Testing"
}
```


Here's C# script code:

```
#r "Newtonsoft.Json"
#r "Twilio"
#r "Microsoft.Azure.WebJobs.Extensions.Twilio"
using System;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs.Extensions.Twilio;
using Twilio.Rest.Api.V2010.Account;
using Twilio.Types;
public static void Run(string myQueueItem, out CreateMessageOptions message, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
// In this example the queue item is a JSON string representing an order that contains the name of a
// customer and a mobile number to send text updates to.
dynamic order = JsonConvert.DeserializeObject(myQueueItem);
string msg = "Hello " + order.name + ", thank you for your order.";
// You must initialize the CreateMessageOptions variable with the "To" phone number.
message = new CreateMessageOptions(new PhoneNumber("+1704XXXXXXX"));
// A dynamic message can be set instead of the body in the output binding. In this example, we use
// the order information to personalize a text message.
message.Body = msg;
}
```


You can't use out parameters in asynchronous code. Here's an asynchronous C# script code example:

```
#r "Newtonsoft.Json"
#r "Twilio"
#r "Microsoft.Azure.WebJobs.Extensions.Twilio"
using System;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs.Extensions.Twilio;
using Twilio.Rest.Api.V2010.Account;
using Twilio.Types;
public static async Task Run(string myQueueItem, IAsyncCollector<CreateMessageOptions> message, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
// In this example the queue item is a JSON string representing an order that contains the name of a
// customer and a mobile number to send text updates to.
dynamic order = JsonConvert.DeserializeObject(myQueueItem);
string msg = "Hello " + order.name + ", thank you for your order.";
// You must initialize the CreateMessageOptions variable with the "To" phone number.
CreateMessageOptions smsText = new CreateMessageOptions(new PhoneNumber("+1704XXXXXXX"));
// A dynamic message can be set instead of the body in the output binding. In this example, we use
// the order information to personalize a text message.
smsText.Body = msg;
await message.AddAsync(smsText);
}
```


### Warmup trigger

The following example shows a warmup trigger in a *function.json* file and a [C# script function](functions-reference-csharp) that runs on each new instance when it's added to your app.

Not supported for version 1.x of the Functions runtime.

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


```
public static void Run(WarmupContext warmupContext, ILogger log)
{
log.LogInformation("Function App instance is warm.");
}
```
