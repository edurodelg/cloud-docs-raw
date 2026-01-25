---
merged_at: 2026-01-25T03:18:14.104982
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-how-to-semantic-chunking.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-semantic-chunking -->

# Chunk and vectorize by document layout or structure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Text data chunking strategies play a key role in optimizing RAG responses and performance. By using the **Document Layout** skill, you can chunk content based on document structure, capturing headings and chunking the content body based on semantic coherence, such as paragraphs and sentences. Chunks are processed independently. Because LLMs work with multiple chunks, when those chunks are of higher quality and semantically coherent, the overall relevance of the query is improved.

The Document Layout skill calls the [layout model](/en-us/azure/ai-services/document-intelligence/prebuilt/layout) from Azure Document Intelligence in Foundry Tools. The model articulates content structure in JSON using Markdown syntax (headings and content), with fields for headings and content stored in a search index on Azure AI Search. The searchable content produced from the Document Layout skill is plain text but you can apply integrated vectorization to generate embeddings for any field in your source documents, including images.

In this article, learn how to:

- Use the Document Layout skill to recognize document structure
- Use the Text Split skill to constrain chunk size to each Markdown section
- Generate embeddings for each chunk
- Use index projections to map embeddings to fields in a search index

For illustration purposes, this article uses the [sample health plan PDFs](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/health-plan) uploaded to Azure Blob Storage and then indexed using the **Import data (new)** wizard.

## Prerequisites

