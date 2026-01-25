---
merged_at: 2026-01-25T03:18:13.786538
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-query-sensitivity-labels.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-sensitivity-labels -->

# Query-Time Microsoft Purview Sensitivity Label Enforcement in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

At query time, Azure AI Search enforces sensitivity label policies defined in [Microsoft Purview](/en-us/purview/create-sensitivity-labels). These policies include evaluation of [READ usage rights](/en-us/purview/rights-management-usage-rights) tied to each document. As a result, users can only retrieve documents they are allowed to view.

This capability extends [document-level access control](search-document-level-access-overview) to align with your organization's [information protection and compliance requirements](/en-us/purview/create-sensitivity-labels) managed in Microsoft Purview.

When Purview sensitivity label indexing is enabled, Azure AI Search checks each document's label metadata during query time. It applies access filters based on Purview policies to return only results the requesting user is allowed to access.

This article explains how query-time sensitivity label enforcement works and how to issue secure search queries.

## Prerequisites

Before you can query a sensitivity-label-enabled index, the following conditions must be met:

You must follow all steps for

[Azure AI Search indexers to ingest Microsoft Purview sensitivity labels](search-indexer-sensitivity-labels).Both the Azure AI Search service and the user issuing the query must belong to the same Microsoft Entra tenant.

The latest

[preview API version 2025-11-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true)or a compatible beta SDK must be used to query the index.Queries must be authenticated using

[Azure role-based access control (RBAC)](search-security-rbac), not API keys. API key access is restricted to index schema retrieval only when Purview sensitivity labels functionality is enabled.

## Limitations

[Microsoft Entra Guest users](/en-us/entra/external-id/b2b-quickstart-add-guest-users-portal)and cross-tenant queries aren't supported.[Autocomplete](/en-us/rest/api/searchservice/documents/autocomplete-post)and[Suggest](/en-us/rest/api/searchservice/documents/suggest-post)APIs are unsupported for Purview-enabled indexes.- If label evaluation fails (for example, Purview APIs are temporarily unavailable), the service returns
**5xx**and does**not**return a partial or unfiltered result set. [ACL-based security filters](search-query-access-control-rbac-enforcement)aren't supported alongside sensitivity label functionality at this time. Don't enable both at the same time. Once combined usage is supported, it will be documented accordingly.- The system evaluates labels only as they existed at the time of the last indexer run; recent label changes may not be reflected until the next scheduled reindex.

## How query-time sensitivity label enforcement works

When you query an index that includes Microsoft Purview sensitivity labels, Azure AI Search checks the associated Purview policies before returning results. In this way, the query returns only documents that the user token is allowed to access.

### 1. User identity and application role input

At query time, Azure AI Search validates both:

- The calling application's RBAC role, provided in the
`Authorization`

header. - The user identity via token, provided in the
`x-ms-query-source-authorization`

header.

Both are required to authorize label-based visibility.

| Input type | Description | Example source |
|---|---|---|
| Application role | Determines whether the calling app has permission to execute queries on the index. | `Authorization: Bearer <app-token>` |
| User identity | Determines which sensitivity labels the end user is allowed to access. | `x-ms-query-source-authorization: Bearer <user-token>` |

### 2. Sensitivity label evaluation

When a query request is received, Azure AI Search evaluates:

- The sensitivityLabel field in each indexed document (extracted from Microsoft Purview during ingestion).
- The user's effective Purview permissions, as defined by Microsoft Entra ID and Purview label policy.

If the user isn't authorized for a document's sensitivity label with extract permissions, that document is excluded from the query results.

Note

Internally, the service builds dynamic access filters similar to RBAC enforcement.

These filters aren't user-visible and can't be modified in the query payload.

### 3. Secure result filtering

Azure AI Search applies the security filter after all user-defined filters and scoring steps.

A document is included in the final result set only if:

- The calling application has a valid role assignment (via RBAC), and
- The user identity token represented by
`x-ms-query-source-authorization`

is valid and permitted to view content with the document's sensitivity label.

If either condition fails, the document is omitted from the results.

