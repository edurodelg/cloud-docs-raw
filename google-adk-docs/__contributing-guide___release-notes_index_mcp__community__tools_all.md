---
merged_at: 2026-02-09T09:31:35.619341
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/contributing-guide/ -->

# Contributing Guide

Thank you for your interest in contributing to Agent Development Kit (ADK)! We welcome contributions to the core frameworks, documentation, and related components, which are listed below.

This guide provides information on how to get involved.

## Preparing to contribute[¶](#preparing-to-contribute)

### Choose the right repository[¶](#choose-the-right-repository)

The ADK project is split across several repositories. Find the right one for your contribution:

| Repository | Description | Detailed Guide |
|---|---|---|
`google/adk-python` |

`CONTRIBUTING.md`

`google/adk-python-community`

`CONTRIBUTING.md`

`google/adk-js`

`CONTRIBUTING.md`

`google/adk-go`

`CONTRIBUTING.md`

`google/adk-java`

`CONTRIBUTING.md`

`google/adk-docs`

`CONTRIBUTING.md`

`google/adk-samples`

`CONTRIBUTING.md`

`google/adk-web`

`adk web`

dev UIThese repositories typically include a `CONTRIBUTING.md`

file in the root of
their repository with more detailed information on requirements, testing, code
review processes, etc. for that particular component.

### Sign a CLA[¶](#sign-a-cla)

