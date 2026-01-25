---
source_url: https://learn.microsoft.com/en-us/azure/search/search-import-data-portal
fetched_at: 2026-01-25T03:12:27.843744
---

# Import data wizards in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

We're consolidating the Azure AI Search wizards. Key changes include:

- The
**Import and vectorize data**wizard is now called**Import data (new)**. - The
**Import data**workflow is now available in**Import data (new)**.

The **Import data** wizard will eventually be deprecated. For now, you can still use this wizard, but we recommend the new wizard for an improved search experience that uses the latest frameworks.

The wizards don't have identical keyword search workflows. Certain skills and capabilities are only available in the old wizard. For more information about their similarities and differences, continue reading this article.

Azure AI Search has two wizards that automate indexing, enrichment, and object creation for various search scenarios:

The

**Import data**wizard supports keyword (nonvector) search. You can extract text and numbers from raw documents. You can also configure applied AI and built-in skills to infer structure and generate searchable text from image files and unstructured data.The

**Import data (new)**wizard supports keyword search, RAG, and multimodal RAG. For keyword search, it modernizes the**Import data**workflow but lacks some functionality, such as automatic metadata field creation. For RAG and multimodal RAG, it connects to your embedding model deployment, sends requests, and generates vectors from text or images.

Despite their differences, the wizards follow similar workflows for content ingestion and indexing. The following table summarizes their capabilities.

| Capability | Import data wizard | Import data (new) wizard |
|---|---|---|
| Index creation | ✅ | ✅ |
| Indexer pipeline creation | ✅ | ✅ |
| Azure Logic Apps connectors | ❌ | ✅ |
| Built-in sample data | ❌ | ❌ |
| Skills-based enrichment | ✅ | ✅ |
| Vector and multimodal support | ❌ | ✅ |
| Semantic ranking support | ❌ | ✅ |
| Knowledge store support | ✅ | ❌ |

Built-in sample data for the hotels sample index is no longer provided, but you can create an identical index by following the [Quickstart: Create an index for keyword search](search-get-started-portal).

