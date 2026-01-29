---
merged_at: 2026-01-29T15:40:29.813393
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/prompt-flow-tools/embedding-tool -->

# Embedding tool for flows in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

The prompt flow Embedding tool enables you to convert text into dense vector representations for various natural language processing tasks.

Tip

For chat and completion tools, learn more about the large language model [(LLM) tool](llm-tool?view=foundry-classic).

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

## Build with the Embedding tool

Create or open a flow in

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). For more information, see[Create a flow](../flow-develop?view=foundry-classic).Select

**+ More tools**>**Embedding**to add the Embedding tool to your flow.Select the connection to one of your provisioned resources. For example, select

**Default_AzureOpenAI**.Enter values for the Embedding tool input parameters described in the

[Inputs table](#inputs).Add more tools to your flow, as needed. Or select

**Run**to run the flow.The outputs are described in the

[Outputs table](#outputs).

## Inputs

The following input parameters are available.

| Name | Type | Description | Required |
|---|---|---|---|
| input | string | The input text to embed. | Yes |
| model, deployment_name | string | The instance of the text-embedding engine to use. | Yes |

## Outputs

The output is a list of vector representations for the input text. For example:

```
[
0.123,
0.456,
0.789
]
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/prompt-flow-tools/prompt-tool -->

# Prompt tool for flows in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

The prompt flow Prompt tool offers a collection of textual templates that serve as a starting point for creating prompts. These templates, based on the [Jinja](https://jinja.palletsprojects.com/en/stable/) template engine, facilitate the definition of prompts. The tool proves useful when prompt tuning is required before the prompts are fed into the large language model (LLM) in the prompt flow.

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

Prepare a prompt. The [LLM tool](llm-tool?view=foundry-classic) and Prompt tool both support [Jinja](https://jinja.palletsprojects.com/en/stable/) templates.

In this example, the prompt incorporates Jinja templating syntax to dynamically generate the welcome message and personalize it based on the user's name. It also presents a menu of options for the user to choose from. Depending on whether the `user_name`

variable is provided, it either addresses the user by name or uses a generic greeting.

```
Welcome to {{ website_name }}!
{% if user_name %}
Hello, {{ user_name }}!
{% else %}
Hello there!
{% endif %}
Please select an option from the menu below:
1. View your account
2. Update personal information
3. Browse available products
4. Contact customer support
```


For more information and best practices, see [Prompt engineering techniques](../../openai/concepts/advanced-prompt-engineering?view=foundry-classic).

## Build with the Prompt tool

Create or open a flow in

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). For more information, see[Create a flow](../flow-develop?view=foundry-classic).Select

**+ Prompt**to add the Prompt tool to your flow.Enter values for the Prompt tool input parameters described in the

[Inputs table](#inputs). For information about how to prepare the prompt input, see[Prerequisites](#prerequisites).Add more tools (such as the

[LLM tool](llm-tool?view=foundry-classic)) to your flow, as needed. Or select**Run**to run the flow.The outputs are described in the

[Outputs table](#outputs).

## Inputs

The following input parameters are available.

| Name | Type | Description | Required |
|---|---|---|---|
| prompt | string | The prompt template in Jinja. | Yes |
| Inputs | - | The list of variables of a prompt template and its assignments. | - |

## Outputs

### Example 1

Inputs:

| Variable | Type | Sample value |
|---|---|---|
| website_name | string | "Microsoft" |
| user_name | string | "Jane" |

Outputs:

```
Welcome to Microsoft! Hello, Jane! Please select an option from the menu below: 1. View your account 2. Update personal information 3. Browse available products 4. Contact customer support
```


### Example 2

Inputs:

| Variable | Type | Sample value |
|---|---|---|
| website_name | string | "Bing" |
| user_name | string | " |

Outputs:

```
Welcome to Bing! Hello there! Please select an option from the menu below: 1. View your account 2. Update personal information 3. Browse available products 4. Contact customer support
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/prompt-flow-tools/llm-tool -->

# LLM tool for flows in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

To use large language models (LLMs) for natural language processing, you use the prompt flow LLM tool.

Tip

For embeddings to convert text into dense vector representations for various natural language processing tasks, see [Embedding tool](embedding-tool?view=foundry-classic).

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

Prepare a prompt as described in the [Prompt tool](prompt-tool?view=foundry-classic#prerequisites) documentation. The LLM tool and Prompt tool both support [Jinja](https://jinja.palletsprojects.com/en/stable/) templates. For more information and best practices, see [Prompt engineering techniques](../../openai/concepts/advanced-prompt-engineering?view=foundry-classic).

## Build with the LLM tool

Create or open a flow in

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). For more information, see[Create a flow](../flow-develop?view=foundry-classic).Select

**+ LLM**to add the LLM tool to your flow.Select the connection to one of your provisioned resources. For example, select

**Default_AzureOpenAI**.From the

**Api**dropdown list, select**chat**or**completion**.Enter values for the LLM tool input parameters described in the

[Text completion inputs table](#inputs). If you selected the**chat**API, see the[Chat inputs table](#chat-inputs). If you selected the**completion**API, see the[Text completion inputs table](#text-completion-inputs). For information about how to prepare the prompt input, see[Prerequisites](#prerequisites).Add more tools to your flow, as needed. Or select

**Run**to run the flow.The outputs are described in the

[Outputs table](#outputs).

## Inputs

The following input parameters are available.

### Text completion inputs

| Name | Type | Description | Required |
|---|---|---|---|
| prompt | string | Text prompt for the language model. | Yes |
| model, deployment_name | string | The language model to use. | Yes |
| max_tokens | integer | The maximum number of tokens to generate in the completion. Default is 16. | No |
| temperature | float | The randomness of the generated text. Default is 1. | No |
| stop | list | The stopping sequence for the generated text. Default is null. | No |
| suffix | string | The text appended to the end of the completion. | No |
| top_p | float | The probability of using the top choice from the generated tokens. Default is 1. | No |
| logprobs | integer | The number of log probabilities to generate. Default is null. | No |
| echo | boolean | The value that indicates whether to echo back the prompt in the response. Default is false. | No |
| presence_penalty | float | The value that controls the model's behavior regarding repeating phrases. Default is 0. | No |
| frequency_penalty | float | The value that controls the model's behavior regarding generating rare phrases. Default is 0. | No |
| best_of | integer | The number of best completions to generate. Default is 1. | No |
| logit_bias | dictionary | The logit bias for the language model. Default is empty dictionary. | No |

### Chat inputs

| Name | Type | Description | Required |
|---|---|---|---|
| prompt | string | The text prompt that the language model should reply to. | Yes |
| model, deployment_name | string | The language model to use. | Yes |
| max_tokens | integer | The maximum number of tokens to generate in the response. Default is inf. | No |
| temperature | float | The randomness of the generated text. Default is 1. | No |
| stop | list | The stopping sequence for the generated text. Default is null. | No |
| top_p | float | The probability of using the top choice from the generated tokens. Default is 1. | No |
| presence_penalty | float | The value that controls the model's behavior regarding repeating phrases. Default is 0. | No |
| frequency_penalty | float | The value that controls the model's behavior regarding generating rare phrases. Default is 0. | No |
| logit_bias | dictionary | The logit bias for the language model. Default is empty dictionary. | No |

## Outputs

The output varies depending on the API you selected for inputs.

| API | Return type | Description |
|---|---|---|
| Completion | string | The text of one predicted completion. |
| Chat | string | The text of one response of conversation. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/prompt-flow-tools/python-tool -->

# Python tool for flows in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

The prompt flow Python tool offers customized code snippets as self-contained executable nodes. You can quickly create Python tools, edit code, and verify results.

## Prerequisites

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

## Build with the Python tool

Create or open a flow in

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). For more information, see[Create a flow](../flow-develop?view=foundry-classic).Select

**+ Python**to add the Python tool to your flow.Enter values for the Python tool input parameters that are described in the

[Inputs table](#inputs). For example, in the**Code**input text box, you can enter the following Python code:`from promptflow import tool @tool def my_python_tool(message: str) -> str: return 'hello ' + message`

For more information, see

[Python code input requirements](#python-code-input-requirements).Add more tools to your flow, as needed. Or select

**Run**to run the flow.The outputs are described in the

[Outputs table](#outputs). Based on the previous example Python code input, if the input message is "world," the output is`hello world`

.

## Inputs

The list of inputs change based on the arguments of the tool function, after you save the code. Adding type to arguments and `return`

values helps the tool show the types properly.

| Name | Type | Description | Required |
|---|---|---|---|
| Code | string | The Python code snippet. | Yes |
| Inputs | - | The list of the tool function parameters and its assignments. | - |

## Outputs

The output is the `return`

value of the Python tool function. For example, consider the following Python tool function:

```
from promptflow import tool
@tool
def my_python_tool(message: str) -> str:
return 'hello ' + message
```


If the input message is "world," the output is `hello world`

.

### Types

| Type | Python example | Description |
|---|---|---|
| int | param: int | Integer type |
| bool | param: bool | Boolean type |
| string | param: str | String type |
| double | param: float | Double type |
| list | param: list or param: List[T] | List type |
| object | param: dict or param: Dict[K, V] | Object type |
| Connection | param: CustomConnection | Connection type is handled specially. |

Parameters with `Connection`

type annotation are treated as connection inputs, which means:

- The prompt flow extension shows a selector to select the connection.
- During execution time, the prompt flow tries to find the connection with the same name from the parameter value that was passed in.

Note

The `Union[...]`

type annotation is only supported for connection type. An example is `param: Union[CustomConnection, OpenAIConnection]`

.

## Python code input requirements

This section describes requirements of the Python code input for the Python tool.

- Python tool code should consist of a complete Python code, including any necessary module imports.
- Python tool code must contain a function decorated with
`@tool`

(tool function), serving as the entry point for execution. The`@tool`

decorator should be applied only once within the snippet. - Python tool function parameters must be assigned in the
`Inputs`

section. - Python tool function shall have a return statement and value, which is the output of the tool.

The following Python code is an example of best practices:

```
from promptflow import tool
@tool
def my_python_tool(message: str) -> str:
return 'hello ' + message
```


## Consume a custom connection in the Python tool

If you're developing a Python tool that requires calling external services with authentication, you can use the custom connection in a prompt flow. It allows you to securely store the access key and then retrieve it in your Python code.

### Create a custom connection

Create a custom connection that stores all your large language model API key or other required credentials.

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../migrate-project?view=foundry-classic).

- An Azure account with an active subscription. If you don't have one, create a
[free Azure account, which includes a free trial subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - If you don't have one,
[create a hub-based project](../hub-create-projects?view=foundry-classic).

Go to the

**Management center**page for your project.Under either the

**Hub**or**Project**heading, select**Connected resources**.Select

**+ New Connection**.Select

**Custom**service. You can define your connection name. You can add multiple key-value pairs to store your credentials and keys by selecting**Add key-value pairs**.Note

Make sure at least one key-value pair is set as secret. Otherwise, the connection won't be created successfully. To set one key-value pair as secret, select

**is secret**to encrypt and store your key value.

### Consume a custom connection in Python

To consume a custom connection in your Python code:

- In the code section in your Python node, import the custom connection library
`from promptflow.connections import CustomConnection`

. Define an input parameter of the type`CustomConnection`

in the tool function. - Parse the input to the input section. Then select your target custom connection in the value dropdown list.

For example:

```
from promptflow import tool
from promptflow.connections import CustomConnection
@tool
def my_python_tool(message: str, myconn: CustomConnection) -> str:
# Get authentication key-values from the custom connection
connection_key1_value = myconn.key1
connection_key2_value = myconn.key2
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/openai/quotas-limits/ -->

# Azure OpenAI in Microsoft Foundry Models quotas and limits

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article contains a quick reference and a detailed description of the quotas and limits for Azure OpenAI.

## Scope of quota

Quotas and limits aren't enforced at the tenant level. Instead, the highest level of quota restrictions is scoped at the Azure subscription level.

## Regional quota allocation

Tokens per minute (TPM) and requests per minute (RPM) limits are defined *per region*, *per subscription*, and *per model or deployment type*.

For example, if the `gpt-4.1`

Global Standard model is listed with a quota of *5 million TPM* and *5,000 RPM*, then *each region* where that [model or deployment type is available](concepts/models?view=foundry-classic) has its own dedicated quota pool of that amount for *each* of your Azure subscriptions. Within a single Azure subscription, it's possible to use a larger quantity of total TPM and RPM quota for a given model and deployment type, as long as you have resources and model deployments spread across multiple regions.

## Quotas and limits reference

The following section provides you with a quick guide to the default quotas and limits that apply to Azure OpenAI:

| Limit name | Limit value |
|---|---|
| Azure OpenAI resources per region, per Azure subscription | 30. |
| Default DALL-E 2 quota limits | 2 concurrent requests. |
| Default DALL-E 3 quota limits | 6 requests per minute |
| Default GPT-image-1 quota limits | 9 requests per minute |
| Default GPT-image-1-mini quota limits | 12 requests per minute |
| Default GPT-image-1.5 quota limits | 9 requests per minute |
| Default Sora quota limits | 60 requests per minute. |
| Default Sora 2 quota limits | 2 parallel tasks |
| Default speech-to-text audio API quota limits | 3 requests per minute. |
| Maximum prompt tokens per request | Varies per model. For more information, see
|

`(tokens in training file) x (# of epochs)`

`/embeddings`

`/chat/completions`

messages`/chat/completions`

functions`/chat completions`

tools[Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs).200 MB via the

[Foundry portal](https://ai.azure.com/?cid=learnDocs).`GPT-4o`

and `GPT-4.1`

maximum images per request (number of images in the messages array or conversation history)`GPT-4 vision-preview`

and `GPT-4 turbo-2024-04-09`

default maximum tokensIncrease the

`max_tokens`

parameter value to avoid truncated responses. `GPT-4o`

maximum tokens defaults to 4,096.11 Our current APIs allow up to 10 custom headers, which are passed through the pipeline and returned. Some customers now exceed this header count, which results in HTTP 431 errors. There's no solution for this error, other than to reduce header volume. In future API versions, we won't pass through custom headers. We recommend that customers don't depend on custom headers in future system architectures.

Note

Quota limits are subject to change.

## GPT-5.2 series

| Model | Deployment Type | Default RPM | Default TPM | Enterprise and MCA-E RPM | Enterprise and MCA-E TPM |
|---|---|---|---|---|---|
`gpt-5.2` |
DataZoneStandard | 3,000 | 300,000 | 30,000 | 3,000,000 |
`gpt-5.2` |
GlobalStandard | 10,000 | 1,000,000 | 100,000 | 10,000,000 |
`gpt-5.2-chat` |
GlobalStandard | 10,000 | 1,000,000 | 50,000 | 5,000,000 |
`gpt-5.2-codex` |
GlobalStandard | 1,000 | 1,000,000 | 10,000 | 10,000,000 |

## GPT-5.1 series

| Model | Deployment Type | Default RPM | Default TPM | Enterprise and MCA-E RPM | Enterprise and MCA-E TPM |
|---|---|---|---|---|---|
`gpt-5.1` |
DataZoneStandard | 3,000 | 300,000 | 30,000 | 3,000,000 |
`gpt-5.1` |
GlobalStandard | 10,000 | 1,000,000 | 100,000 | 10,000,000 |
`gpt-5.1-chat` |
GlobalStandard | 10,000 | 1,000,000 | 50,000 | 5,000,000 |
`gpt-5.1-codex` |
GlobalStandard | 1,000 | 1,000,000 | 10,000 | 10,000,000 |
`gpt-5.1-codex-mini` |
GlobalStandard | 1,000 | 1,000,000 | 10,000 | 10,000,000 |
`gpt-5.1-codex-max` |
GlobalStandard | 10,000 | 1,000,000 | 100,000 | 10,000,000 |

## GPT-5 series

| Model | Deployment Type | Default RPM | Default TPM | Enterprise and MCA-E RPM | Enterprise and MCA-E TPM |
|---|---|---|---|---|---|
`gpt-5` |
DataZoneStandard | 3,000 | 300,000 | 30,000 | 3,000,000 |
`gpt-5` |
GlobalStandard | 10,000 | 1,000,000 | 100,000 | 10,000,000 |
`gpt-5-chat` |
GlobalStandard | 1,000 | 1,000,000 | 5,000 | 5,000,000 |
`gpt-5-mini` |
DataZoneStandard | 300 | 300,000 | 3,000 | 3,000,000 |
`gpt-5-mini` |
GlobalStandard | 1,000 | 1,000,000 | 10,000 | 10,000,000 |
`gpt-5-nano` |
DataZoneStandard | 2,000 | 2,000,000 | 50,000 | 50,000,000 |
`gpt-5-nano` |
GlobalStandard | 5,000 | 5,000,000 | 150,000 | 150,000,000 |
`gpt-5-codex` |
GlobalStandard | 1,000 | 1,000,000 | 10,000 | 10,000,000 |
`gpt-5-pro` |
GlobalStandard | 1,600 | 160,000 | 16,000 | 1,600,000 |

## model-router rate limits

| Model | Deployment Type | Default RPM | Default TPM | Enterprise and MCA-E RPM | Enterprise and MCA-E TPM |
|---|---|---|---|---|---|
`model-router` `(2025-11-18)` |
DataZoneStandard | 150 | 150,000 | 300 | 300,000 |
`model-router` `(2025-11-18)` |
GlobalStandard | 250 | 250,000 | 400 | 400,000 |

## Batch limits

| Limit name | Limit value |
|---|---|
| Maximum Batch input files - (no expiration) | 500 |
| Maximum Batch input files - (expiration set) | 10,000 |
| Maximum input file size | 200 MB |
| Maximum requests per file | 100,000 |

Note

Batch file limits don't apply to output files (for example, `result.jsonl`

, and `error.jsonl`

). To remove batch input file limits, use [Batch with Azure Blob Storage](how-to/batch-blob-storage?view=foundry-classic).

## Batch quota

The table shows the batch quota limit. Quota values for global batch are represented in terms of enqueued tokens. When you submit a file for batch processing, the number of tokens in the file is counted. Until the batch job reaches a terminal state, those tokens count against your total enqueued token limit.

### Global batch

| Model | Enterprise and MCA-E | Default | Monthly credit card-based subscriptions | MSDN subscriptions | Azure for Students, free trials |
|---|---|---|---|---|---|
`gpt-4.1` |
5B | 200M | 50M | 90K | N/A |
`gpt-4.1 mini` |
15B | 1B | 50M | 90K | N/A |
`gpt-4.1-nano` |
15B | 1B | 50M | 90K | N/A |
`gpt-4o` |
5B | 200M | 50M | 90K | N/A |
`gpt-4o-mini` |
15B | 1B | 50M | 90K | N/A |
`gpt-4-turbo` |
300M | 80M | 40M | 90K | N/A |
`gpt-4` |
150M | 30M | 5M | 100K | N/A |
`o3-mini` |
15B | 1B | 50M | 90K | N/A |
`o4-mini` |
15B | 1B | 50M | 90K | N/A |
`gpt-5` |
5B | 200M | 50M | 90K | N/A |

B = billion | M = million | K = thousand

### Data zone batch

| Model | Enterprise and MCA-E | Default | Monthly credit card-based subscriptions | MSDN subscriptions | Azure for Students, free trials |
|---|---|---|---|---|---|
`gpt-4.1` |
500M | 30M | 30M | 90K | N/A |
`gpt-4.1-mini` |
1.5B | 100M | 50M | 90K | N/A |
`gpt-4o` |
500M | 30M | 30M | 90K | N/A |
`gpt-4o-mini` |
1.5B | 100M | 50M | 90K | N/A |
`o3-mini` |
1.5B | 100M | 50M | 90K | N/A |
`gpt-5` |
5B | 200M | 50M | 90K | N/A |

## gpt-oss

| Model | Tokens per minute (TPM) | Requests per minute (RPM) |
|---|---|---|
`gpt-oss-120b` |
5 M | 5 K |

## GPT-4 rate limits

### GPT-4.5 preview Global Standard

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`gpt-4.5` |
Enterprise and MCA-E | 200K | 200 |
`gpt-4.5` |
Default | 150K | 150 |

### GPT-4.1 series Global Standard

| Model | Tier | Quota limit in tokens per minute (TPM) | Requests per minute |
|---|---|---|---|
`gpt-4.1` (2025-04-14) |
Enterprise and MCA-E | 5M | 5K |
`gpt-4.1` (2025-04-14) |
Default | 1M | 1K |
`gpt-4.1-nano` (2025-04-14) |
Enterprise and MCA-E | 150M | 150K |
`gpt-4.1-nano` (2025-04-14) |
Default | 5M | 5K |
`gpt-4.1-mini` (2025-04-14) |
Enterprise and MCA-E | 150M | 150K |
`gpt-4.1-mini` (2025-04-14) |
Default | 5M | 5K |

### GPT-4.1 series Data Zone Standard

| Model | Tier | Quota limit in tokens per minute (TPM) | Requests per minute |
|---|---|---|---|
`gpt-4.1` (2025-04-14) |
Enterprise and MCA-E | 2M | 2K |
`gpt-4.1` (2025-04-14) |
Default | 300K | 300 |
`gpt-4.1-nano` (2025-04-14) |
Enterprise and MCA-E | 50M | 50K |
`gpt-4.1-nano` (2025-04-14) |
Default | 2M | 2K |
`gpt-4.1-mini` (2025-04-14) |
Enterprise and MCA-E | 50M | 50K |
`gpt-4.1-mini` (2025-04-14) |
Default | 2M | 2K |

### GPT-4 Turbo

`gpt-4`

(`turbo-2024-04-09`

) has rate limit tiers with higher limits for certain customer types.

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`gpt-4` (turbo-2024-04-09) |
Enterprise and MCA-E | 2M | 12K |
`gpt-4` (turbo-2024-04-09) |
Default | 450K | 2.7K |

## computer-use-preview Global Standard rate limits

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`computer-use-preview` |
Enterprise and MCA-E | 30M | 300K |
`computer-use-preview` |
Default | 450K | 4.5K |

## o-series rate limits

Important

The ratio of requests per minute to tokens per minute for quota can vary by model. When you deploy a model programmatically or [request a quota increase](https://aka.ms/oai/stuquotarequest), you don't have granular control over tokens per minute and requests per minute as independent values. Quota is allocated in terms of units of capacity, which have corresponding amounts of requests per minute and tokens per minute.

| Model | Capacity | Requests per minute (RPM) | Tokens per minute (TPM) |
|---|---|---|---|
| Older chat models | 1 unit | 6 RPM | 1,000 TPM |
`o1` and `o1-preview` |
1 unit | 1 RPM | 6,000 TPM |
`o3` |
1 unit | 1 RPM | 1,000 TPM |
`o4-mini` |
1 unit | 1 RPM | 1,000 TPM |
`o3-mini` |
1 unit | 1 RPM | 10,000 TPM |
`o1-mini` |
1 unit | 1 RPM | 10,000 TPM |
`o3-pro` |
1 unit | 1 RPM | 10,000 TPM |

This concept is important for programmatic model deployment, because changes in the RPM to TPM ratio can result in accidental misallocation of quota.

### o-series Global Standard

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`codex-mini` |
Enterprise and MCA-E | 10M | 10K |
`o3-pro` |
Enterprise and MCA-E | 16M | 1.6K |
`o4-mini` |
Enterprise and MCA-E | 10M | 10K |
`o3` |
Enterprise and MCA-E | 10M | 10K |
`o3-mini` |
Enterprise and MCA-E | 50M | 5K |
`o1` and `o1-preview` |
Enterprise and MCA-E | 30M | 5K |
`o1-mini` |
Enterprise and MCA-E | 50M | 5K |
`codex-mini` |
Default | 1M | 1K |
`o3-pro` |
Default | 1.6M | 160 |
`o4-mini` |
Default | 1M | 1K |
`o3` |
Default | 1M | 1K |
`o3-mini` |
Default | 5M | 500 |
`o1` and `o1-preview` |
Default | 3M | 500 |
`o1-mini` |
Default | 5M | 500 |

### o-series Data Zone Standard

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`o3` |
Default | 10M | 10K |
`o4-mini` |
Default | 10M | 10K |
`o3-mini` |
Enterprise and MCA-E | 20M | 2K |
`o3-mini` |
Default | 2M | 200 |
`o1` |
Enterprise and MCA-E | 6M | 1K |
`o1` |
Default | 600K | 100 |

### o1-preview and o1-mini Standard

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`o1-preview` |
Enterprise and MCA-E | 600K | 100 |
`o1-mini` |
Enterprise and MCA-E | 1M | 100 |
`o1-preview` |
Default | 300K | 50 |
`o1-mini` |
Default | 500K | 50 |

## gpt-4o rate limits

`gpt-4o`

and `gpt-4o-mini`

have rate limit tiers with higher limits for certain customer types.

### gpt-4o Global Standard

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`gpt-4o` |
Enterprise and MCA-E | 30M | 180K |
`gpt-4o-mini` |
Enterprise and MCA-E | 150M | 1.5M |
`gpt-4o` |
Default | 450K | 2.7K |
`gpt-4o-mini` |
Default | 2M | 12K |

### gpt-4o Data Zone Standard

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`gpt-4o` |
Enterprise and MCA-E | 10M | 60K |
`gpt-4o-mini` |
Enterprise and MCA-E | 20M | 120K |
`gpt-4o` |
Default | 300K | 1.8K |
`gpt-4o-mini` |
Default | 1M | 6K |

### gpt-4o Standard

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`gpt-4o` |
Enterprise and MCA-E | 1M | 6K |
`gpt-4o-mini` |
Enterprise and MCA-E | 2M | 12K |
`gpt-4o` |
Default | 150K | 900 |
`gpt-4o-mini` |
Default | 450K | 2.7K |

### gpt-4o audio

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`gpt-4o-audio-preview` |
Default | 450K | 1K |
`gpt-4o-realtime-preview` |
Default | 800K | 1K |
`gpt-4o-mini-audio-preview` |
Default | 2M | 1K |
`gpt-4o-mini-realtime-preview` |
Default | 800K | 1K |
`gpt-audio` |
Default | 100K | 30 |
`gpt-audio-mini` |
Default | 100K | 30 |
`gpt-realtime` |
Default | 100K | 100 |
`gpt-realtime-mini` |
Default | 100K | 100 |
`gpt-realtime-mini-2025-12-15` |
Default | 100K | 100 |

## GPT-image-1 series rate limits

### GPT-image-1 Global Standard

| Model | Tier | Quota limit in tokens per minute | Requests per minute |
|---|---|---|---|
`gpt-image-1` |
Enterprise and MCA-E | N/A | 60 |
`gpt-image-1` |
Medium | N/A | 36 |
`gpt-image-1` |
Low | N/A | 9 |
`gpt-image-1-mini` |
Low | N/A | 12 |
`gpt-image-1-mini` |
Medium | N/A | 36 |
`gpt-image-1-mini` |
High | N/A | 120 |
`gpt-image-1` |
Low | N/A | 9 |
`gpt-image-1` |
Medium | N/A | 18 |
`gpt-image-1` |
High | N/A | 60 |

## Usage tiers

Global Standard deployments use the global infrastructure of Azure. They dynamically route customer traffic to the data center with the best availability for the customer's inference requests. Similarly, Data Zone Standard deployments allow you to use the global infrastructure of Azure to dynamically route traffic to the data center within the Microsoft-defined data zone with the best availability for each request. This practice enables more consistent latency for customers with low to medium levels of traffic. Customers with high sustained levels of usage might see greater variability in response latency.

Azure OpenAI usage tiers are designed to provide consistent performance for most customers with low to medium levels of traffic. Each usage tier defines the maximum throughput (tokens per minute) you can expect with predictable latency. When your usage stays within your assigned tier, latency remains stable and response times are consistent.

### What happens if you exceed your usage tier?

- If your request throughput exceeds your usage tier—especially during periods of high demand—your response latency may increase significantly.
- Latency can vary and, in some cases, may be more than two times higher than when operating within your usage tier.
- This variability is most noticeable for customers with high sustained usage or bursty traffic patterns.

### Recommended actions If you exceed your usage tier

If you encounter 429 errors or notice increased latency variability, here’s what you should do:

- Request a quota increase: visit the Azure portal to request a higher quota for your subscription.
- Consider upgrading to a premium offer (PTU): for latency-critical or high-volume workloads, upgrade to Provisioned Throughput Units (PTU). PTU provides dedicated resources, guaranteed capacity, and predictable latency—even at scale. This is the best choice for mission-critical applications that require consistent performance.
- Monitor your usage: regularly review your usage metrics in the Azure portal to ensure you are operating within your tier limits. Adjust your workload or deployment strategy as needed.

The usage limit determines the level of usage above which customers might see larger variability in response latency. A customer's usage is defined per model. It's the total number of tokens consumed across all deployments in all subscriptions in all regions for a given tenant.

Note

Usage tiers apply only to Standard, Data Zone Standard, and Global Standard deployment types. Usage tiers don't apply to global batch and provisioned throughput deployments.

### Global Standard, Data Zone Standard, and Standard

| Model | Usage tiers per month |
|---|---|
`gpt-5` |
32 billion tokens |
`gpt-5-mini` |
160 billion tokens |
`gpt-5-nano` |
800 billion tokens |
`gpt-5-chat` |
32 billion tokens |
`gpt-4` + `gpt-4-32k` (all versions) |
6 billion tokens |
`gpt-4o` |
12 billion tokens |
`gpt-4o-mini` |
85 billion tokens |
`o3-mini` |
50 billion tokens |
`o1` |
4 billion tokens |
`o4-mini` |
50 billion tokens |
`o3` |
5 billion tokens |
`gpt-4.1` |
30 billion tokens |
`gpt-4.1-mini` |
150 billion tokens |
`gpt-4.1-nano` |
550 billion tokens |

## Other offer types

If your Azure subscription is linked to certain [offer types](https://azure.microsoft.com/support/legal/offer-details/), your maximum quota values are lower than the values indicated in the previous tables.

GPT-5-pro quota is only available to MCA-E and default quota subscriptions. All other offer types have zero quota for this model by default.

GPT-5 reasoning model quota is 20K TPM and 200 RPM for all offer types that do not have access to MCA-E or default quota. GPT-5-chat is 50K and 50 RPM.

Some offer types are restricted to only Global Standard deployments in the East US2 and Sweden Central regions.


| Tier | Quota limit in tokens per minute |
|---|---|
`Azure for Students` |
1K (all models) Exception o-series, GPT-4.1, and GPT 4.5 Preview: 0 |
`MSDN` |
GPT-4o-mini: 200K computer-use-preview: 8K gpt-4o-realtime-preview: 1K o-series: 0 GPT 4.5 Preview: 0 GPT-4.1: 50K GPT-4.1-nano: 200K |
`Standard` & `Pay-as-you-go` |
GPT-4o-mini: 200K computer-use-preview: 30K o-series: 0 GPT 4.5 Preview: 0 GPT-4.1: 50K GPT-4.1-nano: 200K |
`Azure_MS-AZR-0111P` `Azure_MS-AZR-0035P` `Azure_MS-AZR-0025P` `Azure_MS-AZR-0052P` |
GPT-4o-mini: 200K |
`CSP Integration Sandbox` * |
All models: 0 |
`Lightweight trial` `Free trials` `Azure Pass` |
All models: 0 |

*This limit applies to only a small number of legacy CSP sandbox subscriptions. Use the following query to determine what `quotaId`

value is associated with your subscription.

To determine the offer type associated with your subscription, you can check your `quotaId`

value. If your `quotaId`

value isn't listed in this table, your subscription qualifies for the default quota.

See the [API reference](/en-us/rest/api/resources/subscriptions/get).

```
az login
access_token=$(az account get-access-token --query accessToken -o tsv)
```


```
curl -X GET "https://management.azure.com/subscriptions/{subscriptionId}?api-version=2020-01-01" \
-H "Authorization: Bearer $access_token" \
-H "Content-Type: application/json"
```


## Output

```
{
"authorizationSource": "Legacy",
"displayName": "Pay-As-You-Go",
"id": "/subscriptions/aaaaaa-bbbbb-cccc-ddddd-eeeeee",
"state": "Enabled",
"subscriptionId": "aaaaaa-bbbbb-cccc-ddddd-eeeeee",
"subscriptionPolicies": {
"locationPlacementId": "Public_2014-09-01",
"quotaId": "PayAsYouGo_2014-09-01",
"spendingLimit": "Off"
}
}
```


| Quota allocation/Offer type | Subscription quota ID |
|---|---|
| Enterprise and MCA-E | `EnterpriseAgreement_2014-09-01` |
| Pay-as-you-go | `PayAsYouGo_2014-09-01` |
| MSDN | `MSDN_2014-09-01` |
| CSP Integration Sandbox | `CSPDEVTEST_2018-05-01` |
| Azure for Students | `AzureForStudents_2018-01-01` |
| Free trial | `FreeTrial_2014-09-01` |
| Azure Pass | `AzurePass_2014-09-01` |
| Azure_MS-AZR-0111P | `AzureInOpen_2014-09-01` |
| Azure_MS-AZR-0150P | `LightweightTrial_2016-09-01` |
| Azure_MS-AZR-0035P Azure_MS-AZR-0025P Azure_MS-AZR-0052P |
`MPN_2014-09-01` |
| Azure_MS-AZR-0023P Azure_MS-AZR-0060P Azure_MS-AZR-0148P Azure_MS-AZR-0148G |
`MSDNDevTest_2014-09-01` |
| Default | Any quota ID not listed in this table |

### General best practices to remain within rate limits

To minimize issues related to rate limits, it's a good idea to use the following techniques:

- Implement retry logic in your application.
- Avoid sharp changes in the workload. Increase the workload gradually.
- Test different load increase patterns.
- Increase the quota assigned to your deployment. Move quota from another deployment, if necessary.

## Request quota increases

Quota increase requests can be submitted via the [quota increase request form](https://aka.ms/oai/stuquotarequest). Due to high demand, quota increase requests are accepted and filled in the order they're received. Priority is given to customers who generate traffic that consumes the existing quota allocation. Your request might be denied if this condition isn't met.

You can [submit a service request](../../ai-services/cognitive-services-support-options?view=foundry-classic&context=/azure/ai-foundry/openai/context/context) for other rate limits.

## Regional quota capacity limits

You can view quota availability by region for your subscription in the [Foundry portal](https://ai.azure.com/resource/quota).

To view quota capacity by region for a specific model or version, you can query the [capacity API](/en-us/rest/api/aiservices/accountmanagement/model-capacities/list) for your subscription. Provide a `subscriptionId`

, `model_name`

, and `model_version`

and the API returns the available capacity for that model across all regions and deployment types for your subscription.

Note

Currently, both the Foundry portal and the capacity API return quota/capacity information for models that are [retired](concepts/model-retirements?view=foundry-classic) and no longer available.

See the [API reference](/en-us/rest/api/aiservices/accountmanagement/model-capacities/list).

```
import requests
import json
from azure.identity import DefaultAzureCredential
subscriptionId = "Replace with your subscription ID" #replace with your subscription ID
model_name = "gpt-4o" # Example value, replace with model name
model_version = "2024-08-06" # Example value, replace with model version
token_credential = DefaultAzureCredential()
token = token_credential.get_token('https://management.azure.com/.default')
headers = {'Authorization': 'Bearer ' + token.token}
url = f"https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.CognitiveServices/modelCapacities"
params = {
"api-version": "2024-06-01-preview",
"modelFormat": "OpenAI",
"modelName": model_name,
"modelVersion": model_version
}
response = requests.get(url, params=params, headers=headers)
model_capacity = response.json()
print(json.dumps(model_capacity, indent=2))
```


## Related content

- Explore how to
[manage quota](how-to/quota?view=foundry-classic)for your Azure OpenAI deployments. - Learn more about the
[underlying models that power Azure OpenAI](concepts/models?view=foundry-classic).