[An indexer-based indexing pipeline](search-indexer-overview)with an index that accepts the output. The index must have fields for receiving headings and content.[An index projection](search-how-to-define-index-projections)for one-to-many indexing.[A supported data source](search-indexer-overview#supported-data-sources)having text content that you want to chunk.A skillset with these two skills:

[Document Layout skill](cognitive-search-skill-document-intelligence-layout)that splits documents based on paragraph boundaries. If you use[key-based billing](cognitive-search-attach-cognitive-services), this skill requires Microsoft Foundry to be in the same region as Azure AI Search for AI enrichment. Region requirements are relaxed for keyless billing (preview).[Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding)that generates vector embeddings. This skill*doesn't*have region requirements.


## Prepare data files

You must use a [supported data source](search-indexer-overview#supported-data-sources) for the raw inputs, and the file must be in a format supported by the [Document Layout skill](cognitive-search-skill-document-intelligence-layout).

Supported file formats include PDF, JPEG, JPG, PNG, BMP, TIFF, DOCX, XLSX, PPTX, and HTML.

Supported indexers are any indexer that can handle the supported file formats. These indexers include

[Blob indexers](search-how-to-index-azure-blob-storage),[Microsoft OneLake indexers](search-how-to-index-onelake-files), and[File indexers](search-file-storage-integration).Supported regions for the portal experience of this feature include East US, West Europe, and North Central US. If you're setting up your skillset programmatically, you can use any Azure Document Intelligence region that also provides the AI enrichment feature of Azure AI Search. For more information, see

[Supported regions for the Document Layout skill](cognitive-search-skill-document-intelligence-layout#supported-regions).

You can use the Azure portal, REST APIs, or an Azure SDK package to [create a data source](search-how-to-index-azure-blob-storage).

Tip

To try the Document Layout skill and structure-aware chunking on your own search service, upload the [health plan PDF](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/health-plan) sample files to your supported data source. The [ Import data (new) wizard](search-get-started-portal-import-vectors) is an easy code-free approach for trying out this skill. Be sure to select the

**default parsing mode**to use structure-aware chunking. Otherwise, the

[Markdown parsing mode](search-how-to-index-azure-blob-markdown)is used.

## Create an index for one-to-many indexing

The following example shows a single search document designed around chunks. When you work with chunks, you need a chunk field and a parent field that identifies the chunk's origin. In this example, parent fields are the `text_parent_id`

fields. Child fields are the vector and nonvector chunks of the Markdown section.

The Document Layout skill outputs headings and content. In this example, `header_1`

through `header_3`

store document headings, as detected by the skill. Other content, such as paragraphs, is stored in `chunk`

. The `text_vector`

field is a vector representation of the chunk field content.

You can use the **Import data (new)** wizard in the Azure portal, REST APIs, or an Azure SDK to [create an index](search-how-to-load-search-index). The following index is very similar to what the wizard creates by default. You might have more fields if you add image vectorization.

If you aren't using the wizard, the index must exist on the search service before you create the skillset or run the indexer.

```
{
"name": "my_consolidated_index",
"fields": [
{
"name": "chunk_id",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"retrievable": true,
"stored": true,
"sortable": true,
"facetable": false,
"key": true,
"analyzer": "keyword"
},
{
"name": "text_parent_id",
"type": "Edm.String",
"searchable": false,
"filterable": true,
"retrievable": true,
"stored": true,
"sortable": false,
"facetable": false,
"key": false
},
{
"name": "chunk",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"retrievable": true,
"stored": true,
"sortable": false,
"facetable": false,
"key": false
},
{
"name": "title",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"retrievable": true,
"stored": true,
"sortable": false,
"facetable": false,
"key": false
},
{
"name": "header_1",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"retrievable": true,
"stored": true,
"sortable": false,
"facetable": false,
"key": false
},
{
"name": "header_2",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"retrievable": true,
"stored": true,
"sortable": false,
"facetable": false,
"key": false
},
{
"name": "header_3",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"retrievable": true,
"stored": true,
"sortable": false,
"facetable": false,
"key": false
},
{
"name": "text_vector",
"type": "Collection(Edm.Single)",
"searchable": true,
"filterable": false,
"retrievable": true,
"stored": true,
"sortable": false,
"facetable": false,
"key": false,
"dimensions": 1536,
"stored": false,
"vectorSearchProfile": "profile"
}
],
"vectorSearch": {
"profiles": [
{
"name": "profile",
"algorithm": "algorithm"
}
],
"algorithms": [
{
"name": "algorithm",
"kind": "hnsw"
}
]
}
}
```


## Define a skillset for structure-aware chunking and vectorization

The following example shows a skillset definition that projects individual Markdown sections, chunks, and their vector equivalents as fields in the search index. It uses the [Document Layout skill](cognitive-search-skill-document-intelligence-layout) to detect headings and populate a content field based on semantically coherent paragraphs and sentences in the source document. It uses the [Text Split skill](cognitive-search-skill-textsplit) to split the Markdown content into chunks. It uses the [Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding) to vectorize chunks and any other field for which you want embeddings.

Besides skills, the skillset includes `indexProjections`

and `cognitiveServices`

:

`indexProjections`

are used for indexes containing chunked documents. The projections specify how parent-child content is mapped to fields in a search index for one-to-many indexing. For more information, see[Define an index projection](search-how-to-define-index-projections).`cognitiveServices`

[attaches a Microsoft Foundry resource](cognitive-search-attach-cognitive-services)for billing purposes. The Document Layout skill is available through[Standard pricing](https://azure.microsoft.com/pricing/details/ai-document-intelligence/).

```
POST {endpoint}/skillsets?api-version=2025-09-01
{
"name": "my_skillset",
"description": "A skillset for structure-aware chunking and vectorization with an index projection around markdown section",
"skills": [
{
"@odata.type": "#Microsoft.Skills.Util.DocumentIntelligenceLayoutSkill",
"name": "my_document_intelligence_layout_skill",
"context": "/document",
"outputMode": "oneToMany",
"inputs": [
{
"name": "file_data",
"source": "/document/file_data"
}
],
"outputs": [
{
"name": "markdown_document",
"targetName": "markdownDocument"
}
],
"markdownHeaderDepth": "h3"
},
{
"@odata.type": "#Microsoft.Skills.Text.SplitSkill",
"name": "my_markdown_section_split_skill",
"description": "A skill that splits text into chunks",
"context": "/document/markdownDocument/*",
"inputs": [
{
"name": "text",
"source": "/document/markdownDocument/*/content",
"inputs": []
}
],
"outputs": [
{
"name": "textItems",
"targetName": "pages"
}
],
"defaultLanguageCode": "en",
"textSplitMode": "pages",
"maximumPageLength": 2000,
"pageOverlapLength": 500,
"unit": "characters"
},
{
"@odata.type": "#Microsoft.Skills.Text.AzureOpenAIEmbeddingSkill",
"name": "my_azure_openai_embedding_skill",
"context": "/document/markdownDocument/*/pages/*",
"inputs": [
{
"name": "text",
"source": "/document/markdownDocument/*/pages/*",
"inputs": []
}
],
"outputs": [
{
"name": "embedding",
"targetName": "text_vector"
}
],
"resourceUri": "https://<subdomain>.openai.azure.com",
"deploymentId": "text-embedding-3-small",
"apiKey": "<Azure OpenAI api key>",
"modelName": "text-embedding-3-small"
}
],
"cognitiveServices": {
"@odata.type": "#Microsoft.Azure.Search.CognitiveServicesByKey",
"key": "<Cognitive Services api key>"
},
"indexProjections": {
"selectors": [
{
"targetIndexName": "my_consolidated_index",
"parentKeyFieldName": "text_parent_id",
"sourceContext": "/document/markdownDocument/*/pages/*",
"mappings": [
{
"name": "text_vector",
"source": "/document/markdownDocument/*/pages/*/text_vector"
},
{
"name": "chunk",
"source": "/document/markdownDocument/*/pages/*"
},
{
"name": "title",
"source": "/document/title"
},
{
"name": "header_1",
"source": "/document/markdownDocument/*/sections/h1"
},
{
"name": "header_2",
"source": "/document/markdownDocument/*/sections/h2"
},
{
"name": "header_3",
"source": "/document/markdownDocument/*/sections/h3"
}
]
}
],
"parameters": {
"projectionMode": "skipIndexingParentDocuments"
}
}
}
```


## Configure and run the indexer

After you create a data source, index, and skillset, [create and run the indexer](search-howto-create-indexers#run-the-indexer). This step puts the pipeline into execution.

When you use the [Document Layout skill](cognitive-search-skill-document-intelligence-layout), set the following parameters on the indexer definition:

- Set the
`allowSkillsetToReadFileData`

parameter to`true`

. - Set the
`parsingMode`

parameter to`default`

.

You don't need to set `outputFieldMappings`

in this scenario because `indexProjections`

handle the source field to search field associations. Index projections handle field associations for the Document Layout skill and also regular chunking with the split skill for imported and vectorized data workloads. You still need output field mappings for transformations or complex data mappings with functions which apply in other cases. However, for n-chunks per document, index projections handle this functionality natively.

Here's an example of an indexer creation request.

```
POST {endpoint}/indexers?api-version=2025-09-01
{
"name": "my_indexer",
"dataSourceName": "my_blob_datasource",
"targetIndexName": "my_consolidated_index",
"skillsetName": "my_skillset",
"parameters": {
"batchSize": 1,
"configuration": {
"dataToExtract": "contentAndMetadata",
"parsingMode": "default",
"allowSkillsetToReadFileData": true
}
},
"fieldMappings": [
{
"sourceFieldName": "metadata_storage_path",
"targetFieldName": "title"
}
],
"outputFieldMappings": []
}
```


When you send the request to the search service, the indexer runs.

## Verify results

You can query your search index after processing concludes to test your solution.

To check the results, run a query against the index. Use [Search Explorer](search-explorer) as a search client, or any tool that sends HTTP requests. The following query selects fields that contain the output of Markdown section nonvector content and its vector.

For Search Explorer, you can copy just the JSON and paste it into the JSON view for query execution.

```
POST /indexes/[index name]/docs/search?api-version=[api-version]
{
"search": "copay for in-network providers",
"count": true,
"searchMode": "all",
"vectorQueries": [
{
"kind": "text",
"text": "*",
"fields": "text_vector,image_vector"
}
],
"queryType": "semantic",
"semanticConfiguration": "healthplan-doc-layout-test-semantic-configuration",
"captions": "extractive",
"answers": "extractive|count-3",
"select": "header_1, header_2, header_3"
}
```


If you used the health plan PDFs to test this skill, Search Explorer results for the example query should look similar to the results in the following screenshot.

The query is a

[hybrid query](hybrid-search-how-to-query)over text and vectors, so you see a`@search.rerankerScore`

and results are ranked by that score.`searchMode=all`

means that*all*query terms must be considered for a match (the default is*any*).The query uses semantic ranking, so you see

`captions`

. It also has`answers`

, but they aren't shown in the screenshot. The results are the most semantically relevant to the query input, as determined by the[semantic ranker](semantic-search-overview).The

`select`

statement (not shown in the screenshot) specifies the header fields that the Document Layout skill detects and populates. You can add more fields to the select clause to inspect the content of chunks, title, or any other human readable field.


---

<!-- DOCUMENTO FUSIONADO: knowledge-store-projections-examples.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/knowledge-store-projections-examples -->

# Define projections in a knowledge store

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

*Knowledge stores* are secondary storage that exists in Azure Storage and contain the outputs of Azure AI Search skillsets. They're separate from knowledge sources and knowledge bases, which are used in [agentic retrieval](agentic-retrieval-overview) workflows.

[Projections](knowledge-store-projection-overview) are the component of a [knowledge store definition](knowledge-store-concept-intro) that determines how AI enriched content is stored in Azure Storage. Projections determine the type, quantity, and composition of the data structures containing your content.

In this article, learn the syntax for each type of projection:

Recall that projections are defined under the `knowledgeStore`

property of a skillset.

```
"knowledgeStore" : {
"storageConnectionString": "DefaultEndpointsProtocol=https;AccountName=<Acct Name>;AccountKey=<Acct Key>;",
"projections": [
{
"tables": [ ],
"objects": [ ],
"files": [ ]
}
]
}
```


If you need more background before getting started, review [this check list](knowledge-store-projection-overview#checklist-for-getting-started) for tips and workflow.

Tip

When developing projections, [enable enrichment caching (preview)](enrichment-cache-how-to-configure) so that you can reuse existing enrichments while editing projection definitions. Enrichment caching is a preview feature, so be sure to use the preview REST API on the indexer request. Without caching, simple edits to a projection will result in a full reprocess of enriched content. By caching the enrichments, you can iterate over projections without incurring any skillset processing charges.

## Requirements

All projections have source and destination properties. The source is always internal content from an enrichment tree created during skillset execution. The destination is the name and type of an external object that's created and populated in Azure Storage.

Except for file projections, which only accept binary images, the source must be:

- Valid JSON
- A path to a node in the enrichment tree (for example,
`"source": "/document/objectprojection"`

)

While a node might resolve to a single field, a more common representation is a reference to a complex shape. Complex shapes are created through a shaping methodology, either a [Shaper skill](cognitive-search-skill-shaper) or [an inline shaping definition](knowledge-store-projection-shape#inline-shape), but usually a Shaper skill. The fields or elements of the shape determine the fields in containers and tables.

Shaper skills are favored because it outputs JSON, whereas most skills don't output valid JSON on their own. In many cases, the same data shape created by a Shaper skill can be used equally by both table and object projections.

Given source input requirements, knowing how to [shape data](knowledge-store-projection-shape) becomes a practical requirement for projection definition, especially if you're working with tables.

## Define a table projection

Table projections are recommended for scenarios that call for data exploration, such as analysis with Power BI or workloads that consume data frames. The tables section of a projections array is a list of tables that you want to project.

To define a table projection, use the `tables`

array in the projections property. A table projection has three required properties:

| Property | Description |
|---|---|
| tableName | Determines the name of a new table created in Azure Table Storage. |
| generatedKeyName | Column name for the key that uniquely identifies each row. The value is system-generated. If you omit this property, a column is created automatically that uses the table name and "key" as the naming convention. |
| source | A path to a node in an enrichment tree. The node should be a reference to a complex shape that determines which columns are created in the table. |

In table projections, "source" is usually the output of a [Shaper skill](cognitive-search-skill-shaper) that defines the shape of the table. Tables have rows and columns, and shaping is the mechanism by which rows and columns are specified. You can use a [Shaper skill or inline shapes](knowledge-store-projection-shape). The Shaper skill produces valid JSON, but the source could be the output from any skill, if valid JSON.

Note

Table projections are subject to the [storage limits](/en-us/rest/api/storageservices/understanding-the-table-service-data-model) imposed by Azure Storage. The entity size can't exceed 1 MB and a single property can be no bigger than 64 KB. These constraints make tables a good solution for storing a large number of small entities.

### Single table example

The schema of a table is specified partly by the projection (table name and key), and also by the source that provides the shape of table (columns). This example shows just one table so that you can focus on the details of the definition.

```
"projections" : [
{
"tables": [
{ "tableName": "Hotels", "generatedKeyName": "HotelId", "source": "/document/tableprojection" }
]
}
]
```


Columns are derived from the "source". The following data shape containing HotelId, HotelName, Category, and Description will result in creation of those columns in the table.

```
{
"@odata.type": "#Microsoft.Skills.Util.ShaperSkill",
"name": "#3",
"description": null,
"context": "/document",
"inputs": [
{
"name": "HotelId",
"source": "/document/HotelId"
},
{
"name": "HotelName",
"source": "/document/HotelName"
},
{
"name": "Category",
"source": "/document/Category"
},
{
"name": "Description",
"source": "/document/Description"
},
],
"outputs": [
{
"name": "output",
"targetName": "tableprojection"
}
]
}
```


### Multiple table (slicing) example

A common pattern for table projections is to have multiple related tables, where system-generated partitionKey and rowKey columns are created to support cross-table relationships for all tables under the same projection group.

Creating multiple tables can be useful if you want control over how related data is aggregated. If enriched content has unrelated or independent components, for example the keywords extracted from a document might be unrelated from the entities recognized in the same document, you can split out those fields into adjacent tables.

When you're projecting to multiple tables, the complete shape is projected into each table, unless a child node is the source of another table within the same group. Adding a projection with a source path that is a child of an existing projection results in the child node being sliced out of the parent node and projected into the new yet related table. This technique allows you to define a single node in a Shaper skill that can be the source for all of your projections.

The pattern for multiple tables consists of:

- One table as the parent or main table
- Other tables to contain slices of the enriched content

For example, assume a Shaper skill outputs an "EnrichedShape" that contains hotel information, plus enriched content like key phrases, locations, and organizations. The main table would include fields that describe the hotel (ID, name, description, address, category). Key phrases would get the key phrase column. Entities would get the entity columns.

```
"projections" : [
{
"tables": [
{ "tableName": "MainTable", "generatedKeyName": "HotelId", "source": "/document/EnrichedShape" },
{ "tableName": "KeyPhrases", "generatedKeyName": "KeyPhraseId", "source": "/document/EnrichedShape/*/KeyPhrases/*" },
{ "tableName": "Entities", "generatedKeyName": "EntityId", "source": "/document/EnrichedShape/*/Entities/*" }
]
}
]
```


### Naming relationships

The `generatedKeyName`

and `referenceKeyName`

properties are used to relate data across tables or even across projection types. Each row in the child table has a property pointing back to the parent. The name of the column or property in the child is the `referenceKeyName`

from the parent. When the `referenceKeyName`

isn't provided, the service defaults it to the `generatedKeyName`

from the parent.

Power BI relies on these generated keys to discover relationships within the tables. If you need the column in the child table named differently, set the `referenceKeyName`

property on the parent table. One example would be to set the `generatedKeyName`

as ID on the tblDocument table and the `referenceKeyName`

as DocumentID. This would result in the column in the tblEntities and tblKeyPhrases tables containing the document ID being named DocumentID.

## Define an object projection

Object projections are JSON representations of the enrichment tree that can be sourced from any node. In comparison with table projections, object projections are simpler to define and are used when projecting whole documents. Object projections are limited to a single projection in a container and can't be sliced.

To define an object projection, use the `objects`

array in the projections property. An object projection has three required properties:

| Property | Description |
|---|---|
| storageContainer | Determines the name of a new container created in Azure Storage. |
| generatedKeyName | Column name for the key that uniquely identifies each row. The value is system-generated. If you omit this property, a column is created automatically that uses the table name and "key" as the naming convention. |
| source | A path to a node in an enrichment tree that is the root of the projection. The node is usually a reference to a complex data shape that determines blob structure. |

The following example projects individual hotel documents, one hotel document per blob, into a container called `hotels`

.

```
"knowledgeStore": {
"storageConnectionString": "an Azure storage connection string",
"projections" : [
{
"tables": [ ]
},
{
"objects": [
{
"storageContainer": "hotels",
"source": "/document/objectprojection",
}
]
},
{
"files": [ ]
}
]
}
```


The source is the output of a Shaper skill, named `"objectprojection"`

. Each blob has a JSON representation of each field input.

```
{
"@odata.type": "#Microsoft.Skills.Util.ShaperSkill",
"name": "#3",
"description": null,
"context": "/document",
"inputs": [
{
"name": "HotelId",
"source": "/document/HotelId"
},
{
"name": "HotelName",
"source": "/document/HotelName"
},
{
"name": "Category",
"source": "/document/Category"
},
{
"name": "keyPhrases",
"source": "/document/HotelId/keyphrases/*"
},
],
"outputs": [
{
"name": "output",
"targetName": "objectprojection"
}
]
}
```


## Define a file projection

File projections are always binary, normalized images, where normalization refers to potential resizing and rotation for use in skillset execution. File projections, similar to object projections, are created as blobs in Azure Storage, and contain binary data (as opposed to JSON).

To define a file projection, use the `files`

array in the projections property. A files projection has three required properties:

| Property | Description |
|---|---|
| storageContainer | Determines the name of a new container created in Azure Storage. |
| generatedKeyName | Column name for the key that uniquely identifies each row. The value is system-generated. If you omit this property, a column is created automatically that uses the table name and "key" as the naming convention. |
| source | A path to a node in an enrichment tree that is the root of the projection. For images files, the source is always `/document/normalized_images/*` . File projections only act on the `normalized_images` collection. Neither indexers nor a skillset will pass through the original non-normalized image. |

The destination is always a blob container, with a folder prefix of the base64 encoded value of the document ID. If there are multiple images, they're placed together in the same folder. File projections can't share the same container as object projections and need to be projected into a different container.

The following example projects all normalized images extracted from the document node of an enriched document, into a container called `myImages`

.

```
"projections": [
{
"tables": [ ],
"objects": [ ],
"files": [
{
"storageContainer": "myImages",
"source": "/document/normalized_images/*"
}
]
}
]
```


## Test projections

You can process projections by following these steps:

Set the knowledge store's

`storageConnectionString`

property to a valid V2 general purpose storage account connection string.[Update the skillset](/en-us/rest/api/searchservice/skillsets/create-or-update)by issuing a PUT request with your projection definition in the body of the skillset.[Run the indexer](/en-us/rest/api/searchservice/indexers/run)to put the skillset into execution.[Monitor indexer execution](search-monitor-indexers)to check progress and catch any errors.Use Azure portal to verify object creation in Azure Storage.

If you're projecting tables,

[import them into Power BI](knowledge-store-connect-power-bi)for table manipulation and visualization. In most cases, Power BI autodiscovers the relationships among tables.

## Common issues

Omitting any of the following steps can result in unexpected outcomes. Check for the following conditions if your output doesn't look right.

String enrichments aren't shaped into valid JSON. When strings are enriched, for example

`merged_content`

enriched with key phrases, the enriched property is represented as a child of`merged_content`

within the enrichment tree. The default representation isn't well-formed JSON. At projection time, make sure to transform the enrichment into a valid JSON object with a name and a value. Using a Shaper skill or defining inline shapes help resolve this issue.Omission of

`/*`

at the end of a source path. If the source of a projection is`/document/projectionShape/keyPhrases`

, the key phrases array is projected as a single object/row. Instead, set the source path to`/document/projectionShape/keyPhrases/*`

to yield a single row or object for each of the key phrases.Path syntax errors.

[Path selectors](cognitive-search-concept-annotations-syntax)are case-sensitive and can lead to missing input warnings if you don't use the exact case for the selector.

## Next steps

The next step walks you through shaping and projection of output from a rich skillset. If your skillset is complex, the following article provides examples of both shapes and projections.
