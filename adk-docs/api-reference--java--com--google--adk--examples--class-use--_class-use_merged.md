---
merged_at: 2026-01-25T03:28:16.314550
merged_files: 4
---

# Documentos Fusionados

Este archivo contiene 4 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: examplehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/class-use/Example.html -->

# Uses of Classcom.google.adk.examples.Example

LlmAgent.Builder

exampleProvider(Example... examples)

exampleProvider(List<Example> examples)

abstract Example

build()

List<Example>

getExamples(String query)


---

<!-- DOCUMENTO FUSIONADO: exampleutilshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/class-use/ExampleUtils.html -->

# Uses of Classcom.google.adk.examples.ExampleUtils

JavaScript is disabled on your browser.
Skip navigation links
Overview
Class
Use
Tree
Index
Search
com.google.adk.examples
ExampleUtils
Uses of Class
com.google.adk.examples.ExampleUtils
No usage of com.google.adk.examples.ExampleUtils


---

<!-- DOCUMENTO FUSIONADO: examplebuilderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/class-use/Example.Builder.html -->

# Uses of Classcom.google.adk.examples.Example.Builder

# Uses of Class

com.google.adk.examples.Example.Builder

-
## Uses of

[Example.Builder](../Example.Builder.html)in[com.google.adk.examples](../package-summary.html)Modifier and TypeMethodDescription`static`

[Example.Builder](../Example.Builder.html)Example.[builder](../Example.html#builder())()`abstract`

[Example.Builder](../Example.Builder.html)Example.Builder.[input](../Example.Builder.html#input(com.google.genai.types.Content))(com.google.genai.types.Content input) `abstract`

[Example.Builder](../Example.Builder.html)`abstract`

[Example.Builder](../Example.Builder.html)Example.[toBuilder](../Example.html#toBuilder())()


---

<!-- DOCUMENTO FUSIONADO: baseexampleproviderhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/examples/class-use/BaseExampleProvider.html -->

# Uses of Interfacecom.google.adk.examples.BaseExampleProvider

# Uses of Interface

com.google.adk.examples.BaseExampleProvider

-
## Uses of

[BaseExampleProvider](../BaseExampleProvider.html)in[com.google.adk.agents](../../agents/package-summary.html)Modifier and TypeMethodDescriptionLlmAgent.Builder.[exampleProvider](../../agents/LlmAgent.Builder.html#exampleProvider(com.google.adk.examples.BaseExampleProvider))( [BaseExampleProvider](../BaseExampleProvider.html)exampleProvider) -
## Uses of

[BaseExampleProvider](../BaseExampleProvider.html)in[com.google.adk.examples](../package-summary.html)Modifier and TypeMethodDescription`static`

[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)ExampleUtils.[buildExampleSi](../ExampleUtils.html#buildExampleSi(com.google.adk.examples.BaseExampleProvider,java.lang.String))( [BaseExampleProvider](../BaseExampleProvider.html)exampleProvider,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)query)Builds a formatted few-shot example string for the given query.
