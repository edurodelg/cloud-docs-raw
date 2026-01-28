---
merged_at: 2026-01-28T07:33:20.582223
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
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/reference/reference-model-inference-api -->

# Azure AI Model Inference REST API reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure AI model inference is an API that exposes a common set of capabilities for foundational models and that can be used by developers to consume predictions from a diverse set of models in a uniform and consistent way. Developers can talk with different models deployed in Azure AI Foundry portal without changing the underlying code they are using.

## Benefits

Foundational models, such as language models, have indeed made remarkable strides in recent years. These advancements have revolutionized various fields, including natural language processing and computer vision, and they have enabled applications like chatbots, virtual assistants, and language translation services.

While foundational models excel in specific domains, they lack a uniform set of capabilities. Some models are better at specific task and even across the same task, some models may approach the problem in one way while others in another. Developers can benefit from this diversity by **using the right model for the right job** allowing them to:

- Improve the performance in a specific downstream task.
- Use more efficient models for simpler tasks.
- Use smaller models that can run faster on specific tasks.
- Compose multiple models to develop intelligent experiences.

Having a uniform way to consume foundational models allow developers to realize all those benefits without sacrificing portability or changing the underlying code.

## Inference SDK support

The Azure AI Inference package allows you to consume all models supporting the Azure AI model inference API and easily change among them. Azure AI Inference package is part of the Azure AI Foundry SDK.

| Language | Documentation | Package | Examples |
|---|---|---|---|
| C# |
|

