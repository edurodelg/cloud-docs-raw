---
source_url: https://learn.microsoft.com/en-us/azure/ai-foundry/faq
fetched_at: 2026-01-25T15:22:35.685843
---

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