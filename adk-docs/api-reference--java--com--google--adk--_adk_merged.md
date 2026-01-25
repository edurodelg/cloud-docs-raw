---
merged_at: 2026-01-25T03:28:16.249054
merged_files: 7
---

# Documentos Fusionados

Este archivo contiene 7 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/package-summary.html -->

# Package com.google.adk

package com.google.adk

-
ClassDescriptionThe base class for the types that needs JSON serialization/deserialization capability.Utility class for validating schemas.Utility class for capturing and reporting telemetry data within the ADK.Tracks the current ADK version.


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/package-tree.html -->

# Hierarchy For Package com.google.adk

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk
Hierarchy For Package com.google.adk
Package Hierarchies:
All Packages
Class Hierarchy
java.lang.
Object
com.google.adk.
JsonBaseModel
com.google.adk.
SchemaUtils
com.google.adk.
Telemetry
com.google.adk.
Version


---

<!-- DOCUMENTO FUSIONADO: versionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/Version.html -->

# Class Version

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.Version

Tracks the current ADK version. Useful for tracking headers. Kept as a string literal to avoid
coupling with the build system.

-
## Field Summary

-
## Method Summary


-
## Field Details

-
### JAVA_ADK_VERSION

- See Also:


-


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/package-use.html -->

# Uses of Packagecom.google.adk

# Uses of Package

com.google.adk

Package

Description

-
ClassDescriptionThe base class for the types that needs JSON serialization/deserialization capability.
-
ClassDescriptionThe base class for the types that needs JSON serialization/deserialization capability.
-
ClassDescriptionThe base class for the types that needs JSON serialization/deserialization capability.
-
ClassDescriptionThe base class for the types that needs JSON serialization/deserialization capability.
-
ClassDescriptionThe base class for the types that needs JSON serialization/deserialization capability.
-
ClassDescriptionThe base class for the types that needs JSON serialization/deserialization capability.


---

<!-- DOCUMENTO FUSIONADO: jsonbasemodelhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/JsonBaseModel.html -->

# Class JsonBaseModel

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.JsonBaseModel

- Direct Known Subclasses:

,[AdkWebServer.RunEvalResult](web/AdkWebServer.RunEvalResult.html)

,[Event](events/Event.html)

,[LiveRequest](agents/LiveRequest.html)

,[LlmRequest](models/LlmRequest.html)

,[LlmResponse](models/LlmResponse.html)[Session](sessions/Session.html)

