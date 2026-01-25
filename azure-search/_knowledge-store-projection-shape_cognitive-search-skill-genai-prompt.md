---
merged_at: 2026-01-25T03:18:13.808371
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: knowledge-store-projection-shape.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/knowledge-store-projection-shape -->

# Shaping data for projection into a knowledge store

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

*Knowledge stores* are secondary storage that exists in Azure Storage and contain the outputs of Azure AI Search skillsets. They're separate from knowledge sources and knowledge bases, which are used in [agentic retrieval](agentic-retrieval-overview) workflows.

In Azure AI Search, "shaping data" describes a step in the [knowledge store workflow](knowledge-store-concept-intro) that creates a data representation of the content that you want to project into tables, objects, and files in Azure Storage.

As skills execute, the outputs are written to an enrichment tree in a hierarchy of nodes, and while you might want to view and consume the enrichment tree in its entirety, it's more likely that you'll want a finer grain, creating subsets of nodes for different scenarios, such as placing the nodes related to translated text or extracted entities in specific tables.

By itself, the enrichment tree doesn't include logic that would inform how its content is represented in a knowledge store. Data shapes fill this gap by providing the schema of what goes into each table, object, and file projection. You can think of a data shape as a custom definition or view of the enriched data. You can create as many shapes as you need, and then assign them to [projections](knowledge-store-projection-overview) in a knowledge store definition.

## Approaches for creating shapes

There are two ways to shape enriched content so that it can be projected into a knowledge store:

Use the

[Shaper skill](cognitive-search-skill-shaper)to create nodes in an enrichment tree that are used expressly for projection. Most skills create new content. In contrast, a Shaper skill works with existing nodes, usually to consolidate multiple nodes into a single complex object. This is useful for tables, where you want the output of multiple nodes to be physically expressed as columns in the table.Use an inline shape within the projection definition itself.


Using the Shaper skill externalizes the shape so that it can be used by multiple projections or even other skills. It also ensures that all the mutations of the enrichment tree are contained within the skill, and that the output is an object that can be reused. In contrast, inline shaping allows you to create the shape you need, but is an anonymous object and is only available to the projection for which it's defined.

The approaches can be used together or separately. This article shows both: a Shaper skill for the table projections, and inline shaping with the key phrases table projection.

## Use a Shaper skill

Shaper skills are usually placed at the end of a skillset, creating a view of the data that you want to pass to a projection. This example creates a shape called "tableprojection" containing the following nodes: "reviews_text", "reviews_title", "AzureSearch_DocumentKey", and sentiment scores and key phrases from paged reviews.

```
{
"@odata.type": "#Microsoft.Skills.Util.ShaperSkill",
"name": "#5",
"description": null,
"context": "/document",
"inputs": [
{
"name": "reviews_text",
"source": "/document/reviews_text",
"sourceContext": null,
"inputs": []
},
{
"name": "reviews_title",
"source": "/document/reviews_title",
"sourceContext": null,
"inputs": []
},
{
"name": "AzureSearch_DocumentKey",
"source": "/document/AzureSearch_DocumentKey",
"sourceContext": null,
"inputs": []
},
{
"name": "pages",
"source": null,
"sourceContext": "/document/reviews_text/pages/*",
"inputs": [
{
"name": "Sentiment",
"source": "/document/reviews_text/pages/*/Sentiment",
"sourceContext": null,
"inputs": []
},
{
"name": "LanguageCode",
"source": "/document/Language",
"sourceContext": null,
"inputs": []
},
{
"name": "Page",
"source": "/document/reviews_text/pages/*",
"sourceContext": null,
"inputs": []
},
{
"name": "keyphrase",
"sourceContext": "/document/reviews_text/pages/*/Keyphrases/*",
"inputs": [
{
"source": "/document/reviews_text/pages/*/Keyphrases/*",
"name": "Keyphrases"
}
]
}
]
}
],
"outputs": [
{
"name": "output",
"targetName": "tableprojection"
}
]
}
```


### SourceContext property

Within a Shaper skill, an input can have a `sourceContext`

element. This same property can also be used in inline shapes in projections.

`sourceContext`

is used to construct multi-level, nested objects in an enrichment pipeline. If the input is at a *different* context than the skill context, use the *sourceContext*. The *sourceContext* requires you to define a nested input with the specific element being addressed as the source.

In the previous example, sentiment analysis and key phrases extraction was performed on text that was split into pages for more efficient analysis. Assuming you want the scores and phrases projected into a table, you'll now need to set the context to nested input that provides the score and phrase.

### Projecting a shape into multiple tables

With the `tableprojection`

