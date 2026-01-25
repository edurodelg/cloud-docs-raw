---
merged_at: 2026-01-25T02:11:58.477404
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-agentic-retrieval-concept.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-agentic-retrieval-concept -->

# Agentic retrieval in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

What is agentic retrieval? In Azure AI Search, *agentic retrieval* is a new multi-query pipeline designed for complex questions posed by users or agents in chat and copilot apps. It's intended for [Retrieval Augmented Generation (RAG)](retrieval-augmented-generation-overview) patterns and agent-to-agent workflows.

Here's what it does:

Uses a large language model (LLM) to break down a complex query into smaller, focused subqueries for better coverage over your indexed content. Subqueries can include chat history for extra context.

Runs subqueries in parallel. Each subquery is semantically reranked to promote the most relevant matches.

Combines the best results into a unified response that an LLM can use to generate answers with your proprietary content.

The response is modular yet comprehensive in how it also includes a query plan and source documents. You can choose to use just the search results as grounding data, or invoke the LLM to formulate an answer.


This high-performance pipeline helps you generate high quality grounding data (or an answer) for your chat application, with the ability to answer complex questions quickly.

Programmatically, agentic retrieval is supported through a new [Knowledge Base object](/en-us/rest/api/searchservice/knowledge-bases?view=rest-searchservice-2025-11-01-preview&preserve-view=true) in the 2025-11-01-preview and in Azure SDK preview packages that provide the feature. A knowledge base's retrieval response is designed for downstream consumption by other agents and chat apps.

## Why use agentic retrieval

There are two use cases for agentic retrieval. First, it's the basis of the [Foundry IQ experience](/en-us/azure/ai-foundry/agents/how-to/tools/knowledge-retrieval) in the Microsoft Foundry (new) portal. It provides the knowledge layer for agent solutions in Microsoft Foundry. Second, it's the basis for custom agentic solutions that you create using the Azure AI Search APIs.

You should use agentic retrieval when you want to provide agents and apps with the most relevant content for answering harder questions, leveraging chat context and your proprietary content.

The *agentic* aspect is a reasoning step in query planning processing that's performed by a supported large language model (LLM) that you provide. The LLM analyzes the entire chat thread to identify the underlying information need. Instead of a single, catch-all query, the LLM breaks down compound questions into focused subqueries based on: user questions, chat history, and parameters on the request. The subqueries target your indexed documents (plain text and vectors) in Azure AI Search. This hybrid approach ensures you surface both keyword matches and semantic similarities at once, dramatically improving recall.

The *retrieval* component is the ability to run subqueries simultaneously, merge results, semantically rank results, and return a three-part response that includes grounding data for the next conversation turn, reference data so that you can inspect the source content, and an activity plan that shows query execution steps.

Query expansion and parallel execution, plus the retrieval response, are the key capabilities of agentic retrieval that make it the best choice for generative AI (RAG) applications.

Agentic retrieval adds latency to query processing, but it makes up for it by adding these capabilities:

- Reads in chat history as an input to the retrieval pipeline.
- Deconstructs a complex query that contains multiple "asks" into component parts. For example: "find me a hotel near the beach, with airport transportation, and that's within walking distance of vegetarian restaurants."
- Rewrites an original query into multiple subqueries using synonym maps (optional) and LLM-generated paraphrasing.
- Corrects spelling mistakes.
- Executes all subqueries simultaneously.
- Outputs a unified result as a single string. Alternatively, you can extract parts of the response for your solution. Metadata about query execution and reference data is included in the response.

Agentic retrieval invokes the entire query processing pipeline multiple times for each subquery, but it does so in parallel, preserving the efficiency and performance necessary for a reasonable user experience.

Note

Including an LLM in query planning adds latency to a query pipeline. You can mitigate the effects by using faster models, such as gpt-4o-mini, and summarizing the message threads. You can minimize latency and costs by setting properties that limit LLM processing. You can also exclude LLM processing altogether for just text and hybrid search and your own query planning logic.

## Architecture and workflow

Agentic retrieval is designed for conversational search experiences that use an LLM to intelligently break down complex queries. The system coordinates multiple Azure services to deliver comprehensive search results.

### How it works

The agentic retrieval process works as follows:

