---
source_url: https://google.github.io/adk-docs/api-reference/agentconfig/
fetched_at: 2026-01-25T02:08:01.625025
---

# AgentConfig

The config for the YAML schema to create an agent.

The config for the YAML schema of a LlmAgent.

No Additional PropertiesThe value is used to uniquely identify the LlmAgent class. If it is empty, it is by default an LlmAgent.

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

No Additional PropertiesOptional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

No Additional PropertiesAn argument passed to a function or a class's constructor.

No Additional PropertiesOptional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.model. If not set, the model will be inherited from the ancestor.

Required. LlmAgent.instruction.

Optional. LlmAgent.disallow*transfer*to_parent.

Optional. LlmAgent.disallow*transfer*to_peers.

Optional. LlmAgent.input_schema.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.output_schema.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.output_key.

Optional. LlmAgent.include_contents.

Optional. LlmAgent.tools.

Examples:

For ADK built-in tools in `google.adk.tools`

package, they can be referenced

directly with the name:


```
tools:
- name: google_search
- name: load_memory
```


For user-defined tools, they can be referenced with fully qualified name:


```
tools:
- name: my_library.my_tools.my_tool
```


For tools that needs to be created via functions:


```
tools:
- name: my_library.my_tools.create_tool
args:
- name: param1
value: value1
- name: param2
value: value2
```


For more advanced tools, instead of specifying arguments in config, it's

recommended to define them in Python files and reference them. E.g.,


```
# tools.py
my_mcp_toolset = MCPToolset(
connection_params=StdioServerParameters(
command="npx",
args=["-y", "@notionhq/notion-mcp-server"],
env={"OPENAPI_MCP_HEADERS": NOTION_HEADERS},
)
)
```


Then, reference the toolset in config:


```
tools:
- name: tools.my_mcp_toolset
```


The configuration for a tool.

The config supports these types of tools:

1. ADK built-in tools

2. User-defined tool instances

3. User-defined tool classes

4. User-defined functions that generate tool instances

5. User-defined function tools

For examples:

For ADK built-in tool instances or classes in `google.adk.tools`

package,

they can be referenced directly with the `name`

and optionally with

`args`

.

```
tools:
- name: google_search
- name: AgentTool
args:
agent: ./another_agent.yaml
skip_summarization: true
```


For user-defined tool instances, the `name`

is the fully qualified path

to the tool instance.

```
tools:
- name: my_package.my_module.my_tool
```


For user-defined tool classes (custom tools), the `name`

is the fully

qualified path to the tool class and `args`

is the arguments for the tool.

```
tools:
- name: my_package.my_module.my_tool_class
args:
my_tool_arg1: value1
my_tool_arg2: value2
```


For user-defined functions that generate tool instances, the `name`

is

the fully qualified path to the function and `args`

is passed to the

function as arguments.

```
tools:
- name: my_package.my_module.my_tool_function
args:
my_function_arg1: value1
my_function_arg2: value2
```


The function must have the following signature:

```
def my_function(args: ToolArgsConfig) -> BaseTool:
...
```


For user-defined function tools, the `name`

is the fully qualified path

to the function.

```
tools:
- name: my_package.my_module.my_function_tool
```


If the above use cases don't suffice, users can define a custom tool config

by extending BaseToolConfig and override from_config() in the custom tool.

The args for the tool.

Config to host free key-value pairs for the args in ToolConfig.

Additional Properties of any type are allowed.

Type: objectOptional. LlmAgent.before*model*callbacks.

Example:


