---
merged_at: 2026-01-25T03:28:16.370970
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: models.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/agents/models -->

# AI Models for ADK agents¶

# AI Models for ADK agents[¶](#ai-models-for-adk-agents)

Agent Development Kit (ADK) is designed for flexibility, allowing you to integrate various Large Language Models (LLMs) into your agents. This section details how to leverage Gemini and integrate other popular models effectively, including those hosted externally or running locally.

ADK primarily uses two mechanisms for model integration:

-
**Direct String / Registry:**For models tightly integrated with Google Cloud, such as Gemini models accessed via Google AI Studio or Vertex AI, or models hosted on Vertex AI endpoints. You access these models by providing the model name or endpoint resource string and ADK's internal registry resolves this string to the appropriate backend client. -
**Model connectors:**For broader compatibility, especially models outside the Google ecosystem or those requiring specific client configurations, such as models accessed via Apigee or LiteLLM. You instantiate a specific wrapper class, such as`ApigeeLlm`

or`LiteLlm`

, and pass this object as the`model`

parameter to your`LlmAgent`

.


---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/agents/ -->

# Agents¶

# Agents[¶](#agents)

In Agent Development Kit (ADK), an **Agent** is a self-contained execution unit designed to act autonomously to achieve specific goals. Agents can perform tasks, interact with users, utilize external tools, and coordinate with other agents.

The foundation for all agents in ADK is the `BaseAgent`

class. It serves as the fundamental blueprint. To create functional agents, you typically extend `BaseAgent`

in one of three main ways, catering to different needs – from intelligent reasoning to structured process control.

## Core Agent Categories[¶](#core-agent-categories)

ADK provides distinct agent categories to build sophisticated applications:

-
: These agents utilize Large Language Models (LLMs) as their core engine to understand natural language, reason, plan, generate responses, and dynamically decide how to proceed or which tools to use, making them ideal for flexible, language-centric tasks.**LLM Agents (**`LlmAgent`

,`Agent`

)[Learn more about LLM Agents...](llm-agents/) -
: These specialized agents control the execution flow of other agents in predefined, deterministic patterns (sequence, parallel, or loop) without using an LLM for the flow control itself, perfect for structured processes needing predictable execution.**Workflow Agents (**`SequentialAgent`

,`ParallelAgent`

,`LoopAgent`

)[Explore Workflow Agents...](workflow-agents/) -
: Created by extending**Custom Agents**`BaseAgent`

directly, these agents allow you to implement unique operational logic, specific control flows, or specialized integrations not covered by the standard types, catering to highly tailored application requirements.[Discover how to build Custom Agents...](custom-agents/)

## Choosing the Right Agent Type[¶](#choosing-the-right-agent-type)

The following table provides a high-level comparison to help distinguish between the agent types. As you explore each type in more detail in the subsequent sections, these distinctions will become clearer.

| Feature | LLM Agent (`LlmAgent` ) |
Workflow Agent | Custom Agent (`BaseAgent` subclass) |
|---|---|---|---|
Primary Function |
Reasoning, Generation, Tool Use | Controlling Agent Execution Flow | Implementing Unique Logic/Integrations |
Core Engine |
Large Language Model (LLM) | Predefined Logic (Sequence, Parallel, Loop) | Custom Code |
Determinism |
Non-deterministic (Flexible) | Deterministic (Predictable) | Can be either, based on implementation |
Primary Use |
Language tasks, Dynamic decisions | Structured processes, Orchestration | Tailored requirements, Specific workflows |

## Agents Working Together: Multi-Agent Systems[¶](#agents-working-together-multi-agent-systems)

While each agent type serves a distinct purpose, the true power often comes from combining them. Complex applications frequently employ [multi-agent architectures](multi-agents/) where:

**LLM Agents**handle intelligent, language-based task execution.**Workflow Agents**manage the overall process flow using standard patterns.**Custom Agents**provide specialized capabilities or rules needed for unique integrations.

Understanding these core types is the first step toward building sophisticated, capable AI applications with ADK.

## What's Next?[¶](#whats-next)

Now that you have an overview of the different agent types available in ADK, dive deeper into how they work and how to use them effectively:

Explore how to configure agents powered by large language models, including setting instructions, providing tools, and enabling advanced features like planning and code execution.**LLM Agents:**Learn how to orchestrate tasks using**Workflow Agents:**`SequentialAgent`

,`ParallelAgent`

, and`LoopAgent`

for structured and predictable processes.Discover the principles of extending**Custom Agents:**`BaseAgent`

to build agents with unique logic and integrations tailored to your specific needs.Understand how to combine different agent types to create sophisticated, collaborative systems capable of tackling complex problems.**Multi-Agents:**Learn about the different LLM integrations available and how to select the right model for your agents.**Models:**
