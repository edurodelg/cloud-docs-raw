---
merged_at: 2026-01-28T07:33:20.580787
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/pinecone -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/cosmos-db -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/elasticsearch -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/azure-search -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/references/on-your-data -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/claude-models/data-privacy -->

# Data, privacy, and security for Claude models in Microsoft Foundry (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This article describes how the data that you provide is processed, used, and stored when you use Anthropic Claude models from the Microsoft Marketplace in Microsoft Foundry. Claude in Foundry processes data differently from models sold directly by Azure. When you transact for Claude in Foundry, you will agree to Anthropic's terms of use and Anthropic (not Microsoft) is the processor of the data.

As detailed in the following sections, to the extent Microsoft plays a role in processing data in connection with Claude on Foundry, it will do so pursuant to its own terms.

## What data is processed by Anthropic for Anthropic Claude models in Microsoft Foundry?

When you deploy an Anthropic Claude model from the model catalog in Foundry with pay-per-token offer for inferencing, an API is provisioned. The API gives you access to the model that Anthropic service hosts and manages. To learn more about Anthropic Claude models in Foundry, see [Models from Partners and Community](../../concepts/foundry-models-overview?view=foundry-classic#models-from-partners-and-community).

The model processes your input prompts and generates outputs based on its functionality, as described in the model details. Your use of the model (along with Anthropic's accountability for the model and its outputs) is subject to the terms of use for the model provided by Anthropic. Anthropic acts as the data processor for prompts and outputs sent to, and generated by, an Anthropic Claude API.

## What data is processed by Microsoft for Anthropic Claude models in Microsoft Foundry?

For Anthropic Claude models, Microsoft provides and manages the API deployment infrastructure and API endpoint. This data processing is pursuant to the [Microsoft Products and Services Data Protection Addendum (DPA)](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA). Microsoft also collects certain billing and usage information, which it may share with Anthropic. Such processing is subject to your Marketplace terms with Microsoft.

Note

As explained during the deployment process for Anthropic Claude API deployment, Microsoft will share customer contact information and transaction details (including the usage volume associated with the offering) with the model publisher so that the publisher can contact customers regarding the model. To learn more about information available to model publishers, see [Access insights for the Microsoft commercial marketplace in Partner Center](/en-us/partner-center/insights/analytics).

## Where can I learn about data storage and screening for harmful content for the Anthropic Claude models in Microsoft Foundry?

To learn more about storage of data, screening for harmful content, or other topics specific to the Anthropic Claude API, please see Anthropic's documentation.

## Where is data stored for Anthropic Claude models in Microsoft Foundry

For the Anthropic Claude API, prompts and outputs may be processed anywhere in the world, including outside of your region, for operational purposes. Operational purposes include performance and capacity management.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/whats-new-foundry -->

# What's new in Microsoft Foundry documentation?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Welcome! This article highlights key changes and updates in Microsoft Foundry documentation for December 2025.

This month marks a significant update to our documentation structure. With the introduction of the new Microsoft Foundry portal, we now maintain two corresponding versions of the documentation to support each portal experience. This dual-version approach ensures that users can access accurate, version-specific guidance tailored to their portal environment.

## New articles

Available in Foundry (new) only:

[Developer journey: Idea to prototype](tutorials/developer-journey-idea-to-prototype?view=foundry-classic)[Publish agents in Microsoft Foundry](agents/how-to/publish-agent?view=foundry-classic)[Agent memory concepts](agents/concepts/agent-memory?view=foundry-classic)[Build your own MCP server](mcp/build-your-own-mcp-server?view=foundry-classic)[Manage agent identities with Microsoft Entra ID](agents/concepts/agent-identity?view=foundry-classic)[Optimization model upgrade](observability/how-to/optimization-model-upgrade?view=foundry-classic)[Cluster analysis](observability/how-to/cluster-analysis?view=foundry-classic)[Optimization dashboard](observability/how-to/optimization-dashboard?view=foundry-classic)[Human evaluation](observability/how-to/human-evaluation?view=foundry-classic)[Azure Language tools and agents](../ai-services/language-service/concepts/foundry-tools-agents?view=foundry-classic)[Azure Language CLU Multi-turn conversations](../ai-services/language-service/conversational-language-understanding/concepts/multi-turn-conversations?view=foundry-classic)

Available in both Foundry (new) and Foundry (classic):

[Install CLI SDK](how-to/develop/install-cli-sdk?view=foundry-classic)[SDK overview](how-to/develop/sdk-overview?view=foundry-classic)[High availability and resiliency](how-to/high-availability-resiliency?view=foundry-classic)[Agent service disaster recovery](how-to/agent-service-disaster-recovery?view=foundry-classic)[Agent service operator disaster recovery](how-to/agent-service-operator-disaster-recovery?view=foundry-classic)[Agent service platform disaster recovery](how-to/agent-service-platform-disaster-recovery?view=foundry-classic)[Integrate with other apps](how-to/integrate-with-other-apps?view=foundry-classic)[Create a custom photo avatar](../ai-services/speech-service/text-to-speech-avatar/custom-photo-avatar-create?view=foundry-classic)[Customize voice live](../ai-services/speech-service/voice-live-how-to-customize?view=foundry-classic)[Bring your own model](../ai-services/speech-service/how-to-bring-your-own-model?view=foundry-classic)[Use the LLM-speech API](../ai-services/speech-service/llm-speech?view=foundry-classic)[Priority processing for Foundry Models](openai/concepts/priority-processing?view=foundry-classic)[Classification in Content Understanding Studio](../ai-services/content-understanding/how-to/classification-content-understanding-studio?view=foundry-classic)[Foundry playgrounds](concepts/concept-playgrounds?view=foundry-classic)[Use Claude in Foundry Models](foundry-models/how-to/use-foundry-models-claude?view=foundry-classic)[Monitor and manage agents with Foundry control plane](control-plane/overview?view=foundry-classic)

### Updated articles

All articles were updated in some way this month:

- Articles that apply to the new version were updated to add version-specific information.
- Articles that apply to both the new Microsoft Foundry and classic versions include banners that you can use to switch between the two versions to see the relevant content for each.
- Articles that apply only to the classic version include a banner indicating this limitation.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/guardrails/intervention-points -->

# Intervention points

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Agentic AI expands both capability and attack surface. As soon as an agent can call external tools, write to databases, or trigger downstream processes, malfunctions or malicious attacks can lead to steering it off course, leaking sensitive data, or executing harmful actions. Relying solely on guardrails applied to models can leave these vectors exposed. To close this gap Microsoft Foundry allows guardrails to be applied directly to agents and allows the individual controls within those guardrails to be applied to four different intervention points:

| Intervention Point | Description | Example Control at this Intervention Point |
|---|---|---|
| User input | A query sent from a user to a model or agent. Sometimes referred to as "prompt." Some controls at this intervention point require the inclusion of document embedding by the user to take effect. | Risk: User input attacksAction: Annotate and blockWhen this control is specified in an agent's or model's guardrail, the user's input is scanned by a classification model that detects jailbreak attacks. If an attack is detected, the user's input is blocked from being sent to the model, halting the model. |
| Tool call (Preview) | The next action the agent is proposing to take, as generated by its underlying model. The tool call consists of which tool is called and the arguments it's called with, including data being sent to the tool. | Risk: Hate (High) Action: Annotate and blockWhen this control is specified, every time the agent is about to execute a tool call, the proposed content being sent to the tool is scanned for hateful content. If any is detected, the tool call won't be executed, and the agent stops functioning until there is another user input. |
| Tool response (Preview) | The content sent back by a tool, internal to an agent's orchestration and before the content is to the agent's memory or given back to the end user. | Risk: Indirect attackAction: Annotate and blockWhen this control is specified, the full payload sent back from each tool to this agent is scanned for attempted indirect prompt injection attacks. If detected, the agent stops operating immediately, and prevents the malicious content from being saved by the agent and from maliciously steering the agent off-track. |
| Output | The final content sent back to the end user in response to their query. | Risk: Protected Material for TextAction: Annotate onlyWhen this control is specified, the final content meant to be displayed to the user is scanned for certain types of copyrighted text. If detected, there is a flag in the annotation response for the API used to call this model or agent. |

Important

Only certain types of tools are subject to controls at the tool call and tool response intervention points. Currently, Azure AI Search, Azure Functions, OpenAPI, Sharepoint Grounding, Fabric Data Agent, Bing Grounding, Bing Custom Search, and Browser Automation support moderation.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/guardrails/guardrails-overview -->

# Guardrails and controls overview in Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft Foundry offers safety and security guardrails that can be applied to core models, including image generation models, and agents. Agent guardrails are in preview. Guardrails consist of a set of controls. The controls define a risk to be detected, intervention points to scan for the risk, and the response action to take in the model or agent when the risk is detected. For example, a risk detection could be the annotation of the risk or blocking the model or agent from further output.

Risks are flagged via a set of classification models designed to detect and prevent the output of undesirable behavior and/or harmful content. Four intervention points are currently supported: user input, tool call (Preview), tool response (Preview), and output. Tool call and tool responses intervention points are applicable to agents only and scan the tool call made as well as content sent to the tool, and the output back from the tool, respectively.

Variations in API configurations and application design might affect completions and thus filtering behavior.

Important

The guardrail system applies to all Models sold directly by Azure, except for prompts and completions processed by the audio models such as Whisper. For more information, see [Audio models in Azure OpenAI](../openai/concepts/models?view=foundry#audio-models). The guardrail system currently applies only to agents developed in the Foundry Agent Service, not to other agents registered in the Foundry Control Plane.

## Guardrails for agents vs models

An individual Foundry guardrail can be applied to one or many models and one or many agents in a project. Some controls within a guardrail may not be relevant to models because the risk, intervention point, or action is specific to agentic behavior or tool calls. Those controls aren't run on models using that guardrail.

Some risks in Preview aren't yet supported for agents. When controls involving that risks are created in a guardrail, and the guardrail is applied to an agent, that control won't take effect in that agent. It's still applied to models using the same guardrail.

### Risk applicability

The following table summarizes which risks are applicable to models and agents:

| Risk | Applicable to Models | Applicable to Agents (Preview) |
|---|---|---|
| Hate | ✅ | ✅ |
| Sexual | ✅ | ✅ |
| Self-harm | ✅ | ✅ |
| Violence | ✅ | ✅ |
| User prompt attacks | ✅ | ✅ |
| Indirect attacks | ✅ | ✅ |
| Spotlighting (Preview) | ✅ | ❌ |
| Protected material for code | ✅ | ✅ |
| Protected material for text | ✅ | ✅ |
| Groundedness (Preview) | ✅ | ❌ |
| Personally identifiable information (Preview) | ✅ | ✅ |

### Intervention point applicability

The following table summarizes which intervention points are applicable to models and agents:

| Intervention point | Applicable to Models | Applicable to Agents (Preview) |
|---|---|---|
| User input (prompt) | ✅ | ✅ |
| Tool call (Preview) | ❌ | ✅ |
| Tool response (Preview) | ❌ | ✅ |
| Output (completion) | ✅ | ✅ |

### Action applicability

The following table summarizes which actions are applicable to models and agents:

| Action | Applicable to Models | Applicable to Agents (Preview) |
|---|---|---|
| Annotate | ✅ | ❌ |
| Annotate and block | ✅ | ✅ |

### Guardrail inheritance and override

Important

Risks are detected in an agent based on the guardrail it's assigned, not the guardrail of its underlying model. The agentic guardrail fully overrides the model's guardrail.

**Example scenario:**

- A model deployment has a control with Violence detection set to
**High**for user input and output - An agent using that model has a control with Violence detection set to
**Low**for user input and output. The agent has no controls for Violence detection at all for tool calls and responses

**Expected behavior for Violence detection in that agent:**

- User queries to the agent are scanned for Violence at a
**Low**level - Tool calls generated internally to the agent by its underlying model, including the content then sent to that tool during the tool call's execution, will
**not**be scanned for Violence - The response back from the tool will
**not**be scanned for Violence - The final output returned to the user in response to their original query are scanned for Violence at a
**Low**level

## Default guardrails

By default, models are assigned the **Microsoft.DefaultV2** guardrail. For more information on what is included in the Microsoft Default, see Default safety policy.

Unless another custom guardrail is specified upon creation, agents are assigned by default the guardrails of the model deployment being used by that agent. In other words, if no custom guardrails are specified for an agent, and that agent leverages a GPT-4o mini deployment using a guardrail named "MyCustomGuardrails," the agent will also use "MyCustomGuardrails" until another guardrail is specifically assigned to the agent. An agent will only inherit the Microsoft Default guardrails if its model is using that guardrail or if it's specifically assigned the default manually.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/reference/monitor-service -->

# Foundry Agent Service monitoring data reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

This article contains all the monitoring reference information for this service.

See [Monitor Foundry Agent Service](../how-to/metrics?view=foundry-classic) for details on the data you can collect on your agents.

## Metrics

Here are the most important metrics we think you should monitor for Agent Service. Later in this article is a longer list of all available metrics which contains more details on metrics in this shorter list. *See the below list for most up to date information. We're working on refreshing the tables in the following sections.*

## Supported metrics

This section lists all the automatically collected platform metrics for this service. These metrics are also part of the global list of [all platform metrics supported in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index#supported-metrics-per-resource-type).

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: Agents

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
AgentsNumber of events for AI Agents in this workspace |
`Agents` |
Count | Average, Maximum, Minimum, Total (Sum) | `EventType` |
PT1M | No |
IndexedFilesNumber of files indexed for file search in this workspace |
`IndexedFiles` |
Count | Average, Maximum, Minimum, Total (Sum) | `ErrorCode` , `Status` , `VectorStoreId` |
PT1M | No |
MessagesNumber of events for AI Agent messages in this workspace |
`Messages` |
Count | Average, Maximum, Minimum, Total (Sum) | `EventType` , `ThreadId` |
PT1M | No |
RunsNumber of runs by AI Agents in this workspace |
`Runs` |
Count | Average, Maximum, Minimum, Total (Sum) | `AgentId` , `RunStatus` , `StatusCode` , `StreamType` |
PT1M | No |
ThreadsNumber of events for AI Agent threads in this workspace |
`Threads` |
Count | Average, Maximum, Minimum, Total (Sum) | `EventType` |
PT1M | No |
TokensCount of tokens by AI Agents in this workspace |
`Tokens` |
Count | Average, Maximum, Minimum, Total (Sum) | `AgentId` , `TokenType` |
PT1M | No |
ToolCallsTool calls made by AI Agents in this workspace |
`ToolCalls` |
Count | Average, Maximum, Minimum, Total (Sum) | `AgentId` , `ToolName` |
PT1M | No |

### Category: Model

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Model Deploy FailedNumber of model deployments that failed in this workspace |
`Model Deploy Failed` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `StatusCode` |
PT1M | Yes |
Model Deploy StartedNumber of model deployments started in this workspace |
`Model Deploy Started` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |
Model Deploy SucceededNumber of model deployments that succeeded in this workspace |
`Model Deploy Succeeded` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |
Model Register FailedNumber of model registrations that failed in this workspace |
`Model Register Failed` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `StatusCode` |
PT1M | Yes |
Model Register SucceededNumber of model registrations that succeeded in this workspace |
`Model Register Succeeded` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |

### Category: Quota

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Active CoresNumber of active cores |
`Active Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Active NodesNumber of Acitve nodes. These are the nodes which are actively running a job. |
`Active Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Idle CoresNumber of idle cores |
`Idle Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Idle NodesNumber of idle nodes. Idle nodes are the nodes which are not running any jobs but can accept new job if available. |
`Idle Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Leaving CoresNumber of leaving cores |
`Leaving Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Leaving NodesNumber of leaving nodes. Leaving nodes are the nodes which just finished processing a job and will go to Idle state. |
`Leaving Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Preempted CoresNumber of preempted cores |
`Preempted Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Preempted NodesNumber of preempted nodes. These nodes are the low priority nodes which are taken away from the available node pool. |
`Preempted Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Quota Utilization PercentagePercent of quota utilized |
`Quota Utilization Percentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` , `VmFamilyName` , `VmPriority` |
PT1M | Yes |
Total CoresNumber of total cores |
`Total Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Total NodesNumber of total nodes. This total includes some of Active Nodes, Idle Nodes, Unusable Nodes, Premepted Nodes, Leaving Nodes |
`Total Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Unusable CoresNumber of unusable cores |
`Unusable Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Unusable NodesNumber of unusable nodes. Unusable nodes are not functional due to some unresolvable issue. Azure will recycle these nodes. |
`Unusable Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |

### Category: Resource

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
CpuCapacityMillicoresMaximum capacity of a CPU node in millicores. Capacity is aggregated in one minute intervals. |
`CpuCapacityMillicores` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuMemoryCapacityMegabytesMaximum memory utilization of a CPU node in megabytes. Utilization is aggregated in one minute intervals. |
`CpuMemoryCapacityMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuMemoryUtilizationMegabytesMemory utilization of a CPU node in megabytes. Utilization is aggregated in one minute intervals. |
`CpuMemoryUtilizationMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuMemoryUtilizationPercentageMemory utilization percentage of a CPU node. Utilization is aggregated in one minute intervals. |
`CpuMemoryUtilizationPercentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuUtilizationPercentage of utilization on a CPU node. Utilization is reported at one minute intervals. |
`CpuUtilization` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `runId` , `NodeId` , `ClusterName` |
PT1M | Yes |
CpuUtilizationMillicoresUtilization of a CPU node in millicores. Utilization is aggregated in one minute intervals. |
`CpuUtilizationMillicores` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuUtilizationPercentageUtilization percentage of a CPU node. Utilization is aggregated in one minute intervals. |
`CpuUtilizationPercentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
DiskAvailMegabytesAvailable disk space in megabytes. Metrics are aggregated in one minute intervals. |
`DiskAvailMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
DiskReadMegabytesData read from disk in megabytes. Metrics are aggregated in one minute intervals. |
`DiskReadMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
DiskUsedMegabytesUsed disk space in megabytes. Metrics are aggregated in one minute intervals. |
`DiskUsedMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
DiskWriteMegabytesData written into disk in megabytes. Metrics are aggregated in one minute intervals. |
`DiskWriteMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
GpuCapacityMilliGPUsMaximum capacity of a GPU device in milli-GPUs. Capacity is aggregated in one minute intervals. |
`GpuCapacityMilliGPUs` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuEnergyJoulesInterval energy in Joules on a GPU node. Energy is reported at one minute intervals. |
`GpuEnergyJoules` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `runId` , `rootRunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuMemoryCapacityMegabytesMaximum memory capacity of a GPU device in megabytes. Capacity aggregated in at one minute intervals. |
`GpuMemoryCapacityMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuMemoryUtilizationPercentage of memory utilization on a GPU node. Utilization is reported at one minute intervals. |
`GpuMemoryUtilization` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `runId` , `NodeId` , `DeviceId` , `ClusterName` |
PT1M | Yes |
GpuMemoryUtilizationMegabytesMemory utilization of a GPU device in megabytes. Utilization aggregated in at one minute intervals. |
`GpuMemoryUtilizationMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuMemoryUtilizationPercentageMemory utilization percentage of a GPU device. Utilization aggregated in at one minute intervals. |
`GpuMemoryUtilizationPercentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuUtilizationPercentage of utilization on a GPU node. Utilization is reported at one minute intervals. |
`GpuUtilization` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `runId` , `NodeId` , `DeviceId` , `ClusterName` |
PT1M | Yes |
GpuUtilizationMilliGPUsUtilization of a GPU device in milli-GPUs. Utilization is aggregated in one minute intervals. |
`GpuUtilizationMilliGPUs` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuUtilizationPercentageUtilization percentage of a GPU device. Utilization is aggregated in one minute intervals. |
`GpuUtilizationPercentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
IBReceiveMegabytesNetwork data received over InfiniBand in megabytes. Metrics are aggregated in one minute intervals. |
`IBReceiveMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` , `DeviceId` |
PT1M | Yes |
IBTransmitMegabytesNetwork data sent over InfiniBand in megabytes. Metrics are aggregated in one minute intervals. |
`IBTransmitMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` , `DeviceId` |
PT1M | Yes |
NetworkInputMegabytesNetwork data received in megabytes. Metrics are aggregated in one minute intervals. |
`NetworkInputMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` , `DeviceId` |
PT1M | Yes |
NetworkOutputMegabytesNetwork data sent in megabytes. Metrics are aggregated in one minute intervals. |
`NetworkOutputMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` , `DeviceId` |
PT1M | Yes |
StorageAPIFailureCountAzure Blob Storage API calls failure count. |
`StorageAPIFailureCount` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
StorageAPISuccessCountAzure Blob Storage API calls success count. |
`StorageAPISuccessCount` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |

### Category: Run

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Cancel Requested RunsNumber of runs where cancel was requested for this workspace. Count is updated when cancellation request has been received for a run. |
`Cancel Requested Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Cancelled RunsNumber of runs cancelled for this workspace. Count is updated when a run is successfully cancelled. |
`Cancelled Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Completed RunsNumber of runs completed successfully for this workspace. Count is updated when a run has completed and output has been collected. |
`Completed Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
ErrorsNumber of run errors in this workspace. Count is updated whenever run encounters an error. |
`Errors` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |
Failed RunsNumber of runs failed for this workspace. Count is updated when a run fails. |
`Failed Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Finalizing RunsNumber of runs entered finalizing state for this workspace. Count is updated when a run has completed but output collection still in progress. |
`Finalizing Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Not Responding RunsNumber of runs not responding for this workspace. Count is updated when a run enters Not Responding state. |
`Not Responding Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Not Started RunsNumber of runs in Not Started state for this workspace. Count is updated when a request is received to create a run but run information has not yet been populated. |
`Not Started Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Preparing RunsNumber of runs that are preparing for this workspace. Count is updated when a run enters Preparing state while the run environment is being prepared. |
`Preparing Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Provisioning RunsNumber of runs that are provisioning for this workspace. Count is updated when a run is waiting on compute target creation or provisioning. |
`Provisioning Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Queued RunsNumber of runs that are queued for this workspace. Count is updated when a run is queued in compute target. Can occure when waiting for required compute nodes to be ready. |
`Queued Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Started RunsNumber of runs running for this workspace. Count is updated when run starts running on required resources. |
`Started Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Starting RunsNumber of runs started for this workspace. Count is updated after request to create run and run info, such as the Run Id, has been populated |
`Starting Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
WarningsNumber of run warnings in this workspace. Count is updated whenever a run encounters a warning. |
`Warnings` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |

## Related content

- See
[Monitor Agent Service](../how-to/metrics?view=foundry-classic)for a description of monitoring Agent Service. - See
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)for details on monitoring Azure resources.
