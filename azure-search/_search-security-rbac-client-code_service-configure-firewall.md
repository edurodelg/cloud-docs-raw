---
merged_at: 2026-01-25T02:11:58.445433
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-security-rbac-client-code.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-security-rbac-client-code -->

# Connect your app to Azure AI Search using identities

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In your application code, you can set up a keyless connection to Azure AI Search that uses Microsoft Entra ID and roles for authentication and authorization. Application requests to most Azure services must be authenticated with keys or keyless connections. Developers must be diligent to never expose the keys in an unsecure location. Anyone who gains access to the key is able to authenticate to the service. Keyless authentication offers improved management and security benefits over the account key because there's no key (or connection string) to store.

This article explains how to use `DefaultAzureCredential`

in your application code.

To implement keyless connections in your code, follow these steps:

- Enable role-based access on your search service
- Set environment variables, as needed.
- Use an Azure Identity library credential type to create an Azure AI Search client object.

## Prerequisites

[Azure AI Search](search-create-service-portal), any region but it must be a billable tier (basic or higher).[Role-based access enabled](search-security-enable-roles)on your search service.Role assignments on Azure AI Search. Assign these roles to your identity:

**Search Service Contributor**and**Search Index Data Contributor**for local development (full access)**Search Index Data Reader**for production read-only queries

For step-by-step instructions, see

