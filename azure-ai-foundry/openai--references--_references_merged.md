---
merged_at: 2026-01-25T15:32:35.903345
merged_files: 5
---

# Documentos Fusionados

Este archivo contiene 5 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: pinecone.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/pinecone -->

# Data source - Pinecone (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

The configurable options of Pinecone when using Azure OpenAI On Your Data. This data source is supported starting in API version `2024-02-15-preview`

.

| Name | Type | Required | Description |
|---|---|---|---|
`parameters` |
|

`type`

`pinecone`

.## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
`environment` |
string | True | The environment name of Pinecone. |
`index_name` |
string | True | The name of the Pinecone database index. |
`fields_mapping` |
|

`authentication`

[ApiKeyAuthenticationOptions](#api-key-authentication-options)`embedding_dependency`

[DeploymentNameVectorizationSource](#deployment-name-vectorization-source)`in_scope`

`True`

.`role_information`

`strictness`

`3`

.`top_n_documents`

`5`

.## API key authentication options

The authentication options for Azure OpenAI On Your Data when using an API key.

| Name | Type | Required | Description |
|---|---|---|---|
`key` |
string | True | The API key to use for authentication. |
`type` |
string | True | Must be `api_key` . |

## Deployment name vectorization source

The details of the vectorization source, used by Azure OpenAI On Your Data when applying vector search. This vectorization source is based on an internal embeddings model deployment name in the same Azure OpenAI resource. This vectorization source enables you to use vector search without Azure OpenAI api-key and without Azure OpenAI public network access.

| Name | Type | Required | Description |
|---|---|---|---|
`deployment_name` |
string | True | The embedding model deployment name within the same Azure OpenAI resource. |
`type` |
string | True | Must be `deployment_name` . |

## Fields mapping options

The settings to control how fields are processed.

| Name | Type | Required | Description |
|---|---|---|---|
`content_fields` |
string[] | True | The names of index fields that should be treated as content. |
`content_fields_separator` |
string | False | The separator pattern that content fields should use. Default is `\n` . |
`filepath_field` |
string | False | The name of the index field to use as a filepath. |
`title_field` |
string | False | The name of the index field to use as a title. |
`url_field` |
string | False | The name of the index field to use as a URL. |

## Examples

Prerequisites:

- Configure the role assignments from the user to the Azure OpenAI resource. Required role:
`Cognitive Services OpenAI User`

. - Install
[Az CLI](/en-us/cli/azure/install-azure-cli)and run`az login`

. - Define the following environment variables:
`AzureOpenAIEndpoint`

,`ChatCompletionsDeploymentName`

,`Environment`

,`IndexName`

,`Key`

,`EmbeddingDeploymentName`

.

```
export AzureOpenAIEndpoint=https://example.openai.azure.com/
export ChatCompletionsDeploymentName=turbo
export Environment=testenvironment
export Key=***
export IndexName=pinecone-test-index
export EmbeddingDeploymentName=ada
```


Install the latest pip packages `openai`

, `azure-identity`

.

```
import os
from openai import AzureOpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
endpoint = os.environ.get("AzureOpenAIEndpoint")
deployment = os.environ.get("ChatCompletionsDeploymentName")
environment = os.environ.get("Environment")
key = os.environ.get("Key")
index_name = os.environ.get("IndexName")
embedding_deployment_name = os.environ.get("EmbeddingDeploymentName")
token_provider = get_bearer_token_provider(
DefaultAzureCredential(), "https://cognitiveservices.azure.com/.default")
client = AzureOpenAI(
azure_endpoint=endpoint,
azure_ad_token_provider=token_provider,
api_version="2024-02-15-preview",
)
completion = client.chat.completions.create(
model=deployment,
messages=[
{
"role": "user",
"content": "Who is DRI?",
},
],
extra_body={
"data_sources": [
{
"type": "pinecone",
"parameters": {
"environment": environment,
"authentication": {
"type": "api_key",
"key": key
},
"index_name": index_name,
"fields_mapping": {
"content_fields": [
"content"
]
},
"embedding_dependency": {
"type": "deployment_name",
"deployment_name": embedding_deployment_name
}
}}
],
}
)
print(completion.model_dump_json(indent=2))
```


---

<!-- DOCUMENTO FUSIONADO: cosmos-db.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/cosmos-db -->

# Data source - Azure Cosmos DB for MongoDB vCore

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

The configurable options of Azure Cosmos DB for MongoDB vCore when using Azure OpenAI On Your Data. This data source is supported in API version `2024-02-01`

.

| Name | Type | Required | Description |
|---|---|---|---|
`parameters` |
|

`type`

`azure_cosmos_db`

.## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
`database_name` |
string | True | The MongoDB vCore database name to use with Azure Cosmos DB. |
`container_name` |
string | True | The name of the Azure Cosmos DB resource container. |
`index_name` |
string | True | The MongoDB vCore index name to use with Azure Cosmos DB. |
`fields_mapping` |
|

`authentication`

[ConnectionStringAuthenticationOptions](#connection-string-authentication-options)`embedding_dependency`

[DeploymentNameVectorizationSource](#deployment-name-vectorization-source),[EndpointVectorizationSource](#endpoint-vectorization-source)`in_scope`

`True`

.`role_information`

`strictness`

`3`

.`top_n_documents`

`5`

.## Connection string authentication options

The authentication options for Azure OpenAI On Your Data when using a connection string.

| Name | Type | Required | Description |
|---|---|---|---|
`connection_string` |
string | True | The connection string to use for authentication. |
`type` |
string | True | Must be `connection_string` . |

## Deployment name vectorization source

The details of the vectorization source, used by Azure OpenAI On Your Data when applying vector search. This vectorization source is based on an internal embeddings model deployment name in the same Azure OpenAI resource. This vectorization source enables you to use vector search without Azure OpenAI api-key and without Azure OpenAI public network access.

| Name | Type | Required | Description |
|---|---|---|---|
`deployment_name` |
string | True | The embedding model deployment name within the same Azure OpenAI resource. |
`type` |
string | True | Must be `deployment_name` . |

## Endpoint vectorization source

The details of the vectorization source, used by Azure OpenAI On Your Data when applying vector search. This vectorization source is based on the Azure OpenAI embedding API endpoint.

| Name | Type | Required | Description |
|---|---|---|---|
`endpoint` |
string | True | Specifies the resource endpoint URL from which embeddings should be retrieved. It should be in the format of `https://{YOUR_RESOURCE_NAME}.openai.azure.com/openai/deployments/YOUR_DEPLOYMENT_NAME/embeddings` . The api-version query parameter isn't allowed. |
`authentication` |
|

`type`

`endpoint`

.## API key authentication options

The authentication options for Azure OpenAI On Your Data when using an API key.

| Name | Type | Required | Description |
|---|---|---|---|
`key` |
string | True | The API key to use for authentication. |
`type` |
string | True | Must be `api_key` . |

## Fields mapping options

The settings to control how fields are processed.

| Name | Type | Required | Description |
|---|---|---|---|
`content_fields` |
string[] | True | The names of index fields that should be treated as content. |
`vector_fields` |
string[] | True | The names of fields that represent vector data. |
`content_fields_separator` |
string | False | The separator pattern that content fields should use. Default is `\n` . |
`filepath_field` |
string | False | The name of the index field to use as a filepath. |
`title_field` |
string | False | The name of the index field to use as a title. |
`url_field` |
string | False | The name of the index field to use as a URL. |

## Examples

Prerequisites:

- Configure the role assignments from the user to the Azure OpenAI resource. Required role:
`Cognitive Services OpenAI User`

. - Install
[Az CLI](/en-us/cli/azure/install-azure-cli)and run`az login`

. - Define the following environment variables:
`AzureOpenAIEndpoint`

,`ChatCompletionsDeploymentName`

,`ConnectionString`

,`Database`

,`Container`

,`Index`

,`EmbeddingDeploymentName`

.

Note

The following is for example only. If you use a connection string, store it securely somewhere else, such as in [Azure Key Vault](/en-us/azure/key-vault/general/overview). Don't include the API key directly in your code, and never post it publicly.

```
export AzureOpenAIEndpoint=https://example.openai.azure.com/
export ChatCompletionsDeploymentName=turbo
export ConnectionString='<db-connection-string>'
export Database=testdb
export Container=testcontainer
export Index=testindex
export EmbeddingDeploymentName=ada
```


Install the latest pip packages `openai`

, `azure-identity`

.

```
import os
from openai import AzureOpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
endpoint = os.environ.get("AzureOpenAIEndpoint")
deployment = os.environ.get("ChatCompletionsDeploymentName")
connection_string = os.environ.get("ConnectionString")
database = os.environ.get("Database")
container = os.environ.get("Container")
index = os.environ.get("Index")
embedding_deployment_name = os.environ.get("EmbeddingDeploymentName")
token_provider = get_bearer_token_provider(
DefaultAzureCredential(), "https://cognitiveservices.azure.com/.default")
client = AzureOpenAI(
azure_endpoint=endpoint,
azure_ad_token_provider=token_provider,
api_version="2024-02-01",
)
completion = client.chat.completions.create(
model=deployment,
messages=[
{
"role": "user",
"content": "Who is DRI?",
},
],
extra_body={
"data_sources": [
{
"type": "azure_cosmos_db",
"parameters": {
"authentication": {
"type": "connection_string",
"connection_string": connection_string
},
"database_name": database,
"container_name": container,
"index_name": index,
"fields_mapping": {
"content_fields": [
"content"
],
"vector_fields": [
"contentvector"
]
},
"embedding_dependency": {
"type": "deployment_name",
"deployment_name": embedding_deployment_name
}
}
}
],
}
)
print(completion.model_dump_json(indent=2))
```


---

<!-- DOCUMENTO FUSIONADO: elasticsearch.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/elasticsearch -->

# Data source - Elasticsearch (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

The configurable options for Elasticsearch when using Azure OpenAI On Your Data. This data source is supported starting in API version `2024-02-15-preview`

.

| Name | Type | Required | Description |
|---|---|---|---|
`parameters` |
|

`type`

`elasticsearch`

.## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
`endpoint` |
string | True | The absolute endpoint path for the Elasticsearch resource to use. |
`index_name` |
string | True | The name of the index to use in the referenced Elasticsearch. |
`authentication` |
One of
|

`embedding_dependency`

[DeploymentNameVectorizationSource](#deployment-name-vectorization-source),[EndpointVectorizationSource](#endpoint-vectorization-source),[ModelIdVectorizationSource](#model-id-vectorization-source)`query_type`

is `vector`

.`fields_mapping`

[FieldsMappingOptions](#fields-mapping-options)`in_scope`

`True`

.`query_type`

[QueryType](#query-type)`simple`

`role_information`

`strictness`

`3`

.`top_n_documents`

`5`

.## Authentication Options

Azure OpenAI On Your Data supports multiple authentication types:

### Key and key ID authentication options

The authentication options for Azure OpenAI On Your Data when using an API key.

| Name | Type | Required | Description |
|---|---|---|---|
`key` |
string | True | The Elasticsearch key to use for authentication. |
`key_id` |
string | True | The Elasticsearch key ID to use for authentication. |
`type` |
string | True | Must be `key_and_key_id` . |

### Encoded API key authentication options

The authentication options for Azure OpenAI On Your Data when using an Elasticsearch encoded API key.

| Name | Type | Required | Description |
|---|---|---|---|
`encoded_api_key` |
string | True | The Elasticsearch encoded API key to use for authentication. |
`type` |
string | True | Must be `encoded_api_key` . |

## Deployment name vectorization source

The details of the vectorization source, used by Azure OpenAI On Your Data when applying vector search. This vectorization source is based on an internal embeddings model deployment name in the same Azure OpenAI resource. This vectorization source enables you to use vector search without Azure OpenAI api-key and without Azure OpenAI public network access.

| Name | Type | Required | Description |
|---|---|---|---|
`deployment_name` |
string | True | The embedding model deployment name within the same Azure OpenAI resource. |
`type` |
string | True | Must be `deployment_name` . |

## Endpoint vectorization source

The details of the vectorization source, used by Azure OpenAI On Your Data when applying vector search. This vectorization source is based on the Azure OpenAI embedding API endpoint.

| Name | Type | Required | Description |
|---|---|---|---|
`endpoint` |
string | True | Specifies the resource endpoint URL from which embeddings should be retrieved. It should be in the format of `https://{YOUR_RESOURCE_NAME}.openai.azure.com/openai/deployments/YOUR_DEPLOYMENT_NAME/embeddings` . The api-version query parameter isn't allowed. |
`authentication` |
|

`type`

`endpoint`

.### API key authentication options

The authentication options for Azure OpenAI On Your Data when using an API key.

| Name | Type | Required | Description |
|---|---|---|---|
`key` |
string | True | The API key to use for authentication. |
`type` |
string | True | Must be `api_key` . |

## Model ID vectorization source

The details of the vectorization source, used by Azure OpenAI On Your Data when applying vector search. This vectorization source is based on Elasticsearch model ID.

| Name | Type | Required | Description |
|---|---|---|---|
`model_id` |
string | True | Specifies the model ID to use for vectorization. This model ID must be defined in Elasticsearch. |
`type` |
string | True | Must be `model_id` . |

## Fields mapping options

Optional settings to control how fields are processed when using a configured Elasticsearch resource.

| Name | Type | Required | Description |
|---|---|---|---|
`content_fields` |
string[] | False | The names of index fields that should be treated as content. |
`vector_fields` |
string[] | False | The names of fields that represent vector data. |
`content_fields_separator` |
string | False | The separator pattern that content fields should use. Default is `\n` . |
`filepath_field` |
string | False | The name of the index field to use as a filepath. |
`title_field` |
string | False | The name of the index field to use as a title. |
`url_field` |
string | False | The name of the index field to use as a URL. |

## Query type

The type of Elasticsearch retrieval query that should be executed when using it with Azure OpenAI On Your Data.

| Enum Value | Description |
|---|---|
`simple` |
Represents the default, simple query parser. |
`vector` |
Represents vector search over computed data. |

## Examples

Prerequisites:

- Configure the role assignments from the user to the Azure OpenAI resource. Required role:
`Cognitive Services OpenAI User`

. - Install
[Az CLI](/en-us/cli/azure/install-azure-cli)and run`az login`

. - Define the following environment variables:
`AzureOpenAIEndpoint`

,`ChatCompletionsDeploymentName`

,`SearchEndpoint`

,`IndexName`

,`Key`

,`KeyId`

.

```
export AzureOpenAIEndpoint=https://example.openai.azure.com/
export ChatCompletionsDeploymentName=turbo
export SearchEndpoint='https://example.eastus.azurecontainer.io'
export IndexName=testindex
export Key='***'
export KeyId='***'
```


Install the latest pip packages `openai`

, `azure-identity`

.

```
import os
from openai import AzureOpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
endpoint = os.environ.get("AzureOpenAIEndpoint")
deployment = os.environ.get("ChatCompletionsDeploymentName")
index_name = os.environ.get("IndexName")
search_endpoint = os.environ.get("SearchEndpoint")
key = os.environ.get("Key")
key_id = os.environ.get("KeyId")
token_provider = get_bearer_token_provider(
DefaultAzureCredential(), "https://cognitiveservices.azure.com/.default")
client = AzureOpenAI(
azure_endpoint=endpoint,
azure_ad_token_provider=token_provider,
api_version="2024-02-15-preview",
)
completion = client.chat.completions.create(
model=deployment,
messages=[
{
"role": "user",
"content": "Who is DRI?",
},
],
extra_body={
"data_sources": [
{
"type": "elasticsearch",
"parameters": {
"endpoint": search_endpoint,
"index_name": index_name,
"authentication": {
"type": "key_and_key_id",
"key": key,
"key_id": key_id
}
}
}
]
}
)
print(completion.model_dump_json(indent=2))
```


---

<!-- DOCUMENTO FUSIONADO: azure-search.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/azure-search -->

# Data source - Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

The configurable options of Azure AI Search when using Azure OpenAI On Your Data. This data source is supported in API version `2024-02-01`

.

| Name | Type | Required | Description |
|---|---|---|---|
`parameters` |
|

`type`

`azure_search`

.## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
`endpoint` |
string | True | The absolute endpoint path for the Azure Search resource to use. |
`index_name` |
string | True | The name of the index to use in the referenced Azure Search resource. |
`authentication` |
One of
|

`embedding_dependency`

[DeploymentNameVectorizationSource](#deployment-name-vectorization-source),[EndpointVectorizationSource](#endpoint-vectorization-source)`query_type`

is `vector`

, `vector_simple_hybrid`

, or `vector_semantic_hybrid`

.`fields_mapping`

[FieldsMappingOptions](#fields-mapping-options)`filter`

`in_scope`

`True`

.`query_type`

[QueryType](#query-type)`simple`

`role_information`

`semantic_configuration`

`query_type`

is `semantic`

or `vector_semantic_hybrid`

.`strictness`

`3`

.`top_n_documents`

`5`

.`max_search_queries`

`allow_partial_result`

`include_contexts`

`citations`

and `intent`

. Values can be `citations`

,`intent`

, `all_retrieved_documents`

.## API key authentication options

The authentication options for Azure OpenAI On Your Data when using an API key.

| Name | Type | Required | Description |
|---|---|---|---|
`key` |
string | True | The API key to use for authentication. |
`type` |
string | True | Must be `api_key` . |

## System assigned managed identity authentication options

The authentication options for Azure OpenAI On Your Data when using a system-assigned managed identity.

| Name | Type | Required | Description |
|---|---|---|---|
`type` |
string | True | Must be `system_assigned_managed_identity` . |

## User assigned managed identity authentication options

The authentication options for Azure OpenAI On Your Data when using a user-assigned managed identity.

| Name | Type | Required | Description |
|---|---|---|---|
`managed_identity_resource_id` |
string | True | The resource ID of the user-assigned managed identity to use for authentication. |
`type` |
string | True | Must be `user_assigned_managed_identity` . |

## Access token authentication options

The authentication options for Azure OpenAI On Your Data when using access token.

| Name | Type | Required | Description |
|---|---|---|---|
`access_token` |
string | True | The access token to use for authentication. |
`type` |
string | True | Must be `access_token` . |

## Deployment name vectorization source

The details of the vectorization source, used by Azure OpenAI On Your Data when applying vector search. This vectorization source is based on an internal embeddings model deployment name in the same Azure OpenAI resource. This vectorization source enables you to use vector search without Azure OpenAI api-key and without Azure OpenAI public network access.

| Name | Type | Required | Description |
|---|---|---|---|
`deployment_name` |
string | True | The embedding model deployment name within the same Azure OpenAI resource. |
`type` |
string | True | Must be `deployment_name` . |
`dimensions` |
integer | False | The number of dimensions the embeddings should have. Only supported in `text-embedding-3` and later models. |

## Endpoint vectorization source

The details of the vectorization source, used by Azure OpenAI On Your Data when applying vector search. This vectorization source is based on the Azure OpenAI embedding API endpoint.

| Name | Type | Required | Description |
|---|---|---|---|
`endpoint` |
string | True | Specifies the resource endpoint URL from which embeddings should be retrieved. It should be in the format of `https://{YOUR_RESOURCE_NAME}.openai.azure.com/openai/deployments/YOUR_DEPLOYMENT_NAME/embeddings` . The api-version query parameter isn't allowed. |
`authentication` |
|

`type`

`endpoint`

.`dimensions`

`text-embedding-3`

and later models. This is supported in the api version 2024-10-21.## Fields mapping options

Optional settings to control how fields are processed when using a configured Azure Search resource.

| Name | Type | Required | Description |
|---|---|---|---|
`content_fields` |
string[] | False | The names of index fields that should be treated as content. |
`vector_fields` |
string[] | False | The names of fields that represent vector data. |
`content_fields_separator` |
string | False | The separator pattern that content fields should use. Default is `\n` . |
`filepath_field` |
string | False | The name of the index field to use as a filepath. |
`title_field` |
string | False | The name of the index field to use as a title. |
`url_field` |
string | False | The name of the index field to use as a URL. |

## Query type

The type of Azure Search retrieval query that should be executed when using it as an Azure OpenAI On Your Data.

| Enum Value | Description |
|---|---|
`simple` |
Represents the default, simple query parser. |
`semantic` |
Represents the semantic query parser for advanced semantic modeling. |
`vector` |
Represents vector search over computed data. |
`vector_simple_hybrid` |
Represents a combination of the simple query strategy with vector data. |
`vector_semantic_hybrid` |
Represents a combination of semantic search and vector data querying. |

## Examples

Prerequisites:

- Configure the role assignments from Azure OpenAI system assigned managed identity to Azure search service. Required roles:
`Search Index Data Reader`

,`Search Service Contributor`

. - Configure the role assignments from the user to the Azure OpenAI resource. Required role:
`Cognitive Services OpenAI User`

. - Install
[Az CLI](/en-us/cli/azure/install-azure-cli), and run`az login`

. - Define the following environment variables:
`AzureOpenAIEndpoint`

,`ChatCompletionsDeploymentName`

,`SearchEndpoint`

,`SearchIndex`

.

```
export AzureOpenAIEndpoint=https://example.openai.azure.com/
export ChatCompletionsDeploymentName=turbo
export SearchEndpoint=https://example.search.windows.net
export SearchIndex=example-index
```


Install the latest pip packages `openai`

, `azure-identity`

.

```
import os
from openai import AzureOpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
endpoint = os.environ.get("AzureOpenAIEndpoint")
deployment = os.environ.get("ChatCompletionsDeploymentName")
search_endpoint = os.environ.get("SearchEndpoint")
search_index = os.environ.get("SearchIndex")
token_provider = get_bearer_token_provider(DefaultAzureCredential(), "https://cognitiveservices.azure.com/.default")
client = AzureOpenAI(
azure_endpoint=endpoint,
azure_ad_token_provider=token_provider,
api_version="2024-02-01",
)
completion = client.chat.completions.create(
model=deployment,
messages=[
{
"role": "user",
"content": "Who is DRI?",
},
],
extra_body={
"data_sources": [
{
"type": "azure_search",
"parameters": {
"endpoint": search_endpoint,
"index_name": search_index,
"authentication": {
"type": "system_assigned_managed_identity"
}
}
}
]
}
)
print(completion.model_dump_json(indent=2))
```


---

<!-- DOCUMENTO FUSIONADO: on-your-data.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/on-your-data -->

# Azure OpenAI On Your Data API Reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

This article provides reference documentation for Python and REST for the new Azure OpenAI On Your Data API. The latest API version is `2024-05-01-preview`

[Swagger spec](https://github.com/Azure/azure-rest-api-specs/tree/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/preview/2024-05-01-preview).

Note

Since API version `2024-02-15-preview`

we introduced the following breaking changes comparing to earlier API versions:

- The API path is changed from
`/extensions/chat/completions`

to`/chat/completions`

. - The naming convention of property keys and enum values is changed from camel casing to snake casing. Example:
`deploymentName`

is changed to`deployment_name`

. - The data source type
`AzureCognitiveSearch`

is changed to`azure_search`

. - The citations and intent is moved from assistant message's context tool messages to assistant message's context root level with explicit
[schema defined](#context).

```
POST {endpoint}/openai/deployments/{deployment-id}/chat/completions?api-version={api-version}
```


**Supported versions**

`2024-02-15-preview`

[Swagger spec](https://github.com/Azure/azure-rest-api-specs/blob/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/preview/2024-02-15-preview/inference.json).`2024-02-01`

[Swagger spec](https://github.com/Azure/azure-rest-api-specs/tree/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/stable/2024-02-01).`2024-05-01-preview`

[Swagger spec](https://github.com/Azure/azure-rest-api-specs/tree/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/preview/2024-05-01-preview)

Note

[Pinecone](pinecone?view=foundry-classic), and [Elasticsearch](elasticsearch?view=foundry-classic) are supported as a preview.

## URI parameters

| Name | In | Type | Required | Description |
|---|---|---|---|---|
`deployment-id` |
path | string | True | Specifies the chat completions model deployment name to use for this request. |
`endpoint` |
path | string | True | Azure OpenAI endpoints. For example: `https://{YOUR_RESOURCE_NAME}.openai.azure.com` |
`api-version` |
query | string | True | The API version to use for this operation. |

## Request body

The request body inherits the same schema of chat completions API request. This table shows the parameters unique for Azure OpenAI On Your Data.

| Name | Type | Required | Description |
|---|---|---|---|
`data_sources` |
|

`data_sources`

is not provided, the service uses chat completions model directly, and does not use Azure OpenAI On Your Data. When you specify the `data_sources`

parameter, you won't be able to use the `logprobs`

or `top_logprobs`

parameters.## Response body

The response body inherits the same schema of chat completions API response. The [response chat message](#chat-message) has a `context`

property, which is added for Azure OpenAI On Your Data.

## Chat message

The response assistant message schema inherits from the chat completions assistant [chat message](../reference?view=foundry-classic#chatmessage), and is extended with the property `context`

.

| Name | Type | Required | Description |
|---|---|---|---|
`context` |
|

## Context

| Name | Type | Required | Description |
|---|---|---|---|
`citations` |
|

`intent`

`all_retrieved_documents`

[Retrieved documents](#retrieved-documents)[]## Citation

| Name | Type | Required | Description |
|---|---|---|---|
`content` |
string | True | The content of the citation. |
`title` |
string | False | The title of the citation. |
`url` |
string | False | The URL of the citation. |
`filepath` |
string | False | The file path of the citation. |
`chunk_id` |
string | False | The chunk ID of the citation. |

## Retrieved documents

| Name | Type | Required | Description |
|---|---|---|---|
`search_queries` |
string[] | True | The search queries used to retrieve the document. |
`data_source_index` |
integer | True | The index of the data source. |
`original_search_score` |
double | True | The original search score of the retrieved document. |
`rerank_score` |
double | False | The rerank score of the retrieved document. |
`filter_reason` |
string | False | Represents the rationale for filtering the document. If the document does not undergo filtering, this field will remain unset. Will be `score` if the document is filtered by original search score threshold defined by `strictness` . Will be `rerank` if the document is not filtered by original search score threshold, but is filtered by rerank score and `top_n_documents` . |

## Data source

This list shows the supported data sources.

## Examples

This example shows how to pass conversation history for better results.

Prerequisites:

- Configure the role assignments from Azure OpenAI system assigned managed identity to Azure search service. Required roles:
`Search Index Data Reader`

,`Search Service Contributor`

. - Configure the role assignments from the user to the Azure OpenAI resource. Required role:
`Cognitive Services OpenAI User`

. - Install
[Az CLI](/en-us/cli/azure/install-azure-cli), and run`az login`

. - Define the following environment variables:
`AzureOpenAIEndpoint`

,`ChatCompletionsDeploymentName`

,`SearchEndpoint`

,`SearchIndex`

.

```
export AzureOpenAIEndpoint=https://example.openai.azure.com/
export ChatCompletionsDeploymentName=turbo
export SearchEndpoint=https://example.search.windows.net
export SearchIndex=example-index
```


Install the latest pip packages `openai`

, `azure-identity`

.

```
import os
from openai import AzureOpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
endpoint = os.environ.get("AzureOpenAIEndpoint")
deployment = os.environ.get("ChatCompletionsDeploymentName")
search_endpoint = os.environ.get("SearchEndpoint")
search_index = os.environ.get("SearchIndex")
token_provider = get_bearer_token_provider(DefaultAzureCredential(), "https://cognitiveservices.azure.com/.default")
client = AzureOpenAI(
azure_endpoint=endpoint,
azure_ad_token_provider=token_provider,
api_version="2024-05-01-preview",
)
completion = client.chat.completions.create(
model=deployment,
messages=[
{
"role": "user",
"content": "Who is DRI?",
},
{
"role": "assistant",
"content": "DRI stands for Directly Responsible Individual of a service. Which service are you asking about?"
},
{
"role": "user",
"content": "Opinion mining service"
}
],
extra_body={
"data_sources": [
{
"type": "azure_search",
"parameters": {
"endpoint": search_endpoint,
"index_name": search_index,
"authentication": {
"type": "system_assigned_managed_identity"
}
}
}
]
}
)
print(completion.model_dump_json(indent=2))
# render the citations
content = completion.choices[0].message.content
context = completion.choices[0].message.context
for citation_index, citation in enumerate(context["citations"]):
citation_reference = f"[doc{citation_index + 1}]"
url = "https://example.com/?redirect=" + citation["url"] # replace with actual host and encode the URL
filepath = citation["filepath"]
title = citation["title"]
snippet = citation["content"]
chunk_id = citation["chunk_id"]
replaced_html = f"<a href='{url}' title='{title}\n{snippet}''>(See from file {filepath}, Part {chunk_id})</a>"
content = content.replace(citation_reference, replaced_html)
print(content)
```
