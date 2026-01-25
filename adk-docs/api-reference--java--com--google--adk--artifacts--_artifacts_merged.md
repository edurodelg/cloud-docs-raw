---
merged_at: 2026-01-25T03:28:16.215385
merged_files: 10
---

# Documentos Fusionados

Este archivo contiene 10 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/package-use.html -->

# Uses of Packagecom.google.adk.artifacts

# Uses of Package

com.google.adk.artifacts

Package

Description

-
-
ClassDescriptionBase interface for artifact services.Response for listing artifacts.Builder for
.`ListArtifactsResponse`

Response for listing artifact versions.Builder for.`ListArtifactVersionsResponse`

-
-


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/package-summary.html -->

# Package com.google.adk.artifacts

package com.google.adk.artifacts

-
ClassDescriptionBase interface for artifact services.An artifact service implementation using Google Cloud Storage (GCS).An in-memory implementation of the
.`BaseArtifactService`

Response for listing artifacts.Builder for.`ListArtifactsResponse`

Response for listing artifact versions.Builder for.`ListArtifactVersionsResponse`


---

<!-- DOCUMENTO FUSIONADO: listartifactsresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/ListArtifactsResponse.html -->

# Class ListArtifactsResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.artifacts.ListArtifactsResponse

Response for listing artifacts.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary


-
## Constructor Details

-
### ListArtifactsResponse

public ListArtifactsResponse()

-
-
## Method Details

-
### filenames

-
### builder


-


---

<!-- DOCUMENTO FUSIONADO: listartifactversionsresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/ListArtifactVersionsResponse.html -->

# Class ListArtifactVersionsResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.artifacts.ListArtifactVersionsResponse

Response for listing artifact versions.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary


-
## Constructor Details

-
### ListArtifactVersionsResponse

public ListArtifactVersionsResponse()

-
-
## Method Details

-
### versions

public abstract com.google.common.collect.ImmutableList<com.google.genai.types.Part> versions() -
### builder


-


---

<!-- DOCUMENTO FUSIONADO: listartifactsresponsebuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/ListArtifactsResponse.Builder.html -->

# Class ListArtifactsResponse.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.artifacts.ListArtifactsResponse.Builder

- Enclosing class:
[ListArtifactsResponse](ListArtifactsResponse.html)

Builder for