This article explains how the wizards work to help you with proof-of-concept testing. For step-by-step instructions, see [Try the wizards](#try-the-wizards).

## Supported data sources and scenarios

This section describes the available options in each wizard.

### Data sources

The wizards support the following data sources, most of which use [built-in indexers](search-indexer-overview#supported-data-sources). Exceptions are noted in the table's footnotes.

| Data source | Import data wizard | Import data (new) wizard |
|---|---|---|
|

[Azure Blob Storage](search-how-to-index-azure-blob-storage)[Azure File Storage](search-how-to-index-logic-apps#supported-connectors)1, 2[Azure Queues](search-how-to-index-logic-apps#supported-connectors)1[Azure Table Storage](search-how-to-index-azure-tables)[Azure SQL Database and Managed Instance](search-how-to-index-sql-database)[Cosmos DB for NoSQL](search-how-to-index-cosmosdb-sql)[Cosmos DB for MongoDB](search-how-to-index-cosmosdb-mongodb)[Cosmos DB for Apache Gremlin](search-how-to-index-cosmosdb-gremlin)[MySQL](search-how-to-index-mysql)[OneDrive](search-how-to-index-logic-apps#supported-connectors)1[OneDrive for Business](search-how-to-index-logic-apps#supported-connectors)1[OneLake](search-how-to-index-onelake-files)[Service Bus](search-how-to-index-logic-apps#supported-connectors)1[SharePoint](search-how-to-index-logic-apps#supported-connectors)1, 2[SQL Server on virtual machines](search-how-to-index-sql-server)1 This data source uses an [Azure Logic Apps connector (preview)](search-how-to-index-logic-apps#supported-connectors) instead of a built-in indexer.

2 Instead of using a Logic Apps connector, you can use the Search Service REST APIs to programmatically index data from [Azure File Storage](search-file-storage-integration) or [SharePoint](search-how-to-index-sharepoint-online).

### Skills

Each wizard generates a skillset and outputs field mappings based on options you select. After the skillset is created, you can modify its JSON definition to add or remove skills.

The following skills might appear in a wizard-generated skillset.

| Skill | Import data wizard | Import data (new) wizard |
|---|---|---|
|

1[Azure OpenAI embedding](cognitive-search-skill-azure-openai-embedding)1[Azure Machine Learning (Microsoft Foundry model catalog)](cognitive-search-aml-skill)1[Document layout](cognitive-search-skill-document-intelligence-layout)1[Entity recognition](cognitive-search-skill-entity-recognition-v3)[Image analysis](cognitive-search-skill-image-analysis)2[Key phrase extraction](cognitive-search-skill-keyphrases)[Language detection](cognitive-search-skill-language-detection)[Text translation](cognitive-search-skill-text-translation)[OCR](cognitive-search-skill-ocr)2[PII detection](cognitive-search-skill-pii-detection)[Sentiment analysis](cognitive-search-skill-sentiment)[Shaper](cognitive-search-skill-shaper)3[Text Split](cognitive-search-skill-textsplit)4[Text Merge](cognitive-search-skill-textmerger)41 This skill is available for RAG and multimodal RAG workflows only. Keyword search isn't supported.

2 This skill is available for Azure Storage blobs and Microsoft OneLake files, assuming the default parsing mode. Images can be an image content type (such as PNG or JPG) or an embedded image in an application file (such as PDF).

3 This skill is added when you configure a knowledge store.

4 This skill is added for data chunking when you choose an embedding model. For nonembedding skills, it's added when you set the source field granularity to pages or sentences.

### Semantic ranker

You can [configure semantic ranking](semantic-how-to-configure) to improve the relevance of search results.

| Capability | Import data wizard | Import data (new) wizard |
|---|---|---|
| Semantic ranker | ❌ | ✅ |

### Knowledge store

You can [generate a knowledge store](knowledge-store-create-portal) for secondary storage of enriched (skills-generated) content. A knowledge store is useful for information retrieval workflows that don't require a search engine.

| Capability | Import data wizard | Import data (new) wizard |
|---|---|---|
| Knowledge store | ✅ | ❌ |

## What the wizards create

The following table lists the objects created by the wizards. After the objects are created, you can review their JSON definitions in the Azure portal or call them from code.

| Object | Description |
|---|---|
|

[Data source](/en-us/rest/api/searchservice/data-sources/create)[supported data source](search-indexer-overview#supported-data-sources)on Azure. A data source object is used exclusively with indexers.[Index](/en-us/rest/api/searchservice/indexes/create)[Skillset](/en-us/rest/api/searchservice/skillsets/create)[Knowledge store](knowledge-store-concept-intro)**Import data**wizard.To view these objects after the wizards run:

- Sign in to the
[Azure portal](https://portal.azure.com)and select your search service. - From the left pane, select
**Search management**to find pages for indexes, indexers, data sources, and skillsets.

## Benefits

Before you write any code, you can use the wizards for prototyping and proof-of-concept testing. The wizards connect to external data sources, sample the data to create an initial index, and then import and optionally vectorize the data as JSON documents into an index on Azure AI Search.

If you're evaluating skillsets, the wizards handle output field mappings and add helper functions to create usable objects. [Text Split](cognitive-search-skill-textsplit) is added when you specify a parsing mode. [Text Merge](cognitive-search-skill-textmerger) is added when you choose image analysis so that the wizards can reunite text descriptions with image content. [Shaper](cognitive-search-skill-shaper) is added to support valid projections when you choose the knowledge store option. All of these tasks come with a learning curve. If you're new to enrichment, having these steps handled for you allows you to measure the value of a skill without investing much time and effort.

Sampling is the process by which an index schema is inferred, which has some limitations. When the data source is created, the wizards pick a random sample of documents to decide what columns are part of the data source. Not all files are read, as doing so could potentially take hours for large data sources. Given a selection of documents, source metadata (such as field name or type) is used to create a fields collection in an index schema. Based on the complexity of the source data, you might need to edit the initial schema for accuracy or extend it for completeness. You can make your changes inline on the index definition page.

Overall, the advantages of the wizards are clear: as long as requirements are met, you can create a queryable index within minutes. The wizards handle some of the complexities of indexing, such as serializing data as JSON documents.

## Limitations

The wizards have the following limitations:

The wizards don't support iteration or reuse. Each pass through the wizards creates an index, skillset, and indexer configuration. You can reuse data sources only in the

**Import data**wizard. After you finish the wizards, you can edit the created objects by using other portal tools, the REST APIs, or the Azure SDKs.Source content must reside in a

[supported data source](search-indexer-overview#supported-data-sources).Sampling occurs over a subset of source data. For large data sources, it's possible for the wizards to miss fields. If sampling is insufficient, you might need to extend the schema or correct the inferred data types.

[AI enrichment](cognitive-search-concept-intro), as exposed in the Azure portal, is limited to a subset of built-in skills.A

[knowledge store](knowledge-store-concept-intro), which is only available through the**Import data**wizard, is limited to a few default projections and uses a default naming convention. To customize projections and names, you must create the knowledge store through the REST APIs or Azure SDKs.

## Secure connections

The wizards use the Azure portal controller and public endpoints to make outbound connections. You can't use the wizards if Azure resources are accessed over a private connection or through a shared private link.

You can use the wizards over restricted public connections, but not all functionality is available.

On supported Azure data sources protected by firewalls, you can retrieve data if you have the right firewall rules in place.

The Azure resource must admit network requests from the IP address of the device used on the connection. You should also list Azure AI Search as a trusted service on the resource's network configuration. For example, in Azure Storage, you can list

`Microsoft.Search/searchServices`

as a trusted service.On connections to a Foundry resource for AI enrichment, or on connections to embedding models deployed in the

[Foundry portal](https://ai.azure.com/?cid=learnDocs)or Azure OpenAI, public internet access must be enabled unless your search service meets the creation date, tier, and region requirements for private connections. For more information, see[Make outbound connections through a shared private link](search-indexer-howto-access-private).For AI enrichment, connections to Foundry resources are for

[billing purposes](cognitive-search-attach-cognitive-services). You're billed when API calls for built-in skills (in the**Import data**wizard or the keyword search workflow in the**Import data (new)**wizard) and integrated vectorization (in the**Import data (new)**wizard) exceed the free transaction count (20 per indexer run).If Azure AI Search can't connect:

In the

**Import data (new)**wizard, the error is`"Access denied due to Virtual Network/Firewall rules."`

.In the

**Import data**wizard, there's no error, but the skillset won't be created.


If firewall settings prevent your wizard workflows from succeeding, consider scripted or programmatic approaches instead.

## Workflow

Both wizards follow a similar high-level workflow:

Connect to a supported Azure data source.

(Optional) Add skills to extract or generate content and structure.

Create an index schema, inferred by sampling source data.

Run the wizard to create objects, optionally vectorize data, load data into an index, set a schedule, and configure other options.


The workflow is a one-way pipeline. You can't use the wizard to edit any of the objects that were created, but you can use other portal tools, such as the index designer, indexer designer, or JSON editors, to make allowed updates.

### Starting the wizards

To start the wizards:

Sign in to the

[Azure portal](https://portal.azure.com)and select your search service.On the

**Overview**page, select**Import data**or**Import data (new)**.The wizards open fully expanded in the browser window, giving you more room to work.

Follow the remaining steps to create the index, indexer, and other applicable objects.


You can also launch **Import data** from other Azure services, including Azure Cosmos DB, Azure SQL Database, SQL Managed Instance, and Azure Blob Storage. Look for **Add Azure AI Search** in the left pane on the service overview page.

### Data source configuration in the wizard

The wizards connect to an external [supported data source](search-indexer-overview#supported-data-sources) using the internal logic provided by indexers, which are equipped to sample the source, read metadata, crack documents to read content and structure, and serialize contents as JSON for subsequent import to Azure AI Search.

In the **Import data** wizard, you can paste a connection to a supported data source in a different subscription or region, but the **Choose an existing connection** picker is scoped to the active subscription.


Not all preview data sources are guaranteed to be available in the wizards. Because each data source has the potential to introduce changes downstream, a preview data source is only added when it fully supports all of the wizard's experiences, such as skillset definition and index schema inference.

You can only import from a single table, database view, or equivalent data structure. However, the structure can include hierarchical or nested substructures. For more information, see [How to model complex types](search-howto-complex-data-types).

### Skillset configuration in the wizard

Skillset configuration occurs after the data source definition because the type of data source informs the availability of certain built-in skills. For example, if you're indexing files from Azure Blob Storage, the parsing mode you choose for those files determines whether sentiment analysis is available.

The wizards add not only skills you choose but also skills that are necessary for a successful outcome. For example, if you specify a knowledge store in the **Import data** wizard, the wizard adds a Shaper skill to support projections or physical data structures.

Skillsets are optional, and there's a button at the bottom of the page to skip ahead if you don't want AI enrichment.

### Index schema configuration in the wizard

The wizards sample your data source to detect the fields and field types. Depending on the data source, they might also offer fields for indexing metadata.

Because sampling is an imprecise exercise, review the index for the following considerations:

Is the field list accurate? If your data source contains fields that weren't picked up in sampling, you can manually add the missed fields. You can also remove fields that don't add value to the search experience or won't be used in a

[filter expression](search-query-odata-filter)or[scoring profile](index-add-scoring-profiles).Is the data type appropriate for the incoming data? Azure AI Search supports the

[entity data model (EDM) data types](/en-us/rest/api/searchservice/supported-data-types). For Azure SQL data, there's a[mapping chart](search-how-to-index-sql-database#TypeMapping)that lays out equivalent values. For more information, see[Field mappings and transformations](search-indexer-field-mappings).Do you have one field that can serve as the

*key*? This field must be an Edm.String that uniquely identifies a document. For relational data, it might be mapped to a primary key. For blobs, it might be the`metadata-storage-path`

. If field values include spaces or dashes, you must set the**Base-64 Encode Key**option in the**Create an indexer**step, under**Advanced options**, to suppress the validation check for these characters.Set attributes to determine how that field is used in an index.

Take your time with this step because attributes determine the physical expression of fields in the index. If you want to change attributes later, even programmatically, you almost always need to drop and rebuild the index. Core attributes like

**Searchable**and**Retrievable**have a[negligible effect on storage](search-what-is-an-index#index-size). Enabling filters and using suggesters increase storage requirements.**Searchable**enables full-text search. Every field used in free-form queries or in query expressions must have this attribute. Inverted indexes are created for each field that you mark as**Searchable**.**Retrievable**returns the field in search results. Every field that provides content to search results must have this attribute. Setting this field doesn't appreciably affect index size.**Filterable**allows the field to be referenced in filter expressions. Every field used in a**$filter**expression must have this attribute. Filter expressions are for exact matches. Because text strings remain intact, more storage is required to accommodate the verbatim content.**Facetable**enables the field for faceted navigation. Only fields also marked as**Filterable**can be marked as**Facetable**.**Sortable**allows the field to be used in a sort. Every field used in an**$Orderby**expression must have this attribute.

Do you need

[lexical analysis](search-lucene-query-architecture#stage-2-lexical-analysis)? For Edm.String fields that are**Searchable**, you can set an**Analyzer**if you want language-enhanced indexing and querying.The default is

*Standard Lucene*, but you can choose*Microsoft English*if you wanted to use Microsoft's analyzer for advanced lexical processing, such as resolving irregular noun and verb forms. Only language analyzers can be specified in the Azure portal. If you want to use a custom analyzer or non-language analyzer, such as Keyword or Pattern, you must create it programmatically. For more information, see[Add language analyzers](search-language-support).Do you need typeahead functionality in the form of autocomplete or suggested results? Select the

**Suggester**checkbox to enable[typeahead query suggestions and autocomplete](index-add-suggesters)on selected fields. Suggesters add to the number of tokenized terms in your index and thus consume more storage.

### Indexer configuration in the wizard

The last page of the wizard collects user inputs for indexer configuration. You can [specify a schedule](search-howto-schedule-indexers) and set other options that vary by the data source type.

Internally, the wizard sets up the following definitions, which aren't visible in the indexer until after it's created.

[Field mappings](search-indexer-field-mappings)between the data source and index.[Output field mappings](cognitive-search-output-field-mapping)between the skill output and an index.

## Try the wizards

The best way to understand the benefits and limitations of the wizards is to step through them. The following quickstarts are based on the wizards.