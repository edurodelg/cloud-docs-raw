---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/models-features.html
fetched_at: 2026-01-25T03:12:21.714548
---

# Model support by feature in Amazon Bedrock

This section shows model compatibility with different features in Amazon Bedrock.

###### Note

The following features support all models in Amazon Bedrock

-
Amazon Bedrock API keys

-
Amazon Bedrock Agents

-
Application inference profiles


Model support for the following features is dependent on other features:

-
Prompt management supports all models that support the

[Converse](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_Converse.html)API. To see model support for`Converse`

, refer[Supported models and model features](./conversation-inference-supported-models-features.html). -
Model support for Amazon Bedrock Flows depends on model support for node types that you add to your flow.


## Single-Region foundation model support by feature

The following matrix shows the features that each Amazon Bedrock foundation model is compatible with to use in a given AWS Region:

| Provider | Model | Agents | Batch inference | Continued pre-training | Fine-tuning | Guardrails | Guardrails image filter | Intelligent prompt routing | Knowledge base query | Knowledge base vector embeddings | Model copy | Model evaluation | Model sharing | Prompt optimization | Provisioned Throughput | RAG evaluations | Rerank | Token counting |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Amazon | Nova 2 Lite | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Amazon | Nova Lite | No | Yes | No | No | Yes | No | Yes | Yes | No | Yes | Yes | No | Yes | No | Yes | No | No |
| Amazon | Nova Micro | No | Yes | No | No | Yes | No | No | Yes | No | Yes | Yes | No | Yes | No | Yes | No | No |
| Amazon | Nova Premier | No | No | No | No | No | No | No | No | No | No | No | No | Yes | No | No | No | No |
| Amazon | Nova Pro | No | Yes | No | No | Yes | No | Yes | Yes | No | Yes | Yes | No | Yes | No | Yes | No | No |
| Anthropic | Claude 3 Haiku | No | Yes | No | No | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | No | Yes | No | No |
| Anthropic | Claude 3 Opus | No | Yes | No | No | Yes | Yes | No | No | No | No | Yes | No | Yes | No | Yes | No | No |
| Anthropic | Claude 3 Sonnet | No | Yes | No | No | Yes | Yes | No | Yes | No | No | Yes | No | Yes | No | Yes | No | No |
| Anthropic | Claude 3.5 Haiku | No | Yes | No | No | Yes | No | Yes | Yes | No | No | Yes | No | Yes | No | Yes | No | Yes |
| Anthropic | Claude 3.5 Sonnet | No | Yes | No | No | Yes | Yes | Yes | Yes | No | No | Yes | No | Yes | No | Yes | No | Yes |
| Anthropic | Claude 3.5 Sonnet v2 | No | Yes | No | No | Yes | No | Yes | Yes | No | No | Yes | No | Yes | No | Yes | No | Yes |
| Anthropic | Claude 3.7 Sonnet | No | No | No | No | Yes | No | No | Yes | No | No | Yes | No | Yes | No | Yes | No | Yes |
| Anthropic | Claude Haiku 4.5 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Anthropic | Claude Opus 4 | No | No | No | No | No | No | No | Yes | No | No | No | No | Yes | No | No | No | Yes |
| Anthropic | Claude Opus 4.1 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Anthropic | Claude Opus 4.5 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Anthropic | Claude Sonnet 4 | No | No | No | No | No | No | No | Yes | No | No | No | No | Yes | No | No | No | Yes |
| Anthropic | Claude Sonnet 4.5 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Cohere | Embed v4 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| DeepSeek | DeepSeek-R1 | No | No | No | No | No | No | No | Yes | No | No | Yes | No | Yes | No | Yes | No | No |
| Meta | Llama 3.1 405B Instruct | No | Yes | No | No | Yes | No | No | Yes | No | Yes | Yes | No | No | No | Yes | No | No |
| Meta | Llama 3.1 70B Instruct | No | Yes | No | No | Yes | No | Yes | Yes | No | Yes | Yes | No | Yes | No | Yes | No | No |
| Meta | Llama 3.1 8B Instruct | No | Yes | No | No | Yes | No | Yes | Yes | No | Yes | Yes | No | No | No | Yes | No | No |
| Meta | Llama 3.2 11B Instruct | No | Yes | No | No | No | Yes | No | Yes | No | Yes | Yes | No | Yes | No | Yes | No | No |
| Meta | Llama 3.2 1B Instruct | No | Yes | No | No | No | No | No | No | No | Yes | Yes | No | No | No | Yes | No | No |
| Meta | Llama 3.2 3B Instruct | No | Yes | No | No | No | No | No | No | No | Yes | Yes | No | No | No | Yes | No | No |
| Meta | Llama 3.2 90B Instruct | No | Yes | No | No | No | Yes | No | Yes | No | Yes | Yes | No | No | No | Yes | No | No |
| Meta | Llama 3.3 70B Instruct | No | Yes | No | No | Yes | No | Yes | Yes | No | No | Yes | No | Yes | No | Yes | No | No |
| Meta | Llama 4 Maverick 17B Instruct | No | Yes | No | No | No | No | No | No | No | No | No | No | Yes | No | No | No | No |
| Meta | Llama 4 Scout 17B Instruct | No | Yes | No | No | No | No | No | No | No | No | No | No | Yes | No | No | No | No |
| Mistral AI | Pixtral Large (25.02) | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Conservative Upscale | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Control Sketch | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Control Structure | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Creative Upscale | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Erase Object | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Fast Upscale | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Inpaint | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Outpaint | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Remove Background | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Search and Recolor | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Search and Replace | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Style Guide | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Style Transfer | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| TwelveLabs | Marengo Embed 3.0 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| TwelveLabs | Marengo Embed v2.7 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| TwelveLabs | Pegasus v1.2 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Writer | Palmyra X4 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Writer | Palmyra X5 | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |

