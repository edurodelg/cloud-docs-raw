---
merged_at: 2026-01-25T03:28:16.237959
merged_files: 9
---

# Documentos Fusionados

Este archivo contiene 9 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/package-use.html -->

# Uses of Packagecom.google.adk.memory

# Uses of Package

com.google.adk.memory

-
ClassDescriptionBase contract for memory services.Represents one memory entry.Builder for
.`MemoryEntry`

Represents the response from a memory search.Builder for.`SearchMemoryResponse`


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/package-summary.html -->

# Package com.google.adk.memory

package com.google.adk.memory

-
ClassDescriptionBase contract for memory services.An in-memory memory service for prototyping purposes only.Represents one memory entry.Builder for
.`MemoryEntry`

Represents the response from a memory search.Builder for.`SearchMemoryResponse`


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/package-tree.html -->

# Hierarchy For Package com.google.adk.memory

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.memory.
[InMemoryMemoryService](InMemoryMemoryService.html)(implements com.google.adk.memory.[BaseMemoryService](BaseMemoryService.html)) - com.google.adk.memory.
[MemoryEntry](MemoryEntry.html) - com.google.adk.memory.
[MemoryEntry.Builder](MemoryEntry.Builder.html) - com.google.adk.memory.
[SearchMemoryResponse](SearchMemoryResponse.html) - com.google.adk.memory.
[SearchMemoryResponse.Builder](SearchMemoryResponse.Builder.html)

- com.google.adk.memory.

## Interface Hierarchy

- com.google.adk.memory.
[BaseMemoryService](BaseMemoryService.html)


---

<!-- DOCUMENTO FUSIONADO: searchmemoryresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/SearchMemoryResponse.html -->

# Class SearchMemoryResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.memory.SearchMemoryResponse

