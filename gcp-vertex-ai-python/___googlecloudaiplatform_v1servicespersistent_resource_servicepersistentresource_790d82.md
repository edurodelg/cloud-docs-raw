---
merged_at: 2026-01-25T21:47:44.367206
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicespersistent_resource_servicepersistentresources_9a0970.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicespersistent_resource_servicepersistentresourcese_a1547c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespersistent_resource_servicepersistentresourceserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient -->

# Class PersistentResourceServiceAsyncClient (1.134.0)

```
PersistentResourceServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's machine learning PersistentResource.

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
`PersistentResourceServiceTransport` |
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

### PersistentResourceServiceAsyncClient

```
PersistentResourceServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the persistent resource service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PersistentResourceServiceTransport,Callable[..., PersistentResourceServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the PersistentResourceServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_persistent_resource

```
create_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.CreatePersistentResourceRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
] = None,
persistent_resource_id: typing.Optional[str] = None,
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


Creates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePersistentResourceRequest.html)(
parent="parent_value",
persistent_resource_id="persistent_resource_id_value",
)
# Make the request
operation = client.[create_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_create_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.CreatePersistentResource. |
`parent` |
Required. The resource name of the Location to create the PersistentResource in. Format: |
`persistent_resource` |
Required. The PersistentResource to create. This corresponds to the |
`persistent_resource_id` |
Required. The ID to use for the PersistentResource, which become the final component of the PersistentResource's resource name. The maximum length is 63 characters, and valid characters are |
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

### delete_persistent_resource

```
delete_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.DeletePersistentResourceRequest,
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


Deletes a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeletePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_delete_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.DeletePersistentResource. |
`name` |
Required. The name of the PersistentResource to be deleted. Format: |
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
`PersistentResourceServiceAsyncClient` |
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
`PersistentResourceServiceAsyncClient` |
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
`PersistentResourceServiceAsyncClient` |
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

### get_persistent_resource

```
get_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.GetPersistentResourceRequest,
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
) -> google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
```


Gets a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_get_persistent_resource)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for PersistentResourceService.GetPersistentResource. |
`name` |
Required. The name of the PersistentResource resource. Format: |
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
Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport
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

### list_persistent_resources

```
list_persistent_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
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
google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesAsyncPager
)
```


Lists PersistentResources in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_persistent_resources():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListPersistentResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_persistent_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_list_persistent_resources)(request=request)
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
The request object. Request message for PersistentResourceService.ListPersistentResources. |
`parent` |
Required. The resource name of the Location to list the PersistentResources from. Format: |
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
Response message for PersistentResourceService.ListPersistentResources Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

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

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_persistent_resource_path

`parse_persistent_resource_path(path: str) -> typing.Dict[str, str]`


Parses a persistent_resource path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### persistent_resource_path

```
persistent_resource_path(
project: str, location: str, persistent_resource: str
) -> str
```


Returns a fully-qualified persistent_resource string.

### reboot_persistent_resource

```
reboot_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.RebootPersistentResourceRequest,
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


Reboots a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_reboot_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RebootPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebootPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[reboot_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_reboot_persistent_resource)(request=request)
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
The request object. Request message for PersistentResourceService.RebootPersistentResource. |
`name` |
Required. The name of the PersistentResource resource. Format: |
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

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

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

### update_persistent_resource

```
update_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.persistent_resource_service.UpdatePersistentResourceRequest,
dict,
]
] = None,
*,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
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


Updates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdatePersistentResourceRequest.html)(
)
# Make the request
operation = client.[update_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceAsyncClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceAsyncClient_update_persistent_resource)(request=request)
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
The request object. Request message for UpdatePersistentResource method. |
`persistent_resource` |
Required. The PersistentResource to update. The PersistentResource's |
`update_mask` |
Required. Specify the fields to be overwritten in the PersistentResource by the update method. This corresponds to the |
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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesbatchreadfeaturevaluesrequestentitytypespec_go_b43486.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesbatchreadfeaturevaluesrequestentitytypespec_goo_abd9b1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesbatchreadfeaturevaluesrequestentitytypespec_goog_d06c93.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesbatchreadfeaturevaluesrequestentitytypespec_googl_31cf98.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbatchreadfeaturevaluesrequestentitytypespec_google_e8fdc0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchreadfeaturevaluesrequestentitytypespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesRequest.EntityTypeSpec -->

