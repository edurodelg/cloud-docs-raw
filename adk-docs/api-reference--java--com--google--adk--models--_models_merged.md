---
merged_at: 2026-01-25T02:21:31.667002
merged_files: 19
---

# Documentos Fusionados

Este archivo contiene 19 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: llmregistryllmfactoryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/LlmRegistry.LlmFactory.html -->

# Interface LlmRegistry.LlmFactory

- Enclosing class:
[LlmRegistry](LlmRegistry.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

The factory interface for creating LLM instances.

-
## Method Summary


-
## Method Details

-
### create


-


---

<!-- DOCUMENTO FUSIONADO: modelhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/Model.html -->

# Class Model

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.Model

Represents a model by name or instance.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary


-
## Constructor Details

-
### Model

public Model()

-
-
## Method Details

-
### modelName

-
### model

-
### builder

-
### toBuilder


-


---

<!-- DOCUMENTO FUSIONADO: modelbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/Model.Builder.html -->

# Class Model.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.Model.Builder

- Enclosing class:
[Model](Model.html)

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[Model](Model.html)[build](#build())()`abstract`

[Model.Builder](Model.Builder.html)`abstract`

[Model.Builder](Model.Builder.html)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### modelName

-
### model

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: vertexcredentialshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/VertexCredentials.html -->

# Class VertexCredentials

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.VertexCredentials

Credentials for accessing Gemini models through Vertex.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[VertexCredentials.Builder](VertexCredentials.Builder.html)[builder](#builder())()`abstract`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.auth.oauth2.GoogleCredentials> [location](#location())()[project](#project())()

-
## Constructor Details

-
### VertexCredentials

public VertexCredentials()

-
-
## Method Details

-
### project

-
### location

-
### credentials

-
### builder


-


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/package-summary.html -->

# Package com.google.adk.models

package com.google.adk.models

-
ClassDescriptionAbstract base class for Large Language Models (LLMs).The base class for a live model connection.Represents the Claude Generative AI model by Anthropic.Represents the Gemini Generative AI model.Builder for
.`Gemini`

Manages a persistent, bidirectional connection to the Gemini model via WebSockets for real-time interaction.Central registry for managing Large Language Model (LLM) instances.The factory interface for creating LLM instances.Represents a request to be sent to the LLM.Builder for constructinginstances.`LlmRequest`

Represents a response received from the LLM.Builder for constructinginstances.`LlmResponse`

Represents a model by name or instance.Builder for.`Model`

Credentials for accessing Gemini models through Vertex.Builder for.`VertexCredentials`


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/package-use.html -->

# Uses of Packagecom.google.adk.models

# Uses of Package

com.google.adk.models

Package

Description

-
ClassDescriptionRepresents a request to be sent to the LLM.Represents a response received from the LLM.
-
ClassDescriptionAbstract base class for Large Language Models (LLMs).Represents a request to be sent to the LLM.Represents a response received from the LLM.Represents a model by name or instance.
-
ClassDescriptionRepresents a request to be sent to the LLM.Represents a response received from the LLM.
-
ClassDescriptionAbstract base class for Large Language Models (LLMs).The base class for a live model connection.Represents the Gemini Generative AI model.Builder for
.`Gemini`

The factory interface for creating LLM instances.Represents a request to be sent to the LLM.Builder for constructinginstances.`LlmRequest`

Represents a response received from the LLM.Builder for constructinginstances.`LlmResponse`

Represents a model by name or instance.Builder for.`Model`

Credentials for accessing Gemini models through Vertex.Builder for.`VertexCredentials`

-
ClassDescriptionAbstract base class for Large Language Models (LLMs).The base class for a live model connection.Represents a request to be sent to the LLM.Represents a response received from the LLM.
-
-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/package-tree.html -->

# Hierarchy For Package com.google.adk.models

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.models.
[BaseLlm](BaseLlm.html) - com.google.adk.models.
[Gemini.Builder](Gemini.Builder.html) - com.google.adk.models.
[GeminiLlmConnection](GeminiLlmConnection.html)(implements com.google.adk.models.[BaseLlmConnection](BaseLlmConnection.html)) - com.google.adk.
[JsonBaseModel](../JsonBaseModel.html)- com.google.adk.models.
[LlmRequest](LlmRequest.html) - com.google.adk.models.
[LlmResponse](LlmResponse.html)

- com.google.adk.models.
- com.google.adk.models.
[LlmRegistry](LlmRegistry.html) - com.google.adk.models.
[LlmRequest.Builder](LlmRequest.Builder.html) - com.google.adk.models.
[LlmResponse.Builder](LlmResponse.Builder.html) - com.google.adk.models.
[Model](Model.html) - com.google.adk.models.
[Model.Builder](Model.Builder.html) - com.google.adk.models.
[VertexCredentials](VertexCredentials.html) - com.google.adk.models.
[VertexCredentials.Builder](VertexCredentials.Builder.html)

- com.google.adk.models.

## Interface Hierarchy

- com.google.adk.models.
[BaseLlmConnection](BaseLlmConnection.html) - com.google.adk.models.
[LlmRegistry.LlmFactory](LlmRegistry.LlmFactory.html)


---

<!-- DOCUMENTO FUSIONADO: llmregistryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/LlmRegistry.html -->

# Class LlmRegistry

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.LlmRegistry

Central registry for managing Large Language Model (LLM) instances.

-
## Nested Class Summary

Modifier and TypeClassDescription`static interface`

The factory interface for creating LLM instances. -
## Method Summary

Modifier and TypeMethodDescription`static`

[BaseLlm](BaseLlm.html)Returns an LLM instance for the given model name, using a cached or new factory-created instance.`static void`

[registerLlm](#registerLlm(java.lang.String,com.google.adk.models.LlmRegistry.LlmFactory))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)modelNamePattern,[LlmRegistry.LlmFactory](LlmRegistry.LlmFactory.html)factory)Registers a factory for model names matching the given regex pattern.

-
## Method Details

-
### registerLlm

Registers a factory for model names matching the given regex pattern.- Parameters:
`modelNamePattern`

- Regex pattern for matching model names.`factory`

- Factory to create LLM instances.

-
### getLlm

Returns an LLM instance for the given model name, using a cached or new factory-created instance.- Parameters:
`modelName`

- Model name to look up.- Returns:
- Matching
instance.`BaseLlm`

- Throws:

- If no factory matches the model name.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)


-


---

<!-- DOCUMENTO FUSIONADO: basellmhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/BaseLlm.html -->

# Class BaseLlm

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.BaseLlm

- Direct Known Subclasses:

,[Claude](Claude.html)

,[Gemini](Gemini.html)[LangChain4j](langchain4j/LangChain4j.html)

Abstract base class for Large Language Models (LLMs).

Provides a common interface for interacting with different LLMs.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[BaseLlmConnection](BaseLlmConnection.html)[connect](#connect(com.google.adk.models.LlmRequest))( [LlmRequest](LlmRequest.html)llmRequest)Creates a live connection to the LLM.`abstract io.reactivex.rxjava3.core.Flowable`

< [LlmResponse](LlmResponse.html)>[generateContent](#generateContent(com.google.adk.models.LlmRequest,boolean))( [LlmRequest](LlmRequest.html)llmRequest, boolean stream)Generates one content from the given LLM request and tools.[model](#model())()Returns the name of the LLM model.

-
## Constructor Details

-
### BaseLlm


-
-
## Method Details

-
### model

-
### generateContent

public abstract io.reactivex.rxjava3.core.Flowable<[LlmResponse](LlmResponse.html)> generateContent( [LlmRequest](LlmRequest.html)llmRequest, boolean stream)Generates one content from the given LLM request and tools.- Parameters:
`llmRequest`

- The LLM request containing the input prompt and parameters.`stream`

- A boolean flag indicating whether to stream the response.- Returns:
- A Flowable of LlmResponses. For non-streaming calls, it will only yield one LlmResponse. For streaming calls, it may yield more than one LlmResponse, but all yielded LlmResponses should be treated as one content by merging their parts.

-
### connect

Creates a live connection to the LLM.

-


---

<!-- DOCUMENTO FUSIONADO: geminibuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/Gemini.Builder.html -->

# Class Gemini.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.Gemini.Builder

- Enclosing class:
[Gemini](Gemini.html)

-
## Method Summary

Modifier and TypeMethodDescription[apiClient](#apiClient(com.google.genai.Client))(com.google.genai.Client apiClient) Sets the explicit`Client`

instance for making API calls.Sets the Google Gemini API key.[build](#build())()Builds theinstance.`Gemini`

Sets the name of the Gemini model to use.[vertexCredentials](#vertexCredentials(com.google.adk.models.VertexCredentials))( [VertexCredentials](VertexCredentials.html)vertexCredentials)Sets the Vertex AI credentials.

-
## Method Details

-
### modelName

Sets the name of the Gemini model to use.- Parameters:
`modelName`

- The model name (e.g., "gemini-2.0-flash").- Returns:
- This builder.

-
### apiClient

Sets the explicit`Client`

instance for making API calls. If this is set, apiKey and vertexCredentials will be ignored.- Parameters:
`apiClient`

- The client instance.- Returns:
- This builder.

-
### apiKey

Sets the Google Gemini API key. Ifis also set, the explicit client will take precedence. If`apiClient(Client)`

is also set, this apiKey will take precedence.`vertexCredentials(VertexCredentials)`

- Parameters:
`apiKey`

- The API key.- Returns:
- This builder.

-
### vertexCredentials

Sets the Vertex AI credentials. Ifor`apiClient(Client)`

are also set, they will take precedence over these credentials.`apiKey(String)`

- Parameters:
`vertexCredentials`

- The Vertex AI credentials.- Returns:
- This builder.

-
### build

Builds theinstance.`Gemini`

- Returns:
- A new
instance.`Gemini`

- Throws:

- if modelName is null.[NullPointerException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/NullPointerException.html)


-


---

<!-- DOCUMENTO FUSIONADO: basellmconnectionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/BaseLlmConnection.html -->

# Interface BaseLlmConnection

- All Known Implementing Classes:
[GeminiLlmConnection](GeminiLlmConnection.html)

public interface BaseLlmConnection

The base class for a live model connection.

-
## Method Summary

Modifier and TypeMethodDescription`void`

[close](#close())()Closes the connection.`void`

Closes the connection with an error.`io.reactivex.rxjava3.core.Flowable`

< [LlmResponse](LlmResponse.html)>[receive](#receive())()Receives the model responses.`io.reactivex.rxjava3.core.Completable`

[sendContent](#sendContent(com.google.genai.types.Content))(com.google.genai.types.Content content) Sends a user content to the model.`io.reactivex.rxjava3.core.Completable`

[sendHistory](#sendHistory(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.Content> history)Sends the conversation history to the model.`io.reactivex.rxjava3.core.Completable`

[sendRealtime](#sendRealtime(com.google.genai.types.Blob))(com.google.genai.types.Blob blob) Sends a chunk of audio or a frame of video to the model in realtime.

-
## Method Details

-
### sendHistory

Sends the conversation history to the model.You call this method right after setting up the model connection. The model will respond if the last content is from user, otherwise it will wait for new user input before responding.

-
### sendContent

io.reactivex.rxjava3.core.Completable sendContent(com.google.genai.types.Content content) Sends a user content to the model.The model will respond immediately upon receiving the content. If you send function responses, all parts in the content should be function responses.

-
### sendRealtime

io.reactivex.rxjava3.core.Completable sendRealtime(com.google.genai.types.Blob blob) Sends a chunk of audio or a frame of video to the model in realtime.The model may not respond immediately upon receiving the blob. It will do voice activity detection and decide when to respond.

-
### receive

io.reactivex.rxjava3.core.Flowable<[LlmResponse](LlmResponse.html)> receive()Receives the model responses. -
### close

void close()Closes the connection. -
### close

Closes the connection with an error.

-


---

<!-- DOCUMENTO FUSIONADO: claudehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/Claude.html -->

# Class Claude

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.models.BaseLlm](BaseLlm.html)

com.google.adk.models.Claude

Represents the Claude Generative AI model by Anthropic.

This class provides methods for interacting with Claude models. Streaming and live connections are not currently supported for Claude.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[connect](#connect(com.google.adk.models.LlmRequest))( [LlmRequest](LlmRequest.html)llmRequest)Creates a live connection to the LLM.`io.reactivex.rxjava3.core.Flowable`

< [LlmResponse](LlmResponse.html)>[generateContent](#generateContent(com.google.adk.models.LlmRequest,boolean))( [LlmRequest](LlmRequest.html)llmRequest, boolean stream)Generates one content from the given LLM request and tools.

-
## Constructor Details

-
### Claude

Constructs a new Claude instance.- Parameters:
`modelName`

- The name of the Claude model to use (e.g., "claude-3-opus-20240229").`anthropicClient`

- The Anthropic API client instance.

-
### Claude

public Claude( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)modelName, com.anthropic.client.AnthropicClient anthropicClient, int maxTokens)

-
-
## Method Details

-
### generateContent

public io.reactivex.rxjava3.core.Flowable<[LlmResponse](LlmResponse.html)> generateContent( [LlmRequest](LlmRequest.html)llmRequest, boolean stream)Description copied from class:[BaseLlm](BaseLlm.html#generateContent(com.google.adk.models.LlmRequest,boolean))Generates one content from the given LLM request and tools.- Specified by:

in class[generateContent](BaseLlm.html#generateContent(com.google.adk.models.LlmRequest,boolean))[BaseLlm](BaseLlm.html)- Parameters:
`llmRequest`

- The LLM request containing the input prompt and parameters.`stream`

- A boolean flag indicating whether to stream the response.- Returns:
- A Flowable of LlmResponses. For non-streaming calls, it will only yield one LlmResponse. For streaming calls, it may yield more than one LlmResponse, but all yielded LlmResponses should be treated as one content by merging their parts.

-
### connect

Description copied from class:[BaseLlm](BaseLlm.html#connect(com.google.adk.models.LlmRequest))Creates a live connection to the LLM.

-


---

<!-- DOCUMENTO FUSIONADO: vertexcredentialsbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/VertexCredentials.Builder.html -->

# Class VertexCredentials.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.VertexCredentials.Builder

- Enclosing class:
[VertexCredentials](VertexCredentials.html)

Builder for

[.](VertexCredentials.html)`VertexCredentials`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[VertexCredentials](VertexCredentials.html)[build](#build())()`abstract`

[VertexCredentials.Builder](VertexCredentials.Builder.html)[setCredentials](#setCredentials(com.google.auth.oauth2.GoogleCredentials))(com.google.auth.oauth2.GoogleCredentials value) `abstract`

[VertexCredentials.Builder](VertexCredentials.Builder.html)[setCredentials](#setCredentials(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.auth.oauth2.GoogleCredentials> value)`abstract`

[VertexCredentials.Builder](VertexCredentials.Builder.html)[setLocation](#setLocation(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)value)`abstract`

[VertexCredentials.Builder](VertexCredentials.Builder.html)[setLocation](#setLocation(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> value)`abstract`

[VertexCredentials.Builder](VertexCredentials.Builder.html)[setProject](#setProject(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)value)`abstract`

[VertexCredentials.Builder](VertexCredentials.Builder.html)[setProject](#setProject(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> value)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### setProject

-
### setProject

-
### setLocation

-
### setLocation

-
### setCredentials

public abstract[VertexCredentials.Builder](VertexCredentials.Builder.html)setCredentials( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.auth.oauth2.GoogleCredentials> value) -
### setCredentials

public abstract[VertexCredentials.Builder](VertexCredentials.Builder.html)setCredentials(@Nullable com.google.auth.oauth2.GoogleCredentials value) -
### build


-


---

<!-- DOCUMENTO FUSIONADO: llmrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/LlmRequest.html -->

# Class LlmRequest

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.JsonBaseModel](../JsonBaseModel.html)

com.google.adk.models.LlmRequest

Represents a request to be sent to the LLM.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[LlmRequest.Builder](LlmRequest.Builder.html)[builder](#builder())()`abstract`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GenerateContentConfig> [config](#config())()Returns the configuration for content generation.`abstract`

[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.Content> [contents](#contents())()Returns the list of content sent to the LLM.returns the first system instruction text from the request if present.`com.google.common.collect.ImmutableList`

< [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>Returns all system instruction texts from the request as an immutable list.`abstract com.google.genai.types.LiveConnectConfig`

Returns the configuration for live connections.[model](#model())()Returns the name of the LLM model to be used.`abstract`

[LlmRequest.Builder](LlmRequest.Builder.html)[tools](#tools())()Returns a map of tools available to the LLM.### Methods inherited from class com.google.adk.

[JsonBaseModel](../JsonBaseModel.html)[fromJsonNode](../JsonBaseModel.html#fromJsonNode(com.fasterxml.jackson.databind.JsonNode,java.lang.Class)),[fromJsonString](../JsonBaseModel.html#fromJsonString(java.lang.String,java.lang.Class)),[getMapper](../JsonBaseModel.html#getMapper()),[toJson](../JsonBaseModel.html#toJson()),[toJsonNode](../JsonBaseModel.html#toJsonNode(java.lang.Object)),[toJsonString](../JsonBaseModel.html#toJsonString(java.lang.Object))

-
## Constructor Details

-
### LlmRequest

public LlmRequest()

-
-
## Method Details

-
### model

-
### contents

Returns the list of content sent to the LLM.- Returns:
- A list of
`Content`

objects.

-
### config

Returns the configuration for content generation.- Returns:
- An optional
`GenerateContentConfig`

object containing the generation settings.

-
### liveConnectConfig

public abstract com.google.genai.types.LiveConnectConfig liveConnectConfig()Returns the configuration for live connections. Populated using the RunConfig in the InvocationContext.- Returns:
- An optional
`LiveConnectConfig`

object containing the live connection settings.

-
### tools

-
### getFirstSystemInstruction

-
### getSystemInstructions

Returns all system instruction texts from the request as an immutable list. -
### builder

-
### toBuilder


-


---

<!-- DOCUMENTO FUSIONADO: llmrequestbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/LlmRequest.Builder.html -->

# Class LlmRequest.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.LlmRequest.Builder

- Enclosing class:
[LlmRequest](LlmRequest.html)

Builder for constructing

[instances.](LlmRequest.html)`LlmRequest`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`final`

[LlmRequest.Builder](LlmRequest.Builder.html)[appendInstructions](#appendInstructions(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> instructions)`final`

[LlmRequest.Builder](LlmRequest.Builder.html)[appendTools](#appendTools(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[BaseTool](../tools/BaseTool.html)> tools)`abstract`

[LlmRequest](LlmRequest.html)[build](#build())()`abstract`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GenerateContentConfig> [config](#config())()`abstract`

[LlmRequest.Builder](LlmRequest.Builder.html)[config](#config(com.google.genai.types.GenerateContentConfig))(com.google.genai.types.GenerateContentConfig config) `abstract`

[LlmRequest.Builder](LlmRequest.Builder.html)`abstract`

[LlmRequest.Builder](LlmRequest.Builder.html)[liveConnectConfig](#liveConnectConfig(com.google.genai.types.LiveConnectConfig))(com.google.genai.types.LiveConnectConfig liveConnectConfig) `abstract`

[LlmRequest.Builder](LlmRequest.Builder.html)`final`

[LlmRequest.Builder](LlmRequest.Builder.html)[outputSchema](#outputSchema(com.google.genai.types.Schema))(com.google.genai.types.Schema schema) Sets the output schema for the LLM response.

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### model

-
### contents

@CanIgnoreReturnValue public abstract[LlmRequest.Builder](LlmRequest.Builder.html)contents( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.Content> contents) -
### config

@CanIgnoreReturnValue public abstract[LlmRequest.Builder](LlmRequest.Builder.html)config(com.google.genai.types.GenerateContentConfig config) -
### config

-
### liveConnectConfig

@CanIgnoreReturnValue public abstract[LlmRequest.Builder](LlmRequest.Builder.html)liveConnectConfig(com.google.genai.types.LiveConnectConfig liveConnectConfig) -
### appendInstructions

-
### appendTools

-
### outputSchema

@CanIgnoreReturnValue public final[LlmRequest.Builder](LlmRequest.Builder.html)outputSchema(com.google.genai.types.Schema schema) Sets the output schema for the LLM response. If set, The output content will always be a JSON string that conforms to the schema. -
### build


-


---

<!-- DOCUMENTO FUSIONADO: llmresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/LlmResponse.html -->

# Class LlmResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.JsonBaseModel](../JsonBaseModel.html)

com.google.adk.models.LlmResponse

Represents a response received from the LLM.

-
## Nested Class Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[LlmResponse.Builder](LlmResponse.Builder.html)[builder](#builder())()`abstract`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Content> [content](#content())()Returns the content of the first candidate in the response, if available.`static`

[LlmResponse](LlmResponse.html)[create](#create(com.google.genai.types.GenerateContentResponse))(com.google.genai.types.GenerateContentResponse response) `static`

[LlmResponse](LlmResponse.html)`abstract`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FinishReason> Error code if the response is an error.Error message if the response is an error.`abstract`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GroundingMetadata> Returns the grounding metadata of the first candidate in the response, if available.Indicates that LLM was interrupted when generating the content.[partial](#partial())()Indicates whether the text content is part of a unfinished text stream.`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)Indicates whether the response from the model is complete.`abstract`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GenerateContentResponseUsageMetadata> Usage metadata about the response(s).### Methods inherited from class com.google.adk.

[JsonBaseModel](../JsonBaseModel.html)[fromJsonNode](../JsonBaseModel.html#fromJsonNode(com.fasterxml.jackson.databind.JsonNode,java.lang.Class)),[fromJsonString](../JsonBaseModel.html#fromJsonString(java.lang.String,java.lang.Class)),[getMapper](../JsonBaseModel.html#getMapper()),[toJson](../JsonBaseModel.html#toJson()),[toJsonNode](../JsonBaseModel.html#toJsonNode(java.lang.Object)),[toJsonString](../JsonBaseModel.html#toJsonString(java.lang.Object))

-
## Method Details

-
### content

Returns the content of the first candidate in the response, if available.- Returns:
- An
`Content`

of the first`Candidate`

in the`GenerateContentResponse`

if the response contains at least one candidate., or an empty optional if no candidates are present in the response.

-
### groundingMetadata

-
### partial

-
### turnComplete

-
### errorCode

Error code if the response is an error. Code varies by model. -
### errorMessage

-
### interrupted

-
### usageMetadata

public abstract[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GenerateContentResponseUsageMetadata> usageMetadata()Usage metadata about the response(s). -
### toBuilder

-
### builder

-
### create

-
### create


-


---

<!-- DOCUMENTO FUSIONADO: geminihtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/Gemini.html -->

# Class Gemini

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.models.BaseLlm](BaseLlm.html)

com.google.adk.models.Gemini

Represents the Gemini Generative AI model.

This class provides methods for interacting with the Gemini model, including standard request-response generation and establishing persistent bidirectional connections.

-
## Nested Class Summary

-
## Constructor Summary

ConstructorDescription[Gemini](#%3Cinit%3E(java.lang.String,com.google.adk.models.VertexCredentials))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)modelName,[VertexCredentials](VertexCredentials.html)vertexCredentials)Constructs a new Gemini instance with a Google Gemini API key.Constructs a new Gemini instance.Constructs a new Gemini instance with a Google Gemini API key. -
## Method Summary

Modifier and TypeMethodDescription`static`

[Gemini.Builder](Gemini.Builder.html)[builder](#builder())()Returns a new Builder instance for constructing Gemini objects.[connect](#connect(com.google.adk.models.LlmRequest))( [LlmRequest](LlmRequest.html)llmRequest)Creates a live connection to the LLM.`io.reactivex.rxjava3.core.Flowable`

< [LlmResponse](LlmResponse.html)>[generateContent](#generateContent(com.google.adk.models.LlmRequest,boolean))( [LlmRequest](LlmRequest.html)llmRequest, boolean stream)Generates one content from the given LLM request and tools.

-
## Constructor Details

-
### Gemini

Constructs a new Gemini instance.- Parameters:
`modelName`

- The name of the Gemini model to use (e.g., "gemini-2.0-flash").`apiClient`

- The genai`Client`

instance for making API calls.

-
### Gemini

-
### Gemini

Constructs a new Gemini instance with a Google Gemini API key.- Parameters:
`modelName`

- The name of the Gemini model to use (e.g., "gemini-2.0-flash").`vertexCredentials`

- The Vertex AI credentials to access the Gemini model.


-
-
## Method Details

-
### builder

Returns a new Builder instance for constructing Gemini objects. Note that when building a Gemini object, at least one of apiKey, vertexCredentials, or an explicit apiClient must be set. If multiple are set, the explicit apiClient will take precedence.- Returns:
- A new
.`Gemini.Builder`


-
### generateContent

public io.reactivex.rxjava3.core.Flowable<[LlmResponse](LlmResponse.html)> generateContent( [LlmRequest](LlmRequest.html)llmRequest, boolean stream)Description copied from class:[BaseLlm](BaseLlm.html#generateContent(com.google.adk.models.LlmRequest,boolean))Generates one content from the given LLM request and tools.- Specified by:

in class[generateContent](BaseLlm.html#generateContent(com.google.adk.models.LlmRequest,boolean))[BaseLlm](BaseLlm.html)- Parameters:
`llmRequest`

- The LLM request containing the input prompt and parameters.`stream`

- A boolean flag indicating whether to stream the response.- Returns:
- A Flowable of LlmResponses. For non-streaming calls, it will only yield one LlmResponse. For streaming calls, it may yield more than one LlmResponse, but all yielded LlmResponses should be treated as one content by merging their parts.

-
### connect

Description copied from class:[BaseLlm](BaseLlm.html#connect(com.google.adk.models.LlmRequest))Creates a live connection to the LLM.

-


---

<!-- DOCUMENTO FUSIONADO: geminillmconnectionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/GeminiLlmConnection.html -->

# Class GeminiLlmConnection

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.GeminiLlmConnection

- All Implemented Interfaces:
[BaseLlmConnection](BaseLlmConnection.html)

Manages a persistent, bidirectional connection to the Gemini model via WebSockets for real-time
interaction.

This connection allows sending conversation history, individual messages, function responses, and real-time media blobs (like audio chunks) while continuously receiving responses from the model.

-
## Method Summary

Modifier and TypeMethodDescription`void`

[close](#close())()Closes the connection.`void`

Closes the connection with an error.`io.reactivex.rxjava3.core.Flowable`

< [LlmResponse](LlmResponse.html)>[receive](#receive())()Receives the model responses.`io.reactivex.rxjava3.core.Completable`

[sendContent](#sendContent(com.google.genai.types.Content))(com.google.genai.types.Content content) Sends a user content to the model.`io.reactivex.rxjava3.core.Completable`

[sendHistory](#sendHistory(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.Content> history)Sends the conversation history to the model.`io.reactivex.rxjava3.core.Completable`

[sendRealtime](#sendRealtime(com.google.genai.types.Blob))(com.google.genai.types.Blob blob) Sends a chunk of audio or a frame of video to the model in realtime.

-
## Method Details

-
### sendHistory

public io.reactivex.rxjava3.core.Completable sendHistory( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.Content> history)Description copied from interface:[BaseLlmConnection](BaseLlmConnection.html#sendHistory(java.util.List))Sends the conversation history to the model.You call this method right after setting up the model connection. The model will respond if the last content is from user, otherwise it will wait for new user input before responding.

- Specified by:

in interface[sendHistory](BaseLlmConnection.html#sendHistory(java.util.List))[BaseLlmConnection](BaseLlmConnection.html)

-
### sendContent

public io.reactivex.rxjava3.core.Completable sendContent(com.google.genai.types.Content content) Description copied from interface:[BaseLlmConnection](BaseLlmConnection.html#sendContent(com.google.genai.types.Content))Sends a user content to the model.The model will respond immediately upon receiving the content. If you send function responses, all parts in the content should be function responses.

- Specified by:

in interface[sendContent](BaseLlmConnection.html#sendContent(com.google.genai.types.Content))[BaseLlmConnection](BaseLlmConnection.html)

-
### sendRealtime

public io.reactivex.rxjava3.core.Completable sendRealtime(com.google.genai.types.Blob blob) Description copied from interface:[BaseLlmConnection](BaseLlmConnection.html#sendRealtime(com.google.genai.types.Blob))Sends a chunk of audio or a frame of video to the model in realtime.The model may not respond immediately upon receiving the blob. It will do voice activity detection and decide when to respond.

- Specified by:

in interface[sendRealtime](BaseLlmConnection.html#sendRealtime(com.google.genai.types.Blob))[BaseLlmConnection](BaseLlmConnection.html)

-
### receive

Description copied from interface:[BaseLlmConnection](BaseLlmConnection.html#receive())Receives the model responses.- Specified by:

in interface[receive](BaseLlmConnection.html#receive())[BaseLlmConnection](BaseLlmConnection.html)

-
### close

public void close()Description copied from interface:[BaseLlmConnection](BaseLlmConnection.html#close())Closes the connection.- Specified by:

in interface[close](BaseLlmConnection.html#close())[BaseLlmConnection](BaseLlmConnection.html)

-
### close

Description copied from interface:[BaseLlmConnection](BaseLlmConnection.html#close(java.lang.Throwable))Closes the connection with an error.- Specified by:

in interface[close](BaseLlmConnection.html#close(java.lang.Throwable))[BaseLlmConnection](BaseLlmConnection.html)


-


---

<!-- DOCUMENTO FUSIONADO: llmresponsebuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/LlmResponse.Builder.html -->

# Class LlmResponse.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.models.LlmResponse.Builder

- Enclosing class:
[LlmResponse](LlmResponse.html)

Builder for constructing

[instances.](LlmResponse.html)`LlmResponse`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[build](#build())()`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[content](#content(com.google.genai.types.Content))(com.google.genai.types.Content content) `abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[errorCode](#errorCode(com.google.genai.types.FinishReason))(com.google.genai.types.FinishReason errorCode) `abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[errorMessage](#errorMessage(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)errorMessage)`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[errorMessage](#errorMessage(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> errorMessage)`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[groundingMetadata](#groundingMetadata(com.google.genai.types.GroundingMetadata))(com.google.genai.types.GroundingMetadata groundingMetadata) `abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[groundingMetadata](#groundingMetadata(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GroundingMetadata> groundingMetadata)`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[interrupted](#interrupted(java.lang.Boolean))( [Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)interrupted)`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[interrupted](#interrupted(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> interrupted)`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)`final`

[LlmResponse.Builder](LlmResponse.Builder.html)[response](#response(com.google.genai.types.GenerateContentResponse))(com.google.genai.types.GenerateContentResponse response) `abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[turnComplete](#turnComplete(java.lang.Boolean))( [Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)turnComplete)`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[turnComplete](#turnComplete(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> turnComplete)`abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[usageMetadata](#usageMetadata(com.google.genai.types.GenerateContentResponseUsageMetadata))(com.google.genai.types.GenerateContentResponseUsageMetadata usageMetadata) `abstract`

[LlmResponse.Builder](LlmResponse.Builder.html)[usageMetadata](#usageMetadata(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GenerateContentResponseUsageMetadata> usageMetadata)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### content

-
### interrupted

-
### interrupted

-
### groundingMetadata

public abstract[LlmResponse.Builder](LlmResponse.Builder.html)groundingMetadata(@Nullable com.google.genai.types.GroundingMetadata groundingMetadata) -
### groundingMetadata

public abstract[LlmResponse.Builder](LlmResponse.Builder.html)groundingMetadata( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GroundingMetadata> groundingMetadata) -
### partial

-
### partial

-
### turnComplete

-
### turnComplete

-
### errorCode

public abstract[LlmResponse.Builder](LlmResponse.Builder.html)errorCode(@Nullable com.google.genai.types.FinishReason errorCode) -
### errorCode

public abstract[LlmResponse.Builder](LlmResponse.Builder.html)errorCode( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FinishReason> errorCode) -
### errorMessage

-
### errorMessage

-
### usageMetadata

public abstract[LlmResponse.Builder](LlmResponse.Builder.html)usageMetadata(@Nullable com.google.genai.types.GenerateContentResponseUsageMetadata usageMetadata) -
### usageMetadata

public abstract[LlmResponse.Builder](LlmResponse.Builder.html)usageMetadata( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GenerateContentResponseUsageMetadata> usageMetadata) -
### response

@CanIgnoreReturnValue public final[LlmResponse.Builder](LlmResponse.Builder.html)response(com.google.genai.types.GenerateContentResponse response) -
### build


-