**Workflow initiation**: Your application calls a knowledge base with retrieve action that provides a query and conversation history.**Query planning**: A knowledge base sends your query and conversation history to an LLM, which analyzes the context and breaks down complex questions into focused subqueries. This step is automated and not customizable.**Query execution**: The knowledge base sends the subqueries to your knowledge sources. All subqueries run simultaneously and can be keyword, vector, and hybrid search. Each subquery undergoes semantic reranking to find the most relevant matches. References are extracted and retained for citation purposes.**Result synthesis**: The system combines all results into a unified response with three parts: merged content, source references, and execution details.

Your search index determines query execution and any optimizations that occur during query execution. Specifically, if your index includes searchable text and vector fields, a hybrid query executes. If the only searchable field is a vector field, then only pure vector search is used. The index semantic configuration, plus optional scoring profiles, synonym maps, analyzers, and normalizers (if you add filters) are all used during query execution. You must have named defaults for a semantic configuration and a scoring profile.

### Required components

| Component | Service | Role |
|---|---|---|
LLM |
Azure OpenAI | Creates subqueries from conversation context and later uses grounding data for answer generation |
Knowledge base |
Azure AI Search | Orchestrates the pipeline, connecting to your LLM and managing query parameters |
Knowledge source |
Azure AI Search | Wraps the search index with properties pertaining to knowledge base usage |
Search index |
Azure AI Search | Stores your searchable content (text and vectors) with semantic configuration |
Semantic ranker |
Azure AI Search | Required component that reranks results for relevance (L2 reranking) |

### Integration requirements

Your application drives the pipeline by calling the knowledge base and handling the response. The pipeline returns grounding data that you pass to an LLM for answer generation in your conversation interface. For implementation details, see [Tutorial: Build an end-to-end agentic retrieval solution](agentic-retrieval-how-to-create-pipeline).

Note

Only gpt-4o, gpt-4.1, and gpt-5 series models are supported for query planning. You can use any model for final answer generation.

## How to get started

To create an agentic retrieval solution, you can use the Azure portal, the latest preview REST APIs, or a preview Azure SDK package that provides the functionality.

Currently, the portal only supports creating search index and blob knowledge sources. Other types of knowledge sources must be created programmatically.

