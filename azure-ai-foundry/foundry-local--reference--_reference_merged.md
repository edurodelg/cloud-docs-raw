---
merged_at: 2026-01-26T23:20:36.849561
merged_files: 6
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/windows-server-frequently-asked-questions -->

# Foundry Local on Windows Server 2025

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Foundry Local on Windows Server 2025 lets you run selected Microsoft Foundry model capabilities entirely on a single Windows Server machine you operate. Use this FAQ to quickly confirm what differentiates the Local runtime from the cloud service, how you deploy it, supported OS and GPU scenarios, concurrency behavior, and how the SDK relates to the service.

## Frequently asked questions

**What is the capability differentiation between Foundry Local on Windows Server vs Foundry?****Capability****Foundry Local (on server)****Foundry (cloud)**Model catalog Local catalog is smaller, BYOM possible. Embeddings models aren't yet available in the Local catalog. Broad catalog, including embeddings in the service; managed updates, evaluation, safety tools, and agent services. Scale & HA Single node runtime. No ‑built-in ‑autoscale or ‑multinode‑ distribution. Managed scale, multiregional‑ options, HA/DR patterns, and platform governance. Best for high concurrency and bursting. Concurrency / throughput Limited; throughput declines as concurrent clients grow. No continuous batching today. Cloud scale and load distribution; platform services for concurrency and throughput. APIs OpenAI ‑compatible REST surface for chat/completions; MCP integration possible. Full Foundry APIs, Responses API, Agent Service, eval, and integration with dev tools. Operations You operate it like any server app: install, secure, monitor, back up; manage model bits locally. Enterprise governance, cost controls, environments, RBAC/Networking, evaluation, and integrated DevOps. **Is Foundry Local a Windows component, an app, or a service?**It runs as a service on a Windows Server machine. You can install it by using winget.

`winget install Microsoft.FoundryLocal`

**Which versions of server support Foundry Local?**- Windows Server 2025 Datacenter
- Windows Server 2025 Standard

**Does Foundry Local run on virtual machines with GPU-P?**Foundry Local

**detects the partitioned GPU inside a GPU-P VM**and picks up a CUDA-enabled model when one is available. Otherwise, it falls back appropriately. The execution provider is also automatically selected based on the availability of GPU inside the VM.**What are the concurrency limitations of Foundry Local on server?**Foundry Local isn't optimized to serve multiple users as a shared on-premises endpoint. It doesn't yet support concurrent inference requests. Requests to one Foundry Local endpoint are processed sequentially. You must manage parallel execution across multiple endpoints at the application level. As concurrent requests increase, throughput drops and latency increases. There's no continuous batching in the Local runtime, so request coalescing doesn't happen under load. For multiple users or spiky traffic, move to[Microsoft Foundry](../?view=foundry-classic).**How is Foundry Local SDK different from the Foundry Local service?**The

[Foundry Local SDK](reference-sdk?view=foundry-classic)is a development toolkit to build software or applications by using the Foundry Local service without using the Foundry Local CLI or REST APIs directly.

## Sample code