[Assign roles for development](search-security-rbac#assign-roles-for-development).

## Install Azure Identity client library

To use a keyless approach, update your AI Search enabled code with the Azure Identity client library.

Install the [Azure Identity client library for .NET](https://www.nuget.org/packages/Azure.Identity) and the [Azure Search Documents client library](https://www.nuget.org/packages/Azure.Search.Documents):

```
dotnet add package Azure.Identity
dotnet add package Azure.Search.Documents
```


## Update source code to use DefaultAzureCredential

The Azure Identity library's `DefaultAzureCredential`

allows you to run the same code in the local development environment and in the Azure cloud. Create a single credential and reuse the credential instance as needed to take advantage of token caching.

For more information on `DefaultAzureCredential`

for .NET, see [Azure Identity client library for .NET](/en-us/dotnet/api/overview/azure/identity-readme#defaultazurecredential).

```
using Azure;
using Azure.Search.Documents;
using Azure.Search.Documents.Indexes;
using Azure.Search.Documents.Indexes.Models;
using Azure.Search.Documents.Models;
using Azure.Identity;
using System;
using static System.Environment;
string endpoint = GetEnvironmentVariable("AZURE_SEARCH_ENDPOINT");
string indexName = "my-search-index";
DefaultAzureCredential credential = new();
SearchClient searchClient = new(new Uri(endpoint), indexName, credential);
SearchIndexClient searchIndexClient = new(endpoint, credential);
```


**Reference:** [SearchClient](/en-us/dotnet/api/azure.search.documents.searchclient), [SearchIndexClient](/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient), [DefaultAzureCredential](/en-us/dotnet/api/azure.identity.defaultazurecredential)

## Verify your connection

After setting up the client, verify your connection by running a simple operation. The following example lists indexes on your search service:

```
// List indexes to verify connection
var indexes = searchIndexClient.GetIndexNames();
foreach (var name in indexes)
{
Console.WriteLine(name);
}
```


A successful connection prints the names of your indexes (or an empty list if no indexes exist). If you receive an authentication error, verify that role-based access is enabled and your identity has the required role assignments.

The default authority is Azure public cloud. Custom `audience`

values for sovereign or specialized clouds include:

`https://search.azure.us`

for Azure Government`https://search.azure.cn`

for Azure operated by 21Vianet`https://search.microsoftazure.de`

for Azure Germany

## Local development

Local development using roles includes these steps:

- Assign your personal identity to RBAC roles on the specific resource.
- Use a tool like the Azure CLI or Azure PowerShell to authenticate with Azure.
- Establish environment variables for your resource.

### Roles for local development

As a local developer, your Azure identity needs full control over data plane operations. These are the suggested roles:

- Search Service Contributor, create and manage objects
- Search Index Data Contributor, load and query an index

Find your personal identity with one of the following tools. Use that identity as the `<identity-id>`

value.

Replace placeholders `<role-name>`

, `<identity-id>`

, `<subscription-id>`

, and `<resource-group-name>`

with your actual values in the following commands.

Sign in to Azure CLI.

`az login`

A browser window opens for authentication. After successful sign-in, the terminal displays your subscription information.

Get your personal identity.

`az ad signed-in-user show \ --query id -o tsv`

The command returns your user object ID (a GUID). Save this value for the next step.

Assign the role-based access control (RBAC) role to the identity for the resource group.

`az role assignment create \ --role "<role-name>" \ --assignee "<identity-id>" \ --scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>"`

A successful assignment returns a JSON object with the role assignment details.


### Authentication for local development

Use a tool in your local development environment to authentication to Azure identity. Once you're authenticated, the `DefaultAzureCredential`

instance in your source code finds and uses your identity for authentication purposes.

Select a tool for [authentication during local development](/en-us/python/api/overview/azure/identity-readme#authenticate-during-local-development).

### Configure environment variables for local development

To connect to Azure AI Search, your code needs to know your resource endpoint.

Create an environment variable named `AZURE_SEARCH_ENDPOINT`

for your Azure AI Search endpoint. This URL generally has the format `https://<YOUR-RESOURCE-NAME>.search.windows.net/`

.

## Production workloads

Deploy production workloads includes these steps:

- Choose RBAC roles that adhere to the principle of least privilege.
- Assign RBAC roles to your production identity on the specific resource.
- Set up environment variables for your resource.

### Roles for production workloads

To create your production resources, you need to create a [user-assigned managed identity](/en-us/entra/identity/managed-identities-azure-resources/how-manage-user-assigned-managed-identities?pivots=identity-mi-methods-azp#create-a-user-assigned-managed-identity) then assign that identity to your resources with the correct roles.

The following role is suggested for a production application:

| Role name | Id |
|---|---|
| Search Index Data Reader | 1407120a-92aa-4202-b7e9-c0e197c71c8f |

### Authentication for production workloads

Use the following Azure AI Search **Bicep template** to create the resource and set the authentication for the `identityId`

. Bicep requires the role ID. The `name`

shown in this Bicep snippet isn't the Azure role; it's specific to the Bicep deployment.

```
// main.bicep
param environment string = 'production'
param roleGuid string = ''
module aiSearchRoleUser 'core/security/role.bicep' = {
scope: aiSearchResourceGroup
name: 'aiSearch-role-user'
params: {
principalId: (environment == 'development') ? principalId : userAssignedManagedIdentity.properties.principalId
principalType: (environment == 'development') ? 'User' : 'ServicePrincipal'
roleDefinitionId: roleGuid
}
}
```


The `main.bicep`

file calls the following generic Bicep code to create any role. You have the option to create multiple RBAC roles, such as one for the user and another for production. This allows you to enable both development and production environments within the same Bicep deployment.

```
// core/security/role.bicep
metadata description = 'Creates a role assignment for an identity.'
param principalId string // passed in from main.bicep
@allowed([
'Device'
'ForeignGroup'
'Group'
'ServicePrincipal'
'User'
])
param principalType string = 'ServicePrincipal'
param roleDefinitionId string // Role ID
resource role 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, resourceGroup().id, principalId, roleDefinitionId)
properties: {
principalId: principalId
principalType: principalType
roleDefinitionId: resourceId('Microsoft.Authorization/roleDefinitions', roleDefinitionId)
}
}
```


### Configure environment variables for production workloads

To connect to Azure AI Search, your code needs to know your resource endpoint, and the ID of the managed identity.

Create environment variables for your deployed and keyless Azure AI Search resource:

`AZURE_SEARCH_ENDPOINT`

: This URL is the access point for your Azure AI Search resource. This URL generally has the format`https://<YOUR-RESOURCE-NAME>.search.windows.net/`

.`AZURE_CLIENT_ID`

: This is the identity to authenticate as.

## Troubleshoot common errors

| Error | Cause | Solution |
|---|---|---|
`AuthenticationFailedException` |
Missing or invalid credentials | Ensure you're signed in with `az login` (CLI) or `Connect-AzAccount` (PowerShell). Verify your Azure account has access to the subscription. |
`403 Forbidden` |
Identity lacks required role | Assign the appropriate role (Search Index Data Reader for queries, Search Index Data Contributor for indexing). Role assignments can take up to 10 minutes to propagate. |
`401 Unauthorized` |
RBAC not enabled on search service | Enable role-based access in the Azure portal under Settings > Keys > Role-based access control. |
`ResourceNotFoundException` |
Invalid endpoint or index name | Verify the `AZURE_SEARCH_ENDPOINT` environment variable matches your search service URL (format: `https://<service-name>.search.windows.net` ). |
`CredentialUnavailableException` |
No valid credential found | `DefaultAzureCredential` tries multiple authentication methods. Ensure at least one is configured (Azure CLI, Visual Studio, environment variables). |


---

<!-- DOCUMENTO FUSIONADO: service-configure-firewall.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/service-configure-firewall -->

# Configure network access and firewall rules for Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to restrict network access to a search service's public endpoint. You can configure IP firewall rules to allow only specific IP addresses, ranges, or subnets, and optionally enable exceptions for trusted Azure services.

To block *all* data plane access to the public endpoint, use [private endpoints](service-create-private-endpoint) instead.

## Prerequisites

-
[Azure AI Search service](search-create-service-portal)(Basic tier or higher). Firewall configuration isn't supported on the Free tier.

**Owner**or**Contributor**role on the search service resource.You can also use the

[Management REST API](/en-us/rest/api/searchmanagement/),[Azure PowerShell](/en-us/powershell/module/az.search), or the[Azure CLI](/en-us/cli/azure/search)instead of the Azure portal.

## Configure network access in the Azure portal

Sign in to Azure portal and

[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).Under

**Settings**, select**Networking**on the leftmost pane. If you don't see this option, check your service tier. Networking options are available on the Basic tier and higher.Choose

**Selected IP addresses**. Avoid the**Disabled**option unless you're configuring a[private endpoint](service-create-private-endpoint).Under

**IP Firewall**, select**Add your client IP address**. This step creates an inbound rule for the public IP address of your personal device to Azure AI Search. See[Allow access from the Azure portal IP address](#allow-access-from-the-azure-portal-ip-address)for details.Add other client IP addresses for other devices and services that send requests to a search service.

Specify IP addresses and ranges in the CIDR format. An example of CIDR notation is 8.8.8.0/24, which represents the IPs that range from 8.8.8.0 to 8.8.8.255.

To get the public IP addresses of Azure services, see

[Azure IP Ranges and Service Tags](https://www.microsoft.com/download/details.aspx?id=56519). If your search client is hosted within an Azure function, see[IP addresses in Azure Functions](/en-us/azure/azure-functions/ip-addresses).Under

**Exceptions**, select**Allow Azure services on the trusted services list to access this search service**.The trusted service list includes:

`Microsoft.CognitiveServices`

for Azure OpenAI and Foundry Tools`Microsoft.MachineLearningServices`

for Azure Machine Learning

When you enable this exception, you take a dependency on Microsoft Entra ID authentication, managed identities, and role assignments. Any Foundry Tool or AML feature that has a valid role assignment on your search service can bypass the firewall. See

[Grant access to trusted services](#grant-access-to-trusted-azure-services)for more details.**Save**your changes.

After you enable the IP access control policy for your Azure AI Search service, all requests to the data plane from machines outside the allowed list of IP address ranges are rejected.

When requests originate from IP addresses that aren't in the allowed list, a generic **403 Forbidden** response is returned with no other details.

Important

It can take several minutes for changes to take effect. Wait at least 15 minutes before troubleshooting any problems related to network configuration.

## Allow access from the Azure portal IP address

The Azure portal has its own connection to Azure AI Search, separate from your local device and browser. If you use the Azure portal to manage your search service, you need to add the portal IP address as described in this section, and your client IP address as described in the previous section.

When IP rules are configured, some features of the Azure portal are disabled. For example, you can view and manage service level information, but portal access to the import wizards, indexes, indexers, and other top-level resources are restricted.

You can restore the Azure portal's access to the full range of search service operations by adding the Azure portal IP address to the restricted address range.

To get the Azure portal's IP address, perform `nslookup`

(or `ping`

) on:

`stamp2.ext.search.windows.net`

, which is the domain of the traffic manager for the Azure public cloud.`stamp2.ext.search.azure.us`

for Azure Government cloud.

For nslookup, the IP address is visible in the "Non-authoritative answer" portion of the response. In the following example, the IP address that you should copy is `52.252.175.48`

.

```
$ nslookup stamp2.ext.search.windows.net
Server: ZenWiFi_ET8-0410
Address: 192.168.50.1
Non-authoritative answer:
Name: azsyrie.northcentralus.cloudapp.azure.com
Address: 52.252.175.48
Aliases: stamp2.ext.search.windows.net
azs-ux-prod.trafficmanager.net
azspncuux.management.search.windows.net
```


The IP address in the `Address`

field (52.252.175.48 in this example) is the value to add to your firewall rules.

**Reference:** [nslookup command](/en-us/windows-server/administration/windows-commands/nslookup)

When services run in different regions, they connect to different traffic managers. Regardless of the domain name, the IP address returned from the ping is the correct one to use when defining an inbound firewall rule for the Azure portal in your region.

For ping, the request times out, but the IP address is visible in the response. For example, in the message `"Pinging azsyrie.northcentralus.cloudapp.azure.com [52.252.175.48]"`

, the IP address is `52.252.175.48`

.

A banner informs you that IP rules affect the Azure portal experience. This banner remains visible even after you add the Azure portal's IP address. Remember to wait several minutes for network rules to take effect before testing.

## Grant access to trusted Azure services

Did you select the trusted services exception? If yes, your search service admits requests and responses from a trusted Azure resource without checking for an IP address. A trusted resource must have a managed identity (either system or user-assigned, but usually system). A trusted resource must have a role assignment on Azure AI Search that gives it permission to data and operations.

The trusted service list for Azure AI Search includes:

`Microsoft.CognitiveServices`

for Azure OpenAI and Foundry Tools`Microsoft.MachineLearningServices`

for Azure Machine Learning

Workflows for this network exception are requests originating from Microsoft Foundry or other AML features to Azure AI Search. The trusted services exception is typically for [Azure OpenAI On Your Data](/en-us/azure/ai-services/openai/concepts/use-your-data) scenarios for retrieval augmented generation (RAG) and playground environments.

### Trusted resources must have a managed identity

To set up managed identities for Azure OpenAI and Azure Machine Learning:

[How to configure Azure OpenAI in Foundry Models with managed identities](/en-us/azure/ai-services/openai/how-to/managed-identity)[How to set up authentication between Azure Machine Learning and other services](/en-us/azure/machine-learning/how-to-identity-based-service-authentication).

To set up a managed identity for a Foundry resource:

From the left pane, select

**Resource management**>**Identity**.Set

**System assigned**to**On**.

### Trusted resources must have a role assignment

Once your Azure resource has a managed identity, [assign roles on Azure AI Search](search-security-rbac-client-code) to grant permissions to data and operations.

The trusted services are used for vectorization workloads: generating vectors from text and image content, and sending payloads back to the search service for query execution or indexing. Connections from a trusted service are used to deliver payloads to Azure AI search.

On the leftmost pane, under

**Access control (IAM)**, select**Identity**.Select

**Add**and then select**Add role assignment**.On the

**Roles**page:- Select
**Search Index Data Contributor**to load a search index with vectors generated by an embedding model. Choose this role if you intend to use integrated vectorization during indexing. - Or, select
**Search Index Data Reader**to provide queries containing a vector generated by an embedding model at query time. The embedding used in a query isn't written to an index, so no write permissions are required.

- Select
Select

**Next**.On the

**Members**page, select**Managed identity**and**Select members**.Filter by system-managed identity and then select the managed identity of your Foundry resource.


Note

This article covers the trusted exception for admitting requests to your search service, but Azure AI Search is itself on the trusted services list of other Azure resources. Specifically, you can use the trusted service exception for [connections from Azure AI Search to Azure Storage](search-indexer-howto-access-trusted-service-exception).

## Limitations and considerations

Consider the following when configuring network access:

Some workflows require access to a public endpoint. Specifically, the

in the Azure portal connects to built-in (hosted) sample data and embedding models over a public endpoint. For more information, see**Import data wizard**[Secure connections in the import wizards](search-import-data-portal#secure-connections).If you're in early stages of proof-of-concept testing with sample data, you might want to defer network access controls until you actually need them.

Network rules are scoped to data plane operations against the search service's public endpoint (creating or querying indexes, and all other actions described by the

[Search REST APIs](/en-us/rest/api/searchservice/)).For control plane operations that target service administration, refer to the

[network protections supported by Azure Resource Manager](/en-us/security/benchmark/azure/baselines/azure-resource-manager-security-baseline).

## Next steps

Once a request is allowed through the firewall, it must be authenticated and authorized. You have two options:

[Key-based authentication](search-security-api-keys), where an admin or query API key is provided on the request. This option is the default.[Role-based access control](search-security-rbac)using Microsoft Entra ID, where the caller is a member of a security role on a search service. This is the most secure option. It uses Microsoft Entra ID for authentication and role assignments on Azure AI Search for permissions to data and operations.