```
before_model_callbacks:
- name: my_library.callbacks.before_model_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.after*model*callbacks.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.before*tool*callbacks.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.after*tool*callbacks.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LlmAgent.generate*content*config.

Optional model configuration parameters.

For more information, see ```
Content generation parameters
<https://cloud.google.com/vertex-ai/generative-ai/docs/multimodal/content-generation-parameters>
```

_.

Used to override HTTP request options.

HTTP options to be used in each of the requests.

No Additional PropertiesThe base URL for the AI platform service endpoint.

Specifies the version of the API to use.

Additional HTTP headers to be sent with the request.

Each additional property must conform to the following schema

Type: stringTimeout for the request in milliseconds.

Args passed to the HTTP client.

Additional Properties of any type are allowed.

Type: objectArgs passed to the async HTTP client.

Additional Properties of any type are allowed.

Type: objectExtra parameters to add to the request body.

The structure must match the backend API's request structure.

- VertexAI backend API docs: https://cloud.google.com/vertex-ai/docs/reference/rest

- GeminiAPI backend API docs: https://ai.google.dev/api/rest

Additional Properties of any type are allowed.

Type: objectHTTP retry options for the request.

HTTP retry options to be used in each of the requests.

No Additional PropertiesMaximum number of attempts, including the original request.

If 0 or 1, it means no retries.

Initial delay before the first retry, in fractions of a second.

Maximum delay between retries, in fractions of a second.

Multiplier by which the delay increases after each attempt.

Randomness factor for the delay.

List of HTTP status codes that should trigger a retry.

If not specified, a default set of retryable codes may be used.

Instructions for the model to steer it toward better performance.

For example, "Answer as concisely as possible" or "Don't use technical

terms in your response".

Contains the multi-part content of a message.

No Additional PropertiesList of parts that constitute a single message. Each part may have

a different IANA MIME type.

A datatype containing media content.

Exactly one field within a Part should be set, representing the specific type

of content being conveyed. Using multiple fields within the same `Part`


instance is considered invalid.

Metadata for a given video.

Describes how the video in the Part should be used by the model.

No Additional PropertiesThe frame rate of the video sent to the model. If not specified, the

default value will be 1.0. The fps range is (0.0, 24.0].

Optional. The end offset of the video.

Optional. The start offset of the video.

Indicates if the part is thought from the model.

Optional. Inlined bytes data.

Content blob.

No Additional PropertiesOptional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is not currently used in the Gemini GenerateContent calls.

Required. Raw bytes.

Required. The IANA standard MIME type of the source data.

Optional. URI based data.

URI based data.

No Additional PropertiesOptional. Display name of the file data. Used to provide a label or filename to distinguish file datas. It is not currently used in the Gemini GenerateContent calls.

Required. URI.

Required. The IANA standard MIME type of the source data.

An opaque signature for the thought so it can be reused in subsequent requests.

Optional. Result of executing the [ExecutableCode].

Result of executing the [ExecutableCode].

Only generated when using the [CodeExecution] tool, and always follows a

`part`

containing the [ExecutableCode].

Required. Outcome of the code execution.

Required. Outcome of the code execution.

Optional. Contains stdout when code execution is successful, stderr or other description otherwise.

Optional. Code generated by the model that is meant to be executed.

Code generated by the model that is meant to be executed, and the result returned to the model.

Generated when using the [CodeExecution] tool, in which the code will be

automatically executed, and a corresponding [CodeExecutionResult] will also be

generated.

Required. The code to be executed.

Required. Programming language of the `code`

.

Required. Programming language of the `code`

.

Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values.

A function call.

No Additional PropertiesThe unique id of the function call. If populated, the client to execute the

`function_call`

and return the response with the matching `id`

.

Optional. The function parameters and values in JSON object format. See [FunctionDeclaration.parameters] for parameter details.

Additional Properties of any type are allowed.

Type: objectRequired. The name of the function to call. Matches [FunctionDeclaration.name].

Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model.

A function response.

No Additional PropertiesSignals that function call continues, and more responses will be returned, turning the function call into a generator. Is only applicable to NON*BLOCKING function calls (see FunctionDeclaration.behavior for details), ignored otherwise. If false, the default, future responses will not be considered. Is only applicable to NON*BLOCKING function calls, is ignored otherwise. If set to false, future responses will not be considered. It is allowed to return empty `response`

with `will_continue=False`

to signal that the function call is finished.

Specifies how the response should be scheduled in the conversation. Only applicable to NON*BLOCKING function calls, is ignored otherwise. Defaults to WHEN*IDLE.

Specifies how the response should be scheduled in the conversation.

Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id`

.

Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name].

Required. The function response in JSON object format. Use "output" key to specify function output and "error" key to specify error details (if any). If "output" and "error" keys are not specified, then whole "response" is treated as function output.

