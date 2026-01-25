---
merged_at: 2026-01-25T03:28:16.149823
merged_files: 18
---

# Documentos Fusionados

Este archivo contiene 18 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: exitlooptoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/ExitLoopTool.html -->

# Class ExitLoopTool

static void

exitLoop(ToolContext toolContext)

clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait, wait, wait


---

<!-- DOCUMENTO FUSIONADO: annotationshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/Annotations.html -->

# Class Annotations

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.Annotations

Annotations for tools.

-
## Nested Class Summary

Modifier and TypeClassDescription`static @interface`

The annotation for binding the 'Schema' input. -
## Method Summary


`static @interface `


---

<!-- DOCUMENTO FUSIONADO: toolcontextbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/ToolContext.Builder.html -->

# Class ToolContext.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.ToolContext.Builder

- Enclosing class:
[ToolContext](ToolContext.html)

Builder for

[.](ToolContext.html)`ToolContext`

-
## Method Summary

Modifier and TypeMethodDescription[actions](#actions(com.google.adk.events.EventActions))( [EventActions](../events/EventActions.html)actions)[build](#build())()[functionCallId](#functionCallId(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)functionCallId)

-
## Method Details

-
### actions

-
### functionCallId

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: annotationsschemahtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/Annotations.Schema.html -->

# Annotation Interface Annotations.Schema

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.tools
Annotations
Schema
Contents
Hide sidebar
❮
❯
Show sidebar
Description
Optional Element Summary
Element Details
name
description
Annotation Interface Annotations.Schema
Enclosing class:
Annotations
@Target
({
METHOD
,
PARAMETER
})
@Retention
(
RUNTIME
)
public static @interface
Annotations.Schema
The annotation for binding the 'Schema' input.
Optional Element Summary
Optional Elements
Modifier and Type
Optional Element
Description
String
description
String
name
Element Details
name
String
name
Default:
""
description
String
description
Default:
""


---

<!-- DOCUMENTO FUSIONADO: toolpredicatehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/ToolPredicate.html -->

# Interface ToolPredicate

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

Functional interface to decide whether a tool should be exposed to the LLM based on the current
context.

-
## Method Summary

Modifier and TypeMethodDescription`boolean`

[test](#test(com.google.adk.tools.BaseTool,java.util.Optional))( [BaseTool](BaseTool.html)tool,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[ReadonlyContext](../agents/ReadonlyContext.html)> readonlyContext)Decides if the given tool is selected.

-
## Method Details

-
### test

Decides if the given tool is selected.- Parameters:
`tool`

- The tool to check.`readonlyContext`

- The current context.- Returns:
- true if the tool should be selected, false otherwise.


-


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/package-summary.html -->

# Package com.google.adk.tools

package com.google.adk.tools

-
ClassDescriptionAgentTool implements a tool that allows an agent to call another agent.Annotations for tools.The annotation for binding the 'Schema' input.The base class for all ADK tools.Base interface for toolsets.A built-in code execution tool that is automatically invoked by Gemini 2 models.Exits the loop.Utility class for function calling.FunctionTool implements a customized function calling tool.A built-in tool that is automatically invoked by Gemini 2 models to retrieve search results from Google Search.A tool that loads artifacts and adds them to the session.A function tool that returns the result asynchronously.ToolContext object provides a structured context for executing tools or functions.Builder for
.`ToolContext`

Functional interface to decide whether a tool should be exposed to the LLM based on the current context.


---

<!-- DOCUMENTO FUSIONADO: agenttoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/AgentTool.html -->

# Class AgentTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](BaseTool.html)

com.google.adk.tools.AgentTool

AgentTool implements a tool that allows an agent to call another agent.

-
## Constructor Summary

-
## Method Summary

### Methods inherited from class com.google.adk.tools.

[BaseTool](BaseTool.html)[description](BaseTool.html#description()),[longRunning](BaseTool.html#longRunning()),[name](BaseTool.html#name()),[processLlmRequest](BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))

-
## Constructor Details

-
### AgentTool


-
-
## Method Details

-
### create

-
### create

-
### declaration

Description copied from class:[BaseTool](BaseTool.html#declaration())Gets the`FunctionDeclaration`

representation of this tool.- Overrides:

in class[declaration](BaseTool.html#declaration())[BaseTool](BaseTool.html)

-
### runAsync


-


---

<!-- DOCUMENTO FUSIONADO: functioncallingutilshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/FunctionCallingUtils.html -->

# Class FunctionCallingUtils

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.FunctionCallingUtils

Utility class for function calling.

-
## Method Summary

Modifier and TypeMethodDescription`static com.google.genai.types.FunctionDeclaration`

[buildFunctionDeclaration](#buildFunctionDeclaration(java.lang.reflect.Method,java.util.List))( [Method](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/reflect/Method.html)func,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> ignoreParams)`static com.google.genai.types.Schema`

[buildSchemaFromType](#buildSchemaFromType(java.lang.reflect.Type))( [Type](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/reflect/Type.html)type)

-
## Method Details

-
### buildFunctionDeclaration

-
### buildSchemaFromType


-


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/package-use.html -->

# Uses of Packagecom.google.adk.tools

# Uses of Package

com.google.adk.tools

Package

Description

-
ClassDescriptionThe base class for all ADK tools.ToolContext object provides a structured context for executing tools or functions.
-
ClassDescriptionThe base class for all ADK tools.ToolContext object provides a structured context for executing tools or functions.
-
-
ClassDescriptionAgentTool implements a tool that allows an agent to call another agent.The base class for all ADK tools.FunctionTool implements a customized function calling tool.A function tool that returns the result asynchronously.ToolContext object provides a structured context for executing tools or functions.Builder for
.`ToolContext`

-
ClassDescriptionThe base class for all ADK tools.Base interface for toolsets.ToolContext object provides a structured context for executing tools or functions.
-
ClassDescriptionThe base class for all ADK tools.Base interface for toolsets.ToolContext object provides a structured context for executing tools or functions.
-
ClassDescriptionThe base class for all ADK tools.ToolContext object provides a structured context for executing tools or functions.


---

<!-- DOCUMENTO FUSIONADO: longrunningfunctiontoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/LongRunningFunctionTool.html -->

# Class LongRunningFunctionTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](BaseTool.html)

[com.google.adk.tools.FunctionTool](FunctionTool.html)

com.google.adk.tools.LongRunningFunctionTool

A function tool that returns the result asynchronously.

-
## Method Summary

Modifier and TypeMethodDescription`static`

[LongRunningFunctionTool](LongRunningFunctionTool.html)`static`

[LongRunningFunctionTool](LongRunningFunctionTool.html)`static`

[LongRunningFunctionTool](LongRunningFunctionTool.html)### Methods inherited from class com.google.adk.tools.

[FunctionTool](FunctionTool.html)[create](FunctionTool.html#create(java.lang.Object,java.lang.reflect.Method)),[declaration](FunctionTool.html#declaration()),[runAsync](FunctionTool.html#runAsync(java.util.Map,com.google.adk.tools.ToolContext))### Methods inherited from class com.google.adk.tools.

[BaseTool](BaseTool.html)[description](BaseTool.html#description()),[longRunning](BaseTool.html#longRunning()),[name](BaseTool.html#name()),[processLlmRequest](BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))

-
## Method Details

-
### create

-
### create

-
### create


-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/package-tree.html -->

# Hierarchy For Package com.google.adk.tools

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.tools.
[Annotations](Annotations.html) - com.google.adk.tools.
[BaseTool](BaseTool.html)- com.google.adk.tools.
[AgentTool](AgentTool.html) - com.google.adk.tools.
[BuiltInCodeExecutionTool](BuiltInCodeExecutionTool.html) - com.google.adk.tools.
[FunctionTool](FunctionTool.html)- com.google.adk.tools.
[LongRunningFunctionTool](LongRunningFunctionTool.html)

- com.google.adk.tools.
- com.google.adk.tools.
[GoogleSearchTool](GoogleSearchTool.html) - com.google.adk.tools.
[LoadArtifactsTool](LoadArtifactsTool.html)

- com.google.adk.tools.
- com.google.adk.tools.
[ExitLoopTool](ExitLoopTool.html) - com.google.adk.tools.
[FunctionCallingUtils](FunctionCallingUtils.html) - com.google.adk.agents.
[ReadonlyContext](../agents/ReadonlyContext.html)- com.google.adk.agents.
[CallbackContext](../agents/CallbackContext.html)- com.google.adk.tools.
[ToolContext](ToolContext.html)

- com.google.adk.tools.

- com.google.adk.agents.
- com.google.adk.tools.
[ToolContext.Builder](ToolContext.Builder.html)

- com.google.adk.tools.

## Interface Hierarchy

- java.lang.
[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)- com.google.adk.tools.
[BaseToolset](BaseToolset.html)

- com.google.adk.tools.
- com.google.adk.tools.
[ToolPredicate](ToolPredicate.html)

## Annotation Interface Hierarchy

- com.google.adk.tools.
[Annotations.Schema](Annotations.Schema.html)(implements java.lang.annotation.[Annotation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Annotation.html))


---

<!-- DOCUMENTO FUSIONADO: functiontoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/FunctionTool.html -->

# Class FunctionTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](BaseTool.html)

com.google.adk.tools.FunctionTool

- Direct Known Subclasses:
[LongRunningFunctionTool](LongRunningFunctionTool.html)

FunctionTool implements a customized function calling tool.

-
## Constructor Summary

ModifierConstructorDescription`protected`

[FunctionTool](#%3Cinit%3E(java.lang.Object,java.lang.reflect.Method,boolean))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)instance,[Method](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/reflect/Method.html)func, boolean isLongRunning) -
## Method Summary

Modifier and TypeMethodDescription`static`

[FunctionTool](FunctionTool.html)`static`

[FunctionTool](FunctionTool.html)`static`

[FunctionTool](FunctionTool.html)`static`

[FunctionTool](FunctionTool.html)[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FunctionDeclaration> Gets the`FunctionDeclaration`

representation of this tool.[runAsync](#runAsync(java.util.Map,com.google.adk.tools.ToolContext))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> args,[ToolContext](ToolContext.html)toolContext)Calls a tool.### Methods inherited from class com.google.adk.tools.

[BaseTool](BaseTool.html)[description](BaseTool.html#description()),[longRunning](BaseTool.html#longRunning()),[name](BaseTool.html#name()),[processLlmRequest](BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))

-
## Constructor Details

-
### FunctionTool


-
-
## Method Details

-
### create

-
### create

-
### create

-
### create

-
### declaration

Description copied from class:[BaseTool](BaseTool.html#declaration())Gets the`FunctionDeclaration`

representation of this tool.- Overrides:

in class[declaration](BaseTool.html#declaration())[BaseTool](BaseTool.html)

-
### runAsync


-


---

<!-- DOCUMENTO FUSIONADO: googlesearchtoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/GoogleSearchTool.html -->

# Class GoogleSearchTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](BaseTool.html)

com.google.adk.tools.GoogleSearchTool

A built-in tool that is automatically invoked by Gemini 2 models to retrieve search results from
Google Search.

This tool operates internally within the model and does not require or perform local code execution.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Completable`

[processLlmRequest](#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)Processes the outgoing.`LlmRequest.Builder`

### Methods inherited from class com.google.adk.tools.

[BaseTool](BaseTool.html)[declaration](BaseTool.html#declaration()),[description](BaseTool.html#description()),[longRunning](BaseTool.html#longRunning()),[name](BaseTool.html#name()),[runAsync](BaseTool.html#runAsync(java.util.Map,com.google.adk.tools.ToolContext))

-
## Constructor Details

-
### GoogleSearchTool

public GoogleSearchTool()

-
-
## Method Details

-
### processLlmRequest

public io.reactivex.rxjava3.core.Completable processLlmRequest( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)Description copied from class:[BaseTool](BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))Processes the outgoing.`LlmRequest.Builder`

This implementation adds the current tool's

to the`BaseTool.declaration()`

`GenerateContentConfig`

within the builder. If a tool with function declarations already exists, the current tool's declaration is merged into it. Otherwise, a new tool definition with the current tool's declaration is created. The current tool itself is also added to the builder's internal list of tools. Override this method for processing the outgoing request.- Overrides:

in class[processLlmRequest](BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))[BaseTool](BaseTool.html)


-


---

<!-- DOCUMENTO FUSIONADO: builtincodeexecutiontoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/BuiltInCodeExecutionTool.html -->

# Class BuiltInCodeExecutionTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](BaseTool.html)

com.google.adk.tools.BuiltInCodeExecutionTool

A built-in code execution tool that is automatically invoked by Gemini 2 models.

This tool operates internally within the model and does not require or perform local code execution.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Completable`

[processLlmRequest](#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)Processes the outgoing.`LlmRequest.Builder`

### Methods inherited from class com.google.adk.tools.

[BaseTool](BaseTool.html)[declaration](BaseTool.html#declaration()),[description](BaseTool.html#description()),[longRunning](BaseTool.html#longRunning()),[name](BaseTool.html#name()),[runAsync](BaseTool.html#runAsync(java.util.Map,com.google.adk.tools.ToolContext))

-
## Constructor Details

-
### BuiltInCodeExecutionTool

public BuiltInCodeExecutionTool()

-
-
## Method Details

-
### processLlmRequest

public io.reactivex.rxjava3.core.Completable processLlmRequest( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)Description copied from class:[BaseTool](BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))Processes the outgoing.`LlmRequest.Builder`

This implementation adds the current tool's

to the`BaseTool.declaration()`

`GenerateContentConfig`

within the builder. If a tool with function declarations already exists, the current tool's declaration is merged into it. Otherwise, a new tool definition with the current tool's declaration is created. The current tool itself is also added to the builder's internal list of tools. Override this method for processing the outgoing request.- Overrides:

in class[processLlmRequest](BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))[BaseTool](BaseTool.html)


-


---

<!-- DOCUMENTO FUSIONADO: toolcontexthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/ToolContext.html -->

# Class ToolContext

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.agents.ReadonlyContext](../agents/ReadonlyContext.html)

[com.google.adk.agents.CallbackContext](../agents/CallbackContext.html)

com.google.adk.tools.ToolContext

ToolContext object provides a structured context for executing tools or functions.

-
## Nested Class Summary

-
## Field Summary

### Fields inherited from class com.google.adk.agents.

[CallbackContext](../agents/CallbackContext.html)[eventActions](../agents/CallbackContext.html#eventActions)### Fields inherited from class com.google.adk.agents.

[ReadonlyContext](../agents/ReadonlyContext.html)[invocationContext](../agents/ReadonlyContext.html#invocationContext) -
## Method Summary

Modifier and TypeMethodDescription[actions](#actions())()`static`

[ToolContext.Builder](ToolContext.Builder.html)[builder](#builder(com.google.adk.agents.InvocationContext))( [InvocationContext](../agents/InvocationContext.html)invocationContext)`void`

[functionCallId](#functionCallId(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)functionCallId)Lists the filenames of the artifacts attached to the current session.`void`

[setActions](#setActions(com.google.adk.events.EventActions))( [EventActions](../events/EventActions.html)actions)### Methods inherited from class com.google.adk.agents.

[CallbackContext](../agents/CallbackContext.html)[eventActions](../agents/CallbackContext.html#eventActions()),[loadArtifact](../agents/CallbackContext.html#loadArtifact(java.lang.String,java.util.Optional)),[saveArtifact](../agents/CallbackContext.html#saveArtifact(java.lang.String,com.google.genai.types.Part)),[state](../agents/CallbackContext.html#state())### Methods inherited from class com.google.adk.agents.

[ReadonlyContext](../agents/ReadonlyContext.html)[agentName](../agents/ReadonlyContext.html#agentName()),[branch](../agents/ReadonlyContext.html#branch()),[events](../agents/ReadonlyContext.html#events()),[invocationId](../agents/ReadonlyContext.html#invocationId()),[sessionId](../agents/ReadonlyContext.html#sessionId()),[userContent](../agents/ReadonlyContext.html#userContent())

-
## Method Details

-
### actions

-
### setActions

-
### functionCallId

-
### functionCallId

-
### listArtifacts

-
### builder

-
### toBuilder


-


---

<!-- DOCUMENTO FUSIONADO: basetoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/BaseTool.html -->

# Class BaseTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.BaseTool

- Direct Known Subclasses:

,[AgentTool](AgentTool.html)

,[BaseRetrievalTool](retrieval/BaseRetrievalTool.html)

,[BuiltInCodeExecutionTool](BuiltInCodeExecutionTool.html)

,[FunctionTool](FunctionTool.html)

,[GoogleSearchTool](GoogleSearchTool.html)

,[IntegrationConnectorTool](applicationintegrationtoolset/IntegrationConnectorTool.html)

,[LoadArtifactsTool](LoadArtifactsTool.html)

,[McpAsyncTool](mcp/McpAsyncTool.html)[McpTool](mcp/McpTool.html)

The base class for all ADK tools.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FunctionDeclaration> Gets the`FunctionDeclaration`

representation of this tool.`boolean`

[name](#name())()`io.reactivex.rxjava3.core.Completable`

[processLlmRequest](#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)Processes the outgoing.`LlmRequest.Builder`

[runAsync](#runAsync(java.util.Map,com.google.adk.tools.ToolContext))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> args,[ToolContext](ToolContext.html)toolContext)Calls a tool.

-
## Constructor Details

-
### BaseTool

-
### BaseTool


-
-
## Method Details

-
### name

-
### description

-
### longRunning

public boolean longRunning() -
### declaration

Gets the`FunctionDeclaration`

representation of this tool. -
### runAsync

-
### processLlmRequest

@CanIgnoreReturnValue public io.reactivex.rxjava3.core.Completable processLlmRequest( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)Processes the outgoing.`LlmRequest.Builder`

This implementation adds the current tool's

to the`declaration()`

`GenerateContentConfig`

within the builder. If a tool with function declarations already exists, the current tool's declaration is merged into it. Otherwise, a new tool definition with the current tool's declaration is created. The current tool itself is also added to the builder's internal list of tools. Override this method for processing the outgoing request.

-


---

<!-- DOCUMENTO FUSIONADO: basetoolsethtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/BaseToolset.html -->

# Interface BaseToolset

- All Superinterfaces:
[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

- All Known Implementing Classes:

,[ApplicationIntegrationToolset](applicationintegrationtoolset/ApplicationIntegrationToolset.html)[McpToolset](mcp/McpToolset.html)

Base interface for toolsets.

-
## Method Summary

Modifier and TypeMethodDescription`void`

[close](#close())()Performs cleanup and releases resources held by the toolset.`io.reactivex.rxjava3.core.Flowable`

< [BaseTool](BaseTool.html)>[getTools](#getTools(com.google.adk.agents.ReadonlyContext))( [ReadonlyContext](../agents/ReadonlyContext.html)readonlyContext)Return all tools in the toolset based on the provided context.`default boolean`

[isToolSelected](#isToolSelected(com.google.adk.tools.BaseTool,java.util.Optional,java.util.Optional))( [BaseTool](BaseTool.html)tool,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[ReadonlyContext](../agents/ReadonlyContext.html)> readonlyContext)Helper method to be used by implementers that returns true if the given tool is in the provided list of tools of if testing against the given ToolPredicate returns true (otherwise false).

-
## Method Details

-
### getTools

Return all tools in the toolset based on the provided context.- Parameters:
`readonlyContext`

- Context used to filter tools available to the agent.- Returns:
- A Single emitting a list of tools available under the specified context.

-
### close

Performs cleanup and releases resources held by the toolset.NOTE: This method is invoked, for example, at the end of an agent server's lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.

- Specified by:

in interface[close](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html#close())[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)- Throws:
[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)

-
### isToolSelected

default boolean isToolSelected( [BaseTool](BaseTool.html)tool,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[ReadonlyContext](../agents/ReadonlyContext.html)> readonlyContext)Helper method to be used by implementers that returns true if the given tool is in the provided list of tools of if testing against the given ToolPredicate returns true (otherwise false).- Parameters:
`tool`

- The tool to check.`toolFilter`

- An Optional containing either a ToolPredicate or a List of tool names.`readonlyContext`

- The current context.- Returns:
- true if the tool is selected.


-


---

<!-- DOCUMENTO FUSIONADO: loadartifactstoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/LoadArtifactsTool.html -->

# Class LoadArtifactsTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](BaseTool.html)

com.google.adk.tools.LoadArtifactsTool

A tool that loads artifacts and adds them to the session.

This tool informs the model about available artifacts and provides their content when requested by the model through a function call.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Completable`

[appendArtifactsToLlmRequest](#appendArtifactsToLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FunctionDeclaration> Gets the`FunctionDeclaration`

representation of this tool.`io.reactivex.rxjava3.core.Completable`

[processLlmRequest](#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)Processes the outgoing.`LlmRequest.Builder`

[runAsync](#runAsync(java.util.Map,com.google.adk.tools.ToolContext))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> args,[ToolContext](ToolContext.html)toolContext)Calls a tool.### Methods inherited from class com.google.adk.tools.

[BaseTool](BaseTool.html)[description](BaseTool.html#description()),[longRunning](BaseTool.html#longRunning()),[name](BaseTool.html#name())

-
## Constructor Details

-
### LoadArtifactsTool

public LoadArtifactsTool()

-
-
## Method Details

-
### declaration

Description copied from class:[BaseTool](BaseTool.html#declaration())Gets the`FunctionDeclaration`

representation of this tool.- Overrides:

in class[declaration](BaseTool.html#declaration())[BaseTool](BaseTool.html)

-
### runAsync

-
### processLlmRequest

public io.reactivex.rxjava3.core.Completable processLlmRequest( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)Description copied from class:[BaseTool](BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))Processes the outgoing.`LlmRequest.Builder`

This implementation adds the current tool's

to the`BaseTool.declaration()`

`GenerateContentConfig`

within the builder. If a tool with function declarations already exists, the current tool's declaration is merged into it. Otherwise, a new tool definition with the current tool's declaration is created. The current tool itself is also added to the builder's internal list of tools. Override this method for processing the outgoing request.- Overrides:

in class[processLlmRequest](BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))[BaseTool](BaseTool.html)

-
### appendArtifactsToLlmRequest

public io.reactivex.rxjava3.core.Completable appendArtifactsToLlmRequest( [LlmRequest.Builder](../models/LlmRequest.Builder.html)llmRequestBuilder,[ToolContext](ToolContext.html)toolContext)

-
