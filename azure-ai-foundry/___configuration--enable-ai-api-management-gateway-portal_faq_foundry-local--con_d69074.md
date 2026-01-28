---
merged_at: 2026-01-28T07:33:20.576800
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/configuration/enable-ai-api-management-gateway-portal -->

# Configure AI Gateway in your Foundry resources

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft Foundry integrates with AI Gateway to enable advanced management and governance capabilities. This integration uses Azure API Management behind the scenes.

AI Gateway enables:

- Multi-team token containment (prevent one project from monopolizing capacity).
- Cost control by capping aggregate usage.
- Compliance boundaries for regulated workloads (enforce predictable usage ceilings).
- Registration of
[custom agents for governance](../control-plane/register-custom-agent?view=foundry).

## Prerequisites

Azure subscription (

[create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)).Permissions to create or reuse an Azure API Management (APIM) instance:

- To create an APIM instance:
**Contributor**or**Owner**on the target resource group (or subscription). - To manage an existing APIM instance:
**API Management Service Contributor**(or**Owner**) on the APIM instance. For more information, see[How to use role-based access control in Azure API Management](/en-us/azure/api-management/api-management-role-based-access-control).

- To create an APIM instance:
Access to the Foundry portal (

**Admin console**) for the target Foundry resource.- For example:
**Azure AI Account Owner**or**Azure AI Owner**on the Foundry resource. For more information, see[Role-based access control for Microsoft Foundry](../concepts/rbac-foundry?view=foundry).

- For example:
Decision on whether to create a dedicated APIM instance or reuse an existing one.


## Understand AI Gateway scope

An AI Gateway sits between clients and Microsoft Foundry building blocks, including models or tools. All requests flow through the APIM instance once associated. Limits apply at the project level (each project can have its own TPM and quota settings).


## Choose API Management usage model

When you create a new AI Gateway, decide whether to:

- Create a new APIM instance.
- Use an existing APIM instance.

If you use an existing APIM instance, choose one that meets your organization's governance and networking requirements.

When you create a new instance from the Foundry portal flow, the SKU defaults to Basic v2.

Tip

