---
source_url: https://google.github.io/adk-docs/runtime/
fetched_at: 2026-01-25T03:12:30.411339
---

# Agent Runtime¶

# Agent Runtime[¶](#agent-runtime)

Supported in ADKPython v0.1.0TypeScript v0.2.0Go v0.1.0Java v0.1.0

ADK provides several ways to run and test your agents during development. Choose the method that best fits your development workflow.

## Ways to run agents[¶](#ways-to-run-agents)

-
**Dev UI**

Use

`adk web`

to launch a browser-based interface for interacting with your agents. -
**Command Line**

Use

`adk run`

to interact with your agents directly in the terminal. -
**API Server**

Use

`adk api_server`

to expose your agents through a RESTful API.

## Technical reference[¶](#technical-reference)

For more in-depth information on runtime configuration and behavior, see these pages:

: Understand the core event loop that powers ADK, including the yield/pause/resume cycle.[Event Loop](event-loop/): Learn how to resume agent execution from a previous state.[Resume Agents](resume/): Configure runtime behavior with RunConfig.[Runtime Config](runconfig/)