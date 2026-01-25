---
merged_at: 2026-01-25T02:11:58.378665
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: samples-javascript.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/samples-javascript -->

# JavaScript samples for Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn about JavaScript code samples that demonstrate the functionality and workflow of an Azure AI Search solution. These samples use the [Azure AI Search client library](/en-us/javascript/api/overview/azure/search-documents-readme) for the [Azure SDK for JavaScript](/en-us/azure/developer/javascript/), which you can explore through the following links.

| Target | Link |
|---|---|
| Package download |
|

[@azure/search-documents](/en-us/javascript/api/@azure/search-documents/)[github.com/Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents/test](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents/test)[github.com/Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents)[github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/CHANGELOG.md](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/CHANGELOG.md)## SDK samples

Code samples from the Azure SDK development team demonstrate API usage. You can find these samples in [Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents/samples](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents/samples) on GitHub.

### JavaScript samples

| Sample | Description |
|---|---|
|

[indexes](search-what-is-an-index). This sample category also includes a service statistic sample.[indexers](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents/samples/v11/javascript)[indexers](search-indexer-overview).[dataSourceConnections (for indexers)](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/samples/v11/javascript/dataSourceConnectionOperations.js)[supported data sources](search-indexer-overview#supported-data-sources).[skillsets](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents/samples/v11/javascript)[skillsets](cognitive-search-working-with-skillsets)that are attached to indexers and perform AI-based enrichment during indexing.[synonymMaps](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents/samples/v11/javascript)[synonym maps](search-synonyms).[vectorSearch](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/samples/v12-beta/javascript/vectorSearch.js)[vector query](vector-search-how-to-query).### TypeScript samples

| Sample | Description |
|---|---|
|

[indexes](search-what-is-an-index). This sample category also includes a service statistic sample.[indexers](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/search/search-documents/samples/v11/typescript/src)[indexers](search-indexer-overview).[dataSourceConnections (for indexers)](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/samples/v11/typescript/src/dataSourceConnectionOperations.ts)[supported data sources](search-indexer-overview#supported-data-sources).[skillsets](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/samples/v11/typescript/src/skillSetOperations.ts)[skillsets](cognitive-search-working-with-skillsets)that are attached to indexers and perform AI-based enrichment during indexing.[synonymMaps](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/samples/v11/typescript/src/synonymMapOperations.ts)[synonym maps](search-synonyms).[vectorSearch](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/samples/v12/typescript/src/vectorSearch.ts)[vector search](vector-search-how-to-query).## Doc samples

Code samples from the Azure AI Search team demonstrate features and workflows. The following samples are referenced in tutorials, quickstarts, and how-to articles. You can find these samples in [Azure-Samples/azure-search-javascript-samples](https://github.com/Azure-Samples/azure-search-javascript-samples) on GitHub.

### JavaScript samples

| Sample | Article | Description |
|---|---|---|
|

[Quickstart: Full-text search](search-get-started-text)[quickstart-semantic-ranking-js](https://github.com/Azure-Samples/azure-search-javascript-samples/tree/main/quickstart-semantic-ranking-js)[Quickstart: Semantic ranking](search-get-started-semantic)[quickstart-vector-js](https://github.com/Azure-Samples/azure-search-javascript-samples/tree/main/quickstart-vector-js)[Quickstart: Vector search](search-get-started-vector)### TypeScript samples

| Sample | Article | Description |
|---|---|---|
|

[Quickstart: Semantic ranking](search-get-started-semantic)[quickstart-vector-ts](https://github.com/Azure-Samples/azure-search-javascript-samples/tree/main/quickstart-vector-ts)[Quickstart: Vector search](search-get-started-vector)## Other samples

The following samples are also published by the Azure AI Search team but aren't referenced in documentation. Associated README files provide usage instructions.

| Sample | Description |
|---|---|
|

[azure-search-vector-sample.js](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-javascript/readme.md)[azure-function-search](https://github.com/Azure-Samples/azure-search-javascript-samples/tree/main/azure-function-search)`api`

code used in [Add search to web sites with .NET](tutorial-csharp-overview).[bulk-insert](https://github.com/Azure-Samples/azure-search-javascript-samples/tree/main/bulk-insert)[use the push APIs](search-how-to-load-search-index)to upload and index documents.Tip

Use the [samples browser](/en-us/samples/browse/?languages=javascript&products=azure-cognitive-search) to search for Microsoft code samples on GitHub. You can filter your search by product, service, and language.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-entity-recognition-v3.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-entity-recognition-v3 -->

# Entity Recognition cognitive skill (v3)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Entity Recognition** skill (v3) extracts entities of different types from text. These entities fall under 14 distinct categories, ranging from people and organizations to URLs and phone numbers. This skill uses the [Named Entity Recognition](/en-us/azure/ai-services/language-service/named-entity-recognition/overview) machine learning models provided by [Azure Language in Foundry Tools](/en-us/azure/ai-services/language-service/overview).

Note

This skill is bound to Foundry Tools and requires [a billable resource](cognitive-search-attach-cognitive-services) for transactions that exceed 20 documents per indexer per day. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

## @odata.type

Microsoft.Skills.Text.V3.EntityRecognitionSkill

## Data limits

The maximum size of a record should be 50,000 characters as measured by [ String.Length](/en-us/dotnet/api/system.string.length). If you need to break up your data before sending it to the EntityRecognition skill, consider using the

[Text Split skill](cognitive-search-skill-textsplit). When using a split skill, set the page length to 5000 for the best performance.

## Skill parameters

Parameters are case sensitive and are all optional.

| Parameter name | Description |
|---|---|
`categories` |
Array of categories that should be extracted. Possible category types: `"Person"` , `"Location"` , `"Organization"` , `"Quantity"` , `"DateTime"` , `"URL"` , `"Email"` , `"personType"` , `"Event"` , `"Product"` , `"Skill"` , `"Address"` , `"phoneNumber"` , `"ipAddress"` . If no category is provided, all types are returned. |
`defaultLanguageCode` |
Language code of the input text. If the default language code is not specified, English (en) will be used as the default language code. See the
|
`minimumPrecision` |
A value between 0 and 1. If the confidence score (in the `namedEntities` output) is lower than this value, the entity is not returned. The default is 0. |
`modelVersion` |
(Optional) Specifies the
|

## Skill inputs

| Input name | Description |
|---|---|
`languageCode` |
A string indicating the language of the records. If this parameter is not specified, the default language code will be used to analyze the records. See the
|
`text` |
The text to analyze. |

## Skill outputs

Note

Not all entity categories are supported for all languages. See [Supported Named Entity Recognition (NER) entity categories](/en-us/azure/ai-services/language-service/named-entity-recognition/concepts/named-entity-categories) to know which entity categories are supported for the language you will be using.

| Output name | Description |
|---|---|
`persons` |
An array of strings where each string represents the name of a person. |
`locations` |
An array of strings where each string represents a location. |
`organizations` |
An array of strings where each string represents an organization. |
`quantities` |
An array of strings where each string represents a quantity. |
`dateTimes` |
An array of strings where each string represents a DateTime (as it appears in the text) value. |
`urls` |
An array of strings where each string represents a URL |
`emails` |
An array of strings where each string represents an email |
`personTypes` |
An array of strings where each string represents a PersonType |
`events` |
An array of strings where each string represents an event |
`products` |
An array of strings where each string represents a product |
`skills` |
An array of strings where each string represents a skill |
`addresses` |
An array of strings where each string represents an address |
`phoneNumbers` |
An array of strings where each string represents a telephone number |
`ipAddresses` |
An array of strings where each string represents an IP Address |
`namedEntities` |
An array of complex types that contains the following fields:
|

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Text.V3.EntityRecognitionSkill",
"context": "/document",
"categories": [ "Person", "Email"],
"defaultLanguageCode": "en",
"minimumPrecision": 0.5,
"inputs": [
{
"name": "text",
"source": "/document/content"
},
{
"name": "languageCode",
"source": "/document/language"
}
],
"outputs": [
{
"name": "persons",
"targetName": "people"
},
{
"name": "emails",
"targetName": "emails"
},
{
"name": "namedEntities",
"targetName": "namedEntities"
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
"text": "Contoso Corporation was founded by Jean Martin. They can be reached at contact@contoso.com",
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
"people": [ "Jean Martin"],
"emails":["contact@contoso.com"],
"namedEntities":
[
{
"category": "Person",
"subcategory": null,
"length": 11,
"offset": 35,
"confidenceScore": 0.98,
"text": "Jean Martin"
},
{
"category": "Email",
"subcategory": null,
"length": 19,
"offset": 71,
"confidenceScore": 0.8,
"text": "contact@contoso.com"
}
],
}
}
]
}
```


The offsets returned for entities in the output of this skill are directly returned from the [Language Service APIs](/en-us/azure/ai-services/language-service/overview), which means if you are using them to index into the original string, you should use the [StringInfo](/en-us/dotnet/api/system.globalization.stringinfo) class in .NET in order to extract the correct content. For more information, see [Multilingual and emoji support in Language service features](/en-us/azure/ai-services/language-service/concepts/multilingual-emoji-support).

## Warning cases

If the language code for the document is unsupported, a warning is returned and no entities are extracted.
