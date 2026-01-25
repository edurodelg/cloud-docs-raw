---
source_url: https://learn.microsoft.com/en-us/azure/search/search-indexer-howto-access-private
fetched_at: 2026-01-25T02:05:38.974849
---

# Make outbound connections through a shared private link

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure private, outbound calls from Azure AI Search to an Azure resource that runs within an Azure virtual network.

Setting up a private connection allows a search service to connect to a virtual network IP address instead of a port that's open to the internet. The object created for the connection is called a *shared private link*. On the connection, the search service uses the shared private link internally to reach an Azure resource inside the network boundary.

Shared private link is a premium feature that's billed by usage. When you set up a shared private link, charges for the private endpoint are added to your Azure invoice. As you use the shared private link, data transfer rates for inbound and outbound access are also invoiced. For details, see [Azure Private Link pricing](https://azure.microsoft.com/pricing/details/private-link/).

Note

If you're setting up a private indexer connection to a SQL Managed Instance, see [this article](search-indexer-how-to-access-private-sql) instead for steps specific to that resource type.

## When to use a shared private link

Azure AI Search makes outbound calls to other Azure resources in the following scenarios:

- Knowledge base connections to Azure OpenAI for agentic retrieval workflows
- Indexer or query connections to Azure OpenAI or Azure Vision in Foundry Tools for vectorization
- Indexer connections to supported data sources
- Indexer (skillset) connections to Azure Storage for caching enrichments, debug session sate, or writing to a knowledge store
- Indexer (skillset) connections to Foundry Tools for billing purposes
- Encryption key requests to Azure Key Vault
- Custom skill requests to Azure Functions or similar resource

Shared private links only work for Azure-to-Azure connections. If you're connecting to OpenAI or another external model provider, the connection must be over the public internet.

Shared private links are for operations and data accessed through a [private endpoint](/en-us/azure/private-link/private-endpoint-overview) for Azure resources or clients that run in an Azure virtual network.

A shared private link is:

- Created using Azure AI Search tooling, APIs, or SDKs
- Approved by the Azure resource owner
- Used internally by Azure AI Search on a private connection to a specific Azure resource

Only your search service can use the private links that it creates, and there can be only one shared private link created on your service for each resource and subresource combination.

Once you set up the private link, it's used automatically whenever the search service connects to that resource. You don't need to modify the connection string or alter the client you're using to issue the requests, although the device used for the connection must connect using an authorized IP in the Azure resource's firewall.

There are two scenarios for using [Azure Private Link](/en-us/azure/private-link/private-link-overview) and Azure AI Search together.

Scenario one: create a shared private link when an

*outbound*(indexer or knowledge base) connection to Azure requires a private connection.Scenario two:

[configure search for a private](service-create-private-endpoint)from clients that run in a virtual network.*inbound*connection

Scenario one is covered in this article.

While both scenarios have a dependency on Azure Private Link, they're independent. You can create a shared private link without having to configure your own search service for a private endpoint.

### Limitations

When evaluating shared private links for your scenario, remember these constraints.

Several of the resource types used in a shared private link are in preview. If you're connecting to a preview resource (Azure Database for MySQL or Azure SQL Managed Instance), use a preview version of the Management REST API to create the shared private link. These versions include

`2020-08-01-preview`

,`2021-04-01-preview`

,`2024-03-01-preview`

,`2024-06-01-preview`

, and`2025-02-01-preview`

. We recommend the latest preview API.Indexer execution must use the

