---
merged_at: 2026-01-26T23:20:36.856236
merged_files: 5
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/quotas-limits -->

# Foundry Agent Service quotas and limits

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This article describes the quotas and limits for Foundry Agent Service.

## How quotas and limits apply

Foundry Agent Service enforces limits in two places:

**Agent Service limits**. Limits for agent and thread artifacts, such as file uploads, vector store attachments, message counts, and tool registration.**Model limits**. Quotas and rate limits for the model deployments your agents call.

If you're using threads and messages, see [Threads, runs, and messages in Foundry Agent Service](concepts/threads-runs-messages?view=foundry-classic). If you're using file search, see [Vector stores for file search](concepts/vector-stores?view=foundry&preserve-view=true).

## Default quotas and limits for the service

The following table lists default limits enforced by the Agent Service.

| Limit name | Limit value |
|---|---|
| Maximum number of files per agent/thread | 10,000 |
| Maximum file size for agents | 512 MB |
| Maximum size for all uploaded files for agents | 300 GB |
| Maximum file size in tokens for attaching to a vector store | 2,000,000 tokens |
| Maximum number of messages per thread | 100,000 |
Maximum size of `text` content per message |
1,500,000 characters |
| Maximum number of tools registered per agent | 128 |

## What happens when you reach a limit

When you exceed one of the limits in this article, the related operation fails. For example:

**File exceeds the maximum size**: Uploading the file fails. Split the content into smaller files or reduce file size before you upload.**Vector store token limit**: Attaching a file to a vector store fails if the file exceeds the token limit. Reduce the file content or split it into multiple files.**Thread message cap**: Adding messages can fail after a thread reaches the message limit. Create a new thread for a new conversation session, or archive and rotate threads as part of your application design.**Message content size**: Creating a message can fail if the`text`

content is too large. Send smaller messages, or move large content into files and use file search.**Tool registration cap**: Creating or updating an agent can fail if you register too many tools. Register only the tools you need, and prefer fewer, reusable tools.

For file search scenarios, see [Vector stores for file search](concepts/vector-stores?view=foundry&preserve-view=true) for guidance on managing vector store growth.

## Best practices to stay within limits

Use the following practices to reduce limit-related failures:

**Keep files small and focused**. Prefer multiple smaller documents over a single large document.**Avoid very large messages**. Put long content in uploaded files and query it by using file search.**Plan for long conversations**. Treat threads as session state and rotate to new threads when conversations become very long.**Register only required tools**. Remove unused tools from agent definitions.**Monitor usage trends**. Track agent activity and tokens to identify growth early.

## Quotas and limits for models

Agents follow the quotas and rate limits for the model deployments they use.

For current model quotas and limits, see:

To view or request more model quota, see [Manage and increase quotas for resources with Microsoft Foundry (Foundry projects)](../how-to/quota?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/environment-setup -->

# Set up your environment

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Creating your first agent with Foundry Agent Service is a two-step process:

- Set up your agent environment.
- Create and configure your agent using either the SDK of your choice or the Azure Foundry portal.

Use this article to learn more about setting up your agent environment.

### Required permissions

| Action | Required Role |
|---|---|
| Create an account and project | Azure AI Account Owner |
|

## Set up your agent environment

To get started, you need a Microsoft Foundry resource and a Foundry project.

Agents are created within a specific project, and each project acts as an isolated workspace. This means:

- All agents in the same project share access to the same file storage, thread storage (conversation history), and search indexes.
- Data is isolated between projects. Agents in one project cannot access resources from another.
Projects are currently the unit of sharing and isolation in Foundry. See the
[what is AI foundry](../what-is-foundry?view=foundry-classic)article for more information on Foundry projects.

### Prerequisites

- An Azure subscription -
[Create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - Ensure that the individual creating the account and project has the
**Azure AI Account Owner**role at the subscription scope - If configuring a
[standard setup](#choose-your-setup), the same individual must also have permissions to assign roles to required resources (Cosmos DB, Azure AI Search, Azure Blob Storage). For more information on RBAC roles, specific to Agent Service, see[Agent Service RBAC roles](../concepts/rbac-foundry?view=foundry-classic).- The built-in role needed is
**Role Based Access Administrator**. - Alternatively, having the
**Owner**role at the subscription level also satisfies this requirement. - The key permission needed is:
`Microsoft.Authorization/roleAssignments/write`


- The built-in role needed is

### Choose your setup

Agent Service offers three environment configuration modes to suit different needs:

**Basic Setup**:This setup is compatible with OpenAI Assistants and manages agent states using the platform's built-in storage. It includes the same tools and capabilities as the Assistants API, with added support for non-OpenAI models and tools such as Azure AI Search, and Bing.

**Standard Setup**:Includes everything in the basic setup and fine-grained control over your data by allowing you to use your own Azure resources. All customer data—including files, threads, and vector stores—are stored in your own Azure resources, giving you full ownership and control.

**Standard Setup with Bring Your Own (BYO) Virtual Network**:Includes everything in the Standard Setup, with the added ability to operate entirely within your own virtual network. This setup supports Bring Your Own Virtual Network (BYO virtual network), allowing for strict control over data movement and helping prevent data exfiltration by keeping traffic confined to your network environment.


### Compare setup options

Note

Private Network Isolation in the table below refers to Secured Agent outbound communication. Basic setup doesn't apply, and you can use Private Network Isolation for your Agents with Standard Setup only.

Inbound secured communication can be applied to all of setups below, by adding a private endpoint and disabling the inbound public access for your Foundry Account.

| Use Cases | Basic Setup | Standard Setup with Public Networking | Standard Setup with Private Networking |
|---|---|---|---|
| Get started quickly without managing resources | ✅ | ||
| All conversation history, file, and vector stores are stored in your own resources | ✅ | ✅ | |
| Support for Customer Managed Keys (CMK) | ✅ | ✅ | |
| Private Network Isolation (Bring your own virtual network) | ✅ |

### Deployment options

To customize these templates, see [use your own resources](how-to/use-your-own-resources?view=foundry-classic).

If you want support for Private Network Isolation see [network-secured setup](how-to/virtual-networks?view=foundry-classic) for more information on how to bring your own virtual network.

### [Optional] Model selection in autodeploy template

Important

**Don't change the modelFormat parameter.**

The templates only support deployment of Azure OpenAI models. See which Azure OpenAI models are supported in the [model support](concepts/model-region-support?view=foundry-classic) article.

You can customize the model used by your agent by editing the model parameters in the autodeploy template. To deploy a different model, you need to update at least the `modelName`

and `modelVersion`

parameters.

By default, the deployment template is configured with the following values:

| Model Parameter | Default Value |
|---|---|
| modelName | gpt-4o |
| modelFormat | OpenAI (for Azure OpenAI) |
| modelVersion | 2024-11-20 |
| modelSkuName | GlobalStandard |
| modelLocation | eastus |

### What's next?

- Explore more:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/faq -->

# Foundry Agent Service frequently asked questions

Find answers to common questions about Foundry Agent Service.

If you can't find answers to your questions in this article and you still need help, see [Foundry Tools support and help options](../../ai-services/cognitive-services-support-options?view=foundry-classic). Foundry Agent Service is part of Foundry Tools.

For getting started, see:

## Setup and access

### What's the difference between basic setup and standard setup?

**Basic setup** stores agent state in Microsoft-managed resources.

**Standard setup** stores agent data (threads, files, and vector stores) in your Azure resources that you connect through capability hosts.

To compare setup options and choose the right one, see [Set up your environment](environment-setup?view=foundry-classic#choose-your-setup) and [Capability hosts](concepts/capability-hosts?view=foundry-classic).

### What permissions (RBAC roles) do I need?

Role requirements depend on what you're doing. For example, you typically need permissions to create an account and project, and separate permissions to create and edit agents.

For the current role requirements, see [Required permissions](environment-setup?view=foundry-classic#required-permissions) and [Role-based access control (RBAC) in Microsoft Foundry](../concepts/rbac-foundry?view=foundry-classic).

### Where should I start if I'm new to Foundry Agent Service?

Start with [Set up your environment](environment-setup?view=foundry-classic), then create your first agent.

- Classic experience:
[Quickstart: Create a new agent](quickstart?view=foundry-classic) - New Foundry experience:
[Quickstart: Get started with agents in code](../quickstarts/get-started-code?view=foundry-classic)

## General

### Do you store any data used in the Foundry Agent Service API?

Yes. Foundry Agent Service is a stateful API, which means that it retains data. Two types of data are stored in the Foundry Agent Service API:

**Stateful entities**: Conversations and responses created during usage.**Files and vector stores**: Data uploaded during Foundry Agent Service setup or as part of a response generation.

To learn how conversations and responses work, see [Agent runtime components](concepts/runtime-components?view=foundry-classic).

### Where is this data stored?

**Basic setup**: Data is stored in a secure, Microsoft-managed storage account that's logically separated.**Standard setup**: Data is stored in your own Azure resources, so you have full ownership and control.

To learn about setup options that control where data is stored, see [Set up your environment](environment-setup?view=foundry-classic#choose-your-setup).

### How long is this data stored?

Data persists unless you explicitly delete it.

For concepts and terminology (for example, conversation and response), see [Agent runtime components](concepts/runtime-components?view=foundry-classic).

### Does Foundry Agent Service support CMK encryption?

- Basic setup supports Microsoft-managed keys only.
- Standard setup supports customer-managed keys (CMKs).

### Does Microsoft use my data for training models?

No, Microsoft doesn't use your data for training models. For more information, see the [Responsible AI documentation](/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy).

### Where is data stored geographically?

Foundry Agent Service endpoints are regional, and data is stored in the same region as the endpoint. For more information, see the [Azure data residency documentation](https://azure.microsoft.com/explore/global-infrastructure/data-residency/#overview).

### How am I charged for Foundry Agent Service?

You're charged for inference cost (input and output) of the base model that you're using for each agent (for example, gpt-4-0125). If you created multiple agents, you're charged for the base model attached to each agent.

If you enabled the Code Interpreter tool, you're charged for its use per session. For example, if your agent calls Code Interpreter simultaneously in two threads, this activity creates two Code Interpreter sessions. Each of those sessions is charged.

By default, each session is active for one hour. If your user keeps giving instructions to Code Interpreter in the same thread for up to one hour, you pay this fee only once.

File search is billed based on the vector storage that you use.


For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/ai-foundry/).

### Is there any additional pricing or quota for using Foundry Agent Service?

No. All [quotas](quotas-limits?view=foundry-classic) apply to using models with Foundry Agent Service.

## Tools and integrations

### Where can I learn about tools like Code Interpreter and File Search?

Start with [Tools overview](how-to/tools-classic/overview?view=foundry-classic), then see the tool-specific guidance:

### How do I bring my own storage, Azure Cosmos DB, or Azure AI Search for agent data?

Use capability hosts and connect your own resources.

- Concepts:
[Capability hosts](concepts/capability-hosts?view=foundry-classic) - How-to:
[Use your own resources](how-to/use-your-own-resources?view=foundry-classic)

## Monitoring and operations

### How do I monitor Foundry Agent Service?

To understand usage and monitoring options, see [Metrics](how-to/metrics?view=foundry-classic) and [Monitor the service](reference/monitor-service?view=foundry-classic).

### What should I do for business continuity and disaster recovery (BCDR)?

Agent Service BCDR guidance depends on your setup and the resources you provision. For the current guidance, see [BCDR for agents](overview?view=foundry-classic#bcdr-for-agents).

## Virtual networking

### What is virtual network isolation?

Virtual networks help secure inbound and outbound access to your Azure resources. You achieve network isolation through virtual network integrations in Azure.

For Agent Service private networking requirements and limitations, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic).

### Why do I need subnet delegation?

Agent Service networking uses Azure Container Apps. When you deploy into your virtual network, you must use a dedicated subnet delegated to `Microsoft.App/environments`

.

For details, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic) and [Virtual network configuration](/en-us/azure/container-apps/custom-virtual-networks?tabs=workload-profiles-env#subnet).

### What regions are supported for Class A?

Region availability and limitations can change. For the current requirements and limitations, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic).

### What class range is supported for public or private Class A, B, and C subnets?

Only private Class A, B, and C ranges are supported. No public class ranges are supported.

### What is the minimum size for the agent subnet, and how many IPs should I use?

The recommended delegated agent subnet size is /24. The minimum is /27.

For sizing guidance and how IPs are consumed, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic) and [Virtual network configuration](/en-us/azure/container-apps/custom-virtual-networks?tabs=workload-profiles-env#subnet).

### What is the minimum and recommended address range for virtual networks in Foundry Agent Service?

As long as the agent subnet and private endpoints have address space, the address range for virtual networks can be anything.

### Can I use peered virtual networks? Can I have resources in different virtual networks?

Yes. The virtual network is in your subscription, and you should be able to peer with any virtual network. But data transfer is costly, so we don't recommend it. The requirement is that all resources must be in the same region as the Microsoft Foundry resource.

### Do I need to add any FQDNs to an allow list if I'm using an Azure firewall?

Yes. Allow the required fully qualified domain names (FQDNs) for managed identity as described in [Use Azure Firewall with Azure Container Apps](/en-us/azure/container-apps/use-azure-firewall), or allow the `AzureActiveDirectory`

service tag.

For Agent Service private networking guidance, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic).

### Can multiple Microsoft Foundry resources reuse the virtual network?

Yes, multiple Microsoft Foundry resources can reuse a virtual network. But the agent runtime subnet is per Microsoft Foundry account.

### Does the virtual network need to be in the same resource group as Foundry?

They don't need to be in the same resource group, but they do need to be in the same region.

### What additional configuration do I need if I want to add tools to my agents?

If you're using a network-secured setup, some tools require additional configuration, such as private endpoints and resource connections.

For the current guidance and limitations, see [How to use a virtual network with Foundry Agent Service](how-to/virtual-networks?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/overview -->

# What is Foundry Agent Service?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Most businesses don't want just chatbots. They want automation that's faster and has fewer errors. That desire might mean summarizing documents, processing invoices, managing support tickets, or publishing blog posts. In all cases, the goal is the same: freeing people and resources to focus on higher-value work by offloading repetitive and predictable tasks.

Large language models (LLMs) introduce a new type of automation with systems that can understand unstructured data, make decisions, and generate content. In practice, businesses can have difficulty moving beyond demos and into production. LLMs can drift, be incorrect, and lack accountability. Without visibility, policy enforcement, and orchestration, these models are hard to trust in real business workflows.

*Microsoft Foundry* is designed to change that. It's a platform that combines models, tools, frameworks, and governance into a unified system for building intelligent agents. At the center of this system is *Foundry Agent Service*, which enables the operation of agents across development, deployment, and production.

Agent Service connects the core pieces of Foundry, such as models, tools, and frameworks, into a single runtime. It manages conversations, orchestrates tool calls, enforces content safety, and integrates with identity, networking, and observability systems. These capabilities help you build agents that are secure, scalable, and production ready.

By abstracting away infrastructure complexity and enforcing trust and safety by design, Agent Service can help you move from prototype to production with confidence.

## Prerequisites

- An Azure subscription with permission to create and manage Foundry resources.
- A Foundry project. If you haven't created one yet, start with
[environment setup](environment-setup?view=foundry-classic). - A deployed model that your agent can use. Model and region availability can vary; see
[models that inform agents](concepts/model-region-support?view=foundry-classic).

## Availability, regions, and limits

Agent Service capabilities can vary based on the Foundry experience you're using and the model and region you choose.

- For service limits, quotas, and throttling considerations, see
[Quotas and limits for Agent Service](quotas-limits?view=foundry-classic). - For model and region support, see
[models that inform agents](concepts/model-region-support?view=foundry-classic).

If you're building your first agent, start with the quickstart links in [Get started with Foundry Agent Service](#get-started-with-foundry-agent-service) to make sure you're on the right API path for your Foundry experience.

## What is an AI agent?

Agents make decisions, invoke tools, and participate in workflows. They perform these tasks sometimes independently and sometimes in collaboration with other agents or humans. They're foundational to real process automation.

Agents you create through Foundry aren't monoliths. They're composable units. Each agent has a specific role, is powered by the right model, and is equipped with the right tools. You deploy each agent within a secure, observable, and governable runtime.

An agent has three core components:

**Model (LLM)**: Powers reasoning and language understanding.**Instructions**: Define the agent's goals, behavior, and constraints. They can have the following types:- Declarative:
- Prompt based: A declaratively defined single agent that combines model configuration, instruction, tools, and natural language prompts to drive behavior.
- Workflow: An agentic workflow that can be expressed as a YAML or other code to orchestrate multiple agents together, or to trigger an action on certain criteria.

- Hosted: Containerized agents that are created and deployed in code and are hosted by Foundry.

- Declarative:
**Tools**: Let the agent retrieve knowledge or take action.

Agents receive unstructured inputs such as user prompts, alerts, or messages from other agents. They produce outputs in the form of tool results or messages. Along the way, they might call tools to perform retrieval or trigger actions.

## How do agents in Foundry work?

Think of Foundry as an assembly line for intelligent agents. Like any modern factory, Foundry brings together specialized stations that are each responsible for shaping part of the final product. Instead of machines and conveyor belts, the agent factory uses models, tools, policies, and orchestration to build agents that are secure, testable, and production ready. Here's how the factory works step by step:

### 1. Models

The assembly line starts when you select a model that gives your agent its intelligence. Choose from a growing catalog of large language models (LLMs), including GPT-4o, GPT-4, GPT-3.5 (Azure OpenAI), and others like Llama. The model is the reasoning core of the agent that informs its decisions.

### 2. Customizability

Shape the model to fit your use case. Customize your agent with fine-tuning, distillation, or domain-specific prompts. Encode agent behavior, role-specific knowledge, and patterns from prior performance by using data captured from real conversation content and tool results.

### 3. Knowledge and tools

Equip your agent with tools. These tools let the agent access enterprise knowledge (such as Bing, SharePoint, and Azure AI Search) and take real-world actions (via Azure Logic Apps, Azure Functions, OpenAPI, and more). This step enhances the agent's ability to expand its capabilities.

### 4. Orchestration

The agent needs coordination. [Connected agents](how-to/connected-agents?view=foundry-classic) orchestrate the full lifecycle, such as handling tool calls, updating conversation state, managing retries, and logging outputs.

The agent needs coordination. [Workflows](concepts/workflow?view=foundry-classic) orchestrate the full lifecycle, such as handling tool calls, updating conversation state, managing retries, and logging outputs.

### 5. Observability

Test and monitor agents. Foundry can capture logs, traces, and evaluations at every step. With full conversation-level visibility and Application Insights integration, teams can inspect every decision and continuously improve agents over time.

### 6. Trust

Ensure that agents are suitable and reliable for the workload they're assigned to. Foundry applies enterprise-grade trust features, including identity via Microsoft Entra, role-based access control (RBAC), content filters, encryption, and network isolation. You choose how and where your agents run, by using platform-managed or bring-your-own infrastructure.

The result is an agent that's ready for production: reliable, extensible, and safe to deploy across your workflows.

## Why use Foundry Agent Service?

Agent Service provides a production-ready foundation for deploying intelligent agents in enterprise environments. Here's how it compares across key capabilities:

| Capability | Agent Service |
|---|---|
Visibility into conversations |
Full access to structured
|

**Multiple-agent coordination****Tool orchestration****Trust and safety**[content filters](../openai/how-to/content-filters?view=foundry-classic)to help prevent misuse and mitigate prompt injection risks, including cross-prompt injection attacks (XPIA). All outputs are policy governed.**Enterprise integration**[storage](how-to/use-your-own-resources?view=foundry-classic#use-an-existing-azure-cosmos-db-for-nosql-account-for-conversation-storage),[Azure AI Search index](how-to/use-your-own-resources?view=foundry-classic#use-an-existing-azure-ai-search-resource), and[virtual network](how-to/virtual-networks?view=foundry-classic)to meet compliance needs.**Observability and debugging**[Full traceability](../how-to/develop/trace-agents-sdk?view=foundry-classic)of conversations, tool invocations, and message traces;[Application Insights integration](how-to/metrics?view=foundry-classic)for usage data.**Identity and policy control**## Security, privacy, and compliance

Agent Service is designed for enterprise workloads where you need strong controls over identity, networking, data handling, and safety.

**Safety controls**: Use integrated[content filters](../openai/how-to/content-filters?view=foundry-classic)to help reduce unsafe outputs and mitigate prompt injection risks, including cross-prompt injection attacks (XPIA).**Network isolation and data residency controls**: Use[virtual networks](how-to/virtual-networks?view=foundry-classic)and bring-your-own resources to meet your requirements.**Bring your own resources**: Use your own Azure resources (for example, storage, Azure AI Search, and Azure Cosmos DB for conversation state) to meet compliance and operational needs. See[Use your own resources](how-to/use-your-own-resources?view=foundry-classic).**Responsible AI guidance**: For a broader set of recommendations and governance resources, see[Responsible AI for Microsoft Foundry](../responsible-use-of-ai-overview?view=foundry-classic).

## Get started with Foundry Agent Service

To get started with Agent Service, create a Foundry project in your Azure subscription.

If you're building in code, see [Microsoft Foundry SDKs](../how-to/develop/sdk-overview?view=foundry-classic) for SDK options and guidance.

If it's your first time using the service, start with the [environment setup](environment-setup?view=foundry-classic) and [quickstart](quickstart?view=foundry-classic) guides.

If it's your first time using the service, start with the [environment setup](environment-setup?view=foundry-classic) and [quickstart](../tutorials/quickstart-create-foundry-resources?view=foundry-classic) guides.

Create a project with the required resources. After you create a project, deploy a compatible model such as GPT-4o. When you have a deployed model, you can start making API calls to Agent Service by using the SDKs.

You can find a list of official samples with the new Python agent SDK on [GitHub](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-projects).

## BCDR for agents

To support service resilience, Agent Service relies on customer-provisioned Azure Cosmos DB accounts for business continuity and disaster recovery (BCDR). This approach helps ensure that your agent state can be preserved and recovered in the event of a regional outage.

As an Azure Standard customer, you provision and manage your own single-tenant Azure Cosmos DB account. You store all agent state in this account. You control backup and recovery through native capabilities in Azure Cosmos DB.

If the primary region becomes unavailable, the agent automatically connects to the same Azure Cosmos DB account in the secondary region. Because Cosmos DB preserves all history, the agent can continue operation with minimal disruption.

Provision and maintain your Azure Cosmos DB account, and configure appropriate backup and recovery policies. This effort helps ensure seamless continuity if the primary region becomes unavailable.

For configuration guidance, see [Use your own resources](how-to/use-your-own-resources?view=foundry-classic) and [virtual networks](how-to/virtual-networks?view=foundry-classic).

## Costs

Using Agent Service can incur costs from the model you deploy and the Azure resources you use for your project (for example, logging and any customer-managed resources you connect).

To understand and manage cost drivers, see [Plan and manage costs](../concepts/manage-costs?view=foundry-classic).

## Troubleshooting

If you're blocked getting started, check these common issues:

**Model isn't available in your region**: See[models that inform agents](concepts/model-region-support?view=foundry-classic).**Requests are throttled or fail due to quota**: See[Quotas and limits for Agent Service](quotas-limits?view=foundry-classic).**You can't access resources or deployments**: Confirm your role assignments and follow[environment setup](environment-setup?view=foundry-classic).**You need to debug tool calls or agent behavior**: Start with[trace agents with the SDK](../how-to/develop/trace-agents-sdk?view=foundry-classic)and[metrics](how-to/metrics?view=foundry-classic).

## Related content

- Learn more about the
[models that inform agents](concepts/model-region-support?view=foundry-classic). - Learn about the
[Microsoft Foundry SDKs](../how-to/develop/sdk-overview?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/quickstart -->

# Quickstart: Create a new agent

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Note

This quickstart is for the previous version of agents. See the [ quickstart for Microsoft Foundry](../quickstarts/get-started-code?view=foundry&preserve-view=true) to use the new version of the API.

Foundry Agent Service allows you to create AI agents tailored to your needs through custom instructions and augmented by advanced tools like code interpreter, and custom functions.

## Prerequisites

- An Azure subscription -
[Create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - Ensure that the individual creating the account and project has the
**Azure AI Account Owner**role at the subscription scope, which will grant the necessary permissions for creating the project- Alternatively, having the
**Contributor**or**Owner**role at the subscription level will allow the creation of the project

- Alternatively, having the
- Once the project is created, ensure that the individual creating the agent within the project has the
**Azure AI User**role at the project level

Important

The Microsoft Foundry portal only supports basic agent setup at this time. If you want to perform a standard agent setup, see the [Environment setup](environment-setup?view=foundry-classic) article to learn about more.

## Create a Foundry account and project in Foundry portal

To create an account and project in Foundry, follow these steps:

Go to Foundry. If you are in a project, select Foundry at the top left of the page to go to the Home page.

Use the Agent getting started creation flow for the fastest experience. Click

**Create an agent**.Enter a name for the project. If you want to customize the default values, select

**Advanced options**.Select

**Create**.Wait for your resources to be provisioned.

- An account and project (child resource of your account) will be created.
- The gpt-4o model will automatically be deployed
- A default agent will be created

Once complete, you will land directly in the agent playground and you can start creating agents. You can give your agent instructions on what to do and how to do it. For example:

*"You are a helpful agent that can answer questions about geography."*Then you can start chatting with your agent.Note

If you are getting permission error when trying to configure or create agents ensure you have the

**Azure AI User**on the project.

| [Reference documentation](/en-us/dotnet/api/overview/azure/ai.agents.persistent-readme) | [Samples](https://github.com/azure-ai-foundry/foundry-samples/tree/main/samples-classic/csharp/getting-started-agents) | [Library source code](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/ai/Azure.AI.Agents.Persistent) | [Package (NuGet)](https://www.nuget.org/packages/Azure.AI.Agents.Persistent) |

## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

Create a .NET Console project.

```
dotnet new console
```


Install the .NET package to your project. For example if you're using the .NET CLI, run the following command.

```
dotnet add package Azure.AI.Agents.Persistent
dotnet add package Azure.Identity
```


Next, to authenticate your API requests and run the program, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Use the following code to create and run an agent. To run this code, you will need to get the endpoint for your project. This string is in the format:

`https://<AIFoundryResourceName>.services.ai.azure.com/api/projects/<ProjectName>`


Important

Starting in May 2025, the Azure AI Agent Service uses an endpoint for [Foundry projects](../what-is-foundry?view=foundry-classic#types-of-projects) instead of the connection string that was previously used for hub-based projects. If you're using a hub-based project, you won't be able to use the current versions of the SDK and REST API. For more information, see [SDK usage with hub-based projects](how-to/use-your-own-resources?view=foundry-classic#sdk-usage-with-hub-based-projects).

You can find your endpoint in the **overview** for your project in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs), under **Libraries** > **Foundry**.

Set this endpoint in an environment variable named `ProjectEndpoint`

.

You also need your model's deployment name. You can find it in **Models + Endpoints** in the left navigation menu.

Save the name of your model deployment name as an environment variable named `ModelDeploymentName`

.

```
using Azure;
using Azure.AI.Agents.Persistent;
using Azure.Identity;
using System.Diagnostics;
var projectEndpoint = System.Environment.GetEnvironmentVariable("ProjectEndpoint");
var modelDeploymentName = System.Environment.GetEnvironmentVariable("ModelDeploymentName");
//Create a PersistentAgentsClient and PersistentAgent.
PersistentAgentsClient client = new(projectEndpoint, new DefaultAzureCredential());
//Give PersistentAgent a tool to execute code using CodeInterpreterToolDefinition.
PersistentAgent agent = client.Administration.CreateAgent(
model: modelDeploymentName,
name: "My Test Agent",
instructions: "You politely help with math questions. Use the code interpreter tool when asked to visualize numbers.",
tools: [new CodeInterpreterToolDefinition()]
);
//Create a thread to establish a session between Agent and a User.
PersistentAgentThread thread = client.Threads.CreateThread();
//Ask a question of the Agent.
client.Messages.CreateMessage(
thread.Id,
MessageRole.User,
"Hi, Agent! Draw a graph for a line with a slope of 4 and y-intercept of 9.");
//Have Agent begin processing user's question with some additional instructions associated with the ThreadRun.
ThreadRun run = client.Runs.CreateRun(
thread.Id,
agent.Id,
additionalInstructions: "Please address the user as Jane Doe. The user has a premium account.");
//Poll for completion.
do
{
Thread.Sleep(TimeSpan.FromMilliseconds(500));
run = client.Runs.GetRun(thread.Id, run.Id);
}
while (run.Status == RunStatus.Queued
|| run.Status == RunStatus.InProgress
|| run.Status == RunStatus.RequiresAction);
//Get the messages in the PersistentAgentThread. Includes Agent (Assistant Role) and User (User Role) messages.
Pageable<PersistentThreadMessage> messages = client.Messages.GetMessages(
threadId: thread.Id,
order: ListSortOrder.Ascending);
//Display each message and open the image generated using CodeInterpreterToolDefinition.
foreach (PersistentThreadMessage threadMessage in messages)
{
foreach (MessageContent content in threadMessage.ContentItems)
{
switch (content)
{
case MessageTextContent textItem:
Console.WriteLine($"[{threadMessage.Role}]: {textItem.Text}");
break;
case MessageImageFileContent imageFileContent:
Console.WriteLine($"[{threadMessage.Role}]: Image content file ID = {imageFileContent.FileId}");
BinaryData imageContent = client.Files.GetFileContent(imageFileContent.FileId);
string tempFilePath = Path.Combine(AppContext.BaseDirectory, $"{Guid.NewGuid()}.png");
File.WriteAllBytes(tempFilePath, imageContent.ToArray());
client.Files.DeleteFile(imageFileContent.FileId);
ProcessStartInfo psi = new()
{
FileName = tempFilePath,
UseShellExecute = true
};
Process.Start(psi);
break;
}
}
}
//If you want to delete your agent, uncomment the following lines:
//client.Threads.DeleteThread(threadId: thread.Id);
//client.Administration.DeleteAgent(agentId: agent.Id);
```


| [Reference documentation](https://aka.ms/azsdk/azure-ai-projects/python/reference) | [Samples](https://aka.ms/azsdk/azure-ai-projects/python/samples/) | [Library source code](https://aka.ms/azsdk/azure-ai-projects/python/code) | [Package (PyPi)](https://aka.ms/azsdk/azure-ai-projects/python/package) |

## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

Run the following commands to install the python packages.

```
pip install azure-ai-projects
pip install azure-identity
```


Next, to authenticate your API requests and run the program, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Use the following code to create and run an agent. To run this code, you will need to get the endpoint for your project. This string is in the format:

`https://<AIFoundryResourceName>.services.ai.azure.com/api/projects/<ProjectName>`


Important

Starting in May 2025, the Azure AI Agent Service uses an endpoint for [Foundry projects](../what-is-foundry?view=foundry-classic#types-of-projects) instead of the connection string that was previously used for hub-based projects. If you're using a hub-based project, you won't be able to use the current versions of the SDK and REST API. For more information, see [SDK usage with hub-based projects](how-to/use-your-own-resources?view=foundry-classic#sdk-usage-with-hub-based-projects).

You can find your endpoint in the **overview** for your project in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs), under **Libraries** > **Foundry**.

Set this endpoint as an environment variable named `PROJECT_ENDPOINT`

.

You also need your model's deployment name. You can find it in **Models + Endpoints** in the left navigation menu.

Save the name of your model deployment name as an environment variable named `MODEL_DEPLOYMENT_NAME`

.

```
import os
from pathlib import Path
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential
from azure.ai.agents.models import CodeInterpreterTool
# Create an AIProjectClient instance
project_client = AIProjectClient(
endpoint=os.getenv("PROJECT_ENDPOINT"),
credential=DefaultAzureCredential(),
# Use Azure Default Credential for authentication
)
with project_client:
code_interpreter = CodeInterpreterTool()
agent = project_client.agents.create_agent(
model=os.getenv("MODEL_DEPLOYMENT_NAME"), # Model deployment name
name="my-agent", # Name of the agent
instructions="""You politely help with math questions.
Use the Code Interpreter tool when asked to visualize numbers.""",
# Instructions for the agent
tools=code_interpreter.definitions, # Attach the tool
tool_resources=code_interpreter.resources, # Attach tool resources
)
print(f"Created agent, ID: {agent.id}")
# Create a thread for communication
thread = project_client.agents.threads.create()
print(f"Created thread, ID: {thread.id}")
question = """Draw a graph for a line with a slope of 4
and y-intercept of 9 and provide the file to me?"""
# Add a message to the thread
message = project_client.agents.messages.create(
thread_id=thread.id,
role="user", # Role of the message sender
content=question, # Message content
)
print(f"Created message, ID: {message['id']}")
# Create and process an agent run
run = project_client.agents.runs.create_and_process(
thread_id=thread.id,
agent_id=agent.id,
additional_instructions="""Please address the user as Jane Doe.
The user has a premium account.""",
)
print(f"Run finished with status: {run.status}")
# Check if the run failed
if run.status == "failed":
print(f"Run failed: {run.last_error}")
# Fetch and log all messages
messages = project_client.agents.messages.list(thread_id=thread.id)
print(f"Messages: {messages}")
for message in messages:
print(f"Role: {message.role}, Content: {message.content}")
for this_content in message.content:
print(f"Content Type: {this_content.type}, Content Data: {this_content}")
if this_content.text.annotations:
for annotation in this_content.text.annotations:
print(f"Annotation Type: {annotation.type}, Text: {annotation.text}")
print(f"Start Index: {annotation.start_index}")
print(f"End Index: {annotation.end_index}")
print(f"File ID: {annotation.file_path.file_id}")
# Save every image file in the message
file_id = annotation.file_path.file_id
file_name = f"{file_id}_image_file.png"
project_client.agents.files.save(file_id=file_id, file_name=file_name)
print(f"Saved image file to: {Path.cwd() / file_name}")
#Uncomment these lines to delete the agent when done
#project_client.agents.delete_agent(agent.id)
#print("Deleted agent")
```


| [Reference documentation](/en-us/javascript/api/overview/azure/ai-projects-readme) | [Samples](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/ai/ai-projects/README.md) | [Library source code](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-projects) | [Package (npm)](https://www.npmjs.com/package/@azure/ai-projects) |

## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

Key objects in this code include:

First, initialize a new TypeScript project by running:

```
npm init -y
npm pkg set type="module"
```


Run the following commands to install the npm packages required.

```
npm install @azure/ai-agents @azure/identity
npm install @types/node typescript --save-dev
```


Next, to authenticate your API requests and run the program, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Use the following code to answer the math question `I need to solve the equation '3x + 11 = 14'. Can you help me?`

. To run this code, you'll need to get the endpoint for your project. This string is in the format:

`https://<AIFoundryResourceName>.services.ai.azure.com/api/projects/<ProjectName>`


You can find your endpoint in the **overview** for your project in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs), under **Libraries** > **Foundry**.

Set this endpoint as an environment variable named `PROJECT_ENDPOINT`

in a `.env`

file.

You also need your model's deployment name. You can find it in **Models + Endpoints** in the left navigation menu.

Save the name of your model deployment name as an environment variable named `MODEL_DEPLOYMENT_NAME`

.

Important

- This quickstart code uses environment variables for sensitive configuration. Never commit your
`.env`

file to version control by making sure`.env`

is listed in your`.gitignore`

file. *Remember: If you accidentally commit sensitive information, consider those credentials compromised and rotate them immediately.*

Create a tsconfig.json file with the following content:

```
{
"compilerOptions": {
"module": "nodenext",
"target": "esnext",
"types": ["node"],
"lib": ["esnext"],
"sourceMap": true,
"declaration": true,
"declarationMap": true,
"noUncheckedIndexedAccess": true,
"exactOptionalPropertyTypes": true,
"strict": true,
"verbatimModuleSyntax": true,
"isolatedModules": true,
"noUncheckedSideEffectImports": true,
"moduleDetection": "force",
"skipLibCheck": true,
}
}
```


Next, create an `index.ts`

file and paste in the following code:

```
import { AgentsClient } from "@azure/ai-agents";
import { DefaultAzureCredential } from "@azure/identity";
const projectEndpoint = process.env["PROJECT_ENDPOINT"] || "<project endpoint>";
const modelDeploymentName = process.env["MODEL_DEPLOYMENT_NAME"] || "gpt-4o";
export async function main(): Promise<void> {
// Create an Azure AI Client
const client = new AgentsClient(projectEndpoint, new DefaultAzureCredential());
// Create an agent
const agent = await client.createAgent(modelDeploymentName, {
name: "my-agent",
instructions: "You are a helpful agent specialized in math. When providing mathematical explanations, use plain text formatting with simple characters like +, -, *, / for operations. Do not use LaTeX formatting with backslashes or special notation. Make your explanations clear and easy to read in a terminal.",
});
console.log(`Created agent, agent ID : ${agent.id}`);
// Create a thread
const thread = await client.threads.create();
console.log(`Created thread, thread ID : ${thread.id}`);
// List all threads for the agent
const threads = client.threads.list();
console.log(`Threads for agent ${agent.id}:`);
for await (const t of threads) {
console.log(`Thread ID: ${t.id} created at: ${t.createdAt}`);
}
// Create a message
const message = await client.messages.create(thread.id, "user", "I need to solve the equation `3x + 11 = 14`. Can you help me?");
console.log(`Created message, message ID : ${message.id}`);
// Create and poll a run
console.log("Creating run...");
const run = await client.runs.createAndPoll(thread.id, agent.id, {
pollingOptions: {
intervalInMs: 2000,
},
onResponse: (response): void => {
const parsedBody =
typeof response.parsedBody === "object" && response.parsedBody !== null
? response.parsedBody
: null;
const status = parsedBody && "status" in parsedBody ? parsedBody.status : "unknown";
console.log(`Received response with status: ${status}`);
},
});
console.log(`Run finished with status: ${run.status}`);
const messagesIterator = client.messages.list(thread.id);
console.log("\n\n========================================================");
console.log("=================== CONVERSATION RESULTS ===================");
console.log("========================================================\n");
// Collect all messages first
const messages = [];
for await (const m of messagesIterator) {
messages.push(m);
}
// Reverse the order of messages (or sort by timestamp if available)
messages.reverse();
// Display messages in the new order
for (const m of messages) {
if (m.role === "user") {
console.log(`\n❓ USER QUESTION: ${
Array.isArray(m.content) && m.content[0]?.type === "text" && 'text' in m.content[0]
? m.content[0].text.value
: JSON.stringify(m.content)
}`);
} else if (m.role === "assistant") {
console.log("\n🤖 ASSISTANT'S ANSWER:");
console.log("--------------------------------------------------");
// Extract and print the text content in a more readable format
if (m.content && Array.isArray(m.content)) {
for (const content of m.content) {
if (content.type === "text" && 'text' in content) {
console.log(content.text?.value);
} else {
console.log(content);
}
}
} else {
console.log(JSON.stringify(m.content, null, 2));
}
console.log("--------------------------------------------------\n");
}
}
console.log("\n========================================================");
console.log("====================== END OF RESULTS ======================");
console.log("========================================================\n");
// Clean up
await client.threads.delete(thread.id);
await client.deleteAgent(agent.id);
}
main().catch((err) => {
console.error("The sample encountered an error:", err);
});
```


Run the code using `npx tsx -r dotenv/config index.ts`

. This code answers the question `I need to solve the equation '3x + 11 = 14'. Can you help me?`

. Responses aren't deterministic, your output will look similar to the below output:

```
Created agent, agent ID : asst_X4yDNWrdWKb8LN0SQ6xlzhWk
Created thread, thread ID : thread_TxqZcHL2BqkNWl9dFzBYMIU6
Threads for agent asst_X4yDNWrdWKb8LN0SQ6xlzhWk:
...
Created message, message ID : msg_R0zDsXdc2UbfsNXvS1zeS6hk
Creating run...
Received response with status: queued
Received response with status: in_progress
Received response with status: completed
Run finished with status: completed
========================================================
=================== CONVERSATION RESULTS ===================
========================================================
❓ USER QUESTION: I need to solve the equation `3x + 11 = 14`. Can you help me?
🤖 ASSISTANT'S ANSWER:
--------------------------------------------------
Certainly! Let's solve the equation step by step:
We have:
3x + 11 = 14
### Step 1: Eliminate the constant (+11) on the left-hand side.
Subtract 11 from both sides:
3x + 11 - 11 = 14 - 11
This simplifies to:
3x = 3
We have:
3x + 11 = 14
### Step 1: Eliminate the constant (+11) on the left-hand side.
Subtract 11 from both sides:
3x + 11 - 11 = 14 - 11
This simplifies to:
3x = 3
### Step 2: Solve for x.
Divide both sides by 3:
3x / 3 = 3 / 3
This simplifies to:
x = 1
### Final Answer:
x = 1
--------------------------------------------------
========================================================
====================== END OF RESULTS ======================
========================================================
```


Full [sample source code](https://github.com/Azure-Samples/azure-sdk-for-js-docs/blob/main/samples/foundry/azure-ai-agents-quickstart-math) available.

| [Reference documentation](/en-us/java/api/overview/azure/ai-agents-persistent-readme) | [Samples](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-agents-persistent/src/samples/java/com/azure/ai/agents/persistent) | [Library source code](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-agents-persistent) | [Package (Maven)](https://central.sonatype.com/artifact/com.azure/azure-ai-agents-persistent) |

## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

First, create a New Java console project. You'll need the following dependencies to run the code:

```
<dependencies>
<dependency>
<groupId>com.azure</groupId>
<artifactId>azure-ai-agents-persistent</artifactId>
<version>1.0.0-beta.2</version>
</dependency>
<dependency>
<groupId>com.azure</groupId>
<artifactId>azure-identity</artifactId>
<version>1.17.0-beta.1</version>
</dependency>
</dependencies>
```


Next, to authenticate your API requests and run the program, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Use the following code to create and run an agent. To run this code, you'll need to get the endpoint for your project. This string is in the format:

`https://<AIFoundryResourceName>.services.ai.azure.com/api/projects/<ProjectName>`


Important

Starting in May 2025, the Azure AI Agent Service uses an endpoint for [Foundry projects](../what-is-foundry?view=foundry-classic#types-of-projects) instead of the connection string that was previously used for hub-based projects. If you're using a hub-based project, you won't be able to use the current versions of the SDK and REST API. For more information, see [SDK usage with hub-based projects](how-to/use-your-own-resources?view=foundry-classic#sdk-usage-with-hub-based-projects).

You can find your endpoint in the **overview** for your project in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs), under **Libraries** > **Foundry**.

Set this endpoint in an environment variable named `PROJECT_ENDPOINT`

.

You also need your model's deployment name. You can find it in **Models + Endpoints** in the left navigation menu.

Save the name of your model deployment name as an environment variable named `MODEL_DEPLOYMENT_NAME`

.

## Code example

```
package com.example.agents;
import com.azure.ai.agents.persistent.MessagesClient;
import com.azure.ai.agents.persistent.PersistentAgentsAdministrationClient;
import com.azure.ai.agents.persistent.PersistentAgentsClient;
import com.azure.ai.agents.persistent.PersistentAgentsClientBuilder;
import com.azure.ai.agents.persistent.RunsClient;
import com.azure.ai.agents.persistent.ThreadsClient;
import com.azure.ai.agents.persistent.models.CodeInterpreterToolDefinition;
import com.azure.ai.agents.persistent.models.CreateAgentOptions;
import com.azure.ai.agents.persistent.models.CreateRunOptions;
import com.azure.ai.agents.persistent.models.MessageImageFileContent;
import com.azure.ai.agents.persistent.models.MessageRole;
import com.azure.ai.agents.persistent.models.MessageTextContent;
import com.azure.ai.agents.persistent.models.PersistentAgent;
import com.azure.ai.agents.persistent.models.PersistentAgentThread;
import com.azure.ai.agents.persistent.models.RunStatus;
import com.azure.ai.agents.persistent.models.ThreadMessage;
import com.azure.ai.agents.persistent.models.ThreadRun;
import com.azure.ai.agents.persistent.models.MessageContent;
import com.azure.core.http.rest.PagedIterable;
import com.azure.identity.DefaultAzureCredentialBuilder;
import java.util.Arrays;
public class AgentSample {
public static void main(String[] args) {
// variables for authenticating requests to the agent service
String projectEndpoint = System.getenv("PROJECT_ENDPOINT");
String modelName = System.getenv("MODEL_DEPLOYMENT_NAME");
// initialize clients to manage various aspects of agent runtime
PersistentAgentsClientBuilder clientBuilder = new PersistentAgentsClientBuilder()
.endpoint(projectEndpoint)
.credential(new DefaultAzureCredentialBuilder().build());
PersistentAgentsClient agentsClient = clientBuilder.buildClient();
PersistentAgentsAdministrationClient administrationClient = agentsClient.getPersistentAgentsAdministrationClient();
ThreadsClient threadsClient = agentsClient.getThreadsClient();
MessagesClient messagesClient = agentsClient.getMessagesClient();
RunsClient runsClient = agentsClient.getRunsClient();
String agentName = "my-agent"; // the name of the agent
CreateAgentOptions createAgentOptions = new CreateAgentOptions(modelName)
.setName(agentName)
.setInstructions("You are a helpful agent") // system instructions
.setTools(Arrays.asList(new CodeInterpreterToolDefinition()));
PersistentAgent agent = administrationClient.createAgent(createAgentOptions);
PersistentAgentThread thread = threadsClient.createThread();
ThreadMessage createdMessage = messagesClient.createMessage(
thread.getId(),
MessageRole.USER,
"I need to solve the equation `3x + 11 = 14`. Can you help me?"); // The message to the agent
try {
//run the agent
CreateRunOptions createRunOptions = new CreateRunOptions(thread.getId(), agent.getId())
.setAdditionalInstructions("");
ThreadRun threadRun = runsClient.createRun(createRunOptions);
// wait for the run to complete before printing the message
waitForRunCompletion(thread.getId(), threadRun, runsClient);
printRunMessages(messagesClient, thread.getId());
} catch (InterruptedException e) {
throw new RuntimeException(e);
} finally {
//cleanup - uncomment these lines if you want to delete the agent
//threadsClient.deleteThread(thread.getId());
//administrationClient.deleteAgent(agent.getId());
}
}
// A helper function to print messages from the agent
public static void printRunMessages(MessagesClient messagesClient, String threadId) {
PagedIterable<ThreadMessage> runMessages = messagesClient.listMessages(threadId);
for (ThreadMessage message : runMessages) {
System.out.print(String.format("%1$s - %2$s : ", message.getCreatedAt(), message.getRole()));
for (MessageContent contentItem : message.getContent()) {
if (contentItem instanceof MessageTextContent) {
System.out.print((((MessageTextContent) contentItem).getText().getValue()));
} else if (contentItem instanceof MessageImageFileContent) {
String imageFileId = (((MessageImageFileContent) contentItem).getImageFile().getFileId());
System.out.print("Image from ID: " + imageFileId);
}
System.out.println();
}
}
}
// a helper function to wait until a run has completed running
public static void waitForRunCompletion(String threadId, ThreadRun threadRun, RunsClient runsClient)
throws InterruptedException {
do {
Thread.sleep(500);
threadRun = runsClient.getRun(threadId, threadRun.getId());
}
while (
threadRun.getStatus() == RunStatus.QUEUED
|| threadRun.getStatus() == RunStatus.IN_PROGRESS
|| threadRun.getStatus() == RunStatus.REQUIRES_ACTION);
if (threadRun.getStatus() == RunStatus.FAILED) {
System.out.println(threadRun.getLastError().getMessage());
}
}
}
```


## Prerequisites

[A set up agent environment](environment-setup?view=foundry-classic)- Assign the
**Azure AI User**[RBAC role](../concepts/rbac-foundry?view=foundry-classic)to each team member who needs to create or edit agents using the SDK or Agent Playground- This role must be assigned at the project scope
- Minimum required permissions:
**agents/*/read**,**agents/*/action**,**agents/*/delete**


## Configure and run an agent

To authenticate your API requests, use the [az login](/en-us/cli/azure/authenticate-azure-cli-interactively) command to sign into your Azure subscription.

```
az login
```


Next, you'll need to fetch the Entra ID token to provide as authorization to the API calls. Fetch the token using the CLI command:

```
az account get-access-token --resource 'https://ai.azure.com' | jq -r .accessToken | tr -d '"'
```


Set the access token as an environment variable named `AGENT_TOKEN`

.

To successfully make REST API calls to Foundry Agent Service, you will need to use your project's endpoint:

`https://<your_ai_service_name>.services.ai.azure.com/api/projects/<your_project_name>`


For example, your endpoint will look something like:

`https://exampleaiservice.services.ai.azure.com/api/projects/project`


Set this endpoint as an environment variable named `AZURE_AI_FOUNDRY_PROJECT_ENDPOINT`

.

Note

- For
`api-version`

parameter, the GA API version is`2025-05-01`

and the latest preview API version is`2025-05-15-preview`

. You must use the preview API for tools that are in preview. - Consider making your API version an environment variable, such as
`$API_VERSION`

.

### Create an agent

Note

With Azure AI Agents Service the `model`

parameter requires model deployment name. If your model deployment name is different than the underlying model name, then you would adjust your code to ` "model": "{your-custom-model-deployment-name}"`

.

```
curl --request POST \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/assistants?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN" \
-H "Content-Type: application/json" \
-d '{
"instructions": "You are a helpful agent.",
"name": "my-agent",
"tools": [{"type": "code_interpreter"}],
"model": "gpt-4o-mini"
}'
```


### Create a thread

```
curl --request POST \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN" \
-H "Content-Type: application/json" \
-d ''
```


### Add a user question to the thread

```
curl --request POST \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads/thread_abc123/messages?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN" \
-H "Content-Type: application/json" \
-d '{
"role": "user",
"content": "I need to solve the equation `3x + 11 = 14`. Can you help me?"
}'
```


### Run the thread

```
curl --request POST \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads/thread_abc123/runs?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN" \
-H "Content-Type: application/json" \
-d '{
"assistant_id": "asst_abc123",
}'
```


### Retrieve the status of the run

```
curl --request GET \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads/thread_abc123/runs/run_abc123?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN"
```


### Retrieve the agent response

```
curl --request GET \
--url $AZURE_AI_FOUNDRY_PROJECT_ENDPOINT/threads/thread_abc123/messages?api-version=2025-05-01 \
-H "Authorization: Bearer $AGENT_TOKEN"
```


## Next steps

Learn about the [ tools](how-to/tools/overview?view=foundry-classic) you can use to extend your agents' capabilities, such as accessing the web, provide grounding information, and more.
