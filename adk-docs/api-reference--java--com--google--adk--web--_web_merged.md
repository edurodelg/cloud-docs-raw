---
merged_at: 2026-01-25T02:21:31.695174
merged_files: 17
---

# Documentos Fusionados

Este archivo contiene 17 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: adkwebserverrunevalrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.RunEvalRequest.html -->

# Class AdkWebServer.RunEvalRequest

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer.RunEvalRequest

- Enclosing class:
[AdkWebServer](AdkWebServer.html)

DTO for POST /apps/{appName}/eval_sets/{evalSetId}/run-eval requests. Contains information for
running evaluations.

-
## Field Summary

-
## Constructor Summary

-
## Method Summary


-
## Field Details

-
### evalIds

-
### evalMetrics


-
-
## Constructor Details

-
### RunEvalRequest

public RunEvalRequest()

-
-
## Method Details

-
### getEvalIds

-
### getEvalMetrics


-


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/package-use.html -->

# Uses of Packagecom.google.adk.web

-
DTO for POST /apps/{appName}/eval_sets/{evalSetId}/add-session requests.

Data Transfer Object (DTO) for POST /run and POST /run-sse requests.

A custom SpanExporter that stores relevant span data.

DTO for the response of GET
/apps/{appName}/users/{userId}/sessions/{sessionId}/events/{eventId}/graph.

WebSocket Handler for the /run_live endpoint.

DTO for POST /apps/{appName}/eval_sets/{evalSetId}/run-eval requests.

DTO for the response of POST /apps/{appName}/eval_sets/{evalSetId}/run-eval.

Service for creating and caching Runner instances.

Dynamically compiles and loads ADK

`BaseAgent`

implementations from source files.


---

<!-- DOCUMENTO FUSIONADO: adkwebserveraddsessiontoevalsetrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.AddSessionToEvalSetRequest.html -->

# Class AdkWebServer.AddSessionToEvalSetRequest

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer.AddSessionToEvalSetRequest

- Enclosing class:
[AdkWebServer](AdkWebServer.html)

DTO for POST /apps/{appName}/eval_sets/{evalSetId}/add-session requests. Contains information
to associate a session with an evaluation set.

-
## Field Summary

-
## Constructor Summary

-
## Method Summary


-
## Field Details

-
### evalId

-
### sessionId

-
### userId


-
-
## Constructor Details

-
### AddSessionToEvalSetRequest

public AddSessionToEvalSetRequest()

-
-
## Method Details

-
### getEvalId

-
### getSessionId

-
### getUserId


-


---

<!-- DOCUMENTO FUSIONADO: adkwebservergraphresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.GraphResponse.html -->

# Class AdkWebServer.GraphResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer.GraphResponse

- Enclosing class:
[AdkWebServer](AdkWebServer.html)

DTO for the response of GET
/apps/{appName}/users/{userId}/sessions/{sessionId}/events/{eventId}/graph. Contains the graph
representation (e.g., DOT source).

-
## Field Summary

-
## Constructor Summary

-
## Method Summary


-
## Field Details

-
### dotSrc


-
-
## Constructor Details

-
### GraphResponse

Constructs a GraphResponse.- Parameters:
`dotSrc`

- The graph source string (e.g., in DOT format).

-
### GraphResponse

public GraphResponse()

-
-
## Method Details

-
### getDotSrc


-


---

<!-- DOCUMENTO FUSIONADO: adkwebserveragentrunrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.AgentRunRequest.html -->

# Class AdkWebServer.AgentRunRequest

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer.AgentRunRequest

- Enclosing class:
[AdkWebServer](AdkWebServer.html)

Data Transfer Object (DTO) for POST /run and POST /run-sse requests. Contains information
needed to execute an agent run.

-
## Field Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`com.google.genai.types.Content`

`boolean`


-
## Field Details

-
### appName

-
### userId

-
### sessionId

-
### newMessage

public com.google.genai.types.Content newMessage -
### streaming

public boolean streaming

-
-
## Constructor Details

-
### AgentRunRequest

public AgentRunRequest()

-
-
## Method Details

-
### getAppName

-
### getUserId

-
### getSessionId

-
### getNewMessage

public com.google.genai.types.Content getNewMessage() -
### getStreaming

public boolean getStreaming()

-


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/package-summary.html -->

# Package com.google.adk.web

package com.google.adk.web

-
ClassDescriptionSingle-file Spring Boot application for the Agent Server.DTO for POST /apps/{appName}/eval_sets/{evalSetId}/add-session requests.Spring Boot REST Controller handling agent-related API endpoints.Data Transfer Object (DTO) for POST /run and POST /run-sse requests.A custom SpanExporter that stores relevant span data.DTO for the response of GET /apps/{appName}/users/{userId}/sessions/{sessionId}/events/{eventId}/graph.WebSocket Handler for the /run_live endpoint.Configuration class for OpenTelemetry, setting up the tracer provider and span exporter.DTO for POST /apps/{appName}/eval_sets/{evalSetId}/run-eval requests.DTO for the response of POST /apps/{appName}/eval_sets/{evalSetId}/run-eval.Service for creating and caching Runner instances.Configuration class for WebSocket handling.Dynamically compiles and loads ADK
implementations from source files.`BaseAgent`

Utility class to generate Graphviz DOT representations of Agent structures.


---

<!-- DOCUMENTO FUSIONADO: adkwebserverwebsocketconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.WebSocketConfig.html -->