[azure-ai-inference (NuGet)](https://www.nuget.org/packages/Azure.AI.Inference/)[C# examples](https://aka.ms/azsdk/azure-ai-inference/csharp/samples)[Reference](https://aka.ms/azsdk/azure-ai-inference/java/reference)[azure-ai-inference (Maven)](https://central.sonatype.com/artifact/com.azure/azure-ai-inference/)[Java examples](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-inference/src/samples)[Reference](/en-us/javascript/api/@azure-rest/ai-inference)[@azure/ai-inference (npm)](https://www.npmjs.com/package/@azure/ai-inference)[JavaScript examples](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Reference](https://aka.ms/azsdk/azure-ai-inference/python/reference)[azure-ai-inference (PyPi)](https://pypi.org/project/azure-ai-inference/)[Python examples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/ai/azure-ai-inference/samples)## Capabilities

The following section describes some of the capabilities the API exposes:

### Modalities

The API indicates how developers can consume predictions for the following modalities:

[Get info](/en-us/rest/api/aifoundry/model-inference/get-model-info/get-model-info): Returns the information about the model deployed under the endpoint.[Text embeddings](/en-us/rest/api/aifoundry/model-inference/get-embeddings/get-embeddings): Creates an embedding vector representing the input text.[Chat completions](/en-us/rest/api/aifoundry/model-inference/get-chat-completions/get-chat-completions): Creates a model response for the given chat conversation.[Image embeddings](/en-us/rest/api/aifoundry/model-inference/get-image-embeddings/get-image-embeddings): Creates an embedding vector representing the input text and image.

### Extensibility

The Azure AI Model Inference API specifies a set of modalities and parameters that models can subscribe to. However, some models may have further capabilities that the ones the API indicates. On those cases, the API allows the developer to pass them as extra parameters in the payload.

By setting a header `extra-parameters: pass-through`

, the API will attempt to pass any unknown parameter directly to the underlying model. If the model can handle that parameter, the request completes.

The following example shows a request passing the parameter `safe_prompt`

supported by Mistral-Large, which isn't specified in the Azure AI Model Inference API.

**Request**

```
POST /chat/completions?api-version=2025-04-01
Authorization: Bearer <bearer-token>
Content-Type: application/json
extra-parameters: pass-through
```


```
{
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Explain Riemann's conjecture in 1 paragraph"
}
],
"temperature": 0,
"top_p": 1,
"response_format": { "type": "text" },
"safe_prompt": true
}
```


Note

The default value for `extra-parameters`

is `error`

which returns an error if an extra parameter is indicated in the payload. Alternatively, you can set `extra-parameters: drop`

to drop any unknown parameter in the request. Use this capability in case you happen to be sending requests with extra parameters that you know the model won't support but you want the request to completes anyway. A typical example of this is indicating `seed`

parameter.

### Models with disparate set of capabilities

The Azure AI Model Inference API indicates a general set of capabilities but each of the models can decide to implement them or not. A specific error is returned on those cases where the model can't support a specific parameter.

The following example shows the response for a chat completion request indicating the parameter `reponse_format`

and asking for a reply in `JSON`

format. In the example, since the model doesn't support such capability an error 422 is returned to the user.

**Request**

```
POST /chat/completions?api-version=2025-04-01
Authorization: Bearer <bearer-token>
Content-Type: application/json
```


```
{
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Explain Riemann's conjecture in 1 paragraph"
}
],
"temperature": 0,
"top_p": 1,
"response_format": { "type": "json_object" },
}
```


**Response**

```
{
"status": 422,
"code": "parameter_not_supported",
"detail": {
"loc": [ "body", "response_format" ],
"input": "json_object"
},
"message": "One of the parameters contain invalid values."
}
```


Tip

You can inspect the property `details.loc`

to understand the location of the offending parameter and `details.input`

to see the value that was passed in the request.

## Content safety

The Azure AI model inference API supports [Azure AI Content Safety](../../../ai-studio/concepts/content-filtering.md). When using deployments with Azure AI Content Safety on, inputs and outputs pass through an ensemble of classification models aimed at detecting and preventing the output of harmful content. The content filtering (preview) system detects and takes action on specific categories of potentially harmful content in both input prompts and output completions.

The following example shows the response for a chat completion request that has triggered content safety.

**Request**

```
POST /chat/completions?api-version=2025-04-01
Authorization: Bearer <bearer-token>
Content-Type: application/json
```


```
{
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Chopping tomatoes and cutting them into cubes or wedges are great ways to practice your knife skills."
}
],
"temperature": 0,
"top_p": 1,
}
```


**Response**

```
{
"status": 400,
"code": "content_filter",
"message": "The response was filtered",
"param": "messages",
"type": null
}
```


## Getting started

Azure AI model inference API is available on Azure AI Services resources. You can get started with it the same way as any other Azure product where you [create and configure your resource for Azure AI model inference](/en-us/azure/ai-foundry/model-inference/how-to/quickstart-create-resources), or instance of the service, in your Azure Subscription. You can create as many resources as needed and configure them independently in case you have multiple teams with different requirements.

Once you create an Azure AI Services resource, you must deploy a model before you can start making API calls. By default, no models are available on it, so you can control which ones to start from. See the tutorial [Create your first model deployment in Azure AI model inference](/en-us/azure/ai-foundry/model-inference/how-to/create-model-deployments).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/model-inference/reference/reference-model-inference-chat-completions -->

# Get Chat Completions - Get Chat Completions

Gets chat completions for the provided chat messages.
Completions support a wide variety of tasks and generate text that continues from or "completes"
provided prompt data. The method makes a REST API call to the `/chat/completions`

route
on the given endpoint.

`POST https://{resource}.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview`


## URI Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
|
resource
|
path | True |
string |
The Azure AI Services resource name, for example 'my-resource' |
|
api-version
|
query | True |
string minLength: 1 |
The API version to use for this operation. |

## Request Header

| Name | Required | Type | Description |
|---|---|---|---|
| extra-parameters |
Controls what happens if extra parameters, undefined by the REST API,
are passed in the JSON request payload.
This sets the HTTP request header |

## Request Body

| Name | Required | Type | Description |
|---|---|---|---|
| messages | True | ChatRequestMessage[]: |
The collection of context messages associated with this chat completions request. Typical usage begins with a chat message for the System role that provides instructions for the behavior of the assistant, followed by alternating messages between the User and Assistant roles. |
| frequency_penalty |
number (float) minimum: -2maximum: 2 |
A value that influences the probability of generated tokens appearing based on their cumulative frequency in generated text. Positive values will make tokens less likely to appear as their frequency increases and decrease the likelihood of the model repeating the same statements verbatim. Supported range is [-2, 2]. |
|
| max_tokens |
integer (int32) minimum: 0 |
The maximum number of tokens to generate. |
|
| modalities |
The modalities that the model is allowed to use for the chat completions response. The default modality
is |
||
| model |
string |
ID of the specific AI model to use, if more than one model is available on the endpoint. |
|
| presence_penalty |
number (float) minimum: -2maximum: 2 |
A value that influences the probability of generated tokens appearing based on their existing presence in generated text. Positive values will make tokens less likely to appear when they already exist and increase the model's likelihood to output new topics. Supported range is [-2, 2]. |
|
| response_format | ChatCompletionsResponseFormat: |
An object specifying the format that the model must output. Setting to Setting to
|
|
| seed |
integer (int64) |
If specified, the system will make a best effort to sample deterministically such that repeated requests with the same seed and parameters should return the same result. Determinism is not guaranteed. |
|
| stop |
string[] |
A collection of textual sequences that will end completions generation. |
|
| stream |
boolean |
A value indicating whether chat completions should be streamed for this request. |
|
| temperature |
number (float) minimum: 0maximum: 1 |
The sampling temperature to use that controls the apparent creativity of generated completions. Higher values will make output more random while lower values will make results more focused and deterministic. It is not recommended to modify temperature and top_p for the same completions request as the interaction of these two settings is difficult to predict. Supported range is [0, 1]. |
|
| tool_choice |
|
If specified, the model will configure which of the provided tools it can use for the chat completions response. |
|
| tools |
A list of tools the model may request to call. Currently, only functions are supported as a tool. The model may response with a function call request and provide the input arguments in JSON format for that function. |
||
| top_p |
number (float) minimum: 0maximum: 1 |
An alternative to sampling with temperature called nucleus sampling. This value causes the model to consider the results of tokens with the provided probability mass. As an example, a value of 0.15 will cause only the tokens comprising the top 15% of probability mass to be considered. It is not recommended to modify temperature and top_p for the same completions request as the interaction of these two settings is difficult to predict. Supported range is [0, 1]. |

## Responses

| Name | Type | Description |
|---|---|---|
| 200 OK |
The request has succeeded. |
|
| Other Status Codes |
An unexpected error response. Headers x-ms-error-code: string |

## Security

### api-key

Type:
apiKey

In:
header


### OAuth2Auth

Type:
oauth2

Flow:
implicit

Authorization URL:
https://login.microsoftonline.com/common/oauth2/v2.0/authorize


#### Scopes

| Name | Description |
|---|---|
| https://cognitiveservices.azure.com/.default |

## Examples

|
|

[maximum set chat completion](#maximum-set-chat-completion)[minimum set chat completion](#minimum-set-chat-completion)### Audio modality chat completion

#### Sample request

```
POST https://{resource}.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview
{
"modalities": [
"text",
"audio"
],
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": [
{
"type": "input_audio",
"input_audio": {
"data": "<base64 encoded audio data>",
"format": "wav"
}
}
]
},
{
"role": "assistant",
"content": null,
"audio": {
"id": "abcdef1234"
}
},
{
"role": "user",
"content": [
{
"type": "input_audio",
"input_audio": {
"data": "<base64 encoded audio data>",
"format": "wav"
}
}
]
}
],
"frequency_penalty": 0,
"presence_penalty": 0,
"temperature": 0,
"top_p": 0,
"seed": 21,
"model": "my-model-name"
}
```


#### Sample response

```
{
"id": "kgousajxgzyhugvqekuswuqbk",
"object": "chat.completion",
"created": 1696522361,
"model": "my-model-name",
"usage": {
"completion_tokens": 19,
"prompt_tokens": 28,
"total_tokens": 16,
"completion_tokens_details": {
"audio_tokens": 5,
"total_tokens": 5
},
"prompt_tokens_details": {
"audio_tokens": 10,
"cached_tokens": 0
}
},
"choices": [
{
"index": 0,
"finish_reason": "stop",
"message": {
"role": "assistant",
"content": null,
"tool_calls": null,
"audio": {
"id": "abcdef1234",
"format": "wav",
"data": "<base64 encoded audio data>",
"expires_at": 1896522361,
"transcript": "This is a sample transcript"
}
}
}
]
}
```


### maximum set chat completion

#### Sample request

```
POST https://{resource}.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview
{
"modalities": [
"text"
],
"messages": [
{
"role": "system",
"content": "You are a helpful assistant"
},
{
"role": "user",
"content": "Explain Riemann's conjecture"
},
{
"role": "assistant",
"content": "The Riemann Conjecture is a deep mathematical conjecture around prime numbers and how they can be predicted. It was first published in Riemann's groundbreaking 1859 paper. The conjecture states that the Riemann zeta function has its zeros only at the negative even integers and complex numbers with real part 1/21. Many consider it to be the most important unsolved problem in pure mathematics. The Riemann hypothesis is a way to predict the probability that numbers in a certain range are prime that was also devised by German mathematician Bernhard Riemann in 18594."
},
{
"role": "user",
"content": "Ist it proved?"
}
],
"frequency_penalty": 0,
"stream": true,
"presence_penalty": 0,
"temperature": 0,
"top_p": 0,
"max_tokens": 255,
"response_format": {
"type": "text"
},
"stop": [
"<|endoftext|>"
],
"tools": [
{
"type": "function",
"function": {
"name": "my-function-name",
"description": "A function useful to know if a theroem is proved or not"
}
}
],
"seed": 21,
"model": "my-model-name"
}
```


#### Sample response

```
{
"id": "kgousajxgzyhugvqekuswuqbk",
"object": "chat.completion",
"created": 18,
"model": "my-model-name",
"usage": {
"completion_tokens": 19,
"prompt_tokens": 28,
"total_tokens": 16
},
"choices": [
{
"index": 7,
"finish_reason": "stop",
"message": {
"role": "assistant",
"content": null,
"tool_calls": [
{
"id": "yrobmilsrugmbwukmzo",
"type": "function",
"function": {
"name": "my-function-name",
"arguments": "{ \"arg1\": \"value1\", \"arg2\": \"value2\" }"
}
}
]
}
}
]
}
```


### minimum set chat completion

#### Sample request

```
POST https://{resource}.services.ai.azure.com/models/chat/completions?api-version=2024-05-01-preview
{
"messages": [
{
"role": "user",
"content": "Explain Riemann's conjecture"
}
]
}
```


#### Sample response

```
{
"id": "kgousajxgzyhugvqekuswuqbk",
"object": "chat.completion",
"created": 1234567890,
"model": "my-model-name",
"usage": {
"prompt_tokens": 205,
"completion_tokens": 5,
"total_tokens": 210
},
"choices": [
{
"index": 0,
"finish_reason": "stop",
"message": {
"role": "assistant",
"content": "The Riemann Conjecture is a deep mathematical conjecture around prime numbers and how they can be predicted. It was first published in Riemann's groundbreaking 1859 paper. The conjecture states that the Riemann zeta function has its zeros only at the negative even integers and complex numbers with real part 1/21. Many consider it to be the most important unsolved problem in pure mathematics. The Riemann hypothesis is a way to predict the probability that numbers in a certain range are prime that was also devised by German mathematician Bernhard Riemann in 18594"
}
}
]
}
```


## Definitions

| Name | Description |
|---|---|
|
|

A representation of the possible audio formats for audio.

[Azure.](#azure.core.foundations.error) Core. Foundations. ErrorThe error object.

[Azure.](#azure.core.foundations.errorresponse) Core. Foundations. Error ResponseA response containing error details.

[Azure.](#azure.core.foundations.innererror) Core. Foundations. Inner ErrorAn object containing more specific information about the error. As per Azure REST API guidelines - [https://aka.ms/AzureRestApiGuidelines#handling-errors](https://aka.ms/AzureRestApiGuidelines#handling-errors).

[Chat](#chatchoice) ChoiceThe representation of a single prompt completion as part of an overall chat completions request.
Generally, `n`

choices are generated per provided prompt with a default value of 1.
Token limits and other settings may limit the number of choices generated.

[Chat](#chatcompletions) CompletionsRepresentation of the response data from a chat completions request. Completions support a wide variety of tasks and generate text that continues from or "completes" provided prompt data.

[Chat](#chatcompletionsaudio) Completions AudioA representation of the audio generated by the model.

[Chat](#chatcompletionsmodality) Completions ModalityThe modalities that the model is allowed to use for the chat completions response.

[Chat](#chatcompletionsoptions) Completions OptionsThe configuration information for a chat completions request. Completions support a wide variety of tasks and generate text that continues from or "completes" provided prompt data.

[Chat](#chatcompletionsresponseformatjsonobject) Completions Response Format Json ObjectA response format for Chat Completions that restricts responses to emitting valid JSON objects. Note that to enable JSON mode, some AI models may also require you to instruct the model to produce JSON via a system or user message.

[Chat](#chatcompletionsresponseformatjsonschema) Completions Response Format Json SchemaA response format for Chat Completions that restricts responses to emitting valid JSON objects, with a JSON schema specified by the caller.

[Chat](#chatcompletionsresponseformatjsonschemadefinition) Completions Response Format Json Schema DefinitionThe definition of the required JSON schema in the response, and associated metadata.

[Chat](#chatcompletionsresponseformattext) Completions Response Format TextA response format for Chat Completions that emits text responses. This is the default response format.

[Chat](#chatcompletionstoolcall) Completions Tool CallA function tool call requested by the AI model.

[Chat](#chatcompletionstooldefinition) Completions Tool DefinitionThe definition of a chat completions tool that can call a function.

[Chat](#chatrequestassistantmessage) Request Assistant MessageA request chat message representing response or action from the assistant.

[Chat](#chatrequestaudioreference) Request Audio ReferenceA reference to an audio response generated by the model.

[Chat](#chatrequestsystemmessage) Request System MessageA request chat message containing system instructions that influence how the model will generate a chat completions response.

[Chat](#chatrequesttoolmessage) Request Tool MessageA request chat message representing requested output from a configured tool.

[Chat](#chatrequestusermessage) Request User MessageA request chat message representing user input to the assistant.

[Chat](#chatresponsemessage) Response MessageA representation of a chat message as received in a response.

[Chat](#chatrole) RoleA description of the intended purpose of a message within a chat completions interaction.

[Completions](#completionsfinishreason) Finish ReasonRepresentation of the manner in which a completions response concluded.

[Completions](#completionsusage) UsageRepresentation of the token counts processed for a completions request. Counts consider all tokens across prompts, choices, choice alternates, best_of generations, and other consumers.

[Completions](#completionsusagedetails) Usage DetailsA breakdown of tokens used in a completion.

[Extra](#extraparameters) ParametersControls what happens if extra parameters, undefined by the REST API, are passed in the JSON request payload.

[Function](#functioncall) CallThe name and arguments of a function that should be called, as generated by the model.

[Function](#functiondefinition) DefinitionThe definition of a caller-specified function that chat completions may invoke in response to matching user input.

[Prompt](#promptusagedetails) Usage DetailsA breakdown of tokens used in the prompt/chat history.

### Audio Content Format

A representation of the possible audio formats for audio.

| Value | Description |
|---|---|
| wav |
Specifies audio in WAV format. |
| mp3 |
Specifies audio in MP3 format. |

### Azure. Core. Foundations. Error

The error object.

| Name | Type | Description |
|---|---|---|
| code |
string |
One of a server-defined set of error codes. |
| details |
An array of details about specific errors that led to this reported error. |
|
| innererror |
An object containing more specific information than the current object about the error. |
|
| message |
string |
A human-readable representation of the error. |
| target |
string |
The target of the error. |

### Azure. Core. Foundations. Error Response

A response containing error details.

| Name | Type | Description |
|---|---|---|
| error |
The error object. |

### Azure. Core. Foundations. Inner Error

An object containing more specific information about the error. As per Azure REST API guidelines - [https://aka.ms/AzureRestApiGuidelines#handling-errors](https://aka.ms/AzureRestApiGuidelines#handling-errors).

| Name | Type | Description |
|---|---|---|
| code |
string |
One of a server-defined set of error codes. |
| innererror |
Inner error. |

### Chat Choice

The representation of a single prompt completion as part of an overall chat completions request.
Generally, `n`

choices are generated per provided prompt with a default value of 1.
Token limits and other settings may limit the number of choices generated.

| Name | Type | Description |
|---|---|---|
| finish_reason |
The reason that this chat completions choice completed its generated. |
|
| index |
integer (int32) |
The ordered index associated with this chat completions choice. |
| message |
The chat message for a given chat completions prompt. |

### Chat Completions

Representation of the response data from a chat completions request. Completions support a wide variety of tasks and generate text that continues from or "completes" provided prompt data.

| Name | Type | Description |
|---|---|---|
| choices |
The collection of completions choices associated with this completions response.
Generally, |
|
| created |
integer (unixtime) |
The first timestamp associated with generation activity for this completions response, represented as seconds since the beginning of the Unix epoch of 00:00 on 1 Jan 1970. |
| id |
string |
A unique identifier associated with this chat completions response. |
| model |
string |
The model used for the chat completion. |
| object |
enum:
chat. |
The response object type, which is always |
| usage |
Usage information for tokens processed and generated as part of this completions operation. |

### Chat Completions Audio

A representation of the audio generated by the model.

| Name | Type | Description |
|---|---|---|
| data |
string |
Base64 encoded audio data |
| expires_at |
integer (unixtime) |
The Unix timestamp (in seconds) at which the audio piece expires and can't be any longer referenced by its ID in multi-turn conversations. |
| format |
The format of the audio content. If format is not provided, it will match the format used in the input audio request. |
|
| id |
string |
Unique identifier for the audio response. This value can be used in chat history messages instead of passing the full audio object. |
| transcript |
string |
The transcript of the audio file. |

### Chat Completions Modality

The modalities that the model is allowed to use for the chat completions response.

| Value | Description |
|---|---|
| text |
The model is only allowed to generate text. |
| audio |
The model is allowed to generate audio. |

### Chat Completions Options

The configuration information for a chat completions request. Completions support a wide variety of tasks and generate text that continues from or "completes" provided prompt data.

| Name | Type | Default value | Description |
|---|---|---|---|
| frequency_penalty |
number (float) minimum: -2maximum: 2 |
0 |
A value that influences the probability of generated tokens appearing based on their cumulative frequency in generated text. Positive values will make tokens less likely to appear as their frequency increases and decrease the likelihood of the model repeating the same statements verbatim. Supported range is [-2, 2]. |
| max_tokens |
integer (int32) minimum: 0 |
The maximum number of tokens to generate. |
|
| messages | ChatRequestMessage[]: |
The collection of context messages associated with this chat completions request. Typical usage begins with a chat message for the System role that provides instructions for the behavior of the assistant, followed by alternating messages between the User and Assistant roles. |
|
| modalities |
The modalities that the model is allowed to use for the chat completions response. The default modality
is |
||
| model |
string |
ID of the specific AI model to use, if more than one model is available on the endpoint. |
|
| presence_penalty |
number (float) minimum: -2maximum: 2 |
0 |
A value that influences the probability of generated tokens appearing based on their existing presence in generated text. Positive values will make tokens less likely to appear when they already exist and increase the model's likelihood to output new topics. Supported range is [-2, 2]. |
| response_format | ChatCompletionsResponseFormat: |
An object specifying the format that the model must output. Setting to Setting to
|
|
| seed |
integer (int64) |
If specified, the system will make a best effort to sample deterministically such that repeated requests with the same seed and parameters should return the same result. Determinism is not guaranteed. |
|
| stop |
string[] |
A collection of textual sequences that will end completions generation. |
|
| stream |
boolean |
A value indicating whether chat completions should be streamed for this request. |
|
| temperature |
number (float) minimum: 0maximum: 1 |
0.7 |
The sampling temperature to use that controls the apparent creativity of generated completions. Higher values will make output more random while lower values will make results more focused and deterministic. It is not recommended to modify temperature and top_p for the same completions request as the interaction of these two settings is difficult to predict. Supported range is [0, 1]. |
| tool_choice |
|
If specified, the model will configure which of the provided tools it can use for the chat completions response. |
|
| tools |
A list of tools the model may request to call. Currently, only functions are supported as a tool. The model may response with a function call request and provide the input arguments in JSON format for that function. |
||
| top_p |
number (float) minimum: 0maximum: 1 |
1 |
An alternative to sampling with temperature called nucleus sampling. This value causes the model to consider the results of tokens with the provided probability mass. As an example, a value of 0.15 will cause only the tokens comprising the top 15% of probability mass to be considered. It is not recommended to modify temperature and top_p for the same completions request as the interaction of these two settings is difficult to predict. Supported range is [0, 1]. |

### Chat Completions Response Format Json Object

A response format for Chat Completions that restricts responses to emitting valid JSON objects. Note that to enable JSON mode, some AI models may also require you to instruct the model to produce JSON via a system or user message.

| Name | Type | Description |
|---|---|---|
| type |
string:
json_object |
The response format type to use for chat completions. |

### Chat Completions Response Format Json Schema

A response format for Chat Completions that restricts responses to emitting valid JSON objects, with a JSON schema specified by the caller.

| Name | Type | Description |
|---|---|---|
| json_schema |
The definition of the required JSON schema in the response, and associated metadata. |
|
| type |
string:
json_schema |
The response format type to use for chat completions. |

### Chat Completions Response Format Json Schema Definition

The definition of the required JSON schema in the response, and associated metadata.

| Name | Type | Default value | Description |
|---|---|---|---|
| description |
string |
A description of the response format, used by the AI model to determine how to generate responses in this format. |
|
| name |
string |
The name of the response format. Must be a-z, A-Z, 0-9, or contain underscores and dashes, with a maximum length of 64. |
|
| schema |
|
The definition of the JSON schema |
|
| strict |
boolean |
False |
Whether to enable strict schema adherence when generating the output.
If set to true, the model will always follow the exact schema defined in the |

### Chat Completions Response Format Text

A response format for Chat Completions that emits text responses. This is the default response format.

| Name | Type | Description |
|---|---|---|
| type |
string:
text |
The response format type to use for chat completions. |

### Chat Completions Tool Call

A function tool call requested by the AI model.

| Name | Type | Description |
|---|---|---|
| function |
The details of the function call requested by the AI model. |
|
| id |
string |
The ID of the tool call. |
| type |
enum:
function |
The type of tool call. Currently, only |

### Chat Completions Tool Definition

The definition of a chat completions tool that can call a function.

| Name | Type | Description |
|---|---|---|
| function |
The function definition details for the function tool. |
|
| type |
enum:
function |
The type of the tool. Currently, only |

### Chat Request Assistant Message

A request chat message representing response or action from the assistant.

| Name | Type | Description |
|---|---|---|
| audio |
The audio generated by a previous response in a multi-turn conversation. |
|
| content |
string |
The content of the message. |
| role |
string:
assistant |
The chat role associated with this message. |
| tool_calls |
The tool calls that must be resolved and have their outputs appended to subsequent input messages for the chat completions request to resolve as configured. |

### Chat Request Audio Reference

A reference to an audio response generated by the model.

| Name | Type | Description |
|---|---|---|
| id |
string |
Unique identifier for the audio response. This value corresponds to the id of a previous audio completion. |

### Chat Request System Message

A request chat message containing system instructions that influence how the model will generate a chat completions response.

| Name | Type | Description |
|---|---|---|
| content |
string |
The contents of the system message. |
| role |
string:
system |
The chat role associated with this message. |

### Chat Request Tool Message

A request chat message representing requested output from a configured tool.

| Name | Type | Description |
|---|---|---|
| content |
string |
The content of the message. |
| role |
string:
tool |
The chat role associated with this message. |
| tool_call_id |
string |
The ID of the tool call resolved by the provided content. |

### Chat Request User Message

A request chat message representing user input to the assistant.

| Name | Type | Description |
|---|---|---|
| content |
|
The contents of the user message, with available input types varying by selected model. |
| role |
string:
user |
The chat role associated with this message. |

### Chat Response Message

A representation of a chat message as received in a response.

| Name | Type | Description |
|---|---|---|
| audio |
The audio generated by the model as a response to the messages if the model is configured to generate audio. |
|
| content |
string |
The content of the message. |
| role |
The chat role associated with the message. |
|
| tool_calls |
The tool calls that must be resolved and have their outputs appended to subsequent input messages for the chat completions request to resolve as configured. |

### Chat Role

A description of the intended purpose of a message within a chat completions interaction.

| Value | Description |
|---|---|
| system |
The role that instructs or sets the behavior of the assistant. |
| developer |
The role that provides instructions to the model prioritized ahead of user messages. |
| user |
The role that provides input for chat completions. |
| assistant |
The role that provides responses to system-instructed, user-prompted input. |
| tool |
The role that represents extension tool activity within a chat completions operation. |

### Completions Finish Reason

Representation of the manner in which a completions response concluded.

| Value | Description |
|---|---|
| stop |
Completions ended normally and reached its end of token generation. |
| length |
Completions exhausted available token limits before generation could complete. |
| content_filter |
Completions generated a response that was identified as potentially sensitive per content moderation policies. |
| tool_calls |
Completion ended with the model calling a provided tool for output. |

### Completions Usage

Representation of the token counts processed for a completions request. Counts consider all tokens across prompts, choices, choice alternates, best_of generations, and other consumers.

| Name | Type | Description |
|---|---|---|
| completion_tokens |
integer (int32) |
The number of tokens generated across all completions emissions. |
| completion_tokens_details |
Breakdown of tokens used in a completion. |
|
| prompt_tokens |
integer (int32) |
The number of tokens in the provided prompts for the completions request. |
| prompt_tokens_details |
Breakdown of tokens used in the prompt/chat history. |
|
| total_tokens |
integer (int32) |
The total number of tokens processed for the completions request and response. |

### Completions Usage Details

A breakdown of tokens used in a completion.

| Name | Type | Description |
|---|---|---|
| audio_tokens |
integer (int32) |
The number of tokens corresponding to audio input. |
| total_tokens |
integer (int32) |
The total number of tokens processed for the completions request and response. |

### Extra Parameters

Controls what happens if extra parameters, undefined by the REST API, are passed in the JSON request payload.

| Value | Description |
|---|---|
| error |
The service will error if it detected extra parameters in the request payload. This is the service default. |
| drop |
The service will ignore (drop) extra parameters in the request payload. It will only pass the known parameters to the back-end AI model. |
| pass-through |
The service will pass extra parameters to the back-end AI model. |

### Function Call

The name and arguments of a function that should be called, as generated by the model.

| Name | Type | Description |
|---|---|---|
| arguments |
string |
The arguments to call the function with, as generated by the model in JSON format. Note that the model does not always generate valid JSON, and may hallucinate parameters not defined by your function schema. Validate the arguments in your code before calling your function. |
| name |
string |
The name of the function to call. |

### Function Definition

The definition of a caller-specified function that chat completions may invoke in response to matching user input.

| Name | Type | Description |
|---|---|---|
| description |
string |
A description of what the function does. The model will use this description when selecting the function and interpreting its parameters. |
| name |
string |
The name of the function to be called. |
| parameters |
|
The parameters the function accepts, described as a JSON Schema object. |

### Prompt Usage Details

A breakdown of tokens used in the prompt/chat history.

| Name | Type | Description |
|---|---|---|
| audio_tokens |
integer (int32) |
The number of tokens corresponding to audio input. |
| cached_tokens |
integer (int32) |
The total number of tokens cached. |
