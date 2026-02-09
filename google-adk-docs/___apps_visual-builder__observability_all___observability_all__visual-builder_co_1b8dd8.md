---
merged_at: 2026-02-09T09:31:35.620113
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/apps/ -->

# Apps: workflow management class¶

# Apps: workflow management class[¶](#apps-workflow-management-class)

The ** App** class is a top-level container for an entire Agent Development Kit
(ADK) agent workflow. It is designed to manage the lifecycle, configuration, and
state for a collection of agents grouped by a

**. The**

*root agent***App**class separates the concerns of an agent workflow's overall operational infrastructure from individual agents' task-oriented reasoning.

Defining an ** App** object in your ADK workflow is optional and changes how you
organize your agent code and run your agents. From a practical perspective, you
use the

**class to configure the following features for your agent workflow:**

*App*This guide explains how to use the App class for configuring and managing your ADK agent workflows.

## Purpose of App Class[¶](#purpose-of-app-class)

The ** App** class addresses several architectural issues that arise when
building complex agentic systems:

**Centralized configuration:**Provides a single, centralized location for managing shared resources like API keys and database clients, avoiding the need to pass configuration down through every agent.**Lifecycle management:**Theclass includes*App*and*on startup*hooks, which allow for reliable management of persistent resources such as database connection pools or in-memory caches that need to exist across multiple invocations.*on shutdown***State scope:**It defines an explicit boundary for application-level state with an`app:*`

prefix making the scope and lifetime of this state clear to developers.**Unit of deployment:**Theconcept establishes a formal*App**deployable unit*, simplifying versioning, testing, and serving of agentic applications.

## Define an App object[¶](#define-an-app-object)

The ** App** class is used as the primary container of your agent workflow and
contains the root agent of the project. The

**is the container for the primary controller agent and any additional sub-agents.**

*root agent*### Define app with root agent[¶](#define-app-with-root-agent)

Create a ** root agent** for your workflow by creating a subclass from the

**base class. Then define an**

*Agent***object and configure it with the**

*App***object and optional features, as shown in the following sample code:**

*root agent*from google.adk.agents.llm_agent import Agent
from google.adk.apps import App
root_agent = Agent(
model='gemini-2.5-flash',
name='greeter_agent',
description='An agent that provides a friendly greeting.',
instruction='Reply with Hello, World!',
)
app = App(
name="agents",
root_agent=root_agent,
# Optionally include App-level features:
# plugins, context_cache_config, resumability_config
)


Recommended: Use `app`

variable name

In your agent project code, set your ** App** object to the variable name

`app`

so it is compatible with the ADK command line interface runner tools. ### Run your App agent[¶](#run-your-app-agent)

You can use the ** Runner** class to run your agent workflow using the

`app`

parameter, as shown in the following code sample:import asyncio
from dotenv import load_dotenv
from google.adk.runners import InMemoryRunner
from agent import app # import code from agent.py
load_dotenv() # load API keys and settings
# Set a Runner using the imported application object
runner = InMemoryRunner(app=app)
async def main():
try: # run_debug() requires ADK Python 1.18 or higher:
response = await runner.run_debug("Hello there!")
except Exception as e:
print(f"An error occurred during agent execution: {e}")
if __name__ == "__main__":
asyncio.run(main())


Version requirement for `Runner.run_debug()`


The `Runner.run_debug()`

command requires ADK Python v1.18.0 or higher.
You can also use `Runner.run()`

, which requires more setup code. For
more details, see the

Run your App agent with the `main.py`

code using the following command:

## Next steps[¶](#next-steps)