node defined in the `outputs`

in the previous section, you can slice parts of the `tableprojection`

node into individual, related tables:

```
"projections": [
{
"tables": [
{
"tableName": "hotelReviewsDocument",
"generatedKeyName": "Documentid",
"source": "/document/tableprojection"
},
{
"tableName": "hotelReviewsPages",
"generatedKeyName": "Pagesid",
"source": "/document/tableprojection/pages/*"
},
{
"tableName": "hotelReviewsKeyPhrases",
"generatedKeyName": "KeyPhrasesid",
"source": "/document/tableprojection/pages/*/keyphrase/*"
}
]
}
]
```


## Inline shape for table projections

Inline shaping is the ability to form new shapes within the projection definition itself. Inline shaping has these characteristics:

- The shape is used only by the projection that contains it.
- The shape can be identical to what a Shaper skill produces.

An inline shape is created using `sourceContext`

and `inputs`

.

| Property | Description |
|---|---|
| sourceContext | Sets the root of the projection. |
| inputs | Each input is a column in the table. Name is the column name. Source is the enrichment node that provides the value. |

To project the same data as the previous example, the inline projection option would look like this:

```
"projections": [
{
"tables": [
{
"tableName": "hotelReviewsInlineDocument",
"generatedKeyName": "Documentid",
"sourceContext": "/document",
"inputs": [
{
"name": "reviews_text",
"source": "/document/reviews_text"
},
{
"name": "reviews_title",
"source": "/document/reviews_title"
},
{
"name": "AzureSearch_DocumentKey",
"source": "/document/AzureSearch_DocumentKey"
}
]
},
{
"tableName": "hotelReviewsInlinePages",
"generatedKeyName": "Pagesid",
"sourceContext": "/document/reviews_text/pages/*",
"inputs": [
{
"name": "Sentiment",
"source": "/document/reviews_text/pages/*/Sentiment"
},
{
"name": "LanguageCode",
"source": "/document/Language"
},
{
"name": "Page",
"source": "/document/reviews_text/pages/*"
}
]
},
{
"tableName": "hotelReviewsInlineKeyPhrases",
"generatedKeyName": "KeyPhraseId",
"sourceContext": "/document/reviews_text/pages/*/Keyphrases/*",
"inputs": [
{
"name": "Keyphrases",
"source": "/document/reviews_text/pages/*/Keyphrases/*"
}
]
}
]
}
]
```


One observation from both the approaches is how values of "Keyphrases" are projected using the "sourceContext". The "Keyphrases" node, which contains a collection of strings, is itself a child of the page text. However, because projections require a JSON object and the page is a primitive (string), the "sourceContext" is used to wrap the key phrase into an object with a named property. This technique enables even primitives to be projected independently.

## Inline shape for object projections

You can generate a new shape using the Shaper skill or use inline shaping of the object projection. While the tables example demonstrated the approach of creating a shape and slicing, this example demonstrates the use of inline shaping.

Inline shaping is the ability to create a new shape in the definition of the inputs to a projection. Inline shaping creates an anonymous object that is identical to what a Shaper skill would produce (in this case, `projectionShape`

). Inline shaping is useful if you're defining a shape that you don't plan to reuse.

The projections property is an array. This example adds a new projection instance to the array, where the knowledgeStore definition contains inline projections. When using inline projections, you can omit the Shaper skill.

```
"knowledgeStore" : {
"storageConnectionString": "DefaultEndpointsProtocol=https;AccountName=<Acct Name>;AccountKey=<Acct Key>;",
"projections": [
{
"tables": [ ],
"objects": [
{
"storageContainer": "sampleobject",
"source": null,
"generatedKeyName": "myobject",
"sourceContext": "/document",
"inputs": [
{
"name": "metadata_storage_name",
"source": "/document/metadata_storage_name"
},
{
"name": "metadata_storage_path",
"source": "/document/metadata_storage_path"
},
{
"name": "content",
"source": "/document/content"
},
{
"name": "keyPhrases",
"source": "/document/merged_content/keyphrases/*"
},
{
"name": "entities",
"source": "/document/merged_content/entities/*/name"
},
{
"name": "ocrText",
"source": "/document/normalized_images/*/text"
},
{
"name": "ocrLayoutText",
"source": "/document/normalized_images/*/layoutText"
}
]
}
],
"files": []
}
]
}
```


## Next steps

This article describes the concepts and principles of projection shapes. As a next step, see how these are applied in patterns for table, object, and file projections.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-genai-prompt.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-genai-prompt -->

# GenAI Prompt skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

