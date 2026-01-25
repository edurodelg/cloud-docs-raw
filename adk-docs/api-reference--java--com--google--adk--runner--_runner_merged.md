---
merged_at: 2026-01-25T03:28:16.289357
merged_files: 5
---

# Documentos Fusionados

Este archivo contiene 5 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/runner/package-tree.html -->

# Hierarchy For Package com.google.adk.runner

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.runner
Hierarchy For Package com.google.adk.runner
Package Hierarchies:
All Packages
Class Hierarchy
java.lang.
Object
com.google.adk.runner.
Runner
com.google.adk.runner.
InMemoryRunner


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/runner/package-summary.html -->

# Package com.google.adk.runner

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.runner
Contents
Hide sidebar
❮
❯
Show sidebar
Description
Related Packages
Classes and Interfaces
Package com.google.adk.runner
package
com.google.adk.runner
Related Packages
Package
Description
com.google.adk
Classes
Class
Description
InMemoryRunner
The class for the in-memory GenAi runner, using in-memory artifact and session services.
Runner
The main class for the GenAI Agents runner.


---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/runner/package-use.html -->

# Uses of Packagecom.google.adk.runner

JavaScript is disabled on your browser.
Skip navigation links
Overview
Package
Use
Tree
Index
Search
com.google.adk.runner
Uses of Package
com.google.adk.runner
Packages that use
com.google.adk.runner
Package
Description
com.google.adk.runner
com.google.adk.web
Classes in
com.google.adk.runner
used by
com.google.adk.runner
Class
Description
Runner
The main class for the GenAI Agents runner.
Classes in
com.google.adk.runner
used by
com.google.adk.web
Class
Description
Runner
The main class for the GenAI Agents runner.


---

<!-- DOCUMENTO FUSIONADO: inmemoryrunnerhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/runner/InMemoryRunner.html -->

# Class InMemoryRunner

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.runner.Runner](Runner.html)

com.google.adk.runner.InMemoryRunner

The class for the in-memory GenAi runner, using in-memory artifact and session services.

-
## Constructor Summary

