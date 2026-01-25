---
merged_at: 2026-01-25T02:21:31.632727
merged_files: 36
---

# Documentos Fusionados

Este archivo contiene 36 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: searchmemoryresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/SearchMemoryResponse.html -->

# Interface SearchMemoryResponse

Represents the response from a memory search.

A list of memory entries that are related to the search query.

Represents the response from a memory search.


---

<!-- DOCUMENTO FUSIONADO: listversionsrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/ListVersionsRequest.html -->

# Interface ListVersionsRequest

The parameters for listVersions.

listVersions

The app name.

The filename of the artifact.

The session ID.

The user ID.

The parameters for

`listVersions`

.


---

<!-- DOCUMENTO FUSIONADO: deletesessionrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/DeleteSessionRequest.html -->

# Interface DeleteSessionRequest

The parameters for deleteSession.

deleteSession

The name of the application.

The ID of the session.

The ID of the user.

The parameters for

`deleteSession`

.


---

<!-- DOCUMENTO FUSIONADO: getsessionconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/GetSessionConfig.html -->

# Interface GetSessionConfig

The configuration of getting a session.

Optional

Retrieve events after this timestamp.

The number of recent events to retrieve.

The configuration of getting a session.


---

<!-- DOCUMENTO FUSIONADO: deleteartifactrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/DeleteArtifactRequest.html -->

# Interface DeleteArtifactRequest

The parameters for deleteArtifact.

deleteArtifact

The app name.

The filename of the artifact.

The session ID.

The user ID.

The parameters for

`deleteArtifact`

.


---

<!-- DOCUMENTO FUSIONADO: saveartifactrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/SaveArtifactRequest.html -->

# Interface SaveArtifactRequest

The parameters for saveArtifact.

saveArtifact

The app name.

The artifact to save.

The filename of the artifact.

The session ID.

The user ID.

The parameters for

`saveArtifact`

.


---

<!-- DOCUMENTO FUSIONADO: getsessionrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/GetSessionRequest.html -->

# Interface GetSessionRequest

The parameters for getSession.

getSession

The name of the application.

Optional

The configurations for getting the session.

The ID of the session.

The ID of the user.

The parameters for

`getSession`

.


---

<!-- DOCUMENTO FUSIONADO: listsessionsresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/ListSessionsResponse.html -->

# Interface ListSessionsResponse

The response of listing sessions.

The events and states are not set within each Session object.

A list of sessions.

The response of listing sessions.

The events and states are not set within each Session object.


---

<!-- DOCUMENTO FUSIONADO: createsessionrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/CreateSessionRequest.html -->

# Interface CreateSessionRequest

The parameters for createSession.

createSession

The name of the application.

Optional

The ID of the session. A new ID will be generated if not provided.

The initial state of the session.

The ID of the user.

The parameters for

`createSession`

.


---

<!-- DOCUMENTO FUSIONADO: loadartifactrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/LoadArtifactRequest.html -->

# Interface LoadArtifactRequest

The parameters for loadArtifact.

loadArtifact

The app name.

The filename of the artifact.

The session ID.

The user ID.

Optional

The version of the artifact to load. If not provided, the latest version of the artifact is loaded.

The parameters for

`loadArtifact`

.


---

<!-- DOCUMENTO FUSIONADO: policycheckresulthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/PolicyCheckResult.html -->

# Interface PolicyCheckResult

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
PolicyCheckResult
Interface PolicyCheckResult
interface
PolicyCheckResult
{
outcome
:
string
;
reason
?:
string
;
}
Properties
outcome
outcome
:
string
Optional
reason
reason
?:
string
Properties
outcome
reason
ADK for TypeScript: API Reference
Loading...


---

<!-- DOCUMENTO FUSIONADO: sessionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/Session.html -->

# Interface Session

Represents a session in a conversation between agents and users.

The name of the app.

The events of the session, e.g. user input, model response, function call/response, etc.

The unique identifier of the session.

The last update time of the session.

The state of the session.

The id of the user.

Represents a session in a conversation between agents and users.


---

<!-- DOCUMENTO FUSIONADO: llmrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/LlmRequest.html -->

# Interface LlmRequest

`Optional`

configAdditional config for the generate content request. Tools in generateContentConfig should not be set directly; use appendTools.