# Class AdkWebServer.WebSocketConfig

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer.WebSocketConfig

- All Implemented Interfaces:
`org.springframework.web.socket.config.annotation.WebSocketConfigurer`


- Enclosing class:
[AdkWebServer](AdkWebServer.html)

@Configuration
@EnableWebSocket
public static class AdkWebServer.WebSocketConfig
extends

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)implements org.springframework.web.socket.config.annotation.WebSocketConfigurerConfiguration class for WebSocket handling.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`void`

[registerWebSocketHandlers](#registerWebSocketHandlers(org.springframework.web.socket.config.annotation.WebSocketHandlerRegistry))(org.springframework.web.socket.config.annotation.WebSocketHandlerRegistry registry)

-
## Constructor Details

-
### WebSocketConfig


-
-
## Method Details

-
### registerWebSocketHandlers

public void registerWebSocketHandlers(org.springframework.web.socket.config.annotation.WebSocketHandlerRegistry registry) - Specified by:
`registerWebSocketHandlers`

in interface`org.springframework.web.socket.config.annotation.WebSocketConfigurer`


-


---

<!-- DOCUMENTO FUSIONADO: agentgraphgeneratorhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AgentGraphGenerator.html -->

# Class AgentGraphGenerator

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AgentGraphGenerator

Utility class to generate Graphviz DOT representations of Agent structures.

-
## Constructor Summary

-
## Method Summary


-
## Constructor Details

-
### AgentGraphGenerator

public AgentGraphGenerator()

-
-
## Method Details

-
### getAgentGraphDotSource

public static[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> getAgentGraphDotSource( [BaseAgent](../agents/BaseAgent.html)rootAgent,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>> highlightPairs)Generates the DOT source string for the agent graph.- Parameters:
`rootAgent`

- The root agent of the structure.`highlightPairs`

- A list where each inner list contains two strings (fromNode, toNode) representing an edge to highlight. Order matters for direction.- Returns:
- The DOT source string, or null if graph generation fails.


-


---

<!-- DOCUMENTO FUSIONADO: adkwebserveropentelemetryconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.OpenTelemetryConfig.html -->

# Class AdkWebServer.OpenTelemetryConfig

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer.OpenTelemetryConfig

- Enclosing class:
[AdkWebServer](AdkWebServer.html)

Configuration class for OpenTelemetry, setting up the tracer provider and span exporter.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.opentelemetry.api.OpenTelemetry`

[openTelemetrySdk](#openTelemetrySdk(io.opentelemetry.sdk.trace.SdkTracerProvider))(io.opentelemetry.sdk.trace.SdkTracerProvider sdkTracerProvider) `io.opentelemetry.sdk.trace.SdkTracerProvider`

[sdkTracerProvider](#sdkTracerProvider(com.google.adk.web.AdkWebServer.ApiServerSpanExporter))( [AdkWebServer.ApiServerSpanExporter](AdkWebServer.ApiServerSpanExporter.html)apiServerSpanExporter)

-
## Constructor Details

-
### OpenTelemetryConfig

public OpenTelemetryConfig()

-
-
## Method Details

-
### apiServerSpanExporter

-
### sdkTracerProvider

@Bean(destroyMethod="shutdown") public io.opentelemetry.sdk.trace.SdkTracerProvider sdkTracerProvider( [AdkWebServer.ApiServerSpanExporter](AdkWebServer.ApiServerSpanExporter.html)apiServerSpanExporter) -
### openTelemetrySdk

@Bean public io.opentelemetry.api.OpenTelemetry openTelemetrySdk(io.opentelemetry.sdk.trace.SdkTracerProvider sdkTracerProvider)

-


---

<!-- DOCUMENTO FUSIONADO: adkwebserverrunnerservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.RunnerService.html -->

# Class AdkWebServer.RunnerService

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer.RunnerService

- Enclosing class:
[AdkWebServer](AdkWebServer.html)

Service for creating and caching Runner instances.

-
## Constructor Summary

ConstructorDescription[RunnerService](#%3Cinit%3E(java.util.Map,com.google.adk.artifacts.BaseArtifactService,com.google.adk.sessions.BaseSessionService))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[BaseAgent](../agents/BaseAgent.html)> agentRegistry,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService,[BaseSessionService](../sessions/BaseSessionService.html)sessionService) -
## Method Summary


-
## Constructor Details

-
### RunnerService

@Autowired public RunnerService(@Qualifier("loadedAgentRegistry") [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[BaseAgent](../agents/BaseAgent.html)> agentRegistry,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService,[BaseSessionService](../sessions/BaseSessionService.html)sessionService)

-
-
## Method Details

-
### getRunner


-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/package-tree.html -->

# Hierarchy For Package com.google.adk.web

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- org.springframework.web.socket.handler.AbstractWebSocketHandler (implements org.springframework.web.socket.WebSocketHandler)
- org.springframework.web.socket.handler.TextWebSocketHandler
- com.google.adk.web.
[AdkWebServer.LiveWebSocketHandler](AdkWebServer.LiveWebSocketHandler.html)

- com.google.adk.web.

- org.springframework.web.socket.handler.TextWebSocketHandler
- com.google.adk.web.
[AdkWebServer](AdkWebServer.html)(implements org.springframework.web.servlet.config.annotation.WebMvcConfigurer) - com.google.adk.web.
[AdkWebServer.AddSessionToEvalSetRequest](AdkWebServer.AddSessionToEvalSetRequest.html) - com.google.adk.web.
[AdkWebServer.AgentController](AdkWebServer.AgentController.html) - com.google.adk.web.
[AdkWebServer.AgentRunRequest](AdkWebServer.AgentRunRequest.html) - com.google.adk.web.
[AdkWebServer.ApiServerSpanExporter](AdkWebServer.ApiServerSpanExporter.html)(implements io.opentelemetry.sdk.trace.export.SpanExporter) - com.google.adk.web.
[AdkWebServer.GraphResponse](AdkWebServer.GraphResponse.html) - com.google.adk.web.
[AdkWebServer.OpenTelemetryConfig](AdkWebServer.OpenTelemetryConfig.html) - com.google.adk.web.
[AdkWebServer.RunEvalRequest](AdkWebServer.RunEvalRequest.html) - com.google.adk.web.
[AdkWebServer.RunnerService](AdkWebServer.RunnerService.html) - com.google.adk.web.
[AdkWebServer.WebSocketConfig](AdkWebServer.WebSocketConfig.html)(implements org.springframework.web.socket.config.annotation.WebSocketConfigurer) - com.google.adk.web.
[AgentCompilerLoader](AgentCompilerLoader.html) - com.google.adk.web.
[AgentGraphGenerator](AgentGraphGenerator.html) - com.google.adk.
[JsonBaseModel](../JsonBaseModel.html)- com.google.adk.web.
[AdkWebServer.RunEvalResult](AdkWebServer.RunEvalResult.html)

- com.google.adk.web.

- org.springframework.web.socket.handler.AbstractWebSocketHandler (implements org.springframework.web.socket.WebSocketHandler)


---

<!-- DOCUMENTO FUSIONADO: adkwebserverrunevalresulthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.RunEvalResult.html -->

# Class AdkWebServer.RunEvalResult

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.JsonBaseModel](../JsonBaseModel.html)

com.google.adk.web.AdkWebServer.RunEvalResult

- Enclosing class:
[AdkWebServer](AdkWebServer.html)

DTO for the response of POST /apps/{appName}/eval_sets/{evalSetId}/run-eval. Contains the
results of an evaluation run.

-
## Field Summary

-
## Constructor Summary

-
## Method Summary

### Methods inherited from class com.google.adk.

[JsonBaseModel](../JsonBaseModel.html)[fromJsonNode](../JsonBaseModel.html#fromJsonNode(com.fasterxml.jackson.databind.JsonNode,java.lang.Class)),[fromJsonString](../JsonBaseModel.html#fromJsonString(java.lang.String,java.lang.Class)),[getMapper](../JsonBaseModel.html#getMapper()),[toJson](../JsonBaseModel.html#toJson()),[toJsonNode](../JsonBaseModel.html#toJsonNode(java.lang.Object)),[toJsonString](../JsonBaseModel.html#toJsonString(java.lang.Object))

-
## Field Details

-
### appName

-
### evalSetId

-
### evalId

-
### finalEvalStatus

-
### evalMetricResults

-
### sessionId


-
-
## Constructor Details

-
### RunEvalResult

public RunEvalResult( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalSetId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)finalEvalStatus,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>> evalMetricResults,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Constructs a RunEvalResult.- Parameters:
`appName`

- The application name.`evalSetId`

- The evaluation set ID.`evalId`

- The evaluation ID.`finalEvalStatus`

- The final status of the evaluation.`evalMetricResults`

- The results for each metric.`sessionId`

- The session ID associated with the evaluation.

-
### RunEvalResult

public RunEvalResult()

-


---

<!-- DOCUMENTO FUSIONADO: agentcompilerloaderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AgentCompilerLoader.html -->

# Class AgentCompilerLoader

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AgentCompilerLoader

Dynamically compiles and loads ADK

[implementations from source files. It orchestrates the discovery of the ADK core JAR, compilation of agent sources using the Eclipse JDT (ECJ) compiler, and loading of compiled agents into isolated classloaders. Agents are identified by a public static field named](../agents/BaseAgent.html)`BaseAgent`

`ROOT_AGENT`

. Supports agent organization in
subdirectories or as individual `.java`

files.-
## Constructor Summary

ConstructorDescription[AgentCompilerLoader](#%3Cinit%3E(com.google.adk.web.config.AgentLoadingProperties))( [AgentLoadingProperties](config/AgentLoadingProperties.html)properties)Initializes the loader with agent configuration and proactively attempts to locate the ADK core JAR. -
## Method Summary

Modifier and TypeMethodDescriptionDiscovers, compiles, and loads agents from the configured source directory.

-
## Constructor Details

-
### AgentCompilerLoader

Initializes the loader with agent configuration and proactively attempts to locate the ADK core JAR. This JAR, containingand other core ADK types, is crucial for agent compilation. The location strategy (see`BaseAgent`

`locateAndPrepareAdkCoreJar()`

) includes handling directly available JARs and extracting nested JARs (e.g., in Spring Boot fat JARs) to ensure it's available for the compilation classpath.- Parameters:
`properties`

- Configuration detailing agent source locations and compilation settings.


-
-
## Method Details

-
### loadAgents

Discovers, compiles, and loads agents from the configured source directory.The process for each potential "agent unit" (a subdirectory or a root

`.java`

file):- Collects
`.java`

source files. - Compiles these sources using ECJ (see
`compileSourcesWithECJ(List, Path)`

) into a temporary, unit-specific output directory. This directory is cleaned up on JVM exit. - Creates a dedicated
for the compiled unit, isolating its classes.`URLClassLoader`

- Scans compiled classes for a public static field
`ROOT_AGENT`

assignable to. This field serves as the designated entry point for an agent.`BaseAgent`

- Instantiates and stores the
if found, keyed by its name.`BaseAgent`


- Returns:
- A map of successfully loaded agent names to their
instances. Returns an empty map if the source directory isn't configured or no agents are found.`BaseAgent`

- Throws:

- If an I/O error occurs (e.g., creating temp directories, reading sources).[IOException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/IOException.html)

- Collects

-


---

<!-- DOCUMENTO FUSIONADO: adkwebserverapiserverspanexporterhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.ApiServerSpanExporter.html -->

# Class AdkWebServer.ApiServerSpanExporter

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer.ApiServerSpanExporter

- All Implemented Interfaces:
`io.opentelemetry.sdk.trace.export.SpanExporter`

,

,[Closeable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Closeable.html)[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

- Enclosing class:
[AdkWebServer](AdkWebServer.html)

public static class AdkWebServer.ApiServerSpanExporter
extends

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)implements io.opentelemetry.sdk.trace.export.SpanExporterA custom SpanExporter that stores relevant span data. It handles two types of trace data
storage: 1. Event-ID based: Stores attributes of specific spans (call_llm, send_data,
tool_response) keyed by `gcp.vertex.agent.event_id`. This is used for debugging individual
events. 2. Session-ID based: Stores all exported spans and maintains a mapping from
`session_id` (extracted from `call_llm` spans) to a list of `trace_id`s. This is used for
retrieving all spans related to a session.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.opentelemetry.sdk.common.CompletableResultCode`

[export](#export(java.util.Collection))( [Collection](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Collection.html)<io.opentelemetry.sdk.trace.data.SpanData> spans)`io.opentelemetry.sdk.common.CompletableResultCode`

[flush](#flush())()[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<io.opentelemetry.sdk.trace.data.SpanData> [getEventTraceAttributes](#getEventTraceAttributes(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId)`io.opentelemetry.sdk.common.CompletableResultCode`

[shutdown](#shutdown())()### Methods inherited from class java.lang.

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)[clone](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#clone()),[equals](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#equals(java.lang.Object)),[finalize](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#finalize()),[getClass](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#getClass()),[hashCode](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#hashCode()),[notify](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notify()),[notifyAll](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notifyAll()),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#toString()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long)),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long,int))### Methods inherited from interface io.opentelemetry.sdk.trace.export.SpanExporter

`close`


-
## Constructor Details

-
### ApiServerSpanExporter

public ApiServerSpanExporter()

-
-
## Method Details

-
### getEventTraceAttributes

-
### getSessionToTraceIdsMap

-
### getAllExportedSpans

-
### export

public io.opentelemetry.sdk.common.CompletableResultCode export( [Collection](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Collection.html)<io.opentelemetry.sdk.trace.data.SpanData> spans)- Specified by:
`export`

in interface`io.opentelemetry.sdk.trace.export.SpanExporter`


-
### flush

public io.opentelemetry.sdk.common.CompletableResultCode flush()- Specified by:
`flush`

in interface`io.opentelemetry.sdk.trace.export.SpanExporter`


-
### shutdown

public io.opentelemetry.sdk.common.CompletableResultCode shutdown()- Specified by:
`shutdown`

in interface`io.opentelemetry.sdk.trace.export.SpanExporter`


-


---

<!-- DOCUMENTO FUSIONADO: adkwebserverlivewebsockethandlerhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.LiveWebSocketHandler.html -->

# Class AdkWebServer.LiveWebSocketHandler

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

org.springframework.web.socket.handler.AbstractWebSocketHandler

org.springframework.web.socket.handler.TextWebSocketHandler

com.google.adk.web.AdkWebServer.LiveWebSocketHandler

- All Implemented Interfaces:
`org.springframework.web.socket.WebSocketHandler`


- Enclosing class:
[AdkWebServer](AdkWebServer.html)

@Component
public static class AdkWebServer.LiveWebSocketHandler
extends org.springframework.web.socket.handler.TextWebSocketHandler

WebSocket Handler for the /run_live endpoint.

Manages bidirectional communication for live agent interactions. Assumes the
com.google.adk.runner.Runner class has a method: ```
public Flowable<Event> runLive(Session
session, Flowable<LiveRequest> liveRequests, List<String> modalities)
```


-
## Constructor Summary

ConstructorDescription[LiveWebSocketHandler](#%3Cinit%3E(com.fasterxml.jackson.databind.ObjectMapper,com.google.adk.sessions.BaseSessionService,com.google.adk.web.AdkWebServer.RunnerService))(com.fasterxml.jackson.databind.ObjectMapper objectMapper, [BaseSessionService](../sessions/BaseSessionService.html)sessionService,[AdkWebServer.RunnerService](AdkWebServer.RunnerService.html)runnerService) -
## Method Summary

Modifier and TypeMethodDescription`void`

[afterConnectionClosed](#afterConnectionClosed(org.springframework.web.socket.WebSocketSession,org.springframework.web.socket.CloseStatus))(org.springframework.web.socket.WebSocketSession wsSession, org.springframework.web.socket.CloseStatus status) `void`

[afterConnectionEstablished](#afterConnectionEstablished(org.springframework.web.socket.WebSocketSession))(org.springframework.web.socket.WebSocketSession wsSession) `protected void`

[handleTextMessage](#handleTextMessage(org.springframework.web.socket.WebSocketSession,org.springframework.web.socket.TextMessage))(org.springframework.web.socket.WebSocketSession wsSession, org.springframework.web.socket.TextMessage message) `void`

[handleTransportError](#handleTransportError(org.springframework.web.socket.WebSocketSession,java.lang.Throwable))(org.springframework.web.socket.WebSocketSession wsSession, [Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)exception)### Methods inherited from class org.springframework.web.socket.handler.TextWebSocketHandler

`handleBinaryMessage`

### Methods inherited from class org.springframework.web.socket.handler.AbstractWebSocketHandler

`handleMessage, handlePongMessage, supportsPartialMessages`


-
## Constructor Details

-
### LiveWebSocketHandler

@Autowired public LiveWebSocketHandler(com.fasterxml.jackson.databind.ObjectMapper objectMapper, [BaseSessionService](../sessions/BaseSessionService.html)sessionService,[AdkWebServer.RunnerService](AdkWebServer.RunnerService.html)runnerService)

-
-
## Method Details

-
### afterConnectionEstablished

public void afterConnectionEstablished(org.springframework.web.socket.WebSocketSession wsSession) throws [Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)- Specified by:
`afterConnectionEstablished`

in interface`org.springframework.web.socket.WebSocketHandler`

- Overrides:
`afterConnectionEstablished`

in class`org.springframework.web.socket.handler.AbstractWebSocketHandler`

- Throws:
[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)

-
### handleTextMessage

-
### handleTransportError

public void handleTransportError(org.springframework.web.socket.WebSocketSession wsSession, [Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)exception) throws[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)- Specified by:
`handleTransportError`

in interface`org.springframework.web.socket.WebSocketHandler`

- Overrides:
`handleTransportError`

in class`org.springframework.web.socket.handler.AbstractWebSocketHandler`

- Throws:
[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)

-
### afterConnectionClosed

public void afterConnectionClosed(org.springframework.web.socket.WebSocketSession wsSession, org.springframework.web.socket.CloseStatus status) throws [Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)- Specified by:
`afterConnectionClosed`

in interface`org.springframework.web.socket.WebSocketHandler`

- Overrides:
`afterConnectionClosed`

in class`org.springframework.web.socket.handler.AbstractWebSocketHandler`

- Throws:
[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)


-


---

<!-- DOCUMENTO FUSIONADO: adkwebserverhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.html -->

# Class AdkWebServer

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer

- All Implemented Interfaces:
`org.springframework.web.servlet.config.annotation.WebMvcConfigurer`


@SpringBootApplication
@ConfigurationPropertiesScan
@ComponentScan(basePackages={"com.google.adk.web","com.google.adk.web.config"})
public class AdkWebServer
extends

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)implements org.springframework.web.servlet.config.annotation.WebMvcConfigurerSingle-file Spring Boot application for the Agent Server. Combines configuration, DTOs, and
controller logic.

-
## Nested Class Summary

Modifier and TypeClassDescription`static class`

DTO for POST /apps/{appName}/eval_sets/{evalSetId}/add-session requests.`static class`

Spring Boot REST Controller handling agent-related API endpoints.`static class`

Data Transfer Object (DTO) for POST /run and POST /run-sse requests.`static class`

A custom SpanExporter that stores relevant span data.`static class`

DTO for the response of GET /apps/{appName}/users/{userId}/sessions/{sessionId}/events/{eventId}/graph.`static class`

WebSocket Handler for the /run_live endpoint.`static class`

Configuration class for OpenTelemetry, setting up the tracer provider and span exporter.`static class`

DTO for POST /apps/{appName}/eval_sets/{evalSetId}/run-eval requests.`static class`

DTO for the response of POST /apps/{appName}/eval_sets/{evalSetId}/run-eval.`static class`

Service for creating and caching Runner instances.`static class`

Configuration class for WebSocket handling. -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`void`

[addResourceHandlers](#addResourceHandlers(org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry))(org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry registry) Configures resource handlers for serving static content (like the Dev UI).`void`

[addViewControllers](#addViewControllers(org.springframework.web.servlet.config.annotation.ViewControllerRegistry))(org.springframework.web.servlet.config.annotation.ViewControllerRegistry registry) Configures simple automated controllers: - Redirects the root path "/" to "/dev-ui".Provides the singleton instance of the ArtifactService (InMemory).[loadedAgentRegistry](#loadedAgentRegistry(com.google.adk.web.AgentCompilerLoader,com.google.adk.web.config.AgentLoadingProperties))( [AgentCompilerLoader](AgentCompilerLoader.html)loader,[AgentLoadingProperties](config/AgentLoadingProperties.html)props)`static void`

Main entry point for the Spring Boot application.`com.fasterxml.jackson.databind.ObjectMapper`

### Methods inherited from class java.lang.

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)[clone](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#clone()),[equals](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#equals(java.lang.Object)),[finalize](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#finalize()),[getClass](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#getClass()),[hashCode](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#hashCode()),[notify](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notify()),[notifyAll](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notifyAll()),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#toString()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long)),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long,int))### Methods inherited from interface org.springframework.web.servlet.config.annotation.WebMvcConfigurer

`addArgumentResolvers, addCorsMappings, addErrorResponseInterceptors, addFormatters, addInterceptors, addReturnValueHandlers, configureAsyncSupport, configureContentNegotiation, configureDefaultServletHandling, configureHandlerExceptionResolvers, configureMessageConverters, configurePathMatch, configureViewResolvers, extendHandlerExceptionResolvers, extendMessageConverters, getMessageCodesResolver, getValidator`


-
## Constructor Details

-
### AdkWebServer

public AdkWebServer()

-
-
## Method Details

-
### sessionService

-
### artifactService

Provides the singleton instance of the ArtifactService (InMemory). TODO: configure this based on config (e.g., DB URL)- Returns:
- An instance of BaseArtifactService (currently InMemoryArtifactService).

-
### loadedAgentRegistry

@Bean("loadedAgentRegistry") public[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[BaseAgent](../agents/BaseAgent.html)> loadedAgentRegistry( [AgentCompilerLoader](AgentCompilerLoader.html)loader,[AgentLoadingProperties](config/AgentLoadingProperties.html)props) -
### objectMapper

@Bean public com.fasterxml.jackson.databind.ObjectMapper objectMapper() -
### addResourceHandlers

public void addResourceHandlers(org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry registry) Configures resource handlers for serving static content (like the Dev UI). Maps requests starting with "/dev-ui/" to the directory specified by the 'adk.web.ui.dir' system property.- Specified by:
`addResourceHandlers`

in interface`org.springframework.web.servlet.config.annotation.WebMvcConfigurer`


-
### addViewControllers

public void addViewControllers(org.springframework.web.servlet.config.annotation.ViewControllerRegistry registry) Configures simple automated controllers: - Redirects the root path "/" to "/dev-ui". - Forwards requests to "/dev-ui" to "/dev-ui/index.html" so the ResourceHandler serves it.- Specified by:
`addViewControllers`

in interface`org.springframework.web.servlet.config.annotation.WebMvcConfigurer`


-
### main

Main entry point for the Spring Boot application.- Parameters:
`args`

- Command line arguments.


-


---

<!-- DOCUMENTO FUSIONADO: adkwebserveragentcontrollerhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/AdkWebServer.AgentController.html -->

# Class AdkWebServer.AgentController

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.AdkWebServer.AgentController

- Enclosing class:
[AdkWebServer](AdkWebServer.html)

Spring Boot REST Controller handling agent-related API endpoints.

-
## Constructor Summary

ConstructorDescription[AgentController](#%3Cinit%3E(com.google.adk.sessions.BaseSessionService,com.google.adk.artifacts.BaseArtifactService,java.util.Map,com.google.adk.web.AdkWebServer.ApiServerSpanExporter,com.google.adk.web.AdkWebServer.RunnerService))( [BaseSessionService](../sessions/BaseSessionService.html)sessionService,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[BaseAgent](../agents/BaseAgent.html)> agentRegistry,[AdkWebServer.ApiServerSpanExporter](AdkWebServer.ApiServerSpanExporter.html)apiServerSpanExporter,[AdkWebServer.RunnerService](AdkWebServer.RunnerService.html)runnerService)Constructs the AgentController. -
## Method Summary

Modifier and TypeMethodDescription`org.springframework.http.ResponseEntity`

< [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>[addSessionToEvalSet](#addSessionToEvalSet(java.lang.String,java.lang.String,com.google.adk.web.AdkWebServer.AddSessionToEvalSetRequest))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalSetId,[AdkWebServer.AddSessionToEvalSetRequest](AdkWebServer.AddSessionToEvalSetRequest.html)req)Placeholder for adding a session to an evaluation set.[agentRun](#agentRun(com.google.adk.web.AdkWebServer.AgentRunRequest))( [AdkWebServer.AgentRunRequest](AdkWebServer.AgentRunRequest.html)request)Executes a non-streaming agent run for a given session and message.`org.springframework.web.servlet.mvc.method.annotation.SseEmitter`

[agentRunSse](#agentRunSse(com.google.adk.web.AdkWebServer.AgentRunRequest))( [AdkWebServer.AgentRunRequest](AdkWebServer.AgentRunRequest.html)request)Executes an agent run and streams the resulting events using Server-Sent Events (SSE).`org.springframework.http.ResponseEntity`

< [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>[createEvalSet](#createEvalSet(java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalSetId)Placeholder for creating an evaluation set.Creates a new session where the ID is generated by the service.Creates a new session with a specific ID provided by the client.`org.springframework.http.ResponseEntity`

< [Void](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Void.html)>[deleteArtifact](#deleteArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)artifactName)Deletes an artifact and all its versions.`org.springframework.http.ResponseEntity`

< [Void](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Void.html)>[deleteSession](#deleteSession(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Deletes a specific session.`org.springframework.http.ResponseEntity`

< [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>[getEvalResult](#getEvalResult(java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalResultId)Gets a specific evaluation result.`org.springframework.http.ResponseEntity`

< [AdkWebServer.GraphResponse](AdkWebServer.GraphResponse.html)>[getEventGraph](#getEventGraph(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId)Endpoint to get a graph representation of an event (currently returns a placeholder).[getSession](#getSession(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Retrieves a specific session by its ID.`org.springframework.http.ResponseEntity`

< [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>[getSessionTrace](#getSessionTrace(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Retrieves trace spans for a given session ID.`org.springframework.http.ResponseEntity`

<?> [getTraceDict](#getTraceDict(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId)Endpoint for retrieving trace information stored by the ApiServerSpanExporter, based on event ID.[listApps](#listApps())()Lists available applications.[listArtifactNames](#listArtifactNames(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists the names of all artifacts associated with a session.[listArtifactVersions](#listArtifactVersions(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)artifactName)Lists the available versions for a specific artifact.[listEvalResults](#listEvalResults(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName)Lists all evaluation results for an app.[listEvalSets](#listEvalSets(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName)Placeholder for listing evaluation sets.[listEvalsInEvalSet](#listEvalsInEvalSet(java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalSetId)Placeholder for listing evaluations within an evaluation set.[listSessions](#listSessions(java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId)Lists all non-evaluation sessions for a given app and user.`com.google.genai.types.Part`

Loads the latest or a specific version of an artifact associated with a session.`com.google.genai.types.Part`

[loadArtifactVersion](#loadArtifactVersion(java.lang.String,java.lang.String,java.lang.String,java.lang.String,int))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)artifactName, int versionId)Loads a specific version of an artifact.[runEval](#runEval(java.lang.String,java.lang.String,com.google.adk.web.AdkWebServer.RunEvalRequest))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalSetId,[AdkWebServer.RunEvalRequest](AdkWebServer.RunEvalRequest.html)req)Placeholder for running evaluations.

-
## Constructor Details

-
### AgentController

@Autowired public AgentController( [BaseSessionService](../sessions/BaseSessionService.html)sessionService,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService, @Qualifier("loadedAgentRegistry")[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[BaseAgent](../agents/BaseAgent.html)> agentRegistry,[AdkWebServer.ApiServerSpanExporter](AdkWebServer.ApiServerSpanExporter.html)apiServerSpanExporter,[AdkWebServer.RunnerService](AdkWebServer.RunnerService.html)runnerService)Constructs the AgentController.- Parameters:
`sessionService`

- The service for managing sessions.`artifactService`

- The service for managing artifacts.`agentRegistry`

- The registry of loaded agents.`apiServerSpanExporter`

- The exporter holding all trace data.`runnerService`

- The service for obtaining Runner instances.


-
-
## Method Details

-
### listApps

-
### getTraceDict

@GetMapping("/debug/trace/{eventId}") public org.springframework.http.ResponseEntity<?> getTraceDict(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId)Endpoint for retrieving trace information stored by the ApiServerSpanExporter, based on event ID.- Parameters:
`eventId`

- The ID of the event to trace (expected to be gcp.vertex.agent.event_id).- Returns:
- A ResponseEntity containing the trace data or NOT_FOUND.

-
### getSessionTrace

@GetMapping("/debug/trace/session/{sessionId}") public org.springframework.http.ResponseEntity<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> getSessionTrace(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Retrieves trace spans for a given session ID.- Parameters:
`sessionId`

- The session ID.- Returns:
- A ResponseEntity containing a list of span data maps for the session, or an empty list.

-
### getSession

@GetMapping("/apps/{appName}/users/{userId}/sessions/{sessionId}") public[Session](../sessions/Session.html)getSession(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Retrieves a specific session by its ID.- Parameters:
`appName`

- The application name.`userId`

- The user ID.`sessionId`

- The session ID.- Returns:
- The requested Session object.
- Throws:
`org.springframework.web.server.ResponseStatusException`

- if the session is not found.

-
### listSessions

@GetMapping("/apps/{appName}/users/{userId}/sessions") public[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[Session](../sessions/Session.html)> listSessions(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId)Lists all non-evaluation sessions for a given app and user.- Parameters:
`appName`

- The name of the application.`userId`

- The ID of the user.- Returns:
- A list of sessions, excluding those used for evaluation.

-
### createSessionWithId

@PostMapping("/apps/{appName}/users/{userId}/sessions/{sessionId}") public[Session](../sessions/Session.html)createSessionWithId(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, @RequestBody(required=false)[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state)Creates a new session with a specific ID provided by the client.- Parameters:
`appName`

- The application name.`userId`

- The user ID.`sessionId`

- The desired session ID.`state`

- Optional initial state for the session.- Returns:
- The newly created Session object.
- Throws:
`org.springframework.web.server.ResponseStatusException`

- if a session with the given ID already exists (BAD_REQUEST) or if creation fails (INTERNAL_SERVER_ERROR).

-
### createSession

@PostMapping("/apps/{appName}/users/{userId}/sessions") public[Session](../sessions/Session.html)createSession(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @RequestBody(required=false)[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state)Creates a new session where the ID is generated by the service.- Parameters:
`appName`

- The application name.`userId`

- The user ID.`state`

- Optional initial state for the session.- Returns:
- The newly created Session object.
- Throws:
`org.springframework.web.server.ResponseStatusException`

- if creation fails (INTERNAL_SERVER_ERROR).

-
### deleteSession

@DeleteMapping("/apps/{appName}/users/{userId}/sessions/{sessionId}") public org.springframework.http.ResponseEntity<[Void](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Void.html)> deleteSession(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Deletes a specific session.- Parameters:
`appName`

- The application name.`userId`

- The user ID.`sessionId`

- The session ID to delete.- Returns:
- A ResponseEntity with status NO_CONTENT on success.
- Throws:
`org.springframework.web.server.ResponseStatusException`

- if deletion fails (INTERNAL_SERVER_ERROR).

-
### loadArtifact

@GetMapping("/apps/{appName}/users/{userId}/sessions/{sessionId}/artifacts/{artifactName}") public com.google.genai.types.Part loadArtifact(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)artifactName, @RequestParam(required=false)[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)version)Loads the latest or a specific version of an artifact associated with a session.- Parameters:
`appName`

- The application name.`userId`

- The user ID.`sessionId`

- The session ID.`artifactName`

- The name of the artifact.`version`

- Optional specific version number. If null, loads the latest.- Returns:
- The artifact content as a Part object.
- Throws:
`org.springframework.web.server.ResponseStatusException`

- if the artifact is not found (NOT_FOUND).

-
### loadArtifactVersion

@GetMapping("/apps/{appName}/users/{userId}/sessions/{sessionId}/artifacts/{artifactName}/versions/{versionId}") public com.google.genai.types.Part loadArtifactVersion(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)artifactName, @PathVariable int versionId)Loads a specific version of an artifact.- Parameters:
`appName`

- The application name.`userId`

- The user ID.`sessionId`

- The session ID.`artifactName`

- The name of the artifact.`versionId`

- The specific version number.- Returns:
- The artifact content as a Part object.
- Throws:
`org.springframework.web.server.ResponseStatusException`

- if the artifact version is not found (NOT_FOUND).

-
### listArtifactNames

@GetMapping("/apps/{appName}/users/{userId}/sessions/{sessionId}/artifacts") public[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> listArtifactNames(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists the names of all artifacts associated with a session.- Parameters:
`appName`

- The application name.`userId`

- The user ID.`sessionId`

- The session ID.- Returns:
- A list of artifact names.

-
### listArtifactVersions

@GetMapping("/apps/{appName}/users/{userId}/sessions/{sessionId}/artifacts/{artifactName}/versions") public[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> listArtifactVersions(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)artifactName)Lists the available versions for a specific artifact.- Parameters:
`appName`

- The application name.`userId`

- The user ID.`sessionId`

- The session ID.`artifactName`

- The name of the artifact.- Returns:
- A list of version numbers (integers).

-
### deleteArtifact

@DeleteMapping("/apps/{appName}/users/{userId}/sessions/{sessionId}/artifacts/{artifactName}") public org.springframework.http.ResponseEntity<[Void](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Void.html)> deleteArtifact(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)artifactName)Deletes an artifact and all its versions.- Parameters:
`appName`

- The application name.`userId`

- The user ID.`sessionId`

- The session ID.`artifactName`

- The name of the artifact to delete.- Returns:
- A ResponseEntity with status NO_CONTENT on success.
- Throws:
`org.springframework.web.server.ResponseStatusException`

- if deletion fails (INTERNAL_SERVER_ERROR).

-
### agentRun

Executes a non-streaming agent run for a given session and message.- Parameters:
`request`

- The AgentRunRequest containing run details.- Returns:
- A list of events generated during the run.
- Throws:
`org.springframework.web.server.ResponseStatusException`

- if the session is not found or the run fails.

-
### agentRunSse

@PostMapping(value="/run_sse", produces="text/event-stream") public org.springframework.web.servlet.mvc.method.annotation.SseEmitter agentRunSse(@RequestBody [AdkWebServer.AgentRunRequest](AdkWebServer.AgentRunRequest.html)request)Executes an agent run and streams the resulting events using Server-Sent Events (SSE).- Parameters:
`request`

- The AgentRunRequest containing run details.- Returns:
- A Flux that will stream events to the client.

-
### getEventGraph

@GetMapping("/apps/{appName}/users/{userId}/sessions/{sessionId}/events/{eventId}/graph") public org.springframework.http.ResponseEntity<[AdkWebServer.GraphResponse](AdkWebServer.GraphResponse.html)> getEventGraph(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId)Endpoint to get a graph representation of an event (currently returns a placeholder). Requires Graphviz or similar tooling for full implementation.- Parameters:
`appName`

- Application name.`userId`

- User ID.`sessionId`

- Session ID.`eventId`

- Event ID.- Returns:
- ResponseEntity containing a GraphResponse with placeholder DOT source.
- Throws:
`org.springframework.web.server.ResponseStatusException`

- if the session or event is not found.

-
### createEvalSet

-
### listEvalSets

-
### addSessionToEvalSet

@PostMapping("/apps/{appName}/eval_sets/{evalSetId}/add-session") public org.springframework.http.ResponseEntity<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> addSessionToEvalSet(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalSetId, @RequestBody[AdkWebServer.AddSessionToEvalSetRequest](AdkWebServer.AddSessionToEvalSetRequest.html)req)Placeholder for adding a session to an evaluation set. -
### listEvalsInEvalSet

-
### runEval

@PostMapping("/apps/{appName}/eval_sets/{evalSetId}/run-eval") public[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[AdkWebServer.RunEvalResult](AdkWebServer.RunEvalResult.html)> runEval(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalSetId, @RequestBody[AdkWebServer.RunEvalRequest](AdkWebServer.RunEvalRequest.html)req)Placeholder for running evaluations. -
### getEvalResult

@GetMapping("/apps/{appName}/eval_results/{evalResultId}") public org.springframework.http.ResponseEntity<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> getEvalResult(@PathVariable [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName, @PathVariable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)evalResultId)Gets a specific evaluation result. (STUB - Not Implemented)- Parameters:
`appName`

- The application name.`evalResultId`

- The evaluation result ID.- Returns:
- A ResponseEntity indicating the endpoint is not implemented.

-
### listEvalResults


-
