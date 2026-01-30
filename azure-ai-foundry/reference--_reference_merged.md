---
merged_at: 2026-01-31T00:00:14.669928
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/reference/region-support -->

# Microsoft Foundry feature availability across cloud regions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) brings together various Azure AI capabilities that were previously only available as standalone Azure services. While Microsoft strives to make all features available in all regions where Microsoft Foundry is supported at the same time, feature availability might vary by region. In this article, you learn what Foundry features are available across cloud regions.

## Foundry projects

Foundry is currently available in the following Azure regions.

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) brings together various Azure AI capabilities that were previously only available as standalone Azure services. While Microsoft strives to make all features available in all regions where Foundry is supported at the same time, feature availability might vary by region. In this article, you learn what Foundry features are available across cloud regions.

## Foundry projects

Foundry is currently available in the following Azure regions. You can [create either a Foundry project or hub-based project in Foundry](../how-to/create-projects?view=foundry-classic) in these regions.

- Australia East
- Brazil South
- Canada Central
- Canada East
- Central India
- East Asia
- East US
- East US 2
- France Central
- Germany West Central
- Italy North

- Japan East
- Korea Central
- North Central US
- North Europe
- Norway East
- Qatar Central
- South Africa North
- South Central US
- South India
- Southeast Asia

- Spain Central
- Sweden Central
- Switzerland North
- UAE North
- UK South
- West Europe
- West US
- West US 3
- US Gov Virginia
- US Gov Arizona

- Australia East
- Brazil South
- Canada Central
- Canada East
- Central India
- East Asia
- East US
- East US 2
- France Central
- Germany West Central
- Italy North

- Japan East
- Korea Central
- North Central US
- North Europe
- Norway East
- Qatar Central
- South Africa North
- South Central US
- South India
- Southeast Asia

- Spain Central
- Sweden Central
- Switzerland North
- UAE North
- UK South
- West Europe
- West US
- West US 3

## Foundry features

For maximum feature availability, consider East US 2 or Sweden Central as your primary regions, as they offer the most comprehensive coverage across features.

Use the following table to investigate regional availability for specific features you plan to use.

| Service | Description | Link |
|---|---|---|
| Azure OpenAI | Some models might not be available within the Foundry model catalog. |
|

