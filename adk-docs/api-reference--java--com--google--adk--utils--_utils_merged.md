---
merged_at: 2026-01-25T02:21:31.807501
merged_files: 6
---

# Documentos Fusionados

Este archivo contiene 6 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/utils/package-use.html -->

# Uses of Packagecom.google.adk.utils

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.utils
Uses of Package
com.google.adk.utils
No usage of com.google.adk.utils


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/utils/package-tree.html -->

# Hierarchy For Package com.google.adk.utils

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.utils
Hierarchy For Package com.google.adk.utils
Package Hierarchies:
All Packages
Class Hierarchy
java.lang.
Object
com.google.adk.utils.
CollectionUtils
com.google.adk.utils.
InstructionUtils
com.google.adk.utils.
Pairs


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/utils/package-summary.html -->

# Package com.google.adk.utils

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.utils
Contents
Hide sidebar
❮
❯
Show sidebar
Description
Related Packages
Classes and Interfaces
Package com.google.adk.utils
package
com.google.adk.utils
Related Packages
Package
Description
com.google.adk
Classes
Class
Description
CollectionUtils
Frequently used code snippets for collections.
InstructionUtils
Utility methods for handling instruction templates.
Pairs
Utility class for creating ConcurrentHashMaps.


---

<!-- DOCUMENTO FUSIONADO: collectionutilshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/utils/CollectionUtils.html -->

# Class CollectionUtils

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.utils.CollectionUtils

Frequently used code snippets for collections.

-
## Method Summary

Modifier and TypeMethodDescription`static <T> boolean`

