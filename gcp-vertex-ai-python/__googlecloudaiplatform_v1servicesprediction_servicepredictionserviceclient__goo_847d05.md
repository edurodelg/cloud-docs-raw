---
merged_at: 2026-01-25T21:47:44.345531
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesprediction_servicepredictionserviceclient__goog_14f49c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesprediction_servicepredictionserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient -->

# Class PredictionServiceClient (1.134.0)

```
PredictionServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### PredictionServiceClient

```
PredictionServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the prediction service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PredictionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_direct_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DirectPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DirectPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[direct_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_direct_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.DirectPredict. |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_direct_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DirectRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DirectRawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[direct_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_direct_raw_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.DirectRawPredict. |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_embed_content():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[EmbedContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EmbedContentRequest.html)(
)
# Make the request
response = client.[embed_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_embed_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.EmbedContent. |
`model` |
`str`
Required. The name of the publisher model requested to serve the prediction. Format: |
`content` |
Required. Input content to be embedded. Required. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_explain():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
instances = aiplatform_v1.Value()
instances.null_value = "NULL_VALUE"
request = aiplatform_v1.[ExplainRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplainRequest.html)(
endpoint="endpoint_value",
instances=instances,
)
# Make the request
response = client.[explain](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_explain)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.Explain. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the explanation. Format: |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the explanation call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the explanation call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri. This corresponds to the |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] parameters_schema_uri. This corresponds to the |
`deployed_model_id` |
`str`
If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding Endpoint.traffic_split. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
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
`PredictionServiceClient` |
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
`PredictionServiceClient` |
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
`PredictionServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_generate_content():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
contents = aiplatform_v1.[Content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Content.html)()
contents.parts.text = "text_value"
request = aiplatform_v1.[GenerateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentRequest.html)(
model="model_value",
contents=contents,
)
# Make the request
response = client.[generate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_generate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PredictionService.GenerateContent]. |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: |
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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


Deprecated. Return the API endpoint and client cert source for mutual TLS.

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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
instances = aiplatform_v1.Value()
instances.null_value = "NULL_VALUE"
request = aiplatform_v1.[PredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredictRequest.html)(
endpoint="endpoint_value",
instances=instances,
)
# Make the request
response = client.[predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.Predict. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri. This corresponds to the |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] parameters_schema_uri. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_raw_predict)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.RawPredict. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: |
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. A DeployedModel may have an upper limit on the number of instances it supports per request. When this limit it is exceeded for an AutoML model, the RawPredict method returns an error. When this limit is exceeded for a custom-trained model, the behavior varies depending on the model. You can specify the schema for each instance in the predict_schemata.instance_schema_uri field when you create a Model. This schema applies when you deploy the |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamingPredictResponse
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
def sample_server_streaming_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamingPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = client.[server_streaming_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_server_streaming_predict)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.StreamingPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
`retry` |
`google.api_core.retry.Retry`
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
`Iterable[` |
Response message for PredictionService.StreamingPredict. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
typing.Iterator[
google.cloud.aiplatform_v1.types.prediction_service.StreamDirectPredictRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamDirectPredictResponse
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
def sample_stream_direct_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
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
stream = client.[stream_direct_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_stream_direct_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamDirectPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
`retry` |
`google.api_core.retry.Retry`
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
`Iterable[` |
Response message for PredictionService.StreamDirectPredict. |

### stream_direct_raw_predict

```
stream_direct_raw_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1.types.prediction_service.StreamDirectRawPredictRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamDirectRawPredictResponse
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
def sample_stream_direct_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
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
stream = client.[stream_direct_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_stream_direct_raw_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamDirectRawPredict. The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect. |
`retry` |
`google.api_core.retry.Retry`
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
`Iterable[` |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1.types.prediction_service.GenerateContentResponse
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
def sample_stream_generate_content():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
contents = aiplatform_v1.[Content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Content.html)()
contents.parts.text = "text_value"
request = aiplatform_v1.[GenerateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentRequest.html)(
model="model_value",
contents=contents,
)
# Make the request
stream = client.[stream_generate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_stream_generate_content)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PredictionService.GenerateContent]. |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: |
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
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
`Iterable[` |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[google.api.httpbody_pb2.HttpBody]
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
def sample_stream_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamRawPredictRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamRawPredictRequest.html)(
endpoint="endpoint_value",
)
# Make the request
stream = client.[stream_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_stream_raw_predict)(request=request)
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PredictionService.StreamRawPredict. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: |
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
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
`Iterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

### streaming_predict

```
streaming_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1.types.prediction_service.StreamingPredictRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamingPredictResponse
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
def sample_streaming_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
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
stream = client.[streaming_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_streaming_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamingPredict. The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][]. |
`retry` |
`google.api_core.retry.Retry`
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
`Iterable[` |
Response message for PredictionService.StreamingPredict. |

### streaming_raw_predict

```
streaming_raw_predict(
requests: typing.Optional[
typing.Iterator[
google.cloud.aiplatform_v1.types.prediction_service.StreamingRawPredictRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1.types.prediction_service.StreamingRawPredictResponse
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
def sample_streaming_raw_predict():
# Create a client
client = aiplatform_v1.
```[PredictionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html)()
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
stream = client.[streaming_raw_predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.prediction_service.PredictionServiceClient.html#google_cloud_aiplatform_v1_services_prediction_service_PredictionServiceClient_streaming_raw_predict)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for PredictionService.StreamingRawPredict. The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect. |
`retry` |
`google.api_core.retry.Retry`
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
`Iterable[` |
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_online_store_servicefeatureonlinestores_f0be68.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_online_store_servicefeatureonlinestoreserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient -->

# Class FeatureOnlineStoreServiceClient (1.134.0)

```
FeatureOnlineStoreServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### FeatureOnlineStoreServiceClient

```
FeatureOnlineStoreServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the feature online store service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeatureOnlineStoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
typing.Iterator[
google.cloud.aiplatform_v1.types.feature_online_store_service.FeatureViewDirectWriteRequest
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1.types.feature_online_store_service.FeatureViewDirectWriteResponse
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
def sample_feature_view_direct_write():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
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
stream = client.[feature_view_direct_write](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_feature_view_direct_write)(requests=request_generator())
# Handle the response
for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`requests` |
`Iterator[`
The request object iterator. Request message for FeatureOnlineStoreService.FeatureViewDirectWrite. |
`retry` |
`google.api_core.retry.Retry`
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
`Iterable[` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_fetch_feature_values():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[FetchFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FetchFeatureValuesRequest.html)(
feature_view="feature_view_value",
)
# Make the request
response = client.[fetch_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_fetch_feature_values)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned. |
`feature_view` |
`str`
Required. FeatureView resource format |
`data_key` |
Optional. The request key to fetch feature values for. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
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
`FeatureOnlineStoreServiceClient` |
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
`FeatureOnlineStoreServiceClient` |
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
`FeatureOnlineStoreServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_generate_fetch_access_token():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GenerateFetchAccessTokenRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateFetchAccessTokenRequest.html)(
)
# Make the request
response = client.[generate_fetch_access_token](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_generate_fetch_access_token)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreService.GenerateFetchAccessToken. |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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


Deprecated. Return the API endpoint and client cert source for mutual TLS.

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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_search_nearest_entities():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html)()
# Initialize request argument(s)
query = aiplatform_v1.[NearestNeighborQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborQuery.html)()
query.entity_id = "entity_id_value"
request = aiplatform_v1.[SearchNearestEntitiesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchNearestEntitiesRequest.html)(
feature_view="feature_view_value",
query=query,
)
# Make the request
response = client.[search_nearest_entities](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_service.FeatureOnlineStoreServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_service_FeatureOnlineStoreServiceClient_search_nearest_entities)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for FeatureOnlineStoreService.SearchNearestEntities. |
`retry` |
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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
google.api_core.retry.retry_unary.Retry,
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
`google.api_core.retry.Retry`
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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesgetcontextrequest_googlecloudaiplatform_v_565474.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesgetcontextrequest_googlecloudaiplatform_v1_d9d19c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesgetcontextrequest_googlecloudaiplatform_v1t_2ee08a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgetcontextrequest_googlecloudaiplatform_v1ty_d8ad49.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetcontextrequest_googlecloudaiplatform_v1typ_2e7420.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetcontextrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetContextRequest -->

# Class GetContextRequest (1.134.0)

`GetContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetContext.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Context to retrieve. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|

## Methods

### GetContextRequest

`GetContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetContext.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolparameterkvmatchresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKVMatchResults -->

# Class ToolParameterKVMatchResults (1.134.0)

`ToolParameterKVMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool parameter key value match metric.

## Attribute |
|
|---|---|
Name |
Description |
`tool_parameter_kv_match_metric_values` |
`MutableSequence[`
Output only. Tool parameter key value match metric values. |

## Methods

### ToolParameterKVMatchResults

`ToolParameterKVMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool parameter key value match metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestunedmodelref.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TunedModelRef -->

# Class TunedModelRef (1.134.0)

`TunedModelRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModel Reference for legacy model migration.

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
`tuned_model` |
`str`
Support migration from model registry. This field is a member of `oneof` _ `tuned_model_ref` .
|
`tuning_job` |
`str`
Support migration from tuning job list page, from gemini-1.0-pro-002 to 1.5 and above. This field is a member of `oneof` _ `tuned_model_ref` .
|
`pipeline_job` |
`str`
Support migration from tuning job list page, from bison model to gemini model. This field is a member of `oneof` _ `tuned_model_ref` .
|

## Methods

### TunedModelRef

`TunedModelRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModel Reference for legacy model migration.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureviewdatakey__googlecloudaiplatform_v1b_cc21a6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewdatakey.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDataKey -->

# Class FeatureViewDataKey (1.134.0)

`FeatureViewDataKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Lookup key for a feature view.

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
`key` |
`str`
String key to use for lookup. This field is a member of `oneof` _ `key_oneof` .
|
`composite_key` |
The actual Entity ID will be composed from this struct. This should match with the way ID is defined in the FeatureView spec. This field is a member of `oneof` _ `key_oneof` .
|

## Classes

### CompositeKey

`CompositeKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ID that is comprised from several parts (columns).

## Methods

### FeatureViewDataKey

`FeatureViewDataKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Lookup key for a feature view.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestrajectoryexactmatchspec_googlecloudaiplatfor_bc2ab6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryexactmatchspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchSpec -->

# Class TrajectoryExactMatchSpec (1.134.0)

`TrajectoryExactMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryExactMatch metric - returns 1 if tool calls in the reference trajectory exactly match the predicted trajectory, else 0.

## Methods

### TrajectoryExactMatchSpec

`TrajectoryExactMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryExactMatch metric - returns 1 if tool calls in the reference trajectory exactly match the predicted trajectory, else 0.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewbigtablemetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.BigtableMetadata -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typestrajectoryexactmatchresults_googlecloudaipl_63ce55.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typestrajectoryexactmatchresults_googlecloudaipla_1a55e0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestrajectoryexactmatchresults_googlecloudaiplat_8d8d3b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryexactmatchresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchResults -->

# Class TrajectoryExactMatchResults (1.134.0)

`TrajectoryExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryExactMatch metric.

## Attribute |
|
|---|---|
Name |
Description |
`trajectory_exact_match_metric_values` |
`MutableSequence[`
Output only. TrajectoryExactMatch metric values. |

## Methods

### TrajectoryExactMatchResults

`TrajectoryExactMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for TrajectoryExactMatch metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrecommendspecresponserecommendationquotastate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecResponse.Recommendation.QuotaState -->

# Class QuotaState (1.134.0)

`QuotaState(value)`


The user accelerator quota state.

## Enums |
|
|---|---|
Name |
Description |
`QUOTA_STATE_UNSPECIFIED` |
Unspecified quota state. Quota information not available. |
`QUOTA_STATE_USER_HAS_QUOTA` |
User has enough accelerator quota for the machine type. |
`QUOTA_STATE_NO_USER_QUOTA` |
User does not have enough accelerator quota for the machine type. |

## Methods

### QuotaState

`QuotaState(value)`


The user accelerator quota state.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesaugmentpromptresponse_googlecloudaiplatform_v1type_0cec70.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesaugmentpromptresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AugmentPromptResponse -->

# Class AugmentPromptResponse (1.134.0)

`AugmentPromptResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for AugmentPrompt.

## Attributes |
|
|---|---|
Name |
Description |
`augmented_prompt` |
`MutableSequence[`
Augmented prompt, only text format is supported for now. |
`facts` |
`MutableSequence[`
Retrieved facts from RAG data sources. |

## Methods

### AugmentPromptResponse

`AugmentPromptResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for AugmentPrompt.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateentitytypeoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEntityTypeOperationMetadata -->

# Class CreateEntityTypeOperationMetadata (1.134.0)

```
CreateEntityTypeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create EntityType.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for EntityType. |

## Methods

### CreateEntityTypeOperationMetadata

```
CreateEntityTypeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create EntityType.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgroundingchunkmapsplaceanswersources_googleclouda_c1e563.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgroundingchunkmapsplaceanswersources_googlecloudai_178fe0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgroundingchunkmapsplaceanswersources.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingChunk.Maps.PlaceAnswerSources -->

# Class PlaceAnswerSources (1.134.0)

`PlaceAnswerSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attribute |
|
|---|---|
Name |
Description |
`review_snippets` |
`MutableSequence[`
Snippets of reviews that are used to generate the answer. |

## Classes

### ReviewSnippet

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.

## Methods

### PlaceAnswerSources

`PlaceAnswerSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgooglesearchretrieval.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GoogleSearchRetrieval -->

# Class GoogleSearchRetrieval (1.134.0)

`GoogleSearchRetrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public web data for grounding, powered by Google.

## Attribute |
|
|---|---|
Name |
Description |
`dynamic_retrieval_config` |
Specifies the dynamic retrieval configuration for the given source. |

## Methods

### GoogleSearchRetrieval

`GoogleSearchRetrieval(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to retrieve public web data for grounding, powered by Google.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnotebookruntimetype_googlecloudaiplatform_v1b_ee5854.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookruntimetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookRuntimeType -->

# Class NotebookRuntimeType (1.134.0)

`NotebookRuntimeType(value)`


Represents a notebook runtime type.

## Enums |
|
|---|---|
Name |
Description |
`NOTEBOOK_RUNTIME_TYPE_UNSPECIFIED` |
Unspecified notebook runtime type, NotebookRuntimeType will default to USER_DEFINED. |
`USER_DEFINED` |
runtime or template with coustomized configurations from user. |
`ONE_CLICK` |
runtime or template with system defined configurations. |

## Methods

### NotebookRuntimeType

`NotebookRuntimeType(value)`


Represents a notebook runtime type.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescancelcustomjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelCustomJobRequest -->

# Class CancelCustomJobRequest (1.134.0)

`CancelCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CancelCustomJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the CustomJob to cancel. Format: `projects/{project}/locations/{location}/customJobs/{custom_job}`
|

## Methods

### CancelCustomJobRequest

`CancelCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CancelCustomJob.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesdeletecustomjobrequest_googlecloudaiplatform_v1_b443ee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesdeletecustomjobrequest_googlecloudaiplatform_v1b_041ce0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdeletecustomjobrequest_googlecloudaiplatform_v1be_0966cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeletecustomjobrequest_googlecloudaiplatform_v1bet_45d003.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletecustomjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteCustomJobRequest -->

# Class DeleteCustomJobRequest (1.134.0)

`DeleteCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteCustomJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the CustomJob resource to be deleted. Format: `projects/{project}/locations/{location}/customJobs/{custom_job}`
|

## Methods

### DeleteCustomJobRequest

`DeleteCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteCustomJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodalitytokencount.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModalityTokenCount -->

# Class ModalityTokenCount (1.134.0)

`ModalityTokenCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents token counting info for a single modality.

## Attributes |
|
|---|---|
Name |
Description |
`modality` |
`google.cloud.aiplatform_v1beta1.types.Modality`
The modality associated with this token count. |
`token_count` |
`int`
Number of tokens. |

## Methods

### ModalityTokenCount

`ModalityTokenCount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents token counting info for a single modality.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgroundingchunkmapsplaceanswersourcesreviewsnippet__29bacf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgroundingchunkmapsplaceanswersourcesreviewsnippet.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingChunk.Maps.PlaceAnswerSources.ReviewSnippet -->

# Class ReviewSnippet (1.134.0)

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.

## Attributes |
|
|---|---|
Name |
Description |
`review_id` |
`str`
Id of the review referencing the place. |
`google_maps_uri` |
`str`
A link to show the review on Google Maps. |
`title` |
`str`
Title of the review. |

## Methods

### ReviewSnippet

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatememoryoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateMemoryOperationMetadata -->

# Class UpdateMemoryOperationMetadata (1.134.0)

```
UpdateMemoryOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.UpdateMemory operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UpdateMemoryOperationMetadata

```
UpdateMemoryOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of MemoryBankService.UpdateMemory operation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespersistentresource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PersistentResource -->

# Class PersistentResource (1.134.0)

`PersistentResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. Resource name of a PersistentResource. |
`display_name` |
`str`
Optional. The display name of the PersistentResource. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`resource_pools` |
`MutableSequence[`
Required. The spec of the pools of different resources. |
`state` |
Output only. The detailed state of a Study. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when persistent resource's state is `STOPPING` or `ERROR` .
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the PersistentResource was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the PersistentResource for the first time entered the `RUNNING` state.
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the PersistentResource was most recently updated. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize PersistentResource. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`network` |
`str`
Optional. The full name of the Compute Engine `network ` __
to peered with Vertex AI to host the persistent resources.
For example, `projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
To specify this field, you must have already `configured VPC
Network Peering for Vertex
AI |
`psc_interface_config` |
Optional. Configuration for PSC-I for PersistentResource. |
`encryption_spec` |
Optional. Customer-managed encryption key spec for a PersistentResource. If set, this PersistentResource and all sub-resources of this PersistentResource will be secured by this key. |
`resource_runtime_spec` |
Optional. Persistent Resource runtime spec. For example, used for Ray cluster configuration. |
`resource_runtime` |
Output only. Runtime information of the Persistent Resource. |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of names for the reserved IP ranges under the VPC network that can be used for this persistent resource. If set, we will deploy the persistent resource within the provided IP ranges. Otherwise, the persistent resource is deployed to any IP ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |

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

### State

`State(value)`


Describes the PersistentResource state.

## Methods

### PersistentResource

`PersistentResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistendpointsrequest_googlecloudaiplatformv1_353263.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistendpointsrequest_googlecloudaiplatformv1b_9cc7c5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistendpointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsRequest -->

# Class ListEndpointsRequest (1.134.0)

`ListEndpointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.ListEndpoints.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the Endpoints. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `endpoint` supports `=` and `!=` . `endpoint`
represents the Endpoint ID, i.e. the last segment of the
Endpoint's [resource
name][google.cloud.aiplatform.v1beta1.Endpoint.name].
- `display_name` supports `=` and `!=` .
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- `labels.key:*` or `labels:key` - key existence
- A key including a space must be quoted.
`labels."a key"` .
- `base_model_name` only supports `=` .
Some examples:
- `endpoint=1`
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
- `baseModelName="text-bison"`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListEndpointsResponse.next_page_token of the previous EndpointService.ListEndpoints call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |

## Methods

### ListEndpointsRequest

`ListEndpointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.ListEndpoints.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typesvideoactionrecognitionpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoActionRecognitionPredictionInstance -->

# Class VideoActionRecognitionPredictionInstance (1.134.0)

```
VideoActionRecognitionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Action Recognition.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The Google Cloud Storage location of the video on which to perform the prediction. |
`mime_type` |
`str`
The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime |
`time_segment_start` |
`str`
The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision. |
`time_segment_end` |
`str`
The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video. |

## Methods

### VideoActionRecognitionPredictionInstance

```
VideoActionRecognitionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Action Recognition.

### VideoActionRecognitionPredictionInstance

```
VideoActionRecognitionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Video Action Recognition.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesscheduling__googlecloudaiplatform_v1beta1type_9b4903.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesscheduling.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Scheduling -->

# Class Scheduling (1.134.0)

`Scheduling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


All parameters related to queuing and scheduling of custom jobs.

## Attributes |
|
|---|---|
Name |
Description |
`timeout` |
`google.protobuf.duration_pb2.Duration`
Optional. The maximum job running time. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Optional. Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`strategy` |
Optional. This determines which type of scheduling strategy to use. |
`disable_retries` |
`bool`
Optional. Indicates if the job should retry for internal errors after the job starts running. If true, overrides `Scheduling.restart_job_on_worker_restart` to false.
|
`max_wait_duration` |
`google.protobuf.duration_pb2.Duration`
Optional. This is the maximum duration that a job will wait for the requested resources to be provisioned if the scheduling strategy is set to [Strategy.DWS_FLEX_START]. If set to 0, the job will wait indefinitely. The default is 24 hours. |

## Classes

### Strategy

`Strategy(value)`


Optional. This determines which type of scheduling strategy to use. Right now users have two options such as STANDARD which will use regular on demand resources to schedule the job, the other is SPOT which would leverage spot resources alongwith regular resources to schedule the job.

## Methods

### Scheduling

`Scheduling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


All parameters related to queuing and scheduling of custom jobs.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeleteendpointrequest_googlecloudaiplatform_v_ade806.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeleteendpointrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEndpointRequest -->

# Class DeleteEndpointRequest (1.134.0)

`DeleteEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeleteEndpoint.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Endpoint resource to be deleted. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|

## Methods

### DeleteEndpointRequest

`DeleteEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeleteEndpoint.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeleteschedulerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteScheduleRequest -->

# Class DeleteScheduleRequest (1.134.0)

`DeleteScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.DeleteSchedule.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be deleted. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|

## Methods

### DeleteScheduleRequest

`DeleteScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.DeleteSchedule.


---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1typesgetpipelinejobrequest_googlecloudaiplatform__95e2f2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesgetpipelinejobrequest_googlecloudaiplatform_v_dd6f84.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesgetpipelinejobrequest_googlecloudaiplatform_v1_512515.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesgetpipelinejobrequest_googlecloudaiplatform_v1b_e7de8d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesgetpipelinejobrequest_googlecloudaiplatform_v1be_08dc5b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgetpipelinejobrequest_googlecloudaiplatform_v1bet_85be72.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetpipelinejobrequest_googlecloudaiplatform_v1beta_0579f7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetpipelinejobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPipelineJobRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesaugmentpromptresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptResponse -->

# Class AugmentPromptResponse (1.134.0)

`AugmentPromptResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for AugmentPrompt.

## Attributes |
|
|---|---|
Name |
Description |
`augmented_prompt` |
`MutableSequence[`
Augmented prompt, only text format is supported for now. |
`facts` |
`MutableSequence[`
Retrieved facts from RAG data sources. |

## Methods

### AugmentPromptResponse

`AugmentPromptResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for AugmentPrompt.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesevaluationconfig_googlecloudaiplatform_v1type_772558.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesevaluationconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluationConfig -->

# Class EvaluationConfig (1.134.0)

`EvaluationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation Config for Tuning Job.

## Attributes |
|
|---|---|
Name |
Description |
`metrics` |
`MutableSequence[`
Required. The metrics used for evaluation. |
`output_config` |
Required. Config for evaluation output. |
`autorater_config` |
Optional. Autorater config for evaluation. |

## Methods

### EvaluationConfig

`EvaluationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluation Config for Tuning Job.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeleteendpointrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEndpointRequest -->

# Class DeleteEndpointRequest (1.134.0)

`DeleteEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeleteEndpoint.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Endpoint resource to be deleted. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|

## Methods

### DeleteEndpointRequest

`DeleteEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.DeleteEndpoint.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigexplanationconfigex_cf00d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigexplanationconfigexp_731b76.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigexplanationconfigexplanationbaselinepredictionformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.ExplanationConfig.ExplanationBaseline.PredictionFormat -->

# Class PredictionFormat (1.134.0)

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.

## Enums |
|
|---|---|
Name |
Description |
`PREDICTION_FORMAT_UNSPECIFIED` |
Should not be set. |
`JSONL` |
Predictions are in JSONL files. |
`BIGQUERY` |
Predictions are in BigQuery. |

## Methods

### PredictionFormat

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatefeatureoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureOperationMetadata -->

# Class CreateFeatureOperationMetadata (1.134.0)

```
CreateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Feature.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Feature. |

## Methods

### CreateFeatureOperationMetadata

```
CreateFeatureOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Feature.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestunedmodelref.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModelRef -->

# Class TunedModelRef (1.134.0)

`TunedModelRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModel Reference for legacy model migration.

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
`tuned_model` |
`str`
Support migration from model registry. This field is a member of `oneof` _ `tuned_model_ref` .
|
`tuning_job` |
`str`
Support migration from tuning job list page, from gemini-1.0-pro-002 to 1.5 and above. This field is a member of `oneof` _ `tuned_model_ref` .
|
`pipeline_job` |
`str`
Support migration from tuning job list page, from bison model to gemini model. This field is a member of `oneof` _ `tuned_model_ref` .
|

## Methods

### TunedModelRef

`TunedModelRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModel Reference for legacy model migration.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeatureviewdirectwriterequestdatakeyandfeatu_17e819.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureviewdirectwriterequestdatakeyandfeatur_197899.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewdirectwriterequestdatakeyandfeaturevaluesfeature.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteRequest.DataKeyAndFeatureValues.Feature -->

# Class Feature (1.134.0)

`Feature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

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
`value` |
Feature value. A user provided timestamp may be set in the `FeatureValue.metadata.generate_time` field.
This field is a member of `oneof` _ `data_oneof` .
|
`value_and_timestamp` |
Feature value and timestamp. This field is a member of `oneof` _ `data_oneof` .
|
`name` |
`str`
Feature short name. |

## Classes

### FeatureValueAndTimestamp

`FeatureValueAndTimestamp(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature value and timestamp.

## Methods

### Feature

`Feature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewsync.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewSync -->

# Class FeatureViewSync (1.134.0)

`FeatureViewSync(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FeatureViewSync is a representation of sync operation which copies data from data source to Feature View in Online Store.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. Name of the FeatureViewSync. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}/featureViewSyncs/{feature_view_sync}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when this FeatureViewSync is created. Creation of a FeatureViewSync means that the job is pending / waiting for sufficient resources but may not have started the actual data transfer yet. |
`run_time` |
`google.type.interval_pb2.Interval`
Output only. Time when this FeatureViewSync is finished. |
`final_status` |
`google.rpc.status_pb2.Status`
Output only. Final status of the FeatureViewSync. |
`sync_summary` |
Output only. Summary of the sync job. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### SyncSummary

`SyncSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the Sync job. For continuous syncs, the summary is updated periodically. For batch syncs, it gets updated on completion of the sync.

## Methods

### FeatureViewSync

`FeatureViewSync(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FeatureViewSync is a representation of sync operation which copies data from data source to Feature View in Online Store.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespauseschedulerequest_googlecloudaiplatform_v1beta_85fa6b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespauseschedulerequest_googlecloudaiplatform_v1beta1_df2156.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespauseschedulerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PauseScheduleRequest -->

# Class PauseScheduleRequest (1.134.0)

`PauseScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.PauseSchedule.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be paused. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|

## Methods

### PauseScheduleRequest

`PauseScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.PauseSchedule.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgroundingchunkmapsplaceanswersources.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingChunk.Maps.PlaceAnswerSources -->

# Class PlaceAnswerSources (1.134.0)

`PlaceAnswerSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attribute |
|
|---|---|
Name |
Description |
`review_snippets` |
`MutableSequence[`
Snippets of reviews that are used to generate the answer. |

## Classes

### ReviewSnippet

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.

## Methods

### PlaceAnswerSources

`PlaceAnswerSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstreamingpredictresponse_googlecloudaiplatform_v1t_429d0c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstreamingpredictresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingPredictResponse -->

# Class StreamingPredictResponse (1.134.0)

`StreamingPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingPredict.

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

### StreamingPredictResponse

`StreamingPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingPredict.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatedatasetoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDatasetOperationMetadata -->

# Class CreateDatasetOperationMetadata (1.134.0)

```
CreateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.CreateDataset.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateDatasetOperationMetadata

```
CreateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.CreateDataset.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typessampleconfig_googlecloudaiplatform_v1beta1typesf_e4411b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typessampleconfig_googlecloudaiplatform_v1beta1typesfe_5ea2e9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessampleconfig_googlecloudaiplatform_v1beta1typesfet_b61bcd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessampleconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SampleConfig -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfetchexamplesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesRequest -->

# Class FetchExamplesRequest (1.134.0)

`FetchExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.FetchExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`stored_contents_example_filter` |
The metadata filters for StoredContentsExamples. This field is a member of `oneof` _ `metadata_filter` .
|
`example_store` |
`str`
Required. The name of the ExampleStore resource that the examples should be fetched from. Format: `projects/{project}/locations/{location}/exampleStores/{example_store}`
|
`page_size` |
`int`
Optional. The maximum number of examples to return. The service may return fewer than this value. If unspecified, at most 100 examples will be returned. |
`page_token` |
`str`
Optional. The next_page_token value returned from a previous list [ExampleStoreService.FetchExamplesResponse][] call. |
`example_ids` |
`MutableSequence[str]`
Optional. Example IDs to fetch. If both metadata filters and Example IDs are specified, then both ID and metadata filtering will be applied. |

## Methods

### FetchExamplesRequest

`FetchExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.FetchExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeploypublishermodelrequest__googlecloudaipla_73b21b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeploypublishermodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployPublisherModelRequest -->

# Class DeployPublisherModelRequest (1.134.0)

`DeployPublisherModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.DeployPublisherModel.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. The model to deploy. Format: 1. `publishers/{publisher}/models/{publisher_model}@{version_id}` ,
or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001` .
2. Hugging Face model ID like `google/gemma-2-2b-it` .
3. Custom model Google Cloud Storage URI like
`gs://bucket` .
4. Custom model zip file like `https://example.com/a.zip` .
|
`destination` |
`str`
Required. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`
|
`endpoint_display_name` |
`str`
Optional. The user-specified display name of the endpoint. If not set, a default name will be used. |
`dedicated_resources` |
Optional. The dedicated resources to use for the endpoint. If not set, the default resources will be used. |
`model_display_name` |
`str`
Optional. The user-specified display name of the uploaded model. If not set, a default name will be used. |
`hugging_face_access_token` |
`str`
Optional. The Hugging Face read access token used to access the model artifacts of gated models. |
`accept_eula` |
`bool`
Optional. Whether the user accepts the End User License Agreement (EULA) for the model. |

## Methods

### DeployPublisherModelRequest

`DeployPublisherModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.DeployPublisherModel.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatedatasetoperationmetadata_googlecloudaip_cd3b45.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatedatasetoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetOperationMetadata -->

# Class CreateDatasetOperationMetadata (1.134.0)

```
CreateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.CreateDataset.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateDatasetOperationMetadata

```
CreateDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.CreateDataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesaggregationoutput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AggregationOutput -->

# Class AggregationOutput (1.134.0)

`AggregationOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The aggregation result for the entire dataset and all metrics.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
The dataset used for evaluation & aggregation. |
`aggregation_results` |
`MutableSequence[`
One AggregationResult per metric. |

## Methods

### AggregationOutput

`AggregationOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The aggregation result for the entire dataset and all metrics.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesmeasurementmetric_googlecloudaiplatform_v1typesp_8a1878.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmeasurementmetric_googlecloudaiplatform_v1typespr_412436.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmeasurementmetric_googlecloudaiplatform_v1typespro_6fecab.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmeasurementmetric.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Measurement.Metric -->

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
Output only. The ID of the Metric. The Metric should be defined in [StudySpec's Metrics][google.cloud.aiplatform.v1.StudySpec.metrics]. |
`value` |
`float`
Output only. The value for this metric. |

## Methods

### Metric

`Metric(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a metric in the measurement.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesprobehttpheader.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Probe.HttpHeader -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgroundingchunkmapsplaceanswersourcesreviewsni_b586e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgroundingchunkmapsplaceanswersourcesreviewsnippet.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingChunk.Maps.PlaceAnswerSources.ReviewSnippet -->

# Class ReviewSnippet (1.134.0)

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.

## Attributes |
|
|---|---|
Name |
Description |
`review_id` |
`str`
Id of the review referencing the place. |
`google_maps_uri` |
`str`
A link to show the review on Google Maps. |
`title` |
`str`
Title of the review. |

## Methods

### ReviewSnippet

`ReviewSnippet(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Encapsulates a review snippet.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetdatasetrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetRequest -->

# Class GetDatasetRequest (1.134.0)

`GetDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDataset.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Dataset resource. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetDatasetRequest

`GetDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDataset.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdatasetstats__googlecloudaiplatform_v1beta1ty_42d0ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdatasetstats.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetStats -->

# Class DatasetStats (1.134.0)

`DatasetStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Statistics computed over a tuning dataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`tuning_dataset_example_count` |
`int`
Output only. Number of examples in the tuning dataset. |
`total_tuning_character_count` |
`int`
Output only. Number of tuning characters in the tuning dataset. |
`total_billable_character_count` |
`int`
Output only. Number of billable characters in the tuning dataset. |
`tuning_step_count` |
`int`
Output only. Number of tuning steps for this Tuning Job. |
`user_input_token_distribution` |
Output only. Dataset distributions for the user input tokens. |
`user_output_token_distribution` |
Output only. Dataset distributions for the user output tokens. This field is a member of `oneof` _ `_user_output_token_distribution` .
|
`user_message_per_example_distribution` |
Output only. Dataset distributions for the messages per example. |
`user_dataset_examples` |
`MutableSequence[`
Output only. Sample user messages in the training dataset uri. |

## Methods

### DatasetStats

`DatasetStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Statistics computed over a tuning dataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbatchdeletepipelinejobsresponse_googlecloudai_1095f7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchdeletepipelinejobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchDeletePipelineJobsResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmetricxspecmetricxversion.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetricxSpec.MetricxVersion -->

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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typescreatetensorboardoperationmetadata_googlecloud_d0945a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typescreatetensorboardoperationmetadata_googleclouda_8c7032.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescreatetensorboardoperationmetadata_googlecloudai_3998ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreatetensorboardoperationmetadata_googlecloudaip_212944.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatetensorboardoperationmetadata_googlecloudaipl_cea9f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatetensorboardoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardOperationMetadata -->

# Class CreateTensorboardOperationMetadata (1.134.0)

```
CreateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Tensorboard.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Tensorboard. |

## Methods

### CreateTensorboardOperationMetadata

```
CreateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Tensorboard.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesvideometadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VideoMetadata -->

# Class VideoMetadata (1.134.0)

`VideoMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describes the input video content.

## Attributes |
|
|---|---|
Name |
Description |
`start_offset` |
`google.protobuf.duration_pb2.Duration`
Optional. The start offset of the video. |
`end_offset` |
`google.protobuf.duration_pb2.Duration`
Optional. The end offset of the video. |

## Methods

### VideoMetadata

`VideoMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describes the input video content.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstreamingpredictresponse_googlecloudaiplatfor_9e48a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstreamingpredictresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingPredictResponse -->

# Class StreamingPredictResponse (1.134.0)

`StreamingPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingPredict.

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

### StreamingPredictResponse

`StreamingPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.StreamingPredict.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgettensorboardrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureviewsync__googlecloudaiplatform_v1type_485ec4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewsync.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewSync -->

# Class FeatureViewSync (1.134.0)

`FeatureViewSync(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FeatureViewSync is a representation of sync operation which copies data from data source to Feature View in Online Store.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. Name of the FeatureViewSync. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}/featureViewSyncs/{feature_view_sync}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when this FeatureViewSync is created. Creation of a FeatureViewSync means that the job is pending / waiting for sufficient resources but may not have started the actual data transfer yet. |
`run_time` |
`google.type.interval_pb2.Interval`
Output only. Time when this FeatureViewSync is finished. |
`final_status` |
`google.rpc.status_pb2.Status`
Output only. Final status of the FeatureViewSync. |
`sync_summary` |
Output only. Summary of the sync job. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### SyncSummary

`SyncSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the Sync job. For continuous syncs, the summary is updated periodically. For batch syncs, it gets updated on completion of the sync.

## Methods

### FeatureViewSync

`FeatureViewSync(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FeatureViewSync is a representation of sync operation which copies data from data source to Feature View in Online Store.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgeneratesyntheticdataresponse_googlecloudaiplatfor_4d19a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgeneratesyntheticdataresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateSyntheticDataResponse -->

# Class GenerateSyntheticDataResponse (1.134.0)

```
GenerateSyntheticDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The response containing the generated data.

## Attribute |
|
|---|---|
Name |
Description |
`synthetic_examples` |
`MutableSequence[`
A list of generated synthetic examples. |

## Methods

### GenerateSyntheticDataResponse

```
GenerateSyntheticDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The response containing the generated data.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigexplanationconfigexplanationbaselinepredictionformat.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.ExplanationConfig.ExplanationBaseline.PredictionFormat -->

# Class PredictionFormat (1.134.0)

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.

## Enums |
|
|---|---|
Name |
Description |
`PREDICTION_FORMAT_UNSPECIFIED` |
Should not be set. |
`JSONL` |
Predictions are in JSONL files. |
`BIGQUERY` |
Predictions are in BigQuery. |

## Methods

### PredictionFormat

`PredictionFormat(value)`


The storage format of the predictions generated BatchPrediction job.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typessummarizationverbosityinput_googlecloudaipl_46caf4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessummarizationverbosityinput_googlecloudaipla_0e1f38.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessummarizationverbosityinput_googlecloudaiplat_f599ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessummarizationverbosityinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationVerbosityInput -->

# Class SummarizationVerbosityInput (1.134.0)

`SummarizationVerbosityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization verbosity metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for summarization verbosity score metric. |
`instance` |
Required. Summarization verbosity instance. |

## Methods

### SummarizationVerbosityInput

`SummarizationVerbosityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization verbosity metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesundeploymodeloperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelOperationMetadata -->

# Class UndeployModelOperationMetadata (1.134.0)

```
UndeployModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UndeployModel.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UndeployModelOperationMetadata

```
UndeployModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UndeployModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesworkerpoolspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WorkerPoolSpec -->

# Class WorkerPoolSpec (1.134.0)

`WorkerPoolSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a worker pool in a job.

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
`container_spec` |
The custom container task. This field is a member of `oneof` _ `task` .
|
`python_package_spec` |
The Python packaged task. This field is a member of `oneof` _ `task` .
|
`machine_spec` |
Optional. Immutable. The specification of a single machine. |
`replica_count` |
`int`
Optional. The number of worker replicas to use for this worker pool. |
`nfs_mounts` |
`MutableSequence[`
Optional. List of NFS mount spec. |
`disk_spec` |
Disk spec. |

## Methods

### WorkerPoolSpec

`WorkerPoolSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a worker pool in a job.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgetsessionrequest_googlecloudaiplatform_v1be_f24045.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetsessionrequest_googlecloudaiplatform_v1bet_5a92ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetsessionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSessionRequest -->

# Class GetSessionRequest (1.134.0)

`GetSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.GetSession.

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

### GetSessionRequest

`GetSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.GetSession.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeployvertex.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.DeployVertex -->

# Class DeployVertex (1.134.0)

`DeployVertex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Multiple setups to deploy the PublisherModel.

## Attribute |
|
|---|---|
Name |
Description |
`multi_deploy_vertex` |
`MutableSequence[google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.Deploy]`
Optional. One click deployment configurations. |

## Methods

### DeployVertex

`DeployVertex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Multiple setups to deploy the PublisherModel.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbatchcancelpipelinejobsresponse_googlecloudaiplatf_745f7d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchcancelpipelinejobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCancelPipelineJobsResponse -->

# Class BatchCancelPipelineJobsResponse (1.134.0)

```
BatchCancelPipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchCancelPipelineJobs.

## Attribute |
|
|---|---|
Name |
Description |
`pipeline_jobs` |
`MutableSequence[`
PipelineJobs cancelled. |

## Methods

### BatchCancelPipelineJobsResponse

```
BatchCancelPipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchCancelPipelineJobs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspecalgorithm.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.Algorithm -->

# Class Algorithm (1.134.0)

`Algorithm(value)`


The available search algorithms for the Study.

## Enums |
|
|---|---|
Name |
Description |
`ALGORITHM_UNSPECIFIED` |
The default algorithm used by Vertex AI for `hyperparameter tuning |
`GRID_SEARCH` |
Simple grid search within the feasible space. To use grid search, all parameters must be `INTEGER`, `CATEGORICAL`, or `DISCRETE`. |
`RANDOM_SEARCH` |
Simple random search within the feasible space. |

## Methods

### Algorithm

`Algorithm(value)`


The available search algorithms for the Study.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesundeploymodeloperationmetadata_googlecloudaipla_536e82.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesundeploymodeloperationmetadata_googlecloudaiplat_9c73b5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesundeploymodeloperationmetadata_googlecloudaiplatf_e1557f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesundeploymodeloperationmetadata_googlecloudaiplatfo_caf48c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesundeploymodeloperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelOperationMetadata -->

# Class UndeployModelOperationMetadata (1.134.0)

```
UndeployModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UndeployModel.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UndeployModelOperationMetadata

```
UndeployModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.UndeployModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessummarizationverbosityinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationVerbosityInput -->

# Class SummarizationVerbosityInput (1.134.0)

`SummarizationVerbosityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization verbosity metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for summarization verbosity score metric. |
`instance` |
Required. Summarization verbosity instance. |

## Methods

### SummarizationVerbosityInput

`SummarizationVerbosityInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for summarization verbosity metric.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeletedatasetrequest_googlecloudaiplatform_v1types_b55fb7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletedatasetrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDatasetRequest -->

# Class DeleteDatasetRequest (1.134.0)

`DeleteDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDataset.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Dataset to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|

## Methods

### DeleteDatasetRequest

`DeleteDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgenerationconfigroutingconfigautoroutingmodemodelroutingpreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig.AutoRoutingMode.ModelRoutingPreference -->

# Class ModelRoutingPreference (1.134.0)

`ModelRoutingPreference(value)`


The model routing preference.

## Enums |
|
|---|---|
Name |
Description |
`UNKNOWN` |
Unspecified model routing preference. |
`PRIORITIZE_QUALITY` |
Prefer higher quality over low cost. |
`BALANCED` |
Balanced model routing preference. |
`PRIORITIZE_COST` |
Prefer lower cost over higher quality. |

## Methods

### ModelRoutingPreference

`ModelRoutingPreference(value)`


The model routing preference.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexplainresponse__googlecloudaiplatform_v1beta_6d0de0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplainresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplainResponse -->

# Class ExplainResponse (1.134.0)

`ExplainResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Explain.

## Attributes |
|
|---|---|
Name |
Description |
`explanations` |
`MutableSequence[`
The explanations of the Model's PredictResponse.predictions. It has the same number of elements as instances to be explained. |
`concurrent_explanations` |
`MutableMapping[str, `
This field stores the results of the explanations run in parallel with The default explanation strategy/method. |
`deployed_model_id` |
`str`
ID of the Endpoint's DeployedModel that served this explanation. |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
The predictions that are the output of the predictions call. Same as PredictResponse.predictions. |

## Classes

### ConcurrentExplanation

`ConcurrentExplanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message is a wrapper grouping Concurrent Explanations.

### ConcurrentExplanationsEntry

`ConcurrentExplanationsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

## Methods

### ExplainResponse

`ExplainResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Explain.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgenerationconfigroutingconfigautoroutingmodem_81e642.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgenerationconfigroutingconfigautoroutingmodemodelroutingpreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig.AutoRoutingMode.ModelRoutingPreference -->

# Class ModelRoutingPreference (1.134.0)

`ModelRoutingPreference(value)`


The model routing preference.

## Enums |
|
|---|---|
Name |
Description |
`UNKNOWN` |
Unspecified model routing preference. |
`PRIORITIZE_QUALITY` |
Prefer higher quality over low cost. |
`BALANCED` |
Balanced model routing preference. |
`PRIORITIZE_COST` |
Prefer lower cost over higher quality. |

## Methods

### ModelRoutingPreference

`ModelRoutingPreference(value)`


The model routing preference.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletedatasetrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetRequest -->

# Class DeleteDatasetRequest (1.134.0)

`DeleteDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDataset.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Dataset to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|

## Methods

### DeleteDatasetRequest

`DeleteDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDataset.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistschedulesrequest__googlecloudaiplatform_v1bet_1e7bff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistschedulesrequest__googlecloudaiplatform_v1beta_73af72.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistschedulesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesRequest -->

# Class ListSchedulesRequest (1.134.0)

`ListSchedulesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ListSchedules.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Schedules from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the Schedules that match the filter expression. The following fields are supported: - `display_name` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` : Supports `=` and `!=` comparisons.
- `request` : Supports existence of the |
`page_size` |
`int`
The standard list page size. Default to 100 if not specified. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListSchedulesResponse.next_page_token of the previous ScheduleService.ListSchedules call. |
`order_by` |
`str`
A comma-separated list of fields to order by. The default sort order is in ascending order. Use "desc" after a field name for descending. You can have multiple order_by fields provided. For example, using "create_time desc, end_time" will order results by create time in descending order, and if there are multiple schedules having the same create time, order them by the end time in ascending order. If order_by is not specified, it will order by default with create_time in descending order. Supported fields: - `create_time`
- `start_time`
- `end_time`
- `next_run_time`
|

## Methods

### ListSchedulesRequest

`ListSchedulesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ListSchedules.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestoolparameterkvmatchresults_googlecloudaiplat_3d4c58.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolparameterkvmatchresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchResults -->

# Class ToolParameterKVMatchResults (1.134.0)

`ToolParameterKVMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool parameter key value match metric.

## Attribute |
|
|---|---|
Name |
Description |
`tool_parameter_kv_match_metric_values` |
`MutableSequence[`
Output only. Tool parameter key value match metric values. |

## Methods

### ToolParameterKVMatchResults

`ToolParameterKVMatchResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for tool parameter key value match metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryrecallinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallInput -->

# Class TrajectoryRecallInput (1.134.0)

`TrajectoryRecallInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instances and metric spec for TrajectoryRecall metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for TrajectoryRecall metric. |
`instances` |
`MutableSequence[`
Required. Repeated TrajectoryRecall instance. |

## Methods

### TrajectoryRecallInput

`TrajectoryRecallInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instances and metric spec for TrajectoryRecall metric.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescreateentitytypeoperationmetadata_googleclou_4d0193.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreateentitytypeoperationmetadata_googlecloud_8e0f0a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreateentitytypeoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEntityTypeOperationMetadata -->

# Class CreateEntityTypeOperationMetadata (1.134.0)

```
CreateEntityTypeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create EntityType.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for EntityType. |

## Methods

### CreateEntityTypeOperationMetadata

```
CreateEntityTypeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create EntityType.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespauseschedulerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PauseScheduleRequest -->

# Class PauseScheduleRequest (1.134.0)

`PauseScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.PauseSchedule.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be paused. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|

## Methods

### PauseScheduleRequest

`PauseScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.PauseSchedule.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdatetensorboardoperationmetadata_googlecloudaipl_dcbe8d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatetensorboardoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardOperationMetadata -->

# Class UpdateTensorboardOperationMetadata (1.134.0)

```
UpdateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Tensorboard.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Tensorboard. |

## Methods

### UpdateTensorboardOperationMetadata

```
UpdateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Tensorboard.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragmanageddbconfigscaled.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagManagedDbConfig.Scaled -->

# Class Scaled (1.134.0)

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

## Methods

### Scaled

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.


---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typesstudyspecalgorithm_googlecloudaiplatform_b3e505.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesstudyspecalgorithm_googlecloudaiplatform__1e5f90.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesstudyspecalgorithm_googlecloudaiplatform_v_a0b58c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesstudyspecalgorithm_googlecloudaiplatform_v1_9311a5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesstudyspecalgorithm_googlecloudaiplatform_v1t_63a577.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstudyspecalgorithm_googlecloudaiplatform_v1ty_03688e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecalgorithm.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.Algorithm -->

# Class Algorithm (1.134.0)

`Algorithm(value)`


The available search algorithms for the Study.

## Enums |
|
|---|---|
Name |
Description |
`ALGORITHM_UNSPECIFIED` |
The default algorithm used by Vertex AI for `hyperparameter tuning |
`GRID_SEARCH` |
Simple grid search within the feasible space. To use grid search, all parameters must be `INTEGER`, `CATEGORICAL`, or `DISCRETE`. |
`RANDOM_SEARCH` |
Simple random search within the feasible space. |

## Methods

### Algorithm

`Algorithm(value)`


The available search algorithms for the Study.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatefeaturestoreoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeaturestoreOperationMetadata -->

# Class CreateFeaturestoreOperationMetadata (1.134.0)

```
CreateFeaturestoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Featurestore.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Featurestore. |

## Methods

### CreateFeaturestoreOperationMetadata

```
CreateFeaturestoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Featurestore.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatefeatureviewoperationmetadata_googlecloudaipl_6a800e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatefeatureviewoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureViewOperationMetadata -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletecustomjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteCustomJobRequest -->

# Class DeleteCustomJobRequest (1.134.0)

`DeleteCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteCustomJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the CustomJob resource to be deleted. Format: `projects/{project}/locations/{location}/customJobs/{custom_job}`
|

## Methods

### DeleteCustomJobRequest

`DeleteCustomJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.DeleteCustomJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Dataset -->

# Class Dataset (1.134.0)

`Dataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of DataItems and Annotations on them.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Identifier. The resource name of the Dataset. |
`display_name` |
`str`
Required. The user-defined name of the Dataset. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Dataset. |
`metadata_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing additional information about the Dataset. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/metadata/. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Required. Additional information about the Dataset. |
`data_item_count` |
`int`
Output only. The number of DataItems in this Dataset. Only apply for non-structured Dataset. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Dataset was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Dataset was last updated. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Datasets. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Dataset: - "aiplatform.googleapis.com/dataset_metadata_schema": output only, its value is the [metadata_schema's][google.cloud.aiplatform.v1.Dataset.metadata_schema_uri] title. |
`saved_queries` |
`MutableSequence[`
All SavedQueries belong to the Dataset will be returned in List/Get Dataset response. The annotation_specs field will not be populated except for UI cases which will only use annotation_spec_count. In CreateDataset request, a SavedQuery is created together if this field is set, up to one SavedQuery can be set in CreateDatasetRequest. The SavedQuery should not contain any AnnotationSpec. |
`encryption_spec` |
Customer-managed encryption key spec for a Dataset. If set, this Dataset and all sub-resources of this Dataset will be secured by this key. |
`metadata_artifact` |
`str`
Output only. The resource name of the Artifact that was created in MetadataStore when creating the Dataset. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}` .
|
`model_reference` |
`str`
Optional. Reference to the public base model last used by the dataset. Only set for prompt datasets. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

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

## Methods

### Dataset

`Dataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of DataItems and Annotations on them.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeneratememoriesrequest___googlecloudaiplatfo_8d64d8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratememoriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest -->

# Class GenerateMemoriesRequest (1.134.0)

`GenerateMemoriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.GenerateMemories.

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
`vertex_session_source` |
Defines a Vertex Session as the source content from which to generate memories. This field is a member of `oneof` _ `source` .
|
`direct_contents_source` |
Defines a direct source of content as the source content from which to generate memories. This field is a member of `oneof` _ `source` .
|
`direct_memories_source` |
Defines a direct source of memories that should be uploaded to Memory Bank. This is similar to `CreateMemory` , but it
allows for consolidation between these new memories and
existing memories for the same scope.
This field is a member of `oneof` _ `source` .
|
`parent` |
`str`
Required. The resource name of the ReasoningEngine to generate memories for. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`disable_consolidation` |
`bool`
Optional. If true, generated memories will not be consolidated with existing memories; all generated memories will be added as new memories regardless of whether they are duplicates of or contradictory to existing memories. By default, memory consolidation is enabled. |
`scope` |
`MutableMapping[str, str]`
Optional. The scope of the memories that should be generated. Memories will be consolidated across memories with the same scope. Must be provided unless the scope is defined in the source content. If `scope` is provided, it
will override the scope defined in the source content. Scope
values cannot contain the wildcard character '\*'.
|

## Classes

### DirectContentsSource

`DirectContentsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a direct source of content from which to generate the memories.

### DirectMemoriesSource

`DirectMemoriesSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a direct source of memories that should be uploaded to Memory Bank with consolidation.

### ScopeEntry

`ScopeEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### VertexSessionSource

`VertexSessionSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines an Agent Engine Session from which to generate the memories.
If `scope`

is not provided, the scope will be extracted from the
Session (i.e. {"user_id": sesison.user_id}).

## Methods

### GenerateMemoriesRequest

`GenerateMemoriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.GenerateMemories.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesupdatefeaturegroupoperationmetadata_googlecloudai_da1150.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdatefeaturegroupoperationmetadata_googlecloudaip_4fd5f2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatefeaturegroupoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureGroupOperationMetadata -->

# Class UpdateFeatureGroupOperationMetadata (1.134.0)

```
UpdateFeatureGroupOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update FeatureGroup.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for FeatureGroup. |

## Methods

### UpdateFeatureGroupOperationMetadata

```
UpdateFeatureGroupOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update FeatureGroup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetartifactrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetArtifactRequest -->

# Class GetArtifactRequest (1.134.0)

`GetArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetArtifact.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Artifact to retrieve. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|

## Methods

### GetArtifactRequest

`GetArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetArtifact.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatetensorboardoperationmetadata_googleclou_aa4f56.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatetensorboardoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardOperationMetadata -->

# Class UpdateTensorboardOperationMetadata (1.134.0)

```
UpdateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Tensorboard.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Tensorboard. |

## Methods

### UpdateTensorboardOperationMetadata

```
UpdateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update Tensorboard.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescanceltuningjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelTuningJobRequest -->

# Class CancelTuningJobRequest (1.134.0)

`CancelTuningJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.CancelTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TuningJob to cancel. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`
|

## Methods

### CancelTuningJobRequest

`CancelTuningJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.CancelTuningJob.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesgcssource_googlecloudaiplatform_v1typescre_b785e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesgcssource_googlecloudaiplatform_v1typescrea_04d8b3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgcssource_googlecloudaiplatform_v1typescreat_1f89ae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgcssource_googlecloudaiplatform_v1typescreate_549d44.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgcssource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GcsSource -->

# Class GcsSource (1.134.0)

`GcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Google Cloud Storage location for the input content.

## Attribute |
|
|---|---|
Name |
Description |
`uris` |
`MutableSequence[str]`
Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see https://cloud.google.com/storage/docs/wildcards. |

## Methods

### GcsSource

`GcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Google Cloud Storage location for the input content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatenasjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNasJobRequest -->

# Class CreateNasJobRequest (1.134.0)

`CreateNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CreateNasJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the NasJob in. Format: `projects/{project}/locations/{location}`
|
`nas_job` |
Required. The NasJob to create. |

## Methods

### CreateNasJobRequest

`CreateNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.CreateNasJob.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestaskdescriptionstrategy_googlecloudaiplatform_v1be_0b18e2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestaskdescriptionstrategy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TaskDescriptionStrategy -->

# Class TaskDescriptionStrategy (1.134.0)

`TaskDescriptionStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a generation strategy based on a high-level task description.

## Attribute |
|
|---|---|
Name |
Description |
`task_description` |
`str`
Required. A high-level description of the synthetic data to be generated. |

## Methods

### TaskDescriptionStrategy

`TaskDescriptionStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a generation strategy based on a high-level task description.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesassembledataoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataOperationMetadata -->

# Class AssembleDataOperationMetadata (1.134.0)

```
AssembleDataOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.AssembleData.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### AssembleDataOperationMetadata

```
AssembleDataOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.AssembleData.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfindneighborsrequest__googlecloudaiplatformv1schem_b25f50.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfindneighborsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoclassifica_7c403b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoclassificationinputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs -->

# Class AutoMlVideoClassificationInputs (1.134.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeleteschedulerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteScheduleRequest -->

# Class DeleteScheduleRequest (1.134.0)

`DeleteScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.DeleteSchedule.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be deleted. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|

## Methods

### DeleteScheduleRequest

`DeleteScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.DeleteSchedule.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforec_72a6ac.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforecastinginputstransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation -->

# Class Transformation (1.134.0)

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The categorical string as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.


### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

- Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The text as is--no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.


### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


## Methods

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesllm_utility_service_googlecloudaiplatform_c678f0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesllm_utility_service_googlecloudaiplatform__1430c1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesllm_utility_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service -->

# Package llm_utility_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.llm_utility_service`

package.

## Classes

[LlmUtilityServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceAsyncClient)

Service for LLM related utility functions.

[LlmUtilityServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceClient)

Service for LLM related utility functions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookexecutionjobview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJobView -->

# Class NotebookExecutionJobView (1.134.0)

`NotebookExecutionJobView(value)`


Views for Get/List NotebookExecutionJob

## Enums |
|
|---|---|
Name |
Description |
`NOTEBOOK_EXECUTION_JOB_VIEW_UNSPECIFIED` |
When unspecified, the API defaults to the BASIC view. |
`NOTEBOOK_EXECUTION_JOB_VIEW_BASIC` |
Includes all fields except for direct notebook inputs. |
`NOTEBOOK_EXECUTION_JOB_VIEW_FULL` |
Includes all fields. |

## Methods

### NotebookExecutionJobView

`NotebookExecutionJobView(value)`


Views for Get/List NotebookExecutionJob


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstreamdirectrawpredictresponse_googlecloudaip_4ff533.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstreamdirectrawpredictresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamDirectRawPredictResponse -->

# Class StreamDirectRawPredictResponse (1.134.0)

```
StreamDirectRawPredictResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PredictionService.StreamDirectRawPredict.

## Attribute |
|
|---|---|
Name |
Description |
`output` |
`bytes`
The prediction output. |

## Methods

### StreamDirectRawPredictResponse

```
StreamDirectRawPredictResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PredictionService.StreamDirectRawPredict.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringjobexecutiondetailprocesseddataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJobExecutionDetail.ProcessedDataset -->

# Class ProcessedDataset (1.134.0)

`ProcessedDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Processed dataset information.

## Attributes |
|
|---|---|
Name |
Description |
`location` |
`str`
Actual data location of the processed dataset. |
`time_range` |
`google.type.interval_pb2.Interval`
Dataset time range information if any. |

## Methods

### ProcessedDataset

`ProcessedDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Processed dataset information.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typescreatefeaturegroupoperationmetadata_googleclou_be770c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typescreatefeaturegroupoperationmetadata_googlecloud_2a6948.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescreatefeaturegroupoperationmetadata_googleclouda_bd6a62.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreatefeaturegroupoperationmetadata_googlecloudai_e610aa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatefeaturegroupoperationmetadata_googlecloudaip_8cb457.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatefeaturegroupoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureGroupOperationMetadata -->

# Class CreateFeatureGroupOperationMetadata (1.134.0)

```
CreateFeatureGroupOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create FeatureGroup.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for FeatureGroup. |

## Methods

### CreateFeatureGroupOperationMetadata

```
CreateFeatureGroupOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create FeatureGroup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolparameterkeymatchresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKeyMatchResults -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistschedulesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesRequest -->

# Class ListSchedulesRequest (1.134.0)

`ListSchedulesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ListSchedules.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Schedules from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the Schedules that match the filter expression. The following fields are supported: - `display_name` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` : Supports `=` and `!=` comparisons.
- `request` : Supports existence of the |
`page_size` |
`int`
The standard list page size. Default to 100 if not specified. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListSchedulesResponse.next_page_token of the previous ScheduleService.ListSchedules call. |
`order_by` |
`str`
A comma-separated list of fields to order by. The default sort order is in ascending order. Use "desc" after a field name for descending. You can have multiple order_by fields provided. For example, using "create_time desc, end_time" will order results by create time in descending order, and if there are multiple schedules having the same create time, order them by the end time in ascending order. If order_by is not specified, it will order by default with create_time in descending order. Supported fields: - `create_time`
- `start_time`
- `end_time`
- `next_run_time`
|

## Methods

### ListSchedulesRequest

`ListSchedulesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ListSchedules.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgetdatasetrequest_googlecloudaiplatform_v1beta1ty_27c188.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetdatasetrequest_googlecloudaiplatform_v1beta1typ_bd95c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetdatasetrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDatasetRequest -->

# Class GetDatasetRequest (1.134.0)

`GetDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDataset. Next ID: 4

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Dataset resource. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetDatasetRequest

`GetDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDataset. Next ID: 4


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatetensorboardoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTensorboardOperationMetadata -->

# Class CreateTensorboardOperationMetadata (1.134.0)

```
CreateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Tensorboard.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for Tensorboard. |

## Methods

### CreateTensorboardOperationMetadata

```
CreateTensorboardOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create Tensorboard.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbatchcancelpipelinejobsresponse_googlecloudai_d2fe3c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchcancelpipelinejobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCancelPipelineJobsResponse -->

# Class BatchCancelPipelineJobsResponse (1.134.0)

```
BatchCancelPipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchCancelPipelineJobs.

## Attribute |
|
|---|---|
Name |
Description |
`pipeline_jobs` |
`MutableSequence[`
PipelineJobs cancelled. |

## Methods

### BatchCancelPipelineJobsResponse

```
BatchCancelPipelineJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.BatchCancelPipelineJobs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateindexrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexRequest -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesgetextensionrequest_googlecloudaiplatformv1_dcdd32.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgetextensionrequest_googlecloudaiplatformv1s_827bf1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetextensionrequest_googlecloudaiplatformv1sc_69e204.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetextensionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExtensionRequest -->

# Class GetExtensionRequest (1.134.0)

`GetExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.GetExtension.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Extension resource. Format: `projects/{project}/locations/{location}/extensions/{extension}`
|

## Methods

### GetExtensionRequest

`GetExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.GetExtension.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltextclassificationinputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs -->

# Class AutoMlTextClassificationInputs (1.134.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreadtensorboardblobdataresponse_googlecloudaiplatf_dc8079.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadtensorboardblobdataresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardBlobDataResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetartifactrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetArtifactRequest -->

# Class GetArtifactRequest (1.134.0)

`GetArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetArtifact.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Artifact to retrieve. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|

## Methods

### GetArtifactRequest

`GetArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetArtifact.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Dataset -->

# Class Dataset (1.134.0)

`Dataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of DataItems and Annotations on them.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Identifier. The resource name of the Dataset. |
`display_name` |
`str`
Required. The user-defined name of the Dataset. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Dataset. |
`metadata_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing additional information about the Dataset. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/metadata/. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Required. Additional information about the Dataset. |
`data_item_count` |
`int`
Output only. The number of DataItems in this Dataset. Only apply for non-structured Dataset. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Dataset was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Dataset was last updated. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Datasets. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Dataset: - "aiplatform.googleapis.com/dataset_metadata_schema": output only, its value is the [metadata_schema's][google.cloud.aiplatform.v1beta1.Dataset.metadata_schema_uri] title. |
`saved_queries` |
`MutableSequence[`
All SavedQueries belong to the Dataset will be returned in List/Get Dataset response. The annotation_specs field will not be populated except for UI cases which will only use annotation_spec_count. In CreateDataset request, a SavedQuery is created together if this field is set, up to one SavedQuery can be set in CreateDatasetRequest. The SavedQuery should not contain any AnnotationSpec. |
`encryption_spec` |
Customer-managed encryption key spec for a Dataset. If set, this Dataset and all sub-resources of this Dataset will be secured by this key. |
`metadata_artifact` |
`str`
Output only. The resource name of the Artifact that was created in MetadataStore when creating the Dataset. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}` .
|
`model_reference` |
`str`
Optional. Reference to the public base model last used by the dataset. Only set for prompt datasets. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

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

## Methods

### Dataset

`Dataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of DataItems and Annotations on them.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.tensorboard_service.pagers`

module.

## Classes

[ExportTensorboardTimeSeriesDataAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ExportTensorboardTimeSeriesDataAsyncPager)

```
ExportTensorboardTimeSeriesDataAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `export_tensorboard_time_series_data`

requests.

This class thinly wraps an initial
[ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse) object, and
provides an `__aiter__`

method to iterate through its
`time_series_data_points`

field.

If there are more pages, the `__aiter__`

method will make additional
`ExportTensorboardTimeSeriesData`

requests and continue to iterate
through the `time_series_data_points`

field on the
corresponding responses.

All the usual [ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ExportTensorboardTimeSeriesDataPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ExportTensorboardTimeSeriesDataPager)

```
ExportTensorboardTimeSeriesDataPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `export_tensorboard_time_series_data`

requests.

This class thinly wraps an initial
[ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse) object, and
provides an `__iter__`

method to iterate through its
`time_series_data_points`

field.

If there are more pages, the `__iter__`

method will make additional
`ExportTensorboardTimeSeriesData`

requests and continue to iterate
through the `time_series_data_points`

field on the
corresponding responses.

All the usual [ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTensorboardExperimentsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardExperimentsAsyncPager)

```
ListTensorboardExperimentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_experiments`

requests.

This class thinly wraps an initial
[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_experiments`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardExperiments`

requests and continue to iterate
through the `tensorboard_experiments`

field on the
corresponding responses.

All the usual [ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTensorboardExperimentsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardExperimentsPager)

```
ListTensorboardExperimentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_experiments`

requests.

This class thinly wraps an initial
[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_experiments`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardExperiments`

requests and continue to iterate
through the `tensorboard_experiments`

field on the
corresponding responses.

All the usual [ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTensorboardRunsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardRunsAsyncPager)

```
ListTensorboardRunsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_runs`

requests.

This class thinly wraps an initial
[ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_runs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardRuns`

requests and continue to iterate
through the `tensorboard_runs`

field on the
corresponding responses.

All the usual [ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTensorboardRunsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardRunsPager)

```
ListTensorboardRunsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_runs`

requests.

This class thinly wraps an initial
[ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_runs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardRuns`

requests and continue to iterate
through the `tensorboard_runs`

field on the
corresponding responses.

All the usual [ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTensorboardTimeSeriesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesAsyncPager)

```
ListTensorboardTimeSeriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_time_series`

requests.

This class thinly wraps an initial
[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_time_series`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardTimeSeries`

requests and continue to iterate
through the `tensorboard_time_series`

field on the
corresponding responses.

All the usual [ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTensorboardTimeSeriesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesPager)

```
ListTensorboardTimeSeriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_time_series`

requests.

This class thinly wraps an initial
[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_time_series`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardTimeSeries`

requests and continue to iterate
through the `tensorboard_time_series`

field on the
corresponding responses.

All the usual [ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTensorboardsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardsAsyncPager)

```
ListTensorboardsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboards`

requests.

This class thinly wraps an initial
[ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboards`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboards`

requests and continue to iterate
through the `tensorboards`

field on the
corresponding responses.

All the usual [ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTensorboardsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardsPager)

```
ListTensorboardsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboards`

requests.

This class thinly wraps an initial
[ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboards`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboards`

requests and continue to iterate
through the `tensorboards`

field on the
corresponding responses.

All the usual [ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.
