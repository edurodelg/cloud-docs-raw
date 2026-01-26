---
merged_at: 2026-01-26T23:20:36.879637
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/reference/reference-model-inference-api -->

# Azure AI Model Inference REST API reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure AI model inference is an API that exposes a common set of capabilities for foundational models and that can be used by developers to consume predictions from a diverse set of models in a uniform and consistent way. Developers can talk with different models deployed in Azure AI Foundry portal without changing the underlying code they are using.

## Benefits

Foundational models, such as language models, have indeed made remarkable strides in recent years. These advancements have revolutionized various fields, including natural language processing and computer vision, and they have enabled applications like chatbots, virtual assistants, and language translation services.

While foundational models excel in specific domains, they lack a uniform set of capabilities. Some models are better at specific task and even across the same task, some models may approach the problem in one way while others in another. Developers can benefit from this diversity by **using the right model for the right job** allowing them to:

- Improve the performance in a specific downstream task.
- Use more efficient models for simpler tasks.
- Use smaller models that can run faster on specific tasks.
- Compose multiple models to develop intelligent experiences.

Having a uniform way to consume foundational models allow developers to realize all those benefits without sacrificing portability or changing the underlying code.

## Inference SDK support

The Azure AI Inference package allows you to consume all models supporting the Azure AI model inference API and easily change among them. Azure AI Inference package is part of the Azure AI Foundry SDK.

| Language | Documentation | Package | Examples |
|---|---|---|---|
| C# |
|

