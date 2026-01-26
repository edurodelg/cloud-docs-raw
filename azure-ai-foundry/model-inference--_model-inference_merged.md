---
merged_at: 2026-01-26T23:20:36.870256
merged_files: 3
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/supported-languages -->

# Supported programming languages for Azure AI Inference SDK

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

If you're currently using an Azure AI Inference beta SDK with Microsoft Foundry Models or Azure OpenAI service, we strongly recommend that you transition to the generally available [OpenAI/v1 API](https://aka.ms/openai/v1), which uses an OpenAI stable SDK.

For more information on how to migrate to the OpenAI/v1 API by using an SDK in your programming language of choice, see [Migrate from Azure AI Inference SDK to OpenAI SDK](../how-to/model-inference-to-openai-migration?view=foundry-classic).

All models deployed to Microsoft Foundry Models support the [Azure AI Model Inference API](https://aka.ms/azureai/modelinference) and its associated family of SDKs.

To use these SDKs, connect them to the [Azure AI model inference URI](how-to/inference?view=foundry-classic#azure-openai-inference-endpoint) (usually in the form `https://<resource-name>.services.ai.azure.com/models`

).

## Azure AI Inference package

The Azure AI Inference package allows you to consume all models deployed to the Foundry resource and easily switch the model deployment from one to another. The Azure AI Inference package is part of the Microsoft Foundry SDK.

| Language | Documentation | Package | Examples |
|---|---|---|---|
| C# |
|

[azure-ai-inference (NuGet)](https://www.nuget.org/packages/Azure.AI.Inference/)[C# examples](https://aka.ms/azsdk/azure-ai-inference/csharp/samples)[Reference](https://aka.ms/azsdk/azure-ai-inference/java/reference)[azure-ai-inference (Maven)](https://central.sonatype.com/artifact/com.azure/azure-ai-inference/)[Java examples](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-inference/src/samples)[Reference](/en-us/javascript/api/@azure-rest/ai-inference)[@azure/ai-inference (npm)](https://www.npmjs.com/package/@azure/ai-inference)[JavaScript examples](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Reference](https://aka.ms/azsdk/azure-ai-inference/python/reference)[azure-ai-inference (PyPi)](https://pypi.org/project/azure-ai-inference/)[Python examples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-inference/samples)## Integrations

| Framework | Language | Documentation | Package | Examples |
|---|---|---|---|---|
| LangChain | Python |
|

[langchain-azure-ai (PyPi)](https://pypi.org/project/langchain-azure-ai/)[Python examples](https://github.com/Azure-Samples/azureai-samples/tree/main/scenarios/langchain)[Reference](https://aka.ms/azsdk/azure-ai-inference/python/reference)[llama-index-llms-azure-inference (PyPi)](https://pypi.org/project/llama-index-llms-azure-inference/)[llama-index-embeddings-azure-inference (PyPi)](https://pypi.org/project/llama-index-embeddings-azure-inference/)[Python examples](https://github.com/Azure-Samples/azureai-samples/tree/main/scenarios/llama-index)[Reference](/en-us/semantic-kernel/overview)[semantic-kernel[azure] (PyPi)](https://pypi.org/project/semantic-kernel/)[Python examples](../../ai-studio/how-to/develop/semantic-kernel?view=foundry-classic)[Reference](https://microsoft.github.io/autogen/stable/reference/python/autogen_ext.models.azure.html#autogen_ext.models.azure.AzureAIChatCompletionClient)[autogen-ext[azure] (PyPi)](https://pypi.org/project/autogen-ext/)[Quickstart](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/quickstart.html)## Limitations

Foundry doesn't support the Cohere SDK or the Mistral SDK.

## Next step

- To see what models are currently supported, see
[Foundry Models and capabilities](concepts/models?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/quotas-limits -->

# Microsoft Foundry Models quotas and limits

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This article provides a quick reference and detailed description of the quotas and limits for Microsoft Foundry Models. For quotas and limits specific to the Azure OpenAI in Foundry Models, see [Quota and limits in Azure OpenAI](../openai/quotas-limits?view=foundry-classic).

## Quotas and limits reference

Azure uses quotas and limits to prevent budget overruns due to fraud and to honor Azure capacity constraints. Consider these limits as you scale for production workloads. The following sections provide a quick guide to the default quotas and limits that apply to Azure AI model inference service in Foundry:

### Resource limits (per Azure subscription, per region)

| Limit name | Limit value |
|---|---|
| Foundry resources per region per Azure subscription | 100 |
| Max projects per resource | 250 |
| Max deployments per resource (model deployments within a Foundry resource) | 32 |

### Rate limits

The following table lists limits for Foundry Models for the following rates:

- Tokens per minute
- Requests per minute
- Concurrent request

| Models | Tokens per minute | Requests per minute | Concurrent requests |
|---|---|---|---|
| Azure OpenAI models | Varies per model and SKU. See
|

[limits for Azure OpenAI](../openai/quotas-limits?view=foundry-classic).- DeepSeek-V3-0324

- Llama-4-Maverick-17B-128E-Instruct-FP8

- Grok 3

- Grok 3 mini

- Medium: 30

- High (Enterprise): 100

- Flux.1-Kontext Pro

To increase your quota:

- For Azure OpenAI, use
[Foundry Service: Request for Quota Increase](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR4xPXO648sJKt4GoXAed-0pUMFE1Rk9CU084RjA0TUlVSUlMWEQzVkJDNCQlQCN0PWcu)to submit your request. - For other models, see
[request increases to the default limits](#request-increases-to-the-default-limits).

Due to high demand, we evaluate limit increase requests per request.

### Other limits

| Limit name | Limit value |
|---|---|
Max number of custom headers in API requests1 |
10 |

1 Our current APIs allow up to 10 custom headers, which the pipeline passes through and returns. If you exceed this header count, your request results in an HTTP 431 error. To resolve this error, reduce the header volume. **Future API versions won't pass through custom headers**. We recommend that you don't depend on custom headers in future system architectures.

## Usage tiers

Global Standard deployments use Azure's global infrastructure to dynamically route customer traffic to the data center with best availability for the customer's inference requests. This infrastructure enables more consistent latency for customers with low to medium levels of traffic. Customers with high sustained levels of usage might see more variabilities in response latency.

The Usage Limit determines the level of usage above which customers might see larger variability in response latency. A customer's usage is defined per model and is the total tokens consumed across all deployments in all subscriptions in all regions for a given tenant.

## Request increases to the default limits

Quota increase requests can be submitted via the [quota increase request form](https://aka.ms/oai/stuquotarequest). Due to high demand, quota increase requests are accepted and filled in the order they're received. Priority is given to customers who generate traffic that consumes the existing quota allocation. Your request might be denied if this condition isn't met.

You can [submit a service request](../../ai-services/cognitive-services-support-options?view=foundry-classic&context=/azure/ai-foundry/openai/context/context) for other rate limits.

## General best practices to stay within rate limits

To minimize issues related to rate limits, use the following techniques:

- Implement retry logic in your application.
- Avoid sharp changes in the workload. Increase the workload gradually.
- Test different load increase patterns.
- Increase the quota assigned to your deployment. Move quota from another deployment, if necessary.

## Setting client side timeout

We recommend explicitly setting the client side timeout as follows.

Note

If not explicitly set, the client side timeout exists as per the library used, and may not be the same limits as above.

- Reasoning models (models that generate intermediate reasoning tokens before producing a summarized response): up to 29 minutes.
- Non-reasoning models:
- For streaming, up to 60 seconds.
- For non-streaming requests, up to 29 minutes.


29 minutes here does not mean all requests will take 29 minutes but rather depending on context tokens, generated tokens, and cache hit rates, requests can take up to 29 minutes.

You will need to set a timeout less than the above tuned to your traffic patterns.

For reasoning models including streaming requests, all the reasoning tokens are first generated and then summarized before sending the first response token back to the user.

You can modify the [reasoning effort](../openai/how-to/reasoning?view=foundry-classic) parameter to control the number of reasoning tokens generated in the process.

## Next steps

- Learn more about the
[models available in Foundry Models](../model-inference/concepts/models?view=foundry-classic)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/overview -->

# Foundry Models sold directly by Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This article lists a selection of Microsoft Foundry Models sold directly by Azure along with their capabilities, [deployment types, and regions of availability](deployment-types?view=foundry-classic), excluding [deprecated and legacy models](../../concepts/model-lifecycle-retirement?view=foundry-classic#deprecated). To see a list of Azure OpenAI models that are supported by the Foundry Agent Service, see [Models supported by Agent Service](../../agents/concepts/model-region-support?view=foundry-classic).

Models sold directly by Azure include all Azure OpenAI models and specific, selected models from top providers.

Depending on the [kind of project](../../what-is-foundry?view=foundry-classic&preserve-view=true#work-in-a-foundry-project) you use in Microsoft Foundry, you see a different selection of models. Specifically, if you use a Foundry project built on a Foundry resource, you see the models that are available for standard deployment to a Foundry resource. Alternatively, if you use a hub-based project hosted by a Foundry hub, you see models that are available for deployment to managed compute and serverless APIs. These model selections often overlap because many models support multiple [deployment options](../../concepts/deployments-overview?view=foundry-classic).

Foundry Models are available for standard deployment to a Foundry resource.

To learn more about attributes of Foundry Models sold directly by Azure, see [Explore Foundry Models](../../concepts/foundry-models-overview?view=foundry-classic#models-sold-directly-by-azure).

Note

Foundry Models sold directly by Azure also include select models from top model providers, such as:

- Black Forest Labs:
`FLUX.2-pro`

,`FLUX.1-Kontext-pro`

,`FLUX-1.1-pro`

- Cohere:
`Cohere-command-a`

,`embed-v-4-0`

,`Cohere-rerank-v4.0-pro`

,`Cohere-rerank-v4.0-fast`

- DeepSeek:
`DeepSeek-V3.2`

,`DeepSeek-V3.2-Speciale`

,`DeepSeek-V3.1`

,`DeepSeek-V3-0324`

,`DeepSeek-R1-0528`

,`DeepSeek-R1`

- Moonshot AI:
`Kimi-K2-Thinking`

- Meta:
`Llama-4-Maverick-17B-128E-Instruct-FP8`

,`Llama-3.3-70B-Instruct`

- Microsoft:
`MAI-DS-R1`

,`model-router`

- Mistral:
`mistral-document-ai-2505`

,`Mistral-Large-3`

- xAI:
`grok-code-fast-1`

,`grok-3`

,`grok-3-mini`

,`grok-4-fast-reasoning`

,`grok-4-fast-non-reasoning`

,`grok-4`


To learn about these models, switch to [Other model collections](models-sold-directly-by-azure?view=foundry-classic&pivots=azure-direct-others) at the top of this article.

## Azure OpenAI in Microsoft Foundry models

Azure OpenAI is powered by a diverse set of models with different capabilities and price points. Model availability varies by region and cloud. For Azure Government model availability, refer to [Azure OpenAI in Azure Government](../../openai/azure-government?view=foundry-classic).

| Models | Description |
|---|---|
|

**NEW**`gpt-5.2-codex`

, `gpt-5.2`

, `gpt-5.2-chat`

(**Preview**)[GPT-5.1 series](../../openai/concepts/models?view=foundry-classic#gpt-51)**NEW**`gpt-5.1`

, `gpt-5.1-chat`

, `gpt-5.1-codex`

, `gpt-5.1-codex-mini`

[Sora](/en-us/azure/ai-foundry/foundry-models/concepts/models-sold-directly-by-azure?pivots=azure-openai&tabs=global-standard-aoai%2Cstandard-chat-completions%2Cglobal-standard#video-generation-models)**NEW**sora-2[GPT-5 series](../../openai/concepts/models?view=foundry-classic#gpt-5)[gpt-oss](../../openai/concepts/models?view=foundry-classic#gpt-oss)[codex-mini](../../openai/concepts/models?view=foundry-classic#o-series-models)[GPT-4.1 series](../../openai/concepts/models?view=foundry-classic#gpt-41-series)[computer-use-preview](../../openai/concepts/models?view=foundry-classic#computer-use-preview)[o-series models](../../openai/concepts/models?view=foundry-classic#o-series-models)[Reasoning models](../../openai/how-to/reasoning?view=foundry-classic)with advanced problem solving and increased focus and capability.[GPT-4o, GPT-4o mini, and GPT-4 Turbo](../../openai/concepts/models?view=foundry-classic#gpt-4o-and-gpt-4-turbo)[Embeddings](../../openai/concepts/models?view=foundry-classic#embeddings)[Image generation](../../openai/concepts/models?view=foundry-classic#image-generation-models)`Video generation`

[Audio](../../openai/concepts/models?view=foundry-classic#audio-models)*speech in, speech out*conversational interactions or audio generation.## GPT-5.2

### Region availability

| Model | Region |
|---|---|
`gpt-5.2` |
See the
|

`gpt-5.2-chat`

[models table](#model-summary-table-and-region-availability).`gpt-5.2-codex`

Access will be granted based on Microsoft's eligibility criteria. Customers who previously applied and received access to a limited access model, don't need to reapply as their approved subscriptions will automatically be granted access upon model release.

| Model ID | Description | Context Window | Max Output Tokens | Training Data (up to) |
|---|---|---|---|---|
`gpt-5.2-codex` (2026-01-14) |
-
- Chat Completions API. -
- Structured outputs. - Text and image processing. - Functions, tools, and parallel tool calling. -
- Optimized for
|

Input: 272,000

Output: 128,000

`gpt-5.2`

(2025-12-11)[Reasoning](../../openai/how-to/reasoning?view=foundry-classic)- Chat Completions API.

-

[Responses API](../../openai/how-to/responses?view=foundry-classic).- Structured outputs.

- Text and image processing.

- Functions, tools, and parallel tool calling.

-

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic).Input: 272,000

Output: 128,000

`gpt-5.2-chat`

(2025-12-11)**Preview**-

[Responses API](../../openai/how-to/responses?view=foundry-classic).- Structured outputs

- Functions, tools, and parallel tool calling.

Input: 111,616

Output: 16,384

Caution

We don't recommend using preview models in production. We'll upgrade all deployments of preview models to either future preview versions or to the latest stable, generally available version. Models that are designated preview don't follow the standard Azure OpenAI model lifecycle.

## GPT-5.1

### Region availability

| Model | Region |
|---|---|
`gpt-5.1` |
See the
|

`gpt-5.1-chat`

[models table](#model-summary-table-and-region-availability).`gpt-5.1-codex`

[models table](#model-summary-table-and-region-availability).`gpt-5.1-codex-mini`

[models table](#model-summary-table-and-region-availability).`gpt-5.1-codex-max`

[models table](#model-summary-table-and-region-availability).Access will be granted based on Microsoft's eligibility criteria. Customers who previously applied and received access to a limited access model, don't need to reapply as their approved subscriptions will automatically be granted access upon model release.

| Model ID | Description | Context Window | Max Output Tokens | Training Data (up to) |
|---|---|---|---|---|
`gpt-5.1` (2025-11-13) |
-
- Chat Completions API. -
- Structured outputs. - Text and image processing. - Functions, tools, and parallel tool calling. -
|

Input: 272,000

Output: 128,000

`gpt-5.1-chat`

(2025-11-13) **Preview**[Reasoning](../../openai/how-to/reasoning?view=foundry-classic)- Chat Completions API.

-

[Responses API](../../openai/how-to/responses?view=foundry-classic).- Structured outputs

- Functions, tools, and parallel tool calling.

Input: 111,616

Output: 16,384

`gpt-5.1-codex`

(2025-11-13)[Responses API](../../openai/how-to/responses?view=foundry-classic)only.- Text and image processing

- Structured outputs.

- Functions, tools, and parallel tool calling.

-

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic)- Optimized for

[Codex CLI & Codex VS Code extension](../../openai/how-to/codex?view=foundry-classic)Input: 272,000

Output: 128,000

`gpt-5.1-codex-mini`

(2025-11-13)[Responses API](../../openai/how-to/responses?view=foundry-classic)only.- Text and image processing

- Structured outputs.

- Text and image processing.

- Functions, tools, and parallel tool calling.

-

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic)- Optimized for

[Codex CLI & Codex VS Code extension](../../openai/how-to/codex?view=foundry-classic)Input: 272,000

Output: 128,000

`gpt-5.1-codex-max`

(2025-12-04)[Responses API](../../openai/how-to/responses?view=foundry-classic)only.- Text and image processing

- Structured outputs.

- Text and image processing.

- Functions, tools, and parallel tool calling.

-

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic)- Optimized for

[Codex CLI & Codex VS Code extension](../../openai/how-to/codex?view=foundry-classic)Input: 272,000

Output: 128,000

Caution

We don't recommend using preview models in production. We'll upgrade all deployments of preview models to either future preview versions or to the latest stable, generally available version. Models that are designated preview don't follow the standard Azure OpenAI model lifecycle.

Important

`gpt-5.1`

`reasoning_effort`

defaults to`none`

. When upgrading from previous reasoning models to`gpt-5.1`

, keep in mind that you may need to update your code to explicitly pass a`reasoning_effort`

level if you want reasoning to occur.`gpt-5.1-chat`

adds built-in reasoning capabilities. Like other[reasoning models](../../openai/how-to/reasoning?view=foundry-classic)it does not support parameters like`temperature`

. If you upgrade from using`gpt-5-chat`

(which is not a reasoning model) to`gpt-5.1-chat`

make sure you remove any custom parameters like`temperature`

from your code which are not supported by reasoning models.`gpt-5.1-codex-max`

adds support for setting`reasoning_effort`

to`xhigh`

. Reasoning effort`none`

is not supported with`gpt-5.1-codex-max`

.

## GPT-5

### Region availability

| Model | Region |
|---|---|
`gpt-5` (2025-08-07) |
See the
|

`gpt-5-mini`

(2025-08-07)[models table](#model-summary-table-and-region-availability).`gpt-5-nano`

(2025-08-07)[models table](#model-summary-table-and-region-availability).`gpt-5-chat`

(2025-08-07)[models table](#model-summary-table-and-region-availability).`gpt-5-chat`

(2025-10-03)[models table](#model-summary-table-and-region-availability).`gpt-5-codex`

(2025-09-11)[models table](#model-summary-table-and-region-availability).`gpt-5-pro`

(2025-10-06)[models table](#model-summary-table-and-region-availability).[Registration is required for access to the gpt-5-pro, gpt-5, & gpt-5-codex models](https://aka.ms/oai/gpt5access).`gpt-5-mini`

,`gpt-5-nano`

, and`gpt-5-chat`

do not require registration.

Access will be granted based on Microsoft's eligibility criteria. Customers who previously applied and received access to `o3`

, don't need to reapply as their approved subscriptions will automatically be granted access upon model release.

| Model ID | Description | Context Window | Max Output Tokens | Training Data (up to) |
|---|---|---|---|---|
`gpt-5` (2025-08-07) |
-
- Chat Completions API. -
- Structured outputs. - Text and image processing. - Functions, tools, and parallel tool calling. -
|

Input: 272,000

Output: 128,000

`gpt-5-mini`

(2025-08-07)[Reasoning](../../openai/how-to/reasoning?view=foundry-classic)- Chat Completions API.

-

[Responses API](../../openai/how-to/responses?view=foundry-classic).- Structured outputs.

- Text and image processing.

- Functions, tools, and parallel tool calling.

-

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic).Input: 272,000

Output: 128,000

`gpt-5-nano`

(2025-08-07)[Reasoning](../../openai/how-to/reasoning?view=foundry-classic)- Chat Completions API.

-

[Responses API](../../openai/how-to/responses?view=foundry-classic).- Structured outputs.

- Text and image processing.

- Functions, tools, and parallel tool calling.

-

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic).Input: 272,000

Output: 128,000

`gpt-5-chat`

(2025-08-07)**Preview**-

[Responses API](../../openai/how-to/responses?view=foundry-classic).-

**Input**: Text/Image-

**Output**: Text only`gpt-5-chat`

(2025-10-03)**Preview**1-

[Responses API](../../openai/how-to/responses?view=foundry-classic).-

**Input**: Text/Image-

**Output**: Text only`gpt-5-codex`

(2025-09-11)[Responses API](../../openai/how-to/responses?view=foundry-classic)only.-

**Input**: Text/Image-

**Output**: Text only- Structured outputs.

- Text and image processing.

- Functions, tools, and parallel tool calling.

-

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic)- Optimized for

[Codex CLI & Codex VS Code extension](../../openai/how-to/codex?view=foundry-classic)Input: 272,000

Output: 128,000

`gpt-5-pro`

(2025-10-06)[Reasoning](../../openai/how-to/reasoning?view=foundry-classic)-

[Responses API](../../openai/how-to/responses?view=foundry-classic).- Structured outputs.

- Text and image processing.

- Functions and tools

-

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic).Input: 272,000

Output: 128,000

Note

1 `gpt-5-chat`

version `2025-10-03`

introduces a significant enhancement focused on emotional intelligence and mental health capabilities. This upgrade integrates specialized datasets and refined response strategies to improve the model's ability to:

**Understand and interpret emotional context**more accurately, enabling nuanced and empathetic interactions.**Provide supportive, responsible responses**in conversations related to mental health, ensuring sensitivity and adherence to best practices.

These improvements aim to make GPT-5-chat more context-aware, human-centric, and reliable in scenarios where emotional tone and well-being considerations are critical.

Caution

We don't recommend using preview models in production. We'll upgrade all deployments of preview models to either future preview versions or to the latest stable, generally available version. Models that are designated preview don't follow the standard Azure OpenAI model lifecycle.

## gpt-oss

### Region availability

| Model | Region |
|---|---|
`gpt-oss-120b` |
All Azure OpenAI regions |

### Capabilities

| Model ID | Description | Context Window | Max Output Tokens | Training Data (up to) |
|---|---|---|---|---|
`gpt-oss-120b` (Preview) |
- Text in/text out only - Chat Completions API - Streaming - Function calling - Structured outputs - Reasoning - Available for deployment 1 and via
|
131,072 | 131,072 | May 31, 2024 |
`gpt-oss-20b` (Preview) |
- Text in/text out only - Chat Completions API - Streaming - Function calling - Structured outputs - Reasoning - Available via
|
131,072 | 131,072 | May 31, 2024 |

1 Unlike other Azure OpenAI models `gpt-oss-120b`

requires a [Foundry project](/en-us/azure/ai-foundry/quickstarts/get-started-code?tabs=azure-ai-foundry) to deploy the model.

### Deploy with code

```
az cognitiveservices account deployment create \
--name "Foundry-project-resource" \
--resource-group "test-rg" \
--deployment-name "gpt-oss-120b" \
--model-name "gpt-oss-120b" \
--model-version "1" \
--model-format "OpenAI-OSS" \
--sku-capacity 10 \
--sku-name "GlobalStandard"
```


## GPT-4.1 series

### Region availability

| Model | Region |
|---|---|
`gpt-4.1` (2025-04-14) |
See the
|

`gpt-4.1-nano`

(2025-04-14)[models table](#model-summary-table-and-region-availability).`gpt-4.1-mini`

(2025-04-14)[models table](#model-summary-table-and-region-availability).### Capabilities

Important

A known issue is affecting all GPT 4.1 series models. Large tool or function call definitions that exceed 300,000 tokens will result in failures, even though the 1 million token context limit of the models wasn't reached.

The errors can vary based on API call and underlying payload characteristics.

Here are the error messages for the Chat Completions API:

`Error code: 400 - {'error': {'message': "This model's maximum context length is 300000 tokens. However, your messages resulted in 350564 tokens (100 in the messages, 350464 in the functions). Please reduce the length of the messages or functions.", 'type': 'invalid_request_error', 'param': 'messages', 'code': 'context_length_exceeded'}}`

`Error code: 400 - {'error': {'message': "Invalid 'tools[0].function.description': string too long. Expected a string with maximum length 1048576, but got a string with length 2778531 instead.", 'type': 'invalid_request_error', 'param': 'tools[0].function.description', 'code': 'string_above_max_length'}}`


Here's the error message for the Responses API:

`Error code: 500 - {'error': {'message': 'The server had an error processing your request. Sorry about that! You can retry your request, or contact us through an Azure support request at: https://go.microsoft.com/fwlink/?linkid=2213926 if you keep seeing this error. (Please include the request ID d2008353-291d-428f-adc1-defb5d9fb109 in your email.)', 'type': 'server_error', 'param': None, 'code': None}}`


| Model ID | Description | Context window | Max output tokens | Training data (up to) |
|---|---|---|---|---|
`gpt-4.1` (2025-04-14) |
- Text and image input - Text output - Chat completions API - Responses API - Streaming - Function calling - Structured outputs (chat completions) |
- 1,047,576 - 128,000 (provisioned managed deployments) - 300,000 (batch deployments) |
32,768 | May 31, 2024 |
`gpt-4.1-nano` (2025-04-14) |
- Text and image input - Text output - Chat completions API - Responses API - Streaming - Function calling - Structured outputs (chat completions) |
- 1,047,576 - 128,000 (provisioned managed deployments) - 300,000 (batch deployments) |
32,768 | May 31, 2024 |
`gpt-4.1-mini` (2025-04-14) |
- Text and image input - Text output - Chat completions API - Responses API - Streaming - Function calling - Structured outputs (chat completions) |
- 1,047,576 - 128,000 (provisioned managed deployments) - 300,000 (batch deployments) |
32,768 | May 31, 2024 |

## computer-use-preview

An experimental model trained for use with the [Responses API](../../openai/how-to/responses?view=foundry-classic) computer use tool.

It can be used with third-party libraries to allow the model to control mouse and keyboard input, while getting context from screenshots of the current environment.

Caution

We don't recommend using preview models in production. We'll upgrade all deployments of preview models to either future preview versions or to the latest stable, generally available version. Models that are designated preview don't follow the standard Azure OpenAI model lifecycle.

Registration is required to access `computer-use-preview`

. Access is granted based on Microsoft's eligibility criteria. Customers who have access to other limited access models still need to request access for this model.

To request access, go to [ computer-use-preview limited access model application](https://aka.ms/oai/cuaaccess). When access is granted, you need to create a deployment for the model.

### Region availability

| Model | Region |
|---|---|
`computer-use-preview` |
See the
|

### Capabilities

| Model ID | Description | Context window | Max output tokens | Training data (up to) |
|---|---|---|---|---|
`computer-use-preview` (2025-03-11) |
Specialized model for use with the
- Tools - Streaming - Text (input/output) - Image (input) |

## o-series models

The Azure OpenAI o-series models are designed to tackle reasoning and problem-solving tasks with increased focus and capability. These models spend more time processing and understanding the user's request, making them exceptionally strong in areas like science, coding, and math, compared to previous iterations.

| Model ID | Description | Max request (tokens) | Training data (up to) |
|---|---|---|---|
`codex-mini` (2025-05-16) |
Fine-tuned version of `o4-mini` . -
- Structured outputs. - Text and image processing. - Functions and tools.
|
Input: 200,000 Output: 100,000 |
May 31, 2024 |
`o3-pro` (2025-06-10) |
-
- Structured outputs. - Text and image processing. - Functions and tools.
|

Output: 100,000

`o4-mini`

(2025-04-16)*New*reasoning model, offering[enhanced reasoning abilities](../../openai/how-to/reasoning?view=foundry-classic).- Chat Completions API.

-

[Responses API](../../openai/how-to/responses?view=foundry-classic).- Structured outputs.

- Text and image processing.

- Functions and tools.

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic).Output: 100,000

`o3`

(2025-04-16)*New*reasoning model, offering[enhanced reasoning abilities](../../openai/how-to/reasoning?view=foundry-classic).- Chat Completions API.

-

[Responses API](../../openai/how-to/responses?view=foundry-classic).- Structured outputs.

- Text and image processing.

- Functions, tools, and parallel tool calling.

[Full summary of capabilities](../../openai/how-to/reasoning?view=foundry-classic).Output: 100,000

`o3-mini`

(2025-01-31)[Enhanced reasoning abilities](../../openai/how-to/reasoning?view=foundry-classic).- Structured outputs.

- Text-only processing.

- Functions and tools.

Output: 100,000

`o1`

(2024-12-17)[Enhanced reasoning abilities](../../openai/how-to/reasoning?view=foundry-classic).- Structured outputs.

- Text and image processing.

- Functions and tools.

Output: 100,000

`o1-preview`

(2024-09-12)Output: 32,768

`o1-mini`

(2024-09-12)- Global Standard deployment available by default.

- Standard (regional) deployments are currently only available for select customers who received access as part of the

`o1-preview`

limited access release.Output: 65,536

To learn more about advanced o-series models, see [Getting started with reasoning models](../../openai/how-to/reasoning?view=foundry-classic).

### Region availability

| Model | Region |
|---|---|
`codex-mini` |
East US2 & Sweden Central (Global Standard). |
`o3-pro` |
East US2 & Sweden Central (Global Standard). |
`o4-mini` |
See the
|

`o3`

[models table](#model-summary-table-and-region-availability).`o3-mini`

[models table](#model-summary-table-and-region-availability).`o1`

[models table](#model-summary-table-and-region-availability).`o1-preview`

[models table](#model-summary-table-and-region-availability). This model is available only for customers who were granted access as part of the original limited access.`o1-mini`

[models table](#model-summary-table-and-region-availability).## GPT-4o and GPT-4 Turbo

GPT-4o integrates text and images in a single model, which enables it to handle multiple data types simultaneously. This multimodal approach enhances accuracy and responsiveness in human-computer interactions. GPT-4o matches GPT-4 Turbo in English text and coding tasks while offering superior performance in non-English language tasks and vision tasks, setting new benchmarks for AI capabilities.

## GPT-4 and GPT-4 Turbo models

These models can be used only with the Chat Completions API.

See [Model versions](../../openai/concepts/model-versions?view=foundry-classic) to learn about how Azure OpenAI handles model version upgrades. See [Working with models](../../openai/how-to/working-with-models?view=foundry-classic) to learn how to view and configure the model version settings of your GPT-4 deployments.

| Model ID | Description | Max request (tokens) | Training data (up to) |
|---|---|---|---|
`gpt-4o` (2024-11-20) GPT-4o (Omni) |
- Structured outputs. - Text and image processing. - JSON Mode. - Parallel function calling. - Enhanced accuracy and responsiveness. - Parity with English text and coding tasks compared to GPT-4 Turbo with Vision. - Superior performance in non-English languages and in vision tasks. - Enhanced creative writing ability. |
Input: 128,000 Output: 16,384 |
October 2023 |
`gpt-4o` (2024-08-06) GPT-4o (Omni) |
- Structured outputs. - Text and image processing. - JSON Mode. - Parallel function calling. - Enhanced accuracy and responsiveness. - Parity with English text and coding tasks compared to GPT-4 Turbo with Vision. - Superior performance in non-English languages and in vision tasks. |
Input: 128,000 Output: 16,384 |
October 2023 |
`gpt-4o-mini` (2024-07-18) GPT-4o mini |
- Fast, inexpensive, capable model ideal for replacing GPT-3.5 Turbo series models. - Text and image processing. - JSON Mode. - Parallel function calling. |
Input: 128,000 Output: 16,384 |
October 2023 |
`gpt-4o` (2024-05-13) GPT-4o (Omni) |
- Text and image processing. - JSON Mode. - Parallel function calling. - Enhanced accuracy and responsiveness. - Parity with English text and coding tasks compared to GPT-4 Turbo with Vision. - Superior performance in non-English languages and in vision tasks. |
Input: 128,000 Output: 4,096 |
October 2023 |
`gpt-4` (turbo-2024-04-09) GPT-4 Turbo with Vision |
New generally available model. - Replacement for all previous GPT-4 preview models ( `vision-preview` , `1106-Preview` , `0125-Preview` ). -
|
Input: 128,000 Output: 4,096 |
December 2023 |

Caution

We don't recommend that you use preview models in production. We'll upgrade all deployments of preview models to either future preview versions or to the latest stable, generally available version. Models that are designated preview don't follow the standard Azure OpenAI model lifecycle.

## Embeddings

`text-embedding-3-large`

is the latest and most capable embedding model. You can't upgrade between embeddings models. To move from using `text-embedding-ada-002`

to `text-embedding-3-large`

, you need to generate new embeddings.

`text-embedding-3-large`

`text-embedding-3-small`

`text-embedding-ada-002`


OpenAI reports that testing shows that both the large and small third generation embeddings models offer better average multi-language retrieval performance with the [MIRACL](https://github.com/project-miracl/miracl) benchmark. They still maintain performance for English tasks with the [MTEB](https://github.com/embeddings-benchmark/mteb) benchmark.

| Evaluation benchmark | `text-embedding-ada-002` |
`text-embedding-3-small` |
`text-embedding-3-large` |
|---|---|---|---|
| MIRACL average | 31.4 | 44.0 | 54.9 |
| MTEB average | 61.0 | 62.3 | 64.6 |

The third generation embeddings models support reducing the size of the embedding via a new `dimensions`

parameter. Typically, larger embeddings are more expensive from a compute, memory, and storage perspective. When you can adjust the number of dimensions, you gain more control over overall cost and performance. The `dimensions`

parameter isn't supported in all versions of the OpenAI 1.x Python library. To take advantage of this parameter, we recommend that you upgrade to the latest version: `pip install openai --upgrade`

.

OpenAI's MTEB benchmark testing found that even when the third generation model's dimensions are reduced to less than the 1,536 dimensions of `text-embeddings-ada-002`

, performance remains slightly better.

## Image generation models

The image generation models generate images from text prompts that the user provides. GPT-image-1 series models are in limited access preview. DALL-E 3 is generally available for use with the REST APIs. DALL-E 2 and DALL-E 3 with client SDKs are in preview.

Registration is required to access `gpt-image-1`

, `gpt-image-1-mini`

, or `gpt-image-1.5`

. Access is granted based on Microsoft's eligibility criteria. Customers who have access to other limited access models still need to request access for this model.

To request access, fill out an application form: [Apply for GPT-image-1 access](https://aka.ms/oai/gptimage1access); [Apply for GPT-image-1.5 access](https://aka.ms/oai/gptimage1.5access). When access is granted, you need to create a deployment for the model.

### Region availability

| Model | Region |
|---|---|
`dall-e-3` |
East US Australia East Sweden Central |
`gpt-image-1` |
West US 3 (Global Standard) East US 2 (Global Standard) UAE North (Global Standard) Poland Central (Global Standard) Sweden Central (Global Standard) |
`gpt-image-1-mini` |
West US 3 (Global Standard) East US 2 (Global Standard) UAE North (Global Standard) Poland Central (Global Standard) Sweden Central (Global Standard) |
`gpt-image-1.5` |
West US 3 (Global Standard) East US 2 (Global Standard) UAE North (Global Standard) Poland Central (Global Standard) Sweden Central (Global Standard) |

## Video generation models

Sora is an AI model from OpenAI that can create realistic and imaginative video scenes from text instructions. Sora is in preview.

### Region availability

| Model | Region |
|---|---|
`sora` |
East US 2 (Global Standard) Sweden Central (Global Standard) |
`sora-2` |
East US 2 (Global Standard) Sweden Central (Global Standard) |

## Audio models

Audio models in Azure OpenAI are available via the `realtime`

, `completions`

, and `audio`

APIs.

### GPT-4o audio models

The GPT-4o audio models are part of the GPT-4o model family and support either low-latency, *speech in, speech out* conversational interactions or audio generation.

Caution

We don't recommend using preview models in production. We'll upgrade all deployments of preview models to either future preview versions or to the latest stable, generally available version. Models that are designated preview don't follow the standard Azure OpenAI model lifecycle.

Details about maximum request tokens and training data are available in the following table:

| Model ID | Description | Max request (tokens) | Training data (up to) |
|---|---|---|---|
`gpt-4o-mini-audio-preview` (2024-12-17) GPT-4o audio |
Audio model for audio and text generation. | Input: 128,000 Output: 16,384 |
September 2023 |
`gpt-4o-audio-preview` (2024-12-17) GPT-4o audio |
Audio model for audio and text generation. | Input: 128,000 Output: 16,384 |
September 2023 |
`gpt-4o-realtime-preview` (2025-06-03) GPT-4o audio |
Audio model for real-time audio processing. | Input: 128,000 Output: 4,096 |
October 2023 |
`gpt-4o-realtime-preview` (2024-12-17) GPT-4o audio |
Audio model for real-time audio processing. | Input: 128,000 Output: 4,096 |
October 2023 |
`gpt-4o-mini-realtime-preview` (2024-12-17) GPT-4o audio |
Audio model for real-time audio processing. | Input: 128,000 Output: 4,096 |
October 2023 |
`gpt-realtime` (2025-08-28) (GA)`gpt-realtime-mini` (2025-10-06)`gpt-realtime-mini-2025-12-15` (2025-12-15) `gpt-audio` (2025-08-28)`gpt-audio-mini` (2025-10-06) |
Audio model for real-time audio processing. | Input: 28,672 Output: 4,096 |
October 2023 |

To compare the availability of GPT-4o audio models across all regions, refer to the [models table](#global-standard-model-availability).

### Audio API

The audio models via the `/audio`

API can be used for speech to text, translation, and text to speech.

#### Speech-to-text models

| Model ID | Description | Max request (audio file size) |
|---|---|---|
`whisper` |
General-purpose speech recognition model. | 25 MB |
`gpt-4o-transcribe` |
Speech-to-text model powered by GPT-4o. | 25 MB |
`gpt-4o-mini-transcribe` |
Speech-to-text model powered by GPT-4o mini. | 25 MB |
`gpt-4o-transcribe-diarize` |
Speech-to-text model with automatic speech recognition. | 25 MB |
`gpt-4o-mini-transcribe-2025-12-15` |
Speech-to-text model with automatic speech recognition. Improved transcription accuracy and robustness. | 25 MB |

#### Speech translation models

| Model ID | Description | Max request (audio file size) |
|---|---|---|
`whisper` |
General-purpose speech recognition model. | 25 MB |

#### Text-to-speech models (preview)

| Model ID | Description |
|---|---|
`tts` |
Text-to-speech model optimized for speed. |
`tts-hd` |
Text-to-speech model optimized for quality. |
`gpt-4o-mini-tts` |
Text-to-speech model powered by GPT-4o mini. You can guide the voice to speak in a specific style or tone. |
`gpt-4o-mini-tts-2025-12-15` |
Text-to-speech model powered by GPT-4o mini. You can guide the voice to speak in a specific style or tone. |

## Model summary table and region availability

### Models by deployment type

Azure OpenAI provides customers with choices on the hosting structure that fits their business and usage patterns. The service offers two main types of deployment:

**Standard**: Has a global deployment option, routing traffic globally to provide higher throughput.**Provisioned**: Also has a global deployment option, allowing customers to purchase and deploy provisioned throughput units across Azure global infrastructure.

All deployments can perform the exact same inference operations, but the billing, scale, and performance are substantially different. To learn more about Azure OpenAI deployment types, see our [Deployment types guide](deployment-types?view=foundry-classic).

-
[Global Standard](#tabpanel_1_global-standard-aoai) -
[Global Provisioned managed](#tabpanel_1_global-ptum-aoai) -
[Global Batch](#tabpanel_1_global-batch) -
[Data Zone Standard](#tabpanel_1_datazone-standard) -
[Data Zone Provisioned managed](#tabpanel_1_datazone-provisioned-managed) -
[Data Zone Batch](#tabpanel_1_datazone-batch) -
[Standard](#tabpanel_1_standard) -
[Provisioned managed](#tabpanel_1_provisioned)

### Global Standard model availability

Region |
gpt-5.2-codex, 2026-01-14 |
gpt-5.2, 2025-12-11 |
gpt-5.2-chat, 2025-12-11 |
gpt-5.1-codex-max, 2025-12-04 |
gpt-5.1, 2025-11-13 |
gpt-5.1-chat, 2025-11-13 |
gpt-5.1-codex, 2025-11-13 |
gpt-5.1-codex-mini, 2025-11-13 |
gpt-5-pro, 2025-10-06 |
gpt-5-codex, 2025-09-15 |
gpt-5, 2025-08-07 |
gpt-5-mini, 2025-08-07 |
gpt-5-nano, 2025-08-07 |
gpt-5-chat, 2025-08-07 |
gpt-5-chat, 2025-10-03 |
o3-pro, 2025-06-10 |
codex-mini, 2025-05-16 |
sora, 2025-05-02 |
model-router, 2025-08-07 |
model-router, 2025-05-19 |
model-router, 2025-11-18 |
o3, 2025-04-16 |
o4-mini, 2025-04-16 |
gpt-image-1, 2025-04-15 |
gpt-4.1, 2025-04-14 |
gpt-4.1-nano, 2025-04-14 |
gpt-4.1-mini, 2025-04-14 |
computer-use-preview, 2025-03-11 |
o3-mini, 2025-01-31 |
o1, 2024-12-17 |
gpt-4o, 2024-05-13 |
gpt-4o, 2024-08-06 |
gpt-4o, 2024-11-20 |
gpt-4o-mini, 2024-07-18 |
text-embedding-3-small, 1 |
text-embedding-3-large, 1 |
text-embedding-ada-002, 2 |
gpt-4o-realtime-preview, 2024-12-17 |
gpt-4o-audio-preview, 2024-12-17 |
gpt-4o-mini-realtime-preview, 2024-12-17 |
gpt-4o-mini-audio-preview, 2024-12-17 |
gpt-4o-transcribe, 2025-03-20 |
gpt-4o-mini-tts, 2025-12-15 |
gpt-4o-mini-tts, 2025-03-20 |
gpt-4o-mini-transcribe, 2025-12-15 |
gpt-4o-mini-transcribe, 2025-03-20 |
gpt-image-1-mini, 2025-10-06 |
gpt-audio-mini, 2025-10-06 |
gpt-audio-mini, 2025-12-15 |
gpt-image-1.5, 2025-12-16 |
sora-2, 2025-10-06 |
gpt-realtime-mini, 2025-10-06 |
gpt-realtime-mini, 2025-12-15 |
o3-deep-research, 2025-06-26 |
gpt-realtime, 2025-08-28 |
gpt-audio, 2025-08-28 |
gpt-4o-transcribe-diarize, 2025-10-15 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| australiaeast | - | - | - | - | ✅ | ✅ | ✅ | ✅ | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| brazilsouth | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| canadacentral | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | ✅ | - | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| canadaeast | - | - | - | - | ✅ | ✅ | ✅ | ✅ | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| centralus | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | - | - | ✅ | ✅ | - | ✅ | ✅ | - |
| eastus | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| eastus2 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ |
| francecentral | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| germanywestcentral | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| italynorth | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| japaneast | - | - | - | - | ✅ | ✅ | ✅ | ✅ | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| koreacentral | - | - | - | - | ✅ | ✅ | ✅ | ✅ | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| northcentralus | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| norwayeast | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | ✅ | - | - | - |
| polandcentral | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | ✅ | - | - | ✅ | - | - | - | - | - | - | - |
| southafricanorth | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| southcentralus | - | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| southeastasia | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | - | - | - | ✅ | - | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| southindia | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| spaincentral | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| swedencentral | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | - | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ |
| switzerlandnorth | - | - | - | - | ✅ | ✅ | ✅ | ✅ | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| switzerlandwest | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | ✅ | - | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| uaenorth | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | ✅ | - | - | ✅ | - | - | - | - | - | - | - |
| uksouth | - | - | - | - | ✅ | ✅ | ✅ | ✅ | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| westeurope | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| westus | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | - | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | ✅ | - | - | - |
| westus3 | - | - | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | - | - | - | - | - | - | - | - | ✅ | - | - | ✅ | - | - | - | - | - | - | - |

Note

`o3-deep-research`

is currently only available with Foundry Agent Service. To learn more, see the [Deep Research tool guidance](/en-us/azure/ai-foundry/agents/how-to/tools/deep-research).

This table doesn't include fine-tuning regional availability information. Consult the [fine-tuning section](#fine-tuning-models) for this information.

### Embeddings models

These models can be used only with Embedding API requests.

Note

`text-embedding-3-large`

is the latest and most capable embedding model. You can't upgrade between embedding models. To migrate from using `text-embedding-ada-002`

to `text-embedding-3-large`

, you need to generate new embeddings.

| Model ID | Max request (tokens) | Output dimensions | Training data (up to) |
|---|---|---|---|
`text-embedding-ada-002` (version 2) |
8,192 | 1,536 | Sep 2021 |
`text-embedding-ada-002` (version 1) |
2,046 | 1,536 | Sep 2021 |
`text-embedding-3-large` |
8,192 | 3,072 | Sep 2021 |
`text-embedding-3-small` |
8,192 | 1,536 | Sep 2021 |

Note

When you send an array of inputs for embedding, the maximum number of input items in the array per call to the embedding endpoint is 2,048.

### Image generation models

| Model ID | Max request (characters) |
|---|---|
`gpt-image-1` |
4,000 |
`gpt-image-1-mini` |
4,000 |
`gpt-image-1.5` |
4,000 |
`dall-e-3` |
4,000 |

### Video generation models

| Model ID | Max Request (characters) |
|---|---|
| sora | 4,000 |

## Fine-tuning models

Note

The supported regions for fine-tuning might vary if you use Azure OpenAI models in a Microsoft Foundry project versus outside a project.

| Model ID | Standard regions | Global | Developer | Max request (tokens) | Training data (up to) | Modality |
|---|---|---|---|---|---|---|
`gpt-4o-mini` (2024-07-18) |
North Central US Sweden Central |
✅ | ✅ | Input: 128,000 Output: 16,384 Training example context length: 65,536 |
Oct 2023 | Text to text |
`gpt-4o` (2024-08-06) |
East US2 North Central US Sweden Central |
✅ | ✅ | Input: 128,000 Output: 16,384 Training example context length: 65,536 |
Oct 2023 | Text and vision to text |
`gpt-4.1` (2025-04-14) |
North Central US Sweden Central |
✅ | ✅ | Input: 128,000 Output: 16,384 Training example context length: 65,536 |
May 2024 | Text and vision to text |
`gpt-4.1-mini` (2025-04-14) |
North Central US Sweden Central |
✅ | ✅ | Input: 128,000 Output: 16,384 Training example context length: 65,536 |
May 2024 | Text to text |
`gpt-4.1-nano` (2025-04-14) |
North Central US Sweden Central |
✅ | ✅ | Input: 128,000 Output: 16,384 Training example context length: 32,768 |
May 2024 | Text to text |
`o4-mini` (2025-04-16) |
East US2 Sweden Central |
✅ | ❌ | Input: 128,000 Output: 16,384 Training example context length: 65,536 |
May 2024 | Text to text |
`Ministral-3B` (preview) (2411) |
Not supported | ✅ | ❌ | Input: 128,000 Output: Unknown Training example context length: Unknown |
Unknown | Text to text |
`Qwen-32B` (preview) |
Not supported | ✅ | ❌ | Input: 8,000 Output: 32,000 Training example context length: 8192 |
July 2024 | Text to text |

Note

Global training provides [more affordable](https://aka.ms/aoai-pricing) training per token, but doesn't offer [data residency](https://aka.ms/data-residency). It's currently available to Foundry resources in the following regions:

- Australia East
- Brazil South
- Canada Central
- Canada East
- East US
- East US2
- France Central
- Germany West Central
- Italy North
- Japan East
*(no vision support)* - Korea Central
- North Central US
- Norway East
- Poland Central
*(no 4.1-nano support)* - Southeast Asia
- South Africa North
- South Central US
- South India
- Spain Central
- Sweden Central
- Switzerland West
- Switzerland North
- UK South
- West Europe
- West US
- West US3

## Assistants (preview)

For Assistants, you need a combination of a supported model and a supported region. Certain tools and capabilities require the latest models. The following models are available in the Assistants API, SDK, and Foundry. The following table is for standard deployment. For information on provisioned throughput unit availability, see [Provisioned throughput](../../openai/concepts/provisioned-throughput?view=foundry-classic). The listed models and regions can be used with both Assistants v1 and v2. You can use [Global Standard models](#global-standard-model-availability) if they're supported in the following regions.

| Region | gpt-4o, 2024-05-13 | gpt-4o, 2024-08-06 | gpt-4o-mini, 2024-07-18 | gpt-4, 0613 | gpt-4, 1106-Preview | gpt-4, 0125-Preview | gpt-4, turbo-2024-04-09 | gpt-4-32k, 0613 | gpt-35-turbo, 0613 | gpt-35-turbo, 1106 | gpt-35-turbo, 0125 | gpt-35-turbo-16k, 0613 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| australiaeast | - | - | - | ✅ | ✅ | - | - | ✅ | ✅ | ✅ | ✅ | ✅ |
| eastus | ✅ | ✅ | ✅ | - | - | ✅ | ✅ | - | ✅ | - | ✅ | ✅ |
| eastus2 | ✅ | ✅ | ✅ | - | ✅ | - | ✅ | - | ✅ | - | ✅ | ✅ |
| francecentral | - | - | - | ✅ | ✅ | - | - | ✅ | ✅ | ✅ | - | ✅ |
| japaneast | - | - | - | - | - | - | - | - | ✅ | - | ✅ | ✅ |
| norwayeast | - | - | - | - | ✅ | - | - | - | - | - | - | - |
| southindia | - | - | - | - | ✅ | - | - | - | - | ✅ | ✅ | - |
| swedencentral | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | ✅ | ✅ | ✅ | - | ✅ |
| uksouth | - | - | - | - | ✅ | ✅ | - | - | ✅ | ✅ | ✅ | ✅ |
| westus | ✅ | ✅ | ✅ | - | ✅ | - | ✅ | - | - | ✅ | ✅ | - |
| westus3 | ✅ | ✅ | ✅ | - | ✅ | - | ✅ | - | - | - | ✅ | - |

## Model retirement

For the latest information on model retirements, refer to the [model retirement guide](../../openai/concepts/model-retirements?view=foundry-classic).

## Related content

Note

Foundry Models sold directly by Azure also include all Azure OpenAI models. To learn about these models, switch to the [Azure OpenAI models](models-sold-directly-by-azure?view=foundry-classic&pivots=azure-openai) collection at the top of this article.

## Black Forest Labs models sold directly by Azure

The Black Forest Labs (BFL) collection of image generation models includes FLUX.2 [pro] for image generation and editing through both text and image prompts, FLUX.1 Kontext [pro] for in-context generation and editing, and FLUX1.1 [pro] for text-to-image generation.

You can run these models through the BFL service provider API and through the [images/generations and images/edits endpoints](../../openai/reference-preview?view=foundry-classic).

Note

See the [GitHub sample for image generation with FLUX models in Microsoft Foundry](https://github.com/microsoft-foundry/foundry-samples/blob/main/samples/python/black-forest-labs/flux/README.md) and its associated [notebook](https://github.com/microsoft-foundry/foundry-samples/blob/main/samples/python/black-forest-labs/flux/AIFoundry_ImageGeneration_FLUX.ipynb) that showcases how to create high-quality images from textual prompts.

| Model | Type & API endpoint | Capabilities | Deployment type (region availability) | Project type |
|---|---|---|---|---|
|

**Image generation**-

[BFL service provider API](https://docs.bfl.ai/flux_2/flux2_text_to_image):`<resource-name>/providers/blackforestlabs/v1/flux-2-pro`

**Input:**text and image (32,000 tokens and up to 8 imagesi)-

**Output:**One Image-

**Tool calling:**No-

**Response formats:**Image (PNG and JPG)-

**Key features:**Multi-reference support for up to 8 imagesii; more grounded in real-world knowledge; greater output flexibility; enhanced performance-

**Additional parameters:***(In provider-specific API only)*Supports all parameters.[FLUX.1-Kontext-pro](https://ai.azure.com/explore/models/FLUX.1-Kontext-pro/version/1/registry/azureml-blackforestlabs/?cid=learnDocs)**Image generation**-

[Image API](../../openai/reference-preview?view=foundry-classic):`https://<resource-name>/openai/deployments/{deployment-id}/images/generations`

and

`https://<resource-name>/openai/deployments/{deployment-id}/images/edits`

-

[BFL service provider API](https://docs.bfl.ai/kontext/kontext_text_to_image):`<resource-name>/providers/blackforestlabs/v1/flux-kontext-pro?api-version=preview`

**Input:**text and image (5,000 tokens and 1 image)-

**Output:**One Image-

**Tool calling:**No-

**Response formats**: Image (PNG and JPG)-

**Key features:**Character consistency, advanced editing-

**Additional parameters:***(In provider-specific API only)*`seed`

, `aspect ratio`

, `input_image`

, `prompt_unsampling`

, `safety_tolerance`

, `output_format`

[FLUX-1.1-pro](https://ai.azure.com/explore/models/FLUX-1.1-pro/version/1/registry/azureml-blackforestlabs/?cid=learnDocs)**Image generation**-

[Image API](../../openai/reference-preview?view=foundry-classic):`https://<resource-name>/openai/deployments/{deployment-id}/images/generations`

-

[BFL service provider API](https://docs.bfl.ai/flux_models/flux_1_1_pro):`<resource-name>/providers/blackforestlabs/v1/flux-pro-1.1?api-version=preview`

**Input:**text (5,000 tokens and 1 image)-

**Output:**One Image-

**Tool calling:**No-

**Response formats:**Image (PNG and JPG)-

**Key features:**Fast inference speed, strong prompt adherence, competitive pricing, scalable generation-

**Additional parameters:***(In provider-specific API only)*`width`

, `height`

, `prompt_unsampling`

, `seed`

, `safety_tolerance`

, `output_format`

| Model | Type & API endpoint | Capabilities | Deployment type (region availability) |
|---|---|---|---|
`FLUX.2-pro` |
Image generation -
`<resource-name>/providers/blackforestlabs/v1/flux-2-pro` |
- Input: text (32,000 tokens and up to 8 imagesi) - Output: One Image - Tool calling: No - Response formats: Image (PNG and JPG) - Key features: Multi-reference support for up to 8 imagesii; more grounded in real-world knowledge; greater output flexibility; enhanced performance - Additional parameters: (In provider-specific API only) Supports all parameters. |
- Global standard (all regions) |
`FLUX.1-Kontext-pro` |
Image generation -
`https://<resource-name>/openai/deployments/{deployment-id}/images/generations` and `https://<resource-name>/openai/deployments/{deployment-id}/images/edits` -
`<resource-name>/providers/blackforestlabs/v1/flux-kontext-pro?api-version=preview` |
- Input: text and image (5,000 tokens and 1 image) - Output: One Image - Tool calling: No - Response formats: Image (PNG and JPG) - Key features: Character consistency, advanced editing - Additional parameters: (In provider-specific API only) `seed` , `aspect ratio` , `input_image` , `prompt_unsampling` , `safety_tolerance` , `output_format` |
- Global standard (all regions) |
`FLUX-1.1-pro` |
Image generation -
`https://<resource-name>/openai/deployments/{deployment-id}/images/generations` -
`<resource-name>/providers/blackforestlabs/v1/flux-pro-1.1?api-version=preview` |
- Input: text (5,000 tokens and 1 image) - Output: One Image - Tool calling: No - Response formats: Image (PNG and JPG) - Key features: Fast inference speed, strong prompt adherence, competitive pricing, scalable generation - Additional parameters: (In provider-specific API only) `width` , `height` , `prompt_unsampling` , `seed` , `safety_tolerance` , `output_format` |
- Global standard (all regions) |

i,ii Support for **multiple reference images (up to eight)** is available for FLUX.2[pro] by using the API, but *not* in the playground. See the following [Code samples for FLUX.2[pro]](#code-samples-for-flux2pro).

#### Code samples for FLUX.2[pro]

**Image generation**

- Input: Text
- Output: One image

```
curl -X POST https://<your-resource-name>.api.cognitive.microsoft.com/providers/blackforestlabs/v1/flux-2-pro?api-version… \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {API_KEY}" \
-d '{
"model": "FLUX.2-pro"
"prompt": "A photograph of a red fox in an autumn forest",
"width": 1024,
"height": 1024,
"seed": 42,
"safety_tolerance": 2,
"output_format": "jpeg",
}'
```


**Image editing**

- Input: Up to eight bit-64 encoded images
- Output: One image

```
curl -X POST https://<your-resource-name>.api.cognitive.microsoft.com/providers/blackforestlabs/v1/flux-2-pro?api-version… \
-H "Content-Type: application/json" \
-H "Authorization: Bearer {API_KEY}" \
-d '{
"model": "FLUX.2-pro",
"prompt": "Apply a cinematic, moody lighting effect to all photos. Make them look like scenes from a sci-fi noir film",
"output_format": "jpeg",
"input_image" : "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDA.......",
"input_image_2" : "iVBORw0KGgoAAAANSUhEUgAABAAAAAQACAIAAADwf........"
}'
```


See [this model collection in Microsoft Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=black+forest+labs/?cid=learnDocs).

## Cohere models sold directly by Azure

The Cohere family of models includes various models optimized for different use cases, including chat completions, rerank/text classification, and embeddings. Cohere models are optimized for various use cases that include reasoning, summarization, and question answering.

| Model | Type | Capabilities | Deployment type (region availability) | Project type |
|---|---|---|---|---|
|

**Input:**text-

**Output:**text-

**Languages:**`en`

, `fr`

, `es`

, `it`

, `de`

, `pt-br`

, `ja`

, `zh-cn`

, `ar`

, `vi`

, `hi`

, `ru`

, `id`

, and `nl`

-

**Tool calling:**No-

**Response formats:**JSON-

[Managed compute](../../how-to/deploy-models-managed-pay-go?view=foundry-classic#cohere)[Cohere-rerank-v4.0-fast](https://ai.azure.com/resource/models/Cohere-rerank-v4.0-fast/version/2/registry/azureml-cohere/?cid=learnDocs)**Input:**text-

**Output:**text-

**Languages:**`en`

, `fr`

, `es`

, `it`

, `de`

, `pt-br`

, `ja`

, `zh-cn`

, `ar`

, `vi`

, `hi`

, `ru`

, `id`

, and `nl`

-

**Tool calling:**No-

**Response formats:**JSON-

[Managed compute](../../how-to/deploy-models-managed-pay-go?view=foundry-classic#cohere)[Cohere-command-a](https://ai.azure.com/explore/models/Cohere-command-a/version/1/registry/azureml-cohere/?cid=learnDocs)**Input:**text (131,072 tokens)-

**Output:**text (8,182 tokens)-

**Languages:**`en`

, `fr`

, `es`

, `it`

, `de`

, `pt-br`

, `ja`

, `ko`

, `zh-cn`

, and `ar`

-

**Tool calling:**Yes-

**Response formats:**Text, JSON[embed-v-4-0](https://ai.azure.com/explore/models/embed-v-4-0/version/4/registry/azureml-cohere/?cid=learnDocs)**Input:**text (512 tokens) and images (2MM pixels)-

**Output:**Vector (256, 512, 1024, 1536 dim.)-

**Languages:**`en`

, `fr`

, `es`

, `it`

, `de`

, `pt-br`

, `ja`

, `ko`

, `zh-cn`

, and `ar`

| Model | Type | Capabilities | Deployment type (region availability) |
|---|---|---|---|
|

**Input:**text-

**Output:**text-

**Languages:**`en`

, `fr`

, `es`

, `it`

, `de`

, `pt-br`

, `ja`

, `zh-cn`

, `ar`

, `vi`

, `hi`

, `ru`

, `id`

, and `nl`

-

**Tool calling:**No-

**Response formats:**JSON- Managed compute

[Cohere-rerank-v4.0-fast](https://ai.azure.com/resource/models/Cohere-rerank-v4.0-fast/version/2/registry/azureml-cohere/?cid=learnDocs)**Input:**text-

**Output:**text-

**Languages:**`en`

, `fr`

, `es`

, `it`

, `de`

, `pt-br`

, `ja`

, `zh-cn`

, `ar`

, `vi`

, `hi`

, `ru`

, `id`

, and `nl`

-

**Tool calling:**No-

**Response formats:**JSON- Managed compute

`Cohere-command-a`

**Input:**text (131,072 tokens)-

**Output:**text (8,182 tokens)-

**Languages:**`en`

, `fr`

, `es`

, `it`

, `de`

, `pt-br`

, `ja`

, `ko`

, `zh-cn`

, and `ar`

-

**Tool calling:**Yes-

**Response formats:**Text, JSON`embed-v-4-0`

**Input:**text (512 tokens) and images (2MM pixels)-

**Output:**Vector (256, 512, 1024, 1536 dim.)-

**Languages:**`en`

, `fr`

, `es`

, `it`

, `de`

, `pt-br`

, `ja`

, `ko`

, `zh-cn`

, and `ar`

See [the Cohere model collection in the Foundry portal](https://ai.azure.com/explore/models?selectedCollection=Cohere/?cid=learnDocs,cohere).

## DeepSeek models sold directly by Azure

The DeepSeek family of models includes several reasoning models, which excel at reasoning tasks by using a step-by-step training process, such as language, scientific reasoning, and coding tasks.

| Model | Type | Capabilities | Deployment type (region availability) | Project type |
|---|---|---|---|---|
|

[(with reasoning content)](../how-to/use-chat-reasoning?view=foundry-classic)**Input:**text (128,000 tokens)-

**Output:**(128,000 tokens)-

**Languages:**`en`

and `zh`

-

**Tool calling:**No-

**Response formats:**Text, JSON[DeepSeek-V3.2](https://ai.azure.com/resource/models/DeepSeek-V3.2/version/1/registry/azureml-deepseek?cid=learnDocs)[(with reasoning content)](../how-to/use-chat-reasoning?view=foundry-classic)**Input:**text (128,000 tokens)-

**Output:**(128,000 tokens)-

**Languages:**`en`

and `zh`

-

**Tool calling:**No-

**Response formats:**Text, JSON[DeepSeek-V3.1](https://ai.azure.com/resource/models/DeepSeek-V3.1/version/1/registry/azureml-deepseek?cid=learnDocs)[(with reasoning content)](../how-to/use-chat-reasoning?view=foundry-classic)**Input:**text (131,072 tokens)-

**Output:**(131,072 tokens)-

**Languages:**`en`

and `zh`

-

**Tool calling:**Yes-

**Response formats:**Text, JSON[DeepSeek-R1-0528](https://ai.azure.com/explore/models/deepseek-r1-0528/version/1/registry/azureml-deepseek?cid=learnDocs)[(with reasoning content)](../how-to/use-chat-reasoning?view=foundry-classic)**Input:**text (163,840 tokens)-

**Output:**(163,840 tokens)-

**Languages:**`en`

and `zh`

-

**Tool calling:**No-

**Response formats:**Text.- Global provisioned (all regions)

[DeepSeek-V3-0324](https://ai.azure.com/explore/models/deepseek-v3-0324/version/1/registry/azureml-deepseek?cid=learnDocs)**Input:**text (131,072 tokens)-

**Output:**(131,072 tokens)-

**Languages:**`en`

and `zh`

-

**Tool calling:**Yes-

**Response formats:**Text, JSON- Global provisioned (all regions)

[DeepSeek-R1](https://ai.azure.com/explore/models/deepseek-r1/version/1/registry/azureml-deepseek?cid=learnDocs)[(with reasoning content)](../how-to/use-chat-reasoning?view=foundry-classic)**Input:**text (163,840 tokens)-

**Output:**(163,840 tokens)-

**Languages:**`en`

and `zh`

-

**Tool calling:**No-

**Response formats:**Text.- Global provisioned (all regions)

| Model | Type | Capabilities | Deployment type (region availability) |
|---|---|---|---|
`DeepSeek-V3.2-Speciale` |
chat-completion
|
- Input: text (128,000 tokens) - Output: (128,000 tokens) - Languages: `en` and `zh` - Tool calling: No - Response formats: Text, JSON |
- Global standard (all regions) |
`DeepSeek-V3.2` |
chat-completion
|
- Input: text (128,000 tokens) - Output: (128,000 tokens) - Languages: `en` and `zh` - Tool calling: No - Response formats: Text, JSON |
- Global standard (all regions) |
`DeepSeek-V3.1` |
chat-completion
|
- Input: text (131,072 tokens) - Output: (131,072 tokens) - Languages: `en` and `zh` - Tool calling: Yes - Response formats: Text, JSON |
- Global standard (all regions) |
`DeepSeek-R1-0528` |
chat-completion
|
- Input: text (163,840 tokens) - Output: (163,840 tokens) - Languages: `en` and `zh` - Tool calling: No - Response formats: Text. |
- Global standard (all regions) - Global provisioned (all regions) |
`DeepSeek-V3-0324` |
chat-completion | - Input: text (131,072 tokens) - Output: (131,072 tokens) - Languages: `en` and `zh` - Tool calling: Yes - Response formats: Text, JSON |
- Global standard (all regions) - Global provisioned (all regions) |
`DeepSeek-R1` |
chat-completion
|
- Input: text (163,840 tokens) - Output: (163,840 tokens) - Languages: `en` and `zh` - Tool calling: No - Response formats: Text. |
- Global standard (all regions) - Global provisioned (all regions) |

See [this model collection in the Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=DeepSeek/?cid=learnDocs).

## Meta models sold directly by Azure

Meta Llama models and tools are a collection of pretrained and fine-tuned generative AI text and image reasoning models. Meta models range in scale to include:

- Small language models (SLMs) like 1B and 3B Base and Instruct models for on-device and edge inferencing
- Mid-size large language models (LLMs) like 7B, 8B, and 70B Base and Instruct models
- High-performance models like Meta Llama 3.1-405B Instruct for synthetic data generation and distillation use cases.

| Model | Type | Capabilities | Deployment type (region availability) | Project type |
|---|---|---|---|---|
|

**Input:**text and images (1M tokens)-

**Output:**text (1M tokens)-

**Languages:**`ar`

, `en`

, `fr`

, `de`

, `hi`

, `id`

, `it`

, `pt`

, `es`

, `tl`

, `th`

, and `vi`

-

**Tool calling:**No-

**Response formats:**Text[Llama-3.3-70B-Instruct](https://ai.azure.com/explore/models/Llama-3.3-70B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)**Input:**text (128,000 tokens)-

**Output:**text (8,192 tokens)-

**Languages:**`en`

, `de`

, `fr`

, `it`

, `pt`

, `hi`

, `es`

, and `th`

-

**Tool calling:**No-

**Response formats:**Text| Model | Type | Capabilities | Deployment type (region availability) |
|---|---|---|---|
`Llama-4-Maverick-17B-128E-Instruct-FP8` |
chat-completion | - Input: text and images (1M tokens) - Output: text (1M tokens) - Languages: `ar` , `en` , `fr` , `de` , `hi` , `id` , `it` , `pt` , `es` , `tl` , `th` , and `vi` - Tool calling: No - Response formats: Text |
- Global standard (all regions) |
`Llama-3.3-70B-Instruct` |
chat-completion | - Input: text (128,000 tokens) - Output: text (8,192 tokens) - Languages: `en` , `de` , `fr` , `it` , `pt` , `hi` , `es` , and `th` - Tool calling: No - Response formats: Text |
- Global standard (all regions) |

See [this model collection in the Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Meta/?cid=learnDocs). You can also find several Meta models available [from partners and community](models-from-partners?view=foundry-classic#meta).

## Microsoft models sold directly by Azure

Microsoft models include various model groups such as Model Router, MAI models, Phi models, healthcare AI models, and more. See [the Microsoft model collection in the Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Microsoft/?cid=learnDocs). You can also find several Microsoft models available [from partners and community](models-from-partners?view=foundry-classic#microsoft).

| Model | Type | Capabilities | Deployment type (region availability) | Project type |
|---|---|---|---|---|
1 |

[Model router overview](/en-us/azure/ai-foundry/openai/how-to/model-router).-

**Input:**text, image-

**Output:**text (max output tokens varies2)**Context window:**200,0003-

**Languages:**`en`

- Data Zone standard

4(East US 2, Sweden Central)[MAI-DS-R1](https://ai.azure.com/explore/models/MAI-DS-R1/version/1/registry/azureml/?cid=learnDocs)[(with reasoning content)](../how-to/use-chat-reasoning?view=foundry-classic)**Input:**text (163,840 tokens)-

**Output:**(163,840 tokens)-

**Languages:**`en`

and `zh`

-

**Tool calling:**No-

**Response formats:**Text.| Model | Type | Capabilities | Deployment type (region availability) |
|---|---|---|---|
1 |

[Model router overview](/en-us/azure/ai-foundry/openai/how-to/model-router).-

**Input:**text, image-

**Output:**text (max output tokens varies2)**Context window:**200,0003-

**Languages:**`en`

- Data Zone standard

4(East US 2, Sweden Central)`MAI-DS-R1`

[(with reasoning content)](../how-to/use-chat-reasoning?view=foundry-classic)**Input:**text (163,840 tokens)-

**Output:**(163,840 tokens)-

**Languages:**`en`

and `zh`

-

**Tool calling:**No-

**Response formats:**Text.1 **Model router version** `2025-11-18`

. Earlier versions (`2025-08-07`

and `2025-05-19`

) are also available.

2 **Max output tokens** varies for underlying models in the model router. For example, 32,768 (`GPT-4.1 series`

), 100,000 (`o4-mini`

), 128,000 (`gpt-5 reasoning models`

), and 16,384 (`gpt-5-chat`

).

3 Larger **context windows** are compatible with *some* of the underlying models of the Model Router. That means an API call with a larger context succeeds only if the prompt gets routed to one of such models. Otherwise, the call fails.

4 Billing for **Data Zone Standard** model router deployments begins no earlier than November 1, 2025.

## Mistral models sold directly by Azure

| Model | Type | Capabilities | Deployment type (region availability) | Project type |
|---|---|---|---|---|
|

**Input:**text, image-

**Output:**text-

**Languages:**`en`

, `fr`

, `de`

, `es`

, `it`

, `pt`

, `nl`

, `zh`

, `ja`

, `ko`

, and `ar`

-

**Tool calling:**Yes-

**Response formats:**Text, JSON[mistral-document-ai-2505](https://ai.azure.com/explore/models/mistral-document-ai-2505/version/1/registry/azureml-mistral/?cid=learnDocs)**Input:**image or PDF pages (30 pages, max 30MB PDF file)-

**Output:**text-

**Languages:**`en`

-

**Tool calling:**no-

**Response formats:**Text, JSON, Markdown- Data zone standard (US and EU)

| Model | Type | Capabilities | Deployment type (region availability) |
|---|---|---|---|
`Mistral-Large-3` |
chat-completion | - Input: text, image - Output: text - Languages: `en` , `fr` , `de` , `es` , `it` , `pt` , `nl` , `zh` , `ja` , `ko` , and `ar` - Tool calling: Yes - Response formats: Text, JSON |
- Global standard (West US 3) |
`mistral-document-ai-2505` |
Image-to-Text | - Input: image or PDF pages (30 pages, max 30MB PDF file) - Output: text - Languages: `en` - Tool calling: no - Response formats: Text, JSON, Markdown |
- Global standard (all regions) - Data zone standard (US and EU) |

See [the Mistral model collection in the Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Mistral+AI/?cid=learnDocs). You can also find several Mistral models available [from partners and community](models-from-partners?view=foundry-classic#mistral-ai).

## Moonshot AI models sold directly by Azure

Moonshot AI models include Kimi K2 Thinking, the latest, most capable version of open-source thinking model. Kimi K2 was built as a thinking agent that reasons step-by-step while dynamically invoking tools. It sets a new state-of-the-art on Humanity's Last Exam (HLE), BrowseComp, and other benchmarks by dramatically scaling multi-step reasoning depth and maintaining stable tool-use across 200–300 sequential calls.

Key capabilities of Kimi K2 Thinking include:

**Deep Thinking & Tool Orchestration:**End-to-end trained to interleave chain-of-thought reasoning with function calls, enabling autonomous research, coding, and writing workflows that last hundreds of steps without drift.**Native INT4 Quantization:**Quantization-Aware Training (QAT) is employed in post-training stage to achieve lossless 2x speed-up in low-latency mode.**Stable Long-Horizon Agency:**Maintains coherent goal-directed behavior across up to 200–300 consecutive tool invocations, surpassing prior models that degrade after 30–50 steps.

| Model | Type | Capabilities | Deployment type (region availability) | Project type |
|---|---|---|---|---|
|

[(with reasoning content)](../how-to/use-chat-reasoning?view=foundry-classic)**Input:**text (262,144 tokens)-

**Output:**text (262,144 tokens)-

**Languages:**`en`

and `zh`

-

**Tool calling:**Yes-

**Response formats:**Text| Model | Type | Capabilities | Deployment type (region availability) |
|---|---|---|---|
`Kimi-K2-Thinking` |
chat-completion
|
- Input: text (262,144 tokens) - Output: text (262,144 tokens) - Languages: `en` and `zh` - Tool calling: Yes - Response formats: Text |
- Global standard (all regions) |

See [this model collection in the Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Moonshot+ai/?cid=learnDocs).

## xAI models sold directly by Azure

xAI's Grok models in Foundry Models include a diverse set of models designed to excel in various enterprise domains with different capabilities and price points, including:

Grok 3, a non-reasoning model pretrained by the Colossus datacenter, is tailored for business use cases such as data extraction, coding, and text summarization, with exceptional instruction-following capabilities. It supports a 131,072 token context window, allowing it to handle extensive inputs while maintaining coherence and depth, and is adept at drawing connections across domains and languages.

Grok 3 Mini is a lightweight reasoning model trained to tackle agentic, coding, mathematical, and deep science problems with test-time compute. It also supports a 131,072 token context window for understanding codebases and enterprise documents, and excels at using tools to solve complex logical problems in novel environments, offering raw reasoning traces for user inspection with adjustable thinking budgets.

Grok Code Fast 1, a fast and efficient reasoning model designed for use in agentic coding applications. It was pretrained on a coding-focused data mixture, then post-trained on demonstrations of various coding tasks and tool use as well as demonstrations of correct refusal behaviors based on xAI's safety policy.

[Registration is required for access to the grok-code-fast-1 model](https://aka.ms/xai/grok-code-fast-1).Grok 4 Fast, an efficiency-optimized language model that delivers near-Grok 4 reasoning capabilities with significantly lower latency and cost, and can bypass reasoning entirely for ultra-fast applications. It is trained for safe and effective tool use, with built-in refusal behaviors, a fixed safety-enforcing system prompt, and input filters to prevent misuse.

Grok 4 is the latest reasoning model from xAI with advanced reasoning and tool-use capabilities, enabling it to achieve new state-of-the-art performance across challenging academic and industry benchmarks.

[Registration is required for access to the grok-4 model](https://aka.ms/xai/grok-4). Unlike Grok 4 Fast (reasoning and non-reasoning) models,**Grok 4 doesn't support image input**.

| Model | Type | Capabilities | Deployment type (region availability) | Project type |
|---|---|---|---|---|
|

**Input:**text (256,000 tokens)-

**Output:**text (8,192 tokens)-

**Languages:**`en`

-

**Tool calling:**yes-

**Response formats:**text[grok-4-fast-reasoning](https://ai.azure.com/explore/models/grok-4-fast-reasoning/version/1/registry/azureml-xai/?cid=learnDocs)**Input:**text, image (2,000,000 tokens)-

**Output:**text (2,000,000 tokens)-

**Languages:**`en`

-

**Tool calling:**yes-

**Response formats:**text- Data zone standard (US)

[grok-4-fast-non-reasoning](https://ai.azure.com/explore/models/grok-4-fast-non-reasoning/version/1/registry/azureml-xai/?cid=learnDocs)**Input:**text, image (2,000,000 tokens)-

**Output:**text (2,000,000 tokens)-

**Languages:**`en`

-

**Tool calling:**yes-

**Response formats:**text- Data zone standard (US)

[grok-code-fast-1](https://ai.azure.com/explore/models/grok-code-fast-1/version/1/registry/azureml-xa/?cid=learnDocs)**Input:**text (256,000 tokens)-

**Output:**text (8,192 tokens)-

**Languages:**`en`

-

**Tool calling:**yes-

**Response formats:**text[grok-3](https://ai.azure.com/explore/models/grok-3/version/1/registry/azureml-xai/?cid=learnDocs)**Input:**text (131,072 tokens)-

**Output:**text (131,072 tokens)-

**Languages:**`en`

-

**Tool calling:**yes-

**Response formats:**text- Data zone standard (US)

[grok-3-mini](https://ai.azure.com/explore/models/grok-3-mini/version/1/registry/azureml-xai/?cid=learnDocs)**Input:**text (131,072 tokens)-

**Output:**text (131,072 tokens)-

**Languages:**`en`

-

**Tool calling:**yes-

**Response formats:**text- Data zone standard (US)

| Model | Type | Capabilities | Deployment type (region availability) |
|---|---|---|---|
`grok-4` |
chat-completion | - Input: text, image (256,000 tokens) - Output: text (8,192 tokens) - Languages: `en` - Tool calling: yes - Response formats: text |
- Global standard (all regions) |
`grok-4-fast-reasoning` |
chat-completion | - Input: text, image (2,000,000 tokens) - Output: text (2,000,000 tokens) - Languages: `en` - Tool calling: yes - Response formats: text |
- Global standard (all regions) - Data zone standard (US) |
`grok-4-fast-non-reasoning` |
chat-completion | - Input: text, image (2,000,000 tokens) - Output: text (2,000,000 tokens) - Languages: `en` - Tool calling: yes - Response formats: text |
- Global standard (all regions) - Data zone standard (US) |
`grok-code-fast-1` |
chat-completion | - Input: text (256,000 tokens) - Output: text (8,192 tokens) - Languages: `en` - Tool calling: yes - Response formats: text |
- Global standard (all regions) |
`grok-3` |
chat-completion | - Input: text (131,072 tokens) - Output: text (131,072 tokens) - Languages: `en` - Tool calling: yes - Response formats: text |
- Global standard (all regions) - Data zone standard (US) |
`grok-3-mini` |
chat-completion | - Input: text (131,072 tokens) - Output: text (131,072 tokens) - Languages: `en` - Tool calling: yes - Response formats: text |
- Global standard (all regions) - Data zone standard (US) |

See [the xAI model collection in the Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=xAI/?cid=learnDocs).

## Model region availability by deployment type

Foundry Models gives you choices for the hosting structure that fits your business and usage patterns. The service offers two main types of deployment:

**Standard**: Has a global deployment option, routing traffic globally to provide higher throughput.**Provisioned**: Also has a global deployment option, allowing you to purchase and deploy provisioned throughput units across Azure global infrastructure.

All deployments perform the same inference operations, but the billing, scale, and performance differ. For more information about deployment types, see [Deployment types in Foundry Models](deployment-types?view=foundry-classic).

### Global Standard model availability

Region |
DeepSeek-R1-0528 |
DeepSeek-R1 |
DeepSeek-V3-0324 |
DeepSeek-V3.1 |
FLUX.1-Kontext-pro |
FLUX-1.1-pro |
grok-4 |
grok-4-fast-reasoning |
grok-4-fast-non-reasoning |
grok-code-fast-1 |
grok-3 |
grok-3-mini |
Llama-4-Maverick-17B-128E-Instruct-FP8 |
Llama-3.3-70B-Instruct |
MAI-DS-R1 |
mistral-document-ai-2505 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| australiaeast | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| brazilsouth | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| canadaeast | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| eastus | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| eastus2 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| francecentral | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| germanywestcentral | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| italynorth | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| japaneast | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| koreacentral | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| northcentralus | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| norwayeast | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| polandcentral | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| southafricanorth | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| southcentralus | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| southindia | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| spaincentral | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| swedencentral | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| switzerlandnorth | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| switzerlandwest | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| uaenorth | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| uksouth | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| westeurope | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| westus | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| westus3 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

## Open and custom models

The model catalog offers a larger selection of models from a wider range of providers. For these models, you can't use the option for [standard deployment in Microsoft Foundry resources](../../concepts/deployments-overview?view=foundry-classic#standard-deployment-in-foundry-resources), where models are provided as APIs. Instead, to deploy these models, you might need to host them on your infrastructure, create an AI hub, and provide the underlying compute quota to host the models.

Furthermore, these models can be open-access or IP protected. In both cases, you have to deploy them in managed compute offerings in Foundry. To get started, see [How-to: Deploy to Managed compute](../../how-to/deploy-models-managed?view=foundry-classic).
