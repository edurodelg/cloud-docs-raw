---
source_url: https://google.github.io/adk-docs/streaming/
fetched_at: 2026-01-26T22:56:39.246409
---

# Bidi-streaming (live) in ADK¶

# Bidi-streaming (live) in ADK[¶](#bidi-streaming-live-in-adk)

Bidirectional (Bidi) streaming (live) in ADK adds the low-latency bidirectional voice and video interaction
capability of [Gemini Live API](https://ai.google.dev/gemini-api/docs/live) to
AI agents.

With bidi-streaming, or live, mode, you can provide end users with the experience of natural, human-like voice conversations, including the ability for the user to interrupt the agent's responses with voice commands. Agents with streaming can process text, audio, and video inputs, and they can provide text and audio output.

-
**Quickstart (Bidi-streaming)**

In this quickstart, you'll build a simple agent and use streaming in ADK to implement low-latency and bidirectional voice and video communication.

-
**Bidi-streaming Demo Application**

A production-ready reference implementation showcasing ADK bidirectional streaming with multimodal support (text, audio, image). This FastAPI-based demo demonstrates real-time WebSocket communication, automatic transcription, tool calling with Google Search, and complete streaming lifecycle management. This demo is extensively referenced throughout the development guide series.

-
**Blog post: ADK Bidi-streaming Visual Guide**

A visual guide to real-time multimodal AI agent development with ADK Bidi-streaming. This article provides intuitive diagrams and illustrations to help you understand how Bidi-streaming works and how to build interactive AI agents.

-
**Bidi-streaming development guide series**

A series of articles for diving deeper into the Bidi-streaming development with ADK. You can learn basic concepts and use cases, the core API, and end-to-end application design.

[Part 1: Introduction to ADK Bidi-streaming](dev-guide/part1/)- Fundamentals of Bidi-streaming, Live API technology, ADK architecture components, and complete application lifecycle with FastAPI examples[Part 2: Sending messages with LiveRequestQueue](dev-guide/part2/)- Upstream message flow, sending text/audio/video, activity signals, and concurrency patterns[Part 3: Event handling with run_live()](dev-guide/part3/)- Processing events, handling text/audio/transcriptions, automatic tool execution, and multi-agent workflows[Part 4: Understanding RunConfig](dev-guide/part4/)- Response modalities, streaming modes, session management, session resumption, context window compression, and quota management[Part 5: How to Use Audio, Image and Video](dev-guide/part5/)- Audio specifications, model architectures, audio transcription, voice activity detection, and proactive/affective dialog features

-
**Streaming Tools**

Streaming tools allow tools (functions) to stream intermediate results back to agents and agents can respond to those intermediate results. For example, we can use streaming tools to monitor the changes of the stock price and have the agent react to it. Another example is we can have the agent monitor the video stream, and when there are changes in video stream, the agent can report the changes.

-
**Blog post: Google ADK + Vertex AI Live API**

This article shows how to use Bidi-streaming (live) in ADK for real-time audio/video streaming. It offers a Python server example using LiveRequestQueue to build custom, interactive AI agents.

-
**Blog post: Supercharge ADK Development with Claude Code Skills**

This article demonstrates how to use Claude Code Skills to accelerate ADK development, with an example of building a Bidi-streaming chat app. Learn how to leverage AI-powered coding assistance to build better agents faster.