The contents to send to the model.

`Optional`

modelThe model name.

The tools dictionary. Excluded from JSON serialization.

LLM request class that allows passing in tools, output schema and system instructions to the model.


---

<!-- DOCUMENTO FUSIONADO: liverequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/LiveRequest.html -->

# Interface LiveRequest

`Optional`

activityIf set, signal the end of user activity to the model.

`Optional`

activityIf set, signal the start of user activity to the model.

`Optional`

blobIf set, send the blob to the model in realtime mode.

`Optional`

closeIf set, close the queue.

`Optional`

contentIf set, send the content to the model in turn-by-turn mode.

Request sent to live agents.


---

<!-- DOCUMENTO FUSIONADO: stdioconnectionparamshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/StdioConnectionParams.html -->

# Interface StdioConnectionParams

Defines the parameters for establishing a connection to an MCP server using standard input/output (stdio). This is typically used for running MCP servers as local child processes.

Optional

Defines the parameters for establishing a connection to an MCP server using standard input/output (stdio). This is typically used for running MCP servers as local child processes.


---

<!-- DOCUMENTO FUSIONADO: otelhookshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/OTelHooks.html -->

# Interface OTelHooks

Configuration hooks for OpenTelemetry setup.

This interface defines the structure for configuring OpenTelemetry components including span processors, metric readers, and log record processors.

Optional

Configuration hooks for OpenTelemetry setup.

This interface defines the structure for configuring OpenTelemetry components including span processors, metric readers, and log record processors.


---

<!-- DOCUMENTO FUSIONADO: toolcallpolicycontexthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/ToolCallPolicyContext.html -->

# Interface ToolCallPolicyContext

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
ToolCallPolicyContext
Interface ToolCallPolicyContext
interface
ToolCallPolicyContext
{
tool
:
BaseTool
;
toolArgs
:
Record
<
string
,
unknown
>
;
}
Properties
tool
tool
:
BaseTool
tool
Args
toolArgs
:
Record
<
string
,
unknown
>
Properties
tool
tool
Args
ADK for TypeScript: API Reference
Loading...


---

<!-- DOCUMENTO FUSIONADO: basememoryservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/BaseMemoryService.html -->

# Interface BaseMemoryService

Adds a session to the memory.

The session to add to the memory.

A promise that resolves when the session is added to the memory.

Searches for sessions that match the query.

The request to search memory.

A promise that resolves to SearchMemoryResponse containing the matching memories.

Base interface for memory services.

The service provides functionalities to ingest sessions into memory so that the memory can be used for user queries.


---

<!-- DOCUMENTO FUSIONADO: appendeventrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/AppendEventRequest.html -->

# Interface AppendEventRequest

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
AppendEventRequest
Interface AppendEventRequest
The parameters for
appendEvent
.
interface
AppendEventRequest
{
event
:
Event
;
session
:
Session
;
}
Properties
event
event
:
Event
The event to append.
session
session
:
Session
The session to append the event to.
Properties
event
session
ADK for TypeScript: API Reference
Loading...

The parameters for

`appendEvent`

.


---

<!-- DOCUMENTO FUSIONADO: searchmemoryrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/SearchMemoryRequest.html -->

# Interface SearchMemoryRequest

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
SearchMemoryRequest
Interface SearchMemoryRequest
The parameters for
searchMemory
.
interface
SearchMemoryRequest
{
appName
:
string
;
query
:
string
;
userId
:
string
;
}
Properties
app
Name
appName
:
string
query
query
:
string
user
Id
userId
:
string
Properties
app
Name
query
user
Id
ADK for TypeScript: API Reference
Loading...

The parameters for

`searchMemory`

.


---

<!-- DOCUMENTO FUSIONADO: listsessionsrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/ListSessionsRequest.html -->

# Interface ListSessionsRequest

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
ListSessionsRequest
Interface ListSessionsRequest
The parameters for
listSessions
.
interface
ListSessionsRequest
{
appName
:
string
;
userId
:
string
;
}
Properties
app
Name
appName
:
string
The name of the application.
user
Id
userId
:
string
The ID of the user.
Properties
app
Name
user
Id
ADK for TypeScript: API Reference
Loading...

The parameters for

`listSessions`

