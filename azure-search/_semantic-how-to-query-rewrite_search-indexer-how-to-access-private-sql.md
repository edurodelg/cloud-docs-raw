---
merged_at: 2026-01-25T03:18:14.043698
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: semantic-how-to-query-rewrite.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/semantic-how-to-query-rewrite -->

# Rewrite queries with semantic ranker in Azure AI Search (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Query rewriting is the process of transforming a user's query into a more effective one, adding more terms and refining search results. The search service sends the search query (or a variation of it) to a generative model that generates alternative queries.

Query rewriting improves results from [semantic ranking](search-get-started-semantic) by correcting typos or spelling errors in user queries, and expanding queries with synonyms.

Search with query rewriting works like this:

- The user query is sent via the
`search`

property in the request. - The search service sends the search query (or a variation of it) to a generative model that generates alternative queries.
- The search service uses the original query and the rewritten queries to retrieve search results.

Query rewriting is an optional feature. Without query rewriting, the search service just uses the original query to retrieve search results.

Note

The rewritten queries might not contain all of the exact terms the original query had. This might impact search results if the query was highly specific and required exact matches for unique identifiers or product codes.

## Prerequisites

[Azure AI Search](search-create-service-portal)in any[region that provides query rewrite](search-region-support), with[semantic ranker enabled](semantic-how-to-enable-disable).An existing search index with a

[semantic configuration](semantic-how-to-configure)and rich text content. The examples in this guide use the[hotels-sample-index](search-get-started-portal)sample data to demonstrate query rewriting.To follow the instructions in this article, you need a web client that supports REST API requests. The examples in this article were tested with

