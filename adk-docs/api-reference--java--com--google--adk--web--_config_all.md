---
merged_at: 2026-01-25T03:28:16.432274
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _class-use_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 3 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: adkwebcorsconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/config/class-use/AdkWebCorsConfig.html -->

# Uses of Classcom.google.adk.web.config.AdkWebCorsConfig

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.web.config
AdkWebCorsConfig
Uses of Class
com.google.adk.web.config.AdkWebCorsConfig
No usage of com.google.adk.web.config.AdkWebCorsConfig


---

<!-- DOCUMENTO FUSIONADO: adkwebcorspropertieshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/config/class-use/AdkWebCorsProperties.html -->

# Uses of Record Classcom.google.adk.web.config.AdkWebCorsProperties

# Uses of Record Class

com.google.adk.web.config.AdkWebCorsProperties

-
## Uses of

[AdkWebCorsProperties](../AdkWebCorsProperties.html)in[com.google.adk.web.config](../package-summary.html)Modifier and TypeMethodDescription`org.springframework.web.cors.CorsConfigurationSource`

AdkWebCorsConfig.[corsConfigurationSource](../AdkWebCorsConfig.html#corsConfigurationSource(com.google.adk.web.config.AdkWebCorsProperties))( [AdkWebCorsProperties](../AdkWebCorsProperties.html)corsProperties)


---

<!-- DOCUMENTO FUSIONADO: agentloadingpropertieshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/config/class-use/AgentLoadingProperties.html -->

# Uses of Classcom.google.adk.web.config.AgentLoadingProperties

# Uses of Class

com.google.adk.web.config.AgentLoadingProperties

-
## Uses of

[AgentLoadingProperties](../AgentLoadingProperties.html)in[com.google.adk.web](../../package-summary.html)Modifier and TypeMethodDescriptionAdkWebServer.[loadedAgentRegistry](../../AdkWebServer.html#loadedAgentRegistry(com.google.adk.web.AgentCompilerLoader,com.google.adk.web.config.AgentLoadingProperties))( [AgentCompilerLoader](../../AgentCompilerLoader.html)loader,[AgentLoadingProperties](../AgentLoadingProperties.html)props)ModifierConstructorDescription[AgentCompilerLoader](../../AgentCompilerLoader.html#%3Cinit%3E(com.google.adk.web.config.AgentLoadingProperties))( [AgentLoadingProperties](../AgentLoadingProperties.html)properties)Initializes the loader with agent configuration and proactively attempts to locate the ADK core JAR.


---

<!-- DOCUMENTO FUSIONADO: _config_merged.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 6 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/config/package-summary.html -->

# Package com.google.adk.web.config

package com.google.adk.web.config

-
ClassDescriptionConfiguration class for setting up Cross-Origin Resource Sharing (CORS) in the ADK Web application.Properties for configuring CORS in ADK Web.Properties for loading agents.


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/config/package-use.html -->

# Uses of Packagecom.google.adk.web.config

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.web.config
Uses of Package
com.google.adk.web.config
Packages that use
com.google.adk.web.config
Package
Description
com.google.adk.web
com.google.adk.web.config
Classes in
com.google.adk.web.config
used by
com.google.adk.web
Class
Description
AgentLoadingProperties
Properties for loading agents.
Classes in
com.google.adk.web.config
used by
com.google.adk.web.config
Class
Description
AdkWebCorsProperties
Properties for configuring CORS in ADK Web.


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/config/package-tree.html -->

# Hierarchy For Package com.google.adk.web.config

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.web.config.
[AdkWebCorsConfig](AdkWebCorsConfig.html) - com.google.adk.web.config.
[AgentLoadingProperties](AgentLoadingProperties.html)

- com.google.adk.web.config.

## Record Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- java.lang.
[Record](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Record.html)- com.google.adk.web.config.
[AdkWebCorsProperties](AdkWebCorsProperties.html)

- com.google.adk.web.config.

- java.lang.


---

<!-- DOCUMENTO FUSIONADO: agentloadingpropertieshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/config/AgentLoadingProperties.html -->

# Class AgentLoadingProperties

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.config.AgentLoadingProperties

@Component
@ConfigurationProperties(prefix="adk.agents")
public class AgentLoadingProperties
extends

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)Properties for loading agents.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`void`

[setCompileClasspath](#setCompileClasspath(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)compileClasspath)`void`

[setSourceDir](#setSourceDir(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sourceDir)

-
## Constructor Details

-
### AgentLoadingProperties

public AgentLoadingProperties()

-
-
## Method Details

-
### getSourceDir

-
### setSourceDir

-
### getCompileClasspath

-
### setCompileClasspath


-


---

<!-- DOCUMENTO FUSIONADO: adkwebcorsconfightml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/config/AdkWebCorsConfig.html -->

# Class AdkWebCorsConfig

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.web.config.AdkWebCorsConfig

Configuration class for setting up Cross-Origin Resource Sharing (CORS) in the ADK Web
application. This class defines beans for configuring CORS settings based on properties defined
in

[.](AdkWebCorsProperties.html)`AdkWebCorsProperties`

CORS allows the application to handle requests from different origins, enabling secure communication between the frontend and backend services.

Beans provided:

`CorsConfigurationSource`

: Configures CORS settings such as allowed origins, methods, headers, credentials, and max age.`CorsFilter`

: Applies the CORS configuration to incoming requests.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`org.springframework.web.cors.CorsConfigurationSource`

[corsConfigurationSource](#corsConfigurationSource(com.google.adk.web.config.AdkWebCorsProperties))( [AdkWebCorsProperties](AdkWebCorsProperties.html)corsProperties)`org.springframework.web.filter.CorsFilter`

[corsFilter](#corsFilter(org.springframework.web.cors.CorsConfigurationSource))(org.springframework.web.cors.CorsConfigurationSource corsConfigurationSource)

-
## Constructor Details

-
### AdkWebCorsConfig

public AdkWebCorsConfig()

-
-
## Method Details

-
### corsConfigurationSource

@Bean public org.springframework.web.cors.CorsConfigurationSource corsConfigurationSource( [AdkWebCorsProperties](AdkWebCorsProperties.html)corsProperties) -
### corsFilter

@Bean public org.springframework.web.filter.CorsFilter corsFilter(org.springframework.web.cors.CorsConfigurationSource corsConfigurationSource)

-


---

<!-- DOCUMENTO FUSIONADO: adkwebcorspropertieshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/web/config/AdkWebCorsProperties.html -->

# Record Class AdkWebCorsProperties

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[java.lang.Record](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Record.html)

com.google.adk.web.config.AdkWebCorsProperties

@ConfigurationProperties(prefix="adk.web.cors")
public record AdkWebCorsProperties(

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)mapping,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> origins,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> methods,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> headers, boolean allowCredentials, long maxAge) extends[Record](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Record.html)Properties for configuring CORS in ADK Web. This class is used to load CORS settings from
application properties.

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`boolean`

Returns the value of the`allowCredentials`

record component.`final boolean`

Indicates whether some other object is "equal to" this one.`final int`

[hashCode](#hashCode())()Returns a hash code value for this object.[headers](#headers())()Returns the value of the`headers`

record component.[mapping](#mapping())()Returns the value of the`mapping`

record component.`long`

[maxAge](#maxAge())()Returns the value of the`maxAge`

record component.[methods](#methods())()Returns the value of the`methods`

record component.[origins](#origins())()Returns the value of the`origins`

record component.`final`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[toString](#toString())()Returns a string representation of this record class.

-
## Constructor Details

-
### AdkWebCorsProperties

public AdkWebCorsProperties( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)mapping,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> origins,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> methods,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> headers, boolean allowCredentials, long maxAge)Creates an instance of a`AdkWebCorsProperties`

record class.- Parameters:
`mapping`

- the value for the`mapping`

record component`origins`

- the value for the`origins`

record component`methods`

- the value for the`methods`

record component`headers`

- the value for the`headers`

record component`allowCredentials`

- the value for the`allowCredentials`

record component`maxAge`

- the value for the`maxAge`

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

Indicates whether some other object is "equal to" this one. The objects are equal if the other object is of the same class and if all the record components are equal. Reference components are compared with; primitive components are compared with the`Objects::equals(Object,Object)`

`compare`

method from their corresponding wrapper classes. -
### mapping

Returns the value of the`mapping`

record component.- Returns:
- the value of the
`mapping`

record component

-
### origins

-
### methods

-
### headers

-
### allowCredentials

public boolean allowCredentials()Returns the value of the`allowCredentials`

record component.- Returns:
- the value of the
`allowCredentials`

record component

-
### maxAge

public long maxAge()Returns the value of the`maxAge`

record component.- Returns:
- the value of the
`maxAge`

record component


-