AI Gateway in Azure API Management service is free for the first 100,000 API requests. For more information about costs and pricing for the API Management service, see [API Management Pricing](https://azure.microsoft.com/pricing/details/api-management/).

## Create an AI Gateway

Follow these steps in the Foundry portal to enable AI Gateway for a resource.

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. Select

**Operate**>**Admin console**.Open the

**AI Gateway**tab.Select

**Add AI Gateway**.Select the Foundry resource you want to connect with the gateway.

Select

**Create new**or**Use existing**APIM.Name the gateway, and select

**Add**to create or associate the APIM instance.Validate that the AI Gateway is listed now.

Once AI Gateway is configured for the Foundry resource, each project has its own configuration, including if they want to use AI Gateway or not. New projects created in the Foundry resource have AI Gateway enabled by default. However, existing projects must be enabled for AI Gateway.

To add existing projects to the AI Gateway, select the name of the AI Gateway you created. You see a list of all the projects in the Foundry resource with a column

**Gateway status**showing if the project has AI Gateway enabled or not. Locate your project and then select**Add project to gateway**. The column**Gateway status**shows**Enabled**.

## Governance scenarios

Once you configured AI Gateway for your resource and project, you can:

[Configure token limits for models](../control-plane/how-to-enforce-limits-models?view=foundry).[Add custom agents to Control Plane](../control-plane/register-custom-agent?view=foundry).- Govern MCP and A2A agent tools.

## Clean up resources

If you created a dedicated APIM instance for this purpose:

- Confirm that no other workloads depend on it.
- Disable the AI Gateway for all projects in the Foundry resource it's associated with.
- Remove linked resources in Azure portal.
- Delete the APIM instance with the same name as the AI gateway in Azure portal (if it isn't used for any other purpose).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/faq -->

# Microsoft Foundry (classic) frequently asked questions

FAQ for [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). If you can't find answers to your questions in this document, and still need help check the [Foundry Tools support options guide](../ai-services/cognitive-services-support-options?view=foundry-classic&context=/azure/ai-foundry/openai/context/context). Azure OpenAI is part of Foundry Tools.

## General questions

### Who is Microsoft Foundry (classic) intended for?

Microsoft Foundry (classic) is intended for AI software developers - including cloud architects and technical decision-makers who want to create generative AI applications and custom copilot experiences.

### How can customers access Microsoft Foundry (classic)?

Customers can explore Microsoft Foundry (classic) unauthenticated - including its cutting-edge AI capabilities. When you're ready to begin using templates, tools, and the robust model catalog to stitch together your own AI solutions, you're prompted to register or sign in to your Azure account. Currently, there's no extra charge for using Microsoft Foundry. When deploying solutions, you're billed for the Foundry Tools, Azure Machine Learning, and other Azure resources used inside of Microsoft Foundry (classic) at their existing rates.

### What regions is Microsoft Foundry (classic) available in?

Microsoft Foundry (classic) is available in most regions where Foundry Tools are available. For more information, see [region support for Microsoft Foundry](reference/region-support?view=foundry-classic).

### Can I integrate Microsoft Fabric data into Microsoft Foundry?

Yes. Microsoft Foundry (classic) supports seamless access to data in the Microsoft Fabric datastore Lakehouse without having to move or copy data. Data from Amazon S3 bucket can be accessed via Fabric shortcuts in Microsoft Foundry (classic) portal directly from Amazon S3 location without having to create a copy of the data in Azure.

### Can I use models other than ChatGPT in Microsoft Foundry (classic) portal?

Yes. Microsoft Foundry (classic) includes a robust and growing catalog of frontier and open-source models from OpenAI, Hugging Face, Meta, and more that can be applied over your data. You can even compare models by task using open-source datasets and evaluate the model with your own test data to see how the pretrained model would perform to fit your own use case.

### Will there be multiple varying model benchmarks in Microsoft Foundry (classic) portal based on individual projects and data sources?

In the model benchmarks view, customers can view varying model benchmarks published by Microsoft Foundry.

### Is prompt flow Microsoft's equivalent to LangChain?

Prompt flow is complementary to LangChain and Semantic Kernel and it can work with either. Prompt flow supports LLMOps for generative AI solutions, providing evaluation, connection management, and flow logic to help debug applications, manage deployment, and monitor at scale.

### How is prompt injection handled, and how do we ensure no malicious code is running from prompt injection?

Prompt templates in prompt flow provide robust examples and instructions for avoiding prompt injection attacks in the application. Azure AI Content Safety helps detect offensive or inappropriate content in text and images. Content moderation also checks for jailbreaks.

### What is the billing model for serverless API deployments?

Microsoft Foundry (classic) offers serverless API deployment models and hosted fine-tuning for [Llama 2 family models](how-to/deploy-models-llama?view=foundry-classic). Currently, there's no extra charge for Microsoft Foundry (classic) outside of typical Foundry Tools and other Azure resource charges.

### Can all models be secured with content filtering?

Azure AI Content Safety can be used for AI-generated content from Azure OpenAI in Microsoft Foundry (classic) Models, open-source, and frontier models. For more information, see [How Azure AI Content Safety helps protect users from the classroom to the chatroom](https://aka.ms/contentsafety_GA_blog).

### Do you use my company data to train any of the models?

Azure OpenAI doesn't use customer data to retrain models. For more information, see the [Azure OpenAI data, privacy, and security guide](/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy).

## Learning more and where to ask questions

### Where can I get training to get started learning and build my skills around Azure OpenAI?

Check out our [introduction to Azure OpenAI training course](/en-us/training/modules/explore-azure-openai/).

### Where can I post questions and see answers to other common questions?

- We recommend posting questions on
[Microsoft Q&A](/en-us/answers/tags/387/azure-openai) - Alternatively, you can post questions on
[Stack Overflow](https://stackoverflow.com/search?q=azure+openai)

### Where do I go for Foundry Tools customer support?

You can learn about all the support options for Foundry Tools in the [support and help options guide](../ai-services/cognitive-services-support-options?view=foundry-classic&context=/azure/cognitive-services/openai/context/context).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/concepts/foundry-local-architecture -->

# Foundry Local architecture

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Foundry Local provides efficient, secure, and scalable AI model inference directly on your device. This article explains the core components of Foundry Local and how they work together to deliver AI capabilities.

## Prerequisites

- Install Foundry Local. For setup steps, see
[Get started with Foundry Local](../get-started?view=foundry-classic). - Use a local terminal where the
`foundry`

CLI is available.

## Quick verification

Use the following quick checks to confirm the service is running and reachable.

- Get the service status and local endpoint:

```
foundry service status
```


This command prints the service status and the dynamically assigned local endpoint.

Reference: [Foundry Local CLI Reference](../reference/reference-cli?view=foundry-classic#service-commands)

- Call the local REST status endpoint:

```
curl http://localhost:PORT/openai/status
```


Replace `PORT`

with the port shown by `foundry service status`

. A successful response is JSON that includes `Endpoints`

, `ModelDirPath`

, and `PipeName`

.

Reference: [Foundry Local REST API Reference](../reference/reference-rest?view=foundry-classic#get-openaistatus)

Foundry Local offers these key benefits:

**Low latency**: Run models locally to minimize processing time and deliver faster results.**Data privacy**: Process sensitive data locally without sending it to the cloud for inference, helping meet data protection requirements.**Flexibility**: Support for diverse hardware configurations lets you choose the optimal setup for your needs.**Scalability**: Deploy across various devices, from laptops to servers, to suit different use cases.**Cost-effectiveness**: Reduce cloud computing costs, especially for high-volume applications.**Offline operation**: Work without an internet connection in remote or disconnected environments.**Seamless integration**: Easily incorporate into existing development workflows for smooth adoption.

Foundry Local can still use the network for operations like downloading models and execution providers. If you report a problem, you might choose to share logs (for example, by using `foundry zip-logs`

).

## Key components

The Foundry Local architecture consists of these main components:


### Foundry Local service

The Foundry Local Service includes an OpenAI-compatible REST server that provides a standard interface for working with the inference engine. You can also manage models over REST. Developers use this API to send requests, run models, and get results programmatically.

**Endpoint**: The endpoint is*dynamically allocated*when the service starts. Find it by running the`foundry service status`

command, or by calling`GET /openai/status`

. When using Foundry Local in your applications, use an integration SDK that automatically handles endpoint discovery. For more details, see[Integrate with inference SDKs](../how-to/how-to-integrate-with-inference-sdks?view=foundry-classic)and the[Foundry Local REST API Reference](../reference/reference-rest?view=foundry-classic).**Use Cases**:- Connect Foundry Local to your custom applications
- Execute models through HTTP requests


### ONNX runtime

The ONNX Runtime is a core component that executes AI models. It runs optimized ONNX models efficiently on local hardware like CPUs, GPUs, or NPUs.

**Features**:

- Works with multiple hardware providers (NVIDIA, AMD, Intel, Qualcomm) and device types (NPUs, CPUs, GPUs)
- Offers a consistent interface for running models across different hardware
- Delivers high performance
- Supports quantized models for faster inference

### Model management

Foundry Local provides robust tools for managing AI models, ensuring that they're readily available for inference and easy to maintain. You handle model management through the **Model Cache** and the **Command-Line Interface (CLI)**.

#### Model cache

The model cache stores downloaded AI models locally on your device, which ensures models are ready for inference without needing to download them repeatedly. You can manage the cache by using either the Foundry CLI or REST API.

**Purpose**: Speeds up inference by keeping models locally available**Key Commands**:`foundry cache list`

: Shows all models in your local cache`foundry cache remove <model-name>`

: Removes a specific model from the cache`foundry cache cd <path>`

: Changes the storage location for cached models


#### Model lifecycle

**Download**: Download models from the Foundry model catalog and save them to your local disk.**Load**: Load models into the Foundry Local service memory for inference. Set a TTL (time-to-live) to control how long the model stays in memory (default: 600 seconds).**Run**: Execute model inference for your requests.**Unload**: Remove models from memory to free up resources when no longer needed.**Delete**: Remove models from your local cache to reclaim disk space.

#### Model compilation using Olive

Before you can use models with Microsoft Foundry Local, you must compile and optimize them in the [ONNX](https://onnx.ai) format. Microsoft provides a selection of published models in the Foundry model catalog that are already optimized for Foundry Local. However, you aren't limited to those models - by using [Olive](https://microsoft.github.io/Olive/). Olive is a powerful framework for preparing AI models for efficient inference. It converts models into the ONNX format, optimizes their graph structure, and applies techniques like quantization to improve performance on local hardware.

Tip

To learn more about compiling models for Foundry Local, see [How to compile Hugging Face models to run on Foundry Local](../how-to/how-to-compile-hugging-face-models?view=foundry-classic).

### Hardware abstraction layer

The hardware abstraction layer ensures that Foundry Local runs on various devices by abstracting the underlying hardware. To optimize performance based on the available hardware, Foundry Local supports:

**multiple**, such as NVIDIA CUDA, AMD, Qualcomm, Intel.*execution providers***multiple**, such as CPU, GPU, NPU.*device types*

Note

For Intel NPU support on Windows, install the [Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html) to enable hardware acceleration.

Note

For Qualcomm NPU support, install the [Qualcomm NPU driver](https://softwarecenter.qualcomm.com/catalog/item/QHND). If you encounter the error `Qnn error code 5005: "Failed to load from EpContext model. qnn_backend_manager."`

, this error typically indicates an outdated driver or NPU resource conflicts. Try rebooting to clear NPU resource conflicts, especially after using Windows Copilot+ features.

### Developer experiences

The Foundry Local architecture is designed to provide a seamless developer experience, enabling easy integration and interaction with AI models. Developers can choose from various interfaces to interact with the system, including:

#### Command-Line Interface (CLI)

The Foundry CLI is a powerful tool for managing models, the inference engine, and the local cache.

**Examples**:

`foundry model list`

: Lists all available models in the local cache.`foundry model run <model-name>`

: Runs a model.`foundry service status`

: Checks the status of the service.

Tip

To learn more about the CLI commands, read [Foundry Local CLI Reference](../reference/reference-cli?view=foundry-classic).

#### Inferencing SDK integration

Foundry Local supports integration with various SDKs in most languages, such as the OpenAI SDK, enabling developers to use familiar programming interfaces to interact with the local inference engine.

Tip

To learn more about integrating with inferencing SDKs, read [Integrate inferencing SDKs with Foundry Local](../how-to/how-to-integrate-with-inference-sdks?view=foundry-classic).

#### AI Toolkit for Visual Studio Code

The AI Toolkit for Visual Studio Code provides a user-friendly interface for developers to interact with Foundry Local. It allows users to run models, manage the local cache, and visualize results directly within the IDE.

**Features**:

- Model management: Download, load, and run models from within the IDE.
- Interactive console: Send requests and view responses in real-time.
- Visualization tools: Graphical representation of model performance and results.

**Prerequisites:**

- You have installed
[Foundry Local](../get-started?view=foundry-classic)and have a model service running. - You have installed the
[AI Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-windows-ai-studio.windows-ai-studio)extension.

**Connect a Foundry Local model to AI Toolkit:**

**Add model in AI Toolkit**: Open AI Toolkit from the activity bar of Visual Studio Code. In the 'My Models' panel, select the 'Add model for remote interface' button and then select 'Add a custom model' from the dropdown menu.**Enter the chat-compatible endpoint URL**: Enter`http://localhost:PORT/v1/chat/completions`

, where`PORT`

is the port number of your Foundry Local endpoint. Find the port by running`foundry service status`

. Foundry Local dynamically assigns a port, so it might not always be the same.**Provide the model name**: Enter the exact model name you want to use, for example`phi-3.5-mini`

. List downloaded and cached models with`foundry cache list`

, or use`foundry model list`

to see models available for local use. You'll also be asked to enter a display name, which is only for your local use. To avoid confusion, use the same value as the model name.**Authentication**: If your local setup doesn't require authentication, leave the authentication headers field blank.

After completing these steps, your Foundry Local model appears in the **My Models** list in AI Toolkit. To start using it, right-click the model and select **Load in Playground**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-models/tutorials/get-started-deepseek-r1 -->

# Tutorial: Get started with DeepSeek-R1 reasoning model in Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

In this tutorial, you learn how to deploy and use a DeepSeek reasoning model in Microsoft Foundry. This tutorial uses [DeepSeek-R1](https://ai.azure.com/explore/models/deepseek-r1/version/1/registry/azureml-deepseek?cid=learnDocs) for illustration. However, the content also applies to the newer [DeepSeek-R1-0528](https://ai.azure.com/explore/models/deepseek-r1-0528/version/1/registry/azureml-deepseek?cid=learnDocs) reasoning model.

**What you'll accomplish:**

In this tutorial, you'll deploy the DeepSeek-R1 reasoning model, send inference requests programmatically using code, and parse the reasoning output to understand how the model arrives at its answers.

The steps you perform in this tutorial are:

- Create and configure the Azure resources to use DeepSeek-R1 in Foundry Models.
- Configure the model deployment.
- Use DeepSeek-R1 with the next generation v1 Azure OpenAI APIs to consume the model in code.

## Prerequisites

To complete this article, you need:

An Azure subscription with a valid payment method. If you don't have an Azure subscription, create a

[paid Azure account](https://azure.microsoft.com/pricing/purchase-options/pay-as-you-go)to begin. If you're using[GitHub Models](https://docs.github.com/en/github-models/), you can[upgrade from GitHub Models to Microsoft Foundry Models](../how-to/quickstart-github-models?view=foundry-classic)and create an Azure subscription in the process.Access to Microsoft Foundry with appropriate permissions to create and manage resources. Typically requires Contributor or Owner role on the resource group for creating resources and deploying models.

Install the Azure OpenAI SDK for your programming language:

**Python**:`pip install openai azure-identity`

**.NET**:`dotnet add package Azure.Identity`

and install the OpenAI package**JavaScript**:`npm install openai @azure/identity`

**Java**: Add the Azure Identity package (see code examples for details)


DeepSeek-R1 is a reasoning model that generates explanations alongside answers—see [About reasoning models](#about-reasoning-models) for details.

## Create the resources

To create a Foundry project that supports deployment for DeepSeek-R1, follow these steps. You can also create the resources using [Azure CLI](../how-to/quickstart-create-resources?view=foundry-classic&pivots=programming-language-cli) or [infrastructure as code, with Bicep](../how-to/quickstart-create-resources?view=foundry-classic&pivots=programming-language-bicep).

Tip

Because you can [customize the left pane](../../what-is-foundry?view=foundry-classic#customize-the-left-pane) in the Microsoft Foundry portal, you might see different items than shown in these steps. If you don't see what you're looking for, select **... More** at the bottom of the left pane.

Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**.On the landing page, go to the "Explore models and capabilities" section.

Use the search box on the screen to search for the

**DeepSeek-R1**model and open its model card.Select

**Use this model**. This action opens a wizard to create a Foundry project and resources for you to work in. You can keep the default name for the project or change it.Tip

**Are you using Azure OpenAI in Foundry Models?**When you're connected to the Foundry portal using an Azure OpenAI resource, only Azure OpenAI models show up in the catalog. To view the full list of models, including DeepSeek-R1, use the top**Announcements**section and locate the card with the option**Explore more models**.A new window opens with the full list of models. Select

**DeepSeek-R1**from the list and select**Deploy**. The wizard asks to create a new project.Select the dropdown in the "Advanced options" section of the wizard to see details about settings and other defaults created alongside the project. These defaults are selected for optimal functionality and include:

Property Description Resource group The main container for all the resources in Azure. This container helps you organize resources that work together. It also helps you have a scope for the costs associated with the entire project. Region The region of the resources that you're creating. Foundry resource The resource enabling access to the flagship models in the Foundry model catalog. In this tutorial, a new account is created, but Foundry resources (formerly known as Azure AI Services resource) can be shared across multiple hubs and projects. Hubs use a connection to the resource to have access to the model deployments available there. To learn how you can create connections to Foundry resources to consume models, see [Connect your AI project](../../model-inference/how-to/configure-project-connection?view=foundry-classic).Select

**Create**to create the Foundry project alongside the other defaults. Wait until the project creation is complete. This process takes a few minutes.

- Sign in to
[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. - The project you're working on appears in the upper-left corner.
- To create a new project, select the project name, then
**Create new project**. - Give your project a name and select
**Create project**.

## Deploy the model

When you create the project and resources, a deployment wizard opens. DeepSeek-R1 is available as a Foundry Model sold directly by Azure. You can review the pricing details for the model by selecting the DeepSeek tab on the

[Foundry Models pricing page](https://azure.microsoft.com/pricing/details/ai-foundry-models/deepseek/).Configure the deployment settings. By default, the deployment receives the name of the model you're deploying. The deployment name is used in the

`model`

parameter for requests to route to this particular model deployment. This setup lets you configure specific names for your models when you attach specific configurations.Foundry automatically selects the Foundry resource you created earlier with your project. Use the

**Customize**option to change the connection based on your needs. DeepSeek-R1 is currently available under the**Global Standard**deployment type, which provides higher throughput and performance.Select

**Deploy**.When the deployment finishes, the deployment

**Details**page opens. Now the new model is ready for use.

- Add a model to your project. Select
**Build**in the middle of the page, then**Model**. - Select
**Deploy base model**to open the model catalog. - Find and select the
**DeepSeek-R1**model tile to open its model card and select**Deploy**. You can select**Quick deploy**to use the defaults, or select**Customize deployment**to see and change the deployment settings.

When the deployment finishes, you land on its playground, where you can start to interact with the deployment.

If you prefer to explore the model interactively first, skip to [Use the model in the playground](#use-the-model-in-the-playground).

## Use the model in code

Use the Foundry Models endpoint and credentials to connect to the model.

- Select the
**Details**pane from the upper pane of the Playgrounds to see the deployment's details. Here, you can find the deployment's URI and API key. - Get your resource name from the deployment's URI to use for inferencing the model via code.

Use the next generation v1 Azure OpenAI APIs to consume the model in your code. These code examples use a secure, keyless authentication approach, Microsoft Entra ID, via the [Azure Identity library](/en-us/dotnet/api/overview/azure/identity-readme?view=azure-dotnet&preserve-view=true).

The following code examples demonstrate how to:

Authenticate with Microsoft Entra ID using

`DefaultAzureCredential`

, which automatically attempts multiple authentication methods in sequence:**Environment variables**- Checks for service principal credentials in environment variables**Managed identity**- Uses managed identity if running in Azure (App Service, Functions, VM, etc.)**Azure CLI**- Falls back to Azure CLI credentials if you're authenticated locally**Other methods**- Continues through additional authentication methods as needed

Tip

For local development, ensure you're authenticated with Azure CLI by running

`az login`

. For production deployments in Azure, configure managed identity for your application.Create a chat completion client connected to your model deployment

Send a basic prompt to the DeepSeek-R1 model

Receive and display the response


**Expected output:** A JSON response containing the model's answer, reasoning process (within `<think>`

tags), token usage statistics (prompt tokens, completion tokens, total tokens), and model information.

Install the package `openai`

using your package manager, like pip:

```
pip install --upgrade openai
```


The following example shows how to create a client to consume chat completions and then generate and print out the response:

```
from openai import OpenAI
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
token_provider = get_bearer_token_provider(
DefaultAzureCredential(), "https://cognitiveservices.azure.com/.default"
)
client = OpenAI(
base_url = "https://YOUR-RESOURCE-NAME.openai.azure.com/openai/v1/",
api_key=token_provider,
)
response = client.chat.completions.create(
model="DeepSeek-R1", # Replace with your model deployment name.
messages=[
{"role": "system", "content": "You are a helpful assistant."},
{"role": "user", "content": "How many languages are in the world?"}
]
)
#print(response.choices[0].message)
print(response.model_dump_json(indent=2))
```


**API Reference:**

[OpenAI Python client](https://github.com/openai/openai-python)[OpenAI JavaScript client](https://github.com/openai/openai-node)[OpenAI .NET client](https://github.com/openai/openai-dotnet)[DefaultAzureCredential class](/en-us/dotnet/api/azure.identity.defaultazurecredential)[Chat completions API reference](../../openai/latest?view=foundry-classic#create-chat-completion)[Azure Identity library overview](/en-us/dotnet/api/overview/azure/identity-readme)

Reasoning might generate longer responses and consume a larger number of tokens. See the [rate limits](../../model-inference/quotas-limits?view=foundry-classic) that apply to DeepSeek-R1 models. Consider having a retry strategy to handle rate limits. You can also [request increases to the default limits](../quotas-limits?view=foundry-classic#request-increases-to-the-default-limits).

## About reasoning models

Reasoning models can reach higher levels of performance in domains like math, coding, science, strategy, and logistics. The way these models produce outputs is by explicitly using chain of thought to explore all possible paths before generating an answer. They verify their answers as they produce them, which helps to arrive at more accurate conclusions. As a result, reasoning models might require less context prompts in order to produce effective results.

Reasoning models produce two types of content as outputs:

- Reasoning completions
- Output completions

Both of these completions count towards content generated from the model. Therefore, they contribute to the token limits and costs associated with the model. Some models, like `DeepSeek-R1`

, might respond with the reasoning content. Others, like `o1`

, output only the completions.

### Reasoning content

Some reasoning models, like DeepSeek-R1, generate completions and include the reasoning behind them. The reasoning associated with the completion is included in the response's content within the tags `<think>`

and `</think>`

. The model can select the scenarios for which to generate reasoning content. The following example shows how to generate the reasoning content, using Python:

```
import re
match = re.match(r"<think>(.*?)</think>(.*)", response.choices[0].message.content, re.DOTALL)
print("Response:", )
if match:
print("\tThinking:", match.group(1))
print("\tAnswer:", match.group(2))
else:
print("\tAnswer:", response.choices[0].message.content)
print("Model:", response.model)
print("Usage:")
print("\tPrompt tokens:", response.usage.prompt_tokens)
print("\tTotal tokens:", response.usage.total_tokens)
print("\tCompletion tokens:", response.usage.completion_tokens)
```


```
Thinking: Okay, the user is asking how many languages exist in the world. I need to provide a clear and accurate answer. Let's start by recalling the general consensus from linguistic sources. I remember that the number often cited is around 7,000, but maybe I should check some reputable organizations.\n\nEthnologue is a well-known resource for language data, and I think they list about 7,000 languages. But wait, do they update their numbers? It might be around 7,100 or so. Also, the exact count can vary because some sources might categorize dialects differently or have more recent data. \n\nAnother thing to consider is language endangerment. Many languages are endangered, with some having only a few speakers left. Organizations like UNESCO track endangered languages, so mentioning that adds context. Also, the distribution isn't even. Some countries have hundreds of languages, like Papua New Guinea with over 800, while others have just a few. \n\nA user might also wonder why the exact number is hard to pin down. It's because the distinction between a language and a dialect can be political or cultural. For example, Mandarin and Cantonese are considered dialects of Chinese by some, but they're mutually unintelligible, so others classify them as separate languages. Also, some regions are under-researched, making it hard to document all languages. \n\nI should also touch on language families. The 7,000 languages are grouped into families like Indo-European, Sino-Tibetan, Niger-Congo, etc. Maybe mention a few of the largest families. But wait, the question is just about the count, not the families. Still, it's good to provide a bit more context. \n\nI need to make sure the information is up-to-date. Let me think – recent estimates still hover around 7,000. However, languages are dying out rapidly, so the number decreases over time. Including that note about endangerment and language extinction rates could be helpful. For instance, it's often stated that a language dies every few weeks. \n\nAnother point is sign languages. Does the count include them? Ethnologue includes some, but not all sources might. If the user is including sign languages, that adds more to the count, but I think the 7,000 figure typically refers to spoken languages. For thoroughness, maybe mention that there are also over 300 sign languages. \n\nSummarizing, the answer should state around 7,000, mention Ethnologue's figure, explain why the exact number varies, touch on endangerment, and possibly note sign languages as a separate category. Also, a brief mention of Papua New Guinea as the most linguistically diverse country. \n\nWait, let me verify Ethnologue's current number. As of their latest edition (25th, 2022), they list 7,168 living languages. But I should check if that's the case. Some sources might round to 7,000. Also, SIL International publishes Ethnologue, so citing them as reference makes sense. \n\nOther sources, like Glottolog, might have a different count because they use different criteria. Glottolog might list around 7,000 as well, but exact numbers vary. It's important to highlight that the count isn't exact because of differing definitions and ongoing research. \n\nIn conclusion, the approximate number is 7,000, with Ethnologue being a key source, considerations of endangerment, and the challenges in counting due to dialect vs. language distinctions. I should make sure the answer is clear, acknowledges the variability, and provides key points succinctly.
Answer: The exact number of languages in the world is challenging to determine due to differences in definitions (e.g., distinguishing languages from dialects) and ongoing documentation efforts. However, widely cited estimates suggest there are approximately **7,000 languages** globally.
Model: DeepSeek-R1
Usage:
Prompt tokens: 11
Total tokens: 897
Completion tokens: 886
```


**API Reference:**

### Prompt reasoning models

When building prompts for reasoning models, take the following into consideration:

- Use simple instructions and avoid using chain-of-thought techniques.
- Built-in reasoning capabilities make simple zero-shot prompts as effective as more complex methods.
- When providing additional context or documents, like in RAG scenarios, including only the most relevant information might help prevent the model from over-complicating its response.
- Reasoning models may support the use of system messages. However, they might not follow them as strictly as other non-reasoning models.
- When creating multi-turn applications, consider appending only the final answer from the model, without it's reasoning content, as explained in the
[Reasoning content](#reasoning-content)section.

Notice that reasoning models can take longer times to generate responses. They use long reasoning chains of thought that enable deeper and more structured problem-solving. They also perform self-verification to cross-check their answers and correct their mistakes, thereby showcasing emergent self-reflective behaviors.

### Parameters

Reasoning models support a subset of the standard chat completion parameters to maintain the integrity of their reasoning process.

**Supported parameters:**

`max_tokens`

- Maximum number of tokens to generate in the response`stop`

- Sequences where the API stops generating tokens`stream`

- Enable streaming responses`n`

- Number of completions to generate`frequency_penalty`

- Reduces repetition of token sequences

**Unsupported parameters** (reasoning models don't support these):

`temperature`

- Fixed to optimize reasoning quality`top_p`

- Not configurable for reasoning models`presence_penalty`

- Not available`repetition_penalty`

- Use`frequency_penalty`

instead

**Example using max_tokens:**

```
response = client.chat.completions.create(
model="DeepSeek-R1",
messages=[
{"role": "user", "content": "Explain quantum computing"}
],
max_tokens=1000 # Limit response length
)
```


For the complete list of supported parameters, see the [Chat completions API reference](../../openai/latest?view=foundry-classic#create-chat-completion).

## Use the model in the playground

Use the model in the playground to get an idea of the model's capabilities.

On the deployment details page, select

**Open in playground**in the top bar. This action opens the chat playground.In the

**Deployment**drop down of the chat playground, the deployment you created is already automatically selected.Configure the system prompt as needed.

Enter your prompt and see the outputs.

Select

**View code**to see details about how to access the model deployment programmatically.

As stated previously, immediately a model deployment is complete, you land on the model's playground, where you can start to interact with the deployment. For example, you can enter your prompts, such as "How many languages are in the world?" in the playground.

## What you learned

In this tutorial, you accomplished the following:

- Created Foundry resources for hosting AI models
- Deployed the DeepSeek-R1 reasoning model
- Made authenticated API calls using Microsoft Entra ID
- Sent inference requests and received reasoning outputs
- Parsed reasoning content from model responses to understand the model's thought process
