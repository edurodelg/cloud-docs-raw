---
source_url: https://google.github.io/adk-docs/a2a/quickstart-consuming/
fetched_at: 2026-01-25T03:14:05.791969
---

# Quickstart: Consuming a remote agent via A2A¶

# Quickstart: Consuming a remote agent via A2A[¶](#quickstart-consuming-a-remote-agent-via-a2a)

This quickstart covers the most common starting point for any developer: **"There is a remote agent, how do I let my ADK agent use it via A2A?"**. This is crucial for building complex multi-agent systems where different agents need to collaborate and interact.

## Overview[¶](#overview)

This sample demonstrates the **Agent2Agent (A2A)** architecture in the Agent Development Kit (ADK), showcasing how multiple agents can work together to handle complex tasks. The sample implements an agent that can roll dice and check if numbers are prime.

┌─────────────────┐ ┌──────────────────┐ ┌────────────────────┐
│ Root Agent │───▶│ Roll Agent │ │ Remote Prime │
│ (Local) │ │ (Local) │ │ Agent │
│ │ │ │ │ (localhost:8001) │
│ │───▶│ │◀───│ │
└─────────────────┘ └──────────────────┘ └────────────────────┘


The A2A Basic sample consists of:

**Root Agent**(`root_agent`

): The main orchestrator that delegates tasks to specialized sub-agents**Roll Agent**(`roll_agent`

): A local sub-agent that handles dice rolling operations**Prime Agent**(`prime_agent`

): A remote A2A agent that checks if numbers are prime, this agent is running on a separate A2A server

## Exposing Your Agent with the ADK Server[¶](#exposing-your-agent-with-the-adk-server)

The ADK comes with a built-in CLI command, `adk api_server --a2a`

to expose your agent using the A2A protocol.

In the `a2a_basic`

example, you will first need to expose the `check_prime_agent`

via an A2A server, so that the local root agent can use it.

### 1. Getting the Sample Code[¶](#getting-the-sample-code)

First, make sure you have the necessary dependencies installed:

You can clone and navigate to the here:

`a2a_basic`

sampleAs you'll see, the folder structure is as follows:

a2a_basic/
├── remote_a2a/
│ └── check_prime_agent/
│ ├── __init__.py
│ ├── agent.json
│ └── agent.py
├── README.md
├── __init__.py
└── agent.py # local root agent


#### Main Agent (`a2a_basic/agent.py`

)[¶](#main-agent-a2a_basicagentpy)

: Function tool for rolling dice`roll_die(sides: int)`

: Local agent specialized in dice rolling`roll_agent`

: Remote A2A agent configuration`prime_agent`

: Main orchestrator with delegation logic`root_agent`


#### Remote Prime Agent (`a2a_basic/remote_a2a/check_prime_agent/`

)[¶](#remote-prime-agent-a2a_basicremote_a2acheck_prime_agent)

: Implementation of the prime checking service`agent.py`

: Agent card of the A2A agent`agent.json`

: Prime number checking algorithm`check_prime(nums: list[int])`


### 2. Start the Remote Prime Agent server[¶](#start-the-remote-prime-agent-server)

To show how your ADK agent can consume a remote agent via A2A, you'll first need to start a remote agent server, which will host the prime agent (under `check_prime_agent`

).

# Start the remote a2a server that serves the check_prime_agent on port 8001
adk api_server --a2a --port 8001 contributing/samples/a2a_basic/remote_a2a


## Adding logging for debugging with `--log_level debug`


To enable debug-level logging, you can add `--log_level debug`

to your `adk api_server`

, as in:

## Why use port 8001?

In this quickstart, when testing locally, your agents will be using localhost, so the `port`

for the A2A server for the exposed agent (the remote, prime agent) must be different from the consuming agent's port. The default port for `adk web`

where you will interact with the consuming agent is `8000`

, which is why the A2A server is created using a separate port, `8001`

.

Once executed, you should see something like:

INFO: Started server process [56558]
INFO: Waiting for application startup.
INFO: Application startup complete.
INFO: Uvicorn running on http://127.0.0.1:8001 (Press CTRL+C to quit)


