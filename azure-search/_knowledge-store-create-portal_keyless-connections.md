---
merged_at: 2026-01-25T03:18:14.010372
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: knowledge-store-create-portal.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/knowledge-store-create-portal -->

# Quickstart: Create a knowledge store in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

*Knowledge stores* are secondary storage that exists in Azure Storage and contain the outputs of Azure AI Search skillsets. They're separate from knowledge sources and knowledge bases, which are used in [agentic retrieval](agentic-retrieval-overview) workflows.

In this quickstart, you create a [knowledge store](knowledge-store-concept-intro) that serves as a repository for output generated from an [AI enrichment pipeline](cognitive-search-concept-intro) in Azure AI Search. A knowledge store makes generated content available in Azure Storage for workloads other than search.

First, you set up sample data in Azure Storage. Next, you run the **Import data** wizard to create an enrichment pipeline that also generates a knowledge store. The knowledge store contains original source content pulled from the data source (customer reviews of a hotel), plus AI-generated content that includes a sentiment label, key phrase extraction, and text translation of non-English customer comments.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)or[find an existing service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)in your current subscription. For this quickstart, you can use a free service.An Azure Storage account.

[Create an account](/en-us/azure/storage/common/storage-account-create)or[find an existing account](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Storage%2storageAccounts/). The account type must be**StorageV2 (general purpose V2)**.Sample data hosted in Azure Storage:

