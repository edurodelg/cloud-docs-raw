---
merged_at: 2026-01-25T02:21:31.819758
merged_files: 6
---

# Documentos Fusionados

Este archivo contiene 6 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: inmemorymemoryservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/class-use/InMemoryMemoryService.html -->

# Uses of Classcom.google.adk.memory.InMemoryMemoryService

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.memory
InMemoryMemoryService
Uses of Class
com.google.adk.memory.InMemoryMemoryService
No usage of com.google.adk.memory.InMemoryMemoryService


---

<!-- DOCUMENTO FUSIONADO: basememoryservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/class-use/BaseMemoryService.html -->

# Uses of Interfacecom.google.adk.memory.BaseMemoryService

# Uses of Interface

com.google.adk.memory.BaseMemoryService

-
## Uses of

[BaseMemoryService](../BaseMemoryService.html)in[com.google.adk.memory](../package-summary.html)Modifier and TypeClassDescription`final class`

An in-memory memory service for prototyping purposes only.


---

<!-- DOCUMENTO FUSIONADO: searchmemoryresponsebuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/class-use/SearchMemoryResponse.Builder.html -->

# Uses of Classcom.google.adk.memory.SearchMemoryResponse.Builder

# Uses of Class

com.google.adk.memory.SearchMemoryResponse.Builder

-
## Uses of

[SearchMemoryResponse.Builder](../SearchMemoryResponse.Builder.html)in[com.google.adk.memory](../package-summary.html)Modifier and TypeMethodDescription`static`

[SearchMemoryResponse.Builder](../SearchMemoryResponse.Builder.html)SearchMemoryResponse.[builder](../SearchMemoryResponse.html#builder())()Creates a new builder for.`SearchMemoryResponse`

SearchMemoryResponse.Builder.[setMemories](../SearchMemoryResponse.Builder.html#setMemories(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[MemoryEntry](../MemoryEntry.html)> memories)Sets the list of memory entries using a list.


---

<!-- DOCUMENTO FUSIONADO: memoryentryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/class-use/MemoryEntry.html -->

# Uses of Classcom.google.adk.memory.MemoryEntry

# Uses of Class

com.google.adk.memory.MemoryEntry

-
## Uses of

[MemoryEntry](../MemoryEntry.html)in[com.google.adk.memory](../package-summary.html)Modifier and TypeMethodDescription`abstract`

[MemoryEntry](../MemoryEntry.html)MemoryEntry.Builder.[build](../MemoryEntry.Builder.html#build())()Builds the immutableobject.`MemoryEntry`

Modifier and TypeMethodDescription`abstract com.google.common.collect.ImmutableList`

< [MemoryEntry](../MemoryEntry.html)>SearchMemoryResponse.[memories](../SearchMemoryResponse.html#memories())()Returns a list of memory entries that relate to the search query.Modifier and TypeMethodDescriptionSearchMemoryResponse.Builder.[setMemories](../SearchMemoryResponse.Builder.html#setMemories(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[MemoryEntry](../MemoryEntry.html)> memories)Sets the list of memory entries using a list.


---

<!-- DOCUMENTO FUSIONADO: memoryentrybuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/class-use/MemoryEntry.Builder.html -->

# Uses of Classcom.google.adk.memory.MemoryEntry.Builder

# Uses of Class

com.google.adk.memory.MemoryEntry.Builder

-
## Uses of

[MemoryEntry.Builder](../MemoryEntry.Builder.html)in[com.google.adk.memory](../package-summary.html)Modifier and TypeMethodDescription`static`

[MemoryEntry.Builder](../MemoryEntry.Builder.html)MemoryEntry.[builder](../MemoryEntry.html#builder())()Returns a new builder for creating a.`MemoryEntry`

`abstract`

[MemoryEntry.Builder](../MemoryEntry.Builder.html)Sets the author of the memory.`abstract`

[MemoryEntry.Builder](../MemoryEntry.Builder.html)MemoryEntry.Builder.[setContent](../MemoryEntry.Builder.html#setContent(com.google.genai.types.Content))(com.google.genai.types.Content content) Sets the main content of the memory.`abstract`

[MemoryEntry.Builder](../MemoryEntry.Builder.html)MemoryEntry.Builder.[setTimestamp](../MemoryEntry.Builder.html#setTimestamp(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)timestamp)Sets the timestamp when the original content of this memory happened.MemoryEntry.Builder.[setTimestamp](../MemoryEntry.Builder.html#setTimestamp(java.time.Instant))( [Instant](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Instant.html)instant)A convenience method to set the timestamp from anobject, formatted as an ISO 8601 string.`Instant`

`abstract`

[MemoryEntry.Builder](../MemoryEntry.Builder.html)MemoryEntry.[toBuilder](../MemoryEntry.html#toBuilder())()Creates a new builder with a copy of this entry's values.


---

<!-- DOCUMENTO FUSIONADO: searchmemoryresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/class-use/SearchMemoryResponse.html -->

# Uses of Classcom.google.adk.memory.SearchMemoryResponse

# Uses of Class

com.google.adk.memory.SearchMemoryResponse

-
## Uses of

[SearchMemoryResponse](../SearchMemoryResponse.html)in[com.google.adk.memory](../package-summary.html)Modifier and TypeMethodDescription`abstract`

[SearchMemoryResponse](../SearchMemoryResponse.html)SearchMemoryResponse.Builder.[build](../SearchMemoryResponse.Builder.html#build())()Builds the immutableobject.`SearchMemoryResponse`

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [SearchMemoryResponse](../SearchMemoryResponse.html)>BaseMemoryService.[searchMemory](../BaseMemoryService.html#searchMemory(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)query)Searches for sessions that match the query asynchronously.`io.reactivex.rxjava3.core.Single`

< [SearchMemoryResponse](../SearchMemoryResponse.html)>InMemoryMemoryService.[searchMemory](../InMemoryMemoryService.html#searchMemory(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)query)