.


---

<!-- DOCUMENTO FUSIONADO: runasynctoolrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/RunAsyncToolRequest.html -->

# Interface RunAsyncToolRequest

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
RunAsyncToolRequest
Interface RunAsyncToolRequest
The parameters for
runAsync
.
interface
RunAsyncToolRequest
{
args
:
Record
<
string
,
unknown
>
;
toolContext
:
ToolContext
;
}
Properties
args
args
:
Record
<
string
,
unknown
>
tool
Context
toolContext
:
ToolContext
Properties
args
tool
Context
ADK for TypeScript: API Reference
Loading...

The parameters for

`runAsync`

.


---

<!-- DOCUMENTO FUSIONADO: toolprocessllmrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/ToolProcessLlmRequest.html -->

# Interface ToolProcessLlmRequest

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
ToolProcessLlmRequest
Interface ToolProcessLlmRequest
The parameters for
processLlmRequest
.
interface
ToolProcessLlmRequest
{
llmRequest
:
LlmRequest
;
toolContext
:
ToolContext
;
}
Properties
llm
Request
llmRequest
:
LlmRequest
tool
Context
toolContext
:
ToolContext
Properties
llm
Request
tool
Context
ADK for TypeScript: API Reference
Loading...

The parameters for

`processLlmRequest`

.


---

<!-- DOCUMENTO FUSIONADO: basetoolparamshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/BaseToolParams.html -->

# Interface BaseToolParams

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
BaseToolParams
Interface BaseToolParams
Parameters for the BaseTool constructor.
interface
BaseToolParams
{
description
:
string
;
isLongRunning
?:
boolean
;
name
:
string
;
}
Properties
description
description
:
string
Optional
is
Long
Running
isLongRunning
?:
boolean
name
name
:
string
Properties
description
is
Long
Running
name
ADK for TypeScript: API Reference
Loading...

Parameters for the BaseTool constructor.


---

<!-- DOCUMENTO FUSIONADO: basepolicyenginehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/BasePolicyEngine.html -->

# Interface BasePolicyEngine

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
BasePolicyEngine
Interface BasePolicyEngine
interface
BasePolicyEngine
{
evaluate
(
context
:
ToolCallPolicyContext
)
:
Promise
<
PolicyCheckResult
>
;
}
Implemented by
InMemoryPolicyEngine
Methods
evaluate
evaluate
(
context
:
ToolCallPolicyContext
)
:
Promise
<
PolicyCheckResult
>
Parameters
context
:
ToolCallPolicyContext
Returns
Promise
<
PolicyCheckResult
>
Methods
evaluate
ADK for TypeScript: API Reference
Loading...


---

<!-- DOCUMENTO FUSIONADO: otelexportersconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/OtelExportersConfig.html -->

# Interface OtelExportersConfig

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
OtelExportersConfig
Interface OtelExportersConfig
interface
OtelExportersConfig
{
enableLogging
?:
boolean
;
enableMetrics
?:
boolean
;
enableTracing
?:
boolean
;
}
Properties
Optional
enable
Logging
enableLogging
?:
boolean
Optional
enable
Metrics
enableMetrics
?:
boolean
Optional
enable
Tracing
enableTracing
?:
boolean
Properties
enable
Logging
enable
Metrics
enable
Tracing
ADK for TypeScript: API Reference
Loading...


---

<!-- DOCUMENTO FUSIONADO: basecredentialservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/BaseCredentialService.html -->

# Interface BaseCredentialService

Loads the credential by auth config and current tool context from the backend credential store.

The auth config which contains the auth scheme and auth credential information. auth_config.get_credential_key will be used to build the key to load the credential.

The context of the current invocation when the tool is trying to load the credential.

A promise that resolves to the credential saved in the store.

Abstract class for Service that loads / saves tool credentials from / to the backend credential store.


---

<!-- DOCUMENTO FUSIONADO: listartifactkeysrequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/ListArtifactKeysRequest.html -->

# Interface ListArtifactKeysRequest

