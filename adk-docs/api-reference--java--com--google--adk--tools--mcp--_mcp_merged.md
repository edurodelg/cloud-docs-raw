---
merged_at: 2026-01-25T03:28:16.186657
merged_files: 15
---

# Documentos Fusionados

Este archivo contiene 15 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/package-use.html -->

# Uses of Packagecom.google.adk.tools.mcp

# Uses of Package

com.google.adk.tools.mcp

-
ClassDescriptionManages MCP client sessions.Base exception for all errors originating from
`McpToolset`

.Interface for building McpClientTransport instances.Parameters for establishing a MCP Server-Sent Events (SSE) connection.Builder for.`SseServerParameters`


---

<!-- DOCUMENTO FUSIONADO: conversionutilshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/ConversionUtils.html -->

# Class ConversionUtils

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.mcp.ConversionUtils

Utility class for converting between different representations of MCP tools.

-
## Method Summary

Modifier and TypeMethodDescription`io.modelcontextprotocol.spec.McpSchema.Tool`

[adkToMcpToolType](#adkToMcpToolType(com.google.adk.tools.BaseTool))( [BaseTool](../BaseTool.html)tool)

-
## Method Details

-
### adkToMcpToolType


-


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/package-summary.html -->

# Package com.google.adk.tools.mcp

package com.google.adk.tools.mcp

-
ClassDescriptionUtility class for converting between different representations of MCP tools.The default builder for creating MCP client transports.Initializes a MCP tool.Manages MCP client sessions.Initializes a MCP tool.Connects to a MCP Server, and retrieves MCP Tools into ADK Tools.Exception thrown when there's an error during MCP session initialization.Exception thrown when there's an error during loading tools from the MCP server.Base exception for all errors originating from
`McpToolset`

.Interface for building McpClientTransport instances.Parameters for establishing a MCP Server-Sent Events (SSE) connection.Builder for.`SseServerParameters`


---

<!-- DOCUMENTO FUSIONADO: mcptransportbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/McpTransportBuilder.html -->

# Interface McpTransportBuilder

- All Known Implementing Classes:
[DefaultMcpTransportBuilder](DefaultMcpTransportBuilder.html)

public interface McpTransportBuilder

Interface for building McpClientTransport instances. Implementations of this interface are
responsible for constructing concrete McpClientTransport objects based on the provided connection
parameters.

-
## Method Summary


-
## Method Details

-
### build

Builds an McpClientTransport based on the provided connection parameters.- Parameters:
`connectionParams`

- The parameters required to configure the transport. The type of this object determines the type of transport built.- Returns:
- An instance of McpClientTransport.
- Throws:

- if the connectionParams are not supported or invalid.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)


-


---

<!-- DOCUMENTO FUSIONADO: defaultmcptransportbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/DefaultMcpTransportBuilder.html -->

# Class DefaultMcpTransportBuilder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.mcp.DefaultMcpTransportBuilder

- All Implemented Interfaces:
[McpTransportBuilder](McpTransportBuilder.html)

The default builder for creating MCP client transports. Supports StdioClientTransport based on

`ServerParameters`

and the standard HttpClientSseClientTransport based on [.](SseServerParameters.html)`SseServerParameters`

-
## Constructor Summary

-
## Method Summary


-
## Constructor Details

-
### DefaultMcpTransportBuilder

public DefaultMcpTransportBuilder()

-
-
## Method Details

-
### build

