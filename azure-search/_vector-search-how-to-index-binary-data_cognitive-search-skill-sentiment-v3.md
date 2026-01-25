---
merged_at: 2026-01-25T02:11:58.371183
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-how-to-index-binary-data.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-index-binary-data -->

# Index binary vectors for vector search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search supports the `Collection(Edm.Byte)`

packed binary type to further reduce the storage and memory footprint of vector data. You can use this data type for the output of models such as [Cohere's Embed v3 binary embedding models](https://cohere.com/blog/int8-binary-embeddings) or any other embedding model or process that outputs vectors as binary bytes.

There are three steps to configuring an index for binary vectors:

- Add a vector search algorithm that specifies Hamming distance for binary vector comparison
- Add a vector profile that points to the algorithm
- Add a vector field of type
`Collection(Edm.Byte)`

and assign the Hamming distance

This article uses the REST APIs for illustration, but you can also use an Azure SDK or the Azure portal to add a binary field to an index. You assign the binary data type to fields by using the [Indexes - Create](/en-us/rest/api/searchservice/indexes/create) or [Indexes - Create Or Update](/en-us/rest/api/searchservice/indexes/create-or-update) REST APIs.

Tip

If you're investigating binary vector support for its smaller footprint, you might also consider the vector quantization and storage reduction features in Azure AI Search. Inputs are float32 or float16 embeddings. Output is stored data in a much smaller format. For more information, see [Compress using binary or scalar quantization](vector-search-how-to-quantization) and [Assign narrow data types](vector-search-how-to-assign-narrow-data-types).

## Prerequisites

Familiarity with

[creating an index](search-how-to-create-search-index)and[adding vector fields](vector-search-how-to-create-index).Binary vectors, with one bit per dimension, packaged in uint8 values with eight bits per value. You can get these vectors by using models that directly generate

*packaged binary*vectors or by quantizing vectors into binary vectors in your client application during indexing and retrieval.

## Limitations

No Azure portal support in the

**Import data (new)**wizard.No support for binary fields in the

[AML skill](cognitive-search-aml-skill)that's used for integrated vectorization of models from the Microsoft Foundry model catalog.

## Add a vector search algorithm and vector profile

Vector search algorithms create the query navigation structures during indexing. For binary vector fields, the system uses the Hamming distance metric to perform vector comparisons.

To configure vector search for binary vectors:

Set up an

[Indexes - Create or Update](/en-us/rest/api/searchservice/indexes/create-or-update)(REST API) request.In the index schema, add a

`vectorSearch`

section that specifies profiles and algorithms.Add one or more

[vector search algorithms](vector-search-ranking)that use a similarity metric of`hamming`

. The Hierarchical Navigable Small Worlds (HNSW) algorithm is common, but you can also use Hamming distance with exhaustive K-Nearest Neighbors (KNN).Add one or more vector profiles that specify the algorithm.


The following example shows a basic `vectorSearch`

configuration.

```
"vectorSearch": {
"profiles": [
{
"name": "myHnswProfile",
"algorithm": "myHnsw",
"compression": null,
"vectorizer": null
}
],
"algorithms": [
{
"name": "myHnsw",
"kind": "hnsw",
"hnswParameters": {
"metric": "hamming"
}
},
{
"name": "myExhaustiveKnn",
"kind": "exhaustiveKnn",
"exhaustiveKnnParameters": {
"metric": "hamming"
}
}
]
}
```


## Add a binary field to an index

The fields collection of an index must include a field for the document key, vector fields, and any other fields you need for hybrid search scenarios.

Binary fields use the `Collection(Edm.Byte)`

type and contain embeddings in packed form. For example, if the original embedding dimension is `1024`

, the packed binary vector length is `ceiling(1024 / 8) = 128`

. You get the packed form by setting the `vectorEncoding`

property on the field.

To add a binary vector field to an index:

Add a field to the fields collection and give it a name.

Set the data type to

`Collection(Edm.Byte)`

.Set

`vectorEncoding`

to`packedBit`

for binary encoding.Set

`dimensions`

to`1024`

. Specify the original (unpacked) vector dimension.Set

`vectorSearchProfile`

to a profile you defined in the previous step.Set

`searchable`

to`true`

.

The following field definition is an example of a binary vector field in an index schema.

```
"fields": [
. . .
{
"name": "my-binary-vector-field",
"type": "Collection(Edm.Byte)",
"vectorEncoding": "packedBit",
"dimensions": 1024,
"vectorSearchProfile": "myHnswProfile",
"searchable": true
},
. . .
]
```


## Related content

Review the

[azure-search-vector-samples](https://github.com/Azure/azure-search-vector-samples)repository for end-to-end workflows that include schema definition, vectorization, indexing, and queries.Review the vector search demo code for

[C#](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-dotnet),[Python](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-python), and[JavaScript](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-javascript).


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-sentiment-v3.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-sentiment-v3 -->

# Sentiment cognitive skill (v3)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Sentiment** skill (v3) evaluates unstructured text and for each record, provides sentiment labels (such as "negative", "neutral" and "positive") based on the highest confidence score found by the service at a sentence and document-level. This skill uses the machine learning models provided by version 3 of [Language Service](/en-us/azure/ai-services/language-service/overview) in Foundry Tools. It also exposes [opinion mining capabilities](/en-us/azure/ai-services/language-service/sentiment-opinion-mining/overview), which provides more granular information about the opinions related to attributes of products or services in text.

Note

This skill is bound to Foundry Tools and requires [a billable resource](cognitive-search-attach-cognitive-services) for transactions that exceed 20 documents per indexer per day. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

## @odata.type

Microsoft.Skills.Text.V3.SentimentSkill

## Data limits

The maximum size of a record should be 5000 characters as measured by [ String.Length](/en-us/dotnet/api/system.string.length). If you need to break up your data before sending it to the sentiment skill, use the

[Text Split skill](cognitive-search-skill-textsplit).

## Skill parameters

Parameters are case sensitive.

| Parameter Name | Description |
|---|---|
`defaultLanguageCode` |
(optional) The language code to apply to documents that don't specify language explicitly. See the
|
`modelVersion` |
(optional) Specifies the
|

`includeOpinionMining`

`true`

, enables [the opinion mining feature](/en-us/azure/ai-services/language-service/sentiment-opinion-mining/overview#opinion-mining), which allows aspect-based sentiment analysis to be included in your output results. Defaults to`false`

.## Skill inputs

| Input Name | Description |
|---|---|
`text` |
The text to be analyzed. |
`languageCode` |
(optional) A string indicating the language of the records. If this parameter is not specified, the default value is "en". See the
|

## Skill outputs

| Output Name | Description |
|---|---|
`sentiment` |
A string value that represents the sentiment label of the entire analyzed text (either positive, neutral or negative). |
`confidenceScores` |
A complex type with three double values, one for the positive rating, one for the neutral rating, and one for the negative rating. Values range from 0 to 1.00, where 1.00 represents the highest possible confidence in a given label assignment. |
`sentences` |
A collection of complex types that breaks down the sentiment of the text sentence by sentence. This is also where opinion mining results are returned in the form of targets and assessments if `includeOpinionMining` is set to `true` . |

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Text.V3.SentimentSkill",
"context": "/document",
"includeOpinionMining": true,
"inputs": [
{
"name": "text",
"source": "/document/content"
},
{
"name": "languageCode",
"source": "/document/languageCode"
}
],
"outputs": [
{
"name": "sentiment",
"targetName": "sentiment"
},
{
"name": "confidenceScores",
"targetName": "confidenceScores"
},
{
"name": "sentences",
"targetName": "sentences"
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
"sentiment": "negative",
"confidenceScores": {
"positive": 0.0,
"neutral": 0.0,
"negative": 1.0
},
"sentences": [
{
"text": "I had a terrible time at the hotel.",
"sentiment": "negative",
"confidenceScores": {
"positive": 0.0,
"neutral": 0.0,
"negative": 1.0
},
"offset": 0,
"length": 35,
"targets": [],
"assessments": [],
},
{
"text": "The staff was rude and the food was awful.",
"sentiment": "negative",
"confidenceScores": {
"positive": 0.0,
"neutral": 0.0,
"negative": 1.0
},
"offset":36,
"length": 42,
"targets": [
{
"text": "staff",
"sentiment": "negative",
"confidenceScores": {
"positive": 0.0,
"neutral": 0.0,
"negative": 1.0
},
"offset": 40,
"length": 5,
"relations": [
{
"relationType": "assessment",
"ref": "#/documents/0/sentences/1/assessments/0",
}
]
},
{
"text": "food",
"sentiment": "negative",
"confidenceScores": {
"positive": 0.0,
"neutral": 0.0,
"negative": 1.0
},
"offset": 63,
"length": 4,
"relations": [
{
"relationType": "assessment",
"ref": "#/documents/0/sentences/1/assessments/1",
}
]
}
],
"assessments": [
{
"text": "rude",
"sentiment": "negative",
"confidenceScores": {
"positive": 0.0,
"neutral": 0.0,
"negative": 1.0
},
"offset": 50,
"length": 4,
"isNegated": false
},
{
"text": "awful",
"sentiment": "negative",
"confidenceScores": {
"positive": 0.0,
"neutral": 0.0,
"negative": 1.0
},
"offset": 72,
"length": 5,
"isNegated": false
}
],
}
]
}
}
]
}
```


## Warning cases

If your text is empty, a warning is generated and no sentiment results are returned. If a language is not supported, a warning is generated and no sentiment results are returned.
