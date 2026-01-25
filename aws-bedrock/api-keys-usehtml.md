---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/api-keys-use.html
fetched_at: 2026-01-25T02:04:48.503691
---

# Use an Amazon Bedrock API key

You can use your Amazon Bedrock API key in the following ways:

-
**Set it as environment variable**– The Amazon Bedrock service recognizes the environment variable`AWS_BEARER_TOKEN_BEDROCK`

You have the following options to set the key:-
Open a terminal to set it:

-
**MacOS/Linux**`export AWS_BEARER_TOKEN_BEDROCK=`

`${api-key}`

-
**Windows**`setx AWS_BEARER_TOKEN_BEDROCK "`

`${api-key}`

"

-
-
Set it as an environment variable in your code before you make the API request. For example, you could include the following lines before making the request:

-
**Python**`import os os.environ['AWS_BEARER_TOKEN_BEDROCK'] = "`

`${api-key}`

"

-

-
-
**Specify it in a request**– You can include the Amazon Bedrock API key in the authorization header in the following ways (replace`$AWS_BEARER_TOKEN_BEDROCK`

with the actual value):-
**In a direct HTTP request**– Include the following as an authorization header:`Authorization: Bearer`

`$AWS_BEARER_TOKEN_BEDROCK`

-
**As a parameter in a supported SDK**– Specify the value in the parameter when setting up the client. For example, you can specify it in the`api_key`

field when setting up a client with the[OpenAI Python SDK](https://github.com/openai/openai-python?tab=readme-ov-file#usage).

-

###### Note

Amazon Bedrock API keys are limited to [Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_Operations_Amazon_Bedrock.html) and [Amazon Bedrock Runtime](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_Operations_Amazon_Bedrock_Runtime.html) actions. You can't use them with the following API operations:

-
[Agents for Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_Operations_Agents_for_Amazon_Bedrock.html)or[Agents for Amazon Bedrock Runtime](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_Operations_Agents_for_Amazon_Bedrock.html)API operations. -
[Data Automation for Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_Operations_Data_Automation_for_Amazon_Bedrock.html)or[Runtime for Amazon Bedrock Data Automation](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_Operations_Runtime_for_Amazon_Bedrock_Data_Automation)API operations.

To see an example of using the API key to send a [Converse](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_runtime_Converse.html) request to generate a response, choose the tab for your preferred method, and then follow the steps: