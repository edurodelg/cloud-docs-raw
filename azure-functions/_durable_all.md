---
merged_at: 2026-02-05T08:51:00.326055
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/durable-task-scheduler-work-item-throughput -->

# Azure Functions Durable Task Scheduler action throughput

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Durable Task Scheduler was benchmarked against other storage providers, including the Azure Storage, MSSQL, and Netherite providers. The results show the Durable Task Scheduler provides better [action](durable-task-scheduler-dedicated-sku#what-is-an-action) throughput than the other options, which translates into more orchestrator, entity, and activity tasks being processed in a given time period.

The following table shows the results of a series of benchmarks ran to compare the relative throughput of the Durable Task Scheduler provider vs. the default Azure Storage provider. The Azure Storage provider was chosen as the comparison because it's currently the default and most commonly used backend option for Durable Function apps.


Note

The results shown in the chart are for an early preview version of the Durable Task Scheduler feature, configured with the lowest available scale settings. The results are expected to improve as the backend provider matures and gets closer to general availability.

To test the relative throughput of the backend providers, these benchmarks were run using a standard orchestrator function that calls five activity functions, one for each city, in a sequence. Each activity simply returns a "Hello, {cityName}!" string value and doesn't do any other work.

The intent of the benchmark is to measure the overhead of each backend without doing anything too complicated. This type of sequential orchestration was chosen due to its commonality in function apps that include Durable Functions.

### Test details

The test consists of the following criteria:

- The function app used for this test runs on
**one to four Elastic Premium EP2 instances**. - The orchestration code was written in C# using the
**.NET Isolated worker model on NET 8**. - The same app was used for all storage providers, and the only change was the backend storage provider configuration.
- The test is triggered using an HTTP trigger which starts
**5,000 orchestrations concurrently**.

After the test completes, the throughput is calculated by dividing the total number of completed orchestrations by the total execution time. The test was run multiple times for each storage provider configuration to ensure the results were consistent.

This benchmark showed that the Durable Task Scheduler is roughly **five times faster** than the Azure Storage provider. Your results might vary depending on:

- The complexity of your orchestrations and activities
- The number of orchestrations running concurrently
- The size of the data payloads being passed between orchestrations and activities
- Other factors such as the virtual machine size.

Note

These results are meant to provide a rough comparison of the relative performance of the storage provider backends at the time the test was run. These results shouldn't be taken as definitive.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/durable-task-scheduler-dedicated-sku -->

# Azure Functions Durable Task Scheduler Pricing and SKU Options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Durable Task Scheduler offers two pricing models to accommodate different workload requirements, usage patterns, and preferred billing models:

In this article, you learn about actions, the available SKU options, and their pricing structures.

## What is an action?

An action is a message dispatched by the Durable Task Scheduler to your application, triggering the execution of an orchestrator, activity, or entity functions. Functions triggered by an action include:

- Starting an orchestration or suborchestration
- Starting an activity
- Completing a timer
- Triggering an external event
- Executing an entity operation
- Suspending, resuming, or terminating an orchestration
- Processing the result of an activity, entity call, entity lock, or suborchestration

The following diagram explains how to calculate actions in your orchestration.


### Example

Let's say you have an orchestration that calls three different activities.


In this example, you can see how Durable Task Scheduler processes each action:

- Orchestrator start (
`RunOrchestrator`

) uses one action - Activity 1 (
`(nameof(SayHello), "Tokyo")`

) uses two actions:- Scheduling the activity
- Processing the result

- Activity 2 (
`(nameof(SayHello), "Seattle")`

) uses two actions:- Scheduling the activity
- Processing the result

- Activity 3 (
`(nameof(SayHello), "London")`

) uses two actions:- Scheduling the activity
- Processing the result


## Available SKUs

Durable Task Scheduler offers two SKU options: Dedicated and Consumption (preview).

### Dedicated SKU

The Dedicated SKU provides performance and pricing through preallocated Capacity Units (CUs). You can purchase up to three CUs.

Currently, you're limited to 25 task hubs when using the Dedicated SKU. For more quota, [contact support](https://github.com/Azure/azure-functions-durable-extension/issues).

#### Key features

| Feature | Description |
|---|---|
| Base cost | Fixed monthly cost per CU (regional pricing). Not "per action" billing. |
| Performance | Each CU supports up to 2,000 actions per second and 50GB of orchestration data storage |
| Orchestration data retention | Up to 90 days |
| Custom scaling | Configure CUs to match your workload needs. 1 CU required per deployment. |
| High availability | High availability with multi-CU deployments. A minimum of 3 CUs is required. |

#### Calculating Capacity Units for the Dedicated SKU

##### Example 1

You have an orchestration with 5 activities, plus error handling, and averaging 12 actions per orchestration (orchestrator and activity invocations). Let's calculate running 20 million orchestrations per month.

| Activity | Calculation | Result |
|---|---|---|
| Monthly actions | 20,000,000 × 12 | 240,000,000 actions |
| Actions per second | 240,000,000 ÷ 2,628,000 (seconds in a month) | ≈ 91 actions/second |
| Required CUs | 91 ÷ 2,000 | 240,000,000 actions CUs needed: 0.046 → 1 CU sufficient |

##### Example 2

A large enterprise runs 500 million complex orchestrations monthly, with an average of 15 actions per orchestration (multiple activities with orchestrator coordination).

| Activity | Calculation | Result |
|---|---|---|
| Monthly actions | 500 million × 13 | 6.5 billion actions |
| Actions per second | 6.5 billion ÷ 2,628,000 | ≈ 2,473 actions/second |
| Required CUs | 2,473 ÷ 2,000 | 240,000,000 actions CUs needed: 1.23 → 2 CUs sufficient |

##### Example 3

A Software as a Service (SaaS) platform supports 800 million orchestrations monthly, each with an average of 15 actions (user interactions, background processing, and external API calls).

| Activity | Calculation | Result |
|---|---|---|
| Monthly actions | 800 million × 15 | 12 billion actions |
| Actions per second | 12 billion ÷ 2,628,000 | ≈ 4,571 actions/second |
| Required CUs | 4,571 ÷ 2,000 | 240,000,000 actions CUs needed: 2.29 → 3 CUs sufficient |

### Consumption SKU (preview)

Note

The Consumption SKU is currently in preview. [Learn more about the SKU and orchestration framework recommended for production use.](choose-orchestration-framework#orchestration-framework-options)

The Consumption SKU offers a pay-as-you-use model, ideal for variable workloads and development scenarios.

Currently, you're limited to 5 task hubs when using the Consumption SKU. For more quota, [contact support](https://github.com/Azure/azure-functions-durable-extension/issues).

#### Key Features

| Feature | Description |
|---|---|
| Pay-Per-Use | Only pay for actions dispatched. No upfront costs, minimum commitments, or base fees |
| Performance | Up to 500 actions per second. |
| Data retention | 30-day maximum retention |

##### Example 1

A development team is testing simple orchestrations, each with three actions (using [the "Hello City" pattern](https://github.com/Azure-Samples/Durable-Task-Scheduler/tree/main/quickstarts/durable-functions/dotnet/HelloCities)), and runs 10,000 orchestrations per month.

| Activity | Calculation | Result |
|---|---|---|
| Monthly actions | 10,000 × 3 | 30,000 actions |
| Cost | 30,000 × $0.003 | $90/month |

##### Example 2

An e-commerce application experiences dynamic workload scaling during promotional sales events, especially on weekends. It uses an orchestration comprising seven total actions, which executes approximately 20,000 times per month.

| Activity | Calculation | Result |
|---|---|---|
| Monthly actions | 20,000 × 7 | 140,000 actions |
| Cost | 140,000 × $0.003 | $420/month |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/durable-task-scheduler-dashboard -->

# Debug and manage orchestrations using the Azure Functions Durable Task Scheduler dashboard

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Observe, manage, and debug your task hub or scheduler's orchestrations using the Durable Task Scheduler dashboard. The dashboard is available when you run the [Durable Task Scheduler emulator](durable-task-scheduler#emulator-for-local-development) locally or create a scheduler resource on Azure.

Running the emulator locally doesn't require authentication.

Creating a scheduler resource on Azure requires [assigning the Durable Task Data Contributor role to your identity](durable-task-scheduler-identity). You can then access the dashboard via either:

- The task hub's dashboard endpoint URL in the Azure portal
- Navigate to
`https://dashboard.durabletask.io/`

combined with your task hub endpoint.

In this article, you learn how to:

- Assign one of the Durable Task roles to your developer identity.
- Access the Durable Task Scheduler dashboard.
- View orchestration status and history via the Durable Task Scheduler dashboard.

## Prerequisites

Before you begin:

[Install the latest Azure CLI](/en-us/cli/azure/install-azure-cli)[Create a scheduler and task hub resource](develop-with-durable-task-scheduler)[Configure managed identity for your Durable Task Scheduler resource](durable-task-scheduler-identity)

## Access the Durable Task Scheduler dashboard

Assign the required role to your *developer identity (email)* to gain access to the [Durable Task Scheduler dashboard](durable-task-scheduler-dashboard).

Set the assignee to your developer identity.

`assignee=$(az ad user show --id "someone@microsoft.com" --query "id" --output tsv)`

Set the scope. Granting access on the scheduler scope gives access to

*all*task hubs in that scheduler.**Task Hub**`scope="/subscriptions/SUBSCRIPTION_ID/resourceGroups/RESOURCE_GROUP/providers/Microsoft.DurableTask/schedulers/SCHEDULER_NAME/taskHubs/TASK_HUB_NAME"`

**Scheduler**`scope="/subscriptions/SUBSCRIPTION_ID/resourceGroups/RESOURCE_GROUP/providers/Microsoft.DurableTask/schedulers/SCHEDULER_NAME"`

Grant access. Run the following command to create the role assignment and grant access.

`az role assignment create \ --assignee "$assignee" \ --role "Durable Task Data Contributor" \ --scope "$scope"`

*Expected output*The following output example shows a developer identity assigned with the Durable Task Data Contributor role on the

*scheduler*level:`{ "condition": null, "conditionVersion": null, "createdBy": "YOUR_DEVELOPER_CREDENTIAL_ID", "createdOn": "2024-12-20T01:36:45.022356+00:00", "delegatedManagedIdentityResourceId": null, "description": null, "id": "/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups/YOUR_RESOURCE_GROUP/providers/Microsoft.DurableTask/schedulers/YOUR_DTS_NAME/providers/Microsoft.Authorization/roleAssignments/ROLE_ASSIGNMENT_ID", "name": "ROLE_ASSIGNMENT_ID", "principalId": "YOUR_DEVELOPER_CREDENTIAL_ID", "principalName": "YOUR_EMAIL", "principalType": "User", "resourceGroup": "YOUR_RESOURCE_GROUP", "roleDefinitionId": "/subscriptions/YOUR_SUBSCRIPTION/providers/Microsoft.Authorization/roleDefinitions/ROLE_DEFINITION_ID", "roleDefinitionName": "Durable Task Data Contributor", "scope": "/subscriptions/YOUR_SUBSCRIPTION/resourceGroups/YOUR_RESOURCE_GROUP/providers/Microsoft.DurableTask/schedulers/YOUR_DTS_NAME", "type": "Microsoft.Authorization/roleAssignments", "updatedBy": "YOUR_DEVELOPER_CREDENTIAL_ID", "updatedOn": "2024-12-20T01:36:45.022356+00:00" }`

After granting access, go to

`https://dashboard.durabletask.io/`

and fill out the required information about your scheduler and task hub to see the dashboard.

Note

The following instruction shows a role assignment scoped to a specific task hub. If you need access to *all* task hubs in a scheduler, perform the assignment on the scheduler level.

Navigate to the Durable Task Scheduler resource on the portal.

Click on a task hub name.

In the left menu, select

**Access control (IAM)**.Click

**Add**to add a role assignment.Search for and select

**Durable Task Data Contributor**. Click**Next**.On the

**Members**tab, for**Assign access to**, select**User, group, or service principal**.For

**Members**, click**+ Select members**.In the

**Select members**pane, search for your name or email:Pick your email and click the

**Select**button.Click

**Review + assign**to finish assigning the role.Once the role is assigned, click

**Overview**on the left menu of the task hub resource and navigate to the dashboard URL located at the top*Essentials*section.

## Monitor orchestration progress and execution history

The dashboard allows you to monitor orchestration progress and review execution history. You can also filter by orchestration metadata, such as state and timestamps.


View orchestration inputs and outputs:


## Detailed view of orchestration execution

You can drill into orchestration instances to view execution details and activity progress. This view helps you diagnose problems or gain visibility into the status of an orchestration.

In the following image, the *Timeline* view of an orchestration execution. In this "ProcessDocument" orchestration, the "WriteDoc" activity retried three times (unsuccessfully) with five seconds in between retry.


You can also view inputs and outputs of activities in an orchestration:


### Other views of orchestration execution sequence

The *History* view shows detailed event sequence, timestamps, and payload:


The *Sequence* view gives another way of visualizing event sequence:


## Orchestration management

The dashboard includes features for managing orchestrations on demand, such as starting, pausing, resuming, and terminating.


## Next steps

For Durable Task Scheduler for Durable Functions:

[Quickstart: Configure a Durable Functions app to use the Durable Task Scheduler](quickstart-durable-task-scheduler)[Create Durable Task Scheduler resources and view them in the dashboard](develop-with-durable-task-scheduler)

For Durable Task Scheduler for the Durable Task SDKs:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/troubleshoot-durable-task-scheduler -->

# Troubleshoot the Azure Functions durable task scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

Microsoft support engineers are available to help diagnose issues with your application. If you're not able to diagnose your problem after going through this article, you can file a support ticket by going the **Help** > **Support + troubleshooting** section of durable task scheduler resource on Azure portal.

## Check connection string and access to durable task scheduler

When your app isn't running as expected, first check if you have:

- The correct connection string format.
- Authentication set up correctly.

### Local development

Check the connection string, which should have this format:

`Endpoint=http://localhost:<port number>;Authentication=None`

. Ensure the port number is the one mapped to`8080`

on the[container running the durable task scheduler emulator](quickstart-durable-task-scheduler#set-up-the-durable-task-emulator).Along with the durable task scheduler emulator, make sure

[the Azure Storage emulator, Azurite, is started](quickstart-durable-task-scheduler#test-locally). Azurite is needed for components of the app related to Functions.

### Running on Azure

Check your app for the environment variables

`DURABLE_TASK_SCHEDULER_CONNECTION_STRING`

and`TASKHUB_NAME`

.Check the value of

`DURABLE_TASK_SCHEDULER_CONNECTION_STRING`

. Specifically, verify that the scheduler endpoint and authentication type are correct. The connection string should be formatted as follows when using:*User-assigned managed identity*:`Endpoint={scheduler endpoint};Authentication=ManagedIdentity;ClientID={client id}`

, where`client id`

is the identity's client ID.*System-assigned managed identity*:`Endpoint={scheduler endpoint};Authentication=ManagedIdentity`


Ensure the required role-based access control (RBAC) permission is

[granted to the identity](develop-with-durable-task-scheduler#configure-identity-based-authentication-for-app-to-access-durable-task-scheduler)needing to access the specified task hub or scheduler.- When accessing the dashboard, ensure permission is
[assigned to your own identity (email)](durable-task-scheduler-dashboard#access-the-durable-task-scheduler-dashboard).

- When accessing the dashboard, ensure permission is
If user-assigned managed identity is used, ensure the

[identity is assigned to your app](durable-task-scheduler-identity#assign-managed-identity-to-your-app).

## Error deploying durable functions app to Azure

If your deployment fails with an error such as `Encountered an error (ServiceUnavailable) from host runtime`

from Visual Studio Code, first check your app to ensure the required [environment variables](durable-task-scheduler-identity#add-environment-variables-to-app) are set correctly. Then redeploy your app. If you see an error loading functions, click the "Refresh" button.

## Unknown error retrieving details of this task hub

If you get an `Unknown error retrieving details of this task hub`

error on the durable task scheduler dashboard, the reason could be:

Your identity (email) doesn't have the required permission assigned for that task hub. Follow instructions to

[grant the permission](durable-task-scheduler-dashboard), then access the dashboard again.Your task hub was deleted.


## Can't delete resource

Make sure you delete all task hubs in the durable task scheduler environment. If you haven't, you receive the following error message:

```
{
"error": {
"code": "CannotDeleteResource",
"message": "Cannot delete resource while nested resources exist. Some existing nested resource IDs include: 'Microsoft.DurableTask/schedulers/YOUR_SCHEDULER/taskhubs/YOUR_TASKHUB'. Please delete all nested resources before deleting this resource."
}
}
```


## Can't determine project to build

If, after starting Azurite, you encounter the error: `“Can't determine Project to build. Expected 1 .csproj or .fsproj but found 2”`

:

- Delete the
**bin**and**obj**directories in your app. - Try running
`func start`

again.

## Can't find native binaries for ARM

If you see gRPC errors related to not finding native binaries for ARM (such as on a Mx Mac), you may need to add the following workaround to the end of your `extensions.csproj`

file.

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net6.0</TargetFramework>
<WarningsAsErrors></WarningsAsErrors>
<DefaultItemExcludes>**</DefaultItemExcludes>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.Azure.WebJobs.Extensions.DurableTask" Version="2.13.7" />
<PackageReference Include="Microsoft.Azure.WebJobs.Extensions.DurableTask.AzureManaged" Version="0.3.0-alpha" />
<PackageReference Include="Microsoft.Azure.WebJobs.Script.ExtensionsMetadataGenerator" Version="1.1.3" />
</ItemGroup>
<!-- Add the below groups/targets to workaround gRPC issues on ARM devices. -->
<ItemGroup>
<PackageReference Include="Contrib.Grpc.Core.M1" Version="2.41.0" />
</ItemGroup>
<Target Name="CopyGrpcNativeAssetsToOutDir" AfterTargets="Build">
<ItemGroup>
<NativeAssetToCopy Condition="$([MSBuild]::IsOSPlatform('OSX'))" Include="$(OutDir)runtimes/osx-arm64/native/*"/>
</ItemGroup>
<Copy SourceFiles="@(NativeAssetToCopy)" DestinationFolder="$(OutDir).azurefunctions/runtimes/osx-arm64/native"/>
</Target>
</Project>
```


## Experiencing gRPC runtime issues

For Mx Mac (ARM64) users, you may run into gRPC runtime issues with durable functions. As a workaround:

Reference the

`2.41.0`

version of the`Contrib.Grpc.Core.M1`

NuGet package.Add a custom after-build target that ensures the correct ARM64 version of the gRPC libraries can be found.

`<Project> <ItemGroup> <PackageReference Include="Contrib.Grpc.Core.M1" Version="2.41.0" /> </ItemGroup> <Target Name="CopyGrpcNativeAssetsToOutDir" AfterTargets="Build"> <ItemGroup> <NativeAssetToCopy Condition="$([MSBuild]::IsOSPlatform('OSX'))" Include="$(OutDir)runtimes/osx-arm64/native/*"/> </ItemGroup> <Copy SourceFiles="@(NativeAssetToCopy)" DestinationFolder="$(OutDir).azurefunctions/runtimes/osx-arm64/native"/> </Target> </Project>`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/develop-with-durable-task-scheduler -->

# Develop with Durable Task Scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Durable Task Scheduler is a highly performant, fully managed backend provider for Durable Functions with an [out-of-the-box monitoring dashboard](durable-task-scheduler-dashboard). Azure offers two developer-oriented orchestration frameworks that work with Durable Functions to build apps: Durable Task SDKs and Durable Functions.

In this article, you learn to:

- Run the Durable Task Scheduler emulator
- Perform CRUD operations on a scheduler and task hub.

Learn more about Durable Task Scheduler [features](durable-task-scheduler#feature-highlights), [supported regions](durable-task-scheduler#limitations-and-considerations), and [plans](durable-task-scheduler#limitations-and-considerations).

## Durable Task Scheduler emulator

The Durable Task Scheduler emulator is only available as a Docker image today.

Pull the docker image containing the emulator.

`docker pull mcr.microsoft.com/dts/dts-emulator:latest`

Run the emulator.

`docker run -itP mcr.microsoft.com/dts/dts-emulator:latest`

This command exposes a single task hub named

`default`

. If you need more than one task hub, you can set the environment variable`DTS_TASK_HUB_NAMES`

on the container to a comma-delimited list of task hub names like in the following command:`docker run -itP -e DTS_TASK_HUB_NAMES=taskhub1,taskhub2,taskhub3 mcr.microsoft.com/dts/dts-emulator:latest`


## Prerequisites

## Set up the CLI

Log in to the Azure CLI and make sure you have the latest installed.

`az login az upgrade`

Install the Durable Task Scheduler CLI extension.

`az extension add --name durabletask`

If you already installed the Durable Task Scheduler CLI extension, upgrade to the latest version.

`az extension update --name durabletask`

Check your installed version:

`az extension show --name durabletask`


[Learn more about the various az durabletask commands you can use.](https://github.com/Azure/azure-cli-extensions/tree/main/src/durabletask)

## Create a scheduler and task hub

Create a resource group.

`az group create --name YOUR_RESOURCE_GROUP --location LOCATION`

Using the

`durabletask`

CLI extension, create a scheduler.`az durabletask scheduler create --name "YOUR_SCHEDULER" --resource-group "YOUR_RESOURCE_GROUP" --location "LOCATION" --ip-allowlist "[0.0.0.0/0]" --sku-name "dedicated" --sku-capacity "1"`

The creation process may take up to 15 minutes to complete.

*Output*`{ "id": "/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups/YOUR_RESOURCE_GROUP/providers/Microsoft.DurableTask/schedulers/YOUR_SCHEDULER", "location": "northcentralus", "name": "YOUR_SCHEDULER", "properties": { "endpoint": "https://YOUR_SCHEDULER.northcentralus.durabletask.io", "ipAllowlist": [ "0.0.0.0/0" ], "provisioningState": "Succeeded", "sku": { "capacity": 1, "name": "Dedicated", "redundancyState": "None" } }, "resourceGroup": "YOUR_RESOURCE_GROUP", "systemData": { "createdAt": "2025-01-06T21:22:59Z", "createdBy": "YOUR_EMAIL@example.com", "createdByType": "User", "lastModifiedAt": "2025-01-06T21:22:59Z", "lastModifiedBy": "YOUR_EMAIL@example.com", "lastModifiedByType": "User" }, "tags": {} }`

Create a task hub.

`az durabletask taskhub create --resource-group YOUR_RESOURCE_GROUP --scheduler-name YOUR_SCHEDULER --name YOUR_TASKHUB`

*Output*`{ "id": "/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups/YOUR_RESOURCE_GROUP/providers/Microsoft.DurableTask/schedulers/YOUR_SCHEDULERS/taskHubs/YOUR_TASKHUB", "name": "YOUR_TASKHUB", "properties": { "provisioningState": "Succeeded" }, "resourceGroup": "YOUR_RESOURCE_GROUP", "systemData": { "createdAt": "2024-09-18T22:13:56.5467094Z", "createdBy": "OBJECT_ID", "createdByType": "User", "lastModifiedAt": "2024-09-18T22:13:56.5467094Z", "lastModifiedBy": "OBJECT_ID", "lastModifiedByType": "User" }, "type": "microsoft.durabletask/scheduler/taskhubs" }`


In the Azure portal, search for

**Durable Task Scheduler**and select it from the results.Click

**Create**to open the**Azure Functions: Durable Task Scheduler**pane.Fill out the fields in the

**Basics**tab. Click**Review + create**.Note

The Consumption SKU is currently in preview.

[Learn more about the SKU and orchestration framework combinations recommended for production use.](choose-orchestration-framework#orchestration-framework-options)Once the validation passes, click

**Create**.Deployment may take around 15 to 20 minutes.


## View all Durable Task Scheduler resources in a subscription

Get a list of all scheduler names within a subscription by running the following command.

`az durabletask scheduler list --subscription <SUBSCRIPTION_ID>`

You can narrow down results to a specific resource group by adding the

`--resource-group`

flag.`az durabletask scheduler list --subscription <SUBSCRIPTION_ID> --resource-group <RESOURCE_GROUP_NAME>`


In the Azure portal, search for **Durable Task Scheduler** and select it from the results.


You can see the list of scheduler resources created in all subscriptions you have access to.

## View all task hubs in a Durable Task Scheduler

Retrieve a list of task hubs in a specific scheduler by running:

```
az durabletask taskhub list --resource-group <RESOURCE_GROUP_NAME> --scheduler-name <SCHEDULER_NAME>
```


You can see all the task hubs created in a scheduler on the **Overview** of the resource on Azure portal.


## Delete the scheduler and task hub

Delete the scheduler:

`az durabletask scheduler --resource-group YOUR_RESOURCE_GROUP --scheduler-name YOUR_SCHEDULER`

Delete a task hub:

`az durabletask taskhub delete --resource-group YOUR_RESOURCE_GROUP --scheduler-name YOUR_SCHEDULER --name YOUR_TASKHUB`


Open the scheduler resource on Azure portal and click

**Delete**:Find the scheduler with the task hub you want to delete, then click into that task hub. Click

**Delete**:

## Configure identity-based authentication for app to access Durable Task Scheduler

Durable Task Scheduler **only** supports either *user-assigned* or *system-assigned* managed identity authentication. **User-assigned identities are recommended,** as they aren't tied to the lifecycle of the app and can be reused after the app is deprovisioned.

Learn more about [identity-based access in Durable Task Scheduler](durable-task-scheduler-identity).

## Access the Durable Task Scheduler dashboard

[Assign the required role to your developer identity (email)](durable-task-scheduler-dashboard) to gain access to the Durable Task Scheduler dashboard.

## Next steps

For using Durable Task Scheduler with Durable Functions:

For using Durable Task Scheduler with the Durable Task SDKs:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/durable-task-scheduler-identity -->

# Configure managed identity for Durable Task Scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Durable Task Scheduler **only** supports either *user-assigned* or *system-assigned* managed identity authentication. **User-assigned identities are recommended,** as they aren't tied to the lifecycle of the app and can be reused after the app is deprovisioned.

You can grant the following Durable Task Scheduler related roles to an identity:

| Role | Description |
|---|---|
Durable Task Data Contributor |
Role for all data access operations. This role is a superset of all other roles. |
Durable Task Worker |
Role used by worker applications to interact with the Durable Task Scheduler. Assign this role if your app is used only for processing orchestrations, activities, and entities. |
Durable Task Data Reader |
Role to read all Durable Task Scheduler data. Assign this role if you only need a list of orchestrations and entities payloads. |

Note

Most Durable Functions apps require the *Durable Task Data Contributor* role.

In this article, you learn how to grant permissions to an identity resource and configure your compute app to use the identity for access to schedulers and task hubs.

## Assign role-based access control (RBAC) to a managed identity resource

Create a user-assigned managed identity

`az identity create -g RESOURCE_GROUP_NAME -n IDENTITY_NAME`

Set the assignee to identity resource created

`assignee=$(az identity show --name IDENTITY_NAME --resource-group RESOURCE_GROUP_NAME --query 'clientId' --output tsv)`

Set the scope. Granting access on the scheduler scope gives access to

*all*task hubs in that scheduler.**Task Hub**`scope="/subscriptions/SUBSCRIPTION_ID/resourceGroups/RESOURCE_GROUP_NAME/providers/Microsoft.DurableTask/schedulers/SCHEDULER_NAME/taskHubs/TASKHUB_NAME"`

**Scheduler**`scope="/subscriptions/SUBSCRIPTION_ID/resourceGroups/RESOURCE_GROUP_NAME/providers/Microsoft.DurableTask/schedulers/SCHEDULER_NAME"`

Grant access. Run the following command to create the role assignment and grant access.

`az role assignment create \ --assignee "$assignee" \ --role "Durable Task Data Contributor" \ --scope "$scope"`

*Expected output*The following output example shows a developer identity assigned with the Durable Task Data Contributor role on the

*scheduler*level:`{ "condition": null, "conditionVersion": null, "createdBy": "YOUR_DEVELOPER_CREDENTIAL_ID", "createdOn": "2024-12-20T01:36:45.022356+00:00", "delegatedManagedIdentityResourceId": null, "description": null, "id": "/subscriptions/YOUR_SUBSCRIPTION_ID/resourceGroups/YOUR_RESOURCE_GROUP/providers/Microsoft.DurableTask/schedulers/YOUR_DTS_NAME/providers/Microsoft.Authorization/roleAssignments/ROLE_ASSIGNMENT_ID", "name": "ROLE_ASSIGNMENT_ID", "principalId": "YOUR_DEVELOPER_CREDENTIAL_ID", "principalName": "YOUR_EMAIL", "principalType": "User", "resourceGroup": "YOUR_RESOURCE_GROUP", "roleDefinitionId": "/subscriptions/YOUR_SUBSCRIPTION/providers/Microsoft.Authorization/roleDefinitions/ROLE_DEFINITION_ID", "roleDefinitionName": "Durable Task Data Contributor", "scope": "/subscriptions/YOUR_SUBSCRIPTION/resourceGroups/YOUR_RESOURCE_GROUP/providers/Microsoft.DurableTask/schedulers/YOUR_DTS_NAME", "type": "Microsoft.Authorization/roleAssignments", "updatedBy": "YOUR_DEVELOPER_CREDENTIAL_ID", "updatedOn": "2024-12-20T01:36:45.022356+00:00" }`


Note

The following instruction shows a role assignment scoped to a specific task hub. If you need access to *all* task hubs in a scheduler, perform the assignment on the scheduler level.

Navigate to the durable task scheduler resource on the portal.

Click on a task hub name.

In the left menu, select

**Access control (IAM)**.Click

**Add**to add a role assignment.Search for and select

**Durable Task Data Contributor**. Click**Next**.On the

**Members**tab, for**Assign access to**, select**Managed identity**.For

**Members**, click**+ Select members**.In the

**Select managed identities**pane, expand the**Managed identity**drop-down and select**User-assigned managed identity**.Pick the user-managed identity previously created and click the

**Select**button.Click

**Review + assign**to finish assigning the role.

## Assign managed identity to your app

Now that the identity has the required RBAC to access Durable Task Scheduler, you need to assign it to your app.

Get resource ID of manage identity.

`resource_id=$(az resource show --resource-group RESOURCE_GROUP --name MANAGED_IDENTITY_NAME --resource-type Microsoft.ManagedIdentity/userAssignedIdentities --query id --output tsv)`

Assign the identity to app.

`az functionapp identity assign --resource-group RESOURCE_GROUP_NAME --name FUNCTION_APP_NAME --identities "$resource_id"`


From your app in the portal, select

**Settings**>**Identity**.Click the

**User assigned**tab.Click

**+ Add**, then pick the identity created in the last section. Click the**Add**button.

## Add environment variables to app

Add these two environment variables to app setting:

`TASKHUB_NAME`

: name of task hub`DURABLE_TASK_SCHEDULER_CONNECTION_STRING`

: the format of the string is`"Endpoint={scheduler point};Authentication=ManagedIdentity;ClientID={client id}"`

, where`Endpoint`

is the scheduler endpoint and`client id`

is the identity's client ID.

Get the required information for the Durable Task Scheduler connection string.

To get the scheduler endpoint.

`az durabletask scheduler show --resource-group RESOURCE_GROUP_NAME --name DTS_NAME --query 'properties.endpoint' --output tsv`

To get the client ID of managed identity.

`az identity show --name MANAGED_IDENTITY_NAME --resource-group RESOURCE_GROUP_NAME --query 'clientId' --output tsv`

Use the following command to add environment variable for the scheduler connection string to app.

`az functionapp config appsettings set --resource-group RESOURCE_GROUP_NAME --name FUNCTION_APP_NAME --settings KEY_NAME=KEY_VALUE`

Repeat previous step to add environment variable for task hub name.


Get the required information for the Durable Task Scheduler connection string.

To get your scheduler endpoint, navigate to the

**Overview**tab of your scheduler resource and find "Endpoint" in the top*Essentials*section.To get your managed identity client ID, navigate to the

**Overview**tab of your resource and find "Client ID" in the top*Essentials*section.Navigate to your app on the portal.

In the left menu, click

**Settings**>**Environment variables**.Add environment variable for Durable Task Scheduler connection string.

Add environment variable for task hub name.

Click

**Apply**then**Confirm**to add the variables.

Note

If you use system-assigned identity, your connection string would *not* need the client ID of the identity resource: `"Endpoint={scheduler endpoint};Authentication=ManagedIdentity"`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/durable-task-scheduler-auto-purge -->

# Set autopurge retention policies for Azure Functions Durable Task Scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To prevent reaching the memory limit of a capacity unit (CU), it's best practice to periodically purge orchestration history data. The Durable Task Scheduler offers a lightweight, configurable autopurge feature that helps you manage orchestration data clean-up without manual intervention.

Autopurge operates asynchronously in the background, optimized to minimize system resource usage and prevent interference with other Durable Task operations. Although autopurge doesn't adhere to a strict schedule, its clean-up rate generally aligns with your orchestration scheduling rate.

## How it works

Autopurge is an opt-in feature. You can enable it by defining retention policies that control how long to keep the data of orchestrations in certain statuses. The autopurge feature purges orchestration data associated with terminal statuses. "Terminal" refers to orchestrations that have reached a final state with no further scheduling, event processing, or work item generation. Terminal statuses include:

`Completed`

`Failed`

`Canceled`

`Terminated`


The orchestration instances eligible for autopurge match those targeted by [the Durable SDK PurgeInstancesAsync API](/en-us/dotnet/api/microsoft.durabletask.client.durabletaskclientextensions.purgeinstancesasync?view=durabletask-dotnet-1.x&preserve-view=true).

Autopurge ignores orchestration data associated with non-terminal statuses. "Non-terminal" statuses indicate that the orchestration instance is either actively executing, paused, or in a state where it may resume in the future (waiting for external events or timers). These orchestrations that are continuing as new, where the current *execution* is completed, but a new instance has been started as a continuation.

These statuses include:

`Pending`

`Running`

`Suspended`

`Continued_As_New`


[Once enabled,](#enable-autopurge) autopurge periodically deletes orchestration data older than the retention period you set. Autopurge only

Note

Retention policies you define are applied to **all** task hubs in a scheduler.

### Policy value

Retention value can range from 0 (purge as soon as possible) to the maximum integer value, with the unit being **days**.


Default and Maximum Retention

By default, autopurge retention is set to30 days. This value ensures a balanced approach to data cleanup and resource efficiency.

You can extend the retention period up to amaximum of 90 days, allowing flexibility for scenarios that require longer orchestration history retention.

The retention period refers to the time period since the orchestration entered terminal state. For example, you set a retention value of 1 day. If the orchestration takes 10 days to finish, autopurge won't delete it until the following day. Autopurge isn't triggered until the orchestration finishes.

Although retention periods have no maximum limit, we recommend you avoid retaining large volumes of stale orchestration data for extended periods. This practice ensures efficient use of storage resources and maintains optimal app performance.

### Types of policies

When configuring an autopurge retention policy, you can set either a *specific* or a *default* policy.

**Default policy**purges orchestration data*regardless*of`orchestrationState`

. The following policy purges orchestration data of all statuses covered by the feature after 2 days:`{ "retentionPeriodInDays": 2 }`

**Specific policy**defines purging of orchestration data for specific`orchestrationState`

. The following policy tells Durable Task Scheduler to keep*completed*orchestration data for 1 day, after which this data is purged.`{ "retentionPeriodInDays": 1, "orchestrationState": "Completed" }`


Add specific policies to override the default policy applied to orchestrations. In the following example, the second and third policies override the default policy (`"retentionPeriodInDays": 1`

).

Data associated with

`completed`

orchestrations is deleted as soon as possible.Data associated with

`failed`

orchestrations is purged after 60 days.`[ { "retentionPeriodInDays": 1 }, { "retentionPeriodInDays": 0, "orchestrationState": "Completed" }, { "retentionPeriodInDays": 60, "orchestrationState": "Failed" } ]`


Since no specific policy is set for `canceled`

or `terminated`

orchestrations, the default policy still applies to them, purging their data after 1 day.

[For more information, see the API reference spec for Durable Task Scheduler retention policies.](/en-us/rest/api/durabletask/retention-policies/create-or-replace?view=rest-durabletask-2025-04-01-preview&preserve-view=true)

## Enable autopurge

You can define retention policies using:

- Durable Task CLI
- Azure Resource Manager (ARM)
- Bicep

Make sure you have the latest version of the Durable Task CLI extension.

```
az extension add --name durabletask
az extension update --name durabletask
```


Create or update the retention policy by running the following command.

```
az durabletask retention-policy create --scheduler-name SCHEDULER_NAME --resource-group RESOURCE_GROUP --default-days 1 --completed-days 0 --failed-days 60
```


The following properties specify the retention duration for orchestration data of different statuses.

| Property | Description |
|---|---|
`--canceled-days` or `-x` |
The number of days to retain canceled orchestrations. |
`--completed-days` or `-c` |
The number of days to retain completed orchestrations. |
`--default-days` or `-d` |
The number of days to retain orchestrations. |
`--failed-days` or `-f` |
The number of days to retain failed orchestrations. |
`--terminated-days` or `-t` |
The number of days to retain terminated orchestrations. |

**Example response**

If creation is successful, you receive the following response.

```
{
"id": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RESOURCE_GROUP/providers/Microsoft.DurableTask/schedulers/SCHEDULER_NAMER/retentionPolicies/default",
"name": "default",
"properties": {
"provisioningState": "Succeeded",
"retentionPolicies": [
{
"retentionPeriodInDays": 1
},
{
"orchestrationState": "Completed",
"retentionPeriodInDays": 0
},
{
"orchestrationState": "Failed",
"retentionPeriodInDays": 60
}
]
},
"resourceGroup": "RESOURCE_GROUP",
"systemData": {
"createdAt": "2025-04-23T23:41:17.3165122Z",
"createdBy": "someone@microsoft.com",
"createdByType": "User",
"lastModifiedAt": "2025-04-23T23:41:17.3165122Z",
"lastModifiedBy": "someone@microsoft.com",
"lastModifiedByType": "User"
},
"type": "microsoft.durabletask/schedulers/retentionpolicies"
}
```


Tip

Learn more about the retention policy command via [the CLI reference](/en-us/cli/azure/durabletask/retention-policy?view=azure-cli-latest&preserve-view=true).

## Disable autopurge

Delete the retention policies using the following command. The Durable Task Scheduler stops cleaning orchestration data within 5 to 10 minutes.

```
az durabletask retention-policy delete --scheduler-name SCHEDULER_NAME --resource-group RESOURCE_GROUP
```


## Next steps

Monitor and manage your orchestration status and history using [the Durable Task Scheduler dashboard](durable-task-scheduler-dashboard).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/durable-task-scheduler-auto-scaling -->

# Configure autoscaling for Durable Task SDK app hosted in Azure Container Apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can implement autoscaling in container apps that use the Durable Task Scheduler. Autoscaling maintains the reliability and scalability of long-running workflows by adapting to changing demands without manual intervention.

Control autoscaling by setting the range of application replicas deployed in response to an orchestration, activity, or entity being triggered. The scaler dynamically adjusts the number of container app replicas within that range, allowing your solution to handle spikes in the workload and prevent resource exhaustion.

Note

Autoscaling is supported for apps built using the Durable Task SDKs and hosted in Azure Container Apps.

## Configure the autoscaler

You can set the autoscaler configuration via the Azure portal, a Bicep template, and the Azure CLI.


| Field | Description | Example |
|---|---|---|
| Min replicas | Minimum number of replicas allowed for the container revision at any given time. | 1 |
| Max replicas | Maximum number of replicas allowed for the container revision at any given time. | 10 |
| endpoint | The Durable Task Scheduler endpoint that the scaler connects to. | `https://dts-ID.centralus.durabletask.io` |
| maxConcurrentWorkItemsCount | The maximum concurrent work items dispatched as an event to your compute, such as telling your compute to run an orchestration. | 1 |
| taskhubName | The name of the task hub connected to the scheduler. | taskhub-ID |
| workItemType | The work item type that is being dispatched. Options include Orchestration, Activity, or Entity. | Orchestration |
| Managed identity | The user assigned or system assigned managed identity linked to the scheduler and task hub resource. Ensure the Authenticate with a Managed Identity checkbox is selected. |
someone@example.com |

## Experiment with the sample

In the [Autoscaling in Azure Container Apps sample](https://github.com/Azure-Samples/Durable-Task-Scheduler/tree/main/samples/scenarios/AutoscalingInACA), you use the Azure Developer CLI to implement autoscaling for a container app built with the .NET Durable Task SDK and hosted in Azure Container Apps. The sample showcases an orchestration using the function chaining pattern.

Note

Although this sample uses the Durable Task .NET SDK, autoscaling is language-agnostic.

### Prerequisites

[.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)or later[Docker](https://www.docker.com/products/docker-desktop/)(for building the image)[Azure Developer CLI](/en-us/azure/developer/azure-developer-cli/install-azd)

### Set up your environment

Clone the

`Azure-Samples/Durable-Task-Scheduler`

directory.`git clone https://github.com/Azure-Samples/Durable-Task-Scheduler.git`

Authenticate with Azure using the Azure Developer CLI.

`azd auth login`


### Deploy the solution using Azure Developer CLI

Navigate into the

`AutoscalingInACA`

sample directory.`cd /path/to/Durable-Task-Scheduler/samples/scenarios/AutoscalingInACA`

Provision resources and deploy the application:

`azd up`

When prompted in the terminal, provide the following parameters.

Parameter Description Environment Name Prefix for the resource group created to hold all Azure resources. Azure Location The Azure location for your resources. Azure Subscription The Azure subscription for your resources. This process may take some time to complete. As the

`azd up`

command completes, the CLI output displays two Azure portal links to monitor the deployment progress. The output also demonstrates how`azd up`

:- Creates and configures all necessary Azure resources via the provided Bicep files in the
`./infra`

directory using`azd provision`

. Once provisioned by Azure Developer CLI, you can access these resources via the Azure portal. The files that provision the Azure resources include:`main.parameters.json`

`main.bicep`

- An
`app`

resources directory organized by functionality - A
`core`

reference library that contains the Bicep modules used by the`azd`

template

- Deploys the code using
`azd deploy`


**Expected output**`Packaging services (azd package) (✓) Done: Packaging service client - Image Hash: {IMAGE_HASH} - Target Image: {TARGET_IMAGE} (✓) Done: Packaging service worker - Image Hash: {IMAGE_HASH} - Target Image: {TARGET_IMAGE} Provisioning Azure resources (azd provision) Provisioning Azure resources can take some time. Subscription: SUBSCRIPTION_NAME (SUBSCRIPTION_ID) Location: West US 2 You can view detailed progress in the Azure Portal: https://portal.azure.com/#view/HubsExtension/DeploymentDetailsBlade/~/overview/id/%2Fsubscriptions%SUBSCRIPTION_ID%2Fproviders%2FMicrosoft.Resources%2Fdeployments%2FCONTAINER_APP_ENVIRONMENT (✓) Done: Resource group: GENERATED_RESOURCE_GROUP (1.385s) (✓) Done: Virtual Network: VNET_ID (862ms) (✓) Done: Container Apps Environment: GENERATED_CONTAINER_APP_ENVIRONMENT (54.125s) (✓) Done: Container Registry: GENERATED_REGISTRY (1m27.747s) (✓) Done: Container App: SAMPLE_CLIENT_APP (21.39s) (✓) Done: Container App: SAMPLE_WORKER_APP (24.136s) Deploying services (azd deploy) (✓) Done: Deploying service client - Endpoint: https://SAMPLE_CLIENT_APP.westus2.azurecontainerapps.io/ (✓) Done: Deploying service worker - Endpoint: https://SAMPLE_WORKER_APP.westus2.azurecontainerapps.io/ SUCCESS: Your up workflow to provision and deploy to Azure completed in 10 minutes 34 seconds.`

- Creates and configures all necessary Azure resources via the provided Bicep files in the

### Confirm successful deployment

In the Azure portal, verify the orchestrations are running successfully.

Copy the resource group name from the terminal output.

Sign in to the

[Azure portal](https://portal.azure.com)and search for that resource group name.From the resource group overview page, click on the client container app resource.

Select

**Monitoring**>**Log stream**.Confirm the client container is logging the function chaining tasks.

Navigate back to the resource group page to select the

`worker`

container.Select

**Monitoring**>**Log stream**.Confirm the worker container is logging the function chaining tasks.


### Understanding the custom scaler

This sample includes an `azure.yaml`

configuration file. When you ran `azd up`

, you deployed the entire sample solution to Azure, including a custom scaler for your container apps that automatically scales based on the Durable Task Scheduler's workload.

The custom scaler:

- Monitors the number of pending orchestrations in the task hub.
- Scales the number of worker replicas up with increased workload.
- Scales back down when the load decreases.
- Provides efficient resource utilization by matching capacity to demand.

### Confirm the scaler is configured

Verify the autoscaling is functioning correctly in the deployed solution.

In the Azure portal, navigate to your worker app.

From the left side menu, click

**Application**>**Revisions and replicas**.Click the

**Replicas**tab to verify your application is scaling out.From the left side menu, click

**Application**>**Scale**.Click the scale name to view the scaler settings.


## Next steps

Currently, autoscaling container apps using Durable Functions for Durable Task Scheduler isn't available. In the meantime, [try autoscaling container apps using the Microsoft SQL (MSSQL) backend](../durable-functions-mssql-container-apps-hosting).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/choose-orchestration-framework -->

# Choosing an orchestration framework

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn:

- The benefits of using an orchestration framework.
- Which framework works best for your scenario.

Azure offers two developer-oriented orchestration frameworks you can use to build apps: **Durable Functions** for apps hosted in Azure Functions, and **Durable Task SDKs** for apps hosted on other compute platforms. Orchestrations, also called *workflows*, involve arranging and coordinating multiple (long-running) tasks or processes, often involving multiple systems, to be executed in a certain order. It's important that an orchestration framework guarantees *durable execution*, meaning when there are interruptions or infrastructure failures, execution can continue in another process or machine from the point of failure. The Durable Task SDKs and Durable Functions ensure that orchestrations are executed durably through built-in state persistence and automatic retries, so that you can author orchestrations without the burden of architecting for fault tolerance.

## Scenarios requiring orchestration

The following are scenarios requiring common orchestration patterns that benefit from the Durable Task SDKs and Durable Functions:

**Function chaining:**For scenarios involving sequential steps, where each step may depend on the output of the previous one.**Fan-out/fan-in:**For batch jobs, ETL (extract, transfer, and load), and any scenario that requires parallel processing.**Human interactions:**For two-factor authentication, workflows requiring human intervention.**Asynchronous HTTP APIs:**For any scenario where a client doesn't want to wait for long-running tasks to complete.

The two following scenarios share the *function chaining* pattern.

### Processing orders on an e-commerce website

Let's say you create an e-commerce website. Your website likely needs an order processing workflow for any customer purchase. The workflow may include the following sequential steps:

- Check the inventory
- Process payment
- Update the inventory
- Generate invoice
- Send order confirmation

### Invoking AI agents for planning a trip

In this scenario, let's say you need to create an intelligent trip planner. There's a series of known steps the planner should go through:

- Suggest ideas based on user requirements
- Get preference confirmation
- Make required bookings

You can implement an AI agent for each task, and then write an orchestration that invokes these agents in certain order.

## Orchestration framework options

Both Durable Functions and Durable Task SDK are available in multiple languages but there are some differences in how they can be used.

Knowing which orchestration framework is recommended for production can help you decide which works best for your project. While the Durable Task backend is fully managed and supported, the Durable Functions extension and Durable Task SDKs vary in stability depending on [the pricing model](durable-task-scheduler-dedicated-sku) and the language SDK you use.

The following table shows what client experience is fit for production use.

| Experience | Dedicated SKU | Consumption SKU |
|---|---|---|
| Durable Functions extension in all languages | Generally available | Preview |
| Durable Task .NET SDK | Generally available | Preview |
| Durable Task Python SDK | Generally available | Preview |
| Durable Task Java SDK | Preview | Preview |

### Durable Functions

As a feature of Azure Functions, [Durable Functions](../durable-functions-overview) inherits numerous assets, such as:

- Integrations with other Azure services through the Functions extensions
- Local development experience
- Serverless pricing model
- Hosting in Azure App Service and Azure Container Apps

Durable Functions persists states in a [storage backend](../durable-functions-storage-providers) and supports:

- Two "bring-your-own" (BYO) backends:
- Azure Storage
- Microsoft SQL

- An Azure managed backend:

#### When to use Durable Functions

Consider using Durable Functions if you need to build event-driven apps with workflows. The Azure Functions extensions provide integrations with other Azure services, which make building event-driven scenarios easy. For example, with Durable Functions:

- You can easily start an orchestration when a message comes into your Azure Service Bus or a file uploads to Azure Blob Storage.
- You can easily build an orchestration that runs periodically or in response to an HTTP request with the Azure Functions timer and HTTP trigger, respectively.

Another reason to consider Durable Functions is if you're already writing Azure Function apps and realized that you need workflow. Since Durable Functions programming model is similar to Function's, you can accelerate your development.

#### Try it out

Walk through one of the following quickstarts or samples to learn more about Durable Functions.

##### Quickstarts

| Quickstart | Description | |
|---|---|---|
Durable Task Scheduler |
|

**Azure Storage**-

[.NET](../durable-functions-isolated-create-first-csharp)-

[Python](../quickstart-python-vscode)-

[JavaScript/TypeScript](../quickstart-js-vscode)-

[Java](../quickstart-java)-

[PowerShell](../quickstart-powershell-vscode)**MSSQL**[Create a Durable Functions app with MSSQL](../quickstart-mssql)##### Samples

| Sample | Description | |
|---|---|---|
Order processing workflow |
Create an order processing workflow with Durable Functions: -
-
|
This sample implements an order processing workflow that includes checking inventory, processing payment, updating inventory, and notifying customer. |
Intelligent PDF summarizer |
Create an app that processes PDFs with Durable Functions: -
-
|
This sample demonstrates using Durable Functions to coordinate the steps for processing and summarizing PDFs using Azure Cognitive Services and Azure OpenAI. |

### Durable Task SDKs with Durable Task Scheduler

The Durable Task SDKs are client SDKs that must be used with the Durable Task Scheduler. The Durable Task SDKs connect the orchestrations you write to the Durable Task Scheduler orchestration engine in Azure. Apps that use the Durable Task SDKs can be run on any compute platform, including:

- Azure Kubernetes Service
- Azure Container Apps
- Azure App Service
- Virtual Machines (VMs) on-premises

The [Durable Task Scheduler](durable-task-scheduler) (Java SDK currently in preview) plays the role of both the orchestration engine and the storage backend for orchestration state persistence. The Durable Task Scheduler:

- Is fully managed by Azure, thus removing management overhead
- Provides high orchestration throughput
- Offers an out-of-the-box dashboard for orchestration monitoring and debugging
- Includes a local emulator

#### When to use Durable Task SDKs

If you don't want to use the Azure Functions programming model, the Durable Task SDKs provide a lightweight and relatively unopinionated programming model for authoring workflows.

When you need to run apps on Azure Kubernetes Services or VMs on-premises with official Microsoft support, you should consider using the Durable Task SDKs. While Durable Functions can be run on these platforms as well, there's no official support.

#### Try it out

Walk through one of the following quickstarts to configure your applications to use the Durable Task Scheduler with the Durable Task SDKs.

| Quickstart | Description | |
|---|---|---|
Local development quickstart |
|

**Hosting in Azure Container Apps**[Deploy a Durable Task SDK app to Azure Container Apps](quickstart-container-apps-durable-task-sdk)Note

The Durable Task Framework (DTFx) is an open-source .NET orchestration framework similar to the .NET Durable Task SDK. While it *can* be used to build apps that run on platforms like Azure Kubernetes Services, **DTFx doesn't receive official Microsoft support**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/durable-task-scheduler -->

# Azure Functions Durable Task Scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Durable Task Scheduler provides durable execution in Azure. Durable execution is a fault-tolerant approach to running code that handles failures and interruptions through automatic retries and state persistence. Durable execution helps with scenarios such as:

- Distributed transactions
- Multi-agent orchestration
- Data processing
- Infrastructure management, and others.

You can use the Durable Task Scheduler with [any of the Functions SKUs](../../functions-scale), the [Dedicated SKU](durable-task-scheduler-dedicated-sku#dedicated-sku), or the [Consumption SKU (preview)](durable-task-scheduler-dedicated-sku#consumption-sku-preview).

## Supported regions

You can run the following command to get a list of available regions for Durable Task Scheduler.

```
az provider show --namespace Microsoft.DurableTask --query "resourceTypes[?resourceType=='schedulers'].locations | [0]" --out table
```


Consider using the same region for your Durable Functions app and the Durable Task Scheduler resources to optimize performance and certain network-related functionality.

## Orchestration frameworks

Azure provides two developer-oriented orchestration frameworks you can use to build stateful apps that run on any compute environment, without the need to architect for fault tolerance. You can use the Durable Task Scheduler with the following orchestration frameworks:

- Durable Functions
- Durable Task SDKs

[Learn which orchestration works better for your project.](choose-orchestration-framework)

## Architecture

For all Durable Task Scheduler orchestration frameworks, you can create scheduler instances of type [Microsoft.DurableTask/scheduler](/en-us/azure/templates/microsoft.durabletask/schedulers) using Azure Resource Manager. Each *scheduler* resource internally has its own dedicated compute and memory resources optimized for:

- Dispatching orchestrator, activity, and entity work items
- Storing and querying history at scale with minimal latency
- Providing a rich monitoring experience through
[the Durable Task Scheduler dashboard](durable-task-scheduler-dashboard)

Unlike [the BYO storage providers](../durable-functions-storage-providers), the Durable Task Scheduler provider is a purpose-built backend-as-a-service optimized for the specific needs of the [Durable Task Framework](https://github.com/Azure/durabletask).

The following diagram shows the architecture of the Durable Task Scheduler backend and its interaction with connected apps.


### Operational separation

The Durable Task Scheduler runs in Azure as a separate resource from your app. This isolation is important for several reasons:

**Reduced resource consumption**

Using a managed scheduler like Durable Task Scheduler (instead of a BYO storage provider) reduces CPU and memory resource consumption caused by the overhead of managing partitions and other complex state store interactions.**Fault isolation**

Separating the scheduler from the app reduces the risk of cascading failures and improves overall reliability in your connected apps.**Independent scaling**

The scheduler resource can be scaled independently of the app for better infrastructure resource management and cost optimization. For example, multiple apps can share the same scheduler resource, which is helpful for organizations with multiple teams or projects.**Improved support experience**

The Durable Task Scheduler is a managed service, providing streamlined support and diagnostics for issues regarding the underlying infrastructure.

### App connectivity

Your apps connect to the scheduler resource via a gRPC connection, secured using TLS and authenticated by the app's identity. The endpoint address is in a format similar to `{scheduler-name}.{region}.durabletask.io`

. For example, `myscheduler-123.westus2.durabletask.io`

.

Work items are streamed from the scheduler to the app using a push model, improving end-to-end latency and removing the need for polling. Your apps can process multiple work items in parallel and send responses back to the scheduler when the corresponding orchestration, activity, or entity task is complete.

### State management

The Durable Task Scheduler manages the state of orchestrations and entities internally, without a separate storage account for state management. The internal state store is highly optimized for use with Durable Functions and the Durable Task SDKs, resulting in better durability and reliability and reduced latency.

The scheduler uses a combination of in-memory and persistent internal storage to manage state.

- The in-memory store is used for short-lived state.
- The persistent store is used for recovery and for multi-instance query operations.

## Feature highlights

When you implement one of the Durable Task Scheduler orchestration frameworks, you benefit from several key highlights.

### Durable Task Scheduler dashboard

When a scheduler resource is created, a corresponding dashboard is provided out-of-the-box. The dashboard provides an overview of all orchestrations and entity instances and allows you to:

- Quickly filter by different criteria.
- Gather data about an orchestration instance, such as status, duration, input/output, etc.
- Drill into an instance to get data about sub-orchestrations and activities.
- Perform management operations, such as pausing, terminating, or restarting an orchestration instance.

Access to the dashboard is secured by [identity and role-based access controls](durable-task-scheduler-identity).

For more information, see [Debug and manage orchestrations using the Durable Task Scheduler dashboard](durable-task-scheduler-dashboard).

### Multiple task hubs

State is durably persisted in a *task hub*. A [task hub](../durable-functions-task-hubs):

- Is a logical container for orchestration and entity instances.
- Provides a way to partition the state store.

With one scheduler instance, you can create multiple task hubs that can be used by different apps. Each task hub gets its own [monitoring dashboard](durable-task-scheduler-dashboard). To access a task hub, [the caller's identity must have the required role-based access control (RBAC) permissions](durable-task-scheduler-identity).

Creating multiple task hubs isolates different workloads that can be managed independently. For example, you can:

- Create a task hub for each environment (dev, test, prod).
- Create task hubs for different teams within your organization.
- Share the same scheduler instance across multiple apps.

Scheduler sharing is a great way to optimize cost when multiple teams have scenarios requiring orchestrations. Although you can create multiple task hubs in one scheduler instance, they share the same resources; if one task hub is heavily loaded, it might affect the performance of the other task hubs.

### Emulator for local development

The [Durable Task Scheduler emulator](quickstart-durable-task-scheduler#set-up-the-durable-task-emulator) is a lightweight version of the scheduler backend that runs locally in a Docker container. With it, you can:

- Develop and test your Durable Function app without needing to deploy it to Azure.
- Monitor and manage your orchestrations and entities just like you would in Azure.

By default, the emulator exposes a single task hub named `default`

. To expose multiple task hubs, start the emulator and specify the `DTS_TASK_HUB_NAMES`

environment variable with a comma-separated list of task hub names. For example, to enable two task hubs named `taskhub1`

and `taskhub2`

, you can run the following command:

```
docker run -d -p 8080:8080 -p 8082:8082 -e DTS_TASK_HUB_NAMES=taskhub1,taskhub2 mcr.microsoft.com/dts/dts-emulator:latest
```


Note

The emulator internally stores orchestration and entity state in local memory, so it isn't suitable for production use.

You can see all of the emulator versions available by running the following command:

```
curl -s https://mcr.microsoft.com/v2/dts/dts-emulator/tags/list
```


### Autopurge retention policies

Stale orchestration data should be purged periodically to ensure efficient storage usage. The autopurge feature for Durable Task Scheduler provides a streamlined, configurable solution to manage orchestration instance clean-up automatically. [Learn more about setting autopurge retention policies for Durable Task Scheduler.](durable-task-scheduler-auto-purge)

## Limitations and considerations

**Scheduler quota:**You can currently create up to

**five schedulers per region**per subscription.**Max payload size:**The Durable Task Scheduler has a maximum payload size restriction for the following JSON-serialized data types:

Data type Max size Orchestrator inputs and outputs 1 MB Activity inputs and outputs 1 MB External event data 1 MB Orchestration custom status 1 MB Entity state 1 MB **Feature parity:**[Extended sessions](../durable-functions-azure-storage-provider#extended-sessions)are not available in the Durable Task Scheduler backend yet.**Task hub limits:**You're limited in how many task hubs you can use depending on your billing SKU.

[When using the Dedicated SKU,](durable-task-scheduler-dedicated-sku#dedicated-sku)task hubs are limited to 25.[When using the Consumption SKU,](durable-task-scheduler-dedicated-sku#consumption-sku-preview)task hubs are limited to 5.

For more quota,

[contact support](https://github.com/Azure/azure-functions-durable-extension/issues).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/quickstart-durable-task-scheduler -->

# Quickstart: Configure a Durable Functions app to use Azure Functions Durable Task Scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Write stateful functions in a serverless environment using Durable Functions, a feature of [Azure Functions](../../functions-overview). Scenarios where Durable Functions is useful include orchestrating microservices and workflows, stateful patterns like fan-out/fan-in, and long-running tasks.

You can use the Durable Task Scheduler as a backend for your Durable Functions, to store orchestration and entity runtime state.

In this quickstart, you:

- Configure an existing Durable Functions app to use the Durable Task Scheduler.
- Set up the Durable Task emulator for local development.
- Deploy your app to Azure on the App Service plan using Visual Studio Code.
- Monitor the status of your app and task hub on the Durable Task Scheduler dashboard.

## Prerequisites

This quickstart assumes you already have an Azure Functions project on your local computer with:

- Durable functions added to your project including:
- An
[orchestrator function](../durable-functions-bindings#orchestration-trigger). - A
[client function](../durable-functions-bindings#orchestration-client)that triggers the Durable Functions app.

- An
- The project configured for local debugging.

If you don't meet these prerequisites, we recommend that you begin with one of the following quickstarts to set up a local Functions project:

You also need:

[Docker](https://docs.docker.com/engine/install/)installed to run the Durable Task Scheduler emulator.[Azurite](../../../storage/common/storage-install-azurite#install-azurite)installed.- An
[HTTP test tool](../../functions-develop-local#http-test-tools)that keeps your data secure.

## Add the Durable Task Scheduler package

Install the latest version of the [Microsoft.Azure.Functions.Worker.Extensions.DurableTask.AzureManaged](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask.AzureManaged) package by using the [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.DurableTask.AzureManaged --prerelease
```


Note

The Durable Task Scheduler extension requires **Microsoft.Azure.Functions.Worker.Extensions.DurableTask** version `1.2.2`

or higher.

In host.json, update the `extensionBundle`

property to use the preview version that contains the Durable Task Scheduler package:

```
{
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.29.0, 5.0.0)"
}
}
```


## Update host.json

Update the host.json as follows to use Durable Task Scheduler as the backend.

```
{
"extensions": {
"durableTask": {
"hubName": "%TASKHUB_NAME%",
"storageProvider": {
"type": "azureManaged",
"connectionStringName": "DURABLE_TASK_SCHEDULER_CONNECTION_STRING"
}
}
}
}
```


## Configure local.settings.json

Add connection information for local development:

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "<DEPENDENT ON YOUR PROGRAMMING LANGUAGE>",
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"DURABLE_TASK_SCHEDULER_CONNECTION_STRING": "Endpoint=http://localhost:8080;Authentication=None",
"TASKHUB_NAME": "default"
}
}
```


## Set up the Durable Task emulator

Pull the docker image containing the emulator.

`docker pull mcr.microsoft.com/dts/dts-emulator:latest`

Run the emulator.

`docker run -d -p 8080:8080 -p 8082:8082 mcr.microsoft.com/dts/dts-emulator:latest`

The following output indicates the emulator started successfully.

Make note of the ports exposed on Docker desktop. The scheduler exposes multiple ports for different purposes:

`8080`

: gRPC endpoint that allows an app to connect to the scheduler`8082`

: Endpoint for Durable Task Scheduler dashboard


## Test locally

Go to the root directory of your app and start Azurite.

`azurite start`

Run the application.

`func start`

You should see a list of the functions in your app. If you created your app following one of the Durable Functions quickstarts, you should see something similar to the following output:

Start an orchestration instance by sending an HTTP

`POST`

request to the URL endpoint using the[HTTP test tool](../../functions-develop-local#http-test-tools)you chose.Copy the URL value for

`statusQueryGetUri`

and paste it in your browser's address bar. You should see the status on the orchestration instance:`{ "name": "DurableFunctionsOrchestrationCSharp1", "instanceId": "b50f8b723f2f44149ab9fd2e3790a0e8", "runtimeStatus": "Completed", "input": null, "customStatus": null, "output": [ "Hello Tokyo!", "Hello Seattle!", "Hello London!" ], "createdTime": "2025-02-21T21:09:59Z", "lastUpdatedTime": "2025-02-21T21:10:00Z" }`

To view more details about the orchestration instance, go to

**http://localhost:8082/**access the Durable Task Scheduler dashboard.Click on the

*default*task hub to see its dashboard.

Note

Learn more about the [Durable Task Scheduler dashboard](durable-task-scheduler-dashboard).

The [Durable Task Scheduler emulator](durable-task-scheduler#emulator-for-local-development) stores orchestration data in memory, which means all data is lost when it shuts down.

Running into issues testing? [See the troubleshooting guide.](troubleshoot-durable-task-scheduler)

## Run your app in Azure

### Create required resources

Create a Durable Task Scheduler instance and Azure Functions app on Azure following the *Function app integrated creation flow*. This experience will automatically set up identity-based access and configure the required environment variables for the app to access the scheduler.

Navigate to the Function app creation blade.

In the

**Create Function App (Flex Consumption)**blade, fill in the information in the**Basics**tab.Field Description Subscription Select your Azure subscription. Resource Group Select an existing resource group or click **Create new**to create a new one.Function App name Create a unique name for your function app. Do you want to deploy code or container image? Keep the **Code**option selected.Region Select [one of the supported regions](durable-task-scheduler#limitations-and-considerations).Runtime stack Select the runtime you're using for this quickstart. Version Select your runtime stack version. Instance size Select an instance size, or use the default selection. [Learn more about instance sizes.](../../flex-consumption-plan#instance-sizes)Zone Redundancy Leave as the default **Disabled**setting.Select the

**Durable Functions**tab.Choose

**Azure managed: Durable Task Scheduler**as the backend provider for your Durable Functions.Create a scheduler resource. This action automatically creates a task hub.

Field Description Storage backend Select **Azure managed: Durable Task Scheduler**.Region Make sure the scheduler and function app regions are the same. Durable Task Scheduler Use the scheduler name offered, or click **Create new**to create a custom name.Plan Select the [pricing plan](durable-task-scheduler-dedicated-sku)that fits your project best. Check the[Choosing an orchestration framework](choose-orchestration-framework)guide to determine which plan is best for production use.Capacity units Only applicable when "Dedicated" pricing plan is selected. You can select up to 3 Capacity Units. Click

**Review + create**to review the resource creation.A user-assigned managed identity with the required role-based access control (RBAC) permission is created automatically and added to the Function app. You can find in the summary view information related to the managed identity resource, such as:

The role assigned to it (

*Durable Task Data Contributor*)The assignment scoped to the task hub level


Click

**Create**once validation passes.

Resource deployment could take around 15 to 20 minutes. Once that is finished, you can deploy your app to Azure.

### Deploy your function app to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

#### Apps on Functions Premium plan

If your app is running on the Functions Premium plan, turn on the *Runtime Scale Monitoring* setting after deployment to ensure your app autoscales based on load:

```
az resource update -g <resource_group> -n <function_app_name>/config/web --set properties.functionsRuntimeScaleMonitoringEnabled=1 --resource-type Microsoft.Web/sites
```


## Test your function app

Run the following command to get your function's URL:

```
az functionapp function list --resource-group <RESOURCE_GROUP_NAME> --name <FUNCTION_APP_NAME> --query '[].{Function:name, URL:invokeUrlTemplate}' --output json
```


### Check orchestration status

Check the status of the orchestration instance and activity details on the Durable Task Scheduler dashboard. Accessing the dashboard requires you to log in.

Note

The following instruction shows a role assignment scoped to a specific task hub. If you need access to *all* task hubs in a scheduler, perform the assignment on the scheduler level.

Navigate to the Durable Task Scheduler resource on the portal.

Click on a task hub name.

In the left menu, select

**Access control (IAM)**.Click

**Add**to add a role assignment.Search for and select

**Durable Task Data Contributor**. Click**Next**.On the

**Members**tab, for**Assign access to**, select**User, group, or service principal**.For

**Members**, click**+ Select members**.In the

**Select members**pane, search for your name or email:Pick your email and click the

**Select**button.Click

**Review + assign**to finish assigning the role.Once the role is assigned, click

**Overview**on the left menu of the task hub resource and navigate to the dashboard URL located at the top*Essentials*section.

## Clean up resources

If you no longer need the resources that you created to complete the quickstart, to avoid related costs in your Azure subscription, [delete the resource group](/en-us/azure/azure-resource-manager/management/delete-resource-group?tabs=azure-portal#delete-resource-group) and all related resources.

## Next steps

- Learn more about the
[Durable Task Scheduler dashboard](durable-task-scheduler-dashboard). [Troubleshoot any errors you may encounter](troubleshoot-durable-task-scheduler)while using Durable Task Scheduler.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/durable-task-scheduler-versioning -->

# Orchestration Versioning (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrading and downgrading orchestrations is a key consideration when working with durable orchestration systems. If an orchestration is interrupted and later resumed (for instance, during a host update), Durable Task Scheduler replays the events of the orchestration, ensuring all previous steps were executed successfully before taking the next step. This action ensures reliability, one of the core promises of the durable execution paradigm.

If an orchestration changes between deployments, the steps it takes may no longer be the same. In this case, the system throws a `NonDeterministicError`

, instead of allowing the orchestration to continue.

*Orchestration versioning* prevents problems related to nondeterminism, allowing you to work seamlessly with new (or old) orchestrations. Durable Task Scheduler has two different styles of versioning, which you can use separately or together:

Important

Currently, the Durable Task SDKs aren't available for JavaScript and PowerShell.

Important

Currently, the Durable Task SDKs aren't available for JavaScript and PowerShell.

## Client/context-based conditional versioning

In order for an orchestration to have a version, you must first set it in the client.

The .NET SDK uses the standard host builder extensions.

Note

Available in the .NET SDK (`Microsoft.DurableTask.Client.AzureManaged`

) since v1.9.0.

```
builder.Services.AddDurableTaskClient(builder =>
{
builder.UseDurableTaskScheduler(connectionString);
builder.UseDefaultVersion("1.0.0");
});
```


Note

Available in the Java SDK (`com.microsoft:durabletask-client`

) since v1.6.0.

```
public DurableTaskClient durableTaskClient(DurableTaskProperties properties) {
// Create client using Azure-managed extensions
return DurableTaskSchedulerClientExtensions.createClientBuilder(properties.getConnectionString())
.defaultVersion("1.0")
.build();
}
```


```
c = DurableTaskSchedulerClient(host_address=endpoint, secure_channel=secure_channel,
taskhub=taskhub_name, token_credential=credential,
default_version="1.0.0")
```


Once you add the version to the client, any orchestration started by this host uses the version `1.0.0`

. The version is a simple string and accepts any value. However, the SDK tries to convert it to .NET's `System.Version`

.

- If it
*can*be converted, that library is used for comparison. - If
*not,*a simple string comparison is used.

Supplying the version in the client also makes it available in the `TaskOrchestrationContext`

, meaning you can use the version in conditional statements. As long as newer orchestration versions have the appropriate version gating, both the old and new orchestration versions can run together on the same host.

**Example:**

```
[DurableTask]
class HelloCities : TaskOrchestrator<string, List<string>>
{
private readonly string[] Cities = ["Seattle", "Amsterdam", "Hyderabad", "Kuala Lumpur", "Shanghai", "Tokyo"];
public override async Task<List<string>> RunAsync(TaskOrchestrationContext context, string input)
{
List<string> results = [];
foreach (var city in Cities)
{
results.Add(await context.CallSayHelloAsync($"{city} v{context.Version}"));
if (context.CompareVersionTo("2.0.0") >= 0)
{
results.Add(await context.CallSayGoodbyeAsync($"{city} v{context.Version}"));
}
}
Console.WriteLine("HelloCities orchestration completed.");
return results;
}
}
```


Once you add the version to the client, any orchestration started by this client uses the version `1.0.0`

. The version is a simple string and accepts any value.

Supplying the version in the client also makes it available in `TaskOrchestration`

, meaning you can use the version in conditional statements. As long as newer orchestration versions have the appropriate version gating, both the old and new orchestration versions can run together on the same client.

**Example:**

```
public TaskOrchestration create() {
return ctx -> {
List<String> results = new ArrayList<>();
for (String city : new String[]{ "Seattle", "Amsterdam", "Hyderabad", "Kuala Lumpur", "Shanghai", "Tokyo" }) {
results.add(ctx.callActivity("SayHello", city, String.class).await());
if (VersionUtils.compareVersions(ctx.getVersion(), "2.0.0") >= 0) {
// Simulate a delay for newer versions
results.add(ctx.callActivity("SayGoodbye", city, String.class).await());
}
}
ctx.complete(results);
};
}
```


Once you add the version to the client, any orchestration started by this client uses the version `1.0.0`

. The version is a simple string parsed using `packaging.version`

, which supports semantic versioning comparison and accepts any value.

Supplying the version in the client also makes it available in the `task.OrchestrationContext`

, meaning you can use the version in conditional statements. As long as newer orchestration versions have the appropriate version gating, both the old and new orchestration versions can run together on the same client.

**Example:**

```
def orchestrator(ctx: task.OrchestrationContext, _):
if ctx.version == "1.0.0":
# For version 1.0.0, we use the original logic
result: int = yield ctx.call_activity(activity_v1, input="input for v1")
elif ctx.version == "2.0.0":
# For version 2.0.0, we use the updated logic
result: int = yield ctx.call_activity(activity_v2, input="input for v2")
else:
raise ValueError(f"Unsupported version: {ctx.version}")
return {
'result': result,
}
```


In this example, we added a `SayGoodbye`

activity to the `HelloCities`

orchestration. This activity is only called for orchestration versions `2.0.0`

and higher. With the simple conditional statement, any orchestration with a version less than `2.0.0`

continues to function and any new orchestration includes the new activity.

### When to use client versioning

While client versioning provides the simplest mechanism for versioning orchestrations, interacting with the version can be programming intensive. Use client versioning if:

- You want a standard version across all versions, or
- You require custom logic around specific versions.

## Worker-based versioning

While orchestrations still need a client version to set the version, the worker-based versioning method helps you avoid conditionals in your orchestrations. The *worker* chooses how to act on different versions of orchestrations before they start executing.

Worker versioning requires the following fields to be set:

The version of the worker.

The default version applied to suborchestrations started by the worker.

The strategy that the worker uses to match against the orchestration's version.

Name Description None The version isn't considered when work is being processed Strict The version in the orchestration and the worker must match exactly CurrentOrOlder The version in the orchestration must be equal to or less than the version in the worker The strategy that the worker takes if the version doesn't meet the matching strategy.

Name Description Reject The orchestration is rejected by the worker but remains in the work queue to be attempted again later Fail The orchestration is failed and removed from the work queue

Similar to the client versioning, you can set these fields via the standard host builder pattern.

Note

Available in the .NET SDK (Microsoft.DurableTask.Worker.AzureManaged) since v1.9.0.

```
builder.Services.AddDurableTaskWorker(builder =>
{
builder.AddTasks(r => r.AddAllGeneratedTasks());
builder.UseDurableTaskScheduler(connectionString);
builder.UseVersioning(new DurableTaskWorkerOptions.VersioningOptions
{
Version = "1.0.0",
DefaultVersion = "1.0.0",
MatchStrategy = DurableTaskWorkerOptions.VersionMatchStrategy.Strict,
FailureStrategy = DurableTaskWorkerOptions.VersionFailureStrategy.Reject,
});
});
```


Note

Available in the Java SDK (com.microsoft:durabletask-client) since v1.6.0.

```
private static DurableTaskGrpcWorker createTaskHubServer() {
DurableTaskGrpcWorkerBuilder builder = new DurableTaskGrpcWorkerBuilder();
builder.useVersioning(new DurableTaskGrpcWorkerVersioningOptions(
"1.0",
"1.0",
DurableTaskGrpcWorkerVersioningOptions.VersionMatchStrategy.CURRENTOROLDER,
DurableTaskGrpcWorkerVersioningOptions.VersionFailureStrategy.REJECT));
// Orchestrations can be defined inline as anonymous classes or as concrete classes
builder.addOrchestration(new TaskOrchestrationFactory() {
@Override
public String getName() { return "HelloCities"; }
@Override
public TaskOrchestration create() {
return ctx -> {
List<String> results = new ArrayList<>();
for (String city : new String[]{ "Seattle", "Amsterdam", "Hyderabad", "Kuala Lumpur", "Shanghai", "Tokyo" }) {
results.add(ctx.callActivity("SayHello", city, String.class).await());
}
ctx.complete(results);
};
}
});
// Activities can be defined inline as anonymous classes or as concrete classes
builder.addActivity(new TaskActivityFactory() {
@Override
public String getName() { return "SayHello"; }
@Override
public TaskActivity create() {
return ctx -> {
String input = ctx.getInput(String.class);
return "Hello, " + input + "!";
};
}
});
return builder.build();
}
```


```
with DurableTaskSchedulerWorker(host_address=endpoint, secure_channel=secure_channel,
taskhub=taskhub_name, token_credential=credential) as w:
# This worker is versioned for v2, as the orchestrator code has already been updated
# CURRENT_OR_OLDER allows this worker to process orchestrations versioned below 2.0.0 - e.g. 1.0.0
w.use_versioning(worker.VersioningOptions(
version="2.0.0",
default_version="2.0.0",
match_strategy=worker.VersionMatchStrategy.CURRENT_OR_OLDER,
failure_strategy=worker.VersionFailureStrategy.FAIL
))
w.add_orchestrator(orchestrator)
w.add_activity(activity_v1)
w.add_activity(activity_v2)
w.start()
```


### Failure strategies

**Reject**

Use the `Reject`

failure strategy when the desired behavior is for the orchestration to retry at a later time or on a different worker. During the `Reject`

failure:

- An orchestration is rejected and returned to the work queue.
- An orchestration is dequeued.
- The dequeued orchestration could land on a different worker or the same one again.

The process repeats until a worker that can handle the orchestration is available. This strategy seamlessly handles deployments in which an orchestration is updated. As the deployment progresses, workers that can't handle the orchestration reject it, while workers that can handle it process it.

The ability to have mixed workers and orchestration versions allows for scenarios like blue-green deployments.

**Fail**

Use the `Fail`

failure strategy when no other versions are expected. In this case, the new version is an anomaly and no worker should even attempt to work on it. The Durable Task Scheduler fails the orchestration, putting it in a terminal state.

### When to Use Worker Versioning

Use worker versioning in scenarios where unknown or unsupported orchestration versions shouldn't be executed at all. Instead of placing version handling code in the worker, worker versioning stops the orchestration from ever executing. This method allows for simpler orchestration code. Without any code changes, various deployment scenarios can be handled, like blue-green deployments.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/quickstart-container-apps-durable-task-sdk -->

# Quickstart: Host a Durable Task SDK app on Azure Container Apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Currently, the Durable Task SDKs aren't available for JavaScript and PowerShell.

Important

Currently, the Durable Task SDKs aren't available for JavaScript and PowerShell.

In this quickstart, you learn how to:

- Set up and run the Durable Task Scheduler emulator for local development.
- Run the worker and client projects.
- Check the Azure Container Apps logs.
- Review orchestration status and history via the Durable Task Scheduler dashboard.

## Prerequisites

Before you begin:

- Make sure you have
[.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)or later. - Install
[Docker](https://www.docker.com/products/docker-desktop/)for running the emulator. - Install
[Azure Developer CLI](/en-us/azure/developer/azure-developer-cli/install-azd) - Clone the
[Durable Task Scheduler GitHub repository](https://github.com/Azure-Samples/Durable-Task-Scheduler)to use the quickstart sample.

- Make sure you have
[Python 3.9+](https://www.python.org/downloads/)or later. - Install
[Docker](https://www.docker.com/products/docker-desktop/)for running the emulator. - Install
[Azure Developer CLI](/en-us/azure/developer/azure-developer-cli/install-azd) - Clone the
[Durable Task Scheduler GitHub repository](https://github.com/Azure-Samples/Durable-Task-Scheduler)to use the quickstart sample.

- Make sure you have
[Java 8 or 11](https://www.java.com/en/download/). - Install
[Docker](https://www.docker.com/products/docker-desktop/)for running the emulator. - Install
[Azure Developer CLI](/en-us/azure/developer/azure-developer-cli/install-azd) - Clone the
[Durable Task Scheduler GitHub repository](https://github.com/Azure-Samples/Durable-Task-Scheduler)to use the quickstart sample.

## Prepare the project

In a new terminal window, from the `Azure-Samples/Durable-Task-Scheduler`

directory, navigate into the sample directory.

```
cd /samples/durable-task-sdks/dotnet/FunctionChaining
```


```
cd /samples/durable-task-sdks/python/function-chaining
```


```
cd /samples/durable-task-sdks/java/function-chaining
```


## Deploy using Azure Developer CLI

Run

`azd up`

to provision the infrastructure and deploy the application to Azure Container Apps in a single command.`azd up`

When prompted in the terminal, provide the following parameters.

Parameter Description Environment Name Prefix for the resource group created to hold all Azure resources. Azure Location The Azure location for your resources. Azure Subscription The Azure subscription for your resources. This process may take some time to complete. As the

`azd up`

command completes, the CLI output displays two Azure portal links to monitor the deployment progress. The output also demonstrates how`azd up`

:- Creates and configures all necessary Azure resources via the provided Bicep files in the
`./infra`

directory using`azd provision`

. Once provisioned by Azure Developer CLI, you can access these resources via the Azure portal. The files that provision the Azure resources include:`main.parameters.json`

`main.bicep`

- An
`app`

resources directory organized by functionality - A
`core`

reference library that contains the Bicep modules used by the`azd`

template

- Deploys the code using
`azd deploy`


### Expected output

`Packaging services (azd package) (✓) Done: Packaging service client - Image Hash: {IMAGE_HASH} - Target Image: {TARGET_IMAGE} (✓) Done: Packaging service worker - Image Hash: {IMAGE_HASH} - Target Image: {TARGET_IMAGE} Provisioning Azure resources (azd provision) Provisioning Azure resources can take some time. Subscription: SUBSCRIPTION_NAME (SUBSCRIPTION_ID) Location: West US 2 You can view detailed progress in the Azure Portal: https://portal.azure.com/#view/HubsExtension/DeploymentDetailsBlade/~/overview/id/%2Fsubscriptions%SUBSCRIPTION_ID%2Fproviders%2FMicrosoft.Resources%2Fdeployments%2FCONTAINER_APP_ENVIRONMENT (✓) Done: Resource group: GENERATED_RESOURCE_GROUP (1.385s) (✓) Done: Container Apps Environment: GENERATED_CONTAINER_APP_ENVIRONMENT (54.125s) (✓) Done: Container Registry: GENERATED_REGISTRY (1m27.747s) (✓) Done: Container App: SAMPLE_CLIENT_APP (21.39s) (✓) Done: Container App: SAMPLE_WORKER_APP (24.136s) Deploying services (azd deploy) (✓) Done: Deploying service client - Endpoint: https://SAMPLE_CLIENT_APP.westus2.azurecontainerapps.io/ (✓) Done: Deploying service worker - Endpoint: https://SAMPLE_WORKER_APP.westus2.azurecontainerapps.io/ SUCCESS: Your up workflow to provision and deploy to Azure completed in 10 minutes 34 seconds.`

- Creates and configures all necessary Azure resources via the provided Bicep files in the

## Confirm successful deployment

In the Azure portal, verify the orchestrations are running successfully.

Copy the resource group name from the terminal output.

Sign in to the

[Azure portal](https://portal.azure.com)and search for that resource group name.From the resource group overview page, click on the client container app resource.

Select

**Monitoring**>**Log stream**.

Confirm the client container is logging the function chaining tasks.

Navigate back to the resource group page to select the

`worker`

container.Select

**Monitoring**>**Log stream**.Confirm the worker container is logging the function chaining tasks.


Confirm the sample container app is logging the function chaining tasks.


## Understanding the code

### Client project

The Client project:

- Uses the same connection string logic as the worker
- Implements a sequential orchestration scheduler that:
- Schedules 20 orchestration instances, one at a time
- Waits 5 seconds between scheduling each orchestration
- Tracks all orchestration instances in a list
- Waits for all orchestrations to complete before exiting

- Uses standard logging to show progress and results

```
// Schedule 20 orchestrations sequentially
for (int i = 0; i < TotalOrchestrations; i++)
{
// Create a unique instance ID
string instanceName = $"{name}_{i+1}";
// Schedule the orchestration
string instanceId = await client.ScheduleNewOrchestrationInstanceAsync(
"GreetingOrchestration",
instanceName);
// Wait 5 seconds before scheduling the next one
await Task.Delay(TimeSpan.FromSeconds(IntervalSeconds));
}
// Wait for all orchestrations to complete
foreach (string id in allInstanceIds)
{
OrchestrationMetadata instance = await client.WaitForInstanceCompletionAsync(
id, getInputsAndOutputs: false, CancellationToken.None);
}
```


### Worker Project

The Worker project contains:

**GreetingOrchestration.cs**: Defines the orchestrator and activity functions in a single file**Program.cs**: Sets up the worker host with proper connection string handling

#### Orchestration Implementation

The orchestration directly calls each activity in sequence using the standard `CallActivityAsync`

method:

```
public override async Task<string> RunAsync(TaskOrchestrationContext context, string name)
{
// Step 1: Say hello to the person
string greeting = await context.CallActivityAsync<string>(nameof(SayHelloActivity), name);
// Step 2: Process the greeting
string processedGreeting = await context.CallActivityAsync<string>(nameof(ProcessGreetingActivity), greeting);
// Step 3: Finalize the response
string finalResponse = await context.CallActivityAsync<string>(nameof(FinalizeResponseActivity), processedGreeting);
return finalResponse;
}
```


Each activity is implemented as a separate class decorated with the `[DurableTask]`

attribute:

```
[DurableTask]
public class SayHelloActivity : TaskActivity<string, string>
{
// Implementation details
}
```


The worker uses `Microsoft.Extensions.Hosting`

for proper lifecycle management:

```
var builder = Host.CreateApplicationBuilder();
builder.Services.AddDurableTaskWorker()
.AddTasks(registry => {
registry.AddAllGeneratedTasks();
})
.UseDurableTaskScheduler(connectionString);
var host = builder.Build();
await host.StartAsync();
```


### Client

The Client project:

- Uses the same connection string logic as the worker
- Implements a sequential orchestration scheduler that:
- Schedules 20 orchestration instances, one at a time
- Waits 5 seconds between scheduling each orchestration
- Tracks all orchestration instances in a list
- Waits for all orchestrations to complete before exiting

- Uses standard logging to show progress and results

```
# Schedule all orchestrations first
instance_ids = []
for i in range(TOTAL_ORCHESTRATIONS):
try:
# Create a unique instance name
instance_name = f"{name}_{i+1}"
logger.info(f"Scheduling orchestration #{i+1} ({instance_name})")
# Schedule the orchestration
instance_id = client.schedule_new_orchestration(
"function_chaining_orchestrator",
input=instance_name
)
instance_ids.append(instance_id)
logger.info(f"Orchestration #{i+1} scheduled with ID: {instance_id}")
# Wait before scheduling next orchestration (except for the last one)
if i < TOTAL_ORCHESTRATIONS - 1:
logger.info(f"Waiting {INTERVAL_SECONDS} seconds before scheduling next orchestration...")
await asyncio.sleep(INTERVAL_SECONDS)
# ...
# Wait for all orchestrations to complete
for idx, instance_id in enumerate(instance_ids):
try:
logger.info(f"Waiting for orchestration {idx+1}/{len(instance_ids)} (ID: {instance_id})...")
result = client.wait_for_orchestration_completion(
instance_id,
timeout=120
)
```


### Worker

#### Orchestration Implementation

The orchestration directly calls each activity in sequence using the standard `call_activity`

function:

```
# Orchestrator function
def function_chaining_orchestrator(ctx, name: str) -> str:
"""Orchestrator that demonstrates function chaining pattern."""
logger.info(f"Starting function chaining orchestration for {name}")
# Call first activity - passing input directly without named parameter
greeting = yield ctx.call_activity('say_hello', input=name)
# Call second activity with the result from first activity
processed_greeting = yield ctx.call_activity('process_greeting', input=greeting)
# Call third activity with the result from second activity
final_response = yield ctx.call_activity('finalize_response', input=processed_greeting)
return final_response
```


Each activity is implemented as a separate function:

```
# Activity functions
def say_hello(ctx, name: str) -> str:
"""First activity that greets the user."""
logger.info(f"Activity say_hello called with name: {name}")
return f"Hello {name}!"
def process_greeting(ctx, greeting: str) -> str:
"""Second activity that processes the greeting."""
logger.info(f"Activity process_greeting called with greeting: {greeting}")
return f"{greeting} How are you today?"
def finalize_response(ctx, response: str) -> str:
"""Third activity that finalizes the response."""
logger.info(f"Activity finalize_response called with response: {response}")
return f"{response} I hope you're doing well!"
```


The worker uses `DurableTaskSchedulerWorker`

for proper lifecycle management:

```
with DurableTaskSchedulerWorker(
host_address=host_address,
secure_channel=endpoint != "http://localhost:8080",
taskhub=taskhub_name,
token_credential=credential
) as worker:
# Register activities and orchestrators
worker.add_activity(say_hello)
worker.add_activity(process_greeting)
worker.add_activity(finalize_response)
worker.add_orchestrator(function_chaining_orchestrator)
# Start the worker (without awaiting)
worker.start()
```


The sample container app contains both the worker and client code.

### Client

The client code:

- Uses the same connection string logic as the worker
- Implements a sequential orchestration scheduler that:
- Schedules 20 orchestration instances, one at a time
- Waits 5 seconds between scheduling each orchestration
- Tracks all orchestration instances in a list
- Waits for all orchestrations to complete before exiting

- Uses standard logging to show progress and results

```
// Create client using Azure-managed extensions
DurableTaskClient client = (credential != null
? DurableTaskSchedulerClientExtensions.createClientBuilder(endpoint, taskHubName, credential)
: DurableTaskSchedulerClientExtensions.createClientBuilder(connectionString)).build();
// Start a new instance of the registered "ActivityChaining" orchestration
String instanceId = client.scheduleNewOrchestrationInstance(
"ActivityChaining",
new NewOrchestrationInstanceOptions().setInput("Hello, world!"));
logger.info("Started new orchestration instance: {}", instanceId);
// Block until the orchestration completes. Then print the final status, which includes the output.
OrchestrationMetadata completedInstance = client.waitForInstanceCompletion(
instanceId,
Duration.ofSeconds(30),
true);
logger.info("Orchestration completed: {}", completedInstance);
logger.info("Output: {}", completedInstance.readOutputAs(String.class))
```


### Worker

The orchestration directly calls each activity in sequence using the standard `callActivity`

method:

```
DurableTaskGrpcWorker worker = (credential != null
? DurableTaskSchedulerWorkerExtensions.createWorkerBuilder(endpoint, taskHubName, credential)
: DurableTaskSchedulerWorkerExtensions.createWorkerBuilder(connectionString))
.addOrchestration(new TaskOrchestrationFactory() {
@Override
public String getName() { return "ActivityChaining"; }
@Override
public TaskOrchestration create() {
return ctx -> {
String input = ctx.getInput(String.class);
String x = ctx.callActivity("Reverse", input, String.class).await();
String y = ctx.callActivity("Capitalize", x, String.class).await();
String z = ctx.callActivity("ReplaceWhitespace", y, String.class).await();
ctx.complete(z);
};
}
})
.addActivity(new TaskActivityFactory() {
@Override
public String getName() { return "Reverse"; }
@Override
public TaskActivity create() {
return ctx -> {
String input = ctx.getInput(String.class);
StringBuilder builder = new StringBuilder(input);
builder.reverse();
return builder.toString();
};
}
})
.addActivity(new TaskActivityFactory() {
@Override
public String getName() { return "Capitalize"; }
@Override
public TaskActivity create() {
return ctx -> ctx.getInput(String.class).toUpperCase();
}
})
.addActivity(new TaskActivityFactory() {
@Override
public String getName() { return "ReplaceWhitespace"; }
@Override
public TaskActivity create() {
return ctx -> {
String input = ctx.getInput(String.class);
return input.trim().replaceAll("\\s", "-");
};
}
})
.build();
// Start the worker
worker.start();
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-task-scheduler/quickstart-portable-durable-task-sdks -->

# Quickstart: Create an app with Durable Task SDKs and Durable Task Scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Durable Task SDKs provide a lightweight client library for the Durable Task Scheduler. In this quickstart, you learn how to create orchestrations that use [the fan-out/fan-in application pattern](../durable-functions-overview#fan-in-out) to perform parallel processing.

Important

Currently, the Durable Task SDKs aren't available for JavaScript and PowerShell.

Important

Currently, the Durable Task SDKs aren't available for JavaScript and PowerShell.

- Set up and run the Durable Task Scheduler emulator for local development.
- Run the worker and client projects.
- Review orchestration status and history via the Durable Task Scheduler dashboard.

## Prerequisites

Before you begin:

- Make sure you have
[.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)or later. - Install
[Docker](https://www.docker.com/products/docker-desktop/)for running the emulator. - Clone the
[Durable Task Scheduler GitHub repository](https://github.com/Azure-Samples/Durable-Task-Scheduler)to use the quickstart sample.

- Make sure you have
[Python 3.9+](https://www.python.org/downloads/)or later. - Install
[Docker](https://www.docker.com/products/docker-desktop/)for running the emulator. - Clone the
[Durable Task Scheduler GitHub repository](https://github.com/Azure-Samples/Durable-Task-Scheduler)to use the quickstart sample.

- Make sure you have
[Java 8 or 11](https://www.java.com/en/download/). - Install
[Docker](https://www.docker.com/products/docker-desktop/)for running the emulator. - Clone the
[Durable Task Scheduler GitHub repository](https://github.com/Azure-Samples/Durable-Task-Scheduler)to use the quickstart sample.

## Set up the Durable Task Scheduler emulator

The application code looks for a deployed scheduler and task hub resource. If none is found, the code falls back to the emulator. The emulator simulates a scheduler and task hub in a Docker container, making it ideal for the local development required in this quickstart.

From the

`Azure-Samples/Durable-Task-Scheduler`

root directory, navigate to the .NET SDK sample directory.`cd samples/durable-task-sdks/dotnet/FanOutFanIn`

Pull the Docker image for the emulator.

`docker pull mcr.microsoft.com/dts/dts-emulator:latest`

Run the emulator. The container may take a few seconds to be ready.

`docker run --name dtsemulator -d -p 8080:8080 -p 8082:8082 mcr.microsoft.com/dts/dts-emulator:latest`


Since the example code automatically uses the default emulator settings, you don't need to set any environment variables. The default emulator settings for this quickstart are:

- Endpoint:
`http://localhost:8080`

- Task hub:
`default`


From the

`Azure-Samples/Durable-Task-Scheduler`

root directory, navigate to the Python SDK sample directory.`cd samples/durable-task-sdks/python/fan-out-fan-in`

Pull the Docker image for the emulator.

`docker pull mcr.microsoft.com/dts/dts-emulator:latest`

Run the emulator. The container may take a few seconds to be ready.

`docker run --name dtsemulator -d -p 8080:8080 -p 8082:8082 mcr.microsoft.com/dts/dts-emulator:latest`


Since the example code automatically uses the default emulator settings, you don't need to set any environment variables. The default emulator settings for this quickstart are:

- Endpoint:
`http://localhost:8080`

- Task hub:
`default`


From the

`Azure-Samples/Durable-Task-Scheduler`

root directory, navigate to the Java SDK sample directory.`cd samples/durable-task-sdks/java/fan-out-fan-in`

Pull the Docker image for the emulator.

`docker pull mcr.microsoft.com/dts/dts-emulator:latest`

Run the emulator. The container may take a few seconds to be ready.

`docker run --name dtsemulator -d -p 8080:8080 -p 8082:8082 mcr.microsoft.com/dts/dts-emulator:latest`


Since the example code automatically uses the default emulator settings, you don't need to set any environment variables. The default emulator settings for this quickstart are:

- Endpoint:
`http://localhost:8080`

- Task hub:
`default`


## Run the quickstart

From the

`FanOutFanIn`

directory, navigate to the`Worker`

directory to build and run the worker.`cd Worker dotnet build dotnet run`

In a separate terminal, from the

`FanOutFanIn`

directory, navigate to the`Client`

directory to build and run the client.`cd Client dotnet build dotnet run`


### Understanding the output

When you run this sample, you receive output from both the worker and client processes. [Unpack what happened in the code when you ran the project.](#understanding-the-code-structure)

#### Worker output

The worker output shows:

- Registration of the orchestrator and activities
- Log entries when each activity is called
- Parallel processing of multiple work items
- Final aggregation of results

#### Client output

The client output shows:

- The orchestration starting with a list of work items
- The unique orchestration instance ID
- The final aggregated results, showing each work item and its corresponding result
- Total count of processed items

#### Example output

```
Starting Fan-Out Fan-In Pattern - Parallel Processing Client
Using local emulator with no authentication
Starting parallel processing orchestration with 5 work items
Work items: ["Task1","Task2","Task3","LongerTask4","VeryLongTask5"]
Started orchestration with ID: 7f8e9a6b-1c2d-3e4f-5a6b-7c8d9e0f1a2b
Waiting for orchestration to complete...
Orchestration completed with status: Completed
Processing results:
Work item: Task1, Result: 5
Work item: Task2, Result: 5
Work item: Task3, Result: 5
Work item: LongerTask4, Result: 11
Work item: VeryLongTask5, Result: 13
Total items processed: 5
```


Activate a Python virtual environment.

Install the required packages.

`pip install -r requirements.txt`

Start the worker.

`python worker.py`

**Expected output**You can see output indicating that the worker started and is waiting for work items.

`Starting Fan Out/Fan In pattern worker... Using taskhub: default Using endpoint: http://localhost:8080 Starting gRPC worker that connects to http://localhost:8080 Successfully connected to http://localhost:8080. Waiting for work items...`

In a new terminal, activate the virtual environment and run the client.

You can provide the number of work items as an argument. If no argument is provided, the example runs 10 items by default.

`python client.py [number_of_items]`


### Understanding the output

When you run this sample, you receive output from both the worker and client processes. [Unpack what happened in the code when you ran the project.](#understanding-the-code-structure)

#### Worker output

The worker output shows:

- Registration of the orchestrator and activities.
- Status messages when processing each work item in parallel, showing that they're executing concurrently.
- Random delays for each work item (between 0.5 and 2 seconds) to simulate varying processing times.
- A final message showing the aggregation of results.

#### Client output

The client output shows:

- The orchestration starting with the specified number of work items.
- The unique orchestration instance ID.
- The final aggregated result, which includes:
- The total number of items processed
- The sum of all results (each item result is the square of its value)
- The average of all results


#### Example output

```
Starting fan out/fan in orchestration with 10 items
Waiting for 10 parallel tasks to complete
Orchestrator yielded with 10 task(s) and 0 event(s) outstanding.
Processing work item: 1
Processing work item: 2
Processing work item: 10
Processing work item: 9
Processing work item: 8
Processing work item: 7
Processing work item: 6
Processing work item: 5
Processing work item: 4
Processing work item: 3
Orchestrator yielded with 9 task(s) and 0 event(s) outstanding.
Orchestrator yielded with 8 task(s) and 0 event(s) outstanding.
Orchestrator yielded with 7 task(s) and 0 event(s) outstanding.
Orchestrator yielded with 6 task(s) and 0 event(s) outstanding.
Orchestrator yielded with 5 task(s) and 0 event(s) outstanding.
Orchestrator yielded with 4 task(s) and 0 event(s) outstanding.
Orchestrator yielded with 3 task(s) and 0 event(s) outstanding.
Orchestrator yielded with 2 task(s) and 0 event(s) outstanding.
Orchestrator yielded with 1 task(s) and 0 event(s) outstanding.
All parallel tasks completed, aggregating results
Orchestrator yielded with 1 task(s) and 0 event(s) outstanding.
Aggregating results from 10 items
Orchestration completed with status: COMPLETED
```


From the `fan-out-fan-in`

directory, build and run the application using Gradle.

```
./gradlew runFanOutFanInPattern
```


Tip

If you receive the error message `zsh: permission denied: ./gradlew`

, try running `chmod +x gradlew`

before running the application.

### Understanding the output

When you run this sample, you receive output that shows:

- Registration of the orchestrator and activities.
- Status messages when processing each work item in parallel, showing that they're executing concurrently.
- Random delays for each work item (between 0.5 and 2 seconds) to simulate varying processing times.
- A final message showing the aggregation of results.

[Unpack what happened in the code when you ran the project.](#understanding-the-code-structure)

#### Example output

```
Starting a Gradle Daemon (subsequent builds will be faster)
> Task :runFanOutFanInPattern
Durable Task worker is connecting to sidecar at localhost:8080.
Started new orchestration instance
Orchestration completed: [Name: 'FanOutFanIn_WordCount', ID: '<id-number>', RuntimeStatus: COMPLETED, CreatedAt: 2025-04-25T15:24:47.170Z, LastUpdatedAt: 2025-04-25T15:24:47.287Z, Input: '["Hello, world!","The quick brown fox jumps over t...', Output: '60']
Output: 60
```


Now that you ran the project locally, you can now learn how to [deploy to Azure hosted in Azure Container Apps](#next-steps).

## View orchestration status and history

You can view the orchestration status and history via the [Durable Task Scheduler dashboard](durable-task-scheduler-dashboard). By default, the dashboard runs on port 8082.

- Navigate to http://localhost:8082 in your web browser.
- Click the
**default**task hub. The orchestration instance you created is in the list. - Click the orchestration instance ID to view the execution details, which include:
- The parallel execution of multiple activity tasks
- The fan-in aggregation step
- The input and output at each step
- The time taken for each step


## Understanding the code structure

### The worker project

To demonstrate [the fan-out/fan-in pattern](../durable-functions-overview#fan-in-out), the worker project orchestration creates parallel activity tasks and waits for all to complete. The orchestrator:

- Takes a list of work items as input.
- Fans out by creating a separate task for each work item using
`ProcessWorkItemActivity`

. - Executes all tasks in parallel.
- Waits for all tasks to complete using
`Task.WhenAll`

. - Fans in by aggregating all individual results using
`AggregateResultsActivity`

. - Returns the final aggregated result to the client.

The worker project contains:

**ParallelProcessingOrchestration.cs**: Defines the orchestrator and activity functions in a single file.**Program.cs**: Sets up the worker host with proper connection string handling.

`ParallelProcessingOrchestration.cs`


Using fan-out/fan-in, the orchestration creates parallel activity tasks and waits for all to complete.

```
public override async Task<Dictionary<string, int>> RunAsync(TaskOrchestrationContext context, List<string> workItems)
{
// Step 1: Fan-out by creating a task for each work item in parallel
List<Task<Dictionary<string, int>>> processingTasks = new List<Task<Dictionary<string, int>>>();
foreach (string workItem in workItems)
{
// Create a task for each work item (fan-out)
Task<Dictionary<string, int>> task = context.CallActivityAsync<Dictionary<string, int>>(
nameof(ProcessWorkItemActivity), workItem);
processingTasks.Add(task);
}
// Step 2: Wait for all parallel tasks to complete
Dictionary<string, int>[] results = await Task.WhenAll(processingTasks);
// Step 3: Fan-in by aggregating all results
Dictionary<string, int> aggregatedResults = await context.CallActivityAsync<Dictionary<string, int>>(
nameof(AggregateResultsActivity), results);
return aggregatedResults;
}
```


Each activity is implemented as a separate class decorated with the `[DurableTask]`

attribute.

```
[DurableTask]
public class ProcessWorkItemActivity : TaskActivity<string, Dictionary<string, int>>
{
// Implementation processes a single work item
}
[DurableTask]
public class AggregateResultsActivity : TaskActivity<Dictionary<string, int>[], Dictionary<string, int>>
{
// Implementation aggregates individual results
}
```


`Program.cs`


The worker uses `Microsoft.Extensions.Hosting`

for proper lifecycle management.

```
using Microsoft.Extensions.Hosting;
//..
builder.Services.AddDurableTaskWorker()
.AddTasks(registry =>
{
registry.AddOrchestrator<ParallelProcessingOrchestration>();
registry.AddActivity<ProcessWorkItemActivity>();
registry.AddActivity<AggregateResultsActivity>();
})
.UseDurableTaskScheduler(connectionString);
```


### The client project

The client project:

- Uses the same connection string logic as the worker.
- Creates a list of work items to be processed in parallel.
- Schedules an orchestration instance with the list as input.
- Waits for the orchestration to complete and displays the aggregated results.
- Uses
`WaitForInstanceCompletionAsync`

for efficient polling.

```
List<string> workItems = new List<string>
{
"Task1",
"Task2",
"Task3",
"LongerTask4",
"VeryLongTask5"
};
// Schedule the orchestration with the work items
string instanceId = await client.ScheduleNewOrchestrationInstanceAsync(
"ParallelProcessingOrchestration",
workItems);
// Wait for completion
var instance = await client.WaitForInstanceCompletionAsync(
instanceId,
getInputsAndOutputs: true,
cts.Token);
```


`worker.py`


To demonstrate [the fan-out/fan-in pattern](../durable-functions-overview#fan-in-out), the worker project orchestration creates parallel activity tasks and waits for all to complete. The orchestrator:

- Receives a list of work items as input.
- It "fans out" by creating parallel tasks for each work item (calling
`process_work_item`

for each one). - It waits for all tasks to complete using
`task.when_all`

. - It then "fans in" by aggregating the results with the
`aggregate_results`

activity. - The final aggregated result is returned to the client.

Using fan-out/fan-in, the orchestration creates parallel activity tasks and waits for all to complete.

```
# Orchestrator function
def fan_out_fan_in_orchestrator(ctx, work_items: list) -> dict:
logger.info(f"Starting fan out/fan in orchestration with {len(work_items)} items")
# Fan out: Create a task for each work item
parallel_tasks = []
for item in work_items:
parallel_tasks.append(ctx.call_activity("process_work_item", input=item))
# Wait for all tasks to complete
logger.info(f"Waiting for {len(parallel_tasks)} parallel tasks to complete")
results = yield task.when_all(parallel_tasks)
# Fan in: Aggregate all the results
logger.info("All parallel tasks completed, aggregating results")
final_result = yield ctx.call_activity("aggregate_results", input=results)
return final_result
```


`client.py`


The client project:

- Uses the same connection string logic as the worker.
- Creates a list of work items to be processed in parallel.
- Schedules an orchestration instance with the list as input.
- Waits for the orchestration to complete and displays the aggregated results.
- Uses
`wait_for_orchestration_completion`

for efficient polling.

```
# Generate work items (default 10 items if not specified)
count = int(sys.argv[1]) if len(sys.argv) > 1 else 10
work_items = list(range(1, count + 1))
logger.info(f"Starting new fan out/fan in orchestration with {count} work items")
# Schedule a new orchestration instance
instance_id = client.schedule_new_orchestration(
"fan_out_fan_in_orchestrator",
input=work_items
)
logger.info(f"Started orchestration with ID = {instance_id}")
# Wait for orchestration to complete
logger.info("Waiting for orchestration to complete...")
result = client.wait_for_orchestration_completion(
instance_id,
timeout=60
)
```


To demonstrate [the fan-out/fan-in pattern](../durable-functions-overview#fan-in-out), the `FanOutFanInPattern`

project orchestration creates parallel activity tasks and waits for all to complete. The orchestrator:

- Takes a list of work items as input.
- Fans out by creating a separate task for each work item using ``.
- Executes all tasks in parallel.
- Waits for all tasks to complete using ``.
- Fans in by aggregating all individual results using ``.
- Returns the final aggregated result to the client.

The project contains:

: Defines the orchestrator and activity functions.`DurableTaskSchedulerWorkerExtensions`

worker: Sets up the worker host with proper connection string handling.`DurableTaskSchedulerClientExtension`

client

### Worker

Using fan-out/fan-in, the orchestration creates parallel activity tasks and waits for all to complete.

```
DurableTaskGrpcWorker worker = DurableTaskSchedulerWorkerExtensions.createWorkerBuilder(connectionString)
.addOrchestration(new TaskOrchestrationFactory() {
@Override
public String getName() { return "FanOutFanIn_WordCount"; }
@Override
public TaskOrchestration create() {
return ctx -> {
List<?> inputs = ctx.getInput(List.class);
List<Task<Integer>> tasks = inputs.stream()
.map(input -> ctx.callActivity("CountWords", input.toString(), Integer.class))
.collect(Collectors.toList());
List<Integer> allWordCountResults = ctx.allOf(tasks).await();
int totalWordCount = allWordCountResults.stream().mapToInt(Integer::intValue).sum();
ctx.complete(totalWordCount);
};
}
})
.addActivity(new TaskActivityFactory() {
@Override
public String getName() { return "CountWords"; }
@Override
public TaskActivity create() {
return ctx -> {
String input = ctx.getInput(String.class);
StringTokenizer tokenizer = new StringTokenizer(input);
return tokenizer.countTokens();
};
}
})
.build();
// Start the worker
worker.start();
```


### Client

The client project:

- Uses the same connection string logic as the worker.
- Creates a list of work items to be processed in parallel.
- Schedules an orchestration instance with the list as input.
- Waits for the orchestration to complete and displays the aggregated results.
- Uses
`waitForInstanceCompletion`

for efficient polling.

```
DurableTaskClient client = DurableTaskSchedulerClientExtensions.createClientBuilder(connectionString).build();
// The input is an arbitrary list of strings.
List<String> listOfStrings = Arrays.asList(
"Hello, world!",
"The quick brown fox jumps over the lazy dog.",
"If a tree falls in the forest and there is no one there to hear it, does it make a sound?",
"The greatest glory in living lies not in never falling, but in rising every time we fall.",
"Always remember that you are absolutely unique. Just like everyone else.");
// Schedule an orchestration which will reliably count the number of words in all the given sentences.
String instanceId = client.scheduleNewOrchestrationInstance(
"FanOutFanIn_WordCount",
new NewOrchestrationInstanceOptions().setInput(listOfStrings));
logger.info("Started new orchestration instance: {}", instanceId);
// Block until the orchestration completes. Then print the final status, which includes the output.
OrchestrationMetadata completedInstance = client.waitForInstanceCompletion(
instanceId,
Duration.ofSeconds(30),
true);
logger.info("Orchestration completed: {}", completedInstance);
logger.info("Output: {}", completedInstance.readOutputAs(int.class));
```


## Next steps

Now that you've run the sample locally using the Durable Task Scheduler emulator, try creating a scheduler and task hub resource and deploying to Azure Container Apps.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/function-app-diagnostics -->

# Azure Functions app diagnostics

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions App Diagnostics is a useful resource in the Azure portal for monitoring and diagnosing potential issues in your Durable Functions application. Not only does it help diagnose problems, but it also provides potential solutions and/or relevant documentation to help you resolve issues faster.

## How to use Azure Functions app diagnostics

Go to your Function App resource. In the left menu, select

**Diagnose and solve problems**.Search for “Durable Functions” and select on the result.

You're now inside the Durable Functions detector, which checks for common problems Durable Functions apps tend to have. The detector also gives you links to tools and documentation you might find helpful. Go through the various insights in the detector to learn about the application’s health. Some examples of what the detector tells you include the Durable Functions extension version your app is using, performance issues, and any errors or warnings. If there are issues, you'll see suggestions on how to mitigate and resolve them.


## Other useful detectors

On the left side of the window, there's a list of detectors designed to check for different problems. This section highlights a few.

The *Functions App Down or Report Errors* detector pulls results from different detectors checking key areas of your application that may be the cause of your application being down or reporting errors. The screenshot below shows the checks performed (not all 15 are captured in the screenshot) and the two issues requiring attention.


Maximizing *High CPU Analysis* shows that one app is causing high CPU usage.


The following is suggested when clicking "View Solutions". If you decide to follow the second option, you can easily restart your site by clicking the button.


Maximizing *Memory Analysis* shows the following warning and graph. (Note that there's more content not captured in the screenshot.)


The following is suggested when clicking "View Solutions". You can easily scale up by clicking a button.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-roslyn-analyzer -->

# Durable Functions Rosyln Analyzer (C# only)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Durable Functions Roslyn Analyzer is a live code analyzer that guides C# users to adhere to Durable Functions specific [code constraints](durable-functions-code-constraints). This analyzer is *enabled by default* to check your Durable Functions code and generate warnings and errors when there's any.

## .NET isolated analyzer

Find information (improvements, releases, bug fixes, etc.) about the Roslyn Analyzer for the NET isolated model on [the durabletask-dotnet release notes page](https://github.com/microsoft/durabletask-dotnet/releases).

A list of shipped analyzer rules can be found in the [analyzer release notes](https://github.com/microsoft/durabletask-dotnet/blob/main/src/Analyzers/AnalyzerReleases.Shipped.md).

Note

The .NET Isolated Roslyn Analyzer is only available starting from [Microsoft.Azure.Functions.Worker.Extensions.DurableTask v1.6.0](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask/1.6.0).

## .NET in-process analyzer

Information regarding the Roslyn Analyzer for the **in-process** model can be found on the [Analyzer v0.2.0 release page](https://github.com/Azure/azure-functions-durable-extension/releases/tag/Analyzer-v0.2.0).

The following sections provide configuration instructions for more detailed analysis when using the .NET in-process analyzer.

### Visual Studio

For the best experience, you'll want to enable full solution analysis in your Visual Studio settings. This can be done by going to **Tools** -> **Options** -> **Text Editor** -> **C#** -> **Advanced** -> **"Entire solution"**:


Depending on the version of Visual Studio, you may also see "Enable full solution analysis":


To disable the analyzer, refer to these [instructions](/en-us/visualstudio/code-quality/in-source-suppression-overview).

### Visual Studio Code

Open **Settings** by clicking the wheel icon on the lower left corner, then search for “rosyln”. “Enable Rosyln Analyzers” should show up as one of the results. Check the enable support box.

::: zone-end

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-singletons -->

# Singleton orchestrators in Durable Functions (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For background jobs, you often need to ensure that only one instance of a particular orchestrator runs at a time. You can ensure this kind of singleton behavior in [Durable Functions](durable-functions-overview) by assigning a specific instance ID to an orchestrator when creating it.

## Singleton example

The following example shows an HTTP-trigger function that creates a singleton background job orchestration. The code ensures that only one instance exists for a specified instance ID.

```
[FunctionName("HttpStartSingle")]
public static async Task<HttpResponseMessage> RunSingle(
[HttpTrigger(AuthorizationLevel.Function, methods: "post", Route = "orchestrators/{functionName}/{instanceId}")] HttpRequestMessage req,
[DurableClient] IDurableOrchestrationClient starter,
string functionName,
string instanceId,
ILogger log)
{
// Check if an instance with the specified ID already exists or an existing one stopped running(completed/failed/terminated).
var existingInstance = await starter.GetStatusAsync(instanceId);
if (existingInstance == null
|| existingInstance.RuntimeStatus == OrchestrationRuntimeStatus.Completed
|| existingInstance.RuntimeStatus == OrchestrationRuntimeStatus.Failed
|| existingInstance.RuntimeStatus == OrchestrationRuntimeStatus.Terminated)
{
// An instance with the specified ID doesn't exist or an existing one stopped running, create one.
dynamic eventData = await req.Content.ReadAsAsync<object>();
await starter.StartNewAsync(functionName, instanceId, eventData);
log.LogInformation($"Started orchestration with ID = '{instanceId}'.");
return starter.CreateCheckStatusResponse(req, instanceId);
}
else
{
// An instance with the specified ID exists or an existing one still running, don't create one.
return new HttpResponseMessage(HttpStatusCode.Conflict)
{
Content = new StringContent($"An instance with ID '{instanceId}' already exists."),
};
}
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

By default, instance IDs are randomly generated GUIDs. In the previous example, however, the instance ID is passed in route data from the URL. The code then fetches the orchestration instance metadata to check if an instance having the specified ID is already running. If no such instance is running, a new instance is created with that ID.

Note

There is a potential race condition in this sample. If two instances of **HttpStartSingle** execute concurrently, both function calls will report success, but only one orchestration instance will actually start. Depending on your requirements, this may have undesirable side effects.

The implementation details of the orchestrator function don't actually matter. It could be a regular orchestrator function that starts and completes, or it could be one that runs forever (that is, an [Eternal Orchestration](durable-functions-eternal-orchestrations)). The important point is that there is only ever one instance running at a time.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-extension-upgrade -->

# Upgrade Durable Functions extension version

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Many issues users experience with Durable Functions can be resolved simply by upgrading to the latest version of the extension, which often contains important bug fixes and performance improvements. You can follow the instructions in this article to get the latest version of the Durable Functions extension.

Changes to the extension can be found in the [Release page](https://github.com/Azure/azure-functions-durable-extension/releases) of the `Azure/azure-functions-durable-extension`

repo. You can also configure to receive notifications whenever there's a new extension release by going to the **Releases page**, clicking on **Watch**, then on **Custom**, and finally selecting the **Releases** filter:


## Reference the latest NuGet packages (.NET apps only)

.NET apps can get the latest version of the Durable Functions extension by referencing the latest NuGet package:

If you're using the Netherite or MSSQL [storage providers](durable-functions-storage-providers) (instead of Azure Storage), you need to reference one of the following:

[Netherite, in-process worker](https://www.nuget.org/packages/Microsoft.Azure.DurableTask.Netherite.AzureFunctions)[Netherite, isolated worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask.Netherite)[MSSQL, in-process worker](https://www.nuget.org/packages/Microsoft.DurableTask.SqlServer.AzureFunctions)[MSSQL, isolated worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask.SqlServer)

## Upgrade the extension bundle

[Extension bundles](../extension-bundles) provide an easy and convenient way for non-.NET function apps to reference and use various Azure Function triggers and bindings. For example, if you need to send a message to Event Hubs every time your function is triggered, you can use the Event Hubs extension to gain access to Event Hubs bindings. The Durable Functions extension is also included in each version of extension bundles. Extension bundles are automatically configured in host.json when creating a function app using any of the supported development tools.

Most non-.NET applications rely on extension bundles to gain access to various triggers and bindings. The [latest bundle release](https://github.com/Azure/azure-functions-extension-bundles) often contains the latest version of the Durable Functions extension with critical bug fixes and performance improvements. Therefore, it's important that your app uses the latest version of extension bundles. You can check your host.json file to see whether the version range you're using includes the latest extension bundle version.

## Manually upgrade the Durable Functions extension

If upgrading the extension bundle didn't resolve your problem, and you noticed a newer release of the Durable Functions extension containing a potential fix to your problem, then you could try to manually upgrade the extension itself. Note that this is only intended for advanced scenarios or when time-sensitive fixes are necessary as there are many drawbacks to manually managing extensions. For example, you may have to deal to .NET errors when the extensions you use are incompatible with each other. You also need to manually upgrade extensions to get the latest fixes and patches instead of getting them automatically through the extension bundle.

First, remove the `extensionBundle`

section from your host.json file.

Install the `dotnet`

CLI if you don't already have it. You can get it from this [page](https://www.microsoft.com/net/download/).

Because applications normally use more than one extension, it's recommended that you run the following to manually install all the latest version of all extensions supported by Extension Bundles:

```
func extensions install
```


However, if you **only** wish to install the latest Durable Functions extension release, you would run the following command:

```
func extensions install -p Microsoft.Azure.WebJobs.Extensions.DurableTask -v <version>
```


For example:

```
func extensions install -p Microsoft.Azure.WebJobs.Extensions.DurableTask -v 2.9.1
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-billing -->

# Durable Functions billing

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Durable Functions](durable-functions-overview) is billed the same way as Azure Functions. For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).

When executing orchestrator functions in Azure Functions [Consumption plan](../consumption-plan), you need to be aware of some billing behaviors. The following sections describe these behaviors and their effect in more detail.

## Orchestrator function replay billing

[Orchestrator functions](durable-functions-orchestrations) might replay several times throughout the lifetime of an orchestration. Each replay is viewed by the Azure Functions runtime as a distinct function invocation. For this reason, in the Azure Functions Consumption plan you're billed for each replay of an orchestrator function. Other plan types don't charge for orchestrator function replay.

## Awaiting and yielding in orchestrator functions

When an orchestrator function waits for an asynchronous task to complete, the runtime considers that particular function invocation to be finished. The billing for the orchestrator function stops at that point. It doesn't resume until the next orchestrator function replay. You aren't billed for any time spent awaiting or yielding in an orchestrator function.

Note

Functions calling other functions is considered by some to be a Serverless anti-pattern. This is because of a problem known as *double billing*. When a function calls another function directly, both run at the same time. The called function is actively running code while the calling function is waiting for a response. In this case, you must pay for the time the calling function spends waiting for the called function to run.

There is no double billing in orchestrator functions. An orchestrator function's billing stops while it waits for the result of an activity function or sub-orchestration.

## Durable HTTP polling

Orchestrator functions can make long-running HTTP calls to external endpoints as described in the [HTTP features article](durable-functions-http-features). The *"call HTTP"* APIs might internally poll an HTTP endpoint while following the [asynchronous 202 pattern](durable-functions-http-features#http-202-handling).

There currently isn't direct billing for internal HTTP polling operations. However, internal polling might cause the orchestrator function to periodically replay. You'll be billed standard charges for these internal function replays.

## Azure Storage transactions

Durable Functions uses Azure Storage by default to keep state persistent, process messages, and manage partitions via blob leases. Because you own this storage account, any transaction costs are billed to your Azure subscription. For more information about the Azure Storage artifacts used by Durable Functions, see the [Task hubs article](durable-functions-task-hubs).

Several factors contribute to the actual Azure Storage costs incurred by your Durable Functions app:

- A single function app is associated with a single task hub, which shares a set of Azure Storage resources. These resources are used by all durable functions in a function app. The actual number of functions in the function app has no effect on Azure Storage transaction costs.
- Each function app instance internally polls multiple queues in the storage account by using an exponential-backoff polling algorithm. An idle app instance polls the queues less often than does an active app, which results in fewer transaction costs. For more information about Durable Functions queue-polling behavior when using the Azure Storage provider, see the
[queue-polling section](durable-functions-azure-storage-provider#queue-polling)of the Azure Storage provider documentation. - When running in the Azure Functions Consumption or Premium plans, the
[Azure Functions scale controller](../event-driven-scaling)regularly polls all task-hub queues in the background. If a function app is under light to moderate scale, only a single scale controller instance will poll these queues. If the function app scales out to a large number of instances, more scale controller instances might be added. These additional scale controller instances can increase the total queue-transaction costs. - Each function app instance competes for a set of blob leases. These instances will periodically make calls to the Azure Blob service either to renew held leases or to attempt to acquire new leases. The task hub's configured partition count determines the number of blob leases. Scaling out to a larger number of function app instances likely increases the Azure Storage transaction costs associated with these lease operations.

You can find more information on Azure Storage pricing in the [Azure Storage pricing](https://azure.microsoft.com/pricing/details/storage/) documentation.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-eternal-orchestrations -->

# Eternal orchestrations in Durable Functions (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

*Eternal orchestrations* are orchestrator functions that never end. They're useful when you want to use [Durable Functions](durable-functions-overview) for aggregators and any scenario that requires an infinite loop.

## Orchestration history

As explained in the [orchestration history](durable-functions-orchestrations#orchestration-history) topic, the Durable Task Framework keeps track of the history of each function orchestration. This history grows continuously as long as the orchestrator function continues to schedule new work. If the orchestrator function goes into an infinite loop and continuously schedules work, this history could grow critically large and cause significant performance problems. The *eternal orchestration* concept was designed to mitigate these kinds of problems for applications that need infinite loops.

## Resetting and restarting

Instead of using infinite loops, orchestrator functions reset their state by calling the `continue-as-new`

method of the [orchestration trigger binding](durable-functions-bindings#orchestration-trigger). This method takes a JSON-serializable parameter, which becomes the new input for the next orchestrator function generation.

When you call `continue-as-new`

, the orchestration instance restarts itself with the new input value. The same instance ID is kept, but the orchestrator function's history is reset.

## Eternal orchestration considerations

Keep these considerations in mind when using the `continue-as-new`

method in an orchestration:

When an orchestrator function gets reset by using the

`continue-as-new`

method, the Durable Task Framework maintains the same instance ID but internally it creates and uses a new*execution ID*going forward. This execution ID isn't exposed externally, but it can be useful when debugging orchestration execution.When an unhandled exception occurs during execution, the orchestration enters a

*failed*state and execution terminates. In this state, a call to`continue-as-new`

made from the`finally`

block of a try-catch statement can't restart the orchestration.

Important

If during execution the orchestration encounters an uncaught exception, then the orchestration enters a "failed" state and execution will complete. In particular, this means that a call to *continue-as-new*, even in a `finally`

block, will *not* restart the orchestration in the case of an uncaught exception.

## Periodic work example

One use case for eternal orchestrations is code that needs to do periodic work indefinitely.

```
[FunctionName("Periodic_Cleanup_Loop")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
await context.CallActivityAsync("DoCleanup", null);
// sleep for one hour between cleanups
DateTime nextCleanup = context.CurrentUtcDateTime.AddHours(1);
await context.CreateTimer(nextCleanup, CancellationToken.None);
context.ContinueAsNew(null);
}
```


Note

The previous C# example is for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

The difference between this example and a timer-triggered function is that cleanup trigger times aren't based on a schedule. For example, a CRON schedule that executes a function every hour runs at 1:00, 2:00, 3:00, and so on, and could potentially run into overlap issues. In this example, however, if the cleanup takes 30 minutes, then it schedules at 1:00, 2:30, 4:00, and so on, and there's no chance of overlap.

## Starting an eternal orchestration

Use the *start-new* or *schedule-new* durable client method to start an eternal orchestration, just like you would any other orchestration function.

Note

If you need to ensure a singleton eternal orchestration is running, it's important to maintain the same instance `id`

when starting the orchestration. For more information, see [Instance Management](durable-functions-instance-management).

```
[FunctionName("Trigger_Eternal_Orchestration")]
public static async Task<HttpResponseMessage> OrchestrationTrigger(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = null)] HttpRequestMessage request,
[DurableClient] IDurableOrchestrationClient client)
{
string instanceId = "StaticId";
await client.StartNewAsync("Periodic_Cleanup_Loop", instanceId);
return client.CreateCheckStatusResponse(request, instanceId);
}
```


Note

The previous code is for Durable Functions 2.x. For Durable Functions 1.x, use the `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

## Exit from an eternal orchestration

If an orchestrator function needs to eventually complete, then all you need to do is *not* call `ContinueAsNew`

and let the function exit.

If an orchestrator function is in an infinite loop and needs to be stopped, use the *terminate* API of the [orchestration client binding](durable-functions-bindings#orchestration-client) to stop it. For more information, see [Instance Management](durable-functions-instance-management).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-timers -->

# Timers in Durable Functions (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Durable Functions](durable-functions-overview) provides *durable timers* for use in orchestrator functions to implement delays or to set up timeouts on async actions. Durable timers should be used in orchestrator functions instead of "sleep" or "delay" APIs that may be built into the language.

Durable timers are tasks that are created using the appropriate "create timer" API for the provided language, as shown below, and take either a due time or a duration as an argument.

```
// Put the orchestrator to sleep for 72 hours
DateTime dueTime = context.CurrentUtcDateTime.AddHours(72);
await context.CreateTimer(dueTime, CancellationToken.None);
```


When you "await" the timer task, the orchestrator function will sleep until the specified expiration time.

Note

Orchestrations will continue to process other incoming events while waiting for a timer task to expire.

## Timer limitations

When you create a timer that expires at 4:30 pm UTC, the underlying Durable Task Framework enqueues a message that becomes visible only at 4:30 pm UTC. If the function app is scaled down to zero instances in the meantime, the newly visible timer message will ensure that the function app gets activated again on an appropriate VM.

Note

- For JavaScript, Python, and PowerShell apps, Durable timers are limited to six days. To work around this limitation, you can use the timer APIs in a
`while`

loop to simulate a longer delay. Up-to-date .NET and Java apps support arbitrarily long timers. - Depending on the version of the SDK and
[storage provider](durable-functions-storage-providers)being used, long timers of 6 days or more may be internally implemented using a series of shorter timers (e.g., of 3 day durations) until the desired expiration time is reached. This can be observed in the underlying data store but won't impact the orchestration behavior. - Don't use built-in date/time APIs for getting the current time. When calculating a future date for a timer to expire, always use the orchestrator function's current time API. For more information, see the
[orchestrator function code constraints](durable-functions-code-constraints#dates-and-times)article.

## Usage for delay

The following example illustrates how to use durable timers for delaying execution. The example is issuing a billing notification every day for 10 days.

```
[FunctionName("BillingIssuer")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
for (int i = 0; i < 10; i++)
{
DateTime deadline = context.CurrentUtcDateTime.Add(TimeSpan.FromDays(1));
await context.CreateTimer(deadline, CancellationToken.None);
await context.CallActivityAsync("SendBillingEvent");
}
}
```


Note

The previous C# example targets Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

Warning

Avoid infinite loops in orchestrator functions. For information about how to safely and efficiently implement infinite loop scenarios, see [Eternal Orchestrations](durable-functions-eternal-orchestrations).

## Usage for timeout

This example illustrates how to use durable timers to implement timeouts.

```
[FunctionName("TryGetQuote")]
public static async Task<bool> Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
TimeSpan timeout = TimeSpan.FromSeconds(30);
DateTime deadline = context.CurrentUtcDateTime.Add(timeout);
using (var cts = new CancellationTokenSource())
{
Task activityTask = context.CallActivityAsync("GetQuote");
Task timeoutTask = context.CreateTimer(deadline, cts.Token);
Task winner = await Task.WhenAny(activityTask, timeoutTask);
if (winner == activityTask)
{
// success case
cts.Cancel();
return true;
}
else
{
// timeout case
return false;
}
}
}
```


Note

The previous C# example targets Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

Warning

In .NET, JavaScript, Python, and PowerShell, you must cancel any created durable timers if your code will not wait for them to complete. See the examples above for how to cancel pending timers. The Durable Task Framework will not change an orchestration's status to "Completed" until all outstanding tasks, including durable timer tasks, are either completed or canceled.

This cancellation mechanism using the *when-any* pattern doesn't terminate in-progress activity function or sub-orchestration executions. Rather, it simply allows the orchestrator function to ignore the result and move on. If your function app uses the Consumption plan, you'll still be billed for any time and memory consumed by the abandoned activity function. By default, functions running in the Consumption plan have a timeout of five minutes. If this limit is exceeded, the Azure Functions host is recycled to stop all execution and prevent a runaway billing situation. The [function timeout is configurable](../functions-host-json#functiontimeout).

For a more in-depth example of how to implement timeouts in orchestrator functions, see the [Human Interaction & Timeouts - Phone Verification](durable-functions-phone-verification) article.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-types-features-overview -->

# Durable Functions types and features

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Durable Functions is an extension of [Azure Functions](../functions-overview). You can use Durable Functions for stateful orchestration of function execution. A durable function app is a solution that's made up of different Azure functions. Functions can play different roles in a durable function orchestration.

There are currently four durable function types in Azure Functions: activity, orchestrator, entity, and client. The rest of this section goes into more details about the types of functions involved in an orchestration.

## Orchestrator functions

Orchestrator functions describe how actions are executed and the order in which actions are executed. Orchestrator functions describe the orchestration in code (C# or JavaScript) as shown in [Durable Functions application patterns](durable-functions-overview#application-patterns). An orchestration can have many different types of actions, including [activity functions](#activity-functions), [sub-orchestrations](durable-functions-orchestrations#sub-orchestrations), [waiting for external events](durable-functions-orchestrations#external-events), [HTTP](durable-functions-http-features), and [timers](durable-functions-orchestrations#durable-timers). Orchestrator functions can also interact with [entity functions](#entity-functions).

Note

Orchestrator functions are written using ordinary code, but there are strict requirements on how to write the code. Specifically, orchestrator function code must be *deterministic*. Failing to follow these determinism requirements can cause orchestrator functions to fail to run correctly. Detailed information on these requirements and how to work around them can be found in the [code constraints](durable-functions-code-constraints) topic.

For more detailed information on orchestrator functions and their features, see the [Durable orchestrations](durable-functions-orchestrations) article.

## Activity functions

Activity functions are the basic unit of work in a durable function orchestration. Activity functions are the functions and tasks that are orchestrated in the process. For example, you might create an orchestrator function to process an order. The tasks involve checking the inventory, charging the customer, and creating a shipment. Each task would be a separate activity function. These activity functions may be executed serially, in parallel, or some combination of both.

Unlike orchestrator functions, activity functions aren't restricted in the type of work you can do in them. Activity functions are frequently used to make network calls or run CPU intensive operations. An activity function can also return data back to the orchestrator function. The Durable Task Framework guarantees that each called activity function will be executed *at least once* during an orchestration's execution.

Note

Because activity functions only guarantee *at least once* execution, we recommend you make your activity function logic *idempotent* whenever possible.

Use an [activity trigger](durable-functions-bindings#activity-trigger) to define an activity function. .NET functions receive a `DurableActivityContext`

as a parameter. You can also bind the trigger to any other JSON-serializeable object to pass in inputs to the function. In JavaScript, you can access an input via the `<activity trigger binding name>`

property on the [ context.bindings object](../functions-reference-node#bindings). Activity functions can only have a single value passed to them. To pass multiple values, you must use tuples, arrays, or complex types.

Note

You can trigger an activity function only from an orchestrator function.

## Entity functions

Entity functions define operations for reading and updating small pieces of state. We often refer to these stateful entities as *durable entities*. Like orchestrator functions, entity functions are functions with a special trigger type, *entity trigger*. They can also be invoked from client functions or from orchestrator functions. Unlike orchestrator functions, entity functions do not have any specific code constraints. Entity functions also manage state explicitly rather than implicitly representing state via control flow.

Note

Entity functions and related functionality is only available in Durable Functions 2.0 and above.

For more information about entity functions, see the [Durable Entities](durable-functions-entities) article.

## Client functions

Orchestrator functions are triggered by an [orchestration trigger binding](durable-functions-bindings#orchestration-trigger) and entity functions are triggered by an [entity trigger binding](durable-functions-bindings#entity-trigger). Both of these triggers work by reacting to messages that are enqueued into a [task hub](durable-functions-task-hubs). The primary way to deliver these messages is by using an [orchestrator client binding](durable-functions-bindings#orchestration-client) or an [entity client binding](durable-functions-bindings#entity-client) from within a *client function*. Any non-orchestrator function can be a *client function*. For example, You can trigger the orchestrator from an HTTP-triggered function, an Azure Event Hub triggered function, etc. What makes a function a *client function* is its use of the durable client output binding.

Note

Unlike other function types, orchestrator and entity functions cannot be triggered directly using the buttons in the Azure Portal. If you want to test an orchestrator or entity function in the Azure Portal, you must instead run a *client function* that starts an orchestrator or entity function as part of its implementation. For the simplest testing experience, a *manual trigger* function is recommended.

In addition to triggering orchestrator or entity functions, the *durable client* binding can be used to interact with running orchestrations and entities. For example, orchestrations can be queried, terminated, and can have events raised to them. For more information on managing orchestrations and entities, see the [Instance management](durable-functions-instance-management) article.

## Next steps

To get started, create your first durable function in [C#](durable-functions-isolated-create-first-csharp), [JavaScript](quickstart-js-vscode), [Python](quickstart-python-vscode), [PowerShell](quickstart-powershell-vscode), or [Java](quickstart-java).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-unit-testing-python -->

# Unit testing Durable Functions in Python

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Unit testing is an important part of modern software development practices. Unit tests verify business logic behavior and protect from introducing unnoticed breaking changes in the future. Durable Functions can easily grow in complexity so introducing unit tests helps avoid breaking changes. The following sections explain how to unit test the three function types - Orchestration client, orchestrator, and entity functions.

Note

This guide applies only to Durable Functions apps written in the [Python v2 programming model](../functions-reference-python).

## Prerequisites

The examples in this article require knowledge of the following concepts and frameworks:

- Unit testing
- Durable Functions
- Python
[unittest](https://docs.python.org/3/library/unittest.html) [unittest.mock](https://docs.python.org/3/library/unittest.mock.html)

## Setting up the test environment

To test Durable Functions, it's crucial to set up a proper test environment. This includes creating a test directory and installing Python's `unittest`

module into your Python environment. For more info, see the [Azure Functions Python unit testing overview](../functions-reference-python#unit-testing).

## Unit testing trigger functions

Trigger functions, often referred to as *client* functions, initiate orchestrations and external events. To test these functions:

- Mock the
`DurableOrchestrationClient`

to simulate orchestration execution and status management. - Assign
`DurableOrchestrationClient`

methods such as`start_new`

,`get_status`

, or`raise_event`

with mock functions that return expected values. - Invoke the client function directly with a mocked client and other necessary inputs such as a
`req`

(HTTP request object) for HTTP trigger client functions. - Use assertions and
`unittest.mock`

tools to verify expected orchestration start behavior, parameters, and HTTP responses.

```
import asyncio
import unittest
import azure.functions as func
from unittest.mock import AsyncMock, Mock, patch
from function_app import start_orchestrator
class TestFunction(unittest.TestCase):
@patch('azure.durable_functions.DurableOrchestrationClient')
def test_HttpStart(self, client):
# Get the original method definition as seen in the function_app.py file
func_call = http_start.build().get_user_function().client_function
req = func.HttpRequest(method='GET',
body=b'{}',
url='/api/my_second_function',
route_params={"functionName": "my_orchestrator"})
client.start_new = AsyncMock(return_value="instance_id")
client.create_check_status_response = Mock(return_value="check_status_response")
# Execute the function code
result = asyncio.run(func_call(req, client))
client.start_new.assert_called_once_with("my_orchestrator")
client.create_check_status_response.assert_called_once_with(req, "instance_id")
self.assertEqual(result, "check_status_response")
```


## Unit testing orchestrator functions

Orchestrator functions manage the execution of multiple activity functions. To test an orchestrator:

- Mock the
`DurableOrchestrationContext`

to control function execution. - Replace
`DurableOrchestrationContext`

methods needed for orchestrator execution like`call_activity`

or`create_timer`

with mock functions. These functions will typically return objects of type TaskBase with a`result`

property. - Call the orchestrator recursively, passing the result of the Task generated by the previous yield statement to the next.
- Verify the orchestrator result using the results returned from the orchestrator and
`unittest.mock`

.

```
import unittest
from unittest.mock import Mock, patch, call
from datetime import timedelta
from azure.durable_functions.testing import orchestrator_generator_wrapper
from function_app import my_orchestrator
class TestFunction(unittest.TestCase):
@patch('azure.durable_functions.DurableOrchestrationContext')
def test_chaining_orchestrator(self, context):
# Get the original method definition as seen in the function_app.py file
func_call = my_orchestrator.build().get_user_function().orchestrator_function
# The mock_activity method is defined above with behavior specific to your app.
# It returns a TaskBase object with the result expected from the activity call.
context.call_activity = Mock(side_effect=mock_activity)
# Create a generator using the method and mocked context
user_orchestrator = func_call(context)
# Use orchestrator_generator_wrapper to get the values from the generator.
# Processes the orchestrator in a way that is equivalent to the Durable replay logic
values = [val for val in orchestrator_generator_wrapper(user_orchestrator)]
expected_activity_calls = [call('say_hello', 'Tokyo'),
call('say_hello', 'Seattle'),
call('say_hello', 'London')]
self.assertEqual(context.call_activity.call_count, 3)
self.assertEqual(context.call_activity.call_args_list, expected_activity_calls)
self.assertEqual(values[3], ["Hello Tokyo!", "Hello Seattle!", "Hello London!"])
```


## Unit testing entity functions

Entity functions manage stateful objects with operations. To test an entity function:

- Mock the
`DurableEntityContext`

to simulate the entity's internal state and operation inputs. - Replace
`DurableEntityContext`

methods like`get_state`

,`set_state`

, and`operation_name`

with mocks that return controlled values. - Invoke the entity function directly with the mocked context.
- Use assertions to verify state changes and returned values, along with
`unittest.mock`

utilities.

```
import unittest
from unittest.mock import Mock, patch
from function_app import Counter
class TestEntityFunction(unittest.TestCase):
@patch('azure.durable_functions.DurableEntityContext')
def test_entity_add_operation(self, context_mock):
# Get the original method definition as seen in function_app.py
func_call = Counter.build().get_user_function().entity_function
# Setup mock context behavior
state = 0
result = None
def set_state(new_state):
nonlocal state
state = new_state
def set_result(new_result):
nonlocal result
result = new_result
context_mock.get_state = Mock(return_value=state)
context_mock.set_state = Mock(side_effect=set_state)
context_mock.operation_name = "add"
context_mock.get_input = Mock(return_value=5)
context_mock.set_result = Mock(side_effect=lambda x: set_result)
# Call the entity function with the mocked context
func_call(context_mock)
# Verify the state was updated correctly
context_mock.set_state.assert_called_once_with(5)
self.assertEqual(state, 5)
self.assertEqual(result, None)
```


## Unit testing activity functions

Activity functions require no Durable-specific modifications to be tested. The guidance found in the [Azure Functions Python unit testing overview](../functions-reference-python#unit-testing) is sufficient for testing these functions.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-serialization-and-persistence -->

# Data persistence and serialization in Durable Functions (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Durable Functions runtime automatically persists function parameters, return values, and other state to the [task hub](durable-functions-task-hubs) in order to provide reliable execution. However, the amount and frequency of data persisted to durable storage can impact application performance and storage transaction costs. Depending on the type of data your application stores, data retention and privacy policies may also need to be considered.

## Task Hub Contents

Task hubs store the current state of instances, and any pending messages:

*Instance states*store the current status and history of an instance. For orchestration instances, this state includes the runtime state, the orchestration history, inputs, outputs, and custom status. For entity instances, it includes the entity state.*Messages*store function inputs or outputs, event payloads, and metadata that is used for internal purposes, like routing and end-to-end correlation.

Messages are deleted after being processed, but instance states persist unless they're explicitly deleted by the application or an operator. In particular, an orchestration history remains in storage even after the orchestration completes.

For an example of how states and messages represent the progress of an orchestration, see the [task hub execution example](durable-functions-task-hubs#execution-example).

Where and how states and messages are represented in storage [depends on the storage provider](durable-functions-task-hubs#representation-in-storage). Durable Functions' default provider is [Azure Storage](durable-functions-azure-storage-provider), which persists data to queues, tables, and blobs in an [Azure Storage](https://azure.microsoft.com/services/storage/) account that you specify.

### Types of data that is serialized and persisted

The following list shows the different types of data that will be serialized and persisted when using features of Durable Functions:

- All inputs and outputs of orchestrator, activity, and entity functions, including any IDs and unhandled exceptions
- Orchestrator, activity, and entity function names
- External event names and payloads
- Custom orchestration status payloads
- Orchestration termination messages
- Durable timer payloads
- Durable HTTP request and response URLs, headers, and payloads
- Entity call and signal payloads
- Entity state payloads

### Working with sensitive data

When using the Azure Storage provider, all data is automatically encrypted at rest. However, anyone with access to the storage account can read the data in its unencrypted form. If you need stronger protection for sensitive data, consider first encrypting the data using your own encryption keys so that the data is persisted in its pre-encrypted form.

Alternatively, .NET users have the option of implementing custom serialization providers that provide automatic encryption. An example of custom serialization with encryption can be found in [this GitHub sample](https://github.com/charleszipp/azure-durable-entities-encryption).

Note

If you decide to implement application-level encryption, be aware that orchestrations and entities can exist for indefinite amounts of time. This matters when it comes time to rotate your encryption keys because an orchestration or entities may run longer than your key rotation policy. If a key rotation happens, the key used to encrypt your data may no longer be available to decrypt it the next time your orchestration or entity executes. Customer encryption is therefore recommended only when orchestrations and entities are expected to run for relatively short periods of time.

## Customizing serialization and deserialization

### Default serialization logic

Durable Functions for .NET in-process internally uses [Json.NET](https://www.newtonsoft.com/json/help/html/Introduction.htm) to serialize orchestration and entity data to JSON. The default Json.NET settings used are:

**Inputs, Outputs, and State:**

```
JsonSerializerSettings
{
TypeNameHandling = TypeNameHandling.None,
DateParseHandling = DateParseHandling.None,
}
```


**Exceptions:**

```
JsonSerializerSettings
{
ContractResolver = new ExceptionResolver(),
TypeNameHandling = TypeNameHandling.Objects,
ReferenceLoopHandling = ReferenceLoopHandling.Ignore,
}
```


Read more detailed documentation about `JsonSerializerSettings`

[here](https://www.newtonsoft.com/json/help/html/SerializationSettings.htm).

## Customizing serialization with .NET attributes

During serialization, Json.NET looks for [various attributes](https://www.newtonsoft.com/json/help/html/SerializationAttributes.htm) on classes and properties that control how the data is serialized and deserialized from JSON. If you own the source code for data type passed to Durable Functions APIs, consider adding these attributes to the type to customize serialization and deserialization.

## Customizing serialization with Dependency Injection

Function apps that target .NET and run on the Functions V3 runtime can use [Dependency Injection (DI)](../functions-dotnet-dependency-injection) to customize how data and exceptions are serialized. The following sample code demonstrates how to use DI to override the default Json.NET serialization settings using custom implementations of the `IMessageSerializerSettingsFactory`

and `IErrorSerializerSettingsFactory`

service interfaces.

```
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Azure.WebJobs.Extensions.DurableTask;
using Microsoft.Extensions.DependencyInjection;
using Newtonsoft.Json;
using System.Collections.Generic;
[assembly: FunctionsStartup(typeof(MyApplication.Startup))]
namespace MyApplication
{
public class Startup : FunctionsStartup
{
public override void Configure(IFunctionsHostBuilder builder)
{
builder.Services.AddSingleton<IMessageSerializerSettingsFactory, CustomMessageSerializerSettingsFactory>();
builder.Services.AddSingleton<IErrorSerializerSettingsFactory, CustomErrorSerializerSettingsFactory>();
}
/// <summary>
/// A factory that provides the serialization for all inputs and outputs for activities and
/// orchestrations, as well as entity state.
/// </summary>
internal class CustomMessageSerializerSettingsFactory : IMessageSerializerSettingsFactory
{
public JsonSerializerSettings CreateJsonSerializerSettings()
{
// Return your custom JsonSerializerSettings here
}
}
/// <summary>
/// A factory that provides the serialization for all exceptions thrown by activities
/// and orchestrations
/// </summary>
internal class CustomErrorSerializerSettingsFactory : IErrorSerializerSettingsFactory
{
public JsonSerializerSettings CreateJsonSerializerSettings()
{
// Return your custom JsonSerializerSettings here
}
}
}
}
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-configure-managed-identity -->

# Quickstart: Configure Durable Functions with managed identity

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A managed identity from the access management service [Microsoft Entra ID](../../active-directory/fundamentals/active-directory-whatis) allows your app to access other Microsoft Entra protected resources, such as an Azure Storage account, without handling secrets manually. The identity is managed by the Azure platform, so you do *not* need to provision or rotate any secrets. The recommended way to authenticate access to Azure resources is through using such an identity.

In this quickstart, you complete steps to configure a Durable Functions app using the default **Azure Storage provider** to use identity-based connections for storage account access.

Note

Managed identity is supported in [Durable Functions extension](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask) versions **2.7.0** and greater.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Prerequisites

To complete this quickstart, you need:

- An existing Durable Functions project created in the Azure portal or a local Durable Functions project deployed to Azure.
- Familiarity running a Durable Functions app in Azure.

If you don't have an existing Durable Functions project deployed in Azure, we recommend that you start with one of the following quickstarts:

[Create your first durable function - C#](durable-functions-create-first-csharp)[Create your first durable function - JavaScript](quickstart-js-vscode)[Create your first durable function - Python](quickstart-python-vscode)[Create your first durable function - PowerShell](quickstart-powershell-vscode)[Create your first durable function - Java](quickstart-java)

## Local development

### Use Azure Storage emulator

When developing locally, it's recommended that you use Azurite, which is Azure Storage's local emulator. Configure your app to the emulator by specifying `"AzureWebJobsStorage": "UseDevelopmentStorage=true"`

in the local.settings.json.

### Identity-based connections for local development

Strictly speaking, a managed identity is only available to apps when executing on Azure. However, you can still configure a locally running app to use identity-based connection by using your developer credentials to authenticate against Azure resources. Then, when deployed on Azure, the app will utilize your managed identity configuration instead.

When using developer credentials, the connection attempts to get a token from the following locations, in the said order, for access to your Azure resources:

- A local cache shared between Microsoft applications
- The current user context in Visual Studio
- The current user context in Visual Studio Code
- The current user context in the Azure CLI

If none of these options are successful, an error stating that the app cannot retrieve authentication token for your Azure resources shows up.

#### Configure runtime to use local developer identity

Specify the name of your Azure Storage account in local.settings.json, for example:

`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage__accountName": "<<your Azure Storage account name>>", "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated" } }`

Go to the Azure Storage account resource on the Azure portal, navigate to the

**Access Control (IAM)**tab, and click on**Add role assignment**. Find the following roles:- Storage Queue Data Contributor
- Storage Blob Data Contributor
- Storage Table Data Contributor

Assign the roles to yourself by clicking

**"+ Select members"**and finding your email in the pop-up window. (This email is the one you use to log into Microsoft applications, Azure CLI, or editors in the Visual Studio family.)

## Identity-based connections for app deployed to Azure

### Enable managed identity resource

To begin, enable a managed identity for your application. Your function app must have either a system-assigned managed identity or a user-assigned managed identity. To enable a managed identity for your function app, and to learn more about the differences between the two types of identities, see the [managed identity overview](../../app-service/overview-managed-identity).

### Assign access roles to the managed identity

Navigate to your app's Azure Storage resource on the Azure portal and [assign](/en-us/entra/identity/managed-identities-azure-resources/how-to-assign-access-azure-resource) three role-based access control (RBAC) roles to your managed identity resource:

- Storage Queue Data Contributor
- Storage Blob Data Contributor
- Storage Table Data Contributor

To find your identity resource, select assign access to **Managed identity** and then **+ Select members**

### Add managed identity configuration to your app

Before you can use your app's managed identity, make some changes to the app settings:

In the Azure portal, on your function app resource menu under

**Settings**, select**Environment variables**.In the list of settings, find

**AzureWebJobsStorage**and select the**Delete**icon.Add a setting to link your Azure storage account to the application.

Use

*one of the following methods*depending on the cloud that your app runs in:**Azure cloud**: If your app runs in*global Azure*, add the setting`AzureWebJobsStorage__accountName`

that identifies an Azure storage account name. Example value:`mystorageaccount123`

**Non-Azure cloud**: If your application runs in a cloud outside of Azure, you must add the following three settings to provide specific service URIs (or*endpoints*) of the storage account instead of an account name.Setting name:

`AzureWebJobsStorage__blobServiceUri`

Example value:

`https://mystorageaccount123.blob.core.windows.net/`

Setting name:

`AzureWebJobsStorage__queueServiceUri`

Example value:

`https://mystorageaccount123.queue.core.windows.net/`

Setting name:

`AzureWebJobsStorage__tableServiceUri`

Example value:

`https://mystorageaccount123.table.core.windows.net/`


You can get the values for these URI variables in the storage account information from the

**Endpoints**tab.Note

If you are using

[Azure Government](../../azure-government/documentation-government-welcome)or any other cloud that's separate from global Azure, you must use the option that provides specific service URIs instead of just the storage account name. For more information on using Azure Storage with Azure Government, see the[Develop by using the Storage API in Azure Government](../../azure-government/documentation-government-get-started-connect-to-storage).Finish your managed identity configuration (remember to click "Apply" after making the setting changes):

If you use a

*system-assigned identity*, make no other changes.If you use a

*user-assigned identity*, add the following settings in your app configuration:**AzureWebJobsStorage__credential**, enter**managedidentity****AzureWebJobsStorage__clientId**, get this GUID value from your managed identity resource


Note

Durable Functions does

*not*support`managedIdentityResourceId`

when using user-assigned identity. Use`clientId`

instead.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-external-events -->

# Handling external events in Durable Functions (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Orchestrator functions have the ability to wait and listen for external events. This feature of [Durable Functions](durable-functions-overview) is often useful for handling human interaction or other external triggers.

Note

External events are one-way asynchronous operations. They are not suitable for situations where the client sending the event needs a synchronous response from the orchestrator function.

## Wait for events

The *"wait-for-external-event"* API of the [orchestration trigger binding](durable-functions-bindings#orchestration-trigger) allows an orchestrator function to asynchronously wait and listen for an event delivered by an external client. The listening orchestrator function declares the *name* of the event and the *shape of the data* it expects to receive.

```
[FunctionName("BudgetApproval")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
bool approved = await context.WaitForExternalEvent<bool>("Approval");
if (approved)
{
// approval granted - do the approved action
}
else
{
// approval denied - send a notification
}
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

The preceding example listens for a specific single event and takes action when it's received.

You can listen for multiple events concurrently, like in the following example, which waits for one of three possible event notifications.

```
[FunctionName("Select")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
var event1 = context.WaitForExternalEvent<float>("Event1");
var event2 = context.WaitForExternalEvent<bool>("Event2");
var event3 = context.WaitForExternalEvent<int>("Event3");
var winner = await Task.WhenAny(event1, event2, event3);
if (winner == event1)
{
// ...
}
else if (winner == event2)
{
// ...
}
else if (winner == event3)
{
// ...
}
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

The previous example listens for *any* of multiple events. It's also possible to wait for *all* events.

```
[FunctionName("NewBuildingPermit")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
string applicationId = context.GetInput<string>();
var gate1 = context.WaitForExternalEvent("CityPlanningApproval");
var gate2 = context.WaitForExternalEvent("FireDeptApproval");
var gate3 = context.WaitForExternalEvent("BuildingDeptApproval");
// all three departments must grant approval before a permit can be issued
await Task.WhenAll(gate1, gate2, gate3);
await context.CallActivityAsync("IssueBuildingPermit", applicationId);
}
```


Note

The previous code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

In .NET, if the event payload cannot be converted into the expected type `T`

, an exception is thrown.

The *"wait-for-external-event"* API waits indefinitely for some input. The function app can be safely unloaded while waiting. If and when an event arrives for this orchestration instance, it is awakened automatically and immediately processes the event.

Note

If your function app uses the Consumption Plan, no billing charges are incurred while an orchestrator function is awaiting an external event task, no matter how long it waits.

As with Activity Functions, external events have an *at-least-once* delivery guarantee. This means that, under certain conditions (like restarts, scaling, crashes, etc.), your application may receive duplicates of the same external event. Therefore, we recommend that external events contain some kind of ID that allows them to be manually de-duplicated in orchestrators.

## Send events

You can use the *"raise-event"* API defined by the [orchestration client](durable-functions-bindings#orchestration-client) binding to send an external event to an orchestration. You can also use the built-in [raise event HTTP API](durable-functions-http-api#raise-event) to send an external event to an orchestration.

A raised event includes an *instance ID*, an *eventName*, and *eventData* as parameters. Orchestrator functions handle these events using the [ "wait-for-external-event"](#wait-for-events) APIs. The

*eventName*must match on both the sending and receiving ends in order for the event to be processed. The event data must also be JSON-serializable.

Internally, the *"raise-event"* mechanisms enqueue a message that gets picked up by the waiting orchestrator function. If the instance is not waiting on the specified *event name,* the event message is added to an in-memory queue. If the orchestration instance later begins listening for that *event name,* it will check the queue for event messages.

Note

If there is no orchestration instance with the specified *instance ID*, the event message is discarded.

Below is an example queue-triggered function that sends an "Approval" event to an orchestrator function instance. The orchestration instance ID comes from the body of the queue message.

```
[FunctionName("ApprovalQueueProcessor")]
public static async Task Run(
[QueueTrigger("approval-queue")] string instanceId,
[DurableClient] IDurableOrchestrationClient client)
{
await client.RaiseEventAsync(instanceId, "Approval", true);
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

Internally, the "*raise-event*" API enqueues a message that gets picked up by the waiting orchestrator function. If the instance is not waiting on the specified *event name,* the event message is added to an in-memory buffer. If the orchestration instance later begins listening for that *event name,* it will check the buffer for event messages and trigger the task that was waiting for it.

Note

If there is no orchestration instance with the specified *instance ID*, the event message is discarded.

### HTTP

The following is an example of an HTTP request that raises an "Approval" event to an orchestration instance.

```
POST /runtime/webhooks/durabletask/instances/MyInstanceId/raiseEvent/Approval&code=XXX
Content-Type: application/json
"true"
```


In this case, the instance ID is hardcoded as *MyInstanceId*.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-create-portal -->

# Create Durable Functions using the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Durable Functions](durable-functions-overview) extension for Azure Functions is provided in the NuGet package [Microsoft.Azure.WebJobs.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask). This extension must be installed in your function app. This article shows how to install this package so that you can develop durable functions in the Azure portal.

Note

- If you are developing durable functions in C#, you should instead consider
[Visual Studio 2019 development](durable-functions-isolated-create-first-csharp). - If you are developing durable functions in JavaScript, you should instead consider
[Visual Studio Code development](quickstart-js-vscode).

## Create a function app

You must have a function app to host the execution of any function. A function app lets you group your functions as a logical unit for easier management, deployment, scaling, and sharing of resources. You can create a .NET or JavaScript app.

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Function App**.Under

**Select a hosting option**, select**Consumption**>**Select**to create your app in the default**Consumption**plan. In this[serverless](https://azure.microsoft.com/overview/serverless-computing/)hosting option, you pay only for the time your functions run.[Premium plan](../functions-premium-plan)also offers dynamic scaling. When you run in an App Service plan, you must manage the[scaling of your function app](../functions-scale).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which you create your new function app. [Resource Group](../../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. You should create a new resource group because there are [known limitations when creating new function apps in an existing resource group](../functions-scale#limitations-for-creating-new-function-apps-in-an-existing-resource-group).**Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

. To guarantee a unique app name, you can optionally enable**Secure unique default hostname**, which is currently in preview.**Runtime stack**Preferred language Choose a runtime that supports your favorite function programming language. In-portal editing is only available for JavaScript, PowerShell, Python, TypeScript, and C# script.

To create a C# Script app that supports in-portal editing, you must choose a runtime**Version**that supports the**in-process model**.

C# class library and Java functions must be[developed locally](../functions-develop-local#local-development-environments).**Version**Version number Choose the version of your installed runtime. **Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access.**Operating system**Windows An operating system is preselected for you based on your runtime stack selection, but you can change the setting if necessary. In-portal editing is only supported on Windows. Accept the default options in the remaining tabs, including the default behavior of creating a new storage account on the

**Storage**tab and a new Application Insight instance on the**Monitoring**tab. You can also choose to use an existing storage account or Application Insights instance.Select

**Review + create**to review the app configuration you chose, and then select**Create**to provision and deploy the function app.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

By default, the function app created uses version 2.x of the Azure Functions runtime. The Durable Functions extension works on both versions 1.x and 2.x of the Azure Functions runtime in C#, and version 2.x in JavaScript. However, templates are only available when targeting version 2.x of the runtime regardless of the chosen language.

## Install the durable-functions npm package (JavaScript only)

If you are creating JavaScript Durable Functions, you'll need to install the [ durable-functions npm package](https://www.npmjs.com/package/durable-functions):

From your function app's page, select

**Advanced Tools**under**Development Tools**in the left pane.In the

**Advanced Tools**page, select**Go**.Inside the Kudu console, select

**Debug console**, and then**CMD**.Your function app's file directory structure should display. Navigate to the

`site/wwwroot`

folder. From there, you can upload a`package.json`

file by dragging and dropping it into the file directory window. A sample`package.json`

is below:`{ "dependencies": { "durable-functions": "^1.3.1" } }`

Once your

`package.json`

is uploaded, run the`npm install`

command from the Kudu Remote Execution Console.

## Create an orchestrator function

In your function app, select

**Functions**from the left pane, and then select**Add**from the top menu.In the search field of the

**New Function**page, enter`durable`

, and then choose the**Durable Functions HTTP starter**template.For the

**New Function**name, enter`HttpStart`

, and then select**Create Function**.The function created is used to start the orchestration.

Create another function in the function app, this time by using the

**Durable Functions orchestrator**template. Name your new orchestration function`HelloSequence`

.Create a third function named

`Hello`

by using the**Durable Functions activity**template.

## Test the durable function orchestration

Go back to the

**HttpStart**function, choose**Get function Url**, and select the**Copy to clipboard**icon to copy the URL. You use this URL to start the**HelloSequence**function.Use a secure HTTP test tool to send an HTTP POST request to the URL endpoint. This example is a cURL command that sends a POST request to the durable function:

`curl -X POST https://{your-function-app-name}.azurewebsites.net/api/orchestrators/{functionName} --header "Content-Length: 0"`

In this example,

`{your-function-app-name}`

is the domain that is the name of your function app, and`{functionName}`

is the**HelloSequence**orchestrator function. The response message contains a set of URI endpoints that you can use to monitor and manage the execution, which looks like the following example:`{ "id":"10585834a930427195479de25e0b952d", "statusQueryGetUri":"https://...", "sendEventPostUri":"https://...", "terminatePostUri":"https://...", "rewindPostUri":"https://..." }`

Make sure to choose an HTTP test tool that keeps your data secure. For more information, see

[HTTP test tools](../functions-develop-local#http-test-tools).Call the

`statusQueryGetUri`

endpoint URI and you see the current status of the durable function, which might look like this example:`{ "runtimeStatus": "Running", "input": null, "output": null, "createdTime": "2017-12-01T05:37:33Z", "lastUpdatedTime": "2017-12-01T05:37:36Z" }`

Continue calling the

`statusQueryGetUri`

endpoint until the status changes to**Completed**, and you see a response like the following example:`{ "runtimeStatus": "Completed", "input": null, "output": [ "Hello Tokyo!", "Hello Seattle!", "Hello London!" ], "createdTime": "2017-12-01T05:38:22Z", "lastUpdatedTime": "2017-12-01T05:38:28Z" }`


Your first durable function is now up and running in Azure.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-dotnet-isolated-overview -->

# Overview of Durable Functions in the .NET isolated worker

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article is an overview of Durable Functions in the [.NET isolated worker](../dotnet-isolated-process-guide). The isolated worker allows your Durable Functions app to run on a .NET version different than that of the Azure Functions host.

## Why use Durable Functions in the .NET isolated worker?

Using this model lets you get all the great benefits that come with the Azure Functions .NET isolated worker process. For more information, see [Benefits of the isolated worker model](../dotnet-isolated-process-guide#benefits-of-the-isolated-worker-model). Additionally, this new SDK includes some new [features](#feature-improvements-over-in-process-durable-functions).

### Feature improvements over in-process Durable Functions

- Orchestration input can be injected directly:
`MyOrchestration([OrchestrationTrigger] TaskOrchestrationContext context, T input)`

- Support for strongly typed calls and class-based activities and orchestrations (NOTE: in preview. For more information, see
[here](#source-generator-and-class-based-activities-and-orchestrations).) - Plus all the benefits of the Azure Functions .NET isolated worker.

### Source generator and class-based activities and orchestrations

**Requirement**: add `<PackageReference Include="Microsoft.DurableTask.Generators" Version="1.0.0-preview.1" />`

to your project.

By adding the source generator package, you get access to two new features:

**Class-based activities and orchestrations**, an alternative way to write Durable Functions. Instead of "function-based", you write strongly typed classes, which inherit types from the Durable SDK.**Strongly typed extension methods**for invoking sub orchestrations and activities. These extension methods can also be used from "function-based" activities and orchestrations.

#### Function-based example

```
public static class MyFunctions
{
[Function(nameof(MyActivity))]
public static async Task<string> MyActivity([ActivityTrigger] string input)
{
// implementation
}
[Function(nameof(MyOrchestration))]
public static async Task<string> MyOrchestration([OrchestrationTrigger] TaskOrchestrationContext context, string input)
{
// implementation
return await context.CallActivityAsync(nameof(MyActivity), input);
}
}
```


#### Class-based example

```
[DurableTask(nameof(MyActivity))]
public class MyActivity : TaskActivity<string, string>
{
private readonly ILogger logger;
public MyActivity(ILogger<MyActivity> logger) // activities have access to DI.
{
this.logger = logger;
}
public async override Task<string> RunAsync(TaskActivityContext context, string input)
{
// implementation
}
}
[DurableTask(nameof(MyOrchestration))]
public class MyOrchestration : TaskOrchestrator<string, string>
{
public async override Task<string> RunAsync(TaskOrchestrationContext context, string input)
{
ILogger logger = context.CreateReplaySafeLogger<MyOrchestration>(); // orchestrations do NOT have access to DI.
// An extension method was generated for directly invoking "MyActivity".
return await context.CallMyActivityAsync(input);
}
}
```


## Durable entities

Durable entities are supported in the .NET isolated worker. For more information, see the [developer's guide](durable-functions-dotnet-entities).

## Migration guide

This process assumes you're starting with a .NET Durable Functions 2.x project running in-process with the Functions host.

### Migrate your project

The first step is to [migrate your .NET project to the isolated worker process](../migrate-dotnet-to-isolated-model).

### Update package reference

After you've migrated your app to use the isolate worker process, you must update your Durable Functions NuGet package to reference the isolated worker-specific package, like in this example:

Old:

```
<ItemGroup>
<PackageReference Include="Microsoft.Azure.WebJobs.Extensions.DurableTask" Version="2.9.0" />
</ItemGroup>
```


New:

```
<ItemGroup>
<PackageReference Include="Microsoft.Azure.Functions.Worker.Extensions.DurableTask" Version="1.1.0" />
</ItemGroup>
```


### Update your code

Durable Functions for .NET isolated worker is an entirely new package with different types and namespaces. There are required changes to your code as a result, but many of the APIs line up with no changes needed.

#### Host.json schema

The schema for Durable Functions .NET isolated worker and Durable Functions 2.x has remained the same, no changes should be needed.

#### Public API changes

This table isn't an exhaustive list of changes.

| 2.x | Isolated |
|---|---|
`IDurableOrchestrationClient` |
`DurableTaskClient` |
`IDurableOrchestrationClient.StartNewAsync` |
`DurableTaskClient.ScheduleNewOrchestrationInstanceAsync` |
`IDurableEntityClient.SignalEntityAsync` |
`DurableTaskClient.Entities.SignalEntityAsync` |
`IDurableEntityClient.ReadEntityStateAsync` |
`DurableTaskClient.Entities.GetEntityAsync` |
`IDurableEntityClient.ListEntitiesAsync` |
`DurableTaskClient.Entities.GetAllEntitiesAsync` |
`IDurableEntityClient.CleanEntityStorageAsync` |
`DurableTaskClient.Entities.CleanEntityStorageAsync` |
`IDurableOrchestrationContext` |
`TaskOrchestrationContext` |
`IDurableOrchestrationContext.GetInput<T>()` |
`TaskOrchestrationContext.GetInput<T>()` or inject input as a parameter: `MyOrchestration([OrchestrationTrigger] TaskOrchestrationContext context, T input)` |
`DurableActivityContext` |
No equivalent |
`DurableActivityContext.GetInput<T>()` |
Inject input as a parameter `MyActivity([ActivityTrigger] T input)` |
`IDurableOrchestrationContext.CallActivityWithRetryAsync` |
`TaskOrchestrationContext.CallActivityAsync` , include `TaskOptions` parameter with retry details. |
`IDurableOrchestrationContext.CallSubOrchestratorWithRetryAsync` |
`TaskOrchestrationContext.CallSubOrchestratorAsync` , include `TaskOptions` parameter with retry details. |
`IDurableOrchestrationContext.CallHttpAsync` |
`TaskOrchestrationContext.CallHttpAsync` |
`IDurableOrchestrationContext.CreateReplaySafeLogger(ILogger)` |
`TaskOrchestrationContext.CreateReplaySafeLogger<T>()` or `TaskOrchestrationContext.CreateReplaySafeLogger(string)` |
`IDurableOrchestrationContext.CallEntityAsync` |
`TaskOrchestrationContext.Entities.CallEntityAsync` |
`IDurableOrchestrationContext.SignalEntity` |
`TaskOrchestrationContext.Entities.SignalEntityAsync` |
`IDurableOrchestrationContext.LockAsync` |
`TaskOrchestrationContext.Entities.LockEntitiesAsync` |
`IDurableOrchestrationContext.IsLocked` |
`TaskOrchestrationContext.Entities.InCriticalSection` |
`IDurableEntityContext` |
`TaskEntityContext` . |
`IDurableEntityContext.EntityName` |
`TaskEntityContext.Id.Name` |
`IDurableEntityContext.EntityKey` |
`TaskEntityContext.Id.Key` |
`IDurableEntityContext.OperationName` |
`TaskEntityOperation.Name` |
`IDurableEntityContext.FunctionBindingContext` |
Removed, add `FunctionContext` as an input parameter |
`IDurableEntityContext.HasState` |
`TaskEntityOperation.State.HasState` |
`IDurableEntityContext.BatchSize` |
Removed |
`IDurableEntityContext.BatchPosition` |
Removed |
`IDurableEntityContext.GetState` |
`TaskEntityOperation.State.GetState` |
`IDurableEntityContext.SetState` |
`TaskEntityOperation.State.SetState` |
`IDurableEntityContext.DeleteState` |
`TaskEntityOperation.State.SetState(null)` |
`IDurableEntityContext.GetInput` |
`TaskEntityOperation.GetInput` |
`IDurableEntityContext.Return` |
Removed. Method return value used instead. |
`IDurableEntityContext.SignalEntity` |
`TaskEntityContext.SignalEntity` |
`IDurableEntityContext.StartNewOrchestration` |
`TaskEntityContext.ScheduleNewOrchestration` |
`IDurableEntityContext.DispatchAsync` |
`TaskEntityDispatcher.DispatchAsync` . Constructor params removed. |
`IDurableOrchestrationClient.GetStatusAsync` |
`DurableTaskClient.GetInstanceAsync` |

#### Behavioral changes

- Serialization default behavior has changed from
`Newtonsoft.Json`

to`System.Text.Json`

. For more information, see[here](durable-functions-serialization-and-persistence).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-powershell-v2-sdk-migration-guide -->

# Guide to the standalone Durable Functions PowerShell SDK

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Durable Functions (DF) PowerShell SDK is now available as a standalone module in the PowerShell Gallery: [ AzureFunctions.PowerShell.Durable.SDK](https://www.powershellgallery.com/packages/AzureFunctions.PowerShell.Durable.SDK).
This SDK is now

**generally available (GA)**and is the recommended approach for authoring Durable Functions apps with PowerShell. In this article, we explain the benefits of this change, and what changes you can expect when adopting this new package.

## Motivation behind the standalone SDK

The previous DF SDK was built into the PowerShell language worker. This approach came with the benefit that Durable Functions apps could be authored out of the box for Azure Functions PowerShell users. However, it also came with various shortcomings:

- New features, bug fixes, and other changes were dependent on the PowerShell worker's release cadence.
- Due to the auto-upgrading nature of the PowerShell worker, the DF SDK needed to be conservative about fixing bugs as any behavior changes could constitute a breaking change.
- The replay algorithm utilized by the built-in DF SDK was outdated: other DF SDKs already utilized a faster and more reliable implementation.

By creating a standalone DF PowerShell SDK package, we're able to overcome these shortcomings. These are the benefits of utilizing this new standalone SDK package:

- This SDK includes many highly requested improvements such as better exception and null-value handling, and serialization fixes.
- The package is versioned independently of the PowerShell worker. This allows users to incorporate new features and fixes as soon as they're available, while also avoiding breaking changes from automatic upgrades.
- The replay logic is faster, and more reliable: it uses the same replay engine as the DF isolated SDK for C#.

## Deprecation plan for the built-in DF PowerShell SDK

The built-in DF SDK in the PowerShell worker will remain available for PowerShell 7.4 and prior releases.

We plan to eventually release a new **major** version of the PowerShell worker without the built-in SDK. At that point, users would need to install the SDK separately using this standalone package; the installation steps are described below.

## Install and enable the SDK

See this section to learn how to install and enable new standalone SDK in your existing app.

### Prerequisites

The standalone PowerShell SDK requires the following minimum versions:

[Azure Functions Runtime](../functions-versions)v4.16+[Azure Functions Core Tools](../functions-run-local)v4.0.5095+ (if running locally)- Azure Functions PowerShell app for PowerShell 7.4 or greater

### Opt in to the standalone DF SDK

The following application setting is required to run the standalone PowerShell SDK:

- Name:
`ExternalDurablePowerShellSDK`

- Value:
`"true"`


This application setting will disable the built-in Durable SDK for PowerShell versions 7.4 and above, forcing the worker to use the external SDK.

If you're running locally using [Azure Functions Core Tools](../functions-run-local), you should add this setting to your `local.settings.json`

file. If you're running in Azure, follow these steps with the tool of your choice:

Replace `<FUNCTION_APP_NAME>`

and `<RESOURCE_GROUP_NAME>`

with the name of your function app and resource group, respectively.

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> --resource-group <RESOURCE_GROUP_NAME> --settings ExternalDurablePowerShellSDK="true"
```


### Install and import the SDK

You have two options for installing the SDK package: it can be installed using [Managed Dependencies](../functions-reference-powershell#managed-dependencies-feature), or [bundled with your app content](../functions-reference-powershell#including-modules-in-app-content).
In this section, we describe both options, but only one of them is needed.

#### Installation option 1: Use managed dependencies

To install the SDK as a managed dependency, you'll need to follow the [managed dependencies guidance](../functions-reference-powershell#dependency-management). Please review the guidance for details.
In summary, you first need to ensure your `host.json`

contains a `managedDependency`

section with an `enabled`

property set to `true`

. Below is an example `host.json`

that satisfies this requirement:

```
{
"version": "2.0",
"managedDependency": {
"enabled": true
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[3.*, 4.0.0)"
},
}
```


Then you simply need to specify an entry for the DF SDK in your `requirements.psd1`

file, as in the example below:

```
# This file enables modules to be automatically managed by the Functions service.
# See https://aka.ms/functionsmanageddependency for additional information.
#
@{
# For latest supported version, go to 'https://www.powershellgallery.com/packages/AzureFunctions.PowerShell.Durable.SDK/'.
'AzureFunctions.PowerShell.Durable.SDK' = '2.*'
}
```


#### Installation option 2: Include the SDK module in your app content

To include the standalone DF SDK in your app content, you need to follow the [guidance regarding including modules in app content](../functions-reference-powershell#including-modules-in-app-content). Make sure to review the aforementioned docs for details.
In summary, you'll need to place the SDK package inside a `".\Modules"`

directory located at the root of your app.

For example, from within your application's root, and after creating a `".\Modules"`

directory, you may download the standalone SDK into the modules directory as such:

```
Save-Module -Name AzureFunctions.PowerShell.Durable.SDK -AllowPrerelease -Path ".\Modules"
```


#### Importing the SDK

The final step is importing the SDK into your code's session. To do this, import the PowerShell SDK via `Import-Module AzureFunctions.PowerShell.Durable.SDK -ErrorAction Stop`

in your `profile.ps1`

file.
For example, if your app was scaffolded through templates, your `profile.ps1`

file may end up looking as such:

```
# Azure Functions profile.ps1
#
# This profile.ps1 will get executed every "cold start" of your Function App.
# "cold start" occurs when:
#
# * A Function App starts up for the very first time
# * A Function App starts up after being de-allocated due to inactivity
#
# You can define helper functions, run commands, or specify environment variables
# NOTE: any variables defined that are not environment variables will get reset after the first execution
# Authenticate with Azure PowerShell using MSI.
# Remove this if you are not planning on using MSI or Azure PowerShell.
if ($env:MSI_SECRET) {
Disable-AzContextAutosave -Scope Process | Out-Null
Connect-AzAccount -Identity
}
# Uncomment the next line to enable legacy AzureRm alias in Azure PowerShell.
# Enable-AzureRmAlias
# You can also define functions or aliases that can be referenced in any of your PowerShell functions.
# Import standalone PowerShell SDK
Import-Module AzureFunctions.PowerShell.Durable.SDK -ErrorAction Stop
```


These are all the steps needed to utilize the next PowerShell SDK. Run your app as normal, via `func host start`

in your terminal to start using the SDK.

### SDK reference

See [AzureFunctions.PowerShell.Durable.SDK Module](https://github.com/Azure/azure-functions-durable-powershell/blob/main/src/Help/AzureFunctions.PowerShell.Durable.SDK.md) for the complete reference of the SDK cmdlets and their parameters.

You can also use the `Get-Help`

cmdlet to get detailed descriptions of the SDK cmdlets. In order to do this, you need to import the module first, as shown in the previous section. After that, you can run the following command to get the entire list of cmdlets:

```
Get-Help *-Durable*
```


In order to get detailed help on a specific cmdlet, including usage examples, run:

```
Get-Help Invoke-DurableOrchestration -Full
```


### Migration guide

In this section, we describe the interface and behavioral changes you can expect when utilizing the new SDK.

#### New cmdlets

`Invoke-DurableSubOrchestrator`

is a new cmdlet that allows users to utilize suborchestrators in their workflows.`Suspend-DurableOrchestration`

and`Resume-DurableOrchestration`

are new cmdlets that allow users to suspend and resume orchestrations, respectively.

#### Modified cmdlets

- The
`Get-DurableTaskResult`

cmdlet now only accepts a single Task as it's argument, instead of accepting a list of Tasks. - The
`New-DurableRetryOptions`

cmdlet is renamed to`New-DurableRetryPolicy`

(an alias for the old name is provided for backward compatibility).

#### Behavioral changes

- Exceptions thrown by activities scheduled with
`Wait-DurableTask`

(as in the Fan-Out/Fan-In pattern) are no longer silently ignored. Instead, on an exception, the cmdlet propagates that exception to the orchestrator so that it may be handled by user-code. - Null values are no longer dropped from the result list of a
`Wait-DurableTask`

(i.e., WhenAll) invocation. This means that a successful invocation of`Wait-DurableTask`

without the`-Any`

flag should return an array of the same size as the number of tasks it scheduled.

### Get support and provide feedbsck

Please report any feedback and suggestions to the SDK's [ GitHub repo](https://github.com/Azure/azure-functions-durable-powershell).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-versioning -->

# Versioning challenges and approaches in Durable Functions (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

It is inevitable that functions will be added, removed, and changed over the lifetime of an application. [Durable Functions](durable-functions-overview) allows chaining functions together in ways that weren't previously possible, and this chaining affects how you can handle versioning.

## Types of breaking changes

There are several examples of breaking changes to be aware of. This article discusses the most common ones. The main theme behind all of them is that both new and existing function orchestrations are impacted by changes to function code.

### Changing activity or entity function signatures

A signature change refers to a change in the name, input, or output of a function. If this kind of change is made to an activity or entity function, it could break any orchestrator function that depends on it. This is especially true for type-safe languages. If you update the orchestrator function to accommodate this change, you could break existing in-flight instances.

As an example, suppose we have the following orchestrator function.

```
[FunctionName("FooBar")]
public static Task Run([OrchestrationTrigger] IDurableOrchestrationContext context)
{
bool result = await context.CallActivityAsync<bool>("Foo");
await context.CallActivityAsync("Bar", result);
}
```


This simplistic function takes the results of **Foo** and passes it to **Bar**. Let's assume we need to change the return value of **Foo** from a Boolean to a String to support a wider variety of result values. The result looks like this:

```
[FunctionName("FooBar")]
public static Task Run([OrchestrationTrigger] IDurableOrchestrationContext context)
{
string result = await context.CallActivityAsync<string>("Foo");
await context.CallActivityAsync("Bar", result);
}
```


This change works fine for all new instances of the orchestrator function but may break any in-flight instances. For example, consider the case where an orchestration instance calls a function named `Foo`

, gets back a boolean value, and then checkpoints. If the signature change is deployed at this point, the checkpointed instance will fail immediately when it resumes and replays the call to `Foo`

. This failure happens because the result in the history table is a Boolean value but the new code tries to deserialize it into a String value, resulting in unexpected behavior or even runtime exception for type-safe languages.

This example is just one of many different ways that a function signature change can break existing instances. In general, if an orchestrator needs to change the way it calls a function, then the change is likely to be problematic.

### Changing orchestrator logic

The other class of versioning problems come from changing the orchestrator function code in a way that changes the execution path for in-flight instances.

Consider the following orchestrator function:

```
[FunctionName("FooBar")]
public static Task Run([OrchestrationTrigger] IDurableOrchestrationContext context)
{
bool result = await context.CallActivityAsync<bool>("Foo");
await context.CallActivityAsync("Bar", result);
}
```


Now let's assume you want to make a change to add a new function call in between the two existing function calls.

```
[FunctionName("FooBar")]
public static Task Run([OrchestrationTrigger] IDurableOrchestrationContext context)
{
bool result = await context.CallActivityAsync<bool>("Foo");
if (result)
{
await context.CallActivityAsync("SendNotification");
}
await context.CallActivityAsync("Bar", result);
}
```


This change adds a new function call to *SendNotification* between *Foo* and *Bar*. There are no signature changes. The problem arises when an existing instance resumes from the call to *Bar*. During replay, if the original call to *Foo* returned `true`

, then the orchestrator replay will call into *SendNotification*, which is not in its execution history. The runtime detects this inconsistency and raises a *non-deterministic orchestration* error because it encountered a call to *SendNotification* when it expected to see a call to *Bar*. The same type of problem can occur when adding API calls to other durable operations, like creating durable timers, waiting for external events, calling sub-orchestrations, etc.

## Mitigation strategies

Here are some of the strategies for dealing with versioning challenges:

- Do nothing (not recommended)
- Orchestration versioning (recommended in most cases)
- Stop all in-flight instances
- Side-by-side deployments

### Do nothing

The naive approach to versioning is to do nothing and let in-flight orchestration instances fail. Depending on the type of change, the following types of failures may occur.

- Orchestrations may fail with a
*non-deterministic orchestration*error. - Orchestrations may get stuck indefinitely, reporting a
`Running`

status. - If a function gets removed, any function that tries to call it may fail with an error.
- If a function gets removed after it was scheduled to run, then the app may experience low-level runtime failures in the Durable Task Framework engine, potentially resulting in severe performance degradation.

Because of these potential failures, the "do nothing" strategy is not recommended.

### Orchestration versioning

Note

Orchestration versioning is currently in public preview.

The orchestration versioning feature allows different versions of orchestrations to coexist and execute concurrently without conflicts and non-determinism issues, making it possible to deploy updates while allowing in-flight orchestration instances to complete without manual intervention.

With orchestration versioning:

- Each orchestration instance gets a version permanently associated with it when created
- Orchestrator functions can examine their version and branch execution accordingly
- Workers running newer orchestrator function versions can continue executing orchestration instances created by older versions
- The runtime prevents workers running older orchestrator function versions from executing orchestrations of newer versions

This strategy is recommended for applications that need to support breaking changes while maintaining [zero-downtime deployments](durable-functions-zero-downtime-deployment).

For detailed configuration and implementation guidance, see [Orchestration versioning in Durable Functions](durable-functions-orchestration-versioning).

### Stop all in-flight instances

Another option is to stop all in-flight instances. If you're using the default [Azure Storage provider for Durable Functions](durable-functions-storage-providers#azure-storage), stopping all instances can be done by clearing the contents of the internal **control-queue** and **workitem-queue** queues. You can alternatively stop the function app, delete these queues, and restart the app again. The queues will be recreated automatically once the app restarts. The previous orchestration instances may remain in the "Running" state indefinitely, but they will not clutter your logs with failure messages or cause any harm to your app. This approach is ideal in rapid prototype development, including local development.

Note

This approach requires direct access to the underlying storage resources, and might not be appropriate for all storage providers supported by Durable Functions.

### Side-by-side deployments

The most fail-proof way to ensure that breaking changes are deployed safely is by deploying them side-by-side with your older versions. This can be done using any of the following techniques:

- Deploy all the updates as entirely new functions, leaving existing functions as-is. This generally isn't recommended because of the complexity involved in recursively updating the callers of the new function versions.
- Deploy all the updates as a new function app with a different storage account.
- Deploy a new copy of the function app with the same storage account but with an updated
[task hub](durable-functions-task-hubs)name. This results in the creation of new storage artifacts that can be used by the new version of your app. The old version of your app will continue to execute using the previous set of storage artifacts.

Side-by-side deployment is the recommended technique for deploying new versions of your function apps.

Note

This guidance for the side-by-side deployment strategy uses Azure Storage-specific terms, but applies generally to all supported [Durable Functions storage providers](durable-functions-storage-providers).

### Deployment slots

When doing side-by-side deployments in Azure Functions or Azure App Service, we recommend that you deploy the new version of the function app to a new [Deployment slot](../functions-deployment-slots). Deployment slots allow you to run multiple copies of your function app side-by-side with only one of them as the active *production* slot. When you are ready to expose the new orchestration logic to your existing infrastructure, it can be as simple as swapping the new version into the production slot.

Note

This strategy works best when you use HTTP and webhook triggers for orchestrator functions. For non-HTTP triggers, such as queues or Event Hubs, the trigger definition should [derive from an app setting](../functions-bindings-expressions-patterns#binding-expressions---app-settings) that gets updated as part of the swap operation.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-sub-orchestrations -->

# Sub-orchestrations in Durable Functions (Azure Functions)

In addition to calling activity functions, orchestrator functions can call other orchestrator functions. For example, you can build a larger orchestration out of a library of smaller orchestrator functions. Or you can run multiple instances of an orchestrator function in parallel.

An orchestrator function can call another orchestrator function using the *"call-sub-orchestrator"* API. The [Error Handling & Compensation](durable-functions-error-handling#automatic-retry-on-failure) article has more information on automatic retry.

Sub-orchestrator functions behave just like activity functions from the caller's perspective. They can return a value and throw an exception as the parent orchestrator function anticipates them.

Note

Version 4 of the Node.js programming model for Azure Functions is generally available. The v4 model is designed to provide a more flexible and intuitive experience for JavaScript and TypeScript developers. For more information about the differences between v3 and v4, see the [migration guide](../functions-node-upgrade-v4).

In the following code snippets, JavaScript (PM4) denotes programming model v4, the new experience.

## Example

The following example illustrates an IoT ("Internet of Things") scenario where there are multiple devices that need to be provisioned. The following function represents the provisioning workflow that needs to be executed for each device:

```
public static async Task DeviceProvisioningOrchestration(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
string deviceId = context.GetInput<string>();
// Step 1: Create an installation package in blob storage and return a SAS URL.
Uri sasUrl = await context.CallActivityAsync<Uri>("CreateInstallationPackage", deviceId);
// Step 2: Notify the device that the installation package is ready.
await context.CallActivityAsync("SendPackageUrlToDevice", Tuple.Create(deviceId, sasUrl));
// Step 3: Wait for the device to acknowledge that it has downloaded the new package.
await context.WaitForExternalEvent<bool>("DownloadCompletedAck");
// Step 4: ...
}
```


```
public static async Task DeviceProvisioningOrchestration(
[OrchestrationTrigger] TaskOrchestrationContext context, string deviceId)
{
// Step 1: Create an installation package in blob storage and return a SAS URL.
Uri sasUrl = await context.CallActivityAsync<Uri>("CreateInstallationPackage", deviceId);
// Step 2: Notify the device that the installation package is ready.
await context.CallActivityAsync("SendPackageUrlToDevice", (deviceId, sasUrl));
// Step 3: Wait for the device to acknowledge that it has downloaded the new package.
await context.WaitForExternalEvent<bool>("DownloadCompletedAck");
// Step 4: ...
}
```


```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context) {
const deviceId = context.df.getInput();
// Step 1: Create an installation package in blob storage and return a SAS URL.
const sasUrl = yield context.df.callActivity("CreateInstallationPackage", deviceId);
// Step 2: Notify the device that the installation package is ready.
yield context.df.callActivity("SendPackageUrlToDevice", { id: deviceId, url: sasUrl });
// Step 3: Wait for the device to acknowledge that it has downloaded the new package.
yield context.df.waitForExternalEvent("DownloadCompletedAck");
// Step 4: ...
});
```


```
const df = require("durable-functions");
df.app.orchestration("deviceProvisioningOrchestration", function* (context) {
const deviceId = context.df.getInput();
// Step 1: Create an installation package in blob storage and return a SAS URL.
const sasUrl = yield context.df.callActivity("createInstallationPackage", deviceId);
// Step 2: Notify the device that the installation package is ready.
yield context.df.callActivity("sendPackageUrlToDevice", { id: deviceId, url: sasUrl });
// Step 3: Wait for the device to acknowledge that it has downloaded the new package.
yield context.df.waitForExternalEvent("downloadCompletedAck");
// Step 4: ...
});
```


```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
device_id = context.get_input()
# Step 1: Create an installation package in blob storage and return a SAS URL.
sas_url = yield context.call_activity("CreateInstallationPackage", device_id)
# Step 2: Notify the device that the installation package is ready.
yield context.call_activity("SendPackageUrlToDevice", { "id": device_id, "url": sas_url })
# Step 3: Wait for the device to acknowledge that it has downloaded the new package.
yield context.call_activity("DownloadCompletedAck")
# Step 4: ...
```


```
@FunctionName("DeviceProvisioningOrchestration")
public void deviceProvisioningOrchestration(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
// Step 1: Create an installation package in blob storage and return a SAS URL.
String deviceId = ctx.getInput(String.class);
String blobUri = ctx.callActivity("CreateInstallPackage", deviceId, String.class).await();
// Step 2: Notify the device that the installation package is ready.
String[] args = { deviceId, blobUri };
ctx.callActivity("SendPackageUrlToDevice", args).await();
// Step 3: Wait for the device to acknowledge that it has downloaded the new package.
ctx.waitForExternalEvent("DownloadCompletedAck").await();
// Step 4: ...
}
```


```
param($Context)
$deviceId = $Context.Input
# Step 1: Create an installation package in blob storage and return a SAS URL.
$sasUrl = Invoke-DurableActivity -FunctionName "CreateInstallationPackage" -Input $deviceId
# Step 2: Notify the device that the installation package is ready.
$deviceInfo = @{
id = $deviceId
url = $sasUrl
}
Invoke-DurableActivity -FunctionName "SendPackageUrlToDevice" -Input $deviceInfo
# Step 3: Wait for the device to acknowledge that it has downloaded the new package.
Start-DurableExternalEventListener -EventName "DownloadCompletedAck"
# Step 4: ...
```


This orchestrator function can be used as-is for one-off device provisioning or it can be part of a larger orchestration. In the latter case, the parent orchestrator function can schedule instances of `DeviceProvisioningOrchestration`

using the *"call-sub-orchestrator"* API.

The following example shows how to run multiple orchestrator functions at the same time:

```
[FunctionName("ProvisionNewDevices")]
public static async Task ProvisionNewDevices(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
string[] deviceIds = await context.CallActivityAsync<string[]>("GetNewDeviceIds");
// Run multiple device provisioning flows in parallel
var provisioningTasks = new List<Task>();
foreach (string deviceId in deviceIds)
{
Task provisionTask = context.CallSubOrchestratorAsync("DeviceProvisioningOrchestration", deviceId);
provisioningTasks.Add(provisionTask);
}
await Task.WhenAll(provisioningTasks);
// ...
}
```


Note

The previous C# examples are for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

```
[FunctionName("ProvisionNewDevices")]
public static async Task ProvisionNewDevices(
[OrchestrationTrigger] TaskOrchestrationContext context)
{
string[] deviceIds = await context.CallActivityAsync<string[]>("GetNewDeviceIds");
// Run multiple device provisioning flows in parallel
var provisioningTasks = new List<Task>();
foreach (string deviceId in deviceIds)
{
Task provisionTask = context.CallSubOrchestratorAsync("DeviceProvisioningOrchestration", deviceId);
provisioningTasks.Add(provisionTask);
}
await Task.WhenAll(provisioningTasks);
// ...
}
```


```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context) {
const deviceIds = yield context.df.callActivity("GetNewDeviceIds");
// Run multiple device provisioning flows in parallel
const provisioningTasks = [];
var id = 0;
for (const deviceId of deviceIds) {
const child_id = context.df.instanceId+`:${id}`;
const provisionTask = context.df.callSubOrchestrator("DeviceProvisioningOrchestration", deviceId, child_id);
provisioningTasks.push(provisionTask);
id++;
}
yield context.df.Task.all(provisioningTasks);
// ...
});
```


```
const df = require("durable-functions");
df.app.orchestration("provisionNewDevices", function* (context) {
const deviceIds = yield context.df.callActivity("getNewDeviceIds");
// Run multiple device provisioning flows in parallel
const provisioningTasks = [];
var id = 0;
for (const deviceId of deviceIds) {
const child_id = context.df.instanceId + `:${id}`;
const provisionTask = context.df.callSubOrchestrator(
"deviceProvisioningOrchestration",
deviceId,
child_id
);
provisioningTasks.push(provisionTask);
id++;
}
yield context.df.Task.all(provisioningTasks);
// ...
});
```


```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
device_IDs = yield context.call_activity("GetNewDeviceIds")
# Run multiple device provisioning flows in parallel
provisioning_tasks = []
id_ = 0
for device_id in device_IDs:
child_id = f"{context.instance_id}:{id_}"
provision_task = context.call_sub_orchestrator("DeviceProvisioningOrchestration", device_id, child_id)
provisioning_tasks.append(provision_task)
id_ += 1
yield context.task_all(provisioning_tasks)
# ...
```


```
@FunctionName("ProvisionNewDevices")
public void provisionNewDevices(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
List<?> deviceIDs = ctx.getInput(List.class);
// Schedule each device provisioning sub-orchestration to run in parallel
List<Task<Void>> parallelTasks = deviceIDs.stream()
.map(device -> ctx.callSubOrchestrator("DeviceProvisioningOrchestration", device))
.collect(Collectors.toList());
// ...
}
```


```
param($Context)
$deviceIds = Invoke-DurableActivity -FunctionName "GetNewDeviceIds"
# Run multiple device provisioning flows in parallel
$provisioningTasks = @()
for ($i = 0; $i -lt $deviceIds.Count; $i++) {
$deviceId = $deviceIds[$i]
$childId = "$($Context.InstanceId):$i"
$provisionTask = Invoke-DurableSubOrchestrator `
-FunctionName "DeviceProvisioningOrchestration" `
-Input $deviceId `
-InstanceId $childId `
-NoWait
$provisioningTasks += $provisionTask
}
Wait-DurableTask -Task $provisioningTasks
# ...
```


Note

Sub-orchestrations must be defined in the same function app as the parent orchestration. If you need to call and wait for orchestrations in another function app, consider using the built-in support for HTTP APIs and the HTTP 202 polling consumer pattern. For more information, see the [HTTP Features](durable-functions-http-features) topic.

## Next steps

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-code-constraints -->

# Orchestrator function code constraints

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Durable Functions is an extension of [Azure Functions](../functions-overview) that lets you build stateful apps. You can use an [orchestrator function](durable-functions-orchestrations) to orchestrate the execution of other durable functions within a function app. Orchestrator functions are stateful, reliable, and potentially long-running.

## Orchestrator code constraints

Orchestrator functions use [event sourcing](/en-us/azure/architecture/patterns/event-sourcing) to ensure reliable execution and to maintain local variable state. The [replay behavior](durable-functions-orchestrations#reliability) of orchestrator code creates constraints on the type of code that you can write in an orchestrator function. For example, orchestrator functions must be *deterministic*: an orchestrator function will be replayed multiple times, and it must produce the same result each time.

### Using deterministic APIs

This section provides some simple guidelines that help ensure your code is deterministic.

Orchestrator functions can call any API in their target languages. However, it's important that orchestrator functions call only deterministic APIs. A *deterministic API* is an API that always returns the same value given the same input, no matter when or how often it's called.

The following sections provide guidance on APIs and patterns that you should avoid because they are *not* deterministic. These restrictions apply only to orchestrator functions. Other function types don't have such restrictions.

Note

Several types of code constraints are described below. This list is unfortunately not comprehensive and some use cases might not be covered. The most important thing to consider when writing orchestrator code is whether an API you're using is deterministic. Once you're comfortable with thinking this way, it's easy to understand which APIs are safe to use and which are not without needing to refer to this documented list.

#### Dates and times

APIs that return the current date or time are nondeterministic and should never be used in orchestrator functions. This is because each orchestrator function replay will produce a different value. You should instead use the Durable Functions equivalent API for getting the current date or time, which remains consistent across replays.

Do not use `DateTime.Now`

, `DateTime.UtcNow`

, or equivalent APIs for getting the current time. Classes such as [ Stopwatch](/en-us/dotnet/api/system.diagnostics.stopwatch) should also be avoided. For .NET in-process orchestrator functions, use the

`IDurableOrchestrationContext.CurrentUtcDateTime`

property to get the current time. For .NET isolated orchestrator functions, use the `TaskOrchestrationContext.CurrentDateTimeUtc`

property to get the current time.```
DateTime startTime = context.CurrentUtcDateTime;
// do some work
TimeSpan totalTime = context.CurrentUtcDateTime.Subtract(startTime);
```


#### GUIDs and UUIDs

APIs that return a random GUID or UUID are nondeterministic because the generated value is different for each replay. Depending on which language you use, a built-in API for generating deterministic GUIDs or UUIDs may be available. Otherwise, use an activity function to return a randomly generated GUID or UUID.

Do not use APIs like `Guid.NewGuid()`

to generate random GUIDs. Instead, use the context object's `NewGuid()`

API to generate a random GUID that's safe for orchestrator replay.

```
Guid randomGuid = context.NewGuid();
```


Note

GUIDs generated with orchestration context APIs are [Type 5 UUIDs](https://en.wikipedia.org/wiki/Universally_unique_identifier#Versions_3_and_5_(namespace_name-based)).

#### Random numbers

Use an activity function to return random numbers to an orchestrator function. The return values of activity functions are always safe for replay because they are saved into the orchestration history.

Alternatively, a random number generator with a fixed seed value can be used directly in an orchestrator function. This approach is safe as long as the same sequence of numbers is generated for each orchestration replay.

#### Bindings

An orchestrator function must not use any bindings, including even the [orchestration client](durable-functions-bindings#orchestration-client) and [entity client](durable-functions-bindings#entity-client) bindings. Always use input and output bindings from within a client or activity function. This is important because orchestrator functions may be replayed multiple times, causing nondeterministic and duplicate I/O with external systems.

#### Static variables

Avoid using static variables in orchestrator functions because their values can change over time, resulting in nondeterministic runtime behavior. Instead, use constants, or limit the use of static variables to activity functions.

Note

Even outside of orchestrator functions, using static variables in Azure Functions can be problematic for a variety of reasons since there's no guarantee that static state will persist across multiple function executions. Static variables should be avoided except in very specific usecases, such as best-effort in-memory caching in activity or entity functions.

#### Environment variables

Do not use environment variables in orchestrator functions. Their values can change over time, resulting in nondeterministic runtime behavior. If an orchestrator function needs configuration that's defined in an environment variable, you must pass the configuration value into the orchestrator function as an input or as the return value of an activity function.

#### Network and HTTP

Use activity functions to make outbound network calls. If you need to make an HTTP call from your orchestrator function, you also can use the [durable HTTP APIs](durable-functions-http-features#consuming-http-apis).

#### Thread-blocking APIs

Blocking APIs like "sleep" can cause performance and scale problems for orchestrator functions and should be avoided. In the Azure Functions Consumption plan, they can even result in unnecessary execution time charges. Use alternatives to blocking APIs when they're available. For example, use [Durable timers](durable-functions-timers) to create delays that are safe for replay and don't count towards the execution time of an orchestrator function.

#### Async APIs

Orchestrator code must never start any async operation except those defined by the orchestration trigger's context object. For example, never use `Task.Run`

, `Task.Delay`

, and `HttpClient.SendAsync`

in .NET or `setTimeout`

and `setInterval`

in JavaScript. An orchestrator function should only schedule async work using Durable SDK APIs, like scheduling activity functions. Any other type of async invocations should be done inside activity functions.

#### Async JavaScript functions

Always declare JavaScript orchestrator functions as synchronous generator functions. You must not declare JavaScript orchestrator functions as `async`

because the Node.js runtime doesn't guarantee that asynchronous functions are deterministic.

#### Python coroutines

You must not declare Python orchestrator functions as coroutines. In other words, never declare Python orchestrator functions with the `async`

keyword because coroutine semantics do not align with the Durable Functions replay model. You must always declare Python orchestrator functions as generators, meaning that you should expect the `context`

API to use `yield`

instead of `await`

.

#### .NET threading APIs

The Durable Task Framework runs orchestrator code on a single thread and can't interact with any other threads. Running async continuations on a worker pool thread an orchestration's execution can result in nondeterministic execution or deadlocks. For this reason, orchestrator functions should almost never use threading APIs. For example, never use `ConfigureAwait(continueOnCapturedContext: false)`

in an orchestrator function. This ensures that task continuations run on the orchestrator function's original `SynchronizationContext`

.

Note

The Durable Task Framework attempts to detect accidental use of non-orchestrator threads in orchestrator functions. If it finds a violation, the framework throws a **NonDeterministicOrchestrationException** exception. However, this detection behavior won't catch all violations, and you shouldn't depend on it.

## Versioning

A durable orchestration might run continuously for days, months, years, or even [eternally](durable-functions-eternal-orchestrations). Any code updates made to Durable Functions apps that affect unfinished orchestrations might break the orchestrations' replay behavior. That's why it's important to plan carefully when making updates to code. For a more detailed description of how to version your code, see the [versioning article](durable-functions-versioning).

## Durable tasks

Note

This section describes internal implementation details of the Durable Task Framework. You can use durable functions without knowing this information. It is intended only to help you understand the replay behavior.

Tasks that can safely wait in orchestrator functions are occasionally referred to as *durable tasks*. The Durable Task Framework creates and manages these tasks. Examples are the tasks returned by `CallActivityAsync`

, `WaitForExternalEvent`

, and `CreateTimer`

in .NET orchestrator functions.

These durable tasks are internally managed by a list of `TaskCompletionSource`

objects in .NET. During replay, these tasks are created as part of orchestrator code execution. They're finished as the dispatcher enumerates the corresponding history events.

The tasks are executed synchronously using a single thread until all the history has been replayed. Durable tasks that aren't finished by the end of history replay have appropriate actions carried out. For example, a message might be enqueued to call an activity function.

This section's description of runtime behavior should help you understand why an orchestrator function can't use `await`

or `yield`

in a nondurable task. There are two reasons: the dispatcher thread can't wait for the task to finish, and any callback by that task might potentially corrupt the tracking state of the orchestrator function. Some runtime checks are in place to help detect these violations.

To learn more about how the Durable Task Framework executes orchestrator functions, consult the [Durable Task source code on GitHub](https://github.com/Azure/durabletask). In particular, see [TaskOrchestrationExecutor.cs](https://github.com/Azure/durabletask/blob/master/src/DurableTask.Core/TaskOrchestrationExecutor.cs) and [TaskOrchestrationContext.cs](https://github.com/Azure/durabletask/blob/master/src/DurableTask.Core/TaskOrchestrationContext.cs).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-disaster-recovery-geo-distribution -->

# Disaster recovery and geo-distribution in Durable Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft strives to ensure that Azure services are always available. However, unplanned service outages might happen. When your application requires resiliency, you should configure your app for geo-redundancy.

You should also have a disaster recovery plan in place for handling a regional service outage. An important part of a disaster recovery plan is being prepared to fail over to the secondary replicas of both your app and your storage account when the primary replicas become unavailable.

This article describes example scenarios for configuring disaster recovery and geo-distribution by using the Durable Functions feature of Azure Functions.

## Background

In Durable Functions, all state is persisted in Azure Storage by default. A [task hub](durable-functions-task-hubs) is a logical container for Azure Storage resources that are used for [orchestrations](durable-functions-types-features-overview#orchestrator-functions) and [entities](durable-functions-types-features-overview#entity-functions). Orchestrator, activity, and entity functions can interact with each other only when they belong to the same task hub. This article refers to task hubs when describing scenarios for keeping these Azure Storage resources highly available.

Orchestrations and entities can be triggered via [client functions](durable-functions-types-features-overview#client-functions) that are themselves triggered via HTTP or one of the other supported Azure Functions trigger types. Orchestrations and entities can also be triggered via [built-in HTTP APIs](durable-functions-http-features#built-in-http-apis). For simplicity, this article focuses on scenarios that involve Azure Storage and HTTP-based function triggers, along with options to increase availability and minimize downtime during disaster recovery. This article doesn't explicitly cover other trigger types, such as Azure Service Bus or Azure Cosmos DB triggers.

The scenarios in this article are based on active/passive configurations, which best support the usage of Azure Storage. This pattern consists of deploying a backup (passive) function app to a different region. [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) monitors the primary (active) function app for HTTP availability. It fails over to the backup function app when the primary app fails. For more information, see [Priority traffic-routing method](../../traffic-manager/traffic-manager-routing-methods#priority-traffic-routing-method).

## General considerations

Keep these considerations in mind when you're configuring an active/passive failover configuration for Durable Functions:

- The guidance in this article assumes that you're using the default
[Azure Storage provider](durable-functions-azure-storage-provider)for storing the Durable Functions runtime state. You can also configure alternate storage providers that store state elsewhere, such as in a SQL Server database. Alternate storage providers might require different disaster recovery and geo-distribution strategies. For more information, see[Durable Functions storage providers](durable-functions-storage-providers). - The proposed active/passive configuration ensures that a client can always trigger new orchestrations via HTTP. However, when two function apps share the same task hub in storage, some background storage transactions can be distributed between the apps. As a result of this distribution, this configuration can result in added egress costs for the secondary function app.
- The underlying storage account and task hub are both created in the primary region. The function apps share this storage account and task hub.
- All function apps that are redundantly deployed must share the same function access keys when they're activated via HTTP. The Azure Functions runtime exposes a
[management API](https://github.com/Azure/azure-functions-host/wiki/Key-management-API)that you can use to programmatically add, delete, and update function keys. You can also manage keys by using[Azure Resource Manager APIs](https://www.markheath.net/post/managing-azure-functions-keys-2).

## Scenario 1: Load-balanced compute with shared storage

To mitigate the possibility of downtime if your function app resources become unavailable, this scenario uses two function apps deployed to different regions. We recommend this scenario as a solution for failovers.

Traffic Manager is configured to detect problems in the primary function app and automatically redirect traffic to the function app in the secondary region. This function app shares the same Azure Storage account and task hub. The state of the function apps isn't lost, and work can resume normally. After health is restored to the primary region, Azure Traffic Manager starts routing requests to that function app automatically.

There are several benefits to using this deployment scenario:

- If the compute infrastructure fails, work can resume in the failover region without data loss.
- Traffic Manager takes care of the automatic failover to the healthy function app.
- Traffic Manager automatically re-establishes traffic to the primary function app after the outage ends.

### Scenario-specific considerations

If you deploy the function app by using a dedicated Azure App Service plan, replicating the compute infrastructure in the failover datacenter increases costs.

This scenario covers outages at the compute infrastructure, but the storage account continues to be the single point of failure for the function app. If an Azure Storage outage occurs, the application suffers downtime.

If the function app is failed over, latency increases because the app accesses its storage account across regions.

When the function app is in failover, it accesses the storage service in the original region. The network egress traffic can result in higher costs.

This scenario depends on Traffic Manager. A client application can take some time before it needs to again request the function app address from Traffic Manager. For more information, see

[How Traffic Manager works](../../traffic-manager/traffic-manager-how-it-works).Starting in version 2.3.0 of the Durable Functions extension, you can safely run two function apps at the same time with the same storage account and task hub configuration. The first app to start acquires an application-level blob lease that prevents other apps from stealing messages from the task hub queues. If this first app stops running, its lease expires. A second app can acquire the lease and begin to process task hub messages.

For extension versions before 2.3.0, function apps that are configured to use the same storage account process messages and update storage artifacts concurrently. This concurrent activity results in higher overall latencies and egress costs. If the primary and replica apps ever have different code deployed to them, even temporarily, orchestrations might also fail to run correctly because of orchestrator function inconsistencies across the two apps.

All apps that require geo-distribution for disaster recovery should use version 2.3.0 or later of the Durable Functions extension.


## Scenario 2: Load-balanced compute with regional storage or a regional durable task scheduler

The preceding scenario covers only failures limited to the compute infrastructure. An outage of the function app can also occur when either the storage service or the durable task scheduler fails.

To ensure continuous operation of Durable Functions, the second scenario deploys a dedicated storage account or a durable task scheduler in each region where function apps are hosted. We currently recommend this disaster recovery approach when you're using a durable task scheduler.

This approach adds improvements to the previous scenario:

**Regional state isolation**: Each function app is linked to its own regional storage account or durable task scheduler. If the function app fails, Traffic Manager redirects traffic to the secondary region. Because the function app in each region uses its local storage or durable task scheduler, Durable Functions can continue processing by using the local state.**No added latency on failover**: During a failover, a function app and state provider (storage account or durable task scheduler) are colocated, so there's no added latency in the failover region.**Resilience to state backing failures**: If the storage account or durable task scheduler in one region fails, Durable Functions fails in that region. The failure of Durable Functions triggers redirection to the secondary region. Because both compute and app state are isolated per region, Durable Functions in the failover region remains operational.

### Scenario-specific considerations

- If you deploy the function app by using a dedicated App Service plan, replicating the compute infrastructure in the failover datacenter increases costs.
- The current state isn't failed over. Existing orchestrations and entities are effectively paused and unavailable until the primary region recovers. Whether this tradeoff to preserving latency and minimizing egress costs is acceptable depends on the requirements of the application.

## Scenario 3: Load-balanced compute with shared GRS

This scenario is a modification of the first scenario (implementing a shared storage account). The main difference is that the storage account is created with geo-replication enabled.

This scenario provides the same functional advantages as the first scenario, but it also enables other data recovery advantages:

- Geo-redundant storage (GRS) and read-access GRS (RA-GRS) maximize availability for your storage account.
- If there's a regional outage of the Azure Storage service, you can
[manually initiate a failover to the secondary replica](../../storage/common/storage-initiate-account-failover). In extreme circumstances where a region is lost due to a disaster, Microsoft might initiate a regional failover. In this case, you don't need to take any action. - When a failover happens, the state of Durable Functions is preserved up to the last replication of the storage account. The replication typically occurs every few minutes.

For more information, see [Azure storage disaster recovery planning and failover](../../storage/common/storage-disaster-recovery-guidance).

### Scenario-specific considerations

- A failover to the replica might take some time. Until the failover finishes and Azure Storage DNS records are updated, the function app continues to be inaccessible.
- There's an increased cost for using geo-replicated storage accounts.
- GRS replication copies your data asynchronously. Some of the latest transactions might be lost because of the latency of the replication process.
- As described for the first scenario, we recommend that function apps deployed in this strategy use version 2.3.0 or later of the Durable Functions extension.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-zero-downtime-deployment -->

# Zero-downtime deployment for Durable Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [reliable execution model](durable-functions-orchestrations) of Durable Functions requires that orchestrations be deterministic, which creates an additional challenge to consider when you deploy updates. When a deployment contains changes to activity function signatures or orchestrator logic, in-flight orchestration instances fail. This situation is especially a problem for instances of long-running orchestrations, which might represent hours or days of work.

To prevent these failures from happening, you have several options:

- Delay your deployment until all running orchestration instances have completed.
- Use
[orchestration versioning](durable-functions-orchestration-versioning)to allow different versions of orchestrations to coexist (recommended). - Make sure that any running orchestration instances use the existing versions of your functions.

The following chart compares the four main strategies to achieve a zero-downtime deployment for Durable Functions:

| Strategy | When to use | Pros | Cons |
|---|---|---|---|
|

[breaking changes](durable-functions-versioning), especially those that need to support concurrent execution of different orchestration versions.Built-in feature requiring minimal configuration.

[Name-based versioning](#name-based-versioning)[breaking changes.](durable-functions-versioning)Code duplication.

[Status check with slot](#status-check-with-slot)Doesn't require additional function app management.

Requires periods of time when no orchestrations are running.

[Application routing](#application-routing)Could max out the number of function apps allowed by your subscription. The default is 100.

The remainder of this document describes these strategies in more detail.

Note

The descriptions for these zero-downtime deployment strategies assume you are using the default Azure Storage provider for Durable Functions. The guidance may not be appropriate if you are using a storage provider other than the default Azure Storage provider. For more information on the various storage provider options and how they compare, see the [Durable Functions storage providers](durable-functions-storage-providers) documentation.

## Orchestration versioning

The [orchestration versioning](durable-functions-orchestration-versioning) feature allows you to make breaking changes to orchestrations while avoiding downtime during deployments. This built-in feature enables different versions of orchestrations to coexist and execute concurrently without conflicts.

With orchestration versioning:

- Each orchestration instance gets a version permanently associated with it when created.
- Workers running newer orchestrator versions can continue executing older version instances.
- Workers running older orchestration versions
*can't*execute newer version instances. - Orchestrator functions can examine their version and branch execution accordingly.

This approach facilitates rolling upgrades where workers running different versions of your application can coexist safely. It's the recommended strategy for applications that need to support breaking changes while maintaining zero-downtime deployments.
The orchestration versioning feature is ** backend agnostic**, so you can leverage it regardless of what storage backend your Durable Function app is using.
For detailed configuration and implementation guidance, see

[Orchestration versioning in Durable Functions](durable-functions-orchestration-versioning).

## Name-based versioning

Define new versions of your functions and leave the old versions in your function app. As you can see in the diagram, a function's version becomes part of its name. Because previous versions of functions are preserved, in-flight orchestration instances can continue to reference them. Meanwhile, requests for new orchestration instances call for the latest version, which your orchestration client function can reference from an app setting.

In this strategy, every function must be copied, and its references to other functions must be updated. You can make it easier by writing a script. Here's a [sample project](https://github.com/TsuyoshiUshio/DurableVersioning) with a migration script.

Note

This strategy uses deployment slots to avoid downtime during deployment. For more detailed information about how to create and use new deployment slots, see [Azure Functions deployment slots](../functions-deployment-slots).

## Status check with slot

While the current version of your function app is running in your production slot, deploy the new version of your function app to your staging slot. Before you swap your production and staging slots, check to see if there are any running orchestration instances. After all orchestration instances are complete, you can do the swap. This strategy works when you have predictable periods when no orchestration instances are in flight. This is the best approach when your orchestrations aren't long-running and when your orchestration executions don't frequently overlap.

### Function app configuration

Use the following procedure to set up this scenario.

[Add deployment slots](../functions-deployment-slots#add-a-slot)to your function app for staging and production.For each slot, set the

[AzureWebJobsStorage application setting](../functions-app-settings#azurewebjobsstorage)to the connection of a shared storage account. This storage account connection is used by the Azure Functions runtime to securely store the[functions' access keys](../function-keys-how-to). For the highest level of security, you should use a[managed identity connection](../../app-service/overview-managed-identity)to your storage account.For each slot, create a new app setting, for example,

`DurableManagementStorage`

. Set its value to the connection string of different storage accounts. These storage accounts are used by the Durable Functions extension for[reliable execution](durable-functions-orchestrations). Use a separate storage account for each slot. Don't mark this setting as a deployment slot setting. Again, managed identity-based connections are the most secure.In your function app's

[host.json file's durableTask section](durable-functions-bindings#durable-functions-settings-in-hostjson), specify`connectionStringName`

(Durable 2.x) or`azureStorageConnectionStringName`

(Durable 1.x) as the name of the app setting you created in step 3.

The following diagram shows the described configuration of deployment slots and storage accounts. In this potential predeployment scenario, version 2 of a function app is running in the production slot, while version 1 remains in the staging slot.

### host.json examples

The following JSON fragments are examples of the connection string setting in the *host.json* file.

#### Functions 2.0

```
{
"version": 2.0,
"extensions": {
"durableTask": {
"hubName": "MyTaskHub",
"storageProvider": {
"connectionStringName": "DurableManagementStorage"
}
}
}
}
```


#### Functions 1.x

```
{
"durableTask": {
"azureStorageConnectionStringName": "DurableManagementStorage"
}
}
```


### CI/CD pipeline configuration

Configure your CI/CD pipeline to deploy only when your function app has no pending or running orchestration instances. When you're using Azure Pipelines, you can create a function that checks for these conditions, as in the following example:

```
[FunctionName("StatusCheck")]
public static async Task<IActionResult> StatusCheck(
[HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestMessage req,
[DurableClient] IDurableOrchestrationClient client,
ILogger log)
{
var runtimeStatus = new List<OrchestrationRuntimeStatus>();
runtimeStatus.Add(OrchestrationRuntimeStatus.Pending);
runtimeStatus.Add(OrchestrationRuntimeStatus.Running);
var result = await client.ListInstancesAsync(new OrchestrationStatusQueryCondition() { RuntimeStatus = runtimeStatus }, CancellationToken.None);
return (ActionResult)new OkObjectResult(new { HasRunning = result.DurableOrchestrationState.Any() });
}
```


Next, configure the staging gate to wait until no orchestrations are running. For more information, see [Release deployment control using gates](/en-us/azure/devops/pipelines/release/approvals/gates)

Azure Pipelines checks your function app for running orchestration instances before your deployment starts.

Now the new version of your function app should be deployed to the staging slot.

Finally, swap slots.

Application settings that aren't marked as deployment slot settings are also swapped, so the version 2 app keeps its reference to storage account A. Because orchestration state is tracked in the storage account, any orchestrations running on the version 2 app continue to run in the new slot without interruption.

To use the same storage account for both slots, you can change the names of your task hubs. In this case, you need to manage the state of your slots and your app's HubName settings. To learn more, see [Task hubs in Durable Functions](durable-functions-task-hubs).

## Application routing

This strategy is the most complex. However, it can be used for function apps that don't have time between running orchestrations.

For this strategy, you must create an *application router* in front of your Durable Functions. This router can be implemented with Durable Functions. The router has the responsibility to:

- Deploy the function app.
- Manage the version of Durable Functions.
- Route orchestration requests to function apps.

The first time an orchestration request is received, the router does the following tasks:

- Creates a new function app in Azure.
- Deploys your function app's code to the new function app in Azure.
- Forwards the orchestration request to the new app.

The router manages the state of which version of your app's code is deployed to which function app in Azure.

The router directs deployment and orchestration requests to the appropriate function app based on the version sent with the request. It ignores the patch version.

When you deploy a new version of your app without a breaking change, you can increment the patch version. The router deploys to your existing function app and sends requests for the old and new versions of the code, which are routed to the same function app.

When you deploy a new version of your app with a breaking change, you can increment the major or minor version. Then the application router creates a new function app in Azure, deploys to it, and routes requests for the new version of your app to it. In the following diagram, running orchestrations on the 1.0.1 version of the app keep running, but requests for the 1.1.0 version are routed to the new function app.

The router monitors the status of orchestrations on the 1.0.1 version and removes apps after all orchestrations are finished.

### Tracking store settings

Each function app should use separate scheduling queues, possibly in separate storage accounts. If you want to query all orchestrations instances across all versions of your application, you can share instance and history tables across your function apps. You can share tables by configuring the `trackingStoreConnectionStringName`

and `trackingStoreNamePrefix`

settings in the [host.json settings](durable-functions-bindings#host-json) file so that they all use the same values.

For more information, see [Manage instances in Durable Functions in Azure](durable-functions-instance-management).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-mssql-container-apps-hosting -->

# Host a Durable Functions app in Azure Container Apps (.NET isolated)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides integrated support for developing, deploying, and managing containerized Function Apps on Azure Container Apps. Use Azure Container Apps for your Functions apps when you need to run in the same environment as other microservices, APIs, websites, workflows, or any container hosted programs. Learn more about [running Azure Functions in Container Apps](../../container-apps/functions-overview).

Note

While Durable Functions supports several [storage providers](durable-functions-storage-providers) or *backends*, autoscaling apps hosted in Azure Container Apps is only available with the [Microsoft SQL (MSSQL) backend](../../container-apps/functions-overview#event-driven-scaling). If another backend is used, you have to set minimum replica count to greater than zero.

In this article, you learn how to:

- Create a Docker image from a local Durable Functions project.
- Create an Azure Container App and related resources.
- Deploy the image to the Azure Container App and set up authentication.

## Prerequisites

[Visual Studio Code](https://code.visualstudio.com/download)installed.[.NET 8.0 SDK](https://dotnet.microsoft.com/download).[Docker](https://docs.docker.com/install/)and[Docker ID](https://hub.docker.com/signup)[Azure CLI](/en-us/cli/azure/install-azure-cli)[version 2.47](/en-us/cli/azure/release-notes-azure-cli#april-21-2020)or later.[Azure Functions Core Tools](../functions-run-local)- Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - An HTTP test tool that keeps your data secure. For more information, see
[HTTP test tools](../functions-develop-local#http-test-tools).

## Create a local Durable Functions project

In Visual Studio Code, [create a .NET isolated Durable Functions project configured to use the MSSQL backend](quickstart-mssql).

[Test the app locally](quickstart-mssql#test-locally) and return to this article.

## Add Docker-related files

Create a *Dockerfile* in the project root that describes the minimum required environment to run the function app in a container.

In the project root directory, create a new file named

*Dockerfile*.Copy/paste the following content into the Dockerfile.

`FROM mcr.microsoft.com/dotnet/sdk:8.0 AS installer-env COPY . /src/dotnet-function-app RUN cd /src/dotnet-function-app && \ mkdir -p /home/site/wwwroot && \ dotnet publish *.csproj --output /home/site/wwwroot # To enable ssh & remote debugging on app service change the base image to the one below # FROM mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0-appservice FROM mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0 ENV AzureWebJobsScriptRoot=/home/site/wwwroot \ AzureFunctionsJobHost__Logging__Console__IsEnabled=true COPY --from=installer-env ["/home/site/wwwroot", "/home/site/wwwroot"]`

Save the file.

Add a

*.dockerignore*file with the following content:`local.settings.json`

Save the

*.dockerignore*file.

## Build the container image

Build the Docker image. Find the complete list of supported base images for Azure Functions in the [Azure Functions Base by Microsoft | Docker Hub](https://hub.docker.com/_/microsoft-azure-functions-base)

Start the Docker daemon.

Sign in to Docker with the

command.`docker login`

When prompted, log in with your username and password. A "Login Succeeded" message confirms that you're signed in.

Navigate to your project root directory.

Run the following command to build the image, replacing

`<DOCKER_ID>`

with your Docker Hub account ID:`dockerId=<DOCKER_ID> imageName=IMAGE_NAME> imageVersion=v1.0.0 docker build --tag $dockerId/$imageName:$imageVersion .`

Note

If you're running on an M-series Mac, use

`--platform linux/amd64`

instead.Push the image to Docker:

`docker push $dockerId/$imageName:$imageVersion`

Depending on network speed, the initial image push might take a few minutes. While you're waiting, proceed to the next section.


## Create Azure resources

Create the Azure resources necessary for running Durable Functions on a container app.

**Azure resource group:**Resource group containing all created resources.**Azure Container App environment:**Environment hosting the container app.**Azure Container App:**Image containing the Durable Functions app is deployed to this app.**Azure Storage Account:**Required by the function app to store app-related data, such as application code.

### Initial set up

In a new terminal, log in to your Azure subscription:

`az login az account set -s <subscription_name>`

Run the required commands to set up the Azure Container Apps CLI extension:

`az upgrade az extension add --name containerapp --upgrade az provider register --namespace Microsoft.App az provider register --namespace Microsoft.OperationalInsights`


### Create container app and related resources

A [workload profile](../functions-container-apps-hosting#hosting-and-workload-profiles) determines the amount of compute and memory resources available to the container apps deployed in an environment. Create a **Consumption workload profile** for scale-to-zero support and pay-per-use.

Set the environment variables.

`location=<REGION> resourceGroup=<RESOURCE_GROUP_NAME> storage=<STORAGE_NAME> containerAppEnv=<CONTAINER_APP_ENVIRONMNET_NAME> functionApp=<APP_NAME> vnet=<VNET_NAME>`

Create a resource group.

`az group create --name $resourceGroup --location $location`

Create the container app environment.

`az containerapp env create \ --enable-workload-profiles \ --resource-group $resourceGroup \ --name $containerAppEnv \ --location $location \`

Create a container app based on the Durable Functions image.

`az containerapp create --resource-group $resourceGroup \ --name $functionApp \ --environment $containerAppEnv \ --image $dockerId/$imageName:$imageVersion \ --ingress external \ --kind functionapp \ --query properties.outputs.fqdn`

Make note of the app URL, which should look similar to

`https://<APP_NAME>.<ENVIRONMENT_IDENTIFIER>.<REGION>.azurecontainerapps.io`

.

### Create databases

Create an Azure Storage account, which is required by the function app.

`az storage account create --name $storage --location $location --resource-group $resourceGroup --sku Standard_LRS`

In the Azure portal,

[create an Azure SQL database](/en-us/azure/azure-sql/database/single-database-create-quickstart)to persist state information. During creation:- Enable Azure services and resources to access this server (under
**Networking**) - Set the value for
**Database collation**(under**Additional settings**) to`Latin1_General_100_BIN2_UTF8`

.

- Enable Azure services and resources to access this server (under

Note

Refrain from enabling the **Allow Azure services and resources to access this server** setting for production scenarios. Production applications should implement more secure approaches, such as stronger firewall restrictions or virtual network configurations.

### Configure identity-based authentication

Managed identities make your app more secure by eliminating secrets from your app, such as credentials in the connection strings. While you can choose between [system-assigned and user-assigned managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview), user-assigned managed identity is recommended, as it's not tied to the app lifecycle.

In this section, you set up **user-assigned managed identity** for Azure Storage.

Set the environment variables.

`subscription=<SUBSCRIPTION_ID> identity=<IDENTITY_NAME>`

Create a managed identity resource.

`echo "Creating $identity" az identity create -g $resourceGroup -n $identity --location "$location"`

Assign the user identity to the container app.

`echo "Assigning $identity to app" az containerapp identity assign --resource-group $resourceGroup --name $functionApp --user-assigned $identity`

Set the scope of the role-based access control (RBAC) permissions.

`scope="/subscriptions/$subscription/resourceGroups/$resourceGroup/providers/Microsoft.Storage/storageAccounts/$storage"`

Get the user identity's

`clientId`

.`# Get the identity's ClientId clientId=$(az identity show --name $identity --resource-group $resourceGroup --query 'clientId' --output tsv)`

Assign the role

**Storage Blob Data Owner**role for access to the storage account.`echo "Assign Storage Blob Data Owner role to identity" az role assignment create --assignee "$clientId" --role "Storage Blob Data Owner" --scope "$scope"`


### Set up app settings

Note

Authenticating to the MSSQL database using managed identity isn't supported when hosting a Durable Functions app in Azure Container Apps. For now, this guide authenticates using connection strings.

From the SQL database resource in the Azure portal, navigate to

**Settings**>**Connection strings**to find the connection string.The connection string should have a format similar to:

`dbserver=<SQL_SERVER_NAME> sqlDB=<SQL_DB_NAME> username=<DB_USER_LOGIN> password=<DB_USER_PASSWORD> connStr="Server=tcp:$dbserver.database.windows.net,1433;Initial Catalog=$sqlDB;Persist Security Info=False;User ID=$username;Password=$password;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;"`

If you forget the password from the previous database creation step, you can reset it on the SQL server resource.

Store the SQL database's connection string as a

[secret](../../container-apps/manage-secrets)called*sqldbconnection*in the container app.`az containerapp secret set \ --resource-group $resourceGroup \ --name $functionApp \ --secrets sqldbconnection=$connStr`

Add the following settings to the app:

`az containerapp update \ -n $functionApp \ -g $resourceGroup \ --set-env-vars SQLDB_Connection=secretref:sqldbconnection \ AzureWebJobsStorage__accountName=$storage \ AzureWebJobsStorage__clientId=$clientId \ AzureWebJobsStorage__credential=managedidentity \ FUNCTIONS_WORKER_RUNTIME=dotnet-isolated`


## Test locally

Use an HTTP test tool to send a

`POST`

request to the HTTP trigger endpoint, which should be similar to:`https://<APP NAME>.<ENVIRONMENT_IDENTIFIER>.<REGION>.azurecontainerapps.io/api/DurableFunctionsOrchestrationCSharp1_HttpStart`

The response is the HTTP function's initial result letting you know that the Durable Functions orchestration started successfully. While the response includes a few useful URLs, it doesn't yet display the orchestration's end result.

Copy/paste the URL value for

`statusQueryGetUri`

into your browser's address bar and execute. Alternatively, you can continue to use the HTTP test tool to issue the`GET`

request.The request queries the orchestration instance for the status. You should see that the instance finished and the outputs or results of the Durable Functions app.

`{ "name":"HelloCities", "instanceId":"7f99f9474a6641438e5c7169b7ecb3f2", "runtimeStatus":"Completed", "input":null, "customStatus":null, "output":"Hello, Tokyo! Hello, London! Hello, Seattle!", "createdTime":"2023-01-31T18:48:49Z", "lastUpdatedTime":"2023-01-31T18:48:56Z" }`


## Next steps

Learn more about:

[Azure Container Apps hosting of Azure Functions](../../container-apps/functions-overview).[MSSQL storage provider](https://microsoft.github.io/durabletask-mssql/)architecture, configuration, and workload behavior.- The Azure-managed storage backend,
[Durable Task Scheduler](durable-task-scheduler/durable-task-scheduler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-phone-verification -->

# Human interaction in Durable Functions - Phone verification sample

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This sample demonstrates how to build a [Durable Functions](durable-functions-overview) orchestration that involves human interaction. Whenever a real person is involved in an automated process, the process must be able to send notifications to the person and receive responses asynchronously. It must also allow for the possibility that the person is unavailable. (This last part is where timeouts become important.)

This sample implements an SMS-based phone verification system. These types of flows are often used when verifying a customer's phone number or for multi-factor authentication (MFA). It is a powerful example because the entire implementation is done using a couple small functions. No external data store, such as a database, is required.

Note

Version 4 of the Node.js programming model for Azure Functions is generally available. The v4 model is designed to provide a more flexible and intuitive experience for JavaScript and TypeScript developers. For more information about the differences between v3 and v4, see the [migration guide](../functions-node-upgrade-v4).

In the following code snippets, JavaScript (PM4) denotes programming model v4, the new experience.

## Prerequisites

## Scenario overview

Phone verification is used to verify that end users of your application are not spammers and that they are who they say they are. Multi-factor authentication is a common use case for protecting user accounts from hackers. The challenge with implementing your own phone verification is that it requires a **stateful interaction** with a human being. An end user is typically provided some code (for example, a 4-digit number) and must respond **in a reasonable amount of time**.

Ordinary Azure Functions are stateless (as are many other cloud endpoints on other platforms), so these types of interactions involve explicitly managing state externally in a database or some other persistent store. In addition, the interaction must be broken up into multiple functions that can be coordinated together. For example, you need at least one function for deciding on a code, persisting it somewhere, and sending it to the user's phone. Additionally, you need at least one other function to receive a response from the user and somehow map it back to the original function call in order to do the code validation. A timeout is also an important aspect to ensure security. It can get fairly complex quickly.

The complexity of this scenario is greatly reduced when you use Durable Functions. As you will see in this sample, an orchestrator function can manage the stateful interaction easily and without involving any external data stores. Because orchestrator functions are *durable*, these interactive flows are also highly reliable.

## Configuring Twilio integration

This sample involves using the [Twilio](https://www.twilio.com/) service to send SMS messages to a mobile phone. Azure Functions already has support for Twilio via the [Twilio binding](../functions-bindings-twilio), and the sample uses that feature.

The first thing you need is a Twilio account. You can create one free at [https://www.twilio.com/try-twilio](https://www.twilio.com/try-twilio). Once you have an account, add the following three **app settings** to your function app.

| App setting name | Value description |
|---|---|
TwilioAccountSid |
The SID for your Twilio account |
TwilioAuthToken |
The Auth token for your Twilio account |
TwilioPhoneNumber |
The phone number associated with your Twilio account. This is used to send SMS messages. |

## The functions

This article walks through the following functions in the sample app:

`E4_SmsPhoneVerification`

: An[orchestrator function](durable-functions-bindings#orchestration-trigger)that performs the phone verification process, including managing timeouts and retries.`E4_SendSmsChallenge`

: An[activity function](durable-functions-bindings#activity-trigger)that sends a code via text message.

Note

The `HttpStart`

function in the [sample app and the quickstart](#prerequisites) acts as [Orchestration client](durable-functions-bindings#orchestration-client) which triggers the orchestrator function.

### E4_SmsPhoneVerification orchestrator function

```
[FunctionName("E4_SmsPhoneVerification")]
public static async Task<bool> Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
string phoneNumber = context.GetInput<string>();
if (string.IsNullOrEmpty(phoneNumber))
{
throw new ArgumentNullException(
nameof(phoneNumber),
"A phone number input is required.");
}
int challengeCode = await context.CallActivityAsync<int>(
"E4_SendSmsChallenge",
phoneNumber);
using (var timeoutCts = new CancellationTokenSource())
{
// The user has 90 seconds to respond with the code they received in the SMS message.
DateTime expiration = context.CurrentUtcDateTime.AddSeconds(90);
Task timeoutTask = context.CreateTimer(expiration, timeoutCts.Token);
bool authorized = false;
for (int retryCount = 0; retryCount <= 3; retryCount++)
{
Task<int> challengeResponseTask =
context.WaitForExternalEvent<int>("SmsChallengeResponse");
Task winner = await Task.WhenAny(challengeResponseTask, timeoutTask);
if (winner == challengeResponseTask)
{
// We got back a response! Compare it to the challenge code.
if (challengeResponseTask.Result == challengeCode)
{
authorized = true;
break;
}
}
else
{
// Timeout expired
break;
}
}
if (!timeoutTask.IsCompleted)
{
// All pending timers must be complete or canceled before the function exits.
timeoutCts.Cancel();
}
return authorized;
}
}
```


Note

It may not be obvious at first, but this orchestrator does not violate the [deterministic orchestration constraint](durable-functions-code-constraints). It is deterministic because the `CurrentUtcDateTime`

property is used to calculate the timer expiration time, and it returns the same value on every replay at this point in the orchestrator code. This behavior is important to ensure that the same `winner`

results from every repeated call to `Task.WhenAny`

.

Once started, this orchestrator function does the following:

- Gets a phone number to which it will
*send*the SMS notification. - Calls
**E4_SendSmsChallenge**to send an SMS message to the user and returns back the expected 4-digit challenge code. - Creates a durable timer that triggers 90 seconds from the current time.
- In parallel with the timer, waits for an
**SmsChallengeResponse**event from the user.

The user receives an SMS message with a four-digit code. They have 90 seconds to send that same four-digit code back to the orchestrator function instance to complete the verification process. If they submit the wrong code, they get an additional three tries to get it right (within the same 90-second window).

Warning

It's important to [cancel timers](durable-functions-timers) if you no longer need them to expire, as in the example above when a challenge response is accepted.

## E4_SendSmsChallenge activity function

The **E4_SendSmsChallenge** function uses the Twilio binding to send the SMS message with the four-digit code to the end user.

```
[FunctionName("E4_SendSmsChallenge")]
public static int SendSmsChallenge(
[ActivityTrigger] string phoneNumber,
ILogger log,
[TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "%TwilioPhoneNumber%")]
out CreateMessageOptions message)
{
// Get a random number generator with a random seed (not time-based)
var rand = new Random(Guid.NewGuid().GetHashCode());
int challengeCode = rand.Next(10000);
log.LogInformation($"Sending verification code {challengeCode} to {phoneNumber}.");
message = new CreateMessageOptions(new PhoneNumber(phoneNumber));
message.Body = $"Your verification code is {challengeCode:0000}";
return challengeCode;
}
```


Note

You must first install the `Microsoft.Azure.WebJobs.Extensions.Twilio`

Nuget package for Functions to run the sample code. Don't also install the main [Twilio nuget package](https://www.nuget.org/packages/Twilio/) because this can cause versioning problems that result in build errors.

## Run the sample

Using the HTTP-triggered functions included in the sample, you can start the orchestration by sending the following HTTP POST request:

```
POST http://{host}/orchestrators/E4_SmsPhoneVerification
Content-Length: 14
Content-Type: application/json
"+1425XXXXXXX"
```


```
HTTP/1.1 202 Accepted
Content-Length: 695
Content-Type: application/json; charset=utf-8
Location: http://{host}/runtime/webhooks/durabletask/instances/741c65651d4c40cea29acdd5bb47baf1?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
{"id":"741c65651d4c40cea29acdd5bb47baf1","statusQueryGetUri":"http://{host}/runtime/webhooks/durabletask/instances/741c65651d4c40cea29acdd5bb47baf1?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}","sendEventPostUri":"http://{host}/runtime/webhooks/durabletask/instances/741c65651d4c40cea29acdd5bb47baf1/raiseEvent/{eventName}?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}","terminatePostUri":"http://{host}/runtime/webhooks/durabletask/instances/741c65651d4c40cea29acdd5bb47baf1/terminate?reason={text}&taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}"}
```


The orchestrator function receives the supplied phone number and immediately sends it an SMS message with a randomly generated 4-digit verification code — for example, *2168*. The function then waits 90 seconds for a response.

To reply with the code, you can use [ RaiseEventAsync (.NET) or raiseEvent (JavaScript/TypeScript)](durable-functions-instance-management) inside another function or invoke the


**sendEventPostUri**HTTP POST webhook referenced in the 202 response above, replacing

`{eventName}`

with the name of the event, `SmsChallengeResponse`

:```
POST http://{host}/runtime/webhooks/durabletask/instances/741c65651d4c40cea29acdd5bb47baf1/raiseEvent/SmsChallengeResponse?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
Content-Length: 4
Content-Type: application/json
2168
```


If you send this before the timer expires, the orchestration completes and the `output`

field is set to `true`

, indicating a successful verification.

```
GET http://{host}/runtime/webhooks/durabletask/instances/741c65651d4c40cea29acdd5bb47baf1?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
```


```
HTTP/1.1 200 OK
Content-Length: 144
Content-Type: application/json; charset=utf-8
{"runtimeStatus":"Completed","input":"+1425XXXXXXX","output":true,"createdTime":"2017-06-29T19:10:49Z","lastUpdatedTime":"2017-06-29T19:12:23Z"}
```


If you let the timer expire, or if you enter the wrong code four times, you can query for the status and see a `false`

orchestration function output, indicating that phone verification failed.

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 145
{"runtimeStatus":"Completed","input":"+1425XXXXXXX","output":false,"createdTime":"2017-06-29T19:20:49Z","lastUpdatedTime":"2017-06-29T19:22:23Z"}
```


## Next steps

This sample has demonstrated some of the advanced capabilities of Durable Functions, notably `WaitForExternalEvent`

and `CreateTimer`

APIs. You've seen how these can be combined with `Task.WaitAny`

(C#)/`context.df.Task.any`

(JavaScript/TypeScript)/`context.task_any`

(Python) to implement a reliable timeout system, which is often useful for interacting with real people. You can learn more about how to use Durable Functions by reading a series of articles that offer in-depth coverage of specific topics.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-versions -->

# Durable Functions versions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

*Durable Functions* is an extension of [Azure Functions](../functions-overview) and [Azure WebJobs](../../app-service/webjobs-create) that lets you write stateful functions in a serverless environment. The extension manages state, checkpoints, and restarts for you. If you aren't already familiar with Durable Functions, see the [overview documentation](durable-functions-overview).

## Microsoft.Azure.WebJobs.Extensions.DurableTask v3.x

This section introduces the new [Microsoft.Azure.WebJobs.Extensions.DurableTask v3](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask/3.0.0) package (referred to as WebJobs.Extensions.DurableTask in subsequent sections) and provides details on its updates and changes. This update is only considered a breaking-change for customers running Durable C# apps that use the [in-process model](../functions-dotnet-class-library).

Note

The Durable Functions .NET out-of-process package, Microsoft.Azure.Functions.Worker.Extensions.DurableTask, references Microsoft.Azure.WebJobs.Extensions.DurableTask as its underlying assembly. Thus, this update also applies to Microsoft.Azure.Functions.Worker.Extensions.DurableTask, starting from version [1.2.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask/1.2.0).

### New Azure Storage SDK

By default, Durable Functions use Azure Storage as a storage backend to durably save application state. In WebJobs.Extensions.DurableTask v3, the Azure Storage backend was upgraded to use the latest versions of the Azure Storage SDKs: [Azure.Data.Tables](https://www.nuget.org/packages/Azure.Data.Tables), [Azure.Storage.Blobs](https://www.nuget.org/packages/Azure.Storage.Blobs), and [Azure.Storage.Queues](https://www.nuget.org/packages/Azure.Storage.Queues). The new Azure Storage SDKs are more secured and offer enhanced support for Managed Identity. They also offer better performance, more efficient data handling, and other latest storage features.

### Improved cost efficiency for the Azure Storage backend

In the [Azure Storage backend](durable-functions-azure-storage-provider), the Partition Manager is responsible for distributing [partitions/control queues](durable-functions-azure-storage-provider#control-queues) among workers. The WebJobs.Extensions.DurableTask v3 package uses Partition Manager V3 by default, which is a new design that leverages Azure Tables to manage partition assignments instead of Azure Blob leases. This design can significantly reduce storage costs while making debugging easier. When Partition Manager V3 is used, [a new table](durable-functions-azure-storage-provider#partitions-table), named `Partitions`

, is created in your storage account, allowing you to easily check the partition information.

### Removed support for the Functions v1 runtime

WebJobs.Extensions.DurableTask v3 no longer supports version 1.x of the Azure Functions runtime, support for which is scheduled to end in [September 2026](https://azure.microsoft.com/updates?id=support-for-the-1x-version-of-azure-functions-ends-14-september-2026). If you must use Functions runtime v1, please use a Durable Functions extension version lower than *v2.11.0*. Keep in mind that when the scheduled end of support comes, Durable Functions will drop its support for runtime v1 as well.

### .NET Framework Update

WebJobs.Extensions.DurableTask v3 updates the .NET framework from .NET Core 3.1 to .NET 6, offering improved performance and enhanced compatibility with modern .NET features and libraries. This update aligns with future releases of the Azure Functions extension bundles.

### Migration from WebJobs.Extensions.DurableTask v2.x to v3.x

Migration from WebJobs.Extensions.DurableTask v2.x to v3.x is designed to be straightforward with no code changes required, as the changes are in the background. Simply update your dependencies to start taking advantage of the new features and improvements in v3.x.

- For .NET in-process users:
Update to
[Microsoft.Azure.WebJobs.Extensions.DurableTask version 3.0.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask/3.0.0)or later. - For .NET isolated users:
Update to
[Microsoft.Azure.Functions.Worker.Extensions.DurableTask version 1.2.0](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask/1.2.0)or later. - For users of other languages with extension bundles:
Support for Durable Functions v3 at Extension Bundles will be available starting from version
[4.22.0](https://github.com/Azure/azure-functions-extension-bundles/releases).

Note

WebJobs.Extensions.DurableTask v3 uses the latest version of the Azure Storage SDK, which has a different text encoding (Base64) when compared to the one used in v2 (UTF-8). If you need to downgrade from v3.x to v2.x, to ensure backward compatibility, use at least ** v2.13.5**. For .NET out-of-process users with Microsoft.Azure.Functions.Worker.Extensions.DurableTask, downgrade to

**or higher if reverting from v1.2.x or higher.**

[v1.1.5](https://github.com/Azure/azure-functions-durable-extension/releases/tag/v1.1.5Worker.Extensions.DurableTask)### Support and Maintenance of v2.x

WebJobs.Extensions.DurableTask v2.x continues to receive security updates and bug fixes, ensuring that your existing applications remain secure and stable. However, all new features and enhancements are added exclusively to v3.x. Because of this, you should upgrade to WebJobs.Extensions.DurableTask v3 as soon as you can to take advantage of the latest capabilities and ongoing improvements.

## New features in Microsoft.Azure.WebJobs.Extensions.DurableTask v2.x

This section describes the features of Durable Functions that are added in version 2.x.

Note

This section does not apply to Durable Functions in dotnet isolated worker. For that, see [durable functions isolated process overview](durable-functions-dotnet-isolated-overview).

### Durable entities

In Durable Functions 2.x, we introduced a new [entity functions](durable-functions-entities) concept.

Entity functions define operations for reading and updating small pieces of state, known as *durable entities*. Like orchestrator functions, entity functions are functions with a special trigger type, *entity trigger*. Unlike orchestrator functions, entity functions don't have any specific code constraints. Entity functions also manage state explicitly rather than implicitly representing state via control flow.

To learn more, see the [durable entities](durable-functions-entities) article.

### Durable HTTP

In Durable Functions 2.x, we introduced a new [Durable HTTP](durable-functions-http-features#consuming-http-apis) feature that allows you to:

- Call HTTP APIs directly from orchestration functions (with some documented limitations).
- Implement automatic client-side HTTP 202 status polling.
- Built-in support for
[Azure Managed Identities](../../active-directory/managed-identities-azure-resources/overview).

To learn more, see the [HTTP features](durable-functions-http-features#consuming-http-apis) article.

## Migrate from 1.x to 2.x

This section describes how to migrate your existing version 1.x Durable Functions to version 2.x to take advantage of the new features.

### Upgrade the extension

Install the latest 2.x version of the Durable Functions bindings extension in your project.

#### JavaScript, Python, and PowerShell

Durable Functions 2.x is available starting in version 2.x of the [Azure Functions extension bundle](../extension-bundles).

Python support in Durable Functions requires Durable Functions 2.x or greater.

To update the extension bundle version in your project, open host.json and update the `extensionBundle`

section to use version 4.x (`[4.*, 5.0.0)`

).

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


Note

If Visual Studio Code is not displaying the correct templates after you change the extension bundle version, reload the window by running the *Developer: Reload Window* command (`Ctrl+R` on Windows and Linux, `Command+R` on macOS).

#### Java

Durable Functions 2.x is available starting in version 4.x of the [Azure Functions extension bundle](../extension-bundles). You must use the Azure Functions 4.0 runtime to execute Java functions.

To update the extension bundle version in your project, open host.json and update the `extensionBundle`

section to use version 4.x (`[4.*, 5.0.0)`

).

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


#### .NET

Update your .NET project to use the latest version of the [Durable Functions bindings extension](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask).

See [Register Azure Functions binding extensions](../functions-develop-vs?tabs=in-process#add-bindings) for more information.

### Update your code

Durable Functions 2.x introduces several breaking changes. Durable Functions 1.x applications aren't compatible with Durable Functions 2.x without code changes. This section lists some of the changes you must make when upgrading your version 1.x functions to 2.x.

#### Host.json schema

Durable Functions 2.x uses a new host.json schema. The main changes from 1.x include:

`"storageProvider"`

(and the`"azureStorage"`

subsection) for storage-specific configuration.`"tracing"`

for tracing and logging configuration.`"notifications"`

(and the`"eventGrid"`

subsection) for Event Grid notification configuration.

See the [Durable Functions host.json reference documentation](durable-functions-bindings#durable-functions-2-0-host-json) for details.

#### Default task hub name changes

In version 1.x, if a task hub name wasn't specified in host.json, it was defaulted to "DurableFunctionsHub". In version 2.x, the default task hub name is now derived from the name of the function app. Because of this, if you haven't specified a task hub name when upgrading to 2.x, your code will be operating with new task hub, and all in-flight orchestrations will no longer have an application processing them. To work around this, you can either explicitly set your task hub name to the v1.x default of "DurableFunctionsHub", or you can follow our [zero-downtime deployment guidance](durable-functions-zero-downtime-deployment) for details on how to handle breaking changes for in-flight orchestrations.

#### Public interface changes (.NET only)

In version 1.x, the various *context* objects supported by Durable Functions have abstract base classes intended for use in unit testing. As part of Durable Functions 2.x, these abstract base classes are replaced with interfaces.

The following table represents the main changes:

| 1.x | 2.x |
|---|---|
`DurableOrchestrationClientBase` |
`IDurableOrchestrationClient` or `IDurableClient` |
`DurableOrchestrationContext` or `DurableOrchestrationContextBase` |
`IDurableOrchestrationContext` |
`DurableActivityContext` or `DurableActivityContextBase` |
`IDurableActivityContext` |
`OrchestrationClientAttribute` |
`DurableClientAttribute` |

In the case where an abstract base class contained virtual methods, these virtual methods have been replaced by extension methods defined in `DurableContextExtensions`

.

#### function.json changes

In Durable Functions 1.x, the orchestration client binding uses a `type`

of `orchestrationClient`

. Version 2.x uses `durableClient`

instead.

#### Raise event changes

In Durable Functions 1.x, calling the [raise event](durable-functions-external-events#send-events) API and specifying an instance that didn't exist resulted in a silent failure. Starting in 2.x, raising an event to a non-existent orchestration results in an exception.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-best-practice-reference -->

# Durable Functions best practices and diagnostic tools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article details some best practices when using Durable Functions. It also describes various tools to help diagnose problems during development, testing, and production use.

## Best practices

### Use the latest version of the Durable Functions extension and SDK

There are two components that a function app uses to execute Durable Functions. One is the *Durable Functions SDK* that allows you to write orchestrator, activity, and entity functions using your target programming language. The other is the *Durable extension*, which is the runtime component that actually executes the code. With the exception of .NET in-process apps, the SDK and the extension are versioned independently.

Staying up to date with the latest extension and SDK ensures your application benefits from the latest performance improvements, features, and bug fixes. Upgrading to the latest versions also ensures that Microsoft can collect the latest diagnostic telemetry to help accelerate the investigation process when you open a support case with Azure.

- See
[Upgrade durable functions extension version](durable-functions-extension-upgrade)for instructions on getting the latest extension version. - To ensure you're using the latest version of the SDK, check the package manager of the language you're using.

### Adhere to Durable Functions [code constraints](durable-functions-code-constraints)

The [replay](durable-functions-orchestrations#reliability) behavior of orchestrator code creates constraints on the type of code that you can write in an orchestrator function. An example of a constraint is that your orchestrator function must use deterministic APIs so that each time it’s replayed, it produces the same result.

Note

The Durable Functions Roslyn Analyzer is a live code analyzer that guides C# users to adhere to Durable Functions specific code constraints. See [Durable Functions Roslyn Analyzer](durable-functions-roslyn-analyzer) for instructions on how to enable it on Visual Studio and Visual Studio Code.

### Familiarize yourself with your programming language's Azure Functions performance settings

*Using default settings*, the language runtime you select may impose strict concurrency restrictions on your functions. For example: only allowing 1 function to execute at a time on a given VM. These restrictions can usually be relaxed by *fine tuning* the concurrency and performance settings of your language. If you're looking to optimize the performance of your Durable Functions application, you will need to familiarize yourself with these settings.

Below is a non-exhaustive list of some of the languages that often benefit from fine tuning their performance and concurrency settings, and their guidelines for doing so.

### Guarantee unique Task Hub names per app

Multiple Durable Function apps can share the same storage account. By default, the name of the app is used as the task hub name, which ensures that accidental sharing of task hubs won't happen. If you need to explicitly configure task hub names for your apps in host.json, you must ensure that the names are [ unique](durable-functions-task-hubs#multiple-function-apps). Otherwise, the multiple apps will compete for messages, which could result in undefined behavior, including orchestrations getting unexpectedly "stuck" in the Pending or Running state.

The only exception is if you deploy *copies* of the same app in [multiple regions](durable-functions-disaster-recovery-geo-distribution); in this case, you can use the same task hub for the copies.

### Follow guidance when deploying code changes to running orchestrators

It's inevitable that functions will be added, removed, and changed over the lifetime of an application. Examples of [common breaking changes](durable-functions-versioning) include changing activity or entity function signatures and changing orchestrator logic. These changes are a problem when they affect orchestrations that are still running. If deployed incorrectly, code changes could lead to orchestrations failing with a non-deterministic error, getting stuck indefinitely, performance degradation, etc. Refer to recommended [mitigation strategies](durable-functions-versioning#mitigation-strategies) when making code changes that may impact running orchestrations.

### Keep function inputs and outputs as small as possible

You can run into memory issues if you provide large inputs and outputs to and from Durable Functions APIs.

Inputs and outputs to Durable Functions APIs are serialized into the orchestration history. This means that large inputs and outputs can, over time, greatly contribute to an orchestrator history growing unbounded, which risks causing memory exceptions during [replay](durable-functions-orchestrations#reliability).

To mitigate the impact of large inputs and outputs to APIs, you may choose to delegate some work to sub-orchestrators. This helps load balance the history memory burden from a single orchestrator to multiple ones, therefore keeping the memory footprint of individual histories small.

That said the best practice for dealing with *large* data is to keep it in external storage and to only materialize that data inside Activities, when needed. When taking this approach, instead of communicating the data itself as inputs and/or outputs of Durable Functions APIs, you can pass in some lightweight identifier that allows you to retrieve that data from external storage when needed in your Activities.

### Keep Entity data small

Just like for inputs and outputs to Durable Functions APIs, if an entity's explicit state is too large, you may run into memory issues. In particular, an Entity state needs to be serialized and de-serialized from storage on any request, so large states add serialization latency to each invocation. Therefore, if an Entity needs to track large data, it's recommended to offload the data to external storage and track some lightweight identifier in the entity that allows you to materialize the data from storage when needed.

### Fine tune your Durable Functions concurrency settings

A single worker instance can execute multiple work items concurrently to increase efficiency. However, processing too many work items concurrently risks exhausting resources like CPU capacity, network connections, etc. In many cases, this shouldn’t be a concern because scaling and limiting work items are handled automatically for you. That said, if you’re experiencing performance issues (such as orchestrators taking too long to finish, are stuck in pending, etc.) or are doing performance testing, you could [configure concurrency limits](durable-functions-perf-and-scale#configuration-of-throttles) in the host.json file.

Note

This is not a replacement for fine-tuning the performance and concurrency settings of your language runtime in Azure Functions. The Durable Functions concurrency settings only determine how much work can be assigned to a given VM at a time, but it does not determine the degree of parallelism in processing that work inside the VM. The latter requires fine-tuning the language runtime performance settings.

### Use unique names for your external events

As with activity functions, external events have an *at-least-once* delivery guarantee. This means that, under certain *rare* conditions (which may occur during restarts, scaling, crashes, etc.), your application may receive duplicates of the same external event. Therefore, we recommend that external events contain an ID that allows them to be manually de-duplicated in orchestrators.

Note

The [MSSQL](durable-functions-storage-providers#mssql) storage provider consumes external events and updates orchestrator state transactionally, so in that backend there should be no risk of duplicate events, unlike with the default [Azure Storage storage provider](durable-functions-storage-providers). That said, it is still recommended that external events have unique names so that code is portable across backends.

### Invest in stress testing

As with anything performance related, the ideal concurrency settings and architecture of your app ultimately depends on your application's workload. Therefore, it's recommended that users to invest in a performance testing harness that simulates their expected workload and to use it to run performance and reliability experiments for their app.

### Avoid sensitive data in inputs, outputs, and exceptions

Inputs and outputs (including exceptions) to and from Durable Functions APIs are [durably persisted](durable-functions-serialization-and-persistence) in your [storage provider of choice](durable-functions-storage-providers). If those inputs, outputs, or exceptions contain sensitive data (such as secrets, connection strings, personally identifiable information, etc.) then anyone with read access to your storage provider's resources would be able to obtain them. To safely deal with sensitive data, it is recommended for users to fetch that data *within activity functions* from either Azure Key Vault or environment variables, and to never communicate that data directly to orchestrators or entities. That should help prevent sensitive data from leaking into your storage resources.

Note

This guidance also applies to the `CallHttp`

orchestrator API, which also persists its request and response payloads in storage. If your target HTTP endpoints require authentication, which may be sensitive, it is recommended that users implement the HTTP Call themselves inside of an activity, or to use the [built-in managed identity support offered by CallHttp](durable-functions-http-features#managed-identities), which does not persist any credentials to storage.

Tip

Similarly, avoid logging data containing secrets as anyone with read access to your logs (for example in Application Insights), would be able to obtain those secrets.

## Diagnostic tools

There are several tools available to help you diagnose problems.

### Durable Functions and Durable Task Framework Logs

#### Durable Functions Extension

The Durable extension emits tracking events that allow you to trace the end-to-end execution of an orchestration. These tracking events can be found and queried using the [Application Insights Analytics](/en-us/azure/azure-monitor/logs/log-query-overview) tool in the Azure portal. The verbosity of tracking data emitted can be configured in the `logger`

(Functions 1.x) or `logging`

(Functions 2.0) section of the host.json file. See [configuration details](durable-functions-diagnostics#functions-10).

#### Durable Task Framework

Starting in v2.3.0 of the Durable extension, logs emitted by the underlying Durable Task Framework (DTFx) are also available for collection. See [details on how to enable these logs](durable-functions-diagnostics#durable-task-framework-logging).

### Azure portal

#### Diagnose and solve problems

Azure Function App Diagnostics is a useful resource on Azure portal for monitoring and diagnosing potential issues in your application. It also provides suggestions to help resolve problems based on the diagnosis. See [Azure Function App Diagnostics](function-app-diagnostics).

#### Durable Functions Orchestration traces

Azure portal provides orchestration trace details to help you understand the status of each orchestration instance and trace the end-to-end execution. When you look at the list of functions inside your Azure Functions app, you'll see a **Monitor** column that contains links to the traces. You need to have Applications Insights enabled for your app to get this information.

### Durable Functions Monitor Extension

This is a [Visual Studio Code extension](https://github.com/microsoft/DurableFunctionsMonitor) that provides a UI for monitoring, managing, and debugging your orchestration instances.

### Roslyn Analyzer

The Durable Functions Roslyn Analyzer is a live code analyzer that guides C# users to adhere to Durable Functions specific [code constraints](durable-functions-code-constraints). See [Durable Functions Roslyn Analyzer](durable-functions-roslyn-analyzer) for instructions on how to enable it on Visual Studio and Visual Studio Code.

## Support

For questions and support, you may open an issue in one of the GitHub repos below. When reporting a bug in Azure, including information such as affected instance IDs, time ranges in UTC showing the problem, the application name (if possible) and deployment region will greatly speed up investigations.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/quickstart-java -->

# Quickstart: Create a Java Durable Functions app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Durable Functions, a feature of [Azure Functions](../functions-overview), to write stateful functions in a serverless environment. Durable Functions manages state, checkpoints, and restarts in your application.

In this quickstart, you create and test a "hello world" Durable Functions app in Java.

The most basic Durable Functions app has three functions:

**Orchestrator function**: A workflow that orchestrates other functions.**Activity function**: A function that is called by the orchestrator function, performs work, and optionally returns a value.**Client function**: A regular function in Azure that starts an orchestrator function. This example uses an HTTP-triggered function.

This quickstart describes different ways to create this "hello world" app. Use the selector at the top of the page to set your preferred approach.

## Prerequisites

To complete this quickstart, you need:

The

[Java Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure)version 8 or later installed.[Apache Maven](https://maven.apache.org)version 3.0 or later installed.The latest version of

[Azure Functions Core Tools](../functions-run-local).For Azure Functions

*4.x*, Core Tools version 4.0.4915 or later is required.An HTTP test tool that keeps your data secure. For more information, see

[HTTP test tools](../functions-develop-local#http-test-tools).An Azure subscription. To use Durable Functions, you must have an Azure Storage account.


If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Add required dependencies and plugins to your project

Add the following code to your *pom.xml* file:

```
<properties>
<azure.functions.maven.plugin.version>1.18.0</azure.functions.maven.plugin.version>
<azure.functions.java.library.version>3.0.0</azure.functions.java.library.version>
<durabletask.azure.functions>1.0.0</durabletask.azure.functions>
<functionAppName>your-unique-app-name</functionAppName>
</properties>
<dependencies>
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library</artifactId>
<version>${azure.functions.java.library.version}</version>
</dependency>
<dependency>
<groupId>com.microsoft</groupId>
<artifactId>durabletask-azure-functions</artifactId>
<version>${durabletask.azure.functions}</version>
</dependency>
</dependencies>
<build>
<plugins>
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-compiler-plugin</artifactId>
<version>3.8.1</version>
</plugin>
<plugin>
<groupId>com.microsoft.azure</groupId>
<artifactId>azure-functions-maven-plugin</artifactId>
<version>${azure.functions.maven.plugin.version}</version>
<configuration>
<appName>${functionAppName}</appName>
<resourceGroup>java-functions-group</resourceGroup>
<appServicePlanName>java-functions-app-service-plan</appServicePlanName>
<region>westus</region>
<runtime>
<os>windows</os>
<javaVersion>11</javaVersion>
</runtime>
<appSettings>
<property>
<name>FUNCTIONS_EXTENSION_VERSION</name>
<value>~4</value>
</property>
</appSettings>
</configuration>
<executions>
<execution>
<id>package-functions</id>
<goals>
<goal>package</goal>
</goals>
</execution>
</executions>
</plugin>
<plugin>
<artifactId>maven-clean-plugin</artifactId>
<version>3.1.0</version>
</plugin>
</plugins>
</build>
```


## Add the required JSON files

Add a *host.json* file to your project directory. It should look similar to the following example:

```
{
"version": "2.0",
"logging": {
"logLevel": {
"DurableTask.AzureStorage": "Warning",
"DurableTask.Core": "Warning"
}
},
"extensions": {
"durableTask": {
"hubName": "JavaTestHub"
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


Note

It's important to note that only the Azure Functions v4 extension bundle currently has the necessary support for Durable Functions for Java. Durable Functions for Java is *not* supported in v3 and early extension bundles. For more information on extension bundles, see the [extension bundles documentation](../extension-bundles).

Durable Functions needs a storage provider to store runtime state. Add a *local.settings.json* file to your project directory to configure the storage provider. To use Azure Storage as the provider, set the value of `AzureWebJobsStorage`

to the connection string of your Azure Storage account:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "<your storage account connection string>",
"FUNCTIONS_WORKER_RUNTIME": "java"
}
}
```


## Create your functions

The following sample code shows a basic example of each type of function:

```
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
import java.util.*;
import com.microsoft.durabletask.*;
import com.microsoft.durabletask.azurefunctions.DurableActivityTrigger;
import com.microsoft.durabletask.azurefunctions.DurableClientContext;
import com.microsoft.durabletask.azurefunctions.DurableClientInput;
import com.microsoft.durabletask.azurefunctions.DurableOrchestrationTrigger;
public class DurableFunctionsSample {
/**
* This HTTP-triggered function starts the orchestration.
*/
@FunctionName("StartOrchestration")
public HttpResponseMessage startOrchestration(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@DurableClientInput(name = "durableContext") DurableClientContext durableContext,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
DurableTaskClient client = durableContext.getClient();
String instanceId = client.scheduleNewOrchestrationInstance("Cities");
context.getLogger().info("Created new Java orchestration with instance ID = " + instanceId);
return durableContext.createCheckStatusResponse(request, instanceId);
}
/**
* This is the orchestrator function, which can schedule activity functions, create durable timers,
* or wait for external events in a way that's completely fault-tolerant.
*/
@FunctionName("Cities")
public String citiesOrchestrator(
@DurableOrchestrationTrigger(name = "taskOrchestrationContext") TaskOrchestrationContext ctx) {
String result = "";
result += ctx.callActivity("Capitalize", "Tokyo", String.class).await() + ", ";
result += ctx.callActivity("Capitalize", "London", String.class).await() + ", ";
result += ctx.callActivity("Capitalize", "Seattle", String.class).await() + ", ";
result += ctx.callActivity("Capitalize", "Austin", String.class).await();
return result;
}
/**
* This is the activity function that is invoked by the orchestrator function.
*/
@FunctionName("Capitalize")
public String capitalize(@DurableActivityTrigger(name = "name") String name, final ExecutionContext context) {
context.getLogger().info("Capitalizing: " + name);
return name.toUpperCase();
}
}
```


## Create a local project by using the Maven command

Run the following command to generate a project that contains the basic functions of a Durable Functions app:

```
mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -DarchetypeArtifactId=azure-functions-archetype -DarchetypeVersion=1.62 -Dtrigger=durablefunctions
```


At the prompts, provide the following information:

| Prompt | Action |
|---|---|
groupId |
Enter com.function. |
artifactId |
Enter myDurableFunction. |
version |
Select 1.0-SNAPSHOT. |
package |
Enter com.function. |
Y |
Enter Y and select Enter to confirm. |

Now you have a local project that has the three functions that are in a basic Durable Functions app.

Check to ensure that `com.microsoft:durabletask-azure-functions`

is set as a dependency in your *pom.xml* file.

## Configure the back-end storage provider

Durable Functions needs a storage provider to store runtime state. You can set Azure Storage as the storage provider in *local.settings.json*. Use the connection string of your Azure storage account as the value for `AzureWebJobsStorage`

like in this example:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "<your storage account connection string>",
"FUNCTIONS_WORKER_RUNTIME": "java"
}
}
```


## Create your local project

In Visual Studio Code, select F1 (or select Ctrl/Cmd+Shift+P) to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create New Project**.Select

**Browse**. In the**Select Folder**dialog, go to a folder to use for your project, and then choose**Select**.At the prompts, provide the following information:

Prompt Action **Select a language**Select **Java**.**Select a version of Java**Select **Java 8**or later. Select the Java version that your functions run on in Azure, and one that you verified locally.**Provide a group ID**Enter **com.function**.**Provide an artifact ID**Enter **myDurableFunction**.**Provide a version**Enter **1.0-SNAPSHOT**.**Provide a package name**Enter **com.function**.**Provide an app name**Enter **myDurableFunction**.**Select the build tool for Java project**Select **Maven**.**Select how you would like to open your project**Select **Open in new window**.

You now have a project that has an example HTTP function. You can remove this function if you'd like to, because you add the basic functions of a Durable Functions app in the next step.

## Add functions to the project

In the command palette, enter and then select

**Azure Functions: Create Function**.For

**Change template filter**, select**All**.At the prompts, provide the following information:

Prompt Action **Select a template for your function**Select **DurableFunctionsOrchestration**.**Provide a package name**Enter **com.function**.**Provide a function name**Enter **DurableFunctionsOrchestrator**.In the dialog, choose

**Select storage account**to set up a storage account, and then follow the prompts.

You should now have the three basic functions generated for a Durable Functions app.

## Configure pom.xml and host.json

Add the following dependency to your *pom.xml* file:

```
<dependency>
<groupId>com.microsoft</groupId>
<artifactId>durabletask-azure-functions</artifactId>
<version>1.0.0</version>
</dependency>
```


Add the `extensions`

property to your *host.json* file:

```
"extensions": { "durableTask": { "hubName": "JavaTestHub" }}
```


## Test the function locally

Azure Functions Core Tools gives you the capability to run an Azure Functions project on your local development computer.

Note

Durable Functions for Java requires Azure Functions Core Tools version 4.0.4915 or later. You can see which version is installed by running the `func --version`

command in the terminal.

If you're using Visual Studio Code, open a new terminal window and run the following commands to build the project:

`mvn clean package`

Then, run the durable function:

`mvn azure-functions:run`

In the terminal panel, copy the URL endpoint of your HTTP-triggered function.

Use an HTTP test tool to send an HTTP POST request to the URL endpoint.

The response should look similar to the following example:

`{ "id": "d1b33a60-333f-4d6e-9ade-17a7020562a9", "purgeHistoryDeleteUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/d1b33a60-333f-4d6e-9ade-17a7020562a9?code=ACCupah_QfGKo...", "sendEventPostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/d1b33a60-333f-4d6e-9ade-17a7020562a9/raiseEvent/{eventName}?code=ACCupah_QfGKo...", "statusQueryGetUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/d1b33a60-333f-4d6e-9ade-17a7020562a9?code=ACCupah_QfGKo...", "terminatePostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/d1b33a60-333f-4d6e-9ade-17a7020562a9/terminate?reason={text}&code=ACCupah_QfGKo..." }`

The response is the HTTP function's initial result. It lets you know that the durable orchestration started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs. For now, query the status of the orchestration.

Copy the URL value for

`statusQueryGetUri`

, paste it in your browser's address bar, and execute the request. Alternatively, you can continue to use the HTTP test tool to issue the GET request.The request queries the orchestration instance for the status. You should see that the instance finished and that it includes the outputs or results of the durable function, like in this example:

`{ "name": "Cities", "instanceId": "d1b33a60-333f-4d6e-9ade-17a7020562a9", "runtimeStatus": "Completed", "input": null, "customStatus": "", "output":"TOKYO, LONDON, SEATTLE, AUSTIN", "createdTime": "2022-12-12T05:00:02Z", "lastUpdatedTime": "2022-12-12T05:00:06Z" }`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-troubleshooting-guide -->

# Durable Functions Troubleshooting Guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Durable Functions is an extension of [Azure Functions](../functions-overview) that lets you build serverless orchestrations using ordinary code. For more information on Durable Functions, see the [Durable Functions overview](durable-functions-overview).

This article provides a guide for troubleshooting common scenarios in Durable Functions apps.

Note

Microsoft support engineers are available to assist in diagnosing issues with your application. If you're not able to diagnose your problem using this guide, you can file a support ticket by accessing the **New Support request** blade in the **Support + troubleshooting** section of your function app page in the Azure portal.

Tip

When debugging and diagnosing issues, it's recommended that you start by ensuring your app is using the latest Durable Functions extension version. Most of the time, using the latest version mitigates known issues already reported by other users. Please read the [Upgrade Durable Functions extension version](durable-functions-extension-upgrade) article for instructions on how to upgrade your extension version.

The **Diagnose and solve problems** tab in the Azure portal is a useful resource to monitor and diagnose possible issues related to your application. It also supplies potential solutions to your problems based on the diagnosis. See [Azure Function app diagnostics](function-app-diagnostics) for more details.

If the resources above didn't solve your problem, the following sections provide advice for specific application symptoms:

## Orchestration is stuck in the `Pending`

state

When you start an orchestration, a "start" message gets written to an internal queue managed by the Durable extension, and the status of the orchestration gets set to "Pending". After the orchestration message gets picked up and successfully processed by an available app instance, the status will transition to "Running" (or to some other non-"Pending" state).

Use the following steps to troubleshoot orchestration instances that remain stuck indefinitely in the "Pending" state.

Check the Durable Task Framework traces for warnings or errors for the impacted orchestration instance ID. A sample query can be found in the

[Trace Errors/Warnings section](#trace-errorswarnings).Check the Azure Storage control queues assigned to the stuck orchestrator to see if its "start message" is still there For more information on control queues, see the

[Azure Storage provider control queue documentation](durable-functions-azure-storage-provider#control-queues).Change your app's

[platform configuration](../../app-service/configure-common#configure-general-settings)version to "64 Bit". Sometimes orchestrations don't start because the app is running out of memory. Switching to 64-bit process allows the app to allocate more total memory. This only applies to App Service Basic, Standard, Premium, and Elastic Premium plans. Free or Consumption plans**do not**support 64-bit processes.

## Orchestration starts after a long delay

Normally, orchestrations start within a few seconds after they're scheduled. However, there are certain cases where orchestrations may take longer to start. Use the following steps to troubleshoot when orchestrations take more than a few seconds to start executing.

Refer to the

[documentation on delayed orchestrations in Azure Storage](durable-functions-azure-storage-provider#orchestration-start-delays)to check whether the delay may be caused by known limitations.Check the Durable Task Framework traces for warnings or errors with the impacted orchestration instance ID. A sample query can be found in

[Trace Errors/Warnings section](#trace-errorswarnings).

## Orchestration doesn't complete / is stuck in the `Running`

state

If an orchestration remains in the "Running" state for a long period of time, it usually means that it's waiting for a long-running task that is scheduled to complete. For example, it could be waiting for a durable timer task, an activity task, or an external event task to be completed. However, if you observe that scheduled tasks have completed successfully but the orchestration still isn't making progress, then there might be a problem preventing the orchestration from proceeding to its next task. We often refer to orchestrations in this state as "stuck orchestrations".

Use the following steps to troubleshoot stuck orchestrations:

Try restarting the function app. This step can help if the orchestration gets stuck due to a transient bug or deadlock in either the app or the extension code.

Check the Azure Storage account control queues to see if any queues are growing continuously.

[This Azure Storage messaging KQL query](durable-functions-troubleshooting-guide#azure-storage-messaging)can help identify problems with dequeuing orchestration messages. If the problem impacts only a single control queue, it might indicate a problem that exists only on a specific app instance, in which case scaling up or down to move off the unhealthy VM instance could help.Use the Application Insights query in the

[Azure Storage Messaging section](durable-functions-troubleshooting-guide#azure-storage-messaging)to filter on that queue name as the Partition ID and look for any problems related to that control queue partition.Check the guidance in

[Durable Functions Best Practice and Diagnostic Tools](durable-functions-best-practice-reference). Some problems may be caused by known Durable Functions anti-patterns.Check the

[Durable Functions Versioning documentation](durable-functions-versioning). Some problems may be caused by breaking changes to in-flight orchestration instances.

## Orchestration runs slowly

Heavy data processing, internal errors, and insufficient compute resources can cause orchestrations to execute slower than normal. Use the following steps to troubleshoot orchestrations that are taking longer than expected to execute:

Check the Durable Task Framework traces for warnings or errors for the impacted orchestration instance ID. A sample query can be found in the

[Trace Errors/Warnings section](#trace-errorswarnings).If your app utilizes the .NET in-process model, consider enabling

[extended sessions](durable-functions-azure-storage-provider#extended-sessions). Extended sessions can minimize history loads, which can slow down processing.Check for performance and scalability bottlenecks. Application performance depends on many factors. For example, high CPU usage, or large memory consumption can result in delays. Read

[Performance and scale in Durable Functions](durable-functions-perf-and-scale)for detailed guidance.

## Sample Queries

This section shows how to troubleshoot issues by writing custom [KQL queries](/en-us/azure/data-explorer/kusto/query/) in the Azure Application Insights instance configured for your Azure Functions app.

### Azure Storage Messaging

When using the default Azure Storage provider, all Durable Functions behavior is driven by Azure Storage queue messages and all state related to an orchestration is stored in table storage and blob storage. When Durable Task Framework tracing is enabled, all Azure Storage interactions are logged to Application Insights, and this data is critically important for debugging execution and performance problems.

Starting in v2.3.0 of the Durable Functions extension, you can have these Durable Task Framework logs published to your Application Insights instance by updating your logging configuration in the host.json file. See the [Durable Task Framework logging article](durable-functions-diagnostics) for information and instructions on how to do this.

The following query is for inspecting end-to-end Azure Storage interactions for a specific orchestration instance. Edit `start`

and `orchestrationInstanceID`

to filter by time range and instance ID.

```
let start = datetime(XXXX-XX-XXTXX:XX:XX); // edit this
let orchestrationInstanceID = "XXXXXXX"; //edit this
traces
| where timestamp > start and timestamp < start + 1h
| where customDimensions.Category == "DurableTask.AzureStorage"
| extend taskName = customDimensions["EventName"]
| extend eventType = customDimensions["prop__EventType"]
| extend extendedSession = customDimensions["prop__IsExtendedSession"]
| extend account = customDimensions["prop__Account"]
| extend details = customDimensions["prop__Details"]
| extend instanceId = customDimensions["prop__InstanceId"]
| extend messageId = customDimensions["prop__MessageId"]
| extend executionId = customDimensions["prop__ExecutionId"]
| extend age = customDimensions["prop__Age"]
| extend latencyMs = customDimensions["prop__LatencyMs"]
| extend dequeueCount = customDimensions["prop__DequeueCount"]
| extend partitionId = customDimensions["prop__PartitionId"]
| extend eventCount = customDimensions["prop__TotalEventCount"]
| extend taskHub = customDimensions["prop__TaskHub"]
| extend pid = customDimensions["ProcessId"]
| extend appName = cloud_RoleName
| extend newEvents = customDimensions["prop__NewEvents"]
| where instanceId == orchestrationInstanceID
| sort by timestamp asc
| project timestamp, appName, severityLevel, pid, taskName, eventType, message, details, messageId, partitionId, instanceId, executionId, age, latencyMs, dequeueCount, eventCount, newEvents, taskHub, account, extendedSession, sdkVersion
```


### Trace Errors/Warnings

The following query searches for errors and warnings for a given orchestration instance. You'll need to provide a value for `orchestrationInstanceID`

.

```
let orchestrationInstanceID = "XXXXXX"; // edit this
let start = datetime(XXXX-XX-XXTXX:XX:XX);
traces
| where timestamp > start and timestamp < start + 1h
| extend instanceId = iif(isnull(customDimensions["prop__InstanceId"] ) , customDimensions["prop__instanceId"], customDimensions["prop__InstanceId"] )
| extend logLevel = customDimensions["LogLevel"]
| extend functionName = customDimensions["prop__functionName"]
| extend status = customDimensions["prop__status"]
| extend details = customDimensions["prop__Details"]
| extend reason = customDimensions["prop__reason"]
| where severityLevel >= 1 // to see all logs of severity level "Information" or greater.
| where instanceId == orchestrationInstanceID
| sort by timestamp asc
```


### Control queue / Partition ID logs

The following query searches for all activity associated with an instanceId's control queue. You'll need to provide the value for the instanceID in `orchestrationInstanceID`

and the query's start time in `start`

.

```
let orchestrationInstanceID = "XXXXXX"; // edit this
let start = datetime(XXXX-XX-XXTXX:XX:XX); // edit this
traces // determine control queue for this orchestrator
| where timestamp > start and timestamp < start + 1h
| extend instanceId = customDimensions["prop__TargetInstanceId"]
| extend partitionId = tostring(customDimensions["prop__PartitionId"])
| where partitionId contains "control"
| where instanceId == orchestrationInstanceID
| join kind = rightsemi(
traces
| where timestamp > start and timestamp < start + 1h
| where customDimensions.Category == "DurableTask.AzureStorage"
| extend taskName = customDimensions["EventName"]
| extend eventType = customDimensions["prop__EventType"]
| extend extendedSession = customDimensions["prop__IsExtendedSession"]
| extend account = customDimensions["prop__Account"]
| extend details = customDimensions["prop__Details"]
| extend instanceId = customDimensions["prop__InstanceId"]
| extend messageId = customDimensions["prop__MessageId"]
| extend executionId = customDimensions["prop__ExecutionId"]
| extend age = customDimensions["prop__Age"]
| extend latencyMs = customDimensions["prop__LatencyMs"]
| extend dequeueCount = customDimensions["prop__DequeueCount"]
| extend partitionId = tostring(customDimensions["prop__PartitionId"])
| extend eventCount = customDimensions["prop__TotalEventCount"]
| extend taskHub = customDimensions["prop__TaskHub"]
| extend pid = customDimensions["ProcessId"]
| extend appName = cloud_RoleName
| extend newEvents = customDimensions["prop__NewEvents"]
) on partitionId
| sort by timestamp asc
| project timestamp, appName, severityLevel, pid, taskName, eventType, message, details, messageId, partitionId, instanceId, executionId, age, latencyMs, dequeueCount, eventCount, newEvents, taskHub, account, extendedSession, sdkVersion
```


### Application Insights column reference

Below is a list of the columns projected by the queries above and their respective descriptions.

| Column | Description |
|---|---|
| pid | Process ID of the function app instance. This is useful for determining if the process was recycled while an orchestration was executing. |
| taskName | The name of the event being logged. |
| eventType | The type of message, which usually represents work done by an orchestrator. A full list of its possible values, and their descriptions, is
|

[extended sessions](durable-functions-azure-storage-provider#extended-sessions)is enabled.*after*we send the message.`continue-as-new`

is invoked.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-monitor -->

# Monitor scenario in Durable Functions - Weather watcher sample

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The monitor pattern refers to a flexible *recurring* process in a workflow - for example, polling until certain conditions are met. This article explains a sample that uses [Durable Functions](durable-functions-overview) to implement monitoring.

## Prerequisites

## Scenario overview

This sample monitors a location's current weather conditions and alerts a user by SMS when the skies are clear. You could use a regular timer-triggered function to check the weather and send alerts. However, one problem with this approach is **lifetime management**. If only one alert should be sent, the monitor needs to disable itself after clear weather is detected. The monitoring pattern can end its own execution, among other benefits:

- Monitors run on intervals, not schedules: a timer trigger
*runs*every hour; a monitor*waits*one hour between actions. A monitor's actions won't overlap unless specified, which can be important for long-running tasks. - Monitors can have dynamic intervals: the wait time can change based on some condition.
- Monitors can terminate when some condition is met or be terminated by another process.
- Monitors can take parameters. The sample shows how the same weather-monitoring process can be applied to any requested location and phone number.
- Monitors are scalable. Because each monitor is an orchestration instance, multiple monitors can be created without having to create new functions or define more code.
- Monitors integrate easily into larger workflows. A monitor can be one section of a more complex orchestration function, or a
[sub-orchestration](durable-functions-sub-orchestrations).

## Configuration

### Configuring Twilio integration

This sample involves using the [Twilio](https://www.twilio.com/) service to send SMS messages to a mobile phone. Azure Functions already has support for Twilio via the [Twilio binding](../functions-bindings-twilio), and the sample uses that feature.

The first thing you need is a Twilio account. You can create one free at [https://www.twilio.com/try-twilio](https://www.twilio.com/try-twilio). Once you have an account, add the following three **app settings** to your function app.

| App setting name | Value description |
|---|---|
TwilioAccountSid |
The SID for your Twilio account |
TwilioAuthToken |
The Auth token for your Twilio account |
TwilioPhoneNumber |
The phone number associated with your Twilio account. This is used to send SMS messages. |

### Configuring Weather Underground integration

This sample involves using the Weather Underground API to check current weather conditions for a location.

The first thing you need is a Weather Underground account. You can create one for free at [https://www.wunderground.com/signup](https://www.wunderground.com/signup). Once you have an account, you need to acquire an API key. You can do so by visiting [https://www.wunderground.com/weather/api](https://www.wunderground.com/weather/api/?MR=1), then selecting Key Settings. The Stratus Developer plan is free and sufficient to run this sample.

Once you have an API key, add the following **app setting** to your function app.

| App setting name | Value description |
|---|---|
WeatherUndergroundApiKey |
Your Weather Underground API key. |

## The functions

This article explains the following functions in the sample app:

`E3_Monitor`

: An[orchestrator function](durable-functions-bindings#orchestration-trigger)that calls`E3_GetIsClear`

periodically. It calls`E3_SendGoodWeatherAlert`

if`E3_GetIsClear`

returns true.`E3_GetIsClear`

: An[activity function](durable-functions-bindings#activity-trigger)that checks the current weather conditions for a location.`E3_SendGoodWeatherAlert`

: An activity function that sends an SMS message via Twilio.

### E3_Monitor orchestrator function

```
[FunctionName("E3_Monitor")]
public static async Task Run([OrchestrationTrigger] IDurableOrchestrationContext monitorContext, ILogger log)
{
MonitorRequest input = monitorContext.GetInput<MonitorRequest>();
if (!monitorContext.IsReplaying) { log.LogInformation($"Received monitor request. Location: {input?.Location}. Phone: {input?.Phone}."); }
VerifyRequest(input);
DateTime endTime = monitorContext.CurrentUtcDateTime.AddHours(6);
if (!monitorContext.IsReplaying) { log.LogInformation($"Instantiating monitor for {input.Location}. Expires: {endTime}."); }
while (monitorContext.CurrentUtcDateTime < endTime)
{
// Check the weather
if (!monitorContext.IsReplaying) { log.LogInformation($"Checking current weather conditions for {input.Location} at {monitorContext.CurrentUtcDateTime}."); }
bool isClear = await monitorContext.CallActivityAsync<bool>("E3_GetIsClear", input.Location);
if (isClear)
{
// It's not raining! Or snowing. Or misting. Tell our user to take advantage of it.
if (!monitorContext.IsReplaying) { log.LogInformation($"Detected clear weather for {input.Location}. Notifying {input.Phone}."); }
await monitorContext.CallActivityAsync("E3_SendGoodWeatherAlert", input.Phone);
break;
}
else
{
// Wait for the next checkpoint
var nextCheckpoint = monitorContext.CurrentUtcDateTime.AddMinutes(30);
if (!monitorContext.IsReplaying) { log.LogInformation($"Next check for {input.Location} at {nextCheckpoint}."); }
await monitorContext.CreateTimer(nextCheckpoint, CancellationToken.None);
}
}
log.LogInformation($"Monitor expiring.");
}
[Deterministic]
private static void VerifyRequest(MonitorRequest request)
{
if (request == null)
{
throw new ArgumentNullException(nameof(request), "An input object is required.");
}
if (request.Location == null)
{
throw new ArgumentNullException(nameof(request.Location), "A location input is required.");
}
if (string.IsNullOrEmpty(request.Phone))
{
throw new ArgumentNullException(nameof(request.Phone), "A phone number input is required.");
}
}
```


The orchestrator requires a location to monitor and a phone number to send a message to when the weather becomes clear at the location. This data is passed to the orchestrator as a strongly typed `MonitorRequest`

object.

This orchestrator function performs the following actions:

- Gets the
**MonitorRequest**consisting of the*location*to monitor and the*phone number*to which it sends an SMS notification. - Determines the expiration time of the monitor. The sample uses a hard-coded value for brevity.
- Calls
**E3_GetIsClear**to determine whether there are clear skies at the requested location. - If the weather is clear, calls
**E3_SendGoodWeatherAlert**to send an SMS notification to the requested phone number. - Creates a durable timer to resume the orchestration at the next polling interval. The sample uses a hard-coded value for brevity.
- Continues running until the current UTC time passes the monitor's expiration time, or an SMS alert is sent.

Multiple orchestrator instances can run simultaneously by calling the orchestrator function multiple times. The location to monitor and the phone number to send an SMS alert to can be specified. Finally, do note that the orchestrator function isn't* running while waiting for the timer, so you won't get charged for it.

### E3_GetIsClear activity function

As with other samples, the helper activity functions are regular functions that use the `activityTrigger`

trigger binding. The **E3_GetIsClear** function gets the current weather conditions using the Weather Underground API and determines whether the sky is clear.

```
[FunctionName("E3_GetIsClear")]
public static async Task<bool> GetIsClear([ActivityTrigger] Location location)
{
var currentConditions = await WeatherUnderground.GetCurrentConditionsAsync(location);
return currentConditions.Equals(WeatherCondition.Clear);
}
```


### E3_SendGoodWeatherAlert activity function

The **E3_SendGoodWeatherAlert** function uses the Twilio binding to send an SMS message notifying the end user that it's a good time for a walk.

```
[FunctionName("E3_SendGoodWeatherAlert")]
public static void SendGoodWeatherAlert(
[ActivityTrigger] string phoneNumber,
ILogger log,
[TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "%TwilioPhoneNumber%")]
out CreateMessageOptions message)
{
message = new CreateMessageOptions(new PhoneNumber(phoneNumber));
message.Body = $"The weather's clear outside! Go take a walk!";
}
internal class WeatherUnderground
{
private static readonly HttpClient httpClient = new HttpClient();
private static IReadOnlyDictionary<string, WeatherCondition> weatherMapping = new Dictionary<string, WeatherCondition>()
{
{ "Clear", WeatherCondition.Clear },
{ "Overcast", WeatherCondition.Clear },
{ "Cloudy", WeatherCondition.Clear },
{ "Clouds", WeatherCondition.Clear },
{ "Drizzle", WeatherCondition.Precipitation },
{ "Hail", WeatherCondition.Precipitation },
{ "Ice", WeatherCondition.Precipitation },
{ "Mist", WeatherCondition.Precipitation },
{ "Precipitation", WeatherCondition.Precipitation },
{ "Rain", WeatherCondition.Precipitation },
{ "Showers", WeatherCondition.Precipitation },
{ "Snow", WeatherCondition.Precipitation },
{ "Spray", WeatherCondition.Precipitation },
{ "Squall", WeatherCondition.Precipitation },
{ "Thunderstorm", WeatherCondition.Precipitation },
};
internal static async Task<WeatherCondition> GetCurrentConditionsAsync(Location location)
{
var apiKey = Environment.GetEnvironmentVariable("WeatherUndergroundApiKey");
if (string.IsNullOrEmpty(apiKey))
{
throw new InvalidOperationException("The WeatherUndergroundApiKey environment variable was not set.");
}
var callString = string.Format("http://api.wunderground.com/api/{0}/conditions/q/{1}/{2}.json", apiKey, location.State, location.City);
var response = await httpClient.GetAsync(callString);
var conditions = await response.Content.ReadAsAsync<JObject>();
JToken currentObservation;
if (!conditions.TryGetValue("current_observation", out currentObservation))
{
JToken error = conditions.SelectToken("response.error");
if (error != null)
{
throw new InvalidOperationException($"API returned an error: {error}.");
}
else
{
throw new ArgumentException("Could not find weather for this location. Try being more specific.");
}
}
return MapToWeatherCondition((string)(currentObservation as JObject).GetValue("weather"));
}
private static WeatherCondition MapToWeatherCondition(string weather)
{
foreach (var pair in weatherMapping)
{
if (weather.Contains(pair.Key))
{
return pair.Value;
}
}
return WeatherCondition.Other;
}
}
```


Note

You will need to install the `Microsoft.Azure.WebJobs.Extensions.Twilio`

Nuget package to run the sample code.

## Run the sample

Using the HTTP-triggered functions included in the sample, you can start the orchestration by sending the following HTTP POST request:

```
POST https://{host}/orchestrators/E3_Monitor
Content-Length: 77
Content-Type: application/json
{ "location": { "city": "Redmond", "state": "WA" }, "phone": "+1425XXXXXXX" }
```


```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://{host}/runtime/webhooks/durabletask/instances/f6893f25acf64df2ab53a35c09d52635?taskHub=SampleHubVS&connection=Storage&code={SystemKey}
RetryAfter: 10
{"id": "f6893f25acf64df2ab53a35c09d52635", "statusQueryGetUri": "https://{host}/runtime/webhooks/durabletask/instances/f6893f25acf64df2ab53a35c09d52635?taskHub=SampleHubVS&connection=Storage&code={systemKey}", "sendEventPostUri": "https://{host}/runtime/webhooks/durabletask/instances/f6893f25acf64df2ab53a35c09d52635/raiseEvent/{eventName}?taskHub=SampleHubVS&connection=Storage&code={systemKey}", "terminatePostUri": "https://{host}/runtime/webhooks/durabletask/instances/f6893f25acf64df2ab53a35c09d52635/terminate?reason={text}&taskHub=SampleHubVS&connection=Storage&code={systemKey}"}
```


The **E3_Monitor** instance starts and queries the current weather conditions for the requested location. If the weather is clear, it calls an activity function to send an alert; otherwise, it sets a timer. When the timer expires, the orchestration resumes.

You can see the orchestration's activity by looking at the function logs in the Azure Functions portal.

```
2018-03-01T01:14:41.649 Function started (Id=2d5fcadf-275b-4226-a174-f9f943c90cd1)
2018-03-01T01:14:42.741 Started orchestration with ID = '1608200bb2ce4b7face5fc3b8e674f2e'.
2018-03-01T01:14:42.780 Function completed (Success, Id=2d5fcadf-275b-4226-a174-f9f943c90cd1, Duration=1111ms)
2018-03-01T01:14:52.765 Function started (Id=b1b7eb4a-96d3-4f11-a0ff-893e08dd4cfb)
2018-03-01T01:14:52.890 Received monitor request. Location: Redmond, WA. Phone: +1425XXXXXXX.
2018-03-01T01:14:52.895 Instantiating monitor for Redmond, WA. Expires: 3/1/2018 7:14:52 AM.
2018-03-01T01:14:52.909 Checking current weather conditions for Redmond, WA at 3/1/2018 1:14:52 AM.
2018-03-01T01:14:52.954 Function completed (Success, Id=b1b7eb4a-96d3-4f11-a0ff-893e08dd4cfb, Duration=189ms)
2018-03-01T01:14:53.226 Function started (Id=80a4cb26-c4be-46ba-85c8-ea0c6d07d859)
2018-03-01T01:14:53.808 Function completed (Success, Id=80a4cb26-c4be-46ba-85c8-ea0c6d07d859, Duration=582ms)
2018-03-01T01:14:53.967 Function started (Id=561d0c78-ee6e-46cb-b6db-39ef639c9a2c)
2018-03-01T01:14:53.996 Next check for Redmond, WA at 3/1/2018 1:44:53 AM.
2018-03-01T01:14:54.030 Function completed (Success, Id=561d0c78-ee6e-46cb-b6db-39ef639c9a2c, Duration=62ms)
```


The orchestration completes once its timeout is reached or clear skies are detected. You can also use the `terminate`

API inside another function or invoke the **terminatePostUri** HTTP POST webhook referenced in the preceding 202 response. To use the webhook, replace `{text}`

with the reason for the early termination. The HTTP POST URL looks roughly as follows:

```
POST https://{host}/runtime/webhooks/durabletask/instances/f6893f25acf64df2ab53a35c09d52635/terminate?reason=Because&taskHub=SampleHubVS&connection=Storage&code={systemKey}
```


## Next steps

This sample demonstrates how to use Durable Functions to monitor an external source's status using [durable timers](durable-functions-timers) and conditional logic. The next sample shows how to use external events and [durable timers](durable-functions-timers) to handle human interaction.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/quickstart-python-vscode -->

# Quickstart: Create a Python Durable Functions app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Durable Functions, a feature of [Azure Functions](../functions-overview), to write stateful functions in a serverless environment. You install Durable Functions by installing the [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) in Visual Studio Code. The extension manages state, checkpoints, and restarts in your application.

In this quickstart, you use the Durable Functions extension in Visual Studio Code to locally create and test a "hello world" Durable Functions app in Azure Functions. The Durable Functions app orchestrates and chains together calls to other functions. Then, you publish the function code to Azure. The tools you use are available via the Visual Studio Code extension.


Note

This quickstart uses the decorator-based [v2 programming model for Python](../functions-reference-python). This model gives a simpler file structure and is more code-centric compared to v1.

## Prerequisites

To complete this quickstart, you need:

[Visual Studio Code](https://code.visualstudio.com/download)installed.The Visual Studio Code extension

[Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)installed.The latest version of

[Azure Functions Core Tools](../functions-run-local)installed.An HTTP test tool that keeps your data secure. For more information, see

[HTTP test tools](../functions-develop-local#http-test-tools).An Azure subscription for deploying app to Azure.

[Python](https://www.python.org/)version 3.7, 3.8, 3.9, or 3.10 installed.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project.

In Visual Studio Code, select F1 (or select Ctrl/Cmd+Shift+P) to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create New Project**.Select

**Browse**. In the**Select Folder**dialog, go to a folder to use for your project, and then choose**Select**.At the prompts, provide the following information:

Prompt Action Description **Select a language for your function app project**Select **Python**.Creates a local Python Functions project. **Select a version**Select **Azure Functions v4**.You see this option only when Core Tools isn't already installed. In this case, Core Tools is installed the first time you run the app. **Python version**Select **Python 3.7**,**Python 3.8**,**Python 3.9**, or**Python 3.10**.Visual Studio Code creates a virtual environment by using the version you select. **Select a template for your project's first function**Select **Skip for now**.**Select how you would like to open your project**Select **Open in current window**.Opens Visual Studio Code in the folder you selected.

Visual Studio Code installs Azure Functions Core Tools if it's required to create a project. It also creates a function app project in a folder. This project contains the [host.json](../functions-host-json) and [local.settings.json](../functions-develop-local#local-settings-file) configuration files.

A *requirements.txt* file is also created in the root folder. It specifies the Python packages required to run your function app.

## Install azure-functions-durable from PyPI

When you create the project, the Azure Functions Visual Studio Code extension automatically creates a virtual environment with your selected Python version. You then need to activate the virtual environment in a terminal and install some dependencies required by Azure Functions and Durable Functions.

Open the

*requirements.txt*in the editor and change its content to the following code:`azure-functions azure-functions-durable`

In the current folder, open the editor's integrated terminal (Ctrl+Shift+`).

In the integrated terminal, activate the virtual environment in the current folder, depending on your operating system.


Then, in the integrated terminal where the virtual environment is activated, use pip to install the packages you defined.

```
python -m pip install -r requirements.txt
```


Note

You must install [azure-functions-durable](https://pypi.org/project/azure-functions-durable/) v1.2.4 or above.

## Create your functions

The most basic Durable Functions app has three functions:

**Orchestrator function**: A workflow that orchestrates other functions.**Activity function**: A function that is called by the orchestrator function, performs work, and optionally returns a value.**Client function**: A regular function in Azure that starts an orchestrator function. This example uses an HTTP-triggered function.

## Sample code

To create a basic Durable Functions app by using these three function types, replace the contents of *function_app.py* with the following Python code:

```
import azure.functions as func
import azure.durable_functions as df
myApp = df.DFApp(http_auth_level=func.AuthLevel.ANONYMOUS)
# An HTTP-triggered function with a Durable Functions client binding
@myApp.route(route="orchestrators/{functionName}")
@myApp.durable_client_input(client_name="client")
async def http_start(req: func.HttpRequest, client):
function_name = req.route_params.get('functionName')
instance_id = await client.start_new(function_name)
response = client.create_check_status_response(req, instance_id)
return response
# Orchestrator
@myApp.orchestration_trigger(context_name="context")
def hello_orchestrator(context):
result1 = yield context.call_activity("hello", "Seattle")
result2 = yield context.call_activity("hello", "Tokyo")
result3 = yield context.call_activity("hello", "London")
return [result1, result2, result3]
# Activity
@myApp.activity_trigger(input_name="city")
def hello(city: str):
return f"Hello {city}"
```


Review the following table for an explanation of each function and its purpose in the sample:

| Method | Description |
|---|---|
`hello_orchestrator` |
The orchestrator function, which describes the workflow. In this case, the orchestration starts, invokes three functions in a sequence, and then returns the ordered results of all three functions in a list. |
`hello` |
The activity function, which performs the work that is orchestrated. The function returns a simple greeting to the city passed as an argument. |
`http_start` |
An
`check status` response. |

Note

Durable Functions also supports Python v2 programming model [blueprints](../functions-reference-python#organizing-with-blueprints). To use blueprints, register your blueprint functions by using the [azure-functions-durable](https://pypi.org/project/azure-functions-durable) `Blueprint`

[class](https://github.com/Azure/azure-functions-durable-python/blob/dev/samples-v2/blueprint/durable_blueprints.py). You can register the resulting blueprint as usual. You can use our [sample](https://github.com/Azure/azure-functions-durable-python/tree/dev/samples-v2/blueprint) as an example.

## Configure storage emulator

You can use [Azurite](../../storage/common/storage-use-azurite?tabs=visual-studio-code), an emulator for Azure Storage, to test the function locally. In *local.settings.json*, set the value for `AzureWebJobsStorage`

to `UseDevelopmentStorage=true`

like in this example:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_WORKER_RUNTIME": "python"
}
}
```


To install and start running the Azurite extension in Visual Studio Code, in the command palette, enter **Azurite: Start** and select Enter.

You can use other storage options for your Durable Functions app. For more information about storage options and benefits, see [Durable Functions storage providers](durable-functions-storage-providers).

## Test the function locally

Azure Functions Core Tools gives you the capability to run an Azure Functions project on your local development computer. If it isn't installed, you're prompted to install these tools the first time you start a function in Visual Studio Code.

To test your function, set a breakpoint in the

`hello`

activity function code. Select F5 or select**Debug: Start Debugging**in the command palette to start the function app project. Output from Core Tools appears in the terminal panel.Note

For more information about debugging, see

[Durable Functions diagnostics](durable-functions-diagnostics#debugging).In the terminal panel, copy the URL endpoint of your HTTP-triggered function.

Use your browser or an HTTP test tool to send an HTTP POST request to the URL endpoint.

Replace the last segment with the name of the orchestrator function (

`hello_orchestrator`

). The URL should be similar to`http://localhost:7071/api/orchestrators/hello_orchestrator`

.The response is the HTTP function's initial result. It lets you know that the durable orchestration has started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs. For now, query the status of the orchestration.

Copy the URL value for

`statusQueryGetUri`

, paste it in your browser's address bar, and execute the request. You can also continue to use your HTTP test tool to issue the GET request.The request queries the orchestration instance for the status. You should see that the instance finished and that it includes the outputs or results of the durable function. It looks similar to this example:

`{ "name": "hello_orchestrator", "instanceId": "9a528a9e926f4b46b7d3deaa134b7e8a", "runtimeStatus": "Completed", "input": null, "customStatus": null, "output": [ "Hello Tokyo!", "Hello Seattle!", "Hello London!" ], "createdTime": "2020-03-18T21:54:49Z", "lastUpdatedTime": "2020-03-18T21:54:54Z" }`

To stop debugging, in Visual Studio Code, select Shift+F5.


After you verify that the function runs correctly on your local computer, it's time to publish the project to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](../storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Test your function in Azure

Copy the URL of the HTTP trigger from the output panel. The URL that calls your HTTP-triggered function must be in this format:

`https://<functionappname>.azurewebsites.net/api/orchestrators/hello_orchestrator`

Paste the new URL for the HTTP request in your browser's address bar. When you use the published app, you can expect to get the same status response that you got when you tested locally.


The Python Durable Functions app that you created and published by using Visual Studio Code is ready to use.

## Clean up resources

If you no longer need the resources that you created to complete the quickstart, to avoid related costs in your Azure subscription, [delete the resource group](/en-us/azure/azure-resource-manager/management/delete-resource-group?tabs=azure-portal#delete-resource-group) and all related resources.

## Related content

- Learn about
[common Durable Functions app patterns](durable-functions-overview#application-patterns). - Learn about
[Unit Testing Durable Functions in Python](durable-functions-unit-testing-python)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-storage-providers -->

# Durable Functions storage providers

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Durable Functions is a set of Azure Functions triggers and bindings that are internally powered by the [Durable Task Framework](https://github.com/Azure/durabletask) (DTFx). DTFx supports various backend storage providers, including the Azure Storage provider used by Durable Functions. As of Durable Functions **v2.5.0**, users can configure their function apps to use DTFx storage providers other than the Azure Storage provider.

Note

The default Azure Storage provider for Durable Functions is the easiest to use since it requires no extra configuration. However, there are cost, scalability, and data management tradeoffs that may favor the use of an alternate backend provider.

Durable Functions supports two types of backend providers: "Bring your own (BYO)" and Azure managed. The BYO options include *Azure Storage, Netherite, and Microsoft SQL Server (MSSQL)*. The Azure managed option is the new *durable task scheduler* currently in preview. This article describes all supported backend providers, compares them against each other, and provides basic information about how to get started using them.

Note

It's not currently possible to migrate data from one storage backend provider to another. If you want to use a new provider, you should create a new app configured with the new provider.

## Durable task scheduler (preview)

The durable task scheduler is a fully managed, high performance backend provider for Durable Functions. It was designed and built from scratch with help from Microsoft Research. This new provider aims to provide the best user experience in aspects such as management, observability, performance, and security.

The key benefits of the durable task scheduler include:

- Lower management and operation overhead compared to BYO backend providers
- First-class observability and management
[dashboard](durable-task-scheduler/durable-task-scheduler-dashboard)provided out-of-the-box. - Supports the highest throughput of all backends today.
- Support for authentication using managed identity.

Existing Durable Functions users can leverage the scheduler with no code changes. Learn more about the [durable task scheduler](durable-task-scheduler/durable-task-scheduler), and [how to get started](durable-task-scheduler/quickstart-durable-task-scheduler).

Samples for durable task scheduler can be found on [GitHub](https://github.com/Azure-Samples/Durable-Task-Scheduler/).

## Azure Storage

Azure Storage is the default storage provider for Durable Functions. It uses queues, tables, and blobs to persist orchestration and entity state. It also uses blobs and blob leases to manage partitions. In many cases, the storage account used to store Durable Functions runtime state is the same as the default storage account used by Azure Functions (`AzureWebJobsStorage`

). However, it's also possible to configure Durable Functions with a separate storage account. The Azure Storage provider is built-into the Durable Functions extension and doesn't have any other dependencies.

The key benefits of the Azure Storage provider include:

- No setup required - you can use the storage account that was created for you by the function app setup experience.
- Lowest-cost serverless billing model - Azure Storage has a consumption-based pricing model based entirely on usage (
[more information](durable-functions-billing#azure-storage-transactions)). - Best tooling support - Azure Storage offers cross-platform local emulation and integrates with Visual Studio, Visual Studio Code, and the Azure Functions Core Tools.
- Most mature - Azure Storage was the original and most battle-tested storage backend for Durable Functions.
- Support for using identity instead of secrets for connecting to the storage provider.

The source code for the DTFx components of the Azure Storage storage provider can be found in the [Azure/durabletask](https://github.com/Azure/durabletask/tree/main/src/DurableTask.AzureStorage) GitHub repo.

Note

Standard general purpose Azure Storage accounts are required when using the Azure Storage provider. All other storage account types are not supported. We highly recommend using legacy v1 general purpose storage accounts because the newer v2 storage accounts can be more expensive for Durable Functions workloads. For more information on Azure Storage account types, see the [Storage account overview](../../storage/common/storage-account-overview) documentation.

## Netherite

Note

Support for using the Netherite storage backend with Durable Functions will end 31 March 2028. It is recommended that you start evaluating the Durable Task Scheduler for workloads that you're currently using Netherite for. See [end-of-support announcement](https://azure.microsoft.com/updates/?id=489009).

The Netherite storage backend was designed and developed by [Microsoft Research](https://www.microsoft.com/research). It uses [Azure Event Hubs](../../event-hubs/event-hubs-about) and the [FASTER](https://www.microsoft.com/research/project/faster/) database technology on top of [Azure Page Blobs](../../storage/blobs/storage-blob-pageblob-overview). The design of Netherite enables higher-throughput processing of orchestrations and entities compared to other providers. In some benchmark scenarios, throughput was shown to increase by more than an order of magnitude when compared to the default Azure Storage provider.

The key benefits of the Netherite storage provider include:

- Higher throughput at lower cost compared to other storage providers.
- Supports price-performance optimization, allowing you to scale-up performance as-needed.
- Supports up to 32 data partitions with Event Hubs Basic and Standard SKUs.
- More cost-effective than other providers for high-throughput workloads.

You can learn more about the technical details of the Netherite storage provider, including how to get started using it, in the [Netherite documentation](https://microsoft.github.io/durabletask-netherite). The source code for the Netherite storage provider can be found in the [microsoft/durabletask-netherite](https://github.com/microsoft/durabletask-netherite) GitHub repo. A more in-depth evaluation of the Netherite storage provider is also available in the following research paper: [Serverless Workflows with Durable Functions and Netherite](https://arxiv.org/abs/2103.00033).

Note

The *Netherite* name originates from the world of [Minecraft](https://minecraft.fandom.com/wiki/Netherite).

## Microsoft SQL Server (MSSQL)

The Microsoft SQL Server (MSSQL) storage provider persists all state into a Microsoft SQL Server database. It's compatible with both on-premises and cloud-hosted deployments of SQL Server, including [Azure SQL Database](/en-us/azure/azure-sql/database/sql-database-paas-overview).

The key benefits of the MSSQL storage provider include:

- Supports disconnected environments - no Azure connectivity is required when using a SQL Server installation.
- Portable across multiple environments and clouds, including Azure-hosted and on-premises.
- Strong data consistency, enabling backup/restore and failover without data loss.
- Native support for custom data encryption (a feature of SQL Server).
- Integrates with existing database applications via built-in stored procedures.

You can learn more about the technical details of the MSSQL storage provider, including how to get started using it, in the [Microsoft SQL provider documentation](https://microsoft.github.io/durabletask-mssql). The source code for the MSSQL storage provider can be found in the [microsoft/durabletask-mssql](https://github.com/microsoft/durabletask-mssql) GitHub repo.

## Configuring the Azure storage provider

The Azure Storage provider is the default storage provider and doesn't require any explicit configuration, NuGet package references, or extension bundle references. You can find the full set of **host.json** configuration options [here](durable-functions-bindings#durable-functions-settings-in-hostjson), under the `extensions/durableTask/storageProvider`

path.

### Connections

The `connectionName`

property in host.json is a reference to environment configuration which specifies how the app should connect to Azure Storage. It may specify:

- The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections). Managed identities use Microsoft Entra authentication to provide the most secure connection to your storage account. - The name of an application setting containing a connection string. To obtain a connection string, follow the steps shown at
[Manage storage account access keys](../../storage/common/storage-account-keys-manage).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used. If no value is specified in host.json, the default value is `AzureWebJobsStorage`

.

### Identity-based connections

If you are using [version 2.7.0 or higher of the extension](https://github.com/Azure/azure-functions-durable-extension/releases/tag/v2.7.0) and the Azure storage provider, instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the `connectionName`

property in the trigger and binding configuration.

To use an identity-based connection for Durable Functions, configure the following app settings:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Blob service URI | `<CONNECTION_NAME_PREFIX>__blobServiceUri` |
The data plane URI of the blob service of the storage account, using the HTTPS scheme. | https://<storage_account_name>.blob.core.windows.net |
| Queue service URI | `<CONNECTION_NAME_PREFIX>__queueServiceUri` |
The data plane URI of the queue service of the storage account, using the HTTPS scheme. | https://<storage_account_name>.queue.core.windows.net |
| Table service URI | `<CONNECTION_NAME_PREFIX>__tableServiceUri` |
The data plane URI of a table service of the storage account, using the HTTPS scheme. | https://<storage_account_name>.table.core.windows.net |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](../functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](../functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to Azure storage at runtime. Management roles like [Owner](../../role-based-access-control/built-in-roles#owner) aren't sufficient. The following built-in roles are recommended when using the Durable Functions extension in normal operation:

Your application may require more permissions based on the code you write. If you're using the default behavior or explicitly setting `connectionName`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](../functions-reference#connecting-to-host-storage-with-an-identity) for other permission considerations.

## Configuring alternate storage providers

Configuring alternate storage providers is generally a two-step process:

- Add the appropriate NuGet package to your function app (this requirement is temporary for apps using extension bundles).
- Update the
**host.json**file to specify which storage provider you want to use.

If no storage provider is explicitly configured in host.json, the Azure Storage provider will be enabled by default.

### Configuring durable task scheduler (preview)

See the [durable task scheduler getting started documentation](durable-task-scheduler/quickstart-durable-task-scheduler).

### Configuring the MSSQL storage provider

Enabling the MSSQL storage provider requires a configuration change in your `host.json`

. For C# users, it also requires an additional installation step.

`host.json`

Configuration

The following example shows the minimum configuration required to enable the MSSQL storage provider.

```
{
"version": "2.0",
"extensions": {
"durableTask": {
"storageProvider": {
"type": "mssql",
"connectionStringName": "SQLDB_Connection"
}
}
}
}
```


For more detailed setup instructions, see the [MSSQL provider's getting started documentation](quickstart-mssql) and [documentation on github.io](https://microsoft.github.io/durabletask-mssql/#/quickstart).

#### Install the Durable Task MSSQL extension (.NET only)

Note

If your app uses [Extension Bundles](../extension-bundles), you should ignore this section as Extension Bundles removes the need for manual Extension management.

You'll need to install the latest version of the MSSQL storage provider Extension on NuGet: [ Microsoft.Azure.Functions.Worker.Extensions.DurableTask.SqlServer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask.SqlServer). This usually means including a reference to it in your

`.csproj`

file and building the project.## Comparing storage providers

There are many significant tradeoffs between the various supported storage providers. The following table can be used to help you understand these tradeoffs and decide which storage provider is best for your needs.

Note

Support for using the Netherite storage backend with Durable Functions will end 31 March 2028. It is recommended that you start evaluating the Durable Task Scheduler for workloads that you're currently using Netherite for. See [end-of-support announcement](https://azure.microsoft.com/updates/?id=489009).

| Storage provider | Azure Storage | Netherite | MSSQL | DTS |
|---|---|---|---|---|
| Official support status | ✅ Generally available (GA) | ✅ Generally available (GA) | ✅ Generally available (GA) | Public preview |
| External dependencies | Azure Storage account (general purpose v1) | Azure Event Hubs Azure Storage account (general purpose) |
|

[Azurite v3.12+](../../storage/common/storage-use-azurite)(cross platform)[more information](https://microsoft.github.io/durabletask-netherite/#/emulation))[Windows](/en-us/sql/database-engine/install-windows/install-sql-server),[Linux](/en-us/sql/linux/sql-server-linux-setup), and[Docker containers](/en-us/sql/linux/sql-server-linux-docker-container-deployment))[Durable task scheduler emulator](durable-task-scheduler/durable-task-scheduler#emulator-for-local-development)[more information](https://microsoft.github.io/durabletask-mssql/#/taskhubs))[KEDA 2.0](https://keda.sh/)scaling support(

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-http-features -->

# HTTP Features

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Durable Functions has several features that make it easy to incorporate durable orchestrations and entities into HTTP workflows. This article goes into detail about some of those features.

## Exposing HTTP APIs

Orchestrations and entities can be invoked and managed using HTTP requests. The Durable Functions extension exposes built-in HTTP APIs. It also provides APIs for interacting with orchestrations and entities from within HTTP-triggered functions.

### Built-in HTTP APIs

The Durable Functions extension automatically adds a set of HTTP APIs to the Azure Functions host. With these APIs, you can interact with and manage orchestrations and entities without writing any code.

The following built-in HTTP APIs are supported.

[Start new orchestration](durable-functions-http-api#start-orchestration)[Query orchestration instance](durable-functions-http-api#get-instance-status)[Terminate orchestration instance](durable-functions-http-api#terminate-instance)[Send an external event to an orchestration](durable-functions-http-api#raise-event)[Purge orchestration history](durable-functions-http-api#purge-single-instance-history)[Send an operation event to an entity](durable-functions-http-api#signal-entity)[Get the state of an entity](durable-functions-http-api#get-entity)[Query the list of entities](durable-functions-http-api#list-entities)

See the [HTTP APIs article](durable-functions-http-api) for a full description of all the built-in HTTP APIs exposed by the Durable Functions extension.

### HTTP API URL discovery

The [orchestration client binding](durable-functions-bindings#orchestration-client) exposes APIs that can generate convenient HTTP response payloads. For example, it can create a response containing links to management APIs for a specific orchestration instance. The following examples show an HTTP-trigger function that demonstrates how to use this API for a new orchestration instance:

```
// Copyright (c) .NET Foundation. All rights reserved.
// Licensed under the MIT License. See LICENSE in the project root for license information.
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.DurableTask;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Logging;
namespace VSSample
{
public static class HttpStart
{
[FunctionName("HttpStart")]
public static async Task<HttpResponseMessage> Run(
[HttpTrigger(AuthorizationLevel.Function, methods: "post", Route = "orchestrators/{functionName}")] HttpRequestMessage req,
[DurableClient] IDurableClient starter,
string functionName,
ILogger log)
{
// Function input comes from the request content.
object eventData = await req.Content.ReadAsAsync<object>();
string instanceId = await starter.StartNewAsync(functionName, eventData);
log.LogInformation($"Started orchestration with ID = '{instanceId}'.");
return starter.CreateCheckStatusResponse(req, instanceId);
}
}
}
```


Starting an orchestrator function by using the HTTP-trigger functions shown previously can be done using any HTTP client. The following cURL command starts an orchestrator function named `DoWork`

:

```
curl -X POST https://localhost:7071/orchestrators/DoWork -H "Content-Length: 0" -i
```


Next is an example response for an orchestration that has `abc123`

as its ID. Some details have been removed for clarity.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: http://localhost:7071/runtime/webhooks/durabletask/instances/abc123?code=XXX
Retry-After: 10
{
"id": "abc123",
"purgeHistoryDeleteUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123?code=XXX",
"sendEventPostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123/raiseEvent/{eventName}?code=XXX",
"statusQueryGetUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123?code=XXX",
"terminatePostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123/terminate?reason={text}&code=XXX"
}
```


In the previous example, each of the fields ending in `Uri`

corresponds to a built-in HTTP API. You can use these APIs to manage the target orchestration instance.

Note

The format of the webhook URLs depends on which version of the Azure Functions host you are running. The previous example is for the Azure Functions 2.0 host.

For a description of all built-in HTTP APIs, see the [HTTP API reference](durable-functions-http-api).

### Async operation tracking

The HTTP response mentioned previously is designed to help implement long-running HTTP async APIs with Durable Functions. This pattern is sometimes referred to as the *polling consumer pattern*. The client/server flow works as follows:

- The client issues an HTTP request to start a long-running process like an orchestrator function.
- The target HTTP trigger returns an HTTP 202 response with a Location header that has the value "statusQueryGetUri".
- The client polls the URL in the Location header. The client continues to see HTTP 202 responses with a Location header.
- When the instance finishes or fails, the endpoint in the Location header returns HTTP 200.

This protocol allows coordination of long-running processes with external clients or services that can poll an HTTP endpoint and follow the Location header. Both the client and server implementations of this pattern are built into the Durable Functions HTTP APIs.

Note

By default, all HTTP-based actions provided by [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/) support the standard asynchronous operation pattern. This capability makes it possible to embed a long-running durable function as part of a Logic Apps workflow. You can find more details on Logic Apps support for asynchronous HTTP patterns in the [Azure Logic Apps workflow actions and triggers documentation](../../logic-apps/logic-apps-workflow-actions-triggers).

Note

Interactions with orchestrations can be done from any function type, not just HTTP-triggered functions.

For more information on how to manage orchestrations and entities using client APIs, see the [Instance management article](durable-functions-instance-management).

## Consuming HTTP APIs

As described in the [orchestrator function code constraints](durable-functions-code-constraints), orchestrator functions can't do I/O directly. Instead, they typically call [activity functions](durable-functions-types-features-overview#activity-functions) that do I/O operations.

Starting with Durable Functions 2.0, orchestrations can natively consume HTTP APIs by using the [orchestration trigger binding](durable-functions-bindings#orchestration-trigger).

The following example code shows an orchestrator function making an outbound HTTP request:

```
[FunctionName(nameof(CheckSiteAvailable))]
public static async Task CheckSiteAvailable(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
Uri url = context.GetInput<Uri>();
// Makes an HTTP GET request to the specified endpoint
DurableHttpResponse response =
await context.CallHttpAsync(HttpMethod.Get, url);
if (response.StatusCode >= 400)
{
// handling of error codes goes here
}
}
```


Note

You might wonder why this feature uses the **DurableHttpRequest** and **DurableHttpResponse** types instead of the built-in .NET **HttpRequestMessage** and **HttpResponseMessage** types.

This design choice is intentional. The primary reason is that custom types help ensure users don't make incorrect assumptions about the supported behaviors of the internal HTTP client. Types specific to Durable Functions also make it possible to simplify API design. They also can more easily make available special features like [managed identity integration](#managed-identities) and the [polling consumer pattern](#http-202-handling).

By using the "call HTTP" action, you can do the following actions in your orchestrator functions:

- Call HTTP APIs directly from orchestration functions, with some limitations that are mentioned later.
- Automatically support client-side HTTP 202 status polling patterns.
- Use
[Azure Managed Identities](../../active-directory/managed-identities-azure-resources/overview)to make authorized HTTP calls to other Azure endpoints.

The ability to consume HTTP APIs directly from orchestrator functions is intended as a convenience for a certain set of common scenarios. You can implement all of these features yourself using activity functions. In many cases, activity functions might give you more flexibility.

### HTTP 202 handling (.NET only)

The "call HTTP" API can automatically implement the client side of the polling consumer pattern. If a called API returns an HTTP 202 response with a Location header, the orchestrator function automatically polls the Location resource until receiving a response other than 202. This response will be the response returned to the orchestrator function code.

```
[FunctionName(nameof(CheckSiteAvailabilityWithPolling))]
public static async Task CheckSiteAvailabilityWithPolling(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
Uri url = context.GetInput<Uri>();
// HTTP automatic polling on 202 response is enabled by default in .NET in-process.
DurableHttpResponse response =
await context.CallHttpAsync(HttpMethod.Get, url);
}
```


Note

- Orchestrator functions also natively support the server-side polling consumer pattern, as described in
[Async operation tracking](#async-operation-tracking). This support means that orchestrations in one function app can easily coordinate the orchestrator functions in other function apps. This is similar to the[sub-orchestration](durable-functions-sub-orchestrations)concept, but with support for cross-app communication. This support is particularly useful for microservice-style app development. - The built-in HTTP polling pattern is currently available only in the .NET host.
- The polling pattern is enabled by default in .NET in-process but disabled by default in .NET Isolated. If you want to enable it in .NET Isolated, refer to the sample code and set the asynchronousPatternEnabled argument to true.
- HTTP automatic polling pattern is supported in Durable Functions .NET Isolated starting from version
[v1.5.0](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask/1.5.0)or later.

### Managed identities

Durable Functions natively supports calls to APIs that accept Microsoft Entra tokens for authorization. This support uses [Azure managed identities](../../active-directory/managed-identities-azure-resources/overview) to acquire these tokens.

The following code is an example of an orchestrator function. The function makes authenticated calls to restart a virtual machine by using the Azure Resource Manager [virtual machines REST API](/en-us/rest/api/compute/virtualmachines).

```
[FunctionName("RestartVm")]
public static async Task RunOrchestrator(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
string subscriptionId = "mySubId";
string resourceGroup = "myRG";
string vmName = "myVM";
string apiVersion = "2019-03-01";
// Automatically fetches an Azure AD token for resource = https://management.core.windows.net/.default
// and attaches it to the outgoing Azure Resource Manager API call.
var restartRequest = new DurableHttpRequest(
HttpMethod.Post,
new Uri($"https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.Compute/virtualMachines/{vmName}/restart?api-version={apiVersion}"),
tokenSource: new ManagedIdentityTokenSource("https://management.core.windows.net/.default"));
DurableHttpResponse restartResponse = await context.CallHttpAsync(restartRequest);
if (restartResponse.StatusCode != HttpStatusCode.OK)
{
throw new ArgumentException($"Failed to restart VM: {restartResponse.StatusCode}: {restartResponse.Content}");
}
}
```


In the previous example, the `tokenSource`

parameter is configured to acquire Microsoft Entra tokens for [Azure Resource Manager](../../azure-resource-manager/management/overview). The tokens are identified by the resource URI `https://management.core.windows.net/.default`

. The example assumes that the current function app either is running locally or was deployed as a function app with a managed identity. The local identity or the managed identity is assumed to have permission to manage VMs in the specified resource group `myRG`

.

At runtime, the configured token source automatically returns an OAuth 2.0 access token. The source then adds the token as a bearer token to the Authorization header of the outgoing request. This model is an improvement over manually adding authorization headers to HTTP requests for the following reasons:

- Token refresh is handled automatically. You don't need to worry about expired tokens.
- Tokens are never stored in the durable orchestration state.
- You don't need to write any code to manage token acquisition.

You can find a more complete example in the [precompiled C# RestartVMs sample](https://github.com/Azure/azure-functions-durable-extension/blob/dev/samples/precompiled/RestartVMs.cs).

Managed identities aren't limited to Azure resource management. You can use managed identities to access any API that accepts Microsoft Entra bearer tokens, including Azure services from Microsoft and web apps from partners. A partner's web app can even be another function app. For a list of Azure services from Microsoft that support authentication with Microsoft Entra ID, see [Azure services that support Microsoft Entra authentication](../../active-directory/managed-identities-azure-resources/services-support-managed-identities#azure-services-that-support-azure-ad-authentication).

### Limitations

The built-in support for calling HTTP APIs is a convenience feature. It's not appropriate for all scenarios.

HTTP requests sent by orchestrator functions and their responses are [serialized and persisted](durable-functions-serialization-and-persistence) as messages in the Durable Functions storage provider. This persistent queuing behavior ensures HTTP calls are [reliable and safe for orchestration replay](durable-functions-orchestrations#reliability). However, the persistent queuing behavior also has limitations:

- Each HTTP request involves additional latency when compared to a native HTTP client.
- Depending on the
[configured storage provider](durable-functions-storage-providers), large request or response messages can significantly degrade orchestration performance. For example, when using Azure Storage, HTTP payloads that are too large to fit into Azure Queue messages are compressed and stored in Azure Blob storage. - Streaming, chunked, and binary payloads aren't supported.
- The ability to customize the behavior of the HTTP client is limited.

If any of these limitations might affect your use case, consider instead using activity functions and language-specific HTTP client libraries to make outbound HTTP calls.

### Extensibility (.NET in-process only)

Customizing the behavior of the orchestration's internal HTTP client is possible using [Azure Functions .NET dependency injection](../functions-dotnet-dependency-injection) for the in-process worker. This ability can be useful for making small behavioral changes. It can also be useful for unit testing the HTTP client by injecting mock objects.

The following example demonstrates using dependency injection to disable TLS/SSL certificate validation for orchestrator functions that call external HTTP endpoints.

```
public class Startup : FunctionsStartup
{
public override void Configure(IFunctionsHostBuilder builder)
{
// Register own factory
builder.Services.AddSingleton<
IDurableHttpMessageHandlerFactory,
MyDurableHttpMessageHandlerFactory>();
}
}
public class MyDurableHttpMessageHandlerFactory : IDurableHttpMessageHandlerFactory
{
public HttpMessageHandler CreateHttpMessageHandler()
{
// Disable TLS/SSL certificate validation (not recommended in production!)
return new HttpClientHandler
{
ServerCertificateCustomValidationCallback =
HttpClientHandler.DangerousAcceptAnyServerCertificateValidator,
};
}
}
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/quickstart-powershell-vscode -->

# Quickstart: Create a PowerShell Durable Functions app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Durable Functions, a feature of [Azure Functions](../functions-overview), to write stateful functions in a serverless environment. You install Durable Functions by installing the [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) in Visual Studio Code. The extension manages state, checkpoints, and restarts in your application.

In this quickstart, you use the Durable Functions extension in Visual Studio Code to locally create and test a "hello world" Durable Functions app in Azure Functions. The Durable Functions app orchestrates and chains together calls to other functions. Then, you publish the function code to Azure. The tools you use are available via the Visual Studio Code extension.

## Prerequisites

To complete this quickstart, you need:

[Visual Studio Code](https://code.visualstudio.com/download)installed.The Visual Studio Code extension

[Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)installed.The latest version of

[Azure Functions Core Tools](../functions-run-local)installed.An HTTP test tool that keeps your data secure. For more information, see

[HTTP test tools](../functions-develop-local#http-test-tools).An Azure subscription. To use Durable Functions, you must have an Azure Storage account.


If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project.

In Visual Studio Code, select F1 (or select Ctrl/Cmd+Shift+P) to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create New Project**.Select

**Browse**. In the**Select Folder**dialog, go to a folder to use for your project, and then choose**Select**.At the prompts, provide the following information:

Prompt Action Description **Select a language for your function app project**Select **PowerShell**.Creates a local PowerShell Functions project. **Select a version**Select **Azure Functions v4**.You see this option only when Core Tools isn't already installed. In this case, Core Tools is installed the first time you run the app. **Select a template for your project's first function**Select **Skip for now**.**Select how you would like to open your project**Select **Open in current window**.Opens Visual Studio Code in the folder you selected.

Visual Studio Code installs Azure Functions Core Tools if it's required to create a project. It also creates a function app project in a folder. This project contains the [host.json](../functions-host-json) and [local.settings.json](../functions-develop-local#local-settings-file) configuration files.

A *package.json* file is also created in the root folder.

### Configure the function app to use PowerShell 7.4 and the standalone Durable Functions SDK

Open the *local.settings.json* file and confirm that a setting named `FUNCTIONS_WORKER_RUNTIME_VERSION`

is set to `7.4`

and a setting named `ExternalDurablePowerShellSDK`

is set to `true`

. If they are missing or if they are set to other values, update the contents of the file.

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "",
"FUNCTIONS_WORKER_RUNTIME": "powershell",
"FUNCTIONS_WORKER_RUNTIME_VERSION" : "7.4",
"ExternalDurablePowerShellSDK": "true"
}
}
```


Next, specify an entry for the DF SDK in your `requirements.psd1`

file, as in the example below:

```
# This file enables modules to be automatically managed by the Functions service.
# See https://aka.ms/functionsmanageddependency for additional information.
#
@{
# For latest supported version, go to 'https://www.powershellgallery.com/packages/AzureFunctions.PowerShell.Durable.SDK/'.
'AzureFunctions.PowerShell.Durable.SDK' = '2.*'
}
```


Make sure you use the latest version of the [AzureFunctions.PowerShell.Durable.SDK](https://www.powershellgallery.com/packages/AzureFunctions.PowerShell.Durable.SDK) module. The `2.*`

version specifier ensures you get the latest stable 2.x version.

Add the following line to your `profile.ps1`

file (typically, at the end of the file):

```
Import-Module AzureFunctions.PowerShell.Durable.SDK -ErrorAction Stop
```


## Create your functions

The most basic Durable Functions app has three functions:

**Orchestrator function**: A workflow that orchestrates other functions.**Activity function**: A function that is called by the orchestrator function, performs work, and optionally returns a value.**Client function**: A regular function in Azure that starts an orchestrator function. This example uses an HTTP-triggered function.

### Orchestrator function

Use a template to create the Durable Functions app code in your project.

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Enter **Durable Functions orchestrator**.Creates a Durable Functions app orchestration. **Provide a function name**Enter **HelloOrchestrator**.A name for your durable function.

You added an orchestrator to coordinate activity functions. Open *HelloOrchestrator/run.ps1* to see the orchestrator function. Each call to the Invoke-ActivityFunction cmdlet invokes an activity function named `Hello`

.

Next, you add the referenced `Hello`

activity function.

### Activity function

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions activity**.Creates an activity function. **Provide a function name**Enter **Hello**.The name of your activity function.

You added the `Hello`

activity function that is invoked by the orchestrator. Open *Hello/run.ps1* to see that it's taking a name as input and returning a greeting. An activity function is where you perform actions such as making a database call or performing a computation.

Finally, you add an HTTP-triggered function that starts the orchestration.

### Client function (HTTP starter)

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions HTTP starter**.Creates an HTTP starter function. **Provide a function name**Enter **HttpStart**.The name of your activity function. **Authorization level**Select **Anonymous**.For demo purposes, this value allows the function to be called without using authentication.

You added an HTTP-triggered function that starts an orchestration. Open *HttpStart/run.ps1* to check that it uses the Start-NewOrchestration cmdlet to start a new orchestration. Then it uses the New-OrchestrationCheckStatusResponse cmdlet to return an HTTP response that contains URLs that can be used to monitor and manage the new orchestration.

You now have a Durable Functions app that you can run locally and deploy to Azure.

Tip

This quickstart uses the standalone Durable Functions PowerShell SDK, which is now generally available and provides the best performance and latest features. For more information about the SDK and migration from the legacy built-in version, see the [standalone PowerShell SDK guide](durable-functions-powershell-v2-sdk-migration-guide).

## Test the function locally

Azure Functions Core Tools gives you the capability to run an Azure Functions project on your local development computer. You're prompted to install these tools the first time you start a function in Visual Studio.

To test your function, set a breakpoint in the

`Hello`

activity function code (in*Hello/run.ps1*). Select F5 or select**Debug: Start Debugging**in the command palette to start the function app project. Output from Core Tools appears in the terminal panel.Note

For more information about debugging, see

[Durable Functions diagnostics](durable-functions-diagnostics#debugging).Durable Functions requires an Azure storage account to run. When Visual Studio Code prompts you to select a storage account, choose

**Select storage account**.At the prompts, provide the following information to create a new storage account in Azure.

Prompt Action Description **Select subscription**Select the name of your subscription. Your Azure subscription. **Select a storage account**Select **Create a new storage account**.**Enter the name of the new storage account**Enter a unique name. The name of the storage account to create. **Select a resource group**Enter a unique name. The name of the resource group to create. **Select a location**Select an Azure region. Select a region that is close to you. In the terminal panel, copy the URL endpoint of your HTTP-triggered function.

Use your browser or an HTTP test tool to send an HTTP POST request to the URL endpoint.

Replace the last segment with the name of the orchestrator function (

`HelloOrchestrator`

). The URL should be similar to`http://localhost:7071/api/orchestrators/HelloOrchestrator`

.The response is the HTTP function's initial result. It lets you know that the durable orchestration started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs. For now, query the status of the orchestration.

Copy the URL value for

`statusQueryGetUri`

, paste it in the browser's address bar, and execute the request. You can also continue to use your HTTP test tool to issue the GET request.The request queries the orchestration instance for the status. You must get an eventual response, which shows the instance completed and includes the outputs or results of the durable function. It looks like this example:

`{ "name": "HelloOrchestrator", "instanceId": "9a528a9e926f4b46b7d3deaa134b7e8a", "runtimeStatus": "Completed", "input": null, "customStatus": null, "output": [ "Hello Tokyo!", "Hello Seattle!", "Hello London!" ], "createdTime": "2020-03-18T21:54:49Z", "lastUpdatedTime": "2020-03-18T21:54:54Z" }`

To stop debugging, in Visual Studio Code, select Shift+F5.


After you verify that the function runs correctly on your local computer, it's time to publish the project to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](../storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Test your function in Azure

Make sure the app setting named

`ExternalDurablePowerShellSDK`

is set to`true`

.Copy the URL of the HTTP trigger from the output panel. The URL that calls your HTTP-triggered function should be in this format:

`https://<functionappname>.azurewebsites.net/api/orchestrators/HelloOrchestrator`

Paste the new URL for the HTTP request in your browser's address bar. When you use the published app, you can expect to get the same status response that you got when you tested locally.


The PowerShell Durable Functions app that you created and published by using Visual Studio Code is ready to use.

## Clean up resources

If you no longer need the resources that you created to complete the quickstart, to avoid related costs in your Azure subscription, [delete the resource group](/en-us/azure/azure-resource-manager/management/delete-resource-group?tabs=azure-portal#delete-resource-group) and all related resources.

## Related content

- Learn about
[common Durable Functions app patterns](durable-functions-overview#application-patterns).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-perf-and-scale -->

# Performance and scale in Durable Functions (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To optimize performance and scalability, it's important to understand the unique scaling characteristics of [Durable Functions](durable-functions-overview). In this article, we explain how workers are scaled based on load, and how one can tune the various parameters.

## Worker scaling

A fundamental benefit of the [task hub concept](durable-functions-task-hubs) is that the number of workers that process task hub work items can be continuously adjusted. In particular, applications can add more workers (*scale out*) if the work needs to be processed more quickly, and can remove workers (*scale in*) if there is not enough work to keep the workers busy.
It is even possible to *scale to zero* if the task hub is completely idle. When scaled to zero, there are no workers at all; only the scale controller and the storage need to remain active.

The following diagram illustrates this concept:

### Automatic scaling

As with all Azure Functions running in the Consumption and Elastic Premium plans, Durable Functions supports auto-scale via the [Azure Functions scale controller](../event-driven-scaling#runtime-scaling). The Scale Controller monitors how long messages and tasks have to wait before they are processed. Based on these latencies it can decide whether to add or remove workers.

Note

Starting with Durable Functions 2.0, function apps can be configured to run within VNET-protected service endpoints in the Elastic Premium plan. In this configuration, the Durable Functions triggers initiate scale requests instead of the Scale Controller. For more information, see [Runtime scale monitoring](../functions-networking-options#elastic-premium-plan-with-virtual-network-triggers).

On a premium plan, automatic scaling can help to keep the number of workers (and therefore the operating cost) roughly proportional to the load that the application is experiencing.

### CPU usage

**Orchestrator functions** run their logic multiple times due to their replaying behavior. It's therefore important that orchestrator function threads do not perform CPU-intensive tasks, do I/O, or block for any reason. Any work that may require I/O, blocking, or multiple threads should be moved into activity functions.

**Activity functions** have all the same behaviors as regular queue-triggered functions. They can safely do I/O, execute CPU intensive operations, and use multiple threads. Because activity triggers are stateless, they can freely scale out to an unbounded number of VMs.

**Entity functions** are also executed on a single thread and operations are processed one-at-a-time. However, entity functions do not have any restrictions on the type of code that can be executed.

### Function timeouts

Activity, orchestrator, and entity functions are subject to the same [function timeouts](../functions-scale#timeout) as all Azure Functions. As a general rule, Durable Functions treats function timeouts the same way as unhandled exceptions thrown by the application code.

For example, if an activity times out, the function execution is recorded as a failure, and the orchestrator is notified and handles the timeout just like any other exception: retries take place if specified by the call, or an exception handler may be executed.

### Entity operation batching

To improve performance and reduce cost, a single work item may execute an entire batch of entity operations. On consumption plans, each batch is then billed as a single function execution.

By default, the maximum batch size is 50 for consumption plans and 5000 for all other plans. The maximum batch size can also be configured in the [host.json](durable-functions-bindings#host-json) file. If the maximum batch size is 1, batching is effectively disabled.

Note

If individual entity operations take a long time to execute, it may be beneficial to limit the maximum batch size to reduce the risk of [function timeouts](#function-timeouts), in particular on consumption plans.

## Instance caching

Generally, to process an [orchestration work item](durable-functions-task-hubs#work-items), a worker has to both

- Fetch the orchestration history.
- Replay the orchestrator code using the history.

If the same worker is processing multiple work items for the same orchestration, the storage provider can optimize this process by caching the history in the worker's memory, which eliminates the first step. Moreover, it can cache the mid-execution orchestrator, which eliminates the second step, the history replay, as well.

The typical effect of caching is reduced I/O against the underlying storage service, and overall improved throughput and latency. On the other hand, caching increases the memory consumption on the worker.

Instance caching is currently supported by the Azure Storage provider and by the Netherite storage provider. The table below provides a comparison.

| Azure Storage provider | Netherite storage provider | MSSQL storage provider | |
|---|---|---|---|
Instance caching |
Supported (.NET in-process worker only) |
Supported | Not supported |
Default setting |
Disabled | Enabled | n/a |
Mechanism |
Extended Sessions | Instance Cache | n/a |
Documentation |
See
|

[Instance cache](https://microsoft.github.io/durabletask-netherite/#/caching)Tip

Caching can reduce how often histories are replayed, but it cannot eliminate replay altogether. When developing orchestrators, we highly recommend testing them on a configuration that disables caching. This forced-replay behavior can useful for detecting [orchestrator function code constraints](durable-functions-code-constraints) violations at development time.

### Comparison of caching mechanisms

The providers use different mechanisms to implement caching, and offer different parameters to configure the caching behavior.

**Extended sessions**, as used by the Azure Storage provider, keep mid-execution orchestrators in memory until they are idle for some time. The parameters to control this mechanism are`extendedSessionsEnabled`

and`extendedSessionIdleTimeoutInSeconds`

. For more details, see the section[Extended sessions](durable-functions-azure-storage-provider#extended-sessions)of the Azure Storage provider documentation.

Note

Extended sessions are supported only in the .NET in-process worker.

- The
**Instance cache**, as used by the Netherite storage provider, keeps the state of all instances, including their histories, in the worker's memory, while keeping track of the total memory used. If the cache size exceeds the limit configured by`InstanceCacheSizeMB`

, the least recently used instance data is evicted. If`CacheOrchestrationCursors`

is set to true, the cache also stores the mid-execution orchestrators along with the instance state. For more details, see the section[Instance cache](https://microsoft.github.io/durabletask-netherite/#/caching)of the Netherite storage provider documentation.

Note

Instance caches work for all language SDKs, but the `CacheOrchestrationCursors`

option is available only for the .NET in-process worker.

## Concurrency throttles

A single worker instance can execute multiple [work items](durable-functions-task-hubs#work-items) concurrently. This helps to increase parallelism and more efficiently utilize the workers.
However, if a worker attempts to process too many work items at the same time, it may exhaust its available resources, such as the CPU load, the number of network connections, or the available memory.

To ensure that an individual worker does not overcommit, it may be necessary to throttle the per-instance concurrency. By limiting the number of functions that are concurrently running on each worker, we can avoid exhausting the resource limits on that worker.

Note

The concurrency throttles only apply locally, to limit what is currently being processed **per worker**. Thus, these throttles do not limit the total throughput of the system.

Tip

In some cases, throttling the per-worker concurrency can actually *increase* the total throughput of the system. This can occur when each worker takes less work, causing the scale controller to add more workers to keep up with the queues, which then increases the total throughput.

### Configuration of throttles

Activity, orchestrator, and entity function concurrency limits can be configured in the **host.json** file. The relevant settings are `durableTask/maxConcurrentActivityFunctions`

for activity functions and `durableTask/maxConcurrentOrchestratorFunctions`

for both orchestrator and entity functions. These settings control the maximum number of orchestrator, entity, or activity functions that are loaded into memory on a single worker.

Note

Orchestrations and entities are only loaded into memory when they are actively processing events or operations, or if [instance caching](durable-functions-perf-and-scale#instance-caching) is enabled. After executing their logic and awaiting (i.e. hitting an `await`

(C#) or `yield`

(JavaScript, Python) statement in the orchestrator function code), they may be unloaded from memory. Orchestrations and entities that are unloaded from memory don't count towards the `maxConcurrentOrchestratorFunctions`

throttle. Even if millions of orchestrations or entities are in the "Running" state, they only count towards the throttle limit when they are loaded into active memory. An orchestration that schedules an activity function similarly doesn't count towards the throttle if the orchestration is waiting for the activity to finish executing.

#### Functions 2.0

```
{
"extensions": {
"durableTask": {
"maxConcurrentActivityFunctions": 10,
"maxConcurrentOrchestratorFunctions": 10
}
}
}
```


#### Functions 1.x

```
{
"durableTask": {
"maxConcurrentActivityFunctions": 10,
"maxConcurrentOrchestratorFunctions": 10
}
}
```


### Language runtime considerations

The language runtime you select may impose strict concurrency restrictions or your functions. For example, Durable Function apps written in Python or PowerShell may only support running a single function at a time on a single VM. This can result in significant performance problems if not carefully accounted for. For example, if an orchestrator fans-out to 10 activities but the language runtime restricts concurrency to just one function, then 9 of the 10 activity functions will be stuck waiting for a chance to run. Furthermore, these 9 stuck activities will not be able to be load balanced to any other workers because the Durable Functions runtime will have already loaded them into memory. This becomes especially problematic if the activity functions are long-running.

If the language runtime you are using places a restriction on concurrency, you should update the Durable Functions concurrency settings to match the concurrency settings of your language runtime. This ensures that the Durable Functions runtime will not attempt to run more functions concurrently than is allowed by the language runtime, allowing any pending activities to be load balanced to other VMs. For example, if you have a Python app that restricts concurrency to 4 functions (perhaps it's only configured with 4 threads on a single language worker process or 1 thread on 4 language worker processes) then you should configure both `maxConcurrentOrchestratorFunctions`

and `maxConcurrentActivityFunctions`

to 4.

For more information and performance recommendations for Python, see [Improve throughput performance of Python apps in Azure Functions](../python-scale-performance-reference). The techniques mentioned in this Python developer reference documentation can have a substantial impact on Durable Functions performance and scalability.

## Partition count

Some of the storage providers use a *partitioning* mechanism and allow specifying a `partitionCount`

parameter.

When using partitioning, workers do not directly compete for individual work items. Instead, the work items are first grouped into `partitionCount`

partitions. These partitions are then assigned to workers. This partitioned approach to load distribution can help to reduce the total number of storage accesses required. Also, it can enable [instance caching](durable-functions-perf-and-scale#instance-caching) and improve locality because it creates *affinity*: all work items for the same instance are processed by the same worker.

Note

Partitioning limits scale out because at most `partitionCount`

workers can process work items from a partitioned queue.

The following table shows, for each storage provider, which queues are partitioned, and the allowable range and default values for the `partitionCount`

parameter.

| Azure Storage provider | Netherite storage provider | MSSQL storage provider | |
|---|---|---|---|
Instance messages |
Partitioned | Partitioned | Not partitioned |
Activity messages |
Not partitioned | Partitioned | Not partitioned |
Default `partitionCount` |
4 | 12 | n/a |
Maximum `partitionCount` |
16 | 32 | n/a |
Documentation |
See
|

[Partition count considerations](https://microsoft.github.io/durabletask-netherite/#/settings?id=partition-count-considerations)Warning

The partition count can no longer be changed after a task hub has been created. Thus, it is advisable to set it to a large enough value to accommodate future scale out requirements for the task hub instance.

### Configuration of partition count

The `partitionCount`

parameter can be specified in the **host.json** file. The following example host.json snippet sets the `durableTask/storageProvider/partitionCount`

property (or `durableTask/partitionCount`

in Durable Functions 1.x) to `3`

.

#### Durable Functions 2.x

```
{
"extensions": {
"durableTask": {
"storageProvider": {
"partitionCount": 3
}
}
}
}
```


#### Durable Functions 1.x

```
{
"extensions": {
"durableTask": {
"partitionCount": 3
}
}
}
```


## Considerations to minimize invocation latencies

Under normal circumstances, invocation requests (to activities, orchestrators, entities, etc.) should be processed rather quickly. However, there's no guarantee on the maximum latency of any invocation request as it depends on factors such as: the type of scale behavior your App Service Plan, your concurrency settings, and the size of your application's backlog. As such, we recommend investing in [stress testing](durable-functions-best-practice-reference#invest-in-stress-testing) to measure and optimize your application's tail latencies.

## Performance targets

When planning to use Durable Functions for a production application, it is important to consider the performance requirements early in the planning process. Some basic usage scenarios include:

**Sequential activity execution**: This scenario describes an orchestrator function that runs a series of activity functions one after the other. It most closely resembles the[Function Chaining](durable-functions-sequence)sample.**Parallel activity execution**: This scenario describes an orchestrator function that executes many activity functions in parallel using the[Fan-out, Fan-in](durable-functions-cloud-backup)pattern.**Parallel response processing**: This scenario is the second half of the[Fan-out, Fan-in](durable-functions-cloud-backup)pattern. It focuses on the performance of the fan-in. It's important to note that unlike fan-out, fan-in is done by a single orchestrator function instance, and therefore can only run on a single VM.**External event processing**: This scenario represents a single orchestrator function instance that waits on[external events](durable-functions-external-events), one at a time.**Entity operation processing**: This scenario tests how quickly a*single*[Counter entity](durable-functions-entities)can process a constant stream of operations.

We provide throughput numbers for these scenarios in the respective documentation for the storage providers. In particular:

- for the Azure Storage provider, see
[Performance Targets](durable-functions-azure-storage-provider#performance-targets). - for the Netherite storage provider, see
[Basic Scenarios](https://microsoft.github.io/durabletask-netherite/#/scenarios). - for the MSSQL storage provider, see
[Orchestration Throughput Benchmarks](https://microsoft.github.io/durabletask-mssql/#/scaling?id=orchestration-throughput-benchmarks).

Tip

Unlike fan-out, fan-in operations are limited to a single VM. If your application uses the fan-out, fan-in pattern and you are concerned about fan-in performance, consider sub-dividing the activity function fan-out across multiple [sub-orchestrations](durable-functions-sub-orchestrations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-custom-orchestration-status -->

# Custom orchestration status in Durable Functions (Azure Functions)

Custom orchestration status lets you set a custom status value for your orchestrator function. This status is provided via the [HTTP GetStatus API](durable-functions-http-api#get-instance-status) or the equivalent [SDK API](durable-functions-instance-management#query-instances) on the orchestration client object.

## Sample use cases

### Visualize progress

Clients can poll the status end point and display a progress UI that visualizes the current execution stage. The following sample demonstrates progress sharing:

Note

These C# examples are written for Durable Functions 2.x and are not compatible with Durable Functions 1.x. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

```
[FunctionName("E1_HelloSequence")]
public static async Task<List<string>> Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
var outputs = new List<string>();
outputs.Add(await context.CallActivityAsync<string>("E1_SayHello", "Tokyo"));
context.SetCustomStatus("Tokyo");
outputs.Add(await context.CallActivityAsync<string>("E1_SayHello", "Seattle"));
context.SetCustomStatus("Seattle");
outputs.Add(await context.CallActivityAsync<string>("E1_SayHello", "London"));
context.SetCustomStatus("London");
// returns ["Hello Tokyo!", "Hello Seattle!", "Hello London!"]
return outputs;
}
[FunctionName("E1_SayHello")]
public static string SayHello([ActivityTrigger] string name)
{
return $"Hello {name}!";
}
```


`E1_HelloSequence`

orchestrator function:

```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context){
const outputs = [];
outputs.push(yield context.df.callActivity("E1_SayHello", "Tokyo"));
context.df.setCustomStatus("Tokyo");
outputs.push(yield context.df.callActivity("E1_SayHello", "Seattle"));
context.df.setCustomStatus("Seattle");
outputs.push(yield context.df.callActivity("E1_SayHello", "London"));
context.df.setCustomStatus("London");
// returns ["Hello Tokyo!", "Hello Seattle!", "Hello London!"]
return outputs;
});
```


`E1_SayHello`

activity function:

```
module.exports = async function(context, name) {
return `Hello ${name}!`;
};
```


`E1_HelloSequence`

Orchestrator function

```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
output1 = yield context.call_activity('E1_SayHello', 'Tokyo')
context.set_custom_status('Tokyo')
output2 = yield context.call_activity('E1_SayHello', 'Seattle')
context.set_custom_status('Seattle')
output3 = yield context.call_activity('E1_SayHello', 'London')
context.set_custom_status('London')
return [output1, output2, output3]
main = df.Orchestrator.create(orchestrator_function)
```


`E1_SayHello`

Activity function

```
def main(name: str) -> str:
return f"Hello {name}!"
```


`E1_HelloSequence`

Orchestrator function

```
param($Context)
$output = @()
$output += Invoke-DurableActivity -FunctionName 'E1_SayHello' -Input 'Tokyo'
Set-DurableCustomStatus -CustomStatus 'Tokyo'
$output += Invoke-DurableActivity -FunctionName 'E1_SayHello' -Input 'Seattle'
Set-DurableCustomStatus -CustomStatus 'Seattle'
$output += Invoke-DurableActivity -FunctionName 'E1_SayHello' -Input 'London'
Set-DurableCustomStatus -CustomStatus 'London'
return $output
```


`E1_SayHello`

Activity function

```
param($name)
"Hello $name"
```


```
@FunctionName("HelloCities")
public String helloCitiesOrchestrator(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
String result = "";
result += ctx.callActivity("SayHello", "Tokyo", String.class).await() + ", ";
ctx.setCustomStatus("Tokyo");
result += ctx.callActivity("SayHello", "London", String.class).await() + ", ";
ctx.setCustomStatus("London");
result += ctx.callActivity("SayHello", "Seattle", String.class).await();
ctx.setCustomStatus("Seattle");
return result;
}
@FunctionName("SayHello")
public String sayHello(@DurableActivityTrigger(name = "name") String name) {
return String.format("Hello %s!", name);
}
```


And then the client will receive the output of the orchestration only when `CustomStatus`

field is set to "London":

```
[FunctionName("HttpStart")]
public static async Task<HttpResponseMessage> Run(
[HttpTrigger(AuthorizationLevel.Function, methods: "post", Route = "orchestrators/{functionName}")] HttpRequestMessage req,
[DurableClient] IDurableOrchestrationClient starter,
string functionName,
ILogger log)
{
// Function input comes from the request content.
dynamic eventData = await req.Content.ReadAsAsync<object>();
string instanceId = await starter.StartNewAsync(functionName, (string)eventData);
log.LogInformation($"Started orchestration with ID = '{instanceId}'.");
DurableOrchestrationStatus durableOrchestrationStatus = await starter.GetStatusAsync(instanceId);
while (durableOrchestrationStatus.CustomStatus.ToString() != "London")
{
await Task.Delay(200);
durableOrchestrationStatus = await starter.GetStatusAsync(instanceId);
}
HttpResponseMessage httpResponseMessage = new HttpResponseMessage(HttpStatusCode.OK)
{
Content = new StringContent(JsonConvert.SerializeObject(durableOrchestrationStatus))
};
return httpResponseMessage;
}
}
```


```
const df = require("durable-functions");
module.exports = async function(context, req) {
const client = df.getClient(context);
// Function input comes from the request content.
const eventData = req.body;
const instanceId = await client.startNew(req.params.functionName, undefined, eventData);
context.log(`Started orchestration with ID = '${instanceId}'.`);
let durableOrchestrationStatus = await client.getStatus(instanceId);
while (durableOrchestrationStatus.customStatus.toString() !== "London") {
await new Promise((resolve) => setTimeout(resolve, 200));
durableOrchestrationStatus = await client.getStatus(instanceId);
}
const httpResponseMessage = {
status: 200,
body: JSON.stringify(durableOrchestrationStatus),
};
return httpResponseMessage;
};
```


Note

In JavaScript, the `customStatus`

field will be set when the next `yield`

or `return`

action is scheduled.

```
import json
import logging
import azure.functions as func
import azure.durable_functions as df
from time import sleep
async def main(req: func.HttpRequest, starter: str) -> func.HttpResponse:
client = df.DurableOrchestrationClient(starter)
instance_id = await client.start_new(req.params.functionName, None, None)
logging.info(f"Started orchestration with ID = '{instance_id}'.")
durable_orchestration_status = await client.get_status(instance_id)
while durable_orchestration_status.custom_status != 'London':
sleep(0.2)
durable_orchestration_status = await client.get_status(instance_id)
return func.HttpResponse(body='Success', status_code=200, mimetype='application/json')
```


Note

In Python, the `custom_status`

field will be set when the next `yield`

or `return`

action is scheduled.

The feature is not currently implemented in PowerShell

```
@FunctionName("StartHelloCities")
public HttpResponseMessage startHelloCities(
@HttpTrigger(name = "req") HttpRequestMessage<Void> req,
@DurableClientInput(name = "durableContext") DurableClientContext durableContext,
final ExecutionContext context) throws InterruptedException {
DurableTaskClient client = durableContext.getClient();
String instanceId = client.scheduleNewOrchestrationInstance("HelloCities");
context.getLogger().info("Created new Java orchestration with instance ID = " + instanceId);
OrchestrationMetadata metadata;
try {
metadata = client.waitForInstanceStart(instanceId, Duration.ofMinutes(5), true);
} catch (TimeoutException ex) {
return req.createResponseBuilder(HttpStatus.INTERNAL_SERVER_ERROR).build();
}
while (metadata.readCustomStatusAs(String.class) != "London") {
Thread.sleep(200);
metadata = client.getInstanceMetadata(instanceId, true);
}
return req.createResponseBuilder(HttpStatus.OK).build();
}
```


### Output customization

Another interesting scenario is segmenting users by returning customized output based on unique characteristics or interactions. With the help of custom orchestration status, the client-side code will stay generic. All main modifications will happen on the server side as shown in the following sample:

```
[FunctionName("CityRecommender")]
public static void Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
int userChoice = context.GetInput<int>();
switch (userChoice)
{
case 1:
context.SetCustomStatus(new
{
recommendedCities = new[] {"Tokyo", "Seattle"},
recommendedSeasons = new[] {"Spring", "Summer"}
});
break;
case 2:
context.SetCustomStatus(new
{
recommendedCities = new[] {"Seattle, London"},
recommendedSeasons = new[] {"Summer"}
});
break;
case 3:
context.SetCustomStatus(new
{
recommendedCities = new[] {"Tokyo, London"},
recommendedSeasons = new[] {"Spring", "Summer"}
});
break;
}
// Wait for user selection and refine the recommendation
}
```


`CityRecommender`

orchestrator

```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context) {
const userChoice = context.df.getInput();
switch (userChoice) {
case 1:
context.df.setCustomStatus({
recommendedCities: [ "Tokyo", "Seattle" ],
recommendedSeasons: [ "Spring", "Summer" ],
});
break;
case 2:
context.df.setCustomStatus({
recommendedCities: [ "Seattle", "London" ],
recommendedSeasons: [ "Summer" ],
});
break;
case 3:
context.df.setCustomStatus({
recommendedCity: [ "Tokyo", "London" ],
recommendedSeasons: [ "Spring", "Summer" ],
});
break;
}
// Wait for user selection and refine the recommendation
});
```


`CityRecommender`

orchestrator

```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
userChoice = int(context.get_input())
if userChoice == 1:
context.set_custom_status({
'recommendedCities' : ['Tokyo', 'Seattle'],
'recommendedSeasons' : ['Spring', 'Summer']
}))
if userChoice == 2:
context.set_custom_status({
'recommendedCities' : ['Seattle', 'London']
'recommendedSeasons' : ['Summer']
}))
if userChoice == 3:
context.set_custom_status({
'recommendedCities' : ['Tokyo', 'London'],
'recommendedSeasons' : ['Spring', 'Summer']
}))
# Wait for user selection and refine the recommendation
main = df.Orchestrator.create(orchestrator_function)
```


`CityRecommender`

orchestrator

```
param($Context)
$userChoice = $Context.Input -as [int]
if ($userChoice -eq 1) {
Set-DurableCustomStatus -CustomStatus @{ recommendedCities = @('Tokyo', 'Seattle');
recommendedSeasons = @('Spring', 'Summer')
}
}
if ($userChoice -eq 2) {
Set-DurableCustomStatus -CustomStatus @{ recommendedCities = @('Seattle', 'London');
recommendedSeasons = @('Summer')
}
}
if ($userChoice -eq 3) {
Set-DurableCustomStatus -CustomStatus @{ recommendedCities = @('Tokyo', 'London');
recommendedSeasons = @('Spring', 'Summer')
}
}
# Wait for user selection and refine the recommendation
```


```
@FunctionName("CityRecommender")
public void cityRecommender(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
int userChoice = ctx.getInput(int.class);
switch (userChoice) {
case 1:
ctx.setCustomStatus(new Recommendation(
new String[]{ "Tokyo", "Seattle" },
new String[]{ "Spring", "Summer" }));
break;
case 2:
ctx.setCustomStatus(new Recommendation(
new String[]{ "Seattle", "London" },
new String[]{ "Summer" }));
break;
case 3:
ctx.setCustomStatus(new Recommendation(
new String[]{ "Tokyo", "London" },
new String[]{ "Spring", "Summer" }));
break;
}
// Wait for user selection with an external event
}
class Recommendation {
public Recommendation() { }
public Recommendation(String[] cities, String[] seasons) {
this.recommendedCities = cities;
this.recommendedSeasons = seasons;
}
public String[] recommendedCities;
public String[] recommendedSeasons;
}
```


### Instruction specification

The orchestrator can provide unique instructions to the clients via the custom state. The custom status instructions will be mapped to the steps in the orchestration code:

```
[FunctionName("ReserveTicket")]
public static async Task<bool> Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
string userId = context.GetInput<string>();
int discount = await context.CallActivityAsync<int>("CalculateDiscount", userId);
context.SetCustomStatus(new
{
discount = discount,
discountTimeout = 60,
bookingUrl = "https://www.myawesomebookingweb.com",
});
bool isBookingConfirmed = await context.WaitForExternalEvent<bool>("BookingConfirmed");
context.SetCustomStatus(isBookingConfirmed
? new {message = "Thank you for confirming your booking."}
: new {message = "The booking was not confirmed on time. Please try again."});
return isBookingConfirmed;
}
```


```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context) {
const userId = context.df.getInput();
const discount = yield context.df.callActivity("CalculateDiscount", userId);
context.df.setCustomStatus({
discount,
discountTimeout = 60,
bookingUrl = "https://www.myawesomebookingweb.com",
});
const isBookingConfirmed = yield context.df.waitForExternalEvent("bookingConfirmed");
context.df.setCustomStatus(isBookingConfirmed
? { message: "Thank you for confirming your booking." }
: { message: "The booking was not confirmed on time. Please try again." }
);
return isBookingConfirmed;
});
```


```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
userId = int(context.get_input())
discount = yield context.call_activity('CalculateDiscount', userId)
status = { 'discount' : discount,
'discountTimeout' : 60,
'bookingUrl' : "https://www.myawesomebookingweb.com",
}
context.set_custom_status(status)
is_booking_confirmed = yield context.wait_for_external_event('BookingConfirmed')
context.set_custom_status({'message': 'Thank you for confirming your booking.'} if is_booking_confirmed
else {'message': 'The booking was not confirmed on time. Please try again.'})
return is_booking_confirmed
main = df.Orchestrator.create(orchestrator_function)
```


```
param($Context)
$userId = $Context.Input -as [int]
$discount = Invoke-DurableActivity -FunctionName 'CalculateDiscount' -Input $userId
$status = @{
discount = $discount;
discountTimeout = 60;
bookingUrl = "https://www.myawesomebookingweb.com"
}
Set-DurableCustomStatus -CustomStatus $status
$isBookingConfirmed = Invoke-DurableActivity -FunctionName 'BookingConfirmed'
if ($isBookingConfirmed) {
Set-DurableCustomStatus -CustomStatus @{message = 'Thank you for confirming your booking.'}
} else {
Set-DurableCustomStatus -CustomStatus @{message = 'The booking was not confirmed on time. Please try again.'}
}
return $isBookingConfirmed
```


```
@FunctionName("ReserveTicket")
public boolean reserveTicket(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
String userID = ctx.getInput(String.class);
int discount = ctx.callActivity("CalculateDiscount", userID, int.class).await();
ctx.setCustomStatus(new DiscountInfo(discount, 60, "https://www.myawesomebookingweb.com"));
boolean isConfirmed = ctx.waitForExternalEvent("BookingConfirmed", boolean.class).await();
if (isConfirmed) {
ctx.setCustomStatus("Thank you for confirming your booking.");
} else {
ctx.setCustomStatus("There was a problem confirming your booking. Please try again.");
}
return isConfirmed;
}
class DiscountInfo {
public DiscountInfo() { }
public DiscountInfo(int discount, int discountTimeout, String bookingUrl) {
this.discount = discount;
this.discountTimeout = discountTimeout;
this.bookingUrl = bookingUrl;
}
public int discount;
public int discountTimeout;
public String bookingUrl;
}
```


## Querying custom status with HTTP

The following example shows how custom status values can be queried using the built-in HTTP APIs.

```
public static async Task SetStatusTest([OrchestrationTrigger] IDurableOrchestrationContext context)
{
// ...do work...
// update the status of the orchestration with some arbitrary data
var customStatus = new { nextActions = new [] {"A", "B", "C"}, foo = 2, };
context.SetCustomStatus(customStatus);
// ...do more work...
}
```


```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context) {
// ...do work...
// update the status of the orchestration with some arbitrary data
const customStatus = { nextActions: [ "A", "B", "C" ], foo: 2, };
context.df.setCustomStatus(customStatus);
// ...do more work...
});
```


```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
# ...do work...
custom_status = {'nextActions': ['A','B','C'], 'foo':2}
context.set_custom_status(custom_status)
# ...do more work...
main = df.Orchestrator.create(orchestrator_function)
```


```
param($Context)
# ...do work...
Set-DurableCustomStatus -CustomStatus @{ nextActions = @('A', 'B', 'C');
foo = 2
}
# ...do more work...
```


```
@FunctionName("MyCustomStatusOrchestrator")
public void myCustomStatusOrchestrator(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
// ... do work ...
// update the status of the orchestration with some arbitrary data
CustomStatusPayload payload = new CustomStatusPayload();
payload.nextActions = new String[] { "A", "B", "C" };
payload.foo = 2;
ctx.setCustomStatus(payload);
// ... do more work ...
}
class CustomStatusPayload {
public String[] nextActions;
public int foo;
}
```


While the orchestration is running, external clients can fetch this custom status:

```
GET /runtime/webhooks/durabletask/instances/instance123
```


Clients will get the following response:

```
{
"runtimeStatus": "Running",
"input": null,
"customStatus": { "nextActions": ["A", "B", "C"], "foo": 2 },
"output": null,
"createdTime": "2019-10-06T18:30:24Z",
"lastUpdatedTime": "2019-10-06T19:40:30Z"
}
```


Warning

The custom status payload is limited to 16 KB of UTF-16 JSON text. We recommend you use external storage if you need a larger payload.

## Next steps

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-orchestrations -->

# Durable orchestrations

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Durable Functions is an extension of [Azure Functions](../functions-overview) that provides a way to run stateful functions in a serverless compute environment. Within a durable function app, you can use an *orchestrator function* to orchestrate the execution of other durable functions. Orchestrator functions have the following characteristics:

- They define function workflows by using procedural code. No declarative schemas or designers are needed.
- They can call other durable functions synchronously and asynchronously. Output from called functions can be saved to local variables.
- They're designed to be durable and reliable. Execution progress is automatically saved as a checkpoint when the function calls an
`await`

or`yield`

operator. Local state isn't lost when the process recycles or the virtual machine reboots. - They can be long running. The total lifespan of an
*orchestration instance*can be seconds, days, or months, or the instance can be configured to never end.

This article gives you an overview of orchestrator functions and how they can help you solve various app development challenges. For information about the types of functions available in a Durable Functions app, see [Durable Functions types and features](durable-functions-types-features-overview).

## Orchestration identity

Each *instance* of an orchestration has an instance identifier, also known as an *instance ID*. By default, each instance ID is an autogenerated globally unique identifier (GUID). However, instance IDs can also be any user-generated string value. Each orchestration instance ID must be unique within a [task hub](durable-functions-task-hubs).

The following rules apply to instance IDs:

- They must be between 1 and 100 characters.
- They must not start with
`@`

. - They must not contain
`/`

,`\`

,`#`

, or`?`

characters. - They must not contain control characters.

Note

We generally recommend that you use autogenerated instance IDs whenever possible. User-generated instance IDs are intended for scenarios where there's a one-to-one mapping between an orchestration instance and an external application-specific entity, like a purchase order or a document.

Also, the actual enforcement of character restriction rules can vary depending on the [storage provider](durable-functions-storage-providers) that the app uses. To help ensure correct behavior and compatibility, we strongly recommend that you follow the preceding instance ID rules.

An orchestration's instance ID is a required parameter for most [instance management operations](durable-functions-instance-management). Instance IDs are also important for diagnostics. For instance, you use them when you [search through orchestration tracking data](durable-functions-diagnostics#application-insights) in Application Insights for troubleshooting or analytics purposes. For this reason, we recommend that you save generated instance IDs to an external location that makes it easy to reference them later. Examples of locations include databases or application logs.

## Reliability

Orchestrator functions use the [event sourcing](/en-us/azure/architecture/patterns/event-sourcing) design pattern to help maintain their execution state reliably. Instead of directly storing the current state of an orchestration, the Durable Task Framework uses an append-only store to record the full series of actions the function orchestration takes. An append-only store has many benefits compared to *dumping* the full runtime state. Benefits include increased performance, scalability, and responsiveness. You also get eventual consistency for transactional data and full audit trails and history. The audit trails support reliable compensating actions.

Durable Functions uses event sourcing transparently. Behind the scenes, an orchestrator function uses an `await`

operator in C# and a `yield`

operator in JavaScript and Python. These operators yield control of the orchestrator thread back to the Durable Task Framework dispatcher. In Java functions, there's no special language keyword. Instead, calling `.await()`

on a task yields control back to the dispatcher via a custom instance of `Throwable`

. The dispatcher then commits any new actions scheduled by the orchestrator function to storage. Examples of actions include calling one or more child functions or scheduling a durable timer. The transparent commit action updates the execution history of the orchestration instance by appending all new events into storage, much like an append-only log. Similarly, the commit action creates messages in storage to schedule the actual work. At this point, the orchestrator function can be unloaded from memory. By default, Durable Functions uses Azure Storage as its runtime state store, but other [storage providers are also supported](durable-functions-storage-providers).

When an orchestration function is given more work to do (for example, a response message is received or a durable timer expires), the orchestrator wakes up and re-executes the entire function from the start to rebuild the local state. During the replay, if the code tries to call a function (or do any other asynchronous work), the Durable Task Framework consults the execution history of the current orchestration. If it finds that the [activity function](durable-functions-types-features-overview#activity-functions) has already executed and yielded a result, it replays that function's result, and the orchestrator code continues to run. Replay continues until the function code is finished or until it schedules new asynchronous work.

Note

To help the replay pattern work correctly and reliably, orchestrator function code must be *deterministic*. Nondeterministic orchestrator code can result in runtime errors or other unexpected behavior. For more information about code restrictions for orchestrator functions, see [Orchestrator function code constraints](durable-functions-code-constraints).

Note

If an orchestrator function emits log messages, the replay behavior can cause duplicate log messages to be emitted. For more information about why this behavior occurs and how to work around it, see [App logging](durable-functions-diagnostics#app-logging).

## Orchestration history

The event-sourcing behavior of the Durable Task Framework is closely coupled with the orchestrator function code you write. Suppose you have an activity-chaining orchestrator function, like the following orchestrator function.

Note

Version 4 of the Node.js programming model for Azure Functions is generally available. The v4 model is designed to provide a more flexible and intuitive experience for JavaScript and TypeScript developers. For more information about the differences between v3 and v4, see the [migration guide](../functions-node-upgrade-v4).

In the following code snippets, JavaScript (PM4) denotes programming model v4, the new experience.

```
[FunctionName("HelloCities")]
public static async Task<List<string>> Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
var outputs = new List<string>();
outputs.Add(await context.CallActivityAsync<string>("SayHello", "Tokyo"));
outputs.Add(await context.CallActivityAsync<string>("SayHello", "Seattle"));
outputs.Add(await context.CallActivityAsync<string>("SayHello", "London"));
// Return ["Hello Tokyo!", "Hello Seattle!", "Hello London!"].
return outputs;
}
```


Whenever an activity function is scheduled, the Durable Task Framework saves the execution state of the function at various checkpoints. At each checkpoint, the framework saves the state into a durable storage back end, which is Azure Table Storage by default. This state is referred to as the *orchestration history*.

### History table

Generally speaking, the Durable Task Framework does the following at each checkpoint:

- Saves the execution history into durable storage.
- Enqueues messages for functions the orchestrator wants to invoke.
- Enqueues messages for the orchestrator itself, such as durable timer messages.

When the checkpoint is complete, the orchestrator function is free to be removed from memory until there's more work for it to do.

Note

Azure Storage doesn't provide any transactional guarantees about data consistency between table storage and queues when the data is saved. To handle failures, the [Durable Functions Azure Storage](durable-functions-storage-providers#azure-storage) provider uses *eventual consistency* patterns. These patterns help ensure that no data is lost if there's a crash or loss of connectivity in the middle of a checkpoint. Alternate storage providers, such as the [Durable Functions Microsoft SQL Server (MSSQL) storage provider](durable-functions-storage-providers#mssql), might provide stronger consistency guarantees.

When the function shown earlier finishes, its history looks something like the data in the following table in Table Storage. The entries are abbreviated for illustration purposes.

| PartitionKey (InstanceId) | EventType | Timestamp | Input | Name | Result | Status |
|---|---|---|---|---|---|---|
| eaee885b | ExecutionStarted | 2021-05-05T18:45:28.852Z | null | HelloCities | ||
| eaee885b | OrchestratorStarted | 2021-05-05T18:45:32.362Z | ||||
| eaee885b | TaskScheduled | 2021-05-05T18:45:32.670Z | SayHello | |||
| eaee885b | OrchestratorCompleted | 2021-05-05T18:45:32.670Z | ||||
| eaee885b | TaskCompleted | 2021-05-05T18:45:34.201Z | """Hello Tokyo!""" | |||
| eaee885b | OrchestratorStarted | 2021-05-05T18:45:34.232Z | ||||
| eaee885b | TaskScheduled | 2021-05-05T18:45:34.435Z | SayHello | |||
| eaee885b | OrchestratorCompleted | 2021-05-05T18:45:34.435Z | ||||
| eaee885b | TaskCompleted | 2021-05-05T18:45:34.763Z | """Hello Seattle!""" | |||
| eaee885b | OrchestratorStarted | 2021-05-05T18:45:34.857Z | ||||
| eaee885b | TaskScheduled | 2021-05-05T18:45:34.857Z | SayHello | |||
| eaee885b | OrchestratorCompleted | 2021-05-05T18:45:34.857Z | ||||
| eaee885b | TaskCompleted | 2021-05-05T18:45:34.919Z | """Hello London!""" | |||
| eaee885b | OrchestratorStarted | 2021-05-05T18:45:35.032Z | ||||
| eaee885b | OrchestratorCompleted | 2021-05-05T18:45:35.044Z | ||||
| eaee885b | ExecutionCompleted | 2021-05-05T18:45:35.044Z | "[""Hello Tokyo!"",""Hello Seattle!"",""Hello London!""]" | Completed |

The table columns contain the following values:

**PartitionKey**: The instance ID of the orchestration.**EventType**: The type of the event. For detailed descriptions of all the history event types, see[Durable Task Framework History Events](https://github.com/Azure/durabletask/tree/main/src/DurableTask.Core/History#readme).**Timestamp**: The Coordinated Universal Time timestamp of the history event.**Input**: The JSON-formatted input of the function.**Name**: The name of the invoked function.**Result**: The output of the function, specifically, its return value.

Warning

This table can be useful as a debugging tool. But keep in mind that its format and content might change as the Durable Functions extension evolves.

Every time the function is resumed after waiting for a task to complete, the Durable Task Framework reruns the orchestrator function from scratch. On each rerun, it consults the execution history to determine whether the current asynchronous task is complete. If the execution history shows that the task is already complete, the framework replays the output of that task and moves on to the next task. This process continues until the entire execution history has been replayed. As soon as the current execution history has been replayed, the local variables will have been restored to their previous values.

## Features and patterns

The following sections describe the features and patterns of orchestrator functions.

### Sub-orchestrations

Orchestrator functions can call activity functions, but also other orchestrator functions. For example, you can build a larger orchestration out of a library of orchestrator functions. Or, you can run multiple instances of an orchestrator function in parallel.

For more information and for examples, see [Sub-orchestrations in Durable Functions (Azure Functions)](durable-functions-sub-orchestrations).

### Durable timers

Orchestrations can schedule *durable timers* to implement delays or to set up timeout handling on asynchronous actions. Use durable timers in orchestrator functions instead of language-native `sleep`

APIs.

For more information and for examples, see [Timers in Durable Functions (Azure Functions)](durable-functions-timers).

### External events

Orchestrator functions can wait for external events to update an orchestration instance. This Durable Functions feature is often useful for handling human interactions or other external callbacks.

For more information and for examples, see [Handling external events in Durable Functions (Azure Functions)](durable-functions-external-events).

### Error handling

Orchestrator functions can use the error-handling features of the programming language. Existing patterns like `try`

/`catch`

are supported in orchestration code.

Orchestrator functions can also add retry policies to the activity or sub-orchestrator functions that they call. If an activity or sub-orchestrator function fails with an exception, the specified retry policy can automatically delay and retry the execution up to a specified number of times.

Note

If there's an unhandled exception in an orchestrator function, the orchestration instance finishes in a `Failed`

state. An orchestration instance can't be retried after it fails.

For more information and for examples, see [Handling errors in Durable Functions (Azure Functions)](durable-functions-error-handling).

### Critical sections (Durable Functions 2.x, currently .NET only)

Orchestration instances are single-threaded, so race conditions aren't a concern *within* an orchestration. However, race conditions are possible when orchestrations interact with external systems. To mitigate race conditions when interacting with external systems, orchestrator functions can define *critical sections* by using a `LockAsync`

method in .NET.

The following sample code shows an orchestrator function that defines a critical section. It uses the `LockAsync`

method to enter the critical section. This method requires passing one or more references to a [durable entity](durable-functions-entities), which durably manages the lock state. Only a single instance of this orchestration can execute the code in the critical section at a time.

```
[FunctionName("Synchronize")]
public static async Task Synchronize(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
var lockId = new EntityId("LockEntity", "MyLockIdentifier");
using (await context.LockAsync(lockId))
{
// Critical section. Only one orchestration can enter at a time.
}
}
```


The `LockAsync`

method acquires the durable locks and returns an `IDisposable`

that ends the critical section when disposed. This `IDisposable`

result can be used together with a `using`

block to get a syntactic representation of the critical section. When an orchestrator function enters a critical section, only one instance can execute that block of code. Any other instances that try to enter the critical section are blocked until the previous instance exits the critical section.

The critical section feature is also useful for coordinating changes to durable entities. For more information about critical sections, see [Entity coordination](durable-functions-entities#entity-coordination).

Note

Critical sections are available in Durable Functions 2.0. Currently, only .NET in-process orchestrations implement this feature. Entities and critical sections aren't yet available in Durable Functions for .NET isolated worker orchestrations.

### Calls to HTTP endpoints (Durable Functions 2.x)

Orchestrator functions aren't permitted to do I/O operations, as described in [Orchestrator function code constraints](durable-functions-code-constraints). The typical workaround for this limitation is to wrap any code that needs to do I/O operations in an activity function. Orchestrations that interact with external systems frequently use activity functions to make HTTP calls and return the results to the orchestration.

To streamline this common pattern, orchestrator functions can use the `CallHttpAsync`

method to invoke HTTP APIs directly.

```
[FunctionName("CheckSiteAvailable")]
public static async Task CheckSiteAvailable(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
Uri url = context.GetInput<Uri>();
// Make an HTTP GET request to the specified endpoint.
DurableHttpResponse response =
await context.CallHttpAsync(HttpMethod.Get, url);
if ((int)response.StatusCode == 400)
{
// Handle error codes.
}
}
```


Besides supporting basic request/response patterns, the method supports automatic handling of common asynchronous HTTP 202 polling patterns. It also supports authentication with external services by using [managed identities](/en-us/entra/identity/managed-identities-azure-resources/overview).

For more information and for detailed examples, see [HTTP features](durable-functions-http-features).

Note

Calling HTTP endpoints directly from orchestrator functions is available in Durable Functions 2.0 and later.

### Multiple parameters

It isn't possible to pass multiple parameters to an activity function directly. The recommendation is to pass in an array of objects or composite objects.

In .NET, you can also use [ValueTuple](/en-us/dotnet/csharp/language-reference/builtin-types/value-tuples) objects to pass multiple parameters. The following sample uses [ValueTuple](/en-us/dotnet/csharp/language-reference/builtin-types/value-tuples) features added with [C# 7](/en-us/dotnet/csharp/whats-new/csharp-version-history#c-version-70):

```
[FunctionName("GetCourseRecommendations")]
public static async Task<object> RunOrchestrator(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
string major = "ComputerScience";
int universityYear = context.GetInput<int>();
object courseRecommendations = await context.CallActivityAsync<object>(
"CourseRecommendations",
(major, universityYear));
return courseRecommendations;
}
[FunctionName("CourseRecommendations")]
public static async Task<object> Mapper([ActivityTrigger] IDurableActivityContext inputs)
{
// Parse the input for the student's major and year in university.
(string Major, int UniversityYear) studentInfo = inputs.GetInput<(string, int)>();
// Retrieve and return course recommendations by major and university year.
return new
{
major = studentInfo.Major,
universityYear = studentInfo.UniversityYear,
recommendedCourses = new []
{
"Introduction to .NET Programming",
"Introduction to Linux",
"Becoming an Entrepreneur"
}
};
}
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-task-hubs -->

# Task hubs in Durable Functions (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A *task hub* in [Durable Functions](durable-functions-overview) is a representation of the current state of the application in storage, including all the pending work. While a function app is running, the progress of orchestration, activity, and entity functions is continually stored in the task hub. This ensures that the application can resume processing where it left off, should it require to be restarted after being temporarily stopped or interrupted for some reason. Also, it allows the function app to scale the compute workers dynamically.

Conceptually, a task hub stores the following information:

- The
**instance states**of all orchestration and entity instances. - The messages to be processed, including
- any
**activity messages**that represent activities waiting to be run. - any
**instance messages**that are waiting to be delivered to instances.

- any

The difference between activity and instance messages is that activity messages are stateless, and can thus be processed anywhere, while instance messages need to be delivered to a particular stateful instance (orchestration or entity), identified by its instance ID.

Internally, each storage provider may use a different organization to represent instance states and messages. For example, messages are stored in Azure Storage Queues by the Azure Storage provider, but in relational tables by the MSSQL provider. These differences don't matter as far as the design of the application is concerned, but some of them may influence the performance characteristics. We discuss them in the section [Representation in storage](durable-functions-task-hubs#representation-in-storage) below.

## Work items

The activity messages and instance messages in the task hub represent the work that the function app needs to process. While the function app is running, it continuously fetches *work items* from the task hub. Each work item is processing one or more messages. We distinguish two types of work items:

**Activity work items**: Run an activity function to process an activity message.**Orchestrator work item**: Run an orchestrator or entity function to process one or more instance messages.

Workers can process multiple work items at the same time, subject to the [configured per-worker concurrency limits](durable-functions-perf-and-scale#concurrency-throttles).

Once a worker completes a work item, it commits the effects back to the task hub. These effects vary by the type of function that was executed:

- A completed activity function creates an instance message containing the result, addressed to the parent orchestrator instance.
- A completed orchestrator function updates the orchestration state and history, and may create new messages.
- A completed entity function updates the entity state, and may also create new instance messages.

For orchestrations, each work item represents one **episode** of that orchestration's execution. An episode starts when there are new messages for the orchestrator to process. Such a message may indicate that the orchestration should start; or it may indicate that an activity, entity call, timer, or suborchestration has completed; or it can represent an external event. The message triggers a work item that allows the orchestrator to process the result and to continue with the next episode. That episode ends when the orchestrator either completes, or reaches a point where it must wait for new messages.

### Execution example

Consider a fan-out-fan-in orchestration that starts two activities in parallel, and waits for both of them to complete:

```
[FunctionName("Example")]
public static async Task Run([OrchestrationTrigger] IDurableOrchestrationContext context)
{
Task t1 = context.CallActivityAsync<int>("MyActivity", 1);
Task t2 = context.CallActivityAsync<int>("MyActivity", 2);
await Task.WhenAll(t1, t2);
}
```


After this orchestration is initiated by a client it's processed by the function app as a sequence of work items. Each completed work item updates the task hub state when it commits. These are the steps:

A client requests to start a new orchestration with instance-id "123". After the client completes this request, the task hub contains a placeholder for the orchestration state and an instance message:

The label

`ExecutionStarted`

is one of many[history event types](https://github.com/Azure/durabletask/tree/main/src/DurableTask.Core/History#readme)that identify the various types of messages and events participating in an orchestration's history.A worker executes an

*orchestrator work item*to process the`ExecutionStarted`

message. It calls the orchestrator function which starts executing the orchestration code. This code schedules two activities and then stops executing when it is waiting for the results. After the worker commits this work item, the task hub containsThe runtime state is now

`Running`

, two new`TaskScheduled`

messages were added, and the history now contains the five events`OrchestratorStarted`

,`ExecutionStarted`

,`TaskScheduled`

,`TaskScheduled`

,`OrchestratorCompleted`

. These events represent the first episode of this orchestration's execution.A worker executes an

*activity work item*to process one of the`TaskScheduled`

messages. It calls the activity function with input "2". When the activity function completes, it creates a`TaskCompleted`

message containing the result. After the worker commits this work item, the task hub containsA worker executes an

*orchestrator work item*to process the`TaskCompleted`

message. If the orchestration is still cached in memory, it can just resume execution. Otherwise, the worker first[replays the history to recover the current state of the orchestration](durable-functions-orchestrations#reliability). Then it continues the orchestration, delivering the result of the activity. After receiving this result, the orchestration is still waiting for the result of the other activity, so it once more stops executing. After the worker commits this work item, the task hub containsThe orchestration history now contains three more events

`OrchestratorStarted`

,`TaskCompleted`

,`OrchestratorCompleted`

. These events represent the second episode of this orchestration's execution.A worker executes an

*activity work item*to process the remaining`TaskScheduled`

message. It calls the activity function with input "1". After the worker commits this work item, the task hub containsA worker executes another

*orchestrator work item*to process the`TaskCompleted`

message. After receiving this second result, the orchestration completes. After the worker commits this work item, the task hub containsThe runtime state is now

`Completed`

, and the orchestration history now contains four more events`OrchestratorStarted`

,`TaskCompleted`

,`ExecutionCompleted`

,`OrchestratorCompleted`

. These events represent the third and final episode of this orchestration's execution.

The final history for this orchestration's execution then contains the 12 events `OrchestratorStarted`

, `ExecutionStarted`

, `TaskScheduled`

, `TaskScheduled`

, `OrchestratorCompleted`

, `OrchestratorStarted`

, `TaskCompleted`

, `OrchestratorCompleted`

, `OrchestratorStarted`

, `TaskCompleted`

, `ExecutionCompleted`

, `OrchestratorCompleted`

.

Note

The schedule shown isn't the only one: there are many slightly different possible schedules. For example, if the second activity completes earlier, both `TaskCompleted`

instance messages may be processed by a single work item. In that case, the execution history is a bit shorter, because there are only two episodes, and it contains the following 10 events: `OrchestratorStarted`

, `ExecutionStarted`

, `TaskScheduled`

, `TaskScheduled`

, `OrchestratorCompleted`

, `OrchestratorStarted`

, `TaskCompleted`

, `TaskCompleted`

, `ExecutionCompleted`

, `OrchestratorCompleted`

.

## Task hub management

Next, let's take a closer look at how task hubs are created or deleted, how to use task hubs correctly when running multiple function apps, and how the content of task hubs can be inspected.

### Creation and deletion

An empty task hub with all the required resources is automatically created in storage when a function app is started the first time.

If using the default Azure Storage provider, no extra configuration is required. Otherwise, follow the [instructions for configuring storage providers](durable-functions-storage-providers#configuring-alternate-storage-providers) to ensure that the storage provider can properly provision and access the storage resources required for the task hub.

Note

The task hub is *not* automatically deleted when you stop or delete the function app. You must delete the task hub, its contents, or the containing storage account manually if you no longer want to keep that data.

Tip

In a development scenario, you may need to restart from a clean state often. To do so quickly, you can just [change the configured task hub name](durable-functions-task-hubs#task-hub-names). This will force the creation of a new, empty task hub when you restart the application. Be aware that the old data is not deleted in this case.

### Multiple function apps

If multiple function apps share a storage account, each function app *must* be configured with a separate [task hub name](durable-functions-task-hubs#task-hub-names). This requirement also applies to staging slots: each staging slot must be configured with a unique task hub name. A single storage account can contain multiple task hubs. This restriction generally applies to other storage providers as well.

The following diagram illustrates one task hub per function app in shared and dedicated Azure Storage accounts.

Note

The exception to the task hub sharing rule is if you are configuring your app for regional disaster recovery. See the [disaster recovery and geo-distribution](durable-functions-disaster-recovery-geo-distribution) article for more information.

### Content inspection

There are several common ways to inspect the contents of a task hub:

- Within a function app, the client object provides methods to query the instance store. To learn more about what types of queries are supported, see the
[Instance Management](durable-functions-instance-management)article. - Similarly, The
[HTTP API](durable-functions-http-features)offers REST requests to query the state of orchestrations and entities. See the[HTTP API Reference](durable-functions-http-api)for more details. - The
[Durable Functions Monitor](https://github.com/microsoft/DurableFunctionsMonitor)tool can inspect task hubs and offers various options for visual display.

For some of the storage providers, it is also possible to inspect the task hub by going directly to the underlying storage:

- If using the Azure Storage provider, the instance states are stored in the
[Instance Table](durable-functions-azure-storage-provider#instances-table)and the[History Table](durable-functions-azure-storage-provider#history-table)that can be inspected using tools such as Azure Storage Explorer. - If using the MSSQL storage provider, SQL queries and tools can be used to inspect the task hub contents inside the database.

## Representation in storage

Each storage provider uses a different internal organization to represent task hubs in storage. Understanding this organization, while not required, can be helpful when troubleshooting a function app or when trying to ensure performance, scalability, or cost targets. We thus briefly explain, for each storage provider, how the data is organized in storage. For more information on the various storage provider options and how they compare, see the [Durable Functions storage providers](durable-functions-storage-providers).

### Azure Storage provider

The Azure Storage provider represents the task hub in storage using the following components:

- Two Azure Tables store the instance states.
- One Azure Queue stores the activity messages.
- One or more Azure Queues store the instance messages. Each of these so-called
*control queues*represents a[partition](durable-functions-perf-and-scale#partition-count)that is assigned a subset of all instance messages, based on the hash of the instance ID. - A few extra blob containers used for lease blobs and/or large messages.

For example, a task hub named `xyz`

with `PartitionCount = 4`

contains the following queues and tables:

Next, we describe these components and the role they play in more detail.

For more information how task hubs are represented by the Azure Storage provider, see the [Azure Storage provider](durable-functions-azure-storage-provider) documentation.

### Netherite storage provider

Netherite partitions all of the task hub state into a specified number of partitions. In storage, the following resources are used:

- One Azure Storage blob container that contains all the blobs, grouped by partition.
- One Azure Table that contains published metrics about the partitions.
- An Azure Event Hubs namespace for delivering messages between partitions.

For example, a task hub named `mytaskhub`

with `PartitionCount = 32`

is represented in storage as follows:

Note

All of the task hub state is stored inside the `x-storage`

blob container. The `DurableTaskPartitions`

table and the EventHubs namespace contain redundant data: if their contents are lost, they can be automatically recovered. Therefore it is not necessary to configure the Azure Event Hubs namespace to retain messages past the default expiration time.

Netherite uses an event-sourcing mechanism, based on a log and checkpoints, to represent the current state of a partition. Both block blobs and page blobs are used. It is not possible to read this format from storage directly, so the function app has to be running when querying the instance store.

For more information on task hubs for the Netherite storage provider, see [Task Hub information for the Netherite storage provider](https://microsoft.github.io/durabletask-netherite/#/storage).

### MSSQL storage provider

All task hub data is stored in a single relational database, using several tables:

- The
`dt.Instances`

and`dt.History`

tables store the instance states. - The
`dt.NewEvents`

table stores the instance messages. - The
`dt.NewTasks`

table stores the activity messages.

To enable multiple task hubs to coexist independently in the same database, each table includes a `TaskHub`

column as part of its primary key. Unlike the other two providers, the MSSQL provider doesn't have a concept of partitions.

For more information on task hubs for the MSSQL storage provider, see [Task Hub information for the Microsoft SQL (MSSQL) storage provider](https://microsoft.github.io/durabletask-mssql/#/taskhubs).

## Task hub names

Task hubs are identified by a name that must conform to these rules:

- Contains only alphanumeric characters
- Starts with a letter
- Has a minimum length of 3 characters, maximum length of 45 characters

The task hub name is declared in the *host.json* file, as shown in the following example:

### host.json (Functions 2.0)

```
{
"version": "2.0",
"extensions": {
"durableTask": {
"hubName": "MyTaskHub"
}
}
}
```


### host.json (Functions 1.x)

```
{
"durableTask": {
"hubName": "MyTaskHub"
}
}
```


Task hubs can also be configured using app settings, as shown in the following `host.json`

example file:

### host.json (Functions 1.0)

```
{
"durableTask": {
"hubName": "%MyTaskHub%"
}
}
```


### host.json (Functions 2.0)

```
{
"version": "2.0",
"extensions": {
"durableTask": {
"hubName": "%MyTaskHub%"
}
}
}
```


The task hub name will be set to the value of the `MyTaskHub`

app setting. The following `local.settings.json`

demonstrates how to define the `MyTaskHub`

setting as `samplehubname`

:

```
{
"IsEncrypted": false,
"Values": {
"MyTaskHub" : "samplehubname"
}
}
```


Note

When using deployment slots, it's a best practice to configure the task hub name using app settings. If you want to ensure that a particular slot always uses a particular task hub, use ["slot-sticky" app settings](../functions-deployment-slots#create-a-deployment-setting).

In addition to **host.json**, task hub names can also be configured in [orchestration client binding](durable-functions-bindings#orchestration-client) metadata. This is useful if you need to access orchestrations or entities that live in a separate function app. The following code demonstrates how to write a function that uses the [orchestration client binding](durable-functions-bindings#orchestration-client) to work with a task hub that is configured as an App Setting:

```
[FunctionName("HttpStart")]
public static async Task<HttpResponseMessage> Run(
[HttpTrigger(AuthorizationLevel.Function, methods: "post", Route = "orchestrators/{functionName}")] HttpRequestMessage req,
[DurableClient(TaskHub = "%MyTaskHub%")] IDurableOrchestrationClient starter,
string functionName,
ILogger log)
{
// Function input comes from the request content.
object eventData = await req.Content.ReadAsAsync<object>();
string instanceId = await starter.StartNewAsync(functionName, eventData);
log.LogInformation($"Started orchestration with ID = '{instanceId}'.");
return starter.CreateCheckStatusResponse(req, instanceId);
}
```


Note

The previous example is for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

Note

Configuring task hub names in client binding metadata is only necessary when you use one function app to access orchestrations and entities in another function app. If the client functions are defined in the same function app as the orchestrations and entities, you should avoid specifying task hub names in the binding metadata. By default, all client bindings get their task hub metadata from the **host.json** settings.

Task hub names must start with a letter and consist of only letters and numbers. If not specified, a default task hub name will be used as shown in the following table:

| Durable extension version | Default task hub name |
|---|---|
| 2.x | When deployed in Azure, the task hub name is derived from the name of the function app. When running outside of Azure, the default task hub name is `TestHubName` . |
| 1.x | The default task hub name for all environments is `DurableFunctionsHub` . |

For more information about the differences between extension versions, see the [Durable Functions versions](durable-functions-versions) article.

Note

The name is what differentiates one task hub from another when there are multiple task hubs in a shared storage account. If you have multiple function apps sharing a shared storage account, you must explicitly configure different names for each task hub in the *host.json* files. Otherwise the multiple function apps will compete with each other for messages, which could result in undefined behavior, including orchestrations getting unexpectedly "stuck" in the `Pending`

or `Running`

state.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-sequence -->

# Function chaining in Durable Functions - Hello sequence sample

Function chaining refers to the pattern of executing a sequence of functions in a particular order. Often the output of one function needs to be applied to the input of another function. This article describes the chaining sequence that you create when you complete the Durable Functions quickstart ([C#](durable-functions-isolated-create-first-csharp), [JavaScript](quickstart-js-vscode), [TypeScript](quickstart-ts-vscode), [Python](quickstart-python-vscode), [PowerShell](quickstart-powershell-vscode), or [Java](quickstart-java)). For more information about Durable Functions, see [Durable Functions overview](durable-functions-overview).

## Prerequisites

Note

Version 4 of the Node.js programming model for Azure Functions is generally available. The v4 model is designed to provide a more flexible and intuitive experience for JavaScript and TypeScript developers. For more information about the differences between v3 and v4, see the [migration guide](../functions-node-upgrade-v4).

In the following code snippets, JavaScript (PM4) denotes programming model v4, the new experience.

## The functions

This article explains the following functions in the sample app:

`E1_HelloSequence`

: An [orchestrator function](durable-functions-bindings#orchestration-trigger) that calls `E1_SayHello`

multiple times in a sequence. It stores the outputs from the `E1_SayHello`

calls and records the results.
`E1_SayHello`

: An [activity function](durable-functions-bindings#activity-trigger) that prepends a string with "Hello".
`HttpStart`

: An HTTP triggered [durable client](durable-functions-bindings#orchestration-client) function that starts an instance of the orchestrator.

## E1_HelloSequence orchestrator function

```
[FunctionName("E1_HelloSequence")]
public static async Task<List<string>> Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
var outputs = new List<string>();
outputs.Add(await context.CallActivityAsync<string>("E1_SayHello", "Tokyo"));
outputs.Add(await context.CallActivityAsync<string>("E1_SayHello", "Seattle"));
outputs.Add(await context.CallActivityAsync<string>("E1_SayHello_DirectInput", "London"));
// returns ["Hello Tokyo!", "Hello Seattle!", "Hello London!"]
return outputs;
}
```


All C# orchestration functions must have a parameter of type `DurableOrchestrationContext`

, which exists in the `Microsoft.Azure.WebJobs.Extensions.DurableTask`

assembly. This context object lets you call other *activity* functions and pass input parameters using its `CallActivityAsync`

method.

The code calls `E1_SayHello`

three times in sequence with different parameter values. The return value of each call is added to the `outputs`

list, which is returned at the end of the function.

#### function.json

If you use Visual Studio Code or the Azure portal for development, here's the content of the *function.json* file for the orchestrator function. Most orchestrator *function.json* files look almost exactly like this.

```
{
"bindings": [
{
"name": "context",
"type": "orchestrationTrigger",
"direction": "in"
}
],
"disabled": false
}
```


The important thing is the `orchestrationTrigger`

binding type. All orchestrator functions must use this trigger type.

Warning

To abide by the "no I/O" rule of orchestrator functions, don't use any input or output bindings when using the `orchestrationTrigger`

trigger binding. If other input or output bindings are needed, they should instead be used in the context of `activityTrigger`

functions, which are called by the orchestrator. For more information, see the [orchestrator function code constraints](durable-functions-code-constraints) article.

#### index.js

Here is the orchestrator function:

```
const df = require("durable-functions");
module.exports = df.orchestrator(function* (context) {
context.log("Starting chain sample");
const output = [];
output.push(yield context.df.callActivity("E1_SayHello", "Tokyo"));
output.push(yield context.df.callActivity("E1_SayHello", "Seattle"));
output.push(yield context.df.callActivity("E1_SayHello", "London"));
return output;
});
```


All JavaScript orchestration functions must include the `durable-functions`

module. It's a library that enables you to write Durable Functions in JavaScript. There are three significant differences between an orchestrator function and other JavaScript functions:

- The orchestrator function is a
[generator function](/en-us/scripting/javascript/advanced/iterators-and-generators-javascript).
- The function is wrapped in a call to the
`durable-functions`

module's `orchestrator`

method (here `df`

).
- The function must be synchronous. Because the 'orchestrator' method handles the final call to 'context.done', the function should simply 'return'.

The `context`

object contains a `df`

durable orchestration context object that lets you call other *activity* functions and pass input parameters using its `callActivity`

method. The code calls `E1_SayHello`

three times in sequence with different parameter values, using `yield`

to indicate the execution should wait on the async activity function calls to be returned. The return value of each call is added to the `outputs`

array, which is returned at the end of the function.

```
const df = require("durable-functions");
const helloActivityName = "sayHello";
df.app.orchestration("helloSequence", function* (context) {
context.log("Starting chain sample");
const output = [];
output.push(yield context.df.callActivity(helloActivityName, "Tokyo"));
output.push(yield context.df.callActivity(helloActivityName, "Seattle"));
output.push(yield context.df.callActivity(helloActivityName, "Cairo"));
return output;
});
```


All JavaScript orchestration functions must include the `durable-functions`

module. This module enables you to write Durable Functions in JavaScript. To use the V4 node programming model, you need to install the preview `v3.x`

version of `durable-functions`

.

There are two significant differences between an orchestrator function and other JavaScript functions:

- The orchestrator function is a
[generator function](/en-us/scripting/javascript/advanced/iterators-and-generators-javascript).
- The function must be synchronous. The function should simply 'return'.

The `context`

object contains a `df`

durable orchestration context object that lets you call other *activity* functions and pass input parameters using its `callActivity`

method. The code calls `sayHello`

three times in sequence with different parameter values, using `yield`

to indicate the execution should wait on the async activity function calls to be returned. The return value of each call is added to the `outputs`

array, which is returned at the end of the function.

Note

Python Durable Functions are available for the Functions 3.0 runtime only.

#### function.json

If you use Visual Studio Code or the Azure portal for development, here's the content of the *function.json* file for the orchestrator function. Most orchestrator *function.json* files look almost exactly like this.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"name": "context",
"type": "orchestrationTrigger",
"direction": "in"
}
]
}
```


The important thing is the `orchestrationTrigger`

binding type. All orchestrator functions must use this trigger type.

Warning

To abide by the "no I/O" rule of orchestrator functions, don't use any input or output bindings when using the `orchestrationTrigger`

trigger binding. If other input or output bindings are needed, they should instead be used in the context of `activityTrigger`

functions, which are called by the orchestrator. For more information, see the [orchestrator function code constraints](durable-functions-code-constraints) article.

#### __init__.py

Here is the orchestrator function:

```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
result1 = yield context.call_activity('E1_SayHello', "Tokyo")
result2 = yield context.call_activity('E1_SayHello', "Seattle")
result3 = yield context.call_activity('E1_SayHello', "London")
return [result1, result2, result3]
main = df.Orchestrator.create(orchestrator_function)
```


All Python orchestration functions must include the `durable-functions`

package. It's a library that enables you to write Durable Functions in Python. There are two significant differences between an orchestrator function and other Python functions:

- The orchestrator function is a
[generator function](https://wiki.python.org/moin/Generators).
- The
*file* should register the orchestrator function as an orchestrator by stating `main = df.Orchestrator.create(<orchestrator function name>)`

at the end of the file. This helps distinguish it from other, helper, functions declared in the file.

The `context`

object lets you call other *activity* functions and pass input parameters using its `call_activity`

method. The code calls `E1_SayHello`

three times in sequence with different parameter values, using `yield`

to indicate the execution should wait on the async activity function calls to be returned. The return value of each call is returned at the end of the function.

## E1_SayHello activity function

```
[FunctionName("E1_SayHello")]
public static string SayHello([ActivityTrigger] IDurableActivityContext context)
{
string name = context.GetInput<string>();
return $"Hello {name}!";
}
```


Activities use the `ActivityTrigger`

attribute. Use the provided `IDurableActivityContext`

to perform activity related actions, such as accessing the input value using `GetInput<T>`

.

The implementation of `E1_SayHello`

is a relatively trivial string formatting operation.

Instead of binding to an `IDurableActivityContext`

, you can bind directly to the type that is passed into the activity function. For example:

```
[FunctionName("E1_SayHello_DirectInput")]
public static string SayHelloDirectInput([ActivityTrigger] string name)
{
return $"Hello {name}!";
}
```


#### E1_SayHello/function.json

The *function.json* file for the activity function `E1_SayHello`

is similar to that of `E1_HelloSequence`

except that it uses an `activityTrigger`

binding type instead of an `orchestrationTrigger`

binding type.

```
{
"bindings": [
{
"name": "name",
"type": "activityTrigger",
"direction": "in"
}
],
"disabled": false
}
```


Note

All activity functions called by an orchestration function must use the `activityTrigger`

binding.

The implementation of `E1_SayHello`

is a relatively trivial string formatting operation.

#### E1_SayHello/index.js

```
module.exports = function (context) {
context.done(null, `Hello ${context.bindings.name}!`);
};
```


Unlike the orchestration function, an activity function needs no special setup. The input passed to it by the orchestrator function is located on the `context.bindings`

object under the name of the `activityTrigger`

binding - in this case, `context.bindings.name`

. The binding name can be set as a parameter of the exported function and accessed directly, which is what the sample code does.

The implementation of `sayHello`

is a relatively trivial string formatting operation.

```
const df = require("durable-functions");
const helloActivityName = "sayHello";
df.app.activity(helloActivityName, {
handler: function (input) {
return `Hello ${input}`;
},
});
```


Unlike the orchestration function, an activity function needs no special setup. The input passed to it by the orchestrator function is the first argument to the function. The second argument is the invocation context, which is not used in this example.

#### E1_SayHello/function.json

The *function.json* file for the activity function `E1_SayHello`

is similar to that of `E1_HelloSequence`

except that it uses an `activityTrigger`

binding type instead of an `orchestrationTrigger`

binding type.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"name": "name",
"type": "activityTrigger",
"direction": "in"
}
]
}
```


Note

All activity functions called by an orchestration function must use the `activityTrigger`

binding.

The implementation of `E1_SayHello`

is a relatively trivial string formatting operation.

#### E1_SayHello/__init__.py

```
def main(name: str) -> str:
return f"Hello {name}!"
```


Unlike the orchestrator function, an activity function needs no special setup. The input passed to it by the orchestrator function is directly accessible as the parameter to the function.

## HttpStart client function

You can start an instance of orchestrator function using a client function. You will use the `HttpStart`

HTTP triggered function to start instances of `E1_HelloSequence`

.

```
public static class HttpStart
{
[FunctionName("HttpStart")]
public static async Task<HttpResponseMessage> Run(
[HttpTrigger(AuthorizationLevel.Function, methods: "post", Route = "orchestrators/{functionName}")] HttpRequestMessage req,
[DurableClient] IDurableClient starter,
string functionName,
ILogger log)
{
// Function input comes from the request content.
object eventData = await req.Content.ReadAsAsync<object>();
string instanceId = await starter.StartNewAsync(functionName, eventData);
log.LogInformation($"Started orchestration with ID = '{instanceId}'.");
return starter.CreateCheckStatusResponse(req, instanceId);
}
}
```


To interact with orchestrators, the function must include a `DurableClient`

input binding. You use the client to start an orchestration. It can also help you return an HTTP response containing URLs for checking the status of the new orchestration.

#### HttpStart/function.json

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"route": "orchestrators/{functionName}",
"methods": ["post"]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "starter",
"type": "orchestrationClient",
"direction": "in"
}
],
"disabled": false
}
```


To interact with orchestrators, the function must include a `durableClient`

input binding.

#### HttpStart/index.js

```
const df = require("durable-functions");
module.exports = async function (context, req) {
const client = df.getClient(context);
const instanceId = await client.startNew(req.params.functionName, undefined, req.body);
context.log(`Started orchestration with ID = '${instanceId}'.`);
return client.createCheckStatusResponse(context.bindingData.req, instanceId);
};
```


Use `df.getClient`

to obtain a `DurableOrchestrationClient`

object. You use the client to start an orchestration. It can also help you return an HTTP response containing URLs for checking the status of the new orchestration.

```
const df = require("durable-functions");
const { app } = require("@azure/functions");
app.http("httpStart", {
route: "orchestrators/{orchestratorName}",
extraInputs: [df.input.durableClient()],
handler: async (request, context) => {
const client = df.getClient(context);
const body = await request.json();
const instanceId = await client.startNew(request.params.orchestratorName, { input: body });
context.log(`Started orchestration with ID = '${instanceId}'.`);
return client.createCheckStatusResponse(request, instanceId);
},
});
```


To manage and interact with orchestrators, the function needs a `durableClient`

input binding. This binding needs to be specified in the `extraInputs`

argument when registering the function. A `durableClient`

input can be obtained by calling `df.input.durableClient()`

.

Use `df.getClient`

to obtain a `DurableClient`

object. You use the client to start an orchestration. It can also help you return an HTTP response containing URLs for checking the status of the new orchestration.

#### HttpStart/function.json

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"route": "orchestrators/{functionName}",
"methods": [
"post",
"get"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "starter",
"type": "durableClient",
"direction": "in"
}
]
}
```


To interact with orchestrators, the function must include a `durableClient`

input binding.

#### HttpStart/__init__.py

```
import logging
import azure.functions as func
import azure.durable_functions as df
async def main(req: func.HttpRequest, starter: str) -> func.HttpResponse:
client = df.DurableOrchestrationClient(starter)
instance_id = await client.start_new(req.route_params["functionName"], None, None)
logging.info(f"Started orchestration with ID = '{instance_id}'.")
return client.create_check_status_response(req, instance_id)
```


Use the `DurableOrchestrationClient`

constructor to obtain a Durable Functions client. You use the client to start an orchestration. It can also help you return an HTTP response containing URLs for checking the status of the new orchestration.

## Run the sample

To execute the `E1_HelloSequence`

orchestration, send the following HTTP POST request to the `HttpStart`

function.

```
POST http://{host}/orchestrators/E1_HelloSequence
```


Note

The previous HTTP snippet assumes there is an entry in the `host.json`

file which removes the default `api/`

prefix from all HTTP trigger functions URLs. You can find the markup for this configuration in the `host.json`

file in the samples.

For example, if you're running the sample in a function app named "myfunctionapp", replace "{host}" with "myfunctionapp.azurewebsites.net".

The result is an HTTP 202 response, like this (trimmed for brevity):

```
HTTP/1.1 202 Accepted
Content-Length: 719
Content-Type: application/json; charset=utf-8
Location: http://{host}/runtime/webhooks/durabletask/instances/96924899c16d43b08a536de376ac786b?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
(...trimmed...)
```


At this point, the orchestration is queued up and begins to run immediately. The URL in the `Location`

header can be used to check the status of the execution.

```
GET http://{host}/runtime/webhooks/durabletask/instances/96924899c16d43b08a536de376ac786b?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
```


The result is the status of the orchestration. It runs and completes quickly, so you see it in the *Completed* state with a response that looks like this (trimmed for brevity):

```
HTTP/1.1 200 OK
Content-Length: 179
Content-Type: application/json; charset=utf-8
{"runtimeStatus":"Completed","input":null,"output":["Hello Tokyo!","Hello Seattle!","Hello London!"],"createdTime":"2017-06-29T05:24:57Z","lastUpdatedTime":"2017-06-29T05:24:59Z"}
```


As you can see, the `runtimeStatus`

of the instance is *Completed* and the `output`

contains the JSON-serialized result of the orchestrator function execution.

Note

You can implement similar starter logic for other trigger types, like `queueTrigger`

, `eventHubTrigger`

, or `timerTrigger`

.

Look at the function execution logs. The `E1_HelloSequence`

function started and completed multiple times due to the replay behavior described in the [orchestration reliability](durable-functions-orchestrations#reliability) topic. On the other hand, there were only three executions of `E1_SayHello`

since those function executions do not get replayed.

## Next steps

This sample has demonstrated a simple function-chaining orchestration. The next sample shows how to implement the fan-out/fan-in pattern.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/quickstart-mssql -->

# Quickstart: Create a Durable Functions app that uses the MSSQL storage provider

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Durable Functions, a feature of [Azure Functions](../functions-overview), to write stateful functions in a serverless environment. Durable Functions manages state, checkpoints, and restarts in your application.

Durable Functions supports several [storage providers](durable-functions-storage-providers), also known as *backends*, for storing orchestration and entity runtime state. In this quickstart, you create a Durable Functions app to use the [Microsoft SQL Server (MSSQL) storage provider](durable-functions-storage-providers#mssql) using **Visual Studio Code**.

This quickstart creates a .NET (isolated model) app for demonstration purposes. Content provided in this article applies to other languages in similar ways.

Note

The MSSQL backend was designed to maximize application portability and control over your data. It uses

[Microsoft SQL Server](https://www.microsoft.com/sql-server/)to persist all task hub data so that users get the benefits of a modern, enterprise-grade database management system (DBMS) infrastructure. To learn more about when to use the MSSQL storage provider, see the[storage providers overview](durable-functions-storage-providers).Migrating

[task hub data](durable-functions-task-hubs)across storage providers currently isn't supported. Function apps that have existing runtime data start with a fresh, empty task hub after they switch to the MSSQL back end. Similarly, the task hub contents that are created by using MSSQL can't be preserved if you switch to a different storage provider.

## Prerequisites

To complete this quickstart, you need:

[Visual Studio Code](https://code.visualstudio.com/download)installed.[Azure Functions Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)installed.The latest version of

[Azure Functions Core Tools](../functions-run-local)installed.[.NET 8.0 SDK](https://dotnet.microsoft.com/download)installed.[Docker](https://www.docker.com/products/docker-desktop/)installed.An HTTP test tool that keeps your data secure. For more information, see

[HTTP test tools](../functions-develop-local#http-test-tools).

## Create an Azure Functions project

In Visual Studio Code, create a local Azure Functions project.

On the

**View**menu, select**Command Palette**(or select Ctrl+Shift+P).At the prompt (

`>`

), enter and then select**Azure Functions: Create New Project**.Select

**Browse**. In the**Select Folder**dialog, go to a folder to use for your project, and then choose**Select**.At the prompts, select or enter the following values:

Prompt Action Description **Select a language for your function app project**Select .NET Creates a local C# Functions project **Select a .NET runtime**Select **.NET 8.0 isolated**.Creates a Functions project that supports .NET 8 running in an isolated worker process and the Azure Functions Runtime 4.0. **Select a template for your project's first function**Select **Durable Functions Orchestration**.Creates a Durable Functions orchestration. **Choose a durable storage type**Select **MSSQL**.Selects the MSSQL storage provider. **Provide a function name**Enter **HelloOrchestration**.A name for the orchestration function. **Provide a namespace**Enter **Company.Function**.A namespace for the generated class. **Select how you would like to open your project**Select **Open in current window**.Opens Visual Studio Code in the folder you selected.

Visual Studio Code installs Azure Functions Core Tools if it's required to create the project. It also creates a function app project in a folder. This project contains the [host.json](../functions-host-json) and [local.settings.json](../functions-develop-local#local-settings-file) configuration files.

Another file, *HelloOrchestration.cs*, contains the basic building blocks of a Durable Functions app:

| Method | Description |
|---|---|
`HelloOrchestration` |
Defines the Durable Functions app orchestration. In this case, the orchestration starts, creates a list, and then adds the result of three functions calls to the list. When the three function calls finish, it returns the list. |
`SayHello` |
A simple function app that returns hello. This function contains the business logic that is orchestrated. |
`HelloOrchestration_HttpStart` |
An
check status response. |

For more information about these functions, see [Durable Functions types and features](durable-functions-types-features-overview).

## Set up your database

Note

If you already have an MSSQL-compatible database, you can skip this section and skip the next section on setting up a Docker-based local database.

Because the MSSQL backend is designed for portability, you have several options to set up your backing database. For example, you can set up an on-premises SQL Server instance, use a fully managed instance of [Azure SQL Database](/en-us/azure/azure-sql/database/sql-database-paas-overview), or use any other SQL Server-compatible hosting option.

You can also do local, offline development by using [SQL Server Express](https://www.microsoft.com/sql-server/sql-server-downloads) on your local Windows computer or use a [SQL Server Docker image](https://hub.docker.com/_/microsoft-mssql-server) running in a Docker container.

This quickstart focuses on using a SQL Server Docker image.

### Set up your local Docker-based SQL Server instance

Use the following PowerShell commands to set up a local SQL Server database on Docker. You can install PowerShell on [Windows, macOS, or Linux](/en-us/powershell/scripting/install/installing-powershell).

```
# primary parameters
$pw = "yourStrong(!)Password"
$edition = "Developer"
$port = 1433
$tag = "2019-latest"
$dbname = "DurableDB"
$collation = "Latin1_General_100_BIN2_UTF8"
# pull the image from the Microsoft container registry
docker pull mcr.microsoft.com/mssql/server:$tag
# run the image and provide some basic setup parameters
docker run --name mssql-server -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=$pw" -e "MSSQL_PID=$edition" -p ${port}:1433 -d mcr.microsoft.com/mssql/server:$tag
# wait a few seconds for the container to start...
# create the database with strict binary collation
docker exec -it mssql-server /opt/mssql-tools/bin/sqlcmd -S . -U sa -P "$pw" -Q "CREATE DATABASE [$dbname] COLLATE $collation"
# if sqlcmd is in the mssql-tools18 folder
# docker exec -it mssql-server /opt/mssql-tools18/bin/sqlcmd -C -S . -U sa -P "$pw" -Q "CREATE DATABASE [$dbname] COLLATE $collation"
```


You should now have a local SQL Server running on Docker and listening on port `1443`

. If port `1443`

conflicts with another service, rerun these commands after changing the variable `$port`

to a different value.

To validate your database installation, query your new SQL database:

```
docker exec -it mssql-server /opt/mssql-tools/bin/sqlcmd -S . -U sa -P "$pw" -Q "SELECT name FROM sys.databases"
```


If the database setup completed successfully, the name of your database (for example, **DurableDB**) appears in the command-line output:

```
name
--------------------------------------------------------------
master
tempdb
model
msdb
DurableDB
```


Note

To stop and delete a running container, you can use `docker stop <containerName>`

and `docker rm <containerName>`

respectively. You can use these commands to re-create your container and to stop the container when you finish this quickstart. For more assistance, run `docker --help`

.

#### Troubleshooting

If you run into *"Error response from daemon: OCI runtime exec failed"* when running `docker exec`

to **create** the database, it's likely the folder `/opt/mssql-tools/bin/sqlcmd`

does not exist. Open Docker Desktop, select your SQL Server Docker container, select Files and browse for the mssql-tools folder. Check if this folder has a different name, such as `/opt/mssql-tools18/bin/sqlcmd`

. Update the command accordingly.

In ODBC Driver 18 for SQL Server, the Encrypt connection option is set to true by default. If you run into *"error:1416F086:SSL routines:tls_process_server_certificate:certificate verify failed:self signed certificate"* when running `docker exec`

to perform database operations, append `-C`

, which is equivalent to the ADO.net option `TRUSTSERVERCERTIFICATE = true`

.

### Add SQL connection string to local.settings.json

The MSSQL backend needs a connection string to access your database. How to obtain a connection string depends primarily on your specific MSSQL server provider.

If you use the preceding Docker commands without changing any parameters, your connection string is:

```
Server=localhost,1433;Database=DurableDB;User Id=sa;Password=yourStrong(!)Password;
```


In *local.settings.json*, assign the connection string of the Docker-based SQL server instance to `SQLDB_Connection`

. This variable was added by Visual Studio Code when you picked MSSQL as the backend for your Durable Functions app:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"SQLDB_Connection": "Server=localhost,1433;Database=DurableDB;User Id=sa;Password=yourStrong(!)Password;",
"FUNCTIONS_WORKER_RUNTIME": "<dependent on your programming language>"
}
}
```


### Test locally

Open a terminal window in your app's root folder and run `azurite start`

. Azurite is the Azure Storage emulator, which is needed for running any Function app.

Open another terminal window in your app's root folder and start the Function app by running `func host start`

.

In the terminal window, copy the URL endpoint of your HTTP-triggered function.

Use an HTTP test tool to send an HTTP POST request to the URL endpoint.

The response is the HTTP function's initial result. It lets you know that the Durable Functions orchestration started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs.

Copy the URL value for

`statusQueryGetUri`

, paste it in your browser's address bar, and execute the request. Alternatively, you can also continue to use the HTTP test tool to issue the GET request.The request queries the orchestration instance for the status. You should see that the instance finished and that it includes the outputs or results of the Durable Functions app like in this example:

`{ "name":"HelloCities", "instanceId":"7f99f9474a6641438e5c7169b7ecb3f2", "runtimeStatus":"Completed", "input":null, "customStatus":null, "output":"Hello, Tokyo! Hello, London! Hello, Seattle!", "createdTime":"2023-01-31T18:48:49Z", "lastUpdatedTime":"2023-01-31T18:48:56Z" }`


## Run your app in Azure

To run your app in Azure, you need to create various resources. For convenient clean up later, create all the resources in the same resource group.

### Create an Azure SQL database

Note

If you already have an Azure SQL database or another publicly accessible SQL Server instance that you would like to use, you can go to the next section.

Refrain from enabling the **Allow Azure services and resources to access this [SQL] server** setting for production scenarios. Real applications should implement more secure approaches, such as stronger firewall restrictions or virtual network configurations.

In the Azure portal, you can [create an Azure SQL database](/en-us/azure/azure-sql/database/single-database-create-quickstart). During creation:

- Enable Azure services and resources to access this server (under
*Networking*) - Set the value for
*Database collation*(under*Additional settings*) to`Latin1_General_100_BIN2_UTF8`

.

### Create an Azure Functions app and supporting resources

Open a terminal window and sign in to Azure:

`az login`

Create the following resources in the same resource group and region as your SQL database:

- A general-purpose storage account, which is used to store important app data, such as the application code itself. Storage account names must contain three to 24 characters numbers and lowercase letters only.
- A premium function app plan
- A function app

`# Variables location=<REGION> resourceGroup=<RESOURCE_GROUP_NAME> storage=<STORAGE_NAME> planName=<PREMIUM_PLAN_NAME> functionApp=<APP_NAME> skuStorage="Standard_LRS" skuPlan="EP1" functionsVersion="4" # Create an Azure storage account echo "Creating $storage" az storage account create --name $storage --location "$location" --resource-group $resourceGroup --sku $skuStorage --allow-blob-public-access false # Create a premium plan echo "Creating $premiumPlan" az functionapp plan create --name $planName --resource-group $resourceGroup --location "$location" --sku $skuPlan # Create a function app hosted in the premium plan echo "Creating $functionApp" az functionapp create --name $functionApp --storage-account $storage --plan $planName --resource-group $resourceGroup --functions-version $functionsVersion`


### Create an Azure managed identity

Managed identities make your app more secure by eliminating secrets from your app, such as credentials in the connection strings. You can choose between [system-assigned and user-assigned managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview). This quickstart demonstrates setting up user-assigned managed identity, which is the recommended option as it is not tied to the app lifecycle.

The following commands create the identity resource and assign it to the app:

```
# Variables
subscription=<SUBSCRIPTION_ID>
identity=<IDENTITY_NAME>
# Create a managed identity resource
echo "Creating $identity"
az identity create -g $resourceGroup -n $identity --location "$location"
# Construct the identity resource ID
resourceId="/subscriptions/$subscription/resourceGroups/$resourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/$identity"
# Assign the identity to the Azure Functions app
echo "Assigning $identity to app"
az functionapp identity assign -g $resourceGroup -n $functionApp --identities "$resourceId"
# Get the identity's ClientId and PrincipalId (also called ObjectId) for a later step.
clientId=$(az identity show --name $identity --resource-group $resourceGroup --query 'clientId' --output tsv)
principalId=$(az identity show --name $identity --resource-group $resourceGroup --query 'principalId' --output tsv)
```


### Grant access to Azure Storage and Azure SQL Database

#### Azure Storage

Assign the identity **Storage Blob Data Owner** role for access to the storage account.

```
# Set the scope of the access
scope="/subscriptions/$subscription/resourceGroups/$resourceGroup/providers/Microsoft.Storage/storageAccounts/$storage"
# Assign the role
echo "Assign Storage Blob Data Owner role to identity"
az role assignment create --assignee "$clientId" --role "Storage Blob Data Owner" --scope "$scope"
```


#### Azure SQL Database

Note

Authenticating to Azure SQL database using managed identity is *not* supported when hosting a Durable Functions app in the Flex Consumption plan. If your app is hosted in the Flex Consumption plan, skip to the [set app settings](#set-required-app-settings) section.

Start by setting your developer identity as the database's admin.

The assignee is your identity, so change to your email:

`assignee=$(az ad user show --id "someone@example.com" --query "id" --output tsv)`

Set assignee as admin of the Azure SQL database:

`az sql server ad-admin create --resource-group $resourceGroup --server-name <SQL_SERVER_NAME> --display-name ADMIN --object-id "$assignee"`

Connect to the SQL database created previously using tools such as

[SQL Management Server Studio](/en-us/ssms/download-sql-server-management-studio-ssms)or[Visual Studio Code](/en-us/sql/tools/visual-studio-code-extensions/mssql/mssql-extension-visual-studio-code). Or you can run the following[SQLCMD](/en-us/sql/tools/sqlcmd/sqlcmd-utility)command to connect:`sqlcmd -S <SQL_SERVER_NAME>.database.windows.net -d <DATABASE_NAME> -U <someone@example.com> -P "ACCOUNT_PASSWORD" -G -l 30`

Grant your identity

*db_owner*access by running the following query against the database. The`IDENTITY_OBJECT_ID`

is the*PrincipalId*from the identity creation step.`CREATE USER "<IDENTITY_NAME>" FROM EXTERNAL PROVIDER With OBJECT_ID='<IDENTITY_OBJECT_ID>' ALTER ROLE db_owner ADD MEMBER "<IDENTITY_NAME>"; GO`

Connect to the

`master`

database and grant your identity*dbmanager*access:`CREATE USER "<IDENTITY_NAME>" FROM EXTERNAL PROVIDER With OBJECT_ID='<IDENTITY_OBJECT_ID>' ALTER ROLE dbmanager ADD MEMBER "<IDENTITY_NAME>"; GO`


### Set required app settings

You need to add the following app settings to your app:

`AzureWebJobsStorage__accountName`

: Azure Storage account name`AzureWebJobsStorage__clientId`

: ClientId of the managed identity`AzureWebJobsStorage__credential`

: Credential type, which is*managedidentity*`SQLDB_Connection`

: SQL database connection string

If you're using user-assigned managed identity to authenticate to the SQL database, the connection string should look like the following:

```
dbserver=<SQL_SERVER_NAME>
sqlDB=<SQL_DB_NAME>
clientId=<IDENTITY_CLIENT_ID>
sqlconnstr="Server=tcp:$dbserver.database.windows.net,1433;Initial Catalog=$sqlDB;Persist Security Info=False;User ID=$clientId;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Authentication='Active Directory Managed Identity';"
```


For Flex Consumption apps, use a connection string to authenticate for now. You can find it by going to the SQL database resource on Azure portal, navigating to the **Settings** tab, then clicking on **Connection strings**:


The connection string should have this format:

```
dbserver=<SQL_SERVER_NAME>
sqlDB=<SQL_DB_NAME>
username=<DB_USER_LOGIN>
password=<DB_USER_PASSWORD>
sqlconnstr="Server=tcp:$dbserver.database.windows.net,1433;Initial Catalog=$sqlDB;Persist Security Info=False;User ID=$username;Password=$password;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;"
```


Run the following command to set the settings:

```
az functionapp config appsettings set --name $functionApp --resource-group $resourceGroup --settings AzureWebJobsStorage__accountName="$storage" AzureWebJobsStorage__clientId="$clientId" AzureWebJobsStorage__credential="managedidentity" SQLDB_Connection=$sqlconnstr
```


Delete the existing `AzureWebJobsStorage`

setting:

```
az functionapp config appsettings delete --name $functionApp --resource-group $resourceGroup --setting-names "AzureWebJobsStorage"
```


### Deploy the local project to Azure and test

Finally, in your root project folder, deploy your app to Azure by running:

```
func azure functionapp publish $functionApp
```


After deployment finishes, run the following to get the HTTP trigger URL:

```
az functionapp function list --resource-group $resourceGroup --name $functionApp --query '[].{Function:name, URL:invokeUrlTemplate}' --output json
```


Test just as you did during [local development](#test-locally) with an HTTP test tool.

You can also validate that the MSSQL backend is correctly configured by querying the database for task hub data.

For example, you can query your orchestration instances on your SQL database's overview pane. Select **Query Editor**, authenticate, and then run the following query:

```
SELECT TOP 5 InstanceID, RuntimeStatus, CreatedTime, CompletedTime FROM dt.Instances
```


After you run a simple orchestrator, you should see at least one result, as shown in this example:


## Next steps

- Host a Durable Functions app using the MSSQL backend in
[Azure Container Apps](durable-functions-mssql-container-apps-hosting). - See the
[MSSQL storage provider documentation](https://microsoft.github.io/durabletask-mssql/)for more information about this backend's architecture, configuration, and workload behavior.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/quickstart-js-vscode -->

# Quickstart: Create a JavaScript Durable Functions app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Durable Functions, a feature of [Azure Functions](../functions-overview), to write stateful functions in a serverless environment. You install Durable Functions by installing the [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) in Visual Studio Code. The extension manages state, checkpoints, and restarts in your application.

In this quickstart, you use the Durable Functions extension in Visual Studio Code to locally create and test a "hello world" Durable Functions app in Azure Functions. The Durable Functions app orchestrates and chains together calls to other functions. Then, you publish the function code to Azure. The tools you use are available via the Visual Studio Code extension.

Important

The content of this article changes based on your choice of the Node.js programming model in the selector at the top of the page. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. Learn more about the differences between v3 and v4 in the [migration guide](../functions-node-upgrade-v4).


## Prerequisites

To complete this quickstart, you need:

[Visual Studio Code](https://code.visualstudio.com/download)installed.

- The Visual Studio Code extension
[Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)installed.

- The Visual Studio Code extension
[Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)version 1.10.4 or later installed.

- The latest version of
[Azure Functions Core Tools](../functions-run-local)installed.

[Azure Functions Core Tools](../functions-run-local)version 4.0.5382 or later installed.

An HTTP test tool that keeps your data secure. For more information, see

[HTTP test tools](../functions-develop-local#http-test-tools).An Azure subscription. To use Durable Functions, you must have an Azure Storage account.


[Node.js](https://nodejs.org/)version 16.x+ installed.

[Node.js](https://nodejs.org/)version 18.x+ installed.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project.

In Visual Studio Code, select F1 (or select Ctrl/Cmd+Shift+P) to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create New Project**.Select

**Browse**. In the**Select Folder**dialog, go to a folder to use for your project, and then choose**Select**.

At the prompts, provide the following information:

Prompt Action Description **Select a language for your function app project**Select **JavaScript**.Creates a local Node.js Functions project. **Select a JavaScript programming model**Select **Model V3**.Sets the v3 programming model. **Select a version**Select **Azure Functions v4**.You see this option only when Core Tools isn't already installed. In this case, Core Tools is installed the first time you run the app. **Select a template for your project's first function**Select **Skip for now**.**Select how you would like to open your project**Select **Open in current window**.Opens Visual Studio Code in the folder you selected.

At the prompts, provide the following information:

Prompt Action Description **Select a language for your function app project**Select **JavaScript**.Creates a local Node.js Functions project. **Select a JavaScript programming model**Select **Model V4**.Choose the v4 programming model. **Select a version**Select **Azure Functions v4**.You see this option only when Core Tools isn't already installed. In this case, Core Tools is installed the first time you run the app. **Select a template for your project's first function**Select **Skip for now**.**Select how you would like to open your project**Select **Open in current window**.Opens Visual Studio Code in the folder you selected.

Visual Studio Code installs Azure Functions Core Tools if it's required to create a project. It also creates a function app project in a folder. This project contains the [host.json](../functions-host-json) and [local.settings.json](../functions-develop-local#local-settings-file) configuration files.

A *package.json* file is also created in the root folder.

## Install the Durable Functions npm package

To work with Durable Functions in a Node.js function app, you use a library called *durable-functions*.

To use the v4 programming model, you install the preview v3.x version of the durable-functions library.

- Use the
**View**menu or select Ctrl+Shift+` to open a new terminal in Visual Studio Code.

- Install the durable-functions npm package by running
`npm install durable-functions`

in the root directory of the function app.

- Install the durable-functions npm package preview version by running
`npm install durable-functions@preview`

in the root directory of the function app.

## Create your functions

The most basic Durable Functions app has three functions:

**Orchestrator function**: A workflow that orchestrates other functions.**Activity function**: A function that is called by the orchestrator function, performs work, and optionally returns a value.**Client function**: A regular function in Azure that starts an orchestrator function. This example uses an HTTP-triggered function.

### Orchestrator function

You use a template to create the Durable Functions app code in your project.

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions orchestrator**.Creates a Durable Functions app orchestration. **Choose a durable storage type**Select **Azure Storage (Default)**.Selects the storage back end that's used for your Durable Functions app. **Provide a function name**Enter **HelloOrchestrator**.A name for your durable function.

You added an orchestrator to coordinate activity functions. Open *HelloOrchestrator/index.js* to see the orchestrator function. Each call to `context.df.callActivity`

invokes an activity function named `Hello`

.

Next, add the referenced `Hello`

activity function.

### Activity function

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions activity**.Creates an activity function. **Provide a function name**Enter **Hello**.A name for your durable function.

You added the `Hello`

activity function that is invoked by the orchestrator. Open *Hello/index.js* to see that it's taking a name as input and returning a greeting. An activity function is where you perform "the real work" in your workflow, such as making a database call or performing some nondeterministic computation.

Finally, add an HTTP-triggered function that starts the orchestration.

### Client function (HTTP starter)

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions HTTP starter**.Creates an HTTP starter function. **Provide a function name**Enter **DurableFunctionsHttpStart**.The name of your activity function. **Authorization level**Select **Anonymous**.For demo purposes, this value allows the function to be called without using authentication

You added an HTTP-triggered function that starts an orchestration. Open *DurableFunctionsHttpStart/index.js* to see that it uses `client.startNew`

to start a new orchestration. Then it uses `client.createCheckStatusResponse`

to return an HTTP response that contains URLs that you can use to monitor and manage the new orchestration.

You now have a Durable Functions app that you can run locally and deploy to Azure.

One of the benefits of the v4 programming model is the flexibility of where you write your functions. In the v4 model, you can use a single template to create all three functions in one file in your project.

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions orchestrator**.Creates a file that has a Durable Functions app orchestration, an activity function, and a durable client starter function. **Choose a durable storage type**Select **Azure Storage (Default)**.Sets the storage back end to use for your Durable Functions app. **Provide a function name**Enter **hello**.The name of your durable function.

Open *src/functions/hello.js* to view the functions you created.

You created an orchestrator called `helloOrchestrator`

to coordinate activity functions. Each call to `context.df.callActivity`

invokes an activity function called `hello`

.

You also added the `hello`

activity function that is invoked by the orchestrator. In the same file, you can see that it's taking a name as input and returning a greeting. An activity function is where you perform "the real work" in your workflow, such as making a database call or performing some nondeterministic computation.

Finally, also added an HTTP-triggered function that starts an orchestration. In the same file, you can see that it uses `client.startNew`

to start a new orchestration. Then it uses `client.createCheckStatusResponse`

to return an HTTP response that contains URLs that you can use to monitor and manage the new orchestration.

You now have a Durable Functions app that you can run locally and deploy to Azure.

## Test the function locally

Azure Functions Core Tools gives you the capability to run an Azure Functions project on your local development computer. You're prompted to install these tools the first time you start a function in Visual Studio Code.

To test your function, set a breakpoint in the

`Hello`

activity function code (in*Hello/index.js*). Select F5 or select**Debug: Start Debugging**in the command palette to start the function app project. Output from Core Tools appears in the terminal panel.Note

For more information about debugging, see

[Durable Functions diagnostics](durable-functions-diagnostics#debugging).

To test your function, set a breakpoint in the

`hello`

activity function code (in*src/functions/hello.js*). Select F5 or select**Debug: Start Debugging**in the command palette to start the function app project. Output from Core Tools appears in the terminal panel.Note

For more information about debugging, see

[Durable Functions diagnostics](durable-functions-diagnostics#debugging).

Durable Functions requires an Azure Storage account to run. When Visual Studio Code prompts you to select a storage account, choose

**Select storage account**.At the prompts, provide the following information to create a new storage account in Azure:

Prompt Value Description Select subscription *name of your subscription*Select your Azure subscription Select a storage account Create a new storage account Enter the name of the new storage account *unique name*Name of the storage account to create Select a resource group *unique name*Name of the resource group to create Select a location *region*Select a region close to you In the terminal panel, copy the URL endpoint of your HTTP-triggered function.


Use your browser or an HTTP test tool to send an HTTP POST request to the URL endpoint.

Replace the last segment with the name of the orchestrator function (

`HelloOrchestrator`

). The URL should be similar to`http://localhost:7071/api/orchestrators/HelloOrchestrator`

.The response is the HTTP function's initial result. It lets you know that the durable orchestration started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs. For now, query the status of the orchestration.


Use your browser or an HTTP test tool to send an HTTP POST request to the URL endpoint.

Replace the last segment with the name of the orchestrator function (

`HelloOrchestrator`

). The URL should be similar to`http://localhost:7071/api/orchestrators/HelloOrchestrator`

.The response is the HTTP function's initial result. It lets you know that the durable orchestration started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs. For now, query the status of the orchestration.


Copy the URL value for

`statusQueryGetUri`

, paste it in your browser's address bar, and execute the request. Alternatively, you can also continue to use your HTTP test tool to issue the GET request.The request queries the orchestration instance for the status. You should see that the instance finished and that it includes the outputs or results of the Durable Functions app, like in this example:

`{ "name": "HelloOrchestrator", "instanceId": "9a528a9e926f4b46b7d3deaa134b7e8a", "runtimeStatus": "Completed", "input": null, "customStatus": null, "output": [ "Hello Tokyo!", "Hello Seattle!", "Hello London!" ], "createdTime": "2020-03-18T21:54:49Z", "lastUpdatedTime": "2020-03-18T21:54:54Z" }`


Copy the URL value for

`statusQueryGetUri`

, paste it in your browser's address bar, and execute the request. You can also continue to use your HTTP test tool to issue the GET request.The request queries the orchestration instance for the status. You should see that the instance finished and that it includes the outputs or results of the Durable Functions app, like in this example:

`{ "name": "helloOrchestrator", "instanceId": "6ba3f77933b1461ea1a3828c013c9d56", "runtimeStatus": "Completed", "input": "", "customStatus": null, "output": [ "Hello, Tokyo", "Hello, Seattle", "Hello, Cairo" ], "createdTime": "2023-02-13T23:02:21Z", "lastUpdatedTime": "2023-02-13T23:02:25Z" }`


- In Visual Studio Code, select Shift+F5 to stop debugging.

After you verify that the function runs correctly on your local computer, it's time to publish the project to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](../storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Test your function in Azure

Note

To use the v4 Node.js programming model, make sure that your app is running on at least version 4.25 of the Azure Functions runtime.

On the output panel, copy the URL of the HTTP trigger. The URL that calls your HTTP-triggered function should be in this format:

`https://<functionappname>.azurewebsites.net/api/orchestrators/HelloOrchestrator`


On the output panel, copy the URL of the HTTP trigger. The URL that calls your HTTP-triggered function should be in this format:

`https://<functionappname>.azurewebsites.net/api/orchestrators/helloOrchestrator`


- Paste the new URL for the HTTP request in your browser's address bar. When you use the published app, you can expect to get the same status response that you got when you tested locally.

The JavaScript Durable Functions app that you created and published in Visual Studio Code is ready to use.

## Clean up resources

If you no longer need the resources that you created to complete the quickstart, to avoid related costs in your Azure subscription, [delete the resource group](/en-us/azure/azure-resource-manager/management/delete-resource-group?tabs=azure-portal#delete-resource-group) and all related resources.

## Related content

- Learn about
[common Durable Functions app patterns](durable-functions-overview#application-patterns).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/quickstart-ts-vscode -->

# Quickstart: Create a TypeScript Durable Functions app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Durable Functions, a feature of [Azure Functions](../functions-overview), to write stateful functions in a serverless environment. You install Durable Functions by installing the [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) in Visual Studio Code. The extension manages state, checkpoints, and restarts in your application.

In this quickstart, you use the Durable Functions extension in Visual Studio Code to locally create and test a "hello world" Durable Functions app in Azure Functions. The Durable Functions app orchestrates and chains together calls to other functions. Then, you publish the function code to Azure. The tools you use are available via the Visual Studio Code extension.

Important

The content of this article changes based on your choice of the Node.js programming model in the selector at the top of the page. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. Learn more about the differences between v3 and v4 in the [migration guide](../functions-node-upgrade-v4).

## Prerequisites

To complete this quickstart, you need:

[Visual Studio Code](https://code.visualstudio.com/download)installed.

- The Visual Studio Code extension
[Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)installed.

- The Visual Studio Code extension
[Azure Functions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)version 1.10.4 or later installed.

- The latest version of
[Azure Functions Core Tools](../functions-run-local)installed.

[Azure Functions Core Tools](../functions-run-local)version 4.0.5382 or later installed.

An HTTP test tool that keeps your data secure. For more information, see

[HTTP test tools](../functions-develop-local#http-test-tools).An Azure subscription. To use Durable Functions, you must have an Azure Storage account.


[Node.js](https://nodejs.org/)version 16.x+ installed.

[Node.js](https://nodejs.org/)version 18.x+ installed.

[TypeScript](https://www.typescriptlang.org/)version 4.x+ installed.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project.

In Visual Studio Code, select F1 (or select Ctrl/Cmd+Shift+P) to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create New Project**.Select

**Browse**. In the**Select Folder**dialog, go to a folder to use for your project, and then choose**Select**.

At the prompts, provide the following information:

Prompt Action Description **Select a language for your function app project**Select **TypeScript**.Creates a local Node.js Functions project by using TypeScript. **Select a JavaScript programming model**Select **Model V3**.Sets the v3 programming model. **Select a version**Select **Azure Functions v4**.You see this option only when Core Tools isn't already installed. In this case, Core Tools is installed the first time you run the app. **Select a template for your project's first function**Select **Skip for now**.**Select how you would like to open your project**Select **Open in current window**.Opens Visual Studio Code in the folder you selected.

At the prompts, provide the following information:

Prompt Action Description **Select a language for your function app project**Select **TypeScript**.Creates a local Node.js Functions project by using TypeScript. **Select a JavaScript programming model**Select **Model V4**.Sets the v4 programming model. **Select a version**Select **Azure Functions v4**.You see this option only when Core Tools isn't already installed. In this case, Core Tools is installed the first time you run the app. **Select a template for your project's first function**Select **Skip for now**.**Select how you would like to open your project**Select **Open in current window**.Opens Visual Studio Code in the folder you selected.

Visual Studio Code installs Azure Functions Core Tools if it's required to create a project. It also creates a function app project in a folder. This project contains the [host.json](../functions-host-json) and [local.settings.json](../functions-develop-local#local-settings-file) configuration files.

A *package.json* file and a *tsconfig.json* file are also created in the root folder.

## Install the Durable Functions npm package

To work with Durable Functions in a Node.js function app, you use a library called *durable-functions*.

To use the v4 programming model, you need to install the preview v3.x version of the durable-functions library.

- Use the
**View**menu or select Ctrl+Shift+` to open a new terminal in Visual Studio Code.

- Install the durable-functions npm package by running
`npm install durable-functions`

in the root directory of the function app.

- Install the durable-functions npm package preview version by running
`npm install durable-functions@preview`

in the root directory of the function app.

## Create your functions

The most basic Durable Functions app has three functions:

**Orchestrator function**: A workflow that orchestrates other functions.**Activity function**: A function that is called by the orchestrator function, performs work, and optionally returns a value.**Client function**: A regular function in Azure that starts an orchestrator function. This example uses an HTTP-triggered function.

### Orchestrator function

You use a template to create the Durable Functions code in your project.

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions orchestrator**.Creates a Durable Functions orchestration. **Choose a durable storage type**Select **Azure Storage (Default)**.Sets the storage back end to use for your Durable Functions app. **Provide a function name**Enter **HelloOrchestrator**.The name of your function.

You added an orchestrator to coordinate activity functions. Open *HelloOrchestrator/index.ts* to see the orchestrator function. Each call to `context.df.callActivity`

invokes an activity function named `Hello`

.

Next, you add the referenced `Hello`

activity function.

### Activity function

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions activity**.Creates an activity function. **Provide a function name**Enter **Hello**.A name for your activity function.

You added the `Hello`

activity function that is invoked by the orchestrator. Open *Hello/index.ts* to see that it's taking a name as input and returning a greeting. An activity function is where you perform "the real work" in your workflow, such as making a database call or performing some nondeterministic computation.

Finally, you add an HTTP-triggered function that starts the orchestration.

### Client function (HTTP starter)

In the command palette, enter and then select

`Azure Functions: Create Function`

.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions HTTP starter**.Creates an HTTP starter function. **Provide a function name**Select **DurableFunctionsHttpStart**.The name of your activity function. **Authorization level**Select **Anonymous**.For demo purposes, this value allows the function to be called without using authentication.

You added an HTTP-triggered function that starts an orchestration. Open *DurableFunctionsHttpStart/index.ts* to see that it uses `client.startNew`

to start a new orchestration. Then it uses `client.createCheckStatusResponse`

to return an HTTP response containing URLs that can be used to monitor and manage the new orchestration.

You now have a Durable Functions app that you can run locally and deploy to Azure.

One of the benefits of the v4 programming model is the flexibility of where you write your functions. In the v4 model, you can use a single template to create all three functions in one file in your project.

In the command palette, enter and then select

**Azure Functions: Create Function**.At the prompts, provide the following information:

Prompt Action Description **Select a template for your function**Select **Durable Functions orchestrator**.Creates a file that has a Durable Functions app orchestration, an activity function, and a durable client starter function. **Choose a durable storage type**Select **Azure Storage (Default)**.Sets the storage back end to use for your Durable Function. **Provide a function name**Enter **Hello**.A name for your durable function.

Open *src/functions/hello.ts* to view the functions you created.

You created an orchestrator called `helloOrchestrator`

to coordinate activity functions. Each call to `context.df.callActivity`

invokes an activity function called `hello`

.

You also added the `hello`

activity function that is invoked by the orchestrator. In the same file, you can see that it's taking a name as input and returning a greeting. An activity function is where you perform "the real work" in your workflow, such as making a database call or performing some nondeterministic computation.

Finally, you added an HTTP-triggered function that starts an orchestration. In the same file, you can see that it uses `client.startNew`

to start a new orchestration. Then it uses `client.createCheckStatusResponse`

to return an HTTP response containing URLs that can be used to monitor and manage the new orchestration.

You now have a Durable Functions app that you can run locally and deploy to Azure.

## Test the function locally

Azure Functions Core Tools gives you the capability to run an Azure Functions project on your local development computer. You're prompted to install these tools the first time you start a function in Visual Studio.

To test your function, set a breakpoint in the

`Hello`

activity function code (in*Hello/index.ts*). Select F5 or select**Debug: Start Debugging**in the command palette to start the function app project. Output from Core Tools appears in the terminal panel.Note

For more information about debugging, see

[Durable Functions diagnostics](durable-functions-diagnostics#debugging).

To test your function, set a breakpoint in the

`hello`

activity function code (in*src/functions/hello.ts*). Select F5 or select**Debug: Start Debugging**in the command palette to start the function app project. Output from Core Tools appears in the terminal panel.Note

For more information about debugging, see

[Durable Functions diagnostics](durable-functions-diagnostics#debugging).

Durable Functions requires an Azure Storage account to run. When Visual Studio Code prompts you to select a storage account, select

**Select storage account**.At the prompts, provide the following information to create a new storage account in Azure.

Prompt Action Description **Select subscription**Select the name of your subscription. Your Azure subscription. **Select a storage account**Select **Create a new storage account**.**Enter the name of the new storage account**Enter a unique name. The name of the storage account to create. **Select a resource group**Enter a unique name. The name of the resource group to create. **Select a location**Select an Azure region. Select a region that is close to you. In the terminal panel, copy the URL endpoint of your HTTP-triggered function.


Use your browser or an HTTP test tool to send an HTTP POST request to the URL endpoint.

Replace the last segment with the name of the orchestrator function (

`HelloOrchestrator`

). The URL should be similar to`http://localhost:7071/api/orchestrators/HelloOrchestrator`

.The response is the HTTP function's initial result. It lets you know that the durable orchestration started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs. For now, query the status of the orchestration.


Use your browser or an HTTP test tool to send an HTTP POST request to the URL endpoint.

Replace the last segment with the name of the orchestrator function (

`HelloOrchestrator`

). The URL should be similar to`http://localhost:7071/api/orchestrators/HelloOrchestrator`

.The response is the HTTP function's initial result. It lets you know that the durable orchestration started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs. For now, query the status of the orchestration.


Copy the URL value for

`statusQueryGetUri`

, paste it in your browser's address bar, and execute the request. You can also continue to use your HTTP test tool to issue the GET request.The request queries the orchestration instance for the status. You should see that the instance finished and that it includes the outputs or results of the durable function. It looks similar to this example:

`{ "name": "HelloOrchestrator", "instanceId": "9a528a9e926f4b46b7d3deaa134b7e8a", "runtimeStatus": "Completed", "input": null, "customStatus": null, "output": [ "Hello Tokyo!", "Hello Seattle!", "Hello London!" ], "createdTime": "2020-03-18T21:54:49Z", "lastUpdatedTime": "2020-03-18T21:54:54Z" }`


Copy the URL value for

`statusQueryGetUri`

, paste it in your browser's address bar, and execute the request. You can also continue to use your HTTP test tool to issue the GET request.The request queries the orchestration instance for the status. You should see that the instance finished and that it includes the outputs or results of the Durable Functions app. It looks similar to this example:

`{ "name": "helloOrchestrator", "instanceId": "6ba3f77933b1461ea1a3828c013c9d56", "runtimeStatus": "Completed", "input": "", "customStatus": null, "output": [ "Hello, Tokyo", "Hello, Seattle", "Hello, Cairo" ], "createdTime": "2023-02-13T23:02:21Z", "lastUpdatedTime": "2023-02-13T23:02:25Z" }`


- To stop debugging, in Visual Studio Code, select Shift+F5.

After you verify that the function runs correctly on your local computer, it's time to publish the project to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](../storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Test your function in Azure

Note

To use the v4 node programming model, make sure that your app is running on at least version 4.25 of the Azure Functions runtime.

Copy the URL of the HTTP trigger from the output panel. The URL that calls your HTTP-triggered function should be in this format:

`https://<functionappname>.azurewebsites.net/api/orchestrators/HelloOrchestrator`


Copy the URL of the HTTP trigger from the output panel. The URL that calls your HTTP-triggered function should be in this format:

`https://<functionappname>.azurewebsites.net/api/orchestrators/helloOrchestrator`


- Paste the new URL for the HTTP request in your browser's address bar. When you use the published app, you can expect to get the same status response that you got when you tested locally.

The TypeScript Durable Functions app that you created and published by using Visual Studio Code is ready to use.

## Clean up resources

If you no longer need the resources that you created to complete the quickstart, to avoid related costs in your Azure subscription, [delete the resource group](/en-us/azure/azure-resource-manager/management/delete-resource-group?tabs=azure-portal#delete-resource-group) and all related resources.

## Related content

- Learn about
[common Durable Functions app patterns](durable-functions-overview#application-patterns).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-orchestration-versioning -->

# Orchestration versioning in Durable Functions (Azure Functions) - public preview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Orchestration versioning addresses [the core challenge](durable-functions-versioning) of deploying changes to orchestrator functions while maintaining the deterministic execution model that Durable Functions requires. Without this feature, breaking changes to orchestrator logic or activity function signatures would cause in-flight orchestration instances to fail during replay because they would break the [determinism requirement](durable-functions-code-constraints) that ensures reliable orchestration execution. This built-in feature provides automatic version isolation with minimal configuration. It's backend agnostic, so it can be used by apps leveraging any of the Durable Function's [storage providers](durable-functions-storage-providers), including the [Durable Task Scheduler](durable-task-scheduler/durable-task-scheduler).

Note

For Durable Task Scheduler users, if you're using the Durable Task SDKs instead of Durable functions, you should refer to the [Durable Task SDKs versioning article](durable-task-scheduler/durable-task-scheduler-versioning).

## Terminology

This article uses two related but distinct terms:

**Orchestrator function**(or simply "orchestrator"): Refers to the function code that defines the workflow logic - the template or blueprint for how a workflow should execute.**Orchestration instance**(or simply "orchestration"): Refers to a specific running execution of an orchestrator function, with its own state, instance ID, and inputs. Multiple orchestration instances can run concurrently from the same orchestrator function.

Understanding this distinction is crucial for orchestration versioning, where the orchestrator function code contains version-aware logic, while orchestration instances are permanently associated with a specific version when created.

## How it works

The orchestration versioning feature operates on these core principles:

**Version Association**: When an orchestration instance is created, it gets a version permanently associated with it.**Version-aware Execution**: Orchestrator function code can examine the version value associated with the current orchestration instance and branch execution accordingly.**Backward Compatibility**: Workers running newer orchestrator versions can continue executing orchestration instances created by older orchestrator versions.**Forward Protection**: The runtime automatically prevents workers running older orchestrator versions from executing orchestrations started by newer orchestrator versions.

Important

Orchestration versioning is currently in public preview.

## Prerequisites

Before using orchestration versioning, ensure you have the required package versions for your programming language.

If you're using a non-.NET language (JavaScript, Python, PowerShell, or Java) with [extension bundles](../extension-bundles), your function app must reference **Extension Bundle version 4.26.0 or later**. Configure the `extensionBundle`

range in `host.json`

so that the minimum version is at least `4.26.0`

, for example:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.26.0, 5.0.0)"
}
}
```


See the [extension bundle configuration documentation](../extension-bundles) for details on choosing and updating bundle versions.

Use `Microsoft.Azure.Functions.Worker.Extensions.DurableTask`

version [1.5.0](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask/1.5.0) or later.

## Basic usage

The most common use case for orchestration versioning is when you need to make breaking changes to your orchestrator logic while keeping existing in-flight orchestration instances running with their original version. All you need to do is update the `defaultVersion`

in your `host.json`

and modify your orchestrator code to check the orchestration version and branch execution accordingly. Let's walk through the required steps.

Note

The behavior described in this section targets the most common situations, and this is what the default configuration provides. However, it can be modified if needed (see [Advanced usage](#advanced-usage) for details).

### Step 1: defaultVersion configuration

To configure the default version for your orchestrations, you need to add or update the `defaultVersion`

setting in the `host.json`

file in your Azure Functions project:

```
{
"extensions": {
"durableTask": {
"defaultVersion": "<version>"
}
}
}
```


The version string can follow any format that suits your versioning strategy:

- Multi-part versioning:
`"1.0.0"`

,`"2.1.0"`

- Simple numbering:
`"1"`

,`"2"`

- Date-based:
`"2025-01-01"`

- Custom format:
`"v1.0-release"`


After you set the `defaultVersion`

, all new orchestration instances will be permanently associated with that version.

#### Version comparison rules

When the `Strict`

or `CurrentOrOlder`

strategy is selected (see [Version matching](#version-matching)), the runtime compares the orchestration instance's version with the `defaultVersion`

value of the worker using the following rules:

- Empty or null versions are treated as equal.
- An empty or null version is considered older than any defined version.
- If both versions can be parsed as
`System.Version`

, the`CompareTo`

method is used. - Otherwise, case-insensitive string comparison is performed.

### Step 2: Orchestrator function logic

To implement version-aware logic in your orchestrator function, you can use the context parameter passed to the orchestrator to access the current orchestration instance's version, which allows you to branch your orchestrator logic based on the version.

Important

When implementing version-aware logic, it's **critically important** to preserve the exact orchestrator logic for older versions. Any changes to the sequence, order, or signature of activity calls for existing versions may break deterministic replay and cause in-flight orchestrations to fail or produce incorrect results. The old version code paths must remain unchanged once deployed.

```
[Function("MyOrchestrator")]
public static async Task<string> RunOrchestrator(
[OrchestrationTrigger] TaskOrchestrationContext context)
{
if (context.Version == "1.0")
{
// Original logic for version 1.0
...
}
else if (context.Version == "2.0")
{
// New logic for version 2.0
...
}
...
}
```


Note

The `context.Version`

property is **read-only** and reflects the version that was permanently associated with the orchestration instance when it was created. You cannot modify this value during orchestration execution. If you want to specify a version through means other than `host.json`

, you can do so when starting an orchestration instance with the orchestration client APIs (see [Starting new orchestrations and sub-orchestrations with specific versions](#starting-new-orchestrations-and-sub-orchestrations-with-specific-versions)).

Tip

If you're just starting to use orchestration versioning and you already have in-flight orchestrations that were created before you specified a `defaultVersion`

, you can still add the `defaultVersion`

setting to your `host.json`

now. For all previously created orchestrations, `context.Version`

returns `null`

(or an equivalent language-dependent value), so you can structure your orchestrator logic to handle both the legacy (null version) and new versioned orchestrations accordingly. The following are the language-dependent values to check for the legacy case:

- C#:
`context.Version == null`

or`context.Version is null`

- JavaScript:
`context.df.version == null`

- Python:
`context.version is None`

- PowerShell:
`$null -eq $Context.Version`

- Java:
`context.getVersion() == null`

Also note that specifying`"defaultVersion": null`

in`host.json`

is equivalent to not specifying it at all.

Tip

Depending on your situation, you may prefer branching on different levels. You can make a local change precisely where this change is required, like the example shows. Alternatively, you can branch at a higher level, even at the entire orchestrator implementation level, which introduces some code duplication, but may keep the execution flow clear. It's up to you to choose the approach that best fits your scenario and coding style.

### What happens after deployment

Here's what to expect once you deploy your updated orchestrator function with the new version logic:

**Worker Coexistence**: Workers containing the new orchestrator function code will start, while some workers with the old code are potentially still active.**Version Assignment for New Instances**: All new orchestrations and sub-orchestrations created by the new workers will get the version from`defaultVersion`

assigned to them.**New Worker Compatibility**: New workers will be able to process both the newly created orchestrations and the previously existing orchestrations because the changes performed in Step 2 of the previous section ensure backward compatibility through version-aware branching logic.**Old Worker Restrictions**: Old workers will be allowed to process only the orchestrations with a version*equal to or lower*than the version specified in their own`defaultVersion`

in`host.json`

, because they aren't expected to have orchestrator code compatible with newer versions. This restriction prevents execution errors and unexpected behavior.

Note

Orchestration versioning doesn't influence worker lifecycle. The Azure Functions platform manages worker provisioning and decommissioning based on regular rules depending on hosting options.

### Example: Replacing an activity in the sequence

This example shows how to replace one activity with a different activity in the middle of a sequence using orchestration versioning.

#### Version 1.0

**host.json configuration:**

```
{
"extensions": {
"durableTask": {
"defaultVersion": "1.0"
}
}
}
```


**Orchestrator function:**

```
[Function("ProcessOrderOrchestrator")]
public static async Task<string> ProcessOrder(
[OrchestrationTrigger] TaskOrchestrationContext context)
{
var orderId = context.GetInput<string>();
await context.CallActivityAsync("ValidateOrder", orderId);
await context.CallActivityAsync("ProcessPayment", orderId);
await context.CallActivityAsync("ShipOrder", orderId);
return "Order processed successfully";
}
```


#### Version 2.0 with discount processing

**host.json configuration:**

```
{
"extensions": {
"durableTask": {
"defaultVersion": "2.0"
}
}
}
```


**Orchestrator function:**

```
using DurableTask.Core.Settings;
[Function("ProcessOrderOrchestrator")]
public static async Task<string> ProcessOrder(
[OrchestrationTrigger] TaskOrchestrationContext context)
{
var orderId = context.GetInput<string>();
await context.CallActivityAsync("ValidateOrder", orderId);
if (VersioningSettings.CompareVersions(context.Version, "1.0") <= 0)
{
// Preserve original logic for existing instances
await context.CallActivityAsync("ProcessPayment", orderId);
}
else // a higher version (including 2.0)
{
// New logic with discount processing (replaces payment processing)
await context.CallActivityAsync("ApplyDiscount", orderId);
await context.CallActivityAsync("ProcessPaymentWithDiscount", orderId);
}
await context.CallActivityAsync("ShipOrder", orderId);
return "Order processed successfully";
}
```


## Advanced usage

For more sophisticated versioning scenarios, you can configure other settings to control how the runtime handles version matches and mismatches.

Tip

Use the default configuration (`CurrentOrOlder`

with `Reject`

) for most scenarios to enable safe rolling deployments while preserving orchestration state during version transitions. We recommend proceeding with the advanced configuration only if you have specific requirements that can't be met with the default behavior.

### Version matching

The `versionMatchStrategy`

setting determines how the runtime matches orchestration versions when loading orchestrator functions. It controls which orchestration instances a worker can process based on version compatibility.

#### Configuration

```
{
"extensions": {
"durableTask": {
"defaultVersion": "<version>",
"versionMatchStrategy": "CurrentOrOlder"
}
}
}
```


#### Available strategies

(not recommended): Ignore orchestration version completely. All work received is processed regardless of version. This strategy effectively disables version checking and allows any worker to process any orchestration instance.`None`

: Only process tasks from orchestrations with the exact same version as the version specified by`Strict`

`defaultVersion`

in the worker's`host.json`

. This strategy provides the highest level of version isolation but requires careful deployment coordination to avoid orphaned orchestrations. The consequences of version mismatch are described in the[Version mismatch handling](#version-mismatch-handling)section.(default): Process tasks from orchestrations whose version is less than or equal to the version specified by`CurrentOrOlder`

`defaultVersion`

in the worker's`host.json`

. This strategy enables backward compatibility, allowing newer workers to handle orchestrations started by older orchestrator versions while preventing older workers from processing newer orchestrations. The consequences of version mismatch are described in the[Version mismatch handling](#version-mismatch-handling)section.

### Version mismatch handling

The `versionFailureStrategy`

setting determines what happens when an orchestration instance version doesn't match the current `defaultVersion`

.

**Configuration:**

```
{
"extensions": {
"durableTask": {
"defaultVersion": "<version>",
"versionFailureStrategy": "Reject"
}
}
}
```


**Available strategies:**

(default): Don't process the orchestration. The orchestration instance remains in its current state and can be retried later when a compatible worker becomes available. This strategy is the safest option as it preserves orchestration state.`Reject`

: Fail the orchestration. This strategy immediately terminates the orchestration instance with a failure state, which may be appropriate in scenarios where version mismatches indicate serious deployment issues.`Fail`


### Starting new orchestrations and sub-orchestrations with specific versions

By default, all new orchestration instances are created with the current `defaultVersion`

specified in your `host.json`

configuration. However, you may have scenarios where you need to create orchestrations with a specific version, even if it differs from the current default.

**When to use specific versions:**

**Gradual migration**: You want to keep creating orchestrations with an older version even after deploying a newer version.**Testing scenarios**: You need to test specific version behavior in production.**Rollback situations**: You need to temporarily revert to creating instances with a previous version.**Version-specific workflows**: Different business processes require different orchestration versions.

You can override the default version by providing a specific version value when creating new orchestration instances using the orchestration client APIs. This allows fine-grained control over which version each new orchestration instance uses.

```
[Function("HttpStart")]
public static async Task<HttpResponseData> HttpStart(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestData req,
[DurableClient] DurableTaskClient client,
FunctionContext executionContext)
{
var options = new StartOrchestrationOptions
{
Version = "1.0"
};
string instanceId = await client.ScheduleNewOrchestrationInstanceAsync("ProcessOrderOrchestrator", orderId, options);
// ...
}
```


You can also start sub-orchestrations with specific versions from within an orchestrator function:

```
[Function("MainOrchestrator")]
public static async Task<string> RunMainOrchestrator(
[OrchestrationTrigger] TaskOrchestrationContext context)
{
var subOptions = new SubOrchestratorOptions
{
Version = "1.0"
};
var result = await context.CallSubOrchestratorAsync<string>("ProcessPaymentOrchestrator", orderId, subOptions);
// ...
}
```


### Removing legacy code paths

Over time, you may want to remove legacy code paths from your orchestrator functions to simplify maintenance and reduce technical debt. However, removing code must be done carefully to avoid breaking existing orchestration instances.

**When it's safe to remove legacy code:**

- All orchestration instances using the old version have completed (succeeded, failed, or been terminated)
- No new orchestration instances will be created with the old version
- You have verified through monitoring or querying that no instances are running with the legacy version
- A sufficient time period has passed since the old version was last deployed (considering your business continuity requirements)

**Best practices for removal:**

**Monitor actively running instances**: Use the Durable Functions management APIs to query for instances using specific versions.**Set retention policies**: Define how long you intend to maintain backward compatibility for each version.**Remove incrementally**: Consider removing one version at a time rather than multiple versions simultaneously.**Document removal**: Maintain clear records of when versions were removed and why.

Warning

Removing legacy code paths while orchestration instances are still running those versions may cause deterministic replay failures or unexpected behavior. Always verify that no instances are using the legacy version before removing the code.

## Best practices

### Version management

**Use multi-part versioning**: Adopt a consistent versioning scheme like`major.minor.patch`

.**Document breaking changes**: Clearly document what changes require a new version.**Plan version lifecycle**: Define when to remove legacy code paths.

### Code organization

**Separate version logic**: Use clear branching or separate methods for different versions.**Preserve determinism**: Avoid modifying existing version logic once deployed. If changes are absolutely necessary (such as critical bug fixes), ensure they maintain deterministic behavior and don't alter the sequence of operations, or expect the newer orchestrator versions to fail when processing older orchestrations.**Test thoroughly**: Test all version paths, especially during transitions.

### Monitoring and observability

**Log version information**: Include version in your logging for easier debugging.**Monitor version distribution**: Track which versions are actively running.**Set up alerts**: Monitor for any version-related errors.

## Troubleshooting

### Common issues

**Issue**: Orchestration instances created with version 1.0 are failing after deploying version 2.0**Solution**: Ensure the version 1.0 code path in your orchestrator remains exactly the same. Any changes to the execution sequence may break deterministic replay.

**Issue**: Workers running older orchestrator versions can't execute new orchestrations**Solution**: This is expected behavior. The runtime intentionally prevents older workers from executing orchestrations with newer versions to maintain safety. Ensure all workers are updated to the latest orchestrator version and their`defaultVersion`

setting in`host.json`

is updated accordingly. You can modify this behavior if needed using the advanced configuration options (see[Advanced usage](#advanced-usage)for details).

**Issue**: Version information isn't available in orchestrator (`context.Version`

or`context.getVersion()`

is null, regardless of the`defaultVersion`

setting)**Solution**: Check the[Prerequisites](#prerequisites)section to ensure your environment meets all the requirements for orchestration versioning.

**Issue**: Orchestrations of a newer version are making very slow progress or are completely stuck**Solution**: The problem can have different root causes:**Insufficient newer workers**: Make sure that a sufficient number of workers containing an equal or higher version in`defaultVersion`

are deployed and active to handle the newer orchestrations.**Orchestration routing interference from older workers**: Old workers can interfere with the orchestration routing mechanism, making it harder for new workers to pick up orchestrations for processing. This can be especially noticeable when using certain storage providers (Azure Storage or MSSQL). Normally, the Azure Functions platform ensures that old workers are disposed of soon after a deployment, so any delay is typically not significant. However, if you are using a configuration that allows you to control the lifecycle of older workers, make sure the older workers are eventually shut down. Alternatively, consider using the[Durable Task Scheduler](durable-task-scheduler/durable-task-scheduler), as it provides an improved routing mechanism that is less susceptible to this issue.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-diagnostics -->

# Diagnostics in Durable Functions in Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

There are several options for diagnosing issues with [Durable Functions](durable-functions-overview). Some of these options are the same for regular functions and some of them are unique to Durable Functions.

## Application Insights

[Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview) is the recommended way to do diagnostics and monitoring in Azure Functions. The same applies to Durable Functions. For an overview of how to use Application Insights in your function app, see [Monitor Azure Functions](../functions-monitoring).

The Azure Functions Durable Extension also emits *tracking events* that allow you to trace the end-to-end execution of an orchestration. These tracking events can be found and queried using the [Application Insights Analytics](/en-us/azure/azure-monitor/logs/log-query-overview) tool in the Azure portal.

### Tracking data

Each lifecycle event of an orchestration instance causes a tracking event to be written to the **traces** collection in Application Insights. This event contains a **customDimensions** payload with several fields. Field names are all prepended with `prop__`

.

**hubName**: The name of the task hub in which your orchestrations are running.**appName**: The name of the function app. This field is useful when you have multiple function apps sharing the same Application Insights instance.**slotName**: The[deployment slot](../functions-deployment-slots)in which the current function app is running. This field is useful when you use deployment slots to version your orchestrations.**functionName**: The name of the orchestrator or activity function.**functionType**: The type of the function, such as**Orchestrator**or**Activity**.**instanceId**: The unique ID of the orchestration instance.**state**: The lifecycle execution state of the instance. Valid values include:**Scheduled**: The function was scheduled for execution but hasn't started running yet.**Started**: The function started running but has not yet awaited or completed.**Awaited**: The orchestrator has scheduled some work and is waiting for it to complete.**Listening**: The orchestrator is listening for an external event notification.**Completed**: The function completed successfully.**Failed**: The function failed with an error.

**reason**: Additional data associated with the tracking event. For example, if an instance is waiting for an external event notification, this field indicates the name of the event it is waiting for. If a function fails, this field contains the error details.**isReplay**: Boolean value indicating whether the tracking event is for replayed execution.**extensionVersion**: The version of the Durable Task extension. The version information is especially important data when reporting possible bugs in the extension. Long-running instances may report multiple versions if an update occurs while it is running.**sequenceNumber**: Execution sequence number for an event. Combined with the timestamp helps to order the events by execution time.*Note that this number resets to zero if the host restarts while the instance is running, so it's important to always sort by timestamp first, then sequenceNumber.*

The verbosity of tracking data emitted to Application Insights can be configured in the `logger`

(Functions 1.x) or `logging`

(Functions 2.0) section of the `host.json`

file.

#### Functions 1.0

```
{
"logger": {
"categoryFilter": {
"categoryLevels": {
"Host.Triggers.DurableTask": "Information"
}
}
}
}
```


#### Functions 2.0

```
{
"logging": {
"logLevel": {
"Host.Triggers.DurableTask": "Information",
},
}
}
```


By default, all *non-replay* tracking events are emitted. The volume of data can be reduced by setting `Host.Triggers.DurableTask`

to `"Warning"`

or `"Error"`

in which case tracking events are only emitted for exceptional situations. To enable emitting the verbose orchestration replay events, set the `logReplayEvents`

to `true`

in the [host.json](durable-functions-bindings#host-json) configuration file.

Note

By default, the Azure Functions runtime samples Application Insights telemetry to avoid emitting data too frequently. Sampling can cause tracking information to be lost when many lifecycle events occur in a short period of time. The [Azure Functions Monitoring article](../configure-monitoring#configure-sampling) explains how to configure this behavior.

Inputs and outputs of orchestrator, activity, and entity functions are not logged by default. This default behavior is recommended because logging inputs and outputs could increase Application Insights costs. Function input and output payloads may also contain sensitive information. Instead, the number of bytes for function inputs and outputs are logged instead of the actual payloads by default. If you want the Durable Functions extension to log the full input and output payloads, set the `traceInputsAndOutputs`

property to `true`

in the [host.json](durable-functions-bindings#host-json) configuration file.

### Single instance query

The following query shows historical tracking data for a single instance of the [Hello Sequence](durable-functions-sequence) function orchestration. It's written using the [Kusto Query Language](/en-us/azure/data-explorer/kusto/query/). It filters out replay execution so that only the *logical* execution path is shown. Events can be ordered by sorting by `timestamp`

and `sequenceNumber`

as shown in the query below:

```
let targetInstanceId = "ddd1aaa685034059b545eb004b15d4eb";
let start = datetime(2018-03-25T09:20:00);
traces
| where timestamp > start and timestamp < start + 30m
| where customDimensions.Category == "Host.Triggers.DurableTask"
| extend functionName = customDimensions["prop__functionName"]
| extend instanceId = customDimensions["prop__instanceId"]
| extend state = customDimensions["prop__state"]
| extend isReplay = tobool(tolower(customDimensions["prop__isReplay"]))
| extend sequenceNumber = tolong(customDimensions["prop__sequenceNumber"])
| where isReplay != true
| where instanceId == targetInstanceId
| sort by timestamp asc, sequenceNumber asc
| project timestamp, functionName, state, instanceId, sequenceNumber, appName = cloud_RoleName
```


The result is a list of tracking events that shows the execution path of the orchestration, including any activity functions ordered by the execution time in ascending order.

### Instance summary query

The following query displays the status of all orchestration instances that were run in a specified time range.

```
let start = datetime(2017-09-30T04:30:00);
traces
| where timestamp > start and timestamp < start + 1h
| where customDimensions.Category == "Host.Triggers.DurableTask"
| extend functionName = tostring(customDimensions["prop__functionName"])
| extend instanceId = tostring(customDimensions["prop__instanceId"])
| extend state = tostring(customDimensions["prop__state"])
| extend isReplay = tobool(tolower(customDimensions["prop__isReplay"]))
| extend output = tostring(customDimensions["prop__output"])
| where isReplay != true
| summarize arg_max(timestamp, *) by instanceId
| project timestamp, instanceId, functionName, state, output, appName = cloud_RoleName
| order by timestamp asc
```


The result is a list of instance IDs and their current runtime status.

## Durable Task Framework Logging

The Durable extension logs are useful for understanding the behavior of your orchestration logic. However, these logs don't always contain enough information to debug framework-level performance and reliability issues. Starting in **v2.3.0** of the Durable extension, logs emitted by the underlying Durable Task Framework (DTFx) are also available for collection.

When looking at logs emitted by the DTFx, it's important to understand that the DTFx engine is composed of two components: the core dispatch engine (`DurableTask.Core`

) and one of many supported storage providers (Durable Functions uses `DurableTask.AzureStorage`

by default but [other options are available](durable-functions-storage-providers)).

**DurableTask.Core**: Core orchestration execution and low-level scheduling logs and telemetry.**DurableTask.AzureStorage**: Backend logs specific to the Azure Storage state provider. These logs include detailed interactions with the internal queues, blobs, and storage tables used to store and fetch internal orchestration state.**DurableTask.Netherite**: Backend logs specific to the[Netherite storage provider](https://microsoft.github.io/durabletask-netherite), if enabled.**DurableTask.SqlServer**: Backend logs specific to the[Microsoft SQL (MSSQL) storage provider](https://microsoft.github.io/durabletask-mssql), if enabled.

You can enable these logs by updating the `logging/logLevel`

section of your function app's **host.json** file. The following example shows how to enable warning and error logs from both `DurableTask.Core`

and `DurableTask.AzureStorage`

:

```
{
"version": "2.0",
"logging": {
"logLevel": {
"DurableTask.AzureStorage": "Warning",
"DurableTask.Core": "Warning"
}
}
}
```


If you have Application Insights enabled, these logs are automatically added to the `trace`

collection. You can search them the same way that you search for other `trace`

logs using Kusto queries.

Note

For production applications, it is recommended that you enable `DurableTask.Core`

and the appropriate storage provider (e.g. `DurableTask.AzureStorage`

) logs using the `"Warning"`

filter. Higher verbosity filters such as `"Information"`

are useful for debugging performance issues. However, these log events can be high-volume and can significantly increase Application Insights data storage costs.

The following Kusto query shows how to query for DTFx logs. The most important part of the query is `where customerDimensions.Category startswith "DurableTask"`

since that filters the results to logs in the `DurableTask.Core`

and `DurableTask.AzureStorage`

categories.

```
traces
| where customDimensions.Category startswith "DurableTask"
| project
timestamp,
severityLevel,
Category = customDimensions.Category,
EventId = customDimensions.EventId,
message,
customDimensions
| order by timestamp asc
```


The result is a set of logs written by the Durable Task Framework log providers.

For more information about what log events are available, see the [Durable Task Framework structured logging documentation on GitHub](https://github.com/Azure/durabletask/tree/master/src/DurableTask.Core/Logging#durabletaskcore-logging).

## App Logging

It's important to keep the orchestrator replay behavior in mind when writing logs directly from an orchestrator function. For example, consider the following orchestrator function:

```
[FunctionName("FunctionChain")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context,
ILogger log)
{
log.LogInformation("Calling F1.");
await context.CallActivityAsync("F1");
log.LogInformation("Calling F2.");
await context.CallActivityAsync("F2");
log.LogInformation("Calling F3");
await context.CallActivityAsync("F3");
log.LogInformation("Done!");
}
```


The resulting log data is going to look something like the following example output:

```
Calling F1.
Calling F1.
Calling F2.
Calling F1.
Calling F2.
Calling F3.
Calling F1.
Calling F2.
Calling F3.
Done!
```


Note

Remember that while the logs claim to be calling F1, F2, and F3, those functions are *only* called the first time they are encountered. Subsequent calls that happen during replay are skipped and the outputs are replayed to the orchestrator logic.

If you want to only write logs on non-replay executions, you can write a conditional expression to log only if the "is replaying" flag is `false`

. Consider the example above, but this time with replay checks.

```
[FunctionName("FunctionChain")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context,
ILogger log)
{
if (!context.IsReplaying) log.LogInformation("Calling F1.");
await context.CallActivityAsync("F1");
if (!context.IsReplaying) log.LogInformation("Calling F2.");
await context.CallActivityAsync("F2");
if (!context.IsReplaying) log.LogInformation("Calling F3");
await context.CallActivityAsync("F3");
log.LogInformation("Done!");
}
```


Starting in Durable Functions 2.0, .NET orchestrator functions can create an `ILogger`

that automatically filters out log statements during replay. This automatic filtering is done using the [IDurableOrchestrationContext.CreateReplaySafeLogger(ILogger)](/en-us/dotnet/api/microsoft.azure.webjobs.extensions.durabletask.durablecontextextensions.createreplaysafelogger) API.

```
[FunctionName("FunctionChain")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context,
ILogger log)
{
log = context.CreateReplaySafeLogger(log);
log.LogInformation("Calling F1.");
await context.CallActivityAsync("F1");
log.LogInformation("Calling F2.");
await context.CallActivityAsync("F2");
log.LogInformation("Calling F3");
await context.CallActivityAsync("F3");
log.LogInformation("Done!");
}
```


Note

The previous C# examples are for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

With the previously mentioned changes, the log output is as follows:

```
Calling F1.
Calling F2.
Calling F3.
Done!
```


## Custom Status

Custom orchestration status lets you set a custom status value for your orchestrator function. This custom status is then visible to external clients via the [HTTP status query API](durable-functions-http-api#get-instance-status) or via language-specific API calls. The custom orchestration status enables richer monitoring for orchestrator functions. For example, the orchestrator function code can invoke the "set custom status" API to update the progress for a long-running operation. A client, such as a web page or other external system, could then periodically query the HTTP status query APIs for richer progress information. Sample code for setting a custom status value in an orchestrator function is provided below:

```
[FunctionName("SetStatusTest")]
public static async Task SetStatusTest([OrchestrationTrigger] IDurableOrchestrationContext context)
{
// ...do work...
// update the status of the orchestration with some arbitrary data
var customStatus = new { completionPercentage = 90.0, status = "Updating database records" };
context.SetCustomStatus(customStatus);
// ...do more work...
}
```


Note

The previous C# example is for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

While the orchestration is running, external clients can fetch this custom status:

```
GET /runtime/webhooks/durabletask/instances/instance123?code=XYZ
```


Clients get the following response:

```
{
"runtimeStatus": "Running",
"input": null,
"customStatus": { "completionPercentage": 90.0, "status": "Updating database records" },
"output": null,
"createdTime": "2017-10-06T18:30:24Z",
"lastUpdatedTime": "2017-10-06T19:40:30Z"
}
```


Warning

The custom status payload is limited to 16 KB of UTF-16 JSON text because it needs to be able to fit in an Azure Table Storage column. You can use external storage if you need larger payload.

## Distributed Tracing

Distributed Tracing tracks requests and shows how different services interact with each other. In Durable Functions, it also correlates orchestrations, entities, and activities together. This is helpful to understand how much time steps of the orchestration take relative to the entire orchestration. It is also useful to understand where an application is having an issue or where an exception was thrown. This feature is supported in Application Insights for all languages and storage providers.

Note

- For .NET Isolated apps, Distributed Tracing V2 requires
[Microsoft.Azure.Functions.Worker.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask)**>= v1.4.0**. - For non-.NET apps,
[follow these instructions](durable-functions-extension-upgrade#manually-upgrade-the-durable-functions-extension)to manually install[Microsoft.Azure.WebJobs.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask)**>= v3.2.0**for now. Distributed Tracing will be available in extension bundles**>**.[v4.24.x](https://github.com/Azure/azure-functions-extension-bundles/releases)

### Setting up Distributed Tracing

To set up distributed tracing, update the host.json and set up an Application Insights resource.

#### host.json

```
{
"extensions": {
"durableTask": {
"tracing": {
"distributedTracingEnabled": true,
"version": "V2"
}
}
}
}
```


#### Application Insights

If the Function app is not configured with an Application Insights resource, then configure it following the instructions [here](../configure-monitoring#enable-application-insights-integration).

### Inspecting the traces

In the Application Insights resource, navigate to **Transaction Search**. In the results, check for `Request`

and `Dependency`

events that start with Durable Functions specific prefixes (e.g. `orchestration:`

, `activity:`

, etc.). Selecting one of these events opens up a Gantt chart that shows the end to end distributed trace.

### Troubleshooting

If you don't see the traces in Application Insights, make sure to wait about five minutes after running the application to ensure that all of the data is propagated to the Application Insights resource.

## Debugging

Azure Functions supports debugging function code directly, and that same support carries forward to Durable Functions, whether running in Azure or locally. However, there are a few behaviors to be aware of when debugging:

**Replay**: Orchestrator functions regularly[replay](durable-functions-orchestrations#reliability)when new inputs are received. This behavior means a single*logical*execution of an orchestrator function can result in hitting the same breakpoint multiple times, especially if it is set early in the function code.**Await**: Whenever an`await`

is encountered in an orchestrator function, it yields control back to the Durable Task Framework dispatcher. If it is the first time a particular`await`

has been encountered, the associated task is*never*resumed. Because the task never resumes, stepping*over*the await (F10 in Visual Studio) is not possible. Stepping over only works when a task is being replayed.**Messaging timeouts**: Durable Functions internally uses queue messages to drive execution of orchestrator, activity, and entity functions. In a multi-VM environment, breaking into the debugging for extended periods of time could cause another VM to pick up the message, resulting in duplicate execution. This behavior exists for regular queue-trigger functions as well, but is important to point out in this context since the queues are an implementation detail.**Stopping and starting**: Messages in Durable functions persist between debug sessions. If you stop debugging and terminate the local host process while a durable function is executing, that function may re-execute automatically in a future debug session. This behavior can be confusing when not expected. Using a[fresh task hub](durable-functions-task-hubs#task-hub-management)or clearing the task hub contents between debug sessions is one technique to avoid this behavior.

Tip

When setting breakpoints in orchestrator functions, if you want to only break on non-replay execution, you can set a conditional breakpoint that breaks only if the "is replaying" value is `false`

.

## Storage

By default, Durable Functions stores state in Azure Storage. This behavior means you can inspect the state of your orchestrations using tools such as [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer).

This is useful for debugging because you see exactly what state an orchestration may be in. Messages in the queues can also be examined to learn what work is pending (or stuck in some cases).

Warning

While it's convenient to see execution history in table storage, avoid taking any dependency on this table. It may change as the Durable Functions extension evolves.

Note

Other storage providers can be configured instead of the default Azure Storage provider. Depending on the storage provider configured for your app, you may need to use different tools to inspect the underlying state. For more information, see the [Durable Functions Storage Providers](durable-functions-storage-providers) documentation.

## Durable Functions Monitor

[Durable Functions Monitor](https://github.com/microsoft/DurableFunctionsMonitor) is a graphical tool for monitoring, managing, and debugging orchestration and entity instances. It is available as a Visual Studio Code extension or a standalone app. Information about set up and a list of features can be found in [this Wiki](https://github.com/microsoft/DurableFunctionsMonitor/wiki).

## Durable Functions troubleshooting guide

To troubleshoot common problem symptoms such as orchestrations being stuck, failing to start, running slowly, etc., refer to this [troubleshooting guide](durable-functions-troubleshooting-guide).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-entities -->

# Entity functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Entity functions define operations for reading and updating small pieces of state, known as *durable entities*. Like orchestrator functions, entity functions are functions with a special trigger type, the *entity trigger*. Unlike orchestrator functions, entity functions manage the state of an entity explicitly, rather than implicitly representing state via control flow.
Entities provide a means for scaling out applications by distributing the work across many entities, each with a modestly sized state.

Note

Entity functions and related functionality are only available in [Durable Functions 2.0](durable-functions-versions#migrate-from-1x-to-2x) and above. They are currently supported in .NET in-proc, .NET isolated worker, JavaScript, and Python, but not in PowerShell or Java. Furthermore, entity functions for .NET Isolated are supported when using the Azure Storage or Netherite state providers, but not when using the MSSQL state provider.

Important

Entity functions aren't currently supported in PowerShell and Java.

## General concepts

Entities behave a bit like tiny services that communicate via messages. Each entity has a unique identity and an internal state (if it exists). Like services or objects, entities perform operations when prompted to do so. When an operation executes, it might update the internal state of the entity. It might also call external services and wait for a response. Entities communicate with other entities, orchestrations, and clients by using messages that are implicitly sent via reliable queues.

To prevent conflicts, all operations on a single entity are guaranteed to execute serially, that is, one after another.

Note

When an entity is invoked, it processes its payload to completion and then schedules a new execution to activate once future inputs arrive. As a result, your entity execution logs might show an extra execution after each entity invocation; this is expected.

### Entity ID

Entities are accessed via a unique identifier, the *entity ID*. An entity ID is simply a pair of strings that uniquely identifies an entity instance. It consists of an:

**Entity name**, which is a name that identifies the type of the entity. An example is "Counter." This name must match the name of the entity function that implements the entity. It isn't sensitive to case.**Entity key**, which is a string that uniquely identifies the entity among all other entities of the same name. An example is a GUID.

For example, a `Counter`

entity function might be used for keeping score in an online game. Each instance of the game has a unique entity ID, such as `@Counter@Game1`

and `@Counter@Game2`

. All operations that target a particular entity require specifying an entity ID as a parameter.

### Entity operations

To invoke an operation on an entity, specify the:

**Entity ID**of the target entity.**Operation name**, which is a string that specifies the operation to perform. For example, the`Counter`

entity could support`add`

,`get`

, or`reset`

operations.**Operation input**, which is an optional input parameter for the operation. For example, the add operation can take an integer amount as the input.**Scheduled time**, which is an optional parameter for specifying the delivery time of the operation. For example, an operation can be reliably scheduled to run several days in the future.

Operations can return a result value or an error result, such as a JavaScript error or a .NET exception. This result or error occurs in orchestrations that called the operation.

An entity operation can also create, read, update, and delete the state of the entity. The state of the entity is always durably persisted in storage.

## Define entities

You define entities using a function-based syntax, where entities are represented as functions and operations are explicitly dispatched by the application.

Currently, there are two distinct APIs for defining entities in .NET:

When you use a function-based syntax, entities are represented as functions and operations are explicitly dispatched by the application. This syntax works well for entities with simple state, few operations, or a dynamic set of operations like in application frameworks. This syntax can be tedious to maintain because it doesn't catch type errors at compile time.

The specific APIs depend on whether your C# functions run in an *isolated worker process* (recommended) or in the same process as the host.

The following code is an example of a simple `Counter`

entity implemented as a durable function. This function defines three operations, `add`

, `reset`

, and `get`

, each of which operates on an integer state.

```
[FunctionName("Counter")]
public static void Counter([EntityTrigger] IDurableEntityContext ctx)
{
switch (ctx.OperationName.ToLowerInvariant())
{
case "add":
ctx.SetState(ctx.GetState<int>() + ctx.GetInput<int>());
break;
case "reset":
ctx.SetState(0);
break;
case "get":
ctx.Return(ctx.GetState<int>());
break;
}
}
```


For more information on the function-based syntax and how to use it, see [Function-based syntax](durable-functions-dotnet-entities#function-based-syntax).

Durable entities are available in JavaScript starting with version **1.3.0** of the `durable-functions`

npm package. The following code is the `Counter`

entity implemented as a durable function written in JavaScript.

**Counter/function.json**

```
{
"bindings": [
{
"name": "context",
"type": "entityTrigger",
"direction": "in"
}
],
"disabled": false
}
```


**Counter/index.js**

```
const df = require("durable-functions");
module.exports = df.entity(function(context) {
const currentValue = context.df.getState(() => 0);
switch (context.df.operationName) {
case "add":
const amount = context.df.getInput();
context.df.setState(currentValue + amount);
break;
case "reset":
context.df.setState(0);
break;
case "get":
context.df.return(currentValue);
break;
}
});
```


Note

Refer to the [Azure Functions Python developer guide](../functions-reference-python) for more details about how the V2 model works.

The following code is the `Counter`

entity implemented as a durable function written in Python.

```
import azure.functions as func
import azure.durable_functions as df
# Entity function called counter
@myApp.entity_trigger(context_name="context")
def Counter(context):
current_value = context.get_state(lambda: 0)
operation = context.operation_name
if operation == "add":
amount = context.get_input()
current_value += amount
elif operation == "reset":
current_value = 0
elif operation == "get":
context.set_result(current_value)
context.set_state(current_value)
```


## Access entities

Entities can be accessed using one-way or two-way communication. The following terminology distinguishes the two forms of communication:

**Calling**an entity uses two-way (round-trip) communication. You send an operation message to the entity, and then wait for the response message before you continue. The response message can provide a result value or an error result, such as a JavaScript error or a .NET exception. This result or error is then observed by the caller.**Signaling**an entity uses one-way (fire and forget) communication. You send an operation message but don't wait for a response. While the message is guaranteed to be delivered eventually, the sender doesn't know when and can't observe any result value or errors.

Entities can be accessed from within client functions, from within orchestrator functions, or from within entity functions. Not all forms of communication are supported by all contexts:

- From within clients, you can signal entities and you can read the entity state.
- From within orchestrations, you can signal entities and you can call entities.
- From within entities, you can signal entities.

The following examples illustrate these various ways of accessing entities.

### Example: Client signals an entity

To access entities from an ordinary Azure Function, which is also known as a client function, use the [entity client binding](durable-functions-bindings#entity-client). The following example shows a queue-triggered function signaling an entity using this binding.

Note

For simplicity, the following examples show the loosely typed syntax for accessing entities. In general, we recommend that you [access entities through interfaces](durable-functions-dotnet-entities#accessing-entities-through-interfaces) because it provides more type checking.

```
[FunctionName("AddFromQueue")]
public static Task Run(
[QueueTrigger("durable-function-trigger")] string input,
[DurableClient] IDurableEntityClient client)
{
// Entity operation input comes from the queue message content.
var entityId = new EntityId(nameof(Counter), "myCounter");
int amount = int.Parse(input);
return client.SignalEntityAsync(entityId, "Add", amount);
}
```


```
const df = require("durable-functions");
module.exports = async function (context) {
const client = df.getClient(context);
const entityId = new df.EntityId("Counter", "myCounter");
await client.signalEntity(entityId, "add", 1);
};
```


```
import azure.functions as func
import azure.durable_functions as df
# An HTTP-Triggered Function with a Durable Functions Client to set a value on a durable entity
@myApp.route(route="entitysetvalue")
@myApp.durable_client_input(client_name="client")
async def http_set(req: func.HttpRequest, client):
logging.info('Python HTTP trigger function processing a request.')
entityId = df.EntityId("Counter", "myCounter")
await client.signal_entity(entityId, "add", 1)
return func.HttpResponse("Done", status_code=200)
```


The term *signal* means that the entity API invocation is one-way and asynchronous. It's not possible for a client function to know when the entity has processed the operation. Also, the client function can't observe any result values or exceptions.

### Example: Client reads an entity state

Client functions can also query the state of an entity, as shown in the following example:

```
[FunctionName("QueryCounter")]
public static async Task<HttpResponseMessage> Run(
[HttpTrigger(AuthorizationLevel.Function)] HttpRequestMessage req,
[DurableClient] IDurableEntityClient client)
{
var entityId = new EntityId(nameof(Counter), "myCounter");
EntityStateResponse<JObject> stateResponse = await client.ReadEntityStateAsync<JObject>(entityId);
return req.CreateResponse(HttpStatusCode.OK, stateResponse.EntityState);
}
```


```
const df = require("durable-functions");
module.exports = async function (context) {
const client = df.getClient(context);
const entityId = new df.EntityId("Counter", "myCounter");
const stateResponse = await client.readEntityState(entityId);
return stateResponse.entityState;
};
```


```
# An HTTP-Triggered Function with a Durable Functions Client to retrieve the state of a durable entity
@myApp.route(route="entityreadvalue")
@myApp.durable_client_input(client_name="client")
async def http_read(req: func.HttpRequest, client):
entityId = df.EntityId("Counter", "myCounter")
entity_state_result = await client.read_entity_state(entityId)
entity_state = "No state found"
if entity_state_result.entity_exists:
entity_state = str(entity_state_result.entity_state)
return func.HttpResponse(entity_state)
```


Entity state queries are sent to the Durable tracking store and return the entity's most recently persisted state. This state is always a "committed" state, that is, it's never a temporary intermediate state assumed in the middle of executing an operation. However, it's possible that this state is stale compared to the entity's in-memory state. Only orchestrations can read an entity's in-memory state, as described in the following section.

### Example: Orchestration signals and calls an entity

Orchestrator functions can access entities by using APIs on the [orchestration trigger binding](durable-functions-bindings#orchestration-trigger). The following example code shows an orchestrator function calling and signaling a `Counter`

entity.

```
[FunctionName("CounterOrchestration")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
var entityId = new EntityId(nameof(Counter), "myCounter");
// Two-way call to the entity which returns a value - awaits the response
int currentValue = await context.CallEntityAsync<int>(entityId, "Get");
if (currentValue < 10)
{
// One-way signal to the entity which updates the value - does not await a response
context.SignalEntity(entityId, "Add", 1);
}
}
```


```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context){
const entityId = new df.EntityId("Counter", "myCounter");
// Two-way call to the entity which returns a value - awaits the response
currentValue = yield context.df.callEntity(entityId, "get");
});
```


Note

JavaScript does not currently support signaling an entity from an orchestrator. Use `callEntity`

instead.

```
@myApp.orchestration_trigger(context_name="context")
def orchestrator(context: df.DurableOrchestrationContext):
entityId = df.EntityId("Counter", "myCounter")
context.signal_entity(entityId, "add", 3)
logging.info("signaled entity")
state = yield context.call_entity(entityId, "get")
return state
```


Only orchestrations are capable of calling entities and getting a response, which could be either a return value or an exception. Client functions that use the [client binding](durable-functions-bindings#entity-client) can only signal entities.

Note

Calling an entity from an orchestrator function is similar to calling an [activity function](durable-functions-types-features-overview#activity-functions) from an orchestrator function. The main difference is that entity functions are durable objects with an address, which is the entity ID. Entity functions support specifying an operation name. Activity functions, on the other hand, are stateless and don't have the concept of operations.

### Example: Entity signals an entity

An entity function can send signals to other entities, or even itself, while it executes an operation.
For example, we can modify the previous `Counter`

entity example so that it sends a "milestone-reached" signal to some monitor entity when the counter reaches the value 100.

```
case "add":
var currentValue = ctx.GetState<int>();
var amount = ctx.GetInput<int>();
if (currentValue < 100 && currentValue + amount >= 100)
{
ctx.SignalEntity(new EntityId("MonitorEntity", ""), "milestone-reached", ctx.EntityKey);
}
ctx.SetState(currentValue + amount);
break;
```


```
case "add":
const amount = context.df.getInput();
if (currentValue < 100 && currentValue + amount >= 100) {
const entityId = new df.EntityId("MonitorEntity", "");
context.df.signalEntity(entityId, "milestone-reached", context.df.instanceId);
}
context.df.setState(currentValue + amount);
break;
```


Note

Python doesn't support entity-to-entity signals yet. Please use an orchestrator for signaling entities instead.

## Entity coordination

There might be times when you need to coordinate operations across multiple entities. For example, in a banking application, you might have entities that represent individual bank accounts. When you transfer funds from one account to another, you must ensure that the source account has sufficient funds. You also must ensure that updates to both the source and destination accounts are done in a transactionally consistent way.

### Example: Transfer funds

The following example code transfers funds between two account entities by using an orchestrator function. Coordinating entity updates requires using the `LockAsync`

method to create a *critical section* in the orchestration.

Note

For simplicity, this example reuses the `Counter`

entity defined previously. In a real application, it would be better to define a more detailed `BankAccount`

entity.

```
// This is a method called by an orchestrator function
public static async Task<bool> TransferFundsAsync(
string sourceId,
string destinationId,
int transferAmount,
IDurableOrchestrationContext context)
{
var sourceEntity = new EntityId(nameof(Counter), sourceId);
var destinationEntity = new EntityId(nameof(Counter), destinationId);
// Create a critical section to avoid race conditions.
// No operations can be performed on either the source or
// destination accounts until the locks are released.
using (await context.LockAsync(sourceEntity, destinationEntity))
{
ICounter sourceProxy =
context.CreateEntityProxy<ICounter>(sourceEntity);
ICounter destinationProxy =
context.CreateEntityProxy<ICounter>(destinationEntity);
int sourceBalance = await sourceProxy.Get();
if (sourceBalance >= transferAmount)
{
await sourceProxy.Add(-transferAmount);
await destinationProxy.Add(transferAmount);
// the transfer succeeded
return true;
}
else
{
// the transfer failed due to insufficient funds
return false;
}
}
}
```


In .NET, `LockAsync`

returns `IDisposable`

, which ends the critical section when disposed. This `IDisposable`

result can be used together with a `using`

block to get a syntactic representation of the critical section.

In the preceding example, an orchestrator function transfers funds from a source entity to a destination entity. The `LockAsync`

method locked both the source and destination account entities. This locking ensured that no other client could query or modify the state of either account until the orchestration logic exited the critical section at the end of the `using`

statement. This behavior prevents the possibility of overdrafting from the source account.

Note

When an orchestration terminates, either normally or with an error, any critical sections in progress are implicitly ended and all locks are released.

### Critical section behavior

The `LockAsync`

method creates a critical section in an orchestration. These critical sections prevent other orchestrations from making overlapping changes to a specified set of entities. Internally, the `LockAsync`

API sends "lock" operations to the entities and returns when it receives a "lock acquired" response message from each of these same entities. Both lock and unlock are built-in operations supported by all entities.

No operations from other clients are allowed on an entity while it's in a locked state. This behavior ensures that only one orchestration instance can lock an entity at a time. If a caller tries to invoke an operation on an entity while it's locked by an orchestration, that operation is placed in a pending operation queue. No pending operations are processed until after the holding orchestration releases its lock.

Note

This behavior is slightly different from synchronization primitives used in most programming languages, such as the `lock`

statement in C#. For example, in C#, the `lock`

statement must be used by all threads to ensure proper synchronization across multiple threads. Entities, however, don't require all callers to explicitly lock an entity. If any caller locks an entity, all other operations on that entity are blocked and queued behind that lock.

Locks on entities are durable, so they persist even if the executing process is recycled. Locks are internally persisted as part of an entity's durable state.

Unlike transactions, critical sections don't automatically roll back changes when errors occur. Instead, any error handling, such as roll-back or retry, must be explicitly coded, for example by catching errors or exceptions. This design choice is intentional. Automatically rolling back all the effects of an orchestration is difficult or impossible in general, because orchestrations might run activities and make calls to external services that can't be rolled back. Also, attempts to roll back might themselves fail and require further error handling.

### Critical section rules

Unlike low-level locking primitives in most programming languages, critical sections are *guaranteed not to deadlock*. To prevent deadlocks, we enforce the following restrictions:

- Critical sections can't be nested.
- Critical sections can't create suborchestrations.
- Critical sections can call only entities they have locked.
- Critical sections can't call the same entity using multiple parallel calls.
- Critical sections can signal only entities they haven't locked.

Any violations of these rules cause a runtime error, such as `LockingRulesViolationException`

in .NET, which includes a message that explains what rule was broken.

## Comparison with virtual actors

Many of the durable entities features are inspired by the [actor model](https://en.wikipedia.org/wiki/Actor_model). If you're already familiar with actors, you might recognize many of the concepts described in this article. Durable entities are similar to [virtual actors](https://research.microsoft.com/projects/orleans/), or grains, as popularized by the [Orleans project](http://dotnet.github.io/orleans/). For example:

- Durable entities are addressable via an entity ID.
- Durable entity operations execute serially, one at a time, to prevent race conditions.
- Durable entities are created implicitly when they're called or signaled.
- Durable entities are silently unloaded from memory when not executing operations.

There are some important differences that are worth noting:

- Durable entities prioritize durability over latency, and so might not be appropriate for applications with strict latency requirements.
- Durable entities don't have built-in timeouts for messages. In Orleans, all messages time out after a configurable time. The default is 30 seconds.
- Messages sent between entities are delivered reliably and in order. In Orleans, reliable or ordered delivery is supported for content sent through streams, but isn't guaranteed for all messages between grains.
- Request-response patterns in entities are limited to orchestrations. From within entities, only one-way messaging (also known as signaling) is permitted, as in the original actor model, and unlike grains in Orleans.
- Durable entities don't deadlock. In Orleans, deadlocks can occur and don't resolve until messages time out.
- Durable entities can be used with durable orchestrations and support distributed locking mechanisms.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-cloud-backup -->

# Fan-out/fan-in scenario in Durable Functions - Cloud backup example

*Fan-out/fan-in* refers to the pattern of executing multiple functions concurrently and then performing some aggregation on the results. This article explains a sample that uses [Durable Functions](durable-functions-overview) to implement a fan-in/fan-out scenario. The sample is a durable function that backs up all or some of an app's site content into Azure Storage.

Note

Version 4 of the Node.js programming model for Azure Functions is generally available. The v4 model is designed to provide a more flexible and intuitive experience for JavaScript and TypeScript developers. For more information about the differences between v3 and v4, see the [migration guide](../functions-node-upgrade-v4).

In the following code snippets, JavaScript (PM4) denotes programming model v4, the new experience.

## Prerequisites

## Scenario overview

In this sample, the functions upload all files under a specified directory recursively into blob storage. They also count the total number of bytes that were uploaded.

It's possible to write a single function that takes care of everything. The main problem you would run into is **scalability**. A single function execution can only run on a single virtual machine, so the throughput will be limited by the throughput of that single VM. Another problem is **reliability**. If there's a failure midway through, or if the entire process takes more than 5 minutes, the backup could fail in a partially completed state. It would then need to be restarted.

A more robust approach would be to write two regular functions: one would enumerate the files and add the file names to a queue, and another would read from the queue and upload the files to blob storage. This approach is better in terms of throughput and reliability, but it requires you to provision and manage a queue. More importantly, significant complexity is introduced in terms of **state management** and **coordination** if you want to do anything more, like report the total number of bytes uploaded.

A Durable Functions approach gives you all of the mentioned benefits with very low overhead.

## The functions

This article explains the following functions in the sample app:

`E2_BackupSiteContent`

: An [orchestrator function](durable-functions-bindings#orchestration-trigger) that calls `E2_GetFileList`

to obtain a list of files to back up, then calls `E2_CopyFileToBlob`

to back up each file.
`E2_GetFileList`

: An [activity function](durable-functions-bindings#activity-trigger) that returns a list of files in a directory.
`E2_CopyFileToBlob`

: An activity function that backs up a single file to Azure Blob Storage.

### E2_BackupSiteContent orchestrator function

This orchestrator function essentially does the following:

- Takes a
`rootDirectory`

value as an input parameter.
- Calls a function to get a recursive list of files under
`rootDirectory`

.
- Makes multiple parallel function calls to upload each file into Azure Blob Storage.
- Waits for all uploads to complete.
- Returns the sum total bytes that were uploaded to Azure Blob Storage.

Here is the code that implements the orchestrator function:

```
[FunctionName("E2_BackupSiteContent")]
public static async Task<long> Run(
[OrchestrationTrigger] IDurableOrchestrationContext backupContext)
{
string rootDirectory = backupContext.GetInput<string>()?.Trim();
if (string.IsNullOrEmpty(rootDirectory))
{
rootDirectory = Directory.GetParent(typeof(BackupSiteContent).Assembly.Location).FullName;
}
string[] files = await backupContext.CallActivityAsync<string[]>(
"E2_GetFileList",
rootDirectory);
var tasks = new Task<long>[files.Length];
for (int i = 0; i < files.Length; i++)
{
tasks[i] = backupContext.CallActivityAsync<long>(
"E2_CopyFileToBlob",
files[i]);
}
await Task.WhenAll(tasks);
long totalBytes = tasks.Sum(t => t.Result);
return totalBytes;
}
```


Notice the `await Task.WhenAll(tasks);`

line. All the individual calls to the `E2_CopyFileToBlob`

function were *not* awaited, which allows them to run in parallel. When we pass this array of tasks to `Task.WhenAll`

, we get back a task that won't complete *until all the copy operations have completed*. If you're familiar with the Task Parallel Library (TPL) in .NET, then this is not new to you. The difference is that these tasks could be running on multiple virtual machines concurrently, and the Durable Functions extension ensures that the end-to-end execution is resilient to process recycling.

After awaiting from `Task.WhenAll`

, we know that all function calls have completed and have returned values back to us. Each call to `E2_CopyFileToBlob`

returns the number of bytes uploaded, so calculating the sum total byte count is a matter of adding all those return values together.

The function uses the standard *function.json* for orchestrator functions.

```
{
"bindings": [
{
"name": "context",
"type": "orchestrationTrigger",
"direction": "in"
}
],
"disabled": false
}
```


Here is the code that implements the orchestrator function:

```
const df = require("durable-functions");
module.exports = df.orchestrator(function* (context) {
const rootDirectory = context.df.getInput();
if (!rootDirectory) {
throw new Error("A directory path is required as an input.");
}
const files = yield context.df.callActivity("E2_GetFileList", rootDirectory);
// Backup Files and save Promises into array
const tasks = [];
for (const file of files) {
tasks.push(context.df.callActivity("E2_CopyFileToBlob", file));
}
// wait for all the Backup Files Activities to complete, sum total bytes
const results = yield context.df.Task.all(tasks);
const totalBytes = results.reduce((prev, curr) => prev + curr, 0);
// return results;
return totalBytes;
});
```


Notice the `yield context.df.Task.all(tasks);`

line. All the individual calls to the `E2_CopyFileToBlob`

function were *not* yielded, which allows them to run in parallel. When we pass this array of tasks to `context.df.Task.all`

, we get back a task that won't complete *until all the copy operations have completed*. If you're familiar with `Promise.all`

in JavaScript, then this is not new to you. The difference is that these tasks could be running on multiple virtual machines concurrently, and the Durable Functions extension ensures that the end-to-end execution is resilient to process recycling.

Note

Although tasks are conceptually similar to JavaScript promises, orchestrator functions should use `context.df.Task.all`

and `context.df.Task.any`

instead of `Promise.all`

and `Promise.race`

to manage task parallelization.

After yielding from `context.df.Task.all`

, we know that all function calls have completed and have returned values back to us. Each call to `E2_CopyFileToBlob`

returns the number of bytes uploaded, so calculating the sum total byte count is a matter of adding all those return values together.

Here is the code that implements the orchestrator function:

```
const df = require("durable-functions");
const path = require("path");
const getFileListActivityName = "getFileList";
const copyFileToBlobActivityName = "copyFileToBlob";
df.app.orchestration("backupSiteContent", function* (context) {
const rootDir = context.df.getInput();
if (!rootDir) {
throw new Error("A directory path is required as an input.");
}
const rootDirAbs = path.resolve(rootDir);
const files = yield context.df.callActivity(getFileListActivityName, rootDirAbs);
// Backup Files and save Tasks into array
const tasks = [];
for (const file of files) {
const input = {
backupPath: path.relative(rootDirAbs, file).replace(/\\/g, "/"),
filePath: file,
};
tasks.push(context.df.callActivity(copyFileToBlobActivityName, input));
}
// wait for all the Backup Files Activities to complete, sum total bytes
const results = yield context.df.Task.all(tasks);
const totalBytes = results ? results.reduce((prev, curr) => prev + curr, 0) : 0;
// return results;
return totalBytes;
});
```


Notice the `yield context.df.Task.all(tasks);`

line. All the individual calls to the `copyFileToBlob`

function were *not* yielded, which allows them to run in parallel. When we pass this array of tasks to `context.df.Task.all`

, we get back a task that won't complete *until all the copy operations have completed*. If you're familiar with `Promise.all`

in JavaScript, then this is not new to you. The difference is that these tasks could be running on multiple virtual machines concurrently, and the Durable Functions extension ensures that the end-to-end execution is resilient to process recycling.

Note

Although Tasks are conceptually similar to JavaScript promises, orchestrator functions should use `context.df.Task.all`

and `context.df.Task.any`

instead of `Promise.all`

and `Promise.race`

to manage task parallelization.

After yielding from `context.df.Task.all`

, we know that all function calls have completed and have returned values back to us. Each call to `copyFileToBlob`

returns the number of bytes uploaded, so calculating the sum total byte count is a matter of adding all those return values together.

The function uses the standard *function.json* for orchestrator functions.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"name": "context",
"type": "orchestrationTrigger",
"direction": "in"
}
]
}
```


Here is the code that implements the orchestrator function:

```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
root_directory: str = context.get_input()
if not root_directory:
raise Exception("A directory path is required as input")
files = yield context.call_activity("E2_GetFileList", root_directory)
tasks = []
for file in files:
tasks.append(context.call_activity("E2_CopyFileToBlob", file))
results = yield context.task_all(tasks)
total_bytes = sum(results)
return total_bytes
main = df.Orchestrator.create(orchestrator_function)
```


Notice the `yield context.task_all(tasks);`

line. All the individual calls to the `E2_CopyFileToBlob`

function were *not* yielded, which allows them to run in parallel. When we pass this array of tasks to `context.task_all`

, we get back a task that won't complete *until all the copy operations have completed*. If you're familiar with `asyncio.gather`

in Python, then this is not new to you. The difference is that these tasks could be running on multiple virtual machines concurrently, and the Durable Functions extension ensures that the end-to-end execution is resilient to process recycling.

Note

Although tasks are conceptually similar to Python awaitables, orchestrator functions should use `yield`

as well as the `context.task_all`

and `context.task_any`

APIs to manage task parallelization.

After yielding from `context.task_all`

, we know that all function calls have completed and have returned values back to us. Each call to `E2_CopyFileToBlob`

returns the number of bytes uploaded, so we can calculate the sum total byte count by adding all the return values together.

### Helper activity functions

The helper activity functions, as with other samples, are just regular functions that use the `activityTrigger`

trigger binding.

#### E2_GetFileList activity function

```
[FunctionName("E2_GetFileList")]
public static string[] GetFileList(
[ActivityTrigger] string rootDirectory,
ILogger log)
{
log.LogInformation($"Searching for files under '{rootDirectory}'...");
string[] files = Directory.GetFiles(rootDirectory, "*", SearchOption.AllDirectories);
log.LogInformation($"Found {files.Length} file(s) under {rootDirectory}.");
return files;
}
```


The *function.json* file for `E2_GetFileList`

looks like the following:

```
{
"bindings": [
{
"name": "rootDirectory",
"type": "activityTrigger",
"direction": "in"
}
],
"disabled": false
}
```


And here is the implementation:

```
const readdirp = require("readdirp");
module.exports = function (context, rootDirectory) {
context.log(`Searching for files under '${rootDirectory}'...`);
const allFilePaths = [];
readdirp(
{ root: rootDirectory, entryType: "all" },
function (fileInfo) {
if (!fileInfo.stat.isDirectory()) {
allFilePaths.push(fileInfo.fullPath);
}
},
function (err, res) {
if (err) {
throw err;
}
context.log(`Found ${allFilePaths.length} under ${rootDirectory}.`);
context.done(null, allFilePaths);
}
);
};
```


The function uses the `readdirp`

module (version 2.x) to recursively read the directory structure.

Here is the implementation of the `getFileList`

activity function:

```
const df = require("durable-functions");
const readdirp = require("readdirp");
const getFileListActivityName = "getFileList";
df.app.activity(getFileListActivityName, {
handler: async function (rootDirectory, context) {
context.log(`Searching for files under '${rootDirectory}'...`);
const allFilePaths = [];
for await (const entry of readdirp(rootDirectory, { type: "files" })) {
allFilePaths.push(entry.fullPath);
}
context.log(`Found ${allFilePaths.length} under ${rootDirectory}.`);
return allFilePaths;
},
});
```


The function uses the `readdirp`

module (version `3.x`

) to recursively read the directory structure.

The *function.json* file for `E2_GetFileList`

looks like the following:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"name": "rootDirectory",
"type": "activityTrigger",
"direction": "in"
}
]
}
```


And here is the implementation:

```
import os
from os.path import dirname
from typing import List
def main(rootDirectory: str) -> List[str]:
all_file_paths = []
# We walk the file system
for path, _, files in os.walk(rootDirectory):
# We copy the code for activities and orchestrators
if "E2_" in path:
# For each file, we add their full-path to the list
for name in files:
if name == "__init__.py" or name == "function.json":
file_path = os.path.join(path, name)
all_file_paths.append(file_path)
return all_file_paths
```


Note

You might be wondering why you couldn't just put this code directly into the orchestrator function. You could, but this would break one of the fundamental rules of orchestrator functions, which is that they should never do I/O, including local file system access. For more information, see [Orchestrator function code constraints](durable-functions-code-constraints).

#### E2_CopyFileToBlob activity function

```
[FunctionName("E2_CopyFileToBlob")]
public static async Task<long> CopyFileToBlob(
[ActivityTrigger] string filePath,
Binder binder,
ILogger log)
{
long byteCount = new FileInfo(filePath).Length;
// strip the drive letter prefix and convert to forward slashes
string blobPath = filePath
.Substring(Path.GetPathRoot(filePath).Length)
.Replace('\\', '/');
string outputLocation = $"backups/{blobPath}";
log.LogInformation($"Copying '{filePath}' to '{outputLocation}'. Total bytes = {byteCount}.");
// copy the file contents into a blob
using (Stream source = File.Open(filePath, FileMode.Open, FileAccess.Read, FileShare.Read))
using (Stream destination = await binder.BindAsync<CloudBlobStream>(
new BlobAttribute(outputLocation, FileAccess.Write)))
{
await source.CopyToAsync(destination);
}
return byteCount;
}
```


Note

You will need to install the `Microsoft.Azure.WebJobs.Extensions.Storage`

NuGet package to run the sample code.

The function uses some advanced features of Azure Functions bindings (that is, the use of the `Binder`

parameter), but you don't need to worry about those details for the purpose of this walkthrough.

The *function.json* file for `E2_CopyFileToBlob`

is similarly simple:

```
{
"bindings": [
{
"name": "filePath",
"type": "activityTrigger",
"direction": "in"
},
{
"name": "out",
"type": "blob",
"path": "",
"connection": "AzureWebJobsStorage",
"direction": "out"
}
],
"disabled": false
}
```


The JavaScript implementation uses the [Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) to upload the files to Azure Blob Storage.

```
const fs = require("fs");
const path = require("path");
const storage = require("azure-storage");
module.exports = function (context, filePath) {
const container = "backups";
const root = path.parse(filePath).root;
const blobPath = filePath.substring(root.length).replace("\\", "/");
const outputLocation = `backups/${blobPath}`;
const blobService = storage.createBlobService();
blobService.createContainerIfNotExists(container, (error) => {
if (error) {
throw error;
}
fs.stat(filePath, function (error, stats) {
if (error) {
throw error;
}
context.log(
`Copying '${filePath}' to '${outputLocation}'. Total bytes = ${stats.size}.`
);
const readStream = fs.createReadStream(filePath);
blobService.createBlockBlobFromStream(
container,
blobPath,
readStream,
stats.size,
function (error) {
if (error) {
throw error;
}
context.done(null, stats.size);
}
);
});
});
};
```


The JavaScript implementation of `copyFileToBlob`

uses an Azure Storage output binding to upload the files to Azure Blob storage.

```
const df = require("durable-functions");
const fs = require("fs/promises");
const { output } = require("@azure/functions");
const copyFileToBlobActivityName = "copyFileToBlob";
const blobOutput = output.storageBlob({
path: "backups/{backupPath}",
connection: "StorageConnString",
});
df.app.activity(copyFileToBlobActivityName, {
extraOutputs: [blobOutput],
handler: async function ({ backupPath, filePath }, context) {
const outputLocation = `backups/${backupPath}`;
const stats = await fs.stat(filePath);
context.log(`Copying '${filePath}' to '${outputLocation}'. Total bytes = ${stats.size}.`);
const fileContents = await fs.readFile(filePath);
context.extraOutputs.set(blobOutput, fileContents);
return stats.size;
},
});
```


The *function.json* file for `E2_CopyFileToBlob`

is similarly simple:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"name": "filePath",
"type": "activityTrigger",
"direction": "in"
}
]
}
```


The Python implementation uses the [Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python) to upload the files to Azure Blob Storage.

```
import os
import pathlib
from azure.storage.blob import BlobServiceClient
from azure.core.exceptions import ResourceExistsError
connect_str = os.getenv('AzureWebJobsStorage')
def main(filePath: str) -> str:
# Create the BlobServiceClient object which will be used to create a container client
blob_service_client = BlobServiceClient.from_connection_string(connect_str)
# Create a unique name for the container
container_name = "backups"
# Create the container if it does not exist
try:
blob_service_client.create_container(container_name)
except ResourceExistsError:
pass
# Create a blob client using the local file name as the name for the blob
parent_dir, fname = pathlib.Path(filePath).parts[-2:] # Get last two path components
blob_name = parent_dir + "_" + fname
blob_client = blob_service_client.get_blob_client(container=container_name, blob=blob_name)
# Count bytes in file
byte_count = os.path.getsize(filePath)
# Upload the created file
with open(filePath, "rb") as data:
blob_client.upload_blob(data)
return byte_count
```


The implementation loads the file from disk and asynchronously streams the contents into a blob of the same name in the "backups" container. The return value is the number of bytes copied to storage, that is then used by the orchestrator function to compute the aggregate sum.

Note

This is a perfect example of moving I/O operations into an `activityTrigger`

function. Not only can the work be distributed across many different machines, but you also get the benefits of checkpointing the progress. If the host process gets terminated for any reason, you know which uploads have already completed.

## Run the sample

You can start the orchestration, on Windows, by sending the following HTTP POST request.

```
POST http://{host}/orchestrators/E2_BackupSiteContent
Content-Type: application/json
Content-Length: 20
"D:\\home\\LogFiles"
```


Alternatively, on a Linux Function App (Python currently only runs on Linux for App Service), you can start the orchestration like so:

```
POST http://{host}/orchestrators/E2_BackupSiteContent
Content-Type: application/json
Content-Length: 20
"/home/site/wwwroot"
```


Note

The `HttpStart`

function that you are invoking only works with JSON-formatted content. For this reason, the `Content-Type: application/json`

header is required and the directory path is encoded as a JSON string. Moreover, HTTP snippet assumes there is an entry in the `host.json`

file which removes the default `api/`

prefix from all HTTP trigger functions URLs. You can find the markup for this configuration in the `host.json`

file in the samples.

This HTTP request triggers the `E2_BackupSiteContent`

orchestrator and passes the string `D:\home\LogFiles`

as a parameter. The response provides a link to get the status of the backup operation:

```
HTTP/1.1 202 Accepted
Content-Length: 719
Content-Type: application/json; charset=utf-8
Location: http://{host}/runtime/webhooks/durabletask/instances/b4e9bdcc435d460f8dc008115ff0a8a9?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
(...trimmed...)
```


Depending on how many log files you have in your function app, this operation could take several minutes to complete. You can get the latest status by querying the URL in the `Location`

header of the previous HTTP 202 response.

```
GET http://{host}/runtime/webhooks/durabletask/instances/b4e9bdcc435d460f8dc008115ff0a8a9?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
```


```
HTTP/1.1 202 Accepted
Content-Length: 148
Content-Type: application/json; charset=utf-8
Location: http://{host}/runtime/webhooks/durabletask/instances/b4e9bdcc435d460f8dc008115ff0a8a9?taskHub=DurableFunctionsHub&connection=Storage&code={systemKey}
{"runtimeStatus":"Running","input":"D:\\home\\LogFiles","output":null,"createdTime":"2019-06-29T18:50:55Z","lastUpdatedTime":"2019-06-29T18:51:16Z"}
```


In this case, the function is still running. You are able to see the input that was saved into the orchestrator state and the last updated time. You can continue to use the `Location`

header values to poll for completion. When the status is "Completed", you see an HTTP response value similar to the following:

```
HTTP/1.1 200 OK
Content-Length: 152
Content-Type: application/json; charset=utf-8
{"runtimeStatus":"Completed","input":"D:\\home\\LogFiles","output":452071,"createdTime":"2019-06-29T18:50:55Z","lastUpdatedTime":"2019-06-29T18:51:26Z"}
```


Now you can see that the orchestration is complete and approximately how much time it took to complete. You also see a value for the `output`

field, which indicates that around 450 KB of logs were uploaded.

## Next steps

This sample has shown how to implement the fan-out/fan-in pattern. The next sample shows how to implement the monitor pattern using [durable timers](durable-functions-timers).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-isolated-create-first-csharp -->

# Quickstart: Create a C# Durable Functions app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Durable Functions, a feature of [Azure Functions](../functions-overview), to write stateful functions in a serverless environment. Durable Functions manages state, checkpoints, and restarts in your application.

Like Azure Functions, Durable Functions supports two process models for .NET class library functions. To learn more about the two processes, see [Differences between in-process and isolated worker process .NET Azure Functions](../dotnet-isolated-in-process-differences).

In this quickstart, you use Visual Studio Code to locally create and test a "hello world" Durable Functions app. The function app orchestrates and chains together calls to other functions. Then, you publish the function code in Azure. The tools you use are available via the Visual Studio Code [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions).


## Prerequisites

To complete this quickstart, you need:

[Visual Studio Code](https://code.visualstudio.com/download)installed.The following Visual Studio Code extensions installed:

The latest version of

[Azure Functions Core Tools](../functions-run-local)installed.An Azure subscription. To use Durable Functions, you must have an Azure Storage account.

[.NET Core SDK](https://dotnet.microsoft.com/download)version 3.1 or later installed.An HTTP test tool that keeps your data secure. For more information, see

[HTTP test tools](../functions-develop-local#http-test-tools).

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create an Azure Functions project

In Visual Studio Code, create a local Azure Functions project.

On the

**View**menu, select**Command Palette**(or select Ctrl+Shift+P).At the prompt (

`>`

), enter and then select**Azure Functions: Create New Project**.Select

**Browse**. In the**Select Folder**dialog, go to a folder to use for your project, and then choose**Select**.At the prompts, select or enter the following values:

Prompt Action Description **Select a language for your function app project**Select **C#**.Creates a local C# Functions project. **Select a version**Select **Azure Functions v4**.You see this option only when Core Tools isn't already installed. Core Tools is installed the first time you run the app. **Select a .NET runtime**Select **.NET 8.0 isolated**.Creates a Functions project that supports .NET 8 running in an isolated worker process and the Azure Functions Runtime 4.0. For more information, see [How to target Azure Functions runtime version](../functions-versions).**Select a template for your project's first function**Select **Durable Functions Orchestration**.Creates a Durable Functions orchestration. **Choose a durable storage type**Select **Azure Storage**.The default storage provider for Durable Functions. For more information, see [Durable Functions storage providers](durable-functions-storage-providers).**Provide a function name**Enter **HelloOrchestration**.A name for the orchestration function. **Provide a namespace**Enter **Company.Function**.A namespace for the generated class. **Select how you would like to open your project**Select **Open in current window**.Opens Visual Studio Code in the folder you selected.

Visual Studio Code installs Azure Functions Core Tools if it's required to create the project. It also creates a function app project in a folder. This project contains the [host.json](../functions-host-json) and [local.settings.json](../functions-develop-local#local-settings-file) configuration files.

Another file, *HelloOrchestration.cs*, contains the basic building blocks of a Durable Functions app:

| Method | Description |
|---|---|
`HelloOrchestration` |
Defines the Durable Functions app orchestration. In this case, the orchestration starts, creates a list, and then adds the result of three functions calls to the list. When the three function calls finish, it returns the list. |
`SayHello` |
A simple function app that returns hello. This function contains the business logic that is orchestrated. |
`HelloOrchestration_HttpStart` |
An
check status response. |

For more information about these functions, see [Durable Functions types and features](durable-functions-types-features-overview) or this [C# sample code for Durable Functions](durable-functions-overview?pivots=csharp).

## Configure storage

You can use [Azurite](../../storage/common/storage-use-azurite?tabs=visual-studio-code), an emulator for Azure Storage, to test the function locally. In *local.settings.json*, set the value for `AzureWebJobsStorage`

to `UseDevelopmentStorage=true`

like in this example:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated"
}
}
```


To install and start running the Azurite extension in Visual Studio Code, in the command palette, enter **Azurite: Start** and select Enter.

You can use other storage options for your Durable Functions app. For more information about storage options and benefits, see [Durable Functions storage providers](durable-functions-storage-providers).

## Test the function locally

Azure Functions Core Tools gives you the capability to run an Azure Functions project on your local development computer. You're prompted to install these tools the first time you start a function in Visual Studio Code.

In Visual Studio Code, set a breakpoint in the

`SayHello`

activity function code, and then select F5 to start the function app project. The terminal panel displays output from Core Tools.Note

For more information about debugging, see

[Durable Functions diagnostics](durable-functions-diagnostics#debugging).If the message

*No job functions found*appears,[update your Azure Functions Core Tools installation to the latest version](../functions-core-tools-reference).In the terminal panel, copy the URL endpoint of your HTTP-triggered function.

Use an HTTP test tool to send an HTTP POST request to the URL endpoint.

The response is the HTTP function's initial result. It lets you know that the Durable Functions app orchestration started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs.

At this point, your breakpoint in the activity function should be hit because the orchestration has started. Step through it to get a response for the status of the orchestration.

Copy the URL value for

`statusQueryGetUri`

, paste it in your browser's address bar, and execute the request. Alternatively, you can also continue to use the HTTP test tool to issue the GET request.The request queries the orchestration instance for the status. You should see that the instance finished and that it includes the outputs or results of the Durable Functions app like in this example:

`{ "name":"HelloCities", "instanceId":"7f99f9474a6641438e5c7169b7ecb3f2", "runtimeStatus":"Completed", "input":null, "customStatus":null, "output":"Hello, Tokyo! Hello, London! Hello, Seattle!", "createdTime":"2023-01-31T18:48:49Z", "lastUpdatedTime":"2023-01-31T18:48:56Z" }`

Tip

Learn how you can observe the

[replay behavior](durable-functions-orchestrations#reliability)of a Durable Functions app through breakpoints.To stop debugging, in Visual Studio Code, select Shift+F5.


After you verify that the function runs correctly on your local computer, it's time to publish the project to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](../storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](../functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Test your function in Azure

In the Visual Studio Code output panel, copy the URL of the HTTP trigger. The URL that calls your HTTP-triggered function must be in the following format:

`https://<function-app-name>.azurewebsites.net/api/HelloOrchestration_HttpStart`

Paste the new URL for the HTTP request in your browser's address bar. You must get the same status response that you got when you tested locally when you use the published app.


The C# Durable Functions app that you created and published by using Visual Studio Code is ready to use.

## Clean up resources

If you no longer need the resources that you created to complete the quickstart, to avoid related costs in your Azure subscription, [delete the resource group](/en-us/azure/azure-resource-manager/management/delete-resource-group?tabs=azure-portal#delete-resource-group) and all related resources.

## Related content

- Learn about
[common Durable Functions app patterns](durable-functions-overview#application-patterns).

In this quickstart, you use Visual Studio 2022 to locally create and test a "hello world" Durable Functions app. The function orchestrates and chains together calls to other functions. Then, you publish the function code in Azure. The tools you use are available via the *Azure development workload* in Visual Studio 2022.


## Prerequisites

To complete this quickstart, you need:

[Visual Studio 2022](https://visualstudio.microsoft.com/vs/)installed.Make sure that the

**Azure development**workload is also installed. Visual Studio 2019 also supports Durable Functions development, but the UI and steps are different.The

[Azurite emulator](../../storage/common/storage-use-azurite)installed and running.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create a function app project

The Azure Functions template creates a project that you can publish to a function app in Azure. You can use a function app to group functions as a logical unit to more easily manage, deploy, scale, and share resources.

In Visual Studio, on the

**File**menu, select**New**>**Project**.On

**Create a new project**, search for**functions**, select the**Azure Functions**template, and then select**Next**.For

**Project name**, enter a name for your project, and then select**OK**. The project name must be valid as a C# namespace, so don't use underscores, hyphens, or nonalphanumeric characters.On

**Additional information**, use the settings that are described in the next table.Setting Action Description **Functions worker**Select **.NET 8 Isolated (Long Term Support)**.Creates an Azure Functions project that supports .NET 8 running in an isolated worker process and the Azure Functions Runtime 4.0. For more information, see [How to target the Azure Functions runtime version](../functions-versions).**Function**Enter **Durable Functions Orchestration**.Creates a Durable Functions orchestration. Note

If

**.NET 8 Isolated (Long Term Support)**doesn't appear in the**Functions worker**menu, you might not have the latest Azure Functions tool sets and templates. Go to**Tools**>**Options**>**Projects and Solutions**>**Azure Functions**>**Check for updates to download the latest**.To use the Azurite emulator, make sure that the

**Use Azurite for runtime storage account (AzureWebJobStorage)**checkbox is selected. To create a Functions project by using a Durable Functions orchestration template, select**Create**. The project has the basic configuration files that you need to run your functions.Note

You can choose other storage options for your Durable Functions app. For more information, see

[Durable Functions storage providers](durable-functions-storage-providers).

In your app folder, a file named *Function1.cs* contains three functions. The three functions are the basic building blocks of a Durable Functions app:

| Method | Description |
|---|---|
`RunOrchestrator` |
Defines the Durable Functions app orchestration. In this case, the orchestration starts, creates a list, and then adds the result of three functions calls to the list. When the three function calls finish, it returns the list. |
`SayHello` |
A simple function app that returns hello. This function contains the business logic that is orchestrated. |
`HttpStart` |
An
check status response. |

For more information about these functions, see [Durable Functions types and features](durable-functions-types-features-overview).

## Test the function locally

Azure Functions Core Tools gives you the capability to run an Azure Functions project on your local development computer. You're prompted to install these tools the first time you start a function in Visual Studio Code.

In Visual Studio Code, set a breakpoint in the

`SayHello`

activity function code, and then select F5. If you're prompted, accept the request from Visual Studio to download and install Azure Functions Core (command-line) tools. You might also need to enable a firewall exception so that the tools can handle HTTP requests.Note

For more information about debugging, see

[Durable Functions diagnostics](durable-functions-diagnostics#debugging).Copy the URL of your function from the Azure Functions runtime output.

Paste the URL for the HTTP request in your browser's address bar and execute the request. The following screenshot shows the response to the local GET request that the function returns in the browser:

The response is the HTTP function's initial result. It lets you know that the durable orchestration started successfully. It doesn't yet display the end result of the orchestration. The response includes a few useful URLs.

At this point, your breakpoint in the activity function should be hit because the orchestration started. Step through it to get a response for the status of the orchestration.

Copy the URL value for

`statusQueryGetUri`

, paste it in your browser's address bar, and execute the request.The request queries the orchestration instance for the status. You should see that the instance finished and that it includes the outputs or results of the durable function, like in this example:

`{ "name":"HelloCities", "instanceId":"668814ac6ce84a43a9e6757f81dbc0bc", "runtimeStatus":"Completed", "input":null, "customStatus":null, "output":"Hello, Tokyo! Hello, London! Hello Seattle!", "createdTime":"2023-01-31T16:44:34Z", "lastUpdatedTime":"2023-01-31T16:44:37Z" }`

Tip

Learn how you can observe the

[replay behavior](durable-functions-orchestrations#reliability)of a Durable Functions app through breakpoints.To stop debugging, select Shift+F5.


After you verify that the function runs correctly on your local computer, it's time to publish the project to Azure.

## Publish the project to Azure

You must have a function app in your Azure subscription before you publish your project. You can create a function app in Visual Studio.

In

**Solution Explorer**, right-click the project and then select**Publish**.On the

**Publish**page, make the following selections:- On
**Target**, select**Azure**, and then select**Next**. - On
**Specific target**, select**Azure Function App**, and then select**Next**. - On
**Functions instance**, select**Create new**.

- On
Create a new instance by using the values specified in the following table:

Setting Value Description **Name**A globally unique name The name must uniquely identify your new function app. Accept the suggested name or enter a new name. The following characters are valid: `a-z`

,`0-9`

, and`-`

.**Subscription name**The name of your subscription The function app is created in an Azure subscription. Accept the default subscription or select a different one from the list. [Resource group](../../azure-resource-manager/management/overview)The name of your resource group The function app is created in a resource group. Select **New**to create a new resource group. You can also select an existing resource group from the list.[Plan Type](../functions-scale)**Flex Consumption**When you publish your project to a function app that runs in a [Flex Consumption plan](../flex-consumption-plan), you might pay only for executions of your functions app. Other hosting plans can incur higher costs.**IMPORTANT:**

When creating a Flex Consumption plan, you must first select**App service plan**and then reselect**Flex Consumption**to clear an issue with the dialog.**Operating system****Linux**The Flex Consumption plan currently requires Linux. **Location**The location of the app service Select a location in an [Azure region supported by the Flex Consumption plan](../flex-consumption-how-to#view-currently-supported-regions). When an unsupported region is selected, the**Create**button is grayed-out.**Instance memory size****2048**The [memory size of the virtual machine instances](../flex-consumption-plan#instance-sizes)in which the app runs is unique to the Flex Consumption plan.[Azure Storage](../storage-considerations)A general-purpose storage account The Functions runtime requires a Storage account. Select **New**to configure a general-purpose storage account. You can also use an existing account that meets the[storage account requirements](../storage-considerations#storage-account-requirements).[Application Insights](../functions-monitoring)An Application Insights instance You should turn on Application Insights integration for your function app. Select **New**to create a new instance, either in a new or in an existing Log Analytics workspace. You can also use an existing instance.Select

**Create**to create a function app and its related resources in Azure. The status of resource creation is shown in the lower-left corner of the window.Select

**Finish**. The**Publish profile creation progress**window appears. When the profile is created, select**Close**.On the publish profile page, select

**Publish**to deploy the package that contains your project files to your new function app in Azure.When deployment is complete, the root URL of the function app in Azure is shown on the publish profile page.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The new function app Azure resource opens in the Azure portal.

## Test your function in Azure

On the

**Publish profile**page, copy the base URL of the function app. Replace the`localhost:port`

portion of the URL that you used when you tested the function locally with the new base URL.The URL that calls your durable function HTTP trigger must be in the following format:

`https://<APP_NAME>.azurewebsites.net/api/<FUNCTION_NAME>_HttpStart`

Paste the new URL for the HTTP request in your browser's address bar. When you test the published app, you must get the same status response that you got when you tested locally.


The C# Durable Functions app that you created and published by using Visual Studio is ready to use.

## Clean up resources

If you no longer need the resources that you created to complete the quickstart, to avoid related costs in your Azure subscription, [delete the resource group](/en-us/azure/azure-resource-manager/management/delete-resource-group?tabs=azure-portal#delete-resource-group) and all related resources.

## Related content

- Learn about
[common Durable Functions app patterns](durable-functions-overview#application-patterns).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-error-handling -->

# Handling errors in Durable Functions (Azure Functions)

Durable Function orchestrations are implemented in code and can use the programming language's built-in error-handling features. There really aren't any new concepts you need to learn to add error handling and compensation into your orchestrations. However, there are a few behaviors that you should be aware of.

Note

Version 4 of the Node.js programming model for Azure Functions is generally available. The v4 model is designed to provide a more flexible and intuitive experience for JavaScript and TypeScript developers. For more information about the differences between v3 and v4, see the [migration guide](../functions-node-upgrade-v4).

In the following code snippets, JavaScript (PM4) denotes programming model v4, the new experience.

## Errors in activity functions and sub-orchestrations

In Durable Functions, unhandled exceptions thrown within activity functions or sub-orchestrations are marshaled back to the orchestrator function using standardized exception types.

For example, consider the following orchestrator function that performs a fund transfer between two accounts:

In Durable Functions C# in-process, unhandled exceptions are thrown as [FunctionFailedException](/en-us/dotnet/api/microsoft.azure.webjobs.extensions.durabletask.functionfailedexception).

The exception message typically identifies which activity functions or sub-orchestrations caused the failure. To access more detailed error information, inspect the `InnerException`

property.

```
[FunctionName("TransferFunds")]
public static async Task Run([OrchestrationTrigger] IDurableOrchestrationContext context)
{
var transferDetails = context.GetInput<TransferOperation>();
await context.CallActivityAsync("DebitAccount",
new
{
Account = transferDetails.SourceAccount,
Amount = transferDetails.Amount
});
try
{
await context.CallActivityAsync("CreditAccount",
new
{
Account = transferDetails.DestinationAccount,
Amount = transferDetails.Amount
});
}
catch (FunctionFailedException)
{
// Refund the source account.
// Another try/catch could be used here based on the needs of the application.
await context.CallActivityAsync("CreditAccount",
new
{
Account = transferDetails.SourceAccount,
Amount = transferDetails.Amount
});
}
}
```


Note

The previous C# examples are for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

In Durable Functions C# Isolated, unhandled exceptions are surfaced as [TaskFailedException](/en-us/dotnet/api/microsoft.durabletask.taskfailedexception).

The exception message typically identifies which activity functions or sub-orchestrations caused the failure. To access more detailed error information, inspect the [FailureDetails](/en-us/dotnet/api/microsoft.durabletask.taskfailuredetails) property.

```
[FunctionName("TransferFunds")]
public static async Task Run(
[OrchestrationTrigger] TaskOrchestrationContext context, TransferOperation transferDetails)
{
await context.CallActivityAsync("DebitAccount",
new
{
Account = transferDetails.SourceAccount,
Amount = transferDetails.Amount
});
try
{
await context.CallActivityAsync("CreditAccount",
new
{
Account = transferDetails.DestinationAccount,
Amount = transferDetails.Amount
});
}
catch (TaskFailedException)
{
// Refund the source account.
// Another try/catch could be used here based on the needs of the application.
await context.CallActivityAsync("CreditAccount",
new
{
Account = transferDetails.SourceAccount,
Amount = transferDetails.Amount
});
}
}
```


Note

- The exception message typically identifies which activity functions or sub-orchestrations caused the failure. To access more detailed error information, inspect the
`FailureDetails`

property.
- By default,
`FailureDetails`

includes the **error type**, **error message**, **stack trace**, and any **nested inner exceptions** (each represented as a recursive `FailureDetails`

object). If you want to include additional exception properties in the failure output, see [Include Custom Exception Properties for FailureDetails (.NET Isolated)](#include-custom-exception-properties-for-failuredetails-net-isolated).

```
const df = require("durable-functions");
module.exports = df.orchestrator(function* (context) {
const transferDetails = context.df.getInput();
yield context.df.callActivity("DebitAccount", {
account: transferDetails.sourceAccount,
amount: transferDetails.amount,
});
try {
yield context.df.callActivity("CreditAccount", {
account: transferDetails.destinationAccount,
amount: transferDetails.amount,
});
} catch (error) {
// Refund the source account.
// Another try/catch could be used here based on the needs of the application.
yield context.df.callActivity("CreditAccount", {
account: transferDetails.sourceAccount,
amount: transferDetails.amount,
});
}
})
```


```
const df = require("durable-functions");
df.app.orchestration("transferFunds", function* (context) {
const transferDetails = context.df.getInput();
yield context.df.callActivity("debitAccount", {
account: transferDetails.sourceAccount,
amount: transferDetails.amount,
});
try {
yield context.df.callActivity("creditAccount", {
account: transferDetails.destinationAccount,
amount: transferDetails.amount,
});
} catch (error) {
// Refund the source account.
// Another try/catch could be used here based on the needs of the application.
yield context.df.callActivity("creditAccount", {
account: transferDetails.sourceAccount,
amount: transferDetails.amount,
});
}
});
```


```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
transfer_details = context.get_input()
yield context.call_activity('DebitAccount', {
'account': transfer_details['sourceAccount'],
'amount' : transfer_details['amount']
})
try:
yield context.call_activity('CreditAccount', {
'account': transfer_details['destinationAccount'],
'amount': transfer_details['amount'],
})
except:
yield context.call_activity('CreditAccount', {
'account': transfer_details['sourceAccount'],
'amount': transfer_details['amount']
})
main = df.Orchestrator.create(orchestrator_function)
```


By default, cmdlets in PowerShell don't raise exceptions that can be caught using try/catch blocks. You have two options for changing this behavior:

- Use the
`-ErrorAction Stop`

flag when invoking cmdlets, such as `Invoke-DurableActivity`

.
- Set the
`$ErrorActionPreference`

preference variable to `"Stop"`

in the orchestrator function before invoking cmdlets.

```
param($Context)
$ErrorActionPreference = "Stop"
$transferDetails = $Context.Input
Invoke-DurableActivity -FunctionName 'DebitAccount' -Input @{ account = transferDetails.sourceAccount; amount = transferDetails.amount }
try {
Invoke-DurableActivity -FunctionName 'CreditAccount' -Input @{ account = transferDetails.destinationAccount; amount = transferDetails.amount }
} catch {
Invoke-DurableActivity -FunctionName 'CreditAccount' -Input @{ account = transferDetails.sourceAccount; amount = transferDetails.amount }
}
```


For more information on error handling in PowerShell, see the [Try-Catch-Finally](/en-us/powershell/module/microsoft.powershell.core/about/about_try_catch_finally) PowerShell documentation.

```
@FunctionName("TransferFunds")
public void transferFunds(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
TransferOperation transfer = ctx.getInput(TransferOperation.class);
ctx.callActivity(
"DebitAccount",
new OperationArgs(transfer.sourceAccount, transfer.amount)).await();
try {
ctx.callActivity(
"CreditAccount",
new OperationArgs(transfer.destinationAccount, transfer.amount)).await();
} catch (TaskFailedException ex) {
// Refund the source account on failure
ctx.callActivity(
"CreditAccount",
new OperationArgs(transfer.sourceAccount, transfer.amount)).await();
}
}
```


If the first **CreditAccount** function call fails, the orchestrator function compensates by crediting the funds back to the source account.

## Errors in entity functions

Exception handling behavior for entity functions differs based on the Durable Functions hosting model:

In Durable Functions using C# in-process, original exception types thrown by entity functions are directly returned to the orchestrator.

```
[FunctionName("Function1")]
public static async Task<string> RunOrchestrator(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
try
{
var entityId = new EntityId(nameof(Counter), "myCounter");
await context.CallEntityAsync(entityId, "Add", 1);
}
catch (Exception ex)
{
// The exception type will be InvalidOperationException with the message "this is an entity exception".
}
return string.Empty;
}
[FunctionName("Counter")]
public static void Counter([EntityTrigger] IDurableEntityContext ctx)
{
switch (ctx.OperationName.ToLowerInvariant())
{
case "add":
throw new InvalidOperationException("this is an entity exception");
case "get":
ctx.Return(ctx.GetState<int>());
break;
}
}
```


In Durable Functions C# Isolated, exceptions are surfaced to the orchestrator as an `EntityOperationFailedException`

. To access the original exception details, inspect its `FailureDetails`

property.

```
[Function(nameof(MyOrchestrator))]
public static async Task<List<string>> MyOrchestrator(
[Microsoft.Azure.Functions.Worker.OrchestrationTrigger] TaskOrchestrationContext context)
{
var entityId = new Microsoft.DurableTask.Entities.EntityInstanceId(nameof(Counter), "myCounter");
try
{
await context.Entities.CallEntityAsync(entityId, "Add", 1);
}
catch (EntityOperationFailedException ex)
{
// Add your error handling
}
return new List<string>();
}
```


```
df.app.orchestration("counterOrchestration", function* (context) {
const entityId = new df.EntityId(counterEntityName, "myCounter");
try {
const currentValue = yield context.df.callEntity(entityId, "get");
if (currentValue < 10) {
yield context.df.callEntity(entityId, "add", 1);
}
} catch (err) {
context.log(`Entity call failed: ${err.message ?? err}`);
}
});
```


```
df.app.orchestration("counterOrchestration", function* (context) {
const entityId = new df.EntityId(counterEntityName, "myCounter");
try {
const currentValue = yield context.df.callEntity(entityId, "get");
if (currentValue < 10) {
yield context.df.callEntity(entityId, "add", 1);
}
} catch (err) {
context.log(`Entity call failed: ${err.message ?? err}`);
}
});
```


```
@myApp.orchestration_trigger(context_name="context")
def run_orchestrator(context):
try:
entityId = df.EntityId("Counter", "myCounter")
yield context.call_entity(entityId, "get")
return "finished"
except Exception as e:
# Add your error handling
```


Entity functions aren't currently not supported in PowerShell.

Entity functions aren't currently not supported in Java.

## Automatic retry on failure

When you call activity functions or sub-orchestration functions, you can specify an automatic retry policy. The following example attempts to call a function up to three times and waits 5 seconds between each retry:

```
[FunctionName("TimerOrchestratorWithRetry")]
public static async Task Run([OrchestrationTrigger] IDurableOrchestrationContext context)
{
var retryOptions = new RetryOptions(
firstRetryInterval: TimeSpan.FromSeconds(5),
maxNumberOfAttempts: 3);
await context.CallActivityWithRetryAsync("FlakyFunction", retryOptions, null);
// ...
}
```


Note

The previous C# examples are for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

```
[FunctionName("TimerOrchestratorWithRetry")]
public static async Task Run([OrchestrationTrigger] TaskOrchestrationContext context)
{
var options = TaskOptions.FromRetryPolicy(new RetryPolicy(
maxNumberOfAttempts: 3,
firstRetryInterval: TimeSpan.FromSeconds(5)));
await context.CallActivityAsync("FlakyFunction", options: options);
// ...
}
```


```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context) {
const firstRetryIntervalInMilliseconds = 5000;
const maxNumberOfAttempts = 3;
const retryOptions =
new df.RetryOptions(firstRetryIntervalInMilliseconds, maxNumberOfAttempts);
yield context.df.callActivityWithRetry("FlakyFunction", retryOptions);
// ...
});
```


```
const df = require("durable-functions");
df.app.orchestration("callActivityWithRetry", function* (context) {
const firstRetryIntervalInMilliseconds = 5000;
const maxNumberOfAttempts = 3;
const retryOptions = new df.RetryOptions(firstRetryIntervalInMilliseconds, maxNumberOfAttempts);
yield context.df.callActivityWithRetry("flakyFunction", retryOptions);
// ...
});
```


```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
first_retry_interval_in_milliseconds = 5000
max_number_of_attempts = 3
retry_options = df.RetryOptions(first_retry_interval_in_milliseconds, max_number_of_attempts)
yield context.call_activity_with_retry('FlakyFunction', retry_options)
main = df.Orchestrator.create(orchestrator_function)
```


```
param($Context)
$retryOptions = New-DurableRetryOptions `
-FirstRetryInterval (New-TimeSpan -Seconds 5) `
-MaxNumberOfAttempts 3
Invoke-DurableActivity -FunctionName 'FlakyFunction' -RetryOptions $retryOptions
```


```
@FunctionName("TimerOrchestratorWithRetry")
public void timerOrchestratorWithRetry(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
final int maxAttempts = 3;
final Duration firstRetryInterval = Duration.ofSeconds(5);
RetryPolicy policy = new RetryPolicy(maxAttempts, firstRetryInterval);
TaskOptions options = new TaskOptions(policy);
ctx.callActivity("FlakeyFunction", options).await();
// ...
}
```


The activity function call in the previous example takes a parameter for configuring an automatic retry policy. There are several options for customizing the automatic retry policy:

**Max number of attempts**: The maximum number of attempts. If set to 1, there will be no retry.
**First retry interval**: The amount of time to wait before the first retry attempt.
**Backoff coefficient**: The coefficient used to determine rate of increase of backoff. Defaults to 1.
**Max retry interval**: The maximum amount of time to wait in between retry attempts.
**Retry timeout**: The maximum amount of time to spend doing retries. The default behavior is to retry indefinitely.

## Custom retry handlers

When using the .NET or Java, you also have the option to implement retry handlers in code. This is useful when declarative retry policies aren't expressive enough. For languages that don't support custom retry handlers, you still have the option of implementing retry policies using loops, exception handling, and timers for injecting delays between retries.

```
RetryOptions retryOptions = new RetryOptions(
firstRetryInterval: TimeSpan.FromSeconds(5),
maxNumberOfAttempts: int.MaxValue)
{
Handle = exception =>
{
// True to handle and try again, false to not handle and throw.
if (exception is TaskFailedException failure)
{
// Exceptions from TaskActivities are always this type. Inspect the
// inner Exception to get more details.
}
return false;
};
}
await ctx.CallActivityWithRetryAsync("FlakeyActivity", retryOptions, null);
```


```
TaskOptions retryOptions = TaskOptions.FromRetryHandler(retryContext =>
{
// Don't retry anything that derives from ApplicationException
if (retryContext.LastFailure.IsCausedBy<ApplicationException>())
{
return false;
}
// Quit after N attempts
return retryContext.LastAttemptNumber < 3;
});
try
{
await ctx.CallActivityAsync("FlakeyActivity", options: retryOptions);
}
catch (TaskFailedException)
{
// Case when the retry handler returns false...
}
```


JavaScript doesn't currently support custom retry handlers. However, you still have the option of implementing retry logic directly in the orchestrator function using loops, exception handling, and timers for injecting delays between retries.

JavaScript doesn't currently support custom retry handlers. However, you still have the option of implementing retry logic directly in the orchestrator function using loops, exception handling, and timers for injecting delays between retries.

Python doesn't currently support custom retry handlers. However, you still have the option of implementing retry logic directly in the orchestrator function using loops, exception handling, and timers for injecting delays between retries.

PowerShell doesn't currently support custom retry handlers. However, you still have the option of implementing retry logic directly in the orchestrator function using loops, exception handling, and timers for injecting delays between retries.

```
RetryHandler retryHandler = retryCtx -> {
// Don't retry anything that derives from RuntimeException
if (retryCtx.getLastFailure().isCausedBy(RuntimeException.class)) {
return false;
}
// Quit after N attempts
return retryCtx.getLastAttemptNumber() < 3;
};
TaskOptions options = new TaskOptions(retryHandler);
try {
ctx.callActivity("FlakeyActivity", options).await();
} catch (TaskFailedException ex) {
// Case when the retry handler returns false...
}
```


## Function timeouts

You might want to abandon a function call within an orchestrator function if it's taking too long to complete. The proper way to do this today is by creating a [durable timer](durable-functions-timers) with an "any" task selector, as in the following example:

```
[FunctionName("TimerOrchestrator")]
public static async Task<bool> Run([OrchestrationTrigger] IDurableOrchestrationContext context)
{
TimeSpan timeout = TimeSpan.FromSeconds(30);
DateTime deadline = context.CurrentUtcDateTime.Add(timeout);
using (var cts = new CancellationTokenSource())
{
Task activityTask = context.CallActivityAsync("FlakyFunction");
Task timeoutTask = context.CreateTimer(deadline, cts.Token);
Task winner = await Task.WhenAny(activityTask, timeoutTask);
if (winner == activityTask)
{
// success case
cts.Cancel();
return true;
}
else
{
// timeout case
return false;
}
}
}
```


Note

The previous C# examples are for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

```
[Function("TimerOrchestrator")]
public static async Task<bool> Run([OrchestrationTrigger] TaskOrchestrationContext context)
{
TimeSpan timeout = TimeSpan.FromSeconds(30);
DateTime deadline = context.CurrentUtcDateTime.Add(timeout);
using (var cts = new CancellationTokenSource())
{
Task activityTask = context.CallActivityAsync("FlakyFunction");
Task timeoutTask = context.CreateTimer(deadline, cts.Token);
Task winner = await Task.WhenAny(activityTask, timeoutTask);
if (winner == activityTask)
{
// success case
cts.Cancel();
return true;
}
else
{
// timeout case
return false;
}
}
}
```


```
const df = require("durable-functions");
const moment = require("moment");
module.exports = df.orchestrator(function*(context) {
const deadline = moment.utc(context.df.currentUtcDateTime).add(30, "s");
const activityTask = context.df.callActivity("FlakyFunction");
const timeoutTask = context.df.createTimer(deadline.toDate());
const winner = yield context.df.Task.any([activityTask, timeoutTask]);
if (winner === activityTask) {
// success case
timeoutTask.cancel();
return true;
} else {
// timeout case
return false;
}
});
```


```
const df = require("durable-functions");
const { DateTime } = require("luxon");
df.app.orchestration("timerOrchestrator", function* (context) {
const deadline = DateTime.fromJSDate(context.df.currentUtcDateTime).plus({ seconds: 30 });
const activityTask = context.df.callActivity("flakyFunction");
const timeoutTask = context.df.createTimer(deadline.toJSDate());
const winner = yield context.df.Task.any([activityTask, timeoutTask]);
if (winner === activityTask) {
// success case
timeoutTask.cancel();
return true;
} else {
// timeout case
return false;
}
});
```


```
import azure.functions as func
import azure.durable_functions as df
from datetime import datetime, timedelta
def orchestrator_function(context: df.DurableOrchestrationContext):
deadline = context.current_utc_datetime + timedelta(seconds = 30)
activity_task = context.call_activity('FlakyFunction')
timeout_task = context.create_timer(deadline)
winner = yield context.task_any(activity_task, timeout_task)
if winner == activity_task:
timeout_task.cancel()
return True
else:
return False
main = df.Orchestrator.create(orchestrator_function)
```


```
param($Context)
$expiryTime = New-TimeSpan -Seconds 30
$activityTask = Invoke-DurableActivity -FunctionName 'FlakyFunction'-NoWait
$timerTask = Start-DurableTimer -Duration $expiryTime -NoWait
$winner = Wait-DurableTask -Task @($activityTask, $timerTask) -NoWait
if ($winner -eq $activityTask) {
Stop-DurableTimerTask -Task $timerTask
return $True
}
else {
return $False
}
```


```
@FunctionName("TimerOrchestrator")
public boolean timerOrchestrator(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
Task<Void> activityTask = ctx.callActivity("SlowFunction");
Task<Void> timeoutTask = ctx.createTimer(Duration.ofMinutes(30));
Task<?> winner = ctx.anyOf(activityTask, timeoutTask).await();
if (winner == activityTask) {
// success case
return true;
} else {
// timeout case
return false;
}
}
```


Note

This mechanism doesn't actually terminate in-progress activity function execution. Rather, it simply allows the orchestrator function to ignore the result and move on. For more information, see the [Timers](durable-functions-timers#usage-for-timeout) documentation.

## Unhandled exceptions

If an orchestrator function fails with an unhandled exception, the details of the exception are logged and the instance completes with a `Failed`

status.

## Include Custom Exception Properties for FailureDetails (.NET Isolated)

When running Durable Task workflows in the .NET Isolated model, task failures are automatically serialized into a FailureDetails object. By default, this object includes standard fields such as:

- ErrorType — the exception type name
- Message — the exception message
- StackTrace — the serialized stack trace
- InnerFailure – a nested FailureDetails object for recursive inner exceptions

Starting with Microsoft.Azure.Functions.Worker.Extensions.DurableTask [v1.9.0](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.DurableTask/1.9.0), You can extend this behavior by implementing an IExceptionPropertiesProvider (defined in the Microsoft.DurableTask.Worker starting from [v1.16.1](https://www.nuget.org/packages/Microsoft.DurableTask.Worker/1.16.1)package). This provider defines which exception types and which of their properties should be included in the FailureDetails.Properties dictionary.

Note

- This feature is available in
**.NET Isolated** only. Support for Java will be added in a future release.
- Make sure you're using
**Microsoft.Azure.Functions.Worker.Extensions.DurableTask v1.9.0** or later.
- Make sure you're using
**Microsoft.DurableTask.Worker v1.16.1** or later.

### Implement an Exception Properties Provider

Implement a custom IExceptionPropertiesProvider to extract and return selected properties for the exceptions you care about. The returned dictionary will be serialized into the Properties field of FailureDetails when a matching exception type is thrown.

```
using Microsoft.DurableTask.Worker;
public class CustomExceptionPropertiesProvider : IExceptionPropertiesProvider
{
public IDictionary<string, object?>? GetExceptionProperties(Exception exception)
{
return exception switch
{
ArgumentOutOfRangeException e => new Dictionary<string, object?>
{
["ParamName"] = e.ParamName,
["ActualValue"] = e.ActualValue
},
InvalidOperationException e => new Dictionary<string, object?>
{
["CustomHint"] = "Invalid operation occurred",
["TimestampUtc"] = DateTime.UtcNow
},
_ => null // Other exception types not handled
};
}
}
```


### Register the Provider

Register your custom IExceptionPropertiesProvider in your .NET Isolated worker host, typically in Program.cs:

```
using Microsoft.DurableTask.Worker;
using Microsoft.Extensions.DependencyInjection;
var host = new HostBuilder()
.ConfigureFunctionsWorkerDefaults(builder =>
{
// Register custom exception properties provider
builder.Services.AddSingleton<IExceptionPropertiesProvider, CustomExceptionPropertiesProvider>();
})
.Build();
host.Run();
```


Once registered, any exception that matches one of the handled types will automatically include the configured properties in its FailureDetails.

### Sample FailureDetails Output

When an exception occurs that matches your provider’s configuration, the orchestration receives a serialized FailureDetails structure like this:

```
{
"errorType": "TaskFailedException",
"message": "Activity failed with an exception.",
"stackTrace": "...",
"innerFailure": {
"errorType": "ArgumentOutOfRangeException",
"message": "Specified argument was out of range.",
"properties": {
"ParamName": "count",
"ActualValue": 42
}
}
}
```


## Next steps

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-azure-storage-provider -->

# Azure Storage provider (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This document describes the characteristics of the Durable Functions Azure Storage provider, with a focus on performance and scalability aspects. The Azure Storage provider is the default provider. It stores instance states and queues in an Azure Storage (classic) account.

Note

For more information on the supported storage providers for Durable Functions and how they compare, see the [Durable Functions storage providers](durable-functions-storage-providers) documentation.

In the Azure Storage provider, all function execution is driven by Azure Storage queues. Orchestration and entity status and history are stored in Azure Tables. Azure Blobs and blob leases are used to distribute orchestration instances and entities across multiple app instances (also known as *workers* or simply *VMs*). This section goes into more detail on the various Azure Storage artifacts and how they affect performance and scalability.

## Storage representation

A [task hub](durable-functions-task-hubs) durably persists all instance states and all messages. For a quick overview of how these are used to track the progress of an orchestration, see the [task hub execution example](durable-functions-task-hubs#execution-example).

The Azure Storage provider represents the task hub in storage using the following components:

- Between two and three Azure Tables. Two tables are used to represent histories and instance states. If the Table Partition Manager is enabled, then a third table is introduced to store partition information.
- One Azure Queue stores the activity messages.
- One or more Azure Queues store the instance messages. Each of these so-called
*control queues*represents a[partition](durable-functions-perf-and-scale#partition-count)that is assigned a subset of all instance messages, based on the hash of the instance ID. - A few extra blob containers used for lease blobs and/or large messages.

For example, a task hub named `xyz`

with `PartitionCount = 4`

contains the following queues and tables:

Next, we describe these components and the role they play in more detail.

### History table

The **History** table is an Azure Storage table that contains the history events for all orchestration instances within a task hub. The name of this table is in the form *TaskHubName*History. As instances run, new rows are added to this table. The partition key of this table is derived from the instance ID of the orchestration. Instance IDs are random by default, ensuring optimal distribution of internal partitions in Azure Storage. The row key for this table is a sequence number used for ordering the history events.

When an orchestration instance needs to run, the corresponding rows of the History table are loaded into memory using a range query within a single table partition. These *history events* are then replayed into the orchestrator function code to get it back into its previously checkpointed state. The use of execution history to rebuild state in this way is influenced by the [Event Sourcing pattern](/en-us/azure/architecture/patterns/event-sourcing).

Tip

Orchestration data stored in the History table includes output payloads from activity and suborchestrator functions. Payloads from external events are also stored in the History table. Because the full history is loaded into memory every time an orchestrator needs to execute, a large enough history can result in significant memory pressure on a given virtual machine. The length and size of the orchestration history can be reduced by splitting large orchestrations into multiple suborchestrations or by reducing the size of outputs returned by the activity and suborchestrator functions it calls. Alternatively, you can reduce memory usage by lowering per-VM [concurrency throttles](durable-functions-perf-and-scale#concurrency-throttles) to limit how many orchestrations are loaded into memory concurrently.

### Instances table

The **Instances** table contains the statuses of all orchestration and entity instances within a task hub. As instances are created, new rows are added to this table. The partition key of this table is the orchestration instance ID or entity key and the row key is an empty string. There's one row per orchestration or entity instance.

This table is used to satisfy [instance query requests from code](durable-functions-instance-management#query-instances) and [status query HTTP API](durable-functions-http-api#get-instance-status) calls. It's kept eventually consistent with the contents of the **History** table mentioned previously. The use of a separate Azure Storage table to efficiently satisfy instance query operations in this way is influenced by the [Command and Query Responsibility Segregation (CQRS) pattern](/en-us/azure/architecture/patterns/cqrs).

Tip

The partitioning of the *Instances* table allows it to store millions of orchestration instances without any noticeable impact on runtime performance or scale. However, the number of instances can have a significant impact on [multi-instance query](durable-functions-instance-management#query-all-instances) performance. To control the amount of data stored in these tables, consider periodically [purging old instance data](durable-functions-instance-management#purge-instance-history).

### Partitions table

Note

This table is shown in the task hub only when `Table Partition Manager`

is enabled. To apply it, configure `useTablePartitionManagement`

setting in your app's [host.json](durable-functions-bindings?tabs=2x-durable-functions#host-json).

The **Partitions** table stores the status of partitions for the Durable Functions app and is used to distribute partitions across your app's workers. There's one row per partition.

### Queues

Orchestrator, entity, and activity functions are all triggered by internal queues in the function app's task hub. Using queues in this way provides reliable "at-least-once" message delivery guarantees. There are two types of queues in Durable Functions: the **control queue** and the **work-item queue**.

#### The work-item queue

There's one work-item queue per task hub in Durable Functions. It's a basic queue and behaves similarly to any other `queueTrigger`

queue in Azure Functions. This queue is used to trigger stateless *activity functions* by dequeueing a single message at a time. Each of these messages contains activity function inputs and other metadata, such as which function to execute. When a Durable Functions application scales out to multiple VMs, these VMs all compete to acquire tasks from the work-item queue.

#### Control queues

There are multiple *control queues* per task hub in Durable Functions. A *control queue* is more sophisticated than the simpler work-item queue. Control queues are used to trigger the stateful orchestrator and entity functions. Because the orchestrator and entity function instances are stateful singletons, it's important that each orchestration or entity is only processed by one worker at a time. To achieve this constraint, each orchestration instance or entity is assigned to a single control queue. These control queues are load balanced across workers to ensure that each queue is only processed by one worker at a time. More details on this behavior can be found in subsequent sections.

Control queues contain various orchestration lifecycle message types. Examples include [orchestrator control messages](durable-functions-instance-management), activity function *response* messages, and timer messages. As many as 32 messages will be dequeued from a control queue in a single poll. These messages contain payload data and metadata including which orchestration instance it's intended for. If multiple dequeued messages are intended for the same orchestration instance, they'll be processed as a batch.

Control queue messages are constantly polled using a background thread. The batch size of each queue poll is controlled by the `controlQueueBatchSize`

setting in host.json and has a default of 32 (the maximum value supported by Azure Queues). The maximum number of prefetched control-queue messages that are buffered in memory is controlled by the `controlQueueBufferThreshold`

setting in host.json. The default value for `controlQueueBufferThreshold`

varies depending on various factors, including the type of hosting plan. For more information on these settings, see the [host.json schema](../functions-host-json#durabletask) documentation.

Tip

Increasing the value for `controlQueueBufferThreshold`

allows a single orchestration or entity to process events faster. However, increasing this value can also result in higher memory usage. The higher memory usage is partly due to pulling more messages off the queue and partly due to fetching more orchestration histories into memory. Reducing the value for `controlQueueBufferThreshold`

can therefore be an effective way to reduce memory usage.

#### Queue polling

The durable task extension implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs. When a message is found, the runtime immediately checks for another message. When no message is found, it waits for a period of time before trying again. After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to 30 seconds.

The maximum polling delay is configurable via the `maxQueuePollingInterval`

property in the [host.json file](../functions-host-json#durabletask). Setting this property to a higher value could result in higher message processing latencies. Higher latencies would be expected only after periods of inactivity. Setting this property to a lower value could result in [higher storage costs](durable-functions-billing#azure-storage-transactions) due to increased storage transactions.

Note

When running in the Azure Functions Consumption and Premium plans, the [Azure Functions Scale Controller](../event-driven-scaling) polls each control and work-item queue once every 10 seconds. This extra polling is necessary to determine when to activate function app instances and to make scale decisions. At the time of writing, this 10-second interval is constant and can't be configured.

#### Orchestration start delays

Orchestrations instances are started by putting an `ExecutionStarted`

message in one of the task hub's control queues. Under certain conditions, you may observe multi-second delays between when an orchestration is scheduled to run and when it actually starts running. During this time interval, the orchestration instance remains in the `Pending`

state. There are two potential causes of this delay:

**Backlogged control queues**: If the control queue for this instance contains a large number of messages, it may take time before the`ExecutionStarted`

message is received and processed by the runtime. Message backlogs can happen when orchestrations are processing lots of events concurrently. Events that go into the control queue include orchestration start events, activity completions, durable timers, termination, and external events. If this delay happens under normal circumstances, consider creating a new task hub with a larger number of partitions. Configuring more partitions causes the runtime to create more control queues for load distribution. Each partition corresponds to 1:1 with a control queue, with a maximum of 16 partitions.**Back off polling delays**: Another common cause of orchestration delays is the[previously described back-off polling behavior for control queues](#queue-polling). However, this delay is only expected when an app is scaled out to two or more instances. If there's only one app instance or if the app instance that starts the orchestration is also the same instance that is polling the target control queue, then there won't be a queue polling delay. Back off polling delays can be reduced by updating the**host.json**settings, as described previously.

### Blobs

In most cases, Durable Functions doesn't use Azure Storage Blobs to persist data. However, queues and tables have [size limits](../../azure-resource-manager/management/azure-subscription-service-limits#azure-queue-storage-limits) that can prevent Durable Functions from persisting all of the required data into a storage row or queue message. For example, when a piece of data that needs to be persisted to a queue is greater than 45 KB when serialized, Durable Functions compresses the data and store it in a blob instead. When persisting data to blob storage in this way, Durable Function stores a reference to that blob in the table row or queue message. When Durable Functions needs to retrieve the data it will automatically fetch it from the blob. These blobs are stored in the blob container `<taskhub>-largemessages`

.

#### Performance considerations

The extra compression and blob operation steps for large messages can be expensive in terms of CPU and I/O latency costs. Additionally, Durable Functions needs to load persisted data in memory, and may do so for many different function executions at the same time. As a result, persisting large data payloads can cause high memory usage as well. To minimize memory overhead, consider persisting large data payloads manually (for example, in blob storage) and instead pass around references to this data. This way your code can load the data only when needed to avoid redundant loads during [orchestrator function replays](durable-functions-orchestrations#reliability). However, storing payloads to local disks is *not* recommended since on-disk state is not guaranteed to be available since functions may execute on different VMs throughout their lifetimes.

### Storage account selection

The queues, tables, and blobs used by Durable Functions are created in a configured Azure Storage account. The account to use can be specified using the `durableTask/storageProvider/connectionStringName`

setting (or `durableTask/azureStorageConnectionStringName`

setting in Durable Functions 1.x) in the **host.json** file.

```
{
"extensions": {
"durableTask": {
"storageProvider": {
"connectionStringName": "MyStorageAccountAppSetting"
}
}
}
}
```


Keep in mind these considerations when choosing the storage account used by your Durable function app:

- When not specified, the default
`AzureWebJobsStorage`

storage account is used. - When possible, you should use Microsoft Entra authentication with managed identities to secure your storage account connection. For more information, see
[configure Durable Functions with managed identity](durable-functions-configure-managed-identity). - For performance-sensitive workloads, you should configure a storage account other than the default account (
`AzureWebJobsStorage`

). Durable Functions uses Azure Storage heavily, and using a dedicated storage account isolates Durable Functions storage usage from the internal usage by the Azure Functions host. - Standard general purpose Azure Storage accounts are required when using the Azure Storage provider. All other storage account types aren't currently supported.
- We highly recommend using legacy v1 general purpose storage accounts for Durable Functions. The newer v2 storage accounts can be significantly more expensive for Durable Functions workloads. For more information on Azure Storage account types, see the
[Storage account overview](../../storage/common/storage-account-overview)documentation.

### Orchestrator scale-out

While activity functions can be scaled out infinitely by adding more VMs elastically, individual orchestrator instances and entities are constrained to inhabit a single partition and the maximum number of partitions is bounded by the `partitionCount`

setting in your `host.json`

.

Note

Generally speaking, orchestrator functions are intended to be lightweight and should not require large amounts of computing power. It is therefore not necessary to create a large number of control-queue partitions to get great throughput for orchestrations. Most of the heavy work should be done in stateless activity functions, which can be scaled out infinitely.

The number of control queues is defined in the **host.json** file. The following example host.json snippet sets the `durableTask/storageProvider/partitionCount`

property (or `durableTask/partitionCount`

in Durable Functions 1.x) to `3`

. Note that there are as many control queues as there are partitions.

```
{
"extensions": {
"durableTask": {
"storageProvider": {
"partitionCount": 3
}
}
}
}
```


A task hub can be configured with between 1 and 16 partitions. If not specified, the default partition count is **4**.

During low traffic scenarios, your application will be scaled-in, so partitions will be managed by a small number of workers. As an example, consider the diagram below.

In the previous diagram, we see that orchestrators 1 through 6 are load balanced across partitions. Similarly, partitions, like activities, are load balanced across workers. Partitions are load-balanced across workers regardless of the number of orchestrators that get started.

If you're running on the Azure Functions Consumption or Elastic Premium plans, or if you have load-based auto-scaling configured, more workers will get allocated as traffic increases and partitions will eventually load balance across all workers. If we continue to scale out, eventually each partition will eventually be managed by a single worker. Activities, on the other hand, will continue to be load-balanced across all workers. This is shown in the image below.

The upper-bound of the maximum number of concurrent *active* orchestrations at *any given time* is equal to the number of workers allocated to your application *times* your value for `maxConcurrentOrchestratorFunctions`

. This upper-bound can be made more precise when your partitions are fully scaled-out across workers. When fully scaled-out, and since each worker will have only a single Functions host instance, the maximum number of *active* concurrent orchestrator instances will be equal to your number of partitions *times* your value for `maxConcurrentOrchestratorFunctions`

.

Note

In this context, *active* means that an orchestration or entity is loaded into memory and processing *new events*. If the orchestration or entity is waiting for more events, such as the return value of an activity function, it gets unloaded from memory and is no longer considered *active*. Orchestrations and entities will be subsequently reloaded into memory only when there are new events to process. There's no practical maximum number of *total* orchestrations or entities that can run on a single VM, even if they're all in the "Running" state. The only limitation is the number of *concurrently active* orchestration or entity instances.

The image below illustrates a fully scaled-out scenario where more orchestrators are added but some are inactive, shown in grey.

During scale-out, control queue leases may be redistributed across Functions host instances to ensure that partitions are evenly distributed. These leases are internally implemented as Azure Blob storage leases and ensure that any individual orchestration instance or entity only runs on a single host instance at a time. If a task hub is configured with three partitions (and therefore three control queues), orchestration instances and entities can be load-balanced across all three lease-holding host instances. Additional VMs can be added to increase capacity for activity function execution.

The following diagram illustrates how the Azure Functions host interacts with the storage entities in a scaled out environment.

As shown in the previous diagram, all VMs compete for messages on the work-item queue. However, only three VMs can acquire messages from control queues, and each VM locks a single control queue.

Orchestration instances and entities are distributed across all control queue instances. The distribution is done by hashing the instance ID of the orchestration or the entity name and key pair. Orchestration instance IDs by default are random GUIDs, ensuring that instances are equally distributed across all control queues.

Generally speaking, orchestrator functions are intended to be lightweight and should not require large amounts of computing power. It is therefore not necessary to create a large number of control queue partitions to get great throughput for orchestrations. Most of the heavy work should be done in stateless activity functions, which can be scaled out infinitely.

## Extended sessions

Extended sessions is a [caching mechanism](durable-functions-perf-and-scale#instance-caching) that keeps orchestrations and entities in memory even after they finish processing messages. The typical effect of enabling extended sessions is reduced I/O against the underlying durable store and overall improved throughput.

You can enable extended sessions by setting `durableTask/extendedSessionsEnabled`

to `true`

in the **host.json** file. The `durableTask/extendedSessionIdleTimeoutInSeconds`

setting can be used to control how long an idle session will be held in memory:

```
{
"extensions": {
"durableTask": {
"extendedSessionsEnabled": true,
"extendedSessionIdleTimeoutInSeconds": 30
}
}
}
```


**Functions 1.0**

```
{
"durableTask": {
"extendedSessionsEnabled": true,
"extendedSessionIdleTimeoutInSeconds": 30
}
}
```


There are two potential downsides of this setting to be aware of:

- There's an overall increase in function app memory usage because idle instances are not unloaded from memory as quickly.
- There can be an overall decrease in throughput if there are many concurrent, distinct, short-lived orchestrator or entity function executions.

As an example, if `durableTask/extendedSessionIdleTimeoutInSeconds`

is set to 30 seconds, then a short-lived orchestrator or entity function episode that executes in less than 1 second still occupies memory for 30 seconds. It also counts against the `durableTask/maxConcurrentOrchestratorFunctions`

quota mentioned previously, potentially preventing other orchestrator or entity functions from running.

The specific effects of extended sessions on orchestrator and entity functions are described in the next sections.

Note

This feature is available only for .NET languages such as C# (isolated and in-process models) and F#. Setting `extendedSessionsEnabled`

to `true`

for other platforms can lead to runtime issues, such as silently failing to execute activity and orchestration-triggered functions.

### Orchestrator function replay

As mentioned previously, orchestrator functions are replayed using the contents of the **History** table. By default, the orchestrator function code is replayed every time a batch of messages are dequeued from a control queue. Even if you are using the fan-out, fan-in pattern and are awaiting for all tasks to complete (for example, using `Task.WhenAll()`

in .NET, `context.df.Task.all()`

in JavaScript, or `context.task_all()`

in Python), there will be replays that occur as batches of task responses are processed over time. When extended sessions are enabled, orchestrator function instances are held in memory longer and new messages can be processed without a full history replay.

The performance improvement of extended sessions is most often observed in the following situations:

- When there are a limited number of orchestration instances running concurrently.
- When orchestrations have large number of sequential actions (for example, hundreds of activity function calls) that complete quickly.
- When orchestrations fan-out and fan-in a large number of actions that complete around the same time.
- When orchestrator functions need to process large messages or do any CPU-intensive data processing.

In all other situations, there is typically no observable performance improvement for orchestrator functions.

Note

These settings should only be used after an orchestrator function has been fully developed and tested. The default aggressive replay behavior can be useful for detecting [orchestrator function code constraints](durable-functions-code-constraints) violations at development time, and is therefore disabled by default.

### Performance targets

The following table shows the expected *maximum* throughput numbers for the scenarios described in the [Performance Targets](durable-functions-perf-and-scale#performance-targets) section of the [Performance and Scale](durable-functions-perf-and-scale) article.

"Instance" refers to a single instance of an orchestrator function running on a single small ([A1](/en-us/azure/virtual-machines/sizes-previous-gen)) VM in Azure App Service. In all cases, it is assumed that [extended sessions](#orchestrator-function-replay) are enabled. Actual results may vary depending on the CPU or I/O work performed by the function code.

| Scenario | Maximum throughput |
|---|---|
| Sequential activity execution | 5 activities per second, per instance |
| Parallel activity execution (fan-out) | 100 activities per second, per instance |
| Parallel response processing (fan-in) | 150 responses per second, per instance |
| External event processing | 50 events per second, per instance |
| Entity operation processing | 64 operations per second |

If you are not seeing the throughput numbers you expect and your CPU and memory usage appears healthy, check to see whether the cause is related to [the health of your storage account](../../storage/common/storage-monitoring-diagnosing-troubleshooting#troubleshooting-guidance). The Durable Functions extension can put significant load on an Azure Storage account and sufficiently high loads may result in storage account throttling.

Tip

In some cases you can significantly increase the throughput of external events, activity fan-in, and entity operations by increasing the value of the `controlQueueBufferThreshold`

setting in **host.json**. Increasing this value beyond its default causes the Durable Task Framework storage provider to use more memory to prefetch these events more aggressively, reducing delays associated with dequeueing messages from the Azure Storage control queues. For more information, see the [host.json](durable-functions-bindings#host-json) reference documentation.

### Flex Consumption Plan

The [Flex Consumption plan](../flex-consumption-plan) is an Azure Functions hosting plan that provides many of the benefits of the Consumption plan, including a serverless billing model, while also adding useful features, such as private networking, instance memory size selection, and full support for managed identity authentication.

You should follow these performance recommendations when hosting Durable Functions in the Flex Consumption plan:

- Set the
[always ready instance count](../flex-consumption-how-to#set-always-ready-instance-counts)for the`durable`

group to`1`

. This ensures that there is always one instance ready to handle Durable Functions related requests, thus reducing the application's cold start. - Reduce the
[queue polling interval](durable-functions-azure-storage-provider#queue-polling)to 10 seconds or less. Since this plan type is more sensitive to queue polling delays, lowering the polling interval will help increase the frequency of polling operations, thus ensuring requests are handled faster. However, more frequent polling operations will lead to a higher Azure Storage account cost.

### High throughput processing

The architecture of the Azure Storage backend puts certain limitations on the maximum theoretical performance and scalability of Durable Functions. If your testing shows that Durable Functions on Azure Storage won't meet your throughput requirements, you should consider instead using the [Netherite storage provider for Durable Functions](durable-functions-storage-providers#netherite).

To compare the achievable throughput for various basic scenarios, see the section [Basic Scenarios](https://microsoft.github.io/durabletask-netherite/#/scenarios) of the Netherite storage provider documentation.

The Netherite storage backend was designed and developed by [Microsoft Research](https://www.microsoft.com/research). It uses [Azure Event Hubs](../../event-hubs/event-hubs-about) and the [FASTER](https://www.microsoft.com/research/project/faster/) database technology on top of [Azure Page Blobs](../../storage/blobs/storage-blob-pageblob-overview). The design of Netherite enables significantly higher-throughput processing of orchestrations and entities compared to other providers. In some benchmark scenarios, throughput was shown to increase by more than an order of magnitude when compared to the default Azure Storage provider.

For more information on the supported storage providers for Durable Functions and how they compare, see the [Durable Functions storage providers](durable-functions-storage-providers) documentation.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-dotnet-entities -->

# Developer's guide to durable entities in .NET

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, we describe the available interfaces for developing durable entities with .NET in detail, including examples and general advice.

Entity functions provide serverless application developers with a convenient way to organize application state as a collection of fine-grained entities. For more detail about the underlying concepts, see the [Durable Entities: Concepts](durable-functions-entities) article.

We currently offer two APIs for defining entities:

The

**class-based syntax**represents entities and operations as classes and methods. This syntax produces easily readable code and allows operations to be invoked in a type-checked manner through interfaces.The

**function-based syntax**is a lower-level interface that represents entities as functions. It provides precise control over how the entity operations are dispatched, and how the entity state is managed.

This article focuses primarily on the class-based syntax, as we expect it to be better suited for most applications. However, the [function-based syntax](#function-based-syntax) can be appropriate for applications that wish to define or manage their own abstractions for entity state and operations. Also, it can be appropriate for implementing libraries that require genericity not currently supported by the class-based syntax.

Note

The class-based syntax is just a layer on top of the function-based syntax, so both variants can be used interchangeably in the same application.

## Defining entity classes

The following example is an implementation of a `Counter`

entity that stores a single value of type integer, and offers four operations `Add`

, `Reset`

, `Get`

, and `Delete`

.

```
[JsonObject(MemberSerialization.OptIn)]
public class Counter
{
[JsonProperty("value")]
public int Value { get; set; }
public void Add(int amount)
{
this.Value += amount;
}
public Task Reset()
{
this.Value = 0;
return Task.CompletedTask;
}
public Task<int> Get()
{
return Task.FromResult(this.Value);
}
public void Delete()
{
Entity.Current.DeleteState();
}
[FunctionName(nameof(Counter))]
public static Task Run([EntityTrigger] IDurableEntityContext ctx)
=> ctx.DispatchAsync<Counter>();
}
```


The `Run`

function contains the boilerplate required for using the class-based syntax. It must be a *static* Azure Function. It executes once for each operation message that is processed by the entity. When `DispatchAsync<T>`

is called and the entity isn't already in memory, it constructs an object of type `T`

and populates its fields from the last persisted JSON found in storage (if any). Then it invokes the method with the matching name.

The `EntityTrigger`

Function, `Run`

in this sample, doesn't need to reside within the Entity class itself. It can reside within any valid location for an Azure Function: inside the top-level namespace, or inside a top-level class. However, if nested deeper (e.g, the Function is declared inside a *nested* class), then this Function won't be recognized by the latest runtime.

Note

The state of a class-based entity is **created implicitly** before the entity processes an operation and can be **deleted explicitly** in an operation by calling `Entity.Current.DeleteState()`

.

Note

You need [Azure Functions Core Tools](../functions-run-local) version `4.0.5455`

or above to run entities in the isolated model.

There are two ways of defining an entity as a class in the C# isolated worker model. They produce entities with different state serialization structures.

With the following approach, the entire object is serialized when defining an entity.

```
public class Counter
{
public int Value { get; set; }
public void Add(int amount)
{
this.Value += amount;
}
public Task Reset()
{
this.Value = 0;
return Task.CompletedTask;
}
public Task<int> Get()
{
return Task.FromResult(this.Value);
}
// Delete is implicitly defined when defining an entity this way
[Function(nameof(Counter))]
public static Task Run([EntityTrigger] TaskEntityDispatcher dispatcher)
=> dispatcher.DispatchAsync<Counter>();
}
```


A `TaskEntity<TState>`

-based implementation, which makes it easy to use dependency injection. In this case, state is deserialized to the `State`

property, and no other property is serialized/deserialized.

```
public class Counter : TaskEntity<int>
{
readonly ILogger logger;
public Counter(ILogger<Counter> logger)
{
this.logger = logger;
}
public void Add(int amount)
{
this.State += amount;
}
public Task Reset()
{
this.State = 0;
return Task.CompletedTask;
}
public Task<int> Get()
{
return Task.FromResult(this.State);
}
// Delete is implicitly defined when defining an entity this way
[Function(nameof(Counter))]
public static Task Run([EntityTrigger] TaskEntityDispatcher dispatcher)
=> dispatcher.DispatchAsync<Counter>();
}
```


Warning

When writing entities that derive from `ITaskEntity`

or `TaskEntity<TState>`

, it's important to **not** name your entity trigger method `RunAsync`

. This causes runtime errors when invoking the entity, as there's an ambiguous match with the method name "RunAsync" due to `ITaskEntity`

already defining an instance-level "RunAsync".

### Deleting entities in the isolated model

Deleting an entity in the isolated model is accomplished by setting the entity state to `null`

, and this process depends on the entity implementation path used:

- When deriving from
`ITaskEntity`

or using[function based syntax](#function-based-syntax), delete is accomplished by calling`TaskEntityOperation.State.SetState(null)`

. - When deriving from
`TaskEntity<TState>`

, delete is implicitly defined. However, it can be overridden by defining a method`Delete`

on the entity. State can also be deleted from any operation via`this.State = null`

.- To delete by setting state to null requires
`TState`

to be nullable. - The implicitly defined delete operation deletes non-nullable
`TState`

.

- To delete by setting state to null requires
- When using a POCO as your state (not deriving from
`TaskEntity<TState>`

), delete is implicitly defined. It's possible to override the delete operation by defining a method`Delete`

on the POCO. However, there isn't a way to set state to`null`

in the POCO route, so the implicitly defined delete operation is the only true delete.

### Class Requirements

Entity classes are POCOs (plain old CLR objects) that don't require special superclasses, interfaces, or attributes. However:

- The class must be constructible (see
[Entity construction](#entity-construction)). - The class must be JSON-serializable (see
[Entity serialization](#entity-serialization)).

Also, any method invoked as an operation must satisfy other requirements:

- An operation must have at most one argument but not have any overloads or generic type arguments.
- An operation meant to be called from an orchestration using an interface must return
`Task`

or`Task<T>`

. - Arguments and return values must be serializable values or objects.

### What can operations do?

All entity operations can read and update the entity state, and changes to the state are automatically persisted to storage. Moreover, operations can perform external I/O or other computations, within the general limits common to all Azure Functions.

Operations also have access to functionality provided by the `Entity.Current`

context:

`EntityName`

: the name of the currently executing entity.`EntityKey`

: the key of the currently executing entity.`EntityId`

: the ID of the currently executing entity (includes name and key).`SignalEntity`

: sends a one-way message to an entity.`CreateNewOrchestration`

: starts a new orchestration.`DeleteState`

: deletes the state of this entity.

For example, we can modify the counter entity so it starts an orchestration when the counter reaches 100 and passes the entity ID as an input argument:

```
public void Add(int amount)
{
if (this.Value < 100 && this.Value + amount >= 100)
{
Entity.Current.StartNewOrchestration("MilestoneReached", Entity.Current.EntityId);
}
this.Value += amount;
}
```


## Accessing entities directly

Class-based entities can be accessed directly, using explicit string names for the entity and its operations. This section provides examples. For a deeper explanation of the underlying concepts (such as signals vs. calls), see the discussion in [Access entities](durable-functions-entities#access-entities).

Note

Where possible, you should [accesses entities through interfaces](#accessing-entities-through-interfaces), because it provides more type checking.

### Example: client signals entity

The following Azure Http Function implements a DELETE operation using REST conventions. It sends a delete signal to the counter entity whose key is passed in the URL path.

```
[FunctionName("DeleteCounter")]
public static async Task<HttpResponseMessage> DeleteCounter(
[HttpTrigger(AuthorizationLevel.Function, "delete", Route = "Counter/{entityKey}")] HttpRequestMessage req,
[DurableClient] IDurableEntityClient client,
string entityKey)
{
var entityId = new EntityId("Counter", entityKey);
await client.SignalEntityAsync(entityId, "Delete");
return req.CreateResponse(HttpStatusCode.Accepted);
}
```


### Example: client reads entity state

The following Azure HTTP Function implements a GET operation using REST conventions. It reads the current state of the counter entity whose key is passed in the URL path.

```
[FunctionName("GetCounter")]
public static async Task<HttpResponseMessage> GetCounter(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "Counter/{entityKey}")] HttpRequestMessage req,
[DurableClient] IDurableEntityClient client,
string entityKey)
{
var entityId = new EntityId("Counter", entityKey);
var state = await client.ReadEntityStateAsync<Counter>(entityId);
return req.CreateResponse(state);
}
```


Note

The object returned by `ReadEntityStateAsync`

is just a local copy, that is, a snapshot of the entity state from some earlier point in time. In particular, it can be stale, and modifying this object has no effect on the actual entity.

### Example: Orchestration first signals then calls entity

The following orchestration signals a counter entity to increment it, and then calls the same entity to read its latest value.

```
[FunctionName("IncrementThenGet")]
public static async Task<int> Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
var entityId = new EntityId("Counter", "myCounter");
// One-way signal to the entity - does not await a response
context.SignalEntity(entityId, "Add", 1);
// Two-way call to the entity which returns a value - awaits the response
int currentValue = await context.CallEntityAsync<int>(entityId, "Get");
return currentValue;
}
```


### Example: client signals entity

The following Azure HTTP Function implements a DELETE operation using REST conventions. It sends a delete signal to the counter entity whose key is passed in the URL path.

```
[Function("DeleteCounter")]
public static async Task<HttpResponseData> DeleteCounter(
[HttpTrigger(AuthorizationLevel.Function, "delete", Route = "Counter/{entityKey}")] HttpRequestData req,
[DurableClient] DurableTaskClient client, string entityKey)
{
var entityId = new EntityInstanceId("Counter", entityKey);
await client.Entities.SignalEntityAsync(entityId, "Delete");
return req.CreateResponse(HttpStatusCode.Accepted);
}
```


### Example: client reads entity state

The following Azure HTTP Function implements a GET operation using REST conventions. It reads the current state of the counter entity whose key is passed in the URL path.

```
[Function("GetCounter")]
public static async Task<HttpResponseData> GetCounter(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "Counter/{entityKey}")] HttpRequestData req,
[DurableClient] DurableTaskClient client, string entityKey)
{
var entityId = new EntityInstanceId("Counter", entityKey);
EntityMetadata<int>? entity = await client.Entities.GetEntityAsync<int>(entityId);
HttpResponseData response = request.CreateResponse(HttpStatusCode.OK);
await response.WriteAsJsonAsync(entity.State);
return response;
}
```


### Example: Orchestration first signals then calls entity

The following orchestration signals a counter entity to increment it, and then calls the same entity to read its latest value.

```
[Function("IncrementThenGet")]
public static async Task<int> Run([OrchestrationTrigger] TaskOrchestrationContext context)
{
var entityId = new EntityInstanceId("Counter", "myCounter");
// One-way signal to the entity - does not await a response
await context.Entities.SignalEntityAsync(entityId, "Add", 1);
// Two-way call to the entity which returns a value - awaits the response
int currentValue = await context.Entities.CallEntityAsync<int>(entityId, "Get");
return currentValue;
}
```


## Accessing entities through interfaces

Interfaces can be used for accessing entities via generated proxy objects. This approach ensures that the name and argument type of an operation matches what's implemented. It's recommended to use interfaces when possible to access entities.

For example, we can modify the counter example:

```
public interface ICounter
{
void Add(int amount);
Task Reset();
Task<int> Get();
void Delete();
}
public class Counter : ICounter
{
...
}
```


Entity classes and entity interfaces are similar to the grains and grain interfaces popularized by [Orleans](https://www.microsoft.com/research/project/orleans-virtual-actors/). For a more information about similarities and differences between Durable Entities and Orleans, see [Comparison with virtual actors](durable-functions-entities#comparison-with-virtual-actors).

Besides providing type checking, interfaces are useful for a better separation of concerns within the application. For example, since an entity can implement multiple interfaces, a single entity can serve multiple roles. Also, since multiple entities can implement an interface, general communication patterns can be implemented as reusable libraries.

### Example: client signals entity through interface

Client code can use `SignalEntityAsync<TEntityInterface>`

to send signals to entities that implement `TEntityInterface`

. For example:

```
[FunctionName("DeleteCounter")]
public static async Task<HttpResponseMessage> DeleteCounter(
[HttpTrigger(AuthorizationLevel.Function, "delete", Route = "Counter/{entityKey}")] HttpRequestMessage req,
[DurableClient] IDurableEntityClient client,
string entityKey)
{
var entityId = new EntityId("Counter", entityKey);
await client.SignalEntityAsync<ICounter>(entityId, proxy => proxy.Delete());
return req.CreateResponse(HttpStatusCode.Accepted);
}
```


In this example, the `proxy`

parameter is a dynamically generated instance of `ICounter`

, which internally translates the call to `Delete`

into a signal.

Note

The `SignalEntityAsync`

APIs can be used only for one-way operations. Even if an operation returns `Task<T>`

, the value of the `T`

parameter is always null or `default`

instead of the actual result. For example, it doesn't make sense to signal the `Get`

operation since it doesn't return a value. Instead, clients can either use `ReadStateAsync`

to access the counter state directly or start an orchestrator function that calls the `Get`

operation.

### Example: Orchestration first signals then calls entity through proxy

To call or signal an entity from within an orchestration, `CreateEntityProxy`

can be used, along with the interface type, to generate a proxy for the entity. This proxy can then be used to call or signal operations:

```
[FunctionName("IncrementThenGet")]
public static async Task<int> Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
var entityId = new EntityId("Counter", "myCounter");
var proxy = context.CreateEntityProxy<ICounter>(entityId);
// One-way signal to the entity - does not await a response
proxy.Add(1);
// Two-way call to the entity which returns a value - awaits the response
int currentValue = await proxy.Get();
return currentValue;
}
```


Implicitly, any operations that return `void`

are signaled, and any operations that return `Task`

or `Task<T>`

are called. One can change this default behavior, and signal operations even if they return Task, by using the `SignalEntity<IInterfaceType>`

method explicitly.

### Shorter option for specifying the target

When calling or signaling an entity using an interface, the first argument must specify the target entity. The target can be specified by defining the entity ID or just the entity key when there's only one class that implements the entity:

```
context.SignalEntity<ICounter>(new EntityId(nameof(Counter), "myCounter"), ...);
context.SignalEntity<ICounter>("myCounter", ...);
```


If only the entity key is specified and a unique implementation can't be found at runtime, `InvalidOperationException`

is thrown.

### Restrictions on entity interfaces

As usual, all parameter and return types must be JSON-serializable. Otherwise, serialization exceptions are thrown at runtime. The following rules also apply:

- Entity interfaces must be defined in the same assembly as the entity class.
- Entity interfaces must only define methods.
- Entity interfaces must not contain generic parameters.
- Entity interface methods must not have more than one parameter.
- Entity interface methods must return
`void`

,`Task`

, or`Task<T>`

.

If any of these rules are violated, an `InvalidOperationException`

is thrown at runtime when the interface is used as a type argument to `SignalEntity`

, `SignalEntityAsync`

, or `CreateEntityProxy`

. The exception message explains which rule was broken.

Note

Interface methods returning `void`

can only be signaled (one-way), not called (two-way). Interface methods returning `Task`

or `Task<T>`

can be either called or signaled. If called, they return the result of the operation or re-throw exceptions thrown by the operation. If signaled, they return the default value and not the actual result or exception from the operation.

This isn't currently supported in the .NET isolated worker.

## Entity serialization

Since the state of an entity is durably persisted, the entity class must be serializable. The Durable Functions runtime uses the [Json.NET](https://www.newtonsoft.com/json) library for this purpose, which supports policies and attributes to control the serialization and deserialization process. Most commonly used C# data types (including arrays and collection types) are already serializable, and can easily be used for defining the state of durable entities.

For example, Json.NET can easily serialize and deserialize the following class:

```
[JsonObject(MemberSerialization = MemberSerialization.OptIn)]
public class User
{
[JsonProperty("name")]
public string Name { get; set; }
[JsonProperty("yearOfBirth")]
public int YearOfBirth { get; set; }
[JsonProperty("timestamp")]
public DateTime Timestamp { get; set; }
[JsonProperty("contacts")]
public Dictionary<Guid, Contact> Contacts { get; set; } = new Dictionary<Guid, Contact>();
[JsonObject(MemberSerialization = MemberSerialization.OptOut)]
public struct Contact
{
public string Name;
public string Number;
}
...
}
```


### Serialization Attributes

In the example above, we include several attributes to make the underlying serialization more visible:

- We annotate the class with
`[JsonObject(MemberSerialization.OptIn)]`

to remind us that the class must be serializable, and to persist only members that are explicitly marked as JSON properties. - We annotate the fields to be persisted with
`[JsonProperty("name")]`

to remind us that a field is part of the persisted entity state and to specify the property name to be used in the JSON representation.

However, these attributes aren't required; other conventions or attributes are permitted as long as they work with Json.NET. For example, one can use `[DataContract]`

attributes or no attributes at all:

```
[DataContract]
public class Counter
{
[DataMember]
public int Value { get; set; }
...
}
public class Counter
{
public int Value;
...
}
```


By default, the name of the class isn't* stored as part of the JSON representation: that is, we use `TypeNameHandling.None`

as the default setting. This default behavior can be overridden using `JsonObject`

or `JsonProperty`

attributes.

### Making changes to class definitions

Some care is required when making changes to a class definition after an application runs because the stored JSON object can no longer match the new class definition. It is often possible to deal correctly with changing data formats as long as one understands the deserialization process used by `JsonConvert.PopulateObject`

. The following are examples of changes and their impact:

- When a new property not present in the stored JSON is added, it assumes its default value.
- When a property present in the stored JSON is removed, the previous content is lost.
- When a property is renamed, the effect is that of removing the old one and adding a new one.
- When a property type is changed so it can't be deserialized from the stored JSON, an exception is thrown.
- When a property type is changed so it can still be deserialized from the stored JSON, it does so.

There are many options available for customizing the behavior of Json.NET. For example, to force an exception if the stored JSON contains a field that isn't present in the class, specify the attribute `JsonObject(MissingMemberHandling = MissingMemberHandling.Error)`

. It's also possible to write custom code for deserialization that can read JSON stored in arbitrary formats.

Serialization default behavior has changed from `Newtonsoft.Json`

to` System.Text.Json`

. For more information, see [Customizing serialization and deserialization](durable-functions-serialization-and-persistence?tabs=csharp-isolated#customizing-serialization-and-deserialization).

## Entity construction

Sometimes we want to exert more control over how entity objects are constructed. We now describe several options for changing the default behavior when constructing entity objects.

### Custom initialization on first access

Occasionally we need to perform some special initialization before dispatching an operation to an entity that has never been accessed, or that has been deleted. To specify this behavior, one can add a conditional before the `DispatchAsync`

:

```
[FunctionName(nameof(Counter))]
public static Task Run([EntityTrigger] IDurableEntityContext ctx)
{
if (!ctx.HasState)
{
ctx.SetState(...);
}
return ctx.DispatchAsync<Counter>();
}
```


### Bindings in entity classes

Unlike regular functions, entity class methods don't have direct access to input and output bindings. Instead, binding data must be captured in the entry-point function declaration and then passed to the `DispatchAsync<T>`

method. Any objects passed to `DispatchAsync<T>`

are passed automatically to the entity class constructor as an argument.

The following example shows how a `CloudBlobContainer`

reference from the [blob input binding](../functions-bindings-storage-blob-input) can be made available to a class-based entity.

```
public class BlobBackedEntity
{
[JsonIgnore]
private readonly CloudBlobContainer container;
public BlobBackedEntity(CloudBlobContainer container)
{
this.container = container;
}
// ... entity methods can use this.container in their implementations ...
[FunctionName(nameof(BlobBackedEntity))]
public static Task Run(
[EntityTrigger] IDurableEntityContext context,
[Blob("my-container", FileAccess.Read)] CloudBlobContainer container)
{
// passing the binding object as a parameter makes it available to the
// entity class constructor
return context.DispatchAsync<BlobBackedEntity>(container);
}
}
```


For more information on bindings in Azure Functions, see [Azure Functions triggers and bindings concepts](../functions-triggers-bindings).

### Dependency injection in entity classes

Entity classes support [Azure Functions Dependency Injection](../functions-dotnet-dependency-injection). The following example demonstrates how to register an `IHttpClientFactory`

service into a class-based entity.

```
[assembly: FunctionsStartup(typeof(MyNamespace.Startup))]
namespace MyNamespace
{
public class Startup : FunctionsStartup
{
public override void Configure(IFunctionsHostBuilder builder)
{
builder.Services.AddHttpClient();
}
}
}
```


The following snippet demonstrates how to incorporate the injected service into your entity class:

```
public class HttpEntity
{
[JsonIgnore]
private readonly HttpClient client;
public HttpEntity(IHttpClientFactory factory)
{
this.client = factory.CreateClient();
}
public Task<int> GetAsync(string url)
{
using (var response = await this.client.GetAsync(url))
{
return (int)response.StatusCode;
}
}
[FunctionName(nameof(HttpEntity))]
public static Task Run([EntityTrigger] IDurableEntityContext ctx)
=> ctx.DispatchAsync<HttpEntity>();
}
```


### Custom initialization on first access

```
public class Counter : TaskEntity<int>
{
protected override int InitializeState(TaskEntityOperation operation)
{
// This is called when state is null, giving a chance to customize first-access of entity.
return 10;
}
}
```


### Bindings in entity classes

The following example shows how to use a [blob input binding](../functions-bindings-storage-blob-input) in a class-based entity.

```
public class BlobBackedEntity : TaskEntity<object?>
{
private BlobContainerClient Container { get; set; }
[Function(nameof(BlobBackedEntity))]
public Task DispatchAsync(
[EntityTrigger] TaskEntityDispatcher dispatcher,
[BlobInput("my-container")] BlobContainerClient container)
{
this.Container = container;
return dispatcher.DispatchAsync(this);
}
}
```


For more information on bindings in Azure Functions, see the [Azure Functions Triggers and Bindings](../functions-triggers-bindings) documentation.

### Dependency injection in entity classes

Entity classes support [Azure Functions Dependency Injection](../dotnet-isolated-process-guide#dependency-injection).

The following example demonstrates how to configure an `HttpClient`

in the `program.cs`

file to be imported later in the entity class:

```
public class Program
{
public static void Main()
{
IHost host = new HostBuilder()
.ConfigureFunctionsWorkerDefaults((IFunctionsWorkerApplicationBuilder workerApplication) =>
{
workerApplication.Services.AddHttpClient<HttpEntity>()
.ConfigureHttpClient(client => {/* configure http client here */});
})
.Build();
host.Run();
}
}
```


The following example demonstrates how to incorporate the injected service into your entity class:

```
public class HttpEntity : TaskEntity<object?>
{
private readonly HttpClient client;
public HttpEntity(HttpClient client)
{
this.client = client;
}
public async Task<int> GetAsync(string url)
{
using var response = await this.client.GetAsync(url);
return (int)response.StatusCode;
}
[Function(nameof(HttpEntity))]
public static Task Run([EntityTrigger] TaskEntityDispatcher dispatcher)
=> dispatcher.DispatchAsync<HttpEntity>();
}
```


Note

To avoid issues with serialization, make sure to exclude fields that store injected values from the serialization.

Note

Unlike when using constructor injection in regular .NET Azure Functions, the functions entry point method for class-based entities *must* be declared `static`

. Declaring a function entry point that isn't static can cause conflicts between the normal Azure Functions object initializer and the Durable Entities object initializer.

## Function-based syntax

So far we have focused on the class-based syntax, as we expect it to be better suited for most applications. However, the function-based syntax can be appropriate for applications that wish to define or manage their own abstractions for entity state and operations. Also, it can be appropriate when implementing libraries that require genericity not currently supported by the class-based syntax.

With the function-based syntax, the Entity Function explicitly handles the operation dispatch, and explicitly manages the state of the entity. For example, the following code shows the *Counter* entity implemented using the function-based syntax.

```
[FunctionName("Counter")]
public static void Counter([EntityTrigger] IDurableEntityContext ctx)
{
switch (ctx.OperationName.ToLowerInvariant())
{
case "add":
ctx.SetState(ctx.GetState<int>() + ctx.GetInput<int>());
break;
case "reset":
ctx.SetState(0);
break;
case "get":
ctx.Return(ctx.GetState<int>());
break;
case "delete":
ctx.DeleteState();
break;
}
}
```


### The entity context object

Entity-specific functionality can be accessed via a context object of type `IDurableEntityContext`

. This context object is available as a parameter to the entity function, and via the async-local property `Entity.Current`

.

The following members provide information about the current operation and help to specify a return value:

`EntityName`

: The name of the currently executing entity`EntityKey`

: The key of the currently executing entity`EntityId`

: The ID of the currently executing entity (includes name and key)`OperationName`

: The name of the current operation`GetInput<TInput>()`

: Gets the input for the current operation`Return(arg)`

: Returns a value to the orchestration that called the operation

The following members manage the state of the entity (create, read, update, delete):

`HasState`

: If the entity exists; i.e., has some state`GetState<TState>()`

: Gets the current state of the entity and creates one if it doesn't exist`SetState(arg)`

: Creates or updates the state of the entity`DeleteState()`

: Deletes the state of the entity if it exists

If the state returned by `GetState`

is an object, the application code can modify it. There's no need to call `SetState`

again at the end (but also no harm). If `GetState<TState>`

is called multiple times, the same type must be used.

Finally, the following members signal other entities or start new orchestrations:

`SignalEntity(EntityId, operation, input)`

: Sends a one-way message to an entity`CreateNewOrchestration(orchestratorFunctionName, input)`

: Starts a new orchestration

```
[Function(nameof(Counter))]
public static Task DispatchAsync([EntityTrigger] TaskEntityDispatcher dispatcher)
{
return dispatcher.DispatchAsync(operation =>
{
if (operation.State.GetState(typeof(int)) is null)
{
operation.State.SetState(0);
}
switch (operation.Name.ToLowerInvariant())
{
case "add":
int state = operation.State.GetState<int>();
state += operation.GetInput<int>();
operation.State.SetState(state);
return new(state);
case "reset":
operation.State.SetState(0);
break;
case "get":
return new(operation.State.GetState<int>());
case "delete":
operation.State.SetState(null);
break;
}
return default;
});
}
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-bindings -->

# Bindings for Durable Functions (Azure Functions)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Durable Functions](durable-functions-overview) extension introduces three trigger bindings that control the execution of orchestrator, entity, and activity functions. It also introduces an output binding that acts as a client for the Durable Functions runtime.

This article discusses the use of these four bindings and provides code samples. It also provides information about the Durable Functions configuration properties in *host.json*, the metadata file that contains settings that affect all functions in a function app.

Make sure to select your Durable Functions development language at the top of the article.

Both versions of the [Python programming model for Azure Functions](../functions-reference-python) are supported by Durable Functions. Because Python v2 is the recommended version, examples in this article exclusively feature this version.

## Prerequisites

- Durable Functions SDK, which is the Python Package Index (PyPI) package
`azure-functions-durable`

, version`1.2.2`

or a later version [Extension bundle](../extension-bundles)version 4.x (or a later version), which is set in the*host.json*project file

You can provide feedback and suggestions in the [Durable Functions SDK for Python repository](https://github.com/Azure/azure-functions-durable-python/issues).

## Orchestration trigger

You can use the orchestration trigger to develop [durable orchestrator functions](durable-functions-types-features-overview#orchestrator-functions). This trigger executes when a new orchestration instance is scheduled and when an existing orchestration instance receives an event. Examples of events that can trigger orchestrator functions include durable timer expirations, activity function responses, and events raised by external clients.

When you develop functions in .NET, you use the [OrchestrationTriggerAttribute](/en-us/dotnet/api/microsoft.azure.webjobs.extensions.durabletask.orchestrationtriggerattribute) .NET attribute to configure the orchestration trigger.

For Java, you use the `@DurableOrchestrationTrigger`

annotation to configure the orchestration trigger.

When you use version 4 of the Node.js programming model to develop functions, you import the `app`

object from the `@azure/functions npm`

module. Then you call the `app.orchestration`

method of the Durable Functions API directly in your function code. This method registers your orchestrator function with the Durable Functions framework.

When you write orchestrator functions, you define the orchestration trigger by using the following JSON object in the `bindings`

array of the *function.json* file:

```
{
"name": "<name-of-input-parameter-in-function-signature>",
"orchestration": "<optional-name-of-orchestration>",
"type": "orchestrationTrigger",
"direction": "in"
}
```


The `orchestration`

value is the name of the orchestration that clients must use when they want to start new instances of the orchestrator function. This property is optional. If you don't specify it, the name of the function is used.

When you use the Python v2 programming model, you can define an orchestration trigger by using the `orchestration_trigger`

decorator directly in your Python function code.

In the v2 model, you access the Durable Functions triggers and bindings from an instance of `DFApp`

. You can use this subclass of `FunctionApp`

to export decorators that are specific to Durable Functions.

Internally, this trigger binding polls the configured durable store for new orchestration events. Examples of events include orchestration start events, durable timer expiration events, activity function response events, and external events raised by other functions.

### Trigger behavior

Here are some notes about the orchestration trigger:

**Single-threading**: A single dispatcher thread is used for all orchestrator function execution on a single host instance. For this reason, it's important to ensure that orchestrator function code is efficient and doesn't perform any I/O operations. It's also important to ensure that this thread doesn't do any asynchronous work except when awaiting task types that are specific to Durable Functions.**Poison-message handling**: There's no support for poison messages in orchestration triggers.**Message visibility**: Orchestration trigger messages are dequeued and kept invisible for a configurable duration. The visibility of these messages is renewed automatically as long as the function app is running and healthy.**Return values**: Return values are serialized to JSON and persisted to the orchestration history table in Azure Table Storage. These return values can be queried by the orchestration client binding, described later.

Warning

Orchestrator functions should never use any input or output bindings other than the orchestration trigger binding. Using other bindings can cause problems with the Durable Task extension, because those bindings might not obey the single-threading and I/O rules. If you want to use other bindings, add them to an activity function called from your orchestrator function. For more information about coding constraints for orchestrator functions, see [Orchestrator function code constraints](durable-functions-code-constraints).

Warning

Orchestrator functions should never be declared `async`

.

### Trigger usage

The orchestration trigger binding supports both inputs and outputs. Here are some notes about input and output handling:

**Inputs**: You can invoke orchestration triggers that have inputs. The inputs are accessed through the context input object. All inputs must be JSON-serializable.**Outputs**: Orchestration triggers support both output and input values. The return value of the function is used to assign the output value. The return value must be JSON-serializable.

### Trigger sample

The following code provides an example of a basic *Hello World* orchestrator function. This example orchestrator doesn't schedule any tasks.

The attribute that you use to define the trigger depends on whether you run your C# functions [in the same process as the Functions host process](../functions-dotnet-class-library) or in an [isolated worker process](../dotnet-isolated-process-guide).

```
[FunctionName("HelloWorld")]
public static string RunOrchestrator([OrchestrationTrigger] IDurableOrchestrationContext context)
{
string name = context.GetInput<string>();
return $"Hello {name}!";
}
```


Note

The preceding code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see [Durable Functions versions overview](durable-functions-versions).

```
const { app } = require('@azure/functions');
const df = require('durable-functions');
df.app.orchestration('helloOrchestrator', function* (context) {
const name = context.df.getInput();
return `Hello ${name}`;
});
```


Note

The `durable-functions`

library calls the synchronous `context.done`

method when the generator function exits.

```
import azure.functions as func
import azure.durable_functions as df
myApp = df.DFApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@myApp.orchestration_trigger(context_name="context")
def my_orchestrator(context):
result = yield context.call_activity("Hello", "Tokyo")
return result
```


```
param($Context)
$InputData = $Context.Input
$InputData
```


```
@FunctionName("HelloWorldOrchestration")
public String helloWorldOrchestration(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
return String.format("Hello %s!", ctx.getInput(String.class));
}
```


Most orchestrator functions call activity functions. The following code provides a *Hello World* example that demonstrates how to call an activity function:

```
[FunctionName("HelloWorld")]
public static async Task<string> RunOrchestrator(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
string name = context.GetInput<string>();
string result = await context.CallActivityAsync<string>("SayHello", name);
return result;
}
```


Note

The preceding code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableOrchestrationContext`

instead of `IDurableOrchestrationContext`

. For more information about the differences between versions, see [Durable Functions versions overview](durable-functions-versions).

```
const { app } = require('@azure/functions');
const df = require('durable-functions');
const activityName = 'hello';
df.app.orchestration('helloOrchestrator', function* (context) {
const name = context.df.getInput();
const result = yield context.df.callActivity(activityName, name);
return result;
});
```


```
@FunctionName("HelloWorld")
public String helloWorldOrchestration(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
String input = ctx.getInput(String.class);
String result = ctx.callActivity("SayHello", input, String.class).await();
return result;
}
```


## Activity trigger

You can use the activity trigger to develop functions known as [activity functions](durable-functions-types-features-overview#activity-functions) that are called by orchestrator functions.

You use the [ActivityTriggerAttribute](/en-us/dotnet/api/microsoft.azure.webjobs.extensions.durabletask.activitytriggerattribute) .NET attribute to configure the activity trigger.

You use the `@DurableActivityTrigger`

annotation to configure the activity trigger.

To register your activity function, you import the `app`

object from the `@azure/functions npm`

module. Then you call the `app.activity`

method of the Durable Functions API directly in your function code.

To define the activity trigger, you use the following JSON object in the `bindings`

array of *function.json*:

```
{
"name": "<name-of-input-parameter-in-function-signature>",
"activity": "<optional-name-of-activity>",
"type": "activityTrigger",
"direction": "in"
}
```


The `activity`

value is the name of the activity. This value is the name that orchestrator functions use to invoke this activity function. This property is optional. If you don't specify it, the name of the function is used.

You can define an activity trigger by using the `activity_trigger`

decorator directly in your Python function code.

Internally, this trigger binding polls the configured durable store for new activity execution events.

### Trigger behavior

Here are some notes about the activity trigger:

**Threading**: Unlike the orchestration trigger, activity triggers don't have any restrictions on threading or I/O operations. They can be treated like regular functions.**Poison-message handling**: There's no support for poison messages in activity triggers.**Message visibility**: Activity trigger messages are dequeued and kept invisible for a configurable duration. The visibility of these messages is renewed automatically as long as the function app is running and healthy.**Return values**: Return values are serialized to JSON and persisted to the configured durable store.

### Trigger usage

The activity trigger binding supports both inputs and outputs, just like the orchestration trigger. Here are some notes about input and output handling:

**Inputs**: Activity triggers can be invoked with inputs from an orchestrator function. All inputs must be JSON-serializable.**Outputs**: Activity functions support both output and input values. The return value of the function is used to assign the output value and must be JSON-serializable.**Metadata**: .NET activity functions can bind to a`string instanceId`

parameter to get the instance ID of the calling orchestration.

### Trigger sample

The following code provides an example of a basic *Hello World* activity function.

```
[FunctionName("SayHello")]
public static string SayHello([ActivityTrigger] IDurableActivityContext helloContext)
{
string name = helloContext.GetInput<string>();
return $"Hello {name}!";
}
```


The default parameter type for the .NET `ActivityTriggerAttribute`

binding is [IDurableActivityContext](/en-us/dotnet/api/microsoft.azure.webjobs.extensions.durabletask.idurableactivitycontext) (or [DurableActivityContext](/en-us/previous-versions/dotnet/api/microsoft.azure.webjobs.durableactivitycontext) for Durable Functions 1.x). However, .NET activity triggers also support binding directly to JSON-serializeable types (including primitive types), so you can also use the following simplified version of the function:

```
[FunctionName("SayHello")]
public static string SayHello([ActivityTrigger] string name)
{
return $"Hello {name}!";
}
```


```
const { app } = require('@azure/functions');
const df = require('durable-functions');
const activityName = 'hello';
df.app.activity(activityName, {
handler: (input) => {
return `Hello, ${input}`;
},
});
```


```
import azure.functions as func
import azure.durable_functions as df
myApp = df.DFApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@myApp.activity_trigger(input_name="myInput")
def my_activity(myInput: str):
return "Hello " + myInput
```


```
param($name)
"Hello $name!"
```


```
@FunctionName("SayHello")
public String sayHello(@DurableActivityTrigger(name = "name") String name) {
return String.format("Hello %s!", name);
}
```


### Use input and output bindings

Besides the activity trigger binding, you can also use regular input and output bindings.

For example, an activity function can receive input from an orchestrator function. The activity function can then send that input as a message to Azure Event Hubs.

```
const { app } = require('@azure/functions');
const df = require('durable-functions');
df.app.orchestration('helloOrchestrator', function* (context) {
const input = context.df.getInput();
yield context.df.callActivity('sendToEventHub', input);
return `Message sent: ${input}`;
});
const { EventHubProducerClient } = require("@azure/event-hubs");
const connectionString = process.env.EVENT_HUB_CONNECTION_STRING;
const eventHubName = process.env.EVENT_HUB_NAME;
df.app.activity("sendToEventHub", {
handler: async (message, context) => {
const producer = new EventHubProducerClient(connectionString, eventHubName);
try {
const batch = await producer.createBatch();
batch.tryAdd({ body: message });
await producer.sendBatch(batch);
context.log(`Message sent to Event Hubs: ${message}`);
} catch (err) {
context.log.error("Failed to send message to Event Hubs:", err);
throw err;
} finally {
await producer.close();
}
},
});
app.storageQueue('helloQueueStart', {
queueName: 'start-orchestration',
extraInputs: [df.input.durableClient()],
handler: async (message, context) => {
const client = df.getClient(context);
const orchestratorName = message.orchestratorName || 'helloOrchestrator';
const input = message.input || null;
const instanceId = await client.startNew(orchestratorName, { input });
context.log(`Started orchestration with ID = '${instanceId}'`);
},
});
```


## Orchestration client

You can use the orchestration client binding to write functions that interact with orchestrator functions. These functions are often referred to as [client functions](durable-functions-types-features-overview#client-functions). For example, you can act on orchestration instances in the following ways:

- Start them.
- Query their status.
- Terminate them.
- Send events to them while they're running.
- Purge the instance history.

You can bind to an orchestration client by using the [DurableClientAttribute](/en-us/dotnet/api/microsoft.azure.webjobs.extensions.durabletask.durableclientattribute) attribute ([OrchestrationClientAttribute](/en-us/previous-versions/dotnet/api/microsoft.azure.webjobs.orchestrationclientattribute) in Durable Functions 1.x).

You can bind to an orchestration client by using the `@DurableClientInput`

annotation.

To register your client function, you import the `app`

object from the `@azure/functions npm`

module. Then you call a Durable Functions API method that's specific to your trigger type. For instance, for an HTTP trigger, you call the `app.http`

method. For a queue trigger, you call the `app.storageQueue`

method.

To define the durable client trigger, you use the following JSON object in the `bindings`

array of *function.json*:

```
{
"name": "<name-of-input-parameter-in-function-signature>",
"taskHub": "<optional-name-of-task-hub>",
"connectionName": "<optional-name-of-connection-string-app-setting>",
"type": "orchestrationClient",
"direction": "in"
}
```


- The
`taskHub`

property is used when multiple function apps share the same storage account but need to be isolated from each other. If you don't specify this property, the default value from*host.json*is used. This value must match the value that the target orchestrator functions use. - The
`connectionName`

value is the name of an app setting that contains a storage account connection string. The storage account represented by this connection string must be the same one that the target orchestrator functions use. If you don't specify this property, the default storage account connection string for the function app is used.

Note

In most cases, we recommend that you omit these properties and rely on the default behavior.

You can define a durable client trigger by using the `durable_client_input`

decorator directly in your Python function code.

### Client usage

You typically bind to an implementation of [IDurableClient](/en-us/dotnet/api/microsoft.azure.webjobs.extensions.durabletask.idurableclient) ([DurableOrchestrationClient](/en-us/previous-versions/dotnet/api/microsoft.azure.webjobs.durableorchestrationclient) in Durable Functions 1.x), which gives you full access to all orchestration client APIs that Durable Functions supports.

You typically bind to the `DurableClientContext`

class.

You must use the language-specific SDK to get access to a client object.

The following code provides an example of a queue-triggered function that starts a *Hello World* orchestration.

```
[FunctionName("QueueStart")]
public static Task Run(
[QueueTrigger("durable-function-trigger")] string input,
[DurableClient] IDurableOrchestrationClient starter)
{
// Orchestration input comes from the queue message content.
return starter.StartNewAsync<string>("HelloWorld", input);
}
```


Note

The preceding C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use the `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see [Durable Functions versions overview](durable-functions-versions).

```
const { app } = require('@azure/functions');
const df = require('durable-functions');
app.storageQueue('helloQueueStart', {
queueName: 'start-orchestration',
extraInputs: [df.input.durableClient()],
handler: async (message, context) => {
const client = df.getClient(context);
const orchestratorName = message.orchestratorName || 'helloOrchestrator';
const input = message.input || null;
const instanceId = await client.startNew(orchestratorName, { input });
context.log(`Started orchestration with ID = '${instanceId}' from queue message.`);
},
});
```


```
import azure.functions as func
import azure.durable_functions as df
myApp = df.DFApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@myApp.queue_trigger(
arg_name="msg",
queue_name="start-orchestration",
connection="AzureWebJobsStorage"
)
@myApp.durable_client_input(client_name="client")
async def client_function(msg: func.QueueMessage, client: df.DurableOrchestrationClient):
input_data = msg.get_body().decode("utf-8")
await client.start_new("my_orchestrator", None, input_data)
return None
```


**function.json**

```
{
"bindings": [
{
"name": "InputData",
"type": "queueTrigger",
"queueName": "durable-function-trigger",
"direction": "in"
},
{
"name": "starter",
"type": "durableClient",
"direction": "in"
}
]
}
```


**run.ps1**

```
param([string]$InputData, $TriggerMetadata)
$InstanceId = Start-DurableOrchestration -FunctionName 'HelloWorld' -Input $InputData
```


```
@FunctionName("QueueStart")
public void queueStart(
@QueueTrigger(name = "input", queueName = "durable-function-trigger", connection = "Storage") String input,
@DurableClientInput(name = "durableContext") DurableClientContext durableContext) {
// Orchestration input comes from the queue message content.
durableContext.getClient().scheduleNewOrchestrationInstance("HelloWorld", input);
}
```


For detailed information about starting instances, see [Manage instances in Durable Functions in Azure](durable-functions-instance-management).

## Entity trigger

You can use the entity trigger to develop an [entity function](durable-functions-entities). This trigger supports processing events for a specific entity instance.

Note

Entity triggers are available starting in Durable Functions 2.x.

Internally, this trigger binding polls the configured durable store for new entity operations that need to be executed.

You use the [EntityTriggerAttribute](/en-us/dotnet/api/microsoft.azure.webjobs.extensions.durabletask.entitytriggerattribute) .NET attribute to configure the entity trigger.

To register the entity trigger, you import the `app`

object from the `@azure/functions npm`

module. Then you call the `app.entity`

method of the Durable Functions API directly in your function code.

```
const df = require('durable-functions');
df.app.entity('counter', (context) => {
const currentValue = context.df.getState(() => 0);
switch (context.df.operationName) {
case 'add':
context.df.setState(currentValue + context.df.getInput());
break;
case 'reset':
context.df.setState(0);
break;
case 'get':
context.df.return(currentValue);
break;
}
});
```


Note

Entity triggers aren't yet supported for Java.

Note

Entity triggers aren't yet supported for PowerShell.

You can define an entity trigger by using the `entity_trigger`

decorator directly in your Python function code.

### Trigger behavior

Here are some notes about the entity trigger:

**Single-threading**: A single dispatcher thread is used to process operations for a particular entity. If multiple messages are sent to a single entity concurrently, the operations are processed one at a time.**Poison-message handling**: There's no support for poison messages in entity triggers.**Message visibility**: Entity trigger messages are dequeued and kept invisible for a configurable duration. The visibility of these messages is renewed automatically as long as the function app is running and healthy.**Return values**: Entity functions don't support return values. There are specific APIs that you can use to save state or pass values back to orchestrations.

Any state changes made to an entity during its execution are automatically persisted after execution is complete.

For more information and examples of defining and interacting with entity triggers, see [Entity functions](durable-functions-entities).

## Entity client

You can use the entity client binding to asynchronously trigger [entity functions](#entity-trigger). These functions are sometimes referred to as [client functions](durable-functions-types-features-overview#client-functions).

You can bind to the entity client by using the [DurableClientAttribute](/en-us/dotnet/api/microsoft.azure.webjobs.extensions.durabletask.durableclientattribute) .NET attribute in .NET class library functions.

Note

You can also use the `[DurableClientAttribute]`

to bind to the [orchestration client](#orchestration-client).

Instead of registering an entity client, you use `signalEntity`

or `callEntity`

to call an entity trigger method from any registered function.

From a queue-triggered function, you can use

`client.signalEntity`

:`const { app } = require('@azure/functions'); const df = require('durable-functions'); app.storageQueue('helloQueueStart', { queueName: 'start-orchestration', extraInputs: [df.input.durableClient()], handler: async (message, context) => { const client = df.getClient(context); const entityId = new df.EntityId('counter', 'myCounter'); await client.signalEntity(entityId, 'add', 5); }, });`

From an orchestrator function, you can use

`context.df.callEntity`

:`const { app } = require('@azure/functions'); const df = require('durable-functions'); df.app.orchestration('entityCaller', function* (context) { const entityId = new df.EntityId('counter', 'myCounter'); yield context.df.callEntity(entityId, 'add', 5); yield context.df.callEntity(entityId, 'add', 5); const result = yield context.df.callEntity(entityId, 'get'); return result; });`


You can define an entity client by using the `durable_client_input`

decorator directly in your Python function code.

Note

Entity clients aren't yet supported for Java.

Note

Entity clients aren't yet supported for PowerShell.

For more information and examples of interacting with entities as a client, see [Access entities](durable-functions-entities#access-entities).

## Durable Functions settings in host.json

This section provides information about the Durable Functions configuration properties in *host.json*. For information about general settings in *host.json*, see [host.json reference for Azure Functions 1.x](../functions-host-json-v1) or [host.json reference for Azure Functions 2.x and later](../functions-host-json).

Configuration settings for [Durable Functions](durable-functions-overview).

Note

All major versions of Durable Functions are supported on all versions of the Azure Functions runtime. However, the schema of the *host.json* configuration differs slightly depending on the version of the Azure Functions runtime and the version of the Durable Functions extension that you use.

The following code provides two examples of `durableTask`

settings in *host.json*: one for Durable Functions 2.x and one for Durable Functions 1.x. You can use both examples with Azure Functions 2.0 and 3.0. With Azure Functions 1.0, the available settings are the same, but the `durableTask`

section of *host.json* is located in the root of the *host.json* configuration instead of being a field under `extensions`

.

```
{
"extensions": {
"durableTask": {
"hubName": "MyTaskHub",
"defaultVersion": "1.0",
"versionMatchStrategy": "CurrentOrOlder",
"versionFailureStrategy": "Reject",
"storageProvider": {
"connectionStringName": "AzureWebJobsStorage",
"controlQueueBatchSize": 32,
"controlQueueBufferThreshold": 256,
"controlQueueVisibilityTimeout": "00:05:00",
"FetchLargeMessagesAutomatically": true,
"maxQueuePollingInterval": "00:00:30",
"partitionCount": 4,
"trackingStoreConnectionStringName": "TrackingStorage",
"trackingStoreNamePrefix": "DurableTask",
"useLegacyPartitionManagement": false,
"useTablePartitionManagement": true,
"workItemQueueVisibilityTimeout": "00:05:00",
"QueueClientMessageEncoding": "UTF8"
},
"tracing": {
"traceInputsAndOutputs": false,
"traceReplayEvents": false,
},
"httpSettings":{
"defaultAsyncRequestSleepTimeMilliseconds": 30000,
"useForwardedHost": false,
},
"notifications": {
"eventGrid": {
"topicEndpoint": "https://topic_name.westus2-1.eventgrid.azure.net/api/events",
"keySettingName": "EventGridKey",
"publishRetryCount": 3,
"publishRetryInterval": "00:00:30",
"publishEventTypes": [
"Started",
"Completed",
"Failed",
"Terminated"
]
}
},
"maxConcurrentActivityFunctions": 10,
"maxConcurrentOrchestratorFunctions": 10,
"maxConcurrentEntityFunctions": 10,
"extendedSessionsEnabled": false,
"extendedSessionIdleTimeoutInSeconds": 30,
"useAppLease": true,
"useGracefulShutdown": false,
"maxEntityOperationBatchSize": 50,
"maxOrchestrationActions": 100000,
"storeInputsInOrchestrationHistory": false
}
}
}
```


| Property | Default value | Description |
|---|---|---|
| hubName | TestHubName (DurableFunctionsHub in v1.x) | The name of the hub that stores the current state of a function app. Task hub names must start with a letter and consist of only letters and numbers. If you don't specify a name, the default value is used. Alternate task hub names can be used to isolate multiple Durable Functions applications from each other, even if they use the same storage back end. For more information, see
|

[orchestration versioning](durable-functions-orchestration-versioning)feature to enable scenarios like zero-downtime deployments with breaking changes. You can use any string value for the version.`None`

, `Strict`

, and `CurrentOrOlder`

. For detailed explanations, see [Orchestration versioning](durable-functions-orchestration-versioning).`defaultVersion`

value. Valid values are `Reject`

and `Fail`

. For detailed explanations, see [Orchestration versioning](durable-functions-orchestration-versioning).**Consumption plan for Python**: 32**Consumption plan for other languages**: 128**Dedicated or Premium plan**: 256*hh:mm:ss*format.*hh:mm:ss*format.`true`

, large messages that exceed the queue size limit are retrieved. When this setting is `false`

, a blob URL that points to each large message is retrieved.**Consumption plan**: 10**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine[durable task scheduler](durable-task-scheduler/durable-task-scheduler). Otherwise, the maximum number of concurrent entity executions is limited to the`maxConcurrentOrchestratorFunctions`

value.*hh:mm:ss*format. Higher values can result in higher message processing latencies. Lower values can result in higher storage costs because of increased storage transactions.connectionStringName (v2.x)

azureStorageConnectionStringName (v1.x)

trackingStoreConnectionStringName

`connectionStringName`

value (v2.x) or `azureStorageConnectionStringName`

value (v1.x) connection is used.`trackingStoreConnectionStringName`

is specified. If you don't specify a prefix, the default value of `DurableTask`

is used. If `trackingStoreConnectionStringName`

isn't specified, the History and Instances tables use the `hubName`

value as their prefix, and the `trackingStoreNamePrefix`

setting is ignored.`true`

, the entire contents of function inputs and outputs are logged.`EventGridTopicEndpoint`

URL.*hh:mm:ss*format.`Started`

, `Completed`

, `Failed`

, and `Terminated`

.`extendedSessionsEnabled`

setting is `true`

.[Disaster recovery and geo-distribution in Durable Functions](durable-functions-disaster-recovery-geo-distribution). This setting is available starting in v2.3.0.`false`

, an algorithm is used that reduces the possibility of duplicate function execution when scaling out. This setting is available starting in v2.3.0. **Setting this value to**.`true`

isn't recommendedIn v2.x: false

`true`

, an algorithm is used that's designed to reduce costs for Azure Storage v2 accounts. This setting is available starting in WebJobs.Extensions.DurableTask v2.10.0. Using this setting with a managed identity requires WebJobs.Extensions.DurableTask v3.x or later, or Worker.Extensions.DurableTask v1.2.x or later.**Consumption plan**: 50**Dedicated or Premium plan**: 5,000[batch](durable-functions-perf-and-scale#entity-operation-batching). If this value is 1, batching is disabled, and a separate function invocation processes each operation message. This setting is available starting in v2.6.1.`true`

, the Durable Task Framework saves activity inputs in the History table, and activity function inputs appear in orchestration history query results.`DurableTaskClient`

uses the gRPC client to manage orchestration instances. This setting applies to Durable Functions .NET isolated worker and Java apps.*hh:mm:ss*format for the HTTP client used by the gRPC client in Durable Functions. The client is currently supported for .NET isolated worker apps (.NET 6 and later versions) and for Java apps.Many of these settings are for optimizing performance. For more information, see [Performance and scale](durable-functions-perf-and-scale).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-http-api -->

# HTTP API reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Durable Functions extension exposes a set of built-in HTTP APIs that can be used to perform management tasks on [orchestrations](durable-functions-types-features-overview#orchestrator-functions), [entities](durable-functions-types-features-overview#entity-functions), and [task hubs](durable-functions-task-hubs). These HTTP APIs are extensibility webhooks that are authorized by the Azure Functions host but handled directly by the Durable Functions extension.

The base URL for the APIs mentioned in this article is the same as the base URL for your function app. When developing locally using the [Azure Functions Core Tools](../functions-run-local), the base URL is typically `http://localhost:7071`

. In the Azure Functions hosted service, the base URL is typically `https://{appName}.azurewebsites.net`

. Custom hostnames are also supported if configured on your App Service app.

All HTTP APIs implemented by the extension require the following parameters. The data type of all parameters is `string`

.

| Parameter | Parameter Type | Description |
|---|---|---|
`taskHub` |
Query string | The name of the
|

`connection`

**name**of the connection app setting for the backend storage provider. If not specified, the default connection configuration for the function app is assumed.`systemKey`

`systemKey`

is an authorization key autogenerated by the Azure Functions host. It specifically grants access to the Durable Task extension APIs and can be managed the same way as [other Azure Functions access keys](../security-concepts#function-access-keys). You can generate URLs that contain the correct `taskHub`

, `connection`

, and `systemKey`

query string values using [orchestration client binding](durable-functions-bindings#orchestration-client) APIs, such as the `CreateCheckStatusResponse`

and `CreateHttpManagementPayload`

APIs in .NET, the `createCheckStatusResponse`

and `createHttpManagementPayload`

APIs in JavaScript, etc.

The next few sections cover the specific HTTP APIs supported by the extension and provide examples of how they can be used.

## Start orchestration

Starts executing a new instance of the specified orchestrator function.

### Request

For version 1.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
POST /admin/extensions/DurableTaskExtension/orchestrators/{functionName}/{instanceId?}
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
```


In version 2.x of the Functions runtime, the URL format has all the same parameters but with a slightly different prefix:

```
POST /runtime/webhooks/durabletask/orchestrators/{functionName}/{instanceId?}
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameters:

| Field | Parameter type | Description |
|---|---|---|
`functionName` |
URL | The name of the orchestrator function to start. |
`instanceId` |
URL | Optional parameter. The ID of the orchestration instance. If not specified, the orchestrator function will start with a random instance ID. |
`{content}` |
Request content | Optional. The JSON-formatted orchestrator function input. |

### Response

Several possible status code values can be returned.

**HTTP 202 (Accepted)**: The specified orchestrator function was scheduled to start running. The`Location`

response header contains a URL for polling the orchestration status.**HTTP 400 (Bad request)**: The specified orchestrator function doesn't exist, the specified instance ID was not valid, or request content was not valid JSON.

The following is an example request that starts a `RestartVMs`

orchestrator function and includes JSON object payload:

```
POST /runtime/webhooks/durabletask/orchestrators/RestartVMs?code=XXX
Content-Type: application/json
Content-Length: 83
{
"resourceGroup": "myRG",
"subscriptionId": "aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e"
}
```


The response payload for the **HTTP 202** cases is a JSON object with the following fields:

| Field | Description |
|---|---|
`id` |
The ID of the orchestration instance. |
`statusQueryGetUri` |
The status URL of the orchestration instance. |
`sendEventPostUri` |
The "raise event" URL of the orchestration instance. |
`terminatePostUri` |
The "terminate" URL of the orchestration instance. |
`purgeHistoryDeleteUri` |
The "purge history" URL of the orchestration instance. |
`rewindPostUri` |
(preview) The "rewind" URL of the orchestration instance. |
`suspendPostUri` |
The "suspend" URL of the orchestration instance. |
`resumePostUri` |
The "resume" URL of the orchestration instance. |

The data type of all fields is `string`

.

Here is an example response payload for an orchestration instance with `abc123`

as its ID (formatted for readability):

```
{
"id": "abc123",
"purgeHistoryDeleteUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123?code=XXX",
"sendEventPostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123/raiseEvent/{eventName}?code=XXX",
"statusQueryGetUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123?code=XXX",
"terminatePostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123/terminate?reason={text}&code=XXX",
"suspendPostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123/suspend?reason={text}&code=XXX",
"resumePostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/abc123/resume?reason={text}&code=XXX"
}
```


The HTTP response is intended to be compatible with the *Polling Consumer Pattern*. It also includes the following notable response headers:

**Location**: The URL of the status endpoint. This URL contains the same value as the`statusQueryGetUri`

field.**Retry-After**: The number of seconds to wait between polling operations. The default value is`10`

.

For more information on the asynchronous HTTP polling pattern, see the [HTTP async operation tracking](durable-functions-http-features#async-operation-tracking) documentation.

## Get instance status

Gets the status of a specified orchestration instance.

### Request

For version 1.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
GET /admin/extensions/DurableTaskExtension/instances/{instanceId}
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&showHistory=[true|false]
&showHistoryOutput=[true|false]
&showInput=[true|false]
&returnInternalServerErrorOnFailure=[true|false]
```


In version 2.x of the Functions runtime, the URL format has all the same parameters but with a slightly different prefix:

```
GET /runtime/webhooks/durabletask/instances/{instanceId}
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&showHistory=[true|false]
&showHistoryOutput=[true|false]
&showInput=[true|false]
&returnInternalServerErrorOnFailure=[true|false]
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameters:

| Field | Parameter type | Description |
|---|---|---|
`instanceId` |
URL | The ID of the orchestration instance. |
`showInput` |
Query string | Optional parameter. If set to `false` , the function input will not be included in the response payload. |
`showHistory` |
Query string | Optional parameter. If set to `true` , the orchestration execution history will be included in the response payload. |
`showHistoryOutput` |
Query string | Optional parameter. If set to `true` , the function outputs will be included in the orchestration execution history. |
`createdTimeFrom` |
Query string | Optional parameter. When specified, filters the list of returned instances that were created at or after the given ISO8601 timestamp. |
`createdTimeTo` |
Query string | Optional parameter. When specified, filters the list of returned instances that were created at or before the given ISO8601 timestamp. |
`runtimeStatus` |
Query string | Optional parameter. When specified, filters the list of returned instances based on their runtime status. To see the list of possible runtime status values, see the
|

`returnInternalServerErrorOnFailure`

`true`

, this API will return an HTTP 500 response instead of a 200 if the instance is in a failure state. This parameter is intended for automated status polling scenarios.### Response

Several possible status code values can be returned.

**HTTP 200 (OK)**: The specified instance is in a completed or failed state.**HTTP 202 (Accepted)**: The specified instance is in progress.**HTTP 400 (Bad Request)**: The specified instance failed or was terminated.**HTTP 404 (Not Found)**: The specified instance doesn't exist or has not started running.**HTTP 500 (Internal Server Error)**: Returned only when the`returnInternalServerErrorOnFailure`

is set to`true`

and the specified instance failed with an unhandled exception.

The response payload for the **HTTP 200** and **HTTP 202** cases is a JSON object with the following fields:

| Field | Data type | Description |
|---|---|---|
`runtimeStatus` |
string | The runtime status of the instance. Values include Running, Pending, Failed, Canceled, Terminated, Completed, Suspended. |
`input` |
JSON | The JSON data used to initialize the instance. This field is `null` if the `showInput` query string parameter is set to `false` . |
`customStatus` |
JSON | The JSON data used for custom orchestration status. This field is `null` if not set. |
`output` |
JSON | The JSON output of the instance. This field is `null` if the instance is not in a completed state. |
`createdTime` |
string | The time at which the instance was created. Uses ISO 8601 extended notation. |
`lastUpdatedTime` |
string | The time at which the instance last persisted. Uses ISO 8601 extended notation. |
`historyEvents` |
JSON | A JSON array containing the orchestration execution history. This field is `null` unless the `showHistory` query string parameter is set to `true` . |

Here is an example response payload including the orchestration execution history and activity outputs (formatted for readability):

```
{
"createdTime": "2018-02-28T05:18:49Z",
"historyEvents": [
{
"EventType": "ExecutionStarted",
"FunctionName": "E1_HelloSequence",
"Timestamp": "2018-02-28T05:18:49.3452372Z"
},
{
"EventType": "TaskCompleted",
"FunctionName": "E1_SayHello",
"Result": "Hello Tokyo!",
"ScheduledTime": "2018-02-28T05:18:51.3939873Z",
"Timestamp": "2018-02-28T05:18:52.2895622Z"
},
{
"EventType": "TaskCompleted",
"FunctionName": "E1_SayHello",
"Result": "Hello Seattle!",
"ScheduledTime": "2018-02-28T05:18:52.8755705Z",
"Timestamp": "2018-02-28T05:18:53.1765771Z"
},
{
"EventType": "TaskCompleted",
"FunctionName": "E1_SayHello",
"Result": "Hello London!",
"ScheduledTime": "2018-02-28T05:18:53.5170791Z",
"Timestamp": "2018-02-28T05:18:53.891081Z"
},
{
"EventType": "ExecutionCompleted",
"OrchestrationStatus": "Completed",
"Result": [
"Hello Tokyo!",
"Hello Seattle!",
"Hello London!"
],
"Timestamp": "2018-02-28T05:18:54.3660895Z"
}
],
"input": null,
"customStatus": { "nextActions": ["A", "B", "C"], "foo": 2 },
"lastUpdatedTime": "2018-02-28T05:18:54Z",
"output": [
"Hello Tokyo!",
"Hello Seattle!",
"Hello London!"
],
"runtimeStatus": "Completed"
}
```


The **HTTP 202** response also includes a **Location** response header that references the same URL as the `statusQueryGetUri`

field mentioned previously.

## Get all instances status

You can also query the status of all instances by removing the `instanceId`

from the 'Get instance status' request. In this case, the basic parameters are the same as the 'Get instance status'. Query string parameters for filtering are also supported.

### Request

For version 1.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
GET /admin/extensions/DurableTaskExtension/instances
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&createdTimeFrom={timestamp}
&createdTimeTo={timestamp}
&runtimeStatus={runtimeStatus1,runtimeStatus2,...}
&instanceIdPrefix={prefix}
&showInput=[true|false]
&top={integer}
```


In version 2.x of the Functions runtime, the URL format has all the same parameters but with a slightly different prefix:

```
GET /runtime/webhooks/durableTask/instances?
taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&createdTimeFrom={timestamp}
&createdTimeTo={timestamp}
&runtimeStatus={runtimeStatus1,runtimeStatus2,...}
&instanceIdPrefix={prefix}
&showInput=[true|false]
&top={integer}
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameters:

| Field | Parameter type | Description |
|---|---|---|
`showInput` |
Query string | Optional parameter. If set to `false` , the function input will not be included in the response payload. |
`showHistoryOutput` |
Query string | Optional parameter. If set to `true` , the function outputs will be included in the orchestration execution history. |
`createdTimeFrom` |
Query string | Optional parameter. When specified, filters the list of returned instances that were created at or after the given ISO8601 timestamp. |
`createdTimeTo` |
Query string | Optional parameter. When specified, filters the list of returned instances that were created at or before the given ISO8601 timestamp. |
`runtimeStatus` |
Query string | Optional parameter. When specified, filters the list of returned instances based on their runtime status. To see the list of possible runtime status values, see the
|

`instanceIdPrefix`

[version 2.7.2](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask/2.7.2)of the extension.`top`

### Response

Here is an example of response payloads including the orchestration status (formatted for readability):

```
[
{
"instanceId": "7af46ff000564c65aafbfe99d07c32a5",
"runtimeStatus": "Completed",
"input": null,
"customStatus": null,
"output": [
"Hello Tokyo!",
"Hello Seattle!",
"Hello London!"
],
"createdTime": "2018-06-04T10:46:39Z",
"lastUpdatedTime": "2018-06-04T10:46:47Z"
},
{
"instanceId": "80eb7dd5c22f4eeba9f42b062794321e",
"runtimeStatus": "Running",
"input": null,
"customStatus": null,
"output": null,
"createdTime": "2018-06-04T15:18:28Z",
"lastUpdatedTime": "2018-06-04T15:18:38Z"
},
{
"instanceId": "9124518926db408ab8dfe84822aba2b1",
"runtimeStatus": "Completed",
"input": null,
"customStatus": null,
"output": [
"Hello Tokyo!",
"Hello Seattle!",
"Hello London!"
],
"createdTime": "2018-06-04T10:46:54Z",
"lastUpdatedTime": "2018-06-04T10:47:03Z"
},
{
"instanceId": "d100b90b903c4009ba1a90868331b11b",
"runtimeStatus": "Pending",
"input": null,
"customStatus": null,
"output": null,
"createdTime": "2018-06-04T15:18:39Z",
"lastUpdatedTime": "2018-06-04T15:18:39Z"
}
]
```


Note

This operation can be very expensive in terms of Azure Storage I/O if you are using the [default Azure Storage provider](durable-functions-storage-providers#azure-storage) and if there are a lot of rows in the Instances table. More details on Instance table can be found in the [Azure Storage provider](durable-functions-azure-storage-provider#instances-table) documentation.

If more results exist, a continuation token is returned in the response header. The name of the header is `x-ms-continuation-token`

.

Caution

The query result may return fewer items than the limit specified by `top`

. When receiving results, you should therefore *always* check to see if there is a continuation token.

If you set continuation token value in the next request header, you can get the next page of results. This name of the request header is also `x-ms-continuation-token`

.

## Purge single instance history

Deletes the history and related artifacts for a specified orchestration instance.

### Request

For version 1.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
DELETE /admin/extensions/DurableTaskExtension/instances/{instanceId}
?taskHub={taskHub}
&connection={connection}
&code={systemKey}
```


In version 2.x of the Functions runtime, the URL format has all the same parameters but with a slightly different prefix:

```
DELETE /runtime/webhooks/durabletask/instances/{instanceId}
?taskHub={taskHub}
&connection={connection}
&code={systemKey}
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameters:

| Field | Parameter type | Description |
|---|---|---|
`instanceId` |
URL | The ID of the orchestration instance. |

### Response

The following HTTP status code values can be returned.

**HTTP 200 (OK)**: The instance history has been purged successfully.**HTTP 404 (Not Found)**: The specified instance doesn't exist.

The response payload for the **HTTP 200** case is a JSON object with the following field:

| Field | Data type | Description |
|---|---|---|
`instancesDeleted` |
integer | The number of instances deleted. For the single instance case, this value should always be `1` . |

Here is an example response payload (formatted for readability):

```
{
"instancesDeleted": 1
}
```


## Purge multiple instance histories

You can also delete the history and related artifacts for multiple instances within a task hub by removing the `{instanceId}`

from the 'Purge single instance history' request. To selectively purge instance history, use the same filters described in the 'Get all instances status' request.

### Request

For version 1.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
DELETE /admin/extensions/DurableTaskExtension/instances
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&createdTimeFrom={timestamp}
&createdTimeTo={timestamp}
&runtimeStatus={runtimeStatus1,runtimeStatus2,...}
```


In version 2.x of the Functions runtime, the URL format has all the same parameters but with a slightly different prefix:

```
DELETE /runtime/webhooks/durabletask/instances
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&createdTimeFrom={timestamp}
&createdTimeTo={timestamp}
&runtimeStatus={runtimeStatus1,runtimeStatus2,...}
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameters:

| Field | Parameter type | Description |
|---|---|---|
`createdTimeFrom` |
Query string | Filters the list of purged instances that were created at or after the given ISO8601 timestamp. |
`createdTimeTo` |
Query string | Optional parameter. When specified, filters the list of purged instances that were created at or before the given ISO8601 timestamp. |
`runtimeStatus` |
Query string | Optional parameter. When specified, filters the list of purged instances based on their runtime status. To see the list of possible runtime status values, see the
|

Note

This operation can be very expensive in terms of Azure Storage I/O if you are using the [default Azure Storage provider](durable-functions-storage-providers#azure-storage) and if there are many rows in the Instances and/or History tables. More details on these tables can be found in the [Performance and scale in Durable Functions (Azure Functions)](durable-functions-azure-storage-provider#instances-table) documentation.

### Response

The following HTTP status code values can be returned.

**HTTP 200 (OK)**: The instance history has been purged successfully.**HTTP 404 (Not Found)**: No instances were found that match the filter expression.

The response payload for the **HTTP 200** case is a JSON object with the following field:

| Field | Data type | Description |
|---|---|---|
`instancesDeleted` |
integer | The number of instances deleted. |

Here is an example response payload (formatted for readability):

```
{
"instancesDeleted": 250
}
```


## Raise event

Sends an event notification message to a running orchestration instance.

### Request

For version 1.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
POST /admin/extensions/DurableTaskExtension/instances/{instanceId}/raiseEvent/{eventName}
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
```


In version 2.x of the Functions runtime, the URL format has all the same parameters but with a slightly different prefix:

```
POST /runtime/webhooks/durabletask/instances/{instanceId}/raiseEvent/{eventName}
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameters:

| Field | Parameter type | Description |
|---|---|---|
`instanceId` |
URL | The ID of the orchestration instance. |
`eventName` |
URL | The name of the event that the target orchestration instance is waiting on. |
`{content}` |
Request content | The JSON-formatted event payload. |

### Response

Several possible status code values can be returned.

**HTTP 202 (Accepted)**: The raised event was accepted for processing.**HTTP 400 (Bad request)**: The request content was not of type`application/json`

or was not valid JSON.**HTTP 404 (Not Found)**: The specified instance was not found.**HTTP 410 (Gone)**: The specified instance has completed or failed and cannot process any raised events.

Here is an example request that sends the JSON string `"incr"`

to an instance waiting for an event named **operation**:

```
POST /admin/extensions/DurableTaskExtension/instances/bcf6fb5067b046fbb021b52ba7deae5a/raiseEvent/operation?taskHub=DurableFunctionsHub&connection=Storage&code=XXX
Content-Type: application/json
Content-Length: 6
"incr"
```


The responses for this API do not contain any content.

## Terminate instance

Terminates a running orchestration instance.

### Request

For version 1.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
POST /admin/extensions/DurableTaskExtension/instances/{instanceId}/terminate
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&reason={text}
```


In version 2.x of the Functions runtime, the URL format has all the same parameters but with a slightly different prefix:

```
POST /runtime/webhooks/durabletask/instances/{instanceId}/terminate
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&reason={text}
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameter.

| Field | Parameter Type | Description |
|---|---|---|
`instanceId` |
URL | The ID of the orchestration instance. |
`reason` |
Query string | Optional. The reason for terminating the orchestration instance. |

### Response

Several possible status code values can be returned.

**HTTP 202 (Accepted)**: The terminate request was accepted for processing.**HTTP 404 (Not Found)**: The specified instance was not found.**HTTP 410 (Gone)**: The specified instance has completed or failed.

Here is an example request that terminates a running instance and specifies a reason of **buggy**:

```
POST /admin/extensions/DurableTaskExtension/instances/bcf6fb5067b046fbb021b52ba7deae5a/terminate?reason=buggy&taskHub=DurableFunctionsHub&connection=Storage&code=XXX
```


The responses for this API do not contain any content.

## Suspend instance

Suspends a running orchestration instance.

### Request

In version 2.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
POST /runtime/webhooks/durabletask/instances/{instanceId}/suspend
?reason={text}
&taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
```


| Field | Parameter Type | Description |
|---|---|---|
`instanceId` |
URL | The ID of the orchestration instance. |
`reason` |
Query string | Optional. The reason for suspending the orchestration instance. |

Several possible status code values can be returned.

**HTTP 202 (Accepted)**: The suspend request was accepted for processing.**HTTP 404 (Not Found)**: The specified instance was not found.**HTTP 410 (Gone)**: The specified instance has completed, failed, or terminated.

The responses for this API do not contain any content.

## Resume instance

Resumes a suspended orchestration instance.

### Request

In version 2.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
POST /runtime/webhooks/durabletask/instances/{instanceId}/resume
?reason={text}
&taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
```


| Field | Parameter Type | Description |
|---|---|---|
`instanceId` |
URL | The ID of the orchestration instance. |
`reason` |
Query string | Optional. The reason for resuming the orchestration instance. |

Several possible status code values can be returned.

**HTTP 202 (Accepted)**: The resume request was accepted for processing.**HTTP 404 (Not Found)**: The specified instance was not found.**HTTP 410 (Gone)**: The specified instance has completed, failed, or terminated.

The responses for this API do not contain any content.

## Rewind instance (preview)

Restores a failed orchestration instance into a running state by replaying the most recent failed operations.

### Request

For version 1.x of the Functions runtime, the request is formatted as follows (multiple lines are shown for clarity):

```
POST /admin/extensions/DurableTaskExtension/instances/{instanceId}/rewind
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&reason={text}
```


In version 2.x of the Functions runtime, the URL format has all the same parameters but with a slightly different prefix:

```
POST /runtime/webhooks/durabletask/instances/{instanceId}/rewind
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&reason={text}
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameter.

| Field | Parameter Type | Description |
|---|---|---|
`instanceId` |
URL | The ID of the orchestration instance. |
`reason` |
Query string | Optional. The reason for rewinding the orchestration instance. |

### Response

Several possible status code values can be returned.

**HTTP 202 (Accepted)**: The rewind request was accepted for processing.**HTTP 404 (Not Found)**: The specified instance was not found.**HTTP 410 (Gone)**: The specified instance has completed or was terminated.

Here is an example request that rewinds a failed instance and specifies a reason of **fixed**:

```
POST /admin/extensions/DurableTaskExtension/instances/bcf6fb5067b046fbb021b52ba7deae5a/rewind?reason=fixed&taskHub=DurableFunctionsHub&connection=Storage&code=XXX
```


The responses for this API do not contain any content.

## Signal entity

Sends a one-way operation message to a [Durable Entity](durable-functions-types-features-overview#entity-functions). If the entity doesn't exist, it will be created automatically.

Note

Durable entities are available starting in Durable Functions 2.0.

### Request

The HTTP request is formatted as follows (multiple lines are shown for clarity):

```
POST /runtime/webhooks/durabletask/entities/{entityName}/{entityKey}
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&op={operationName}
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameters:

| Field | Parameter type | Description |
|---|---|---|
`entityName` |
URL | The name (type) of the entity. |
`entityKey` |
URL | The key (unique ID) of the entity. |
`op` |
Query string | Optional. The name of the user-defined operation to invoke. |
`{content}` |
Request content | The JSON-formatted event payload. |

Here is an example request that sends a user-defined "Add" message to a `Counter`

entity named `steps`

. The content of the message is the value `5`

. If the entity does not already exist, it will be created by this request:

```
POST /runtime/webhooks/durabletask/entities/Counter/steps?op=Add
Content-Type: application/json
5
```


Note

By default with [class-based entities in .NET](durable-functions-dotnet-entities#defining-entity-classes), specifying the `op`

value of `delete`

will delete the state of an entity. If the entity defines an operation named `delete`

, however, that user-defined operation will be invoked instead.

### Response

This operation has several possible responses:

**HTTP 202 (Accepted)**: The signal operation was accepted for asynchronous processing.**HTTP 400 (Bad request)**: The request content was not of type`application/json`

, was not valid JSON, or had an invalid`entityKey`

value.**HTTP 404 (Not Found)**: The specified`entityName`

was not found.

A successful HTTP request does not contain any content in the response. A failed HTTP request may contain JSON-formatted error information in the response content.

## Get entity

Gets the state of the specified entity.

### Request

The HTTP request is formatted as follows (multiple lines are shown for clarity):

```
GET /runtime/webhooks/durabletask/entities/{entityName}/{entityKey}
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
```


### Response

This operation has two possible responses:

**HTTP 200 (OK)**: The specified entity exists.**HTTP 404 (Not Found)**: The specified entity was not found.

A successful response contains the JSON-serialized state of the entity as its content.

### Example

The following example HTTP request gets the state of an existing `Counter`

entity named `steps`

:

```
GET /runtime/webhooks/durabletask/entities/Counter/steps
```


If the `Counter`

entity simply contained a number of steps saved in a `currentValue`

field, the response content might look like the following (formatted for readability):

```
{
"currentValue": 5
}
```


## List entities

You can query for multiple entities by the entity name or by the last operation date.

### Request

The HTTP request is formatted as follows (multiple lines are shown for clarity):

```
GET /runtime/webhooks/durabletask/entities/{entityName}
?taskHub={taskHub}
&connection={connectionName}
&code={systemKey}
&lastOperationTimeFrom={timestamp}
&lastOperationTimeTo={timestamp}
&fetchState=[true|false]
&top={integer}
```


Request parameters for this API include the default set mentioned previously as well as the following unique parameters:

| Field | Parameter type | Description |
|---|---|---|
`entityName` |
URL | Optional. When specified, filters the list of returned entities by their entity name (case-insensitive). |
`fetchState` |
Query string | Optional parameter. If set to `true` , the entity state will be included in the response payload. |
`lastOperationTimeFrom` |
Query string | Optional parameter. When specified, filters the list of returned entities that processed operations after the given ISO8601 timestamp. |
`lastOperationTimeTo` |
Query string | Optional parameter. When specified, filters the list of returned entities that processed operations before the given ISO8601 timestamp. |
`top` |
Query string | Optional parameter. When specified, limits the number of entities returned by the query. |

### Response

A successful HTTP 200 response contains a JSON-serialized array of entities and optionally the state of each entity.

By default the operation returns the first 100 entities that match the query criteria. The caller can specify a query string parameter value for `top`

to return a different maximum number of results. If more results exist beyond what is returned, a continuation token is also returned in the response header. The name of the header is `x-ms-continuation-token`

.

If you set continuation token value in the next request header, you can get the next page of results. This name of the request header is also `x-ms-continuation-token`

.

### Example - list all entities

The following example HTTP request lists all entities in the task hub:

```
GET /runtime/webhooks/durabletask/entities
```


The response JSON may look like the following (formatted for readability):

```
[
{
"entityId": { "key": "cats", "name": "counter" },
"lastOperationTime": "2019-12-18T21:45:44.6326361Z",
},
{
"entityId": { "key": "dogs", "name": "counter" },
"lastOperationTime": "2019-12-18T21:46:01.9477382Z"
},
{
"entityId": { "key": "mice", "name": "counter" },
"lastOperationTime": "2019-12-18T21:46:15.4626159Z"
},
{
"entityId": { "key": "radio", "name": "device" },
"lastOperationTime": "2019-12-18T21:46:18.2616154Z"
},
]
```


### Example - filtering the list of entities

The following example HTTP request lists just the first two entities of type `counter`

and also fetches their state:

```
GET /runtime/webhooks/durabletask/entities/counter?top=2&fetchState=true
```


The response JSON may look like the following (formatted for readability):

```
[
{
"entityId": { "key": "cats", "name": "counter" },
"lastOperationTime": "2019-12-18T21:45:44.6326361Z",
"state": { "value": 9 }
},
{
"entityId": { "key": "dogs", "name": "counter" },
"lastOperationTime": "2019-12-18T21:46:01.9477382Z",
"state": { "value": 10 }
}
]
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-instance-management -->

# Manage instances in Durable Functions in Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Orchestrations in Durable Functions are long-running stateful functions that can be started, queried, suspended, resumed, and terminated using built-in management APIs. Several other instance management APIs are also exposed by the Durable Functions [orchestration client binding](durable-functions-bindings#orchestration-client), such as sending external events to instances, purging instance history, etc. This article goes into the details of all supported instance management operations.

## Start instances

The *start-new* (or *schedule-new*) method on the [orchestration client binding](durable-functions-bindings#orchestration-client) starts a new orchestration instance. Internally, this method writes a message via the [Durable Functions storage provider](durable-functions-storage-providers) and then returns. This message asynchronously triggers the start of an [orchestration function](durable-functions-types-features-overview#orchestrator-functions) with the specified name.

The parameters for starting a new orchestration instance are as follows:

**Name**: The name of the orchestrator function to schedule.**Input**: Any JSON-serializable data that should be passed as the input to the orchestrator function.**InstanceId**: (Optional) The unique ID of the instance. If you don't specify this parameter, the method uses a random ID.

Tip

Use a random identifier for the instance ID whenever possible. Random instance IDs help ensure an equal load distribution when you're scaling orchestrator functions across multiple VMs. The proper time to use non-random instance IDs is when the ID must come from an external source, or when you're implementing the [singleton orchestrator](durable-functions-singletons) pattern.

The following code is an example function that starts a new orchestration instance:

```
[FunctionName("HelloWorldQueueTrigger")]
public static async Task Run(
[QueueTrigger("start-queue")] string input,
[DurableClient] IDurableOrchestrationClient starter,
ILogger log)
{
string instanceId = await starter.StartNewAsync("HelloWorld", input);
log.LogInformation($"Started orchestration with ID = '{instanceId}'.");
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

### Azure Functions Core Tools

You can also start an instance directly by using the [ func durable start-new command](../functions-core-tools-reference#func-durable-start-new) in Core Tools, which takes the following parameters:

: Name of the function to start.`function-name`

(required): Input to the function, either inline or through a JSON file. For files, add a prefix to the path to the file with`input`

(optional)`@`

, such as`@path/to/file.json`

.: ID of the orchestration instance. If you don't specify this parameter, the command uses a random GUID.`id`

(optional): Name of the application setting containing the storage connection string to use. The default is AzureWebJobsStorage.`connection-string-setting`

(optional): Name of the Durable Functions task hub to use. The default is DurableFunctionsHub. You can also set this in`task-hub-name`

(optional)[host.json](durable-functions-bindings#host-json)by using durableTask:HubName.

Note

Core Tools commands assume you are running them from the root directory of a function app. If you explicitly provide the `connection-string-setting`

and `task-hub-name`

parameters, you can run the commands from any directory. Although you can run these commands without a function app host running, you might find that you can't observe some effects unless the host is running. For example, the `start-new`

command enqueues a start message into the target task hub, but the orchestration doesn't actually run unless there is a function app host process running that can process the message.

Note

The Core Tools commands are currently only supported when using the default [Azure Storage provider](durable-functions-storage-providers) for persisting runtime state.

The following command starts the function named HelloWorld, and passes the contents of the file `counter-data.json`

to it:

```
func durable start-new --function-name HelloWorld --input @counter-data.json --task-hub-name TestTaskHub
```


## Query instances

After starting new orchestration instances, you'll most likely need to query their runtime status to learn whether they are running, have completed, or have failed.

The *get-status* method on the [orchestration client binding](durable-functions-bindings#orchestration-client) queries the status of an orchestration instance.

It takes an `instanceId`

(required), `showHistory`

(optional), `showHistoryOutput`

(optional), and `showInput`

(optional) as parameters.

: If set to`showHistory`

`true`

, the response contains the execution history.: If set to`showHistoryOutput`

`true`

, the execution history contains activity outputs.: If set to`showInput`

`false`

, the response won't contain the input of the function. The default value is`true`

.

The method returns an object with the following properties:

**Name**: The name of the orchestrator function.**InstanceId**: The instance ID of the orchestration (should be the same as the`instanceId`

input).**CreatedTime**: The time at which the orchestrator function started running.**LastUpdatedTime**: The time at which the orchestration last checkpointed.**Input**: The input of the function as a JSON value. This field isn't populated if`showInput`

is false.**CustomStatus**: Custom orchestration status in JSON format.**Output**: The output of the function as a JSON value (if the function has completed). If the orchestrator function failed, this property includes the failure details. If the orchestrator function was suspended or terminated, this property includes the reason for the suspension or termination (if any).**RuntimeStatus**: One of the following values:**Pending**: The instance has been scheduled but has not yet started running.**Running**: The instance has started running.**Completed**: The instance has completed normally.**ContinuedAsNew**: The instance has restarted itself with a new history. This state is a transient state.**Failed**: The instance failed with an error.**Terminated**: The instance was stopped abruptly.**Suspended**: The instance was suspended and may be resumed at a later point in time.

**History**: The execution history of the orchestration. This field is only populated if`showHistory`

is set to`true`

.

Note

An orchestrator is not marked as `Completed`

until all of its scheduled tasks have finished *and* the orchestrator has returned. In other words, it is not sufficient for an orchestrator to reach its `return`

statement for it to be marked as `Completed`

. This is particularly relevant for cases where `WhenAny`

is used; those orchestrators often `return`

before all the scheduled tasks have executed.

This method returns `null`

(.NET and Java), `undefined`

(JavaScript), or `None`

(Python) if the instance doesn't exist.

```
[FunctionName("GetStatus")]
public static async Task Run(
[DurableClient] IDurableOrchestrationClient client,
[QueueTrigger("check-status-queue")] string instanceId)
{
DurableOrchestrationStatus status = await client.GetStatusAsync(instanceId);
// do something based on the current status.
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

### Azure Functions Core Tools

It's also possible to get the status of an orchestration instance directly by using the [ func durable get-runtime-status command](../functions-core-tools-reference#func-durable-get-runtime-status) in Core Tools.

Note

Core Tools commands are currently only supported when using the default [Azure Storage provider](durable-functions-storage-providers) for persisting runtime state.

The `durable get-runtime-status`

command takes the following parameters:

: ID of the orchestration instance.`id`

(required): If set to`show-input`

(optional)`true`

, the response contains the input of the function. The default value is`false`

.: If set to`show-output`

(optional)`true`

, the response contains the output of the function. The default value is`false`

.: Name of the application setting containing the storage connection string to use. The default is`connection-string-setting`

(optional)`AzureWebJobsStorage`

.: Name of the Durable Functions task hub to use. The default is`task-hub-name`

(optional)`DurableFunctionsHub`

. It can also be set in[host.json](durable-functions-bindings#host-json), by using durableTask:HubName.

The following command retrieves the status (including input and output) of an instance with an orchestration instance ID of 0ab8c55a66644d68a3a8b220b12d209c. It assumes that you are running the `func`

command from the root directory of the function app:

```
func durable get-runtime-status --id 0ab8c55a66644d68a3a8b220b12d209c --show-input true --show-output true
```


You can use the `durable get-history`

command to retrieve the history of an orchestration instance. It takes the following parameters:

: ID of the orchestration instance.`id`

(required): Name of the application setting containing the storage connection string to use. The default is`connection-string-setting`

(optional)`AzureWebJobsStorage`

.: Name of the Durable Functions task hub to use. The default is`task-hub-name`

(optional)`DurableFunctionsHub`

. It can also be set in host.json, by using durableTask:HubName.

```
func durable get-history --id 0ab8c55a66644d68a3a8b220b12d209c
```


## Query all instances

You can use APIs in your language SDK to query the statuses of all orchestration instances in your [task hub](durable-functions-task-hubs). This *"list-instances"* or *"get-status"* API returns a list of objects that represent the orchestration instances matching the query parameters.

```
[FunctionName("GetAllStatus")]
public static async Task Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestMessage req,
[DurableClient] IDurableOrchestrationClient client,
ILogger log)
{
var noFilter = new OrchestrationStatusQueryCondition();
OrchestrationStatusQueryResult result = await client.ListInstancesAsync(
noFilter,
CancellationToken.None);
foreach (DurableOrchestrationStatus instance in result.DurableOrchestrationState)
{
log.LogInformation(JsonConvert.SerializeObject(instance));
}
// Note: ListInstancesAsync only returns the first page of results.
// To request additional pages provide the result.ContinuationToken
// to the OrchestrationStatusQueryCondition's ContinuationToken property.
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

### Azure Functions Core Tools

It's also possible to query instances directly, by using the [ func durable get-instances command](../functions-core-tools-reference#func-durable-get-instances) in Core Tools.

Note

The Core Tools commands are currently only supported when using the default [Azure Storage provider](durable-functions-storage-providers) for persisting runtime state.

The `durable get-instances`

command takes the following parameters:

: This command supports paging. This parameter corresponds to the number of instances retrieved per request. The default is 10.`top`

(optional): A token to indicate which page or section of instances to retrieve. Each`continuation-token`

(optional)`get-instances`

execution returns a token to the next set of instances.: Name of the application setting containing the storage connection string to use. The default is`connection-string-setting`

(optional)`AzureWebJobsStorage`

.: Name of the Durable Functions task hub to use. The default is`task-hub-name`

(optional)`DurableFunctionsHub`

. It can also be set in[host.json](durable-functions-bindings#host-json), by using durableTask:HubName.

```
func durable get-instances
```


## Query instances with filters

What if you don't really need all the information that a standard instance query can provide? For example, what if you're just looking for the orchestration creation time, or the orchestration runtime status? You can narrow your query by applying filters.

```
[FunctionName("QueryStatus")]
public static async Task Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestMessage req,
[DurableClient] IDurableOrchestrationClient client,
ILogger log)
{
// Get the first 100 running or pending instances that were created between 7 and 1 day(s) ago
var queryFilter = new OrchestrationStatusQueryCondition
{
RuntimeStatus = new[]
{
OrchestrationRuntimeStatus.Pending,
OrchestrationRuntimeStatus.Running,
},
CreatedTimeFrom = DateTime.UtcNow.Subtract(TimeSpan.FromDays(7)),
CreatedTimeTo = DateTime.UtcNow.Subtract(TimeSpan.FromDays(1)),
PageSize = 100,
};
OrchestrationStatusQueryResult result = await client.ListInstancesAsync(
queryFilter,
CancellationToken.None);
foreach (DurableOrchestrationStatus instance in result.DurableOrchestrationState)
{
log.LogInformation(JsonConvert.SerializeObject(instance));
}
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

### Azure Functions Core Tools

In the Azure Functions Core Tools, you can also use the `durable get-instances`

command with filters. In addition to the aforementioned `top`

, `continuation-token`

, `connection-string-setting`

, and `task-hub-name`

parameters, you can use three filter parameters (`created-after`

, `created-before`

, and `runtime-status`

).

Note

The Core Tools commands are currently only supported when using the default [Azure Storage provider](durable-functions-storage-providers) for persisting runtime state.

The following are the parameters for the `durable get-instances`

command.

: Retrieve the instances created after this date/time (UTC). ISO 8601 formatted datetimes accepted.`created-after`

(optional): Retrieve the instances created before this date/time (UTC). ISO 8601 formatted datetimes accepted.`created-before`

(optional): Retrieve the instances with a particular status (for example, running or completed). Can provide multiple (space separated) statuses.`runtime-status`

(optional): Number of instances retrieved per request. The default is 10.`top`

(optional): A token to indicate which page or section of instances to retrieve. Each`continuation-token`

(optional)`get-instances`

execution returns a token to the next set of instances.: Name of the application setting containing the storage connection string to use. The default is`connection-string-setting`

(optional)`AzureWebJobsStorage`

.: Name of the Durable Functions task hub to use. The default is`task-hub-name`

(optional)`DurableFunctionsHub`

. It can also be set in[host.json](durable-functions-bindings#host-json), by using durableTask:HubName.

If you don't provide any filters (`created-after`

, `created-before`

, or `runtime-status`

), the command simply retrieves `top`

instances, with no regard to runtime status or creation time.

```
func durable get-instances --created-after 2021-03-10T13:57:31Z --created-before 2021-03-10T23:59Z --top 15
```


## Terminate instances

If you have an orchestration instance that is taking too long to run, or you just need to stop it before it completes for any reason, you can terminate it.

The two parameters for the terminate API are an *instance ID* and a *reason* string, which are written to logs and to the instance status.

```
[FunctionName("TerminateInstance")]
public static Task Run(
[DurableClient] IDurableOrchestrationClient client,
[QueueTrigger("terminate-queue")] string instanceId)
{
string reason = "Found a bug";
return client.TerminateAsync(instanceId, reason);
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

A terminated instance will eventually transition into the `Terminated`

state. However, this transition will not happen immediately. Rather, the terminate operation will be queued in the task hub along with other operations for that instance. You can use the [instance query](#query-instances) APIs to know when a terminated instance has actually reached the `Terminated`

state.

Note

Instance termination doesn't currently propagate. Activity functions and sub-orchestrations run to completion, regardless of whether you've terminated the orchestration instance that called them.

## Suspend and Resume instances

Suspending an orchestration allows you to stop a running orchestration. Unlike with termination, you have the option to resume a suspended orchestrator at a later point in time.

The two parameters for the suspend API are an instance ID and a reason string, which are written to logs and to the instance status.

```
[FunctionName("SuspendResumeInstance")]
public static async Task Run(
[DurableClient] IDurableOrchestrationClient client,
[QueueTrigger("suspend-resume-queue")] string instanceId)
{
// To suspend an orchestration
string suspendReason = "Need to pause workflow";
await client.SuspendAsync(instanceId, suspendReason);
// To resume an orchestration
string resumeReason = "Continue workflow";
await client.ResumeAsync(instanceId, resumeReason);
}
```


A suspended instance will eventually transition to the `Suspended`

state. However, this transition will not happen immediately. Rather, the suspend operation will be queued in the task hub along with other operations for that instance. You can use the instance query APIs to know when a running instance has actually reached the Suspended state.

When a suspended orchestrator is resumed, its status will change back to `Running`

.

### Azure Functions Core Tools

You can also terminate an orchestration instance directly, by using the [ func durable terminate command](../functions-core-tools-reference#func-durable-terminate) in Core Tools.

Note

The Core Tools commands are currently only supported when using the default [Azure Storage provider](durable-functions-storage-providers) for persisting runtime state.

The `durable terminate`

command takes the following parameters:

: ID of the orchestration instance to terminate.`id`

(required): Reason for termination.`reason`

(optional): Name of the application setting containing the storage connection string to use. The default is`connection-string-setting`

(optional)`AzureWebJobsStorage`

.: Name of the Durable Functions task hub to use. The default is`task-hub-name`

(optional)`DurableFunctionsHub`

. It can also be set in[host.json](durable-functions-bindings#host-json), by using durableTask:HubName.

The following command terminates an orchestration instance with an ID of 0ab8c55a66644d68a3a8b220b12d209c:

```
func durable terminate --id 0ab8c55a66644d68a3a8b220b12d209c --reason "Found a bug"
```


## Send events to instances

In some scenarios, orchestrator functions need to wait and listen for external events. Examples scenarios where this is useful include the [monitoring](durable-functions-overview#monitoring) and [human interaction](durable-functions-overview#human) scenarios.

You can send event notifications to running instances by using the *raise event* API of the [orchestration client](durable-functions-bindings#orchestration-client). Orchestrations can listen and respond to these events using the *wait for external event* orchestrator API.

The parameters for *raise event* are as follows:

*Instance ID*: The unique ID of the instance.*Event name*: The name of the event to send.*Event data*: A JSON-serializable payload to send to the instance.

```
[FunctionName("RaiseEvent")]
public static Task Run(
[DurableClient] IDurableOrchestrationClient client,
[QueueTrigger("event-queue")] string instanceId)
{
int[] eventData = new int[] { 1, 2, 3 };
return client.RaiseEventAsync(instanceId, "MyEvent", eventData);
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

Note

If there is no orchestration instance with the specified instance ID, the event message is discarded. If an instance exists but it is not yet waiting for the event, the event will be stored in the instance state until it is ready to be received and processed.

### Azure Functions Core Tools

You can also raise an event to an orchestration instance directly, by using the [ func durable raise-event command](../functions-core-tools-reference#func-durable-raise-event) in Core Tools.

Note

The Core Tools commands are currently only supported when using the default [Azure Storage provider](durable-functions-storage-providers) for persisting runtime state.

The `durable raise-event`

command takes the following parameters:

: ID of the orchestration instance.`id`

(required): Name of the event to raise.`event-name`

: Data to send to the orchestration instance. This can be the path to a JSON file, or you can provide the data directly on the command line.`event-data`

(optional): Name of the application setting containing the storage connection string to use. The default is`connection-string-setting`

(optional)`AzureWebJobsStorage`

.: Name of the Durable Functions task hub to use. The default is`task-hub-name`

(optional)`DurableFunctionsHub`

. It can also be set in[host.json](durable-functions-bindings#host-json), by using durableTask:HubName.

```
func durable raise-event --id 0ab8c55a66644d68a3a8b220b12d209c --event-name MyEvent --event-data @eventdata.json
```


```
func durable raise-event --id 1234567 --event-name MyOtherEvent --event-data 3
```


## Wait for orchestration completion

In long-running orchestrations, you may want to wait and get the results of an orchestration. In these cases, it's also useful to be able to define a timeout period on the orchestration. If the timeout is exceeded, the state of the orchestration should be returned instead of the results.

The *"wait for completion or create check status response"* API can be used to get the actual output from an orchestration instance synchronously. By default, this method has a default timeout of 10 seconds and a polling interval of 1 second.

Here is an example HTTP-trigger function that demonstrates how to use this API:

```
// Copyright (c) .NET Foundation. All rights reserved.
// Licensed under the MIT License. See LICENSE in the project root for license information.
using System;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.DurableTask;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Logging;
namespace VSSample
{
public static class HttpSyncStart
{
private const string Timeout = "timeout";
private const string RetryInterval = "retryInterval";
[FunctionName("HttpSyncStart")]
public static async Task<HttpResponseMessage> Run(
[HttpTrigger(AuthorizationLevel.Function, methods: "post", Route = "orchestrators/{functionName}/wait")]
HttpRequestMessage req,
[DurableClient] IDurableOrchestrationClient starter,
string functionName,
ILogger log)
{
// Function input comes from the request content.
object eventData = await req.Content.ReadAsAsync<object>();
string instanceId = await starter.StartNewAsync(functionName, eventData);
log.LogInformation($"Started orchestration with ID = '{instanceId}'.");
TimeSpan timeout = GetTimeSpan(req, Timeout) ?? TimeSpan.FromSeconds(30);
TimeSpan retryInterval = GetTimeSpan(req, RetryInterval) ?? TimeSpan.FromSeconds(1);
return await starter.WaitForCompletionOrCreateCheckStatusResponseAsync(
req,
instanceId,
timeout,
retryInterval);
}
private static TimeSpan? GetTimeSpan(HttpRequestMessage request, string queryParameterName)
{
string queryParameterStringValue = request.RequestUri.ParseQueryString()[queryParameterName];
if (string.IsNullOrEmpty(queryParameterStringValue))
{
return null;
}
return TimeSpan.FromSeconds(double.Parse(queryParameterStringValue));
}
}
}
```


Call the function with the following line. Use 2 seconds for the timeout and 0.5 second for the retry interval:

```
curl -X POST "http://localhost:7071/orchestrators/E1_HelloSequence/wait?timeout=2&retryInterval=0.5"
```


Note

The above cURL command assumes you have an orchestrator function named `E1_HelloSequence`

in your project. Because of how the HTTP trigger function is written, you can replace it with the name of any orchestrator function in your project.

Depending on the time required to get the response from the orchestration instance, there are two cases:

- The orchestration instances complete within the defined timeout (in this case 2 seconds), and the response is the actual orchestration instance output, delivered synchronously:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Thu, 14 Dec 2021 06:14:29 GMT
Transfer-Encoding: chunked
[
"Hello Tokyo!",
"Hello Seattle!",
"Hello London!"
]
```


- The orchestration instances can't complete within the defined timeout, and the response is the default one described in
[HTTP API URL discovery](durable-functions-http-api):

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Date: Thu, 14 Dec 2021 06:13:51 GMT
Location: http://localhost:7071/runtime/webhooks/durabletask/instances/d3b72dddefce4e758d92f4d411567177?taskHub={taskHub}&connection={connection}&code={systemKey}
Retry-After: 10
Transfer-Encoding: chunked
{
"id": "d3b72dddefce4e758d92f4d411567177",
"sendEventPostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/d3b72dddefce4e758d92f4d411567177/raiseEvent/{eventName}?taskHub={taskHub}&connection={connection}&code={systemKey}",
"statusQueryGetUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/d3b72dddefce4e758d92f4d411567177?taskHub={taskHub}&connection={connection}&code={systemKey}",
"terminatePostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/d3b72dddefce4e758d92f4d411567177/terminate?reason={text}&taskHub={taskHub}&connection={connection}&code={systemKey}",
"suspendPostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/d3b72dddefce4e758d92f4d411567177/suspend?reason={text}&taskHub={taskHub}&connection={connection}&code={systemKey}",
"resumePostUri": "http://localhost:7071/runtime/webhooks/durabletask/instances/d3b72dddefce4e758d92f4d411567177/resume?reason={text}&taskHub={taskHub}&connection={connection}&code={systemKey}"
}
```


Note

The format of the webhook URLs might differ, depending on which version of the Azure Functions host you are running. The preceding example is for the Azure Functions 3.0 host.

## Retrieve HTTP management webhook URLs

You can use an external system to monitor or to raise events to an orchestration. External systems can communicate with Durable Functions through the webhook URLs that are part of the default response described in [HTTP API URL discovery](durable-functions-http-features#http-api-url-discovery). The webhook URLs can alternatively be accessed programmatically using the [orchestration client binding](durable-functions-bindings#orchestration-client). Specifically, the *create HTTP management payload* API can be used to get a serializable object that contains these webhook URLs.

The *create HTTP management payload* API has one parameter:

*Instance ID*: The unique ID of the instance.

The methods return an object with the following string properties:

**Id**: The instance ID of the orchestration (should be the same as the`InstanceId`

input).**StatusQueryGetUri**: The status URL of the orchestration instance.**SendEventPostUri**: The "raise event" URL of the orchestration instance.**TerminatePostUri**: The "terminate" URL of the orchestration instance.**PurgeHistoryDeleteUri**: The "purge history" URL of the orchestration instance.**suspendPostUri**: The "suspend" URL of the orchestration instance.**resumePostUri**: The "resume" URL of the orchestration instance.

Functions can send instances of these objects to external systems to monitor or raise events on the corresponding orchestrations, as shown in the following examples:

```
[FunctionName("SendInstanceInfo")]
public static void SendInstanceInfo(
[ActivityTrigger] IDurableActivityContext ctx,
[DurableClient] IDurableOrchestrationClient client,
[CosmosDB(
databaseName: "MonitorDB",
containerName: "HttpManagementPayloads",
Connection = "CosmosDBConnectionSetting")]out dynamic document)
{
HttpManagementPayload payload = client.CreateHttpManagementPayload(ctx.InstanceId);
// send the payload to Azure Cosmos DB
document = new { Payload = payload, id = ctx.InstanceId };
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `DurableActivityContext`

instead of `IDurableActivityContext`

, you must use the `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

## Rewind instances

If you have an orchestration failure for an unexpected reason, you can *rewind* the instance to a previously healthy state by using an API built for that purpose.

Note

This API is not intended to be a replacement for proper error handling and retry policies. Rather, it is intended to be used only in cases where orchestration instances fail for unexpected reasons. Orchestrations in states other than `Failed`

(e.g., `Running`

, `Pending`

, `Terminated`

, `Completed`

) cannot be "rewound". For more information on error handling and retry policies, see the [Error handling](durable-functions-error-handling) article.

Use the `RewindAsync`

(.NET) or `rewind`

(JavaScript) method of the orchestration client binding to put the orchestration back into the `Running`

state. This method reruns the activity or sub-orchestration execution failures that caused the orchestration failure. The method only attempts to rerun failed activities, either within the parent or failed sub-orchestrations. It doesn't remedy orchestrations that failed for other reasons.

For example, let's say you have a workflow involving a series of [human approvals](durable-functions-overview#human). Suppose there are a series of activity functions that notify someone that their approval is needed, and wait out the real-time response. After all of the approval activities have received responses or timed out, suppose that another activity fails due to an application misconfiguration, such as an invalid database connection string. The result is an orchestration failure deep into the workflow. With the `RewindAsync`

(.NET) or `rewind`

(JavaScript) API, an application administrator can fix the configuration error, and rewind the failed orchestration back to the state immediately before the failure. None of the human-interaction steps need to be re-approved, and the orchestration can now complete successfully.

Note

The *rewind* feature doesn't support rewinding orchestration instances that use durable timers.

```
[FunctionName("RewindInstance")]
public static Task Run(
[DurableClient] IDurableOrchestrationClient client,
[QueueTrigger("rewind-queue")] string instanceId)
{
string reason = "Orchestrator failed and needs to be revived.";
return client.RewindAsync(instanceId, reason);
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

### Azure Functions Core Tools

You can also rewind an orchestration instance directly by using the [ func durable rewind command](../functions-core-tools-reference#func-durable-rewind) in Core Tools.

Note

The Core Tools commands are currently only supported when using the default [Azure Storage provider](durable-functions-storage-providers) for persisting runtime state.

The `durable rewind`

command takes the following parameters:

: ID of the orchestration instance.`id`

(required): Reason for rewinding the orchestration instance.`reason`

(optional): Name of the application setting containing the storage connection string to use. The default is`connection-string-setting`

(optional)`AzureWebJobsStorage`

.: Name of the Durable Functions task hub to use. By default, the task hub name in the`task-hub-name`

(optional)[host.json](durable-functions-bindings#host-json)file is used.

```
func durable rewind --id 0ab8c55a66644d68a3a8b220b12d209c --reason "Orchestrator failed and needs to be revived."
```


## Purge instance history

To remove all the data associated with an orchestration, you can purge the instance history. For example, you might want to delete any storage resources associated with a completed instance. To do so, use the *purge instance* API defined by the [orchestration client](durable-functions-bindings#orchestration-client).

This first example shows how to purge a single orchestration instance.

```
[FunctionName("PurgeInstanceHistory")]
public static Task Run(
[DurableClient] IDurableOrchestrationClient client,
[QueueTrigger("purge-queue")] string instanceId)
{
return client.PurgeInstanceHistoryAsync(instanceId);
}
```


The next example shows a timer-triggered function that purges the history for all orchestration instances that completed after the specified time interval. In this case, it removes data for all instances completed 30 or more days ago. This example function is scheduled to run once per day, at 12:00 PM UTC:

```
[FunctionName("PurgeInstanceHistory")]
public static Task Run(
[DurableClient] IDurableOrchestrationClient client,
[TimerTrigger("0 0 12 * * *")] TimerInfo myTimer)
{
return client.PurgeInstanceHistoryAsync(
DateTime.MinValue,
DateTime.UtcNow.AddDays(-30),
new List<OrchestrationStatus>
{
OrchestrationStatus.Completed
});
}
```


Note

The previous C# code is for Durable Functions 2.x. For Durable Functions 1.x, you must use `OrchestrationClient`

attribute instead of the `DurableClient`

attribute, and you must use the `DurableOrchestrationClient`

parameter type instead of `IDurableOrchestrationClient`

. For more information about the differences between versions, see the [Durable Functions versions](durable-functions-versions) article.

Note

For the purge history operation to succeed, the runtime status of the target instance must be **Completed**, **Terminated**, or **Failed**.

### Azure Functions Core Tools

You can purge an orchestration instance's history by using the [ func durable purge-history command](../functions-core-tools-reference#func-durable-purge-history) in Core Tools. Similar to the second C# example in the preceding section, it purges the history for all orchestration instances created during a specified time interval. You can further filter purged instances by runtime status.

Note

The Core Tools commands are currently only supported when using the default [Azure Storage provider](durable-functions-storage-providers) for persisting runtime state.

The `durable purge-history`

command has several parameters:

: Purge the history of instances created after this date/time (UTC). ISO 8601 formatted datetimes accepted.`created-after`

(optional): Purge the history of instances created before this date/time (UTC). ISO 8601 formatted datetimes accepted.`created-before`

(optional): Purge the history of instances with a particular status (for example, running or completed). Can provide multiple (space separated) statuses.`runtime-status`

(optional): Name of the application setting containing the storage connection string to use. The default is`connection-string-setting`

(optional)`AzureWebJobsStorage`

.: Name of the Durable Functions task hub to use. By default, the task hub name in the`task-hub-name`

(optional)[host.json](durable-functions-bindings#host-json)file is used.

The following command deletes the history of all failed instances created before November 14, 2021 at 7:35 PM (UTC).

```
func durable purge-history --created-before 2021-11-14T19:35:00.0000000Z --runtime-status failed
```


## Delete a task hub

Using the [ func durable delete-task-hub command](../functions-core-tools-reference#func-durable-delete-task-hub) in Core Tools, you can delete all storage artifacts associated with a particular task hub, including Azure storage tables, queues, and blobs.

Note

The Core Tools commands are currently only supported when using the default [Azure Storage provider](durable-functions-storage-providers) for persisting runtime state.

The `durable delete-task-hub`

command has two parameters:

: Name of the application setting containing the storage connection string to use. The default is`connection-string-setting`

(optional)`AzureWebJobsStorage`

.: Name of the Durable Functions task hub to use. By default, the task hub name in the`task-hub-name`

(optional)[host.json](durable-functions-bindings#host-json)file is used.

The following command deletes all Azure storage data associated with the `UserTest`

task hub.

```
func durable delete-task-hub --task-hub-name UserTest
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-overview -->

# What are Durable Functions?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

*Durable Functions* is a feature of [Azure Functions](../functions-overview) that lets you write stateful functions in a serverless compute environment. The extension lets you define stateful workflows by writing [ orchestrator functions](durable-functions-orchestrations) and stateful entities by writing

[using the Azure Functions programming model. Behind the scenes, the extension manages state, checkpoints, and restarts for you, allowing you to focus on your business logic.](durable-functions-entities)

*entity functions*## Supported languages

Durable Functions is designed to work with all Azure Functions programming languages but might have different minimum requirements for each language. The following table shows the minimum supported app configurations:

| Language stack | Azure Functions runtime versions | Language worker version | Minimum bundles version |
|---|---|---|---|
| .NET / C# / F# | Functions 1.0+ | In-process Out-of-process |
n/a |
| JavaScript/TypeScript (v3 prog. model) | Functions 2.0+ | Node 8+ | 2.x bundles |
| JavaScript/TypeScript (v4 prog. model) | Functions 4.25+ | Node 18+ | 3.15+ bundles |
| Python | Functions 2.0+ | Python 3.7+ | 2.x bundles |
| Python (v2 prog. model) | Functions 4.0+ | Python 3.7+ | 3.15+ bundles |
| PowerShell | Functions 3.0+ | PowerShell 7+ | 2.x bundles |
| Java | Functions 4.0+ | Java 8+ | 4.x bundles |

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](../functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](../functions-node-upgrade-v4).

Important

This article uses tabs to support multiple versions of the Python programming model. The v2 model is generally available and is designed to provide a more code-centric way for authoring functions through decorators. For more information about the v2 model, see the [Azure Functions Python developer guide](../functions-reference-python).

Like Azure Functions, there are templates to help you develop Durable Functions using [Visual Studio](durable-functions-isolated-create-first-csharp?pivots=code-editor-visualstudio), [Visual Studio Code](quickstart-js-vscode), and the [Azure portal](durable-functions-create-portal).

## Application patterns

The primary use case for Durable Functions is simplifying complex, stateful coordination requirements in serverless applications. The following sections describe typical application patterns that can benefit from Durable Functions:

[Function chaining](#chaining)[Fan-out/fan-in](#fan-in-out)[Async HTTP APIs](#async-http)[Monitoring](#monitoring)[Human interaction](#human)[Aggregator (stateful entities)](#aggregator)

### Pattern #1: Function chaining

In the function chaining pattern, a sequence of functions executes in a specific order. In this pattern, the output of one function is applied to the input of another function. The use of queues between each function ensures that the system stays durable and scalable, even though there's a flow of control from one function to the next.


You can use Durable Functions to implement the function chaining pattern concisely as shown in the following example.

Important

[Support ends for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](../migrate-dotnet-to-isolated-model).

In this example, the values `F1`

, `F2`

, `F3`

, and `F4`

are the names of other functions in the same function app. You can implement control flow by using normal imperative coding constructs. Code executes from the top down. The code can involve existing language control flow semantics, like conditionals and loops. You can include error handling logic in `try`

/`catch`

/`finally`

blocks.

```
[FunctionName("Chaining")]
public static async Task<object> Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
try
{
var x = await context.CallActivityAsync<object>("F1", null);
var y = await context.CallActivityAsync<object>("F2", x);
var z = await context.CallActivityAsync<object>("F3", y);
return await context.CallActivityAsync<object>("F4", z);
}
catch (Exception)
{
// Error handling or compensation goes here.
}
}
```


You can use the `context`

parameter to invoke other functions by name, pass parameters, and return function output. Each time the code calls `await`

, the Durable Functions framework checkpoints the progress of the current function instance. If the process or virtual machine recycles midway through the execution, the function instance resumes from the preceding `await`

call. For more information, see the next section, Pattern #2: Fan-out/fan-in.

In this example, the values `F1`

, `F2`

, `F3`

, and `F4`

are the names of other functions in the same function app. You can implement control flow by using normal imperative coding constructs. Code executes from the top down. The code can involve existing language control flow semantics, like conditionals and loops. You can include error handling logic in `try`

/`catch`

/`finally`

blocks.

```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context) {
try {
const x = yield context.df.callActivity("F1");
const y = yield context.df.callActivity("F2", x);
const z = yield context.df.callActivity("F3", y);
return yield context.df.callActivity("F4", z);
} catch (error) {
// Error handling or compensation goes here.
}
});
```


You can use the `context.df`

object to invoke other functions by name, pass parameters, and return function output. Each time the code calls `yield`

, the Durable Functions framework checkpoints the progress of the current function instance. If the process or virtual machine recycles midway through the execution, the function instance resumes from the preceding `yield`

call. For more information, see the next section, Pattern #2: Fan-out/fan-in.

Note

The `context`

object in JavaScript represents the entire [function context](../functions-reference-node#context-object). Access the Durable Functions context using the `df`

property on the main context.

In this example, the values `F1`

, `F2`

, `F3`

, and `F4`

are the names of other functions in the same function app. You can implement control flow by using normal imperative coding constructs. Code executes from the top down. The code can involve existing language control flow semantics, like conditionals and loops.

```
import azure.functions as func
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
x = yield context.call_activity("F1", None)
y = yield context.call_activity("F2", x)
z = yield context.call_activity("F3", y)
result = yield context.call_activity("F4", z)
return result
main = df.Orchestrator.create(orchestrator_function)
```


You can use the `context`

object to invoke other functions by name, pass parameters, and return function output. Each time the code calls `yield`

, the Durable Functions framework checkpoints the progress of the current function instance. If the process or virtual machine recycles midway through the execution, the function instance resumes from the preceding `yield`

call. For more information, see the next section, Pattern #2: Fan-out/fan-in.

Note

The `context`

object in Python represents the orchestration context. Access the main Azure Functions context using the `function_context`

property on the orchestration context.

In this example, the values `F1`

, `F2`

, `F3`

, and `F4`

are the names of other functions in the same function app. You can implement control flow by using normal imperative coding constructs. Code executes from the top down. The code can involve existing language control flow semantics, like conditionals and loops.

```
param($Context)
$X = Invoke-DurableActivity -FunctionName 'F1'
$Y = Invoke-DurableActivity -FunctionName 'F2' -Input $X
$Z = Invoke-DurableActivity -FunctionName 'F3' -Input $Y
Invoke-DurableActivity -FunctionName 'F4' -Input $Z
```


You can use the `Invoke-DurableActivity`

command to invoke other functions by name, pass parameters, and return function output. Each time the code calls `Invoke-DurableActivity`

without the `NoWait`

switch, the Durable Functions framework checkpoints the progress of the current function instance. If the process or virtual machine recycles midway through the execution, the function instance resumes from the preceding `Invoke-DurableActivity`

call. For more information, see the next section, Pattern #2: Fan-out/fan-in.

In this example, the values `F1`

, `F2`

, `F3`

, and `F4`

are the names of other functions in the same function app. You can implement control flow by using normal imperative coding constructs. Code executes from the top down. The code can involve existing language control flow semantics, like conditionals and loops.

```
@FunctionName("Chaining")
public double functionChaining(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
String input = ctx.getInput(String.class);
int x = ctx.callActivity("F1", input, int.class).await();
int y = ctx.callActivity("F2", x, int.class).await();
int z = ctx.callActivity("F3", y, int.class).await();
return ctx.callActivity("F4", z, double.class).await();
}
```


You can use the `ctx`

object to invoke other functions by name, pass parameters, and return function output. The output of these methods is a `Task<V>`

object where `V`

is the type of data returned by the invoked function. Each time you call `Task<V>.await()`

, the Durable Functions framework checkpoints the progress of the current function instance. If the process unexpectedly recycles midway through the execution, the function instance resumes from the preceding `Task<V>.await()`

call. For more information, see the next section, Pattern #2: Fan-out/fan-in.

### Pattern #2: Fan-out/fan-in

In the fan-out/fan-in pattern, you execute multiple functions in parallel and then wait for all functions to finish. Often, some aggregation work is done on the results that are returned from the functions.


With normal functions, you can fan out by having the function send multiple messages to a queue. Fanning back in is much more challenging. To fan in, in a normal function, you write code to track when the queue-triggered functions end, and then store function outputs.

The Durable Functions extension handles this pattern with relatively simple code:

```
[FunctionName("FanOutFanIn")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
var parallelTasks = new List<Task<int>>();
// Get a list of N work items to process in parallel.
object[] workBatch = await context.CallActivityAsync<object[]>("F1", null);
for (int i = 0; i < workBatch.Length; i++)
{
Task<int> task = context.CallActivityAsync<int>("F2", workBatch[i]);
parallelTasks.Add(task);
}
await Task.WhenAll(parallelTasks);
// Aggregate all N outputs and send the result to F3.
int sum = parallelTasks.Sum(t => t.Result);
await context.CallActivityAsync("F3", sum);
}
```


The fan-out work is distributed to multiple instances of the `F2`

function. The work is tracked by using a dynamic list of tasks. `Task.WhenAll`

is called to wait for all the called functions to finish. Then, the `F2`

function outputs are aggregated from the dynamic task list and passed to the `F3`

function.

The automatic checkpointing that happens at the `await`

call on `Task.WhenAll`

ensures that a potential midway crash or reboot doesn't require restarting an already completed task.

```
const df = require("durable-functions");
module.exports = df.orchestrator(function*(context) {
const parallelTasks = [];
// Get a list of N work items to process in parallel.
const workBatch = yield context.df.callActivity("F1");
for (let i = 0; i < workBatch.length; i++) {
parallelTasks.push(context.df.callActivity("F2", workBatch[i]));
}
yield context.df.Task.all(parallelTasks);
// Aggregate all N outputs and send the result to F3.
const sum = parallelTasks.reduce((prev, curr) => prev + curr, 0);
yield context.df.callActivity("F3", sum);
});
```


The fan-out work is distributed to multiple instances of the `F2`

function. The work is tracked by using a dynamic list of tasks. `context.df.Task.all`

API is called to wait for all the called functions to finish. Then, the `F2`

function outputs are aggregated from the dynamic task list and passed to the `F3`

function.

The automatic checkpointing that happens at the `yield`

call on `context.df.Task.all`

ensures that a potential midway crash or reboot doesn't require restarting an already completed task.

```
import azure.durable_functions as df
def orchestrator_function(context: df.DurableOrchestrationContext):
# Get a list of N work items to process in parallel.
work_batch = yield context.call_activity("F1", None)
parallel_tasks = [ context.call_activity("F2", b) for b in work_batch ]
outputs = yield context.task_all(parallel_tasks)
# Aggregate all N outputs and send the result to F3.
total = sum(outputs)
yield context.call_activity("F3", total)
main = df.Orchestrator.create(orchestrator_function)
```


The fan-out work is distributed to multiple instances of the `F2`

function. The work is tracked by using a dynamic list of tasks. `context.task_all`

API is called to wait for all the called functions to finish. Then, the `F2`

function outputs are aggregated from the dynamic task list and passed to the `F3`

function.

The automatic checkpointing that happens at the `yield`

call on `context.task_all`

ensures that a potential midway crash or reboot doesn't require restarting an already completed task.

```
param($Context)
# Get a list of work items to process in parallel.
$WorkBatch = Invoke-DurableActivity -FunctionName 'F1'
$ParallelTasks =
foreach ($WorkItem in $WorkBatch) {
Invoke-DurableActivity -FunctionName 'F2' -Input $WorkItem -NoWait
}
$Outputs = Wait-ActivityFunction -Task $ParallelTasks
# Aggregate all outputs and send the result to F3.
$Total = ($Outputs | Measure-Object -Sum).Sum
Invoke-DurableActivity -FunctionName 'F3' -Input $Total
```


The fan-out work is distributed to multiple instances of the `F2`

function. Please note the usage of the `NoWait`

switch on the `F2`

function invocation: this switch allows the orchestrator to proceed invoking `F2`

without waiting for activity completion. The work is tracked by using a dynamic list of tasks. The `Wait-ActivityFunction`

command is called to wait for all the called functions to finish. Then, the `F2`

function outputs are aggregated from the dynamic task list and passed to the `F3`

function.

The automatic checkpointing that happens at the `Wait-ActivityFunction`

call ensures that a potential midway crash or reboot doesn't require restarting an already completed task.

```
@FunctionName("FanOutFanIn")
public Integer fanOutFanInOrchestrator(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
// Get the list of work-items to process in parallel
List<?> batch = ctx.callActivity("F1", List.class).await();
// Schedule each task to run in parallel
List<Task<Integer>> parallelTasks = batch.stream()
.map(item -> ctx.callActivity("F2", item, Integer.class))
.collect(Collectors.toList());
// Wait for all tasks to complete, then return the aggregated sum of the results
List<Integer> results = ctx.allOf(parallelTasks).await();
return results.stream().reduce(0, Integer::sum);
}
```


The fan-out work is distributed to multiple instances of the `F2`

function. The work is tracked by using a dynamic list of tasks. `ctx.allOf(parallelTasks).await()`

is called to wait for all the called functions to finish. Then, the `F2`

function outputs are aggregated from the dynamic task list and returned as the orchestrator function's output.

The automatic checkpointing that happens at the `.await()`

call on `ctx.allOf(parallelTasks)`

ensures that an unexpected process recycle doesn't require restarting any already completed tasks.

Note

In rare circumstances, it's possible that a crash could happen in the window after an activity function completes but before its completion is saved into the orchestration history. If this happens, the activity function would rerun from the beginning after the process recovers.

### Pattern #3: Async HTTP APIs

The async HTTP API pattern addresses the problem of coordinating the state of long-running operations with external clients. A common way to implement this pattern is by having an HTTP endpoint trigger the long-running action. Then, redirect the client to a status endpoint that the client polls to learn when the operation is finished.


Durable Functions provides *built-in support* for this pattern, simplifying or even removing the code you need to write to interact with long-running function executions. For example, the Durable Functions quickstart samples ([C#](durable-functions-isolated-create-first-csharp), [JavaScript](quickstart-js-vscode), [TypeScript](quickstart-ts-vscode), [Python](quickstart-python-vscode), [PowerShell](quickstart-powershell-vscode), and [Java](quickstart-java)) show a simple REST command that you can use to start new orchestrator function instances. After an instance starts, the extension exposes webhook HTTP APIs that query the orchestrator function status.

The following example shows REST commands that start an orchestrator and query its status. For clarity, some protocol details are omitted from the example.

```
> curl -X POST https://myfunc.azurewebsites.net/api/orchestrators/DoWork -H "Content-Length: 0" -i
HTTP/1.1 202 Accepted
Content-Type: application/json
Location: https://myfunc.azurewebsites.net/runtime/webhooks/durabletask/instances/b79baf67f717453ca9e86c5da21e03ec
{"id":"b79baf67f717453ca9e86c5da21e03ec", ...}
> curl https://myfunc.azurewebsites.net/runtime/webhooks/durabletask/instances/b79baf67f717453ca9e86c5da21e03ec -i
HTTP/1.1 202 Accepted
Content-Type: application/json
Location: https://myfunc.azurewebsites.net/runtime/webhooks/durabletask/instances/b79baf67f717453ca9e86c5da21e03ec
{"runtimeStatus":"Running","lastUpdatedTime":"2019-03-16T21:20:47Z", ...}
> curl https://myfunc.azurewebsites.net/runtime/webhooks/durabletask/instances/b79baf67f717453ca9e86c5da21e03ec -i
HTTP/1.1 200 OK
Content-Length: 175
Content-Type: application/json
{"runtimeStatus":"Completed","lastUpdatedTime":"2019-03-16T21:20:57Z", ...}
```


Because the Durable Functions runtime manages state for you, you don't need to implement your own status-tracking mechanism.

The Durable Functions extension exposes built-in HTTP APIs that manage long-running orchestrations. You can alternatively implement this pattern yourself by using your own function triggers (such as HTTP, a queue, or Azure Event Hubs) and the [durable client binding](durable-functions-bindings#orchestration-client). For example, you might use a queue message to trigger termination. Or, you might use an HTTP trigger that's protected by a Microsoft Entra authentication policy instead of the built-in HTTP APIs that use a generated key for authentication.

For more information, see the [HTTP features](durable-functions-http-features) article, which explains how you can expose asynchronous, long-running processes over HTTP using the Durable Functions extension.

### Pattern #4: Monitor

The monitor pattern refers to a flexible, recurring process in a workflow. An example is polling until specific conditions are met. You can use a regular [timer trigger](../functions-bindings-timer) to address a basic scenario, such as a periodic cleanup job, but its interval is static and managing instance lifetimes becomes complex. You can use Durable Functions to create flexible recurrence intervals, manage task lifetimes, and create multiple monitor processes from a single orchestration.

An example of the monitor pattern is to reverse the earlier async HTTP API scenario. Instead of exposing an endpoint for an external client to monitor a long-running operation, the long-running monitor consumes an external endpoint, and then waits for a state change.


In a few lines of code, you can use Durable Functions to create multiple monitors that observe arbitrary endpoints. The monitors can end execution when a condition is met, or another function can use the durable orchestration client to terminate the monitors. You can change a monitor's `wait`

interval based on a specific condition (for example, exponential backoff.)

The following code implements a basic monitor:

```
[FunctionName("MonitorJobStatus")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
int jobId = context.GetInput<int>();
int pollingInterval = GetPollingInterval();
DateTime expiryTime = GetExpiryTime();
while (context.CurrentUtcDateTime < expiryTime)
{
var jobStatus = await context.CallActivityAsync<string>("GetJobStatus", jobId);
if (jobStatus == "Completed")
{
// Perform an action when a condition is met.
await context.CallActivityAsync("SendAlert", jobId);
break;
}
// Orchestration sleeps until this time.
var nextCheck = context.CurrentUtcDateTime.AddSeconds(pollingInterval);
await context.CreateTimer(nextCheck, CancellationToken.None);
}
// Perform more work here, or let the orchestration end.
}
```


```
const df = require("durable-functions");
const moment = require("moment");
module.exports = df.orchestrator(function*(context) {
const jobId = context.df.getInput();
const pollingInterval = getPollingInterval();
const expiryTime = getExpiryTime();
while (moment.utc(context.df.currentUtcDateTime).isBefore(expiryTime)) {
const jobStatus = yield context.df.callActivity("GetJobStatus", jobId);
if (jobStatus === "Completed") {
// Perform an action when a condition is met.
yield context.df.callActivity("SendAlert", jobId);
break;
}
// Orchestration sleeps until this time.
const nextCheck = moment.utc(context.df.currentUtcDateTime).add(pollingInterval, 's');
yield context.df.createTimer(nextCheck.toDate());
}
// Perform more work here, or let the orchestration end.
});
```


```
import azure.durable_functions as df
import json
from datetime import timedelta
def orchestrator_function(context: df.DurableOrchestrationContext):
job = json.loads(context.get_input())
job_id = job["jobId"]
polling_interval = job["pollingInterval"]
expiry_time = job["expiryTime"]
while context.current_utc_datetime < expiry_time:
job_status = yield context.call_activity("GetJobStatus", job_id)
if job_status == "Completed":
# Perform an action when a condition is met.
yield context.call_activity("SendAlert", job_id)
break
# Orchestration sleeps until this time.
next_check = context.current_utc_datetime + timedelta(seconds=polling_interval)
yield context.create_timer(next_check)
# Perform more work here, or let the orchestration end.
main = df.Orchestrator.create(orchestrator_function)
```


```
param($Context)
$output = @()
$jobId = $Context.Input.JobId
$machineId = $Context.Input.MachineId
$pollingInterval = New-TimeSpan -Seconds $Context.Input.PollingInterval
$expiryTime = $Context.Input.ExpiryTime
while ($Context.CurrentUtcDateTime -lt $expiryTime) {
$jobStatus = Invoke-DurableActivity -FunctionName 'GetJobStatus' -Input $jobId
if ($jobStatus -eq "Completed") {
# Perform an action when a condition is met.
$output += Invoke-DurableActivity -FunctionName 'SendAlert' -Input $machineId
break
}
# Orchestration sleeps until this time.
Start-DurableTimer -Duration $pollingInterval
}
# Perform more work here, or let the orchestration end.
$output
```


```
@FunctionName("Monitor")
public String monitorOrchestrator(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
JobInfo jobInfo = ctx.getInput(JobInfo.class);
String jobId = jobInfo.getJobId();
Instant expiryTime = jobInfo.getExpirationTime();
while (ctx.getCurrentInstant().compareTo(expiryTime) < 0) {
String status = ctx.callActivity("GetJobStatus", jobId, String.class).await();
// Perform an action when a condition is met
if (status.equals("Completed")) {
// send an alert and exit
ctx.callActivity("SendAlert", jobId).await();
break;
}
// wait N minutes before doing the next poll
Duration pollingDelay = jobInfo.getPollingDelay();
ctx.createTimer(pollingDelay).await();
}
return "done";
}
```


When a request is received, a new orchestration instance is created for that job ID. The instance polls a status until either a condition is met or until a time out expires. A durable timer controls the polling interval. Then, more work can be performed, or the orchestration can end.

### Pattern #5: Human interaction

Many automated processes involve some kind of human interaction. Involving humans in an automated process is tricky because people aren't as highly available and as responsive as cloud services. An automated process might allow for this interaction by using time-outs and compensation logic.

An approval process is an example of a business process that involves human interaction. Approval from a manager might be required for an expense report that exceeds a certain dollar amount. If the manager doesn't approve the expense report within 72 hours (might be the manager went on vacation), an escalation process kicks in to get the approval from someone else (perhaps the manager's manager).


You can implement the pattern in this example by using an orchestrator function. The orchestrator uses a [durable timer](durable-functions-timers) to request approval. The orchestrator escalates if time out occurs. The orchestrator waits for an [external event](durable-functions-external-events), such as a notification that's generated by a human interaction.

These examples create an approval process to demonstrate the human interaction pattern:

```
[FunctionName("ApprovalWorkflow")]
public static async Task Run(
[OrchestrationTrigger] IDurableOrchestrationContext context)
{
await context.CallActivityAsync("RequestApproval", null);
using (var timeoutCts = new CancellationTokenSource())
{
DateTime dueTime = context.CurrentUtcDateTime.AddHours(72);
Task durableTimeout = context.CreateTimer(dueTime, timeoutCts.Token);
Task<bool> approvalEvent = context.WaitForExternalEvent<bool>("ApprovalEvent");
if (approvalEvent == await Task.WhenAny(approvalEvent, durableTimeout))
{
timeoutCts.Cancel();
await context.CallActivityAsync("ProcessApproval", approvalEvent.Result);
}
else
{
await context.CallActivityAsync("Escalate", null);
}
}
}
```


To create the durable timer, call `context.CreateTimer`

. The notification is received by `context.WaitForExternalEvent`

. Then, `Task.WhenAny`

is called to decide whether to escalate (time-out happens first) or process the approval (the approval is received before time-out).

```
const df = require("durable-functions");
const moment = require('moment');
module.exports = df.orchestrator(function*(context) {
yield context.df.callActivity("RequestApproval");
const dueTime = moment.utc(context.df.currentUtcDateTime).add(72, 'h');
const durableTimeout = context.df.createTimer(dueTime.toDate());
const approvalEvent = context.df.waitForExternalEvent("ApprovalEvent");
const winningEvent = yield context.df.Task.any([approvalEvent, durableTimeout]);
if (winningEvent === approvalEvent) {
durableTimeout.cancel();
yield context.df.callActivity("ProcessApproval", approvalEvent.result);
} else {
yield context.df.callActivity("Escalate");
}
});
```


To create the durable timer, call `context.df.createTimer`

. The notification is received by `context.df.waitForExternalEvent`

. Then, `context.df.Task.any`

is called to decide whether to escalate (time-out happens first) or process the approval (the approval is received before time-out).

```
import azure.durable_functions as df
import json
from datetime import timedelta
def orchestrator_function(context: df.DurableOrchestrationContext):
yield context.call_activity("RequestApproval", None)
due_time = context.current_utc_datetime + timedelta(hours=72)
durable_timeout_task = context.create_timer(due_time)
approval_event_task = context.wait_for_external_event("ApprovalEvent")
winning_task = yield context.task_any([approval_event_task, durable_timeout_task])
if approval_event_task == winning_task:
durable_timeout_task.cancel()
yield context.call_activity("ProcessApproval", approval_event_task.result)
else:
yield context.call_activity("Escalate", None)
main = df.Orchestrator.create(orchestrator_function)
```


To create the durable timer, call `context.create_timer`

. The notification is received by `context.wait_for_external_event`

. Then, `context.task_any`

is called to decide whether to escalate (time-out happens first) or process the approval (the approval is received before time-out).

```
param($Context)
$output = @()
$duration = New-TimeSpan -Seconds $Context.Input.Duration
$managerId = $Context.Input.ManagerId
$output += Invoke-DurableActivity -FunctionName "RequestApproval" -Input $managerId
$durableTimeoutEvent = Start-DurableTimer -Duration $duration -NoWait
$approvalEvent = Start-DurableExternalEventListener -EventName "ApprovalEvent" -NoWait
$firstEvent = Wait-DurableTask -Task @($approvalEvent, $durableTimeoutEvent) -Any
if ($approvalEvent -eq $firstEvent) {
Stop-DurableTimerTask -Task $durableTimeoutEvent
$output += Invoke-DurableActivity -FunctionName "ProcessApproval" -Input $approvalEvent
}
else {
$output += Invoke-DurableActivity -FunctionName "EscalateApproval"
}
$output
```


To create the durable timer, call `Start-DurableTimer`

. The notification is received by `Start-DurableExternalEventListener`

. Then, `Wait-DurableTask`

is called to decide whether to escalate (time out happens first) or process the approval (the approval is received before time-out).

```
@FunctionName("ApprovalWorkflow")
public void approvalWorkflow(
@DurableOrchestrationTrigger(name = "ctx") TaskOrchestrationContext ctx) {
ApprovalInfo approvalInfo = ctx.getInput(ApprovalInfo.class);
ctx.callActivity("RequestApproval", approvalInfo).await();
Duration timeout = Duration.ofHours(72);
try {
// Wait for an approval. A TaskCanceledException will be thrown if the timeout expires.
boolean approved = ctx.waitForExternalEvent("ApprovalEvent", timeout, boolean.class).await();
approvalInfo.setApproved(approved);
ctx.callActivity("ProcessApproval", approvalInfo).await();
} catch (TaskCanceledException timeoutEx) {
ctx.callActivity("Escalate", approvalInfo).await();
}
}
```


The `ctx.waitForExternalEvent(...).await()`

method call pauses the orchestration until it receives an event named `ApprovalEvent`

, which has a `boolean`

payload. If the event is received, an activity function is called to process the approval result. However, if no such event is received before the `timeout`

(72 hours) expires, a `TaskCanceledException`

is raised, and the `Escalate`

activity function is called.

Note

There's no charge for time spent waiting for external events when running in the Consumption plan.

An external client can deliver the event notification to a waiting orchestrator function by using the [built-in HTTP APIs](durable-functions-http-api#raise-event):

```
curl -d "true" http://localhost:7071/runtime/webhooks/durabletask/instances/{instanceId}/raiseEvent/ApprovalEvent -H "Content-Type: application/json"
```


An event can also be raised using the durable orchestration client from another function in the same function app:

```
[FunctionName("RaiseEventToOrchestration")]
public static async Task Run(
[HttpTrigger] string instanceId,
[DurableClient] IDurableOrchestrationClient client)
{
bool isApproved = true;
await client.RaiseEventAsync(instanceId, "ApprovalEvent", isApproved);
}
```


```
import azure.durable_functions as df
async def main(client: str):
durable_client = df.DurableOrchestrationClient(client)
is_approved = True
await durable_client.raise_event(instance_id, "ApprovalEvent", is_approved)
```


```
Send-DurableExternalEvent -InstanceId $InstanceId -EventName "ApprovalEvent" -EventData "true"
```


```
@FunctionName("RaiseEventToOrchestration")
public void raiseEventToOrchestration(
@HttpTrigger(name = "instanceId") String instanceId,
@DurableClientInput(name = "durableContext") DurableClientContext durableContext) {
DurableTaskClient client = durableContext.getClient();
client.raiseEvent(instanceId, "ApprovalEvent", true);
}
```


### Pattern #6: Aggregator (stateful entities)

The sixth pattern is about aggregating event data over a period of time into a single, addressable *entity*. In this pattern, the data being aggregated might come from multiple sources, might be delivered in batches, or might be scattered over long periods of time. The aggregator might need to take action on event data as it arrives, and external clients might need to query the aggregated data.


The tricky thing about trying to implement this pattern with normal, stateless functions is that concurrency control becomes a huge challenge. Not only do you need to worry about multiple threads modifying the same data at the same time, you also need to worry about ensuring that the aggregator only runs on a single virtual machine at a time.

You can use [Durable entities](durable-functions-entities) to easily implement this pattern as a single function.

```
[FunctionName("Counter")]
public static void Counter([EntityTrigger] IDurableEntityContext ctx)
{
int currentValue = ctx.GetState<int>();
switch (ctx.OperationName.ToLowerInvariant())
{
case "add":
int amount = ctx.GetInput<int>();
ctx.SetState(currentValue + amount);
break;
case "reset":
ctx.SetState(0);
break;
case "get":
ctx.Return(currentValue);
break;
}
}
```


Durable entities can also be modeled as classes in .NET. This model can be useful if the list of operations is fixed and becomes large. The following example is an equivalent implementation of the `Counter`

entity using .NET classes and methods.

```
public class Counter
{
[JsonProperty("value")]
public int CurrentValue { get; set; }
public void Add(int amount) => this.CurrentValue += amount;
public void Reset() => this.CurrentValue = 0;
public int Get() => this.CurrentValue;
[FunctionName(nameof(Counter))]
public static Task Run([EntityTrigger] IDurableEntityContext ctx)
=> ctx.DispatchAsync<Counter>();
}
```


```
const df = require("durable-functions");
module.exports = df.entity(function(context) {
const currentValue = context.df.getState(() => 0);
switch (context.df.operationName) {
case "add":
const amount = context.df.getInput();
context.df.setState(currentValue + amount);
break;
case "reset":
context.df.setState(0);
break;
case "get":
context.df.return(currentValue);
break;
}
});
```


```
import azure.functions as func
import azure.durable_functions as df
def entity_function(context: df.DurableOrchestrationContext):
current_value = context.get_state(lambda: 0)
operation = context.operation_name
if operation == "add":
amount = context.get_input()
current_value += amount
context.set_result(current_value)
elif operation == "reset":
current_value = 0
elif operation == "get":
context.set_result(current_value)
context.set_state(current_value)
main = df.Entity.create(entity_function)
```


Note

Durable entities are currently not supported in PowerShell.

Note

Durable entities are currently not supported in Java.

Clients can enqueue *operations* for (also known as *signaling*) an entity function using the [entity client binding](durable-functions-bindings#entity-client).

```
[FunctionName("EventHubTriggerCSharp")]
public static async Task Run(
[EventHubTrigger("device-sensor-events")] EventData eventData,
[DurableClient] IDurableEntityClient entityClient)
{
var metricType = (string)eventData.Properties["metric"];
var delta = BitConverter.ToInt32(eventData.Body, eventData.Body.Offset);
// The "Counter/{metricType}" entity is created on-demand.
var entityId = new EntityId("Counter", metricType);
await entityClient.SignalEntityAsync(entityId, "add", delta);
}
```


Note

Dynamically generated proxies are also available in .NET for signaling entities in a type-safe way. And in addition to signaling, clients can also query for the state of an entity function using [type-safe methods](durable-functions-dotnet-entities#accessing-entities-through-interfaces) on the orchestration client binding.

```
import azure.functions as func
import azure.durable_functions as df
async def main(req: func.HttpRequest, starter: str) -> func.HttpResponse:
client = df.DurableOrchestrationClient(starter)
entity_id = df.EntityId("Counter", "myCounter")
instance_id = await client.signal_entity(entity_id, "add", 1)
return func.HttpResponse("Entity signaled")
```


Entity functions are available in [Durable Functions 2.0](durable-functions-versions) and above for C#, JavaScript, and Python.

## The technology

Behind the scenes, the Durable Functions extension is built on top of the [Durable Task Framework](https://github.com/Azure/durabletask), an open-source library on GitHub that's used to build workflows in code. Like Azure Functions is the serverless evolution of Azure WebJobs, Durable Functions is the serverless evolution of the Durable Task Framework. Microsoft and other organizations use the Durable Task Framework extensively to automate mission-critical processes. It's a natural fit for the serverless Azure Functions environment.

## Code constraints

In order to provide reliable and long-running execution guarantees, orchestrator functions have a set of coding rules that must be followed. For more information, see [Orchestrator function code constraints](durable-functions-code-constraints).

## Billing

Durable Functions is billed the same as Azure Functions. For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/). When executing orchestrator functions in Azure Functions [Consumption plan](../consumption-plan), there are some billing behaviors to be aware of. For more information on these behaviors, see the [Durable Functions billing](durable-functions-billing) article.

## Jump right in

You can get started with Durable Functions in under 10 minutes by completing one of these language-specific quickstart tutorials:

[C# using Visual Studio](durable-functions-isolated-create-first-csharp)[JavaScript using Visual Studio Code](quickstart-js-vscode)[TypeScript using Visual Studio Code](quickstart-ts-vscode)[Python using Visual Studio Code](quickstart-python-vscode)[PowerShell using Visual Studio Code](quickstart-powershell-vscode)[Java using Maven](quickstart-java)

In these quickstarts, you locally create and test a *Hello world* durable function. You then publish the function code to Azure. The function you create orchestrates and chains together calls to other functions.

## Publications

Durable Functions is developed in collaboration with Microsoft Research. As a result, the Durable Functions team actively produces research papers and artifacts; these include:

[Durable Functions: Semantics for Stateful Serverless](https://www.microsoft.com/research/uploads/prod/2021/10/DF-Semantics-Final.pdf)*(OOPSLA'21)*[Serverless Workflows with Durable Functions and Netherite](https://arxiv.org/pdf/2103.00033.pdf)*(preprint)*

## Video demo

The following video highlights the benefits of Durable Functions:

## Other orchestration options

Durable Functions is an advanced extension for [Azure Functions](../functions-overview), and might not be appropriate for all applications. For a comparison with other Azure orchestration technologies, see [Compare Azure Functions and Azure Logic Apps](../functions-compare-logic-apps-ms-flow-webjobs#compare-azure-functions-and-azure-logic-apps).
