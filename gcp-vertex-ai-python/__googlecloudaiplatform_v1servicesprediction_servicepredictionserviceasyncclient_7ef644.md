---
merged_at: 2026-01-25T21:47:44.346787
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesprediction_servicepredictionserviceasyncclient__25a2d1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesprediction_servicepredictionserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient -->

# Class PredictionServiceAsyncClient (1.134.0)

```
PredictionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.prediction_service.transports.base.PredictionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.prediction_service.transports.base.PredictionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for online predictions and explanations.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`PredictionServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### PredictionServiceAsyncClient

```
PredictionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.prediction_service.transports.base.PredictionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.prediction_service.transports.base.PredictionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the prediction service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PredictionServiceTransport,Callable[..., PredictionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the PredictionServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTlsChannelError` |
If mutual TLS transport creation failed for any reason. |

### cached_content_path

`cached_content_path(project: str, location: str, cached_content: str) -> str`


Returns a fully-qualified cached_content string.

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### direct_predict

```
direct_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.DirectPredictRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.prediction_service.DirectPredictResponse
```


Perform an unary online prediction request to a gRPC model server for Vertex first-party products and frameworks.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_direct_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DirectPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DirectPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = await client.[direct_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_direct_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PredictionService.DirectPredict. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for PredictionService.DirectPredict. |

### direct_raw_predict

```
direct_raw_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.DirectRawPredictRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.prediction_service.DirectRawPredictResponse
```


Perform an unary online prediction request to a gRPC model server for custom containers.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_direct_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DirectRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DirectRawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = await client.[direct_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_direct_raw_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PredictionService.DirectRawPredict. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for PredictionService.DirectRawPredict. |

### embed_content

```
embed_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.EmbedContentRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
content: typing.Optional[google.cloud.aiplatform_v1.types.content.Content] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.prediction_service.EmbedContentResponse
```


Embed content with multimodal inputs.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_embed_content():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[EmbedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EmbedContentRequest.html)(
)
# Make the request
response = await client.[embed_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_embed_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PredictionService.EmbedContent. |
`model` |
Required. The name of the publisher model requested to serve the prediction. Format: |
`content` |
Required. Input content to be embedded. Required. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for PredictionService.EmbedContent. |

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### explain

```
explain(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.ExplainRequest, dict
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
parameters: typing.Optional[google.protobuf.struct_pb2.Value] = None,
deployed_model_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.prediction_service.ExplainResponse
```


Perform an online explanation.

If xref_deployed_model_id is specified, the corresponding DeployModel must have xref_explanation_spec populated. If xref_deployed_model_id is not specified, all DeployedModels must have xref_explanation_spec populated.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_explain():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
instances = aiplatform_v1.Value()
instances.null_value = "NULL_VALUE"
request = aiplatform_v1.[ExplainRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplainRequest.html)(
endpoint="endpoint_value",
instances=instances,
)
# Make the request
response = await client.[explain](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_explain)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PredictionService.Explain. |
`endpoint` |
Required. The name of the Endpoint requested to serve the explanation. Format: |
`instances` |
`:class:`
Required. The instances that are the input to the explanation call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the explanation call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri. This corresponds to the |
`parameters` |
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] parameters_schema_uri. This corresponds to the |
`deployed_model_id` |
If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding Endpoint.traffic_split. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for PredictionService.Explain. |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`PredictionServiceAsyncClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`PredictionServiceAsyncClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`PredictionServiceAsyncClient` |
The constructed client. |

### generate_content

```
generate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.GenerateContentRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
contents: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1.types.content.Content]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.prediction_service.GenerateContentResponse
```


Generate content with multimodal inputs.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_generate_content():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
contents = aiplatform_v1.[Content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Content.html)()
contents.parts.text = "text_value"
request = aiplatform_v1.[GenerateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentRequest.html)(
model="model_value",
contents=contents,
)
# Make the request
response = await client.[generate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_generate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [PredictionService.GenerateContent]. |
`model` |
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: |
`contents` |
`:class:`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for [PredictionService.GenerateContent]. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.prediction_service.transports.base.PredictionServiceTransport
]
```


Returns an appropriate transport class.

Parameter |
|
|---|---|
Name |
Description |
`label` |
`typing.Optional[str]`
The name of the desired transport. If none is provided, then the first transport in the registry is used. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### parse_cached_content_path

`parse_cached_content_path(path: str) -> typing.Dict[str, str]`


Parses a cached_content path into its component segments.

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_template_path

`parse_template_path(path: str) -> typing.Dict[str, str]`


Parses a template path into its component segments.

### predict

```
predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.PredictRequest, dict
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
parameters: typing.Optional[google.protobuf.struct_pb2.Value] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.prediction_service.PredictResponse
```


Perform an online prediction.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
instances = aiplatform_v1.Value()
instances.null_value = "NULL_VALUE"
request = aiplatform_v1.[PredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredictRequest.html)(
endpoint="endpoint_value",
instances=instances,
)
# Make the request
response = await client.[predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PredictionService.Predict. |
`endpoint` |
Required. The name of the Endpoint requested to serve the prediction. Format: |
`instances` |
`:class:`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri. This corresponds to the |
`parameters` |
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] parameters_schema_uri. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for PredictionService.Predict. |

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### raw_predict

```
raw_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.RawPredictRequest, dict
]
] = None,
*,
endpoint: typing.Optional[str] = None,
http_body: typing.Optional[google.api.httpbody_pb2.HttpBody] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api.httpbody_pb2.HttpBody
```


Perform an online prediction with an arbitrary HTTP payload.

The response includes the following HTTP headers:

`X-Vertex-AI-Endpoint-Id`

: ID of the xref_Endpoint that served this prediction.`X-Vertex-AI-Deployed-Model-Id`

: ID of the Endpoint's xref_DeployedModel that served this prediction.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = await client.[raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_raw_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PredictionService.RawPredict. |
`endpoint` |
Required. The name of the Endpoint requested to serve the prediction. Format: |
`http_body` |
The prediction input. Supports HTTP headers and arbitrary data payload. A DeployedModel may have an upper limit on the number of instances it supports per request. When this limit it is exceeded for an AutoML model, the RawPredict method returns an error. When this limit is exceeded for a custom-trained model, the behavior varies depending on the model. You can specify the schema for each instance in the predict_schemata.instance_schema_uri field when you create a Model. This schema applies when you deploy the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api.httpbody_pb2.HttpBody` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

### server_streaming_predict

```
server_streaming_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.StreamingPredictRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Awaitable[
typing.AsyncIterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamingPredictResponse
]
]
```