[Quickstart: Agentic retrieval in the Azure portal](get-started-portal-agentic-retrieval)[Quickstart: Agentic retrieval](search-get-started-agentic-retrieval)(C#, Java, JavaScript, Python, TypeScript, REST)

## Availability and pricing

Agentic retrieval is available in [selected regions](search-region-support). Knowledge sources and knowledge bases also have [maximum limits](search-limits-quotas-capacity#agentic-retrieval-limits) that vary by service tier.

It has a dependency on premium features. If you disable semantic ranker for your search service, you effectively disable agentic retrieval.

| Plan | Description |
|---|---|
| Free | A free tier search service provides 50 million free agentic reasoning tokens per month. On higher tiers, you can choose between the free plan (default) and the standard plan. |
| Standard | The standard plan is pay-as-you-go pricing once the monthly free quota is consumed. After the free quota is used up, you are charged an additional fee for each additional one million agentic reasoning tokens. You aren't notified when the transition occurs. For more information about charges by currency, see the
|

Token-based billing for LLM-based query planning and [answer synthesis](agentic-retrieval-how-to-answer-synthesis) (optional) is pay-as-you-go in Azure OpenAI. It's token based for both input and output tokens. The model you assign to the knowledge base is the one [charged for token usage](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/#pricing). For example, if you use gpt-4o, the token charge appears in the bill for gpt-4o.

Token-based billing for agentic retrieval is the number of tokens returned by each subquery.

| Aspect | Classic single-query pipeline | Agentic retrieval multi-query pipeline |
|---|---|---|
| Unit | Query based (1,000 queries) per unit of currency | Token based (1 million tokens per unit of currency) |
| Cost per unit | Uniform cost per query | Uniform cost per token |
| Cost estimation | Estimate query count | Estimate token usage |
| Free tier | 1,000 free queries | 50 million free tokens |

### Example: Estimate costs

Agentic retrieval has two billing models: billing from Azure OpenAI (query planning and, if enabled, answer synthesis) and billing from Azure AI Search for agentic retrieval.

This pricing example omits answer synthesis, but helps illustrate the estimation process. Your costs could be lower. For the actual price of transactions, see [Azure OpenAI pricing](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/#pricing).

#### Estimated billing costs for query planning

To estimate the query plan costs as pay-as-you-go in Azure OpenAI, let's assume gpt-4o-mini:

- 15 cents for 1 million input tokens.
- 60 cents for 1 million output tokens.
- 2,000 input tokens for average chat conversation size.
- 350 tokens for average output plan size.

#### Estimated billing costs for query execution

To estimate agentic retrieval token counts, start with an idea of what an average document in your index looks like. For example, you might approximate:

- 10,000 chunks, where each chunk is one to two paragraphs of a PDF.
- 500 tokens per chunk.
- Each subquery reranks up to 50 chunks.
- On average, there are three subqueries per query plan.

#### Calculating price of execution

Assume we make 2,000 agentic retrievals with three subqueries per plan. This gives us about 6,000 total queries.

Rerank 50 chunks per subquery, which is 300,000 total chunks.

Average chunk is 500 tokens, so the total tokens for reranking is 150 million.

Given a hypothetical price of 0.022 per token, $3.30 is the total cost for reranking in US dollars.

Moving on to query plan costs: 2,000 input tokens multiplied by 2,000 agentic retrievals equal 4 million input tokens for a total of 60 cents.

Estimate the output costs based on an average of 350 tokens. If we multiply 350 by 2,000 agentic retrievals, we get 700,000 output tokens total for a total of 42 cents.


Putting it all together, you'd pay about $3.30 for agentic retrieval in Azure AI Search, 60 cents for input tokens in Azure OpenAI, and 42 cents for output tokens in Azure OpenAI, for $1.02 for query planning total. The combined cost for the full execution is $4.32.

#### Tips for controlling costs

Review the activity log in the response to find out what queries were issued to which sources and the parameters used. You can reissue those queries against your indexes and use a public tokenizer to estimate tokens and compare to API-reported usage. Precise reconstruction of a query or response isn't guaranteed however. Factors include the type of knowledge source, such as public web data or a remote SharePoint knowledge source that's predicated on a user identity, which can affect query reproduction.

Reduce the number of knowledge sources (indexes); consolidating content can lower fan-out and token volume.

Lower the reasoning effort to reduce LLM usage during query planning and query expansion (iterative search).

Organize content so the most relevant information can be found with fewer sources and documents (For example, curated summaries or tables).


---

<!-- DOCUMENTO FUSIONADO: search-indexer-sensitivity-labels.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-indexer-sensitivity-labels -->

# Use Azure AI Search indexers to ingest Microsoft Purview sensitivity labels and enforce document-level security

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Azure AI Search now supports automatic extraction of [Microsoft Purview sensitivity labels](/en-us/purview/sensitivity-labels) at document-level during indexing, with label-based access control enforced at query time. Available in public preview, this feature enables organizations to align search experiences with existing [information protection policies](/en-us/purview/create-sensitivity-labels) defined in Microsoft Purview.

With sensitivity label indexing, Azure AI Search extracts and stores metadata that describes each document's sensitivity level. It also enforces label-based access control, ensuring that only authorized users can view or retrieve labeled content in search results.

This functionality is available for the following data sources:

[Azure Blob Storage](search-how-to-index-azure-blob-storage)[Azure Data Lake Storage Gen2](search-how-to-index-azure-data-lake-storage)[SharePoint in Microsoft 365 (Preview)](search-how-to-index-sharepoint-online)[Microsoft OneLake](search-how-to-index-onelake-files)

Important

The feature is available in all regions except West US2. Use the [REST API version 2025-11-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true) or a preview SDK to evaluate the feature.

Portal configuration and debug mode for administrators aren't supported at this time.

### Policy enforcement

At query time, Azure AI Search evaluates sensitivity labels and enforces [document-level access control](search-document-level-access-overview) in accordance with the user's Microsoft Entra ID token and Purview label policies.

Only users authorized to access content with [READ usage right](/en-us/purview/rights-management-usage-rights) under a given label can retrieve corresponding documents in search results. There's a delay in how often the labels are pulled from a document after changed.

When configured [on a schedule](search-howto-schedule-indexers), the indexer pulls new documents and updates from the data source. It captures:

- Newly added documents and their associated sensitivity labels
- Changes in document content
- Updates to sensitivity labels on existing documents

These updates are detected if they occurred since the last indexer run.

## Prerequisites

[Microsoft Purview sensitivity label policies](/en-us/purview/create-sensitivity-labels)must be configured and[applied to documents](/en-us/purview/sensitivity-labels)before indexing.[Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator)or[Privileged Role Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#privileged-role-administrator)roles in your Microsoft Entra tenant are required to grant the search service access to Purview APIs and sensitivity labels.Both the Azure AI Search service and end users querying the content must belong to the same Microsoft Entra tenant. Guest users and multitenant scenarios aren't supported.

File types must be included in the

[Purview sensitivity labels supported formats list](/en-us/purview/sensitivity-labels-sharepoint-onedrive-files#supported-file-types)and also be recognized as[Office supported file types](search-how-to-index-azure-blob-storage#supported-document-formats)by Azure AI Search indexers.

## Limitations

There's a known issue with document deletion and sensitivity labels. When sensitivity labels are enabled for an index, the indexer fails to enumerate the index’s documents. As a result, soft delete operations don't run because the indexer can't list the documents that need to be removed. This applies to indexers that support soft delete, including Azure Blob, ADLS Gen2, OneLake, SharePoint.

Initial release supports REST API version 2025-11-01-preview and associated beta SDK only. There's no portal experience for configuration or management.

This feature isn't supported when used simultaneously with

[ACL-based security filters](search-query-access-control-rbac-enforcement)(currently also in preview). Test each feature independently until Microsoft announces official coexistence support.[Autocomplete](/en-us/rest/api/searchservice/documents/autocomplete-post)and[Suggest](/en-us/rest/api/searchservice/documents/suggest-post)APIs are disabled for Purview-enabled indexes, as they can't yet enforce label-based access control.Guest accounts and cross-tenant queries aren't supported.

In the initial release, sensitivity label-enabled indexes don't support unlabeled documents and don't return them in query results. This capability will be documented when available.

The following indexer features don't support documents with sensitivity labels. If you use any of these features in a skillset or indexer, they don't process those documents.

- Custom Web API skill
- GenAI Prompt skill
- Knowledge store
- Indexer enrichment cache
- Debug sessions


The following steps must be followed in order to configure sensitivity label synchronization in Azure AI Search.

## 1. Enable AI Search managed identity

Enable a [system-assigned managed identity for your Azure AI Search service](search-how-to-managed-identities). This identity is required for the indexer to securely access Microsoft Purview and extract label metadata.

## 2. Enable RBAC on your AI Search service

[Enable a role-based access control (RBAC)](search-security-enable-roles) on your Azure AI Search service. This step is required so content-related operations such as indexing content and query the index succeed. Keep both RBAC and API keys to avoid disrupting operations that rely on API keys.

## 3. Granting access to extract sensitivity labels

Accessing Microsoft Purview sensitivity label metadata involves highly privileged operations, including reading encrypted content and security classifications. To enable this capability in Azure AI Search, you must grant specific roles to the service's managed identity—following your organization's internal governance and approval processes.

### Identify your Global or Privileged Role Administrators

If you need to determine who can authorize permissions for the search service, you can locate active or eligible Global Administrators in your Microsoft Entra tenant.

In the

[Azure portal](https://portal.azure.com), search for**Microsoft Entra ID**.In the left navigation pane, select

**Manage > Roles and administrators**.Search for the

**Global Administrator**or**Privileged Role Administrator**role and select it.Under

**Eligible assignments**and**Active assignments**, review the list of administrators authorized to run the permissions setup process.

### Secure Governance Approval

Engage your internal security or compliance teams to review the request. Microsoft recommends following your company's standard governance and security review process before proceeding with any role assignments.

Once approved, a Global Administrator or Privileged Role Administrator must assign the following roles to the Azure AI Search system-assigned managed identity:

**Content.SuperUser**– for label and content extraction**UnifiedPolicy.Tenant.Read**– for Purview policy and label metadata access

### Assign Roles via PowerShell

Your Global Administrator or Privileged Role Administrator should use the following PowerShell script to grant the required permissions. Replace the placeholder values with your actual subscription, resource group, and search service names.

```
Install-Module -Name Az -Scope CurrentUser
Install-Module -Name Microsoft.Entra -AllowClobber
Import-Module Az.Resources
Connect-Entra -Scopes 'Application.ReadWrite.All'
$resourceIdWithManagedIdentity = "subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.Search/searchServices/<searchServiceName>"
$managedIdentityObjectId = (Get-AzResource -ResourceId $resourceIdWithManagedIdentity).Identity.PrincipalId
# Microsoft Information Protection (MIP)
$MIPResourceSP = Get-EntraServicePrincipal -Filter "appID eq '870c4f2e-85b6-4d43-bdda-6ed9a579b725'"
New-EntraServicePrincipalAppRoleAssignment -ServicePrincipalId $managedIdentityObjectId -Principal $managedIdentityObjectId -ResourceId $MIPResourceSP.Id -Id "8b2071cd-015a-4025-8052-1c0dba2d3f64"
# ARM Service Principal for policy read
$ARMSResourceSP = Get-EntraServicePrincipal -Filter "appID eq '00000012-0000-0000-c000-000000000000'"
New-EntraServicePrincipalAppRoleAssignment -ServicePrincipalId $managedIdentityObjectId -Principal $managedIdentityObjectId -ResourceId $ARMSResourceSP.Id -Id "7347eb49-7a1a-43c5-8eac-a5cd1d1c7cf0"
```


The appID roles in the provided PowerShell script are associated to the following Azure roles:

| AppID | Service Principal |
|---|---|
`870c4f2e-85b6-4d43-bdda-6ed9a579b725` |
Microsoft Info Protection Sync Service |
`00000012-0000-0000-c000-000000000000` |
Azure Resource Manager |

## 4. Configure the index to enable Purview sensitivity label

When sensitivity label support is required, set the purviewEnabled property to true in your [index definition](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true).

Important

**purviewEnabled** property must be set to true when the index is created. This setting is permanent and can't be modified later.
When **purviewEnabled** is set to true, only RBAC authentication is supported for all document operations APIs.
API key access is limited to index schema retrieval (list and get).

```
PUT https://{service}.search.windows.net/indexes('{indexName}')?api-version=2025-11-01-preview
{
"purviewEnabled": true,
"fields": [
{
"name": "sensitivityLabel",
"type": "Edm.String",
"filterable": true,
"sensitivityLabel": true,
"retrievable": true
}
]
}
```


## 5. Configure the data source

To enable sensitivity label ingestion, configure the [data source](/en-us/rest/api/searchservice/data-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) with the indexerPermissionOptions property set to ["sensitivityLabel"].

```
{
"name": "purview-sensitivity-datasource",
"type": "azureblob", // < adjust type value according to the data source you are enabling this for: sharepoint, onelake, adlsgen2.
"indexerPermissionOptions": [ "sensitivityLabel" ],
"credentials": {
"connectionString": <your-connection-string>;"
},
"container": {
"name": "<container-name>"
}
}
```


The `indexerPermissionOptions`

property instructs the indexer to extract sensitivity label metadata during ingestion and attach it to the indexed document.

## 6. Configure index projections in your skillset (if applicable)

If your indexer has a [skillset](cognitive-search-working-with-skillsets) and you're implementing data chunking through [split skill](cognitive-search-skill-textsplit), for example, if you have integrated vectorization, you must ensure you also map the sensitivity label to each chunk via [index projections in the skillset](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true).

```
PUT https://{service}.search.windows.net/skillsets/{skillset}?api-version=2025-11-01-preview
{
"name": "my-skillset",
"skills": [
{
"@odata.type": "#Microsoft.Skills.Text.SplitSkill",
"name": "#split",
"context": "/document",
"inputs": [{ "name": "text", "source": "/document/content" }],
"outputs": [{ "name": "textItems", "targetName": "chunks" }]
}
// ... (other skills such as embeddings, entity recognition, etc.)
],
"indexProjections": {
"selectors": [
{
"targetIndexName": "chunks-index",
"parentKeyFieldName": "parentId", // must exist in target index
"sourceContext": "/document/chunks/*", // match your split output path
"mappings": [
{ "name": "chunkId", "source": "/document/chunks/*/id" }, // if you create an id per chunk
{ "name": "content", "source": "/document/chunks/*/text" }, // chunk text
{ "name": "parentId", "source": "/document/id" }, // parent doc id
{ "name": "sensitivityLabel", "source": "/document/metadata_sensitivity_label" } // <-- parent → child
]
}
],
"parameters": {
"projectionMode": "skipIndexingParentDocuments"
}
}
}
```


## 7. Configure the indexer

- Define field mappings in your
[indexer definition](/en-us/rest/api/searchservice/indexers/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)to route extracted label metadata to the index fields. If your data source emits label metadata under a different field name (for example, metadata_sensitivity_label), map it explicitly.

```
{
"fieldMappings": [
{
"sourceFieldName": "metadata_sensitivity_label",
"targetFieldName": "sensitivityLabel"
}
]
}
```


- Sensitivity label updates are indexed automatically when changes to a document's label, content, or metadata are detected during a scheduled indexer run.
[Configure the indexer on a recurring schedule](search-howto-schedule-indexers). The minimum supported interval is every 5 minutes.
