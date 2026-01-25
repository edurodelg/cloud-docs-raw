---
merged_at: 2026-01-25T02:11:58.365515
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-security-managed-encryption-cross-tenant.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-security-managed-encryption-cross-tenant -->

# Configure customer-managed keys across different tenants

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When Azure Key Vault and Azure AI Search are in different Azure tenants, use a Microsoft Entra multitenant app to enable [customer-managed key (CMK) encryption](search-security-manage-encryption-keys) using a key from another tenant.

## Prerequisites

A tenant containing the search service that has content you want to encrypt. Azure AI Search must be

[configured for role-based access](search-security-enable-roles). Support for CMK requires Basic pricing tier or higher.A separate tenant having the Azure Key Vault and the encryption keys you want to use. Azure Key Vault must be

[configured for role-based access](/en-us/azure/key-vault/general/rbac-guide).Azure CLI for sending requests.


## Create a multitenant Microsoft Entra application in tenant A

Use the Azure CLI to send requests. We refer to the tenant containing Azure AI Search as *tenant A*.

Get the tenant ID:

`az account show --query tenantId --output tsv`

Make sure you're signed in to tenant A:

`az login --tenant <tenant-A-id>`

Create the application registration:

`az ad app create --display-name cross-tenant-auth --sign-in-audience AzureADMultipleOrgs`

Save the app ID output from this step.


## Add a client secret to the multitenant application

To add the client secret to the multitenant application in tenant A, run the following command:

`az ad app credential reset --id <multitenant-app-id>`

Save the password output from this step. The password output is a required input for

[setting up CMK](search-security-manage-encryption-keys)in Azure AI Search.To specify when the client secret expires, you can specify an end-date parameter to this command.

`az ad app credential reset --id <multitenant-app-id> --end-date <end-date>`

The end-date parameter accepts a date in ISO 8601 format. For example:

`az ad app credential reset --id <multitenant-app-id> --end-date 2026-12-31`

.

## Create a service principal in tenant B for the multitenant application

We refer to the tenant containing Azure Key Vault as *tenant B*. In tenant B, create a service principal for the multitenant application in tenant A.

Sign in to tenant B:

`az login --tenant <tenant-B-id>`

Create the service principal using the multitenant app ID output from the first step:

`az ad sp create --id <multitenant-app-id>`

This service principal is an instance of the multitenant application in tenant A. Roles assigned to this service principal in tenant B are also assigned to the multitenant application in tenant A.

Verify the link between tenant A and B by reviewing the "appOwnerOrganizationId" in the following command:

`az ad sp show --id <multitenant-app-id>`

This command displays the service principal details in JSON. Look for the "appOwnerOrganizationId" field in the output to confirm it matches tenant A's ID.

Save the object ID of the service principal (from the

`"id"`

field) from this step. The object ID is a required input for setting up CMK in Azure AI Search.Get the resource ID for Azure Key Vault:

`az keyvault show --name <key-vault-name> --query id --output tsv`

Assign the

**Key Vault Crypto Service Encryption User**role on the key vault in tenant B to the new service principal.`az role assignment create --assignee <service-principal-object-id> --role "Key Vault Crypto Service Encryption User" --scope <key-vault-resource-id>`

An example of this assignment might look like this:

`az role assignment create --assignee 12345678-1234-1234-1234-123456789012 --role "Key Vault Crypto Service Encryption User" --scope /subscriptions/87654321-4321-4321-4321-210987654321/resourceGroups/myKeyVaultRG/providers/Microsoft.KeyVault/vaults/myCompanyKeyVault`


## Test encryption

Create a test index in the search service (tenant A) to validate the setup. Use the multitenant app ID and the credentials you added in the "access credentials" object to authenticate to the key vault in the other tenant.

You can use this sample index schema for testing. You can use the Azure portal to add an index and provide this JSON, or use a [REST client](search-get-started-text) to send a Create Index request.

```
{
"name": "cross-tenant-cmk-test",
"fields": [
{
"name": "id",
"type": "Edm.String",
"key": true
}
],
"encryptionKey": {
"keyVaultUri": "https://myCompanyKeyVault.vault.azure.net/",
"keyVaultKeyName": "search-encryption-key",
"keyVaultKeyVersion": "abc123def456ghi789",
"accessCredentials": {
"applicationId": "12345678-1234-1234-1234-123456789012",
"applicationSecret": "secretValueFromStep2"
}
}
}
```


