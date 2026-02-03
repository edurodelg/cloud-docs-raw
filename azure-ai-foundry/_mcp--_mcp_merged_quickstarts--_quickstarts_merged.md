---
merged_at: 2026-02-04T00:35:27.903274
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
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/quickstarts/hub-get-started-code -->

# Quickstart: Get started with Microsoft Foundry (Hub projects)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Tip

An alternate Foundry project quickstart is available: [Quickstart: Get started with Microsoft Foundry (Foundry projects)](get-started-code?view=foundry-classic).

This quickstart sets up your local environment for hub-based projects, deploys a model, and builds a simple traced/evaluable chat script.

## Prerequisites

- Azure subscription.
- Existing hub project (or
[create one](../how-to/hub-create-projects?view=foundry-classic)). If not, consider using a Foundry project quickstart.

## Set up your development environment

- Install prerequisites (Python, Azure CLI, login).
- Install packages:

```
pip install azure-ai-inference azure-identity azure-ai-projects==1.0.0b10
```


Different project types need distinct azure-ai-projects versions. Keep each project in its own isolated environment to avoid conflicts.


## Deploy a model

- Portal: Sign in, open hub project.
- Model catalog: select gpt-4o-mini.
- Use this model > accept default deployment name > Deploy.
- After success: Open in playground to verify.

## Build your chat app

Create chat.py with sample code:

```
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential
project_connection_string = "<your-connection-string-goes-here>"
project = AIProjectClient.from_connection_string(
conn_str=project_connection_string, credential=DefaultAzureCredential()
)
chat = project.inference.get_chat_completions_client()
response = chat.complete(
model="gpt-4o-mini",
messages=[
{
"role": "system",
"content": "You are an AI assistant that speaks like a techno punk rocker from 2350. Be cool but not too cool. Ya dig?",
},
{"role": "user", "content": "Hey, can you help me with my taxes? I'm a freelancer."},
],
)
print(response.choices[0].message.content)
```


Insert your project connection string from the project Overview page (copy, replace placeholder in code).

Run:

```
python chat.py
```


## Add prompt templating

Add get_chat_response using mustache template (see chat-template.py sample) then invoke with user/context messages.

Run again to view templated response.

## Clean up resources

Delete deployment or project when done to avoid charges.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/quickstarts/get-started-playground -->

# Quickstart: Get answers in the chat playground

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Learn how to use the chat playground in [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) to explore AI model capabilities interactively. This quickstart focuses on the web-based UI experience; to build applications programmatically, see [Build a custom chat app using the SDK](get-started-code?view=foundry-classic).

Deploy (or reuse) a chat model and send prompts to receive AI-generated responses.

In this quickstart, you learn how to:

- Configure a system message to guide model behavior.
- Send a user question and receive a response.
- Interpret model responses and recognize limitations.
- Add safety system messages to ensure responsible AI use.

