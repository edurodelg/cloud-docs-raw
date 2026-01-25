---
merged_at: 2026-01-25T03:28:16.294186
merged_files: 5
---

# Documentos Fusionados

Este archivo contiene 5 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: eventstreamhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/class-use/EventStream.html -->

# Uses of Classcom.google.adk.events.EventStream

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.events
EventStream
Uses of Class
com.google.adk.events.EventStream
No usage of com.google.adk.events.EventStream


---

<!-- DOCUMENTO FUSIONADO: eventactionshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/class-use/EventActions.html -->

# Uses of Classcom.google.adk.events.EventActions

# Uses of Class

com.google.adk.events.EventActions

-
## Uses of

[EventActions](../EventActions.html)in[com.google.adk.agents](../../agents/package-summary.html)Modifier and TypeMethodDescriptionCallbackContext.[eventActions](../../agents/CallbackContext.html#eventActions())()Returns the EventActions associated with this context.ModifierConstructorDescription[CallbackContext](../../agents/CallbackContext.html#%3Cinit%3E(com.google.adk.agents.InvocationContext,com.google.adk.events.EventActions))( [InvocationContext](../../agents/InvocationContext.html)invocationContext,[EventActions](../EventActions.html)eventActions)Initializes callback context. -
## Uses of

[EventActions](../EventActions.html)in[com.google.adk.events](../package-summary.html)Modifier and TypeMethodDescriptionEvent.Builder.[actions](../Event.Builder.html#actions(com.google.adk.events.EventActions))( [EventActions](../EventActions.html)value)EventActions.Builder.[merge](../EventActions.Builder.html#merge(com.google.adk.events.EventActions))( [EventActions](../EventActions.html)other)`void`

Event.[setActions](../Event.html#setActions(com.google.adk.events.EventActions))( [EventActions](../EventActions.html)actions) -
## Uses of

[EventActions](../EventActions.html)in[com.google.adk.tools](../../tools/package-summary.html)Modifier and TypeMethodDescriptionToolContext.Builder.[actions](../../tools/ToolContext.Builder.html#actions(com.google.adk.events.EventActions))( [EventActions](../EventActions.html)actions)`void`

ToolContext.[setActions](../../tools/ToolContext.html#setActions(com.google.adk.events.EventActions))( [EventActions](../EventActions.html)actions)


---

<!-- DOCUMENTO FUSIONADO: eventactionsbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/class-use/EventActions.Builder.html -->

# Uses of Classcom.google.adk.events.EventActions.Builder

# Uses of Class

com.google.adk.events.EventActions.Builder

-
## Uses of

[EventActions.Builder](../EventActions.Builder.html)in[com.google.adk.events](../package-summary.html)Modifier and TypeMethodDescriptionEventActions.Builder.[artifactDelta](../EventActions.Builder.html#artifactDelta(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html), com.google.genai.types.Part> value)`static`

[EventActions.Builder](../EventActions.Builder.html)EventActions.[builder](../EventActions.html#builder())()EventActions.Builder.[endInvocation](../EventActions.Builder.html#endInvocation(boolean))(boolean endInvocation) EventActions.Builder.[escalate](../EventActions.Builder.html#escalate(boolean))(boolean escalate) EventActions.Builder.[merge](../EventActions.Builder.html#merge(com.google.adk.events.EventActions))( [EventActions](../EventActions.html)other)EventActions.Builder.[requestedAuthConfigs](../EventActions.Builder.html#requestedAuthConfigs(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>> value)EventActions.Builder.[skipSummarization](../EventActions.Builder.html#skipSummarization(boolean))(boolean skipSummarization) EventActions.Builder.[stateDelta](../EventActions.Builder.html#stateDelta(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> value)EventActions.[toBuilder](../EventActions.html#toBuilder())()EventActions.Builder.[transferToAgent](../EventActions.Builder.html#transferToAgent(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)agentId)


---

<!-- DOCUMENTO FUSIONADO: eventbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/class-use/Event.Builder.html -->

# Uses of Classcom.google.adk.events.Event.Builder

# Uses of Class

com.google.adk.events.Event.Builder

-
## Uses of

[Event.Builder](../Event.Builder.html)in[com.google.adk.events](../package-summary.html)Modifier and TypeMethodDescriptionEvent.Builder.[actions](../Event.Builder.html#actions(com.google.adk.events.EventActions))( [EventActions](../EventActions.html)value)`static`

[Event.Builder](../Event.Builder.html)Event.[builder](../Event.html#builder())()Event.Builder.[content](../Event.Builder.html#content(com.google.genai.types.Content))(com.google.genai.types.Content value) Event.Builder.[errorCode](../Event.Builder.html#errorCode(com.google.genai.types.FinishReason))(com.google.genai.types.FinishReason value) Event.Builder.[errorMessage](../Event.Builder.html#errorMessage(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)value)Event.Builder.[errorMessage](../Event.Builder.html#errorMessage(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> value)Event.Builder.[groundingMetadata](../Event.Builder.html#groundingMetadata(com.google.genai.types.GroundingMetadata))(com.google.genai.types.GroundingMetadata value) Event.Builder.[groundingMetadata](../Event.Builder.html#groundingMetadata(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GroundingMetadata> value)Event.Builder.[interrupted](../Event.Builder.html#interrupted(java.lang.Boolean))( [Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)value)Event.Builder.[interrupted](../Event.Builder.html#interrupted(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> value)Event.Builder.[invocationId](../Event.Builder.html#invocationId(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)value)Event.Builder.[longRunningToolIds](../Event.Builder.html#longRunningToolIds(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Set](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Set.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>> value)Event.Builder.[longRunningToolIds](../Event.Builder.html#longRunningToolIds(java.util.Set))( [Set](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Set.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> value)Event.Builder.[timestamp](../Event.Builder.html#timestamp(long))(long value) Event.[toBuilder](../Event.html#toBuilder())()Creates a builder pre-filled with this event's values.Event.Builder.[turnComplete](../Event.Builder.html#turnComplete(java.lang.Boolean))( [Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)value)Event.Builder.[turnComplete](../Event.Builder.html#turnComplete(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> value)


---

<!-- DOCUMENTO FUSIONADO: eventhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/class-use/Event.html -->

# Uses of Classcom.google.adk.events.Event

# Uses of Class

com.google.adk.events.Event

Package

Description

-
## Uses of

[Event](../Event.html)in[com.google.adk](../../package-summary.html)Modifier and TypeMethodDescription`static void`

Telemetry.[traceToolResponse](../../Telemetry.html#traceToolResponse(com.google.adk.agents.InvocationContext,java.lang.String,com.google.adk.events.Event))( [InvocationContext](../../agents/InvocationContext.html)invocationContext,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)eventId,[Event](../Event.html)functionResponseEvent)Traces tool response event. -
## Uses of

[Event](../Event.html)in[com.google.adk.agents](../../agents/package-summary.html)Modifier and TypeMethodDescriptionReadonlyContext.[events](../../agents/ReadonlyContext.html#events())()Returns an unmodifiable view of the events of the session.`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>BaseAgent.[runAsync](../../agents/BaseAgent.html#runAsync(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)parentContext)Runs the agent asynchronously.`protected abstract io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>BaseAgent.[runAsyncImpl](../../agents/BaseAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Agent-specific asynchronous logic.`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>LlmAgent.[runAsyncImpl](../../agents/LlmAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>LoopAgent.[runAsyncImpl](../../agents/LoopAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>ParallelAgent.[runAsyncImpl](../../agents/ParallelAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Runs sub-agents in parallel and emits their events.`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>SequentialAgent.[runAsyncImpl](../../agents/SequentialAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Runs sub-agents sequentially.`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>BaseAgent.[runLive](../../agents/BaseAgent.html#runLive(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)parentContext)Runs the agent synchronously.`protected abstract io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>BaseAgent.[runLiveImpl](../../agents/BaseAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Agent-specific synchronous logic.`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>LlmAgent.[runLiveImpl](../../agents/LlmAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>LoopAgent.[runLiveImpl](../../agents/LoopAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>ParallelAgent.[runLiveImpl](../../agents/ParallelAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Not supported for ParallelAgent.`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>SequentialAgent.[runLiveImpl](../../agents/SequentialAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Runs sub-agents sequentially in live mode. -
## Uses of

[Event](../Event.html)in[com.google.adk.events](../package-summary.html)Modifier and TypeMethodDescriptionEvent.Builder.[build](../Event.Builder.html#build())()`static`

[Event](../Event.html)Parses an event from a JSON string.Modifier and TypeMethodDescriptionEventStream.[iterator](../EventStream.html#iterator())()Returns an iterator that fetches events lazily.ModifierConstructorDescription[EventStream](../EventStream.html#%3Cinit%3E(java.util.function.Supplier))( [Supplier](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/function/Supplier.html)<[Event](../Event.html)> eventSupplier)Constructs a new event stream. -
## Uses of

[Event](../Event.html)in[com.google.adk.flows](../../flows/package-summary.html)Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>BaseFlow.[run](../../flows/BaseFlow.html#run(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Run this flow.`default io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>BaseFlow.[runLive](../../flows/BaseFlow.html#runLive(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext) -
## Uses of

[Event](../Event.html)in[com.google.adk.flows.llmflows](../../flows/llmflows/package-summary.html)Modifier and TypeMethodDescriptionRequestProcessor.RequestProcessingResult.[events](../../flows/llmflows/RequestProcessor.RequestProcessingResult.html#events())()ResponseProcessor.ResponseProcessingResult.[events](../../flows/llmflows/ResponseProcessor.ResponseProcessingResult.html#events())()`static io.reactivex.rxjava3.core.Maybe`

< [Event](../Event.html)>Functions.[handleFunctionCalls](../../flows/llmflows/Functions.html#handleFunctionCalls(com.google.adk.agents.InvocationContext,com.google.adk.events.Event,java.util.Map))( [InvocationContext](../../agents/InvocationContext.html)invocationContext,[Event](../Event.html)functionCallEvent,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[BaseTool](../../tools/BaseTool.html)> tools)`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>BaseLlmFlow.[run](../../flows/llmflows/BaseLlmFlow.html#run(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Executes the full LLM flow by repeatedly calling`BaseLlmFlow.runOneStep(com.google.adk.agents.InvocationContext)`

until a final response is produced.`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>BaseLlmFlow.[runLive](../../flows/llmflows/BaseLlmFlow.html#runLive(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Executes the LLM flow in streaming mode.Modifier and TypeMethodDescription`static io.reactivex.rxjava3.core.Maybe`

< [Event](../Event.html)>Functions.[handleFunctionCalls](../../flows/llmflows/Functions.html#handleFunctionCalls(com.google.adk.agents.InvocationContext,com.google.adk.events.Event,java.util.Map))( [InvocationContext](../../agents/InvocationContext.html)invocationContext,[Event](../Event.html)functionCallEvent,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[BaseTool](../../tools/BaseTool.html)> tools)`static void`

Functions.[populateClientFunctionCallId](../../flows/llmflows/Functions.html#populateClientFunctionCallId(com.google.adk.events.Event))( [Event](../Event.html)modelResponseEvent)Populates missing function call IDs in the provided event's content.`protected io.reactivex.rxjava3.core.Single`

< [ResponseProcessor.ResponseProcessingResult](../../flows/llmflows/ResponseProcessor.ResponseProcessingResult.html)>BaseLlmFlow.[postprocess](../../flows/llmflows/BaseLlmFlow.html#postprocess(com.google.adk.agents.InvocationContext,com.google.adk.events.Event,com.google.adk.models.LlmRequest,com.google.adk.models.LlmResponse))( [InvocationContext](../../agents/InvocationContext.html)context,[Event](../Event.html)baseEventForLlmResponse,[LlmRequest](../../models/LlmRequest.html)llmRequest,[LlmResponse](../../models/LlmResponse.html)llmResponse)Post-processes the LLM response after receiving it from the LLM.Modifier and TypeMethodDescriptionRequestProcessor.RequestProcessingResult.[create](../../flows/llmflows/RequestProcessor.RequestProcessingResult.html#create(com.google.adk.models.LlmRequest,java.lang.Iterable))( [LlmRequest](../../models/LlmRequest.html)updatedRequest,[Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<[Event](../Event.html)> events)ResponseProcessor.ResponseProcessingResult.[create](../../flows/llmflows/ResponseProcessor.ResponseProcessingResult.html#create(com.google.adk.models.LlmResponse,java.lang.Iterable,java.util.Optional))( [LlmResponse](../../models/LlmResponse.html)updatedResponse,[Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<[Event](../Event.html)> events,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> transferToAgent) -
## Uses of

[Event](../Event.html)in[com.google.adk.runner](../../runner/package-summary.html)Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>Runs the agent in the standard mode using a provided Session object.`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>Asynchronously runs the agent for a given user and session, processing a new message and using a default.`RunConfig`

`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>Runner.[runAsync](../../runner/Runner.html#runAsync(java.lang.String,java.lang.String,com.google.genai.types.Content,com.google.adk.agents.RunConfig))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, com.google.genai.types.Content newMessage,[RunConfig](../../agents/RunConfig.html)runConfig)Runs the agent in the standard mode.`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>Runner.[runLive](../../runner/Runner.html#runLive(com.google.adk.sessions.Session,com.google.adk.agents.LiveRequestQueue,com.google.adk.agents.RunConfig))( [Session](../../sessions/Session.html)session,[LiveRequestQueue](../../agents/LiveRequestQueue.html)liveRequestQueue,[RunConfig](../../agents/RunConfig.html)runConfig)Runs the agent in live mode, appending generated events to the session.`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>Runner.[runLive](../../runner/Runner.html#runLive(java.lang.String,java.lang.String,com.google.adk.agents.LiveRequestQueue,com.google.adk.agents.RunConfig))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[LiveRequestQueue](../../agents/LiveRequestQueue.html)liveRequestQueue,[RunConfig](../../agents/RunConfig.html)runConfig)Retrieves the session and runs the agent in live mode.`io.reactivex.rxjava3.core.Flowable`

< [Event](../Event.html)>Runner.[runWithSessionId](../../runner/Runner.html#runWithSessionId(java.lang.String,com.google.genai.types.Content,com.google.adk.agents.RunConfig))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, com.google.genai.types.Content newMessage,[RunConfig](../../agents/RunConfig.html)runConfig)Runs the agent asynchronously with a default user ID. -
## Uses of

[Event](../Event.html)in[com.google.adk.sessions](../../sessions/package-summary.html)Modifier and TypeMethodDescription`default io.reactivex.rxjava3.core.Single`

< [Event](../Event.html)>BaseSessionService.[appendEvent](../../sessions/BaseSessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))( [Session](../../sessions/Session.html)session,[Event](../Event.html)event)Appends an event to an in-memory session object and updates the session's state based on the event's state delta, if applicable.`io.reactivex.rxjava3.core.Single`

< [Event](../Event.html)>InMemorySessionService.[appendEvent](../../sessions/InMemorySessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))( [Session](../../sessions/Session.html)session,[Event](../Event.html)event)`io.reactivex.rxjava3.core.Single`

< [Event](../Event.html)>VertexAiSessionService.[appendEvent](../../sessions/VertexAiSessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))( [Session](../../sessions/Session.html)session,[Event](../Event.html)event)`abstract com.google.common.collect.ImmutableList`

< [Event](../Event.html)>ListEventsResponse.[events](../../sessions/ListEventsResponse.html#events())()Session.[events](../../sessions/Session.html#events())()Modifier and TypeMethodDescription`default io.reactivex.rxjava3.core.Single`

< [Event](../Event.html)>BaseSessionService.[appendEvent](../../sessions/BaseSessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))( [Session](../../sessions/Session.html)session,[Event](../Event.html)event)Appends an event to an in-memory session object and updates the session's state based on the event's state delta, if applicable.`io.reactivex.rxjava3.core.Single`

< [Event](../Event.html)>InMemorySessionService.[appendEvent](../../sessions/InMemorySessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))( [Session](../../sessions/Session.html)session,[Event](../Event.html)event)`io.reactivex.rxjava3.core.Single`

< [Event](../Event.html)>VertexAiSessionService.[appendEvent](../../sessions/VertexAiSessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))( [Session](../../sessions/Session.html)session,[Event](../Event.html)event) -
## Uses of

[Event](../Event.html)in[com.google.adk.web](../../web/package-summary.html)Modifier and TypeMethodDescriptionAdkWebServer.AgentController.[agentRun](../../web/AdkWebServer.AgentController.html#agentRun(com.google.adk.web.AdkWebServer.AgentRunRequest))( [AdkWebServer.AgentRunRequest](../../web/AdkWebServer.AgentRunRequest.html)request)Executes a non-streaming agent run for a given session and message.