ConstructorDescription[InMemoryRunner](#%3Cinit%3E(com.google.adk.agents.BaseAgent))( [BaseAgent](../agents/BaseAgent.html)agent)[InMemoryRunner](#%3Cinit%3E(com.google.adk.agents.BaseAgent,java.lang.String))( [BaseAgent](../agents/BaseAgent.html)agent,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName) -
## Method Summary

### Methods inherited from class com.google.adk.runner.

[Runner](Runner.html)[agent](Runner.html#agent()),[appName](Runner.html#appName()),[artifactService](Runner.html#artifactService()),[runAsync](Runner.html#runAsync(com.google.adk.sessions.Session,com.google.genai.types.Content,com.google.adk.agents.RunConfig)),[runAsync](Runner.html#runAsync(java.lang.String,java.lang.String,com.google.genai.types.Content)),[runAsync](Runner.html#runAsync(java.lang.String,java.lang.String,com.google.genai.types.Content,com.google.adk.agents.RunConfig)),[runLive](Runner.html#runLive(com.google.adk.sessions.Session,com.google.adk.agents.LiveRequestQueue,com.google.adk.agents.RunConfig)),[runLive](Runner.html#runLive(java.lang.String,java.lang.String,com.google.adk.agents.LiveRequestQueue,com.google.adk.agents.RunConfig)),[runWithSessionId](Runner.html#runWithSessionId(java.lang.String,com.google.genai.types.Content,com.google.adk.agents.RunConfig)),[sessionService](Runner.html#sessionService())

-
## Constructor Details

-
### InMemoryRunner

-
### InMemoryRunner


-


---

<!-- DOCUMENTO FUSIONADO: runnerhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/runner/Runner.html -->

# Class Runner

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.runner.Runner

- Direct Known Subclasses:
[InMemoryRunner](InMemoryRunner.html)

The main class for the GenAI Agents runner.

-
## Constructor Summary

ConstructorDescription[Runner](#%3Cinit%3E(com.google.adk.agents.BaseAgent,java.lang.String,com.google.adk.artifacts.BaseArtifactService,com.google.adk.sessions.BaseSessionService))( [BaseAgent](../agents/BaseAgent.html)agent,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService,[BaseSessionService](../sessions/BaseSessionService.html)sessionService)Creates a new`Runner`

. -
## Method Summary

Modifier and TypeMethodDescription[agent](#agent())()[appName](#appName())()`io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>Runs the agent in the standard mode using a provided Session object.`io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>Asynchronously runs the agent for a given user and session, processing a new message and using a default.`RunConfig`

`io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runAsync](#runAsync(java.lang.String,java.lang.String,com.google.genai.types.Content,com.google.adk.agents.RunConfig))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, com.google.genai.types.Content newMessage,[RunConfig](../agents/RunConfig.html)runConfig)Runs the agent in the standard mode.`io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runLive](#runLive(com.google.adk.sessions.Session,com.google.adk.agents.LiveRequestQueue,com.google.adk.agents.RunConfig))( [Session](../sessions/Session.html)session,[LiveRequestQueue](../agents/LiveRequestQueue.html)liveRequestQueue,[RunConfig](../agents/RunConfig.html)runConfig)Runs the agent in live mode, appending generated events to the session.`io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runLive](#runLive(java.lang.String,java.lang.String,com.google.adk.agents.LiveRequestQueue,com.google.adk.agents.RunConfig))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[LiveRequestQueue](../agents/LiveRequestQueue.html)liveRequestQueue,[RunConfig](../agents/RunConfig.html)runConfig)Retrieves the session and runs the agent in live mode.`io.reactivex.rxjava3.core.Flowable`

< [Event](../events/Event.html)>[runWithSessionId](#runWithSessionId(java.lang.String,com.google.genai.types.Content,com.google.adk.agents.RunConfig))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, com.google.genai.types.Content newMessage,[RunConfig](../agents/RunConfig.html)runConfig)Runs the agent asynchronously with a default user ID.

-
## Constructor Details

-
### Runner

public Runner( [BaseAgent](../agents/BaseAgent.html)agent,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)appName,[BaseArtifactService](../artifacts/BaseArtifactService.html)artifactService,[BaseSessionService](../sessions/BaseSessionService.html)sessionService)Creates a new`Runner`

.

-
-
## Method Details

-
### agent

-
### appName

-
### artifactService

-
### sessionService

-
### runAsync

public io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runAsync( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, com.google.genai.types.Content newMessage,[RunConfig](../agents/RunConfig.html)runConfig)Runs the agent in the standard mode.- Parameters:
`userId`

- The ID of the user for the session.`sessionId`

- The ID of the session to run the agent in.`newMessage`

- The new message from the user to process.`runConfig`

- Configuration for the agent run.- Returns:
- A Flowable stream of
objects generated by the agent during execution.`Event`


-
### runAsync

public io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runAsync( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId, com.google.genai.types.Content newMessage)Asynchronously runs the agent for a given user and session, processing a new message and using a default.`RunConfig`

This method initiates an agent execution within the specified session, appending the provided new message to the session's history. It utilizes a default

`RunConfig`

to control execution parameters. The method returns a stream ofobjects representing the agent's activity during the run.`Event`

- Parameters:
`userId`

- The ID of the user initiating the session.`sessionId`

- The ID of the session in which the agent will run.`newMessage`

- The new`Content`

message to be processed by the agent.- Returns:
- A
`Flowable`

emittingobjects generated by the agent.`Event`


-
### runAsync

public io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runAsync( [Session](../sessions/Session.html)session, com.google.genai.types.Content newMessage,[RunConfig](../agents/RunConfig.html)runConfig)Runs the agent in the standard mode using a provided Session object.- Parameters:
`session`

- The session to run the agent in.`newMessage`

- The new message from the user to process.`runConfig`

- Configuration for the agent run.- Returns:
- A Flowable stream of
objects generated by the agent during execution.`Event`


-
### runLive

public io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runLive( [Session](../sessions/Session.html)session,[LiveRequestQueue](../agents/LiveRequestQueue.html)liveRequestQueue,[RunConfig](../agents/RunConfig.html)runConfig)Runs the agent in live mode, appending generated events to the session.- Returns:
- stream of events from the agent.

-
### runLive

public io.reactivex.rxjava3.core.Flowable<[Event](../events/Event.html)> runLive( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)userId,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)sessionId,[LiveRequestQueue](../agents/LiveRequestQueue.html)liveRequestQueue,[RunConfig](../agents/RunConfig.html)runConfig)Retrieves the session and runs the agent in live mode.- Returns:
- stream of events from the agent.
- Throws:

- if the session is not found.[IllegalArgumentException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/IllegalArgumentException.html)

-
### runWithSessionId


-
