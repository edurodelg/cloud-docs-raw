---
merged_at: 2026-01-25T02:21:31.866929
merged_files: 4
---

# Documentos Fusionados

Este archivo contiene 4 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/langchain4j/package-use.html -->

# Uses of Packagecom.google.adk.models.langchain4j

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.models.langchain4j
Uses of Package
com.google.adk.models.langchain4j
No usage of com.google.adk.models.langchain4j


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/langchain4j/package-tree.html -->

# Hierarchy For Package com.google.adk.models.langchain4j

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.models.langchain4j
Hierarchy For Package com.google.adk.models.langchain4j
Package Hierarchies:
All Packages
Class Hierarchy
java.lang.
Object
com.google.adk.models.
BaseLlm
com.google.adk.models.langchain4j.
LangChain4j


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/langchain4j/package-summary.html -->

# Package com.google.adk.models.langchain4j

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.models.langchain4j
Contents
Hide sidebar
❮
❯
Show sidebar
Description
Related Packages
Classes and Interfaces
Package com.google.adk.models.langchain4j
package
com.google.adk.models.langchain4j
Related Packages
Package
Description
com.google.adk.models
Classes
Class
Description
LangChain4j


---

<!-- DOCUMENTO FUSIONADO: langchain4jhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/models/langchain4j/LangChain4j.html -->

# Class LangChain4j

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.models.BaseLlm](../BaseLlm.html)

com.google.adk.models.langchain4j.LangChain4j

-
## Constructor Summary

ConstructorDescription[LangChain4j](#%3Cinit%3E(dev.langchain4j.model.chat.ChatModel))(dev.langchain4j.model.chat.ChatModel chatModel) [LangChain4j](#%3Cinit%3E(dev.langchain4j.model.chat.ChatModel,dev.langchain4j.model.chat.StreamingChatModel,java.lang.String))(dev.langchain4j.model.chat.ChatModel chatModel, dev.langchain4j.model.chat.StreamingChatModel streamingChatModel, [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)modelName)[LangChain4j](#%3Cinit%3E(dev.langchain4j.model.chat.ChatModel,java.lang.String))(dev.langchain4j.model.chat.ChatModel chatModel, [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)modelName)[LangChain4j](#%3Cinit%3E(dev.langchain4j.model.chat.StreamingChatModel))(dev.langchain4j.model.chat.StreamingChatModel streamingChatModel) [LangChain4j](#%3Cinit%3E(dev.langchain4j.model.chat.StreamingChatModel,java.lang.String))(dev.langchain4j.model.chat.StreamingChatModel streamingChatModel, [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)modelName) -
## Method Summary

Modifier and TypeMethodDescription[connect](#connect(com.google.adk.models.LlmRequest))( [LlmRequest](../LlmRequest.html)llmRequest)Creates a live connection to the LLM.`io.reactivex.rxjava3.core.Flowable`

< [LlmResponse](../LlmResponse.html)>[generateContent](#generateContent(com.google.adk.models.LlmRequest,boolean))( [LlmRequest](../LlmRequest.html)llmRequest, boolean stream)Generates one content from the given LLM request and tools.

-
## Constructor Details

-
### LangChain4j

public LangChain4j(dev.langchain4j.model.chat.ChatModel chatModel) -
### LangChain4j

-
### LangChain4j

public LangChain4j(dev.langchain4j.model.chat.StreamingChatModel streamingChatModel) -
### LangChain4j

public LangChain4j(dev.langchain4j.model.chat.StreamingChatModel streamingChatModel, [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)modelName) -
### LangChain4j

public LangChain4j(dev.langchain4j.model.chat.ChatModel chatModel, dev.langchain4j.model.chat.StreamingChatModel streamingChatModel, [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)modelName)

-
-
## Method Details

-
### generateContent

public io.reactivex.rxjava3.core.Flowable<[LlmResponse](../LlmResponse.html)> generateContent( [LlmRequest](../LlmRequest.html)llmRequest, boolean stream)Description copied from class:[BaseLlm](../BaseLlm.html#generateContent(com.google.adk.models.LlmRequest,boolean))Generates one content from the given LLM request and tools.- Specified by:

in class[generateContent](../BaseLlm.html#generateContent(com.google.adk.models.LlmRequest,boolean))[BaseLlm](../BaseLlm.html)- Parameters:
`llmRequest`

- The LLM request containing the input prompt and parameters.`stream`

- A boolean flag indicating whether to stream the response.- Returns:
- A Flowable of LlmResponses. For non-streaming calls, it will only yield one LlmResponse. For streaming calls, it may yield more than one LlmResponse, but all yielded LlmResponses should be treated as one content by merging their parts.

-
### connect

Description copied from class:[BaseLlm](../BaseLlm.html#connect(com.google.adk.models.LlmRequest))Creates a live connection to the LLM.

-