## Query example

Here's an example of a query request using Microsoft Purview sensitivity label enforcement.

The query token is passed in the request headers. Both headers must include valid bearer tokens representing the application and the end user.

```
POST {{endpoint}}/indexes/sensitivity-docs/docs/search?api-version=2025-11-01-preview
Authorization: Bearer {{app-query-token}}
x-ms-query-source-authorization: Bearer {{user-query-token}}
Content-Type: application/json
{
"search": "*",
"select": "title,summary,sensitivityLabel",
"orderby": "title asc"
}
```


## Sensitivity label handling in Azure AI Search

When Azure AI Search indexes document content with sensitivity labels from sources like SharePoint, Azure Blob, and others, it stores both the content and the label metadata. The search query returns indexed content along with the GUID that identifies the sensitivity label applied to the document, only if the user has data READ access for that document. This GUID uniquely identifies the label but doesn't include human-readable properties such as the label name or associated permissions.

Note that the GUID alone is insufficient for scenarios that include user interface because sensitivity labels often carry other policy controls enforced by [Microsoft Purview Information Protection](/en-us/purview/sensitivity-labels), such as: print permissions or screenshot and screen capture restrictions. Azure AI Search doesn't surface these capabilities.

To display label names and/or enforce UI-specific restrictions, your application must call the Microsoft Purview Information Protection endpoint to retrieve full label metadata and associated permissions.

