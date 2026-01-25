---
merged_at: 2026-01-25T02:21:31.825145
merged_files: 5
---

# Documentos Fusionados

Este archivo contiene 5 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/network/package-tree.html -->

# Hierarchy For Package com.google.adk.network

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.network
Hierarchy For Package com.google.adk.network
Package Hierarchies:
All Packages
Class Hierarchy
java.lang.
Object
com.google.adk.network.
ApiResponse
(implements java.lang.
AutoCloseable
)
com.google.adk.network.
HttpApiResponse


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/network/package-use.html -->

# Uses of Packagecom.google.adk.network

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.network
Uses of Package
com.google.adk.network
Packages that use
com.google.adk.network
Package
Description
com.google.adk.network
Classes in
com.google.adk.network
used by
com.google.adk.network
Class
Description
ApiResponse
The API response contains a response to a call to the GenAI APIs.


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/network/package-summary.html -->

# Package com.google.adk.network

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.network
Contents
Hide sidebar
❮
❯
Show sidebar
Description
Related Packages
Classes and Interfaces
Package com.google.adk.network
package
com.google.adk.network
Related Packages
Package
Description
com.google.adk
Classes
Class
Description
ApiResponse
The API response contains a response to a call to the GenAI APIs.
HttpApiResponse
Wraps a real HTTP response to expose the methods needed by the GenAI SDK.


---

<!-- DOCUMENTO FUSIONADO: apiresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/network/ApiResponse.html -->

# Class ApiResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.network.ApiResponse

- All Implemented Interfaces:
[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

- Direct Known Subclasses:
[HttpApiResponse](HttpApiResponse.html)

The API response contains a response to a call to the GenAI APIs.

-
## Constructor Summary

-
## Method Summary


-
## Constructor Details

-
### ApiResponse

public ApiResponse()

-
-
## Method Details

-
### getEntity

public abstract okhttp3.ResponseBody getEntity()Gets the ResponseBody. -
### close

public abstract void close()- Specified by:

in interface[close](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html#close())[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)


-


---

<!-- DOCUMENTO FUSIONADO: httpapiresponsehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/network/HttpApiResponse.html -->

# Class HttpApiResponse

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.network.ApiResponse](ApiResponse.html)

com.google.adk.network.HttpApiResponse

- All Implemented Interfaces:
[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

Wraps a real HTTP response to expose the methods needed by the GenAI SDK.

-
## Constructor Summary

ConstructorDescription[HttpApiResponse](#%3Cinit%3E(okhttp3.Response))(okhttp3.Response response) Constructs a HttpApiResponse instance with the response. -
## Method Summary


-
## Constructor Details

-
### HttpApiResponse

public HttpApiResponse(okhttp3.Response response) Constructs a HttpApiResponse instance with the response.

-
-
## Method Details

-
### getEntity

public okhttp3.ResponseBody getEntity()Returns the ResponseBody from the response.- Specified by:

in class[getEntity](ApiResponse.html#getEntity())[ApiResponse](ApiResponse.html)

-
### close

public void close()Closes the Http response.- Specified by:

in interface[close](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html#close())[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)- Specified by:

in class[close](ApiResponse.html#close())[ApiResponse](ApiResponse.html)


-
