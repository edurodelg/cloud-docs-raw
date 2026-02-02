---
merged_at: 2026-02-02T16:14:00.823040
merged_files: 4
---


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