ADK for TypeScript: API Reference
System
Light
Dark
Search…
Preparing search index...
ListArtifactKeysRequest
Interface ListArtifactKeysRequest
The parameters for
listArtifactKeys
.
interface
ListArtifactKeysRequest
{
appName
:
string
;
sessionId
:
string
;
userId
:
string
;
}
Properties
app
Name
appName
:
string
The app name.
session
Id
sessionId
:
string
The session ID.
user
Id
userId
:
string
The user ID.
Properties
app
Name
session
Id
user
Id
ADK for TypeScript: API Reference
Loading...

The parameters for

`listArtifactKeys`

.


---

<!-- DOCUMENTO FUSIONADO: streamablehttpconnectionparamshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/StreamableHTTPConnectionParams.html -->

# Interface StreamableHTTPConnectionParams

Defines the parameters for establishing a connection to an MCP server over HTTP using Server-Sent Events (SSE) for streaming.

Usage: const connectionParams: StreamableHTTPConnectionParams = { type: 'StreamableHTTPConnectionParams', url: 'http://localhost:8788/mcp' };

Optional

Defines the parameters for establishing a connection to an MCP server over HTTP using Server-Sent Events (SSE) for streaming.

Usage: const connectionParams: StreamableHTTPConnectionParams = { type: 'StreamableHTTPConnectionParams', url: 'http://localhost:8788/mcp' };


---

<!-- DOCUMENTO FUSIONADO: geminiparamshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/GeminiParams.html -->

# Interface GeminiParams

`Optional`

apiThe API key to use for the Gemini API. If not provided, it will look for the GOOGLE_GENAI_API_KEY or GEMINI_API_KEY environment variable.

`Optional`

headersHeaders to merge with internally crafted headers.

`Optional`

locationThe Vertex AI location. Required if `vertexai`

is true.

`Optional`

modelThe name of the model to use. Defaults to 'gemini-2.5-flash'.

`Optional`

projectThe Vertex AI project ID. Required if `vertexai`

is true.

`Optional`

vertexaiWhether to use Vertex AI. If true, `project`

, `location`

should be provided.

The parameters for creating a Gemini instance.


---

<!-- DOCUMENTO FUSIONADO: eventactionshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/EventActions.html -->

# Interface EventActions

Indicates that the event is updating an artifact. key is the filename, value is the version.

`Optional`

escalateThe agent is escalating to a higher level agent.

Authentication configurations requested by tool responses.

This field will only be set by a tool response event indicating tool request auth credential.

A dict of tool confirmation requested by this event, keyed by the function call id.

`Optional`

skipIf true, it won't call model to summarize function response. Only used for function_response event.

Indicates that the event is updating the state with the given delta.

`Optional`

transferIf set, the event transfers to the specified agent.

Represents the actions attached to an event.


---

<!-- DOCUMENTO FUSIONADO: basellmconnectionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/BaseLlmConnection.html -->

# Interface BaseLlmConnection

Closes the llm server connection.

Receives the model response using the llm server connection.

A generator of LlmResponse.

Sends the content to the model.

The model will respond immediately upon receiving the content. If you send function responses, all parts in the content should be function responses.

The content to send to the model.

Sends the conversation history to the model.

You call this method right after setting up the model connection. The model will respond if the last content is from user, otherwise it will wait for new user input before responding.

The conversation history to send to the model.

Sends a chunk of audio or a frame of video to the model in realtime.

The model may not respond immediately upon receiving the blob. It will do voice activity detection and decide when to respond.

The blob to send to the model.

The base class for a live model connection.


---

<!-- DOCUMENTO FUSIONADO: baseartifactservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/BaseArtifactService.html -->

# Interface BaseArtifactService

Deletes an artifact.

The request to delete an artifact.

A promise that resolves when the artifact is deleted.

Lists all the artifact filenames within a session.

The request to list artifact keys.

A promise that resolves to a list of all artifact filenames within a session.

Lists all versions of an artifact.

The request to list versions.

A promise that resolves to a list of all available versions of the artifact.

Gets an artifact from the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename.

The request to load an artifact.

A promise that resolves to the artifact or undefined if not found.

Saves an artifact to the artifact service storage.

The artifact is a file identified by the app name, user ID, session ID, and filename. After saving the artifact, a revision ID is returned to identify the artifact version.

The request to save an artifact.

A promise that resolves to The revision ID. The first version of the artifact has a revision ID of 0. This is incremented by 1 after each successful save.