The **GenAI (Generative AI) Prompt** skill executes a *chat completion* request against a large language model (LLM) deployed in [Azure OpenAI in Foundry Models](/en-us/azure/ai-services/openai/overview) or [Microsoft Foundry](../ai-foundry/what-is-foundry). Use this skill to create new information that can be indexed and stored as searchable content.

Here are some examples of how the GenAI prompt skill can help you create content:

- Verbalize images
- Summarize large passages of text
- Simplify complex content
- Perform any other task that you can articulate in a prompt

The GenAI Prompt skill is available in the [latest preview REST API](/en-us/rest/api/searchservice/skillsets/create?view=rest-searchservice-2025-11-01-preview&preserve-view=true). This skill supports text, image, and multimodal content, such as a PDF that contains text and images.

Tip

It's common to use this skill combined with a data chunking skill. The following tutorials demonstrate image verbalization with two different data chunking techniques:

## Supported models

You can use any

[chat completion inference model](../ai-foundry/foundry-models/concepts/models)deployed in Foundry, such as GPT models, Deepseek R#, Llama-4-Mavericj, and Cohere-command-r. For GPT models specifically, only the chat completions API endpoints are supported. Endpoints using the Azure OpenAI Responses API (containing`/openai/responses`

in the URI) aren't currently compatible.For image verbalization, the model you use to analyze the image determines what image formats are supported.

For GPT-5 models, the

`temperature`

parameter is not supported in the same way as previous models. If defined, it must be set to`1.0`

, as other values will result in errors.Billing is based on the pricing of the model you use.


Note

The search service connects to your model over a public endpoint, so there are no region location requirements, but if you're using an all-up Azure solution, you should check the [Azure AI Search regions](search-region-support) and the [Azure OpenAI model regions](/en-us/azure/ai-services/openai/concepts/models) to find suitable pairs, especially if you have data residency requirements.

## Prerequisites

An

[Azure OpenAI in Foundry Models resource](../ai-foundry/openai/how-to/create-resource)or[Foundry project](../ai-foundry/how-to/create-projects).A