[Speech service supported regions](../../ai-services/speech-service/regions?view=foundry-classic)[What is Azure AI Content Safety?](../../ai-services/content-safety/overview?view=foundry-classic#region-availability).[Agent Service region availability](../../ai-services/agents/concepts/model-region-support?view=foundry-classic#azure-openai-models).| Service | Description | Link |
|---|---|---|
| Azure OpenAI | Some models might not be available within the model catalog. |
|

[Speech service supported regions](../../ai-services/speech-service/regions?view=foundry-classic).[Region availability for models in serverless deployment](../how-to/deploy-models-serverless-availability?view=foundry-classic).[What is Azure AI Content Safety?](../../ai-services/content-safety/overview?view=foundry-classic#region-availability).[Agent Service region availability](../../ai-services/agents/concepts/model-region-support?view=foundry-classic#azure-openai-models).## Foundry in sovereign clouds

### Azure Government (United States)

Available only to US government entities and their partners. For more information, see [Azure Government documentation](/en-us/azure/azure-government/documentation-government-welcome) and [Compare Azure Government and global Azure](/en-us/azure/azure-government/compare-azure-government-global-azure).

**Foundry portal URL:****Regions:**- US Gov Arizona
- US Gov Virginia

**Available pricing tiers:**- Standard. For more information, see
[Foundry pricing](https://azure.microsoft.com/pricing/details/ai-foundry/).

- Standard. For more information, see
**Supported features:**[Azure OpenAI in Foundry Models](../openai/azure-government?view=foundry-classic)- Foundry Tools
[Speech](../../ai-services/speech-service/regions?view=foundry-classic)- Speech playground (preview)
- Language playground (preview)
- Language +
[Translator](../../ai-services/translator/reference/sovereign-clouds?view=foundry-classic) - Vision + Document
- Content Safety

- Model catalog. For the list of supported models, see
[Machine learning cloud parity](../../machine-learning/reference-machine-learning-cloud-parity?view=foundry-classic). - Templates (preview)
- Prompt flow
- Tracing (preview)
- Guardrails & controls
- Content filters
- Profanity blocklist (preview)

- Management center

**Unsupported features in Azure Government regions:**- Serverless endpoints
- Content Understanding
- Agents playground
- Images playground
- Real-time audio playground
- Healthcare playground
- Fine-tuning
- Azure AI Agents
- Batch jobs
- Azure OpenAI Evaluation
- Deploy Web App
- VS Code Extension


## Use AI to find the best region

Use AI to help you find the right region for your needs. Open [Ask AI](../concepts/ask-ai?view=foundry-classic) and customize this prompt for your specific case:

```
Based on the features I need for my Foundry project, which regions would you recommend to create the project?
I need: [list your required features here, such as: gpt-4o models, speech capabilities, custom avatar training, etc.]
```


*Copilot is powered by AI, so surprises and mistakes are possible. For more information, see Copilot general use FAQs.*

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/reference/foundry-project-rest-preview -->

# Microsoft Foundry Project REST reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

API Version: 2025-11-15-preview

## Agents - create agent

```
POST {endpoint}/agents?api-version=2025-11-15-preview
```


Creates the agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| definition | object | Yes | ||
| └─ kind |
|

[RaiConfig](#raiconfig)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

- Must start and end with alphanumeric characters,

- Can contain hyphens in the middle

- Must not exceed 63 characters.

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - list agents

```
GET {endpoint}/agents?api-version=2025-11-15-preview
```


Returns the list of all agents.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| kind | query | No | Filter agents by kind. If not provided, all agents are returned. | |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and`desc` for descending order. |
| after | query | No | string | A cursor for use in pagination. `after` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list. |
| before | query | No | string | A cursor for use in pagination. `before` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - get agent

```
GET {endpoint}/agents/{agent_name}?api-version=2025-11-15-preview
```


Retrieves the agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - update agent

```
POST {endpoint}/agents/{agent_name}?api-version=2025-11-15-preview
```


Updates the agent by adding a new version if there are any changes to the agent definition. If no changes, returns the existing agent version.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| definition | object | Yes | ||
| └─ kind |
|

[RaiConfig](#raiconfig)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - delete agent

```
DELETE {endpoint}/agents/{agent_name}?api-version=2025-11-15-preview
```


Deletes an agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - update agent from manifest

```
POST {endpoint}/agents/{agent_name}/import?api-version=2025-11-15-preview
```


Updates the agent from a manifest by adding a new version if there are any changes to the agent definition. If no changes, returns the existing agent version.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent to update. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A human-readable description of the agent. | No | |
| manifest_id | string | The manifest ID to import the agent version from. | Yes | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No | |
| parameter_values | object | The inputs to the manifest that will result in a fully materialized Agent. | Yes |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - list agent container operations

```
GET {endpoint}/agents/{agent_name}/operations?api-version=2025-11-15-preview
```


List container operations for an agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent. |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and`desc` for descending order. |
| after | query | No | string | A cursor for use in pagination. `after` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list. |
| before | query | No | string | A cursor for use in pagination. `before` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - get agent container operation

```
GET {endpoint}/agents/{agent_name}/operations/{operation_id}?api-version=2025-11-15-preview
```


Get the status of a container operation for an agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent. |
| operation_id | path | Yes | string | The operation ID. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - create agent version

```
POST {endpoint}/agents/{agent_name}/versions?api-version=2025-11-15-preview
```


Create a new agent version.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The unique name that identifies the agent. Name can be used to retrieve/update/delete the agent. - Must start and end with alphanumeric characters, - Can contain hyphens in the middle - Must not exceed 63 characters. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| definition | object | Yes | ||
| └─ kind |
|

[RaiConfig](#raiconfig)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - list agent versions

```
GET {endpoint}/agents/{agent_name}/versions?api-version=2025-11-15-preview
```


Returns the list of versions of an agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent to retrieve versions for. |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and`desc` for descending order. |
| after | query | No | string | A cursor for use in pagination. `after` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list. |
| before | query | No | string | A cursor for use in pagination. `before` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - get agent version

```
GET {endpoint}/agents/{agent_name}/versions/{agent_version}?api-version=2025-11-15-preview
```


Retrieves a specific version of an agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent to retrieve. |
| agent_version | path | Yes | string | The version of the agent to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - delete agent version

```
DELETE {endpoint}/agents/{agent_name}/versions/{agent_version}?api-version=2025-11-15-preview
```


Deletes a specific version of an agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent to delete. |
| agent_version | path | Yes | string | The version of the agent to delete |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - get agent container

```
GET {endpoint}/agents/{agent_name}/versions/{agent_version}/containers/default?api-version=2025-11-15-preview
```


Get a container for a specific version of an agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent. |
| agent_version | path | Yes | string | The version of the agent. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - list agent version container operations

```
GET {endpoint}/agents/{agent_name}/versions/{agent_version}/containers/default/operations?api-version=2025-11-15-preview
```


List container operations for a specific version of an agent.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent. |
| agent_version | path | Yes | string | The version of the agent. |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and`desc` for descending order. |
| after | query | No | string | A cursor for use in pagination. `after` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list. |
| before | query | No | string | A cursor for use in pagination. `before` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - delete agent container

```
POST {endpoint}/agents/{agent_name}/versions/{agent_version}/containers/default:delete?api-version=2025-11-15-preview
```


Delete a container for a specific version of an agent. If the container doesn't exist, the operation will be no-op.
The operation is a long-running operation. Following the design guidelines for long-running operations in Azure REST APIs.
[https://github.com/microsoft/api-guidelines/blob/vNext/azure/ConsiderationsForServiceDesign.md#action-operations](https://github.com/microsoft/api-guidelines/blob/vNext/azure/ConsiderationsForServiceDesign.md#action-operations)

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent. |
| agent_version | path | Yes | string | The version of the agent. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 202

**Description**: The request has been accepted for processing, but processing has not yet completed.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - start agent container

```
POST {endpoint}/agents/{agent_name}/versions/{agent_version}/containers/default:start?api-version=2025-11-15-preview
```


Start a container for a specific version of an agent. If the container is already running, the operation will be no-op.
The operation is a long-running operation. Following the design guidelines for long-running operations in Azure REST APIs.
[https://github.com/microsoft/api-guidelines/blob/vNext/azure/ConsiderationsForServiceDesign.md#action-operations](https://github.com/microsoft/api-guidelines/blob/vNext/azure/ConsiderationsForServiceDesign.md#action-operations)

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent. |
| agent_version | path | Yes | string | The version of the agent. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| max_replicas | integer | The maximum number of replicas. Defaults to 1. | No | 1 |
| min_replicas | integer | The minimum number of replicas. Defaults to 1. | No | 1 |

### Responses

**Status Code:** 202

**Description**: The request has been accepted for processing, but processing has not yet completed.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - stop agent container

```
POST {endpoint}/agents/{agent_name}/versions/{agent_version}/containers/default:stop?api-version=2025-11-15-preview
```


Stop a container for a specific version of an agent. If the container is not running, or already stopped, the operation will be no-op.
The operation is a long-running operation. Following the design guidelines for long-running operations in Azure REST APIs.
[https://github.com/microsoft/api-guidelines/blob/vNext/azure/ConsiderationsForServiceDesign.md#action-operations](https://github.com/microsoft/api-guidelines/blob/vNext/azure/ConsiderationsForServiceDesign.md#action-operations)

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent. |
| agent_version | path | Yes | string | The version of the agent. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 202

**Description**: The request has been accepted for processing, but processing has not yet completed.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - update agent container

```
POST {endpoint}/agents/{agent_name}/versions/{agent_version}/containers/default:update?api-version=2025-11-15-preview
```


Update a container for a specific version of an agent. If the container is not running, the operation will be no-op.
The operation is a long-running operation. Following the design guidelines for long-running operations in Azure REST APIs.
[https://github.com/microsoft/api-guidelines/blob/vNext/azure/ConsiderationsForServiceDesign.md#action-operations](https://github.com/microsoft/api-guidelines/blob/vNext/azure/ConsiderationsForServiceDesign.md#action-operations)

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The name of the agent. |
| agent_version | path | Yes | string | The version of the agent. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| max_replicas | integer | The maximum number of replicas. | No | |
| min_replicas | integer | The minimum number of replicas. | No |

### Responses

**Status Code:** 202

**Description**: The request has been accepted for processing, but processing has not yet completed.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - create agent version from manifest

```
POST {endpoint}/agents/{agent_name}/versions:import?api-version=2025-11-15-preview
```


Create a new agent version from a manifest.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| agent_name | path | Yes | string | The unique name that identifies the agent. Name can be used to retrieve/update/delete the agent. - Must start and end with alphanumeric characters, - Can contain hyphens in the middle - Must not exceed 63 characters. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A human-readable description of the agent. | No | |
| manifest_id | string | The manifest ID to import the agent version from. | Yes | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No | |
| parameter_values | object | The inputs to the manifest that will result in a fully materialized Agent. | Yes |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Agents - create agent from manifest

```
POST {endpoint}/agents:import?api-version=2025-11-15-preview
```


Creates an agent from a manifest.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A human-readable description of the agent. | No | |
| manifest_id | string | The manifest ID to import the agent version from. | Yes | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No | |
| name | string | The unique name that identifies the agent. Name can be used to retrieve/update/delete the agent. - Must start and end with alphanumeric characters, - Can contain hyphens in the middle - Must not exceed 63 characters. |
Yes | |
| parameter_values | object | The inputs to the manifest that will result in a fully materialized Agent. | Yes |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Connections - list

```
GET {endpoint}/connections?api-version=2025-11-15-preview
```


List all connections in the project, without populating connection credentials

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| connectionType | query | No | List connections of this specific type | |
| defaultConnection | query | No | boolean | List connections that are default connections |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Connections - get

```
GET {endpoint}/connections/{name}?api-version=2025-11-15-preview
```


Get a connection by name, without populating connection credentials

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The friendly name of the connection, provided by the user. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Connections - get with credentials

```
POST {endpoint}/connections/{name}/getConnectionWithCredentials?api-version=2025-11-15-preview
```


Get a connection by name, with its connection credentials

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The friendly name of the connection, provided by the user. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Datasets - list latest

```
GET {endpoint}/datasets?api-version=2025-11-15-preview
```


List the latest version of each DatasetVersion

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Datasets - list versions

```
GET {endpoint}/datasets/{name}/versions?api-version=2025-11-15-preview
```


List all versions of the given DatasetVersion

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Datasets - get version

```
GET {endpoint}/datasets/{name}/versions/{version}?api-version=2025-11-15-preview
```


Get the specific version of the DatasetVersion. The service returns 404 Not Found error if the DatasetVersion does not exist.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The specific version id of the DatasetVersion to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Datasets - delete version

```
DELETE {endpoint}/datasets/{name}/versions/{version}?api-version=2025-11-15-preview
```


Delete the specific version of the DatasetVersion. The service returns 204 No Content if the DatasetVersion was deleted successfully or if the DatasetVersion does not exist.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The version of the DatasetVersion to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 204

**Description**: There is no content to send for this request, but the headers may be useful.

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Datasets - create or update version

```
PATCH {endpoint}/datasets/{name}/versions/{version}?api-version=2025-11-15-preview
```


Create a new or update an existing DatasetVersion with the given version id

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The specific version id of the DatasetVersion to create or update. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/merge-patch+json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | The asset description text. | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No | |
| type | object | Enum to determine the type of data. | Yes |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** 201

**Description**: The request has succeeded and a new resource has been created as a result.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Datasets - get credentials

```
POST {endpoint}/datasets/{name}/versions/{version}/credentials?api-version=2025-11-15-preview
```


Get the SAS credential to access the storage account associated with a Dataset version.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The specific version id of the DatasetVersion to operate on. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Datasets - start pending upload version

```
POST {endpoint}/datasets/{name}/versions/{version}/startPendingUpload?api-version=2025-11-15-preview
```


Start a new or get an existing pending upload of a dataset for a specific version.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The specific version id of the DatasetVersion to operate on. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| connectionName | string | Azure Storage Account connection name to use for generating temporary SAS token | No | |
| pendingUploadId | string | If PendingUploadId is not provided, a random GUID will be used. | No | |
| pendingUploadType | enum | BlobReference is the only supported type. Possible values: `BlobReference` |
Yes |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Deployments - list

```
GET {endpoint}/deployments?api-version=2025-11-15-preview
```


List all deployed models in the project

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| modelPublisher | query | No | string | Model publisher to filter models by |
| modelName | query | No | string | Model name (the publisher specific name) to filter models by |
| deploymentType | query | No | Type of deployment to filter list by | |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Deployments - get

```
GET {endpoint}/deployments/{name}?api-version=2025-11-15-preview
```


Get a deployed model.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | Name of the deployment |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluation rules - list

```
GET {endpoint}/evaluationrules?api-version=2025-11-15-preview
```


List all evaluation rules.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| actionType | query | No | Filter by the type of evaluation rule. | |
| agentName | query | No | string | Filter by the agent name. |
| enabled | query | No | boolean | Filter by the enabled status. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluation rules - get

```
GET {endpoint}/evaluationrules/{id}?api-version=2025-11-15-preview
```


Get an evaluation rule.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| id | path | Yes | string | Unique identifier for the evaluation rule. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluation rules - delete

```
DELETE {endpoint}/evaluationrules/{id}?api-version=2025-11-15-preview
```


Delete an evaluation rule.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| id | path | Yes | string | Unique identifier for the evaluation rule. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 204

**Description**: There is no content to send for this request, but the headers may be useful.

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluation rules - create or update

```
PUT {endpoint}/evaluationrules/{id}?api-version=2025-11-15-preview
```


Create or update an evaluation rule.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| id | path | Yes | string | Unique identifier for the evaluation rule. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| action | object | Evaluation action model. | Yes | |
| └─ type |
|

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** 201

**Description**: The request has succeeded and a new resource has been created as a result.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluation taxonomies - list

```
GET {endpoint}/evaluationtaxonomies?api-version=2025-11-15-preview
```


List evaluation taxonomies

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| inputName | query | No | string | Filter by the evaluation input name. |
| inputType | query | No | string | Filter by taxonomy input type. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluation taxonomies - get

```
GET {endpoint}/evaluationtaxonomies/{name}?api-version=2025-11-15-preview
```


Get an evaluation run by name.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluation taxonomies - delete

```
DELETE {endpoint}/evaluationtaxonomies/{name}?api-version=2025-11-15-preview
```


Delete an evaluation taxonomy by name.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 204

**Description**: There is no content to send for this request, but the headers may be useful.

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluation taxonomies - create

```
PUT {endpoint}/evaluationtaxonomies/{name}?api-version=2025-11-15-preview
```


Create an evaluation taxonomy.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the evaluation taxonomy. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | The asset description text. | No | |
| properties | object | Additional properties for the evaluation taxonomy. | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No | |
| taxonomyCategories | array | List of taxonomy categories. | No | |
| taxonomyInput | object | Input configuration for the evaluation taxonomy. | Yes | |
| └─ type |
|

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** 201

**Description**: The request has succeeded and a new resource has been created as a result.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluation taxonomies - update

```
PATCH {endpoint}/evaluationtaxonomies/{name}?api-version=2025-11-15-preview
```


Update an evaluation taxonomy.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the evaluation taxonomy. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | The asset description text. | No | |
| properties | object | Additional properties for the evaluation taxonomy. | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No | |
| taxonomyCategories | array | List of taxonomy categories. | No | |
| taxonomyInput | object | Input configuration for the evaluation taxonomy. | No | |
| └─ type |
|

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluators - list latest versions

```
GET {endpoint}/evaluators?api-version=2025-11-15-preview
```


List the latest version of each evaluator

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| type | query | No | Filter evaluators by type. Possible values: 'all', 'custom', 'builtin'. | |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluators - list versions

```
GET {endpoint}/evaluators/{name}/versions?api-version=2025-11-15-preview
```


List all versions of the given evaluator

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| type | query | No | Filter evaluators by type. Possible values: 'all', 'custom', 'builtin'. | |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluators - create version

```
POST {endpoint}/evaluators/{name}/versions?api-version=2025-11-15-preview
```


Create a new EvaluatorVersion with auto incremented version id

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| categories | array | The categories of the evaluator | Yes | |
| definition | object | Base evaluator configuration with discriminator | Yes | |
| └─ data_schema | The JSON schema (Draft 2020-12) for the evaluator's input data. This includes parameters like type, properties, required. | No | ||
| └─ init_parameters | The JSON schema (Draft 2020-12) for the evaluator's input parameters. This includes parameters like type, properties, required. | No | ||
| └─ metrics | object | List of output metrics produced by this evaluator | No | |
| └─ type |
|

### Responses

**Status Code:** 201

**Description**: The request has succeeded and a new resource has been created as a result.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluators - get version

```
GET {endpoint}/evaluators/{name}/versions/{version}?api-version=2025-11-15-preview
```


Get the specific version of the EvaluatorVersion. The service returns 404 Not Found error if the EvaluatorVersion does not exist.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The specific version id of the EvaluatorVersion to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluators - delete version

```
DELETE {endpoint}/evaluators/{name}/versions/{version}?api-version=2025-11-15-preview
```


Delete the specific version of the EvaluatorVersion. The service returns 204 No Content if the EvaluatorVersion was deleted successfully or if the EvaluatorVersion does not exist.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The version of the EvaluatorVersion to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 204

**Description**: There is no content to send for this request, but the headers may be useful.

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Evaluators - update version

```
PATCH {endpoint}/evaluators/{name}/versions/{version}?api-version=2025-11-15-preview
```


Update an existing EvaluatorVersion with the given version id

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The version of the EvaluatorVersion to update. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| categories | array | The categories of the evaluator | No | |
| description | string | The asset description text. | No | |
| display_name | string | Display Name for evaluator. It helps to find the evaluator easily in Foundry. It does not need to be unique. | No | |
| metadata | object | Metadata about the evaluator | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Indexes - list latest

```
GET {endpoint}/indexes?api-version=2025-11-15-preview
```


List the latest version of each Index

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Indexes - list versions

```
GET {endpoint}/indexes/{name}/versions?api-version=2025-11-15-preview
```


List all versions of the given Index

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Indexes - get version

```
GET {endpoint}/indexes/{name}/versions/{version}?api-version=2025-11-15-preview
```


Get the specific version of the Index. The service returns 404 Not Found error if the Index does not exist.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The specific version id of the Index to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Indexes - delete version

```
DELETE {endpoint}/indexes/{name}/versions/{version}?api-version=2025-11-15-preview
```


Delete the specific version of the Index. The service returns 204 No Content if the Index was deleted successfully or if the Index does not exist.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The version of the Index to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 204

**Description**: There is no content to send for this request, but the headers may be useful.

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Indexes - create or update version

```
PATCH {endpoint}/indexes/{name}/versions/{version}?api-version=2025-11-15-preview
```


Create a new or update an existing Index with the given version id

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the resource |
| version | path | Yes | string | The specific version id of the Index to create or update. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/merge-patch+json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | The asset description text. | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No | |
| type | object | Yes |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** 201

**Description**: The request has succeeded and a new resource has been created as a result.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Insights - generate

```
POST {endpoint}/insights?api-version=2025-11-15-preview
```


Generate Insights

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| Repeatability-Request-ID | header | No | string | Unique, client-generated identifier for ensuring request idempotency. Use the same ID for retries to prevent duplicate evaluations. |
| Repeatability-First-Sent | header | No | string | Timestamp indicating when this request was first initiated. Used in conjunction with repeatability-request-id for idempotency control. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| displayName | string | User friendly display name for the insight. | Yes | |
| id | string | The unique identifier for the insights report. | Yes | |
| metadata | object | Metadata about the insights. | Yes | |
| └─ completedAt | string | The timestamp when the insights were completed. | No | |
| └─ createdAt | string | The timestamp when the insights were created. | No | |
| request | object | The request of the insights report. | Yes | |
| └─ type |
|

[InsightType](#insighttype)### Responses

**Status Code:** 201

**Description**: The request has succeeded and a new resource has been created as a result.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Insights - list

```
GET {endpoint}/insights?api-version=2025-11-15-preview
```


List all insights in reverse chronological order (newest first).

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| type | query | No | Filter by the type of analysis. | |
| evalId | query | No | string | Filter by the evaluation ID. |
| runId | query | No | string | Filter by the evaluation run ID. |
| agentName | query | No | string | Filter by the agent name. |
| includeCoordinates | query | No | boolean | Whether to include coordinates for visualization in the response. Defaults to false. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Insights - get

```
GET {endpoint}/insights/{id}?api-version=2025-11-15-preview
```


Get a specific insight by Id.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| id | path | Yes | string | The unique identifier for the insights report. |
| includeCoordinates | query | No | boolean | Whether to include coordinates for visualization in the response. Defaults to false. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Create memory store

```
POST {endpoint}/memory_stores?api-version=2025-11-15-preview
```


Create a memory store.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| definition | object | Base definition for memory store configurations. | Yes | |
| └─ kind |
|

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## List memory stores

```
GET {endpoint}/memory_stores?api-version=2025-11-15-preview
```


List all memory stores.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and`desc` for descending order. |
| after | query | No | string | A cursor for use in pagination. `after` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list. |
| before | query | No | string | A cursor for use in pagination. `before` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Update memory store

```
POST {endpoint}/memory_stores/{name}?api-version=2025-11-15-preview
```


Update a memory store.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the memory store to update. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A human-readable description of the memory store. | No | |
| metadata | object | Arbitrary key-value metadata to associate with the memory store. | No |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Get memory store

```
GET {endpoint}/memory_stores/{name}?api-version=2025-11-15-preview
```


Retrieve a memory store.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the memory store to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Delete memory store

```
DELETE {endpoint}/memory_stores/{name}?api-version=2025-11-15-preview
```


Delete a memory store.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the memory store to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Get update result

```
GET {endpoint}/memory_stores/{name}/updates/{update_id}?api-version=2025-11-15-preview
```


Get memory store update result.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the memory store. |
| update_id | path | Yes | string | The ID of the memory update operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Delete scope memories

```
POST {endpoint}/memory_stores/{name}:delete_scope?api-version=2025-11-15-preview
```


Delete all memories associated with a specific scope from a memory store.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the memory store. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| scope | string | The namespace that logically groups and isolates memories to delete, such as a user ID. | Yes |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Search memories

```
POST {endpoint}/memory_stores/{name}:search_memories?api-version=2025-11-15-preview
```


Search for relevant memories from a memory store based on conversation context.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the memory store to search. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| items | array | Items for which to search for relevant memories. | No | |
| options | object | Memory search options. | No | |
| └─ max_memories | integer | Maximum number of memory items to return. | No | |
| previous_search_id | string | The unique ID of the previous search request, enabling incremental memory search from where the last operation left off. | No | |
| scope | string | The namespace that logically groups and isolates memories, such as a user ID. | Yes |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Update memories

```
POST {endpoint}/memory_stores/{name}:update_memories?api-version=2025-11-15-preview
```


Update memory store with conversation memories.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | The name of the memory store to update. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| items | array | Conversation items from which to extract memories. | No | |
| previous_update_id | string | The unique ID of the previous update request, enabling incremental memory updates from where the last operation left off. | No | |
| scope | string | The namespace that logically groups and isolates memories, such as a user ID. | Yes | |
| update_delay | integer | Timeout period before processing the memory update in seconds. If a new update request is received during this period, it will cancel the current request and reset the timeout. Set to 0 to immediately trigger the update without delay. Defaults to 300 (5 minutes). |
No | 300 |

### Responses

**Status Code:** 202

**Description**: The request has been accepted for processing, but processing has not yet completed.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Create conversation

```
POST {endpoint}/openai/conversations?api-version=2025-11-15-preview
```


Create a conversation.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| items | array | Initial items to include the conversation context. You may add up to 20 items at a time. |
No | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## List conversations

```
GET {endpoint}/openai/conversations?api-version=2025-11-15-preview
```


Returns the list of all conversations.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and`desc` for descending order. |
| after | query | No | string | A cursor for use in pagination. `after` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list. |
| before | query | No | string | A cursor for use in pagination. `before` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list. |
| agent_name | query | No | string | Filter by agent name. If provided, only items associated with the specified agent will be returned. |
| agent_id | query | No | string | Filter by agent ID in the format `name:version` . If provided, only items associated with the specified agent ID will be returned. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Update conversation

```
POST {endpoint}/openai/conversations/{conversation_id}?api-version=2025-11-15-preview
```


Update a conversation.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| conversation_id | path | Yes | string | The id of the conversation to update. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Get conversation

```
GET {endpoint}/openai/conversations/{conversation_id}?api-version=2025-11-15-preview
```


Retrieves a conversation.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| conversation_id | path | Yes | string | The id of the conversation to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Delete conversation

```
DELETE {endpoint}/openai/conversations/{conversation_id}?api-version=2025-11-15-preview
```


Deletes a conversation.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| conversation_id | path | Yes | string | The id of the conversation to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Create conversation items

```
POST {endpoint}/openai/conversations/{conversation_id}/items?api-version=2025-11-15-preview
```


Create items in a conversation with the given ID.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| conversation_id | path | Yes | string | The id of the conversation on which the item needs to be created. |
| include | query | No | array | Additional fields to include in the response. See the `include` parameter for listing Conversation items for more information. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| items | array | The items to add to the conversation. You may add up to 20 items at a time. | Yes |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## List conversation items

```
GET {endpoint}/openai/conversations/{conversation_id}/items?api-version=2025-11-15-preview
```


List all items for a conversation with the given ID.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| conversation_id | path | Yes | string | The id of the conversation on which the items needs to be listed. |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and`desc` for descending order. |
| after | query | No | string | A cursor for use in pagination. `after` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list. |
| before | query | No | string | A cursor for use in pagination. `before` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list. |
| item_type | query | No | Filter by item type. If provided, only items of the specified type will be returned. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Get conversation item

```
GET {endpoint}/openai/conversations/{conversation_id}/items/{item_id}?api-version=2025-11-15-preview
```


Get a single item from a conversation with the given IDs.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| conversation_id | path | Yes | string | The ID of the conversation that contains the item. |
| item_id | path | Yes | string | The id of the conversation item to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Delete conversation item

```
DELETE {endpoint}/openai/conversations/{conversation_id}/items/{item_id}?api-version=2025-11-15-preview
```


Delete an item from a conversation with the given IDs.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| conversation_id | path | Yes | string | The id of the conversation on which the item needs to be deleted from. |
| item_id | path | Yes | string | The id of the conversation item to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - list evals

```
GET {endpoint}/openai/evals?api-version=2025-11-15-preview
```


List all evaluations List evaluations for a project.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| after | query | No | string | Identifier for the last run from the previous pagination request. |
| limit | query | No | Number of runs to retrieve. | |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order for runs by timestamp. Use `asc` for ascending order or `desc` for descending order. Defaults to `asc` . |
| order_by | query | No | string Possible values: `created_at` , `updated_at` |
Evals can be ordered by creation time or last updated time. Use`created_at` for creation time or `updated_at` for last updated time. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - create eval

```
POST {endpoint}/openai/evals?api-version=2025-11-15-preview
```


Create evaluation Create the structure of an evaluation that can be used to test a model's performance. An evaluation is a set of testing criteria and the config for a data source, which dictates the schema of the data used in the evaluation. After creating an evaluation, you can run it on different models and model parameters. We support several types of graders and datasources. For more information, see the

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data_source_config | object | A CustomDataSourceConfig object that defines the schema for the data source used for the evaluation runs. This schema is used to define the shape of the data that will be: - Used to define your testing criteria and - What data is required when creating a run |
Yes | |
| └─ include_sample_schema | boolean | Whether the eval should expect you to populate the sample namespace (ie, by generating responses off of your data source) | No | |
| └─ item_schema | object | The json schema for each row in the data source. | No | |
| └─ metadata | object | Metadata filters for the stored completions data source. | No | |
| └─ scenario | enum | Data schema scenario. Possible values: `red_team` , `responses` , `traces` |
No | |
| └─ type | enum | The object type, which is always `label_model` .Possible values: `azure_ai_source` |
No | |
| metadata |
|

useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters.

`{{item.variable_name}}`

. To reference the model's output, use the `sample`

namespace (ie, `{{sample.output_text}}`

).### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - delete eval

```
DELETE {endpoint}/openai/evals/{eval_id}?api-version=2025-11-15-preview
```


Delete an evaluation Delete an evaluation.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | The ID of the evaluation to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - get eval

```
GET {endpoint}/openai/evals/{eval_id}?api-version=2025-11-15-preview
```


Get an evaluation Get an evaluation by ID.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | The ID of the evaluation to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - update eval

```
POST {endpoint}/openai/evals/{eval_id}?api-version=2025-11-15-preview
```


Update an evaluation Update certain properties of an evaluation.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | The ID of the evaluation to update. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| metadata |
|

useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters.

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - list runs

```
GET {endpoint}/openai/evals/{eval_id}/runs?api-version=2025-11-15-preview
```


Get a list of runs for an evaluation Get a list of runs for an evaluation.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | The ID of the evaluation to retrieve runs for. |
| after | query | No | string | Identifier for the last run from the previous pagination request. |
| limit | query | No | Number of runs to retrieve. | |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order for runs by timestamp. Use `asc` for ascending order or `desc` for descending order. Defaults to `asc` . |
| status | query | No | string Possible values: `queued` , `in_progress` , `completed` , `canceled` , `failed` . Filter runs by status. One of `queued` , `in_progress` , `failed` , `completed` , `canceled` . |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - create eval run

```
POST {endpoint}/openai/evals/{eval_id}/runs?api-version=2025-11-15-preview
```


Create evaluation run

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | The ID of the evaluation to create a run for. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data_source | object | A JsonlRunDataSource object with that specifies a JSONL file that matches the eval | Yes | |
| └─ input_messages |
|

`item.input_trajectory`

), or a template with variable references to the `item`

namespace.[RedTeamItemGenerationParams](#redteamitemgenerationparams)[OpenAI.CreateEvalResponsesRunDataSourceSamplingParams](#openaicreateevalresponsesrundatasourcesamplingparams)[OpenAI.EvalJsonlFileContentSource](#openaievaljsonlfilecontentsource)or[OpenAI.EvalJsonlFileIdSource](#openaievaljsonlfileidsource)or[OpenAI.EvalResponsesSource](#openaievalresponsessource)`item`

namespace in this run's data source.[Target](#target)[OpenAI.Metadata](#openaimetadata)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters.

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - delete eval run

```
DELETE {endpoint}/openai/evals/{eval_id}/runs/{run_id}?api-version=2025-11-15-preview
```


Delete evaluation run Delete an eval run.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | The ID of the evaluation to delete the run from. |
| run_id | path | Yes | string | The ID of the run to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - get eval run

```
GET {endpoint}/openai/evals/{eval_id}/runs/{run_id}?api-version=2025-11-15-preview
```


Get an evaluation run Get an evaluation run by ID.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | The ID of the evaluation to retrieve runs for. |
| run_id | path | Yes | string | The ID of the run to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - cancel eval run

```
POST {endpoint}/openai/evals/{eval_id}/runs/{run_id}?api-version=2025-11-15-preview
```


Cancel evaluation run Cancel an ongoing evaluation run.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | The ID of the evaluation whose run you want to cancel. |
| run_id | path | Yes | string | The ID of the run to cancel. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - get eval run output items

```
GET {endpoint}/openai/evals/{eval_id}/runs/{run_id}/output_items?api-version=2025-11-15-preview
```


Get evaluation run output items Get a list of output items for an evaluation run.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | |
| run_id | path | Yes | string | The ID of the run to retrieve output items for. |
| after | query | No | string | Identifier for the last run from the previous pagination request. |
| limit | query | No | Number of runs to retrieve. | |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order for runs by timestamp. Use `asc` for ascending order or `desc` for descending order. Defaults to `asc` . |
| status | query | No | string Possible values: `fail` , `pass` |
Filter output items by status. Use `failed` to filter by failed outputitems or `pass` to filter by passed output items. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## OpenAI evals - get eval run output item

```
GET {endpoint}/openai/evals/{eval_id}/runs/{run_id}/output_items/{output_item_id}?api-version=2025-11-15-preview
```


Get an output item of an evaluation run Get an evaluation run output item by ID.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| eval_id | path | Yes | string | The ID of the evaluation to retrieve runs for. |
| run_id | path | Yes | string | The ID of the run to retrieve. |
| output_item_id | path | Yes | string | The ID of the output item to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Create fine tuning job

```
POST {endpoint}/openai/fine-tuning/jobs?api-version=2025-11-15-preview
```


Creates a fine-tuning job which begins the process of creating a new model from a given dataset.

Response includes details of the enqueued job including job status and the name of the fine-tuned models once complete.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| hyperparameters | object | The hyperparameters used for the fine-tuning job. This value is now deprecated in favor of `method` , and should be passed in under the `method` parameter. |
No | |
| └─ batch_size | enum | Possible values: `auto` |
No | |
| └─ learning_rate_multiplier | enum | Possible values: `auto` |
No | |
| └─ n_epochs | enum | Possible values: `auto` |
No | |
| integrations | array | A list of integrations to enable for your fine-tuning job. | No | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No | |
| method |
|

[supported models](https://platform.openai.com/docs/guides/fine-tuning#which-models-can-be-fine-tuned).If a seed is not specified, one will be generated for you.

For example, a

`suffix`

of "custom-model-name" would produce a model name like `ft:gpt-4o-mini:openai:custom-model-name:7p4lURel`

.Your dataset must be formatted as a JSONL file. Additionally, you must upload your file with the purpose

`fine-tune`

.The contents of the file should differ depending on if the model uses the chat, completions format, or if the fine-tuning method uses the preference format.

See the

[fine-tuning guide](https://platform.openai.com/docs/guides/model-optimization)for more details.If you provide this file, the data is used to generate validation

metrics periodically during fine-tuning. These metrics can be viewed in

the fine-tuning results file.

The same data should not be present in both train and validation files.

Your dataset must be formatted as a JSONL file. You must upload your file with the purpose

`fine-tune`

.See the

[fine-tuning guide](https://platform.openai.com/docs/guides/model-optimization)for more details.### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## List paginated fine tuning jobs

```
GET {endpoint}/openai/fine-tuning/jobs?api-version=2025-11-15-preview
```


List your organization's fine-tuning jobs

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| after | query | No | string | Identifier for the last job from the previous pagination request. |
| limit | query | No | integer | Number of fine-tuning jobs to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Retrieve fine tuning job

```
GET {endpoint}/openai/fine-tuning/jobs/{fine_tuning_job_id}?api-version=2025-11-15-preview
```


Get info about a fine-tuning job.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| fine_tuning_job_id | path | Yes | string | The ID of the fine-tuning job. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Cancel fine tuning job

```
POST {endpoint}/openai/fine-tuning/jobs/{fine_tuning_job_id}/cancel?api-version=2025-11-15-preview
```


Immediately cancel a fine-tune job.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| fine_tuning_job_id | path | Yes | string | The ID of the fine-tuning job to cancel. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## List fine tuning job checkpoints

```
GET {endpoint}/openai/fine-tuning/jobs/{fine_tuning_job_id}/checkpoints?api-version=2025-11-15-preview
```


List checkpoints for a fine-tuning job.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| fine_tuning_job_id | path | Yes | string | The ID of the fine-tuning job to get checkpoints for. |
| after | query | No | string | Identifier for the last checkpoint ID from the previous pagination request. |
| limit | query | No | integer | Number of checkpoints to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## List fine tuning job events

```
GET {endpoint}/openai/fine-tuning/jobs/{fine_tuning_job_id}/events?api-version=2025-11-15-preview
```


Get fine-grained status updates for a fine-tuning job.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| fine_tuning_job_id | path | Yes | string | The ID of the fine-tuning job to get events for. |
| after | query | No | string | Identifier for the last event from the previous pagination request. |
| limit | query | No | integer | Number of events to retrieve. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Pause fine tuning job

```
POST {endpoint}/openai/fine-tuning/jobs/{fine_tuning_job_id}/pause?api-version=2025-11-15-preview
```


Pause a running fine-tune job.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| fine_tuning_job_id | path | Yes | string | The ID of the fine-tuning job to pause. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Resume fine tuning job

```
POST {endpoint}/openai/fine-tuning/jobs/{fine_tuning_job_id}/resume?api-version=2025-11-15-preview
```


Resume a paused fine-tune job.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| fine_tuning_job_id | path | Yes | string | The ID of the fine-tuning job to resume. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Create response - create response stream

```
POST {endpoint}/openai/responses?api-version=2025-11-15-preview
```


Creates a model response. Creates a model response (streaming response).

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | No | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| agent |
|

[Learn more about background responses](https://platform.openai.com/docs/guides/background).supported values are:

-

`code_interpreter_call.outputs`

: Includes the outputs of python code executionin code interpreter tool call items.

-

`computer_call_output.output.image_url`

: Include image urls from the computer call output.-

`file_search_call.results`

: Include the search results ofthe file search tool call.

-

`message.input_image.image_url`

: Include image urls from the input message.-

`message.output_text.logprobs`

: Include logprobs with assistant messages.-

`reasoning.encrypted_content`

: Includes an encrypted version of reasoningtokens in reasoning item outputs. This enables reasoning items to be used in

multi-turn conversations when using the Responses API statelessly (like

when the

`store`

parameter is set to `false`

, or when an organization isenrolled in the zero data retention program).

Learn more:

-

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)-

[Image inputs](https://platform.openai.com/docs/guides/images)-

[File inputs](https://platform.openai.com/docs/guides/pdf-files)-

[Managing conversation state](https://platform.openai.com/docs/guides/conversation-state)-

[Function calling](https://platform.openai.com/docs/guides/function-calling)When using along with

`previous_response_id`

, the instructions from a previousresponse will not be carried over to the next response. This makes it simple

to swap out system (or developer) messages in new responses.

[reasoning tokens](https://platform.openai.com/docs/guides/reasoning).useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

create multi-turn conversations. Learn more about

[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).[OpenAI.Prompt](#openaiprompt)[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).[OpenAI.Reasoning](#openaireasoning)**o-series models only**Configuration options for reasoning models.

[OpenAI.ServiceTier](#openaiservicetier)API.

as it is generated using server-sent events.

for more information.

We generally recommend altering this or

`top_p`

but not both.text or structured JSON data. See

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)and

[Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)[OpenAI.ToolChoiceOptions](#openaitoolchoiceoptions)or[OpenAI.ToolChoiceObject](#openaitoolchoiceobject)a response. See the

`tools`

parameter to see how to specify which toolsthe model can call.

can specify which tool to use by setting the

`tool_choice`

parameter.The two categories of tools you can provide the model are:

-

**Built-in tools**: Tools that are provided by OpenAI that extend themodel's capabilities, like file search.

-

**Function calls (custom tools)**: Functions that are defined by you,enabling the model to call your own code.

where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.-

`auto`

: If the context of this response and previous ones exceedsthe model's context window size, the model will truncate the

response to fit the context window by dropping input items in the

middle of the conversation.

-

`disabled`

(default): If a model response will exceed the context windowsize for a model, the request will fail with a 400 error.

Possible values:

`auto`

, `disabled`

[Learn more about safety best practices](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

[OpenAI.ResponseStreamEvent](#openairesponsestreamevent)**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## List responses

```
GET {endpoint}/openai/responses?api-version=2025-11-15-preview
```


Returns the list of all responses.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and`desc` for descending order. |
| after | query | No | string | A cursor for use in pagination. `after` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list. |
| before | query | No | string | A cursor for use in pagination. `before` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list. |
| agent_name | query | No | string | Filter by agent name. If provided, only items associated with the specified agent will be returned. |
| agent_id | query | No | string | Filter by agent ID in the format `name:version` . If provided, only items associated with the specified agent ID will be returned. |
| conversation_id | query | No | string | Filter by conversation ID. If provided, only responses associated with the specified conversation will be returned. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Get response - get response stream

```
GET {endpoint}/openai/responses/{response_id}?api-version=2025-11-15-preview
```


Retrieves a model response with the given ID. Retrieves a model response with the given ID (streaming response).

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | No | string | The API version to use for this operation. |
| response_id | path | Yes | string | |
| include[] | query | No | array | |
| stream | query | No | boolean | |
| starting_after | query | No | integer | |
| accept | header | No | string Possible values: `text/event-stream` |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

[OpenAI.ResponseStreamEvent](#openairesponsestreamevent)**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Delete response

```
DELETE {endpoint}/openai/responses/{response_id}?api-version=2025-11-15-preview
```


Deletes a model response.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| response_id | path | Yes | string | The ID of the response to delete. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Cancel response

```
POST {endpoint}/openai/responses/{response_id}/cancel?api-version=2025-11-15-preview
```


Cancels a model response.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| response_id | path | Yes | string | The ID of the response to cancel. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## List input items

```
GET {endpoint}/openai/responses/{response_id}/input_items?api-version=2025-11-15-preview
```


Returns a list of input items for a given response.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| response_id | path | Yes | string | |
| limit | query | No | integer | A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 20. |
| order | query | No | string Possible values: `asc` , `desc` |
Sort order by the `created_at` timestamp of the objects. `asc` for ascending order and`desc` for descending order. |
| after | query | No | string | A cursor for use in pagination. `after` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include after=obj_foo in order to fetch the next page of the list. |
| before | query | No | string | A cursor for use in pagination. `before` is an object ID that defines your place in the list.For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include before=obj_foo in order to fetch the previous page of the list. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json | object | The response data for a requested list of items. |

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Redteams - list

```
GET {endpoint}/redTeams/runs?api-version=2025-11-15-preview
```


List a redteam by name.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Redteams - get

```
GET {endpoint}/redTeams/runs/{name}?api-version=2025-11-15-preview
```


Get a redteam by name.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| name | path | Yes | string | Identifier of the red team run. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Redteams - create

```
POST {endpoint}/redTeams/runs:run?api-version=2025-11-15-preview
```


Creates a redteam run.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| applicationScenario | string | Application scenario for the red team operation, to generate scenario specific attacks. | No | |
| attackStrategies | array | List of attack strategies or nested lists of attack strategies. | No | |
| displayName | string | Name of the red-team run. | No | |
| id | string | Identifier of the red team run. | Yes | |
| numTurns | integer | Number of simulation rounds. | No | |
| properties | object | Red team's properties. Unlike tags, properties are add-only. Once added, a property cannot be removed. | No | |
| riskCategories | array | List of risk categories to generate attack objectives for. | No | |
| simulationOnly | boolean | Simulation-only or Simulation + Evaluation. Default false, if true the scan outputs conversation not evaluation result. | No | False |
| status | string | Status of the red-team. It is set by service and is read-only. | No | |
| tags | object | Red team's tags. Unlike properties, tags are fully mutable. | No | |
| target | object | Abstract class for target configuration. | Yes | |
| └─ type | string | Type of the model configuration. | No |

### Responses

**Status Code:** 201

**Description**: The request has succeeded and a new resource has been created as a result.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Schedules - list

```
GET {endpoint}/schedules?api-version=2025-11-15-preview
```


List all schedules.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Schedules - delete

```
DELETE {endpoint}/schedules/{id}?api-version=2025-11-15-preview
```


Delete a schedule.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| id | path | Yes | string | Identifier of the schedule. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 204

**Description**: There is no content to send for this request, but the headers may be useful.

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Schedules - get

```
GET {endpoint}/schedules/{id}?api-version=2025-11-15-preview
```


Get a schedule by id.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| id | path | Yes | string | Identifier of the schedule. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Schedules - create or update

```
PUT {endpoint}/schedules/{id}?api-version=2025-11-15-preview
```


Create or update a schedule by id.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| id | path | Yes | string | Identifier of the schedule. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Request Body

**Content-Type**: application/json

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | Description of the schedule. | No | |
| displayName | string | Name of the schedule. | No | |
| enabled | boolean | Enabled status of the schedule. | Yes | |
| id | string | Identifier of the schedule. | Yes | |
| properties | object | Schedule's properties. Unlike tags, properties are add-only. Once added, a property cannot be removed. | No | |
| provisioningStatus | object | Schedule provisioning status. | No | |
| systemData | object | System metadata for the resource. | Yes | |
| tags | object | Schedule's tags. Unlike properties, tags are fully mutable. | No | |
| task | object | Schedule task model. | Yes | |
| └─ configuration | object | Configuration for the task. | No | |
| └─ type |
|

[TriggerType](#triggertype)### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** 201

**Description**: The request has succeeded and a new resource has been created as a result.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Schedules - list runs

```
GET {endpoint}/schedules/{id}/runs?api-version=2025-11-15-preview
```


List all schedule runs.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| id | path | Yes | string | Identifier of the schedule. |
| x-ms-client-request-id | header | No | An opaque, globally-unique, client-generated string identifier for the request. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Schedules - get run

```
GET {endpoint}/schedules/{scheduleId}/runs/{runId}?api-version=2025-11-15-preview
```


Get a schedule run by id.

### URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| endpoint | path | Yes | string url |
Foundry Project endpoint in the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/{project-name}` . If you only have one Project in your Foundry Hub, or to target the default Project in your Hub, use the form `https://{ai-services-account-name}.services.ai.azure.com/api/projects/_project` |
| api-version | query | Yes | string | The API version to use for this operation. |
| scheduleId | path | Yes | string | Identifier of the schedule. |
| runId | path | Yes | string | Identifier of the schedule run. |

### Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| Authorization | True | string | Example: `Authorization: Bearer {Azure_AI_Foundry_Project_Auth_Token}` To generate an auth token using Azure CLI: `az account get-access-token --resource https://ai.azure.com/` Type: oauth2 Authorization Url: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize` scope: `https://ai.azure.com/.default` |

### Responses

**Status Code:** 200

**Description**: The request has succeeded.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

**Status Code:** default

**Description**: An unexpected error response.

Content-Type |
Type |
Description |
|---|---|---|
| application/json |
|

## Components

### A2ATool

An agent implementing the A2A protocol.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| agent_card_path | string | The path to the agent card relative to the `base_url` .If not provided, defaults to `/.well-known/agent-card.json` |
No | |
| base_url | string | Base URL of the agent. | No | |
| project_connection_id | string | The connection ID in the project for the A2A server. The connection stores authentication and other connection details needed to connect to the A2A server. |
No | |
| type | enum | The type of the tool. Always `a2a` .Possible values: `a2a_preview` |
Yes |

### AISearchIndexResource

A AI Search Index resource.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| filter | string | filter string for search resource.
|

### AgentClusterInsightResult

Insights from the agent cluster analysis.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| clusterInsight |
|

Possible values:

`AgentClusterInsight`

### AgentClusterInsightsRequest

Insights on set of Agent Evaluation Results

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| agentName | string | Identifier for the agent. | Yes | |
| modelConfiguration | object | Configuration of the model used in the insight generation. | No | |
| └─ modelDeploymentName | string | The model deployment to be evaluated. Accepts either the deployment name alone or with the connection name as `{connectionName}/<modelDeploymentName>` . |
No | |
| type | enum | The type of request. Possible values: `AgentClusterInsight` |
Yes |

### AgentContainerObject

The details of the container of a specific version of an agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | string | The creation time of the container. | Yes | |
| error_message | string | The error message if the container failed to operate, if any. | No | |
| max_replicas | integer | The maximum number of replicas for the container. Default is 1. | No | |
| min_replicas | integer | The minimum number of replicas for the container. Default is 1. | No | |
| object | enum | The object type, which is always 'agent.container'. Possible values: `agent.container` |
Yes | |
| status | object | Status of the container of a specific version of an agent. | Yes | |
| updated_at | string | The last update time of the container. | Yes |

### AgentContainerOperationError

The error details of the container operation, if any.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code | string | The error code of the container operation, if any. | Yes | |
| message | string | The error message of the container operation, if any. | Yes | |
| type | string | The error type of the container operation, if any. | Yes |

### AgentContainerOperationObject

The container operation for a specific version of an agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| agent_id | string | The ID of the agent. | Yes | |
| agent_version_id | string | The ID of the agent version. | Yes | |
| container | object | The details of the container of a specific version of an agent. | No | |
| └─ created_at | string | The creation time of the container. | No | |
| └─ error_message | string | The error message if the container failed to operate, if any. | No | |
| └─ max_replicas | integer | The maximum number of replicas for the container. Default is 1. | No | |
| └─ min_replicas | integer | The minimum number of replicas for the container. Default is 1. | No | |
| └─ object | enum | The object type, which is always 'agent.container'. Possible values: `agent.container` |
No | |
| └─ status |
|

### AgentContainerOperationStatus

Status of the container operation for a specific version of an agent.

| Property | Value |
|---|---|
Description |
Status of the container operation for a specific version of an agent. |
Type |
string |
Values |
`NotStarted` `InProgress` `Succeeded` `Failed` |

### AgentContainerStatus

Status of the container of a specific version of an agent.

| Property | Value |
|---|---|
Description |
Status of the container of a specific version of an agent. |
Type |
string |
Values |
`Starting` `Running` `Stopping` `Stopped` `Failed` `Deleting` `Deleted` `Updating` |

### AgentDefinition

### Discriminator for AgentDefinition

This component uses the property `kind`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`workflow` |
|

`hosted`

[HostedAgentDefinition](#hostedagentdefinition)`container_app`

[ContainerAppAgentDefinition](#containerappagentdefinition)`prompt`

[PromptAgentDefinition](#promptagentdefinition)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| kind |
|

### AgentId

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| name | string | The name of the agent. | Yes | |
| type | enum | Possible values: `agent_id` |
Yes | |
| version | string | The version identifier of the agent. | Yes |

### AgentKind

| Property | Value |
|---|---|
Type |
string |
Values |
`prompt` `hosted` `container_app` `workflow` |

### AgentObject

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| id | string | The unique identifier of the agent. | Yes | |
| name | string | The name of the agent. | Yes | |
| object | enum | The object type, which is always 'agent'. Possible values: `agent` |
Yes | |
| versions | object | The latest version of the agent. | Yes | |
| └─ latest |
|

### AgentProtocol

| Property | Value |
|---|---|
Type |
string |
Values |
`activity_protocol` `responses` |

### AgentReference

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| name | string | The name of the agent. | Yes | |
| type | enum | Possible values: `agent_reference` |
Yes | |
| version | string | The version identifier of the agent. | No |

### AgentTaxonomyInput

Input configuration for the evaluation taxonomy when the input type is agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| riskCategories | array | List of risk categories to evaluate against. | Yes | |
| target | object | Represents a target specifying an Azure AI agent. | Yes | |
| └─ name | string | The unique identifier of the Azure AI agent. | No | |
| └─ tool_descriptions | array | The parameters used to control the sampling behavior of the agent during text generation. | No | |
| └─ type | enum | The type of target, always `azure_ai_agent` .Possible values: `azure_ai_agent` |
No | |
| └─ version | string | The version of the Azure AI agent. | No | |
| type | enum | Input type of the evaluation taxonomy. Possible values: `agent` |
Yes |

### AgentTaxonomyInputUpdate

Input configuration for the evaluation taxonomy when the input type is agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| riskCategories | array | List of risk categories to evaluate against. | No | |
| target | object | Represents a target specifying an Azure AI agent. | No | |
| └─ name | string | The unique identifier of the Azure AI agent. | No | |
| └─ tool_descriptions | array | The parameters used to control the sampling behavior of the agent during text generation. | No | |
| └─ type | enum | The type of target, always `azure_ai_agent` .Possible values: `azure_ai_agent` |
No | |
| └─ version | string | The version of the Azure AI agent. | No | |
| type | enum | Input type of the evaluation taxonomy. Possible values: `agent` |
No |

### AgentVersionObject

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | integer | The Unix timestamp (seconds) when the agent was created. | Yes | |
| definition |
|

useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

Possible values:

`agent.version`

### AgenticIdentityCredentials

Agentic identity credential definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The credential type Possible values: `AgenticIdentityToken` |
Yes |

### ApiErrorResponse

Error response for API failures.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| error |
|

### ApiKeyCredentials

API Key Credential definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| key | string | API Key | No | |
| type | enum | The credential type Possible values: `ApiKey` |
Yes |

### AssetCredentialResponse

Represents a reference to a blob for consumption

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| blobReference | object | Blob reference details. | Yes | |
| └─ blobUri | string | Blob URI path for client to upload data. Example: `https://blob.windows.core.net/Container/Path` |
No | |
| └─ credential |
|

### AssetId

Identifier of a saved asset.

**Type**: string

### AttackStrategy

Strategies for attacks.

| Property | Value |
|---|---|
Description |
Strategies for attacks. |
Type |
string |
Values |
`easy` `moderate` `difficult` `ascii_art` `ascii_smuggler` `atbash` `base64` `binary` `caesar` `character_space` `jailbreak` `ansii_attack` `character_swap` `suffix_append` `string_join` `unicode_confusable` `unicode_substitution` `diacritic` `flip` `leetspeak` `rot13` `morse` `url` `baseline` `indirect_jailbreak` `tense` `multi_turn` `crescendo` |

### Azure.Core.Foundations.Error

The error object.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code | string | One of a server-defined set of error codes. | Yes | |
| details | array | An array of details about specific errors that led to this reported error. | No | |
| innererror | object | An object containing more specific information about the error. As per Azure REST API guidelines -
|

[Azure.Core.Foundations.InnerError](#azurecorefoundationsinnererror)### Azure.Core.Foundations.ErrorResponse

A response containing error details.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| error | object | The error object. | Yes | |
| └─ code | string | One of a server-defined set of error codes. | No | |
| └─ details | array | An array of details about specific errors that led to this reported error. | No | |
| └─ innererror |
|

### Azure.Core.Foundations.InnerError

An object containing more specific information about the error. As per Azure REST API guidelines - [https://aka.ms/AzureRestApiGuidelines#handling-errors](https://aka.ms/AzureRestApiGuidelines#handling-errors).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code | string | One of a server-defined set of error codes. | No | |
| innererror | object | An object containing more specific information about the error. As per Azure REST API guidelines -
|

[Azure.Core.Foundations.InnerError](#azurecorefoundationsinnererror)### Azure.Core.Foundations.OperationState

Enum describing allowed operation states.

| Property | Value |
|---|---|
Type |
string |
Values |
`NotStarted` `Running` `Succeeded` `Failed` `Canceled` |

### Azure.Core.uuid

Universally Unique Identifier

**Type**: string

**Format**: uuid

### AzureAIAgentTarget

Represents a target specifying an Azure AI agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| name | string | The unique identifier of the Azure AI agent. | Yes | |
| tool_descriptions | array | The parameters used to control the sampling behavior of the agent during text generation. | No | |
| type | enum | The type of target, always `azure_ai_agent` .Possible values: `azure_ai_agent` |
Yes | |
| version | string | The version of the Azure AI agent. | No |

### AzureAIAgentTargetUpdate

Represents a target specifying an Azure AI agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| name | string | The unique identifier of the Azure AI agent. | No | |
| tool_descriptions | array | The parameters used to control the sampling behavior of the agent during text generation. | No | |
| type | enum | The type of target, always `azure_ai_agent` .Possible values: `azure_ai_agent` |
No | |
| version | string | The version of the Azure AI agent. | No |

### AzureAIAssistantTarget

Represents a target specifying an Azure AI Assistant (Agent V1) endpoint, including its id.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| id | string | The unique identifier of the Azure AI Assistant. | No | |
| tool_descriptions | array | The descriptions of tools available to the assistant. | Yes | |
| type | enum | The type of target, always `azure_ai_assistant` .Possible values: `azure_ai_assistant` |
Yes |

### AzureAIAssistantTargetUpdate

Represents a target specifying an Azure AI Assistant (Agent V1) endpoint, including its id.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| id | string | The unique identifier of the Azure AI Assistant. | No | |
| tool_descriptions | array | The descriptions of tools available to the assistant. | No | |
| type | enum | The type of target, always `azure_ai_assistant` .Possible values: `azure_ai_assistant` |
No |

### AzureAIEvaluator

Azure AI Evaluator definition for foundry evaluators.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data_mapping | object | The model to use for the evaluation. Must support structured outputs. | No | |
| evaluator_name | string | The name of the evaluator. | Yes | |
| evaluator_version | string | The version of the evaluator. | No | |
| initialization_parameters | object | The initialization parameters for the evaluation. Must support structured outputs. | No | |
| name | string | The name of the grader. | Yes | |
| type | enum | The object type, which is always `label_model` .Possible values: `azure_ai_evaluator` |
Yes |

### AzureAIModelTarget

Represents a target specifying an Azure AI model for operations requiring model selection.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| model | string | The unique identifier of the Azure AI model. | No | |
| sampling_params | object | Represents a set of parameters used to control the sampling behavior of a language model during text generation. | No | |
| └─ max_completion_tokens | integer | The maximum number of tokens allowed in the completion. | No | |
| └─ seed | integer | The random seed for reproducibility. | No | |
| └─ temperature | number | The temperature parameter for sampling. | No | |
| └─ top_p | number | The top-p parameter for nucleus sampling. | No | |
| type | enum | The type of target, always `azure_ai_model` .Possible values: `azure_ai_model` |
Yes |

### AzureAIModelTargetUpdate

Represents a target specifying an Azure AI model for operations requiring model selection.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| model | string | The unique identifier of the Azure AI model. | No | |
| sampling_params | object | Represents a set of parameters used to control the sampling behavior of a language model during text generation. | No | |
| └─ max_completion_tokens | integer | The maximum number of tokens allowed in the completion. | No | |
| └─ seed | integer | The random seed for reproducibility. | No | |
| └─ temperature | number | The temperature parameter for sampling. | No | |
| └─ top_p | number | The top-p parameter for nucleus sampling. | No | |
| type | enum | The type of target, always `azure_ai_model` .Possible values: `azure_ai_model` |
No |

### AzureAIRedTeam

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_generation_params | object | Represents the parameters for red team item generation. | Yes | |
| └─ attack_strategies | array | The collection of attack strategies to be used. | No | |
| └─ num_turns | integer | The number of turns allowed in the game. | No | |
| └─ type | enum | The type of item generation parameters, always `red_team` .Possible values: `red_team` |
No | |
| target | object | Base class for targets with discriminator support. | Yes | |
| └─ type | string | The type of target. | No | |
| type | enum | The type of data source. Always `azure_ai_red_team` .Possible values: `azure_ai_red_team` |
Yes |

### AzureAIResponses

Represents a data source for evaluation runs that are specific to Continuous Evaluation scenarios.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| event_configuration_id | string | The event configuration name associated with this evaluation run. | Yes | |
| item_generation_params | object | Represents the parameters for continuous evaluation item generation. | Yes | |
| └─ data_mapping | object | Mapping from source fields to response_id field, required for retrieving chat history. | No | |
| └─ max_num_turns | integer | The maximum number of turns of chat history to evaluate. | No | |
| └─ source |
|

`ResponseRetrieval`

.Possible values:

`response_retrieval`

`AzureAIResponses`

.Possible values:

`azure_ai_responses`

### AzureAISearchAgentTool

The input definition information for an Azure AI search tool as used to configure an agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| azure_ai_search | object | A set of index resources used by the `azure_ai_search` tool. |
Yes | |
| └─ indexes | array | The indices attached to this agent. There can be a maximum of 1 index resource attached to the agent. |
No | |
| type | enum | The object type, which is always 'azure_ai_search'. Possible values: `azure_ai_search` |
Yes |

### AzureAISearchIndex

Azure AI Search Index Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Type of index Possible values: `AzureSearch` |
Yes |

### AzureAISearchIndexUpdate

Azure AI Search Index Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Type of index Possible values: `AzureSearch` |
Yes |

### AzureAISearchQueryType

Available query types for Azure AI Search tool.

| Property | Value |
|---|---|
Description |
Available query types for Azure AI Search tool. |
Type |
string |
Values |
`simple` `semantic` `vector` `vector_simple_hybrid` `vector_semantic_hybrid` |

### AzureAISearchToolResource

A set of index resources used by the `azure_ai_search`

tool.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| indexes | array | The indices attached to this agent. There can be a maximum of 1 index resource attached to the agent. |
Yes |

### AzureAISource

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| scenario | enum | Data schema scenario. Possible values: `red_team` , `responses` , `traces` |
Yes | |
| type | enum | The object type, which is always `label_model` .Possible values: `azure_ai_source` |
Yes |

### AzureFunctionAgentTool

The input definition information for an Azure Function Tool, as used to configure an Agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| azure_function | object | The definition of Azure function. | Yes | |
| └─ function | object | The definition of azure function and its parameters. | No | |
| └─ description | string | A description of what the function does, used by the model to choose when and how to call the function. | No | |
| └─ name | string | The name of the function to be called. | No | |
| └─ parameters | The parameters the functions accepts, described as a JSON Schema object. | No | ||
| └─ input_binding |
|

[AzureFunctionBinding](#azurefunctionbinding)Possible values:

`azure_function`

### AzureFunctionBinding

The structure for keeping storage queue name and URI.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| storage_queue | object | The structure for keeping storage queue name and URI. | Yes | |
| └─ queue_name | string | The name of an Azure function storage queue. | No | |
| └─ queue_service_endpoint | string | URI to the Azure Storage Queue service allowing you to manipulate a queue. | No | |
| type | enum | The type of binding, which is always 'storage_queue'. Possible values: `storage_queue` |
Yes |

### AzureFunctionDefinition

The definition of Azure function.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| function | object | The definition of azure function and its parameters. | Yes | |
| └─ description | string | A description of what the function does, used by the model to choose when and how to call the function. | No | |
| └─ name | string | The name of the function to be called. | No | |
| └─ parameters | The parameters the functions accepts, described as a JSON Schema object. | No | ||
| input_binding | object | The structure for keeping storage queue name and URI. | Yes | |
| └─ storage_queue |
|

Possible values:

`storage_queue`

[AzureFunctionStorageQueue](#azurefunctionstoragequeue)Possible values:

`storage_queue`

### AzureFunctionStorageQueue

The structure for keeping storage queue name and URI.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| queue_name | string | The name of an Azure function storage queue. | Yes | |
| queue_service_endpoint | string | URI to the Azure Storage Queue service allowing you to manipulate a queue. | Yes |

### AzureOpenAIModelConfiguration

Azure OpenAI model configuration. The API version would be selected by the service for querying the model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| modelDeploymentName | string | Deployment name for AOAI model. Example: gpt-4o if in AIServices or connection based `connection_name/deployment_name` (e.g. `my-aoai-connection/gpt-4o` ). |
Yes | |
| type | enum | Possible values: `AzureOpenAIModel` |
Yes |

### BaseCredentials

A base class for connection credentials

### Discriminator for BaseCredentials

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`ApiKey` |
|

`AAD`

[EntraIDCredentials](#entraidcredentials)`CustomKeys`

[CustomCredential](#customcredential)`SAS`

[SASCredentials](#sascredentials)`None`

[NoAuthenticationCredentials](#noauthenticationcredentials)`AgenticIdentityToken`

[AgenticIdentityCredentials](#agenticidentitycredentials)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | object | The credential type used by the connection | Yes |

### BingCustomSearchAgentTool

The input definition information for a Bing custom search tool as used to configure an agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| bing_custom_search_preview | object | The bing custom search tool parameters. | Yes | |
| └─ search_configurations | array | The project connections attached to this tool. There can be a maximum of 1 connection resource attached to the tool. |
No | |
| type | enum | The object type, which is always 'bing_custom_search'. Possible values: `bing_custom_search_preview` |
Yes |

### BingCustomSearchConfiguration

A bing custom search configuration.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| count | integer | The number of search results to return in the bing api response | No | |
| freshness | string | Filter search results by a specific time range. See
|

### BingCustomSearchToolParameters

The bing custom search tool parameters.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| search_configurations | array | The project connections attached to this tool. There can be a maximum of 1 connection resource attached to the tool. |
Yes |

### BingGroundingAgentTool

The input definition information for a bing grounding search tool as used to configure an agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| bing_grounding | object | The bing grounding search tool parameters. | Yes | |
| └─ search_configurations | array | The search configurations attached to this tool. There can be a maximum of 1 search configuration resource attached to the tool. |
No | |
| type | enum | The object type, which is always 'bing_grounding'. Possible values: `bing_grounding` |
Yes |

### BingGroundingSearchConfiguration

Search configuration for Bing Grounding

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| count | integer | The number of search results to return in the bing api response | No | |
| freshness | string | Filter search results by a specific time range. See
|

### BingGroundingSearchToolParameters

The bing grounding search tool parameters.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| search_configurations | array | The search configurations attached to this tool. There can be a maximum of 1 search configuration resource attached to the tool. |
Yes |

### BlobReference

Blob reference details.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| blobUri | string | Blob URI path for client to upload data. Example: `https://blob.windows.core.net/Container/Path` |
Yes | |
| credential | object | SAS Credential definition | Yes | |
| └─ sasUri | string | SAS uri | No | |
| └─ type | enum | Type of credential Possible values: `SAS` |
No | |
| storageAccountArmId | string | ARM ID of the storage account to use. | Yes |

### BrowserAutomationAgentTool

The input definition information for a Browser Automation Tool, as used to configure an Agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| browser_automation_preview | object | Definition of input parameters for the Browser Automation Tool. | Yes | |
| └─ connection |
|

Possible values:

`browser_automation_preview`

### BrowserAutomationToolConnectionParameters

Definition of input parameters for the connection used by the Browser Automation Tool.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| project_connection_id | string | The ID of the project connection to your Azure Playwright resource. | Yes |

### BrowserAutomationToolParameters

Definition of input parameters for the Browser Automation Tool.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| connection | object | Definition of input parameters for the connection used by the Browser Automation Tool. | Yes | |
| └─ project_connection_id | string | The ID of the project connection to your Azure Playwright resource. | No |

### CaptureStructuredOutputsTool

A tool for capturing structured outputs

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| outputs | object | A structured output that can be produced by the agent. | Yes | |
| └─ description | string | A description of the output to emit. Used by the model to determine when to emit the output. | No | |
| └─ name | string | The name of the structured output. | No | |
| └─ schema | The JSON schema for the structured output. | No | ||
| └─ strict | boolean | Whether to enforce strict validation. Default `true` . |
No | |
| type | enum | The type of the tool. Always `capture_structured_outputs` .Possible values: `capture_structured_outputs` |
Yes |

### ChartCoordinate

Coordinates for the analysis chart.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| size | integer | Size of the chart element. | Yes | |
| x | integer | X-axis coordinate. | Yes | |
| y | integer | Y-axis coordinate. | Yes |

### ChatSummaryMemoryItem

A memory item containing a summary extracted from conversations.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| kind | enum | The kind of the memory item. Possible values: `chat_summary` |
Yes |

### ClusterInsightResult

Insights from the cluster analysis.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| clusters | array | List of clusters identified in the insights. | Yes | |
| coordinates | object | Optional mapping of IDs to 2D coordinates used by the UX for visualization. The map keys are string identifiers (for example, a cluster id or a sample id) and the values are the coordinates and visual size for rendering on a 2D chart. This property is omitted unless the client requests coordinates (for example, by passing `includeCoordinates=true` as a query parameter).Example: `<br> {<br> "cluster-1": { "x": 12, "y": 34, "size": 8 },<br> "sample-123": { "x": 18, "y": 22, "size": 4 }<br> }<br> ` Coordinates are intended only for client-side visualization and do not modify the canonical insights results. |
No | |
| summary | object | Summary of the error cluster analysis. | Yes | |
| └─ method | string | Method used for clustering. | No | |
| └─ sampleCount | integer | Total number of samples analyzed. | No | |
| └─ uniqueClusterCount | integer | Total number of unique clusters. | No | |
| └─ uniqueSubclusterCount | integer | Total number of unique subcluster labels. | No | |
| └─ usage |
|

### ClusterTokenUsage

Token usage for cluster analysis

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| inputTokenUsage | integer | input token usage | Yes | |
| outputTokenUsage | integer | output token usage | Yes | |
| totalTokenUsage | integer | total token usage | Yes |

### CodeBasedEvaluatorDefinition

Code-based evaluator definition using python code

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code_text | string | Inline code text for the evaluator | Yes | |
| type | enum | Possible values: `code` |
Yes |

### Connection

Response from the list and get connections operations

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| credentials | object | A base class for connection credentials | Yes | |
| └─ type |
|

### ConnectionType

The Type (or category) of the connection

| Property | Value |
|---|---|
Description |
The Type (or category) of the connection |
Type |
string |
Values |
`AzureOpenAI` `AzureBlob` `AzureStorageAccount` `CognitiveSearch` `CosmosDB` `ApiKey` `AppConfig` `AppInsights` `CustomKeys` `RemoteTool` |

### ContainerAppAgentDefinition

The container app agent definition.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| container_app_resource_id | string | The resource ID of the Azure Container App that hosts this agent. Not mutable across versions. | Yes | |
| container_protocol_versions | array | The protocols that the agent supports for ingress communication of the containers. | Yes | |
| ingress_subdomain_suffix | string | The suffix to apply to the app subdomain when sending ingress to the agent. This can be a label (e.g., '---current'), a specific revision (e.g., '--0000001'), or empty to use the default endpoint for the container app. | Yes | |
| kind | enum | Possible values: `container_app` |
Yes |

### ContinuousEvalItemGenerationParams

Represents the parameters for continuous evaluation item generation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data_mapping | object | Mapping from source fields to response_id field, required for retrieving chat history. | Yes | |
| max_num_turns | integer | The maximum number of turns of chat history to evaluate. | Yes | |
| source | object | Yes | ||
| └─ content | array | The content of the jsonl file. | No | |
| └─ id | string | The identifier of the file. | No | |
| └─ type | enum | The type of jsonl source. Always `file_id` .Possible values: `file_id` |
No | |
| type | enum | The type of item generation parameters, always `ResponseRetrieval` .Possible values: `response_retrieval` |
Yes |

### ContinuousEvaluationRuleAction

Evaluation rule action for continuous evaluation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| evalId | string | Eval Id to add continuous evaluation runs to. | Yes | |
| maxHourlyRuns | integer | Maximum number of evaluation runs allowed per hour. | No | |
| type | enum | Possible values: `continuousEvaluation` |
Yes |

### CosmosDBIndex

CosmosDB Vector Store Index Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Type of index Possible values: `CosmosDBNoSqlVectorStore` |
Yes |

### CosmosDBIndexUpdate

CosmosDB Vector Store Index Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Type of index Possible values: `CosmosDBNoSqlVectorStore` |
Yes |

### CreateAgentFromManifestRequest

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A human-readable description of the agent. | No | |
| manifest_id | string | The manifest ID to import the agent version from. | Yes | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No | |
| name | string | The unique name that identifies the agent. Name can be used to retrieve/update/delete the agent. - Must start and end with alphanumeric characters, - Can contain hyphens in the middle - Must not exceed 63 characters. |
Yes | |
| parameter_values | object | The inputs to the manifest that will result in a fully materialized Agent. | Yes |

### CreateAgentRequest

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| definition | object | Yes | ||
| └─ kind |
|

[RaiConfig](#raiconfig)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

- Must start and end with alphanumeric characters,

- Can contain hyphens in the middle

- Must not exceed 63 characters.

### CreateAgentVersionFromManifestRequest

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A human-readable description of the agent. | No | |
| manifest_id | string | The manifest ID to import the agent version from. | Yes | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No | |
| parameter_values | object | The inputs to the manifest that will result in a fully materialized Agent. | Yes |

### CreateAgentVersionRequest

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| definition | object | Yes | ||
| └─ kind |
|

[RaiConfig](#raiconfig)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

### CreateEvalRequest

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data_source_config | object | A CustomDataSourceConfig object that defines the schema for the data source used for the evaluation runs. This schema is used to define the shape of the data that will be: - Used to define your testing criteria and - What data is required when creating a run |
Yes | |
| └─ include_sample_schema | boolean | Whether the eval should expect you to populate the sample namespace (ie, by generating responses off of your data source) | No | |
| └─ item_schema | object | The json schema for each row in the data source. | No | |
| └─ metadata | object | Metadata filters for the stored completions data source. | No | |
| └─ scenario | enum | Data schema scenario. Possible values: `red_team` , `responses` , `traces` |
No | |
| └─ type | enum | The object type, which is always `label_model` .Possible values: `azure_ai_source` |
No | |
| metadata |
|

useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters.

`{{item.variable_name}}`

. To reference the model's output, use the `sample`

namespace (ie, `{{sample.output_text}}`

).### CreateEvalRunRequest

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data_source | object | A JsonlRunDataSource object with that specifies a JSONL file that matches the eval | Yes | |
| └─ input_messages |
|

`item.input_trajectory`

), or a template with variable references to the `item`

namespace.[RedTeamItemGenerationParams](#redteamitemgenerationparams)[OpenAI.CreateEvalResponsesRunDataSourceSamplingParams](#openaicreateevalresponsesrundatasourcesamplingparams)[OpenAI.EvalJsonlFileContentSource](#openaievaljsonlfilecontentsource)or[OpenAI.EvalJsonlFileIdSource](#openaievaljsonlfileidsource)or[OpenAI.EvalResponsesSource](#openaievalresponsessource)`item`

namespace in this run's data source.[Target](#target)[OpenAI.Metadata](#openaimetadata)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters.

### CreatedBy

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| agent | object | No | ||
| └─ name | string | The name of the agent. | No | |
| └─ type | enum | Possible values: `agent_id` |
No | |
| └─ version | string | The version identifier of the agent. | No | |
| response_id | string | The response on which the item is created. | No |

### CredentialType

The credential type used by the connection

| Property | Value |
|---|---|
Description |
The credential type used by the connection |
Type |
string |
Values |
`ApiKey` `AAD` `SAS` `CustomKeys` `None` `AgenticIdentityToken` |

### CronTrigger

Cron based trigger.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| endTime | string | End time for the cron schedule in ISO 8601 format. | No | |
| expression | string | Cron expression that defines the schedule frequency. | Yes | |
| startTime | string | Start time for the cron schedule in ISO 8601 format. | No | |
| timeZone | string | Time zone for the cron schedule. | No | UTC |
| type | enum | Possible values: `Cron` |
Yes |

### CustomCredential

Custom credential definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The credential type Possible values: `CustomKeys` |
Yes |

### DailyRecurrenceSchedule

Daily recurrence schedule.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| hours | array | Hours for the recurrence schedule. | Yes | |
| type | enum | Daily recurrence type. Possible values: `Daily` |
Yes |

### DatasetType

Enum to determine the type of data.

| Property | Value |
|---|---|
Description |
Enum to determine the type of data. |
Type |
string |
Values |
`uri_file` `uri_folder` |

### DatasetVersion

DatasetVersion Definition

### Discriminator for DatasetVersion

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`uri_file` |
|

`uri_folder`

[FolderDatasetVersion](#folderdatasetversion)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| connectionName | string | The Azure Storage Account connection name. Required if startPendingUploadVersion was not called before creating the Dataset | No | |
| dataUri | string | URI of the data (
|

### DatasetVersionUpdate

DatasetVersion Definition

### Discriminator for DatasetVersionUpdate

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`uri_file` |
|

`uri_folder`

[FolderDatasetVersionUpdate](#folderdatasetversionupdate)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | The asset description text. | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No | |
| type | object | Enum to determine the type of data. | Yes |

### DayOfWeek

Days of the week for recurrence schedule.

| Property | Value |
|---|---|
Description |
Days of the week for recurrence schedule. |
Type |
string |
Values |
`Sunday` `Monday` `Tuesday` `Wednesday` `Thursday` `Friday` `Saturday` |

### DeleteAgentResponse

A deleted agent Object

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| deleted | boolean | Whether the agent was successfully deleted. | Yes | |
| name | string | The name of the agent. | Yes | |
| object | enum | The object type. Always 'agent.deleted'. Possible values: `agent.deleted` |
Yes |

### DeleteAgentVersionResponse

A deleted agent version Object

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| deleted | boolean | Whether the agent was successfully deleted. | Yes | |
| name | string | The name of the agent. | Yes | |
| object | enum | The object type. Always 'agent.deleted'. Possible values: `agent.version.deleted` |
Yes | |
| version | string | The version identifier of the agent. | Yes |

### DeleteEvalResponse

A deleted evaluation Object

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| deleted | boolean | Whether the eval was successfully deleted. | Yes | |
| eval_id | string | id of the eval. | Yes | |
| object | enum | The object type. Always 'eval.deleted'. Possible values: `eval.deleted` |
Yes |

### DeleteEvalRunResponse

A deleted evaluation run Object.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| deleted | boolean | Whether the eval was successfully deleted. | No | |
| object | enum | The object type. Always 'eval.deleted'. Possible values: `eval.deleted` |
No | |
| run_id | string | id of the eval. | No |

### DeleteMemoryStoreResponse

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| deleted | boolean | Whether the memory store was successfully deleted. | Yes | |
| name | string | The name of the memory store. | Yes | |
| object | enum | The object type. Always 'memory_store.deleted'. Possible values: `memory_store.deleted` |
Yes |

### DeleteResponseResult

The result of a delete response operation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| deleted | enum | Always return true Possible values: `True` |
Yes | |
| id | string | The operation ID. | Yes | |
| object | enum | Always return 'response'. Possible values: `response` |
Yes |

### Deployment

Model Deployment Definition

### Discriminator for Deployment

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`ModelDeployment` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| name | string | Name of the deployment | Yes | |
| type | object | Yes |

### DeploymentType

| Property | Value |
|---|---|
Type |
string |
Values |
`ModelDeployment` |

### EntraIDCredentials

Entra ID credential definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The credential type Possible values: `AAD` |
Yes |

### Eval

An Eval object with a data source config and testing criteria. An Eval represents a task to be done for your LLM integration. Like:

- Improve the quality of my chatbot
- See how well my chatbot handles customer support
- Check if o4-mini is better at my usecase than gpt-4o

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | object | Yes | ||
| created_by | string | the name of the person who created the run. | No | |
| data_source_config | object | A CustomDataSourceConfig object that defines the schema for the data source used for the evaluation runs. This schema is used to define the shape of the data that will be: - Used to define your testing criteria and - What data is required when creating a run |
Yes | |
| └─ include_sample_schema | boolean | Whether the eval should expect you to populate the sample namespace (ie, by generating responses off of your data source) | No | |
| └─ item_schema | object | The json schema for each row in the data source. | No | |
| └─ metadata | object | Metadata filters for the stored completions data source. | No | |
| └─ scenario | enum | Data schema scenario. Possible values: `red_team` , `responses` , `traces` |
No | |
| └─ type | enum | The object type, which is always `label_model` .Possible values: `azure_ai_source` |
No | |
| id | string | Unique identifier for the evaluation. | Yes | |
| metadata |
|

useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

Possible values:

`eval`

Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters.

### EvalCompareReport

Insights from the evaluation comparison.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| comparisons | array | Comparison results for each treatment run against the baseline. | Yes | |
| method | string | The statistical method used for comparison. | Yes | |
| type | enum | The type of insights result. Possible values: `EvaluationComparison` |
Yes |

### EvalResult

Result of the evaluation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| name | string | name of the check | Yes | |
| passed | boolean | indicates if the check passed or failed | Yes | |
| score | number | score | Yes | |
| type | string | type of the check | Yes |

### EvalRun

A schema representing an evaluation run.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | object | Yes | ||
| created_by | string | the name of the person who created the run. | No | |
| data_source | object | A JsonlRunDataSource object with that specifies a JSONL file that matches the eval | Yes | |
| └─ input_messages |
|

`item.input_trajectory`

), or a template with variable references to the `item`

namespace.[RedTeamItemGenerationParams](#redteamitemgenerationparams)[OpenAI.CreateEvalResponsesRunDataSourceSamplingParams](#openaicreateevalresponsesrundatasourcesamplingparams)[OpenAI.EvalJsonlFileContentSource](#openaievaljsonlfilecontentsource)or[OpenAI.EvalJsonlFileIdSource](#openaievaljsonlfileidsource)or[OpenAI.EvalResponsesSource](#openaievalresponsessource)`item`

namespace in this run's data source.[Target](#target)[OpenAI.EvalApiError](#openaievalapierror)[OpenAI.Metadata](#openaimetadata)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

Possible values:

`eval.run`

Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters.

[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)### EvalRunDataSource

Base class for run data sources with discriminator support.

### Discriminator for EvalRunDataSource

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`azure_ai_traces` |
|

`azure_ai_responses`

[AzureAIResponses](#azureairesponses)`azure_ai_target_completions`

[TargetCompletions](#targetcompletions)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | string | The data source type discriminator. | Yes |

### EvalRunOutputItem

A schema representing an evaluation run output item.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | object | Yes | ||
| datasource_item | object | Details of the input data source item. | Yes | |
| datasource_item_id | object | Yes | ||
| eval_id | string | The identifier of the evaluation group. | Yes | |
| id | string | Unique identifier for the evaluation run output item. | Yes | |
| object | enum | The type of the object. Always "eval.run.output_item". Possible values: `eval.run.output_item` |
Yes | |
| results | array | A list of grader results for this output item. | Yes | |
| run_id | string | The identifier of the evaluation run associated with this output item. | Yes | |
| sample | object | Yes | ||
| └─ error |
|

[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.numeric](#openainumeric)[OpenAI.numeric](#openainumeric)[OpenAI.EvalRunOutputItemSampleUsage](#openaievalrunoutputitemsampleusage)### EvalRunOutputItemResult

A single grader result for an evaluation run output item.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| label | string | The label associated with the test criteria metric (e.g., "pass", "fail", "good", "bad"). | No | |
| metric | string | The name of the metric (e.g., "fluency", "f1_score"). | No | |
| name | string | The name of the grader. | Yes | |
| passed | boolean | Whether the grader considered the output a pass. | Yes | |
| properties | object | Additional details about the test criteria metric. | No | |
| reason | string | The reason for the test criteria metric. | No | |
| sample | object | Optional sample or intermediate data produced by the grader. | No | |
| score | object | Yes | ||
| threshold | number | The threshold used to determine pass/fail for this test criteria, if it is numerical. | No | |
| type | string | The grader type (for example, "string-check-grader"). | No |

### EvalRunResultCompareItem

Metric comparison for a treatment against the baseline.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| deltaEstimate | number | Estimated difference between treatment and baseline. | Yes | |
| pValue | number | P-value for the treatment effect. | Yes | |
| treatmentEffect | object | Treatment Effect Type. | Yes | |
| treatmentRunId | string | The treatment run ID. | Yes | |
| treatmentRunSummary | object | Summary statistics of a metric in an evaluation run. | Yes | |
| └─ average | number | Average value of the metric in the evaluation run. | No | |
| └─ runId | string | The evaluation run ID. | No | |
| └─ sampleCount | integer | Number of samples in the evaluation run. | No | |
| └─ standardDeviation | number | Standard deviation of the metric in the evaluation run. | No |

### EvalRunResultComparison

Comparison results for treatment runs against the baseline.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| baselineRunSummary | object | Summary statistics of a metric in an evaluation run. | Yes | |
| └─ average | number | Average value of the metric in the evaluation run. | No | |
| └─ runId | string | The evaluation run ID. | No | |
| └─ sampleCount | integer | Number of samples in the evaluation run. | No | |
| └─ standardDeviation | number | Standard deviation of the metric in the evaluation run. | No | |
| compareItems | array | List of comparison results for each treatment run. | Yes | |
| evaluator | string | Name of the evaluator for this testing criteria. | Yes | |
| metric | string | Metric being evaluated. | Yes | |
| testingCriteria | string | Name of the testing criteria. | Yes |

### EvalRunResultSummary

Summary statistics of a metric in an evaluation run.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| average | number | Average value of the metric in the evaluation run. | Yes | |
| runId | string | The evaluation run ID. | Yes | |
| sampleCount | integer | Number of samples in the evaluation run. | Yes | |
| standardDeviation | number | Standard deviation of the metric in the evaluation run. | Yes |

### EvaluationComparisonRequest

Evaluation Comparison Request

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| baselineRunId | string | The baseline run ID for comparison. | Yes | |
| evalId | string | Identifier for the evaluation. | Yes | |
| treatmentRunIds | array | List of treatment run IDs for comparison. | Yes | |
| type | enum | The type of request. Possible values: `EvaluationComparison` |
Yes |

### EvaluationResultSample

A sample from the evaluation result.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| evaluationResult | object | Result of the evaluation. | Yes | |
| └─ name | string | name of the check | No | |
| └─ passed | boolean | indicates if the check passed or failed | No | |
| └─ score | number | score | No | |
| └─ type | string | type of the check | No | |
| type | enum | Evaluation Result Sample Type Possible values: `EvaluationResultSample` |
Yes |

### EvaluationRule

Evaluation rule model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| action | object | Evaluation action model. | Yes | |
| └─ type |
|

### EvaluationRuleAction

Evaluation action model.

### Discriminator for EvaluationRuleAction

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`continuousEvaluation` |
|

`humanEvaluation`

[HumanEvaluationRuleAction](#humanevaluationruleaction)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | object | Type of the evaluation action. | Yes |

### EvaluationRuleActionType

Type of the evaluation action.

| Property | Value |
|---|---|
Description |
Type of the evaluation action. |
Type |
string |
Values |
`continuousEvaluation` `humanEvaluation` |

### EvaluationRuleEventType

Type of the evaluation rule event.

| Property | Value |
|---|---|
Description |
Type of the evaluation rule event. |
Type |
string |
Values |
`responseCompleted` `manual` |

### EvaluationRuleFilter

Evaluation filter model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| agentName | string | Filter by agent name. | Yes |

### EvaluationRunClusterInsightResult

Insights from the evaluation run cluster analysis.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| clusterInsight |
|

Possible values:

`EvaluationRunClusterInsight`

### EvaluationRunClusterInsightsRequest

Insights on set of Evaluation Results

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| evalId | string | Evaluation Id for the insights. | Yes | |
| modelConfiguration | object | Configuration of the model used in the insight generation. | No | |
| └─ modelDeploymentName | string | The model deployment to be evaluated. Accepts either the deployment name alone or with the connection name as `{connectionName}/<modelDeploymentName>` . |
No | |
| runIds | array | List of evaluation run IDs for the insights. | Yes | |
| type | enum | The type of insights request. Possible values: `EvaluationRunClusterInsight` |
Yes |

### EvaluationScheduleTask

Evaluation task for the schedule.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| evalId | string | Identifier of the evaluation group. | Yes | |
| evalRun | object | The evaluation run payload. | Yes | |
| type | enum | Possible values: `Evaluation` |
Yes |

### EvaluationTaxonomy

Evaluation Taxonomy Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| id | string | Asset ID, a unique identifier for the asset | No | |
| name | string | The name of the resource | Yes | |
| properties | object | Additional properties for the evaluation taxonomy. | No | |
| taxonomyCategories | array | List of taxonomy categories. | No | |
| taxonomyInput | object | Input configuration for the evaluation taxonomy. | Yes | |
| └─ type |
|

### EvaluationTaxonomyCreateOrUpdate

Evaluation Taxonomy Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | The asset description text. | No | |
| properties | object | Additional properties for the evaluation taxonomy. | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No | |
| taxonomyCategories | array | List of taxonomy categories. | No | |
| taxonomyInput | object | Input configuration for the evaluation taxonomy. | Yes | |
| └─ type |
|

### EvaluationTaxonomyInput

Input configuration for the evaluation taxonomy.

### Discriminator for EvaluationTaxonomyInput

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`agent` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | object | Type of the evaluation taxonomy input. | Yes |

### EvaluationTaxonomyInputType

Type of the evaluation taxonomy input.

| Property | Value |
|---|---|
Description |
Type of the evaluation taxonomy input. |
Type |
string |
Values |
`agent` `policy` |

### EvaluationTaxonomyInputUpdate

Input configuration for the evaluation taxonomy.

### Discriminator for EvaluationTaxonomyInputUpdate

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`agent` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | object | Type of the evaluation taxonomy input. | Yes |

### EvaluationTaxonomyUpdate

Evaluation Taxonomy Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | The asset description text. | No | |
| properties | object | Additional properties for the evaluation taxonomy. | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No | |
| taxonomyCategories | array | List of taxonomy categories. | No | |
| taxonomyInput | object | Input configuration for the evaluation taxonomy. | No | |
| └─ type |
|

### EvaluatorCategory

The category of the evaluator

| Property | Value |
|---|---|
Description |
The category of the evaluator |
Type |
string |
Values |
`quality` `safety` `agents` |

### EvaluatorDefinition

Base evaluator configuration with discriminator

### Discriminator for EvaluatorDefinition

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`code` |
|

`prompt`

[PromptBasedEvaluatorDefinition](#promptbasedevaluatordefinition)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data_schema | The JSON schema (Draft 2020-12) for the evaluator's input data. This includes parameters like type, properties, required. | No | ||
| init_parameters | The JSON schema (Draft 2020-12) for the evaluator's input parameters. This includes parameters like type, properties, required. | No | ||
| metrics | object | List of output metrics produced by this evaluator | No | |
| type | object | The type of evaluator definition | Yes |

### EvaluatorDefinitionType

The type of evaluator definition

| Property | Value |
|---|---|
Description |
The type of evaluator definition |
Type |
string |
Values |
`prompt` `code` `prompt_and_code` `service` `openai_graders` |

### EvaluatorMetric

Evaluator Metric

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| desirable_direction | object | The direction of the metric indicating whether a higher value is better, a lower value is better, or neutral | No | |
| is_primary | boolean | Indicates if this metric is primary when there are multiple metrics. | No | |
| max_value | number | Maximum value for the metric. If not specified, it is assumed to be unbounded. | No | |
| min_value | number | Minimum value for the metric | No | |
| type | object | The type of the evaluator | No |

### EvaluatorMetricDirection

The direction of the metric indicating whether a higher value is better, a lower value is better, or neutral

| Property | Value |
|---|---|
Description |
The direction of the metric indicating whether a higher value is better, a lower value is better, or neutral |
Type |
string |
Values |
`increase` `decrease` `neutral` |

### EvaluatorMetricType

The type of the evaluator

| Property | Value |
|---|---|
Description |
The type of the evaluator |
Type |
string |
Values |
`ordinal` `continuous` `boolean` |

### EvaluatorType

The type of the evaluator

| Property | Value |
|---|---|
Description |
The type of the evaluator |
Type |
string |
Values |
`builtin` `custom` |

### EvaluatorVersion

Evaluator Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| categories | array | The categories of the evaluator | Yes | |
| created_at | integer | Creation date/time of the evaluator | Yes | |
| created_by | string | Creator of the evaluator | Yes | |
| definition | object | Base evaluator configuration with discriminator | Yes | |
| └─ data_schema | The JSON schema (Draft 2020-12) for the evaluator's input data. This includes parameters like type, properties, required. | No | ||
| └─ init_parameters | The JSON schema (Draft 2020-12) for the evaluator's input parameters. This includes parameters like type, properties, required. | No | ||
| └─ metrics | object | List of output metrics produced by this evaluator | No | |
| └─ type |
|

### EvaluatorVersionCreate

Evaluator Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| categories | array | The categories of the evaluator | Yes | |
| definition | object | Base evaluator configuration with discriminator | Yes | |
| └─ data_schema | The JSON schema (Draft 2020-12) for the evaluator's input data. This includes parameters like type, properties, required. | No | ||
| └─ init_parameters | The JSON schema (Draft 2020-12) for the evaluator's input parameters. This includes parameters like type, properties, required. | No | ||
| └─ metrics | object | List of output metrics produced by this evaluator | No | |
| └─ type |
|

### EvaluatorVersionUpdate

Evaluator Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| categories | array | The categories of the evaluator | No | |
| description | string | The asset description text. | No | |
| display_name | string | Display Name for evaluator. It helps to find the evaluator easily in Foundry. It does not need to be unique. | No | |
| metadata | object | Metadata about the evaluator | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No |

### FabricDataAgentToolParameters

The fabric data agent tool parameters.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| project_connections | array | The project connections attached to this tool. There can be a maximum of 1 connection resource attached to the tool. |
No |

### FileDatasetVersion

FileDatasetVersion Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Dataset type Possible values: `uri_file` |
Yes |

### FileDatasetVersionUpdate

FileDatasetVersion Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Dataset type Possible values: `uri_file` |
Yes |

### FolderDatasetVersion

FileDatasetVersion Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Dataset type Possible values: `uri_folder` |
Yes |

### FolderDatasetVersionUpdate

FileDatasetVersion Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Dataset type Possible values: `uri_folder` |
Yes |

### HostedAgentDefinition

The hosted agent definition.

### Discriminator for HostedAgentDefinition

This component uses the property `kind`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`hosted` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| container_protocol_versions | array | The protocols that the agent supports for ingress communication of the containers. | Yes | |
| cpu | string | The CPU configuration for the hosted agent. | Yes | |
| environment_variables | object | Environment variables to set in the hosted agent container. | No | |
| kind | enum | Possible values: `hosted` |
Yes | |
| memory | string | The memory configuration for the hosted agent. | Yes | |
| tools | array | An array of tools the hosted agent's model may call while generating a response. You can specify which tool to use by setting the `tool_choice` parameter. |
No |

### HourlyRecurrenceSchedule

Hourly recurrence schedule.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `Hourly` |
Yes |

### HumanEvaluationRuleAction

Evaluation rule action for human evaluation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| templateId | object | Identifier of a saved asset. | Yes | |
| type | enum | Possible values: `humanEvaluation` |
Yes |

### ImageBasedHostedAgentDefinition

The image-based deployment definition for a hosted agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| image | string | The image for the hosted agent. | Yes | |
| kind | enum | Possible values: `hosted` |
Yes |

### Index

Index resource Definition

### Discriminator for Index

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`AzureSearch` |
|

`ManagedAzureSearch`

[ManagedAzureAISearchIndex](#managedazureaisearchindex)`CosmosDBNoSqlVectorStore`

[CosmosDBIndex](#cosmosdbindex)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| id | string | Asset ID, a unique identifier for the asset | No | |
| name | string | The name of the resource | Yes | |
| type | object | Yes | ||
| version | string | The version of the resource | Yes |

### IndexType

| Property | Value |
|---|---|
Type |
string |
Values |
`AzureSearch` `CosmosDBNoSqlVectorStore` `ManagedAzureSearch` |

### IndexUpdate

Index resource Definition

### Discriminator for IndexUpdate

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`AzureSearch` |
|

`ManagedAzureSearch`

[ManagedAzureAISearchIndexUpdate](#managedazureaisearchindexupdate)`CosmosDBNoSqlVectorStore`

[CosmosDBIndexUpdate](#cosmosdbindexupdate)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | The asset description text. | No | |
| tags | object | Tag dictionary. Tags can be added, removed, and updated. | No | |
| type | object | Yes |

### Insight

The response body for cluster insights.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| displayName | string | User friendly display name for the insight. | Yes | |
| id | string | The unique identifier for the insights report. | Yes | |
| metadata | object | Metadata about the insights. | Yes | |
| └─ completedAt | string | The timestamp when the insights were completed. | No | |
| └─ createdAt | string | The timestamp when the insights were created. | No | |
| request | object | The request of the insights report. | Yes | |
| └─ type |
|

[InsightType](#insighttype)### InsightCluster

A cluster of analysis samples.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | Description of the analysis cluster. | Yes | |
| id | string | The id of the analysis cluster. | Yes | |
| label | string | Label for the cluster | Yes | |
| samples | array | List of samples that belong to this cluster. Empty if samples are part of subclusters. | No | |
| subClusters | array | List of subclusters within this cluster. Empty if no subclusters exist. | No | |
| suggestion | string | Suggestion for the cluster | Yes | |
| suggestionTitle | string | The title of the suggestion for the cluster | Yes | |
| weight | integer | The weight of the analysis cluster. This indicate number of samples in the cluster. | Yes |

### InsightModelConfiguration

Configuration of the model used in the insight generation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| modelDeploymentName | string | The model deployment to be evaluated. Accepts either the deployment name alone or with the connection name as `{connectionName}/<modelDeploymentName>` . |
Yes |

### InsightRequest

The request of the insights report.

### Discriminator for InsightRequest

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`EvaluationRunClusterInsight` |
|

`AgentClusterInsight`

[AgentClusterInsightsRequest](#agentclusterinsightsrequest)`EvaluationComparison`

[EvaluationComparisonRequest](#evaluationcomparisonrequest)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | object | The request of the insights. | Yes |

### InsightResult

The result of the insights.

### Discriminator for InsightResult

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`EvaluationComparison` |
|

`EvaluationRunClusterInsight`

[EvaluationRunClusterInsightResult](#evaluationrunclusterinsightresult)`AgentClusterInsight`

[AgentClusterInsightResult](#agentclusterinsightresult)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | object | The request of the insights. | Yes |

### InsightSample

A sample from the analysis.

### Discriminator for InsightSample

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`EvaluationResultSample` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| correlationInfo | object | Info about the correlation for the analysis sample. | Yes | |
| features | object | Features to help with additional filtering of data in UX. | Yes | |
| id | string | The unique identifier for the analysis sample. | Yes | |
| type | object | The type of sample used in the analysis. | Yes |

### InsightScheduleTask

Insight task for the schedule.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| insight | object | The response body for cluster insights. | Yes | |
| └─ displayName | string | User friendly display name for the insight. | No | |
| └─ id | string | The unique identifier for the insights report. | No | |
| └─ metadata |
|

[InsightRequest](#insightrequest)[InsightResult](#insightresult)[Azure.Core.Foundations.OperationState](#azurecorefoundationsoperationstate)Possible values:

`Insight`

### InsightSummary

Summary of the error cluster analysis.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| method | string | Method used for clustering. | Yes | |
| sampleCount | integer | Total number of samples analyzed. | Yes | |
| uniqueClusterCount | integer | Total number of unique clusters. | Yes | |
| uniqueSubclusterCount | integer | Total number of unique subcluster labels. | Yes | |
| usage | object | Token usage for cluster analysis | Yes | |
| └─ inputTokenUsage | integer | input token usage | No | |
| └─ outputTokenUsage | integer | output token usage | No | |
| └─ totalTokenUsage | integer | total token usage | No |

### InsightType

The request of the insights.

| Property | Value |
|---|---|
Type |
string |
Values |
`EvaluationRunClusterInsight` `AgentClusterInsight` `EvaluationComparison` |

### InsightsMetadata

Metadata about the insights.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| completedAt | string | The timestamp when the insights were completed. | No | |
| createdAt | string | The timestamp when the insights were created. | Yes |

### ItemGenerationParams

Represents the set of parameters used to control item generation operations.

### Discriminator for ItemGenerationParams

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | string | The type of item generation parameters to use. | Yes |

### ManagedAzureAISearchIndex

Managed Azure AI Search Index Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Type of index Possible values: `ManagedAzureSearch` |
Yes |

### ManagedAzureAISearchIndexUpdate

Managed Azure AI Search Index Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Type of index Possible values: `ManagedAzureSearch` |
Yes |

### MemoryItem

A single memory item stored in the memory store, containing content and metadata.

### Discriminator for MemoryItem

This component uses the property `kind`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`user_profile` |
|

`chat_summary`

[ChatSummaryMemoryItem](#chatsummarymemoryitem)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | string | The content of the memory. | Yes | |
| kind | object | Memory item kind. | Yes | |
| memory_id | string | The unique ID of the memory item. | Yes | |
| scope | string | The namespace that logically groups and isolates memories, such as a user ID. | Yes | |
| updated_at | integer | The last update time of the memory item. | Yes |

### MemoryItemKind

Memory item kind.

| Property | Value |
|---|---|
Description |
Memory item kind. |
Type |
string |
Values |
`user_profile` `chat_summary` |

### MemoryOperation

Represents a single memory operation (create, update, or delete) performed on a memory item.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| kind | object | Memory operation kind. | Yes | |
| memory_item | object | A single memory item stored in the memory store, containing content and metadata. | Yes | |
| └─ content | string | The content of the memory. | No | |
| └─ kind |
|

### MemoryOperationKind

Memory operation kind.

| Property | Value |
|---|---|
Description |
Memory operation kind. |
Type |
string |
Values |
`create` `update` `delete` |

### MemorySearchItem

A retrieved memory item from memory search.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| memory_item | object | A single memory item stored in the memory store, containing content and metadata. | Yes | |
| └─ content | string | The content of the memory. | No | |
| └─ kind |
|

### MemorySearchOptions

Memory search options.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| max_memories | integer | Maximum number of memory items to return. | No |

### MemorySearchTool

A tool for integrating memories into the agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| memory_store_name | string | The name of the memory store to use. | Yes | |
| scope | string | The namespace used to group and isolate memories, such as a user ID. Limits which memories can be retrieved or updated. Use special variable `{{$userId}}` to scope memories to the current signed-in user. |
Yes | |
| search_options | object | Memory search options. | No | |
| └─ max_memories | integer | Maximum number of memory items to return. | No | |
| type | enum | The type of the tool. Always `memory_search` .Possible values: `memory_search` |
Yes | |
| update_delay | integer | Time to wait before updating memories after inactivity (seconds). Default 300. | No | 300 |

### MemorySearchToolCallItemParam

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| results | array | The results returned from the memory search. | No | |
| type | enum | Possible values: `memory_search_call` |
Yes |

### MemorySearchToolCallItemResource

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| results | array | The results returned from the memory search. | No | |
| status | enum | The status of the memory search tool call. One of `in_progress` ,`searching` , `completed` , `incomplete` or `failed` ,Possible values: `in_progress` , `searching` , `completed` , `incomplete` , `failed` |
Yes | |
| type | enum | Possible values: `memory_search_call` |
Yes |

### MemoryStoreDefaultDefinition

Default memory store implementation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| chat_model | string | The name or identifier of the chat completion model deployment used for memory processing. | Yes | |
| embedding_model | string | The name or identifier of the embedding model deployment used for memory processing. | Yes | |
| kind | enum | The kind of the memory store. Possible values: `default` |
Yes | |
| options | object | Default memory store configurations. | No | |
| └─ chat_summary_enabled | boolean | Whether to enable chat summary extraction and storage. Default is true. | No | True |
| └─ user_profile_details | string | Specific categories or types of user profile information to extract and store. | No | |
| └─ user_profile_enabled | boolean | Whether to enable user profile extraction and storage. Default is true. | No | True |

### MemoryStoreDefaultOptions

Default memory store configurations.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| chat_summary_enabled | boolean | Whether to enable chat summary extraction and storage. Default is true. | Yes | True |
| user_profile_details | string | Specific categories or types of user profile information to extract and store. | No | |
| user_profile_enabled | boolean | Whether to enable user profile extraction and storage. Default is true. | Yes | True |

### MemoryStoreDefinition

Base definition for memory store configurations.

### Discriminator for MemoryStoreDefinition

This component uses the property `kind`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`default` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| kind | object | The type of memory store implementation to use. | Yes |

### MemoryStoreDeleteScopeResponse

Response for deleting memories from a scope.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| deleted | boolean | Whether the deletion operation was successful. | Yes | |
| name | string | The name of the memory store. | Yes | |
| object | enum | The object type. Always 'memory_store.scope.deleted'. Possible values: `memory_store.scope.deleted` |
Yes | |
| scope | string | The scope from which memories were deleted. | Yes |

### MemoryStoreKind

The type of memory store implementation to use.

| Property | Value |
|---|---|
Description |
The type of memory store implementation to use. |
Type |
string |
Values |
`default` |

### MemoryStoreObject

A memory store that can store and retrieve user memories.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | integer | The Unix timestamp (seconds) when the memory store was created. | Yes | |
| definition | object | Base definition for memory store configurations. | Yes | |
| └─ kind |
|

Possible values:

`memory_store`

### MemoryStoreOperationUsage

Usage statistics of a memory store operation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| embedding_tokens | integer | The number of embedding tokens. | Yes | |
| input_tokens | integer | The number of input tokens. | Yes | |
| input_tokens_details | object | A detailed breakdown of the input tokens. | Yes | |
| └─ cached_tokens | integer | The number of tokens that were retrieved from the cache.
|
No | |
| output_tokens | integer | The number of output tokens. | Yes | |
| output_tokens_details | object | A detailed breakdown of the output tokens. | Yes | |
| └─ reasoning_tokens | integer | The number of reasoning tokens. | No | |
| total_tokens | integer | The total number of tokens used. | Yes |

### MemoryStoreSearchResponse

Memory search response.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| memories | array | Related memory items found during the search operation. | Yes | |
| search_id | string | The unique ID of this search request. Use this value as previous_search_id in subsequent requests to perform incremental searches. | Yes | |
| usage | object | Usage statistics of a memory store operation. | Yes | |
| └─ embedding_tokens | integer | The number of embedding tokens. | No | |
| └─ input_tokens | integer | The number of input tokens. | No | |
| └─ input_tokens_details | object | A detailed breakdown of the input tokens. | No | |
| └─ cached_tokens | integer | The number of tokens that were retrieved from the cache.
|
No | |
| └─ output_tokens | integer | The number of output tokens. | No | |
| └─ output_tokens_details | object | A detailed breakdown of the output tokens. | No | |
| └─ reasoning_tokens | integer | The number of reasoning tokens. | No | |
| └─ total_tokens | integer | The total number of tokens used. | No |

### MemoryStoreUpdateCompletedResult

Memory update result.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| memory_operations | array | A list of individual memory operations that were performed during the update. | Yes | |
| usage | object | Usage statistics of a memory store operation. | Yes | |
| └─ embedding_tokens | integer | The number of embedding tokens. | No | |
| └─ input_tokens | integer | The number of input tokens. | No | |
| └─ input_tokens_details | object | A detailed breakdown of the input tokens. | No | |
| └─ cached_tokens | integer | The number of tokens that were retrieved from the cache.
|
No | |
| └─ output_tokens | integer | The number of output tokens. | No | |
| └─ output_tokens_details | object | A detailed breakdown of the output tokens. | No | |
| └─ reasoning_tokens | integer | The number of reasoning tokens. | No | |
| └─ total_tokens | integer | The total number of tokens used. | No |

### MemoryStoreUpdateResponse

Provides the status of a memory store update operation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| error | object | No | ||
| └─ additionalInfo | object | No | ||
| └─ code | string | No | ||
| └─ debugInfo | object | No | ||
| └─ details | array | No | ||
| └─ message | string | No | ||
| └─ param | string | No | ||
| └─ type | string | No | ||
| result | object | Memory update result. | No | |
| └─ memory_operations | array | A list of individual memory operations that were performed during the update. | No | |
| └─ usage |
|

### MemoryStoreUpdateStatus

Status of a memory store update operation.

| Property | Value |
|---|---|
Description |
Status of a memory store update operation. |
Type |
string |
Values |
`queued` `in_progress` `completed` `failed` `superseded` |

### MicrosoftFabricAgentTool

The input definition information for a Microsoft Fabric tool as used to configure an agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| fabric_dataagent_preview | object | The fabric data agent tool parameters. | Yes | |
| └─ project_connections | array | The project connections attached to this tool. There can be a maximum of 1 connection resource attached to the tool. |
No | |
| type | enum | The object type, which is always 'fabric_dataagent'. Possible values: `fabric_dataagent_preview` |
Yes |

### ModelDeployment

Model Deployment Definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| capabilities | object | Capabilities of deployed model | Yes | |
| connectionName | string | Name of the connection the deployment comes from | No | |
| modelName | string | Publisher-specific name of the deployed model | Yes | |
| modelPublisher | string | Name of the deployed model's publisher | Yes | |
| modelVersion | string | Publisher-specific version of the deployed model | Yes | |
| sku | object | Sku information | Yes | |
| └─ capacity | integer | Sku capacity | No | |
| └─ family | string | Sku family | No | |
| └─ name | string | Sku name | No | |
| └─ size | string | Sku size | No | |
| └─ tier | string | Sku tier | No | |
| type | enum | The type of the deployment Possible values: `ModelDeployment` |
Yes |

### ModelSamplingParams

Represents a set of parameters used to control the sampling behavior of a language model during text generation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| max_completion_tokens | integer | The maximum number of tokens allowed in the completion. | Yes | |
| seed | integer | The random seed for reproducibility. | Yes | |
| temperature | number | The temperature parameter for sampling. | Yes | |
| top_p | number | The top-p parameter for nucleus sampling. | Yes |

### ModelSamplingParamsUpdate

Represents a set of parameters used to control the sampling behavior of a language model during text generation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| max_completion_tokens | integer | The maximum number of tokens allowed in the completion. | No | |
| seed | integer | The random seed for reproducibility. | No | |
| temperature | number | The temperature parameter for sampling. | No | |
| top_p | number | The top-p parameter for nucleus sampling. | No |

### MonthlyRecurrenceSchedule

Monthly recurrence schedule.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| daysOfMonth | array | Days of the month for the recurrence schedule. | Yes | |
| type | enum | Monthly recurrence type. Possible values: `Monthly` |
Yes |

### NoAuthenticationCredentials

Credentials that do not require authentication

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The credential type Possible values: `None` |
Yes |

### OAuthConsentRequestItemResource

Request from the service for the user to perform OAuth consent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| consent_link | string | The link the user can use to perform OAuth consent. | Yes | |
| id | string | Yes | ||
| server_label | string | The server label for the OAuth consent request. | Yes | |
| type | enum | Possible values: `oauth_consent_request` |
Yes |

### OneTimeTrigger

One-time trigger.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| timeZone | string | Time zone for the one-time trigger. | No | UTC |
| triggerAt | string | Date and time for the one-time trigger in ISO 8601 format. | Yes | |
| type | enum | Possible values: `OneTime` |
Yes |

### OpenAI.Annotation

### Discriminator for OpenAI.Annotation

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`file_citation` |
|

`url_citation`

[OpenAI.AnnotationUrlCitation](#openaiannotationurlcitation)`file_path`

[OpenAI.AnnotationFilePath](#openaiannotationfilepath)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.AnnotationFileCitation

A citation to a file.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| file_id | string | The ID of the file. | Yes | |
| filename | string | The filename of the file cited. | Yes | |
| index | integer | The index of the file in the list of files. | Yes | |
| type | enum | The type of the file citation. Always `file_citation` .Possible values: `file_citation` |
Yes |

### OpenAI.AnnotationFilePath

A path to a file.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| file_id | string | The ID of the file. | Yes | |
| index | integer | The index of the file in the list of files. | Yes | |
| type | enum | The type of the file path. Always `file_path` .Possible values: `file_path` |
Yes |

### OpenAI.AnnotationType

| Property | Value |
|---|---|
Type |
string |
Values |
`file_citation` `url_citation` `file_path` `container_file_citation` |

### OpenAI.AnnotationUrlCitation

A citation for a web resource used to generate a model response.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| end_index | integer | The index of the last character of the URL citation in the message. | Yes | |
| start_index | integer | The index of the first character of the URL citation in the message. | Yes | |
| title | string | The title of the web resource. | Yes | |
| type | enum | The type of the URL citation. Always `url_citation` .Possible values: `url_citation` |
Yes | |
| url | string | The URL of the web resource. | Yes |

### OpenAI.ApproximateLocation

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| city | string | No | ||
| country | string | No | ||
| region | string | No | ||
| timezone | string | No | ||
| type | enum | Possible values: `approximate` |
Yes |

### OpenAI.ChatCompletionTool

A function tool that can be used to generate a response.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| function |
|

`function`

is supported.Possible values:

`function`

### OpenAI.CodeInterpreterOutput

### Discriminator for OpenAI.CodeInterpreterOutput

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`image` |
|

`logs`

[OpenAI.CodeInterpreterOutputLogs](#openaicodeinterpreteroutputlogs)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.CodeInterpreterOutputImage

The image output from the code interpreter.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of the output. Always 'image'. Possible values: `image` |
Yes | |
| url | string | The URL of the image output from the code interpreter. | Yes |

### OpenAI.CodeInterpreterOutputLogs

The logs output from the code interpreter.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| logs | string | The logs output from the code interpreter. | Yes | |
| type | enum | The type of the output. Always 'logs'. Possible values: `logs` |
Yes |

### OpenAI.CodeInterpreterOutputType

| Property | Value |
|---|---|
Type |
string |
Values |
`logs` `image` |

### OpenAI.CodeInterpreterTool

A tool that runs Python code to help generate a response to a prompt.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| container | object | Configuration for a code interpreter container. Optionally specify the IDs of the files to run the code on. |
Yes | |
| └─ file_ids | array | An optional list of uploaded files to make available to your code. | No | |
| └─ type | enum | Always `auto` .Possible values: `auto` |
No | |
| type | enum | The type of the code interpreter tool. Always `code_interpreter` .Possible values: `code_interpreter` |
Yes |

### OpenAI.CodeInterpreterToolAuto

Configuration for a code interpreter container. Optionally specify the IDs of the files to run the code on.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| file_ids | array | An optional list of uploaded files to make available to your code. | No | |
| type | enum | Always `auto` .Possible values: `auto` |
Yes |

### OpenAI.CodeInterpreterToolCallItemParam

A tool call to run code.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code | string | The code to run, or null if not available. | Yes | |
| container_id | string | The ID of the container used to run the code. | Yes | |
| outputs | array | The outputs generated by the code interpreter, such as logs or images. Can be null if no outputs are available. |
Yes | |
| type | enum | Possible values: `code_interpreter_call` |
Yes |

### OpenAI.CodeInterpreterToolCallItemResource

A tool call to run code.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code | string | The code to run, or null if not available. | Yes | |
| container_id | string | The ID of the container used to run the code. | Yes | |
| outputs | array | The outputs generated by the code interpreter, such as logs or images. Can be null if no outputs are available. |
Yes | |
| status | enum | Possible values: `in_progress` , `completed` , `incomplete` , `interpreting` , `failed` |
Yes | |
| type | enum | Possible values: `code_interpreter_call` |
Yes |

### OpenAI.ComparisonFilter

A filter used to compare a specified attribute key to a given value using a defined comparison operation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| key | string | The key to compare against the value. | Yes | |
| type | enum | Specifies the comparison operator:`eq` (equal), `ne` (not equal), `gt` (greater than), `gte` (greater than or equal), `lt` (less than), `lte` (less than or equal).Possible values: `eq` , `ne` , `gt` , `gte` , `lt` , `lte` |
Yes | |
| value | string or number or boolean | Yes |

### OpenAI.CompoundFilter

Combine multiple filters using `and`

or `or`

.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| filters | array | Array of filters to combine. Items can be `ComparisonFilter` or `CompoundFilter` . |
Yes | |
| type | enum | Type of operation: `and` or `or` .Possible values: `and` , `or` |
Yes |

### OpenAI.ComputerAction

### Discriminator for OpenAI.ComputerAction

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`click` |
|

`double_click`

[OpenAI.ComputerActionDoubleClick](#openaicomputeractiondoubleclick)`drag`

[OpenAI.ComputerActionDrag](#openaicomputeractiondrag)`move`

[OpenAI.ComputerActionMove](#openaicomputeractionmove)`screenshot`

[OpenAI.ComputerActionScreenshot](#openaicomputeractionscreenshot)`scroll`

[OpenAI.ComputerActionScroll](#openaicomputeractionscroll)`type`

[OpenAI.ComputerActionTypeKeys](#openaicomputeractiontypekeys)`wait`

[OpenAI.ComputerActionWait](#openaicomputeractionwait)`keypress`

[OpenAI.ComputerActionKeyPress](#openaicomputeractionkeypress)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.ComputerActionClick

A click action.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| button | enum | Indicates which mouse button was pressed during the click. One of `left` , `right` , `wheel` , `back` , or `forward` .Possible values: `left` , `right` , `wheel` , `back` , `forward` |
Yes | |
| type | enum | Specifies the event type. For a click action, this property is always set to `click` .Possible values: `click` |
Yes | |
| x | integer | The x-coordinate where the click occurred. | Yes | |
| y | integer | The y-coordinate where the click occurred. | Yes |

### OpenAI.ComputerActionDoubleClick

A double click action.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Specifies the event type. For a double click action, this property is always set to `double_click` .Possible values: `double_click` |
Yes | |
| x | integer | The x-coordinate where the double click occurred. | Yes | |
| y | integer | The y-coordinate where the double click occurred. | Yes |

### OpenAI.ComputerActionDrag

A drag action.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| path | array | An array of coordinates representing the path of the drag action. Coordinates will appear as an array of objects, eg `<br>[<br> { x: 100, y: 200 },<br> { x: 200, y: 300 }<br>]<br>` |
Yes | |
| type | enum | Specifies the event type. For a drag action, this property is always set to `drag` .Possible values: `drag` |
Yes |

### OpenAI.ComputerActionKeyPress

A collection of keypresses the model would like to perform.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| keys | array | The combination of keys the model is requesting to be pressed. This is an array of strings, each representing a key. |
Yes | |
| type | enum | Specifies the event type. For a keypress action, this property is always set to `keypress` .Possible values: `keypress` |
Yes |

### OpenAI.ComputerActionMove

A mouse move action.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Specifies the event type. For a move action, this property is always set to `move` .Possible values: `move` |
Yes | |
| x | integer | The x-coordinate to move to. | Yes | |
| y | integer | The y-coordinate to move to. | Yes |

### OpenAI.ComputerActionScreenshot

A screenshot action.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Specifies the event type. For a screenshot action, this property is always set to `screenshot` .Possible values: `screenshot` |
Yes |

### OpenAI.ComputerActionScroll

A scroll action.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| scroll_x | integer | The horizontal scroll distance. | Yes | |
| scroll_y | integer | The vertical scroll distance. | Yes | |
| type | enum | Specifies the event type. For a scroll action, this property is always set to `scroll` .Possible values: `scroll` |
Yes | |
| x | integer | The x-coordinate where the scroll occurred. | Yes | |
| y | integer | The y-coordinate where the scroll occurred. | Yes |

### OpenAI.ComputerActionType

| Property | Value |
|---|---|
Type |
string |
Values |
`screenshot` `click` `double_click` `scroll` `type` `wait` `keypress` `drag` `move` |

### OpenAI.ComputerActionTypeKeys

An action to type in text.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| text | string | The text to type. | Yes | |
| type | enum | Specifies the event type. For a type action, this property is always set to `type` .Possible values: `type` |
Yes |

### OpenAI.ComputerActionWait

A wait action.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Specifies the event type. For a wait action, this property is always set to `wait` .Possible values: `wait` |
Yes |

### OpenAI.ComputerToolCallItemParam

A tool call to a computer use tool. See the
[computer use guide](https://platform.openai.com/docs/guides/tools-computer-use) for more information.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| action |
|

Possible values:

`computer_call`

### OpenAI.ComputerToolCallItemResource

A tool call to a computer use tool. See the
[computer use guide](https://platform.openai.com/docs/guides/tools-computer-use) for more information.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| action |
|

`in_progress`

, `completed`

, or`incomplete`

. Populated when items are returned via API.Possible values:

`in_progress`

, `completed`

, `incomplete`

Possible values:

`computer_call`

### OpenAI.ComputerToolCallOutputItemOutput

### Discriminator for OpenAI.ComputerToolCallOutputItemOutput

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`computer_screenshot` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.ComputerToolCallOutputItemOutputComputerScreenshot

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| file_id | string | No | ||
| image_url | string | No | ||
| type | enum | Possible values: `computer_screenshot` |
Yes |

### OpenAI.ComputerToolCallOutputItemOutputType

A computer screenshot image used with the computer use tool.

| Property | Value |
|---|---|
Description |
A computer screenshot image used with the computer use tool. |
Type |
string |
Values |
`computer_screenshot` |

### OpenAI.ComputerToolCallOutputItemParam

The output of a computer tool call.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| acknowledged_safety_checks | array | The safety checks reported by the API that have been acknowledged by the developer. |
No | |
| call_id | string | The ID of the computer tool call that produced the output. | Yes | |
| output |
|

Possible values:

`computer_call_output`

### OpenAI.ComputerToolCallOutputItemResource

The output of a computer tool call.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| acknowledged_safety_checks | array | The safety checks reported by the API that have been acknowledged by the developer. |
No | |
| call_id | string | The ID of the computer tool call that produced the output. | Yes | |
| output |
|

`in_progress`

, `completed`

, or`incomplete`

. Populated when items are returned via API.Possible values:

`in_progress`

, `completed`

, `incomplete`

Possible values:

`computer_call_output`

### OpenAI.ComputerToolCallSafetyCheck

A pending safety check for the computer call.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code | string | The type of the pending safety check. | Yes | |
| id | string | The ID of the pending safety check. | Yes | |
| message | string | Details about the pending safety check. | Yes |

### OpenAI.ComputerUsePreviewTool

A tool that controls a virtual computer.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| display_height | integer | The height of the computer display. | Yes | |
| display_width | integer | The width of the computer display. | Yes | |
| environment | enum | The type of computer environment to control. Possible values: `windows` , `mac` , `linux` , `ubuntu` , `browser` |
Yes | |
| type | enum | The type of the computer use tool. Always `computer_use_preview` .Possible values: `computer_use_preview` |
Yes |

### OpenAI.ConversationItemList

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data | array | Yes | ||
| first_id | string | Yes | ||
| has_more | boolean | Yes | ||
| last_id | string | Yes | ||
| object | enum | Possible values: `list` |
Yes |

### OpenAI.ConversationResource

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | integer | Yes | ||
| id | string | The unique ID of the conversation. | Yes | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
Yes | |
| object | enum | The object type, which is always 'conversation'. Possible values: `conversation` |
Yes |

### OpenAI.Coordinate

An x/y coordinate pair, e.g. `{ x: 100, y: 200 }`

.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| x | integer | The x-coordinate. | Yes | |
| y | integer | The y-coordinate. | Yes |

### OpenAI.CreateConversationRequest

Create a conversation

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| items | array | Initial items to include the conversation context. You may add up to 20 items at a time. |
No | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No |

### OpenAI.CreateEvalCompletionsRunDataSource

A CompletionsRunDataSource object describing a model sampling configuration.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input_messages | object | No | ||
| └─ item_reference | string | No | ||
| └─ template | array | No | ||
| └─ type | enum | Possible values: `item_reference` |
No | |
| model | string | The name of the model to use for generating completions (e.g. "o3-mini"). | No | |
| sampling_params |
|

[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.Metadata](#openaimetadata)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

`stored_completions`

.Possible values:

`stored_completions`

`completions`

.Possible values:

`completions`

### OpenAI.CreateEvalCompletionsRunDataSourceInputMessagesItemReference

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_reference | string | Yes | ||
| type | enum | Possible values: `item_reference` |
Yes |

### OpenAI.CreateEvalCompletionsRunDataSourceInputMessagesTemplate

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| template | array | Yes | ||
| type | enum | Possible values: `template` |
Yes |

### OpenAI.CreateEvalCompletionsRunDataSourceSamplingParams

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| max_completion_tokens |
|

[OpenAI.ReasoningEffort](#openaireasoningeffort)Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

determine how to respond in the format.

underscores and dashes, with a maximum length of 64.

If set to true, the model will always follow the exact schema defined

in the

`schema`

field. Only a subset of JSON Schema is supported when`strict`

is `true`

. To learn more, read the [Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)

guide.guide

`json_object`

.Possible values:

`json_object`

### OpenAI.CreateEvalCustomDataSourceConfig

A CustomDataSourceConfig object that defines the schema for the data source used for the evaluation runs. This schema is used to define the shape of the data that will be:

- Used to define your testing criteria and
- What data is required when creating a run

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| include_sample_schema | boolean | Whether the eval should expect you to populate the sample namespace (ie, by generating responses off of your data source) | No | |
| item_schema | object | The json schema for each row in the data source. | Yes | |
| type | enum | The type of data source. Always `custom` .Possible values: `custom` |
Yes |

### OpenAI.CreateEvalJsonlRunDataSource

A JsonlRunDataSource object with that specifies a JSONL file that matches the eval

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| source | object | Yes | ||
| └─ content | array | The content of the jsonl file. | No | |
| └─ id | string | The identifier of the file. | No | |
| └─ type | enum | The type of jsonl source. Always `file_id` .Possible values: `file_id` |
No | |
| type | enum | The type of data source. Always `jsonl` .Possible values: `jsonl` |
Yes |

### OpenAI.CreateEvalLogsDataSourceConfig

A data source config which specifies the metadata property of your logs query.
This is usually metadata like `usecase=chatbot`

or `prompt-version=v2`

, etc.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| metadata | object | Metadata filters for the logs data source. | No | |
| type | enum | The type of data source. Always `logs` .Possible values: `logs` |
Yes |

### OpenAI.CreateEvalResponsesRunDataSource

A ResponsesRunDataSource object describing a model sampling configuration.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input_messages | object | No | ||
| └─ item_reference | string | No | ||
| └─ template | array | No | ||
| └─ type | enum | Possible values: `item_reference` |
No | |
| model | string | The name of the model to use for generating completions (e.g. "o3-mini"). | No | |
| sampling_params |
|

[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.ReasoningEffort](#openaireasoningeffort)Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

[OpenAI.numeric](#openainumeric)[OpenAI.numeric](#openainumeric)`responses`

.Possible values:

`responses`

`responses`

.Possible values:

`responses`

### OpenAI.CreateEvalResponsesRunDataSourceInputMessagesItemReference

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_reference | string | Yes | ||
| type | enum | Possible values: `item_reference` |
Yes |

### OpenAI.CreateEvalResponsesRunDataSourceInputMessagesTemplate

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| template | array | Yes | ||
| type | enum | Possible values: `template` |
Yes |

### OpenAI.CreateEvalResponsesRunDataSourceSamplingParams

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| max_completion_tokens |
|

[OpenAI.ReasoningEffort](#openaireasoningeffort)Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

[OpenAI.CreateEvalResponsesRunDataSourceSamplingParamsText](#openaicreateevalresponsesrundatasourcesamplingparamstext)### OpenAI.CreateEvalResponsesRunDataSourceSamplingParamsText

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| format |
|

Configuring

`{ "type": "json_schema" }`

enables Structured Outputs,which ensures the model will match your supplied JSON schema. Learn more in the

The default format is

`{ "type": "text" }`

with no additional options.*Not recommended for gpt-4o and newer models:**

Setting to

`{ "type": "json_object" }`

enables the older JSON mode, whichensures the message the model generates is valid JSON. Using

`json_schema`

is preferred for models that support it.

### OpenAI.CreateEvalStoredCompletionsDataSourceConfig

Deprecated in favor of LogsDataSourceConfig.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| metadata | object | Metadata filters for the stored completions data source. | No | |
| type | enum | The type of data source. Always `stored_completions` .Possible values: `stored_completions` |
Yes |

### OpenAI.CreateFineTuningJobRequest

**Valid models:**

```
babbage-002
davinci-002
gpt-3.5-turbo
gpt-4o-mini
```


| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| hyperparameters | object | The hyperparameters used for the fine-tuning job. This value is now deprecated in favor of `method` , and should be passed in under the `method` parameter. |
No | |
| └─ batch_size | enum | Possible values: `auto` |
No | |
| └─ learning_rate_multiplier | enum | Possible values: `auto` |
No | |
| └─ n_epochs | enum | Possible values: `auto` |
No | |
| integrations | array | A list of integrations to enable for your fine-tuning job. | No | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No | |
| method |
|

[supported models](https://platform.openai.com/docs/guides/fine-tuning#which-models-can-be-fine-tuned).If a seed is not specified, one will be generated for you.

For example, a

`suffix`

of "custom-model-name" would produce a model name like `ft:gpt-4o-mini:openai:custom-model-name:7p4lURel`

.Your dataset must be formatted as a JSONL file. Additionally, you must upload your file with the purpose

`fine-tune`

.The contents of the file should differ depending on if the model uses the chat, completions format, or if the fine-tuning method uses the preference format.

See the

[fine-tuning guide](https://platform.openai.com/docs/guides/model-optimization)for more details.If you provide this file, the data is used to generate validation

metrics periodically during fine-tuning. These metrics can be viewed in

the fine-tuning results file.

The same data should not be present in both train and validation files.

Your dataset must be formatted as a JSONL file. You must upload your file with the purpose

`fine-tune`

.See the

[fine-tuning guide](https://platform.openai.com/docs/guides/model-optimization)for more details.### OpenAI.CreateFineTuningJobRequestIntegration

### Discriminator for OpenAI.CreateFineTuningJobRequestIntegration

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`wandb` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | string (see valid models below) | Yes |

### OpenAI.CreateFineTuningJobRequestWandbIntegration

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `wandb` |
Yes | |
| wandb | object | Yes | ||
| └─ entity | string | No | ||
| └─ name | string | No | ||
| └─ project | string | No | ||
| └─ tags | array | No |

### OpenAI.CreateResponse

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| agent | object | No | ||
| └─ name | string | The name of the agent. | No | |
| └─ type | enum | Possible values: `agent_reference` |
No | |
| └─ version | string | The version identifier of the agent. | No | |
| background | boolean | Whether to run the model response in the background.
|
No | False |
| conversation | object | No | ||
| └─ id | string | No | ||
| include | array | Specify additional output data to include in the model response. Currently supported values are: - `code_interpreter_call.outputs` : Includes the outputs of python code executionin code interpreter tool call items. - `computer_call_output.output.image_url` : Include image urls from the computer call output.- `file_search_call.results` : Include the search results ofthe file search tool call. - `message.input_image.image_url` : Include image urls from the input message.- `message.output_text.logprobs` : Include logprobs with assistant messages.- `reasoning.encrypted_content` : Includes an encrypted version of reasoningtokens in reasoning item outputs. This enables reasoning items to be used in multi-turn conversations when using the Responses API statelessly (like when the `store` parameter is set to `false` , or when an organization isenrolled in the zero data retention program). |
No | |
| input | string or array | No | ||
| instructions | string | A system (or developer) message inserted into the model's context. When using along with `previous_response_id` , the instructions from a previousresponse will not be carried over to the next response. This makes it simple to swap out system (or developer) messages in new responses. |
No | |
| max_output_tokens | integer | An upper bound for the number of tokens that can be generated for a response, including visible output tokens and
|

useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

create multi-turn conversations. Learn more about

[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).[OpenAI.ResponsePromptVariables](#openairesponsepromptvariables)prompt. The substitution values can either be strings, or other

Response input types like images or files.

**o-series models only**Configuration options for reasoning models.

[OpenAI.ReasoningEffort](#openaireasoningeffort)Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

**Deprecated**: use`summary`

instead. A summary of the reasoning performed by the model. This can be useful for debugging and understanding the model's reasoning process. One of `auto`

, `concise`

, or `detailed`

.Possible values:

`auto`

, `concise`

, `detailed`

useful for debugging and understanding the model's reasoning process.

One of

`auto`

, `concise`

, or `detailed`

.Possible values:

`auto`

, `concise`

, `detailed`

* If set to 'auto', then the request will be processed with the service tier

configured in the Project settings. Unless otherwise configured, the Project will use 'default'.

* If set to 'default', then the request will be processed with the standard

pricing and performance for the selected model.

* If set to '

[flex](https://platform.openai.com/docs/guides/flex-processing)'or 'priority', then the request will be processed with the corresponding service

tier.

[Contact sales](https://openai.com/contact-sales)to learn more about Priority processing.* When not set, the default behavior is 'auto'.

When the

`service_tier`

parameter is set, the response body will include the `service_tier`

value based on the processing mode actually used to serve the request. This response value

may be different from the value set in the parameter.

API.

as it is generated using server-sent events.

for more information.

We generally recommend altering this or

`top_p`

but not both.text or structured JSON data. See

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)and

[Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)`none`

means the model will not call any tool and instead generates a message.`auto`

means the model can pick between generating a message or calling one ormore tools.

`required`

means the model must call one or more tools.[OpenAI.ToolChoiceObjectType](#openaitoolchoiceobjecttype)[Learn more about built-in tools](https://platform.openai.com/docs/guides/tools).can specify which tool to use by setting the

`tool_choice`

parameter.The two categories of tools you can provide the model are:

-

**Built-in tools**: Tools that are provided by OpenAI that extend themodel's capabilities, like file search.

-

**Function calls (custom tools)**: Functions that are defined by you,enabling the model to call your own code.

where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.-

`auto`

: If the context of this response and previous ones exceedsthe model's context window size, the model will truncate the

response to fit the context window by dropping input items in the

middle of the conversation.

-

`disabled`

(default): If a model response will exceed the context windowsize for a model, the request will fail with a 400 error.

Possible values:

`auto`

, `disabled`

[Learn more about safety best practices](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).### OpenAI.DeletedConversationResource

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| deleted | boolean | Yes | ||
| id | string | Yes | ||
| object | enum | Possible values: `conversation.deleted` |
Yes |

### OpenAI.EasyInputMessage

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | string or array | Yes | ||
| role | string | Yes |

### OpenAI.Error

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| additionalInfo | object | No | ||
| code | string | Yes | ||
| debugInfo | object | No | ||
| details | array | No | ||
| message | string | Yes | ||
| param | string | Yes | ||
| type | string | Yes |

### OpenAI.EvalApiError

An object representing an error response from the Eval API.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code | string | The error code. | Yes | |
| message | string | The error message. | Yes |

### OpenAI.EvalGraderLabelModel

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input | array | Yes | ||
| labels | array | The labels to assign to each item in the evaluation. | Yes | |
| model | string | The model to use for the evaluation. Must support structured outputs. | Yes | |
| name | string | The name of the grader. | Yes | |
| passing_labels | array | The labels that indicate a passing result. Must be a subset of labels. | Yes | |
| type | enum | The object type, which is always `label_model` .Possible values: `label_model` |
Yes |

### OpenAI.EvalGraderPython

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| image_tag | string | The image tag to use for the python script. | No | |
| name | string | The name of the grader. | Yes | |
| pass_threshold | object | No | ||
| source | string | The source code of the python script. | Yes | |
| type | enum | The object type, which is always `python` .Possible values: `python` |
Yes |

### OpenAI.EvalGraderScoreModel

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input | array | The input text. This may include template strings. | Yes | |
| model | string | The model to use for the evaluation. | Yes | |
| name | string | The name of the grader. | Yes | |
| pass_threshold | object | No | ||
| range | array | The range of the score. Defaults to `[0, 1]` . |
No | |
| sampling_params | object | No | ||
| └─ max_completions_tokens |
|

[OpenAI.ReasoningEffort](#openaireasoningeffort)Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

[OpenAI.integer](#openaiinteger)[OpenAI.numeric](#openainumeric)[OpenAI.numeric](#openainumeric)`score_model`

.Possible values:

`score_model`

### OpenAI.EvalGraderScoreModelSamplingParams

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| max_completions_tokens | object | No | ||
| reasoning_effort |
|

Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

### OpenAI.EvalGraderStringCheck

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input | string | The input text. This may include template strings. | Yes | |
| name | string | The name of the grader. | Yes | |
| operation | enum | The string check operation to perform. One of `eq` , `ne` , `like` , or `ilike` .Possible values: `eq` , `ne` , `like` , `ilike` |
Yes | |
| reference | string | The reference text. This may include template strings. | Yes | |
| type | enum | The object type, which is always `string_check` .Possible values: `string_check` |
Yes |

### OpenAI.EvalGraderTextSimilarity

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| evaluation_metric | enum | The evaluation metric to use. One of `cosine` , `fuzzy_match` , `bleu` ,`gleu` , `meteor` , `rouge_1` , `rouge_2` , `rouge_3` , `rouge_4` , `rouge_5` ,or `rouge_l` .Possible values: `cosine` , `fuzzy_match` , `bleu` , `gleu` , `meteor` , `rouge_1` , `rouge_2` , `rouge_3` , `rouge_4` , `rouge_5` , `rouge_l` |
Yes | |
| input | string | The text being graded. | Yes | |
| name | string | The name of the grader. | Yes | |
| pass_threshold | object | Yes | ||
| reference | string | The text being graded against. | Yes | |
| type | enum | The type of grader. Possible values: `text_similarity` |
Yes |

### OpenAI.EvalItem

A message input to the model with a role indicating instruction following
hierarchy. Instructions given with the `developer`

or `system`

role take
precedence over instructions given with the `user`

role. Messages with the
`assistant`

role are presumed to have been generated by the model in previous
interactions.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | object | A text input to the model. | Yes | |
| └─ data | string | Base64-encoded audio data. | No | |
| └─ detail | string | No | ||
| └─ format | enum | The format of the audio data. Currently supported formats are `mp3` and`wav` .Possible values: `mp3` , `wav` |
No | |
| └─ image_url | string | No | ||
| └─ text | string | No | ||
| └─ type | enum | The type of the input item. Always `input_audio` .Possible values: `input_audio` |
No | |
| role | enum | The role of the message input. One of `user` , `assistant` , `system` , or`developer` .Possible values: `user` , `assistant` , `system` , `developer` |
Yes | |
| type | enum | The type of the message input. Always `message` .Possible values: `message` |
No |

### OpenAI.EvalItemContentInputImage

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| detail | string | No | ||
| image_url | string | Yes | ||
| type | enum | Possible values: `input_image` |
Yes |

### OpenAI.EvalItemContentOutputText

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| text | string | Yes | ||
| type | enum | Possible values: `output_text` |
Yes |

### OpenAI.EvalJsonlFileContentSource

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | array | The content of the jsonl file. | Yes | |
| type | enum | The type of jsonl source. Always `file_content` .Possible values: `file_content` |
Yes |

### OpenAI.EvalJsonlFileContentSourceContent

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item | object | Yes | ||
| sample | object | No |

### OpenAI.EvalJsonlFileIdSource

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| id | string | The identifier of the file. | Yes | |
| type | enum | The type of jsonl source. Always `file_id` .Possible values: `file_id` |
Yes |

### OpenAI.EvalResponsesSource

A EvalResponsesSource object describing a run data source configuration.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_after | object | No | ||
| created_before | object | No | ||
| instructions_search | string | No | ||
| metadata | object | No | ||
| model | string | No | ||
| reasoning_effort | object | Constrains effort on reasoning for reasoning models. Currently supported values are none, minimal, low, medium, and high. Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response. gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1. All models before gpt-5.1 default to medium reasoning effort, and do not support none. The gpt-5-pro model defaults to (and only supports) high reasoning effort. |
No | |
| temperature | object | No | ||
| tools | array | No | ||
| top_p | object | No | ||
| type | enum | The type of run data source. Always `responses` .Possible values: `responses` |
Yes | |
| users | array | No |

### OpenAI.EvalRunOutputItemSample

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| error |
|

[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.numeric](#openainumeric)[OpenAI.numeric](#openainumeric)[OpenAI.EvalRunOutputItemSampleUsage](#openaievalrunoutputitemsampleusage)### OpenAI.EvalRunOutputItemSampleInput

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | string | Yes | ||
| role | string | Yes |

### OpenAI.EvalRunOutputItemSampleOutput

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | string | No | ||
| role | string | No |

### OpenAI.EvalRunOutputItemSampleUsage

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| cached_tokens |
|

[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)### OpenAI.EvalRunPerModelUsage

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| cached_tokens |
|

[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)### OpenAI.EvalRunPerTestingCriteriaResults

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| failed |
|

[OpenAI.integer](#openaiinteger)### OpenAI.EvalRunResultCounts

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| errored |
|

[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)[OpenAI.integer](#openaiinteger)### OpenAI.EvalStoredCompletionsSource

A StoredCompletionsRunDataSource configuration describing a set of filters

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_after | object | No | ||
| created_before | object | No | ||
| limit | object | No | ||
| metadata |
|

useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

`stored_completions`

.Possible values:

`stored_completions`

### OpenAI.FileSearchTool

A tool that searches for relevant content from uploaded files.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| filters | object | No | ||
| max_num_results | integer | The maximum number of results to return. This number should be between 1 and 50 inclusive. | No | |
| ranking_options | object | No | ||
| └─ ranker | enum | The ranker to use for the file search. Possible values: `auto` , `default-2024-11-15` |
No | |
| └─ score_threshold | number | The score threshold for the file search, a number between 0 and 1. Numbers closer to 1 will attempt to return only the most relevant results, but may return fewer results. | No | |
| type | enum | The type of the file search tool. Always `file_search` .Possible values: `file_search` |
Yes | |
| vector_store_ids | array | The IDs of the vector stores to search. | Yes |

### OpenAI.FileSearchToolCallItemParam

The results of a file search tool call. See the
[file search guide](https://platform.openai.com/docs/guides/tools-file-search) for more information.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| queries | array | The queries used to search for files. | Yes | |
| results | array | The results of the file search tool call. | No | |
| type | enum | Possible values: `file_search_call` |
Yes |

### OpenAI.FileSearchToolCallItemResource

The results of a file search tool call. See the
[file search guide](https://platform.openai.com/docs/guides/tools-file-search) for more information.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| queries | array | The queries used to search for files. | Yes | |
| results | array | The results of the file search tool call. | No | |
| status | enum | The status of the file search tool call. One of `in_progress` ,`searching` , `incomplete` or `failed` ,Possible values: `in_progress` , `searching` , `completed` , `incomplete` , `failed` |
Yes | |
| type | enum | Possible values: `file_search_call` |
Yes |

### OpenAI.Filters

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| filters | array | Array of filters to combine. Items can be `ComparisonFilter` or `CompoundFilter` . |
Yes | |
| key | string | The key to compare against the value. | Yes | |
| type | enum | Type of operation: `and` or `or` .Possible values: `and` , `or` |
Yes | |
| value | string or number or boolean | The value to compare against the attribute key; supports string, number, or boolean types. | Yes |

### OpenAI.FineTuneDPOHyperparameters

The hyperparameters used for the DPO fine-tuning job.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| batch_size | enum | Possible values: `auto` |
No | |
| beta | enum | Possible values: `auto` |
No | |
| learning_rate_multiplier | enum | Possible values: `auto` |
No | |
| n_epochs | enum | Possible values: `auto` |
No |

### OpenAI.FineTuneDPOMethod

Configuration for the DPO fine-tuning method.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| hyperparameters |
|

### OpenAI.FineTuneMethod

The method used for fine-tuning.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| dpo |
|

[OpenAI.FineTuneReinforcementMethod](#openaifinetunereinforcementmethod)[OpenAI.FineTuneSupervisedMethod](#openaifinetunesupervisedmethod)`supervised`

, `dpo`

, or `reinforcement`

.Possible values:

`supervised`

, `dpo`

, `reinforcement`

### OpenAI.FineTuneReinforcementHyperparameters

The hyperparameters used for the reinforcement fine-tuning job.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| batch_size | enum | Possible values: `auto` |
No | |
| compute_multiplier | enum | Possible values: `auto` |
No | |
| eval_interval | enum | Possible values: `auto` |
No | |
| eval_samples | enum | Possible values: `auto` |
No | |
| learning_rate_multiplier | enum | Possible values: `auto` |
No | |
| n_epochs | enum | Possible values: `auto` |
No | |
| reasoning_effort | enum | Level of reasoning effort. Possible values: `default` , `low` , `medium` , `high` |
No |

### OpenAI.FineTuneReinforcementMethod

Configuration for the reinforcement fine-tuning method.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| grader | object | A StringCheckGrader object that performs a string comparison between input and reference using a specified operation. | Yes | |
| └─ calculate_output | string | A formula to calculate the output based on grader results. | No | |
| └─ evaluation_metric | enum | The evaluation metric to use. One of `cosine` , `fuzzy_match` , `bleu` ,`gleu` , `meteor` , `rouge_1` , `rouge_2` , `rouge_3` , `rouge_4` , `rouge_5` ,or `rouge_l` .Possible values: `cosine` , `fuzzy_match` , `bleu` , `gleu` , `meteor` , `rouge_1` , `rouge_2` , `rouge_3` , `rouge_4` , `rouge_5` , `rouge_l` |
No | |
| └─ graders |
|

`eq`

, `ne`

, `like`

, or `ilike`

.Possible values:

`eq`

, `ne`

, `like`

, `ilike`

`[0, 1]`

.[OpenAI.EvalGraderScoreModelSamplingParams](#openaievalgraderscoremodelsamplingparams)`multi`

.Possible values:

`multi`

[OpenAI.FineTuneReinforcementHyperparameters](#openaifinetunereinforcementhyperparameters)### OpenAI.FineTuneSupervisedHyperparameters

The hyperparameters used for the fine-tuning job.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| batch_size | enum | Possible values: `auto` |
No | |
| learning_rate_multiplier | enum | Possible values: `auto` |
No | |
| n_epochs | enum | Possible values: `auto` |
No |

### OpenAI.FineTuneSupervisedMethod

Configuration for the supervised fine-tuning method.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| hyperparameters |
|

### OpenAI.FineTuningIntegration

### Discriminator for OpenAI.FineTuningIntegration

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`wandb` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | string (see valid models below) | Yes |

### OpenAI.FineTuningIntegrationWandb

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of the integration being enabled for the fine-tuning job Possible values: `wandb` |
Yes | |
| wandb | object | The settings for your integration with Weights and Biases. This payload specifies the project that metrics will be sent to. Optionally, you can set an explicit display name for your run, add tags to your run, and set a default entity (team, username, etc) to be associated with your run. |
Yes | |
| └─ entity | string | The entity to use for the run. This allows you to set the team or username of the WandB user that you would like associated with the run. If not set, the default entity for the registered WandB API key is used. |
No | |
| └─ name | string | A display name to set for the run. If not set, we will use the Job ID as the name. | No | |
| └─ project | string | The name of the project that the new run will be created under. | No | |
| └─ tags | array | A list of tags to be attached to the newly created run. These tags are passed through directly to WandB. Some default tags are generated by OpenAI: "openai/finetune", "openai/{base-model}", "openai/{ftjob-abcdef}". |
No |

### OpenAI.FineTuningJob

The `fine_tuning.job`

object represents a fine-tuning job that has been created through the API.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | integer | The Unix timestamp (in seconds) for when the fine-tuning job was created. | Yes | |
| error | object | For fine-tuning jobs that have `failed` , this will contain more information on the cause of the failure. |
Yes | |
| └─ code | string | A machine-readable error code. | No | |
| └─ message | string | A human-readable error message. | No | |
| └─ param | string | The parameter that was invalid, usually `training_file` or `validation_file` . This field will be null if the failure was not parameter-specific. |
No | |
| estimated_finish | integer | The Unix timestamp (in seconds) for when the fine-tuning job is estimated to finish. The value will be null if the fine-tuning job is not running. | No | |
| fine_tuned_model | string | The name of the fine-tuned model that is being created. The value will be null if the fine-tuning job is still running. | Yes | |
| finished_at | integer | The Unix timestamp (in seconds) for when the fine-tuning job was finished. The value will be null if the fine-tuning job is still running. | Yes | |
| hyperparameters | object | The hyperparameters used for the fine-tuning job. This value will only be returned when running `supervised` jobs. |
Yes | |
| └─ batch_size | enum | Possible values: `auto` |
No | |
| └─ learning_rate_multiplier | enum | Possible values: `auto` |
No | |
| └─ n_epochs | enum | Possible values: `auto` |
No | |
| id | string | The object identifier, which can be referenced in the API endpoints. | Yes | |
| integrations | array | A list of integrations to enable for this fine-tuning job. | No | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
Yes | |
| method |
|

Possible values:

`fine_tuning.job`

`validating_files`

, `queued`

, `running`

, `succeeded`

, `failed`

, or `cancelled`

.Possible values:

`validating_files`

, `queued`

, `running`

, `succeeded`

, `failed`

, `cancelled`

### OpenAI.FineTuningJobCheckpoint

The `fine_tuning.job.checkpoint`

object represents a model checkpoint for a fine-tuning job that is ready to use.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | integer | The Unix timestamp (in seconds) for when the checkpoint was created. | Yes | |
| fine_tuned_model_checkpoint | string | The name of the fine-tuned checkpoint model that is created. | Yes | |
| fine_tuning_job_id | string | The name of the fine-tuning job that this checkpoint was created from. | Yes | |
| id | string | The checkpoint identifier, which can be referenced in the API endpoints. | Yes | |
| metrics | object | Metrics at the step number during the fine-tuning job. | Yes | |
| └─ full_valid_loss | number | No | ||
| └─ full_valid_mean_token_accuracy | number | No | ||
| └─ step | number | No | ||
| └─ train_loss | number | No | ||
| └─ train_mean_token_accuracy | number | No | ||
| └─ valid_loss | number | No | ||
| └─ valid_mean_token_accuracy | number | No | ||
| object | enum | The object type, which is always "fine_tuning.job.checkpoint". Possible values: `fine_tuning.job.checkpoint` |
Yes | |
| step_number | integer | The step number that the checkpoint was created at. | Yes |

### OpenAI.FineTuningJobEvent

Fine-tuning job event object

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_at | integer | The Unix timestamp (in seconds) for when the fine-tuning job was created. | Yes | |
| data | The data associated with the event. | No | ||
| id | string | The object identifier. | Yes | |
| level | enum | The log level of the event. Possible values: `info` , `warn` , `error` |
Yes | |
| message | string | The message of the event. | Yes | |
| object | enum | The object type, which is always "fine_tuning.job.event". Possible values: `fine_tuning.job.event` |
Yes | |
| type | enum | The type of event. Possible values: `message` , `metrics` |
No |

### OpenAI.FunctionObject

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A description of what the function does, used by the model to choose when and how to call the function. | No | |
| name | string | The name of the function to be called. Must be a-z, A-Z, 0-9, or contain underscores and dashes, with a maximum length of 64. | Yes | |
| parameters | The parameters the functions accepts, described as a JSON Schema object. See the
Omitting `parameters` defines a function with an empty parameter list. |

`parameters`

field. Only a subset of JSON Schema is supported when `strict`

is `true`

. Learn more about Structured Outputs in the### OpenAI.FunctionTool

Defines a function in your own code the model can choose to call.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A description of the function. Used by the model to determine whether or not to call the function. | No | |
| name | string | The name of the function to call. | Yes | |
| parameters | A JSON schema object describing the parameters of the function. | Yes | ||
| strict | boolean | Whether to enforce strict parameter validation. Default `true` . |
Yes | |
| type | enum | The type of the function tool. Always `function` .Possible values: `function` |
Yes |

### OpenAI.FunctionToolCallItemParam

A tool call to run a function. See the
[function calling guide](https://platform.openai.com/docs/guides/function-calling) for more information.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| arguments | string | A JSON string of the arguments to pass to the function. | Yes | |
| call_id | string | The unique ID of the function tool call generated by the model. | Yes | |
| name | string | The name of the function to run. | Yes | |
| type | enum | Possible values: `function_call` |
Yes |

### OpenAI.FunctionToolCallItemResource

A tool call to run a function. See the
[function calling guide](https://platform.openai.com/docs/guides/function-calling) for more information.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| arguments | string | A JSON string of the arguments to pass to the function. | Yes | |
| call_id | string | The unique ID of the function tool call generated by the model. | Yes | |
| name | string | The name of the function to run. | Yes | |
| status | enum | The status of the item. One of `in_progress` , `completed` , or`incomplete` . Populated when items are returned via API.Possible values: `in_progress` , `completed` , `incomplete` |
Yes | |
| type | enum | Possible values: `function_call` |
Yes |

### OpenAI.FunctionToolCallOutputItemParam

The output of a function tool call.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| call_id | string | The unique ID of the function tool call generated by the model. | Yes | |
| output | string | A JSON string of the output of the function tool call. | Yes | |
| type | enum | Possible values: `function_call_output` |
Yes |

### OpenAI.FunctionToolCallOutputItemResource

The output of a function tool call.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| call_id | string | The unique ID of the function tool call generated by the model. | Yes | |
| output | string | A JSON string of the output of the function tool call. | Yes | |
| status | enum | The status of the item. One of `in_progress` , `completed` , or`incomplete` . Populated when items are returned via API.Possible values: `in_progress` , `completed` , `incomplete` |
Yes | |
| type | enum | Possible values: `function_call_output` |
Yes |

### OpenAI.GraderLabelModel

A LabelModelGrader object which uses a model to assign labels to each item in the evaluation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input | array | Yes | ||
| labels | array | The labels to assign to each item in the evaluation. | Yes | |
| model | string | The model to use for the evaluation. Must support structured outputs. | Yes | |
| name | string | The name of the grader. | Yes | |
| passing_labels | array | The labels that indicate a passing result. Must be a subset of labels. | Yes | |
| type | enum | The object type, which is always `label_model` .Possible values: `label_model` |
Yes |

### OpenAI.GraderMulti

A MultiGrader object combines the output of multiple graders to produce a single score.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| calculate_output | string | A formula to calculate the output based on grader results. | Yes | |
| graders | object | A StringCheckGrader object that performs a string comparison between input and reference using a specified operation. | Yes | |
| └─ evaluation_metric | enum | The evaluation metric to use. One of `cosine` , `fuzzy_match` , `bleu` ,`gleu` , `meteor` , `rouge_1` , `rouge_2` , `rouge_3` , `rouge_4` , `rouge_5` ,or `rouge_l` .Possible values: `cosine` , `fuzzy_match` , `bleu` , `gleu` , `meteor` , `rouge_1` , `rouge_2` , `rouge_3` , `rouge_4` , `rouge_5` , `rouge_l` |
No | |
| └─ image_tag | string | The image tag to use for the python script. | No | |
| └─ input | array | No | ||
| └─ labels | array | The labels to assign to each item in the evaluation. | No | |
| └─ model | string | The model to use for the evaluation. Must support structured outputs. | No | |
| └─ name | string | The name of the grader. | No | |
| └─ operation | enum | The string check operation to perform. One of `eq` , `ne` , `like` , or `ilike` .Possible values: `eq` , `ne` , `like` , `ilike` |
No | |
| └─ passing_labels | array | The labels that indicate a passing result. Must be a subset of labels. | No | |
| └─ range | array | The range of the score. Defaults to `[0, 1]` . |
No | |
| └─ reference | string | The text being graded against. | No | |
| └─ sampling_params |
|

`label_model`

.Possible values:

`label_model`

`multi`

.Possible values:

`multi`

### OpenAI.GraderPython

A PythonGrader object that runs a python script on the input.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| image_tag | string | The image tag to use for the python script. | No | |
| name | string | The name of the grader. | Yes | |
| source | string | The source code of the python script. | Yes | |
| type | enum | The object type, which is always `python` .Possible values: `python` |
Yes |

### OpenAI.GraderScoreModel

A ScoreModelGrader object that uses a model to assign a score to the input.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input | array | The input text. This may include template strings. | Yes | |
| model | string | The model to use for the evaluation. | Yes | |
| name | string | The name of the grader. | Yes | |
| range | array | The range of the score. Defaults to `[0, 1]` . |
No | |
| sampling_params | object | No | ||
| └─ max_completions_tokens |
|

[OpenAI.ReasoningEffort](#openaireasoningeffort)Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

[OpenAI.integer](#openaiinteger)[OpenAI.numeric](#openainumeric)[OpenAI.numeric](#openainumeric)`score_model`

.Possible values:

`score_model`

### OpenAI.GraderStringCheck

A StringCheckGrader object that performs a string comparison between input and reference using a specified operation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input | string | The input text. This may include template strings. | Yes | |
| name | string | The name of the grader. | Yes | |
| operation | enum | The string check operation to perform. One of `eq` , `ne` , `like` , or `ilike` .Possible values: `eq` , `ne` , `like` , `ilike` |
Yes | |
| reference | string | The reference text. This may include template strings. | Yes | |
| type | enum | The object type, which is always `string_check` .Possible values: `string_check` |
Yes |

### OpenAI.GraderTextSimilarity

A TextSimilarityGrader object which grades text based on similarity metrics.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| evaluation_metric | enum | The evaluation metric to use. One of `cosine` , `fuzzy_match` , `bleu` ,`gleu` , `meteor` , `rouge_1` , `rouge_2` , `rouge_3` , `rouge_4` , `rouge_5` ,or `rouge_l` .Possible values: `cosine` , `fuzzy_match` , `bleu` , `gleu` , `meteor` , `rouge_1` , `rouge_2` , `rouge_3` , `rouge_4` , `rouge_5` , `rouge_l` |
Yes | |
| input | string | The text being graded. | Yes | |
| name | string | The name of the grader. | Yes | |
| reference | string | The text being graded against. | Yes | |
| type | enum | The type of grader. Possible values: `text_similarity` |
Yes |

### OpenAI.ImageGenTool

A tool that generates images using a model like `gpt-image-1`

.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| background | enum | Background type for the generated image. One of `transparent` ,`opaque` , or `auto` . Default: `auto` .Possible values: `transparent` , `opaque` , `auto` |
No | |
| input_image_mask | object | Optional mask for inpainting. Contains `image_url` (string, optional) and `file_id` (string, optional). |
No | |
| └─ file_id | string | File ID for the mask image. | No | |
| └─ image_url | string | Base64-encoded mask image. | No | |
| model | enum | The image generation model to use. Default: `gpt-image-1` .Possible values: `gpt-image-1` |
No | |
| moderation | enum | Moderation level for the generated image. Default: `auto` .Possible values: `auto` , `low` |
No | |
| output_compression | integer | Compression level for the output image. Default: 100. | No | 100 |
| output_format | enum | The output format of the generated image. One of `png` , `webp` , or`jpeg` . Default: `png` .Possible values: `png` , `webp` , `jpeg` |
No | |
| partial_images | integer | Number of partial images to generate in streaming mode, from 0 (default value) to 3. | No | 0 |
| quality | enum | The quality of the generated image. One of `low` , `medium` , `high` ,or `auto` . Default: `auto` .Possible values: `low` , `medium` , `high` , `auto` |
No | |
| size | enum | The size of the generated image. One of `1024x1024` , `1024x1536` ,`1536x1024` , or `auto` . Default: `auto` .Possible values: `1024x1024` , `1024x1536` , `1536x1024` , `auto` |
No | |
| type | enum | The type of the image generation tool. Always `image_generation` .Possible values: `image_generation` |
Yes |

### OpenAI.ImageGenToolCallItemParam

An image generation request made by the model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| result | string | The generated image encoded in base64. | Yes | |
| type | enum | Possible values: `image_generation_call` |
Yes |

### OpenAI.ImageGenToolCallItemResource

An image generation request made by the model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| result | string | The generated image encoded in base64. | Yes | |
| status | enum | Possible values: `in_progress` , `completed` , `generating` , `failed` |
Yes | |
| type | enum | Possible values: `image_generation_call` |
Yes |

### OpenAI.Includable

Specify additional output data to include in the model response. Currently supported values are:

`code_interpreter_call.outputs`

: Includes the outputs of python code execution in code interpreter tool call items.`computer_call_output.output.image_url`

: Include image urls from the computer call output.`file_search_call.results`

: Include the search results of the file search tool call.`message.input_image.image_url`

: Include image urls from the input message.`message.output_text.logprobs`

: Include logprobs with assistant messages.`reasoning.encrypted_content`

: Includes an encrypted version of reasoning tokens in reasoning item outputs. This enables reasoning items to be used in multi-turn conversations when using the Responses API statelessly (like when the`store`

parameter is set to`false`

, or when an organization is enrolled in the zero data retention program).

| Property | Value |
|---|---|
Description |
Specify additional output data to include in the model response. Currently supported values are: - `code_interpreter_call.outputs` : Includes the outputs of python code executionin code interpreter tool call items. - `computer_call_output.output.image_url` : Include image urls from the computer call output.- `file_search_call.results` : Include the search results ofthe file search tool call. - `message.input_image.image_url` : Include image urls from the input message.- `message.output_text.logprobs` : Include logprobs with assistant messages.- `reasoning.encrypted_content` : Includes an encrypted version of reasoningtokens in reasoning item outputs. This enables reasoning items to be used in multi-turn conversations when using the Responses API statelessly (like when the `store` parameter is set to `false` , or when an organization isenrolled in the zero data retention program). |
Type |
string |
Values |
`code_interpreter_call.outputs` `computer_call_output.output.image_url` `file_search_call.results` `message.input_image.image_url` `message.output_text.logprobs` `reasoning.encrypted_content` `web_search_call.results` `web_search_call.action.sources` `memory_search_call.results` |

### OpenAI.ItemContent

### Discriminator for OpenAI.ItemContent

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`input_audio` |
|

`output_audio`

[OpenAI.ItemContentOutputAudio](#openaiitemcontentoutputaudio)`refusal`

[OpenAI.ItemContentRefusal](#openaiitemcontentrefusal)`input_text`

[OpenAI.ItemContentInputText](#openaiitemcontentinputtext)`input_image`

[OpenAI.ItemContentInputImage](#openaiitemcontentinputimage)`input_file`

[OpenAI.ItemContentInputFile](#openaiitemcontentinputfile)`output_text`

[OpenAI.ItemContentOutputText](#openaiitemcontentoutputtext)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.ItemContentInputAudio

An audio input to the model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data | string | Base64-encoded audio data. | Yes | |
| format | enum | The format of the audio data. Currently supported formats are `mp3` and`wav` .Possible values: `mp3` , `wav` |
Yes | |
| type | enum | The type of the input item. Always `input_audio` .Possible values: `input_audio` |
Yes |

### OpenAI.ItemContentInputFile

A file input to the model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| file_data | string | The content of the file to be sent to the model. | No | |
| file_id | string | The ID of the file to be sent to the model. | No | |
| filename | string | The name of the file to be sent to the model. | No | |
| type | enum | The type of the input item. Always `input_file` .Possible values: `input_file` |
Yes |

### OpenAI.ItemContentInputImage

An image input to the model. Learn about [image inputs](https://platform.openai.com/docs/guides/vision).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| detail | enum | The detail level of the image to be sent to the model. One of `high` , `low` , or `auto` . Defaults to `auto` .Possible values: `low` , `high` , `auto` |
No | |
| file_id | string | The ID of the file to be sent to the model. | No | |
| image_url | string | The URL of the image to be sent to the model. A fully qualified URL or base64 encoded image in a data URL. | No | |
| type | enum | The type of the input item. Always `input_image` .Possible values: `input_image` |
Yes |

### OpenAI.ItemContentInputText

A text input to the model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| text | string | The text input to the model. | Yes | |
| type | enum | The type of the input item. Always `input_text` .Possible values: `input_text` |
Yes |

### OpenAI.ItemContentOutputAudio

An audio output from the model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data | string | Base64-encoded audio data from the model. | Yes | |
| transcript | string | The transcript of the audio data from the model. | Yes | |
| type | enum | The type of the output audio. Always `output_audio` .Possible values: `output_audio` |
Yes |

### OpenAI.ItemContentOutputText

A text output from the model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| annotations | array | The annotations of the text output. | Yes | |
| logprobs | array | No | ||
| text | string | The text output from the model. | Yes | |
| type | enum | The type of the output text. Always `output_text` .Possible values: `output_text` |
Yes |

### OpenAI.ItemContentRefusal

A refusal from the model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| refusal | string | The refusal explanationfrom the model. | Yes | |
| type | enum | The type of the refusal. Always `refusal` .Possible values: `refusal` |
Yes |

### OpenAI.ItemContentType

Multi-modal input and output contents.

| Property | Value |
|---|---|
Description |
Multi-modal input and output contents. |
Type |
string |
Values |
`input_text` `input_audio` `input_image` `input_file` `output_text` `output_audio` `refusal` |

### OpenAI.ItemParam

Content item used to generate a response.

### Discriminator for OpenAI.ItemParam

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`message` |
|

`function_call_output`

[OpenAI.FunctionToolCallOutputItemParam](#openaifunctiontoolcalloutputitemparam)`file_search_call`

[OpenAI.FileSearchToolCallItemParam](#openaifilesearchtoolcallitemparam)`computer_call`

[OpenAI.ComputerToolCallItemParam](#openaicomputertoolcallitemparam)`computer_call_output`

[OpenAI.ComputerToolCallOutputItemParam](#openaicomputertoolcalloutputitemparam)`web_search_call`

[OpenAI.WebSearchToolCallItemParam](#openaiwebsearchtoolcallitemparam)`function_call`

[OpenAI.FunctionToolCallItemParam](#openaifunctiontoolcallitemparam)`reasoning`

[OpenAI.ReasoningItemParam](#openaireasoningitemparam)`item_reference`

[OpenAI.ItemReferenceItemParam](#openaiitemreferenceitemparam)`image_generation_call`

[OpenAI.ImageGenToolCallItemParam](#openaiimagegentoolcallitemparam)`code_interpreter_call`

[OpenAI.CodeInterpreterToolCallItemParam](#openaicodeinterpretertoolcallitemparam)`local_shell_call`

[OpenAI.LocalShellToolCallItemParam](#openailocalshelltoolcallitemparam)`local_shell_call_output`

[OpenAI.LocalShellToolCallOutputItemParam](#openailocalshelltoolcalloutputitemparam)`mcp_list_tools`

[OpenAI.MCPListToolsItemParam](#openaimcplisttoolsitemparam)`mcp_approval_request`

[OpenAI.MCPApprovalRequestItemParam](#openaimcpapprovalrequestitemparam)`mcp_approval_response`

[OpenAI.MCPApprovalResponseItemParam](#openaimcpapprovalresponseitemparam)`mcp_call`

[OpenAI.MCPCallItemParam](#openaimcpcallitemparam)`memory_search_call`

[MemorySearchToolCallItemParam](#memorysearchtoolcallitemparam)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.ItemReferenceItemParam

An internal identifier for an item to reference.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| id | string | The service-originated ID of the previously generated response item being referenced. | Yes | |
| type | enum | Possible values: `item_reference` |
Yes |

### OpenAI.ItemResource

Content item used to generate a response.

### Discriminator for OpenAI.ItemResource

This component uses the property `type`

to discriminate between different types:

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| created_by | object | No | ||
| └─ agent |
|

[OpenAI.ItemType](#openaiitemtype)### OpenAI.ItemType

| Property | Value |
|---|---|
Type |
string |
Values |
`message` `file_search_call` `function_call` `function_call_output` `computer_call` `computer_call_output` `web_search_call` `reasoning` `item_reference` `image_generation_call` `code_interpreter_call` `local_shell_call` `local_shell_call_output` `mcp_list_tools` `mcp_approval_request` `mcp_approval_response` `mcp_call` `structured_outputs` `workflow_action` `memory_search_call` `oauth_consent_request` |

### OpenAI.ListFineTuningJobCheckpointsResponse

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data | array | Yes | ||
| first_id | string | No | ||
| has_more | boolean | Yes | ||
| last_id | string | No | ||
| object | enum | Possible values: `list` |
Yes |

### OpenAI.ListFineTuningJobEventsResponse

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data | array | Yes | ||
| has_more | boolean | Yes | ||
| object | enum | Possible values: `list` |
Yes |

### OpenAI.ListPaginatedFineTuningJobsResponse

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| data | array | Yes | ||
| has_more | boolean | Yes | ||
| object | enum | Possible values: `list` |
Yes |

### OpenAI.LocalShellExecAction

Execute a shell command on the server.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| command | array | The command to run. | Yes | |
| env | object | Environment variables to set for the command. | Yes | |
| timeout_ms | integer | Optional timeout in milliseconds for the command. | No | |
| type | enum | The type of the local shell action. Always `exec` .Possible values: `exec` |
Yes | |
| user | string | Optional user to run the command as. | No | |
| working_directory | string | Optional working directory to run the command in. | No |

### OpenAI.LocalShellTool

A tool that allows the model to execute shell commands in a local environment.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of the local shell tool. Always `local_shell` .Possible values: `local_shell` |
Yes |

### OpenAI.LocalShellToolCallItemParam

A tool call to run a command on the local shell.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| action |
|

Possible values:

`local_shell_call`

### OpenAI.LocalShellToolCallItemResource

A tool call to run a command on the local shell.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| action |
|

Possible values:

`in_progress`

, `completed`

, `incomplete`

Possible values:

`local_shell_call`

### OpenAI.LocalShellToolCallOutputItemParam

The output of a local shell tool call.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| output | string | A JSON string of the output of the local shell tool call. | Yes | |
| type | enum | Possible values: `local_shell_call_output` |
Yes |

### OpenAI.LocalShellToolCallOutputItemResource

The output of a local shell tool call.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| output | string | A JSON string of the output of the local shell tool call. | Yes | |
| status | enum | Possible values: `in_progress` , `completed` , `incomplete` |
Yes | |
| type | enum | Possible values: `local_shell_call_output` |
Yes |

### OpenAI.Location

### Discriminator for OpenAI.Location

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`approximate` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.LocationType

| Property | Value |
|---|---|
Type |
string |
Values |
`approximate` |

### OpenAI.LogProb

The log probability of a token.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| bytes | array | Yes | ||
| logprob | number | Yes | ||
| token | string | Yes | ||
| top_logprobs | array | Yes |

### OpenAI.MCPApprovalRequestItemParam

A request for human approval of a tool invocation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| arguments | string | A JSON string of arguments for the tool. | Yes | |
| name | string | The name of the tool to run. | Yes | |
| server_label | string | The label of the MCP server making the request. | Yes | |
| type | enum | Possible values: `mcp_approval_request` |
Yes |

### OpenAI.MCPApprovalRequestItemResource

A request for human approval of a tool invocation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| arguments | string | A JSON string of arguments for the tool. | Yes | |
| name | string | The name of the tool to run. | Yes | |
| server_label | string | The label of the MCP server making the request. | Yes | |
| type | enum | Possible values: `mcp_approval_request` |
Yes |

### OpenAI.MCPApprovalResponseItemParam

A response to an MCP approval request.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| approval_request_id | string | The ID of the approval request being answered. | Yes | |
| approve | boolean | Whether the request was approved. | Yes | |
| reason | string | Optional reason for the decision. | No | |
| type | enum | Possible values: `mcp_approval_response` |
Yes |

### OpenAI.MCPApprovalResponseItemResource

A response to an MCP approval request.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| approval_request_id | string | The ID of the approval request being answered. | Yes | |
| approve | boolean | Whether the request was approved. | Yes | |
| reason | string | Optional reason for the decision. | No | |
| type | enum | Possible values: `mcp_approval_response` |
Yes |

### OpenAI.MCPCallItemParam

An invocation of a tool on an MCP server.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| arguments | string | A JSON string of the arguments passed to the tool. | Yes | |
| error | string | The error from the tool call, if any. | No | |
| name | string | The name of the tool that was run. | Yes | |
| output | string | The output from the tool call. | No | |
| server_label | string | The label of the MCP server running the tool. | Yes | |
| type | enum | Possible values: `mcp_call` |
Yes |

### OpenAI.MCPCallItemResource

An invocation of a tool on an MCP server.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| arguments | string | A JSON string of the arguments passed to the tool. | Yes | |
| error | string | The error from the tool call, if any. | No | |
| name | string | The name of the tool that was run. | Yes | |
| output | string | The output from the tool call. | No | |
| server_label | string | The label of the MCP server running the tool. | Yes | |
| type | enum | Possible values: `mcp_call` |
Yes |

### OpenAI.MCPListToolsItemParam

A list of tools available on an MCP server.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| error | string | Error message if the server could not list tools. | No | |
| server_label | string | The label of the MCP server. | Yes | |
| tools | array | The tools available on the server. | Yes | |
| type | enum | Possible values: `mcp_list_tools` |
Yes |

### OpenAI.MCPListToolsItemResource

A list of tools available on an MCP server.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| error | string | Error message if the server could not list tools. | No | |
| server_label | string | The label of the MCP server. | Yes | |
| tools | array | The tools available on the server. | Yes | |
| type | enum | Possible values: `mcp_list_tools` |
Yes |

### OpenAI.MCPListToolsTool

A tool available on an MCP server.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| annotations | Additional annotations about the tool. | No | ||
| description | string | The description of the tool. | No | |
| input_schema | The JSON schema describing the tool's input. | Yes | ||
| name | string | The name of the tool. | Yes |

### OpenAI.MCPTool

Give the model access to additional tools via remote Model Context Protocol
(MCP) servers. [Learn more about MCP](https://platform.openai.com/docs/guides/tools-remote-mcp).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| allowed_tools | object | No | ||
| └─ tool_names | array | List of allowed tool names. | No | |
| headers | object | Optional HTTP headers to send to the MCP server. Use for authentication or other purposes. |
No | |
| project_connection_id | string | The connection ID in the project for the MCP server. The connection stores authentication and other connection details needed to connect to the MCP server. | No | |
| require_approval | object (see valid models below) | Specify which of the MCP server's tools require approval. | No | |
| server_label | string | A label for this MCP server, used to identify it in tool calls. | Yes | |
| server_url | string | The URL for the MCP server. | Yes | |
| type | enum | The type of the MCP tool. Always `mcp` .Possible values: `mcp` |
Yes |

### OpenAI.Metadata

Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters.

**Type**: object

### OpenAI.Prompt

Reference to a prompt template and its variables.
[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| id | string | The unique identifier of the prompt template to use. | Yes | |
| variables | object | Optional map of values to substitute in for variables in your prompt. The substitution values can either be strings, or other Response input types like images or files. |
No | |
| version | string | Optional version of the prompt template. | No |

### OpenAI.RankingOptions

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| ranker | enum | The ranker to use for the file search. Possible values: `auto` , `default-2024-11-15` |
No | |
| score_threshold | number | The score threshold for the file search, a number between 0 and 1. Numbers closer to 1 will attempt to return only the most relevant results, but may return fewer results. | No |

### OpenAI.Reasoning

**o-series models only**

Configuration options for reasoning models.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| effort | object | Constrains effort on reasoning for reasoning models. Currently supported values are none, minimal, low, medium, and high. Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response. gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1. All models before gpt-5.1 default to medium reasoning effort, and do not support none. The gpt-5-pro model defaults to (and only supports) high reasoning effort. |
No | |
| generate_summary | enum | Deprecated: use `summary` instead. A summary of the reasoning performed by the model. This can be useful for debugging and understanding the model's reasoning process. One of `auto` , `concise` , or `detailed` .Possible values: `auto` , `concise` , `detailed` |
No | |
| summary | enum | A summary of the reasoning performed by the model. This can be useful for debugging and understanding the model's reasoning process. One of `auto` , `concise` , or `detailed` .Possible values: `auto` , `concise` , `detailed` |
No |

### OpenAI.ReasoningEffort

Constrains effort on reasoning for reasoning models.

Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

| Property | Value |
|---|---|
Description |
Constrains effort on reasoning for reasoning models. Currently supported values are none, minimal, low, medium, and high. Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response. gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1. All models before gpt-5.1 default to medium reasoning effort, and do not support none. The gpt-5-pro model defaults to (and only supports) high reasoning effort. |
Type |
string |
Values |
`none` `minimal` `low` `medium` `high` |

### OpenAI.ReasoningItemParam

A description of the chain of thought used by a reasoning model while generating
a response. Be sure to include these items in your `input`

to the Responses API
for subsequent turns of a conversation if you are manually
[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| encrypted_content | string | The encrypted content of the reasoning item - populated when a response is generated with `reasoning.encrypted_content` in the `include` parameter. |
No | |
| summary | array | Reasoning text contents. | Yes | |
| type | enum | Possible values: `reasoning` |
Yes |

### OpenAI.ReasoningItemResource

A description of the chain of thought used by a reasoning model while generating
a response. Be sure to include these items in your `input`

to the Responses API
for subsequent turns of a conversation if you are manually
[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| encrypted_content | string | The encrypted content of the reasoning item - populated when a response is generated with `reasoning.encrypted_content` in the `include` parameter. |
No | |
| summary | array | Reasoning text contents. | Yes | |
| type | enum | Possible values: `reasoning` |
Yes |

### OpenAI.ReasoningItemSummaryPart

### Discriminator for OpenAI.ReasoningItemSummaryPart

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`summary_text` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.ReasoningItemSummaryPartType

| Property | Value |
|---|---|
Type |
string |
Values |
`summary_text` |

### OpenAI.ReasoningItemSummaryTextPart

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| text | string | Yes | ||
| type | enum | Possible values: `summary_text` |
Yes |

### OpenAI.Response

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| agent | object | No | ||
| └─ name | string | The name of the agent. | No | |
| └─ type | enum | Possible values: `agent_id` |
No | |
| └─ version | string | The version identifier of the agent. | No | |
| background | boolean | Whether to run the model response in the background.
|
No | False |
| conversation | object | Yes | ||
| └─ id | string | No | ||
| created_at | integer | Unix timestamp (in seconds) of when this Response was created. | Yes | |
| error | object | An error object returned when the model fails to generate a Response. | Yes | |
| └─ code |
|

Possible values:

`max_output_tokens`

, `content_filter`

[reasoning tokens](https://platform.openai.com/docs/guides/reasoning).useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

`response`

.Possible values:

`response`

- The length and order of items in the

`output`

array is dependenton the model's response.

- Rather than accessing the first item in the

`output`

array andassuming it's an

`assistant`

message with the content generated bythe model, you might consider using the

`output_text`

property wheresupported in SDKs.

from all

`output_text`

items in the `output`

array, if any are present.Supported in the Python and JavaScript SDKs.

create multi-turn conversations. Learn more about

[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).[OpenAI.ResponsePromptVariables](#openairesponsepromptvariables)prompt. The substitution values can either be strings, or other

Response input types like images or files.

**o-series models only**Configuration options for reasoning models.

[OpenAI.ReasoningEffort](#openaireasoningeffort)Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

**Deprecated**: use`summary`

instead. A summary of the reasoning performed by the model. This can be useful for debugging and understanding the model's reasoning process. One of `auto`

, `concise`

, or `detailed`

.Possible values:

`auto`

, `concise`

, `detailed`

useful for debugging and understanding the model's reasoning process.

One of

`auto`

, `concise`

, or `detailed`

.Possible values:

`auto`

, `concise`

, `detailed`

* If set to 'auto', then the request will be processed with the service tier

configured in the Project settings. Unless otherwise configured, the Project will use 'default'.

* If set to 'default', then the request will be processed with the standard

pricing and performance for the selected model.

* If set to '

[flex](https://platform.openai.com/docs/guides/flex-processing)'or 'priority', then the request will be processed with the corresponding service

tier.

[Contact sales](https://openai.com/contact-sales)to learn more about Priority processing.* When not set, the default behavior is 'auto'.

When the

`service_tier`

parameter is set, the response body will include the `service_tier`

value based on the processing mode actually used to serve the request. This response value

may be different from the value set in the parameter.

`completed`

, `failed`

,`in_progress`

, `cancelled`

, `queued`

, or `incomplete`

.Possible values:

`completed`

, `failed`

, `in_progress`

, `cancelled`

, `queued`

, `incomplete`

We generally recommend altering this or

`top_p`

but not both.text or structured JSON data. See

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)and

[Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)`none`

means the model will not call any tool and instead generates a message.`auto`

means the model can pick between generating a message or calling one ormore tools.

`required`

means the model must call one or more tools.[OpenAI.ToolChoiceObjectType](#openaitoolchoiceobjecttype)[Learn more about built-in tools](https://platform.openai.com/docs/guides/tools).can specify which tool to use by setting the

`tool_choice`

parameter.The two categories of tools you can provide the model are:

*

**Built-in tools**: Tools that are provided by OpenAI that extend themodel's capabilities, like

[web search](https://platform.openai.com/docs/guides/tools-web-search)or

[file search](https://platform.openai.com/docs/guides/tools-file-search). Learn more about[built-in tools](https://platform.openai.com/docs/guides/tools).*

**Function calls (custom tools)**: Functions that are defined by you,enabling the model to call your own code. Learn more about

[function calling](https://platform.openai.com/docs/guides/function-calling).where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.-

`auto`

: If the context of this response and previous ones exceedsthe model's context window size, the model will truncate the

response to fit the context window by dropping input items in the

middle of the conversation.

-

`disabled`

(default): If a model response will exceed the context windowsize for a model, the request will fail with a 400 error.

Possible values:

`auto`

, `disabled`

[OpenAI.ResponseUsage](#openairesponseusage)a breakdown of output tokens, and the total tokens used.

[Learn more about safety best practices](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).### OpenAI.ResponseCodeInterpreterCallCodeDeltaEvent

Emitted when a partial code snippet is streamed by the code interpreter.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| delta | string | The partial code snippet being streamed by the code interpreter. | Yes | |
| item_id | string | The unique identifier of the code interpreter tool call item. | Yes | |
| output_index | integer | The index of the output item in the response for which the code is being streamed. | Yes | |
| type | enum | The type of the event. Always `response.code_interpreter_call_code.delta` .Possible values: `response.code_interpreter_call_code.delta` |
Yes |

### OpenAI.ResponseCodeInterpreterCallCodeDoneEvent

Emitted when the code snippet is finalized by the code interpreter.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code | string | The final code snippet output by the code interpreter. | Yes | |
| item_id | string | The unique identifier of the code interpreter tool call item. | Yes | |
| output_index | integer | The index of the output item in the response for which the code is finalized. | Yes | |
| type | enum | The type of the event. Always `response.code_interpreter_call_code.done` .Possible values: `response.code_interpreter_call_code.done` |
Yes |

### OpenAI.ResponseCodeInterpreterCallCompletedEvent

Emitted when the code interpreter call is completed.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The unique identifier of the code interpreter tool call item. | Yes | |
| output_index | integer | The index of the output item in the response for which the code interpreter call is completed. | Yes | |
| type | enum | The type of the event. Always `response.code_interpreter_call.completed` .Possible values: `response.code_interpreter_call.completed` |
Yes |

### OpenAI.ResponseCodeInterpreterCallInProgressEvent

Emitted when a code interpreter call is in progress.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The unique identifier of the code interpreter tool call item. | Yes | |
| output_index | integer | The index of the output item in the response for which the code interpreter call is in progress. | Yes | |
| type | enum | The type of the event. Always `response.code_interpreter_call.in_progress` .Possible values: `response.code_interpreter_call.in_progress` |
Yes |

### OpenAI.ResponseCodeInterpreterCallInterpretingEvent

Emitted when the code interpreter is actively interpreting the code snippet.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The unique identifier of the code interpreter tool call item. | Yes | |
| output_index | integer | The index of the output item in the response for which the code interpreter is interpreting code. | Yes | |
| type | enum | The type of the event. Always `response.code_interpreter_call.interpreting` .Possible values: `response.code_interpreter_call.interpreting` |
Yes |

### OpenAI.ResponseCompletedEvent

Emitted when the model response is complete.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| response | object | Yes | ||
| └─ agent |
|

[Learn more about background responses](https://platform.openai.com/docs/guides/background).[OpenAI.ResponseError](#openairesponseerror)Possible values:

`max_output_tokens`

, `content_filter`

When using along with

`previous_response_id`

, the instructions from a previousresponse will not be carried over to the next response. This makes it simple

to swap out system (or developer) messages in new responses.

[reasoning tokens](https://platform.openai.com/docs/guides/reasoning).useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

`response`

.Possible values:

`response`

- The length and order of items in the

`output`

array is dependenton the model's response.

- Rather than accessing the first item in the

`output`

array andassuming it's an

`assistant`

message with the content generated bythe model, you might consider using the

`output_text`

property wheresupported in SDKs.

from all

`output_text`

items in the `output`

array, if any are present.Supported in the Python and JavaScript SDKs.

create multi-turn conversations. Learn more about

[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).[OpenAI.Prompt](#openaiprompt)[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).[OpenAI.Reasoning](#openaireasoning)**o-series models only**Configuration options for reasoning models.

[OpenAI.ServiceTier](#openaiservicetier)`completed`

, `failed`

,`in_progress`

, `cancelled`

, `queued`

, or `incomplete`

.Possible values:

`completed`

, `failed`

, `in_progress`

, `cancelled`

, `queued`

, `incomplete`

We generally recommend altering this or

`top_p`

but not both.text or structured JSON data. See

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)and

[Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)[OpenAI.ToolChoiceOptions](#openaitoolchoiceoptions)or[OpenAI.ToolChoiceObject](#openaitoolchoiceobject)a response. See the

`tools`

parameter to see how to specify which toolsthe model can call.

can specify which tool to use by setting the

`tool_choice`

parameter.The two categories of tools you can provide the model are:

*

**Built-in tools**: Tools that are provided by OpenAI that extend themodel's capabilities, like

[web search](https://platform.openai.com/docs/guides/tools-web-search)or

[file search](https://platform.openai.com/docs/guides/tools-file-search). Learn more about[built-in tools](https://platform.openai.com/docs/guides/tools).*

**Function calls (custom tools)**: Functions that are defined by you,enabling the model to call your own code. Learn more about

[function calling](https://platform.openai.com/docs/guides/function-calling).where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.-

`auto`

: If the context of this response and previous ones exceedsthe model's context window size, the model will truncate the

response to fit the context window by dropping input items in the

middle of the conversation.

-

`disabled`

(default): If a model response will exceed the context windowsize for a model, the request will fail with a 400 error.

Possible values:

`auto`

, `disabled`

[OpenAI.ResponseUsage](#openairesponseusage)a breakdown of output tokens, and the total tokens used.

[Learn more about safety best practices](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).`response.completed`

.Possible values:

`response.completed`

### OpenAI.ResponseContentPartAddedEvent

Emitted when a new content part is added.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content_index | integer | The index of the content part that was added. | Yes | |
| item_id | string | The ID of the output item that the content part was added to. | Yes | |
| output_index | integer | The index of the output item that the content part was added to. | Yes | |
| part | object | Yes | ||
| └─ type |
|

`response.content_part.added`

.Possible values:

`response.content_part.added`

### OpenAI.ResponseContentPartDoneEvent

Emitted when a content part is done.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content_index | integer | The index of the content part that is done. | Yes | |
| item_id | string | The ID of the output item that the content part was added to. | Yes | |
| output_index | integer | The index of the output item that the content part was added to. | Yes | |
| part | object | Yes | ||
| └─ type |
|

`response.content_part.done`

.Possible values:

`response.content_part.done`

### OpenAI.ResponseCreatedEvent

An event that is emitted when a response is created.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| response | object | Yes | ||
| └─ agent |
|

[Learn more about background responses](https://platform.openai.com/docs/guides/background).[OpenAI.ResponseError](#openairesponseerror)Possible values:

`max_output_tokens`

, `content_filter`

When using along with

`previous_response_id`

, the instructions from a previousresponse will not be carried over to the next response. This makes it simple

to swap out system (or developer) messages in new responses.

[reasoning tokens](https://platform.openai.com/docs/guides/reasoning).useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

`response`

.Possible values:

`response`

- The length and order of items in the

`output`

array is dependenton the model's response.

- Rather than accessing the first item in the

`output`

array andassuming it's an

`assistant`

message with the content generated bythe model, you might consider using the

`output_text`

property wheresupported in SDKs.

from all

`output_text`

items in the `output`

array, if any are present.Supported in the Python and JavaScript SDKs.

create multi-turn conversations. Learn more about

[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).[OpenAI.Prompt](#openaiprompt)[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).[OpenAI.Reasoning](#openaireasoning)**o-series models only**Configuration options for reasoning models.

[OpenAI.ServiceTier](#openaiservicetier)`completed`

, `failed`

,`in_progress`

, `cancelled`

, `queued`

, or `incomplete`

.Possible values:

`completed`

, `failed`

, `in_progress`

, `cancelled`

, `queued`

, `incomplete`

We generally recommend altering this or

`top_p`

but not both.text or structured JSON data. See

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)and

[Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)[OpenAI.ToolChoiceOptions](#openaitoolchoiceoptions)or[OpenAI.ToolChoiceObject](#openaitoolchoiceobject)a response. See the

`tools`

parameter to see how to specify which toolsthe model can call.

can specify which tool to use by setting the

`tool_choice`

parameter.The two categories of tools you can provide the model are:

*

**Built-in tools**: Tools that are provided by OpenAI that extend themodel's capabilities, like

[web search](https://platform.openai.com/docs/guides/tools-web-search)or

[file search](https://platform.openai.com/docs/guides/tools-file-search). Learn more about[built-in tools](https://platform.openai.com/docs/guides/tools).*

**Function calls (custom tools)**: Functions that are defined by you,enabling the model to call your own code. Learn more about

[function calling](https://platform.openai.com/docs/guides/function-calling).where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.-

`auto`

: If the context of this response and previous ones exceedsthe model's context window size, the model will truncate the

response to fit the context window by dropping input items in the

middle of the conversation.

-

`disabled`

(default): If a model response will exceed the context windowsize for a model, the request will fail with a 400 error.

Possible values:

`auto`

, `disabled`

[OpenAI.ResponseUsage](#openairesponseusage)a breakdown of output tokens, and the total tokens used.

[Learn more about safety best practices](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).`response.created`

.Possible values:

`response.created`

### OpenAI.ResponseError

An error object returned when the model fails to generate a Response.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code |
|

### OpenAI.ResponseErrorCode

The error code for the response.

| Property | Value |
|---|---|
Description |
The error code for the response. |
Type |
string |
Values |
`server_error` `rate_limit_exceeded` `invalid_prompt` `vector_store_timeout` `invalid_image` `invalid_image_format` `invalid_base64_image` `invalid_image_url` `image_too_large` `image_too_small` `image_parse_error` `image_content_policy_violation` `invalid_image_mode` `image_file_too_large` `unsupported_image_media_type` `empty_image_file` `failed_to_download_image` `image_file_not_found` |

### OpenAI.ResponseErrorEvent

Emitted when an error occurs.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| code | string | The error code. | Yes | |
| message | string | The error message. | Yes | |
| param | string | The error parameter. | Yes | |
| type | enum | The type of the event. Always `error` .Possible values: `error` |
Yes |

### OpenAI.ResponseFailedEvent

An event that is emitted when a response fails.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| response | object | Yes | ||
| └─ agent |
|

[Learn more about background responses](https://platform.openai.com/docs/guides/background).[OpenAI.ResponseError](#openairesponseerror)Possible values:

`max_output_tokens`

, `content_filter`

When using along with

`previous_response_id`

, the instructions from a previousresponse will not be carried over to the next response. This makes it simple

to swap out system (or developer) messages in new responses.

[reasoning tokens](https://platform.openai.com/docs/guides/reasoning).useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

`response`

.Possible values:

`response`

- The length and order of items in the

`output`

array is dependenton the model's response.

- Rather than accessing the first item in the

`output`

array andassuming it's an

`assistant`

message with the content generated bythe model, you might consider using the

`output_text`

property wheresupported in SDKs.

from all

`output_text`

items in the `output`

array, if any are present.Supported in the Python and JavaScript SDKs.

create multi-turn conversations. Learn more about

[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).[OpenAI.Prompt](#openaiprompt)[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).[OpenAI.Reasoning](#openaireasoning)**o-series models only**Configuration options for reasoning models.

[OpenAI.ServiceTier](#openaiservicetier)`completed`

, `failed`

,`in_progress`

, `cancelled`

, `queued`

, or `incomplete`

.Possible values:

`completed`

, `failed`

, `in_progress`

, `cancelled`

, `queued`

, `incomplete`

We generally recommend altering this or

`top_p`

but not both.text or structured JSON data. See

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)and

[Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)[OpenAI.ToolChoiceOptions](#openaitoolchoiceoptions)or[OpenAI.ToolChoiceObject](#openaitoolchoiceobject)a response. See the

`tools`

parameter to see how to specify which toolsthe model can call.

can specify which tool to use by setting the

`tool_choice`

parameter.The two categories of tools you can provide the model are:

*

**Built-in tools**: Tools that are provided by OpenAI that extend themodel's capabilities, like

[web search](https://platform.openai.com/docs/guides/tools-web-search)or

[file search](https://platform.openai.com/docs/guides/tools-file-search). Learn more about[built-in tools](https://platform.openai.com/docs/guides/tools).*

**Function calls (custom tools)**: Functions that are defined by you,enabling the model to call your own code. Learn more about

[function calling](https://platform.openai.com/docs/guides/function-calling).where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.-

`auto`

: If the context of this response and previous ones exceedsthe model's context window size, the model will truncate the

response to fit the context window by dropping input items in the

middle of the conversation.

-

`disabled`

(default): If a model response will exceed the context windowsize for a model, the request will fail with a 400 error.

Possible values:

`auto`

, `disabled`

[OpenAI.ResponseUsage](#openairesponseusage)a breakdown of output tokens, and the total tokens used.

[Learn more about safety best practices](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).`response.failed`

.Possible values:

`response.failed`

### OpenAI.ResponseFileSearchCallCompletedEvent

Emitted when a file search call is completed (results found).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The ID of the output item that the file search call is initiated. | Yes | |
| output_index | integer | The index of the output item that the file search call is initiated. | Yes | |
| type | enum | The type of the event. Always `response.file_search_call.completed` .Possible values: `response.file_search_call.completed` |
Yes |

### OpenAI.ResponseFileSearchCallInProgressEvent

Emitted when a file search call is initiated.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The ID of the output item that the file search call is initiated. | Yes | |
| output_index | integer | The index of the output item that the file search call is initiated. | Yes | |
| type | enum | The type of the event. Always `response.file_search_call.in_progress` .Possible values: `response.file_search_call.in_progress` |
Yes |

### OpenAI.ResponseFileSearchCallSearchingEvent

Emitted when a file search is currently searching.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The ID of the output item that the file search call is initiated. | Yes | |
| output_index | integer | The index of the output item that the file search call is searching. | Yes | |
| type | enum | The type of the event. Always `response.file_search_call.searching` .Possible values: `response.file_search_call.searching` |
Yes |

### OpenAI.ResponseFormat

### Discriminator for OpenAI.ResponseFormat

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`json_object` |
|

`json_schema`

[OpenAI.ResponseFormatJsonSchema](#openairesponseformatjsonschema)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `text` , `json_object` , `json_schema` |
Yes |

### OpenAI.ResponseFormatJsonObject

JSON object response format. An older method of generating JSON responses.
Using `json_schema`

is recommended for models that support it. Note that the
model will not generate JSON without a system or user message instructing it
to do so.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of response format being defined. Always `json_object` .Possible values: `json_object` |
Yes |

### OpenAI.ResponseFormatJsonSchema

The schema for the response format, described as a JSON Schema object.
Learn how to build JSON schemas [here](https://json-schema.org/).JSON Schema response format. Used to generate structured JSON responses.
Learn more about [Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| json_schema | object | Structured Outputs configuration options, including a JSON Schema. | Yes | |
| └─ description | string | A description of what the response format is for, used by the model to determine how to respond in the format. |
No | |
| └─ name | string | The name of the response format. Must be a-z, A-Z, 0-9, or contain underscores and dashes, with a maximum length of 64. |
No | |
| └─ schema | object | No | ||
| └─ strict | boolean | Whether to enable strict schema adherence when generating the output. If set to true, the model will always follow the exact schema defined in the `schema` field. Only a subset of JSON Schema is supported when`strict` is `true` . To learn more, read the
guide |
No | False |
| type | enum | The type of response format being defined. Always `json_schema` .Possible values: `json_schema` |
Yes |

### OpenAI.ResponseFormatText

Default response format. Used to generate text responses.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of response format being defined. Always `text` .Possible values: `text` |
Yes |

### OpenAI.ResponseFunctionCallArgumentsDeltaEvent

Emitted when there is a partial function-call arguments delta.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| delta | string | The function-call arguments delta that is added. | Yes | |
| item_id | string | The ID of the output item that the function-call arguments delta is added to. | Yes | |
| output_index | integer | The index of the output item that the function-call arguments delta is added to. | Yes | |
| type | enum | The type of the event. Always `response.function_call_arguments.delta` .Possible values: `response.function_call_arguments.delta` |
Yes |

### OpenAI.ResponseFunctionCallArgumentsDoneEvent

Emitted when function-call arguments are finalized.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| arguments | string | The function-call arguments. | Yes | |
| item_id | string | The ID of the item. | Yes | |
| output_index | integer | The index of the output item. | Yes | |
| type | enum | Possible values: `response.function_call_arguments.done` |
Yes |

### OpenAI.ResponseImageGenCallCompletedEvent

Emitted when an image generation tool call has completed and the final image is available.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The unique identifier of the image generation item being processed. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| type | enum | The type of the event. Always 'response.image_generation_call.completed'. Possible values: `response.image_generation_call.completed` |
Yes |

### OpenAI.ResponseImageGenCallGeneratingEvent

Emitted when an image generation tool call is actively generating an image (intermediate state).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The unique identifier of the image generation item being processed. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| type | enum | The type of the event. Always 'response.image_generation_call.generating'. Possible values: `response.image_generation_call.generating` |
Yes |

### OpenAI.ResponseImageGenCallInProgressEvent

Emitted when an image generation tool call is in progress.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The unique identifier of the image generation item being processed. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| type | enum | The type of the event. Always 'response.image_generation_call.in_progress'. Possible values: `response.image_generation_call.in_progress` |
Yes |

### OpenAI.ResponseImageGenCallPartialImageEvent

Emitted when a partial image is available during image generation streaming.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The unique identifier of the image generation item being processed. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| partial_image_b64 | string | Base64-encoded partial image data, suitable for rendering as an image. | Yes | |
| partial_image_index | integer | 0-based index for the partial image (backend is 1-based, but this is 0-based for the user). | Yes | |
| type | enum | The type of the event. Always 'response.image_generation_call.partial_image'. Possible values: `response.image_generation_call.partial_image` |
Yes |

### OpenAI.ResponseInProgressEvent

Emitted when the response is in progress.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| response | object | Yes | ||
| └─ agent |
|

[Learn more about background responses](https://platform.openai.com/docs/guides/background).[OpenAI.ResponseError](#openairesponseerror)Possible values:

`max_output_tokens`

, `content_filter`

When using along with

`previous_response_id`

, the instructions from a previousresponse will not be carried over to the next response. This makes it simple

to swap out system (or developer) messages in new responses.

[reasoning tokens](https://platform.openai.com/docs/guides/reasoning).useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

`response`

.Possible values:

`response`

- The length and order of items in the

`output`

array is dependenton the model's response.

- Rather than accessing the first item in the

`output`

array andassuming it's an

`assistant`

message with the content generated bythe model, you might consider using the

`output_text`

property wheresupported in SDKs.

from all

`output_text`

items in the `output`

array, if any are present.Supported in the Python and JavaScript SDKs.

create multi-turn conversations. Learn more about

[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).[OpenAI.Prompt](#openaiprompt)[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).[OpenAI.Reasoning](#openaireasoning)**o-series models only**Configuration options for reasoning models.

[OpenAI.ServiceTier](#openaiservicetier)`completed`

, `failed`

,`in_progress`

, `cancelled`

, `queued`

, or `incomplete`

.Possible values:

`completed`

, `failed`

, `in_progress`

, `cancelled`

, `queued`

, `incomplete`

We generally recommend altering this or

`top_p`

but not both.text or structured JSON data. See

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)and

[Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)[OpenAI.ToolChoiceOptions](#openaitoolchoiceoptions)or[OpenAI.ToolChoiceObject](#openaitoolchoiceobject)a response. See the

`tools`

parameter to see how to specify which toolsthe model can call.

can specify which tool to use by setting the

`tool_choice`

parameter.The two categories of tools you can provide the model are:

*

**Built-in tools**: Tools that are provided by OpenAI that extend themodel's capabilities, like

[web search](https://platform.openai.com/docs/guides/tools-web-search)or

[file search](https://platform.openai.com/docs/guides/tools-file-search). Learn more about[built-in tools](https://platform.openai.com/docs/guides/tools).*

**Function calls (custom tools)**: Functions that are defined by you,enabling the model to call your own code. Learn more about

[function calling](https://platform.openai.com/docs/guides/function-calling).where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.-

`auto`

: If the context of this response and previous ones exceedsthe model's context window size, the model will truncate the

response to fit the context window by dropping input items in the

middle of the conversation.

-

`disabled`

(default): If a model response will exceed the context windowsize for a model, the request will fail with a 400 error.

Possible values:

`auto`

, `disabled`

[OpenAI.ResponseUsage](#openairesponseusage)a breakdown of output tokens, and the total tokens used.

[Learn more about safety best practices](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).`response.in_progress`

.Possible values:

`response.in_progress`

### OpenAI.ResponseIncompleteEvent

An event that is emitted when a response finishes as incomplete.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| response | object | Yes | ||
| └─ agent |
|

[Learn more about background responses](https://platform.openai.com/docs/guides/background).[OpenAI.ResponseError](#openairesponseerror)Possible values:

`max_output_tokens`

, `content_filter`

When using along with

`previous_response_id`

, the instructions from a previousresponse will not be carried over to the next response. This makes it simple

to swap out system (or developer) messages in new responses.

[reasoning tokens](https://platform.openai.com/docs/guides/reasoning).useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

`response`

.Possible values:

`response`

- The length and order of items in the

`output`

array is dependenton the model's response.

- Rather than accessing the first item in the

`output`

array andassuming it's an

`assistant`

message with the content generated bythe model, you might consider using the

`output_text`

property wheresupported in SDKs.

from all

`output_text`

items in the `output`

array, if any are present.Supported in the Python and JavaScript SDKs.

create multi-turn conversations. Learn more about

[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).[OpenAI.Prompt](#openaiprompt)[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).[OpenAI.Reasoning](#openaireasoning)**o-series models only**Configuration options for reasoning models.

[OpenAI.ServiceTier](#openaiservicetier)`completed`

, `failed`

,`in_progress`

, `cancelled`

, `queued`

, or `incomplete`

.Possible values:

`completed`

, `failed`

, `in_progress`

, `cancelled`

, `queued`

, `incomplete`

We generally recommend altering this or

`top_p`

but not both.text or structured JSON data. See

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)and

[Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)[OpenAI.ToolChoiceOptions](#openaitoolchoiceoptions)or[OpenAI.ToolChoiceObject](#openaitoolchoiceobject)a response. See the

`tools`

parameter to see how to specify which toolsthe model can call.

can specify which tool to use by setting the

`tool_choice`

parameter.The two categories of tools you can provide the model are:

*

**Built-in tools**: Tools that are provided by OpenAI that extend themodel's capabilities, like

[web search](https://platform.openai.com/docs/guides/tools-web-search)or

[file search](https://platform.openai.com/docs/guides/tools-file-search). Learn more about[built-in tools](https://platform.openai.com/docs/guides/tools).*

**Function calls (custom tools)**: Functions that are defined by you,enabling the model to call your own code. Learn more about

[function calling](https://platform.openai.com/docs/guides/function-calling).where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.-

`auto`

: If the context of this response and previous ones exceedsthe model's context window size, the model will truncate the

response to fit the context window by dropping input items in the

middle of the conversation.

-

`disabled`

(default): If a model response will exceed the context windowsize for a model, the request will fail with a 400 error.

Possible values:

`auto`

, `disabled`

[OpenAI.ResponseUsage](#openairesponseusage)a breakdown of output tokens, and the total tokens used.

[Learn more about safety best practices](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).`response.incomplete`

.Possible values:

`response.incomplete`

### OpenAI.ResponseMCPCallArgumentsDeltaEvent

Emitted when there is a delta (partial update) to the arguments of an MCP tool call.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| delta | The partial update to the arguments for the MCP tool call. | Yes | ||
| item_id | string | The unique identifier of the MCP tool call item being processed. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| type | enum | The type of the event. Always 'response.mcp_call.arguments_delta'. Possible values: `response.mcp_call.arguments_delta` |
Yes |

### OpenAI.ResponseMCPCallArgumentsDoneEvent

Emitted when the arguments for an MCP tool call are finalized.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| arguments | The finalized arguments for the MCP tool call. | Yes | ||
| item_id | string | The unique identifier of the MCP tool call item being processed. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| type | enum | The type of the event. Always 'response.mcp_call.arguments_done'. Possible values: `response.mcp_call.arguments_done` |
Yes |

### OpenAI.ResponseMCPCallCompletedEvent

Emitted when an MCP tool call has completed successfully.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of the event. Always 'response.mcp_call.completed'. Possible values: `response.mcp_call.completed` |
Yes |

### OpenAI.ResponseMCPCallFailedEvent

Emitted when an MCP tool call has failed.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of the event. Always 'response.mcp_call.failed'. Possible values: `response.mcp_call.failed` |
Yes |

### OpenAI.ResponseMCPCallInProgressEvent

Emitted when an MCP tool call is in progress.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The unique identifier of the MCP tool call item being processed. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| type | enum | The type of the event. Always 'response.mcp_call.in_progress'. Possible values: `response.mcp_call.in_progress` |
Yes |

### OpenAI.ResponseMCPListToolsCompletedEvent

Emitted when the list of available MCP tools has been successfully retrieved.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of the event. Always 'response.mcp_list_tools.completed'. Possible values: `response.mcp_list_tools.completed` |
Yes |

### OpenAI.ResponseMCPListToolsFailedEvent

Emitted when the attempt to list available MCP tools has failed.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of the event. Always 'response.mcp_list_tools.failed'. Possible values: `response.mcp_list_tools.failed` |
Yes |

### OpenAI.ResponseMCPListToolsInProgressEvent

Emitted when the system is in the process of retrieving the list of available MCP tools.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The type of the event. Always 'response.mcp_list_tools.in_progress'. Possible values: `response.mcp_list_tools.in_progress` |
Yes |

### OpenAI.ResponseOutputItemAddedEvent

Emitted when a new output item is added.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item | object | Content item used to generate a response. | Yes | |
| └─ created_by |
|

[OpenAI.ItemType](#openaiitemtype)`response.output_item.added`

.Possible values:

`response.output_item.added`

### OpenAI.ResponseOutputItemDoneEvent

Emitted when an output item is marked done.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item | object | Content item used to generate a response. | Yes | |
| └─ created_by |
|

[OpenAI.ItemType](#openaiitemtype)`response.output_item.done`

.Possible values:

`response.output_item.done`

### OpenAI.ResponsePromptVariables

Optional map of values to substitute in for variables in your prompt. The substitution values can either be strings, or other Response input types like images or files.

**Type**: object

### OpenAI.ResponseQueuedEvent

Emitted when a response is queued and waiting to be processed.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| response | object | Yes | ||
| └─ agent |
|

[Learn more about background responses](https://platform.openai.com/docs/guides/background).[OpenAI.ResponseError](#openairesponseerror)Possible values:

`max_output_tokens`

, `content_filter`

When using along with

`previous_response_id`

, the instructions from a previousresponse will not be carried over to the next response. This makes it simple

to swap out system (or developer) messages in new responses.

[reasoning tokens](https://platform.openai.com/docs/guides/reasoning).useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

`response`

.Possible values:

`response`

- The length and order of items in the

`output`

array is dependenton the model's response.

- Rather than accessing the first item in the

`output`

array andassuming it's an

`assistant`

message with the content generated bythe model, you might consider using the

`output_text`

property wheresupported in SDKs.

from all

`output_text`

items in the `output`

array, if any are present.Supported in the Python and JavaScript SDKs.

create multi-turn conversations. Learn more about

[managing conversation state](https://platform.openai.com/docs/guides/conversation-state).[OpenAI.Prompt](#openaiprompt)[Learn more](https://platform.openai.com/docs/guides/text?api-mode=responses#reusable-prompts).[OpenAI.Reasoning](#openaireasoning)**o-series models only**Configuration options for reasoning models.

[OpenAI.ServiceTier](#openaiservicetier)`completed`

, `failed`

,`in_progress`

, `cancelled`

, `queued`

, or `incomplete`

.Possible values:

`completed`

, `failed`

, `in_progress`

, `cancelled`

, `queued`

, `incomplete`

We generally recommend altering this or

`top_p`

but not both.text or structured JSON data. See

[Text inputs and outputs](https://platform.openai.com/docs/guides/text)and

[Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs)[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)[OpenAI.ToolChoiceOptions](#openaitoolchoiceoptions)or[OpenAI.ToolChoiceObject](#openaitoolchoiceobject)a response. See the

`tools`

parameter to see how to specify which toolsthe model can call.

can specify which tool to use by setting the

`tool_choice`

parameter.The two categories of tools you can provide the model are:

*

**Built-in tools**: Tools that are provided by OpenAI that extend themodel's capabilities, like

[web search](https://platform.openai.com/docs/guides/tools-web-search)or

[file search](https://platform.openai.com/docs/guides/tools-file-search). Learn more about[built-in tools](https://platform.openai.com/docs/guides/tools).*

**Function calls (custom tools)**: Functions that are defined by you,enabling the model to call your own code. Learn more about

[function calling](https://platform.openai.com/docs/guides/function-calling).where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.-

`auto`

: If the context of this response and previous ones exceedsthe model's context window size, the model will truncate the

response to fit the context window by dropping input items in the

middle of the conversation.

-

`disabled`

(default): If a model response will exceed the context windowsize for a model, the request will fail with a 400 error.

Possible values:

`auto`

, `disabled`

[OpenAI.ResponseUsage](#openairesponseusage)a breakdown of output tokens, and the total tokens used.

[Learn more about safety best practices](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).Possible values:

`response.queued`

### OpenAI.ResponseReasoningDeltaEvent

Emitted when there is a delta (partial update) to the reasoning content.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content_index | integer | The index of the reasoning content part within the output item. | Yes | |
| delta | The partial update to the reasoning content. | Yes | ||
| item_id | string | The unique identifier of the item for which reasoning is being updated. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| type | enum | The type of the event. Always 'response.reasoning.delta'. Possible values: `response.reasoning.delta` |
Yes |

### OpenAI.ResponseReasoningDoneEvent

Emitted when the reasoning content is finalized for an item.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content_index | integer | The index of the reasoning content part within the output item. | Yes | |
| item_id | string | The unique identifier of the item for which reasoning is finalized. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| text | string | The finalized reasoning text. | Yes | |
| type | enum | The type of the event. Always 'response.reasoning.done'. Possible values: `response.reasoning.done` |
Yes |

### OpenAI.ResponseReasoningSummaryDeltaEvent

Emitted when there is a delta (partial update) to the reasoning summary content.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| delta | The partial update to the reasoning summary content. | Yes | ||
| item_id | string | The unique identifier of the item for which the reasoning summary is being updated. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| summary_index | integer | The index of the summary part within the output item. | Yes | |
| type | enum | The type of the event. Always 'response.reasoning_summary.delta'. Possible values: `response.reasoning_summary.delta` |
Yes |

### OpenAI.ResponseReasoningSummaryDoneEvent

Emitted when the reasoning summary content is finalized for an item.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The unique identifier of the item for which the reasoning summary is finalized. | Yes | |
| output_index | integer | The index of the output item in the response's output array. | Yes | |
| summary_index | integer | The index of the summary part within the output item. | Yes | |
| text | string | The finalized reasoning summary text. | Yes | |
| type | enum | The type of the event. Always 'response.reasoning_summary.done'. Possible values: `response.reasoning_summary.done` |
Yes |

### OpenAI.ResponseReasoningSummaryPartAddedEvent

Emitted when a new reasoning summary part is added.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The ID of the item this summary part is associated with. | Yes | |
| output_index | integer | The index of the output item this summary part is associated with. | Yes | |
| part | object | Yes | ||
| └─ type |
|

`response.reasoning_summary_part.added`

.Possible values:

`response.reasoning_summary_part.added`

### OpenAI.ResponseReasoningSummaryPartDoneEvent

Emitted when a reasoning summary part is completed.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The ID of the item this summary part is associated with. | Yes | |
| output_index | integer | The index of the output item this summary part is associated with. | Yes | |
| part | object | Yes | ||
| └─ type |
|

`response.reasoning_summary_part.done`

.Possible values:

`response.reasoning_summary_part.done`

### OpenAI.ResponseReasoningSummaryTextDeltaEvent

Emitted when a delta is added to a reasoning summary text.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| delta | string | The text delta that was added to the summary. | Yes | |
| item_id | string | The ID of the item this summary text delta is associated with. | Yes | |
| output_index | integer | The index of the output item this summary text delta is associated with. | Yes | |
| summary_index | integer | The index of the summary part within the reasoning summary. | Yes | |
| type | enum | The type of the event. Always `response.reasoning_summary_text.delta` .Possible values: `response.reasoning_summary_text.delta` |
Yes |

### OpenAI.ResponseReasoningSummaryTextDoneEvent

Emitted when a reasoning summary text is completed.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | The ID of the item this summary text is associated with. | Yes | |
| output_index | integer | The index of the output item this summary text is associated with. | Yes | |
| summary_index | integer | The index of the summary part within the reasoning summary. | Yes | |
| text | string | The full text of the completed reasoning summary. | Yes | |
| type | enum | The type of the event. Always `response.reasoning_summary_text.done` .Possible values: `response.reasoning_summary_text.done` |
Yes |

### OpenAI.ResponseRefusalDeltaEvent

Emitted when there is a partial refusal text.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content_index | integer | The index of the content part that the refusal text is added to. | Yes | |
| delta | string | The refusal text that is added. | Yes | |
| item_id | string | The ID of the output item that the refusal text is added to. | Yes | |
| output_index | integer | The index of the output item that the refusal text is added to. | Yes | |
| type | enum | The type of the event. Always `response.refusal.delta` .Possible values: `response.refusal.delta` |
Yes |

### OpenAI.ResponseRefusalDoneEvent

Emitted when refusal text is finalized.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content_index | integer | The index of the content part that the refusal text is finalized. | Yes | |
| item_id | string | The ID of the output item that the refusal text is finalized. | Yes | |
| output_index | integer | The index of the output item that the refusal text is finalized. | Yes | |
| refusal | string | The refusal text that is finalized. | Yes | |
| type | enum | The type of the event. Always `response.refusal.done` .Possible values: `response.refusal.done` |
Yes |

### OpenAI.ResponseStreamEvent

### Discriminator for OpenAI.ResponseStreamEvent

This component uses the property `type`

to discriminate between different types:

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| sequence_number | integer | The sequence number for this event. | Yes | |
| type |
|

### OpenAI.ResponseStreamEventType

| Property | Value |
|---|---|
Type |
string |
Values |
`response.audio.delta` `response.audio.done` `response.audio_transcript.delta` `response.audio_transcript.done` `response.code_interpreter_call_code.delta` `response.code_interpreter_call_code.done` `response.code_interpreter_call.completed` `response.code_interpreter_call.in_progress` `response.code_interpreter_call.interpreting` `response.completed` `response.content_part.added` `response.content_part.done` `response.created` `error` `response.file_search_call.completed` `response.file_search_call.in_progress` `response.file_search_call.searching` `response.function_call_arguments.delta` `response.function_call_arguments.done` `response.in_progress` `response.failed` `response.incomplete` `response.output_item.added` `response.output_item.done` `response.refusal.delta` `response.refusal.done` `response.output_text.annotation.added` `response.output_text.delta` `response.output_text.done` `response.reasoning_summary_part.added` `response.reasoning_summary_part.done` `response.reasoning_summary_text.delta` `response.reasoning_summary_text.done` `response.web_search_call.completed` `response.web_search_call.in_progress` `response.web_search_call.searching` `response.image_generation_call.completed` `response.image_generation_call.generating` `response.image_generation_call.in_progress` `response.image_generation_call.partial_image` `response.mcp_call.arguments_delta` `response.mcp_call.arguments_done` `response.mcp_call.completed` `response.mcp_call.failed` `response.mcp_call.in_progress` `response.mcp_list_tools.completed` `response.mcp_list_tools.failed` `response.mcp_list_tools.in_progress` `response.queued` `response.reasoning.delta` `response.reasoning.done` `response.reasoning_summary.delta` `response.reasoning_summary.done` |

### OpenAI.ResponseTextDeltaEvent

Emitted when there is an additional text delta.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content_index | integer | The index of the content part that the text delta was added to. | Yes | |
| delta | string | The text delta that was added. | Yes | |
| item_id | string | The ID of the output item that the text delta was added to. | Yes | |
| output_index | integer | The index of the output item that the text delta was added to. | Yes | |
| type | enum | The type of the event. Always `response.output_text.delta` .Possible values: `response.output_text.delta` |
Yes |

### OpenAI.ResponseTextDoneEvent

Emitted when text content is finalized.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content_index | integer | The index of the content part that the text content is finalized. | Yes | |
| item_id | string | The ID of the output item that the text content is finalized. | Yes | |
| output_index | integer | The index of the output item that the text content is finalized. | Yes | |
| text | string | The text content that is finalized. | Yes | |
| type | enum | The type of the event. Always `response.output_text.done` .Possible values: `response.output_text.done` |
Yes |

### OpenAI.ResponseTextFormatConfiguration

### Discriminator for OpenAI.ResponseTextFormatConfiguration

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`text` |
|

`json_object`

[OpenAI.ResponseTextFormatConfigurationJsonObject](#openairesponsetextformatconfigurationjsonobject)`json_schema`

[OpenAI.ResponseTextFormatConfigurationJsonSchema](#openairesponsetextformatconfigurationjsonschema)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

Configuring

`{ "type": "json_schema" }`

enables Structured Outputs,which ensures the model will match your supplied JSON schema. Learn more in the

The default format is

`{ "type": "text" }`

with no additional options.**Not recommended for gpt-4o and newer models:**Setting to

`{ "type": "json_object" }`

enables the older JSON mode, whichensures the message the model generates is valid JSON. Using

`json_schema`

is preferred for models that support it.

### OpenAI.ResponseTextFormatConfigurationJsonObject

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `json_object` |
Yes |

### OpenAI.ResponseTextFormatConfigurationJsonSchema

JSON Schema response format. Used to generate structured JSON responses.
Learn more about [Structured Outputs](https://platform.openai.com/docs/guides/structured-outputs).

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A description of what the response format is for, used by the model to determine how to respond in the format. |
No | |
| name | string | The name of the response format. Must be a-z, A-Z, 0-9, or contain underscores and dashes, with a maximum length of 64. |
Yes | |
| schema | object | Yes | ||
| strict | boolean | Whether to enable strict schema adherence when generating the output. If set to true, the model will always follow the exact schema defined in the `schema` field. Only a subset of JSON Schema is supported when`strict` is `true` . To learn more, read the
guide |
No | False |
| type | enum | The type of response format being defined. Always `json_schema` .Possible values: `json_schema` |
Yes |

### OpenAI.ResponseTextFormatConfigurationText

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `text` |
Yes |

### OpenAI.ResponseTextFormatConfigurationType

An object specifying the format that the model must output.

Configuring `{ "type": "json_schema" }`

enables Structured Outputs,
which ensures the model will match your supplied JSON schema. Learn more in the

The default format is `{ "type": "text" }`

with no additional options.

**Not recommended for gpt-4o and newer models:**

Setting to `{ "type": "json_object" }`

enables the older JSON mode, which
ensures the message the model generates is valid JSON. Using `json_schema`

is preferred for models that support it.

| Property | Value |
|---|---|
Description |
An object specifying the format that the model must output. |

Configuring `{ "type": "json_schema" }`

enables Structured Outputs,
which ensures the model will match your supplied JSON schema. Learn more in the

The default format is `{ "type": "text" }`

with no additional options.

**Not recommended for gpt-4o and newer models:**

Setting to `{ "type": "json_object" }`

enables the older JSON mode, which
ensures the message the model generates is valid JSON. Using `json_schema`

is preferred for models that support it. |
| **Type** | string |
| **Values** | `text`

`json_schema`

`json_object`

|

### OpenAI.ResponseUsage

Represents token usage details including input tokens, output tokens, a breakdown of output tokens, and the total tokens used.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input_tokens | integer | The number of input tokens. | Yes | |
| input_tokens_details | object | A detailed breakdown of the input tokens. | Yes | |
| └─ cached_tokens | integer | The number of tokens that were retrieved from the cache.
|
No | |
| output_tokens | integer | The number of output tokens. | Yes | |
| output_tokens_details | object | A detailed breakdown of the output tokens. | Yes | |
| └─ reasoning_tokens | integer | The number of reasoning tokens. | No | |
| total_tokens | integer | The total number of tokens used. | Yes |

### OpenAI.ResponseWebSearchCallCompletedEvent

Note: web_search is not yet available via Azure OpenAI.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | Unique ID for the output item associated with the web search call. | Yes | |
| output_index | integer | The index of the output item that the web search call is associated with. | Yes | |
| type | enum | The type of the event. Always `response.web_search_call.completed` .Possible values: `response.web_search_call.completed` |
Yes |

### OpenAI.ResponseWebSearchCallInProgressEvent

Note: web_search is not yet available via Azure OpenAI.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | Unique ID for the output item associated with the web search call. | Yes | |
| output_index | integer | The index of the output item that the web search call is associated with. | Yes | |
| type | enum | The type of the event. Always `response.web_search_call.in_progress` .Possible values: `response.web_search_call.in_progress` |
Yes |

### OpenAI.ResponseWebSearchCallSearchingEvent

Note: web_search is not yet available via Azure OpenAI.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| item_id | string | Unique ID for the output item associated with the web search call. | Yes | |
| output_index | integer | The index of the output item that the web search call is associated with. | Yes | |
| type | enum | The type of the event. Always `response.web_search_call.searching` .Possible values: `response.web_search_call.searching` |
Yes |

### OpenAI.ResponsesAssistantMessageItemParam

A message parameter item with the `assistant`

role.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | string or array | Yes | ||
| role | enum | The role of the message, which is always `assistant` .Possible values: `assistant` |
Yes |

### OpenAI.ResponsesAssistantMessageItemResource

A message resource item with the `assistant`

role.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | array | The content associated with the message. | Yes | |
| role | enum | The role of the message, which is always `assistant` .Possible values: `assistant` |
Yes |

### OpenAI.ResponsesDeveloperMessageItemParam

A message parameter item with the `developer`

role.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | string or array | Yes | ||
| role | enum | The role of the message, which is always `developer` .Possible values: `developer` |
Yes |

### OpenAI.ResponsesDeveloperMessageItemResource

A message resource item with the `developer`

role.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | array | The content associated with the message. | Yes | |
| role | enum | The role of the message, which is always `developer` .Possible values: `developer` |
Yes |

### OpenAI.ResponsesMessageItemParam

A response message item, representing a role and content, as provided as client request parameters.

### Discriminator for OpenAI.ResponsesMessageItemParam

This component uses the property `role`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`user` |
|

`system`

[OpenAI.ResponsesSystemMessageItemParam](#openairesponsessystemmessageitemparam)`developer`

[OpenAI.ResponsesDeveloperMessageItemParam](#openairesponsesdevelopermessageitemparam)`assistant`

[OpenAI.ResponsesAssistantMessageItemParam](#openairesponsesassistantmessageitemparam)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| role | object | The collection of valid roles for responses message items. | Yes | |
| type | enum | The type of the responses item, which is always 'message'. Possible values: `message` |
Yes |

### OpenAI.ResponsesMessageItemResource

A response message resource item, representing a role and content, as provided on service responses.

### Discriminator for OpenAI.ResponsesMessageItemResource

This component uses the property `role`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`user` |
|

`system`

[OpenAI.ResponsesSystemMessageItemResource](#openairesponsessystemmessageitemresource)`developer`

[OpenAI.ResponsesDeveloperMessageItemResource](#openairesponsesdevelopermessageitemresource)`assistant`

[OpenAI.ResponsesAssistantMessageItemResource](#openairesponsesassistantmessageitemresource)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| role | object | The collection of valid roles for responses message items. | Yes | |
| status | enum | The status of the item. One of `in_progress` , `completed` , or`incomplete` . Populated when items are returned via API.Possible values: `in_progress` , `completed` , `incomplete` |
Yes | |
| type | enum | The type of the responses item, which is always 'message'. Possible values: `message` |
Yes |

### OpenAI.ResponsesMessageRole

The collection of valid roles for responses message items.

| Property | Value |
|---|---|
Description |
The collection of valid roles for responses message items. |
Type |
string |
Values |
`system` `developer` `user` `assistant` |

### OpenAI.ResponsesSystemMessageItemParam

A message parameter item with the `system`

role.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | string or array | Yes | ||
| role | enum | The role of the message, which is always `system` .Possible values: `system` |
Yes |

### OpenAI.ResponsesSystemMessageItemResource

A message resource item with the `system`

role.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | array | The content associated with the message. | Yes | |
| role | enum | The role of the message, which is always `system` .Possible values: `system` |
Yes |

### OpenAI.ResponsesUserMessageItemParam

A message parameter item with the `user`

role.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | string or array | Yes | ||
| role | enum | The role of the message, which is always `user` .Possible values: `user` |
Yes |

### OpenAI.ResponsesUserMessageItemResource

A message resource item with the `user`

role.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| content | array | The content associated with the message. | Yes | |
| role | enum | The role of the message, which is always `user` .Possible values: `user` |
Yes |

### OpenAI.ServiceTier

Specifies the processing type used for serving the request.

- If set to 'auto', then the request will be processed with the service tier configured in the Project settings. Unless otherwise configured, the Project will use 'default'.
- If set to 'default', then the request will be processed with the standard pricing and performance for the selected model.
- If set to '
[flex](https://platform.openai.com/docs/guides/flex-processing)' or 'priority', then the request will be processed with the corresponding service tier.[Contact sales](https://openai.com/contact-sales)to learn more about Priority processing. - When not set, the default behavior is 'auto'.

When the `service_tier`

parameter is set, the response body will include the `service_tier`

value based on the processing mode actually used to serve the request. This response value
may be different from the value set in the parameter.

| Property | Value |
|---|---|
Description |
Specifies the processing type used for serving the request. * If set to 'auto', then the request will be processed with the service tier configured in the Project settings. Unless otherwise configured, the Project will use 'default'. * If set to 'default', then the request will be processed with the standard pricing and performance for the selected model. * If set to '
or 'priority', then the request will be processed with the corresponding service tier.
* When not set, the default behavior is 'auto'. When the `service_tier` parameter is set, the response body will include the `service_tier` value based on the processing mode actually used to serve the request. This response value may be different from the value set in the parameter. |
Type |
string |
Values |
`auto` `default` `flex` `scale` `priority` |

### OpenAI.TextResponseFormatConfiguration

An object specifying the format that the model must output.

Configuring `{ "type": "json_schema" }`

enables Structured Outputs,
which ensures the model will match your supplied JSON schema. Learn more in the

The default format is `{ "type": "text" }`

with no additional options.

*Not recommended for gpt-4o and newer models:**

Setting to `{ "type": "json_object" }`

enables the older JSON mode, which
ensures the message the model generates is valid JSON. Using `json_schema`

is preferred for models that support it.

### Discriminator for OpenAI.TextResponseFormatConfiguration

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | string | Yes |

### OpenAI.Tool

### Discriminator for OpenAI.Tool

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`function` |
|

`file_search`

[OpenAI.FileSearchTool](#openaifilesearchtool)`computer_use_preview`

[OpenAI.ComputerUsePreviewTool](#openaicomputerusepreviewtool)`web_search_preview`

[OpenAI.WebSearchPreviewTool](#openaiwebsearchpreviewtool)`code_interpreter`

[OpenAI.CodeInterpreterTool](#openaicodeinterpretertool)`image_generation`

[OpenAI.ImageGenTool](#openaiimagegentool)`local_shell`

[OpenAI.LocalShellTool](#openailocalshelltool)`mcp`

[OpenAI.MCPTool](#openaimcptool)`bing_grounding`

[BingGroundingAgentTool](#binggroundingagenttool)`fabric_dataagent_preview`

[MicrosoftFabricAgentTool](#microsoftfabricagenttool)`sharepoint_grounding_preview`

[SharepointAgentTool](#sharepointagenttool)`azure_ai_search`

[AzureAISearchAgentTool](#azureaisearchagenttool)`openapi`

[OpenApiAgentTool](#openapiagenttool)`bing_custom_search_preview`

[BingCustomSearchAgentTool](#bingcustomsearchagenttool)`browser_automation_preview`

[BrowserAutomationAgentTool](#browserautomationagenttool)`azure_function`

[AzureFunctionAgentTool](#azurefunctionagenttool)`capture_structured_outputs`

[CaptureStructuredOutputsTool](#capturestructuredoutputstool)`a2a_preview`

[A2ATool](#a2atool)`memory_search`

[MemorySearchTool](#memorysearchtool)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.ToolChoiceObject

### Discriminator for OpenAI.ToolChoiceObject

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`file_search` |
|

`computer_use_preview`

[OpenAI.ToolChoiceObjectComputer](#openaitoolchoiceobjectcomputer)`web_search_preview`

[OpenAI.ToolChoiceObjectWebSearch](#openaitoolchoiceobjectwebsearch)`image_generation`

[OpenAI.ToolChoiceObjectImageGen](#openaitoolchoiceobjectimagegen)`code_interpreter`

[OpenAI.ToolChoiceObjectCodeInterpreter](#openaitoolchoiceobjectcodeinterpreter)`function`

[OpenAI.ToolChoiceObjectFunction](#openaitoolchoiceobjectfunction)`mcp`

[OpenAI.ToolChoiceObjectMCP](#openaitoolchoiceobjectmcp)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

[Learn more about built-in tools](https://platform.openai.com/docs/guides/tools).### OpenAI.ToolChoiceObjectCodeInterpreter

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `code_interpreter` |
Yes |

### OpenAI.ToolChoiceObjectComputer

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `computer_use_preview` |
Yes |

### OpenAI.ToolChoiceObjectFileSearch

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `file_search` |
Yes |

### OpenAI.ToolChoiceObjectFunction

Use this option to force the model to call a specific function.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| name | string | The name of the function to call. | Yes | |
| type | enum | For function calling, the type is always `function` .Possible values: `function` |
Yes |

### OpenAI.ToolChoiceObjectImageGen

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `image_generation` |
Yes |

### OpenAI.ToolChoiceObjectMCP

Use this option to force the model to call a specific tool on a remote MCP server.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| name | string | The name of the tool to call on the server. | No | |
| server_label | string | The label of the MCP server to use. | Yes | |
| type | enum | For MCP tools, the type is always `mcp` .Possible values: `mcp` |
Yes |

### OpenAI.ToolChoiceObjectType

Indicates that the model should use a built-in tool to generate a response.
[Learn more about built-in tools](https://platform.openai.com/docs/guides/tools).

| Property | Value |
|---|---|
Description |
Indicates that the model should use a built-in tool to generate a response. |
|

**Type****Values**`file_search`

`function`

`computer_use_preview`

`web_search_preview`

`image_generation`

`code_interpreter`

`mcp`

### OpenAI.ToolChoiceObjectWebSearch

Note: web_search is not yet available via Azure OpenAI.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `web_search_preview` |
Yes |

### OpenAI.ToolChoiceOptions

Controls which (if any) tool is called by the model.

`none`

means the model will not call any tool and instead generates a message.

`auto`

means the model can pick between generating a message or calling one or
more tools.

`required`

means the model must call one or more tools.

| Property | Value |
|---|---|
Description |
Controls which (if any) tool is called by the model.`none` means the model will not call any tool and instead generates a message.`auto` means the model can pick between generating a message or calling one ormore tools. `required` means the model must call one or more tools. |
Type |
string |
Values |
`none` `auto` `required` |

### OpenAI.ToolType

A tool that can be used to generate a response.

| Property | Value |
|---|---|
Description |
A tool that can be used to generate a response. |
Type |
string |
Values |
`file_search` `function` `computer_use_preview` `web_search_preview` `mcp` `code_interpreter` `image_generation` `local_shell` `bing_grounding` `browser_automation_preview` `fabric_dataagent_preview` `sharepoint_grounding_preview` `azure_ai_search` `openapi` `bing_custom_search_preview` `capture_structured_outputs` `a2a_preview` `azure_function` `memory_search` |

### OpenAI.TopLogProb

The top log probability of a token.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| bytes | array | Yes | ||
| logprob | number | Yes | ||
| token | string | Yes |

### OpenAI.UpdateConversationRequest

Update a conversation

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No |

### OpenAI.VectorStoreFileAttributes

Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters, booleans, or numbers.

**Type**: object

### OpenAI.WebSearchAction

### Discriminator for OpenAI.WebSearchAction

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`find` |
|

`open_page`

[OpenAI.WebSearchActionOpenPage](#openaiwebsearchactionopenpage)`search`

[OpenAI.WebSearchActionSearch](#openaiwebsearchactionsearch)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type |
|

### OpenAI.WebSearchActionFind

Action type "find": Searches for a pattern within a loaded page.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| pattern | string | The pattern or text to search for within the page. | Yes | |
| type | enum | The action type. Possible values: `find` |
Yes | |
| url | string | The URL of the page searched for the pattern. | Yes |

### OpenAI.WebSearchActionOpenPage

Action type "open_page" - Opens a specific URL from search results.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The action type. Possible values: `open_page` |
Yes | |
| url | string | The URL opened by the model. | Yes |

### OpenAI.WebSearchActionSearch

Action type "search" - Performs a web search query.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| query | string | The search query. | Yes | |
| sources | array | The sources used in the search. | No | |
| type | enum | The action type. Possible values: `search` |
Yes |

### OpenAI.WebSearchActionSearchSources

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | Possible values: `url` |
Yes | |
| url | string | Yes |

### OpenAI.WebSearchActionType

| Property | Value |
|---|---|
Type |
string |
Values |
`search` `open_page` `find` |

### OpenAI.WebSearchPreviewTool

Note: web_search is not yet available via Azure OpenAI.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| search_context_size | enum | High level guidance for the amount of context window space to use for the search. One of `low` , `medium` , or `high` . `medium` is the default.Possible values: `low` , `medium` , `high` |
No | |
| type | enum | The type of the web search tool. One of `web_search_preview` or `web_search_preview_2025_03_11` .Possible values: `web_search_preview` |
Yes | |
| user_location | object | No | ||
| └─ type |
|

### OpenAI.WebSearchToolCallItemParam

The results of a web search tool call. See the
[web search guide](https://platform.openai.com/docs/guides/tools-web-search) for more information.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| action | object | Yes | ||
| └─ type |
|

Possible values:

`web_search_call`

### OpenAI.WebSearchToolCallItemResource

The results of a web search tool call. See the
[web search guide](https://platform.openai.com/docs/guides/tools-web-search) for more information.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| action | object | Yes | ||
| └─ type |
|

Possible values:

`in_progress`

, `searching`

, `completed`

, `failed`

Possible values:

`web_search_call`

### OpenAI.integer

**Type**: integer

**Format**: int64

### OpenAI.numeric

**Type**: number

**Format**: double

### OpenApiAgentTool

The input definition information for an OpenAPI tool as used to configure an agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| openapi | object | The input definition information for an openapi function. | Yes | |
| └─ auth |
|

Possible values:

`openapi`

### OpenApiAnonymousAuthDetails

Security details for OpenApi anonymous authentication

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | enum | The object type, which is always 'anonymous'. Possible values: `anonymous` |
Yes |

### OpenApiAuthDetails

authentication details for OpenApiFunctionDefinition

### Discriminator for OpenApiAuthDetails

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`anonymous` |
|

`project_connection`

[OpenApiProjectConnectionAuthDetails](#openapiprojectconnectionauthdetails)`managed_identity`

[OpenApiManagedAuthDetails](#openapimanagedauthdetails)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | object | Authentication type for OpenApi endpoint. Allowed types are: - Anonymous (no authentication required) - Project Connection (requires project_connection_id to endpoint, as setup in Foundry) - Managed_Identity (requires audience for identity based auth) |
Yes |

### OpenApiAuthType

Authentication type for OpenApi endpoint. Allowed types are:

- Anonymous (no authentication required)
- Project Connection (requires project_connection_id to endpoint, as setup in Foundry)
- Managed_Identity (requires audience for identity based auth)

| Property | Value |
|---|---|
Type |
string |
Values |
`anonymous` `project_connection` `managed_identity` |

### OpenApiFunctionDefinition

The input definition information for an openapi function.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| auth | object | authentication details for OpenApiFunctionDefinition | Yes | |
| └─ type |
|

### OpenApiManagedAuthDetails

Security details for OpenApi managed_identity authentication

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| security_scheme | object | Security scheme for OpenApi managed_identity authentication | Yes | |
| └─ audience | string | Authentication scope for managed_identity auth type | No | |
| type | enum | The object type, which is always 'managed_identity'. Possible values: `managed_identity` |
Yes |

### OpenApiManagedSecurityScheme

Security scheme for OpenApi managed_identity authentication

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| audience | string | Authentication scope for managed_identity auth type | Yes |

### OpenApiProjectConnectionAuthDetails

Security details for OpenApi project connection authentication

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| security_scheme | object | Security scheme for OpenApi managed_identity authentication | Yes | |
| └─ project_connection_id | string | Project connection id for Project Connection auth type | No | |
| type | enum | The object type, which is always 'project_connection'. Possible values: `project_connection` |
Yes |

### OpenApiProjectConnectionSecurityScheme

Security scheme for OpenApi managed_identity authentication

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| project_connection_id | string | Project connection id for Project Connection auth type | Yes |

### PagedConnection

Paged collection of Connection items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The Connection items  | Yes |

### PagedDatasetVersion

Paged collection of DatasetVersion items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The DatasetVersion items  | Yes |

### PagedDeployment

Paged collection of Deployment items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The Deployment items  | Yes |

### PagedEvaluationRule

Paged collection of EvaluationRule items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The EvaluationRule items  | Yes |

### PagedEvaluationTaxonomy

Paged collection of EvaluationTaxonomy items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The EvaluationTaxonomy items  | Yes |

### PagedEvaluatorVersion

Paged collection of EvaluatorVersion items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The EvaluatorVersion items  | Yes |

### PagedIndex

Paged collection of Index items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The Index items  | Yes |

### PagedInsight

Paged collection of Insight items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The Insight items  | Yes |

### PagedRedTeam

Paged collection of RedTeam items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The RedTeam items  | Yes |

### PagedSchedule

Paged collection of Schedule items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The Schedule items  | Yes |

### PagedScheduleRun

Paged collection of ScheduleRun items

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| nextLink | string | The link to the next page of items | No | |
| value | array | The ScheduleRun items  | Yes |

### PendingUploadRequest

Represents a request for a pending upload.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| connectionName | string | Azure Storage Account connection name to use for generating temporary SAS token | No | |
| pendingUploadId | string | If PendingUploadId is not provided, a random GUID will be used. | No | |
| pendingUploadType | enum | BlobReference is the only supported type. Possible values: `BlobReference` |
Yes |

### PendingUploadResponse

Represents the response for a pending upload request

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| blobReference | object | Blob reference details. | Yes | |
| └─ blobUri | string | Blob URI path for client to upload data. Example: `https://blob.windows.core.net/Container/Path` |
No | |
| └─ credential |
|

Possible values:

`BlobReference`

### PromptAgentDefinition

The prompt agent definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| instructions | string | A system (or developer) message inserted into the model's context. | No | |
| kind | enum | Possible values: `prompt` |
Yes | |
| model | string | The model deployment to use for this agent. | Yes | |
| reasoning | object | o-series models onlyConfiguration options for reasoning models. |
No | |
| └─ effort |
|

Currently supported values are none, minimal, low, medium, and high.

Reducing reasoning effort can result in faster responses and fewer tokens used on reasoning in a response.

gpt-5.1 defaults to none, which does not perform reasoning. The supported reasoning values for gpt-5.1 are none, low, medium, and high. Tool calls are supported for all reasoning values in gpt-5.1.

All models before gpt-5.1 default to medium reasoning effort, and do not support none.

The gpt-5-pro model defaults to (and only supports) high reasoning effort.

**Deprecated**: use`summary`

instead. A summary of the reasoning performed by the model. This can be useful for debugging and understanding the model's reasoning process. One of `auto`

, `concise`

, or `detailed`

.Possible values:

`auto`

, `concise`

, `detailed`

useful for debugging and understanding the model's reasoning process.

One of

`auto`

, `concise`

, or `detailed`

.Possible values:

`auto`

, `concise`

, `detailed`

We generally recommend altering this or

`top_p`

but not both.[OpenAI.ResponseTextFormatConfiguration](#openairesponsetextformatconfiguration)can specify which tool to use by setting the

`tool_choice`

parameter.where the model considers the results of the tokens with top_p probability

mass. So 0.1 means only the tokens comprising the top 10% probability mass

are considered.

We generally recommend altering this or

`temperature`

but not both.### PromptBasedEvaluatorDefinition

Prompt-based evaluator

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| prompt_text | string | The prompt text used for evaluation | Yes | |
| type | enum | Possible values: `prompt` |
Yes |

### ProtocolVersionRecord

A record mapping for a single protocol and its version.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| protocol | object | Yes | ||
| version | string | The version string for the protocol, e.g. 'v0.1.1'. | Yes |

### RaiConfig

Configuration for Responsible AI (RAI) content filtering and safety features.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| rai_policy_name | string | The name of the RAI policy to apply. | Yes |

### RecurrenceSchedule

Recurrence schedule model.

### Discriminator for RecurrenceSchedule

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`Hourly` |
|

`Daily`

[DailyRecurrenceSchedule](#dailyrecurrenceschedule)`Weekly`

[WeeklyRecurrenceSchedule](#weeklyrecurrenceschedule)`Monthly`

[MonthlyRecurrenceSchedule](#monthlyrecurrenceschedule)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | object | Recurrence type. | Yes |

### RecurrenceTrigger

Recurrence based trigger.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| endTime | string | End time for the recurrence schedule in ISO 8601 format. | No | |
| interval | integer | Interval for the recurrence schedule. | Yes | |
| schedule | object | Recurrence schedule model. | Yes | |
| └─ type |
|

Possible values:

`Recurrence`

### RecurrenceType

Recurrence type.

| Property | Value |
|---|---|
Description |
Recurrence type. |
Type |
string |
Values |
`Hourly` `Daily` `Weekly` `Monthly` |

### RedTeam

Red team details.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| applicationScenario | string | Application scenario for the red team operation, to generate scenario specific attacks. | No | |
| attackStrategies | array | List of attack strategies or nested lists of attack strategies. | No | |
| displayName | string | Name of the red-team run. | No | |
| id | string | Identifier of the red team run. | Yes | |
| numTurns | integer | Number of simulation rounds. | No | |
| properties | object | Red team's properties. Unlike tags, properties are add-only. Once added, a property cannot be removed. | No | |
| riskCategories | array | List of risk categories to generate attack objectives for. | No | |
| simulationOnly | boolean | Simulation-only or Simulation + Evaluation. Default false, if true the scan outputs conversation not evaluation result. | No | False |
| status | string | Status of the red-team. It is set by service and is read-only. | No | |
| tags | object | Red team's tags. Unlike properties, tags are fully mutable. | No | |
| target | object | Abstract class for target configuration. | Yes | |
| └─ type | string | Type of the model configuration. | No |

### RedTeamItemGenerationParams

Represents the parameters for red team item generation.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| attack_strategies | array | The collection of attack strategies to be used. | Yes | |
| num_turns | integer | The number of turns allowed in the game. | Yes | |
| type | enum | The type of item generation parameters, always `red_team` .Possible values: `red_team` |
Yes |

### RiskCategory

Risk category for the attack objective.

| Property | Value |
|---|---|
Description |
Risk category for the attack objective. |
Type |
string |
Values |
`HateUnfairness` `Violence` `Sexual` `SelfHarm` `ProtectedMaterial` `CodeVulnerability` `UngroundedAttributes` `ProhibitedActions` `SensitiveDataLeakage` `TaskAdherence` |

### SASCredentials

Shared Access Signature (SAS) credential definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| SAS | string | SAS token | No | |
| type | enum | The credential type Possible values: `SAS` |
Yes |

### SampleType

The type of sample used in the analysis.

| Property | Value |
|---|---|
Type |
string |
Values |
`EvaluationResultSample` |

### SasCredential

SAS Credential definition

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| sasUri | string | SAS uri | Yes | |
| type | enum | Type of credential Possible values: `SAS` |
Yes |

### Schedule

Schedule model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | Description of the schedule. | No | |
| displayName | string | Name of the schedule. | No | |
| enabled | boolean | Enabled status of the schedule. | Yes | |
| id | string | Identifier of the schedule. | Yes | |
| properties | object | Schedule's properties. Unlike tags, properties are add-only. Once added, a property cannot be removed. | No | |
| provisioningStatus | object | Schedule provisioning status. | No | |
| systemData | object | System metadata for the resource. | Yes | |
| tags | object | Schedule's tags. Unlike properties, tags are fully mutable. | No | |
| task | object | Schedule task model. | Yes | |
| └─ configuration | object | Configuration for the task. | No | |
| └─ type |
|

[TriggerType](#triggertype)### ScheduleProvisioningStatus

Schedule provisioning status.

| Property | Value |
|---|---|
Description |
Schedule provisioning status. |
Type |
string |
Values |
`Creating` `Updating` `Deleting` `Succeeded` `Failed` |

### ScheduleRun

Schedule run model.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| error | string | Error information for the schedule run. | No | |
| id | string | Identifier of the schedule run. | Yes | |
| properties | object | Properties of the schedule run. | Yes | |
| scheduleId | string | Identifier of the schedule. | Yes | |
| success | boolean | Trigger success status of the schedule run. | Yes | |
| triggerTime | string | Trigger time of the schedule run. | No |

### ScheduleTask

Schedule task model.

### Discriminator for ScheduleTask

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`Evaluation` |
|

`Insight`

[InsightScheduleTask](#insightscheduletask)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| configuration | object | Configuration for the task. | No | |
| type | object | Type of the task. | Yes |

### ScheduleTaskType

Type of the task.

| Property | Value |
|---|---|
Description |
Type of the task. |
Type |
string |
Values |
`Evaluation` `Insight` |

### SeedPromptsRedTeamItemGenerationParams

Represents the parameters for red team item generation with seed prompts.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| attack_strategies | array | The collection of attack strategies to be used. | Yes | |
| num_turns | integer | The number of turns allowed in the game. | Yes | |
| source | object | Yes | ||
| └─ content | array | The content of the jsonl file. | No | |
| └─ id | string | The identifier of the file. | No | |
| └─ type | enum | The type of jsonl source. Always `file_id` .Possible values: `file_id` |
No | |
| type | enum | The type of item generation parameters, always `red_team` .Possible values: `red_team_seed_prompts` |
Yes |

### SharepointAgentTool

The input definition information for a sharepoint tool as used to configure an agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| sharepoint_grounding_preview | object | The sharepoint grounding tool parameters. | Yes | |
| └─ project_connections | array | The project connections attached to this tool. There can be a maximum of 1 connection resource attached to the tool. |
No | |
| type | enum | The object type, which is always 'sharepoint_grounding'. Possible values: `sharepoint_grounding_preview` |
Yes |

### SharepointGroundingToolParameters

The sharepoint grounding tool parameters.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| project_connections | array | The project connections attached to this tool. There can be a maximum of 1 connection resource attached to the tool. |
No |

### Sku

Sku information

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| capacity | integer | Sku capacity | Yes | |
| family | string | Sku family | Yes | |
| name | string | Sku name | Yes | |
| size | string | Sku size | Yes | |
| tier | string | Sku tier | Yes |

### StructuredInputDefinition

An structured input that can participate in prompt template substitutions and tool argument binding.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| default_value | The default value for the input if no run-time value is provided. | No | ||
| description | string | A human-readable description of the input. | No | |
| required | boolean | Whether the input property is required when the agent is invoked. | No | False |
| schema | The JSON schema for the structured input (optional). | No |

### StructuredOutputDefinition

A structured output that can be produced by the agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A description of the output to emit. Used by the model to determine when to emit the output. | Yes | |
| name | string | The name of the structured output. | Yes | |
| schema | The JSON schema for the structured output. | Yes | ||
| strict | boolean | Whether to enforce strict validation. Default `true` . |
Yes |

### StructuredOutputsItemResource

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| output | The structured output captured during the response. | Yes | ||
| type | enum | Possible values: `structured_outputs` |
Yes |

### Target

Base class for targets with discriminator support.

### Discriminator for Target

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`azure_ai_model` |
|

`azure_ai_agent`

[AzureAIAgentTarget](#azureaiagenttarget)`azure_ai_assistant`

[AzureAIAssistantTarget](#azureaiassistanttarget)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | string | The type of target. | Yes |

### TargetCompletions

Represents a data source for target-based completion evaluation configuration.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| input_messages | object | No | ||
| └─ item_reference | string | No | ||
| └─ type | enum | Possible values: `item_reference` |
No | |
| source | object | Yes | ||
| └─ content | array | The content of the jsonl file. | No | |
| └─ id | string | The identifier of the file. | No | |
| └─ type | enum | The type of jsonl source. Always `file_id` .Possible values: `file_id` |
No | |
| target | object | Base class for targets with discriminator support. | Yes | |
| └─ type | string | The type of target. | No | |
| type | enum | The type of data source, always `TargetCompletions` .Possible values: `azure_ai_target_completions` |
Yes |

### TargetConfig

Abstract class for target configuration.

### Discriminator for TargetConfig

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`AzureOpenAIModel` |
|

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | string | Type of the model configuration. | Yes |

### TargetUpdate

Base class for targets with discriminator support.

### Discriminator for TargetUpdate

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`azure_ai_model` |
|

`azure_ai_assistant`

[AzureAIAssistantTargetUpdate](#azureaiassistanttargetupdate)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | string | The type of target. | Yes |

### TaxonomyCategory

Taxonomy category definition.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | Description of the taxonomy category. | No | |
| id | string | Unique identifier of the taxonomy category. | Yes | |
| name | string | Name of the taxonomy category. | Yes | |
| properties | object | Additional properties for the taxonomy category. | No | |
| riskCategory | object | Risk category for the attack objective. | Yes | |
| subCategories | array | List of taxonomy sub categories. | Yes |

### TaxonomyRedTeamItemGenerationParams

Represents the parameters for red team item generation with seed prompts.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| attack_strategies | array | The collection of attack strategies to be used. | Yes | |
| num_turns | integer | The number of turns allowed in the game. | Yes | |
| source | object | Yes | ||
| └─ content | array | The content of the jsonl file. | No | |
| └─ id | string | The identifier of the file. | No | |
| └─ type | enum | The type of jsonl source. Always `file_id` .Possible values: `file_id` |
No | |
| type | enum | The type of item generation parameters, always `red_team` .Possible values: `red_team_taxonomy` |
Yes |

### TaxonomySubCategory

Taxonomy sub-category definition.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | Description of the taxonomy sub-category. | No | |
| enabled | boolean | List of taxonomy items under this sub-category. | Yes | |
| id | string | Unique identifier of the taxonomy sub-category. | Yes | |
| name | string | Name of the taxonomy sub-category. | Yes | |
| properties | object | Additional properties for the taxonomy sub-category. | No |

### ToolDescription

Description of a tool that can be used by an agent.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A brief description of the tool's purpose. | No | |
| name | string | The name of the tool. | No |

### ToolProjectConnection

A project connection resource.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| project_connection_id | string | A project connection in a ToolProjectConnectionList attached to this tool. | Yes |

### TracesEvalRunDataSource

Represents a data source for evaluation runs that operate over Agent traces stored in Application Insights.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| lookback_hours | integer | Lookback window (in hours) applied when retrieving traces from Application Insights. | No | 168 |
| trace_ids | array | Collection of Agent trace identifiers that should be evaluated. | Yes | |
| type | enum | The type of data source, always `azure_ai_traces` .Possible values: `azure_ai_traces` |
Yes |

### TreatmentEffectType

Treatment Effect Type.

| Property | Value |
|---|---|
Type |
string |
Values |
`TooFewSamples` `Inconclusive` `Changed` `Improved` `Degraded` |

### Trigger

Base model for Trigger of the schedule.

### Discriminator for Trigger

This component uses the property `type`

to discriminate between different types:

| Type Value | Schema |
|---|---|
`Cron` |
|

`Recurrence`

[RecurrenceTrigger](#recurrencetrigger)`OneTime`

[OneTimeTrigger](#onetimetrigger)| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| type | object | Type of the trigger. | Yes |

### TriggerType

Type of the trigger.

| Property | Value |
|---|---|
Description |
Type of the trigger. |
Type |
string |
Values |
`Cron` `Recurrence` `OneTime` |

### UpdateAgentFromManifestRequest

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| description | string | A human-readable description of the agent. | No | |
| manifest_id | string | The manifest ID to import the agent version from. | Yes | |
| metadata | object | Set of 16 key-value pairs that can be attached to an object. This can be useful for storing additional information about the object in a structured format, and querying for objects via API or the dashboard. Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters. |
No | |
| parameter_values | object | The inputs to the manifest that will result in a fully materialized Agent. | Yes |

### UpdateAgentRequest

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| definition | object | Yes | ||
| └─ kind |
|

[RaiConfig](#raiconfig)useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

### UpdateEvalParametersBody

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| metadata |
|

useful for storing additional information about the object in a structured

format, and querying for objects via API or the dashboard.

Keys are strings with a maximum length of 64 characters. Values are strings

with a maximum length of 512 characters.

Keys are strings with a maximum length of 64 characters. Values are strings with a maximum length of 512 characters.

### UserProfileMemoryItem

A memory item specifically containing user profile information extracted from conversations, such as preferences, interests, and personal details.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| kind | enum | The kind of the memory item. Possible values: `user_profile` |
Yes |

### WeeklyRecurrenceSchedule

Weekly recurrence schedule.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| daysOfWeek | array | Days of the week for the recurrence schedule. | Yes | |
| type | enum | Weekly recurrence type. Possible values: `Weekly` |
Yes |

### WorkflowActionOutputItemResource

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| action_id | string | Unique identifier for the action. | Yes | |
| kind | string | The kind of CSDL action (e.g., 'SetVariable', 'InvokeAzureAgent'). | Yes | |
| parent_action_id | string | ID of the parent action if this is a nested action. | No | |
| previous_action_id | string | ID of the previous action if this action follows another. | No | |
| status | enum | Status of the action (e.g., 'in_progress', 'completed', 'failed', 'cancelled'). Possible values: `completed` , `failed` , `in_progress` , `cancelled` |
Yes | |
| type | enum | Possible values: `workflow_action` |
Yes |

### WorkflowAgentDefinition

The workflow agent definition.

| Name | Type | Description | Required | Default |
|---|---|---|---|---|
| kind | enum | Possible values: `workflow` |
Yes | |
| workflow | string | The CSDL YAML definition of the workflow. | No |

### integer

**Type**: integer

**Format**: int64