Additional Properties of any type are allowed.

Type: objectOptional. Text part (can be code).

Optional. The producer of the content. Must be either 'user' or

'model'. Useful to set for multi-turn conversations, otherwise can be

empty. If role is not specified, SDK will determine the role.

A file uploaded to the API.

No Additional PropertiesThe `File`

resource name. The ID (name excluding the "files/" prefix) can contain up to 40 characters that are lowercase alphanumeric or dashes (-). The ID cannot start or end with a dash. If the name is empty on create, a unique name will be generated. Example: `files/123-456`


Optional. The human-readable display name for the `File`

. The display name must be no more than 512 characters in length, including spaces. Example: 'Welcome Image'

Output only. MIME type of the file.

Output only. Size of the file in bytes.

Output only. The timestamp of when the `File`

was created.

Output only. The timestamp of when the `File`

will be deleted. Only set if the `File`

is scheduled to expire.

Output only. The timestamp of when the `File`

was last updated.

Output only. SHA-256 hash of the uploaded bytes. The hash value is encoded in base64 format.

Output only. The URI of the `File`

.

Output only. The URI of the `File`

, only set for downloadable (generated) files.

Output only. Processing state of the File.

State for the lifecycle of a File.

Output only. The source of the `File`

.

Source of the File.

Output only. Metadata for a video.

Additional Properties of any type are allowed.

Type: objectOutput only. Error status if File processing failed.

Status of a File that uses a common error model.

No Additional PropertiesA list of messages that carry the error details. There is a common set of message types for APIs to use.

Additional Properties of any type are allowed.

Type: objectA list of messages that carry the error details. There is a common set of message types for APIs to use.

The status code. 0 for OK, 1 for CANCELLED

A datatype containing media content.

Exactly one field within a Part should be set, representing the specific type

of content being conveyed. Using multiple fields within the same `Part`


instance is considered invalid.

A datatype containing media content.

Exactly one field within a Part should be set, representing the specific type

of content being conveyed. Using multiple fields within the same `Part`


instance is considered invalid.

Value that controls the degree of randomness in token selection.

Lower temperatures are good for prompts that require a less open-ended or

creative response, while higher temperatures can lead to more diverse or

creative results.

Tokens are selected from the most to least probable until the sum

of their probabilities equals this value. Use a lower value for less

random responses and a higher value for more random responses.

For each token selection step, the `top_k`

tokens with the

highest probabilities are sampled. Then tokens are further filtered based

on `top_p`

with the final token selected using temperature sampling. Use

a lower number for less random responses and a higher number for more

random responses.

Number of response variations to return.

Maximum number of tokens that can be generated in the response.

List of strings that tells the model to stop generating text if one

of the strings is encountered in the response.

Whether to return the log probabilities of the tokens that were

chosen by the model at each step.

Number of top candidate tokens to return the log probabilities for

at each generation step.

Positive values penalize tokens that already appear in the

generated text, increasing the probability of generating more diverse

content.

Positive values penalize tokens that repeatedly appear in the

generated text, increasing the probability of generating more diverse

content.

When `seed`

is fixed to a specific number, the model makes a best

effort to provide the same response for repeated requests. By default, a

random number is used.

Output response mimetype of the generated candidate text.

Supported mimetype:

- `text/plain`

: (default) Text output.

- `application/json`

: JSON response in the candidates.

The model needs to be prompted to output the appropriate response type,

otherwise the behavior is undefined.

This is a preview feature.

The `Schema`

object allows the definition of input and output data types.

These types can be objects, but also primitives and arrays.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema).

`application/json`

: Schema for JSON response.Additional Properties of any type are allowed.

Type: objectSchema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Can either be a boolean or an object; controls the presence of additional properties.

Optional. A map of definitions for use by `ref`

Only allowed at the root of the schema.

Each additional property must conform to the following schema

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Allows indirect references between schema nodes. The value should be a valid reference to a child of the root `defs`

. For example, the following schema defines a reference to a schema node named "Pet": type: object properties: pet: ref: #/defs/Pet defs: Pet: type: object properties: name: type: string The value of the "pet" property is a reference to the schema node named "Pet". See details in https://json-schema.org/understanding-json-schema/structuring

