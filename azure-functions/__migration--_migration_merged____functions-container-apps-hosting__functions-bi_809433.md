---
merged_at: 2026-02-05T08:51:00.595442
merged_files: 2
---


---
<!-- Source: N/A -->

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
| Reserved concurrency specifies the maximum number of concurrent instances that a function can have. This limit ensures that a portion of your account's concurrency quota is set aside exclusively for that function. AWS Lambda dynamically scales out to handle incoming requests even when reserved concurrency is set, as long as the requests don't exceed the specified reserved concurrency limit. The lower limit for reserved concurrency in AWS Lambda is 1. The upper limit for reserved concurrency in AWS Lambda is determined by the account's regional concurrency quota. By default, this limit is 1,000 concurrent operations for each region. | Azure Functions doesn't have an equivalent feature to reserved concurrency. To achieve similar functionality, isolate specific functions into separate function apps and set the maximum scale-out limit for each app. Azure Functions dynamically scales out, or adds more instances, and scales in, or removes instances, within the scale-out limit set. By default, apps that run in a Flex Consumption plan start with a configurable limit of 100 overall instances. The lowest maximum instance count value is 1, and the highest supported maximum instance count value is 1,000.
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

The default maximum instance count is 100, and it must be set to a value between 1 and 1,000.

Note

Reducing maximum instance count below 40 for HTTP function apps can cause frequent request failures and prolonged throttling windows when traffic exceeds capacity. This setting is intended only for advanced scenarios where limited scale-out is acceptable and has been fully tested.

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-container-apps-hosting -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redisstream -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-java -->

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
<!-- Source: N/A -->

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
public class HttpTriggerCSharp(ILogger<HttpTriggerCSharp> logger)
{
[Function("HttpTriggerCSharp")]
public IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get")] HttpRequest req)
{
logger.LogInformation("C# HTTP trigger function processed a request.");
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

---
<!-- Source: N/A -->

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
