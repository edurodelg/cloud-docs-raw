---
merged_at: 2026-01-25T02:21:31.977950
merged_files: 3
---

# Documentos Fusionados

Este archivo contiene 3 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _audio_all.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _class-use_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vertexspeechclienthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/audio/class-use/VertexSpeechClient.html -->

# Uses of Classcom.google.adk.flows.llmflows.audio.VertexSpeechClient

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows.audio
VertexSpeechClient
Uses of Class
com.google.adk.flows.llmflows.audio.VertexSpeechClient
No usage of com.google.adk.flows.llmflows.audio.VertexSpeechClient


---

<!-- DOCUMENTO FUSIONADO: speechclientinterfacehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/audio/class-use/SpeechClientInterface.html -->

# Uses of Interfacecom.google.adk.flows.llmflows.audio.SpeechClientInterface

# Uses of Interface

com.google.adk.flows.llmflows.audio.SpeechClientInterface

-
## Uses of

[SpeechClientInterface](../SpeechClientInterface.html)in[com.google.adk.flows.llmflows.audio](../package-summary.html)Modifier and TypeClassDescription`class`

Implementation of SpeechClientInterface using Vertex AI SpeechClient.


---

<!-- DOCUMENTO FUSIONADO: _audio_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 5 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/audio/package-use.html -->

# Uses of Packagecom.google.adk.flows.llmflows.audio

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.flows.llmflows.audio
Uses of Package
com.google.adk.flows.llmflows.audio
Packages that use
com.google.adk.flows.llmflows.audio
Package
Description
com.google.adk.flows.llmflows.audio
Classes in
com.google.adk.flows.llmflows.audio
used by
com.google.adk.flows.llmflows.audio
Class
Description
SpeechClientInterface
Interface for a speech-to-text client.


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/audio/package-summary.html -->

# Package com.google.adk.flows.llmflows.audio

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.flows.llmflows.audio
Contents
Hide sidebar
❮
❯
Show sidebar
Description
Related Packages
Classes and Interfaces
Package com.google.adk.flows.llmflows.audio
package
com.google.adk.flows.llmflows.audio
Related Packages
Package
Description
com.google.adk.flows.llmflows
All Classes and Interfaces
Interfaces
Classes
Class
Description
SpeechClientInterface
Interface for a speech-to-text client.
VertexSpeechClient
Implementation of SpeechClientInterface using Vertex AI SpeechClient.


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/audio/package-tree.html -->

# Hierarchy For Package com.google.adk.flows.llmflows.audio

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.flows.llmflows.audio.
[VertexSpeechClient](VertexSpeechClient.html)(implements com.google.adk.flows.llmflows.audio.[SpeechClientInterface](SpeechClientInterface.html))

- com.google.adk.flows.llmflows.audio.

## Interface Hierarchy

- java.lang.
[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)- com.google.adk.flows.llmflows.audio.
[SpeechClientInterface](SpeechClientInterface.html)

- com.google.adk.flows.llmflows.audio.


---

<!-- DOCUMENTO FUSIONADO: speechclientinterfacehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/audio/SpeechClientInterface.html -->

# Interface SpeechClientInterface

