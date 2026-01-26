---
merged_at: 2026-01-26T21:02:36.356612
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-create-private-site-access_run-functions-from-deployment-package__fu_eb2144.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-create-private-site-access_run-functions-from-deployment-package.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-create-private-site-access.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-private-site-access -->

# Tutorial: Establish Azure Functions private site access

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to enable [private site access](functions-networking-options#private-endpoints) with Azure Functions. By using private site access, you can require that your function code is only triggered from a specific virtual network.

Private site access is useful in scenarios when access to the function app needs to be limited to a specific virtual network. For example, the function app may be applicable to only employees of a specific organization, or services which are within the specified virtual network (such as another Azure Function, Azure Virtual Machine, or an AKS cluster).

If a Functions app needs to access Azure resources within the virtual network, or connected via [service endpoints](../virtual-network/virtual-network-service-endpoints-overview), then [virtual network integration](functions-create-vnet) is needed.

In this tutorial, you learn how to configure private site access for your function app:

- Create a virtual machine
- Create an Azure Bastion service
- Create an Azure Functions app
- Configure a virtual network service endpoint
- Create and deploy an Azure Function
- Invoke the function from outside and within the virtual network

If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Topology

The following diagram shows the architecture of the solution to be created:

## Prerequisites

For this tutorial, it's important that you understand IP addressing and subnetting. You can start with [this article that covers the basics of addressing and subnetting](https://support.microsoft.com/help/164015/understanding-tcp-ip-addressing-and-subnetting-basics). Many more articles and videos are available online.

## Sign in to Azure portal

Sign in to the [Azure portal](https://portal.azure.com).

## Create a virtual machine

The first step in this tutorial is to create a new virtual machine inside a virtual network. The virtual machine will be used to access your function once you've restricted its access to only be available from within the virtual network.

Select the

**Create a resource**button.In the search field, type

**Windows Server**, and select**Windows Server**in the search results.Select

**Windows Server 2019 Datacenter**from the list of Windows Server options, and press the**Create**button.In the

*Basics*tab, use the VM settings as specified in the table below the image:Setting Suggested value Description *Subscription*Your subscription The subscription under which your resources are created. *Resource group*myResourceGroup Choose the resource group to contain all the resources for this tutorial. Using the same resource group makes it easier to clean up resources when you're done with this tutorial. *Virtual machine name*myVM The VM name needs to be unique in the resource group *Region*(US) North Central US Choose a region near you or near the functions to be accessed. *Public inbound ports*None Select **None**to ensure there is no inbound connectivity to the VM from the internet. Remote access to the VM will be configured via the Azure Bastion service.Choose the

*Networking*tab and select**Create new**to configure a new virtual network.In

*Create virtual network*, use the settings in the table below the image:Setting Suggested value Description *Name*myResourceGroup-vnet You can use the default name generated for your virtual network. *Address range*10.10.0.0/16 Use a single address range for the virtual network. *Subnet name*Tutorial Name of the subnet. *Address range*(subnet)10.10.1.0/24 The subnet size defines how many interfaces can be added to the subnet. This subnet is used by the VM. A /24 subnet provides 254 host addresses. Select

**OK**to create the virtual network.Back in the

*Networking*tab, ensure**None**is selected for*Public IP*.Choose the

*Management*tab, then in*Diagnostic storage account*, choose**Create new**to create a new Storage account.Leave the default values for the

*Identity*,*Auto-shutdown*, and*Backup*sections.Select

*Review + create*. After validation completes, select**Create**. The VM create process takes a few minutes.

## Configure Azure Bastion

[Azure Bastion](https://azure.microsoft.com/services/azure-bastion/) is a fully managed Azure service which provides secure RDP and SSH access to virtual machines directly from the Azure portal. Using the Azure Bastion service removes the need to configure network settings related to RDP access.

In the portal, choose

**Add**at the top of the resource group view.In the search field, type

**Bastion**.Select

**Bastion**in the search results.Select

**Create**to begin the process of creating a new Azure Bastion resource. You will notice an error message in the*Virtual network*section as there is not yet an AzureBastionSubnet subnet. The subnet is created in the following steps. Use the settings in the table below the image:Setting Suggested value Description *Name*myBastion The name of the new Bastion resource *Region*North Central US Choose a [region](https://azure.microsoft.com/regions/)near you or near other services your functions access.*Virtual network*myResourceGroup-vnet The virtual network in which the Bastion resource will be created in *Subnet*AzureBastionSubnet The subnet in your virtual network to which the new Bastion host resource will be deployed. You must create a subnet using the name value **AzureBastionSubnet**. This value lets Azure know which subnet to deploy the Bastion resources to. You must use a subnet of at least**/27**or larger (/27, /26, and so on).Note

For a detailed, step-by-step guide to creating an Azure Bastion resource, refer to the

[Create an Azure Bastion host](../bastion/tutorial-create-host-portal)tutorial.Create a subnet in which Azure can provision the Azure Bastion host. Choosing

**Manage subnet configuration**opens a new pane where you can define a new subnet. Choose**+ Subnet**to create a new subnet.The subnet must be of the name

**AzureBastionSubnet**and the subnet prefix must be at least**/27**. Select**OK**to create the subnet.On the

*Create a Bastion*page, select the newly created**AzureBastionSubnet**from the list of available subnets.Select

**Review & Create**. Once validation completes, select**Create**. It will take a few minutes for the Azure Bastion resource to be created.

## Create an Azure Functions app

The next step is to create a function app in Azure using the [Consumption plan](consumption-plan). You deploy your function code to this resource later in the tutorial.

In the portal, choose

**Add**at the top of the resource group view.Select

**Compute > Function App**On the

*Basics*section, use the function app settings as specified in the table below.Setting Suggested value Description *Resource Group*myResourceGroup Choose the resource group to contain all the resources for this tutorial. Using the same resource group for the function app and VM makes it easier to clean up resources when you're done with this tutorial. *Function App name*Globally unique name Name that identifies your new function app. Valid characters are a-z (case insensitive), 0-9, and -. *Publish*Code Option to publish code files or a Docker container. *Runtime stack*Preferred language Choose a runtime that supports your favorite function programming language. *Region*North Central US Choose a [region](https://azure.microsoft.com/regions/)near you or near other services your functions access.Select the

**Next: Hosting >**button.For the

*Hosting*section, select the proper*Storage account*,*Operating system*, and*Plan*as described in the following table.Setting Suggested value Description *Storage account*Globally unique name Create a storage account used by your function app. Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only. You can also use an existing account, which must meet the [storage account requirements](storage-considerations#storage-account-requirements).*Operating system*Preferred operating system An operating system is pre-selected for you based on your runtime stack selection, but you can change the setting if necessary. *Plan*Consumption The [hosting plan](functions-scale)dictates how the function app is scaled and resources available to each instance.Select

**Review + Create**to review the app configuration selections.Select

**Create**to provision and deploy the function app.

## Configure access restrictions

The next step is to configure [access restrictions](../app-service/app-service-ip-restrictions) to ensure only resources on the virtual network can invoke the function.

[Private site](functions-networking-options#private-endpoints) access is enabled by creating an Azure Virtual Network [service endpoint](../virtual-network/virtual-network-service-endpoints-overview) between the function app and the specified virtual network. Access restrictions are implemented via service endpoints. Service endpoints ensure only traffic originating from within the specified virtual network can access the designated resource. In this case, the designated resource is the Azure Function.

Within the function app, select the

**Networking**link under the*Settings*section header.The

*Networking*page is the starting point to configure Azure Front Door, the Azure CDN, and also Access Restrictions.Select

**Configure Access Restrictions**to configure private site access.On the

*Access Restrictions*page, you see only the default restriction in place. The default doesn't place any restrictions on access to the function app. Select**Add rule**to create a private site access restriction configuration.In the

*Add Access Restriction*pane, provide a*Name*,*Priority*, and*Description*for the new rule.Select

**Virtual Network**from the*Type*drop-down box, then select the previously created virtual network, and then select the**Tutorial**subnet.Note

It may take several minutes to enable the service endpoint.

The

*Access Restrictions*page now shows that there is a new restriction. It may take a few seconds for the*Endpoint status*to change from Disabled through Provisioning to Enabled.Important

Each function app has an

[Advanced Tool (Kudu) site](../app-service/app-service-ip-restrictions#restrict-access-to-an-scm-site)that is used to manage function app deployments. This site is accessed from a URL like:`<FUNCTION_APP_NAME>.scm.azurewebsites.net`

. Enabling access restrictions on the Kudu site prevents the deployment of the project code from a local developer workstation, and then an agent is needed within the virtual network to perform the deployment.

## Access the functions app

Return to the previously created function app. In the

*Overview*section, copy the URL.If you try to access the function app now from your computer outside of your virtual network, you'll receive an HTTP 403 page indicating that access is forbidden.

Return to the resource group and select the previously created virtual machine. In order to access the site from the VM, you need to connect to the VM via the Azure Bastion service.

Select

**Connect**and then choose**Bastion**.Provide the required username and password to log into the virtual machine.

Note

For enhanced security, you should require Microsoft Entra authentication to access your virtual machines in Azure.

Select

**Connect**. A new browser window will pop up to allow you to interact with the virtual machine. It's possible to access the site from the web browser on the VM because the VM is accessing the site through the virtual network. While the site is only accessible from within the designated virtual network, a public DNS entry remains.

## Create a function

The next step in this tutorial is to create an HTTP-triggered Azure Function. Invoking the function via an HTTP GET or POST should result in a response of "Hello, {name}".

Follow one of the following quickstarts to create and deploy your Azure Functions app.

When publishing your Azure Functions project, choose the function app resource that you created earlier in this tutorial.

Verify the function is deployed.


## Invoke the function directly

In order to test access to the function, you need to copy the function URL. Select the deployed function, and then select

**Get Function Url**. Then click the**Copy**button to copy the URL to your clipboard.Paste the URL into a web browser. When you now try to access the function app from a computer outside of your virtual network, you receive an HTTP 403 response indicating access to the app is forbidden.


## Invoke the function from the virtual network

Accessing the function via a web browser (by using the Azure Bastion service) on the configured VM on the virtual network results in success!

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.


---

<!-- DOCUMENTO FUSIONADO: run-functions-from-deployment-package.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/run-functions-from-deployment-package -->

# Run your functions from a package file in Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure, you can run your functions directly from a deployment package file in your function app. The other option is to deploy your files in the `c:\home\site\wwwroot`

(Windows) or `/home/site/wwwroot`

(Linux) directory of your function app.

This article describes the benefits of running your functions from a package. It also shows how to enable this functionality in your function app.

## Benefits of running from a package file

There are several benefits to running functions from a package file:

- Reduces the risk of file copy locking issues.
- Can be deployed to a production app (with restart).
- Verifies the files that are running in your app.
- Improves the performance of
[Azure Resource Manager deployments](functions-infrastructure-as-code). - Reduces cold-start times, particularly for JavaScript functions with large npm package trees.

For more information, see [this announcement](https://github.com/Azure/app-service-announcements/issues/84).

## Enable functions to run from a package

Function apps on the [Flex Consumption](flex-consumption-plan) hosting plan run from a package by default. No special configuration needs to be done.

To enable your function app to run from a package on the [Consumption](consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) hosting plans, add a `WEBSITE_RUN_FROM_PACKAGE`

app setting to your function app. The `WEBSITE_RUN_FROM_PACKAGE`

app setting can have one of the following values:

| Value | Description |
|---|---|
`1` |
Indicates that the function app runs from a local package file deployed in the `c:\home\data\SitePackages` (Windows) or `/home/data/SitePackages` (Linux) folder of your function app. |
`<URL>` |
Sets a URL that is the remote location of the specific package file you want to run. Required for functions apps running on Linux in a Consumption plan. |

The following table indicates the recommended `WEBSITE_RUN_FROM_PACKAGE`

values for deployment to a specific operating system and hosting plan:

| Hosting plan | Windows | Linux |
|---|---|---|
|

`1`

is highly recommended.`<URL>`

is supported.[Premium](functions-premium-plan)`1`

is recommended.`1`

is recommended.[Dedicated](dedicated-plan)`1`

is recommended.`1`

is recommended.## General considerations

- Do not add the
`WEBSITE_RUN_FROM_PACKAGE`

app setting to apps on the[Flex Consumption](flex-consumption-plan)plan. - The package file must be .zip formatted. Tar and gzip formats aren't supported.
[Zip deployment](#integration-with-zip-deployment)is recommended.- When deploying your function app to Windows, you should set
`WEBSITE_RUN_FROM_PACKAGE`

to`1`

and publish with zip deployment. - When you run from a package, the
`wwwroot`

folder is read-only and you receive an error if you write files to this directory. Files are also read-only in the Azure portal. - The maximum size for a deployment package file is 1 GB.
- The deployment uses temporary storage when unpacking your project files. This means that your function app must have enough available temporary storage space to hold the contents of your package. Keep in mind that the temporary storage limit for a Consumption plan is
[500 MB per plan](functions-scale#service-limits). To learn about how to troubleshoot issues with temporary storage, see[How to troubleshoot temporary storage on Azure App Service](/en-us/troubleshoot/azure/app-service/temporary-storage-for-azure-app-service).

- The deployment uses temporary storage when unpacking your project files. This means that your function app must have enough available temporary storage space to hold the contents of your package. Keep in mind that the temporary storage limit for a Consumption plan is
- You can't use the local cache when running from a deployment package.
- If your project needs to use remote build, don't use the
`WEBSITE_RUN_FROM_PACKAGE`

app setting. Instead, add the`SCM_DO_BUILD_DURING_DEPLOYMENT=true`

deployment customization app setting. For Linux, also add the`ENABLE_ORYX_BUILD=true`

setting. For more information, see[Remote build](functions-deployment-technologies#remote-build).

Note

The `WEBSITE_RUN_FROM_PACKAGE`

app setting does not work with MSDeploy as described in [MSDeploy VS. ZipDeploy](https://github.com/projectkudu/kudu/wiki/MSDeploy-VS.-ZipDeploy). You will receive an error during deployment, such as `ARM-MSDeploy Deploy Failed`

. To resolve this error, change `/MSDeploy`

to `/ZipDeploy`

.

### Add the WEBSITE_RUN_FROM_PACKAGE setting

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

### Creating the zip archive

The zip archive you deploy must contain all of the files needed to run your function app. You can manually create a zip archive from the contents of a Functions project folder using built-in .zip compression functionality or non-Microsoft tools.

The archive must include the [host.json](functions-host-json) file at the root of the extracted folder. The selected language stack for the function app creates other requirements:

Important

For languages that generate compiled output for deployment, make sure to compress the contents of the output folder you plan to publish and not the entire project folder. When Functions extracts the contents of the zip archive, the `host.json`

file must exist in the root of the package.

## Use WEBSITE_RUN_FROM_PACKAGE = 1

This section provides information about how to run your function app from a local package file.

### Considerations for deploying from an on-site package

- Using an on-site package is the recommended option for running from the deployment package, except when running on Linux hosted in a Consumption plan.
[Zip deployment](#integration-with-zip-deployment)is the recommended way to upload a deployment package to your site.- When not using zip deployment, make sure the
`c:\home\data\SitePackages`

(Windows) or`/home/data/SitePackages`

(Linux) folder has a file named`packagename.txt`

. This file contains only the name, without any whitespace, of the package file in this folder that's currently running.

### Integration with zip deployment

Zip deployment is a feature of Azure App Service that lets you deploy your function app project to the `wwwroot`

directory. The project is packaged as a .zip deployment file. The same APIs can be used to deploy your package to the `c:\home\data\SitePackages`

(Windows) or `/home/data/SitePackages`

(Linux) folder.

When you set the `WEBSITE_RUN_FROM_PACKAGE`

app setting value to `1`

, the zip deployment APIs copy your package to the `c:\home\data\SitePackages`

(Windows) or `/home/data/SitePackages`

(Linux) folder instead of extracting the files to `c:\home\site\wwwroot`

(Windows) or `/home/site/wwwroot`

(Linux). It also creates the `packagename.txt`

file. After your function app is automatically restarted, the package is mounted to `wwwroot`

as a read-only filesystem. For more information about zip deployment, see [Zip deployment for Azure Functions](deployment-zip-push).

Note

When a deployment occurs, a restart of the function app is triggered. Function executions currently running during the deploy are terminated. For information about how to write stateless and defensive functions, sett [Write functions to be stateless](performance-reliability#write-functions-to-be-stateless).

## Use WEBSITE_RUN_FROM_PACKAGE = URL

This section provides information about how to run your function app from a package deployed to a URL endpoint. This option is the only one supported for running from a Linux-hosted package with a Consumption plan. This option is not supported in the [Flex Consumption](flex-consumption-plan) plan.

### Considerations for deploying from a URL

- Do not set
`WEBSITE_RUN_FROM_PACKAGE = <URL>`

in apps on the[Flex Consumption](flex-consumption-plan)plan. This option is not supported. - Function apps running on Windows experience a slight increase in
[cold-start time](event-driven-scaling#cold-start)when the application package is deployed to a URL endpoint via`WEBSITE_RUN_FROM_PACKAGE = <URL>`

. - When you specify a URL, you must also
[manually sync triggers](functions-deployment-technologies#trigger-syncing)after you publish an updated package. - The Functions runtime must have permissions to access the package URL.
- Don't deploy your package to Azure Blob Storage as a public blob. Instead, use a private container with a
[shared access signature (SAS)](../storage/common/storage-sas-overview)or[use a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity)to enable the Functions runtime to access the package. - You must maintain any SAS URLs used for deployment. When an SAS expires, the package can no longer be deployed. In this case, you must generate a new SAS and update the setting in your function app. You can eliminate this management burden by
[using a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity). - When running on a Premium plan, make sure to
[eliminate cold starts](functions-premium-plan#eliminate-cold-starts). - When you're running on a Dedicated plan, ensure you enable
[Always On](dedicated-plan#always-on). - You can use
[Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer)to upload package files to blob containers in your storage account.

### Manually uploading a package to Blob Storage

To deploy a zipped package when using the URL option, you must create a .zip compressed deployment package and upload it to the destination. The following procedure deploys to a container in Blob Storage:

Create a .zip package for your project using the utility of your choice.

In the

[Azure portal](https://portal.azure.com), search for your storage account name or browse for it in the storage accounts list.In the storage account, select

**Containers**under**Data storage**.Select

**+ Container**to create a new Blob Storage container in your account.In the

**New container**page, provide a**Name**(for example,*deployments*), ensure the**Anonymous access level**is**Private**, and then select**Create**.Select the container you created, select

**Upload**, browse to the location of the .zip file you created with your project, and then select**Upload**.After the upload completes, choose your uploaded blob file, and copy the URL. If you aren't

[using a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity), you might need to generate a SAS URL.Search for your function app or browse for it in the

**Function App**page.In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select**+ Add**.Enter the value

`WEBSITE_RUN_FROM_PACKAGE`

for the**Name**, and paste the URL of your package in Blob Storage for the**Value**.Select

**Apply**, and then select**Apply**and**Confirm**to save the setting and restart the function app.

Now you can run your function in Azure to verify that deployment of the deployment package .zip file was successful.

### Fetch a package from Azure Blob Storage using a managed identity

You can configure Azure Blob Storage to [authorize requests with Microsoft Entra ID](/en-us/azure/storage/blobs/authorize-access-azure-active-directory?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). This configuration means that instead of generating a SAS key with an expiration, you can instead rely on the application's [managed identity](/en-us/azure/app-service/overview-managed-identity). By default, the app's system-assigned identity is used. If you wish to specify a user-assigned identity, you can set the `WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID`

app setting to the resource ID of that identity. The setting can also accept `SystemAssigned`

as a value, which is equivalent to omitting the setting.

To enable the package to be fetched using the identity:

Ensure that the blob is

[configured for private access](/en-us/azure/storage/blobs/anonymous-read-access-configure#set-the-anonymous-access-level-for-a-container).Grant the identity the

[Storage Blob Data Reader](/en-us/azure/role-based-access-control/built-in-roles#storage-blob-data-reader)role with scope over the package blob. See[Assign an Azure role for access to blob data](/en-us/azure/storage/blobs/assign-azure-role-data-access)for details on creating the role assignment.Set the

`WEBSITE_RUN_FROM_PACKAGE`

application setting to the blob URL of the package. This URL is usually of the form`https://{storage-account-name}.blob.core.windows.net/{container-name}/{path-to-package}`

or similar.If you wish to specify a user-assigned identity, you can set the

`WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID`

app setting to the resource ID of that identity. The setting can also accept "SystemAssigned" as a value, although this is the same as omitting the setting altogether. A resource ID is a standard representation for a resource in Azure. For a user-assigned managed identity, that is going to be`/subscriptions/subid/resourcegroups/rg-name/providers/Microsoft.ManagedIdentity/userAssignedIdentities/identity-name`

. The resource ID of a user-assigned managed identity can be obtained in the**Settings**->**Properties**->**ID for the user assigned managed identity**.


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-error-pages_functions-concurrency.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-error-pages.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-error-pages -->

# Azure Functions error handling and retries

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Handling errors in Azure Functions helps you avoid lost data, avoid missed events, and monitor the health of your application. It's also an important way to help you understand the retry behaviors of event-based triggers.

This article describes general strategies for error handling and the available retry strategies.

Important

The preview of retry policy support for certain triggers was removed in December 2022. Retry policies for supported triggers are now in general availability (GA). The [Retries](#retries) section of this article lists extensions that currently support retry policies.

## Handling errors

Errors that occur in an Azure function can come from:

- Use of built-in Azure Functions
[triggers and bindings](functions-triggers-bindings). - Calls to APIs of underlying Azure services.
- Calls to REST endpoints.
- Calls to client libraries, packages, or non-Microsoft APIs.

To avoid loss of data or missed messages, you should practice good error handling. This table describes some recommended error-handling practices and provides links to more information:

| Recommendation | Details |
|---|---|
| Enable Application Insights | Azure Functions integrates with Application Insights to collect error data, performance data, and runtime logs. Use Application Insights to discover and better understand errors that occur in your function executions. To learn more, see
|

[Binding error codes](#binding-error-codes)in this article. Depending on your specific retry strategy, you might also raise a new exception to run the function again.[Retries](#retries)in this article.[Designing Azure Functions for identical input](functions-idempotent).Tip

When you use output bindings, you can't handle errors that occur from accessing the remote service. Because of this behavior, you should validate all data passed to your output bindings to avoid raising any known exceptions. If you must be able to handle such exceptions in your function code, you should access the remote service by using the client SDK instead of relying on output bindings.

## Retries

Two kinds of retries are available for your functions:

- Built-in retry behaviors of individual trigger extensions
- Retry policies that the Azure Functions runtime provides

The following table indicates which triggers support retries and where the retry behavior is configured. It also links to more information about errors that come from the underlying services.

| Trigger/binding | Retry source | Configuration |
|---|---|---|
| Azure Cosmos DB |
|

[Binding extension](functions-bindings-storage-blob-trigger#poison-blobs)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](../event-grid/delivery-and-retry)[Retry policies](#retry-policies)[Retry policies](#retry-policies)[Binding extension](functions-bindings-storage-queue-trigger#poison-messages)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](functions-bindings-rabbitmq-trigger#dead-letter-queues)[Dead letter queue](https://www.rabbitmq.com/dlx.html)[Binding extension](functions-bindings-service-bus-trigger)[host.json](functions-bindings-service-bus#hostjson-settings)*[Retry policies](#retry-policies)* Requires version 5.x of the Azure Service Bus extension. In older extension versions, the [Service Bus dead letter queue](../service-bus-messaging/service-bus-dead-letter-queues#maximum-delivery-count) implements retry behaviors.

## Retry policies

With Azure Functions, you can define retry policies for specific trigger types. The runtime enforces these retry policies. The following trigger types currently support retry policies:

Retry support is the same for both v1 and v2 Python programming models.

Retry policies aren't supported in version 1.x of the Azure Functions runtime.

The retry policy tells the runtime to rerun a failed execution until either successful completion occurs or the maximum number of retries is reached.

A retry policy is evaluated when a function that a supported trigger type executes raises an uncaught exception. As a best practice, you should catch all exceptions in your code and raise new exceptions for any errors that you want to result in a retry.

Important

Event Hubs checkpoints aren't written until after the retry policy for the execution finishes. Because of this behavior, progress on the specific partition is paused until the current batch finishes processing. For more information, see [Reliable event processing with Azure Functions and Event Hubs](functions-reliable-event-processing).

Version 5.x of the Event Hubs extension supports extra retry capabilities for interactions between the Azure Functions host and the event hub. For more information, see `clientRetryOptions`

in the [Event Hubs host.json reference](functions-bindings-event-hubs#host-json).

### Retry strategies

You can configure two retry strategies that are supported by policy:

A specified amount of time is allowed to elapse between each retry.

When you use a Consumption plan, you're billed only for the time that your function code is running. You aren't billed for the wait time between executions in either of these retry strategies.

### Maximum retry counts

You can configure the maximum number of times that a function execution is retried before eventual failure. The current retry count is stored in the memory of the instance.

It's possible for an instance to have a failure between retry attempts. When an instance fails during a retry policy, the retry count is lost. When there are instance failures, the Event Hubs trigger can resume processing and retry the batch on a new instance, with the retry count reset to zero. The timer trigger doesn't resume on a new instance.

This behavior means that the maximum retry count is a best effort. In some rare cases, an execution could be retried more than the requested maximum number of times. For timer triggers, the retries can be less than the requested maximum number.

### Retry examples

Examples are provided for both fixed delay and exponential backoff strategies. To see examples for a specific strategy, you must first select that strategy on the previous tab.

Function-level retries are supported with the following NuGet packages:

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)version 1.9.0 and later[Microsoft.Azure.Functions.Worker.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs)version 5.2.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Kafka](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kafka)version 3.8.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer)version 4.2.0 and later

```
[Function(nameof(TimerFunction))]
[FixedDelayRetry(5, "00:00:10")]
public static void Run([TimerTrigger("0 */5 * * * *")] TimerInfo timerInfo,
FunctionContext context)
{
var logger = context.GetLogger(nameof(TimerFunction));
logger.LogInformation($"Function Ran. Next timer schedule = {timerInfo.ScheduleStatus?.Next}");
}
```


| Property | Description |
|---|---|
`MaxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`DelayInterval` |
The delay used between retries. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a retry policy defined in the `function.json`

file:

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


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
const { app } = require('@azure/functions');
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: (myTimer, context) => {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
},
});
```


The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTriggerWithRetry(myTimer: Timer, context: InvocationContext): Promise<void> {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
}
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: timerTriggerWithRetry,
});
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import logging
from azure.functions import AuthLevel, Context, FunctionApp, TimerRequest
app = FunctionApp(http_auth_level=AuthLevel.ANONYMOUS)
@app.timer_trigger(schedule="*/1 * * * * *", arg_name="mytimer",
run_on_startup=False,
use_monitor=False)
@app.retry(strategy="fixed_delay", max_retry_count="3",
delay_interval="00:00:01")
def mytimer(mytimer: TimerRequest, context: Context) -> None:
logging.info(f'Current retry count: {context.retry_context.retry_count}')
if context.retry_context.retry_count == \
context.retry_context.max_retry_count:
logging.info(
f"Max retries of {context.retry_context.max_retry_count} for "
f"function {context.function_name} has been reached")
else:
raise Exception("This is a retryable exception")
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixed_delay` and `exponential_backoff` . |
`max_retry_count` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delay_interval` |
The delay used between retries when you're using a `fixed_delay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimum_interval` |
The minimum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximum_interval` |
The maximum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

```
@FunctionName("TimerTriggerJava1")
@FixedDelayRetry(maxRetryCount = 4, delayInterval = "00:00:10")
public void run(
@TimerTrigger(name = "timerInfo", schedule = "0 */5 * * * *") String timerInfo,
final ExecutionContext context
) {
context.getLogger().info("Java Timer trigger function executed at: " + LocalDateTime.now());
}
```


## Binding error codes

When you're integrating with Azure services, errors might originate from the APIs of the underlying services. Information that relates to binding-specific errors is available in the "Exceptions and return codes" sections of the following articles:

[Azure Cosmos DB](/en-us/rest/api/cosmos-db/http-status-codes-for-cosmosdb)[Blob Storage](functions-bindings-storage-blob-output#exceptions-and-return-codes)[Event Grid](../event-grid/troubleshoot-errors)[Event Hubs](functions-bindings-event-hubs-output#exceptions-and-return-codes)[IoT Hub](functions-bindings-event-iot-output#exceptions-and-return-codes)[Notification Hubs](functions-bindings-notification-hubs#exceptions-and-return-codes)[Queue Storage](functions-bindings-storage-queue-output#exceptions-and-return-codes)[Service Bus](functions-bindings-service-bus-output#exceptions-and-return-codes)[Table Storage](functions-bindings-storage-table-output#exceptions-and-return-codes)


---

<!-- DOCUMENTO FUSIONADO: functions-concurrency.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-concurrency -->

# Concurrency in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, a single function app instance allows for multiple events to be processed concurrently. Because these run on the same compute instance, they share memory, CPU, and connection resources. In certain hosting plans, high demand on a specific instance causes the Functions host to automatically create new instances to handle the increased load. In these *dynamic scale* plans, there's a tradeoff between concurrency and scaling behaviors. To provide more control over how your app runs, Functions provides a way for you to manage the number of concurrent executions.

Functions provides two main ways of managing concurrency:

[Fixed per-instance concurrency](#fixed-per-instance-concurrency): You can configure host-level limits on concurrency that are specific to individual triggers. This model is the default concurrency behavior for Functions.[Dynamic concurrency](#dynamic-concurrency): For certain trigger types, the Functions host can automatically determine the best level of concurrency for that trigger in your function app. You must[opt in to this concurrency model](#dynamic-concurrency-configuration).

This article describes the concurrency behaviors of event-driven triggers in Functions and how these behaviors affect scaling in dynamic plans. It also compares the fixed per-instance and dynamic concurrency models.

## Scaling versus concurrency

For functions that use event-based triggers or respond to HTTP requests, you can quickly reach the limits of concurrent executions during periods of high demand. During such periods, you must be able to scale your function app by adding instances to avoid a backlog in processing incoming requests. The way that we scale your app depends on your hosting plan:

| Scale type | Hosting plans | Description |
|---|---|---|
| Dynamic (event-driven) scaling |
|

[Event-driven scaling in Azure Functions](event-driven-scaling).[Dedicated (App Service) plans](dedicated-plan)[set up an autoscale scheme](dedicated-plan#scaling).Before any scaling might occur, your function app attempts to handle increases in load by handling multiple invocations of the same type in a single instance. As a result, these concurrent executions on a given instance directly impact scale decisions. For instance, when an app in a dynamic scale plan hits a concurrency limit, it might need to scale to keep up with incoming demand.

The balance of scale versus concurrency you try to achieve in your app depends on where bottlenecks might occur: in processing (CPU-intensive process limitations) or in a downstream service (I/O-based limitations).

## Fixed per-instance concurrency

By default, most triggers support a fixed per-instance concurrency configuration model via [target-based scaling](functions-target-based-scaling). In this model, each trigger type has a per-instance concurrency limit.

You can override the concurrency default values for most triggers by setting a specific per-instance concurrency for that trigger type. For many triggers, you configure concurrency settings in the [host.json file](functions-host-json). For example, the [Azure Service Bus trigger](functions-bindings-service-bus-trigger) provides both a `MaxConcurrentCalls`

and a `MaxConcurrentSessions`

setting in *host.json*. These settings work together to control the maximum number of messages that each function app processes concurrently on each instance.

In certain target-based scaling scenarios, such as when you use an Apache Kafka or Azure Cosmos DB trigger, the concurrency configuration is in the function declaration, not in the *host.json* file. Other trigger types have built-in mechanisms for load balancing invocations across instances. For example, Azure Event Hubs and Azure Cosmos DB both use a partition-based scheme.

For trigger types that support concurrency configuration, the concurrency settings are applied to all running instances. This way, you can control the maximum concurrency for your functions on each instance. For example, when your function is CPU-intensive or resource-intensive, you might choose to limit concurrency to keep instances healthy. In this case, you can rely on scaling to handle increased loads. Similarly, when your function makes requests to a downstream service that's being throttled, you should also consider limiting concurrency to avoid overloading the downstream service.

## HTTP trigger concurrency

*Applies only to the Flex Consumption plan*

HTTP trigger concurrency is a special type of fixed per-instance concurrency. In HTTP trigger concurrency, the default concurrency also depends on the [instance size](flex-consumption-plan#instance-sizes).

The Flex Consumption plan scales all HTTP trigger functions together as a group. For more information, see [Per-function scaling](event-driven-scaling#per-function-scaling).

The following table indicates the default concurrency setting for HTTP triggers on a given instance, based on the configured instance memory size:

| Instance size (MB) | Default concurrency* |
|---|---|
| 512 | 4 |
| 2,048 | 16 |
| 4,096 | 32 |

*In Python apps, all instance sizes use an HTTP trigger concurrency level of one by default.

These default values should work well for most cases, and you can start with them. Consider that at a given number of HTTP requests, increasing the HTTP concurrency value reduces the number of instances required to handle HTTP requests. Likewise, decreasing the HTTP concurrency value requires more instances to handle the same load.

If you need to fine-tune the HTTP concurrency, you can do so by using the Azure CLI. For more information, see [Set HTTP concurrency limits](flex-consumption-how-to#set-http-concurrency-limits).

The default concurrency values in the preceding table apply only when you don't set your own HTTP concurrency setting. When you don't explicitly set an HTTP concurrency setting, the default concurrency increases as shown in the table when you change the instance size. After you specifically set an HTTP concurrency value, that value is maintained despite changes in the instance size.

## Determine optimal fixed per-instance concurrency

Fixed per-instance concurrency configurations give you control of certain trigger behaviors, such as throttling your functions. But it can be difficult to determine the optimal values for these settings. Generally, you have to arrive at acceptable values by an iterative process of load testing. Even after you determine a set of values that work for a particular load profile, the number of events that arrive from your connected services can change from day to day. This variability can cause your app to run with suboptimal values. For example, your function app might process demanding message payloads on the last day of the week, which requires you to throttle concurrency down. However, during the rest of the week, the message payloads might be lighter, which means you can use a higher concurrency level the rest of the week.

Ideally, the system should allow instances to process as much work as they can while keeping each instance healthy and latencies low. Dynamic concurrency is designed for that purpose.

## Dynamic concurrency

Functions provides a dynamic concurrency model that simplifies configuring concurrency for all function apps that run in the same plan.

Note

Dynamic concurrency is currently only supported for the Azure Blob Storage, Azure Queue Storage, and Service Bus triggers. Also, you must use the extension versions listed in [Extension support](#extension-support), later in this article.

### Benefits

Dynamic concurrency provides the following benefits:

**Simplified configuration**: You no longer have to manually determine per-trigger concurrency settings. The system learns the optimal values for your workload over time.**Dynamic adjustments**: Concurrency is adjusted up or down dynamically in real time, which allows the system to adapt to changing load patterns over time.**Instance health protection**: The runtime limits concurrency to levels that a function app instance can comfortably handle. These limits protect the app from overloading itself by taking on more work than it should.**Improved throughput**: Overall throughput is improved, because individual instances don't pull more work than they can quickly process. As a result, work is load-balanced more effectively across instances. For functions that can handle higher loads, higher throughput can be obtained by increasing concurrency to values above the default configuration.

### Dynamic concurrency configuration

You can turn on dynamic concurrency at the host level in the *host.json* file. When it's turned on, the concurrency levels of any binding extensions that support this feature are adjusted automatically as needed. In these cases, dynamic concurrency settings override any manually configured concurrency settings.

By default, dynamic concurrency is turned off. When you turn on dynamic concurrency, concurrency starts at a level of one for each function. The concurrency level is adjusted up to an optimal value, which the host determines.

You can turn on dynamic concurrency in your function app by adding the following settings to your *host.json* file:

```
{
"version": "2.0",
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
}
}
```


When `snapshotPersistenceEnabled`

is `true`

, which is the default value, the learned concurrency values are periodically persisted to storage. New instances start from those values instead of starting from a level of one and having to redo the learning.

### Concurrency manager

Behind the scenes, when dynamic concurrency is turned on, a concurrency manager process runs in the background. This manager constantly monitors instance health metrics, like CPU and thread utilization, and changes throttles as needed. When one or more throttles are turned on, function concurrency is adjusted down until the host is healthy again. When throttles are turned off, concurrency can increase. Various heuristics are used to intelligently adjust concurrency up or down as needed based on these throttles. Over time, concurrency for each function stabilizes to a particular level. Because it can take time to determine the optimal concurrency value, use dynamic concurrency only if a suboptimal value is acceptable for your solution initially or after a period of inactivity.

Concurrency levels are managed for each individual function. Specifically, the system balances between resource-intensive functions that require a low level of concurrency and more lightweight functions that can handle higher concurrency. The balance of concurrency for each function helps to maintain the overall health of the function app instance.

When dynamic concurrency is turned on, you find dynamic concurrency decisions in your logs. For example, log entries are added when various throttles are turned on, and whenever concurrency is adjusted up or down for each function. These logs are written under the **Host.Concurrency** log category in the **traces** table.

### Extension support

Dynamic concurrency is enabled for a function app at the host level, and any extensions that support dynamic concurrency run in that mode. Dynamic concurrency requires collaboration between the host and individual trigger extensions. Only the listed versions of the following extensions support dynamic concurrency.

| Extension | Version | Description |
|---|---|---|
Queue Storage |
|

`BatchSize`

and `NewBatchThreshold`

configuration options govern concurrency. When you use dynamic concurrency, those configuration values are ignored. Dynamic concurrency is integrated into the message loop, so the number of messages retrieved per iteration is dynamically adjusted. When throttles are turned on, the host is overloaded. Message processing is paused until the throttles are turned off. When the throttles are turned off, concurrency increases.**Blob Storage**[Version 5.x](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage)(Storage extension)**Service Bus**[Version 5.x](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ServiceBus)**Single dispatch topic/queue processing**: Each invocation of your function processes a single message. When you use a fixed per-instance configuration, the

`MaxConcurrentCalls`

configuration option governs concurrency. When you use dynamic concurrency, that configuration value is ignored, and concurrency is adjusted dynamically.**Session-based single dispatch topic/queue processing**: Each invocation of your function processes a single message. Depending on the number of active sessions for your topic or queue, each instance leases one or more sessions. Messages in each session are processed serially, to guarantee ordering in a session. When you don't use dynamic concurrency, the

`MaxConcurrentSessions`

setting governs concurrency. When dynamic concurrency is turned on, the `MaxConcurrentSessions`

value is ignored, and the number of sessions that each instance processes is dynamically adjusted.**Batch processing**: Each invocation of your function processes a batch of messages, governed by the

`MaxMessageCount`

setting. Because batch invocations are serial, concurrency for your batch-triggered function is always one, and dynamic concurrency doesn't apply.## Next steps

For more information, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: _____index_functions-cli-samples_consumption-plan_functions-identity-access-azur_1d277e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____index_functions-cli-samples_consumption-plan_functions-identity-access-azure_6395b7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___index_functions-cli-samples_consumption-plan_functions-identity-access-azure-_f0c7d0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __index_functions-cli-samples_consumption-plan.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _index_functions-cli-samples.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/ -->

# Azure Functions documentation

Azure Functions is a managed platform-as-a-service (PaaS) provider that provides event-driven and scheduled compute resources for Azure cloud services. You can focus on the code that matters most to you and Functions handles the rest. Functions can provide scalable and serverless hosting for your code projects written in the most productive language for you. You can use Functions to build web APIs, respond to database changes, process IoT streams, manage message queues, and more.

## About Azure Functions

### Overview

### Concept

## Create your first function

### Get started

### Quickstart

## Languages

### Concept

### How-To Guide

## AI integration

### Concept

### Tutorial

### Reference

## Develop functions

### Concept

-
[Azure Functions developer guide](functions-reference) -
[Azure Functions triggers and bindings concepts](functions-triggers-bindings) -
[Code and test Azure Functions locally](functions-develop-local)


---

<!-- DOCUMENTO FUSIONADO: functions-cli-samples.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-cli-samples -->

# Azure CLI Samples

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

These end-to-end Azure CLI scripts are provided to help you learn how to provision and managing the Azure resources required by Azure Functions. You must use the [Azure Functions Core Tools](functions-run-local) to create actual Azure Functions code projects from the command line on your local computer and deploy code to these Azure resources. For a complete end-to-end example of developing and deploying from the command line using both Core Tools and the Azure CLI, see one of these language-specific command line quickstarts:

The following table includes links to bash scripts that you can use to create and manage the Azure resources required by Azure Functions using the Azure CLI.

| Create app | Description |
|---|---|
|

[Create a serverless Python function app](scripts/functions-cli-create-serverless-python)[Create a function app in a scalable Premium plan](scripts/functions-cli-create-premium-plan)[Create a function app in a dedicated (App Service) plan](scripts/functions-cli-create-app-service-plan)| Integrate | Description |
|---|---|
|

[Create a function app and connect to an Azure Cosmos DB](scripts/functions-cli-create-function-app-connect-to-cosmos-db)[Create a Python function app and mount an Azure Files share](scripts/functions-cli-mount-files-storage-linux)| Continuous deployment | Description |
|---|---|
|


---

<!-- DOCUMENTO FUSIONADO: consumption-plan.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/consumption-plan -->

# Azure Functions Consumption plan hosting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you're using the Consumption plan, instances of the Azure Functions host are dynamically added and removed based on the number of incoming events.

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

The Consumption plan scales automatically, even during periods of high load. When running functions in a Consumption plan, you're charged for compute resources only when your functions are running. On a Consumption plan, a function execution times out after a configurable period of time.

Tip

The Flex Consumption plan is now the recommended serverless hosting plan for Azure Functions. It offers faster scaling, reduced cold starts, private networking, and more control over performance and cost. For more information, see [Flex Consumption plan](flex-consumption-plan).

## Billing

Billing is based on number of executions, execution time, and memory used. Usage is aggregated across all functions within a function app. For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).

To learn more about how to estimate costs when running in a Consumption plan, see [Understanding Consumption plan costs](functions-consumption-costs).

## Create a Consumption plan function app

When you create a function app in the Azure portal, the Consumption plan is the default. When using APIs to create your function app, you don't have to first create an App Service plan as you do with Premium and Dedicated plans.

In Consumption plan hosting, each function app typically runs in its own plan. In the Azure portal or in code, you might also see the Consumption plan referred to as `Dynamic`

or `Y1`

.

Use the following links to learn how to create a serverless function app in a Consumption plan, either programmatically or in the Azure portal:

You can also create function apps in a Consumption plan when you publish a Functions project from [Visual Studio Code](how-to-create-function-vs-code#create-the-function-app-in-azure) or [Visual Studio](functions-create-your-first-function-visual-studio#publish-the-project-to-azure).

## Multiple apps in the same plan

The general recommendation is for each function app to have its own Consumption plan. However, if needed, function apps in the same region can be assigned to the same Consumption plan. Keep in mind that there's a [limit to the number of function apps that can run in a Consumption plan](functions-scale#service-limits). Function apps in the same plan still scale independently of each other.


---

<!-- DOCUMENTO FUSIONADO: functions-identity-access-azure-sql-with-managed-identity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-identity-access-azure-sql-with-managed-identity -->

# Tutorial: Connect a function app to Azure SQL with managed identity and SQL bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides a [managed identity](../active-directory/managed-identities-azure-resources/overview), which is a turn-key solution for securing access to [Azure SQL Database](/en-us/azure/sql-database/) and other Azure services. Managed identities make your app more secure by eliminating secrets from your app, such as credentials in the connection strings. In this tutorial, you'll add managed identity to an Azure Function that utilizes [Azure SQL bindings](functions-bindings-azure-sql). A sample Azure Function project with SQL bindings is available in the [ToDo backend example](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/).

When you're finished with this tutorial, your Azure Function will connect to Azure SQL database without the need of username and password.

An overview of the steps you'll take:

## Grant database access to Microsoft Entra user

First enable Microsoft Entra authentication to SQL database by assigning a Microsoft Entra user as the Active Directory admin of the server. This user is different from the Microsoft account you used to sign up for your Azure subscription. It must be a user that you created, imported, synced, or invited into Microsoft Entra ID. For more information on allowed Microsoft Entra users, see [Microsoft Entra features and limitations in SQL database](/en-us/azure/azure-sql/database/authentication-aad-overview#azure-ad-features-and-limitations).

Enabling Microsoft Entra authentication can be completed via the Azure portal, PowerShell, or Azure CLI. Directions for Azure CLI are below and information completing this via Azure portal and PowerShell is available in the [Azure SQL documentation on Microsoft Entra authentication](/en-us/azure/azure-sql/database/authentication-aad-configure).

If your Microsoft Entra tenant doesn't have a user yet, create one by following the steps at

[Add or delete users using Microsoft Entra ID](../active-directory/fundamentals/add-users-azure-active-directory).Find the object ID of the Microsoft Entra user using the

and replace`az ad user list`

*<user-principal-name>*. The result is saved to a variable.For Azure CLI 2.37.0 and newer:

`azureaduser=$(az ad user list --filter "userPrincipalName eq '<user-principal-name>'" --query [].id --output tsv)`

For older versions of Azure CLI:

`azureaduser=$(az ad user list --filter "userPrincipalName eq '<user-principal-name>'" --query [].objectId --output tsv)`

Tip

To see the list of all user principal names in Microsoft Entra ID, run

`az ad user list --query [].userPrincipalName`

.Add this Microsoft Entra user as an Active Directory admin using

command in the Cloud Shell. In the following command, replace`az sql server ad-admin create`

*<server-name>*with the server name (without the`.database.windows.net`

suffix).`az sql server ad-admin create --resource-group myResourceGroup --server-name <server-name> --display-name ADMIN --object-id $azureaduser`


For more information on adding an Active Directory admin, see [Provision a Microsoft Entra administrator for your server](/en-us/azure/azure-sql/database/authentication-aad-configure#provision-azure-ad-admin-sql-database)

## Enable system-assigned managed identity on Azure Function

In this step we'll add a system-assigned identity to the Azure Function. In later steps, this identity will be given access to the SQL database.

To enable system-assigned managed identity in the Azure portal:

- Create an Azure Function in the portal as you normally would. Navigate to it in the portal.
- Scroll down to the Settings group in the left navigation.
- Select Identity.
- Within the System assigned tab, switch Status to On. Click Save.


For information on enabling system-assigned managed identity through Azure CLI or PowerShell, check out more information on [using managed identities with Azure Functions](../app-service/overview-managed-identity?tabs=dotnet&toc=/azure/azure-functions/toc.json#add-a-system-assigned-identity).

Tip

For user-assigned managed identity, switch to the User Assigned tab. Click Add and select a Managed Identity. For more information on creating user-assigned managed identity, see the [Manage user-assigned managed identities](../active-directory/managed-identities-azure-resources/how-manage-user-assigned-managed-identities).

## Grant SQL database access to the managed identity

In this step we'll connect to the SQL database with a Microsoft Entra user account and grant the managed identity access to the database.

Open your preferred SQL tool and login with a Microsoft Entra user account (such as the Microsoft Entra user we assigned as administrator). This can be accomplished in Cloud Shell with the SQLCMD command.

`sqlcmd -S <server-name>.database.windows.net -d <db-name> -U <aad-user-name> -P "<aad-password>" -G -l 30`

In the SQL prompt for the database you want, run the following commands to grant permissions to your function. For example,

`CREATE USER [<identity-name>] FROM EXTERNAL PROVIDER; ALTER ROLE db_datareader ADD MEMBER [<identity-name>]; ALTER ROLE db_datawriter ADD MEMBER [<identity-name>]; GO`

*<identity-name>*is the name of the managed identity in Microsoft Entra ID. If the identity is system-assigned, the name is always the same as the name of your Function app.

## Configure Azure Function SQL connection string

In the final step we'll configure the Azure Function SQL connection string to use Microsoft Entra managed identity authentication.

The connection string setting name is identified in our Functions code as the binding attribute "ConnectionStringSetting", as seen in the SQL input binding [attributes and annotations](functions-bindings-azure-sql-input?pivots=programming-language-csharp#attributes).

In the application settings of our Function App the SQL connection string setting should be updated to follow this format:

`Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; Database=testdb`


*testdb* is the name of the database we're connecting to and *demo.database.windows.net* is the name of the server we're connecting to.

Tip

For user-assigned managed identity, use `Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; User Id=ClientIdOfManagedIdentity; Database=testdb`

.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-errors.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-errors -->

# Azure Functions error handling and retries

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Handling errors in Azure Functions helps you avoid lost data, avoid missed events, and monitor the health of your application. It's also an important way to help you understand the retry behaviors of event-based triggers.

This article describes general strategies for error handling and the available retry strategies.

Important

The preview of retry policy support for certain triggers was removed in December 2022. Retry policies for supported triggers are now in general availability (GA). The [Retries](#retries) section of this article lists extensions that currently support retry policies.

## Handling errors

Errors that occur in an Azure function can come from:

- Use of built-in Azure Functions
[triggers and bindings](functions-triggers-bindings). - Calls to APIs of underlying Azure services.
- Calls to REST endpoints.
- Calls to client libraries, packages, or non-Microsoft APIs.

To avoid loss of data or missed messages, you should practice good error handling. This table describes some recommended error-handling practices and provides links to more information:

| Recommendation | Details |
|---|---|
| Enable Application Insights | Azure Functions integrates with Application Insights to collect error data, performance data, and runtime logs. Use Application Insights to discover and better understand errors that occur in your function executions. To learn more, see
|

[Binding error codes](#binding-error-codes)in this article. Depending on your specific retry strategy, you might also raise a new exception to run the function again.[Retries](#retries)in this article.[Designing Azure Functions for identical input](functions-idempotent).Tip

When you use output bindings, you can't handle errors that occur from accessing the remote service. Because of this behavior, you should validate all data passed to your output bindings to avoid raising any known exceptions. If you must be able to handle such exceptions in your function code, you should access the remote service by using the client SDK instead of relying on output bindings.

## Retries

Two kinds of retries are available for your functions:

- Built-in retry behaviors of individual trigger extensions
- Retry policies that the Azure Functions runtime provides

The following table indicates which triggers support retries and where the retry behavior is configured. It also links to more information about errors that come from the underlying services.

| Trigger/binding | Retry source | Configuration |
|---|---|---|
| Azure Cosmos DB |
|

[Binding extension](functions-bindings-storage-blob-trigger#poison-blobs)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](../event-grid/delivery-and-retry)[Retry policies](#retry-policies)[Retry policies](#retry-policies)[Binding extension](functions-bindings-storage-queue-trigger#poison-messages)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](functions-bindings-rabbitmq-trigger#dead-letter-queues)[Dead letter queue](https://www.rabbitmq.com/dlx.html)[Binding extension](functions-bindings-service-bus-trigger)[host.json](functions-bindings-service-bus#hostjson-settings)*[Retry policies](#retry-policies)* Requires version 5.x of the Azure Service Bus extension. In older extension versions, the [Service Bus dead letter queue](../service-bus-messaging/service-bus-dead-letter-queues#maximum-delivery-count) implements retry behaviors.

## Retry policies

With Azure Functions, you can define retry policies for specific trigger types. The runtime enforces these retry policies. The following trigger types currently support retry policies:

Retry support is the same for both v1 and v2 Python programming models.

Retry policies aren't supported in version 1.x of the Azure Functions runtime.

The retry policy tells the runtime to rerun a failed execution until either successful completion occurs or the maximum number of retries is reached.

A retry policy is evaluated when a function that a supported trigger type executes raises an uncaught exception. As a best practice, you should catch all exceptions in your code and raise new exceptions for any errors that you want to result in a retry.

Important

Event Hubs checkpoints aren't written until after the retry policy for the execution finishes. Because of this behavior, progress on the specific partition is paused until the current batch finishes processing. For more information, see [Reliable event processing with Azure Functions and Event Hubs](functions-reliable-event-processing).

Version 5.x of the Event Hubs extension supports extra retry capabilities for interactions between the Azure Functions host and the event hub. For more information, see `clientRetryOptions`

in the [Event Hubs host.json reference](functions-bindings-event-hubs#host-json).

### Retry strategies

You can configure two retry strategies that are supported by policy:

A specified amount of time is allowed to elapse between each retry.

When you use a Consumption plan, you're billed only for the time that your function code is running. You aren't billed for the wait time between executions in either of these retry strategies.

### Maximum retry counts

You can configure the maximum number of times that a function execution is retried before eventual failure. The current retry count is stored in the memory of the instance.

It's possible for an instance to have a failure between retry attempts. When an instance fails during a retry policy, the retry count is lost. When there are instance failures, the Event Hubs trigger can resume processing and retry the batch on a new instance, with the retry count reset to zero. The timer trigger doesn't resume on a new instance.

This behavior means that the maximum retry count is a best effort. In some rare cases, an execution could be retried more than the requested maximum number of times. For timer triggers, the retries can be less than the requested maximum number.

### Retry examples

Examples are provided for both fixed delay and exponential backoff strategies. To see examples for a specific strategy, you must first select that strategy on the previous tab.

Function-level retries are supported with the following NuGet packages:

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)version 1.9.0 and later[Microsoft.Azure.Functions.Worker.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs)version 5.2.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Kafka](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kafka)version 3.8.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer)version 4.2.0 and later

```
[Function(nameof(TimerFunction))]
[FixedDelayRetry(5, "00:00:10")]
public static void Run([TimerTrigger("0 */5 * * * *")] TimerInfo timerInfo,
FunctionContext context)
{
var logger = context.GetLogger(nameof(TimerFunction));
logger.LogInformation($"Function Ran. Next timer schedule = {timerInfo.ScheduleStatus?.Next}");
}
```


| Property | Description |
|---|---|
`MaxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`DelayInterval` |
The delay used between retries. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a retry policy defined in the `function.json`

file:

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


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
const { app } = require('@azure/functions');
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: (myTimer, context) => {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
},
});
```


The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTriggerWithRetry(myTimer: Timer, context: InvocationContext): Promise<void> {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
}
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: timerTriggerWithRetry,
});
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import logging
from azure.functions import AuthLevel, Context, FunctionApp, TimerRequest
app = FunctionApp(http_auth_level=AuthLevel.ANONYMOUS)
@app.timer_trigger(schedule="*/1 * * * * *", arg_name="mytimer",
run_on_startup=False,
use_monitor=False)
@app.retry(strategy="fixed_delay", max_retry_count="3",
delay_interval="00:00:01")
def mytimer(mytimer: TimerRequest, context: Context) -> None:
logging.info(f'Current retry count: {context.retry_context.retry_count}')
if context.retry_context.retry_count == \
context.retry_context.max_retry_count:
logging.info(
f"Max retries of {context.retry_context.max_retry_count} for "
f"function {context.function_name} has been reached")
else:
raise Exception("This is a retryable exception")
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixed_delay` and `exponential_backoff` . |
`max_retry_count` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delay_interval` |
The delay used between retries when you're using a `fixed_delay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimum_interval` |
The minimum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximum_interval` |
The maximum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

```
@FunctionName("TimerTriggerJava1")
@FixedDelayRetry(maxRetryCount = 4, delayInterval = "00:00:10")
public void run(
@TimerTrigger(name = "timerInfo", schedule = "0 */5 * * * *") String timerInfo,
final ExecutionContext context
) {
context.getLogger().info("Java Timer trigger function executed at: " + LocalDateTime.now());
}
```


## Binding error codes

When you're integrating with Azure services, errors might originate from the APIs of the underlying services. Information that relates to binding-specific errors is available in the "Exceptions and return codes" sections of the following articles:

[Azure Cosmos DB](/en-us/rest/api/cosmos-db/http-status-codes-for-cosmosdb)[Blob Storage](functions-bindings-storage-blob-output#exceptions-and-return-codes)[Event Grid](../event-grid/troubleshoot-errors)[Event Hubs](functions-bindings-event-hubs-output#exceptions-and-return-codes)[IoT Hub](functions-bindings-event-iot-output#exceptions-and-return-codes)[Notification Hubs](functions-bindings-notification-hubs#exceptions-and-return-codes)[Queue Storage](functions-bindings-storage-queue-output#exceptions-and-return-codes)[Service Bus](functions-bindings-service-bus-output#exceptions-and-return-codes)[Table Storage](functions-bindings-storage-table-output#exceptions-and-return-codes)


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-signalr-service-output_functions-bindings-web-pubsub-input.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-signalr-service-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-output -->

# SignalR Service output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the *SignalR* output binding to send one or more messages using Azure SignalR Service. You can broadcast a message to:

- All connected clients
- Connected clients in a specified group
- Connected clients authenticated to a specific user

The output binding also allows you to manage groups, such as adding a client or user to a group, removing a client or user from a group.

For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

### Broadcast to all clients

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a function that sends a message using the output binding to all connected clients. The *newMessage* is the name of the method to be invoked on each client.

```
[Function(nameof(BroadcastToAll))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRMessageAction BroadcastToAll([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
using var bodyReader = new StreamReader(req.Body);
return new SignalRMessageAction("newMessage")
{
// broadcast to all the connected clients without specifying any connection, user or group.
Arguments = new[] { bodyReader.ReadToEnd() },
};
}
```


Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
// You can use any other trigger type instead.
app.http('broadcast', {
methods: ['GET'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"target": "newMessage",
"arguments": [request.body]
});
}
});
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
message = req.get_json()
signalROutput.set(json.dumps({
'target': 'newMessage',
'arguments': [ message ]
}))
```


```
@FunctionName("sendMessage")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRMessage sendMessage(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req) {
SignalRMessage message = new SignalRMessage();
message.target = "newMessage";
message.arguments.add(req.getBody());
return message;
}
```


### Send to a user

You can send a message only to connections that have been authenticated to a user by setting the *user ID* in the SignalR message.

```
[Function(nameof(SendToUser))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRMessageAction SendToUser([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
using var bodyReader = new StreamReader(req.Body);
return new SignalRMessageAction("newMessage")
{
Arguments = new[] { bodyReader.ReadToEnd() },
UserId = "userToSend",
};
}
```


Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
message = req.get_json()
signalROutput.set(json.dumps({
#message will only be sent to this user ID
'userId': 'userId1',
'target': 'newMessage',
'arguments': [ message ]
}))
```


```
@FunctionName("sendMessage")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRMessage sendMessage(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req) {
SignalRMessage message = new SignalRMessage();
message.userId = "userId1";
message.target = "newMessage";
message.arguments.add(req.getBody());
return message;
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
app.http('sendToUser', {
methods: ['GET'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"target": "newMessage",
"arguments": [request.body],
"userId": "userId1",
});
}
});
```


### Send to a group

You can send a message only to connections that have been added to a group by setting the *group name* in the SignalR message.

```
[Function(nameof(SendToGroup))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRMessageAction SendToGroup([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
using var bodyReader = new StreamReader(req.Body);
return new SignalRMessageAction("newMessage")
{
Arguments = new[] { bodyReader.ReadToEnd() },
GroupName = "groupToSend"
};
}
```


Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
app.http('sendToGroup', {
methods: ['GET'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"target": "newMessage",
"arguments": [request.body],
"groupName": "myGroup",
});
}
});
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
message = req.get_json()
signalROutput.set(json.dumps({
#message will only be sent to this group
'groupName': 'myGroup',
'target': 'newMessage',
'arguments': [ message ]
}))
```


```
@FunctionName("sendMessage")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRMessage sendMessage(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req) {
SignalRMessage message = new SignalRMessage();
message.groupName = "myGroup";
message.target = "newMessage";
message.arguments.add(req.getBody());
return message;
}
```


### Group management

SignalR Service allows users or connections to be added to groups. Messages can then be sent to a group. You can use the `SignalR`

output binding to manage groups.

Specify `SignalRGroupActionType`

to add or remove a member. The following example removes a user from a group.

```
[Function(nameof(RemoveFromGroup))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRGroupAction RemoveFromGroup([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
return new SignalRGroupAction(SignalRGroupActionType.Remove)
{
GroupName = "group1",
UserId = "user1"
};
}
```


Note

In order to get the `ClaimsPrincipal`

correctly bound, you must have configured the authentication settings in Azure Functions.

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
// The following function adds a user to a group
app.http('addUserToGroup', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"userId": req.query.userId,
"groupName": "myGroup",
"action": "add"
});
}
});
// The following function removes a user from a group
app.http('removeUserFromGroup', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"userId": req.query.userId,
"groupName": "myGroup",
"action": "remove"
});
}
});
```


Complete PowerShell examples are pending.

The following example adds a user to a group.

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
signalROutput.set(json.dumps({
'userId': 'userId1',
'groupName': 'myGroup',
'action': 'add'
}))
```


The following example removes a user from a group.

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
signalROutput.set(json.dumps({
'userId': 'userId1',
'groupName': 'myGroup',
'action': 'remove'
}))
```


The following example adds a user to a group.

```
@FunctionName("addToGroup")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRGroupAction addToGroup(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req,
@BindingName("userId") String userId) {
SignalRGroupAction groupAction = new SignalRGroupAction();
groupAction.action = "add";
groupAction.userId = userId;
groupAction.groupName = "myGroup";
return action;
}
```


The following example removes a user from a group.

```
@FunctionName("removeFromGroup")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRGroupAction removeFromGroup(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req,
@BindingName("userId") String userId) {
SignalRGroupAction groupAction = new SignalRGroupAction();
groupAction.action = "remove";
groupAction.userId = userId;
groupAction.groupName = "myGroup";
return action;
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

The following table explains the properties of the `SignalROutput`

attribute.

| Attribute property | Description |
|---|---|
HubName |
This value must be set to the name of the SignalR hub for which the connection information is generated. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Annotations

The following table explains the supported settings for the `SignalROutput`

annotation.

| Setting | Description |
|---|---|
name |
Variable name used in function code for connection info object. |
hubName |
This value must be set to the name of the SignalR hub for which the connection information is generated. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `signalR` . |
direction |
Must be set to `out` . |
name |
Variable name used in function code for connection info object. |
hubName |
This value must be set to the name of the SignalR hub for which the connection information is generated. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-web-pubsub-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub-input -->

# Azure Web PubSub input bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Our extension provides two input binding targeting different needs.

-
To let a client connect to Azure Web PubSub Service, it must know the service endpoint URL and a valid access token. The

`WebPubSubConnection`

input binding produces required information, so client doesn't need to handle this token generation itself. The token is time-limited and can authenticate a specific user to a connection. Therefore, don't cache the token or share it between clients. An HTTP trigger working with this input binding can be used for clients to retrieve the connection information. -
When using Static Web Apps,

`HttpTrigger`

is the only supported trigger. In Web PubSub scenarios, the`WebPubSubContext`

input binding helps users deserialize upstream HTTP requests from the service under Web PubSub protocols. So customers can get similar results comparing to`WebPubSubTrigger`

to easily handle in functions. When used with`HttpTrigger`

, customer requires to configure the HttpTrigger exposed url in event handler accordingly.

`WebPubSubConnection`


### Example

The following example shows an HTTP trigger function that acquires Web PubSub connection information using the input binding and returns it over HTTP. In following example, the `UserId`

is passed in through client request query part like `?userid={User-A}`

.

```
[Function("WebPubSubConnectionInputBinding")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[WebPubSubConnectionInput(Hub = "<hub>", , UserId = "{query.userid}", Connection = "<web_pubsub_connection_name>")] WebPubSubConnection connectionInfo)
{
var response = req.CreateResponse(HttpStatusCode.OK);
response.WriteAsJsonAsync(connectionInfo);
return response;
}
```


```
const { app, input } = require('@azure/functions');
const connection = input.generic({
type: 'webPubSubConnection',
name: 'connection',
userId: '{query.userId}',
hub: '<hub>'
});
app.http('negotiate', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [connection],
handler: async (request, context) => {
return { body: JSON.stringify(context.extraInputs.get('connection')) };
},
});
```


Create a folder *negotiate* and update *negotiate/function.json* and copy following JSON codes.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "webPubSubConnection",
"name": "connection",
"userId": "{query.userid}",
"hub": "<hub>",
"direction": "in"
}
]
}
```


Define function in *negotiate/ init.py*.

```
import logging
import azure.functions as func
def main(req: func.HttpRequest, connection) -> func.HttpResponse:
return func.HttpResponse(connection)
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

### Get authenticated user ID

If the function is triggered by an authenticated client, you can add a user ID claim to the generated token. You can easily add authentication to a function app using App Service Authentication.

App Service Authentication sets HTTP headers named `x-ms-client-principal-id`

and `x-ms-client-principal-name`

that contain the authenticated user's client principal ID and name, respectively.

You can set the `UserId`

property of the binding to the value from either header using a binding expression: `{headers.x-ms-client-principal-id}`

or `{headers.x-ms-client-principal-name}`

.

```
[Function("WebPubSubConnectionInputBinding")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[WebPubSubConnectionInput(Hub = "<hub>", , UserId = "{headers.x-ms-client-principal-id}", Connection = "<web_pubsub_connection_name>")] WebPubSubConnection connectionInfo)
{
var response = req.CreateResponse(HttpStatusCode.OK);
response.WriteAsJsonAsync(connectionInfo);
return response;
}
```


```
const { app, input } = require('@azure/functions');
const connection = input.generic({
type: 'webPubSubConnection',
name: 'connection',
userId: '{headers.x-ms-client-principal-id}',
hub: '<hub>'
});
app.http('negotiate', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [connection],
handler: async (request, context) => {
return { body: JSON.stringify(context.extraInputs.get('connection')) };
},
});
```


Create a folder *negotiate* and update *negotiate/function.json* and copy following JSON codes.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "webPubSubConnection",
"name": "connection",
"userId": "{headers.x-ms-client-principal-id}",
"hub": "<hub>",
"direction": "in"
}
]
}
```


Define function in *negotiate/ init.py*.

```
import logging
import azure.functions as func
def main(req: func.HttpRequest, connection) -> func.HttpResponse:
return func.HttpResponse(connection)
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

### Configuration

The following table explains the binding configuration properties that you set in the function.json file and the `WebPubSubConnection`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `webPubSubConnection` |
direction |
n/a | Must be set to `in` |
name |
n/a | Variable name used in function code for input connection binding object. |
hub |
Hub | Required - The value must be set to the name of the Web PubSub hub for the function to be triggered. We support set the value in attribute as higher priority, or it can be set in app settings as a global value. |
userId |
UserId | Optional - the value of the user identifier claim to be set in the access key token. |
clientProtocol |
ClientProtocol | Optional - The client protocol type. Valid values include `default` and `mqtt` . For MQTT clients, you must set it to `mqtt` . For other clients, you can omit the property or set it to `default` . |
connection |
Connection | Required - The name of the app setting that contains the Web PubSub Service connection string (defaults to "WebPubSubConnectionString"). |

### Usage

`WebPubSubConnection`

provides following properties.

| Binding Name | Binding Type | Description |
|---|---|---|
| BaseUri | Uri | Web PubSub client connection uri. |
| Uri | Uri | Absolute Uri of the Web PubSub connection, contains `AccessToken` generated base on the request. |
| AccessToken | string | Generated `AccessToken` based on request UserId and service information. |

`WebPubSubConnection`

provides following properties.

| Binding Name | Description |
|---|---|
| baseUrl | Web PubSub client connection uri. |
| url | Absolute Uri of the Web PubSub connection, contains `AccessToken` generated base on the request. |
| accessToken | Generated `AccessToken` based on request UserId and service information. |

Note

The Web PubSub extensions for Java isn't supported yet.

### More customization of generated token

Limited to the binding parameter types don't support a way to pass list nor array, the `WebPubSubConnection`

isn't fully supported with all the parameters server SDK has, especially `roles`

, and also includes `groups`

and `expiresAfter`

.

When customer needs to add roles or delay building the access token in the function, we suggest you to work with [server SDK for C#](/en-us/dotnet/api/overview/azure/messaging.webpubsub-readme).

```
[Function("WebPubSubConnectionCustomRoles")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req)
{
var serviceClient = new WebPubSubServiceClient(new Uri(endpoint), "<hub>", "<web-pubsub-connection-string>");
var userId = req.Query["userid"].FirstOrDefault();
// your method to get custom roles.
var roles = GetRoles(userId);
var url = await serviceClient.GetClientAccessUriAsync(TimeSpan.FromMinutes(5), userId, roles);
var response = req.CreateResponse(HttpStatusCode.OK);
response.WriteString(url.ToString());
return response;
}
```


When customer needs to add roles or delay building the access token in the function, we suggest you working with [server SDK for JavaScript](/en-us/javascript/api/overview/azure/web-pubsub).

```
const { app } = require('@azure/functions');
const { WebPubSubServiceClient } = require('@azure/web-pubsub');
app.http('negotiate', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
const serviceClient = new WebPubSubServiceClient(process.env.WebPubSubConnectionString, "<hub>");
let token = await serviceClient.getAuthenticationToken({ userId: req.query.userid, roles: ["webpubsub.joinLeaveGroup", "webpubsub.sendToGroup"] });
return { body: token.url };
},
});
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

`WebPubSubContext`


### Example

```
// validate method when upstream set as http://<func-host>/api/{event}
[Function("validate")]
public static HttpResponseData Validate(
[HttpTrigger(AuthorizationLevel.Anonymous, "options")] HttpRequestData req,
[WebPubSubContextInput] WebPubSubContext wpsReq)
{
return BuildHttpResponseData(req, wpsReq.Response);
}
// Respond AbuseProtection to put header correctly.
private static HttpResponseData BuildHttpResponseData(HttpRequestData request, SimpleResponse wpsResponse)
{
var response = request.CreateResponse();
response.StatusCode = (HttpStatusCode)wpsResponse.Status;
response.Body = response.Body;
foreach (var header in wpsResponse.Headers)
{
response.Headers.Add(header.Key, header.Value);
}
return response;
}
```


```
const { app, input } = require('@azure/functions');
const wpsContext = input.generic({
type: 'webPubSubContext',
name: 'wpsContext'
});
app.http('connect', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [wpsContext],
handler: async (request, context) => {
var wpsRequest = context.extraInputs.get('wpsContext');
return { "userId": wpsRequest.request.connectionContext.userId };
}
});
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

### Configuration

The following table explains the binding configuration properties that you set in the functions.json file and the `WebPubSubContext`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `webPubSubContext` . |
direction |
n/a | Must be set to `in` . |
name |
n/a | Variable name used in function code for input Web PubSub request. |
connection |
Connection | Optional - the name of an app settings or setting collection that specifies the upstream Azure Web PubSub service. The value is used for
`null` means the validation isn't needed and always succeed. |

Important

For optimal security, your function app should use managed identities when connecting to the Web PubSub service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize a managed identity request by using Microsoft Entra ID](../azure-web-pubsub/howto-authorize-from-managed-identity).

### Usage

`WebPubSubContext`

provides following properties.

| Binding Name | Binding Type | Description | Properties |
|---|---|---|---|
| request | `WebPubSubEventRequest` |
Request from client, see following table for details. | `WebPubSubConnectionContext` from request header and other properties deserialized from request body describe the request, for example, `Reason` for `DisconnectedEventRequest` . |
| response | `HttpResponseMessage` |
Extension builds response mainly for `AbuseProtection` and errors cases. |
- |
| errorMessage | string | Describe the error details when processing the upstream request. | - |
| hasError | bool | Flag to indicate whether it's a valid Web PubSub upstream request. | - |
| isPreflight | bool | Flag to indicate whether it's a preflight request of `AbuseProtection` . |
- |

For `WebPubSubEventRequest`

, it's deserialized to different classes that provide different information about the request scenario. For `PreflightRequest`

or not valid cases, user can check the flags `IsPreflight`

and `HasError`

to know. We suggest you to return system build response `WebPubSubContext.Response`

directly, or customer can log errors on demand. In different scenarios, customer can read the request properties as following.

| Derived Class | Description | Properties |
|---|---|---|
`PreflightRequest` |
Used in `AbuseProtection` when `IsPreflight` is true |
- |
`ConnectEventRequest` |
Used in system `Connect` event type |
Claims, Query, Subprotocols, ClientCertificates |
`ConnectedEventRequest` |
Used in system `Connected` event type |
- |
`UserEventRequest` |
Used in user event type | Data, DataType |
`DisconnectedEventRequest` |
Used in system `Disconnected` event type |
Reason |

Note

Though the

`WebPubSubContext`

is an input binding provides similar request deserialize way under`HttpTrigger`

comparing to`WebPubSubTrigger`

, there's limitations, i.e. connection state post merge isn't supported. The return response is still respected by the service side, but users require to build the response themselves. If users have needs to set the event response, you should return a`HttpResponseMessage`

contains`ConnectEventResponse`

or messages for user event asresponse bodyand put connection state with key`ce-connectionstate`

inresponse header.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-diagnostics -->

# Azure Functions diagnostics overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you’re running a function app, you want to be prepared for any issues that may arise, from 4xx errors to trigger failures. Azure Functions diagnostics is an intelligent and interactive experience to help you troubleshoot your function app with no configuration or extra cost. When you do run into issues with your function app, Azure Functions diagnostics points out what’s wrong. It guides you to the right information to more easily and quickly troubleshoot and resolve the issue. This article shows you the basics of how to use Azure Functions diagnostics to more quickly diagnose and solve common function app issues.

## Start Azure Functions diagnostics

To start Azure Functions diagnostics:

Navigate to your function app in the

[Azure portal](https://portal.azure.com).Select

**Diagnose and solve problems**to open Azure Functions diagnostics.Choose a category that best describes the issue of your function app by using the keywords in the homepage tile. You can also type a keyword that best describes your issue in the search bar. For example, you could type

`execution`

to see a list of diagnostic reports related to your function app execution and open them directly from the homepage.

## Use the Interactive interface

Once you select a homepage category that best aligns with your function app's problem, Azure Functions diagnostics' interactive interface, named Genie, can guide you through diagnosing and solving problem of your app. You can use the tile shortcuts provided by Genie to view the full diagnostic report of the problem category that you're interested in. The tile shortcuts provide you a direct way of accessing your diagnostic metrics.


After selecting a tile, you can see a list of topics related to the issue described in the tile. These topics provide snippets of notable information from the full report. Select any of these topics to investigate the issues further. Also, you can select **View Full Report** to explore all the topics on a single page.


## View a diagnostic report

After you choose a topic, you can view a diagnostic report specific to your function app. Diagnostic reports use status icons to indicate if there are any specific issues with your app. You see detailed description of the issue, recommended actions, related-metrics, and helpful docs. Customized diagnostic reports are generated from a series of checks run on your function app. Diagnostic reports can be a useful tool for pinpointing problems in your function app and guiding you towards resolving the issue.

## Find the problem code

For script-based functions, you can use **Function Execution and Errors** under **Function App Down or Reporting Errors** to narrow down on the line of code causing exceptions or errors. You can use this tool for getting to the root cause and fixing issues from a specific line of code. This option isn't available for precompiled C# and Java functions.


## Next steps

You can ask questions or provide feedback on Azure Functions diagnostics at [UserVoice](https://feedback.azure.com/d365community/forum/9df02822-f224-ec11-b6e6-000d3a4f0da0). Include `[Diag]`

in the title of your feedback.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-openapi-definition -->

# Expose serverless APIs from HTTP endpoints using Azure API Management

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Azure API Management in the portal to let you expose your HTTP trigger function endpoints as REST APIs. These APIs are described using an OpenAPI definition. This JSON (or YAML) file contains information about what operations are available in an API. It includes details about how the request and response data for the API should be structured. By integrating your function app, you can have API Management generate these OpenAPI definitions.

This article shows you how to integrate your function app with API Management. This integration works for function apps developed in any [supported language](supported-languages). You can also [import your function app from Azure API Management](../api-management/import-function-app-as-api).

For C# class library functions, you can also [use Visual Studio](openapi-apim-integrate-visual-studio) to create and publish serverless API that integrate with API Management.

## Create the API Management instance

To create an API Management instance linked to your function app:

Select the function app, choose

**API Management**from the left menu, and then select**Create new**under**API Management**.Use the API Management settings as specified in the following table:

Setting Suggested value Description **Subscription**Your subscription The subscription under which this new resource is created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The same resource as your function app, which should get set for you. **Region**Location of the service Consider choosing the same location as your function app. **Resource name**Globally unique name A name is generated based on the name of your function app. **Organization name**Contoso The name of the organization used in the developer portal and for email notifications. **Administrator email**your email Email that received system notifications from API Management. **Pricing tier**Consumption Consumption tier isn't available in all regions. For complete pricing details, see the [API Management pricing page](https://azure.microsoft.com/pricing/details/api-management/)Choose

**Review + create**and then**Create**to create the API Management instance, which may take several minutes.

## Import functions

After the API Management instance is created, you can import your HTTP triggered function endpoints. This example imports an endpoint named TurbineRepair.

In the API Management page, select

**Link API**.The

**Import Azure Functions**opens with the**TurbineRepair**function highlighted. Choose**Select**to continue.In the

**Create from Function App**page, accept the defaults, and then select**Create**. Azure creates the API for the function.

## Download the OpenAPI definition

After your functions have been imported, you can download the OpenAPI definition from the API Management instance.

Select

**Download OpenAPI definition**at the top of the page.Save the downloaded JSON file, and then open it. Review the definition.


## Next steps

You can now refine the definition in API Management in the portal. You can also [learn more about API Management](../api-management/api-management-key-concepts).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-maven-intellij -->

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
<!-- Source: N/A -->

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