Contributions to this project must be accompanied by a
[Contributor License Agreement](https://cla.developers.google.com/about) (CLA).
You (or your employer) retain the copyright to your contribution; this simply
gives us permission to use and redistribute your contributions as part of the
project.

If you or your current employer have already signed the Google CLA (even if it was for a different project), you probably don't need to do it again.

Visit [https://cla.developers.google.com/](https://cla.developers.google.com/) to see your current agreements or to
sign a new one.

### Review community guidelines[¶](#review-community-guidelines)

This project follows
[Google's Open Source Community Guidelines](https://opensource.google/conduct/).

## Join the discussion[¶](#join-the-discussion)

Have questions, want to share ideas, or discuss how you're using ADK? Head over
to our ** Python**,

**,**

[TypeScript](https://github.com/google/adk-js/discussions)**, or**

[Go](https://github.com/google/adk-go/discussions)**Discussions!**

[Java](https://github.com/google/adk-java/discussions)This is the primary place for:

- Asking questions and getting help from the community and maintainers.
- Sharing your projects or use cases (
`Show and Tell`

). - Discussing potential features or improvements before creating a formal issue.
- General conversation about ADK.

## How to contribute[¶](#how-to-contribute)

There are several ways you can contribute to ADK:

### Reporting issues[¶](#reporting-issues-bugs-errors)

If you find a bug in the framework or an error in the documentation:

**Framework Bugs:**Open an issue in,`google/adk-python`

,`google/adk-js`

, or`google/adk-go`

`google/adk-java`

**Documentation Errors:**[Open an issue in](https://github.com/google/adk-docs/issues/new?template=bug_report.md)`google/adk-docs`

(use bug template)

### Suggesting enhancements[¶](#suggesting-enhancements)

Have an idea for a new feature or an improvement to an existing one?

**Framework Enhancements:**Open an issue in,`google/adk-python`

,`google/adk-js`

, or`google/adk-go`

`google/adk-java`

**Documentation Enhancements:**[Open an issue in](https://github.com/google/adk-docs/issues/new)`google/adk-docs`


### Improving documentation[¶](#improving-documentation)

Found a typo, unclear explanation, or missing information? Submit your changes directly:

**How:**Submit a Pull Request (PR) with your suggested improvements.**Where:**[Create a Pull Request in](https://github.com/google/adk-docs/pulls)`google/adk-docs`


### Writing code[¶](#writing-code)

Help fix bugs, implement new features or contribute code samples for the documentation:

**How:** Submit a Pull Request (PR) with your code changes.

**Python Framework:**[Create a Pull Request in](https://github.com/google/adk-python/pulls)`google/adk-python`

**TypeScript Framework:**[Create a Pull Request in](https://github.com/google/adk-js/pulls)`google/adk-js`

**Go Framework:**[Create a Pull Request in](https://github.com/google/adk-go/pulls)`google/adk-go`

**Java Framework:**[Create a Pull Request in](https://github.com/google/adk-java/pulls)`google/adk-java`

**Documentation:**[Create a Pull Request in](https://github.com/google/adk-docs/pulls)`google/adk-docs`


### Code reviews[¶](#code-reviews)

-
All contributions, including those from project members, undergo a review process.

-
We use GitHub Pull Requests (PRs) for code submission and review. Please ensure your PR clearly describes the changes you are making.


## License[¶](#license)

By contributing, you agree that your contributions will be licensed under the
project's
[Apache 2.0 License](https://github.com/google/adk-docs/blob/main/LICENSE).

## Questions?[¶](#questions)

If you get stuck or have questions, feel free to open an issue on the relevant repository's issue tracker.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/release-notes/ -->

# ADK release notes¶

# ADK release notes[¶](#adk-release-notes)

You can find the release notes in the code repositories for each supported language. For detailed information on ADK releases, see these locations:

You can find the release notes in the code repositories for each supported language. For detailed information on ADK releases, see these locations:

---
<!-- Source: https://google.github.io/adk-docs/ -->

# Agent Development Kit

Agent Development Kit (ADK) is a flexible and modular framework for **developing
and deploying AI agents**. While optimized for Gemini and the Google ecosystem,
ADK is **model-agnostic**, **deployment-agnostic**, and is built for
**compatibility with other frameworks**. ADK was designed to make agent
development feel more like software development, to make it easier for
developers to create, deploy, and orchestrate agentic architectures that range
from simple tasks to complex workflows.

Get started:

[Start with Python](/adk-docs/get-started/python/)
[Start with TypeScript](/adk-docs/get-started/typescript/)
[Start with Go](/adk-docs/get-started/go/)
[Start with Java](/adk-docs/get-started/java/)

## Learn more[¶](#learn-more)

[ Watch "Introducing Agent Development Kit"!](https://www.youtube.com/watch?v=zgrOwow_uTQ)

-
**Flexible Orchestration**

Define workflows using workflow agents (

`Sequential`

,`Parallel`

,`Loop`

) for predictable pipelines, or leverage LLM-driven dynamic routing (`LlmAgent`

transfer) for adaptive behavior. -
**Multi-Agent Architecture**

Build modular and scalable applications by composing multiple specialized agents in a hierarchy. Enable complex coordination and delegation.

-
**Rich Tool Ecosystem**

Equip agents with diverse capabilities: use pre-built tools (Search, Code Exec), create custom functions, integrate 3rd-party libraries, or even use other agents as tools.

-
**Deployment Ready**

Containerize and deploy your agents anywhere – run locally, scale with Vertex AI Agent Engine, or integrate into custom infrastructure using Cloud Run or Docker.

-
**Built-in Evaluation**

Systematically assess agent performance by evaluating both the final response quality and the step-by-step execution trajectory against predefined test cases.

-
**Building Safe and Secure Agents**

Learn how to building powerful and trustworthy agents by implementing security and safety patterns and best practices into your agent's design.

---
<!-- Source: https://google.github.io/adk-docs/mcp/ -->

# Model Context Protocol (MCP)¶

# Model Context Protocol (MCP)[¶](#model-context-protocol-mcp)

The
[Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction) is
an open standard designed to standardize how Large Language Models (LLMs) like
Gemini and Claude communicate with external applications, data sources, and
tools. Think of it as a universal connection mechanism that simplifies how LLMs
obtain context, execute actions, and interact with various systems.

## How does MCP work?[¶](#how-does-mcp-work)

MCP follows a client-server architecture, defining how data (resources), interactive templates (prompts), and actionable functions (tools) are exposed by an MCP server and consumed by an MCP client (which could be an LLM host application or an AI agent).

## MCP Tools in ADK[¶](#mcp-tools-in-adk)

ADK helps you both use and consume MCP tools in your agents, whether you're trying to build a tool to call an MCP service, or exposing an MCP server for other developers or agents to interact with your tools.

See [Tools and Integrations](/adk-docs/integrations/) for pre-built
MCP tools you can use in your agents. Refer to the
[MCP Tools documentation](/adk-docs/tools-custom/mcp-tools/) for code samples
and design patterns that help you use ADK together with MCP servers, including:

**Using Existing MCP Servers within ADK**: An ADK agent can act as an MCP client and use tools provided by external MCP servers.**Exposing ADK Tools via an MCP Server**: How to build an MCP server that wraps ADK tools, making them accessible to any MCP client.

## ADK Agent and FastMCP server[¶](#adk-agent-and-fastmcp-server)

ADK uses [FastMCP](https://github.com/jlowin/fastmcp) to handle all the
complex MCP protocol details and server management, so you can focus on
building great tools. It's designed to be high-level and Pythonic; in most
cases, decorating a function is all you need.

Refer to the [MCP Tools](/adk-docs/tools-custom/mcp-tools/) documentation on
how you can use ADK together with the FastMCP server running on Cloud Run.

## MCP Servers for Google Cloud Genmedia[¶](#mcp-servers-for-google-cloud-genmedia)

[MCP Tools for Genmedia Services](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
is a set of open-source MCP servers that enable you to integrate Google Cloud
generative media services—such as Imagen, Veo, Chirp 3 HD voices, and Lyria—into
your AI applications.

Agent Development Kit (ADK) and [Genkit](https://genkit.dev/) provide built-in
support for these MCP tools, allowing your AI agents to effectively orchestrate
generative media workflows. For implementation guidance, refer to the [ADK
example
agent](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia/sample-agents/adk)
and the
[Genkit example](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia/sample-agents/genkit).

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

See recent recordings below, or browse all past calls on our [YouTube playlist](https://www.youtube.com/playlist?list=PLwi6PfxEP7zZbBPmWiZ8QbPcuKyAY5RR3).

[
Community Call
](https://www.youtube.com/watch?v=h9Lueiqo89E)

### 📞 Jan 2026 Recording

Discussions include Session Service schema for cross-language support, TypeScript multi-agent demo, API Registry for MCP servers, and third-party tool integrations.

[
Community Call
](https://www.youtube.com/watch?v=cNVWhrbdn-E)

### 📞 Dec 2025 Recording

Discussions include the ADK TypeScript launch, Gemini 3 Flash support, bidirectional streaming for voice agents, and the Visual Builder UI.

[
Community Call
](https://www.youtube.com/watch?v=bftUz-WBqyw)

### 📞 Nov 2025 Recording

Discussions include the ADK Go launch, the reflect & retry plugin for error recovery, and time travel debugging for rewinding agent sessions.

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
<!-- Source: https://google.github.io/adk-docs/tools/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/performance/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/built-in-tools/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/function-tools/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/authentication/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/express-mode/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/google-cloud/vertex-ai-search/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/tools/gemini-api/computer-use/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/gemini-api/google-search/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/gemini-api/code-execution/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/tools/limitations/ -->

# Limitations for ADK tools¶

# Limitations for ADK tools[¶](#limitations-for-adk-tools)

Some ADK tools have limitations that can impact how you implement them within an agent workflow. This page lists these tool limitations and workarounds, if available.

## One tool per agent limitation[¶](#one-tool-one-agent)

ONLY for Search in ADK Python v1.15.0 and lower

This limitation only applies to the use of Google Search and Vertex AI Search tools in ADK Python v1.15.0 and lower. ADK Python release v1.16.0 and higher provides a built-in workaround to remove this limitation.

In general, you can use more than one tool in an agent, but use of specific tools within an agent excludes the use of any other tools in that agent. The following ADK Tools can only be used by themselves, without any other tools, in a single agent object:

[Code Execution](/adk-docs/tools/gemini-api/code-execution/)with Gemini API[Google Search](/adk-docs/tools/gemini-api/google-search/)with Gemini API[Vertex AI Search](/adk-docs/tools/google-cloud/vertex-ai-search/)

For example, the following approach that uses one of these tools along with
other tools, within a single agent, is ** not supported**:

### Workaround #1: AgentTool.create() method[¶](#workaround-1-agenttoolcreate-method)

The following code sample demonstrates how to use multiple built-in tools or how to use built-in tools with other tools by using multiple agents:

from google.adk.tools.agent_tool import AgentTool
from google.adk.agents import Agent
from google.adk.tools import google_search
from google.adk.code_executors import BuiltInCodeExecutor
search_agent = Agent(
model='gemini-2.0-flash',
name='SearchAgent',
instruction="""
You're a specialist in Google Search
""",
tools=[google_search],
)
coding_agent = Agent(
model='gemini-2.0-flash',
name='CodeAgent',
instruction="""
You're a specialist in Code Execution
""",
code_executor=BuiltInCodeExecutor(),
)
root_agent = Agent(
name="RootAgent",
model="gemini-2.0-flash",
description="Root Agent",
tools=[AgentTool(agent=search_agent), AgentTool(agent=coding_agent)],
)


import com.google.adk.agents.BaseAgent;
import com.google.adk.agents.LlmAgent;
import com.google.adk.tools.AgentTool;
import com.google.adk.tools.BuiltInCodeExecutionTool;
import com.google.adk.tools.GoogleSearchTool;
import com.google.common.collect.ImmutableList;
public class NestedAgentApp {
private static final String MODEL_ID = "gemini-2.0-flash";
public static void main(String[] args) {
// Define the SearchAgent
LlmAgent searchAgent =
LlmAgent.builder()
.model(MODEL_ID)
.name("SearchAgent")
.instruction("You're a specialist in Google Search")
.tools(new GoogleSearchTool()) // Instantiate GoogleSearchTool
.build();
// Define the CodingAgent
LlmAgent codingAgent =
LlmAgent.builder()
.model(MODEL_ID)
.name("CodeAgent")
.instruction("You're a specialist in Code Execution")
.tools(new BuiltInCodeExecutionTool()) // Instantiate BuiltInCodeExecutionTool
.build();
// Define the RootAgent, which uses AgentTool.create() to wrap SearchAgent and CodingAgent
BaseAgent rootAgent =
LlmAgent.builder()
.name("RootAgent")
.model(MODEL_ID)
.description("Root Agent")
.tools(
AgentTool.create(searchAgent), // Use create method
AgentTool.create(codingAgent) // Use create method
)
.build();
// Note: This sample only demonstrates the agent definitions.
// To run these agents, you'd need to integrate them with a Runner and SessionService,
// similar to the previous examples.
System.out.println("Agents defined successfully:");
System.out.println(" Root Agent: " + rootAgent.name());
System.out.println(" Search Agent (nested): " + searchAgent.name());
System.out.println(" Code Agent (nested): " + codingAgent.name());
}
}


### Workaround #2: bypass_multi_tools_limit[¶](#workaround-2-bypass_multi_tools_limit)

ADK Python has a built-in workaround which bypasses this limitation for
`GoogleSearchTool`

and `VertexAiSearchTool`

(use `bypass_multi_tools_limit=True`

to enable it),
as shown in the
[built_in_multi_tools](https://github.com/google/adk-python/tree/main/contributing/samples/built_in_multi_tools).
sample agent.

Warning

Built-in tools cannot be used within a sub-agent, with the exception of
`GoogleSearchTool`

and `VertexAiSearchTool`

in ADK Python because of the
workaround mentioned above.

For example, the following approach that uses built-in tools within sub-agents
is **not supported**:

url_context_agent = Agent(
model='gemini-2.5-flash',
name='UrlContextAgent',
instruction="""
You're a specialist in URL Context
""",
tools=[url_context],
)
coding_agent = Agent(
model='gemini-2.5-flash',
name='CodeAgent',
instruction="""
You're a specialist in Code Execution
""",
code_executor=BuiltInCodeExecutor(),
)
root_agent = Agent(
name="RootAgent",
model="gemini-2.5-flash",
description="Root Agent",
sub_agents=[
url_context_agent,
coding_agent
],
)


LlmAgent searchAgent =
LlmAgent.builder()
.model("gemini-2.5-flash")
.name("SearchAgent")
.instruction("You're a specialist in Google Search")
.tools(new GoogleSearchTool())
.build();
LlmAgent codingAgent =
LlmAgent.builder()
.model("gemini-2.5-flash")
.name("CodeAgent")
.instruction("You're a specialist in Code Execution")
.tools(new BuiltInCodeExecutionTool())
.build();
LlmAgent rootAgent =
LlmAgent.builder()
.name("RootAgent")
.model("gemini-2.5-flash")
.description("Root Agent")
.subAgents(searchAgent, codingAgent) // Not supported, as the sub agents use built in tools.
.build();