[Download HotelReviews_Free.csv](https://github.com/Azure-Samples/azure-search-sample-data/blob/main/hotelreviews/HotelReviews_data.csv), which contains 19 pieces of customer feedback about a single hotel (originates from Kaggle.com). This CSV is in a repo with other sample data. If you don't want the whole repo, copy the raw content and paste it into a spreadsheet app on your device.[Upload the file to a blob container](/en-us/azure/storage/blobs/storage-quickstart-blobs-portal)in Azure Storage.


Note

This quickstart uses [Foundry Tools](https://azure.microsoft.com/services/cognitive-services/) for AI enrichment. Because the workload is so small, Foundry Tools is tapped behind the scenes for free processing for up to 20 transactions. This means that you can complete this exercise without having to create an extra Microsoft Foundry resource.

## Start the wizard

Sign in to the

[Azure portal](https://portal.azure.com/)with your Azure account.[Find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)and on the Overview page, select**Import data**on the command bar to create a knowledge store in four steps.

### Step 1: Create a data source

Because the data is multiple rows in one CSV file, set the *parsing mode* to get one search document for each row.

In

**Connect to your data**, choose**Azure Blob Storage**.For the

**Name**, enter "hotel-reviews-ds".For

**Data to extract**, choose**Content and Metadata**.For

**Parsing mode**, select**Delimited text**, and then select the**First Line Contains Header**checkbox. Make sure the**Delimiter character**is a comma (,).In

**Connection String**, choose an existing connection if the storage account is in the same subscription. Otherwise, paste in a connection string to your Azure Storage account.A connection string can be full access, having the following format:

`DefaultEndpointsProtocol=https;AccountName=<YOUR-ACCOUNT-NAME>;AccountKey=<YOUR-ACCOUNT-KEY>;EndpointSuffix=core.windows.net`

Or, a connection string can reference a managed identity, assuming it's

[configured and assigned a role](search-how-to-managed-identities)in Azure Storage:`ResourceId=/subscriptions/<YOUR-SUBSCRIPTION-ID>/resourceGroups/<YOUR-RESOURCE-GROUP-NAME>/providers/Microsoft.Storage/storageAccounts/<YOUR-ACCOUNT-NAME>;`

In

**Containers**, enter the name of the blob container holding the data ("hotel-reviews").Your page should look similar to the following screenshot.

Continue to the next page.


### Step 2: Add skills

In this wizard step, add skills for AI enrichment. The source data consists of customer reviews in English and French. Skills that are relevant for this data set include key phrase extraction, sentiment detection, and text translation. In a later step, these enrichments are "projected" into a knowledge store as Azure tables.

Expand

**Attach Foundry Tools**.**Free (Limited enrichments)**is selected by default. You can use this resource because the number of records in HotelReviews-Free.csv is 19 and this free resource allows up to 20 transactions a day.Expand

**Add enrichments**.For

**Skillset name**, enter "hotel-reviews-ss".For

**Source data field**, select**reviews_text**.For

**Enrichment granularity level**, select**Pages (5000 characters chunks)**.For

**Text Cognitive Skills**, select the following skills:**Extract key phrases****Translate text****Language detection****Detect sentiment**

Your page should look like the following screenshot:

Scroll down and expand

**Save enrichments to knowledge store**.Select

**Choose an existing connection**and then select an Azure Storage account. The Containers page appears so that you can create a container for projections. We recommend adopting a prefix naming convention, such as "kstore-hotel-reviews" to distinguish between source content and knowledge store content.Returning to the Import data wizard, select the following

**Azure table projections**. The wizard always offers the**Documents**projection. Other projections are offered depending on the skills you select (such as**Key phrases**), or the enrichment granularity (**Pages**):**Documents****Pages****Key phrases**

The following screenshot shows the table projection selections in the wizard.

Continue to the next page.


### Step 3: Configure the index

In this wizard step, configure an index for optional full-text search queries. You don't need a search index for a knowledge store, but the indexer requires one in order to run.

In this step, the wizard samples your data source to infer fields and data types. You only need to select the attributes for your desired behavior. For example, the **Retrievable** attribute allows the search service to return a field value, while the **Searchable** attribute enables full text search on the field.

For

**Index name**, enter "hotel-reviews-idx".For attributes, accept the default selections:

**Retrievable**and**Searchable**for the new fields that the pipeline is creating.Your index should look similar to the following image. Because the list is long, not all fields are visible in the image.

Continue to the next page.


### Step 4: Configure and run the indexer

In this wizard step, configure an indexer that pulls together the data source, skillset, and the index you defined in the previous wizard steps.

For

**Name**, enter "hotel-reviews-idxr".For

**Schedule**, keep the default**Once**.Select

**Submit**to run the indexer. Data extraction, indexing, application of cognitive skills all happen in this step.

### Step 5: Check status

In the **Overview** page, open the **Indexers** tab in the middle of the page, and then select **hotels-reviews-idxr**. Within a minute or two, status should progress from "In progress" to "Success" with zero errors and warnings.

## Check tables in Azure portal

In the Azure portal,

[open the Storage account](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Storage%2storageAccounts/)used to create the knowledge store.In the storage account's left pane, select

**Storage browser**to view the new tables.You should see three tables, one for each projection that was offered in the "Save enrichments" section of the "Add enrichments" page.

"hotelReviewssDocuments" contains all of the first-level nodes of a document's enrichment tree that aren't collections.

"hotelReviewssKeyPhrases" contains a long list of just the key phrases extracted from all reviews. Skills that output collections (arrays), such as key phrases and entities, send output to a standalone table.

"hotelReviewssPages" contains enriched fields created over each page that was split from the document. In this skillset and data source, page-level enrichments consisting of sentiment labels and translated text. A pages table (or a sentences table if you specify that particular level of granularity) is created when you choose "pages" granularity in the skillset definition.


All of these tables contain ID columns to support table relationships in other tools and apps. When you open a table, scroll past these fields to view the content fields added by the pipeline.

In this quickstart, the table for "hotelReviewssPages" should look similar to the following screenshot:


## Clean up

When you're working in your own subscription, it's a good idea at the end of a project to identify whether you still need the resources you created. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

You can find and manage resources in the Azure portal, using the **All resources** or **Resource groups** link in the left-navigation pane.

If you're using a free service, remember that you're limited to three indexes, indexers, and data sources. You can delete individual items in the Azure portal to stay under the limit.

Tip

If you want to repeat this exercise or try a different AI enrichment walkthrough, delete the **hotel-reviews-idxr** indexer and the related objects to recreate them. Deleting the indexer resets the free daily transaction counter to zero.

## Next step

Now that you've been introduced to a knowledge store, take a closer look at each step by completing the REST API walkthrough. The walkthrough explains tasks that the wizard handled internally.


---

<!-- DOCUMENTO FUSIONADO: keyless-connections.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/keyless-connections -->

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
