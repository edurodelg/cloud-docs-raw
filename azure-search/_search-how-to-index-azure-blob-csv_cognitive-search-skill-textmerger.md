---
merged_at: 2026-01-25T02:11:58.047274
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-azure-blob-csv.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-azure-blob-csv -->

# Index CSV blobs and files using delimitedText parsing mode

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to**: [Blob storage indexers](search-how-to-index-azure-blob-storage), [Files indexers](search-file-storage-integration)

In Azure AI Search, indexers for Azure Blob Storage and Azure Files support a `delimitedText`

parsing mode for CSV files that treats each line in the CSV as a separate search document. For example, given the following comma-delimited text, the `delimitedText`

parsing mode would result in two documents in the search index:

```
id, datePublished, tags
1, 2016-01-12, "azure-search,azure,cloud"
2, 2016-07-07, "cloud,mobile"
```


If a field inside the CSV file contains the delimiter, it should be wrapped in quotes. If the field contains a quote, it must be escaped using double quotes (`""`

).

```
id, datePublished, tags
1, 2020-01-05, "tags,with,""quoted text"""
```


Without the `delimitedText`

parsing mode, the entire contents of the CSV file would be treated as one search document.

Whenever you create multiple search documents from a single blob, be sure to review [Indexing blobs to produce multiple search documents](search-how-to-index-azure-blob-one-to-many) to understand how document key assignments work. The blob indexer is capable of finding or generating values that uniquely define each new document. Specifically, it can create a transitory `AzureSearch_DocumentKey`

when a blob is parsed into smaller parts, where the value is then used as the search document's key in the index.

## Set up CSV indexing

To index CSV blobs, create or update an indexer definition with the `delimitedText`

parsing mode on a [Create Indexer](/en-us/rest/api/searchservice/indexers/create) request.

Only UTF-8 encoding is supported.

```
{
"name" : "my-csv-indexer",
... other indexer properties
"parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
}
```


`firstLineContainsHeaders`

indicates that the first (nonblank) line of each blob contains headers. If blobs don't contain an initial header line, the headers should be specified in the indexer configuration:

```
"parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
```


You can customize the delimiter character using the `delimitedTextDelimiter`

configuration setting. For example:

```
"parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextDelimiter" : "|" } }
```


Note

In delimited text parsing mode, Azure AI Search assumes that all blobs are CSV. If you have a mix of CSV and non-CSV blobs in the same data source, consider using [file extension filters](search-blob-storage-integration#controlling-which-blobs-are-indexed) to control which files are imported on each indexer run.

## Request examples

Putting it all together, here are the complete payload examples.

Datasource:

```
POST https://[service name].search.windows.net/datasources?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
"name" : "my-blob-datasource",
"type" : "azureblob",
"credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
"container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
}
```


Indexer:

```
POST https://[service name].search.windows.net/indexers?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
"name" : "my-csv-indexer",
"dataSourceName" : "my-blob-datasource",
"targetIndexName" : "my-target-index",
"parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
}
```


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-textmerger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-textmerger -->

# Text Merge cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Text Merge** skill consolidates text from an array of strings into a single field.

Note

This skill isn't bound to Foundry Tools. It's nonbillable and has no Foundry Tools key requirement.

## @odata.type

Microsoft.Skills.Text.MergeSkill

## Skill parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
`insertPreTag` |
String to be included before every insertion. The default value is `" "` . To omit the space, set the value to `""` . |
`insertPostTag` |
String to be included after every insertion. The default value is `" "` . To omit the space, set the value to `""` . |

## Skill inputs

| Input name | Description |
|---|---|
`itemsToInsert` |
Array of strings to be merged. |
`text` |
(optional) Main text body to be inserted into. If `text` is not provided, elements of `itemsToInsert` will be concatenated. |
`offsets` |
(optional) Array of positions within `text` where `itemsToInsert` should be inserted. If provided, the number of elements of `text` must equal the number of elements of `textToInsert` . Otherwise all items will be appended at the end of `text` . |

## Skill outputs

| Output name | Description |
|---|---|
`mergedText` |
The resulting merged text. |
`mergedOffsets` |
Array of positions within `mergedText` where elements of `itemsToInsert` were inserted. |

## Sample input

A JSON document providing usable input for this skill could be:

```
{
"values": [
{
"recordId": "1",
"data":
{
"text": "The brown fox jumps over the dog",
"itemsToInsert": ["quick", "lazy"],
"offsets": [3, 28]
}
}
]
}
```


## Sample output

This example shows the output of the previous input, assuming that the *insertPreTag* is set to `" "`

, and *insertPostTag* is set to `""`

.

```
{
"values": [
{
"recordId": "1",
"data":
{
"mergedText": "The quick brown fox jumps over the lazy dog"
}
}
]
}
```


## Extended sample skillset definition

A common scenario for using Text Merge is to merge the textual representation of images (text from an OCR skill, or the caption of an image) into the content field of a document.

The following example skillset uses the OCR skill to extract text from images embedded in the document. Next, it creates a *merged_text* field to contain both original and OCRed text from each image. You can learn more about the OCR skill [here](cognitive-search-skill-ocr).

```
{
"description": "Extract text from images and merge with content text to produce merged_text",
"skills":
[
{
"description": "Extract text (plain and structured) from image.",
"@odata.type": "#Microsoft.Skills.Vision.OcrSkill",
"context": "/document/normalized_images/*",
"defaultLanguageCode": "en",
"detectOrientation": true,
"inputs": [
{
"name": "image",
"source": "/document/normalized_images/*"
}
],
"outputs": [
{
"name": "text"
}
]
},
{
"@odata.type": "#Microsoft.Skills.Text.MergeSkill",
"description": "Create merged_text, which includes all the textual representation of each image inserted at the right location in the content field.",
"context": "/document",
"insertPreTag": " ",
"insertPostTag": " ",
"inputs": [
{
"name":"text",
"source": "/document/content"
},
{
"name": "itemsToInsert",
"source": "/document/normalized_images/*/text"
},
{
"name":"offsets",
"source": "/document/normalized_images/*/contentOffset"
}
],
"outputs": [
{
"name": "mergedText",
"targetName" : "merged_text"
}
]
}
]
}
```


The example above assumes that a normalized-images field exists. To get normalized-images field, set the *imageAction* configuration in your indexer definition to *generateNormalizedImages* as shown below:

```
{
//...rest of your indexer definition goes here ...
"parameters":{
"configuration":{
"dataToExtract":"contentAndMetadata",
"imageAction":"generateNormalizedImages"
}
}
}
```