Perform a server-side streaming online prediction request for Vertex LLM streaming.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_server_streaming_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamingPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = await client.[server_streaming_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_server_streaming_predict)(request=request)
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PredictionService.StreamingPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[` |
Response message for PredictionService.StreamingPredict. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### stream_direct_predict

```
stream_direct_predict(
requests: typing.Optional[
typing.AsyncIterator[
google.cloud.aiplatform_v1.types.prediction_service.StreamDirectPredictRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Awaitable[
typing.AsyncIterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamDirectPredictResponse
]
]
```


Perform a streaming online prediction request to a gRPC model server for Vertex first-party products and frameworks.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stream_direct_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamDirectPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamDirectPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1.StreamDirectPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = await client.[stream_direct_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_stream_direct_predict)(requests=request_generator())
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`AsyncIterator[`
The request object AsyncIterator. Request message for PredictionService.StreamDirectPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[` |
Response message for PredictionService.StreamDirectPredict. |

### stream_direct_raw_predict

```
stream_direct_raw_predict(
requests: typing.Optional[
typing.AsyncIterator[
google.cloud.aiplatform_v1.types.prediction_service.StreamDirectRawPredictRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Awaitable[
typing.AsyncIterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamDirectRawPredictResponse
]
]
```


Perform a streaming online prediction request to a gRPC model server for custom containers.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stream_direct_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamDirectRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamDirectRawPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1.StreamDirectRawPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = await client.[stream_direct_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_stream_direct_raw_predict)(requests=request_generator())
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`AsyncIterator[`
The request object AsyncIterator. Request message for PredictionService.StreamDirectRawPredict. The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[` |
Response message for PredictionService.StreamDirectRawPredict. |

### stream_generate_content

```
stream_generate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.GenerateContentRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
contents: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1.types.content.Content]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Awaitable[
typing.AsyncIterable[
google.cloud.aiplatform_v1.types.prediction_service.GenerateContentResponse
]
]
```


Generate content with multimodal inputs with streaming support.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stream_generate_content():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
contents = aiplatform_v1.[Content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Content.html)()
contents.parts.text = "text_value"
request = aiplatform_v1.[GenerateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentRequest.html)(
model="model_value",
contents=contents,
)
# Make the request
stream = await client.[stream_generate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_stream_generate_content)(request=request)
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [PredictionService.GenerateContent]. |
`model` |
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: |
`contents` |
`:class:`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[` |
Response message for [PredictionService.GenerateContent]. |

### stream_raw_predict

```
stream_raw_predict(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.StreamRawPredictRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
http_body: typing.Optional[google.api.httpbody_pb2.HttpBody] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Awaitable[typing.AsyncIterable[google.api.httpbody_pb2.HttpBody]]
```


Perform a streaming online prediction with an arbitrary HTTP payload.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stream_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamRawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = await client.[stream_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_stream_raw_predict)(request=request)
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PredictionService.StreamRawPredict. |
`endpoint` |
Required. The name of the Endpoint requested to serve the prediction. Format: |
`http_body` |
The prediction input. Supports HTTP headers and arbitrary data payload. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

### streaming_predict

```
streaming_predict(
requests: typing.Optional[
typing.AsyncIterator[
google.cloud.aiplatform_v1.types.prediction_service.StreamingPredictRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Awaitable[
typing.AsyncIterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamingPredictResponse
]
]
```


Perform a streaming online prediction request for Vertex first-party products and frameworks.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_streaming_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamingPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1.StreamingPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = await client.[streaming_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_streaming_predict)(requests=request_generator())
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`AsyncIterator[`
The request object AsyncIterator. Request message for PredictionService.StreamingPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[` |
Response message for PredictionService.StreamingPredict. |

### streaming_raw_predict

```
streaming_raw_predict(
requests: typing.Optional[
typing.AsyncIterator[
google.cloud.aiplatform_v1.types.prediction_service.StreamingRawPredictRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Awaitable[
typing.AsyncIterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamingRawPredictResponse
]
]
```


Perform a streaming online prediction request through gRPC.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_streaming_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamingRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingRawPredictRequest.html)(
endpoint="endpoint_value",
)
# This method expects an iterator which contains
# 'aiplatform_v1.StreamingRawPredictRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = await client.[streaming_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceAsyncClient_streaming_raw_predict)(requests=request_generator())
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`AsyncIterator[`
The request object AsyncIterator. Request message for PredictionService.StreamingRawPredict. The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[` |
Response message for PredictionService.StreamingRawPredict. |

### template_path

`template_path(project: str, location: str, template: str) -> str`


Returns a fully-qualified template string.

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |


---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesgetdatalabelingjobrequest_googlecloudaiplatfo_619dfd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesgetdatalabelingjobrequest_googlecloudaiplatfor_6ef320.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesgetdatalabelingjobrequest_googlecloudaiplatform_82dc60.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesgetdatalabelingjobrequest_googlecloudaiplatform__432e1e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgetdatalabelingjobrequest_googlecloudaiplatform_v_403a22.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetdatalabelingjobrequest_googlecloudaiplatform_v1_0bcbca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetdatalabelingjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDataLabelingJobRequest -->

# Class GetDataLabelingJobRequest (1.134.0)

`GetDataLabelingJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetDataLabelingJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DataLabelingJob. Format: `projects/{project}/locations/{location}/dataLabelingJobs/{data_labeling_job}`
|

## Methods

### GetDataLabelingJobRequest

`GetDataLabelingJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetDataLabelingJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescancelpipelinejobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelPipelineJobRequest -->

# Class CancelPipelineJobRequest (1.134.0)

`CancelPipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.CancelPipelineJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PipelineJob to cancel. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipeline_job}`
|

## Methods

### CancelPipelineJobRequest

`CancelPipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.CancelPipelineJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfindneighborsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsRequest -->

# Class FindNeighborsRequest (1.134.0)

`FindNeighborsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The request message for MatchService.FindNeighbors.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the index endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index_id` |
`str`
The ID of the DeployedIndex that will serve the request. This request is sent to a specific IndexEndpoint, as per the IndexEndpoint.network. That IndexEndpoint also has IndexEndpoint.deployed_indexes, and each such index has a DeployedIndex.id field. The value of the field below must equal one of the DeployedIndex.id fields of the IndexEndpoint that is being called for this request. |
`queries` |
`MutableSequence[`
The list of queries. |
`return_full_datapoint` |
`bool`
If set to true, the full datapoints (including all vector values and restricts) of the nearest neighbors are returned. Note that returning full datapoint will significantly increase the latency and cost of the query. |

## Classes

### Query

`Query(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A query to find a number of the nearest neighbors (most similar vectors) of a vector.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### FindNeighborsRequest

`FindNeighborsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The request message for MatchService.FindNeighbors.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessampleconfig__googlecloudaiplatform_v1typesge_445e8c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessampleconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SampleConfig -->

# Class SampleConfig (1.134.0)

`SampleConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Active learning data sampling config. For every active learning labeling iteration, it will select a batch of data based on the sampling strategy.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`initial_batch_sample_percentage` |
`int`
The percentage of data needed to be labeled in the first batch. This field is a member of `oneof` _ `initial_batch_sample_size` .
|
`following_batch_sample_percentage` |
`int`
The percentage of data needed to be labeled in each following batch (except the first batch). This field is a member of `oneof` _ `following_batch_sample_size` .
|
`sample_strategy` |
Field to choose sampling strategy. Sampling strategy will decide which data should be selected for human labeling in every batch. |

## Classes

### SampleStrategy

`SampleStrategy(value)`


Sample strategy decides which subset of DataItems should be selected for human labeling in every batch.

## Methods

### SampleConfig

`SampleConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Active learning data sampling config. For every active learning labeling iteration, it will select a batch of data based on the sampling strategy.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetindexendpointrequest_googlecloudaiplatform_v1ty_d96e45.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetindexendpointrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetIndexEndpointRequest -->

# Class GetIndexEndpointRequest (1.134.0)

`GetIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.GetIndexEndpoint

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the IndexEndpoint resource. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|

## Methods

### GetIndexEndpointRequest

`GetIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.GetIndexEndpoint


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslargemodelreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LargeModelReference -->

# Class LargeModelReference (1.134.0)

`LargeModelReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the Large Model.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The unique name of the large Foundation or pre-built model. Like "chat-bison", "text-bison". Or model name with version ID, like "chat-bison@001", "text-bison@005", etc. |

## Methods

### LargeModelReference

`LargeModelReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the Large Model.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeaturegroupbigquery__googlecloudaiplatform_v1typ_f46676.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeaturegroupbigquery__googlecloudaiplatform_v1type_c76ecb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturegroupbigquery.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureGroup.BigQuery -->

# Class BigQuery (1.134.0)

`BigQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input source type for BigQuery Tables and Views.

## Attributes |
|
|---|---|
Name |
Description |
`big_query_source` |
Required. Immutable. The BigQuery source URI that points to either a BigQuery Table or View. |
`entity_id_columns` |
`MutableSequence[str]`
Optional. Columns to construct entity_id / row keys. If not provided defaults to `entity_id` .
|
`static_data_source` |
`bool`
Optional. Set if the data source is not a time-series. |
`time_series` |
Optional. If the source is a time-series source, this can be set to control how downstream sources (ex: FeatureView ) will treat time-series sources. If not set, will treat the source as a time-series source with `feature_timestamp` as
timestamp column and no scan boundary.
|
`dense` |
`bool`
Optional. If set, all feature values will be fetched from a single row per unique entityId including nulls. If not set, will collapse all rows for each unique entityId into a singe row with any non-null values if present, if no non-null values are present will sync null. ex: If source has schema `(entity_id, feature_timestamp, f0, f1)` and the following
rows: `(e1, 2020-01-01T10:00:00.123Z, 10, 15)`
`(e1, 2020-02-01T10:00:00.123Z, 20, null)` If dense is
set, `(e1, 20, null)` is synced to online stores. If dense
is not set, `(e1, 20, 15)` is synced to online stores.
|

## Classes

### TimeSeries

`TimeSeries(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### BigQuery

`BigQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input source type for BigQuery Tables and Views.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistmodelsresponse_googlecloudaiplatform_v1typesde_c29940.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodelsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelsResponse -->

# Class ListModelsResponse (1.134.0)

`ListModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModels

## Attributes |
|
|---|---|
Name |
Description |
`models` |
`MutableSequence[`
List of Models in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListModelsRequest.page_token to obtain that page. |

## Methods

### ListModelsResponse

`ListModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModels


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeaturevaluesoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesOperationMetadata -->

# Class DeleteFeatureValuesOperationMetadata (1.134.0)

```
DeleteFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that delete Feature values.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore delete Features values. |

## Methods

### DeleteFeatureValuesOperationMetadata

```
DeleteFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that delete Feature values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitor -->

# Class ModelMonitor (1.134.0)

`ModelMonitor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Model Monitoring Service serves as a central hub for the analysis and visualization of data quality and performance related to models. ModelMonitor stands as a top level resource for overseeing your model monitoring tasks.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`tabular_objective` |
Optional default tabular model monitoring objective. This field is a member of `oneof` _ `default_objective` .
|
`name` |
`str`
Immutable. Resource name of the ModelMonitor. Format: `projects/{project}/locations/{location}/modelMonitors/{model_monitor}` .
|
`display_name` |
`str`
The display name of the ModelMonitor. The name can be up to 128 characters long and can consist of any UTF-8. |
`model_monitoring_target` |
The entity that is subject to analysis. Currently only models in Vertex AI Model Registry are supported. If you want to analyze the model which is outside the Vertex AI, you could register a model in Vertex AI Model Registry using just a display name. |
`training_dataset` |
Optional training dataset used to train the model. It can serve as a reference dataset to identify changes in production. |
`notification_spec` |
Optional default notification spec, it can be overridden in the ModelMonitoringJob notification spec. |
`output_spec` |
Optional default monitoring metrics/logs export spec, it can be overridden in the ModelMonitoringJob output spec. If not specified, a default Google Cloud Storage bucket will be created under your project. |
`explanation_spec` |
Optional model explanation spec. It is used for feature attribution monitoring. |
`model_monitoring_schema` |
Monitoring Schema is to specify the model's features, prediction outputs and ground truth properties. It is used to extract pertinent data from the dataset and to process features based on their properties. Make sure that the schema aligns with your dataset, if it does not, we will be unable to extract data from the dataset. It is required for most models, but optional for Vertex AI AutoML Tables unless the schem information is not available. |
`encryption_spec` |
Customer-managed encryption key spec for a ModelMonitor. If set, this ModelMonitor and all sub-resources of this ModelMonitor will be secured by this key. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelMonitor was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelMonitor was updated most recently. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### ModelMonitoringTarget

`ModelMonitoringTarget(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The monitoring target refers to the entity that is subject to analysis. e.g. Vertex AI Model version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ModelMonitor

`ModelMonitor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Model Monitoring Service serves as a central hub for the analysis and visualization of data quality and performance related to models. ModelMonitor stands as a top level resource for overseeing your model monitoring tasks.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeature__googlecloudaiplatform_v1typeslistindexen_fd7b81.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeature__googlecloudaiplatform_v1typeslistindexend_fa107c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeature.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Feature -->

# Class Feature (1.134.0)

`Feature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature Metadata information. For example, color is a feature that describes an apple.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. Name of the Feature. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}/features/{feature}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}/features/{feature}`
The last part feature is assigned by the client. The feature
can be up to 64 characters long and can consist only of
ASCII Latin letters A-Z and a-z, underscore(\_), and ASCII
digits 0-9 starting with a letter. The value will be unique
given an entity type.
|
`description` |
`str`
Description of the Feature. |
`value_type` |
Immutable. Only applicable for Vertex AI Feature Store (Legacy). Type of Feature value. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Only applicable for Vertex AI Feature Store (Legacy). Timestamp when this EntityType was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Only applicable for Vertex AI Feature Store (Legacy). Timestamp when this EntityType was most recently updated. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your Features. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one Feature (System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`disable_monitoring` |
`bool`
Optional. Only applicable for Vertex AI Feature Store (Legacy). If not set, use the monitoring_config defined for the EntityType this Feature belongs to. Only Features with type (Feature.ValueType) BOOL, STRING, DOUBLE or INT64 can enable monitoring. If set to true, all types of data monitoring are disabled despite the config on EntityType. |
`monitoring_stats_anomalies` |
`MutableSequence[`
Output only. Only applicable for Vertex AI Feature Store (Legacy). The list of historical stats and anomalies with specified objectives. |
`version_column_name` |
`str`
Only applicable for Vertex AI Feature Store. The name of the BigQuery Table/View column hosting data for this version. If no value is provided, will use feature_id. |
`point_of_contact` |
`str`
Entity responsible for maintaining this feature. Can be comma separated list of email addresses or URIs. |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

### MonitoringStatsAnomaly

`MonitoringStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of historical SnapshotAnalysis or ImportFeaturesAnalysis stats requested by user, sorted by FeatureStatsAnomaly.start_time descending.

### ValueType

`ValueType(value)`


Only applicable for Vertex AI Legacy Feature Store. An enum representing the value type of a feature.

## Methods

### Feature

`Feature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature Metadata information. For example, color is a feature that describes an apple.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistindexendpointsrequest__googlecloudaiplatform_v_c71c4e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistindexendpointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsRequest -->

# Class ListIndexEndpointsRequest (1.134.0)

`ListIndexEndpointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.ListIndexEndpoints.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the IndexEndpoints. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `index_endpoint` supports = and !=. `index_endpoint`
represents the IndexEndpoint ID, ie. the last segment of
the IndexEndpoint's
resourcename.
- `display_name` supports =, != and regex() (uses
`re2 ` __
syntax)
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality
`labels.key:* or labels:key - key existence A key including a space must be quoted.` \ labels."a
key"\`.
Some examples:
- `index_endpoint="1"`
- `display_name="myDisplayName"`
- \`regex(display_name, "^A") -> The display name starts
with an A.
- `labels.myKey="myValue"`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListIndexEndpointsResponse.next_page_token of the previous IndexEndpointService.ListIndexEndpoints call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |

## Methods

### ListIndexEndpointsRequest

`ListIndexEndpointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.ListIndexEndpoints.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetragengineconfigrequest_googlecloudaiplatform_v1_dd4e9a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetragengineconfigrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetRagEngineConfigRequest -->

# Class GetRagEngineConfigRequest (1.134.0)

`GetRagEngineConfigRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagEngineConfig

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the RagEngineConfig resource. Format: `projects/{project}/locations/{location}/ragEngineConfig`
|

## Methods

### GetRagEngineConfigRequest

`GetRagEngineConfigRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.GetRagEngineConfig


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetmodelmonitorrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelMonitorRequest -->

# Class GetModelMonitorRequest (1.134.0)

`GetModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.GetModelMonitor.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ModelMonitor resource. Format: `projects/{project}/locations/{location}/modelMonitors/{model_monitor}`
|

## Methods

### GetModelMonitorRequest

`GetModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.GetModelMonitor.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typespairwisemetricresult_googlecloudaiplatform__109cb1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespairwisemetricresult_googlecloudaiplatform_v_6c417a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespairwisemetricresult_googlecloudaiplatform_v1_c14ffa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespairwisemetricresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricResult -->

# Class PairwiseMetricResult (1.134.0)

`PairwiseMetricResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pairwise metric result.

## Attributes |
|
|---|---|
Name |
Description |
`pairwise_choice` |
Output only. Pairwise metric choice. |
`explanation` |
`str`
Output only. Explanation for pairwise metric score. |
`custom_output` |
Output only. Spec for custom output. |

## Methods

### PairwiseMetricResult

`PairwiseMetricResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pairwise metric result.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesundeployindexoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployIndexOperationMetadata -->

# Class UndeployIndexOperationMetadata (1.134.0)

```
UndeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.UndeployIndex.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UndeployIndexOperationMetadata

```
UndeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.UndeployIndex.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringschemafieldschema_googleclouda_d60c28.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringschemafieldschema.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringSchema.FieldSchema -->

# Class FieldSchema (1.134.0)

`FieldSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schema field definition.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Field name. |
`data_type` |
`str`
Supported data types are: `float` `integer` `boolean`
`string` `categorical`
|
`repeated` |
`bool`
Describes if the schema field is an array of given data type. |

## Methods

### FieldSchema

`FieldSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schema field definition.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitormodelmonitoringtargetvertexmodelsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitor.ModelMonitoringTarget.VertexModelSource -->

# Class VertexModelSource (1.134.0)

`VertexModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model in Vertex AI Model Registry.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Model resource name. Format: projects/{project}/locations/{location}/models/{model}. |
`model_version_id` |
`str`
Model version id. |

## Methods

### VertexModelSource

`VertexModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model in Vertex AI Model Registry.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesexportdatarequest_googlecloudaiplatform_v1typesfi_5f5c54.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexportdatarequest_googlecloudaiplatform_v1typesfin_c5d0cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportDataRequest -->

# Class ExportDataRequest (1.134.0)

`ExportDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ExportData.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Dataset resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`export_config` |
Required. The desired output location. |

## Methods

### ExportDataRequest

`ExportDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ExportData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfindneighborsrequestqueryrrf.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsRequest.Query.RRF -->

# Class RRF (1.134.0)

`RRF(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for RRF algorithm that combines search results.

## Attribute |
|
|---|---|
Name |
Description |
`alpha` |
`float`
Required. Users can provide an alpha value to give more weight to dense vs sparse results. For example, if the alpha is 0, we only return sparse and if the alpha is 1, we only return dense. |

## Methods

### RRF

`RRF(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for RRF algorithm that combines search results.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgettensorboardrequest_googlecloudaiplatform_v_c3c20a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgettensorboardrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardRequest -->

# Class GetTensorboardRequest (1.134.0)

`GetTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.GetTensorboard.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Tensorboard resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|

## Methods

### GetTensorboardRequest

`GetTensorboardRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.GetTensorboard.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatefeatureviewoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureViewOperationMetadata -->

# Class UpdateFeatureViewOperationMetadata (1.134.0)

```
UpdateFeatureViewOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update FeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for FeatureView Update. |

## Methods

### UpdateFeatureViewOperationMetadata

```
UpdateFeatureViewOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update FeatureView.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesragmanageddbconfigscaled_googlecloudaipla_cdcc48.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesragmanageddbconfigscaled_googlecloudaiplat_24abc4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesragmanageddbconfigscaled_googlecloudaiplatf_96bb92.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragmanageddbconfigscaled_googlecloudaiplatfo_4c3a34.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragmanageddbconfigscaled_googlecloudaiplatfor_619b1d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragmanageddbconfigscaled.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagManagedDbConfig.Scaled -->

# Class Scaled (1.134.0)

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

## Methods

### Scaled

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessupervisedhyperparametersadaptersize.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SupervisedHyperParameters.AdapterSize -->

# Class AdapterSize (1.134.0)

`AdapterSize(value)`


Supported adapter sizes for tuning.

## Enums |
|
|---|---|
Name |
Description |
`ADAPTER_SIZE_UNSPECIFIED` |
Adapter size is unspecified. |
`ADAPTER_SIZE_ONE` |
Adapter size 1. |
`ADAPTER_SIZE_TWO` |
Adapter size 2. |
`ADAPTER_SIZE_FOUR` |
Adapter size 4. |
`ADAPTER_SIZE_EIGHT` |
Adapter size 8. |
`ADAPTER_SIZE_SIXTEEN` |
Adapter size 16. |
`ADAPTER_SIZE_THIRTY_TWO` |
Adapter size 32. |

## Methods

### AdapterSize

`AdapterSize(value)`


Supported adapter sizes for tuning.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetfeatureonlinestorerequest_googlecloudaiplatform_3dffd5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetfeatureonlinestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureOnlineStoreRequest -->

# Class GetFeatureOnlineStoreRequest (1.134.0)

```
GetFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.GetFeatureOnlineStore.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureOnlineStore resource. |

## Methods

### GetFeatureOnlineStoreRequest

```
GetFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.GetFeatureOnlineStore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdiskspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DiskSpec -->

# Class DiskSpec (1.134.0)

`DiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of disk options.

## Attributes |
|
|---|---|
Name |
Description |
`boot_disk_type` |
`str`
Type of the boot disk (default is "pd-ssd"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) or "pd-standard" (Persistent Disk Hard Disk Drive). |
`boot_disk_size_gb` |
`int`
Size in GB of the boot disk (default is 100GB). |

## Methods

### DiskSpec

`DiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of disk options.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslisthyperparametertuningjobsrequest_googlecloudaip_e45eed.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisthyperparametertuningjobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsRequest -->

# Class ListHyperparameterTuningJobsRequest (1.134.0)

```
ListHyperparameterTuningJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListHyperparameterTuningJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the HyperparameterTuningJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListHyperparameterTuningJobsResponse.next_page_token of the previous JobService.ListHyperparameterTuningJobs call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListHyperparameterTuningJobsRequest

```
ListHyperparameterTuningJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListHyperparameterTuningJobs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturegroupbigquery.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.BigQuery -->

# Class BigQuery (1.134.0)

`BigQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input source type for BigQuery Tables and Views.

## Attributes |
|
|---|---|
Name |
Description |
`big_query_source` |
Required. Immutable. The BigQuery source URI that points to either a BigQuery Table or View. |
`entity_id_columns` |
`MutableSequence[str]`
Optional. Columns to construct entity_id / row keys. If not provided defaults to `entity_id` .
|
`static_data_source` |
`bool`
Optional. Set if the data source is not a time-series. |
`time_series` |
Optional. If the source is a time-series source, this can be set to control how downstream sources (ex: FeatureView ) will treat time-series sources. If not set, will treat the source as a time-series source with `feature_timestamp` as
timestamp column and no scan boundary.
|
`dense` |
`bool`
Optional. If set, all feature values will be fetched from a single row per unique entityId including nulls. If not set, will collapse all rows for each unique entityId into a singe row with any non-null values if present, if no non-null values are present will sync null. ex: If source has schema `(entity_id, feature_timestamp, f0, f1)` and the following
rows: `(e1, 2020-01-01T10:00:00.123Z, 10, 15)`
`(e1, 2020-02-01T10:00:00.123Z, 20, null)` If dense is
set, `(e1, 20, null)` is synced to online stores. If dense
is not set, `(e1, 20, 15)` is synced to online stores.
|

## Classes

### TimeSeries

`TimeSeries(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### BigQuery

`BigQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input source type for BigQuery Tables and Views.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeslistdatasetsresponse_googlecloudaiplatform_v1bet_f2a8d5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistdatasetsresponse_googlecloudaiplatform_v1beta_733aa2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistdatasetsresponse_googlecloudaiplatform_v1beta1_4be16f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistdatasetsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsResponse -->

# Class ListDatasetsResponse (1.134.0)

`ListDatasetsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListDatasets.

## Attributes |
|
|---|---|
Name |
Description |
`datasets` |
`MutableSequence[`
A list of Datasets that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListDatasetsResponse

`ListDatasetsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListDatasets.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatefeatureviewoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureViewOperationMetadata -->

# Class CreateFeatureViewOperationMetadata (1.134.0)

```
CreateFeatureViewOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create FeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for FeatureView Create. |

## Methods

### CreateFeatureViewOperationMetadata

```
CreateFeatureViewOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create FeatureView.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureviewbigtablemetadata_googlecloudaiplat_7bc228.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewbigtablemetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.BigtableMetadata -->

# Class BigtableMetadata (1.134.0)

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for the Cloud Bigtable that supports directly interacting Bigtable instances.

## Attribute |
|
|---|---|
Name |
Description |
`read_app_profile` |
`str`
The Bigtable App Profile to use for reading from Bigtable. |

## Methods

### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for the Cloud Bigtable that supports directly interacting Bigtable instances.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratememoriesresponsegeneratedmemory.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesResponse.GeneratedMemory -->

# Class GeneratedMemory (1.134.0)

`GeneratedMemory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A memory generated by the operation.

## Attributes |
|
|---|---|
Name |
Description |
`memory` |
The generated Memory. |
`action` |
The action that was performed on the Memory. |

## Classes

### Action

`Action(value)`


Actions that can be performed on a Memory.

## Methods

### GeneratedMemory

`GeneratedMemory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A memory generated by the operation.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typestoolparameterkeymatchresults_googlecloudaipl_1e8d8e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestoolparameterkeymatchresults_googlecloudaipla_2da3d3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolparameterkeymatchresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchResults -->

# Class ToolParameterKeyMatchResults (1.134.0)

```
ToolParameterKeyMatchResults(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Results for tool parameter key match metric.

## Attribute |
|
|---|---|
Name |
Description |
`tool_parameter_key_match_metric_values` |
`MutableSequence[`
Output only. Tool parameter key match metric values. |

## Methods

### ToolParameterKeyMatchResults

```
ToolParameterKeyMatchResults(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Results for tool parameter key match metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchmigrateresourcesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchMigrateResourcesResponse -->

# Class BatchMigrateResourcesResponse (1.134.0)

```
BatchMigrateResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MigrationService.BatchMigrateResources.

## Attribute |
|
|---|---|
Name |
Description |
`migrate_resource_responses` |
`MutableSequence[`
Successfully migrated resources. |

## Methods

### BatchMigrateResourcesResponse

```
BatchMigrateResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for MigrationService.BatchMigrateResources.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeaturevaluesrequestselecttimerangeandfeature.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesRequest.SelectTimeRangeAndFeature -->

# Class SelectTimeRangeAndFeature (1.134.0)

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select time range and feature. Values of the selected feature generated within an inclusive time range will be deleted. Using this option permanently deletes the feature values from the specified feature IDs within the specified time range. This might include data from the online storage. If you want to retain any deleted historical data in the online storage, you must re-ingest it.

## Attributes |
|
|---|---|
Name |
Description |
`time_range` |
`google.type.interval_pb2.Interval`
Required. Select feature generated within a half-inclusive time range. The time range is lower inclusive and upper exclusive. |
`feature_selector` |
Required. Selectors choosing which feature values to be deleted from the EntityType. |
`skip_online_storage_delete` |
`bool`
If set, data will not be deleted from online storage. When time range is older than the data in online storage, setting this to be true will make the deletion have no impact on online serving. |

## Methods

### SelectTimeRangeAndFeature

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select time range and feature. Values of the selected feature generated within an inclusive time range will be deleted. Using this option permanently deletes the feature values from the specified feature IDs within the specified time range. This might include data from the online storage. If you want to retain any deleted historical data in the online storage, you must re-ingest it.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslisthyperparametertuningjobsrequest_googlec_c681c5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslisthyperparametertuningjobsrequest_googlecl_b068a1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslisthyperparametertuningjobsrequest_googleclo_c3f7e5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisthyperparametertuningjobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsRequest -->

# Class ListHyperparameterTuningJobsRequest (1.134.0)

```
ListHyperparameterTuningJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListHyperparameterTuningJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the HyperparameterTuningJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListHyperparameterTuningJobsResponse.next_page_token of the previous JobService.ListHyperparameterTuningJobs call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListHyperparameterTuningJobsRequest

```
ListHyperparameterTuningJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListHyperparameterTuningJobs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistbatchpredictionjobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsRequest -->

# Class ListBatchPredictionJobsRequest (1.134.0)

```
ListBatchPredictionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListBatchPredictionJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the BatchPredictionJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `model_display_name` supports `=` , `!=` comparisons.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListBatchPredictionJobsResponse.next_page_token of the previous JobService.ListBatchPredictionJobs call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListBatchPredictionJobsRequest

```
ListBatchPredictionJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListBatchPredictionJobs.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgetexamplestorerequest_googlecloudaiplatform_d36e71.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetexamplestorerequest_googlecloudaiplatform__4aee0b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetexamplestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExampleStoreRequest -->

# Class GetExampleStoreRequest (1.134.0)

`GetExampleStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.GetExampleStore.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ExampleStore. Format: `projects/{project}/locations/{location}/exampleStores/{example_store}`
|

## Methods

### GetExampleStoreRequest

`GetExampleStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.GetExampleStore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmeasurementmetric.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Measurement.Metric -->

# Class Metric (1.134.0)

`Metric(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a metric in the measurement.

## Attributes |
|
|---|---|
Name |
Description |
`metric_id` |
`str`
Output only. The ID of the Metric. The Metric should be defined in [StudySpec's Metrics][google.cloud.aiplatform.v1beta1.StudySpec.metrics]. |
`value` |
`float`
Output only. The value for this metric. |

## Methods

### Metric

`Metric(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a metric in the measurement.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesundeployindexoperationmetadata_googlecloudaip_0fe01a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesundeployindexoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployIndexOperationMetadata -->

# Class UndeployIndexOperationMetadata (1.134.0)

```
UndeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.UndeployIndex.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UndeployIndexOperationMetadata

```
UndeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.UndeployIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesprediction_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service -->

# Package prediction_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.prediction_service`

package.

## Classes

[PredictionServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceAsyncClient)

A service for online predictions and explanations.

[PredictionServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.prediction_service.PredictionServiceClient)

A service for online predictions and explanations.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesupdatefeaturestoreoperationmetadata_googlec_4047c6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdatefeaturestoreoperationmetadata_googlecl_4f8b7a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatefeaturestoreoperationmetadata_googleclo_27dc66.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatefeaturestoreoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeaturestoreOperationMetadata -->

# Class UpdateFeaturestoreOperationMetadata (1.134.0)

```
UpdateFeaturestoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Featurestore.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore. |

## Methods

### UpdateFeaturestoreOperationMetadata

```
UpdateFeaturestoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Featurestore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreateindexrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexRequest -->

# Class CreateIndexRequest (1.134.0)

`CreateIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.CreateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the Index in. Format: `projects/{project}/locations/{location}`
|
`index` |
Required. The Index to create. |

## Methods

### CreateIndexRequest

`CreateIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.CreateIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimagesegmentationinputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs -->

# Class AutoMlImageSegmentationInputs (1.134.0)

```
AutoMlImageSegmentationInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`budget_milli_node_hours` |
`int`
The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node_hour = actual_hour \*
number_of_nodes_involved. Or actaul_wall_clock_hours =
train_budget_milli_node_hours / (number_of_nodes_involved \*
1000) For modelType `cloud-high-accuracy-1` \ (default),
the budget must be between 20,000 and 2,000,000 milli node
hours, inclusive. The default value is 192,000 which
represents one day in wall time (1000 milli \* 24 hours \* 8
nodes).
|
`base_model_id` |
`str`
The ID of the `base` model. If it is specified, the new
model will be trained based on the `base` model.
Otherwise, the new model will be trained from scratch. The
`base` model must be in the same Project and Location as
the new Model to train, and have the same modelType.
|

## Classes

### ModelType

`ModelType(value)`


## Methods

### AutoMlImageSegmentationInputs

```
AutoMlImageSegmentationInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageSegmentationInputs

```
AutoMlImageSegmentationInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesstreamdirectpredictresponse_googlecloudaiplatform_f397cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstreamdirectpredictresponse_googlecloudaiplatform__498448.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstreamdirectpredictresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamDirectPredictResponse -->

# Class StreamDirectPredictResponse (1.134.0)

`StreamDirectPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamDirectPredict.

## Attributes |
|
|---|---|
Name |
Description |
`outputs` |
`MutableSequence[`
The prediction output. |
`parameters` |
The parameters that govern the prediction. |

## Methods

### StreamDirectPredictResponse

`StreamDirectPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamDirectPredict.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigratableresourceautomlmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigratableResource.AutomlModel -->

# Class AutomlModel (1.134.0)

`AutomlModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Model in automl.googleapis.com.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Full resource name of automl Model. Format: `projects/{project}/locations/{location}/models/{model}` .
|
`model_display_name` |
`str`
The Model's display name in automl.googleapis.com. |

## Methods

### AutomlModel

`AutomlModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one Model in automl.googleapis.com.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmetricxspecmetricxversion_googlecloudaiplatfo_285690.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmetricxspecmetricxversion.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxSpec.MetricxVersion -->

# Class MetricxVersion (1.134.0)

`MetricxVersion(value)`


MetricX Version options.

## Enums |
|
|---|---|
Name |
Description |
`METRICX_VERSION_UNSPECIFIED` |
MetricX version unspecified. |
`METRICX_24_REF` |
MetricX 2024 (2.6) for translation + reference (reference-based). |
`METRICX_24_SRC` |
MetricX 2024 (2.6) for translation + source (QE). |
`METRICX_24_SRC_REF` |
MetricX 2024 (2.6) for translation + source + reference (source-reference-combined). |

## Methods

### MetricxVersion

`MetricxVersion(value)`


MetricX Version options.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratememoriesoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesOperationMetadata -->

# Class GenerateMemoriesOperationMetadata (1.134.0)

```
GenerateMemoriesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.GenerateMemories operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### GenerateMemoriesOperationMetadata

```
GenerateMemoriesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.GenerateMemories operation.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesfeature_online_store_servicefeatureonlinestore_6b23c5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_online_store_servicefeatureonlinestores_c98a2c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_online_store_servicefeatureonlinestoreserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient -->

# Class FeatureOnlineStoreServiceAsyncClient (1.134.0)

```
FeatureOnlineStoreServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for fetching feature values from the online store.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`FeatureOnlineStoreServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### FeatureOnlineStoreServiceAsyncClient

```
FeatureOnlineStoreServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the feature online store service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,FeatureOnlineStoreServiceTransport,Callable[..., FeatureOnlineStoreServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeatureOnlineStoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTlsChannelError` |
If mutual TLS transport creation failed for any reason. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### feature_view_direct_write

```
feature_view_direct_write(
requests: typing.Optional[
typing.AsyncIterator[
google.cloud.aiplatform_v1.types.feature_online_store_service.FeatureViewDirectWriteRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Awaitable[
typing.AsyncIterable[
google.cloud.aiplatform_v1.types.feature_online_store_service.FeatureViewDirectWriteResponse
]
]
```


Bidirectional streaming RPC to directly write to feature values in a feature view. Requests may not have a one-to-one mapping to responses and responses may be returned out-of-order to reduce latency.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_feature_view_direct_write():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[FeatureViewDirectWriteRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewDirectWriteRequest.html)(
)
# This method expects an iterator which contains
# 'aiplatform_v1.FeatureViewDirectWriteRequest' objects
# Here we create a generator that yields a single `request` for
# demonstrative purposes.
requests = [request]
def request_generator():
for request in requests:
yield request
# Make the request
stream = await client.[feature_view_direct_write](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_feature_online_store_service_FeatureOnlineStoreServiceAsyncClient_feature_view_direct_write)(requests=request_generator())
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`AsyncIterator[`
The request object AsyncIterator. Request message for FeatureOnlineStoreService.FeatureViewDirectWrite. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`AsyncIterable[` |
Response message for FeatureOnlineStoreService.FeatureViewDirectWrite. |

### feature_view_path

```
feature_view_path(
project: str, location: str, feature_online_store: str, feature_view: str
) -> str
```


Returns a fully-qualified feature_view string.

### fetch_feature_values

```
fetch_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_service.FetchFeatureValuesRequest,
dict,
]
] = None,
*,
feature_view: typing.Optional[str] = None,
data_key: typing.Optional[
google.cloud.aiplatform_v1.types.feature_online_store_service.FeatureViewDataKey
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.feature_online_store_service.FetchFeatureValuesResponse
)
```


Fetch feature values under a FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_fetch_feature_values():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[FetchFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FetchFeatureValuesRequest.html)(
feature_view="feature_view_value",
)
# Make the request
response = await client.[fetch_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_feature_online_store_service_FeatureOnlineStoreServiceAsyncClient_fetch_feature_values)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned. |
`feature_view` |
Required. FeatureView resource format |
`data_key` |
Optional. The request key to fetch feature values for. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureOnlineStoreService.FetchFeatureValues |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`FeatureOnlineStoreServiceAsyncClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`FeatureOnlineStoreServiceAsyncClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`FeatureOnlineStoreServiceAsyncClient` |
The constructed client. |

### generate_fetch_access_token

```
generate_fetch_access_token(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_service.GenerateFetchAccessTokenRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.feature_online_store_service.GenerateFetchAccessTokenResponse
)
```


RPC to generate an access token for the given feature view. FeatureViews under the same FeatureOnlineStore share the same access token.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_generate_fetch_access_token():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GenerateFetchAccessTokenRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateFetchAccessTokenRequest.html)(
)
# Make the request
response = await client.[generate_fetch_access_token](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_feature_online_store_service_FeatureOnlineStoreServiceAsyncClient_generate_fetch_access_token)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeatureOnlineStoreService.GenerateFetchAccessToken. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureOnlineStoreService.GenerateFetchAccessToken. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.feature_online_store_service.transports.base.FeatureOnlineStoreServiceTransport
]
```


Returns an appropriate transport class.

Parameter |
|
|---|---|
Name |
Description |
`label` |
`typing.Optional[str]`
The name of the desired transport. If none is provided, then the first transport in the registry is used. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_feature_view_path

`parse_feature_view_path(path: str) -> typing.Dict[str, str]`


Parses a feature_view path into its component segments.

### search_nearest_entities

```
search_nearest_entities(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_service.SearchNearestEntitiesRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.feature_online_store_service.SearchNearestEntitiesResponse
)
```


Search the nearest entities under a FeatureView. Search only works for indexable feature view; if a feature view isn't indexable, returns Invalid argument response.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_search_nearest_entities():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html)()
# Initialize request argument(s)
query = aiplatform_v1.[NearestNeighborQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborQuery.html)()
query.entity_id = "entity_id_value"
request = aiplatform_v1.[SearchNearestEntitiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchNearestEntitiesRequest.html)(
feature_view="feature_view_value",
query=query,
)
# Make the request
response = await client.[search_nearest_entities](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient.html#google_cloud_aiplatform_v1_services_feature_online_store_service_FeatureOnlineStoreServiceAsyncClient_search_nearest_entities)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for FeatureOnlineStoreService.SearchNearestEntities. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for FeatureOnlineStoreService.SearchNearestEntities |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesdeletesessionrequest_googlecloudaiplatfor_b15062.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesdeletesessionrequest_googlecloudaiplatform_d293ca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesdeletesessionrequest_googlecloudaiplatform__584855.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdeletesessionrequest_googlecloudaiplatform_v_7f186e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeletesessionrequest_googlecloudaiplatform_v1_838687.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletesessionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSessionRequest -->

# Class DeleteSessionRequest (1.134.0)

`DeleteSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.DeleteSession.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the session. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}`
|

## Methods

### DeleteSessionRequest

`DeleteSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.DeleteSession.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchnearestentitiesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchNearestEntitiesResponse -->

# Class SearchNearestEntitiesResponse (1.134.0)

```
SearchNearestEntitiesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreService.SearchNearestEntities

## Attribute |
|
|---|---|
Name |
Description |
`nearest_neighbors` |
The nearest neighbors of the query entity. |

## Methods

### SearchNearestEntitiesResponse

```
SearchNearestEntitiesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreService.SearchNearestEntities


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetpipelinejobrequest_googlecloudaiplatform_v_5179d9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetpipelinejobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPipelineJobRequest -->

# Class GetPipelineJobRequest (1.134.0)

`GetPipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.GetPipelineJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PipelineJob resource. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipeline_job}`
|

## Methods

### GetPipelineJobRequest

`GetPipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.GetPipelineJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringnotificationspecnotificationchannelconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringNotificationSpec.NotificationChannelConfig -->

# Class NotificationChannelConfig (1.134.0)

`NotificationChannelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Google Cloud Notification Channel config.

## Attribute |
|
|---|---|
Name |
Description |
`notification_channel` |
`str`
Resource names of the NotificationChannels. Must be of the format `projects/`
|

## Methods

### NotificationChannelConfig

`NotificationChannelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Google Cloud Notification Channel config.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreateragcorpusoperationmetadata_googlecloudaipla_647338.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreateragcorpusoperationmetadata_googlecloudaiplat_92e6a9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateragcorpusoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateRagCorpusOperationMetadata -->

# Class CreateRagCorpusOperationMetadata (1.134.0)

```
CreateRagCorpusOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.CreateRagCorpus.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateRagCorpusOperationMetadata

```
CreateRagCorpusOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.CreateRagCorpus.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateragcorpusoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateRagCorpusOperationMetadata -->

# Class UpdateRagCorpusOperationMetadata (1.134.0)

```
UpdateRagCorpusOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.UpdateRagCorpus.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateRagCorpusOperationMetadata

```
UpdateRagCorpusOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.UpdateRagCorpus.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragfileparsingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagFileParsingConfig -->

# Class RagFileParsingConfig (1.134.0)

`RagFileParsingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the parsing config for RagFiles.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`layout_parser` |
The Layout Parser to use for RagFiles. This field is a member of `oneof` _ `parser` .
|
`llm_parser` |
The LLM Parser to use for RagFiles. This field is a member of `oneof` _ `parser` .
|

## Classes

### LayoutParser

`LayoutParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Document AI Layout Parser config.

### LlmParser

`LlmParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the advanced parsing for RagFiles.

## Methods

### RagFileParsingConfig

`RagFileParsingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the parsing config for RagFiles.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesbatchdeletepipelinejobsresponse_googlecloudaipla_6429e2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesbatchdeletepipelinejobsresponse_googlecloudaiplat_6c314c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbatchdeletepipelinejobsresponse_googlecloudaiplatf_d22965.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchdeletepipelinejobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchDeletePipelineJobsResponse -->

# Class BatchDeletePipelineJobsResponse (1.134.0)

```
BatchDeletePipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchDeletePipelineJobs.

## Attribute |
|
|---|---|
Name |
Description |
`pipeline_jobs` |
`MutableSequence[`
PipelineJobs deleted. |

## Methods

### BatchDeletePipelineJobsResponse

```
BatchDeletePipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchDeletePipelineJobs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoobjecttrackinginputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs -->

# Class AutoMlVideoObjectTrackingInputs (1.134.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletefeaturevaluesrequestselecttimerangeandfeature.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesRequest.SelectTimeRangeAndFeature -->

# Class SelectTimeRangeAndFeature (1.134.0)

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select time range and feature. Values of the selected feature generated within an inclusive time range will be deleted. Using this option permanently deletes the feature values from the specified feature IDs within the specified time range. This might include data from the online storage. If you want to retain any deleted historical data in the online storage, you must re-ingest it.

## Attributes |
|
|---|---|
Name |
Description |
`time_range` |
`google.type.interval_pb2.Interval`
Required. Select feature generated within a half-inclusive time range. The time range is lower inclusive and upper exclusive. |
`feature_selector` |
Required. Selectors choosing which feature values to be deleted from the EntityType. |
`skip_online_storage_delete` |
`bool`
If set, data will not be deleted from online storage. When time range is older than the data in online storage, setting this to be true will make the deletion have no impact on online serving. |

## Methods

### SelectTimeRangeAndFeature

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select time range and feature. Values of the selected feature generated within an inclusive time range will be deleted. Using this option permanently deletes the feature values from the specified feature IDs within the specified time range. This might include data from the online storage. If you want to retain any deleted historical data in the online storage, you must re-ingest it.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoactionrec_e4bf8f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoactionreco_1dc95e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoactionrecognitioninputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs -->

# Class AutoMlVideoActionRecognitionInputs (1.134.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatefeaturestoreoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeaturestoreOperationMetadata -->

# Class UpdateFeaturestoreOperationMetadata (1.134.0)

```
UpdateFeaturestoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Featurestore.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore. |

## Methods

### UpdateFeaturestoreOperationMetadata

```
UpdateFeaturestoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Featurestore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesautomaticresources.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AutomaticResources -->

# Class AutomaticResources (1.134.0)

`AutomaticResources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that to large degree are decided by Vertex AI, and require only a modest additional configuration. Each Model supporting these resources documents its specific guidelines.

## Attributes |
|
|---|---|
Name |
Description |
`min_replica_count` |
`int`
Immutable. The minimum number of replicas this DeployedModel will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas up to max_replica_count, and as traffic decreases, some of these extra replicas may be freed. If the requested value is too large, the deployment will error. |
`max_replica_count` |
`int`
Immutable. The maximum number of replicas this DeployedModel may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the DeployedModel increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, a no upper bound for scaling under heavy traffic will be assume, though Vertex AI may be unable to scale beyond certain replica number. |

## Methods

### AutomaticResources

`AutomaticResources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that to large degree are decided by Vertex AI, and require only a modest additional configuration. Each Model supporting these resources documents its specific guidelines.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesgetdatalabelingjobrequest_googlecloudaipla_cd087c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesgetdatalabelingjobrequest_googlecloudaiplat_85634a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgetdatalabelingjobrequest_googlecloudaiplatf_c0cd7f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetdatalabelingjobrequest_googlecloudaiplatfo_19faac.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetdatalabelingjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDataLabelingJobRequest -->

# Class GetDataLabelingJobRequest (1.134.0)

`GetDataLabelingJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetDataLabelingJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DataLabelingJob. Format: `projects/{project}/locations/{location}/dataLabelingJobs/{data_labeling_job}`
|

## Methods

### GetDataLabelingJobRequest

`GetDataLabelingJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetDataLabelingJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesqueryreasoningengineresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryReasoningEngineResponse -->

# Class QueryReasoningEngineResponse (1.134.0)

```
QueryReasoningEngineResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [ReasoningEngineExecutionService.Query][]

## Attribute |
|
|---|---|
Name |
Description |
`output` |
`google.protobuf.struct_pb2.Value`
Response provided by users in JSON object format. |

## Methods

### QueryReasoningEngineResponse

```
QueryReasoningEngineResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [ReasoningEngineExecutionService.Query][]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistindexendpointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsRequest -->

# Class ListIndexEndpointsRequest (1.134.0)

`ListIndexEndpointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.ListIndexEndpoints.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the IndexEndpoints. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `index_endpoint` supports = and !=. `index_endpoint`
represents the IndexEndpoint ID, ie. the last segment of
the IndexEndpoint's
resourcename.
- `display_name` supports =, != and regex() (uses
`re2 ` __
syntax)
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality
`labels.key:* or labels:key - key existence A key including a space must be quoted.` \ labels."a
key"\`.
Some examples:
- `index_endpoint="1"`
- `display_name="myDisplayName"`
- \`regex(display_name, "^A") -> The display name starts
with an A.
- `labels.myKey="myValue"`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListIndexEndpointsResponse.next_page_token of the previous IndexEndpointService.ListIndexEndpoints call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |

## Methods

### ListIndexEndpointsRequest

`ListIndexEndpointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.ListIndexEndpoints.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgetexecutionrequest_googlecloudaiplatform_v1beta1_064e19.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetexecutionrequest_googlecloudaiplatform_v1beta1t_66336d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetExecutionRequest -->

# Class GetExecutionRequest (1.134.0)

`GetExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetExecution.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Execution to retrieve. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|

## Methods

### GetExecutionRequest

`GetExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetExecution.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadtensorboardblobdataresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardBlobDataResponse -->

# Class ReadTensorboardBlobDataResponse (1.134.0)

```
ReadTensorboardBlobDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ReadTensorboardBlobData.

## Attribute |
|
|---|---|
Name |
Description |
`blobs` |
`MutableSequence[`
Blob messages containing blob bytes. |

## Methods

### ReadTensorboardBlobDataResponse

```
ReadTensorboardBlobDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ReadTensorboardBlobData.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesclientconnectionconfig_googlecloudaiplatform_v1bet_88b4cb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesclientconnectionconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ClientConnectionConfig -->

# Class ClientConnectionConfig (1.134.0)

`ClientConnectionConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations (e.g. inference timeout) that are applied on your endpoints.

## Attribute |
|
|---|---|
Name |
Description |
`inference_timeout` |
`google.protobuf.duration_pb2.Duration`
Customizable online prediction request timeout. |

## Methods

### ClientConnectionConfig

`ClientConnectionConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations (e.g. inference timeout) that are applied on your endpoints.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfindneighborsrequestqueryrrf.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsRequest.Query.RRF -->

# Class RRF (1.134.0)

`RRF(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for RRF algorithm that combines search results.

## Attribute |
|
|---|---|
Name |
Description |
`alpha` |
`float`
Required. Users can provide an alpha value to give more weight to dense vs sparse results. For example, if the alpha is 0, we only return sparse and if the alpha is 1, we only return dense. |

## Methods

### RRF

`RRF(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for RRF algorithm that combines search results.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformprediction__googlecloudaiplatform_v1typesexportfeatureval_2bcb3b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformprediction__googlecloudaiplatform_v1typesexportfeaturevalu_24f437.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformprediction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction -->

# Package prediction (1.134.0)

API documentation for `aiplatform.prediction`

package.

## Classes

[DefaultSerializer](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.DefaultSerializer)

Default serializer for serialization and deserialization for prediction.

[Handler](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.Handler)

Interface for Handler class to handle prediction requests.

[LocalEndpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.LocalEndpoint)

Class that represents a local endpoint.

[LocalModel](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.LocalModel)

Class that represents a local model.

[PredictionHandler](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.PredictionHandler)

Default prediction handler for the prediction requests sent to the application.

[Predictor](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.Predictor)

Interface of the Predictor class for Custom Prediction Routines.

The Predictor is responsible for the ML logic for processing a prediction request. Specifically, the Predictor must define: (1) How to load all model artifacts used during prediction into memory. (2) The logic that should be executed at predict time.

When using the default `PredictionHandler`

, the `Predictor`

will be invoked as
follows:

```
predictor.postprocess(predictor.predict(predictor.preprocess(prediction_input)))
```


[Serializer](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.Serializer)

Interface to implement serialization and deserialization for prediction.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexportfeaturevaluesoperationmetadata_googlecloudai_9656bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportfeaturevaluesoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFeatureValuesOperationMetadata -->

# Class ExportFeatureValuesOperationMetadata (1.134.0)

```
ExportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that exports Features values.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore export Feature values. |

## Methods

### ExportFeatureValuesOperationMetadata

```
ExportFeatureValuesOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that exports Features values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateendpointoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointOperationMetadata -->

# Class UpdateEndpointOperationMetadata (1.134.0)

```
UpdateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UpdateEndpointLongRunning.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateEndpointOperationMetadata

```
UpdateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UpdateEndpointLongRunning.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesprobehttpheader_googlecloudaiplatform_v1beta_3ed99c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesprobehttpheader_googlecloudaiplatform_v1beta1_de2818.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesprobehttpheader.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Probe.HttpHeader -->

# Class HttpHeader (1.134.0)

`HttpHeader(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpHeader describes a custom header to be used in HTTP probes

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The header field name. This will be canonicalized upon output, so case-variant names will be understood as the same header. |
`value` |
`str`
The header field value |

## Methods

### HttpHeader

`HttpHeader(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpHeader describes a custom header to be used in HTTP probes


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesretrievememoriesresponseretrievedmemory.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesResponse.RetrievedMemory -->

# Class RetrievedMemory (1.134.0)

`RetrievedMemory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A retrieved memory.

## Attributes |
|
|---|---|
Name |
Description |
`memory` |
The retrieved Memory. |
`distance` |
`float`
The distance between the query and the retrieved Memory. Smaller values indicate more similar memories. This is only set if similarity search was used for retrieval. |

## Methods

### RetrievedMemory

`RetrievedMemory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A retrieved memory.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesclientconnectionconfig_googlecloudaiplatform__e2ab72.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesclientconnectionconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ClientConnectionConfig -->

# Class ClientConnectionConfig (1.134.0)

`ClientConnectionConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations (e.g. inference timeout) that are applied on your endpoints.

## Attribute |
|
|---|---|
Name |
Description |
`inference_timeout` |
`google.protobuf.duration_pb2.Duration`
Customizable online prediction request timeout. |

## Methods

### ClientConnectionConfig

`ClientConnectionConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations (e.g. inference timeout) that are applied on your endpoints.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetentitytyperequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetEntityTypeRequest -->

# Class GetEntityTypeRequest (1.134.0)

`GetEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetEntityType.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the EntityType resource. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
|

## Methods

### GetEntityTypeRequest

`GetEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetEntityType.


---

<!-- DOCUMENTO FUSIONADO: definition_v1beta1.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/definition_v1beta1 -->

# Types for Google Cloud Aiplatform V1beta1 Schema Trainingjob Definition v1beta1 API

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecasting(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Forecasting Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1beta1/types_.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs)

#### metadata()

The metadata information.

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_time_series_forecasting.AutoMlForecastingInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_time_series_forecasting.AutoMlForecastingMetadata](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingMetadata_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### target_column()

The name of the column that the model is to predict.

**Type**

#### time_series_identifier_column()

The name of the column that identifies the time series.

**Type**

#### time_column()

The name of the column that identifies time order in the time series.

**Type**

#### transformations()

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using “.” as the delimiter.

**Type**MutableSequence[

[google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1beta1/types_.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation)]

#### optimization_objective()

Objective function the model is optimizing towards. The training process creates a model that optimizes the value of the objective function over the validation set.

The supported optimization objectives:

“minimize-rmse” (default) - Minimize root-mean-squared error (RMSE).

“minimize-mae” - Minimize mean-absolute error (MAE).

“minimize-rmsle” - Minimize root-mean-squared log error (RMSLE).

“minimize-rmspe” - Minimize root-mean-squared percentage error (RMSPE).

“minimize-wape-mae” - Minimize the combination of weighted absolute percentage error (WAPE) and mean-absolute-error (MAE).

“minimize-quantile-loss” - Minimize the quantile loss at the quantiles defined in

`quantiles`

.**Type**

#### train_budget_milli_node_hours()

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend’s discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won’t be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

**Type**

#### weight_column()

Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1.

**Type**

#### time_series_attribute_columns()

Column names that should be used as attribute columns. The value of these columns does not vary as a function of time. For example, store ID or item color.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### unavailable_at_forecast_columns()

Names of columns that are unavailable when a forecast is requested. This column contains information for the given entity (identified by the time_series_identifier_column) that is unknown before the forecast For example, actual weather on a given day.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### available_at_forecast_columns()

Names of columns that are available and provided when a forecast is requested. These columns contain information for the given entity (identified by the time_series_identifier_column column) that is known at forecast. For example, predicted weather for a specific day.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### data_granularity()

Expected difference in time granularity between rows in the data.

#### forecast_horizon()

The amount of time into the future for which forecasted
values for the target are returned. Expressed in number of
units defined by the `data_granularity`

field.

**Type**

#### context_window()

The amount of time into the past training and prediction
data is used for model training and prediction respectively.
Expressed in number of units defined by the
`data_granularity`

field.

**Type**

#### export_evaluated_data_items_config()

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

#### quantiles()

Quantiles to use for minimize-quantile-loss
`optimization_objective`

. Up to 5 quantiles are allowed of
values between 0 and 1, exclusive. Required if the value of
optimization_objective is minimize-quantile-loss. Represents
the percent quantiles to use for that objective. Quantiles
must be unique.

**Type**MutableSequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### validation_options()

Validation options for the data validation component. The available options are:

“fail-pipeline” - default, will validate against the validation and fail the pipeline if it fails.

“ignore-validation” - ignore the results of the validation and continue

**Type**

#### additional_experiments()

Additional experiment flags for the time series forcasting training.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

*class* Granularity(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A duration of time expressed in time granularity units.

#### unit()

The time granularity unit of this time period. The supported units are:

“minute”

“hour”

“day”

“week”

“month”

“year”.

**Type**

#### quantity()

The number of granularity_units between data points in the
training data. If `granularity_unit`

is `minute`

, can be
1, 5, 10, 15, or 30. For all other values of
`granularity_unit`

, must be 1.

**Type**

#### quantity(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### unit(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### auto()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### numeric()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### categorical()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### timestamp()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### text()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

*class* AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will infer the proper transformation based on the statistic of dataset.

#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The categorical string as is–no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the “unknown” category. The “unknown” category gets its own special lookup index and resulting embedding.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The text as is–no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


#### column_name()

**Type**

#### time_format()

The format in which that time field is expressed. The time_format must either be one of:

`unix-seconds`

`unix-milliseconds`

`unix-microseconds`

`unix-nanoseconds`


(for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch);

or be written in `strftime`

syntax.

If time_format is not set, then the default format is RFC
3339 `date-time`

format, where `time-offset`

= `"Z"`

(e.g. 1985-04-12T23:20:50.52Z)

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_format(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### auto(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_time_series_forecasting.AutoMlForecastingInputs.Transformation.AutoTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.AutoTransformation_ )

#### categorical(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_time_series_forecasting.AutoMlForecastingInputs.Transformation.CategoricalTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.CategoricalTransformation_ )

#### numeric(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_time_series_forecasting.AutoMlForecastingInputs.Transformation.NumericTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.NumericTransformation_ )

#### text(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_time_series_forecasting.AutoMlForecastingInputs.Transformation.TextTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.TextTransformation_ )

#### timestamp(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_time_series_forecasting.AutoMlForecastingInputs.Transformation.TimestampTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.TimestampTransformation_ )

#### additional_experiments(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### available_at_forecast_columns(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### context_window(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### data_granularity(*: [Granularity](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Granularity_ )

#### export_evaluated_data_items_config(*: gcastd_export_evaluated_data_items_config.ExportEvaluatedDataItemsConfi* )

#### forecast_horizon(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### optimization_objective(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### quantiles(*: MutableSequence[*[float](https://docs.python.org/3/library/functions.html#float) )

[float](https://docs.python.org/3/library/functions.html#float)

#### target_column(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_column(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_series_attribute_columns(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_series_identifier_column(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### train_budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### transformations(*: MutableSequence[[Transformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation)_ )

#### unavailable_at_forecast_columns(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### validation_options(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### weight_column(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Model metadata specific to AutoML Forecasting.

#### train_cost_milli_node_hours()

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

**Type**

#### train_cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

#### inputs()

The input parameters of this TrainingJob.

#### metadata()

The metadata information.

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_image_classification.AutoMlImageClassificationInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_image_classification.AutoMlImageClassificationMetadata](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationMetadata_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

#### base_model_id()

The ID of the `base`

model. If it is specified, the new
model will be trained based on the `base`

model.
Otherwise, the new model will be trained from scratch. The
`base`

model must be in the same Project and Location as
the new Model to train, and have the same modelType.

**Type**

#### budget_milli_node_hours()

The training budget of creating this model, expressed in
milli node hours i.e. 1,000 value in this field means 1 node
hour. The actual metadata.costMilliNodeHours will be equal
or less than this value. If further model training ceases to
provide any improvements, it will stop without using the
full budget and the metadata.successfulStopReason will be
`model-converged`

. Note, node_hour = actual_hour *
number_of_nodes_involved. For modelType
`cloud`

(default), the budget must be between 8,000 and
800,000 milli node hours, inclusive. The default value is
192,000 which represents one day in wall time, considering 8
nodes are used. For model types `mobile-tf-low-latency-1`

,
`mobile-tf-versatile-1`

, `mobile-tf-high-accuracy-1`

,
the training budget must be between 1,000 and 100,000 milli
node hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.

**Type**

#### disable_early_stopping()

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Classification might stop training before the entire training budget has been used.

**Type**

#### multi_label()

If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each image just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each image multiple annotations may be applicable).

**Type**

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A Model best tailored to be used within
Google Cloud, and which cannot be exported.
Default.
MOBILE_TF_LOW_LATENCY_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow or Core
ML model and used on a mobile or edge device
afterwards. Expected to have low latency, but
may have lower prediction quality than other
mobile models.
MOBILE_TF_VERSATILE_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow or Core
ML model and used on a mobile or edge device
with afterwards.
MOBILE_TF_HIGH_ACCURACY_1 (4):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow or Core
ML model and used on a mobile or edge device
afterwards. Expected to have a higher latency,
but should also have a higher prediction quality
than other mobile models.
```


#### CLOUD(* = * )

#### MOBILE_TF_HIGH_ACCURACY_1(* = * )

#### MOBILE_TF_LOW_LATENCY_1(* = * )

#### MOBILE_TF_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### base_model_id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### disable_early_stopping(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### model_type(*: [ModelType](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationInputs.ModelType_ )

#### multi_label(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### cost_milli_node_hours()

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

**Type**

#### successful_stop_reason()

For successful job completions, this is the reason why the job has finished.

*class* SuccessfulStopReason(value)

Bases: `proto.enums.Enum`


Values:

```
SUCCESSFUL_STOP_REASON_UNSPECIFIED (0):
Should not be set.
BUDGET_REACHED (1):
The inputs.budgetMilliNodeHours had been
reached.
MODEL_CONVERGED (2):
Further training of the Model ceased to
increase its quality, since it already has
converged.
```


#### BUDGET_REACHED(* = * )

#### MODEL_CONVERGED(* = * )

#### SUCCESSFUL_STOP_REASON_UNSPECIFIED(* = * )

#### cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### successful_stop_reason(*: [SuccessfulStopReason](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationMetadata.SuccessfulStopReason_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetection(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

#### inputs()

The input parameters of this TrainingJob.

#### metadata()

The metadata information

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_image_object_detection.AutoMlImageObjectDetectionInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_image_object_detection.AutoMlImageObjectDetectionMetadata](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionMetadata_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

#### budget_milli_node_hours()

The training budget of creating this model, expressed in
milli node hours i.e. 1,000 value in this field means 1 node
hour. The actual metadata.costMilliNodeHours will be equal
or less than this value. If further model training ceases to
provide any improvements, it will stop without using the
full budget and the metadata.successfulStopReason will be
`model-converged`

. Note, node_hour = actual_hour *
number_of_nodes_involved. For modelType
`cloud`

(default), the budget must be between 20,000 and
900,000 milli node hours, inclusive. The default value is
216,000 which represents one day in wall time, considering 9
nodes are used. For model types `mobile-tf-low-latency-1`

,
`mobile-tf-versatile-1`

, `mobile-tf-high-accuracy-1`

the
training budget must be between 1,000 and 100,000 milli node
hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.

**Type**

#### disable_early_stopping()

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used.

**Type**

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD_HIGH_ACCURACY_1 (1):
A model best tailored to be used within
Google Cloud, and which cannot be exported.
Expected to have a higher latency, but should
also have a higher prediction quality than other
cloud models.
CLOUD_LOW_LATENCY_1 (2):
A model best tailored to be used within
Google Cloud, and which cannot be exported.
Expected to have a low latency, but may have
lower prediction quality than other cloud
models.
MOBILE_TF_LOW_LATENCY_1 (3):
A model that, in addition to being available
within Google Cloud can also be exported (see
ModelService.ExportModel) and used on a mobile
or edge device with TensorFlow afterwards.
Expected to have low latency, but may have lower
prediction quality than other mobile models.
MOBILE_TF_VERSATILE_1 (4):
A model that, in addition to being available
within Google Cloud can also be exported (see
ModelService.ExportModel) and used on a mobile
or edge device with TensorFlow afterwards.
MOBILE_TF_HIGH_ACCURACY_1 (5):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) and used on a mobile
or edge device with TensorFlow afterwards.
Expected to have a higher latency, but should
also have a higher prediction quality than other
mobile models.
```


#### CLOUD_HIGH_ACCURACY_1(* = * )

#### CLOUD_LOW_LATENCY_1(* = * )

#### MOBILE_TF_HIGH_ACCURACY_1(* = * )

#### MOBILE_TF_LOW_LATENCY_1(* = * )

#### MOBILE_TF_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### disable_early_stopping(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### model_type(*: [ModelType](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionInputs.ModelType_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### cost_milli_node_hours()

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

**Type**

#### successful_stop_reason()

For successful job completions, this is the reason why the job has finished.

*class* SuccessfulStopReason(value)

Bases: `proto.enums.Enum`


Values:

```
SUCCESSFUL_STOP_REASON_UNSPECIFIED (0):
Should not be set.
BUDGET_REACHED (1):
The inputs.budgetMilliNodeHours had been
reached.
MODEL_CONVERGED (2):
Further training of the Model ceased to
increase its quality, since it already has
converged.
```


#### BUDGET_REACHED(* = * )

#### MODEL_CONVERGED(* = * )

#### SUCCESSFUL_STOP_REASON_UNSPECIFIED(* = * )

#### cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### successful_stop_reason(*: [SuccessfulStopReason](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionMetadata.SuccessfulStopReason_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

#### inputs()

The input parameters of this TrainingJob.

#### metadata()

The metadata information.

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_image_segmentation.AutoMlImageSegmentationInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentationInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_image_segmentation.AutoMlImageSegmentationMetadata](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentationMetadata_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

#### budget_milli_node_hours()

The training budget of creating this model, expressed in
milli node hours i.e. 1,000 value in this field means 1 node
hour. The actual metadata.costMilliNodeHours will be equal
or less than this value. If further model training ceases to
provide any improvements, it will stop without using the
full budget and the metadata.successfulStopReason will be
`model-converged`

. Note, node_hour = actual_hour *
number_of_nodes_involved. Or actaul_wall_clock_hours =
train_budget_milli_node_hours / (number_of_nodes_involved *
1000) For modelType `cloud-high-accuracy-1`

(default),
the budget must be between 20,000 and 2,000,000 milli node
hours, inclusive. The default value is 192,000 which
represents one day in wall time (1000 milli * 24 hours * 8
nodes).

**Type**

#### base_model_id()

The ID of the `base`

model. If it is specified, the new
model will be trained based on the `base`

model.
Otherwise, the new model will be trained from scratch. The
`base`

model must be in the same Project and Location as
the new Model to train, and have the same modelType.

**Type**

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD_HIGH_ACCURACY_1 (1):
A model to be used via prediction calls to
uCAIP API. Expected to have a higher latency,
but should also have a higher prediction quality
than other models.
CLOUD_LOW_ACCURACY_1 (2):
A model to be used via prediction calls to
uCAIP API. Expected to have a lower latency but
relatively lower prediction quality.
MOBILE_TF_LOW_LATENCY_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow model
and used on a mobile or edge device afterwards.
Expected to have low latency, but may have lower
prediction quality than other mobile models.
```


#### CLOUD_HIGH_ACCURACY_1(* = * )

#### CLOUD_LOW_ACCURACY_1(* = * )

#### MOBILE_TF_LOW_LATENCY_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### base_model_id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### model_type(*: [ModelType](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentationInputs.ModelType_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### cost_milli_node_hours()

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

**Type**

#### successful_stop_reason()

For successful job completions, this is the reason why the job has finished.

*class* SuccessfulStopReason(value)

Bases: `proto.enums.Enum`


Values:

```
SUCCESSFUL_STOP_REASON_UNSPECIFIED (0):
Should not be set.
BUDGET_REACHED (1):
The inputs.budgetMilliNodeHours had been
reached.
MODEL_CONVERGED (2):
Further training of the Model ceased to
increase its quality, since it already has
converged.
```


#### BUDGET_REACHED(* = * )

#### MODEL_CONVERGED(* = * )

#### SUCCESSFUL_STOP_REASON_UNSPECIFIED(* = * )

#### cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### successful_stop_reason(*: [SuccessfulStopReason](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentationMetadata.SuccessfulStopReason_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Tables Model.

#### inputs()

The input parameters of this TrainingJob.

#### metadata()

The metadata information.

**Type**[google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesMetadata](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1beta1/types_.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesMetadata)

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesMetadata](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesMetadata_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### optimization_objective_recall_value()

Required when optimization_objective is “maximize-precision-at-recall”. Must be between 0 and 1, inclusive.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `additional_optimization_objective_config`

.

**Type**

#### optimization_objective_precision_value()

Required when optimization_objective is “maximize-recall-at-precision”. Must be between 0 and 1, inclusive.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `additional_optimization_objective_config`

.

**Type**

#### prediction_type()

The type of prediction the Model is to produce. “classification” - Predict one out of multiple target values is picked for each row.

“regression” - Predict a value based on its


relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings.

**Type**

#### target_column()

The column name of the target column that the model is to predict.

**Type**

#### transformations()

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using “.” as the delimiter.

**Type**MutableSequence[

[google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1beta1/types_.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation)]

#### optimization_objective()

Objective function the model is optimizing towards. The training process creates a model that maximizes/minimizes the value of the objective function over the validation set.

The supported optimization objectives depend on the prediction type. If the field is not set, a default objective function is used.

classification (binary):

“maximize-au-roc” (default) - Maximize the


area under the receiver operating characteristic (ROC) curve. “minimize-log-loss” - Minimize log loss.

“maximize-au-prc” - Maximize the area under


the precision-recall curve. “maximize-precision-at-recall” - Maximize precision for a specified recall value. “maximize-recall-at-precision” - Maximize recall for a specified precision value.

classification (multi-class):

“minimize-log-loss” (default) - Minimize log


loss.

regression:

“minimize-rmse” (default) - Minimize


root-mean-squared error (RMSE). “minimize-mae”

Minimize mean-absolute error (MAE). “minimize-rmsle” - Minimize root-mean-squared log error (RMSLE).

**Type**

#### train_budget_milli_node_hours()

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend’s discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won’t be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

**Type**

#### disable_early_stopping()

Use the entire training budget. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that AutoML Tables might stop training before the entire training budget has been used.

**Type**

#### weight_column_name()

Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1.

**Type**

#### export_evaluated_data_items_config()

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

#### additional_experiments()

Additional experiment flags for the Tables training pipeline.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

*class* Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### auto()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### numeric()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### categorical()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### timestamp()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### text()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### repeated_numeric()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### repeated_categorical()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### repeated_text()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

*class* AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will infer the proper transformation based on the statistic of dataset.

#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* CategoricalArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Treats the column as categorical array and performs following transformation functions.

For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.

Empty arrays treated as an embedding of zeroes.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The categorical string as is–no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the “unknown” category. The “unknown” category gets its own special lookup index and resulting embedding.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Treats the column as numerical array and performs following transformation functions.

All transformations for Numerical types applied to the average of the all elements.

The average of empty arrays is treated as zero.


#### column_name()

**Type**

#### invalid_values_allowed()

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### invalid_values_allowed(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


#### column_name()

**Type**

#### invalid_values_allowed()

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### invalid_values_allowed(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Treats the column as text array and performs following transformation functions.

Concatenate all text values in the array into a single text value using a space (” “) as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.

Empty arrays treated as an empty text.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The text as is–no change to case, punctuation, spelling, tense, and so on.

Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.

Tokenization is based on unicode script boundaries.

Missing values get their own lookup index and resulting embedding.

Stop-words receive no special treatment and are not removed.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the

timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


#### column_name()

**Type**

#### time_format()

The format in which that time field is expressed. The time_format must either be one of:

`unix-seconds`

`unix-milliseconds`

`unix-microseconds`

`unix-nanoseconds`

(for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch); or be written in`strftime`

syntax. If time_format is not set, then the default format is RFC 3339`date-time`

format, where`time-offset`

=`"Z"`

(e.g. 1985-04-12T23:20:50.52Z)**Type**

#### invalid_values_allowed()

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### invalid_values_allowed(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### time_format(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### auto(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesInputs.Transformation.AutoTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.AutoTransformation_ )

#### categorical(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesInputs.Transformation.CategoricalTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.CategoricalTransformation_ )

#### numeric(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesInputs.Transformation.NumericTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.NumericTransformation_ )

#### repeated_categorical(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation_ )

#### repeated_numeric(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesInputs.Transformation.NumericArrayTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.NumericArrayTransformation_ )

#### repeated_text(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesInputs.Transformation.TextArrayTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.TextArrayTransformation_ )

#### text(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesInputs.Transformation.TextTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.TextTransformation_ )

#### timestamp(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_tables.AutoMlTablesInputs.Transformation.TimestampTransformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.TimestampTransformation_ )

#### additional_experiments(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### disable_early_stopping(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### export_evaluated_data_items_config(*: gcastd_export_evaluated_data_items_config.ExportEvaluatedDataItemsConfi* )

#### optimization_objective(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### optimization_objective_precision_value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### optimization_objective_recall_value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### prediction_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### target_column(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### train_budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### transformations(*: MutableSequence[[Transformation](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation)_ )

#### weight_column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Model metadata specific to AutoML Tables.

#### train_cost_milli_node_hours()

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

**Type**

#### train_cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Text Classification Model.

#### inputs()

The input parameters of this TrainingJob.

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_text_classification.AutoMlTextClassificationInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextClassificationInputs_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextClassificationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### multi_label()

**Type**

#### multi_label(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs


#### inputs(*: google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_text_extraction.AutoMlTextExtractionInput* )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

#### inputs()

The input parameters of this TrainingJob.

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_text_sentiment.AutoMlTextSentimentInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextSentimentInputs_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextSentimentInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### sentiment_max()

A sentiment is expressed as an integer ordinal, where higher value means a more positive sentiment. The range of sentiments that will be used is between 0 and sentimentMax (inclusive on both ends), and all the values in the range must be represented in the dataset before a model can be created. Only the Annotations with this sentimentMax will be used for training. sentimentMax value must be between 1 and 10 (inclusive).

**Type**

#### sentiment_max(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognition(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

#### inputs()

The input parameters of this TrainingJob.

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_video_action_recognition.AutoMlVideoActionRecognitionInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognitionInputs_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognitionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A model best tailored to be used within
Google Cloud, and which c annot be exported.
Default.
MOBILE_VERSATILE_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a mobile or
edge device afterwards.
MOBILE_JETSON_VERSATILE_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) to a Jetson device
afterwards.
MOBILE_CORAL_VERSATILE_1 (4):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a Coral device
afterwards.
```


#### CLOUD(* = * )

#### MOBILE_CORAL_VERSATILE_1(* = * )

#### MOBILE_JETSON_VERSATILE_1(* = * )

#### MOBILE_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### model_type(*: [ModelType](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognitionInputs.ModelType_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Video Classification Model.

#### inputs()

The input parameters of this TrainingJob.

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_video_classification.AutoMlVideoClassificationInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoClassificationInputs_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoClassificationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A model best tailored to be used within
Google Cloud, and which cannot be exported.
Default.
MOBILE_VERSATILE_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a mobile or
edge device afterwards.
MOBILE_JETSON_VERSATILE_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) to a Jetson device
afterwards.
```


#### CLOUD(* = * )

#### MOBILE_JETSON_VERSATILE_1(* = * )

#### MOBILE_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### model_type(*: [ModelType](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoClassificationInputs.ModelType_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoObjectTracking(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.

#### inputs()

The input parameters of this TrainingJob.

#### inputs(*: [google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.automl_video_object_tracking.AutoMlVideoObjectTrackingInputs](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoObjectTrackingInputs_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoObjectTrackingInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A model best tailored to be used within
Google Cloud, and which c annot be exported.
Default.
MOBILE_VERSATILE_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a mobile or
edge device afterwards.
MOBILE_CORAL_VERSATILE_1 (3):
A versatile model that is meant to be
exported (see ModelService.ExportModel) and used
on a Google Coral device.
MOBILE_CORAL_LOW_LATENCY_1 (4):
A model that trades off quality for low
latency, to be exported (see
ModelService.ExportModel) and used on a Google
Coral device.
MOBILE_JETSON_VERSATILE_1 (5):
A versatile model that is meant to be
exported (see ModelService.ExportModel) and used
on an NVIDIA Jetson device.
MOBILE_JETSON_LOW_LATENCY_1 (6):
A model that trades off quality for low
latency, to be exported (see
ModelService.ExportModel) and used on an NVIDIA
Jetson device.
```


#### CLOUD(* = * )

#### MOBILE_CORAL_LOW_LATENCY_1(* = * )

#### MOBILE_CORAL_VERSATILE_1(* = * )

#### MOBILE_JETSON_LOW_LATENCY_1(* = * )

#### MOBILE_JETSON_VERSATILE_1(* = * )

#### MOBILE_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### model_type(*: [ModelType](../definition_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoObjectTrackingInputs.ModelType_ )

*class* google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.ExportEvaluatedDataItemsConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Configuration for exporting test set predictions to a BigQuery table.

#### destination_bigquery_uri()

URI of desired destination BigQuery table. Expected format: bq://<project_id>:<dataset_id>:

If not specified, then results are exported to the following auto-created BigQuery table: <project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd’T’HH_mm_ss_SSS’Z’>.evaluated_examples

**Type**

#### override_existing_table()

If true and an export destination is specified, then the contents of the destination are overwritten. Otherwise, if the export destination already exists, then the export operation fails.

**Type**

#### destination_bigquery_uri(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### override_existing_table(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)
