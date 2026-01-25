---
merged_at: 2026-01-25T03:28:16.298979
merged_files: 5
---

# Documentos Fusionados

Este archivo contiene 5 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/retrieval/package-use.html -->

# Uses of Packagecom.google.adk.tools.retrieval

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.tools.retrieval
Uses of Package
com.google.adk.tools.retrieval
Packages that use
com.google.adk.tools.retrieval
Package
Description
com.google.adk.tools.retrieval
Classes in
com.google.adk.tools.retrieval
used by
com.google.adk.tools.retrieval
Class
Description
BaseRetrievalTool
Base class for retrieval tools.


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/retrieval/package-tree.html -->

# Hierarchy For Package com.google.adk.tools.retrieval

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.tools.
[BaseTool](../BaseTool.html)- com.google.adk.tools.retrieval.
[BaseRetrievalTool](BaseRetrievalTool.html)- com.google.adk.tools.retrieval.
[VertexAiRagRetrieval](VertexAiRagRetrieval.html)

- com.google.adk.tools.retrieval.

- com.google.adk.tools.retrieval.

- com.google.adk.tools.


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/retrieval/package-summary.html -->

# Package com.google.adk.tools.retrieval

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.tools.retrieval
Contents
Hide sidebar
❮
❯
Show sidebar
Description
Related Packages
Classes and Interfaces
Package com.google.adk.tools.retrieval
package
com.google.adk.tools.retrieval
Related Packages
Package
Description
com.google.adk.tools
com.google.adk.tools.applicationintegrationtoolset
com.google.adk.tools.mcp
Classes
Class
Description
BaseRetrievalTool
Base class for retrieval tools.
VertexAiRagRetrieval
A retrieval tool that fetches context from Vertex AI RAG.


---

<!-- DOCUMENTO FUSIONADO: baseretrievaltoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/retrieval/BaseRetrievalTool.html -->

# Class BaseRetrievalTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](../BaseTool.html)

com.google.adk.tools.retrieval.BaseRetrievalTool

- Direct Known Subclasses:
[VertexAiRagRetrieval](VertexAiRagRetrieval.html)

Base class for retrieval tools.

-
## Constructor Summary

ConstructorDescription[BaseRetrievalTool](#%3Cinit%3E(java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)name,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description)[BaseRetrievalTool](#%3Cinit%3E(java.lang.String,java.lang.String,boolean))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)name,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description, boolean isLongRunning) -
## Method Summary

Modifier and TypeMethodDescription[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FunctionDeclaration> Gets the`FunctionDeclaration`

representation of this tool.### Methods inherited from class com.google.adk.tools.

[BaseTool](../BaseTool.html)[description](../BaseTool.html#description()),[longRunning](../BaseTool.html#longRunning()),[name](../BaseTool.html#name()),[processLlmRequest](../BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext)),[runAsync](../BaseTool.html#runAsync(java.util.Map,com.google.adk.tools.ToolContext))

-
## Constructor Details

-
### BaseRetrievalTool

-
### BaseRetrievalTool


-
-
## Method Details

-
### declaration

Description copied from class:[BaseTool](../BaseTool.html#declaration())Gets the`FunctionDeclaration`

representation of this tool.- Overrides:

in class[declaration](../BaseTool.html#declaration())[BaseTool](../BaseTool.html)


-


---

<!-- DOCUMENTO FUSIONADO: vertexairagretrievalhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/retrieval/VertexAiRagRetrieval.html -->

# Class VertexAiRagRetrieval

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](../BaseTool.html)

[com.google.adk.tools.retrieval.BaseRetrievalTool](BaseRetrievalTool.html)

com.google.adk.tools.retrieval.VertexAiRagRetrieval

A retrieval tool that fetches context from Vertex AI RAG.

This tool allows to retrieve relevant information based on a query using Vertex AI RAG service. It supports configuration of rag resources and a vector distance threshold.

-
## Constructor Summary

ConstructorDescription[VertexAiRagRetrieval](#%3Cinit%3E(java.lang.String,java.lang.String,com.google.cloud.aiplatform.v1.VertexRagServiceClient,java.lang.String,java.util.List,java.lang.Double))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)name,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description, com.google.cloud.aiplatform.v1.VertexRagServiceClient vertexRagServiceClient,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)parent,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.cloud.aiplatform.v1.RetrieveContextsRequest.VertexRagStore.RagResource> ragResources,[Double](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Double.html)vectorDistanceThreshold) -
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Completable`

[processLlmRequest](#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))( [LlmRequest.Builder](../../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](../ToolContext.html)toolContext)Processes the outgoing.`LlmRequest.Builder`

[runAsync](#runAsync(java.util.Map,com.google.adk.tools.ToolContext))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> args,[ToolContext](../ToolContext.html)toolContext)Calls a tool.### Methods inherited from class com.google.adk.tools.retrieval.

[BaseRetrievalTool](BaseRetrievalTool.html)[declaration](BaseRetrievalTool.html#declaration())### Methods inherited from class com.google.adk.tools.

[BaseTool](../BaseTool.html)[description](../BaseTool.html#description()),[longRunning](../BaseTool.html#longRunning()),[name](../BaseTool.html#name())

-
## Constructor Details

-
### VertexAiRagRetrieval

public VertexAiRagRetrieval(@Nonnull [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)name, @Nonnull[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description, @Nonnull com.google.cloud.aiplatform.v1.VertexRagServiceClient vertexRagServiceClient, @Nonnull[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)parent, @Nullable[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.cloud.aiplatform.v1.RetrieveContextsRequest.VertexRagStore.RagResource> ragResources, @Nullable[Double](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Double.html)vectorDistanceThreshold)

-
-
## Method Details

-
### processLlmRequest

@CanIgnoreReturnValue public io.reactivex.rxjava3.core.Completable processLlmRequest( [LlmRequest.Builder](../../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](../ToolContext.html)toolContext)Description copied from class:[BaseTool](../BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))Processes the outgoing.`LlmRequest.Builder`

This implementation adds the current tool's

to the`BaseTool.declaration()`

`GenerateContentConfig`

within the builder. If a tool with function declarations already exists, the current tool's declaration is merged into it. Otherwise, a new tool definition with the current tool's declaration is created. The current tool itself is also added to the builder's internal list of tools. Override this method for processing the outgoing request.- Overrides:

in class[processLlmRequest](../BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))[BaseTool](../BaseTool.html)

-
### runAsync


-
