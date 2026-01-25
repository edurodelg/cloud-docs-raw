---
merged_at: 2026-01-25T02:11:58.467391
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-how-to-debug-skillset.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-how-to-debug-skillset -->

# Debug an Azure AI Search skillset in Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Start a portal-based debug session to identify and resolve errors, validate changes, and push changes to an existing skillset in your Azure AI Search service.

A debug session is a cached indexer and skillset execution, scoped to a single document, that you can use to edit and test skillset changes interactively. When you're finished debugging, you can save your changes to the skillset.

For background on how a debug session works, see [Debug sessions in Azure AI Search](cognitive-search-debug-session). To practice a debug workflow with a sample document, see [Tutorial: Debug sessions](cognitive-search-tutorial-debug-sessions).

## Prerequisites

An Azure AI Search service, any region or tier.

An Azure Storage account, used to save session state.

An existing enrichment pipeline, including a data source, a skillset, an indexer, and an index.


## Limitations

Debug sessions work with all generally available [indexer data sources](search-data-sources-gallery) and most preview data sources, with the following exceptions:

SharePoint indexer.

Azure Cosmos DB for MongoDB indexer.

For the Azure Cosmos DB for NoSQL, if a row fails during index and there's no corresponding metadata, the debug session might not pick the correct row.

For the SQL API of Azure Cosmos DB, if a partitioned collection was previously non-partitioned, the debug session won't find the document.

For custom skills, a user-assigned managed identity isn't supported for a debug session connection to Azure Storage. As stated in the prerequisites, you can use a system managed identity, or specify a full access connection string that includes a key. For more information, see

[Connect a search service to other Azure resources using a managed identity](search-how-to-managed-identities).

## Security and permissions

To save a debug session to Azure storage, the search service identity must have

**Storage Blob Data Contributor**permissions on Azure Storage. Otherwise, plan on choosing a full access connection string for the debug session connection to Azure Storage.If the Azure Storage account is behind a firewall, configure it to

[allow search service access](search-indexer-howto-access-ip-restricted).

## Create a debug session

Sign in to the

