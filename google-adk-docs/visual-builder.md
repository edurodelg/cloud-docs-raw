---
source_url: https://google.github.io/adk-docs/visual-builder/
fetched_at: 2026-02-08T00:46:01.115648
---

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