- All Superinterfaces:
[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

- All Known Implementing Classes:
[VertexSpeechClient](VertexSpeechClient.html)

Interface for a speech-to-text client. Allows for different implementations (e.g., Cloud, Mocks).

-
## Method Summary


-
## Method Details

-
### recognize

com.google.cloud.speech.v1.RecognizeResponse recognize(com.google.cloud.speech.v1.RecognitionConfig config, com.google.cloud.speech.v1.RecognitionAudio audio) throws [Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)Performs synchronous speech recognition.- Parameters:
`config`

- The recognition configuration.`audio`

- The audio data to transcribe.- Returns:
- The recognition response.
- Throws:

- if an error occurs during recognition.[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)

-
### close

Closes the client and releases any resources.- Specified by:

in interface[close](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html#close())[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)- Throws:

- if an error occurs during closing.[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)


-


---

<!-- DOCUMENTO FUSIONADO: vertexspeechclienthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/audio/VertexSpeechClient.html -->

# Class VertexSpeechClient

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.audio.VertexSpeechClient

- All Implemented Interfaces:

,[SpeechClientInterface](SpeechClientInterface.html)[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

Implementation of SpeechClientInterface using Vertex AI SpeechClient.

-
## Constructor Summary

ConstructorDescriptionConstructs a VertexSpeechClient, initializing the underlying Google Cloud SpeechClient. -
## Method Summary

Modifier and TypeMethodDescription`void`

[close](#close())()Closes the client and releases any resources.`com.google.cloud.speech.v1.RecognizeResponse`

[recognize](#recognize(com.google.cloud.speech.v1.RecognitionConfig,com.google.cloud.speech.v1.RecognitionAudio))(com.google.cloud.speech.v1.RecognitionConfig config, com.google.cloud.speech.v1.RecognitionAudio audio) Performs synchronous speech recognition on the given audio input.

-
## Constructor Details

-
### VertexSpeechClient

Constructs a VertexSpeechClient, initializing the underlying Google Cloud SpeechClient.- Throws:

- if SpeechClient creation fails.[IOException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/IOException.html)


-
-
## Method Details

-
### recognize

public com.google.cloud.speech.v1.RecognizeResponse recognize(com.google.cloud.speech.v1.RecognitionConfig config, com.google.cloud.speech.v1.RecognitionAudio audio) Performs synchronous speech recognition on the given audio input.- Specified by:

in interface[recognize](SpeechClientInterface.html#recognize(com.google.cloud.speech.v1.RecognitionConfig,com.google.cloud.speech.v1.RecognitionAudio))[SpeechClientInterface](SpeechClientInterface.html)- Parameters:
`config`

- Recognition configuration (e.g., language, encoding).`audio`

- Audio data to recognize.- Returns:
- The recognition result.

-
### close

Description copied from interface:[SpeechClientInterface](SpeechClientInterface.html#close())Closes the client and releases any resources.- Specified by:

in interface[close](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html#close())[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)- Specified by:

in interface[close](SpeechClientInterface.html#close())[SpeechClientInterface](SpeechClientInterface.html)- Throws:

- if an error occurs during closing.[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)


-


---

<!-- DOCUMENTO FUSIONADO: _class-use_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 14 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: basichtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/Basic.html -->

# Uses of Classcom.google.adk.flows.llmflows.Basic

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows
Basic
Uses of Class
com.google.adk.flows.llmflows.Basic
No usage of com.google.adk.flows.llmflows.Basic


---

<!-- DOCUMENTO FUSIONADO: contentshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/Contents.html -->

# Uses of Classcom.google.adk.flows.llmflows.Contents

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows
Contents
Uses of Class
com.google.adk.flows.llmflows.Contents
No usage of com.google.adk.flows.llmflows.Contents


---

<!-- DOCUMENTO FUSIONADO: exampleshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/Examples.html -->

# Uses of Classcom.google.adk.flows.llmflows.Examples

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows
Examples
Uses of Class
com.google.adk.flows.llmflows.Examples
No usage of com.google.adk.flows.llmflows.Examples


---

<!-- DOCUMENTO FUSIONADO: identityhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/Identity.html -->

# Uses of Classcom.google.adk.flows.llmflows.Identity

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows
Identity
Uses of Class
com.google.adk.flows.llmflows.Identity
No usage of com.google.adk.flows.llmflows.Identity


---

<!-- DOCUMENTO FUSIONADO: autoflowhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/AutoFlow.html -->

# Uses of Classcom.google.adk.flows.llmflows.AutoFlow

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows
AutoFlow
Uses of Class
com.google.adk.flows.llmflows.AutoFlow
No usage of com.google.adk.flows.llmflows.AutoFlow


---

<!-- DOCUMENTO FUSIONADO: functionshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/Functions.html -->

# Uses of Classcom.google.adk.flows.llmflows.Functions

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows
Functions
Uses of Class
com.google.adk.flows.llmflows.Functions
No usage of com.google.adk.flows.llmflows.Functions


---

<!-- DOCUMENTO FUSIONADO: instructionshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/Instructions.html -->

# Uses of Classcom.google.adk.flows.llmflows.Instructions

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows
Instructions
Uses of Class
com.google.adk.flows.llmflows.Instructions
No usage of com.google.adk.flows.llmflows.Instructions


---

<!-- DOCUMENTO FUSIONADO: agenttransferhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/AgentTransfer.html -->

# Uses of Classcom.google.adk.flows.llmflows.AgentTransfer

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows
AgentTransfer
Uses of Class
com.google.adk.flows.llmflows.AgentTransfer
No usage of com.google.adk.flows.llmflows.AgentTransfer


---

<!-- DOCUMENTO FUSIONADO: basellmflowhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/BaseLlmFlow.html -->

# Uses of Classcom.google.adk.flows.llmflows.BaseLlmFlow

# Uses of Class

com.google.adk.flows.llmflows.BaseLlmFlow

-
## Uses of

[BaseLlmFlow](../BaseLlmFlow.html)in[com.google.adk.agents](../../../agents/package-summary.html) -
## Uses of

[BaseLlmFlow](../BaseLlmFlow.html)in[com.google.adk.flows.llmflows](../package-summary.html)Modifier and TypeClassDescription`class`

LLM flow with automatic agent transfer support.`class`

Basic LLM flow with fixed request processors and no response post-processing.


---

<!-- DOCUMENTO FUSIONADO: singleflowhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/SingleFlow.html -->

# Uses of Classcom.google.adk.flows.llmflows.SingleFlow

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.flows.llmflows
SingleFlow
Uses of Class
com.google.adk.flows.llmflows.SingleFlow
Packages that use
SingleFlow
Package
Description
com.google.adk.flows.llmflows
Uses of
SingleFlow
in
com.google.adk.flows.llmflows
Subclasses of
SingleFlow
in
com.google.adk.flows.llmflows
Modifier and Type
Class
Description
class
AutoFlow
LLM flow with automatic agent transfer support.


---

<!-- DOCUMENTO FUSIONADO: responseprocessorhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/ResponseProcessor.html -->

# Uses of Interfacecom.google.adk.flows.llmflows.ResponseProcessor

# Uses of Interface

com.google.adk.flows.llmflows.ResponseProcessor

-
## Uses of

[ResponseProcessor](../ResponseProcessor.html)in[com.google.adk.flows.llmflows](../package-summary.html)Modifier and TypeFieldDescription`protected static final com.google.common.collect.ImmutableList`

< [ResponseProcessor](../ResponseProcessor.html)>SingleFlow.[RESPONSE_PROCESSORS](../SingleFlow.html#RESPONSE_PROCESSORS)`protected final`

[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)< [ResponseProcessor](../ResponseProcessor.html)>BaseLlmFlow.[responseProcessors](../BaseLlmFlow.html#responseProcessors)


---

<!-- DOCUMENTO FUSIONADO: responseprocessorresponseprocessingresulthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/ResponseProcessor.ResponseProcessingResult.html -->

# Uses of Classcom.google.adk.flows.llmflows.ResponseProcessor.ResponseProcessingResult

# Uses of Class

com.google.adk.flows.llmflows.ResponseProcessor.ResponseProcessingResult

-
## Uses of

[ResponseProcessor.ResponseProcessingResult](../ResponseProcessor.ResponseProcessingResult.html)in[com.google.adk.flows.llmflows](../package-summary.html)Modifier and TypeMethodDescriptionResponseProcessor.ResponseProcessingResult.[create](../ResponseProcessor.ResponseProcessingResult.html#create(com.google.adk.models.LlmResponse,java.lang.Iterable,java.util.Optional))( [LlmResponse](../../../models/LlmResponse.html)updatedResponse,[Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<[Event](../../../events/Event.html)> events,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> transferToAgent)Modifier and TypeMethodDescription`protected io.reactivex.rxjava3.core.Single`

< [ResponseProcessor.ResponseProcessingResult](../ResponseProcessor.ResponseProcessingResult.html)>BaseLlmFlow.[postprocess](../BaseLlmFlow.html#postprocess(com.google.adk.agents.InvocationContext,com.google.adk.events.Event,com.google.adk.models.LlmRequest,com.google.adk.models.LlmResponse))( [InvocationContext](../../../agents/InvocationContext.html)context,[Event](../../../events/Event.html)baseEventForLlmResponse,[LlmRequest](../../../models/LlmRequest.html)llmRequest,[LlmResponse](../../../models/LlmResponse.html)llmResponse)Post-processes the LLM response after receiving it from the LLM.`io.reactivex.rxjava3.core.Single`

< [ResponseProcessor.ResponseProcessingResult](../ResponseProcessor.ResponseProcessingResult.html)>ResponseProcessor.[processResponse](../ResponseProcessor.html#processResponse(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmResponse))( [InvocationContext](../../../agents/InvocationContext.html)context,[LlmResponse](../../../models/LlmResponse.html)response)Process the LLM response as part of the post-processing stage.


---

<!-- DOCUMENTO FUSIONADO: requestprocessorhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/RequestProcessor.html -->

# Uses of Interfacecom.google.adk.flows.llmflows.RequestProcessor

# Uses of Interface

com.google.adk.flows.llmflows.RequestProcessor

-
## Uses of

[RequestProcessor](../RequestProcessor.html)in[com.google.adk.flows.llmflows](../package-summary.html)Modifier and TypeClassDescription`final class`

that handles agent transfer for LLM flow.`RequestProcessor`

`final class`

that handles basic information to build the LLM request.`RequestProcessor`

`final class`

that populates content in request for LLM flows.`RequestProcessor`

`final class`

that populates examples in LLM request.`RequestProcessor`

`final class`

that gives the agent identity from the framework`RequestProcessor`

`final class`

that handles instructions and global instructions for LLM flows.`RequestProcessor`

Modifier and TypeFieldDescription`protected static final com.google.common.collect.ImmutableList`

< [RequestProcessor](../RequestProcessor.html)>SingleFlow.[REQUEST_PROCESSORS](../SingleFlow.html#REQUEST_PROCESSORS)`protected final`

[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)< [RequestProcessor](../RequestProcessor.html)>BaseLlmFlow.[requestProcessors](../BaseLlmFlow.html#requestProcessors)ModifierConstructorDescription[BaseLlmFlow](../BaseLlmFlow.html#%3Cinit%3E(java.util.List,java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[RequestProcessor](../RequestProcessor.html)> requestProcessors,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[ResponseProcessor](../ResponseProcessor.html)> responseProcessors)[BaseLlmFlow](../BaseLlmFlow.html#%3Cinit%3E(java.util.List,java.util.List,java.util.Optional))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[RequestProcessor](../RequestProcessor.html)> requestProcessors,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[ResponseProcessor](../ResponseProcessor.html)> responseProcessors,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> maxSteps)`protected`

[SingleFlow](../SingleFlow.html#%3Cinit%3E(java.util.List,java.util.List,java.util.Optional))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[RequestProcessor](../RequestProcessor.html)> requestProcessors,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[ResponseProcessor](../ResponseProcessor.html)> responseProcessors,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> maxSteps)


---

<!-- DOCUMENTO FUSIONADO: requestprocessorrequestprocessingresulthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/class-use/RequestProcessor.RequestProcessingResult.html -->

# Uses of Classcom.google.adk.flows.llmflows.RequestProcessor.RequestProcessingResult

# Uses of Class

com.google.adk.flows.llmflows.RequestProcessor.RequestProcessingResult

-
## Uses of

[RequestProcessor.RequestProcessingResult](../RequestProcessor.RequestProcessingResult.html)in[com.google.adk.flows.llmflows](../package-summary.html)Modifier and TypeMethodDescriptionRequestProcessor.RequestProcessingResult.[create](../RequestProcessor.RequestProcessingResult.html#create(com.google.adk.models.LlmRequest,java.lang.Iterable))( [LlmRequest](../../../models/LlmRequest.html)updatedRequest,[Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<[Event](../../../events/Event.html)> events)Modifier and TypeMethodDescription`protected io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](../RequestProcessor.RequestProcessingResult.html)>BaseLlmFlow.[preprocess](../BaseLlmFlow.html#preprocess(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../../agents/InvocationContext.html)context,[LlmRequest](../../../models/LlmRequest.html)llmRequest)Pre-processes the LLM request before sending it to the LLM.`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](../RequestProcessor.RequestProcessingResult.html)>AgentTransfer.[processRequest](../AgentTransfer.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../../agents/InvocationContext.html)context,[LlmRequest](../../../models/LlmRequest.html)request)`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](../RequestProcessor.RequestProcessingResult.html)>Basic.[processRequest](../Basic.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../../agents/InvocationContext.html)context,[LlmRequest](../../../models/LlmRequest.html)request)`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](../RequestProcessor.RequestProcessingResult.html)>Contents.[processRequest](../Contents.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../../agents/InvocationContext.html)context,[LlmRequest](../../../models/LlmRequest.html)request)`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](../RequestProcessor.RequestProcessingResult.html)>Examples.[processRequest](../Examples.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../../agents/InvocationContext.html)context,[LlmRequest](../../../models/LlmRequest.html)request)`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](../RequestProcessor.RequestProcessingResult.html)>Identity.[processRequest](../Identity.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../../agents/InvocationContext.html)context,[LlmRequest](../../../models/LlmRequest.html)request)`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](../RequestProcessor.RequestProcessingResult.html)>Instructions.[processRequest](../Instructions.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../../agents/InvocationContext.html)context,[LlmRequest](../../../models/LlmRequest.html)request)`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](../RequestProcessor.RequestProcessingResult.html)>RequestProcessor.[processRequest](../RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../../agents/InvocationContext.html)context,[LlmRequest](../../../models/LlmRequest.html)request)Process the LLM request as part of the pre-processing stage.


---

<!-- DOCUMENTO FUSIONADO: _llmflows_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 17 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/package-use.html -->

# Uses of Packagecom.google.adk.flows.llmflows

# Uses of Package

com.google.adk.flows.llmflows

-
ClassDescriptionA basic flow that calls the LLM in a loop until a final response is generated.
-
ClassDescriptionA basic flow that calls the LLM in a loop until a final response is generated.Basic LLM flow with fixed request processors and no response post-processing.


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/package-summary.html -->

# Package com.google.adk.flows.llmflows

package com.google.adk.flows.llmflows

-
ClassDescription
that handles agent transfer for LLM flow.`RequestProcessor`

LLM flow with automatic agent transfer support.A basic flow that calls the LLM in a loop until a final response is generated.that handles basic information to build the LLM request.`RequestProcessor`

that populates content in request for LLM flows.`RequestProcessor`

that populates examples in LLM request.`RequestProcessor`

Utility class for handling function calls.that gives the agent identity from the framework`RequestProcessor`

that handles instructions and global instructions for LLM flows.`RequestProcessor`

Basic LLM flow with fixed request processors and no response post-processing.


---

<!-- DOCUMENTO FUSIONADO: responseprocessorresponseprocessingresulthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/ResponseProcessor.ResponseProcessingResult.html -->

# Class ResponseProcessor.ResponseProcessingResult

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.ResponseProcessor.ResponseProcessingResult

- Enclosing interface:
[ResponseProcessor](ResponseProcessor.html)

-
## Constructor Summary

-
## Method Summary


-
## Constructor Details

-
### ResponseProcessingResult

public ResponseProcessingResult()

-
-
## Method Details

-
### updatedResponse

-
### events

-
### transferToAgent

-
### create

public static[ResponseProcessor.ResponseProcessingResult](ResponseProcessor.ResponseProcessingResult.html)create( [LlmResponse](../../models/LlmResponse.html)updatedResponse,[Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<[Event](../../events/Event.html)> events,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> transferToAgent)

-


---

<!-- DOCUMENTO FUSIONADO: responseprocessorhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/ResponseProcessor.html -->

# Interface ResponseProcessor

public interface ResponseProcessor

-
## Nested Class Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [ResponseProcessor.ResponseProcessingResult](ResponseProcessor.ResponseProcessingResult.html)>[processResponse](#processResponse(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmResponse))( [InvocationContext](../../agents/InvocationContext.html)context,[LlmResponse](../../models/LlmResponse.html)response)Process the LLM response as part of the post-processing stage.

-
## Method Details

-
### processResponse

io.reactivex.rxjava3.core.Single<[ResponseProcessor.ResponseProcessingResult](ResponseProcessor.ResponseProcessingResult.html)> processResponse( [InvocationContext](../../agents/InvocationContext.html)context,[LlmResponse](../../models/LlmResponse.html)response)Process the LLM response as part of the post-processing stage.- Parameters:
`context`

- the invocation context.`response`

- the LLM response to process.- Returns:
- a list of events generated during processing (if any).


-


---

<!-- DOCUMENTO FUSIONADO: requestprocessorrequestprocessingresulthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/RequestProcessor.RequestProcessingResult.html -->

# Class RequestProcessor.RequestProcessingResult

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.RequestProcessor.RequestProcessingResult

- Enclosing interface:
[RequestProcessor](RequestProcessor.html)

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[create](#create(com.google.adk.models.LlmRequest,java.lang.Iterable))( [LlmRequest](../../models/LlmRequest.html)updatedRequest,[Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<[Event](../../events/Event.html)> events)[events](#events())()`abstract`

[LlmRequest](../../models/LlmRequest.html)

-
## Constructor Details

-
### RequestProcessingResult

public RequestProcessingResult()

-
-
## Method Details

-
### updatedRequest

-
### events

-
### create

public static[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)create( [LlmRequest](../../models/LlmRequest.html)updatedRequest,[Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<[Event](../../events/Event.html)> events)

-


---

<!-- DOCUMENTO FUSIONADO: requestprocessorhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/RequestProcessor.html -->

# Interface RequestProcessor

- All Known Implementing Classes:

,[AgentTransfer](AgentTransfer.html)

,[Basic](Basic.html)

,[Contents](Contents.html)

,[Examples](Examples.html)

,[Identity](Identity.html)[Instructions](Instructions.html)

public interface RequestProcessor

-
## Nested Class Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)>[processRequest](#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Process the LLM request as part of the pre-processing stage.

-
## Method Details

-
### processRequest

io.reactivex.rxjava3.core.Single<[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)> processRequest( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Process the LLM request as part of the pre-processing stage.- Parameters:
`context`

- the invocation context.`request`

- the LLM request to process.- Returns:
- a list of events generated during processing (if any).


-


---

<!-- DOCUMENTO FUSIONADO: autoflowhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/AutoFlow.html -->

# Class AutoFlow

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.flows.llmflows.BaseLlmFlow](BaseLlmFlow.html)

[com.google.adk.flows.llmflows.SingleFlow](SingleFlow.html)

com.google.adk.flows.llmflows.AutoFlow

- All Implemented Interfaces:
[BaseFlow](../BaseFlow.html)

LLM flow with automatic agent transfer support.

-
## Field Summary

### Fields inherited from class com.google.adk.flows.llmflows.

[BaseLlmFlow](BaseLlmFlow.html)[maxSteps](BaseLlmFlow.html#maxSteps),[requestProcessors](BaseLlmFlow.html#requestProcessors),[responseProcessors](BaseLlmFlow.html#responseProcessors),[stepsCompleted](BaseLlmFlow.html#stepsCompleted) -
## Constructor Summary

-
## Method Summary

### Methods inherited from class com.google.adk.flows.llmflows.

[BaseLlmFlow](BaseLlmFlow.html)[postprocess](BaseLlmFlow.html#postprocess(com.google.adk.agents.InvocationContext,com.google.adk.events.Event,com.google.adk.models.LlmRequest,com.google.adk.models.LlmResponse)),[preprocess](BaseLlmFlow.html#preprocess(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest)),[run](BaseLlmFlow.html#run(com.google.adk.agents.InvocationContext)),[runLive](BaseLlmFlow.html#runLive(com.google.adk.agents.InvocationContext))

-
## Constructor Details

-
### AutoFlow

public AutoFlow() -
### AutoFlow


-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/package-tree.html -->

# Hierarchy For Package com.google.adk.flows.llmflows

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.flows.llmflows.
[AgentTransfer](AgentTransfer.html)(implements com.google.adk.flows.llmflows.[RequestProcessor](RequestProcessor.html)) - com.google.adk.flows.llmflows.
[BaseLlmFlow](BaseLlmFlow.html)(implements com.google.adk.flows.[BaseFlow](../BaseFlow.html))- com.google.adk.flows.llmflows.
[SingleFlow](SingleFlow.html)- com.google.adk.flows.llmflows.
[AutoFlow](AutoFlow.html)

- com.google.adk.flows.llmflows.

- com.google.adk.flows.llmflows.
- com.google.adk.flows.llmflows.
[Basic](Basic.html)(implements com.google.adk.flows.llmflows.[RequestProcessor](RequestProcessor.html)) - com.google.adk.flows.llmflows.
[Contents](Contents.html)(implements com.google.adk.flows.llmflows.[RequestProcessor](RequestProcessor.html)) - com.google.adk.flows.llmflows.
[Examples](Examples.html)(implements com.google.adk.flows.llmflows.[RequestProcessor](RequestProcessor.html)) - com.google.adk.flows.llmflows.
[Functions](Functions.html) - com.google.adk.flows.llmflows.
[Identity](Identity.html)(implements com.google.adk.flows.llmflows.[RequestProcessor](RequestProcessor.html)) - com.google.adk.flows.llmflows.
[Instructions](Instructions.html)(implements com.google.adk.flows.llmflows.[RequestProcessor](RequestProcessor.html)) - com.google.adk.flows.llmflows.
[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html) - com.google.adk.flows.llmflows.
[ResponseProcessor.ResponseProcessingResult](ResponseProcessor.ResponseProcessingResult.html)

- com.google.adk.flows.llmflows.

## Interface Hierarchy

- com.google.adk.flows.llmflows.
[RequestProcessor](RequestProcessor.html) - com.google.adk.flows.llmflows.
[ResponseProcessor](ResponseProcessor.html)


---

<!-- DOCUMENTO FUSIONADO: exampleshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/Examples.html -->

# Class Examples

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.Examples

- All Implemented Interfaces:
[RequestProcessor](RequestProcessor.html)

[that populates examples in LLM request.](RequestProcessor.html)

`RequestProcessor`

-
## Nested Class Summary

### Nested classes/interfaces inherited from interface com.google.adk.flows.llmflows.

[RequestProcessor](RequestProcessor.html)[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html) -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)>[processRequest](#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Process the LLM request as part of the pre-processing stage.

-
## Constructor Details

-
### Examples

public Examples()

-
-
## Method Details

-
### processRequest

public io.reactivex.rxjava3.core.Single<[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)> processRequest( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Description copied from interface:[RequestProcessor](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))Process the LLM request as part of the pre-processing stage.- Specified by:

in interface[processRequest](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))[RequestProcessor](RequestProcessor.html)- Parameters:
`context`

- the invocation context.`request`

- the LLM request to process.- Returns:
- a list of events generated during processing (if any).


-


---

<!-- DOCUMENTO FUSIONADO: basichtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/Basic.html -->

# Class Basic

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.Basic

- All Implemented Interfaces:
[RequestProcessor](RequestProcessor.html)

[that handles basic information to build the LLM request.](RequestProcessor.html)

`RequestProcessor`

-
## Nested Class Summary

### Nested classes/interfaces inherited from interface com.google.adk.flows.llmflows.

[RequestProcessor](RequestProcessor.html)[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html) -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)>[processRequest](#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Process the LLM request as part of the pre-processing stage.

-
## Constructor Details

-
### Basic

public Basic()

-
-
## Method Details

-
### processRequest

public io.reactivex.rxjava3.core.Single<[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)> processRequest( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Description copied from interface:[RequestProcessor](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))Process the LLM request as part of the pre-processing stage.- Specified by:

in interface[processRequest](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))[RequestProcessor](RequestProcessor.html)- Parameters:
`context`

- the invocation context.`request`

- the LLM request to process.- Returns:
- a list of events generated during processing (if any).


-


---

<!-- DOCUMENTO FUSIONADO: contentshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/Contents.html -->

# Class Contents

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.Contents

- All Implemented Interfaces:
[RequestProcessor](RequestProcessor.html)

[that populates content in request for LLM flows.](RequestProcessor.html)

`RequestProcessor`

-
## Nested Class Summary

### Nested classes/interfaces inherited from interface com.google.adk.flows.llmflows.

[RequestProcessor](RequestProcessor.html)[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html) -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)>[processRequest](#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Process the LLM request as part of the pre-processing stage.

-
## Constructor Details

-
### Contents

public Contents()

-
-
## Method Details

-
### processRequest

public io.reactivex.rxjava3.core.Single<[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)> processRequest( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Description copied from interface:[RequestProcessor](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))Process the LLM request as part of the pre-processing stage.- Specified by:

in interface[processRequest](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))[RequestProcessor](RequestProcessor.html)- Parameters:
`context`

- the invocation context.`request`

- the LLM request to process.- Returns:
- a list of events generated during processing (if any).


-


---

<!-- DOCUMENTO FUSIONADO: identityhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/Identity.html -->

# Class Identity

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.Identity

- All Implemented Interfaces:
[RequestProcessor](RequestProcessor.html)

[that gives the agent identity from the framework](RequestProcessor.html)

`RequestProcessor`

-
## Nested Class Summary

### Nested classes/interfaces inherited from interface com.google.adk.flows.llmflows.

[RequestProcessor](RequestProcessor.html)[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html) -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)>[processRequest](#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Process the LLM request as part of the pre-processing stage.

-
## Constructor Details

-
### Identity

public Identity()

-
-
## Method Details

-
### processRequest

public io.reactivex.rxjava3.core.Single<[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)> processRequest( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Description copied from interface:[RequestProcessor](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))Process the LLM request as part of the pre-processing stage.- Specified by:

in interface[processRequest](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))[RequestProcessor](RequestProcessor.html)- Parameters:
`context`

- the invocation context.`request`

- the LLM request to process.- Returns:
- a list of events generated during processing (if any).


-


---

<!-- DOCUMENTO FUSIONADO: instructionshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/Instructions.html -->

# Class Instructions

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.Instructions

- All Implemented Interfaces:
[RequestProcessor](RequestProcessor.html)

[that handles instructions and global instructions for LLM flows.](RequestProcessor.html)

`RequestProcessor`

-
## Nested Class Summary

### Nested classes/interfaces inherited from interface com.google.adk.flows.llmflows.

[RequestProcessor](RequestProcessor.html)[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html) -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)>[processRequest](#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Process the LLM request as part of the pre-processing stage.

-
## Constructor Details

-
### Instructions

public Instructions()

-
-
## Method Details

-
### processRequest

public io.reactivex.rxjava3.core.Single<[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)> processRequest( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Description copied from interface:[RequestProcessor](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))Process the LLM request as part of the pre-processing stage.- Specified by:

in interface[processRequest](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))[RequestProcessor](RequestProcessor.html)- Parameters:
`context`

- the invocation context.`request`

- the LLM request to process.- Returns:
- a list of events generated during processing (if any).


-


---

<!-- DOCUMENTO FUSIONADO: functionshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/Functions.html -->

# Class Functions

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.Functions

Utility class for handling function calls.

-
## Method Summary

Modifier and TypeMethodDescription`static`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)Generates a unique ID for a function call.[getLongRunningFunctionCalls](#getLongRunningFunctionCalls(java.util.List,java.util.Map))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.FunctionCall> functionCalls,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[BaseTool](../../tools/BaseTool.html)> tools)`static io.reactivex.rxjava3.core.Maybe`

< [Event](../../events/Event.html)>[handleFunctionCalls](#handleFunctionCalls(com.google.adk.agents.InvocationContext,com.google.adk.events.Event,java.util.Map))( [InvocationContext](../../agents/InvocationContext.html)invocationContext,[Event](../../events/Event.html)functionCallEvent,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[BaseTool](../../tools/BaseTool.html)> tools)`static void`

[populateClientFunctionCallId](#populateClientFunctionCallId(com.google.adk.events.Event))( [Event](../../events/Event.html)modelResponseEvent)Populates missing function call IDs in the provided event's content.

-
## Method Details

-
### generateClientFunctionCallId

Generates a unique ID for a function call. -
### populateClientFunctionCallId

Populates missing function call IDs in the provided event's content.If the event contains function calls without an ID, this method generates a unique client-side ID for each and updates the event content.

- Parameters:
`modelResponseEvent`

- The event potentially containing function calls.

-
### handleFunctionCalls

-
### getLongRunningFunctionCalls


-


---

<!-- DOCUMENTO FUSIONADO: agenttransferhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/AgentTransfer.html -->

# Class AgentTransfer

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.AgentTransfer

- All Implemented Interfaces:
[RequestProcessor](RequestProcessor.html)

[that handles agent transfer for LLM flow.](RequestProcessor.html)

`RequestProcessor`

-
## Nested Class Summary

### Nested classes/interfaces inherited from interface com.google.adk.flows.llmflows.

[RequestProcessor](RequestProcessor.html)[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html) -
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)>[processRequest](#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Process the LLM request as part of the pre-processing stage.`static void`

[transferToAgent](#transferToAgent(java.lang.String,com.google.adk.tools.ToolContext))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)agentName,[ToolContext](../../tools/ToolContext.html)toolContext)Marks the target agent for transfer using the tool context.

-
## Constructor Details

-
### AgentTransfer

public AgentTransfer()

-
-
## Method Details

-
### processRequest

public io.reactivex.rxjava3.core.Single<[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)> processRequest( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)request)Description copied from interface:[RequestProcessor](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))Process the LLM request as part of the pre-processing stage.- Specified by:

in interface[processRequest](RequestProcessor.html#processRequest(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))[RequestProcessor](RequestProcessor.html)- Parameters:
`context`

- the invocation context.`request`

- the LLM request to process.- Returns:
- a list of events generated during processing (if any).

-
### transferToAgent

Marks the target agent for transfer using the tool context.

-


---

<!-- DOCUMENTO FUSIONADO: singleflowhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/SingleFlow.html -->

# Class SingleFlow

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.flows.llmflows.BaseLlmFlow](BaseLlmFlow.html)

com.google.adk.flows.llmflows.SingleFlow

- All Implemented Interfaces:
[BaseFlow](../BaseFlow.html)

- Direct Known Subclasses:
[AutoFlow](AutoFlow.html)

Basic LLM flow with fixed request processors and no response post-processing.

-
## Field Summary

Modifier and TypeFieldDescription`protected static final com.google.common.collect.ImmutableList`

< [RequestProcessor](RequestProcessor.html)>`protected static final com.google.common.collect.ImmutableList`

< [ResponseProcessor](ResponseProcessor.html)>### Fields inherited from class com.google.adk.flows.llmflows.

[BaseLlmFlow](BaseLlmFlow.html)[maxSteps](BaseLlmFlow.html#maxSteps),[requestProcessors](BaseLlmFlow.html#requestProcessors),[responseProcessors](BaseLlmFlow.html#responseProcessors),[stepsCompleted](BaseLlmFlow.html#stepsCompleted) -
## Constructor Summary

ModifierConstructorDescription`protected`

[SingleFlow](#%3Cinit%3E(java.util.List,java.util.List,java.util.Optional))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[RequestProcessor](RequestProcessor.html)> requestProcessors,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[ResponseProcessor](ResponseProcessor.html)> responseProcessors,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> maxSteps)[SingleFlow](#%3Cinit%3E(java.util.Optional))( [Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> maxSteps) -
## Method Summary

### Methods inherited from class com.google.adk.flows.llmflows.

[BaseLlmFlow](BaseLlmFlow.html)[postprocess](BaseLlmFlow.html#postprocess(com.google.adk.agents.InvocationContext,com.google.adk.events.Event,com.google.adk.models.LlmRequest,com.google.adk.models.LlmResponse)),[preprocess](BaseLlmFlow.html#preprocess(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest)),[run](BaseLlmFlow.html#run(com.google.adk.agents.InvocationContext)),[runLive](BaseLlmFlow.html#runLive(com.google.adk.agents.InvocationContext))

-
## Field Details

-
### REQUEST_PROCESSORS

-
### RESPONSE_PROCESSORS

protected static final com.google.common.collect.ImmutableList<[ResponseProcessor](ResponseProcessor.html)> RESPONSE_PROCESSORS

-
-
## Constructor Details

-
### SingleFlow

public SingleFlow() -
### SingleFlow

-
### SingleFlow

protected SingleFlow( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[RequestProcessor](RequestProcessor.html)> requestProcessors,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[ResponseProcessor](ResponseProcessor.html)> responseProcessors,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> maxSteps)

-


---

<!-- DOCUMENTO FUSIONADO: basellmflowhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/llmflows/BaseLlmFlow.html -->

# Class BaseLlmFlow

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.flows.llmflows.BaseLlmFlow

- All Implemented Interfaces:
[BaseFlow](../BaseFlow.html)

- Direct Known Subclasses:
[SingleFlow](SingleFlow.html)

-
## Field Summary

Modifier and TypeFieldDescription`protected final int`

`protected final`

[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)< [RequestProcessor](RequestProcessor.html)>`protected final`

[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)< [ResponseProcessor](ResponseProcessor.html)>`protected int`

-
## Constructor Summary

ConstructorDescription[BaseLlmFlow](#%3Cinit%3E(java.util.List,java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[RequestProcessor](RequestProcessor.html)> requestProcessors,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[ResponseProcessor](ResponseProcessor.html)> responseProcessors)[BaseLlmFlow](#%3Cinit%3E(java.util.List,java.util.List,java.util.Optional))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[RequestProcessor](RequestProcessor.html)> requestProcessors,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[ResponseProcessor](ResponseProcessor.html)> responseProcessors,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> maxSteps) -
## Method Summary

Modifier and TypeMethodDescription`protected io.reactivex.rxjava3.core.Single`

< [ResponseProcessor.ResponseProcessingResult](ResponseProcessor.ResponseProcessingResult.html)>[postprocess](#postprocess(com.google.adk.agents.InvocationContext,com.google.adk.events.Event,com.google.adk.models.LlmRequest,com.google.adk.models.LlmResponse))( [InvocationContext](../../agents/InvocationContext.html)context,[Event](../../events/Event.html)baseEventForLlmResponse,[LlmRequest](../../models/LlmRequest.html)llmRequest,[LlmResponse](../../models/LlmResponse.html)llmResponse)Post-processes the LLM response after receiving it from the LLM.`protected io.reactivex.rxjava3.core.Single`

< [RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)>[preprocess](#preprocess(com.google.adk.agents.InvocationContext,com.google.adk.models.LlmRequest))( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)llmRequest)Pre-processes the LLM request before sending it to the LLM.`io.reactivex.rxjava3.core.Flowable`

< [Event](../../events/Event.html)>[run](#run(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Executes the full LLM flow by repeatedly calling`runOneStep(com.google.adk.agents.InvocationContext)`

until a final response is produced.`io.reactivex.rxjava3.core.Flowable`

< [Event](../../events/Event.html)>[runLive](#runLive(com.google.adk.agents.InvocationContext))( [InvocationContext](../../agents/InvocationContext.html)invocationContext)Executes the LLM flow in streaming mode.

-
## Field Details

-
### requestProcessors

-
### responseProcessors

-
### stepsCompleted

protected int stepsCompleted -
### maxSteps

protected final int maxSteps

-
-
## Constructor Details

-
### BaseLlmFlow

public BaseLlmFlow( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[RequestProcessor](RequestProcessor.html)> requestProcessors,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[ResponseProcessor](ResponseProcessor.html)> responseProcessors) -
### BaseLlmFlow

public BaseLlmFlow( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[RequestProcessor](RequestProcessor.html)> requestProcessors,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[ResponseProcessor](ResponseProcessor.html)> responseProcessors,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> maxSteps)

-
-
## Method Details

-
### preprocess

protected io.reactivex.rxjava3.core.Single<[RequestProcessor.RequestProcessingResult](RequestProcessor.RequestProcessingResult.html)> preprocess( [InvocationContext](../../agents/InvocationContext.html)context,[LlmRequest](../../models/LlmRequest.html)llmRequest)Pre-processes the LLM request before sending it to the LLM. Executes all registered.`RequestProcessor`

-
### postprocess

protected io.reactivex.rxjava3.core.Single<[ResponseProcessor.ResponseProcessingResult](ResponseProcessor.ResponseProcessingResult.html)> postprocess( [InvocationContext](../../agents/InvocationContext.html)context,[Event](../../events/Event.html)baseEventForLlmResponse,[LlmRequest](../../models/LlmRequest.html)llmRequest,[LlmResponse](../../models/LlmResponse.html)llmResponse)Post-processes the LLM response after receiving it from the LLM. Executes all registeredinstances. Handles function calls if present in the response.`ResponseProcessor`

-
### run

Executes the full LLM flow by repeatedly calling`runOneStep(com.google.adk.agents.InvocationContext)`

until a final response is produced. -
### runLive

Executes the LLM flow in streaming mode.Handles sending history and live requests to the LLM, receiving responses, processing them, and managing agent transfers.


-