Description copied from interface:[McpTransportBuilder](McpTransportBuilder.html#build(java.lang.Object))Builds an McpClientTransport based on the provided connection parameters.- Specified by:

in interface[build](McpTransportBuilder.html#build(java.lang.Object))[McpTransportBuilder](McpTransportBuilder.html)- Parameters:
`connectionParams`

- The parameters required to configure the transport. The type of this object determines the type of transport built.- Returns:
- An instance of McpClientTransport.


-


---

<!-- DOCUMENTO FUSIONADO: sseserverparametershtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/SseServerParameters.html -->

# Class SseServerParameters

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.mcp.SseServerParameters

Parameters for establishing a MCP Server-Sent Events (SSE) connection.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[SseServerParameters.Builder](SseServerParameters.Builder.html)[builder](#builder())()Creates a new builder for.`SseServerParameters`

[headers](#headers())()Optional headers to include in the SSE connection request.`abstract`

[Duration](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Duration.html)The timeout for reading data from the SSE stream.`abstract`

[Duration](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Duration.html)[timeout](#timeout())()The timeout for the initial connection attempt.`abstract`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[url](#url())()The URL of the SSE server.

-
## Constructor Details

-
### SseServerParameters

public SseServerParameters()

-
-
## Method Details

-
### url

The URL of the SSE server. -
### headers

-
### timeout

The timeout for the initial connection attempt. -
### sseReadTimeout

The timeout for reading data from the SSE stream. -
### builder

Creates a new builder for.`SseServerParameters`


-


---

<!-- DOCUMENTO FUSIONADO: sseserverparametersbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/SseServerParameters.Builder.html -->

# Class SseServerParameters.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.mcp.SseServerParameters.Builder

- Enclosing class:
[SseServerParameters](SseServerParameters.html)

Builder for

[.](SseServerParameters.html)`SseServerParameters`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[SseServerParameters](SseServerParameters.html)[build](#build())()Builds a newinstance.`SseServerParameters`

`abstract`

[SseServerParameters.Builder](SseServerParameters.Builder.html)Sets the headers for the SSE connection request.`abstract`

[SseServerParameters.Builder](SseServerParameters.Builder.html)[sseReadTimeout](#sseReadTimeout(java.time.Duration))( [Duration](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Duration.html)sseReadTimeout)Sets the timeout for reading data from the SSE stream.`abstract`

[SseServerParameters.Builder](SseServerParameters.Builder.html)Sets the timeout for the initial connection attempt.`abstract`

[SseServerParameters.Builder](SseServerParameters.Builder.html)Sets the URL of the SSE server.

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### url

Sets the URL of the SSE server. -
### headers

Sets the headers for the SSE connection request. -
### timeout

Sets the timeout for the initial connection attempt. -
### sseReadTimeout

Sets the timeout for reading data from the SSE stream. -
### build

Builds a newinstance.`SseServerParameters`


-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/package-tree.html -->

# Hierarchy For Package com.google.adk.tools.mcp

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.tools.
[BaseTool](../BaseTool.html)- com.google.adk.tools.mcp.
[McpAsyncTool](McpAsyncTool.html) - com.google.adk.tools.mcp.
[McpTool](McpTool.html)

- com.google.adk.tools.mcp.
- com.google.adk.tools.mcp.
[ConversionUtils](ConversionUtils.html) - com.google.adk.tools.mcp.
[DefaultMcpTransportBuilder](DefaultMcpTransportBuilder.html)(implements com.google.adk.tools.mcp.[McpTransportBuilder](McpTransportBuilder.html)) - com.google.adk.tools.mcp.
[McpSessionManager](McpSessionManager.html) - com.google.adk.tools.mcp.
[McpToolset](McpToolset.html)(implements com.google.adk.tools.[BaseToolset](../BaseToolset.html)) - com.google.adk.tools.mcp.
[SseServerParameters](SseServerParameters.html) - com.google.adk.tools.mcp.
[SseServerParameters.Builder](SseServerParameters.Builder.html) - java.lang.
[Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)(implements java.io.[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html))- java.lang.
[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)- java.lang.
[RuntimeException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/RuntimeException.html)- com.google.adk.tools.mcp.
[McpToolset.McpToolsetException](McpToolset.McpToolsetException.html)- com.google.adk.tools.mcp.
[McpToolset.McpInitializationException](McpToolset.McpInitializationException.html) - com.google.adk.tools.mcp.
[McpToolset.McpToolLoadingException](McpToolset.McpToolLoadingException.html)

- com.google.adk.tools.mcp.

- com.google.adk.tools.mcp.

- java.lang.

- java.lang.

- com.google.adk.tools.

## Interface Hierarchy

- com.google.adk.tools.mcp.
[McpTransportBuilder](McpTransportBuilder.html)


---

<!-- DOCUMENTO FUSIONADO: mcptoolsetmcptoolloadingexceptionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/McpToolset.McpToolLoadingException.html -->

# Class McpToolset.McpToolLoadingException

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[java.lang.Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)

[java.lang.Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)

[java.lang.RuntimeException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/RuntimeException.html)

[com.google.adk.tools.mcp.McpToolset.McpToolsetException](McpToolset.McpToolsetException.html)

com.google.adk.tools.mcp.McpToolset.McpToolLoadingException

- All Implemented Interfaces:
[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html)

- Enclosing class:
[McpToolset](McpToolset.html)

Exception thrown when there's an error during loading tools from the MCP server.

- See Also:

-
## Constructor Summary

-
## Method Summary

### Methods inherited from class java.lang.

[Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)[addSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#addSuppressed(java.lang.Throwable)),[fillInStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#fillInStackTrace()),[getCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getCause()),[getLocalizedMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getLocalizedMessage()),[getMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getMessage()),[getStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getStackTrace()),[getSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getSuppressed()),[initCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#initCause(java.lang.Throwable)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace()),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintStream)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintWriter)),[setStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#setStackTrace(java.lang.StackTraceElement%5B%5D)),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#toString())

-
## Constructor Details

-
### McpToolLoadingException


-


---

<!-- DOCUMENTO FUSIONADO: mcptoolsetmcpinitializationexceptionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/McpToolset.McpInitializationException.html -->

# Class McpToolset.McpInitializationException

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[java.lang.Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)

[java.lang.Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)

[java.lang.RuntimeException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/RuntimeException.html)

[com.google.adk.tools.mcp.McpToolset.McpToolsetException](McpToolset.McpToolsetException.html)

com.google.adk.tools.mcp.McpToolset.McpInitializationException

- All Implemented Interfaces:
[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html)

- Enclosing class:
[McpToolset](McpToolset.html)

Exception thrown when there's an error during MCP session initialization.

- See Also:

-
## Constructor Summary

-
## Method Summary

### Methods inherited from class java.lang.

[Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)[addSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#addSuppressed(java.lang.Throwable)),[fillInStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#fillInStackTrace()),[getCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getCause()),[getLocalizedMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getLocalizedMessage()),[getMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getMessage()),[getStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getStackTrace()),[getSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getSuppressed()),[initCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#initCause(java.lang.Throwable)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace()),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintStream)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintWriter)),[setStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#setStackTrace(java.lang.StackTraceElement%5B%5D)),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#toString())

-
## Constructor Details

-
### McpInitializationException


-


---

<!-- DOCUMENTO FUSIONADO: mcptoolsetmcptoolsetexceptionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/McpToolset.McpToolsetException.html -->

# Class McpToolset.McpToolsetException

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[java.lang.Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)

[java.lang.Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)

[java.lang.RuntimeException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/RuntimeException.html)

com.google.adk.tools.mcp.McpToolset.McpToolsetException

- All Implemented Interfaces:
[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html)

- Direct Known Subclasses:

,[McpToolset.McpInitializationException](McpToolset.McpInitializationException.html)[McpToolset.McpToolLoadingException](McpToolset.McpToolLoadingException.html)

- Enclosing class:
[McpToolset](McpToolset.html)

Base exception for all errors originating from

`McpToolset`

.- See Also:

-
## Constructor Summary

-
## Method Summary

### Methods inherited from class java.lang.

[Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)[addSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#addSuppressed(java.lang.Throwable)),[fillInStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#fillInStackTrace()),[getCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getCause()),[getLocalizedMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getLocalizedMessage()),[getMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getMessage()),[getStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getStackTrace()),[getSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getSuppressed()),[initCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#initCause(java.lang.Throwable)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace()),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintStream)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintWriter)),[setStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#setStackTrace(java.lang.StackTraceElement%5B%5D)),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#toString())

-
## Constructor Details

-
### McpToolsetException


-


---

<!-- DOCUMENTO FUSIONADO: mcpsessionmanagerhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/McpSessionManager.html -->

# Class McpSessionManager

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.mcp.McpSessionManager

Manages MCP client sessions.

This class provides methods for creating and initializing MCP client sessions, handling different connection parameters and transport builders.

-
## Constructor Summary

ConstructorDescription[McpSessionManager](#%3Cinit%3E(java.lang.Object))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams)[McpSessionManager](#%3Cinit%3E(java.lang.Object,com.google.adk.tools.mcp.McpTransportBuilder))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams,[McpTransportBuilder](McpTransportBuilder.html)transportBuilder) -
## Method Summary

Modifier and TypeMethodDescription`io.modelcontextprotocol.client.McpAsyncClient`

`io.modelcontextprotocol.client.McpSyncClient`

`static io.modelcontextprotocol.client.McpAsyncClient`

[initializeAsyncSession](#initializeAsyncSession(java.lang.Object))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams)`static io.modelcontextprotocol.client.McpAsyncClient`

[initializeAsyncSession](#initializeAsyncSession(java.lang.Object,com.google.adk.tools.mcp.McpTransportBuilder))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams,[McpTransportBuilder](McpTransportBuilder.html)transportBuilder)`static io.modelcontextprotocol.client.McpSyncClient`

[initializeSession](#initializeSession(java.lang.Object))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams)`static io.modelcontextprotocol.client.McpSyncClient`

[initializeSession](#initializeSession(java.lang.Object,com.google.adk.tools.mcp.McpTransportBuilder))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams,[McpTransportBuilder](McpTransportBuilder.html)transportBuilder)

-
## Constructor Details

-
### McpSessionManager

-
### McpSessionManager


-
-
## Method Details

-
### createSession

public io.modelcontextprotocol.client.McpSyncClient createSession() -
### initializeSession

public static io.modelcontextprotocol.client.McpSyncClient initializeSession( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams) -
### initializeSession

public static io.modelcontextprotocol.client.McpSyncClient initializeSession( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams,[McpTransportBuilder](McpTransportBuilder.html)transportBuilder) -
### createAsyncSession

public io.modelcontextprotocol.client.McpAsyncClient createAsyncSession() -
### initializeAsyncSession

public static io.modelcontextprotocol.client.McpAsyncClient initializeAsyncSession( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams) -
### initializeAsyncSession

public static io.modelcontextprotocol.client.McpAsyncClient initializeAsyncSession( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)connectionParams,[McpTransportBuilder](McpTransportBuilder.html)transportBuilder)

-


---

<!-- DOCUMENTO FUSIONADO: mcptoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/McpTool.html -->

# Class McpTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](../BaseTool.html)

com.google.adk.tools.mcp.McpTool

Initializes a MCP tool.

This wraps a MCP Tool interface and an active MCP Session. It invokes the MCP Tool through executing the tool from remote MCP Session.

-
## Constructor Summary

ConstructorDescription[McpTool](#%3Cinit%3E(io.modelcontextprotocol.spec.McpSchema.Tool,io.modelcontextprotocol.client.McpSyncClient,com.google.adk.tools.mcp.McpSessionManager))(io.modelcontextprotocol.spec.McpSchema.Tool mcpTool, io.modelcontextprotocol.client.McpSyncClient mcpSession, [McpSessionManager](McpSessionManager.html)mcpSessionManager)Creates a new McpTool with the default ObjectMapper.[McpTool](#%3Cinit%3E(io.modelcontextprotocol.spec.McpSchema.Tool,io.modelcontextprotocol.client.McpSyncClient,com.google.adk.tools.mcp.McpSessionManager,com.fasterxml.jackson.databind.ObjectMapper))(io.modelcontextprotocol.spec.McpSchema.Tool mcpTool, io.modelcontextprotocol.client.McpSyncClient mcpSession, [McpSessionManager](McpSessionManager.html)mcpSessionManager, com.fasterxml.jackson.databind.ObjectMapper objectMapper)Creates a new McpTool with the default ObjectMapper. -
## Method Summary

Modifier and TypeMethodDescription[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FunctionDeclaration> Gets the`FunctionDeclaration`

representation of this tool.`io.modelcontextprotocol.client.McpSyncClient`

[runAsync](#runAsync(java.util.Map,com.google.adk.tools.ToolContext))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> args,[ToolContext](../ToolContext.html)toolContext)Calls a tool.`com.google.genai.types.Schema`

[toGeminiSchema](#toGeminiSchema(io.modelcontextprotocol.spec.McpSchema.JsonSchema))(io.modelcontextprotocol.spec.McpSchema.JsonSchema openApiSchema) ### Methods inherited from class com.google.adk.tools.

[BaseTool](../BaseTool.html)[description](../BaseTool.html#description()),[longRunning](../BaseTool.html#longRunning()),[name](../BaseTool.html#name()),[processLlmRequest](../BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))

-
## Constructor Details

-
### McpTool

public McpTool(io.modelcontextprotocol.spec.McpSchema.Tool mcpTool, io.modelcontextprotocol.client.McpSyncClient mcpSession, [McpSessionManager](McpSessionManager.html)mcpSessionManager)Creates a new McpTool with the default ObjectMapper.- Parameters:
`mcpTool`

- The MCP tool to wrap.`mcpSession`

- The MCP session to use to call the tool.`mcpSessionManager`

- The MCP session manager to use to create new sessions.- Throws:

- If mcpTool or mcpSession are null.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)

-
### McpTool

public McpTool(io.modelcontextprotocol.spec.McpSchema.Tool mcpTool, io.modelcontextprotocol.client.McpSyncClient mcpSession, [McpSessionManager](McpSessionManager.html)mcpSessionManager, com.fasterxml.jackson.databind.ObjectMapper objectMapper)Creates a new McpTool with the default ObjectMapper.- Parameters:
`mcpTool`

- The MCP tool to wrap.`mcpSession`

- The MCP session to use to call the tool.`mcpSessionManager`

- The MCP session manager to use to create new sessions.`objectMapper`

- The ObjectMapper to use to convert JSON schemas.- Throws:

- If mcpTool or mcpSession are null.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)


-
-
## Method Details

-
### getMcpSession

public io.modelcontextprotocol.client.McpSyncClient getMcpSession() -
### toGeminiSchema

public com.google.genai.types.Schema toGeminiSchema(io.modelcontextprotocol.spec.McpSchema.JsonSchema openApiSchema) -
### declaration

Description copied from class:[BaseTool](../BaseTool.html#declaration())Gets the`FunctionDeclaration`

representation of this tool.- Overrides:

in class[declaration](../BaseTool.html#declaration())[BaseTool](../BaseTool.html)

-
### runAsync


-


---

<!-- DOCUMENTO FUSIONADO: mcpasynctoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/McpAsyncTool.html -->

# Class McpAsyncTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](../BaseTool.html)

com.google.adk.tools.mcp.McpAsyncTool

Initializes a MCP tool.

This wraps a MCP Tool interface and an active MCP Session. It invokes the MCP Tool through executing the tool from remote MCP Session.

-
## Constructor Summary

ConstructorDescription[McpAsyncTool](#%3Cinit%3E(io.modelcontextprotocol.spec.McpSchema.Tool,io.modelcontextprotocol.client.McpAsyncClient,com.google.adk.tools.mcp.McpSessionManager))(io.modelcontextprotocol.spec.McpSchema.Tool mcpTool, io.modelcontextprotocol.client.McpAsyncClient mcpSession, [McpSessionManager](McpSessionManager.html)mcpSessionManager)Creates a new McpAsyncTool with the default ObjectMapper.[McpAsyncTool](#%3Cinit%3E(io.modelcontextprotocol.spec.McpSchema.Tool,io.modelcontextprotocol.client.McpAsyncClient,com.google.adk.tools.mcp.McpSessionManager,com.fasterxml.jackson.databind.ObjectMapper))(io.modelcontextprotocol.spec.McpSchema.Tool mcpTool, io.modelcontextprotocol.client.McpAsyncClient mcpSession, [McpSessionManager](McpSessionManager.html)mcpSessionManager, com.fasterxml.jackson.databind.ObjectMapper objectMapper)Creates a new McpAsyncTool -
## Method Summary

Modifier and TypeMethodDescription[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FunctionDeclaration> Gets the`FunctionDeclaration`

representation of this tool.`io.modelcontextprotocol.client.McpAsyncClient`

[runAsync](#runAsync(java.util.Map,com.google.adk.tools.ToolContext))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> args,[ToolContext](../ToolContext.html)toolContext)Calls a tool.`com.google.genai.types.Schema`

[toGeminiSchema](#toGeminiSchema(io.modelcontextprotocol.spec.McpSchema.JsonSchema))(io.modelcontextprotocol.spec.McpSchema.JsonSchema openApiSchema) ### Methods inherited from class com.google.adk.tools.

[BaseTool](../BaseTool.html)[description](../BaseTool.html#description()),[longRunning](../BaseTool.html#longRunning()),[name](../BaseTool.html#name()),[processLlmRequest](../BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))

-
## Constructor Details

-
### McpAsyncTool

public McpAsyncTool(io.modelcontextprotocol.spec.McpSchema.Tool mcpTool, io.modelcontextprotocol.client.McpAsyncClient mcpSession, [McpSessionManager](McpSessionManager.html)mcpSessionManager)Creates a new McpAsyncTool with the default ObjectMapper.- Parameters:
`mcpTool`

- The MCP tool to wrap.`mcpSession`

- The MCP session to use to call the tool.`mcpSessionManager`

- The MCP session manager to use to create new sessions.- Throws:

- If mcpTool or mcpSession are null.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)

-
### McpAsyncTool

public McpAsyncTool(io.modelcontextprotocol.spec.McpSchema.Tool mcpTool, io.modelcontextprotocol.client.McpAsyncClient mcpSession, [McpSessionManager](McpSessionManager.html)mcpSessionManager, com.fasterxml.jackson.databind.ObjectMapper objectMapper)Creates a new McpAsyncTool- Parameters:
`mcpTool`

- The MCP tool to wrap.`mcpSession`

- The MCP session to use to call the tool.`mcpSessionManager`

- The MCP session manager to use to create new sessions.`objectMapper`

- The ObjectMapper to use to convert JSON schemas.- Throws:

- If mcpTool or mcpSession are null.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)


-
-
## Method Details

-
### getMcpSession

public io.modelcontextprotocol.client.McpAsyncClient getMcpSession() -
### toGeminiSchema

public com.google.genai.types.Schema toGeminiSchema(io.modelcontextprotocol.spec.McpSchema.JsonSchema openApiSchema) -
### declaration

Description copied from class:[BaseTool](../BaseTool.html#declaration())Gets the`FunctionDeclaration`

representation of this tool.- Overrides:

in class[declaration](../BaseTool.html#declaration())[BaseTool](../BaseTool.html)

-
### runAsync


-


---

<!-- DOCUMENTO FUSIONADO: mcptoolsethtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/mcp/McpToolset.html -->

# Class McpToolset

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.mcp.McpToolset

- All Implemented Interfaces:

,[BaseToolset](../BaseToolset.html)[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

Connects to a MCP Server, and retrieves MCP Tools into ADK Tools.

Attributes:

`connectionParams`

: The connection parameters to the MCP server. Can be either`ServerParameters`

or`SseServerParameters`

.`session`

: The MCP session being initialized with the connection.

-
## Nested Class Summary

Modifier and TypeClassDescription`static class`

Exception thrown when there's an error during MCP session initialization.`static class`

Exception thrown when there's an error during loading tools from the MCP server.`static class`

Base exception for all errors originating from`McpToolset`

. -
## Constructor Summary

ConstructorDescription[McpToolset](#%3Cinit%3E(com.google.adk.tools.mcp.McpSessionManager,com.fasterxml.jackson.databind.ObjectMapper,java.util.Optional))( [McpSessionManager](McpSessionManager.html)mcpSessionManager, com.fasterxml.jackson.databind.ObjectMapper objectMapper,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter)Initializes the McpToolset with an McpSessionManager.[McpToolset](#%3Cinit%3E(com.google.adk.tools.mcp.SseServerParameters))( [SseServerParameters](SseServerParameters.html)connectionParams)Initializes the McpToolset with SSE server parameters, using the ObjectMapper used across the ADK and no tool filter.[McpToolset](#%3Cinit%3E(com.google.adk.tools.mcp.SseServerParameters,com.fasterxml.jackson.databind.ObjectMapper))( [SseServerParameters](SseServerParameters.html)connectionParams, com.fasterxml.jackson.databind.ObjectMapper objectMapper)Initializes the McpToolset with SSE server parameters and no tool filter.[McpToolset](#%3Cinit%3E(com.google.adk.tools.mcp.SseServerParameters,com.fasterxml.jackson.databind.ObjectMapper,java.util.Optional))( [SseServerParameters](SseServerParameters.html)connectionParams, com.fasterxml.jackson.databind.ObjectMapper objectMapper,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter)Initializes the McpToolset with SSE server parameters.[McpToolset](#%3Cinit%3E(com.google.adk.tools.mcp.SseServerParameters,java.util.Optional))( [SseServerParameters](SseServerParameters.html)connectionParams,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter)Initializes the McpToolset with SSE server parameters, using the ObjectMapper used across the ADK.[McpToolset](#%3Cinit%3E(io.modelcontextprotocol.client.transport.ServerParameters))(io.modelcontextprotocol.client.transport.ServerParameters connectionParams) Initializes the McpToolset with local server parameters, using the ObjectMapper used across the ADK and no tool filter.[McpToolset](#%3Cinit%3E(io.modelcontextprotocol.client.transport.ServerParameters,com.fasterxml.jackson.databind.ObjectMapper))(io.modelcontextprotocol.client.transport.ServerParameters connectionParams, com.fasterxml.jackson.databind.ObjectMapper objectMapper) Initializes the McpToolset with local server parameters and no tool filter.[McpToolset](#%3Cinit%3E(io.modelcontextprotocol.client.transport.ServerParameters,com.fasterxml.jackson.databind.ObjectMapper,java.util.Optional))(io.modelcontextprotocol.client.transport.ServerParameters connectionParams, com.fasterxml.jackson.databind.ObjectMapper objectMapper, [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter)Initializes the McpToolset with local server parameters.[McpToolset](#%3Cinit%3E(io.modelcontextprotocol.client.transport.ServerParameters,java.util.Optional))(io.modelcontextprotocol.client.transport.ServerParameters connectionParams, [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter)Initializes the McpToolset with local server parameters, using the ObjectMapper used across the ADK. -
## Method Summary

Modifier and TypeMethodDescription`void`

[close](#close())()Performs cleanup and releases resources held by the toolset.`io.reactivex.rxjava3.core.Flowable`

< [BaseTool](../BaseTool.html)>[getTools](#getTools(com.google.adk.agents.ReadonlyContext))( [ReadonlyContext](../../agents/ReadonlyContext.html)readonlyContext)Return all tools in the toolset based on the provided context.### Methods inherited from class java.lang.

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)[clone](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#clone()),[equals](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#equals(java.lang.Object)),[finalize](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#finalize()),[getClass](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#getClass()),[hashCode](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#hashCode()),[notify](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notify()),[notifyAll](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notifyAll()),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#toString()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long)),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long,int))### Methods inherited from interface com.google.adk.tools.

[BaseToolset](../BaseToolset.html)[isToolSelected](../BaseToolset.html#isToolSelected(com.google.adk.tools.BaseTool,java.util.Optional,java.util.Optional))

-
## Constructor Details

-
### McpToolset

public McpToolset( [SseServerParameters](SseServerParameters.html)connectionParams, com.fasterxml.jackson.databind.ObjectMapper objectMapper,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter)Initializes the McpToolset with SSE server parameters.- Parameters:
`connectionParams`

- The SSE connection parameters to the MCP server.`objectMapper`

- An ObjectMapper instance for parsing schemas.`toolFilter`

- An Optional containing either a ToolPredicate or a List of tool names.

-
### McpToolset

public McpToolset( [SseServerParameters](SseServerParameters.html)connectionParams, com.fasterxml.jackson.databind.ObjectMapper objectMapper)Initializes the McpToolset with SSE server parameters and no tool filter.- Parameters:
`connectionParams`

- The SSE connection parameters to the MCP server.`objectMapper`

- An ObjectMapper instance for parsing schemas.

-
### McpToolset

public McpToolset(io.modelcontextprotocol.client.transport.ServerParameters connectionParams, com.fasterxml.jackson.databind.ObjectMapper objectMapper, [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter)Initializes the McpToolset with local server parameters.- Parameters:
`connectionParams`

- The local server connection parameters to the MCP server.`objectMapper`

- An ObjectMapper instance for parsing schemas.`toolFilter`

- An Optional containing either a ToolPredicate or a List of tool names.

-
### McpToolset

public McpToolset(io.modelcontextprotocol.client.transport.ServerParameters connectionParams, com.fasterxml.jackson.databind.ObjectMapper objectMapper) Initializes the McpToolset with local server parameters and no tool filter.- Parameters:
`connectionParams`

- The local server connection parameters to the MCP server.`objectMapper`

- An ObjectMapper instance for parsing schemas.

-
### McpToolset

Initializes the McpToolset with SSE server parameters, using the ObjectMapper used across the ADK.- Parameters:
`connectionParams`

- The SSE connection parameters to the MCP server.`toolFilter`

- An Optional containing either a ToolPredicate or a List of tool names.

-
### McpToolset

Initializes the McpToolset with SSE server parameters, using the ObjectMapper used across the ADK and no tool filter.- Parameters:
`connectionParams`

- The SSE connection parameters to the MCP server.

-
### McpToolset

public McpToolset(io.modelcontextprotocol.client.transport.ServerParameters connectionParams, [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter)Initializes the McpToolset with local server parameters, using the ObjectMapper used across the ADK.- Parameters:
`connectionParams`

- The local server connection parameters to the MCP server.`toolFilter`

- An Optional containing either a ToolPredicate or a List of tool names.

-
### McpToolset

public McpToolset(io.modelcontextprotocol.client.transport.ServerParameters connectionParams) Initializes the McpToolset with local server parameters, using the ObjectMapper used across the ADK and no tool filter.- Parameters:
`connectionParams`

- The local server connection parameters to the MCP server.

-
### McpToolset

public McpToolset( [McpSessionManager](McpSessionManager.html)mcpSessionManager, com.fasterxml.jackson.databind.ObjectMapper objectMapper,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> toolFilter)Initializes the McpToolset with an McpSessionManager.- Parameters:
`mcpSessionManager`

- A McpSessionManager instance for testing.`objectMapper`

- An ObjectMapper instance for parsing schemas.`toolFilter`

- An Optional containing either a ToolPredicate or a List of tool names.


-
-
## Method Details

-
### getTools

Description copied from interface:[BaseToolset](../BaseToolset.html#getTools(com.google.adk.agents.ReadonlyContext))Return all tools in the toolset based on the provided context.- Specified by:

in interface[getTools](../BaseToolset.html#getTools(com.google.adk.agents.ReadonlyContext))[BaseToolset](../BaseToolset.html)- Parameters:
`readonlyContext`

- Context used to filter tools available to the agent.- Returns:
- A Single emitting a list of tools available under the specified context.

-
### close

public void close()Description copied from interface:[BaseToolset](../BaseToolset.html#close())Performs cleanup and releases resources held by the toolset.NOTE: This method is invoked, for example, at the end of an agent server's lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.

- Specified by:

in interface[close](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html#close())[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)- Specified by:

in interface[close](../BaseToolset.html#close())[BaseToolset](../BaseToolset.html)


-