## Cross-Region inference profile support by feature

The following matrix shows the features that each Amazon Bedrock foundation model is compatible with to use in a given AWS Region:

Cross-Region inference profiles can route inference requests to foundation models in different Regions within a defined geographical area. To learn more about inference profiles, see [Supported Regions and models for inference profiles](./inference-profiles-support.html). The following table shows inference profile support by different Amazon Bedrock features:

| Provider | Model | Agents | Batch inference | Custom model import | Flows | Guardrails | Guardrails image filter | Intelligent prompt routing | Knowledge base query | Latency | Model evaluation | Prompt management | Provisioned Throughput | Rerank |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Amazon | Nova 2 Lite | No | Yes | No | No | No | No | No | No | No | No | No | No | No |
| Amazon | Nova Lite | No | Yes | No | No | No | No | Yes | Yes | No | No | No | No | No |
| Amazon | Nova Micro | No | Yes | No | No | No | No | No | Yes | No | No | No | No | No |
| Amazon | Nova Premier | No | Yes | No | No | No | No | No | No | No | No | No | No | No |
| Amazon | Nova Pro | No | Yes | No | No | No | No | Yes | Yes | Yes | No | No | No | No |
| Anthropic | Claude 3 Haiku | No | No | No | No | No | Yes | Yes | Yes | No | No | No | No | No |
| Anthropic | Claude 3 Opus | No | Yes | No | No | No | Yes | No | No | No | No | No | No | No |
| Anthropic | Claude 3 Sonnet | No | Yes | No | No | No | Yes | No | Yes | No | No | No | No | No |
| Anthropic | Claude 3.5 Haiku | No | Yes | No | No | No | No | Yes | Yes | Yes | No | No | No | No |
| Anthropic | Claude 3.5 Sonnet | No | Yes | No | No | No | Yes | Yes | Yes | No | No | No | No | No |
| Anthropic | Claude 3.5 Sonnet v2 | No | Yes | No | No | No | No | Yes | Yes | No | No | No | No | No |
| Anthropic | Claude 3.7 Sonnet | No | Yes | No | No | No | No | No | Yes | No | No | No | No | No |
| Anthropic | Claude Haiku 4.5 | No | Yes | No | No | Yes | No | No | No | No | No | No | No | No |
| Anthropic | Claude Opus 4 | No | No | No | No | Yes | No | No | Yes | No | No | No | No | No |
| Anthropic | Claude Opus 4.1 | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Anthropic | Claude Opus 4.5 | No | Yes | No | No | Yes | No | No | No | No | No | No | No | No |
| Anthropic | Claude Sonnet 4 | No | Yes | No | No | Yes | No | No | Yes | No | No | No | No | No |
| Anthropic | Claude Sonnet 4.5 | No | Yes | No | No | Yes | No | No | Yes | No | No | No | No | No |
| Cohere | Embed v4 | No | No | No | No | No | No | No | No | No | No | No | No | No |
| DeepSeek | DeepSeek-R1 | No | No | No | No | Yes | No | No | Yes | No | No | No | No | No |
| Meta | Llama 3.1 405B Instruct | No | Yes | No | No | No | No | No | Yes | Yes | No | No | No | No |
| Meta | Llama 3.1 70B Instruct | No | Yes | No | No | No | No | Yes | Yes | Yes | No | No | No | No |
| Meta | Llama 3.1 8B Instruct | No | Yes | No | No | No | No | Yes | Yes | No | No | No | No | No |
| Meta | Llama 3.2 11B Instruct | No | Yes | No | No | Yes | Yes | Yes | Yes | No | No | No | No | No |
| Meta | Llama 3.2 1B Instruct | No | Yes | No | No | Yes | No | No | No | No | No | No | No | No |
| Meta | Llama 3.2 3B Instruct | No | Yes | No | No | Yes | No | No | No | No | No | No | No | No |
| Meta | Llama 3.2 90B Instruct | No | Yes | No | No | Yes | Yes | Yes | Yes | No | No | No | No | No |
| Meta | Llama 3.3 70B Instruct | No | Yes | No | No | No | No | Yes | Yes | No | No | No | No | No |
| Meta | Llama 4 Maverick 17B Instruct | No | Yes | No | No | Yes | No | No | No | No | No | No | No | No |
| Meta | Llama 4 Scout 17B Instruct | No | Yes | No | No | Yes | No | No | No | No | No | No | No | No |
| Mistral AI | Pixtral Large (25.02) | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Conservative Upscale | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Control Sketch | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Control Structure | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Creative Upscale | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Erase Object | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Fast Upscale | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Inpaint | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Outpaint | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Remove Background | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Search and Recolor | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Search and Replace | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Style Guide | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Stability AI | Stable Image Style Transfer | No | No | No | No | No | No | No | No | No | No | No | No | No |
| TwelveLabs | Marengo Embed 3.0 | No | No | No | No | No | No | No | No | No | No | No | No | No |
| TwelveLabs | Marengo Embed v2.7 | No | No | No | No | No | No | No | No | No | No | No | No | No |
| TwelveLabs | Pegasus v1.2 | No | No | No | No | Yes | No | No | No | No | No | No | No | No |
| Writer | Palmyra X4 | No | No | No | No | Yes | No | No | No | No | No | No | No | No |
| Writer | Palmyra X5 | No | No | No | No | Yes | No | No | No | No | No | No | No | No |