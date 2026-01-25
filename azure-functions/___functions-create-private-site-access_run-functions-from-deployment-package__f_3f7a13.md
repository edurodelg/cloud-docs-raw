---
merged_at: 2026-01-25T15:41:11.657224
merged_files: 2
---

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
