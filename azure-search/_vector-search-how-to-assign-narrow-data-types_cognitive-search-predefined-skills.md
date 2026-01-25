---
merged_at: 2026-01-25T03:18:13.764519
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-how-to-assign-narrow-data-types.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-assign-narrow-data-types -->

# Assign narrow data types to vector fields in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An easy way to reduce vector size is to store embeddings in a smaller data format. Most embedding models output 32-bit floating point numbers. However, if you quantize your vectors or use an embedding model that natively supports quantization, the output might be float16, int16, or int8, which are significantly smaller than float32. You can accommodate these smaller vector sizes by assigning a narrow data type to a vector field. In the vector index, narrow data types consume less storage.

You assign data types to fields in an index definition. Use the Azure portal, the [Search Service REST APIs](/en-us/rest/api/searchservice/indexes/create), or an Azure SDK package that provides the feature.

## Prerequisites

- An embedding model that outputs small data formats, such as text-embedding-3 or Cohere V3 embedding models.

## Supported narrow data types

Review the

[data types used for vector fields](/en-us/rest/api/searchservice/supported-data-types#edm-data-types-for-vector-fields)for recommended usage:`Collection(Edm.Single)`

: 32-bit floating point (default)`Collection(Edm.Half)`

: 16-bit floating point (narrow)`Collection(Edm.Int16)`

: 16-bit signed integer (narrow)`Collection(Edm.SByte)`

: 8-bit signed integer (narrow)`Collection(Edm.Byte)`

: 8-bit unsigned integer (only allowed with packed binary data types)

From that list, determine which data type is valid for your embedding model's output or for vectors that undergo custom quantization.

The following table provides links to several embedding models that can use a narrow data type,

`Collection(Edm.Half)`

, without extra quantization. You can cast from float32 to float16 using`Collection(Edm.Half)`

with no extra work.Embedding model Native output Assign this type in Azure AI Search [text-embedding-ada-002](/en-us/azure/ai-foundry/foundry-models/concepts/models-sold-directly-by-azure#embeddings)`Float32`

`Collection(Edm.Single)`

or`Collection(Edm.Half)`

[text-embedding-3-small](/en-us/azure/ai-foundry/foundry-models/concepts/models-sold-directly-by-azure#embeddings)`Float32`

`Collection(Edm.Single)`

or`Collection(Edm.Half)`

[text-embedding-3-large](/en-us/azure/ai-foundry/foundry-models/concepts/models-sold-directly-by-azure#embeddings)`Float32`

`Collection(Edm.Single)`

or`Collection(Edm.Half)`

[Cohere V3 embedding models with int8 embedding_type](https://docs.cohere.com/reference/embed)`Int8`

`Collection(Edm.SByte)`

You can use other narrow data types if your model emits embeddings in the smaller data format or if you have custom quantization that converts vectors to a smaller format.

Understand the tradeoffs of a narrow data type.

`Collection(Edm.Half)`

has less information, which results in lower resolution. If your data is homogeneous or dense, losing extra detail or nuance could lead to unacceptable results at query time because there's less detail that can be used to distinguish nearby vectors apart.

## Assign the data type

[Define and build an index](vector-search-how-to-create-index). You can use the Azure portal, [Indexes - Create Or Update](/en-us/rest/api/searchservice/indexes/create-or-update) (REST API), or an Azure SDK package for this step.

This field definition uses a narrow data type, `Collection(Edm.Half)`

, that accepts a float32 embedding stored as a float16 value. As is true for all vector fields, set the `dimensions`

and `vectorSearchProfile`

properties. The specifics of the `vectorSearchProfile`

are immaterial to the datatype.

Set `retrievable`

and `stored`

to true if you want to visually check the values of the field. On a subsequent rebuild, you can change these properties to false for reduced storage requirements.

```
{
"name": "nameEmbedding",
"type": "Collection(Edm.Half)",
"searchable": true,
"filterable": false,
"retrievable": true,
"sortable": false,
"facetable": false,
"key": false,
"indexAnalyzer": null,
"searchAnalyzer": null,
"analyzer": null,
"synonymMaps": [],
"dimensions": 1536,
"vectorSearchProfile": "myHnswProfile"
}
```


Recall that vector fields aren't filterable, sortable, or facetable. They can't be used as keys and don't use analyzers or synonym maps.

### Working with a production index

You assign data types on new fields when they're created. You can't change the data type of an existing field, and you can't drop a field without [rebuilding the index](search-howto-reindex). For established indexes already in production, a common workaround is to create new fields with the desired revisions and then remove obsolete fields during a planned index rebuild.

## Check results

Verify the field content matches the data type. Assuming the vector field is marked as

`retrievable`

, use[Search explorer](search-explorer)or[Search - POST](/en-us/rest/api/searchservice/documents/search-post?)(REST API) to return vector field content.To check vector index size, refer to the vector index size column on the

**Search management > Indexes**page in the[Azure portal](https://portal.azure.com). You can also use[Indexes - Get Statistics](/en-us/rest/api/searchservice/indexes/get-statistics)(REST API) or an equivalent Azure SDK method.

Note

The field's data type creates the physical data structure. To change a data type later, either [drop and rebuild the index](search-howto-reindex) or create a second field with the new definition.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-predefined-skills.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-predefined-skills -->

# Skills for extra processing during indexing (Azure AI Search)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes the skills in Azure AI Search that you can include in a [skillset](cognitive-search-working-with-skillsets) to access external processing.

A *skill* is an atomic operation that transforms content in some way. Often, it's an operation that recognizes or extracts text, but it can also be a utility skill that reshapes existing enrichments. The output is usually text-based for use in [full-text search](search-lucene-query-architecture) or vectors for use in [vector search](vector-search-overview).

Skills are organized into the following categories:

A

*built-in skill*wraps API calls to another Azure resource, where the inputs, outputs, and processing steps are well understood. Some built-in skills require an attached resource solely for billing, while others use your Azure-hosted model or resource for both billing and processing.A

*custom skill*provides custom code that executes externally to the search service. It's accessed through a URI. Custom code is often made available through an Azure function app. To attach an open-source or third-party vectorization model, use a custom skill.A

*utility skill*is internal to Azure AI Search, with no dependency on external resources or outbound connections. Most utility skills are nonbillable.

## Built-in skills

There are two types of built-in skills:

- Skills that connect to a
[Microsoft Foundry resource](#foundry-resource)(for billing only) - Skills that connect to an
[Azure-hosted model or resource](#azure-hosted-model-or-resource)(for billing and processing)

### Foundry resource

Skills in this category call subservices of Foundry Tools. For billing rather than processing, you must [attach a Foundry resource to your skillset](cognitive-search-attach-cognitive-services). Azure AI Search uses internal resources to execute these skills and only uses your Foundry resource for billing purposes.

A small quantity of processing is nonbillable, but at larger volumes, processing is billable. These skills are based on pretrained models from Foundry Tools, which means you can't train the models using your own data.

These skills are billed at the Standard rate.

| Skill | Description | Metered by |
|---|---|---|
|

[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))[Custom Entity Lookup](cognitive-search-skill-custom-entity-lookup)[pricing](https://azure.microsoft.com/pricing/details/search/))[Entity Linking](cognitive-search-skill-entity-linking-v3)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))[Entity Recognition](cognitive-search-skill-entity-recognition-v3)`"Person"`

, `"Location"`

, `"Organization"`

, `"Quantity"`

, `"DateTime"`

, `"URL"`

, `"Email"`

, `"PersonType"`

, `"Event"`

, `"Product"`

, `"Skill"`

, `"Address"`

, `"Phone Number"`

and `"IP Address"`

fields.[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))[Image Analysis](cognitive-search-skill-image-analysis)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))[Key Phrase Extraction](cognitive-search-skill-keyphrases)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))[Language Detection](cognitive-search-skill-language-detection)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))[OCR](cognitive-search-skill-ocr)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))[PII Detection](cognitive-search-skill-pii-detection)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))[Sentiment](cognitive-search-skill-sentiment-v3)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))[Text Translation](cognitive-search-skill-text-translation)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/))### Azure-hosted model or resource