### 3. Look out for the required agent card (`agent-card.json`

) of the remote agent[¶](#look-out-for-the-required-agent-card-agent-json-of-the-remote-agent)

A2A Protocol requires that each agent must have an agent card that describes what it does.

If someone else has already built the remote A2A agent that you are looking to consume in your agent, then you should confirm that they have an agent card (`agent-card.json`

).

In the sample, the `check_prime_agent`

already has an agent card provided:

{
"capabilities": {},
"defaultInputModes": ["text/plain"],
"defaultOutputModes": ["application/json"],
"description": "An agent specialized in checking whether numbers are prime. It can efficiently determine the primality of individual numbers or lists of numbers.",
"name": "check_prime_agent",
"skills": [
{
"id": "prime_checking",
"name": "Prime Number Checking",
"description": "Check if numbers in a list are prime using efficient mathematical algorithms",
"tags": ["mathematical", "computation", "prime", "numbers"]
}
],
"url": "http://localhost:8001/a2a/check_prime_agent",
"version": "1.0.0"
}


## More info on agent cards in ADK

In ADK, you can use a `to_a2a(root_agent)`

wrapper which automatically generates an agent card for you. If you're interested in learning more about how to expose your existing agent so others can use it, then please look at the [A2A Quickstart (Exposing)](../quickstart-exposing/) tutorial.

### 4. Run the Main (Consuming) Agent[¶](#run-the-main-consuming-agent)

#### How it works[¶](#how-it-works)

The main agent uses the `RemoteA2aAgent()`

function to consume the remote agent (`prime_agent`

in our example). As you can see below, `RemoteA2aAgent()`

requires the `name`

, `description`

, and the URL of the `agent_card`

.

<...code truncated...>
from google.adk.agents.remote_a2a_agent import AGENT_CARD_WELL_KNOWN_PATH
from google.adk.agents.remote_a2a_agent import RemoteA2aAgent
prime_agent = RemoteA2aAgent(
name="prime_agent",
description="Agent that handles checking if numbers are prime.",
agent_card=(
f"http://localhost:8001/a2a/check_prime_agent{AGENT_CARD_WELL_KNOWN_PATH}"
),
)
<...code truncated>


Then, you can simply use the `RemoteA2aAgent`

in your agent. In this case, `prime_agent`

is used as one of the sub-agents in the `root_agent`

below:

from google.adk.agents.llm_agent import Agent
from google.genai import types
root_agent = Agent(
model="gemini-2.0-flash",
name="root_agent",
instruction="""
<You are a helpful assistant that can roll dice and check if numbers are prime.
You delegate rolling dice tasks to the roll_agent and prime checking tasks to the prime_agent.
Follow these steps:
1. If the user asks to roll a die, delegate to the roll_agent.
2. If the user asks to check primes, delegate to the prime_agent.
3. If the user asks to roll a die and then check if the result is prime, call roll_agent first, then pass the result to prime_agent.
Always clarify the results before proceeding.>
""",
global_instruction=(
"You are DicePrimeBot, ready to roll dice and check prime numbers."
),
sub_agents=[roll_agent, prime_agent],
tools=[example_tool],
generate_content_config=types.GenerateContentConfig(
safety_settings=[
types.SafetySetting( # avoid false alarm about rolling dice.
category=types.HarmCategory.HARM_CATEGORY_DANGEROUS_CONTENT,
threshold=types.HarmBlockThreshold.OFF,
),
]
),
)


## Example Interactions[¶](#example-interactions)

Once both your main and remote agents are running, you can interact with the root agent to see how it calls the remote agent via A2A:

**Simple Dice Rolling:**
This interaction uses a local agent, the Roll Agent:

**Prime Number Checking:**

This interaction uses a remote agent via A2A, the Prime Agent:

**Combined Operations:**

This interaction uses both the local Roll Agent and the remote Prime Agent:

User: Roll a 10-sided die and check if it's prime
Bot: I rolled an 8 for you.
Bot: 8 is not a prime number.


## Next Steps[¶](#next-steps)

Now that you have created an agent that's using a remote agent via an A2A server, the next step is to learn how to connect to it from another agent.

: Learn how to expose your existing agent so that other agents can use it via the A2A Protocol.**A2A Quickstart (Exposing)**