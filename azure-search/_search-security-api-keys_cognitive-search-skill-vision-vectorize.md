---
merged_at: 2026-01-25T02:11:58.420343
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-security-api-keys.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-security-api-keys -->

# Connect to Azure AI Search using keys

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search supports both identity-based and key-based authentication (default) for connections to your search service.

A request made to a search service endpoint is accepted if both the request and the API key are valid and if the search service is configured to allow API keys on a request.

Important

When you create a search service, key-based authentication is the default, but it's not the most secure option. We recommend that you replace it with [role-based access](search-security-enable-roles).

## Prerequisites

You must be an Owner, Contributor, or [Search Service Contributor](/en-us/azure/role-based-access-control/built-in-roles#search-service-contributor) to view or manage keys.

## Enabled by default

In the Azure portal, authentication is specified on the **Settings** > **Keys** page. Options set to either **API keys** (default) or **Both** allow API keys on a request.


## Types of keys

An API key is a unique string composed of 52 randomly generated numbers and letters. Visually, there's no distinction between an admin key or query key. If you lose track of what type of key is specified in your application, you can [check the key values in the Azure portal](#find-existing-keys).

There are two kinds of keys used for authenticating a request:

| Type | Permission level | How it's created | Maximum |
|---|---|---|---|
| Admin | Full access (read-write) for all data plane (content) operations | Two admin keys, primary and secondary, are generated when the service is created and can be individually regenerated on demand. Having two allows you to roll over one key while using the second key for continued access to the service. |
2 |
| Query | Read-only access, scoped to the documents collection of a search index | One query key is generated with the service. More can be created on demand by a search service administrator. | 50 |

## Find existing keys

You can view and manage API keys using the [Azure portal](https://portal.azure.com), [PowerShell](/en-us/powershell/module/az.search), [Azure CLI](/en-us/cli/azure/search), or [REST API](/en-us/rest/api/searchmanagement/).

Sign in to the

[Azure portal](https://portal.azure.com)and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).From the left pane, select

**Settings**>**Keys**to view admin and query keys.

## Use keys on connections

Key-based authentication is used only for data plane (content) requests, such as creating or querying index and any other action that's performed using the [Search Service REST API](/en-us/rest/api/searchservice/operation-groups).

In your source code, you can directly specify the API key in a request header. Alternatively, you can store it as an [environment variable](/en-us/azure/ai-services/cognitive-services-environment-variables) or app setting in your project and then reference the variable in the request.

- Admin keys are used for creating, modifying, or deleting objects.
- Admin keys are also used to GET object definitions and system information, such as
[LIST Indexes](/en-us/rest/api/searchservice/indexes/list)or[GET Service Statistics](/en-us/rest/api/searchservice/get-service-statistics/get-service-statistics). - Query keys are typically distributed to client applications that issue queries.

Recall that key authentication is enabled by default and supports data plane operations such as indexing and queries.

However, if you [disable API keys](search-security-enable-roles#disable-api-key-authentication) and set up role assignments, the Azure portal uses role assignments instead.

## Create query keys

Query keys are used for read-only access to documents within an index for operations targeting a documents collection. Search, filter, and suggestion queries are all operations that take a query key. Any read-only operation that returns system data or object definitions, such as an index definition or indexer status, requires an admin key.

Restricting access and operations in client apps is essential to safeguarding the search assets on your service. Always use a query key rather than an admin key for any query originating from a client app.

Sign in to the

[Azure portal](https://portal.azure.com)and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).From the left pane, select

**Settings**>**Keys**to view API keys.Under

**Manage query keys**, use the query key already generated for your service, or create new query keys. The default query key isn't named, but other generated query keys can be named for manageability.

## Regenerate admin keys

Two admin keys are created for each service so that you can rotate a primary key while using the secondary key for business continuity.

Sign in to the

[Azure portal](https://portal.azure.com)and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).From the left pane, select

**Settings**>**Keys**.Copy the secondary key.

For all applications, update the API key settings to use the secondary key.

Regenerate the primary key.

Update all applications to use the new primary key.


If you inadvertently regenerate both keys at the same time, all client requests using those keys will fail with HTTP 403 Forbidden. However, content isn't deleted and you aren't locked out permanently.

You can still access the service through the Azure portal or programmatically. Management functions are operative through a subscription ID not a service API key, and are thus still available even if your API keys aren't.

After you create new keys via portal or management layer, access is restored to your content (indexes, indexers, data sources, synonym maps) once you provide those keys on requests.

## Migrate from keys to roles

If you want to transition to role-based access, it's helpful to understand how keys map to [built-in roles in Azure AI Search](search-security-rbac#built-in-roles-used-in-search):

- An admin key corresponds to the
**Search Service Contributor**and**Search Index Data Contributor**roles. - A query key corresponds to the
**Search Index Data Reader**role.

## Secure keys

Use role assignments to restrict access to API keys.

It's not possible to use [customer-managed key encryption](search-security-manage-encryption-keys) to encrypt API keys. Only sensitive data within the search service itself (for example, index content or connection strings in data source object definitions) can be CMK-encrypted.

Sign in to the

[Azure portal](https://portal.azure.com)and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).From the left pane, select

**Access control (IAM)**, and then select the**Role assignments**tab.In the

**Role**filter, select the roles that have permission to view or manage keys (Owner, Contributor, Search Service Contributor). The resulting security principals assigned to those roles have key permissions on your search service.As a precaution, also check the

**Classic administrators**tab to determine whether administrators and co-administrators have access.

## Best practices

For production workloads, switch to

[Microsoft Entra ID and role-based access](search-security-rbac-client-code). Alternatively, if you want to continue using API keys, be sure to always monitor[who has access to your API keys](#secure-keys)and[regenerate API keys](#regenerate-admin-keys)on a regular cadence.Only use API keys if data disclosure isn't a risk (for example, when using sample data) and if you're operating behind a firewall. Exposing API keys puts both your data and your search service at risk of unauthorized use.

If you use an API key, store it securely somewhere else, such as in

[Azure Key Vault](/en-us/azure/key-vault/general/overview). Don't include the API key directly in your code, and never post it publicly.Always check code, samples, and training material before publishing to make sure you don't inadvertently expose an API key.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-vision-vectorize.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-vision-vectorize -->

# Azure Vision multimodal embeddings skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This skill is in public preview under [Supplemental Terms of Use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). The [2024-05-01-Preview REST API](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2024-05-01-Preview&preserve-view=true) and newer preview APIs support this feature.

The **Azure Vision multimodal embeddings** skill uses the [multimodal embeddings API](/en-us/azure/ai-services/computer-vision/concept-image-retrieval) from Azure Vision in Foundry Tools to generate embeddings for text or image input.

For transactions that exceed 20 documents per indexer per day, this skill requires you to [attach a billable Microsoft Foundry resource](cognitive-search-attach-cognitive-services) to your skillset. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/). Image extraction is also [billable by Azure AI Search](https://azure.microsoft.com/pricing/details/search/).

The Microsoft Foundry resource is used for billing purposes only. Content processing occurs on separate resources managed and maintained by Azure AI Search. Your data is processed in the [Geo](https://azure.microsoft.com/explore/global-infrastructure/data-residency/) where your resource is deployed.

## Supported regions

Supported regions vary by modality and how the skill connects to the Azure Vision multimodal embeddings API.

| Approach | Requirement |
|---|---|
Import data (new) wizard |

- Find a
[region that supports multimodal embeddings](/en-us/azure/ai-services/computer-vision/overview-image-analysis?tabs=4-0#region-availability)in Azure Vision. - Verify the
[region supports AI enrichment](search-region-support)in Azure AI Search. - Create an Azure AI Search service and
[Azure AI multi-service account](https://portal.azure.com/#create/Microsoft.CognitiveServicesAllInOne)in the same region.

[key-based connection](cognitive-search-attach-cognitive-services#bill-through-a-keyless-connection)for billing- Find a
[region that supports multimodal embeddings](/en-us/azure/ai-services/computer-vision/overview-image-analysis?tabs=4-0#region-availability)in Azure Vision. - Verify the
[region supports AI enrichment](search-region-support)in Azure AI Search. - Create an Azure AI Search service and Microsoft Foundry resource in the same region.

[keyless connection](cognitive-search-attach-cognitive-services#bill-through-a-keyless-connection)for billing[each service is available](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/table).## @odata.type

Microsoft.Skills.Vision.VectorizeSkill

## Data limits

The input limits for the skill can be found in the [Azure Vision documentation](/en-us/azure/ai-services/computer-vision/concept-image-retrieval#input-requirements) for images and text. Consider using the [Text Split skill](cognitive-search-skill-textsplit) if you need data chunking for text inputs.

Applicable inputs include:

- Image input file size must be less than 20 megabytes (MB). Image size must be greater than 10 x 10 pixels and less than 16,000 x 16,000 pixels.
- Text input string must be between (inclusive) one word and 70 words.

## Skill parameters

Parameters are case sensitive.

| Inputs | Description |
|---|---|
`modelVersion` |
(Required) The model version (`2023-04-15` ) to be passed to the Azure Vision multimodal embeddings API for generating embeddings. Vector embeddings can only be compared and matched if they're from the same model type. Images vectorized by one model won't be searchable through a different model. The latest Image Analysis API offers two models:
|

## Skill inputs

Skill definition inputs include name, source, and inputs. The following table provides valid values for name of the input. You can also specify recursive inputs. For more information, see the [REST API reference](/en-us/rest/api/searchservice/skillsets/create?view=rest-searchservice-2025-03-01-preview#inputfieldmappingentry&preserve-view=true) and [Create a skillset](cognitive-search-defining-skillset).

| Input | Description |
|---|---|
`text` |
The input text to be vectorized. If you're using data chunking, the source might be `/document/pages/*` . |
`image` |
Complex Type. Currently only works with "/document/normalized_images" field, produced by the Azure blob indexer when `imageAction` is set to a value other than `none` . |
`url` |
The URL to download the image to be vectorized. |
`queryString` |
The query string of the URL to download the image to be vectorized. Useful if you store the URL and SAS token in separate paths. |

Only one of `text`

, `image`

or `url`

/`queryString`

can be configured for a single instance of the skill. If you want to vectorize both images and text within the same skillset, include two instances of this skill in the skillset definition, one for each input type you would like to use.

## Skill outputs

| Output | Description |
|---|---|
`vector` |
Output embedding array of floats for the input text or image. |

## Sample definition

For text input, consider a blob that has the following content:

```
{
"content": "Forests, grasslands, deserts, and mountains are all part of the Patagonian landscape that spans more than a million square kilometers of South America."
}
```


For text inputs, your skill definition might look like this:

```
{
"@odata.type": "#Microsoft.Skills.Vision.VectorizeSkill",
"context": "/document",
"modelVersion": "2023-04-15",
"inputs": [
{
"name": "text",
"source": "/document/content"
}
],
"outputs": [
{
"name": "vector",
"targetName": "text_vector"
}
]
}
```


For image input, a second skill definition in the same skillset might look like this:

```
{
"@odata.type": "#Microsoft.Skills.Vision.VectorizeSkill",
"context": "/document/normalized_images/*",
"modelVersion": "2023-04-15",
"inputs": [
{
"name": "image",
"source": "/document/normalized_images/*"
}
],
"outputs": [
{
"name": "vector",
"targetName": "image_vector"
}
]
}
```


If you want to vectorize images directly from your blob storage data source rather than extract images during indexing, your skill definition should specify a URL, and perhaps a SAS token depending on storage security. For this scenario, your skill definition might look like this:

```
{
"@odata.type": "#Microsoft.Skills.Vision.VectorizeSkill",
"context": "/document",
"modelVersion": "2023-04-15",
"inputs": [
{
"name": "url",
"source": "/document/metadata_storage_path"
},
{
"name": "queryString",
"source": "/document/metadata_storage_sas_token"
}
],
"outputs": [
{
"name": "vector",
"targetName": "image_vector"
}
]
}
```


## Sample output

For the given input, a vectorized embedding output is produced. Output is 1,024 dimensions, which is the number of dimensions supported by the Azure Vision multimodal API.

```
{
"text_vector": [
0.018990106880664825,
-0.0073809814639389515,
....
0.021276434883475304,
]
}
```


The output resides in memory. To send this output to a field in the search index, you must define an [outputFieldMapping](cognitive-search-output-field-mapping) that maps the vectorized embedding output (which is an array) to a [vector field](vector-search-how-to-create-index). Assuming the skill output resides in the document's **vector** node, and **content_vector** is the field in the search index, the outputFieldMapping in the indexer should look like:

```
"outputFieldMappings": [
{
"sourceFieldName": "/document/vector/*",
"targetFieldName": "content_vector"
}
]
```


For mapping image embeddings to the index, you use [index projections](index-projections-concept-intro). The payload for `indexProjections`

might look something like the following example. image_content_vector is a field in the index, and it's populated with the content found in the **vector** of the **normalized_images** array.

```
"indexProjections": {
"selectors": [
{
"targetIndexName": "myTargetIndex",
"parentKeyFieldName": "ParentKey",
"sourceContext": "/document/normalized_images/*",
"mappings": [
{
"name": "image_content_vector",
"source": "/document/normalized_images/*/vector"
}
]
}
]
}
```
