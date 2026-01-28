---
merged_at: 2026-01-28T07:33:20.578663
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-models/quotas-limits -->

# Microsoft Foundry Models quotas and limits

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This article provides a quick reference and detailed description of the quotas and limits for Microsoft Foundry Models. For quotas and limits specific to the Azure OpenAI in Foundry Models, see [Quota and limits in Azure OpenAI](../openai/quotas-limits?view=foundry-classic).

## Quotas and limits reference

Azure uses quotas and limits to prevent budget overruns due to fraud and to honor Azure capacity constraints. Consider these limits as you scale for production workloads. The following sections provide a quick guide to the default quotas and limits that apply to Azure AI model inference service in Foundry:

### Resource limits (per Azure subscription, per region)

| Limit name | Limit value |
|---|---|
| Foundry resources per region per Azure subscription | 100 |
| Max projects per resource | 250 |
| Max deployments per resource (model deployments within a Foundry resource) | 32 |

### Rate limits

The following table lists limits for Foundry Models for the following rates:

- Tokens per minute
- Requests per minute
- Concurrent request

| Models | Tokens per minute | Requests per minute | Concurrent requests |
|---|---|---|---|
| Azure OpenAI models | Varies per model and SKU. See
|

[limits for Azure OpenAI](../openai/quotas-limits?view=foundry-classic).- DeepSeek-V3-0324

- Llama-4-Maverick-17B-128E-Instruct-FP8

- Grok 3

- Grok 3 mini

- Medium: 30

- High (Enterprise): 100

- Flux.1-Kontext Pro

To increase your quota:

- For Azure OpenAI, use
[Foundry Service: Request for Quota Increase](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR4xPXO648sJKt4GoXAed-0pUMFE1Rk9CU084RjA0TUlVSUlMWEQzVkJDNCQlQCN0PWcu)to submit your request. - For other models, see
[request increases to the default limits](#request-increases-to-the-default-limits).

Due to high demand, we evaluate limit increase requests per request.

### Other limits

| Limit name | Limit value |
|---|---|
Max number of custom headers in API requests1 |
10 |

1 Our current APIs allow up to 10 custom headers, which the pipeline passes through and returns. If you exceed this header count, your request results in an HTTP 431 error. To resolve this error, reduce the header volume. **Future API versions won't pass through custom headers**. We recommend that you don't depend on custom headers in future system architectures.

## Usage tiers

Global Standard deployments use Azure's global infrastructure to dynamically route customer traffic to the data center with best availability for the customer's inference requests. This infrastructure enables more consistent latency for customers with low to medium levels of traffic. Customers with high sustained levels of usage might see more variabilities in response latency.

The Usage Limit determines the level of usage above which customers might see larger variability in response latency. A customer's usage is defined per model and is the total tokens consumed across all deployments in all subscriptions in all regions for a given tenant.

## Request increases to the default limits

Quota increase requests can be submitted via the [quota increase request form](https://aka.ms/oai/stuquotarequest). Due to high demand, quota increase requests are accepted and filled in the order they're received. Priority is given to customers who generate traffic that consumes the existing quota allocation. Your request might be denied if this condition isn't met.

You can [submit a service request](../../ai-services/cognitive-services-support-options?view=foundry-classic&context=/azure/ai-foundry/openai/context/context) for other rate limits.

## General best practices to stay within rate limits

To minimize issues related to rate limits, use the following techniques:

- Implement retry logic in your application.
- Avoid sharp changes in the workload. Increase the workload gradually.
- Test different load increase patterns.
- Increase the quota assigned to your deployment. Move quota from another deployment, if necessary.

## Setting client side timeout

We recommend explicitly setting the client side timeout as follows.

Note

If not explicitly set, the client side timeout exists as per the library used, and may not be the same limits as above.

- Reasoning models (models that generate intermediate reasoning tokens before producing a summarized response): up to 29 minutes.
- Non-reasoning models:
- For streaming, up to 60 seconds.
- For non-streaming requests, up to 29 minutes.


29 minutes here does not mean all requests will take 29 minutes but rather depending on context tokens, generated tokens, and cache hit rates, requests can take up to 29 minutes.

You will need to set a timeout less than the above tuned to your traffic patterns.

For reasoning models including streaming requests, all the reasoning tokens are first generated and then summarized before sending the first response token back to the user.

You can modify the [reasoning effort](../openai/how-to/reasoning?view=foundry-classic) parameter to control the number of reasoning tokens generated in the process.

## Next steps

- Learn more about the
[models available in Foundry Models](../model-inference/concepts/models?view=foundry-classic)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/ai-services/content-safety-overview -->

# Content Safety in the Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Azure AI Content Safety is an AI service that detects harmful user-generated and AI-generated content in applications and services. Azure AI Content Safety includes APIs that help you detect and prevent the output of harmful content. The interactive Content Safety **try it out** page in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs) lets you view, explore, and try out sample code for detecting harmful content across different modalities.

## Features

Use Azure AI Content Safety for the following scenarios:

### Text content

**Moderate text content**: Scans and moderates text content. It identifies and categorizes text based on different levels of severity to ensure appropriate responses.**Groundedness detection**: Determines if the AI's responses are based on trusted, user-provided sources. This feature ensures that the answers are "grounded" in the intended material. Groundedness detection helps improve the reliability and factual accuracy of responses.**Protected material detection for text**: Identifies protected text material, such as known song lyrics, articles, or other content. This feature ensures that the AI doesn't output this content without permission.**Protected material detection for code**: Detects code segments in the model's output that match known code from public repositories. This feature helps prevent uncredited or unauthorized reproduction of source code.**Prompt shields**: Provides a unified API to address "Jailbreak" and "Indirect Attacks":- Jailbreak Attacks: Attempts by users to manipulate the AI into bypassing its safety protocols or ethical guidelines. Examples include prompts designed to trick the AI into giving inappropriate responses or performing tasks it was programmed to avoid.
- Indirect Attacks: Also known as Cross-Domain Prompt Injection Attacks. Indirect attacks involve embedding malicious prompts within documents that the AI might process. For example, if a document contains hidden instructions, the AI might inadvertently follow them, leading to unintended or unsafe outputs.


### Image content

**Moderate image content**: Similar to text moderation, this feature filters and assesses image content to detect inappropriate or harmful visuals.**Moderate multimodal content**: Designed to handle a combination of text and images. It assesses the overall context and any potential risks across multiple types of content.

### Custom filtering

**Custom categories**: Allows users to define specific categories for moderating and filtering content. Tailors safety protocols to unique needs.**Safety system message**: Provides a method for setting up a "System Message" to instruct the AI on desired behavior and limitations. It reinforces safety boundaries and helps prevent unwanted outputs.

## Understand harm categories

### Harm categories

| Category | Description | API term |
|---|---|---|
| Hate and Fairness | Hate and fairness harms refer to any content that attacks or uses discriminatory language with reference to a person or identity group based on certain differentiating attributes of these groups. This includes, but isn't limited to:
|
`Hate` |
| Sexual | Sexual describes language related to anatomical organs and genitals, romantic relationships and sexual acts, acts portrayed in erotic or affectionate terms, including those portrayed as an assault or a forced sexual violent act against one's will. This includes but isn't limited to:
|
`Sexual` |
| Violence | Violence describes language related to physical actions intended to hurt, injure, damage, or kill someone or something; describes weapons, guns, and related entities. This includes, but isn't limited to:
|
`Violence` |
| Self-Harm | Self-harm describes language related to physical actions intended to purposely hurt, injure, damage one's body or kill oneself. This includes, but isn't limited to:
|
`SelfHarm` |

### Severity levels

| Level | Description |
|---|---|
| Safe | Content might be related to violence, self-harm, sexual, or hate categories. However, the terms are used in general, journalistic, scientific, medical, and similar professional contexts, which are appropriate for most audiences. |
| Low | Content that expresses prejudiced, judgmental, or opinionated views, includes offensive use of language, stereotyping, use-cases exploring a fictional world (for example, gaming, literature) and depictions at low intensity. |
| Medium | Content that uses offensive, insulting, mocking, intimidating, or demeaning language towards specific identity groups, includes depictions of seeking and executing harmful instructions, fantasies, glorification, promotion of harm at medium intensity. |
| High | Content that displays explicit and severe harmful instructions, actions, damage, or abuse; includes endorsement, glorification, or promotion of severe harmful acts, extreme or illegal forms of harm, radicalization, or nonconsensual power exchange or abuse. |

## Limitations

For supported regions, rate limits, and input requirements for all features, see the [Content Safety service overview](/en-us/azure/ai-services/content-safety/overview). For supported languages, see the [Language support](/en-us/azure/ai-services/content-safety/language-support) page.

## Next step

Get started using Azure AI Content Safety in Foundry portal by following the [How-to guide](/en-us/azure/ai-services/content-safety/how-to/foundry).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/ -->

# Foundry Local (preview) documentation

Safely design, customize, and manage AI applications and agents on-device.

This browser is no longer supported.

Upgrade to Microsoft Edge to take advantage of the latest features, security updates, and technical support.

Safely design, customize, and manage AI applications and agents on-device.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/what-is-foundry-local -->

# What is Foundry Local?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

Foundry Local is an on-device AI inference solution that you use to run AI models locally through a CLI, SDK, or REST API.

## Prerequisites

- Install Foundry Local. Follow
[Get started with Foundry Local](get-started?view=foundry-classic). - Use a terminal (for example, Windows Terminal or macOS Terminal).
- Have an internet connection for first-time model downloads.
- If you use Foundry Local only on your device, you don't need an Azure subscription and there are no Azure RBAC role requirements.

## Try it (CLI)

Run these commands to verify your installation and run a model locally.

```
foundry --help
foundry model list
foundry model run qwen2.5-0.5b
```


`foundry --help`

prints the available CLI commands.`foundry model list`

lists available models. The first run might download execution providers for your hardware.`foundry model run qwen2.5-0.5b`

downloads the model (first run) and starts an interactive prompt in your terminal.

Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

## Key features

**On-device inference**: Run models locally to reduce costs and help keep data on your device.**Model customization**: Select a preset model or use your own to meet specific needs.**Cost efficiency**: Use existing hardware to eliminate recurring cloud costs and make AI more accessible.**Seamless integration**: Integrate with your apps through the SDK, API endpoints, or CLI. For multi-user or high-throughput workloads, move to[Microsoft Foundry](../?view=foundry-classic).

## Use cases

Foundry Local is ideal when you need to:

- Keep sensitive data on your device
- Operate in limited or offline environments
- Reduce cloud inference costs
- Get low latency AI responses for real-time applications
- Experiment with AI models before you deploy to the cloud

## Frequently asked questions

### Does Foundry Local send my prompts or outputs to Microsoft?

Foundry Local is designed to run inference on your device. When you send prompts to a local Foundry Local endpoint (for example, `http://localhost:PORT`

), your prompts and model outputs are processed locally.

Foundry Local can still use the network for operations like:

**Model and component downloads**: The first time you run a model, Foundry Local downloads the model files. It might also download execution providers for your hardware.**Optional diagnostics you choose to share**: If you report a problem, you might choose to share logs (for example, by using`foundry zip-logs`

).

Your use of Foundry Local is governed by the product terms and licenses that apply to the software and the models you run. If the terms allow Microsoft to collect diagnostic information, the details are described in those terms and the [Microsoft Privacy Statement](https://www.microsoft.com/en-us/privacy/privacystatement).

### Do I need an Azure subscription?

No. Foundry Local runs on your hardware, letting you run supported models locally without requiring an Azure subscription.

### Do I need special drivers for NPU acceleration?

Install the driver for your NPU hardware:

Intel NPU: Install the

[Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html)to enable NPU acceleration on Windows.Qualcomm NPU: Install the

[Qualcomm NPU driver](https://softwarecenter.qualcomm.com/catalog/item/QHND)to enable NPU acceleration. If you see the error`Qnn error code 5005: Failed to load from EpContext model. qnn_backend_manager.`

, it likely indicates an outdated driver or an NPU resource conflict. Reboot to clear the conflict, especially after using Windows Copilot+ features.

After you install the drivers, Foundry Local automatically detects and uses the NPU.

## Get started

Follow the [Get started with Foundry Local](get-started?view=foundry-classic) guide to set up Foundry Local, discover models, and run your first local AI model.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-local/get-started -->

# Get started with Foundry Local

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

- Foundry Local is available in preview. Public preview releases provide early access to features that are in active deployment.
- Features, approaches, and processes can change or have limited capabilities, before General Availability (GA).

This guide shows you how to set up Foundry Local to run AI models on your device.

## Prerequisites

Your system must meet the following requirements to run Foundry Local:

**Operating System**: Windows 10 (x64), Windows 11 (x64/ARM), Windows Server 2025, macOS.**Hardware**: Minimum 8 GB RAM and 3 GB free disk space. Recommended 16 GB RAM and 15 GB free disk space.**Network**: Internet connection to download models and execution providers. After you download a model, you can run cached models offline.**Acceleration (optional)**: NVIDIA GPU (2000 series or newer), AMD GPU (6000 series or newer), AMD NPU, Intel iGPU, Intel NPU (32 GB or more of memory), Qualcomm Snapdragon X Elite (8 GB or more of memory), Qualcomm NPU, or Apple silicon.

To install Foundry Local by using the commands in this quickstart:

- On Windows, make sure
`winget`

is available. - On macOS, install Homebrew if you use the
`brew`

option.

Note

New NPUs are supported only on systems running Windows 24H2 or later. If you use an Intel NPU on Windows, install the [Intel NPU driver](https://www.intel.com/content/www/us/en/download/794734/intel-npu-driver-windows.html) to enable NPU acceleration in Foundry Local.

Make sure you have admin rights to install software.

Tip

If you see a service connection error after installation (for example, 'Request to local service failed'), run `foundry service restart`

.

## Quickstart

Get started quickly with Foundry Local:

### Option 1: Quick CLI setup

**Install Foundry Local**.**Windows**: Open a terminal and run the following command.`winget install Microsoft.FoundryLocal`

**macOS**: Open a terminal and run the following command.

Alternatively, you can download the installer from the`brew tap microsoft/foundrylocal brew install foundrylocal`

[Foundry Local GitHub repository](https://aka.ms/foundry-local-installer).

Reference:

[Foundry Local documentation](https://aka.ms/foundry-local-docs)**Verify the installation**. Run:`foundry --version`

You should see the installed version number.

Reference:

[Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)**Run your first model**. Open a terminal and run this command:`foundry model run qwen2.5-0.5b`

Foundry Local downloads the model, which can take a few minutes depending on your internet speed, then runs it. After the model starts, interact with it by using the command-line interface (CLI). For example, you can ask:

`Why is the sky blue?`


Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

### Option 2: Download starter projects

For practical, hands-on learning, download one of the starter projects that demonstrate real-world scenarios:

[Chat Application Starter](https://github.com/microsoft/Foundry-Local/tree/main/samples/electron/foundry-chat): Build a local chat interface with multiple model support.[Summarize Sample](https://github.com/microsoft/Foundry-Local/tree/main/samples/python/summarize): A command-line utility that generates summaries of text files or direct text input.[Function Calling Example](https://github.com/microsoft/Foundry-Local/tree/main/samples/python/functioncalling): Enable and use function calling with Phi-4 mini.

Each project includes:

- Step-by-step setup instructions
- Complete source code
- Configuration examples
- Best practices

Tip

These starter projects align with scenarios in the [how-to guides](how-to/how-to-chat-application-with-open-web-ui?view=foundry-classic) and provide immediate practical value.

Tip

Replace `qwen2.5-0.5b`

with any model name from the catalog (run `foundry model list`

to view available models). Foundry Local downloads the variant that best matches your system's hardware and software configuration. For example, if you have an NVIDIA GPU, Foundry Local downloads the CUDA version. If you have a Qualcomm NPU, Foundry Local downloads the NPU variant. If you have no GPU or NPU, Foundry Local downloads the CPU version.

When you run `foundry model list`

the first time, you see a download progress bar while Foundry Local downloads the execution providers for your hardware.

Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

## Explore commands

The Foundry CLI organizes commands into these main categories:

**Model**: Commands for managing and running models.**Service**: Commands for managing the Foundry Local service.**Cache**: Commands for managing the local model cache (downloaded models on local disk).

To view all commands, use:

```
foundry --help
```


```
foundry model --help
```


foundry --help

```
foundry service --help
```


View **cache** commands:

```
foundry cache --help
```


Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

## Optional: Run the latest GPT OSS 20B model

Run the `gpt-oss-20b`

model:

```
foundry model run gpt-oss-20b
```


Important

If the model isn't available for your device, run a smaller model (for example, `qwen2.5-0.5b`

).

For the CUDA variant, you typically need an NVIDIA GPU with 16 GB of VRAM or more.

Foundry Local version **0.6.87** or later adds support for this model. Check your version with:

```
foundry --version
```


Reference: [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic)

Tip

For details on all CLI commands, see [Foundry Local CLI reference](reference/reference-cli?view=foundry-classic).

## Upgrade Foundry Local

Run the command for your OS to upgrade Foundry Local.

- Windows: In a terminal, run:
`winget upgrade --id Microsoft.FoundryLocal`

- macOS: In a terminal, run:
`brew upgrade foundrylocal`


## Uninstall Foundry Local

To uninstall Foundry Local, run the command for your operating system:

**Windows**: Open a terminal and run:`winget uninstall Microsoft.FoundryLocal`

**macOS**: Open a terminal and run:`brew rm foundrylocal brew untap microsoft/foundrylocal brew cleanup --scrub`


## Troubleshooting

### Service connection problems

If you see this error when you run `foundry model list`

or a similar command:

```
foundry model list
Exception: Request to local service failed.
Uri: http://127.0.0.1:0/foundry/list
The requested address is not valid in its context. (127.0.0.1:0)
Please check service status with 'foundry service status'.
```


Run this command to restart the service:

```
foundry service restart
```


This command fixes cases where the service runs but isn't accessible because of a port binding problem.

Reference: [Best practices and troubleshooting](reference/reference-best-practice?view=foundry-classic)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/content-safety/data-privacy -->

# Data, privacy, and security for Azure AI Content Safety

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

This article provides details regarding how your data is processed, used, and stored by Azure AI Content Safety.

Azure AI Content Safety was designed with privacy and security in mind; however, the customer is responsible for its use and the implementation of this technology.

## How is data retained and what customer controls are available?

Azure AI Content Safety works to filter harmful content. This system works by running the input through an ensemble of classification models. Once your Azure AI Content Safety resource is created, you can submit text and images to the model through the REST API, client libraries, or the Azure AI Content Safety Studio; the model generates outputs that are returned through the API.

No input texts or images are stored in the model during detection (except for customer-supplied blocklists, as discussed below), and user inputs are not used to train, retrain, or improve the Azure AI Content Safety models.

**Blocklist data**. The Blocklist API allows customers to upload their block items for the purpose of supplementing the Azure AI Content Safety model.**Block Item data is stored in Azure Storage, encrypted at rest by Microsoft Managed keys, within the same region as the resource and logically isolated with the customer's Azure subscription and API Credentials**. Uploaded items can be deleted by the user via the DELETE API operation. Block Items are not used to improve the Azure AI Content Safety models.

To learn more about Microsoft's privacy and security commitments visit the [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/CloudServices/Azure/default.aspx).

## Is customer data processed by Azure AI Content Safety transmitted outside of the Azure AI Content Safety service or the selected region?

No. Microsoft hosts the Azure AI Content Safety models within our Azure infrastructure. All customer data sent to Azure AI Content Safety remains within Azure AI Content Safety and in the region you chose and will not be transmitted to other regions.

## Is customer data used to train the Azure AI Content Safety models?

No. We do not use customer data to train, retrain or improve the models in Azure AI Content Safety.

## Does Azure OpenAI Abuse Monitoring apply to the data that customers send to Azure AI Content Safety?

No. The Azure OpenAI [Abuse Monitoring process](/en-us/azure/ai-foundry/openai/concepts/abuse-monitoring) does not apply to customer data transmitted to Azure AI Content Safety. User input data sent to Azure AI Content Safety is not stored or made available for human review by Microsoft employees.

## Feedback and Reporting

If you have feedback on Azure AI Content Safety; suspect that Azure AI Content Safety is being used in a manner that is abusive or illegal, infringes on your rights or the rights of other people, or violates these policies; or if the system fails to block harmful content that you believe should have been filtered, please report it to this [email](mailto:acm-team@microsoft.com).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/content-safety/transparency-note -->

# Transparency note: Azure AI Content Safety

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

## What is a Transparency note?

An AI system includes not only the technology, but also the people who will use it, the people who will be affected by it, and the environment in which it is deployed. Creating a system that is fit for its intended purpose requires an understanding of how technology works, what its capabilities and limitations are, and how to achieve the best performance. Microsoft's Transparency Notes are intended to help you understand how our AI technology works, the choices system owners can make that influence system performance and behavior, and the importance of thinking about the whole system, including the technology, the people, and the environment. You can use Transparency Notes when developing or deploying your own system or share them with the people who will use or be affected by your system.

Microsoft's Transparency Notes are part of a broader effort at Microsoft to put our AI Principles into practice. To find out more, see the [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai).

## The basics of Azure AI Content Safety

### Introduction

Azure AI Content Safety detects harmful user-generated and AI-generated content in applications and services. Azure AI Content Safety includes text, image, and multimodal APIs that allow you to detect material that is harmful, and an Interactive Studio that allows you to view, explore and try out sample code for detecting harmful content across different modalities.

Custom categories is a feature that allows users to define and detect categories tailored to their specific content moderation needs. Custom categories empower users with greater flexibility and control over their content safety measures.

### Key terms

**Default categories**

The categories below describe the types of harmful content which Azure AI Content Safety detects.

Category |
Description |
|---|---|
| Hate | The hate category describes language attacks or uses that include pejorative or discriminatory language with reference to a person or identity group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance, and body size. |
| Sexual | The sexual category describes language related to anatomical organs and genitals, romantic relationships, acts portrayed in erotic or affectionate terms, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one's will, prostitution, pornography, and abuse. |
| Violence | The violence category describes language related to physical actions intended to hurt, injure, damage, or kill someone or something; describes weapons, etc. |
| Self-Harm | The self-harm category describes language related to physical actions intended to purposely hurt, injure, or damage one's body, or kill oneself. |

**Severity levels**

Content flags applied by the service assign a severity level rating, which indicates the severity of displaying the flagged content.

| Severity Level 0 – Safe | Content may be related to violence, self-harm, sexual or hate categories but the terms are used in general, journalistic, scientific, medical, and similar professional contexts that are appropriate for most audiences. |
|---|---|
| Severity Level 2 – Low | Content that expresses prejudiced, judgmental, or opinionated views, includes offensive use of language, stereotyping, use cases exploring a fictional world (for example, gaming, literature) and depictions at low intensity. |
| Severity Level 4 – Medium | Content that uses offensive, insulting, mocking, intimidating, or demeaning language towards specific identity groups, includes depictions of seeking and executing harmful instructions, fantasies, glorification, promotion of harm at medium intensity. |
| Severity Level 6 – High | Content that displays explicit and severe harmful instructions, actions, damage, or abuse, includes endorsement, glorification, promotion of severe harmful acts, extreme or illegal forms of harm, radicalization, and non-consensual power exchange or abuse. |

**Custom categories**

With custom categories, Azure AI Content Safety extends its capabilities beyond predefined content categories. Users can now create custom definitions that are unique to their environment, enabling a more personalized and relevant content moderation experience. This feature supports a wide range of use cases, from brand protection to community guidelines enforcement.

## Capabilities

### System behavior

Azure AI Content Safety uses artificial intelligence to analyze user-generated and AI-generated content and flag any harmful content (for a given severity level) such as hate speech, sexual, violent and self-harm activities. Clear and understandable explanations are provided, allowing users to understand why content was flagged or removed.

Different types of analysis are available in Azure AI Content Safety:

Type |
Functionality |
|---|---|
| Text Detection API | Scans text for hate, sexual, violence, and self-harm content, with multi-severity risk levels. |
| Image Detection API | Scans images for hate, sexual, violence, and self-harm content, with multi-severity risk levels. |
| Multimodal Detection API | Scans both images and text (including separate text or text extracted from an image using optical character recognition) for hate content, with multi-severity risk levels. |
| Azure AI Content Safety Studio | Azure AI Content Safety Studio is an online tool that customers can use to visually explore, understand, and evaluate the Azure AI Content Safety service. The studio provides a platform for customers to experiment with the different Azure AI Content Safety classifications and to interactively sample returned data without writing any code. |

### Use cases

#### Intended uses

Azure AI Content Safety can be used in multiple scenarios. The system's intended uses include:

**Social media platforms:**Customers can use Azure AI Content Safety on their social media platforms to help prevent the spread of harmful content, such as hate speech, cyberbullying, and pornography.**E-commerce websites:**E-commerce customers can use Azure AI Content Safety to help screen product listings and reviews for harmful content, such as fake reviews and offensive language.**Gaming platforms:**Gaming platforms can use Azure AI Content Safety to help detect misconduct, as well as to prevent inappropriate behavior in chats and forums.**News websites:**News websites can use Azure AI Content Safety to ensure that user comments remain civil and respectful, and to help prevent the spread of misinformation and hate speech.**Video-sharing platforms**: Video-sharing platforms can use Azure AI Content Safety to detect and remove inappropriate content, such as violence, hate speech, and pornography.

#### Considerations when choosing other use cases

We encourage customers to leverage Azure AI Content Safety in their innovative solutions or applications. However, here are some considerations when choosing a use case:

**Customization:**Different applications and solutions might have different requirements when it comes to content safety. It's important to experiment with severity levels for Azure AI Content Safety and set them to meet the needs of your specific use case. Custom categories are intended to enhance content moderation by allowing users to define what is important for their specific context. It is not intended to replace the existing content categories but to complement them, providing a more granular level of content safety.**Transparency:**Some end users might want to understand how your application or solution moderates content. When you choose to use Azure AI Content Safety, it's important to ensure that the service provides transparency and clear communication with your users about how content is moderated and why certain content might be flagged or removed.**Legal and regulatory considerations**: Organizations need to evaluate potential specific legal and regulatory obligations when using any Foundry Tools and solutions, which may not be appropriate for use in every industry or scenario. Additionally, Foundry Tools or solutions are not designed for and may not be used in ways prohibited in applicable terms of service and relevant codes of conduct.

## Limitations

### Technical limitations, operational factors, and ranges

Azure AI Content Safety has some technical limitations that can affect performance. Some of these limitations are:

**Accuracy:** Azure AI Content Safety might not be perfectly accurate in detecting inappropriate content. This is because the system relies on algorithms and machine learning, which can have biases and errors.

**Unsupported languages:** Azure AI Content Safety might not be able to detect inappropriate content in languages that it has not been trained or tested to process. Currently, Azure AI Content Safety is available in English, German, Japanese, Spanish, French, Italian, Portuguese, and Chinese.

**Image recognition:** Azure AI Content Safety might not be able to detect inappropriate content in images that are not clearly discernible or that have been edited.

**Evolving nature of content:** Azure AI Content Safety might not keep up with the evolving nature of online content. As new types of inappropriate content emerge (for example, new language or usage patterns), there may be a delay in Azure AI Content Safety's ability to detect these new types of content.

Azure AI Content Safety also has some operational factors that need to be considered for its effectiveness. Some of these factors are:

**Volume of content:** Azure AI Content Safety might struggle to handle large volumes of content. This can lead to delays in detecting inappropriate content.

**Time sensitivity:** Some types of inappropriate content require immediate action. Azure AI Content Safety might be unable to identify these types of content quickly in order to alert moderators.

**Contextual analysis:** Azure AI Content Safety might be unable to analyze content in context to determine whether it is inappropriate. For example, certain words might be appropriate in some contexts but not in others.

**Improve your custom categories:** While custom categories offer increased customization, they may require additional setup and tuning. Users should be aware of the potential need for iterative adjustments to achieve optimal performance.

It is important to rigorously evaluate Azure AI Content Safety on real data before deploying and to continue monitoring the system once deployed to ensure appropriate performance.

## System performance

In this section, we'll review what performance means for Azure AI Content Safety, best practices for improving performance, and limitations as they relate to Azure AI Content Safety.

**General performance guidelines**

Because Azure AI Content Safety serves various uses, there's no universally applicable estimate of accuracy. The performance of Azure AI Content Safety is affected by the customer use case and data. In the following sections we describe how to understand accuracy for Azure AI Content Safety at a high level.

**Accuracy**

The performance of Azure AI Content Safety is measured by examining how well the system detects harmful content. For example, one might count the true prevalence of harmful content in some text based on human judgment, and then compare with the output of the system from processing the same text. Comparing human judgment with the system recognized entities would allow you to classify the events into two kinds of correct (or "true") events and two kinds of incorrect (or "false") events.

Error Type |
Definition |
Example |
|---|---|---|
| True Positive | The model correctly identifies harmful content. | When harmful content such as "you are an idiot" is flagged as hate, the system returns a severity level of 2. The system correctly rejects the harmful content. |
| False Positive | The model incorrectly identifies harmless content as harmful. | When harmless content such as "you are a good person" is flagged as hate and returns a severity level of 4. The system incorrectly blocks the content. |
| True Negative | The model correctly identifies harmless content. | When harmless content such as "you are a good person", the system returns a severity level of 0. The system correctly accepts the content. |
| False Negative | The model fails to identify harmful content. | When harmful content such as "you are an idiot", the system returns a severity level of 0. The system incorrectly accepts the content. |

The consequences of a false positive or a false negative will vary depending upon how you use the Azure AI Content Safety system.

**Severity levels, match severity levels, and matched conditions**

System configuration influences system accuracy. Azure AI Content Safety detects harmful content by comparing the model output severity levels for a given input and uses a match severity level to accept or reject the input as a match.

Term |
Definition |
|---|---|
| Severity levels | The higher the severity of input content, the larger this value is. The values are: 0, 2, 4, or 6. |
| Match Severity Levels (Only Studio has this feature) | Match severity is a configurable value that determines the match severity level required to be considered a positive match. If the match severity level is set to 0, then the system will accept any match severity levels; if the match severity level is set to 6, then it will only accept inputs with a 6 (100%) match severity level. Studio has a default match severity level that you can change to suit your application. |

With your evaluation results, you can adjust the match severity levels for your specific use case and validate your results by testing with your data (only Azure AI Content Safety Studio has this feature). For example, games for children typically have higher content safety requirements than games available for adults only. For children's games, you might set the match severity level lower than the default match severity level. In contrast, for adults the match severity level could be higher than the default. Based on each evaluation result, you can iteratively adjust the match severity level until the trade-off between false positives and false negatives matches the needs in your use case.

### Best practices to improve accuracy

Below are some recommendations to obtain the best results.

**Meet specifications**

The following specifications are important to be aware of:

**Text and image format:**The current system only supports text and image inputs.- Maximum length of text: In Azure AI Content Safety API, the text input limit is 1000 characters per text API call. The fewer characters, the more accurate the result will be.

**Design the system to support human judgment**

We recommend using Azure AI Content Safety to support people making accurate and efficient judgments, rather than fully automating a process. Meaningful human review is important to:

- Detect and resolve cases of misidentification or other failures.
- Provide support to people who believe their content was incorrectly flagged.

For example, in gaming scenarios, legitimate content can be rejected due to having a false positive. In this case, a human reviewer can intervene and help the customer verify the results.

**Use AI features responsibly**

Use of Azure AI Content Safety is subject to the requirements of the Azure OpenAI Service Code of Conduct. If you will enable end users to create or deploy custom categories using Azure AI Content Safety, those users should be informed of those requirements and bound to adhere to them when using the system.

### Best practices for improving system performance

Do:

- Monitor the system's performance regularly to ensure that the tradeoff is appropriate for your use case.
- Adjust the severity levels for blocking based on user feedback and observed trends in content safety.
- Consider the impact of the system's performance on different user populations and adjust accordingly. For example, certain words or images may be considered offensive in one culture but not in another, and the system should be trained to detect this and adjust its risk levels accordingly.
- Take steps to mitigate any unintended consequences of adjusting the risk levels for blocking, such as over-removal of content or the spread of harmful content.
- To maximize the effectiveness of custom categories, we recommend:
- Clearly defining your custom category. The services will use the definition to augment the training dataset.
- Preparing a high quality dataset to cover both positive and negative samples, so the model has more accurate results.
- Regularly reviewing and updating the categories based on content trends.
- Utilizing user feedback to update category definitions and training samples.


Don't:

- Set the severity levels too low: If the severity levels for blocking are set too low, the system might flag a lot of content even if it is not harmful. This can negatively affect the user experience by making it difficult for users to post legitimate content without being flagged.
- Set the severity levels too high: Conversely, if the severity levels for blocking are set too high, the content safety system might not flag content as harmful. This can harm users and communities by allowing inappropriate content to be disseminated.
- Ignore feedback from users and communities: Content safety systems are designed to serve the needs of users and communities, and it is important to listen to their feedback about the system's performance. For example, if users are consistently reporting false positives or false negatives, the system should be adjusted accordingly.
- Over-relying on automated decision-making: Content safety systems often rely on automated decision-making to flag inappropriate content, but it is important to ensure appropriate human oversight and intervention to avoid errors and biases. For example, if the system flags content as inappropriate, a human moderator should review the decision to ensure that it is accurate and fair.

## Evaluating and integrating Azure AI Content Safety for your use

### Evaluation methods

Before a large-scale deployment or rollout of any Azure AI Content Safety, system owners should conduct an evaluation phase. The methods used to evaluate a system for content safety considerations typically involve analyzing large datasets of harmful content and evaluating the system's ability to accurately identify and flag potentially harmful or inappropriate content.

It's important to evaluate how the system performs across different demographic groups and geographic areas. The groups of people that are included in the evaluation depend on the type of content that is being evaluated and the intended audience of the system. For example, if the system is designed to monitor social media posts, the dataset might include a diverse range of users from various geographic locations, backgrounds, and age groups. However, if the system is designed for use in a specific industry or niche market, the dataset might be limited to users who are in that specific group.

The evaluation itself might involve a combination of automated testing and manual review by content safety experts to ensure that the system is effectively identifying potentially harmful or inappropriate content. The results of the evaluation are then used to improve the system and to optimize its performance for real-world use.

This evaluation should be conducted in the context where you'll use the system, and with people who will interact with the system. Some best practices for evaluating Azure AI Content Safety include:

- Work with your analytics and research teams to collect ground truth evaluation data.
- Establish baseline accuracy, false positive and false negative rates.
- Choose an appropriate match severity level for your use case.
- Determine whether the error distribution is skewed towards specific groups of data or categories.
- Evaluation is likely to be an iterative process. For example, you can start with 50 rows or images for each category and then assess the false positive and false negative results.
- In addition to analyzing accuracy data, you can also analyze feedback from the people making judgments based on the system output.

Warning

**Content warning: Sample Content in Content Safety Studio.**

Content Safety Studio includes prepopulated data sets to enable you to test the system and tailor it to your requirements. These data sets contain objectionable content to enable this feature to function. This content should be reviewed with discretion. In some cases, image content will be blurred by default, and you can select a toggle to unblur the content.

### Best practices for evaluating and integrating Azure AI Content Safety

**Appropriate human oversight for the system is critical to ensure that it is being used effectively and responsibly.**This includes ensuring that the people who are responsible for oversight understand the system's intended uses, how to interact with the system effectively, how to interpret system behavior, and when and how to intervene in or override the system. Considerations such as UX and UI design and the use of severity levels can inform human oversight strategies and help prevent over-reliance on system outputs. For example, for a product like a content safety system, it is important to provide content moderators with the training and resources that they need to effectively oversee the system. This might involve providing access to training materials and documentation, as well as ongoing support from content safety experts.**Establish feedback channels for users and affected groups.**AI-powered products and features require ongoing monitoring and improvement. Establish channels to collect questions and concerns from users as well as from people who are affected by the system. For example, build feedback features into the user experience. Invite feedback on the usefulness and accuracy of outputs and give users a separate and clear path to report outputs that are problematic.