Represents the response from a memory search.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[SearchMemoryResponse.Builder](SearchMemoryResponse.Builder.html)[builder](#builder())()Creates a new builder for.`SearchMemoryResponse`

`abstract com.google.common.collect.ImmutableList`

< [MemoryEntry](MemoryEntry.html)>[memories](#memories())()Returns a list of memory entries that relate to the search query.

-
## Constructor Details

-
### SearchMemoryResponse

public SearchMemoryResponse()

-
-
## Method Details

-
### memories

Returns a list of memory entries that relate to the search query. -
### builder

Creates a new builder for.`SearchMemoryResponse`


-


---

<!-- DOCUMENTO FUSIONADO: searchmemoryresponsebuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/SearchMemoryResponse.Builder.html -->

# Class SearchMemoryResponse.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.memory.SearchMemoryResponse.Builder

- Enclosing class:
[SearchMemoryResponse](SearchMemoryResponse.html)

Builder for

[.](SearchMemoryResponse.html)`SearchMemoryResponse`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[SearchMemoryResponse](SearchMemoryResponse.html)[build](#build())()Builds the immutableobject.`SearchMemoryResponse`

[setMemories](#setMemories(java.util.List))( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[MemoryEntry](MemoryEntry.html)> memories)Sets the list of memory entries using a list.

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### setMemories

Sets the list of memory entries using a list. -
### build

Builds the immutableobject.`SearchMemoryResponse`


-


---

<!-- DOCUMENTO FUSIONADO: memoryentryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/MemoryEntry.html -->

# Class MemoryEntry

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.memory.MemoryEntry

Represents one memory entry.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[author](#author())()Returns the author of the memory, or null if not set.`static`

[MemoryEntry.Builder](MemoryEntry.Builder.html)[builder](#builder())()Returns a new builder for creating a.`MemoryEntry`

`abstract com.google.genai.types.Content`

[content](#content())()Returns the main content of the memory.`abstract`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)Returns the timestamp when the original content of this memory happened, or null if not set.`abstract`

[MemoryEntry.Builder](MemoryEntry.Builder.html)Creates a new builder with a copy of this entry's values.

-
## Constructor Details

-
### MemoryEntry

public MemoryEntry()

-
-
## Method Details

-
### content

public abstract com.google.genai.types.Content content()Returns the main content of the memory. -
### author

Returns the author of the memory, or null if not set. -
### timestamp

Returns the timestamp when the original content of this memory happened, or null if not set.This string will be forwarded to LLM. Preferred format is ISO 8601 format

-
### builder

Returns a new builder for creating a.`MemoryEntry`

-
### toBuilder

Creates a new builder with a copy of this entry's values.- Returns:
- a new
instance.`MemoryEntry.Builder`


-


---

<!-- DOCUMENTO FUSIONADO: memoryentrybuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/MemoryEntry.Builder.html -->

# Class MemoryEntry.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.memory.MemoryEntry.Builder

- Enclosing class:
[MemoryEntry](MemoryEntry.html)

Builder for

[.](MemoryEntry.html)`MemoryEntry`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[MemoryEntry](MemoryEntry.html)[build](#build())()Builds the immutableobject.`MemoryEntry`

`abstract`

[MemoryEntry.Builder](MemoryEntry.Builder.html)Sets the author of the memory.`abstract`

[MemoryEntry.Builder](MemoryEntry.Builder.html)[setContent](#setContent(com.google.genai.types.Content))(com.google.genai.types.Content content) Sets the main content of the memory.`abstract`

[MemoryEntry.Builder](MemoryEntry.Builder.html)[setTimestamp](#setTimestamp(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)timestamp)Sets the timestamp when the original content of this memory happened.[setTimestamp](#setTimestamp(java.time.Instant))( [Instant](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Instant.html)instant)A convenience method to set the timestamp from anobject, formatted as an ISO 8601 string.`Instant`


-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### setContent

Sets the main content of the memory.This is a required field.

-
### setAuthor

Sets the author of the memory. -
### setTimestamp

Sets the timestamp when the original content of this memory happened. -
### setTimestamp

A convenience method to set the timestamp from anobject, formatted as an ISO 8601 string.`Instant`

- Parameters:
`instant`

- The timestamp as an Instant object.

-
### build

Builds the immutableobject.`MemoryEntry`


-


---

<!-- DOCUMENTO FUSIONADO: basememoryservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/BaseMemoryService.html -->

# Interface BaseMemoryService

- All Known Implementing Classes:
[InMemoryMemoryService](InMemoryMemoryService.html)

public interface BaseMemoryService

Base contract for memory services.

The service provides functionalities to ingest sessions into memory so that the memory can be used for user queries.

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Completable`

[addSessionToMemory](#addSessionToMemory(com.google.adk.sessions.Session))( [Session](../sessions/Session.html)session)Adds a session to the memory service.`io.reactivex.rxjava3.core.Single`

< [SearchMemoryResponse](SearchMemoryResponse.html)>[searchMemory](#searchMemory(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)query)Searches for sessions that match the query asynchronously.

-
## Method Details

-
### addSessionToMemory

Adds a session to the memory service.A session may be added multiple times during its lifetime.

- Parameters:
`session`

- The session to add.

-
### searchMemory

io.reactivex.rxjava3.core.Single<[SearchMemoryResponse](SearchMemoryResponse.html)> searchMemory( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)query)Searches for sessions that match the query asynchronously.- Parameters:
`appName`

- The name of the application.`userId`

- The id of the user.`query`

- The query to search for.- Returns:
- A
containing the matching memories.`SearchMemoryResponse`


-


---

<!-- DOCUMENTO FUSIONADO: inmemorymemoryservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/memory/InMemoryMemoryService.html -->

# Class InMemoryMemoryService

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.memory.InMemoryMemoryService

- All Implemented Interfaces:
[BaseMemoryService](BaseMemoryService.html)

An in-memory memory service for prototyping purposes only.

Uses keyword matching instead of semantic search.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Completable`

[addSessionToMemory](#addSessionToMemory(com.google.adk.sessions.Session))( [Session](../sessions/Session.html)session)Adds a session to the memory service.`io.reactivex.rxjava3.core.Single`

< [SearchMemoryResponse](SearchMemoryResponse.html)>[searchMemory](#searchMemory(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)query)Searches for sessions that match the query asynchronously.

-
## Constructor Details

-
### InMemoryMemoryService

public InMemoryMemoryService()

-
-
## Method Details

-
### addSessionToMemory

Description copied from interface:[BaseMemoryService](BaseMemoryService.html#addSessionToMemory(com.google.adk.sessions.Session))Adds a session to the memory service.A session may be added multiple times during its lifetime.

- Specified by:

in interface[addSessionToMemory](BaseMemoryService.html#addSessionToMemory(com.google.adk.sessions.Session))[BaseMemoryService](BaseMemoryService.html)- Parameters:
`session`

- The session to add.

-
### searchMemory

public io.reactivex.rxjava3.core.Single<[SearchMemoryResponse](SearchMemoryResponse.html)> searchMemory( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)query)Description copied from interface:[BaseMemoryService](BaseMemoryService.html#searchMemory(java.lang.String,java.lang.String,java.lang.String))Searches for sessions that match the query asynchronously.- Specified by:

in interface[searchMemory](BaseMemoryService.html#searchMemory(java.lang.String,java.lang.String,java.lang.String))[BaseMemoryService](BaseMemoryService.html)- Parameters:
`appName`

- The name of the application.`userId`

- The id of the user.`query`

- The query to search for.- Returns:
- A
containing the matching memories.`SearchMemoryResponse`


-