The base class for the types that needs JSON serialization/deserialization capability.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static <T extends`

[JsonBaseModel](JsonBaseModel.html)>

T[fromJsonNode](#fromJsonNode(com.fasterxml.jackson.databind.JsonNode,java.lang.Class))(com.fasterxml.jackson.databind.JsonNode jsonNode, [Class](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Class.html)<T> clazz)Deserializes a JsonNode to an object of the given type.`static <T extends`

[JsonBaseModel](JsonBaseModel.html)>

T[fromJsonString](#fromJsonString(java.lang.String,java.lang.Class))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)jsonString,[Class](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Class.html)<T> clazz)Deserializes a Json string to an object of the given type.`static com.fasterxml.jackson.databind.ObjectMapper`

[toJson](#toJson())()`protected static com.fasterxml.jackson.databind.JsonNode`

[toJsonNode](#toJsonNode(java.lang.Object))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)object)Serializes an object to a JsonNode.`protected static`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[toJsonString](#toJsonString(java.lang.Object))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)object)Serializes an object to a Json string.

-
## Constructor Details

-
### JsonBaseModel

public JsonBaseModel()

-
-
## Method Details

-
### toJsonString

-
### getMapper

public static com.fasterxml.jackson.databind.ObjectMapper getMapper() -
### toJson

-
### toJsonNode

Serializes an object to a JsonNode. -
### fromJsonString

Deserializes a Json string to an object of the given type. -
### fromJsonNode

public static <T extends[JsonBaseModel](JsonBaseModel.html)> T fromJsonNode(com.fasterxml.jackson.databind.JsonNode jsonNode, [Class](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Class.html)<T> clazz)Deserializes a JsonNode to an object of the given type.

-


---

<!-- DOCUMENTO FUSIONADO: schemautilshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/SchemaUtils.html -->

# Class SchemaUtils

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.SchemaUtils

Utility class for validating schemas.

-
## Method Summary

Modifier and TypeMethodDescription`static void`

[validateMapOnSchema](#validateMapOnSchema(java.util.Map,com.google.genai.types.Schema,java.lang.Boolean))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> args, com.google.genai.types.Schema schema,[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)isInput)Validates a map against a schema.[validateOutputSchema](#validateOutputSchema(java.lang.String,com.google.genai.types.Schema))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)output, com.google.genai.types.Schema schema)Validates an output string against a schema.

-
## Method Details

-
### validateMapOnSchema

public static void validateMapOnSchema( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> args, com.google.genai.types.Schema schema,[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)isInput)Validates a map against a schema.- Parameters:
`args`

- The map to validate.`schema`

- The schema to validate against.`isInput`

- Whether the map is an input or output.- Throws:

- If the map does not match the schema.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)

-
### validateOutputSchema

public static[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> validateOutputSchema( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)output, com.google.genai.types.Schema schema) throws com.fasterxml.jackson.core.JsonProcessingExceptionValidates an output string against a schema.- Parameters:
`output`

- The output string to validate.`schema`

- The schema to validate against.- Returns:
- The output map.
- Throws:

- If the output string does not match the schema.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)`com.fasterxml.jackson.core.JsonProcessingException`

- If the output string cannot be parsed.


-


---

<!-- DOCUMENTO FUSIONADO: telemetryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/Telemetry.html -->

# Class Telemetry

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.Telemetry

Utility class for capturing and reporting telemetry data within the ADK. This class provides
methods to trace various aspects of the agent's execution, including tool calls, tool responses,
LLM interactions, and data handling. It leverages OpenTelemetry for tracing and logging for
detailed information. These traces can then be exported through the ADK Dev Server UI.

-
## Method Summary

Modifier and TypeMethodDescription`static io.opentelemetry.api.trace.Tracer`

Gets the tracer.`static void`

[traceCallLlm](#traceCallLlm(com.google.adk.agents.InvocationContext,java.lang.String,com.google.adk.models.LlmRequest,com.google.adk.models.LlmResponse))( [InvocationContext](agents/InvocationContext.html)invocationContext,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId,[LlmRequest](models/LlmRequest.html)llmRequest,[LlmResponse](models/LlmResponse.html)llmResponse)Traces a call to the LLM.`static void`

[traceSendData](#traceSendData(com.google.adk.agents.InvocationContext,java.lang.String,java.util.List))( [InvocationContext](agents/InvocationContext.html)invocationContext,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.Content> data)Traces the sending of data (history or new content) to the agent/model.`static void`

[traceToolCall](#traceToolCall(java.util.Map))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> args)Traces tool call arguments.`static void`

[traceToolResponse](#traceToolResponse(com.google.adk.agents.InvocationContext,java.lang.String,com.google.adk.events.Event))( [InvocationContext](agents/InvocationContext.html)invocationContext,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId,[Event](events/Event.html)functionResponseEvent)Traces tool response event.

-
## Method Details

-
### traceToolCall

-
### traceToolResponse

public static void traceToolResponse( [InvocationContext](agents/InvocationContext.html)invocationContext,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId,[Event](events/Event.html)functionResponseEvent)Traces tool response event.- Parameters:
`invocationContext`

- The invocation context for the current agent run.`eventId`

- The ID of the event.`functionResponseEvent`

- The function response event.

-
### traceCallLlm

public static void traceCallLlm( [InvocationContext](agents/InvocationContext.html)invocationContext,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId,[LlmRequest](models/LlmRequest.html)llmRequest,[LlmResponse](models/LlmResponse.html)llmResponse)Traces a call to the LLM.- Parameters:
`invocationContext`

- The invocation context.`eventId`

- The ID of the event associated with this LLM call/response.`llmRequest`

- The LLM request object.`llmResponse`

- The LLM response object.

-
### traceSendData

public static void traceSendData( [InvocationContext](agents/InvocationContext.html)invocationContext,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.Content> data)Traces the sending of data (history or new content) to the agent/model.- Parameters:
`invocationContext`

- The invocation context.`eventId`

- The ID of the event, if applicable.`data`

- A list of content objects being sent.

-
### getTracer

public static io.opentelemetry.api.trace.Tracer getTracer()Gets the tracer.- Returns:
- The tracer.


-