[.](ListArtifactsResponse.html)`ListArtifactsResponse`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[ListArtifactsResponse](ListArtifactsResponse.html)[build](#build())()`abstract`

[ListArtifactsResponse.Builder](ListArtifactsResponse.Builder.html)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### filenames

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/package-tree.html -->

# Hierarchy For Package com.google.adk.artifacts

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.artifacts.
[GcsArtifactService](GcsArtifactService.html)(implements com.google.adk.artifacts.[BaseArtifactService](BaseArtifactService.html)) - com.google.adk.artifacts.
[InMemoryArtifactService](InMemoryArtifactService.html)(implements com.google.adk.artifacts.[BaseArtifactService](BaseArtifactService.html)) - com.google.adk.artifacts.
[ListArtifactsResponse](ListArtifactsResponse.html) - com.google.adk.artifacts.
[ListArtifactsResponse.Builder](ListArtifactsResponse.Builder.html) - com.google.adk.artifacts.
[ListArtifactVersionsResponse](ListArtifactVersionsResponse.html) - com.google.adk.artifacts.
[ListArtifactVersionsResponse.Builder](ListArtifactVersionsResponse.Builder.html)

- com.google.adk.artifacts.

## Interface Hierarchy

- com.google.adk.artifacts.
[BaseArtifactService](BaseArtifactService.html)


---

<!-- DOCUMENTO FUSIONADO: listartifactversionsresponsebuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/ListArtifactVersionsResponse.Builder.html -->

# Class ListArtifactVersionsResponse.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.artifacts.ListArtifactVersionsResponse.Builder

- Enclosing class:
[ListArtifactVersionsResponse](ListArtifactVersionsResponse.html)

Builder for

[.](ListArtifactVersionsResponse.html)`ListArtifactVersionsResponse`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[ListArtifactVersionsResponse](ListArtifactVersionsResponse.html)[build](#build())()`abstract`

[ListArtifactVersionsResponse.Builder](ListArtifactVersionsResponse.Builder.html)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### versions

public abstract[ListArtifactVersionsResponse.Builder](ListArtifactVersionsResponse.Builder.html)versions( [List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.Part> versions) -
### build


-


---

<!-- DOCUMENTO FUSIONADO: baseartifactservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/BaseArtifactService.html -->

# Interface BaseArtifactService

- All Known Implementing Classes:

,[GcsArtifactService](GcsArtifactService.html)[InMemoryArtifactService](InMemoryArtifactService.html)

public interface BaseArtifactService

Base interface for artifact services.

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Completable`

[deleteArtifact](#deleteArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Deletes an artifact.`io.reactivex.rxjava3.core.Single`

< [ListArtifactsResponse](ListArtifactsResponse.html)>[listArtifactKeys](#listArtifactKeys(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists all the artifact filenames within a session.`io.reactivex.rxjava3.core.Single`

<com.google.common.collect.ImmutableList< [Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)>>[listVersions](#listVersions(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Lists all the versions (as revision IDs) of an artifact.`io.reactivex.rxjava3.core.Maybe`

<com.google.genai.types.Part> [loadArtifact](#loadArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,java.util.Optional))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> version)Gets an artifact.`io.reactivex.rxjava3.core.Single`

< [Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)>[saveArtifact](#saveArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,com.google.genai.types.Part))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename, com.google.genai.types.Part artifact)Saves an artifact.

-
## Method Details

-
### saveArtifact

io.reactivex.rxjava3.core.Single<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> saveArtifact( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename, com.google.genai.types.Part artifact)Saves an artifact.- Parameters:
`appName`

- the app name`userId`

- the user ID`sessionId`

- the session ID`filename`

- the filename`artifact`

- the artifact- Returns:
- the revision ID (version) of the saved artifact.

-
### loadArtifact

io.reactivex.rxjava3.core.Maybe<com.google.genai.types.Part> loadArtifact( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> version)Gets an artifact.- Parameters:
`appName`

- the app name`userId`

- the user ID`sessionId`

- the session ID`filename`

- the filename`version`

- Optional version number. If null, loads the latest version.- Returns:
- the artifact or empty if not found

-
### listArtifactKeys

io.reactivex.rxjava3.core.Single<[ListArtifactsResponse](ListArtifactsResponse.html)> listArtifactKeys( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists all the artifact filenames within a session.- Parameters:
`appName`

- the app name`userId`

- the user ID`sessionId`

- the session ID- Returns:
- the list artifact response containing filenames

-
### deleteArtifact

-
### listVersions

io.reactivex.rxjava3.core.Single<com.google.common.collect.ImmutableList<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)>> listVersions( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Lists all the versions (as revision IDs) of an artifact.- Parameters:
`appName`

- the app name`userId`

- the user ID`sessionId`

- the session ID`filename`

- the artifact filename- Returns:
- A list of integer version numbers.


-


---

<!-- DOCUMENTO FUSIONADO: inmemoryartifactservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/InMemoryArtifactService.html -->

# Class InMemoryArtifactService

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.artifacts.InMemoryArtifactService

- All Implemented Interfaces:
[BaseArtifactService](BaseArtifactService.html)

An in-memory implementation of the

[.](BaseArtifactService.html)`BaseArtifactService`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Completable`

[deleteArtifact](#deleteArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Deletes all versions of the given artifact.`io.reactivex.rxjava3.core.Single`

< [ListArtifactsResponse](ListArtifactsResponse.html)>[listArtifactKeys](#listArtifactKeys(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists filenames of stored artifacts for the session.`io.reactivex.rxjava3.core.Single`

<com.google.common.collect.ImmutableList< [Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)>>[listVersions](#listVersions(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Lists all versions of the specified artifact.`io.reactivex.rxjava3.core.Maybe`

<com.google.genai.types.Part> [loadArtifact](#loadArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,java.util.Optional))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> version)Loads an artifact by version or latest.`io.reactivex.rxjava3.core.Single`

< [Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)>[saveArtifact](#saveArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,com.google.genai.types.Part))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename, com.google.genai.types.Part artifact)Saves an artifact in memory and assigns a new version.

-
## Constructor Details

-
### InMemoryArtifactService

public InMemoryArtifactService()

-
-
## Method Details

-
### saveArtifact

public io.reactivex.rxjava3.core.Single<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> saveArtifact( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename, com.google.genai.types.Part artifact)Saves an artifact in memory and assigns a new version.- Specified by:

in interface[saveArtifact](BaseArtifactService.html#saveArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,com.google.genai.types.Part))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- the app name`userId`

- the user ID`sessionId`

- the session ID`filename`

- the filename`artifact`

- the artifact- Returns:
- Single with assigned version number.

-
### loadArtifact

public io.reactivex.rxjava3.core.Maybe<com.google.genai.types.Part> loadArtifact( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> version)Loads an artifact by version or latest.- Specified by:

in interface[loadArtifact](BaseArtifactService.html#loadArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,java.util.Optional))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- the app name`userId`

- the user ID`sessionId`

- the session ID`filename`

- the filename`version`

- Optional version number. If null, loads the latest version.- Returns:
- Maybe with the artifact, or empty if not found.

-
### listArtifactKeys

public io.reactivex.rxjava3.core.Single<[ListArtifactsResponse](ListArtifactsResponse.html)> listArtifactKeys( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists filenames of stored artifacts for the session.- Specified by:

in interface[listArtifactKeys](BaseArtifactService.html#listArtifactKeys(java.lang.String,java.lang.String,java.lang.String))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- the app name`userId`

- the user ID`sessionId`

- the session ID- Returns:
- Single with list of artifact filenames.

-
### deleteArtifact

public io.reactivex.rxjava3.core.Completable deleteArtifact( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Deletes all versions of the given artifact.- Specified by:

in interface[deleteArtifact](BaseArtifactService.html#deleteArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- the app name`userId`

- the user ID`sessionId`

- the session ID`filename`

- the filename- Returns:
- Completable indicating completion.

-
### listVersions

public io.reactivex.rxjava3.core.Single<com.google.common.collect.ImmutableList<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)>> listVersions( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Lists all versions of the specified artifact.- Specified by:

in interface[listVersions](BaseArtifactService.html#listVersions(java.lang.String,java.lang.String,java.lang.String,java.lang.String))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- the app name`userId`

- the user ID`sessionId`

- the session ID`filename`

- the artifact filename- Returns:
- Single with list of version numbers.


-


---

<!-- DOCUMENTO FUSIONADO: gcsartifactservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/artifacts/GcsArtifactService.html -->

# Class GcsArtifactService

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.artifacts.GcsArtifactService

- All Implemented Interfaces:
[BaseArtifactService](BaseArtifactService.html)

An artifact service implementation using Google Cloud Storage (GCS).

-
## Constructor Summary

ConstructorDescription[GcsArtifactService](#%3Cinit%3E(java.lang.String,com.google.cloud.storage.Storage))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)bucketName, com.google.cloud.storage.Storage storageClient)Initializes the GcsArtifactService. -
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Completable`

[deleteArtifact](#deleteArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Deletes all versions of the specified artifact from GCS.`io.reactivex.rxjava3.core.Single`

< [ListArtifactsResponse](ListArtifactsResponse.html)>[listArtifactKeys](#listArtifactKeys(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists artifact filenames for a user and session.`io.reactivex.rxjava3.core.Single`

<com.google.common.collect.ImmutableList< [Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)>>[listVersions](#listVersions(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Lists all available versions for a given artifact.`io.reactivex.rxjava3.core.Maybe`

<com.google.genai.types.Part> [loadArtifact](#loadArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,java.util.Optional))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> version)Loads an artifact from GCS.`io.reactivex.rxjava3.core.Single`

< [Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)>[saveArtifact](#saveArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,com.google.genai.types.Part))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename, com.google.genai.types.Part artifact)Saves an artifact to GCS and assigns a new version.

-
## Constructor Details

-
### GcsArtifactService

Initializes the GcsArtifactService.- Parameters:
`bucketName`

- The name of the GCS bucket to use.`storageClient`

- The GCS storage client instance.


-
-
## Method Details

-
### saveArtifact

public io.reactivex.rxjava3.core.Single<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> saveArtifact( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename, com.google.genai.types.Part artifact)Saves an artifact to GCS and assigns a new version.- Specified by:

in interface[saveArtifact](BaseArtifactService.html#saveArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,com.google.genai.types.Part))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- Application name.`userId`

- User ID.`sessionId`

- Session ID.`filename`

- Artifact filename.`artifact`

- Artifact content to save.- Returns:
- Single with assigned version number.

-
### loadArtifact

public io.reactivex.rxjava3.core.Maybe<com.google.genai.types.Part> loadArtifact( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)> version)Loads an artifact from GCS.- Specified by:

in interface[loadArtifact](BaseArtifactService.html#loadArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String,java.util.Optional))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- Application name.`userId`

- User ID.`sessionId`

- Session ID.`filename`

- Artifact filename.`version`

- Optional version to load. Loads latest if empty.- Returns:
- Maybe with loaded artifact, or empty if not found.

-
### listArtifactKeys

public io.reactivex.rxjava3.core.Single<[ListArtifactsResponse](ListArtifactsResponse.html)> listArtifactKeys( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists artifact filenames for a user and session.- Specified by:

in interface[listArtifactKeys](BaseArtifactService.html#listArtifactKeys(java.lang.String,java.lang.String,java.lang.String))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- Application name.`userId`

- User ID.`sessionId`

- Session ID.- Returns:
- Single with sorted list of artifact filenames.

-
### deleteArtifact

public io.reactivex.rxjava3.core.Completable deleteArtifact( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Deletes all versions of the specified artifact from GCS.- Specified by:

in interface[deleteArtifact](BaseArtifactService.html#deleteArtifact(java.lang.String,java.lang.String,java.lang.String,java.lang.String))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- Application name.`userId`

- User ID.`sessionId`

- Session ID.`filename`

- Artifact filename.- Returns:
- Completable indicating operation completion.

-
### listVersions

public io.reactivex.rxjava3.core.Single<com.google.common.collect.ImmutableList<[Integer](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Integer.html)>> listVersions( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)filename)Lists all available versions for a given artifact.- Specified by:

in interface[listVersions](BaseArtifactService.html#listVersions(java.lang.String,java.lang.String,java.lang.String,java.lang.String))[BaseArtifactService](BaseArtifactService.html)- Parameters:
`appName`

- Application name.`userId`

- User ID.`sessionId`

- Session ID.`filename`

- Artifact filename.- Returns:
- Single with sorted list of version numbers.


-
