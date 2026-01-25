---
merged_at: 2026-01-25T02:21:31.654645
merged_files: 21
---

# Documentos Fusionados

Este archivo contiene 21 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: getsessionconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/GetSessionConfig.html -->

# Class GetSessionConfig

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.GetSessionConfig

Configuration for getting a session.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary


-
## Constructor Details

-
### GetSessionConfig

public GetSessionConfig()

-
-
## Method Details

-
### numRecentEvents

-
### afterTimestamp

-
### builder


-


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/package-use.html -->

# Uses of Packagecom.google.adk.sessions

# Uses of Package

com.google.adk.sessions

Package

Description

-
-
-
-
ClassDescriptionThe API response contains a response to a call to the GenAI APIs.Configuration for getting a session.Builder for
.`GetSessionConfig`

Base client for the HTTP APIs.Response for listing events.Builder for.`ListEventsResponse`

Response for listing sessions.Builder for.`ListSessionsResponse`

Builder for.`Session`

Represents a general error that occurred during session management operations.Aobject that also keeps track of the changes to the state.`State`

-


---

<!-- DOCUMENTO FUSIONADO: listeventsresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/ListEventsResponse.html -->

# Class ListEventsResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.ListEventsResponse

Response for listing events.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[ListEventsResponse.Builder](ListEventsResponse.Builder.html)[builder](#builder())()`abstract com.google.common.collect.ImmutableList`

< [Event](../events/Event.html)>[events](#events())()

-
## Constructor Details

-
### ListEventsResponse

public ListEventsResponse()

-
-
## Method Details

-
### events

-
### nextPageToken

-
### builder


-


---

<!-- DOCUMENTO FUSIONADO: listsessionsresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/ListSessionsResponse.html -->

# Class ListSessionsResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.ListSessionsResponse

Response for listing sessions.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[ListSessionsResponse.Builder](ListSessionsResponse.Builder.html)[builder](#builder())()`abstract com.google.common.collect.ImmutableList`

< [Session](Session.html)>[sessions](#sessions())()

-
## Constructor Details

-
### ListSessionsResponse

public ListSessionsResponse()

-
-
## Method Details

-
### sessions

-
### sessionIds

-
### builder


-


---

<!-- DOCUMENTO FUSIONADO: listsessionsresponsebuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/ListSessionsResponse.Builder.html -->

# Class ListSessionsResponse.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.ListSessionsResponse.Builder

- Enclosing class:
[ListSessionsResponse](ListSessionsResponse.html)

Builder for

[.](ListSessionsResponse.html)`ListSessionsResponse`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[ListSessionsResponse](ListSessionsResponse.html)[build](#build())()`abstract`

[ListSessionsResponse.Builder](ListSessionsResponse.Builder.html)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### sessions

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: listeventsresponsebuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/ListEventsResponse.Builder.html -->

# Class ListEventsResponse.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.ListEventsResponse.Builder

- Enclosing class:
[ListEventsResponse](ListEventsResponse.html)

Builder for

[.](ListEventsResponse.html)`ListEventsResponse`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[ListEventsResponse](ListEventsResponse.html)[build](#build())()`abstract`

[ListEventsResponse.Builder](ListEventsResponse.Builder.html)`abstract`

[ListEventsResponse.Builder](ListEventsResponse.Builder.html)[nextPageToken](#nextPageToken(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)nextPageToken)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### events

-
### nextPageToken

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/package-summary.html -->

# Package com.google.adk.sessions

package com.google.adk.sessions

-
ClassDescriptionThe API response contains a response to a call to the GenAI APIs.Configuration for getting a session.Builder for
.`GetSessionConfig`

Base client for the HTTP APIs.Wraps a real HTTP response to expose the methods needed by the GenAI SDK.An in-memory implementation ofassuming`BaseSessionService`

objects are mutable regarding their state map, events list, and last update time.`Session`

Response for listing events.Builder for.`ListEventsResponse`

Response for listing sessions.Builder for.`ListSessionsResponse`

Builder for.`Session`

Represents a general error that occurred during session management operations.Indicates that a requested session could not be found.Utility functions for session service.Aobject that also keeps track of the changes to the state.`State`

TODO: Use the genai HttpApiClient and ApiResponse methods once they are public.


---

<!-- DOCUMENTO FUSIONADO: getsessionconfigbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/GetSessionConfig.Builder.html -->

# Class GetSessionConfig.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.GetSessionConfig.Builder

- Enclosing class:
[GetSessionConfig](GetSessionConfig.html)

Builder for

[.](GetSessionConfig.html)`GetSessionConfig`

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[GetSessionConfig.Builder](GetSessionConfig.Builder.html)[afterTimestamp](#afterTimestamp(java.time.Instant))( [Instant](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Instant.html)afterTimestamp)`abstract`

[GetSessionConfig](GetSessionConfig.html)[build](#build())()`abstract`

[GetSessionConfig.Builder](GetSessionConfig.Builder.html)[numRecentEvents](#numRecentEvents(int))(int numRecentEvents)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### numRecentEvents

-
### afterTimestamp

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: apiresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/ApiResponse.html -->

# Class ApiResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.ApiResponse

- All Implemented Interfaces:
[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

- Direct Known Subclasses:
[HttpApiResponse](HttpApiResponse.html)

The API response contains a response to a call to the GenAI APIs.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract void`

[close](#close())()`abstract okhttp3.ResponseBody`

Gets the HttpEntity.

-
## Constructor Details

-
### ApiResponse

public ApiResponse()

-
-
## Method Details

-
### getResponseBody

public abstract okhttp3.ResponseBody getResponseBody()Gets the HttpEntity. -
### close

public abstract void close()- Specified by:

in interface[close](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html#close())[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)


-


---

<!-- DOCUMENTO FUSIONADO: sessionutilshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/SessionUtils.html -->

# Class SessionUtils

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.SessionUtils

Utility functions for session service.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static com.google.genai.types.Content`

[decodeContent](#decodeContent(com.google.genai.types.Content))(com.google.genai.types.Content content) Decodes Base64-encoded inline blobs in content.`static com.google.genai.types.Content`

[encodeContent](#encodeContent(com.google.genai.types.Content))(com.google.genai.types.Content content) Base64-encodes inline blobs in content.

-
## Constructor Details

-
### SessionUtils

public SessionUtils()

-
-
## Method Details

-
### encodeContent

public static com.google.genai.types.Content encodeContent(com.google.genai.types.Content content) Base64-encodes inline blobs in content. -
### decodeContent

public static com.google.genai.types.Content decodeContent(com.google.genai.types.Content content) Decodes Base64-encoded inline blobs in content.

-


---

<!-- DOCUMENTO FUSIONADO: sessionbuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/Session.Builder.html -->

# Class Session.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.Session.Builder

- Enclosing class:
[Session](Session.html)

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription[build](#build())()[lastUpdateTime](#lastUpdateTime(java.time.Instant))( [Instant](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Instant.html)lastUpdateTime)[lastUpdateTimeSeconds](#lastUpdateTimeSeconds(double))(double seconds) [state](#state(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state)

-
## Constructor Details

-
### Builder


-
-
## Method Details

-
### id

-
### state

-
### state

-
### appName

-
### userId

-
### events

-
### lastUpdateTime

-
### lastUpdateTimeSeconds

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: sessionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/Session.html -->

# Class Session

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.JsonBaseModel](../JsonBaseModel.html)

com.google.adk.sessions.Session

-
## Nested Class Summary

-
## Method Summary

Modifier and TypeMethodDescription[appName](#appName())()`static`

[Session.Builder](Session.Builder.html)[events](#events())()`static`

[Session](Session.html)`double`

[id](#id())()`void`

[lastUpdateTime](#lastUpdateTime(java.time.Instant))( [Instant](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Instant.html)lastUpdateTime)[state](#state())()[toString](#toString())()[userId](#userId())()### Methods inherited from class com.google.adk.

[JsonBaseModel](../JsonBaseModel.html)[fromJsonNode](../JsonBaseModel.html#fromJsonNode(com.fasterxml.jackson.databind.JsonNode,java.lang.Class)),[fromJsonString](../JsonBaseModel.html#fromJsonString(java.lang.String,java.lang.Class)),[getMapper](../JsonBaseModel.html#getMapper()),[toJson](../JsonBaseModel.html#toJson()),[toJsonNode](../JsonBaseModel.html#toJsonNode(java.lang.Object)),[toJsonString](../JsonBaseModel.html#toJsonString(java.lang.Object))

-
## Method Details

-
### builder

-
### id

-
### state

-
### events

-
### appName

-
### userId

-
### lastUpdateTime

-
### lastUpdateTime

-
### getLastUpdateTimeAsDouble

public double getLastUpdateTimeAsDouble() -
### toString

-
### fromJson


-


---

<!-- DOCUMENTO FUSIONADO: httpapiclienthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/HttpApiClient.html -->

# Class HttpApiClient

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.HttpApiClient

Base client for the HTTP APIs.

-
## Field Summary

-
## Method Summary

Modifier and TypeMethodDescription`@Nullable`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[apiKey](#apiKey())()Returns the API key for Google AI APIs.`@Nullable`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[location](#location())()Returns the location for Vertex AI APIs.`@Nullable`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[project](#project())()Returns the project ID for Vertex AI APIs.Sends a Http request given the http method, path, and request json string.`boolean`

[vertexAI](#vertexAI())()Returns whether the client is using Vertex AI APIs.

-
## Field Details

-
### MEDIA_TYPE_APPLICATION_JSON

public static final okhttp3.MediaType MEDIA_TYPE_APPLICATION_JSON

-
-
## Method Details

-
### request

Sends a Http request given the http method, path, and request json string. -
### vertexAI

public boolean vertexAI()Returns whether the client is using Vertex AI APIs. -
### project

Returns the project ID for Vertex AI APIs. -
### location

Returns the location for Vertex AI APIs. -
### apiKey

Returns the API key for Google AI APIs.

-


---

<!-- DOCUMENTO FUSIONADO: httpapiresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/HttpApiResponse.html -->

# Class HttpApiResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.sessions.ApiResponse](ApiResponse.html)

com.google.adk.sessions.HttpApiResponse

- All Implemented Interfaces:
[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

Wraps a real HTTP response to expose the methods needed by the GenAI SDK.

-
## Constructor Summary

ConstructorDescription[HttpApiResponse](#%3Cinit%3E(okhttp3.Response))(okhttp3.Response response) Constructs a HttpApiResponse instance with the response. -
## Method Summary

Modifier and TypeMethodDescription`void`

[close](#close())()Closes the Http response.`okhttp3.ResponseBody`

Returns the HttpEntity from the response.

-
## Constructor Details

-
### HttpApiResponse

public HttpApiResponse(okhttp3.Response response) Constructs a HttpApiResponse instance with the response.

-
-
## Method Details

-
### getResponseBody

public okhttp3.ResponseBody getResponseBody()Returns the HttpEntity from the response.- Specified by:

in class[getResponseBody](ApiResponse.html#getResponseBody())[ApiResponse](ApiResponse.html)

-
### close

public void close()Closes the Http response.- Specified by:

in interface[close](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html#close())[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)- Specified by:

in class[close](ApiResponse.html#close())[ApiResponse](ApiResponse.html)


-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/package-tree.html -->

# Hierarchy For Package com.google.adk.sessions

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.sessions.
[ApiResponse](ApiResponse.html)(implements java.lang.[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html))- com.google.adk.sessions.
[HttpApiResponse](HttpApiResponse.html)

- com.google.adk.sessions.
- com.google.adk.sessions.
[GetSessionConfig](GetSessionConfig.html) - com.google.adk.sessions.
[GetSessionConfig.Builder](GetSessionConfig.Builder.html) - com.google.adk.sessions.
[HttpApiClient](HttpApiClient.html) - com.google.adk.sessions.
[InMemorySessionService](InMemorySessionService.html)(implements com.google.adk.sessions.[BaseSessionService](BaseSessionService.html)) - com.google.adk.
[JsonBaseModel](../JsonBaseModel.html)- com.google.adk.sessions.
[Session](Session.html)

- com.google.adk.sessions.
- com.google.adk.sessions.
[ListEventsResponse](ListEventsResponse.html) - com.google.adk.sessions.
[ListEventsResponse.Builder](ListEventsResponse.Builder.html) - com.google.adk.sessions.
[ListSessionsResponse](ListSessionsResponse.html) - com.google.adk.sessions.
[ListSessionsResponse.Builder](ListSessionsResponse.Builder.html) - com.google.adk.sessions.
[Session.Builder](Session.Builder.html) - com.google.adk.sessions.
[SessionUtils](SessionUtils.html) - com.google.adk.sessions.
[State](State.html)(implements java.util.concurrent.[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<K,V>) - java.lang.
[Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)(implements java.io.[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html))- java.lang.
[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)- java.lang.
[RuntimeException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/RuntimeException.html)- com.google.adk.sessions.
[SessionException](SessionException.html)- com.google.adk.sessions.
[SessionNotFoundException](SessionNotFoundException.html)

- com.google.adk.sessions.

- com.google.adk.sessions.

- java.lang.

- java.lang.
- com.google.adk.sessions.
[VertexAiSessionService](VertexAiSessionService.html)(implements com.google.adk.sessions.[BaseSessionService](BaseSessionService.html))

- com.google.adk.sessions.

## Interface Hierarchy

- com.google.adk.sessions.
[BaseSessionService](BaseSessionService.html)


---

<!-- DOCUMENTO FUSIONADO: sessionnotfoundexceptionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/SessionNotFoundException.html -->

# Class SessionNotFoundException

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[java.lang.Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)

[java.lang.Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)

[java.lang.RuntimeException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/RuntimeException.html)

[com.google.adk.sessions.SessionException](SessionException.html)

com.google.adk.sessions.SessionNotFoundException

- All Implemented Interfaces:
[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html)

Indicates that a requested session could not be found.

- See Also:

-
## Constructor Summary

ConstructorDescription[SessionNotFoundException](#%3Cinit%3E(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)message)[SessionNotFoundException](#%3Cinit%3E(java.lang.String,java.lang.Throwable))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)message,[Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)cause) -
## Method Summary

### Methods inherited from class java.lang.

[Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)[addSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#addSuppressed(java.lang.Throwable)),[fillInStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#fillInStackTrace()),[getCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getCause()),[getLocalizedMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getLocalizedMessage()),[getMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getMessage()),[getStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getStackTrace()),[getSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getSuppressed()),[initCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#initCause(java.lang.Throwable)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace()),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintStream)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintWriter)),[setStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#setStackTrace(java.lang.StackTraceElement%5B%5D)),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#toString())

-
## Constructor Details

-
### SessionNotFoundException

-
### SessionNotFoundException


-


---

<!-- DOCUMENTO FUSIONADO: sessionexceptionhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/SessionException.html -->

# Class SessionException

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[java.lang.Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)

[java.lang.Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)

[java.lang.RuntimeException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/RuntimeException.html)

com.google.adk.sessions.SessionException

- All Implemented Interfaces:
[Serializable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/Serializable.html)

- Direct Known Subclasses:
[SessionNotFoundException](SessionNotFoundException.html)

Represents a general error that occurred during session management operations.

- See Also:

-
## Constructor Summary

ConstructorDescription[SessionException](#%3Cinit%3E(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)message)[SessionException](#%3Cinit%3E(java.lang.String,java.lang.Throwable))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)message,[Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)cause)[SessionException](#%3Cinit%3E(java.lang.Throwable))( [Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)cause) -
## Method Summary

### Methods inherited from class java.lang.

[Throwable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html)[addSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#addSuppressed(java.lang.Throwable)),[fillInStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#fillInStackTrace()),[getCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getCause()),[getLocalizedMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getLocalizedMessage()),[getMessage](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getMessage()),[getStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getStackTrace()),[getSuppressed](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#getSuppressed()),[initCause](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#initCause(java.lang.Throwable)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace()),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintStream)),[printStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#printStackTrace(java.io.PrintWriter)),[setStackTrace](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#setStackTrace(java.lang.StackTraceElement%5B%5D)),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Throwable.html#toString())

-
## Constructor Details

-
### SessionException

-
### SessionException

-
### SessionException


-


---

<!-- DOCUMENTO FUSIONADO: statehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/State.html -->

# Class State

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.State

A

[object that also keeps track of the changes to the state.](State.html)`State`

-
## Nested Class Summary

-
## Field Summary

-
## Constructor Summary

ConstructorDescription[State](#%3Cinit%3E(java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state)[State](#%3Cinit%3E(java.util.concurrent.ConcurrentMap,java.util.concurrent.ConcurrentMap))( [ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state,[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> delta) -
## Method Summary

Modifier and TypeMethodDescription`void`

[clear](#clear())()`boolean`

[containsKey](#containsKey(java.lang.Object))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)key)`boolean`

[containsValue](#containsValue(java.lang.Object))( [Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)value)[entrySet](#entrySet())()`boolean`

`boolean`

[hasDelta](#hasDelta())()`int`

[hashCode](#hashCode())()`boolean`

[isEmpty](#isEmpty())()[keySet](#keySet())()`void`

[putIfAbsent](#putIfAbsent(java.lang.String,java.lang.Object))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)key,[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)value)`boolean`

`boolean`

`int`

[size](#size())()[values](#values())()### Methods inherited from class java.lang.

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)[clone](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#clone()),[finalize](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#finalize()),[getClass](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#getClass()),[notify](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notify()),[notifyAll](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notifyAll()),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#toString()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long)),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long,int))### Methods inherited from interface java.util.concurrent.

[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)[compute](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html#compute(K,java.util.function.BiFunction)),[computeIfAbsent](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html#computeIfAbsent(K,java.util.function.Function)),[computeIfPresent](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html#computeIfPresent(K,java.util.function.BiFunction)),[forEach](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html#forEach(java.util.function.BiConsumer)),[getOrDefault](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html#getOrDefault(java.lang.Object,V)),[merge](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html#merge(K,V,java.util.function.BiFunction)),[replaceAll](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html#replaceAll(java.util.function.BiFunction))

-
## Field Details

-
### APP_PREFIX

- See Also:

-
### USER_PREFIX

- See Also:

-
### TEMP_PREFIX

- See Also:


-
-
## Constructor Details

-
### State

-
### State


-
-
## Method Details

-
### clear

-
### containsKey

- Specified by:

in interface[containsKey](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html#containsKey(java.lang.Object))[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>

-
### containsValue

- Specified by:

in interface[containsValue](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html#containsValue(java.lang.Object))[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>

-
### entrySet

-
### equals

-
### get

-
### hashCode

-
### isEmpty

-
### keySet

-
### put

-
### putIfAbsent

- Specified by:

in interface[putIfAbsent](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html#putIfAbsent(K,V))[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>- Specified by:

in interface[putIfAbsent](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html#putIfAbsent(K,V))[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)>

-
### putAll

-
### remove

-
### remove

-
### replace

-
### replace

-
### size

-
### values

-
### hasDelta

public boolean hasDelta()

-


---

<!-- DOCUMENTO FUSIONADO: basesessionservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/BaseSessionService.html -->

# Interface BaseSessionService

- All Known Implementing Classes:

,[InMemorySessionService](InMemorySessionService.html)[VertexAiSessionService](VertexAiSessionService.html)

-
## Method Summary

Modifier and TypeMethodDescription`default io.reactivex.rxjava3.core.Single`

< [Event](../events/Event.html)>[appendEvent](#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))( [Session](Session.html)session,[Event](../events/Event.html)event)Appends an event to an in-memory session object and updates the session's state based on the event's state delta, if applicable.`default io.reactivex.rxjava3.core.Completable`

[closeSession](#closeSession(com.google.adk.sessions.Session))( [Session](Session.html)session)Closes a session.`default io.reactivex.rxjava3.core.Single`

< [Session](Session.html)>[createSession](#createSession(java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId)Creates a new session with the specified application name and user ID, using a default state (null) and allowing the service to generate a unique session ID.`io.reactivex.rxjava3.core.Single`

< [Session](Session.html)>[createSession](#createSession(java.lang.String,java.lang.String,java.util.concurrent.ConcurrentMap,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Creates a new session with the specified parameters.`io.reactivex.rxjava3.core.Completable`

[deleteSession](#deleteSession(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Deletes a specific session.`io.reactivex.rxjava3.core.Maybe`

< [Session](Session.html)>[getSession](#getSession(java.lang.String,java.lang.String,java.lang.String,java.util.Optional))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[GetSessionConfig](GetSessionConfig.html)> config)Retrieves a specific session, optionally filtering the events included.`io.reactivex.rxjava3.core.Single`

< [ListEventsResponse](ListEventsResponse.html)>[listEvents](#listEvents(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists the events within a specific session.`io.reactivex.rxjava3.core.Single`

< [ListSessionsResponse](ListSessionsResponse.html)>[listSessions](#listSessions(java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId)Lists sessions associated with a specific application and user.

-
## Method Details

-
### createSession

io.reactivex.rxjava3.core.Single<[Session](Session.html)> createSession( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @Nullable[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state, @Nullable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Creates a new session with the specified parameters.- Parameters:
`appName`

- The name of the application associated with the session.`userId`

- The identifier for the user associated with the session.`state`

- An optional map representing the initial state of the session. Can be null or empty.`sessionId`

- An optional client-provided identifier for the session. If empty or null, the service should generate a unique ID.- Returns:
- The newly created
instance.`Session`

- Throws:

- if creation fails.[SessionException](SessionException.html)

-
### createSession

Creates a new session with the specified application name and user ID, using a default state (null) and allowing the service to generate a unique session ID.This is a shortcut for

with null state and a null session ID.`createSession(String, String, Map, String)`

- Parameters:
`appName`

- The name of the application associated with the session.`userId`

- The identifier for the user associated with the session.- Returns:
- The newly created
instance.`Session`

- Throws:

- if creation fails.[SessionException](SessionException.html)

-
### getSession

io.reactivex.rxjava3.core.Maybe<[Session](Session.html)> getSession( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[GetSessionConfig](GetSessionConfig.html)> config)Retrieves a specific session, optionally filtering the events included.- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user.`sessionId`

- The unique identifier of the session to retrieve.`config`

- Optional configuration to filter the events returned within the session (e.g., limit number of recent events, filter by timestamp). If empty, default retrieval behavior is used (potentially all events or a service-defined limit).- Returns:
- An
containing the`Optional`

if found, otherwise`Session`

.`Optional.empty()`

- Throws:

- for retrieval errors other than not found.[SessionException](SessionException.html)

-
### listSessions

Lists sessions associated with a specific application and user.The

objects in the response typically contain only metadata (like ID, creation time) and not the full event list or state to optimize performance.`Session`

- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user whose sessions are to be listed.- Returns:
- A
containing a list of matching sessions.`ListSessionsResponse`

- Throws:

- if listing fails.[SessionException](SessionException.html)

-
### deleteSession

io.reactivex.rxjava3.core.Completable deleteSession( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Deletes a specific session.- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user.`sessionId`

- The unique identifier of the session to delete.- Throws:

- if the session doesn't exist.[SessionNotFoundException](SessionNotFoundException.html)

- for other deletion errors.[SessionException](SessionException.html)

-
### listEvents

io.reactivex.rxjava3.core.Single<[ListEventsResponse](ListEventsResponse.html)> listEvents( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists the events within a specific session. Supports pagination via the response object.- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user.`sessionId`

- The unique identifier of the session whose events are to be listed.- Returns:
- A
containing a list of events and an optional token for retrieving the next page.`ListEventsResponse`

- Throws:

- if the session doesn't exist.[SessionNotFoundException](SessionNotFoundException.html)

- for other listing errors.[SessionException](SessionException.html)

-
### closeSession

Closes a session. This is currently a placeholder and may involve finalizing session state or performing cleanup actions in future implementations. The default implementation does nothing.- Parameters:
`session`

- The session object to close.

-
### appendEvent

@CanIgnoreReturnValue default io.reactivex.rxjava3.core.Single<[Event](../events/Event.html)> appendEvent( [Session](Session.html)session,[Event](../events/Event.html)event)Appends an event to an in-memory session object and updates the session's state based on the event's state delta, if applicable.This method primarily modifies the passed

`session`

object in memory. Persisting these changes typically requires a separate call to an update/save method provided by the specific service implementation, or might happen implicitly depending on the implementation's design.If the event is marked as partial (e.g.,

`event.isPartial() == true`

), it is returned directly without modifying the session state or event list. State delta keys starting withare ignored during state updates.`State.TEMP_PREFIX`

- Parameters:
`session`

- Theobject to which the event should be appended (will be mutated).`Session`

`event`

- Theto append.`Event`

- Returns:
- The appended
instance (or the original event if it was partial).`Event`

- Throws:

- if session or event is null.[NullPointerException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/NullPointerException.html)


-


---

<!-- DOCUMENTO FUSIONADO: inmemorysessionservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/InMemorySessionService.html -->

# Class InMemorySessionService

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

- All Implemented Interfaces:
[BaseSessionService](BaseSessionService.html)

[assuming](BaseSessionService.html)

`BaseSessionService`

[objects are mutable regarding their state map, events list, and last update time.](Session.html)

`Session`

This implementation stores sessions, user state, and app state directly in memory using concurrent maps for basic thread safety. It is suitable for testing or single-node deployments where persistence is not required.

Note: State merging (app/user state prefixed with `_app_`

/ `_user_`

) occurs
during retrieval operations (`getSession`

, `createSession`

).

-
## Constructor Summary

ConstructorDescriptionCreates a new instance of the in-memory session service with empty storage. -
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [Event](../events/Event.html)>[appendEvent](#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))( [Session](Session.html)session,[Event](../events/Event.html)event)Appends an event to an in-memory session object and updates the session's state based on the event's state delta, if applicable.`io.reactivex.rxjava3.core.Single`

< [Session](Session.html)>[createSession](#createSession(java.lang.String,java.lang.String,java.util.concurrent.ConcurrentMap,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @Nullable[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state, @Nullable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Creates a new session with the specified parameters.`io.reactivex.rxjava3.core.Completable`

[deleteSession](#deleteSession(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Deletes a specific session.`io.reactivex.rxjava3.core.Maybe`

< [Session](Session.html)>[getSession](#getSession(java.lang.String,java.lang.String,java.lang.String,java.util.Optional))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[GetSessionConfig](GetSessionConfig.html)> configOpt)Retrieves a specific session, optionally filtering the events included.`io.reactivex.rxjava3.core.Single`

< [ListEventsResponse](ListEventsResponse.html)>[listEvents](#listEvents(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists the events within a specific session.`io.reactivex.rxjava3.core.Single`

< [ListSessionsResponse](ListSessionsResponse.html)>[listSessions](#listSessions(java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId)Lists sessions associated with a specific application and user.### Methods inherited from class java.lang.

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)[clone](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#clone()),[equals](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#equals(java.lang.Object)),[finalize](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#finalize()),[getClass](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#getClass()),[hashCode](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#hashCode()),[notify](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notify()),[notifyAll](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notifyAll()),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#toString()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long)),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long,int))### Methods inherited from interface com.google.adk.sessions.

[BaseSessionService](BaseSessionService.html)[closeSession](BaseSessionService.html#closeSession(com.google.adk.sessions.Session)),[createSession](BaseSessionService.html#createSession(java.lang.String,java.lang.String))

-
## Constructor Details

-
### InMemorySessionService

public InMemorySessionService()Creates a new instance of the in-memory session service with empty storage.

-
-
## Method Details

-
### createSession

public io.reactivex.rxjava3.core.Single<[Session](Session.html)> createSession( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @Nullable[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state, @Nullable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Description copied from interface:[BaseSessionService](BaseSessionService.html#createSession(java.lang.String,java.lang.String,java.util.concurrent.ConcurrentMap,java.lang.String))Creates a new session with the specified parameters.- Specified by:

in interface[createSession](BaseSessionService.html#createSession(java.lang.String,java.lang.String,java.util.concurrent.ConcurrentMap,java.lang.String))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application associated with the session.`userId`

- The identifier for the user associated with the session.`state`

- An optional map representing the initial state of the session. Can be null or empty.`sessionId`

- An optional client-provided identifier for the session. If empty or null, the service should generate a unique ID.- Returns:
- The newly created
instance.`Session`


-
### getSession

public io.reactivex.rxjava3.core.Maybe<[Session](Session.html)> getSession( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[GetSessionConfig](GetSessionConfig.html)> configOpt)Description copied from interface:[BaseSessionService](BaseSessionService.html#getSession(java.lang.String,java.lang.String,java.lang.String,java.util.Optional))Retrieves a specific session, optionally filtering the events included.- Specified by:

in interface[getSession](BaseSessionService.html#getSession(java.lang.String,java.lang.String,java.lang.String,java.util.Optional))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user.`sessionId`

- The unique identifier of the session to retrieve.`configOpt`

- Optional configuration to filter the events returned within the session (e.g., limit number of recent events, filter by timestamp). If empty, default retrieval behavior is used (potentially all events or a service-defined limit).- Returns:
- An
containing the`Optional`

if found, otherwise`Session`

.`Optional.empty()`


-
### listSessions

public io.reactivex.rxjava3.core.Single<[ListSessionsResponse](ListSessionsResponse.html)> listSessions( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId)Description copied from interface:[BaseSessionService](BaseSessionService.html#listSessions(java.lang.String,java.lang.String))Lists sessions associated with a specific application and user.The

objects in the response typically contain only metadata (like ID, creation time) and not the full event list or state to optimize performance.`Session`

- Specified by:

in interface[listSessions](BaseSessionService.html#listSessions(java.lang.String,java.lang.String))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user whose sessions are to be listed.- Returns:
- A
containing a list of matching sessions.`ListSessionsResponse`


-
### deleteSession

public io.reactivex.rxjava3.core.Completable deleteSession( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Description copied from interface:[BaseSessionService](BaseSessionService.html#deleteSession(java.lang.String,java.lang.String,java.lang.String))Deletes a specific session.- Specified by:

in interface[deleteSession](BaseSessionService.html#deleteSession(java.lang.String,java.lang.String,java.lang.String))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user.`sessionId`

- The unique identifier of the session to delete.

-
### listEvents

public io.reactivex.rxjava3.core.Single<[ListEventsResponse](ListEventsResponse.html)> listEvents( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Description copied from interface:[BaseSessionService](BaseSessionService.html#listEvents(java.lang.String,java.lang.String,java.lang.String))Lists the events within a specific session. Supports pagination via the response object.- Specified by:

in interface[listEvents](BaseSessionService.html#listEvents(java.lang.String,java.lang.String,java.lang.String))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user.`sessionId`

- The unique identifier of the session whose events are to be listed.- Returns:
- A
containing a list of events and an optional token for retrieving the next page.`ListEventsResponse`


-
### appendEvent

@CanIgnoreReturnValue public io.reactivex.rxjava3.core.Single<[Event](../events/Event.html)> appendEvent( [Session](Session.html)session,[Event](../events/Event.html)event)Description copied from interface:[BaseSessionService](BaseSessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))Appends an event to an in-memory session object and updates the session's state based on the event's state delta, if applicable.This method primarily modifies the passed

`session`

object in memory. Persisting these changes typically requires a separate call to an update/save method provided by the specific service implementation, or might happen implicitly depending on the implementation's design.If the event is marked as partial (e.g.,

`event.isPartial() == true`

), it is returned directly without modifying the session state or event list. State delta keys starting withare ignored during state updates.`State.TEMP_PREFIX`

- Specified by:

in interface[appendEvent](BaseSessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))[BaseSessionService](BaseSessionService.html)- Parameters:
`session`

- Theobject to which the event should be appended (will be mutated).`Session`

`event`

- Theto append.`Event`

- Returns:
- The appended
instance (or the original event if it was partial).`Event`


-


---

<!-- DOCUMENTO FUSIONADO: vertexaisessionservicehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/sessions/VertexAiSessionService.html -->

# Class VertexAiSessionService

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.sessions.VertexAiSessionService

- All Implemented Interfaces:
[BaseSessionService](BaseSessionService.html)

TODO: Use the genai HttpApiClient and ApiResponse methods once they are public.

-
## Constructor Summary

ConstructorDescriptionCreates a session service with default configuration.[VertexAiSessionService](#%3Cinit%3E(java.lang.String,java.lang.String,com.google.adk.sessions.HttpApiClient))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)project,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)location,[HttpApiClient](HttpApiClient.html)apiClient)Creates a new instance of the Vertex AI Session Service with a custom ApiClient for testing.[VertexAiSessionService](#%3Cinit%3E(java.lang.String,java.lang.String,java.util.Optional,java.util.Optional))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)project,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)location,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.auth.oauth2.GoogleCredentials> credentials,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<com.google.genai.types.HttpOptions> httpOptions)Creates a session service with specified project, location, credentials, and HTTP options. -
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Single`

< [Event](../events/Event.html)>[appendEvent](#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))( [Session](Session.html)session,[Event](../events/Event.html)event)Appends an event to an in-memory session object and updates the session's state based on the event's state delta, if applicable.`io.reactivex.rxjava3.core.Single`

< [Session](Session.html)>[createSession](#createSession(java.lang.String,java.lang.String,java.util.concurrent.ConcurrentMap,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Creates a new session with the specified parameters.`io.reactivex.rxjava3.core.Completable`

[deleteSession](#deleteSession(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Deletes a specific session.`io.reactivex.rxjava3.core.Maybe`

< [Session](Session.html)>[getSession](#getSession(java.lang.String,java.lang.String,java.lang.String,java.util.Optional))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[GetSessionConfig](GetSessionConfig.html)> config)Retrieves a specific session, optionally filtering the events included.`io.reactivex.rxjava3.core.Single`

< [ListEventsResponse](ListEventsResponse.html)>[listEvents](#listEvents(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Lists the events within a specific session.`io.reactivex.rxjava3.core.Single`

< [ListSessionsResponse](ListSessionsResponse.html)>[listSessions](#listSessions(java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId)Lists sessions associated with a specific application and user.### Methods inherited from class java.lang.

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)[clone](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#clone()),[equals](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#equals(java.lang.Object)),[finalize](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#finalize()),[getClass](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#getClass()),[hashCode](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#hashCode()),[notify](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notify()),[notifyAll](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notifyAll()),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#toString()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long)),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long,int))### Methods inherited from interface com.google.adk.sessions.

[BaseSessionService](BaseSessionService.html)[closeSession](BaseSessionService.html#closeSession(com.google.adk.sessions.Session)),[createSession](BaseSessionService.html#createSession(java.lang.String,java.lang.String))

-
## Constructor Details

-
### VertexAiSessionService

Creates a new instance of the Vertex AI Session Service with a custom ApiClient for testing. -
### VertexAiSessionService

public VertexAiSessionService()Creates a session service with default configuration. -
### VertexAiSessionService


-
-
## Method Details

-
### createSession

public io.reactivex.rxjava3.core.Single<[Session](Session.html)> createSession( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId, @Nullable[ConcurrentMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentMap.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> state, @Nullable[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Description copied from interface:[BaseSessionService](BaseSessionService.html#createSession(java.lang.String,java.lang.String,java.util.concurrent.ConcurrentMap,java.lang.String))Creates a new session with the specified parameters.- Specified by:

in interface[createSession](BaseSessionService.html#createSession(java.lang.String,java.lang.String,java.util.concurrent.ConcurrentMap,java.lang.String))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application associated with the session.`userId`

- The identifier for the user associated with the session.`state`

- An optional map representing the initial state of the session. Can be null or empty.`sessionId`

- An optional client-provided identifier for the session. If empty or null, the service should generate a unique ID.- Returns:
- The newly created
instance.`Session`


-
### listSessions

public io.reactivex.rxjava3.core.Single<[ListSessionsResponse](ListSessionsResponse.html)> listSessions( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId)Description copied from interface:[BaseSessionService](BaseSessionService.html#listSessions(java.lang.String,java.lang.String))Lists sessions associated with a specific application and user.The

objects in the response typically contain only metadata (like ID, creation time) and not the full event list or state to optimize performance.`Session`

- Specified by:

in interface[listSessions](BaseSessionService.html#listSessions(java.lang.String,java.lang.String))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user whose sessions are to be listed.- Returns:
- A
containing a list of matching sessions.`ListSessionsResponse`


-
### listEvents

public io.reactivex.rxjava3.core.Single<[ListEventsResponse](ListEventsResponse.html)> listEvents( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Description copied from interface:[BaseSessionService](BaseSessionService.html#listEvents(java.lang.String,java.lang.String,java.lang.String))Lists the events within a specific session. Supports pagination via the response object.- Specified by:

in interface[listEvents](BaseSessionService.html#listEvents(java.lang.String,java.lang.String,java.lang.String))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user.`sessionId`

- The unique identifier of the session whose events are to be listed.- Returns:
- A
containing a list of events and an optional token for retrieving the next page.`ListEventsResponse`


-
### getSession

public io.reactivex.rxjava3.core.Maybe<[Session](Session.html)> getSession( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[Optional](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)<[GetSessionConfig](GetSessionConfig.html)> config)Description copied from interface:[BaseSessionService](BaseSessionService.html#getSession(java.lang.String,java.lang.String,java.lang.String,java.util.Optional))Retrieves a specific session, optionally filtering the events included.- Specified by:

in interface[getSession](BaseSessionService.html#getSession(java.lang.String,java.lang.String,java.lang.String,java.util.Optional))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user.`sessionId`

- The unique identifier of the session to retrieve.`config`

- Optional configuration to filter the events returned within the session (e.g., limit number of recent events, filter by timestamp). If empty, default retrieval behavior is used (potentially all events or a service-defined limit).- Returns:
- An
containing the`Optional`

if found, otherwise`Session`

.`Optional.empty()`


-
### deleteSession

public io.reactivex.rxjava3.core.Completable deleteSession( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId)Description copied from interface:[BaseSessionService](BaseSessionService.html#deleteSession(java.lang.String,java.lang.String,java.lang.String))Deletes a specific session.- Specified by:

in interface[deleteSession](BaseSessionService.html#deleteSession(java.lang.String,java.lang.String,java.lang.String))[BaseSessionService](BaseSessionService.html)- Parameters:
`appName`

- The name of the application.`userId`

- The identifier of the user.`sessionId`

- The unique identifier of the session to delete.

-
### appendEvent

Description copied from interface:[BaseSessionService](BaseSessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))Appends an event to an in-memory session object and updates the session's state based on the event's state delta, if applicable.This method primarily modifies the passed

`session`

object in memory. Persisting these changes typically requires a separate call to an update/save method provided by the specific service implementation, or might happen implicitly depending on the implementation's design.If the event is marked as partial (e.g.,

`event.isPartial() == true`

), it is returned directly without modifying the session state or event list. State delta keys starting withare ignored during state updates.`State.TEMP_PREFIX`

- Specified by:

in interface[appendEvent](BaseSessionService.html#appendEvent(com.google.adk.sessions.Session,com.google.adk.events.Event))[BaseSessionService](BaseSessionService.html)- Parameters:
`session`

- Theobject to which the event should be appended (will be mutated).`Session`

`event`

- Theto append.`Event`

- Returns:
- The appended
instance (or the original event if it was partial).`Event`


-