Skills in this category call Azure-hosted models or resources that you own for both billing and processing. Although Azure Content Understanding is part of Foundry Tools, the Azure Content Understanding skill connects to your deployed resource for processing, not just billing.

These skills are billed at the Standard rate.

| Skill | Description | Metered by |
|---|---|---|
|

[pricing](https://azure.microsoft.com/pricing/details/content-understanding/))[Azure OpenAI Embedding](cognitive-search-skill-azure-openai-embedding)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/#pricing))[GenAI Prompt](cognitive-search-skill-genai-prompt)[pricing](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/#pricing))## Custom skills

Skills in this category wrap external code that you design, develop, and deploy to the web. You can then call the module from within a skillset as a custom skill.

For guidance on creating a custom skill, see [Define a custom interface](cognitive-search-custom-skill-interface) and [Example: Creating a custom skill for AI enrichment](cognitive-search-create-custom-skill-example).

| Skill | Description | Metered by |
|---|---|---|
|

[Custom Entity Lookup](cognitive-search-skill-custom-entity-lookup)[Web API](cognitive-search-custom-skill-web-api)## Utility skills

Skills in this category execute only on Azure AI Search, iterate mostly on nodes in the enrichment cache, and are mostly nonbillable.

| Skill | Description | Metered by |
|---|---|---|
|
