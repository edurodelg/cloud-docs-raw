---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/model-parameters.html
fetched_at: 2026-01-25T02:05:48.371427
---

# Inference request parameters and response fields for foundation models

The topics in this section describe the request parameters and response fields for the models that Amazon Bedrock supplies. When you make inference calls to models with the model invocation ([InvokeModel](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_InvokeModel.html), [InvokeModelWithResponseStream](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_InvokeModelWithResponseStream.html), [Converse](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_Converse.html), and [ConverseStream](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_ConverseStream.html)) API operations, you include request parameters depending on the model that you're using.

If you created a [custom model](./custom-models.html), use the same inference parameters as the foundation model from which it was customized.

If you are [importing a customized model into Amazon Bedrock](./model-customization-import-model.html), make sure to use the same inference
parameters that is mentioned for the customized model you are importing. If you are using
inference parameters that do not match with the inference parameters mentioned for that
model in this documentation, those parameters will be ignored.

Before viewing model parameters for different models, you should familiarize yourself with what model inference is by reading the following chapter: [Submit prompts and generate responses with model inference](./inference.html).

Refer to the following pages for more information about different models in Amazon Bedrock:

-
For a table of models and their IDs to use with the model invocation API operations, the Regions they're supported in, and the general features that they support, see

[Supported foundation models in Amazon Bedrock](./models-supported.html). -
For a table of the Amazon Bedrock Regions that each model is supported in, see

[Model support by AWS Region in Amazon Bedrock](./models-regions.html). -
For a table of the Amazon Bedrock features that each model supports, see

[Model support by feature in Amazon Bedrock](./models-features.html). -
To check if the Converse API (

`Converse`

and`ConverseStream`

) supports a specific model, see[Supported models and model features](./conversation-inference-supported-models-features.html). -
When you make inference calls to a model, you include a prompt for the model. For general information about creating prompts for the models that Amazon Bedrock supports, see

[Prompt engineering concepts](./prompt-engineering-guidelines.html). -
For code examples, see

[Code examples for Amazon Bedrock using AWS SDKs](./service_code_examples.html).

Select a topic to learn about models for that provider and their parameters.