For a more complete sample code implementation, see the
[Hello World App](https://github.com/google/adk-python/tree/main/contributing/samples/hello_world_app)
code example.

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
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/observability/bigquery-agent-analytics/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/observability/logging/ -->

# Agent activity logging¶

# Agent activity logging[¶](#agent-activity-logging)

Agent Development Kit (ADK) uses Python's standard `logging`

module to provide flexible and powerful logging capabilities. Understanding how to configure and interpret these logs is crucial for monitoring agent behavior and debugging issues effectively.

## Logging Philosophy[¶](#logging-philosophy)

ADK's approach to logging is to provide detailed diagnostic information without being overly verbose by default. It is designed to be configured by the application developer, allowing you to tailor the log output to your specific needs, whether in a development or production environment.

**Standard Library:**It uses the standard`logging`

library, so any configuration or handler that works with it will work with ADK.**Hierarchical Loggers:**Loggers are named hierarchically based on the module path (e.g.,`google_adk.google.adk.agents.llm_agent`

), allowing for fine-grained control over which parts of the framework produce logs.**User-Configured:**The framework does not configure logging itself. It is the responsibility of the developer using the framework to set up the desired logging configuration in their application's entry point.

## How to Configure Logging[¶](#how-to-configure-logging)

You can configure logging in your main application script (e.g., `main.py`

) before you initialize and run your agent. The simplest way is to use `logging.basicConfig`

.

### Example Configuration[¶](#example-configuration)

To enable detailed logging, including `DEBUG`

level messages, add the following to the top of your script:

import logging
logging.basicConfig(
level=logging.DEBUG,
format='%(asctime)s - %(levelname)s - %(name)s - %(message)s'
)
# Your ADK agent code follows...
# from google.adk.agents import LlmAgent
# ...


### Configuring Logging with the ADK CLI[¶](#configuring-logging-with-the-adk-cli)

When running agents using the ADK's built-in web or API servers, you can easily control the log verbosity directly from the command line. The `adk web`

, `adk api_server`

, and `adk deploy cloud_run`

commands all accept a `--log_level`

option.

This provides a convenient way to set the logging level without modifying your agent's source code.


Note:The command-line setting always takes precedence over the programmatic configuration (like`logging.basicConfig`

) for ADK's loggers. It's recommended to use`INFO`

or`WARNING`

in production and enable`DEBUG`

only when troubleshooting.

**Example using adk web:**

To start the web server with `DEBUG`

level logging, run:

The available log levels for the `--log_level`

option are:

`DEBUG`

`INFO`

(default)`WARNING`

`ERROR`

`CRITICAL`


You can also use

`-v`

or`--verbose`

as a shortcut for`--log_level DEBUG`

.

### Log Levels[¶](#log-levels)

ADK uses standard log levels to categorize messages. The configured level determines what information gets logged.

| Level | Description | Type of Information Logged |
|---|---|---|
`DEBUG` |
Crucial for debugging. The most verbose level for fine-grained diagnostic information. |
|
`INFO` |
General information about the agent's lifecycle. |
|
`WARNING` |
Indicates a potential issue or deprecated feature use. The agent continues to function, but attention may be required. |
|
`ERROR` |
A serious error that prevented an operation from completing. |
|


Note:It is recommended to use`INFO`

or`WARNING`

in production environments. Only enable`DEBUG`

when actively troubleshooting an issue, as`DEBUG`

logs can be very verbose and may contain sensitive information.

## Reading and Understanding the Logs[¶](#reading-and-understanding-the-logs)

The `format`

string in the `basicConfig`

example determines the structure of each log message.

Here’s a sample log entry:

2025-07-08 11:22:33,456 - DEBUG - google_adk.google.adk.models.google_llm - LLM Request: contents { ... }


| Log Segment | Format Specifier | Meaning |
|---|---|---|
`2025-07-08 11:22:33,456` |
`%(asctime)s` |
Timestamp |
`DEBUG` |
`%(levelname)s` |
Severity level |
`google_adk.models.google_llm` |
`%(name)s` |
Logger name (the module that produced the log) |
`LLM Request: contents { ... }` |
`%(message)s` |
The actual log message |

By reading the logger name, you can immediately pinpoint the source of the log and understand its context within the agent's architecture.

## Debugging with Logs: A Practical Example[¶](#debugging-with-logs-a-practical-example)

**Scenario:** Your agent is not producing the expected output, and you suspect the prompt being sent to the LLM is incorrect or missing information.

**Steps:**

-
**Enable DEBUG Logging:**In your`main.py`

, set the logging level to`DEBUG`

as shown in the configuration example. -
**Run Your Agent:**Execute your agent's task as you normally would. -
**Inspect the Logs:**Look through the console output for a message from the`google.adk.models.google_llm`

logger that starts with`LLM Request:`

.[...](#__codelineno-5-1)[2025-07-10 15:26:13,778 - DEBUG - google_adk.google.adk.models.google_llm - Sending out request, model: gemini-2.0-flash, backend: GoogleLLMVariant.GEMINI_API, stream: False](#__codelineno-5-2)[2025-07-10 15:26:13,778 - DEBUG - google_adk.google.adk.models.google_llm -](#__codelineno-5-3)[LLM Request:](#__codelineno-5-4)[-----------------------------------------------------------](#__codelineno-5-5)[System Instruction:](#__codelineno-5-6)[You roll dice and answer questions about the outcome of the dice rolls.](#__codelineno-5-8)[You can roll dice of different sizes.](#__codelineno-5-9)[You can use multiple tools in parallel by calling functions in parallel(in one request and in one round).](#__codelineno-5-10)[It is ok to discuss previous dice roles, and comment on the dice rolls.](#__codelineno-5-11)[When you are asked to roll a die, you must call the roll_die tool with the number of sides. Be sure to pass in an integer. Do not pass in a string.](#__codelineno-5-12)[You should never roll a die on your own.](#__codelineno-5-13)[When checking prime numbers, call the check_prime tool with a list of integers. Be sure to pass in a list of integers. You should never pass in a string.](#__codelineno-5-14)[You should not check prime numbers before calling the tool.](#__codelineno-5-15)[When you are asked to roll a die and check prime numbers, you should always make the following two function calls:](#__codelineno-5-16)[1. You should first call the roll_die tool to get a roll. Wait for the function response before calling the check_prime tool.](#__codelineno-5-17)[2. After you get the function response from roll_die tool, you should call the check_prime tool with the roll_die result.](#__codelineno-5-18)[2.1 If user asks you to check primes based on previous rolls, make sure you include the previous rolls in the list.](#__codelineno-5-19)[3. When you respond, you must include the roll_die result from step 1.](#__codelineno-5-20)[You should always perform the previous 3 steps when asking for a roll and checking prime numbers.](#__codelineno-5-21)[You should not rely on the previous history on prime results.](#__codelineno-5-22)[You are an agent. Your internal name is "hello_world_agent".](#__codelineno-5-25)[The description about you is "hello world agent that can roll a dice of 8 sides and check prime numbers."](#__codelineno-5-27)[-----------------------------------------------------------](#__codelineno-5-28)[Contents:](#__codelineno-5-29)[{"parts":[{"text":"Roll a 6 sided dice"}],"role":"user"}](#__codelineno-5-30)[{"parts":[{"function_call":{"args":{"sides":6},"name":"roll_die"}}],"role":"model"}](#__codelineno-5-31)[{"parts":[{"function_response":{"name":"roll_die","response":{"result":2}}}],"role":"user"}](#__codelineno-5-32)[-----------------------------------------------------------](#__codelineno-5-33)[Functions:](#__codelineno-5-34)[roll_die: {'sides': {'type': <Type.INTEGER: 'INTEGER'>}}](#__codelineno-5-35)[check_prime: {'nums': {'items': {'type': <Type.INTEGER: 'INTEGER'>}, 'type': <Type.ARRAY: 'ARRAY'>}}](#__codelineno-5-36)[-----------------------------------------------------------](#__codelineno-5-37)[2025-07-10 15:26:13,779 - INFO - google_genai.models - AFC is enabled with max remote calls: 10.](#__codelineno-5-39)[2025-07-10 15:26:14,309 - INFO - google_adk.google.adk.models.google_llm -](#__codelineno-5-40)[LLM Response:](#__codelineno-5-41)[-----------------------------------------------------------](#__codelineno-5-42)[Text:](#__codelineno-5-43)[I have rolled a 6 sided die, and the result is 2.](#__codelineno-5-44)[...](#__codelineno-5-45) -
**Analyze the Prompt:**By examining the`System Instruction`

,`contents`

,`functions`

sections of the logged request, you can verify:- Is the system instruction correct?
- Is the conversation history (
`user`

and`model`

turns) accurate? - Is the most recent user query included?
- Are the correct tools being provided to the model?
- Are the tools correctly called by the model?
- How long it takes for the model to respond?


This detailed output allows you to diagnose a wide range of issues, from incorrect prompt engineering to problems with tool definitions, directly from the log files.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/observability/bigquery-agent-analytics/ -->

# Redirecting...

You're being redirected to a
new destination
.

---
<!-- Source: https://google.github.io/adk-docs/observability/logging/ -->

# Agent activity logging¶

# Agent activity logging[¶](#agent-activity-logging)

Agent Development Kit (ADK) uses Python's standard `logging`

module to provide flexible and powerful logging capabilities. Understanding how to configure and interpret these logs is crucial for monitoring agent behavior and debugging issues effectively.

## Logging Philosophy[¶](#logging-philosophy)

ADK's approach to logging is to provide detailed diagnostic information without being overly verbose by default. It is designed to be configured by the application developer, allowing you to tailor the log output to your specific needs, whether in a development or production environment.

**Standard Library:**It uses the standard`logging`

library, so any configuration or handler that works with it will work with ADK.**Hierarchical Loggers:**Loggers are named hierarchically based on the module path (e.g.,`google_adk.google.adk.agents.llm_agent`

), allowing for fine-grained control over which parts of the framework produce logs.**User-Configured:**The framework does not configure logging itself. It is the responsibility of the developer using the framework to set up the desired logging configuration in their application's entry point.

## How to Configure Logging[¶](#how-to-configure-logging)

You can configure logging in your main application script (e.g., `main.py`

) before you initialize and run your agent. The simplest way is to use `logging.basicConfig`

.

### Example Configuration[¶](#example-configuration)

To enable detailed logging, including `DEBUG`

level messages, add the following to the top of your script:

import logging
logging.basicConfig(
level=logging.DEBUG,
format='%(asctime)s - %(levelname)s - %(name)s - %(message)s'
)
# Your ADK agent code follows...
# from google.adk.agents import LlmAgent
# ...


### Configuring Logging with the ADK CLI[¶](#configuring-logging-with-the-adk-cli)

When running agents using the ADK's built-in web or API servers, you can easily control the log verbosity directly from the command line. The `adk web`

, `adk api_server`

, and `adk deploy cloud_run`

commands all accept a `--log_level`

option.

This provides a convenient way to set the logging level without modifying your agent's source code.


Note:The command-line setting always takes precedence over the programmatic configuration (like`logging.basicConfig`

) for ADK's loggers. It's recommended to use`INFO`

or`WARNING`

in production and enable`DEBUG`

only when troubleshooting.

**Example using adk web:**

To start the web server with `DEBUG`

level logging, run:

The available log levels for the `--log_level`

option are:

`DEBUG`

`INFO`

(default)`WARNING`

`ERROR`

`CRITICAL`


You can also use

`-v`

or`--verbose`

as a shortcut for`--log_level DEBUG`

.

### Log Levels[¶](#log-levels)

ADK uses standard log levels to categorize messages. The configured level determines what information gets logged.

| Level | Description | Type of Information Logged |
|---|---|---|
`DEBUG` |
Crucial for debugging. The most verbose level for fine-grained diagnostic information. |
|
`INFO` |
General information about the agent's lifecycle. |
|
`WARNING` |
Indicates a potential issue or deprecated feature use. The agent continues to function, but attention may be required. |
|
`ERROR` |
A serious error that prevented an operation from completing. |
|


Note:It is recommended to use`INFO`

or`WARNING`

in production environments. Only enable`DEBUG`

when actively troubleshooting an issue, as`DEBUG`

logs can be very verbose and may contain sensitive information.

## Reading and Understanding the Logs[¶](#reading-and-understanding-the-logs)

The `format`

string in the `basicConfig`

example determines the structure of each log message.

Here’s a sample log entry:

2025-07-08 11:22:33,456 - DEBUG - google_adk.google.adk.models.google_llm - LLM Request: contents { ... }


| Log Segment | Format Specifier | Meaning |
|---|---|---|
`2025-07-08 11:22:33,456` |
`%(asctime)s` |
Timestamp |
`DEBUG` |
`%(levelname)s` |
Severity level |
`google_adk.models.google_llm` |
`%(name)s` |
Logger name (the module that produced the log) |
`LLM Request: contents { ... }` |
`%(message)s` |
The actual log message |

By reading the logger name, you can immediately pinpoint the source of the log and understand its context within the agent's architecture.

## Debugging with Logs: A Practical Example[¶](#debugging-with-logs-a-practical-example)

**Scenario:** Your agent is not producing the expected output, and you suspect the prompt being sent to the LLM is incorrect or missing information.

**Steps:**

-
**Enable DEBUG Logging:**In your`main.py`

, set the logging level to`DEBUG`

as shown in the configuration example. -
**Run Your Agent:**Execute your agent's task as you normally would. -
**Inspect the Logs:**Look through the console output for a message from the`google.adk.models.google_llm`

logger that starts with`LLM Request:`

.[...](#__codelineno-5-1)[2025-07-10 15:26:13,778 - DEBUG - google_adk.google.adk.models.google_llm - Sending out request, model: gemini-2.0-flash, backend: GoogleLLMVariant.GEMINI_API, stream: False](#__codelineno-5-2)[2025-07-10 15:26:13,778 - DEBUG - google_adk.google.adk.models.google_llm -](#__codelineno-5-3)[LLM Request:](#__codelineno-5-4)[-----------------------------------------------------------](#__codelineno-5-5)[System Instruction:](#__codelineno-5-6)[You roll dice and answer questions about the outcome of the dice rolls.](#__codelineno-5-8)[You can roll dice of different sizes.](#__codelineno-5-9)[You can use multiple tools in parallel by calling functions in parallel(in one request and in one round).](#__codelineno-5-10)[It is ok to discuss previous dice roles, and comment on the dice rolls.](#__codelineno-5-11)[When you are asked to roll a die, you must call the roll_die tool with the number of sides. Be sure to pass in an integer. Do not pass in a string.](#__codelineno-5-12)[You should never roll a die on your own.](#__codelineno-5-13)[When checking prime numbers, call the check_prime tool with a list of integers. Be sure to pass in a list of integers. You should never pass in a string.](#__codelineno-5-14)[You should not check prime numbers before calling the tool.](#__codelineno-5-15)[When you are asked to roll a die and check prime numbers, you should always make the following two function calls:](#__codelineno-5-16)[1. You should first call the roll_die tool to get a roll. Wait for the function response before calling the check_prime tool.](#__codelineno-5-17)[2. After you get the function response from roll_die tool, you should call the check_prime tool with the roll_die result.](#__codelineno-5-18)[2.1 If user asks you to check primes based on previous rolls, make sure you include the previous rolls in the list.](#__codelineno-5-19)[3. When you respond, you must include the roll_die result from step 1.](#__codelineno-5-20)[You should always perform the previous 3 steps when asking for a roll and checking prime numbers.](#__codelineno-5-21)[You should not rely on the previous history on prime results.](#__codelineno-5-22)[You are an agent. Your internal name is "hello_world_agent".](#__codelineno-5-25)[The description about you is "hello world agent that can roll a dice of 8 sides and check prime numbers."](#__codelineno-5-27)[-----------------------------------------------------------](#__codelineno-5-28)[Contents:](#__codelineno-5-29)[{"parts":[{"text":"Roll a 6 sided dice"}],"role":"user"}](#__codelineno-5-30)[{"parts":[{"function_call":{"args":{"sides":6},"name":"roll_die"}}],"role":"model"}](#__codelineno-5-31)[{"parts":[{"function_response":{"name":"roll_die","response":{"result":2}}}],"role":"user"}](#__codelineno-5-32)[-----------------------------------------------------------](#__codelineno-5-33)[Functions:](#__codelineno-5-34)[roll_die: {'sides': {'type': <Type.INTEGER: 'INTEGER'>}}](#__codelineno-5-35)[check_prime: {'nums': {'items': {'type': <Type.INTEGER: 'INTEGER'>}, 'type': <Type.ARRAY: 'ARRAY'>}}](#__codelineno-5-36)[-----------------------------------------------------------](#__codelineno-5-37)[2025-07-10 15:26:13,779 - INFO - google_genai.models - AFC is enabled with max remote calls: 10.](#__codelineno-5-39)[2025-07-10 15:26:14,309 - INFO - google_adk.google.adk.models.google_llm -](#__codelineno-5-40)[LLM Response:](#__codelineno-5-41)[-----------------------------------------------------------](#__codelineno-5-42)[Text:](#__codelineno-5-43)[I have rolled a 6 sided die, and the result is 2.](#__codelineno-5-44)[...](#__codelineno-5-45) -
**Analyze the Prompt:**By examining the`System Instruction`

,`contents`

,`functions`

sections of the logged request, you can verify:- Is the system instruction correct?
- Is the conversation history (
`user`

and`model`

turns) accurate? - Is the most recent user query included?
- Are the correct tools being provided to the model?
- Are the tools correctly called by the model?
- How long it takes for the model to respond?


This detailed output allows you to diagnose a wide range of issues, from incorrect prompt engineering to problems with tool definitions, directly from the log files.

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
