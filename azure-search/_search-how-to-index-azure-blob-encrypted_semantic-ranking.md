---
merged_at: 2026-01-25T03:18:14.040334
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-azure-blob-encrypted.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-azure-blob-encrypted -->

# Tutorial: Index and enrich encrypted blobs for full-text search in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to use [Azure AI Search](search-what-is-azure-search) to index documents that were encrypted with a customer-managed key in [Azure Blob Storage](/en-us/azure/storage/blobs/storage-blobs-introduction).

Normally, an indexer can't extract content from blobs that were encrypted using [client-side encryption](/en-us/azure/storage/blobs/client-side-encryption) in the Azure Blob Storage client library. This is because the indexer doesn't have access to the customer-managed encryption key in [Azure Key Vault](/en-us/azure/key-vault/general/overview). However, using the [DecryptBlobFile custom skill](https://github.com/Azure-Samples/azure-search-power-skills/blob/main/Utils/DecryptBlobFile) and the [Document Extraction skill](cognitive-search-skill-document-extraction), you can provide controlled access to the key to decrypt the files and then extract content from them. This unlocks the ability to index and enrich these documents without compromising the encryption status of your stored documents.

Starting with previously encrypted whole documents (unstructured text) such as PDF, HTML, DOCX, and PPTX in Azure Blob Storage, this tutorial uses a REST client and the Search REST APIs to:

- Define a pipeline that decrypts the documents and extracts text from them
- Define an index to store the output
- Execute the pipeline to create and load the index
- Explore results using full-text search and a rich query syntax

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Azure AI Search](search-create-service-portal)on any tier or region.[Azure Storage](https://azure.microsoft.com/services/storage/), Standard performance (general-purpose v2).Blobs encrypted with a customer-managed key. To create sample data, see

[Tutorial: Encrypt and decrypt blobs using Azure Key Vault](/en-us/azure/storage/blobs/storage-encrypt-decrypt-blobs-key-vault).[Azure Key Vault](https://azure.microsoft.com/services/key-vault/)in the same subscription as Azure AI Search. The key vault must have**soft-delete**and**purge protection**enabled.

Custom skill deployment creates an Azure Function app and an Azure Storage account. These resources are created for you, so they aren't listed as a prerequisite. When you finish this tutorial, remember to clean up the resources so that you aren't billed for services you're not using.

Note

Skillsets often require [attaching a Microsoft Foundry resource](cognitive-search-attach-cognitive-services). As written, this skillset has no dependency on Foundry, so no key is required. If you later add enrichments that invoke built-in skills, remember to update your skillset accordingly.

## Deploy the custom skill

This tutorial uses the sample [DecryptBlobFile](https://github.com/Azure-Samples/azure-search-power-skills/blob/main/Utils/DecryptBlobFile) project from the [Azure Search Power Skills](https://github.com/Azure-Samples/azure-search-power-skills) GitHub repository. In this section, you deploy the skill to an Azure Function so that it can be used in a skillset. A built-in deployment script creates an Azure Function resource with a **psdbf-function-app-** prefix and loads the skill. You're prompted to provide a subscription and resource group. Be sure to choose the subscription that contains your Azure Key Vault instance.

Operationally, the DecryptBlobFile skill takes the URL and SAS token for each blob as inputs. It outputs the downloaded, decrypted file using the file reference contract that Azure AI Search expects. Recall that DecryptBlobFile needs the encryption key to perform the decryption. As part of setup, you also create an access policy that grants DecryptBlobFile function access to the encryption key in Azure Key Vault.

On the

[DecryptBlobFile landing page](https://github.com/Azure-Samples/azure-search-power-skills/blob/main/Utils/DecryptBlobFile#deployment), select**Deploy to Azure**to open the Resource Manager template in the Azure portal.Choose the subscription where your Azure Key Vault instance exists. This tutorial doesn't work if you choose a different subscription.

Select an existing resource group or create a new one. A dedicated resource group makes cleanup easier later.

Select

**Review + create**, agree to the terms, and then select**Create**to deploy the Azure Function.Wait for the deployment to finish.


You should have an Azure Function app that contains the decryption logic and an Azure Storage resource that will store application data. In the next steps, you give the app permissions to access the key vault and collect information that you'll need for the REST calls.

## Grant permissions in Azure Key Vault

Go to your Azure Key Vault service in the Azure portal.

[Create an access policy](/en-us/azure/key-vault/general/assign-access-policy-portal)in the Azure Key Vault that grants key access to the custom skill.From the left pane, select

**Access policies**, and then select**+ Create**to start the**Create an access policy**wizard.On the

**Permissions**page, under**Configure from template**, select**Azure Data Lake Storage or Azure Storage**.Select

**Next**.On the

**Principal**page, select the Azure Function instance you deployed. You can search for it using its resource prefix, which has a default value of**psdbf-function-app**.Select

**Next**.On

**Review + create**, select**Create**.

## Collect app information

Go to the

**psdbf-function-app**function in the Azure portal. Make a note of the following properties you'll need for the REST calls.Get the function URL, which can be found under

**Essentials**on the main page for the function.Get the host key code, which can be found by going to

**App keys**and showing the**default**key, and copying the value.

## Get an admin key and URL for Azure AI Search

Sign in to the

[Azure portal](https://portal.azure.com).On your search service

**Overview**page, get the name of your search service. You can confirm your service name by reviewing the endpoint URL. For example, if your endpoint URL is`https://mydemo.search.windows.net`

, your service name is`mydemo`

.In

**Settings**>**Keys**, get an admin key for full rights on the service. There are two interchangeable admin keys, provided for business continuity in case you need to roll one over. You can use either key on requests to add, modify, or delete objects.

An API key is required in the header of every request sent to your service. A valid key establishes trust, on a per-request basis, between the application sending the request and the service that handles it.

## Set up a REST client

Create the following variables for endpoints and keys.

| Variable | Where to get it |
|---|---|
`admin-key` |
On the Keys page of the Azure AI Search service. |
`search-service-name` |
The name of the Azure AI Search service. The URL is `https://{{search-service-name}}.search.windows.net` . |
`storage-connection-string` |
In the storage account, on the Access Keys tab, select key1 > Connection string. |
`storage-container-name` |
The name of the blob container that has the encrypted files to be indexed. |
`function-uri` |
In the Azure Function, under Essentials on the main page. |
`function-code` |
In the Azure Function, by going to App keys, showing the default key, and copying the value. |
`api-version` |
Leave as 2020-06-30. |
`datasource-name` |
Leave as encrypted-blobs-ds. |
`index-name` |
Leave as encrypted-blobs-idx. |
`skillset-name` |
Leave as encrypted-blobs-ss. |
`indexer-name` |
Leave as encrypted-blobs-ixr. |

## Review and run each request

Use the following HTTP requests to create the objects of an enrichment pipeline.

**PUT request to create the index**: This search index holds the data that Azure AI Search uses and returns.**POST request to create the data source**: This data source specifies the connection to your storage account containing the encrypted blob files.**PUT request to create the skillset**: The skillset specifies the custom skill definition for the Azure Function that will decrypt the blob file data. It also specifies a[DocumentExtractionSkill](cognitive-search-skill-document-extraction)to extract the text from each document after it's decrypted.**PUT request to create the indexer**: Running the indexer retrieves the blobs, applies the skillset, and indexes and stores the results. You must run this request last. The custom skill in the skillset invokes the decryption logic.

## Monitor indexing

Indexing and enrichment commence as soon as you submit the Create Indexer request. Depending on how many documents are in your storage account, indexing can take a while. To find out whether the indexer is still running, send a **Get Indexer Status** request and review the response to learn whether the indexer is running or view error and warning information.

If you're using the Free tier, expect the following message: `"Could not extract content or metadata from your document. Truncated extracted text to '32768' characters"`

. This message appears because blob indexing on the Free tier has a [32,000 limit on character extraction](search-limits-quotas-capacity#indexer-limits). You don't see this message for this data set on higher tiers.

## Search your content

After indexer execution is finished, you can run queries to verify that the data is successfully decrypted and indexed. Go to your Azure AI Search service in the Azure portal and use the [Search Explorer](search-explorer) to run queries over the indexed data.

## Clean up resources

When you're working in your own subscription, at the end of a project, it's a good idea to remove the resources that you no longer need. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

You can find and manage resources in the Azure portal, using the All resources or Resource groups link in the left-navigation pane.

## Next steps

Now that you've indexed encrypted files, you can [iterate on this pipeline by adding more skills](cognitive-search-defining-skillset) to enrich and gain more insights into your data.

If you're working with doubly encrypted data, you might want to investigate the index encryption features available in Azure AI Search. Although the indexer needs decrypted data for indexing purposes, once the index exists, it can be encrypted in a search index using a customer-managed key. This ensures that your data is always encrypted when at rest. For more information, see [Configure customer-managed keys for data encryption in Azure AI Search](search-security-manage-encryption-keys).


---

<!-- DOCUMENTO FUSIONADO: semantic-ranking.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/semantic-ranking -->

# Semantic ranking in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, *semantic ranker* is a feature that measurably improves search relevance by using Microsoft's language understanding models to rerank search results. Semantic ranker is also built into [agentic retrieval](agentic-retrieval-overview). This article is a high-level introduction to help you understand the behaviors and benefits of semantic ranker.

Semantic ranker is a premium feature that's billed by usage, but you can use it for free subject to [service limits](/en-us/azure/search/search-limits-quotas-capacity#index-limits) for the free tier. We recommend this article for background, but if you'd rather get started, [follow these steps](#how-to-get-started-with-semantic-ranker).

## What is semantic ranking?

Semantic ranker is a collection of query-side capabilities that improve the quality of an initial [BM25-ranked](index-similarity-and-scoring) or [RRF-ranked](hybrid-search-ranking) search result for text-based queries, the text portion of vector queries, and hybrid queries. Semantic ranking extends the query execution pipeline in three ways:

First, it always adds secondary ranking over an initial result set that was scored using BM25 or Reciprocal Rank Fusion (RRF). This secondary ranking uses multilingual, deep learning models adapted from Microsoft Bing to promote the most semantically relevant results.

Second, it returns captions and optionally extracts answers in the response, which you can render on a search page to improve the user's search experience.

Third, if you enable query rewrite, it expands an initial query string into multiple semantically similar query strings.


Secondary ranking and "answers" apply to the query response. Query rewrite is part of the query request.

Here are the capabilities of the semantic reranker.

| Capability | Description |
|---|---|
| L2 ranking | Uses the context or semantic meaning of a query to compute a new relevance score over preranked results. |
|

[Semantic answers](semantic-answers)[Query rewrite](semantic-how-to-query-rewrite)## How semantic ranker works

Semantic ranker takes a query and results, then sends them to language understanding models hosted by Microsoft. It scans for better matches.

The following illustration explains the concept. Consider the term "capital". It has different meanings depending on whether the context is finance, law, geography, or grammar. Through language understanding, the semantic ranker detects context and promotes results that fit query intent.


Semantic ranking uses a lot of resources and time. To finish processing within the expected latency of a query operation, the system consolidates and reduces inputs to the semantic ranker. This approach helps complete the reranking step as quickly as possible.

Semantic ranking has three steps:

- Collect and summarize inputs
- Score results by using the semantic ranker
- Output rescored results, captions, and answers

### How the system collects and summarizes inputs

In semantic ranking, the query subsystem passes search results as an input to summarization and ranking models. Because the ranking models have input size constraints and are processing intensive, search results must be sized and structured (summarized) for efficient handling.

The semantic ranker starts with a

[BM25-ranked result](index-ranking-similarity)from a text query or an[RRF-ranked result](hybrid-search-ranking)from a vector or hybrid query. The reranking exercise uses only text. Even if results include more than 50 results, only the top 50 results progress to semantic ranking. Typically, semantic ranking uses informational and descriptive fields.For each document in the search result, the summarization model accepts up to 2,000 tokens, where a token is approximately 10 characters. The model assembles inputs from the "title", "keyword", and "content" fields listed in the

[semantic configuration](semantic-how-to-configure).The system trims excessively long strings to ensure the overall length meets the input requirements of the summarization step. This trimming exercise is why it's important to add fields to your semantic configuration in priority order. If you have very large documents with text-heavy fields, the system ignores anything after the maximum limit.

Semantic field Token limit "title" 128 tokens "keywords 128 tokens "content" remaining tokens The summarization output is a summary string for each document, composed of the most relevant information from each field. The system sends summary strings to the ranker for scoring, and to machine reading comprehension models for captions and answers.

As of November 2024, the maximum length of each generated summary string passed to the semantic ranker is 2,048 tokens. Previously, it was 256 tokens.


## How results are scored

The system scores results based on the caption and any other content from the summary string that fills out the 2,048 token length.

The system evaluates captions for conceptual and semantic relevance, relative to the query you provide.

The system assigns a

**@search.rerankerScore**to each document based on the semantic relevance of the document for the given query. Scores range from 4 to 0 (high to low), where a higher score indicates higher relevance.Score Meaning 4.0 The document is highly relevant and answers the question completely, though the passage might contain extra text unrelated to the question. 3.0 The document is relevant but lacks details that would make it complete. 2.0 The document is somewhat relevant; it answers the question either partially or only addresses some aspects of the question. 1.0 The document is related to the question, and it answers a small part of it. 0.0 The document is irrelevant. The system lists matches in descending order by score and includes them in the query response payload. The payload includes answers, plain text and highlighted captions, and any fields that you marked as retrievable or specified in a select clause.


Note

For any given query, the distributions of **@search.rerankerScore** can exhibit slight variations due to conditions at the infrastructure level. Ranking model updates can also affect the distribution. For these reasons, if you're writing custom code for minimum thresholds or [setting the threshold property](vector-search-how-to-query#set-thresholds-to-exclude-low-scoring-results-preview) for vector and hybrid queries, don't make the limits too granular.

### Outputs of semantic ranker

From each summary string, the machine reading comprehension models find passages that are the most representative.

The outputs are:

A

[semantic caption](semantic-how-to-query-request)for the document. Each caption is available in a plain text version and a highlight version, and is frequently fewer than 200 words per document.An optional

[semantic answer](semantic-answers), assuming you specified the`answers`

parameter, the query was posed as a question, and a passage is found in the long string that provides a likely answer to the question.

Captions and answers are always verbatim text from your index. There's no generative AI model in this workflow that creates or composes new content.

## Semantic capabilities and limitations

What semantic ranker *can* do:

Promote matches that are semantically closer to the intent of original query.

Find strings to use as captions and answers. The response returns captions and answers, which you can render on a search results page.


What semantic ranker *can't* do is rerun the query over the entire corpus to find semantically relevant results. Semantic ranking reranks the existing result set, consisting of the top 50 results as scored by the default ranking algorithm. Furthermore, semantic ranker can't create new information or strings. The language models extract captions and answers verbatim from your content, so if the results don't include answer-like text, they won't produce one.

Although semantic ranking isn't beneficial in every scenario, certain content can benefit significantly from its capabilities. The language models in semantic ranker work best on searchable content that is information-rich and structured as prose. A knowledge base, online documentation, or documents that contain descriptive content see the most gains from semantic ranker capabilities.

The underlying technology is from Bing and Microsoft Research, and integrated into the Azure AI Search infrastructure as an add-on feature. For more information about the research and AI investments backing semantic ranker, see [How AI from Bing is powering Azure AI Search (Microsoft Research Blog)](https://www.microsoft.com/research/blog/the-science-behind-semantic-search-how-ai-from-bing-is-powering-azure-cognitive-search/).

The following video provides an overview of the capabilities.

## How semantic ranker uses synonym maps

If you enable support for [synonym maps associated to a field](search-synonyms#assign-synonyms-to-fields) in your search index, and include that field in the [semantic ranker configuration](semantic-how-to-configure), the semantic ranker automatically applies the configured synonyms during the reranking process.

## Availability and pricing

Semantic ranker is available [in selected regions](search-region-support). Use it as a standalone feature and as a built-in component of [agentic retrieval](agentic-retrieval-overview).

You can disable semantic ranker for your search service, use it on a limited basis for free, or use it more expansively with pay-as-you-go billing:

| Plan | Description |
|---|---|
| Free | A free tier search service provides 1,000 semantic ranker requests per month and 50 million free agentic reasoning tokens per month. Higher tiers can also use the free plan. |
| Standard | The standard plan is pay-as-you-go pricing once the monthly free quota is consumed. After the first 1,000 semantic ranker requests, you pay for each additional 1,000 requests. After the first 50 million agentic reasoning tokens per month, you pay a nominal fee for each one million agentic reasoning tokens. The transition from Free to Standard is seamless. You aren't notified when the transition occurs. For more information about charges by currency, see the
|

The [Azure AI Search pricing page](https://azure.microsoft.com/pricing/details/search/) shows you the billing rate for different currencies and intervals.

Charges for semantic ranker occur when query requests include `queryType=semantic`

and the search string isn't empty (for example, `search=pet friendly hotels in New York`

). If your search string is empty (`search=*`

), you aren't charged, even if the queryType is set to semantic.

## How to get started with semantic ranker

[Configure semantic ranker for the search service, choosing a pricing plan](semantic-how-to-enable-disable). The free plan is the default.
