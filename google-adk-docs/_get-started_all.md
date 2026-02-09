---
merged_at: 2026-02-09T09:31:35.396941
merged_files: 9
---


---
<!-- Source: https://google.github.io/adk-docs/get-started/ -->

# Get started¶

# Get started[¶](#get-started)

Agent Development Kit (ADK) is designed to empower developers to quickly build, manage, evaluate and deploy AI-powered agents. These quick start guides get you set up and running a simple agent in less than 20 minutes.

-
**Python Quickstart**

Create your first Python ADK agent in minutes.

-
**Go Quickstart**

Create your first Go ADK agent in minutes.

-
**Java Quickstart**

Create your first Java ADK agent in minutes.

-
**TypeScript Quickstart**

Create your first TypeScript ADK agent in minutes.

---
<!-- Source: https://google.github.io/adk-docs/get-started/installation/ -->

# Installing ADK¶

# Installing ADK[¶](#installing-adk)

## Create & activate virtual environment[¶](#create-activate-virtual-environment)

We recommend creating a virtual Python environment using
[venv](https://docs.python.org/3/library/venv.html):

Now, you can activate the virtual environment using the appropriate command for your operating system and environment:

# Mac / Linux
source .venv/bin/activate
# Windows CMD:
.venv\Scripts\activate.bat
# Windows PowerShell:
.venv\Scripts\Activate.ps1


### Install ADK[¶](#install-adk)

(Optional) Verify your installation:

### Install ADK and ADK DevTools[¶](#install-adk-and-adk-devtools)

## Create a new Go module[¶](#create-a-new-go-module)

If you are starting a new project, you can create a new Go module:

## Install ADK[¶](#install-adk_1)

To add the ADK to your project, run the following command:

This will add the ADK as a dependency to your `go.mod`

file.

(Optional) Verify your installation by checking your `go.mod`

file for the `google.golang.org/adk`

entry.

You can either use maven or gradle to add the `google-adk`

and `google-adk-dev`

package.

`google-adk`

is the core Java ADK library. Java ADK also comes with a pluggable example SpringBoot server to run your agents seamlessly. This optional
package is present as part of `google-adk-dev`

.

If you are using maven, add the following to your `pom.xml`

:

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
<groupId>com.example.agent</groupId>
<artifactId>adk-agents</artifactId>
<version>1.0-SNAPSHOT</version>
<!-- Specify the version of Java you'll be using -->
<properties>
<maven.compiler.source>17</maven.compiler.source>
<maven.compiler.target>17</maven.compiler.target>
<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
<dependencies>
<!-- The ADK core dependency -->
<dependency>
<groupId>com.google.adk</groupId>
<artifactId>google-adk</artifactId>
<version>0.5.0</version>
</dependency>
<!-- The ADK dev web UI to debug your agent -->
<dependency>
<groupId>com.google.adk</groupId>
<artifactId>google-adk-dev</artifactId>
<version>0.5.0</version>
</dependency>
</dependencies>
</project>


Here's a [complete pom.xml](https://github.com/google/adk-docs/tree/main/examples/java/cloud-run/pom.xml) file for reference.

If you are using gradle, add the dependency to your build.gradle:

dependencies {
implementation 'com.google.adk:google-adk:0.5.0'
implementation 'com.google.adk:google-adk-dev:0.5.0'
}


You should also configure Gradle to pass `-parameters`

to `javac`

. (Alternatively, use `@Schema(name = "...")`

).

## Next steps[¶](#next-steps)

- Try creating your first agent with the
**Quickstart**

---
<!-- Source: https://google.github.io/adk-docs/get-started/python/ -->

# Python Quickstart for ADK¶

# Python Quickstart for ADK[¶](#python-quickstart-for-adk)

This guide shows you how to get up and running with Agent Development Kit (ADK) for Python. Before you start, make sure you have the following installed:

- Python 3.10 or later
`pip`

for installing packages

## Installation[¶](#installation)

Install ADK by running the following command:

## Recommended: create and activate a Python virtual environment

Create a Python virtual environment:

Activate the Python virtual environment:

## Create an agent project[¶](#create-an-agent-project)

Run the `adk create`

command to start a new agent project.

### Explore the agent project[¶](#explore-the-agent-project)

The created agent project has the following structure, with the `agent.py`

file containing the main control code for the agent.

## Update your agent project[¶](#update-your-agent-project)

The `agent.py`

file contains a `root_agent`

definition which is the only
required element of an ADK agent. You can also define tools for the agent to
use. Update the generated `agent.py`

code to include a `get_current_time`

tool
for use by the agent, as shown in the following code:

from google.adk.agents.llm_agent import Agent
# Mock tool implementation
def get_current_time(city: str) -> dict:
"""Returns the current time in a specified city."""
return {"status": "success", "city": city, "time": "10:30 AM"}
root_agent = Agent(
model='gemini-3-flash-preview',
name='root_agent',
description="Tells the current time in a specified city.",
instruction="You are a helpful assistant that tells the current time in cities. Use the 'get_current_time' tool for this purpose.",
tools=[get_current_time],
)


### Set your API key[¶](#set-your-api-key)

This project uses the Gemini API, which requires an API key. If you
don't already have Gemini API key, create a key in Google AI Studio on the
[API Keys](https://aistudio.google.com/app/apikey) page.

In a terminal window, write your API key into an `.env`

file as an environment variable:

## Using other AI models with ADK

ADK supports the use of many generative AI models. For more
information on configuring other models in ADK agents, see
[Models & Authentication](/adk-docs/agents/models).

## Run your agent[¶](#run-your-agent)

You can run your ADK agent with an interactive command-line interface using the
`adk run`

command or the ADK web user interface provided by the ADK using the
`adk web`

command. Both these options allow you to test and interact with your
agent.

### Run with command-line interface[¶](#run-with-command-line-interface)

Run your agent using the `adk run`

command-line tool.

### Run with web interface[¶](#run-with-web-interface)

The ADK framework provides web interface you can use to test and interact with your agent. You can start the web interface using the following command:

Note

Run this command from the **parent directory** that contains your
`my_agent/`

folder. For example, if your agent is inside `agents/my_agent/`

,
run `adk web`

from the `agents/`

directory.

This command starts a web server with a chat interface for your agent. You can access the web interface at (http://localhost:8000). Select the agent at the upper left corner and type a request.

Caution: ADK Web for development only

ADK Web is ** not meant for use in production deployments**. You should
use ADK Web for development and debugging purposes only.

## Next: Build your agent[¶](#next-build-your-agent)

Now that you have ADK installed and your first agent running, try building your own agent with our build guides:

---
<!-- Source: https://google.github.io/adk-docs/get-started/typescript/ -->

# TypeScript Quickstart for ADK¶

# TypeScript Quickstart for ADK[¶](#typescript-quickstart-for-adk)

This guide shows you how to get up and running with Agent Development Kit for TypeScript. Before you start, make sure you have the following installed:

- Node.js 24.13.0 or later
- Node Package Manager (npm) 11.8.0 or later

## Create an agent project[¶](#create-an-agent-project)

Create an empty `my-agent`

directory for your project:

### Configure project and dependencies[¶](#configure-project-and-dependencies)

Use the `npm`

tool to install and configure dependencies for your project,
including the package file, ADK TypeScript main
library, and developer tools. Run the following commands from your
`my-agent/`

directory to create the `package.json`

file and install the
project dependencies:

cd my-agent/
# initialize a project as an ES module
npm init --yes
npm pkg set type="module"
npm pkg set main="agent.ts"
# install ADK libraries
npm install @google/adk
# install dev tools as a dev dependency
npm install -D @google/adk-devtools


### Define the agent code[¶](#define-the-agent-code)

Create the code for a basic agent, including a simple implementation of an ADK
[Function Tool](/adk-docs/tools/function-tools/), called `getCurrentTime`

.
Create an `agent.ts`

file in your project directory and add the following code:

import {FunctionTool, LlmAgent} from '@google/adk';
import {z} from 'zod';
/* Mock tool implementation */
const getCurrentTime = new FunctionTool({
name: 'get_current_time',
description: 'Returns the current time in a specified city.',
parameters: z.object({
city: z.string().describe("The name of the city for which to retrieve the current time."),
}),
execute: ({city}) => {
return {status: 'success', report: `The current time in ${city} is 10:30 AM`};
},
});
export const rootAgent = new LlmAgent({
name: 'hello_time_agent',
model: 'gemini-2.5-flash',
description: 'Tells the current time in a specified city.',
instruction: `You are a helpful assistant that tells the current time in a city.
Use the 'getCurrentTime' tool for this purpose.`,
tools: [getCurrentTime],
});


### Set your API key[¶](#set-your-api-key)

This project uses the Gemini API, which requires an API key. If you
don't already have Gemini API key, create a key in Google AI Studio on the
[API Keys](https://aistudio.google.com/app/apikey) page.

In a terminal window, write your API key into your `.env`

file of your project
to set environment variables:

## Using other AI models with ADK

ADK supports the use of many generative AI models. For more
information on configuring other models in ADK agents, see
[Models & Authentication](/adk-docs/agents/models).

## Run your agent[¶](#run-your-agent)

You can run your ADK agent with the `@google/adk-devtools`

library as an
interactive command-line interface using the `run`

command or the ADK web user
interface using the `web`

command. Both these options allow you to test and
interact with your agent.

### Run with command-line interface[¶](#run-with-command-line-interface)

Run your agent with the ADK TypeScript command-line interface tool using the following command:

### Run with web interface[¶](#run-with-web-interface)

Run your agent with the ADK web interface using the following command:

This command starts a web server with a chat interface for your agent. You can access the web interface at (http://localhost:8000). Select your agent at the upper right corner and type a request.

Caution: ADK Web for development only

ADK Web is ** not meant for use in production deployments**. You should
use ADK Web for development and debugging purposes only.

## Next: Build your agent[¶](#next-build-your-agent)

Now that you have ADK installed and your first agent running, try building your own agent with our build guides:

---
<!-- Source: https://google.github.io/adk-docs/get-started/go/ -->

# Go Quickstart for ADK¶

# Go Quickstart for ADK[¶](#go-quickstart-for-adk)

This guide shows you how to get up and running with Agent Development Kit for Go. Before you start, make sure you have the following installed:

- Go 1.24.4 or later
- ADK Go v0.2.0 or later

## Create an agent project[¶](#create-an-agent-project)

Create an agent project with the following files and directory structure:

## Create this project structure using the command line

### Define the agent code[¶](#define-the-agent-code)

Create the code for a basic agent that uses the built-in
[Google Search tool](/adk-docs/tools/built-in-tools/#google-search). Add the
following code to the `my_agent/agent.go`

file in your project directory:

package main
import (
"context"
"log"
"os"
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/cmd/launcher"
"google.golang.org/adk/cmd/launcher/full"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/geminitool"
"google.golang.org/genai"
)
func main() {
ctx := context.Background()
model, err := gemini.NewModel(ctx, "gemini-3-pro-preview", &genai.ClientConfig{
APIKey: os.Getenv("GOOGLE_API_KEY"),
})
if err != nil {
log.Fatalf("Failed to create model: %v", err)
}
timeAgent, err := llmagent.New(llmagent.Config{
Name: "hello_time_agent",
Model: model,
Description: "Tells the current time in a specified city.",
Instruction: "You are a helpful assistant that tells the current time in a city.",
Tools: []tool.Tool{
geminitool.GoogleSearch{},
},
})
if err != nil {
log.Fatalf("Failed to create agent: %v", err)
}
config := &launcher.Config{
AgentLoader: agent.NewSingleLoader(timeAgent),
}
l := full.NewLauncher()
if err = l.Execute(ctx, config, os.Args[1:]); err != nil {
log.Fatalf("Run failed: %v\n\n%s", err, l.CommandLineSyntax())
}
}


### Configure project and dependencies[¶](#configure-project-and-dependencies)

Use the `go mod`

command to initialize the project modules and install the
required packages based on the `import`

statement in your agent code file:

### Set your API key[¶](#set-your-api-key)

This project uses the Gemini API, which requires an API key. If you
don't already have Gemini API key, create a key in Google AI Studio on the
[API Keys](https://aistudio.google.com/app/apikey) page.

In a terminal window, write your API key into the `.env`

or `env.bat`

file of
your project to set environment variables:

## Using other AI models with ADK

ADK supports the use of many generative AI models. For more
information on configuring other models in ADK agents, see
[Models & Authentication](/adk-docs/agents/models).

## Run your agent[¶](#run-your-agent)

You can run your ADK agent using the interactive command-line interface you defined or the ADK web user interface provided by the ADK Go command line tool. Both these options allow you to test and interact with your agent.

### Run with command-line interface[¶](#run-with-command-line-interface)

Run your agent using the following Go command:

# Remember to load keys and settings: source .env OR env.bat
go run agent.go


### Run with web interface[¶](#run-with-web-interface)

Run your agent with the ADK web interface using the following Go command:

# Remember to load keys and settings: source .env OR env.bat
go run agent.go web api webui


This command starts a web server with a chat interface for your agent. You can access the web interface at (http://localhost:8080). Select your agent at the upper left corner and type a request.

Caution: ADK Web for development only

ADK Web is ** not meant for use in production deployments**. You should
use ADK Web for development and debugging purposes only.

## Next: Build your agent[¶](#next-build-your-agent)

Now that you have ADK installed and your first agent running, try building your own agent with our build guides:

---
<!-- Source: https://google.github.io/adk-docs/get-started/about/ -->

# Agent Development Kit (ADK)¶

# Agent Development Kit (ADK)[¶](#agent-development-kit-adk)

** Build, Evaluate and Deploy agents, seamlessly! **

ADK is designed to empower developers to build, manage, evaluate and deploy AI-powered agents. It provides a robust and flexible environment for creating both conversational and non-conversational agents, capable of handling complex tasks and workflows.

## Core Concepts[¶](#core-concepts)

ADK is built around a few key primitives and concepts that make it powerful and flexible. Here are the essentials:

**Agent:**The fundamental worker unit designed for specific tasks. Agents can use language models (`LlmAgent`

) for complex reasoning, or act as deterministic controllers of the execution, which are called "[workflow agents](../../agents/workflow-agents/)" (`SequentialAgent`

,`ParallelAgent`

,`LoopAgent`

).**Tool:**Gives agents abilities beyond conversation, letting them interact with external APIs, search information, run code, or call other services.**Callbacks:**Custom code snippets you provide to run at specific points in the agent's process, allowing for checks, logging, or behavior modifications.**Session Management (**Handles the context of a single conversation (`Session`

&`State`

):`Session`

), including its history (`Events`

) and the agent's working memory for that conversation (`State`

).**Memory:**Enables agents to recall information about a user across*multiple*sessions, providing long-term context (distinct from short-term session`State`

).**Artifact Management (**Allows agents to save, load, and manage files or binary data (like images, PDFs) associated with a session or user.`Artifact`

):**Code Execution:**The ability for agents (usually via Tools) to generate and execute code to perform complex calculations or actions.**Planning:**An advanced capability where agents can break down complex goals into smaller steps and plan how to achieve them like a ReAct planner.**Models:**The underlying LLM that powers`LlmAgent`

s, enabling their reasoning and language understanding abilities.**Event:**The basic unit of communication representing things that happen during a session (user message, agent reply, tool use), forming the conversation history.**Runner:**The engine that manages the execution flow, orchestrates agent interactions based on Events, and coordinates with backend services.

**Note:** Features like Multimodal Streaming, Evaluation, Deployment,
Debugging, and Trace are also part of the broader ADK ecosystem, supporting
real-time interaction and the development lifecycle.

## Key Capabilities[¶](#key-capabilities)

ADK offers several key advantages for developers building agentic applications:

**Multi-Agent System Design:**Easily build applications composed of multiple, specialized agents arranged hierarchically. Agents can coordinate complex tasks, delegate sub-tasks using LLM-driven transfer or explicit`AgentTool`

invocation, enabling modular and scalable solutions.**Rich Tool Ecosystem:**Equip agents with diverse capabilities. ADK supports integrating custom functions (`FunctionTool`

), using other agents as tools (`AgentTool`

), leveraging built-in functionalities like code execution, and interacting with external data sources and APIs (e.g., Search, Databases). Support for long-running tools allows handling asynchronous operations effectively.**Flexible Orchestration:**Define complex agent workflows using built-in workflow agents (`SequentialAgent`

,`ParallelAgent`

,`LoopAgent`

) alongside LLM-driven dynamic routing. This allows for both predictable pipelines and adaptive agent behavior.**Integrated Developer Tooling:**Develop and iterate locally with ease. ADK includes tools like a command-line interface (CLI) and a Developer UI for running agents, inspecting execution steps (events, state changes), debugging interactions, and visualizing agent definitions.**Native Streaming Support:**Build real-time, interactive experiences with native support for bidirectional streaming (text and audio). This integrates seamlessly with underlying capabilities like the[Multimodal Live API for the Gemini Developer API](https://ai.google.dev/gemini-api/docs/live)(or for[Vertex AI](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/multimodal-live)), often enabled with simple configuration changes.**Built-in Agent Evaluation:**Assess agent performance systematically. The framework includes tools to create multi-turn evaluation datasets and run evaluations locally (via CLI or the dev UI) to measure quality and guide improvements.**Broad LLM Support:**While optimized for Google's Gemini models, the framework is designed for flexibility, allowing integration with various LLMs (potentially including open-source or fine-tuned models) through its`BaseLlm`

interface.**Artifact Management:**Enable agents to handle files and binary data. The framework provides mechanisms (`ArtifactService`

, context methods) for agents to save, load, and manage versioned artifacts like images, documents, or generated reports during their execution.**Extensibility and Interoperability:**ADK promotes an open ecosystem. While providing core tools, it allows developers to easily integrate and reuse third-party tools and data connectors.**State and Memory Management:**Automatically handles short-term conversational memory (`State`

within a`Session`

) managed by the`SessionService`

. Provides integration points for longer-term`Memory`

services, allowing agents to recall user information across multiple sessions.

## Get Started[¶](#get-started)

- Ready to build your first agent?
[Try the quickstart](../quickstart/)

---
<!-- Source: https://google.github.io/adk-docs/get-started/java/ -->

# Java Quickstart for ADK¶

# Java Quickstart for ADK[¶](#java-quickstart-for-adk)

This guide shows you how to get up and running with Agent Development Kit for Java. Before you start, make sure you have the following installed:

- Java 17 or later
- Maven 3.9 or later

## Create an agent project[¶](#create-an-agent-project)

Create an agent project with the following files and directory structure:

my_agent/
src/main/java/com/example/agent/
HelloTimeAgent.java # main agent code
AgentCliRunner.java # command-line interface
pom.xml # project configuration
.env # API keys or project IDs


## Create this project structure using the command line

### Define the agent code[¶](#define-the-agent-code)

Create the code for a basic agent, including a simple implementation of an ADK
[Function Tool](/adk-docs/tools-custom/function-tools/), called `getCurrentTime()`

.
Add the following code to the `HelloTimeAgent.java`

file in your project
directory:

package com.example.agent;
import com.google.adk.agents.BaseAgent;
import com.google.adk.agents.LlmAgent;
import com.google.adk.tools.Annotations.Schema;
import com.google.adk.tools.FunctionTool;
import java.util.Map;
public class HelloTimeAgent {
public static BaseAgent ROOT_AGENT = initAgent();
private static BaseAgent initAgent() {
return LlmAgent.builder()
.name("hello-time-agent")
.description("Tells the current time in a specified city")
.instruction("""
You are a helpful assistant that tells the current time in a city.
Use the 'getCurrentTime' tool for this purpose.
""")
.model("gemini-2.5-flash")
.tools(FunctionTool.create(HelloTimeAgent.class, "getCurrentTime"))
.build();
}
/** Mock tool implementation */
@Schema(description = "Get the current time for a given city")
public static Map<String, String> getCurrentTime(
@Schema(name = "city", description = "Name of the city to get the time for") String city) {
return Map.of(
"city", city,
"forecast", "The time is 10:30am."
);
}
}


Caution: Gemini 3 compatibility

ADK Java v0.3.0 and lower is not compatible with
[Gemini 3 Pro Preview](https://ai.google.dev/gemini-api/docs/models#gemini-3-pro)
due to thought signature changes for function calling. Use Gemini 2.5
or lower models instead.

### Configure project and dependencies[¶](#configure-project-and-dependencies)

An ADK agent project requires this dependency in your
`pom.xml`

project file:

<dependencies>
<dependency>
<groupId>com.google.adk</groupId>
<artifactId>google-adk</artifactId>
<version>0.5.0</version>
</dependency>
</dependencies>


Update the `pom.xml`

project file to include this dependency and
additional settings with the following configuration code:

## Complete `pom.xml`

configuration for project

The following code shows a complete `pom.xml`

configuration for
this project:

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
<groupId>com.example.agent</groupId>
<artifactId>adk-agents</artifactId>
<version>1.0-SNAPSHOT</version>
<!-- Specify the version of Java you'll be using -->
<properties>
<maven.compiler.source>17</maven.compiler.source>
<maven.compiler.target>17</maven.compiler.target>
<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
<dependencies>
<!-- The ADK core dependency -->
<dependency>
<groupId>com.google.adk</groupId>
<artifactId>google-adk</artifactId>
<version>0.3.0</version>
</dependency>
<!-- The ADK dev web UI to debug your agent -->
<dependency>
<groupId>com.google.adk</groupId>
<artifactId>google-adk-dev</artifactId>
<version>0.3.0</version>
</dependency>
</dependencies>
</project>


### Set your API key[¶](#set-your-api-key)

This project uses the Gemini API, which requires an API key. If you
don't already have Gemini API key, create a key in Google AI Studio on the
[API Keys](https://aistudio.google.com/app/apikey) page.

In a terminal window, write your API key into your `.env`

file of your project
to set environment variables:

## Using other AI models with ADK

ADK supports the use of many generative AI models. For more
information on configuring other models in ADK agents, see
[Models & Authentication](/adk-docs/agents/models).

### Create an agent command-line interface[¶](#create-an-agent-command-line-interface)

Create a `AgentCliRunner.java`

class to allow you to run and interact with
`HelloTimeAgent`

from the command line. This code shows how to create a
`RunConfig`

object to run the agent and a `Session`

object to interact with the
running agent.

package com.example.agent;
import com.google.adk.agents.RunConfig;
import com.google.adk.events.Event;
import com.google.adk.runner.InMemoryRunner;
import com.google.adk.sessions.Session;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
import io.reactivex.rxjava3.core.Flowable;
import java.util.Scanner;
import static java.nio.charset.StandardCharsets.UTF_8;
public class AgentCliRunner {
public static void main(String[] args) {
RunConfig runConfig = RunConfig.builder().build();
InMemoryRunner runner = new InMemoryRunner(HelloTimeAgent.ROOT_AGENT);
Session session = runner
.sessionService()
.createSession(runner.appName(), "user1234")
.blockingGet();
try (Scanner scanner = new Scanner(System.in, UTF_8)) {
while (true) {
System.out.print("\nYou > ");
String userInput = scanner.nextLine();
if ("quit".equalsIgnoreCase(userInput)) {
break;
}
Content userMsg = Content.fromParts(Part.fromText(userInput));
Flowable<Event> events = runner.runAsync(session.userId(), session.id(), userMsg, runConfig);
System.out.print("\nAgent > ");
events.blockingForEach(event -> {
if (event.finalResponse()) {
System.out.println(event.stringifyContent());
}
});
}
}
}
}


## Run your agent[¶](#run-your-agent)

You can run your ADK agent using the interactive command-line interface
`AgentCliRunner`

class you defined or the ADK web user interface provided by
the ADK using the `AdkWebServer`

class. Both these options allow you to test and
interact with your agent.

### Run with command-line interface[¶](#run-with-command-line-interface)

Run your agent with the command-line interface `AgentCliRunner`

class
using the following Maven command:

# Remember to load keys and settings: source .env OR env.bat
mvn compile exec:java -Dexec.mainClass="com.example.agent.AgentCliRunner"


### Run with web interface[¶](#run-with-web-interface)

Run your agent with the ADK web interface using the following Maven command:

# Remember to load keys and settings: source .env OR env.bat
mvn compile exec:java \
-Dexec.mainClass="com.google.adk.web.AdkWebServer" \
-Dexec.args="--adk.agents.source-dir=target --server.port=8000"


This command starts a web server with a chat interface for your agent. You can access the web interface at (http://localhost:8000). Select your agent at the upper left corner and type a request.

Caution: ADK Web for development only

ADK Web is ** not meant for use in production deployments**. You should
use ADK Web for development and debugging purposes only.

## Next: Build your agent[¶](#next-build-your-agent)

Now that you have ADK installed and your first agent running, try building your own agent with our build guides:

---
<!-- Source: https://google.github.io/adk-docs/get-started/quickstart/ -->

# Build a multi-tool agent¶

# Build a multi-tool agent[¶](#build-a-multi-tool-agent)

This quickstart guides you through installing the Agent Development Kit (ADK), setting up a basic agent with multiple tools, and running it locally either in the terminal or in the interactive, browser-based dev UI.

This quickstart assumes a local IDE (VS Code, PyCharm, IntelliJ IDEA, etc.) with Python 3.10+ or Java 17+ and terminal access. This method runs the application entirely on your machine and is recommended for internal development.

## 1. Set up Environment & Install ADK[¶](#set-up-environment-install-adk)

Create & Activate Virtual Environment (Recommended):

# Create
python -m venv .venv
# Activate (each new terminal)
# macOS/Linux: source .venv/bin/activate
# Windows CMD: .venv\Scripts\activate.bat
# Windows PowerShell: .venv\Scripts\Activate.ps1


Install ADK:

Create a new project directory, initialize it, and install dependencies:

mkdir my-adk-agent
cd my-adk-agent
npm init -y
npm install @google/adk @google/adk-devtools
npm install -D typescript


Create a `tsconfig.json`

file with the following content. This configuration ensures your project correctly handles modern Node.js modules.

To install ADK and setup the environment, proceed to the following steps.

## 2. Create Agent Project[¶](#create-agent-project)

### Project structure[¶](#project-structure)

You will need to create the following project structure:

Create the folder `multi_tool_agent`

:

Note for Windows users

When using ADK on Windows for the next few steps, we recommend creating
Python files using File Explorer or an IDE because the following commands
(`mkdir`

, `echo`

) typically generate files with null bytes and/or incorrect
encoding.

`__init__.py`

[¶](#__init__py)

Now create an `__init__.py`

file in the folder:

Your `__init__.py`

should now look like this:

`agent.py`

[¶](#agentpy)

Create an `agent.py`

file in the same folder:

Copy and paste the following code into `agent.py`

:

import datetime
from zoneinfo import ZoneInfo
from google.adk.agents import Agent
def get_weather(city: str) -> dict:
"""Retrieves the current weather report for a specified city.
Args:
city (str): The name of the city for which to retrieve the weather report.
Returns:
dict: status and result or error msg.
"""
if city.lower() == "new york":
return {
"status": "success",
"report": (
"The weather in New York is sunny with a temperature of 25 degrees"
" Celsius (77 degrees Fahrenheit)."
),
}
else:
return {
"status": "error",
"error_message": f"Weather information for '{city}' is not available.",
}
def get_current_time(city: str) -> dict:
"""Returns the current time in a specified city.
Args:
city (str): The name of the city for which to retrieve the current time.
Returns:
dict: status and result or error msg.
"""
if city.lower() == "new york":
tz_identifier = "America/New_York"
else:
return {
"status": "error",
"error_message": (
f"Sorry, I don't have timezone information for {city}."
),
}
tz = ZoneInfo(tz_identifier)
now = datetime.datetime.now(tz)
report = (
f'The current time in {city} is {now.strftime("%Y-%m-%d %H:%M:%S %Z%z")}'
)
return {"status": "success", "report": report}
root_agent = Agent(
name="weather_time_agent",
model="gemini-2.0-flash",
description=(
"Agent to answer questions about the time and weather in a city."
),
instruction=(
"You are a helpful agent who can answer user questions about the time and weather in a city."
),
tools=[get_weather, get_current_time],
)


`.env`

[¶](#env)

Create a `.env`

file in the same folder:

More instructions about this file are described in the next section on [Set up the model](#set-up-the-model).

You will need to create the following project structure in your `my-adk-agent`

directory:

`agent.ts`

[¶](#agentts)

Create an `agent.ts`

file in your project folder:

Copy and paste the following code into `agent.ts`

:

import 'dotenv/config';
import { FunctionTool, LlmAgent } from '@google/adk';
import { z } from 'zod';
const getWeather = new FunctionTool({
name: 'get_weather',
description: 'Retrieves the current weather report for a specified city.',
parameters: z.object({
city: z.string().describe('The name of the city for which to retrieve the weather report.'),
}),
execute: ({ city }) => {
if (city.toLowerCase() === 'new york') {
return {
status: 'success',
report:
'The weather in New York is sunny with a temperature of 25 degrees Celsius (77 degrees Fahrenheit).',
};
} else {
return {
status: 'error',
error_message: `Weather information for '${city}' is not available.`,
};
}
},
});
const getCurrentTime = new FunctionTool({
name: 'get_current_time',
description: 'Returns the current time in a specified city.',
parameters: z.object({
city: z.string().describe("The name of the city for which to retrieve the current time."),
}),
execute: ({ city }) => {
let tz_identifier: string;
if (city.toLowerCase() === 'new york') {
tz_identifier = 'America/New_York';
} else {
return {
status: 'error',
error_message: `Sorry, I don't have timezone information for ${city}.`,
};
}
const now = new Date();
const report = `The current time in ${city} is ${now.toLocaleString('en-US', { timeZone: tz_identifier })}`;
return { status: 'success', report: report };
},
});
export const rootAgent = new LlmAgent({
name: 'weather_time_agent',
model: 'gemini-2.5-flash',
description: 'Agent to answer questions about the time and weather in a city.',
instruction: 'You are a helpful agent who can answer user questions about the time and weather in a city.',
tools: [getWeather, getCurrentTime],
});


`.env`

[¶](#env_1)

Create a `.env`

file in the same folder:

More instructions about this file are described in the next section on [Set up the model](#set-up-the-model).

Java projects generally feature the following project structure:

project_folder/
├── pom.xml (or build.gradle)
├── src/
├── └── main/
│ └── java/
│ └── agents/
│ └── multitool/
└── test/


### Create `MultiToolAgent.java`

[¶](#create-multitoolagentjava)

Create a `MultiToolAgent.java`

source file in the `agents.multitool`

package
in the `src/main/java/agents/multitool/`

directory.

Copy and paste the following code into `MultiToolAgent.java`

:

package agents.multitool;
import com.google.adk.agents.BaseAgent;
import com.google.adk.agents.LlmAgent;
import com.google.adk.events.Event;
import com.google.adk.runner.InMemoryRunner;
import com.google.adk.sessions.Session;
import com.google.adk.tools.Annotations.Schema;
import com.google.adk.tools.FunctionTool;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
import io.reactivex.rxjava3.core.Flowable;
import java.nio.charset.StandardCharsets;
import java.text.Normalizer;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Map;
import java.util.Scanner;
public class MultiToolAgent {
private static String USER_ID = "student";
private static String NAME = "multi_tool_agent";
// The run your agent with Dev UI, the ROOT_AGENT should be a global public static final variable.
public static final BaseAgent ROOT_AGENT = initAgent();
public static BaseAgent initAgent() {
return LlmAgent.builder()
.name(NAME)
.model("gemini-2.0-flash")
.description("Agent to answer questions about the time and weather in a city.")
.instruction(
"You are a helpful agent who can answer user questions about the time and weather"
+ " in a city.")
.tools(
FunctionTool.create(MultiToolAgent.class, "getCurrentTime"),
FunctionTool.create(MultiToolAgent.class, "getWeather"))
.build();
}
public static Map<String, String> getCurrentTime(
@Schema(name = "city",
description = "The name of the city for which to retrieve the current time")
String city) {
String normalizedCity =
Normalizer.normalize(city, Normalizer.Form.NFD)
.trim()
.toLowerCase()
.replaceAll("(\\p{IsM}+|\\p{IsP}+)", "")
.replaceAll("\\s+", "_");
return ZoneId.getAvailableZoneIds().stream()
.filter(zid -> zid.toLowerCase().endsWith("/" + normalizedCity))
.findFirst()
.map(
zid ->
Map.of(
"status",
"success",
"report",
"The current time in "
+ city
+ " is "
+ ZonedDateTime.now(ZoneId.of(zid))
.format(DateTimeFormatter.ofPattern("HH:mm"))
+ "."))
.orElse(
Map.of(
"status",
"error",
"report",
"Sorry, I don't have timezone information for " + city + "."));
}
public static Map<String, String> getWeather(
@Schema(name = "city",
description = "The name of the city for which to retrieve the weather report")
String city) {
if (city.toLowerCase().equals("new york")) {
return Map.of(
"status",
"success",
"report",
"The weather in New York is sunny with a temperature of 25 degrees Celsius (77 degrees"
+ " Fahrenheit).");
} else {
return Map.of(
"status", "error", "report", "Weather information for " + city + " is not available.");
}
}
public static void main(String[] args) throws Exception {
InMemoryRunner runner = new InMemoryRunner(ROOT_AGENT);
Session session =
runner
.sessionService()
.createSession(NAME, USER_ID)
.blockingGet();
try (Scanner scanner = new Scanner(System.in, StandardCharsets.UTF_8)) {
while (true) {
System.out.print("\nYou > ");
String userInput = scanner.nextLine();
if ("quit".equalsIgnoreCase(userInput)) {
break;
}
Content userMsg = Content.fromParts(Part.fromText(userInput));
Flowable<Event> events = runner.runAsync(USER_ID, session.id(), userMsg);
System.out.print("\nAgent > ");
events.blockingForEach(event -> System.out.println(event.stringifyContent()));
}
}
}
}


## 3. Set up the model[¶](#set-up-the-model)

Your agent's ability to understand user requests and generate responses is
powered by a Large Language Model (LLM). Your agent needs to make secure calls
to this external LLM service, which **requires authentication credentials**. Without
valid authentication, the LLM service will deny the agent's requests, and the
agent will be unable to function.

Model Authentication guide

For a detailed guide on authenticating to different models, see the [Authentication guide](/adk-docs/agents/models/google-gemini#google-ai-studio).
This is a critical step to ensure your agent can make calls to the LLM service.

- Get an API key from
[Google AI Studio](https://aistudio.google.com/apikey). -
When using Python, open the

file located inside (`.env`

`multi_tool_agent/`

) and copy-paste the following code.When using Java, define environment variables:

When using TypeScript, the

`.env`

file is automatically loaded by the`import 'dotenv/config';`

line at the top of your`agent.ts`

file.`env title=""multi_tool_agent/.env" GOOGLE_GENAI_USE_VERTEXAI=FALSE GOOGLE_GENAI_API_KEY=PASTE_YOUR_ACTUAL_API_KEY_HERE`

-
Replace

`PASTE_YOUR_ACTUAL_API_KEY_HERE`

with your actual`API KEY`

.

- Set up a
[Google Cloud project](https://cloud.google.com/vertex-ai/generative-ai/docs/start/quickstarts/quickstart-multimodal#setup-gcp)and[enable the Vertex AI API](https://console.cloud.google.com/flows/enableapi?apiid=aiplatform.googleapis.com). - Set up the
[gcloud CLI](https://cloud.google.com/vertex-ai/generative-ai/docs/start/quickstarts/quickstart-multimodal#setup-local). - Authenticate to Google Cloud from the terminal by running
`gcloud auth application-default login`

. -
When using Python, open the

file located inside (`.env`

`multi_tool_agent/`

). Copy-paste the following code and update the project ID and location.multi_tool_agent/.env[GOOGLE_GENAI_USE_VERTEXAI=TRUE](#__codelineno-23-1)[GOOGLE_CLOUD_PROJECT=YOUR_PROJECT_ID](#__codelineno-23-2)[GOOGLE_CLOUD_LOCATION=LOCATION](#__codelineno-23-3)When using Java, define environment variables:

terminal[export GOOGLE_GENAI_USE_VERTEXAI=TRUE](#__codelineno-24-1)[export GOOGLE_CLOUD_PROJECT=YOUR_PROJECT_ID](#__codelineno-24-2)[export GOOGLE_CLOUD_LOCATION=LOCATION](#__codelineno-24-3)When using TypeScript, the

`.env`

file is automatically loaded by the`import 'dotenv/config';`

line at the top of your`agent.ts`

file.

- You can sign up for a free Google Cloud project and use Gemini for free with an eligible account!
- Set up a
[Google Cloud project with Vertex AI Express Mode](https://cloud.google.com/vertex-ai/generative-ai/docs/start/express-mode/overview) - Get an API key from your Express mode project. This key can be used with ADK to use Gemini models for free, as well as access to Agent Engine services.

- Set up a
-
When using Python, open the

file located inside (`.env`

`multi_tool_agent/`

). Copy-paste the following code and update the project ID and location.multi_tool_agent/.env[GOOGLE_GENAI_USE_VERTEXAI=TRUE](#__codelineno-26-1)[GOOGLE_API_KEY=PASTE_YOUR_ACTUAL_EXPRESS_MODE_API_KEY_HERE](#__codelineno-26-2)When using Java, define environment variables:

terminal[export GOOGLE_GENAI_USE_VERTEXAI=TRUE](#__codelineno-27-1)[export GOOGLE_API_KEY=PASTE_YOUR_ACTUAL_EXPRESS_MODE_API_KEY_HERE](#__codelineno-27-2)When using TypeScript, the

`.env`

file is automatically loaded by the`import 'dotenv/config';`

line at the top of your`agent.ts`

file.

## 4. Run Your Agent[¶](#run-your-agent)

Using the terminal, navigate to the parent directory of your agent project
(e.g. using `cd ..`

):

There are multiple ways to interact with your agent:

Authentication Setup for Vertex AI Users

If you selected **"Gemini - Google Cloud Vertex AI"** in the previous step, you must authenticate with Google Cloud before launching the dev UI.

Run this command and follow the prompts:

**Note:** Skip this step if you're using "Gemini - Google AI Studio".

Run the following command to launch the **dev UI**.

Caution: ADK Web for development only

ADK Web is ** not meant for use in production deployments**. You should
use ADK Web for development and debugging purposes only.

Note for Windows users

When hitting the `_make_subprocess_transport NotImplementedError`

, consider using `adk web --no-reload`

instead.

**Step 1:** Open the URL provided (usually `http://localhost:8000`

or
`http://127.0.0.1:8000`

) directly in your browser.

**Step 2.** In the top-left corner of the UI, you can select your agent in
the dropdown. Select "multi_tool_agent".

Troubleshooting

If you do not see "multi_tool_agent" in the dropdown menu, make sure you
are running `adk web`

in the **parent folder** of your agent folder
(i.e. the parent folder of multi_tool_agent).

**Step 3.** Now you can chat with your agent using the textbox:

**Step 4.** By using the `Events`

tab at the left, you can inspect
individual function calls, responses and model responses by clicking on the
actions:

On the `Events`

tab, you can also click the `Trace`

button to see the trace logs for each event that shows the latency of each function calls:

**Step 5.** You can also enable your microphone and talk to your agent:

Model support for voice/video streaming

In order to use voice/video streaming in ADK, you will need to use Gemini models that support the Live API. You can find the **model ID(s)** that supports the Gemini Live API in the documentation:

You can then replace the `model`

string in `root_agent`

in the `agent.py`

file you created earlier ([jump to section](#agentpy)). Your code should look something like:

Tip

When using `adk run`

you can inject prompts into the agent to start by
piping text to the command like so:

Run the following command, to chat with your Weather agent.

To exit, use Cmd/Ctrl+C.

`adk api_server`

enables you to create a local FastAPI server in a single
command, enabling you to test local cURL requests before you deploy your
agent.

To learn how to use `adk api_server`

for testing, refer to the
[documentation on using the API server](/adk-docs/runtime/api-server/).

Using the terminal, navigate to your agent project directory:

There are multiple ways to interact with your agent:

Run the following command to launch the **dev UI**.

**Step 1:** Open the URL provided (usually `http://localhost:8000`

or
`http://127.0.0.1:8000`

) directly in your browser.

**Step 2.** In the top-left corner of the UI, select your agent from the dropdown. The agents are listed by their filenames, so you should select "agent".

Troubleshooting

If you do not see "agent" in the dropdown menu, make sure you
are running `npx adk web`

in the directory containing your `agent.ts`

file.

**Step 3.** Now you can chat with your agent using the textbox:

**Step 4.** By using the `Events`

tab at the left, you can inspect
individual function calls, responses and model responses by clicking on the
actions:

On the `Events`

tab, you can also click the `Trace`

button to see the trace logs for each event that shows the latency of each function calls:

`npx adk api_server`

enables you to create a local Express.js server in a single
command, enabling you to test local cURL requests before you deploy your
agent.

To learn how to use `api_server`

for testing, refer to the
[documentation on testing](/adk-docs/runtime/api-server/).

Using the terminal, navigate to the parent directory of your agent project
(e.g. using `cd ..`

):

project_folder/ <-- navigate to this directory
├── pom.xml (or build.gradle)
├── src/
├── └── main/
│ └── java/
│ └── agents/
│ └── multitool/
│ └── MultiToolAgent.java
└── test/


Run the following command from the terminal to launch the Dev UI.

**DO NOT change the main class name of the Dev UI server.**

mvn exec:java \
-Dexec.mainClass="com.google.adk.web.AdkWebServer" \
-Dexec.args="--adk.agents.source-dir=src/main/java" \
-Dexec.classpathScope="compile"


**Step 1:** Open the URL provided (usually `http://localhost:8080`

or
`http://127.0.0.1:8080`

) directly in your browser.

**Step 2.** In the top-left corner of the UI, you can select your agent in
the dropdown. Select "multi_tool_agent".

Troubleshooting

If you do not see "multi_tool_agent" in the dropdown menu, make sure you
are running the `mvn`

command at the location where your Java source code
is located (usually `src/main/java`

).

**Step 3.** Now you can chat with your agent using the textbox:

**Step 4.** You can also inspect individual function calls, responses and
model responses by clicking on the actions:

Caution: ADK Web for development only

ADK Web is ** not meant for use in production deployments**. You should
use ADK Web for development and debugging purposes only.

With Maven, run the `main()`

method of your Java class
with the following command:

With Gradle, the `build.gradle`

or `build.gradle.kts`

build file
should have the following Java plugin in its `plugins`

section:

Then, elsewhere in the build file, at the top-level,
create a new task to run the `main()`

method of your agent:

tasks.register('runAgent', JavaExec) {
classpath = sourceSets.main.runtimeClasspath
mainClass = 'agents.multitool.MultiToolAgent'
}


Finally, on the command-line, run the following command:

### 📝 Example prompts to try[¶](#example-prompts-to-try)

- What is the weather in New York?
- What is the time in New York?
- What is the weather in Paris?
- What is the time in Paris?

## 🎉 Congratulations![¶](#congratulations)

You've successfully created and interacted with your first agent using ADK!

## 🛣️ Next steps[¶](#next-steps)

**Go to the tutorial**: Learn how to add memory, session, state to your agent:[tutorial](../../tutorials/).**Delve into advanced configuration:**Explore the[setup](../installation/)section for deeper dives into project structure, configuration, and other interfaces.**Understand Core Concepts:**Learn about[agents concepts](../../agents/).

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/get-started/streaming/ -->

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

---
<!-- Source: https://google.github.io/adk-docs/get-started/streaming/quickstart-streaming/ -->

# Build a streaming agent with Python¶

# Build a streaming agent with Python[¶](#build-a-streaming-agent-with-python)

With this quickstart, you'll learn to create a simple agent and use ADK Streaming to enable voice and video communication with it that is low-latency and bidirectional. We will install ADK, set up a basic "Google Search" agent, try running the agent with Streaming with `adk web`

tool, and then explain how to build a simple asynchronous web app by yourself using ADK Streaming and [FastAPI](https://fastapi.tiangolo.com/).

**Note:** This guide assumes you have experience using a terminal in Windows, Mac, and Linux environments.

## Supported models for voice/video streaming[¶](#supported-models)

In order to use voice/video streaming in ADK, you will need to use Gemini models that support the Live API. You can find the **model ID(s)** that supports the Gemini Live API in the documentation:

## 1. Setup Environment & Install ADK[¶](#setup-environment-install-adk)

Create & Activate Virtual Environment (Recommended):

# Create
python -m venv .venv
# Activate (each new terminal)
# macOS/Linux: source .venv/bin/activate
# Windows CMD: .venv\Scripts\activate.bat
# Windows PowerShell: .venv\Scripts\Activate.ps1


Install ADK:

## 2. Project Structure[¶](#project-structure)

Create the following folder structure with empty files:

adk-streaming/ # Project folder
└── app/ # the web app folder
├── .env # Gemini API key
└── google_search_agent/ # Agent folder
├── __init__.py # Python package
└── agent.py # Agent definition


### agent.py[¶](#agentpy)

Copy-paste the following code block into the `agent.py`

file.

For `model`

, please double check the model ID as described earlier in the [Models section](#supported-models).

from google.adk.agents import Agent
from google.adk.tools import google_search # Import the tool
root_agent = Agent(
# A unique name for the agent.
name="basic_search_agent",
# The Large Language Model (LLM) that agent will use.
# Please fill in the latest model id that supports live from
# https://google.github.io/adk-docs/get-started/streaming/quickstart-streaming/#supported-models
model="...",
# A short description of the agent's purpose.
description="Agent to answer questions using Google Search.",
# Instructions to set the agent's behavior.
instruction="You are an expert researcher. You always stick to the facts.",
# Add google_search tool to perform grounding with Google search.
tools=[google_search]
)


`agent.py`

is where all your agent(s)' logic will be stored, and you must have a `root_agent`

defined.

Notice how easily you integrated [grounding with Google Search](https://ai.google.dev/gemini-api/docs/grounding?lang=python#configure-search) capabilities. The `Agent`

class and the `google_search`

tool handle the complex interactions with the LLM and grounding with the search API, allowing you to focus on the agent's *purpose* and *behavior*.

Copy-paste the following code block to `__init__.py`

file.

## 3. Set up the platform[¶](#set-up-the-platform)

To run the agent, choose a platform from either Google AI Studio or Google Cloud Vertex AI:

- Get an API key from
[Google AI Studio](https://aistudio.google.com/apikey). -
Open the

file located inside (`.env`

`app/`

) and copy-paste the following code. -
Replace

`PASTE_YOUR_ACTUAL_API_KEY_HERE`

with your actual`API KEY`

.

- You need an existing
[Google Cloud](https://cloud.google.com/?e=48754805&hl=en)account and a project.- Set up a
[Google Cloud project](https://cloud.google.com/vertex-ai/generative-ai/docs/start/quickstarts/quickstart-multimodal#setup-gcp) - Set up the
[gcloud CLI](https://cloud.google.com/vertex-ai/generative-ai/docs/start/quickstarts/quickstart-multimodal#setup-local) - Authenticate to Google Cloud, from the terminal by running
`gcloud auth login`

. [Enable the Vertex AI API](https://console.cloud.google.com/flows/enableapi?apiid=aiplatform.googleapis.com).

- Set up a
-
Open the

file located inside (`.env`

`app/`

). Copy-paste the following code and update the project ID and location.

## 4. Try the agent with `adk web`

[¶](#try-the-agent-with-adk-web)

Now it's ready to try the agent. Run the following command to launch the **dev UI**. First, make sure to set the current directory to `app`

:

Also, set `SSL_CERT_FILE`

variable with the following command. This is required for the voice and video tests later.

Then, run the dev UI:

Note for Windows users

When hitting the `_make_subprocess_transport NotImplementedError`

, consider using `adk web --no-reload`

instead.

Caution: ADK Web for development only

ADK Web is ** not meant for use in production deployments**. You should
use ADK Web for development and debugging purposes only.

Open the URL provided (usually `http://localhost:8000`

or
`http://127.0.0.1:8000`

) **directly in your browser**. This connection stays
entirely on your local machine. Select `google_search_agent`

.

### Try with voice and video[¶](#try-with-voice-and-video)

To try with voice, reload the web browser, click the microphone button to enable the voice input, and ask the the following questions in voice. The agent will use the google_search tool to get the latest information to answer those questions. You will hear the answer in voice in real-time.

- What is the weather in New York?
- What is the time in New York?
- What is the weather in Paris?
- What is the time in Paris?

To try with video, reload the web browser, click the camera button to enable the video input, and ask questions like "What do you see?". The agent will answer what they see in the video input.

#### Caveat[¶](#caveat)

- You can not use text chat with the native-audio models. You will see errors when entering text messages on
`adk web`

.

### Stop the tool[¶](#stop-the-tool)

Stop `adk web`

by pressing `Ctrl-C`

on the console.

### Note on ADK Streaming[¶](#note-on-adk-streaming)

The following features will be supported in the future versions of the ADK Streaming: Callback, LongRunningTool, ExampleTool, and Shell agent (e.g. SequentialAgent).

Congratulations! You've successfully created and interacted with your first Streaming agent using ADK!

## Next steps: build custom streaming app[¶](#next-steps-build-custom-streaming-app)

The [Bidi-streaming development guide series](../../../streaming/dev-guide/part1/) gives an overview of the server and client code for a custom asynchronous web app built with ADK Streaming, enabling real-time, bidirectional audio and text communication.

---
<!-- Source: https://google.github.io/adk-docs/get-started/streaming/quickstart-streaming-java/ -->

# Build a streaming agent with Java¶

# Build a streaming agent with Java[¶](#build-a-streaming-agent-with-java)

This quickstart guide will walk you through the process of creating a basic agent and leveraging ADK Streaming with Java to facilitate low-latency, bidirectional voice interactions.

You'll begin by setting up your Java and Maven environment, structuring your project, and defining the necessary dependencies. Following this, you'll create a simple `ScienceTeacherAgent`

, test its text-based streaming capabilities using the Dev UI, and then progress to enabling live audio communication, transforming your agent into an interactive voice-driven application.

**Create your first agent**[¶](#create-your-first-agent)

**Prerequisites**[¶](#prerequisites)

-
In this getting started guide, you will be programming in Java. Check if

**Java**is installed on your machine. Ideally, you should be using Java 17 or more (you can check that by typing**java -version**) -
You’ll also be using the

**Maven**build tool for Java. So be sure to have[Maven installed](https://maven.apache.org/install.html)on your machine before going further (this is the case for Cloud Top or Cloud Shell, but not necessarily for your laptop).

**Prepare the project structure**[¶](#prepare-the-project-structure)

To get started with ADK Java, let’s create a Maven project with the following directory structure:

Follow the instructions in [Installation](../../installation/) page to add `pom.xml`

for using the ADK package.

Note

Feel free to use whichever name you like for the root directory of your project (instead of adk-agents)

**Running a compilation**[¶](#running-a-compilation)

Let’s see if Maven is happy with this build, by running a compilation (**mvn compile** command):

$ mvn compile
[INFO] Scanning for projects...
[INFO]
[INFO] --------------------< adk-agents:adk-agents >--------------------
[INFO] Building adk-agents 1.0-SNAPSHOT
[INFO] from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- resources:3.3.1:resources (default-resources) @ adk-demo ---
[INFO] skip non existing resourceDirectory /home/user/adk-demo/src/main/resources
[INFO]
[INFO] --- compiler:3.13.0:compile (default-compile) @ adk-demo ---
[INFO] Nothing to compile - all classes are up to date.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.347 s
[INFO] Finished at: 2025-05-06T15:38:08Z
[INFO] ------------------------------------------------------------------------


Looks like the project is set up properly for compilation!

**Creating an agent**[¶](#creating-an-agent)

Create the **ScienceTeacherAgent.java** file under the `src/main/java/agents/`

directory with the following content:

package samples.liveaudio;
import com.google.adk.agents.BaseAgent;
import com.google.adk.agents.LlmAgent;
/** Science teacher agent. */
public class ScienceTeacherAgent {
// Field expected by the Dev UI to load the agent dynamically
// (the agent must be initialized at declaration time)
public static final BaseAgent ROOT_AGENT = initAgent();
// Please fill in the latest model id that supports live API from
// https://google.github.io/adk-docs/get-started/streaming/quickstart-streaming/#supported-models
public static BaseAgent initAgent() {
return LlmAgent.builder()
.name("science-app")
.description("Science teacher agent")
.model("...") // Pleaase fill in the latest model id for live API
.instruction("""
You are a helpful science teacher that explains
science concepts to kids and teenagers.
""")
.build();
}
}


We will use `Dev UI`

to run this agent later. For the tool to automatically recognize the agent, its Java class has to comply with the following two rules:

- The agent should be stored in a global
**public static**variable named**ROOT_AGENT**of type**BaseAgent**and initialized at declaration time. - The agent definition has to be a
**static**method so it can be loaded during the class initialization by the dynamic compiling classloader.

**Run agent with Dev UI**[¶](#run-agent-with-adk-web-server)

`Dev UI`

is a web server where you can quickly run and test your agents for development purpose, without building your own UI application for the agents.

**Define environment variables**[¶](#define-environment-variables)

To run the server, you’ll need to export two environment variables:

- a Gemini key that you can
[get from AI Studio](https://ai.google.dev/gemini-api/docs/api-key), - a variable to specify we’re not using Vertex AI this time.

**Run Dev UI**[¶](#run-dev-ui)

Run the following command from the terminal to launch the Dev UI.

mvn exec:java \
-Dexec.mainClass="com.google.adk.web.AdkWebServer" \
-Dexec.args="--adk.agents.source-dir=." \
-Dexec.classpathScope="compile"


**Step 1:** Open the URL provided (usually `http://localhost:8080`

or
`http://127.0.0.1:8080`

) directly in your browser.

**Step 2.** In the top-left corner of the UI, you can select your agent in
the dropdown. Select "science-app".

Troubleshooting

If you do not see "science-app" in the dropdown menu, make sure you
are running the `mvn`

command from the root of your maven project.

Caution: ADK Web for development only

ADK Web is ** not meant for use in production deployments**. You should
use ADK Web for development and debugging purposes only.

## Try Dev UI with voice and video[¶](#try-dev-ui-with-voice-and-video)

With your favorite browser, navigate to: [http://127.0.0.1:8080/](http://127.0.0.1:8080/)

You should see the following interface:

Click the microphone button to enable the voice input, and ask a question `What's the electron?`

in voice. You will hear the answer in voice in real-time.

To try with video, reload the web browser, click the camera button to enable the video input, and ask questions like "What do you see?". The agent will answer what they see in the video input.

### Caveat[¶](#caveat)

- You can not use text chat with the native-audio models. You will see errors when entering text messages on
`adk web`

.

### Stop the tool[¶](#stop-the-tool)

Stop the tool by pressing `Ctrl-C`

on the console.

**Run agent with a custom live audio app**[¶](#run-agent-with-live-audio)

Now, let's try audio streaming with the agent and a custom live audio application.

**A Maven pom.xml build file for Live Audio**[¶](#a-maven-pomxml-build-file-for-live-audio)

Replace your existing pom.xml with the following.

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
<groupId>com.google.adk.samples</groupId>
<artifactId>google-adk-sample-live-audio</artifactId>
<version>0.1.0</version>
<name>Google ADK - Sample - Live Audio</name>
<description>
A sample application demonstrating a live audio conversation using ADK,
runnable via samples.liveaudio.LiveAudioRun.
</description>
<packaging>jar</packaging>
<properties>
<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
<java.version>17</java.version>
<auto-value.version>1.11.0</auto-value.version>
<!-- Main class for exec-maven-plugin -->
<exec.mainClass>samples.liveaudio.LiveAudioRun</exec.mainClass>
<google-adk.version>0.1.0</google-adk.version>
</properties>
<dependencyManagement>
<dependencies>
<dependency>
<groupId>com.google.cloud</groupId>
<artifactId>libraries-bom</artifactId>
<version>26.53.0</version>
<type>pom</type>
<scope>import</scope>
</dependency>
</dependencies>
</dependencyManagement>
<dependencies>
<dependency>
<groupId>com.google.adk</groupId>
<artifactId>google-adk</artifactId>
<version>${google-adk.version}</version>
</dependency>
<dependency>
<groupId>commons-logging</groupId>
<artifactId>commons-logging</artifactId>
<version>1.2</version> <!-- Or use a property if defined in a parent POM -->
</dependency>
</dependencies>
<build>
<plugins>
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-compiler-plugin</artifactId>
<version>3.13.0</version>
<configuration>
<source>${java.version}</source>
<target>${java.version}</target>
<parameters>true</parameters>
<annotationProcessorPaths>
<path>
<groupId>com.google.auto.value</groupId>
<artifactId>auto-value</artifactId>
<version>${auto-value.version}</version>
</path>
</annotationProcessorPaths>
</configuration>
</plugin>
<plugin>
<groupId>org.codehaus.mojo</groupId>
<artifactId>build-helper-maven-plugin</artifactId>
<version>3.6.0</version>
<executions>
<execution>
<id>add-source</id>
<phase>generate-sources</phase>
<goals>
<goal>add-source</goal>
</goals>
<configuration>
<sources>
<source>.</source>
</sources>
</configuration>
</execution>
</executions>
</plugin>
<plugin>
<groupId>org.codehaus.mojo</groupId>
<artifactId>exec-maven-plugin</artifactId>
<version>3.2.0</version>
<configuration>
<mainClass>${exec.mainClass}</mainClass>
<classpathScope>runtime</classpathScope>
</configuration>
</plugin>
</plugins>
</build>
</project>


**Creating Live Audio Run tool**[¶](#creating-live-audio-run-tool)

Create the **LiveAudioRun.java** file under the `src/main/java/`

directory with the following content. This tool runs the agent on it with live audio input and output.

package samples.liveaudio;
import com.google.adk.agents.LiveRequestQueue;
import com.google.adk.agents.RunConfig;
import com.google.adk.events.Event;
import com.google.adk.runner.Runner;
import com.google.adk.sessions.InMemorySessionService;
import com.google.common.collect.ImmutableList;
import com.google.genai.types.Blob;
import com.google.genai.types.Modality;
import com.google.genai.types.PrebuiltVoiceConfig;
import com.google.genai.types.Content;
import com.google.genai.types.Part;
import com.google.genai.types.SpeechConfig;
import com.google.genai.types.VoiceConfig;
import io.reactivex.rxjava3.core.Flowable;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.net.URL;
import javax.sound.sampled.AudioFormat;
import javax.sound.sampled.AudioInputStream;
import javax.sound.sampled.AudioSystem;
import javax.sound.sampled.DataLine;
import javax.sound.sampled.LineUnavailableException;
import javax.sound.sampled.Mixer;
import javax.sound.sampled.SourceDataLine;
import javax.sound.sampled.TargetDataLine;
import java.util.UUID;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.ConcurrentMap;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.atomic.AtomicBoolean;
import agents.ScienceTeacherAgent;
/** Main class to demonstrate running the {@link LiveAudioAgent} for a voice conversation. */
public final class LiveAudioRun {
private final String userId;
private final String sessionId;
private final Runner runner;
private static final javax.sound.sampled.AudioFormat MIC_AUDIO_FORMAT =
new javax.sound.sampled.AudioFormat(16000.0f, 16, 1, true, false);
private static final javax.sound.sampled.AudioFormat SPEAKER_AUDIO_FORMAT =
new javax.sound.sampled.AudioFormat(24000.0f, 16, 1, true, false);
private static final int BUFFER_SIZE = 4096;
public LiveAudioRun() {
this.userId = "test_user";
String appName = "LiveAudioApp";
this.sessionId = UUID.randomUUID().toString();
InMemorySessionService sessionService = new InMemorySessionService();
this.runner = new Runner(ScienceTeacherAgent.ROOT_AGENT, appName, null, sessionService);
ConcurrentMap<String, Object> initialState = new ConcurrentHashMap<>();
var unused =
sessionService.createSession(appName, userId, initialState, sessionId).blockingGet();
}
private void runConversation() throws Exception {
System.out.println("Initializing microphone input and speaker output...");
RunConfig runConfig =
RunConfig.builder()
.setStreamingMode(RunConfig.StreamingMode.BIDI)
.setResponseModalities(ImmutableList.of(new Modality("AUDIO")))
.setSpeechConfig(
SpeechConfig.builder()
.voiceConfig(
VoiceConfig.builder()
.prebuiltVoiceConfig(
PrebuiltVoiceConfig.builder().voiceName("Aoede").build())
.build())
.languageCode("en-US")
.build())
.build();
LiveRequestQueue liveRequestQueue = new LiveRequestQueue();
Flowable<Event> eventStream =
this.runner.runLive(
runner.sessionService().createSession(userId, sessionId).blockingGet(),
liveRequestQueue,
runConfig);
AtomicBoolean isRunning = new AtomicBoolean(true);
AtomicBoolean conversationEnded = new AtomicBoolean(false);
ExecutorService executorService = Executors.newFixedThreadPool(2);
// Task for capturing microphone input
Future<?> microphoneTask =
executorService.submit(() -> captureAndSendMicrophoneAudio(liveRequestQueue, isRunning));
// Task for processing agent responses and playing audio
Future<?> outputTask =
executorService.submit(
() -> {
try {
processAudioOutput(eventStream, isRunning, conversationEnded);
} catch (Exception e) {
System.err.println("Error processing audio output: " + e.getMessage());
e.printStackTrace();
isRunning.set(false);
}
});
// Wait for user to press Enter to stop the conversation
System.out.println("Conversation started. Press Enter to stop...");
System.in.read();
System.out.println("Ending conversation...");
isRunning.set(false);
try {
// Give some time for ongoing processing to complete
microphoneTask.get(2, TimeUnit.SECONDS);
outputTask.get(2, TimeUnit.SECONDS);
} catch (Exception e) {
System.out.println("Stopping tasks...");
}
liveRequestQueue.close();
executorService.shutdownNow();
System.out.println("Conversation ended.");
}
private void captureAndSendMicrophoneAudio(
LiveRequestQueue liveRequestQueue, AtomicBoolean isRunning) {
TargetDataLine micLine = null;
try {
DataLine.Info info = new DataLine.Info(TargetDataLine.class, MIC_AUDIO_FORMAT);
if (!AudioSystem.isLineSupported(info)) {
System.err.println("Microphone line not supported!");
return;
}
micLine = (TargetDataLine) AudioSystem.getLine(info);
micLine.open(MIC_AUDIO_FORMAT);
micLine.start();
System.out.println("Microphone initialized. Start speaking...");
byte[] buffer = new byte[BUFFER_SIZE];
int bytesRead;
while (isRunning.get()) {
bytesRead = micLine.read(buffer, 0, buffer.length);
if (bytesRead > 0) {
byte[] audioChunk = new byte[bytesRead];
System.arraycopy(buffer, 0, audioChunk, 0, bytesRead);
Blob audioBlob = Blob.builder().data(audioChunk).mimeType("audio/pcm").build();
liveRequestQueue.realtime(audioBlob);
}
}
} catch (LineUnavailableException e) {
System.err.println("Error accessing microphone: " + e.getMessage());
e.printStackTrace();
} finally {
if (micLine != null) {
micLine.stop();
micLine.close();
}
}
}
private void processAudioOutput(
Flowable<Event> eventStream, AtomicBoolean isRunning, AtomicBoolean conversationEnded) {
SourceDataLine speakerLine = null;
try {
DataLine.Info info = new DataLine.Info(SourceDataLine.class, SPEAKER_AUDIO_FORMAT);
if (!AudioSystem.isLineSupported(info)) {
System.err.println("Speaker line not supported!");
return;
}
final SourceDataLine finalSpeakerLine = (SourceDataLine) AudioSystem.getLine(info);
finalSpeakerLine.open(SPEAKER_AUDIO_FORMAT);
finalSpeakerLine.start();
System.out.println("Speaker initialized.");
for (Event event : eventStream.blockingIterable()) {
if (!isRunning.get()) {
break;
}
AtomicBoolean audioReceived = new AtomicBoolean(false);
processEvent(event, audioReceived);
event.content().ifPresent(content -> content.parts().ifPresent(parts -> parts.forEach(part -> playAudioData(part, finalSpeakerLine))));
}
speakerLine = finalSpeakerLine; // Assign to outer variable for cleanup in finally block
} catch (LineUnavailableException e) {
System.err.println("Error accessing speaker: " + e.getMessage());
e.printStackTrace();
} finally {
if (speakerLine != null) {
speakerLine.drain();
speakerLine.stop();
speakerLine.close();
}
conversationEnded.set(true);
}
}
private void playAudioData(Part part, SourceDataLine speakerLine) {
part.inlineData()
.ifPresent(
inlineBlob ->
inlineBlob
.data()
.ifPresent(
audioBytes -> {
if (audioBytes.length > 0) {
System.out.printf(
"Playing audio (%s): %d bytes%n",
inlineBlob.mimeType(),
audioBytes.length);
speakerLine.write(audioBytes, 0, audioBytes.length);
}
}));
}
private void processEvent(Event event, java.util.concurrent.atomic.AtomicBoolean audioReceived) {
event
.content()
.ifPresent(
content ->
content
.parts()
.ifPresent(parts -> parts.forEach(part -> logReceivedAudioData(part, audioReceived))));
}
private void logReceivedAudioData(Part part, AtomicBoolean audioReceived) {
part.inlineData()
.ifPresent(
inlineBlob ->
inlineBlob
.data()
.ifPresent(
audioBytes -> {
if (audioBytes.length > 0) {
System.out.printf(
" Audio (%s): received %d bytes.%n",
inlineBlob.mimeType(),
audioBytes.length);
audioReceived.set(true);
} else {
System.out.printf(
" Audio (%s): received empty audio data.%n",
inlineBlob.mimeType());
}
}));
}
public static void main(String[] args) throws Exception {
LiveAudioRun liveAudioRun = new LiveAudioRun();
liveAudioRun.runConversation();
System.out.println("Exiting Live Audio Run.");
}
}


**Run the Live Audio Run tool**[¶](#run-the-live-audio-run-tool)

To run Live Audio Run tool, use the following command on the `adk-agents`

directory:

Then you should see:

$ mvn compile exec:java
...
Initializing microphone input and speaker output...
Conversation started. Press Enter to stop...
Speaker initialized.
Microphone initialized. Start speaking...


With this message, the tool is ready to take voice input. Talk to the agent with a question like `What's the electron?`

.

Caution

When you observe the agent keep speaking by itself and doesn't stop, try using earphones to suppress the echoing.

**Summary**[¶](#summary)

Streaming for ADK enables developers to create agents capable of low-latency, bidirectional voice and video communication, enhancing interactive experiences. The article demonstrates that text streaming is a built-in feature of ADK Agents, requiring no additional specific code, while also showcasing how to implement live audio conversations for real-time voice interaction with an agent. This allows for more natural and dynamic communication, as users can speak to and hear from the agent seamlessly.