The [Medical report summary tool](https://github.com/microsoft/foundry-local-on-windowsserver-samples) demonstrates a medical report summarizer and translator using Foundry Local running in a remote Windows Server.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-best-practice -->

# Best practices and troubleshooting guide for Foundry Local

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

This article lists best practices and troubleshooting tips for Foundry Local.

## Prerequisites

- Install Foundry Local.
- Have internet access to download models (recommended).
- If you use the machine-scope installation workaround in this article, run PowerShell as Administrator.

### Verify the CLI

Run the following command to confirm that the Foundry Local CLI is installed and available in your PATH:

```
foundry --help
```


This command lists available commands and options.

Reference: [Foundry Local CLI Reference](reference-cli?view=foundry-classic)

## Security best practices

- Run Foundry Local only in environments that comply with your organization's security policies.
- Make sure your device meets your organization's security requirements when you handle sensitive data.
- Encrypt disks on devices that cache models containing sensitive fine-tuning data.

## Licensing considerations

Review the licensing implications for the models you run in Foundry Local. To view the full model license terms for each model in the catalog, run the following command. In the following command, replace the placeholder * <model>* with the model name:

```
foundry model info <model> --license
```


Reference: [Foundry Local CLI Reference](reference-cli?view=foundry-classic)

## Performance best practices

If you experience slow inference, consider the following strategies:

- Stop any AI Toolkit for VS Code inference session before you run Foundry Local.
- Use GPU acceleration when available.
- Identify bottlenecks by monitoring memory usage during inference.
- Try more quantized model variants (for example, INT8 instead of FP16).
- Adjust batch sizes for noninteractive workloads.

## Production deployment scope

Foundry Local is for on-device inference, not distributed, containerized, or multi-machine production deployments.

## Troubleshooting

### Common issues and solutions

| Issue | Possible cause | Solution |
|---|---|---|
| Slow inference | CPU-only model with a large parameter count. | Use GPU-optimized model variants when available. |
| Model download failures | Network connectivity issues. | Check your internet connection, and run `foundry cache list` to verify cache status. |
Service connection errors (`Request to local service failed. Uri:http://127.0.0.1:0/foundry/list` ) |
Port binding issues or the service isn't accessible. | Run `foundry service restart` to restart the service and resolve port binding problems. |
| Service fails to start. | Port conflicts or permission issues. | Run `foundry service restart` , or
`foundry zip-logs` . |
| Intel NPU not detected or not working | Missing or outdated Intel NPU driver. | Install the
|

`Qnn error code 5005: "Failed to load from EpContext model. qnn_backend_manager."`

)[Qualcomm NPU driver](https://softwarecenter.qualcomm.com/catalog/item/QHND). If the issue persists, reboot to clear NPU resource conflicts, especially after using Windows Copilot+ features.`winget install Microsoft.FoundryLocal --scope machine`

fails with “The current system configuration doesn't support the installation of this package.”[Installation issues](#installation-issues).### Installation issues

If `winget install Microsoft.FoundryLocal --scope machine`

fails with “The current system configuration doesn't support the installation of this package.”, use `Add-AppxProvisionedPackage`

instead.

- Download the
`.msix`

and its dependency package. - Run PowerShell as Administrator.
- Run the following command to install Foundry Local for all users:

```
Add-AppxProvisionedPackage -Online -PackagePath .\FoundryLocal.msix `
-DependencyPackagePath .\VcLibs.appx -SkipLicense
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-catalog-api -->

# Catalog API reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Foundry Local lets you build and integrate your own catalog service. This article covers:

- Model format required for the catalog API
- Request and response format required for your catalog API to integrate with Foundry Local

## Prerequisites

- You have Foundry Local installed.
- You can run a web service that exposes a
`POST`

endpoint. - Your model artifacts are available in ONNX format.
- Azure role-based access control (RBAC): Not applicable.

## Model format

To work with Foundry Local, your model catalog must contain model files in the [Open Neural Network Exchange (ONNX)](https://onnx.ai/) format. To learn how to compile Hugging Face and PyTorch models to ONNX, see [Compile Hugging Face models to run on Foundry Local](../how-to/how-to-compile-hugging-face-models?view=foundry-classic).

## API format

### Request

Implement a POST endpoint in your catalog service that accepts a JSON request body. The request format for the catalog API is as follows:

**Method**:`POST`

**Content-Type**:`application/json`


#### Example request

```
curl -X POST <your-catalog-api-endpoint> \
-H "Content-Type: application/json" \
-d '{
"resourceIds": [
{
"resourceId": "azureml",
"entityContainerType": "Registry"
}
],
"indexEntitiesRequest": {
"filters": [
{
"field": "type",
"operator": "eq",
"values": [
"models"
]
},
{
"field": "kind",
"operator": "eq",
"values": [
"Versioned"
]
},
{
"field": "properties/variantInfo/variantMetadata/device",
"operator": "eq",
"values": [
"cpu",
"gpu"
]
},
{
"field": "properties/variantInfo/variantMetadata/executionProvider",
"operator": "eq",
"values": [
"cpuexecutionprovider",
"webgpuexecutionprovider"
]
}
],
"pageSize": 10,
"skip": null,
"continuationToken": null
}
}'
```


Replace `<your-catalog-api-endpoint>`

with your catalog service URL.

**What to expect**

- A successful response includes an
`indexEntitiesResponse`

object. - Search results are returned in
`indexEntitiesResponse.value`

.

Reference:

The request body must be a JSON object with the following fields:

`resourceIds`

: An array of resource IDs that specify the resources to query. Each item includes:`resourceId`

: The ID of the resource.`entityContainerType`

: The type of entity container, such as`Registry`

,`Workspace`

, and others.

`indexEntitiesRequest`

: An object that contains the search parameters.`filters`

: An array of filter objects that specify the criteria for filtering the search results. Each filter includes:`field`

: The field to filter on, such as`type`

,`kind`

, and others.`operator`

: The operator to use for the filter. For example,`eq`

(equals),`ne`

(not equals),`gt`

(greater than),`lt`

(less than), and others.`values`

: An array of values to match against the field.

`orderBy`

: An array of fields to order the results by.`searchText`

: A string to search for in the results.`pageSize`

: The maximum number of results to return (for pagination).`skip`

: The number of results to skip (for pagination).`continuationToken`

: A token for pagination to continue from a previous request.


#### Filterable fields (optional)

Implement the catalog API so it accepts the [Request](#request) format. Server-side filtering is optional. Skipping server-side filtering is faster to implement but is less efficient for searching models.

If you implement server-side filtering, use the following fields:

`type`

: The type of the model, such as`models`

,`datasets`

, and others.`kind`

: The kind of the model, such as`Versioned`

,`Unversioned`

, and others.`properties/variantInfo/variantMetadata/device`

: The device type, such as`cpu`

,`gpu`

, and others.`properties/variantInfo/variantMetadata/executionProvider`

: The execution provider, such as`cpuexecutionprovider`

,`webgpuexecutionprovider`

, and others.

### Response

The catalog API returns a JSON object that contains the search results.

#### Example response

```
{
"indexEntitiesResponse": {
"totalCount": 1,
"value": [
{
"assetId": "example-asset-id",
"version": "1",
"properties": {
"name": "example-model",
"version": 1,
"variantInfo": {
"variantMetadata": {
"device": "cpu",
"executionProvider": "cpuexecutionprovider"
}
}
}
}
],
"nextSkip": null,
"continuationToken": null
}
}
```


#### Response schema

```
{
"$schema": "http://json-schema.org/draft-07/schema#",
"type": "object",
"properties": {
"indexEntitiesResponse": {
"type": "object",
"properties": {
"totalCount": {
"type": "integer",
"description": "The total count of entities."
},
"value": {
"type": "array",
"description": "An array of LocalModel objects.",
"items": {
"$ref": "#/definitions/LocalModel"
}
},
"nextSkip": {
"type": "integer",
"description": "The number of items to skip for the next request."
},
"continuationToken": {
"type": "string",
"description": "A token to continue fetching results."
}
}
}
},
"definitions": {
"LocalModel": {
"type": "object",
"properties": {
"annotations": {
"type": "object",
"description": "Annotations associated with the model.",
"properties": {
"tags": {
"type": "object",
"description": "Tags associated with the annotation.",
"properties": {
"author": { "type": "string" },
"alias": { "type": "string" },
"directoryPath": { "type": "string" },
"license": { "type": "string" },
"licenseDescription": { "type": "string" },
"promptTemplate": { "type": "string" },
"task": { "type": "string" }
}
},
"systemCatalogData": {
"type": "object",
"properties": {
"publisher": { "type": "string" },
"displayName": { "type": "string" }
}
},
"name": { "type": "string" }
}
},
"properties": {
"type": "object",
"description": "Properties of the model.",
"properties": {
"name": { "type": "string" },
"version": { "type": "integer" },
"alphanumericVersion": { "type": "string" },
"variantInfo": {
"type": "object",
"properties": {
"parents": {
"type": "array",
"items": {
"type": "object",
"properties": {
"assetId": { "type": "string" }
}
}
},
"variantMetadata": {
"type": "object",
"properties": {
"modelType": { "type": "string" },
"device": { "type": "string" },
"executionProvider": { "type": "string" },
"fileSizeBytes": { "type": "integer" }
}
}
}
}
}
},
"version": {
"type": "string",
"description": "The version of the model."
},
"assetId": {
"type": "string",
"description": "The asset ID of the model."
}
}
}
}
}
```


Reference:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-cli -->

# Foundry Local CLI reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

This article provides a comprehensive reference for the Foundry Local command-line interface (CLI). The CLI organizes commands into logical categories to help you manage models, control the service, and maintain your local cache.

## Prerequisites

- Install Foundry Local. For setup steps, see
[Get started with Foundry Local](../get-started?view=foundry-classic). - Use a local terminal where the
`foundry`

CLI is available. - Ensure you have internet access for first-time downloads (execution providers and models).
- Azure RBAC: Not applicable (runs locally).
- If you have an Intel NPU on Windows, install the
[Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html)for optimal NPU acceleration.

## Quick verification

Run these commands to confirm the CLI is installed and the service is reachable.

Show CLI help:

`foundry --help`

This command prints usage information and the list of available command groups.

Reference:

[Overview](#overview)Check the service status:

`foundry service status`

This command prints whether the Foundry Local service is running and includes its local endpoint.

Reference:

[Service commands](#service-commands)

## Overview

Use the built-in help to explore commands and options.

The CLI organizes commands into three main categories:

**Model**: Commands for managing and running AI models**Service**: Commands for controlling the Foundry Local service**Cache**: Commands for managing your local model storage

## Model commands

The following table summarizes the commands related to managing and running models:

Note

You can specify the `model`

argument by its **alias** or **model ID**. Using an alias:

- Selects the best model for your available hardware automatically. For example, if you have an Nvidia GPU available, Foundry Local selects the best GPU model. If you have a supported NPU available, Foundry Local selects the NPU model.
- Lets you use a shorter name without needing to remember the model ID.

If you want to run a specific model, use the model ID. For example, to run the `qwen2.5-0.5b`

on CPU - irrespective of your available hardware - use: `foundry model run qwen2.5-0.5b-instruct-generic-cpu`

.

Command |
Description |
|---|---|
`foundry model --help` |
Displays all available model-related commands and their usage. |
`foundry model run <model>` |
Runs a specified model, downloads it if it isn't cached, and starts an interaction. |
`foundry model list` |
Lists all available models for local use. On first run, it downloads execution providers (EPs) for your hardware. |
`foundry model list --filter <key>=<value>` |
Lists models filtered by the specified criteria (device, task, alias, provider). |
`foundry model info <model>` |
Displays detailed information about a specific model. |
`foundry model info <model> --license` |
Displays the license information for a specific model. |
`foundry model download <model>` |
Downloads a model to the local cache without running it. |
`foundry model load <model>` |
Loads a model into the service. |
`foundry model unload <model>` |
Unloads a model from the service. |

### Model list ordering

When multiple model ID variants are available for an alias, the model list shows the models in priority order. The first model in the list is the model that runs when you specify the model by `alias`

.

### Model list filtering

The `foundry model list`

command supports filtering models by using the `--filter`

option. You can filter models based on a single attribute by using key-value pairs.

```
foundry model list --filter <key>=<value>
```


This command prints models that match the filter key and value.

Reference: [Model list filtering](#model-list-filtering)

Note

When you run `foundry model list`

for the first time after installation, Foundry Local automatically downloads the relevant execution providers (EPs) for your machine's hardware configuration. You see a progress bar indicating the download completion before the model list appears.

**Supported filter keys:**

#### device - Hardware Device Type

Filters models by the hardware device they run on.

**Possible values:**

`CPU`

- Central processing unit models`GPU`

- Graphics processing unit models`NPU`

- Neural processing unit models

#### provider - Execution Provider

Filters models by their execution provider or runtime.

**Possible values:**

`CPUExecutionProvider`

- CPU-based execution`CUDAExecutionProvider`

- NVIDIA CUDA GPU execution`WebGpuExecutionProvider`

- WebGPU execution`QNNExecutionProvider`

- Qualcomm Neural Network execution (NPU)`OpenVINOExecutionProvider`

- Intel OpenVINO execution`NvTensorRTRTXExecutionProvider`

- NVIDIA TensorRT execution`VitisAIExecutionProvider`

- AMD Vitis AI execution

#### task - Model Task Type

Filters models by their intended use case or task.

**Common values:**

`chat-completion`

: Conversational AI models`text-generation`

: Text generation models

#### alias - Model Alias

Filters models by their alias identifier. Supports wildcard matching with `*`

suffix.

**Sample values:**

`phi4-cpu`

`qwen2.5-coder-0.5b-instruct-generic-cpu`

`deepseek-r1-distill-qwen-1.5b-generic-cpu`

`phi-4-mini-instruct-generic-cpu`


### Special filter features

**Negation Support:** Prefix any value with `!`

to exclude matching models.

```
foundry model list --filter device=!GPU
```


This command excludes GPU models from the results.

Reference: [Special filter features](#special-filter-features)

**Wildcard Matching (alias only):** Append `*`

to match prefixes when filtering by alias.

```
foundry model list --filter alias=qwen*
```


This command returns models whose alias starts with `qwen`

.

Reference: [Special filter features](#special-filter-features)

### Examples

```
foundry model list --filter device=GPU
foundry model list --filter task=chat-completion
foundry model list --filter provider=CUDAExecutionProvider
```


These examples filter the model list by device, task, and execution provider.

Reference: [Model list filtering](#model-list-filtering)

Note

- All comparisons are case-insensitive.
- Only one filter can be used per command.
- Unrecognized filter keys result in an error.

## Service commands

The following table summarizes the commands related to managing and running the Foundry Local service:

Command |
Description |
|---|---|
`foundry service --help` |
Displays all available service-related commands and their usage. |
`foundry service start` |
Starts the Foundry Local service. |
`foundry service stop` |
Stops the Foundry Local service. |
`foundry service restart` |
Restarts the Foundry Local service. |
`foundry service status` |
Displays the current status of the Foundry Local service. |
`foundry service ps` |
Lists all models currently loaded in the Foundry Local service. |
`foundry service diag` |
Displays the logs of the Foundry Local service. |
`foundry service set <options>` |
Sets the configuration of the Foundry Local service. |

## Cache commands

The following table summarizes the commands for managing the local cache where models are stored:

Command |
Description |
|---|---|
`foundry cache --help` |
Shows all available cache-related commands and their usage. |
`foundry cache location` |
Shows the current cache directory. |
`foundry cache list` |
Lists all models stored in the local cache. |
`foundry cache cd <path>` |
Changes the cache directory to the specified path. |
`foundry cache remove <model>` |
Removes a model from the local cache. |

## Execution providers

Execution providers are hardware-specific acceleration libraries that run models as efficiently as possible on your device.

### Built-in execution providers

Foundry Local includes the CPU execution provider, the WebGPU execution provider, and the CUDA execution provider.

The CPU execution provider uses [Microsoft Linear Algebra Subroutines (MLAS)](https://github.com/microsoft/mlas) to run on any CPU and is the CPU fallback for Foundry Local.

The WebGPU execution provider uses [Dawn](https://github.com/google/dawn), the native implementation of the web-based API, for acceleration on any GPU, and is the GPU fallback for Foundry Local.

The CUDA execution provider uses NVIDIA CUDA for acceleration on NVIDIA GPUs. It requires an NVIDIA GeForce RTX 30 series and later with a minimum recommended driver version 32.0.15.5585 and CUDA version 12.5. It's subject to the following license terms: [License Agreement for NVIDIA Software Development Kits—EULA](https://docs.nvidia.com/cuda/eula/index.html).

### Plugin execution providers

The execution providers listed in the following table are available for dynamic download and registration on Windows, depending on device and driver compatibility. They're subject to the license terms specified.

Foundry Local automatically downloads these execution providers on first run. The plugin execution providers automatically update when new versions are available.

| Name (Vendor) | Requirements | License terms |
|---|---|---|
`NvTensorRTRTXExecutionProvider` (NVIDIA) |
NVIDIA GeForce RTX 30XX and later versions with minimum recommended driver version 32.0.15.5585 and CUDA version 12.5 |
|

`OpenVINOExecutionProvider`

(Intel)GPU: Intel AlderLake (12th Gen) and later versions with min recommended driver 32.0.101.1029

NPU: Intel ArrowLake (15th Gen) and later versions with min recommended driver 32.0.100.4239

[Intel OBL Distribution Commercial Use License Agreement v2025.02.12](https://cdrdv2.intel.com/v1/dl/getContent/849090?explicitVersion=true)`QNNExecutionProvider`

(Qualcomm)Snapdragon(R) X Plus - X1Pxxxxx - Qualcomm(R) Hexagon(TM) NPU with minimum driver version 30.0.140.0 and later versions

`VitisAIExecutionProvider`

(AMD)Max: Adrenalin Edition 25.9.1 with NPU driver 32.00.0203.297

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-rest -->

# Foundry Local REST API Reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Caution

This API refers to the REST API available in the Foundry Local CLI. This API is under active development and may include breaking changes without notice. We strongly recommend monitoring the changelog before building production applications.

## POST /v1/chat/completions

This endpoint processes chat completion requests.

It's fully compatible with the [OpenAI Chat Completions API](https://platform.openai.com/docs/api-reference/chat/create).

**Request Body:**

*---Standard OpenAI Properties---*

`model`

(string)

The specific model to use for completion.`messages`

(array)

The conversation history as a list of messages.- Each message requires:
`role`

(string)

The message sender's role. Must be`system`

,`user`

, or`assistant`

.`content`

(string)

The actual message text.


- Each message requires:
`temperature`

(number, optional)

Controls randomness, ranging from 0 to 2. Higher values (0.8) create varied outputs, while lower values (0.2) create focused, consistent outputs.`top_p`

(number, optional)

Controls token selection diversity from 0 to 1. A value of 0.1 means only the tokens in the top 10% probability are considered.`n`

(integer, optional)

Number of alternative completions to generate for each input message.`stream`

(boolean, optional)

When true, sends partial message responses as server-sent events, ending with a`data: [DONE]`

message.`stop`

(string or array, optional)

Up to 4 sequences that will cause the model to stop generating further tokens.`max_tokens`

(integer, optional)

Maximum number of tokens to generate. For newer models, use`max_completion_tokens`

instead.`max_completion_tokens`

(integer, optional)

Maximum number of tokens the model can generate, including visible output and reasoning tokens.`presence_penalty`

(number, optional)

Value between -2.0 and 2.0. Positive values encourage the model to discuss new topics by penalizing tokens that have already appeared.`frequency_penalty`

(number, optional)

Value between -2.0 and 2.0. Positive values discourage repetition by penalizing tokens based on their frequency in the text.`logit_bias`

(map, optional)

Adjusts the probability of specific tokens appearing in the completion.`user`

(string, optional)

A unique identifier for your end-user that helps with monitoring and abuse prevention.`functions`

(array, optional)

Available functions for which the model can generate JSON inputs.- Each function must include:
`name`

(string)

Function name.`description`

(string)

Function description.`parameters`

(object)

Function parameters described as a JSON Schema object.


- Each function must include:
`function_call`

(string or object, optional)

Controls how the model responds to function calls.- If object, can include:
`name`

(string, optional)

The name of the function to call.`arguments`

(object, optional)

The arguments to pass to the function.


- If object, can include:
`metadata`

(object, optional)

A dictionary of metadata key-value pairs.`top_k`

(number, optional)

The number of highest probability vocabulary tokens to keep for top-k-filtering.`random_seed`

(integer, optional)

Seed for reproducible random number generation.`ep`

(string, optional)

Overwrite the provider for ONNX models. Supports:`"dml"`

,`"cuda"`

,`"qnn"`

,`"cpu"`

,`"webgpu"`

.`ttl`

(integer, optional)

Time to live in seconds for the model in memory.`tools`

(object, optional)

Tools calculated for the request.

**Response body:**

`id`

(string)

Unique identifier for the chat completion.`object`

(string)

The object type, always`"chat.completion"`

.`created`

(integer)

Creation timestamp in epoch seconds.`model`

(string)

The model used for completion.`choices`

(array)

List of completion choices, each containing:`index`

(integer)

The index of this choice.`message`

(object)

The generated message with:`role`

(string)

Always`"assistant"`

for responses.`content`

(string)

The actual generated text.

`finish_reason`

(string)

Why generation stopped (e.g.,`"stop"`

,`"length"`

,`"function_call"`

).

`usage`

(object)

Token usage statistics:`prompt_tokens`

(integer)

Tokens in the prompt.`completion_tokens`

(integer)

Tokens in the completion.`total_tokens`

(integer)

Total tokens used.


**Example:**

Request body

```
{
"model": "qwen2.5-0.5b-instruct-generic-cpu",
"messages": [
{
"role": "user",
"content": "Hello, how are you?"
}
],
"temperature": 0.7,
"top_p": 1,
"n": 1,
"stream": false,
"stop": null,
"max_tokens": 100,
"presence_penalty": 0,
"frequency_penalty": 0,
"logit_bias": {},
"user": "user_id_123",
"functions": [],
"function_call": null,
"metadata": {}
}
```


Response body

```
{
"id": "chatcmpl-1234567890",
"object": "chat.completion",
"created": 1677851234,
"model": "qwen2.5-0.5b-instruct-generic-cpu",
"choices": [
{
"index": 0,
"message": {
"role": "assistant",
"content": "I'm doing well, thank you! How can I assist you today?"
},
"finish_reason": "stop"
}
],
"usage": {
"prompt_tokens": 10,
"completion_tokens": 20,
"total_tokens": 30
}
}
```


## GET /openai/status

Get server status information.

**Response body:**

`Endpoints`

(array of strings)

The HTTP server binding endpoints.`ModelDirPath`

(string)

Directory where local models are stored.`PipeName`

(string)

The current NamedPipe server name.

**Example:**

Response body

```
{
"Endpoints": ["http://localhost:5272"],
"ModelDirPath": "/path/to/models",
"PipeName": "inference_agent"
}
```


## GET /foundry/list

Get a list of available Foundry Local models in the catalog.

**Response:**

`models`

(array)

Array of model objects. Each model includes:`name`

: The unique identifier for the model.`displayName`

: A human-readable name for the model, often the same as the name.`providerType`

: The type of provider hosting the model (for example, AzureFoundry).`uri`

: The resource URI pointing to the model's location in the registry.`version`

: The version number of the model.`modelType`

: The format or type of the model (for example, ONNX).`promptTemplate`

:`assistant`

: The template for the assistant's response.`prompt`

: The template for the user-assistant interaction.

`publisher`

: The entity or organization that published the model.`task`

: The primary task the model is designed to perform (for example, chat completion).`runtime`

:`deviceType`

: The type of hardware the model is designed to run on (for example, CPU).`executionProvider`

: The execution provider used for running the model.

`fileSizeMb`

: The size of the model file in megabytes.`modelSettings`

:`parameters`

: A list of configurable parameters for the model.

`alias`

: An alternative name or shorthand for the model`supportsToolCalling`

: Indicates whether the model supports tool-calling functionality.`license`

: The license type under which the model is distributed.`licenseDescription`

: A detailed description or link to the license terms.`parentModelUri`

: The URI of the parent model from which this model is derived.


## GET /openai/models

Get a list of cached models, including local and registered external models.

**Response:**

- 200 OK

An array of model names as strings.

**Example:**

Response body

```
["Phi-4-mini-instruct-generic-cpu", "phi-3.5-mini-instruct-generic-cpu"]
```


## POST /openai/download

Download a model from the catalog to local storage.

Note

Large model downloads can take a long time. Set a high timeout for this request to avoid early termination.

**Request Body:**

`model`

(`WorkspaceInferenceModel`

object)`Uri`

(string)

The model URI to download.`Name`

(string) The model name.`ProviderType`

(string, optional)

The provider type (for example,`"AzureFoundryLocal"`

,`"HuggingFace"`

).`Path`

(string, optional)

Remote path to the model files. For example, in a Hugging Face repository, this is the path to the model files.`PromptTemplate`

(`Dictionary<string, string>`

, optional)

Includes:`system`

(string, optional)

The template for the system message.`user`

(string, optional) The template for the user's message.`assistant`

(string, optional)

The template for the assistant's response.`prompt`

(string, optional)

The template for the user-assistant interaction.

`Publisher`

(string, optional)

The publisher of the model.

`token`

(string, optional)

Authentication token for protected models (GitHub or Hugging Face).`progressToken`

(object, optional)

For AITK only. Token to track download progress.`customDirPath`

(string, optional)

Custom download directory (used for CLI, not needed for AITK).`bufferSize`

(integer, optional)

HTTP download buffer size in KB. No effect on NIM or Azure Foundry models.`ignorePipeReport`

(boolean, optional)

If`true`

, forces progress reporting via HTTP stream instead of pipe. Defaults to`false`

for AITK and`true`

for Foundry Local.

**Streaming Response:**

During download, the server streams progress updates in the format:

```
("file name", percentage_complete)
```


**Final Response body:**

`Success`

(boolean)

Whether the download completed successfully.`ErrorMessage`

(string, optional)

Error details if download failed.

**Example:**

Request URI

```
POST /openai/download
```


Request body

Note that the version suffix must be supplied in the model name.

```
{
"model": {
"Uri": "azureml://registries/azureml/models/Phi-4-mini-instruct-generic-cpu/versions/4",
"ProviderType": "AzureFoundryLocal",
"Name": "Phi-4-mini-instruct-generic-cpu:4",
"Publisher": "",
"PromptTemplate": {
"system": "<|system|>{Content}<|end|>",
"user": "<|user|>{Content}<|end|>",
"assistant": "<|assistant|>{Content}<|end|>",
"prompt": "<|user|>{Content}<|end|><|assistant|>"
}
}
}
```


Response stream

```
("genai_config.json", 0.01)
("genai_config.json", 0.2)
("model.onnx.data", 0.5)
("model.onnx.data", 0.78)
...
("", 1)
```


Final response

```
{
"Success": true,
"ErrorMessage": null
}
```


## GET /openai/load/{name}

Load a model into memory for faster inference.

**URI Parameters:**

`name`

(string)

The model name to load.

**Query Parameters:**

`unload`

(boolean, optional)

Whether to automatically unload the model after idle time. Defaults to`true`

.`ttl`

(integer, optional)

Time to live in seconds. If it's greater than 0, this value overrides the`unload`

parameter.`ep`

(string, optional)

Execution provider to run this model. Supports:`"dml"`

,`"cuda"`

,`"qnn"`

,`"cpu"`

,`"webgpu"`

.

If not specified, uses settings from`genai_config.json`

.

**Response:**

- 200 OK

Empty response body

**Example:**

Request URI

```
GET /openai/load/Phi-4-mini-instruct-generic-cpu?ttl=3600&ep=dml
```


## GET /openai/unload/{name}

Unload a model from memory.

**URI Parameters:**

`name`

(string) The model name to unload.

**Query Parameters:**

`force`

(boolean, optional) If`true`

, ignores TTL settings and unloads immediately.

**Response:**

- 200 OK Empty response body

**Example:**

Request URI

```
GET /openai/unload/Phi-4-mini-instruct-generic-cpu?force=true
```


## GET /openai/unloadall

Unloads all models from memory.

**Response:**

- 200 OK

Empty response body

## GET /openai/loadedmodels

Get the list of currently loaded models.

**Response:**

- 200 OK

An array of model names as strings.

**Example:**

Response body

```
["Phi-4-mini-instruct-generic-cpu", "phi-3.5-mini-instruct-generic-cpu"]
```


## GET /openai/getgpudevice

Get the current GPU device ID.

**Response:**

- 200 OK

An integer representing the current GPU device ID.

## GET /openai/setgpudevice/{deviceId}

Set the active GPU device.

**URI Parameters:**

`deviceId`

(integer)

The GPU device ID to use.

**Response:**

- 200 OK

Empty response body

**Example:**

- Request URI
`GET /openai/setgpudevice/1`


## POST /v1/chat/completions/tokenizer/encode/count

Counts tokens for a given chat completion request without performing inference.

**Request Body:**

- Content-Type: application/json
- JSON object in
`ChatCompletionCreateRequest`

format with:`model`

(string)

Model to use for tokenization.`messages`

(array)

Array of message objects with`role`

and`content`

.


**Response Body:**

- Content-Type: application/json
- JSON object with token count:
`tokenCount`

(integer)

Number of tokens in the request.


**Example:**

Request body

```
{
"messages": [
{
"role": "system",
"content": "This is a system message"
},
{
"role": "user",
"content": "Hello, what is Microsoft?"
}
],
"model": "Phi-4-mini-instruct-cuda-gpu"
}
```


Response body

```
{
"tokenCount": 23
}
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/reference/reference-sdk -->

# Foundry Local SDK reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

The Foundry Local SDK simplifies AI model management in local environments by providing control plane operations separate from data plane inference code. This reference documents SDK implementations for Python, JavaScript, C#, and Rust.

## Python SDK Reference

### Prerequisites

- Install Foundry Local and ensure the
`foundry`

command is available on your`PATH`

. - Use Python 3.9 or later.

### Installation

Install the Python package:

```
pip install foundry-local-sdk
```


### Quickstart

Use this snippet to verify that the SDK can start the service and reach the local catalog.

```
from foundry_local import FoundryLocalManager
manager = FoundryLocalManager()
manager.start_service()
catalog = manager.list_catalog_models()
print(f"Catalog models available: {len(catalog)}")
```


This example prints a non-zero number when the service is running and the catalog is available.

References:

### FoundryLocalManager Class

The `FoundryLocalManager`

class provides methods to manage models, cache, and the Foundry Local service.

#### Initialization

```
from foundry_local import FoundryLocalManager
# Initialize and optionally bootstrap with a model
manager = FoundryLocalManager(alias_or_model_id=None, bootstrap=True)
```


`alias_or_model_id`

: (optional) Alias or Model ID to download and load at startup.`bootstrap`

: (default True) If True, starts the service if not running and loads the model if provided.

### A note on aliases

Many methods outlined in this reference have an `alias_or_model_id`

parameter in the signature. You can pass into the method either an **alias** or **model ID** as a value. Using an alias will:

- Select the
*best model*for the available hardware. For example, if a Nvidia CUDA GPU is available, Foundry Local selects the CUDA model. If a supported NPU is available, Foundry Local selects the NPU model. - Allow you to use a shorter name without needing to remember the model ID.

Tip

We recommend passing into the `alias_or_model_id`

parameter an **alias** because when you deploy your application, Foundry Local acquires the best model for the end user's machine at run-time.

Note

If you have an Intel NPU on Windows, ensure you have installed the [Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html) for optimal NPU acceleration.

### Service Management

| Method | Signature | Description |
|---|---|---|
`is_service_running()` |
`() -> bool` |
Checks if the Foundry Local service is running. |
`start_service()` |
`() -> None` |
Starts the Foundry Local service. |
`service_uri` |
`@property -> str` |
Returns the service URI. |
`endpoint` |
`@property -> str` |
Returns the service endpoint. |
`api_key` |
`@property -> str` |
Returns the API key (from env or default). |

### Catalog Management

| Method | Signature | Description |
|---|---|---|
`list_catalog_models()` |
`() -> list[FoundryModelInfo]` |
Lists all available models in the catalog. |
`refresh_catalog()` |
`() -> None` |
Refreshes the model catalog. |
`get_model_info()` |
`(alias_or_model_id: str, raise_on_not_found=False) -> FoundryModelInfo \| None` |
Gets model info by alias or ID. |

### Cache Management

| Method | Signature | Description |
|---|---|---|
`get_cache_location()` |
`() -> str` |
Returns the model cache directory path. |
`list_cached_models()` |
`() -> list[FoundryModelInfo]` |
Lists models downloaded to the local cache. |

### Model Management

| Method | Signature | Description |
|---|---|---|
`download_model()` |
`(alias_or_model_id: str, token: str = None, force: bool = False) -> FoundryModelInfo` |
Downloads a model to the local cache. |
`load_model()` |
`(alias_or_model_id: str, ttl: int = 600) -> FoundryModelInfo` |
Loads a model into the inference server. |
`unload_model()` |
`(alias_or_model_id: str, force: bool = False) -> None` |
Unloads a model from the inference server. |
`list_loaded_models()` |
`() -> list[FoundryModelInfo]` |
Lists all models currently loaded in the service. |

### FoundryModelInfo

The methods `list_catalog_models()`

, `list_cached_models()`

, and `list_loaded_models()`

return a list of `FoundryModelInfo`

objects. You can use the information contained in this object to further refine the list. Or get the information for a model directly by calling the `get_model_info(alias_or_model_id)`

method.

These objects contain the following fields:

| Field | Type | Description |
|---|---|---|
`alias` |
`str` |
Alias of the model. |
`id` |
`str` |
Unique identifier of the model. |
`version` |
`str` |
Version of the model. |
`execution_provider` |
`str` |
The accelerator (
|

`device_type`

`DeviceType`

`uri`

`str`

`file_size_mb`

`int`

`supports_tool_calling`

`bool`

`prompt_template`

`dict \| None`

`provider`

`str`

`publisher`

`str`

`license`

`str`

`task`

`str`

`chat-completions`

or `automatic-speech-recognition`

.`ep_override`

`str \| None`

### Execution Providers

One of:

`CPUExecutionProvider`

- CPU-based execution`CUDAExecutionProvider`

- NVIDIA CUDA GPU execution`WebGpuExecutionProvider`

- WebGPU execution`QNNExecutionProvider`

- Qualcomm Neural Network execution (NPU)`OpenVINOExecutionProvider`

- Intel OpenVINO execution`NvTensorRTRTXExecutionProvider`

- NVIDIA TensorRT execution`VitisAIExecutionProvider`

- AMD Vitis AI execution

## Example Usage

The following code demonstrates how to use the `FoundryLocalManager`

class to manage models and interact with the Foundry Local service.

```
from foundry_local import FoundryLocalManager
# By using an alias, the most suitable model will be selected
# to your end-user's device.
alias = "qwen2.5-0.5b"
# Create a FoundryLocalManager instance. This will start the Foundry.
manager = FoundryLocalManager()
# List available models in the catalog
catalog = manager.list_catalog_models()
print(f"Available models in the catalog: {catalog}")
# Download and load a model
model_info = manager.download_model(alias)
model_info = manager.load_model(alias)
print(f"Model info: {model_info}")
# List models in cache
local_models = manager.list_cached_models()
print(f"Models in cache: {local_models}")
# List loaded models
loaded = manager.list_loaded_models()
print(f"Models running in the service: {loaded}")
# Unload a model
manager.unload_model(alias)
```


This example lists models, downloads and loads one model, and then unloads it.

References:

### Integrate with OpenAI SDK

Install the OpenAI package:

```
pip install openai
```


The following code demonstrates how to integrate the `FoundryLocalManager`

with the OpenAI SDK to interact with a local model.

```
import openai
from foundry_local import FoundryLocalManager
# By using an alias, the most suitable model will be downloaded
# to your end-user's device.
alias = "qwen2.5-0.5b"
# Create a FoundryLocalManager instance. This will start the Foundry
# Local service if it is not already running and load the specified model.
manager = FoundryLocalManager(alias)
# The remaining code uses the OpenAI Python SDK to interact with the local model.
# Configure the client to use the local Foundry service
client = openai.OpenAI(
base_url=manager.endpoint,
api_key=manager.api_key # API key is not required for local usage
)
# Set the model to use and generate a streaming response
stream = client.chat.completions.create(
model=manager.get_model_info(alias).id,
messages=[{"role": "user", "content": "Why is the sky blue?"}],
stream=True
)
# Print the streaming response
for chunk in stream:
if chunk.choices[0].delta.content is not None:
print(chunk.choices[0].delta.content, end="", flush=True)
```


This example streams a chat completion response from the local model.

References:

## JavaScript SDK Reference

### Prerequisites

- Install Foundry Local and ensure the
`foundry`

command is available on your`PATH`

.

### Installation

Install the package from npm:

```
npm install foundry-local-sdk
```


### Quickstart

Use this snippet to verify that the SDK can start the service and reach the local catalog.

```
import { FoundryLocalManager } from "foundry-local-sdk";
const manager = new FoundryLocalManager();
await manager.startService();
const catalogModels = await manager.listCatalogModels();
console.log(`Catalog models available: ${catalogModels.length}`);
```


This example prints a non-zero number when the service is running and the catalog is available.

References:

### FoundryLocalManager Class

The `FoundryLocalManager`

class lets you manage models, control the cache, and interact with the Foundry Local service in both browser and Node.js environments.

#### Initialization

```
import { FoundryLocalManager } from "foundry-local-sdk";
const foundryLocalManager = new FoundryLocalManager();
```


Available options:

`host`

: Base URL of the Foundry Local service`fetch`

: (optional) Custom fetch implementation for environments like Node.js

### A note on aliases

Many methods outlined in this reference have an `aliasOrModelId`

parameter in the signature. You can pass into the method either an **alias** or **model ID** as a value. Using an alias will:

- Select the
*best model*for the available hardware. For example, if a Nvidia CUDA GPU is available, Foundry Local selects the CUDA model. If a supported NPU is available, Foundry Local selects the NPU model. - Allow you to use a shorter name without needing to remember the model ID.

Tip

We recommend passing into the `aliasOrModelId`

parameter an **alias** because when you deploy your application, Foundry Local acquires the best model for the end user's machine at run-time.

Note

If you have an Intel NPU on Windows, ensure you have installed the [Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html) for optimal NPU acceleration.

### Service Management

| Method | Signature | Description |
|---|---|---|
`init()` |
`(aliasOrModelId?: string) => Promise<FoundryModelInfo \| void>` |
Initializes the SDK and optionally loads a model. |
`isServiceRunning()` |
`() => Promise<boolean>` |
Checks if the Foundry Local service is running. |
`startService()` |
`() => Promise<void>` |
Starts the Foundry Local service. |
`serviceUrl` |
`string` |
The base URL of the Foundry Local service. |
`endpoint` |
`string` |
The API endpoint (`serviceUrl` + `/v1` ). |
`apiKey` |
`string` |
The API key (none). |

### Catalog Management

| Method | Signature | Description |
|---|---|---|
`listCatalogModels()` |
`() => Promise<FoundryModelInfo[]>` |
Lists all available models in the catalog. |
`refreshCatalog()` |
`() => Promise<void>` |
Refreshes the model catalog. |
`getModelInfo()` |
`(aliasOrModelId: string, throwOnNotFound = false) => Promise<FoundryModelInfo \| null>` |
Gets model info by alias or ID. |

### Cache Management

| Method | Signature | Description |
|---|---|---|
`getCacheLocation()` |
`() => Promise<string>` |
Returns the model cache directory path. |
`listCachedModels()` |
`() => Promise<FoundryModelInfo[]>` |
Lists models downloaded to the local cache. |

### Model Management

| Method | Signature | Description |
|---|---|---|
`downloadModel()` |
`(aliasOrModelId: string, token?: string, force = false, onProgress?) => Promise<FoundryModelInfo>` |
Downloads a model to the local cache. |
`loadModel()` |
`(aliasOrModelId: string, ttl = 600) => Promise<FoundryModelInfo>` |
Loads a model into the inference server. |
`unloadModel()` |
`(aliasOrModelId: string, force = false) => Promise<void>` |
Unloads a model from the inference server. |
`listLoadedModels()` |
`() => Promise<FoundryModelInfo[]>` |
Lists all models currently loaded in the service. |

## Example Usage

The following code demonstrates how to use the `FoundryLocalManager`

class to manage models and interact with the Foundry Local service.

```
import { FoundryLocalManager } from "foundry-local-sdk";
// By using an alias, the most suitable model will be downloaded
// to your end-user's device.
// TIP: You can find a list of available models by running the
// following command in your terminal: `foundry model list`.
const alias = "qwen2.5-0.5b";
const manager = new FoundryLocalManager();
// Initialize the SDK and optionally load a model
const modelInfo = await manager.init(alias);
console.log("Model Info:", modelInfo);
// Check if the service is running
const isRunning = await manager.isServiceRunning();
console.log(`Service running: ${isRunning}`);
// List available models in the catalog
const catalog = await manager.listCatalogModels();
// Download and load a model
await manager.downloadModel(alias);
await manager.loadModel(alias);
// List models in cache
const localModels = await manager.listCachedModels();
// List loaded models
const loaded = await manager.listLoadedModels();
// Unload a model
await manager.unloadModel(alias);
```


This example downloads and loads a model, then lists cached and loaded models.

References:

## Integration with OpenAI Client

Install the OpenAI package:

```
npm install openai
```


The following code demonstrates how to integrate the `FoundryLocalManager`

with the OpenAI client to interact with a local model.

```
import { OpenAI } from "openai";
import { FoundryLocalManager } from "foundry-local-sdk";
// By using an alias, the most suitable model will be downloaded
// to your end-user's device.
// TIP: You can find a list of available models by running the
// following command in your terminal: `foundry model list`.
const alias = "qwen2.5-0.5b";
// Create a FoundryLocalManager instance. This will start the Foundry
// Local service if it is not already running.
const foundryLocalManager = new FoundryLocalManager();
// Initialize the manager with a model. This will download the model
// if it is not already present on the user's device.
const modelInfo = await foundryLocalManager.init(alias);
console.log("Model Info:", modelInfo);
const openai = new OpenAI({
baseURL: foundryLocalManager.endpoint,
apiKey: foundryLocalManager.apiKey,
});
async function streamCompletion() {
const stream = await openai.chat.completions.create({
model: modelInfo.id,
messages: [{ role: "user", content: "What is the golden ratio?" }],
stream: true,
});
for await (const chunk of stream) {
if (chunk.choices[0]?.delta?.content) {
process.stdout.write(chunk.choices[0].delta.content);
}
}
}
streamCompletion();
```


This example streams a chat completion response from the local model.

References:

## Browser Usage

The SDK includes a browser-compatible version where you must specify the host URL manually:

```
import { FoundryLocalManager } from "foundry-local-sdk/browser";
// Specify the service URL
// Run the Foundry Local service using the CLI: `foundry service start`
// and use the URL from the CLI output
const host = "HOST";
const manager = new FoundryLocalManager({ host });
// Note: The `init`, `isServiceRunning`, and `startService` methods
// are not available in the browser version
```


Note

The browser version doesn't support the `init`

, `isServiceRunning`

, and `startService`

methods. You must ensure that the Foundry Local service is running before using the SDK in a browser environment. You can start the service using the Foundry Local CLI: `foundry service start`

. You can glean the service URL from the CLI output.

#### Example Usage

```
import { FoundryLocalManager } from "foundry-local-sdk/browser";
// Specify the service URL
// Run the Foundry Local service using the CLI: `foundry service start`
// and use the URL from the CLI output
const host = "HOST";
const manager = new FoundryLocalManager({ host });
const alias = "qwen2.5-0.5b";
// Get all available models
const catalog = await manager.listCatalogModels();
console.log("Available models in catalog:", catalog);
// Download and load a specific model
await manager.downloadModel(alias);
await manager.loadModel(alias);
// View models in your local cache
const localModels = await manager.listCachedModels();
console.log("Cached models:", localModels);
// Check which models are currently loaded
const loaded = await manager.listLoadedModels();
console.log("Loaded models in inference service:", loaded);
// Unload a model when finished
await manager.unloadModel(alias);
```


References:

## C# SDK Reference

### Project setup guide

There are two NuGet packages for the Foundry Local SDK - a WinML and a cross-platform package - that have the same API surface but are optimized for different platforms:

**Windows**: Uses the`Microsoft.AI.Foundry.Local.WinML`

package that's specific to Windows applications, which uses the Windows Machine Learning (WinML) framework.**Cross-platform**: Uses the`Microsoft.AI.Foundry.Local`

package that can be used for cross-platform applications (Windows, Linux, macOS).

Depending on your target platform, follow these instructions to create a new C# application and add the necessary dependencies:

Use Foundry Local in your C# project by following these Windows-specific or Cross-Platform (macOS/Linux/Windows) instructions:

- Create a new C# project and navigate into it:
`dotnet new console -n app-name cd app-name`

- Open and edit the
`app-name.csproj`

file to:`<Project Sdk="Microsoft.NET.Sdk"> <PropertyGroup> <OutputType>Exe</OutputType> <TargetFramework>net9.0-windows10.0.26100</TargetFramework> <RootNamespace>app-name</RootNamespace> <ImplicitUsings>enable</ImplicitUsings> <Nullable>enable</Nullable> <WindowsAppSDKSelfContained>false</WindowsAppSDKSelfContained> <WindowsPackageType>None</WindowsPackageType> <EnableCoreMrtTooling>false</EnableCoreMrtTooling> </PropertyGroup> <ItemGroup> <PackageReference Include="Microsoft.AI.Foundry.Local.WinML" Version="0.8.2.1" /> <PackageReference Include="Microsoft.Extensions.Logging" Version="9.0.10" /> <PackageReference Include="OpenAI" Version="2.5.0" /> </ItemGroup> </Project>`

- Create a
`nuget.config`

file in the project root with the following content so that the packages restore correctly:`<?xml version="1.0" encoding="utf-8"?> <configuration> <packageSources> <clear /> <add key="nuget.org" value="https://api.nuget.org/v3/index.json" /> <add key="ORT" value="https://aiinfra.pkgs.visualstudio.com/PublicPackages/_packaging/ORT/nuget/v3/index.json" /> </packageSources> <packageSourceMapping> <packageSource key="nuget.org"> <package pattern="*" /> </packageSource> <packageSource key="ORT"> <package pattern="*Foundry*" /> </packageSource> </packageSourceMapping> </configuration>`


### Quickstart

Use this snippet to verify that the SDK can initialize and access the local model catalog.

```
using Microsoft.AI.Foundry.Local;
using Microsoft.Extensions.Logging;
using System.Linq;
var config = new Configuration
{
AppName = "app-name",
LogLevel = Microsoft.AI.Foundry.Local.LogLevel.Information,
};
using var loggerFactory = LoggerFactory.Create(builder =>
{
builder.SetMinimumLevel(Microsoft.Extensions.Logging.LogLevel.Information);
});
var logger = loggerFactory.CreateLogger<Program>();
await FoundryLocalManager.CreateAsync(config, logger);
var manager = FoundryLocalManager.Instance;
var catalog = await manager.GetCatalogAsync();
var models = await catalog.ListModelsAsync();
Console.WriteLine($"Models available: {models.Count()}");
```


This example prints the number of models available for your hardware.

References:

### Redesign

To improve your ability to ship applications using on-device AI, there are substantial changes to the architecture of the C# SDK in version `0.8.0`

and later. In this section, we outline the key changes to help you migrate your applications to the latest version of the SDK.

Note

In the SDK version `0.8.0`

and later, there are breaking changes in the API from previous versions.

The following diagram shows how the previous architecture - for versions earlier than `0.8.0`

- relied heavily on using a REST webserver to manage models and inference like chat completions:

The SDK would use a Remote Procedural Call (RPC) to find Foundry Local CLI executable on the machine, start the webserver, and then communicate with it over HTTP. This architecture had several limitations, including:

- Complexity in managing the webserver lifecycle.
- Challenging deployment: End users needed to have the Foundry Local CLI installed on their machines
*and*your application. - Version management of the CLI and SDK could lead to compatibility issues.

To address these issues, the redesigned architecture in version `0.8.0`

and later uses a more streamlined approach. The new architecture is as follows:

In this new architecture:

- Your application is
**self-contained**. It doesn't require the Foundry Local CLI to be installed separately on the end user's machine making it easier for you to deploy applications. - The REST
**web server is**. You can still use the web server if you want to integrate with other tools that communicate over HTTP. Read*optional*[Use chat completions via REST server with Foundry Local](../how-to/how-to-integrate-with-inference-sdks?view=foundry-classic)for details on how to use this feature. - The SDK has
**native support for chat completions and audio transcriptions**, allowing you to build conversational AI applications with fewer dependencies. Read[Use Foundry Local native chat completions API](../how-to/how-to-use-native-chat-completions?view=foundry-classic)for details on how to use this feature. - On Windows devices, you can use a Windows ML build that handles
**hardware acceleration**for models on the device by pulling in the right runtime and drivers.

#### API changes

Version `0.8.0`

and later provides a more object-orientated and composable API. The main entry point continues to be the `FoundryLocalManager`

class, but instead of being a flat set of methods that operate via static calls to a stateless HTTP API, the SDK now exposes methods on the `FoundryLocalManager`

instance that maintain state about the service and models.

| Primitive | Versions < 0.8.0 | Versions >= 0.8.0 |
|---|---|---|
Configuration |
N/A | `config = Configuration(...)` |
Get Manager |
`mgr = FoundryLocalManager();` |
`await FoundryLocalManager.CreateAsync(config, logger);` `var mgr = FoundryLocalManager.Instance;` |
Get Catalog |
N/A | `catalog = await mgr.GetCatalogAsync();` |
List Models |
`mgr.ListCatalogModelsAsync();` |
`catalog.ListModelsAsync();` |
Get Model |
`mgr.GetModelInfoAsync("aliasOrModelId");` |
`catalog.GetModelAsync(alias: "alias");` |
Get Variant |
N/A | `model.SelectedVariant;` |
Set Variant |
N/A | `model.SelectVariant();` |
Download a model |
`mgr.DownloadModelAsync("aliasOrModelId");` |
`model.DownloadAsync()` |
Load a model |
`mgr.LoadModelAsync("aliasOrModelId");` |
`model.LoadAsync()` |
Unload a model |
`mgr.UnloadModelAsync("aliasOrModelId");` |
`model.UnloadAsync()` |
List loaded models |
`mgr.ListLoadedModelsAsync();` |
`catalog.GetLoadedModelsAsync();` |
Get model path |
N/A | `model.GetPathAsync()` |
Start service |
`mgr.StartServiceAsync();` |
`mgr.StartWebServerAsync();` |
Stop service |
`mgr.StopServiceAsync();` |
`mgr.StopWebServerAsync();` |
Cache location |
`mgr.GetCacheLocationAsync();` |
`config.ModelCacheDir` |
List cached models |
`mgr.ListCachedModelsAsync();` |
`catalog.GetCachedModelsAsync();` |

The API allows Foundry Local to be more configurable over the web server, logging, cache location, and model variant selection. For example, the `Configuration`

class allows you to set up the application name, logging level, web server URLs, and directories for application data, model cache, and logs:

```
var config = new Configuration
{
AppName = "app-name",
LogLevel = Microsoft.AI.Foundry.Local.LogLevel.Information,
Web = new Configuration.WebService
{
Urls = "http://127.0.0.1:55588"
},
AppDataDir = "./foundry_local_data",
ModelCacheDir = "{AppDataDir}/model_cache",
LogsDir = "{AppDataDir}/logs"
};
```


References:

In the previous version of the Foundry Local C# SDK, you couldn't configure these settings directly through the SDK, which limited your ability to customize the behavior of the service.

### Reduce application package size

The Foundry Local SDK pulls in `Microsoft.ML.OnnxRuntime.Foundry`

NuGet package as a dependency. The `Microsoft.ML.OnnxRuntime.Foundry`

package provides the *inference runtime bundle*, which is the set of libraries required to efficiently run inference on specific vendor hardware devices. The inference runtime bundle includes the following components:

**ONNX Runtime library**: The core inference engine (`onnxruntime.dll`

).**ONNX Runtime Execution Provider (EP) library**. A hardware-specific backend in ONNX Runtime that optimizes and executes parts of a machine learning model a hardware accelerator. For example:- CUDA EP:
`onnxruntime_providers_cuda.dll`

- QNN EP:
`onnxruntime_providers_qnn.dll`


- CUDA EP:
**Independent Hardware Vendor (IHV) libraries**. For example:- WebGPU: DirectX dependencies (
`dxcompiler.dll`

,`dxil.dll`

) - QNN: Qualcomm QNN dependencies (
`QnnSystem.dll`

, etc.)

- WebGPU: DirectX dependencies (

The following table summarizes what EP and IHV libraries are bundled with your application and what WinML will download/install at runtime:

In all platforms and architectures, the CPU EP is required. The WebGPU EP and IHV libraries are small in size (for example, WebGPU only adds ~7MB to your application package) and are required in Windows and macOS. However, the CUDA and QNN EPs are large in size (for example, CUDA adds ~1GB to your application package) so we recommend excluding these EPs from your application package. WinML will download/install CUDA and QNN at runtime if the end user has compatible hardware.

Note

We're working on removing the CUDA and QNN EPs from the `Microsoft.ML.OnnxRuntime.Foundry`

package in future releases so that you don't need to include an `ExcludeExtraLibs.props`

file to remove them from your application package.

To reduce the size of your application package, you can create an `ExcludeExtraLibs.props`

file in your project directory with the following content, which excludes the CUDA and QNN EP and IHV libraries when you publish your application:

```
<Project>
<!-- we want to ensure we're using the onnxruntime libraries from Foundry Local Core so
we delete the WindowsAppSdk versions once they're unzipped. -->
<Target Name="ExcludeOnnxRuntimeLibs" AfterTargets="ExtractMicrosoftWindowsAppSDKMsixFiles">
<Delete Files="$(MicrosoftWindowsAppSDKMsixContent)\onnxruntime.dll"/>
<Delete Files="$(MicrosoftWindowsAppSDKMsixContent)\onnxruntime_providers_shared.dll"/>
<Message Importance="Normal" Text="Deleted onnxruntime libraries from $(MicrosoftWindowsAppSDKMsixContent)." />
</Target>
<!-- Remove CUDA EP and IHV libraries on Windows x64 -->
<Target Name="ExcludeCudaLibs" Condition="'$(RuntimeIdentifier)'=='win-x64'" AfterTargets="ResolvePackageAssets">
<ItemGroup>
<!-- match onnxruntime*cuda.* (we're matching %(Filename) which excludes the extension) -->
<NativeCopyLocalItems Remove="@(NativeCopyLocalItems)"
Condition="$([System.Text.RegularExpressions.Regex]::IsMatch('%(Filename)',
'^onnxruntime.*cuda.*', RegexOptions.IgnoreCase))" />
</ItemGroup>
<Message Importance="Normal" Text="Excluded onnxruntime CUDA libraries from package." />
</Target>
<!-- Remove QNN EP and IHV libraries on Windows arm64 -->
<Target Name="ExcludeQnnLibs" Condition="'$(RuntimeIdentifier)'=='win-arm64'" AfterTargets="ResolvePackageAssets">
<ItemGroup>
<NativeCopyLocalItems Remove="@(NativeCopyLocalItems)"
Condition="$([System.Text.RegularExpressions.Regex]::IsMatch('%(Filename)%(Extension)',
'^QNN.*\.dll', RegexOptions.IgnoreCase))" />
<NativeCopyLocalItems Remove="@(NativeCopyLocalItems)"
Condition="$([System.Text.RegularExpressions.Regex]::IsMatch('%(Filename)',
'^libQNNhtp.*', RegexOptions.IgnoreCase))" />
<NativeCopyLocalItems Remove="@(NativeCopyLocalItems)"
Condition="'%(FileName)%(Extension)' == 'onnxruntime_providers_qnn.dll'" />
</ItemGroup>
<Message Importance="Normal" Text="Excluded onnxruntime QNN libraries from package." />
</Target>
<!-- need to manually copy on linux-x64 due to the nuget packages not having the correct props file setup -->
<ItemGroup Condition="'$(RuntimeIdentifier)' == 'linux-x64'">
<!-- 'Update' as the Core package will add these dependencies, but we want to be explicit about the version -->
<PackageReference Update="Microsoft.ML.OnnxRuntime.Gpu" />
<PackageReference Update="Microsoft.ML.OnnxRuntimeGenAI.Cuda" />
<OrtNativeLibs Include="$(NuGetPackageRoot)microsoft.ml.onnxruntime.gpu.linux/$(OnnxRuntimeVersion)/runtimes/$(RuntimeIdentifier)/native/*" />
<OrtGenAINativeLibs Include="$(NuGetPackageRoot)microsoft.ml.onnxruntimegenai.cuda/$(OnnxRuntimeGenAIVersion)/runtimes/$(RuntimeIdentifier)/native/*" />
</ItemGroup>
<Target Name="CopyOrtNativeLibs" AfterTargets="Build" Condition=" '$(RuntimeIdentifier)' == 'linux-x64'">
<Copy SourceFiles="@(OrtNativeLibs)" DestinationFolder="$(OutputPath)"></Copy>
<Copy SourceFiles="@(OrtGenAINativeLibs)" DestinationFolder="$(OutputPath)"></Copy>
</Target>
</Project>
```


In your project file (`.csproj`

), add the following line to import the `ExcludeExtraLibs.props`

file:

```
<!-- other project file content -->
<Import Project="ExcludeExtraLibs.props" />
```


#### Windows: CUDA dependencies

The CUDA EP is pulled into your Linux application via `Microsoft.ML.OnnxRuntime.Foundry`

, but we don't include the IHV libraries. If you want to allow your end users with CUDA-enabled devices to benefit from higher performance, you need *add* the following CUDA IHV libraries to your application:

- CUBLAS v12.8.4 (
[download from NVIDIA Developer](https://developer.download.nvidia.com/compute/cuda/redist/libcublas/windows-x86_64/libcublas-windows-x86_64-12.8.4.1-archive.zip))- cublas64_12.dll
- cublasLt64_12.dll

- CUDA RT v12.8.90 (
[download from NVIDIA Developer](https://developer.download.nvidia.com/compute/cuda/redist/cuda_cudart/windows-x86_64/cuda_cudart-windows-x86_64-12.8.90-archive.zip))- cudart64_12.dll

- CUDNN v9.8.0 (
[download from NVIDIA Developer](https://developer.download.nvidia.com/compute/cudnn/redist/cudnn/windows-x86_64/cudnn-windows-x86_64-9.8.0.87_cuda12-archive.zip))- cudnn_graph64_9.dll
- cudnn_ops64_9.dll
- cudnn64_9.dll

- CUDA FFT v11.3.3.83 (
[download from NVIDIA Developer](https://developer.download.nvidia.com/compute/cuda/redist/libcufft/windows-x86_64/libcufft-windows-x86_64-11.3.3.83-archive.zip))- cufft64_11.dll


Warning

Adding the CUDA EP and IHV libraries to your application increase the size of your application package by 1GB.

### Samples

- For sample applications that demonstrate how to use the Foundry Local C# SDK, see the
[Foundry Local C# SDK Samples GitHub repository](https://aka.ms/foundrylocalSDK).

### API reference

- For more details on the Foundry Local C# SDK read
[Foundry Local C# SDK API Reference](https://aka.ms/fl-csharp-api-ref).

## Rust SDK reference

The Rust SDK for Foundry Local provides a way to manage models, control the cache, and interact with the Foundry Local service.

### Prerequisites

- Install Foundry Local and ensure the
`foundry`

command is available on your`PATH`

. - Use Rust 1.70.0 or later.

### Installation

To use the Foundry Local Rust SDK, add the following to your `Cargo.toml`

:

```
[dependencies]
foundry-local = "0.1.0"
```


Alternatively, you can add the Foundry Local crate using `cargo`

:

```
cargo add foundry-local
```


### Quickstart

Use this snippet to verify that the SDK can start the service and read the local catalog.

```
use anyhow::Result;
use foundry_local::FoundryLocalManager;
#[tokio::main]
async fn main() -> Result<()> {
let mut manager = FoundryLocalManager::builder().bootstrap(true).build().await?;
let models = manager.list_catalog_models().await?;
println!("Catalog models available: {}", models.len());
Ok(())
}
```


This example prints a non-zero number when the service is running and the catalog is available.

References:

`FoundryLocalManager`


Manager for Foundry Local SDK operations.

#### Fields

`service_uri: Option<String>`

— URI of the Foundry service.`client: Option<HttpClient>`

— HTTP client for API requests.`catalog_list: Option<Vec<FoundryModelInfo>>`

— Cached list of catalog models.`catalog_dict: Option<HashMap<String, FoundryModelInfo>>`

— Cached dictionary of catalog models.`timeout: Option<u64>`

— Optional HTTP client timeout.

#### Methods

`pub fn builder() -> FoundryLocalManagerBuilder`


Create a new builder for`FoundryLocalManager`

.`pub fn service_uri(&self) -> Result<&str>`


Get the service URI.

**Returns:**URI of the Foundry service.`fn client(&self) -> Result<&HttpClient>`


Get the HTTP client instance.

**Returns:**HTTP client.`pub fn endpoint(&self) -> Result<String>`


Get the endpoint for the service.

**Returns:**Endpoint URL.`pub fn api_key(&self) -> String`


Get the API key for authentication.

**Returns:**API key.`pub fn is_service_running(&mut self) -> bool`


Check if the service is running and set the service URI if found.

**Returns:**`true`

if running,`false`

otherwise.`pub fn start_service(&mut self) -> Result<()>`


Start the Foundry Local service.`pub async fn list_catalog_models(&mut self) -> Result<&Vec<FoundryModelInfo>>`


Get a list of available models in the catalog.`pub fn refresh_catalog(&mut self)`


Refresh the catalog cache.`pub async fn get_model_info(&mut self, alias_or_model_id: &str, raise_on_not_found: bool) -> Result<FoundryModelInfo>`


Get model information by alias or ID.

**Arguments:**`alias_or_model_id`

: Alias or Model ID.`raise_on_not_found`

: If true, error if not found.

`pub async fn get_cache_location(&self) -> Result<String>`


Get the cache location as a string.`pub async fn list_cached_models(&mut self) -> Result<Vec<FoundryModelInfo>>`


List cached models.`pub async fn download_model(&mut self, alias_or_model_id: &str, token: Option<&str>, force: bool) -> Result<FoundryModelInfo>`


Download a model.

**Arguments:**`alias_or_model_id`

: Alias or Model ID.`token`

: Optional authentication token.`force`

: Force re-download if already cached.

`pub async fn load_model(&mut self, alias_or_model_id: &str, ttl: Option<i32>) -> Result<FoundryModelInfo>`


Load a model for inference.

**Arguments:**`alias_or_model_id`

: Alias or Model ID.`ttl`

: Optional time-to-live in seconds.

`pub async fn unload_model(&mut self, alias_or_model_id: &str, force: bool) -> Result<()>`


Unload a model.

**Arguments:**`alias_or_model_id`

: Alias or Model ID.`force`

: Force unload even if in use.

`pub async fn list_loaded_models(&mut self) -> Result<Vec<FoundryModelInfo>>`


List loaded models.

`FoundryLocalManagerBuilder`


Builder for creating a `FoundryLocalManager`

instance.

#### Fields

`alias_or_model_id: Option<String>`

— Alias or model ID to download and load.`bootstrap: bool`

— Whether to start the service if not running.`timeout_secs: Option<u64>`

— HTTP client timeout in seconds.

#### Methods

`pub fn new() -> Self`


Create a new builder instance.`pub fn alias_or_model_id(mut self, alias_or_model_id: impl Into<String>) -> Self`


Set the alias or model ID to download and load.`pub fn bootstrap(mut self, bootstrap: bool) -> Self`


Set whether to start the service if not running.`pub fn timeout_secs(mut self, timeout_secs: u64) -> Self`


Set the HTTP client timeout in seconds.`pub async fn build(self) -> Result<FoundryLocalManager>`


Build the`FoundryLocalManager`

instance.

`FoundryModelInfo`


Represents information about a model.

#### Fields

`alias: String`

— The model alias.`id: String`

— The model ID.`version: String`

— The model version.`runtime: ExecutionProvider`

— The execution provider (CPU, CUDA, etc.).`uri: String`

— The model URI.`file_size_mb: i32`

— Model file size in MB.`prompt_template: serde_json::Value`

— Prompt template for the model.`provider: String`

— Provider name.`publisher: String`

— Publisher name.`license: String`

— License type.`task: String`

— Model task (e.g., text-generation).

#### Methods

`from_list_response(response: &FoundryListResponseModel) -> Self`


Creates a`FoundryModelInfo`

from a catalog response.`to_download_body(&self) -> serde_json::Value`


Converts the model info to a JSON body for download requests.

`ExecutionProvider`


Enum for supported execution providers.

`CPU`

`WebGPU`

`CUDA`

`QNN`


##### Methods

`get_alias(&self) -> String`


Returns a string alias for the execution provider.

`ModelRuntime`


Describes the runtime environment for a model.

`device_type: DeviceType`

`execution_provider: ExecutionProvider`
