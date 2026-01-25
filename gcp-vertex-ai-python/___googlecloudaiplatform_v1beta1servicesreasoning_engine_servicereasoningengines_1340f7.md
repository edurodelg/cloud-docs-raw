---
merged_at: 2026-01-25T21:47:44.361856
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesreasoning_engine_servicereasoningenginese_eb45cf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesreasoning_engine_servicereasoningengineser_cf4c32.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesreasoning_engine_servicereasoningengineserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient -->

# Class ReasoningEngineServiceAsyncClient (1.134.0)

```
ReasoningEngineServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's Reasoning Engines.

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
`ReasoningEngineServiceTransport` |
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

### ReasoningEngineServiceAsyncClient

```
ReasoningEngineServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the reasoning engine service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ReasoningEngineServiceTransport,Callable[..., ReasoningEngineServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ReasoningEngineServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_reasoning_engine

```
create_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.CreateReasoningEngineRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
reasoning_engine: typing.Optional[
google.cloud.aiplatform_v1beta1.types.reasoning_engine.ReasoningEngine
] = None,
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


Creates a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
reasoning_engine = aiplatform_v1beta1.[ReasoningEngine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngine.html)()
reasoning_engine.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateReasoningEngineRequest.html)(
parent="parent_value",
reasoning_engine=reasoning_engine,
)
# Make the request
operation = client.[create_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_create_reasoning_engine)(request=request)
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
The request object. Request message for ReasoningEngineService.CreateReasoningEngine. |
`parent` |
Required. The resource name of the Location to create the ReasoningEngine in. Format: |
`reasoning_engine` |
Required. The ReasoningEngine to create. This corresponds to the |
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

### delete_reasoning_engine

```
delete_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.DeleteReasoningEngineRequest,
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


Deletes a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_delete_reasoning_engine)(request=request)
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
The request object. Request message for ReasoningEngineService.DeleteReasoningEngine. |
`name` |
Required. The name of the ReasoningEngine resource to be deleted. Format: |
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
`ReasoningEngineServiceAsyncClient` |
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
`ReasoningEngineServiceAsyncClient` |
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
`ReasoningEngineServiceAsyncClient` |
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

### get_reasoning_engine

```
get_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.GetReasoningEngineRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.reasoning_engine.ReasoningEngine
```


Gets a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_get_reasoning_engine)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ReasoningEngineService.GetReasoningEngine. |
`name` |
Required. The name of the ReasoningEngine resource. Format: |
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
ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.transports.base.ReasoningEngineServiceTransport
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

### git_repository_link_path

```
git_repository_link_path(
project: str, location: str, connection: str, git_repository_link: str
) -> str
```


Returns a fully-qualified git_repository_link string.

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

### list_reasoning_engines

```
list_reasoning_engines(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesRequest,
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
google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.pagers.ListReasoningEnginesAsyncPager
)
```


Lists reasoning engines in a location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_reasoning_engines():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListReasoningEnginesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_reasoning_engines](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_list_reasoning_engines)(request=request)
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
The request object. Request message for ReasoningEngineService.ListReasoningEngines. |
`parent` |
Required. The resource name of the Location to list the ReasoningEngines from. Format: |
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
Response message for ReasoningEngineService.ListReasoningEngines Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

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

### parse_git_repository_link_path

`parse_git_repository_link_path(path: str) -> typing.Dict[str, str]`


Parses a git_repository_link path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

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

### update_reasoning_engine

```
update_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.UpdateReasoningEngineRequest,
dict,
]
] = None,
*,
reasoning_engine: typing.Optional[
google.cloud.aiplatform_v1beta1.types.reasoning_engine.ReasoningEngine
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
) -> google.api_core.operation_async.AsyncOperation
```


Updates a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html)()
# Initialize request argument(s)
reasoning_engine = aiplatform_v1beta1.[ReasoningEngine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngine.html)()
reasoning_engine.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateReasoningEngineRequest.html)(
reasoning_engine=reasoning_engine,
)
# Make the request
operation = client.[update_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.ReasoningEngineServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_service_ReasoningEngineServiceAsyncClient_update_reasoning_engine)(request=request)
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
The request object. Request message for ReasoningEngineService.UpdateReasoningEngine. |
`reasoning_engine` |
Required. The ReasoningEngine which replaces the resource on the server. This corresponds to the |
`update_mask` |
Optional. Mask specifying which fields to update. This corresponds to the |
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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typeslistfeatureviewsresponse_googlecloudaipla_4761fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeslistfeatureviewsresponse_googlecloudaiplat_04b72b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistfeatureviewsresponse_googlecloudaiplatf_50ef51.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistfeatureviewsresponse_googlecloudaiplatfo_3457dc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistfeatureviewsresponse_googlecloudaiplatfor_bddee7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeatureviewsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse -->

# Class ListFeatureViewsResponse (1.134.0)

`ListFeatureViewsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.ListFeatureViews.

## Attributes |
|
|---|---|
Name |
Description |
`feature_views` |
`MutableSequence[`
The FeatureViews matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureViewsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureViewsResponse

`ListFeatureViewsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.ListFeatureViews.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslustremount.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LustreMount -->

# Class LustreMount (1.134.0)

`LustreMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a mount configuration for Lustre file system.

## Attributes |
|
|---|---|
Name |
Description |
`instance_ip` |
`str`
Required. IP address of the Lustre instance. |
`volume_handle` |
`str`
Required. The unique identifier of the Lustre volume. |
`filesystem` |
`str`
Required. The name of the Lustre filesystem. |
`mount_point` |
`str`
Required. Destination mount path. The Lustre file system will be mounted for the user under /mnt/lustre/ |

## Methods

### LustreMount

`LustreMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a mount configuration for Lustre file system.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfetchexamplesresponse_googlecloudaiplatform_v_c0f459.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfetchexamplesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse -->

# Class FetchExamplesResponse (1.134.0)

`FetchExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.FetchExamples.

## Attributes |
|
|---|---|
Name |
Description |
`examples` |
`MutableSequence[`
The examples in the Example Store that satisfy the metadata filters. |
`next_page_token` |
`str`
A token, which can be sent as [FetchExamplesRequest.page_token][] to retrieve the next page. Absence of this field indicates there are no subsequent pages. |

## Methods

### FetchExamplesResponse

`FetchExamplesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.FetchExamples.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstartnotebookruntimeoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeOperationMetadata -->

# Class StartNotebookRuntimeOperationMetadata (1.134.0)

```
StartNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.StartNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### StartNotebookRuntimeOperationMetadata

```
StartNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.StartNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typessuggesttrialsresponse_googlecloudaiplatformv1sche_a25b32.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessuggesttrialsresponse_googlecloudaiplatformv1schem_20a2d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessuggesttrialsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SuggestTrialsResponse -->

# Class SuggestTrialsResponse (1.134.0)

`SuggestTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.SuggestTrials.

## Attributes |
|
|---|---|
Name |
Description |
`trials` |
`MutableSequence[`
A list of Trials. |
`study_state` |
The state of the Study. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time at which the operation was started. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time at which operation processing completed. |

## Methods

### SuggestTrialsResponse

`SuggestTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.SuggestTrials.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltextextraction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtraction -->

# Class AutoMlTextExtraction (1.134.0)

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlTextExtraction

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

### AutoMlTextExtraction

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessyntheticexample_googlecloudaiplatform_v1beta1type_42ed75.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessyntheticexample.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SyntheticExample -->

# Class SyntheticExample (1.134.0)

`SyntheticExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single synthetic example, composed of multiple fields. Used for providing few-shot examples in the request and for returning generated examples in the response.

## Attribute |
|
|---|---|
Name |
Description |
`fields` |
`MutableSequence[`
Required. A list of fields that constitute an example. |

## Methods

### SyntheticExample

`SyntheticExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single synthetic example, composed of multiple fields. Used for providing few-shot examples in the request and for returning generated examples in the response.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletefeaturevaluesrequestselectentity.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesRequest.SelectEntity -->

# Class SelectEntity (1.134.0)

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select entity. If an entity id is selected, all the feature values corresponding to the entity id will be deleted, including the entityId.

## Attribute |
|
|---|---|
Name |
Description |
`entity_id_selector` |
Required. Selectors choosing feature values of which entity id to be deleted from the EntityType. |

## Methods

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Message to select entity. If an entity id is selected, all the feature values corresponding to the entity id will be deleted, including the entityId.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesmodelmonitoringanomalytabularanomaly_google_aa25ff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodelmonitoringanomalytabularanomaly_googlec_5bd1e5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringanomalytabularanomaly_googlecl_f1f003.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringanomalytabularanomaly.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAnomaly.TabularAnomaly -->

# Class TabularAnomaly (1.134.0)

`TabularAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular anomaly details.

## Attributes |
|
|---|---|
Name |
Description |
`anomaly_uri` |
`str`
Additional anomaly information. e.g. Google Cloud Storage uri. |
`summary` |
`str`
Overview of this anomaly. |
`anomaly` |
`google.protobuf.struct_pb2.Value`
Anomaly body. |
`trigger_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time the anomaly was triggered. |
`condition` |
The alert condition associated with this anomaly. |

## Methods

### TabularAnomaly

`TabularAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular anomaly details.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstartnotebookruntimerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StartNotebookRuntimeRequest -->

# Class StartNotebookRuntimeRequest (1.134.0)

`StartNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StartNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### StartNotebookRuntimeRequest

`StartNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StartNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistmetadatastoresresponse_googlecloudaiplatform_v_f27bf8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmetadatastoresresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse -->

# Class ListMetadataStoresResponse (1.134.0)

`ListMetadataStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataStores.

## Attributes |
|
|---|---|
Name |
Description |
`metadata_stores` |
`MutableSequence[`
The MetadataStores found for the Location. |
`next_page_token` |
`str`
A token, which can be sent as ListMetadataStoresRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListMetadataStoresResponse

`ListMetadataStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataStores.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletehyperparametertuningjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteHyperparameterTuningJobRequest -->

# Class DeleteHyperparameterTuningJobRequest (1.134.0)

```
DeleteHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob resource to be deleted. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### DeleteHyperparameterTuningJobRequest

```
DeleteHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteHyperparameterTuningJob.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexplanationmetadatainputmetadatafeaturevalued_67a455.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadatainputmetadatafeaturevaluedomain.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata.FeatureValueDomain -->

# Class FeatureValueDomain (1.134.0)

`FeatureValueDomain(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Domain details of the input feature value. Provides numeric information about the feature, such as its range (min, max). If the feature has been pre-processed, for example with z-scoring, then it provides information about how to recover the original feature. For example, if the input feature is an image and it has been pre-processed to obtain 0-mean and stddev = 1 values, then original_mean, and original_stddev refer to the mean and stddev of the original feature (e.g. image tensor) from which input feature (with mean = 0 and stddev = 1) was obtained.

## Attributes |
|
|---|---|
Name |
Description |
`min_value` |
`float`
The minimum permissible value for this feature. |
`max_value` |
`float`
The maximum permissible value for this feature. |
`original_mean` |
`float`
If this input feature has been normalized to a mean value of 0, the original_mean specifies the mean value of the domain prior to normalization. |
`original_stddev` |
`float`
If this input feature has been normalized to a standard deviation of 1.0, the original_stddev specifies the standard deviation of the domain prior to normalization. |

## Methods

### FeatureValueDomain

`FeatureValueDomain(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Domain details of the input feature value. Provides numeric information about the feature, such as its range (min, max). If the feature has been pre-processed, for example with z-scoring, then it provides information about how to recover the original feature. For example, if the input feature is an image and it has been pre-processed to obtain 0-mean and stddev = 1 values, then original_mean, and original_stddev refer to the mean and stddev of the original feature (e.g. image tensor) from which input feature (with mean = 0 and stddev = 1) was obtained.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslisttrainingpipelinesresponse_googlecloudaiplatfor_b338c5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisttrainingpipelinesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse -->

# Class ListTrainingPipelinesResponse (1.134.0)

```
ListTrainingPipelinesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.ListTrainingPipelines

## Attributes |
|
|---|---|
Name |
Description |
`training_pipelines` |
`MutableSequence[`
List of TrainingPipelines in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListTrainingPipelinesRequest.page_token to obtain that page. |

## Methods

### ListTrainingPipelinesResponse

```
ListTrainingPipelinesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.ListTrainingPipelines


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesaddexecutioneventsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddExecutionEventsRequest -->

# Class AddExecutionEventsRequest (1.134.0)

`AddExecutionEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddExecutionEvents.

## Attributes |
|
|---|---|
Name |
Description |
`execution` |
`str`
Required. The resource name of the Execution that the Events connect Artifacts with. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|
`events` |
`MutableSequence[`
The Events to create and add. |

## Methods

### AddExecutionEventsRequest

`AddExecutionEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddExecutionEvents.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeslistnotebookruntimesresponse_googlecloudai_4a64a0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistnotebookruntimesresponse_googlecloudaip_d540be.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistnotebookruntimesresponse_googlecloudaipl_cb18bd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistnotebookruntimesresponse_googlecloudaipla_24e3f7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistnotebookruntimesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse -->

# Class ListNotebookRuntimesResponse (1.134.0)

```
ListNotebookRuntimesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimes.

## Attributes |
|
|---|---|
Name |
Description |
`notebook_runtimes` |
`MutableSequence[`
List of NotebookRuntimes in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListNotebookRuntimesRequest.page_token to obtain that page. |

## Methods

### ListNotebookRuntimesResponse

```
ListNotebookRuntimesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimes.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltextsentiment.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextSentiment -->

# Class AutoMlTextSentiment (1.134.0)

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlTextSentiment

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

### AutoMlTextSentiment

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragretrievalconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagRetrievalConfig -->

# Class RagRetrievalConfig (1.134.0)

`RagRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the context retrieval config.

## Attributes |
|
|---|---|
Name |
Description |
`top_k` |
`int`
Optional. The number of contexts to retrieve. |
`hybrid_search` |
Optional. Config for Hybrid Search. |
`filter` |
Optional. Config for filters. |
`ranking` |
Optional. Config for ranking and reranking. |

## Classes

### Filter

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### HybridSearch

`HybridSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Hybrid Search.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Ranking

`Ranking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ranking and reranking.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RagRetrievalConfig

`RagRetrievalConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the context retrieval config.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesautoscalingmetricspec_googlecloudaiplatform_v_31cb60.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesautoscalingmetricspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AutoscalingMetricSpec -->

# Class AutoscalingMetricSpec (1.134.0)

`AutoscalingMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The metric specification that defines the target resource utilization (CPU utilization, accelerator's duty cycle, and so on) for calculating the desired replica count.

## Attributes |
|
|---|---|
Name |
Description |
`metric_name` |
`str`
Required. The resource metric name. Supported metrics: - For Online Prediction: - `aiplatform.googleapis.com/prediction/online/accelerator/duty_cycle`
- `aiplatform.googleapis.com/prediction/online/cpu/utilization`
- `aiplatform.googleapis.com/prediction/online/request_count`
|
`target` |
`int`
The target resource utilization in percentage (1% - 100%) for the given metric; once the real usage deviates from the target by a certain percentage, the machine replicas change. The default value is 60 (representing 60%) if not provided. |
`monitored_resource_labels` |
`MutableMapping[str, str]`
Optional. The Cloud Monitoring monitored resource labels as key value pairs used for metrics filtering. See Cloud Monitoring Labels https://cloud.google.com/monitoring/api/v3/metric-model#generic-label-info |

## Classes

### MonitoredResourceLabelsEntry

```
MonitoredResourceLabelsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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

### AutoscalingMetricSpec

`AutoscalingMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The metric specification that defines the target resource utilization (CPU utilization, accelerator's duty cycle, and so on) for calculating the desired replica count.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreasoningengine.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngine -->

# Class ReasoningEngine (1.134.0)

`ReasoningEngine(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The resource name of the ReasoningEngine. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`display_name` |
`str`
Required. The display name of the ReasoningEngine. |
`description` |
`str`
Optional. The description of the ReasoningEngine. |
`spec` |
Optional. Configurations of the ReasoningEngine |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ReasoningEngine was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ReasoningEngine was most recently updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`encryption_spec` |
Customer-managed encryption key spec for a ReasoningEngine. If set, this ReasoningEngine and all sub-resources of this ReasoningEngine will be secured by this key. |
`labels` |
`MutableMapping[str, str]`
Labels for the ReasoningEngine. |

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

### ReasoningEngine

`ReasoningEngine(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesstudyspecparameterspecconditionalparameterspecca_57a356.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesstudyspecparameterspecconditionalparameterspeccat_8c6f55.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstudyspecparameterspecconditionalparameterspeccate_c4ade8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspecparameterspecconditionalparameterspeccategoricalvaluecondition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.CategoricalValueCondition -->

# Class CategoricalValueCondition (1.134.0)

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
Required. Matches values of the parent parameter of 'CATEGORICAL' type. All values must exist in `categorical_value_spec` of parent parameter.
|

## Methods

### CategoricalValueCondition

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatecachedcontentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateCachedContentRequest -->

# Class UpdateCachedContentRequest (1.134.0)

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

## Attributes |
|
|---|---|
Name |
Description |
`cached_content` |
Required. The cached content to update |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The list of fields to update. |

## Methods

### UpdateCachedContentRequest

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnotebookexecutionjobgcsnotebooksource_googlec_dd9dbb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookexecutionjobgcsnotebooksource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.GcsNotebookSource -->

# Class GcsNotebookSource (1.134.0)

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`
|
`generation` |
`str`
The version of the Cloud Storage object to read. If unset, the current version of the object is read. See https://cloud.google.com/storage/docs/metadata#generation-number. |

## Methods

### GcsNotebookSource

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateendpointlongrunningrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointLongRunningRequest -->

# Class UpdateEndpointLongRunningRequest (1.134.0)

```
UpdateEndpointLongRunningRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.UpdateEndpointLongRunning.

## Attribute |
|
|---|---|
Name |
Description |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. Currently we only support updating the `client_connection_config` field, all the other fields'
update will be blocked.
|

## Methods

### UpdateEndpointLongRunningRequest

```
UpdateEndpointLongRunningRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.UpdateEndpointLongRunning.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesflexstart_googlecloudaiplatform_v1beta1types_0c47bd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesflexstart_googlecloudaiplatform_v1beta1typesd_dbed52.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesflexstart.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FlexStart -->

# Class FlexStart (1.134.0)

`FlexStart(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FlexStart is used to schedule the deployment workload on DWS resource. It contains the max duration of the deployment.

## Attribute |
|
|---|---|
Name |
Description |
`max_runtime_duration` |
`google.protobuf.duration_pb2.Duration`
The max duration of the deployment is max_runtime_duration. The deployment will be terminated after the duration. The max_runtime_duration can be set up to 7 days. |

## Methods

### FlexStart

`FlexStart(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FlexStart is used to schedule the deployment workload on DWS resource. It contains the max duration of the deployment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletehyperparametertuningjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteHyperparameterTuningJobRequest -->

# Class DeleteHyperparameterTuningJobRequest (1.134.0)

```
DeleteHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob resource to be deleted. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### DeleteHyperparameterTuningJobRequest

```
DeleteHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteHyperparameterTuningJob.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescitation_googlecloudaiplatform_v1beta1typesli_4d8c5e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescitation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Citation -->

# Class Citation (1.134.0)

`Citation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source attributions for content.

## Attributes |
|
|---|---|
Name |
Description |
`start_index` |
`int`
Output only. Start index into the content. |
`end_index` |
`int`
Output only. End index into the content. |
`uri` |
`str`
Output only. Url reference of the attribution. |
`title` |
`str`
Output only. Title of the attribution. |
`license_` |
`str`
Output only. License of the attribution. |
`publication_date` |
`google.type.date_pb2.Date`
Output only. Publication date of the attribution. |

## Methods

### Citation

`Citation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source attributions for content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistreasoningenginesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse -->

# Class ListReasoningEnginesResponse (1.134.0)

```
ListReasoningEnginesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ReasoningEngineService.ListReasoningEngines

## Attributes |
|
|---|---|
Name |
Description |
`reasoning_engines` |
`MutableSequence[`
List of ReasoningEngines in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListReasoningEnginesRequest.page_token to obtain that page. |

## Methods

### ListReasoningEnginesResponse

```
ListReasoningEnginesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ReasoningEngineService.ListReasoningEngines


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformfeature___googlecloudaiplatformv1beta1schematrainingjobd_323f58.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformfeature___googlecloudaiplatformv1beta1schematrainingjobde_ba15f0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformfeature___googlecloudaiplatformv1beta1schematrainingjobdef_841beb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformfeature.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Feature -->

# Class Feature (1.134.0)

```
Feature(
feature_name: str,
featurestore_id: typing.Optional[str] = None,
entity_type_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Managed feature resource for Vertex AI.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### entity_type_name

Full qualified resource name of the managed entityType in which this Feature is.

### featurestore_name

Full qualified resource name of the managed featurestore in which this Feature is.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### Feature

```
Feature(
feature_name: str,
featurestore_id: typing.Optional[str] = None,
entity_type_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed feature given a feature resource name or a feature ID.

Example Usage:

```
my_feature = aiplatform.Feature(
feature_name='projects/123/locations/us-central1/featurestores/my_featurestore_id/ entityTypes/my_entity_type_id/features/my_feature_id'
)
or
my_feature = aiplatform.Feature(
feature_name='my_feature_id',
featurestore_id='my_featurestore_id',
entity_type_id='my_entity_type_id',
)
```


Parameters |
|
|---|---|
Name |
Description |
`feature_name` |
`str`
Required. A fully-qualified feature resource name or a feature ID. Example: "projects/123/locations/us-central1/featurestores/my_featurestore_id/entityTypes/my_entity_type_id/features/my_feature_id" or "my_feature_id" when project and location are initialized or passed, with featurestore_id and entity_type_id passed. |
`featurestore_id` |
`str`
Optional. Featurestore ID of an existing featurestore to retrieve feature from, when feature_name is passed as Feature ID. |
`entity_type_id` |
`str`
Optional. EntityType ID of an existing entityType to retrieve feature from, when feature_name is passed as Feature ID. The EntityType must exist in the Featurestore if provided by the featurestore_id. |
`project` |
`str`
Optional. Project to retrieve feature from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve feature from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Feature. Overrides credentials set in aiplatform.init. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If only one of featurestore_id or entity_type_id is provided. |

### create

```
create(
feature_id: str,
value_type: str,
entity_type_name: str,
featurestore_id: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.feature.Feature
```


Creates a Feature resource in an EntityType.

Example Usage:

```
my_feature = aiplatform.Feature.create(
feature_id='my_feature_id',
value_type='INT64',
entity_type_name='projects/123/locations/us-central1/featurestores/my_featurestore_id/ entityTypes/my_entity_type_id'
)
or
my_feature = aiplatform.Feature.create(
feature_id='my_feature_id',
value_type='INT64',
entity_type_name='my_entity_type_id',
featurestore_id='my_featurestore_id',
)
```


### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### get_entity_type

`get_entity_type() -> google.cloud.aiplatform.featurestore.entity_type.EntityType`


Retrieves the managed entityType in which this Feature is.

### get_featurestore

```
get_featurestore() -> (
google.cloud.aiplatform.featurestore.featurestore.Featurestore
)
```


Retrieves the managed featurestore in which this Feature is.

### list

```
list(
entity_type_name: str,
featurestore_id: typing.Optional[str] = None,
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.featurestore.feature.Feature]
```


Lists existing managed feature resources in an entityType, given an entityType resource name or an entity_type ID.

Example Usage:

```
my_features = aiplatform.Feature.list(
entity_type_name='projects/123/locations/us-central1/featurestores/my_featurestore_id/ entityTypes/my_entity_type_id'
)
or
my_features = aiplatform.Feature.list(
entity_type_name='my_entity_type_id',
featurestore_id='my_featurestore_id',
)
```


Parameters |
|
|---|---|
Name |
Description |
`entity_type_name` |
`str`
Required. A fully-qualified entityType resource name or an entity_type ID of an existing entityType to list features in. The EntityType must exist in the Featurestore if provided by the featurestore_id. Example: "projects/123/locations/us-central1/featurestores/my_featurestore_id/entityTypes/my_entity_type_id" or "my_entity_type_id" when project and location are initialized or passed, with featurestore_id passed. |
`featurestore_id` |
`str`
Optional. Featurestore ID of an existing featurestore to list features in, when entity_type_name is passed as entity_type ID. |
`filter` |
`str`
Optional. Lists the Features that match the filter expression. The following filters are supported: - |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - |
`project` |
`str`
Optional. Project to list features in. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to list features in. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to list features. Overrides credentials set in aiplatform.init. |

### search

```
search(
query: typing.Optional[str] = None,
page_size: typing.Optional[int] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.featurestore.feature.Feature]
```


Searches existing managed Feature resources.

Example Usage:

```
my_features = aiplatform.Feature.search()
```


Parameters |
|
|---|---|
Name |
Description |
`query` |
`str`
Optional. Query string that is a conjunction of field-restricted queries and/or field-restricted filters. Field-restricted queries and filters can be combined using |
`page_size` |
`int`
Optional. The maximum number of Features to return. The service may return fewer than this value. If unspecified, at most 100 Features will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`project` |
`str`
Optional. Project to list features in. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to list features in. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to list features. Overrides credentials set in aiplatform.init. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.featurestore.feature.Feature
```


Updates an existing managed feature resource.

Example Usage:

```
my_feature = aiplatform.Feature(
feature_name='my_feature_id',
featurestore_id='my_featurestore_id',
entity_type_id='my_entity_type_id',
)
my_feature.update(
description='update my description',
)
```


Parameters |
|
|---|---|
Name |
Description |
`description` |
`str`
Optional. Description of the Feature. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Features. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

### wait

`wait()`


Helper method that blocks until all futures are complete.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlfore_9357f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforec_622b12.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforecastinginputstransformationnumerictransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.NumericTransformation -->

# Class NumericTransformation (1.134.0)

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

- Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


## Methods

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

- Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

- Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesundeployindexrequest_googlecloudaiplatform_v1_a6793d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesundeployindexrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployIndexRequest -->

# Class UndeployIndexRequest (1.134.0)

`UndeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UndeployIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. |

## Methods

### UndeployIndexRequest

`UndeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UndeployIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestunedmodelcheckpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TunedModelCheckpoint -->

# Class TunedModelCheckpoint (1.134.0)

`TunedModelCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModelCheckpoint for the Tuned Model of a Tuning Job.

## Attributes |
|
|---|---|
Name |
Description |
`checkpoint_id` |
`str`
The ID of the checkpoint. |
`epoch` |
`int`
The epoch of the checkpoint. |
`step` |
`int`
The step of the checkpoint. |
`endpoint` |
`str`
The Endpoint resource name that the checkpoint is deployed to. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .
|

## Methods

### TunedModelCheckpoint

`TunedModelCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModelCheckpoint for the Tuned Model of a Tuning Job.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecdeveloperconnect_47ef5e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecdeveloperconnects_f81c4b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecdeveloperconnectsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.SourceCodeSpec.DeveloperConnectSource -->

# Class DeveloperConnectSource (1.134.0)

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.

## Attribute |
|
|---|---|
Name |
Description |
`config` |
Required. The Developer Connect configuration that defines the specific repository, revision, and directory to use as the source code root. |

## Methods

### DeveloperConnectSource

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeaturestoresresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse -->

# Class ListFeaturestoresResponse (1.134.0)

`ListFeaturestoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeaturestores.

## Attributes |
|
|---|---|
Name |
Description |
`featurestores` |
`MutableSequence[`
The Featurestores matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeaturestoresRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeaturestoresResponse

`ListFeaturestoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeaturestores.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexportdataconfigexportuse_googlecloudaiplatform_v1_930d29.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportdataconfigexportuse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportDataConfig.ExportUse -->

# Class ExportUse (1.134.0)

`ExportUse(value)`


ExportUse indicates the usage of the exported files. It restricts file destination, format, annotations to be exported, whether to allow unannotated data to be exported and whether to clone files to temp Cloud Storage bucket.

## Enums |
|
|---|---|
Name |
Description |
`EXPORT_USE_UNSPECIFIED` |
Regular user export. |
`CUSTOM_CODE_TRAINING` |
Export for custom code training. |

## Methods

### ExportUse

`ExportUse(value)`


ExportUse indicates the usage of the exported files. It restricts file destination, format, annotations to be exported, whether to allow unannotated data to be exported and whether to clone files to temp Cloud Storage bucket.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodeleulaacceptance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModelEulaAcceptance -->

# Class PublisherModelEulaAcceptance (1.134.0)

```
PublisherModelEulaAcceptance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [ModelGardenService.UpdatePublisherModelEula][].

## Attributes |
|
|---|---|
Name |
Description |
`project_number` |
`int`
The project number requesting access for named model. |
`publisher_model` |
`str`
The publisher model resource name. |
`publisher_model_eula_acked` |
`bool`
The EULA content acceptance status. |

## Methods

### PublisherModelEulaAcceptance

```
PublisherModelEulaAcceptance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [ModelGardenService.UpdatePublisherModelEula][].


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesspeculativedecodingspec_googlecloudaiplatform_v1_cda5b0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesspeculativedecodingspec_googlecloudaiplatform_v1b_03f114.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesspeculativedecodingspec_googlecloudaiplatform_v1be_c7cc02.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesspeculativedecodingspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpeculativeDecodingSpec -->

# Class SpeculativeDecodingSpec (1.134.0)

`SpeculativeDecodingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Speculative Decoding.

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
`draft_model_speculation` |
draft model speculation. This field is a member of `oneof` _ `speculation` .
|
`ngram_speculation` |
N-Gram speculation. This field is a member of `oneof` _ `speculation` .
|
`speculative_token_count` |
`int`
The number of speculative tokens to generate at each step. |

## Classes

### DraftModelSpeculation

`DraftModelSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.

### NgramSpeculation

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

## Methods

### SpeculativeDecodingSpec

`SpeculativeDecodingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Speculative Decoding.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescandidate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Candidate -->

# Class Candidate (1.134.0)

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A response candidate generated from the model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`index` |
`int`
Output only. Index of the candidate. |
`content` |
Output only. Content parts of the candidate. |
`avg_logprobs` |
`float`
Output only. Average log probability score of the candidate. |
`logprobs_result` |
Output only. Log-likelihood scores for the response tokens and top tokens |
`finish_reason` |
Output only. The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens. |
`safety_ratings` |
`MutableSequence[`
Output only. List of ratings for the safety of a response candidate. There is at most one rating per category. |
`finish_message` |
`str`
Output only. Describes the reason the mode stopped generating tokens in more detail. This is only filled when `finish_reason` is set.
This field is a member of `oneof` _ `_finish_message` .
|
`citation_metadata` |
Output only. Source attribution of the generated content. |
`grounding_metadata` |
Output only. Metadata specifies sources used to ground generated content. |
`url_context_metadata` |
Output only. Metadata related to url context retrieval tool. |

## Classes

### FinishReason

`FinishReason(value)`


The reason why the model stopped generating tokens. If empty, the model has not stopped generating the tokens.

## Methods

### Candidate

`Candidate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A response candidate generated from the model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodelmonitoringinputvertexendpointlogs_googl_859a2a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringinputvertexendpointlogs_google_ef0027.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringinputvertexendpointlogs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput.VertexEndpointLogs -->

# Class VertexEndpointLogs (1.134.0)

`VertexEndpointLogs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Endpoint request response logging.

## Attribute |
|
|---|---|
Name |
Description |
`endpoints` |
`MutableSequence[str]`
List of endpoint resource names. The endpoints must enable the logging with the [Endpoint].[request_response_logging_config], and must contain the deployed model corresponding to the model version specified in [ModelMonitor].[model_monitoring_target]. |

## Methods

### VertexEndpointLogs

`VertexEndpointLogs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Endpoint request response logging.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service -->

# Package job_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.job_service`

package.

## Classes

[JobServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceAsyncClient)

A service for creating and managing Vertex AI's jobs.

[JobServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.JobServiceClient)

A service for creating and managing Vertex AI's jobs.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers)

API documentation for `aiplatform_v1beta1.services.job_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistfeaturegroupsresponse_googlecloudaiplatfo_f0530c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeaturegroupsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse -->

# Class ListFeatureGroupsResponse (1.134.0)

`ListFeatureGroupsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureGroups.

## Attributes |
|
|---|---|
Name |
Description |
`feature_groups` |
`MutableSequence[`
The FeatureGroups matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureGroupsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureGroupsResponse

`ListFeatureGroupsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureGroups.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesslacksourceslackchannelsslackchannel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SlackSource.SlackChannels.SlackChannel -->

# Class SlackChannel (1.134.0)

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.

## Attributes |
|
|---|---|
Name |
Description |
`channel_id` |
`str`
Required. The Slack channel ID. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. The starting timestamp for messages to import. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. The ending timestamp for messages to import. |

## Methods

### SlackChannel

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesprobegrpcaction_googlecloudaiplatform_v1bet_612c8c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesprobegrpcaction_googlecloudaiplatform_v1beta_535dde.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesprobegrpcaction_googlecloudaiplatform_v1beta1_30682a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesprobegrpcaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Probe.GrpcAction -->

# Class GrpcAction (1.134.0)

`GrpcAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GrpcAction checks the health of a container using a gRPC service.

## Attributes |
|
|---|---|
Name |
Description |
`port` |
`int`
Port number of the gRPC service. Number must be in the range 1 to 65535. |
`service` |
`str`
Service is the name of the service to place in the gRPC HealthCheckRequest (see https://github.com/grpc/grpc/blob/master/doc/health-checking.md). If this is not specified, the default behavior is defined by gRPC. |

## Methods

### GrpcAction

`GrpcAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GrpcAction checks the health of a container using a gRPC service.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesassignnotebookruntimeoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssignNotebookRuntimeOperationMetadata -->

# Class AssignNotebookRuntimeOperationMetadata (1.134.0)

```
AssignNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.AssignNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### AssignNotebookRuntimeOperationMetadata

```
AssignNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.AssignNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeschatcompletionsrequest_googlecloudaiplatform__0cd4e3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeschatcompletionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ChatCompletionsRequest -->

# Class ChatCompletionsRequest (1.134.0)

`ChatCompletionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.ChatCompletions]

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`http_body` |
`google.api.httpbody_pb2.HttpBody`
Optional. The prediction input. Supports HTTP headers and arbitrary data payload. |

## Methods

### ChatCompletionsRequest

`ChatCompletionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.ChatCompletions]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestunedmodelcheckpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModelCheckpoint -->

# Class TunedModelCheckpoint (1.134.0)

`TunedModelCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModelCheckpoint for the Tuned Model of a Tuning Job.

## Attributes |
|
|---|---|
Name |
Description |
`checkpoint_id` |
`str`
The ID of the checkpoint. |
`epoch` |
`int`
The epoch of the checkpoint. |
`step` |
`int`
The step of the checkpoint. |
`endpoint` |
`str`
The Endpoint resource name that the checkpoint is deployed to. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .
|

## Methods

### TunedModelCheckpoint

`TunedModelCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TunedModelCheckpoint for the Tuned Model of a Tuning Job.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesreasoning_engine_execution_service_google_ea19c3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesreasoning_engine_execution_service_googlec_62ad27.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesreasoning_engine_execution_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service -->

# Package reasoning_engine_execution_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.reasoning_engine_execution_service`

package.

## Classes

[ReasoningEngineExecutionServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient)

A service for executing queries on Reasoning Engine.

[ReasoningEngineExecutionServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceClient)

A service for executing queries on Reasoning Engine.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletetensorboardexperimentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardExperimentRequest -->

# Class DeleteTensorboardExperimentRequest (1.134.0)

```
DeleteTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardExperiment.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardExperiment to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|

## Methods

### DeleteTensorboardExperimentRequest

```
DeleteTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardExperiment.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreateendpointoperationmetadata_googlecloudai_f565e2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreateendpointoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEndpointOperationMetadata -->

# Class CreateEndpointOperationMetadata (1.134.0)

```
CreateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.CreateEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`deployment_stage` |
Output only. The deployment stage of the model. Only populated if this CreateEndpoint request deploys a model at the same time. |

## Methods

### CreateEndpointOperationMetadata

```
CreateEndpointOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.CreateEndpoint.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstreamrawpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamRawPredictRequest -->

# Class StreamRawPredictRequest (1.134.0)

`StreamRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamRawPredict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. |

## Methods

### StreamRawPredictRequest

`StreamRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamRawPredict.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesragvectordbconfigragmanageddb__googlecloudaipla_0dca86.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesragvectordbconfigragmanageddb__googlecloudaiplat_3bd46c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesragvectordbconfigragmanageddb__googlecloudaiplatf_643b8f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragvectordbconfigragmanageddb__googlecloudaiplatfo_96c21b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragvectordbconfigragmanageddb.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagVectorDbConfig.RagManagedDb -->

# Class RagManagedDb (1.134.0)

`RagManagedDb(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the default RAG-managed Vector DB.

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
`knn` |
Performs a KNN search on RagCorpus. Default choice if not specified. This field is a member of `oneof` _ `retrieval_strategy` .
|
`ann` |
Performs an ANN search on RagCorpus. Use this if you have a lot of files (> 10K) in your RagCorpus and want to reduce the search latency. This field is a member of `oneof` _ `retrieval_strategy` .
|

## Classes

### ANN

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

### KNN

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.

## Methods

### RagManagedDb

`RagManagedDb(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the default RAG-managed Vector DB.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesimportragfilesrequest_googlecloudaiplatform_v1type_f9602c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportragfilesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportRagFilesRequest -->

# Class ImportRagFilesRequest (1.134.0)

`ImportRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ImportRagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the RagCorpus resource into which to import files. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`import_rag_files_config` |
Required. The config for the RagFiles to be synced and imported into the RagCorpus. VertexRagDataService.ImportRagFiles. |

## Methods

### ImportRagFilesRequest

`ImportRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ImportRagFiles.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelversioncheckpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelVersionCheckpoint -->

# Class ModelVersionCheckpoint (1.134.0)

`ModelVersionCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A proto representation of a Spanner-stored ModelVersionCheckpoint. The meaning of the fields is equivalent to their in-Spanner counterparts.

## Attributes |
|
|---|---|
Name |
Description |
`checkpoint_id` |
`str`
The ID of the checkpoint. |
`epoch` |
`int`
The epoch of the checkpoint. |
`step` |
`int`
The step of the checkpoint. |

## Methods

### ModelVersionCheckpoint

`ModelVersionCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A proto representation of a Spanner-stored ModelVersionCheckpoint. The meaning of the fields is equivalent to their in-Spanner counterparts.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgetdatasetversionrequest_googlecloudaiplatform_v1_951850.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetdatasetversionrequest_googlecloudaiplatform_v1t_6ab0d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetdatasetversionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDatasetVersionRequest -->

# Class GetDatasetVersionRequest (1.134.0)

`GetDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDatasetVersion. Next ID: 4

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{dataset_version}`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetDatasetVersionRequest

`GetDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetDatasetVersion. Next ID: 4


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturevaluemetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValue.Metadata -->

# Class Metadata (1.134.0)

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

## Attribute |
|
|---|---|
Name |
Description |
`generate_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Feature generation timestamp. Typically, it is provided by user at feature ingestion time. If not, feature store will use the system timestamp when the data is ingested into feature store. Legacy Feature Store: For streaming ingestion, the time, aligned by days, must be no older than five years (1825 days) and no later than one year (366 days) in the future. |

## Methods

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdateindexendpointrequest_googlecloudaiplatform_v_8a125e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateindexendpointrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexEndpointRequest -->

# Class UpdateIndexEndpointRequest (1.134.0)

`UpdateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UpdateIndexEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
Required. The IndexEndpoint which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateIndexEndpointRequest

`UpdateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UpdateIndexEndpoint.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletemodelmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelMonitoringJobRequest -->

# Class DeleteModelMonitoringJobRequest (1.134.0)

```
DeleteModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.DeleteModelMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the model monitoring job to delete. Format: `projects/{project}/locations/{location}/modelMonitors/{model_monitor}/modelMonitoringJobs/{model_monitoring_job}`
|

## Methods

### DeleteModelMonitoringJobRequest

```
DeleteModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.DeleteModelMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesuseractionreference_googlecloudaiplatform_v1_29d4ad.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesuseractionreference_googlecloudaiplatform_v1b_a06f72.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesuseractionreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UserActionReference -->

# Class UserActionReference (1.134.0)

`UserActionReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


References an API call. It contains more information about long running operation and Jobs that are triggered by the API call.

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
`operation` |
`str`
For API calls that return a long running operation. Resource name of the long running operation. Format: `projects/{project}/locations/{location}/operations/{operation}`
This field is a member of `oneof` _ `reference` .
|
`data_labeling_job` |
`str`
For API calls that start a LabelingJob. Resource name of the LabelingJob. Format: `projects/{project}/locations/{location}/dataLabelingJobs/{data_labeling_job}`
This field is a member of `oneof` _ `reference` .
|
`method` |
`str`
The method name of the API RPC call. For example, "/google.cloud.aiplatform.{apiVersion}.DatasetService.CreateDataset". |

## Methods

### UserActionReference

`UserActionReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


References an API call. It contains more information about long running operation and Jobs that are triggered by the API call.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesspeculativedecodingspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpeculativeDecodingSpec -->

# Class SpeculativeDecodingSpec (1.134.0)

`SpeculativeDecodingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Speculative Decoding.

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
`draft_model_speculation` |
draft model speculation. This field is a member of `oneof` _ `speculation` .
|
`ngram_speculation` |
N-Gram speculation. This field is a member of `oneof` _ `speculation` .
|
`speculative_token_count` |
`int`
The number of speculative tokens to generate at each step. |

## Classes

### DraftModelSpeculation

`DraftModelSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.

### NgramSpeculation

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

## Methods

### SpeculativeDecodingSpec

`SpeculativeDecodingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Speculative Decoding.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesundeployindexrequest_googlecloudaiplatform_v1beta_2cf53d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesundeployindexrequest_googlecloudaiplatform_v1beta1_3804cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesundeployindexrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployIndexRequest -->

# Class UndeployIndexRequest (1.134.0)

`UndeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UndeployIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. |

## Methods

### UndeployIndexRequest

`UndeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UndeployIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginespecsourcecodespecdeveloperconnectsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.SourceCodeSpec.DeveloperConnectSource -->

# Class DeveloperConnectSource (1.134.0)

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.

## Attribute |
|
|---|---|
Name |
Description |
`config` |
Required. The Developer Connect configuration that defines the specific repository, revision, and directory to use as the source code root. |

## Methods

### DeveloperConnectSource

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesaddcontextchildrenrequest_googlecloudaiplatfo_cef6e0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesaddcontextchildrenrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextChildrenRequest -->

# Class AddContextChildrenRequest (1.134.0)

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the parent Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`child_contexts` |
`MutableSequence[str]`
The resource names of the child Contexts. |

## Methods

### AddContextChildrenRequest

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecparameterspecconditionalparameterspeccategoricalvaluecondition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.CategoricalValueCondition -->

# Class CategoricalValueCondition (1.134.0)

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
Required. Matches values of the parent parameter of 'CATEGORICAL' type. All values must exist in `categorical_value_spec` of parent parameter.
|

## Methods

### CategoricalValueCondition

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesgeneratecontentresponsepromptfeedbackblockedrea_eeebc4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesgeneratecontentresponsepromptfeedbackblockedreas_6d8e19.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgeneratecontentresponsepromptfeedbackblockedreaso_e0138d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgeneratecontentresponsepromptfeedbackblockedreason_c42814.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgeneratecontentresponsepromptfeedbackblockedreason.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentResponse.PromptFeedback.BlockedReason -->

# Class BlockedReason (1.134.0)

`BlockedReason(value)`


Blocked reason enumeration.

## Enums |
|
|---|---|
Name |
Description |
`BLOCKED_REASON_UNSPECIFIED` |
Unspecified blocked reason. |
`SAFETY` |
Candidates blocked due to safety. |
`OTHER` |
Candidates blocked due to other reason. |
`BLOCKLIST` |
Candidates blocked due to the terms which are included from the terminology blocklist. |
`PROHIBITED_CONTENT` |
Candidates blocked due to prohibited content. |
`MODEL_ARMOR` |
The user prompt was blocked by Model Armor. |
`JAILBREAK` |
The user prompt was blocked due to jailbreak. |

## Methods

### BlockedReason

`BlockedReason(value)`


Blocked reason enumeration.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeatureviewsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse -->

# Class ListFeatureViewsResponse (1.134.0)

`ListFeatureViewsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.ListFeatureViews.

## Attributes |
|
|---|---|
Name |
Description |
`feature_views` |
`MutableSequence[`
The FeatureViews matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureViewsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureViewsResponse

`ListFeatureViewsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureOnlineStoreAdminService.ListFeatureViews.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesaddexecutioneventsrequest_googlecloudaiplatform_v1_9727b5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesaddexecutioneventsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddExecutionEventsRequest -->

# Class AddExecutionEventsRequest (1.134.0)

`AddExecutionEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddExecutionEvents.

## Attributes |
|
|---|---|
Name |
Description |
`execution` |
`str`
Required. The resource name of the Execution that the Events connect Artifacts with. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|
`events` |
`MutableSequence[`
The Events to create and add. |

## Methods

### AddExecutionEventsRequest

`AddExecutionEventsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddExecutionEvents.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadatainputmetadatavisualizationoverlaytype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata.Visualization.OverlayType -->

# Class OverlayType (1.134.0)

`OverlayType(value)`


How the original image is displayed in the visualization.

## Enums |
|
|---|---|
Name |
Description |
`OVERLAY_TYPE_UNSPECIFIED` |
Default value. This is the same as NONE. |
`NONE` |
No overlay. |
`ORIGINAL` |
The attributions are shown on top of the original image. |
`GRAYSCALE` |
The attributions are shown on top of grayscaled version of the original image. |
`MASK_BLACK` |
The attributions are used as a mask to reveal predictive parts of the image and hide the un-predictive parts. |

## Methods

### OverlayType

`OverlayType(value)`


How the original image is displayed in the visualization.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragretrievalconfigranking_googlecloudaiplatform_v1_182553.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragretrievalconfigranking.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagRetrievalConfig.Ranking -->

# Class Ranking (1.134.0)

`Ranking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ranking and reranking.

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
`rank_service` |
Optional. Config for Rank Service. This field is a member of `oneof` _ `ranking_config` .
|
`llm_ranker` |
Optional. Config for LlmRanker. This field is a member of `oneof` _ `ranking_config` .
|

## Classes

### LlmRanker

`LlmRanker(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for LlmRanker.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### RankService

`RankService(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Rank Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### Ranking

`Ranking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ranking and reranking.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesvertexaisearch.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexAISearch -->

# Class VertexAISearch (1.134.0)

`VertexAISearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieve from Vertex AI Search datastore or engine for
grounding. datastore and engine are mutually exclusive. See
[https://cloud.google.com/products/agent-builder](https://cloud.google.com/products/agent-builder)

## Attributes |
|
|---|---|
Name |
Description |
`datastore` |
`str`
Optional. Fully-qualified Vertex AI Search data store resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`
|
`engine` |
`str`
Optional. Fully-qualified Vertex AI Search engine resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}`
|
`max_results` |
`int`
Optional. Number of search results to return per query. The default value is 10. The maximumm allowed value is 10. |
`filter` |
`str`
Optional. Filter strings to be passed to the search API. |
`data_store_specs` |
`MutableSequence[`
Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used. |

## Classes

### DataStoreSpec

`DataStoreSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Define data stores within engine to filter on in a search
call and configurations for those data stores. For more
information, see
[https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec](https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec)

## Methods

### VertexAISearch

`VertexAISearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieve from Vertex AI Search datastore or engine for
grounding. datastore and engine are mutually exclusive. See
[https://cloud.google.com/products/agent-builder](https://cloud.google.com/products/agent-builder)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typescancelhyperparametertuningjobrequest_google_81b0d8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescancelhyperparametertuningjobrequest_googlec_eec3d0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescancelhyperparametertuningjobrequest_googlecl_a8052e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescancelhyperparametertuningjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelHyperparameterTuningJobRequest -->

# Class CancelHyperparameterTuningJobRequest (1.134.0)

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob to cancel. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### CancelHyperparameterTuningJobRequest

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualizationoverlaytype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata.Visualization.OverlayType -->

# Class OverlayType (1.134.0)

`OverlayType(value)`


How the original image is displayed in the visualization.

## Enums |
|
|---|---|
Name |
Description |
`OVERLAY_TYPE_UNSPECIFIED` |
Default value. This is the same as NONE. |
`NONE` |
No overlay. |
`ORIGINAL` |
The attributions are shown on top of the original image. |
`GRAYSCALE` |
The attributions are shown on top of grayscaled version of the original image. |
`MASK_BLACK` |
The attributions are used as a mask to reveal predictive parts of the image and hide the un-predictive parts. |

## Methods

### OverlayType

`OverlayType(value)`


How the original image is displayed in the visualization.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespairwisequestionansweringqualityspec_googlecloudai_40cf0c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespairwisequestionansweringqualityspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseQuestionAnsweringQualitySpec -->

# Class PairwiseQuestionAnsweringQualitySpec (1.134.0)

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering quality. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### PairwiseQuestionAnsweringQualitySpec

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesinputstransformationautotransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.AutoTransformation -->

# Class AutoTransformation (1.134.0)

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

## Methods

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesindex_service_googlecloudaiplatform_v1beta1typ_db8da9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesindex_service_googlecloudaiplatform_v1beta1type_29759b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service -->

# Package index_service (1.134.0)

API documentation for `aiplatform_v1.services.index_service`

package.

## Classes

[IndexServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient)

A service for creating and managing Vertex AI's Index resources.

[IndexServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceClient)

A service for creating and managing Vertex AI's Index resources.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.pagers)

API documentation for `aiplatform_v1.services.index_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletenotebookruntimerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeRequest -->

# Class DeleteNotebookRuntimeRequest (1.134.0)

```
DeleteNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### DeleteNotebookRuntimeRequest

```
DeleteNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdateindexendpointrequest_googlecloudaiplatf_b1d52c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateindexendpointrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexEndpointRequest -->

# Class UpdateIndexEndpointRequest (1.134.0)

`UpdateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UpdateIndexEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
Required. The IndexEndpoint which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateIndexEndpointRequest

`UpdateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.UpdateIndexEndpoint.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletenotebookruntimerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeRequest -->

# Class DeleteNotebookRuntimeRequest (1.134.0)

```
DeleteNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be deleted. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### DeleteNotebookRuntimeRequest

```
DeleteNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesuseractionreference__googlecloudaiplatform_v1_e8f22c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesuseractionreference__googlecloudaiplatform_v1b_92ad5b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesuseractionreference__googlecloudaiplatform_v1be_e33c66.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesuseractionreference__googlecloudaiplatform_v1bet_328fd9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesuseractionreference__googlecloudaiplatform_v1beta_412a57.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesuseractionreference__googlecloudaiplatform_v1beta1_f67f95.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesuseractionreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UserActionReference -->

# Class UserActionReference (1.134.0)

`UserActionReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


References an API call. It contains more information about long running operation and Jobs that are triggered by the API call.

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
`operation` |
`str`
For API calls that return a long running operation. Resource name of the long running operation. Format: `projects/{project}/locations/{location}/operations/{operation}`
This field is a member of `oneof` _ `reference` .
|
`data_labeling_job` |
`str`
For API calls that start a LabelingJob. Resource name of the LabelingJob. Format: `projects/{project}/locations/{location}/dataLabelingJobs/{data_labeling_job}`
This field is a member of `oneof` _ `reference` .
|
`method` |
`str`
The method name of the API RPC call. For example, "/google.cloud.aiplatform.{apiVersion}.DatasetService.CreateDataset". |

## Methods

### UserActionReference

`UserActionReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


References an API call. It contains more information about long running operation and Jobs that are triggered by the API call.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgetmodeldeploymentmonitoringjobrequest_google_9f9271.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetmodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelDeploymentMonitoringJobRequest -->

# Class GetModelDeploymentMonitoringJobRequest (1.134.0)

```
GetModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### GetModelDeploymentMonitoringJobRequest

```
GetModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreplicatedvoiceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReplicatedVoiceConfig -->

# Class ReplicatedVoiceConfig (1.134.0)

`ReplicatedVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for the replicated voice to use.

## Attributes |
|
|---|---|
Name |
Description |
`mime_type` |
`str`
Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents
16-bit signed little-endian wav data, with a 24kHz sampling
rate. `mime_type` will default to `audio/wav` if not
set.
|
`voice_sample_audio` |
`bytes`
Optional. The sample of the custom voice. |

## Methods

### ReplicatedVoiceConfig

`ReplicatedVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for the replicated voice to use.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstoredcontentsexampleparameters__googleclouda_80f13f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstoredcontentsexampleparameters.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExampleParameters -->

# Class StoredContentsExampleParameters (1.134.0)

```
StoredContentsExampleParameters(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The metadata filters that will be used to search StoredContentsExamples. If a field is unspecified, then no filtering for that field will be applied

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
`search_key` |
`str`
The exact search key to use for retrieval. This field is a member of `oneof` _ `query` .
|
`content_search_key` |
The chat history to use to generate the search key for retrieval. This field is a member of `oneof` _ `query` .
|
`function_names` |
Optional. The function names for filtering. |

## Classes

### ContentSearchKey

`ContentSearchKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The chat history to use to generate the search key for retrieval.

## Methods

### StoredContentsExampleParameters

```
StoredContentsExampleParameters(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The metadata filters that will be used to search StoredContentsExamples. If a field is unspecified, then no filtering for that field will be applied

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestrialstate_googlecloudaiplatformv1beta1schema_6a8bb1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrialstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Trial.State -->

# Class State (1.134.0)

`State(value)`


Describes a Trial state.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
The Trial state is unspecified. |
`REQUESTED` |
Indicates that a specific Trial has been requested, but it has not yet been suggested by the service. |
`ACTIVE` |
Indicates that the Trial has been suggested. |
`STOPPING` |
Indicates that the Trial should stop according to the service. |
`SUCCEEDED` |
Indicates that the Trial is completed successfully. |
`INFEASIBLE` |
Indicates that the Trial should not be attempted again. The service will set a Trial to INFEASIBLE when it's done but missing the final_measurement. |

## Methods

### State

`State(value)`


Describes a Trial state.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforecasting.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecasting -->

# Class AutoMlForecasting (1.134.0)

`AutoMlForecasting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Forecasting Model.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |
`metadata` |
The metadata information. |

## Methods

### AutoMlForecasting

`AutoMlForecasting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Forecasting Model.

### AutoMlForecasting

`AutoMlForecasting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Forecasting Model.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesmodelexportformatexportablecontent_googlecl_51910b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodelexportformatexportablecontent_googleclo_7ce7cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelexportformatexportablecontent_googleclou_c69db3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelexportformatexportablecontent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.ExportFormat.ExportableContent -->

# Class ExportableContent (1.134.0)

`ExportableContent(value)`


The Model content that can be exported.

## Enums |
|
|---|---|
Name |
Description |
`EXPORTABLE_CONTENT_UNSPECIFIED` |
Should not be used. |
`ARTIFACT` |
Model artifact and any of its supported files. Will be exported to the location specified by the `artifactDestination` field of the ExportModelRequest.output_config object. |
`IMAGE` |
The container image that is to be used when deploying this Model. Will be exported to the location specified by the `imageDestination` field of the ExportModelRequest.output_config object. |

## Methods

### ExportableContent

`ExportableContent(value)`


The Model content that can be exported.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessecretref.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SecretRef -->

# Class SecretRef (1.134.0)

`SecretRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable.

## Attributes |
|
|---|---|
Name |
Description |
`secret` |
`str`
Required. The name of the secret in Cloud Secret Manager. Format: {secret_name}. |
`version` |
`str`
The Cloud Secret Manager secret version. Can be 'latest' for the latest version, an integer for a specific version, or a version alias. |

## Methods

### SecretRef

`SecretRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslisttensorboardrunsresponse_googlecloudaiplat_0762f3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisttensorboardrunsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse -->

# Class ListTensorboardRunsResponse (1.134.0)

`ListTensorboardRunsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboardRuns.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_runs` |
`MutableSequence[`
The TensorboardRuns mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardRunsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardRunsResponse

`ListTensorboardRunsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboardRuns.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmetadataschemasresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse -->

# Class ListMetadataSchemasResponse (1.134.0)

`ListMetadataSchemasResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataSchemas.

## Attributes |
|
|---|---|
Name |
Description |
`metadata_schemas` |
`MutableSequence[`
The MetadataSchemas found for the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListMetadataSchemasRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListMetadataSchemasResponse

`ListMetadataSchemasResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataSchemas.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfindneighborsresponseneighbor_googlecloudaip_82a555.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfindneighborsresponseneighbor_googlecloudaipl_15a925.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfindneighborsresponseneighbor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsResponse.Neighbor -->

# Class Neighbor (1.134.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Attributes |
|
|---|---|
Name |
Description |
`datapoint` |
The datapoint of the neighbor. Note that full datapoints are returned only when "return_full_datapoint" is set to true. Otherwise, only the "datapoint_id" and "crowding_tag" fields are populated. |
`distance` |
`float`
The distance between the neighbor and the dense embedding query. |
`sparse_distance` |
`float`
The distance between the neighbor and the query sparse_embedding. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelexportformatexportablecontent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model.ExportFormat.ExportableContent -->

# Class ExportableContent (1.134.0)

`ExportableContent(value)`


The Model content that can be exported.

## Enums |
|
|---|---|
Name |
Description |
`EXPORTABLE_CONTENT_UNSPECIFIED` |
Should not be used. |
`ARTIFACT` |
Model artifact and any of its supported files. Will be exported to the location specified by the `artifactDestination` field of the ExportModelRequest.output_config object. |
`IMAGE` |
The container image that is to be used when deploying this Model. Will be exported to the location specified by the `imageDestination` field of the ExportModelRequest.output_config object. |

## Methods

### ExportableContent

`ExportableContent(value)`


The Model content that can be exported.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateModelDeploymentMonitoringJobRequest -->

# Class UpdateModelDeploymentMonitoringJobRequest (1.134.0)

```
UpdateModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.UpdateModelDeploymentMonitoringJob.

## Attributes |
|
|---|---|
Name |
Description |
`model_deployment_monitoring_job` |
Required. The model monitoring configuration which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask is used to specify the fields to be overwritten in the ModelDeploymentMonitoringJob resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to
override all fields. For the objective config, the user can
either provide the update mask for
model_deployment_monitoring_objective_configs or any
combination of its nested fields, such as:
model_deployment_monitoring_objective_configs.objective_config.training_dataset.
Updatable fields:
- `display_name`
- `model_deployment_monitoring_schedule_config`
- `model_monitoring_alert_config`
- `logging_sampling_strategy`
- `labels`
- `log_ttl`
- `enable_monitoring_pipeline_logs` . and
- `model_deployment_monitoring_objective_configs` . or
- `model_deployment_monitoring_objective_configs.objective_config.training_dataset`
- `model_deployment_monitoring_objective_configs.objective_config.training_prediction_skew_detection_config`
- `model_deployment_monitoring_objective_configs.objective_config.prediction_drift_detection_config`
|

## Methods

### UpdateModelDeploymentMonitoringJobRequest

```
UpdateModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.UpdateModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typessearchmodeldeploymentmonitoringstatsanomaliesreq_1d340b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typessearchmodeldeploymentmonitoringstatsanomaliesrequ_64bf60.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessearchmodeldeploymentmonitoringstatsanomaliesreque_7b5901.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessearchmodeldeploymentmonitoringstatsanomaliesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesRequest (1.134.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.SearchModelDeploymentMonitoringStatsAnomalies.

## Attributes |
|
|---|---|
Name |
Description |
`model_deployment_monitoring_job` |
`str`
Required. ModelDeploymentMonitoring Job resource name. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|
`deployed_model_id` |
`str`
Required. The DeployedModel ID of the [ModelDeploymentMonitoringObjectiveConfig.deployed_model_id]. |
`feature_display_name` |
`str`
The feature display name. If specified, only return the stats belonging to this feature. Format: ModelMonitoringStatsAnomalies.FeatureHistoricStatsAnomalies.feature_display_name, example: "user_destination". |
`objectives` |
`MutableSequence[`
Required. Objectives of the stats to retrieve. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
A page token received from a previous JobService.SearchModelDeploymentMonitoringStatsAnomalies call. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The earliest timestamp of stats being generated. If not set, indicates fetching stats till the earliest possible one. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The latest timestamp of stats being generated. If not set, indicates feching stats till the latest possible one. |

## Classes

### StatsAnomaliesObjective

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

## Methods

### SearchModelDeploymentMonitoringStatsAnomaliesRequest

```
SearchModelDeploymentMonitoringStatsAnomaliesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.SearchModelDeploymentMonitoringStatsAnomalies.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistmetadataschemasresponse_googlecloudaiplat_146419.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmetadataschemasresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse -->

# Class ListMetadataSchemasResponse (1.134.0)

`ListMetadataSchemasResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataSchemas.

## Attributes |
|
|---|---|
Name |
Description |
`metadata_schemas` |
`MutableSequence[`
The MetadataSchemas found for the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListMetadataSchemasRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListMetadataSchemasResponse

`ListMetadataSchemasResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataSchemas.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service -->

# Package metadata_service (1.134.0)

API documentation for `aiplatform_v1.services.metadata_service`

package.

## Classes

[MetadataServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceAsyncClient)

Service for reading and writing metadata entries.

[MetadataServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient)

Service for reading and writing metadata entries.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers)

API documentation for `aiplatform_v1.services.metadata_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslisttrainingpipelinesresponse_googlecloudaip_31079a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslisttrainingpipelinesresponse_googlecloudaipl_1410d8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisttrainingpipelinesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse -->

# Class ListTrainingPipelinesResponse (1.134.0)

```
ListTrainingPipelinesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.ListTrainingPipelines

## Attributes |
|
|---|---|
Name |
Description |
`training_pipelines` |
`MutableSequence[`
List of TrainingPipelines in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListTrainingPipelinesRequest.page_token to obtain that page. |

## Methods

### ListTrainingPipelinesResponse

```
ListTrainingPipelinesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PipelineService.ListTrainingPipelines


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesslacksourceslackchannelsslackchannel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SlackSource.SlackChannels.SlackChannel -->

# Class SlackChannel (1.134.0)

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.

## Attributes |
|
|---|---|
Name |
Description |
`channel_id` |
`str`
Required. The Slack channel ID. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. The starting timestamp for messages to import. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. The ending timestamp for messages to import. |

## Methods

### SlackChannel

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslisttensorboardsresponse_googlecloudaiplatfor_a92fd0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisttensorboardsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse -->

# Class ListTensorboardsResponse (1.134.0)

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboards` |
`MutableSequence[`
The Tensorboards mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardsResponse

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforecastinginputstransformationautotransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.AutoTransformation -->

# Class AutoTransformation (1.134.0)

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

## Methods

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesvertexaisearch__googlecloudaiplatform_v1beta1type_d7b250.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesvertexaisearch__googlecloudaiplatform_v1beta1types_f8086f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesvertexaisearch.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VertexAISearch -->

# Class VertexAISearch (1.134.0)

`VertexAISearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieve from Vertex AI Search datastore or engine for
grounding. datastore and engine are mutually exclusive. See
[https://cloud.google.com/products/agent-builder](https://cloud.google.com/products/agent-builder)

## Attributes |
|
|---|---|
Name |
Description |
`datastore` |
`str`
Optional. Fully-qualified Vertex AI Search data store resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`
|
`engine` |
`str`
Optional. Fully-qualified Vertex AI Search engine resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}`
|
`max_results` |
`int`
Optional. Number of search results to return per query. The default value is 10. The maximumm allowed value is 10. |
`filter` |
`str`
Optional. Filter strings to be passed to the search API. |
`data_store_specs` |
`MutableSequence[`
Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used. |

## Classes

### DataStoreSpec

`DataStoreSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Define data stores within engine to filter on in a search
call and configurations for those data stores. For more
information, see
[https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec](https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec)

## Methods

### VertexAISearch

`VertexAISearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieve from Vertex AI Search datastore or engine for
grounding. datastore and engine are mutually exclusive. See
[https://cloud.google.com/products/agent-builder](https://cloud.google.com/products/agent-builder)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeneratememoriesrequestdirectcontentssource_g_c1bf7d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratememoriesrequestdirectcontentssource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.DirectContentsSource -->

# Class DirectContentsSource (1.134.0)

`DirectContentsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a direct source of content from which to generate the memories.

## Attribute |
|
|---|---|
Name |
Description |
`events` |
`MutableSequence[`
Required. The source content (i.e. chat history) to generate memories from. |

## Classes

### Event

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single piece of conversation from which to generate memories.

## Methods

### DirectContentsSource

`DirectContentsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a direct source of content from which to generate the memories.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesveohyperparameters.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VeoHyperParameters -->

# Class VeoHyperParameters (1.134.0)

`VeoHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Veo.

## Attributes |
|
|---|---|
Name |
Description |
`epoch_count` |
`int`
Optional. Number of complete passes the model makes over the entire training dataset during training. |
`learning_rate_multiplier` |
`float`
Optional. Multiplier for adjusting the default learning rate. |
`tuning_task` |
Optional. The tuning task. Either I2V or T2V. |

## Classes

### TuningTask

`TuningTask(value)`


An enum defining the tuning task used for Veo.

## Methods

### VeoHyperParameters

`VeoHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Veo.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragvectordbconfigragmanageddb_googlecloudaipl_ea259f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragvectordbconfigragmanageddb.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.RagManagedDb -->

# Class RagManagedDb (1.134.0)

`RagManagedDb(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the default RAG-managed Vector DB.

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
`knn` |
Performs a KNN search on RagCorpus. Default choice if not specified. This field is a member of `oneof` _ `retrieval_strategy` .
|
`ann` |
Performs an ANN search on RagCorpus. Use this if you have a lot of files (> 10K) in your RagCorpus and want to reduce the search latency. This field is a member of `oneof` _ `retrieval_strategy` .
|

## Classes

### ANN

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

### KNN

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.

## Methods

### RagManagedDb

`RagManagedDb(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the default RAG-managed Vector DB.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstransformationtexttransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.TextTransformation -->

# Class TextTransformation (1.134.0)

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.

## Methods

### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.

### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesupdatedatasetrequest_googlecloudaiplatform_v1t_014e99.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesupdatedatasetrequest_googlecloudaiplatform_v1ty_5f72ed.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesupdatedatasetrequest_googlecloudaiplatform_v1typ_b440db.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesupdatedatasetrequest_googlecloudaiplatform_v1type_23d04e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdatedatasetrequest_googlecloudaiplatform_v1types_090572.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatedatasetrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDatasetRequest -->

# Class UpdateDatasetRequest (1.134.0)

`UpdateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.UpdateDataset.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
Required. The Dataset which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
Updatable fields:
- `display_name`
- `description`
- `labels`
|

## Methods

### UpdateDatasetRequest

`UpdateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.UpdateDataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Type -->

# Class Type (1.134.0)

`Type(value)`


Type contains the list of OpenAPI data types as defined by
[https://swagger.io/docs/specification/data-models/data-types/](https://swagger.io/docs/specification/data-models/data-types/)

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Not specified, should not be used. |
`STRING` |
OpenAPI string type |
`NUMBER` |
OpenAPI number type |
`INTEGER` |
OpenAPI integer type |
`BOOLEAN` |
OpenAPI boolean type |
`ARRAY` |
OpenAPI array type |
`OBJECT` |
OpenAPI object type |

## Methods

### Type

`Type(value)`


Type contains the list of OpenAPI data types as defined by
[https://swagger.io/docs/specification/data-models/data-types/](https://swagger.io/docs/specification/data-models/data-types/)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragembeddingmodelconfighybridsearchconfig_goo_a93023.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragembeddingmodelconfighybridsearchconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagEmbeddingModelConfig.HybridSearchConfig -->

# Class HybridSearchConfig (1.134.0)

`HybridSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for hybrid search.

## Attributes |
|
|---|---|
Name |
Description |
`sparse_embedding_config` |
Optional. The configuration for sparse embedding generation. This field is optional the default behavior depends on the vector database choice on the RagCorpus. |
`dense_embedding_model_prediction_endpoint` |
Required. The Vertex AI Prediction Endpoint that hosts the embedding model for dense embedding generations. |

## Methods

### HybridSearchConfig

`HybridSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for hybrid search.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgettensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardTimeSeriesRequest -->

# Class GetTensorboardTimeSeriesRequest (1.134.0)

```
GetTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.GetTensorboardTimeSeries.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardTimeSeries resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### GetTensorboardTimeSeriesRequest

```
GetTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.GetTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplanation__googlecloudaiplatform_v1beta1typeslis_480e48.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Explanation -->

# Class Explanation (1.134.0)

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation of a prediction (provided in PredictResponse.predictions) produced by the Model on a given instance.

## Attributes |
|
|---|---|
Name |
Description |
`attributions` |
`MutableSequence[`
Output only. Feature attributions grouped by predicted outputs. For Models that predict only one output, such as regression Models that predict only one score, there is only one attibution that explains the predicted output. For Models that predict multiple outputs, such as multiclass Models that predict multiple classes, each element explains one specific item. Attribution.output_index can be used to identify which output this attribution is explaining. By default, we provide Shapley values for the predicted class. However, you can configure the explanation request to generate Shapley values for any other classes too. For example, if a model predicts a probability of `0.4` for
approving a loan application, the model's decision is to
reject the application since
`p(reject) = 0.6 > p(approve) = 0.4` , and the default
Shapley values would be computed for rejection decision and
not approval, even though the latter might be the positive
class.
If users set
ExplanationParameters.top_k,
the attributions are sorted by
instance_output_value
in descending order. If
ExplanationParameters.output_indices
is specified, the attributions are stored by
Attribution.output_index
in the same order as they appear in the output_indices.
|
`neighbors` |
`MutableSequence[`
Output only. List of the nearest neighbors for example-based explanations. For models deployed with the examples explanations feature enabled, the attributions field is empty and instead the neighbors field is populated. |

## Methods

### Explanation

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation of a prediction (provided in PredictResponse.predictions) produced by the Model on a given instance.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistmodelversionsresponse_googlecloudaiplatfo_86a82e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelversionsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsResponse -->

# Class ListModelVersionsResponse (1.134.0)

`ListModelVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModelVersions

## Attributes |
|
|---|---|
Name |
Description |
`models` |
`MutableSequence[`
List of Model versions in the requested page. In the returned Model name field, version ID instead of regvision tag will be included. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListModelVersionsRequest.page_token to obtain that page. |

## Methods

### ListModelVersionsResponse

`ListModelVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModelVersions


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletetensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTensorboardTimeSeriesRequest -->

# Class DeleteTensorboardTimeSeriesRequest (1.134.0)

```
DeleteTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardTimeSeries.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardTimeSeries to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### DeleteTensorboardTimeSeriesRequest

```
DeleteTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeslistmodelversionsresponse_googlecloudaiplatform__597824.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistmodelversionsresponse_googlecloudaiplatform_v_03b1b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistmodelversionsresponse_googlecloudaiplatform_v1_3d1f18.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodelversionsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsResponse -->

# Class ListModelVersionsResponse (1.134.0)

`ListModelVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModelVersions

## Attributes |
|
|---|---|
Name |
Description |
`models` |
`MutableSequence[`
List of Model versions in the requested page. In the returned Model name field, version ID instead of regvision tag will be included. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListModelVersionsRequest.page_token to obtain that page. |

## Methods

### ListModelVersionsResponse

`ListModelVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.ListModelVersions


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service -->

# Package tensorboard_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.tensorboard_service`

package.

## Classes

[TensorboardServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceAsyncClient)

TensorboardService

[TensorboardServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.TensorboardServiceClient)

TensorboardService

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers)

API documentation for `aiplatform_v1beta1.services.tensorboard_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistmodelversioncheckpointsresponse_googlecloudaip_a15500.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodelversioncheckpointsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionCheckpointsResponse -->

# Class ListModelVersionCheckpointsResponse (1.134.0)

```
ListModelVersionCheckpointsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelVersionCheckpoints

## Attributes |
|
|---|---|
Name |
Description |
`checkpoints` |
`MutableSequence[`
List of Model Version checkpoints. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListModelVersionCheckpointsRequest.page_token to obtain that page. |

## Methods

### ListModelVersionCheckpointsResponse

```
ListModelVersionCheckpointsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelVersionCheckpoints


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessafetysetting.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SafetySetting -->

# Class SafetySetting (1.134.0)

`SafetySetting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Safety settings.

## Attributes |
|
|---|---|
Name |
Description |
`category` |
Required. Harm category. |
`threshold` |
Required. The harm block threshold. |
`method` |
Optional. Specify if the threshold is used for probability or severity score. If not specified, the threshold is used for probability score. |

## Classes

### HarmBlockMethod

`HarmBlockMethod(value)`


Probability vs severity.

### HarmBlockThreshold

`HarmBlockThreshold(value)`


Probability based thresholds levels for blocking.

## Methods

### SafetySetting

`SafetySetting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Safety settings.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatemodeldeploymentmonitoringjobrequest__go_867b18.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelDeploymentMonitoringJobRequest -->

# Class UpdateModelDeploymentMonitoringJobRequest (1.134.0)

```
UpdateModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.UpdateModelDeploymentMonitoringJob.

## Attributes |
|
|---|---|
Name |
Description |
`model_deployment_monitoring_job` |
Required. The model monitoring configuration which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask is used to specify the fields to be overwritten in the ModelDeploymentMonitoringJob resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to
override all fields. For the objective config, the user can
either provide the update mask for
model_deployment_monitoring_objective_configs or any
combination of its nested fields, such as:
model_deployment_monitoring_objective_configs.objective_config.training_dataset.
Updatable fields:
- `display_name`
- `model_deployment_monitoring_schedule_config`
- `model_monitoring_alert_config`
- `logging_sampling_strategy`
- `labels`
- `log_ttl`
- `enable_monitoring_pipeline_logs` . and
- `model_deployment_monitoring_objective_configs` . or
- `model_deployment_monitoring_objective_configs.objective_config.training_dataset`
- `model_deployment_monitoring_objective_configs.objective_config.training_prediction_skew_detection_config`
- `model_deployment_monitoring_objective_configs.objective_config.prediction_drift_detection_config`
|

## Methods

### UpdateModelDeploymentMonitoringJobRequest

```
UpdateModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.UpdateModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfindneighborsresponseneighbor_googlecloudaiplatfor_fe5c36.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfindneighborsresponseneighbor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsResponse.Neighbor -->

# Class Neighbor (1.134.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Attributes |
|
|---|---|
Name |
Description |
`datapoint` |
The datapoint of the neighbor. Note that full datapoints are returned only when "return_full_datapoint" is set to true. Otherwise, only the "datapoint_id" and "crowding_tag" fields are populated. |
`distance` |
`float`
The distance between the neighbor and the dense embedding query. |
`sparse_distance` |
`float`
The distance between the neighbor and the query sparse_embedding. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespoststartupscriptconfigpoststartupscriptbehavior.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PostStartupScriptConfig.PostStartupScriptBehavior -->

# Class PostStartupScriptBehavior (1.134.0)

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post-startup script behavior.

## Enums |
|
|---|---|
Name |
Description |
`POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` |
Unspecified post-startup script behavior. |
`RUN_ONCE` |
Run the post-startup script only once, during runtime creation. |
`RUN_EVERY_START` |
Run the post-startup script after every start. |
`DOWNLOAD_AND_RUN_EVERY_START` |
After every start, download the post-startup script from its source and run it. |

## Methods

### PostStartupScriptBehavior

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post-startup script behavior.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typestensorboardtimeseriesvaluetype_googlecloudaipla_42a5a7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typestensorboardtimeseriesvaluetype_googlecloudaiplat_2d9ba4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestensorboardtimeseriesvaluetype_googlecloudaiplatf_b5e78d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestensorboardtimeseriesvaluetype_googlecloudaiplatfo_4f0949.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestensorboardtimeseriesvaluetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardTimeSeries.ValueType -->

# Class ValueType (1.134.0)

`ValueType(value)`


An enum representing the value type of a TensorboardTimeSeries.

## Enums |
|
|---|---|
Name |
Description |
`VALUE_TYPE_UNSPECIFIED` |
The value type is unspecified. |
`SCALAR` |
Used for TensorboardTimeSeries that is a list of scalars. E.g. accuracy of a model over epochs/time. |
`TENSOR` |
Used for TensorboardTimeSeries that is a list of tensors. E.g. histograms of weights of layer in a model over epoch/time. |
`BLOB_SEQUENCE` |
Used for TensorboardTimeSeries that is a list of blob sequences. E.g. set of sample images with labels over epochs/time. |

## Methods

### ValueType

`ValueType(value)`


An enum representing the value type of a TensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnfsmount.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NfsMount -->

# Class NfsMount (1.134.0)

`NfsMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a mount configuration for Network File System (NFS) to mount.

## Attributes |
|
|---|---|
Name |
Description |
`server` |
`str`
Required. IP address of the NFS server. |
`path` |
`str`
Required. Source path exported from NFS server. Has to start with '/', and combined with the ip address, it indicates the source mount path in the form of `server:path`
|
`mount_point` |
`str`
Required. Destination mount path. The NFS will be mounted for the user under /mnt/nfs/ |

## Methods

### NfsMount

`NfsMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a mount configuration for Network File System (NFS) to mount.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchmodeldeploymentmonitoringstatsanomaliesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesRequest (1.134.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.SearchModelDeploymentMonitoringStatsAnomalies.

## Attributes |
|
|---|---|
Name |
Description |
`model_deployment_monitoring_job` |
`str`
Required. ModelDeploymentMonitoring Job resource name. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|
`deployed_model_id` |
`str`
Required. The DeployedModel ID of the [ModelDeploymentMonitoringObjectiveConfig.deployed_model_id]. |
`feature_display_name` |
`str`
The feature display name. If specified, only return the stats belonging to this feature. Format: ModelMonitoringStatsAnomalies.FeatureHistoricStatsAnomalies.feature_display_name, example: "user_destination". |
`objectives` |
`MutableSequence[`
Required. Objectives of the stats to retrieve. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
A page token received from a previous JobService.SearchModelDeploymentMonitoringStatsAnomalies call. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The earliest timestamp of stats being generated. If not set, indicates fetching stats till the earliest possible one. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The latest timestamp of stats being generated. If not set, indicates feching stats till the latest possible one. |

## Classes

### StatsAnomaliesObjective

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

## Methods

### SearchModelDeploymentMonitoringStatsAnomaliesRequest

```
SearchModelDeploymentMonitoringStatsAnomaliesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.SearchModelDeploymentMonitoringStatsAnomalies.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplainrequest_googlecloudaiplatform_v1typesindexd_57fe06.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplainrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplainRequest -->

# Class ExplainRequest (1.134.0)

`ExplainRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Explain.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the explanation. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the explanation call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the explanation call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri. |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] parameters_schema_uri. |
`explanation_spec_override` |
If specified, overrides the explanation_spec of the DeployedModel. Can be used for explaining prediction results with different configurations, such as: - Explaining top-5 predictions results as opposed to top-1; - Increasing path count or step count of the attribution methods to reduce approximate errors; - Using different baselines for explaining the prediction results. |
`deployed_model_id` |
`str`
If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding Endpoint.traffic_split. |

## Methods

### ExplainRequest

`ExplainRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Explain.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesindexdatapointnumericrestriction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexDatapoint.NumericRestriction -->

# Class NumericRestriction (1.134.0)

`NumericRestriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This field allows restricts to be based on numeric comparisons rather than categorical tokens.

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
`value_int` |
`int`
Represents 64 bit integer. This field is a member of `oneof` _ `Value` .
|
`value_float` |
`float`
Represents 32 bit float. This field is a member of `oneof` _ `Value` .
|
`value_double` |
`float`
Represents 64 bit float. This field is a member of `oneof` _ `Value` .
|
`namespace` |
`str`
The namespace of this restriction. e.g.: cost. |
`op` |
This MUST be specified for queries and must NOT be specified for datapoints. |

## Classes

### Operator

`Operator(value)`


Which comparison operator to use. Should be specified for queries only; specifying this for a datapoint is an error.

Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

## Methods

### NumericRestriction

`NumericRestriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This field allows restricts to be based on numeric comparisons rather than categorical tokens.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeserroranalysisannotationattributeditem_googleclou_21c476.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeserroranalysisannotationattributeditem_googlecloud_b2c938.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeserroranalysisannotationattributeditem_googleclouda_48e36a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeserroranalysisannotationattributeditem.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ErrorAnalysisAnnotation.AttributedItem -->

# Class AttributedItem (1.134.0)

`AttributedItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.

## Attributes |
|
|---|---|
Name |
Description |
`annotation_resource_name` |
`str`
The unique ID for each annotation. Used by FE to allocate the annotation in DB. |
`distance` |
`float`
The distance of this item to the annotation. |

## Methods

### AttributedItem

`AttributedItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginecontextspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineContextSpec -->

# Class ReasoningEngineContextSpec (1.134.0)

`ReasoningEngineContextSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how Agent Engine sub-resources should manage context.

## Attribute |
|
|---|---|
Name |
Description |
`memory_bank_config` |
Optional. Specification for a Memory Bank, which manages memories for the Agent Engine. |

## Classes

### MemoryBankConfig

`MemoryBankConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for a Memory Bank.

## Methods

### ReasoningEngineContextSpec

`ReasoningEngineContextSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how Agent Engine sub-resources should manage context.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesartifacttypeschema.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ArtifactTypeSchema -->

# Class ArtifactTypeSchema (1.134.0)

`ArtifactTypeSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of a artifact type in MLMD.

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
`schema_title` |
`str`
The name of the type. The format of the title must be: . Examples:
- `aiplatform.Model`
- `acme.CustomModel` When this field is set, the type must
be pre-registered in the MLMD store.
This field is a member of `oneof` _ `kind` .
|
`schema_uri` |
`str`
Points to a YAML file stored on Cloud Storage describing the format. Deprecated. Use [PipelineArtifactTypeSchema.schema_title][] or [PipelineArtifactTypeSchema.instance_schema][] instead. This field is a member of `oneof` _ `kind` .
|
`instance_schema` |
`str`
Contains a raw YAML string, describing the format of the properties of the type. This field is a member of `oneof` _ `kind` .
|
`schema_version` |
`str`
The schema version of the artifact. If the value is not set, it defaults to the latest version in the system. |

## Methods

### ArtifactTypeSchema

`ArtifactTypeSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of a artifact type in MLMD.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistfeaturemonitorsresponse_googlecloudaipla_df4b2c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistfeaturemonitorsresponse_googlecloudaiplat_fb5dfa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeaturemonitorsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse -->

# Class ListFeatureMonitorsResponse (1.134.0)

`ListFeatureMonitorsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureMonitors.

## Attributes |
|
|---|---|
Name |
Description |
`feature_monitors` |
`MutableSequence[`
The FeatureMonitors matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureMonitorsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureMonitorsResponse

`ListFeatureMonitorsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeatureRegistryService.ListFeatureMonitors.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturevaluemetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValue.Metadata -->

# Class Metadata (1.134.0)

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

## Attribute |
|
|---|---|
Name |
Description |
`generate_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Feature generation timestamp. Typically, it is provided by user at feature ingestion time. If not, feature store will use the system timestamp when the data is ingested into feature store. Legacy Feature Store: For streaming ingestion, the time, aligned by days, must be no older than five years (1825 days) and no later than one year (366 days) in the future. |

## Methods

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeletenotebookruntimetemplaterequest_googlecloudai_ea039c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletenotebookruntimetemplaterequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteNotebookRuntimeTemplateRequest -->

# Class DeleteNotebookRuntimeTemplateRequest (1.134.0)

```
DeleteNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntimeTemplate.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: `projects/{project}/locations/{location}/notebookRuntimeTemplates/{notebook_runtime_template}`
|

## Methods

### DeleteNotebookRuntimeTemplateRequest

```
DeleteNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntimeTemplate.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupgradenotebookruntimeoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeOperationMetadata -->

# Class UpgradeNotebookRuntimeOperationMetadata (1.134.0)

```
UpgradeNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.UpgradeNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### UpgradeNotebookRuntimeOperationMetadata

```
UpgradeNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.UpgradeNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typeslistfeaturemonitorsrequest__googlecloudai_211c0f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeslistfeaturemonitorsrequest__googlecloudaip_1cee03.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistfeaturemonitorsrequest__googlecloudaipl_b79b27.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistfeaturemonitorsrequest__googlecloudaipla_3924fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistfeaturemonitorsrequest__googlecloudaiplat_843222.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeaturemonitorsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsRequest -->

# Class ListFeatureMonitorsRequest (1.134.0)

`ListFeatureMonitorsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.ListFeatureMonitors.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureGroup to list FeatureMonitors. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}`
|
`filter` |
`str`
Optional. Lists the FeatureMonitors that match the filter expression. The following fields are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality and key presence.
Examples:
- `create_time > "2020-01-01" OR update_time > "2020-01-01"`
FeatureMonitors created or updated after 2020-01-01.
- `labels.env = "prod"` FeatureGroups with label "env" set
to "prod".
|
`page_size` |
`int`
Optional. The maximum number of FeatureGroups to return. The service may return fewer than this value. If unspecified, at most 100 FeatureMonitors will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`page_token` |
`str`
Optional. A page token, received from a previous FeatureRegistryService.ListFeatureMonitors call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureRegistryService.ListFeatureMonitors must match the call that provided the page token. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields: - `create_time`
- `update_time`
|

## Methods

### ListFeatureMonitorsRequest

`ListFeatureMonitorsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.ListFeatureMonitors.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnotebookexecutionjobdataformrepositorysource_googl_ea060b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnotebookexecutionjobdataformrepositorysource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob.DataformRepositorySource -->

# Class DataformRepositorySource (1.134.0)

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.

## Attributes |
|
|---|---|
Name |
Description |
`dataform_repository_resource_name` |
`str`
The resource name of the Dataform Repository. Format: `projects/{project_id}/locations/{location}/repositories/{repository_id}`
|
`commit_sha` |
`str`
The commit SHA to read repository with. If unset, the file will be read at HEAD. |

## Methods

### DataformRepositorySource

`DataformRepositorySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Dataform Repository containing the input notebook.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetmodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetModelDeploymentMonitoringJobRequest -->

# Class GetModelDeploymentMonitoringJobRequest (1.134.0)

```
GetModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### GetModelDeploymentMonitoringJobRequest

```
GetModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnastrialstate_googlecloudaiplatform_v1beta1typest_6d7cc8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnastrialstate_googlecloudaiplatform_v1beta1typesty_222c6c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnastrialstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasTrial.State -->

# Class State (1.134.0)

`State(value)`


Describes a NasTrial state.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
The NasTrial state is unspecified. |
`REQUESTED` |
Indicates that a specific NasTrial has been requested, but it has not yet been suggested by the service. |
`ACTIVE` |
Indicates that the NasTrial has been suggested. |
`STOPPING` |
Indicates that the NasTrial should stop according to the service. |
`SUCCEEDED` |
Indicates that the NasTrial is completed successfully. |
`INFEASIBLE` |
Indicates that the NasTrial should not be attempted again. The service will set a NasTrial to INFEASIBLE when it's done but missing the final_measurement. |

## Methods

### State

`State(value)`


Describes a NasTrial state.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Type -->

# Class Type (1.134.0)

`Type(value)`


Type contains the list of OpenAPI data types as defined by
[https://swagger.io/docs/specification/data-models/data-types/](https://swagger.io/docs/specification/data-models/data-types/)

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Not specified, should not be used. |
`STRING` |
OpenAPI string type |
`NUMBER` |
OpenAPI number type |
`INTEGER` |
OpenAPI integer type |
`BOOLEAN` |
OpenAPI boolean type |
`ARRAY` |
OpenAPI array type |
`OBJECT` |
OpenAPI object type |

## Methods

### Type

`Type(value)`


Type contains the list of OpenAPI data types as defined by
[https://swagger.io/docs/specification/data-models/data-types/](https://swagger.io/docs/specification/data-models/data-types/)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelversioncheckpoint_googlecloudaiplatform__d4a619.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelversioncheckpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelVersionCheckpoint -->

# Class ModelVersionCheckpoint (1.134.0)

`ModelVersionCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A proto representation of a Spanner-stored ModelVersionCheckpoint. The meaning of the fields is equivalent to their in-Spanner counterparts.

## Attributes |
|
|---|---|
Name |
Description |
`checkpoint_id` |
`str`
The ID of the checkpoint. |
`epoch` |
`int`
The epoch of the checkpoint. |
`step` |
`int`
The step of the checkpoint. |

## Methods

### ModelVersionCheckpoint

`ModelVersionCheckpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A proto representation of a Spanner-stored ModelVersionCheckpoint. The meaning of the fields is equivalent to their in-Spanner counterparts.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessafetysetting.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetySetting -->

# Class SafetySetting (1.134.0)

`SafetySetting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Safety settings.

## Attributes |
|
|---|---|
Name |
Description |
`category` |
Required. Harm category. |
`threshold` |
Required. The harm block threshold. |
`method` |
Optional. Specify if the threshold is used for probability or severity score. If not specified, the threshold is used for probability score. |

## Classes

### HarmBlockMethod

`HarmBlockMethod(value)`


Probability vs severity.

### HarmBlockThreshold

`HarmBlockThreshold(value)`


Probability based thresholds levels for blocking.

## Methods

### SafetySetting

`SafetySetting(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Safety settings.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragfileparsingconfig__googlecloudaiplatform__ff495a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragfileparsingconfig__googlecloudaiplatform_v_9b3229.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragfileparsingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileParsingConfig -->

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
`advanced_parser` |
The Advanced Parser to use for RagFiles. This field is a member of `oneof` _ `parser` .
|
`layout_parser` |
The Layout Parser to use for RagFiles. This field is a member of `oneof` _ `parser` .
|
`llm_parser` |
The LLM Parser to use for RagFiles. This field is a member of `oneof` _ `parser` .
|
`use_advanced_pdf_parsing` |
`bool`
Whether to use advanced PDF parsing. |

## Classes

### AdvancedParser

`AdvancedParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the advanced parsing for RagFiles.

### LayoutParser

`LayoutParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Document AI Layout Parser config.

### LlmParser

`LlmParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the LLM parsing for RagFiles.

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessearchmodelmonitoringstatsresponse_googleclou_1a26fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchmodelmonitoringstatsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsResponse -->

# Class SearchModelMonitoringStatsResponse (1.134.0)

```
SearchModelMonitoringStatsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelMonitoringService.SearchModelMonitoringStats.

## Attributes |
|
|---|---|
Name |
Description |
`monitoring_stats` |
`MutableSequence[`
Stats retrieved for requested objectives. |
`next_page_token` |
`str`
The page token that can be used by the next ModelMonitoringService.SearchModelMonitoringStats call. |

## Methods

### SearchModelMonitoringStatsResponse

```
SearchModelMonitoringStatsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelMonitoringService.SearchModelMonitoringStats.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnfsmount.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NfsMount -->

# Class NfsMount (1.134.0)

`NfsMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a mount configuration for Network File System (NFS) to mount.

## Attributes |
|
|---|---|
Name |
Description |
`server` |
`str`
Required. IP address of the NFS server. |
`path` |
`str`
Required. Source path exported from NFS server. Has to start with '/', and combined with the ip address, it indicates the source mount path in the form of `server:path`
|
`mount_point` |
`str`
Required. Destination mount path. The NFS will be mounted for the user under /mnt/nfs/ |

## Methods

### NfsMount

`NfsMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a mount configuration for Network File System (NFS) to mount.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesimportragfilesrequest_googlecloudaiplatform__f85bca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportragfilesrequest_googlecloudaiplatform_v_378ab8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportragfilesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportRagFilesRequest -->

# Class ImportRagFilesRequest (1.134.0)

`ImportRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ImportRagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the RagCorpus resource into which to import files. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`import_rag_files_config` |
Required. The config for the RagFiles to be synced and imported into the RagCorpus. VertexRagDataService.ImportRagFiles. |

## Methods

### ImportRagFilesRequest

`ImportRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ImportRagFiles.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringSpec -->

# Class ModelMonitoringSpec (1.134.0)

`ModelMonitoringSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Monitoring monitoring job spec. It outlines the specifications for monitoring objectives, notifications, and result exports.

## Attributes |
|
|---|---|
Name |
Description |
`objective_spec` |
The monitoring objective spec. |
`notification_spec` |
The model monitoring notification spec. |
`output_spec` |
The Output destination spec for metrics, error logs, etc. |

## Methods

### ModelMonitoringSpec

`ModelMonitoringSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Monitoring monitoring job spec. It outlines the specifications for monitoring objectives, notifications, and result exports.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltexte_f9f266.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltextextraction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtraction -->

# Class AutoMlTextExtraction (1.134.0)

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlTextExtraction

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

### AutoMlTextExtraction

`AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupgradenotebookruntimeoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpgradeNotebookRuntimeOperationMetadata -->

# Class UpgradeNotebookRuntimeOperationMetadata (1.134.0)

```
UpgradeNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.UpgradeNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### UpgradeNotebookRuntimeOperationMetadata

```
UpgradeNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.UpgradeNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesindexdatapointsparseembedding_googlecloudaiplat_4038d1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesindexdatapointsparseembedding_googlecloudaiplatf_2d41fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesindexdatapointsparseembedding_googlecloudaiplatfo_0e99ca.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesindexdatapointsparseembedding_googlecloudaiplatfor_5dd5ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesindexdatapointsparseembedding.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexDatapoint.SparseEmbedding -->

# Class SparseEmbedding (1.134.0)

`SparseEmbedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature embedding vector for sparse index. An array of numbers whose values are located in the specified dimensions.

## Attributes |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. The list of embedding values of the sparse vector. |
`dimensions` |
`MutableSequence[int]`
Required. The list of indexes for the embedding values of the sparse vector. |

## Methods

### SparseEmbedding

`SparseEmbedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature embedding vector for sparse index. An array of numbers whose values are located in the specified dimensions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatesessionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSessionRequest -->

# Class UpdateSessionRequest (1.134.0)

`UpdateSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.UpdateSession.

## Attributes |
|
|---|---|
Name |
Description |
`session` |
Required. The session to update. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Field mask is used to control which fields get updated. If the mask is not present, all fields will be updated. |

## Methods

### UpdateSessionRequest

`UpdateSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.UpdateSession.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfunctioncallingconfig_googlecloudaiplatform_v_8b8361.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfunctioncallingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionCallingConfig -->

# Class FunctionCallingConfig (1.134.0)

`FunctionCallingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Function calling config.

## Attributes |
|
|---|---|
Name |
Description |
`mode` |
Optional. Function calling mode. |
`allowed_function_names` |
`MutableSequence[str]`
Optional. Function names to call. Only set when the Mode is ANY. Function names should match [FunctionDeclaration.name]. With mode set to ANY, model will predict a function call from the set of function names provided. |

## Classes

### Mode

`Mode(value)`


Function calling mode.

## Methods

### FunctionCallingConfig

`FunctionCallingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Function calling config.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupgradenotebookruntimerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpgradeNotebookRuntimeRequest -->

# Class UpgradeNotebookRuntimeRequest (1.134.0)

```
UpgradeNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpgradeNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### UpgradeNotebookRuntimeRequest

```
UpgradeNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpgradeNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragretrievalconfigranking__googlecloudaiplatf_de5064.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragretrievalconfigranking.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagRetrievalConfig.Ranking -->

# Class Ranking (1.134.0)

`Ranking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ranking and reranking.

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
`rank_service` |
Optional. Config for Rank Service. This field is a member of `oneof` _ `ranking_config` .
|
`llm_ranker` |
Optional. Config for LlmRanker. This field is a member of `oneof` _ `ranking_config` .
|

## Classes

### LlmRanker

`LlmRanker(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for LlmRanker.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### RankService

`RankService(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Rank Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### Ranking

`Ranking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ranking and reranking.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeletenotebookruntimetemplaterequest_googlecl_5fba50.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletenotebookruntimetemplaterequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteNotebookRuntimeTemplateRequest -->

# Class DeleteNotebookRuntimeTemplateRequest (1.134.0)

```
DeleteNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntimeTemplate.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource to be deleted. Format: `projects/{project}/locations/{location}/notebookRuntimeTemplates/{notebook_runtime_template}`
|

## Methods

### DeleteNotebookRuntimeTemplateRequest

```
DeleteNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.DeleteNotebookRuntimeTemplate.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadatainputmetadatavisualizationtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata.Visualization.Type -->

# Class Type (1.134.0)

`Type(value)`


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.integrated_gradients_attribution].

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Should not be used. |
`PIXELS` |
Shows which pixel contributed to the image prediction. |
`OUTLINES` |
Shows which region contributed to the image prediction by outlining the region. |

## Methods

### Type

`Type(value)`


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.integrated_gradients_attribution].


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistmetadatastoresresponse_googlecloudaipla_43d19e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistmetadatastoresresponse_googlecloudaiplat_a38aff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistmetadatastoresresponse_googlecloudaiplatf_176ed6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmetadatastoresresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresResponse -->

# Class ListMetadataStoresResponse (1.134.0)

`ListMetadataStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataStores.

## Attributes |
|
|---|---|
Name |
Description |
`metadata_stores` |
`MutableSequence[`
The MetadataStores found for the Location. |
`next_page_token` |
`str`
A token, which can be sent as ListMetadataStoresRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListMetadataStoresResponse

`ListMetadataStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListMetadataStores.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecparameterspecconditionalparameterspecdiscretevaluecondition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.DiscreteValueCondition -->

# Class DiscreteValueCondition (1.134.0)

`DiscreteValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match discrete values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. Matches values of the parent parameter of 'DISCRETE' type. All values must exist in `discrete_value_spec` of parent parameter.
The Epsilon of the value matching is 1e-10.
|

## Methods

### DiscreteValueCondition

`DiscreteValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match discrete values from parent parameter.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeleteragcorpusrequest_googlecloudaiplatform_v1typ_559664.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeleteragcorpusrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteRagCorpusRequest -->

# Class DeleteRagCorpusRequest (1.134.0)

`DeleteRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.DeleteRagCorpus.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the RagCorpus resource to be deleted. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`force` |
`bool`
Optional. If set to true, any RagFiles in this RagCorpus will also be deleted. Otherwise, the request will only work if the RagCorpus has no RagFiles. |

## Methods

### DeleteRagCorpusRequest

`DeleteRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.DeleteRagCorpus.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestensorboardblobsequence.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardBlobSequence -->

# Class TensorboardBlobSequence (1.134.0)

`TensorboardBlobSequence(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One point viewable on a blob metric plot, but mostly just a wrapper
message to work around repeated fields can't be used directly within
`oneof`

fields.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[google.cloud.aiplatform_v1.types.TensorboardBlob]`
List of blobs contained within the sequence. |

## Methods

### TensorboardBlobSequence

`TensorboardBlobSequence(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One point viewable on a blob metric plot, but mostly just a wrapper
message to work around repeated fields can't be used directly within
`oneof`

fields.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualizationtype_60ee4a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualizationtype__246047.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualizationtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata.Visualization.Type -->

# Class Type (1.134.0)

`Type(value)`


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1.ExplanationParameters.integrated_gradients_attribution].

## Enums |
|
|---|---|
Name |
Description |
`TYPE_UNSPECIFIED` |
Should not be used. |
`PIXELS` |
Shows which pixel contributed to the image prediction. |
`OUTLINES` |
Shows which region contributed to the image prediction by outlining the region. |

## Methods

### Type

`Type(value)`


Type of the image visualization. Only applicable to [Integrated Gradients attribution][google.cloud.aiplatform.v1.ExplanationParameters.integrated_gradients_attribution].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspecparameterspecconditionalparameterspecdiscretevaluecondition.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.DiscreteValueCondition -->

# Class DiscreteValueCondition (1.134.0)

`DiscreteValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match discrete values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. Matches values of the parent parameter of 'DISCRETE' type. All values must exist in `discrete_value_spec` of parent parameter.
The Epsilon of the value matching is 1e-10.
|

## Methods

### DiscreteValueCondition

`DiscreteValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match discrete values from parent parameter.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescounttokensresponse_googlecloudaiplatform_v1b_b358de.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescounttokensresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CountTokensResponse -->

# Class CountTokensResponse (1.134.0)

`CountTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.CountTokens.

## Attributes |
|
|---|---|
Name |
Description |
`total_tokens` |
`int`
The total number of tokens counted across all instances from the request. |
`total_billable_characters` |
`int`
The total number of billable characters counted across all instances from the request. |
`prompt_tokens_details` |
`MutableSequence[`
Output only. List of modalities that were processed in the request input. |

## Methods

### CountTokensResponse

`CountTokensResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.CountTokens.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service -->

# Package model_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.model_service`

package.

## Classes

[ModelServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient)

A service for managing Vertex AI's machine learning Models.

[ModelServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient)

A service for managing Vertex AI's machine learning Models.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers)

API documentation for `aiplatform_v1beta1.services.model_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typeslistbatchpredictionjobsresponse_googleclo_423385.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeslistbatchpredictionjobsresponse_googleclou_02003d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistbatchpredictionjobsresponse_googlecloud_773a3c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistbatchpredictionjobsresponse_googleclouda_e91dff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistbatchpredictionjobsresponse_googlecloudai_da6599.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistbatchpredictionjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse -->

# Class ListBatchPredictionJobsResponse (1.134.0)

```
ListBatchPredictionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListBatchPredictionJobs

## Attributes |
|
|---|---|
Name |
Description |
`batch_prediction_jobs` |
`MutableSequence[`
List of BatchPredictionJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListBatchPredictionJobsRequest.page_token to obtain that page. |

## Methods

### ListBatchPredictionJobsResponse

```
ListBatchPredictionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListBatchPredictionJobs


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupgradenotebookruntimerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpgradeNotebookRuntimeRequest -->

# Class UpgradeNotebookRuntimeRequest (1.134.0)

```
UpgradeNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpgradeNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be upgrade. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### UpgradeNotebookRuntimeRequest

```
UpgradeNotebookRuntimeRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpgradeNotebookRuntime.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesinputstransformationtexttransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.TextTransformation -->

# Class TextTransformation (1.134.0)

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.

## Methods

### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.

### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfindneighborsresponse_googlecloudaiplatform_v1typ_78b28e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfindneighborsresponse_googlecloudaiplatform_v1type_67c8c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfindneighborsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsResponse -->

# Class FindNeighborsResponse (1.134.0)

`FindNeighborsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The response message for MatchService.FindNeighbors.

## Attribute |
|
|---|---|
Name |
Description |
`nearest_neighbors` |
`MutableSequence[`
The nearest neighbors of the query datapoints. |

## Classes

### NearestNeighbors

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Methods

### FindNeighborsResponse

`FindNeighborsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The response message for MatchService.FindNeighbors.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesembedcontentresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EmbedContentResponse -->

# Class EmbedContentResponse (1.134.0)

`EmbedContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.EmbedContent.

## Attributes |
|
|---|---|
Name |
Description |
`embedding` |
The embedding generated from the input content. |
`usage_metadata` |
Metadata about the response(s). |
`truncated` |
`bool`
Whether the input content was truncated before generating the embedding. |

## Classes

### Embedding

`Embedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of floats representing an embedding.

## Methods

### EmbedContentResponse

`EmbedContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.EmbedContent.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesindexdatapointnumericrestriction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexDatapoint.NumericRestriction -->

# Class NumericRestriction (1.134.0)

`NumericRestriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This field allows restricts to be based on numeric comparisons rather than categorical tokens.

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
`value_int` |
`int`
Represents 64 bit integer. This field is a member of `oneof` _ `Value` .
|
`value_float` |
`float`
Represents 32 bit float. This field is a member of `oneof` _ `Value` .
|
`value_double` |
`float`
Represents 64 bit float. This field is a member of `oneof` _ `Value` .
|
`namespace` |
`str`
The namespace of this restriction. e.g.: cost. |
`op` |
This MUST be specified for queries and must NOT be specified for datapoints. |

## Classes

### Operator

`Operator(value)`


Which comparison operator to use. Should be specified for queries only; specifying this for a datapoint is an error.

Datapoints for which Operator is true relative to the query's Value field will be allowlisted.

## Methods

### NumericRestriction

`NumericRestriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This field allows restricts to be based on numeric comparisons rather than categorical tokens.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesevaluateinstancesrequest__googlecloudaiplatform_v1_43c90c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesevaluateinstancesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluateInstancesRequest -->

# Class EvaluateInstancesRequest (1.134.0)

`EvaluateInstancesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EvaluationService.EvaluateInstances.

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
`exact_match_input` |
Auto metric instances. Instances and metric spec for exact match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`bleu_input` |
Instances and metric spec for bleu metric. This field is a member of `oneof` _ `metric_inputs` .
|
`rouge_input` |
Instances and metric spec for rouge metric. This field is a member of `oneof` _ `metric_inputs` .
|
`fluency_input` |
LLM-based metric instance. General text generation metrics, applicable to other categories. Input for fluency metric. This field is a member of `oneof` _ `metric_inputs` .
|
`coherence_input` |
Input for coherence metric. This field is a member of `oneof` _ `metric_inputs` .
|
`safety_input` |
Input for safety metric. This field is a member of `oneof` _ `metric_inputs` .
|
`groundedness_input` |
Input for groundedness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`fulfillment_input` |
Input for fulfillment metric. This field is a member of `oneof` _ `metric_inputs` .
|
`summarization_quality_input` |
Input for summarization quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pairwise_summarization_quality_input` |
Input for pairwise summarization quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`summarization_helpfulness_input` |
Input for summarization helpfulness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`summarization_verbosity_input` |
Input for summarization verbosity metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_quality_input` |
Input for question answering quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pairwise_question_answering_quality_input` |
Input for pairwise question answering quality metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_relevance_input` |
Input for question answering relevance metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_helpfulness_input` |
Input for question answering helpfulness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`question_answering_correctness_input` |
Input for question answering correctness metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pointwise_metric_input` |
Input for pointwise metric. This field is a member of `oneof` _ `metric_inputs` .
|
`pairwise_metric_input` |
Input for pairwise metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_call_valid_input` |
Tool call metric instances. Input for tool call valid metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_name_match_input` |
Input for tool name match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_parameter_key_match_input` |
Input for tool parameter key match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`tool_parameter_kv_match_input` |
Input for tool parameter key value match metric. This field is a member of `oneof` _ `metric_inputs` .
|
`comet_input` |
Translation metrics. Input for Comet metric. This field is a member of `oneof` _ `metric_inputs` .
|
`metricx_input` |
Input for Metricx metric. This field is a member of `oneof` _ `metric_inputs` .
|
`location` |
`str`
Required. The resource name of the Location to evaluate the instances. Format: `projects/{project}/locations/{location}`
|

## Methods

### EvaluateInstancesRequest

`EvaluateInstancesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EvaluationService.EvaluateInstances.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistfeatureonlinestoresrequest__googlecloudaiplatf_00d928.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeatureonlinestoresrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresRequest -->

# Class ListFeatureOnlineStoresRequest (1.134.0)

```
ListFeatureOnlineStoresRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list FeatureOnlineStores. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the FeatureOnlineStores that match the filter expression. The following fields are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality and key presence.
Examples:
- `create_time > "2020-01-01" OR update_time > "2020-01-01"`
FeatureOnlineStores created or updated after 2020-01-01.
- `labels.env = "prod"` FeatureOnlineStores with label
"env" set to "prod".
|
`page_size` |
`int`
The maximum number of FeatureOnlineStores to return. The service may return fewer than this value. If unspecified, at most 100 FeatureOnlineStores will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`page_token` |
`str`
A page token, received from a previous FeatureOnlineStoreAdminService.ListFeatureOnlineStores call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureOnlineStoreAdminService.ListFeatureOnlineStores must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields: - `create_time`
- `update_time`
|

## Methods

### ListFeatureOnlineStoresRequest

```
ListFeatureOnlineStoresRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesremovecontextchildrenrequest_googlecloudaipla_53e516.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesremovecontextchildrenrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveContextChildrenRequest -->

# Class RemoveContextChildrenRequest (1.134.0)

```
RemoveContextChildrenRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [MetadataService.DeleteContextChildrenRequest][].

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the parent Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`child_contexts` |
`MutableSequence[str]`
The resource names of the child Contexts. |

## Methods

### RemoveContextChildrenRequest

```
RemoveContextChildrenRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [MetadataService.DeleteContextChildrenRequest][].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespscautomatedendpoints.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PscAutomatedEndpoints -->

# Class PscAutomatedEndpoints (1.134.0)

`PscAutomatedEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PscAutomatedEndpoints defines the output of the forwarding rule automatically created by each PscAutomationConfig.

## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Corresponding project_id in pscAutomationConfigs |
`network` |
`str`
Corresponding network in pscAutomationConfigs. |
`match_address` |
`str`
Ip Address created by the automated forwarding rule. |

## Methods

### PscAutomatedEndpoints

`PscAutomatedEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PscAutomatedEndpoints defines the output of the forwarding rule automatically created by each PscAutomationConfig.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesdeletetensorboardtimeseriesrequest_googlec_61484b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesdeletetensorboardtimeseriesrequest_googlecl_248ba4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdeletetensorboardtimeseriesrequest_googleclo_48d546.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeletetensorboardtimeseriesrequest_googleclou_be455e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletetensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTensorboardTimeSeriesRequest -->

# Class DeleteTensorboardTimeSeriesRequest (1.134.0)

```
DeleteTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardTimeSeries.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardTimeSeries to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### DeleteTensorboardTimeSeriesRequest

```
DeleteTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessupervisedhyperparameters.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SupervisedHyperParameters -->

# Class SupervisedHyperParameters (1.134.0)

`SupervisedHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for SFT.

## Attributes |
|
|---|---|
Name |
Description |
`epoch_count` |
`int`
Optional. Number of complete passes the model makes over the entire training dataset during training. |
`learning_rate_multiplier` |
`float`
Optional. Multiplier for adjusting the default learning rate. |
`adapter_size` |
Optional. Adapter size for tuning. |

## Classes

### AdapterSize

`AdapterSize(value)`


Supported adapter sizes for tuning.

## Methods

### SupervisedHyperParameters

`SupervisedHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for SFT.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringjoblatestmonitoringp_ac7f1f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringjoblatestmonitoringpipelinemetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringJob.LatestMonitoringPipelineMetadata -->

# Class LatestMonitoringPipelineMetadata (1.134.0)

```
LatestMonitoringPipelineMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


All metadata of most recent monitoring pipelines.

## Attributes |
|
|---|---|
Name |
Description |
`run_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The time that most recent monitoring pipelines that is related to this run. |
`status` |
`google.rpc.status_pb2.Status`
The status of the most recent monitoring pipeline. |

## Methods

### LatestMonitoringPipelineMetadata

```
LatestMonitoringPipelineMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


All metadata of most recent monitoring pipelines.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessecretref.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SecretRef -->

# Class SecretRef (1.134.0)

`SecretRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable.

## Attributes |
|
|---|---|
Name |
Description |
`secret` |
`str`
Required. The name of the secret in Cloud Secret Manager. Format: {secret_name}. |
`version` |
`str`
The Cloud Secret Manager secret version. Can be 'latest' for the latest version, an integer for a specific version, or a version alias. |

## Methods

### SecretRef

`SecretRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typessearchfeaturesresponse_googlecloudaiplatform_v1be_c51795.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessearchfeaturesresponse_googlecloudaiplatform_v1bet_9c7bbb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessearchfeaturesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse -->

# Class SearchFeaturesResponse (1.134.0)

`SearchFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.SearchFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[`
The Features matching the request. Fields returned: - `name`
- `description`
- `labels`
- `create_time`
- `update_time`
|
`next_page_token` |
`str`
A token, which can be sent as SearchFeaturesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### SearchFeaturesResponse

`SearchFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.SearchFeatures.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateextensionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExtensionRequest -->

# Class UpdateExtensionRequest (1.134.0)

`UpdateExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.UpdateExtension.

## Attributes |
|
|---|---|
Name |
Description |
`extension` |
Required. The Extension which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Mask specifying which fields to update. Supported fields: :: * `display_name`
* `description`
* `runtime_config`
* `tool_use_examples`
* `manifest.description`
|

## Methods

### UpdateExtensionRequest

`UpdateExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.UpdateExtension.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespscautomatedendpoints_googlecloudaiplatform_v1type_7607f6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespscautomatedendpoints.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PscAutomatedEndpoints -->

# Class PscAutomatedEndpoints (1.134.0)

`PscAutomatedEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PscAutomatedEndpoints defines the output of the forwarding rule automatically created by each PscAutomationConfig.

## Attributes |
|
|---|---|
Name |
Description |
`project_id` |
`str`
Corresponding project_id in pscAutomationConfigs |
`network` |
`str`
Corresponding network in pscAutomationConfigs. |
`match_address` |
`str`
Ip Address created by the automated forwarding rule. |

## Methods

### PscAutomatedEndpoints

`PscAutomatedEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PscAutomatedEndpoints defines the output of the forwarding rule automatically created by each PscAutomationConfig.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesremovecontextchildrenrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveContextChildrenRequest -->

# Class RemoveContextChildrenRequest (1.134.0)

```
RemoveContextChildrenRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [MetadataService.DeleteContextChildrenRequest][].

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the parent Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`child_contexts` |
`MutableSequence[str]`
The resource names of the child Contexts. |

## Methods

### RemoveContextChildrenRequest

```
RemoveContextChildrenRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [MetadataService.DeleteContextChildrenRequest][].


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestuningjob___googlecloudaiplatform_v1typesdeletemod_e2c63e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestuningjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TuningJob -->

# Class TuningJob (1.134.0)

`TuningJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a TuningJob that runs with Google owned models.

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
`base_model` |
`str`
The base model that is being tuned. See `Supported models |
`pre_tuned_model` |
The pre-tuned model for continuous tuning. This field is a member of `oneof` _ `source_model` .
|
`supervised_tuning_spec` |
Tuning Spec for Supervised Fine Tuning. This field is a member of `oneof` _ `tuning_spec` .
|
`name` |
`str`
Output only. Identifier. Resource name of a TuningJob. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`
|
`tuned_model_display_name` |
`str`
Optional. The display name of the TunedModel. The name can be up to 128 characters long and can consist of any UTF-8 characters. For continuous tuning, tuned_model_display_name will by default use the same display name as the pre-tuned model. If a new display name is provided, the tuning job will create a new model instead of a new version. |
`description` |
`str`
Optional. The description of the TuningJob. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TuningJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TuningJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TuningJob entered any of the following JobStates: `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` ,
`JOB_STATE_CANCELLED` , `JOB_STATE_EXPIRED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the TuningJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize TuningJob and generated resources such as Model and Endpoint. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`experiment` |
`str`
Output only. The Experiment associated with this TuningJob. |
`tuned_model` |
Output only. The tuned model resources associated with this TuningJob. |
`tuning_data_stats` |
Output only. The tuning data statistics associated with this TuningJob. |
`encryption_spec` |
Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key. |
`service_account` |
`str`
The service account that the tuningJob workload runs as. If not specified, the Vertex AI Secure Fine-Tuned Service Agent in the project will be used. See https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service
account.
|

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

### TuningJob

`TuningJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a TuningJob that runs with Google owned models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdeletemodeldeploymentmonitoringjobrequest_googlec_d048c9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeletemodeldeploymentmonitoringjobrequest_googlecl_abf241.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteModelDeploymentMonitoringJobRequest -->

# Class DeleteModelDeploymentMonitoringJobRequest (1.134.0)

```
DeleteModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the model monitoring job to delete. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### DeleteModelDeploymentMonitoringJobRequest

```
DeleteModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeleteragfilerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagFileRequest -->

# Class DeleteRagFileRequest (1.134.0)

`DeleteRagFileRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.DeleteRagFile.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the RagFile resource to be deleted. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}/ragFiles/{rag_file}`
|
`force_delete` |
`bool`
Optional. If set to true, any errors generated by external vector database during the deletion will be ignored. The default value is false. |

## Methods

### DeleteRagFileRequest

`DeleteRagFileRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.DeleteRagFile.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespausemodeldeploymentmonitoringjobrequest_googleclo_8eb456.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespausemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PauseModelDeploymentMonitoringJobRequest -->

# Class PauseModelDeploymentMonitoringJobRequest (1.134.0)

```
PauseModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.PauseModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob to pause. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### PauseModelDeploymentMonitoringJobRequest

```
PauseModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.PauseModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeleteragcorpusrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteRagCorpusRequest -->

# Class DeleteRagCorpusRequest (1.134.0)

`DeleteRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.DeleteRagCorpus.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the RagCorpus resource to be deleted. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`force` |
`bool`
Optional. If set to true, any RagFiles in this RagCorpus will also be deleted. Otherwise, the request will only work if the RagCorpus has no RagFiles. |

## Methods

### DeleteRagCorpusRequest

`DeleteRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.DeleteRagCorpus.
