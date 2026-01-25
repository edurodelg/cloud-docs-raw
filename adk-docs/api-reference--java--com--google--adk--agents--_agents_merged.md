---
merged_at: 2026-01-25T02:21:31.608625
merged_files: 41
---

# Documentos Fusionados

Este archivo contiene 41 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: callbacksaftertoolcallbacksynchtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.AfterToolCallbackSync.html -->

# Interface Callbacks.AfterToolCallbackSync

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

Helper interface to allow for sync afterToolCallback. The function is wrapped into an async one
before being processed further.

-
## Method Summary


-
## Method Details

-
### call


-


---

<!-- DOCUMENTO FUSIONADO: callbacksaftermodelcallbacksynchtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.AfterModelCallbackSync.html -->

# Interface Callbacks.AfterModelCallbackSync

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

Helper interface to allow for sync afterModelCallback. The function is wrapped into an async
one before being processed further.

-
## Method Summary


-
## Method Details

-
### call


-


---

<!-- DOCUMENTO FUSIONADO: callbacksbeforemodelcallbacksynchtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.BeforeModelCallbackSync.html -->

# Interface Callbacks.BeforeModelCallbackSync

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

Helper interface to allow for sync beforeModelCallback. The function is wrapped into an async
one before being processed further.

-
## Method Summary


-
## Method Details

-
### call


-


---

<!-- DOCUMENTO FUSIONADO: baseagentconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/BaseAgentConfig.html -->

# Class BaseAgentConfig

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.BaseAgentConfig

- Direct Known Subclasses:
[LlmAgentConfig](LlmAgentConfig.html)

Base configuration for all agents.

workInProgress: Config agent features are not yet ready for public use.

-
## Constructor Summary

-
## Method Summary


-
## Constructor Details

-
### BaseAgentConfig

public BaseAgentConfig()

-
-
## Method Details

-
### name

-
### setName

-
### description

-
### setDescription


-


---

<!-- DOCUMENTO FUSIONADO: callbacksafteragentcallbacksynchtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.AfterAgentCallbackSync.html -->

# Interface Callbacks.AfterAgentCallbackSync

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

Helper interface to allow for sync afterAgentCallback. The function is wrapped into an async
one before being processed further.

-
## Method Summary