Optional. The value should be validated against any (one or more) of the subschemas in the list.

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Default value of the data.

Optional. The description of the data.

Optional. Possible values of the element of primitive type with enum format. Examples: 1. We can define direction as : {type:STRING, format:enum, enum:["EAST", NORTH", "SOUTH", "WEST"]} 2. We can define apartment number as : {type:INTEGER, format:enum, enum:["101", "201", "301"]}

Optional. Example of the object. Will only populated when the object is the root.

Optional. The format of the data. Supported formats: for NUMBER type: "float", "double" for INTEGER type: "int32", "int64" for STRING type: "email", "byte", etc

Optional. SCHEMA FIELDS FOR TYPE ARRAY Schema of the elements of Type.ARRAY.

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Maximum number of the elements for Type.ARRAY.

Optional. Maximum length of the Type.STRING

Optional. Maximum number of the properties for Type.OBJECT.

Optional. Maximum value of the Type.INTEGER and Type.NUMBER

Optional. Minimum number of the elements for Type.ARRAY.

Optional. SCHEMA FIELDS FOR TYPE STRING Minimum length of the Type.STRING

Optional. Minimum number of the properties for Type.OBJECT.

Optional. SCHEMA FIELDS FOR TYPE INTEGER and NUMBER Minimum value of the Type.INTEGER and Type.NUMBER

Optional. Indicates if the value may be null.

Optional. Pattern of the Type.STRING to restrict a string to a regular expression.

Optional. SCHEMA FIELDS FOR TYPE OBJECT Properties of Type.OBJECT.

Each additional property must conform to the following schema

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. The order of the properties. Not a standard field in open api spec. Only used to support the order of the properties.

Optional. Required properties of Type.OBJECT.

Optional. The title of the Schema.

Optional. The type of the data.

Optional. The type of the data.

Optional. Output schema of the generated response.

This is an alternative to `response_schema`

that accepts [JSON
Schema](https://json-schema.org/). If set,

`response_schema`

must be`response_mime_type`

is required. While the full JSON Schema`$id`

- `$defs`

- `$ref`

- `$anchor`

`type`

- `format`

- `title`

- `description`

- `enum`

(for strings and`items`

- `prefixItems`

- `minItems`

- `maxItems`

- `minimum`

-`maximum`

- `anyOf`

- `oneOf`

(interpreted the same as `anyOf`

) -`properties`

- `additionalProperties`

- `required`

The non-standard`propertyOrdering`

property may also be set. Cyclic references are`$ref`

is set on a sub-schema, no other properties, except for than those`$`

, may be set.Configuration for model router requests.

The configuration for routing the request to a specific model.

No Additional PropertiesAutomated routing.

When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

No Additional PropertiesThe model routing preference.

Manual routing.

When manual routing is set, the specified model will be used directly.

No Additional PropertiesThe model name to use. Only the public LLM models are accepted. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models).

Configuration for model selection.

Config for model selection.

No Additional PropertiesOptions for feature selection preference.

Options for feature selection preference.

Safety settings in the request to block unsafe content in the

response.

Safety settings.

No Additional PropertiesDetermines if the harm block method uses probability or probability

and severity scores.

Optional.

Specify if the threshold is used for probability or severity score. If not

specified, the threshold is used for probability score.

Required. Harm category.

Required. Harm category.

Required. The harm block threshold.

Required. The harm block threshold.

Code that enables the system to interact with external systems to

perform an action outside of the knowledge and scope of the model.

Tool details of a tool that the model may use to generate a response.

No Additional PropertiesList of function declarations that the tool supports.

Defines a function that the model can generate JSON inputs for.

The inputs are based on ```
OpenAPI 3.0 specifications
<https://spec.openapis.org/oas/v3.0.3>
```

_.

Defines the function behavior.

Defines the function behavior. Defaults to `BLOCKING`

.

Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function.

Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots and dashes, with a maximum length of 64.

Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example: `{ "type": "object", "properties": { "name": { "type": "string" }, "age": { "type": "integer" } }, "additionalProperties": false, "required": ["name", "age"], "propertyOrdering": ["name", "age"] }`

This field is mutually exclusive with `parameters`

.

Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function.

Schema is used to define the format of input/output data.

Represents a select subset of an [OpenAPI 3.0 schema
object](https://spec.openapis.org/oas/v3.0.3#schema-object). More fields may

Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function. This field is mutually exclusive with `response`

.

Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation.

Defines a retrieval tool that model can call to access external knowledge.

No Additional PropertiesOptional. Deprecated. This option is no longer supported.

Use data source powered by external API for grounding.

Retrieve from data source powered by external API for grounding.

The external API is not owned by Google, but need to follow the pre-defined

API spec.

The authentication config to access the API. Deprecated. Please use auth_config instead.

The generic reusable api auth config.

Deprecated. Please use AuthConfig (google/cloud/aiplatform/master/auth.proto)

instead.

The API secret.

The API secret.

No Additional PropertiesRequired. The SecretManager secret version resource name storing API key. e.g. projects/{project}/secrets/{secret}/versions/{version}

The API key string. Either this or `api_key_secret_version`

must be set.

The API spec that the external API implements.

The API spec that the external API implements.

The authentication config to access the API.

Auth configuration to run the extension.

No Additional PropertiesConfig for API key auth.

Config for authentication with API key.

No Additional PropertiesThe API key to be used in the request directly.

Type of auth scheme.

Type of auth scheme.

Config for Google Service Account auth.

Config for Google Service Account Authentication.

No Additional PropertiesOptional. The service account that the extension execution service runs as. - If the service account is specified, the `iam.serviceAccounts.getAccessToken`

permission should be granted to Vertex AI Extension Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) on the specified service account. - If not specified, the Vertex AI Extension Service Agent will be used to execute the Extension.

Config for HTTP Basic auth.

Config for HTTP Basic Authentication.

No Additional PropertiesRequired. The name of the SecretManager secret version resource storing the base64 encoded credentials. Format: `projects/{project}/secrets/{secrete}/versions/{version}`

- If specified, the `secretmanager.versions.access`

permission should be granted to Vertex AI Extension Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) on the specified resource.

Config for user oauth.

Config for user oauth.

No Additional PropertiesAccess token for extension endpoint. Only used to propagate token from [[ExecuteExtensionRequest.runtime*auth*config]] at request time.

The service account used to generate access tokens for executing the Extension. - If the service account is specified, the `iam.serviceAccounts.getAccessToken`

permission should be granted to Vertex AI Extension Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) on the provided service account.

Config for user OIDC auth.

Config for user OIDC auth.

No Additional PropertiesOpenID Connect formatted ID token for extension endpoint. Only used to propagate token from [[ExecuteExtensionRequest.runtime*auth*config]] at request time.

The service account used to generate an OpenID Connect (OIDC)-compatible JWT token signed by the Google OIDC Provider (accounts.google.com) for extension endpoint (https://cloud.google.com/iam/docs/create-short-lived-credentials-direct#sa-credentials-oidc). - The audience for the token will be set to the URL in the server url defined in the OpenApi spec. - If the service account is provided, the service account should grant `iam.serviceAccounts.getOpenIdToken`

permission to Vertex AI Extension Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents).

Parameters for the elastic search API.

The search parameters to use for the ELASTIC_SEARCH spec.

No Additional PropertiesThe ElasticSearch index to use.

Optional. Number of hits (chunks) to request. When specified, it is passed to Elasticsearch as the `num_hits`

param.

The ElasticSearch search template to use.

The endpoint of the external API. The system will call the API at this endpoint to retrieve the data for grounding. Example: https://acme.com:443/search

Parameters for the simple search API.

The search parameters to use for SIMPLE_SEARCH spec.

Set to use data source powered by Vertex AI Search.

Retrieve from Vertex AI Search datastore or engine for grounding.

datastore and engine are mutually exclusive. See

https://cloud.google.com/products/agent-builder

Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used.

Define data stores within engine to filter on in a search call and configurations for those data stores.

For more information, see

https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec

Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`


Optional. Filter specification to filter documents in the data store specified by data_store field. For more information on filtering, see [Filtering](https://cloud.google.com/generative-ai-app-builder/docs/filter-search-metadata)

Optional. Fully-qualified Vertex AI Search data store resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`


Optional. Fully-qualified Vertex AI Search engine resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}`


Optional. Filter strings to be passed to the search API.

Optional. Number of search results to return per query. The default value is 10. The maximumm allowed value is 10.

Set to use data source powered by Vertex RAG store. User data is uploaded via the VertexRagDataService.

Retrieve from Vertex RAG Store for grounding.

No Additional PropertiesOptional. Deprecated. Please use rag_resources instead.

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

The definition of the Rag resource.

No Additional PropertiesOptional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`


Optional. rag*file*id. The files should be in the same rag*corpus set in rag*corpus field.

Optional. The retrieval config for the Rag query.

Specifies the context retrieval config.

No Additional PropertiesOptional. Config for filters.

Config for filters.

No Additional PropertiesOptional. String for metadata filtering.

Optional. Only returns contexts with vector distance smaller than the threshold.

Optional. Only returns contexts with vector similarity larger than the threshold.

Optional. Config for Hybrid Search.

Config for Hybrid Search.

No Additional PropertiesOptional. Alpha value controls the weight between dense and sparse vector search results. The range is [0, 1], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally.

Optional. Config for ranking and reranking.

Config for ranking and reranking.

No Additional PropertiesOptional. Config for LlmRanker.

Config for LlmRanker.

No Additional PropertiesOptional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models).

Optional. Config for Rank Service.

Config for Rank Service.

No Additional PropertiesOptional. The model name of the rank service. Format: `semantic-ranker-512@latest`


Optional. The number of contexts to retrieve.

Optional. Number of top k results to return from the selected corpora.

Optional. Currently only supported for Gemini Multimodal Live API. In Gemini Multimodal Live API, if `store_context`

bool is specified, Gemini will leverage it to automatically memorize the interactions between the client and Gemini, and retrieve context when needed to augment the response generation for users' ongoing and future interactions.

