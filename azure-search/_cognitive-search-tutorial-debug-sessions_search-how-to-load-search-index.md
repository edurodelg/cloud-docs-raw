---
merged_at: 2026-01-25T02:11:58.522577
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-tutorial-debug-sessions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-tutorial-debug-sessions -->

# Tutorial: Fix a skillset using Debug Sessions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, a skillset coordinates the actions of skills that analyze, transform, or create searchable content. Frequently, the output of one skill becomes the input of another. When inputs depend on outputs, mistakes in skillset definitions and field associations can result in missed operations and data.

**Debug Sessions** is an Azure portal tool that provides a holistic visualization of a skillset that executes on Azure AI Search. Using this tool, you can drill down to specific steps to easily see where an action might be falling down.

In this tutorial, you use **Debug Sessions** to find and fix missing inputs and outputs. The tutorial is all-inclusive. It provides sample data, a REST file that creates objects, and instructions for debugging problems in the skillset.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).Azure AI Search.

[Create a service](search-create-service-portal)or[find an existing service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)in your current subscription. You can use a free service for this tutorial. The Free tier doesn't provide managed identity support for an Azure AI Search service. You must use keys for connections to Azure Storage.Azure Storage account with

[Blob storage](/en-us/azure/storage/blobs/), used for hosting sample data and for persisting cached data created during a debug session. If you're using a free search service, the storage account must have shared access keys enabled and it must allow public network access.[Visual Studio Code](https://code.visualstudio.com/download)with a[REST client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client).[Sample debug-sessions.rest file](https://github.com/Azure-Samples/azure-search-rest-samples/blob/main/debug-sessions/debug-sessions.rest)used to create the enrichment pipeline.

Note