Interface for artifact services.


---

<!-- DOCUMENTO FUSIONADO: runconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/RunConfig.html -->

# Interface RunConfig

`Optional`

enableIf enabled, the model will detect emotions and adapt its responses accordingly.

`Optional`

inputInput transcription for live agents with audio input from user.

`Optional`

maxA limit on the total number of llm calls for a given run.

Valid Values:

`Optional`

outputOutput audio transcription config.

`Optional`

proactivityConfigures the proactivity of the model. This allows the model to respond proactively to the input and to ignore irrelevant input.

`Optional`

realtimeRealtime input config for live agents with audio input from user.

`Optional`

responseThe output modalities. If not set, it's default to AUDIO.

`Optional`

saveWhether or not to save the input blobs as artifacts.

`Optional`

speechSpeech configuration for the live agent.

`Optional`

streamingStreaming mode, None or StreamingMode.SSE or StreamingMode.BIDI.

`Optional`

supportWhether to support CFC (Compositional Function Calling). Only applicable for StreamingMode.SSE. If it's true. the LIVE API will be invoked. Since only LIVE API supports CFC

WARNING: This feature is **experimental** and its API or behavior may
change in future releases.

Configs for runtime behavior of agents.


---

<!-- DOCUMENTO FUSIONADO: llmresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/LlmResponse.html -->

# Interface LlmResponse

`Optional`

contentThe content of the response.

`Optional`

customThe custom metadata of the LlmResponse. An optional key-value pair to label an LlmResponse. NOTE: the entire object must be JSON serializable.

`Optional`

errorError code if the response is an error. Code varies by model.

`Optional`

errorError message if the response is an error.

`Optional`

finishThe finish reason of the response.

`Optional`

groundingThe grounding metadata of the response.

`Optional`

inputAudio transcription of user input.

`Optional`

interruptedFlag indicating that LLM was interrupted when generating the content. Usually it's due to user interruption during a bidi streaming.

`Optional`

liveThe session resumption update of the LlmResponse

`Optional`

outputAudio transcription of model output.

`Optional`

partialIndicates whether the text content is part of a unfinished text stream. Only used for streaming mode and when the content is plain text.

`Optional`

turnIndicates whether the response from the model is complete. Only used for streaming mode.

`Optional`

usageThe usage metadata of the LlmResponse.

LLM response class that provides the first candidate response from the model if available. Otherwise, returns error code and message.


---

<!-- DOCUMENTO FUSIONADO: eventhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/typescript/interfaces/Event.html -->

# Interface Event

The actions taken by the agent.

`Optional`

author"user" or the name of the agent, indicating who appended the event to the session.

`Optional`

branchThe branch of the event. The format is like agent_1.agent_2.agent_3, where agent_1 is the parent of agent_2, and agent_2 is the parent of agent_3.

Branch is used when multiple sub-agent shouldn't see their peer agents' conversation history.

`Optional`

contentThe content of the response.

`Optional`

customThe custom metadata of the LlmResponse. An optional key-value pair to label an LlmResponse. NOTE: the entire object must be JSON serializable.

`Optional`

errorError code if the response is an error. Code varies by model.

`Optional`

errorError message if the response is an error.

`Optional`

finishThe finish reason of the response.

`Optional`

groundingThe grounding metadata of the response.

The unique identifier of the event. Do not assign the ID. It will be assigned by the session.

`Optional`

inputAudio transcription of user input.

`Optional`

interruptedFlag indicating that LLM was interrupted when generating the content. Usually it's due to user interruption during a bidi streaming.

The invocation ID of the event. Should be non-empty before appending to a session.

`Optional`

liveThe session resumption update of the LlmResponse

`Optional`

longSet of ids of the long running function calls. Agent client will know from this field about which function call is long running. Only valid for function call event

`Optional`

outputAudio transcription of model output.

`Optional`

partialIndicates whether the text content is part of a unfinished text stream. Only used for streaming mode and when the content is plain text.

The timestamp of the event.

`Optional`

turnIndicates whether the response from the model is complete. Only used for streaming mode.

`Optional`

usageThe usage metadata of the LlmResponse.

Represents an event in a conversation between agents and users.

It is used to store the content of the conversation, as well as the actions taken by the agents like function calls, etc.