[private execution environment](search-howto-run-reset-indexers#indexer-execution-environment)that's specific to your search service. Private endpoint connections aren't supported from the multitenant content processing environment. The configuration setting for this requirement is covered in this article.Review shared private link

[resource limits for each tier](search-limits-quotas-capacity#shared-private-link-resource-limits).The resource type

`Microsoft.CognitiveServices/accounts`

for kind`AIServices`

isn't currently supported. This means that shared private link for Foundry resources with this kind can't be created at this time. If you require to use an Azure OpenAI embedding model for your skill or vectorizer, and need private communication, create an Azure OpenAI resource and a shared private link with the`Microsoft.CognitiveServices/accounts`

with subtype`openai_account`

as a workaround.

## Prerequisites

[A supported Azure resource](#supported-resource-types), configured to run in a virtual network.An Azure AI Search service with tier and region requirements, by workload:

Workload Tier requirements Region requirements Service creation requirements Indexers without skillsets Basic and higher None None Skillsets with embedding skills ( [integrated vectorization](vector-search-integrated-vectorization))Basic and higher [High capacity regions](search-limits-quotas-capacity#partition-storage-gb)[After April 3, 2024](search-how-to-upgrade#check-your-service-creation-or-upgrade-date)Skillsets using other [built-in](cognitive-search-predefined-skills)or custom skillsStandard 1 (S1) and higher None [After April 3, 2024](search-how-to-upgrade#check-your-service-creation-or-upgrade-date)Knowledge bases calling Azure OpenAI for query planning or passing search results Basic and higher None None Permissions on both Azure AI Search and the Azure resource:

Resource Permissions Azure AI Search `Microsoft.Search/searchServices/sharedPrivateLinkResources/write`


`Microsoft.Search/searchServices/sharedPrivateLinkResources/read`


`Microsoft.Search/searchServices/sharedPrivateLinkResources/operationStatuses/read`

Other Azure resource Permission to approve private endpoint connections. For example, on Azure Storage, you need `Microsoft.Storage/storageAccounts/privateEndpointConnectionsApproval/action`

.

### Supported resource types

You can create a shared private link for the following resources.

| Resource type | Subresource (or Group ID) |
|---|---|
Microsoft.Storage/storageAccounts 1 |
`blob` , `table` , `dfs` , `file` |
Microsoft.DocumentDB/databaseAccounts 2 |
`Sql` |
Microsoft.Sql/servers 3 |
`sqlServer` |
| Microsoft.KeyVault/vaults | `vault` |
| Microsoft.DBforMySQL/servers (preview) | `mysqlServer` |
Microsoft.Web/sites 4 |
`sites` |
Microsoft.Sql/managedInstances (preview) 5 |
`managedInstance` |
Microsoft.CognitiveServices/accounts 6 7 |
`openai_account` |
Microsoft.CognitiveServices/accounts 8 |
`cognitiveservices_account` |
Microsoft.Fabric/privateLinkServicesForFabric 9 |
`workspace` |

1 If Azure Storage and Azure AI Search are in the same region, the connection to storage is made over the Microsoft backbone network, which means a shared private link is redundant for this configuration. However, if you already set up a private endpoint for Azure Storage, you should also set up a shared private link or the connection is refused on the storage side. Also, if you're using multiple storage formats for various scenarios in search, make sure to create a separate shared private link for each subresource.

2 The `Microsoft.DocumentDB/databaseAccounts`

resource type is used for indexer connections to Azure Cosmos DB for NoSQL. The provider name and group ID are case-sensitive.

3 The `Microsoft.Sql/servers`

resource type is used for connections to Azure SQL database. There's currently no support for a shared private link to Azure Synapse SQL.

4 The `Microsoft.Web/sites`

resource type is used for App service and Azure functions. In the context of Azure AI Search, an Azure function is the more likely scenario. An Azure function is commonly used for hosting the logic of a custom skill. Azure Function has Consumption, Premium, and Dedicated [App Service hosting plans](/en-us/azure/app-service/overview-hosting-plans). The [App Service Environment (ASE)](/en-us/azure/app-service/environment/overview), [Azure Kubernetes Service (AKS)](/en-us/azure/aks/intro-kubernetes) and [Azure API Management](/en-us/azure/api-management/api-management-key-concepts) aren't supported at this time.

5 See [Create a shared private link for a SQL Managed Instance](search-indexer-how-to-access-private-sql) for instructions.

6 The `Microsoft.CognitiveServices/accounts`

resource type is used for vectorizer and indexer connections to Azure OpenAI embedding models when implementing [integrated vectorization](vector-search-integrated-vectorization). There's support for shared private link to support the Azure Vision multimodal embeddings via [Microsoft Foundry resources](/en-us/azure/ai-services/multi-service-resource).

7 Shared private link for Azure OpenAI is only supported in public cloud and [Microsoft Azure Government](https://azure.microsoft.com/explore/global-infrastructure/government/). Other cloud offerings don't have support for shared private links for `openai_account`

Group ID.

8 Shared private links are supported for connections to Foundry resources. For AI enrichment, Azure AI Search connects to a Foundry resource for [billing purposes](cognitive-search-attach-cognitive-services). These connections can be private through a shared private link, which is only supported when configuring [a managed identity (keyless configuration)](cognitive-search-attach-cognitive-services#bill-through-a-keyless-connection) in the skillset definition.

9 Shared private link is supported for connections to OneLake workspace. To create a `privateLinkServicesForFabric`

resource specific to a workspace, [register](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider) `Microsoft.Fabric`

namespace to your subscription and refer to step 2 as documented in [Create the private link service in Azure](/en-us/fabric/security/security-workspace-level-private-links-set-up#step-2-create-the-private-link-service-in-azure). Note that when using a shared private link, the OneLake data source configuration must be defined with a specific connection string as outlined in the [OneLake indexer documentation](search-how-to-index-onelake-files#define-the-data-source).

## 1 - Create a shared private link

Use the Azure portal, Management REST API, the Azure CLI, or Azure PowerShell to create a shared private link.

Here are a few tips:

- Give the private link a meaningful name. In the Azure PaaS resource, a shared private link appears alongside other private endpoints. A name like "shared-private-link-for-search" can remind you how it's used.

When you complete the steps in this section, you have a shared private link that's provisioned in a pending state. **It takes several minutes to create the link**. Once it's created, the resource owner must approve the request before it's operational.

Sign in to the

[Azure portal](https://portal.azure.com)and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).Under

**Settings**on the left pane, select**Networking**.On the

**Shared Private Access**page, select**+ Add Shared Private Access**.Select either

**Connect to an Azure resource in my directory**or**Connect to an Azure resource by resource ID**.If you select the first option (recommended), the Azure portal helps you pick the appropriate Azure resource and fills in other properties, such as the group ID of the resource and the resource type.

If you select the second option, enter the Azure resource ID manually and choose the appropriate group ID from the list at the beginning of this article.

Confirm the provisioning status is "Updating".

Once the resource is successfully created, the provisioning state of the resource changes to "Succeeded".


### Shared private link creation workflow

A `202 Accepted`

response is returned on success. The process of creating an outbound private endpoint is a long-running (asynchronous) operation. It involves deploying the following resources:

A private endpoint, allocated with a private IP address in a

`"Pending"`

state. The private IP address is obtained from the address space that's allocated to the virtual network of the execution environment for the search service-specific private indexer. Upon approval of the private endpoint, any communication from Azure AI Search to the Azure resource originates from the private IP address and a secure private link channel.A private DNS zone for the type of resource, based on the group ID. By deploying this resource, you ensure that any DNS lookup to the private resource utilizes the IP address that's associated with the private endpoint.


## 2 - Approve the private endpoint connection

Approval of the private endpoint connection is granted on the Azure PaaS side. Explicit approval by the resource owner is required. The following steps cover approval using the Azure portal, but here are some links to approve the connection programmatically from the Azure PaaS side:

- On Azure Storage, use
[Private Endpoint Connections - Put](/en-us/rest/api/storagerp/private-endpoint-connections/put) - On Azure Cosmos DB, use
[Private Endpoint Connections - Create Or Update](/en-us/rest/api/cosmos-db-resource-provider/private-endpoint-connections/create-or-update) - On Azure OpenAI, use
[Private Endpoint Connections - Create Or Update](/en-us/rest/api/aiservices/accountmanagement/private-endpoint-connections/create-or-update?view=rest-aiservices-accountmanagement-2023-05-01&preserve-view=true) - On Microsoft Onelake, use
[Private Endpoints - Approve via CLI](/en-us/cli/azure/network/private-endpoint-connection#az-network-private-endpoint-connection-approve)or[Private Endpoints - Approve via Portal](/en-us/azure/private-link/manage-private-endpoint#manage-private-endpoint-connections-on-azure-paas-resources)

Using the Azure portal, perform the following steps:

Open the

**Networking**page of the Azure PaaS resource.[text](https://ms.portal.azure.com/#blade%2FHubsExtension%2FResourceMenuBlade%2Fid%2F%2Fsubscriptions%2Fa5b1ca8b-bab3-4c26-aebe-4cf7ec4791a0%2FresourceGroups%2Ftest-private-endpoint%2Fproviders%2FMicrosoft.Network%2FprivateEndpoints%2Ftest-private-endpoint)Find the section that lists the private endpoint connections. The following example is for a storage account.

Select the connection, and then select

**Approve**. It can take a few minutes for the status to be updated in the Azure portal.

After the private endpoint is approved, Azure AI Search creates the necessary DNS zone mappings in the DNS zone that's created for it.

Although the private endpoint link on the **Networking** page is active, it won't resolve.


Selecting the link produces an error. A status message of `"The access token is from the wrong issuer"`

and `must match the tenant associated with this subscription`

appears because the backend private endpoint resource is provisioned by Microsoft in a Microsoft-managed tenant, while the linked resource (Azure AI Search) is in your tenant. It's by design you can't access the private endpoint resource by selecting the private endpoint connection link.

Follow the instructions in the next section to check the status of your shared private link.

## 3 - Check shared private link status

On the Azure AI Search side, you can confirm request approval by revisiting the Shared Private Access page of the search service **Networking** page. Connection state should be approved.


Alternatively, you can also obtain connection state by using the [Shared Private Link Resources - Get](/en-us/rest/api/searchmanagement/shared-private-link-resources/get).

```
az rest --method get --uri https://management.azure.com/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/contoso/providers/Microsoft.Search/searchServices/contoso-search/sharedPrivateLinkResources/blob-pe?api-version=2025-09-01
```


This would return a JSON, where the connection state shows up as "status" under the "properties" section. Following is an example for a storage account.

```
{
"name": "blob-pe",
"properties": {
"privateLinkResourceId": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/contoso/providers/Microsoft.Storage/storageAccounts/contoso-storage",
"groupId": "blob",
"requestMessage": "please approve",
"status": "Approved",
"resourceRegion": null,
"provisioningState": "Succeeded"
}
}
```


If the provisioning state (`properties.provisioningState`

) of the resource is "Succeeded" and connection state(`properties.status`

) is "Approved", it means that the shared private link resource is functional and the indexer can be configured to communicate over the private endpoint.

## 4 - Configure the indexer to run in the private environment

[Indexer execution](search-howto-run-reset-indexers#indexer-execution-environment) occurs in either a private environment that's specific to the search service, or a multitenant environment that's used internally to offload expensive skillset processing for multiple customers.

The execution environment is transparent, but once you start building firewall rules or establishing private connections, you must take indexer execution into account. For a private connection, configure indexer execution to always run in the private environment.

This step shows you how to configure the indexer to run in the private environment using the REST API. You can also set the execution environment using the JSON editor in the Azure portal.

Note

You can perform this step before the private endpoint connection is approved. However, until the private endpoint connection shows as approved, any existing indexer that tries to communicate with a secure resource (such as the storage account) will end up in a transient failure state and new indexers will fail to be created.

Create the data source definition, index, and skillset (if you're using one) as you would normally. There are no properties in any of these definitions that vary when using a shared private endpoint.

[Create an indexer](/en-us/rest/api/searchservice/indexers/create)that points to the data source, index, and skillset that you created in the preceding step. In addition, force the indexer to run in the private execution environment by setting the indexer`executionEnvironment`

configuration property to`private`

.`{ "name": "indexer", "dataSourceName": "blob-datasource", "targetIndexName": "index", "parameters": { "configuration": { "executionEnvironment": "private" } }, "fieldMappings": [] }`


After the indexer is created successfully, it should connect to the Azure resource over the private endpoint connection. You can monitor the status of the indexer by using the [Indexer Status API](/en-us/rest/api/searchservice/indexers/get-status).

Note

If you already have existing indexers, you can update them via the [PUT API](/en-us/rest/api/searchservice/indexers/create) by setting the `executionEnvironment`

to `private`

or using the JSON editor in the Azure portal.

## 5 - Test the shared private link

If you haven't done so already, verify that your Azure PaaS resource refuses connections from the public internet. If connections are accepted, review the DNS settings in the

**Networking**page of your Azure PaaS resource.Choose a tool that can invoke an outbound request scenario, such as an indexer connection to a private endpoint. An easy choice is using an

[import wizard](search-get-started-portal), but you can also try a REST client and REST APIs for more precision. Assuming that your search service isn't also configured for a private connection, the REST client connection to search can be over the public internet.Set the connection string to the private Azure PaaS resource. The format of the connection string doesn't change for shared private link. The search service invokes the shared private link internally.

For indexer workloads, the connection string is in the data source definition. An example of a data source might look like this:

`{ "name": "my-blob-ds", "type": "azureblob", "subtype": null, "credentials": { "connectionString": "DefaultEndpointsProtocol=https;AccountName=<YOUR-STORAGE-ACCOUNT>;AccountKey=..." }`

For indexer workloads, remember to set the execution environment in the indexer definition. An example of an indexer definition might look like this:

`"name": "indexer", "dataSourceName": "my-blob-ds", "targetIndexName": "my-index", "parameters": { "configuration": { "executionEnvironment": "private" } }, "fieldMappings": [] }`

Run the indexer. If the indexer execution succeeds and the search index is populated, the shared private link is working.


## Troubleshooting

If your indexer creation fails with "Data source credentials are invalid," check the approval status of the shared private link before debugging the connection. If the status is

`Approved`

, check the`properties.provisioningState`

property. If it's`Incomplete`

, there might be a problem with underlying dependencies. In this case, reissue the`PUT`

request to re-create the shared private link. You might also need to repeat the approval step.If indexers fail consistently or intermittently, check the

on the indexer. The value should be set to`executionEnvironment`

property`private`

. If you didn't set this property, and indexer runs succeeded in the past, it's because the search service used a private environment of its own accord. A search service moves processing out of the multitenant environment if the system is under load.If you get an error when creating a shared private link, check

[service limits](search-limits-quotas-capacity)to verify that you're under the quota for your tier.

## Next steps

Learn more about private endpoints and other secure connection methods: