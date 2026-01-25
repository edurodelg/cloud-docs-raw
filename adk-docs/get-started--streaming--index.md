---
source_url: https://google.github.io/adk-docs/get-started/streaming/
fetched_at: 2026-01-25T02:03:45.926982
---

# Build a streaming agent¶

# Build a streaming agent[¶](#build-a-streaming-agent)

The Agent Development Kit (ADK) enables real-time, interactive experiences with your AI agents through streaming. This allows for features like live voice conversations, real-time tool use, and continuous updates from your agent.

This page provides quickstart examples to get you up and running with streaming capabilities in both Python and Java ADK.

-
**Python ADK: Streaming agent**

This example demonstrates how to set up a basic streaming interaction with an agent using Python ADK. It typically involves using the

`Runner.run_live()`

method and handling asynchronous events.

-
**Java ADK: Streaming agent**

This example demonstrates how to set up a basic streaming interaction with an agent using Java ADK. It involves using the

`Runner.runLive()`

method, a`LiveRequestQueue`

, and handling the`Flowable<Event>`

stream.