---
merged_at: 2026-01-28T07:23:42.230024
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/evaluate/user-sim/ -->

# User Simulation¶

# User Simulation[¶](#user-simulation)

When evaluating conversational agents, it is not always practical to use a fixed set of user prompts, as the conversation can proceed in unexpected ways. For example, if the agent needs the user to supply two values to perform a task, it may ask for those values one at a time or both at once. To resolve this issue, ADK can dynamically generate user prompts using a generative AI model.

To use this feature, you must specify a
[ ConversationScenario](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/conversation_scenarios.py)
which dictates the user's goals in their conversation with the agent.
A sample conversation scenario for the

[agent is shown below:](https://github.com/google/adk-python/tree/main/contributing/samples/hello_world)

`hello_world`

{
"starting_prompt": "What can you do for me?",
"conversation_plan": "Ask the agent to roll a 20-sided die. After you get the result, ask the agent to check if it is prime."
}


The `starting_prompt`

in a conversation scenario specifies a fixed initial
prompt that the user should use to start the conversation with the agent.
Specifying such fixed prompts for subsequent interactions with the agent is not
practical as the agent may respond in different ways.
Instead, the `conversation_plan`

provides a guideline for how the rest of the
conversation with the agent should proceed.
An LLM uses this conversation plan, along with the conversation history, to
dynamically generate user prompts until it judges that the conversation is
complete.

Try it in Colab

Test this entire workflow yourself in an interactive notebook on
[Simulating User Conversations to Dynamically Evaluate ADK Agents](https://github.com/google/adk-samples/blob/main/python/notebooks/evaluation/user_simulation_in_adk_evals.ipynb).
You'll define a conversation scenario, run a "dry run" to check the
dialogue, and then perform a full evaluation to score the agent's responses.

## Example: Evaluating the `hello_world`

agent with conversation scenarios[¶](#example-evaluating-the-hello_world-agent-with-conversation-scenarios)

`hello_world`

To add evaluation cases containing conversation scenarios to a new or existing
[ EvalSet](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_set.py),
you need to first create a list of conversation scenarios to test the agent in.

Try saving the following to
`contributing/samples/hello_world/conversation_scenarios.json`

:

{
"scenarios": [
{
"starting_prompt": "What can you do for me?",
"conversation_plan": "Ask the agent to roll a 20-sided die. After you get the result, ask the agent to check if it is prime."
},
{
"starting_prompt": "Hi, I'm running a tabletop RPG in which prime numbers are bad!",
"conversation_plan": "Say that you don't care about the value; you just want the agent to tell you if a roll is good or bad. Once the agent agrees, ask it to roll a 6-sided die. Finally, ask the agent to do the same with 2 20-sided dice."
}
]
}


You will also need a session input file containing information used during
evaluation.
Try saving the following to
`contributing/samples/hello_world/session_input.json`

:

Then, you can add the conversation scenarios to an `EvalSet`

:

# (optional) create a new EvalSet
adk eval_set create \
contributing/samples/hello_world \
eval_set_with_scenarios
# add conversation scenarios to the EvalSet as new eval cases
adk eval_set add_eval_case \
contributing/samples/hello_world \
eval_set_with_scenarios \
--scenarios_file contributing/samples/hello_world/conversation_scenarios.json \
--session_input_file contributing/samples/hello_world/session_input.json


By default, ADK runs evaluations with metrics that require the agent's expected
response to be specified.
Since that is not the case for a dynamic conversation scenario, we will use an
[ EvalConfig](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_config.py)
with some alternate supported metrics.

Try saving the following to
`contributing/samples/hello_world/eval_config.json`

:

{
"criteria": {
"hallucinations_v1": {
"threshold": 0.5,
"evaluate_intermediate_nl_responses": true
},
"safety_v1": {
"threshold": 0.8
}
}
}


Finally, you can use the `adk eval`

command to run the evaluation:

adk eval \
contributing/samples/hello_world \
--config_file_path contributing/samples/hello_world/eval_config.json \
eval_set_with_scenarios \
--print_detailed_results


## User simulator configuration[¶](#user-simulator-configuration)

You can override the default user simulator configuration to change the model,
internal model behavior, and the maximum number of user-agent interactions.
The below `EvalConfig`

shows the default user simulator configuration:

{
"criteria": {
# same as before
},
"user_simulator_config": {
"model": "gemini-2.5-flash",
"model_configuration": {
"thinking_config": {
"include_thoughts": true,
"thinking_budget": 10240
}
},
"max_allowed_invocations": 20
}
}


`model`

: The model backing the user simulator.`model_configuration`

: Awhich controls the model behavior.`GenerateContentConfig`

`max_allowed_invocations`

: The maximum user-agent interactions allowed before the conversation is forcefully terminated. This should be set to be greater than the longest reasonable user-agent interaction in your`EvalSet`

.

---
<!-- Source: https://google.github.io/adk-docs/streaming/streaming-tools/ -->

# Streaming Tools¶

# Streaming Tools[¶](#streaming-tools)

Streaming tools allows tools(functions) to stream intermediate results back to agents and agents can respond to those intermediate results. For example, we can use streaming tools to monitor the changes of the stock price and have the agent react to it. Another example is we can have the agent monitor the video stream, and when there is changes in video stream, the agent can report the changes.

Info

This is only supported in streaming(live) agents/api.

To define a streaming tool, you must adhere to the following:

**Asynchronous Function:**The tool must be an`async`

Python function.**AsyncGenerator Return Type:**The function must be typed to return an`AsyncGenerator`

. The first type parameter to`AsyncGenerator`

is the type of the data you`yield`

(e.g.,`str`

for text messages, or a custom object for structured data). The second type parameter is typically`None`

if the generator doesn't receive values via`send()`

.

We support two types of streaming tools: - Simple type. This is a one type of streaming tools that only take non-video/-audio streams(the streams that you feed to adk web or adk runner) as input. - Video streaming tools. This only works in video streaming and the video stream(the streams that you feed to adk web or adk runner) will be passed into this function.

Now let's define an agent that can monitor stock price changes and monitor the video stream changes.

import asyncio
from typing import AsyncGenerator
from google.adk.agents import LiveRequestQueue
from google.adk.agents.llm_agent import Agent
from google.adk.tools.function_tool import FunctionTool
from google.genai import Client
from google.genai import types as genai_types
async def monitor_stock_price(stock_symbol: str) -> AsyncGenerator[str, None]:
"""This function will monitor the price for the given stock_symbol in a continuous, streaming and asynchronously way."""
print(f"Start monitor stock price for {stock_symbol}!")
# Let's mock stock price change.
await asyncio.sleep(4)
price_alert1 = f"the price for {stock_symbol} is 300"
yield price_alert1
print(price_alert1)
await asyncio.sleep(4)
price_alert1 = f"the price for {stock_symbol} is 400"
yield price_alert1
print(price_alert1)
await asyncio.sleep(20)
price_alert1 = f"the price for {stock_symbol} is 900"
yield price_alert1
print(price_alert1)
await asyncio.sleep(20)
price_alert1 = f"the price for {stock_symbol} is 500"
yield price_alert1
print(price_alert1)
# for video streaming, `input_stream: LiveRequestQueue` is required and reserved key parameter for ADK to pass the video streams in.
async def monitor_video_stream(
input_stream: LiveRequestQueue,
) -> AsyncGenerator[str, None]:
"""Monitor how many people are in the video streams."""
print("start monitor_video_stream!")
client = Client(vertexai=False)
prompt_text = (
"Count the number of people in this image. Just respond with a numeric"
" number."
)
last_count = None
while True:
last_valid_req = None
print("Start monitoring loop")
# use this loop to pull the latest images and discard the old ones
while input_stream._queue.qsize() != 0:
live_req = await input_stream.get()
if live_req.blob is not None and live_req.blob.mime_type == "image/jpeg":
last_valid_req = live_req
# If we found a valid image, process it
if last_valid_req is not None:
print("Processing the most recent frame from the queue")
# Create an image part using the blob's data and mime type
image_part = genai_types.Part.from_bytes(
data=last_valid_req.blob.data, mime_type=last_valid_req.blob.mime_type
)
contents = genai_types.Content(
role="user",
parts=[image_part, genai_types.Part.from_text(prompt_text)],
)
# Call the model to generate content based on the provided image and prompt
response = client.models.generate_content(
model="gemini-2.0-flash-exp",
contents=contents,
config=genai_types.GenerateContentConfig(
system_instruction=(
"You are a helpful video analysis assistant. You can count"
" the number of people in this image or video. Just respond"
" with a numeric number."
)
),
)
if not last_count:
last_count = response.candidates[0].content.parts[0].text
elif last_count != response.candidates[0].content.parts[0].text:
last_count = response.candidates[0].content.parts[0].text
yield response
print("response:", response)
# Wait before checking for new images
await asyncio.sleep(0.5)
# Use this exact function to help ADK stop your streaming tools when requested.
# for example, if we want to stop `monitor_stock_price`, then the agent will
# invoke this function with stop_streaming(function_name=monitor_stock_price).
def stop_streaming(function_name: str):
"""Stop the streaming
Args:
function_name: The name of the streaming function to stop.
"""
pass
root_agent = Agent(
model="gemini-2.0-flash-exp",
name="video_streaming_agent",
instruction="""
You are a monitoring agent. You can do video monitoring and stock price monitoring
using the provided tools/functions.
When users want to monitor a video stream,
You can use monitor_video_stream function to do that. When monitor_video_stream
returns the alert, you should tell the users.
When users want to monitor a stock price, you can use monitor_stock_price.
Don't ask too many questions. Don't be too talkative.
""",
tools=[
monitor_video_stream,
monitor_stock_price,
FunctionTool(stop_streaming),
]
)


Here are some sample queries to test: - Help me monitor the stock price for $XYZ stock. - Help me monitor how many people are there in the video stream.

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/community/ -->

# Community Resources¶

# Community Resources[¶](#community-resources)

Welcome! This page highlights resources built and maintained by the Agent Development Kit community.

Info

Google and the ADK team do not provide support for the content linked in these external community resources.

## Getting Started[¶](#getting-started)

[
Video Demo
](https://www.youtube.com/watch?v=zgrOwow_uTQ)

### 📺 Introducing Agent Development Kit

A demo of building a multi-agent travel planner, showcasing core design principles.

[
Video
](https://www.youtube.com/watch?v=44C8u0CDtSo)

### 📺 Getting started with Agent Development Kit

Learn the fundamentals of agent definition and how to run and debug your first agent.

[
Video
](https://www.youtube.com/watch?v=5ZmaWY7UX6k)

### 📺 Getting Started with ADK Tools

A guide to building a software bug assistant using tools like MCP and Google Search.

## ADK Community Calls[¶](#adk-community-calls)

Stay Connected

Join the [ADK Community Google Group](https://groups.google.com/g/adk-community) for updates, calendar invites, and to connect with the ADK community.

[
Community Call
](https://www.youtube.com/watch?v=cNVWhrbdn-E)

### 📞 ADK Community Call (Dec 2025)

Discussions include the ADK TypeScript launch, Gemini 3 Flash support, bidirectional streaming for voice agents, and the Visual Builder UI.

[
Community Call
](https://www.youtube.com/watch?v=bftUz-WBqyw)

### 📞 ADK Community Call (Nov 2025)

Discussions include the ADK Go launch, the reflect & retry plugin for error recovery, and time travel debugging for rewinding agent sessions.

[
Community Call
](https://www.youtube.com/watch?v=A95mQaSRKik)

### 📞 ADK Community Call (Oct 2025)

Discussions include the ADK roadmap, context compaction and caching for reducing cost and latency, and community contribution guidelines.

## Courses & Deep Dives[¶](#courses-deep-dives)

[
Online Course
](https://www.kaggle.com/learn-guide/5-day-agents)

### 🎓 5-Day AI Agents Intensive Course with Google

Build with core ADK agent components including, models, tools, memory, evaluation, and deployment.

[
Video Course
](https://www.youtube.com/watch?v=P4VFL9nIaIA)

### 🎓 ADK Masterclass: Build AI Agents & Automate Workflows

A complete crash course that takes you from beginner to expert with 12 hands-on examples.

[
Website
](https://raphaelmansuy.github.io/adk_training/)

### 🎓 ADK Training Hub

Master ADK from first principles to production with comprehensive tutorials and examples.

[
YouTube Playlist
](https://www.youtube.com/playlist?list=PLLrA_pU9-Gz2HwepRUVpq1TEPuYWo_fSi)

### 🎓 Master Agentic AI with ADK

A step-by-step playlist covering everything from setup to deploying and scaling agents.

[
YouTube Playlist
](https://www.youtube.com/playlist?list=PL6tW9BrhiPTAZts0W5nQS9dbW6VMnLKab)

### 🎓 Google ADK End-to-end Course

Build, deploy, and scale production-ready agents with this in-depth course series.

[
Blog Series
](https://iamulya.one/tags/building-intelligent-agents-with-google-adk/)

### 🎓 Building Intelligent Agents with Google ADK

A developer's guide to building intelligent agents with Google's code-first Python toolkit.

[
Online Course
](https://github.com/arjunprabhulal/google-adk-masterclass)

### 🎓 Google ADK Masterclass: Hands-on Series

Build production-ready AI agents with 20 modules covering agents, workflows, tools, memory, and MCP integrations.

[
YouTube Playlist
](https://www.youtube.com/playlist?list=PL0Zc2RFDZsM_MkHOzWNJpaT4EH5fQxA8n)

### 📻️ ADK News - ADK Podcast in Japanese

An auto-generated Japanese podcast about ADK, created by an ADK agent that covers commit logs, release notes, and blog posts.

## Agent Tutorials and Demos[¶](#agent-tutorials-and-demos)

[
Video Tutorial
](https://www.youtube.com/watch?v=efcUXoMX818)

### 📖 How to Build a Data Science Agent with ADK

A deep dive into building a multi-agent system for database queries, Python analysis, and BigQuery ML.

[
Video Tutorial
](https://www.youtube.com/watch?v=hPzjkQFV5yI)

### 📖 Build a Browser Use Agent with ADK and Selenium

Learn to build an agent that enhances a retail website's product data by filling in missing information.

[
Jupyter Notebook
](https://github.com/google/adk-docs/blob/main/examples/python/notebooks/shop_agent.ipynb)

### 📖 Build an E-commerce Recommendation Agent

A tutorial on creating a simple multi-agent system for generative e-commerce recommendations.

[
Blog Post
](https://medium.com/google-cloud/google-adk-vertex-ai-live-api-125238982d5e)

### 📖 Google ADK + Vertex AI Live API

Go beyond the ADK CLI by building real-time, streaming experiences with the Live API.

[
Video Demo
](https://www.youtube.com/watch?v=LwHPYyw7u6U)

### 📺 Shopper's Concierge Demo

See how AI agents can revolutionize shopping with personalized, real-time recommendations.

[
Gallery
](https://agentdirectory.folch.ai/)

### 📖 ADK Agent Directory

Discover and test production-ready ADK agents for web search, image generation, research, and more.

## ADK for Java[¶](#adk-for-java)

[
Video Talk
](https://www.youtube.com/watch?v=L6V6aQixOZU)

### ☕ Discover ADK Java for Building AI Agents

A presentation to help you build your first AI agents in Java.

[
YouTube Playlist
](https://www.youtube.com/playlist?list=PLLMxXO6kMiNhP87WYQ8CeC3xpV3EnF9cu)

### ☕ Google ADK for Java Tutorials

Step-by-step tutorials covering A2A, MCP, multi-agent systems, and callbacks in Java.

[
Codelab
](https://codelabs.developers.google.com/adk-java-getting-started)

### ☕ Build AI Agents with ADK for Java

Move beyond simple LLM calls to create autonomous Java agents that reason, plan, and use tools.

## Translations[¶](#translations)

Community-provided translations of the ADK documentation.

## Contributing Your Resource[¶](#contributing-your-resource)

Have an ADK resource to share (tutorial, translation, tool, video, or example)?

Refer to the steps in the ** Contributing Guide** for more information on how to get involved!

Thank you for your contributions to Agent Development Kit! ❤️

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/plugins/reflect-and-retry/ -->

# Reflect and Retry Tool Plugin¶

# Reflect and Retry Tool Plugin[¶](#reflect-and-retry-tool-plugin)

The Reflect and Retry Tool plugin can help your agent recover from error
responses from ADK [Tools](/adk-docs/tools-custom/) and automatically retry the
tool request. This plugin intercepts tool failures, provides structured guidance
to the AI model for reflection and correction, and retries the operation up to a
configurable limit. This plugin can help you build more resilience into your
agent workflows, including the following capabilities:

**Concurrency safe**: Uses locking to safely handle parallel tool executions.**Configurable scope**: Tracks failures per-invocation (default) or globally.**Granular tracking**: Failure counts are tracked per-tool.**Custom error extraction**: Supports detecting errors in normal tool responses.

## Add Reflect and Retry Plugin[¶](#add-reflect-and-retry-plugin)

Add this plugin to your ADK workflow by adding it to the plugins setting of your ADK project's App object, as shown below:

from google.adk.apps.app import App
from google.adk.plugins import ReflectAndRetryToolPlugin
app = App(
name="my_app",
root_agent=root_agent,
plugins=[
ReflectAndRetryToolPlugin(max_retries=3),
],
)


With this configuration, if any tool called by an agent returns an error, the request is updated and tried again, up to a maximum of 3 attempts, per tool.

## Configuration settings[¶](#configuration-settings)

The Reflect and Retry Plugin has the following configuration options:

: (optional) Total number of additional attempts the system makes to receive a non-error response. Default value is 3.`max_retries`

: (optional) If set to`throw_exception_if_retry_exceeded`

`False`

, the system does not raise an error if the final retry attempt fails. Default value is`True`

.: (optional)`tracking_scope`

: Track tool failures across a single invocation and user. This value is the default.`TrackingScope.INVOCATION`

: Track tool failures across all invocations and all users.`TrackingScope.GLOBAL`


### Advanced configuration[¶](#advanced-configuration)

You can further modify the behavior of this plugin by extending the
`ReflectAndRetryToolPlugin`

class. The following code sample
demonstrates a simple extension of the behavior by selecting
responses with an error status:

class CustomRetryPlugin(ReflectAndRetryToolPlugin):
async def extract_error_from_result(self, *, tool, tool_args,tool_context,
result):
# Detect error based on response content
if result.get('status') == 'error':
return result
return None # No error detected
# add this modified plugin to your App object:
error_handling_plugin = CustomRetryPlugin(max_retries=5)


## Next steps[¶](#next-steps)

For complete code samples using the Reflect and Retry plugin, see the following:

[Basic](https://github.com/google/adk-python/tree/main/contributing/samples/plugin_reflect_tool_retry/basic)code sample[Hallucinating function name](https://github.com/google/adk-python/tree/main/contributing/samples/plugin_reflect_tool_retry/hallucinating_func_name)code sample

---
<!-- Source: https://google.github.io/adk-docs/streaming/ -->

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
