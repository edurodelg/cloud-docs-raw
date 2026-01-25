---
merged_at: 2026-01-25T02:11:58.357916
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-named-entity-recognition.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-named-entity-recognition -->

# Named Entity Recognition cognitive skill (v2)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Named Entity Recognition** skill (v2) extracts named entities from text. Available entities include the types `person`

, `location`

and `organization`

.

Important

Named entity recognition skill (v2) (**Microsoft.Skills.Text.NamedEntityRecognitionSkill**) is now discontinued replaced by [Microsoft.Skills.Text.V3.EntityRecognitionSkill](cognitive-search-skill-entity-recognition-v3). Follow the recommendations in [Deprecated Azure AI Search skills](cognitive-search-skill-deprecated) to migrate to a supported skill.

Note

As you expand scope by increasing the frequency of processing, adding more documents, or adding more AI algorithms, you will need to [attach a billable Microsoft Foundry resource](cognitive-search-attach-cognitive-services). Charges accrue when calling APIs in Foundry Tools, and for image extraction as part of the document-cracking stage in Azure AI Search. There are no charges for text extraction from documents. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

Image extraction is an extra charge metered by Azure AI Search, as described on the [pricing page](https://azure.microsoft.com/pricing/details/search/). Text extraction is free.

## @odata.type

Microsoft.Skills.Text.NamedEntityRecognitionSkill

## Data limits

The maximum size of a record should be 50,000 characters as measured by [ String.Length](/en-us/dotnet/api/system.string.length). If you need to break up your data before sending it to the key phrase extractor, consider using the

[Text Split skill](cognitive-search-skill-textsplit). If you do use a text split skill, set the page length to 5000 for the best performance.

## Skill parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
| categories | Array of categories that should be extracted. Possible category types: `"Person"` , `"Location"` , `"Organization"` . If no category is provided, all types are returned. |
| defaultLanguageCode | Language code of the input text. The following languages are supported: `de, en, es, fr, it` |
| minimumPrecision | A number between 0 and 1. If the precision is lower than this value, the entity is not returned. The default is 0. |

## Skill inputs

| Input name | Description |
|---|---|
| languageCode | Optional. Default is `"en"` . |
| text | The text to analyze. |

## Skill outputs

| Output name | Description |
|---|---|
| persons | An array of strings where each string represents the name of a person. |
| locations | An array of strings where each string represents a location. |
| organizations | An array of strings where each string represents an organization. |
| entities | An array of complex types. Each complex type includes the following fields:
|

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Text.NamedEntityRecognitionSkill",
"categories": [ "Person", "Location", "Organization"],
"defaultLanguageCode": "en",
"inputs": [
{
"name": "text",
"source": "/document/content"
}
],
"outputs": [
{
"name": "persons",
"targetName": "people"
}
]
}
```


## Sample input

```
{
"values": [
{
"recordId": "1",
"data":
{
"text": "This is the loan application for Joe Romero, a Microsoft employee who was born in Chile and who then moved to Australia… Ana Smith is provided as a reference.",
"languageCode": "en"
}
}
]
}
```


## Sample output

```
{
"values": [
{
"recordId": "1",
"data" :
{
"persons": [ "Joe Romero", "Ana Smith"],
"locations": ["Chile", "Australia"],
"organizations":["Microsoft"],
"entities":
[
{
"category":"person",
"value": "Joe Romero",
"offset": 33,
"confidence": 0.87
},
{
"category":"person",
"value": "Ana Smith",
"offset": 124,
"confidence": 0.87
},
{
"category":"location",
"value": "Chile",
"offset": 88,
"confidence": 0.99
},
{
"category":"location",
"value": "Australia",
"offset": 112,
"confidence": 0.99
},
{
"category":"organization",
"value": "Microsoft",
"offset": 54,
"confidence": 0.99
}
]
}
}
]
}
```


## Warning cases

If the language code for the document is unsupported, a warning is returned and no entities are extracted.


---

<!-- DOCUMENTO FUSIONADO: search-security-get-encryption-keys.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-security-get-encryption-keys -->

# Find encrypted objects and information

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, customer-managed encryption keys are created, stored, and managed in Azure Key Vault. If you need to determine whether an object is encrypted, or what key name or version is used in Azure Key Vault, use the REST API or an Azure SDK to retrieve the **encryptionKey** property from the object definition in your search service.

Objects that aren't encrypted with a customer-managed key have an empty **encryptionKey** property. Otherwise, you might see a definition similar to the following example.

```
"encryptionKey":{
"keyVaultUri":"https://demokeyvault.vault.azure.net",
"keyVaultKeyName":"myEncryptionKey",
"keyVaultKeyVersion":"eaab6a663d59439ebb95ce2fe7d5f660",
"accessCredentials":{
"applicationId":"00001111-aaaa-2222-bbbb-3333cccc4444",
"applicationSecret":"myApplicationSecret"
}
}
```


The **encryptionKey** construct is the same for all encrypted objects. It's a first-level property, on the same level as the object name and description.

## Permissions for retrieving object definitions

You must have [Search Service Contributor](search-security-rbac#built-in-roles-used-in-search) or equivalent permissions. To use [key-based authentication](search-security-api-keys) instead, provide an admin API key. Admin permissions are required on requests that return object definitions and metadata. The easiest way to get the admin API key is through the Azure portal.

Sign in to the

[Azure portal](https://portal.azure.com/)and open the search service overview page.On the left side, select

**Keys**and copy an admin API.

For the remaining steps, switch to PowerShell and the REST API. The Azure portal doesn't show encryption key information for any object.

## Retrieve object properties

Use PowerShell and REST to run the following commands to set up the variables and get object definitions.

Alternatively, you can also use the Azure SDK for [.NET](/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient.getindexes), [Python](/en-us/python/api/azure-search-documents/azure.search.documents.indexes.searchindexclient), [JavaScript](/en-us/javascript/api/@azure/search-documents/searchindexclient), and [Java](/en-us/java/api/com.azure.search.documents.indexes.searchindexclient.getindex).

First, connect to your Azure account.

```
Connect-AzAccount
```


If you have more than one active subscription in your tenant, specify the subscription containing your search service:

```
Set-AzContext -Subscription <your-subscription-ID>
```


Set up the headers used on each request in the current session. Provide the admin API key used for search service authentication.

```
$headers = @{
'api-key' = '<YOUR-ADMIN-API-KEY>'
'Content-Type' = 'application/json'
'Accept' = 'application/json' }
```


To return a list of all search indexes, set the endpoint to the indexes collection.

```
$uri= 'https://<YOUR-SEARCH-SERVICE>.search.windows.net/indexes?api-version=2025-09-01&$select=name'
Invoke-RestMethod -Uri $uri -Headers $headers | ConvertTo-Json
```


To return a specific index definition, provide its name in the path. The encryptionKey property is at the end.

```
$uri= 'https://<YOUR-SEARCH-SERVICE>.search.windows.net/indexes/<YOUR-INDEX-NAME>?api-version=2025-09-01'
Invoke-RestMethod -Uri $uri -Headers $headers | ConvertTo-Json
```


To return synonym maps, set the endpoint to the synonyms collection and then send the request.

```
$uri= 'https://<YOUR-SEARCH-SERVICE>.search.windows.net/synonyms?api-version=2025-09-01&$select=name'
Invoke-RestMethod -Uri $uri -Headers $headers | ConvertTo-Json
```


The following example returns a specific synonym map definition, including the encryptionKey property is towards the end of the definition.

```
$uri= 'https://<YOUR-SEARCH-SERVICE>.search.windows.net/synonyms/<YOUR-SYNONYM-MAP-NAME>?api-version=2025-09-01'
Invoke-RestMethod -Uri $uri -Headers $headers | ConvertTo-Json
```


Use the same pattern to return the encryptionKey property for other top-level objects such as indexers, skillsets, data sources, and index aliases.

## Next steps

We recommend that you [enable logging](/en-us/azure/key-vault/general/logging) on Azure Key Vault so that you can monitor key usage.

For more information about using Azure Key or configuring customer managed encryption:
