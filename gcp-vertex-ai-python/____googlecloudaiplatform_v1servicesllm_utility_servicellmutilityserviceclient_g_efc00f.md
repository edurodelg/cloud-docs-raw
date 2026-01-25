---
merged_at: 2026-01-25T21:47:44.396484
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesllm_utility_servicellmutilityserviceclient_go_8d197a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesllm_utility_servicellmutilityserviceclient_goo_d9517b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesllm_utility_servicellmutilityserviceclient_goog_30bf04.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesllm_utility_servicellmutilityserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.llm_utility_service.LlmUtilityServiceClient -->

# Class LlmUtilityServiceClient (1.134.0)

```
LlmUtilityServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for LLM related utility functions.

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
`LlmUtilityServiceTransport` |
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

### LlmUtilityServiceClient

```
LlmUtilityServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the llm utility service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,LlmUtilityServiceTransport,Callable[..., LlmUtilityServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the LlmUtilityServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### compute_tokens

```
compute_tokens(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.llm_utility_service.ComputeTokensRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.llm_utility_service.ComputeTokensResponse
```


Return a list of tokens based on the input text.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_compute_tokens():
# Create a client
client = aiplatform_v1.
```[LlmUtilityServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.llm_utility_service.LlmUtilityServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ComputeTokensRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ComputeTokensRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[compute_tokens](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.llm_utility_service.LlmUtilityServiceClient.html#google_cloud_aiplatform_v1_services_llm_utility_service_LlmUtilityServiceClient_compute_tokens)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ComputeTokens RPC call. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to get lists of tokens and token ids. This corresponds to the |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Optional. The instances that are the input to token computing API call. Schema is identical to the prediction schema of the text model, even for the non-text models, like chat models, or Codey models. This corresponds to the |
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
Response message for ComputeTokens RPC call. |

### count_tokens

```
count_tokens(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.prediction_service.CountTokensRequest, dict
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.prediction_service.CountTokensResponse
```


Perform a token counting.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_count_tokens():
# Create a client
client = aiplatform_v1.
```[LlmUtilityServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.llm_utility_service.LlmUtilityServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CountTokensRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CountTokensRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = client.[count_tokens](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.llm_utility_service.LlmUtilityServiceClient.html#google_cloud_aiplatform_v1_services_llm_utility_service_LlmUtilityServiceClient_count_tokens)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PredictionService.CountTokens][]. |
`endpoint` |
`str`
Required. The name of the Endpoint requested to perform token counting. Format: |
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Optional. The instances that are the input to token counting call. Schema is identical to the prediction schema of the underlying model. This corresponds to the |
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
Response message for [PredictionService.CountTokens][]. |

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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

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
`LlmUtilityServiceClient` |
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
`LlmUtilityServiceClient` |
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
`LlmUtilityServiceClient` |
The constructed client. |

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesevaluation_serviceevaluationserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceAsyncClient -->

# Class EvaluationServiceAsyncClient (1.134.0)

```
EvaluationServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Vertex AI Online Evaluation Service.

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
`EvaluationServiceTransport` |
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

### EvaluationServiceAsyncClient

```
EvaluationServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the evaluation service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,EvaluationServiceTransport,Callable[..., EvaluationServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the EvaluationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### evaluate_dataset

```
evaluate_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.evaluation_service.EvaluateDatasetRequest,
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
) -> google.api_core.operation_async.AsyncOperation
```


Evaluates a dataset based on a set of given metrics.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_evaluate_dataset():
# Create a client
client = aiplatform_v1beta1.
```[EvaluationServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceAsyncClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1beta1.[EvaluationDataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluationDataset.html)()
dataset.gcs_source.uris = ['uris_value1', 'uris_value2']
output_config = aiplatform_v1beta1.[OutputConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.OutputConfig.html)()
output_config.gcs_destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[EvaluateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetRequest.html)(
location="location_value",
dataset=dataset,
output_config=output_config,
)
# Make the request
operation = client.[evaluate_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_evaluation_service_EvaluationServiceAsyncClient_evaluate_dataset)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EvaluationService.EvaluateDataset. |
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
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be
|

### evaluate_instances

```
evaluate_instances(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.evaluation_service.EvaluateInstancesRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.evaluation_service.EvaluateInstancesResponse
```


Evaluates instances based on a given metric.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_evaluate_instances():
# Create a client
client = aiplatform_v1beta1.
```[EvaluationServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[EvaluateInstancesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateInstancesRequest.html)(
location="location_value",
)
# Make the request
response = await client.[evaluate_instances](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_evaluation_service_EvaluationServiceAsyncClient_evaluate_instances)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EvaluationService.EvaluateInstances. |
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
Response message for EvaluationService.EvaluateInstances. |

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
`EvaluationServiceAsyncClient` |
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
`EvaluationServiceAsyncClient` |
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
`EvaluationServiceAsyncClient` |
The constructed client. |

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
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicemodelmonitoringserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient -->

# Class ModelMonitoringServiceClient (1.134.0)

```
ModelMonitoringServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_monitoring_service.transports.base.ModelMonitoringServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_monitoring_service.transports.base.ModelMonitoringServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI Model moitoring. This
includes `ModelMonitor`

resources, `ModelMonitoringJob`

resources.

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
`ModelMonitoringServiceTransport` |
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

### ModelMonitoringServiceClient

```
ModelMonitoringServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_monitoring_service.transports.base.ModelMonitoringServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_monitoring_service.transports.base.ModelMonitoringServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the model monitoring service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ModelMonitoringServiceTransport,Callable[..., ModelMonitoringServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ModelMonitoringServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_prediction_job_path

```
batch_prediction_job_path(
project: str, location: str, batch_prediction_job: str
) -> str
```


Returns a fully-qualified batch_prediction_job string.

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

### create_model_monitor

```
create_model_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.CreateModelMonitorRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_monitor: typing.Optional[
google.cloud.aiplatform_v1beta1.types.model_monitor.ModelMonitor
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Creates a ModelMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_model_monitor():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateModelMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelMonitorRequest.html)(
parent="parent_value",
)
# Make the request
operation = client.[create_model_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_create_model_monitor)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.CreateModelMonitor. |
`parent` |
`str`
Required. The resource name of the Location to create the ModelMonitor in. Format: |
`model_monitor` |
Required. The ModelMonitor to create. This corresponds to the |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### create_model_monitoring_job

```
create_model_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.CreateModelMonitoringJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_monitoring_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.model_monitoring_job.ModelMonitoringJob
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.model_monitoring_job.ModelMonitoringJob
```


Creates a ModelMonitoringJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_model_monitoring_job():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateModelMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelMonitoringJobRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_model_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_create_model_monitoring_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.CreateModelMonitoringJob. |
`parent` |
`str`
Required. The parent of the ModelMonitoringJob. Format: |
`model_monitoring_job` |
Required. The ModelMonitoringJob to create This corresponds to the |
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
Represents a model monitoring job that analyze dataset using different monitoring algorithm. |

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

### delete_model_monitor

```
delete_model_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.DeleteModelMonitorRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a ModelMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_model_monitor():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteModelMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelMonitorRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_delete_model_monitor)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.DeleteModelMonitor. |
`name` |
`str`
Required. The name of the ModelMonitor resource to be deleted. Format: |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_model_monitoring_job

```
delete_model_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.DeleteModelMonitoringJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a ModelMonitoringJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_model_monitoring_job():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteModelMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_delete_model_monitoring_job)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.DeleteModelMonitoringJob. |
`name` |
`str`
Required. The resource name of the model monitoring job to delete. Format: |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

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
`ModelMonitoringServiceClient` |
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
`ModelMonitoringServiceClient` |
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
`ModelMonitoringServiceClient` |
The constructed client. |

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

### get_model_monitor

```
get_model_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.GetModelMonitorRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.model_monitor.ModelMonitor
```


Gets a ModelMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_model_monitor():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelMonitorRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_get_model_monitor)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.GetModelMonitor. |
`name` |
`str`
Required. The name of the ModelMonitor resource. Format: |
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
Vertex AI Model Monitoring Service serves as a central hub for the analysis and visualization of data quality and performance related to models. ModelMonitor stands as a top level resource for overseeing your model monitoring tasks. |

### get_model_monitoring_job

```
get_model_monitoring_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.GetModelMonitoringJobRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.model_monitoring_job.ModelMonitoringJob
```


Gets a ModelMonitoringJob.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_model_monitoring_job():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelMonitoringJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelMonitoringJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model_monitoring_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_get_model_monitoring_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.GetModelMonitoringJob. |
`name` |
`str`
Required. The resource name of the ModelMonitoringJob. Format: |
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
Represents a model monitoring job that analyze dataset using different monitoring algorithm. |

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

### list_model_monitoring_jobs

```
list_model_monitoring_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitoringJobsPager
)
```


Lists ModelMonitoringJobs. Callers may choose to read across
multiple Monitors as per
`AIP-159 <https://google.aip.dev/159>`

__ by using '-' (the
hyphen or dash character) as a wildcard character instead of
modelMonitor id in the parent. Format
`projects/{project_id}/locations/{location}/moodelMonitors/-/modelMonitoringJobs`


```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_model_monitoring_jobs():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelMonitoringJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_monitoring_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_list_model_monitoring_jobs)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.ListModelMonitoringJobs. |
`parent` |
`str`
Required. The parent of the ModelMonitoringJob. Format: |
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
Response message for ModelMonitoringService.ListModelMonitoringJobs. Iterating over this object will yield results and resolve additional pages automatically. |

### list_model_monitors

```
list_model_monitors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitorsPager
)
```


Lists ModelMonitors in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_model_monitors():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelMonitorsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_monitors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_list_model_monitors)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.ListModelMonitors. |
`parent` |
`str`
Required. The resource name of the Location to list the ModelMonitors from. Format: |
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
Response message for ModelMonitoringService.ListModelMonitors Iterating over this object will yield results and resolve additional pages automatically. |

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

### model_monitor_path

`model_monitor_path(project: str, location: str, model_monitor: str) -> str`


Returns a fully-qualified model_monitor string.

### model_monitoring_job_path

```
model_monitoring_job_path(
project: str, location: str, model_monitor: str, model_monitoring_job: str
) -> str
```


Returns a fully-qualified model_monitoring_job string.

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### parse_batch_prediction_job_path

`parse_batch_prediction_job_path(path: str) -> typing.Dict[str, str]`


Parses a batch_prediction_job path into its component segments.

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

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_monitor_path

`parse_model_monitor_path(path: str) -> typing.Dict[str, str]`


Parses a model_monitor path into its component segments.

### parse_model_monitoring_job_path

`parse_model_monitoring_job_path(path: str) -> typing.Dict[str, str]`


Parses a model_monitoring_job path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### schedule_path

`schedule_path(project: str, location: str, schedule: str) -> str`


Returns a fully-qualified schedule string.

### search_model_monitoring_alerts

```
search_model_monitoring_alerts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsRequest,
dict,
]
] = None,
*,
model_monitor: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.SearchModelMonitoringAlertsPager
)
```


Returns the Model Monitoring alerts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_search_model_monitoring_alerts():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchModelMonitoringAlertsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringAlertsRequest.html)(
model_monitor="model_monitor_value",
)
# Make the request
page_result = client.[search_model_monitoring_alerts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_search_model_monitoring_alerts)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.SearchModelMonitoringAlerts. |
`model_monitor` |
`str`
Required. ModelMonitor resource name. Format: |
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
Response message for ModelMonitoringService.SearchModelMonitoringAlerts. Iterating over this object will yield results and resolve additional pages automatically. |

### search_model_monitoring_stats

```
search_model_monitoring_stats(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsRequest,
dict,
]
] = None,
*,
model_monitor: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.SearchModelMonitoringStatsPager
)
```


Searches Model Monitoring Stats generated within a given time window.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_search_model_monitoring_stats():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchModelMonitoringStatsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsRequest.html)(
model_monitor="model_monitor_value",
)
# Make the request
page_result = client.[search_model_monitoring_stats](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_search_model_monitoring_stats)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.SearchModelMonitoringStats. |
`model_monitor` |
`str`
Required. ModelMonitor resource name. Format: |
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
Response message for ModelMonitoringService.SearchModelMonitoringStats. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_model_monitor

```
update_model_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.UpdateModelMonitorRequest,
dict,
]
] = None,
*,
model_monitor: typing.Optional[
google.cloud.aiplatform_v1beta1.types.model_monitor.ModelMonitor
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Updates a ModelMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_model_monitor():
# Create a client
client = aiplatform_v1beta1.
```[ModelMonitoringServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateModelMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelMonitorRequest.html)(
)
# Make the request
operation = client.[update_model_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.ModelMonitoringServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_monitoring_service_ModelMonitoringServiceClient_update_model_monitor)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelMonitoringService.UpdateModelMonitor. |
`model_monitor` |
Required. The model monitoring configuration which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Mask specifying which fields to update. This corresponds to the |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicemetadataserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient -->

# Class MetadataServiceAsyncClient (1.134.0)

```
MetadataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.metadata_service.transports.base.MetadataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.metadata_service.transports.base.MetadataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for reading and writing metadata entries.

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
`MetadataServiceTransport` |
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

### MetadataServiceAsyncClient

```
MetadataServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.metadata_service.transports.base.MetadataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.metadata_service.transports.base.MetadataServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the metadata service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MetadataServiceTransport,Callable[..., MetadataServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the MetadataServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### add_context_artifacts_and_executions

```
add_context_artifacts_and_executions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.AddContextArtifactsAndExecutionsRequest,
dict,
]
] = None,
*,
context: typing.Optional[str] = None,
artifacts: typing.Optional[typing.MutableSequence[str]] = None,
executions: typing.Optional[typing.MutableSequence[str]] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.metadata_service.AddContextArtifactsAndExecutionsResponse
)
```


Adds a set of Artifacts and Executions to a Context. If any of the Artifacts or Executions have already been added to a Context, they are simply skipped.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_add_context_artifacts_and_executions():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddContextArtifactsAndExecutionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddContextArtifactsAndExecutionsRequest.html)(
context="context_value",
)
# Make the request
response = await client.[add_context_artifacts_and_executions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_add_context_artifacts_and_executions)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.AddContextArtifactsAndExecutions. |
`context` |
Required. The resource name of the Context that the Artifacts and Executions belong to. Format: |
`artifacts` |
`:class:`
The resource names of the Artifacts to attribute to the Context. Format: |
`executions` |
`:class:`
The resource names of the Executions to associate with the Context. Format: |
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
Response message for MetadataService.AddContextArtifactsAndExecutions. |

### add_context_children

```
add_context_children(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.AddContextChildrenRequest,
dict,
]
] = None,
*,
context: typing.Optional[str] = None,
child_contexts: typing.Optional[typing.MutableSequence[str]] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_service.AddContextChildrenResponse
```


Adds a set of Contexts as children to a parent Context. If any of the child Contexts have already been added to the parent Context, they are simply skipped. If this call would create a cycle or cause any Context to have more than 10 parents, the request will fail with an INVALID_ARGUMENT error.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_add_context_children():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddContextChildrenRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddContextChildrenRequest.html)(
context="context_value",
)
# Make the request
response = await client.[add_context_children](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_add_context_children)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.AddContextChildren. |
`context` |
Required. The resource name of the parent Context. Format: |
`child_contexts` |
`:class:`
The resource names of the child Contexts. This corresponds to the |
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
Response message for MetadataService.AddContextChildren. |

### add_execution_events

```
add_execution_events(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.AddExecutionEventsRequest,
dict,
]
] = None,
*,
execution: typing.Optional[str] = None,
events: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1.types.event.Event]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_service.AddExecutionEventsResponse
```


Adds Events to the specified Execution. An Event indicates whether an Artifact was used as an input or output for an Execution. If an Event already exists between the Execution and the Artifact, the Event is skipped.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_add_execution_events():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddExecutionEventsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddExecutionEventsRequest.html)(
execution="execution_value",
)
# Make the request
response = await client.[add_execution_events](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_add_execution_events)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.AddExecutionEvents. |
`execution` |
Required. The resource name of the Execution that the Events connect Artifacts with. Format: |
`events` |
`:class:`
The Events to create and add. This corresponds to the |
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
Response message for MetadataService.AddExecutionEvents. |

### artifact_path

```
artifact_path(
project: str, location: str, metadata_store: str, artifact: str
) -> str
```


Returns a fully-qualified artifact string.

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

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_artifact

```
create_artifact(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateArtifactRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
artifact: typing.Optional[
google.cloud.aiplatform_v1.types.artifact.Artifact
] = None,
artifact_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.artifact.Artifact
```


Creates an Artifact associated with a MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_artifact():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateArtifactRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateArtifactRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_artifact](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_create_artifact)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.CreateArtifact. |
`parent` |
Required. The resource name of the MetadataStore where the Artifact should be created. Format: |
`artifact` |
Required. The Artifact to create. This corresponds to the |
`artifact_id` |
The {artifact} portion of the resource name with the format: |
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
Instance of a general artifact. |

### create_context

```
create_context(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateContextRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
context: typing.Optional[google.cloud.aiplatform_v1.types.context.Context] = None,
context_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.context.Context
```


Creates a Context associated with a MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_context():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateContextRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateContextRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_context](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_create_context)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.CreateContext. |
`parent` |
Required. The resource name of the MetadataStore where the Context should be created. Format: |
`context` |
Required. The Context to create. This corresponds to the |
`context_id` |
The {context} portion of the resource name with the format: |
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
Instance of a general context. |

### create_execution

```
create_execution(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateExecutionRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
execution: typing.Optional[
google.cloud.aiplatform_v1.types.execution.Execution
] = None,
execution_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.execution.Execution
```


Creates an Execution associated with a MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_execution():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateExecutionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateExecutionRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_execution](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_create_execution)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.CreateExecution. |
`parent` |
Required. The resource name of the MetadataStore where the Execution should be created. Format: |
`execution` |
Required. The Execution to create. This corresponds to the |
`execution_id` |
The {execution} portion of the resource name with the format: |
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
Instance of a general execution. |

### create_metadata_schema

```
create_metadata_schema(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateMetadataSchemaRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
metadata_schema: typing.Optional[
google.cloud.aiplatform_v1.types.metadata_schema.MetadataSchema
] = None,
metadata_schema_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_schema.MetadataSchema
```


Creates a MetadataSchema.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_metadata_schema():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
metadata_schema = aiplatform_v1.[MetadataSchema](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetadataSchema.html)()
metadata_schema.schema = "schema_value"
request = aiplatform_v1.[CreateMetadataSchemaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateMetadataSchemaRequest.html)(
parent="parent_value",
metadata_schema=metadata_schema,
)
# Make the request
response = await client.[create_metadata_schema](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_create_metadata_schema)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.CreateMetadataSchema. |
`parent` |
Required. The resource name of the MetadataStore where the MetadataSchema should be created. Format: |
`metadata_schema` |
Required. The MetadataSchema to create. This corresponds to the |
`metadata_schema_id` |
The {metadata_schema} portion of the resource name with the format: |
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
Instance of a general MetadataSchema. |

### create_metadata_store

```
create_metadata_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateMetadataStoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
metadata_store: typing.Optional[
google.cloud.aiplatform_v1.types.metadata_store.MetadataStore
] = None,
metadata_store_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Initializes a MetadataStore, including allocation of resources.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_metadata_store():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateMetadataStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateMetadataStoreRequest.html)(
parent="parent_value",
)
# Make the request
operation = client.[create_metadata_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_create_metadata_store)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.CreateMetadataStore. |
`parent` |
Required. The resource name of the Location where the MetadataStore should be created. Format: |
`metadata_store` |
Required. The MetadataStore to create. This corresponds to the |
`metadata_store_id` |
The {metadatastore} portion of the resource name with the format: |
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
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be
|

### delete_artifact

```
delete_artifact(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.DeleteArtifactRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Deletes an Artifact.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_artifact():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteArtifactRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteArtifactRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_artifact](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_delete_artifact)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.DeleteArtifact. |
`name` |
Required. The resource name of the Artifact to delete. Format: |
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
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_context

```
delete_context(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.DeleteContextRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a stored Context.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_context():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteContextRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteContextRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_context](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_delete_context)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.DeleteContext. |
`name` |
Required. The resource name of the Context to delete. Format: |
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
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_execution

```
delete_execution(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.DeleteExecutionRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Deletes an Execution.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_execution():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteExecutionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteExecutionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_execution](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_delete_execution)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.DeleteExecution. |
`name` |
Required. The resource name of the Execution to delete. Format: |
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
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_metadata_store

```
delete_metadata_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.DeleteMetadataStoreRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Deletes a single MetadataStore and all its child resources (Artifacts, Executions, and Contexts).

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_metadata_store():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteMetadataStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteMetadataStoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_metadata_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_delete_metadata_store)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.DeleteMetadataStore. |
`name` |
Required. The resource name of the MetadataStore to delete. Format: |
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
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

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

### execution_path

```
execution_path(
project: str, location: str, metadata_store: str, execution: str
) -> str
```


Returns a fully-qualified execution string.

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
`MetadataServiceAsyncClient` |
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
`MetadataServiceAsyncClient` |
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
`MetadataServiceAsyncClient` |
The constructed client. |

### get_artifact

```
get_artifact(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetArtifactRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.artifact.Artifact
```


Retrieves a specific Artifact.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_artifact():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetArtifactRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetArtifactRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_artifact](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_get_artifact)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.GetArtifact. |
`name` |
Required. The resource name of the Artifact to retrieve. Format: |
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
Instance of a general artifact. |

### get_context

```
get_context(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetContextRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.context.Context
```


Retrieves a specific Context.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_context():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetContextRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetContextRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_context](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_get_context)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.GetContext. |
`name` |
Required. The resource name of the Context to retrieve. Format: |
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
Instance of a general context. |

