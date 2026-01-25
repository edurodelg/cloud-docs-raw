---
merged_at: 2026-01-25T03:28:16.328585
merged_files: 4
---

# Documentos Fusionados

Este archivo contiene 4 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/package-tree.html -->

# Hierarchy For Package com.google.adk.flows

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.flows
Hierarchy For Package com.google.adk.flows
Package Hierarchies:
All Packages
Interface Hierarchy
com.google.adk.flows.
BaseFlow


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/package-use.html -->

# Uses of Packagecom.google.adk.flows

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.flows
Uses of Package
com.google.adk.flows
Packages that use
com.google.adk.flows
Package
Description
com.google.adk.flows.llmflows
Classes in
com.google.adk.flows
used by
com.google.adk.flows.llmflows
Class
Description
BaseFlow
Interface for the execution flows to run a group of agents.


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/package-summary.html -->

# Package com.google.adk.flows

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.flows
Contents
Hide sidebar
❮
❯
Show sidebar
Description
Related Packages
Classes and Interfaces
Package com.google.adk.flows
package
com.google.adk.flows
Related Packages
Package
Description
com.google.adk
com.google.adk.flows.llmflows
Interfaces
Class
Description
BaseFlow
Interface for the execution flows to run a group of agents.


---

<!-- DOCUMENTO FUSIONADO: baseflowhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/flows/BaseFlow.html -->

# Interface BaseFlow

- All Known Implementing Classes:

,[AutoFlow](llmflows/AutoFlow.html)

,[BaseLlmFlow](llmflows/BaseLlmFlow.html)[SingleFlow](llmflows/SingleFlow.html)

public interface BaseFlow

Interface for the execution flows to run a group of agents.

-
## Method Summary

Modifier and TypeMethodDescription`io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[run](#run(com.google.adk.agents.InvocationContext))( [InvocationContext](../agents/InvocationContext.html)invocationContext)Run this flow.`default io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runLive](#runLive(com.google.adk.agents.InvocationContext))( [InvocationContext](../agents/InvocationContext.html)invocationContext)

-
## Method Details

-
### run

Run this flow.To implement this method, the flow should follow the below requirements:

- 1. `session` should be treated as immutable, DO NOT change it.
- 2. The caller who trigger the flow is responsible for updating the session as the events being generated. The subclass implementation will assume session is updated after each yield event statement.
- 3. A flow may spawn sub-agent flows depending on the agent definition.

-
### runLive


-
