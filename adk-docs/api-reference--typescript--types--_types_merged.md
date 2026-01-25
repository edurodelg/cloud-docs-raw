---
merged_at: 2026-01-25T03:28:16.226552
merged_files: 9
---

# Documentos Fusionados

Este archivo contiene 9 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: singleaftertoolcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/types/SingleAfterToolCallback.html -->

# Type Alias SingleAfterToolCallback

A callback that runs after a tool is called.

When present, the returned dict will be used as tool result.

A callback that runs after a tool is called.


---

<!-- DOCUMENTO FUSIONADO: singlebeforetoolcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/types/SingleBeforeToolCallback.html -->

# Type Alias SingleBeforeToolCallback

A callback that runs before a tool is called.

The tool response. When present, the returned tool response will be used and the framework will skip calling the actual tool.

A callback that runs before a tool is called.


---

<!-- DOCUMENTO FUSIONADO: singlebeforemodelcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/types/SingleBeforeModelCallback.html -->

# Type Alias SingleBeforeModelCallback

A callback that runs before a request is sent to the model.

The content to return to the user. When present, the model call will be skipped and the provided content will be returned to user.

A callback that runs before a request is sent to the model.


---

<!-- DOCUMENTO FUSIONADO: singleaftermodelcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/types/SingleAfterModelCallback.html -->

# Type Alias SingleAfterModelCallback

A callback that runs after a response is received from the model.

The content to return to the user. When present, the actual model response will be ignored and the provided content will be returned to user.

A callback that runs after a response is received from the model.


---

<!-- DOCUMENTO FUSIONADO: aftertoolcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/types/AfterToolCallback.html -->

# Type Alias AfterToolCallback

A single callback or a list of callbacks.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until acallback does not return None.

A single callback or a list of callbacks.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until acallback does not return None.


---

<!-- DOCUMENTO FUSIONADO: beforetoolcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/types/BeforeToolCallback.html -->

# Type Alias BeforeToolCallback

A single callback or a list of callbacks.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

A single callback or a list of callbacks.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.


---

<!-- DOCUMENTO FUSIONADO: aftermodelcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/types/AfterModelCallback.html -->

# Type Alias AfterModelCallback

A single callback or a list of callbacks.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

A single callback or a list of callbacks.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.


---

<!-- DOCUMENTO FUSIONADO: beforemodelcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/types/BeforeModelCallback.html -->

# Type Alias BeforeModelCallback

A single callback or a list of callbacks.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.

A single callback or a list of callbacks.

When a list of callbacks is provided, the callbacks will be called in the order they are listed until a callback does not return None.


---

<!-- DOCUMENTO FUSIONADO: mcpconnectionparamshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/types/MCPConnectionParams.html -->

# Type Alias MCPConnectionParams

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
MCPConnectionParams
Type Alias MCPConnectionParams
MCPConnectionParams
:
StdioConnectionParams
|
StreamableHTTPConnectionParams
A union of all supported MCP connection parameter types.
ADK for TypeScript: API Reference
Loading...

A union of all supported MCP connection parameter types.
