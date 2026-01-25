---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/features-regions.html
fetched_at: 2026-01-25T03:12:16.830466
---

# Feature support by AWS Region in Amazon Bedrock

This section shows Amazon Bedrock feature compatibility for different AWS Regions.

###### Note

Note the following:

-
Model inference (

[InvokeModel](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_InvokeModel.html),[InvokeModelWithResponseStream](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_InvokeModelWithResponseStream.html),[Converse](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_Converse.html),[ConverseStream](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_ConverseStream.html)) is available in all Regions supported by Amazon Bedrock. -
Model evaluation in Europe (Paris) is only available for automatic evaluation jobs.

-
Provisioned Throughput in AWS GovCloud (US-West) is only available for custom models with no-commitment.


You can refer to the following resources to learn more about AWS Regions:

-
For a list of AWS Region names and their region codes, see

[AWS Regions](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-regions.html). -
For a list of AWS Regions that support Amazon Bedrock, see

[Amazon Bedrock endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/bedrock.html).

###### Note

Some AWS Regions are opt-in and require activation in AWS Billing and Cost Management before use. For a list of these Regions, see [Opt-in status](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-regions.html#regions-opt-in-status).

The following table shows feature support by Region:

| Feature | US East (N. Virginia) | US East (Ohio) | US West (N. California) | US West (Oregon) | AWS GovCloud (US-East) | AWS GovCloud (US-West) | Africa (Cape Town) | Asia Pacific (Taipei) | Asia Pacific (Tokyo) | Asia Pacific (Seoul) | Asia Pacific (Osaka) | Asia Pacific (Mumbai) | Asia Pacific (Hyderabad) | Asia Pacific (Singapore) | Asia Pacific (Sydney) | Asia Pacific (Jakarta) | Asia Pacific (Melbourne) | Asia Pacific (Malaysia) | Asia Pacific (Thailand) | Canada (Central) | Canada West (Calgary) | Europe (Frankfurt) | Europe (Zurich) | Europe (Stockholm) | Europe (Milan) | Europe (Spain) | Europe (Ireland) | Europe (London) | Europe (Paris) | Israel (Tel Aviv) | Middle East (UAE) | Middle East (Bahrain) | Mexico (Central) | South America (São Paulo) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| API keys | Yes | No | No | Yes | Yes | Yes | No | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes |
| Agents | Yes | No | No | Yes | No | Yes | No | No | Yes | Yes | No | Yes | No | Yes | Yes | No | No | No | No | Yes | No | Yes | Yes | No | No | No | Yes | Yes | Yes | No | No | No | No | Yes |
| Application inference profiles | Yes | Yes | No | Yes | Yes | No | No | No | Yes | Yes | No | Yes | No | Yes | Yes | No | No | No | No | Yes | No | Yes | No | No | No | No | Yes | Yes | Yes | No | No | No | No | Yes |
| Batch inference | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| Continued pre-training | Yes | No | No | Yes | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Custom model import | Yes | Yes | No | Yes | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | Yes | No | No | No | No | No | No | No | No | No | No | No | No |
| Fine-tuning | Yes | No | No | Yes | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Flows | Yes | Yes | No | Yes | Yes | Yes | No | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes |
| Guardrails | Yes | Yes | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | Yes |
| Guardrails image filter | Yes | Yes | No | Yes | No | Yes | No | No | Yes | Yes | No | Yes | No | Yes | Yes | No | No | No | No | No | No | Yes | No | No | No | No | Yes | Yes | No | No | No | No | No | No |
| Intelligent prompt routing | Yes | Yes | No | Yes | Yes | Yes | No | No | Yes | Yes | No | Yes | No | No | Yes | No | No | No | No | No | No | Yes | No | No | No | No | Yes | No | Yes | No | No | No | No | No |
| Knowledge base query | Yes | Yes | No | Yes | Yes | Yes | No | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes |
| Knowledge base vector embeddings | Yes | Yes | No | Yes | Yes | Yes | No | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes |
| Latency | Yes | Yes | No | Yes | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No | No |
| Model copy | Yes | Yes | No | Yes | No | Yes | No | No | Yes | Yes | No | Yes | No | Yes | Yes | No | No | No | No | Yes | No | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes |
| Model evaluation | Yes | Yes | No | Yes | Yes | Yes | No | No | Yes | No | No | Yes | No | No | Yes | No | No | No | No | Yes | No | Yes | Yes | No | No | No | Yes | Yes | Yes | No | No | No | No | Yes |
| Model sharing | Yes | No | No | Yes | No | No | No | No | No | No | No | Yes | No | No | Yes | No | No | No | No | No | No | No | No | No | No | No | Yes | Yes | Yes | No | No | No | No | No |
| Prompt management | Yes | Yes | No | Yes | Yes | Yes | No | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes | No | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes | No | No | No | No | Yes |
| Prompt optimization | Yes | No | No | Yes | No | No | No | No | No | No | No | Yes | No | No | Yes | No | No | No | No | Yes | No | Yes | No | No | No | No | Yes | Yes | Yes | No | No | No | No | Yes |
| Provisioned Throughput | Yes | No | No | Yes | No | No | No | No | No | No | No | Yes | No | No | Yes | No | No | No | No | Yes | No | Yes | No | No | No | No | Yes | Yes | Yes | No | No | No | No | Yes |
| RAG evaluations | Yes | Yes | No | Yes | Yes | Yes | No | No | Yes | No | No | Yes | No | No | Yes | No | No | No | No | Yes | No | Yes | Yes | No | No | No | Yes | Yes | Yes | No | No | No | No | Yes |
| Rerank | Yes | No | No | Yes | No | No | No | No | Yes | No | No | No | No | No | No | No | No | No | No | Yes | No | Yes | No | No | No | No | No | No | No | No | No | No | No | No |
| Token counting | Yes | Yes | No | Yes | No | No | No | No | Yes | No | No | Yes | No | Yes | Yes | No | No | No | No | No | No | Yes | Yes | No | No | No | Yes | Yes | No | No | No | No | No | Yes |