Optional. Only return results with vector distance smaller than the threshold.

Optional. Google Search tool type. Specialized retrieval tool

that is powered by Google Search.

Tool to support Google Search in Model. Powered by Google.

No Additional PropertiesOptional. Filter search results to a specific time range.

If customers set a start time, they must set an end time (and vice versa).

Represents a time interval, encoded as a start time (inclusive) and an end time (exclusive).

The start time must be less than or equal to the end time.

When the start equals the end time, the interval is an empty interval.

(matches no time)

When both start and end are unspecified, the interval matches any time.

The start time of the interval.

The end time of the interval.

Optional. GoogleSearchRetrieval tool type. Specialized retrieval tool that is powered by Google search.

Tool to retrieve public web data for grounding, powered by Google.

No Additional PropertiesSpecifies the dynamic retrieval configuration for the given source.

Describes the options to customize dynamic retrieval.

No Additional PropertiesThe mode of the predictor to be used in dynamic retrieval.

Config for the dynamic retrieval config mode.

Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used.

Optional. Enterprise web search tool type. Specialized retrieval

tool that is powered by Vertex AI Search and Sec4 compliance.

Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

Optional. Google Maps tool type. Specialized retrieval tool

that is powered by Google Maps.

Tool to support Google Maps in Model.

No Additional PropertiesOptional. Auth config for the Google Maps tool.

Optional. Tool to support URL context retrieval.

Tool to support URL context retrieval.

Optional. CodeExecution tool type. Enables the model to execute code as part of generation.

Tool that executes code generated by the model, and automatically returns the result to the model.

See also [ExecutableCode]and [CodeExecutionResult] which are input and output

to this tool.

Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations.

Tool to support computer use.

No Additional PropertiesRequired. The environment being operated.

Required. The environment being operated.

Definition for a tool the client can call.

Additional Properties of any type are allowed.

Type: objectAdditional Properties of any type are allowed.

Type: objectAdditional properties describing a Tool to clients.

NOTE: all properties in ToolAnnotations are **hints**.

They are not guaranteed to provide a faithful description of

tool behavior (including descriptive properties like `title`

).

Clients should never make tool use decisions based on ToolAnnotations

received from untrusted servers.

Additional Properties of any type are allowed.