# Class EntityTypeSpec (1.134.0)

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type_id` |
`str`
Required. ID of the EntityType to select Features. The EntityType id is the entity_type_id specified during EntityType creation. |
`feature_selector` |
Required. Selectors choosing which Feature values to read from the EntityType. |
`settings` |
`MutableSequence[`
Per-Feature settings for the batch read. |

## Methods

### EntityTypeSpec

`EntityTypeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Selects Features of an EntityType to read values of and specifies read settings.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdedicatedresourcesscaletozerospec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DedicatedResources.ScaleToZeroSpec -->

# Class ScaleToZeroSpec (1.134.0)

`ScaleToZeroSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for scale-to-zero feature.

## Attributes |
|
|---|---|
Name |
Description |
`min_scaleup_period` |
`google.protobuf.duration_pb2.Duration`
Optional. Minimum duration that a deployment will be scaled up before traffic is evaluated for potential scale-down. [MinValue=300] (5 minutes) [MaxValue=28800] (8 hours) |
`idle_scaledown_period` |
`google.protobuf.duration_pb2.Duration`
Optional. Duration of no traffic before scaling to zero. [MinValue=300] (5 minutes) [MaxValue=28800] (8 hours) |

## Methods

### ScaleToZeroSpec

`ScaleToZeroSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for scale-to-zero feature.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeaturestoresrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresRequest -->

# Class ListFeaturestoresRequest (1.134.0)

`ListFeaturestoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeaturestores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list Featurestores. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the featurestores that match the filter expression. The following fields are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `online_serving_config.fixed_node_count` : Supports
`=` , `!=` , , `>` , `<>` , and `>=`
comparisons.
- `labels` : Supports key-value equality and key presence.
Examples:
- `create_time > "2020-01-01" OR update_time > "2020-01-01"`
Featurestores created or updated after 2020-01-01.
- `labels.env = "prod"` Featurestores with label "env" set
to "prod".
|
`page_size` |
`int`
The maximum number of Featurestores to return. The service may return fewer than this value. If unspecified, at most 100 Featurestores will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.ListFeaturestores call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.ListFeaturestores must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields: - `create_time`
- `update_time`
- `online_serving_config.fixed_node_count`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListFeaturestoresRequest

`ListFeaturestoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeaturestores.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespredictrequest__googlecloudaiplatform_v1beta1_0fc0c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictRequest -->

# Class PredictRequest (1.134.0)

`PredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Predict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] parameters_schema_uri. |
`labels` |
`MutableMapping[str, str]`
Optional. The user labels for Imagen billing usage only. Only Imagen supports labels. For other use cases, it will be ignored. |

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

### PredictRequest

`PredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Predict.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesharmcategory_googlecloudaiplatform_v1beta1typ_be22b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesharmcategory.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.HarmCategory -->

# Class HarmCategory (1.134.0)

`HarmCategory(value)`


Harm categories that will block the content.

## Enums |
|
|---|---|
Name |
Description |
`HARM_CATEGORY_UNSPECIFIED` |
The harm category is unspecified. |
`HARM_CATEGORY_HATE_SPEECH` |
The harm category is hate speech. |
`HARM_CATEGORY_DANGEROUS_CONTENT` |
The harm category is dangerous content. |
`HARM_CATEGORY_HARASSMENT` |
The harm category is harassment. |
`HARM_CATEGORY_SEXUALLY_EXPLICIT` |
The harm category is sexually explicit content. |
`HARM_CATEGORY_CIVIC_INTEGRITY` |
Deprecated: Election filter is not longer supported. The harm category is civic integrity. |
`HARM_CATEGORY_JAILBREAK` |
The harm category is for jailbreak prompts. |

## Methods

### HarmCategory

`HarmCategory(value)`


Harm categories that will block the content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisttensorboardexperimentsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse -->

# Class ListTensorboardExperimentsResponse (1.134.0)

```
ListTensorboardExperimentsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardExperiments.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_experiments` |
`MutableSequence[`
The TensorboardExperiments mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardExperimentsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardExperimentsResponse

```
ListTensorboardExperimentsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardExperiments.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesliststudiesrequest_googlecloudaiplatform_v1beta1_06f4fd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesliststudiesrequest_googlecloudaiplatform_v1beta1t_d00629.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesliststudiesrequest_googlecloudaiplatform_v1beta1ty_a4ea54.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesliststudiesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesRequest -->

# Class ListStudiesRequest (1.134.0)

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Study from. Format: `projects/{project}/locations/{location}`
|
`page_token` |
`str`
Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages. |
`page_size` |
`int`
Optional. The maximum number of studies to return per "page" of results. If unspecified, service will pick an appropriate default. |

## Methods

### ListStudiesRequest

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisttensorboardtimeseriesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse -->

# Class ListTensorboardTimeSeriesResponse (1.134.0)

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`MutableSequence[`
The TensorboardTimeSeries mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardTimeSeriesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardTimeSeriesResponse

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistnastrialdetailsrequest_googlecloudaiplatf_1f9ba6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistnastrialdetailsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsRequest -->

# Class ListNasTrialDetailsRequest (1.134.0)

`ListNasTrialDetailsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasTrialDetails.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the NasJob resource. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListNasTrialDetailsResponse.next_page_token of the previous JobService.ListNasTrialDetails call. |

## Methods

### ListNasTrialDetailsRequest

`ListNasTrialDetailsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasTrialDetails.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnasjobspecmultitrialalgorithmspectraintrialspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJobSpec.MultiTrialAlgorithmSpec.TrainTrialSpec -->

# Class TrainTrialSpec (1.134.0)

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

## Attributes |
|
|---|---|
Name |
Description |
`train_trial_job_spec` |
Required. The spec of a train trial job. The same spec applies to all train trials. |
`max_parallel_trial_count` |
`int`
Required. The maximum number of trials to run in parallel. |
`frequency` |
`int`
Required. Frequency of search trials to start train stage. Top N [TrainTrialSpec.max_parallel_trial_count] search trials will be trained for every M [TrainTrialSpec.frequency] trials searched. |

## Methods

### TrainTrialSpec

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexportfiltersplit_googlecloudaiplatform_v1beta1typ_8ffbb4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportfiltersplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFilterSplit -->

# Class ExportFilterSplit (1.134.0)

`ExportFilterSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the given filters, data pieces not matched by any filter are ignored. Currently only supported for Datasets containing DataItems. If any of the filters in this message are to match nothing, then they can be set as '-' (the minus sign).

Supported only for unstructured Datasets.

## Attributes |
|
|---|---|
Name |
Description |
`training_filter` |
`str`
Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. |
`validation_filter` |
`str`
Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. |
`test_filter` |
`str`
Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. |

## Methods

### ExportFilterSplit

`ExportFilterSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the given filters, data pieces not matched by any filter are ignored. Currently only supported for Datasets containing DataItems. If any of the filters in this message are to match nothing, then they can be set as '-' (the minus sign).

Supported only for unstructured Datasets.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturemonitor.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureMonitor -->

# Class FeatureMonitor (1.134.0)

`FeatureMonitor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Monitor.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. Name of the FeatureMonitor. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}/featureMonitors/{featureMonitor}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureMonitor was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureMonitor was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your FeatureMonitor. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureMonitor(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`description` |
`str`
Optional. Description of the FeatureMonitor. |
`schedule_config` |
Required. Schedule config for the FeatureMonitor. |
`feature_selection_config` |
Required. Feature selection config for the FeatureMonitor. |

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

### FeatureMonitor

`FeatureMonitor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Monitor.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesnotebook_service_googlecloudaiplatform__e1f26b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesnotebook_service_googlecloudaiplatform_v_767ae2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesnotebook_service_googlecloudaiplatform_v1_465644.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesnotebook_service_googlecloudaiplatform_v1t_2c5001.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesnotebook_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service -->

# Package notebook_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.notebook_service`

package.

## Classes

[NotebookServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceAsyncClient)

The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

[NotebookServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.NotebookServiceClient)

The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers)

API documentation for `aiplatform_v1beta1.services.notebook_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadfeaturevaluesresponseheader.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadFeatureValuesResponse.Header -->

# Class Header (1.134.0)

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
The resource name of the EntityType from the ReadFeatureValuesRequest. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
|
`feature_descriptors` |
`MutableSequence[`
List of Feature metadata corresponding to each piece of ReadFeatureValuesResponse.EntityView.data. |

## Methods

### Header

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesgen_ai_tuning_service_googlecloudaiplatformv1be_3ba9cb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesgen_ai_tuning_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service -->

# Package gen_ai_tuning_service (1.134.0)

API documentation for `aiplatform_v1.services.gen_ai_tuning_service`

package.

## Classes

[GenAiTuningServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient)

A service for creating and managing GenAI Tuning Jobs.

[GenAiTuningServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient)

A service for creating and managing GenAI Tuning Jobs.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers)

API documentation for `aiplatform_v1.services.gen_ai_tuning_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesMetadata -->

# Class AutoMlTablesMetadata (1.134.0)

`AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Tables.

## Attribute |
|
|---|---|
Name |
Description |
`train_cost_milli_node_hours` |
`int`
Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget. |

## Methods

### AutoMlTablesMetadata

`AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Tables.

### AutoMlTablesMetadata

`AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Tables.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistfeatureonlinestoresresponse_googleclouda_3610d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistfeatureonlinestoresresponse_googlecloudai_3b816d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeatureonlinestoresresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse -->

# Class ListFeatureOnlineStoresResponse (1.134.0)

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

## Attributes |
|
|---|---|
Name |
Description |
`feature_online_stores` |
`MutableSequence[`
The FeatureOnlineStores matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureOnlineStoresRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureOnlineStoresResponse

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisttrialsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsRequest -->

# Class ListTrialsRequest (1.134.0)

`ListTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListTrials.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Study to list the Trial from. Format: `projects/{project}/locations/{location}/studies/{study}`
|
`page_token` |
`str`
Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages. |
`page_size` |
`int`
Optional. The number of Trials to retrieve per "page" of results. If unspecified, the service will pick an appropriate default. |

## Methods

### ListTrialsRequest

`ListTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListTrials.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesretrievalmetadata_googlecloudaiplatform_v1typeslis_fb6c00.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesretrievalmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrievalMetadata -->

# Class RetrievalMetadata (1.134.0)

`RetrievalMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to retrieval in the grounding flow.

## Attribute |
|
|---|---|
Name |
Description |
`google_search_dynamic_retrieval_score` |
`float`
Optional. Score indicating how likely information from Google Search could help answer the prompt. The score is in the range `[0, 1]` , where 0 is the least likely and 1 is
the most likely. This score is only populated when Google
Search grounding and dynamic retrieval is enabled. It will
be compared to the threshold to determine whether to trigger
Google Search.
|

## Methods

### RetrievalMetadata

`RetrievalMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to retrieval in the grounding flow.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisttensorboardexperimentsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse -->

# Class ListTensorboardExperimentsResponse (1.134.0)

```
ListTensorboardExperimentsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardExperiments.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_experiments` |
`MutableSequence[`
The TensorboardExperiments mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardExperimentsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardExperimentsResponse

```
ListTensorboardExperimentsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardExperiments.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeslisttensorboardtimeseriesresponse_googlecloudaip_a39cb7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslisttensorboardtimeseriesresponse_googlecloudaipl_0ff814.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslisttensorboardtimeseriesresponse_googlecloudaipla_b07585.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisttensorboardtimeseriesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse -->

# Class ListTensorboardTimeSeriesResponse (1.134.0)

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`MutableSequence[`
The TensorboardTimeSeries mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardTimeSeriesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardTimeSeriesResponse

```
ListTensorboardTimeSeriesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ListTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeaturevaluesresponseselectentity.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesResponse.SelectEntity -->

# Class SelectEntity (1.134.0)

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

## Attributes |
|
|---|---|
Name |
Description |
`offline_storage_deleted_entity_row_count` |
`int`
The count of deleted entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. |
`online_storage_deleted_entity_count` |
`int`
The count of deleted entities in the online storage. Each entity ID corresponds to one entity. |

## Methods

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeletefeaturerequest_googlecloudaiplatform_v1_310f2f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletefeaturerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureRequest -->

# Class DeleteFeatureRequest (1.134.0)

`DeleteFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeature. Request message for FeatureRegistryService.DeleteFeature.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Features to be deleted. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}/features/{feature}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}/features/{feature}`
|

## Methods

### DeleteFeatureRequest

`DeleteFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeature. Request message for FeatureRegistryService.DeleteFeature.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisttrialsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsRequest -->

# Class ListTrialsRequest (1.134.0)

`ListTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListTrials.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Study to list the Trial from. Format: `projects/{project}/locations/{location}/studies/{study}`
|
`page_token` |
`str`
Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages. |
`page_size` |
`int`
Optional. The number of Trials to retrieve per "page" of results. If unspecified, the service will pick an appropriate default. |

## Methods

### ListTrialsRequest

`ListTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListTrials.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgroundingmetadata_googlecloudaiplatformv1sche_d0fede.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgroundingmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingMetadata -->

# Class GroundingMetadata (1.134.0)

`GroundingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata returned to client when grounding is enabled.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`web_search_queries` |
`MutableSequence[str]`
Optional. Web search queries for the following-up web search. |
`search_entry_point` |
Optional. Google search entry for the following-up web searches. This field is a member of `oneof` _ `_search_entry_point` .
|
`retrieval_queries` |
`MutableSequence[str]`
Optional. Queries executed by the retrieval tools. |
`grounding_chunks` |
`MutableSequence[`
List of supporting references retrieved from specified grounding source. |
`grounding_supports` |
`MutableSequence[`
Optional. List of grounding support. |
`retrieval_metadata` |
Optional. Output only. Retrieval metadata. This field is a member of `oneof` _ `_retrieval_metadata` .
|
`google_maps_widget_context_token` |
`str`
Optional. Output only. Resource name of the Google Maps widget context token to be used with the PlacesContextElement widget to render contextual data. This is populated only for Google Maps grounding. This field is a member of `oneof` _ `_google_maps_widget_context_token` .
|
`source_flagging_uris` |
`MutableSequence[`
List of source flagging uris. This is currently populated only for Google Maps grounding. |

## Classes

### SourceFlaggingUri

`SourceFlaggingUri(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source content flagging uri for a place or review. This is currently populated only for Google Maps grounding.

## Methods

### GroundingMetadata

`GroundingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata returned to client when grounding is enabled.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictinstance_v1types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types -->

# Package instance_v1.types (1.134.0)

API documentation for `instance_v1.types`

package.

## Classes

[ImageClassificationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageClassificationPredictionInstance)

Prediction input format for Image Classification.

[ImageObjectDetectionPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageObjectDetectionPredictionInstance)

Prediction input format for Image Object Detection.

[ImageSegmentationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageSegmentationPredictionInstance)

Prediction input format for Image Segmentation.

[TextClassificationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextClassificationPredictionInstance)

Prediction input format for Text Classification.

[TextExtractionPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextExtractionPredictionInstance)

Prediction input format for Text Extraction.

[TextSentimentPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextSentimentPredictionInstance)

Prediction input format for Text Sentiment.

[VideoActionRecognitionPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.VideoActionRecognitionPredictionInstance)

Prediction input format for Video Action Recognition.

[VideoClassificationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.VideoClassificationPredictionInstance)

Prediction input format for Video Classification.

[VideoObjectTrackingPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.VideoObjectTrackingPredictionInstance)

Prediction input format for Video Object Tracking.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformprivateendpoint_googlecloudaiplatform_v1beta1servicesmodel_3a66f5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformprivateendpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PrivateEndpoint -->

# Class PrivateEndpoint (1.134.0)

```
PrivateEndpoint(
endpoint_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Represents a Vertex AI PrivateEndpoint resource.

## Classes

### PrivateServiceConnectConfig

```
PrivateServiceConnectConfig(
project_allowlist: typing.Optional[typing.Sequence[str]] = None,
)
```


Represents a Vertex AI PrivateServiceConnectConfig resource.

## Properties

### create_time

Time this resource was created.

### dedicated_endpoint_dns

The dedicated endpoint dns for this Endpoint.

This property is only available if dedicated endpoint is enabled. If dedicated endpoint is not enabled, this property returns None.

### dedicated_endpoint_enabled

The dedicated endpoint is enabled for this Endpoint.

This property will be true if dedicated endpoint is enabled.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### explain_http_uri

HTTP path to send explain requests to, used when calling `PrivateEndpoint.explain()`


### gca_resource

The underlying resource proto representation.

### health_http_uri

HTTP path to send health check requests to, used when calling `PrivateEndpoint.health_check()`


### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### network

The full name of the Google Compute Engine
[network](https://cloud.google.com/vpc/docs/vpc#networks) to which this
Endpoint should be peered.

Takes the format `projects/{project}/global/networks/{network}`

. Where
{project} is a project number, as in `12345`

, and {network} is a network name.

Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.

### predict_http_uri

HTTP path to send prediction requests to, used when calling `PrivateEndpoint.predict()`


### preview

Return an Endpoint instance with preview features enabled.

### private_service_connect_config

The Private Service Connect configuration for this Endpoint.

### resource_name

Full qualified resource name.

### traffic_split

A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel.

If a DeployedModel's ID is not listed in this map, then it receives no traffic.

The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment.

### update_time

Time this resource was last updated.

## Methods

### PrivateEndpoint

```
PrivateEndpoint(
endpoint_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves a PrivateEndpoint resource.

Example usage: my_private_endpoint = aiplatform.PrivateEndpoint( endpoint_name="projects/123/locations/us-central1/endpoints/1234567891234567890" )

```
or (when project and location are initialized)
my_private_endpoint = aiplatform.PrivateEndpoint(
endpoint_name="1234567891234567890"
)
```


Parameters |
|
|---|---|
Name |
Description |
`endpoint_name` |
`str`
Required. A fully-qualified endpoint resource name or endpoint ID. Example: "projects/123/locations/us-central1/endpoints/my_endpoint_id" or "my_endpoint_id" when project and location are initialized or passed. |
`project` |
`str`
Optional. Project to retrieve endpoint from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve endpoint from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the Endpoint being retrieved is not a PrivateEndpoint. |
`ImportError` |
If there is an issue importing the `urllib3` package. |

### create

```
create(
display_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
network: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync=True,
private_service_connect_config: typing.Union[
google.cloud.aiplatform.models.PrivateEndpoint.PrivateServiceConnectConfig,
None,
google.cloud.aiplatform_v1.types.service_networking.PrivateServiceConnectConfig,
] = None,
enable_request_response_logging=False,
request_response_logging_sampling_rate: typing.Optional[float] = None,
request_response_logging_bq_destination_table: typing.Optional[str] = None,
inference_timeout: typing.Optional[int] = None,
) -> google.cloud.aiplatform.models.PrivateEndpoint
```


Creates a new PrivateEndpoint.

Example usage: For PSA based private endpoint: my_private_endpoint = aiplatform.PrivateEndpoint.create( display_name="my_endpoint_name", project="my_project_id", location="us-central1", network="projects/123456789123/global/networks/my_vpc" )

```
or (when project and location are initialized)
my_private_endpoint = aiplatform.PrivateEndpoint.create(
display_name="my_endpoint_name",
network="projects/123456789123/global/networks/my_vpc"
)
```


For PSC based private endpoint: my_private_endpoint = aiplatform.PrivateEndpoint.create( display_name="my_endpoint_name", project="my_project_id", location="us-central1", private_service_connect=aiplatform.compat.types.service_networking.PrivateServiceConnectConfig( enable_private_service_connect=True, project_allowlist=["test-project"]), )

```
or (when project and location are initialized)
my_private_endpoint = aiplatform.PrivateEndpoint.create(
display_name="my_endpoint_name",
private_service_connect=aiplatform.compat.types.service_networking.PrivateServiceConnectConfig(
enable_private_service_connect=True,
project_allowlist=["test-project"]),
)
```


Parameters |
|
|---|---|
Name |
Description |
`private_service_connect_config` |
`typing.Union[google.cloud.aiplatform.models.PrivateEndpoint.PrivateServiceConnectConfig, NoneType, `
(aiplatform.compat.types.service_networking.PrivateServiceConnectConfig): |
`request_response_logging_sampling_rate` |
`float`
Optional. The request response logging sampling rate. If not set, default is 0.0. |
`request_response_logging_bq_destination_table` |
`str`
Optional. The request response logging bigquery destination. If not set, will create a table with name: |
`inference_timeout` |
`int`
Optional. It defines the prediction timeout, in seconds, for online predictions using cloud-based endpoints. This applies to either PSC endpoints, when private_service_connect_config is set, or dedicated endpoints, when dedicated_endpoint_enabled is true. |
`display_name` |
`str`
Required. The user-defined name of the Endpoint. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`project` |
`str`
Optional. Project to retrieve endpoint from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve endpoint from. If not set, location set in aiplatform.init will be used. |
`network` |
`str`
Optional. The full name of the Compute Engine network to which this Endpoint will be peered. E.g. "projects/123456789123/global/networks/my_vpc". Private services access must already be configured for the network. If left unspecified, the network set with aiplatform.init will be used. Cannot be set together with private_service_connect_config. |
`description` |
`str`
Optional. The description of the Endpoint. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`str`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_request_response_logging` |
`bool`
Optional. Whether to enable request & response logging for this endpoint. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A network must be instantiated when creating a |
`PrivateEndpoint.` |

Returns |
|
|---|---|
Type |
Description |
`endpoint (aiplatform.PrivateEndpoint)` |
Created endpoint. |

### delete

`delete(force: bool = False, sync: bool = True) -> None`


Deletes this Vertex AI PrivateEndpoint resource. If force is set to True, all models on this PrivateEndpoint will be undeployed prior to deletion.

Parameters |
|
|---|---|
Name |
Description |
`force` |
`bool`
Required. If force is set to True, all deployed models on this Endpoint will be undeployed first. Default is False. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`FailedPrecondition` |
If models are deployed on this Endpoint and force = False. |

### deploy

```
deploy(
model: google.cloud.aiplatform.models.Model,
deployed_model_display_name: typing.Optional[str] = None,
machine_type: typing.Optional[str] = None,
min_replica_count: int = 1,
max_replica_count: int = 1,
accelerator_type: typing.Optional[str] = None,
accelerator_count: typing.Optional[int] = None,
gpu_partition_size: typing.Optional[str] = None,
tpu_topology: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync=True,
disable_container_logging: bool = False,
traffic_percentage: typing.Optional[int] = 0,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
reservation_affinity_type: typing.Optional[str] = None,
reservation_affinity_key: typing.Optional[str] = None,
reservation_affinity_values: typing.Optional[typing.List[str]] = None,
spot: bool = False,
system_labels: typing.Optional[typing.Dict[str, str]] = None,
required_replica_count: typing.Optional[int] = 0,
autoscaling_target_cpu_utilization: typing.Optional[int] = None,
autoscaling_target_accelerator_duty_cycle: typing.Optional[int] = None,
autoscaling_target_request_count_per_minute: typing.Optional[int] = None,
autoscaling_target_pubsub_num_undelivered_messages: typing.Optional[int] = None,
autoscaling_pubsub_subscription_labels: typing.Optional[
typing.Dict[str, str]
] = None,
) -> None
```


Deploys a Model to the PrivateEndpoint.

Example Usage: PSA based private endpoint my_private_endpoint.deploy( model=my_model )

```
PSC based private endpoint
psc_endpoint.deploy(
model=first_model,
)
psc_endpoint.deploy(
model=second_model,
traffic_percentage=50,
)
psc_endpoint.deploy(
model=third_model,
traffic_percentage={
'first_model_id': 40,
'second_model_id': 30,
'third_model_id': 30
},
)
```


Parameters |
|
|---|---|
Name |
Description |
`deployed_model_display_name` |
`str`
Optional. The display name of the DeployedModel. If not provided upon creation, the Model's display_name is used. |
`machine_type` |
`str`
Optional. The type of machine. Not specifying machine type will result in model to be deployed with automatic resources. |
`min_replica_count` |
`int`
Optional. The minimum number of machine replicas this deployed model will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed. |
`max_replica_count` |
`int`
Optional. The maximum number of replicas this deployed model may be deployed on when the traffic against it increases. If requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the deployed model increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, the larger value of min_replica_count or 1 will be used. If value provided is smaller than min_replica_count, it will automatically be increased to be min_replica_count. |
`accelerator_type` |
`str`
Optional. Hardware accelerator type. Must also set accelerator_count if used. One of ACCELERATOR_TYPE_UNSPECIFIED, NVIDIA_TESLA_K80, NVIDIA_TESLA_P100, NVIDIA_TESLA_V100, NVIDIA_TESLA_P4, NVIDIA_TESLA_T4 |
`accelerator_count` |
`int`
Optional. The number of accelerators to attach to a worker replica. |
`gpu_partition_size` |
`str`
Optional. The GPU partition Size for Nvidia MIG. |
`tpu_topology` |
`str`
Optional. The TPU topology to use for the DeployedModel. Required for CloudTPU multihost deployments. |
`service_account` |
`str`
The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project. Users deploying the Model must have the |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Metadata describing the Model's input and output for explanation. |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. For more details, see |
`metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`traffic_percentage` |
`int`
Optional. Desired traffic to newly deployed model. Defaults to 0 if there are pre-existing deployed models. Defaults to 100 if there are no pre-existing deployed models. Defaults to 100 for PSA based private endpoint. Negative values should not be provided. Traffic of previously deployed models at the endpoint will be scaled down to accommodate new deployed model's traffic. Should not be provided if traffic_split is provided. |
`traffic_split` |
`Dict[str, int]`
Optional. Only supported by PSC base private endpoint. A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at the moment. Key for model being deployed is "0". Should not be provided if traffic_percentage is provided. |
`reservation_affinity_type` |
`str`
Optional. The type of reservation affinity. One of NO_RESERVATION, ANY_RESERVATION, SPECIFIC_RESERVATION, SPECIFIC_THEN_ANY_RESERVATION, SPECIFIC_THEN_NO_RESERVATION |
`reservation_affinity_key` |
`str`
Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use |
`reservation_affinity_values` |
`List[str]`
Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation. Format: 'projects/{project_id_or_number}/zones/{zone}/reservations/{reservation_name}' |
`spot` |
`bool`
Optional. Whether to schedule the deployment workload on spot VMs. |
`system_labels` |
`Dict[str, str]`
Optional. System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only. |
`required_replica_count` |
`int`
Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial model deployment/mutation is desired, with a value greater than or equal to 1 and fewer than or equal to min_replica_count. If set, the model deploy/mutate operation will succeed once available_replica_count reaches required_replica_count, and the rest of the replicas will be retried. |
`model` |
`aiplatform.Model`
Required. Model to be deployed. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### direct_predict

```
direct_predict(
inputs: typing.List,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Prediction
```


Makes a direct (gRPC) prediction against this Endpoint for a pre-built image.

Parameters |
|
|---|---|
Name |
Description |
`inputs` |
`List`
Required. The inputs that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### direct_predict_async

```
direct_predict_async(
inputs: typing.List,
*,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Makes an asynchronous direct (gRPC) prediction against this Endpoint for a pre-built image.

Example usage:

```
response = await my_endpoint.direct_predict_async(inputs=[...])
my_predictions = response.predictions
```
```


Parameters |
|
|---|---|
Name |
Description |
`inputs` |
`List`
Required. The inputs that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### direct_raw_predict

```
direct_raw_predict(
method_name: str, request: bytes, timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Makes a direct (gRPC) prediction request using arbitrary headers for a custom container.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
response = my_endpoint.direct_raw_predict(request=b'...')
```
```


Parameters |
|
|---|---|
Name |
Description |
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform prediction. |
`request` |
`bytes`
The body of the prediction request in bytes. |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### direct_raw_predict_async

```
direct_raw_predict_async(
method_name: str, request: bytes, timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Makes a direct (gRPC) prediction request for a custom container.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
response = await my_endpoint.direct_raw_predict(request=b'...')
```
```


Parameters |
|
|---|---|
Name |
Description |
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform prediction. |
`request` |
`bytes`
The body of the prediction request in bytes. |
`timeout` |
`Optional[float]`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
The resulting prediction. |

### explain

`explain()`


Make a prediction with explanations against this Endpoint.

Example usage: response = my_endpoint.explain(instances=[...]) my_explanations = response.explanations

Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`deployed_model_id` |
`str`
Optional. If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding this Endpoint's traffic split. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions, explanations, and Model ID. |

### explain_async

```
explain_async(
instances: typing.List[typing.Dict],
*,
parameters: typing.Optional[typing.Dict] = None,
deployed_model_id: typing.Optional[str] = None,
timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Make a prediction with explanations against this Endpoint.

Example usage:

```
response = await my_endpoint.explain_async(instances=[...])
my_explanations = response.explanations
```
```


Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`deployed_model_id` |
`str`
Optional. If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding this Endpoint's traffic split. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions, explanations, and Model ID. |

### health_check

`health_check() -> bool`


Makes a request to this PrivateEndpoint's health check URI. Must be within network that this PrivateEndpoint is in. This is only supported by PSA based private endpoint.

Example Usage: if my_private_endpoint.health_check(): print("PrivateEndpoint is healthy!")

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If a model has not been deployed a request cannot be made. |
`RuntimeError` |
If the endpoint is PSC based private endpoint. |

Returns |
|
|---|---|
Type |
Description |
`bool` |
Checks if calls can be made to this PrivateEndpoint. |

### invoke

```
invoke(
request_path: str,
body: bytes,
headers: typing.Dict[str, str],
deployed_model_id: typing.Optional[str] = None,
stream: bool = False,
timeout: typing.Optional[float] = None,
endpoint_override: typing.Optional[str] = None,
) -> typing.Iterator[bytes]
```


Makes a prediction request for arbitrary paths.

Example usage: my_endpoint = aiplatform.PrivateEndpoint(ENDPOINT_ID) response = my_endpoint.invoke( request_path="/v1/chat/completions", body = json.dumps(DATA).encode("utf-8"), headers = {'Content-Type':'application/json'}, endpoint_override="10.128.0.3", ) status_code = response.status_code results = json.dumps(response.text)

```
for stream_response in my_endpoint.invoke(
request_path="/v1/chat/completions",
body = json.dumps(DATA).encode("utf-8"),
headers = {'Content-Type':'application/json'},
stream=True,
endpoint_override="10.128.0.3",
):
stream_response_text = stream_response.decode('utf-8')
```


Parameters |
|
|---|---|
Name |
Description |
`request_path` |
`str`
The request url to the model server. The request path must be a string that starts with a forward slash. Root can't be accessed. |
`body` |
`bytes`
The body of the prediction request in bytes. This must not exceed 1.5 mb per request. |
`headers` |
`Dict[str, str]`
The header of the request as a dictionary. There are no restrictions on the header. |
`deployed_model_id` |
`str`
Optional. If specified, this InvokeRequest will be served by the chosen DeployedModel, overriding this Endpoint's traffic split. |
`stream` |
`bool`
If set to True, streaming will be enabled. |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |
`endpoint_override` |
`Optional[str]`
The Private Service Connect endpoint's IP address or DNS that points to the endpoint's service attachment. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If a endpoint override is not provided for PSC based endpoint. |
`ValueError` |
If a endpoint override is invalid for PSC based endpoint. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.models.PrivateEndpoint]
```


List all PrivateEndpoint resource instances.

Example Usage: my_private_endpoints = aiplatform.PrivateEndpoint.list()

```
or
my_private_endpoints = aiplatform.PrivateEndpoint.list(
filter='labels.my_label="my_label_value" OR display_name=!"old_endpoint"',
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`List[models.PrivateEndpoint]` |
A list of PrivateEndpoint resource objects. |

### list_models

```
list_models() -> (
typing.List[google.cloud.aiplatform_v1.types.endpoint.DeployedModel]
)
```


Returns a list of the models deployed to this Endpoint.

Returns |
|
|---|---|
Type |
Description |
`deployed_models (List[aiplatform.gapic.DeployedModel])` |
A list of the models deployed in this Endpoint. |

### predict

```
predict(
instances: typing.List,
parameters: typing.Optional[typing.Dict] = None,
endpoint_override: typing.Optional[str] = None,
) -> google.cloud.aiplatform.models.Prediction
```


Make a prediction against this PrivateEndpoint using a HTTP request.
For PSA based private endpoint, this method must be called within the
network the PrivateEndpoint is peered to. Otherwise, the predict() call
will fail with error code 404. To check, use `PrivateEndpoint.network`

.

For PSC based priviate endpoint, the project where caller credential are from must be allowlisted.

Example usage: PSA based private endpoint:

```
response = my_private_endpoint.predict(instances=[...], parameters={...})
my_predictions = response.predictions
PSC based private endpoint:
After creating PSC Endpoint pointing to the endpoint's
ServiceAttachment, use the PSC Endpoint IP Address or DNS as
endpoint_override.
psc_endpoint_address = "10.0.1.23"
or
psc_endpoint_address = "test.my.prediction"
response = my_private_endpoint.predict(instances=[...],
endpoint_override=psc_endpoint_address)
my_predictions = response.predictions
```


Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. Instance types mut be JSON serializable. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`endpoint_override` |
`Optional[str]`
The Private Service Connect endpoint's IP address or DNS that points to the endpoint's service attachment. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If a model has not been deployed a request cannot be made for PSA based endpoint. |
`ValueError` |
If a endpoint override is not provided for PSC based endpoint. |
`ValueError` |
If a endpoint override is invalid for PSC based endpoint. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction object with returned predictions and Model ID. |

### predict_async

```
predict_async(
instances: typing.List,
*,
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Prediction
```


Make an asynchronous prediction against this Endpoint. Example usage:

```
response = await my_endpoint.predict_async(instances=[...])
my_predictions = response.predictions
```
```


Parameters |
|
|---|---|
Name |
Description |
`instances` |
`List`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`float`
Optional. The timeout for this request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`prediction (aiplatform.Prediction)` |
Prediction with returned predictions and Model ID. |

### raw_predict

```
raw_predict(
body: bytes,
headers: typing.Dict[str, str],
endpoint_override: typing.Optional[str] = None,
) -> requests.models.Response
```


Make a prediction request using arbitrary headers.
This method must be called within the network the PrivateEndpoint is peered to.
Otherwise, the predict() call will fail with error code 404. To check, use `PrivateEndpoint.network`

.

Example usage: my_endpoint = aiplatform.PrivateEndpoint(ENDPOINT_ID)

```
# PSA based private endpint
response = my_endpoint.raw_predict(
body = b'{"instances":[{"feat_1":val_1, "feat_2":val_2}]}',
headers = {'Content-Type':'application/json'}
)
# PSC based private endpoint
response = my_endpoint.raw_predict(
body = b'{"instances":[{"feat_1":val_1, "feat_2":val_2}]}',
headers = {'Content-Type':'application/json'},
endpoint_override = "10.1.0.23"
)
status_code = response.status_code
results = json.dumps(response.text)
```


Parameters |
|
|---|---|
Name |
Description |
`body` |
`bytes`
The body of the prediction request in bytes. This must not exceed 1.5 mb per request. |
`headers` |
`Dict[str, str]`
The header of the request as a dictionary. There are no restrictions on the header. |
`endpoint_override` |
`Optional[str]`
The Private Service Connect endpoint's IP address or DNS that points to the endpoint's service attachment. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If a endpoint override is not provided for PSC based endpoint. |
`ValueError` |
If a endpoint override is invalid for PSC based endpoint. |

### stream_direct_predict

```
stream_direct_predict(
inputs_iterator: typing.Iterator[typing.List],
parameters: typing.Optional[typing.Dict] = None,
timeout: typing.Optional[float] = None,
) -> typing.Iterator[google.cloud.aiplatform.models.Prediction]
```


Makes a streaming direct (gRPC) prediction against this Endpoint for a pre-built image.

Parameters |
|
|---|---|
Name |
Description |
`inputs_iterator` |
`Iterator[List]`
Required. An iterator of the inputs that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`parameters` |
`Dict`
Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] |
`timeout` |
`Optional[float] :Yields: *predictions (Iterator[aiplatform.Prediction])* -- The resulting streamed predictions.`
Optional. The timeout for this request in seconds. |

### stream_direct_raw_predict

```
stream_direct_raw_predict(
method_name: str,
requests: typing.Iterator[bytes],
timeout: typing.Optional[float] = None,
) -> typing.Iterator[google.cloud.aiplatform.models.Prediction]
```


Makes a direct (gRPC) streaming prediction request for a custom container.

Example usage:

```
my_endpoint = aiplatform.Endpoint(ENDPOINT_ID)
for stream_response in my_endpoint.stream_direct_raw_predict(
request=b'...'
):
yield stream_response
```
```


Parameters |
|
|---|---|
Name |
Description |
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform prediction. |
`requests` |
`Iterator[bytes]`
The body of the prediction requests in bytes. |
`timeout` |
`Optional[float] :Yields: *predictions (Iterator[aiplatform.Prediction])* -- The resulting streamed predictions.`
Optional. The timeout for this request in seconds. |

### stream_raw_predict

```
stream_raw_predict(
body: bytes,
headers: typing.Dict[str, str],
endpoint_override: typing.Optional[str] = None,
) -> typing.Iterator[bytes]
```


Make a streaming prediction request using arbitrary headers.

Example usage: my_endpoint = aiplatform.PrivateEndpoint(ENDPOINT_ID)

```
# Prepare the request body
request_body = json.dumps({...}).encode('utf-8')
# Define the headers
headers = {
'Content-Type': 'application/json',
}
# Use stream_raw_predict to send the request and process the response
for stream_response in psc_endpoint.stream_raw_predict(
body=request_body,
headers=headers,
endpoint_override="10.128.0.26" # Replace with your actual endpoint
):
stream_response_text = stream_response.decode('utf-8')
```


Parameters |
|
|---|---|
Name |
Description |
`body` |
`bytes`
The body of the prediction request in bytes. This must not exceed 10 mb per request. |
`headers` |
`Dict[str, str]`
The header of the request as a dictionary. There are no restrictions on the header. |
`endpoint_override` |
`Optional[str] :Yields: *predictions (Iterator[bytes])* -- The streaming prediction results as lines of bytes.`
The Private Service Connect endpoint's IP address or DNS that points to the endpoint's service attachment. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If a endpoint override is not provided for PSC based endpoint. |
`ValueError` |
If a endpoint override is invalid for PSC based endpoint. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### undeploy

```
undeploy(
deployed_model_id: str,
sync=True,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
) -> None
```


Undeploys a deployed model from the PrivateEndpoint.

Example Usage: PSA based private endpoint: my_private_endpoint.undeploy( deployed_model_id="1234567891232567891" )

```
or
my_deployed_model_id = my_private_endpoint.list_models()[0].id
my_private_endpoint.undeploy(
deployed_model_id=my_deployed_model_id
)
```


Parameters |
|
|---|---|
Name |
Description |
`traffic_split` |
`Dict[str, int]`
Optional. Only supported by PSC based private endpoint. A map of DeployedModel IDs to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. Required if undeploying a model with non-zero traffic from an Endpoint with multiple deployed models. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at the moment. If a DeployedModel's ID is not listed in this map, then it receives no traffic. |
`deployed_model_id` |
`str`
Required. The ID of the DeployedModel to be undeployed from the PrivateEndpoint. Use PrivateEndpoint.list_models() to get the deployed model ID. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### undeploy_all

`undeploy_all(sync: bool = True) -> google.cloud.aiplatform.models.PrivateEndpoint`


Undeploys every model deployed to this PrivateEndpoint.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### update

```
update(
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.PrivateEndpoint
```


Updates a PrivateEndpoint.

Example usage: PSC based private endpoint

```
my_endpoint = my_endpoint.update(
display_name='my-updated-endpoint',
description='my updated description',
labels={'key': 'value'},
traffic_split={
'123456': 20,
'234567': 80,
},
)
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The display name of the Endpoint. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the Endpoint. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Endpoints. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`traffic_split` |
`Dict[str, int]`
Optional. Only supported by PSC based private endpoint A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `traffic_split` is set for PSA based private endpoint. |

Returns |
|
|---|---|
Type |
Description |
`Endpoint (aiplatform.Prediction)` |
Updated endpoint resource. |

### wait

`wait()`


Helper method that blocks until all futures are complete.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_garden_servicemodelgardenserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient -->

# Class ModelGardenServiceClient (1.134.0)

```
ModelGardenServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_garden_service.transports.base.ModelGardenServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_garden_service.transports.base.ModelGardenServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The interface of Model Garden Service.

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
`ModelGardenServiceTransport` |
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

### ModelGardenServiceClient

```
ModelGardenServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_garden_service.transports.base.ModelGardenServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_garden_service.transports.base.ModelGardenServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the model garden service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ModelGardenServiceTransport,Callable[..., ModelGardenServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ModelGardenServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### accept_publisher_model_eula

```
accept_publisher_model_eula(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.AcceptPublisherModelEulaRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
publisher_model: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.model_garden_service.PublisherModelEulaAcceptance
)
```


Accepts the EULA acceptance status of a publisher model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_accept_publisher_model_eula():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AcceptPublisherModelEulaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AcceptPublisherModelEulaRequest.html)(
parent="parent_value",
publisher_model="publisher_model_value",
)
# Make the request
response = client.[accept_publisher_model_eula](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_accept_publisher_model_eula)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelGardenService.AcceptPublisherModelEula. |
`parent` |
`str`
Required. The project requesting access for named model. The format is |
`publisher_model` |
`str`
Required. The name of the PublisherModel resource. Format: |
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
Response message for [ModelGardenService.UpdatePublisherModelEula][]. |

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

### check_publisher_model_eula_acceptance

```
check_publisher_model_eula_acceptance(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.CheckPublisherModelEulaAcceptanceRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
publisher_model: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.model_garden_service.PublisherModelEulaAcceptance
)
```


Checks the EULA acceptance status of a publisher model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_check_publisher_model_eula_acceptance():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CheckPublisherModelEulaAcceptanceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckPublisherModelEulaAcceptanceRequest.html)(
parent="parent_value",
publisher_model="publisher_model_value",
)
# Make the request
response = client.[check_publisher_model_eula_acceptance](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_check_publisher_model_eula_acceptance)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [ModelGardenService.CheckPublisherModelEula][]. |
`parent` |
`str`
Required. The project requesting access for named model. The format is |
`publisher_model` |
`str`
Required. The name of the PublisherModel resource. Format: |
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
Response message for [ModelGardenService.UpdatePublisherModelEula][]. |

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

### deploy

```
deploy(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.DeployRequest,
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
) -> google.api_core.operation.Operation
```


Deploys a model to a new endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_deploy():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeployRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.html)(
publisher_model_name="publisher_model_name_value",
destination="destination_value",
)
# Make the request
operation = client.[deploy](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_deploy)(request=request)
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
The request object. Request message for ModelGardenService.Deploy. |
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

### deploy_publisher_model

```
deploy_publisher_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.DeployPublisherModelRequest,
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
) -> google.api_core.operation.Operation
```


Deploys publisher models.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_deploy_publisher_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeployPublisherModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployPublisherModelRequest.html)(
model="model_value",
destination="destination_value",
)
# Make the request
operation = client.[deploy_publisher_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_deploy_publisher_model)(request=request)
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
The request object. Request message for ModelGardenService.DeployPublisherModel. |
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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### export_publisher_model

```
export_publisher_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.ExportPublisherModelRequest,
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
) -> google.api_core.operation.Operation
```


Exports a publisher model to a user provided Google Cloud Storage bucket.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_export_publisher_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
destination = aiplatform_v1beta1.[GcsDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GcsDestination.html)()
destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ExportPublisherModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelRequest.html)(
name="name_value",
destination=destination,
parent="parent_value",
)
# Make the request
operation = client.[export_publisher_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_export_publisher_model)(request=request)
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
The request object. Request message for ModelGardenService.ExportPublisherModel. |
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
`ModelGardenServiceClient` |
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
`ModelGardenServiceClient` |
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
`ModelGardenServiceClient` |
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

### get_publisher_model

```
get_publisher_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.GetPublisherModelRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.publisher_model.PublisherModel
```


Gets a Model Garden publisher model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_publisher_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPublisherModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPublisherModelRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_publisher_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_get_publisher_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelGardenService.GetPublisherModel |
`name` |
`str`
Required. The name of the PublisherModel resource. Format: |
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
A Model Garden Publisher Model. |

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

### list_publisher_models

```
list_publisher_models(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
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
google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers.ListPublisherModelsPager
)
```


Lists publisher models in Model Garden.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_publisher_models():
# Create a client
client = aiplatform_v1beta1.
```[ModelGardenServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPublisherModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_publisher_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_garden_service_ModelGardenServiceClient_list_publisher_models)(request=request)
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
The request object. Request message for ModelGardenService.ListPublisherModels. |
`parent` |
`str`
Required. The name of the Publisher from which to list the PublisherModels. Format: |
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
Response message for ModelGardenService.ListPublisherModels. Iterating over this object will yield results and resolve additional pages automatically. |

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

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

### parse_publisher_model_path

`parse_publisher_model_path(path: str) -> typing.Dict[str, str]`


Parses a publisher_model path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### publisher_model_path

`publisher_model_path(publisher: str, model: str) -> str`


Returns a fully-qualified publisher_model string.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesdeployment_resource_pool_servicedeploymentreso_cfe0f3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdeployment_resource_pool_servicedeploymentresou_12f805.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdeployment_resource_pool_servicedeploymentresourcepoolserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient -->

# Class DeploymentResourcePoolServiceClient (1.134.0)

```
DeploymentResourcePoolServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service that manages the DeploymentResourcePool resource.

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
`DeploymentResourcePoolServiceTransport` |
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

### DeploymentResourcePoolServiceClient

```
DeploymentResourcePoolServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.transports.base.DeploymentResourcePoolServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the deployment resource pool service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,DeploymentResourcePoolServiceTransport,Callable[..., DeploymentResourcePoolServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the DeploymentResourcePoolServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_deployment_resource_pool

```
create_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.CreateDeploymentResourcePoolRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform_v1.types.deployment_resource_pool.DeploymentResourcePool
] = None,
deployment_resource_pool_id: typing.Optional[str] = None,
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


Create a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[CreateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDeploymentResourcePoolRequest.html)(
parent="parent_value",
deployment_resource_pool=deployment_resource_pool,
deployment_resource_pool_id="deployment_resource_pool_id_value",
)
# Make the request
operation = client.[create_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_create_deployment_resource_pool)(request=request)
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
The request object. Request message for CreateDeploymentResourcePool method. |
`parent` |
`str`
Required. The parent location resource where this DeploymentResourcePool will be created. Format: |
`deployment_resource_pool` |
Required. The DeploymentResourcePool to create. This corresponds to the |
`deployment_resource_pool_id` |
`str`
Required. The ID to use for the DeploymentResourcePool, which will become the final component of the DeploymentResourcePool's resource name. The maximum length is 63 characters, and valid characters are |
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

### delete_deployment_resource_pool

```
delete_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.DeleteDeploymentResourcePoolRequest,
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


Delete a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_delete_deployment_resource_pool)(request=request)
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
The request object. Request message for DeleteDeploymentResourcePool method. |
`name` |
`str`
Required. The name of the DeploymentResourcePool to delete. Format: |
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

### deployment_resource_pool_path

```
deployment_resource_pool_path(
project: str, location: str, deployment_resource_pool: str
) -> str
```


Returns a fully-qualified deployment_resource_pool string.

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
`DeploymentResourcePoolServiceClient` |
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
`DeploymentResourcePoolServiceClient` |
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
`DeploymentResourcePoolServiceClient` |
The constructed client. |

### get_deployment_resource_pool

```
get_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.GetDeploymentResourcePoolRequest,
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
) -> google.cloud.aiplatform_v1.types.deployment_resource_pool.DeploymentResourcePool
```


Get a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDeploymentResourcePoolRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_get_deployment_resource_pool)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for GetDeploymentResourcePool method. |
`name` |
`str`
Required. The name of the DeploymentResourcePool to retrieve. Format: |
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
A description of resources that can be shared by multiple DeployedModels, whose underlying specification consists of a DedicatedResources. |

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

### list_deployment_resource_pools

```
list_deployment_resource_pools(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
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
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsPager
)
```


List DeploymentResourcePools in a location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_deployment_resource_pools():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListDeploymentResourcePoolsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_deployment_resource_pools](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_list_deployment_resource_pools)(request=request)
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
The request object. Request message for ListDeploymentResourcePools method. |
`parent` |
`str`
Required. The parent Location which owns this collection of DeploymentResourcePools. Format: |
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
Response message for ListDeploymentResourcePools method. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_deployment_resource_pool_path

`parse_deployment_resource_pool_path(path: str) -> typing.Dict[str, str]`


Parses a deployment_resource_pool path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### query_deployed_models

```
query_deployed_models(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
dict,
]
] = None,
*,
deployment_resource_pool: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsPager
)
```


List DeployedModels that have been deployed on this DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_query_deployed_models():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryDeployedModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsRequest.html)(
deployment_resource_pool="deployment_resource_pool_value",
)
# Make the request
page_result = client.[query_deployed_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_query_deployed_models)(request=request)
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
The request object. Request message for QueryDeployedModels method. |
`deployment_resource_pool` |
`str`
Required. The name of the target DeploymentResourcePool to query. Format: |
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
Response message for QueryDeployedModels method. Iterating over this object will yield results and resolve additional pages automatically. |

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

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

### update_deployment_resource_pool

```
update_deployment_resource_pool(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.UpdateDeploymentResourcePoolRequest,
dict,
]
] = None,
*,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform_v1.types.deployment_resource_pool.DeploymentResourcePool
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


Update a DeploymentResourcePool.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_deployment_resource_pool():
# Create a client
client = aiplatform_v1.
```[DeploymentResourcePoolServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html)()
# Initialize request argument(s)
deployment_resource_pool = aiplatform_v1.[DeploymentResourcePool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeploymentResourcePool.html)()
deployment_resource_pool.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[UpdateDeploymentResourcePoolRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDeploymentResourcePoolRequest.html)(
deployment_resource_pool=deployment_resource_pool,
)
# Make the request
operation = client.[update_deployment_resource_pool](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient.html#google_cloud_aiplatform_v1_services_deployment_resource_pool_service_DeploymentResourcePoolServiceClient_update_deployment_resource_pool)(request=request)
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
The request object. Request message for UpdateDeploymentResourcePool method. |
`deployment_resource_pool` |
Required. The DeploymentResourcePool to update. The DeploymentResourcePool's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The list of fields to update. This corresponds to the |
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformpipelinejobschedule___googlecloudaiplatform_v1beta1typese_605562.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformpipelinejobschedule___googlecloudaiplatform_v1beta1typesex_13f50f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformpipelinejobschedule.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJobSchedule -->

# Class PipelineJobSchedule (1.134.0)

```
PipelineJobSchedule(
pipeline_job: google.cloud.aiplatform.pipeline_jobs.PipelineJob,
display_name: str,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
)
```


Retrieves a PipelineJobSchedule resource and instantiates its representation.

## Parameters |
|
|---|---|
Name |
Description |
`pipeline_job` |
`PipelineJob`
Required. PipelineJob used to init the schedule. |
`display_name` |
`str`
Required. The user-defined name of this PipelineJobSchedule. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to create this PipelineJobSchedule. Overrides credentials set in aiplatform.init. |
`project` |
`str`
Optional. The project that you want to run this PipelineJobSchedule in. If not set, the project used for the PipelineJob will be used. |
`location` |
`str`
Optional. Location to create PipelineJobSchedule. If not set, location used for the PipelineJob will be used. |

## Properties

### allow_queueing

Whether current Schedule allows queueing.

### create_time

Time this resource was created.

### cron

Current Schedule cron.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### max_concurrent_run_count

Current Schedule max_concurrent_run_count.

### max_run_count

Current Schedule max_run_count.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### state

Current Schedule state.

### update_time

Time this resource was last updated.

## Methods

### create

```
create(
cron: str,
start_time: typing.Optional[str] = None,
end_time: typing.Optional[str] = None,
allow_queueing: bool = False,
max_run_count: typing.Optional[int] = None,
max_concurrent_run_count: int = 1,
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
create_request_timeout: typing.Optional[float] = None,
) -> None
```


Create a PipelineJobSchedule.

Parameters |
|
|---|---|
Name |
Description |
`cron` |
`str`
Required. Time specification (cron schedule expression) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix: "CRON_TZ=${IANA_TIME_ZONE}" or "TZ=${IANA_TIME_ZONE}". The ${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 * * * *", or "TZ=America/New_York 1 * * * *". |
`start_time` |
`str`
Optional. Timestamp after which the first run can be scheduled. If unspecified, it defaults to the schedule creation timestamp. |
`end_time` |
`str`
Optional. Timestamp after which no more runs will be scheduled. If unspecified, then runs will be scheduled indefinitely. |
`allow_queueing` |
`bool`
Optional. Whether new scheduled runs can be queued when max_concurrent_runs limit is reached. |
`max_run_count` |
`int`
Optional. Maximum run count of the schedule. If specified, The schedule will be completed when either started_run_count >= max_run_count or when end_time is reached. Must be positive and <= 2^63-1. |
`max_concurrent_run_count` |
`int`
Optional. Maximum number of runs that can be started concurrently for this PipelineJobSchedule. |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |
`network` |
`str`
Optional. The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the network set in aiplatform.init will be used. Otherwise, the job is not peered with any network. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Helper method that return True is Schedule is done. False otherwise.

### get

```
get(
schedule_id: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.Any
```


Get a Vertex AI Schedule for the given resource_name.

Parameters |
|
|---|---|
Name |
Description |
`schedule_id` |
`str`
Required. Schedule ID used to identify or locate the schedule. |
`project` |
`str`
Optional. Project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.pipeline_job_schedules.PipelineJobSchedule]
```


List all instances of this PipelineJobSchedule resource.

Example Usage:

aiplatform.PipelineJobSchedule.list( filter='display_name="experiment_a27"', order_by='create_time desc' )

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |

### list_jobs

```
list_jobs(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
enable_simple_view: bool = True,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.pipeline_jobs.PipelineJob]
```


List all PipelineJob 's created by this PipelineJobSchedule.

Example usage:

pipeline_job_schedule.list_jobs(order_by='create_time_desc')

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`enable_simple_view` |
`bool`
Optional. Whether to pass the |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |

### pause

`pause() -> None`


Starts asynchronous pause on the Schedule.

Changes Schedule state from State.ACTIVE to State.PAUSED.

### resume

`resume(catch_up: bool = True) -> None`


Starts asynchronous resume on the Schedule.

Changes Schedule state from State.PAUSED to State.ACTIVE.

Parameter |
|
|---|---|
Name |
Description |
`catch_up` |
`bool`
Optional. Whether to backfill missed runs when the Schedule is resumed from State.PAUSED. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
display_name: typing.Optional[str] = None,
cron: typing.Optional[str] = None,
start_time: typing.Optional[str] = None,
end_time: typing.Optional[str] = None,
allow_queueing: typing.Optional[bool] = None,
max_run_count: typing.Optional[int] = None,
max_concurrent_run_count: typing.Optional[int] = None,
) -> None
```


Update an existing PipelineJobSchedule.

Example usage:

pipeline_job_schedule.update( display_name='updated-display-name', cron='* * * * *', )

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of this PipelineJobSchedule. |
`cron` |
`str`
Optional. Time specification (cron schedule expression) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix: "CRON_TZ=${IANA_TIME_ZONE}" or "TZ=${IANA_TIME_ZONE}". The ${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 * * * *", or "TZ=America/New_York 1 * * * *". |
`start_time` |
`str`
Optional. Timestamp after which the first run can be scheduled. If unspecified, it defaults to the schedule creation timestamp. |
`end_time` |
`str`
Optional. Timestamp after which no more runs will be scheduled. If unspecified, then runs will be scheduled indefinitely. |
`allow_queueing` |
`bool`
Optional. Whether new scheduled runs can be queued when max_concurrent_runs limit is reached. |
`max_run_count` |
`int`
Optional. Maximum run count of the schedule. If specified, The schedule will be completed when either started_run_count >= max_run_count or when end_time is reached. Must be positive and <= 2^63-1. |
`max_concurrent_run_count` |
`int`
Optional. Maximum number of runs that can be started concurrently for this PipelineJobSchedule. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
User tried to call update() before create(). |

### wait

`wait() -> None`


Wait for all runs scheduled by this Schedule to complete.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesexamples_googlecloudaiplatform_v1typeslistfe_66e9e0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexamples_googlecloudaiplatform_v1typeslistfea_cfff83.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexamples.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Examples -->

# Class Examples (1.134.0)

`Examples(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Example-based explainability that returns the nearest neighbors from the provided dataset.

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
`example_gcs_source` |
The Cloud Storage input instances. This field is a member of `oneof` _ `source` .
|
`nearest_neighbor_search_config` |
`google.protobuf.struct_pb2.Value`
The full configuration for the generated index, the semantics are the same as metadata and should match `NearestNeighborSearchConfig ` __.
This field is a member of `oneof` _ `config` .
|
`presets` |
Simplified preset configuration, which automatically sets configuration values based on the desired query speed-precision trade-off and modality. This field is a member of `oneof` _ `config` .
|
`gcs_source` |
The Cloud Storage locations that contain the instances to be indexed for approximate nearest neighbor search. |
`neighbor_count` |
`int`
The number of neighbors to return when querying for examples. |

## Classes

### ExampleGcsSource

`ExampleGcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage input instances.

## Methods

### Examples

`Examples(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Example-based explainability that returns the nearest neighbors from the provided dataset.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeatureviewsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsRequest -->

# Class ListFeatureViewsRequest (1.134.0)

`ListFeatureViewsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViews.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureOnlineStore to list FeatureViews. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}`
|
`filter` |
`str`
Lists the FeatureViews that match the filter expression. The following filters are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`>=` , and `<>` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality as well as key
presence.
Examples:
- `create_time > \"2020-01-31T15:30:00.000000Z\" OR update_time > \"2020-01-31T15:30:00.000000Z\"`
--> FeatureViews created or updated after
2020-01-31T15:30:00.000000Z.
- `labels.active = yes AND labels.env = prod` -->
FeatureViews having both (active: yes) and (env: prod)
labels.
- `labels.env: *` --> Any FeatureView which has a label
with 'env' as the key.
|
`page_size` |
`int`
The maximum number of FeatureViews to return. The service may return fewer than this value. If unspecified, at most 1000 FeatureViews will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeatureOnlineStoreAdminService.ListFeatureViews call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeatureOnlineStoreAdminService.ListFeatureViews must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `feature_view_id`
- `create_time`
- `update_time`
|

## Methods

### ListFeatureViewsRequest

`ListFeatureViewsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.ListFeatureViews.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesvertex_rag_data_service_googlecloudaiplat_e5b3b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesvertex_rag_data_service_googlecloudaiplatf_5b306a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_data_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service -->

# Package vertex_rag_data_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.vertex_rag_data_service`

package.

## Classes

[VertexRagDataServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient)

A service for managing user data for RAG.

[VertexRagDataServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.VertexRagDataServiceClient)

A service for managing user data for RAG.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers)

API documentation for `aiplatform_v1beta1.services.vertex_rag_data_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistragfilesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesRequest -->

# Class ListRagFilesRequest (1.134.0)

`ListRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ListRagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the RagCorpus from which to list the RagFiles. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListRagFilesResponse.next_page_token of the previous VertexRagDataService.ListRagFiles call. |

## Methods

### ListRagFilesRequest

`ListRagFilesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ListRagFiles.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragmanageddbconfigunprovisioned_googlecloudaiplatf_bb1972.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragmanageddbconfigunprovisioned.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagManagedDbConfig.Unprovisioned -->

# Class Unprovisioned (1.134.0)

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

## Methods

### Unprovisioned

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletefeaturevaluesresponseselectentity.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesResponse.SelectEntity -->

# Class SelectEntity (1.134.0)

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.

## Attributes |
|
|---|---|
Name |
Description |
`offline_storage_deleted_entity_row_count` |
`int`
The count of deleted entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. |
`online_storage_deleted_entity_count` |
`int`
The count of deleted entities in the online storage. Each entity ID corresponds to one entity. |

## Methods

### SelectEntity

`SelectEntity(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectEntity option.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbatchpredictionjob____googlecloudaiplatform_v1type_3d350d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchpredictionjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchPredictionJob -->

# Class BatchPredictionJob (1.134.0)

`BatchPredictionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the BatchPredictionJob. |
`display_name` |
`str`
Required. The user-defined name of this BatchPredictionJob. |
`model` |
`str`
The name of the Model resource that produces the predictions via this job, must share the same ancestor Location. Starting this job has no impact on any existing deployments of the Model and their resources. Exactly one of model and unmanaged_container_model must be set. The model resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
if no version is specified, the default version will be
deployed.
The model resource could also be a publisher model. Example:
`publishers/{publisher}/models/{model}` or
`projects/{project}/locations/{location}/publishers/{publisher}/models/{model}`
|
`model_version_id` |
`str`
Output only. The version ID of the Model that produces the predictions via this job. |
`unmanaged_container_model` |
Contains model information necessary to perform batch prediction without requiring uploading to model registry. Exactly one of model and unmanaged_container_model must be set. |
`input_config` |
Required. Input configuration of the instances on which predictions are performed. The schema of any single instance may be specified via the [Model's][google.cloud.aiplatform.v1.BatchPredictionJob.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri. |
`instance_config` |
Configuration for how to convert batch prediction input instances to the prediction instances that are sent to the Model. |
`model_parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the predictions. The schema of the parameters may be specified via the [Model's][google.cloud.aiplatform.v1.BatchPredictionJob.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] parameters_schema_uri. |
`output_config` |
Required. The Configuration specifying where output predictions should be written. The schema of any single prediction may be specified as a concatenation of [Model's][google.cloud.aiplatform.v1.BatchPredictionJob.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri and prediction_schema_uri. |
`dedicated_resources` |
The config of resources used by the Model during the batch prediction. If the Model supports DEDICATED_RESOURCES this config may be provided (and the job will use these resources), if the Model doesn't support AUTOMATIC_RESOURCES, this config must be provided. |
`service_account` |
`str`
The service account that the DeployedModel's container runs as. If not specified, a system generated one will be used, which has minimal permissions and the custom container, if used, may not have enough permission to access other Google Cloud resources. Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`manual_batch_tuning_parameters` |
Immutable. Parameters configuring the batch behavior. Currently only applicable when dedicated_resources are used (in other cases Vertex AI does the tuning itself). |
`generate_explanation` |
`bool`
Generate explanation with the batch prediction results. When set to `true` , the batch prediction output changes
based on the `predictions_format` field of the
BatchPredictionJob.output_config
object:
- `bigquery` : output includes a column named
`explanation` . The value is a struct that conforms to
the Explanation
object.
- `jsonl` : The JSON objects on each line include an
additional entry keyed `explanation` . The value of the
entry is a JSON object that conforms to the
Explanation
object.
- `csv` : Generating explanations for CSV format is not
supported.
If this field is set to true, either the
Model.explanation_spec
or
explanation_spec
must be populated.
|
`explanation_spec` |
Explanation configuration for this BatchPredictionJob. Can be specified only if generate_explanation is set to `true` .
This value overrides the value of
Model.explanation_spec.
All fields of
explanation_spec
are optional in the request. If a field of the
explanation_spec
object is not populated, the corresponding field of the
Model.explanation_spec
object is inherited.
|
`output_info` |
Output only. Information further describing the output of this job. |
`state` |
Output only. The detailed state of the job. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when the job's state is JOB_STATE_FAILED or JOB_STATE_CANCELLED. |
`partial_failures` |
`MutableSequence[google.rpc.status_pb2.Status]`
Output only. Partial failures encountered. For example, single files that can't be read. This field never exceeds 20 entries. Status details fields contain standard Google Cloud error details. |
`resources_consumed` |
Output only. Information about resources that had been consumed by this job. Provided in real time at best effort basis, as well as a final value once the job completes. Note: This field currently may be not populated for batch predictions that use AutoML Models. |
`completion_stats` |
Output only. Statistics on completed and failed prediction instances. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the BatchPredictionJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the BatchPredictionJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the BatchPredictionJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the BatchPredictionJob was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize BatchPredictionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a BatchPredictionJob. If this is set, then all resources created by the BatchPredictionJob will be encrypted with the provided encryption key. |
`disable_container_logging` |
`bool`
For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by
default. Please note that the logs incur cost, which are
subject to `Cloud Logging
pricing |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### InputConfig

`InputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the input to BatchPredictionJob. See Model.supported_input_storage_formats for Model's supported input formats, and how instances should be expressed via any of them.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### InstanceConfig

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

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

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes this job's output. Supplements output_config.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### BatchPredictionJob

`BatchPredictionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typestrialparameter_googlecloudaiplatform_v1typesmode_ff859c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestrialparameter_googlecloudaiplatform_v1typesmodel_d86eaf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestrialparameter_googlecloudaiplatform_v1typesmodelm_984f97.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestrialparameter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Trial.Parameter -->

# Class Parameter (1.134.0)

`Parameter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a parameter to be tuned.

## Attributes |
|
|---|---|
Name |
Description |
`parameter_id` |
`str`
Output only. The ID of the parameter. The parameter should be defined in [StudySpec's Parameters][google.cloud.aiplatform.v1.StudySpec.parameters]. |
`value` |
`google.protobuf.struct_pb2.Value`
Output only. The value of the parameter. `number_value`
will be set if a parameter defined in StudySpec is in type
'INTEGER', 'DOUBLE' or 'DISCRETE'. `string_value` will be
set if a parameter defined in StudySpec is in type
'CATEGORICAL'.
|

## Methods

### Parameter

`Parameter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a parameter to be tuned.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringstatsanomaliesfeaturehistoricstatsanomalies.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringStatsAnomalies.FeatureHistoricStatsAnomalies -->

# Class FeatureHistoricStatsAnomalies (1.134.0)

```
FeatureHistoricStatsAnomalies(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Historical Stats (and Anomalies) for a specific Feature.

## Attributes |
|
|---|---|
Name |
Description |
`feature_display_name` |
`str`
Display Name of the Feature. |
`threshold` |
Threshold for anomaly detection. |
`training_stats` |
Stats calculated for the Training Dataset. |
`prediction_stats` |
`MutableSequence[`
A list of historical stats generated by different time window's Prediction Dataset. |

## Methods

### FeatureHistoricStatsAnomalies

```
FeatureHistoricStatsAnomalies(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Historical Stats (and Anomalies) for a specific Feature.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlimage_f1129c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlimageclassificationmetadatasuccessfulstopreason.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationMetadata.SuccessfulStopReason -->

# Class SuccessfulStopReason (1.134.0)

Further training of the Model ceased to increase its quality, since it already has converged.

Methods

SuccessfulStopReason

SuccessfulStopReason(value)

SuccessfulStopReason

SuccessfulStopReason(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewoptimizedconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.OptimizedConfig -->

# Class OptimizedConfig (1.134.0)

`OptimizedConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for FeatureViews created in Optimized FeatureOnlineStore.

## Attribute |
|
|---|---|
Name |
Description |
`automatic_resources` |
Optional. A description of resources that the FeatureView uses, which to large degree are decided by Vertex AI, and optionally allows only a modest additional configuration. If min_replica_count is not set, the default value is 2. If max_replica_count is not set, the default value is 6. The max allowed replica count is 1000. |

## Methods

### OptimizedConfig

`OptimizedConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for FeatureViews created in Optimized FeatureOnlineStore.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragmanageddbconfigunprovisioned_googleclouda_9aa855.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragmanageddbconfigunprovisioned_googlecloudai_765bc1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragmanageddbconfigunprovisioned.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagManagedDbConfig.Unprovisioned -->

# Class Unprovisioned (1.134.0)

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

## Methods

### Unprovisioned

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadfeaturevaluesresponseheader.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesResponse.Header -->

# Class Header (1.134.0)

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
The resource name of the EntityType from the ReadFeatureValuesRequest. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
|
`feature_descriptors` |
`MutableSequence[`
List of Feature metadata corresponding to each piece of ReadFeatureValuesResponse.EntityView.data. |

## Methods

### Header

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigtrainingdataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.TrainingDataset -->

# Class TrainingDataset (1.134.0)

`TrainingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training Dataset information.

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
`dataset` |
`str`
The resource name of the Dataset used to train this Model. This field is a member of `oneof` _ `data_source` .
|
`gcs_source` |
The Google Cloud Storage uri of the unmanaged Dataset used to train this Model. This field is a member of `oneof` _ `data_source` .
|
`bigquery_source` |
The BigQuery table of the unmanaged Dataset used to train this Model. This field is a member of `oneof` _ `data_source` .
|
`data_format` |
`str`
Data format of the dataset, only applicable if the input is from Google Cloud Storage. The possible formats are: "tf-record" The source file is a TFRecord file. "csv" The source file is a CSV file. "jsonl" The source file is a JSONL file. |
`target_field` |
`str`
The target field name the model is to predict. This field will be excluded when doing Predict and (or) Explain for the training data. |
`logging_sampling_strategy` |
Strategy to sample data from Training Dataset. If not set, we process the whole dataset. |

## Methods

### TrainingDataset

`TrainingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training Dataset information.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicessession_servicesessionserviceclient_google_3b0b1d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicessession_servicesessionserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient -->

# Class SessionServiceClient (1.134.0)

```
SessionServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.session_service.transports.base.SessionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.session_service.transports.base.SessionServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that manages Vertex Session related resources.

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
`SessionServiceTransport` |
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

### SessionServiceClient

```
SessionServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.session_service.transports.base.SessionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.session_service.transports.base.SessionServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the session service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,SessionServiceTransport,Callable[..., SessionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the SessionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### append_event

```
append_event(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.AppendEventRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
event: typing.Optional[
google.cloud.aiplatform_v1beta1.types.session.SessionEvent
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.session_service.AppendEventResponse
```


Appends an event to a given session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_append_event():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
event = aiplatform_v1beta1.[SessionEvent](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SessionEvent.html)()
event.author = "author_value"
event.invocation_id = "invocation_id_value"
request = aiplatform_v1beta1.[AppendEventRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AppendEventRequest.html)(
name="name_value",
event=event,
)
# Make the request
response = client.[append_event](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_append_event)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for SessionService.AppendEvent. |
`name` |
`str`
Required. The resource name of the session to append event to. Format: |
`event` |
Required. The event to append to the session. This corresponds to the |
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
Response message for SessionService.AppendEvent. |

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

### create_session

```
create_session(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.CreateSessionRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
session: typing.Optional[
google.cloud.aiplatform_v1beta1.types.session.Session
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


Creates a new xref_Session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
session = aiplatform_v1beta1.[Session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session.html)()
session.user_id = "user_id_value"
request = aiplatform_v1beta1.[CreateSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSessionRequest.html)(
parent="parent_value",
session=session,
)
# Make the request
operation = client.[create_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_create_session)(request=request)
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
The request object. Request message for SessionService.CreateSession. |
`parent` |
`str`
Required. The resource name of the location to create the session in. Format: |
`session` |
Required. The session to create. This corresponds to the |
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
An object representing a long-running operation. The result type for the operation will be Session A session contains a set of actions between users and Vertex agents. |

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

### delete_session

```
delete_session(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.DeleteSessionRequest,
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


Deletes details of the specific xref_Session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSessionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_delete_session)(request=request)
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
The request object. Request message for SessionService.DeleteSession. |
`name` |
`str`
Required. The resource name of the session. Format: |
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
`SessionServiceClient` |
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
`SessionServiceClient` |
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
`SessionServiceClient` |
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

### get_session

```
get_session(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.GetSessionRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.session.Session
```


Gets details of the specific xref_Session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetSessionRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_get_session)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for SessionService.GetSession. |
`name` |
`str`
Required. The resource name of the session. Format: |
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
A session contains a set of actions between users and Vertex agents. |

### list_events

```
list_events(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
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
) -> google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsPager
```


Lists xref_Events in a given session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_events():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListEventsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_events](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_list_events)(request=request)
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
The request object. Request message for SessionService.ListEvents. |
`parent` |
`str`
Required. The resource name of the session to list events from. Format: |
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
Response message for SessionService.ListEvents. Iterating over this object will yield results and resolve additional pages automatically. |

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

### list_sessions

```
list_sessions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
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
) -> google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsPager
```


Lists xref_Sessions in a given reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_sessions():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSessionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_sessions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_list_sessions)(request=request)
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
The request object. Request message for SessionService.ListSessions. |
`parent` |
`str`
Required. The resource name of the location to list sessions from. Format: |
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
Response message for SessionService.ListSessions. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### parse_session_event_path

`parse_session_event_path(path: str) -> typing.Dict[str, str]`


Parses a session_event path into its component segments.

### parse_session_path

`parse_session_path(path: str) -> typing.Dict[str, str]`


Parses a session path into its component segments.

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

### session_event_path

```
session_event_path(
project: str, location: str, reasoning_engine: str, session: str, event: str
) -> str
```


Returns a fully-qualified session_event string.

### session_path

```
session_path(
project: str, location: str, reasoning_engine: str, session: str
) -> str
```


Returns a fully-qualified session string.

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

### update_session

```
update_session(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.session_service.UpdateSessionRequest,
dict,
]
] = None,
*,
session: typing.Optional[
google.cloud.aiplatform_v1beta1.types.session.Session
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
) -> google.cloud.aiplatform_v1beta1.types.session.Session
```


Updates the specific xref_Session.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_session():
# Create a client
client = aiplatform_v1beta1.
```[SessionServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html)()
# Initialize request argument(s)
session = aiplatform_v1beta1.[Session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session.html)()
session.user_id = "user_id_value"
request = aiplatform_v1beta1.[UpdateSessionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSessionRequest.html)(
session=session,
)
# Make the request
response = client.[update_session](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient.html#google_cloud_aiplatform_v1beta1_services_session_service_SessionServiceClient_update_session)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for SessionService.UpdateSession. |
`session` |
Required. The session to update. Format: |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Field mask is used to control which fields get updated. If the mask is not present, all fields will be updated. This corresponds to the |
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
A session contains a set of actions between users and Vertex agents. |

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmemory_bank_servicememorybankserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient -->

# Class MemoryBankServiceClient (1.134.0)

```
MemoryBankServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.memory_bank_service.transports.base.MemoryBankServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.memory_bank_service.transports.base.MemoryBankServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing memories for LLM applications.

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
`MemoryBankServiceTransport` |
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

### MemoryBankServiceClient

```
MemoryBankServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.memory_bank_service.transports.base.MemoryBankServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.memory_bank_service.transports.base.MemoryBankServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the memory bank service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MemoryBankServiceTransport,Callable[..., MemoryBankServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MemoryBankServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_memory

```
create_memory(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.CreateMemoryRequest,
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
) -> google.api_core.operation.Operation
```


Create a Memory.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
memory = aiplatform_v1beta1.[Memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory.html)()
memory.fact = "fact_value"
request = aiplatform_v1beta1.[CreateMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMemoryRequest.html)(
parent="parent_value",
memory=memory,
)
# Make the request
operation = client.[create_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_create_memory)(request=request)
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
The request object. Request message for MemoryBankService.CreateMemory. |
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

### delete_memory

```
delete_memory(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.DeleteMemoryRequest,
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


Delete a Memory.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMemoryRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_delete_memory)(request=request)
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
The request object. Request message for MemoryBankService.DeleteMemory. |
`name` |
`str`
Required. The resource name of the Memory to delete. Format: |
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
`MemoryBankServiceClient` |
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
`MemoryBankServiceClient` |
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
`MemoryBankServiceClient` |
The constructed client. |

### generate_memories

```
generate_memories(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.GenerateMemoriesRequest,
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
) -> google.api_core.operation.Operation
```


Generate memories.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_generate_memories():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
vertex_session_source = aiplatform_v1beta1.[VertexSessionSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.VertexSessionSource.html)()
vertex_session_source.session = "session_value"
request = aiplatform_v1beta1.[GenerateMemoriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.html)(
vertex_session_source=vertex_session_source,
parent="parent_value",
)
# Make the request
operation = client.[generate_memories](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_generate_memories)(request=request)
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
The request object. Request message for MemoryBankService.GenerateMemories. |
`parent` |
`str`
Required. The resource name of the ReasoningEngine to generate memories for. Format: |
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

### get_memory

```
get_memory(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.GetMemoryRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.memory_bank.Memory
```


Get a Memory.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetMemoryRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_get_memory)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MemoryBankService.GetMemory. |
`name` |
`str`
Required. The resource name of the Memory. Format: |
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
A memory. |

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

### list_memories

```
list_memories(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
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
google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesPager
)
```


List Memories.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_memories():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListMemoriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_memories](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_list_memories)(request=request)
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
The request object. Request message for MemoryBankService.ListMemories. |
`parent` |
`str`
Required. The resource name of the ReasoningEngine to list the Memories under. Format: |
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
Response message for MemoryBankService.ListMemories. Iterating over this object will yield results and resolve additional pages automatically. |

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

### memory_path

`memory_path(project: str, location: str, reasoning_engine: str, memory: str) -> str`


Returns a fully-qualified memory string.

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

### parse_memory_path

`parse_memory_path(path: str) -> typing.Dict[str, str]`


Parses a memory path into its component segments.

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### parse_session_path

`parse_session_path(path: str) -> typing.Dict[str, str]`


Parses a session path into its component segments.

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

### retrieve_memories

```
retrieve_memories(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.RetrieveMemoriesRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.memory_bank_service.RetrieveMemoriesResponse
```


Retrieve memories.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_retrieve_memories():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
similarity_search_params = aiplatform_v1beta1.[SimilaritySearchParams](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest.SimilaritySearchParams.html)()
similarity_search_params.search_query = "search_query_value"
request = aiplatform_v1beta1.[RetrieveMemoriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest.html)(
similarity_search_params=similarity_search_params,
parent="parent_value",
)
# Make the request
response = client.[retrieve_memories](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_retrieve_memories)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MemoryBankService.RetrieveMemories. |
`parent` |
`str`
Required. The resource name of the ReasoningEngine to retrieve memories from. Format: |
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
Response message for MemoryBankService.RetrieveMemories. |

### session_path

```
session_path(
project: str, location: str, reasoning_engine: str, session: str
) -> str
```


Returns a fully-qualified session string.

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

### update_memory

```
update_memory(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.UpdateMemoryRequest,
dict,
]
] = None,
*,
memory: typing.Optional[
google.cloud.aiplatform_v1beta1.types.memory_bank.Memory
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


Update a Memory.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_memory():
# Create a client
client = aiplatform_v1beta1.
```[MemoryBankServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html)()
# Initialize request argument(s)
memory = aiplatform_v1beta1.[Memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Memory.html)()
memory.fact = "fact_value"
request = aiplatform_v1beta1.[UpdateMemoryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateMemoryRequest.html)(
memory=memory,
)
# Make the request
operation = client.[update_memory](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient.html#google_cloud_aiplatform_v1beta1_services_memory_bank_service_MemoryBankServiceClient_update_memory)(request=request)
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
The request object. Request message for MemoryBankService.UpdateMemory. |
`memory` |
Required. The Memory which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to update. Supported fields: :: * |
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