This tutorial also uses [Foundry Tools](https://azure.microsoft.com/services/cognitive-services/) for language detection, entity recognition, and key phrase extraction. Because the workload is so small, Foundry Tools is tapped behind the scenes for free processing for up to 20 transactions. This means that you can complete this exercise without having to create a billable Microsoft Foundry resource.

## Set up the sample data

This section creates the sample data set in Azure Blob Storage so that the indexer and skillset have content to work with.

[Download sample data (clinical-trials-pdf-19)](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/_ARCHIVE/clinical-trials/clinical-trials-pdf-19), consisting of 19 files.[Create an Azure Storage account](/en-us/azure/storage/common/storage-account-create?tabs=azure-portal)or[find an existing account](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Storage%2storageAccounts/).Choose the same region as Azure AI Search to avoid bandwidth charges.

Choose the StorageV2 (general purpose V2) account type.


Go to the Azure Storage services pages in the Azure portal and create a Blob container. Best practice is to specify the access level "private". Name your container

`clinicaltrialdataset`

.In container, select

**Upload**to upload the sample files you downloaded and unzipped in the first step.In the Azure portal, select

**Settings**>**Access Keys**and copy the connection string for Azure Storage.

## Copy a key and URL

This tutorial uses API keys for authentication and authorization. You need the search service endpoint and an API key, which you can get from the Azure portal.

Sign in to the

[Azure portal](https://portal.azure.com), go to the**Overview**page, and copy the URL. An example endpoint might look like`https://mydemo.search.windows.net`

.Under

**Settings**>**Keys**, copy an admin key. Admin keys are used to add, modify, and delete objects. There are two interchangeable admin keys. Copy either one.

A valid API key establishes trust, on a per-request basis, between the application sending the request and the search service handling it.

## Create data source, skillset, index, and indexer

In this section, create a "buggy" workflow that you can fix in this tutorial.

Start Visual Studio Code and open the

`debug-sessions.rest`

file.Provide the following variables: search service URL, search services admin API key, storage connection string, and the name of the blob container storing the PDFs.

Send each request in turn. Creating the indexer takes several minutes to complete.

Close the file.


## Check results in the Azure portal

The sample code intentionally creates a buggy index as a consequence of problems that occurred during skillset execution. The problem is that the index is missing data.

In Azure portal, on the search service

**Overview**page, select the**Indexes**tab.Select

*clinical-trials*.Enter this JSON query string in Search explorer's JSON view. It returns fields for specific documents (identified by the unique

`metadata_storage_path`

field).`"search": "*", "select": "metadata_storage_path, organizations, locations", "count": true`

Run the query. You should see empty values for

`organizations`

and`locations`

.These fields should have been populated through the skillset's

[Entity Recognition skill](cognitive-search-skill-entity-recognition-v3), used to detect organizations and locations anywhere within the blob's content. In the next exercise, you debug the skillset to determine what went wrong.

Another way to investigate errors and warnings is through the Azure portal.

On the

**Indexers**tab, select*clinical-trials-idxr*.Notice that while the indexer job succeeded overall, there were warnings.

Select

**Success**to view the warnings. If there are mostly errors, the detail link is**Failed**. You should see a long list of every warning emitted by the indexer.

## Start your debug session

From the search service left-navigation pane, under

**Search management**, select**Debug sessions**.Select

**+ Add Debug Session**.Give the session a name.

In Indexer template, provide the indexer name. The indexer has references to the data source, the skillset, and index.

Select the storage account.

**Save**the session.A debug session opens to the settings page. You can make modifications to the initial configuration and override any defaults. A debug session only works with a single document. The default is to accept the first document in the collection as the basis of your debug sessions. You can

[choose a specific document to debug](cognitive-search-how-to-debug-skillset#create-a-debug-session)by providing its URI in Azure Storage.When the debug session finishes initializing, you should see a skills workflow with mappings and a search index. The enriched document data structure appears in a details pane on the side. We excluded it from the following screenshot so that you could see more of the workflow.


## Find issues with the skillset

Any issues reported by the indexer are indicated as **Errors** and **Warnings**.

Notice that the number of errors and warnings is a smaller list than the one displayed earlier because this list is only detailing the errors for a single document. Like the list displayed by the indexer, you can select on a warning message and see the details of this warning.

Select **Warnings** to review the notifications. You should see four:

"Could not execute skill because one or more skill inputs were invalid. Required skill input is missing. Name: 'text', Source: '/document/content'."

"Could not map output field 'locations' to search index. Check the 'outputFieldMappings' property of your indexer. Missing value '/document/merged_content/locations'."

"Could not map output field 'organizations' to search index. Check the 'outputFieldMappings' property of your indexer. Missing value '/document/merged_content/organizations'."

"Skill executed but may have unexpected results because one or more skill inputs were invalid. Optional skill input is missing. Name: 'languageCode', Source: '/document/languageCode'. Expression language parsing issues: Missing value '/document/languageCode'."


Many skills have a "languageCode" parameter. By inspecting the operation, you can see that this language code input is missing from the `EntityRecognitionSkill.#1`

, which is the same entity recognition skill that is having trouble with 'locations' and 'organizations' output.

Because all four notifications are about this skill, your next step is to debug this skill. If possible, start by solving input issues first before moving on to output issues.

## Fix missing skill input values

On the work surface, select the skill that's reporting the warnings. In this tutorial, it's the entity recognition skill.

The Skill details pane opens to the right with sections for iterations and their respective inputs and outputs, skill settings for the JSON definition of the skill, and messages for any errors and warnings that this skill is emitting.

Hover over each input (or select an input) to show the values in the

**Expression evaluator**. Notice that the displayed result for this input doesn’t look like a text input. It looks like a series of new line characters`\n \n\n\n\n`

instead of text. The lack of text means that no entities can be identified. Either this document doesn't meet the prerequisites of the skill, or there's another input that should be used instead.Switch back to

**Enriched data structure**and review the enrichment nodes for this document. Notice the`\n \n\n\n\n`

for "content" has no originating source, but another value for "merged_content" has OCR output. Although there's no indication, the content of this PDF appears to be a JPEG file, as evidenced by the extracted and processed text in "merged_content".Switch back to the skill and select

**Skillset settings**to open the JSON definition.Change the expression from

`/document/content`

to`/document/merged_content`

, and then select**Save**. Notice that the warning is no longer listed.Select

**Run**in the session's window menu. This kicks off another execution of the skillset using the document.Once the debug session execution completes, notice that the warnings count has reduced by one. Warnings show that the error for text input is gone, but the other warnings remain. The next step is to address the warning about the missing or empty value

`/document/languageCode`

.Select the skill and hover over

`/document/languageCode`

. The value for this input is null, which isn't a valid input.As with the previous issue, start by reviewing the

**Enriched data structure**for evidence of its nodes. Notice that there's no "languageCode" node, but there's one for "language". So, there's a typo in the skill settings.Copy the expression

`/document/language`

.In the Skill details pane, select

**Skill Settings**for the #1 skill and paste the new value,`/document/language`

.Select

**Save**.Select

**Run**.After the debug session execution completes, you can check the results in the Skills detail pane. When you hover over

`/document/language`

, you should see`en`

as the value in the**Expression evaluator**.

Notice that the input warnings are gone. There now remain just the two warnings about output fields for organizations and locations.

## Fix missing skill output values

The messages say to check the 'outputFieldMappings' property of your indexer, so lets start there.

Select

**Output Field Mappings**on the work surface. Notice that the output field mappings are missing.As a first step, confirm that the search index has the expected fields. In this case, the index has fields for "locations" and "organizations".

If there's no problem with the index, the next step is to check skill outputs. As before, select the

**Enriched data structure**, and scroll the nodes to find "locations" and "organizations". Notice that the parent is "content" instead of "merged_content". The context is wrong.Switch back to Skills detail pane for the entity recognition skill.

In

**Skill Settings**, change`context`

to`document/merged_content`

. At this point, you should have three modifications to the skill definition altogether.Select

**Save**.Select

**Run**.

All of the errors are resolved.

## Commit changes to the skillset

When the debug session was initiated, the search service created a copy of the skillset. This was done to protect the original skillset on your search service. Now that you debugged your skillset, the fixes can be committed (overwrite the original skillset).

Alternatively, if you aren't ready to commit changes, you can save the debug session and reopen it later.

Select

**Commit changes**in the main Debug sessions menu.Select

**OK**to confirm that you wish to update your skillset.Close Debug session and open

**Indexers**from the left pane.Select 'clinical-trials-idxr'.

Select

**Reset**.Select

**Run**.Select

**Refresh**to show the status of the reset and run commands.

When the indexer finishes running, there should be a green checkmark and the word Success next to the time stamp for the latest run in the **Execution history** tab. To ensure that the changes are applied:

In the left pane, open

**Indexes**.Select 'clinical-trials' index and in the Search explorer tab, enter this query string:

`$select=metadata_storage_path, organizations, locations&$count=true`

to return fields for specific documents (identified by the unique`metadata_storage_path`

field).Select

**Search**.

The results should show that organizations and locations are now populated with the expected values.

## Clean up resources

When you're working in your own subscription, it's a good idea at the end of a project to identify whether you still need the resources you created. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

You can find and manage resources in the Azure portal, using the **All resources** or **Resource groups** link in the left-navigation pane.

The free service is limited to three indexes, indexers, and data sources. You can delete individual items in the Azure portal to stay under the limit.

## Next steps

This tutorial touched on various aspects of skillset definition and processing. To learn more about concepts and workflows, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: search-how-to-load-search-index.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-load-search-index -->

# Load data into a search index in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to import documents into a predefined search index using REST APIs, Azure SDKs, or the Azure portal.

Tip

For the fastest path to loading data, use the [Import data wizard](search-import-data-portal) in the Azure portal, which creates an index and loads it in one workflow.

## Prerequisites

An Azure AI Search service (any tier).

[Create a service](search-create-service-portal)or[find an existing one](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).An existing search index. This article assumes you already

[created an index](search-how-to-create-search-index). If you need to create and load in one step, use an[Import wizard](search-import-data-portal)or[indexer](search-indexer-overview).Permissions to load documents:

**Key-based authentication**: An[admin API key](search-security-api-keys)for your search service.**Role-based authentication**:[Search Index Data Contributor](search-security-rbac)role on the search service.

For SDK development, install the Azure Search client library:

- .NET:
[Azure.Search.Documents](https://www.nuget.org/packages/Azure.Search.Documents/) - Python:
[azure-search-documents](https://pypi.org/project/azure-search-documents/) - JavaScript:
[@azure/search-documents](https://www.npmjs.com/package/@azure/search-documents) - Java:
[azure-search-documents](https://central.sonatype.com/artifact/com.azure/azure-search-documents)

- .NET:

## Use the Azure portal

In the Azure portal, use an [import wizard](search-import-data-portal) to create and load indexes in a seamless workflow. If you want to load an existing index, choose an alternative approach.

Sign in to the

[Azure portal](https://portal.azure.com/)with your Azure account and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).On the

**Overview**page, select**Import data**or**Import data (new)**on the command bar to create and populate a search index.You can follow these links to review the workflow:

[Quickstart: Create an Azure AI Search index](search-get-started-portal)and[Quickstart: Integrated vectorization](search-get-started-portal-import-vectors).After the wizard is finished, use

[Search Explorer](search-explorer)to check for results.

Tip

The import wizards create and run indexers. If indexers are already defined, you can [reset and run an indexer](search-howto-run-reset-indexers) from the Azure portal, which is useful if you're adding fields incrementally. Reset forces the indexer to start over, picking up all fields from all source documents.

## Use the REST APIs

[Documents - Index](/en-us/rest/api/searchservice/documents) is the REST API for importing data into a search index.

The body of the request contains one or more documents to be indexed. Documents are uniquely identified through a case-sensitive key. Each document is associated with an action: "upload", "delete", "merge", or "mergeOrUpload". Upload requests must include the document data as a set of key/value pairs.

REST APIs are useful for initial proof-of-concept testing, where you can test indexing workflows without having to write much code. The `@search.action`

parameter determines whether documents are added in full, or partially in terms of new or replacement values for specific fields.

[ Quickstart: Full-text search using REST](search-get-started-text) explains the steps. The following example is a modified version of the example. The value is trimmed for brevity and the first HotelId value is altered to avoid overwriting an existing document.

Formulate a POST call specifying the index name, the "docs/index" endpoint, and a request body that includes the

`@search.action`

parameter.`POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/index?api-version=2025-09-01 Content-Type: application/json api-key: [admin key] { "value": [ { "@search.action": "upload", "HotelId": "1111", "HotelName": "Stay-Kay City Hotel", "Description": "The hotel is ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Time's Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities.", "Category": "Boutique", "Tags": [ "pool", "air conditioning", "concierge" ] }, { "@search.action": "mergeOrUpload", "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "This is description is replacing the original one for this hotel. New and changed values overwrite the previous ones. In a comma-delimited list like Tags, be sure to provide the full list because there is no merging of values within the field itself.", "Category": "Boutique", "Tags": [ "pool", "free wifi", "concierge", "my first new tag", "my second new tag" ] } ] }`

Set the

`@search.action`

parameter to`upload`

to create or overwrite a document. Set it to`merge`

or`uploadOrMerge`

if you're targeting updates to specific fields within the document. The previous example shows both actions.Action Effect upload Similar to an "upsert" where the document is inserted if it's new, and updated or replaced if it exists. If the document is missing values that the index requires, the document field's value is set to null. merge Updates a document that already exists, and fails a document that can't be found. Merge replaces existing values. For this reason, be sure to check for collection fields that contain multiple values, such as fields of type `Collection(Edm.String)`

. For example, if a`tags`

field starts with a value of`["budget"]`

and you execute a merge with`["economy", "pool"]`

, the final value of the`tags`

field is`["economy", "pool"]`

. It isn't`["budget", "economy", "pool"]`

.mergeOrUpload Behaves like merge if the document exists, and upload if the document is new. This is the most common action for incremental updates. delete Delete removes the specified document from the index. Any field you specify in a delete operation, other than the key field, is ignored. If you want to remove an individual field from a document, use merge instead and set the field explicitly to null. For more information, see [Delete documents in a search index](search-how-to-delete-documents).There are no ordering guarantees for which action in the request body is executed first. It's not recommended to have multiple "merge" actions associated with the same document in a single request body. If there are multiple "merge" actions required for the same document, perform the merging client-side before updating the document in the search index.

In primitive collections, if the document contains a Tags field of type

`Collection(Edm.String)`

with a value of ["budget"], and you execute a merge with a value of ["economy", "pool"] for Tag, the final value of the Tags field will be ["economy", "pool"]. It isn't ["budget", "economy", "pool"].In complex collections, if the document contains a complex collection field named Rooms with a value of [{ "Type": "Budget Room", "BaseRate": 75.0 }], and you execute a merge with a value of [{ "Type": "Standard Room" }, { "Type": "Budget Room", "BaseRate": 60.5 }], the final value of the Rooms field will be [{ "Type": "Standard Room" }, { "Type": "Budget Room", "BaseRate": 60.5 }]. It won't be either of the following:

[{ "Type": "Budget Room", "BaseRate": 75.0 }, { "Type": "Standard Room" }, { "Type": "Budget Room", "BaseRate": 60.5 }] (append elements)

[{ "Type": "Standard Room", "BaseRate": 75.0 }, { "Type": "Budget Room", "BaseRate": 60.5 }] (merge elements in order, then append any extras)


Note

When you upload DateTimeOffset values with time zone information to your index, Azure AI Search normalizes these values to UTC. For example, 2025-01-13T14:03:00-08:00 will be stored as 2025-01-13T22:03:00Z. If you need to store time zone information, add an extra column to your index.

Send the request.

The following table explains the various per-document

[status codes](/en-us/rest/api/searchservice/http-status-codes)that can be returned in the response. Some status codes indicate problems with the request itself, while others indicate temporary error conditions. The latter you should retry after a delay.Status code Meaning Retryable Notes 200 Document was successfully modified or deleted. n/a Delete operations are [idempotent](https://en.wikipedia.org/wiki/Idempotence). That is, even if a document key doesn't exist in the index, attempting a delete operation with that key results in a 200 status code.201 Document was successfully created. n/a 400 There was an error in the document that prevented it from being indexed. No The error message in the response indicates what is wrong with the document. 404 The document couldn't be merged because the given key doesn't exist in the index. No This error doesn't occur for uploads since they create new documents, and it doesn't occur for deletes because they're [idempotent](https://en.wikipedia.org/wiki/Idempotence).409 A version conflict was detected when attempting to index a document. Yes This can happen when you're trying to index the same document more than once concurrently. 422 The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'. Yes 429 Indicates that you have exceeded your quota on the number of documents per index. No You must either create a new index or upgrade for higher capacity limits. 503 Your search service is temporarily unavailable, possibly due to heavy load. Yes Your code should wait before retrying in this case or you risk prolonging the service unavailability. Note

If your client code frequently encounters a 207 response, one possible reason is that the system is under load. You can confirm this by checking the

`statusCode`

property for 503. If this is the case, we recommend throttling indexing requests. Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.[Look up the documents](/en-us/rest/api/searchservice/documents/get)you just added as a validation step:`GET https://[service name].search.windows.net/indexes/hotel-sample-index/docs/1111?api-version=2025-09-01`


**Reference:** [Documents - Index](/en-us/rest/api/searchservice/documents), [Documents - Get](/en-us/rest/api/searchservice/documents/get)

A successful index request returns HTTP 200 (OK) for a batch where all documents succeeded, or HTTP 207 (Multi-Status) if some documents failed. The response body contains status for each document:

```
{
"value": [
{ "key": "1111", "status": true, "statusCode": 201 },
{ "key": "2", "status": true, "statusCode": 200 }
]
}
```


When the document key or ID is new, **null** becomes the value for any field that's unspecified in the document. For actions on an existing document, updated values replace the previous values. Any fields that weren't specified in a "merge" or "mergeUpload" are left intact in the search index.

## Use the Azure SDKs

Programmability is provided in the following Azure SDKs.

The Azure SDK for Python provides the following APIs for simple and bulk document uploads into an index:

**Reference:** [SearchClient](/en-us/python/api/azure-search-documents/azure.search.documents.searchclient), [IndexDocumentsBatch](/en-us/python/api/azure-search-documents/azure.search.documents.indexdocumentsbatch)

Code samples include:

Be sure to check the

[azure-search-vector-samples](https://github.com/Azure/azure-search-vector-samples)repo for code examples showing how to index vector fields.

## Verify your data load

After loading documents, verify the data is indexed correctly.

- In the Azure portal, open the search service
**Overview**page. - Select
**Search explorer**from the command bar. - Select your index from the dropdown.
- Select
**Search**to run an empty query that returns all documents. - Verify the document count and spot-check field values.

## How data import works

A search service accepts JSON documents that conform to the index schema. A search service can import and index plain text content and vector content in JSON documents.

Plain text content is retrieved from fields in the external data source, from metadata properties, or from enriched content that's generated by a

[skillset](cognitive-search-working-with-skillsets). Skills can extract or infer textual descriptions from images and unstructured content.Vector content is retrieved from a data source that provides it, or it's created by a skillset that implements

[integrated vectorization](vector-search-integrated-vectorization)in an Azure AI Search indexer workload.

You can prepare these documents yourself, but if content resides in a [supported data source](search-indexer-overview#supported-data-sources), running an [indexer](search-indexer-overview) or using an Import wizard can automate document retrieval, JSON serialization, and indexing.

Once data is indexed, the physical data structures of the index are locked in. For guidance on what can and can't be changed, see [Update and rebuild an index](search-howto-reindex).

Indexing isn't a background process. A search service balances indexing and query workloads, but if [query latency is too high](search-performance-analysis#impact-of-indexing-on-queries), you can either [add capacity](search-capacity-planning#add-or-remove-partitions-and-replicas) or identify periods of low query activity for loading an index.

For more information, see [Data import strategies](search-what-is-data-import).

## Troubleshoot common errors

| Error | Cause | Solution |
|---|---|---|
| HTTP 400 Bad Request | Document contains invalid data or missing required fields | Check the error message for the specific field. Ensure all required fields are present and data types match the index schema. |
| HTTP 404 Not Found (merge) | Attempting to merge a document that doesn't exist | Use `mergeOrUpload` instead of `merge` if the document might not exist. |
| HTTP 409 Conflict | Concurrent updates to the same document | Implement retry logic with exponential backoff. |
| HTTP 413 Payload Too Large | Batch size exceeds limits | Reduce the number of documents per batch. Maximum batch size is 1,000 documents or 16 MB. |
| HTTP 429 Too Many Requests | Quota exceeded | Check your service tier limits. Consider upgrading or creating a new index. |
| HTTP 503 Service Unavailable | Service is under heavy load | Implement retry logic with exponential backoff. Reduce indexing request frequency. |