For this quickstart, you can use either a hub-based project or a Foundry project. For more information about the differences between these two project types, see [Project types](../what-is-foundry?view=foundry-classic#types-of-projects).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The following Azure RBAC roles are required. To verify your role, see
[Manage access control](../how-to/create-azure-ai-resource?view=foundry-classic#manage-access-control).**Owner**on the subscription to create a project and assign roles.**Azure AI User**on the project to deploy models (assigned automatically when you create the project as Owner of the subscription).


## Deploy a model

In the portal, you can explore a rich catalog of cutting-edge models from many different providers. For this tutorial, search and then select the **gpt-4o** model.

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**. If you're in a project, select

**Microsoft Foundry**in the upper-left breadcrumb to leave the project. You'll create a new one in a moment.From the landing page or

, select[Model catalog](https://ai.azure.com/explore/models)**gpt-4o**(or**gpt-4o-mini**).Select

**Use this model**. When prompted, enter a new project name and select**Create**.Review the deployment name and select

**Create**.Then select

**Connect and deploy**after selecting a deployment type.Select

**Open in playground**from the deployment page after it's deployed.You land in the Chat playground with the model pre-deployed and ready to use.


If you're building an agent, you can instead start with **Create an agent**. The steps are similar, but in a different order. Once the project is created, you arrive at the Agent playground instead of the Chat playground.

## Use the chat playground

Use the [Foundry](https://ai.azure.com/?cid=learnDocs) playground to interact with deployed chat models and test prompts in real time.

To get answers from your deployed model in the chat playground:

In the

**System message**text box, provide a prompt to guide the assistant. For example, for a customer support scenario, use: "You're a helpful customer support agent. Answer questions about product features, pricing, and troubleshooting. If you don't know the answer, offer to escalate to a specialist." You can tailor the prompt for your specific use case.Optionally, add a safety system message by selecting the

**Add section**button, and then**Safety system messages**. Choose from the prebuilt messages, and then edit them to your needs.Select

**Apply changes**to save your changes. When prompted to see if you want to update the system message, select**Continue**.In the chat session pane, enter the following question: "How much do the TrailWalker hiking shoes cost?"

Select the right arrow icon to send.

The assistant either replies that it doesn't know the answer or provides a generic response, such as noting price variability. This is expected because the model doesn't have access to current product data.


**Understanding the response:** The model generated text based on its training data and system message, but without grounding data (like a product catalog), it can't provide accurate domain-specific answers. This limitation is normal and expected in this scenario.

Next, add your data so the model can answer domain-specific questions. Try the enterprise chat web app tutorial.

### Troubleshooting

| Issue | Action |
|---|---|
| No deployed models listed | Deploy a model from the model catalog first. |
| Repeated generic answers | Refine system message or add domain data. |
| Safety message overrides tone | Adjust or remove conflicting safety sections. |
| Slow first response | Allow for cold start; subsequent prompts are faster. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/quickstarts/get-started-code -->

# Microsoft Foundry quickstart

The Microsoft Foundry SDK is available in multiple languages, including Python, Java, TypeScript, and C#. This quickstart provides instructions for each of these languages.

In the portal, you can explore a rich catalog of cutting-edge models from many different providers. For this tutorial, search and then select the **gpt-4o** model.

Chat completions are the basic building block of AI applications. Using chat completions you can send a list of messages and get a response from the model.

Substitute your endpoint for the `endpoint`

in this code:

```
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential
project = AIProjectClient(
endpoint="https://your-foundry-resource-name.ai.azure.com/api/projects/project-name",
credential=DefaultAzureCredential(),
)
models = project.get_openai_client(api_version="2024-10-21")
response = models.chat.completions.create(
model="gpt-4o",
messages=[
{"role": "system", "content": "You are a helpful writing assistant"},
{"role": "user", "content": "Write me a poem about flowers"},
],
)
print(response.choices[0].message.content)
```


```
using System.ClientModel.Primitives;
using Azure.Identity;
using OpenAI;
using OpenAI.Chat;
#pragma warning disable OPENAI001
string projectEndpoint = System.Environment.GetEnvironmentVariable("AZURE_AI_INFERENCE")!;
string modelDeploymentName = System.Environment.GetEnvironmentVariable("AZURE_AI_MODEL")!;
BearerTokenPolicy tokenPolicy = new(
new DefaultAzureCredential(),
"https://ai.azure.com/.default");
OpenAIClient openAIClient = new(
authenticationPolicy: tokenPolicy,
options: new OpenAIClientOptions()
{
Endpoint = new($"{projectEndpoint}/openai/v1"),
});
ChatClient chatClient = openAIClient.GetChatClient(modelDeploymentName);
ChatCompletion completion = await chatClient.CompleteChatAsync(
[
new SystemChatMessage("You are a helpful assistant."),
new UserChatMessage("How many feet are in a mile?")
]);
Console.WriteLine(completion.Content[0].Text);
```


```
// Get the Azure AI endpoint and deployment name from environment variables
const endpoint = process.env.PROJECT_ENDPOINT as string;
const deployment = process.env.MODEL_DEPLOYMENT_NAME || 'gpt-4o';
// Create an Azure OpenAI Client
const project = new AIProjectClient(endpoint, new DefaultAzureCredential());
const client = await project.getAzureOpenAIClient({
// The API version should match the version of the Azure OpenAI resource
apiVersion: "2024-12-01-preview"
});
// Create a chat completion
const chatCompletion = await client.chat.completions.create({
model: deployment,
messages: [
{ role: "system", content: "You are a helpful writing assistant" },
{ role: "user", content: "Write me a poem about flowers" },
],
});
console.log(`\n==================== 🌷 COMPLETIONS POEM ====================\n`);
console.log(chatCompletion.choices[0].message.content);
```


```
package com.azure.ai.foundry.samples;
import com.azure.ai.inference.ChatCompletionsClient;
import com.azure.ai.inference.ChatCompletionsClientBuilder;
import com.azure.ai.inference.models.ChatCompletions;
import com.azure.core.credential.AzureKeyCredential;
import com.azure.core.credential.TokenCredential;
import com.azure.core.exception.HttpResponseException;
import com.azure.core.util.logging.ClientLogger;
import com.azure.identity.DefaultAzureCredentialBuilder;
/**
* Sample demonstrating non-streaming chat completion functionality
* using the Azure AI Inference SDK, wired to your AOAI project endpoint.
*
* Environment variables:
* - PROJECT_ENDPOINT: Required. Your Azure AI project endpoint.
* - AZURE_AI_API_KEY: Optional. Your API key (falls back to DefaultAzureCredential).
* - AZURE_MODEL_DEPLOYMENT_NAME: Optional. Model deployment name (default: "phi-4").
* - AZURE_MODEL_API_PATH: Optional. API path segment (default: "deployments").
* - CHAT_PROMPT: Optional. The prompt to send (uses a default if not provided).
*
* SDK Features Demonstrated:
* - Using the Azure AI Inference SDK (com.azure:azure-ai-inference:1.0.0-beta.5)
* - Creating a ChatCompletionsClient with Azure or API key authentication
* - Configuring endpoint paths for different model deployments
* - Using the simplified complete() method for quick completions
* - Accessing response content through strongly-typed objects
* - Implementing proper error handling for service requests
* - Choosing between DefaultAzureCredential and AzureKeyCredential
*
*/
public class ChatCompletionSample {
private static final ClientLogger logger = new ClientLogger(ChatCompletionSample.class);
public static void main(String[] args) {
// 1) Read and validate the project endpoint
String projectEndpoint = System.getenv("PROJECT_ENDPOINT");
if (projectEndpoint == null || projectEndpoint.isBlank()) {
logger.error("PROJECT_ENDPOINT is required but not set");
return;
}
// 2) Optional auth + model settings
String apiKey = System.getenv("AZURE_AI_API_KEY");
String deploymentName = System.getenv("AZURE_MODEL_DEPLOYMENT_NAME");
String apiPath = System.getenv("AZURE_MODEL_API_PATH");
String prompt = System.getenv("CHAT_PROMPT");
if (deploymentName == null || deploymentName.isBlank()) {
deploymentName = "phi-4";
logger.info("No AZURE_MODEL_DEPLOYMENT_NAME provided, using default: {}", deploymentName);
}
if (apiPath == null || apiPath.isBlank()) {
apiPath = "deployments";
logger.info("No AZURE_MODEL_API_PATH provided, using default: {}", apiPath);
}
if (prompt == null || prompt.isBlank()) {
prompt = "What best practices should I follow when asking an AI model to review Java code?";
logger.info("No CHAT_PROMPT provided, using default prompt: {}", prompt);
}
try {
// 3) Build the full inference endpoint URL
String fullEndpoint = projectEndpoint.endsWith("/")
? projectEndpoint
: projectEndpoint + "/";
fullEndpoint += apiPath + "/" + deploymentName;
logger.info("Using inference endpoint: {}", fullEndpoint);
// 4) Create the client with key or token credential :contentReference[oaicite:0]{index=0}
ChatCompletionsClient client;
if (apiKey != null && !apiKey.isBlank()) {
logger.info("Authenticating using API key");
client = new ChatCompletionsClientBuilder()
.credential(new AzureKeyCredential(apiKey))
.endpoint(fullEndpoint)
.buildClient();
} else {
logger.info("Authenticating using DefaultAzureCredential");
TokenCredential credential = new DefaultAzureCredentialBuilder().build();
client = new ChatCompletionsClientBuilder()
.credential(credential)
.endpoint(fullEndpoint)
.buildClient();
}
// 5) Send a simple chat completion request
logger.info("Sending chat completion request with prompt: {}", prompt);
ChatCompletions completions = client.complete(prompt);
// 6) Process the response
String content = completions.getChoice().getMessage().getContent();
logger.info("Received response from model");
System.out.println("\nResponse from AI assistant:\n" + content);
} catch (HttpResponseException e) {
// Handle API errors
int status = e.getResponse().getStatusCode();
logger.error("Service error {}: {}", status, e.getMessage());
if (status == 401 || status == 403) {
logger.error("Authentication failed. Check API key or Azure credentials.");
} else if (status == 404) {
logger.error("Deployment not found. Verify deployment name and endpoint.");
} else if (status == 429) {
logger.error("Rate limit exceeded. Please retry later.");
}
} catch (Exception e) {
// Handle all other exceptions
logger.error("Error in chat completion: {}", e.getMessage(), e);
}
}
}
```


Replace `YOUR-FOUNDRY-RESOURCE-NAME`

with your values:

```
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/openai/deployments/gpt-4o/chat/completions?api-version=2024-10-21' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json' \
-d '{
"messages": [
{"role": "system",
"content": "You are a helpful writing assistant"},
{"role": "user",
"content": "Write me a poem about flowers"}
],
"model": "gpt-4o"
}'
```


- In the chat playground, fill in the prompt and select
**Send**.
- The model returns a response in the
**Response** pane.

Create an agent and chat with it.

Substitute your endpoint for the `endpoint`

in this code:

```
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential
from azure.ai.agents.models import ListSortOrder, FilePurpose
project = AIProjectClient(
endpoint="https://your-foundry-resource-name.ai.azure.com/api/projects/project-name",
credential=DefaultAzureCredential(),
)
agent = project.agents.create_agent(
model="gpt-4o",
name="my-agent",
instructions="You are a helpful writing assistant")
thread = project.agents.threads.create()
message = project.agents.messages.create(
thread_id=thread.id,
role="user",
content="Write me a poem about flowers")
run = project.agents.runs.create_and_process(thread_id=thread.id, agent_id=agent.id)
if run.status == "failed":
# Check if you got "Rate limit is exceeded.", then you want to get more quota
print(f"Run failed: {run.last_error}")
# Get messages from the thread
messages = project.agents.messages.list(thread_id=thread.id)
# Get the last message from the sender
messages = project.agents.messages.list(thread_id=thread.id, order=ListSortOrder.ASCENDING)
for message in messages:
if message.run_id == run.id and message.text_messages:
print(f"{message.role}: {message.text_messages[-1].text.value}")
# Delete the agent once done
project.agents.delete_agent(agent.id)
print("Deleted agent")
```


```
using Azure;
using Azure.Identity;
using Azure.AI.Agents.Persistent;
// Creating the Client for agents
var projectEndpoint = System.Environment.GetEnvironmentVariable("AZURE_AI_ENDPOINT");
var modelDeploymentName = System.Environment.GetEnvironmentVariable("AZURE_AI_MODEL");
PersistentAgentsClient client = new(projectEndpoint, new DefaultAzureCredential());
// Create an Agent with toolResources and process Agent run
PersistentAgent agent = client.Administration.CreateAgent(
model: modelDeploymentName,
name: "SDK Test Agent - Tutor",
instructions: "You are a personal electronics tutor. Write and run code to answer questions.",
tools: new List<ToolDefinition> { new CodeInterpreterToolDefinition() });
// Create thread for communication
PersistentAgentThread thread = client.Threads.CreateThread();
// Create message to thread
PersistentThreadMessage messageResponse = client.Messages.CreateMessage(
thread.Id,
MessageRole.User,
"I need to solve the equation `3x + 11 = 14`. Can you help me?");
// Run the Agent
ThreadRun run = client.Runs.CreateRun(thread, agent);
// Wait for the run to complete
do
{
Thread.Sleep(TimeSpan.FromMilliseconds(500));
run = client.Runs.GetRun(thread.Id, run.Id);
}
while (run.Status == RunStatus.Queued
|| run.Status == RunStatus.InProgress);
Pageable<PersistentThreadMessage> messages = client.Messages.GetMessages(
threadId: thread.Id,
order: ListSortOrder.Ascending
);
// Print the messages in the thread
WriteMessages(messages);
// Delete the thread and agent after use
client.Threads.DeleteThread(thread.Id);
client.Administration.DeleteAgent(agent.Id);
// Temporary function to use a list of messages in the thread and write them to the console.
static void WriteMessages(IEnumerable<PersistentThreadMessage> messages)
{
foreach (PersistentThreadMessage threadMessage in messages)
{
Console.Write($"{threadMessage.CreatedAt:yyyy-MM-dd HH:mm:ss} - {threadMessage.Role,10}: ");
foreach (MessageContent contentItem in threadMessage.ContentItems)
{
if (contentItem is MessageTextContent textItem)
{
Console.Write(textItem.Text);
}
else if (contentItem is MessageImageFileContent imageFileItem)
{
Console.Write($"<image from ID: {imageFileItem.FileId}");
}
Console.WriteLine();
}
}
}
```


```
const endpoint = process.env.PROJECT_ENDPOINT as string;
const deployment = process.env.MODEL_DEPLOYMENT_NAME || 'gpt-4o';
const client = new AIProjectClient(endpoint, new DefaultAzureCredential());
// Create an Agent
const agent = await client.agents.createAgent(deployment, {
name: 'my-agent',
instructions: 'You are a helpful agent'
});
console.log(`\n==================== 🕵️ POEM AGENT ====================`);
// Create a thread and message
const thread = await client.agents.threads.create();
const prompt = 'Write me a poem about flowers';
console.log(`\n---------------- 📝 User Prompt ---------------- \n${prompt}`);
await client.agents.messages.create(thread.id, 'user', prompt);
// Create run
let run = await client.agents.runs.create(thread.id, agent.id);
// Wait for run to complete
console.log(`\n---------------- 🚦 Run Status ----------------`);
while (['queued', 'in_progress', 'requires_action'].includes(run.status)) {
// Avoid adding a lot of messages to the console
await new Promise((resolve) => setTimeout(resolve, 1000));
run = await client.agents.runs.get(thread.id, run.id);
console.log(`Run status: ${run.status}`);
}
console.log('\n---------------- 📊 Token Usage ----------------');
console.table([run.usage]);
const messagesIterator = await client.agents.messages.list(thread.id);
const assistantMessage = await getAssistantMessage(messagesIterator);
console.log('\n---------------- 💬 Response ----------------');
printAssistantMessage(assistantMessage);
// Clean up
console.log(`\n---------------- 🧹 Clean Up Poem Agent ----------------`);
await client.agents.deleteAgent(agent.id);
console.log(`Deleted Agent, Agent ID: ${agent.id}`);
```


```
package com.azure.ai.foundry.samples;
import com.azure.ai.agents.persistent.PersistentAgentsClient;
import com.azure.ai.agents.persistent.PersistentAgentsClientBuilder;
import com.azure.ai.agents.persistent.PersistentAgentsAdministrationClient;
import com.azure.ai.agents.persistent.models.CreateAgentOptions;
import com.azure.ai.agents.persistent.models.CreateThreadAndRunOptions;
import com.azure.ai.agents.persistent.models.PersistentAgent;
import com.azure.ai.agents.persistent.models.ThreadRun;
import com.azure.core.credential.TokenCredential;
import com.azure.core.exception.HttpResponseException;
import com.azure.core.util.logging.ClientLogger;
import com.azure.identity.DefaultAzureCredentialBuilder;
/**
* Sample demonstrating how to work with Azure AI Agents using the Azure AI Agents Persistent SDK.
*
* This sample shows how to:
* - Set up authentication with Azure credentials
* - Create a persistent agent with custom instructions
* - Start a thread and run with the agent
* - Access various properties of the agent and thread run
* - Work with the PersistentAgentsClient and PersistentAgentsAdministrationClient
*
* Environment variables:
* - AZURE_ENDPOINT: Optional fallback. The base endpoint for your Azure AI service if PROJECT_ENDPOINT is not provided.
* - PROJECT_ENDPOINT: Required. The endpoint for your Azure AI Project.
* - MODEL_DEPLOYMENT_NAME: Optional. The model deployment name (defaults to "gpt-4o").
* - AGENT_NAME: Optional. The name to give to the created agent (defaults to "java-quickstart-agent").
* - AGENT_INSTRUCTIONS: Optional. The instructions for the agent (defaults to a helpful assistant).
*
* Note: This sample requires proper Azure authentication. It uses DefaultAzureCredential which supports
* multiple authentication methods including environment variables, managed identities, and interactive login.
*
* SDK Features Demonstrated:
* - Using the Azure AI Agents Persistent SDK (com.azure:azure-ai-agents-persistent:1.0.0-beta.2)
* - Creating an authenticated client with DefaultAzureCredential
* - Using the PersistentAgentsClientBuilder pattern for client instantiation
* - Working with the PersistentAgentsAdministrationClient for agent management
* - Creating agents with specific configurations (name, model, instructions)
* - Starting threads and runs for agent conversations
* - Working with agent state and thread management
* - Accessing agent and thread run properties
* - Implementing proper error handling for Azure service interactions
*/
public class AgentSample {
private static final ClientLogger logger = new ClientLogger(AgentSample.class);
public static void main(String[] args) {
// Load environment variables with better error handling, supporting both .env and system environment variables
String endpoint = System.getenv("AZURE_ENDPOINT");
String projectEndpoint = System.getenv("PROJECT_ENDPOINT");
String modelName = System.getenv("MODEL_DEPLOYMENT_NAME");
String agentName = System.getenv("AGENT_NAME");
String instructions = System.getenv("AGENT_INSTRUCTIONS");
// Check for required endpoint configuration
if (projectEndpoint == null && endpoint == null) {
String errorMessage = "Environment variables not configured. Required: either PROJECT_ENDPOINT or AZURE_ENDPOINT must be set.";
logger.error("ERROR: {}", errorMessage);
logger.error("Please set your environment variables or create a .env file. See README.md for details.");
return;
}
// Use AZURE_ENDPOINT as fallback if PROJECT_ENDPOINT not set
if (projectEndpoint == null) {
projectEndpoint = endpoint;
logger.info("Using AZURE_ENDPOINT as PROJECT_ENDPOINT: {}", projectEndpoint);
}
// Set defaults for optional parameters with informative logging
if (modelName == null) {
modelName = "gpt-4o";
logger.info("No MODEL_DEPLOYMENT_NAME provided, using default: {}", modelName);
}
if (agentName == null) {
agentName = "java-quickstart-agent";
logger.info("No AGENT_NAME provided, using default: {}", agentName);
}
if (instructions == null) {
instructions = "You are a helpful assistant that provides clear and concise information.";
logger.info("No AGENT_INSTRUCTIONS provided, using default instructions");
}
// Create Azure credential with DefaultAzureCredentialBuilder
// This supports multiple authentication methods including environment variables,
// managed identities, and interactive browser login
logger.info("Building DefaultAzureCredential");
TokenCredential credential = new DefaultAzureCredentialBuilder().build();
try {
// Build the general agents client
logger.info("Creating PersistentAgentsClient with endpoint: {}", projectEndpoint);
PersistentAgentsClient agentsClient = new PersistentAgentsClientBuilder()
.endpoint(projectEndpoint)
.credential(credential)
.buildClient();
// Derive the administration client
logger.info("Getting PersistentAgentsAdministrationClient");
PersistentAgentsAdministrationClient adminClient =
agentsClient.getPersistentAgentsAdministrationClient();
// Create an agent
logger.info("Creating agent with name: {}, model: {}", agentName, modelName);
PersistentAgent agent = adminClient.createAgent(
new CreateAgentOptions(modelName)
.setName(agentName)
.setInstructions(instructions)
);
logger.info("Agent created: ID={}, Name={}", agent.getId(), agent.getName());
logger.info("Agent model: {}", agent.getModel());
// Start a thread/run on the general client
logger.info("Creating thread and run with agent ID: {}", agent.getId());
ThreadRun runResult = agentsClient.createThreadAndRun(
new CreateThreadAndRunOptions(agent.getId())
);
logger.info("ThreadRun created: ThreadId={}", runResult.getThreadId());
// List available getters on ThreadRun for informational purposes
logger.info("\nAvailable getters on ThreadRun:");
for (var method : ThreadRun.class.getMethods()) {
if (method.getName().startsWith("get")) {
logger.info(" - {}", method.getName());
}
}
logger.info("\nDemo completed successfully!");
} catch (HttpResponseException e) {
// Handle service-specific errors with detailed information
int statusCode = e.getResponse().getStatusCode();
logger.error("Service error {}: {}", statusCode, e.getMessage());
logger.error("Refer to the Azure AI Agents documentation for troubleshooting information.");
} catch (Exception e) {
// Handle general exceptions
logger.error("Error in agent sample: {}", e.getMessage(), e);
}
}
}
```


Replace `YOUR-FOUNDRY-RESOURCE-NAME`

and `YOUR-PROJECT-NAME`

with your values:

```
# Create agent
curl --request POST --url "https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/assistants?api-version=v1" \
-h "authorization: Bearer $AZURE_AI_AUTH_TOKEN" \
-h "content-type: application/json" \
-d '{
"model": "gpt-4o",
"name": "my-agent",
"instructions": "You are a helpful writing assistant"
}'
#Lets say agent ID created is asst_123456789. Use this to run the agent
# Create thread
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/threads?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json'
#Lets say thread ID created is thread_123456789. Use this in the next step
# Create message using thread ID
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/threads/thread_123456789/messages?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json' \
-d '{
"role": "user",
"content": "Write me a poem about flowers"
}'
# Run thread with the agent - use both agent id and thread id
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/threads/thread_123456789/runs?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json' \
--data '{
"assistant_id": "asst_123456789"
}'
# List the messages in the thread using thread ID
curl --request GET --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/threads/thread_123456789/messages?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json'
# Delete agent once done using agent id
curl --request DELETE --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/assistants/asst_123456789?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json'
```


When you're ready to try an agent, a default agent is created for you. To chat with this agent:

- In the left pane, select
**Playgrounds**.
- In the
**Agents playground** card, select **Let's go**.
- Add instructions, such as, "You are a helpful writing assistant."
- Start chatting with your agent, for example, "Write me a poem about flowers."

Agents have powerful capabilities through the use of tools. Let's add a file search tool that enables us to do knowledge retrieval.

Substitute your endpoint for the `endpoint`

in this code:

```
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential
from azure.ai.agents.models import ListSortOrder, FileSearchTool
project = AIProjectClient(
endpoint="https://your-foundry-resource-name.ai.azure.com/api/projects/project-name",
credential=DefaultAzureCredential(),
)
# Upload file and create vector store
file = project.agents.files.upload(file_path="./product_info_1.md", purpose=FilePurpose.AGENTS)
vector_store = project.agents.vector_stores.create_and_poll(file_ids=[file.id], name="my_vectorstore")
# Create file search tool and agent
file_search = FileSearchTool(vector_store_ids=[vector_store.id])
agent = project.agents.create_agent(
model="gpt-4o",
name="my-assistant",
instructions="You are a helpful assistant and can search information from uploaded files",
tools=file_search.definitions,
tool_resources=file_search.resources,
)
# Create thread and process user message
thread = project.agents.threads.create()
project.agents.messages.create(thread_id=thread.id, role="user", content="Hello, what Contoso products do you know?")
run = project.agents.runs.create_and_process(thread_id=thread.id, agent_id=agent.id)
# Handle run status
if run.status == "failed":
print(f"Run failed: {run.last_error}")
# Print thread messages
messages = project.agents.messages.list(thread_id=thread.id, order=ListSortOrder.ASCENDING)
for message in messages:
if message.run_id == run.id and message.text_messages:
print(f"{message.role}: {message.text_messages[-1].text.value}")
# Cleanup resources
project.agents.vector_stores.delete(vector_store.id)
project.agents.files.delete(file_id=file.id)
project.agents.delete_agent(agent.id)
```


```
using Azure;
using Azure.Identity;
using Azure.AI.Agents.Persistent;
// Creating the Client for agents and vector stores
var projectEndpoint = System.Environment.GetEnvironmentVariable("AZURE_AI_ENDPOINT");
var modelDeploymentName = System.Environment.GetEnvironmentVariable("AZURE_AI_MODEL");
PersistentAgentsClient client = new(projectEndpoint, new DefaultAzureCredential());
PersistentAgentFileInfo uploadedAgentFile = client.Files.UploadFile(
filePath: "product_info_1.md",
purpose: PersistentAgentFilePurpose.Agents);
// Create a vector store with the file and wait for it to be processed.
// If you do not specify a vector store, create_message will create a vector store with a default expiration policy of seven days after they were last active
Dictionary<string, string> fileIds = new()
{
{ uploadedAgentFile.Id, uploadedAgentFile.Filename }
};
PersistentAgentsVectorStore vectorStore = client.VectorStores.CreateVectorStore(
name: "my_vector_store");
// Add file ID to vector store.
VectorStoreFile vctFile = client.VectorStores.CreateVectorStoreFile(
vectorStoreId: vectorStore.Id,
fileId: uploadedAgentFile.Id
);
Console.WriteLine($"Added file to vector store. The id file in the vector store is {vctFile.Id}.");
FileSearchToolResource fileSearchToolResource = new FileSearchToolResource();
fileSearchToolResource.VectorStoreIds.Add(vectorStore.Id);
// Create an Agent with toolResources and process Agent run
PersistentAgent agent = client.Administration.CreateAgent(
model: modelDeploymentName,
name: "SDK Test Agent - Retrieval",
instructions: "You are a helpful agent that can help fetch data from files you know about.",
tools: new List<ToolDefinition> { new FileSearchToolDefinition() },
toolResources: new ToolResources() { FileSearch = fileSearchToolResource });
// Create thread for communication
PersistentAgentThread thread = client.Threads.CreateThread();
// Create message to thread
PersistentThreadMessage messageResponse = client.Messages.CreateMessage(
thread.Id,
MessageRole.User,
"Can you give me information on how to mount the product?");
// Run the Agent
ThreadRun run = client.Runs.CreateRun(thread, agent);
// Wait for the run to complete
// This is a blocking call, so it will wait until the run is completed
do
{
Thread.Sleep(TimeSpan.FromMilliseconds(500));
run = client.Runs.GetRun(thread.Id, run.Id);
}
while (run.Status == RunStatus.Queued
|| run.Status == RunStatus.InProgress);
// Create a list of messages in the thread and write them to the console.
Pageable<PersistentThreadMessage> messages = client.Messages.GetMessages(
threadId: thread.Id,
order: ListSortOrder.Ascending
);
WriteMessages(messages, fileIds);
// Delete the thread and agent after use
client.VectorStores.DeleteVectorStore(vectorStore.Id);
client.Files.DeleteFile(uploadedAgentFile.Id);
client.Threads.DeleteThread(thread.Id);
client.Administration.DeleteAgent(agent.Id);
// Helper method to write messages to the console
static void WriteMessages(IEnumerable<PersistentThreadMessage> messages, Dictionary<string, string> fileIds)
{
foreach (PersistentThreadMessage threadMessage in messages)
{
Console.Write($"{threadMessage.CreatedAt:yyyy-MM-dd HH:mm:ss} - {threadMessage.Role,10}: ");
foreach (MessageContent contentItem in threadMessage.ContentItems)
{
if (contentItem is MessageTextContent textItem)
{
if (threadMessage.Role == MessageRole.Agent && textItem.Annotations.Count > 0)
{
string strMessage = textItem.Text;
foreach (MessageTextAnnotation annotation in textItem.Annotations)
{
if (annotation is MessageTextFilePathAnnotation pathAnnotation)
{
strMessage = replaceReferences(fileIds, pathAnnotation.FileId, pathAnnotation.Text, strMessage);
}
else if (annotation is MessageTextFileCitationAnnotation citationAnnotation)
{
strMessage = replaceReferences(fileIds, citationAnnotation.FileId, citationAnnotation.Text, strMessage);
}
}
Console.Write(strMessage);
}
else
{
Console.Write(textItem.Text);
}
}
else if (contentItem is MessageImageFileContent imageFileItem)
{
Console.Write($"<image from ID: {imageFileItem.FileId}");
}
Console.WriteLine();
}
}
}
// Helper method to replace file references in the text
static string replaceReferences(Dictionary<string, string> fileIds, string fileID, string placeholder, string text)
{
if (fileIds.TryGetValue(fileID, out string replacement))
return text.Replace(placeholder, $" [{replacement}]");
else
return text.Replace(placeholder, $" [{fileID}]");
}
```


```
// Upload a file named product_info_1.md
console.log(`\n==================== 🕵️ FILE AGENT ====================`);
const __dirname = path.dirname(fileURLToPath(import.meta.url));
const filePath = path.join(__dirname, '../data/product_info_1.md');
const fileStream = fs.createReadStream(filePath);
fileStream.on('data', (chunk: string | Buffer) => {
console.log(`Read ${chunk.length} bytes of data.`);
});
const file = await client.agents.files.upload(fileStream, 'assistants', {
fileName: 'product_info_1.md'
});
console.log(`Uploaded file, ID: ${file.id}`);
const vectorStore = await client.agents.vectorStores.create({
fileIds: [file.id], // Associate the uploaded file with the vector store
name: 'my_vectorstore'
});
console.log('\n---------------- 🗃️ Vector Store Info ----------------');
console.table([
{
'Vector Store ID': vectorStore.id,
'Usage (bytes)': vectorStore.usageBytes,
'File Count': vectorStore.fileCounts?.total ?? 'N/A'
}
]);
// Create an Agent and a FileSearch tool
const fileSearchTool = ToolUtility.createFileSearchTool([vectorStore.id]);
const fileAgent = await client.agents.createAgent(deployment, {
name: 'my-file-agent',
instructions: 'You are a helpful assistant and can search information from uploaded files',
tools: [fileSearchTool.definition],
toolResources: fileSearchTool.resources
});
// Create a thread and message
const fileSearchThread = await client.agents.threads.create({ toolResources: fileSearchTool.resources });
const filePrompt = 'What are the steps to setup the TrailMaster X4 Tent?';
console.log(`\n---------------- 📝 User Prompt ---------------- \n${filePrompt}`);
await client.agents.messages.create(fileSearchThread.id, 'user', filePrompt);
// Create run
let fileSearchRun = await client.agents.runs.create(fileSearchThread.id, fileAgent.id).stream();
for await (const eventMessage of fileSearchRun) {
if (eventMessage.event === DoneEvent.Done) {
console.log(`Run completed: ${eventMessage.data}`);
}
if (eventMessage.event === ErrorEvent.Error) {
console.log(`An error occurred. ${eventMessage.data}`);
}
}
const fileSearchMessagesIterator = await client.agents.messages.list(fileSearchThread.id);
const fileAssistantMessage = await getAssistantMessage(fileSearchMessagesIterator);
console.log(`\n---------------- 💬 Response ---------------- \n`);
printAssistantMessage(fileAssistantMessage);
// Clean up
console.log(`\n---------------- 🧹 Clean Up File Agent ----------------`);
client.agents.vectorStores.delete(vectorStore.id);
client.agents.files.delete(file.id);
client.agents.deleteAgent(fileAgent.id);
console.log(`Deleted VectorStore, File, and FileAgent. FileAgent ID: ${fileAgent.id}`);
```


```
package com.azure.ai.foundry.samples;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import com.azure.ai.agents.persistent.PersistentAgentsClient;
import com.azure.ai.agents.persistent.PersistentAgentsClientBuilder;
import com.azure.ai.agents.persistent.PersistentAgentsAdministrationClient;
import com.azure.ai.agents.persistent.models.CreateAgentOptions;
import com.azure.ai.agents.persistent.models.CreateThreadAndRunOptions;
import com.azure.ai.agents.persistent.models.PersistentAgent;
import com.azure.ai.agents.persistent.models.ThreadRun;
import com.azure.core.exception.HttpResponseException;
import com.azure.core.util.logging.ClientLogger;
import com.azure.identity.DefaultAzureCredentialBuilder;
/**
* Sample demonstrating agent creation with document capabilities using Azure AI Agents Persistent SDK.
*
* This sample shows how to:
* - Set up authentication with Azure credentials
* - Create a temporary document file for demonstration purposes
* - Create a persistent agent with custom instructions for document search
* - Start a thread and run with the agent that can access document content
* - Work with file-based knowledge sources for agent interactions
*
* Environment variables:
* - AZURE_ENDPOINT: Optional fallback. The base endpoint for your Azure AI service if PROJECT_ENDPOINT is not provided.
* - PROJECT_ENDPOINT: Required. The endpoint for your Azure AI Project.
* - MODEL_DEPLOYMENT_NAME: Optional. The model deployment name (defaults to "gpt-4o").
* - AGENT_NAME: Optional. The name to give to the created agent (defaults to "java-file-search-agent").
* - AGENT_INSTRUCTIONS: Optional. The instructions for the agent (defaults to document-focused instructions).
*
* Note: This sample demonstrates the creation of an agent that can process document content.
* In a real-world scenario, you might want to integrate with Azure AI Search or similar services
* for more advanced document processing capabilities.
*
* SDK Features Demonstrated:
* - Using the Azure AI Agents Persistent SDK (com.azure:azure-ai-agents-persistent:1.0.0-beta.2)
* - Creating an authenticated client with DefaultAzureCredential
* - Using the PersistentAgentsClientBuilder for client instantiation
* - Working with the PersistentAgentsAdministrationClient for agent management
* - Creating temporary document files for agent access
* - Adding document knowledge sources to agents
* - Creating document-aware agents that can search and reference content
* - Starting threads and runs for document-based Q&A
* - Error handling for Azure service and file operations
*/
public class FileSearchAgentSample {
private static final ClientLogger logger = new ClientLogger(FileSearchAgentSample.class);
public static void main(String[] args) {
// Load environment variables with proper error handling
String endpoint = System.getenv("AZURE_ENDPOINT");
String projectEndpoint = System.getenv("PROJECT_ENDPOINT");
String modelName = System.getenv("MODEL_DEPLOYMENT_NAME");
String agentName = System.getenv("AGENT_NAME");
String instructions = System.getenv("AGENT_INSTRUCTIONS");
// Check for required endpoint configuration
if (projectEndpoint == null && endpoint == null) {
String errorMessage = "Environment variables not configured. Required: either PROJECT_ENDPOINT or AZURE_ENDPOINT must be set.";
logger.error("ERROR: {}", errorMessage);
logger.error("Please set your environment variables or create a .env file. See README.md for details.");
return;
}
// Set defaults for optional parameters
if (modelName == null) {
modelName = "gpt-4o";
logger.info("No MODEL_DEPLOYMENT_NAME provided, using default: {}", modelName);
}
if (agentName == null) {
agentName = "java-file-search-agent";
logger.info("No AGENT_NAME provided, using default: {}", agentName);
}
if (instructions == null) {
instructions = "You are a helpful assistant that can answer questions about documents.";
logger.info("No AGENT_INSTRUCTIONS provided, using default instructions: {}", instructions);
}
logger.info("Building DefaultAzureCredential");
var credential = new DefaultAzureCredentialBuilder().build();
// Use AZURE_ENDPOINT as fallback if PROJECT_ENDPOINT not set
String finalEndpoint = projectEndpoint != null ? projectEndpoint : endpoint;
logger.info("Using endpoint: {}", finalEndpoint);
try {
// Build the general agents client with proper error handling
logger.info("Creating PersistentAgentsClient with endpoint: {}", finalEndpoint);
PersistentAgentsClient agentsClient = new PersistentAgentsClientBuilder()
.endpoint(finalEndpoint)
.credential(credential)
.buildClient();
// Derive the administration client
logger.info("Getting PersistentAgentsAdministrationClient");
PersistentAgentsAdministrationClient adminClient =
agentsClient.getPersistentAgentsAdministrationClient();
// Create sample document for demonstration
Path tmpFile = createSampleDocument();
logger.info("Created sample document at: {}", tmpFile);
String filePreview = Files.readString(tmpFile).substring(0, 200) + "...";
logger.info("{}", filePreview);
// Create the agent with proper configuration
logger.info("Creating agent with name: {}, model: {}", agentName, modelName);
PersistentAgent agent = adminClient.createAgent(
new CreateAgentOptions(modelName)
.setName(agentName)
.setInstructions(instructions)
);
logger.info("Agent ID: {}", agent.getId());
logger.info("Agent model: {}", agent.getModel());
// Start a thread and run on the general client
logger.info("Creating thread and run with agent ID: {}", agent.getId());
ThreadRun threadRun = agentsClient.createThreadAndRun(
new CreateThreadAndRunOptions(agent.getId())
);
logger.info("ThreadRun ID: {}", threadRun.getThreadId());
// Display success message
logger.info("\nDemo completed successfully!");
} catch (HttpResponseException e) {
// Handle service-specific errors with detailed information
int statusCode = e.getResponse().getStatusCode();
logger.error("Service error {}: {}", statusCode, e.getMessage());
logger.error("Refer to the Azure AI Agents documentation for troubleshooting information.");
} catch (IOException e) {
// Handle IO exceptions specifically for file operations
logger.error("I/O error while creating sample document: {}", e.getMessage(), e);
} catch (Exception e) {
// Handle general exceptions
logger.error("Error in file search agent sample: {}", e.getMessage(), e);
}
}
/**
* Creates a sample markdown document with cloud computing information.
*
* This method demonstrates:
* - Creating a temporary file that will be automatically deleted when the JVM exits
* - Writing structured markdown content to the file
* - Logging file creation and preview of content
*
* In a real application, you might read existing files or create more complex documents.
* You could also upload them to a document storage service for persistent access.
*
* @return Path to the created temporary file
* @throws IOException if an I/O error occurs during file creation or writing
*/
private static Path createSampleDocument() throws IOException {
logger.info("Creating sample document");
String content = """
# Cloud Computing Overview
Cloud computing is the delivery of computing services over the internet, including servers, storage,
databases, networking, software, analytics, and intelligence. Cloud services offer faster innovation,
flexible resources, and economies of scale.
## Key Cloud Service Models
1. **Infrastructure as a Service (IaaS)** - Provides virtualized computing resources
2. **Platform as a Service (PaaS)** - Provides hardware and software tools over the internet
3. **Software as a Service (SaaS)** - Delivers software applications over the internet
## Major Cloud Providers
- Microsoft Azure
- Amazon Web Services (AWS)
- Google Cloud Platform (GCP)
- IBM Cloud
## Benefits of Cloud Computing
- Cost efficiency
- Scalability
- Reliability
- Performance
- Security
""";
Path tempFile = Files.createTempFile("cloud-doc", ".md");
Files.writeString(tempFile, content);
logger.info("Sample document created at: {}", tempFile);
return tempFile;
}
}
```


Replace `YOUR-FOUNDRY-RESOURCE-NAME`

and `YOUR-PROJECT-NAME`

with your values:

```
#Upload the file
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/files?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-f purpose="assistant" \
-f file="@product_info_1.md" #File object (not file name) to be uploaded.
#Lets say file ID created is assistant-123456789. Use this in the next step
# create vector store
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/vector_stores?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json' \
-d '{
"name": "my_vectorstore",
"file_ids": ["assistant-123456789"]
}'
#Lets say Vector Store ID created is vs_123456789. Use this in the next step
# Create Agent for File Search
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/assistants?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json' \
-d '{
"model": "gpt-4o",
"name": "my-assistant",
"instructions": "You are a helpful assistant and can search information from uploaded files",
"tools": [{"type": "file_search"}],
"tool_resources": {"file_search": {"vector_store_ids": ["vs_123456789"]}}
}'
#Lets say agent ID created is asst_123456789. Use this to run the agent
# Create thread
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/threads?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json'
#Lets say thread ID created is thread_123456789. Use this in the next step
# Create message using thread ID
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/threads/thread_123456789/messages?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json' \
-d '{
"role": "user",
"content": "Hello, what Contoso products do you know?"
}'
# Run thread with the agent - use both agent id and thread id
curl --request POST --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/threads/thread_123456789/runs?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json' \
--data '{
"assistant_id": "asst_123456789"
}'
# List the messages in the thread using thread ID
curl --request GET --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/threads/thread_123456789/messages?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json'
# Delete agent once done using agent id
curl --request DELETE --url 'https://YOUR-FOUNDRY-RESOURCE-NAME.services.ai.azure.com/api/projects/YOUR-PROJECT-NAME/assistants/asst_123456789?api-version=v1' \
-h 'authorization: Bearer $AZURE_AI_AUTH_TOKEN' \
-h 'content-type: application/json'
```


- In your agent's
**Setup** pane, scroll down if necessary to find **Knowledge**.
- Select
**Add**.
- Select
**Files** to upload the product_info_1.md file.
- Select
**Select local files** under **Add files**.
- Select
**Upload and save**.
- Change your agents instructions, such as, "You are a helpful assistant and can search information from uploaded files."
- Ask a question, such as, "Hello, what Contoso products do you know?"
- To add more files, select the
**...** on the AgentVectorStore, then select **Manage**.

If you no longer need any of the resources you created, delete the resource group associated with your project.
