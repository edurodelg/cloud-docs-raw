---
merged_at: 2026-01-25T03:18:13.745018
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-csharp-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/tutorial-csharp-overview -->

# Step 1 - Overview of adding search to a static web app with .NET

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial builds a website that searches through a catalog of books and then deploys the website to an Azure Static Web App.

## What does the sample do?

This sample website provides access to a catalog of 10,000 books. You can search the catalog by entering text in the search bar. While you enter text, the website uses the search index's suggestion feature to autocomplete the text. When the query finishes, the website displays the list of books with a portion of the details. You can select a book to see all the details, stored in the search index, of the book.


The search experience includes:

[Search](search-query-create)– provides search functionality for the application.[Suggest](search-add-autocomplete-suggestions)– provides suggestions as the user is typing in the search bar.[Facets and filters](search-faceted-navigation)- provides a faceted navigation structure that filters by author or language.[Paginated results](search-pagination-page-layout)- provides paging controls for scrolling through results.[Document Lookup](search-query-overview#document-look-up)– looks up a document by ID to retrieve all of its contents for the details page.

## How is the sample organized?

The [sample code](https://github.com/Azure-Samples/azure-search-static-web-app) includes the following components:

| App | Purpose | GitHub Repository Location |
|---|---|---|
| client | React app (presentation layer) to display books, with search. It calls the Azure Function app. |
|

[/azure-search-static-web-app/api](https://github.com/Azure-Samples/azure-search-static-web-app/tree/main/api)[/azure-search-static-web-app/bulk-insert](https://github.com/Azure-Samples/azure-search-static-web-app/tree/main/bulk-insert)## Set up your development environment

Create services and install the following software for your local development environment.

[Azure AI Search](search-create-service-portal), any region or tier[.NET 9](https://dotnet.microsoft.com/download/dotnet)or latest version[Git](https://git-scm.com/downloads)[Visual Studio Code](https://code.visualstudio.com/)[C# Dev Tools extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit)[Azure Static Web App extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps)

This tutorial doesn't run the Azure Function API locally. If you want to run it locally, install [azure-functions-core-tools](/en-us/azure/azure-functions/functions-run-local?tabs=linux%2ccsharp%2cbash#install-the-azure-functions-core-tools).

## Fork and clone the search sample with git

To deploy the Static Web App, you need to fork the sample repository. The web apps use your GitHub fork location to decide the build actions and deployment content. Code execution in the Static Web App happens remotely, with Azure Static Web Apps reading the code from your forked sample.

On GitHub, fork the

[azure-search-static-web-app repository](https://github.com/Azure-Samples/azure-search-static-web-app).Complete the

[fork process](https://docs.github.com/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)in your web browser with your GitHub account. This tutorial uses your fork as part of the deployment to an Azure Static Web App.At a Bash terminal, download your forked sample application to your local computer.

Replace

`YOUR-GITHUB-ALIAS`

with your GitHub alias.`git clone https://github.com/YOUR-GITHUB-ALIAS/azure-search-static-web-app.git`

At the same Bash terminal, go into your forked repository for this website search example:

`cd azure-search-static-web-app`

Use the Visual Studio Code command,

`code .`

to open your forked repository. You accomplish the remaining tasks from Visual Studio Code, unless specified.`code .`


---

<!-- DOCUMENTO FUSIONADO: vector-search-vectorizer-azure-open-ai.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-vectorizer-azure-open-ai -->

# Azure OpenAI vectorizer

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Azure OpenAI** vectorizer connects to an embedding model deployed to your [Azure OpenAI in Foundry Models](/en-us/azure/ai-services/openai/overview) resource or [Microsoft Foundry](/en-us/azure/ai-foundry/what-is-azure-ai-foundry) project to generate embeddings at query time. Your data is processed in the [Geo](https://azure.microsoft.com/explore/global-infrastructure/data-residency/) where your model is deployed.

Although vectorizers are used at query time, you specify them in index definitions and reference them on vector fields through a vector profile. For more information, see [Configure a vectorizer in a search index](vector-search-how-to-configure-vectorizer).

The Azure OpenAI vectorizer is called `AzureOpenAIVectorizer`

in the REST API. Use the latest stable version of [Indexes - Create (REST API)](/en-us/rest/api/searchservice/indexes/create) or an Azure SDK package that provides the feature.

Note

This vectorizer is bound to Azure OpenAI and is charged at the [Azure OpenAI Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/#pricing).

## Prerequisites

An

[Azure OpenAI in Foundry Models resource](/en-us/azure/ai-foundry/openai/how-to/create-resource)or[Foundry project](/en-us/azure/ai-foundry/how-to/create-projects).Your Azure OpenAI resource must have a

[custom subdomain](/en-us/azure/ai-services/cognitive-services-custom-subdomains), such as`https://<resource-name>.openai.azure.com`

. You can find this endpoint on the**Keys and Endpoint**page in the Azure portal and use it for the`resourceUri`

property in this skill.The

[parent resource](/en-us/azure/ai-services/multi-service-resource)of your Foundry project provides access to multiple endpoints, including`https://<resource-name>.openai.azure.com`

,`https://<resource-name>.services.ai.azure.com`

, and`https://<resource-name>.cognitiveservices.azure.com`

. You can find these endpoints on the**Keys and Endpoint**page in the Azure portal and use any of them for the`resourceUri`

property in this skill.

An Azure OpenAI embedding model deployed to your resource or project. For supported models, see the next section.


## Vectorizer parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
`resourceUri` |
(Required) The URI of the model provider. Supported domains are:
|
`apiKey` |
The secret key used to access the model. If you provide a key, leave `authIdentity` empty. If you set both `apiKey` and `authIdentity` , the `apiKey` is used on the connection. |
`deploymentId` |
(Required) The ID of the deployed Azure OpenAI embedding model. This is the deployment name you specified when you deployed the model. |
`authIdentity` |
A user-managed identity used by the search service for the connection. You can use either a
`apiKey` and `authIdentity` blank. The system-managed identity is used automatically. A managed identity must have
|

`modelName`

`deploymentId`

. Supported values are:`text-embedding-ada-002`

`text-embedding-3-large`

`text-embedding-3-small`


## Supported vector query types

The Azure OpenAI vectorizer only supports `text`

vector queries.

## Expected field dimensions

The expected field dimensions for a field configured with an Azure OpenAI vectorizer depend on the `modelName`

that is configured.

`modelName` |
Minimum dimensions | Maximum dimensions |
|---|---|---|
| text-embedding-ada-002 | 1536 | 1536 |
| text-embedding-3-large | 1 | 3072 |
| text-embedding-3-small | 1 | 1536 |

## Sample definition

```
"vectorizers": [
{
"name": "my-openai-vectorizer",
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "https://my-fake-azure-openai-resource.openai.azure.com",
"apiKey": "0000000000000000000000000000000000000",
"deploymentId": "my-ada-002-deployment",
"authIdentity": null,
"modelName": "text-embedding-ada-002",
},
}
]
```
