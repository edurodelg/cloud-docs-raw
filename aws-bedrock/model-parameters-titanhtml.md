---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/model-parameters-titan.html
fetched_at: 2026-01-25T03:12:35.571617
---

# Amazon Titan models

This section describes the request parameters and response fields for Amazon Titan models. Use this information
to make inference calls to Amazon Titan models with the [InvokeModel](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_InvokeModel.html) and [InvokeModelWithResponseStream](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_InvokeModelWithResponseStream.html) (streaming) operations.
This section also includes Python code examples that shows how to call Amazon Titan models. To use a model in an inference operation, you need the model ID for the model.
To get the model ID, see [Supported foundation models in Amazon Bedrock](./models-supported.html). Some
models also work with the [Converse API](./conversation-inference.html).
To check if the Converse API supports a specific Amazon Titan model, see
[Supported models and
model features](./conversation-inference-supported-models-features.html). For more code examples,
see [Code examples for Amazon Bedrock using AWS SDKs](./service_code_examples.html).

Foundation models in Amazon Bedrock support input and output modalities, which vary from model to
model. To check the modalities that Amazon Titan models support, see [Supported foundation models in Amazon Bedrock](./models-supported.html). To check which Amazon Bedrock
features the Amazon Titan models support, see [Supported foundation models in Amazon Bedrock](./models-supported.html). To check which AWS Regions that Amazon Titan models
are available in, see [Supported foundation models in Amazon Bedrock](./models-supported.html).

When you make inference calls with Amazon Titan models, you include a prompt for the model. For general information
about creating prompts for the models that Amazon Bedrock supports, see [ Prompt engineering concepts](./prompt-engineering-guidelines.html).