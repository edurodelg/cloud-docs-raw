---
merged_at: 2026-01-29T15:40:29.812452
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/mcp/get-started -->

# Get started with Foundry MCP Server (preview) using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Foundry MCP Server (preview) is a Microsoft-managed, cloud-hosted implementation of the Model Context Protocol (MCP). It exposes curated tools that let your agents perform read and write operations against Foundry services without calling backend APIs directly.

Use an MCP-compliant client such as Visual Studio Code to connect to the public endpoint, authenticate with Entra ID, and let LLMs access the tools. After you connect, you can build agents that invoke these tools with natural language prompts.

In this article, you learn how to:

- Connect to Foundry MCP Server with GitHub Copilot in Visual Studio Code
- Run prompts to test Foundry MCP Server tools and interact with Azure resources

Note

This feature is currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

- Azure account with an active subscription. If you don't have one,
[create a free Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - Foundry project. If you don't have a project, create one with the
[Microsoft Foundry SDK Quickstart](/en-us/azure/ai-foundry/quickstarts/get-started-code?tabs=python#first-run-experience). [Visual Studio Code](https://code.visualstudio.com/download).[GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)Visual Studio Code extension.

## Benefits of Foundry MCP Server

**Cloud-hosted interface for AI tool orchestration**: Foundry MCP Server (preview) provides a secure, scalable endpoint for MCP-compliant clients. You don't need to deploy infrastructure, enabling seamless integration and multi-agent scenarios.**Identity and access control**: The server enforces authentication and authorization with Microsoft Entra ID. It performs all operations within the authenticated user's permissions (On-Behalf-Of flow).**Scenario-focused, extensible tools**: The MCP Server exposes a growing set of tools for read and write operations on models, deployments, evaluations, and agents in Foundry. The tools are extensible, letting developers and agents interact with services without knowing backend APIs or data schemas.**Accelerated agent and developer productivity**: Natural language workflows (via MCP clients and large language models) enable rapid tool discovery and invocation, streamlining development and multi-agent orchestration.

## Install and start Foundry MCP Server

Select an option to install Foundry MCP Server in Visual Studio Code.

Install Foundry MCP Server in your user profile so it's available to all workspaces in Visual Studio Code.

Open the

**Command Palette**(`Ctrl`+`Shift`+`P`).Search for

**MCP:Add Server**.Select the

**HTTP (Http or Server-Sent Events)**option.Enter

`https://mcp.ai.azure.com`

as the URL.Enter a friendly name such as

*foundry-mcp-remote*, then press`Enter`. Visual Studio Code adds the following server entry under your user profile:`{ "servers": { "foundry-mcp-remote": { "type": "http", "url": "https://mcp.ai.azure.com" } } }`

Open the

**Command Palette**(`Ctrl`+`Shift`+`P`).Search for and select

**MCP:List Servers**.Select Foundry MCP Server you added and choose

**Start Server**.When prompted, sign in to Azure so the MCP server can interact with services in your subscription.

Open GitHub Copilot and select

**Agent Mode**.Select the tools icon, search for

*Foundry*to filter the list, and confirm the server appears.Learn more about Agent Mode in the

[Visual Studio Code documentation](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode).

## Use prompts to test Foundry MCP Server

Open the GitHub Copilot chat panel and confirm

**Agent Mode**is selected.Enter a prompt that uses Foundry MCP Server tools—for example

*Tell me about the latest models on Foundry*.Copilot requests permission to run the required Foundry MCP Server operation. Select

**Continue**or use the arrow to choose a more specific behavior:**Current session**always runs the operation in the current GitHub Copilot Agent Mode session.**Current workspace**always runs the command for the current Visual Studio Code workspace.**Always allow**sets the operation to always run for any GitHub Copilot Agent Mode session or any Visual Studio Code workspace.

The response resembles the following shortened output:

`Latest / Notable Foundry Models (Preview Snapshot) Curated from the model catalog and benchmark data you requested. I've grouped by category and highlighted truly recent arrivals (2025 releases or late 2024 previews), plus why you'd pick them. Where available, I note cost, performance, or capability signals (e.g., throughput_gtps, reasoning focus, modality). 1. Frontier & Reasoning Models gpt-5-pro (2025-10-06) – Latest flagship conversational / reasoning model from OpenAI; expect top-tier multi-turn coherence and complex tool orchestration. gpt-5 (2025-08-07), gpt-5-mini, gpt-5-nano – New performance tiers; mini/nano are cost-optimized for high-volume requests. o3-pro (2025-06-10) – High reasoning accuracy (multiple >0.95 accuracy slices) but very high latency (p50 ~102s) indicating chain-of-thought style deliberation. Use only for tasks requiring deep reasoning (complex math, logic). o3 (2025-04-16) – Balanced reasoning; much faster than o3-pro; good accuracy/quality trade-off. o4-mini (2025-04-16) – Successor in "o" line; strong quality with better latency than o3-pro. Phi-4 (versions through 7) – Microsoft small frontier open model; competitive quality at radically lower token cost (input $0.125 / 1M tokens). Strong for cost-sensitive general tasks. // Further output omitted`

Explore and test Foundry MCP Server operations with other prompts, such as:

`What tools can I use from Foundry MCP Server (preview)? Tell me about the latest models on Foundry Show me details about the GPT-5-mini model on Foundry`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/mcp/available-tools -->

# Available tools and example prompts for Foundry MCP Server (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the following sections to find available tools and example prompts for Foundry MCP Server (preview). Foundry MCP Server lets you use conversational prompts instead of API calls to interact with Foundry services.

Note

This feature is currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Dataset management

**evaluation_dataset_create (write)**

Create or update a dataset version in a Foundry project.

Example prompts include:

- "Upload my customer support Q&A dataset from this Azure Blob Storage URL."
- "Create a new dataset version 2.0 for my training data located at
`<blob-storage-account-url>`

." - "Register a new evaluation dataset called
`product-reviews-v1`

from my blob storage."

**evaluation_dataset_get (read)**

Get a dataset by name and version, or list all datasets in the project.

Example prompts include:

- "Show me all datasets in my Foundry project"
- "Get details for the 'customer-support-qa' dataset version 2"
- "List all available datasets I can use for evaluation"

## Evaluation operations

**evaluation_create (write)**

Create an evaluation run for a dataset using one or more evaluators.

Example prompts include:

- "Create an evaluation run for my customer service dataset using Relevance, Groundedness, and Coherence evaluators."
- "Run an evaluation on dataset-456 with Violence, HateUnfairness, and ContentSafety evaluators for my chatbot model."
- "Evaluate my QA model using the F1Score, BleuScore, and RougeScore metrics on the test dataset."

**evaluation_get (read)**

List evaluation runs in the Azure AI Project.

Example prompts include:

- "Show me all evaluation runs in my Foundry project"
- "List the recent evaluations I've run this week"
- "Get the status of all my model evaluations"

**evaluation_comparison_create (write)**

Create comparison results of evaluations within a group.

Example prompts include:

- "Compare the performance of my baseline model against the two new fine-tuned versions."
- "Create a comparison between run-baseline-123 and treatment runs run-124, run-125 for evaluation eval-456."
- "I want to compare Model A vs Model B performance on the same evaluation metrics."

**evaluation_comparison_get (read)**

Get or list comparison results of evaluations within a group.

Example prompts include:

- "Get the results of comparison insight-789."
- "Show me the comparison results I created yesterday."
- "Retrieve all evaluation comparison insights from my project."

## Model catalog and details

**model_catalog_list (read)**

List models from the Foundry model catalog.

Example prompts include:

- "Show me all GPT-4 models available in the catalog."
- "List all Microsoft-published models with MIT license."
- "Find models I can use for free in the playground."
- "What models are available for text generation from OpenAI?"

**model_details_get (read)**

Get full model details and code sample from Foundry.

Example prompts include:

- "Get detailed information and code samples for GPT-5-mini."
- "Show me the specifications and usage examples for the Llama-2-70b model."
- "I need the documentation and sample code for the text-embedding-ada-002 model."

## Model deployment Management

**model_deploy (write)**

Create or update a model deployment in the specified Foundry account.

Example prompts include:

- "Deploy GPT-5-mini as 'production-chatbot' with 20 capacity units"
- "Create a new deployment called 'content-generator' using the GPT-4o model."
- "Deploy the latest version of text-davinci-003 for my application."

**model_deployment_get (read)**

Get one or more model deployments from a Foundry account.

Example prompts include:

- "Show me all my current model deployments."
- "Get details for my 'production-chatbot' deployment."
- "List all deployments in my Foundry account."

**model_deployment_delete (write)**

Delete a specific model deployment by name.

Example prompts include:

- "Delete the 'old-test-deployment' that I'm no longer using."
- "Remove my staging deployment to free up quota."
- "Clean up that deprecated model deployment from my Foundry account
`<account-name>`

."

## Model analytics and recommendations

**model_benchmark_get (read)**

Fetch benchmark data for Foundry models.

Example prompts include:

- "Show me benchmark data for all available models."
- "Get performance comparisons across different model families."
- "I want to see accuracy and cost metrics for various models."

**model_benchmark_subset_get (read)**

Get benchmark data for specific model name and version pairs.

Example prompts include:

- "Compare benchmark performance between GPT-4 and GPT-3.5-turbo."
- "Get benchmark data for Claude-3 vs Llama-2-70b models."
- "Show me performance metrics for the specific model versions I'm considering."

**model_similar_models_get (read)**

Returns a list of similar models based on deployment or model details.

Example prompts include:

- "Find models similar to my current GPT-4 deployment."
- "What alternatives are there to the model I'm currently using?"
- "Show me models with similar capabilities to my production deployment."

**model_switch_recommendations_get (read)**

Get model switch recommendations based on benchmark data.

Example prompts include:

- "Recommend better models based on my current deployment's performance."
- "Should I switch from my current model to something more cost-effective?"
- "Get optimization recommendations for my production model deployment."
- "What models would give me better quality/cost ratio than what I'm using now?"

## Model monitoring and operations

**model_monitoring_metrics_get (read)**

Get monitoring metrics for a model deployment.

Example prompts include:

- "Show me the request metrics for my production-chatbot deployment."
- "Get latency statistics for my GPT-4o deployment over the last week."
- "Check the quota usage for my text-embedding deployment."
- "What are the error rates for my content-generator model?"

**model_deprecation_info_get (read)**

Get deployment info enriched with deprecation data.

Example prompts include:

- "Check if my production deployment is using a deprecated model version."
- "Get deprecation information for my legacy-chatbot deployment."
- "Are any of my current deployments scheduled for retirement?"

**model_quota_list (read)**

List available deployment quota and usage for a subscription in a region.

Example prompts include:

- "Check my available quota in East US region."
- "How much capacity do I have left for new deployments in West Europe?"
- "Show me quota usage across all regions for my subscription."

## Example conversation examples

**Complete Model Evaluation Workflow:**

- "Upload my evaluation dataset from this blob storage URL."
- "Run an evaluation using Relevance, Groundedness, and Safety evaluators."
- "Compare my baseline model against the new fine-tuned version."
- "Show me the comparison results with statistical significance."

**Model Deployment & Optimization:**

- "Show me all GPT-4 models available in the catalog."
- "Deploy GPT-4o as 'customer-service-bot' with 15 capacity units."
- "Monitor the request latency for my new deployment."
- "Recommend more cost-effective alternatives based on current usage."

**Resource Management & Cleanup:**

- "List all my current deployments and their usage."
- "Check which deployments are using deprecated model versions."
- "Show me my quota usage across all regions."
- "Delete unused test deployments to free up capacity."

## Related content

- Get started with
[Foundry MCP Server](get-started?view=foundry) - Learn how to
[build your own MCP server](build-your-own-mcp-server?view=foundry) - Try the example workflows above in your own Microsoft Foundry project

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/mcp/security-best-practices -->

# Foundry MCP Server best practices and security guidance

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Foundry MCP Server (preview) tools to automate read and write operations across Foundry resources (deployments, datasets, evaluations, monitoring, analytics). This guidance helps you verify intent, reduce risk, and apply security and governance practices before you run MCP tools.

Note

This feature is currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Interpreting the response

MCP Server provides output that is passed to the language model selected for your agent (for example, Visual Studio Code with GitHub Copilot). The language model combines this output with the conversation context to generate a final response based on its capabilities. Always verify the accuracy of the language model’s response. It may include details that are inferred or generated beyond the MCP Server’s original output.

## Impact of write operations

Write operations have a critical impact on Foundry resources. Proceed with caution and proper planning when you interact with Foundry MCP Server (preview), just as you would when using the portal, SDKs, or REST APIs. For example:

- Deployments: Immediately affect live apps and billing.
- Deletions: Permanently remove resources and can break dependent services.
- Evaluations: Consume compute quota and incur costs.
- Datasets: Can overwrite existing versions.

Examples of resource impact:

- Deleting a deployment breaks all applications using that endpoint.
- Large evaluations can consume significant quota allocation.
- New deployments start billing immediately.
- Overwriting a dataset affects evaluation reproducibility.

## Best practices for safe executions

Follow these practices to make sure write operations run as you intend:

### Tool execution verification

**Verify tool selection**: Confirm the correct MCP tool and parameters match your intention before execution.**Check parameters**: Review all tool parameters (resource IDs, deployment names, dataset paths) for accuracy.- For example, many model and deployment related tools would take Foundry resource ID in the format of
`/subscriptions/{subscription_id}/resourceGroups/{resource_group_name}/providers/Microsoft.CognitiveServices/accounts/{account_name}`

- this Foundry resource ID has the information about the subscription, resource group name, and the Foundry account name. - Similarly, many agent and evaluation related tools would take Foundry project endpoint in the format of
`https://{account_name}.services.ai.azure.com/api/projects/{project_name}`

, which has the information about the Foundry account name and the project name. - If you provide project resource ID in the format of
`/subscriptions/{subscription_id}/resourceGroups/{resource_group_name}/providers/Microsoft.CognitiveServices/accounts/{account_name}/projects/{project_name}`

that you can find from either Properties page of the account on Azure portal or Microsoft Foundry project details page, the language model used in your MCP Host will extract needed info and formulate the parameters to pass to the MCP tools. Confirm before approval that intended parameter values are passed to the MCP tools.

- For example, many model and deployment related tools would take Foundry resource ID in the format of
**Check environment targeting**: Make sure resource endpoints and project URLs point to the intended environment.

### Resource management via MCP server

**Check dependencies**: Use monitoring tools to make sure no app depends on a resource before you delete it.**Check quota**: Query quota status before you create new deployments or run large evaluations.**Resource discovery**: List existing deployments and datasets before making changes.**Plan capacity**: Check available quota and usage metrics before resource-intensive operations.

### Safe MCP operation practices

**Test in nonproduction**: Use development project endpoints first.**Make incremental changes**: Change one resource at a time instead of making bulk updates.**Validate changes**: Use read-only tools to confirm changes take effect.**Handle errors**: Monitor responses for errors or unexpected results.

### Documentation and tracking

**Log operations**: Use Azure resource Activity Logs to track affected resources.**Back up configuration**: Export current deployment and dataset configurations before you modify them.**Track changes**: Record MCP operation details for troubleshooting and rollback.

## Security and governance

This section summarizes identity, access control, policy, network isolation, and data residency considerations to help you apply governance before MCP operations.

### Identity and access management

Authenticate to Foundry MCP Server (preview) using a Microsoft Entra token scoped to `https://mcp.ai.azure.com`

.

Azure role-based access control (RBAC) applies to all operations on Foundry resources supported by Foundry MCP Server (preview). Operations run according to the authenticated user's permissions.

### Allow tenant admin control via Azure Policy

Tenant admins can use Azure Policy to grant or block access to Foundry MCP Server (preview) for selected users or workload identities.

Materialize the service principal for Foundry MCP Server (preview) application ID by running

`az ad sp create --id fcdfa2de-b65b-4b54-9a1c-81c8a18282d9`

. The application ID used in this command represents Foundry MCP Server (preview).Find the enterprise application for Foundry MCP Server (preview) using the application ID. Open the

[Azure portal Entra ID page](https://portal.azure.com/#view/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/%7E/Overview)and search for the application ID`fcdfa2de-b65b-4b54-9a1c-81c8a18282d9`

.Click Conditional Access under Security on the left pane of the selected app for Foundry MCP Server (preview) and click New Policy to specify the users or workload identities.

Select

**Grant**, then choose**Block access**.

After the policy is in place, designated users and groups can't obtain the Entra token needed to connect.

### Network isolation

Foundry MCP Server (preview) currently doesn't support network isolation. It exposes the public endpoint `https://mcp.ai.azure.com`

that any MCP client can use. It connects to your Foundry resource through its public endpoint. If your Foundry resources use Azure Private Links, the server can't reach them and operations fail.

### Data Residency

Foundry MCP Server (preview) ("MCP Server") uses a global stateless proxy architecture. Data created by backend services that interact with MCP Server stays encrypted at rest in the region you select. MCP Server itself doesn't store data. For performance and availability, requests and responses can be processed in data centers in the European Union (EU) or the United States (US), with all data encrypted in transit.

Important

By using this preview feature, you are acknowledging and consenting to any cross-region processing that may occur. As an example, an EU resource accessed by a US user could be routed through US infrastructure. If your organization requires strict in-region processing, do not use the Foundry MCP Server (preview) or restrict its use to scenarios that remain within your selected region.

## Troubleshooting and FAQs

Use this section to quickly diagnose common MCP Server issues.

### Authentication failures

Check your permissions in Entra ID and confirm your access token is valid. Sign out, then sign back in to your Azure account in Visual Studio Code. For more information, see Manage users and authentication in Entra ID.

### Permission errors

Check your resource role assignments in the Azure portal to make sure you have the permissions for the operations you need. For more information, see [Role-based access control for Microsoft Foundry](../concepts/rbac-foundry?view=foundry).

### Server connectivity issues

Make sure your network allows outbound HTTPS connections to Azure services and no firewall rules block the MCP Server endpoint. See Azure connectivity troubleshooting for more help.

### Tool discovery problems

Make sure the MCP server is running and tools are loaded by checking the Output view in Visual Studio Code. Restart VS Code or reload your workspace to fix discovery issues.

## Related content

- Review
[available tools and example prompts](available-tools?view=foundry)for Foundry MCP Server - Get started with
[Foundry MCP Server](get-started?view=foundry) - Learn how to
[build your own MCP server](build-your-own-mcp-server?view=foundry)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/mcp/build-your-own-mcp-server -->

# Build and register a Model Context Protocol (MCP) server

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction) provides a standard interface for AI agents to interact with APIs and external services. When you need to integrate private or internal enterprise systems that don't have existing MCP server implementations, you can build your own custom server. This article shows you how to create a remote MCP server using Azure Functions, register it in a private organizational tool catalog using Azure API Center, and connect it to Foundry Agent Service.

This approach enables you to securely integrate internal APIs and services into the Microsoft Foundry ecosystem, allowing agents to call your enterprise-specific tools through a standardized MCP interface.

## Prerequisites

- A Foundry project with Agent Service enabled. For setup instructions, see
[Quickstart: Get started with Agent Service](../agents/quickstart?view=foundry). - An Azure subscription and permissions to create resources. At minimum, you typically need the Contributor role on the target resource group.
[Python](https://www.python.org/downloads/)version 3.11 or higher installed on your local development machine.[Azure Functions Core Tools](/en-us/azure/azure-functions/functions-run-local?pivots=programming-language-python#install-the-azure-functions-core-tools)version 4.0.7030 or higher.[Azure Developer CLI](https://aka.ms/azd)installed for deployment automation.- For local development and debugging:
[Visual Studio Code](https://code.visualstudio.com/)[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code

- An
[Azure API Center resource](/en-us/azure/api-center/overview)(optional, required only for organizational tool catalog registration).

Note

Agent Service connects only to publicly accessible MCP server endpoints.

## Understand the request flow

The high-level flow looks like this:

- You deploy an MCP server (this article uses Azure Functions) that exposes one or more MCP tools.
- You optionally register the server in Azure API Center so it shows up in an organizational tool catalog.
- In Foundry portal, you connect the MCP server to Agent Service.
- When an agent needs a tool, Agent Service calls your MCP server endpoint.
- Your MCP server validates the request, calls your internal API, and returns the tool result.

## Build an MCP server by using Azure Functions

Azure Functions is a serverless compute service that provides scale-to-zero capability, burst scaling, and enterprise features including identity-based access and virtual networking. The lightweight programming model makes it straightforward to build MCP servers so you can focus on implementing your business logic rather than infrastructure management.

Open a terminal or command prompt and navigate to the folder where you want to create your project.

Run the

`azd init`

command to initialize the project from[this sample MCP server template](https://github.com/Azure-Samples/remote-mcp-functions-python):`azd init --template remote-mcp-functions-python -e mcpserver-python`

Review the sample code structure. The template includes:

- Function definitions for MCP endpoints.
- Configuration for authentication and authorization.
- Deployment scripts for Azure.

Customize the MCP server functions to expose your specific APIs and services. Modify the function code to implement the tools and capabilities your agents need.

Test your MCP server locally by using the Azure Functions Core Tools:

`func start`

Deploy your MCP server to Azure by using the Azure Developer CLI:

`azd up`

Follow the prompts to select your Azure subscription and resource group.

After deployment completes, save the following information for later steps:

- Remote MCP server endpoint:
`https://{function_app_name}.azurewebsites.net/runtime/webhooks/mcp`

- Authentication information: For access key authentication, note the
`mcp_extension`

system key in the Azure portal.

If you prefer a CLI workflow to retrieve function access keys, see

[Work with access keys in Azure Functions](/en-us/azure/azure-functions/function-keys-how-to?tabs=azure-cli#get-your-function-access-keys).- Remote MCP server endpoint:

For detailed implementation guidance, see [Quickstart: Build a custom remote MCP server using Azure Functions](/en-us/azure/azure-functions/scenario-custom-remote-mcp-server?pivots=programming-language-python).

## Secure your MCP server endpoint

Before you share your MCP server with others, define and apply a security baseline:

- Require authentication. Avoid anonymous access unless your scenario explicitly needs it.
- Treat credentials as secrets. Don't hard-code keys in code or check them into source control. Store secrets in a secure store such as
[Azure Key Vault](/en-us/azure/key-vault/general/overview). - Implement least privilege for downstream calls. If your MCP server calls internal APIs, scope permissions to only what the exposed tools need.
- Log and monitor tool calls. Use Azure Functions logging to trace requests and troubleshoot failures.

For Agent Service authentication patterns (for example, key-based authentication, Microsoft Entra identities, and OAuth identity passthrough), see [MCP server authentication](../agents/how-to/mcp-authentication?view=foundry).

For governance and operational guidance when you run MCP tools, see [Foundry MCP Server best practices and security guidance](security-best-practices?view=foundry).

## Register your MCP server in the organizational tool catalog

When you register your MCP server in Azure API Center, you create a private organizational tool catalog. This step is optional but recommended for sharing MCP servers across your organization with consistent governance and discoverability.

To register your MCP server:

Sign in to the

[Azure portal](https://portal.azure.com)and go to your Azure API Center resource.Tip

The API Center name becomes your private tool catalog name in the registry filter. Choose an informative name that helps users identify your organization's tool catalog.

Register your remote MCP server by adding it as an API:

a. In the left navigation pane, select

**APIs**.b. Select

**+ Add API**and provide the required information about your MCP server.c. Configure environments and deployments following the tutorial:

[Add environments and deployments for APIs in Azure API Center](/en-us/azure/api-center/configure-environments-deployments).Configure authentication for your MCP server (optional):

a. In the left navigation pane of your API Center resource, select

**Governance**>**Authorization**.b. Select

**Add configuration**.c. Choose the security scheme that matches your MCP server requirements:

**API Key**: Developers provide the API key during tool configuration in Foundry**OAuth**: Configure OAuth 2.0 authentication parameters**HTTP**: Configure bearer token authorization

d. Provide the required authentication details for your selected scheme.

Note

If you choose API Key authentication, the key you store in Azure Key Vault isn't automatically used in Foundry. Developers must provide the API key when configuring the MCP server connection.

Configure access management (optional):

a. Go to your registered MCP server in API Center.

b. Select

**Details**>**Versions**>**Manage Access (preview)**.c. Configure which users or groups can access this MCP server through the organizational catalog.


After registration, your MCP server appears in the Foundry tool catalog with the governance and authentication settings you configured.

## Connect the MCP server to Agent Service

You can connect your MCP server to Agent Service through the organizational tool catalog (if you registered it) or as a custom MCP tool.

### Connect using the organizational tool catalog

If you registered your MCP server in Azure API Center, users with appropriate access can discover and configure it:

In

[Foundry portal](https://ai.azure.com), go to your project.Go to

**Build**>**Tools**or open Agent Builder.Browse the organizational tool catalog to find your registered MCP server.

Follow the configuration guidance displayed in the tool catalog to add the server to your agent.


### Connect using a custom MCP tool

If you don't register your MCP server in the organizational catalog, add it directly as a custom tool:

In

[Foundry portal](https://ai.azure.com), go to your project.Go to

**Build**>**Tools**or open Agent Builder.Select

**Add tool**>**Custom**>**Model Context Protocol**.Enter your MCP server details:

**Name**: Unique name for your remote MCP server**Remote MCP Server endpoint**: Enter your remote MCP server endpoint URL (for example,`https://{function_app_name}.azurewebsites.net/runtime/webhooks/mcp`

)**Authentication**: Select the authentication method. For**Key-based**authentication, provide the following credential:**Credential**:`"x-functions-key": "{mcp_extension_system_key}"`


Select

**Connect**to register the custom MCP tool.

For detailed configuration steps (including project connections and approval workflows), see [Connect to Model Context Protocol servers (preview)](../agents/how-to/tools/model-context-protocol?view=foundry).

After connecting your MCP server, agents in your Foundry project can call the tools and functions exposed by your custom server.

## Verify the MCP server works end to end

After you deploy and connect the server, verify that the server is discoverable and that an agent can successfully invoke a tool.

In Foundry portal, confirm the MCP server appears in your project tool list.

Create an agent (or open an existing agent) and add the MCP server tool.

Run a prompt that should require one of your MCP tools.

If approval is enabled, review the tool name and arguments, then approve the call.

Confirm the tool call succeeds.

If the tool call fails, open the Function App logs in Azure portal to confirm the MCP endpoint was invoked and to diagnose errors.


## Troubleshooting

Here are some common issues you might encounter when building and connecting your MCP server:

**MCP server connection fails**: Confirm the server URL is publicly reachable and uses the MCP webhook path (`/runtime/webhooks/mcp`

). Check the Function App logs in Azure portal for errors.**Authentication errors (401/403)**: Verify you're using the correct key or token for the authentication method you selected. Rotate keys that might have been exposed, and update any saved credentials.**Tool discovery problems**: If you registered the server in Azure API Center, confirm the API is published and you have access to it. If you added a custom tool, confirm the endpoint URL is correct.**Tool call succeeds but an internal API fails**: Review your MCP server logs to confirm what request was sent to the downstream API. Verify the MCP server identity or API credentials have the required permissions.

## Clean up resources

When you're done, delete Azure resources created by the template to avoid ongoing charges.

In your MCP server project folder, run:

`azd down --purge`

If you registered the server in Azure API Center, remove the API entry if you no longer need it.


## Related content

[Get started with Agent Service](../agents/quickstart?view=foundry)[Connect to Model Context Protocol servers (preview)](../agents/how-to/tools/model-context-protocol?view=foundry)[MCP server authentication](../agents/how-to/mcp-authentication?view=foundry)[Get started with Foundry MCP Server (preview) using Visual Studio Code](get-started?view=foundry)[Foundry MCP Server best practices and security guidance](security-best-practices?view=foundry)[Explore available tools and example prompts for Foundry MCP Server (preview)](available-tools?view=foundry)[Add environments and deployments in Azure API Center](/en-us/azure/api-center/configure-environments-deployments)[Azure Functions Python developer guide](/en-us/azure/azure-functions/functions-reference-python)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/speech-service/speech-to-text/data-privacy-security -->

# Data and Privacy for Speech to text

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

Note

This article is provided for informational purposes only and not for the purpose of providing legal advice. We strongly recommend seeking specialist legal advice when implementing Speech Services.

This article provides some high-level details regarding how speech to text processes data provided by customers. Note that audio data of humans speaking and the related text transcripts may be considered personal data and/or sensitive data under various privacy regulations and laws because it contains not only the voice of humans, but the content of the audio may also contain personal information depending on the context within which the audio was collected. Audio data and the related text transcripts may also be regulated under various communications laws or other law and regulations. As an important reminder, you are responsible for the implementation of this technology and are required to obtain all necessary permissions for processing of the data, as well as any licenses, permissions or other proprietary rights required for the content you input into the speech to text service. It is your responsibility to comply with all applicable laws and regulations in your jurisdiction.

## What data does speech to text process?

Speech to text processes the following types of data:

**Audio input or voice audio:**All speech to text features accept voice audio as an input that is streamed through the Speech SDK/REST API into the service endpoint. In batch transcription, audio input will be sent to a storage location instructed by the customer, and the Speech service accesses and processes the audio input for the purposes of providing the transcription services requested. See more information about how to specify storage in[How to use batch transcription](/en-us/azure/cognitive-services/speech-service/batch-transcription).**Input transcription text:**In the pronunciation assessment, transcribed text is sent together with an input voice audio as "correct" text. Pronunciations are assessed based on the input transcriptions.**Transcription for speech translation:**When the speech translation feature is used, transcribed text that speech to text generated is translated into a specified language through the[Translator service](/en-us/azure/cognitive-services/translator/translator-info-overview).

The text translation service is used only to convert text from one language to another. No input/output data is retained by Speech service after the completion of a translation request. See [What is the Translator service](/en-us/azure/cognitive-services/translator/translator-info-overview) for more information about the text translation service.

If users need transcribed/translated text in an audio format, the feature sends the output text to [text to speech](/en-us/azure/cognitive-services/speech-service/text-to-speech). Again, no data is persisted in the text to speech data processing.

## How does speech to text process data?

### Real-time speech to text

When a client application sends audio input to speech to text, the speech recognition engine parses audio and converts it to text. Relying upon its acoustic and linguistic or language understanding features, speech to text selects candidate words and phrases that may be uttered in the audio input. The transcription output represents the best inference or prediction in text format of what was spoken in the audio input.

For real-time speech to text, audio input is processed only on the Azure's server memory, and no data is stored at rest. All data in-transit are encrypted for protection. See [Trusted Cloud: security, privacy, compliance, resiliency, and IP](https://azure.microsoft.com/blog/trusted-cloud-security-privacy-compliance-resiliency-and-ip/) for more information about Azure-wide security and privacy protection.

### Batch transcription

In batch transcription, customers specify their chosen storage location of both audio input and output transcription text files for Speech service to access, process, and provide the transcription output. The customer controls the storage of this data, including the retention of such data. Customers may set a retention time for generated transcription text files by using a parameter called "timeToLive". See [Batch Transcription -- Configuration Properties](/en-us/azure/cognitive-services/speech-service/batch-transcription#configuration-properties) for more detail.

See the data flows for each Speech to text feature:

### Speaker diarization/separation

This feature is available for both real-time and batch API. When customers enable the speaker separation (diarization) option (disabled by default), the speech to text engine analyzes and extracts unique voice characteristics signals from the audio input to differentiate the audio between speakers. These voice characteristics signals are used and temporarily retained for the sole purpose of annotating the transcription output with markers next to text for Speaker 1 (Guest-1) or Speaker 2 (Guest-2). Upon completion of the process, all signal data used to separate the speakers is discarded. The speaker separation feature supports the separation of two or more speakers in a single audio file. Speaker Separation does not support speaker identity recognition enrollment or the ability to track unique speakers across multiple audio files.

### Language detection

Language detection is similar to speech recognition except that the model calculates probabilities of mapping between phonemes and languages. Each language has specific phonemes and phoneme combinations, which characterize the language. The language detection model identifies the characteristics in phonemes to calculate likelihood of languages used in an input voice.

### Speech translation

When speech translation is used, first, an audio input is used to generate machine-transcribed text with speech to text. Then the machine-transcribed text is sent to the text translation service to convert the text (in the source language) to another language. If customers need translated text in an audio format, this feature can send the translated text to [text to speech](/en-us/azure/cognitive-services/speech-service/text-to-speech). Customers have the option to produce translated text only or translated voice output.

### Speech containers

With speech containers, customers deploy Speech services APIs to their own environment through Docker containers. Since all speech components run on customers' controlled environment, audio data inputs and transcription outputs are processed within customers' container and is not sent to the cloud based Speech service. See [Install and run Docker containers for the Speech service APIs](/en-us/azure/cognitive-services/speech-service/speech-container-howto?tabs=stt%2Ccsharp%2Csimple-format) for more information.

### Security for customers' data in speech container

The security of customer data is a shared responsibility. Details on the security model of Azure AI containers, like the speech container can be found in [Foundry Tools container security](/en-us/azure/cognitive-services/cognitive-services-container-support?tabs=luis#azure-cognitive-services-container-security).

You are responsible for securing and maintaining the equipment and infrastructure required to operate speech containers located on your premises, such as your edge device and network.

To learn more about Microsoft's privacy and security commitments visit [the Microsoft Trust Center](https://www.microsoft.com/TrustCenter/CloudServices/Azure/default.aspx).

## Data storage and retention

### No data trace

When doing real-time speech to text, fast transcription, pronunciation assessment, and speech translation, Microsoft does not retain or store the data provided by customers. In batch transcription, customers specify their own storage locations to send the audio input. Generated transcription text may be stored either in customer's own storage or Microsoft storage if no storage is specified. If output transcriptions are stored in Microsoft storage, customers may delete the data either by calling a deletion API or setting the timeToLive parameter to automatically delete the data in a specified time. See more details in [How to use batch transcription - Speech service - Foundry Tools](/en-us/azure/cognitive-services/speech-service/batch-transcription).

To learn more about Microsoft's privacy and security commitments visit the Microsoft [Trust Center](https://www.microsoft.com/TrustCenter/CloudServices/Azure/default.aspx).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/speech-service/speech-to-text/transparency-note -->

# Use cases for Speech to text

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

## What is a Transparency Note?

An AI system includes not only the technology, but also the people who will use it, the people who will be affected by it, and the environment in which it is deployed. Creating a system that is fit for its intended purpose requires an understanding of how the technology works, what its capabilities and limitations are, and how to achieve the best performance. Microsoft's Transparency Notes are intended to help you understand how our AI technology works, the choices system owners can make that influence system performance and behavior, and the importance of thinking about the whole system, including the technology, the people, and the environment. You can use Transparency Notes when developing or deploying your own system, or share them with the people who will use or be affected by your system.

Microsoft's Transparency Notes are part of a broader effort at Microsoft to put our AI Principles into practice. To find out more, see the [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai).

## The basics of speech to text

Speech to text, also known as automatic speech recognition (ASR), is a feature under the Azure Speech in Foundry Tools service, which is a part of Foundry Tools. [Speech to text](/en-us/azure/cognitive-services/speech-service/Speech-to-Text) converts spoken audio into text. Speech to text in Azure supports more than 140 locales for input. For the latest list of supported locales, see [Language and voice support for the Speech service](/en-us/azure/ai-services/speech-service/language-support).

### Key terms

Term |
Definition |
|---|---|
| Audio input | The streamed audio data or audio file that's used as an input for the speech to text feature. Audio input can contain not only voice, but also silence and non-speech noise. Speech to text generates text for the voice parts of audio input. |
| Utterance | A component of audio input that contains human voice. One utterance can consist of a single word or multiple words, such as a phrase. |
| Transcription | The text output of the speech to text feature. This automatically generated text output leverages speech models and is sometimes called machine transcription or automated speech recognition (ASR). Transcription in this context is fully automated and therefore different from human transcription, which is text that is generated by human transcribers. |
| Speech model | An automatically generated, machine-learned numerical representation of an utterance that is used to infer a transcription from an audio input. Speech models are trained on voice data that includes various speech styles, languages, accents, dialects, and intonations, and on acoustic variations that are generated by using different types of recording devices. A speech model numerically represents both acoustic and linguistic features, which are used to predict what text should be associated with the utterance. |
| Real-time API | An API that accepts requests with audio input, and returns a response in real time with transcription within the same network connection. |
| Language Detection API | A type of real-time API that detects what language is spoken in an audio input. A language is inferred based on voice sound in the audio input. |
| Speech Translation API | Another type of real-time API that generates transcriptions of a given audio input then translates them into a language specified by the user. This is a cascaded service of Speech Services and Text Translator. |
| Batch API | A service that is used to send audio input to be transcribed at a later time. You specify the location of audio files and other parameters, such as the language of recognition. The service loads the audio input asynchronously and transcribes it. When transcription is complete, text files are loaded back to a location that you specify. |
| Diarization | Diarization answers the question of who spoke and when. It differentiates speakers in an audio input based on their voice characteristics. Both real-time and batch APIs support diarization and are capable of differentiating speakers' voices on monochannel recordings. Diarization is combined with speech to text functionality to provide transcription outputs that contain a speaker entry for each transcribed segment. The transcription output is tagged as GUEST1, GUEST2, GUEST3, etc. based on the number of speakers in the audio conversation. |
| Word error rate(WER) |
|

## Capabilities

### System behavior

Below we are listing the main ways to call our speech to text service.

[Real-time Speech to text API](/en-us/azure/ai-services/speech-service/speech-to-text)

This is a common API call via the Speech SDK or REST API to send an audio input and receive a text transcription in real time. The speech system uses a speech model to recognize what is spoken in an input audio. During real-time speech to text, the system takes an audio stream as input and continuously determines the most likely sequence of words that produced the audio that's observed so far. The model is trained on a large amount of diverse audio across typical usage scenarios and a wide range of speakers. For example, this feature is often used for voice-enabled queries or dictation within an organization's service or application.

[Batch transcription API](/en-us/azure/ai-services/speech-service/batch-transcription)

Batch transcription is another type of API call. It’s typically used to send prerecorded audio inputs and to receive transcribed text asynchronously (that is, at a later time). To use this API, you can specify locations for multiple audio files. The speech to text technology reads the audio input from the file and generates transcription text files that are returned to the storage location that you specify. This feature is used to support larger transcription jobs in which it is not necessary to provide end users with the transcription content in real time. An example is transcribing call center recordings to gain insights into customers and call center agent performance.

When you use batch transcription, you can choose to use the Whisper model instead of the default Azure Speech to text model. To determine whether the Whisper model is appropriate for your use case, you can compare how the output between these models differs in the batch. Try it out in [Speech Studio](https://speech.microsoft.com/), and then perform deeper evaluations by using the test capabilities through custom speech. Note that the Whisper model is also available thorough Azure OpenAI.

#### Speech translation API

This API converts audio input to text, and then translates it into another language. The translated transcription output can be returned in text format, or you can choose to have the text synthesized into audible speech by using [text to speech](/en-us/azure/cognitive-services/speech-service/text-to-speech). For more information, see [What is Azure Translator in Foundry Tools?](/en-us/azure/ai-services/translator/translator-overview)

#### Sub-features and options

The APIs above can optionally use the following sub-features:

: Azure Speech enables developers to customize the speech to text models in order to improve the recognition accuracy for a specific scenario. There are two ways to customize speech to text:[Model customization](/en-us/azure/ai-services/speech-service/custom-speech-overview)- At runtime through the use of the
[phrase list](/en-us/azure/ai-services/speech-service/improve-accuracy-phrase-list?tabs=terminal&pivots=programming-language-csharp)feature - Ahead of time through the use of
[custom speech](/en-us/azure/ai-services/speech-service/custom-speech-overview)

- At runtime through the use of the
: Unlike in a default API call, in which a language or locale for an audio input must be specified in advance, with language detection, you can specify multiple locales and let the service detect which language should be used to recognize a specific part of the audio.[Language detection](/en-us/azure/cognitive-services/speech-service/how-to-automatic-language-detection?pivots=programming-language-csharp)**Diarization**: This feature is disabled by default. If you choose to enable this feature, the service differentiates different speakers' utterances. The resulting transcription text contains a "speaker" property that indicates GUEST1, GUEST2, GUEST3, and so on, which denotes which speaker is speaking in an audio file.

### Use cases

Speech to text can offer different ways for users to interact with applications and devices. Instead of typing words on a keyboard or using their hands for touchscreen interactions, speech to text technology allows users to operate applications and devices by voice and through dictation.

**Smart assistants**: Companies that are developing smart assistants on appliances, cars, and homes can use speech to text to enable natural interface search queries or to trigger certain features by voice. This is called _command-and-_*control*.**Chat bots**: Companies can build chat bot applications, in which users can use voice-enabled queries or commands to interact with bots.**Voice typing**: Apps can allow users to use voice to dictate long-form text. Voice typing can be used to enter text for messaging, emails, and documents.**Voice commanding**: Users can trigger certain actions by voice (command-and-control). Two common examples are entering query text by voice and selecting a menu item by voice.**Voice translation**: You can use the speech translation features of speech to text technology to communicate by voice with other users who speak different languages. Speech translation enables voice-to-voice communication across multiple languages. See the latest list of supported locales in[Language and voice support for the Speech service](/en-us/azure/cognitive-services/speech-service/language-support).**Call center transcriptions**: Companies often record conversations with their users in scenarios like customer support calls. Audio recordings can be sent to the batch API for transcription.**Mixed-language dictation**: Users can use speech to text technology to dictate in multiple languages. Using language detection, a dictation application can automatically detect spoken languages and transcribe appropriately without requiring a user to specify which language they speak.**Live conversation transcription**: When speakers are all in the same room using a single-microphone setup, do live transcription about which speaker (Guest1, Guest2, Guest3, and so on) makes each statement.**Conversation transcription of prerecorded audio**: After the recording of audio with multiple speakers you can use our service to get the transcription about which speaker (Guest1, Guest2, Guest3, and so on) makes each statement.

### Considerations when choosing other use cases

The speech to text API offers convenient options for developing voice-enabled applications, but it is very important to consider the context in which you will integrate the API. You must ensure that you comply with all laws and regulations that apply to your application. This includes understanding your obligations under privacy and communication laws, including national and regional privacy, eavesdropping, and wiretap laws that apply to your jurisdiction. Collect and process only audio that is within the reasonable expectations of your users. This includes ensuring that you have all necessary and appropriate consents from users for you to collect, process, and store their audio data.

Many applications are designed and intended to be used by a specific individual user for voice-enabled queries, commands, or dictation. However, the microphone for your application might pick up sound or voice from non-primary users. To avoid unintentionally capturing the voices of non-primary users, you should consider the following information:

**Microphone considerations**: Often, you cannot control who might speak near the input device that sends audio input to the speech to text cloud service. You should encourage your users to take extra care when they use voice-enabled features and applications in a public or open environment where other people's voices might be easily captured.**Use speech to text only in experiences and features that are within the reasonable expectations of your users**: Audio data that contains a person speaking is personal information. Speech to text is not intended to be used for covert audio surveillance purposes, in a manner that violates legal requirements, or in applications and devices in public spaces or locations where users might have a reasonable expectation of privacy. Use the Speech service only to collect and process audio in ways that are within the reasonable expectations of your users. This includes ensuring that you have all necessary and appropriate consents from users to collect, process, and store their audio data.**Azure Speech service and integration of the Whisper model**: The Whisper model enhances the Azure Speech service with advanced features like multilingual recognition and readability. The Speech service also enriches the performance of the Whisper model by enabling larger-scale batch transcriptions and speaker diarization. Whether to use the default Speech service speech to text model or Whisper model depends on the specific use case. We recommend that you take advantage of the batch try out and custom speech experiences in Speech Studio to evaluate both options to find the best fit for your business needs.**Conversation transcription on prerecorded events**: The system will perform better if all speakers are in the same acoustic environment (for example, the conversation takes place in a room in which people speak into a common microphone).**Conversation transcription**: Although there is no limitation on the numbers of speakers in the conversation, the system performs better when the number of speakers is under 30.**Legal and regulatory considerations**: Organizations need to evaluate potential specific legal and regulatory obligations when using any Foundry Tools and solutions, which may not be appropriate for use in every industry or scenario. Additionally, Foundry Tools or solutions are not designed for and may not be used in ways prohibited in applicable terms of service and relevant codes of conduct.

### Unsupported uses

**Conversation transcription with speaker recognition**: The Speech service is not designed to provide diarization with speaker recognition, and it cannot be used to identify individuals. In other words, speakers will be presented as Guest1, Guest2, Guest3, and so on, in the transcription. These will be randomly assigned and may not be used to identify individual speakers in the conversation. For each conversation transcription, the assignment of Guest1, Guest2, Guest3, and so on, will be random.

To prevent any potential for misuse of Speech service for identification purposes, you are responsible for ensuring that you use the service, including the diarization feature, only for supported uses, and that you have a proper legal basis and any required consents in place for all uses of the service.

## Limitations

Speech to text recognizes what's spoken in an audio input, and then generates transcription outputs. This requires proper setup for the expected languages used in the audio input and spoken styles. Non-optimal settings might lead to lower accuracy.

### Technical limitations, operational factors, and ranges

#### Language of accuracy

The industry standard to measure speech to text accuracy is [word error rate (WER)](https://en.wikipedia.org/wiki/Word_error_rate). To understand the detailed WER calculation, see [Test the accuracy of a custom speech model](/en-us/azure/cognitive-services/speech-service/how-to-custom-speech-evaluate-data).

#### Transcription accuracy and system limitations

Speech to text uses a unified speech recognition machine learning model to transcribe what is spoken in a wide range of contexts and topic domains, including command-and-control, dictation, and conversations. You don't need to consider using different models for your application or feature scenarios.

However, you need to specify a language or locale for each audio input. The language or locale must match the actual language that's spoken in an input voice. For more information, see the list of [supported locales](/en-us/azure/cognitive-services/speech-service/language-support).

Many factors can lead to a lower accuracy in transcription:

**Acoustic quality:**Speech to text–enabled applications and devices might use a wide variety of microphone types and specifications. Unified speech models have been created based on various voice audio device scenarios, such as telephones, mobile phones, and speaker devices. However, voice quality might be degraded by the way a user speaks into a microphone, even if they use a high-quality microphone. For example, if a speaker is located far from the microphone, the input quality would be too low. A speaker who is too close to the microphone could also cause audio quality deterioration. Both cases can adversely affect the accuracy of speech to text.**Non-speech noise:**If an input audio contains a certain level of noise, accuracy is affected. Noise might come from the audio devices that are used to make a recording, or audio input itself might contain noise, such as background or environmental noise.**Overlapped speech:**There might be multiple speakers within range of an audio input device, and they might speak at the same time. Also, other speakers might speak in the background while the main user is speaking.**Vocabularies:**The speech to text model has been trained on a wide variety of words in many domains. However, users might speak organization-specific terms and jargon that aren't in a standard vocabulary. If a word that doesn't exist in a model appears in the audio, the result is an error in transcription.**Accents:**Even within one locale, such as in English - United States (en-US), many people have different accents. Very specific accents might also lead to an error in transcription.**Mismatched locales:**Users might not speak the languages that you expect. If you specified English - United States (en-US) for an audio input, but a speaker spoke in Swedish, for example, accuracy would be reduced.**Insertion errors**: At times, the speech to text models can produce insertion errors in the presence of noise or soft background speech. This is limited when you use the Speech service, but it’s slightly more frequent when you use the Whisper model, as stated in the OpenAI[model card](https://github.com/openai/whisper/blob/main/model-card.md#performance-and-limitations).

Because of these acoustic and linguistic variations, you should expect a certain level of inaccuracy in the output text when you design an application.

## System performance

System performance is measured by these key factors (from the user's point of view):

- Word error rate (WER)
- Token error rate (TER)
- Runtime latency

A model is considered better only when it shows significant improvements (such as a 5% relative WER improvement) in all scenarios (like transcription of conversation speech, call center transcription, dictation, and voice assistant) while being in line with the resource usage and response latency goals.

For diarization, we measure the quality by using word diarization error rate (WDER). The lower the WDER, the better the quality of diarization.

### Best practices for improving system performance

As described earlier, acoustic conditions like background noise, side speech, distance to microphone, and speaking styles and characteristics can adversely affect the accuracy of what is recognized.

For better speech experiences, consider the following application or service design principles:

**Design UIs to match input locales:**Mismatched locales reduce accuracy. The Speech SDK supports[automatic language detection](/en-us/azure/cognitive-services/speech-service/how-to-automatic-language-detection?pivots=programming-language-csharp), but it detects only one out of four locales that are specified at runtime. You still need to know the locale that your users will speak in. Your UI should clearly indicate which languages the users can speak in via a dropdown that lists the languages that are supported. For more information, see the[supported locales](/en-us/azure/cognitive-services/speech-service/language-support).**Allow users to try again:**Misrecognition might occur due to a temporary issue, such as unclear or fast speech or a long pause. If your application expects specific transcriptions, such as predefined action commands like "Yes" and "No" and it did not get any of them, users should be able to try again. A typical method is to tell users, "Sorry, I didn't get that. Please try again."**Confirm before you take an action by voice:**Just as with keyboard-based, click-based, or tap-based UIs, if an audio input can trigger an action, users should be given an opportunity to confirm the action, especially by displaying or playing back what was recognized or transcribed. A typical example is sending a text message by voice. An app repeats what was recognized and asks for confirmation: "You said, 'Thank you.' Send it or change it?"**Add custom vocabularies:**The general speech recognition model that's provided by speech to text covers a broad vocabulary. However, scenario-specific jargon and named entities (for example, people names and product names) might be underrepresented. What words and phrases are likely to be spoken can vary significantly depending on the scenario. If you can anticipate which words and phrases will be spoken (for instance, when a user selects an item from a list), you might want to use the phrasal list grammar. For more information, see "Improving recognition accuracy" in[Get started with speech to text](/en-us/azure/cognitive-services/speech-service/get-started-speech-to-text?tabs=script%2Cbrowser%2Cwindowsinstall&pivots=programming-language-csharp).**Use custom speech:**If speech to text accuracy in your application scenarios remains low, you might want to consider customizing the model for your acoustic and linguistic variations. You can create your own models by training them by using your own voice audio data or text data. For details, see[custom speech](/en-us/azure/cognitive-services/speech-service/custom-speech-overview).

## Evaluation of speech to text

A speech to text model is evaluated through testing. The goal of testing is to confirm that the model performs well across each of the key scenarios and in prevalent audio conditions, and that we are achieving our fairness goals across demographic factors.

### Evaluation methods

For model evaluation, test datasets are used. Both a regression test and a model performance test are run before each model deployment. Key metrics for regression tests are WER, TER, WDER (if diarization is enabled when doing speech to text), and latency at the 90th percentile.

### Evaluation results

We strive to ship all model updates regression-free (that is, the updated model should only improve the current production model). Each candidate is compared directly to the current production model. To consider a model for deployment, we must see at least a 5% relative WER improvement over the current production model.

Speech to text models are trained and tuned by using voice audio that has variations, including:

- Microphones and device specifications
- Speech environment
- Speech scenarios
- Languages and accents of speakers
- Age and gender of speakers
- Ethnic background of speakers

For diarization, additional data variations are used:

- Length of time each speaker speaks
- Number of speakers
- Emotional speech that alters pitch and tone

The resulting speech to text system transcribes the user's spoken words into text, which then can be used by a dialog system with natural language understanding or for analytics like summarization or sentiment.

### Fairness considerations

At Microsoft, we strive to empower every person on the planet to achieve more. An essential part of this goal is working to create technologies and products that are fair and inclusive. Fairness is a multidimensional, sociotechnical topic, and it affects many different aspects of our product development. Learn more about [the Microsoft approach to fairness](https://www.microsoft.com/ai/responsible-ai?activetab=pivot1%3Aprimaryr6).

One dimension we need to consider is how well the system performs for different groups of people. Research has shown that without conscious effort focused on improving performance for all groups, it is often possible for the performance of an AI system to vary across groups based on factors such as race, ethnicity, region, gender, and age.

Each version of the speech to text model is tested and evaluated against various test sets to make sure that the model can perform without a large gap in each of the evaluation criteria. More granular fairness results are coming soon.

## Evaluating and integrating speech to text for your use

The performance of speech to text will vary depending on the real-world uses and conditions that you implement. To ensure optimal performance in your scenario, you should conduct your own evaluations of the solutions you implement by using speech to text.

A test voice dataset should consist of actual voice inputs that were collected in your applications in production. You should randomly sample data to reflect real user variations over a certain period of time. Also, the test dataset should be refreshed periodically to reflect changes in the variations.

## Guidance for integration and responsible use with speech to text

As Microsoft works to help customers responsibly develop and deploy solutions by using speech to text, we are taking a principled approach to upholding personal agency and dignity by considering the AI systems' fairness, reliability & safety, privacy & security, inclusiveness, transparency, and human accountability. These considerations reflect our commitment to developing Responsible AI.

When getting ready to deploy AI-powered products or features, the following activities help to set you up for success:

**Understand what it can do**: Fully assess the capabilities of speech to text to understand its capabilities and limitations. Understand how it will perform in your particular scenario and context by thoroughly testing it with real life conditions and data.**Respect an individual's right to privacy**: Only collect data and information from individuals for lawful and justifiable purposes. Only use data and information that you have consent to use for this purpose.**Legal review**: Obtain appropriate legal advice to review your solution, particularly if you will use it in sensitive or high-risk applications. Understand what restrictions you might need to work within and your responsibility to resolve any issues that might come up in the future. Do not provide any legal advice or guidance.**Human-in-the-loop**: Keep a human-in-the-loop and include human oversight as a consistent pattern area to explore. This means ensuring constant human oversight of the AI-powered product or feature and maintaining the role of humans in decision making. Ensure that you can have real-time human intervention in the solution to prevent harm. This enables you to manage situations when the AI model does not perform as required.**Security**: Ensure that your solution is secure and has adequate controls to preserve the integrity of your content and prevent unauthorized access.**Build trust with affected stakeholders**: Communicate the expected benefits and potential risks to affected stakeholders. Help people understand why the data is needed and how the use of the data will lead to their benefit. Describe data handling in an understandable way.**Customer feedback loop**: Provide a feedback channel that allows users and individuals to report issues with the service once it's been deployed. After you've deployed an AI-powered product or feature, it requires ongoing monitoring and improvement. Be ready to implement any feedback and suggestions for improvement. Establish channels to collect questions and concerns from affected stakeholders (people who might be directly or indirectly affected by the system, including employees, visitors, and the general public).**Feedback**: Seek out feedback from a diverse sampling of the community during the development and evaluation process (for example, from historically marginalized groups, people with disabilities, and service workers). See:[Community jury](/en-us/azure/architecture/guide/responsible-innovation/community-jury/).**User study**: Any consent or disclosure recommendations should be framed in a user study. Evaluate the first and continuous-use experience with a representative sample of the community to validate that the design choices lead to effective disclosure. Conduct user research with 10-20 community members (affected stakeholders) to evaluate their comprehension of the information and to determine if their expectations are met.

## Recommendations for preserving privacy

A successful privacy approach empowers individuals with information and provides controls and protection to preserve their privacy.

**Consent to process and store audio input**: Be sure to have all necessary permissions from your end users before you use the speech to text-enabled features in your applications or devices. Also ensure that you have permission for Microsoft to process this data as your third-party cloud service processor. Note that the real-time API does not separately store any of the audio input and transcription output data. However, you can design your application or device to retain end-user data, such as transcription text. You have an option to turn on local data logging via the Speech SDK (see [Enable logging in the Speech SDK](/en-us/azure/ai-services/speech-service/how-to-use-logging)).