[Visual Studio Code](https://code.visualstudio.com/download)and the[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)extension.

Tip

Content that includes explanations or definitions work best for semantic ranking.

## Make a search request with query rewrites

In this REST API example, use [Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to formulate the request.

Paste the following request into a web client as a template.

`POST https://[search-service-name].search.windows.net/indexes/hotels-sample-index/docs/search?api-version=2025-11-01-preview { "search": "newer hotel near the water with a great restaurant", "semanticConfiguration":"en-semantic-config", "queryType":"semantic", "queryRewrites":"generative|count-5", "queryLanguage":"en-US", "debug":"queryRewrites", "top": 1 }`

Replace

`search-service-name`

with your search service name.Replace

`hotels-sample-index`

with your index name if it's different.Set "search" to a full text search query. The search property is required for query rewriting, unless you specify

[vector queries](#vector-queries-with-query-rewrite). If you specify vector queries, then the "search" text must match the`"text"`

property of the`"vectorQueries"`

object. Your search string can support either the[simple syntax](query-simple-syntax)or[full Lucene syntax](query-lucene-syntax).Set "semanticConfiguration" to a

[predefined semantic configuration](semantic-how-to-configure)embedded in your index.Set "queryType" to "semantic". You either need to set "queryType" to "semantic" or include a nonempty "semanticQuery" property in the request.

[Semantic ranking](semantic-search-overview)is required for query rewriting.Set "queryRewrites" to "generative|count-5" to get up to five query rewrites. You can set the count to any value between 1 and 10.

Since you requested query rewrites by setting the "queryRewrites" property, you must set "queryLanguage" to the search text language. The search service uses the same language for the query rewrites. In this example, you use "en-US". The supported locales are:

`en-AU`

,`en-CA`

,`en-GB`

,`en-IN`

,`en-US`

,`ar-EG`

,`ar-JO`

,`ar-KW`

,`ar-MA`

,`ar-SA`

,`bg-BG`

,`bn-IN`

,`ca-ES`

,`cs-CZ`

,`da-DK`

,`de-DE`

,`el-GR`

,`es-ES`

,`es-MX`

,`et-EE`

,`eu-ES`

,`fa-AE`

,`fi-FI`

,`fr-CA`

,`fr-FR`

,`ga-IE`

,`gl-ES`

,`gu-IN`

,`he-IL`

,`hi-IN`

,`hr-BA`

,`hr-HR`

,`hu-HU`

,`hy-AM`

,`id-ID`

,`is-IS`

,`it-IT`

,`ja-JP`

,`kn-IN`

,`ko-KR`

,`lt-LT`

,`lv-LV`

,`ml-IN`

,`mr-IN`

,`ms-BN`

,`ms-MY`

,`nb-NO`

,`nl-BE`

,`nl-NL`

,`no-NO`

,`pa-IN`

,`pl-PL`

,`pt-BR`

,`pt-PT`

,`ro-RO`

,`ru-RU`

,`sk-SK`

,`sl-SL`

,`sr-BA`

,`sr-ME`

,`sr-RS`

,`sv-SE`

,`ta-IN`

,`te-IN`

,`th-TH`

,`tr-TR`

,`uk-UA`

,`ur-PK`

,`vi-VN`

,`zh-CN`

,`zh-TW`

.Set "debug" to "queryRewrites" to get the query rewrites in the response.

Tip

Only set

`"debug": "queryRewrites"`

for testing purposes. For better performance, don't use debug in production.Set "top" to 1 to return only the top search result.


Send the request to execute the query and return results.


Next, you evaluate the search results with the query rewrites.

## Evaluate the response

Here's an example of a response that includes query rewrites:

```
"@search.debug": {
"semantic": null,
"queryRewrites": {
"text": {
"inputQuery": "newer hotel near the water with a great restaurant",
"rewrites": [
"new waterfront hotels with top-rated eateries",
"new waterfront hotels with top-rated restaurants",
"new waterfront hotels with excellent dining",
"new waterfront hotels with top-rated dining",
"new water-side hotels with top-rated restaurants"
]
},
"vectors": []
}
},
"value": [
{
"@search.score": 58.992092,
"@search.rerankerScore": 2.815633535385132,
"HotelId": "18",
"HotelName": "Ocean Water Resort & Spa",
"Description": "New Luxury Hotel for the vacation of a lifetime. Bay views from every room, location near the pier, rooftop pool, waterfront dining & more.",
"Description_fr": "Nouvel h\u00f4tel de luxe pour des vacances inoubliables. Vue sur la baie depuis chaque chambre, emplacement pr\u00e8s de la jet\u00e9e, piscine sur le toit, restaurant au bord de l'eau et plus encore.",
"Category": "Luxury",
"Tags": [
"view",
"pool",
"restaurant"
],
"ParkingIncluded": true,
"LastRenovationDate": "2020-11-14T00:00:00Z",
"Rating": 4.2,
"Location": {
"type": "Point",
"coordinates": [
-82.537735,
27.943701
],
"crs": {
"type": "name",
"properties": {
"name": "EPSG:4326"
}
}
},
//... more properties redacted for brevity
}
]
```


Here are some key points to note:

- Because you set the "debug" property to "queryRewrites" for testing, the response includes a
`@search.debug`

object with the text input query and query rewrites. - Because you set the "queryRewrites" property to "generative|count-5", the response includes up to five query rewrites.
- The
`"inputQuery"`

value is the query sent to the generative model for query rewriting. The input query isn't always the same as the user's`"search"`

query.

Here's an example of a response without query rewrites.

```
"@search.debug": {
"semantic": null,
"queryRewrites": {
"text": {
"inputQuery": "",
"rewrites": []
},
"vectors": []
}
},
"value": [
{
"@search.score": 7.774868,
"@search.rerankerScore": 2.815633535385132,
"HotelId": "18",
"HotelName": "Ocean Water Resort & Spa",
"Description": "New Luxury Hotel for the vacation of a lifetime. Bay views from every room, location near the pier, rooftop pool, waterfront dining & more.",
"Description_fr": "Nouvel h\u00f4tel de luxe pour des vacances inoubliables. Vue sur la baie depuis chaque chambre, emplacement pr\u00e8s de la jet\u00e9e, piscine sur le toit, restaurant au bord de l'eau et plus encore.",
"Category": "Luxury",
"Tags": [
"view",
"pool",
"restaurant"
],
"ParkingIncluded": true,
"LastRenovationDate": "2020-11-14T00:00:00Z",
"Rating": 4.2,
"Location": {
"type": "Point",
"coordinates": [
-82.537735,
27.943701
],
"crs": {
"type": "name",
"properties": {
"name": "EPSG:4326"
}
}
},
//... more properties redacted for brevity
}
]
```


## Vector queries with query rewrite

You can include vector queries in your search request to combine keyword search and vector search into a single request and a unified response.

Here's an example of a query that includes a vector query with query rewrites. Modify a [previous example](#make-a-search-request-with-query-rewrites) to include a vector query.

- Add a "vectorQueries" object to the request. This object includes a vector query with the "kind" set to "text".
- The "text" value is the same as the "search" value. These values must be identical for query rewriting to work.

```
POST https://[search-service-name].search.windows.net/indexes/hotels-sample-index/docs/search?api-version=2025-11-01-preview
{
"search": "newer hotel near the water with a great restaurant",
"vectorQueries": [
{
"kind": "text",
"text": "newer hotel near the water with a great restaurant",
"k": 50,
"fields": "Description",
"queryRewrites": "generative|count-3"
}
],
"semanticConfiguration":"en-semantic-config",
"queryType":"semantic",
"queryRewrites":"generative|count-5",
"queryLanguage":"en-US",
"top": 1
}
```


The response includes query rewrites for both the text query and the vector query.

## Test query rewrites with debug

You should test your query rewrites to ensure that they're working as expected. Set the `"debug": "queryRewrites"`

property in your query request to get the query rewrites in the response. Setting `"debug"`

is optional for testing purposes. For better performance, don't set this property in production.

### Partial response reasons

You might observe that the debug (test) response includes an empty array for the `text.rewrites`

and `vectors`

properties.

```
{
"@odata.context": "https://demo-search-svc.search.windows.net/indexes('hotels-sample-index')/$metadata#docs(*)",
"@search.debug": {
"semantic": null,
"queryRewrites": {
"text": {
"rewrites": []
},
"vectors": []
}
},
"@search.semanticPartialResponseReason": "Transient",
"@search.semanticQueryRewriteResultType": "OriginalQueryOnly",
//... more properties redacted for brevity
}
```


In the preceding example:

- The response includes a
`@search.semanticPartialResponseReason`

property with a value of "Transient". This message means that at least one of the queries failed to complete. - The response also includes a
`@search.semanticQueryRewriteResultType`

property with a value of "OriginalQueryOnly". This message means that the query rewrites are unavailable. Only the original query is used to retrieve search results.

## Next steps

Semantic ranking can be used in hybrid queries that combine keyword search and vector search into a single request and a unified response.


---

<!-- DOCUMENTO FUSIONADO: search-indexer-how-to-access-private-sql.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-indexer-how-to-access-private-sql -->

# Create a shared private link for a SQL managed instance from Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure an indexer in Azure AI Search for a private connection to a SQL managed instance that runs within a virtual network. The private connection is through a [shared private link](search-indexer-howto-access-private) and Azure Private Link.

On a private connection to a managed instance, the fully qualified domain name (FQDN) of the instance must include the [DNS Zone](/en-us/azure/azure-sql/managed-instance/connectivity-architecture-overview#virtual-cluster-connectivity-architecture). Currently, only the Azure AI Search Management REST API provides a `dnsZonePrefix`

parameter for accepting the DNS zone specification.

Although you can call the Management REST API directly, it's easier to use the Azure CLI `az rest`

module to send Management REST API calls from a command line. This article uses the Azure CLI with REST to set up the private link.

Note

This article refers to Azure portal for obtaining properties and confirming steps. However, when creating the shared private link for SQL Managed Instance, make sure you're using the REST API. Although the Networking tab lists `Microsoft.Sql/managedInstances`

as an option, the Azure portal doesn't currently support the extended URL format used by SQL Managed Instance.

## Prerequisites

Azure AI Search, Basic or higher. If you're using

[AI enrichment](cognitive-search-concept-intro)and skillsets, use Standard 2 (S2) or higher. See[Service limits](search-limits-quotas-capacity#shared-private-link-resource-limits)for details.Azure SQL Managed Instance, configured to run in a virtual network.

You should have a minimum of Contributor permissions on both Azure AI Search and SQL Managed Instance.

Azure SQL Managed Instance connection string. Managed identity isn't currently supported with shared private link. Your connection string must include a user name and password.


Note

Shared private links are billable through [Azure Private Link pricing](https://azure.microsoft.com/pricing/details/private-link/) and charges are invoiced based on usage.

## 1 - Retrieve connection information

In this section, get the DNS zone from the host name and a connection string.

In Azure portal, find the SQL managed instance object.

On the

**Overview**tab, locate the Host property. Copy the*DNS zone*portion of the FQDN for the next step. The DNS zone is part of the domain name of the SQL Managed Instance. For example, if the FQDN of the SQL Managed Instance is`my-sql-managed-instance.a1b22c333d44.database.windows.net`

, the DNS zone is`a1b22c333d44`

.On the

**Connection strings**tab, copy the ADO.NET connection string for a later step. It's needed for the data source connection when testing the private connection.

For more information about connection properties, see [Create an Azure SQL Managed Instance](/en-us/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql#retrieve-connection-details-to-sql-managed-instance&preserve-view=true).

## 2 - Create the body of the request

Using a text editor, create the JSON for the shared private link.

`{ "name": "{{shared-private-link-name}}", "properties": { "privateLinkResourceId": "/subscriptions/{{target-resource-subscription-ID}}/resourceGroups/{{target-resource-rg}}/providers/Microsoft.Sql/managedInstances/{{target-resource-name}}", "dnsZonePrefix": "a1b22c333d44", "groupId": "managedInstance", "requestMessage": "please approve" } }`

Provide a meaningful name for the shared private link. The shared private link appears alongside other private endpoints. A name like "shared-private-link-for-search" can remind you how it's used.

Paste in the DNS zone name in "dnsZonePrefix" that you retrieved in an earlier step.

Edit the "privateLinkResourceId", substitute valid for values for the placeholders. Provide a valid subscription ID, resource group name, and managed instance name.

Save the file locally as

*create-pe.json*(or use another name, remembering to update the Azure CLI syntax in the next step).In the Azure CLI, type

`dir`

to note the current location of the file.

## 3 - Create a shared private link

From the command line, sign into Azure using

`az login`

.If you have multiple subscriptions, make sure you're using the one you intend to use:

`az account show`

.To set the subscription, use

`az account set --subscription {{subscription ID}}`

Call the

`az rest`

command to use the[Management REST API](/en-us/rest/api/searchmanagement)of Azure AI Search.Because shared private link support for SQL managed instances is still in preview, you need a preview version of the management REST API. Use

`2021-04-01-preview`

or a later preview API version for this step. We recommend using the latest preview API version.`az rest --method put --uri https://management.azure.com/subscriptions/{{search-service-subscription-ID}}/resourceGroups/{{search service-resource-group}}/providers/Microsoft.Search/searchServices/{{search-service-name}}/sharedPrivateLinkResources/{{shared-private-link-name}}?api-version=2025-05-01-preview --body @create-pe.json`

Provide the subscription ID, resource group name, and service name of your Azure AI Search resource.

Provide the same shared private link name that you specified in the JSON body.

Provide a path to the

*create-pe.json*file if you've navigated away from the file location. You can type`dir`

at the command line to confirm the file is in the current directory.Run the command.


When you complete these steps, you should have a shared private link that's provisioned in a pending state. **It takes several minutes to create the link**. Once it's created, the resource owner needs to approve the request before it's operational.

You can check the status of the shared private link in the Azure portal. On your search service page, under **Settings** > **Properties**, scroll down to find the shared private link resources and view the JSON value. When the provisioning state changes from *pending* to *succeeded*, you can continue on to the next step.

## 4 - Approve the private endpoint connection

On the SQL Managed Instance side, the resource owner must approve the private connection request you created.

In the Azure portal, open the

**Security**>**Private endpoint connections**of the managed instance.Find the section that lists the private endpoint connections.

Select the connection, and then select

**Approve**. It can take a few minutes for the status to be updated in the Azure portal.

After the private endpoint is approved, Azure AI Search creates the necessary DNS zone mappings in the DNS zone that's created for it.

## 5 - Check shared private link status

On the Azure AI Search side, you can confirm request approval by revisiting the Shared Private Access tab of the search service **Networking** page. Connection state should be approved.

## 6 - Configure the indexer to run in the private environment

You can now configure an indexer and its data source to use an outbound private connection to your managed instance.

This article assumes a [REST client](search-get-started-text) and uses the REST APIs.

[Create the data source definition](search-how-to-index-sql-database)as you would normally for Azure SQL. By default, a managed instance listens on port 3342, but on a virtual network it listens on 1433.Provide the connection string that you copied earlier with an Initial Catalog set to your database name.

`POST https://myservice.search.windows.net/datasources?api-version=2025-09-01 Content-Type: application/json api-key: admin-key { "name" : "my-sql-datasource", "description" : "A database for testing Azure AI Search indexes.", "type" : "azuresql", "credentials" : { "connectionString" : "Server=tcp:contoso.a1b22c333d44.database.windows.net,1433;Persist Security Info=false; User ID=<your user name>; Password=<your password>;MultipleActiveResultsSets=False; Encrypt=True;Connection Timeout=30;Initial Catalog=<your database name>" }, "container" : { "name" : "Name of table or view to index", "query" : null (not supported in the Azure SQL indexer) }, "dataChangeDetectionPolicy": null, "dataDeletionDetectionPolicy": null, "encryptionKey": null }`

[Create the indexer definition](search-howto-create-indexers), setting the indexer`executionEnvironment`

to "private".[Indexer execution](search-howto-run-reset-indexers#indexer-execution-environment)occurs in either a private execution environment that's specific to your search service, or a multitenant environment hosted by Microsoft and used to offload expensive skillset processing for multiple customers.**When connecting over a private endpoint, indexer execution must be private.**`POST https://myservice.search.windows.net/indexers?api-version=2025-09-01 Content-Type: application/json api-key: admin-key { "name": "indexer", "dataSourceName": "my-sql-datasource", "targetIndexName": "my-search-index", "parameters": { "configuration": { "executionEnvironment": "private" } }, "fieldMappings": [] }`

Run the indexer. If the indexer execution succeeds and the search index is populated, the shared private link is working.


You can monitor the status of the indexer in Azure portal or by using the [Indexer Status API](/en-us/rest/api/searchservice/indexers/get-status).

You can use [ Search explorer](search-explorer) in Azure portal to check the contents of the index.

## 7 - Test the shared private link

If you ran the indexer in the previous step and successfully indexed content from your managed instance, then the test was successful. However, if the indexer fails or there's no content in the index, you can modify your objects and repeat testing by choosing any client that can invoke an outbound request from an indexer.

An easy choice is [running an indexer](search-howto-run-reset-indexers) in Azure portal, but you can also try a [REST client](search-get-started-text) and REST APIs for more precision. Assuming that your search service isn't also configured for a private connection, the REST client connection to Azure AI Search can be over the public internet.

Here are some reminders for testing:

If you use a REST client, use the

[Management REST API](/en-us/rest/api/searchmanagement/)and the[2021-04-01-Preview API version](/en-us/rest/api/searchmanagement/management-api-versions)to create the shared private link. Use the[Search REST API](/en-us/rest/api/searchservice/)and a[stable API version](/en-us/rest/api/searchservice/search-service-api-versions)to create and invoke indexers and data sources.You can use the Import data wizard to create an indexer, data source, and index. However, the generated indexer won't have the correct execution environment setting.

You can edit data source and indexer JSON in Azure portal to change properties, including the execution environment and the connection string.

You can reset and rerun the indexer in Azure portal. Reset is important for this scenario because it forces a full reprocessing of all documents.

You can use Search explorer to check the contents of the index.