[azure-ai-inference (NuGet)](https://www.nuget.org/packages/Azure.AI.Inference/)[C# examples](https://aka.ms/azsdk/azure-ai-inference/csharp/samples)[Reference](https://aka.ms/azsdk/azure-ai-inference/java/reference)[azure-ai-inference (Maven)](https://central.sonatype.com/artifact/com.azure/azure-ai-inference/)[Java examples](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-inference/src/samples)[Reference](/en-us/javascript/api/@azure-rest/ai-inference)[@azure/ai-inference (npm)](https://www.npmjs.com/package/@azure/ai-inference)[JavaScript examples](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Reference](https://aka.ms/azsdk/azure-ai-inference/python/reference)[azure-ai-inference (PyPi)](https://pypi.org/project/azure-ai-inference/)[Python examples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-inference/samples)## Capabilities

The following section describes some of the capabilities the API exposes:

### Modalities

The API indicates how developers can consume predictions for the following modalities:

[Get info](/en-us/rest/api/aifoundry/model-inference/get-model-info/get-model-info): Returns the information about the model deployed under the endpoint.[Text embeddings](/en-us/rest/api/aifoundry/model-inference/get-embeddings/get-embeddings): Creates an embedding vector representing the input text.[Chat completions](/en-us/rest/api/aifoundry/model-inference/get-chat-completions/get-chat-completions): Creates a model response for the given chat conversation.[Image embeddings](/en-us/rest/api/aifoundry/model-inference/get-image-embeddings/get-image-embeddings): Creates an embedding vector representing the input text and image.

### Extensibility

The Azure AI Model Inference API specifies a set of modalities and parameters that models can subscribe to. However, some models may have further capabilities that the ones the API indicates. On those cases, the API allows the developer to pass them as extra parameters in the payload.

By setting a header `extra-parameters: pass-through`

, the API will attempt to pass any unknown parameter directly to the underlying model. If the model can handle that parameter, the request completes.

The following example shows a request passing the parameter `safe_prompt`

supported by Mistral-Large, which isn't specified in the Azure AI Model Inference API.

**Request**

```
POST /chat/completions?api-version=2025-04-01
Authorization: Bearer <bearer-token>
Content-Type: application/json
extra-parameters: pass-through
```


```
{
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Explain Riemann's conjecture in 1 paragraph"
}
],
"temperature": 0,
"top_p": 1,
"response_format": { "type": "text" },
"safe_prompt": true
}
```


Note

The default value for `extra-parameters`

is `error`

which returns an error if an extra parameter is indicated in the payload. Alternatively, you can set `extra-parameters: drop`

to drop any unknown parameter in the request. Use this capability in case you happen to be sending requests with extra parameters that you know the model won't support but you want the request to completes anyway. A typical example of this is indicating `seed`

parameter.

### Models with disparate set of capabilities

The Azure AI Model Inference API indicates a general set of capabilities but each of the models can decide to implement them or not. A specific error is returned on those cases where the model can't support a specific parameter.

The following example shows the response for a chat completion request indicating the parameter `reponse_format`

and asking for a reply in `JSON`

format. In the example, since the model doesn't support such capability an error 422 is returned to the user.

**Request**

```
POST /chat/completions?api-version=2025-04-01
Authorization: Bearer <bearer-token>
Content-Type: application/json
```


```
{
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Explain Riemann's conjecture in 1 paragraph"
}
],
"temperature": 0,
"top_p": 1,
"response_format": { "type": "json_object" },
}
```


**Response**

```
{
"status": 422,
"code": "parameter_not_supported",
"detail": {
"loc": [ "body", "response_format" ],
"input": "json_object"
},
"message": "One of the parameters contain invalid values."
}
```


Tip

You can inspect the property `details.loc`

to understand the location of the offending parameter and `details.input`

to see the value that was passed in the request.

## Content safety

The Azure AI model inference API supports [Azure AI Content Safety](../../../ai-studio/concepts/content-filtering.md). When using deployments with Azure AI Content Safety on, inputs and outputs pass through an ensemble of classification models aimed at detecting and preventing the output of harmful content. The content filtering (preview) system detects and takes action on specific categories of potentially harmful content in both input prompts and output completions.

The following example shows the response for a chat completion request that has triggered content safety.

**Request**

```
POST /chat/completions?api-version=2025-04-01
Authorization: Bearer <bearer-token>
Content-Type: application/json
```


```
{
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Chopping tomatoes and cutting them into cubes or wedges are great ways to practice your knife skills."
}
],
"temperature": 0,
"top_p": 1,
}
```


**Response**

```
{
"status": 400,
"code": "content_filter",
"message": "The response was filtered",
"param": "messages",
"type": null
}
```


## Getting started

Azure AI model inference API is available on Azure AI Services resources. You can get started with it the same way as any other Azure product where you [create and configure your resource for Azure AI model inference](/en-us/azure/ai-foundry/model-inference/how-to/quickstart-create-resources), or instance of the service, in your Azure Subscription. You can create as many resources as needed and configure them independently in case you have multiple teams with different requirements.

Once you create an Azure AI Services resource, you must deploy a model before you can start making API calls. By default, no models are available on it, so you can control which ones to start from. See the tutorial [Create your first model deployment in Azure AI model inference](/en-us/azure/ai-foundry/model-inference/how-to/create-model-deployments).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/reference/reference-model-inference-chat-completions -->

# Get Chat Completions - Get Chat Completions

Gets chat completions for the provided chat messages.
Completions support a wide variety of tasks and generate text that continues from or "completes"
provided prompt data. The method makes a REST API call to the `/chat/completions`

route
on the given endpoint.

`POST https://{resource}.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview`


## URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
|
resource
|
path | True |
string |
The Azure AI Services resource name, for example 'my-resource' |
|
api-version
|
query | True |
string minLength: 1 |
The API version to use for this operation. |

## Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| extra-parameters |
Controls what happens if extra parameters, undefined by the REST API,
are passed in the JSON request payload.
This sets the HTTP request header |

## Request Body

| Name | Required | Type | Description |
|---|---|---|---|
| messages | True | ChatRequestMessage[]: |
The collection of context messages associated with this chat completions request. Typical usage begins with a chat message for the System role that provides instructions for the behavior of the assistant, followed by alternating messages between the User and Assistant roles. |
| frequency_penalty |
number (float) minimum: -2maximum: 2 |
A value that influences the probability of generated tokens appearing based on their cumulative frequency in generated text. Positive values will make tokens less likely to appear as their frequency increases and decrease the likelihood of the model repeating the same statements verbatim. Supported range is [-2, 2]. |
|
| max_tokens |
integer (int32) minimum: 0 |
The maximum number of tokens to generate. |
|
| modalities |
The modalities that the model is allowed to use for the chat completions response. The default modality
is |
||
| model |
string |
ID of the specific AI model to use, if more than one model is available on the endpoint. |
|
| presence_penalty |
number (float) minimum: -2maximum: 2 |
A value that influences the probability of generated tokens appearing based on their existing presence in generated text. Positive values will make tokens less likely to appear when they already exist and increase the model's likelihood to output new topics. Supported range is [-2, 2]. |
|
| response_format | ChatCompletionsResponseFormat: |
An object specifying the format that the model must output. Setting to Setting to
|
|
| seed |
integer (int64) |
If specified, the system will make a best effort to sample deterministically such that repeated requests with the same seed and parameters should return the same result. Determinism is not guaranteed. |
|
| stop |
string[] |
A collection of textual sequences that will end completions generation. |
|
| stream |
boolean |
A value indicating whether chat completions should be streamed for this request. |
|
| temperature |
number (float) minimum: 0maximum: 1 |
The sampling temperature to use that controls the apparent creativity of generated completions. Higher values will make output more random while lower values will make results more focused and deterministic. It is not recommended to modify temperature and top_p for the same completions request as the interaction of these two settings is difficult to predict. Supported range is [0, 1]. |
|
| tool_choice |
|
If specified, the model will configure which of the provided tools it can use for the chat completions response. |
|
| tools |
A list of tools the model may request to call. Currently, only functions are supported as a tool. The model may response with a function call request and provide the input arguments in JSON format for that function. |
||
| top_p |
number (float) minimum: 0maximum: 1 |
An alternative to sampling with temperature called nucleus sampling. This value causes the model to consider the results of tokens with the provided probability mass. As an example, a value of 0.15 will cause only the tokens comprising the top 15% of probability mass to be considered. It is not recommended to modify temperature and top_p for the same completions request as the interaction of these two settings is difficult to predict. Supported range is [0, 1]. |

## Responses

| Name | Type | Description |
|---|---|---|
| 200 OK |
The request has succeeded. |
|
| Other Status Codes |
An unexpected error response. Headers x-ms-error-code: string |

## Security

### api-key

Type:
apiKey

In:
header


### OAuth2Auth

Type:
oauth2

Flow:
implicit

Authorization URL:
https://login.microsoftonline.com/common/oauth2/v2.0/authorize


#### Scopes

| Name | Description |
|---|---|
| https://cognitiveservices.azure.com/.default |

## Examples

|
|

[maximum set chat completion](#maximum-set-chat-completion)[minimum set chat completion](#minimum-set-chat-completion)### Audio modality chat completion

#### Sample request

```
POST https://{resource}.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview
{
"modalities": [
"text",
"audio"
],
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": [
{
"type": "input_audio",
"input_audio": {
"data": "<base64 encoded audio data>",
"format": "wav"
}
}
]
},
{
"role": "assistant",
"content": null,
"audio": {
"id": "abcdef1234"
}
},
{
"role": "user",
"content": [
{
"type": "input_audio",
"input_audio": {
"data": "<base64 encoded audio data>",
"format": "wav"
}
}
]
}
],
"frequency_penalty": 0,
"presence_penalty": 0,
"temperature": 0,
"top_p": 0,
"seed": 21,
"model": "my-model-name"
}
```


#### Sample response

```
{
"id": "kgousajxgzyhugvqekuswuqbk",
"object": "chat.completion",
"created": 1696522361,
"model": "my-model-name",
"usage": {
"completion_tokens": 19,
"prompt_tokens": 28,
"total_tokens": 16,
"completion_tokens_details": {
"audio_tokens": 5,
"total_tokens": 5
},
"prompt_tokens_details": {
"audio_tokens": 10,
"cached_tokens": 0
}
},
"choices": [
{
"index": 0,
"finish_reason": "stop",
"message": {
"role": "assistant",
"content": null,
"tool_calls": null,
"audio": {
"id": "abcdef1234",
"format": "wav",
"data": "<base64 encoded audio data>",
"expires_at": 1896522361,
"transcript": "This is a sample transcript"
}
}
}
]
}
```


### maximum set chat completion

#### Sample request

```
POST https://{resource}.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview
{
"modalities": [
"text"
],
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Explain Riemann's conjecture"
},
{
"role": "assistant",
"content": "The Riemann Conjecture is a deep mathematical conjecture around prime numbers and how they can be predicted. It was first published in Riemann's groundbreaking 1859 paper. The conjecture states that the Riemann zeta function has its zeros only at the negative even integers and complex numbers with real part 1/21. Many consider it to be the most important unsolved problem in pure mathematics. The Riemann hypothesis is a way to predict the probability that numbers in a certain range are prime that was also devised by German mathematician Bernhard Riemann in 18594."
},
{
"role": "user",
"content": "Ist it proved?"
}
],
"frequency_penalty": 0,
"stream": true,
"presence_penalty": 0,
"temperature": 0,
"top_p": 0,
"max_tokens": 255,
"response_format": {
"type": "text"
},
"stop": [
"<|endoftext|>"
],
"tools": [
{
"type": "function",
"function": {
"name": "my-function-name",
"description": "A function useful to know if a theroem is proved or not"
}
}
],
"seed": 21,
"model": "my-model-name"
}
```


#### Sample response

```
{
"id": "kgousajxgzyhugvqekuswuqbk",
"object": "chat.completion",
"created": 18,
"model": "my-model-name",
"usage": {
"completion_tokens": 19,
"prompt_tokens": 28,
"total_tokens": 16
},
"choices": [
{
"index": 7,
"finish_reason": "stop",
"message": {
"role": "assistant",
"content": null,
"tool_calls": [
{
"id": "yrobmilsrugmbwukmzo",
"type": "function",
"function": {
"name": "my-function-name",
"arguments": "{ \"arg1\": \"value1\", \"arg2\": \"value2\" }"
}
}
]
}
}
]
}
```


### minimum set chat completion

#### Sample request

```
POST https://{resource}.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview
{
"messages": [
{
"role": "user",
"content": "Explain Riemann's conjecture"
}
]
}
```


#### Sample response

```
{
"id": "kgousajxgzyhugvqekuswuqbk",
"object": "chat.completion",
"created": 1234567890,
"model": "my-model-name",
"usage": {
"prompt_tokens": 205,
"completion_tokens": 5,
"total_tokens": 210
},
"choices": [
{
"index": 0,
"finish_reason": "stop",
"message": {
"role": "assistant",
"content": "The Riemann Conjecture is a deep mathematical conjecture around prime numbers and how they can be predicted. It was first published in Riemann's groundbreaking 1859 paper. The conjecture states that the Riemann zeta function has its zeros only at the negative even integers and complex numbers with real part 1/21. Many consider it to be the most important unsolved problem in pure mathematics. The Riemann hypothesis is a way to predict the probability that numbers in a certain range are prime that was also devised by German mathematician Bernhard Riemann in 18594"
}
}
]
}
```


## Definitions

| Name | Description |
|---|---|
|
|

A representation of the possible audio formats for audio.

[Azure.](#azure.core.foundations.error) Core. Foundations. ErrorThe error object.

[Azure.](#azure.core.foundations.errorresponse) Core. Foundations. Error ResponseA response containing error details.

[Azure.](#azure.core.foundations.innererror) Core. Foundations. Inner ErrorAn object containing more specific information about the error. As per Azure REST API guidelines - [https://aka.ms/AzureRestApiGuidelines#handling-errors](https://aka.ms/AzureRestApiGuidelines#handling-errors).

[Chat](#chatchoice) ChoiceThe representation of a single prompt completion as part of an overall chat completions request.
Generally, `n`

choices are generated per provided prompt with a default value of 1.
Token limits and other settings may limit the number of choices generated.

[Chat](#chatcompletions) CompletionsRepresentation of the response data from a chat completions request. Completions support a wide variety of tasks and generate text that continues from or "completes" provided prompt data.

[Chat](#chatcompletionsaudio) Completions AudioA representation of the audio generated by the model.

[Chat](#chatcompletionsmodality) Completions ModalityThe modalities that the model is allowed to use for the chat completions response.

[Chat](#chatcompletionsoptions) Completions OptionsThe configuration information for a chat completions request. Completions support a wide variety of tasks and generate text that continues from or "completes" provided prompt data.

[Chat](#chatcompletionsresponseformatjsonobject) Completions Response Format Json ObjectA response format for Chat Completions that restricts responses to emitting valid JSON objects. Note that to enable JSON mode, some AI models may also require you to instruct the model to produce JSON via a system or user message.

[Chat](#chatcompletionsresponseformatjsonschema) Completions Response Format Json SchemaA response format for Chat Completions that restricts responses to emitting valid JSON objects, with a JSON schema specified by the caller.

[Chat](#chatcompletionsresponseformatjsonschemadefinition) Completions Response Format Json Schema DefinitionThe definition of the required JSON schema in the response, and associated metadata.

[Chat](#chatcompletionsresponseformattext) Completions Response Format TextA response format for Chat Completions that emits text responses. This is the default response format.

[Chat](#chatcompletionstoolcall) Completions Tool CallA function tool call requested by the AI model.

[Chat](#chatcompletionstooldefinition) Completions Tool DefinitionThe definition of a chat completions tool that can call a function.

[Chat](#chatrequestassistantmessage) Request Assistant MessageA request chat message representing response or action from the assistant.

[Chat](#chatrequestaudioreference) Request Audio ReferenceA reference to an audio response generated by the model.

[Chat](#chatrequestsystemmessage) Request System MessageA request chat message containing system instructions that influence how the model will generate a chat completions response.

[Chat](#chatrequesttoolmessage) Request Tool MessageA request chat message representing requested output from a configured tool.

[Chat](#chatrequestusermessage) Request User MessageA request chat message representing user input to the assistant.

[Chat](#chatresponsemessage) Response MessageA representation of a chat message as received in a response.

[Chat](#chatrole) RoleA description of the intended purpose of a message within a chat completions interaction.

[Completions](#completionsfinishreason) Finish ReasonRepresentation of the manner in which a completions response concluded.

[Completions](#completionsusage) UsageRepresentation of the token counts processed for a completions request. Counts consider all tokens across prompts, choices, choice alternates, best_of generations, and other consumers.

[Completions](#completionsusagedetails) Usage DetailsA breakdown of tokens used in a completion.

[Extra](#extraparameters) ParametersControls what happens if extra parameters, undefined by the REST API, are passed in the JSON request payload.

[Function](#functioncall) CallThe name and arguments of a function that should be called, as generated by the model.

[Function](#functiondefinition) DefinitionThe definition of a caller-specified function that chat completions may invoke in response to matching user input.

[Prompt](#promptusagedetails) Usage DetailsA breakdown of tokens used in the prompt/chat history.

### Audio Content Format

A representation of the possible audio formats for audio.

| Value | Description |
|---|---|
| wav |
Specifies audio in WAV format. |
| mp3 |
Specifies audio in MP3 format. |

### Azure. Core. Foundations. Error

The error object.

| Name | Type | Description |
|---|---|---|
| code |
string |
One of a server-defined set of error codes. |
| details |
An array of details about specific errors that led to this reported error. |
|
| innererror |
An object containing more specific information than the current object about the error. |
|
| message |
string |
A human-readable representation of the error. |
| target |
string |
The target of the error. |

### Azure. Core. Foundations. Error Response

A response containing error details.

| Name | Type | Description |
|---|---|---|
| error |
The error object. |

### Azure. Core. Foundations. Inner Error

An object containing more specific information about the error. As per Azure REST API guidelines - [https://aka.ms/AzureRestApiGuidelines#handling-errors](https://aka.ms/AzureRestApiGuidelines#handling-errors).

| Name | Type | Description |
|---|---|---|
| code |
string |
One of a server-defined set of error codes. |
| innererror |
Inner error. |

### Chat Choice

The representation of a single prompt completion as part of an overall chat completions request.
Generally, `n`

choices are generated per provided prompt with a default value of 1.
Token limits and other settings may limit the number of choices generated.

| Name | Type | Description |
|---|---|---|
| finish_reason |
The reason that this chat completions choice completed its generated. |
|
| index |
integer (int32) |
The ordered index associated with this chat completions choice. |
| message |
The chat message for a given chat completions prompt. |

### Chat Completions

Representation of the response data from a chat completions request. Completions support a wide variety of tasks and generate text that continues from or "completes" provided prompt data.

| Name | Type | Description |
|---|---|---|
| choices |
The collection of completions choices associated with this completions response.
Generally, |
|
| created |
integer (unixtime) |
The first timestamp associated with generation activity for this completions response, represented as seconds since the beginning of the Unix epoch of 00:00 on 1 Jan 1970. |
| id |
string |
A unique identifier associated with this chat completions response. |
| model |
string |
The model used for the chat completion. |
| object |
enum:
chat. |
The response object type, which is always |
| usage |
Usage information for tokens processed and generated as part of this completions operation. |

### Chat Completions Audio

A representation of the audio generated by the model.

| Name | Type | Description |
|---|---|---|
| data |
string |
Base64 encoded audio data |
| expires_at |
integer (unixtime) |
The Unix timestamp (in seconds) at which the audio piece expires and can't be any longer referenced by its ID in multi-turn conversations. |
| format |
The format of the audio content. If format is not provided, it will match the format used in the input audio request. |
|
| id |
string |
Unique identifier for the audio response. This value can be used in chat history messages instead of passing the full audio object. |
| transcript |
string |
The transcript of the audio file. |

### Chat Completions Modality

The modalities that the model is allowed to use for the chat completions response.

| Value | Description |
|---|---|
| text |
The model is only allowed to generate text. |
| audio |
The model is allowed to generate audio. |

### Chat Completions Options

The configuration information for a chat completions request. Completions support a wide variety of tasks and generate text that continues from or "completes" provided prompt data.

| Name | Type | Default value | Description |
|---|---|---|---|
| frequency_penalty |
number (float) minimum: -2maximum: 2 |
0 |
A value that influences the probability of generated tokens appearing based on their cumulative frequency in generated text. Positive values will make tokens less likely to appear as their frequency increases and decrease the likelihood of the model repeating the same statements verbatim. Supported range is [-2, 2]. |
| max_tokens |
integer (int32) minimum: 0 |
The maximum number of tokens to generate. |
|
| messages | ChatRequestMessage[]: |
The collection of context messages associated with this chat completions request. Typical usage begins with a chat message for the System role that provides instructions for the behavior of the assistant, followed by alternating messages between the User and Assistant roles. |
|
| modalities |
The modalities that the model is allowed to use for the chat completions response. The default modality
is |
||
| model |
string |
ID of the specific AI model to use, if more than one model is available on the endpoint. |
|
| presence_penalty |
number (float) minimum: -2maximum: 2 |
0 |
A value that influences the probability of generated tokens appearing based on their existing presence in generated text. Positive values will make tokens less likely to appear when they already exist and increase the model's likelihood to output new topics. Supported range is [-2, 2]. |
| response_format | ChatCompletionsResponseFormat: |
An object specifying the format that the model must output. Setting to Setting to
|
|
| seed |
integer (int64) |
If specified, the system will make a best effort to sample deterministically such that repeated requests with the same seed and parameters should return the same result. Determinism is not guaranteed. |
|
| stop |
string[] |
A collection of textual sequences that will end completions generation. |
|
| stream |
boolean |
A value indicating whether chat completions should be streamed for this request. |
|
| temperature |
number (float) minimum: 0maximum: 1 |
0.7 |
The sampling temperature to use that controls the apparent creativity of generated completions. Higher values will make output more random while lower values will make results more focused and deterministic. It is not recommended to modify temperature and top_p for the same completions request as the interaction of these two settings is difficult to predict. Supported range is [0, 1]. |
| tool_choice |
|
If specified, the model will configure which of the provided tools it can use for the chat completions response. |
|
| tools |
A list of tools the model may request to call. Currently, only functions are supported as a tool. The model may response with a function call request and provide the input arguments in JSON format for that function. |
||
| top_p |
number (float) minimum: 0maximum: 1 |
1 |
An alternative to sampling with temperature called nucleus sampling. This value causes the model to consider the results of tokens with the provided probability mass. As an example, a value of 0.15 will cause only the tokens comprising the top 15% of probability mass to be considered. It is not recommended to modify temperature and top_p for the same completions request as the interaction of these two settings is difficult to predict. Supported range is [0, 1]. |

### Chat Completions Response Format Json Object

A response format for Chat Completions that restricts responses to emitting valid JSON objects. Note that to enable JSON mode, some AI models may also require you to instruct the model to produce JSON via a system or user message.

| Name | Type | Description |
|---|---|---|
| type |
string:
json_object |
The response format type to use for chat completions. |

### Chat Completions Response Format Json Schema

A response format for Chat Completions that restricts responses to emitting valid JSON objects, with a JSON schema specified by the caller.

| Name | Type | Description |
|---|---|---|
| json_schema |
The definition of the required JSON schema in the response, and associated metadata. |
|
| type |
string:
json_schema |
The response format type to use for chat completions. |

### Chat Completions Response Format Json Schema Definition

The definition of the required JSON schema in the response, and associated metadata.

| Name | Type | Default value | Description |
|---|---|---|---|
| description |
string |
A description of the response format, used by the AI model to determine how to generate responses in this format. |
|
| name |
string |
The name of the response format. Must be a-z, A-Z, 0-9, or contain underscores and dashes, with a maximum length of 64. |
|
| schema |
|
The definition of the JSON schema |
|
| strict |
boolean |
False |
Whether to enable strict schema adherence when generating the output.
If set to true, the model will always follow the exact schema defined in the |

### Chat Completions Response Format Text

A response format for Chat Completions that emits text responses. This is the default response format.

| Name | Type | Description |
|---|---|---|
| type |
string:
text |
The response format type to use for chat completions. |

### Chat Completions Tool Call

A function tool call requested by the AI model.

| Name | Type | Description |
|---|---|---|
| function |
The details of the function call requested by the AI model. |
|
| id |
string |
The ID of the tool call. |
| type |
enum:
function |
The type of tool call. Currently, only |

### Chat Completions Tool Definition

The definition of a chat completions tool that can call a function.

| Name | Type | Description |
|---|---|---|
| function |
The function definition details for the function tool. |
|
| type |
enum:
function |
The type of the tool. Currently, only |

### Chat Request Assistant Message

A request chat message representing response or action from the assistant.

| Name | Type | Description |
|---|---|---|
| audio |
The audio generated by a previous response in a multi-turn conversation. |
|
| content |
string |
The content of the message. |
| role |
string:
assistant |
The chat role associated with this message. |
| tool_calls |
The tool calls that must be resolved and have their outputs appended to subsequent input messages for the chat completions request to resolve as configured. |

### Chat Request Audio Reference

A reference to an audio response generated by the model.

| Name | Type | Description |
|---|---|---|
| id |
string |
Unique identifier for the audio response. This value corresponds to the id of a previous audio completion. |

### Chat Request System Message

A request chat message containing system instructions that influence how the model will generate a chat completions response.

| Name | Type | Description |
|---|---|---|
| content |
string |
The contents of the system message. |
| role |
string:
system |
The chat role associated with this message. |

### Chat Request Tool Message

A request chat message representing requested output from a configured tool.

| Name | Type | Description |
|---|---|---|
| content |
string |
The content of the message. |
| role |
string:
tool |
The chat role associated with this message. |
| tool_call_id |
string |
The ID of the tool call resolved by the provided content. |

### Chat Request User Message

A request chat message representing user input to the assistant.

| Name | Type | Description |
|---|---|---|
| content |
|
The contents of the user message, with available input types varying by selected model. |
| role |
string:
user |
The chat role associated with this message. |

### Chat Response Message

A representation of a chat message as received in a response.

| Name | Type | Description |
|---|---|---|
| audio |
The audio generated by the model as a response to the messages if the model is configured to generate audio. |
|
| content |
string |
The content of the message. |
| role |
The chat role associated with the message. |
|
| tool_calls |
The tool calls that must be resolved and have their outputs appended to subsequent input messages for the chat completions request to resolve as configured. |

### Chat Role

A description of the intended purpose of a message within a chat completions interaction.

| Value | Description |
|---|---|
| system |
The role that instructs or sets the behavior of the assistant. |
| developer |
The role that provides instructions to the model prioritized ahead of user messages. |
| user |
The role that provides input for chat completions. |
| assistant |
The role that provides responses to system-instructed, user-prompted input. |
| tool |
The role that represents extension tool activity within a chat completions operation. |

### Completions Finish Reason

Representation of the manner in which a completions response concluded.

| Value | Description |
|---|---|
| stop |
Completions ended normally and reached its end of token generation. |
| length |
Completions exhausted available token limits before generation could complete. |
| content_filter |
Completions generated a response that was identified as potentially sensitive per content moderation policies. |
| tool_calls |
Completion ended with the model calling a provided tool for output. |

### Completions Usage

Representation of the token counts processed for a completions request. Counts consider all tokens across prompts, choices, choice alternates, best_of generations, and other consumers.

| Name | Type | Description |
|---|---|---|
| completion_tokens |
integer (int32) |
The number of tokens generated across all completions emissions. |
| completion_tokens_details |
Breakdown of tokens used in a completion. |
|
| prompt_tokens |
integer (int32) |
The number of tokens in the provided prompts for the completions request. |
| prompt_tokens_details |
Breakdown of tokens used in the prompt/chat history. |
|
| total_tokens |
integer (int32) |
The total number of tokens processed for the completions request and response. |

### Completions Usage Details

A breakdown of tokens used in a completion.

| Name | Type | Description |
|---|---|---|
| audio_tokens |
integer (int32) |
The number of tokens corresponding to audio input. |
| total_tokens |
integer (int32) |
The total number of tokens processed for the completions request and response. |

### Extra Parameters

Controls what happens if extra parameters, undefined by the REST API, are passed in the JSON request payload.

| Value | Description |
|---|---|
| error |
The service will error if it detected extra parameters in the request payload. This is the service default. |
| drop |
The service will ignore (drop) extra parameters in the request payload. It will only pass the known parameters to the back-end AI model. |
| pass-through |
The service will pass extra parameters to the back-end AI model. |

### Function Call

The name and arguments of a function that should be called, as generated by the model.

| Name | Type | Description |
|---|---|---|
| arguments |
string |
The arguments to call the function with, as generated by the model in JSON format. Note that the model does not always generate valid JSON, and may hallucinate parameters not defined by your function schema. Validate the arguments in your code before calling your function. |
| name |
string |
The name of the function to call. |

### Function Definition

The definition of a caller-specified function that chat completions may invoke in response to matching user input.

| Name | Type | Description |
|---|---|---|
| description |
string |
A description of what the function does. The model will use this description when selecting the function and interpreting its parameters. |
| name |
string |
The name of the function to be called. |
| parameters |
|
The parameters the function accepts, described as a JSON Schema object. |

### Prompt Usage Details

A breakdown of tokens used in the prompt/chat history.

| Name | Type | Description |
|---|---|---|
| audio_tokens |
integer (int32) |
The number of tokens corresponding to audio input. |
| cached_tokens |
integer (int32) |
The total number of tokens cached. |
