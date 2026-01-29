---
merged_at: 2026-01-29T15:32:00.692145
merged_files: 2
---


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

Refer to the [MCP Tools documentation](/adk-docs/tools-custom/mcp-tools/) for code samples
and design patterns that help you use ADK together with MCP servers, including:

**Using Existing MCP Servers within ADK**: An ADK agent can act as an MCP client and use tools provided by external MCP servers.**Exposing ADK Tools via an MCP Server**: How to build an MCP server that wraps ADK tools, making them accessible to any MCP client.

## MCP Toolbox for Databases[¶](#mcp-toolbox-for-databases)

[MCP Toolbox for Databases](https://github.com/googleapis/genai-toolbox) is an
open-source MCP server that securely exposes your backend data sources as a
set of pre-built, production-ready tools for Gen AI agents. It functions as a
universal abstraction layer, allowing your ADK agent to securely query, analyze,
and retrieve information from a wide array of databases with built-in support.

The MCP Toolbox server includes a comprehensive library of connectors, ensuring that agents can safely interact with your complex data estate.

### Supported Data Sources[¶](#supported-data-sources)

MCP Toolbox provides out-of-the-box toolsets for the following databases and data platforms:

#### Google Cloud[¶](#google-cloud)

[BigQuery](https://googleapis.github.io/genai-toolbox/resources/sources/bigquery/)(including tools for SQL execution, schema discovery, and AI-powered time series forecasting)[AlloyDB](https://googleapis.github.io/genai-toolbox/resources/sources/alloydb-pg/)(PostgreSQL-compatible, with tools for both standard queries and natural language queries)[AlloyDB Admin](https://googleapis.github.io/genai-toolbox/resources/sources/alloydb-admin/)[Spanner](https://googleapis.github.io/genai-toolbox/resources/sources/spanner/)(supporting both GoogleSQL and PostgreSQL dialects)- Cloud SQL (with dedicated support for
[Cloud SQL for PostgreSQL](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-pg/),[Cloud SQL for MySQL](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-mysql/), and[Cloud SQL for SQL Server](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-mssql/)) [Cloud SQL Admin](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-admin/)[Firestore](https://googleapis.github.io/genai-toolbox/resources/sources/firestore/)[Bigtable](https://googleapis.github.io/genai-toolbox/resources/sources/bigtable/)[Dataplex](https://googleapis.github.io/genai-toolbox/resources/sources/dataplex/)(for data discovery and metadata search)[Cloud Monitoring](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-monitoring/)

#### Relational & SQL Databases[¶](#relational-sql-databases)

[PostgreSQL](https://googleapis.github.io/genai-toolbox/resources/sources/postgres/)(generic)[MySQL](https://googleapis.github.io/genai-toolbox/resources/sources/mysql/)(generic)[Microsoft SQL Server](https://googleapis.github.io/genai-toolbox/resources/sources/mssql/)(generic)[ClickHouse](https://googleapis.github.io/genai-toolbox/resources/sources/clickhouse/)[TiDB](https://googleapis.github.io/genai-toolbox/resources/sources/tidb/)[OceanBase](https://googleapis.github.io/genai-toolbox/resources/sources/oceanbase/)[Firebird](https://googleapis.github.io/genai-toolbox/resources/sources/firebird/)[SQLite](https://googleapis.github.io/genai-toolbox/resources/sources/sqlite/)[YugabyteDB](https://googleapis.github.io/genai-toolbox/resources/sources/yugabytedb/)

#### NoSQL & Key-Value Stores[¶](#nosql-key-value-stores)

#### Graph Databases[¶](#graph-databases)

#### Data Platforms & Federation[¶](#data-platforms-federation)

[Looker](https://googleapis.github.io/genai-toolbox/resources/sources/looker/)(for running Looks, queries, and building dashboards via the Looker API)[Trino](https://googleapis.github.io/genai-toolbox/resources/sources/trino/)(for running federated queries across multiple sources)

#### Other[¶](#other)

### Documentation[¶](#documentation)

Refer to the
[MCP Toolbox for Databases](/adk-docs/tools/google-cloud/mcp-toolbox-for-databases/)
documentation on how you can use ADK together with the MCP Toolbox for
Databases. For getting started with the MCP Toolbox for Databases, a blog post [Tutorial : MCP Toolbox for Databases - Exposing Big Query Datasets](https://medium.com/google-cloud/tutorial-mcp-toolbox-for-databases-exposing-big-query-datasets-9321f0064f4e) and Codelab [MCP Toolbox for Databases:Making BigQuery datasets available to MCP clients](https://codelabs.developers.google.com/mcp-toolbox-bigquery-dataset?hl=en#0) are also available.

## ADK Agent and FastMCP server[¶](#adk-agent-and-fastmcp-server)

[FastMCP](https://github.com/jlowin/fastmcp) handles all the complex MCP protocol details and server management, so you can focus on building great tools. It's designed to be high-level and Pythonic; in most cases, decorating a function is all you need.

Refer to the [MCP Tools documentation](/adk-docs/tools-custom/mcp-tools/) documentation on
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