### get_execution

```
get_execution(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetExecutionRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.execution.Execution
```


Retrieves a specific Execution.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_execution():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetExecutionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetExecutionRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_execution](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_get_execution)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.GetExecution. |
`name` |
Required. The resource name of the Execution to retrieve. Format: |
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
Instance of a general execution. |

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

### get_metadata_schema

```
get_metadata_schema(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetMetadataSchemaRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_schema.MetadataSchema
```


Retrieves a specific MetadataSchema.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_metadata_schema():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetMetadataSchemaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetMetadataSchemaRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_metadata_schema](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_get_metadata_schema)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.GetMetadataSchema. |
`name` |
Required. The resource name of the MetadataSchema to retrieve. Format: |
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
Instance of a general MetadataSchema. |

### get_metadata_store

```
get_metadata_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetMetadataStoreRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_store.MetadataStore
```


Retrieves a specific MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_metadata_store():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetMetadataStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetMetadataStoreRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_metadata_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_get_metadata_store)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.GetMetadataStore. |
`name` |
Required. The resource name of the MetadataStore to retrieve. Format: |
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
Instance of a metadata store. Contains a set of metadata that can be queried. |

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
google.cloud.aiplatform_v1.services.metadata_service.transports.base.MetadataServiceTransport
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

### list_artifacts

```
list_artifacts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.metadata_service.pagers.ListArtifactsAsyncPager
)
```


Lists Artifacts in the MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_artifacts():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListArtifactsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_artifacts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_list_artifacts)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.ListArtifacts. |
`parent` |
Required. The MetadataStore whose Artifacts should be listed. Format: |
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
Response message for MetadataService.ListArtifacts. Iterating over this object will yield results and resolve additional pages automatically. |

### list_contexts

```
list_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.metadata_service.pagers.ListContextsAsyncPager
```


Lists Contexts on the MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_contexts():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_list_contexts)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.ListContexts |
`parent` |
Required. The MetadataStore whose Contexts should be listed. Format: |
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
Response message for MetadataService.ListContexts. Iterating over this object will yield results and resolve additional pages automatically. |

### list_executions

```
list_executions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.metadata_service.pagers.ListExecutionsAsyncPager
)
```


Lists Executions in the MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_executions():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListExecutionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_executions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_list_executions)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.ListExecutions. |
`parent` |
Required. The MetadataStore whose Executions should be listed. Format: |
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
Response message for MetadataService.ListExecutions. Iterating over this object will yield results and resolve additional pages automatically. |

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

### list_metadata_schemas

```
list_metadata_schemas(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataSchemasAsyncPager
)
```


Lists MetadataSchemas.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_metadata_schemas():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListMetadataSchemasRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_metadata_schemas](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_list_metadata_schemas)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.ListMetadataSchemas. |
`parent` |
Required. The MetadataStore whose MetadataSchemas should be listed. Format: |
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
Response message for MetadataService.ListMetadataSchemas. Iterating over this object will yield results and resolve additional pages automatically. |

### list_metadata_stores

```
list_metadata_stores(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataStoresAsyncPager
)
```


Lists MetadataStores for a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_metadata_stores():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListMetadataStoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_metadata_stores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_list_metadata_stores)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.ListMetadataStores. |
`parent` |
Required. The Location whose MetadataStores should be listed. Format: |
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
Response message for MetadataService.ListMetadataStores. Iterating over this object will yield results and resolve additional pages automatically. |

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

### metadata_schema_path

```
metadata_schema_path(
project: str, location: str, metadata_store: str, metadata_schema: str
) -> str
```


Returns a fully-qualified metadata_schema string.

### metadata_store_path

`metadata_store_path(project: str, location: str, metadata_store: str) -> str`


Returns a fully-qualified metadata_store string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_metadata_schema_path

`parse_metadata_schema_path(path: str) -> typing.Dict[str, str]`


Parses a metadata_schema path into its component segments.

### parse_metadata_store_path

`parse_metadata_store_path(path: str) -> typing.Dict[str, str]`


Parses a metadata_store path into its component segments.

### purge_artifacts

```
purge_artifacts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.PurgeArtifactsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Purges Artifacts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_purge_artifacts():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PurgeArtifactsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeArtifactsRequest.html)(
parent="parent_value",
filter="filter_value",
)
# Make the request
operation = client.[purge_artifacts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_purge_artifacts)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.PurgeArtifacts. |
`parent` |
Required. The metadata store to purge Artifacts from. Format: |
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
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be
|

### purge_contexts

```
purge_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.PurgeContextsRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Purges Contexts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_purge_contexts():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PurgeContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeContextsRequest.html)(
parent="parent_value",
filter="filter_value",
)
# Make the request
operation = client.[purge_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_purge_contexts)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.PurgeContexts. |
`parent` |
Required. The metadata store to purge Contexts from. Format: |
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
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be
|

### purge_executions

```
purge_executions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.PurgeExecutionsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Purges Executions.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_purge_executions():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PurgeExecutionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeExecutionsRequest.html)(
parent="parent_value",
filter="filter_value",
)
# Make the request
operation = client.[purge_executions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_purge_executions)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.PurgeExecutions. |
`parent` |
Required. The metadata store to purge Executions from. Format: |
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
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be
|

### query_artifact_lineage_subgraph

```
query_artifact_lineage_subgraph(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.QueryArtifactLineageSubgraphRequest,
dict,
]
] = None,
*,
artifact: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.lineage_subgraph.LineageSubgraph
```


Retrieves lineage of an Artifact represented through Artifacts and Executions connected by Event edges and returned as a LineageSubgraph.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_query_artifact_lineage_subgraph():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryArtifactLineageSubgraphRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryArtifactLineageSubgraphRequest.html)(
artifact="artifact_value",
)
# Make the request
response = await client.[query_artifact_lineage_subgraph](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_query_artifact_lineage_subgraph)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.QueryArtifactLineageSubgraph. |
`artifact` |
Required. The resource name of the Artifact whose Lineage needs to be retrieved as a LineageSubgraph. Format: |
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
A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes. |

### query_context_lineage_subgraph

```
query_context_lineage_subgraph(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.QueryContextLineageSubgraphRequest,
dict,
]
] = None,
*,
context: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.lineage_subgraph.LineageSubgraph
```


Retrieves Artifacts and Executions within the specified Context, connected by Event edges and returned as a LineageSubgraph.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_query_context_lineage_subgraph():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryContextLineageSubgraphRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryContextLineageSubgraphRequest.html)(
context="context_value",
)
# Make the request
response = await client.[query_context_lineage_subgraph](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_query_context_lineage_subgraph)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.QueryContextLineageSubgraph. |
`context` |
Required. The resource name of the Context whose Artifacts and Executions should be retrieved as a LineageSubgraph. Format: |
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
A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes. |

### query_execution_inputs_and_outputs

```
query_execution_inputs_and_outputs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.QueryExecutionInputsAndOutputsRequest,
dict,
]
] = None,
*,
execution: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.lineage_subgraph.LineageSubgraph
```


Obtains the set of input and output Artifacts for this Execution, in the form of LineageSubgraph that also contains the Execution and connecting Events.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_query_execution_inputs_and_outputs():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryExecutionInputsAndOutputsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryExecutionInputsAndOutputsRequest.html)(
execution="execution_value",
)
# Make the request
response = await client.[query_execution_inputs_and_outputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_query_execution_inputs_and_outputs)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.QueryExecutionInputsAndOutputs. |
`execution` |
Required. The resource name of the Execution whose input and output Artifacts should be retrieved as a LineageSubgraph. Format: |
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
A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes. |

### remove_context_children

```
remove_context_children(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.RemoveContextChildrenRequest,
dict,
]
] = None,
*,
context: typing.Optional[str] = None,
child_contexts: typing.Optional[typing.MutableSequence[str]] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_service.RemoveContextChildrenResponse
```


Remove a set of children contexts from a parent Context. If any of the child Contexts were NOT added to the parent Context, they are simply skipped.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_remove_context_children():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RemoveContextChildrenRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveContextChildrenRequest.html)(
context="context_value",
)
# Make the request
response = await client.[remove_context_children](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_remove_context_children)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [MetadataService.DeleteContextChildrenRequest][]. |
`context` |
Required. The resource name of the parent Context. Format: |
`child_contexts` |
`:class:`
The resource names of the child Contexts. This corresponds to the |
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
Response message for MetadataService.RemoveContextChildren. |

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

### update_artifact

```
update_artifact(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.UpdateArtifactRequest,
dict,
]
] = None,
*,
artifact: typing.Optional[
google.cloud.aiplatform_v1.types.artifact.Artifact
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.artifact.Artifact
```


Updates a stored Artifact.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_artifact():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateArtifactRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateArtifactRequest.html)(
)
# Make the request
response = await client.[update_artifact](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_update_artifact)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.UpdateArtifact. |
`artifact` |
Required. The Artifact containing updates. The Artifact's Artifact.name field is used to identify the Artifact to be updated. Format: |
`update_mask` |
Optional. A FieldMask indicating which fields should be updated. This corresponds to the |
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
Instance of a general artifact. |

### update_context

```
update_context(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.UpdateContextRequest, dict
]
] = None,
*,
context: typing.Optional[google.cloud.aiplatform_v1.types.context.Context] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.context.Context
```


Updates a stored Context.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_context():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateContextRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateContextRequest.html)(
)
# Make the request
response = await client.[update_context](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_update_context)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.UpdateContext. |
`context` |
Required. The Context containing updates. The Context's Context.name field is used to identify the Context to be updated. Format: |
`update_mask` |
Optional. A FieldMask indicating which fields should be updated. This corresponds to the |
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
Instance of a general context. |

### update_execution

```
update_execution(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.UpdateExecutionRequest,
dict,
]
] = None,
*,
execution: typing.Optional[
google.cloud.aiplatform_v1.types.execution.Execution
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.execution.Execution
```


Updates a stored Execution.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_execution():
# Create a client
client = aiplatform_v1.
```[MetadataServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateExecutionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExecutionRequest.html)(
)
# Make the request
response = await client.[update_execution](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceAsyncClient_update_execution)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for MetadataService.UpdateExecution. |
`execution` |
Required. The Execution containing updates. The Execution's Execution.name field is used to identify the Execution to be updated. Format: |
`update_mask` |
Optional. A FieldMask indicating which fields should be updated. This corresponds to the |
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
Instance of a general execution. |

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

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessresult_goog_fecda8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessresult_googl_567ba7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessresult_google_ea66fd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessresult_googlec_b73ea8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessresult_googlecl_60e53c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessresult_googleclo_527e73.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessresult_googleclou_5b3072.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringcorrectnessresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessResult -->

# Class QuestionAnsweringCorrectnessResult (1.134.0)

```
QuestionAnsweringCorrectnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Correctness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering correctness score. |
`confidence` |
`float`
Output only. Confidence for question answering correctness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringCorrectnessResult

```
QuestionAnsweringCorrectnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringhelpfulnessresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessResult -->

# Class QuestionAnsweringHelpfulnessResult (1.134.0)

```
QuestionAnsweringHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Helpfulness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering helpfulness score. |
`confidence` |
`float`
Output only. Confidence for question answering helpfulness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringHelpfulnessResult

```
QuestionAnsweringHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeaturemonitorjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsAsyncPager -->

# Class ListFeatureMonitorJobsAsyncPager (1.134.0)

```
ListFeatureMonitorJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
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


A pager for iterating through `list_feature_monitor_jobs`

requests.

This class thinly wraps an initial
[ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_monitor_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureMonitorJobs`

requests and continue to iterate
through the `feature_monitor_jobs`

field on the
corresponding responses.

All the usual [ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureMonitorJobsAsyncPager

```
ListFeatureMonitorJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesnotebook_servicepagerslistnotebookexecutio_f88b4b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesnotebook_servicepagerslistnotebookexecutionjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager -->

# Class ListNotebookExecutionJobsAsyncPager (1.134.0)

```
ListNotebookExecutionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
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


A pager for iterating through `list_notebook_execution_jobs`

requests.

This class thinly wraps an initial
[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_execution_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookExecutionJobs`

requests and continue to iterate
through the `notebook_execution_jobs`

field on the
corresponding responses.

All the usual [ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookExecutionJobsAsyncPager

```
ListNotebookExecutionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmigration_servicepagerssearchmigratableresourcesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesAsyncPager -->

# Class SearchMigratableResourcesAsyncPager (1.134.0)

```
SearchMigratableResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchMigratableResourcesAsyncPager

```
SearchMigratableResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfeaturestoremonitoringconfigthresholdconfig_goog_0f62f6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeaturestoremonitoringconfigthresholdconfig_googl_d42235.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeaturestoremonitoringconfigthresholdconfig_google_71cf0b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturestoremonitoringconfigthresholdconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeaturestoreMonitoringConfig.ThresholdConfig -->

# Class ThresholdConfig (1.134.0)

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`value` |
`float`
Specify a threshold value that can trigger the alert. 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. Each feature must have a non-zero threshold if they need to be monitored. Otherwise no alert will be triggered for that feature. This field is a member of `oneof` _ `threshold` .
|

## Methods

### ThresholdConfig

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryanyordermatchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryAnyOrderMatchInstance -->

# Class TrajectoryAnyOrderMatchInstance (1.134.0)

```
TrajectoryAnyOrderMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryAnyOrderMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`predicted_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for predicted tool call trajectory. This field is a member of `oneof` _ `_predicted_trajectory` .
|
`reference_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for reference tool call trajectory. This field is a member of `oneof` _ `_reference_trajectory` .
|

## Methods

### TrajectoryAnyOrderMatchInstance

```
TrajectoryAnyOrderMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryAnyOrderMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeneratememoriesrequestvertexsessionsource_go_90be9d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratememoriesrequestvertexsessionsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.VertexSessionSource -->

# Class VertexSessionSource (1.134.0)

`VertexSessionSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines an Agent Engine Session from which to generate the memories.
If `scope`

is not provided, the scope will be extracted from the
Session (i.e. {"user_id": sesison.user_id}).

## Attributes |
|
|---|---|
Name |
Description |
`session` |
`str`
Required. The resource name of the Session to generate memories for. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}`
|
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Time range to define which session events should be used to generate memories. Start time (inclusive) of the time range. If not set, the start time is unbounded. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. End time (exclusive) of the time range. If not set, the end time is unbounded. |

## Methods

### VertexSessionSource

`VertexSessionSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines an Agent Engine Session from which to generate the memories.
If `scope`

is not provided, the scope will be extracted from the
Session (i.e. {"user_id": sesison.user_id}).


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspecmedianautomatedstoppingspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.MedianAutomatedStoppingSpec -->

# Class MedianAutomatedStoppingSpec (1.134.0)

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.

## Attribute |
|
|---|---|
Name |
Description |
`use_elapsed_duration` |
`bool`
True if median automated stopping rule applies on Measurement.elapsed_duration. It means that elapsed_duration field of latest measurement of current Trial is used to compute median objective value for each completed Trials. |

## Methods

### MedianAutomatedStoppingSpec

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagersli_d3b0ab.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagerslistfeatureonlinestorespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresPager -->

# Class ListFeatureOnlineStoresPager (1.134.0)

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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


A pager for iterating through `list_feature_online_stores`

requests.

This class thinly wraps an initial
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_online_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureOnlineStores`

requests and continue to iterate
through the `feature_online_stores`

field on the
corresponding responses.

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureOnlineStoresPager

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdeployment_resource_pool_servicepagersquerydeployedmodelsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsAsyncPager -->

# Class QueryDeployedModelsAsyncPager (1.134.0)

```
QueryDeployedModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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


A pager for iterating through `query_deployed_models`

requests.

This class thinly wraps an initial
[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`deployed_models`

field.

If there are more pages, the `__aiter__`

method will make additional
`QueryDeployedModels`

requests and continue to iterate
through the `deployed_models`

field on the
corresponding responses.

All the usual [QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### QueryDeployedModelsAsyncPager

```
QueryDeployedModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerslistmodelm_5c2d4a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerslistmodelmo_f8c7da.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerslistmodelmon_514c61.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerslistmodelmonitoringjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitoringJobsAsyncPager -->

# Class ListModelMonitoringJobsAsyncPager (1.134.0)

```
ListModelMonitoringJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
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


A pager for iterating through `list_model_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_monitoring_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelMonitoringJobs`

requests and continue to iterate
through the `model_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelMonitoringJobsAsyncPager

```
ListModelMonitoringJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeploy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.Deploy -->

# Class Deploy (1.134.0)

`Deploy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

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
`dedicated_resources` |
A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration. This field is a member of `oneof` _ `prediction_resources` .
|
`automatic_resources` |
A description of resources that to large degree are decided by Vertex AI, and require only a modest additional configuration. This field is a member of `oneof` _ `prediction_resources` .
|
`shared_resources` |
`str`
The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
This field is a member of `oneof` _ `prediction_resources` .
|
`model_display_name` |
`str`
Optional. Default model display name. |
`large_model_reference` |
Optional. Large model reference. When this is set, model_artifact_spec is not needed. |
`container_spec` |
Optional. The specification of the container that is to be used when deploying this Model in Vertex AI. Not present for Large Models. |
`artifact_uri` |
`str`
Optional. The path to the directory containing the Model artifact and any of its supporting files. |
`deploy_task_name` |
`str`
Optional. The name of the deploy task (e.g., "text to image generation"). This field is a member of `oneof` _ `_deploy_task_name` .
|
`deploy_metadata` |
Optional. Metadata information about this deployment config. This field is a member of `oneof` _ `_deploy_metadata` .
|
`title` |
`str`
Required. The title of the regional resource reference. |
`public_artifact_uri` |
`str`
Optional. The signed URI for ephemeral Cloud Storage access to model artifact. |

## Classes

### DeployMetadata

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.

## Methods

### Deploy

`Deploy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesnotebook_servicepagerslistnotebookruntimetempla_67345e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesnotebook_servicepagerslistnotebookruntimetemplatesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesAsyncPager -->

# Class ListNotebookRuntimeTemplatesAsyncPager (1.134.0)

```
ListNotebookRuntimeTemplatesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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


A pager for iterating through `list_notebook_runtime_templates`

requests.

This class thinly wraps an initial
[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_runtime_templates`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookRuntimeTemplates`

requests and continue to iterate
through the `notebook_runtime_templates`

field on the
corresponding responses.

All the usual [ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimeTemplatesAsyncPager

```
ListNotebookRuntimeTemplatesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragvectordbconfigragmanageddbann_googleclouda_362287.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragvectordbconfigragmanageddbann.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.RagManagedDb.ANN -->

# Class ANN (1.134.0)

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

## Attributes |
|
|---|---|
Name |
Description |
`tree_depth` |
`int`
The depth of the tree-based structure. Only depth values of 2 and 3 are supported. Recommended value is 2 if you have if you have O(10K) files in the RagCorpus and set this to 3 if more than that. Default value is 2. |
`leaf_count` |
`int`
Number of leaf nodes in the tree-based structure. Each leaf node contains groups of closely related vectors along with their corresponding centroid. Recommended value is 10 \* sqrt(num of RagFiles in your RagCorpus). Default value is 500. |

## Methods

### ANN

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictparams_v1typesvideoobjecttrackingpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoObjectTrackingPredictionParams -->

# Class VideoObjectTrackingPredictionParams (1.134.0)

```
VideoObjectTrackingPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Object Tracking.

## Attributes |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`float`
The Model only returns predictions with at least this confidence score. Default value is 0.0 |
`max_predictions` |
`int`
The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50. |
`min_bounding_box_size` |
`float`
Only bounding boxes with shortest edge at least that long as a relative value of video frame size are returned. Default value is 0.0. |

## Methods

### VideoObjectTrackingPredictionParams

```
VideoObjectTrackingPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Object Tracking.

### VideoObjectTrackingPredictionParams

```
VideoObjectTrackingPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Object Tracking.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesgenerationconfigroutingconfigautoroutingmode__go_a01865.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgenerationconfigroutingconfigautoroutingmode__goo_76e866.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgenerationconfigroutingconfigautoroutingmode__goog_5b3609.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgenerationconfigroutingconfigautoroutingmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig.AutoRoutingMode -->

# Class AutoRoutingMode (1.134.0)

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_routing_preference` |
The model routing preference. This field is a member of `oneof` _ `_model_routing_preference` .
|

## Classes

### ModelRoutingPreference

`ModelRoutingPreference(value)`


The model routing preference.

## Methods

### AutoRoutingMode

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstringarray_googlecloudaiplatform_v1typescome_6c48e9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstringarray.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StringArray -->

# Class StringArray (1.134.0)

`StringArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of string values.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
A list of string values. |

## Methods

### StringArray

`StringArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of string values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescometspeccometversion.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CometSpec.CometVersion -->

# Class CometVersion (1.134.0)

`CometVersion(value)`


Comet version options.

## Enums |
|
|---|---|
Name |
Description |
`COMET_VERSION_UNSPECIFIED` |
Comet version unspecified. |
`COMET_22_SRC_REF` |
Comet 22 for translation + source + reference (source-reference-combined). |

## Methods

### CometVersion

`CometVersion(value)`


Comet version options.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagerslistdeploymentresourcepoolspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsPager -->

# Class ListDeploymentResourcePoolsPager (1.134.0)

```
ListDeploymentResourcePoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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


A pager for iterating through `list_deployment_resource_pools`

requests.

This class thinly wraps an initial
[ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`deployment_resource_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDeploymentResourcePools`

requests and continue to iterate
through the `deployment_resource_pools`

field on the
corresponding responses.

All the usual [ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDeploymentResourcePoolsPager

```
ListDeploymentResourcePoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesstoredcontentsexamplesearchkeygenerationmeth_ff1d5d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstoredcontentsexamplesearchkeygenerationmetho_7674dc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstoredcontentsexamplesearchkeygenerationmethod.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExample.SearchKeyGenerationMethod -->

# Class SearchKeyGenerationMethod (1.134.0)

`SearchKeyGenerationMethod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options for generating the search key from the conversation history.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`last_entry` |
Use only the last entry of the conversation history ( `contents_example.contents` ) as the search key.
This field is a member of `oneof` _ `method` .
|

## Classes

### LastEntry

`LastEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for using only the last entry of the conversation history as the search key.

## Methods

### SearchKeyGenerationMethod

`SearchKeyGenerationMethod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options for generating the search key from the conversation history.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnotebookexecutionjobworkbenchruntime_googlecloudai_3e19be.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnotebookexecutionjobworkbenchruntime.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob.WorkbenchRuntime -->

# Class WorkbenchRuntime (1.134.0)

`WorkbenchRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a Workbench Instances-based environment.

## Methods

### WorkbenchRuntime

`WorkbenchRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a Workbench Instances-based environment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessafetyspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetySpec -->

# Class SafetySpec (1.134.0)

`SafetySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for safety metric.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### SafetySpec

`SafetySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for safety metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesassessdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest -->

# Class AssessDataRequest (1.134.0)

`AssessDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.AssessData. Used only for MULTIMODAL datasets.

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
`tuning_validation_assessment_config` |
Optional. Configuration for the tuning validation assessment. This field is a member of `oneof` _ `assessment_config` .
|
`tuning_resource_usage_assessment_config` |
Optional. Configuration for the tuning resource usage assessment. This field is a member of `oneof` _ `assessment_config` .
|
`batch_prediction_validation_assessment_config` |
Optional. Configuration for the batch prediction validation assessment. This field is a member of `oneof` _ `assessment_config` .
|
`batch_prediction_resource_usage_assessment_config` |
Optional. Configuration for the batch prediction resource usage assessment. This field is a member of `oneof` _ `assessment_config` .
|
`name` |
`str`
Required. The name of the Dataset resource. Used only for MULTIMODAL datasets. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`gemini_request_read_config` |
Optional. The Gemini request read config for the dataset. |

## Classes

### BatchPredictionResourceUsageAssessmentConfig

```
BatchPredictionResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction resource usage assessment.

### BatchPredictionValidationAssessmentConfig

```
BatchPredictionValidationAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction validation assessment.

### TuningResourceUsageAssessmentConfig

```
TuningResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the tuning resource usage assessment.

### TuningValidationAssessmentConfig

```
TuningValidationAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the tuning validation assessment.

## Methods

### AssessDataRequest

`AssessDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.AssessData. Used only for MULTIMODAL datasets.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesstudyspecmedianautomatedstoppingspec_goog_a7de97.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesstudyspecmedianautomatedstoppingspec_googl_23d1e8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesstudyspecmedianautomatedstoppingspec_google_a2f099.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesstudyspecmedianautomatedstoppingspec_googlec_221d47.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstudyspecmedianautomatedstoppingspec_googlecl_9afb66.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecmedianautomatedstoppingspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.MedianAutomatedStoppingSpec -->

# Class MedianAutomatedStoppingSpec (1.134.0)

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.

## Attribute |
|
|---|---|
Name |
Description |
`use_elapsed_duration` |
`bool`
True if median automated stopping rule applies on Measurement.elapsed_duration. It means that elapsed_duration field of latest measurement of current Trial is used to compute median objective value for each completed Trials. |

## Methods

### MedianAutomatedStoppingSpec

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfigthresholdconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig.ThresholdConfig -->

# Class ThresholdConfig (1.134.0)

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`value` |
`float`
Specify a threshold value that can trigger the alert. 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. Each feature must have a non-zero threshold if they need to be monitored. Otherwise no alert will be triggered for that feature. This field is a member of `oneof` _ `threshold` .
|

## Methods

### ThresholdConfig

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreateendpointrequest_googlecloudaiplatform_v1type_5dd47e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateendpointrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEndpointRequest -->

# Class CreateEndpointRequest (1.134.0)

`CreateEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.CreateEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the Endpoint in. Format: `projects/{project}/locations/{location}`
|
`endpoint` |
Required. The Endpoint to create. |
`endpoint_id` |
`str`
Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are `[a-z0-9-]` . The
last character must be a letter or number.
If the first character is a number, this value may be up to
9 characters, and valid characters are `[0-9]` with no
leading zeros.
When using HTTP/JSON, this field is populated based on a
query string argument, such as `?endpoint_id=12345` . This
is the fallback for fields that are not included in either
the URI or the body.
|

## Methods

### CreateEndpointRequest

`CreateEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.CreateEndpoint.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadfeaturevaluesresponseentityview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadFeatureValuesResponse.EntityView -->

# Class EntityView (1.134.0)

`EntityView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Entity view with Feature values.

## Attributes |
|
|---|---|
Name |
Description |
`entity_id` |
`str`
ID of the requested entity. |
`data` |
`MutableSequence[`
Each piece of data holds the k requested values for one requested Feature. If no values for the requested Feature exist, the corresponding cell will be empty. This has the same size and is in the same order as the features from the header ReadFeatureValuesResponse.header. |

## Classes

### Data

`Data(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Container to hold value(s), successive in time, for one Feature from the request.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### EntityView

`EntityView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Entity view with Feature values.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesjob_servicepagerslistmodeldeploymentmonito_f21431.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistmodeldeploymentmonitoringjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListModelDeploymentMonitoringJobsPager -->

# Class ListModelDeploymentMonitoringJobsPager (1.134.0)

```
ListModelDeploymentMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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


A pager for iterating through `list_model_deployment_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_deployment_monitoring_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelDeploymentMonitoringJobs`

requests and continue to iterate
through the `model_deployment_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelDeploymentMonitoringJobsPager

```
ListModelDeploymentMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdirectuploadsource_googlecloudaiplatform_v1b_50823c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdirectuploadsource_googlecloudaiplatform_v1be_45bf82.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdirectuploadsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectUploadSource -->

# Class DirectUploadSource (1.134.0)

`DirectUploadSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The input content is encapsulated and uploaded in the request.

## Methods

### DirectUploadSource

`DirectUploadSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The input content is encapsulated and uploaded in the request.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdoublearray.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DoubleArray -->

# Class DoubleArray (1.134.0)

`DoubleArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of double values.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
A list of double values. |

## Methods

### DoubleArray

`DoubleArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of double values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgenerationconfigroutingconfigautoroutingmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig.AutoRoutingMode -->

# Class AutoRoutingMode (1.134.0)

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_routing_preference` |
The model routing preference. This field is a member of `oneof` _ `_model_routing_preference` .
|

## Classes

### ModelRoutingPreference

`ModelRoutingPreference(value)`


The model routing preference.

## Methods

### AutoRoutingMode

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardt_136e5d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardti_4df7a7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardtimeseriesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesAsyncPager -->

# Class ListTensorboardTimeSeriesAsyncPager (1.134.0)

```
ListTensorboardTimeSeriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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
[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse) object, and
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

All the usual [ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardTimeSeriesAsyncPager

```
ListTensorboardTimeSeriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslisthyperparametertuningjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListHyperparameterTuningJobsAsyncPager -->

# Class ListHyperparameterTuningJobsAsyncPager (1.134.0)

```
ListHyperparameterTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
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


A pager for iterating through `list_hyperparameter_tuning_jobs`

requests.

This class thinly wraps an initial
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`hyperparameter_tuning_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListHyperparameterTuningJobs`

requests and continue to iterate
through the `hyperparameter_tuning_jobs`

field on the
corresponding responses.

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListHyperparameterTuningJobsAsyncPager

```
ListHyperparameterTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicestensorboard_servicepagersexporttensorboard_e0166e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicepagersexporttensorboardtimeseriesdatapager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ExportTensorboardTimeSeriesDataPager -->

# Class ExportTensorboardTimeSeriesDataPager (1.134.0)

```
ExportTensorboardTimeSeriesDataPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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
[ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataResponse) object, and
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

All the usual [ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ExportTensorboardTimeSeriesDataPager

```
ExportTensorboardTimeSeriesDataPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodeldeploymentmonitoringscheduleconfig_googleclou_151e41.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodeldeploymentmonitoringscheduleconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringScheduleConfig -->

# Class ModelDeploymentMonitoringScheduleConfig (1.134.0)

```
ModelDeploymentMonitoringScheduleConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for scheduling monitoring job.

## Attributes |
|
|---|---|
Name |
Description |
`monitor_interval` |
`google.protobuf.duration_pb2.Duration`
Required. The model monitoring job scheduling interval. It will be rounded up to next full hour. This defines how often the monitoring jobs are triggered. |
`monitor_window` |
`google.protobuf.duration_pb2.Duration`
The time window of the prediction data being included in each prediction dataset. This window specifies how long the data should be collected from historical model results for each run. If not set, ModelDeploymentMonitoringScheduleConfig.monitor_interval will be used. e.g. If currently the cutoff time is 2022-01-08 14:30:00 and the monitor_window is set to be 3600, then data from 2022-01-08 13:30:00 to 2022-01-08 14:30:00 will be retrieved and aggregated to calculate the monitoring statistics. |

## Methods

### ModelDeploymentMonitoringScheduleConfig

```
ModelDeploymentMonitoringScheduleConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for scheduling monitoring job.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstreamdirectrawpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamDirectRawPredictRequest -->

# Class StreamDirectRawPredictRequest (1.134.0)

```
StreamDirectRawPredictRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PredictionService.StreamDirectRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`method_name` |
`str`
Optional. Fully qualified name of the API method being invoked to perform predictions. Format: `/namespace.Service/Method/` Example:
`/tensorflow.serving.PredictionService/Predict`
|
`input` |
`bytes`
Optional. The prediction input. |

## Methods

### StreamDirectRawPredictRequest

```
StreamDirectRawPredictRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PredictionService.StreamDirectRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typestrajectory_googlecloudaiplatform_v1beta1t_0d67d0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typestrajectory_googlecloudaiplatform_v1beta1ty_c8551b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typestrajectory_googlecloudaiplatform_v1beta1typ_e1e088.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typestrajectory_googlecloudaiplatform_v1beta1type_6eb9d9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestrajectory_googlecloudaiplatform_v1beta1types_766ec7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectory.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Trajectory -->

# Class Trajectory (1.134.0)

`Trajectory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for trajectory.

## Attribute |
|
|---|---|
Name |
Description |
`tool_calls` |
`MutableSequence[`
Required. Tool calls in the trajectory. |

## Methods

### Trajectory

`Trajectory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for trajectory.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookexecutionjobworkbenchruntime.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.WorkbenchRuntime -->

# Class WorkbenchRuntime (1.134.0)

`WorkbenchRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a Workbench Instances-based environment.

## Methods

### WorkbenchRuntime

`WorkbenchRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for a Workbench Instances-based environment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatemetadataschemarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMetadataSchemaRequest -->

# Class CreateMetadataSchemaRequest (1.134.0)

`CreateMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataSchema.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the MetadataSchema should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`metadata_schema` |
Required. The MetadataSchema to create. |
`metadata_schema_id` |
`str`
The {metadata_schema} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/metadataSchemas/{metadataschema}`
If not provided, the MetadataStore's ID will be a UUID
generated by the service. Must be 4-128 characters in
length. Valid characters are `/` a-z][0-9]`-/` . Must be
unique across all MetadataSchemas in the parent Location.
(Otherwise the request will fail with ALREADY_EXISTS, or
PERMISSION_DENIED if the caller can't view the preexisting
MetadataSchema.)
|

## Methods

### CreateMetadataSchemaRequest

`CreateMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateMetadataSchema.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesthresholdconfig__googlecloudaiplatform_v1beta1type_7f6293.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesthresholdconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ThresholdConfig -->

# Class ThresholdConfig (1.134.0)

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for feature monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`value` |
`float`
Specify a threshold value that can trigger the alert. If this threshold config is for feature distribution distance: 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. Each feature must have a non-zero threshold if they need to be monitored. Otherwise no alert will be triggered for that feature. This field is a member of `oneof` _ `threshold` .
|

## Methods

### ThresholdConfig

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for feature monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessupervisedtuningspectuningmode_googlecloudaip_530001.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessupervisedtuningspectuningmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SupervisedTuningSpec.TuningMode -->

# Class TuningMode (1.134.0)

`TuningMode(value)`


Supported tuning modes.

## Enums |
|
|---|---|
Name |
Description |
`TUNING_MODE_UNSPECIFIED` |
Tuning mode is unspecified. |
`TUNING_MODE_FULL` |
Full fine-tuning mode. |
`TUNING_MODE_PEFT_ADAPTER` |
PEFT adapter tuning mode. |

## Methods

### TuningMode

`TuningMode(value)`


Supported tuning modes.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfluencyspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FluencySpec -->

# Class FluencySpec (1.134.0)

`FluencySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fluency score metric.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### FluencySpec

`FluencySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fluency score metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespipeline_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.pipeline_service.pagers`

module.

## Classes

[ListPipelineJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager)

```
ListPipelineJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse,
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


A pager for iterating through `list_pipeline_jobs`

requests.

This class thinly wraps an initial
[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`pipeline_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPipelineJobs`

requests and continue to iterate
through the `pipeline_jobs`

field on the
corresponding responses.

All the usual [ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListPipelineJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListPipelineJobsPager)

```
ListPipelineJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListPipelineJobsResponse,
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


A pager for iterating through `list_pipeline_jobs`

requests.

This class thinly wraps an initial
[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`pipeline_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPipelineJobs`

requests and continue to iterate
through the `pipeline_jobs`

field on the
corresponding responses.

All the usual [ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrainingPipelinesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesAsyncPager)

```
ListTrainingPipelinesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse,
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


A pager for iterating through `list_training_pipelines`

requests.

This class thinly wraps an initial
[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse) object, and
provides an `__aiter__`

method to iterate through its
`training_pipelines`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTrainingPipelines`

requests and continue to iterate
through the `training_pipelines`

field on the
corresponding responses.

All the usual [ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrainingPipelinesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesPager)

```
ListTrainingPipelinesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse,
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


A pager for iterating through `list_training_pipelines`

requests.

This class thinly wraps an initial
[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse) object, and
provides an `__iter__`

method to iterate through its
`training_pipelines`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTrainingPipelines`

requests and continue to iterate
through the `training_pipelines`

field on the
corresponding responses.

All the usual [ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesmergeversionaliasesrequest_googlecloudaipla_8f0451.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmergeversionaliasesrequest_googlecloudaiplat_0c607e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmergeversionaliasesrequest_googlecloudaiplatf_63b2f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmergeversionaliasesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MergeVersionAliasesRequest -->

# Class MergeVersionAliasesRequest (1.134.0)

`MergeVersionAliasesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.MergeVersionAliases.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the model version to merge aliases, with a version ID explicitly included. Example: `projects/{project}/locations/{location}/models/{model}@1234`
|
`version_aliases` |
`MutableSequence[str]`
Required. The set of version aliases to merge. The alias should be at most 128 characters, and match `` `a-z][a-zA-Z0-9-]` {0,126}[a-z-0-9]``. Add the ` `-` ` prefix
to an alias means removing that alias from the version.
`-` is NOT counted in the 128 characters. Example:
`-golden` means removing the `golden` alias from the
version.
There is NO ordering in aliases, which means
1) The aliases returned from GetModel API might not have the
exactly same order from this MergeVersionAliases API. 2)
Adding and deleting the same alias in the request is not
recommended, and the 2 operations will be cancelled out.
|

## Methods

### MergeVersionAliasesRequest

`MergeVersionAliasesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.MergeVersionAliases.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesthresholdconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ThresholdConfig -->

# Class ThresholdConfig (1.134.0)

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for feature monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`value` |
`float`
Specify a threshold value that can trigger the alert. If this threshold config is for feature distribution distance: 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. Each feature must have a non-zero threshold if they need to be monitored. Otherwise no alert will be triggered for that feature. This field is a member of `oneof` _ `threshold` .
|

## Methods

### ThresholdConfig

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for feature monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardexperimentsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardExperimentsAsyncPager -->

# Class ListTensorboardExperimentsAsyncPager (1.134.0)

```
ListTensorboardExperimentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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
[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse) object, and
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

All the usual [ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardExperimentsAsyncPager

```
ListTensorboardExperimentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessmoothgradconfig___googlecloudaiplatform_v1beta1ty_5ed4dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessmoothgradconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SmoothGradConfig -->

# Class SmoothGradConfig (1.134.0)

`SmoothGradConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details:

[https://arxiv.org/pdf/1706.03825.pdf](https://arxiv.org/pdf/1706.03825.pdf)

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
`noise_sigma` |
`float`
This is a single float value and will be used to add noise to all the features. Use this field when all features are normalized to have the same distribution: scale to range [0, 1], [-1, 1] or z-scoring, where features are normalized to have 0-mean and 1-variance. Learn more about `normalization ` __.
For best results the recommended value is about 10% - 20% of
the standard deviation of the input feature. Refer to
section 3.2 of the SmoothGrad paper:
https://arxiv.org/pdf/1706.03825.pdf. Defaults to 0.1.
If the distribution is different per feature, set
feature_noise_sigma
instead for each feature.
This field is a member of `oneof` _ `GradientNoiseSigma` .
|
`feature_noise_sigma` |
This is similar to noise_sigma, but provides additional flexibility. A separate noise sigma can be provided for each feature, which is useful if their distributions are different. No noise is added to features that are not set. If this field is unset, noise_sigma will be used for all features. This field is a member of `oneof` _ `GradientNoiseSigma` .
|
`noisy_sample_count` |
`int`
The number of gradient samples to use for approximation. The higher this number, the more accurate the gradient is, but the runtime complexity increases by this factor as well. Valid range of its value is [1, 50]. Defaults to 3. |

## Methods

### SmoothGradConfig

`SmoothGradConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details:

[https://arxiv.org/pdf/1706.03825.pdf](https://arxiv.org/pdf/1706.03825.pdf)

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesbleuresults_googlecloudaiplatform_v1beta1typ_99ccac.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbleuresults_googlecloudaiplatform_v1beta1type_7690be.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbleuresults.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BleuResults -->

# Class BleuResults (1.134.0)

`BleuResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for bleu metric.

## Attribute |
|
|---|---|
Name |
Description |
`bleu_metric_values` |
`MutableSequence[`
Output only. Bleu metric values. |

## Methods

### BleuResults

`BleuResults(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Results for bleu metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesscalar.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Scalar -->

# Class Scalar (1.134.0)

`Scalar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One point viewable on a scalar metric plot.

## Attribute |
|
|---|---|
Name |
Description |
`value` |
`float`
Value of the point at this step / timestamp. |

## Methods

### Scalar

`Scalar(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One point viewable on a scalar metric plot.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfluencyspec_googlecloudaiplatform_v1typescsvs_dd4e63.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfluencyspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FluencySpec -->

# Class FluencySpec (1.134.0)

`FluencySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fluency score metric.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### FluencySpec

`FluencySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for fluency score metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescsvsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CsvSource -->

# Class CsvSource (1.134.0)

`CsvSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for CSV input content.

## Attribute |
|
|---|---|
Name |
Description |
`gcs_source` |
Required. Google Cloud Storage location. |

## Methods

### CsvSource

`CsvSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The storage details for CSV input content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_servicetensorboardserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient -->

# Class TensorboardServiceClient (1.134.0)

```
TensorboardServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.tensorboard_service.transports.base.TensorboardServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.tensorboard_service.transports.base.TensorboardServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


TensorboardService

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
`TensorboardServiceTransport` |
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

### TensorboardServiceClient

```
TensorboardServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.tensorboard_service.transports.base.TensorboardServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.tensorboard_service.transports.base.TensorboardServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the tensorboard service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,TensorboardServiceTransport,Callable[..., TensorboardServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the TensorboardServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_create_tensorboard_runs

```
batch_create_tensorboard_runs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.BatchCreateTensorboardRunsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.tensorboard_service.CreateTensorboardRunRequest
]
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
google.cloud.aiplatform_v1.types.tensorboard_service.BatchCreateTensorboardRunsResponse
)
```


Batch create TensorboardRuns.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_create_tensorboard_runs():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1.[CreateTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardRunRequest.html)()
requests.parent = "parent_value"
requests.tensorboard_run.display_name = "display_name_value"
requests.tensorboard_run_id = "tensorboard_run_id_value"
request = aiplatform_v1.[BatchCreateTensorboardRunsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateTensorboardRunsRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
response = client.[batch_create_tensorboard_runs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_batch_create_tensorboard_runs)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.BatchCreateTensorboardRuns. |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to create the TensorboardRuns in. Format: |
`requests` |
`MutableSequence[`
Required. The request message specifying the TensorboardRuns to create. A maximum of 1000 TensorboardRuns can be created in a batch. This corresponds to the |
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
Response message for TensorboardService.BatchCreateTensorboardRuns. |

### batch_create_tensorboard_time_series

```
batch_create_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.BatchCreateTensorboardTimeSeriesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.tensorboard_service.CreateTensorboardTimeSeriesRequest
]
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
google.cloud.aiplatform_v1.types.tensorboard_service.BatchCreateTensorboardTimeSeriesResponse
)
```


Batch create TensorboardTimeSeries that belong to a TensorboardExperiment.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_create_tensorboard_time_series():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1.[CreateTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardTimeSeriesRequest.html)()
requests.parent = "parent_value"
requests.tensorboard_time_series.display_name = "display_name_value"
requests.tensorboard_time_series.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1.[BatchCreateTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateTensorboardTimeSeriesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
response = client.[batch_create_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_batch_create_tensorboard_time_series)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.BatchCreateTensorboardTimeSeries. |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to create the TensorboardTimeSeries in. Format: |
`requests` |
`MutableSequence[`
Required. The request message specifying the TensorboardTimeSeries to create. A maximum of 1000 TensorboardTimeSeries can be created in a batch. This corresponds to the |
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
Response message for TensorboardService.BatchCreateTensorboardTimeSeries. |

### batch_read_tensorboard_time_series_data

```
batch_read_tensorboard_time_series_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.BatchReadTensorboardTimeSeriesDataRequest,
dict,
]
] = None,
*,
tensorboard: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.tensorboard_service.BatchReadTensorboardTimeSeriesDataResponse
)
```


Reads multiple TensorboardTimeSeries' data. The data point number limit is 1000 for scalars, 100 for tensors and blob references. If the number of data points stored is less than the limit, all data is returned. Otherwise, the number limit of data points is randomly selected from this time series and returned.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_read_tensorboard_time_series_data():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[BatchReadTensorboardTimeSeriesDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadTensorboardTimeSeriesDataRequest.html)(
tensorboard="tensorboard_value",
time_series=['time_series_value1', 'time_series_value2'],
)
# Make the request
response = client.[batch_read_tensorboard_time_series_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_batch_read_tensorboard_time_series_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.BatchReadTensorboardTimeSeriesData. |
`tensorboard` |
`str`
Required. The resource name of the Tensorboard containing TensorboardTimeSeries to read data from. Format: |
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
Response message for TensorboardService.BatchReadTensorboardTimeSeriesData. |

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

### create_tensorboard

```
create_tensorboard(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.CreateTensorboardRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tensorboard: typing.Optional[
google.cloud.aiplatform_v1.types.tensorboard.Tensorboard
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Creates a Tensorboard.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_tensorboard():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
tensorboard = aiplatform_v1.[Tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tensorboard.html)()
tensorboard.display_name = "display_name_value"
request = aiplatform_v1.[CreateTensorboardRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardRequest.html)(
parent="parent_value",
tensorboard=tensorboard,
)
# Make the request
operation = client.[create_tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_create_tensorboard)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.CreateTensorboard. |
`parent` |
`str`
Required. The resource name of the Location to create the Tensorboard in. Format: |
`tensorboard` |
Required. The Tensorboard to create. This corresponds to the |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### create_tensorboard_experiment

```
create_tensorboard_experiment(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.CreateTensorboardExperimentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tensorboard_experiment: typing.Optional[
google.cloud.aiplatform_v1.types.tensorboard_experiment.TensorboardExperiment
] = None,
tensorboard_experiment_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_experiment.TensorboardExperiment
```


Creates a TensorboardExperiment.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_tensorboard_experiment():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateTensorboardExperimentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardExperimentRequest.html)(
parent="parent_value",
tensorboard_experiment_id="tensorboard_experiment_id_value",
)
# Make the request
response = client.[create_tensorboard_experiment](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_create_tensorboard_experiment)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.CreateTensorboardExperiment. |
`parent` |
`str`
Required. The resource name of the Tensorboard to create the TensorboardExperiment in. Format: |
`tensorboard_experiment` |
The TensorboardExperiment to create. This corresponds to the |
`tensorboard_experiment_id` |
`str`
Required. The ID to use for the Tensorboard experiment, which becomes the final component of the Tensorboard experiment's resource name. This value should be 1-128 characters, and valid characters are |
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
A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard. |

### create_tensorboard_run

```
create_tensorboard_run(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.CreateTensorboardRunRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tensorboard_run: typing.Optional[
google.cloud.aiplatform_v1.types.tensorboard_run.TensorboardRun
] = None,
tensorboard_run_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_run.TensorboardRun
```


Creates a TensorboardRun.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_tensorboard_run():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
tensorboard_run = aiplatform_v1.[TensorboardRun](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardRun.html)()
tensorboard_run.display_name = "display_name_value"
request = aiplatform_v1.[CreateTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardRunRequest.html)(
parent="parent_value",
tensorboard_run=tensorboard_run,
tensorboard_run_id="tensorboard_run_id_value",
)
# Make the request
response = client.[create_tensorboard_run](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_create_tensorboard_run)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.CreateTensorboardRun. |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to create the TensorboardRun in. Format: |
`tensorboard_run` |
Required. The TensorboardRun to create. This corresponds to the |
`tensorboard_run_id` |
`str`
Required. The ID to use for the Tensorboard run, which becomes the final component of the Tensorboard run's resource name. This value should be 1-128 characters, and valid characters are |
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
TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc |

### create_tensorboard_time_series

```
create_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.CreateTensorboardTimeSeriesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
tensorboard_time_series: typing.Optional[
google.cloud.aiplatform_v1.types.tensorboard_time_series.TensorboardTimeSeries
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_time_series.TensorboardTimeSeries
```


Creates a TensorboardTimeSeries.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_tensorboard_time_series():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
tensorboard_time_series = aiplatform_v1.[TensorboardTimeSeries](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardTimeSeries.html)()
tensorboard_time_series.display_name = "display_name_value"
tensorboard_time_series.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1.[CreateTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTensorboardTimeSeriesRequest.html)(
parent="parent_value",
tensorboard_time_series=tensorboard_time_series,
)
# Make the request
response = client.[create_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_create_tensorboard_time_series)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.CreateTensorboardTimeSeries. |
`parent` |
`str`
Required. The resource name of the TensorboardRun to create the TensorboardTimeSeries in. Format: |
`tensorboard_time_series` |
Required. The TensorboardTimeSeries to create. This corresponds to the |
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
TensorboardTimeSeries maps to times series produced in training runs |

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

### delete_tensorboard

```
delete_tensorboard(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.DeleteTensorboardRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a Tensorboard.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_tensorboard():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTensorboardRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTensorboardRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_delete_tensorboard)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.DeleteTensorboard. |
`name` |
`str`
Required. The name of the Tensorboard to be deleted. Format: |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_tensorboard_experiment

```
delete_tensorboard_experiment(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.DeleteTensorboardExperimentRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a TensorboardExperiment.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_tensorboard_experiment():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTensorboardExperimentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTensorboardExperimentRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_tensorboard_experiment](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_delete_tensorboard_experiment)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.DeleteTensorboardExperiment. |
`name` |
`str`
Required. The name of the TensorboardExperiment to be deleted. Format: |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_tensorboard_run

```
delete_tensorboard_run(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.DeleteTensorboardRunRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a TensorboardRun.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_tensorboard_run():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTensorboardRunRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_tensorboard_run](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_delete_tensorboard_run)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.DeleteTensorboardRun. |
`name` |
`str`
Required. The name of the TensorboardRun to be deleted. Format: |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_tensorboard_time_series

```
delete_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.DeleteTensorboardTimeSeriesRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a TensorboardTimeSeries.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_tensorboard_time_series():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTensorboardTimeSeriesRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_delete_tensorboard_time_series)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.DeleteTensorboardTimeSeries. |
`name` |
`str`
Required. The name of the TensorboardTimeSeries to be deleted. Format: |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### export_tensorboard_time_series_data

```
export_tensorboard_time_series_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
dict,
]
] = None,
*,
tensorboard_time_series: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ExportTensorboardTimeSeriesDataPager
)
```


Exports a TensorboardTimeSeries' data. Data is returned in paginated responses.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_export_tensorboard_time_series_data():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ExportTensorboardTimeSeriesDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataRequest.html)(
tensorboard_time_series="tensorboard_time_series_value",
)
# Make the request
page_result = client.[export_tensorboard_time_series_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_export_tensorboard_time_series_data)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.ExportTensorboardTimeSeriesData. |
`tensorboard_time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to export data from. Format: |
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
Response message for TensorboardService.ExportTensorboardTimeSeriesData. Iterating over this object will yield results and resolve additional pages automatically. |

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
`TensorboardServiceClient` |
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
`TensorboardServiceClient` |
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
`TensorboardServiceClient` |
The constructed client. |

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

### get_tensorboard

```
get_tensorboard(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.GetTensorboardRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard.Tensorboard
```


Gets a Tensorboard.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_tensorboard():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTensorboardRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_get_tensorboard)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.GetTensorboard. |
`name` |
`str`
Required. The name of the Tensorboard resource. Format: |
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
Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects. |

### get_tensorboard_experiment

```
get_tensorboard_experiment(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.GetTensorboardExperimentRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_experiment.TensorboardExperiment
```


Gets a TensorboardExperiment.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_tensorboard_experiment():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTensorboardExperimentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardExperimentRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_tensorboard_experiment](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_get_tensorboard_experiment)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.GetTensorboardExperiment. |
`name` |
`str`
Required. The name of the TensorboardExperiment resource. Format: |
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
A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard. |

### get_tensorboard_run

```
get_tensorboard_run(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.GetTensorboardRunRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_run.TensorboardRun
```


Gets a TensorboardRun.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_tensorboard_run():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardRunRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_tensorboard_run](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_get_tensorboard_run)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.GetTensorboardRun. |
`name` |
`str`
Required. The name of the TensorboardRun resource. Format: |
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
TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc |

### get_tensorboard_time_series

```
get_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.GetTensorboardTimeSeriesRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_time_series.TensorboardTimeSeries
```


Gets a TensorboardTimeSeries.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_tensorboard_time_series():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardTimeSeriesRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_get_tensorboard_time_series)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.GetTensorboardTimeSeries. |
`name` |
`str`
Required. The name of the TensorboardTimeSeries resource. Format: |
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
TensorboardTimeSeries maps to times series produced in training runs |

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

### list_tensorboard_experiments

```
list_tensorboard_experiments(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardExperimentsPager
)
```


Lists TensorboardExperiments in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_tensorboard_experiments():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTensorboardExperimentsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tensorboard_experiments](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_list_tensorboard_experiments)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.ListTensorboardExperiments. |
`parent` |
`str`
Required. The resource name of the Tensorboard to list TensorboardExperiments. Format: |
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
Response message for TensorboardService.ListTensorboardExperiments. Iterating over this object will yield results and resolve additional pages automatically. |

### list_tensorboard_runs

```
list_tensorboard_runs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardRunsPager
)
```


Lists TensorboardRuns in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_tensorboard_runs():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTensorboardRunsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tensorboard_runs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_list_tensorboard_runs)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.ListTensorboardRuns. |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to list TensorboardRuns. Format: |
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
Response message for TensorboardService.ListTensorboardRuns. Iterating over this object will yield results and resolve additional pages automatically. |

### list_tensorboard_time_series

```
list_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesPager
)
```


Lists TensorboardTimeSeries in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_tensorboard_time_series():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_list_tensorboard_time_series)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.ListTensorboardTimeSeries. |
`parent` |
`str`
Required. The resource name of the TensorboardRun to list TensorboardTimeSeries. Format: |
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
Response message for TensorboardService.ListTensorboardTimeSeries. Iterating over this object will yield results and resolve additional pages automatically. |

### list_tensorboards

```
list_tensorboards(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardsPager
)
```


Lists Tensorboards in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_tensorboards():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListTensorboardsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_tensorboards](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_list_tensorboards)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.ListTensorboards. |
`parent` |
`str`
Required. The resource name of the Location to list Tensorboards. Format: |
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
Response message for TensorboardService.ListTensorboards. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_tensorboard_experiment_path

`parse_tensorboard_experiment_path(path: str) -> typing.Dict[str, str]`


Parses a tensorboard_experiment path into its component segments.

### parse_tensorboard_path

`parse_tensorboard_path(path: str) -> typing.Dict[str, str]`


Parses a tensorboard path into its component segments.

### parse_tensorboard_run_path

`parse_tensorboard_run_path(path: str) -> typing.Dict[str, str]`


Parses a tensorboard_run path into its component segments.

### parse_tensorboard_time_series_path

`parse_tensorboard_time_series_path(path: str) -> typing.Dict[str, str]`


Parses a tensorboard_time_series path into its component segments.

### read_tensorboard_blob_data

```
read_tensorboard_blob_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.ReadTensorboardBlobDataRequest,
dict,
]
] = None,
*,
time_series: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> typing.Iterable[
google.cloud.aiplatform_v1.types.tensorboard_service.ReadTensorboardBlobDataResponse
]
```


Gets bytes of TensorboardBlobs. This is to allow reading blob data stored in consumer project's Cloud Storage bucket without users having to obtain Cloud Storage access permission.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_read_tensorboard_blob_data():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ReadTensorboardBlobDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardBlobDataRequest.html)(
time_series="time_series_value",
)
# Make the request
stream = client.[read_tensorboard_blob_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_read_tensorboard_blob_data)(request=request)
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
The request object. Request message for TensorboardService.ReadTensorboardBlobData. |
`time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to list Blobs. Format: |
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
Response message for TensorboardService.ReadTensorboardBlobData. |

### read_tensorboard_size

```
read_tensorboard_size(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.ReadTensorboardSizeRequest,
dict,
]
] = None,
*,
tensorboard: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_service.ReadTensorboardSizeResponse
```


Returns the storage size for a given TensorBoard instance.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_read_tensorboard_size():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ReadTensorboardSizeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardSizeRequest.html)(
tensorboard="tensorboard_value",
)
# Make the request
response = client.[read_tensorboard_size](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_read_tensorboard_size)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.ReadTensorboardSize. |
`tensorboard` |
`str`
Required. The name of the Tensorboard resource. Format: |
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
Response message for TensorboardService.ReadTensorboardSize. |

### read_tensorboard_time_series_data

```
read_tensorboard_time_series_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.ReadTensorboardTimeSeriesDataRequest,
dict,
]
] = None,
*,
tensorboard_time_series: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.tensorboard_service.ReadTensorboardTimeSeriesDataResponse
)
```


Reads a TensorboardTimeSeries' data. By default, if the number of data points stored is less than 1000, all data is returned. Otherwise, 1000 data points is randomly selected from this time series and returned. This value can be changed by changing max_data_points, which can't be greater than 10k.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_read_tensorboard_time_series_data():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ReadTensorboardTimeSeriesDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardTimeSeriesDataRequest.html)(
tensorboard_time_series="tensorboard_time_series_value",
)
# Make the request
response = client.[read_tensorboard_time_series_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_read_tensorboard_time_series_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.ReadTensorboardTimeSeriesData. |
`tensorboard_time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to read data from. Format: |
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
Response message for TensorboardService.ReadTensorboardTimeSeriesData. |

### read_tensorboard_usage

```
read_tensorboard_usage(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.ReadTensorboardUsageRequest,
dict,
]
] = None,
*,
tensorboard: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_service.ReadTensorboardUsageResponse
```


Returns a list of monthly active users for a given TensorBoard instance.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_read_tensorboard_usage():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ReadTensorboardUsageRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageRequest.html)(
tensorboard="tensorboard_value",
)
# Make the request
response = client.[read_tensorboard_usage](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_read_tensorboard_usage)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.ReadTensorboardUsage. |
`tensorboard` |
`str`
Required. The name of the Tensorboard resource. Format: |
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
Response message for TensorboardService.ReadTensorboardUsage. |

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

### tensorboard_experiment_path

```
tensorboard_experiment_path(
project: str, location: str, tensorboard: str, experiment: str
) -> str
```


Returns a fully-qualified tensorboard_experiment string.

### tensorboard_path

`tensorboard_path(project: str, location: str, tensorboard: str) -> str`


Returns a fully-qualified tensorboard string.

### tensorboard_run_path

```
tensorboard_run_path(
project: str, location: str, tensorboard: str, experiment: str, run: str
) -> str
```


Returns a fully-qualified tensorboard_run string.

### tensorboard_time_series_path

```
tensorboard_time_series_path(
project: str,
location: str,
tensorboard: str,
experiment: str,
run: str,
time_series: str,
) -> str
```


Returns a fully-qualified tensorboard_time_series string.

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

### update_tensorboard

```
update_tensorboard(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.UpdateTensorboardRequest,
dict,
]
] = None,
*,
tensorboard: typing.Optional[
google.cloud.aiplatform_v1.types.tensorboard.Tensorboard
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Updates a Tensorboard.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_tensorboard():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
tensorboard = aiplatform_v1.[Tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tensorboard.html)()
tensorboard.display_name = "display_name_value"
request = aiplatform_v1.[UpdateTensorboardRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardRequest.html)(
tensorboard=tensorboard,
)
# Make the request
operation = client.[update_tensorboard](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_update_tensorboard)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.UpdateTensorboard. |
`tensorboard` |
Required. The Tensorboard's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the Tensorboard resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. This corresponds to the |
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
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### update_tensorboard_experiment

```
update_tensorboard_experiment(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.UpdateTensorboardExperimentRequest,
dict,
]
] = None,
*,
tensorboard_experiment: typing.Optional[
google.cloud.aiplatform_v1.types.tensorboard_experiment.TensorboardExperiment
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_experiment.TensorboardExperiment
```


Updates a TensorboardExperiment.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_tensorboard_experiment():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateTensorboardExperimentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardExperimentRequest.html)(
)
# Make the request
response = client.[update_tensorboard_experiment](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_update_tensorboard_experiment)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.UpdateTensorboardExperiment. |
`tensorboard_experiment` |
Required. The TensorboardExperiment's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardExperiment resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. This corresponds to the |
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
A TensorboardExperiment is a group of TensorboardRuns, that are typically the results of a training job run, in a Tensorboard. |

### update_tensorboard_run

```
update_tensorboard_run(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.UpdateTensorboardRunRequest,
dict,
]
] = None,
*,
tensorboard_run: typing.Optional[
google.cloud.aiplatform_v1.types.tensorboard_run.TensorboardRun
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_run.TensorboardRun
```


Updates a TensorboardRun.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_tensorboard_run():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
tensorboard_run = aiplatform_v1.[TensorboardRun](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardRun.html)()
tensorboard_run.display_name = "display_name_value"
request = aiplatform_v1.[UpdateTensorboardRunRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardRunRequest.html)(
tensorboard_run=tensorboard_run,
)
# Make the request
response = client.[update_tensorboard_run](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_update_tensorboard_run)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.UpdateTensorboardRun. |
`tensorboard_run` |
Required. The TensorboardRun's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardRun resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. This corresponds to the |
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
TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc |

### update_tensorboard_time_series

```
update_tensorboard_time_series(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.UpdateTensorboardTimeSeriesRequest,
dict,
]
] = None,
*,
tensorboard_time_series: typing.Optional[
google.cloud.aiplatform_v1.types.tensorboard_time_series.TensorboardTimeSeries
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.tensorboard_time_series.TensorboardTimeSeries
```


Updates a TensorboardTimeSeries.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_tensorboard_time_series():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
tensorboard_time_series = aiplatform_v1.[TensorboardTimeSeries](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardTimeSeries.html)()
tensorboard_time_series.display_name = "display_name_value"
tensorboard_time_series.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1.[UpdateTensorboardTimeSeriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardTimeSeriesRequest.html)(
tensorboard_time_series=tensorboard_time_series,
)
# Make the request
response = client.[update_tensorboard_time_series](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_update_tensorboard_time_series)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.UpdateTensorboardTimeSeries. |
`tensorboard_time_series` |
Required. The TensorboardTimeSeries' |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardTimeSeries resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. This corresponds to the |
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
TensorboardTimeSeries maps to times series produced in training runs |

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

### write_tensorboard_experiment_data

```
write_tensorboard_experiment_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.WriteTensorboardExperimentDataRequest,
dict,
]
] = None,
*,
tensorboard_experiment: typing.Optional[str] = None,
write_run_data_requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.tensorboard_service.WriteTensorboardRunDataRequest
]
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
google.cloud.aiplatform_v1.types.tensorboard_service.WriteTensorboardExperimentDataResponse
)
```


Write time series data points of multiple TensorboardTimeSeries in multiple TensorboardRun's. If any data fail to be ingested, an error is returned.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_write_tensorboard_experiment_data():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
write_run_data_requests = aiplatform_v1.[WriteTensorboardRunDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteTensorboardRunDataRequest.html)()
write_run_data_requests.tensorboard_run = "tensorboard_run_value"
write_run_data_requests.time_series_data.tensorboard_time_series_id = "tensorboard_time_series_id_value"
write_run_data_requests.time_series_data.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1.[WriteTensorboardExperimentDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteTensorboardExperimentDataRequest.html)(
tensorboard_experiment="tensorboard_experiment_value",
write_run_data_requests=write_run_data_requests,
)
# Make the request
response = client.[write_tensorboard_experiment_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_write_tensorboard_experiment_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.WriteTensorboardExperimentData. |
`tensorboard_experiment` |
`str`
Required. The resource name of the TensorboardExperiment to write data to. Format: |
`write_run_data_requests` |
`MutableSequence[`
Required. Requests containing per-run TensorboardTimeSeries data to write. This corresponds to the |
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
Response message for TensorboardService.WriteTensorboardExperimentData. |

### write_tensorboard_run_data

```
write_tensorboard_run_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.tensorboard_service.WriteTensorboardRunDataRequest,
dict,
]
] = None,
*,
tensorboard_run: typing.Optional[str] = None,
time_series_data: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.tensorboard_data.TimeSeriesData
]
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
google.cloud.aiplatform_v1.types.tensorboard_service.WriteTensorboardRunDataResponse
)
```


Write time series data points into multiple TensorboardTimeSeries under a TensorboardRun. If any data fail to be ingested, an error is returned.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_write_tensorboard_run_data():
# Create a client
client = aiplatform_v1.
```[TensorboardServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html)()
# Initialize request argument(s)
time_series_data = aiplatform_v1.[TimeSeriesData](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TimeSeriesData.html)()
time_series_data.tensorboard_time_series_id = "tensorboard_time_series_id_value"
time_series_data.value_type = "BLOB_SEQUENCE"
request = aiplatform_v1.[WriteTensorboardRunDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteTensorboardRunDataRequest.html)(
tensorboard_run="tensorboard_run_value",
time_series_data=time_series_data,
)
# Make the request
response = client.[write_tensorboard_run_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient.html#google_cloud_aiplatform_v1_services_tensorboard_service_TensorboardServiceClient_write_tensorboard_run_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for TensorboardService.WriteTensorboardRunData. |
`tensorboard_run` |
`str`
Required. The resource name of the TensorboardRun to write data to. Format: |
`time_series_data` |
`MutableSequence[`
Required. The TensorboardTimeSeries data to write. Values with in a time series are indexed by their step value. Repeated writes to the same step will overwrite the existing value for that step. The upper limit of data points per write request is 5000. This corresponds to the |
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
Response message for TensorboardService.WriteTensorboardRunData. |