Modifier and TypeMethodDescription[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Content> [call](#call(com.google.adk.agents.CallbackContext))( [CallbackContext](CallbackContext.html)callbackContext)

-
## Method Details

-
### call


-


---

<!-- DOCUMENTO FUSIONADO: callbacksbeforeagentcallbacksynchtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.BeforeAgentCallbackSync.html -->

# Interface Callbacks.BeforeAgentCallbackSync

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

Helper interface to allow for sync beforeAgentCallback. The function is wrapped into an async
one before being processed further.

-
## Method Summary

Modifier and TypeMethodDescription[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Content> [call](#call(com.google.adk.agents.CallbackContext))( [CallbackContext](CallbackContext.html)callbackContext)

-
## Method Details

-
### call


-


---

<!-- DOCUMENTO FUSIONADO: callbacksbeforeagentcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.BeforeAgentCallback.html -->

# Interface Callbacks.BeforeAgentCallback

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Maybe`

<com.google.genai.types.Content> [call](#call(com.google.adk.agents.CallbackContext))( [CallbackContext](CallbackContext.html)callbackContext)Async callback before agent runs.

-
## Method Details

-
### call

io.reactivex.rxjava3.core.Maybe<com.google.genai.types.Content> call( [CallbackContext](CallbackContext.html)callbackContext)Async callback before agent runs.- Parameters:
`callbackContext`

- Callback context.- Returns:
- content override, or empty to continue.


-


---

<!-- DOCUMENTO FUSIONADO: callbacksafteragentcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.AfterAgentCallback.html -->

# Interface Callbacks.AfterAgentCallback

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Maybe`

<com.google.genai.types.Content> [call](#call(com.google.adk.agents.CallbackContext))( [CallbackContext](CallbackContext.html)callbackContext)Async callback after agent runs.

-
## Method Details

-
### call

io.reactivex.rxjava3.core.Maybe<com.google.genai.types.Content> call( [CallbackContext](CallbackContext.html)callbackContext)Async callback after agent runs.- Parameters:
`callbackContext`

- Callback context.- Returns:
- modified content, or empty to keep original.


-


---

<!-- DOCUMENTO FUSIONADO: callbackshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.html -->

# Class Callbacks

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.Callbacks

Functional interfaces for agent lifecycle callbacks.

-
## Nested Class Summary

Modifier and TypeClassDescription`static interface`

`static interface`

Helper interface to allow for sync afterAgentCallback.`static interface`

`static interface`

Helper interface to allow for sync afterModelCallback.`static interface`

`static interface`

Helper interface to allow for sync afterToolCallback.`static interface`

`static interface`

Helper interface to allow for sync beforeAgentCallback.`static interface`

`static interface`

Helper interface to allow for sync beforeModelCallback.`static interface`

`static interface`

Helper interface to allow for sync beforeToolCallback. -
## Method Summary


---

<!-- DOCUMENTO FUSIONADO: liverequestqueuehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/LiveRequestQueue.html -->

# Class LiveRequestQueue

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.LiveRequestQueue

A queue of live requests to be sent to the model.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`void`

[close](#close())()`void`

[content](#content(com.google.genai.types.Content))(com.google.genai.types.Content content) `io.reactivex.rxjava3.core.Flowable`

< [LiveRequest](LiveRequest.html)>[get](#get())()`void`

[realtime](#realtime(com.google.genai.types.Blob))(com.google.genai.types.Blob blob) `void`

[send](#send(com.google.adk.agents.LiveRequest))( [LiveRequest](LiveRequest.html)request)

-
## Constructor Details

-
### LiveRequestQueue

public LiveRequestQueue()

-
-
## Method Details

-
### close

public void close() -
### content

public void content(com.google.genai.types.Content content) -
### realtime

public void realtime(com.google.genai.types.Blob blob) -
### send

-
### get


-


---

<!-- DOCUMENTO FUSIONADO: callbacksbeforemodelcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.BeforeModelCallback.html -->

# Interface Callbacks.BeforeModelCallback

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Maybe`

< [LlmResponse](../models/LlmResponse.html)>[call](#call(com.google.adk.agents.CallbackContext,com.google.adk.models.LlmRequest))( [CallbackContext](CallbackContext.html)callbackContext,[LlmRequest](../models/LlmRequest.html)llmRequest)Async callback before LLM invocation.

-
## Method Details

-
### call

io.reactivex.rxjava3.core.Maybe<[LlmResponse](../models/LlmResponse.html)> call( [CallbackContext](CallbackContext.html)callbackContext,[LlmRequest](../models/LlmRequest.html)llmRequest)Async callback before LLM invocation.- Parameters:
`callbackContext`

- Callback context.`llmRequest`

- LLM request.- Returns:
- response override, or empty to continue.


-


---

<!-- DOCUMENTO FUSIONADO: callbacksaftermodelcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.AfterModelCallback.html -->

# Interface Callbacks.AfterModelCallback

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Maybe`

< [LlmResponse](../models/LlmResponse.html)>[call](#call(com.google.adk.agents.CallbackContext,com.google.adk.models.LlmResponse))( [CallbackContext](CallbackContext.html)callbackContext,[LlmResponse](../models/LlmResponse.html)llmResponse)Async callback after LLM response.

-
## Method Details

-
### call

io.reactivex.rxjava3.core.Maybe<[LlmResponse](../models/LlmResponse.html)> call( [CallbackContext](CallbackContext.html)callbackContext,[LlmResponse](../models/LlmResponse.html)llmResponse)Async callback after LLM response.- Parameters:
`callbackContext`

- Callback context.`llmResponse`

- LLM response.- Returns:
- modified response, or empty to keep original.


-


---

<!-- DOCUMENTO FUSIONADO: liverequestbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/LiveRequest.Builder.html -->

# Class LiveRequest.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.LiveRequest.Builder

- Enclosing class:
[LiveRequest](LiveRequest.html)

Builder for constructing

[instances.](LiveRequest.html)`LiveRequest`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[LiveRequest.Builder](LiveRequest.Builder.html)[blob](#blob(com.google.genai.types.Blob))(com.google.genai.types.Blob blob) `abstract`

[LiveRequest.Builder](LiveRequest.Builder.html)`final`

[LiveRequest](LiveRequest.html)[build](#build())()`abstract`

[LiveRequest.Builder](LiveRequest.Builder.html)`abstract`

[LiveRequest.Builder](LiveRequest.Builder.html)`abstract`

[LiveRequest.Builder](LiveRequest.Builder.html)[content](#content(com.google.genai.types.Content))(com.google.genai.types.Content content) `abstract`

[LiveRequest.Builder](LiveRequest.Builder.html)

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
### content

-
### blob

-
### blob

-
### close

-
### close

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: callbacksbeforetoolcallbacksynchtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.BeforeToolCallbackSync.html -->

# Interface Callbacks.BeforeToolCallbackSync

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

Helper interface to allow for sync beforeToolCallback. The function is wrapped into an async
one before being processed further.

-
## Method Summary


-
## Method Details

-
### call

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>> call( [InvocationContext](InvocationContext.html)invocationContext,[BaseTool](../tools/BaseTool.html)baseTool,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> input,[ToolContext](../tools/ToolContext.html)toolContext)

-


---

<!-- DOCUMENTO FUSIONADO: readonlycontexthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/ReadonlyContext.html -->

# Class ReadonlyContext

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.ReadonlyContext

- Direct Known Subclasses:
[CallbackContext](CallbackContext.html)

Provides read-only access to the context of an agent run.

-
## Field Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescriptionReturns the name of the agent currently running.[branch](#branch())()Returns the branch of the current invocation, if present.[events](#events())()Returns an unmodifiable view of the events of the session.Returns the ID of the current invocation.Returns the session ID.[state](#state())()Returns an unmodifiable view of the state of the session.[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Content> Returns the user content that initiated this invocation.

-
## Field Details

-
### invocationContext


-
-
## Constructor Details

-
### ReadonlyContext


-
-
## Method Details

-
### userContent

Returns the user content that initiated this invocation. -
### invocationId

Returns the ID of the current invocation. -
### branch

-
### agentName

Returns the name of the agent currently running. -
### sessionId

Returns the session ID. -
### events

-
### state


-


---

<!-- DOCUMENTO FUSIONADO: instructionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Instruction.html -->

# Interface Instruction

- All Known Implementing Classes:

,[Instruction.Provider](Instruction.Provider.html)[Instruction.Static](Instruction.Static.html)

In the instructions, you should describe concisely what the agent will do, when it should defer to other agents/tools, and how it should respond to the user.

Templating is supported using placeholders like `{variable_name}`

or ```
{artifact.artifact_name}
```

. These are replaced with values from the agent's session state or
loaded artifacts, respectively. For example, an instruction like ```
"Translate the following
text to {language}: {user_query}"
```

would substitute `{language}`

and `{user_query}`

with their corresponding values from the session state.

Instructions can also be dynamically constructed using [ Instruction.Provider](Instruction.Provider.html). This
allows for more complex logic where the instruction text is generated based on the current

[. Additionally, an instruction could be built to include specific information based on based on some external factors fetched during the Provider call like the current time, the result of some API call, etc.](ReadonlyContext.html)

`ReadonlyContext`

-
## Nested Class Summary

Modifier and TypeInterfaceDescription`static final record`

Returns an instruction dynamically constructed from the given context.`static final record`

Plain instruction directly provided to the agent.


---

<!-- DOCUMENTO FUSIONADO: callbacksaftertoolcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.AfterToolCallback.html -->

# Interface Callbacks.AfterToolCallback

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

-
## Method Summary


-
## Method Details

-
### call

io.reactivex.rxjava3.core.Maybe<[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>> call( [InvocationContext](InvocationContext.html)invocationContext,[BaseTool](../tools/BaseTool.html)baseTool,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> input,[ToolContext](../tools/ToolContext.html)toolContext,[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)response)Async callback after tool runs.- Parameters:
`invocationContext`

- Invocation context.`baseTool`

- Tool instance.`input`

- Tool input arguments.`toolContext`

- Tool context.`response`

- Raw tool response.- Returns:
- processed result, or empty to keep original.


-


---

<!-- DOCUMENTO FUSIONADO: runconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/RunConfig.html -->

# Class RunConfig

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.RunConfig

Configuration to modify an agent's LLM's underlying behavior.

-
## Nested Class Summary

Modifier and TypeClassDescription`static class`

Builder for.`RunConfig`

`static enum`

Streaming mode for the runner. -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[RunConfig.Builder](RunConfig.Builder.html)[builder](#builder())()`static`

[RunConfig.Builder](RunConfig.Builder.html)`abstract int`

`abstract @Nullable com.google.genai.types.AudioTranscriptionConfig`

`abstract com.google.common.collect.ImmutableList`

<com.google.genai.types.Modality> `abstract boolean`

`abstract @Nullable com.google.genai.types.SpeechConfig`

`abstract`

[RunConfig.StreamingMode](RunConfig.StreamingMode.html)

-
## Constructor Details

-
### RunConfig

public RunConfig()

-
-
## Method Details

-
### speechConfig

public abstract @Nullable com.google.genai.types.SpeechConfig speechConfig() -
### responseModalities

public abstract com.google.common.collect.ImmutableList<com.google.genai.types.Modality> responseModalities() -
### saveInputBlobsAsArtifacts

public abstract boolean saveInputBlobsAsArtifacts() -
### streamingMode

-
### outputAudioTranscription

public abstract @Nullable com.google.genai.types.AudioTranscriptionConfig outputAudioTranscription() -
### maxLlmCalls

public abstract int maxLlmCalls() -
### builder

-
### builder


-


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/package-summary.html -->

# Package com.google.adk.agents

package com.google.adk.agents

-
ClassDescriptionBase class for all agents.Base configuration for all agents.The context of various callbacks for an agent invocation.Functional interfaces for agent lifecycle callbacks.Helper interface to allow for sync afterAgentCallback.Helper interface to allow for sync afterModelCallback.Helper interface to allow for sync afterToolCallback.Helper interface to allow for sync beforeAgentCallback.Helper interface to allow for sync beforeModelCallback.Helper interface to allow for sync beforeToolCallback.Utility methods for normalizing agent callbacks.Represents an instruction that can be provided to an agent to guide its behavior.Returns an instruction dynamically constructed from the given context.Plain instruction directly provided to the agent.The context for an agent invocation.Represents a request to be sent to a live connection to the LLM model.Builder for constructing
instances.`LiveRequest`

A queue of live requests to be sent to the model.The LLM-based agent.Builder for.`LlmAgent`

Enum to define if contents of previous events should be included in requests to the underlying LLM.Configuration for LlmAgent.An agent that runs its sub-agents sequentially in a loop.Builder for.`LoopAgent`

A shell agent that runs its sub-agents in parallel in isolated manner.Builder for.`ParallelAgent`

Provides read-only access to the context of an agent run.Configuration to modify an agent's LLM's underlying behavior.Builder for.`RunConfig`

Streaming mode for the runner.An agent that runs its sub-agents sequentially.Builder for.`SequentialAgent`


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/package-use.html -->

# Uses of Packagecom.google.adk.agents

# Uses of Package

com.google.adk.agents

Package

Description

-
-
ClassDescriptionBase class for all agents.Base configuration for all agents.The context of various callbacks for an agent invocation.Helper interface to allow for sync afterAgentCallback.Helper interface to allow for sync afterModelCallback.Helper interface to allow for sync afterToolCallback.Helper interface to allow for sync beforeAgentCallback.Helper interface to allow for sync beforeModelCallback.Helper interface to allow for sync beforeToolCallback.Represents an instruction that can be provided to an agent to guide its behavior.The context for an agent invocation.Represents a request to be sent to a live connection to the LLM model.Builder for constructing
instances.`LiveRequest`

A queue of live requests to be sent to the model.The LLM-based agent.Builder for.`LlmAgent`

Enum to define if contents of previous events should be included in requests to the underlying LLM.An agent that runs its sub-agents sequentially in a loop.Builder for.`LoopAgent`

A shell agent that runs its sub-agents in parallel in isolated manner.Builder for.`ParallelAgent`

Provides read-only access to the context of an agent run.Configuration to modify an agent's LLM's underlying behavior.Builder for.`RunConfig`

Streaming mode for the runner.An agent that runs its sub-agents sequentially.Builder for.`SequentialAgent`

-
-
-
ClassDescriptionBase class for all agents.A queue of live requests to be sent to the model.Configuration to modify an agent's LLM's underlying behavior.
-
ClassDescriptionBase class for all agents.The context of various callbacks for an agent invocation.The context for an agent invocation.Provides read-only access to the context of an agent run.
-
-
-
-


---

<!-- DOCUMENTO FUSIONADO: instructionstatichtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Instruction.Static.html -->

# Record Class Instruction.Static

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[java.lang.Record](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Record.html)

com.google.adk.agents.Instruction.Static

- All Implemented Interfaces:
[Instruction](Instruction.html)

- Enclosing interface:
[Instruction](Instruction.html)

Plain instruction directly provided to the agent.

-
## Nested Class Summary

### Nested classes/interfaces inherited from interface com.google.adk.agents.

[Instruction](Instruction.html)[Instruction.Provider](Instruction.Provider.html),[Instruction.Static](Instruction.Static.html) -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`final boolean`

Indicates whether some other object is "equal to" this one.`final int`

[hashCode](#hashCode())()Returns a hash code value for this object.Returns the value of the`instruction`

record component.`final`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[toString](#toString())()Returns a string representation of this record class.

-
## Constructor Details

-
### Static

Creates an instance of a`Static`

record class.- Parameters:
`instruction`

- the value for the`instruction`

record component


-
-
## Method Details

-
### toString

-
### hashCode

-
### equals

Indicates whether some other object is "equal to" this one. The objects are equal if the other object is of the same class and if all the record components are equal. All components in this record class are compared with.`Objects::equals(Object,Object)`

-
### instruction

Returns the value of the`instruction`

record component.- Returns:
- the value of the
`instruction`

record component


-


---

<!-- DOCUMENTO FUSIONADO: llmagentconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/LlmAgentConfig.html -->

# Class LlmAgentConfig

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.agents.BaseAgentConfig](BaseAgentConfig.html)

com.google.adk.agents.LlmAgentConfig

Configuration for LlmAgent.

workInProgress: Config agent features are not yet ready for public use.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[model](#model())()`void`

[setDisallowTransferToParent](#setDisallowTransferToParent(java.lang.Boolean))( [Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)disallowTransferToParent)`void`

[setDisallowTransferToPeers](#setDisallowTransferToPeers(java.lang.Boolean))( [Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)disallowTransferToPeers)`void`

[setInstruction](#setInstruction(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)instruction)`void`

`void`

[setOutputKey](#setOutputKey(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)outputKey)### Methods inherited from class com.google.adk.agents.

[BaseAgentConfig](BaseAgentConfig.html)[description](BaseAgentConfig.html#description()),[name](BaseAgentConfig.html#name()),[setDescription](BaseAgentConfig.html#setDescription(java.lang.String)),[setName](BaseAgentConfig.html#setName(java.lang.String))

-
## Constructor Details

-
### LlmAgentConfig

public LlmAgentConfig()

-
-
## Method Details

-
### model

-
### setModel

-
### instruction

-
### setInstruction

-
### disallowTransferToParent

-
### setDisallowTransferToParent

-
### disallowTransferToPeers

-
### setDisallowTransferToPeers

-
### outputKey

-
### setOutputKey


-


---

<!-- DOCUMENTO FUSIONADO: callbacksbeforetoolcallbackhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Callbacks.BeforeToolCallback.html -->

# Interface Callbacks.BeforeToolCallback

- Enclosing class:
[Callbacks](Callbacks.html)

- Functional Interface:
- This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.

-
## Method Summary

Modifier and TypeMethodDescription[call](#call(com.google.adk.agents.InvocationContext,com.google.adk.tools.BaseTool,java.util.Map,com.google.adk.tools.ToolContext))( [InvocationContext](InvocationContext.html)invocationContext,[BaseTool](../tools/BaseTool.html)baseTool,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> input,[ToolContext](../tools/ToolContext.html)toolContext)Async callback before tool runs.

-
## Method Details

-
### call

io.reactivex.rxjava3.core.Maybe<[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>> call( [InvocationContext](InvocationContext.html)invocationContext,[BaseTool](../tools/BaseTool.html)baseTool,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> input,[ToolContext](../tools/ToolContext.html)toolContext)Async callback before tool runs.- Parameters:
`invocationContext`

- Invocation context.`baseTool`

- Tool instance.`input`

- Tool input arguments.`toolContext`

- Tool context.- Returns:
- override result, or empty to continue.


-


---

<!-- DOCUMENTO FUSIONADO: callbackutilhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/CallbackUtil.html -->

# Class CallbackUtil

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.CallbackUtil

Utility methods for normalizing agent callbacks.

-
## Method Summary

Modifier and TypeMethodDescription`static @Nullable com.google.common.collect.ImmutableList`

< [Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)>[getAfterAgentCallbacks](#getAfterAgentCallbacks(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback)Normalizes after-agent callbacks.`static @Nullable com.google.common.collect.ImmutableList`

< [Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)>[getBeforeAgentCallbacks](#getBeforeAgentCallbacks(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback)Normalizes before-agent callbacks.

-
## Method Details

-
### getBeforeAgentCallbacks

@CanIgnoreReturnValue public static @Nullable com.google.common.collect.ImmutableList<[Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)> getBeforeAgentCallbacks( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback)Normalizes before-agent callbacks.- Parameters:
`beforeAgentCallback`

- Callback list (sync or async).- Returns:
- normalized async callbacks, or null if input is null.

-
### getAfterAgentCallbacks

@CanIgnoreReturnValue public static @Nullable com.google.common.collect.ImmutableList<[Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)> getAfterAgentCallbacks( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback)Normalizes after-agent callbacks.- Parameters:
`afterAgentCallback`

- Callback list (sync or async).- Returns:
- normalized async callbacks, or null if input is null.


-


---

<!-- DOCUMENTO FUSIONADO: liverequesthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/LiveRequest.html -->

# Class LiveRequest

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.JsonBaseModel](../JsonBaseModel.html)

com.google.adk.agents.LiveRequest

Represents a request to be sent to a live connection to the LLM model.

-
## Nested Class Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Blob> [blob](#blob())()Returns the blob of the request.`static`

[LiveRequest.Builder](LiveRequest.Builder.html)[builder](#builder())()[close](#close())()Returns whether the connection should be closed.`abstract`

[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Content> [content](#content())()Returns the content of the request.`static`

[LiveRequest](LiveRequest.html)[fromJsonString](#fromJsonString(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)json)Deserializes a Json string to aobject.`LiveRequest`

`boolean`

Extracts boolean value from the close field or returns false if unset.`abstract`

[LiveRequest.Builder](LiveRequest.Builder.html)### Methods inherited from class com.google.adk.

[JsonBaseModel](../JsonBaseModel.html)[fromJsonNode](../JsonBaseModel.html#fromJsonNode(com.fasterxml.jackson.databind.JsonNode,java.lang.Class)),[fromJsonString](../JsonBaseModel.html#fromJsonString(java.lang.String,java.lang.Class)),[getMapper](../JsonBaseModel.html#getMapper()),[toJson](../JsonBaseModel.html#toJson()),[toJsonNode](../JsonBaseModel.html#toJsonNode(java.lang.Object)),[toJsonString](../JsonBaseModel.html#toJsonString(java.lang.Object))

-
## Method Details

-
### content

Returns the content of the request.If set, send the content to the model in turn-by-turn mode.

- Returns:
- An optional
`Content`

object containing the content of the request.

-
### blob

Returns the blob of the request.If set, send the blob to the model in realtime mode.

- Returns:
- An optional
`Blob`

object containing the blob of the request.

-
### close

-
### shouldClose

public boolean shouldClose()Extracts boolean value from the close field or returns false if unset. -
### builder

-
### toBuilder

-
### fromJsonString

Deserializes a Json string to aobject.`LiveRequest`


-


---

<!-- DOCUMENTO FUSIONADO: parallelagentbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/ParallelAgent.Builder.html -->

# Class ParallelAgent.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.ParallelAgent.Builder

- Enclosing class:
[ParallelAgent](ParallelAgent.html)

Builder for

[.](ParallelAgent.html)`ParallelAgent`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[afterAgentCallback](#afterAgentCallback(com.google.adk.agents.Callbacks.AfterAgentCallback))( [Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)afterAgentCallback)[afterAgentCallback](#afterAgentCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback)[beforeAgentCallback](#beforeAgentCallback(com.google.adk.agents.Callbacks.BeforeAgentCallback))( [Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)beforeAgentCallback)[beforeAgentCallback](#beforeAgentCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback)[build](#build())()[description](#description(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### name

-
### description

-
### subAgents

-
### subAgents

-
### beforeAgentCallback

@CanIgnoreReturnValue public[ParallelAgent.Builder](ParallelAgent.Builder.html)beforeAgentCallback( [Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)beforeAgentCallback) -
### beforeAgentCallback

@CanIgnoreReturnValue public[ParallelAgent.Builder](ParallelAgent.Builder.html)beforeAgentCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback) -
### afterAgentCallback

@CanIgnoreReturnValue public[ParallelAgent.Builder](ParallelAgent.Builder.html)afterAgentCallback( [Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)afterAgentCallback) -
### afterAgentCallback

@CanIgnoreReturnValue public[ParallelAgent.Builder](ParallelAgent.Builder.html)afterAgentCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback) -
### build


-


---

<!-- DOCUMENTO FUSIONADO: runconfigstreamingmodehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/RunConfig.StreamingMode.html -->

# Enum Class RunConfig.StreamingMode

- All Implemented Interfaces:

,[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html)

,[Comparable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Comparable.html)<[RunConfig.StreamingMode](RunConfig.StreamingMode.html)>[Constable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/constant/Constable.html)

- Enclosing class:
[RunConfig](RunConfig.html)

Streaming mode for the runner. Required for BaseAgent.runLive() to work.

-
## Nested Class Summary

### Nested classes/interfaces inherited from class java.lang.

[Enum](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.html)[Enum.EnumDesc](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.EnumDesc.html)<[E](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.EnumDesc.html#type-param-E)extends[Enum](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.html)<[E](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.EnumDesc.html#type-param-E)>> -
## Enum Constant Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[RunConfig.StreamingMode](RunConfig.StreamingMode.html)Returns the enum constant of this class with the specified name.`static`

[RunConfig.StreamingMode](RunConfig.StreamingMode.html)[][values](#values())()Returns an array containing the constants of this enum class, in the order they are declared.

-
## Enum Constant Details

-
### NONE

-
### SSE

-
### BIDI


-
-
## Method Details

-
### values

Returns an array containing the constants of this enum class, in the order they are declared.- Returns:
- an array containing the constants of this enum class, in the order they are declared

-
### valueOf

Returns the enum constant of this class with the specified name. The string must match*exactly*an identifier used to declare an enum constant in this class. (Extraneous whitespace characters are not permitted.)- Parameters:
`name`

- the name of the enum constant to be returned.- Returns:
- the enum constant with the specified name
- Throws:

- if this enum class has no constant with the specified name[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)

- if the argument is null[NullPointerException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/NullPointerException.html)


-


---

<!-- DOCUMENTO FUSIONADO: sequentialagentbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/SequentialAgent.Builder.html -->

# Class SequentialAgent.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.SequentialAgent.Builder

- Enclosing class:
[SequentialAgent](SequentialAgent.html)

Builder for

[.](SequentialAgent.html)`SequentialAgent`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[afterAgentCallback](#afterAgentCallback(com.google.adk.agents.Callbacks.AfterAgentCallback))( [Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)afterAgentCallback)[afterAgentCallback](#afterAgentCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback)[beforeAgentCallback](#beforeAgentCallback(com.google.adk.agents.Callbacks.BeforeAgentCallback))( [Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)beforeAgentCallback)[beforeAgentCallback](#beforeAgentCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback)[build](#build())()[description](#description(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### name

-
### description

-
### subAgents

-
### subAgents

-
### beforeAgentCallback

@CanIgnoreReturnValue public[SequentialAgent.Builder](SequentialAgent.Builder.html)beforeAgentCallback( [Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)beforeAgentCallback) -
### beforeAgentCallback

@CanIgnoreReturnValue public[SequentialAgent.Builder](SequentialAgent.Builder.html)beforeAgentCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback) -
### afterAgentCallback

@CanIgnoreReturnValue public[SequentialAgent.Builder](SequentialAgent.Builder.html)afterAgentCallback( [Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)afterAgentCallback) -
### afterAgentCallback

@CanIgnoreReturnValue public[SequentialAgent.Builder](SequentialAgent.Builder.html)afterAgentCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback) -
### build


-


---

<!-- DOCUMENTO FUSIONADO: llmagentincludecontentshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/LlmAgent.IncludeContents.html -->

# Enum Class LlmAgent.IncludeContents

- All Implemented Interfaces:

,[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html)

,[Comparable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Comparable.html)<[LlmAgent.IncludeContents](LlmAgent.IncludeContents.html)>[Constable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/constant/Constable.html)

- Enclosing class:
[LlmAgent](LlmAgent.html)

Enum to define if contents of previous events should be included in requests to the underlying
LLM.

-
## Nested Class Summary

### Nested classes/interfaces inherited from class java.lang.

[Enum](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.html)[Enum.EnumDesc](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.EnumDesc.html)<[E](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.EnumDesc.html#type-param-E)extends[Enum](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.html)<[E](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.EnumDesc.html#type-param-E)>> -
## Enum Constant Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[LlmAgent.IncludeContents](LlmAgent.IncludeContents.html)Returns the enum constant of this class with the specified name.`static`

[LlmAgent.IncludeContents](LlmAgent.IncludeContents.html)[][values](#values())()Returns an array containing the constants of this enum class, in the order they are declared.

-
## Enum Constant Details

-
### DEFAULT

-
### NONE


-
-
## Method Details

-
### values

Returns an array containing the constants of this enum class, in the order they are declared.- Returns:
- an array containing the constants of this enum class, in the order they are declared

-
### valueOf

Returns the enum constant of this class with the specified name. The string must match*exactly*an identifier used to declare an enum constant in this class. (Extraneous whitespace characters are not permitted.)- Parameters:
`name`

- the name of the enum constant to be returned.- Returns:
- the enum constant with the specified name
- Throws:

- if this enum class has no constant with the specified name[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)

- if the argument is null[NullPointerException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/NullPointerException.html)


-


---

<!-- DOCUMENTO FUSIONADO: sequentialagenthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/SequentialAgent.html -->

# Class SequentialAgent

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.agents.BaseAgent](BaseAgent.html)

com.google.adk.agents.SequentialAgent

An agent that runs its sub-agents sequentially.

-
## Nested Class Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[SequentialAgent.Builder](SequentialAgent.Builder.html)[builder](#builder())()`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runAsyncImpl](#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Runs sub-agents sequentially.`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runLiveImpl](#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Runs sub-agents sequentially in live mode.### Methods inherited from class com.google.adk.agents.

[BaseAgent](BaseAgent.html)[afterAgentCallback](BaseAgent.html#afterAgentCallback()),[beforeAgentCallback](BaseAgent.html#beforeAgentCallback()),[description](BaseAgent.html#description()),[findAgent](BaseAgent.html#findAgent(java.lang.String)),[findSubAgent](BaseAgent.html#findSubAgent(java.lang.String)),[name](BaseAgent.html#name()),[parentAgent](BaseAgent.html#parentAgent()),[parentAgent](BaseAgent.html#parentAgent(com.google.adk.agents.BaseAgent)),[rootAgent](BaseAgent.html#rootAgent()),[runAsync](BaseAgent.html#runAsync(com.google.adk.agents.InvocationContext)),[runLive](BaseAgent.html#runLive(com.google.adk.agents.InvocationContext)),[subAgents](BaseAgent.html#subAgents())

-
## Method Details

-
### builder

-
### runAsyncImpl

protected io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runAsyncImpl( [InvocationContext](InvocationContext.html)invocationContext)Runs sub-agents sequentially.- Specified by:

in class[runAsyncImpl](BaseAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))[BaseAgent](BaseAgent.html)- Parameters:
`invocationContext`

- Invocation context.- Returns:
- Flowable emitting events from sub-agents.

-
### runLiveImpl

protected io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runLiveImpl( [InvocationContext](InvocationContext.html)invocationContext)Runs sub-agents sequentially in live mode.- Specified by:

in class[runLiveImpl](BaseAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))[BaseAgent](BaseAgent.html)- Parameters:
`invocationContext`

- Invocation context.- Returns:
- Flowable emitting events from sub-agents in live mode.


-


---

<!-- DOCUMENTO FUSIONADO: runconfigbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/RunConfig.Builder.html -->

# Class RunConfig.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.RunConfig.Builder

- Enclosing class:
[RunConfig](RunConfig.html)

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[build](#build())()`abstract`

[RunConfig.Builder](RunConfig.Builder.html)[setMaxLlmCalls](#setMaxLlmCalls(int))(int maxLlmCalls) `abstract`

[RunConfig.Builder](RunConfig.Builder.html)[setOutputAudioTranscription](#setOutputAudioTranscription(com.google.genai.types.AudioTranscriptionConfig))(com.google.genai.types.AudioTranscriptionConfig outputAudioTranscription) `abstract`

[RunConfig.Builder](RunConfig.Builder.html)[setResponseModalities](#setResponseModalities(java.lang.Iterable))( [Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<com.google.genai.types.Modality> responseModalities)`abstract`

[RunConfig.Builder](RunConfig.Builder.html)[setSaveInputBlobsAsArtifacts](#setSaveInputBlobsAsArtifacts(boolean))(boolean saveInputBlobsAsArtifacts) `abstract`

[RunConfig.Builder](RunConfig.Builder.html)[setSpeechConfig](#setSpeechConfig(com.google.genai.types.SpeechConfig))(com.google.genai.types.SpeechConfig speechConfig) `abstract`

[RunConfig.Builder](RunConfig.Builder.html)[setStreamingMode](#setStreamingMode(com.google.adk.agents.RunConfig.StreamingMode))( [RunConfig.StreamingMode](RunConfig.StreamingMode.html)streamingMode)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### setSpeechConfig

@CanIgnoreReturnValue public abstract[RunConfig.Builder](RunConfig.Builder.html)setSpeechConfig(com.google.genai.types.SpeechConfig speechConfig) -
### setResponseModalities

@CanIgnoreReturnValue public abstract[RunConfig.Builder](RunConfig.Builder.html)setResponseModalities( [Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<com.google.genai.types.Modality> responseModalities) -
### setSaveInputBlobsAsArtifacts

@CanIgnoreReturnValue public abstract[RunConfig.Builder](RunConfig.Builder.html)setSaveInputBlobsAsArtifacts(boolean saveInputBlobsAsArtifacts) -
### setStreamingMode

@CanIgnoreReturnValue public abstract[RunConfig.Builder](RunConfig.Builder.html)setStreamingMode( [RunConfig.StreamingMode](RunConfig.StreamingMode.html)streamingMode) -
### setOutputAudioTranscription

@CanIgnoreReturnValue public abstract[RunConfig.Builder](RunConfig.Builder.html)setOutputAudioTranscription(com.google.genai.types.AudioTranscriptionConfig outputAudioTranscription) -
### setMaxLlmCalls

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: loopagentbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/LoopAgent.Builder.html -->

# Class LoopAgent.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.LoopAgent.Builder

- Enclosing class:
[LoopAgent](LoopAgent.html)

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[afterAgentCallback](#afterAgentCallback(com.google.adk.agents.Callbacks.AfterAgentCallback))( [Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)afterAgentCallback)[afterAgentCallback](#afterAgentCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback)[beforeAgentCallback](#beforeAgentCallback(com.google.adk.agents.Callbacks.BeforeAgentCallback))( [Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)beforeAgentCallback)[beforeAgentCallback](#beforeAgentCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback)[build](#build())()[description](#description(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description)[maxIterations](#maxIterations(int))(int maxIterations) [maxIterations](#maxIterations(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> maxIterations)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### name

-
### description

-
### subAgents

-
### subAgents

-
### maxIterations

-
### maxIterations

-
### beforeAgentCallback

@CanIgnoreReturnValue public[LoopAgent.Builder](LoopAgent.Builder.html)beforeAgentCallback( [Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)beforeAgentCallback) -
### beforeAgentCallback

@CanIgnoreReturnValue public[LoopAgent.Builder](LoopAgent.Builder.html)beforeAgentCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback) -
### afterAgentCallback

@CanIgnoreReturnValue public[LoopAgent.Builder](LoopAgent.Builder.html)afterAgentCallback( [Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)afterAgentCallback) -
### afterAgentCallback

@CanIgnoreReturnValue public[LoopAgent.Builder](LoopAgent.Builder.html)afterAgentCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback) -
### build


-


---

<!-- DOCUMENTO FUSIONADO: loopagenthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/LoopAgent.html -->

# Class LoopAgent

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.agents.BaseAgent](BaseAgent.html)

com.google.adk.agents.LoopAgent

An agent that runs its sub-agents sequentially in a loop.

The loop continues until a sub-agent escalates, or until the maximum number of iterations is reached (if specified).

-
## Nested Class Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[LoopAgent.Builder](LoopAgent.Builder.html)[builder](#builder())()`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runAsyncImpl](#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Agent-specific asynchronous logic.`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runLiveImpl](#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Agent-specific synchronous logic.### Methods inherited from class com.google.adk.agents.

[BaseAgent](BaseAgent.html)[afterAgentCallback](BaseAgent.html#afterAgentCallback()),[beforeAgentCallback](BaseAgent.html#beforeAgentCallback()),[description](BaseAgent.html#description()),[findAgent](BaseAgent.html#findAgent(java.lang.String)),[findSubAgent](BaseAgent.html#findSubAgent(java.lang.String)),[name](BaseAgent.html#name()),[parentAgent](BaseAgent.html#parentAgent()),[parentAgent](BaseAgent.html#parentAgent(com.google.adk.agents.BaseAgent)),[rootAgent](BaseAgent.html#rootAgent()),[runAsync](BaseAgent.html#runAsync(com.google.adk.agents.InvocationContext)),[runLive](BaseAgent.html#runLive(com.google.adk.agents.InvocationContext)),[subAgents](BaseAgent.html#subAgents())

-
## Method Details

-
### builder

-
### runAsyncImpl

protected io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runAsyncImpl( [InvocationContext](InvocationContext.html)invocationContext)Description copied from class:[BaseAgent](BaseAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))Agent-specific asynchronous logic.- Specified by:

in class[runAsyncImpl](BaseAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))[BaseAgent](BaseAgent.html)- Parameters:
`invocationContext`

- Current invocation context.- Returns:
- stream of agent-generated events.

-
### runLiveImpl

protected io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runLiveImpl( [InvocationContext](InvocationContext.html)invocationContext)Description copied from class:[BaseAgent](BaseAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))Agent-specific synchronous logic.- Specified by:

in class[runLiveImpl](BaseAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))[BaseAgent](BaseAgent.html)- Parameters:
`invocationContext`

- Current invocation context.- Returns:
- stream of agent-generated events.


-


---

<!-- DOCUMENTO FUSIONADO: parallelagenthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/ParallelAgent.html -->

# Class ParallelAgent

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.agents.BaseAgent](BaseAgent.html)

com.google.adk.agents.ParallelAgent

A shell agent that runs its sub-agents in parallel in isolated manner.

This approach is beneficial for scenarios requiring multiple perspectives or attempts on a single task, such as running different algorithms simultaneously or generating multiple responses for review by a subsequent evaluation agent.

-
## Nested Class Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[ParallelAgent.Builder](ParallelAgent.Builder.html)[builder](#builder())()`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runAsyncImpl](#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Runs sub-agents in parallel and emits their events.`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runLiveImpl](#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Not supported for ParallelAgent.### Methods inherited from class com.google.adk.agents.

[BaseAgent](BaseAgent.html)[afterAgentCallback](BaseAgent.html#afterAgentCallback()),[beforeAgentCallback](BaseAgent.html#beforeAgentCallback()),[description](BaseAgent.html#description()),[findAgent](BaseAgent.html#findAgent(java.lang.String)),[findSubAgent](BaseAgent.html#findSubAgent(java.lang.String)),[name](BaseAgent.html#name()),[parentAgent](BaseAgent.html#parentAgent()),[parentAgent](BaseAgent.html#parentAgent(com.google.adk.agents.BaseAgent)),[rootAgent](BaseAgent.html#rootAgent()),[runAsync](BaseAgent.html#runAsync(com.google.adk.agents.InvocationContext)),[runLive](BaseAgent.html#runLive(com.google.adk.agents.InvocationContext)),[subAgents](BaseAgent.html#subAgents())

-
## Method Details

-
### builder

-
### runAsyncImpl

protected io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runAsyncImpl( [InvocationContext](InvocationContext.html)invocationContext)Runs sub-agents in parallel and emits their events.Sets the branch and merges event streams from all sub-agents.

- Specified by:

in class[runAsyncImpl](BaseAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))[BaseAgent](BaseAgent.html)- Parameters:
`invocationContext`

- Invocation context.- Returns:
- Flowable emitting events from all sub-agents.

-
### runLiveImpl

protected io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runLiveImpl( [InvocationContext](InvocationContext.html)invocationContext)Not supported for ParallelAgent.- Specified by:

in class[runLiveImpl](BaseAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))[BaseAgent](BaseAgent.html)- Parameters:
`invocationContext`

- Invocation context.- Returns:
- Flowable that always throws UnsupportedOperationException.


-


---

<!-- DOCUMENTO FUSIONADO: instructionproviderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/Instruction.Provider.html -->

# Record Class Instruction.Provider

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[java.lang.Record](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Record.html)

com.google.adk.agents.Instruction.Provider

- All Implemented Interfaces:
[Instruction](Instruction.html)

- Enclosing interface:
[Instruction](Instruction.html)

public static record Instruction.Provider(

[Function](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/function/Function.html)<[ReadonlyContext](ReadonlyContext.html), io.reactivex.rxjava3.core.Single<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>> getInstruction) extends[Record](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Record.html)implements[Instruction](Instruction.html)Returns an instruction dynamically constructed from the given context.

-
## Nested Class Summary

### Nested classes/interfaces inherited from interface com.google.adk.agents.

[Instruction](Instruction.html)[Instruction.Provider](Instruction.Provider.html),[Instruction.Static](Instruction.Static.html) -
## Constructor Summary

ConstructorDescription[Provider](#%3Cinit%3E(java.util.function.Function))( [Function](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/function/Function.html)<[ReadonlyContext](ReadonlyContext.html), io.reactivex.rxjava3.core.Single<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>> getInstruction)Creates an instance of a`Provider`

record class. -
## Method Summary

Modifier and TypeMethodDescription`final boolean`

Indicates whether some other object is "equal to" this one.[Function](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/function/Function.html)< [ReadonlyContext](ReadonlyContext.html), io.reactivex.rxjava3.core.Single<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>>Returns the value of the`getInstruction`

record component.`final int`

[hashCode](#hashCode())()Returns a hash code value for this object.`final`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[toString](#toString())()Returns a string representation of this record class.

-
## Constructor Details

-
### Provider

Creates an instance of a`Provider`

record class.- Parameters:
`getInstruction`

- the value for the`getInstruction`

record component


-
-
## Method Details

-
### toString

-
### hashCode

-
### equals

Indicates whether some other object is "equal to" this one. The objects are equal if the other object is of the same class and if all the record components are equal. All components in this record class are compared with.`Objects::equals(Object,Object)`

-
### getInstruction

Returns the value of the`getInstruction`

record component.- Returns:
- the value of the
`getInstruction`

record component


-


---

<!-- DOCUMENTO FUSIONADO: invocationcontexthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/InvocationContext.html -->

# Class InvocationContext

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.InvocationContext

The context for an agent invocation.

-
## Method Summary

Modifier and TypeMethodDescription[agent](#agent())()`void`

[appName](#appName())()[branch](#branch())()`void`

`static`

[InvocationContext](InvocationContext.html)[copyOf](#copyOf(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)other)`static`

[InvocationContext](InvocationContext.html)[create](#create(com.google.adk.sessions.BaseSessionService,com.google.adk.artifacts.BaseArtifactService,com.google.adk.agents.BaseAgent,com.google.adk.sessions.Session,com.google.adk.agents.LiveRequestQueue,com.google.adk.agents.RunConfig))( [BaseSessionService](../sessions/BaseSessionService.html)sessionService,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService,[BaseAgent](BaseAgent.html)agent,[Session](../sessions/Session.html)session,[LiveRequestQueue](LiveRequestQueue.html)liveRequestQueue,[RunConfig](RunConfig.html)runConfig)`static`

[InvocationContext](InvocationContext.html)[create](#create(com.google.adk.sessions.BaseSessionService,com.google.adk.artifacts.BaseArtifactService,java.lang.String,com.google.adk.agents.BaseAgent,com.google.adk.sessions.Session,com.google.genai.types.Content,com.google.adk.agents.RunConfig))( [BaseSessionService](../sessions/BaseSessionService.html)sessionService,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)invocationId,[BaseAgent](BaseAgent.html)agent,[Session](../sessions/Session.html)session, com.google.genai.types.Content userContent,[RunConfig](RunConfig.html)runConfig)`boolean`

`boolean`

`int`

[hashCode](#hashCode())()`void`

`static`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[session](#session())()`void`

[setEndInvocation](#setEndInvocation(boolean))(boolean endInvocation) [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Content> [userId](#userId())()

-
## Method Details

-
### create

public static[InvocationContext](InvocationContext.html)create( [BaseSessionService](../sessions/BaseSessionService.html)sessionService,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)invocationId,[BaseAgent](BaseAgent.html)agent,[Session](../sessions/Session.html)session, com.google.genai.types.Content userContent,[RunConfig](RunConfig.html)runConfig) -
### create

public static[InvocationContext](InvocationContext.html)create( [BaseSessionService](../sessions/BaseSessionService.html)sessionService,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService,[BaseAgent](BaseAgent.html)agent,[Session](../sessions/Session.html)session,[LiveRequestQueue](LiveRequestQueue.html)liveRequestQueue,[RunConfig](RunConfig.html)runConfig) -
### copyOf

-
### sessionService

-
### artifactService

-
### liveRequestQueue

-
### invocationId

-
### branch

-
### branch

-
### agent

-
### agent

-
### session

-
### userContent

-
### runConfig

-
### endInvocation

public boolean endInvocation() -
### setEndInvocation

public void setEndInvocation(boolean endInvocation) -
### appName

-
### userId

-
### newInvocationContextId

-
### incrementLlmCallsCount

- Throws:
[LlmCallsLimitExceededException](../exceptions/LlmCallsLimitExceededException.html)

-
### equals

-
### hashCode


-


---

<!-- DOCUMENTO FUSIONADO: callbackcontexthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/CallbackContext.html -->

# Class CallbackContext

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.agents.ReadonlyContext](ReadonlyContext.html)

com.google.adk.agents.CallbackContext

- Direct Known Subclasses:
[ToolContext](../tools/ToolContext.html)

The context of various callbacks for an agent invocation.

-
## Field Summary

### Fields inherited from class com.google.adk.agents.

[ReadonlyContext](ReadonlyContext.html)[invocationContext](ReadonlyContext.html#invocationContext) -
## Constructor Summary

ConstructorDescription[CallbackContext](#%3Cinit%3E(com.google.adk.agents.InvocationContext,com.google.adk.events.EventActions))( [InvocationContext](InvocationContext.html)invocationContext,[EventActions](../events/EventActions.html)eventActions)Initializes callback context. -
## Method Summary

Modifier and TypeMethodDescriptionReturns the EventActions associated with this context.`io.reactivex.rxjava3.core.Maybe`

<com.google.genai.types.Part> [loadArtifact](#loadArtifact(java.lang.String,java.util.Optional))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> version)Loads an artifact from the artifact service associated with the current session.`void`

[saveArtifact](#saveArtifact(java.lang.String,com.google.genai.types.Part))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename, com.google.genai.types.Part artifact)Saves an artifact and records it as a delta for the current session.[state](#state())()Returns the delta-aware state of the current callback.### Methods inherited from class com.google.adk.agents.

[ReadonlyContext](ReadonlyContext.html)[agentName](ReadonlyContext.html#agentName()),[branch](ReadonlyContext.html#branch()),[events](ReadonlyContext.html#events()),[invocationId](ReadonlyContext.html#invocationId()),[sessionId](ReadonlyContext.html#sessionId()),[userContent](ReadonlyContext.html#userContent())

-
## Field Details

-
### eventActions


-
-
## Constructor Details

-
### CallbackContext

Initializes callback context.- Parameters:
`invocationContext`

- Current invocation context.`eventActions`

- Callback event actions.


-
-
## Method Details

-
### state

Returns the delta-aware state of the current callback.- Overrides:

in class[state](ReadonlyContext.html#state())[ReadonlyContext](ReadonlyContext.html)

-
### eventActions

Returns the EventActions associated with this context. -
### loadArtifact

public io.reactivex.rxjava3.core.Maybe<com.google.genai.types.Part> loadArtifact( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> version)Loads an artifact from the artifact service associated with the current session.- Parameters:
`filename`

- Artifact file name.`version`

- Artifact version (optional).- Returns:
- loaded part, or empty if not found.
- Throws:

- if the artifact service is not initialized.[IllegalStateException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalStateException.html)

-
### saveArtifact

Saves an artifact and records it as a delta for the current session.- Parameters:
`filename`

- Artifact file name.`artifact`

- Artifact content to save.- Throws:

- if the artifact service is not initialized.[IllegalStateException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalStateException.html)


-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/package-tree.html -->

# Hierarchy For Package com.google.adk.agents

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.agents.
[BaseAgent](BaseAgent.html)- com.google.adk.agents.
[LlmAgent](LlmAgent.html) - com.google.adk.agents.
[LoopAgent](LoopAgent.html) - com.google.adk.agents.
[ParallelAgent](ParallelAgent.html) - com.google.adk.agents.
[SequentialAgent](SequentialAgent.html)

- com.google.adk.agents.
- com.google.adk.agents.
[BaseAgentConfig](BaseAgentConfig.html)- com.google.adk.agents.
[LlmAgentConfig](LlmAgentConfig.html)

- com.google.adk.agents.
- com.google.adk.agents.
[Callbacks](Callbacks.html) - com.google.adk.agents.
[CallbackUtil](CallbackUtil.html) - com.google.adk.agents.
[InvocationContext](InvocationContext.html) - com.google.adk.
[JsonBaseModel](../JsonBaseModel.html)- com.google.adk.agents.
[LiveRequest](LiveRequest.html)

- com.google.adk.agents.
- com.google.adk.agents.
[LiveRequest.Builder](LiveRequest.Builder.html) - com.google.adk.agents.
[LiveRequestQueue](LiveRequestQueue.html) - com.google.adk.agents.
[LlmAgent.Builder](LlmAgent.Builder.html) - com.google.adk.agents.
[LoopAgent.Builder](LoopAgent.Builder.html) - com.google.adk.agents.
[ParallelAgent.Builder](ParallelAgent.Builder.html) - com.google.adk.agents.
[ReadonlyContext](ReadonlyContext.html)- com.google.adk.agents.
[CallbackContext](CallbackContext.html)

- com.google.adk.agents.
- com.google.adk.agents.
[RunConfig](RunConfig.html) - com.google.adk.agents.
[RunConfig.Builder](RunConfig.Builder.html) - com.google.adk.agents.
[SequentialAgent.Builder](SequentialAgent.Builder.html)

- com.google.adk.agents.

## Interface Hierarchy

- com.google.adk.agents.Callbacks.AfterAgentCallbackBase
- com.google.adk.agents.
[Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html) - com.google.adk.agents.
[Callbacks.AfterAgentCallbackSync](Callbacks.AfterAgentCallbackSync.html)

- com.google.adk.agents.
- com.google.adk.agents.Callbacks.AfterModelCallbackBase
- com.google.adk.agents.
[Callbacks.AfterModelCallback](Callbacks.AfterModelCallback.html) - com.google.adk.agents.
[Callbacks.AfterModelCallbackSync](Callbacks.AfterModelCallbackSync.html)

- com.google.adk.agents.
- com.google.adk.agents.Callbacks.AfterToolCallbackBase
- com.google.adk.agents.
[Callbacks.AfterToolCallback](Callbacks.AfterToolCallback.html) - com.google.adk.agents.
[Callbacks.AfterToolCallbackSync](Callbacks.AfterToolCallbackSync.html)

- com.google.adk.agents.
- com.google.adk.agents.Callbacks.BeforeAgentCallbackBase
- com.google.adk.agents.
[Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html) - com.google.adk.agents.
[Callbacks.BeforeAgentCallbackSync](Callbacks.BeforeAgentCallbackSync.html)

- com.google.adk.agents.
- com.google.adk.agents.Callbacks.BeforeModelCallbackBase
- com.google.adk.agents.
[Callbacks.BeforeModelCallback](Callbacks.BeforeModelCallback.html) - com.google.adk.agents.
[Callbacks.BeforeModelCallbackSync](Callbacks.BeforeModelCallbackSync.html)

- com.google.adk.agents.
- com.google.adk.agents.Callbacks.BeforeToolCallbackBase
- com.google.adk.agents.
[Callbacks.BeforeToolCallback](Callbacks.BeforeToolCallback.html) - com.google.adk.agents.
[Callbacks.BeforeToolCallbackSync](Callbacks.BeforeToolCallbackSync.html)

- com.google.adk.agents.
- com.google.adk.agents.
[Instruction](Instruction.html)

## Enum Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- java.lang.
[Enum](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Enum.html)<E> (implements java.lang.[Comparable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Comparable.html)<T>, java.lang.constant.[Constable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/constant/Constable.html), java.io.[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html))- com.google.adk.agents.
[LlmAgent.IncludeContents](LlmAgent.IncludeContents.html) - com.google.adk.agents.
[RunConfig.StreamingMode](RunConfig.StreamingMode.html)

- com.google.adk.agents.

- java.lang.

## Record Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- java.lang.
[Record](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Record.html)- com.google.adk.agents.
[Instruction.Provider](Instruction.Provider.html)(implements com.google.adk.agents.[Instruction](Instruction.html)) - com.google.adk.agents.
[Instruction.Static](Instruction.Static.html)(implements com.google.adk.agents.[Instruction](Instruction.html))

- com.google.adk.agents.

- java.lang.


---

<!-- DOCUMENTO FUSIONADO: baseagenthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/BaseAgent.html -->

# Class BaseAgent

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.BaseAgent

- Direct Known Subclasses:

,[LlmAgent](LlmAgent.html)

,[LoopAgent](LoopAgent.html)

,[ParallelAgent](ParallelAgent.html)[SequentialAgent](SequentialAgent.html)

Base class for all agents.

-
## Constructor Summary

ConstructorDescription[BaseAgent](#%3Cinit%3E(java.lang.String,java.lang.String,java.util.List,java.util.List,java.util.List))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)name,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<? extends[BaseAgent](BaseAgent.html)> subAgents,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)> beforeAgentCallback,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)> afterAgentCallback)Creates a new BaseAgent. -
## Method Summary

Modifier and TypeMethodDescription`final`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)Gets the one-line description of the agent's capability.Finds an agent (this or descendant) by name.`@Nullable`

[BaseAgent](BaseAgent.html)[findSubAgent](#findSubAgent(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)name)Recursively search sub agent by name.`final`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[name](#name())()Gets the agent's unique name.Retrieves the parent agent in the agent tree.`protected void`

[parentAgent](#parentAgent(com.google.adk.agents.BaseAgent))( [BaseAgent](BaseAgent.html)parentAgent)Sets the parent agent.Returns the root agent for this agent by traversing up the parent chain.`io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runAsync](#runAsync(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)parentContext)Runs the agent asynchronously.`protected abstract io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runAsyncImpl](#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Agent-specific asynchronous logic.`io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runLive](#runLive(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)parentContext)Runs the agent synchronously.`protected abstract io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runLiveImpl](#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Agent-specific synchronous logic.

-
## Constructor Details

-
### BaseAgent

public BaseAgent( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)name,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<? extends[BaseAgent](BaseAgent.html)> subAgents,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)> beforeAgentCallback,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)> afterAgentCallback)Creates a new BaseAgent.- Parameters:
`name`

- Unique agent name. Cannot be "user" (reserved).`description`

- Agent purpose.`subAgents`

- Agents managed by this agent.`beforeAgentCallback`

- Callbacks before agent execution. Invoked in order until one doesn't return null.`afterAgentCallback`

- Callbacks after agent execution. Invoked in order until one doesn't return null.


-
-
## Method Details

-
### name

-
### description

Gets the one-line description of the agent's capability.- Returns:
- the description of the agent.

-
### parentAgent

Retrieves the parent agent in the agent tree.- Returns:
- the parent agent, or
`null`

if this agent does not have a parent.

-
### parentAgent

Sets the parent agent.- Parameters:
`parentAgent`

- The parent agent to set.

-
### rootAgent

Returns the root agent for this agent by traversing up the parent chain.- Returns:
- the root agent.

-
### findAgent

-
### findSubAgent

-
### subAgents

-
### beforeAgentCallback

-
### afterAgentCallback

-
### runAsync

Runs the agent asynchronously.- Parameters:
`parentContext`

- Parent context to inherit.- Returns:
- stream of agent-generated events.

-
### runLive

Runs the agent synchronously.- Parameters:
`parentContext`

- Parent context to inherit.- Returns:
- stream of agent-generated events.

-
### runAsyncImpl

protected abstract io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runAsyncImpl( [InvocationContext](InvocationContext.html)invocationContext)Agent-specific asynchronous logic.- Parameters:
`invocationContext`

- Current invocation context.- Returns:
- stream of agent-generated events.

-
### runLiveImpl

protected abstract io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runLiveImpl( [InvocationContext](InvocationContext.html)invocationContext)Agent-specific synchronous logic.- Parameters:
`invocationContext`

- Current invocation context.- Returns:
- stream of agent-generated events.


-


---

<!-- DOCUMENTO FUSIONADO: llmagenthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/LlmAgent.html -->

# Class LlmAgent

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.agents.BaseAgent](BaseAgent.html)

com.google.adk.agents.LlmAgent

The LLM-based agent.

-
## Nested Class Summary

Modifier and TypeClassDescription`static class`

Builder for.`LlmAgent`

`static enum`

Enum to define if contents of previous events should be included in requests to the underlying LLM. -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[LlmAgent.Builder](LlmAgent.Builder.html)[builder](#builder())()Returns afor`LlmAgent.Builder`

.`LlmAgent`

Constructs the text global instruction for this agent based on the`globalInstruction`

field.[canonicalInstruction](#canonicalInstruction(com.google.adk.agents.ReadonlyContext))( [ReadonlyContext](ReadonlyContext.html)context)Constructs the text instruction for this agent based on the`instruction`

field.`io.reactivex.rxjava3.core.Flowable`

< [BaseTool](../tools/BaseTool.html)>Overload of canonicalTools that defaults to an empty context.`io.reactivex.rxjava3.core.Flowable`

< [BaseTool](../tools/BaseTool.html)>[canonicalTools](#canonicalTools(com.google.adk.agents.ReadonlyContext))( [ReadonlyContext](ReadonlyContext.html)context)Convenience overload of canonicalTools that accepts a non-optional ReadonlyContext.`io.reactivex.rxjava3.core.Flowable`

< [BaseTool](../tools/BaseTool.html)>[canonicalTools](#canonicalTools(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[ReadonlyContext](ReadonlyContext.html)> context)Constructs the list of tools for this agent based on thefield.`tools()`

`protected`

[BaseLlmFlow](../flows/llmflows/BaseLlmFlow.html)`boolean`

`boolean`

[executor](#executor())()[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.GenerateContentConfig> [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Schema> [maxSteps](#maxSteps())()[model](#model())()[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.Schema> `boolean`

[planning](#planning())()`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runAsyncImpl](#runAsyncImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Agent-specific asynchronous logic.`protected io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runLiveImpl](#runLiveImpl(com.google.adk.agents.InvocationContext))( [InvocationContext](InvocationContext.html)invocationContext)Agent-specific synchronous logic.[tools](#tools())()### Methods inherited from class com.google.adk.agents.

[BaseAgent](BaseAgent.html)[afterAgentCallback](BaseAgent.html#afterAgentCallback()),[beforeAgentCallback](BaseAgent.html#beforeAgentCallback()),[description](BaseAgent.html#description()),[findAgent](BaseAgent.html#findAgent(java.lang.String)),[findSubAgent](BaseAgent.html#findSubAgent(java.lang.String)),[name](BaseAgent.html#name()),[parentAgent](BaseAgent.html#parentAgent()),[parentAgent](BaseAgent.html#parentAgent(com.google.adk.agents.BaseAgent)),[rootAgent](BaseAgent.html#rootAgent()),[runAsync](BaseAgent.html#runAsync(com.google.adk.agents.InvocationContext)),[runLive](BaseAgent.html#runLive(com.google.adk.agents.InvocationContext)),[subAgents](BaseAgent.html#subAgents())

-
## Constructor Details

-
### LlmAgent


-
-
## Method Details

-
### builder

Returns afor`LlmAgent.Builder`

.`LlmAgent`

-
### determineLlmFlow

-
### runAsyncImpl

protected io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runAsyncImpl( [InvocationContext](InvocationContext.html)invocationContext)Description copied from class:[BaseAgent](BaseAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))Agent-specific asynchronous logic.- Specified by:

in class[runAsyncImpl](BaseAgent.html#runAsyncImpl(com.google.adk.agents.InvocationContext))[BaseAgent](BaseAgent.html)- Parameters:
`invocationContext`

- Current invocation context.- Returns:
- stream of agent-generated events.

-
### runLiveImpl

protected io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runLiveImpl( [InvocationContext](InvocationContext.html)invocationContext)Description copied from class:[BaseAgent](BaseAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))Agent-specific synchronous logic.- Specified by:

in class[runLiveImpl](BaseAgent.html#runLiveImpl(com.google.adk.agents.InvocationContext))[BaseAgent](BaseAgent.html)- Parameters:
`invocationContext`

- Current invocation context.- Returns:
- stream of agent-generated events.

-
### canonicalInstruction

public io.reactivex.rxjava3.core.Single<[Map.Entry](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.Entry.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)>> canonicalInstruction( [ReadonlyContext](ReadonlyContext.html)context)Constructs the text instruction for this agent based on the`instruction`

field. Also returns a boolean indicating that state injection should be bypassed when the instruction is constructed with an.`Instruction.Provider`

This method is only for use by Agent Development Kit.

- Parameters:
`context`

- The context to retrieve the session state.- Returns:
- The resolved instruction as a
`Single`

wrapped Map.Entry. The key is the instruction string and the value is a boolean indicating if state injection should be bypassed.

-
### canonicalGlobalInstruction

public io.reactivex.rxjava3.core.Single<[Map.Entry](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.Entry.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Boolean](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Boolean.html)>> canonicalGlobalInstruction( [ReadonlyContext](ReadonlyContext.html)context)Constructs the text global instruction for this agent based on the`globalInstruction`

field. Also returns a boolean indicating that state injection should be bypassed when the instruction is constructed with an.`Instruction.Provider`

This method is only for use by Agent Development Kit.

- Parameters:
`context`

- The context to retrieve the session state.- Returns:
- The resolved global instruction as a
`Single`

wrapped Map.Entry. The key is the instruction string and the value is a boolean indicating if state injection should be bypassed.

-
### canonicalTools

public io.reactivex.rxjava3.core.Flowable<[BaseTool](../tools/BaseTool.html)> canonicalTools( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[ReadonlyContext](ReadonlyContext.html)> context)Constructs the list of tools for this agent based on thefield.`tools()`

This method is only for use by Agent Development Kit.

- Parameters:
`context`

- The context to retrieve the session state.- Returns:
- The resolved list of tools as a
`Single`

wrapped list of.`BaseTool`


-
### canonicalTools

Overload of canonicalTools that defaults to an empty context. -
### canonicalTools

Convenience overload of canonicalTools that accepts a non-optional ReadonlyContext. -
### instruction

-
### globalInstruction

-
### model

-
### planning

public boolean planning() -
### maxSteps

-
### generateContentConfig

-
### exampleProvider

-
### includeContents

-
### tools

-
### toolsUnion

-
### disallowTransferToParent

public boolean disallowTransferToParent() -
### disallowTransferToPeers

public boolean disallowTransferToPeers() -
### beforeModelCallback

-
### afterModelCallback

-
### beforeToolCallback

-
### afterToolCallback

-
### inputSchema

-
### outputSchema

-
### executor

-
### outputKey

-
### resolvedModel


-


---

<!-- DOCUMENTO FUSIONADO: llmagentbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/agents/LlmAgent.Builder.html -->

# Class LlmAgent.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.agents.LlmAgent.Builder

- Enclosing class:
[LlmAgent](LlmAgent.html)

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[afterAgentCallback](#afterAgentCallback(com.google.adk.agents.Callbacks.AfterAgentCallback))( [Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)afterAgentCallback)[afterAgentCallback](#afterAgentCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback)[afterAgentCallbackSync](#afterAgentCallbackSync(com.google.adk.agents.Callbacks.AfterAgentCallbackSync))( [Callbacks.AfterAgentCallbackSync](Callbacks.AfterAgentCallbackSync.html)afterAgentCallbackSync)[afterModelCallback](#afterModelCallback(com.google.adk.agents.Callbacks.AfterModelCallback))( [Callbacks.AfterModelCallback](Callbacks.AfterModelCallback.html)afterModelCallback)[afterModelCallback](#afterModelCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterModelCallbackBase> afterModelCallback)[afterModelCallbackSync](#afterModelCallbackSync(com.google.adk.agents.Callbacks.AfterModelCallbackSync))( [Callbacks.AfterModelCallbackSync](Callbacks.AfterModelCallbackSync.html)afterModelCallbackSync)[afterToolCallback](#afterToolCallback(com.google.adk.agents.Callbacks.AfterToolCallback))( [Callbacks.AfterToolCallback](Callbacks.AfterToolCallback.html)afterToolCallback)[afterToolCallback](#afterToolCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterToolCallbackBase> afterToolCallbacks)[afterToolCallbackSync](#afterToolCallbackSync(com.google.adk.agents.Callbacks.AfterToolCallbackSync))( [Callbacks.AfterToolCallbackSync](Callbacks.AfterToolCallbackSync.html)afterToolCallbackSync)[beforeAgentCallback](#beforeAgentCallback(com.google.adk.agents.Callbacks.BeforeAgentCallback))( [Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)beforeAgentCallback)[beforeAgentCallback](#beforeAgentCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback)[beforeAgentCallbackSync](#beforeAgentCallbackSync(com.google.adk.agents.Callbacks.BeforeAgentCallbackSync))( [Callbacks.BeforeAgentCallbackSync](Callbacks.BeforeAgentCallbackSync.html)beforeAgentCallbackSync)[beforeModelCallback](#beforeModelCallback(com.google.adk.agents.Callbacks.BeforeModelCallback))( [Callbacks.BeforeModelCallback](Callbacks.BeforeModelCallback.html)beforeModelCallback)[beforeModelCallback](#beforeModelCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeModelCallbackBase> beforeModelCallback)[beforeModelCallbackSync](#beforeModelCallbackSync(com.google.adk.agents.Callbacks.BeforeModelCallbackSync))( [Callbacks.BeforeModelCallbackSync](Callbacks.BeforeModelCallbackSync.html)beforeModelCallbackSync)[beforeToolCallback](#beforeToolCallback(com.google.adk.agents.Callbacks.BeforeToolCallback))( [Callbacks.BeforeToolCallback](Callbacks.BeforeToolCallback.html)beforeToolCallback)[beforeToolCallback](#beforeToolCallback(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeToolCallbackBase> beforeToolCallbacks)[beforeToolCallbackSync](#beforeToolCallbackSync(com.google.adk.agents.Callbacks.BeforeToolCallbackSync))( [Callbacks.BeforeToolCallbackSync](Callbacks.BeforeToolCallbackSync.html)beforeToolCallbackSync)[build](#build())()[description](#description(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)description)[disallowTransferToParent](#disallowTransferToParent(boolean))(boolean disallowTransferToParent) [disallowTransferToPeers](#disallowTransferToPeers(boolean))(boolean disallowTransferToPeers) [exampleProvider](#exampleProvider(com.google.adk.examples.BaseExampleProvider))( [BaseExampleProvider](../examples/BaseExampleProvider.html)exampleProvider)[exampleProvider](#exampleProvider(com.google.adk.examples.Example...))( [Example](../examples/Example.html)... examples)[exampleProvider](#exampleProvider(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[Example](../examples/Example.html)> examples)[generateContentConfig](#generateContentConfig(com.google.genai.types.GenerateContentConfig))(com.google.genai.types.GenerateContentConfig generateContentConfig) [globalInstruction](#globalInstruction(com.google.adk.agents.Instruction))( [Instruction](Instruction.html)globalInstruction)[globalInstruction](#globalInstruction(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)globalInstruction)[includeContents](#includeContents(com.google.adk.agents.LlmAgent.IncludeContents))( [LlmAgent.IncludeContents](LlmAgent.IncludeContents.html)includeContents)[inputSchema](#inputSchema(com.google.genai.types.Schema))(com.google.genai.types.Schema inputSchema) [instruction](#instruction(com.google.adk.agents.Instruction))( [Instruction](Instruction.html)instruction)[instruction](#instruction(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)instruction)[maxSteps](#maxSteps(int))(int maxSteps) [outputSchema](#outputSchema(com.google.genai.types.Schema))(com.google.genai.types.Schema outputSchema) [planning](#planning(boolean))(boolean planning) `protected void`

[validate](#validate())()

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### name

-
### description

-
### model

-
### model

-
### instruction

-
### instruction

-
### globalInstruction

-
### globalInstruction

-
### subAgents

-
### subAgents

-
### tools

-
### tools

-
### generateContentConfig

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)generateContentConfig(com.google.genai.types.GenerateContentConfig generateContentConfig) -
### exampleProvider

-
### exampleProvider

-
### exampleProvider

-
### includeContents

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)includeContents( [LlmAgent.IncludeContents](LlmAgent.IncludeContents.html)includeContents) -
### planning

-
### maxSteps

-
### disallowTransferToParent

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)disallowTransferToParent(boolean disallowTransferToParent) -
### disallowTransferToPeers

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)disallowTransferToPeers(boolean disallowTransferToPeers) -
### beforeModelCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)beforeModelCallback( [Callbacks.BeforeModelCallback](Callbacks.BeforeModelCallback.html)beforeModelCallback) -
### beforeModelCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)beforeModelCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeModelCallbackBase> beforeModelCallback) -
### beforeModelCallbackSync

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)beforeModelCallbackSync( [Callbacks.BeforeModelCallbackSync](Callbacks.BeforeModelCallbackSync.html)beforeModelCallbackSync) -
### afterModelCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)afterModelCallback( [Callbacks.AfterModelCallback](Callbacks.AfterModelCallback.html)afterModelCallback) -
### afterModelCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)afterModelCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterModelCallbackBase> afterModelCallback) -
### afterModelCallbackSync

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)afterModelCallbackSync( [Callbacks.AfterModelCallbackSync](Callbacks.AfterModelCallbackSync.html)afterModelCallbackSync) -
### beforeAgentCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)beforeAgentCallback( [Callbacks.BeforeAgentCallback](Callbacks.BeforeAgentCallback.html)beforeAgentCallback) -
### beforeAgentCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)beforeAgentCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeAgentCallbackBase> beforeAgentCallback) -
### beforeAgentCallbackSync

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)beforeAgentCallbackSync( [Callbacks.BeforeAgentCallbackSync](Callbacks.BeforeAgentCallbackSync.html)beforeAgentCallbackSync) -
### afterAgentCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)afterAgentCallback( [Callbacks.AfterAgentCallback](Callbacks.AfterAgentCallback.html)afterAgentCallback) -
### afterAgentCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)afterAgentCallback( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterAgentCallbackBase> afterAgentCallback) -
### afterAgentCallbackSync

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)afterAgentCallbackSync( [Callbacks.AfterAgentCallbackSync](Callbacks.AfterAgentCallbackSync.html)afterAgentCallbackSync) -
### beforeToolCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)beforeToolCallback( [Callbacks.BeforeToolCallback](Callbacks.BeforeToolCallback.html)beforeToolCallback) -
### beforeToolCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)beforeToolCallback(@Nullable [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.BeforeToolCallbackBase> beforeToolCallbacks) -
### beforeToolCallbackSync

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)beforeToolCallbackSync( [Callbacks.BeforeToolCallbackSync](Callbacks.BeforeToolCallbackSync.html)beforeToolCallbackSync) -
### afterToolCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)afterToolCallback( [Callbacks.AfterToolCallback](Callbacks.AfterToolCallback.html)afterToolCallback) -
### afterToolCallback

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)afterToolCallback(@Nullable [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.adk.agents.Callbacks.AfterToolCallbackBase> afterToolCallbacks) -
### afterToolCallbackSync

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)afterToolCallbackSync( [Callbacks.AfterToolCallbackSync](Callbacks.AfterToolCallbackSync.html)afterToolCallbackSync) -
### inputSchema

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)inputSchema(com.google.genai.types.Schema inputSchema) -
### outputSchema

@CanIgnoreReturnValue public[LlmAgent.Builder](LlmAgent.Builder.html)outputSchema(com.google.genai.types.Schema outputSchema) -
### executor

-
### outputKey

-
### validate

protected void validate() -
### build


-