Verify the index was created successfully:

```
GET https://<search-service>.search.windows.net/indexes/cross-tenant-cmk-test?api-version=2025-09-01
```


For more information about how to rotate or manage keys, see [Configure customer-managed keys for data encryption](search-security-manage-encryption-keys).


---

<!-- DOCUMENTO FUSIONADO: search-multi-region.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-multi-region -->

# Multi-region deployments in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Although Azure AI Search is a single-region service, you can achieve higher availability and resiliency by deploying multiple search services with identical configurations and content across multiple regions.

This article describes the components of a multi-region solution, which relies on your custom script or code to handle failover if a service becomes unavailable.

For more information about the reliability features of Azure AI Search, including intra-regional resiliency via availability zones, see [Reliability in Azure AI Search](/en-us/azure/reliability/reliability-ai-search).

## Why use multiple regions?

If you need two or more search services, creating them in different regions can meet the following operational requirements:

**Resiliency to region outages**. If there's an outage, Azure AI Search doesn't provide instant failover to another region.**Fast performance for a globally distributed application**. If indexing and query requests come from around the world, users who are closest to the host data center experience faster performance. Creating more services in regions with close proximity to these users can equalize performance for everyone.

## Multi-region architecture

In a multi-region setup, two or more search services are located in different regions and have synchronized indexes. Users are automatically routed to the service with the lowest latency.

Azure AI Search doesn't provide an automated method of index replication across regions. However, you can synchronize data using [push or pull model indexing](search-what-is-data-import), both of which are described in the following section. You can also add Azure Traffic Manager or another load balancer for [request redirection](#request-failover-and-redirection).

The following diagram illustrates a geo-distributed set of search services:

Tip

For a complete implementation, see the [Bicep sample](https://github.com/Azure-Samples/azure-search-multiple-regions) on GitHub. The sample deploys a fully configured, multi-region search solution that can be modified to your regions and indexing strategies.

## Data synchronization

To synchronize two or more distinct search services, you can either:

- Push content into an index using
[Documents - Index (REST API)](/en-us/rest/api/searchservice/documents/)or an equivalent API in the Azure SDKs. - Pull content into an index using an
[indexer](search-indexer-overview).

If you use the REST APIs to [push content into your index](search-what-is-data-import#pushing-data-to-an-index), you can synchronize multiple search services by sending updates to each service whenever changes occur. Ensure that your code handles cases in which an update fails for one service but succeeds for other services.

## Data residency

When you create multiple search services in different regions, your content is stored in the region you chose for each service.

Azure AI Search doesn't store data outside of your specified region without your authorization. Authorization is implicit when you use features that write to Azure Storage, for which you provide a storage account in your preferred region. These features include:

If your search service and storage account are in the same region, network traffic uses private IP addresses over the Microsoft backbone network, so you can't configure IP firewalls or private endpoints for network security. As an alternative, use the [trusted service exception](search-indexer-howto-access-trusted-service-exception).

## Request failover and redirection

For redundancy at the request level, Azure provides several [load-balancing options](/en-us/azure/architecture/guide/technology-choices/load-balancing-overview):

Use [Azure Application Gateway](/en-us/azure/application-gateway/overview) to load balance between servers in a region at the application layer.

By default, service endpoints are accessed through a public internet connection. Use Application Gateway if you set up a private endpoint for client connections that originate from within a virtual network.

As you evaluate these load-balancing options, consider the following points:

Azure AI Search is a backend service that accepts indexing and query requests from a client.

By default, service endpoints are accessed through a public internet connection. We recommend

[Azure Application Gateway](/en-us/azure/application-gateway/overview)for private endpoints that originate from within a virtual network.Azure AI Search accepts requests addressed to the

`<your-search-service-name>.search.windows.net`

endpoint. If you reach the same endpoint using a different DNS name in the host header, such as a CNAME, the request is rejected.Requests from the client to a search service must be authenticated. To access search operations, the caller must have

[role-based permissions](search-security-rbac)or provide an[API key](search-security-api-keys)with the request.