You can use the GUID returned by Azure AI Search to resolve the label properties and call the [Purview Labels APIs](/en-us/graph/api/sensitivitylabel-get) to fetch the label name, description, and policy settings. This [end-to-end demo sample](https://aka.ms/Ignite25/aisearch-purview-sensitivity-labels-repo) includes code that shows how to call the endpoint from a user interface. It also demonstrates how to extract the label name and expose it as part of the citations used in your RAG applications or agents.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-custom-skill-interface.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-custom-skill-interface -->

# Add a custom skill to an Azure AI Search enrichment pipeline

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An [AI enrichment pipeline](cognitive-search-concept-intro) can include both [built-in skills](cognitive-search-predefined-skills) and [custom skills](cognitive-search-custom-skill-web-api) that you personally create and publish. Your custom code executes externally from the search service (for example, as an Azure function), but accepts inputs and sends outputs to the skillset just like any other skill. Your data is processed in the [Geo](https://azure.microsoft.com/explore/global-infrastructure/data-residency/) where your model is deployed.

Custom skills might sound complex but can be simple and straightforward in terms of implementation. If you have existing packages that provide pattern matching or classification models, the content you extract from blobs could be passed to these models for processing. Since AI enrichment is Azure-based, your model should be on Azure also. Some common hosting methodologies include using [Azure Functions](cognitive-search-create-custom-skill-example) or [Containers](https://github.com/Microsoft/SkillsExtractorCognitiveSearch).

If you're building a custom skill, this article describes the interface you use to integrate the skill into the pipeline. The primary requirement is the ability to accept inputs and emit outputs in ways that are consumable within the [skillset](cognitive-search-defining-skillset) as a whole. As such, the focus of this article is on the input and output formats that the enrichment pipeline requires.

## Benefits of custom skills

Building a custom skill gives you a way to insert transformations unique to your content. For example, you could build custom classification models to differentiate business and financial contracts and documents, or add a speech recognition skill to reach deeper into audio files for relevant content. For a step-by-step example, see [Example: Creating a custom skill for AI enrichment](cognitive-search-create-custom-skill-example).

## Set the endpoint and time-out interval

The interface for a custom skill is specified through the [Custom Web API skill](cognitive-search-custom-skill-web-api).

```
"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",
"description": "This skill has a 230 second time-out",
"uri": "https://[your custom skill uri goes here]",
"authResourceId": "[for managed identity connections, your app's client ID goes here]",
"timeout": "PT230S",
```


The URI is the HTTPS endpoint of your function or app. When setting the URI, make sure the URI is secure (HTTPS). If your code is hosted in an Azure function app, the URI should include an [API key in the header or as a URI parameter](/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger#api-key-authorization) to authorize the request.

If instead your function or app uses Azure managed identities and Azure roles for authentication and authorization, the custom skill can include an authentication token on the request. The following points describe the requirements for this approach:

The search service, which sends the request on the indexer's behalf, must be

[configured to use a managed identity](search-how-to-managed-identities)(either system or user-assigned) so that the caller can be authenticated by Microsoft Entra ID.Your function or app must be

[configured for Microsoft Entra ID](/en-us/azure/app-service/configure-authentication-provider-aad).Your

[custom skill definition](cognitive-search-custom-skill-web-api)must include an`authResourceId`

property. This property takes an application (client) ID, in a[supported format](/en-us/azure/active-directory/develop/security-best-practices-for-app-registration#application-id-uri):`api://<appId>`

.

By default, the connection to the endpoint times out if a response isn't returned within a 30-second window (`PT30S`

). The indexing pipeline is synchronous and indexing will produce a time-out error if a response isn't received in that time frame. You can increase the interval to a maximum value of 230 seconds by setting the `timeout`

parameter (`PT230S`

).

## Format Web API inputs

The Web API must accept an array of records to be processed. Within each record, provide a property bag as input to your Web API.

Suppose you want to create a basic enricher that identifies the first date mentioned in the text of a contract. In this example, the custom skill accepts a single input "contractText" as the contract text. The skill also has a single output, which is the date of the contract. To make the enricher more interesting, return this "contractDate" in the shape of a multipart complex type.

Your Web API should be ready to receive a batch of input records. Each member of the "values" array represents the input for a particular record. Each record is required to have the following elements:

A "recordId" member that is the unique identifier for a particular record. When your enricher returns the results, it must provide this "recordId" in order to allow the caller to match the record results to their input.

A "data" member, which is essentially a bag of input fields for each record.


The resulting Web API request might look like this:

```
{
"values": [
{
"recordId": "a1",
"data":
{
"contractText":
"This is a contract that was issues on November 3, 2023 and that involves... "
}
},
{
"recordId": "b5",
"data":
{
"contractText":
"In the City of Seattle, WA on February 5, 2018 there was a decision made..."
}
},
{
"recordId": "c3",
"data":
{
"contractText": null
}
}
]
}
```


In practice, your code can be called with hundreds or thousands of records instead of only the three shown here.

## Format Web API outputs

The format of the output is a set of records containing a "recordId", and a property bag. This particular example has only one output, but you could output more than one property. As a best practice, consider returning error and warning messages if a record couldn't be processed.

```
{
"values":
[
{
"recordId": "b5",
"data" :
{
"contractDate": { "day" : 5, "month": 2, "year" : 2018 }
}
},
{
"recordId": "a1",
"data" : {
"contractDate": { "day" : 3, "month": 11, "year" : 2023 }
}
},
{
"recordId": "c3",
"data" :
{
},
"errors": [ { "message": "contractText field required "} ],
"warnings": [ {"message": "Date not found" } ]
}
]
}
```


## Add a custom skill to a skillset

When you create a Web API enricher, you can describe HTTP headers and parameters as part of the request. The following snippet shows how request parameters and optional HTTP headers can be included in the skillset definition. Setting an HTTP header is useful if you need to pass configuration settings to your code.

```
{
"skills": [
{
"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",
"name": "myCustomSkill",
"description": "This skill calls an Azure function, which in turn calls TA sentiment",
"uri": "https://indexer-e2e-webskill.azurewebsites.net/api/DateExtractor?language=en",
"context": "/document",
"httpHeaders": {
"DateExtractor-Api-Key": "foo"
},
"inputs": [
{
"name": "contractText",
"source": "/document/content"
}
],
"outputs": [
{
"name": "contractDate",
"targetName": "date"
}
]
}
]
}
```


## Watch this video

For a video introduction and demo, watch the following demo.

## Next steps

This article covered the interface requirements necessary for integrating a custom skill into a skillset. Continue with these links to learn more about custom skills and skillset composition.
