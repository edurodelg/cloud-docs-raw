---
merged_at: 2026-01-26T23:20:36.822849
merged_files: 15
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/threads-runs-messages -->

# Threads, runs, and messages in Foundry Agent Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Foundry Agent Service supports persistent threads, runs, and messages. These components are essential for managing conversation states and interactions with users.

## Agent components

When you use an agent, the following steps are involved:

**Create an agent:**Create an agent to start sending messages and receiving responses.**Create a thread:**Create a thread once and append messages to it as users reply. The conversation history is maintained and managed automatically.**Send messages:**Both the agent and the user can send messages. These messages can include text, images, and other files.**Run the agent:**When you initiate a run, the agent processes the messages in the thread and performs tasks based on its configuration. It might append new messages to the thread as part of its response.**Monitor the run status:**Monitor the run until it completes.**Get the response:**After the agent creates a response, display it to the user.

## Agent

An agent is a configurable orchestration component that uses AI models with instructions, tools, parameters, and optional safety and governance controls. At run time, an agent uses these components and a given thread's message history to respond to user inputs.

## Threads

Threads are conversation sessions between an agent and a user. They store messages and automatically handle truncation to fit content into a model’s context. When you create a thread, you can append new messages (up to 100,000 per thread) as users respond.

## Messages

Messages are the individual pieces of communication within a thread. They can be created by either the agent or the user and can include text, or other files. Messages are stored as a list within the thread, allowing for a structured and organized conversation flow.

## Runs

A run involves invoking the agent on the thread. The agent processes the messages in the thread and might append new messages, which are responses from the agent. The agent uses its configuration and the thread's messages to perform tasks by calling models and tools. As part of a run, the agent appends messages to the thread.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/runtime-components -->

# Agent runtime components

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft Foundry Agent Service uses a small set of runtime objects to generate outputs and optionally persist state across turns.

This article explains the roles of an **agent**, **conversation**, and **response**, and how they work together during response generation.

## Prerequisites

- A
[Microsoft Foundry project](../../how-to/create-projects?view=foundry). - Familiarity with the
[agent development lifecycle](development-lifecycle?view=foundry)(optional).

## Agent components

When you work with an agent, you follow these steps:

**Create an agent**: Define an agent to start sending messages and receiving responses.**Create a conversation (optional)**: Use a conversation to maintain history across turns. If you don't use a conversation, carry forward context by using the output from a previous response.**Generate a response**: The agent processes input items in the conversation and any instructions provided in the request. The agent might append items to the conversation.**Check response status**: Monitor the response until it finishes (especially in streaming or background mode).**Retrieve the response**: Display the generated response to the user.


The diagram illustrates a loop: you provide user input (and optionally conversation history), the service generates a response (including tool calls when configured), and the resulting items can be reused as context for the next turn.

## Agent

An agent is a persisted orchestration definition that combines AI models, instructions, code, tools, parameters, and optional safety or governance controls.

Store agents as named, versioned assets in Microsoft Foundry. During response generation, the agent definition works with interaction history (conversation or previous response) to process and respond to user input.

## Conversation

A conversation manages states automatically, so you don't need to pass inputs manually for each turn.

Conversations are durable objects with unique identifiers. After creation, you can reuse them across sessions.

Conversations store items, which can include messages, tool calls, tool outputs, and other data.

### When to use a conversation

Use a conversation when you want:

**Multi-turn continuity**: Keep a stable history across turns without rebuilding context yourself.**Cross-session continuity**: Reuse the same conversation for a user who returns later.**Easier debugging**: Inspect what happened over time (for example, tool calls and outputs).

If you don't create a conversation, you can still build multi-turn flows by using the output from a previous response as the starting point for the next request. For an overview of how this approach differs from older thread-based patterns, see [Migrate to the Agents SDK](../how-to/migrate?view=foundry).

## Conversation items

Conversations store **items** rather than only chat messages. Items capture what happened during response generation so the next turn can reuse that context.

Common item types include:

**Message items**: User or assistant messages.**Tool call items**: Records of tool invocations the agent attempted.**Tool output items**: Outputs returned by tools (for example, retrieval results).**Output items**: The response content you display back to the user.

For examples that show how conversations and responses work together in code, see [Create and use memory in Foundry Agent Service](../how-to/memory-usage?view=foundry).

## Response

Response generation invokes the agent. The agent uses its configuration and any provided history (conversation or previous response) to perform tasks by calling models and tools. As part of response generation, the agent appends items to the conversation.

You can also generate a response without defining an agent. In this case, you provide all configurations directly in the request and use them only for that response. This approach is useful for simple scenarios with minimal tools.

## Streaming and background responses

Some response generation modes return results incrementally (streaming) or complete asynchronously (background). In these cases, you typically monitor the response until it finishes and then consume the final output items.

For details about response modes and how to consume outputs, see [Responses API](../../openai/how-to/responses?view=foundry).

## Security and data handling

Because conversations and responses can persist user-provided content and tool outputs, treat runtime data like application data:

**Avoid storing secrets in prompts or conversation history**. Use connections and managed secret stores instead (for example,[Set up a Key Vault connection](../../how-to/set-up-key-vault-connection?view=foundry)).**Use least privilege for tool access**. When a tool accesses external systems, the agent can potentially read or send data through that tool.**Be careful with non-Microsoft services**. If your agent calls tools backed by non-Microsoft services, some data might flow to those services. For related considerations, see[Discover tools in the Foundry Tools](tool-catalog?view=foundry).

## Limits and constraints

Limits can depend on the model, region, and the tools you attach (for example, streaming availability and tool support). For current availability and constraints for responses, see [Responses API](../../openai/how-to/responses?view=foundry).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/vector-stores -->

# Vector stores for file search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Vector store objects give the [file search](../how-to/tools/file-search?view=foundry) tool the ability to search your files. When you add a file to a vector store, the service parses, chunks, embeds, and indexes it so the tool can run both keyword and semantic search.

Vector stores can be attached to both agents and conversations. Currently, you can attach at most one vector store to an agent and at most one vector store to a conversation. For a conceptual overview of conversations, see [Agent runtime components](runtime-components?view=foundry).

In the current agents developer experience, response generation uses **responses** and **conversations**. Some SDKs and older samples use the term *run*. If you see both terms, treat *run* as response generation. For background and migration guidance, see [How to migrate to the new agent service](../how-to/migrate?view=foundry).

For a list of limits for vector search (such as maximum allowable file sizes), see the [quotas and limits](../quotas-limits?view=foundry) article.

## Key concepts

| Term | Meaning |
|---|---|
| Vector store | A container for searchable file content (chunks and embeddings) used by the file search tool. |
| Ingestion | The asynchronous process that parses, chunks, embeds, and indexes a file for search. |
| Readiness | Whether ingestion has completed and the vector store is searchable. |
| Expiration policy | A lifecycle policy that expires a vector store after a period of inactivity. |

## How vector stores work with file search

File search applies retrieval best practices to help your agent find the right content from your files. Depending on the query and your data, the tool can:

- Rewrite user queries to improve retrieval.
- Break down complex queries into multiple searches.
- Run both keyword and semantic searches across agent and conversation vector stores.
- Rerank results before adding them to the model context.