[supported model](#supported-models)deployed to your resource or project.For Azure OpenAI, copy the endpoint with the

`openai.azure.com`

domain from the**Keys and Endpoint**page in the Azure portal. Use this endpoint for the`Uri`

parameter in this skill.For Foundry, copy the target URI for the deployment from the

**Models**page in the Foundry portal. Use this endpoint for the`Uri`

parameter in this skill.

Authentication can be key-based with an API key from your Foundry or Azure OpenAI resource. However, we recommend role-based access using a

[search service managed identity](search-how-to-managed-identities)assigned to a role.On Azure OpenAI, assign

to the managed identity.**Cognitive Services OpenAI User**On Foundry, assign

to the managed identity.**Azure AI User**


## @odata.type

`#Microsoft.Skills.Custom.ChatCompletionSkill`


## Data limits

| Limit | Notes |
|---|---|
`maxTokens` |
Default is 1024 if omitted. Maximum value is model-dependent. |
| Request time-out | 30 seconds (default). Override with the `timeout` property (`PT##S` ). |
| Images | Base 64–encoded images and image URLs are supported. Size limit is model-dependent. |

## Skill parameters

| Property | Type | Required | Notes |
|---|---|---|---|
`uri` |
string | Yes | Public endpoint of the deployed model. Supported domains are:
|
`apiKey` |
string | Cond.* | Secret key for the model. Leave blank when using managed identity. |
`authIdentity` |
string | Cond.* | User-assigned managed identity client ID (Azure OpenAI only). Leave blank to use the system-assigned identity. |
`commonModelParameters` |
object | No | Standard generation controls such as `temperature` , `maxTokens` , etc. |
`extraParameters` |
object | No | Open dictionary passed through to the underlying model API. |
`extraParametersBehavior` |
string | No | `"pass-through"` | `"drop"` | `"error"` (default `"error"` ). |
`responseFormat` |
object | No | Controls whether the model returns text, a free-form JSON object, or a strongly typed JSON schema. `responseFormat` payload examples: {responseFormat: { type: text }}, {responseFormat: { type: json_object }}, {responseFormat: { type: json_schema }} |

* **Exactly one** of `apiKey`

, `authIdentity`

, or the service’s **system-assigned** identity must be used.

`commonModelParameters`

defaults

| Parameter | Default |
|---|---|
`model` |
(deployment default) |
`frequencyPenalty` |
0 |
`presencePenalty` |
0 |
`maxTokens` |
1024 |
`temperature` |
0.7 |
`seed` |
null |
`stop` |
null |

## Skill inputs

| Input name | Type | Required | Description |
|---|---|---|---|
`systemMessage` |
string | Yes | System-level instruction (ex: "You are a helpful assistant."). |
`userMessage` |
string | Yes | User prompt. |
`text` |
string | No | Optional text appended to `userMessage` (text-only scenarios). |
`image` |
string (Base 64 data-URL) | No | Adds an image to the prompt (multimodal models only). |
`imageDetail` |
string (`low` | `high` | `auto` ) |
No | Fidelity hint for Azure OpenAI multimodal models. |

## Skill outputs

| Output name | Type | Description |
|---|---|---|
`response` |
string or JSON object |
Model output in the format requested by `responseFormat.type` . |
`usageInformation` |
JSON object | Token counts and echo of model parameters. |

## Sample definitions

### Text-only summarization

```
{
"@odata.type": "#Microsoft.Skills.Custom.ChatCompletionSkill",
"name": "Summarizer",
"description": "Summarizes document content.",
"context": "/document",
"timeout": "PT30S",
"inputs": [
{ "name": "text", "source": "/document/content" },
{ "name": "systemMessage", "source": "='You are a concise AI assistant.'" },
{ "name": "userMessage", "source": "='Summarize the following text:'" }
],
"outputs": [ { "name": "response" } ],
"uri": "https://demo.openai.azure.com/openai/deployments/gpt-4o/chat/completions",
"apiKey": "<api-key>",
"commonModelParameters": { "temperature": 0.3 }
}
```


### Text + image description

```
{
"@odata.type": "#Microsoft.Skills.Custom.ChatCompletionSkill",
"name": "Image Describer",
"context": "/document/normalized_images/*",
"inputs": [
{ "name": "image", "source": "/document/normalized_images/*/data" },
{ "name": "imageDetail", "source": "=high" },
{ "name": "systemMessage", "source": "='You are a useful AI assistant.'" },
{ "name": "userMessage", "source": "='Describe this image:'" }
],
"outputs": [ { "name": "response" } ],
"uri": "https://demo.openai.azure.com/openai/deployments/gpt-4o/chat/completions",
"authIdentity": "11111111-2222-3333-4444-555555555555",
"responseFormat": { "type": "text" }
}
```


### Structured numerical fact-finder

```
{
"@odata.type": "#Microsoft.Skills.Custom.ChatCompletionSkill",
"name": "NumericalFactFinder",
"context": "/document",
"inputs": [
{ "name": "systemMessage", "source": "='You are an AI assistant that helps people find information.'" },
{ "name": "userMessage", "source": "='Find all the numerical data and put it in the specified fact format.'"},
{ "name": "text", "source": "/document/content" }
],
"outputs": [ { "name": "response" } ],
"uri": "https://demo.openai.azure.com/openai/deployments/gpt-4o/chat/completions",
"apiKey": "<api-key>",
"responseFormat": {
"type": "json_schema",
"jsonSchemaProperties": {
"name": "NumericalFactObj",
"strict": true,
"schema": {
"type": "object",
"properties": {
"facts": {
"type": "array",
"items": {
"type": "object",
"properties": {
"number": { "type": "number" },
"fact": { "type": "string" }
},
"required": [ "number", "fact" ]
}
}
},
"required": [ "facts" ],
"additionalProperties": false
}
}
}
}
```


### Sample output (truncated)

```
{
"response": {
"facts": [
{ "number": 32.0, "fact": "Jordan scored 32 points per game in 1986-87." },
{ "number": 6.0, "fact": "He won 6 NBA championships." }
]
},
"usageInformation": {
"usage": {
"completion_tokens": 203,
"prompt_tokens": 248,
"total_tokens": 451
}
}
}
```


### Best practices

- Chunk long documents with the
**Text Split**skill to stay within the model’s context window. - For high-volume indexing, dedicate a separate model deployment to this skill so that token quotas for query-time RAG workloads remain unaffected.
- To minimize latency, co-locate the model and your Azure AI Search service in the same Azure region.
- Use
`responseFormat.json_schema`

with**GPT-4o**for reliable structured extraction and easier mapping to index fields. - Monitor token usage and submit
**quota-increase requests**if the indexer saturates your Tokens per Minute (TPM) limits.

### Errors and warnings

| Condition | Result |
|---|---|
Missing or invalid `uri` |
Error |
| No authentication method specified | Error |
Both `apiKey` and `authIdentity` supplied |
Error |
| Unsupported model for multimodal prompt | Error |
| Input exceeds model token limit | Error |
Model returns invalid JSON for `json_schema` |
Warning – raw string returned in `response` |