[isNullOrEmpty](#isNullOrEmpty(java.lang.Iterable))( [Iterable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Iterable.html)<T> iterable)Checks if the given iterable is null or empty.

-
## Method Details

-
### isNullOrEmpty

Checks if the given iterable is null or empty.- Parameters:
`iterable`

- the iterable to check- Returns:
- true if the iterable is null or empty, false otherwise


-


---

<!-- DOCUMENTO FUSIONADO: instructionutilshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/utils/InstructionUtils.html -->

# Class InstructionUtils

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.utils.InstructionUtils

Utility methods for handling instruction templates.

-
## Method Summary

Modifier and TypeMethodDescription`static io.reactivex.rxjava3.core.Single`

< [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>[injectSessionState](#injectSessionState(com.google.adk.agents.InvocationContext,java.lang.String))( [InvocationContext](../agents/InvocationContext.html)context,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)template)Populates placeholders in an instruction template string with values from the session state or loaded artifacts.

-
## Method Details

-
### injectSessionState

public static io.reactivex.rxjava3.core.Single<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> injectSessionState( [InvocationContext](../agents/InvocationContext.html)context,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)template)Populates placeholders in an instruction template string with values from the session state or loaded artifacts.**Placeholder Syntax:**Placeholders are enclosed by one or more curly braces at the start and end, e.g.,

`{key}`

or`{{key}}`

. The core`key`

is extracted from whatever is between the innermost pair of braces after trimming whitespace and possibly removing the`?`

which denotes optionality (e.g.`{key?}`

). The`key`

itself must not contain curly braces. For typical usage, a single pair of braces like`{my_variable}`

is standard.The extracted

`key`

determines the source and name of the value:**Session State Variables:**The`key`

(e.g.,`"variable_name"`

or`"prefix:variable_name"`

) refers to a variable in session state.- Simple name:
`{variable_name}`

. The`variable_name`

part must be a valid identifier as per`isValidStateName(String)`

. Invalid names will result in the placeholder being returned as is. - Prefixed name:
`{prefix:variable_name}`

. Valid prefixes are:["app:"](../sessions/State.html#APP_PREFIX),["user:"](../sessions/State.html#USER_PREFIX), and["temp:"](../sessions/State.html#TEMP_PREFIX)The part of the name following the prefix must also be a valid identifier. Invalid prefixes will result in the placeholder being returned as is.

- Simple name:

**Artifacts:**The`key`

starts with "`artifact.`

" (e.g.,`"artifact.file_name"`

).**Optional Placeholders:**A`key`

can be marked as optional by appending a question mark`?`

at its very end, inside the braces.- Example:
`{optional_variable?}`

,`{{artifact.optional_file.txt?}}`

- If an optional placeholder cannot be resolved (e.g., variable not found, artifact not found), it is replaced with an empty string.

**Example Usage:**`InvocationContext context = ...; // Assume this is initialized with session and artifact service Session session = context.session(); session.state().put("user:name", "Alice"); context.artifactService().saveArtifact( session.appName(), session.userId(), session.id(), "knowledge.txt", Part.fromText("Origins of the universe: At first, there was-")); String template = "You are {user:name}'s assistant. Answer questions based on your knowledge. Your knowledge: {artifact.knowledge.txt}." + " Your extra knowledge: {artifact.missing_artifact.txt?}"; Single<String> populatedStringSingle = InstructionUtils.injectSessionState(context, template); populatedStringSingle.subscribe( result -> System.out.println(result), // Expected: "You are Alice's assistant. Answer questions based on your knowledge. Your knowledge: Origins of the universe: At first, there was-. Your extra knowledge: " error -> System.err.println("Error populating template: " + error.getMessage()) );`

- Parameters:
`context`

- The invocation context providing access to session state and artifact services.`template`

- The instruction template string containing placeholders to be populated.- Returns:
- A
`Single`

that will emit the populated instruction string upon successful resolution of all non-optional placeholders. Emits the original template if it is empty or contains no placeholders that are processed. - Throws:

- if the template or context is null.[NullPointerException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/NullPointerException.html)

- if a non-optional variable or artifact is not found.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)


-


---

<!-- DOCUMENTO FUSIONADO: pairshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/utils/Pairs.html -->

# Class Pairs

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.utils.Pairs

Utility class for creating ConcurrentHashMaps.

-
## Method Summary

Modifier and TypeMethodDescription`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of())()Returns a new, empty`ConcurrentHashMap`

.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V))(K k1, V v1) Returns a new`ConcurrentHashMap`

containing a single mapping.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V,K,V))(K k1, V v1, K k2, V v2) Returns a new`ConcurrentHashMap`

containing two mappings.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V,K,V,K,V))(K k1, V v1, K k2, V v2, K k3, V v3) Returns a new`ConcurrentHashMap`

containing three mappings.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V,K,V,K,V,K,V))(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4) Returns a new`ConcurrentHashMap`

containing four mappings.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V,K,V,K,V,K,V,K,V))(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5) Returns a new`ConcurrentHashMap`

containing five mappings.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V,K,V,K,V,K,V,K,V,K,V))(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6) Returns a new`ConcurrentHashMap`

containing six mappings.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V,K,V,K,V,K,V,K,V,K,V,K,V))(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7) Returns a new`ConcurrentHashMap`

containing seven mappings.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V,K,V,K,V,K,V,K,V,K,V,K,V,K,V))(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7, K k8, V v8) Returns a new`ConcurrentHashMap`

containing eight mappings.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V,K,V,K,V,K,V,K,V,K,V,K,V,K,V,K,V))(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7, K k8, V v8, K k9, V v9) Returns a new`ConcurrentHashMap`

containing nine mappings.`static <K,`

V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K, V> [of](#of(K,V,K,V,K,V,K,V,K,V,K,V,K,V,K,V,K,V,K,V))(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7, K k8, V v8, K k9, V v9, K k10, V v10) Returns a new`ConcurrentHashMap`

containing ten mappings.

-
## Method Details

-
### of

Returns a new, empty`ConcurrentHashMap`

.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Returns:
- an empty
`ConcurrentHashMap`


-
### of

Returns a new`ConcurrentHashMap`

containing a single mapping.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the mapping's key`v1`

- the mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mapping - Throws:

- if the key or the value is[NullPointerException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/NullPointerException.html)`null`


-
### of

Returns a new`ConcurrentHashMap`

containing two mappings. This method leverages`java.util.Map.of`

for initial validation.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the first mapping's key`v1`

- the first mapping's value`k2`

- the second mapping's key`v2`

- the second mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mappings

-
### of

Returns a new`ConcurrentHashMap`

containing three mappings. This method leverages`java.util.Map.of`

for initial validation.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the first mapping's key`v1`

- the first mapping's value`k2`

- the second mapping's key`v2`

- the second mapping's value`k3`

- the third mapping's key`v3`

- the third mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mappings

-
### of

Returns a new`ConcurrentHashMap`

containing four mappings. This method leverages`java.util.Map.of`

for initial validation.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the first mapping's key`v1`

- the first mapping's value`k2`

- the second mapping's key`v2`

- the second mapping's value`k3`

- the third mapping's key`v3`

- the third mapping's value`k4`

- the fourth mapping's key`v4`

- the fourth mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mappings

-
### of

public static <K,V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K,V> of (K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5) Returns a new`ConcurrentHashMap`

containing five mappings. This method leverages`java.util.Map.of`

for initial validation.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the first mapping's key`v1`

- the first mapping's value`k2`

- the second mapping's key`v2`

- the second mapping's value`k3`

- the third mapping's key`v3`

- the third mapping's value`k4`

- the fourth mapping's key`v4`

- the fourth mapping's value`k5`

- the fifth mapping's key`v5`

- the fifth mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mappings

-
### of

public static <K,V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K,V> of (K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6) Returns a new`ConcurrentHashMap`

containing six mappings. This method leverages`java.util.Map.of`

for initial validation.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the first mapping's key`v1`

- the first mapping's value`k2`

- the second mapping's key`v2`

- the second mapping's value`k3`

- the third mapping's key`v3`

- the third mapping's value`k4`

- the fourth mapping's key`v4`

- the fourth mapping's value`k5`

- the fifth mapping's key`v5`

- the fifth mapping's value`k6`

- the sixth mapping's key`v6`

- the sixth mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mappings - Throws:

- if there are any duplicate keys (behavior inherited from Map.of)[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)

- if any key or value is[NullPointerException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/NullPointerException.html)`null`

(behavior inherited from Map.of)

-
### of

public static <K,V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K,V> of (K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7) Returns a new`ConcurrentHashMap`

containing seven mappings. This method leverages`java.util.Map.of`

for initial validation.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the first mapping's key`v1`

- the first mapping's value`k2`

- the second mapping's key`v2`

- the second mapping's value`k3`

- the third mapping's key`v3`

- the third mapping's value`k4`

- the fourth mapping's key`v4`

- the fourth mapping's value`k5`

- the fifth mapping's key`v5`

- the fifth mapping's value`k6`

- the sixth mapping's key`v6`

- the sixth mapping's value`k7`

- the seventh mapping's key`v7`

- the seventh mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mappings

-
### of

public static <K,V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K,V> of (K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7, K k8, V v8) Returns a new`ConcurrentHashMap`

containing eight mappings. This method leverages`java.util.Map.of`

for initial validation.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the first mapping's key`v1`

- the first mapping's value`k2`

- the second mapping's key`v2`

- the second mapping's value`k3`

- the third mapping's key`v3`

- the third mapping's value`k4`

- the fourth mapping's key`v4`

- the fourth mapping's value`k5`

- the fifth mapping's key`v5`

- the fifth mapping's value`k6`

- the sixth mapping's key`v6`

- the sixth mapping's value`k7`

- the seventh mapping's key`v7`

- the seventh mapping's value`k8`

- the eighth mapping's key`v8`

- the eighth mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mappings

-
### of

public static <K,V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K,V> of (K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7, K k8, V v8, K k9, V v9) Returns a new`ConcurrentHashMap`

containing nine mappings. This method leverages`java.util.Map.of`

for initial validation.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the first mapping's key`v1`

- the first mapping's value`k2`

- the second mapping's key`v2`

- the second mapping's value`k3`

- the third mapping's key`v3`

- the third mapping's value`k4`

- the fourth mapping's key`v4`

- the fourth mapping's value`k5`

- the fifth mapping's key`v5`

- the fifth mapping's value`k6`

- the sixth mapping's key`v6`

- the sixth mapping's value`k7`

- the seventh mapping's key`v7`

- the seventh mapping's value`k8`

- the eighth mapping's key`v8`

- the eighth mapping's value`k9`

- the ninth mapping's key`v9`

- the ninth mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mappings

-
### of

public static <K,V> [ConcurrentHashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/concurrent/ConcurrentHashMap.html)<K,V> of (K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7, K k8, V v8, K k9, V v9, K k10, V v10) Returns a new`ConcurrentHashMap`

containing ten mappings. This method leverages`java.util.Map.of`

for initial validation.- Type Parameters:
`K`

- the`ConcurrentHashMap`

's key type`V`

- the`ConcurrentHashMap`

's value type- Parameters:
`k1`

- the first mapping's key`v1`

- the first mapping's value`k2`

- the second mapping's key`v2`

- the second mapping's value`k3`

- the third mapping's key`v3`

- the third mapping's value`k4`

- the fourth mapping's key`v4`

- the fourth mapping's value`k5`

- the fifth mapping's key`v5`

- the fifth mapping's value`k6`

- the sixth mapping's key`v6`

- the sixth mapping's value`k7`

- the seventh mapping's key`v7`

- the seventh mapping's value`k8`

- the eighth mapping's key`v8`

- the eighth mapping's value`k9`

- the ninth mapping's key`v9`

- the ninth mapping's value`k10`

- the tenth mapping's key`v10`

- the tenth mapping's value- Returns:
- a
`ConcurrentHashMap`

containing the specified mappings


-
