---
merged_at: 2026-01-25T03:18:13.735250
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-vectorizer-ai-services-vision.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-vectorizer-ai-services-vision -->

# Azure Vision vectorizer

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This vectorizer is in public preview under [Supplemental Terms of Use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). The [2024-05-01-Preview REST API](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2024-05-01-Preview&preserve-view=true) and newer preview APIs support this feature.

The **Azure Vision** vectorizer connects to Azure Vision in Foundry Tools via a [Microsoft Foundry resource](/en-us/azure/ai-services/multi-service-resource). At query time, the vectorizer uses the [multimodal embeddings API](/en-us/azure/ai-services/computer-vision/concept-image-retrieval) to generate embeddings.

To determine where this model is accessible, see the [region availability for multimodal embeddings](/en-us/azure/ai-services/computer-vision/overview-image-analysis?tabs=4-0#region-availability). Your data is processed in the [Geo](https://azure.microsoft.com/explore/global-infrastructure/data-residency/) where your model is deployed.

Note

This vectorizer is bound to Foundry Tools. Execution of the vectorizer is charged at the [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

## Vectorizer parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
`resourceUri` |
The endpoint of the Foundry resource, which must have the the `https://<resource-name>.services.ai.azure.com` or `https://<resource-name>.cognitiveservices.azure.com` format. You can find this endpoint on the Keys and Endpoint page in the Azure portal. |
`apiKey` |
The API key of the Foundry resource. |
`modelVersion` |
(Required) The model version to be passed to the Azure Vision API for generating embeddings. It's important that all embeddings stored in a given index field are generated using the same `modelVersion` . For information about version support for this model refer to
|
`authIdentity` |
A user-managed identity used by the search service for connecting to Foundry. You can use either a
`apiKey` and `authIdentity` blank. The system-managed identity is used automatically. A managed identity must have Cognitive Services User permissions to use this vectorizer. |

## Supported vector query types

The Azure Vision vectorizer supports `text`

, `imageUrl`

, and `imageBinary`

vector queries.

## Expected field dimensions

A vector field configured with the Azure Vision vectorizer should have a dimensions value of 1024.

## Sample definition

```
"vectorizers": [
{
"name": "my-ai-services-vision-vectorizer",
"kind": "aiServicesVision",
"aiServicesVisionParameters": {
"resourceUri": "https://westus.api.cognitive.microsoft.com/",
"apiKey": "0000000000000000000000000000000000000",
"authIdentity": null,
"modelVersion": "2023-04-15"
},
}
]
```


---

<!-- DOCUMENTO FUSIONADO: agentic-knowledge-source-how-to-web-manage.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-how-to-web-manage -->

# Manage access to Web Knowledge Source in your Azure subscription

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Web Knowledge Source, which uses Grounding with Bing Search and/or Grounding with Bing Custom Search, is a

[First Party Consumption Service](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/EAEAS)governed by the[Grounding with Bing terms of use](https://www.microsoft.com/en-us/bing/apis/grounding-legal-enterprise)and the[Microsoft Privacy Statement](https://www.microsoft.com/en-us/privacy/privacystatement).The

[Microsoft Data Protection Addendum](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA)doesn't apply to data sent to Web Knowledge Source. When Customer uses Web Knowledge Source, Customer Data flows outside the Azure compliance and Geo boundary. This also means use of Web Knowledge Source waives all elevated Government Community Cloud security and compliance commitments to include data sovereignty and screened/citizenship-based support, as applicable.Use of Web Knowledge Source incurs costs; learn more about

[pricing](https://www.microsoft.com/en-us/bing/apis/grounding-pricing).

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

As an Azure admin, you can use the Azure CLI to enable or disable the use of [Web Knowledge Source](agentic-knowledge-source-how-to-web) at the subscription level. This setting applies to all search services within the specified subscription.

## Prerequisites

Have

**Owner**or**Contributor**access to the subscription.Have the

[Azure CLI](/en-us/cli/azure/install-azure-cli)installed. If you're not already signed in to Azure, run`az login`

.

## Check the current access state

To check the current status of Web Knowledge Source access, run the following command.

```
az feature show --name WebKnowledgeSourceDisabled --namespace Microsoft.Search --subscription "<subscription-id>"
```


The output shows the `state`

property, which indicates the current registration status:

`Registered`

means access is**disabled**.`Unregistered`

means access is**enabled**, which is the default state.

## Enable use of Web Knowledge Source

Access to Web Knowledge Source is enabled by default. If access has been disabled, you can run the following command to enable it.

```
az feature unregister --name WebKnowledgeSourceDisabled --namespace Microsoft.Search --subscription "<subscription-id>"
```


## Disable use of Web Knowledge Source

Run the following command to disable access to Web Knowledge Source.

```
az feature register --name WebKnowledgeSourceDisabled --namespace Microsoft.Search --subscription "<subscription-id>"
```
