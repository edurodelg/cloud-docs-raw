---
merged_at: 2026-01-25T15:32:35.905626
merged_files: 5
---

# Documentos Fusionados

Este archivo contiene 5 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: limited-access.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/limited-access -->

# Limited access for Azure Direct Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

As part of Microsoft's commitment to responsible AI, we have designed and operate Azure Direct Models (as defined in the [Product Terms](https://www.microsoft.com/licensing/terms/welcome/welcomepage)) with the intention of respecting the rights of individuals and society and fostering transparent human-computer interaction. For this reason, certain Azure Direct Models (or versions of them) are designated as Limited Access Services, and access and use are subject to eligibility criteria determined by Microsoft. Unless otherwise indicated in the service, all Azure customers are eligible for access to Azure Direct Models, and all uses consistent with the Product Terms and Code of Conduct are permitted, so customers are not required to submit a registration form unless they are: (a) accessing an Azure Direct Model designated as a Limited Access Service, or (b) requesting approval to modify Guardrails (previously content filters) and/or abuse monitoring for an Azure Direct Model.

Azure Direct Models are made available to customers under the terms governing their subscription to Microsoft Azure Services, including [Product Terms](https://www.microsoft.com/licensing/terms/welcome/welcomepage) such as the Universal License Terms applicable to Microsoft Generative AI Services and the product offering terms for the Azure Direct Model. Please review these terms carefully as they contain important conditions and obligations governing your use.

Azure OpenAI Service is made available to customers under the terms governing their subscription to Microsoft Azure Services, including such as the Universal License Terms applicable to Microsoft Generative AI Services and the product offering terms for Azure OpenAI. Please review these terms carefully as they contain important conditions and obligations governing your use of Azure OpenAI Service.

## Registration for modified Guardrails and/or abuse monitoring

All customers have the ability to configure severity thresholds on Guardrails (previously content filters), however, the modified Guardrails approval process is required to turn the Guardrails partially or fully off. Customers who wish to modify Guardrails and/or modify abuse monitoring are subject to additional eligibility criteria and requirements. At this time, modified Guardrails (previously content filters) and/or modified abuse monitoring for Azure Direct Models are available only to customers and partners managed by a Microsoft account team or under an eligible program, and are subject to additional requirements. Customers meeting these requirements can request approval for modified Guardrails and/or modified abuse monitoring using the following forms:

## Important links

[Register to modify Guardrails (previously content filters)](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUMlBQNkZMR0lFRldORTdVQzQ0TEI5Q1ExOSQlQCN0PWcu)(if needed)[Register to modify abuse monitoring](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUOE9MUTFMUlpBNk5IQlZWWkcyUEpWWEhGOCQlQCN0PWcu)(if needed)

Some advanced models from Azure Direct Models may have more stringent criteria for turning off abuse monitoring.

## Help and support

Frequently asked questions about Limited Access can be found on the [Foundry Tools Limited Access](/en-us/azure/ai-services/cognitive-services-limited-access) page. If you need help with Azure OpenAI, see the [Foundry Tools support options](/en-us/azure/ai-services/cognitive-services-support-options) page. Report abuse of Azure OpenAI [here](https://aka.ms/reportabuse).


---

<!-- DOCUMENTO FUSIONADO: customer-copyright-commitment.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment -->

# Customer Copyright Commitment Required Mitigations

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

Note

The requirements described below apply only to customers using Azure OpenAI in Microsoft Foundry Models ("Azure OpenAI") and other Covered Products with configurable Metaprompts or other safety systems ("Configurable GAI Services"). They do not apply to customers using other Covered Products including Copilots with safety systems that are fixed. The only Configurable GAI Services are Microsoft Copilot Studio and GitHub Copilot; the Universal Required Mitigations do not apply to these offerings, but service-specific mitigations apply instead.

The Customer Copyright Commitment ("CCC") is a provision in the Microsoft Product Terms that describes Microsoft's obligation to defend customers against certain third-party intellectual property claims relating to Output Content. For Azure OpenAI and any Configurable GAI Service, Customer also must have implemented all mitigations required by the Azure OpenAI documentation in the offering that delivered the Output Content that is the subject of the claim. The required mitigations to maintain CCC coverage are set forth below.

This page describes only the required mitigations necessary to maintain CCC coverage for Azure OpenAI and Configurable GAI Services. It is not an exhaustive list of requirements or mitigations required to use Azure OpenAI (or Configurable GAI Services) responsibly in compliance with the documentation. Azure OpenAI customers must comply with the [Code of Conduct](/en-us/legal/ai-code-of-conduct?context=%2Fazure%2Fcognitive-services%2Fopenai%2Fcontext%2Fcontext) at all times.

The mitigations below take effect on the dates indicated. For new Configurable GAI Services, features, models, or use cases, new CCC requirements will be posted and take effect at or following the launch of such Configurable GAI Service, feature, model, or use case. Otherwise, customers will have six months from the date of publication  to implement any new mitigations required to maintain coverage under the CCC. The Effective Date indicates when the mitigation must be deployed. If a customer tenders a claim for defense, the customer will be required to demonstrate compliance with all relevant requirements, both  and as listed in the Product Terms.

## Universal Required Mitigations

Universal required mitigations must be implemented to maintain CCC coverage for all offerings delivering Output Content from Azure OpenAI and Configurable GAI Services, with the exceptions of GitHub Offerings and Microsoft Copilot Studio. The requirements are set forth here:

**Azure OpenAI & Configurable GAI Services - Universal Required Mitigations:**

Category |
Required Mitigation |
Effective Date |
|---|---|---|
| Metaprompt | The customer offering must include a metaprompt directing the model to prevent copyright infringement in its output, for example, the sample metaprompt, "To Avoid Copyright Infringements" at:
|

[Red teaming large language models (LLMs)](/en-us/azure/ai-foundry/openai/concepts/red-teaming). More information on systematic measurement is at:[Overview of Responsible AI practices for Azure OpenAI models - Foundry Tools - Microsoft Learn.](overview?view=foundry-classic)## Additional Required Mitigations Per Azure OpenAI Use Case

Additional required mitigations are required to maintain CCC coverage for offerings delivering Output Content from Azure OpenAI, depending on what use cases the customer is using. As used below, “use case” refers to a major intended use of your application by your users. Use cases may have been indicated on a Limited Access Form. More information about use cases is available at: [Transparency Note for Azure OpenAI - Foundry Tools | Microsoft Learn](transparency-note?view=foundry-classic). Requirements are cumulative, meaning that the customer offering must include the required mitigations for all use cases. These additional requirements do not apply to Configurable GAI Services, only Azure OpenAI.

Not all content types can be generated by every application. The following required mitigations must be enabled for any use case described below. Azure OpenAI Guardrails (previously content filters) include protected material detection and Prompt Shield. Protected material detection can analyze both text and code. Different filters must be on depending on content type.

The required mitigations are set forth here:

**Azure OpenAI Only - Additional Required Mitigations Per Use Case**

**Text and Code Use Cases:**

Content type |
Use Case |
Category |
Required Mitigation |
Effective Date |
|---|---|---|---|---|
| Code generation | Code generation or transformation scenarios, or other open code generation scenarios | Guardrails (previously content filters) | The protected material code model must be configured on in either annotate or filter mode. If choosing to use annotate mode, customer must comply with any cited license provided for Output Content that is the subject of the claim. The jailbreak model (i.e., Prompt Shield for jailbreak attacks) must be configured on in filter mode. |
December 1, 2023 |
| If using the asynchronous filter feature, Output Content retroactively flagged as protected material code is not covered by the CCC, unless customer complies with its cited license. | May 21, 2024 | |||
| Text generation | Journalistic content, writing assistance, or other open text generation scenarios | Guardrails | The protected material text model must be configured on in filter mode. The jailbreak model (i.e., Prompt Shield for jailbreak attacks) must be configured on in filter mode. | December 1, 2023 |
| If using the asynchronous filter feature, Output Content retroactively flagged as protected material text is not covered by the CCC. | May 21, 2024 |

**Image generation models, OpenAI Whisper model, and all other use cases:**

No additional requirements.

## Required Mitigations for GitHub Offerings

The below are the only required mitigations that apply to GitHub Offerings, and separately took effect in the Product Terms on November 1, 2023.

**Required Mitigations for GitHub Offerings Only**

Category |
Required Mitigation |
Effective Date |
|---|---|---|
| GitHub Offerings | Either the Duplicate Detection filtering feature must be set to the "Block" setting, or, if using annotate mode, customers must comply with cited licenses. Customers can learn how to enable the Duplicate Detection filter at
|

## Required Mitigations for Microsoft Copilot Studio

The below are the only required mitigations that apply to Microsoft Copilot Studio.

**Required Mitigations for Copilot Studio Only**

Category |
Required Mitigation |
Effective Date |
|---|---|---|
| Bring your own model | If Customer chooses to connect to or incorporate a model hosted outside of Copilot Studio, the Output Content from such model is not covered by the CCC unless such model runs in Azure OpenAI and meets the required mitigations  for Azure OpenAI. | June 1, 2025 |


---

<!-- DOCUMENTO FUSIONADO: data-privacy.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy -->

# Data, privacy, and security for Azure Direct Models in Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

This article provides details regarding how data provided by you to Azure Direct Models in Microsoft Foundry are processed, used, and stored. Azure Direct Model means an AI model designated and deployed as an “Azure Direct Model” in Foundry, and includes Azure OpenAI models. Azure Direct Models store and process data to provide the service and to monitor for uses that violate the applicable product terms. Please also see [Microsoft Products and Services Data Protection Addendum](https://aka.ms/DPA), which governs data processing by Azure Direct Models. Foundry is an Azure service; [learn more](/en-us/compliance/regulatory/offering-home) about applicable Azure compliance offerings.

Important

Your prompts (inputs) and completions (outputs), your embeddings, and your training data:

- are NOT available to other customers.
- are NOT available to OpenAI or other Azure Direct Model providers.
- are NOT used by Azure Direct Model providers to improve their models or services.
- are NOT used to train any generative AI foundation models without your permission or instruction.
- Customer Data, Prompts, and Completions are NOT used to improve Microsoft or third-party products or services without your explicit permission or instruction.

Your fine-tuned Azure Direct Models are available exclusively for your use.

Foundry is an Azure service; Microsoft hosts the Azure Direct Models in Microsoft's Azure environment and Azure Direct Models do NOT interact with any services operated by Azure Direct Model providers, for example, OpenAI (e.g. ChatGPT, or the OpenAI API).

## What data does Foundry process to provide Azure Direct Models?

Foundry processes the following types of data to provide Azure Direct Models:

**Prompts and generated content**. When prompts are submitted by the user, content is generated by the service, via the completions, chat completions, images, and embeddings operations.**Uploaded data**. You can upload your own data for use with certain service features (e.g.,[fine-tuning](/en-us/azure/ai-foundry/openai/how-to/fine-tuning?pivots=programming-language-studio),[assistants API](/en-us/azure/ai-foundry/openai/how-to/batch?tabs=standard-input&pivots=programming-language-ai-studio),[batch processing](/en-us/azure/ai-foundry/openai/how-to/batch?tabs=standard-input&pivots=programming-language-ai-studio)) using the Files API or vector store.**Data for stateful entities**. When you use certain optional features of Azure Direct Models and Agents, such as the[Responses API](/en-us/azure/ai-foundry/openai/how-to/responses), the Threads feature of the[Assistants API](/en-us/azure/ai-foundry/openai/how-to/assistant), and Stored completions, the service creates a data store to persist message history and other content, in accordance with how you configure the feature.**Augmented data included with or via prompts**. When you use data associated with stateful entities, the service retrieves relevant data from a configured data store and augments the prompt to produce generations that are grounded with your data. Prompts may also be augmented with data retrieved from a source included in the prompt itself, such as a URL.**Training & validation data**. You can provide your own training data consisting of prompt-completion pairs for the purposes of[fine-tuning a model](/en-us/azure/ai-foundry/openai/how-to/fine-tuning?pivots=programming-language-studio).

## How does Foundry process data to provide Azure Direct Models?

The diagram below illustrates how your data is processed. This diagram covers several types of processing:

- How Foundry processes your prompts via inferencing with Azure Direct Models to generate content (including when additional data from a designated data source is added to a prompt using Azure OpenAI on your data, Assistants, or batch processing).
- How the Assistants feature stores data in connection with Messages, Threads, and Runs.
- How the Responses API feature stores data to persist message history.
- How the Batch feature processes your uploaded data.
- How Foundry creates a fine-tuned (custom) model with your uploaded data.
- How Foundry and Microsoft personnel analyze prompts and completions (text and image) for harmful content and for patterns suggesting the use of the service in a manner that violates the Code of Conduct or other applicable product terms.

As depicted in the diagram above, managed customers may [apply to modify abuse monitoring](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUOE9MUTFMUlpBNk5IQlZWWkcyUEpWWEhGOCQlQCN0PWcu).

### Generating completions, images or embeddings through inferencing

Azure Direct Models (base or fine-tuned) deployed in your Foundry resource process your input prompts and generate responses with text, images, or embeddings. Prompts and completions are evaluated in real time for harmful content types and content generation is filtered based on configured thresholds. Learn more at [Guardrails (previously content filters) overview](/en-us/azure/ai-foundry/openai/concepts/content-filter).

Prompts and responses are processed within the customer-specified [geography](https://azure.microsoft.com/explore/global-infrastructure/geographies/) (unless you are using a Global or DataZone deployment type), but may be processed between regions within the geography for operational purposes (including performance and capacity management). See below for information about location of processing when using a Global or DataZone deployment type.

**The models are stateless: no prompts or completions are stored in the model. Additionally, prompts and completions are not used to train, retrain, or improve the base models.**

### Understanding location of processing for "Global" and "Data zone" deployment types

In addition to standard deployments, Foundry offers Azure Direct Model deployment options labeled as 'Global' and 'DataZone.' For any [deployment type](/en-us/azure/ai-foundry/foundry-models/concepts/deployment-types) labeled 'Global,' prompts and responses may be processed in any geography where the relevant Azure Direct Model is deployed (learn more about [region availability of models](/en-us/azure/ai-foundry/openai/concepts/models#model-summary-table-and-region-availability)). For any deployment type labeled as 'DataZone,' prompts and responses may be processed in any geography within the specified data zone, as defined by Microsoft. If you create a DataZone deployment in a Foundry resource located in the United States, prompts and responses may be processed anywhere within the United States. If you create a DataZone deployment in a Foundry resource located in a European Union Member Nation, prompts and responses may be processed in that or any other European Union Member Nation. For both Global and DataZone deployment types, any data stored at rest, such as uploaded data, and including the abuse monitoring data store created for Global and DataZone deployments, is stored in the customer-designated geography. Only the location of processing is affected when a customer uses a Global deployment type or DataZone deployment type in Azure Direct Models; Azure data processing and compliance commitments remain applicable.

### Augmenting prompts to "ground" generated results "on your data"

The Azure OpenAI "on your data" feature lets you connect data sources to ground the generated results with your data. The data remains stored in the data source and location you designate; Azure OpenAI does not create a duplicate data store. When a user prompt is received, the service retrieves relevant data from the connected data source and augments the prompt. The model processes this augmented prompt and the generated content is returned as described above. Learn more about [how to use the On Your Data feature securely](/en-us/azure/ai-foundry/openai/how-to/on-your-data-configuration).

### Data storage for Azure Direct Models features

Some Azure Direct Models features store data in the service. This data is either uploaded by the customer, using the Files API or vector store, or is automatically stored in connection with certain stateful entities such as the Responses API, the Threads feature of the Assistants API, and Stored completions. Data stored for such features:

- Is stored at rest in the Foundry resource in the customer's Azure tenant, within the same
[geography](https://azure.microsoft.com/explore/global-infrastructure/geographies/)as the resource; - Is always encrypted at rest with Microsoft’s AES-256-encryption by default, with the option of using a customer managed key (certain preview features may not support customer-managed keys). Microsoft-managed keys are always used to ensure baseline encryption for all stored data.
- Can be deleted by the customer at any time.

Note

Models or features in preview might not support all of the above conditions.

Stored data may be used with the following service features/capabilities:

**Creating a customized (fine-tuned) model**. Learn more about[how fine-tuning works](/en-us/azure/ai-foundry/openai/how-to/fine-tuning?tabs=turbo%2Cpython-new&pivots=programming-language-studio). Fine-tuned models are exclusively available to the customer whose data was used to create the fine-tuned model, are encrypted at rest (when not deployed for inferencing), and can be deleted by the customer at any time. Training data uploaded for fine-tuning is not used to train any generative AI foundation models without your permission or instruction.**Batch processing**. Learn more about[how batch processing works](https://aka.ms/aoai-batch-how-to). Batch processing is a Global deployment type; data stored at rest remains in the designated Azure geography until processing capacity becomes available; processing may occur in any geography where the relevant Azure Direct Model is deployed (learn more about[region availability of models](/en-us/azure/ai-foundry/openai/concepts/models#model-summary-table-and-region-availability)).**Responses API**. Learn more about how the[Responses API](/en-us/azure/ai-foundry/openai/how-to/responses?tabs=python-secure)works. This API stores message history and other content related to message history. This is required for multi-turn conversations and workflows.**Assistants API (preview)**. Learn more about[how the Assistants API works](/en-us/azure/ai-foundry/openai/concepts/assistants). Some features of Assistants, such as Threads, store message history and other content.**Stored completions (preview)**. Stored completions stores input-output pairs from the customer’s deployed Azure OpenAI models such as GPT-4o through the chat completions API and displays the pairs in the[Foundry portal](https://ai.azure.com/). This allows customers to build datasets with their production data, which can then be used for evaluating or fine-tuning models (as permitted in applicable Product Terms).

### Preventing abuse

To reduce the risk of abusive or harmful use, Azure Direct Models includes abuse monitoring features. To learn more about abuse monitoring, see [abuse monitoring](/en-us/azure/ai-foundry/openai/concepts/abuse-monitoring).

Safety evaluations of fine-tuned models evaluate a fine-tuned model for potentially harmful responses using [Azure’s risk and safety metrics](/en-us/azure/ai-studio/concepts/evaluation-metrics-built-in#risk-and-safety-metrics). Only the resulting assessment (deployable or not deployable) is logged by the service.

The Azure Direct Models abuse monitoring system is designed to detect and mitigate instances of recurring content and/or behaviors that suggest use of the service in a manner that may violate the [code of conduct](/en-us/legal/ai-code-of-conduct?context=%2Fazure%2Fcognitive-services%2Fopenai%2Fcontext%2Fcontext) or other applicable product terms. As described [here](/en-us/azure/ai-foundry/openai/concepts/abuse-monitoring), the system employs algorithms and heuristics to detect indicators of potential abuse. When these indicators are detected, a sample of customer’s prompts and completions may be selected for review. Review is conducted by automated means including by AI models such as LLMs by default, with additional reviews by human reviewers as necessary. Detailed information about automated review and human review is available at [Abuse monitoring](/en-us/azure/ai-foundry/openai/concepts/abuse-monitoring).

For automated review, customer’s prompts and completions are not stored by the system or used to train the AI models or other systems. The abuse monitoring data store where prompts and completions are stored for human review is logically separated by customer resource (each request includes the resource ID of the customer’s Foundry resource). A separate data store is located in each geography in which the Azure Direct Model is available, and a customer’s prompts and generated content are stored in the Azure geography where the customer’s Foundry resource is deployed, within the Azure Direct Models service boundary. Human reviewers assessing potential abuse can access prompts and completions data only when that data has already been flagged by the abuse monitoring system, or when the prompts and completions are part of a potentially abusive pattern of use. The human reviewers are authorized Microsoft employees who access the data via point wise queries using request IDs, Secure Access Workstations (SAWs), and Just-In-Time (JIT) request approval granted by team managers. For Azure Direct Models deployed in the European Economic Area, the authorized Microsoft employees are located in the European Economic Area.

If the customer has been approved for modified abuse monitoring (learn more at [Abuse Monitoring](/en-us/azure/ai-foundry/openai/concepts/abuse-monitoring))), the data storage and human review process described above is not performed. However, automated review may still be conducted, leveraging algorithms including AI models that review prompts and completions at the time provided or generated, as applicable. If such automated review detects content potentially indicating severe or recurring abuse in the customer’s subscription, the customer may be subject to limitations on access, as provided in the Product Terms for Responsible Use of Microsoft AI Services. The customer may also be asked to agree to have abuse monitoring with human review turned on to reduce the risk of future limitations on access (e.g., throttling and/or suspension of the account or subscription where abuse has been detected).

Note

Azure Preview features, including Azure Direct Models in preview, may employ different privacy practices, including with respect to abuse monitoring. Previews may be subject to supplemental terms at: [Supplemental Terms of use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

### Preventing harmful content generation

Azure Direct Models include a system designed to detect and prevent the output of harmful content. To learn more about Guardrails (previously content filters), see [Guardrails](/en-us/azure/ai-services/openai/concepts/content-filter).

Guardrails occurs synchronously as the service processes prompts to generate content as described above and [here](/en-us/azure/ai-foundry/openai/concepts/content-filter). No prompts or generated content are stored in the content classifier models, and prompts and outputs are not used to train any generative AI foundation models without your permission or instruction.

## How can a customer verify if data storage for abuse monitoring is off?

There are two ways for customers, once approved to turn off abuse monitoring, to verify that data storage for abuse monitoring has been turned off in their approved Azure subscription:

- Using the Azure portal, or
- Azure CLI (or any management API).

Note

The value of "false" for the "ContentLogging" attribute appears only if data storage for abuse monitoring is turned off. Otherwise, this property will not appear in either Azure portal or Azure CLI's output.

### Prerequisites

- Sign into Azure
- Select the Azure Subscription which hosts the Foundry resource.
- Navigate to the
**Overview**page of the Foundry resource.

Go to the resource Overview page

Click on the

**JSON view**link on the top right corner as shown in the image below.

There will be a value in the Capabilities list called "ContentLogging" which will appear and be set to FALSE when logging for abuse monitoring is off.

```
{
"name":"ContentLogging",
"value":"false"
}
```


To learn more about Microsoft's privacy and security commitments see the [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/CloudServices/Azure/default.aspx).

## Change log

| Date | Changes |
|---|---|
| 3 October 2025 | Expanded document to Azure Direct Models; separated Guardrails (previously content filters) and abuse monitoring sections; added clarifications on abuse monitoring and severe or recurring abuse. |
| 17 December 2024 | Added information about data processing and storage in connection with new Stored completions feature; added language clarifying that Azure OpenAI features in preview may not support all data storage conditions; removed "preview" designation for Batch processing |
| 18 November 2024 | Added information about location of data processing for new ‘Data zone’ deployment types; added information about new AI review of prompts and completions as part of preventing abuse and generation of harmful content |
| 4 September 2024 | Added information (and revised existing text accordingly) about data processing for new features including Assistants API (preview), Batch (preview), and Global Deployments; revised language related to location of data processing, in accordance with
|

[Azure OpenAI Service abuse monitoring](/en-us/azure/ai-foundry/openai/concepts/abuse-monitoring). Added summary note. Updated and streamlined content and updated diagrams for additional clarity. added change log## See also

[Code of conduct for Azure OpenAI Service integrations](/en-us/legal/ai-code-of-conduct?context=%2Fazure%2Fcognitive-services%2Fopenai%2Fcontext%2Fcontext)[Overview of Responsible AI practices for Azure OpenAI models](/en-us/azure/ai-foundry/responsible-ai/openai/overview)[Transparency note and use cases for Azure OpenAI Service](transparency-note?view=foundry-classic)[Data Residency in Azure](https://azure.microsoft.com/explore/global-infrastructure/data-residency/)- Compare
[Azure OpenAI in Azure Government](/en-us/azure/ai-foundry/openai/azure-government) [Limited access to Azure OpenAI Service](limited-access?view=foundry-classic)- Report abuse of Azure OpenAI Service through the
[Report Abuse Portal](https://msrc.microsoft.com/report/abuse) - Report problematic to
[cscraireport@microsoft.com](mailto:cscraireport@microsoft.com)


---

<!-- DOCUMENTO FUSIONADO: overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/overview -->

# Overview of responsible AI practices for Azure OpenAI models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

Many of the Azure OpenAI models are generative AI models that demonstrate improvements in advanced capabilities such as content and code generation, summarization, and search. With many of these improvements also come increased responsible AI challenges related to harmful content, manipulation, human-like behavior, privacy, and more. For more information about the capabilities, limitations, and appropriate use cases for these models, review the [Transparency Note](/en-us/azure/ai-foundry/responsible-ai/openai/transparency-note).

In addition to the Transparency Note, we provide technical recommendations and resources to help customers design, develop, deploy, and use AI systems that implement the Azure OpenAI models responsibly. Our recommendations are grounded in the [Microsoft Responsible AI Standard](https://aka.ms/RAI), which sets policy requirements that our own engineering teams follow. Much of the content of the Standard follows a pattern, asking teams to identify, measure, and mitigate potential harms, and plan for how to operate the AI system. In alignment with those practices, these recommendations are organized into four stages:

**Identify**: Identify and prioritize potential harms that could result from your AI system through iterative red-teaming, stress-testing, and analysis.**Measure**: Measure the frequency and severity of those harms by establishing clear metrics, creating measurement test sets, and completing iterative, systematic testing (both manual and automated).**Mitigate**: Mitigate harms by implementing tools and strategies such as[prompt engineering](/en-us/azure/ai-foundry/openai/concepts/prompt-engineering)and using our[Guardrails (previously content filters)](/en-us/azure/ai-foundry/openai/concepts/content-filter). Repeat measurement to test effectiveness after implementing mitigations.**Operate**: Define and execute a deployment and operational readiness plan.

In addition to their correspondence to the Microsoft Responsible AI Standard, these stages correspond closely to the functions in the [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework).

## Identify

The first stage of the Responsible AI lifecycle is identifying potential harms that could occur in or be caused by an AI system. The earlier you begin to identify potential harms, the more effective you can be at mitigating them. When assessing potential harms, develop an understanding of the types of harms that could result from using the Azure OpenAI Service in your specific contexts. This section provides recommendations and resources you can use to identify harms through an impact assessment, iterative red team testing, stress-testing, and analysis. Red teaming and stress-testing are approaches where a group of testers intentionally probe a system to identify its limitations, risk surface, and vulnerabilities.

These steps produce a prioritized list of potential harms for each specific scenario.

**Identify harms that are relevant**for your specific model, application, and deployment scenario.- Identify potential harms associated with the model and model capabilities (for example, GPT-3 model versus GPT-4 model) that you use in your system. Each model has different capabilities, limitations, and risks.
- Identify any other harms or increased scope of harm presented by the intended use of the system you're developing. Consider using a
[Responsible AI Impact Assessment](https://aka.ms/rai)to identify potential harms.- For example, consider an AI system that summarizes text. Some uses of text generation are lower risk than others. If the system is used in a healthcare domain for summarizing doctor's notes, the risk of harm arising from inaccuracies is higher than if the system is summarizing online articles.


**Prioritize harms based on elements of risk such as frequency and severity**. Assess the level of risk for each harm and the likelihood of each risk occurring to prioritize the list of harms you identified. Consider working with subject matter experts and risk managers within your organization and with relevant external stakeholders when appropriate.**Conduct red team testing and stress testing**starting with the highest priority harms. Develop a better understanding of whether and how the identified harms occur in your scenario. Identify new harms you didn't initially anticipate.**Share this information with relevant stakeholders**by using your organization's internal compliance processes.

At the end of this Identify stage, you have a documented, prioritized list of harms. When new harms and new instances of harms emerge through further testing and use of the system, update and improve this list.

## Measure

After you identify a prioritized list of harms, develop an approach for systematic measurement of each harm and conduct evaluations of the AI system. You can use manual and automated approaches to measurement. We recommend you use both approaches, starting with manual measurement.

Manual measurement is useful for:

- Measuring progress on a small set of priority issues. When mitigating specific harms, it's often most productive to keep manually checking progress against a small dataset until the harm is no longer observed before moving to automated measurement.
- Defining and reporting metrics until automated measurement is reliable enough to use alone.
- Spot-checking periodically to measure the quality of automatic measurement.

Automated measurement is useful for:

- Measuring at a large scale with increased coverage to provide more comprehensive results.
- Ongoing measurement to monitor for any regression as the system, usage, and mitigations evolve.

The following recommendations help you measure your AI system for potential harms. We recommend you first complete this process manually and then develop a plan to automate the process:

**Create inputs that are likely to produce each prioritized harm:**Create measurement sets by generating many diverse examples of targeted inputs that are likely to produce each prioritized harm.**Generate System Outputs:**Pass in the examples from the measurement sets as inputs to the system to generate system outputs. Document the outputs.**Evaluate System Outputs and Report Results to Relevant Stakeholders****Define clear metrics.**For each intended use of your system, establish metrics that measure the frequency and degree of severity of each potentially harmful output. Create clear definitions to classify outputs that you consider harmful or problematic in the context of your system and scenario, for each type of prioritized harm you identified.**Assess the outputs**against the clear metric definitions. Record and quantify the occurrences of harmful outputs. Repeat the measurements periodically to assess mitigations and monitor for any regression.**Share this information with relevant stakeholders**by using your organization's internal compliance processes.


At the end of this measurement stage, you should have a defined measurement approach to benchmark how your system performs for each potential harm as well as an initial set of documented results. As you continue implementing and testing mitigations, refine the metrics and measurement sets. For example, add metrics for new harms that you initially didn't anticipate. Update the results.

## Mitigate

Mitigating harms presented by large language models such as the Azure OpenAI models requires an iterative, layered approach that includes experimentation and continual measurement. We recommend developing a mitigation plan that encompasses four layers of mitigations for the harms you identified in the earlier stages of this process:

- At the
**model level**, understand the model(s) you use and what fine-tuning steps the model developers take to align the model toward its intended uses and to reduce the risk of potentially harmful uses and outcomes.- For example, developers use reinforcement learning methods as a responsible AI tool to better align GPT-4 toward the designers' intended goals.

- At the
**safety system level**, understand the platform level mitigations that the developers implement, such as the[Azure OpenAI Guardrails (previously content filters)](/en-us/azure/ai-foundry/openai/concepts/content-filter)which help to block the output of harmful content. - At the
**application level**, application developers can implement metaprompt and user-centered design and user experience mitigations. Metaprompts are instructions you provide to the model to guide its behavior. Their use can make a critical difference in guiding the system to behave in accordance with your expectations. User-centered design and user experience (UX) interventions are also key mitigation tools to prevent misuse and overreliance on AI. - At the
**positioning level**, educate the people who use or are affected by your system about its capabilities and limitations.

The following sections provide specific recommendations to implement mitigations at the different layers. Not all of these mitigations are appropriate for every scenario. Conversely, these mitigations might be insufficient for some scenarios. Give careful consideration to your scenario and the prioritized harms you identified. As you implement mitigations, develop a process to **measure and document their effectiveness** for your system and scenario.

**Model level Mitigations:**Review and identify which Azure OpenAI base model best suits the system you're building. Educate yourself about its capabilities, limitations, and any measures taken to reduce the risk of the potential harms you identified. For example, if you use GPT-4, in addition to reading this Transparency Note, review OpenAI's[GPT-4 System Card](https://cdn.openai.com/papers/gpt-4-system-card.pdf)that explains the safety challenges presented by the model and the safety processes that OpenAI adopted to prepare GPT-4 for deployment. Experiment with different versions of the model(s) (including through red teaming and measuring) to see how the harms present differently.**Safety System Level Mitigations:**Identify and evaluate the effectiveness of platform level solutions such as the[Azure OpenAI Guardrails (previously content filters)](/en-us/azure/ai-foundry/openai/concepts/content-filter)to help mitigate the potential harms that you identified.**Application Level Mitigations:**Prompt engineering, including**metaprompt tuning, can be an effective mitigation**for many different types of harm. Review and implement metaprompt (also called the "system message" or "system prompt") guidance and best practices documented[here](/en-us/azure/ai-foundry/openai/concepts/prompt-engineering).Implement the following user-centered design and user experience (UX) interventions, guidance, and best practices to guide users to use the system as intended and to prevent overreliance on the AI system:

**Review and edit interventions:**Design the user experience (UX) to encourage people who use the system to review and edit the AI-generated outputs before accepting them (see[HAX G9](https://www.microsoft.com/en-us/haxtoolkit/library/?taxonomy_guideline-term%5B%5D=11): Support efficient correction).**Highlight potential inaccuracies in the AI-generated outputs**(see[HAX G2](https://www.microsoft.com/en-us/haxtoolkit/library/?taxonomy_guideline-term%5B%5D=4): Make clear how well the system can do what it can do), both when users first start using the system and at appropriate times during ongoing use. In the first run experience (FRE), notify users that AI-generated outputs might contain inaccuracies and that they should verify information. Throughout the experience, include reminders to check AI-generated output for potential inaccuracies, both overall and in relation to specific types of content the system might generate incorrectly. For example, if your measurement process determines that your system has lower accuracy with numbers, mark numbers in generated outputs to alert the user and encourage them to check the numbers or seek external sources for verification.**User responsibility.**Remind people that they're accountable for the final content when they're reviewing AI-generated content. For example, when offering code suggestions, remind the developer to review and test suggestions before accepting.**Disclose AI's role in the interaction.**Make people aware that they're interacting with an AI system (as opposed to another human). Where appropriate, inform content consumers that content is partly or fully generated by an AI model. Such notices might be required by law or applicable best practices. They can reduce inappropriate reliance on AI-generated outputs and can help consumers use their own judgment about how to interpret and act on such content.**Prevent the system from anthropomorphizing.**AI models might output content containing opinions, emotive statements, or other formulations that could imply that they're human-like. Such content could be mistaken for a human identity. Such content could mislead people to think that a system has certain capabilities when it doesn't. Implement mechanisms that reduce the risk of such outputs or incorporate disclosures to help prevent misinterpretation of outputs.**Cite references and information sources.**If your system generates content based on references sent to the model, clearly citing information sources helps people understand where the AI-generated content is coming from.**Limit the length of inputs and outputs, where appropriate.**Restricting input and output length can reduce the likelihood of producing undesirable content, misuse of the system beyond its intended uses, or other harmful or unintended uses.**Structure inputs and/or system outputs.**Use[prompt engineering](/en-us/azure/ai-foundry/openai/concepts/prompt-engineering)techniques within your application to structure inputs to the system to prevent open-ended responses. You can also limit outputs to be structured in certain formats or patterns. For example, if your system generates dialog for a fictional character in response to queries, limit the inputs so that people can only query for a predetermined set of concepts.**Prepare pre-determined responses.**There are certain queries to which a model might generate offensive, inappropriate, or otherwise harmful responses. When harmful or offensive queries or responses are detected, you can design your system to deliver a predetermined response to the user. Predetermined responses should be crafted thoughtfully. For example, the application can provide prewritten answers to questions such as "who/what are you?" to avoid having the system respond with anthropomorphized responses. You can also use predetermined responses for questions like, "What are your terms of use?" to direct people to the correct policy.**Restrict automatic posting on social media.**Limit how people can automate your product or service. For example, you might choose to prohibit automated posting of AI-generated content to external sites (including social media), or to prohibit the automated execution of generated code.**Bot detection.**Devise and implement a mechanism to prohibit users from building an API on top of your product.

**Positioning Level Mitigations:****Be appropriately transparent.**Provide the right level of transparency to people who use the system, so that they can make informed decisions around the use of the system.**Provide system documentation.**Produce and provide educational materials for your system, including explanations of its capabilities and limitations. For example, this content could be in the form of a "learn more" page accessible via the system.**Publish user guidelines and best practices.**Help users and stakeholders use the system appropriately by publishing best practices, for example on prompt crafting, reviewing generations before accepting them, and so on. Such guidelines can help people understand how the system works. When possible, incorporate the guidelines and best practices directly into the UX.


As you implement mitigations to address potential identified harms, develop a process for ongoing measurement of the effectiveness of such mitigations. Document measurement results. Review those measurement results to continually improve the system.

## Operate

After you put measurement and mitigation systems in place, define and execute a deployment and operational readiness plan. This stage includes completing appropriate reviews of your system and mitigation plans with relevant stakeholders, establishing pipelines to collect telemetry and feedback, and developing an incident response and rollback plan.

Consider the following recommendations for deploying and operating a system that uses the Azure OpenAI service with appropriate, targeted harms mitigations:

Work with compliance teams within your organization to understand what types of reviews are required for your system and when to complete them. Reviews might include legal review, privacy review, security review, accessibility review, and others.

Develop and implement the following components:

**Phased delivery plan.**Launch systems that use the Azure OpenAI service gradually with a phased delivery approach. This approach gives a limited set of people the opportunity to try the system, provide feedback, report issues and concerns, and suggest improvements before the system is released more widely. It also helps you manage the risk of unanticipated failure modes, unexpected system behaviors, and unexpected concerns being reported.**Incident response plan.**Develop an incident response plan and evaluate the time needed to respond to an incident.**Rollback plan.**Ensure you can roll back the system quickly and efficiently if an unanticipated incident occurs.**Immediate action for unanticipated harms.**Build the necessary features and processes to block problematic prompts and responses as they're discovered and as close to real-time as possible. When unanticipated harms occur, block the problematic prompts and responses as quickly as possible. Develop and deploy appropriate mitigations. Investigate the incident and implement a long-term solution.**Mechanism to block people who misuse your system.**Develop a mechanism to identify users who violate your content policies (for example, by generating hate speech) or are otherwise using your system for unintended or harmful purposes. Take action against further abuse. For example, if a user frequently uses your system to generate content that is blocked or flagged by content safety systems, consider blocking them from further use of your system. Implement an appeal mechanism where appropriate.**Effective user feedback channels.**Implement feedback channels through which stakeholders (and the general public, if applicable) can submit feedback or report issues with generated content or that otherwise arise during their use of the system. Document how you process, consider, and address such feedback. Evaluate the feedback and work to improve the system based on user feedback. One approach could be to include buttons with generated content that allow users to identify content as "inaccurate," "harmful," or "incomplete." This approach could provide a more widely used, structured, and feedback signal for analysis.**Telemetry data.**Identify and record (consistent with applicable privacy laws, policies, and commitments) signals that indicate user satisfaction or their ability to use the system as intended. Use telemetry data to identify gaps and improve the system.


This document is not intended to be, and should not be construed as providing, legal advice. The jurisdiction in which you're operating may have various regulatory or legal requirements that apply to your AI system. Consult a legal specialist if you are uncertain about laws or regulations that might apply to your system, especially if you think those might impact these recommendations. Be aware that not all of these recommendations and resources are appropriate for every scenario, and conversely, these recommendations and resources may be insufficient for some scenarios.

## Learn more about responsible AI

[Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai)[Microsoft responsible AI resources](https://www.microsoft.com/ai/responsible-ai-resources)[Microsoft Azure Learning courses on responsible AI](/en-us/training/paths/responsible-ai-business-principles/)


---

<!-- DOCUMENTO FUSIONADO: transparency-note.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/transparency-note -->

# Transparency note for Azure OpenAI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Non-English translations are provided for convenience only. Please consult the [ EN-US version of this document](/en-us/azure/ai-foundry/responsible-ai/openai/customer-copyright-commitment) for the definitive version.

## What is a transparency note?

An AI system includes not only the technology, but also the people who use it, the people who are affected by it, and the environment in which it's deployed. Creating a system that is fit for its intended purpose requires an understanding of how the technology works, what its capabilities and limitations are, and how to achieve the best performance. Microsoft's Transparency Notes are intended to help you understand how our AI technology works, the choices system owners can make that influence system performance and behavior, and the importance of thinking about the whole system, including the technology, the people, and the environment. You can use Transparency Notes when developing or deploying your own system, or share them with the people who will use or be affected by your system.

Microsoft's Transparency Notes are part of a broader effort at Microsoft to put our AI Principles into practice. To find out more, see the [Microsoft's AI principles](https://www.microsoft.com/ai/responsible-ai).

## The basics of the Azure OpenAI Models

Azure OpenAI provides customers with a fully managed Foundry Tool that lets developers and data scientists apply OpenAI's powerful models including models that can generate natural language, code, and images. Within the Azure OpenAI Service, the OpenAI models are integrated with Microsoft-developed Guardrails (previously content filters) and abuse detection models. Learn more about Guardrails (previously content filters) [here](/en-us/azure/ai-foundry/openai/concepts/content-filter) and abuse detection [here](/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy).

### Introduction

| Model group | Text / code | Vision | Audio / Speech |
|---|---|---|---|
| GPT-3 & Codex | ✅ | ||
| DALL-E 2 & 3 | ✅ | ||
| GPT-image-1 | ✅ | ||
| Whisper | ✅ | ||
| GPT-4 Turbo with Vision | ✅ | ✅ | |
| GPT-4o GPT-4o-mini |
✅ | ✅ | ✅ |
| GPT-4.1 GPT-4.1-mini GPT-4.1-nano |
✅ | ✅ | |
| GPT-4.5 | ✅ | ✅ | |
| GPT-5 | ✅ | ✅ | |
| GPT-5.1-Codex-Max | ✅ | ✅ | |
| GPT-oss-120b | ✅ | ||
| o1 series | ✅ | ✅ | |
| o3/o3-pro | ✅ | ✅ | |
| o3-mini | ✅ | ||
o4-mini/codex-mini1 |
✅ | ✅ | |
| o3-deep-research o4-mini-deep-research |
✅ | ||
| computer-use-preview | ✅ | ✅ |

1`codex-mini`

is a fine-tuned version of `o4-mini`

specifically for use in Codex CLI. For more information, please see [OpenAI's documentation](https://platform.openai.com/docs/models/codex-mini-latest).

Select the tabs to see content for the relevant model type.

As part of the fully managed Azure OpenAI Service, the **GPT-3** models analyze and generate natural language, Codex models analyze and generate code and plain text code commentary, and **GPT-4** and **reasoning models** (including o-series models and GPT-5) can understand and generate natural language and code. These models use an autoregressive architecture, meaning they use data from prior observations to predict the most probable next word. This process is then repeated by appending the newly generated content to the original text to produce the complete generated response. Because the response is conditioned on the input text, these models can be applied to various tasks simply by changing the input text.

The GPT-3 series of models are pretrained on a wide body of publicly available free text data. This data is sourced from a combination of web crawling (specifically, a filtered version of [Common Crawl](https://commoncrawl.org/the-data/), which includes a broad range of text from the internet and comprises 60 percent of the weighted pretraining dataset) and higher-quality datasets, including an expanded version of the WebText dataset, two internet-based books corpora and English-language Wikipedia. The GPT-4 base model was trained using publicly available data (such as internet data) and data that was licensed by OpenAI. The model was fine-tuned using reinforcement learning with human feedback (RLHF).

The Computer Use (Preview) model accepts text input on the first turn, and screenshot image on the second and following turns, and outputs commands to the keyboard and mouse. The Computer Use model and the Computer Use Tool enable developers to build agentic AI systems.

Learn more about the training and modeling techniques in OpenAI's [GPT-3](https://arxiv.org/abs/2005.14165), [GPT-4](https://arxiv.org/abs/2303.08774), and [Codex](https://arxiv.org/abs/2107.03374) research papers.

**Fine tuning** refers to using *Supervised Fine Tuning* to adjust a base model's weights to provide better responses based on a provided training set. All use cases and considerations for large language models apply to fine-tuned models, but there are additional considerations as well.

Important

Fine-tuning is only available for text and code models, not vision or speech models.

### Key terms

Term |
Definition |
|---|---|
| Prompt | The text you send to the service in the API call. This text is then input into the model. For example, one might input the following prompt:`Convert the questions to a command:` `Q: Ask Constance if we need some bread` `A: send-msg 'find constance' Do we need some bread?` `Q: Send a message to Greg to figure out if things are ready for Wednesday.` `A:` |
| Completion or Generation | The text Azure OpenAI outputs in response. For example, the service may respond with the following answer to the above prompt: `send-msg 'find greg' figure out if things are ready for Wednesday.` |
| Token | Azure OpenAI processes text by breaking it down into tokens. Tokens can be words or just chunks of characters. For example, the word `hamburger` gets broken up into the tokens `ham` , `bur` and `ger` , while a short and common word like `pear` is a single token. Many tokens start with a whitespace, for example ` hello` and ` bye` . |
| Fine tuning | Supervised fine-tuning (SFT), reinforcement fine-tuning (RFT), and direct preference optimization (DPO, or preference fine-tuning) for large language models refer to the process of taking a pre-trained language model, often trained on a massive dataset, and further training it on a more specific task with labeled data. This involves adjusting the weights of the model using this smaller, specific dataset so that the model becomes more specialized in the tasks it can perform, enhancing its performance and accuracy. |
| Model Weights | Model weights are parameters within the model that are learned from the data during the training process. They determine the output of the model for a given input. These weights are adjusted in response to the error the model made in its predictions, with the aim of minimizing this error. |
| Ungrounded content | Content that is generated by the model that is non-factual or inaccurate from what was present in the source materials. |
| Agentic AI systems | Autonomous AI systems that sense and act upon their environment to achieve goals. |
| Autonomy | The ability to independently execute actions and exercise control over system behavior with limited or no direct human supervision. |
| Computer Use tool | A tool that when used with the Computer Use model captures mouse and keyboard actions generated by the mode and directly translates them into executable commands. This makes it possible for developers to automate computer use tasks. |
| Deep research | A fine-tuned version of the o-series reasoning models that is designed for deep research tasks. It takes a high-level query and returns a structured, citation-rich report by leveraging an agentic model capable of decomposing the task, performing web searches, and synthesizing results. |

## Capabilities

The reasoning models, GPT-4, GPT-3, Codex models, and Azure OpenAI evaluation use natural language instructions and examples in the prompt to identify the task. The model then completes the task by predicting the most probable next text. This technique is known as "in-context" learning. These models are not retrained during this step but instead give predictions based on the context you include in the prompt.

There are three main approaches for in-context learning. These approaches vary based on the amount of task-specific data that is given to the model:

**Few-shot** : In this case, a user includes several examples in the prompt that demonstrate the expected answer format and content. The following example shows a few-shot prompt providing multiple examples:

```
Convert the questions to a command:
Q: Ask Constance if we need some bread
A: send-msg `find constance` Do we need some bread?
Q: Send a message to Greg to figure out if things are ready for Wednesday.
A: send-msg `find greg` Is everything ready forWednesday?
Q: Ask Ilya if we're still having our meeting thisevening
A: send-msg `find ilya` Are we still having a meetingthis evening?
Q: Contact the ski store and figure out if I can getmy skis fixed before I leave on Thursday
A: send-msg `find ski store` Would it be possible toget my skis fixed before I leave on Thursday?
Q: Thank Nicolas for lunch
A: send-msg `find nicolas` Thank you for lunch!
Q: Tell Constance that I won't be home before 19:30tonight — unmovable meeting.
A: send-msg `find constance` I won't be home before19:30 tonight. I have a meeting I can't move.
Q: Tell John that I need to book an appointment at10:30
A:
```


The number of examples typically ranges from 0 to 100 depending on how many can fit in the maximum input length for a single prompt. Few-shot learning enables a major reduction in the amount of task-specific data required for accurate predictions.

**One-shot** : This case is the same as the few-shot approach except only one example is provided. The following example shows a one-shot prompt:

```
Convert the questions to a command:
Q: Ask Constance if we need some bread
A: send-msg `find constance` Do we need some bread?
Q: Send a message to Greg to figure out if things are ready for Wednesday.
A:
```


**Zero-shot**: In this case, no examples are provided to the model and only the task request is provided. The following example shows a zero-shot prompt:

```
Convert the question to a command:
Q: Ask Constance if we need some bread
A:
```


**Chain-of-thought** : Azure OpenAI's reasoning models have advanced reasoning capabilities using chain-of-thought (CoT) techniques. CoT techniques generate intermediate reasoning steps before providing a response, enabling them to address more complex challenges through step-by-step problem solving. o1 demonstrates improvements in benchmarks for reasoning-heavy domains such as research, strategy, science, coding and math, among others. These models have safety improvements from advanced reasoning capabilities, with the ability to reason through and apply safety rules more effectively. This results in better performance alongside safety benchmarks such as generating illicit advice, choosing stereotyped responses, and succumbing to known jailbreaks.

For greater detail on this family of models’ capabilities, see the [OpenAI o1 System Card](https://cdn.openai.com/o1-system-card-20241205.pdf), [o3-mini System Card](https://openai.com/index/o3-mini-system-card/), [o3/o4-mini System Card](https://openai.com/index/o3-o4-mini-system-card/), [Deep Research System Card](https://openai.com/index/deep-research-system-card/), and [GPT-5 System Card](https://openai.com/index/gpt-5-system-card/).

**Azure OpenAI Evaluation**

The evaluation of large language models is a critical step in measuring their performance across various tasks and dimensions. This task is especially important for fine-tuned models, where assessing the performance gains (or losses) from training is crucial. Without thorough evaluations, it can become challenging to understand how different versions of the model may impact your specific application.

Azure OpenAI Evaluation is a UI-based experience to evaluate data, including generated datasets from an Azure OpenAI deployment, or other manually curated files.

Azure OpenAI Evaluation has an optional step of generating responses. If the user opts into this step, we provide a prompt (System/User Message) to instruct the model how to generate responses.

Azure OpenAI Evaluation includes 9 categories of tests to score results. Some require ground truth data (like factuality), while others do not (schema validation). Graders are a mixture of CPU-based and model-based. Here is the list of testing criteria: Factuality, Sentiment, Valid JSON or XML, Criteria Match, Custom Prompt, Semantic Similarity, Contains string, Matches Schema and Text quality.

**Text-to-action**

The Computer Use (Preview) model enables text-to-action capabilities, allowing users to provide natural language instructions that the model translates into actionable steps within graphical user interfaces. Given a command like "Fill out the customer support form with this information," the model identifies the relevant fields, inputs the correct data, and submits the form. It can navigate web interfaces, extract and input structured or unstructured data, automate workflows, and enforce compliance with security policies. By understanding intent and executing actions accordingly, it streamlines business operations, making automation more accessible and efficient.

## Use cases

### Intended uses

Text models can be used in multiple scenarios. The following list isn't comprehensive, but it illustrates the diversity of tasks that can be supported for models with appropriate mitigations:

**Chat and conversation interaction**: Users can interact with a conversational agent that responds with responses drawn from trusted documents such as internal company documentation or tech support documentation. Conversations must be limited to answering scoped questions.**Chat and conversation creation**: Users can create a conversational agent that responds with responses drawn from trusted documents such as internal company documentation or tech support documentation. Conversations must be limited to answering scoped questions.**Code generation or transformation scenarios**: For example, converting one programming language to another, generating docstrings for functions, converting natural language to SQL.**Journalistic content**: For use to create new journalistic content or to rewrite journalistic content submitted by the user as a writing aid for predefined topics. Users cannot use the application as a general content creation tool for all topics.**Question-answering**: Users can ask questions and receive answers from trusted source documents such as internal company documentation. The application doesn't generate answers ungrounded in trusted source documentation.**Reason over structured and unstructured data**: Users can analyze inputs using classification, sentiment analysis of text, or entity extraction. Examples include analyzing product feedback sentiment, analyzing support calls and transcripts, and refining text-based search with embeddings.**Search**: Users can search trusted source documents such as internal company documentation. The application doesn't generate results ungrounded in trusted source documentation.**Summarization**: Users can submit content to be summarized for predefined topics built into the application and cannot use the application as an open-ended summarizer. Examples include summarization of internal company documentation, call center transcripts, technical reports, and product reviews.**Writing assistance on specific topics**: Users can create new content or rewrite content submitted by the user as a writing aid for business content or pre-defined topics. Users can only rewrite or create content for specific business purposes or predefined topics and cannot use the application as a general content creation tool for all topics. Examples of business content include proposals and reports. For journalistic use, see above**Journalistic content**use case.**Data generation for fine-tuning**: Users can use a model in Azure OpenAI to generate data which is used solely to fine-tune (i) another Azure OpenAI model, using the fine-tuning capabilities of Azure OpenAI, and/or (ii) another Azure AI custom model, using the fine-tuning capabilities of the Foundry Tool. Generating data and fine-tuning models is limited to internal users only; the fine-tuned model may only be used for inferencing in the applicable Foundry Tool and, for Azure OpenAI service, only for customer's permitted use case(s) under this form.

#### Fine-tuned use cases

The following are additional use cases we recommend for fine-tuned models. Fine tuning is most appropriate for:

**Steering the style, format, tone or qualitative aspects of responses**via examples of the desired responses.**Ensuring the model reliably produces a desired output**such as providing responses in a specific format or ensuring responses are grounded by information in the prompt.**Use cases with many edge cases**that cannot be covered within examples in the prompt, such as complex natural language to code examples.**Improving performance at specific skills or tasks**such as classification, summarization, or formatting – that can be hard to describe within a prompt.**Reducing costs or latency**by utilizing shorter prompts, or swapping a fine-tuned version of a smaller/faster model for a more general-purpose model (e.g. fine tuned GPT-3.5-Turbo for GPT-4).

As with base models, the use case prohibitions outlined in the [Azure OpenAI Code of conduct](/en-us/legal/ai-code-of-conduct?context=%2Fazure%2Fcognitive-services%2Fopenai%2Fcontext%2Fcontext) apply to fine-tuned models as well.

Fine tuning alone is not recommended for scenarios where you want to extend your model to include out-of-domain information, where explainability or grounding are important, or where the underlying data are updated frequently.

#### Reasoning model use cases

The advanced reasoning capabilities of the reasoning models may be best suited for reasoning-heavy uses in science, coding, math, and similar fields. Specific use cases could include:

**Complex code generation, analysis and optimization**: Algorithm generation and advanced coding tasks to help developers execute multi-step workflows, better understanding the steps taken in code development.**Advanced problem solving**: Comprehensive brainstorming sessions, strategy development and breaking down multifaceted issues.**Complex document comparison**: Analyzing contracts, case files, or legal documents to discern subtle differences in document contents.**Instruction following and workflow management**: Handling workflows that require shorter context.

For greater detail on intended uses, visit the [OpenAI o1 System Card](https://cdn.openai.com/o1-system-card-20241205.pdf), [o3-mini System Card](https://openai.com/index/o3-mini-system-card/), [o3/o4-mini System Card](https://openai.com/index/o3-o4-mini-system-card/), and [GPT-5 System Card](https://openai.com/index/gpt-5-system-card/).

#### Deep research use cases

Deep research models are fine-tuned versions of the o-series reasoning models that are designed to take a high-level query and return a structured, citation-rich report. The models create subqueries and gather information from web searches in several iterations before returning a final response. Use cases could include the following, with adequate human oversight:

**Complex research & literature review**: Synthesizing findings across hundreds of papers, identifying gaps or contradictions in research, proposing novel hypotheses or research directions.**Scientific discovery & hypothesis generation**: Exploring connections between findings across disciplines, generating testable hypotheses or experimental designs, assisting in interpretation of raw experimental data.**Advanced technical problem solving**: Debugging complex systems (for example, distributed software, robotics), designing novel algorithms or architectures, and solving advanced math or physics problems.**Augmenting long-term planning**: Helping executives or researchers plan 10-year technology roadmaps, modeling long-range scenarios in AI safety, biosecurity, or climate, evaluating second- and third-order effects of decisions.

Deep research models are available as a tool in the [Azure AI Agents](/en-us/azure/ai-foundry/agents/how-to/tools/deep-research) service. For greater detail on intended uses, see the [OpenAI Deep Research System Card](https://openai.com/index/deep-research-system-card/).

#### Azure OpenAI evaluation use cases

Azure OpenAI evaluation is a text-only feature and can't be used with models that support non-text inputs. Evals can be used in multiple scenarios including but not limited to:

**Text matching/comparison evaluation**: This is helpful for scenarios where the user wants to check if the output matches an expected string. Users can also compare two sets of values and score the relationships. Examples include, but are not limited to, multiple-choice questions where answers are compared to an answer key, and string validation.**Text quality**: Text quality assesses response quality with methods such as Bleu, Rouge or cosine algorithms and is widely used in various natural language processing tasks such as machine translation, text summarization, and text generation, among others.**Classification-based evaluation**: Classification-based evaluation assesses the performance of a model by assigning responses to predefined categories or labels or by comparing the model's output to a reference set of correct answers. Automated grading, sentiment analysis, and product categorization are among some of the common use cases.**Conversational quality evaluation**: Conversational quality evaluation involves comparing responses against predefined criteria using a detailed chain-of-thought (CoT) prompt. Common use cases include customer support, chatbot development, and educational assessments, among others.**Criteria-based evaluation**: One common scenario for criteria-based evaluation is factuality. Assessing factual accuracy involves comparing a submitted answer to an expert answer, focusing solely on factual content. This can be useful in educational tools to improve the accuracy of answers provided by LLMs or in research assistance tools to assess the factual accuracy of responses generated by LLMs in academic settings.**String validity evaluation**: one common scenario would be to check if model's response follows a specific schema or is valid JSON or XML content.

#### Computer Use (Preview) use cases

The capabilities of Computer Use are best suited for developing agentic AI systems that can autonomously interact with GUIs. Specific use cases could include:

Automated Web Navigation and Interaction: Navigating navigation of web-based interfaces autonomously to retrieve and present information from trusted sources, such as internal company resources or structured databases. The model follows predefined navigation rules to extract relevant data while ensuring compliance with security policies.

Web-Based Task Automation: Automating repetitive web-based tasks, such as filling out forms, submitting data, or interacting with web applications. Computer Use can click buttons, enter text, and process structured data but operates only within authorized workflows and domains.

Structured and Unstructured Data Extraction: Extracting relevant data from structured sources like tables and spreadsheets, as well as unstructured sources such as PDFs, scanned documents, or emails. This capability is useful for tasks like financial data processing, contract analysis, or customer support ticket categorization.

Automated Form Filling and Data Entry: Extracting information from structured databases or user inputs and use it to populate web-based forms. This is useful for automating customer service requests, HR processes, or CRM updates while ensuring accuracy and consistency in data handling.

Web-Based Image Analysis: Analyzing images found on web pages to detect and tag objects, scenes, or relevant patterns. Computer Use can extract visual information to support applications like inventory management, document processing, or object classification.

Interactive Visual Search and Identification: Assisting users in locating relevant visual content through structured searches. For example, Computer Use can identify products in an e-commerce catalog, recognize landmarks in travel applications, or retrieve specific images from digital archives based on predefined criteria.

Automated Compliance and Policy Checks: Scanning web-based content such as uploaded files, contracts, or internal documentation for adherence to predefined compliance rules. Computer Use can flag missing information, inconsistencies, or potential violations to help enforce regulatory standards within an organization.

Automated Workflow Execution for Business Applications: Defining multi-step workflows for navigating enterprise applications, such as generating reports, updating records, or retrieving analytics. Computer Use follows predefined steps within business tools and adheres to access control policies to ensure secure execution.


### Considerations when choosing a use case

We encourage customers to use the Azure OpenAI GPT-4, o-series, GPT-3, Codex, and Computer Use models in their innovative solutions or applications as approved in their [Limited Access registration form](/en-us/azure/ai-foundry/responsible-ai/openai/limited-access). However, here are some considerations when choosing a use case:

**Not suitable for open-ended, unconstrained content generation.**Scenarios where users can generate content on any topic are more likely to produce offensive or harmful text. The same is true of longer generations.**Not suitable for scenarios where up-to-date, factually accurate information is crucial**unless you have human reviewers or are using the models to search your own documents and have verified suitability for your scenario. The service doesn't have information about events that occur after its training date, likely has missing knowledge about some topics, and may not always produce factually accurate information.**Avoid scenarios where use or misuse of the system could result in significant physical or psychological injury to an individual.**For example, scenarios that diagnose patients or prescribe medications have the potential to cause significant harm. Incorporating meaningful human review and oversight into the scenario can help reduce the risk of harmful outcomes.**Avoid scenarios where use or misuse of the system could have a consequential impact on life opportunities or legal status.**Examples include scenarios where the AI system could affect an individual's legal status, legal rights, or their access to credit, education, employment, healthcare, housing, insurance, social welfare benefits, services, opportunities, or the terms on which they're provided. Incorporating meaningful human review and oversight into the scenario can help reduce the risk of harmful outcomes.**Avoid high stakes scenarios that could lead to harm.**The models hosted by Azure OpenAI service reflect certain societal views, biases, and other undesirable content present in the training data or the examples provided in the prompt. As a result, we caution against using the models in high-stakes scenarios where unfair, unreliable, or offensive behavior might be extremely costly or lead to harm. Incorporating meaningful human review and oversight into the scenario can help reduce the risk of harmful outcomes.**Carefully consider use cases in high stakes domains or industry:**Examples include but are not limited to healthcare, medicine, finance, or legal.**Carefully consider well-scoped chatbot scenarios.**Limiting the use of the service in chatbots to a narrow domain reduces the risk of generating unintended or undesirable responses.**Carefully consider all generative use cases.**Content generation scenarios may be more likely to produce unintended outputs and these scenarios require careful consideration and mitigations.**Legal and regulatory considerations**: Organizations need to evaluate potential specific legal and regulatory obligations when using any Foundry Tools and solutions, which may not be appropriate for use in every industry or scenario. Additionally, Foundry Tools or solutions are not designed for and may not be used in ways prohibited in applicable terms of service and relevant codes of conduct.

When choosing a use case for Computer Use, users should factor in the following considerations in addition to those listed above:

- Avoid scenarios where actions are irreversible or highly consequential: These include, but are not limited to, the ability to send an email (such as to the wrong recipient), ability to modify or delete files that are important to you, ability to make financial transactions or directly interacting with outside services, sharing sensitive information publicly, granting access to critical systems, or executing commands that could alter system functionality or security.
- Degradation of performance on advanced uses: Computer Use is best suited for use cases around completing tasks with GUIs, such as accessing websites and computer desktops. It may not perform well doing more advanced tasks such as editing code, writing extensive text, and making complex decisions.
- Ensure adequate human oversight and control. Consider including controls to help users verify, review and/or approve actions in a timely manner, which may include reviewing planned tasks or calls to external data sources, for example, as appropriate for your system. Consider including controls for adequate user remediation of system failures, particularly in high-risk scenarios and use cases.
- Clearly define actions and associated requirements. Clearly defining which actions are allowed (action boundaries), prohibited, or need explicit authorization may help Computer Use operate as expected and with the appropriate level of human oversight.
- Clearly define intended operating environments. Clearly define the intended operating environments (domain boundaries) where Computer Use is designed to perform effectively.
- Ensure appropriate intelligibility in decision making. Providing information to users before, during, and after actions are taken may help them understand action justification or why certain actions were taken or the application is behaving a certain way, where to intervene, and how to troubleshoot issues.
- For further information, consult the
[Fostering appropriate reliance on Generative AI guide](/en-us/ai/playbook/technology-guidance/overreliance-on-ai/overreliance-on-ai).

When choosing a use case for deep research, users should factor in the following considerations in addition to those listed above:

**Ensure adequate human oversight and control**: Provide mechanisms to help ensure that users review deep research reports and validate cited sources and content.**Check citations for copyrighted content**: The deep research tool conducts web searches when preparing responses, and copyrighted materials may be cited. Check the source citations included in the report, and ensure you use and attribute copyrighted material appropriately.

## Limitations

When it comes to large-scale natural language models, vision models, and speech models, there are fairness and responsible AI issues to consider. People use language and images to describe the world and to express their beliefs, assumptions, attitudes, and values. As a result, publicly available text and image data typically used to train large-scale natural language processing and image generation models contains societal biases relating to race, gender, religion, age, and other groups of people, as well as other undesirable content. Similarly, speech models can exhibit different levels of accuracy across different demographic groups and languages. These societal biases are reflected in the distributions of words, phrases, and syntactic structures.

### Technical limitations, operational factors, and ranges

Caution

Be advised that this section contains illustrative examples which include terms and language that some individuals might find offensive.

Large-scale natural language, image, and speech models trained with such data can potentially behave in ways that are unfair, unreliable, or offensive, in turn causing harms. Some of the ways are listed here. We emphasize that these types of harms are not mutually exclusive. A single model can exhibit more than one type of harm, potentially relating to multiple different groups of people. For example:

**Allocation:**These models can be used in ways that lead to unfair allocation of resources or opportunities. For example, automated résumé screening systems can withhold employment opportunities from one gender if they are trained on résumé data that reflects the existing gender imbalance in a particular industry. Or the image generation models could be used to create imagery in the style of a known artist, which could affect the value of the artist's work or the artist's life opportunities. GPT-4 vision models could be used to identify individual behaviors and patterns that might have negative impacts on life opportunities.**Quality of service:**The Azure OpenAI models are trained primarily on English text and images with English text descriptions. Languages other than English will experience worse performance. English language varieties with less representation in the training data might experience worse performance than standard American English. The publicly available images used to train the image generation models might reinforce public bias and other undesirable content. The DALL·E models are also unable to consistently generate comprehensible text at this time. Speech models might introduce other limitations, for example, translations using the Whisper model in Azure OpenAI are limited to English output only. Broadly speaking, with Speech-to-Text models, be sure to properly specify a language (or locale) for each audio input to improve accuracy in transcription. Additionally, acoustic quality of the audio input, non-speech noise, overlapped speech, vocabulary, accents, and insertion errors might also affect the quality of your transcription or translation.**Stereotyping:**These models can reinforce stereotypes. For example, when translating "He is a nurse" and "She is a doctor" into a genderless language such as Turkish and then back into English, many machine translation systems yield the stereotypical (and incorrect) results of "She is a nurse" and "He is a doctor." With DALL·E, when generating an image based on the prompt "Fatherless children," the model could generate images of Black children only, reinforcing harmful stereotypes that might exist in publicly available images. The GPT-4 vision models might also reinforce stereotypes based on the contents of the input image, by relying on components of the image and making assumptions that might not always be true.**Demeaning:**The natural language and vision models in the Azure OpenAI service can demean people. For example, an open-ended content generation system with inappropriate or insufficient mitigations might produce content that is offensive or demeaning to a particular group of people.**Overrepresentation and underrepresentation:**The natural language and vision models in the Azure OpenAI service can over- or under-represent groups of people, or even erase their representation entirely. For example, if text prompts that contain the word "gay" are detected as potentially harmful or offensive, this identification could lead to the underrepresentation or even erasure of legitimate image generations by or about the LGBTQIA+ community.**Inappropriate or offensive content:**The natural language and vision models in the Azure OpenAI service can produce other types of inappropriate or offensive content. Examples include the ability to generate text that is inappropriate in the context of the text or image prompt; the ability to create images that potentially contain harmful artifacts such as hate symbols; images that elicit harmful connotations; images that relate to contested, controversial, or ideologically polarizing topics; images that are manipulative; images that contain sexually charged content that is not caught by sexual-related guardrails; and images that relate to sensitive or emotionally charged topics. For example, a well-intentioned text prompt aimed to create an image of the New York skyline with clouds and airplanes flying over it might unintentionally generate images that illicit sentiments related to the events surrounding 9/11.**Disinformation and misinformation about sensitive topics:**Because DALL·E and GPT-image-1 are powerful image generation models, they can be used to produce disinformation and misinformation that can be harmful. For example, a user could prompt the model to generate an image of a political leader engaging in activity of a violent or sexual (or simply inaccurate) nature that might lead to consequential harms, including but not limited to public protests, political change, or fake news. The GPT-4 visions models could also be used in a similar vein. The model might reinforce disinformation or misinformation about sensitive topics if the prompt contains such information without mitigation.**Information reliability:**Language and vision model responses can generate nonsensical content or fabricate content that might sound reasonable but is inaccurate with respect to external validation sources. Even when drawing responses from trusted source information, responses might misrepresent that content. Transcriptions or translations might result in inaccurate text.**False information:**Azure OpenAI doesn't fact-check or verify content that is provided by customers or users. Depending on how you have developed your application, it might produce false information unless you have built in mitigations (**see Best practices for improving system performance**).

### Risks and limitations of fine-tuning

When customers fine-tune Azure OpenAI models, it can improve model performance and accuracy on specific tasks and domains, but it can also introduce new risks and limitations that customers should be aware of. These risks and limitations apply to all [Azure OpenAI models that support fine-tuning](/en-us/azure/ai-foundry/openai/concepts/models#fine-tuning-models). Some of these risks and limitations are:

**Data quality and representation**: The quality and representativeness of the data used for fine-tuning can affect the model's behavior and outputs. If the data is noisy, incomplete, outdated, or if it contains harmful content like stereotypes, the model can inherit these issues and produce inaccurate or harmful results. For example, if the data contains gender stereotypes, the model can amplify them and generate sexist language. Customers should carefully select and pre-process their data to ensure that it's relevant, diverse, and balanced for the intended task and domain.**Model robustness and generalization**: The model's ability to handle diverse and complex inputs and scenarios can decrease after fine-tuning, especially if the data is too narrow or specific. The model can overfit to the data and lose some of its general knowledge and capabilities. For example, if the data is only about sports, the model can struggle to answer questions or generate text about other topics. Customers should evaluate the model's performance and robustness on a variety of inputs and scenarios and avoid using the model for tasks or domains that are outside its scope.**Regurgitation**: While your training data is not available to Microsoft or any third-party customers, poorly fine-tuned models may regurgitate, or directly repeat, training data. Customers are responsible for removing any PII or otherwise protected information from their training data and should assess their fine-tuned models for over-fitting or otherwise low-quality responses. To avoid regurgitation, customers are encouraged to provide large and diverse datasets.**Model transparency and explainability**: The model's logic and reasoning can become more opaque and difficult to understand after fine-tuning, especially if the data is complex or abstract. A fine-tuned model can produce outputs that are unexpected, inconsistent, or contradictory, and customers may not be able to explain how or why the model arrived at those outputs. For example, if the data is about legal or medical terms, the model can generate outputs that are inaccurate or misleading, and customers may not be able to verify or justify them. Customers should monitor and audit the model's outputs and behavior and provide clear and accurate information and guidance to the end-users of the model.

To help mitigate the risks associated with advanced fine-tuned models, we have implemented additional [evaluation steps](/en-us/azure/ai-foundry/openai/how-to/fine-tuning?tabs=azure-openai%2Cturbo%2Cpython-new&pivots=programming-language-studio#safety-evaluation-gpt-4-gpt-4o-and-gpt-4o-mini-fine-tuning---public-preview) to help detect and prevent harmful content in the training and outputs of fine-tuned models. The fine-tuned model evaluation filters are set to predefined thresholds and cannot be modified by customers; they aren't tied to any custom guardrails and control configuration you may have created.

### Reasoning model limitations

- Reasoning models are best suited for use cases that involve heavy reasoning and may not perform well on some natural language tasks such as personal or creative writing when compared to earlier AOAI models.
- The new reasoning capabilities may increase certain types of risks, requiring refined methods and approaches towards risk management protocols and evaluating and monitoring system behavior. For example, o1's CoT reasoning capabilities have demonstrated improvements in persuasiveness, and simple in-context scheming.
- Users may experience that the reasoning family of models takes more time to reason through responses and should account for the additional time and latency in developing applications.
**Psychological influences**: If prompted and in certain circumstances, GPT-5 Reasoning in Azure OpenAI may produce outputs that suggest emotions, thoughts, or physical presence. The model could offer advice without full context, which may be unsuitable for some users. The model might express affection, impersonate others, or encourage ongoing interaction—potentially leading to users forming social relationships with AI. Developers using GPT-5 should implement safeguards and disclose risks for users of their applications. For example, users should be notified that they are interacting with an AI system and be informed of such psychological risks.

For greater detail on these limitations, see the [OpenAI o1 System Card](https://cdn.openai.com/o1-system-card-20241205.pdf), [o3-mini System Card](https://openai.com/index/o3-mini-system-card/), [o3/o4-mini System Card](https://openai.com/index/o3-o4-mini-system-card/), and [GPT-5 System Card](https://openai.com/index/gpt-5-system-card/).

### GPT-4o limitations

- The
`gpt-4o-realtime-preview`

audio translation capabilities may output non-English languages in a non-native accent. This may limit the effectiveness of language performance in audio outputs. Language supportability is in line with existing gpt-4o model versions. - Users may experience that
`gpt-4o-realtime-preview`

is less robust in noisy environments and should account for noise sensitivity when developing applications.

For more best practices, see the [OpenAI 4o System Card](https://openai.com/index/gpt-4o-system-card/).

### GPT-4.1 limitations

- The 4.1-series models introduce the ability to create inference requests with up to 1M context tokens, including images. Due to the extended length, there may be differences in system behavior and risks when compared to other models.
- Users should thoroughly evaluate and test their applications and use cases that leverage this longer context capability and should account for this additional effort when developing applications.

### Risk and limitations of Computer Use (Preview)

Warning

Computer Use carries substantial security and privacy risks and user responsibility. Computer Use comes with significant security and privacy risks. Both errors in judgment by the AI and the presence of malicious or confusing instructions on web pages, desktops, or other operating environments which the AI encounters may cause it to execute commands you or others do not intend, which could compromise the security of your or other users’ browsers, computers, and any accounts to which AI has access, including personal, financial, or enterprise systems.

We strongly recommend taking appropriate measures to address these risks, such as using the Computer Use tool on virtual machines with no access to sensitive data or critical resources.

Verify and check actions taken: Computer Use might make mistakes and perform unintended actions. This can be due to the model not fully understanding the GUI, having unclear instructions or encountering an unexpected scenario.

Carefully consider and monitor use: Computer Use, in some limited circumstances, may perform actions without explicit authorization, some of which may be high-risk (e.g. send communications)

Developers will need to be systematically aware of, and defend against, situations where the model can be fooled into executing commands that are harmful to the user or the system, such as downloading malware, leaking credentials, or issuing fraudulent financial transactions. Particular attention should be paid to the fact that screenshot inputs are untrusted by nature and may include malicious instructions aimed at the model.

Evaluate in isolation: We recommend only evaluating Computer Use in isolated containers without access to sensitive data or credentials.

Opaque decision-making processes: As agents combine large language models with external systems, tracing the “why” behind their decisions can become challenging. End users using such an agent built using the Computer Use model may find it difficult to understand why certain tools or combination of tools were chosen to answer a query, complicating trust and verification of the agent’s outputs or actions.

Evolving best practices and standards: If you are using Computer Use to build an agentic system, bear in mind that Agents are an emerging technology, and guidance on safe integration, transparent tool usage, and responsible deployment continues to evolve. Keeping up with the latest best practices and auditing procedures is crucial, as even well-intentioned uses can become risky without ongoing review and refinement.

### Azure OpenAI evaluation limitations

**Data Quality**: When you're using Azure OpenAI Evaluation, be aware that poor quality data can lead to misleading or unreliable evaluation results.**Configuration quality:**If a customer improperly defines the prompt or evaluators or provides invalid evaluation data, the results of the Azure OpenAI Evaluation service will be incorrect and invalid. Refer to the[Azure OpenAI documentation](/en-us/azure/ai-foundry/openai/how-to/evaluations)for details on how to set up an evaluation run.**Limited scope**: Azure OpenAI evaluation only supports text-based natural language models. It doesn't support any risk and safety metrics to evaluate generated responses for risk and safety severity scores (e.g., hateful and unfair content, sexual content, violent content, and self-harm related content).

## System performance

In many AI systems, performance is often defined in relation to accuracy—that is, how often the AI system offers a correct prediction or output. With large-scale natural language models and vision models, two different users might look at the same output and have different opinions of how useful or relevant it's, which means that performance for these systems must be defined more flexibly. Here, we broadly consider performance to mean that the application performs as you and your users expect, including not generating harmful outputs.

Azure OpenAI service can support a wide range of applications like search, classification, code generation, image generation, and image understanding, each with different performance metrics and mitigation strategies. There are several steps you can take to mitigate some of the concerns listed under "Limitations" and to improve performance. Other important mitigation techniques are outlined in the section [Evaluating and integrating Azure OpenAI for your use](#evaluating-and-integrating-azure-openai-natural-language-and-vision-models-for-your-use).

### Best practices for improving system performance

**Show and tell when designing prompts.**With natural language models and speech models, make it clear to the model what kind of outputs you expect through instructions, examples, or a combination of the two. If you want the model to rank a list of items in alphabetical order or to classify a paragraph by sentiment, show the model that is what you want.**Keep your application on topic.**Carefully structure prompts and image inputs to reduce the chance of producing undesired content, even if a user tries to use it for this purpose. For instance, you might indicate in your prompt that a chatbot only engages in conversations about mathematics and otherwise responds "I'm sorry. I'm afraid I can't answer that." Adding adjectives like "polite" and examples in your desired tone to your prompt can also help steer outputs.**Provide quality data.**With text and code models, if you are trying to build a classifier or get the model to follow a pattern, make sure that there are enough examples. Be sure to proofread your examples—the model is usually capable of processing basic spelling mistakes and giving you a response, but it also might assume errors are intentional which could affect the response. Providing quality data also includes giving your model reliable data to draw responses from in chat and question answering systems.**Provide trusted data.**Retrieving or uploading untrusted data into your systems could compromise the security of your systems or applications. To mitigate these risks in your applicable applications (including applications using the Assistants API), we recommend logging and monitoring LLM interactions (inputs/outputs) to detect and analyze potential prompt injections, clearly delineating user input to minimize risk of prompt injection, restricting the LLM's access to sensitive resources, limiting its capabilities to the minimum required, and isolating it from critical systems and resources. Learn about additional mitigation approaches in[Security guidance for Large Language Models | Microsoft Learn.](/en-us/ai/playbook/technology-guidance/generative-ai/mlops-in-openai/security/security-recommend)**Configure parameters to improve accuracy or groundedness of responses**. Augmenting prompts with data retrieved from trusted sources – such as by using the Azure OpenAI "on your data" feature – can reduce, but not completely eliminate, the likelihood of generating inaccurate responses or false information. Steps you can take to further improve the accuracy of responses include carefully selecting the trusted and relevant data source and configuring custom parameters such as “strictness”, “limit responses to data content” and “number of retrieved documents to be considered” as appropriate to your use cases or scenarios. Learn more about configuring these settings for[Azure OpenAI on Your Data](/en-us/azure/ai-foundry/openai/concepts/use-your-data).**Limit the length, structure, and rate of inputs and outputs.**Restricting the length or structure of inputs and outputs can increase the likelihood that the application will stay on task and mitigate, at least in part, any potentially unfair, unreliable, or offensive behavior. Other options to reduce the risk of misuse include (i) restricting the source of inputs (for example, limiting inputs to a particular domain or to authenticated users rather than being open to anyone on the internet) and (ii) implementing usage rate limits.**Encourage human review of outputs prior to publication or dissemination.**With generative AI, there is potential for generating content that might be offensive or not related to the task at hand, even with mitigations in place. To ensure that the generated output meets the task of the user, consider building ways to remind users to review their outputs for quality prior to sharing widely. This practice can reduce many different harms, including offensive material, disinformation, and more.**Implement additional scenario-specific mitigations.**Refer to the mitigations outlined in[Evaluating and integrating Azure OpenAI for your use](#evaluating-and-integrating-azure-openai-natural-language-and-vision-models-for-your-use)including content moderation strategies. These recommendations do not represent every mitigation required for your application. Newer models such as GPT-4o and reasoning models may provide responses in sensitive scenarios and are more likely to attempt to reduce potentially harmful outputs in their responses rather than refuse to respond altogether. It's important to understand this behavior when evaluating and integrating content moderation for your use case; adjustments to filtering severity may be needed depending on your use case.**Avoid triggering mandatory safeguards.**Azure Direct Models may have safeguards to prevent security exploits including output of raw CoT and biosecurity content. Use of a model in a manner that creates a security exploit or evades or attempts to evade a protection on the model, including by circumventing these safeguards, violates the Acceptable Use Policy for Online Services and may result in suspension. For greater detail on best practices, visit the[OpenAI o1 System Card](https://cdn.openai.com/o1-system-card-20241205.pdf),[o3-mini System Card](https://openai.com/index/o3-mini-system-card/),[o3/o4-mini System Card](https://openai.com/index/o3-o4-mini-system-card/), and[GPT-5 System Card](https://openai.com/index/gpt-5-system-card/).

#### Best practices and recommendations for fine tuning

To mitigate the risks and limitations of fine-tuning models on Azure OpenAI, we recommend customers to follow some best practices and guidelines, such as:

**Data selection and preprocessing**: Customers should carefully select and pre-process their data to ensure that it's relevant, diverse, and balanced for the intended task and domain. Customers should also remove or anonymize any sensitive or personal information from the data, such as names, addresses, or email addresses, to protect the privacy and security of the data subjects. Customers should also check and correct any errors or inconsistencies in the data, such as spelling, grammar, or formatting, to improve the data quality and readability.**Include a system message in your training data**for chat-completion formatted models, to steer your responses, and use that same system message when using your fine-tuned model for inferencing. Leaving the system message blank tends to produce low-accuracy fine-tuned models, and forgetting to include the same system message when inferencing may result in the fine-tuned model reverting to the behavior of the base model.**Model evaluation and testing: Customers should evaluate and test the fine-tuned model's performance**and robustness on a variety of inputs and scenarios and compare it with the original model and other baselines. Customers should also use appropriate metrics and criteria to measure the model's accuracy, reliability, and fairness, and to identify any potential errors or biases in the model's outputs and behavior.**Model documentation and communication**: Customers should document and communicate the model's purpose, scope, limitations, and assumptions, and provide clear and accurate information and guidance to the end-users of the model.

#### Best practices and recommendations for Azure OpenAI evaluation

**Robust ground truth data**: In general in large-scale natural language models, customers should carefully select and pre-process their data to ensure that it's relevant, diverse, and balanced for the intended task and domain. Customers should also remove or anonymize any sensitive or personal information from the data, such as names, addresses, or email addresses, to protect the privacy and security of the data subjects. Customers should also check and correct any errors or inconsistencies in the data, such as spelling, grammar, or formatting, to improve the data quality and readability.

Specifically for Azure OpenAI evaluation, the accuracy of the ground truth data provided by the user is crucial because inaccurate ground truth data leads to meaningless and inaccurate evaluation results. Ensuring the quality and reliability of this data is essential for obtaining valid assessments of the model's performance. Inaccurate ground truth data can skew the evaluation metrics, resulting in misleading conclusions about the model's capabilities. Therefore, users must carefully curate and verify their ground truth data to ensure that the evaluation process accurately reflects the model's true performance. This is particularly important when making decisions about deploying the model in real-world applications**Prompt definition for evaluation**: The prompt you use in your evaluation should match the prompt you plan to use in production. These prompts provide the instructions for the model to follow. Similar to the OpenAI playground, you can create multiple inputs to include few-shot examples in your prompt. Refer to[Prompt engineering techniques](/en-us/azure/ai-foundry/openai/concepts/prompt-engineering?tabs=chat)for more details on some advanced techniques in prompt design and prompt engineering.**Diverse metrics**: Use a combination of metrics to capture different aspects of performance such as accuracy, fluency and relevance.**Human-in-the-loop**: Integrate human feedback alongside automated evaluation to ensure that subjective nuances are accurately captured.**Transparency**: Clearly communicate the evaluation criteria to users, enabling them to understand how decisions are made.**Continual evaluation and testing**: Continually evaluate the model's performance to identify and address any regressions or negative user experience.

## Evaluating and integrating Azure OpenAI natural language and vision models for your use

The steps in conducting an Azure OpenAI evaluation are:

**Provide data for evaluation**: Either an uploaded flat file in JSONL format, or generated data based on a series of prompts.**Specify test cases to evaluate the data**: Select one or more test cases to score the provided data with passing / failing grades.**Review and filter results**: Each test includes a definition of passing and failing scores. After an evaluation runs, users can review their row-by-row results to see individual test results, or filter on passed / failed.

For additional information on how to evaluate and integrate these models responsibly, please see the [RAI Overview document](/en-us/azure/ai-foundry/responsible-ai/openai/overview).

## Learn more about responsible AI

[Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai)[Microsoft responsible AI resources](https://www.microsoft.com/ai/responsible-ai-resources)[Microsoft Azure Learning courses on responsible AI](/en-us/training/paths/responsible-ai-business-principles/)
