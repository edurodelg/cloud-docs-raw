---
source_url: https://google.github.io/adk-docs/apps/
fetched_at: 2026-02-05T08:19:29.197137
---

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