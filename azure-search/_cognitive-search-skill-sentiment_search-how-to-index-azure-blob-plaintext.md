---
merged_at: 2026-01-25T03:18:13.738086
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-sentiment.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-sentiment -->

# Sentiment cognitive skill (v2)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Sentiment** skill (v2) evaluates unstructured text along a positive-negative continuum, and for each record, returns a numeric score between 0 and 1. Scores close to 1 indicate positive sentiment, and scores close to 0 indicate negative sentiment. This skill uses the machine learning models provided by [Text Analytics](/en-us/azure/ai-services/language-service/overview) in Foundry Tools.

Important

The Sentiment skill (v2) (**Microsoft.Skills.Text.SentimentSkill**) is now discontinued, replaced by [Microsoft.Skills.Text.V3.SentimentSkill](cognitive-search-skill-sentiment-v3). Follow the recommendations in [Deprecated Azure AI Search skills](cognitive-search-skill-deprecated) to migrate to a supported skill.

Note

As you expand scope by increasing the frequency of processing, adding more documents, or adding more AI algorithms, you will need to [attach a billable Microsoft Foundry resource](cognitive-search-attach-cognitive-services). Charges accrue when calling APIs in Foundry Tools, and for image extraction as part of the document-cracking stage in Azure AI Search. There are no charges for text extraction from documents.

Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/). Image extraction pricing is described on the [Azure AI Search pricing page](https://azure.microsoft.com/pricing/details/search/).

## @odata.type

Microsoft.Skills.Text.SentimentSkill

## Data limits

The maximum size of a record should be 5000 characters as measured by [ String.Length](/en-us/dotnet/api/system.string.length). If you need to break up your data before sending it to the sentiment analyzer, use the

[Text Split skill](cognitive-search-skill-textsplit).

## Skill parameters

Parameters are case sensitive.

| Parameter Name | Description |
|---|---|
`defaultLanguageCode` |
(optional) The language code to apply to documents that don't specify language explicitly. See the
|

## Skill inputs

| Input Name | Description |
|---|---|
`text` |
The text to be analyzed. |
`languageCode` |
(Optional) A string indicating the language of the records. If this parameter is not specified, the default value is "en". See the
|

## Skill outputs

| Output Name | Description |
|---|---|
`score` |
A value between 0 and 1 that represents the sentiment of the analyzed text. Values close to 0 have negative sentiment, close to 0.5 have neutral sentiment, and values close to 1 have positive sentiment. |

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Text.SentimentSkill",
"inputs": [
{
"name": "text",
"source": "/document/content"
},
{
"name": "languageCode",
"source": "/document/languagecode"
}
],
"outputs": [
{
"name": "score",
"targetName": "mySentiment"
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
"data": {
"text": "I had a terrible time at the hotel. The staff was rude and the food was awful.",
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
"data": {
"score": 0.01
}
}
]
}
```


## Warning cases

If your text is empty, a warning is generated and no sentiment score is returned. If a language is not supported, a warning is generated and no sentiment score is returned.


---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-azure-blob-plaintext.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-azure-blob-plaintext -->

# Index plain text blobs and files in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to**: [Blob indexers](search-how-to-index-azure-blob-storage), [File indexers](search-file-storage-integration)

When using an indexer to extract searchable blob text or file content for full text search, you can assign a parsing mode to get better indexing outcomes. By default, the indexer parses a blob's `content`

property as a single chunk of text. However, if all blobs and files contain plain text in the same encoding, you can significantly improve indexing performance by using the `text`

parsing mode.

Recommendations for `text`

parsing include either of the following characteristics:

- File type is
`.txt`

- Files are of any type, but the content itself is text (for example, program source code, HTML, XML, and so forth). For files in a markup language, the syntax characters come through as static text.

Recall that all indexers serialize to JSON. By default, the content of the entire text file is indexed within one large field as `"content": "<file-contents>"`

. New line and return instructions are embedded in the content field and expressed as `\r\n\`

.

If you want a more refined or granular outcome, and if the file type is compatible, consider the following solutions:

parsing mode, if the source is CSV`delimitedText`

, if the source is JSON`jsonArray`

or`jsonLines`


An alternative third option for breaking content into multiple parts requires advanced features in the form of [AI enrichment](cognitive-search-concept-intro). It adds analysis that identifies and assigns chunks of the file to different search fields. You might find a full or partial solution through [built-in skills](cognitive-search-predefined-skills) such as entity recognition or keyword extraction, but a more likely solution might be a custom learning model that understands your content, wrapped in a [custom skill](cognitive-search-custom-skill-interface).

## Set up plain text indexing

To index plain text blobs, create or update an indexer definition with the `parsingMode`

configuration property set to `text`

on a [Create Indexer](/en-us/rest/api/searchservice/indexers/create) request:

```
PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
... other parts of indexer definition
"parameters" : { "configuration" : { "parsingMode" : "text" } }
}
```


By default, the `UTF-8`

encoding is assumed. To specify a different encoding, use the `encoding`

configuration property. The supported [list of encodings](/en-us/dotnet/fundamentals/runtime-libraries/system-text-encoding#list-of-encodings) is under **.NET 5 and later support** column.

```
{
... other parts of indexer definition
"parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "iso-8859-1" } }
}
```


## Request example

Parsing modes are specified in the indexer definition.

```
POST https://[service name].search.windows.net/indexers?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
"name" : "my-plaintext-indexer",
"dataSourceName" : "my-blob-datasource",
"targetIndexName" : "my-target-index",
"parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
}
```