[Azure portal](https://portal.azure.com)and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).On the left menu, select

**Search management**>**Debug sessions**.On the action bar at the top, select

**Add debug session**.In

**Debug session name**, provide a name that will help you remember which skillset, indexer, and data source the debug session is about.In

**Indexer template**, select the indexer that drives the skillset you want to debug. Copies of both the indexer and skillset are used to initialize the session.In

**Document to debug**, choose the first document in the index or select a specific document. If you select a specific document, depending on the data source, you're asked for a URI or a row ID.If your specific document is a blob, provide the blob URI. You can find the URI in the blob property page in the Azure portal.

In

**Storage account**, choose a general-purpose storage account for caching the debug session.Select

**Authenticate using managed identity**if you previously assigned**Storage Blob Data Contributor**permissions to the search service system-managed identity. If you don't check this box, the search service connects using a full access connection string.Select

**Save**.- Azure AI Search creates a blob container on Azure Storage named
*ms-az-cognitive-search-debugsession*. - Within that container, it creates a folder using the name you provided for the session name.
- It starts your debug session.

- Azure AI Search creates a blob container on Azure Storage named

The debug session begins by executing the indexer and skillset on the selected document. The document's content and metadata are visible and available in the session.

A debug session can be canceled while it's executing. If you hit the **Cancel** button you should be able to analyze partial results.

It's expected for a debug session to take longer to execute than the indexer since it goes through extra processing.

## Start with errors and warnings

Indexer execution history in the Azure portal gives you the full error and warning list for all documents. In a debug session, the errors and warnings are limited to one document. You can work through this list, make your changes, and then return to the list to verify whether issues are resolved.

Remember that a debug session is based on one document from the entire index. If an input or output looks wrong, the problem could be specific to that document. You can choose a different document to confirm whether errors and warnings are pervasive or specific to a single document.

Select **Errors** or **Warnings** for a list of issues.

As a best practice, resolve problems with inputs before moving on to outputs.

To prove whether a modification resolves an error, follow these steps:

Select

**Save**in the skill details pane to preserve your changes.Select

**Run**in the session window to invoke skillset execution using the modified definition.Return to

**Errors**or**Warnings**to see if the count is reduced.

## View enriched or generated content

AI enrichment pipelines extract or infer information and structure from source documents, creating an enriched document in the process. An enriched document is first created during document cracking and populated with a root node (`/document`

), plus nodes for any content that is lifted directly from the data source, such as metadata and the document key. More nodes are created by skills during skill execution, where each skill output adds a new node to the enrichment tree.

All content created or used by a skillset appears in the Expression Evaluator. You can hover over the links to view each input or output value in the enriched document tree. To view the input or output of each skill, follow these steps:

In a debug session, expand the blue arrow to view context-sensitive details. By default, the detail is the enriched document data structure. However, if you select a skill or a mapping, the detail is about that object.

Select a skill.

Follow the links to drill further into skills processing. For example, the following screenshot shows the output of the first iteration of the Text Split skill.


## Check index mappings

If skills produce output but the search index is empty, check the field mappings. Field mappings specify how content moves out of the pipeline and into a search index.


Select one of the mapping options and expand the details view to review source and target definitions.

are found in skillsets that provide integrated vectorization, such as the skills created by the**Projection Mappings**. These mappings determine parent-child (chunk) field mappings and whether a secondary index is created for just the chunked content**Import data (new)**wizardare found in indexers and are used when skillsets invoke built-in or custom skills. These mappings are used to set the data path from a node in the enrichment tree to a field in the search index. For more information about paths, see**Output Field Mappings**[enrichment node path syntax](cognitive-search-concept-annotations-syntax).are found in indexer definitions and they establish the data path from raw content in the data source and a field in the index. You can use field mappings to add encoding and decoding steps as well.**Field Mappings**

This example shows the details for a projection mapping. You can edit the JSON to fix any mapping issues.

## Edit skill definitions

If the field mappings are correct, check individual skills for configuration and content. If a skill fails to produce output, it might be missing a property or parameter, which can be determined through error and validation messages.

Other issues, such as an invalid context or input expression, can be harder to resolve because the error will tell you what is wrong, but not how to fix it. For help with context and input syntax, see [Reference enrichments in an Azure AI Search skillset](cognitive-search-concept-annotations-syntax#background-concepts). For help with individual messages, see [Troubleshooting common indexer errors and warnings](cognitive-search-common-errors-warnings).

The following steps show you how to get information about a skill.

Select a skill on the work surface. The Skill details pane opens to the right.

Edit a skill definition using

**Skill Settings**. You can edit the JSON directly.Check the

[path syntax for referencing nodes](cognitive-search-concept-annotations-syntax)in an enrichment tree. Following are some of the most common input paths:`/document/content`

for chunks of text. This node is populated from the blob's content property.`/document/merged_content`

for chunks of text in skillets that include Text Merge skill.`/document/normalized_images/*`

for text that is recognized or inferred from images.


## Debug a custom skill locally

Custom skills can be more challenging to debug because the code runs externally, so the debug session can't be used to debug them. This section describes how to locally debug your Custom Web API skill, debug session, Visual Studio Code and [ngrok](https://ngrok.com/docs) or [Tunnelmole](https://github.com/robbie-cahill/tunnelmole-client). This technique works with custom skills that execute in [Azure Functions](/en-us/azure/azure-functions/functions-overview) or any other Web Framework that runs locally (for example, [FastAPI](https://fastapi.tiangolo.com/)).

### Get a public URL

This section describes two approaches for getting a public URL to a custom skill.

#### Use Tunnelmole

Tunnelmole is an open source tunneling tool that can create a public URL that forwards requests to your local machine through a tunnel.

Install Tunnelmole:

- npm:
`npm install -g tunnelmole`

- Linux:
`curl -s https://tunnelmole.com/sh/install-linux.sh | sudo bash`

- Mac:
`curl -s https://tunnelmole.com/sh/install-mac.sh --output install-mac.sh && sudo bash install-mac.sh`

- Windows: Install by using npm. Or if you don't have Node.js installed, download the
[precompiled .exe file for Windows](https://tunnelmole.com/downloads/tmole.exe)and put it somewhere in your PATH.

- npm:
Run this command to create a new tunnel:

`tmole 7071`

You should see a response that looks like this:

`http://m5hdpb-ip-49-183-170-144.tunnelmole.net is forwarding to localhost:7071 https://m5hdpb-ip-49-183-170-144.tunnelmole.net is forwarding to localhost:7071`

In the preceding example,

`https://m5hdpb-ip-49-183-170-144.tunnelmole.net`

forwards to port`7071`

on your local machine, which is the default port where Azure functions are exposed.

#### Use ngrok

[ ngrok](https://ngrok.com/docs) is a popular, closed source, cross-platform application that can create a tunneling or forwarding URL, so that internet requests reach your local machine. Use ngrok to forward requests from an enrichment pipeline in your search service to your machine to allow local debugging.

Install ngrok.

Open a terminal and go to the folder with the ngrok executable.

Run ngrok with the following command to create a new tunnel:

`ngrok http 7071`

Note

By default, Azure functions are exposed on 7071. Other tools and configurations might require that you provide a different port.

When ngrok starts, copy and save the public forwarding URL for the next step. The forwarding URL is randomly generated.


### Configure in Azure portal

Once you have a public URL for your custom skill, modify your Custom Web API Skill URI within a debug session to call the Tunnelmole or ngrok forwarding URL. Be sure to append "/api/FunctionName" when using Azure Function for executing the skillset code.

You can edit the skill definition in the **Skill settings** section of the **Skill details** pane.

### Test your code

At this point, new requests from your debug session should now be sent to your local Azure Function. You can use breakpoints in your Visual Studio Code to debug your code or run step by step.

## Next steps

Now that you understand the layout and capabilities of the Debug Sessions visual editor, try the tutorial for a hands-on experience.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-textsplit.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-textsplit -->

# Text Split cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Some parameters are in public preview under [Supplemental Terms of Use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). The [preview REST API](/en-us/rest/api/searchservice/index-preview) supports these parameters.

The **Text Split** skill breaks text into chunks of text. You can specify whether you want to break the text into sentences or into pages of a particular length. Positional metadata like offset and ordinal position are also available as outputs. This skill is useful if there are maximum text length requirements in other skills downstream, such as embedding skills that pass data chunks to embedding models on Azure OpenAI and other model providers. For more information about this scenario, see [Chunk documents for vector search](vector-search-how-to-chunk-documents).

Several parameters are version-specific. The skills parameter table notes the API version in which a parameter was introduced so that you know whether a [version upgrade](search-api-migration) is required. To use version-specific features such as *token chunking* in **2024-09-01-preview**, you can use the Azure portal, or target a REST API version, or check an Azure SDK change log to see if it supports the feature.

The Azure portal supports most preview features and can be used to create or update a skillset. For updates to the Text Split skill, edit the skillset JSON definition to add new preview parameters.

Note

This skill isn't bound to Foundry Tools. It's non-billable and has no Foundry Tools key requirement.

## @odata.type

Microsoft.Skills.Text.SplitSkill

## Skill Parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
`textSplitMode` |
Either `pages` or `sentences` . Pages have a configurable maximum length, but the skill attempts to avoid truncating a sentence so the actual length might be smaller. Sentences are a string that terminates at sentence-ending punctuation, such as a period, question mark, or exclamation point, assuming the language has sentence-ending punctuation. |
`maximumPageLength` |
Only applies if `textSplitMode` is set to `pages` . For `unit` set to `characters` , this parameter refers to the maximum page length in characters as measured by `String.Length` . The minimum value is 300, the maximum is 50000, and the default value is 5000. The algorithm does its best to break the text on sentence boundaries, so the size of each chunk might be slightly less than `maximumPageLength` . For `unit` set to `azureOpenAITokens` , the maximum page length is the token length limit of the model. For text embedding models, a general recommendation for page length is 512 tokens. |
`defaultLanguageCode` |
(optional) One of the following language codes: `am, bs, cs, da, de, en, es, et, fr, he, hi, hr, hu, fi, id, is, it, ja, ko, lv, no, nl, pl, pt-PT, pt-BR, ru, sk, sl, sr, sv, tr, ur, zh-Hans` . Default is English (en). A few things to consider:
|
`pageOverlapLength` |
Only applies if `textSplitMode` is set to `pages` . Each page starts with this number of characters or tokens from the end of the previous page. If this parameter is set to 0, there's no overlapping text on successive pages. This
|
`maximumPagesToTake` |
Only applies if `textSplitMode` is set to `pages` . Number of pages to return. The default is 0, which means to return all pages. You should set this value if only a subset of pages are needed. This
|
`unit` |
Only applies if `textSplitMode` is set to `pages` . Specifies whether to chunk by `characters` (default) or `azureOpenAITokens` . Setting the unit affects `maximumPageLength` and `pageOverlapLength` . |
`azureOpenAITokenizerParameters` An object providing extra parameters for the `azureOpenAITokens` unit. `encoderModelName` is a designated tokenizer used for converting text into tokens, essential for natural language processing (NLP) tasks. Different models use different tokenizers. Valid values include cl100k_base (default) used by GPT-4. Other valid values are r50k_base, p50k_base, and p50k_edit. The skill implements the tiktoken library by way of
`Microsoft.ML.Tokenizers` but doesn't support every encoder. For example, there's currently no support for o200k_base encoding used by GPT-4o. `allowedSpecialTokens` defines a collection of special tokens that are permitted within the tokenization process. Special tokens are string that you want to treat uniquely, ensuring they aren't split during tokenization. For example ["[START"], "[END]"]. If the `tiktoken` library doesn't perform tokenization as expected, either due to language-specific limitations or other unexpected behaviors, it's recommended to use text splitting instead. |

## Skill Inputs

| Parameter name | Description |
|---|---|
`text` |
The text to split into substring. |
`languageCode` |
(Optional) Language code for the document. If you don't know the language of the text inputs (for example, if you're using
`languageCode` to a language isn't in the supported list for the `defaultLanguageCode` , a warning is emitted and the text isn't split. |

## Skill Outputs

| Parameter name | Description |
|---|---|
`textItems` |
Output is an array of substrings that were extracted. `textItems` is the default name of the output. `targetName` is optional, but if you have multiple Text Split skills, make sure to set `targetName` so that you don't overwrite the data from the first skill with the second one. If `targetName` is set, use it in output field mappings or in downstream skills that consume the skill output, such as an embedding skill. |
`offsets` |
Output is an array of offsets that were extracted. The value at each index is an object containing the offset of the text item at that index in three encodings: UTF-8, UTF-16, and CodePoint. `offsets` is the default name of the output. `targetName` is optional, but if you have multiple Text Split skills, make sure to set `targetName` so that you don't overwrite the data from the first skill with the second one. If `targetName` is set, use it in output field mappings or in downstream skills that consume the skill output, such as an embedding skill. |
`lengths` |
Output is an array of lengths that were extracted. The value at each index is an object containing the offset of the text item at that index in three encodings: UTF-8, UTF-16, and CodePoint. `lengths` is the default name of the output. `targetName` is optional, but if you have multiple Text Split skills, make sure to set `targetName` so that you don't overwrite the data from the first skill with the second one. If `targetName` is set, use it in output field mappings or in downstream skills that consume the skill output, such as an embedding skill. |
`ordinalPositions` |
Output is an array of ordinal positions corresponding to the position of the text item within the source text. `ordinalPositions` is the default name of the output. `targetName` is optional, but if you have multiple Text Split skills, make sure to set `targetName` so that you don't overwrite the data from the first skill with the second one. If `targetName` is set, use it in output field mappings or in downstream skills that consume the skill output, such as an embedding skill. |

## Sample definition

```
{
"name": "SplitSkill",
"@odata.type": "#Microsoft.Skills.Text.SplitSkill",
"description": "A skill that splits text into chunks",
"context": "/document",
"defaultLanguageCode": "en",
"textSplitMode": "pages",
"unit": "azureOpenAITokens",
"azureOpenAITokenizerParameters":{
"encoderModelName":"cl100k_base",
"allowedSpecialTokens": [
"[START]",
"[END]"
]
},
"maximumPageLength": 512,
"inputs": [
{
"name": "text",
"source": "/document/text"
},
{
"name": "languageCode",
"source": "/document/language"
}
],
"outputs": [
{
"name": "textItems",
"targetName": "pages"
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
"text": "This is the loan application for Joe Romero, a Microsoft employee who was born in Chile and who then moved to Australia...",
"languageCode": "en"
}
},
{
"recordId": "2",
"data": {
"text": "This is the second document, which will be broken into several pages...",
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
"pages": [
"This is the loan...",
"In the next section, we continue..."
],
"offsets": [
{
"utf8": 0,
"utf16": 0,
"codePoint": 0
},
{
"utf8": 146,
"utf16": 146,
"codePoint": 146
}
],
"lengths": [
{
"utf8": 146,
"utf16": 146,
"codePoint": 146
},
{
"utf8": 211,
"utf16": 211,
"codePoint": 211
}
],
"ordinalPositions" : [
1,
2
]
}
},
{
"recordId": "2",
"data": {
"pages": [
"This is the second document...",
"In the next section of the second doc..."
],
"offsets": [
{
"utf8": 0,
"utf16": 0,
"codePoint": 0
},
{
"utf8": 115,
"utf16": 115,
"codePoint": 115
}
],
"lengths": [
{
"utf8": 115,
"utf16": 115,
"codePoint": 115
},
{
"utf8": 209,
"utf16": 209,
"codePoint": 209
}
],
"ordinalPositions" : [
1,
2
]
}
}
]
}
```


Note

This example sets `textItems`

to `pages`

through `targetName`

. Because `targetName`

is set, `pages`

is the value you should use to select the output from the Text Split skill. Use `/document/pages/*`

in downstream skills, indexer [output field mappings](cognitive-search-concept-annotations-syntax), [knowledge store projections](knowledge-store-projection-overview), and [index projections](index-projections-concept-intro).
This example doesn't set `offsets`

, `lengths`

, or `ordinalPosition`

to any other name, so the value you should use in downstream skills would be unchanged.
`offsets`

and `lengths`

are complex types rather than primitives, because they contain the values for multiple encoding types. The value you should use to obtain a specific encoding, for example UTF-8, would look like this: `/document/offsets/*/utf8`

.

## Example for chunking and vectorization

This example is for integrated vectorization.

`pageOverlapLength`

: Overlapping text is useful in[data chunking](vector-search-how-to-chunk-documents)scenarios because it preserves continuity between chunks generated from the same document.`maximumPagesToTake`

: Limits on page intake are useful in[vectorization](vector-search-how-to-generate-embeddings)scenarios because it helps you stay under the maximum input limits of the embedding models providing the vectorization.

### Sample definition

This definition adds `pageOverlapLength`

of 100 characters and `maximumPagesToTake`

of one.

Assuming the `maximumPageLength`

is 5,000 characters (the default), then `"maximumPagesToTake": 1`

processes the first 5,000 characters of each source document.

This example sets `textItems`

to `myPages`

through `targetName`

. Because `targetName`

is set, `myPages`

is the value you should use to select the output from the Text Split skill. Use `/document/myPages/*`

in downstream skills, indexer [output field mappings](cognitive-search-concept-annotations-syntax), [knowledge store projections](knowledge-store-projection-overview), and [index projections](index-projections-concept-intro).

```
{
"@odata.type": "#Microsoft.Skills.Text.SplitSkill",
"textSplitMode" : "pages",
"maximumPageLength": 1000,
"pageOverlapLength": 100,
"maximumPagesToTake": 1,
"defaultLanguageCode": "en",
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
"name": "textItems",
"targetName": "myPages"
}
]
}
```


### Sample input (same as previous example)

```
{
"values": [
{
"recordId": "1",
"data": {
"text": "This is the loan application for Joe Romero, a Microsoft employee who was born in Chile and who then moved to Australia...",
"languageCode": "en"
}
},
{
"recordId": "2",
"data": {
"text": "This is the second document, which will be broken into several sections...",
"languageCode": "en"
}
}
]
}
```


### Sample output (notice the overlap)

Within each "textItems" array, trailing text from the first item is copied into the beginning of the second item.

```
{
"values": [
{
"recordId": "1",
"data": {
"myPages": [
"This is the loan...Here is the overlap part",
"Here is the overlap part...In the next section, we continue..."
]
}
},
{
"recordId": "2",
"data": {
"myPages": [
"This is the second document...Here is the overlap part...",
"Here is the overlap part...In the next section of the second doc..."
]
}
}
]
}
```


## Error cases

If a language isn't supported, a warning is generated.
