---
merged_at: 2026-01-25T02:11:58.451463
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: semantic-search-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/semantic-search-overview -->

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


---

<!-- DOCUMENTO FUSIONADO: search-get-started-rbac.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-get-started-rbac -->

# Quickstart: Connect to a search service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use role-based access control (RBAC) and Microsoft Entra ID to establish a keyless connection to your Azure AI Search service. You then use Python in Visual Studio Code to interact with your service.

Keyless connections provide enhanced security through granular permissions and identity-based authentication. We don't recommend hard-coded API keys, but if you prefer them, see [Connect to Azure AI Search using keys](search-security-api-keys).

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An

[Azure AI Search service](search-create-service-portal)in any region or tier.The

[Azure CLI](/en-us/cli/azure/install-azure-cli)for keyless authentication with Microsoft Entra ID.[Visual Studio Code](https://code.visualstudio.com/)with the[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)and[Jupyter package](https://jupyter.org/install).

## Configure role-based access

In this section, you enable RBAC on your Azure AI Search service and assign the necessary roles for creating, loading, and querying search objects. For more information about these steps, see [Connect to Azure AI Search using roles](search-security-rbac).

To configure access:

Sign in to the

[Azure portal](https://portal.azure.com)and select your search service.From the left pane, select

**Settings > Keys**.Select

**Role-based access control**or**Both**if you need time to transition clients to RBAC.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**role to your user account or managed identity.Repeat the role assignment for

**Search Index Data Contributor**.

## Get service information

In this section, you retrieve the subscription ID and endpoint of your Azure AI Search service. If you only have one subscription, skip the subscription ID and only retrieve the endpoint. You use these values in the remaining sections of this quickstart.

To get your service information:

Sign in to the

[Azure portal](https://portal.azure.com)and select your search service.From the left pane, select

**Overview**.Make a note of the subscription ID and endpoint.


## Sign in to Azure

Before you connect to your Azure AI Search service, use the Azure CLI to sign in to the subscription that contains your service. This step establishes your Microsoft Entra identity, which `DefaultAzureCredential`

uses to authenticate requests in the next section.

To sign in:

On your local system, open a command-line tool.

Check the active subscription and tenant in your local environment.

`az account show`

If the active subscription and tenant aren't valid for your search service, run the following commands to update their values. You can find the subscription ID on the search service

**Overview**page in the Azure portal. To find the tenant ID, select the name of your subscription on the**Overview**page, and then locate the**Parent management group**value.`az account set --subscription <your-subscription-id> az login --tenant <your-tenant-id>`


## Connect to Azure AI Search

Note

This section illustrates the basic Python pattern for keyless connections. For comprehensive guidance, see a specific quickstart or tutorial, such as [Quickstart: Agentic retrieval](search-get-started-agentic-retrieval).

You can use Python notebooks in Visual Studio Code to send requests to your Azure AI Search service. For request authentication, use the `DefaultAzureCredential`

class from the Azure Identity library.

To connect using Python:

On your local system, open Visual Studio Code.

Create a

`.ipynb`

file.Create a code cell to install the

`azure-identity`

and`azure-search-documents`

libraries.`pip install azure-identity azure-search-documents`

Create another code cell to authenticate and connect to your search service.

`from azure.identity import DefaultAzureCredential from azure.search.documents.indexes import SearchIndexClient service_endpoint = "PUT-YOUR-SEARCH-SERVICE-ENDPOINT-HERE" credential = DefaultAzureCredential() client = SearchIndexClient(endpoint = service_endpoint, credential = credential) # List existing indexes indexes = client.list_indexes() for index in indexes: index_dict = index.as_dict() print(json.dumps(index_dict, indent = 2))`

Set

`service_endpoint`

to the value you obtained in[Get service information](#get-service-information).Select

**Run All**to run both code cells.The output should list the existing indexes (if any) on your search service, indicating a successful connection.


### Troubleshoot 401 errors

If you encounter a 401 error, follow these troubleshooting steps:

Revisit

[Configure role-based access](#configure-role-based-access). Your search service must have**Role-based access control**or**Both**enabled. Policies at the subscription or resource group level might override your role assignments.Revisit

[Sign in to Azure](#sign-in-to-azure). You must sign in to the subscription that contains your search service.Make sure your endpoint variable has surrounding quotes.

If all else fails, restart your device to remove cached tokens and then repeat the steps in this quickstart, starting with

[Sign in to Azure](#sign-in-to-azure).

In this quickstart, you use role-based access control (RBAC) and Microsoft Entra ID to establish a keyless connection to your Azure AI Search service. You then use REST in Visual Studio Code to interact with your service.

Keyless connections provide enhanced security through granular permissions and identity-based authentication. We don't recommend hard-coded API keys, but if you prefer them, see [Connect to Azure AI Search using keys](search-security-api-keys).

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An

[Azure AI Search service](search-create-service-portal)in any region or tier.The

[Azure CLI](/en-us/cli/azure/install-azure-cli)for keyless authentication with Microsoft Entra ID.[Visual Studio Code](https://code.visualstudio.com/)with the[REST Client extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client).

## Configure role-based access

In this section, you enable RBAC on your Azure AI Search service and assign the necessary roles for creating, loading, and querying search objects. For more information about these steps, see [Connect to Azure AI Search using roles](search-security-rbac).

To configure access:

Sign in to the

[Azure portal](https://portal.azure.com)and select your search service.From the left pane, select

**Settings > Keys**.Select

**Role-based access control**or**Both**if you need time to transition clients to RBAC.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**role to your user account or managed identity.Repeat the role assignment for

**Search Index Data Contributor**.

## Get service information

In this section, you retrieve the subscription ID and endpoint of your Azure AI Search service. If you only have one subscription, skip the subscription ID and only retrieve the endpoint. You use these values in the remaining sections of this quickstart.

To get your service information:

Sign in to the

[Azure portal](https://portal.azure.com)and select your search service.From the left pane, select

**Overview**.Make a note of the subscription ID and endpoint.


## Sign in to Azure

Before you connect to your Azure AI Search service, use the Azure CLI to sign in to the subscription that contains your service.

To sign in:

On your local system, open a command-line tool.

Check the active subscription and tenant in your local environment.

`az account show`

If the active subscription and tenant aren't valid for your search service, run the following commands to update their values. You can find the subscription ID on the search service

**Overview**page in the Azure portal. To find the tenant ID, select the name of your subscription on the**Overview**page, and then locate the**Parent management group**value.`az account set --subscription <your-subscription-id> az login --tenant <your-tenant-id>`


## Get token

REST API calls require the inclusion of a Microsoft Entra ID token. You use this token to authenticate requests in the next section.

To get your token:

Using the same command-line tool, generate an access token.

`az account get-access-token --scope https://search.azure.com/.default --query accessToken --output tsv`

Make a note of the token output.


## Connect to Azure AI Search

Note

This section illustrates the basic REST pattern for keyless connections. For comprehensive guidance, see a specific quickstart or tutorial, such as [Quickstart: Agentic retrieval](search-get-started-agentic-retrieval).

You can use the REST Client extension in Visual Studio Code to send requests to your Azure AI Search service. For request authentication, include an `Authorization`

header with the Microsoft Entra ID token you previously generated.

To connect using REST:

On your local system, open Visual Studio Code.

Create a

`.rest`

or`.http`

file.Paste the following variables and request into the file.

`@baseUrl = PUT-YOUR-SEARCH-SERVICE-ENDPOINT-HERE @token = PUT-YOUR-PERSONAL-IDENTITY-TOKEN-HERE ### List existing indexes GET {{baseUrl}}/indexes?api-version=2025-09-01 HTTP/1.1 Content-Type: application/json Authorization: Bearer {{token}}`

Set

`@baseUrl`

to the value you obtained in[Get service information](#get-service-information).Set

`@token`

to the value you obtained in[Get token](#get-token).Under

`### List existing indexes`

, select**Send Request**.You should receive an

`HTTP/1.1 200 OK`

response, indicating a successful connection to your search service.

### Troubleshoot 401 errors

If you encounter a 401 error, follow these troubleshooting steps:

Revisit

[Configure role-based access](#configure-role-based-access). Your search service must have**Role-based access control**or**Both**enabled. Policies at the subscription or resource group level might override your role assignments.Revisit

[Sign in to Azure](#sign-in-to-azure). You must sign in to the subscription that contains your search service.Make sure your endpoint and token variables don't have surrounding quotes or extra spaces.

Make sure your token doesn't have the

`@`

symbol in the request header. For example, if the variable is`@token`

, the reference in the request should be`{{token}}`

.If all else fails, restart your device to remove cached tokens and then repeat the steps in this quickstart, starting with

[Sign in to Azure](#sign-in-to-azure).