Type: objectAdditional Properties of any type are allowed.

Type: objectAdditional Properties of any type are allowed.

Type: objectAssociates model output to a specific function call.

Tool config.

This config is shared for all tools provided in the request.

No Additional PropertiesOptional. Function calling config.

Function calling config.

No Additional PropertiesOptional. Function calling mode.

Config for the function calling config mode.

Optional. Function names to call. Only set when the Mode is ANY. Function names should match [FunctionDeclaration.name]. With mode set to ANY, model will predict a function call from the set of function names provided.

Optional. Retrieval config.

Retrieval config.

No Additional PropertiesOptional. The location of the user.

An object that represents a latitude/longitude pair.

This is expressed as a pair of doubles to represent degrees latitude and

degrees longitude. Unless specified otherwise, this object must conform to the

<a href="https://en.wikipedia.org/wiki/World_Geodetic_System#1984_version">

WGS84 standard</a>. Values must be within normalized ranges.

The latitude in degrees. It must be in the range [-90.0, +90.0].

The longitude in degrees. It must be in the range [-180.0, +180.0]

The language code of the user.

Labels with user-defined metadata to break down billed charges.

Each additional property must conform to the following schema

Type: stringResource name of a context cache that can be used in subsequent

requests.

The requested modalities of the response. Represents the set of

modalities that the model can return.

If specified, the media resolution specified will be used.

The media resolution to use.

The speech generation configuration.

The speech generation configuration.

No Additional PropertiesThe configuration for the speaker to use.

The configuration for the voice to use.

No Additional PropertiesThe configuration for the speaker to use.

The configuration for the prebuilt speaker to use.

No Additional PropertiesThe name of the prebuilt voice to use.

The configuration for the multi-speaker setup.

It is mutually exclusive with the voice_config field.

The configuration for the multi-speaker setup.

No Additional PropertiesThe configuration for the speaker to use.

The configuration for the speaker to use.

No Additional PropertiesThe name of the speaker to use. Should be the same as in the

prompt.

The configuration for the voice to use.

Language code (ISO 639. e.g. en-US) for the speech synthesization.

Only available for Live API.

If enabled, audio timestamp will be included in the request to the

model.

The configuration for automatic function calling.

The configuration for automatic function calling.

No Additional PropertiesWhether to disable automatic function calling.

If not set or set to False, will enable automatic function calling.

If set to True, will disable automatic function calling.

If automatic function calling is enabled,

maximum number of remote calls for automatic function calling.

This number should be a positive integer.

If not set, SDK will set maximum number of remote calls to 10.

The thinking features configuration.

The thinking features configuration.

No Additional PropertiesIndicates whether to include thoughts in the response. If true, thoughts are returned only if the model supports thought and thoughts are available.

Indicates the thinking budget in tokens. 0 is DISABLED. -1 is AUTOMATIC. The default values and allowed ranges are model dependent.

The config for the YAML schema of a LoopAgent.

No Additional PropertiesThe value is used to uniquely identify the LoopAgent class.

Specific value:`"LoopAgent"`

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

Optional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. LoopAgent.max_iterations.

The config for the YAML schema of a ParallelAgent.

No Additional PropertiesThe value is used to uniquely identify the ParallelAgent class.

Specific value:`"ParallelAgent"`

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

Optional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

The config for the YAML schema of a SequentialAgent.

No Additional PropertiesThe value is used to uniquely identify the SequentialAgent class.

Specific value:`"SequentialAgent"`

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

Optional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

The config for the YAML schema of a BaseAgent.

Do not use this class directly. It's the base class for all agent configs.

Required. The class of the agent. The value is used to differentiate among different agent classes.

`"BaseAgent"`

Required. The name of the agent.

Optional. The description of the agent.

Optional. The sub-agents of the agent.

The config for the reference to another agent.

Optional. The before*agent*callbacks of the agent.

Example:


```
before_agent_callbacks:
- name: my_library.security_callbacks.before_agent_callback
```


Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Optional. The after*agent*callbacks of the agent.

Code reference config for a variable, a function, or a class.

This config is used for configuring callbacks and tools.

Additional Properties of any type are allowed.

Type: object