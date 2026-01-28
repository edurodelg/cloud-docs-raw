---
merged_at: 2026-01-28T07:23:42.229385
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/visual-builder/ -->

# Visual Builder for agents¶

# Visual Builder for agents[¶](#visual-builder-for-agents)

The ADK Visual Builder is a web-based tool that provides a visual workflow design environment for creating and managing ADK agents. It allows you to design, build, and test your agents in a beginner-friendly graphical interface, and includes an AI-powered assistant to help you build agents.

Experimental

The Visual Builder feature is an experimental release. We welcome your
[feedback](https://github.com/google/adk-python/issues/new?template=feature_request.md)!

## Get started[¶](#get-started)

The Visual Builder interface is part of the ADK Web tool user interface.
Make sure you have ADK library
[installed](/adk-docs/get-started/installation/#python)
and then run the ADK Web user interface.

## Tip: Run from a code development directory

The Visual Builder tool writes project files to new subdirectories located in the directory where you run the ADK Web tool. Make sure you run this command from a developer directory location where you have write access.

**Figure 1:** ADK Web controls to start the Visual Builder tool.

To create an agent with Visual Builder:

- In top left of the page, select the
**+**(plus sign), as shown in*Figure 1*, to start creating an agent. - Type a name for your agent application and select
**Create**. - Edit your agent by doing any of the following:
- In the left panel, edit agent component values.
- In the central panel, add new agent components .
- In the right panel, use prompts to modify the agent or get help.

- In bottom left corner, select
**Save**to save your agent. - Interact with your new agent to test it.
- In top left of the page, select the pencil icon, as shown in
*Figure 1*, to continue editing your agent.

Here are few things to note when using Visual Builder:

**Create agent and save:**When creating an agent, make sure you select**Save**before exiting the editing interface, otherwise your new agent may not be editable.**Agent editing:**Edit (pencil icon) for agents is*only*available for agents created with Visual Builder**Add tools:**When adding existing custom Tools to a Visual Builder agent, specify a fully-qualified Python function name.

## Workflow component support[¶](#workflow-component-support)

The Visual Builder tool provides a drag-and-drop user interface for constructing agents, as well as an AI-powered development Assistant that can answer questions and edit your agent workflow. The tool supports all the essential components for building an ADK agent workflow, including:

**Agents****Root Agent**: The primary controlling agent for a workflow. All other agents in an ADK agent workflow are considered Sub Agents.An agent powered by a generative AI model.**LLM Agent:**A workflow agent that executes a series of sub-agents in a sequence.**Sequential Agent:**A workflow agent that repeatedly executes a sub-agent until a certain condition is met.**Loop Agent:**A workflow agent that executes multiple sub-agents concurrently.**Parallel Agent:**

**Tools**A limited set of ADK-provided tools can be added to agents.**Prebuilt tools:**You can build and add custom tools to your workflow.**Custom tools:**

**Components**A flow control component that lets you modify the behavior of agents at the start and end of agent workflow events.**Callbacks**


Some advanced ADK features are not supported by Visual Builder due to
limitations of the Agent Config feature. For more information, see the
Agent Config [Known limitations](/adk-docs/agents/config/#known-limitations).

## Project code output[¶](#project-code-output)

The Visual Builder tool generates code in the [Agent Config](/adk-docs/agents/config/)
format, using `.yaml`

configuration files for agents and Python code for custom
tools. These files are generated in a subfolder of the directory where you ran
the ADK Web interface. The following listing shows an example layout for a
DiceAgent project:

DiceAgent/
root_agent.yaml # main agent code
sub_agent_1.yaml # sub agents (if any)
tools/ # tools directory
__init__.py
dice_tool.py # tool code


Editing generated agents

You can edit the generated files in your development environment. However, some changes may not be compatible with Visual Builder.

## Next steps[¶](#next-steps)

Using the Visual Builder development Assistant, try building a new agent using this prompt:

Help me add a dice roll tool to my current agent.
Use the default model if you need to configure that.


Check out more information on the Agent Config code format used by Visual Builder and the available options:

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
<!-- Source: https://google.github.io/adk-docs/deploy/ -->

# Deploying Your Agent¶

# Deploying Your Agent[¶](#deploying-your-agent)

Once you've built and tested your agent using ADK, the next step is to deploy it so it can be accessed, queried, and used in production or integrated with other applications. Deployment moves your agent from your local development machine to a scalable and reliable environment.

## Deployment Options[¶](#deployment-options)

Your ADK agent can be deployed to a range of different environments based on your needs for production readiness or custom flexibility:

### Agent Engine in Vertex AI[¶](#agent-engine-in-vertex-ai)

[Agent Engine](agent-engine/) is a fully managed auto-scaling service on Google Cloud
specifically designed for deploying, managing, and scaling AI agents built with
frameworks such as ADK.

Learn more about [deploying your agent to Vertex AI Agent Engine](agent-engine/).

### Cloud Run[¶](#cloud-run)

[Cloud Run](https://cloud.google.com/run) is a managed auto-scaling compute platform on
Google Cloud that enables you to run your agent as a container-based
application.

Learn more about [deploying your agent to Cloud Run](cloud-run/).

### Google Kubernetes Engine (GKE)[¶](#google-kubernetes-engine-gke)

[Google Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine) is a managed
Kubernetes service of Google Cloud that allows you to run your agent in a containerized
environment. GKE is a good option if you need more control over the deployment as well as
for running Open Models.

Learn more about [deploying your agent to GKE](gke/).

### Other Container-friendly Infrastructure[¶](#other-container-friendly-infrastructure)

You can manually package your Agent into a container image and then run it in any environment that supports container images. For example you can run it locally in Docker or Podman. This is a good option if you prefer to run offline or disconnected, or otherwise in a system that has no connection to Google Cloud.

Follow the instructions for [deploying your agent to Cloud Run](cloud-run/#deployment-commands).
In the "Deployment Commands" section for gcloud CLI, you will find an example FastAPI entry point and
Dockerfile.

---
<!-- Source: https://google.github.io/adk-docs/context/caching/ -->

# Context caching with Gemini¶

# Context caching with Gemini[¶](#context-caching-with-gemini)

When working with agents to complete tasks, you may want to reuse extended instructions or large sets of data across multiple agent requests to a generative AI model. Resending this data for each agent request is slow, inefficient, and can be expensive. Using context caching features in generative AI models can significantly speed up responses and lower the number of tokens sent to the model for each request.

The ADK Context Caching feature allows you to cache request data with generative AI models that support it, including Gemini 2.0 and higher models. This document explains how to configure and use this feature.

## Configure context caching[¶](#configure-context-caching)

You configure the context caching feature at the ADK `App`

object level,
which wraps your agent. Use the `ContextCacheConfig`

class to configure
these settings, as shown in the following code sample:

from google.adk import Agent
from google.adk.apps.app import App
from google.adk.agents.context_cache_config import ContextCacheConfig
root_agent = Agent(
# configure an agent using Gemini 2.0 or higher
)
# Create the app with context caching configuration
app = App(
name='my-caching-agent-app',
root_agent=root_agent,
context_cache_config=ContextCacheConfig(
min_tokens=2048, # Minimum tokens to trigger caching
ttl_seconds=600, # Store for up to 10 minutes
cache_intervals=5, # Refresh after 5 uses
),
)


## Configuration settings[¶](#configuration-settings)

The `ContextCacheConfig`

class has the following settings that control how
caching works for your agent. When you configure these settings, they apply to
all agents within your app.

(int): The minimum number of tokens required in a request to enable caching. This setting allows you to avoid the overhead of caching for very small requests where the performance benefit would be negligible. Defaults to`min_tokens`

`0`

.(int): The time-to-live (TTL) for the cache in seconds. This setting determines how long the cached content is stored before it is refreshed. Defaults to`ttl_seconds`

`1800`

(30 minutes).(int): The maximum number of times the same cached content can be used before it expires. This setting allows you to control how frequently the cache is updated, even if the TTL has not expired. Defaults to`cache_intervals`

`10`

.

## Next steps[¶](#next-steps)

For a full implementation of how to use and test the context caching feature, see the following sample:

: A code sample that demonstrates how to analyze the performance of context caching.`cache_analysis`


If your use case requires that you provide instructions that are used throughout
a session, consider using the `static_instruction`

parameter for an agent, which
allows you to amend the system instructions for a generative model. For more
details, see this sample code:

: An implementation of a digital pet agent using static instructions.`static_instruction`

---
<!-- Source: https://google.github.io/adk-docs/tutorials/coding-with-ai/ -->

# Coding with AI¶

# Coding with AI[¶](#coding-with-ai)

The Agent Development Kit (ADK) documentation supports the
[ /llms.txt standard](https://llmstxt.org/), providing a machine-readable index
of the documentation optimized for Large Language Models (LLMs). This allows you
to easily use the ADK documentation as context in your AI-powered development
environment.

## What is llms.txt?[¶](#what-is-llmstxt)

`llms.txt`

is a standardized text file that acts as a map for LLMs, listing the
most important documentation pages and their descriptions. This helps AI tools
understand the structure of the ADK documentation and retrieve relevant
information to answer your questions.

The ADK documentation provides the following files that are automatically generated with every update:

| File | Best For... | URL |
|---|---|---|
`llms.txt` |
Tools that can fetch links dynamically |
`https://google.github.io/adk-docs/llms.txt` |

`llms-full.txt`

`https://google.github.io/adk-docs/llms-full.txt`

## Usage in Development Tools[¶](#usage-in-development-tools)

You can use these files to power your AI coding assistants with ADK knowledge. This functionality allows your agents to autonomously search and read the ADK documentation while planning tasks and generating code.

### Gemini CLI[¶](#gemini-cli)

The [Gemini CLI](https://geminicli.com/) can be configured to query the ADK
documentation using the
[ADK Docs Extension](https://github.com/derailed-dash/adk-docs-ext).

**Installation:**

To install the extension, run the following command:

**Usage:**

Once installed, the extension is automatically enabled. You can ask questions
about ADK directly in the Gemini CLI, and it will use the `llms.txt`

file and
ADK documentation to provide accurate answers and generate code.

For example, you can ask the following question from within Gemini CLI:

How do I create a function tool using Agent Development Kit?


### Antigravity[¶](#antigravity)

The [Antigravity](https://antigravity.google/) IDE can be configured to access
the ADK documentation by running a custom MCP server that points to the
`llms.txt`

file for ADK.

**Prerequisites:**

Ensure you have the [ uv](https://docs.astral.sh/uv/) tool installed, as this
configuration uses

`uvx`

to run the documentation server without manual
installation.**Configuration:**

- Open the MCP store via the
**...**(more) menu at the top of the editor's agent panel. - Click on
**Manage MCP Servers**. - Click on
**View raw config**. -
Add the following entry to

`mcp_config.json`

with your custom MCP server configuration. If this is your first MCP server, you can paste the entire code block:

Refer to the
[Antigravity MCP documentation](https://antigravity.google/docs/mcp) for more
information on managing MCP servers.

**Usage:**

Once configured, you can prompt the coding agent with instructions like:

Use the ADK docs to build a multi-tool agent that uses Gemini 2.5 Pro and includes a mock weather lookup tool and a custom calculator tool. Verify the agent using

`adk run`

.

### Claude Code[¶](#claude-code)

[Claude Code](https://code.claude.com/docs/en/overview) can be configured to
query the ADK documentation by adding an
[MCP server](https://code.claude.com/docs/en/mcp).

**Installation:**

To add an MCP server for the ADK docs to Claude Code, run the following command:

claude mcp add adk-docs --transport stdio -- uvx --from mcpdoc mcpdoc --urls AgentDevelopmentKit:https://google.github.io/adk-docs/llms.txt --transport stdio


**Usage:**

Once installed, the MCP server is automatically enabled. You can ask questions
about ADK directly in Claude Code, and it will use the `llms.txt`

file and ADK
documentation to provide accurate answers and generate code.

For example, you can ask the following question from within Claude Code:

How do I create a function tool using Agent Development Kit?


### Cursor[¶](#cursor)

The [Cursor](https://cursor.com/) IDE can be configured to access the ADK
documentation by running a custom MCP server that points to the `llms.txt`

file
for ADK.

**Prerequisites:**

Ensure you have the [ uv](https://docs.astral.sh/uv/) tool installed, as this
configuration uses

`uvx`

to run the documentation server without manual
installation.**Configuration:**

- Open
**Cursor Settings**and navigate to the**Tools & MCP**tab. - Click on
**New MCP Server**, which will open`mcp.json`

for editing. -
Add the following entry to

`mcp.json`

with your custom MCP server configuration. If this is your first MCP server, you can paste the entire code block:

Refer to the [Cursor MCP documentation](https://cursor.com/docs/context/mcp) for
more information on managing MCP servers.

**Usage:**

Once configured, you can prompt the coding agent with instructions like:

Use the ADK docs to build a multi-tool agent that uses Gemini 2.5 Pro and includes a mock weather lookup tool and a custom calculator tool. Verify the agent using

`adk run`

.

### Other Tools[¶](#other-tools)

Any tool that supports the `llms.txt`

standard or can ingest documentation from
a URL can benefit from these files. You can provide the URL
`https://google.github.io/adk-docs/llms.txt`

(or `llms-full.txt`

) to your tool's
knowledge base configuration or MCP server configuration.
