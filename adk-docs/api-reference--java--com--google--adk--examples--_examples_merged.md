---
merged_at: 2026-01-25T03:28:16.254126
merged_files: 7
---

# Documentos Fusionados

Este archivo contiene 7 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/package-summary.html -->

# Package com.google.adk.examples

package com.google.adk.examples

-
ClassDescriptionAn interface that provides examples for a given query.Represents an few-shot example.Builder for constructing
instances.`Example`

Utility class for examples.

`Example`


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/package-use.html -->

# Uses of Packagecom.google.adk.examples

# Uses of Package

com.google.adk.examples

-
ClassDescriptionAn interface that provides examples for a given query.Represents an few-shot example.
-
ClassDescriptionAn interface that provides examples for a given query.Represents an few-shot example.Builder for constructing
instances.`Example`


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/package-tree.html -->

# Hierarchy For Package com.google.adk.examples

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.examples.
[Example](Example.html) - com.google.adk.examples.
[Example.Builder](Example.Builder.html) - com.google.adk.examples.
[ExampleUtils](ExampleUtils.html)

- com.google.adk.examples.

## Interface Hierarchy

- com.google.adk.examples.
[BaseExampleProvider](BaseExampleProvider.html)


---

<!-- DOCUMENTO FUSIONADO: baseexampleproviderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/BaseExampleProvider.html -->

# Interface BaseExampleProvider

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.examples
BaseExampleProvider
Contents
Hide sidebar
❮
❯
Show sidebar
Description
Method Summary
Method Details
getExamples(String)
Interface BaseExampleProvider
public interface
BaseExampleProvider
An interface that provides examples for a given query.
Method Summary
All Methods
Instance Methods
Abstract Methods
Modifier and Type
Method
Description
List
<
Example
>
getExamples
(
String
query)
Method Details
getExamples
List
<
Example
>
getExamples
(
String
query)


---

<!-- DOCUMENTO FUSIONADO: examplebuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/Example.Builder.html -->

# Class Example.Builder

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.examples.Example.Builder

- Enclosing class:
[Example](Example.html)

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`abstract`

[Example](Example.html)[build](#build())()`abstract`

[Example.Builder](Example.Builder.html)[input](#input(com.google.genai.types.Content))(com.google.genai.types.Content input) `abstract`

[Example.Builder](Example.Builder.html)

-
## Constructor Details

-
### Builder

public Builder()

-
-
## Method Details

-
### input

-
### output

-
### build


-


---

<!-- DOCUMENTO FUSIONADO: examplehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/Example.html -->

# Class Example

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.examples.Example

Represents an few-shot example.

-
## Nested Class Summary

-
## Constructor Summary

-
## Method Summary

Modifier and TypeMethodDescription`static`

[Example.Builder](Example.Builder.html)[builder](#builder())()`abstract com.google.genai.types.Content`

[input](#input())()`abstract`

[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<com.google.genai.types.Content> [output](#output())()`abstract`

[Example.Builder](Example.Builder.html)

-
## Constructor Details

-
### Example

public Example()

-
-
## Method Details

-
### input

public abstract com.google.genai.types.Content input() -
### output

-
### builder

-
### toBuilder


-


---

<!-- DOCUMENTO FUSIONADO: exampleutilshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/ExampleUtils.html -->

# Class ExampleUtils

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.examples.ExampleUtils

Utility class for examples.

-
## Method Summary

Modifier and TypeMethodDescription`static`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[buildExampleSi](#buildExampleSi(com.google.adk.examples.BaseExampleProvider,java.lang.String))( [BaseExampleProvider](BaseExampleProvider.html)exampleProvider,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)query)Builds a formatted few-shot example string for the given query.

-
## Method Details

-
### buildExampleSi

Builds a formatted few-shot example string for the given query.- Parameters:
`exampleProvider`

- Source of examples.`query`

- User query.- Returns:
- formatted string with few-shot examples.


-