For current default retrieval settings (chunk size and overlap, embedding model, and the maximum number of chunks added to context), see [How it works](../how-to/tools/file-search?view=foundry#how-it-works).

## Where your data lives (basic vs standard agent setup)

Where files and search resources live depends on your agent setup:

**Basic agent setup**: File search uses Microsoft-managed storage and search resources.**Standard agent setup**: File search uses the Azure Blob Storage and Azure AI Search resources you connect during setup, so your files remain in your storage.

To set up your environment, see [Agent environment setup](../environment-setup?view=foundry). For more detail, see [Dependency on agent setup](../how-to/tools/file-search?view=foundry#dependency-on-agent-setup).

## Ensure vector store readiness before creating responses

Ensure all files in a vector store are fully processed before you create a response. This step ensures that all the data in your vector store is searchable.

To check readiness, use the SDK polling helpers (for example, *create-and-poll* and *upload-and-poll*) or poll the vector store object until its status is **completed**. For code examples, see [File search tool for agents](../how-to/tools/file-search?view=foundry).

As a fallback, response generation includes a 60-second maximum wait when the conversation's vector store contains files that are still being processed. This fallback wait doesn't apply to the agent's vector store.

## Add files and manage vector stores

Adding files to vector stores is an asynchronous operation. To ensure ingestion completes, use the create-and-poll helpers in the official SDKs. If you aren't using an SDK, retrieve the vector store object and monitor its file counts to confirm ingestion.

Files can also be added to a vector store after it's created by creating vector store files. Alternatively, you can add several files to a vector store by creating batches of up to 500 files.

When you upload a file to create a vector store, the system automatically:

**Chunks your content**into manageable pieces.**Converts each chunk**into high-dimensional vectors using embedding models.**Stores these vectors**in an optimized search index.**Creates associations**between the vectors and your original content.

## Basic agent setup: Deleting files from vector stores

If you're using a basic agent setup, files can be removed from a vector store by either:

- Deleting the vector store file object.
- Deleting the underlying file object, which removes the file from all vector store configurations across all agents and conversations in your organization.

### Managing costs with expiration policies

For the basic agent setup, Microsoft Foundry Agent Service uses vector store objects as a resource and you're billed based on the size of the vector store objects you create. The size of a vector store is the sum of all the parsed chunks from your files and their corresponding embeddings.

To help you manage the costs associated with these vector store objects, you can use expiration policies. You can set these policies when creating or updating the vector store object.

### Conversation vector stores have default expiration policies

Vector stores created using conversation helpers have a default expiration policy of seven days after they were last active (defined as the last time the vector store was used during response generation).

When a vector store expires, response generation for that conversation fails. To fix the issue, recreate a new vector store with the same files and reattach it to the conversation. For more detail, see [Conversation vector stores have default expiration policies](../how-to/tools/file-search?view=foundry#conversation-vector-stores-have-default-expiration-policies).

## Supported file types and key limits

For the supported file types list and encoding requirements, see [Supported file types](../how-to/tools/file-search?view=foundry#supported-file-types).

Key limits to keep in mind:

- You can attach at most one vector store to an agent and at most one vector store to a conversation.
- File size and token limits vary by feature. See
[Quotas and limits](../quotas-limits?view=foundry).

## Troubleshooting

**Your vector store isn't searchable yet**: Wait for ingestion to finish. Use SDK polling helpers or poll the vector store until its status is**completed**.**Response generation fails after a few days**: Your conversation vector store might have expired. Recreate a new vector store with the same files and reattach it.**A file disappeared from multiple agents or conversations**: You might have deleted the underlying file object, which removes the file from all vector store configurations across your organization.**Uploads or ingestion fail**: Check file size and token limits in[Quotas and limits](../quotas-limits?view=foundry).

## Next steps

- Learn more about the
[file search tool](../how-to/tools/file-search?view=foundry) - Review
[tool best practices](tool-best-practice?view=foundry)for guidance on reliability and security - Learn about
[agent runtime components](runtime-components?view=foundry)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/agent-memory -->

# Memory in Microsoft Foundry Agent Service (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Memory (preview) in Foundry Agent Service and the Memory Store API (preview) are licensed to you as part of your Azure subscription and are subject to terms applicable to "Previews" in the [Microsoft Product Terms](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) and the [Microsoft Products and Services Data Protection Addendum](https://aka.ms/DPA), as well as the Microsoft Generative AI Services Previews terms in the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Memory in Microsoft Foundry Agent Service is a managed, long-term memory solution. It enables agent continuity across sessions, devices, and workflows. By creating and managing memory stores, you can build agents that retain user preferences, maintain conversation history, and deliver personalized experiences.

This article provides an overview of agent memory, including its concepts, use cases, and limitations. For usage instructions, see [Create and use memory in Foundry Agent Service](../how-to/memory-usage?view=foundry).

## What is memory?

Memory is persistent knowledge retained by an agent across sessions. Generally, agent memory falls into two categories:

**Short-term memory**tracks the current session's conversation and maintains immediate context for ongoing interactions. Agent orchestration frameworks typically manage this memory as part of the session context.**Long-term memory**retains distilled knowledge across sessions. The model can recall and build on previous user interactions over time. Long-term memory requires a persistent system that extracts, consolidates, and manages knowledge.

Memory in Foundry Agent Service is designed for long-term memory. It extracts meaningful information from conversations, consolidates it into durable knowledge, and makes it available across sessions.

## How memory works

Behind the scenes, memories are stored as items in a managed memory store. The system applies consolidation and conflict‑resolution logic where applicable. Currently, consolidation is performed for user profile memories to merge duplicate or overlapping profile information. Chat summary memories aren't consolidated.

Memory operates in the following phases:

**Extraction:**When a user interacts with an agent, the system actively extracts key information from the conversation, such as user preferences, facts, and relevant context. For example, preferences like "allergic to dairy" and summaries of recent activities are identified and stored.**Consolidation:**Extracted memories are consolidated to keep the memory store efficient and relevant. The system uses LLMs to merge similar or duplicate topics so that the agent doesn't store redundant information. Conflicting facts, such as a new allergy, are resolved to maintain an accurate memory.**Retrieval:**When the agent needs to recall information, it uses hybrid search techniques to find the most relevant memories. This allows the agent to quickly surface the right context, making conversations feel natural and informed. Core memories, such as user profile and preferences, are retrieved at the beginning of a conversation so that the agent is immediately aware of the user's core needs.

Here's an example of how memory can improve and personalize interactions between a recipe agent and a user who previously expressed a food allergy:

Tip

Need help deciding when to use memory? Consider these guidelines:

- Use memory for user-specific context that persists over time.
- Use a
[Foundry IQ knowledge base](../how-to/tools/knowledge-retrieval?view=foundry)to ground your agent on curated organizational content. - Use the
[file search tool](../how-to/tools/file-search?view=foundry)to search user-provided documents during an interaction.

## Memory types

Memory in Foundry Agent Service extracts and stores two types of long-term memory:

| Type | Description | Configuration |
|---|---|---|
| User profile memory | Information and preferences about the user, such as preferred name, dietary restrictions, and language preference. These memories are considered "static" with respect to a conversation because they generally don't depend on the current chat context. Retrieve user profile memories once at the beginning of each conversation. | Specify `user_profile_details` in a
|
| Chat summary memory | A distilled summary of each topic or thread covered in a chat session. These memories allow users to continue conversations or reference prior sessions without repeating earlier context. Retrieve chat summary memories based on the current conversation to surface relevant threads. | Enable `chat_summaries` in a
|

## Working with memory

There are two ways to use memory for agent interactions:

**Memory search tool:**Attach the memory search tool to a prompt agent to enable reading from and writing to the memory store during conversations. This approach is ideal for most scenarios because it simplifies memory management. For more information, see[Use memories via an agent tool](../how-to/memory-usage?view=foundry#use-memories-via-an-agent-tool).**Memory store APIs:**Interact directly with the memory store using the low-level APIs. This approach provides more control and flexibility for advanced use cases. For more information, see[Use memories via APIs](../how-to/memory-usage?view=foundry#use-memories-via-apis).

## Use cases

The following examples illustrate how memory can enhance various types of agents.

A customer support agent that remembers your name, previous issues and resolutions, ticket numbers, and your preferred contact method (chat, email, or call back). This memory helps you avoid repeating information, so conversations are more efficient and satisfying.

A personal shopping assistant that remembers your size in specific brands, preferred colors, past returns, and recent purchases. The agent can suggest relevant items as soon as you start a session and avoid recommending products you already own.


## Security risks

When you work with memory in Foundry Agent Service, the large language model (LLM) extracts and consolidates memories based on conversations. Protect memory against threats such as prompt injection and memory corruption. These risks arise when incorrect or harmful data is stored in the agent's memory, potentially influencing agent responses and actions.

To mitigate security risks, consider these actions:

**Use**Validate all prompts entering or leaving the memory system to prevent malicious content.[Azure AI Content Safety](https://ai.azure.com/explore/contentsafety)and its[prompt injection detection](../../../ai-services/content-safety/concepts/jailbreak-detection?view=foundry):**Perform attack and adversarial testing:**Regularly stress-test your agent for injection vulnerabilities through controlled adversarial exercises.

## Limitations and quotas

- You must use chat and embedding models from Azure OpenAI. Other model providers aren't currently supported.
- You must set the
`scope`

value explicitly. Automatic population from the user identity specified in the request isn't currently supported. - Maximum scopes per memory store: 100
- Maximum memories per scope: 10,000
- Search memories: 1,000 requests per minute
- Update memories: 1,000 requests per minute

For broader Foundry Agent Service quotas and limits, see [Foundry Agent Service quotas and limits](../quotas-limits?view=foundry).

## Pricing

During the public preview, memory features are free. You're only billed for usage of the chat and embedding models.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/what-is-memory -->

# Memory in Microsoft Foundry Agent Service (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Memory (preview) in Foundry Agent Service and the Memory Store API (preview) are licensed to you as part of your Azure subscription and are subject to terms applicable to "Previews" in the [Microsoft Product Terms](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) and the [Microsoft Products and Services Data Protection Addendum](https://aka.ms/DPA), as well as the Microsoft Generative AI Services Previews terms in the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Memory in Microsoft Foundry Agent Service is a managed, long-term memory solution. It enables agent continuity across sessions, devices, and workflows. By creating and managing memory stores, you can build agents that retain user preferences, maintain conversation history, and deliver personalized experiences.

This article provides an overview of agent memory, including its concepts, use cases, and limitations. For usage instructions, see [Create and use memory in Foundry Agent Service](../how-to/memory-usage?view=foundry).

## What is memory?

Memory is persistent knowledge retained by an agent across sessions. Generally, agent memory falls into two categories:

**Short-term memory**tracks the current session's conversation and maintains immediate context for ongoing interactions. Agent orchestration frameworks typically manage this memory as part of the session context.**Long-term memory**retains distilled knowledge across sessions. The model can recall and build on previous user interactions over time. Long-term memory requires a persistent system that extracts, consolidates, and manages knowledge.

Memory in Foundry Agent Service is designed for long-term memory. It extracts meaningful information from conversations, consolidates it into durable knowledge, and makes it available across sessions.

## How memory works

Behind the scenes, memories are stored as items in a managed memory store. The system applies consolidation and conflict‑resolution logic where applicable. Currently, consolidation is performed for user profile memories to merge duplicate or overlapping profile information. Chat summary memories aren't consolidated.

Memory operates in the following phases:

**Extraction:**When a user interacts with an agent, the system actively extracts key information from the conversation, such as user preferences, facts, and relevant context. For example, preferences like "allergic to dairy" and summaries of recent activities are identified and stored.**Consolidation:**Extracted memories are consolidated to keep the memory store efficient and relevant. The system uses LLMs to merge similar or duplicate topics so that the agent doesn't store redundant information. Conflicting facts, such as a new allergy, are resolved to maintain an accurate memory.**Retrieval:**When the agent needs to recall information, it uses hybrid search techniques to find the most relevant memories. This allows the agent to quickly surface the right context, making conversations feel natural and informed. Core memories, such as user profile and preferences, are retrieved at the beginning of a conversation so that the agent is immediately aware of the user's core needs.

Here's an example of how memory can improve and personalize interactions between a recipe agent and a user who previously expressed a food allergy:

Tip

Need help deciding when to use memory? Consider these guidelines:

- Use memory for user-specific context that persists over time.
- Use a
[Foundry IQ knowledge base](../how-to/tools/knowledge-retrieval?view=foundry)to ground your agent on curated organizational content. - Use the
[file search tool](../how-to/tools/file-search?view=foundry)to search user-provided documents during an interaction.

## Memory types

Memory in Foundry Agent Service extracts and stores two types of long-term memory:

| Type | Description | Configuration |
|---|---|---|
| User profile memory | Information and preferences about the user, such as preferred name, dietary restrictions, and language preference. These memories are considered "static" with respect to a conversation because they generally don't depend on the current chat context. Retrieve user profile memories once at the beginning of each conversation. | Specify `user_profile_details` in a
|
| Chat summary memory | A distilled summary of each topic or thread covered in a chat session. These memories allow users to continue conversations or reference prior sessions without repeating earlier context. Retrieve chat summary memories based on the current conversation to surface relevant threads. | Enable `chat_summaries` in a
|

## Working with memory

There are two ways to use memory for agent interactions:

**Memory search tool:**Attach the memory search tool to a prompt agent to enable reading from and writing to the memory store during conversations. This approach is ideal for most scenarios because it simplifies memory management. For more information, see[Use memories via an agent tool](../how-to/memory-usage?view=foundry#use-memories-via-an-agent-tool).**Memory store APIs:**Interact directly with the memory store using the low-level APIs. This approach provides more control and flexibility for advanced use cases. For more information, see[Use memories via APIs](../how-to/memory-usage?view=foundry#use-memories-via-apis).

## Use cases

The following examples illustrate how memory can enhance various types of agents.

A customer support agent that remembers your name, previous issues and resolutions, ticket numbers, and your preferred contact method (chat, email, or call back). This memory helps you avoid repeating information, so conversations are more efficient and satisfying.

A personal shopping assistant that remembers your size in specific brands, preferred colors, past returns, and recent purchases. The agent can suggest relevant items as soon as you start a session and avoid recommending products you already own.


## Security risks

When you work with memory in Foundry Agent Service, the large language model (LLM) extracts and consolidates memories based on conversations. Protect memory against threats such as prompt injection and memory corruption. These risks arise when incorrect or harmful data is stored in the agent's memory, potentially influencing agent responses and actions.

To mitigate security risks, consider these actions:

**Use**Validate all prompts entering or leaving the memory system to prevent malicious content.[Azure AI Content Safety](https://ai.azure.com/explore/contentsafety)and its[prompt injection detection](../../../ai-services/content-safety/concepts/jailbreak-detection?view=foundry):**Perform attack and adversarial testing:**Regularly stress-test your agent for injection vulnerabilities through controlled adversarial exercises.

## Limitations and quotas

- You must use chat and embedding models from Azure OpenAI. Other model providers aren't currently supported.
- You must set the
`scope`

value explicitly. Automatic population from the user identity specified in the request isn't currently supported. - Maximum scopes per memory store: 100
- Maximum memories per scope: 10,000
- Search memories: 1,000 requests per minute
- Update memories: 1,000 requests per minute

For broader Foundry Agent Service quotas and limits, see [Foundry Agent Service quotas and limits](../quotas-limits?view=foundry).

## Pricing

During the public preview, memory features are free. You're only billed for usage of the chat and embedding models.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/standard-agent-setup -->

# Built-in enterprise readiness with standard agent setup

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Standard Agent Setup uses customer-managed, single-tenant Azure resources to store agent state and keep all agent data under your control.

In this setup:

- Agent states (conversations, responses) are stored in your own Azure resources.

## Leveraging your own resources for storing customer data

Both standard setup configurations are designed to give you complete control over sensitive data by requiring the use of your own Azure resources. The required Bring Your Own (BYO) resources include:

**BYO File Storage**: All files uploaded by developers (during agent configuration) or end-users (during interactions) are stored directly in the customer’s Azure Storage account.**BYO Search**: All vector stores created by the agent leverage the customer’s Azure AI Search resource.**BYO Thread Storage**: All customer messages and conversation history will be stored in the customer’s own Azure Cosmos DB account.

By bundling these BYO features (file storage, search, and thread storage), the standard setup guarantees that your deployment is secure by default. All data processed by Foundry Agent Service is automatically stored at rest in your own Azure resources, helping you meet internal policies, compliance requirements, and enterprise security standards.

### Azure Cosmos DB for NoSQL

Your existing Azure Cosmos DB for NoSQL Account used in standard setup must have a total throughput limit of at least **3000 RU/s**. Both **Provisioned Throughput** and **Serverless** modes are supported.

When you use standard setup, **three containers** will be provisioned in your existing Cosmos DB account, and **each container requires 1000 RU/s**.

- thread-message-store: End-user conversations
- system-thread-message-store: Internal system messages
- agent-entity-store: Agent metadata including their instructions, tools, name, etc.

## Project-Level Data Isolation

Standard setup enforces project-level data isolation by default. Two blob storage containers will automatically be provisioned in your storage account, one for files and one for intermediate system data (chunks, embeddings) and three containers will be provisioned in your Cosmos DB, one for user systems, one for system messages, and one for user inputs related to created agents such as their instructions, tools, name, etc. This default behavior was chosen to reduce setup complexity while still enforcing strict data boundaries between projects.

## Capability hosts

** Capability hosts** are sub-resources on both the Account and Project, enabling interaction with the Agent Service.

**Account Capability Host**: The account capability host has an empty request body except for the parameter capabilityHostKind="Agents".**Project Capability Host**: Specifies resources for storing agent state, either managed multitenant (basic setup) or customer-owned (standard setup), single-tenant resource. Think of project capability host as the project settings.

### Limitations

**Update Not Supported**: Cannot update the capability host for a project or account.

## Step by Step Provisioning Process

### Manual

Create project dependent resources for standard setup

- Create new (or pass in resource ID of existing) Cosmos DB resource
- Create new (or pass in resource ID of existing) Azure Storage resource
- Create new (or pass in resource ID of existing) Azure AI Search resource
- Create a new Key Vault resource
- [Optional]: Create new application insights resource
- [Optional]: pass in resource ID of existing Foundry resource

Create Microsoft Foundry Resource (cognitive service/accounts kind=AIServices)

Create Account-level connections

- Create account connection to Application Insights resource

Deploy gpt-4o or other agent compatible model

Create Project (cognitive service/accounts/project)

Create project connections

- [if provided] Project connection to Foundry resource
- Create project connection to Azure Storage account
- Create project connection to Azure AI Search account
- Create project connection to Cosmos DB account

Assign the project-managed identity (including for SMI) the following roles:

- Cosmos DB Operator at the scope of the account level for the Cosmos DB account resource
- Storage Account Contributor at the scope of the account level for the Storage Account resource

Set Account capability host with empty properties section.

Set Project capability host with properties Cosmos DB, Azure Storage, AI Search connections

Assign the Project Managed Identity (both for SMI and UMI) the following roles on the specified resource scopes:

- Azure AI Search (can be assigned either before or after capHost creation)
- Assign roles: Search Index Data Contributor, Search Service Contributor

- Azure Blob Storage Container:
`<workspaceId>-azureml-blobstore`

- Assign role: Storage Blob Data Contributor

- Azure Blob Storage Container:
`<workspaceId>- agents-blobstore`

- Assign role: Storage Blob Data Owner

- Cosmos DB for NoSQL Database:
`enterprise_memory`

- Assign role: Cosmos DB Built-in Data Contributor
- Scope: Database level to cover all containers (no individual container specific role assignment).


- Azure AI Search (can be assigned either before or after capHost creation)
Once all resources are provisioned, all developers who want to create/edit agents in the project should be assigned the role: Azure AI User on the project scope.


### Use Bicep template

Use an existing Azure OpenAI, Azure Storage account, Azure Cosmos DB for NoSQL account and/or Azure AI Search resource by providing the full ARM resource ID in the [standard agent template file](https://github.com/azure-ai-foundry/foundry-samples/blob/main/infrastructure/infrastructure-setup-bicep/43-standard-agent-setup-with-customization/main.bicep).

#### Use an existing Azure OpenAI resource

Follow the steps in basic agent setup to get the Foundry Tools account resource ID.

In the standard agent template file, replace the following placeholders:

`existingAoaiResourceId:/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{serviceName}`


#### Use an existing Azure Storage account for file storage

To get your storage account resource ID, sign in to the Azure CLI and select the subscription with your storage account:

`az login`

Then run the command:

`az storage account show --resource-group <your-resource-group> --name <your-storage-account> --query "id" --output tsv`

The output is the

`aiStorageAccountResourceID`

you need to use in the template.In the standard agent template file, replace the following placeholders:

`aiStorageAccountResourceId:/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}`


#### Use an existing Azure Cosmos DB for NoSQL account for thread storage

An Azure Cosmos DB for NoSQL account is created for each Foundry account.

For every project under a Foundry account, three containers are deployed within the same Cosmos DB account. Each container requires a minimum of 1000 RU/s.

For example, if two projects are deployed under the same Foundry account, the Cosmos DB account must be configured with at least 6000 RU/s (3 containers × 1000 RU/s × 2 projects) to ensure sufficient throughput.

Both provisioned throughput and serverless modes are supported.

Note

Insufficient RU/s capacity in the Cosmos DB account will result in capability host provisioning failures during deployment.

To get your Azure Cosmos DB account resource ID, sign in to the Azure CLI and select the subscription with your account:

`az login`

Then run the command:

`az cosmosdb show --resource-group <your-resource-group> --name <your-comosdb-account> --query "id" --output tsv`

The output is the

`cosmosDBResourceId`

you need to use in the template.In the standard agent template file, replace the following placeholders:

`cosmosDBResourceId:/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DocumentDB/databaseAccounts/{cosmosDbAccountName}`


#### Use an existing Azure AI Search resource

To get your Azure AI Search resource ID, sign into Azure CLI and select the subscription with your search resource:

`az login`

Then run the command:

`az search service show --resource-group <your-resource-group> --name <your-search-service> --query "id" --output tsv`

In the standard agent template file, replace the following placeholders:

`aiSearchServiceResourceId:/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Search/searchServices/{searchServiceName}`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/model-region-support -->

# Supported models and regions for Foundry Agent Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

In this article, you learn which Azure OpenAI models and regions are supported for agents in Microsoft Foundry Agent Service. These models have different capabilities and price points.

Microsoft Foundry offers two main types of deployments:

*Standard*includes a global deployment option that routes traffic globally to provide higher throughput.*Provisioned*also includes a global deployment option. You can purchase and deploy provisioned throughput units across the Azure global infrastructure.

All deployments can perform the same inference operations. However, the billing, scale, and performance are substantially different. To learn more about Azure OpenAI deployment types, see [Deployment types for Microsoft Foundry Models](../../foundry-models/concepts/deployment-types?view=foundry-classic).

## How to use this page

Use the tables in this article to choose a supported combination of deployment type, model version, and Azure region.

**Deployment type**: Use the tabs to select the deployment type you plan to use (standard or provisioned).**Region**: The**Region**column lists the Azure region where you deploy the model.**Availability markers**:- ✅: Supported.
- Blank cells or
`-`

: Not supported.


## Available models

Foundry Agent Service supports the following Azure OpenAI models in the listed regions.

Keep in mind that model availability varies by region and cloud. Certain tools and capabilities require the latest models. The following models are available in the REST API and SDKs.

Note

[Hub-based projects](../../what-is-foundry?view=foundry-classic#types-of-projects)are limited to the following models: gpt-4o, gpt-4o-mini, gpt-4, and gpt-35-turbo.[Spillover traffic management](../../openai/how-to/spillover-traffic-management?view=foundry-classic)for[provisioned throughput](../../openai/concepts/provisioned-throughput?view=foundry-classic)is compatible with agents.- For information on Class A subnet support, see the
[setup guide on GitHub](https://github.com/azure-ai-foundry/foundry-samples/tree/main/infrastructure/infrastructure-setup-bicep/15-private-network-standard-agent-setup). - The
[file search tool](../how-to/tools-classic/file-search?view=foundry-classic)is currently unavailable in the Italy North and Brazil South regions. - The gpt-5 models can use only the
[code interpreter](../how-to/tools-classic/code-interpreter?view=foundry-classic)and[file search](../how-to/tools-classic/file-search?view=foundry-classic)tools. [Registration](https://aka.ms/openai/gpt-5/2025-08-07)is required to use the gpt-5 models. Access is granted according to Microsoft's eligibility criteria.

Note

[Spillover traffic management](../../openai/how-to/spillover-traffic-management?view=foundry-classic)for[provisioned throughput](../../openai/concepts/provisioned-throughput?view=foundry-classic)is compatible with agents.- For information on Class A subnet support, see the
[setup guide on GitHub](https://github.com/azure-ai-foundry/foundry-samples/tree/main/infrastructure/infrastructure-setup-bicep/15-private-network-standard-agent-setup). - The
[file search tool](../how-to/tools/file-search?view=foundry&preserve-view=true)is currently unavailable in the Italy North and Brazil South regions. - The gpt-5 models are available for the
[code interpreter](../how-to/tools/code-interpreter?view=foundry&preserve-view=true)and[file search](../how-to/tools/file-search?view=foundry&preserve-view=true)tools. [Registration](https://aka.ms/openai/gpt-5/2025-08-07)is required to use the gpt-5 models. Access is granted according to Microsoft's eligibility criteria.

| Region | gpt-5.2, 2025-12-11 | gpt-5.1, 2025-11-13 | gpt-5, 2025-08-07 | gpt-5-mini, 2025-08-07 | gpt-5-nano, 2025-08-07 | gpt-5-chat, 2025-08-07 | gpt-4.1, 2025-04-14 | gpt-4.1-nano, 2025-04-14 | gpt-4.1-mini, 2025-04-14 | gpt-4o, 2024-05-13 | gpt-4o, 2024-08-06 | gpt-4o, 2024-11-20 | gpt-4o-mini, 2024-07-18 | gpt-4, 0613 | gpt-4, turbo-2024-04-09 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
`australiaeast` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | |||
`brazilsouth` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | ||||||
`canadaeast` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | |||||
`eastus` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | |||||
`eastus2` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
`francecentral` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ||||||
`germanywestcentral` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ||||||
`italynorth` |
✅ | ✅ | ✅ | - | - | ✅ | ✅ | - | - | ||||||
`japaneast` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | |||
`norwayeast` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ||||||
`southafricanorth` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | ||||||
`southcentralus` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | |||||
`southindia` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ||||
`swedencentral` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
`switzerlandnorth` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | |||
`uksouth` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | |||
`westeurope` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | - | ✅ | ||||||
`westus` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ||||||
`westus3` |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

## Other model collections

The following lists of Foundry Models are available for your agents to use.

**Models sold directly by Azure:**

**MAI-DS-R1**: Deterministic, precision-focused reasoning.**grok-4**: Frontier-scale reasoning for complex, multiple-step problem solving.**grok-4-fast-reasoning**: Accelerated agentic reasoning optimized for workflow automation.**grok-4-fast-non-reasoning**: High-throughput, low-latency generation and system routing.**grok-3**: Strong reasoning for complex, system-level workflows.**grok-3-mini**: Lightweight model optimized for interactive, high-volume use cases.**Llama-3.3-70B-Instruct**: Versatile model for enterprise Q&A, decision support, and system orchestration.**Llama-4-Maverick-17B-128E-Instruct-FP8**: FP8-optimized model that delivers fast, cost-efficient inference.**DeepSeek-V3-0324**: Multimodal understanding across text and images.**DeepSeek-V3.1**: Enhanced multimodal reasoning and grounded retrieval.**DeepSeek-R1-0528**: Advanced long-form and multiple-step reasoning.**gpt-oss-120b**: Open-ecosystem model that supports transparency and reproducibility.

## View all agent-supported models in the Foundry portal

To see a full list of the supported models in the Foundry portal:

- Sign in to
[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. - Go to the
**Model catalog**. - Filter the models by
**Capabilities**and select**Agent supported**.

- Sign in to
[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. - Select
**Discover**in the upper-right navigation, then**Models**in the left pane. - Open the
**Capabilities**dropdown and select the**Agent supported**filter.

## Verify model support

Model availability can change over time.

- To verify what you can deploy for your project and region, use the Foundry portal model experience described in the previous section.
- If you use provisioned throughput, make sure you have provisioned throughput units (PTUs) available in the target region. For background, see
[Provisioned throughput](../../openai/concepts/provisioned-throughput?view=foundry-classic).

## Troubleshooting

### A model or version isn't available in your region

- Confirm you selected the right tab for your deployment type.
- Try a different region that supports the model and version.
- If you're using gpt-5 models, make sure your subscription has access. Some models require registration.

### File search isn't available

- File search isn't available in Italy North and Brazil South. Choose a supported region, or use a different tool.

### Provisioned throughput deployment fails

- Confirm you have enough PTUs available in the region.
- Review
[Provisioned throughput](../../openai/concepts/provisioned-throughput?view=foundry-classic)and[Spillover traffic management](../../openai/how-to/spillover-traffic-management?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/development-lifecycle -->

# Agent development lifecycle

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The agent building experience in Microsoft Foundry includes tools for development and observability, from agent creation to embedding your agent into your applications. You can use the Foundry portal or code to build, customize, and test your agent's behavior. You can then iterate with tracing, evaluation, and monitoring to improve quality and reliability. When you're ready, publish your agent as an agent application to share it and integrate it into your apps.

## Prerequisites

- A
[Microsoft Foundry project](../../how-to/create-projects?view=foundry) - Familiarity with the
[Agents playground](../../concepts/concept-playgrounds?view=foundry)

## Lifecycle at a glance

Use this lifecycle as a practical checklist while you build and ship an agent.

**Choose an agent type**: Start with a prompt-based agent, a workflow, or a hosted agent.**Create your agent and start testing**: Iterate in the playground or in code.**Add tools and data**: Attach tools for retrieval and actions, and validate the configuration before you save.**Save changes as versions**: Capture meaningful milestones and compare versions.**Debug with tracing**: Use tracing to confirm tool calls, latency, and end-to-end behavior. For details, see[Agent tracing overview](../../observability/concepts/trace-agent-concept?view=foundry).**Evaluate quality and safety**: Run repeatable evaluations to catch regressions before publishing. For conceptual guidance, see[Agent evaluators](../../concepts/evaluation-evaluators/agent-evaluators?view=foundry).**Publish and integrate**: Publish a stable endpoint and integrate it into your application. For steps, see[Publish and share agents in Microsoft Foundry](../how-to/publish-agent?view=foundry).**Monitor and iterate**: Monitor performance and quality in production, then update and republish as needed. For guidance, see[Monitor quality and safety](../../how-to/monitor-quality-safety?view=foundry).

## Types of agents

There are three types of agents:

**Prompt-based**: A prompt-based agent is a declaratively defined single agent that combines model configuration, instructions, tools, and natural language prompts to drive behavior. You can extend it by attaching tools for knowledge and memory. You can edit, version, test, evaluate, monitor, and publish prompt-based agents from the[Agents playground](../../concepts/concept-playgrounds?view=foundry)in the Foundry portal.**Workflow**: Use workflows to build a more advanced workflow that orchestrates a sequence of actions or coordinates multiple agents. Workflows have their own interface in the portal, but the same lifecycle applies. For details, see[Build a workflow in Microsoft Foundry](workflow?view=foundry).**Hosted**: Hosted agents are containerized agents that you build in code by using supported frameworks or custom code. Foundry Agent Service deploys and manages these agents. You don't edit hosted agents in the agent-building UI, but you can still invoke, evaluate, monitor, and publish them. For details, see[What are hosted agents?](hosted-agents?view=foundry)

You can create prompt-based agents and workflows in the Foundry portal or your own development environment by using the CLI, SDK, or REST API. For more information, see the [quickstart](../../quickstarts/get-started-code?view=foundry).

## Creating a prompt-based agent

If you already know what kind of agent you want to create, name it and then start configuring its model instructions and tools.

Note

After you name your agent, you can't change the name. In code, you refer to your agent by `<agent_name>:<version>`

.

## Develop in code

If you prefer to work in code, use supported ways to bring your agent code into a development environment from which you can test locally and then deploy to Azure.

From the **Code** tab in the agent playground's chat pane, you can take a code snippet that references your agent to a dedicated Visual Studio Code for the Web cloud environment. The snippet comes preconfigured with the packages and extensions that you need, along with instructions to efficiently develop and deploy your Foundry agent to Azure. You can also copy the code snippet directly to your preferred development environment. For details, see the [playground documentation](../../concepts/concept-playgrounds?view=foundry#open-in-vs-code-capability).

## Core capabilities for the agent development lifecycle

The agent building experience offers integrated experiences for each core step of the agent development lifecycle. Use these core capabilities as you develop your production-ready agent application. Each capability has in-depth documentation where you can learn more.

### Save changes as versions

After you create the first version of a prompt-based agent or a workflow, save subsequent changes as new versions. You can test unsaved changes in the agent playground. But if you want to view conversation history, monitor your agent's performance, or run full evaluations, you need to save your changes.

Agent versioning provides the following capabilities for managing agent configurations and iterations. This system ensures that all changes are tracked, testable, and comparable across versions.

**Version immutability**: Each version of an agent is immutable after you save it. Any modifications to an existing version require saving and creating a new version. This requirement helps ensure version integrity and prevents accidental overwrites.**Draft state management**: You can test agents in an unsaved state for experimentation. You lose unsaved changes if you leave the Foundry portal, so save frequently to preserve important modifications.**Version control operations**: You can direct requests to specific agent versions to enable controlled deployment and rollback capabilities.**Version history navigation**: You can access the version history for any agent, go to any specific version, and perform the following comparisons:- Agent setup comparison: Compare configuration settings between versions. You can choose which versions you want to compare by using the version dropdown list.
- Chat output comparison: Analyze response differences between agent versions by using identical inputs.
- YAML definition comparison: Review differences in agent definitions.


### Add tools

You can make your agent more powerful by giving it knowledge (specific files or indexes) or by allowing it to take actions (calling external APIs). Tools are available for most use cases, from simple file uploads to custom Model Context Protocol (MCP) server connections. For more complicated tools, you might need to configure authentication or add connections as part of attaching them to an agent.

To save an agent with a tool attached, you must successfully configure the tool. You can reuse configured tools across agents. For information about available tools, see the [tools catalog](tool-catalog?view=foundry).

### Debug and validate by using tracing

As you add tools and iterate on prompts, use tracing to validate end-to-end behavior:

- Confirm whether the agent called the tools you expected.
- Inspect tool inputs and outputs.
- Identify latency hotspots across model and tool calls.

For more information, see [Agent tracing overview](../../observability/concepts/trace-agent-concept?view=foundry).

### Evaluate quality and safety

Before you publish your agent (and after any meaningful change), run evaluations to catch regressions and measure quality consistently across versions.

- For the key evaluation dimensions for agents, see
[Agent evaluators](../../concepts/evaluation-evaluators/agent-evaluators?view=foundry). - For a code-first workflow you can automate, see
[Evaluate your AI agents locally](../../how-to/develop/agent-evaluate-sdk?view=foundry).

### Monitor after publishing

After you publish an agent application, treat it like production software:

- Monitor quality and safety signals.
- Review traces when behavior changes.
- Update and republish when you fix issues or make improvements.

For guidance, see [Monitor quality and safety](../../how-to/monitor-quality-safety?view=foundry).

### Plan for identity and permissions

Tools and downstream resources often require authentication. When you publish an agent, its identity and permission model can change. Make sure your published agent has only the access it needs.

For details, see [Agent identity concepts in Microsoft Foundry](agent-identity?view=foundry).

### Security and access

Treat your agent configuration like application code. Protect secrets and permissions throughout the lifecycle:

- Use least privilege and role assignments instead of embedding keys. For more information, see
[Role-based access control in Foundry portal](../../concepts/rbac-foundry?view=foundry). - Store secrets in a managed secret store and reference them through connections instead of hardcoding them in code, configuration files, or prompts. For guidance, see
[Set up a Key Vault connection](../../how-to/set-up-key-vault-connection?view=foundry). - Before publishing, confirm that the agent identity and tool connections in the published agent application have only the access they need. For details, see
[Agent identity concepts in Microsoft Foundry](agent-identity?view=foundry).

### Publish your agent or workflow

After you create an agent or workflow version that you're happy with, [publish it as an agent application](../how-to/publish-agent?view=foundry). You get a stable endpoint that you can open and test in the browser, share with others, or embed in your existing applications. You and your collaborators can validate performance and identify what needs refinement. You can make any necessary updates and republish a new version at any time.

## Common pitfalls

**Unsaved changes are temporary**: If you want to compare versions, view history, or run full evaluations, save your changes as a version.**Tools must be configured before saving**: If a tool requires authentication or a connection, complete setup before you save.**Publishing can require permission updates**: After publishing, recheck resource access for the published agent identity and remove any access the agent no longer needs.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/agent-to-agent-authentication -->

# Agent2Agent (A2A) authentication

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Most Agent2Agent (A2A) endpoints require authentication to access the endpoint and its underlying service. Authentication ensures only authorized users can invoke your A2A tools in Microsoft Foundry Agent Service (Agent Service).

In general, there are two authentication scenarios:

**Shared authentication**: Every user of your agent uses the same identity to authenticate to the A2A endpoint. Individual user context doesn't persist. For example, if you build a chat agent to retrieve information from Azure Cosmos DB for your organization, you might want every user to access the same shared container without signing in.**Individual authentication**: Each user of your agent authenticates with their own account so their user context persists. For example, if you build a coding agent that retrieves commits and pull requests from GitHub, you might want each developer to sign in with their own GitHub account.

## Prerequisites

Before you choose an authentication method, you need:

- Access to the
[Foundry portal](https://ai.azure.com/?cid=learnDocs)and a project. If you don't have one, see[Create projects in Foundry](../../how-to/create-projects?view=foundry). - Permissions to create project connections and configure agents. For details, see
[Role-based access control in the Foundry portal](../../concepts/rbac-foundry?view=foundry). - The A2A endpoint URL you want to connect to, and which authentication methods it supports.
- Credentials for your selected authentication method:
- Key-based: an API key, personal access token (PAT), or other token.
- Microsoft Entra authentication: role assignments for the agent identity or project managed identity on the underlying service.
- OAuth identity passthrough: a managed OAuth option from the endpoint publisher, or an OAuth app registration (custom OAuth).


## Choose an authentication method

Use the following guidance to choose a method:

| Your goal | Recommended method |
|---|---|
| Use one shared identity for all users | Key-based authentication or Microsoft Entra authentication |
| Preserve each user's identity and permissions | OAuth identity passthrough |
| Avoid managing secrets when the underlying service supports Microsoft Entra | Microsoft Entra authentication |
| Connect to an A2A endpoint that doesn't require auth | Unauthenticated access |

## Supported authentication methods

| Method | Description | User context persists |
|---|---|---|
| Key-based | Provide an API key or access token to authenticate with the A2A endpoint. | No |
| Microsoft Entra - agent identity | Use the agent identity to authenticate with the A2A endpoint. Assign the required roles on the underlying service. | No |
| Microsoft Entra - project managed identity | Use the project managed identity to authenticate with the A2A endpoint. Assign the required roles on the underlying service. | No |
| OAuth identity passthrough | Prompt users interacting with your agent to sign in and authorize access to the A2A endpoint. | Yes |
| Unauthenticated access | Use this method only when the A2A endpoint doesn't require authentication. | No |

## Key-based authentication

Note

People who have access to the project can access a secret stored in a project connection. Store only shared secrets in a project connection. For user-specific access, use OAuth identity passthrough.

Pass an API key, a personal access token (PAT), or other credentials to A2A endpoints that support key-based authentication. For improved security, store shared credentials in a project connection instead of passing them at runtime.

When you connect your A2A endpoint to an agent in the Foundry portal, Foundry creates a project connection for you. Provide the credential name and credential value. For example:

- Credential name:
`Authorization`

- Credential value:
`Bearer <your-token>`


When the agent invokes the A2A endpoint, Agent Service retrieves the credentials from the project connection and passes them to the A2A endpoint.

For security:

- Use least-privilege credentials where possible.
- Rotate tokens regularly.
- Restrict access to projects that contain shared secrets.

## Microsoft Entra authentication

Use Microsoft Entra authentication when the A2A endpoint and its underlying service accept Microsoft Entra tokens.

### Agent identity

Use your agent identity to authenticate with A2A endpoints that support agent identity authentication. If you create your agent by using Agent Service, you automatically assign an agent identity to it.

Before publishing, agents in the same project share a common identity. After you publish an agent, it gets a unique identity. For background and identity lifecycle details, see [Agent identity concepts in Microsoft Foundry](agent-identity?view=foundry).

Make sure the agent identity has the required role assignments on the underlying service that powers the A2A endpoint.

When the agent invokes the A2A endpoint, Agent Service uses the available agent identity to request an authorization token and passes it to the A2A endpoint.

### Foundry project managed identity

Use your Foundry project's managed identity to authenticate with A2A endpoints that support managed identity authentication.

Make sure the project managed identity has the required role assignments on the underlying service that powers the A2A endpoint.

When the agent invokes the A2A endpoint, Agent Service uses the project's managed identity to request an authorization token and passes it to the A2A endpoint.

## OAuth identity passthrough

Note

To use OAuth identity passthrough, users interacting with your agent need at least the **Azure AI User** role on the project.

OAuth identity passthrough is available for authentication to Microsoft and non-Microsoft A2A endpoints and underlying services that are compliant with OAuth, including Microsoft Entra.

Use OAuth identity passthrough to prompt users interacting with your agent to sign in to the A2A endpoint and its underlying service. Agent Service securely stores the user's credentials and uses them only within the context of the agent communicating with the A2A endpoint.

OAuth doesn't grant unlimited access to a user's data. Part of the protocol is specifying what the A2A endpoint can access and what it can do. For more information, see the [Microsoft security](https://www.microsoft.com/security/business/security-101/what-is-oauth) documentation.

When you use OAuth identity passthrough, the agent uses credentials from the user interacting with the agent to connect to the A2A endpoint. The first time a user interacts with the agent, Agent Service generates a consent link. After the user signs in and consents, the agent can discover and invoke tools on the A2A endpoint with that user's credentials.

The user's OAuth credentials are stored securely and scoped to the specific user and the specific agent they interacted with. These credentials typically include a refresh token and an access token.

An OAuth flow typically uses two tokens.

**Access token**

- Used to call APIs (for example Microsoft Graph, GitHub).
- Short-lived by design. Usually minutes to an hour (commonly 1 hour).
- Purpose: limit the damage if stolen.
- When it expires, the OAuth app can use a refresh token (if available) to get a new one.

**Refresh token**

- Used only to get new access tokens.
- Longer-lived. Can last hours, days, weeks, or even “until revoked” depending on server settings.
- Can often be revoked by the user (for example, using account settings).
- Some providers rotate refresh tokens each time they’re used (for extra security).

Agent Service supports two OAuth options: **managed OAuth** and **custom OAuth**.

- With managed OAuth, Microsoft or the A2A endpoint publisher manages the OAuth app.
- With custom OAuth, you bring your own OAuth app registration.

If you use custom OAuth, provide the required information, such as a client ID, client secret (if required), authorization URL, token URL, refresh URL, and requested scopes.

Note

If you use custom OAuth, you get a redirect URL. Add it to your OAuth app registration so Agent Service can complete the flow.

## Unauthenticated access

Use unauthenticated access only when the A2A endpoint doesn't require authentication.

## Set up authentication for an A2A connection

Identify the A2A endpoint you want to connect to and the authentication method it supports.

Create or select a project connection that stores the A2A endpoint URL, authentication method, and any required credentials.

- For general connection guidance, see
[Add a new connection to your project](../../how-to/connections-add?view=foundry). - For A2A-specific connection configuration and end-to-end A2A tool setup, see
[Add an A2A agent endpoint to Foundry Agent Service](../how-to/tools/agent-to-agent?view=foundry).

- For general connection guidance, see
Configure your agent to use the A2A tool and reference the project connection.


## Validate

- Trigger an A2A tool call from your agent.
- Confirm the tool call completes successfully.
- If you're using OAuth identity passthrough, confirm a new user gets a consent link and that subsequent calls succeed after the user consents.

## Troubleshooting

| Issue | Cause | Resolution |
|---|---|---|
| Key-based authentication fails | Invalid or expired token, or the endpoint expects a different header name or value format | Regenerate or rotate the credential and update the project connection. Confirm the required header name and value format in the endpoint documentation. |
| Microsoft Entra authentication fails | The identity doesn't have the required role assignments on the underlying service | Assign the required roles to the agent identity or project managed identity on the underlying service, and then try again. |
| Consent completes but tool calls still fail | The user doesn't have access in the underlying service | Confirm the user has access to the underlying service and has the Azure AI User role (or higher) on the project. |
| You don't get a consent link when you expect one | OAuth identity passthrough isn't configured for the connection, or the agent didn't invoke the A2A tool | Confirm the project connection is configured for OAuth identity passthrough and trigger an A2A tool call again. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/tool-catalog -->

# Discover and manage tools in the Foundry tool catalog (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Foundry Tools is the place to discover and manage tools you use with agents and workflows in Microsoft Foundry.

Note

This feature is currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

You can use Foundry Tools to:

- Discover tools such as Model Context Protocol (MCP) servers and built-in tools.
- Configure tools once, then add them to agents or workflows.
- Filter, search, and sort tools.

## Prerequisites

To use Foundry Tools, you need:

- Access to a Foundry project in the Foundry portal.
- Permission to view and manage tools in that project.

## Where to find Foundry Tools

In the Foundry portal, go to your project and then select **Build** > **Tools**.

## Key concepts

Use these definitions to keep the terminology consistent:

| Term | Meaning |
|---|---|
| Foundry Tools | The portal experience where you discover, configure, and manage tools for agents and workflows. |
| Tool catalog | The browsable list of available tools (public and organizational). |
| Private tool catalog | An organization-scoped catalog for tools that only users in your organization can discover and configure. |
| MCP server | A server that exposes tools using the Model Context Protocol (MCP). |
| Remote MCP server | An MCP server hosted by the publisher. You configure it by providing the required settings (for example, an endpoint and authentication details). |
| Local MCP server | An MCP server you host yourself, then connect to Foundry by providing its remote endpoint. |
| Custom tool | A tool you add by providing your own endpoint or specification (for example, an MCP endpoint, an OpenAPI spec, or Agent-to-Agent (A2A) endpoints). |

Note

If you're interested in bringing your official, remote MCP server(s) to all Foundry customers, fill out this [form](https://forms.office.com/r/EEvMNceMRU).

## Considerations for using non-Microsoft services and servers

Your use of connected non-Microsoft services and servers ("non-Microsoft services") is subject to the terms between you and the service provider. Non-Microsoft services are non-Microsoft products under your agreement governing use of Microsoft online services. When you connect to non-Microsoft services, some of your data (such as prompt content) is sent to the non-Microsoft service, or your application might receive data from the non-Microsoft service. You're responsible for your use of non-Microsoft services and data, along with any charges associated with that use.

Third parties (not Microsoft) create the non-Microsoft services, including remote MCP servers, that you choose to connect. Microsoft doesn't test or verify these servers. Microsoft has no responsibility to you or others in relation to your use of any non-Microsoft services.

Carefully review and track the MCP servers you add to Foundry Agent Service. Rely on servers hosted by trusted service providers themselves rather than proxies.

The MCP tool can pass custom headers that a remote MCP server might require for authentication. Treat any credentials as secrets:

- Only provide the minimum required headers.
- Don't include credentials in prompts.
- If you log requests for auditing, avoid logging secrets or sensitive prompt content.
- Review the provider's data handling practices, including retention and data location.

## Foundry Tools and private tools catalog

Foundry provides both Foundry Tools and private tool catalogs.

Foundry Tools includes a curated list of tools available for building agents. If you need tools that are only visible within your organization, create a [private tool catalog](../how-to/private-tool-catalog?view=foundry).

## Find the right tools in Foundry Tools

### Tool types

Foundry Tools includes three types of tool catalog entries:

**Remote MCP server**: The MCP server publisher has already hosted the server and provided a static or dynamic MCP server endpoint. Foundry developers need to follow the configuration guidance to provide the appropriate information to finish the setup.

**Local MCP server**: The publisher doesn't host the server. You host it, then connect it to Foundry by providing its endpoint. To build and register your own server, see [Build and register a Model Context Protocol (MCP) server](../../mcp/build-your-own-mcp-server?view=foundry). To connect an MCP endpoint to an agent, see [Connect to Model Context Protocol servers](../how-to/tools/model-context-protocol?view=foundry).

**Custom**: These MCP servers are converted from Azure Logic App Connectors. Foundry developers need additional [configuration](https://aka.ms/FoundryCustomTool) to convert to remote MCP servers.

### Filter and search

Foundry Tools provides the following filters to help you find the right tools for your agents:

| Filter | Description |
|---|---|
| Publisher | Microsoft or non-Microsoft publisher |
| Category | Categories such as databases, analytics, web, and more |
| Registry | Public: Public remote and local MCP servers in the catalogLogic Apps connectors: Azure Logic Apps connectors that you convert to remote MCP servers for use in a private tool catalog. |
| Supported authentication | Authentication method an MCP server supports. For more information, see
|

When you select a tool, Foundry Tools shows the setup details you need to configure it.

## Availability and limitations

Tool availability can vary by model and region.

For the latest model and region support details across tools, see [Best practices for using tools in Microsoft Foundry Agent Service](tool-best-practice?view=foundry).

## Manage tools you've configured

In your tools list, you can find the tools you've configured, along with details such as endpoints and authentication settings. You can also add tools to agents and workflows.

Before you delete a tool, check which agents or workflows use it. Deleting a tool can break runs that depend on it.

To explore tools while you build, use the Agents playground. For more information, see [Microsoft Foundry Playgrounds](../../concepts/concept-playgrounds?view=foundry).

Foundry Tools contains three sections:

**Configured**: Configured tools are ready to use because you've completed their setup (authentication and required settings). Built-in tools include:Tool Description [Azure AI Search](../how-to/tools/ai-search?view=foundry)Use an existing Azure AI Search index to ground agents with data in the index, and chat with your data. [Browser Automation (preview)](../how-to/tools/browser-automation?view=foundry)Perform real-world browser tasks through natural language prompts. [Code Interpreter](../how-to/tools/code-interpreter?view=foundry)Enable agents to write and run Python code in a sandboxed execution environment. [Custom Code Interpreter (preview)](../how-to/tools/custom-code-interpreter?view=foundry)Use a custom code interpreter MCP server to customize resources, available Python packages, and the Container Apps environment the agent uses. [Computer Use (preview)](../how-to/tools/computer-use?view=foundry)Specialized tool that uses a model that can perform tasks by interacting with computer systems and applications through their user interfaces. [File Search](../how-to/tools/file-search?view=foundry)Augment agents with knowledge from outside its model, such as proprietary product information or documents provided by your users. [Grounding with Bing tools](../how-to/tools/bing-tools?view=foundry)Enable your agent to use Grounding with Bing Search to access and return information from the internet. [Image Generation (preview)](../how-to/tools/image-generation?view=foundry)Enable image generation as part of conversations and multi-step workflows. [Microsoft Fabric (preview)](../how-to/tools/fabric?view=foundry)Integrate your agent with the [Microsoft Fabric data agent](https://go.microsoft.com/fwlink/?linkid=2312815)to unlock powerful data analysis capabilities.[SharePoint (preview)](../how-to/tools/sharepoint?view=foundry)Integrate your agents with Microsoft SharePoint to chat with your private documents securely. [Web Search (preview)](../how-to/tools/web-search?view=foundry)Enable models to retrieve and ground responses with real-time information from the public web before generating output. **Catalog**: Available from the public or organizational Foundry Tool Catalog, including remote and local MCP servers and Azure Logic Apps connectors, which may require setup before use.**Custom**: These allow you to bring your own APIs using remote MCP server endpoints, A2A endpoints, OpenAPI 3.0 specs, or functions.Tool Description [Model Context Protocol (preview)](../how-to/tools/model-context-protocol?view=foundry)Give the agent access to tools hosted on an existing MCP endpoint. [OpenAPI 3.0 specified tool](../how-to/tools/openapi?view=foundry)Connect your Foundry agents to external APIs using functions with an OpenAPI 3.0 specification. [Agent-to-Agent tool (preview)](../how-to/tools/agent-to-agent?view=foundry)Connect your Foundry agents to other agents through A2A-compatible endpoints.

## Troubleshooting

Use these checks to resolve common issues:

**You can't find the tool catalog**: Confirm you're in the correct project, then go to**Build**>**Tools**.**A tool is visible but you can't configure it**: Review the tool's required authentication and configuration inputs, and verify you have access to any dependent services.**Your agent doesn't call a tool**: Use the validation guidance in[Best practices for using tools in Microsoft Foundry Agent Service](tool-best-practice?view=foundry).

## Related content

[Create a private tool catalog](../how-to/private-tool-catalog?view=foundry)[Connect to Model Context Protocol servers](../how-to/tools/model-context-protocol?view=foundry)[Build and register a Model Context Protocol (MCP) server](../../mcp/build-your-own-mcp-server?view=foundry)[Foundry MCP Server best practices and security guidance](../../mcp/security-best-practices?view=foundry)[Get started with Foundry MCP Server (preview) using Visual Studio Code](../../mcp/get-started?view=foundry)[Bring your remote, official MCP server to all Foundry customers](https://forms.office.com/r/EEvMNceMRU)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/tool-best-practice -->

# Tool best practices for Microsoft Foundry Agent Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Tools help your agent retrieve information, take actions, and use external capabilities (such as retrieval, search, and API calls). Use the guidance in this article to choose tools, improve tool-calling reliability, and protect sensitive data.

Tip

In your agent instructions, describe what each tool is for and when to use it. For example:

`When you need information from my indexed documents, use File Search. When you need to call an API, use the OpenAPI tool. When a tool call fails or returns no results, explain what happened and ask a follow-up question.`


## Prerequisites

- Access to a Foundry project in the Foundry portal.
- A model deployed in the same project.
- Any required connections configured for the tools you plan to use (for example, Azure AI Search, SharePoint, or Bing grounding).

## Configure and validate tool usage

- Configure tools and connections in the Foundry tool catalog. See
[Discover and manage tools in the Foundry tool catalog (preview)](tool-catalog?view=foundry). - Review run traces to confirm when your agent calls tools and to inspect tool inputs and outputs. For end-to-end tracing setup, see
[Trace your application](../../how-to/develop/trace-application?view=foundry).

## Improve tool-calling reliability

### Control tool calling with `tool_choice`


`tool_choice`

is the most deterministic way to control whether the model calls a tool.

`auto`

: The model decides whether to call tools.`required`

: The model must call one or more tools.`none`

: The model does not call tools.

For details, see `tool_choice`

in [Foundry project REST (preview)](../../reference/foundry-project-rest-preview?view=foundry).

### Write effective tool instructions

- Keep instructions specific and consistent with your tool setup.
- Tell the model what each tool is for.
- If you have multiple tools that overlap, add a decision rule (for example, “Use File Search before Web Search for internal content.”).

## Secure tool usage

Tools can send and receive data outside the model. Use these practices to reduce security and privacy risks:

- Treat tool outputs as untrusted input and validate critical values before acting on them.
- Send only the information required to complete the task.
- Don’t include keys, tokens, or other credentials in prompts.
- Avoid logging secrets in traces or application logs.
- If you connect to non-Microsoft services (for example, third-party MCP servers), review the considerations in
[Discover and manage tools in the Foundry tool catalog (preview)](tool-catalog?view=foundry). - If you need centralized routing and policy enforcement for MCP tools, see
[Tools governance with AI Gateway (preview)](../how-to/tools/governance?view=foundry).

## Tool support by region and model

Tool availability depends on both **region** and **model**.

**How to use the tables**:

**Yes**/**yes**: Supported.**No**/**no**: Not supported.**Limited**: Partially supported (capability depends on the tool and model).

Tools are available in the following [regions](../../openai/how-to/responses?view=foundry#region-availability) with the following limitations.

Note

This region availability table only accounts for service availability. You need to make sure the model you want to use is also available in the same region.

| Region Name | Agent2Agent | Azure AI Search | Browser Automation | Code Interpreter | Computer Use | Fabric Data Agent | File Search | Function | Grounding with Bing Custom Search | Grounding with Bing Search | Image Generation | MCP | OpenAPI | SharePoint | Web Search |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| australiaeast | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| brazilsouth | yes | yes | yes | yes | no | yes | yes | no | yes | yes | yes | yes | yes | yes | yes |
| canadaeast | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| eastus | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| eastus2 | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| francecentral | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| germanywestcentral | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| italynorth | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| japaneast | yes | yes | yes | no | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| koreacentral | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| northcentralus | yes | yes | yes | yes | no | yes | yes | no | yes | yes | yes | yes | yes | yes | yes |
| norwayeast | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| polandcentral | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| southafricanorth | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| southcentralus | yes | yes | yes | no | no | yes | yes | no | yes | yes | yes | yes | yes | yes | yes |
| southeastasia | yes | yes | yes | no | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| southindia | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| spaincentral | yes | yes | yes | no | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| swedencentral | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| switzerlandnorth | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| uaenorth | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| uksouth | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |
| westus | yes | yes | yes | yes | no | yes | yes | no | yes | yes | yes | yes | yes | yes | yes |
| westus3 | yes | yes | yes | yes | no | yes | yes | yes | yes | yes | yes | yes | yes | yes | yes |

Tools are supported by the following models.

Note

For the image generation tool, you need both the `gpt-image-1`

model and a large language model (LLM) as the orchestrator in the same Microsoft Foundry project.

| Model | agent2agent | Azure AI Search | Browser Automation | Code Interpreter | Computer Use | Fabric Data Agent | File Search | Function | Grounding Bing Custom | Grounding Bing Search | Image Generation | MCP | OpenAPI | SharePoint | Web Search |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| gpt-5 | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| gpt-5-mini | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| gpt-5-nano | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| gpt-5-chat | No | No | No | No | No | No | Yes | No | No | No | No | No | No | No | No |
| gpt-5-pro | Yes | Yes | Yes | No | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| o4-mini | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| o3 | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| o3-mini | Yes | Yes | Yes | No | No | Yes | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes |
| o1 | Yes | Yes | Yes | No | No | Yes | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes |
| computer-use-preview | No | No | No | No | Yes | No | No | No | No | No | No | No | No | No | No |
| gpt-4.1 | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| gpt-4.1-mini | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| gpt-4.1-nano | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| gpt-4o | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| gpt-4o-mini | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| gpt-image-1 | No | No | No | No | No | No | No | No | No | No | Yes | No | No | No | No |
| DeepSeek-V3.0324 | No | Limited | No | Yes | No | Limited | Yes | Yes | Limited | Limited | No | Limited | No | Limited | No |
| DeepSeek-V3.1 | No | Limited | No | Yes | No | Limited | No | No | Limited | Limited | No | Limited | No | Limited | No |
| Llama-3.3-70B-Instruct | No | No | No | Yes | No | No | Yes | No | No | No | No | No | No | No | No |
| Llama-4-Maverick-178-128E-Instr | No | Limited | No | No | No | Limited | Yes | Yes | Limited | Limited | No | Limited | No | Limited | No |
| grok-3-mini | No | Limited | No | No | No | Limited | No | Yes | Limited | Limited | No | Limited | No | Limited | No |
| grok-4-fast-non-reasoning | No | Limited | No | No | No | Limited | No | Yes | Limited | Limited | No | Limited | No | Limited | No |
| grok-4-fast-reasoning | No | Limited | No | No | No | Limited | No | Yes | Limited | Limited | No | Limited | No | Limited | No |

## Troubleshooting

Use these checks to resolve common issues:

**Your agent doesn’t call a tool**:- Confirm the tool is attached to the agent.
- Confirm the model supports the tool.
- If you need deterministic behavior, set
`tool_choice`

to`required`

. - Review run traces to confirm whether the model produced a tool call.

**Tool calls return empty or irrelevant results**:- Improve tool descriptions and agent instructions.
- For retrieval tools, ensure your data is ingested and searchable.

**Tool calls fail**:- Verify tool configuration and authentication.
- For MCP and OpenAPI tools, validate the endpoint is reachable and returns expected responses.


## FAQ

**How do I validate whether a tool was called?**

Review run traces to confirm whether your agent called a tool and to inspect tool inputs and outputs. For end-to-end tracing setup, see [Trace your application](../../how-to/develop/trace-application?view=foundry).

**How do I make tool usage more reliable?**

Start with clear tool instructions. If you need deterministic tool calling, use `tool_choice`

. For details, see [Control tool calling with tool_choice](#control-tool-calling-with-tool_choice).

## Related content

[Discover and manage tools in the Foundry tool catalog (preview)](tool-catalog?view=foundry)[Tools governance with AI Gateway (preview)](../how-to/tools/governance?view=foundry)- Tool how-tos:
[Azure AI Search](../how-to/tools/ai-search?view=foundry)[File search](../how-to/tools/file-search?view=foundry)[Web search (preview)](../how-to/tools/web-search?view=foundry)[Grounding with Bing tools](../how-to/tools/bing-tools?view=foundry)[SharePoint (preview)](../how-to/tools/sharepoint?view=foundry)[Fabric data agent (preview)](../how-to/tools/fabric?view=foundry)[Model Context Protocol (MCP) (preview)](../how-to/tools/model-context-protocol?view=foundry)[OpenAPI tool](../how-to/tools/openapi?view=foundry)[Function calling](../how-to/tools/function-calling?view=foundry)[Code interpreter](../how-to/tools/code-interpreter?view=foundry)[Browser automation (preview)](../how-to/tools/browser-automation?view=foundry)[Computer Use (preview)](../how-to/tools/computer-use?view=foundry)[Image generation (preview)](../how-to/tools/image-generation?view=foundry)[Agent2Agent (A2A) tool (preview)](../how-to/tools/agent-to-agent?view=foundry)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/workflow -->

# Build a workflow in Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Workflows are UI-based tools in Microsoft Foundry. Use them to create declarative, predefined sequences of actions that orchestrate agents and business logic in a visual builder.

Workflows enable you to build intelligent automation systems that seamlessly blend AI agents with business processes in a visual manner. Traditional single-agent systems are limited in their ability to handle complex, multifaceted tasks. By orchestrating multiple agents, each with specialized skills or roles, you can create systems that are more robust, adaptive, and capable of solving real-world problems collaboratively.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - A project in Microsoft Foundry. For more information, see
[Create projects](../../how-to/create-projects?view=foundry). - Access to create and run workflows in your Foundry project. For more information, see
[Azure role-based access control (RBAC) in Foundry](../../concepts/rbac-foundry?view=foundry).

## When to use workflows

Use workflows when you want to:

- Orchestrate multiple agents in a repeatable process.
- Add branching logic (for example, if/else) and variable handling without writing code.
- Create human-in-the-loop steps (for example, approvals or clarifying questions).

If you want to edit workflow YAML in Visual Studio Code or run workflows in a local playground, see:

[Work with Declarative (Low-code) Agent workflows in Visual Studio Code](../how-to/vs-code-agents-workflow-low-code?view=foundry)[Work with Hosted (Pro-code) Agent workflows in Visual Studio Code](../how-to/vs-code-agents-workflow-pro-code?view=foundry)

## Workflow concepts

To create a workflow in Foundry, you can begin with a blank workflow or select one of the templates of predefined orchestration patterns:

| Pattern | Description | Typical use case |
|---|---|---|
| Human in the loop | Asks the user a question and awaits user input to proceed | Creating approval requests during workflow execution and waiting for human approval, or obtaining information from the user |
| Sequential | Passes the result from one agent to the next in a defined order | Step-by-step workflows, pipelines, or multiple-stage processing |
| Group chat | Dynamically passes control between agents based on context or rules | Dynamic workflows, escalation, fallback, or expert handoff scenarios |

For more information, see [Microsoft Agent Framework workflow orchestrations](/en-us/agent-framework/user-guide/workflows/orchestrations/overview).

## Create a workflow

The following steps show you how to create a sequential type of workflow as an example:

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. On the upper-right menu, select

**Build**.Select

**Create new workflow**>**Sequential**.Assign an agent to the agent nodes by selecting each agent node in the workflow and either selecting the desired agent or creating a new one. For more information, see

[Add agents to your workflow](#add-agents-to-your-workflow)later in this article.Select

**Save**in the visualizer to save the changes.Important

Workflows aren't saved automatically. Select

**Save**every time you want to save changes to your workflow.Select

**Run Workflow**.Interact with the workflow in the chat window.

Optionally, add new nodes to your workflow. The next section in this article provides information about nodes.


## Verify your workflow run

After you select **Run Workflow**, verify that:

- Each node completes in the visualizer.
- You see the expected responses in the chat window.
- Any variables you save (for example, JSON output from an agent node) contain the values you expect.

## Add nodes to your workflow

Nodes define the building blocks of your workflow. Common node types include:

**Agent**: Invoke an agent.**Logic**: Use*if/else*,*go to*, or*for each*.**Data transformation**: Set a variable or parse a value.**Basic chat**: Send a message or ask a question to an agent.

When you select a prebuilt workflow, a workflow of nodes appears in the builder. Each node corresponds to a specific action or component, and it performs a step in sequence. You can modify the order of the nodes by selecting the three dots on a node and then selecting **move**. You can add new nodes by selecting the plus (**+**) icon in the workspace.

## Add agents to your workflow

You can add any Foundry agent from your project to the workflow. Agent nodes also allow you to create new agents and give them customized capabilities by configuring their model, prompt, and tools.

For advanced options and comprehensive information about agent creation, go to the **Foundry Agent** tab in the Foundry portal.

### Add an existing agent

In the workflow visualizer, select the plus sign.

In the pop-up dropdown list, select

**Invoke agent**.In the

**Create new agent**window, select**existing**.Enter the agent name to search for existing agents in your Foundry project.

Select the desired agent to add it into your workflow.


### Create a new agent

In the workflow visualizer, select the plus sign.

In the pop-up dropdown list, select

**Invoke agent**.Enter an agent name and description of what the agent does.

Select

**Add**.In the

**Invoke an agent**window, configure the agent.Select

**Save**.

### Configure an output response format for invoking an agent

Create an

**Invoke agent**node.In the

**Invoke agent**configuration window, select**Create a new agent**.Configure the agent to send output as a JSON schema:

- Select
**Details**. - Select the parameter icon.
- For
**Text format**, select**JSON Schema**.

- Select
Copy the desired JSON schema and paste it in the

**Add response format**window. The following screenshot shows a math example. Select**Save**.

Important

Don't include secrets (passwords, keys, tokens) in JSON schemas, prompts, or saved workflow variables.

```
{
"name": "math_response",
"schema": {
"type": "object",
"properties": {
"steps": {
"type": "array",
"items": {
"type": "object",
"properties": {
"explanation": {
"type": "string"
},
"output": {
"type": "string"
}
},
"required": [
"explanation",
"output"
],
"additionalProperties": false
}
},
"final_answer": {
"type": "string"
}
},
"additionalProperties": false,
"required": [
"steps",
"final_answer"
]
},
"strict": true
}
```


Select

**Action settings**. Then select**Save output json_object/json_schema as**.Select

**Create new variable**. Choose a variable name, and then select**Done**.

## Use additional features

**YAML visualizer view**: When you set the**YAML Visualizer View**toggle to**On**, the workflow is stored in a YAML file. You can modify it in the visualizer and the YAML view. Saving creates a new version, and you have access to the version history.The visualizer and the YAML are editable. Any changes to the YAML file are reflected in the visualizer.

**Versioning**: Each time you save your workflow, a new, unchangeable version is created. To view the version history or delete older versions, open the**Version**dropdown list to the left of the**Save**button.**Notes on your workflow visualizer**: You can add notes on the workflow visualizer to add more context or information for your workflow. In the upper-left corner of the workflow visualizer, select**Add note**.

## Create expressions by using Power Fx

Power Fx is a low-code language that uses Excel-like formulas. Use Power Fx to create complex logic that allows your agents to manipulate data. For instance, a Power Fx formula can set the value of a variable, parse a string, or use an expression in a condition. For more information, see the [Power Fx overview](/en-us/power-platform/power-fx/overview) and [formula reference](/en-us/power-platform/power-fx/formula-reference-copilot-studio).

### Use variables in a formula

To use a variable in a Power Fx formula, you must add a prefix to its name to indicate the variable's scope:

- For system variables, use
`System.`

- For local variables, use
`Local.`


Here are the system variables:

| Name | Description |
|---|---|
`Activity` |
Information about the current activity |
`Bot` |
Information about the agent |
`Conversation` |
Information about the current conversation |
`Conversation.Id` |
Unique ID of the current conversation |
`Conversation.LocalTimeZone` |
Time zone of the user, in the IANA Time Zone Database format |
`Conversation.LocalTimeZoneOffset` |
Time offset from UTC for the current local time zone |
`Conversation.InTestMode` |
Boolean flag that represents if the conversation is happening on a test canvas |
`ConversationId` |
Unique ID of the current conversation |
`InternalId` |
Internal identifier for the system |
`LastMessage` |
Information about the previous message that the user sent |
`LastMessage.Id` |
ID of the previous message that the user sent |
`LastMessage.Text` |
Previous message that the user sent |
`LastMessageId` |
ID of the previous message that the user sent |
`LastMessageText` |
Previous message that the user sent |
`Recognizer` |
Information about intent recognition and the triggering message |
`User` |
Information about the user currently talking to the agent |
`User.Language` |
User language locale per conversation |
`UserLanguage` |
User language locale per conversation |

### Use literal values in a formula

In addition to using variables in a Power Fx formula, you can enter literal values. To use a literal value in a formula, you must enter it in the format that corresponds to its [type](/en-us/microsoft-copilot-studio/authoring-variables-about?tabs=webApp).

The following table lists the data types and the format of their corresponding literal values:

| Type | Format examples |
|---|---|
| String | `"hi"` , `"hello world!"` , `"copilot"` |
| Boolean | Only `true` or `false` |
| Number | `1` , `532` , `5.258` ,`-9201` |
| Record and table | `[1]` , `[45, 8, 2]` , `["cats", "dogs"]` , `{ id: 1 }` , `{ message: "hello" }` , `{ name: "John", info: { age: 25, weight: 175 } }` |
| Date and time | `Time(5,0,23)` , `Date(2022,5,24)` , `DateTimeValue("May 10, 2022 5:00:00 PM")` |
| Choice | Not supported |
| Blank | Only `Blank()` |

#### Common Power Fx formulas

The following table lists the Power Fx formulas that you can use with each data type.

| Type | Power Fx formulas |
|---|---|
| String | `[Text function][1]` `[Concat and Concatenate functions][2]` `[Len function][3]` `[Lower, Upper, and Proper functions][4]` `[IsMatch, Match, and MatchAll functions][5]` `[EndsWith and StartsWith functions][6]` `[Find function][7]` `[Replace and Substitute function][8]` |
| Boolean | `[Boolean function][9]` `[And, Or, and Not functions][10]` `[If and Switch functions][11]` |
| Number | `[Decimal, Float, and Value functions][12]` `[Int, Round, RoundDown, RoundUp, and Trunc functions][13]` |
| Record and table | `[Concat and Concatenate functions][14]` `[Count, CountA, CountIf, and CountRows functions][15]` `[ForAll function][16]` `[First, FirstN, Index, Last, and LastN functions][17]` `[Filter, Search, and LookUp functions][18]` `[JSON function][19]` `[ParseJSON function][20]` |
| Date and time | `[Date, DateTime, and Time functions][21]` `[DateValue, TimeValue, and DateTimeValue functions][22]` `[Day, Month, Year, Hour, Minute, Second, and Weekday functions][23]` `[Now, Today, IsToday, UTCNow, UTCToday, IsUTCToday functions][24]` `[DateAdd, DateDiff, and TimeZoneOffset functions][25]` `[Text function][26]` |
| Blank | `[Blank, Coalesce, IsBlank, and IsEmpty functions][27]` `[Error, IfError, IsError, IsBlankOrError functions][28]` |

### Use Power Fx to set a variable

In this example, a Power Fx expression stores and outputs the customer's name in capital letters:

Create a workflow and add an

**Ask a question**node.On the pane that appears, in the

**Ask a question**box, enter**What is your name?**or another message. In the**Save user response as**box, enter a variable name; for example,`Var01`

. Then select**Done**.Add a

**Send message**action. On the pane that appears, in the**Message to send**area, enter`{Upper(Local.Var01)}`

. Then select**Done**.Select

**Preview**.On the preview pane, send a message to the agent to invoke the workflow.


## Use Power Fx to create if/else flows

In this example, you add an if/else flow and build a condition by using system variables.

Create a workflow and add an

**Ask a question**node.Select the

**+**icon and add an**if/else**flow.Type

`System.`

in the**Condition**box to build a condition statement for each if/else branch.Select a

**Next Action**for the next step in the workflow.Select

**Done**. Select**Save**to save your workflow.

## Troubleshooting

- If you don't see
**Workflows**or you can't create or edit workflows, confirm your project access and permissions. See[Azure role-based access control (RBAC) in Foundry](../../concepts/rbac-foundry?view=foundry). - If your changes don't appear, confirm you selected
**Save**in the visualizer. - If a workflow run doesn't produce the output you expect, verify that each agent node has an agent assigned and that any saved outputs (for example, JSON schema outputs) are valid.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/capability-hosts -->

# Capability hosts

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Note

Updating capability hosts is not supported. To modify a capability host, you must delete the existing one and recreate it with the new configuration.

Capability hosts are sub-resources that you configure at both the Microsoft Foundry account and Foundry project scopes. They tell Foundry Agent Service where to store and process agent data, including:

**Conversation history (threads)****File uploads****Vector stores**

## Prerequisites

- A
[Microsoft Foundry project](../../how-to/create-projects?view=foundry-classic) - If you use your own resources for agent data (standard agent setup), create the required Azure resources and connections:
- Permissions to create the resources and, for standard agent setup, assign access to the required Azure resources. For details, see
[Required permissions](../environment-setup?view=foundry-classic#required-permissions)and[Role-based access control (RBAC) in Microsoft Foundry](../../concepts/rbac-foundry?view=foundry-classic).

## Why use capability hosts?

Capability hosts allow you to **bring your own Azure resources** instead of using the default Microsoft-managed platform resources. This gives you:

**Data sovereignty**- Keep all agent data within your Azure subscription.**Security control**- Use your own storage accounts, databases, and search services.**Compliance**- Meet specific regulatory or organizational requirements.

## How do capability hosts work?

Creating capability hosts isn't required. If you want agents to use your own Azure resources, create capability hosts at both the account and project scopes.

### Default behavior (Microsoft-managed resources)

If you don't create an account-level and project-level capability host, the Agent Service automatically uses Microsoft-managed Azure resources for:

- Thread storage (conversation history, agent definitions)
- File storage (uploaded documents)
- Vector search (embeddings and retrieval)

### Bring-your-own resources

When you create capability hosts at both the account and project levels, agent data is stored and processed using your Azure resources in your subscription. This configuration is called **standard agent setup**. For network-secured standard agent setup, deploy all related resources in the same region as your virtual network (VNet). For guidance, see [Create a new network-secured environment with user-managed identity](../how-to/virtual-networks?view=foundry-classic).

To learn more about standard agent setup, see [Built-in enterprise readiness with standard agent setup](standard-agent-setup?view=foundry-classic).

Note

We recommend using separate Foundry accounts and projects for standard agent setup and basic agent setup. Avoid mixing setup types within the same Foundry account.

#### Configuration hierarchy

Capability hosts follow a hierarchy where more specific configurations override broader ones:

**Service defaults**(Microsoft-managed search and storage) - Used when no capability host is configured.**Account-level capability host**- Provides shared defaults for all projects under the account.**Project-level capability host**- Overrides account-level and service defaults for that specific project.

## Understand capability host constraints

When creating capability hosts, be aware of these important constraints to avoid conflicts:

**One capability host per scope**: Each account and each project can only have one active capability host. Attempting to create a second capability host with a different name at the same scope will result in a 409 conflict.**Configuration updates are not supported**: If you need to change configuration, you must delete the existing capability host and recreate it.

## Create connections for capability hosts

Capability hosts reference connection names that you create in your Foundry account and project. Before you configure a project capability host for standard agent setup, create connections for the resources that store agent data:

**Thread storage**: Azure Cosmos DB connection**File storage**: Azure Storage connection**Vector store**: Azure AI Search connection

If you want to use model deployments from your own Azure OpenAI resource, also create an Azure OpenAI connection.

To add connections in the Foundry portal, see [Add a new connection to your project](../../how-to/connections-add?view=foundry-classic).

## Configure capability hosts

### Required properties (project capability host)

To use your own resources for agent data (standard agent setup), configure the project capability host with the following properties:

| Property | Purpose | Required Azure resource | Example connection name |
|---|---|---|---|
`threadStorageConnections` |
Stores agent definitions, conversation history and chat threads | Azure Cosmos DB | `"my-cosmosdb-connection"` |
`vectorStoreConnections` |
Handles vector storage for retrieval and search | Azure AI Search | `"my-ai-search-connection"` |
`storageConnections` |
Manages file uploads and blob storage | Azure Storage Account | `"my-storage-connection"` |

### Optional property

| Property | Purpose | Required Azure resource | When to use |
|---|---|---|---|
`aiServicesConnections` |
Use your own model deployments | Azure OpenAI | When you want to use models from your existing Azure OpenAI resource instead of the built-in account level ones. |

**Account capability host**

Use an account capability host to enable Agent Service and (optionally) define defaults that projects can inherit.

```
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/capabilityHosts/{name}?api-version=2025-06-01
{
"properties": {
"capabilityHostKind": "Agents"
}
}
```


Reference: [Foundry account management REST API](/en-us/rest/api/aifoundry/accountmanagement/operation-groups)

**Project capability host**

This configuration overrides service defaults and any account-level settings. All agents in this project will use your specified resources:

```
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/projects/{projectName}/capabilityHosts/{name}?api-version=2025-06-01
{
"properties": {
"capabilityHostKind": "Agents",
"threadStorageConnections": ["my-cosmos-db-connection"],
"vectorStoreConnections": ["my-ai-search-connection"],
"storageConnections": ["my-storage-account-connection"],
"aiServicesConnections": ["my-azure-openai-connection"]
}
}
```


Reference: [Project Capability Hosts - Create or update](/en-us/rest/api/aifoundry/accountmanagement/project-capability-hosts/create-or-update)

### Optional: account-level defaults with project overrides

Set shared defaults at the account level that apply to all projects:

```
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/capabilityHosts/{name}?api-version=2025-06-01
{
"properties": {
"capabilityHostKind": "Agents",
"threadStorageConnections": ["shared-cosmosdb-connection"],
"vectorStoreConnections": ["shared-ai-search-connection"],
"storageConnections": ["shared-storage-connection"]
}
}
```


Note

All Foundry projects will inherit these settings. Then override specific settings at the project level as needed.

## Verify your configuration

Use these steps to confirm that capability hosts are configured the way you expect:

Get the account capability host and confirm it exists.

`GET https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/capabilityHosts?api-version=2025-06-01`

Get the project capability host and confirm it references the expected connection names.

`GET https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/projects/{projectName}/capabilityHosts?api-version=2025-06-01`

If you update connections or want to change where data is stored, delete and recreate the capability hosts with the updated configuration.


## Delete capability hosts

Warning

Deleting a capability host will affect all agents that depend on it. Make sure you understand the impact before proceeding. For instance, if you delete the project and account capability host, agents in your project will no longer have access to the files, thread, and vector stores it previously did.

### Delete an account-level capability host

```
DELETE https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/capabilityHosts/{name}?api-version=2025-06-01
```


### Delete a project-level capability host

```
DELETE https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{accountName}/projects/{projectName}/capabilityHosts/{name}?api-version=2025-06-01
```


## Troubleshooting

If you're experiencing issues when creating capability hosts, this section provides solutions to the most common problems and errors.

### HTTP 409 Conflict errors

#### Problem: Multiple capability hosts per scope

**Symptoms:** You receive a 409 Conflict error when trying to create a capability host, even though you believe the scope is empty.

**Error message:**

```
{
"error": {
"code": "Conflict",
"message": "There is an existing Capability Host with name: existing-host, provisioning state: Succeeded for workspace: /subscriptions/.../workspaces/my-workspace, cannot create a new Capability Host with name: new-host for the same ClientId."
}
}
```


**Root cause:** Each account and each project can only have one active capability host. You're trying to create a capability host with a different name when one already exists at the same scope.

**Solution:**

**Check existing capability hosts**- Query the scope to see what already exists**Use consistent naming**- Ensure you're using the same name across all requests for the same scope**Review your requirements**- Determine if the existing capability host meets your needs

**Validation steps:**
Use the GET requests in [Verify your configuration](#verify-your-configuration) to confirm whether a capability host already exists at the target scope.

#### Problem: Concurrent operations in progress

**Symptoms:** You receive a 409 Conflict error indicating that another operation is currently running.

**Error message:**

```
{
"error": {
"code": "Conflict",
"message": "Create: Capability Host my-host is currently in non creating, retry after its complete: /subscriptions/.../workspaces/my-workspace"
}
}
```


**Root cause:** You're trying to create a capability host while another operation (update, delete, modify) is in progress at the same scope.

**Solution:**

**Wait for current operation to complete**- Check the status of ongoing operations**Monitor operation progress**- Use the operations API to track completion**Implement retry logic**- Use exponential backoff for temporary conflicts

**Operation monitoring:**

```
GET https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/locations/{location}/operationResults/{operationId}?api-version=2025-06-01
```


### Best practices for conflict prevention

#### 1. Pre-request validation

Always verify the current state before making changes:

- Query existing capability hosts in the target scope
- Check for any ongoing operations
- Understand the current configuration

#### 2. Implement retry logic with exponential backoff

```
try
{
var response = await CreateCapabilityHostAsync(request);
return response;
}
catch (HttpRequestException ex) when (ex.Message.Contains("409"))
{
if (ex.Message.Contains("existing Capability Host with name"))
{
// Handle name conflict - check if existing resource is acceptable
var existing = await GetExistingCapabilityHostAsync();
if (IsAcceptable(existing))
{
return existing; // Use existing resource
}
else
{
throw new InvalidOperationException("Scope already has a capability host with different name");
}
}
else if (ex.Message.Contains("currently in non creating"))
{
// Handle concurrent operation - implement retry with backoff
await Task.Delay(TimeSpan.FromSeconds(30));
return await CreateCapabilityHostAsync(request); // Retry once
}
}
```


#### 3. Understand idempotent behavior

The system supports idempotent create requests:

**Same name + same configuration**→ Returns existing resource (200 OK)**Same name + different configuration**→ Returns 400 Bad Request**Different name**→ Returns 409 Conflict

#### 4. Configuration change workflow

Since updates aren't supported, follow this sequence for configuration changes:

- Delete the existing capability host
- Wait for deletion to complete
- Create a new capability host with the desired configuration

## Next steps

- Learn about
[standard agent setup](standard-agent-setup?view=foundry-classic). - Set up your account and project:
[Set up your environment](../environment-setup?view=foundry-classic). - Add and manage connections:
[Add a new connection to your project](../../how-to/connections-add?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/agent-identity -->

# Agent identity concepts in Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An *agent identity* is a specialized identity type in [Microsoft Entra ID](/en-us/entra/fundamentals/what-is-entra) that's designed specifically for AI agents. It provides a standardized framework for governing, authenticating, and authorizing AI agents across Microsoft services. This framework enables agents to securely access resources, interact with users, and communicate with other systems.

Microsoft Foundry automatically provisions and manages agent identities throughout the agent lifecycle. This integration simplifies permission management while maintaining security and auditability as agents move from development to production.

This article explains how agent identities relate to Microsoft Entra ID objects, how Foundry uses them when an agent calls tools, and how to apply least-privilege access with Azure role-based access control (RBAC).

## Prerequisites

- Understanding of
[Microsoft Entra ID and OAuth](/en-us/entra/architecture/auth-sync-overview)authentication - Familiarity with
[Azure role-based access control (RBAC)](/en-us/azure/role-based-access-control/overview) - Basic knowledge of AI agents and their runtime requirements

For Foundry-specific RBAC roles and scopes, see [Azure role-based access control in Foundry](../../concepts/rbac-foundry?view=foundry).

## How agent identities work in Foundry

Foundry uses Microsoft Entra ID agent identities to support two related needs:

**Management and governance**: Give administrators a consistent way to inventory agents, apply policies, and audit activity.**Tool authentication**: Let an agent authenticate to downstream systems (for example, Azure Storage) without embedding secrets in prompts, code, or connection strings.

At a high level, Foundry does the following:

- Provisions an
**agent identity blueprint**and one or more**agent identities**in Microsoft Entra ID. - Assigns RBAC roles (or other permission models, depending on the target system) to the agent identity.
- When the agent invokes a tool, Foundry requests an access token for the downstream service and uses that token to authenticate the tool call.

### Terms used in this article

| Term | What it means in Foundry |
|---|---|
| Agent identity | A Microsoft Entra ID service principal that represents the agent at runtime. |
| Agent identity blueprint | A Microsoft Entra ID object that governs a class of agent identities and is used for lifecycle operations. |
`agentIdentityId` |
The identifier you use when assigning permissions to the agent identity. |
| Audience | The resource identifier for the downstream service the token is meant for (for example, `https://storage.azure.com` ). |

## Key concepts

The Agent ID platform framework introduces formal *agent identities* and *agent identity blueprints* in Microsoft Entra ID to represent AI agents. You can use this framework to securely communicate with AI agents. This framework also enables those AI agents to securely communicate with web services, other AI agents, and various systems.

### Agent identity

An agent identity is a special service principal in Microsoft Entra ID. It represents an identity that the agent identity blueprint created and is authorized to impersonate.

#### Security benefits

Agent identities help address specific security challenges that AI agents pose:

- Distinguish operations that AI agents perform from operations that workforce, customer, or workload identities perform.
- Enable AI agents to gain right-sized access across systems.
- Prevent AI agents from gaining access to critical security roles and systems.
- Scale identity management to large numbers of AI agents that can be quickly created and destroyed.

#### Authentication capabilities

Agent identities support two key authentication scenarios:

**Attended (delegated access or on-behalf-of flow)**: The agent operates on behalf of a human user. It uses delegated permissions that the user grants. The agent can then act under the user's authority to access resources or APIs as that user.**Unattended**: The agent acts under its own authority. It acts as a service or an application identity by using its app-assigned roles, RBAC, or Microsoft Graph permissions. Or it acts as an autonomous identity with user-like claims that allow the agent to authenticate and operate independently.

### Agent identity blueprint

An agent identity blueprint serves as the reusable, governing template from which all associated agent identities are created. It corresponds to a *kind*, *type*, or *class* of agents. It acts as the management object for all agent identity instances of that class.

#### Blueprint capabilities

Agent identity blueprints serve three essential purposes:

**Type classification**: The blueprint establishes the category of agent, such as "Contoso Sales Agent." This classification enables administrators to:

- Apply Conditional Access policies to all agents of that type.
- Disable or revoke permissions for all agents of that kind.
- Audit and govern agents at scale through consistent, blueprint-based controls.

**Identity creation authority**: Services that create agent identities use the blueprint to authenticate. Blueprints have OAuth credentials that services use to request tokens from Microsoft Entra ID for creating, updating, or deleting agent identities. These credentials include client secrets, certificates, or federated credentials like managed identities.

**Runtime authentication platform**: The hosting service uses the blueprint during runtime authentication. The service requests an access token by using the blueprint's OAuth credentials. It then presents that token to Microsoft Entra ID to obtain a token for one of its agent identities.

#### Blueprint metadata

For example, an organization might use an AI agent called the "Contoso Sales Agent." The blueprint defines information such as:

- The name of the agent type: "Contoso Sales Agent."
- The publisher or organization responsible for the blueprint: "Contoso."
- The roles that the agent might perform: "sales manager" or "sales rep."
- Microsoft Graph permissions or delegated scopes: "read the signed-in user's calendar."

## Foundry integration

Foundry automatically integrates with Microsoft Entra Agent ID by creating and managing identities throughout the agent development lifecycle. When you create your first agent in a Foundry project, the system provisions a default agent identity blueprint and a default agent identity for your project.

### Shared project identity

All unpublished or in-development agents within the same project share a common identity. This design simplifies permission management because unpublished agents typically require the same access patterns and permission configurations. The shared identity approach provides these benefits:

**Simplified administration**: Administrators can centrally manage permissions for all in-development agents within a project.**Reduced identity sprawl**: Using a single identity per project prevents unnecessary identity creation during early experimentation.**Developer autonomy**: After the shared identity is configured, developers can independently build and test agents without repeatedly configuring new permissions.

To find your shared agent identity blueprint and agent identity, go to your Foundry project in the [Azure portal](https://portal.azure.com). On the **Overview** pane, select **JSON View**. Choose the latest API version to view and copy the identities.

### Distinct agent identity

When an agent's permissions, auditability, or lifecycle requirements diverge from the project defaults, you should upgrade to a distinct identity. Publishing an agent automatically creates a dedicated agent identity blueprint and agent identity. Both are bound to the agent application resource. This distinct identity represents the agent's system authority for accessing its own resources.

Common scenarios that require distinct identities include:

- Agents ready for integration testing.
- Agents prepared for production consumption.
- Agents that require unique permission sets.
- Agents that need independent audit trails.

To find the distinct agent identity blueprint and agent identity, go to your agent application resource in the Azure portal. On the **Overview** pane, select **JSON View**. Choose the latest API version to view and copy the identities.

## Tool authentication

Agents access remote resources and tools by using agent identities for authentication. The authentication mechanism differs based on the agent's publication status:

**Unpublished agents**: Authenticate by using the shared project's agent identity.**Published agents**: Authenticate by using the unique agent identity that's associated with the agent application.

When you [publish an agent](../how-to/publish-agent?view=foundry), you must reassign RBAC permissions to the new agent identity for any resources that the agent needs to access. This reassignment ensures that the published agent maintains appropriate access while operating under its distinct identity.

### Supported tools

Currently, the tools that support authentication with an agent identity are:

**Model Context Protocol (MCP)**: Use your agent's identity to authenticate with MCP servers that support agent identity authentication. For details, see[Model Context Protocol (preview)](../how-to/tools/model-context-protocol?view=foundry)and[MCP server authentication](../how-to/mcp-authentication?view=foundry).**Agent-to-Agent (A2A)**: Enable secure communication between agents by using agent identities. For details, see[Agent-to-Agent tool (preview)](../how-to/tools/agent-to-agent?view=foundry)and[Agent2Agent (A2A) authentication](agent-to-agent-authentication?view=foundry).

Other tools and integrations might use different authentication methods (for example, key-based authentication or OAuth identity passthrough). Use the tool documentation to confirm supported authentication.

### Configure MCP tool authentication

To configure an MCP tool to authenticate by using an agent identity:

Ensure that you have an MCP server that you want to configure as a tool for your agent.

Get the ID for the agent identity. In the Azure portal, go to your Foundry project. On the

**Overview**pane, select**JSON View**and choose the latest API version. Copy the`agentIdentityId`

value.Create a connection to your remote MCP server that uses

`AgenticIdentityToken`

as the authentication type. The**Audience**box specifies which service or API the token is intended to access. For example:- For an MCP server that lists blobs in your storage account, set the audience as
`https://storage.azure.com`

. - For an Azure Logic Apps MCP server, set the audience as
`https://logic.azure.com`

.

You can create the connection by using either the REST API or the Foundry portal:

To get an access token, run the commands

`az login`

and then`az account get-access-token`

.`PUT https://management.azure.com/subscriptions/{{subscription_id}}/resourceGroups/{{resource_group}}/providers/Microsoft.CognitiveServices/accounts/{{account_name}}/projects/{{project_name}}/connections/{{mcp_connection_name}}?api-version={{api_version}} Authorization: Bearer {{token}} Content-Type: application/json { "tags": null, "location": null, "name": "{YOUR_CONNECTION_NAME}", "type": "CognitiveServices/accounts/projects/connections", "properties": { "authType": "AgenticIdentityToken", "group": "ServicesAndApps", "category": "RemoteTool", "expiryTime": null, "target": "{YOUR_MCP_REMOTE_URL}", "isSharedToAll": true, "sharedUserList": [], "audience": "{YOUR_AUDIENCE}", "Credentials": {}, "metadata": { "ApiType": "Azure" } } }`

- For an MCP server that lists blobs in your storage account, set the audience as
Assign to the agent identity the required permissions for its actions by using the

`agentIdentityId`

value that you copied. For example:- For an MCP server that lists blob containers, assign the
**Storage Blob Data Contributor**role at the**Azure Storage Account**scope. - For an Azure Logic Apps MCP server, assign the
**Logic Apps Standard Reader**role on the**Logic App**resource.

- For an MCP server that lists blob containers, assign the
Connect the tool. If you're using code, create an agent with the MCP tool. (For details, see the MCP documentation.) If you're using the Foundry portal, the MCP tool is automatically added to the agent.


When the agent invokes the MCP server, it uses the available agent identity to obtain an authorization token for the **audience** value. It then passes the token to the MCP server for authentication.

## Security considerations

Agent identities help you reduce risk by removing the need to embed long-lived credentials in agent configurations. Use these practices to keep access least-privilege and auditable:

- Assign only the permissions the agent needs for its tool actions. Prefer narrow scopes (resource or resource group) over subscription-wide access.
- Treat the shared project identity as a broader blast radius. If an agent needs tighter controls or separate auditing, publish it so it gets a distinct identity, and assign roles to that new identity.
- Review and log access to non-Microsoft tools and servers. If a tool call leaves Microsoft services, your data handling and retention depend on the external provider.

## Limitations

- Only some tools currently support agent identity authentication. Check the tool documentation for supported authentication.
- Publishing an agent changes which identity is used for tool calls (shared project identity versus distinct agent identity). Plan for role reassignment when you publish.

## Common issues

These issues commonly cause tool authentication failures when using agent identities:

**Roles assigned to the wrong identity**: Confirm you granted permissions to the current identity used by the agent (shared project identity for unpublished agents, distinct identity for published agents).**Missing role assignments**: Ensure the agent identity has the required RBAC role on the target resource. For Foundry roles and scopes, see[Azure role-based access control in Foundry](../../concepts/rbac-foundry?view=foundry).**Incorrect audience**: Ensure the audience matches the downstream service you’re calling (for example,`https://storage.azure.com`

for Azure Storage).

For tool-specific troubleshooting, see the tool documentation:

## Manage agent identities

You can view and manage all agent identities in your tenant through the Microsoft Entra admin center. Go to the [tab for agent identities](https://entra.microsoft.com/?Microsoft_AAD_RegisteredApps=stage1&exp.EnableAgentIDUX=true#view/Microsoft_AAD_RegisteredApps/AllAgents.MenuView/%7E/allAgentIds) to see an inventory of all agents in your tenant, including Foundry agents, Microsoft Copilot Studio agents, and others.

In this experience, you can enable built-in security controls, including:

**Conditional Access**: Apply access policies to agent identities.**Identity protection**: Monitor and protect agent identities from threats.**Network access**: Control network-based access for agents.**Governance**: Manage expiration, owners, and sponsors for agent identities.

For more information about Microsoft Entra Agent ID features, see [Microsoft Entra documentation](/en-us/entra/fundamentals/what-is-entra).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/hosted-agents -->

# What are hosted agents?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you build agentic applications by using open-source frameworks, you typically manage containerization, web server setup, security integration, memory persistence, infrastructure scaling, data transmission, instrumentation, and version rollbacks. These tasks become even more challenging in heterogeneous cloud environments.

Hosted agents in Foundry Agent Service solve these challenges for Microsoft Foundry users. By using this managed platform, you can deploy and operate AI agents securely and at scale. You can use your custom agent code or a preferred agent framework with streamlined deployment and management.

## Prerequisites

- A
[Microsoft Foundry project](../../how-to/create-projects?view=foundry) - Basic understanding of
[containerization and Docker](/en-us/azure/container-instances/container-instances-overview) - Familiarity with
[Azure Container Registry](/en-us/azure/container-registry/container-registry-intro) - Knowledge of your preferred agent framework (LangGraph, Microsoft Agent Framework, or custom code)

## At a glance

Hosted agents let you bring your own agent code and run it as a managed containerized service.

Use this article to:

- Understand what hosted agents are and when to use them.
- Package and test your agent locally before deployment.
- Create, manage, publish, and monitor hosted agents.

If you want to jump to a task, see:

[Package code and test locally](#package-code-and-test-locally)[Create a hosted agent](#create-a-hosted-agent)[Manage hosted agents](#manage-hosted-agents)[Publish hosted agents to channels](#publish-hosted-agents-to-channels)[Troubleshoot hosted agent endpoints](#troubleshoot-hosted-agent-endpoints)

## Limits, pricing, and availability (preview)

Hosted agents are currently in preview.

**Region availability**: North Central US only.**Private networking support**: You can't create hosted agents by using the standard setup for network isolation within network-isolated Foundry resources. For details, see[Configure virtual networks](../how-to/virtual-networks?view=foundry).**Preview limits**: For the full list of preview limits, see[Limitations during preview](#limitations-during-preview).**Pricing**: For updates on pricing, see the Foundry[pricing page](https://azure.microsoft.com/pricing/details/ai-foundry/).

## Security and data handling

Treat a hosted agent like production application code.

**Don't put secrets in container images or environment variables**. Use managed identities and connections, and store secrets in a managed secret store. For guidance, see[Set up a Key Vault connection](../../how-to/set-up-key-vault-connection?view=foundry).**Use least privilege**. Grant only the permissions your agent needs. For identity concepts, see[Agent identity concepts in Microsoft Foundry](agent-identity?view=foundry).**Be careful with non-Microsoft tools and servers**. If your agent calls tools backed by non-Microsoft services, some data might flow to those services. Review data sharing, retention, and location policies for any non-Microsoft service you connect.

## Understand key concepts

### Hosted agents

Hosted agents are containerized agentic AI applications that run on Agent Service. Unlike prompt-based agents, developers build hosted agents through code and deploy them as container images on Microsoft-managed pay-as-you-go infrastructure.

Hosted agents follow a standard lifecycle: create, start, update, stop, and delete. Each phase provides specific capabilities and status transitions to help you manage your agent deployments effectively.

Note

Hosted agents are currently in preview. For current constraints and availability, see [Limits, pricing, and availability (preview)](#limits-pricing-and-availability-preview).

### Hosting adapter

The hosting adapter is a framework abstraction layer that helps expose supported agent frameworks (or your custom code) as an HTTP service for local testing and hosted deployments.

The hosting adapter provides several key benefits for developers:

**Simplified local testing**: Run your agent locally and validate the HTTP surface area before you containerize and deploy.

**Automatic protocol translation**: The adapter handles all complex conversions between the Foundry request and response formats and your agent framework's native data structures. These activities include:

- Conversation management
- Message serialization
- Streaming event generation

**Observability integration**: Export traces, metrics, and logs by using OpenTelemetry.

**Seamless Foundry integration**: Your locally developed agents work with the Foundry Responses API, conversation management, and authentication flows.

### Managed service capabilities

Agent Service handles:

- Provisioning and autoscaling of agents
- Conversation orchestration and state management
- Identity management
- Integration with Foundry tools and models
- Built-in observability and evaluation capabilities
- Enterprise-grade security, compliance, and governance

Important

If you use Agent Service to host agents that interact with non-Microsoft servers or agents, you take on the risk. Review all data that you share with non-Microsoft servers or agents. Be aware of non-Microsoft practices for retention and location of data. You're responsible for managing whether your data flows outside your organization's Azure compliance and geographic boundaries, along with any related implications.

### Framework and language support

| Framework | Python | C# |
|---|---|---|
| Microsoft Agent Framework | ✅ | ✅ |
| LangGraph | ✅ | ❌ |
| Custom code | ✅ | ✅ |

### Public adapter packages

- Python:
`azure-ai-agentserver-core`

,`azure-ai-agentserver-agentframework`

,`azure-ai-agentserver-langgraph`

- .NET:
`Azure.AI.AgentServer.Core`

,`Azure.AI.AgentServer.AgentFramework`


## Package code and test locally

Before you deploy to Microsoft Foundry, build and test your agent locally:

**Run your agent locally**: Use the hosting adapter to start a local web server that automatically exposes your agent as a REST API.**Test by using REST calls**: The local server runs on`localhost:8088`

and accepts standard HTTP requests.**Build the container image**: Create a container image from your source files by using an`azure-ai-agentserver-*`

package to wrap your agent code.**Use the Azure Developer CLI**: Use`azd`

to streamline the packaging and deployment process.

### Local testing by using the REST API

When you run your agent locally by using the hosting adapter, it automatically starts a web server on `localhost:8088`

. You can test your agent by using any REST client.

```
@baseUrl = http://localhost:8088
POST {{baseUrl}}/responses
Content-Type: application/json
{
"input": {
"messages": [
{
"role": "user",
"content": "Where is Seattle?"
}
]
}
}
```


This local testing approach lets you:

- Validate agent behavior before containerization.
- Debug issues in your development environment.
- Test different input scenarios quickly.
- Verify API compatibility with the Foundry Responses API.

## Create a hosted agent

### Create a hosted agent by using the Azure Developer CLI

Developers can use the Azure Developer CLI `ai agent`

extension for seamless and rapid provisioning and deployment of their agentic applications on Microsoft Foundry.

This extension simplifies the setup of Foundry resources, models, tools, and knowledge resources. For example, it simplifies the setup of Azure Container Registry for bringing your own container, Application Insights for logging and monitoring, a managed identity, and role-based access control (RBAC). In other words, it provides everything you need to get started with hosted agents in Foundry Agent Service.

This extension is currently in preview. Don't use it for production.

To get started:

Install the Azure Developer CLI on your device.

If you already have the Azure Developer CLI installed, check if you have the latest version of

`azd`

installed:`azd version`

To upgrade to the latest version, see

[Install or update the Azure Developer CLI](/en-us/azure/developer/azure-developer-cli/install-azd).If you're starting with no existing Foundry resources and you want to simplify all the required infrastructure provisioning and RBAC, download the Foundry starter template. The template automatically installs the

`ai agent`

extension. When prompted, you can provide an environment name which creates a resource group named`rg-<name-you-provide>`

.`azd init -t https://github.com/Azure-Samples/azd-ai-starter-basic`

To check all installed extensions:

`azd ext list`

Make sure you have the latest version of the Foundry

`azd`

agent extension installed.If you have an existing Foundry project where you want to deploy your agent, and you want to provision only the additional resources that you might need for deploying your agent, run this command afterward:

`azd ai agent init --project-id /subscriptions/[SUBSCRIPTIONID]/resourceGroups/[RESOURCEGROUPNAME]/providers/Microsoft.CognitiveServices/accounts/[ACCOUNTNAME]/projects/[PROJECTNAME]`

Initialize the template by configuring the parameters in the agent definition:

`azd ai agent init -m <repo-path-to-agent.yaml>`

The GitHub repo for an agent that you want to host on Foundry contains the application code, referenced dependencies, Dockerfile for containerization, and the

`agent.yaml`

file that contains your agent's definition. To configure your agent, set values for the parameters that you're prompted for. This action registers your agent under`Services`

in`azure.yaml`

for the downloaded template. You can get started with samples on[GitHub](https://github.com/azure-ai-foundry/foundry-samples).To open and view all Bicep and configuration files associated with your

`azd`

-based deployments, use this command:`code .`

Package, provision, and deploy your agent code as a managed application on Foundry:

`azd up`

This command abstracts the underlying execution of the commands

`azd infra generate`

,`azd provision`

, and`azd deploy`

. It also creates a hosted agent version and deployment on Foundry Agent Service. If you already have a version of a hosted agent,`azd`

creates a new version of the same agent. To learn more about how you can do non-versioned updates, along with starting, stopping, and deleting your hosted agent deployments and versions, see the[management section](#manage-hosted-agents)of this article.

Make sure you have RBAC enabled so that `azd`

can provision the services and models for you. For Foundry role guidance, see [Role-based access control in Foundry portal](../../concepts/rbac-foundry?view=foundry). For Azure built-in roles, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

### Roles and permissions

If you have an existing Foundry resource and need to create a new Foundry project to deploy a hosted agent, you need

**Azure AI Owner**roles.If you have an existing project and want to create the model deployment and container registry in the project, you need

**Azure AI Owner**role on Foundry in addition to the**Contributor**role on the Azure subscription.If you have everything configured in the project to deploy a hosted agent, you need

**Reader**on the Foundry account and**Azure AI User**on the project.

Refer to [this article](../../concepts/authentication-authorization-foundry?view=foundry#built-in-roles-overview) to learn more about built-in roles in Foundry.

### Resource cleanup

To prevent unnecessary charges, clean up your Azure resources after you complete your work with the application.

When to clean up:

- After you finish testing or demonstrating the application.
- When the application is no longer needed or you transition to a different project or environment.
- When you complete development and are ready to decommission the application.

To delete all associated resources and shut down the application, run the following command:

```
azd down
```


This process might take up to 20 minutes to complete.

## Create a hosted agent by using the Foundry SDK

When you create a hosted agent, the system registers the agent definition in Microsoft Foundry and tries to create a deployment for that agent version.

### Prerequisites for deployment

Before you deploy a hosted agent, make sure that you have:

A container image hosted in

[Azure Container Registry](https://azure.microsoft.com/services/container-registry/).For more information, see

[Create a private container registry](/en-us/azure/container-registry/container-registry-get-started-portal).Access to assign roles in Azure Container Registry. You need at least User Access Administrator or Owner permissions on the container registry.

The Azure AI Projects SDK installed.

`pip install azure-ai-projects`


### Build and push your Docker image to Azure Container Registry

To build your agent as a Docker container and upload it to Azure Container Registry:

Build your Docker image locally:

`docker build -t myagent:v1 .`

Sign in to Azure Container Registry:

`az acr login --name myregistry`

Tag your image for the registry:

`docker tag myagent:v1 myregistry.azurecr.io/myagent:v1`

Push the image to Azure Container Registry:

`docker push myregistry.azurecr.io/myagent:v1`


For detailed guidance on working with Docker images in Azure Container Registry, see [Push and pull Docker images](/en-us/azure/container-registry/container-registry-get-started-docker-cli).

### Configure Azure Container Registry permissions

Before you create the agent, give your project's managed identity access to pull from the container registry that houses your image. This step ensures that all dependencies are available within the container.

In the

[Azure portal](https://portal.azure.com), go to your Foundry project resource.On the left pane, select

**Identity**.Under

**System assigned**, copy the**Object (principal) ID**value. This value is the managed identity that you'll assign the Azure Container Instances role to.Grant pull permissions by assigning the Container Registry Repository Reader role to your project's managed identity on the container registry. For detailed steps, see

[Azure Container Registry roles and permissions](/en-us/azure/container-registry/container-registry-roles).

### Create an account-level capability host

Hosted agents require an account-level capability host with public hosting enabled.

Updating capability hosts isn't supported. If you already have a capability host for your Microsoft Foundry account, delete it and recreate it with `enablePublicHostingEnvironment`

set to `true`

.

Use `az rest`

so you don't have to manage tokens manually.

#### Azure CLI (bash)

```
az rest --method put \
--url "https://management.azure.com/subscriptions/[SUBSCRIPTIONID]/resourceGroups/[RESOURCEGROUPNAME]/providers/Microsoft.CognitiveServices/accounts/[ACCOUNTNAME]/capabilityHosts/accountcaphost?api-version=2025-10-01-preview" \
--headers "content-type=application/json" \
--body '{
"properties": {
"capabilityHostKind": "Agents",
"enablePublicHostingEnvironment": true
}
}'
```


#### Azure CLI (PowerShell)

```
az rest --method put `
--url "https://management.azure.com/subscriptions/[SUBSCRIPTIONID]/resourceGroups/[RESOURCEGROUPNAME]/providers/Microsoft.CognitiveServices/accounts/[ACCOUNTNAME]/capabilityHosts/accountcaphost?api-version=2025-10-01-preview" `
--headers "content-type=application/json" `
--body '{
"properties": {
"capabilityHostKind": "Agents",
"enablePublicHostingEnvironment": true
}
}'
```


### Create the hosted agent version

Install version>=2.0.0b2 of the Azure AI Projects SDK.

```
pip install --pre azure-ai-projects==2.0.0b2
```


Use the Azure AI Projects SDK to create and register your agent:

```
from azure.ai.projects import AIProjectClient
from azure.ai.projects.models import ImageBasedHostedAgentDefinition, ProtocolVersionRecord, AgentProtocol
from azure.identity import DefaultAzureCredential
# Initialize the client
client = AIProjectClient(
endpoint="https://your-project.services.ai.azure.com/api/projects/project-name",
credential=DefaultAzureCredential()
)
# Create the agent from a container image
agent = client.agents.create_version(
agent_name="my-agent",
definition=ImageBasedHostedAgentDefinition(
container_protocol_versions=[ProtocolVersionRecord(protocol=AgentProtocol.RESPONSES, version="v1")],
cpu="1",
memory="2Gi",
image="your-registry.azurecr.io/your-image:tag",
environment_variables={
"AZURE_AI_PROJECT_ENDPOINT": "https://your-project.services.ai.azure.com/api/projects/project-name",
"MODEL_NAME": "gpt-4",
"CUSTOM_SETTING": "value"
}
)
)
```


Here are the key parameters:

`PROJECT_ENDPOINT`

: Endpoint URL for your Foundry project.`AGENT_NAME`

: Unique name for your agent.`CONTAINER_IMAGE`

: Full Azure Container Registry image URL with tag.`CPU/Memory`

: Resource allocation (for example,`1`

for CPU,`2Gi`

for memory).

Note

- Ensure that your container image is accessible from the Foundry project.
`DefaultAzureCredential`

handles authentication automatically.

The agent appears in the Foundry portal after you create it.

## Manage hosted agents

### Update an agent

You can update an agent in two ways: versioned updates and non-versioned updates.

#### Versioned update

Use a versioned update to modify the runtime configuration for your agent. This process creates a new version of the agent.

Changes that trigger a new version include:

**Container image**: Updating to a new image or tag.**Resource allocation**: Changing CPU or memory settings.**Environment variables**: Adding, removing, or modifying environment variables.**Protocol versions**: Updating supported protocol versions.

To create a new version, use the same `client.agents.create_version()`

method shown in the creation example with your updated configuration.

#### Non-versioned update

Use a non-versioned update to modify horizontal scale configuration (minimum and maximum replicas) or agent metadata such as description and tags. This process doesn't create a new version.

```
az cognitiveservices agent update
```


The arguments for this command include:

| Argument | Required | Description |
|---|---|---|
`--account-name -a` |
✅ | Foundry Tools account name. |
`--agent-version` |
✅ | Foundry Tools hosted agent version. |
`--name -n` |
✅ | Foundry Tools hosted agent name. |
`--project-name` |
✅ | AI project name. |
`--description` |
❌ | Description of the agent. |
`--max-replicas` |
❌ | Maximum number of replicas for horizontal scaling. |
`--min-replicas` |
❌ | Minimum number of replicas for horizontal scaling. |
`--tags` |
❌ | Space-separated tags: `key[=value] [key[=value] ...]` . Use two single quotation marks (`''` ) to clear existing tags. |

Here's an example:

```
az cognitiveservices agent update --account-name myAccount --project-name myProject --name myAgent --agent-version 1 --min-replicas 1 --max-replicas 2
```


### Start an agent deployment

After you create your hosted agent version, start the deployment by using the `az`

CLI extension to make it available for requests. You can also start a hosted agent that you previously stopped.

```
az cognitiveservices agent start
```


The arguments for this command include:

| Argument | Required | Description |
|---|---|---|
`--account-name -a` |
✅ | Foundry Tools account name |
`--agent-version` |
✅ | Foundry Tools hosted agent version |
`--name -n` |
✅ | Foundry Tools hosted agent name |
`--project-name` |
✅ | AI project name |
`--min-replicas` |
❌ | Minimum number of replicas for horizontal scaling |
`--max-replicas` |
❌ | Maximum number of replicas for horizontal scaling |

If you don't specify max and min replicas during agent start operation, the default value is 1 for both the arguments.

Here's an example:

```
az cognitiveservices agent start --account-name myAccount --project-name myProject --name myAgent --agent-version 1
```


When you start an agent:

- Current status:
**Stopped** - Allowed operation:
**Start** - Transitory status:
**Starting** - Final status:
**Started**(if successful) or**Failed**(if unsuccessful)

### View container Log Stream

The container Logstream API for hosted agents gives you access to the system and console logs of the azure container app deployed on your behalf in Microsoft's Azure environment to enable self-serve debuggability for agent startup and runtime errors during deployment.

#### REST API Details

| Item | Value |
|---|---|
Method |
`GET` |
Route |
`/agents/v2.0/subscriptions/{subscription}/resourceGroups/{resourceGroup}/providers/Microsoft.MachineLearningServices/workspaces/{workspace}/agents/{agentName}/versions/{agentVersion}/containers/default:logstream` |
Description |
Streams console or system logs for a specific hosted agent replica. |
Content-Type |
`text/plain` (chunked streaming) |

#### Path parameters

`subscription`

,`resourceGroup`

,`workspace`

: identify the AML workspace hosting the agent.`agentName`

,`agentVersion`

: specify the agent deployment/version whose container logs are requested.

#### Query parameters

| Name | Default | Notes |
|---|---|---|
`kind` |
`console` |
`console` returns container stdout/stderr, `system` returns container app event stream. |
`replica_name` |
empty | When omitted, the server chooses the first replica for console logs. Required to target a specific replica. |
`tail` |
`20` |
Number of trailing lines returned. Enforced to `1-300` . |

#### Timeout Settings

- Max Connection Duration: The maximum duration for a log stream connection is
`10 minutes`

. After this period, the server will automatically close the client connection. - Idle Timeout: This timeout is set to
`1 minute`

. It applies when there is no response from the client, or if there is no activity after the previous response during the log stream. If the connection remains idle for 1 minute, it will be closed by the server.

#### Response status codes

`200 OK`

: Plain-text stream of log lines, one per line.`404 Not Found`

: Agent version, replica, or container log endpoint was not found.`401/403`

: Caller lacks authorization.`5xx`

: Propagated from downstream Container Apps calls when details or tokens cannot be fetched.

#### Response samples

#### 200 OK (console logs)

```
HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Transfer-Encoding: chunked
2025-12-15T08:43:48.72656 Connecting to the container 'agent-container'...
2025-12-15T08:43:48.75451 Successfully Connected to container: 'agent-container' [Revision: 'je90fe655aa742ef9a188b9fd14d6764--7tca06b', Replica: 'je90fe655aa742ef9a188b9fd14d6764--7tca06b-6898b9c89f-mpkjc']
2025-12-15T08:33:59.0671054Z stdout F INFO: 127.0.0.1:42588 - "GET /readiness HTTP/1.1" 200 OK
2025-12-15T08:34:29.0649033Z stdout F INFO: 127.0.0.1:60246 - "GET /readiness HTTP/1.1" 200 OK
2025-12-15T08:34:59.0644467Z stdout F INFO: 127.0.0.1:43994 - "GET /readiness HTTP/1.1" 200 OK
2025-12-15T08:35:29.0651892Z stdout F INFO: 127.0.0.1:59368 - "GET /readiness HTTP/1.1" 200 OK
2025-12-15T08:35:59.0644637Z stdout F INFO: 127.0.0.1:57488 - "GET /readiness HTTP/1.1" 200 OK
```


#### 200 OK (system logs)

```
HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Transfer-Encoding: chunked
{"TimeStamp":"2025-12-15T16:51:33Z","Type":"Normal","ContainerAppName":null,"RevisionName":null,"ReplicaName":null,"Msg":"Connecting to the events collector...","Reason":"StartingGettingEvents","EventSource":"ContainerAppController","Count":1}
{"TimeStamp":"2025-12-15T16:51:34Z","Type":"Normal","ContainerAppName":null,"RevisionName":null,"ReplicaName":null,"Msg":"Successfully connected to events server","Reason":"ConnectedToEventsServer","EventSource":"ContainerAppController","Count":1}
### Stop an agent deployment
To stop the hosted agent, set the maximum replica for your agent deployment to zero and use the following command:
```bash
az cognitiveservices agent stop
```


The arguments for this command include:

| Argument | Required | Description |
|---|---|---|
`--account-name -a` |
✅ | Foundry Tools account name |
`--agent-version` |
✅ | Foundry Tools hosted agent version |
`--name -n` |
✅ | Foundry Tools hosted agent name |
`--project-name` |
✅ | AI project name |

Here's an example:

```
az cognitiveservices agent stop --account-name myAccount --project-name myProject --name myAgent --agent-version 1
```


When you stop an agent:

- Current status:
**Running** - Allowed operation:
**Stop** - Transitory status:
**Stopping** - Final status:
**Stopped**(if successful) or**Running**(if unsuccessful)

### Delete an agent

You can delete agents at various levels, depending on what you want to remove.

#### Delete a deployment only

The following command stops the running agent but keeps the agent version for future use. Use it when you want to stop the agent temporarily or switch to a different version.

```
az cognitiveservices agent delete-deployment
```


The arguments for this command include:

| Argument | Required | Description |
|---|---|---|
`--account-name -a` |
✅ | Foundry Tools account name |
`--agent-version` |
✅ | Foundry Tools hosted agent version |
`--name -n` |
✅ | Foundry Tools hosted agent name |
`--project-name` |
✅ | AI project name |

#### Delete the agent

The following command removes all versions and deployments for the agent. Use it when you no longer need the agent and want to clean up all associated resources.

If you provide `agent_version`

and you delete the agent deployment, the operation deletes the agent definition associated with that version. If the agent deployment is running, the operation doesn't succeed.

If you don't provide `agent_version`

, the operation deletes all agent versions associated with the agent name.

```
az cognitiveservices agent delete
```


The arguments for this command include:

| Argument | Required | Description |
|---|---|---|
`--account-name -a` |
✅ | Foundry Tools account name. |
`--name -n` |
✅ | Foundry Tools hosted agent name. |
`--project-name` |
✅ | AI project name. |
`--agent-version` |
❌ | Foundry Tools hosted agent version. If you don't provide it, the command deletes all versions. |

### List hosted agents

#### List all versions of a hosted agent

```
az cognitiveservices agent list-versions
```


The arguments for this command include:

| Argument | Required | Description |
|---|---|---|
`--account-name -a` |
✅ | Foundry Tools account name |
`--name -n` |
✅ | Foundry Tools hosted agent name |
`--project-name` |
✅ | AI project name |

#### Show details of a hosted agent

```
az cognitiveservices agent show
```


The arguments for this command include:

| Argument | Required | Description |
|---|---|---|
`--account-name -a` |
✅ | Foundry Tools account name |
`--name -n` |
✅ | Foundry Tools hosted agent name |
`--project-name` |
✅ | AI project name |

### Invoke hosted agents

You can view and test hosted agents in the agent playground UI. Hosted agents expose an API that's compatible with OpenAI responses. Use the Azure AI Projects SDK to invoke this API.

```
#!/usr/bin/env python3
"""
Call a deployed Microsoft Foundry agent
"""
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient
from azure.ai.projects.models import AgentReference
# Configuration
PROJECT_ENDPOINT = "https://your-project.services.ai.azure.com/api/projects/your-project"
AGENT_NAME = "your-agent-name"
AGENT_VERSION = "1" # Optional: specify version, or use latest
# Initialize the client and retrieve the agent
client = AIProjectClient(endpoint=PROJECT_ENDPOINT, credential=DefaultAzureCredential())
agent = client.agents.retrieve(agent_name=AGENT_NAME)
# Get the OpenAI client and send a message
openai_client = client.get_openai_client()
response = openai_client.responses.create(
input=[{"role": "user", "content": "Hello! What can you help me with?"}],
extra_body={"agent": AgentReference(name=agent.name, version=AGENT_VERSION).as_dict()}
)
print(f"Agent response: {response.output_text}")
Reference: [Azure AI Projects SDK for Python](/python/api/overview/azure/ai-projects-readme?view=azure-python-preview&preserve-view=true)
```


### Use tools with hosted agents

Before your hosted agent can run with Foundry tools, create a connection to your remote Model Context Protocol (MCP) server on Foundry.

The `RemoteMCPTool`

connection supports these authentication mechanisms:

**Stored credentials**: Use predefined credentials stored in the system.**Project managed identity**: Use the managed identity for the Foundry project.

Choose your authentication method:

**For shared identity**: Use key-based or Foundry project managed identity authentication when every user of your agent should use the same identity. Individual user identity or context doesn't persist with these methods.**For individual user context**: Use OAuth identity passthrough when every user of your agent should use their own account to authenticate with the MCP server. This approach preserves personal user context.

For more information, see [Connect to Model Context Protocol servers](../how-to/tools/model-context-protocol?view=foundry).

Reference the Foundry tool connection ID for Remote MCP servers within your agent code by using an environment variable. Wrap it by using the Hosting adapter for testing locally. Build and push your Docker image to Azure Container Registry (ACR). Configure image pull permissions on the ACR. Create a capability host by following the instructions mentioned [above](#create-a-hosted-agent) and proceed to registering your agent on Foundry.

Create a hosted agents version with tools definition by using the Foundry SDK.

```
from azure.ai.projects import AIProjectClient
from azure.ai.projects.models import ImageBasedHostedAgentDefinition, ProtocolVersionRecord, AgentProtocol
from azure.identity import DefaultAzureCredential
# Initialize the client
client = AIProjectClient(
endpoint="https://your-project.services.ai.azure.com/api/projects/project-name",
credential=DefaultAzureCredential()
)
# Create the agent from a container image
agent = client.agents.create_version(
agent_name="my-agent",
description="Coding agent expert in assisting with github issues",
definition=ImageBasedHostedAgentDefinition(
container_protocol_versions=[ProtocolVersionRecord(protocol=AgentProtocol.RESPONSES, version="v1")],
cpu="1",
memory="2Gi",
image="your-registry.azurecr.io/your-image:tag",
tools=[
{
"type": "code_interpreter"
},
{
"type": "mcp",
"project_connection_id": "github_connection_id"
}
],
environment_variables={
"AZURE_AI_PROJECT_ENDPOINT": "https://your-project.services.ai.azure.com/api/projects/project-name",
"MODEL_NAME": "gpt-4",
"CUSTOM_SETTING": "value"
}
)
)
```


Start the agent by using Azure Cognitive Services CLI or from within Agent Builder in the new Foundry UI.

Currently supported built-in Foundry tools include:

- Code Interpreter
- Image Generation
- Web Search

## Manage observability with hosted agents

Hosted agents support exposing OpenTelemetry traces, metrics, and logs from underlying frameworks to Microsoft Foundry with Application Insights or any user-specified OpenTelemetry Collector endpoint.

If you use the `azd ai agent`

CLI extension, Application Insights is automatically provisioned and connected to your Foundry project for you. Your project's managed identity is granted the Azure AI User role on the Foundry resource so that traces are exported to Application Insights.

If you use the Foundry SDK, you need to perform these steps independently. For more information, see [Enable tracing in your project](../../how-to/develop/trace-application?view=foundry#enable-tracing-in-your-project).

The hosting adapter provides:

**Complete OpenTelemetry setup**:`TracerProvider`

,`MeterProvider`

,`LoggerProvider`

.**Auto-instrumentation**: HTTP requests, database calls, AI model calls.**Azure Monitor integration**: Exporters, formatting, authentication.**Performance optimization**: Sampling, batching, resource detection.**Live metrics**: Real-time dashboard in Application Insights.

### Local tracing

Install and set up AI Toolkit for Visual Studio Code (VS Code) by following

[Trace in AI Toolkit](https://code.visualstudio.com/docs/intelligentapps/tracing).Set up and export the environment variable

`OTEL_EXPORTER_ENDPOINT`

. You can find the endpoint from AI Toolkit for VS Code after you select the**Start Collector**button.Invoke the agent and find traces in AI Toolkit.


### Tracing in the Foundry portal

You can also review traces for your hosted agent on the **Traces** tab in the playground.

### Export traces to your OpenTelemetry-compatible server

To send traces to your own OpenTelemetry collector or compatible observability platform, use the environment variable `OTEL_EXPORTER_ENDPOINT`

.

## Manage conversations by using hosted agents

Hosted agents integrate seamlessly with the conversation management system in Microsoft Foundry. This integration enables stateful, multiple-turn interactions without manual state management.

### How conversations work with hosted agents

**Conversation objects**: Foundry automatically creates durable conversation objects with unique identifiers that persist across multiple agent interactions. When a user starts a conversation with your hosted agent, the platform maintains this conversation context automatically.

**State management**: Unlike traditional APIs where you manually pass conversation history, hosted agents receive conversation context automatically. The Foundry runtime manages:

- Previous messages and responses.
- Tool calls and their outputs.
- Agent instructions and configuration.
- Conversation metadata and time stamps.

**Conversation items**: Each conversation contains structured items that the system automatically maintains:

**Messages**: User inputs and agent responses with time stamps.**Tool calls**: Function invocations with parameters and results.**Tool outputs**: Structured responses from external services.**System messages**: Internal state and context information.

### Conversation persistence and reuse

**Cross-session continuity**: Conversations persist beyond individual requests. Users can return to previous discussions with full context maintained.

**Conversation reuse**: Users can access the same conversation from multiple channels and applications. Conversations maintain consistent state and history.

**Automatic cleanup**: Foundry manages conversation lifecycle and cleanup based on your project's retention policies.

## Evaluate and test hosted agents

Microsoft Foundry provides comprehensive evaluation and testing capabilities that are designed for hosted agents. Use these capabilities to validate performance, compare versions, and help ensure quality before deployment.

### Built-in evaluation capabilities

**Agent performance evaluation**: Foundry includes built-in evaluation metrics to assess your hosted agent's effectiveness:

- Response quality and relevance
- Task completion accuracy
- Tool usage effectiveness
- Conversation coherence and context retention
- Response time and efficiency metrics

**Agent-specific evaluation**: Evaluate hosted agents by using the Azure AI Evaluation SDK with built-in evaluators that are designed for agentic workflows. The SDK provides specialized evaluators for measuring agent performance across key dimensions like intent resolution, task adherence, and tool usage accuracy.

### Testing workflows for hosted agents

**Development testing**: Test your hosted agent locally during development by using the agent playground and local testing tools before deployment.

**Staging validation**: Deploy to a staging environment to validate behavior by using real Foundry infrastructure while maintaining isolation from production.

**Production monitoring**: Continuously monitor deployed hosted agents by using automated evaluation runs to detect performance degradation or problems.

### Structured evaluation approaches

**Test dataset creation**: Create comprehensive test datasets that cover:

- Common user interaction patterns.
- Edge cases and error scenarios.
- Multiple-turn conversation flows.
- Tool usage scenarios.
- Performance stress tests.

**Supported evaluation metrics**: The Azure AI Evaluation SDK provides the following evaluators for agent workflows:

**Intent Resolution**: Measures how well the agent identifies and understands user requests.**Task Adherence**: Evaluates whether the agent's responses adhere to assigned tasks and system instructions.**Tool Call Accuracy**: Assesses whether the agent makes correct function tool calls for user requests.**Additional Quality Metrics**: Enables the use of relevance, coherence, and fluency with agent messages.

### Evaluation best practices

**Test with representative data**: Create evaluation datasets that represent your actual user interactions and use cases.

**Monitor agent performance**: Use the Foundry portal to track agent performance and review conversation traces.

**Use iterative evaluation**: Regularly evaluate agent versions during development to catch problems early and measure improvements.

For more information about evaluating agents, see [Evaluate your AI agents locally](../../how-to/develop/agent-evaluate-sdk?view=foundry) and [Agent evaluators](../../concepts/evaluation-evaluators/agent-evaluators?view=foundry).

## Publish hosted agents to channels

Publishing transforms your hosted agent from a development asset into a managed Azure resource with a dedicated endpoint, independent identity, and governance capabilities. After you publish your hosted agent, you can share it across multiple channels and platforms.

### Publishing process for hosted agents

When you publish a hosted agent, Microsoft Foundry automatically:

- Creates an agent application resource with a dedicated invocation URL.
- Provisions a distinct agent identity that's separate from your project's shared identity.
- Registers the agent in the Microsoft Entra agent registry for discovery and governance.
- Enables stable endpoint access that remains consistent as you deploy new agent versions.

Unlike prompt-based agents that you can edit in the portal, hosted agents keep their code-based implementation while gaining the same publishing and sharing capabilities.

### Available publishing channels

**Web application preview**: Use a web interface to demonstrate and test your hosted agent with stakeholders. It's instant and shareable.

**Microsoft 365 Copilot and Teams**: Integrate your hosted agent directly into Microsoft 365 Copilot and Microsoft Teams through a streamlined, no-code publishing flow. Your agent appears in the agent store for organizational or shared scope distribution.

**Stable API endpoint**: Access your hosted agent programmatically through a consistent REST API that remains unchanged as you update agent versions.

**Custom applications**: Embed your hosted agent into existing applications by using the stable endpoint and SDK integration.

### Publishing considerations for hosted agents

**Identity management**: Published hosted agents use their own agent identity. You need to reconfigure permissions for any Azure resources that your agent accesses. Permissions for the shared development identity don't automatically transfer.

**Version control**: Publishing creates a deployment that references your current agent version. You can update the published agent by deploying new versions without changing the public endpoint.

**Authentication**: Published agents support RBAC-based authentication by default. This authentication includes automatic permission handling for Azure Bot Service integration when you're publishing to Microsoft 365 channels.

For detailed publishing instructions, see [Publish and share agents](../how-to/publish-agent?view=foundry).

## Troubleshoot hosted agent endpoints

If your agent deployment fails, view error logs by selecting **View deployment logs**. If you get 4xx errors, use the following table to determine next steps. If the agent endpoint returns 5xx status codes, contact Microsoft support.

| Error classification | HTTP status code | Solution |
|---|---|---|
`SubscriptionIsNotRegistered` |
400 | Register the feature or subscription provider. |
`InvalidAcrPullCredentials` (`AcrPullWithMSIFailed` ) |
401 | Fix the managed identity or registry RBAC. |
`UnauthorizedAcrPull` (`AcrPullUnauthorized` ) |
403 | Provide the correct credentials or identity. |
`AcrImageNotFound` |
404 | Correct the image name or tag, or publish the image. |
`RegistryNotFound` |
400/404 | Fix registry DNS or server spelling, or network reachability. |
`ValidationError` |
400 | Correct invalid request fields. |
`UserError` (generic) |
400 | Inspect the message and fix the configuration. |

## Understand preview details

### Limitations during preview

| Dimension | Limit |
|---|---|
| Microsoft Foundry resources with hosted agents per Azure subscription | 100 |
| Maximum number of hosted agents per Foundry resource | 200 |
Maximum `min_replica` count for an agent deployment |
2 |
Maximum `max_replica` count for an agent deployment |
5 |

### Hosting pricing

Billing for managed hosting runtime is enabled no earlier than February 1, 2026, during the preview. For updates on pricing, check the Foundry [pricing page](https://azure.microsoft.com/pricing/details/ai-foundry/).

### Region availability

Currently, North Central US is the only supported region for hosted agents.

### Private networking support

Currently, you can't create hosted agents by using the standard setup within network-isolated Foundry resources. For more information, see [Configure virtual networks](../how-to/virtual-networks?view=foundry).
