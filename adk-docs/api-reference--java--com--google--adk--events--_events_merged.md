---
merged_at: 2026-01-25T03:28:16.243617
merged_files: 8
---

# Documentos Fusionados

Este archivo contiene 8 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/package-summary.html -->

# Package com.google.adk.events

package com.google.adk.events

-
ClassDescriptionRepresents an event in a session.Builder for
.`Event`

Represents the actions attached to an event.Builder for.`EventActions`

Iterable stream ofobjects.`Event`


`Event`

`EventActions`

`Event`


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/package-use.html -->

# Uses of Packagecom.google.adk.events

# Uses of Package

com.google.adk.events

Package

Description

-
-
ClassDescriptionRepresents an event in a session.Represents the actions attached to an event.
-
ClassDescriptionRepresents an event in a session.Builder for
.`Event`

Represents the actions attached to an event.Builder for.`EventActions`

-
-
-
-
-
-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/package-tree.html -->

# Hierarchy For Package com.google.adk.events

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.events.
[Event.Builder](Event.Builder.html) - com.google.adk.events.
[EventActions](EventActions.html) - com.google.adk.events.
[EventActions.Builder](EventActions.Builder.html) - com.google.adk.events.
[EventStream](EventStream.html)(implements java.lang.[Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<T>) - com.google.adk.
[JsonBaseModel](../JsonBaseModel.html)- com.google.adk.events.
[Event](Event.html)

- com.google.adk.events.

- com.google.adk.events.


---

<!-- DOCUMENTO FUSIONADO: eventstreamhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/EventStream.html -->

# Class EventStream

-
## Constructor Summary

Constructors

Constructs a new event stream.

-
## Method Summary

Returns an iterator that fetches events lazily.

### Methods inherited from class java.lang.[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[clone](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#clone()), [equals](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#equals(java.lang.Object)), [finalize](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#finalize()), [getClass](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#getClass()), [hashCode](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#hashCode()), [notify](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notify()), [notifyAll](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notifyAll()), [toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#toString()), [wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait()), [wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long)), [wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long,int))


---

<!-- DOCUMENTO FUSIONADO: eventactionsbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/EventActions.Builder.html -->

# Class EventActions.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.events.EventActions.Builder

- Enclosing class:
[EventActions](EventActions.html)

Builder for

[.](EventActions.html)`EventActions`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[artifactDelta](#artifactDelta(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html), com.google.genai.types.Part> value)[build](#build())()[endInvocation](#endInvocation(boolean))(boolean endInvocation) [escalate](#escalate(boolean))(boolean escalate) [merge](#merge(com.google.adk.events.EventActions))( [EventActions](EventActions.html)other)[skipSummarization](#skipSummarization(boolean))(boolean skipSummarization) [stateDelta](#stateDelta(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> value)[transferToAgent](#transferToAgent(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)agentId)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### skipSummarization

-
### stateDelta

-
### artifactDelta

@CanIgnoreReturnValue public[EventActions.Builder](EventActions.Builder.html)artifactDelta( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html), com.google.genai.types.Part> value) -
### transferToAgent

-
### escalate

-
### requestedAuthConfigs

@CanIgnoreReturnValue public[EventActions.Builder](EventActions.Builder.html)requestedAuthConfigs( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>> value) -
### endInvocation

-
### merge

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: eventbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/Event.Builder.html -->

# Class Event.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.events.Event.Builder

- Enclosing class:
[Event](Event.html)

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[actions](#actions(com.google.adk.events.EventActions))( [EventActions](EventActions.html)value)[build](#build())()[content](#content(com.google.genai.types.Content))(com.google.genai.types.Content value) [errorCode](#errorCode(com.google.genai.types.FinishReason))(com.google.genai.types.FinishReason value) [errorMessage](#errorMessage(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)value)[errorMessage](#errorMessage(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> value)[groundingMetadata](#groundingMetadata(com.google.genai.types.GroundingMetadata))(com.google.genai.types.GroundingMetadata value) [groundingMetadata](#groundingMetadata(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GroundingMetadata> value)[interrupted](#interrupted(java.lang.Boolean))( [Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)value)[interrupted](#interrupted(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> value)[invocationId](#invocationId(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)value)[longRunningToolIds](#longRunningToolIds(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Set](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Set.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>> value)[longRunningToolIds](#longRunningToolIds(java.util.Set))( [Set](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Set.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> value)[timestamp](#timestamp(long))(long value) [turnComplete](#turnComplete(java.lang.Boolean))( [Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)value)[turnComplete](#turnComplete(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> value)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### id

-
### invocationId

-
### author

-
### content

-
### content

-
### actions

-
### longRunningToolIds

-
### longRunningToolIds

-
### partial

-
### partial

-
### turnComplete

-
### turnComplete

-
### errorCode

@CanIgnoreReturnValue public[Event.Builder](Event.Builder.html)errorCode(@Nullable com.google.genai.types.FinishReason value) -
### errorCode

@CanIgnoreReturnValue public[Event.Builder](Event.Builder.html)errorCode( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FinishReason> value) -
### errorMessage

-
### errorMessage

-
### interrupted

-
### interrupted

-
### timestamp

-
### timestamp

-
### branch

-
### branch

-
### groundingMetadata

@CanIgnoreReturnValue public[Event.Builder](Event.Builder.html)groundingMetadata(@Nullable com.google.genai.types.GroundingMetadata value) -
### groundingMetadata

@CanIgnoreReturnValue public[Event.Builder](Event.Builder.html)groundingMetadata( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GroundingMetadata> value) -
### build


-


---

<!-- DOCUMENTO FUSIONADO: eventactionshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/EventActions.html -->

# Class EventActions

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.events.EventActions

Represents the actions attached to an event.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)< [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html), com.google.genai.types.Part>`static`

[EventActions.Builder](EventActions.Builder.html)[builder](#builder())()`boolean`

[escalate](#escalate())()`int`

[hashCode](#hashCode())()`void`

[setArtifactDelta](#setArtifactDelta(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html), com.google.genai.types.Part> artifactDelta)`void`

[setEndInvocation](#setEndInvocation(boolean))(boolean endInvocation) `void`

[setEndInvocation](#setEndInvocation(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> endInvocation)`void`

[setEscalate](#setEscalate(boolean))(boolean escalate) `void`

[setEscalate](#setEscalate(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> escalate)`void`

[setRequestedAuthConfigs](#setRequestedAuthConfigs(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>> requestedAuthConfigs)`void`

[setSkipSummarization](#setSkipSummarization(boolean))(boolean skipSummarization) `void`

[setSkipSummarization](#setSkipSummarization(java.lang.Boolean))( [Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)skipSummarization)`void`

[setSkipSummarization](#setSkipSummarization(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> skipSummarization)`void`

[setStateDelta](#setStateDelta(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> stateDelta)`void`

[setTransferToAgent](#setTransferToAgent(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)transferToAgent)`void`

[setTransferToAgent](#setTransferToAgent(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> transferToAgent)

-
## Constructor Details

-
### EventActions

public EventActions()Default constructor for Jackson.

-
-
## Method Details

-
### skipSummarization

-
### setSkipSummarization

-
### setSkipSummarization

-
### setSkipSummarization

public void setSkipSummarization(boolean skipSummarization) -
### stateDelta

-
### setStateDelta

-
### artifactDelta

-
### setArtifactDelta

-
### transferToAgent

-
### setTransferToAgent

-
### setTransferToAgent

-
### escalate

-
### setEscalate

-
### setEscalate

public void setEscalate(boolean escalate) -
### requestedAuthConfigs

-
### setRequestedAuthConfigs

public void setRequestedAuthConfigs( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>> requestedAuthConfigs) -
### endInvocation

-
### setEndInvocation

-
### setEndInvocation

public void setEndInvocation(boolean endInvocation) -
### builder

-
### toBuilder

-
### equals

-
### hashCode


-


---

<!-- DOCUMENTO FUSIONADO: eventhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/events/Event.html -->

# Class Event

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.JsonBaseModel](../JsonBaseModel.html)

com.google.adk.events.Event

Represents an event in a session.

-
## Nested Class Summary

-
## Method Summary

Modifier and TypeMethodDescription[actions](#actions())()[author](#author())()The author of the event, it could be the name of the agent or "user" literal.[branch](#branch())()The branch of the event.`void`

Sets the branch for this event.`void`

`static`

[Event.Builder](Event.Builder.html)[builder](#builder())()[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Content> [content](#content())()`boolean`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FinishReason> `final boolean`

Returns true if this is a final response.`static`

[Event](Event.html)Parses an event from a JSON string.`final com.google.common.collect.ImmutableList`

<com.google.genai.types.FunctionCall> Returns all function calls from this event.`final com.google.common.collect.ImmutableList`

<com.google.genai.types.FunctionResponse> Returns all function responses from this event.`static`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GroundingMetadata> The grounding metadata of the event.`int`

[hashCode](#hashCode())()[id](#id())()The event id.Id of the invocation that this event belongs to.Set of ids of the long running function calls.[partial](#partial())()partial is true for incomplete chunks from the LLM streaming response.`void`

[setActions](#setActions(com.google.adk.events.EventActions))( [EventActions](EventActions.html)actions)`void`

`void`

[setContent](#setContent(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Content> content)`void`

[setErrorCode](#setErrorCode(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.FinishReason> errorCode)`void`

[setErrorMessage](#setErrorMessage(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> errorMessage)`void`

[setGroundingMetadata](#setGroundingMetadata(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GroundingMetadata> groundingMetadata)`void`

`void`

[setInterrupted](#setInterrupted(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> interrupted)`void`

[setInvocationId](#setInvocationId(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)invocationId)`void`

[setLongRunningToolIds](#setLongRunningToolIds(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Set](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Set.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>> longRunningToolIds)`void`

[setPartial](#setPartial(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> partial)`void`

[setTimestamp](#setTimestamp(long))(long timestamp) `void`

[setTurnComplete](#setTurnComplete(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)> turnComplete)`final`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)Converts the event content into a readable string.`long`

The timestamp of the event.Creates a builder pre-filled with this event's values.[toString](#toString())()### Methods inherited from class com.google.adk.

[JsonBaseModel](../JsonBaseModel.html)[fromJsonNode](../JsonBaseModel.html#fromJsonNode(com.fasterxml.jackson.databind.JsonNode,java.lang.Class)),[fromJsonString](../JsonBaseModel.html#fromJsonString(java.lang.String,java.lang.Class)),[getMapper](../JsonBaseModel.html#getMapper()),[toJson](../JsonBaseModel.html#toJson()),[toJsonNode](../JsonBaseModel.html#toJsonNode(java.lang.Object)),[toJsonString](../JsonBaseModel.html#toJsonString(java.lang.Object))

-
## Method Details

-
### generateEventId

-
### id

The event id. -
### setId

-
### invocationId

Id of the invocation that this event belongs to. -
### setInvocationId

-
### author

The author of the event, it could be the name of the agent or "user" literal. -
### setAuthor

-
### content

-
### setContent

-
### actions

-
### setActions

-
### longRunningToolIds

-
### setLongRunningToolIds

-
### partial

-
### setPartial

-
### turnComplete

-
### setTurnComplete

-
### errorCode

-
### setErrorCode

-
### errorMessage

-
### setErrorMessage

-
### interrupted

-
### setInterrupted

-
### branch

-
### branch

Sets the branch for this event.Format: agentA.agentB.agentC — shows hierarchy of nested agents.

- Parameters:
`branch`

- Branch identifier.

-
### branch

-
### groundingMetadata

The grounding metadata of the event. -
### setGroundingMetadata

public void setGroundingMetadata( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GroundingMetadata> groundingMetadata) -
### timestamp

public long timestamp()The timestamp of the event. -
### setTimestamp

public void setTimestamp(long timestamp) -
### functionCalls

public final com.google.common.collect.ImmutableList<com.google.genai.types.FunctionCall> functionCalls()Returns all function calls from this event. -
### functionResponses

public final com.google.common.collect.ImmutableList<com.google.genai.types.FunctionResponse> functionResponses()Returns all function responses from this event. -
### finalResponse

public final boolean finalResponse()Returns true if this is a final response. -
### stringifyContent

Converts the event content into a readable string.Includes text, function calls, and responses.

- Returns:
- Stringified content.

-
### builder

-
### fromJson

-
### toBuilder

Creates a builder pre-filled with this event's values. -
### equals

-
### toString

-
### hashCode


-
